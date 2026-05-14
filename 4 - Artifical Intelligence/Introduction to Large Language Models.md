---
title: LLM
aliases:
  - Introduction to Large Language Models
tags:
  - fb20
  - master
  - 6CP
description: ""
draft: false
---
[https://frankniujc.github.io/teaching/intro2llm/](https://frankniujc.github.io/teaching/intro2llm/)

ES GIBT AUFZEICHNUNGEN

---

# Klausurfragen

Wissensfragen

- Was ist ein Morpheme mit Beispiel
- Was sind zwei Ansätze von parameter-efficient fine-tuning
- Vergleiche F1 mit Accuracy
- Hauptunterschied zwischen decoder self-attention und encoder self-attention
- Instrinsic vs extrinsic evalution
- Beste Architectur in diesem Anwendungsszenario
- Warum ist Tokinize schwer bei diese Anwendung
- N-Gram Problemlösung mit OOV
- Was ist Instruction Tuning und wie macht man das
- Bestandteile von HMM
- Unterschied information need and a query
- word embeddings vs. one-hot encoding
- RNNs vs. Transformer
- CNN und ngram modeling / How does a 1D CNN process textual input
- Wie wird BERT in IR integriert
- mono-stage vs. a duo-stage ranking
- Imagine you are designing a re-ranking system for a legal document retrieval task. Discuss two specific challenges that you expect compared to general web search, and two approaches how you might adapt neural re-ranking models to this domain.
- HNSW erklären

Rechenfragen

- Tokinazition
- Tf, IDF, TF-IDF
- Inverted Index
- HMM / Viterbi
- Precision/Recall/Accuracy/F1
- ranked evaluation metrics (MRR, AP, nDCG@X)
- Byte-Pair Encoding

# IR – Neural IR

## Simple Neural Techniques

### CNN

Sliding window aproach

Es ist nicht feasable für jede wort kombination ein embedding zu lernen, daher werden CNNs benutzt um dynamisch 2-gram embeddings zu erstellen

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/d91acd54-a7c0-4102-a8dc-9620efc19aa9/image.png)

### RNN

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/eafbcb3e-87a1-46ae-a9ec-637af32ebc50/image.png)

### Encoder - Decoder Architecture

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/f0af8123-a7c9-4260-bf21-ae3dbab1ba25/image.png)

Attention

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/03592aa2-dcd0-4440-bda9-72e01f0ffce0/image.png)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/5c5ba1dc-cc9c-4489-87d5-eb29e14d4d62/image.png)

## Transformer Architecture

### Bidirectional Encoder Representations from Transformers (BERT)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/7b23427a-6657-440f-8693-c8779f5f15b7/image.png)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/511d7e77-c185-4520-a029-37e02352f64c/image.png)

# IR – Dense Retrieval

## Dense Retrival

### Neural Re-Ranking

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/a09bec0b-84b2-4999-9335-a0c147672050/image.png)

### Dense Retrieval (with Re-Ranking)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/3cfc7e88-1591-49a3-a0b1-0c2589c76f8c/image.png)

Reranking kann auch weggelassen werden falls dense retrival gut genug

## Training

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/66bde0af-4257-4b88-b0d9-4fca036f8417/image.png)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/5aa6019f-1711-4de4-bcfe-b64d70ca8e9d/image.png)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/820ea5eb-761f-4825-bbae-2e6430e87fe5/image.png)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/e8e07571-b891-4fe5-82c1-0f6b73c961d0/image.png)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/301f65df-c317-40bf-b50c-7d87ac279201/image.png)

## BERTDOT Model

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/d5b80491-b203-4168-8270-e1540f504a80/image.png)

## Indexing Techniques

### Flat Index

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/31cd6bfb-f62d-4ac7-9f84-feb46633c8e9/image.png)

### Inverted File Index (IVF)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/b23f4b08-fd62-4376-8d30-f66d0f311742/image.png)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/4bc2c517-8006-491d-9c4e-724d0d139aca/image.png)

### Product Quantization

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/1b873f48-1f9e-4ce4-9856-d5137d33cdc6/image.png)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/7a39ce3d-edeb-48e0-99c0-be1302b8847d/image.png)

### Graph Indices

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/7ff2088c-d7df-4755-baf5-30a657b83ae2/image.png)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/98763598-4cdf-4c64-ad04-94c4f62a4743/image.png)

## Knowledge Destillation ****

## DistilBERT

Kleineres Bert Modell aber trotzdedm effizient durch Training mit knowledge distillation

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/5e4c9cf2-3006-494c-8dcc-86ef8f32e97a/image.png)

# IR - Neural Re-Ranking

## Neural Re-Ranking

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/d41b2ac8-0510-46a5-914d-3a41c8ba32b8/image.png)

