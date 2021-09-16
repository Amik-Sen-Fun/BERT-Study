# Technical-Project-1-NLP

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

## Fine Tuning Bert
- BERT Models have too many parameters to trains and the weights alone weight around 400 MB
 
