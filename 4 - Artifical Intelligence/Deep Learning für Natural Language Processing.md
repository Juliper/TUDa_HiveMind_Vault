---
title: DL4NLP
aliases:
  - Deep Learning für Natural Language Processing
tags:
  - fb20
  - bachelor
  - semester-6
  - 6CP
description: ""
draft: false
---

## Formeln

### Metriken

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/19d7b082-e722-407a-a87c-afbf1c34e545/Untitled.png)

- Accuracy := $\frac{TN + TP}{Datasetsize}$
- Precision := $\frac{TP}{TP + FP} = P$
- Recall := $\frac{TP}{TP+FN} = R$
- F-1 := $\frac{2PR}{P + R}$

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/ec670b5c-6289-4281-a6fe-401c0205d3d8/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/fd9ab048-93ed-47a7-8f9f-b2a9887a4000/Untitled.png)

### Sigmoid (für Binaty Classification)

$$ \sigma(x)=\frac{1}{1+exp(-x)}=\frac{exp(x)}{exp(x)+1}\\ \sigma'(x)=\sigma(x)\cdot(1-\sigma(x)) $$

### Binary Cross Entropy / Loss Functions

- $L_{logistic} = -y~log~\hat{y}~ - (1-y)~log(1 - \hat{y})\\ L'_{logistic} = -\frac{y-\hat{y}}{\hat{y}(1-\hat{y})}$

### Softmax für normalisierung

- $softmax(x_{[i]})=\frac{exp(x_{[i]})}{\sum^K_{k=1}exp(x_{[k]})}$
- $softmax(x_{[i]};T)=\frac{exp(x_{[i]}/T)}{\sum^K_{k=1}exp(x_{[k]}/T)}$

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/52e10a3d-e9b9-4a71-908a-656d6d0d6cb2/Untitled.png)

### Loss für Softmax (Categorical cross-entropy loss (aka. negative log likelihood))

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/e17c5690-5123-4c60-9f19-5710ba2a374e/Untitled.png)

### ReLU Aktivierungsfunktion

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/83c74c9a-8bf6-4da4-ad50-f5b30512a2d8/Untitled.png)

## Begriffe

Supervised Learning

Self Supervised

- Distributional hypothesis := Wörter im selben Kontext sind ähnlich

Negative sampling

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/9f3ea963-16ab-4e83-9284-5addfc356419/Untitled.png)

Teacher Forcing := richtiger Input bei decoder wird vorgegeben damit Fehler nicht propagieren

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/8e01c7f8-640d-44e9-9723-509d83456ac7/Untitled.png)

CONTINUOUS PROMPTS := kein text als prompt sondern direkt vektoren

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/55fd5d18-f9c5-490c-846e-a70ce879ecb2/Untitled.png)

## Übungen

### 1. Übung

### Perceptron Training

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/5fe67f4a-f4de-4570-a14d-f8e4da22b2b5/Untitled.png)

Mittels Backpropagation Gradient/neue Gewichte berechnen

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/f7ccd8fa-403f-4562-bba7-4262838f13cf/Untitled.png)

Neues Gewicht = Altes - LearningRate * Gradient

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/9aff2ca0-cf93-456b-9dd5-55bdf009c988/Untitled.png)

### MLP Funktion

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/93afbd5b-b0ef-4886-9aef-0136608c5945/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/0520c556-c04b-4498-a760-203cc71ac136/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/7f6e3089-9c77-49d2-87dd-7c5487a4e60c/Untitled.png)

### 2. Übung

- Accuracy := $\frac{TN + TP}{Datasetsize}$
- Precision := $\frac{TP}{TP + FP} = P$
- Recall := $\frac{TP}{TP+FN} = R$
- F-1 := $\frac{2PR}{P + R}$

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/8241914d-4c6a-45ed-a782-5ce4005d1cc0/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/fd0ec28a-4412-43bf-8986-569a3d757dd9/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/f9ead5db-f17b-4479-b642-04b28e1b8fe9/Untitled.png)

### 3. Übung

### 4. Übung

### 5. Übung

## NLP Aufgaben

### Classification

- Sentiment classification := Labeling von Emotionen, Meinungen und Stimmungen von Text
- Standford Natural Language Inference (SNLI) := Bestimmen ob zwei Sätze sich wiedersprechen, bestärken oder neutral sind
- Recognizing Textual Entailment (RTE) := Bestimmen ob Text die Hypothese bestärkt (binary)
- Coreference resolution (WSC — Winograd Schema Challenge) := Bestimmen Was/Wen ein Pronomen refenziert
- BoolQ := Text mit Frage die mit Ja/Nein beantwortet werden soll
- MultiRC: Multi-Sentence Reading Comprehension := Text und mehrere Fragen mit möglichen Antwortenliste
- Extractive Question Answering: Text mit Fragen und Antwort in Form von Abschnitt des Texts sein

### Text generation

- translation
- Document summarization
- Dialogue: PersonaChat

### Name Entity Recognition (NER) / BIO Tagging

- O für Wörter ohne definierten Typen
- I-TYP für alle anderen
- Wenn zwei gleiche typen hintereinander zweiter startet mit B-TYP

## Evaluation

### Cross validation

- K-Fold := Data in K Teile splitten und K-1 für Training verwenden und bei jedem Fold durchrotieren

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/3a13ee18-2ac4-4872-9902-f28dc5400479/Untitled.png)

## Benchmarks

- SuperGLUE (Benchmark)
- BLEU (Bilingual Evaluation Understudy) := misst n-gram overlap
    - Nur Precision und misst nur exakte n-gram Übereinstimmungen
    - Für Machine Translation
- ROUGE (Recall-Oriented Understudy for Gisting Evaluation)

## Mathe

### Multivariablen Gradient Decent

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/79c40bea-74ac-4e84-8668-116ecf6fb504/Untitled.png)

### Heavily nested functions

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/2eeb78ae-d11c-4d80-9e0a-d6f9badcaf83/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/8ef13102-bd3d-4226-a6ca-ec5367c76cfe/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/746f61a4-d4d9-4224-a2ae-a214937cf08c/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/feaf2d1a-9cf1-47bc-8f2a-7491e79237db/Untitled.png)

## Herausforderungen von NLP

### Warum ist NLP schwer?

- Sprache ist mehrdeutig
- Man kann das selbe in vielen Arten ausdrücken
- Man kann von Wörtern den Sinn nicht ableiten
- Bedeutung von Satz kann von einzel Bedeutung der Wörter abweichen
- Man kann Wörter auf unendliche Arten kombinieren

## Textdarstellungen

### Wort Vektordarstellung

- OneHotEncoding := Vector mit größe des Vokabulars
- Byte-pair Encodings := Start mit nur einzelnen Buchstaben und dann häufigste Kombo hinzufügen
    - Verhindert OOV

### Satz Vektordarstellung

- (Averaged) Bag-of-words := $\frac{Summe ~~ aller ~~ Tokens ~~ im ~~ Dokument ~~ OneHotKodierung}{Größe~~Dokument}$
    - UNK/OOV Token für unbekannte Wörter
    - Tokenordnung geht verloren

## Wie Modell trainieren

### Arten des Trainings

- Gradient Descent := man nimmt gesamte Eingabe und updated dann Gewichte
- (Online) Stochastic Gradient Descent := Man nimmt zufällig einen Wert und updated direkt

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/94c21b0b-6289-4078-a51c-4ef01e1e1a41/Untitled.png)

- Minibatch Stochastic Gradient Descent := Man nimmt zufällig mehrere Werte und updated dann

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/e053cb5a-8f74-4b06-8f2c-e592b56ba933/Untitled.png)

## Log-linear multi-class classification

### Was bedeutet die Matrix?

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/00478c00-67c7-45aa-875d-347d984cdf8d/Untitled.png)

### CBOW

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/f925c9cd-7128-4448-aa68-fb40ea5cadba/Untitled.png)

## Language models

### Wahrscheinlichkeiten

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/f201ee5a-e6df-461a-9f69-80a9a48c357b/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/20de5e22-7524-4fd6-97eb-d74af56b63a8/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/92786c15-be21-43a1-b874-a35363c067e3/Untitled.png)

### Language Models Evaluate

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/8be0a5de-af0c-4be3-a2ba-efba43061487/Untitled.png)

### Probleme bei n-gram language Models (classical LM)