Training wie bei Dense Retrival

Wichtig: Training Loss ist nur am Anfang relevant und hat später weniger ausagekraft. Dannach eher MME oder so beachten

### Cosine similarity

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/73d48cc9-cab8-48aa-b84d-f598f820fa59/image.png)

### Basic MatchPyramid approach

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/8c214e20-d126-42a8-b7bf-e6e20d9f979f/image.png)

1. Encoding Layer := Wörter werden mit Vektoren ersetzt
    
2. Match Matrix
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/29622a93-b586-4f9d-9137-c1c5f22fdf07/image.png)
    
3. CNN Layer := 2D-CNN hinzufügen
    

## BERT Re-Ranking

### BERT_CAT

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/895235b3-c9fc-4a0e-a857-463ff2dda7c8/image.png)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/f475da39-d163-40f7-9e86-749a79c1e678/image.png)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/91b324f7-1e85-4719-899e-78075e6fab74/image.png)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/631d1a49-bc55-40bd-a025-1dcfc4979a85/image.png)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/f58ac6ae-15bf-452c-b0c4-81e233cd6767/image.png)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/ef07e693-7e9b-40b1-b570-a942509dd4e7/image.png)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/d54ae6a5-103a-4b21-aec2-4ded790463d9/image.png)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/034fd148-6540-49ae-89fb-22ee7282e285/image.png)

# LLMs Grundlagen

LLMs weisen Sätzen eine Wahrscheinlichekeit, dass Sie in einem Text auftreten zu. Mögliche Benutzungsstenarien:

- Spracherkennung/Rechtschreibung := Erhaltene Sätze werden korrigiert wenn sie sehr unwahrscheinlich sind und zu einem neuen Satz verwandelt der wahrscheinlicher ist
- Sprach-Gererierung

### N-Gram Models

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/58c28419-09aa-44d9-8441-a92862d1079b/image.png)

Das Problem ist, dass viele Sätze selten bis garnicht vorkommen und man über viele Wahrscheinlichkeiten nur schlecht aussagen treffen kann

Lösung: Wie limitieren den Kontext nur auf die k-Tokens davor und nicht alles (markov assumption)

Zudem werden Wahrschienlichkeiten immer kleiner und sind daher anfällig für underflow → Lösung ist log

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/2d18e0da-8245-44a8-9649-c4667fc6aabe/image.png)

### Evaluation

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/3eb0352d-66db-4bfa-9df8-813dfaeb64ae/image.png)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/c7cdbe20-be57-4c53-8c98-6bfeb1714ebc/image.png)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/693aeb93-3767-45d0-900d-2e04512b260f/image.png)

### Generation with N-Gram Models

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/2736a67c-d152-4cd7-9590-5a794ca103dd/image.png)

### Out-Of-Vocabulary Problem

- UNK token verwenden für unbekannte Worte
- Smoothing := Einfach Wahrscheinlichkeiten hinzudichten
    - - 1 überall aber muss ausgeglichen werden
    - - k nicht 1 sonder fraktion adden
- Backoff := wenn n-gram nicht existiert dann in n-1 aufteilen und suchen usw. bis gefunden
- Interpolation := verschiedene n-gram gewichtet addieren
- Subword-tokenization := BytePairEncoding/WordPiece/SentencePiece

WordPiece

Merged nicht einfach die häufigste Kombination sondern merged die Tokens deren Kombination sehr wahrscheinlich vorkommt (also mehr oder weniger umgekehrt)

SentencePiece

Sieht Leerzeichen auch als Tokens (bei BPE und WordPiece nicht so)

# Neural LLM

## Basic Neural Language Models

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/40db501a-d640-48fe-aec7-4a076e3d8dda/image.png)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/77c2ab53-29fb-4adb-beab-818059a41a60/image.png)

## RNN and Transformer LM

### RNN

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/582bcdc8-ea42-46d0-8c61-06322bd446b2/image.png)

- Beliebige input länge
- Forget long inputs
- Vanishing/Exploding Gradients
- Schwer zu parallelisieren

### Transformer

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/099db68c-690f-4ec0-bfea-a809b0a26170/image.png)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/242aa1c9-4428-4a72-bdfa-e38e60dd0261/image.png)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/175d244a-d41f-402c-92e5-db10fb91c840/image.png)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/8c673a48-24b0-433d-b3c3-ee63dc37a85a/image.png)

Lösung attention mask

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/a0949391-5249-4470-8906-b97c9ebdf566/image.png)

# LLM Adaptation

LLMs werden mit Aufgaben traniert, welche nicht der letzendlichen Nutzeranwendungen entsprechen.

### Tuning

