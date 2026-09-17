---
title: "Moment of Untruth: Dealing with Negative Queries in Video Moment Retrieval"
authors: "Kevin Flanagan, Dima Damen, Michael Wray"
Year: 'Error: `format` can only be applied to dates. Tried for format object'
Url: ""
ZoteroLink: "[PDF](zotero://select/library/items/BAHUW2X9)"
tags:
---
### Tags
#VMR #Moment-DETR 

### General Notes & Main Standalone Notes
#### Main Standalone Note 1
# Task

- For each video $V_i$ within a corpus, there exists a set of query sentences $q_{i,j}$ with corresponding moments given as start $t_{i,j}^s$ and end $t_{i,j}^e$ times
- collectively describe this as the set of queries for video $V_i: Q_i = \{(q_{i,j},t_{i,j}^s, t_{i,j}^e)\}$
- during training, models learn to predict the start/end times of a moment given the corresponding query sentence for the $i$-th video
- _issue_: at inference time, methods are evaluated on their ability to correctly localise the query sentence $q_{i,j}$ which is always assumed to be contained within video $V_i$
    
    - methods rank and select the highest proposal/predicted moment $(\tilde t_{i,j}^s, \tilde t_{i,j}^e)$ and compare this to the ground truth moment $(t_{i,j}^s, t_{i,j}^e)$ directly during evaluation
    - make assumption that all query sentences $q_{i,j}$, positive or negative, are relevant and contained within a video $V_i$

# Data

- **In-Domain (ID)**
    
    - allow for the inspection of a model’s ability to differentiate specific details in videos
    - feasible events that do not occur in a given video
    - collected by shuffling video-sentence pairs within dataset
        
        - to get similarity scores between query sentence $q_k$ and video $V_i$, calculate the cosine similarity between $q_k\notin Q_i$ and each $q_{i,j} \in Q_i$ and take the maximum of those similarity scores to be the sentence-video pseudo-similarity score
        - each sentence is assigned to a video whose video-sentence similarity score is in the lowest 50th percentile for that sentence
            
            - reduces the chance that the new assignment actually contains that moment
- **Out-of-Domain (OOD)**
    
    - enable the inspection of a model’s ability to recognize that a query is entirely irrelevant to the scenario
    - queries which belong to an entirely different scenario to the selected video and are extremely unlikely to be present within it
    - generated via LLM
        
        - extremely unlikely scenarios are selected specific to dataset

# VMR Methods

- many based on Moment-DETR
- utilize **frozen video and text encoders** followed by a **projection layer** to match dimentionality
    
    - produces video features $\textbf V = \{v_c\}_{c=1}^{L_v}$
        
        - $L_v$ is the number of video clips
    - produces text features $\textbf Q = \{q_w\}{w=1}^{L_q}$  
        
        - $L_q$ is the number of query sentence tokens
- typically pass these video and text features into a **Transformer encoder** to produce text-attended video tokens
- common to use **Transformer decoder** with $M$ trainable position embeddings (moment queries) as input alongside the text-attended video tokens
    
    - produces $M$ final video representations
        
        - may be used as input to the heads
- Use three **prediction heads**
    
    - foreground matching head
        
        - produces the indicator scores $\tilde f_m$, where $m$ is the index of the candidate moment predictions
        - typically produces by set of feed forward layers and an activation function on top of the $M$ video representations
        - aim to predict likelihood of the moment matching the query
    - boundary prediction head
        
        - predicts the moment boundaries $\tilde d_m$
        - two outputs
            
            - either start/end time offsets
            - or moment centre and width
    - saliency head
        
        - predicts [[saliency scores]] $\tilde s_c$, where $c$ is the clip index
        - input to head is typically the output of the video encoder or earlier representations
        - scores used only for the [[highlight detection]] task - aims to detect text-guided highlights for a given video

# Negative-Aware Video Moment Retrieval (NA-VMR)

