---
title: "MARS: What Retrieval Signals Are Hidden in Multimodal Large Language Models for Text-Video Retrieval?"
authors: "Uicheol Jung, Juyoung Hong, Geuntaek Lim, Yukyung Choi"
Year: '2026'
Url: "https://arxiv.org/abs/2609.02565"
ZoteroLink: "[PDF](zotero://select/library/items/ZGZ9GKLB)"
tags:
---
### Tags
#Text-Video #MLLM

### General Notes & Main Standalone Notes
#### Main Standalone Note 1
- MARS
    
    - Multi-layer Adaptive Representation Slots
    - constructs each slot by fusing hidden states from multiple decoder layers with slot-specific layer weights
    - different slots can emphasize different layerwise evidence instead of compressing all information into one global vector
    - preserves complementary cues through multiple adaptive representation slots
    - compares corresponding slots before aggregating their similarities
    - introduces a hard negative-aware slot specialization loss and a diversity loss to encourage slots to capture distinct matching signals

# Problem

- given batch of paired texts and videos $B=\{(t_i, v_i)\}_{i=1}^B$, text-video retrieval aims to assign higher similarity scores to matched text-video pairs than to mismatched pairs
- denote similarity between text $t_i$ and video $v_j$ by $S[i,j]$, forming a score matrix $S \in \mathbb R^{B\times B}$, where rows correspond to texts and columns correspond to videos
- let $a \ in \{t, v\}$ denote the query side, with $S^t=S$ for text-to-video retrieval and $S^v = S^T$ for video-to-text retrieval

# MARS

- **Representation token prompting**
    
    - chat-formatted prompt for each input and place $M$ learnable adaptive representation tokens in the model response field, where each token corresponds to one adaptive representation slot
    - adaptive representation tokens are shared across text and video inputs
        
        - $\{e_m^{slot}\}_{m=1}^M$, where $e_m^{slot}\in \mathbb R^D$
    - MLLM follows causal attention, so use the hidden states immediately preceding the adaptive representation tokens as slot representations
        
        - let $\textbf h_{i,m,t}^{(h)}, \textbf h_{j,m,v}^{(n)}\in \mathbb R^D$ denote the hidden states from the $n$-th decoder layer for the $m$-th slot of text sample $i$ and video sample $j$
- **Multi-layer adaptive slot construction**
    
    - to construct each slot from hidden states across multiple decoder layers, apply slot-wise weighted layer fusion
        
        - for the $m$-th slot, we use a learnable vector $\textbf w_m \in \mathbb R^N$ to assign weights to different decoder layers
        - normalized layer weight $\alpha_{m,n}$ is computed as $\alpha_{m,n} = \frac{exp(w_{m,n})}{\sum_{n’=1}^N exp(w_{m,n’})}$
    - hidden states from different layers are then fused to obtain the text and video slot embeddings
        
        - $\textbf z_{i,m}^t = \sum_{n=1}^N \alpha_{m,n}\textbf h_{i,m,t}^{(n)}, \; \textbf z_{j,m}^v = \sum_{n=1}^N \alpha_{m,n}\textbf h_{j,m,v}^{(n)}$
        - apply $L_2$-normalisation to each slot embedding, denoted $\hat z$
- **Slot-wise matching**
    
    - comparison of the normalized text and video slot embeddings in a slot-aligned manner
        
        - for the $m$-th slot compute the slot-wise cosine similarity matrix
        - $S_m[i,j]=\langle \hat z_{i,m}^t, \hat z_{j,m}^v\rangle$
            
            - $S_m^t=S_m$ and $S_m^v = S_m^\top$
    - aggregate slot-wise similarities across $M$ slots for similarity score
        
        - $S[i,j]=\sum_ {m=1}^M \beta _m S_m [i,j]$
            
            - slot weights $\beta _m = 1/M$  
- **Hard-negative-aware slot specialization**
    
    - hard negatives commonly used to strengthen cross-modal alignment by providing confusing mismatched samples
    - for each query side $a \in \{t,v\}$ we select the hardest negative using the corresponding score matrix
        
        - $j_a^*(i)=\arg \ max_{j\neq i}S^a[i,j]$
        - _Assumption_: This is during training they know which samples are negative and using the score they can therefore find the hardest negative
    - Slot-wise positive-negative gap
        
        - $\Delta_m^a(i) = S_m^a[i,i]-S_m^a[i,j_a^*(i)]$
        - measures how much the positive pair is separated from the selected hard negative at slot $m$  
    - take the largest slot-wise gap across slots
        
        - $gap^a(i) = \max_{1\leq m\leq M}\Delta_m^a(i)$
        - selects the most discriminative slot for each hard negative
    - Query-side hinge loss
        
        - $\mathcal L_{hn}^a=\frac 1 B \sum_{i=1}^B \max(0,\delta - gap^a(i))$
            
            - $\delta$ is the margin
            - when gap smaller than $\delta$ this promotes a larger separation between the positive pair and the selected hard negative
    - final hard-negative-aware slot specialization loss is obtained by averaging the text and video query sides
        
        - $\mathcal L_{hn} = \frac 1 2 \sum_{a\in\{t,v\}}\mathcal L_{hn}^a$  