- Whole model tuning := ALLE Parameter des Models werden trainiert
- Head-tuning := Nur eine bestimmte Schicht des Models wird trainiert

### Parameter-efficient Fine-tuning

- Adapters := Füge eine Adapterschicht hinzu, welche nur trainiert wird. (Speichereffizienter als whole-model aber trotzdem aufwändig zu berechnen weil ganzer pass nötig)
- Selective := Wählt bestimmte Komponenten des bestehenden Models zum trainieren aus (BitFit nimmt zum Beispiel nur Bias)

### Prompting

Backlog:

* SkipGram, CBOW, Glove
* Transformer, Positional Encoding, Scaled Dot PRoduct Attention, Multi Head Attention, Feed Forward Network, Layer normilazition, Decoer and encoder block
* T5 Encoder, Cross Attention
* GPT casual mask, self attention

# Klausuraufgabensammlung

Here are the solutions to the HW5 Problem Set in Obsidian format.

# Intro2LLM - HW5 Review Problem Set Solutions

## Task 1: Multiple Choice Questions

|**Question**|**Answer**|**Explanation / Citation**|
|---|---|---|
|**1**|**C**|Semantics is concerned with the study of meaning.|
|**2**|**C**|Dependency parsing focuses on word relationships (head $\to$ dependent), while constituency parsing uses hierarchical trees.|
|**3**|**B**|Homonymy is when meanings of a word are unrelated (e.g., bank/bank).|
|**4**|**B**|ELIZA used keyword processing and simple pattern-matching rules.|
|**5**|**C**|Recall is the number of relevant items selected divided by the total number of relevant items.|
|**6**|**B**|BM25 contains a saturation function, whereas TF-IDF grows linearly/logarithmically without a cap.|
|**7**|**C**|MRR (Mean Reciprocal Rank) focuses on the rank of the _first_ relevant document.|
|**8**|**C**|Count-based vectors (like TF-IDF) are sparse vectors (mostly zeros).|
|**9**|**A**|CBOW predicts context words given a center word (Note: The option A says "Predict context... given center", actually Skip-gram predicts context, CBOW predicts center from context. However, based on the provided options, option A is the standard inversion description or B "Predict a word given its bag-of-words context" is the precise definition. Let's look closer at B. B says "Predict a word given its bag-of-words context". This is the definition of CBOW. Option A describes Skip-Gram. **Correction:** The correct answer is **B** based on standard definitions, but let's re-read the options carefully. Option A: "Predict the context words given a center word" (Skip-gram). Option B: "Predict a word given its bag-of-words context" (CBOW). **Answer is B**).|
|**10**|**A**|Global embeddings (GloVe) are one vector per word-type; Contextual (BERT) are one vector per token based on surroundings.|
|**11**|**C**|The operation is the Dot product (often scaled) of Q and $K^T$.|
|**12**|**B**|Necessary because the self-attention mechanism is permutation invariant.|
|**13**|**C**|GPT family uses Decoder-only architecture.|
|**14**|**B**|The model creates a "task vector" from demonstrations that encodes task information.|
|**15**|**B**|CoT involves providing examples that include intermediate reasoning steps.|
|**16**|**B**|Using multiple sampled reasoning paths and taking a majority vote.|
|**17**|**C**|Distraction is when irrelevant retrieved context causes an incorrect answer.|
|**18**|**C**|Knowledge is hypothesized to be stored in Feed Forward MLP layers.|
|**19**|**B**|Every answer must be a span found directly in the passage.|
|**20**|**B**|"Man is to Computer Programmer as Woman is to Homemaker" is the bias example.|

---

## Task 2: Short Answer Questions

**1. What is a language model?** A language model is a probabilistic model that assigns probabilities to sequences of words.

**2. What does "Zero-shot" prompting mean?** It means prompting the model to perform a specific task without providing any examples or demonstrations.

**3. What does the acronym "RAG" stand for in the context of Large Language Models?** Retrieval-Augmented Generation.

**4. What is the mathematical purpose of the Softmax function in the output layer of a neural network?** It converts the raw output logits into a valid probability distribution (where probabilities sum to 1).

**5. How does increasing the Temperature $(\tau > 0)$ affect the text generated by a language model?** Increasing temperature flattens the probability distribution, making the generated text more random and diverse.

---

## Task 3: Transformer

### 3a) Tokenization (BPE)

**Context:**

- Initial Vocabulary: `{b, e, h, i, n, o, r, s, t, w}`
    
- Corpus:
    
    - `w o r s e` (10)
        
    - `h o r s e` (5)
        
    - `w o r s t` (5)
        
    - `b e h i n d` (2)
        

**1. BPE Iteration 1**