- Da wir nur anhand der Vorkommnisse im Corpus Wahrscheinlichkeiten berechnen können wir schlecht generalisieren (Having observed black car and blue car does not influence our estimates of the event red car if we haven’t see it before)
- Long range dependecies: To capture a dependency between the next word and the word 10 positions in the past, we need to see a relevant 11-gram in the text

### Aufbau eines neural LM

1. k Tokens als Input
2. embedding der Tokens lookupen und konkatinieren (Dimension vergrößert sich dadurch)
3. Danach NN

### Pro Con neural LM

- ≈ linear increase in parameters with k + 1
- The size of the output vocabulary affects the computation time
- The softmax at the output layer requires an expensive matrix-vector multiplication with the matrix W 2 ∈ Rdhid×|V | , followed by |V | exponentiations

## Dot product

### Dot product

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/2be978ab-46d1-4c11-8a24-f86a2ad93592/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/bd0940d0-db79-4686-abf2-f3f7b6cfee98/Untitled.png)

## Wie bekommt man word embeddings

## Wie bekommt man word embeddings

- k-th markov verinfachen → k Wörter davor UND danach betreachten (weil nur word embeddings wichtig und nicht die ausgegeben wahrscheinlichekits verteilung)
- task anpassen := Softmax (super aufwendig) vereinfachen zu binary (wort passt in context oder nicht)

konkrete tasks:

### word2vec (with negative sampling)

- entfernt hidden layers
- corpus für postive beispiele und negative (einfach wort ersetzen)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/df4abd4a-d998-42d9-8d1b-786866e982d8/Untitled.png)

- cbow
- predict center word given context words

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/c2a27c45-f171-4552-97ea-3c919e8647d8/Untitled.png)

- Skipgram ist auch in word2vec
- predict context words given center word

### Fasttext embeddings

will OOV vermeiden

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/0c769408-66ef-4a24-a377-2e3fdf63ca97/Untitled.png)

## Probleme von word embeddings

- Antonyme treten auch häufig im selben Kontext auf
- polysemi wörter mit mehreren Bedeutungen schwierig
- training corpus kann biased sein weil Mensch

## RNN

## RNNs Abstraktion

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/6d25e291-edec-4977-9234-2b8ff317f4bb/Untitled.png)

### Encoder

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/b3f251c2-6d13-48dd-9fd4-5a7a70bf5d90/Untitled.png)

### Transducer

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/6e21cb22-3fd3-4d7f-8e78-3ba3577b8fad/Untitled.png)

## RNN Architectures

### Simple RNN

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/36a3e4c3-d94b-4ed9-bbab-beda4f15ba97/Untitled.png)

- Gradients might vanish (become exceedingly close to 0) as they propagate back through the computation graph
- Kann schwer longdependencies abbilden

### Gated architectures

Anpassung der zwischenzustände wird gezielt durch gates gesteuert

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/65e33b56-58c0-46f4-9156-f28c0eba572b/Untitled.png)

### LSTM

Benutzt keine hard sondern softgates und soll vanishing gradients problem lösen

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/bc1fd46a-ba0a-4bf8-96c5-fc43c964be20/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/cb8b24df-e0a5-4bd7-bbcb-837fc8473acf/Untitled.png)

## Encoder-decoder architectur

RNNs kann zwar beliebig lange inputs nehmen aber output ist immer gleich lang wie input

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/5d3d9fcc-1654-4cd1-9355-160e54d6c2f5/Untitled.png)

### Encoder-Decoder Model

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/779f4b9a-6c5d-4108-b12c-13923d1086b1/Untitled.png)

## Attention mechanism

## Attention mechanism

Encoder-Decoder schlecht bei langen Abhängigkeiten

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/b5b1fac4-f624-436e-bdf3-5bd4d97e06f0/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/6b9c1a8c-0ca8-46b4-aa6b-817f5107201a/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/9ccf76e0-d942-411a-a213-b51dc5a73a72/Untitled.png)

Warum $\sqrt{d_{dec}}$ := ist die Standardabweichung des Vektorprodukts → neuer Vektor wieder 0 means und 1 varianz

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/dc993fca-a209-4edc-8d51-b3447623cbfa/Untitled.png)

## Attention Gneralisiert

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/191a0e1b-12cf-44a6-bdfe-efebc22685de/Untitled.png)

## Design Choices

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/19cd32e0-eb4e-4522-9bb9-74057d32836e/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/55e78692-46f3-4262-ab15-b4a55f0dfd4f/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/33971c59-a698-4f88-af52-0d04d3458b08/Untitled.png)

## Transformer

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/2d059d59-f368-446b-b78e-2e53fec1dc2b/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/72b88851-c244-4600-bc20-f84b8554af40/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/acf899a8-7657-4edb-856b-eafee6e4bc35/Untitled.png)

## Transformers

### CONTEXTUALIZED REPRESENTATIONS

- In RNNs ist jeder State die Zusammenfassung der sequenz aber auch die Bedeutung des aktuellen worts im context (weil word embeddings alleine Probleme mit polysemy und antonyme haben)
- Cross-attention für relevante informationen aus input für aktuellen state mit contextual cues
- RNN state in decoder aktuell nur für attention query → stattdessen direkt word embedding verwenden

### Encoder Block

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/a16ab42f-1dbd-4885-87fa-a21dc6d28cb0/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/899a2b3a-58f7-46d1-8dde-f580b8cf03ff/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/35959aba-aa77-44d1-8409-3df90a239bb8/Untitled.png)

### Multihead Attention

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/9f172e57-f071-459a-9346-0a4df493c035/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/e4750050-ce1c-4402-b06a-771adc3e3e10/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/b79eae08-328e-47ce-964c-17113557f8e9/Untitled.png)

### Residual Connections (nochmal angucken)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/3c483f27-e279-414c-a8a1-d6ea383dce35/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/921ac0b7-22f6-483f-ad0e-fecb00127555/Untitled.png)

### Positional embeddings (nochmal angucken lol)

- Durch parallele Verabreitung geht Wortordnung verloren

## BERT

## BERT (encoder only)

### First task

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/60ecf8d8-59f4-475b-98da-899c662776e6/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/4ecdf197-a935-4072-bba3-d3509b8625cb/Untitled.png)

### Second Task

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/5d10b30d-60c4-4e0d-8a2e-683bb2b6dbd7/Untitled.png)

### ALLES

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/bd2c537a-f8bd-439e-84d4-d72bff323410/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/97ddcb40-d38d-4ec6-bc4e-affab6f4eb50/Untitled.png)

## BERT Finetuning

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/b632338f-d10f-492d-8972-e856c7c63ea6/Untitled.png)

### Decoder Head

- Zusätzliche Schichten (FFNN + Softmax) nach BERT

Konkrete Beispiele

### Single Sequence Classification

- Decoder Head hinzufügen
- Sequenz mit CLS durch BERT jagen
- CLS dann in decoder head

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/9e627dba-f4da-45de-a948-c80a0c40775a/Untitled.png)

### Sentence Pair Classification

- Decoder head hinzufügen
- Beide Sequenzen durch BERT mit CLS und SEP
- CLS dann in decoder head

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/0b2b2ea2-160d-428f-8524-4a6b45ee9958/Untitled.png)

### Span Extraction QA

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/976af1a9-4fdd-46bc-851e-d7cf4462dd66/Untitled.png)

### Sequence Labeling

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/6858687d-ac57-45c5-bc1d-47248e7b347e/Untitled.png)

## Andere Arten von Pretraining

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/b63633f8-7d91-4256-9abc-ad601b24f715/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/b0a40c59-4e1a-4280-9b03-8e050cf33708/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/5b848298-9449-4edd-a2be-dc2bccf851f9/Untitled.png)

## PRETRAINED LANGUAGE MODEL ARCHITECTURES im Vergleich

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/82ec8edf-cad1-4b63-9607-6f47f6fd178c/Untitled.png)

## Transformerarten im Vergleich

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/a68943eb-5545-43cc-8293-d0bd9b415001/Untitled.png)

T5

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/2606c3b5-d767-44df-bdc8-88bd3bf1c082/Untitled.png)

BERT

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/edb7f5d1-0ae4-41f8-a7b2-ec111fdd11b6/Untitled.png)

GPT 2

## Attention Mask (verwirrt)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/638391ba-51b1-46de-951e-1ccb908be9cc/Untitled.png)

## Arten von Language Modeling

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/1341a072-f294-4e34-aabf-92fad6790e46/Untitled.png)

