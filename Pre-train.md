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

# 2 A formal description of prompting

**Supervised learning in NLP**

| $x$ | input |
| --- | --- |
| $P(y|x;\theta)$ | model |
| $y$ | output |

In order to learn parameter $\theta$, we use a dataset containing pairs of inputs and outputs.

**Prompting Basics**

supervised learning学习$P(y|x;\theta)$，需要输入输出对作为数据集。

在Prompting learning中，模型model the probability $P(x;\theta)$, and use this probability to predict $y$.

主要包括以下三步：

1. Prompt addition
    
    
    | $x$ | input | I love this movie. |
    | --- | --- | --- |
    | $f_{prompt}(\cdot)$ | prompting function
    [X]: input slot
    [Z]: answer slot, in the middle is a cloze prompt, in the end is a prefix prompt
    the number of [X] and [Z] varies. | [X] Overall, it was a [Z] movie. |
    | $x'=f_{prompt}(x)$ | prompt | I love this movie. Overall, it was a [Z] movie. |
2. Answer search
    
    
    | $z$ | answer | amazing, bad, … |
    | --- | --- | --- |
    | $f_{fill}(x',z)$ | filled prompt | I love this movie. Overall, it was a bad movie. |
    | $f_{fill}(x',z^*)$ | answered prompt | I love this movie. Overall, it was a amazing movie. |
    
    Finally, we search over the set of potential answers z by calculating the probability of their corresponding filled prompts using a pre-trained LM $P(\cdot; θ)$.
    $\hat{z}=search_{z\in Z}P(f_{fill}(x',z);\theta)$
    
    This search function could be an argmax search that searches for the highest-scoring output, or sampling that randomly generates outputs following the probability distribution of the LM.
    
3. Answer mapping