- outputs tuple $(\tilde y, \tilde t^s, \tilde t ^e)$ containing
    
    - prediction score, $\tilde y$
        
        - if $\tilde y = 0$ then timestamps are considered invalid and rejected
        - if $\tilde y = 1$ then times are considered valid and compared to the ground truth moments as normal
    - predicted start/end times $\tilde t^s$ and $\tilde t^e$
- for training both positive and negative queries need to be utilised
    
    - $Q_i^+=\{(y_{i,j} = 1, q_{i,j},t_{i,j}^s, t_{i,j}^e)\}$
    - $Q_i^- = \{(y_{i,j} = 0, q_{i,k})\}$
- uses an alteration of the Moment-DETR methods
    
    - generated negative queries are used to train the model to differentiate between positive and negative video-sentence pairs, enabling Negative-Aware Video Moment Retrieval
    - add binary classification head on top of the base Video Moment Retrieval model which classifies queries as positive or negative
        
        - Indicator score and saliency score predictions are combined and passed into a recurrent (RNN) layer
            
            - indicator score denotes the likelihood of the moment matching the query
            - saliency scores are much more discriminative between positive and negative
            - RNN maintains the temporal knowledge within the features while handling variable video lengths
        - RNN output at final step is passed into feed-forward layer (MLP) and a sigmoid activation function to produce the final prediction score, $\tilde y$
        - $\tilde y = \sigma (MLP(RNN(\tilde f \oplus \tilde s)))$
- **Losses**
    
    - binary cross entropy loss is applied to the classification head output
        
        - positive queries take ground truth value of $y=1$
        - negative queries GT value of $y=0$
        - $\mathcal L_p = \lambda _p(y\log \tilde y + (1-y)\log(1-\tilde y))$
            
            - $\tilde y$ is the output prediction from classification head
            - $\lambda _p$ is the loss weighting
    - typically methods utilise
        
        - foreground matching head loss $\mathcal L_f$ on the indicator scores
        - boundary loss $\mathcal L b$ across the start/end times
        - saliency loss $\mathcal L_s$ applied to the saliency scores
    - for positive queries losses can be applied as normal
        
        - negative queries are adapted
            
            - $\mathcal L_b$ set to 0 as no ground truth boundary to predict
            - all ground truth values for the indicator and saliency scores are set to 0 for $\mathcal L_f$ and $\mathcal L_s$
            - may need to be adjusted if for example they involve contrastive losses
    - $\mathcal L^+ = \mathcal L_f + \mathcal L_b +\mathcal L_s + \mathcal L_p$      $\mathcal L^- = \mathcal L_f^-+\mathcal L_s^-+\mathcal L_p$  
    - $\mathcal L_{tot}$ is the weighted sum of the losses for positives, ID negativees and OOD negatives
        
        - $\mathcal L_{tot} = \lambda^+\mathcal L^+ +\lambda _{ID}^- \mathcal L_{ID}^- + \lambda_{OOD}^- \mathcal L_{OOD}^-$



