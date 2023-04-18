# Pre-train, Prompt, and Predict: A Systematic Survey of
Prompting Methods in Natural Language Processing

# 1 Two sea changes in NLP

**Fully Supervised Learning** played a central role in NLP

> a task-specific model is trained solely on a dataset of input-output examples for the target task
> 

其发展经历了以下四个阶段：

1. Feature engineering (Non-neural Network)
    
    > NLP researchers or engineers used their domain knowledge to define and extract salient features from raw data and provide models with the appropriate inductive bias to learn from this limited data.
    > 
2. Architecture engineering (Neural Network)
    
    > Inductive bias was rather provided through the design of a suitable network architecture conducive to learning such features
    > 
3. Objective engineering (Pre-train, Fine-tune) **Sea change 1**
    
    > A model with a fixed architecture is pre-trained as a language model (LM). LM will be adapted to different downstream tasks by introducing additional parameters and fine-tuning them using task-specific objective functions.
    > 
    
    Object engineering的原因：goal is designing the training objectives used at both the pre-training and fine-tuning stages.
    
4. Prompt engineering (Pre-train, Prompt, Predict)  **We are in the middle of Sea change 2**
    
    > downstream tasks are reformulated to look more like those solved during the original LM training with the help of a textual prompt
    > 