# Training Objective

- three objectives
    
    - symmetric contrastive alignment
        
        - $\mathcal L_{NCE}^a = -\frac 1 B \sum_{i=1}^B \log \frac{exp(\gamma S ^a[i,i])}{\sum_{j=1}^B exp(\gamma S^a[i,j])}$
        - $\mathcal L_{NCE}=\frac 1 2 \sum_{a\in \{t,v\}}\mathcal L _{NCE} ^a$
            
            - $\gamma$ is a scaling factor
    - slot diversity regularizaton
        
        - since multiple slots are extracted from the same input, different slots can become redundant
        - apply a squared cosine similarity regularizer within each side
            
            - $\mathcal L_{div}^a = \frac 1 {BM(M-1)} \sum_{i=1}^B \sum_{m\neq m’}[(\hat z_{i,m}^a)^{\top} \hat z_{i,m’}^a]^2$
            - $\mathcal L_{div} = \frac 1 2 \sum_{a\in\{t,v\}}\mathcal L_{div}^a$
    - hard-negative-aware slot specialization
- Together the final training objective
    
    - $\mathcal L = \mathcal L_{NCE} + \lambda_{div}\mathcal L_{div} + \lambda_{hn}\mathcal L_{hn}$
        
        - $\lambda_{div}$ and $\lambda_{hn}$ are loss weights

# Questions

- is a [[hard negative]] a hard to confirm negative or an obvious solid negative?
    
    - training example that belongs to a different class than your target (a negative sample), but is so similar or confusable with the target that the model easily mistakes it for a positive one



### PDF Annotations & Text Highlights
- **Highlight:** "MARS (Multi-layer Adaptive Representation Slots)." [(Page 2)](zotero://open-pdf/library/items/ZGZ9GKLB?page=2&annotation=SGEJ2Y24)
  
- **Highlight:** "adapted MLLMs into multimodal embedders through prompt-based extraction" [(Page 2)](zotero://open-pdf/library/items/ZGZ9GKLB?page=2&annotation=G4NJG37F)
  
- **Highlight:** "approaches predominantly derive the embedding from a single token" [(Page 2)](zotero://open-pdf/library/items/ZGZ9GKLB?page=2&annotation=9C7MMXD9)
  
- **Highlight:** "ingle-token extraction fails to fully exploit the multi-layered representations within MLLMs" [(Page 2)](zotero://open-pdf/library/items/ZGZ9GKLB?page=2&annotation=CPPYERX6)
  

- **Highlight:** "MLLM follows causal attention" [(Page 3)](zotero://open-pdf/library/items/ZGZ9GKLB?page=3&annotation=ZLHKDDP5)
  
- **Highlight:** "Hard negatives are commonly used to strengthen cross-modal alignment by providing confusing mismatched samples" [(Page 4)](zotero://open-pdf/library/items/ZGZ9GKLB?page=4&annotation=QZV474WU)
  



- **Highlight:** "MARS is evaluated across multiple established text-video retrieval benchmarks, these datasets may not fully reflect opendomain scenarios involving substantially longer videos, noisy descriptions, or diverse user queries" [(Page 10)](zotero://open-pdf/library/items/ZGZ9GKLB?page=10&annotation=NLVKVJBK)
  
- **Highlight:** "study focuses on video-level retrieval and does not explicitly address temporal grounding or moment-level retrieval" [(Page 10)](zotero://open-pdf/library/items/ZGZ9GKLB?page=10&annotation=J74AWEMJ)
  


### Images

![[PhD/Sources/Images/JungMARSWhat2026/image-3-x62-y472.png]]![[PhD/Sources/Images/JungMARSWhat2026/image-5-x64-y585.png]]![[PhD/Sources/Images/JungMARSWhat2026/image-5-x66-y465.png]]![[PhD/Sources/Images/JungMARSWhat2026/image-5-x314-y465.png]]