- **Pairs and Frequencies:**
    
    - `o r`: 10 (worse) + 5 (horse) + 5 (worst) = **20**
        
    - `r s`: 10 (worse) + 5 (horse) + 5 (worst) = **20**
        
    - `w o`: 10 + 5 = 15
        
    - `s e`: 10 + 5 = 15
        
    - (Others have lower frequencies)
        
- **Merge Decision:** The tie is between `or` and `rs`. Alphabetically, `o` comes before `r`.
    
- **Result:** The pair **`or`** is merged first.
    

**2. BPE Iteration 2**

- **Updated Corpus:**
    
    - `w (or) s e` (10)
        
    - `h (or) s e` (5)
        
    - `w (or) s t` (5)
        
    - `b e h i n d` (2)
        
- **New Pairs and Frequencies:**
    
    - `(or) s`: 10 (worse) + 5 (horse) + 5 (worst) = **20**
        
    - `w (or)`: 10 + 5 = 15
        
    - `s e`: 10 + 5 = 15
        
- **Result:** The pair **`ors`** (merging the symbol `or` with `s`) is merged next.
    

**3. Handling Morphology**

- **Answer:** Subword approaches are superior for complex words (like German compounds) because they can segment unseen, rare words into meaningful, frequent sub-units (like "Recht", "Schutz", etc.) seen during training, rather than treating the entire complex word as an "Unknown" (`<unk>`) token.
    

### 3b) Transformer Math

**Notations:**

**Q1: The Residual Stream (Simplified)**

Assuming a block is Attention followed by MLP, and ignoring Layer Norm:

1. Intermediate state: $z = x_l + Attn_l(x_l)$
    
2. Output state: $x_{l+1} = z + MLP_l(z)$
    

Combined equation:

$$x_{l+1} = x_l + Attn_l(x_l) + MLP_l(x_l + Attn_l(x_l))$$

**Q2: Layer Normalization**

Layer Normalization normalizes the inputs across the features for each token independently to have mean 0 and variance 1, then scales and shifts them.

Equations:

$$\mu = \frac{1}{d} \sum_{i=1}^{d} x_i$$

$$\sigma^2 = \frac{1}{d} \sum_{i=1}^{d} (x_i - \mu)^2$$

$$y = LN(x) = \gamma \odot \frac{x - \mu}{\sqrt{\sigma^2 + \epsilon}} + \beta$$

**Q3: Scaled Dot-Product Self-Attention**

1. **Linear Projections:**
    
    $$Q = X W_Q$$
    
    $$K = X W_K$$
    
    $$V = X W_V$$
    
2. **Attention Weights:**
    
    $$\text{Scores} = \frac{QK^T}{\sqrt{d}}$$
    
    (Note: The scaling factor is $\frac{1}{\sqrt{d}}$ or $\frac{1}{\sqrt{d_k}}$).
    
3. **Attention Output:**
    
    $$\text{Output} = \text{softmax}\left( \frac{QK^T}{\sqrt{d}} \right) V$$
    

---

## Task 4: Word Sense Disambiguation

**Sentence (S):** "The worker left the chemical plant."

**Sense 1 ($D_1$):** "A living organism of the kind exemplified by trees."

**Sense 2 ($D_2$):** "A building where chemical manufacturing processes occur."

### 1. Preprocessing

Constraint: Lowercase; remove `{the, a, by, of, where}`. Keep others.

- **Bag(S):** `{worker, left, chemical, plant}`
    
- **Bag($D_1$):** `{living, organism, kind, exemplified, trees}`
    
- **Bag($D_2$):** `{building, chemical, manufacturing, processes, occur}`
    

### 2. Simplified Lesk Algorithm

Task: Compute overlap between $S$ and Definitions (excluding target word "plant").

- **Overlap($S, D_1$):**
    
    - $S$ terms: `worker, left, chemical`
        
    - $D_1$ terms: `living, organism, kind, exemplified, trees`
        
    - **Score:** 0
        
- **Overlap($S, D_2$):**
    
    - $S$ terms: `worker, left, chemical`
        
    - $D_2$ terms: `building, chemical, manufacturing, processes, occur`
        
    - Match: "chemical"
        
    - **Score:** 1
        

**Result:** The algorithm assigns **Sense 2 (Industrial)**.

### 3. Vector Space Model

**Vocabulary:** $V = [\text{worker}, \text{chemical}, \text{organism}, \text{building}]$

**Vectors:**

- $\vec{v}_S = [1, 1, 0, 0]$
    
- $\vec{v}_{D2} = [0, 1, 0, 1]$
    

**Calculation:**

1. **Dot Product:**
    
    $$\vec{v}_S \cdot \vec{v}_{D2} = (1 \cdot 0) + (1 \cdot 1) + (0 \cdot 0) + (0 \cdot 1) = 1$$
    