## Autoregressive Decoder-only models

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/6a78c7dd-a1f8-4c15-b792-37eb30ba9cba/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/4673331a-7887-4d6f-b919-98384410cbc0/Untitled.png)

zero, one, few shot learning auch in-context learning genannt

## Prompt-tuning MLMs

promping kann auch mit bidirectional encoder only models passieren, aber schweirig weil sie nicht für text generation trainiert wurden

Idee: Prompt als MLM

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/4df7ec2b-a834-4a75-933b-2d0560eec64d/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/c722e6b7-053d-4f76-849d-7bed834ccb81/Untitled.png)

## RLHF: Reinforcement learning from human preferences

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/81624d99-d8ab-404b-a01e-d8d67e5c9296/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/6c4efc78-cda0-4523-8d60-462fd8d2b3f5/Untitled.png)

## LMs erweitern

We can extend language models with information retrieval components (RAG) or access to general APIs (Toolformer)

### Toolformer

## Explainability of AI

### Motivation

- Um Systeme zu verbessern muss man verstehen, warum Sie so handeln
- KI kann uns neue Perspektiven liefern, wenn wir sie verstehen
- Unfaires verhalten nachvollziehen und verhindern
# Begrifflichkeiten

- Gold standard data := Mehrere Experten labeln Dataset und aus allen labels wird gold label bestimmt (Inter-Annotator Agreement)
- Hugging Face := Datasets Website
- n-gram := n Tokens nebeneinander

# Welche Aufgaben versucht NLP zu lösen?

## Klassifikation

- Binary Classification := Text in Positiv/Negativ einordnen (IMDB)
    
    - Benötigt semantic compositionality, long-range dependencies
- Inference Task := Text und Hypothese in folgerichtig, widersprüchlich oder unbestimmt (SNLI dataset hat RTE adaptiert)
    
- Extractive Question Answering := Text und Fragen → Muss Informationen zurückgeben
    
    ### BIO (Sequence labeling)
    
    O := Out of Entity
    
    I-X := In entity X (Start wird so markiert)
    
    B-X := Begin von entity X (wenn zwei wörter mit der Selben entity zusamme nstehen wird das zweite so gelabelt)
    
    ### SuperGLUE
    
    SuperGLUE (**General Language Understanding Evaluation**) := Benchmark für Sprachverständnis in Englisch
    
    - Recognizing Textual Entailment (RTE / Binary Classification) := Text und Hypothese gegeben und dann positive oder negativ
    - Coreference resolution := Liste von Nomen und ein Pronomen gegeben → Bezieht sich Pronomen auf die Nomen
        - Benötigt everyday knowledge and commonsense reasoning
    - BoolQ := Frage und Text → Frage beantowrten (Ja Nein)
        - Benötigt complex, non-factoid information, requires difficult entailment-like inference
    - Multi-Sentence Reading Comprehension (MulitiRC) := Text,Frage, Liste möglicher Antworten → beantworten
        - benptigt weitreichendes Textverständnis

## Text Generation

- Machine Translation := (WMT dataset)
    - Viele Möglichkeiten der Übersetzung (beste schwer zu finden)
- Document Summarization := Aus großem Dokument Zusammenfassung generiern
- Dialogue := Nächsten Satz in Dialog erstellen

## Klassifikation als generation

Jede Aufgabe (auch Klassifikation) ist am Ende ein Text zu Text Format (also geben Text und dann generieren Text)

Dadurch kann man Klassifikation und Generation zusammenfassen

# Wie evaluieren wir die Outputs?

- Es sind Training und Test datasets gegeben
- Train → Validation → Test

## Cross validation

Bei kleinen Datasets

- Data in K Teile spliten
- K -1 Teile isind Train Data und 1 ist Test Data

## Confusion matrix

||Predicted Negative|Predicted Positive|
|---|---|---|
|Actually Negative|True negative (TN)|False positive (FP)|
|Actually Positive|False negative (FN)|True positive (TP)|

Accuracy := (TN + TP) / Test Set Size (Wahrscheinlichkeit, dass unser System richtig liegt)

Precision (P) := TP / (TP + FP) (Wahrscheinlichkeit, dass wenn unser System Positive Predicted es auch recht hat)

Recall (R) := TP / (TP + FN) (Wahrscheinlichkeit wieviel der Positive Sachen auch “gefunden” wurden)

F1 := 2* P * R / (P + R)

## Metriken für Text Generation

- BLEU (Bilingual Evaluation Understudy) für machine translation
    - Nimmt Rferenz (gewollte Übersetzung) und erzeugte Übersetzung und berechnet n-gram overlap (wieviele Tokens der Länge n gleich sind)
    - Benutzt nur Precision (kein Recall)
    - Erlaubt nur exakte n-gram matching
- ROUGE (Recall-Oriented Understudy for Gisting Evaluation)
    - Verschiedene Varianten ROUGE-N,-L,-W,-S
    - ROUGE-N wie BLEU aber benutzt recall statt precision
    - ROUGE-L misst längste gemeinsame Subsequenz

## Probleme bei Evaluation

- Annahme von Gold Label bei eundeutigen Sachen gut (bei z.B. Übersetzung schwieirig)
- Human annotator sind voreingenommen
- Artifakts in Training Data (Wenn immer Negative wenn negation im Text vorkommt merkt sich system einfach da)


# Wie minimiert man Funktionen?

- Für einfach Funktionen normaler Kram
- Brute Force (alles berechnen)
- Gradient-based := willkürlichen Punkt nehmen und dann “den berg runter gehen” lol (findet nur lokale Minimum)

## Komplexe (verschachtelte Funktionen ableiten)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/39ce9496-081d-433c-abb5-544ad7788fbc/Untitled.png)


# Herausforderungen von NLP

- Sprache kann mehrdeutig sein und auf verschiedene Arten kann das Selbe ausgedrückt werden
- Kann durch Supervised machine learning behoben werden
    - ML versucht dann Muster oder Regelmäsigkeiten zu erknnen von annotierten Input/Output Paaren
    - Ml funktioniert gut, wenn man schwer Regeln festlegen kann aber trotzdem der Output simple festgelegt werden kann
- Sprache ist aber sehr kompliziert
    - Symbolic und diskret
        - Wörter haben für uns Bedeutungen, die durch das Wort selbst aber nicht ableitbar sind
    - kompositorisch
        - Buchstaben → Wörter → Phrase → Satz
        - Wörter können in einem Satz andere Bedeutung haben
    - karg
        - Unendliche viele Sätze sind möglich

# Suervised Learning on Text Data

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/388ff194-9e8e-4270-97f9-7be5f25d162a/Untitled.png)

# Wie kann man einen Text als Vektor darstellen?

### Bag of Words

- Vektor dessen Länge dem Vokabular entspricht (jeder Eintrag stellt ein Wort da)
- Die Summe aller EInträge ergibt 1
- Hammingdistanz aller Vokabeln ist 2 (da sich immer nur 2 “Bits” unterscheiden)
- Reihenfolge der auftretenden Wörter wird nicht dargestellt
- Beinhaltet auch ein UNK oder OOV Vokabel um unbekanntes zu kennzeichnen

### Subword units (Byte-pair encoding)

- Vokabular besteht am Anfang nur aus Zeichen
- Die Häufigsten Kombinationen werden dann vereint und zusätzlich in das Vokabular aufgenommen (wiederhole das eine bestimmte Anzahl)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cec6fd80-8f9b-4ae8-8747-7863c719dd2e/Untitled.png)

# Binary text classification

Bis jetzt gibt unsere Funktion Werte von - bis + unendlich zurück

### Sigmoid

Stellt auch die Wahrscheinlichkeit, dass der Input zu 1 ausgewertet wird

$$ \sigma(t) = \frac{exp(t)}{exp(t) + 1} $$

$$ \sigma'(t) = \sigma(t) \cdot (1 - \sigma(t)) $$


# Wie weiß ich ob mein Model gut ist?

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b294c49f-c432-4ec7-9c0c-f87d8b7865ab/Untitled.png)

## Loss functions

corpus wide loss := Loss alle Trainingsdaten addieren und dann durch ANzahl der Daten teilen

### Binary cross-entropy loss (logistic loss)

$$ L_{logistics} = -y\cdot log ~\hat y - (1-y) \cdot log(1 - \hat y) $$

## Mittels Loss function bessere Gewichte finden

