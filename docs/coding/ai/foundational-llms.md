---
title: Foundational Large Language Models and Text Generation
---

# Foundational Large Language Models and Text Generation

## Introduction

An LLM is an advanced AI system.

Specializes in: processing, understanding and generating human-like text

Trained on Massive Text Data

Capabilities:

- Machine Transaltion
- Creative Text Generation
- Question Answering
- Text Summarization
- Resoning Tasks

## Large Language Models

A large Language model **predict the probability of a sequence of words**. 

Modern LLMs are based on Neural Models (Transformers)

They evolved from RNNs (Recurrent neural networks) 

e.g. LSTM (long short-term Memory), GRU (gated recurrent unit)

They were sequential (process input and output sequence sequentially)

As a result, Compute intensive and hard to parallelize

Transformers:

Parallel processing (due to self attention)

Faster to train and easier to parallelize than RNNs, however the cost of self-attention is quadratic in the context length

## Transformers

Developed by Google in (2017)

Explicitly designed as a **"sequence-to-sequence model" **

e.g. convert sequences from one domain into sequences in another domain, such as translating French sentences into English sentence

Which is applied using Encoder and Decoder Structure

### Encoder

Responsible for **processing the input sequence** (e.g., a French sentence<br> It converts the input text into a **continuous representation**, a series of embedding vectors (Z), that holds contextual information for each token.<br>Steps:

| **1. Normalization** | Input text is cleaned—lowercased, punctuation handled, etc. |
| --- | --- |
| **2. Tokenization** | The sentence is split into smaller units called **tokens** (words or subwords). |
| **3. Embedding Conversion** | Each token is mapped to a **vector** (a list of numbers) that captures meaning. |
| **4. Positional Encoding** | Since transformers don’t understand sequence naturally, this adds position info. |
| **5. Self-Attention** | Each token "looks at" others to learn context (Who is important to me?). |
| **6. Feedforward Layers** | Deeper processing through fully connected neural nets. |
| **7. Output = Embedding Z** | The final representations (Z) capture meaning + context for each input token. |

### Encoder’s Layer

1. Muti-head self-attention
2. A position-wise feed-forward network
3. Normalization layer
4. Residual connections

!!! tip

    **Self-Attention Mechanism**: A crucial part of the encoder's processing is the **self-attention mechanism**. This mechanism allows each token in the input sequence to **dynamically attend to any other token**, which is vital for understanding contextual relationships within the sequence. For instance, in the sentence "The tiger jumped out of a tree to get a drink because it was thirsty," self-attention helps determine that "the tiger" and "it" refer to the same object. This is achieved by creating query, key, and value vectors for each input embedding, calculating scores to determine how much each word should 'attend' to others (dot product of query with keys), normalizing these scores to obtain attention weights, and then using these weights to combine the value vectors, resulting in a **context-aware representation for each word**

    ??? note "Steps"

        1. **Creating Queries, Keys, and Values (Q, K, V)**:
            - Each input embedding (a high-dimensional vector representing the meaning of a token) is multiplied by three different **learned weight matrices**: Wq, Wk, and Wv.
            - This multiplication generates three distinct vectors for each word:
                - **Query (Q) vector**: Helps the model ask, "Which other words in the sequence are relevant to me?”
                - **Key (K) vector**: Acts like a label, helping the model identify how a word might be relevant to other words.
                - **Value (V) vector**: Holds the actual content information of the word
            - In practice, these computations are performed efficiently at the same time by stacking the Q, K, and V vectors for all tokens into matrices and multiplying them together.
        2. **Calculating Scores (Dot Product)**:
            - Scores are computed to determine how much each word should 'attend' to other words in the sequence.
            - This is done by taking the **dot product of the query vector** of one word with the **key vectors of all the words** in the sequence. A higher dot product score indicates a stronger potential relationship.
        3. **Normalization**:
            - The calculated scores are then **divided by the square root of the key vector dimension** (d_k) for stability.
            - Following this, the scores are passed through a **softmax function**. This step normalizes the scores into a probability distribution, yielding **attention weights**. These weights indicate how strongly each word is connected to the others.
        4. **Weighted Values**:
            - Finally, **each value vector is multiplied by its corresponding attention weight.**
            - The results of these multiplications are then **summed up**, producing a **context-aware representation** for each word. This new representation effectively incorporates information from all other words in the sequence, weighted by their relevance.

#### Multi-head self-attention

The encoder employs **multi-head attention**, which involves running multiple sets of query, key, and value matrices in parallel. Each "head" can focus on different aspects of the input relationships. The outputs from these heads are then combined, providing a richer representation of the input sequence. This improves the model's ability to handle complex language patterns and long-range dependencies, essential for tasks requiring a nuanced understanding of language structure

#### Layer Normalization & Residual Connections

**Function and Location**

- Each layer in a Transformer, which includes a Multi-Head Attention module and a Feedforward layer, incorporates **layer normalization and residual connections**.
- This integrated application is referred to as the "**Add and Norm**" layer. The "Add" specifically corresponds to the residual connection, and "Norm" refers to layer normalization.
-  This "Add and Norm" layer is applied to the output of both the Multi-Head Attention module and the Feedforward layer.

**Layer Normalization**

- **Mechanism**: Layer normalization computes the **mean and variance of the activations** to normalize them within a given layer. This process is crucial for stabilizing the training of deep networks.
- **Benefits**: By normalizing activations, layer normalization helps to **reduce covariate shift**, which is the change in the distribution of network activations due to changes in network parameters during training. It also **improves gradient flow**, which means gradients can propagate more effectively through the network, leading to **faster convergence during training** and **improved overall performance** of the model.

**Residual Connections**

- **Mechanism**: Residual connections work by **propagating the inputs to the output of one or more layers5**. Essentially, they create a "shortcut" that allows information to bypass one or more layers directly to a later point in the network.
- **Benefits**: This direct propagation makes the **optimization procedure easier to learn** for the model. Crucially, it also **helps to mitigate common problems in deep neural networks like vanishing and exploding gradients5**. Vanishing gradients occur when gradients become too small to effectively update network weights, while exploding gradients cause updates to become too large, leading to instability. By providing direct paths, residual connections help maintain a stable gradient flow.

#### **Feedforward Layer**

After the multi-head attention module and subsequent "Add and Norm" (layer normalization and residual connections), the data is fed into a feedforward layer. This layer applies independent, position-wise transformations, adding non-linearity and complexity to the model's representations

#### **Output:**

**Contextual Representation (Z)**: The culmination of the encoder's processing of the input sequence is a **"series of embedding vectors Z representing the entire input sequence"**. This output Z is a continuous, context-rich representation that captures the contextual information for each token in the original input. Notably, the size of this output Z is linear in the size of the encoder's input. This Z is then passed to the decoder to facilitate the generation of the output sequence

### Decoder

**Decoder's primary function is to generate the output text** (e.g., an English translation) **autoregressively**, using a representation provided by the encoder

Each decoder, like each encoder, is composed of a series of layers. Each layer within the decoder comprises **key components**: a multi-head self-attention mechanism, a position-wise feed-forward network, normalization layers, and residual connections. These normalization layers and residual connections are referred to as "Add & Norm" layers in Figure 1 of the book.

**Mechanism of the Original Decoder**:

- The decoder operates **token-by-token**, starting with a 'start-of-sequence' token.
- It employs **two types of attention mechanisms** within its layers:
    - **Masked self-attention**: This mechanism ensures that each position in the output sequence can **only attend to earlier positions**. This is critical for **preserving the auto-regressive property** of the decoder, preventing it from "seeing" future tokens in the output sequence that it is trying to predict.
    - **Encoder-decoder cross-attention**: This mechanism allows the decoder to **focus on relevant parts of the input sequence** by utilizing the contextual embeddings (the Z vectors) generated by the encoder. This connects the generation process to the information processed by the encoder.
- This iterative process continues until the decoder predicts an 'end-of-sequence' token, completing the output sequence generation.
- As we discussed previously, the **Feedforward Layer** then processes the output of the attention modules, adding non-linearity and complexity through two linear transformations with a non-linear activation function in between. Following this, another **"Add & Norm" step** is applied, which, as we noted, involves residual connections (propagating inputs to ease optimization and mitigate gradient issues) and layer normalization (stabilizing activations and improving gradient flow).

## Mixture of Experts (MoE)

- Architecture that combines Multiple Speacialized Sub-models (’Experts’) to improve overall performance, particulary on complex tasks.
- Form of Ensemble Learning
- Doesnot use all the experts and learn to route input to specfic Experts. As a result **Sparse Activation**: only subset of Experts Activated.

### Components

1. Experts: Transformer based acrrchitecture
2. Gating Network (Router): Determine how much each Expert will contribute
3. Combination Mechanism:  Weighted Average

## Large Reasoning Models

**Large Reasoning Models** are AI models (like GPT, Llama, DeepSeek, etc.) designed not just to generate text, but to actually **reason - **that is, to solve multi-step problems, explain their answers, and make logical connections.

#### **Why Can’t Vanilla Transformers Reason Well?**

- **Vanilla Transformers** (the standard architecture behind models like GPT-2/3) are great at memorizing patterns, but they struggle with **multi-step thinking** or complex logic.
- To make them better at reasoning, researchers use **special prompting methods**, **training strategies**, and sometimes tweak the architecture.

### Prompting Techniques

#### **1. Chain-of-Thought (CoT) Prompting**

- Instead of just asking for an answer, you ask the model to **show its steps**, like a student explaining their math work.
- Example:
    - Normal: “What’s 13 + 24?” → 37
    - CoT: “What’s 13 + 24?”
        - “13 + 20 = 33, 33 + 4 = 37, so the answer is 37.”
- This makes the model much better at **multi-step or tricky questions**.

#### **2. Tree-of-Thoughts (ToT)**

- Think of this as the model **exploring many possible solution paths** (like in chess, where you imagine several moves ahead) and picking the best one.
- Useful for problems that have more than one way to solve, or where you want the model to “search” through options.

#### **3. Least-to-Most Prompting**

- The model **starts with simple sub-problems**, solves them, and then **uses those answers** to solve harder problems.
- It’s like building up from basics to tough questions, step by step.

### Training Methodologies for reasoning

#### **1. Fine-Tuning on Reasoning Datasets**

- Models get extra training on **special datasets** full of reasoning tasks (like logic puzzles, math, or riddles).
- This makes them better at those specific types of reasoning.

#### **2. Instruction Tuning**

- The model is trained to **follow human instructions** in plain language.
- This helps it understand and follow complex tasks described by users.

#### **3. Reinforcement Learning from Human Feedback (RLHF)**

- After initial training, the model’s answers are scored by humans for **quality and helpfulness**.
- The model then learns to prefer answers that humans liked, making its reasoning **more natural and coherent**.

#### **4. Knowledge Distillation**

- A **big, smart model** (the teacher) solves problems and explains its reasoning.
- A **smaller model** (the student) learns by copying the teacher’s way of reasoning, so it gets smarter **without needing as much computing power**.

#### 5. Novel RL Techniques **(e.g., DeepSeek’s GRPO):** 

- Some models (like DeepSeek-R1) use new methods where the model learns from rules and self-comparison, not just human labels.

### **Inference-Time Techniques (How Models Think at Runtime)**

- **Beam Search:** The model keeps track of multiple possible outputs and picks the best one.
- **Temperature Scaling:** Controls how “random” or “focused” the model’s output is. Lower temperature = more focused on likely answers; higher = more creative/varied.
- **External Knowledge (RAG):** The model can pull in facts from external sources (like Wikipedia or databases) to help answer questions.

## Training the Transformer

Training vs. Inference in Transformer Models

??? note "Explaination"

    ## Training vs. Inference in Transformer Models

    Understanding the difference between **training** and **inference** is crucial when working with large language models (LLMs) like GPT, BERT, or Gemini.

    ---

    ### 1. Training

    **Goal:**

    Teach the model to understand and generate language by adjusting its internal parameters (weights) using vast datasets.

    #### Key Points:

    - **What Happens?**
        - The model is exposed to massive amounts of text data.
        - It learns patterns, relationships, grammar, facts, and reasoning by predicting target outputs (like the next word or missing words).
        - After each prediction, the model compares its guess to the correct answer and updates its parameters to improve future predictions.
    - **Process:**
        1. **Input:** Large, diverse text dataset.
        2. **Forward Pass:** Model makes predictions on batches of data.
        3. **Loss Calculation:** Measures difference between predictions and correct answers.
        4. **Backward Pass:** Uses gradients to update parameters.
        5. **Repeat:** This cycle continues for many passes (epochs) until the model reaches good performance.
    - **Resource Intensive:**
        - Requires huge computation power (GPUs/TPUs), memory, and time (days to weeks).
        - Performed only once per model (except for fine-tuning).

    #### Example:

    - Training GPT-3 involved hundreds of billions of words and powerful supercomputers.

    ---

    ### 2. Inference

    **Goal:**

    Use the trained model to make predictions, generate text, answer questions, or perform other tasks.

    #### Key Points:

    - **What Happens?**
        - The model receives new input data (like a prompt or question).
        - It processes this input using its trained parameters to generate an output (text, answer, etc.).
        - No parameters are changed during inference—the model just uses what it has already learned.
    - **Process:**
        1. **Input:** User prompt or task.
        2. **Forward Pass:** Model computes output based on input and its learned weights.
        3. **Output:** Returns prediction, text, or answer.
    - **Less Resource Demanding:**
        - Usually much faster and less computationally intensive than training.
        - Can run on less powerful hardware (sometimes even on personal devices).
        - Performed every time you interact with the model (e.g., every chat message).

    #### Example:

    - When you ask ChatGPT a question, it’s performing inference using its pretrained parameters.

    ---

    ### 3. Summary Table

    | Aspect | Training | Inference |
    | --- | --- | --- |
    | Purpose | Learn patterns from data | Use learned patterns |
    | Parameter Change | Yes, parameters are updated | No, parameters are fixed |
    | Data | Huge text datasets | New, unseen input |
    | Compute Needs | Very high (GPUs/TPUs, clusters) | Lower (CPUs/GPUs, even mobile) |
    | Time | Hours to weeks | Seconds or less |
    | Frequency | Once (per model or fine-tuning) | Every use |

    ---

    ### 4. Analogy

    - **Training** is like going to school—learning from many textbooks and exercises.
    - **Inference** is like taking a test or answering questions using what you learned at school.

    ---

    **In summary:**

    - **Training** builds the model’s intelligence and capabilities.
    - **Inference** puts those capabilities to use, generating outputs for real-world tasks.

### **Data Preparation**

1. **Cleaning** — Remove errors, duplicates, and inconsistencies from the raw text data.
2. **Tokenization** — Break down text into pieces (“tokens”), such as words or subwords (e.g., with Byte-Pair Encoding or Unigram tokenization). Each token is mapped to a unique number (token ID).
3. **Splitting** — Divide the data into:
    - **Training set:** Used to train the model.
    - **Test/Validation set:** Used to check how well the model is learning.

### **Training Loop**

1. **Batch Processing** — Feed the model small groups (**batches**) of tokenized sequences from the training set, which are processed in parallel.
2. **Forward Pass & Loss Calculation** 
    - **Purpose:** Measure how well the model is predicting.
    - **What happens:**
        - The model takes input sequences and tries to predict the next token (or the masked token, depending on the task).
        - The predicted tokens are compared to the correct tokens using a **loss function** (commonly cross-entropy loss), which measures prediction error.
3. **Backward Pass & Optimization** 
    - **Purpose:** Improve the model.
    - **What happens:**
        - The loss is used to calculate gradients (how much each model parameter contributed to the error).
        - An optimizer (like Adam or SGD) updates the model's parameters in the direction that reduces the loss.
4. **Repeat**
    - **Purpose:** Continue learning.
    - **What happens:** This cycle repeats for many iterations (epochs) until the model reaches a desired performance level or a set number of tokens have been processed.

!!! tip

    **Context Length**

    - This is how many previous tokens the model can “remember” at once.
    - **Longer context = better understanding** of longer passages, but **needs more memory and compute**.

    **Example:** GPT-2 has a context window of 1024 tokens; modern models like Gemini 1.5 Pro can handle millions.

### **Approaches to Formulating the Training Task (Pre-training)**

Transformer models can be categorized based on their architecture and the way they are pre-trained.

#### **Decoder-only Models (e.g., GPT family)**

- **Task:** **Language modeling** — Predict the next token in a sequence.
- **How:** The input is a sequence of tokens; the target is the same sequence shifted right by one position.
- **Effect:** The model learns to generate coherent text and is good at tasks like text completion, answering questions, and summarization.
- **Example:**<br>Input: “The cat sat on the”<br>Target: “cat sat on the mat”<br>The model learns to predict “mat” after seeing “The cat sat on the”.

#### Encoder-only Models (e.g., BERT)

- **Task:** **Masked Language Modeling (MLM)** and **Next Sentence Prediction (NSP)**
- **How:**
    - **MLM:** Randomly mask some tokens in the input and train the model to predict the missing words.
    - **NSP:** Given a pair of sentences, predict if the second sentence follows the first.
- **Effect:** These models are very strong at understanding and analyzing language (classification, information extraction), but **cannot generate coherent new text**.
- **Example (MLM):**<br>Input: “The cat sat on the \[MASK\].”<br>Target: “mat”

#### Encoder-decoder Models (e.g., T5, original Transformer)

- **Task:** **Sequence-to-sequence (seq2seq)** — Convert an input sequence into a target sequence.
- **How:** Used for tasks like translation (English → French), summarization, or question answering.
- **Effect:** Flexible for both understanding and generating text.
- **Example:**<br>Input: “Translate English to French: The cat sat on the mat.”<br>Target: “Le chat s’est assis sur le tapis.”

## Evolution of Transformers

### **1. Birth of the Transformer (2017)**

- **What happened?**Google introduced the Transformer architecture in the 2017 paper "Attention is All You Need."
- **Why was this important?**
    - **Replaced RNNs:** Prior models (like LSTM, GRU) processed sequences one step at a time, making them slow and bad at remembering long-range information.
    - **Parallelization:** Transformers process entire sequences at once, making training much faster.
    - **Self-Attention:** The core innovation. Each word in a sentence can "pay attention" to all other words, capturing context more effectively.

---

### **2. Transformer Architecture Basics**

- **Encoder:** Reads input (e.g., an English sentence) and builds a contextual representation.
- **Decoder:** Generates output (e.g., a translated French sentence) using this representation.
- **Key Components:**
    - **Embedding & Positional Encoding:** Converts words to vectors and adds position info.
    - **Multi-Head Attention:** Lets the model focus on different parts of the input simultaneously.
    - **Layer Normalization & Residual Connections:** Helps stable and efficient training.
    - **Feedforward Layer:** Adds complexity and non-linearity.

---

### **3. Shift to Decoder-Only Models**

- **For tasks like text generation (LLMs), models use just the decoder part.**
- **Masked Self-Attention:** The model can only "see" previous words when generating text, preventing it from cheating by looking ahead.

---

### **4. The Scaling Era (Pre-2022)**

- **GPT-1 (2018):** First big decoder-only LLM. Showed pre-training on lots of text improves performance.
- **BERT (2018):** Used only the encoder for "understanding" tasks (not generation).
- **GPT-2 (2019):** 1.5B parameters, showed scaling up improves zero-shot and few-shot performance.
- **GPT-3 (2020):** 175B parameters, excelled at few-shot learning, could generalize to many tasks with little or no extra training.
- **LaMDA, Gopher, GLaM:** Bigger models, new data curation methods, and first large "Mixture of Experts" (MoE) models for efficiency.

---

### **5. Chinchilla Paradigm Shift (2022)**

- **Old belief:** Make models bigger (more parameters), not necessarily train on more data.
- **Chinchilla finding:** You need to scale both parameters and data size together for the best results with a fixed compute budget.
- **Result:** Chinchilla (70B parameters, lots of data) outperformed much larger but less data-rich models like Gopher (280B).

---

### **6. Modern LLMs: Efficiency, Multimodality, and Diverse Scaling**

- **PaLM, PaLM 2:** Google's giant models, PaLM 2 shows you can get better with smarter design, not just more size.
- **Gemini (Google):** Multimodal (handles text, images, audio, video), ultra-long context (remembers millions of tokens), and uses MoE for efficiency.
- **Gemma:** Lighter, open-access models using Gemini research, efficient for their size.
- **LLaMA (Meta):** Powerful open models, Llama 2/3 fine-tuned for chat, open for commercial use.
- **Mixtral (Mistral AI):** Sparse MoE model, fewer parameters active per token, faster and more efficient.
- **OpenAI O1, DeepSeek:** Focused on reasoning, using new RL/AI training methods.

---

### **7. Key Trends and Innovations**

- **Scaling & Efficiency:** Not just bigger, but smarter—balance model size and data, use MoE and parameter-efficient fine-tuning (Adapters, LoRA, Soft Prompts).
- **Architectural Refinements:** Decoder-only models dominate for generative tasks.
- **Context Length Expansion:** Models can remember much longer contexts (e.g., Gemini 1.5 Pro up to 1 million tokens).
- **Enhanced Capabilities:** From simple text to complex reasoning, coding, math, translation, and more.
- **Multimodality:** Models now process and generate text, images, audio, and video.
- **Training/Fine-Tuning:** New techniques (RLHF, RLAIF, DPO) align models with human preferences and reduce toxicity/bias.
- **Inference Acceleration:** Methods like quantization, distillation, Flash Attention, and speculative decoding make serving large models practical.

---

### **8. Current Limitations**

- LLMs still struggle with:
    - Fully human-like conversation
    - Advanced math
    - Deep ethical alignment

But rapid research continues to narrow these gaps.

---

### GPT-1 (2018, OpenAI)

- Decoder Only
- Trained on BooksCorpus dataset
- I**nnovatons:**
    - Combining Transformers & Unsupervised Pre-training: 

        Trained on un-labeled data (unsupervised pre-training) then fined tuned using labeled data (supervised training)

    - Task-aware Input Transformation:
        - GPT-1 introduced ways to format different tasks (like question answering or textual entailment) so the same model could handle them without changing its structure:
            - **Textual Entailment:** Premise and hypothesis concatenated with a delimiter (\[p, $, h\]).
            - **Question Answering:** Context, question, and a possible answer combined in a single sequence (\[c, q, $, a\]).
        - **No task-specific heads needed:** The same model could handle many tasks, just by changing how input was formatted.
- Performance and Impact:
    - Outperformed previous models on various language understanding benchmarks.
    - Showed that **unsupervised pre-training + supervised fine-tuning** is more powerful than using supervised data alone.
- Limitations:
    - **Repetitive outputs:** Sometimes repeated phrases, especially for prompts very different from its training data.
    - **Weak multi-turn reasoning:** Struggled to follow or remember context over several interactions.
    - **Limited long-range coherence:** Could write fluent short passages, but longer texts often became disjointed or lost track of the topic.
    - **Short context window:** Couldn’t “remember” very far back in the text.

### BERT (2018, Google)

??? note "Details"

    ## BERT: Bidirectional Encoder Representations from Transformers

    **Introduced by Google in 2018, BERT was a landmark model in the evolution of Transformer-based language models, debuting alongside OpenAI’s GPT-1 but following a fundamentally different approach.**

    ---

    ### 1. **Architecture**

    - **Encoder-Only:**
        - Unlike the original Transformer (encoder-decoder) and GPT-1 (decoder-only), BERT uses just the encoder part.
        - It’s designed for **understanding** input sequences and their context, not for generating text step-by-step.

    ---

    ### 2. **Core Innovations**

    #### a) **Bidirectional Contextual Understanding**

    - BERT reads text in both directions (left-to-right and right-to-left) at once, capturing richer context than unidirectional models.
    - This allows BERT to understand the full context of a word by considering words before and after it.

    #### b) **Pre-training Objectives**

    - **Masked Language Modeling (MLM):**
        - Random words in a sentence are replaced with a `[MASK]` token.
        - BERT learns to predict the masked word from the surrounding context.
        - Example:<br>Input: “The cat sat on the \[MASK\].”<br>Target: “mat”
    - **Next Sentence Prediction (NSP):**
        - BERT is given pairs of sentences and learns to predict if the second logically follows the first.
        - This helps BERT understand sentence relationships, useful for tasks like question answering and inference.

    ---

    ### 3. **Strengths & Use Cases**

    - **Natural Language Understanding (NLU):**
        - BERT excels at tasks that need deep understanding of text, such as:
            - Question-answering (QA)
            - Sentiment analysis
            - Natural language inference (NLI)
            - Named entity recognition
            - Text classification
    - **Bidirectionality:**
        - The model considers both previous and next words for every token, resulting in more nuanced and robust understanding.

    ---

    ### 4. **Limitations**

    - **Cannot Generate Text:**
        - BERT’s encoder-only design means it cannot generate text or complete sentences—unlike decoder-only models such as GPT-1.
        - Its outputs are not suitable for open-ended text generation, but are perfect for analysis and understanding tasks.

    ---

    ### 5. **BERT vs. GPT-1: Evolutionary Fork**

    - **Understanding (BERT) vs. Generation (GPT-1):**
        - BERT: Focuses on deep contextual understanding for analysis.
        - GPT-1: Focuses on generating text, content creation, and open-ended tasks.
    - **Bidirectionality:**
        - BERT: Bidirectional context (left and right).
        - GPT-1: Unidirectional (left to right).
    - **Dominance:**
        - Most modern generative LLMs use decoder-only designs (like GPT-1), but BERT’s encoder-only approach remains best for NLU.

    ---

    ### 6. **Technical Specs (BERT-Large, from Table 1)**

    | Hyperparameter | Value |
    | --- | --- |
    | Optimizer | ADAM |
    | Number of Parameters | 340M |
    | Vocabulary Size | ~30,000 |
    | Embedding Dimension | 1024 |
    | Key Dimension | 64 |
    | Number of Attention Heads (H) | 16 |
    | Number of Encoder Layers | 24 |
    | Decoder Layers | N/A |
    | Feed Forward Dimension | 4096 |
    | Context Token Size | 512 |
    | Pre-training Tokens | ~3.3B |

    ---

    ### 7. **BERT’s Lasting Impact**

    - **Foundation for NLU tasks:** BERT set new benchmarks in language understanding and inspired a whole family of “BERT-like” models (RoBERTa, ALBERT, DistilBERT, etc.).
    - **Proof of Unsupervised Pre-training:** Like GPT-1, BERT demonstrated the value of pre-training on large unlabeled corpora, then fine-tuning for specific tasks.

    ---

    **In summary:**

    BERT pioneered deep, bidirectional understanding in transformer models, making it the go-to architecture for analytical and comprehension-heavy language tasks, while generative LLMs (like GPT-1 and successors) specialized in producing fluent, human-like text.

### GPT-2 (2019)

??? note "Details"

    ## GPT-2: Generative Pre-trained Transformer 2

    **Released by OpenAI in 2019, GPT-2 was a transformative leap in large language models, building directly on GPT-1’s foundation and setting new standards for generative AI.**

    ---

    ### 1. **Architecture**

    - **Decoder-only Transformer:**
        - Like GPT-1, GPT-2 uses only the decoder part of the Transformer, optimized for generating text sequences.
        - This design became the dominant choice for generative LLMs.

    ---

    ### 2. **Key Innovations**

    #### a) **Massive Scaling (Data & Parameters)**

    - **Parameter Scaling:**
        - GPT-2 increased its size from GPT-1’s 117 million parameters to **1.5 billion parameters**.
        - OpenAI also released smaller versions (117M, 345M, 762M) to study the impact of scale.
    - **Data Scaling:**
        - Switched from BooksCorpus (5GB) to **WebText** (40GB, ~45 million webpages from quality Reddit links).
        - This dataset was more diverse and reflected real-world language usage.

    #### b) **Improved Text Generation**

    - **Results:**
        - Generated much more coherent, realistic, and contextually appropriate text than GPT-1.
        - Better at capturing long-range dependencies and commonsense reasoning.

    #### c) **Zero-Shot Learning**

    - **Breakthrough:**
        - GPT-2 could generalize to new tasks **without task-specific training** (zero-shot transfer).
        - Example: Given a translation prompt (e.g., “English: Hello, German:”), GPT-2 could attempt a translation just from instructions, never having seen translation data during fine-tuning.
        - Performance on these tasks improved log-linearly as the model scaled up.

    ---

    ### 3. **Performance and Impact**

    - **Human-like text generation:**
        - GPT-2 became known for producing impressively fluent and creative text, making it useful for content creation, conversation, and brainstorming.
    - **Limits:**
        - Did **not** surpass the best models for reading comprehension, summarization, or translation at the time.
        - Still occasionally generated plausible-sounding but incorrect or nonsensical answers (“hallucination”).

    ---

    ### 4. **Significance in LLM Evolution**

    - **Scaling Laws:**
        - Demonstrated a clear relationship: **more data + bigger models = better performance** (especially for generative and reasoning tasks).
    - **Zero-shot abilities:**
        - Opened the door for models to solve tasks with minimal or no examples, reducing reliance on large labeled datasets.
    - **Set the stage for GPT-3:**
        - GPT-3 took these principles even further, leading to even more capable and general-purpose language models.

    ---

    ### 5. **Summary Table: GPT-2 vs. GPT-1**

    | Feature | GPT-1 | GPT-2 |
    | --- | --- | --- |
    | Year | 2018 | 2019 |
    | Architecture | Decoder-only | Decoder-only |
    | Parameters | 117M | 1.5B (largest) |
    | Training Data | 5GB BooksCorpus | 40GB WebText |
    | Zero-shot Learning | Limited | Yes (strong) |
    | Text Coherence | Fair | Excellent |
    | Use Cases | Generation | Generation, zero-shot transfer |

    ---

    **In summary:**

    GPT-2 showed that simply making models bigger and training them on more (and better) data leads to dramatic improvements in generative AI. It proved the value of scale in LLMs and introduced the world to zero-shot capabilities, paving the way for the even more powerful GPT-3 and beyond.

### GPT-3/3.5/4

??? note "Details"

    ## GPT-3, GPT-3.5, and GPT-4: Advancements in Transformer LLMs

    The GPT-3, GPT-3.5, and GPT-4 series from OpenAI represent major milestones in the evolution of Transformer-based large language models (LLMs), building upon the foundations of GPT-1 and GPT-2. These models use the **decoder-only variant** of the Transformer architecture, optimized for generating output sequences from input prompts.

    ---

    ### GPT-3 (2020)

    - **Massive Scale:**
        - 175 billion parameters (vs. GPT-2's 1.5B), enabling more nuanced, context-aware, and coherent text generation.
        - Trained on a vast and diverse dataset, supporting improved generalization and knowledge.
    - **Few-Shot and Zero-Shot Learning:**
        - Able to perform new tasks with just a few examples (few-shot) or even none (zero-shot) by interpreting instructions in the prompt.
        - Reduced need for task-specific fine-tuning.
    - **Broader Generalization:**
        - Outperformed GPT-2 on a wide range of NLP tasks, including translation, question answering, and summarization, all without explicit re-training.
    - **Commercial Availability:**
        - Released as a commercial API, making advanced LLM capabilities widely accessible.

    ---

    ### GPT-3.5

    - **InstructGPT Foundation:**
        - Introduced SFT (Supervised Fine-Tuning) on human demonstrations and RLHF (Reinforcement Learning from Human Feedback) for better alignment with human preferences.
        - Even a 1.3B parameter InstructGPT model outperformed the 175B parameter vanilla GPT-3 on instruction-following and helpfulness.
    - **GPT-3.5 Turbo:**
        - Optimized for dialogue and code generation.
        - Supported very large context windows (up to 16,385 tokens) and outputs up to 4,096 tokens.
        - Improved instruction following, truthfulness, and reduced toxicity.

    ---

    ### GPT-4

    - **Multimodality:**
        - First in the GPT series to accept both **text and image inputs** (and output text), expanding scope to vision-language tasks.
    - **Advanced Reasoning and Knowledge:**
        - Demonstrates stronger general knowledge and complex reasoning, matching or exceeding human-level performance in many domains (math, coding, law, medicine, psychology).
    - **Vast Context Window:**
        - Handles up to 128,000 tokens of input, enabling deep comprehension of long documents.
    - **Versatility:**
        - Excels at a diverse array of complex tasks without specialized instructions, outperforming earlier models like GPT-3.5 in both breadth and depth.

    ---

    ### Key Trends in the Evolution of the GPT Series

    - **Decoder-Only Dominance:**
        - GPT models consistently use the decoder-only Transformer, ideal for text generation, vs. encoder-only models (like BERT) for understanding.
    - **Validation of Scaling Laws:**
        - Consistent performance gains as model size and dataset size increase:
            - GPT-1: 117M parameters, ~1.25B tokens
            - GPT-2: 1.5B parameters, ~10B tokens
            - GPT-3: 175B parameters, ~300B tokens
    - **Emergent Few-Shot and Zero-Shot Learning:**
        - Larger models naturally gain the ability to generalize to new tasks with little or no training examples.
    - **Advanced Fine-Tuning (SFT + RLHF):**
        - Critical for aligning models with human values and preferences, reducing undesirable outputs, and improving instruction-following.
    - **Move Towards Multimodality:**
        - GPT-4’s image+text capabilities set the stage for future AI models to handle multiple data types, not just text.

    ---

    ### Summary Table

    | Model | Parameters | Context Window | Notable Features | Input Types | Alignment Techniques |
    | --- | --- | --- | --- | --- | --- |
    | GPT-3 | 175B | ~2-4K tokens | Few/Zero-shot, broad generalization | Text | Pre-training only |
    | GPT-3.5 | ~1.3B-175B | up to 16K | SFT + RLHF, optimized for dialogue and code | Text | SFT, RLHF |
    | GPT-4 | (Not public) | up to 128K | Multimodal (text+image), advanced reasoning | Text+Image | SFT, RLHF |

    ---

    ### In Essence

    The progression from GPT-3 to GPT-4 underscores the power of scaling, advanced alignment, and architectural choices. These models are not only larger and more capable, but also more flexible, aligned with human intent, and increasingly multimodal—paving the way for even more general and powerful AI systems.

### LaMDA (2021, Google)

??? note "Details"

    ## LaMDA (Language Model for Dialogue Applications)

    LaMDA is a large-scale language model developed by Google and introduced in 2021, representing a specialized approach to conversational AI within the evolution of Transformer-based models.

    ---

    ### 1. **Purpose and Specialization**

    - **Dialogue-First Design:**

        LaMDA was built specifically for open-ended, sustained conversation. Unlike traditional chatbots restricted to set domains, LaMDA is engineered to discuss virtually any topic, focusing on maintaining conversational flow and depth.

    - **Conversational Flow:**

        Trained on dialogue-centric data, LaMDA emphasizes ongoing, explorative, and natural exchanges—mimicking the unpredictability and richness of human conversational dynamics.

    ---

    ### 2. **Comparison to GPT Models**

    - **Specialization vs. Generalization:**
        - **GPT-3 and successors** are designed for general-purpose language tasks: text generation, reasoning, coding, summarization, etc.
        - **LaMDA’s focus** is on dialogue, prioritizing the quality, continuity, and naturalness of conversations over broad multi-task performance.
    - **Conversational Depth:**
        - GPT models excel at long-form content and multi-tasking with minimal prompts.
        - LaMDA excels at sustaining engaging, context-aware dialogue, aiming to make conversations feel more human.

    ---

    ### 3. **Architectural and Technical Details**

    | Attribute | LaMDA Value |
    | --- | --- |
    | **Architecture** | Transformer (decoder-only) |
    | **Parameters** | 137 billion |
    | **Pre-training Tokens** | ~168 billion |
    | **Optimizer** | ADAM |
    | **Vocabulary Size** | ~32,000 |
    | **Embedding Dim.** | 8192 |
    | **Key Dim.** | 128 |
    | **Attention Heads** | 128 |
    | **Decoder Layers** | 64 |
    | **Context Token Size** | N/A |

    - **Scale:**

        LaMDA is a very large model, though slightly smaller than GPT-3 (175B parameters). Its scale supports nuanced, context-rich dialogue.

    - **Training:**

        Focused on dialogue data, optimizing for conversational continuity rather than just factual recall or general task execution.

    ---

    ### 4. **Significance in Transformer Evolution**

    - **Emergence of Specialization:**

        LaMDA demonstrates that LLM progress isn't just about ever-larger, generalist models, but also about tailoring architectures and training for complex, focused applications—like truly human-like conversation.

    - **Complementary to Generalist LLMs:**

        The divergence between LaMDA (dialogue specialist) and GPT-3 (generalist) illustrates multiple evolutionary paths for Transformer models, with some prioritized for conversational AI and others for broad multi-task capabilities.

    ---

    ### 5. **Summary Table: LaMDA vs. GPT-3**

    | Feature | LaMDA | GPT-3 |
    | --- | --- | --- |
    | **Parameters** | 137B | 175B |
    | **Primary Focus** | Open-ended dialogue | General tasks |
    | **Training Data** | Dialogue-centric | Broad internet |
    | **Strength** | Conversational flow | Generalization, few-shot |
    | **Architecture** | Transformer (decoder-only) | Transformer (decoder-only) |
    | **Release Year** | 2021 | 2020 |

    ---

    **In summary:**

    LaMDA is a landmark example of how large language models can be specialized for deep, nuanced, and natural conversations. Its development underscores the importance of both scaling and specialization in the evolution of Transformer-based AI, complementing the generalist approach of models like GPT-3 by advancing the state of conversational AI.

### Gopher (2021, DeepMind)

??? note "Details"

    ## Gopher: A Landmark in Scaling Laws and Data Quality for LLMs

    Gopher, introduced by DeepMind in 2021, stands out as a major milestone in the evolution of large language models (LLMs), especially regarding the understanding of scaling laws and the critical role of dataset quality.

    ---

    ### 1. **Architecture and Scale**

    - **Decoder-Only Transformer:**<br>Like many state-of-the-art LLMs (e.g., GPT-3), Gopher uses a decoder-only Transformer architecture.
    - **Parameters:**<br>280 billion, making it one of the largest LLMs at its time (larger than GPT-3’s 175B).
    - **Technical Specs:**
        - **Decoder Layers:** 80
        - **Embedding Dimension:** 16,384
        - **Attention Heads:** 128
        - **Context Token Size:** 2,048
        - **Optimizer:** ADAM

    ---

    ### 2. **Training Data and Quality Focus**

    - **Dataset:**<br>Gopher was trained on **MassiveText**, a carefully curated dataset comprising over 10TB of data (~2.45B documents) from diverse sources: web pages, books, news, and code.
    - **Training Tokens:**<br>~300 billion tokens.
    - **Data Quality:**
        - Extensive filtering and deduplication to remove low-quality or duplicate content.
        - This improved downstream performance, highlighting data quality as being as important as quantity in LLM training.

    ---

    ### 3. **Optimization Techniques**

    - **Learning Rate Schedule:**<br>Warmup for 1,500 steps, then decayed using a cosine schedule.
    - **Scaling Rule:**<br>As model size increased, learning rates were reduced and batch sizes increased.
    - **Gradient Clipping:**<br>Global gradient norm clipped at 1 for training stability.

    ---

    ### 4. **Capabilities and Performance**

    - **Strengths:**
        - Outperformed previous SOTA models in 81% of evaluated tasks, including knowledge, reading comprehension, scientific understanding, and general Q&A.
        - Excelled at knowledge-intensive tasks.
    - **Weaknesses:**
        - Struggled with reasoning-heavy tasks (e.g., abstract algebra), showing that parameter count alone does not guarantee reasoning ability.
    - **Ablation Study:**
        - Increasing model size significantly boosted logical reasoning and reading comprehension, but had diminishing returns on general knowledge.

    ---

    ### 5. **Impact on LLM Evolution**

    - **Scaling Laws:**
        - Gopher reaffirmed that increased size and data led to better performance, driving the “scaling laws” paradigm in LLMs.
    - **Data Quality Emphasis:**
        - Pioneered the idea that high-quality, deduplicated data is essential, not just raw scale.
    - **Compute-Optimal Scaling (vs. Chinchilla):**
        - Later, the Chinchilla model (70B parameters) outperformed Gopher, despite being smaller, by being trained on more data. This revealed that **scaling parameters and data together is optimal**, not just scaling model size.
    - **Specialization vs. Generalization:**
        - Gopher’s mixed results on reasoning-intensive tasks led to greater research into reasoning-specific training methods and prompting strategies.

    ---

    ### 6. **Summary Table: Gopher’s Technical Profile**

    | Attribute | Value |
    | --- | --- |
    | Architecture | Decoder-only Transformer |
    | Parameters | 280B |
    | Decoder Layers | 80 |
    | Embedding Dimension | 16,384 |
    | Attention Heads | 128 |
    | Context Token Size | 2,048 |
    | Optimizer | ADAM |
    | Training Tokens | ~300B |
    | Training Dataset | MassiveText (10TB+, 2.45B docs) |

    ---

    ### 7. **Significance**

    Gopher’s development marked:

    - A validation and refinement of scaling laws for LLMs.
    - The elevation of data quality to a top-tier concern in model training.
    - A turning point that led to “compute-optimal” models (like Chinchilla) and new research into reasoning-boosting techniques.

    **In summary:**

    Gopher was a crucial step forward in the LLM landscape—not just for its scale, but for advancing the science of how best to balance model size and data quality for future breakthroughs.

### GLaM (2022, Google)

??? note "Details"

    ## GLaM (Generalist Language Model): Pioneering Sparse Mixture-of-Experts for Scalable and Efficient LLMs

    GLaM, developed by Google in 2022, marks a major milestone in the evolution of Transformer-based large language models by introducing an effective and scalable **Mixture-of-Experts (MoE)** architecture.

    ---

    ### 1. **Architectural Innovation: Mixture of Experts (MoE)**

    - **First Sparsely-Activated MoE LLM:**<br>GLaM is the first large-scale language model to employ a sparsely-activated Mixture-of-Experts architecture.
    - **How MoE Works:**
        - The model contains multiple “experts” (specialized transformer sub-models).
        - A “gating network” or router decides which experts should process each part of the input.
        - Only a small subset of experts are activated per token, making computation “sparse” compared to dense models (where all parameters are active for every computation).
        - The outputs from selected experts are combined to form the final prediction.
    - **Specialization:**<br>Experts can become proficient in different data sub-domains, enhancing the model’s ability to handle diverse and complex tasks.

    ---

    ### 2. **Scale and Computational Efficiency**

    - **Parameters:**
        - GLaM contains **1.2 trillion parameters**—massively surpassing previous models like GPT-3 (175B) and Gopher (280B).
        - However, only a fraction of these parameters are activated for any given input, leading to significant efficiency gains.
    - **Energy and Compute:**
        - Used **only 1/3 the energy of GPT-3** and **half the FLOPs for inference** despite being much larger in total parameter count.
        - Demonstrates that MoE models can be both **larger and more efficient** than dense counterparts.

    ---

    ### 3. **Performance**

    - **Superior to GPT-3:**
        - GLaM achieved **better overall performance** on language tasks compared to GPT-3, while being more efficient.
    - **Proof of Efficient Scaling:**
        - Showed that computational efficiency and high performance are not mutually exclusive.

    ---

    ### 4. **Broader Impact on LLM Evolution**

    #### a) **Alternative Scaling Paradigm**

    - Prior to GLaM, the main route to better performance was to increase *dense* parameter and data size (e.g., GPT-3, Gopher).
    - GLaM proved that **sparse activation (MoE)** offers a new way to scale up LLMs without unreasonable increases in compute or energy cost.

    #### b) **Efficiency Focus**

    - GLaM shifted the field’s focus to the **quality vs. latency/cost tradeoff**—emphasizing that efficient architectures are crucial as models grow.

    #### c) **Architectural Diversification**

    - GLaM’s success encouraged the development of other MoE models (e.g., Mixtral 8x7B, Gemini) and diversified the LLM ecosystem beyond standard dense Transformers.

    ---

    ### 5. **Legacy and Influence**

    - **Foundation for Future MoE Models:**
        - GLaM’s demonstration of sparse activation’s effectiveness laid the groundwork for newer, efficient LLMs using MoE, such as Google’s Gemini and Mixtral.
    - **Signaled a Shift in LLM Evolution:**
        - The field now seeks not only to make models larger, but also smarter about how size and compute are used.

    ---

    ### 6. **Summary Table: GLaM vs. Dense LLMs**

    | Model | Architecture | Total Params | Active Params per Inference | Efficiency | Performance |
    | --- | --- | --- | --- | --- | --- |
    | GPT-3 | Dense Transformer | 175B | 175B | Low | Good |
    | Gopher | Dense Transformer | 280B | 280B | Low | Good |
    | GLaM | Sparse MoE | 1.2T | Fraction (sparse) | High (uses 1/3 energy of GPT-3) | Superior to GPT-3 |

    ---

    **In summary:**

    GLaM was a breakthrough in LLM design, proving that *how* you scale (sparse MoE) is as important as *how much* you scale, paving the way for more efficient, powerful, and specialized language models.

### Chinchilla (2022, DeepMind)

??? note "Details"

    ## Chinchilla: Redefining Scaling Laws for Large Language Models

    Chinchilla, released by DeepMind in 2022, marks a paradigm shift in the development of Transformer-based Large Language Models (LLMs) by fundamentally redefining optimal scaling laws for efficient training.

    ---

    ### 1. **Background: The Scaling Law Debate**

    - **Pre-Chinchilla Wisdom:**<br>Influenced by Kaplan et al., the prevailing view was to scale parameter count much more rapidly than dataset size when increasing compute. This led to massive models like GPT-3 (175B params) and Gopher (280B), both trained on relatively modest data volumes (e.g., Gopher with 300B tokens).
    - **Chinchilla’s Challenge:**<br>Chinchilla’s research found that **near-equal scaling** of parameters and training data is actually optimal for a given compute budget. This means:

        > If you increase compute 100-fold, you should increase both model size and data size about 10-fold each.

    ---

    ### 2. **Chinchilla’s Validation: Smarter, Not Just Bigger**

    - **Model:**<br>Chinchilla (70B parameters)
        - Trained with the *same compute budget* as the much larger Gopher (280B).
        - Used **1.4 trillion** training tokens (vs. Gopher’s 300B).
    - **Results:**
        - **Chinchilla, despite being 4x smaller than Gopher, outperformed it on every major evaluation.**
        - Outperformed other major models like GPT-3 and Megatron-Turing NLG (530B) on a wide range of downstream tasks.
        - Smaller size also means **lower inference costs and memory demands**.
        - Demonstrated that more data (not just more parameters) is *crucial* for performance and efficiency.

    ---

    ### 3. **Technical Characteristics**

    | Attribute | Value |
    | --- | --- |
    | Architecture | Decoder-only Transformer |
    | Parameter Count | 70B |
    | Optimizer | ADAM-W |
    | Vocabulary Size | ~32,000 |
    | Embedding Dimension | 8192 |
    | Key Dimension | 128 |
    | Attention Heads | 64 |
    | Decoder Layers | 80 |
    | Feedforward Dimension | 32,768 |
    | Context Token Size | 2048 |
    | Pre-Training Tokens | ~1.4 trillion |

    ---

    ### 4. **Impact on LLM Evolution**

    #### a) **Revolutionized Scaling Laws**

    - Provided empirical proof that **balancing model size and dataset size** is the compute-optimal route for LLMs.
    - Contradicted previous approaches that favored overwhelmingly increasing parameter count.

    #### b) **Refocused LLM Development**

    - Shifted industry emphasis to also **scaling up data** (with quality), not just parameters.
    - Raised concerns about reaching the "data ceiling"—the limit of available high-quality text data for future models.

    #### c) **Efficiency Without MoE**

    - While models like GLaM (2022) pursued efficiency through sparse Mixture-of-Experts, Chinchilla showed that **dense architectures** can still be highly efficient—if trained with the right data-to-parameter ratio.

    #### d) **Continued Decoder-Only Dominance**

    - Like Gopher and GPT-3, Chinchilla used a decoder-only Transformer, reinforcing this as the dominant architecture for generative LLMs.

    ---

    ### 5. **Broader Influence**

    - **Compute-Optimal Training:**<br>Chinchilla’s methodology has shaped the training strategies of subsequent models, including Google Gemini, which explicitly employs Chinchilla-style scaling in its largest models.
    - **Paradigm Shift:**<br>The insight that *how* you balance parameters and data is more important than ever-larger models has become a foundational principle for advanced LLM development.

    ---

    **Summary:**

    Chinchilla’s breakthrough was to demonstrate, with hard evidence, that balanced scaling of both model size and data is the key to getting the most out of available compute. This finding has redefined the trajectory of LLM research and set a new standard for efficiency and performance in the field.

### PaLM (2022, Google)

??? note "Details"

    ## PaLM (Pathways Language Model): Massive Scale and Advanced Capabilities

    PaLM, released by Google AI in 2022, represents a landmark in the evolution of Transformer-based large language models (LLMs) through its unprecedented scale, broad capabilities, and infrastructure innovations.

    ---

    ### 1. **Scale and Capabilities**

    - **Enormous Model Size:**
        - **540 billion parameters**, making it the largest LLM at its time of release.
        - Surpassed models like GPT-3 (175B), Gopher (280B), and Megatron-Turing NLG (530B).
    - **Versatile Abilities:**
        - Excels at tasks including common sense reasoning, arithmetic reasoning, joke explanation, code generation, and translation.
        - Achieved state-of-the-art (SOTA) results on many language benchmarks (e.g., GLUE, SuperGLUE).

    ---

    ### 2. **Technical Specifications**

    | Attribute | Value |
    | --- | --- |
    | Architecture | Decoder-only Transformer |
    | Parameters | 540B |
    | Pre-training Tokens | ~300B |
    | Optimizer | ADAM |
    | Vocabulary Size | ~32,000 |
    | Embedding Dimension | 8192 |
    | Attention Heads | 64 |
    | Decoder Layers | 80 |
    | Foundation for PaLM 2 | Yes |

    ---

    ### 3. **Training Infrastructure: Pathways System**

    - **Pathways:**
        - Google’s distributed training system, allowing PaLM to be efficiently trained across two TPU v4 Pods.
        - Enabled training of extremely large models with practical time and resource efficiency.
    - **Efficiency:**
        - Demonstrated that infrastructure and distributed systems are key to scaling LLMs.

    ---

    ### 4. **Position in Scaling Law Evolution**

    - **Pre-Chinchilla Scaling Paradigm:**
        - PaLM embodies the "scale parameters first" philosophy before Chinchilla’s findings in 2022.
        - Trained on ~300B tokens—comparable to GPT-3 and Gopher—but with a far larger parameter count.
        - **Contrast:**
            - Chinchilla (70B params, 1.4T tokens) showed that *balancing* model size and data is optimal for compute and performance.
            - PaLM is viewed as the apex of the old paradigm, preceding Google’s shift to Chinchilla-style scaling in models like Gemini.

    ---

    ### 5. **Architectural Choice**

    - **Decoder-Only:**
        - Like GPT-3 and Gopher, PaLM uses a decoder-only Transformer, optimized for generative tasks (predicting the next token in a sequence).

    ---

    ### 6. **Legacy and Influence**

    - **Foundation for PaLM 2 and Gemini:**
        - PaLM’s architecture and capabilities informed the development of PaLM 2 (2023), which achieved better performance with fewer parameters.
        - Google’s Gemini models adopted Chinchilla-style, compute-optimal training—balancing data and parameter count for efficiency and capability.
    - **Pushed Boundaries:**
        - PaLM demonstrated the upper limits of scale-centric LLMs and the critical role of infrastructure in enabling new AI capabilities.

    ---

    ### 7. **Summary Table: PaLM vs. Key Contemporaries**

    | Model | Parameters | Pre-training Tokens | Scaling Philosophy | SOTA Performance | Foundation For |
    | --- | --- | --- | --- | --- | --- |
    | GPT-3 | 175B | ~300B | Scale parameters | Yes | GPT-3.5, GPT-4 |
    | Gopher | 280B | ~300B | Scale parameters | Yes | Chinchilla |
    | PaLM | 540B | ~300B | Scale parameters | Yes | PaLM 2, Gemini |
    | Chinchilla | 70B | 1.4T | Balance params+data | Yes (over PaLM) | Gemini |

    ---

    **In summary:**

    PaLM exemplified the power and limitations of the “scale-up-parameters” era, achieving state-of-the-art capabilities and enabling new LLM applications through massive scale and advanced infrastructure. Its legacy persists in newer, more compute-efficient models, and in the shift to scaling laws that balance model size with data, as exemplified by Chinchilla and Gemini.

### PaLM 2 (2023, Google)

??? note "Details"

    ## PaLM 2: Efficient Scaling and Enhanced Capabilities in LLM Evolution

    PaLM 2, announced by Google in May 2023, is a major advancement in Transformer-based large language models (LLMs), building on the foundation of PaLM while introducing significant enhancements in efficiency and performance.

    ---

    ### 1. **Key Characteristics and Advancements**

    - **Improved Efficiency:**
        - **More capable than PaLM** but with **fewer total parameters**.
        - Reflects a shift from brute-force scaling (adding more parameters) to smarter, more resource-efficient model design.
    - **Architectural & Training Enhancements:**
        - Achieves its performance gains through architectural and training refinements (specifics not publicly detailed).
        - Indicates continuous progress in LLM design beyond just raw scale.

    ---

    ### 2. **Advanced Tasks and Commercial Impact**

    - **Excels at Advanced Reasoning:**
        - Strong performance on code generation, math, classification, question answering, translation, and more.
        - Demonstrates broad utility and improved complex reasoning abilities.
    - **Commercial Foundation:**
        - Serves as the **basis for Google Cloud Generative AI** models, underpinning many enterprise and commercial offerings.

    ---

    ### 3. **Evolution in LLM Scaling Philosophy**

    - **From “Parameters First” to “Efficient Scaling”:**
        - **PaLM (2022):** 540B parameters, trained on ~300B tokens, reflecting the old paradigm of prioritizing model size.
        - **PaLM 2:** Achieves greater capability with a smaller parameter count—conceptually aligned with the **Chinchilla (2022) insight** that optimal performance comes from *balancing* parameter count and data size.
    - **Alignment with Chinchilla’s Lessons:**
        - Chinchilla demonstrated that “near equal scaling in parameters and data is optimal with increasing compute.”
        - PaLM 2’s efficiency and performance gains suggest Google’s early adoption of these compute-optimal scaling principles, preceding full adoption in models like Gemini.

    ---

    ### 4. **Legacy and Roadmap Significance**

    - **Pivotal Role:**
        - PaLM 2 is a key link between the scale-centric PaLM and the compute-optimal, multimodal Gemini series.
        - Helped shift Google’s LLM development from sheer size to efficiency, aligning with industry-wide best practices.
    - **Foundation for Future Models:**
        - Many of Google’s latest generative AI offerings are built on PaLM 2.
        - Later models, like Gemini, explicitly use Chinchilla-style compute-optimal scaling.

    ---

    ### 5. **Summary Table: PaLM vs. PaLM 2**

    | Feature | PaLM (2022) | PaLM 2 (2023) |
    | --- | --- | --- |
    | Parameters | 540B | Fewer (undisclosed) |
    | Scaling Philosophy | Parameters-first | Efficient, balanced |
    | Performance | SOTA at release | Superior, more efficient |
    | Commercial Use | Foundation for PaLM 2, Gemini | Google Cloud AI platform |
    | Chinchilla-Style Scaling | No | Partial/Transitional |

    ---

    **In summary:**

    PaLM 2 reflects Google’s pivot toward more sophisticated, resource-aware LLMs, achieving higher capability and efficiency not just through scale, but through smarter architecture and training. It stands as a milestone in the ongoing evolution towards compute-optimal and versatile AI models.

many more…

---

## Fine Tuning LLMs

- **Definition:**

    Fine-tuning is a specialized training phase that follows the initial, broad pre-training of an LLM.

    - **Pre-training:** The LLM learns general language patterns from a massive, unlabeled dataset.
    - **Fine-tuning:** The already pre-trained LLM is further trained on a smaller, high-quality, often labeled dataset tailored to a specific task, domain, or behavior.
- **Why important?**
    - Makes general-purpose LLMs perform well on specialized real-world tasks (e.g., customer support, medical Q&A, code generation).
    - Improves alignment with human preferences (helpfulness, safety, style).
    - Is much cheaper and faster than pre-training.

---

### **2. Benefits of Fine-Tuning**

- **Instruction following:**The LLM learns to follow explicit instructions (summarize, translate, write code).
- **Dialogue:**Fine-tuning on dialogue data makes LLMs better at conversational tasks (multi-turn interaction).
- **Safety:**Reduces harmful, biased, or toxic outputs through careful curation and human feedback.
- **Generalizability:**Boosts performance on targeted challenges (translation, question-answering, summarization).

---

### **3. Key Fine-Tuning Techniques**

#### **A. Supervised Fine-Tuning (SFT)**

- The model is further trained on labeled, task-specific data (input-output pairs).
- Example: Training on prompt-response pairs for Q&A or summarization.
- Makes models safer, more accurate, and better at following instructions.

#### **B. Reinforcement Learning from Human Feedback (RLHF)**

- Fine-tuning the model based on human preference rankings of outputs.
- **Process:**
    1. **Reward Model:** Train a model to score outputs based on human preferences.
    2. **Policy Optimization:** Use RL to steer the LLM to generate outputs that maximize the reward model’s score.
- **Variants:**
    - **RLAIF:** Same as RLHF but uses AI-generated feedback.
    - **DPO:** Direct Preference Optimization, uses preference data directly, often skipping reward modeling.
- **Goal:**Makes models more helpful, truthful, and less likely to give unsafe or unhelpful responses.

#### **C. Parameter Efficient Fine-Tuning (PEFT)**

- For very large LLMs, retraining all parameters is expensive; PEFT methods only update a small subset.
- **Popular PEFT approaches:**
    - **Adapter-based:** Add small neural modules (adapters) into the model; only train these.
    - **LoRA (Low-Rank Adaptation):** Add tiny trainable matrices; freeze main weights, update only these.
        - **QLoRA:** Uses quantized weights for greater efficiency.
    - **Soft Prompting:** Learn small, continuous vectors (“soft prompts”) that condition the model for a task.
- **Advantages:**
    - Dramatically reduces compute and memory cost.
    - Easy to swap-in/swap-out for multi-task or personalized LLMs.

---

### **4. Fine-Tuning in LLM Evolution (Historical Context)**

- **GPT-1 (2018):** Combined unsupervised pre-training with supervised fine-tuning—a breakthrough in using general models for specific tasks.
- **GPT-3 (2020):** Showed strong few-shot and zero-shot capabilities, reducing the reliance on fine-tuning for many tasks.
- **InstructGPT:** Used SFT + RLHF to make models much better at instruction following and safer, even outperforming larger, non-fine-tuned models.
- **DeepSeek-R1:** Uses SFT, RL, and rejection sampling to iteratively improve reasoning and generate synthetic data for further refinement (especially for "chain-of-thought" reasoning).
- **Gemini Nano:** Uses distillation + fine-tuning to make smaller, efficient models that still perform well on specialized tasks.

## Methods for Using LLMs Effectively

### **1. Prompt Engineering**

**Definition:**

Crafting and refining the input text (“prompts”) to guide the LLM’s output toward your specific goals.

**Key Techniques:**

- **Zero-shot prompting:**
    - Give only a task description.
    - Example: *“Translate this sentence to French: ‘Hello, how are you?’”*
- **Few-shot prompting:**
    - Add a few examples to teach the model the task.
    - Example:

        ```plain text

English: Hello, how are you?

French: Bonjour, comment ça va ?

English: Good morning

French:

```

- **Chain-of-Thought (CoT) prompting:**
    - Show step-by-step reasoning to encourage the model to do the same.
    - Example:*“Q: If there are 3 apples and you eat 1, how many are left? A: There are 3 apples. You eat 1. 3-1=2. Answer: 2.”*

**Why it matters:**

Well-designed prompts can make an LLM much more accurate, relevant, and reliable for your task.

---

### **2. Sampling Techniques and Parameters**

These control how the LLM picks its next word, balancing creativity and accuracy.

**Main Techniques:**

- **Greedy Search:**
    - Always picks the highest-probability word.
    - Output: Predictable, safe, but may be repetitive.
- **Random Sampling:**
    - Picks based on probability—adds variety, but can be less coherent.
- **Temperature:**
    - Adjusts riskiness:
        - Low temperature (0.2): Conservative, less diverse
        - High temperature (1.0+): More random, creative
- **Top-K Sampling:**
    - Samples from the top K most likely words.
- **Top-P (Nucleus) Sampling:**
    - Samples from the smallest set of words whose probabilities sum to P (e.g., 0.9).
- **Best-of-N Sampling:**
    - Generates N responses, then picks the best based on a metric (like logic or relevance).

**Why it matters:**

Fine-tuning these parameters lets you control if you want precise, safe outputs or more creative, diverse text.

---

### **3. Accelerating Inference (Making LLMs Faster and Cheaper)**

As LLMs get bigger, making them fast, cheap, and practical is crucial.

**A. Output-Approximating Methods**

May slightly change output, but speed things up a lot.

- **Quantization:**
    - Uses fewer bits for computations (e.g., 8-bit instead of 32-bit floats), reducing memory and speeding up inference.
- **Distillation:**
    - Trains a smaller “student” model to mimic a larger “teacher” model’s output.
    - Example: Gemini Nano uses this to stay small but high-quality.

**B. Output-Preserving Methods**

No change in output—just faster.

- **Flash Attention:**
    - Optimizes the core attention calculation, reducing time and memory usage.
- **Prefix Caching (KV Cache):**
    - Remembers already-processed parts of the input, so repetitive work isn’t redone, especially useful in chat or document processing.
- **Speculative Decoding:**
    - A smaller model “guesses ahead,” and the big model checks/accepts those guesses, speeding up generation.
- **Batching & Parallelization:**
    - Process multiple requests at once or split work across many processors for efficiency.

**Why it matters:**

These methods enable LLMs to serve more users, with lower costs and faster responses—critical for real-world applications.

---

### **Summary Table**

| **Technique Category** | **Method/Example** | **What it does** | **When to use** |
| --- | --- | --- | --- |
| Prompt Engineering | Zero-shot, Few-shot, CoT | Directs model output | Task guidance, reasoning |
| Sampling | Top-K, Top-P, Temp, BoN | Controls creativity and accuracy | Text generation, Q&A |
| Output-Approximating | Quantization, Distillation | Makes models smaller/faster | Resource-limited environments |
| Output-Preserving (Fast) | Flash Attention, KV Cache, Speculative Decoding | Speeds up inference, no quality loss | All real-time deployments |
| General Optimization | Batching, Parallelization | Increases throughput and efficiency | High-load systems |

## Practice Questions

??? question "1. What does a large language model do, and what architecture are modern LLMs based on?"

    It predicts the probability of a sequence of words. Modern LLMs are based on neural models called Transformers, which evolved from RNNs such as LSTM and GRU.

??? question "2. Why did Transformers replace RNNs?"

    RNNs process sequences one step at a time, so they are compute intensive and hard to parallelize. Transformers use self-attention to process the whole sequence in parallel, so they train faster and parallelize more easily (though the cost of self-attention is quadratic in the context length).

??? question "3. What are the encoder and the decoder responsible for?"

    The encoder processes the input sequence into a context-rich series of embedding vectors (Z). The decoder generates the output text token by token (autoregressively) using that representation.

??? question "4. How does self-attention work?"

    Each input embedding is multiplied by learned weight matrices to make query, key, and value vectors. The dot product of a query with all keys gives scores, which are scaled by the square root of the key dimension and passed through softmax to get attention weights. The value vectors are multiplied by those weights and summed to give a context-aware representation for each word.

??? question "5. What is the difference between training and inference?"

    Training adjusts the model's parameters using huge datasets and needs very high compute, done once per model (or fine-tuning). Inference uses the trained model with fixed parameters to answer a new prompt, is much cheaper, and happens every time you use the model.

??? question "6. How do decoder-only, encoder-only, and encoder-decoder models differ?"

    Decoder-only models (the GPT family) predict the next token and are good at generation. Encoder-only models (BERT) use masked language modeling and are strong at understanding but can't generate text. Encoder-decoder models (T5, the original Transformer) convert an input sequence into an output sequence, for example translation.

??? question "7. What did Chinchilla show about scaling?"

    For a fixed compute budget, parameters and training data should be scaled together. Chinchilla (70B parameters, about 1.4 trillion tokens) outperformed the much larger Gopher (280B parameters, about 300B tokens).

??? question "8. What is a Mixture of Experts (MoE) model?"

    An architecture that combines multiple specialized sub-models (experts). A gating network (router) decides how much each expert contributes, and only a subset of experts is activated per input (sparse activation), which makes very large models more efficient.