2. **Magnitudes:**
    
    $$||\vec{v}_S|| = \sqrt{1^2 + 1^2 + 0^2 + 0^2} = \sqrt{2}$$
    
    $$||\vec{v}_{D2}|| = \sqrt{0^2 + 1^2 + 0^2 + 1^2} = \sqrt{2}$$
    
3. **Cosine Similarity:**
    
    $$\text{Sim}(S, D_2) = \frac{\vec{v}_S \cdot \vec{v}_{D2}}{||\vec{v}_S|| \cdot ||\vec{v}_{D2}||} = \frac{1}{\sqrt{2} \cdot \sqrt{2}} = \frac{1}{2} = 0.5$$
    

**Result:** 0.5








# Final prepare
Wichtige Konzepte

## Basics
* What is Computational Linguistics (CL) / NLP := How we can build computer systems that can understand and use human langugage
* What is LM := Estimate the likelihood of sequence of texts, Model that assigns probabilities to sequences of words.
* Language Modelling Pipeline := 
	1. Collect Data
	2. Tokenize
	3. Modelling Task (Next Word Prediction, Masked Language Modeling)
* Intrinsic: Query und gewollte Lösungen sind gegeben und werden als Benchmark verwendet
* Extrinsic: Benutzer nutzen den Suchdienst und man schaut wie effizient sie aufgaben lösen können usw.
* SuperGLUE := benchmark für challenging NLP tasks (QA, WSD, NLI)
* Transfomrers gut für := Protein Folding, Image Classification, Climate Research
* SQuAD (Stanford question answering dataset) := (Pasage, question, answer)
## Cross entropy loss
![[Pasted image 20260223120445.png]]
## Linguistik
* Study of language
### Phonetics
* How speechsound are physically produced and percieved
### Phonology
* How sounds are mentally organised and patterned with in a language
### Motphology
* Study of words
* Morphem kleines Sinn beinhaltende einheit
* 2 Types Morphologie
	* Inflectional Morphology -> How words change their form (to walk, walking, walks, ...)
	* Derivational Morphology -> New words are created (happy, unhappy; teach, teacher)
### Syntax
* Study of word order
	* regulariteis and constraints of word order and phrase structure (Manning & Schütze, 2003, p. 93)
### Semantik
* Study of meaning
### Pragmatic
* Study of language in use
	* J: I find X boring -> M: Me <span style="color:rgb(192, 0, 0)">too</span>
	* Too ist ein social que und nur hier bei der benutzng hat es eine bedeuteung aber nicht alleinstehend
### Discourse
* Study of the structure of text and dialogie
* How different sentences and paragrapphs form a bigger narrative (Thompson et al. (2024 ) Discourse Structure for the Minecraft Dialogue Corpus)
### Tokenization
* Segmenting an input stream into an ordered sequence of units
* Challenging weil viele verschiedene Sprachen
* Primär text verständlich für maschinen machen
### WordNet
* Hierarchical lexicon and thesaurus of english
* Graph structure
	* Nodes: synsets (Wort bedeutungen)
	* wn.synsets('dog')
### Parts of Speech (PoS)
* Verbs := sleep, eat, sell, ...
* Determiners := the, a ,some
* Preposition := up, at, before
* Adverbs := today, very, happily
* Conjunctions := and, or, because
* Interjections := um, wow, oh dear
Combinations
* Phrase := hierarchical grouping of words
	* NP := a mouse
	* VP := give the book to Mary
	* AdjP := very happy that you went
	* PerposP := in the sink
* Clause := phrase of verb and almost all its dependents
* Sentence := syntactically independent clause
### Ambiguity
*Lexical
* Homonym: Gleich geschrieben aber andere Bedeutung (Bank)
* Homophony: Gleicher Sound aber verschiedene Bedeutung (wwod, would)
* Polysemy: Gleich geschrieben aber mehre Ähnliche Bedeutungen (line of people, line drawn  on paper)
*Syntactic*
* Ich sah den Polizist mit Fernrohr
	* Polizist hat Fernrohr oder Ich
*Semantic*
* Sätze können mehrdeutig sein bei gleicher Syntax
*Pragmatic*
* Do you know who's coming to the party? (Entweder wirklich nachfragen oder rhetorische Frage weil jemand krasses kommt)
### How to solve Ambiguity
Three tricks:
* context is not ambigious
* use one sense per discourse
* Lesk Algorithm
#### Lesks Algorithm
* Sense si of ambiguous word w is likely to be the intended sense if many of the words used in the dictionary definition of si are also used in the definitions of words in the context window.
* Choose the sense si that maximizes overlap(Di, B).

