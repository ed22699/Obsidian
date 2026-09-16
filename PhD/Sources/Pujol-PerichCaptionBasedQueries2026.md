---
title: "Beyond Caption-Based Queries for Video Moment Retrieval"
authors: "David Pujol-Perich, Albert Clapés, Dima Damen, Sergio Escalera, Michael Wray"
Year: '2026'
Url: "https://arxiv.org/abs/2603.02363"
ZoteroLink: "[PDF](zotero://select/library/items/7C5KIEAU)"
tags:
---
### Tags
#VMR

### General Notes & Main Standalone Notes
#### Main Standalone Note 1
# Problem

- Given video-query pair $(v_i,q_i)$ the task is to predict the start-end times $\{(s_j,e_j)\}_{j=1}^M$ of all temporal segments in $v_i$ corresponding to the textural query $q_i$
    
    - i.e. moments
- looking at how the textual queries are defined
    
    - _captioning annotations_: annotators typically watch the videos before writing a sentence to describe the moment - brings visual bias
    - _search queries_ are a lot less specific

# Dataset

- Use two LLMs
    
    - a rewriter which simplifies captions whilst keeping core semantics
    - a verify that checks the underlying meaning is still correct
- has various levels of simplification in the HD-EPIC dataset - S1, S2, S3
- As multiple instances that can fall under the same moment, recall and mean Average Precision (mAP) are as follows
    
    - Recall
        
        - $g_i$ correct if under a certain IOU threshold $\tau(R_m(g_i, \tau) = 1$ if
            
            - prediction detecting had highest confidence, or
            - predictions with higher confidences successfully retrieved other GT moments
        - $R_m(\tau) = \frac 1 {|\mathcal G|}\sum_{g_i \in \mathcal G} R_m(g_i, \tau)$
    - mAP
        
        - evaluated each GT individually. For a given $g_i$ and threshold $\tau$
            
            - predictions intersecting $g_i$ with $IOU \geq \tau$ considered true positives
            - predictions not matching any GT are considered false positives
            - predictions matching other GT moments (not $g_i$) are ignored to avoid penalizing $g_i$ for different, yet correct, prediction
        - $mAP_m(\tau) = \frac 1 {|\mathcal G|} \sum_{g_i \in \mathcal G} AP_m(g_i, \tau)$

# Evaluation

- search queries partitioned into two subsets
    
    - $\mathcal D_{single}^{search}$ - under-specified queries that map to a single GT
    - $\mathcal D_{multi}^{search}$ - under-specified queries that map to multiple GT moments
    - partitioning also occurs for the original caption-based dataset
- Struggles with multi-moment queries at inference time
    
    - number of active decoder queries can be thought as the “compute budget” available to retrieve all the GT moments
    - if only 2 queries are activated in a 4-moment instance, the upper bound of retrieved moments is 50%
    - **active decoder-query collapse**
        
        - can be mitigated by preventing models from overfitting to the single-moment prior encoded in the training data
        - two structural causes
            
            - coordination collapse
                
                - arises from how the self-attention within each decoder layer enforces coordination among decoder queries
                - drives them to agree on which query should handle the GT moment and which should remain inactive
                - standard decoder layer defined:
                    
                    - $\hat Q^{l+1} = FFN(CA(SA(\hat Q^l),M))$
                    - where $M\in \mathbb R^{T\times F}$ are the fused multi-modal features
                    - CA denotes gross-attention
                    - FFN a feed-forward network
                    - SA is self attention
                - CA module injects the cross-modality information, SA pushes decoder queries apart from each other to avoid redundancy
                    
                    - _issue_: also drives the majority of decoder queries to deactivate
                    - _solution_: remove this SA module while leaving the losses unchanged
                        
                        - $Q^{l+1} = FFN(CA(Q^l,M))$
                        - removal of inter-query communication prevents the coordination-based shortcuts, encouraging each decoder query to act independently
                        - _issue_: also removes model’s built-in mechanism for avoiding redundant predictions
                        - _solution_: apply non-maximal suppression (NMS) during post-processing, filtering out overlapping/redundant predictions
            - index collapse
                
                - mitigating the coordination collapse the model is still able to overfit to the single-moment prior so still suffers active decoder-query collapse, the issue being an index collapse
                    
                    - same decoder query indices repeatedly dominate the output confidence, while the rest remain inactive
                - _solution_: apply targeted query dropout strategy
                    
                    - randomly zeroes out $k\%$ of learnable queries $Q\in \mathbb R^{Q\times F}$ during each training iteration
                    - $\hat Q = Q \odot M, \; M\sim \mathbb B(1-k)$
                        
                        - $\mathbb B$ is sampling from the Bernoulli distribution with keep probability $(1-k)$
                    - the regularization promotes the model to distribute supervision across more queries, preventing over-reliance on a fixed subset



### PDF Annotations & Text Highlights
- **Highlight:** "captions, which are written by annotators after watching the videos" [(Page )](zotero://open-pdf/library/items/7C5KIEAU?page=&annotation=KAMVWW9I)
  
- **Highlight:** "This annotation process induces a visual bias, leading to overly descriptive and fine-grained queries" [(Page )](zotero://open-pdf/library/items/7C5KIEAU?page=&annotation=82TMLP52)
  
- **Highlight:** "These captions, which we name caption-based queries, induce a visual bias—overly descriptive visuallyinformed textual annotations" [(Page )](zotero://open-pdf/library/items/7C5KIEAU?page=&annotation=ZFLD9A3Y)
  
- **Highlight:** "a language gap" [(Page 2)](zotero://open-pdf/library/items/7C5KIEAU?page=2&annotation=8BQGPFHT)
  
- **Highlight:** "multi-moment gap" [(Page 2)](zotero://open-pdf/library/items/7C5KIEAU?page=2&annotation=5XYMW52D)
  
- **Highlight:** "proposal-based and proposal-free methods" [(Page 2)](zotero://open-pdf/library/items/7C5KIEAU?page=2&annotation=NPCMQUIN)
  
- **Highlight:** "Proposal-based approaches generate candidate temporal segments through temporal anchors [3," [(Page 2)](zotero://open-pdf/library/items/7C5KIEAU?page=2&annotation=7GGDKS98)
  
- **Highlight:** "14," [(Page 2)](zotero://open-pdf/library/items/7C5KIEAU?page=2&annotation=T2PR3P94)
  
- **Highlight:** "sliding-windows [1, 7]" [(Page 2)](zotero://open-pdf/library/items/7C5KIEAU?page=2&annotation=EBGG2SNA)
  
- **Highlight:** "proposal-free" [(Page 2)](zotero://open-pdf/library/items/7C5KIEAU?page=2&annotation=F2LX5MET)
  
- **Highlight:** "these works adopt DETR-based architectures [6]" [(Page 2)](zotero://open-pdf/library/items/7C5KIEAU?page=2&annotation=KAXC3MDB)
  
- **Highlight:** "aradigm was introduced by [20]," [(Page 2)](zotero://open-pdf/library/items/7C5KIEAU?page=2&annotation=FC9YIWA4)
  
- **Highlight:** "follow-ups like [29, 30, 50]" [(Page 2)](zotero://open-pdf/library/items/7C5KIEAU?page=2&annotation=LFC2B8Q3)
  
- **Highlight:** "recent studies have begun exploring the role of language biases in generalization [23, 26]" [(Page 2)](zotero://open-pdf/library/items/7C5KIEAU?page=2&annotation=PL9839Y2)
  
- **Highlight:** "we generate underspecified queries from fine-grained ones through an LLMbased pipeline" [(Page 3)](zotero://open-pdf/library/items/7C5KIEAU?page=3&annotation=MG262CQR)
  
- **Highlight:** "rewriter agent receives a fine-grained caption and rewrites it into a less detailed version while preserving the core semantics." [(Page 3)](zotero://open-pdf/library/items/7C5KIEAU?page=3&annotation=UZCIA4QA)
  
- **Highlight:** "Queries with a high similarity are merged into the same group, forming a multimoment instance." [(Page 3)](zotero://open-pdf/library/items/7C5KIEAU?page=3&annotation=FC59VYK2)
  
- **Highlight:** "The proposed search-query pipeline enables us to introduce three search-query benchmarks, denoted by “-S”" [(Page 3)](zotero://open-pdf/library/items/7C5KIEAU?page=3&annotation=QRDC4H6Z)
  
- **Highlight:** "we derive three progressively under-specified variants—i.e., S1, S2, S3—by gradually removing contextual details." [(Page 3)](zotero://open-pdf/library/items/7C5KIEAU?page=3&annotation=JP9M9KXV)
  

- **Highlight:** "mean Average Precision (mAP)" [(Page 4)](zotero://open-pdf/library/items/7C5KIEAU?page=4&annotation=6W99ZPG2)
  
- **Highlight:** "we consider a given moment gi to be correctly retrieved under a certain IOU threshold τ (Rm(gi, τ ) = 1), if 1) the prediction detecting it had the highest confidence, or 2) all the predictions with higher confidences successfully retrieved other GT moments" [(Page 4)](zotero://open-pdf/library/items/7C5KIEAU?page=4&annotation=JIXYNUKF)
  
- **Highlight:** "predictions intersecting gi with IOU≥ τ are considered true positives" [(Page 4)](zotero://open-pdf/library/items/7C5KIEAU?page=4&annotation=5BBGISHR)
  
- **Highlight:** "redictions not matching any GT are considered false positives" [(Page 4)](zotero://open-pdf/library/items/7C5KIEAU?page=4&annotation=FDSBI2IU)
  
- **Highlight:** "redictions matching other GT moments (not gi) are ignored to avoid penalizing gi for a different, yet correct, prediction" [(Page 4)](zotero://open-pdf/library/items/7C5KIEAU?page=4&annotation=MLT759AM)
  
- **Highlight:** "we evaluate two representative models—i.e., CG-DETR [29] and LD-DETR [50]" [(Page 5)](zotero://open-pdf/library/items/7C5KIEAU?page=5&annotation=HZUY6UGR)
  

- **Highlight:** "degradation mostly stems from misalignment between caption-based training datacharacterized by a single relevant moment as GT—and search-based evaluation data, which frequently contains multiple valid moments." [(Page 5)](zotero://open-pdf/library/items/7C5KIEAU?page=5&annotation=VX22GACH)
  
- **Highlight:** "bias towards expecting a single GT moment" [(Page 5)](zotero://open-pdf/library/items/7C5KIEAU?page=5&annotation=AMZBSDYG)
  

- **Highlight:** "In VMR, the number of active decoder queries can also be thought as the “compute budget” available to retrieve all the GT moments" [(Page 6)](zotero://open-pdf/library/items/7C5KIEAU?page=6&annotation=WASMEF8F)
  
- **Highlight:** "when only 2 queries are activated in a 4-moment instance, the upper bound of retrieved moments is 50%. We term this phenomenon active decoder-query collapse." [(Page 6)](zotero://open-pdf/library/items/7C5KIEAU?page=6&annotation=XAF5FD86)
  
- **Highlight:** "possible by preventing models from overfitting to the single-moment prior encoded in the training data" [(Page 6)](zotero://open-pdf/library/items/7C5KIEAU?page=6&annotation=TKJZN7JU)
  
- **Highlight:** "resulting in a consistent increase in the number of active decoder queries" [(Page 6)](zotero://open-pdf/library/items/7C5KIEAU?page=6&annotation=L45BTEZG)
  
- **Highlight:** "(-SA+QD), substantially improve performance across all search-query datasets" [(Page 7)](zotero://open-pdf/library/items/7C5KIEAU?page=7&annotation=7Q24XCIK)
  

- **Highlight:** "results confirm that merely increasing the number of active queries through additional supervision is insufficient; effective generalization to multi-moment setups also requires diversity-promoting mechanisms that encourage complementary behavior in decoder querie" [(Page 7)](zotero://open-pdf/library/items/7C5KIEAU?page=7&annotation=32WWQ3Q2)
  



### Images

![[PhD/Sources/Images/Pujol-PerichCaptionBasedQueries2026/image-4-x51-y599.png]]![[PhD/Sources/Images/Pujol-PerichCaptionBasedQueries2026/image-5-x311-y509.png]]![[PhD/Sources/Images/Pujol-PerichCaptionBasedQueries2026/image-6-x51-y596.png]]![[PhD/Sources/Images/Pujol-PerichCaptionBasedQueries2026/image-7-x311-y596.png]]![[PhD/Sources/Images/Pujol-PerichCaptionBasedQueries2026/image-8-x312-y416.png]]