### Online Stochastic Gradient Descent

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/abd6285f-2f5c-4250-b835-9fee930d276d/Untitled.png)

- Online weil nur ein example verwendet wird

### Minibatch Stochastic Gradient Descent

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2b04e0dc-457d-4b71-ae03-cf611da8a10f/Untitled.png)

- Nimmt m (1 bis n) examples und macht an sich das selbe
- große ms geben gute abschätzung für corpuswide gradients
- kleine ms mehr updates und schnellere konvergenz (braucht mehr memory)
- Kann gut parallelisiert werden

# Wie sieht es bei multi calss calssification?

## Perceptron (simple linear model)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1a4725ab-1430-49e9-8277-b736a757a4bd/Untitled.png)

- Kann Sachen nur linear einordenen (1D mit Punkt, 2D mit Linie, 3D mit Hyperplane)

### Beispiel Darstellung von W (Text wird Sprache zugeordnet) (embedding matrix)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9ce8adf3-8ac5-4a72-830e-297d394317bc/Untitled.png)

- Jede Spalte repräsentier die Sprache bezüglicher ihrer Wörter (ähliche Sprachen haben auch ähnliche Spalten Einträge)
- Jeder Zeile repräsentiert ein Wort und dessen zugehörigkeit zu den einzelnen Sprachen

## bag-of-words → continous bag-of-words (CBOW)

- Bag-of-words mit z.B. obiger Matrix multiplizieren

## Wie können wir unser Ergebnis jetzt in eine Wahrscheinlichkeits darstellung umwandeln?

### Softmax

$$ softmax(x_{[i]}) = \frac{exp(x_{[i]})}{\sum^K_{k=1} exp(x_{[k]})} $$

- Bildet jeden Wert des Vektors auf eine Zahl zwischen 0 und 1 ab
- Die Summe alle Eintrqge ist 1

# Wie bestimmt man die Loss function bei Softmax (classification)

$$ L_{cross-entropy}(\hat y,y) = \sum^k_{k=1} y_{[k]} log (\hat y_{[k]} ) $$

# Kann man solche Transformationen einfach kombinieren für bessere Ergenbisse? (activation function)

Immer wieder lineare Transformationen machen keinen Sinn, da man sie zu einer zusammenfassen könnte

## Multi Layer Perceptron (MLP)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e970b39f-6c96-4e9e-89c0-e5715e0693da/Untitled.png)

## Was kann g sein?

### Sigmoid

### tanh

$$ tanh(z) = \frac{e^{2z} - 1}{e^{2z} + 1} $$

### ReLU

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bb88b716-2aa1-4a9a-ae4e-60ace6cb5cd6/Untitled.png)


# Probability Refresher

- $Pr(W_1 = w_1)$ := die Wahrscheinlichkeit, dass W_1 dem Wort w_1 entspricht
- $Pr(W_1 = w_1 \cap W_2 = w_2)$ := die Wahrscheinlichkeit, dass W_1 = w_1 und W_2 = w_2
- $Pr(W_2 = w_2 |W_1 = w_1)$ = $\frac{P(W_1,W_2)}{P(W_1)}$:= die Wahrscheinlichkeit, dass W_2 = w_2 ist, wenn W_1 = w_1 ist
- Variablen sind unabghängig, genau dann wenn $P(X,Y) = P(X) \cdot P(Y)$
- Variablen sind conditional unabhängig von Z , genau dann wenn $P(X,Y|Z) = P(X|Z) \cdot P(Y|Z)$

# Language Models

- Soll Sätzen Wahrscheinlichkeiten zuordnen
- Soll die Wahrscheinlichkeit von Worten nach einer bestimmten Wortsequenz angeben

## Classical language models (counting-based)

## Chainrule of probability

$$ Abk. ~~ Pr(W_1 = w_1 \cap W_2 = w_2 \cap W_3 = w_3) = Pr(w_1,w_2,w_3) $$

$$ Pr(w_1,w_2,w_3) = Pr(w_1 | <s>) \cdot Pr(w_2 | <s>,w_1) \cdot Pr(w_3|<s>,w_1,w_2) $$

- Für lange Texte ist die Wahrscheinlichkeit am Ende irgenwann 0
- Nicht wirklich brauchbar (laaange abhängigkeiten)

### k-th order markov assumption (zur Vereinfachung)

- Die Wahrscheinlichkeit des nächsten Wortes ist nur von den k vorherigen abhängig

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/12f20b24-6b09-4b86-b1fd-68600ddaf9da/Untitled.png)

## Wie bestimmt man die Wahrscheinlichkeiten?

### Maximum Likelihood Estimation (counting and dividing) mit kth prderr markov assumption

$$ \hat P_{MLE} (W_i = w | w_{i-k:i-1}) = \frac{\#(w_{i-k}~~w_{i-k+1}~~...~~w_{i-1}~~w)}{\#(w_{i-k}~~w_{i-k+1}~~...~~w_{i-1})} $$

Um einen Nenner = 0 zu vermeiden:

$$ \hat P_{add-\alpha} (W_i = w | w_{i-k:i-1}) = \frac{\#(w_{i-k}~~w_{i-k+1}~~...~~w_{i-1}~~w) + \alpha}{\#(w_{i-k}~~w_{i-k+1}~~...~~w_{i-1}) + \alpha |V|}~~~~0\leq \alpha \leq1 $$

## Was ist die Loss function von einem Language Model? (Perplexity)

Perplexity of LM

$$ 2^{\text{cross-entropy}} = 2^{-\frac{1}{n} \sum^n_{i=1} logPr(s_i)} $$

## Was sind Nachteile dieser n-gram Language models?

- Um Abhängigkeiten zwischen dem nächsetn und 10 Wörter davor zu bestimmen müssen wir 11-gram im text kennen (long dependencies)
- Genralisiert nicht über Kontext (rotes Auto und schwarzes Auto komplett verschiedene Sachen für ihn)

## Neural Language Models

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/72e033e1-18d7-4a19-868a-9d1b5ab935b3/Untitled.png)

Soll einen input von k Worten nehmen und dann eine Wahrscheinlichkeitsverteilung für Wort k+1 zurückgeben

Verbindung aus Look-Up operatin und MLP

Jede Zeile von E lernt eine Wort darstellung und jede Spalte von W^2 lernt eine Wort darstelung

## Embeding Layer (Look-up operation)

Word Embedings teilen Vokabeln bestimmte Charakteristiken zu (wie z.B. mit den Sprachen letztes Mal)

### Was sind Vorteil gegeüber counting-based?

- Komplexität steigt nur linear bei mehr parametern
- Je größer das Vokabular, desto länger die Berechnugszeit
- Die Softmax Funktion am Ende ist teuer (weil matrix mal vektor)


![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9fcf77dc-1ce4-455f-8c97-2d651503ec8f/Untitled.png)

# Dot product recap

- Ist die Summe der Produkte aller Einträge von zwei Vektoren
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8579154b-5469-41a7-8dd7-56a881f79a08/Untitled.png)
    
- Es ist auch Geometrisch darstellbar
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3cf71b00-d0a6-4e71-b76a-7fd92f769bea/Untitled.png)
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/75f0de25-98b2-4071-a3fd-a2140ad1b669/Untitled.png)
    
    - $||u|| = \sqrt{u_1^2 + u_2^2 + u_3^3}$
- Es ist auch eine Skalare Projektion
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9b29cdec-576b-4b3d-996a-ce4cd5471da3/Untitled.png)
    
- Das dot product von zwei unit vectoren (Länge ist 1) entsprecht dem cos(Winkel zwischen den Vektoren)
    
- Dot product can sogar die distanz messen wie die euklidische norm
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dfc43f7e-b5c7-43ba-9bc5-dfb182a929b2/Untitled.png)
    

# Distributional hypothesis

Bedeutet, dass Wörter mit ähnlicher Bedeutung auch meistens in ähnlichen contexten auftreten

One-Hot encoding für wörter ist neutral (alle Wörte gleich, keine Ähnlichkeit)

### Word-context matrices (schlechte Idee)

- Jede Zeile ist ein Wort
- Jede Spalte stellt ein kontext da in dem Wörter auftreten können
- Ein Eintrag stellt die Stärke der Verbindung zwischen Wort und Kontext da

Probleme

- Manche Einträge werden schlecht trainiert weil sie selten vorkommen
- Sehr hohe Dimension

