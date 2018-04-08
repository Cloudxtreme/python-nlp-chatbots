### Word embedding 

Image and audio data is rich and high dimesnional consisting of pixel-intensities (for images) or power spectral densities(for audio) which can be readily used to perform any tasks. However, natural language processing systems traditionally treat words as discrete atomic symbols, and therefore 'cat' may be represented as Id537 and 'dog' as Id143. These encodings are arbitrary, and provide no useful information to the system regarding the relationships that may exist between the individual symbols.

One approach is to use a distinct flag for each word. Suppose there are 10000 distinct words in a corpus, a single word like "Hello" will be represented as a 1 x 10000 vector with one 1, for Hello and rest all 0's. This kind of representation is called **One-Hot-Encoding**. Representing text data in a vectorized form will lead to very big sparse matrices (consists of only 1s and 0s). This will lead to even more weights to train in neural networks will only lead to increase in computational time.

Another disavdantage with this kind of an approach for representing text data is that the similarities between the words in not accounted for. The eucledian distance between any two words is going to be the same. However, in reality that is not the case, some words are similar in meaning or can be found near to each other in a sentence. This needs to be captured in the vectorized representation of text data.

**Word Embedding** is a solution to tackle all these problems. It is an approach to provide a **dense** vector representation of words that also capture something about their meaning.  In this approach, a word represented as a 1x 10000 vector in **One-Hot-Encoding** will be represnted as a 1 x 300 vector. Note that 300 is just a random number I just chose, it can be any number. In this representation the eucledian distance between words such as "like" and "enjoy" (which we know are similar) would be lesser in comparison with the distance between "like" and another irrelevant word like "planet.

There are two famous word embedding methods called **word2vec** by researchers at Google and **GloVe** by researchers at Stanford.

### word2vec embedding methodology

**word2vec** is one algorithm learning a word embedding from a text corpus. There are two main training algorithms that can be used to learn the embedding from text; **continuous bag of words (CBOW)** and **skip grams**.

Let's take a sentence to look at how both the approaches work. Consider the sentence below:

"The quick brown fox jumped over the dog"

Say we are using a window size of 2 i.e., 2 words to the left and right. For CBOW, the input and output on which the network wll be trained is as shown below:

Input| Output
-------|---------
\{The, quick,fox,jumped}|\{brown}
\{quick, brown,jumped,over}|\{fox}
\{brown,fox,over,the}|\{jumped}
\{fox,jumped,the,dog}|\{over}

The **skip-gram** appraoch training would be the same except the input and output just get swapped. This approach is more like **predicting the context given the word** while the CBOW approach is like **predicting the word given its context**.

Input| Output
-------|---------
\{brown}|\{The, quick,fox,jumped}
\{fox}|\{quick, brown,jumped,over}
\{jumped}|\{brown,fox,over,the}
\{over}|\{fox,jumped,the,dog}

  In word2vec, a simple neural network with a single hidden layer will be trained, but then we're not actually going to use that neural network for the task we trained it on. Instead the goal is actually to learn the weights of the hidden layer, which are actually the word vecotrs that we are trying to learn.
  
  Word2Vec models require a lot of text. Training your own word vectors may be the best approach for a given NLP problem. But it can take a long time, a fast computer with a lot of RAM and disk space, and perhaps some expertise in finessing the input data and training algorithm. Fortunately for us, we can simply use an existing pre-trained **word2vec** word embeddings developed by Google or Stanford's **GloVe** word embeddings.
 
 
 
 