* Grammar
* Dependency Grammar, Word Dependency Parsing
* Yamadas Algorithm
### Dependency Parsing
Raw sentence -> PoS Tagging -> Dependency parsing
#### Formal Conditions on Dependency Graphs
• G is (weakly) connected:
	•For every node i, there is a node j such that i -> j or j -> i
• G is acyclic:
	•If i -> j then not j -> * i
• G obeys the single-head constraint:
	•I fi -> j, then not k -> j, for any k != i
• G is projective:
	•If i -> j then i ->* k for any k such that i < k < j or j < k < i
* No crossing edges.
* Wird oftmals vernachlässigt weil lange abhängigkeiten das brechen
#### Yamada's
Hat Stack + Queue und drei Operationen
* Shift := nimmt Wort aus Queue und packt es an Stack Ende
* Right := nimmt letztes wort aus stack. letztes wrt dann abhängig zu vorletzen wort.
* Left := nimmt vorletztes wort aus stack. vorletztes wrt dann abhängig zu letzen wort.
## CosSim
$$\text{cos}(\theta) = \frac{\mathbf{A} \cdot \mathbf{B}}{\|\mathbf{A}\| \|\mathbf{B}\|} = \frac{\sum_{i=1}^{n} A_i B_i}{\sqrt{\sum_{i=1}^{n} A_i^2} \sqrt{\sum_{i=1}^{n} B_i^2}}$$
## Dot Product
a * b = a1 * b1 + a2 * b2 + a3 * b3 + ...

## IR
information need: An information need is a user's underlying goal
query: query is the specific formulation of that need in a search system
![[Pasted image 20260212222343.png]]
### Inverted Index
Statistiken sind für jeden Term gespeichert:
- DF := wieviele Dokumente enthalten Term
    - Terme die eher selten vorkommen sind in der Regel relevanter für die Suche
    - daher: log(|D| / df)
- TF := Wieoft Term in einem Dokument
    - meistens log(1 + tf) weil länge dokumet normalisieren
- PostingList := Jeder Term hat eine eigene Liste in der steht in welchem Dokument und wie oft der Term auftritt
### Arten von queries
- Exact matching: match full words and concatenate multiple query words with “or”
- Boolean queries: “and” / “or” / “not” operators between words
- Expanded queries: automatically incorporate synonyms and other similar or relevant words into the query, kann durch word embeddings gemacht werden
- Wildcard queries, phrase queries, phonetic queries (e.g. Soundex) …
### TF-IDF
- Würd generell für Wortgewichtung in anderen Anwendungen verwendet
![[Pasted image 20260212222402.png]]
### BM25
Im gegensatz zu TF-IDF ist die Funktion schnel gesättigt und daher besser in praxis???
TF IDF weight always increasing

k1 bestimmt skalierung von tf (0 = binary, groß = raw)
b bestimmt dokumentenlänge nomralisierung (0 = keine normalisierung, 1 = relative tf)
![[Pasted image 20260212222421.png]]

### Latent Semantic Analysis (LSA)
* TF-IDF is actually pretty stupid:
	* Car vs cars → lemmatisation, wordnet…
	* Car vs automobile → different tokens!
	* No generalisation
* TF-IDF is very sparse:
	* We need to keep track of an M x N matrix of token frequencies
Basic idea: use singular value decomposition (SVD) to
encourage generalization. (Also andere Darstellung für Wörter)
![[Pasted image 20260221180559.png]]
![[Pasted image 20260212224627.png]]
![[Pasted image 20260212224829.png]]
### Evaluation
Intrinsic: Query und gewollte Lösungen sind gegeben und werden als Benchmark verwendet Extrinsic: Benutzer nutzen den Suchdienst und man schaut wie effizient sie aufgaben lösen können usw.
![[Pasted image 20260212225152.png]]
* You can increase recall (R) by returning more documents
	* A system that returns all docs has 100% recall!
* The converse is also true: It’s easy to get high precision (P) for very low recall

![[Pasted image 20260212225217.png]]
### MRR: Mean Reciprocal Rank (binary relevance)
![[Pasted image 20260212225231.png]]
### MAP: Mean Average Precision (binary relevance)
![[Pasted image 20260212225248.png]]
![[Pasted image 20260212225305.png]]
Immer durch die relevante Dokumente in gesamter collection teilen

### nDCG: normalized Discounted Cumulative Gain (non-binary relevance)
![[Pasted image 20260212225319.png]]
![[Pasted image 20260212225332.png]]











## Wortdarstellung
### Wie können wir text darstellen?
* One Hot encoding
	* Problem es gibt viele Worte und daher ist Vektor super lang
	* Alle wörter sind semantisch gleich → schlecht
	* Lösung context analysieren