### Word Embeddings von Language Models

Wir können unsere aktuellen neural language models verwenden

- Kleine Änderungen (nicht nur die k Worte davor betrachten)
- Softmax kann weggelassen werden weil wir keine Wahrscheinlichkeitsvertailung haben wollen nur einen Score für wie gut das Wort ist

Wie stellen wir das an?

Wir wandeln es in eine Binary Classification um (Zielwort muss nur als gut oder schlecht bewertet werden)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1f915659-89a3-4834-9f84-0a4cc17f55ba/Untitled.png)

# word2vec (für word-embedding training)

- Ist nur noch ein log linear model (for speed)
- Kontext (Vektoren) wird summiert (CBOW) und mit Ziel dot product
- Gleiche Wörte sind näher (dot product)

### **Continuous Bag of Words (CBOW)**

w_i ist entweder das richtige oder falsche Wort in dem Kontext. Soll bestimmen ob w_i passt. Trainiert nur E

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9722d4f0-1df0-45fa-816f-07139172fb39/Untitled.png)

### Skip-Gram

Soll diesmal den Kontext anhand w_i vorhersagen.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d3f0931d-7e2a-4be1-9091-a78ed7690308/Untitled.png)

# FastText embeddings

Teile Worte in n-grams auf welche alle ihren eigenen EMbeddings eintrag haben (n zwischen 3 und 6)

# Probleme bei word embeddings

- Antonyme treten häufig im selben Kontext auf (kaufen-verkaufen)
- Benutze Daten können voreingenommen sein (Wie menschen schrieben)
- Wörter können mehrere Bedeutungen haben (Bank)

# Recurrent Neural Networks (RNN) Abstraktion

- Soll eine Sequenz an inputs verarbeiten und einen Output mit fester Länge zurückgeben
- Verwirft die markov assumption (nimmt komplette sequenz)
- Bernutzt states (Vektoren) um inforamtionen zur nächsten Position zu geben

z.B.

$$ y_3 = RNN(x_{1:3})~~~~y_2=RNN(x_{1:2})~~~~y_1=RNN(x_1) $$

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3cb6a374-fd3a-4cb0-bd62-d5127895bb83/Untitled.png)

Encoder

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ffb316a1-8858-4204-9f43-51ef527d47ee/Untitled.png)

Transducer

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/956d79f3-7f8f-4e67-b43f-75d256d9e932/Untitled.png)

Das Problem ist, dass aktuell jede Prediction nur die Vergangenheit (s_1) berücksichttigt

- Die Idee ist einfach einmal von recht-links und links-rechts zu berechnen und die ergebnisse dann aneinanderhängen

# Konkrete RNN

### Simple RNN (S-RNN)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/99abe11a-386a-48d3-93fa-ad20e1aa28df/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d2523bfe-7fa5-4e67-a2f3-bf3cb8984448/Untitled.png)

- Das Problem ist dass bei tiefen netzwerken die gradienten verschwinden können (lange Backpropagation)
- lange Abhängigkeiten gehen verloren

### Gated RNN

- states und Eingaben werden als Speicher verstanden
- Speicherzugriffe werden durch gates limitiert

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7edd568b-5e56-46e1-81d0-7395b6986f30/Untitled.png)

- Hier sind die gates aber noch nicht differenzierbar
- und nicht lernbar
- deswegen nächstes wird mit soft gates ersetzt

### Long Short-Term Memory

Soll vanishing gradients lösen

- Teilt state Vektor in zwei (memory cells und working memory)
- Memory cells sollen memory und error gradients über Zeit merken
- Memory cells werdne von differenzierbarne gates controlliert
- Kann inputs beliebiger länger annehmen

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8d26a3f1-1eeb-4c79-85a8-4de843eeee60/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a16a7201-1d9f-4a64-89a0-7cfa77fbb78e/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9a037218-5ff5-460d-bf18-2b38651273ad/Untitled.png)


- MLP können nicht mit variablen input Längen umgehen
- RNN können mit variablen Input Längen umgehen
- RNN hat Problem mit Variablen output längen

# Encoder-decoder architectures

Sequence-to-sequence models lösen das Problem, dass beim generieren des ersten Tokens nicht der gesamte kontext bekannt ist

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d8c0f5d2-b879-46d4-ae5f-e19243f7f294/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/53585d5c-bd1b-40a4-b037-a6f33f5032f0/Untitled.png)

- Warum sollte zur Initialisierung des hidden state des decoders der hidden state des encoder transformiert werden
    - Down-Up Scae passend zum hidden state
    - Endoced und Decoder haben verschiedenen Größen weil eine Aufgabe schweiriger bzw. einfacher sein kann
- Was ist teacher forcing? (Wird vorallem am Anfang verwendet)
    - Wir geben dem decoder als input nicht das vorher generierte Token sondern das richtige aus den Trainings Daten
    - Ansonsten würden wir dem nächsten decoder Schritt seh wahrscheinlich einen falschen Input geben wodurch die prediction auch falsch wird

# Überblick NLP Aufgaben

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/02187824-15cc-4630-9120-846765db40b3/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9a1e28ea-4503-4a87-b4b1-a0d6519ed0f9/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e154299b-65b1-431d-86e0-c087a7762a74/Untitled.png)

# Attention mechanism

- multilayer bidirectional LSTM haben Probleme bei machine translation wegen long dependencies
    - vanishing gradient problem (Je länger der Input, desto länger der Ourput und desto größer die Lücke zwischen den Signalen)
    - hidden State ist endlich (encoder teilt Infromationen über diesen mit decoder)
    - Je mehr Tokens RNN liest desto weniger kann er sich an einzelne erinnern

1. ENERGY Nimmt aktuellen decoder Zustand und alle encoder Zustände und berechnet jeweils die “energy” zwischen den Paaren mit dot product
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cdebb25b-078b-4526-af1a-12d01c9a0384/Untitled.png)
    
2. SCALE Das Ergebniss wird durch sqrt(Dimension von Decoder oder Encoder) geteilt (welche ist egal weil müssen eh die selbe d haben) damit im nächsten Schritt die Zahlen durch exp nicht gegen unendlich gehen
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2e7673cc-1329-4c30-b7a9-598a03d73eae/Untitled.png)
    
3. NORMALIZE Zeigt an wie wichtig dieser Encoder Sate für den Decoder state ist
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/08f705fe-1d5e-4d64-bbdd-c4eb3a03d330/Untitled.png)
    
4. SUM da wir jetzt alle einzelnen Importances haben müssen wir diese Zusammenfassen (dot product)
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5cc4ae59-7617-4069-a34f-d113a28acabd/Untitled.png)
    

# Attention mechanism (Abstraktion)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/026dfbb7-3e5e-42fc-9c2a-c41c4004ba25/Untitled.png)

# Attention mechanism (Design Choices)

## Wie berechnen wir die Energy?

### Dot Product

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/57bb9f1d-7adb-48e7-8ce3-d5d8bdab8546/Untitled.png)

- Dimensionen müssen gleich sein
- Keine zusätzlichen Parameter

### tanh attention

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/111db66f-6c53-4d3a-b343-9586fd434ca3/Untitled.png)

- Dim müssen nicht gleich sein (werden nur zusammengehängt)
- zusätzliche Parameter W $(W_1\in\R^{(d_q +d_k)\times h},W_2\in \R^h)$

### Bilinear attention (schlecht)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/eb186b45-5b05-418a-a797-b71f081e3efd/Untitled.png)

- DIm müssen nicht gleich sein
- Zusätzliche Parameter $(W \in \R^d_q \times d_k)$

## Parametrisierung

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a69709bb-0d3e-43a9-b30e-7afed04ba0af/Untitled.png)

## Direction

### Encoder-Decoder Attention

Decoder benutzt states von encoder

### Cross attention

Zwischen encoder und decoder

### Self-attention

Encoder benutzt selbst attention



- MLP fixed input length
- RNN gut für kurze sequenzen
- RNN + attention funktioniert gut mit kurzen und langen squenzen

# Was war gut an RNN

- memory cells (Zusammenfassung der jetzigen sequenz)
    - Haben aber begrenze Kapaztät
- Wir kennen Position des word in der Sequenz
    - Wird durch state und input
- Es muss trotzdem bei einer Sequenz der Länge n auch n-mal ausgeführet werden (schwer zu parallelisieren)
- Skalliert schlecht bei großer tiefe (vanishing gradients)
- Closed vocabulary (Ein Wort = Ein Vektor, Leute verschreiben sich aber und Sprache wandelt sich)