### PDF Annotations & Text Highlights
- **Highlight:** "current task formulation assumes that the queried moment is present in the video, resulting in false positive moment predictions when irrelevant query sentences are provided." [(Page )](zotero://open-pdf/library/items/BAHUW2X9?page=&annotation=A54736B3)
  
- **Highlight:** "highlight examples of In-Domain (ID) and Out-Of-Domain (OOD) negatives" [(Page 2)](zotero://open-pdf/library/items/BAHUW2X9?page=2&annotation=LNX7PESB)
  
- **Highlight:** "We train the model with both ID and OOD negatives, showing both are necessary." [(Page 2)](zotero://open-pdf/library/items/BAHUW2X9?page=2&annotation=EJINS4PA)
  
- **Highlight:** "introduced in [1, 12]," [(Page 2)](zotero://open-pdf/library/items/BAHUW2X9?page=2&annotation=9EQ9T9YC)
  
- **Highlight:** "proposalbased" [(Page 2)](zotero://open-pdf/library/items/BAHUW2X9?page=2&annotation=BNPHWBAD)
  
- **Highlight:** "proposalfree methods" [(Page 2)](zotero://open-pdf/library/items/BAHUW2X9?page=2&annotation=B2V7B43M)
  
- **Highlight:** "21]," [(Page 2)](zotero://open-pdf/library/items/BAHUW2X9?page=2&annotation=B7WW6BFX)
  
- **Highlight:** "Moment-DETR [21]" [(Page 2)](zotero://open-pdf/library/items/BAHUW2X9?page=2&annotation=STIRDDKU)
  
- **Highlight:** "DEtection TRansformer (DETR) [3]" [(Page 2)](zotero://open-pdf/library/items/BAHUW2X9?page=2&annotation=57XK98WA)
  
- **Highlight:** "Despite progress in moment retrieval performance, all methods assume queries at inference are always positive." [(Page 2)](zotero://open-pdf/library/items/BAHUW2X9?page=2&annotation=IIFSQ4DK)
  
- **Highlight:** "ideo Corpus Moment Retrieval" [(Page 2)](zotero://open-pdf/library/items/BAHUW2X9?page=2&annotation=LHBKBEZ6)
  
- **Highlight:** "Video Corpus Moment Retrieval (VCMR) [10, 17, 22, 47]" [(Page 2)](zotero://open-pdf/library/items/BAHUW2X9?page=2&annotation=IBDHWNH5)
  
- **Highlight:** "VCMR works under the assumption that the query is present in exactly one video in the corpus" [(Page 3)](zotero://open-pdf/library/items/BAHUW2X9?page=3&annotation=XMQA2AU4)
  
- **Highlight:** "no active scheme to determine negatives" [(Page 3)](zotero://open-pdf/library/items/BAHUW2X9?page=3&annotation=DPXUP5QQ)
  
- **Highlight:** "lighted [5]" [(Page 3)](zotero://open-pdf/library/items/BAHUW2X9?page=3&annotation=P5EKWSA6)
  
- **Highlight:** "Negative-Aware Video Moment Retrieval (NA-VMR)" [(Page 3)](zotero://open-pdf/library/items/BAHUW2X9?page=3&annotation=3UAGEVQY)
  
- **Highlight:** "return a moment span only for positive query sentences that are contained within the video" [(Page 3)](zotero://open-pdf/library/items/BAHUW2X9?page=3&annotation=8TBUHYA7)
  

- **Highlight:** "huffling videosentence pairs within the dataset," [(Page 4)](zotero://open-pdf/library/items/BAHUW2X9?page=4&annotation=K99RPF72)
  
- **Highlight:** "get the similarity score between query sentence qk and video Vi, you first calculate the cosine similarity between qk ∈/ Qi and each qi,j ∈ Qi and take the maximum of those similarity scores to be the sentence-video pseudo-similarity score" [(Page 4)](zotero://open-pdf/library/items/BAHUW2X9?page=4&annotation=QRSYI4NQ)
  
- **Highlight:** "for a cooking dataset, the scenario of competitive sport might be chosen" [(Page 4)](zotero://open-pdf/library/items/BAHUW2X9?page=4&annotation=5SAAPE8Q)
  
- **Highlight:** "Moment-DETR [21]." [(Page 4)](zotero://open-pdf/library/items/BAHUW2X9?page=4&annotation=N44YWNZ5)
  
- **Highlight:** "frozen video and text encoders" [(Page 4)](zotero://open-pdf/library/items/BAHUW2X9?page=4&annotation=ZNNYT7CH)
  
- **Highlight:** "followed by a projection layer to match dimensionality" [(Page 4)](zotero://open-pdf/library/items/BAHUW2X9?page=4&annotation=C5MYS76L)
  
- **Highlight:** "pass these video and text features into a Transformer encoder to produce text-attended video tokens" [(Page 4)](zotero://open-pdf/library/items/BAHUW2X9?page=4&annotation=GW4CDFE9)
  
- **Highlight:** "foreground matching head produces the indicator scores" [(Page 4)](zotero://open-pdf/library/items/BAHUW2X9?page=4&annotation=RVZGWWFB)
  
- **Highlight:** "aim to predict the likelihood of the moment matching the query" [(Page 4)](zotero://open-pdf/library/items/BAHUW2X9?page=4&annotation=MU85HRV6)
  
- **Highlight:** "boundary prediction head" [(Page 4)](zotero://open-pdf/library/items/BAHUW2X9?page=4&annotation=3HPT4FF9)
  
- **Highlight:** "saliency head" [(Page 4)](zotero://open-pdf/library/items/BAHUW2X9?page=4&annotation=ZMJFJ3XP)
  

- **Highlight:** "⊕ operation in Equation 1 represents a generic combination." [(Page 5)](zotero://open-pdf/library/items/BAHUW2X9?page=5&annotation=9ZN8MIGP)
  
- **Highlight:** "in our case, a summation of the indicator and saliency scores" [(Page 5)](zotero://open-pdf/library/items/BAHUW2X9?page=5&annotation=PKD45GWV)
  
- **Highlight:** "add an extra classification head on top of the indicator and saliency score predictions." [(Page 5)](zotero://open-pdf/library/items/BAHUW2X9?page=5&annotation=KYJBLQ83)
  
- **Highlight:** "During training, the saliency and indicator scores are set to 0 for the negative queries and the losses are adjusted where necessary" [(Page 5)](zotero://open-pdf/library/items/BAHUW2X9?page=5&annotation=9CQFHXMB)
  
- **Highlight:** "providing both human annotated moment start/end times and saliency" [(Page 5)](zotero://open-pdf/library/items/BAHUW2X9?page=5&annotation=5R8PIRWF)
  
- **Highlight:** "scores for each video-sentence pair" [(Page 6)](zotero://open-pdf/library/items/BAHUW2X9?page=6&annotation=LGFKEWED)
  
- **Highlight:** "Charades-STA is made up of home videos with scripted actions and provides just moment start/end times." [(Page 6)](zotero://open-pdf/library/items/BAHUW2X9?page=6&annotation=ZW7H8AGP)
  
- **Highlight:** "The results show that methods are unable to distinguish between positives and negatives when the indicator score is used. Using saliency scores fares better for QVHighlights, though methods struggle on Charades-STA" [(Page 6)](zotero://open-pdf/library/items/BAHUW2X9?page=6&annotation=UYKXK5PI)
  


- **Highlight:** "there is a trade-off between moment recall scores and negative rejection, this allows the model to be more robust" [(Page 8)](zotero://open-pdf/library/items/BAHUW2X9?page=8&annotation=MQSQ9ZYA)
  
- **Highlight:** "remains a trade-off between localising positive moments and rejecting negative query sentences" [(Page 8)](zotero://open-pdf/library/items/BAHUW2X9?page=8&annotation=UMW5I94W)
  
- **Highlight:** "pseudo-saliency scores used for datasets without ground truth human-annotated saliency scores are not as informative, which results in weaker negative rejection performance particularly in the in-domain case" [(Page 8)](zotero://open-pdf/library/items/BAHUW2X9?page=8&annotation=RJMIR4DE)
  


### Images

![[PhD/Sources/Images/FlanaganMomentUntruth/image-4-x46-y535.png]]![[PhD/Sources/Images/FlanaganMomentUntruth/image-5-x48-y464.png]]![[PhD/Sources/Images/FlanaganMomentUntruth/image-7-x34-y374.png]]![[PhD/Sources/Images/FlanaganMomentUntruth/image-7-x35-y144.png]]