### Distributional similarity based representations
* You can get a lot of value by representing a word by means of its neighbors
* The meaning of an unclear or ambiguous word should be determined by considering the words with which it is associated in the context.
### Zwei vektoren für Wort darstellung
* Count
	* man zählt einfach wörter (tf-idf, LSA) also wie oft wort in dokumenten
	* wörter werden drch die counts der nearby words dargestellt
	* sparse
* Predict
	* word2vec, GloVe, BERT, GPT-2, GPT-3, GPT-4…
	* Dense
	* Representation is created by training a classifier to predict whether a word is likely to appear nearby
	* Contextual embeddings
Count
+ Fast training
+ Efficient usage of statistics
+ Long & Sparse!; Length = |V|; most elements are zero
+ Primarily used to capture word similarity
+ Disproportionate importance given to small counts
Prediction
* Scales with corpus size
* Inefficient usage of statistics
* Short and Dense
• Length = any hidden size (50-10000)
• Nearly nothing is zero
* Generate improved performance on other tasks
* Can capture complex patterns beyond word similarity
### Word2Vec
Wörter als Vektoren darstellen mit lokalen Kontext fenster. Es gibt zwei Varianten:
#### CBOW (Continuous Bag of Words)
* Predict a word given its BoW context
* Ignoriert wort reihenfolge
#### Skip-Gram
* Aus einem Wort wird der Kontext vorhergesagt.
### GloVe
![[Pasted image 20260222120629.png]]
Benutzt globale Wort Kookkurrenz Matrix. Also zählt im gesamten Korpus das gemiensame auftreten.

## RNN
Hidden state sollt ein der theorie gesamten context capturen aber Problem vanishing gradients

Pro Layer immer als Input:
1. h_state (am anfang alles 0 oder random)
2. Input (One-Hot, Word Embedding)

Und dann:
1. input = (input_size, h_size) (input)  # embedding layer
2. h_state = (h_size, h_size) (h_state)
3. neuer h_state = tanh(input + h_state)
4. out = (h_size, output_size) (neuer h_state)

![[Pasted image 20260222174038.png]]

## Softmax
![[Pasted image 20260222123417.png]]
![[Pasted image 20260222215756.png]]
## Byte-based rokenization
* Bytes selbst werden encoded und nicht buchstaben oder subwords
* Spezifisch für eine Sprache
* Modularity
## Attention + Transformer
Transformer Evolution:
Decoder -> Encoder -> Encoder-Decoder -> Decoder
![[Pasted image 20260222224006.png]]

![[Pasted image 20260222180818.png]]
![[Pasted image 20260222215359.png]]
### Positional Embedding
Sin für gerade und cos für ungerade
![[Pasted image 20260222182449.png]]
### Residiual Stream
![[Pasted image 20260222181108.png]]
 Auch:
![[Pasted image 20260222222951.png]]


### Layer Normilization
![[Pasted image 20260222181347.png]]

### Scaled Dot Product Attention
![[Pasted image 20260222181558.png]]
![[Pasted image 20260222183541.png]]
### Attention Head
![[Pasted image 20260222223743.png]]
## RoPE
![[Pasted image 20260222183013.png]]
![[Pasted image 20260222183027.png]]
![[Pasted image 20260222183042.png]]
## Decoders vs Encoders vs Encoder-Decoders
### Decoder
![[Pasted image 20260222183231.png]]
### Encoder
![[Pasted image 20260222183252.png]]
BERT wird trainiert mit masked language modelling
* random token masken
* ersetzen mit mask, correkt word or random
### Encoder-Decoders
![[Pasted image 20260222183323.png]]
#### T5 - Text to Text Transfer Transformer
* Training := replace spans of input wit placeholders 

## Wie Natural Language Understanding Task lösen?
Evolution
Rule-based -> Statistical models -> BERT (pretrain and finetune) -> LLM (in context learning usw)

NLU lösen als classificcation tesk
* Input word embeddings
* output: alles haha

Also Architektur immer Transformer + Classifier
GPT ist jetzt anders
## Bayes and chainrule
![[Pasted image 20260222213615.png]]
![[Pasted image 20260222213827.png]]
## Scaling Laws
Testloss sinkt mit größerem Compute, Dataset Size und Parameters
## OpenAI tut Dinge
* No more finetuning
* Keep scaling
* Keine classifiers nur noch in context learning
* Zuviele Parameter als nötig
## In context learning (ICL)
Zero, few shot usw
## Chain of thought
## Parameter efficient fine tuning (PEFT)
* Aktuelle Modelle are massively over parameterized
* Nur kleines subset finetunen
Ansatz ist das man matrix in kleinere matrizen zerlegen kann wenn rank klein ist M = UV
![[Pasted image 20260222220435.png]]
Da LLM Gewichte low rank und auch dessen updates
![[Pasted image 20260222220548.png]]