# Transformer (encoder-decoder architecture)

anfang von Vorlesung 10 gucken falls unklar

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3fa7c777-b5b7-44a6-a516-cd0983f45320/Untitled.png)

## Wie wird kontext repräsentiert?

### Wie war es in RNNs

- Jeder state stellt die bisherige Sequenz da und den Sinn des aktuellen Worts im Kontext (zwei Jobs für einen Vektor sind schlecht)

Bei Transformer die auf RNNs verzichten wollen benutzen wir die input word reprensetation

## Transformer attention Block

### Multi-head attention

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ee04d524-4e95-480e-8d0f-616618ada13d/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/597b6f9f-b668-4640-b227-984f5aa7a92d/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/afdfbc38-ca4c-4d44-98cc-3240d8272557/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/00cb15d9-add6-43a9-8765-5d8941339e75/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/202ef1ff-1e79-4c1d-8b34-6f6f8e40088b/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b079dd7a-1bd2-4fff-9200-29531bc73f54/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/df56480e-e317-467f-ac3d-8fbb3766d124/Untitled.png)

### residual connection

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9adc75af-061b-40c8-98aa-13fe0733d07f/Untitled.png)

### position wise linear layer

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f153700c-4beb-4a95-bfe9-a33fa8307e77/Untitled.png)

## Byte-pair embeddings

- Vokabular mit nur Charakters
- Merge most frequently characters and add them
- repeat n times

## Positional Embeddings

Durch die fehldenden RNNs haben wir keine Informationen über die Wort Reihenfolge

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c35a8029-3536-4828-9248-f8435bb609af/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8d0211a6-0a6d-417e-aa3e-7aa09c2bf6b8/Untitled.png)

wenn test zu lange embedding einfach kopieren


- Transformer ist gut bei sequence-to-sequence
- es skaliert gut (viele Schichten und Parameter)
- Leicht zu optimisieren (residual connections)
- schnell (parallel encoding)
- Aber man kann es auch nur für Aufgaben benutzen für das es trainiert wurde

# BERT (pretrained language models PLM)

Idee: Train Transfomrer Model in etwas wie word2vec und benutze pretrained contextulaized embeddings für andere Aufgaben

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ebe59f81-0505-4869-b3d4-01d25aaeacaa/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/efc1d848-1417-4766-8349-b63308ed971a/Untitled.png)

## Next Sentence Prediction

Wir wollen nicht nur contextulaized embeddings für wörter sondern ganze satz embeddings

Wir erstellen also eine Aufgabe den nächsten Satz anhand des vorherigen Satzes vorherzusagen

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e5984251-ab53-4881-be4e-c28960113764/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/372d1a64-9a62-4584-9d69-980b89f5428b/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/00a06d99-845c-4f99-ada0-50c2e337e56f/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8c381ad4-c868-445a-9882-75402e52d950/Untitled.png)

## Wie und wo wird BERT angewendet

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/eb987a0b-46a0-4500-9073-e32c7de2e93a/Untitled.png)

### Was sind decoder heads?

- random initalisierte neurtale netzwerk layers (meistens linear)
- ganze neurale netzwerke/ganzer Transformer/einzelne lineare Schicht
- Wird auf den Transfomer gesetzt um unsere Aufgabe zu lösen

### BERT für single sequenze klassifikation

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8e528698-7721-437f-bbed-425ae2ef53d8/Untitled.png)

### BERT für sentence pair classification

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a3dcadf3-fb2b-45ab-a3d0-1eddfa2cf200/Untitled.png)

### BERT: span extraction QA

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/962543f3-7343-40c6-b52f-62220c7c2ebe/Untitled.png)

### BERT: sequence labeling

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/499c2714-76ab-47cd-9148-60ef747b6ec7/Untitled.png)

## Varainten von pretraining tasks

- Masked Language Modelling (MLM) und Next Sentence Prediction(NSP) bis jetzt

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/748c2cf8-4dc1-437e-ac53-52b0e08f1e30/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4f0f6de3-a5a0-45ee-a83c-50f4a5d9e2fd/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fa252af8-aa45-4af1-bcab-c6bc110e8372/Untitled.png)


# Typen von Transformer Architekturen

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/51ac4ae4-6487-4d36-9863-a836d1892b29/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/51204587-04e6-48b4-b674-a3769462aaaf/Untitled.png)

- Man könnte eine Sequenz übergebe wo das zu generierende gemasked ist (lange sequenz gemasked tokens, hat das model noch nicht so gehabt sehr komplex)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3e4f1be0-d637-4f11-8759-811f436975f9/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/092e3d87-36bd-4b95-8dc7-38e86ee6b327/Untitled.png)

# Autoregressive decoder-only Models

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bfc89775-0d52-4384-b5d8-6c068ccda2c1/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a223de21-70ff-4217-9bf0-02e1285dcaa5/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/baa79fc1-11be-4d41-8ac7-216bd6d57aab/Untitled.png)

## Prompting

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8c3e3499-990b-42bf-95bd-e0a26e2d4f9d/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/18668e2a-34c5-4c37-8f9a-3a318882b40e/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/840753e6-e68a-4e4c-8654-a13b1b0ae939/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/62cbb300-f35b-49a7-ad0b-275d3d7d8aab/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4ccaba93-1c5f-44a9-a572-540ef9c16a13/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/def0e19e-c950-4fb9-9791-f1643075f139/Untitled.png)

# Kann man promt-tuning auch bei MLMs benutzten?

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3eec1c93-06dd-4ce0-a8f6-2aac30838165/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ad60d029-6a22-4bb5-8044-d589aa90be82/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a8829249-c290-4ca5-9ac5-dbe2fe42ca52/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8b10b9ce-ef4e-44aa-ac43-257e330231c1/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8c483daa-2494-4c2a-80f1-6dd9ab893d3f/Untitled.png)


# Recap

## NLP Tasks

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/92a2dc12-ba55-4b82-bb6e-507866eec44a/Untitled.png)

### Seq. calssification

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/41f9b3a1-4e8d-4f80-8df3-1f53c9438264/Untitled.png)

### Seq. labeling

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e87f7aae-623b-4ee2-8048-fffb678b55f2/Untitled.png)

### Seq. to seq.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/42e1b44e-a08c-486f-ac01-868f95d2880b/Untitled.png)

## Attention

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/36da6e76-6899-4822-b35d-a418b8e0a537/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e39ddf28-f4ef-4a75-ba14-9851270b3c40/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1883d72c-f114-4752-a543-cd3a0ee207ee/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b0c98049-cb42-4a7f-b6a7-9f6cc937c70a/Untitled.png)

## Transformer

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cab6d099-6162-4483-bba0-88c5e63632d8/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c78cfcfb-f0f1-4701-9e54-cd57ac9c4950/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/649d61d0-2df4-4eb2-b02d-320085126f6c/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e85a0ecf-ad7b-4c12-b855-3e5f237aacf4/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e4a973af-4721-4a01-ad7c-889bc4eedfd3/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/eb74012f-2dec-4ded-aa98-b4a6612e1308/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8d34e2dc-db50-4284-b4af-add049c4844e/Untitled.png)

- Transformer based networks haben an sich kein Sinn für word order
- Residual connections ermöglicht das skalieren in die Tiefe

### Multi Head attention

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/97afb851-bd47-4f1f-96f9-15cada095dbe/Untitled.png)

## BERT

MLM

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fa7849c5-1e99-4a1f-8ea9-99c6d1c54dac/Untitled.png)

NSP

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/83f7065f-dd53-409a-a7e1-b5a66ea4865c/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0c6c8bc8-d897-4632-9a51-3e455cac15de/Untitled.png)

### Wie trainieren wir BERT für unsere Aufgabe

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4f974f15-5d81-4333-8350-94c73a4fc34f/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b335af75-d6e0-45a8-b43f-059c63130e86/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b09f62d8-cbdf-4ebc-aa7a-ab116ac96422/Untitled.png)

## Pretraining Tasks for PLM

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/88f5686a-f94f-42b9-9967-c4c312f9d612/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bcba9257-eb27-47bb-b7a4-65d1ede07e68/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/380683a6-3f74-4627-9f60-3d38a0ff3247/Untitled.png)

