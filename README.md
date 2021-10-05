# Technical-Project-1-NLP

## NLP with Deep Learning 

- Neural Networks work in NLP because NN work in a continuous space where as text is a discrete space, to bridge this gap Word Embeddings were brought into pictures.

- **Word Embedding** were developed just as a lookup table to cover this gap. They are often pretrained on text corpus from co-occurence statistics.

- PROBLEMS : Initially the word embeddings were applied ina context free manner. Ex. Bank of a river and an Investment Bank. In both sentences the word _Bank_ has a different

- SOLUTION: We started making embedding by keeping the context in the corpus.

## Key Concepts of BERT 

- This is with reference to the videos of Chris McCormick

- It is very huge and expensive to train so, it compensates for that by leveraging Transfer Learning

- The way to understand BERT is to go as :

```mermaid
Attention --> Transformers --> BERT
```

- Let's try to skip them for now and move on :p, we will come back if needed 

- The flow that for now we are gonna follow is something like 

```
Input Representation and WordPiece embeddings --> BERT Applications --> BERT training --> BERT Transformer

In BERT Training we will see Masked Language Model and Next Sentence Prediction
```

## Input and WordPiece Embeddings 

- **Word Embedding** - This is a feature representation of a word. In BERT every word (around 30K words) has a fixed set of Features (768 around features) and it has some floating point value associated with it. Once you put in a word, there is a dictionary which maps it to it's id and then it look's up for the embedding value.So Basically what happen is that 

```
word ---BERT Word Embedder--> [......768 columns with some floating values......]
```

Now BERT has a fixed vocabulary of 30K words, So what happens if we encounter a new word??

- It **Breaks downs unknown words into subwords**
```
KROXYLDYPHIVC - is broken into K + RO + X + LD + YP + HI + VC

since there might be subwords which are also not present in BERT vocabulary, BERT contains embeddings for each letters also. 
After breaking into subwords BERT doesnot combine them, instead it uses them as seperate embedding so you might have more embeddings than words due to this reason.
NOTE: The FastText Model had information about subwords also.
```
- In BERT Model Token some of the words start with **"##"** these words denotes the subword 

## Fine Tuning Bert - 1
- BERT Models have too many parameters to trains and the weights alone weight around 400 MB
- The Embedding Layers have around 24M weights and the 12 transformers have around 7M X 12 weights with total of 109 M weights hence BERT is very large.
- For platform like twitter it becomes difficult to run such expensive models as the throughput is very high. So they use a method known as **distillation** to cut down unnecessary weights.  

### Knowledge Distillation 

- **Motivation :** To compress models
- Why not go with traditional Pruning for compression? _Answer:_ 1. It does not allow changing the model family 2. There might be some architecture dependent problems

- Knowledge Distillation depends on 
  - Consistency 
  - Patience
## Fine Tuning Bert - 2

- BERT is a very domain specific language: 
- The Following work can be done by BERT
  - Classification
  - Name Entity Relation
  - Part Of Speech Tagging 
  - Specific Question Answering
- The following cannot be done by BERT:
  - Language Model - Something that can tell you about next word and stuff
  - Text Generation
  - Translation

### Formatting Required for BERT
- We need to add special tokens at the start and the end of each sentence.
- We need to pad and Truncate all sentences to a single constant length, which we can choose but the max length is 512 tokens
- Explicitly differentiate real tokens from padding tokens with the "attention mask" this is basically a binary array.
- Some Special Tokens are :
  - \[SEP\] - Seperator Token used when two sentences are given and we are asked to determine something._It's id is 102_
  - \[CLS\] -Stands for classification token. Now, there are 12 transformer layers stacked on to each other, after the 12th layer the [CLS] embedding is passed to the classifier._It's id is 101._
  - \[PAD\] - Padding token is used to make the length constant and they do have an impact on the result and are computed on. _It's id is 0_