## AI Handlungen erklären
Explainability := Warum hat KI bestimmte prediction gemacht
Interpretability := Understand AI System, Revrese engineer an AI System, Interpret LLMs
![[Pasted image 20260222221939.png]]

### LLM as a whole
![[Pasted image 20260222222114.png]]
### Layer Level
* Früher dachte man Bert layer lernene die klassiche NLP Pipeline
	* tokenizer, tagger, parser, ner, ...
* Aber stimmt nicht lol
### GridLoc Probing
GridLoc Probing ist ein Analyseverfahren, bei dem man aus den Hidden States eines Transformers vorhersagt, an welcher Position sich ein Token im Satz befindet. Dadurch kann man messen, wie stark und in welchen Layern absolute Positionsinformation im Modell kodiert ist.
### Neuron Level
* Knowledge Neuron Thesis := Facts in LLM sind in Feed Forward MLP
	* Auch nichtz wirklich wahr und vereinfachung
	* Speichern eher komplexe muster und nicht wirklich wissen
### Circuit Discovery
## Neural Re Ranking
Ordner ein Ergebnis neu durch matching
* Sind trainiert mit query, relevant und non relevant data
### BERT CAT (monoBERT, vanilla BERT)
* Bekommt [CLS] query [SEP] passage als input
* CLS token ist dann score
![[Pasted image 20260223105746.png]]

## Query Types
Factoid questions
* When was the 43. president elected
Narrative (open-ended) questions
* Tell me a story about the rise in interest for X
Complex/hybrid questions
* Kombiniert 1 und 2
## Dense Retrival
Ersetzt auch erste Stage (BM25 oder so) mit BERT DOT oder ähnliches und benutzt kein Neural Re ranking
### Lifecycle
1. Training (z.B. BERT DOT)
2. Indexing (Collection in nearest neighbor indexing)
3. Searching (Score it DOT PRoduct)
* Documents werden einmal mit BERT DOT in VEctoren umgewandelt und abgespeichert und wueries weerden dynamisch bei anfrage in vector umgewandelt
![[Pasted image 20260223111208.png]]
### Indexing techniques
* Flat Index := Brute Force (einfach alle Paare vergleichen)
* Inverted File Index (IVF) := documente in cluster einteilnen und query nur mit centroids der cluster vergleichen; top cluster auswählen und dann wieder flat index
* Product Quantization
	* big float vector in kleinen int vector umwandeln
* Graph indices
	* Schichten auf denne immer ein graph ist
	* Wenn lokales minimum dann gehts in die nächste schicht


## LLM Agent
Agent := Intelligent Agent that interacts with environment
* Pyhsical or digital environment or human as environment

Multiple Levels of Agents
1. Text agent
	* Simple text action and obseervation like ELIZA
2. LLM agent
	* Use LLM to act
3. Reasoning agent
	* Use LLM to reason and to act
	* ReAct
## Solutions for Question Answering
### Code Augmentation for Computing (PoT Programm of Thought)
* LM can produce code and execute it then in an environment and therefor gains deterministicc results
### Retrival Augmented Generation (RAG)
* Use Information Retrival to get relevant Documents for query and augement initial user query
* 'Distraction' := Irrelevant documents can worsen the performance
	* Solutions for Distraction:
	1. Natrual Language Inference (NLI remove context that contradicts question
	2. LM Finetuning with relevant and irrelevant contexts
	3. Interleaving decomposition : Complex query is splitted into multiple simple queries

### Tool Calling
* Special Tokens for Searchengines, Calculators, ...


## Solution for Reasoning and Knowledge tasks -> ReAct
Reason and Act
* Reasoning update Internal beliefs and action + observation to plan next steps
![[Pasted image 20260221171637.png]]

## Code
```python
corpus = ['I did not hit her', 'I did not', 'Oh hi Mark'] #Korpus mit 3 Sätzen
ifidf = tfidf = TfidfVectorizer(stop_words='english') #entfernt stopwords

# erstellt tensor aus dense matrix
# Bei uns als Erbeniss (Anzahl Dokumente x Anzahl Wörter)
x = torch.tensor(tfidf.fit_transform(corpus).todense()) 
```

```python
Word2Vec:
	# Layer um one-hot vocab in embedding zumzuwandeln
	self.embed = EmbeddingLayer(vocab_size, embedding_size) 
	# Wieder expanden um das vocab zu predicten (meistens mit softmax)
	self.expand = LinearLayer(embedding_size, vocab_size)
```



![[Pasted image 20260221020917.png]]