## Typen von Architekturen

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/778b55ad-cffe-4215-aaf8-ee3564cfc635/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b77f1123-a335-4f59-8a5a-14561991718a/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c0faac16-648c-4a6b-9cff-254f7d77557f/Untitled.png)

# NLP today



# Altklausur SoSe2021

## Aufgabe 1

### Activasion Function

ReLU

$$ max(0,x) $$

Sigmoid

$$ \frac{1}{1 + e^{-x}} $$

tanh

$$ \frac{e^{2z} - 1}{e^{2z} + 1} $$

Softmax

$$ \frac{e^{x_{[i]}}}{\sum^K_{k=1} e^{x_{[k]}}} $$

## Aufgabe 2

### Hamming Distance

Die Hamming-Distanz ist eine metrische Methode, die die Anzahl der unterschiedlichen Positionen zwischen zwei gleich langen Zeichenketten zählt.

### BIO tagging

Beim BIO-Tagging werden Wörter oder Tokens in einem Text mit Tags versehen, um die Anfangspunkte (B), die Inneren (I) und alles außerhalb (O) von benannten Entitäten zu kennzeichnen und so Named Entity Recognition (NER) zu ermöglichen.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ddee6e2f-b6ac-4072-9472-68a18fc5b48b/Untitled.png)

## Aufgabe 3

### BERT Downstream Tasks

- single sequence classification
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8e528698-7721-437f-bbed-425ae2ef53d8/Untitled.png)
    
- sentence pair classification
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a3dcadf3-fb2b-45ab-a3d0-1eddfa2cf200/Untitled.png)
    
- span extraction QA
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/962543f3-7343-40c6-b52f-62220c7c2ebe/Untitled.png)
    
- sequence labeling
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/499c2714-76ab-47cd-9148-60ef747b6ec7/Untitled.png)
    

### BERT Training Tasks

- MLM := Wörter werden gemasked und BERT soll predicten was da vorher war
- NSP := Zwei Sätze als Eingabe und es soll vorhergesagt werden ob der zweite Satz wirklich auf den anderen folgt

### Transformers vs. RNNs

- Transformer können lqnge Abhängigkeiten gut einfangen
- Transformer können parallel aggieren

## Aufgabe 4

### Einfacher Weg für sentence embeddings

- Alle Wort embeddings addieren
- dann durch Anzahl teilen

### Unterschiede zwischen Encoder-Decoder Transformer und BERT

- BERT ist ein Encoder only Modell

### Self attention

## Aufgabe 5

## Aufgabe 6

# Übungen

## Übung 1

- Perceptron is used for binary classification
- ReLU is nicht stetig differenzierbar
- Ein Perceptron kann…
    - separate data with a hyperplane
    - solve the OR problem
    - solve the AND problem
    - decide all linearly separable sets
    - NICHT XOR lösen

Perceptron Training

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/afd18520-521f-4185-8fb1-8dc22f94b48e/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6365d391-c944-49c6-9707-0e8a66f5e7f9/Untitled.png)

Neural Network Funktion

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9ef10a6e-263c-4f9e-b171-c5ba75890eaf/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1d98012f-19c4-4f1e-89a8-7494505d20a7/Untitled.png)

## Übung 2

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e411759e-d4ad-4a70-afe6-54c8105fcb49/Untitled.png)

Back propagation

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/abb7875a-ef05-4759-b6ea-8c435c1af279/Untitled.png)

# Coding

- data = pd.read_csv(data_loc, delimiter=’\t’)
- selected = data[(data['word1'] == 'happy') & (data['word2'] == 'young')]['SimLex999'].item()

# Fragensammlung

What is NLP and how does it relate to deep learning? How do log-linear models differ from deep neural networks in text classification? What are language models and how are they used in text generation? How do RNNs encode text information and what are some limitations of this approach? What is self-attention and how does it improve upon RNNs for text classification? What is BERT and how does it use self-attention for language modeling? How do Transformers differ from RNNs and what advantages do they offer for text generation? What is GPT and how does it use a decoder-only model for language modeling? How can prompting and in-context learning improve upon traditional LLMs? ?

Harder: What are some potential ethical concerns related to the development and use of large language models like GPT? How do different evaluation metrics (e.g., precision, recall, F1 score) help us assess the performance of NLP models? What are some common pre-processing steps that are applied to text data before it can be used for NLP tasks? How can transfer learning be used to improve the performance of NLP models on new tasks or domains? What is adversarial training and how can it be used to improve the robustness of NLP models against attacks? How do attention mechanisms work in neural networks and what advantages do they offer for NLP tasks? What is unsupervised learning and how can it be used for NLP tasks like clustering or topic modeling? How can reinforcement learning be used to train NLP models that interact with users (e.g., chatbots)? What are some challenges associated with training deep learning models on large-scale text datasets, and how can they be addressed? How do different types of word embeddings (e.g., GloVe, Word2Vec) differ in terms of their architecture and performance on downstream tasks?

What is the difference between deep learning and traditional machine learning algorithms? How can natural language processing be used in real-world applications? Can you explain the concept of backpropagation and how it is used in deep learning?

What are some common challenges in natural language processing, and how can deep learning help address them? How do mathematical concepts like calculus and linear algebra relate to deep learning? Can you explain the concept of overfitting in deep learning, and how it can be avoided? What are some popular deep learning frameworks or libraries, and how do they differ from each other? How can deep learning be used for tasks like sentiment analysis or machine translation? Harder: Can you explain the difference between supervised and unsupervised learning in the context of natural language processing, and give an example of each? How can deep learning be used for tasks like question answering or text summarization? What are some common challenges in training deep neural networks, and how can they be addressed? Can you explain the concept of attention mechanisms in deep learning, and how they can be used for tasks like machine translation? How can deep learning be used for more advanced natural language processing tasks like sentiment analysis at the document level or named entity recognition?

What is the IMDB dataset and how is it used in binary sentiment classification? Can you explain what a logistic regression model is and how it relates to neural networks? How do log-linear models work for text classification and what are their advantages? What are some challenges of applying supervised machine learning to natural language processing tasks? How can numerical representations be used to analyze natural language text? Harder: Can you explain how sparsity affects natural language processing and how it can be addressed using log-linear models? How does the choice of feature representation impact the performance of log-linear models for text classification? Can you explain how regularization is used to prevent overfitting in log-linear models and how it affects model performance? What are some limitations of using logistic regression models for natural language processing tasks and how can they be addressed using more complex models? How can unsupervised learning techniques be used to improve the performance of supervised machine learning models for natural language processing tasks? Can you explain how deep neural networks are used for text classification and what advantages they offer over traditional machine learning models?

What is the difference between a parameter and a hyperparameter in deep learning? How does the choice of loss function affect the performance of a neural network? Can you explain how regularization techniques such as L1 and L2 regularization work in deep learning? Harder: How does the vanishing gradient problem affect the training of deep neural networks, and what are some techniques to mitigate this issue? Can you explain how convolutional neural networks (CNNs) are used in natural language processing, and provide an example of a successful application? What is transfer learning in deep learning, and how can it be applied to improve the performance of NLP models?

Example questions: What is the difference between a unigram and a bigram language model? How do you train a neural language model? Can you explain the concept of backpropagation in MLP models? What is the purpose of using pre-trained word embeddings in natural language processing? How do you evaluate the performance of a language model? Can you give an example of how non-linearity can improve the performance of a neural network? Harder: What is the difference between a continuous bag-of-words (CBOW) and a skip-gram model for word embeddings? How do you handle out-of-vocabulary words in a language model? Can you explain the concept of perplexity in language modeling and how it is calculated? What are some common techniques for regularization in neural language models? How do you incorporate contextual information into a language model?

Example questions: What is the difference between deep learning and traditional machine learning? How can natural language processing be used in chatbots? What are some common text classification tasks? How do word embeddings help with natural language processing tasks? Can you explain how neural language models work? What is the distributional hypothesis and how does it relate to word embeddings? Can you explain the difference between word2vec and FastText embeddings? Harder: How can you evaluate the quality of word embeddings? What are some challenges in using word embeddings for low-resource languages? Can you explain how contextualized word embeddings differ from static word embeddings? How can you incorporate domain-specific knowledge into pre-trained word embeddings? What are some techniques for reducing the dimensionality of high-dimensional word embeddings? Can you explain how adversarial training can be used to improve the robustness of text classification models? How can you handle out-of-vocabulary words when using pre-trained word embeddings?

