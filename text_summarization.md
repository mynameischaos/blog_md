---
title: Text Summarization
date: 2016-09-21 21:00:00
---

## Text Summarization
* **topic representation**(based on the topic to score the sentences.)
* **indicator representation**(often use ML to score the importance of each sentences.)
* **select sentences**(to summarize the text. such as greedy approach or globally optimizing)


### 1. How do Extractive Summarizers Work?
* **Intermediate representation**(Topic representation: frequency, TF-IDF, topic words, lexical chain——WordNet， latent semantic analysis, full blown Bayesain topic model)
* **Indicator representation**(represent the importance of each sentence.)
* **Score sentences**(by using machine learning techniques to discover indicator weights. such as LexRank)
* **Select summary sentences**(maximal marginal relevance approaches: iterative greedy procedure, global selection)

### 2. Topic Representation Approaches
1. **Topic Words**(topic signatures)
2. **Frequency-driven Approaches**(word probability and TF.IDF)
	* Word propability(SUMBASIC).
	* TF-IDF weighting(Term Frequency*Inverse Document Frequency).  (Centroid summarization.)
	* lexical chains(WordNet.)
	
3. **Latent Semantic Analysis** 
	* Matrix(Singular Value Decomposition, SVD)
4. **Bayesian Topic Models**
5. **Sentence Clustering and Domain-dependent Topics**

### 3. Influence of Context

### 3.1 Web Summarization

### 3.2 Summarization of Scientific Articles

### 3.3 Query-focused Summarization

### 3.4 Email-Summarization

### 4. Indicator Representations and Machine Leanring for summarization

### 4.1 Graph Methods for Sentence Importance 

### 4.2 Machine Learning for Summarization

### 5. Selecting Summary Sentences

### 5.1 Greedy Approaches: Maximal Marginal Relevance

### 5.2 Global Summary Selection