Example questions: What is the difference between NLP and traditional programming? How does deep learning differ from other machine learning techniques? Can you explain the concept of a recurrent neural network and how it is used in NLP? What is text classification and how can it be applied in real-world scenarios? Can you provide an example of vector concatenation and how it can be used in NLP? How does the CBOW method work in NLP? What is the Markov property and how is it relevant to NLP? What are some advantages of using gated architectures over simple RNNs in NLP? Can you explain the concept of LSTM and its role in NLP? Harder: How can RNNs be used for language modeling and what are some challenges associated with this approach? What is the difference between a unidirectional and bidirectional RNN, and how can they be used in NLP tasks? Can you explain the concept of attention mechanisms in NLP and how they can improve the performance of RNNs? What are some common techniques for pre-processing text data before feeding it into an NLP model? How can transfer learning be applied to NLP tasks, and what are some benefits of this approach? Can you explain the concept of generative models in NLP, and provide an example of how they can be used to generate text? What is the role of word embeddings in NLP, and how do they differ from traditional one-hot encoding methods? How can unsupervised learning techniques such as clustering or topic modeling be applied to text data in NLP? Can you discuss some ethical considerations that arise when using NLP models for tasks such as sentiment analysis or language translation? What are some current challenges facing the field of NLP, and what research directions are being pursued to address these challenges

Example Questions:

- What is Deep Learning and how is it used in NLP?
- Can you explain the concept of an Autoregressive Encoder-Decoder model and its applications in NLP?
- How do Recurrent Neural Networks (RNNs) differ from other types of neural networks, and what advantages do they offer for NLP tasks?
- What is the Attention Mechanism, and how does it improve the performance of encoder-decoder models in NLP?
- Can you explain the Abstracted Attention Mechanism and its design choices in more detail?
- What are some common NLP tasks that can benefit from encoder-decoder architectures with attention mechanisms?
- What is the Creative Commons Attribution-ShareAlike 4.0 International License, and how does it apply to this PDF? Harder:
- How does the use of an Autoregressive Encoder-Decoder model with attention mechanisms compare to other state-of-the-art approaches for text generation tasks such as GPT-3?
- Can you explain how the Abstracted Attention Mechanism can be extended to handle long-term dependencies in NLP tasks?
- What are some challenges associated with using Recurrent Neural Networks (RNNs) for NLP tasks, and how have researchers attempted to address these challenges?
- How can Deep Learning techniques be used to improve the performance of traditional rule-based systems for NLP tasks such as named entity recognition or sentiment analysis?
- What are some ethical considerations that arise when using Deep Learning models for NLP tasks, and how can these concerns be addressed?

Example Questions How does the attention mechanism contribute to the performance of Transformer models in natural language processing? Can you explain the concept of contextualized representations and their significance in NLP tasks? What are the key components of the encoder-decoder architecture in Transformer models? How do Transformers address the issue of modeling long dependencies in sequences compared to recurrent networks? Can you provide an overview of the research conducted by Dr. Martin Tutek in the field of NLP? What is the role of the Ubiquitous Knowledge Processing department at the Technical University of Darmstadt? Harder What are some potential challenges or limitations of using Transformers in natural language processing tasks, and how are researchers addressing them? Can you explain the concept of positional embeddings in Transformers and how they contribute to the model's understanding of word order in a sequence? In the context of Transformers, what are byte-pair encodings and how do they help in handling out-of-vocabulary words? How does the self-attention mechanism in Transformers differ from traditional attention mechanisms used in recurrent neural networks? What are some recent advancements or variations of the Transformer model that have been proposed in the field of natural language processing? How does the concept of transfer learning apply to Transformers, and what are some benefits and challenges associated with it in NLP tasks?

What is the Transformer architecture and how does it relate to contextualized representations? How do byte-pair encodings and positional embeddings improve natural language processing? Can you explain the differences between the encoder and decoder blocks in the Transformer model? What are some useful resources for learning more about the Transformer and BERT models? What are some variants of pretraining tasks for BERT? What is the pretraining objective for BERT? Can you provide an example of how self-attention works in the Transformer model? How does BERT perform on text classification tasks compared to other models? What are some limitations of the Transformer and BERT models? How can the Transformer and BERT models be fine-tuned for specific natural language processing tasks? Harder How does the Transformer model compare to other models in terms of computational efficiency and accuracy? Can you explain how the BERT model is able to capture both local and global context in natural language processing? What are some potential applications of the Transformer and BERT models beyond natural language processing? How do the Transformer and BERT models handle out-of-vocabulary words? Can you explain how the attention mechanism in the Transformer model can be used for tasks beyond natural language processing? What are some challenges in fine-tuning the Transformer and BERT models for specific natural language processing tasks? How do the Transformer and BERT models handle long sequences of text? Can you explain how the pretraining objective for BERT differs from other pretraining objectives used in natural language processing? What are some limitations of the self-attention mechanism used in the Transformer model? How do the Transformer and BERT models handle tasks that require reasoning and inference, such as question answering?

What is the difference between autoregressive decoder-only models and bidirectional encoder-only transformers? How can zero-shot learning be used in natural language processing? What is prompting and how can it be used in text generation? What is the purpose of GPT-2 in question answering? What is the license for content from ACL Anthology papers? Harder In the GPT-2 model, what are the differences between zero-shot question answering and prompted one-shot question answering? , Can you explain the concept of bidirectional encoder-only transformers and their advantages in downstream tasks? How does autoregressive decoding contribute to text generation in decoder-only models? What are some potential limitations or challenges associated with zero-shot learning in natural language processing? Could you provide a brief overview of the image from the GPT2 paper related to zero-shot question answering?

### Techincal Terms

- Online Learning
    
    updating weights after every single input point is called online learning
    
- Batch processing
    
    minimize the error over a larger number of data points, called a batch
    
- reinforcement learning
    
- perceptron
    
- binary sentiment classification
    
- supervised machine learning
    
- self supervised learning
    
- sub-word embeddings
    
- NLP (Natural Language Processing)
    
- Deep Learning
    
- Log-linear models
    
- Deep neural networks
    
- LMs (Language Models)
    
- Word embeddings
    
- RNNs (Recurrent Neural Networks)
    
- Self-attention
    
- BERT (Bidirectional Encoder Representations from Transformers)
    
- Transformers
    
- GPT (Generative Pre-trained Transformer)
    
- LLMs (Large Language Models)
    
- Minimize functions
    
- Multivariate functions
    
- Heavily nested functions
    
- Efficient computation of gradient
    
- Stochastic gradient descent
    
- Backpropagation
    
- Numerical representation of natural language text
    
- Binary text classification
    
- Log-linear models
    
- Supervised machine learning
    
- Finding the best model's parameter
    
- Loss function for softmax
    
- Decision rule and natural interpretation of the log-linear model
    
- Word embeddings
    
- MLP (Multilayer Perceptron)
    
- Non-linearity
    
- Neural language models
    
- Classical language models
    
- Deep Learning
    
- Natural Language Processing
    
- Text Classification
    
- Word Embeddings
    
- Neural Language Models
    
- Distributional Hypothesis
    
- Word2Vec
    
- FastText Embeddings
    
- Natural Language Processing (NLP)
    
- Deep Learning
    
- Recurrent Neural Networks (RNN)
    
- Text Classification
    
- Vector Concatenation
    
- Vector Addition/Averaging (CBOW)
    
- Markov Property
    
- Simple RNN
    
- Gated Architectures
    
- Long Short-Term Memory (LSTM)
    
- Natural Language Processing (NLP)
    
- Autoregressive Encoder-Decoder
    
- Recurrent Neural Networks (RNNs)
    
- Attention Mechanism
    
- Abstracted Attention Mechanism
    
- NLP Tasks
    
- Transformers
    
- Contextualized Representations
    
- Encoder-Decoder Architecture
    
- Attention Mechanism
    
- Recurrent Networks
    
- Long Dependencies
    
- Transformer architecture
    
- Contextualized representations
    
- Byte-pair encodings
    
- Positional embeddings
    
- Encoder and decoder blocks
    
- Pretraining tasks
    
- Pretraining objective
    
- Self-attention
    
- Text classification
    
- Fine-tuning
    
- Types of Transformer Architectures
    
- Autoregressive decoder-only Models
    
- Zero-shot, one-shot and few-shot learning
    
- Prompting
    
- Prompt-tuning MLMs