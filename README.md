# Sarcasm-Detection-NLP
Exploratory techniques for Sarcasm Detection (NLP)
Natural language processing (NLP) is a technique where we make the machine understand human written linguistics. A natural language refers to the way humans use words to communicate ideas, feelings and emotions. There are basically two types of NLP
1.	Semantic NLP: Understanding the meaning and emotion
2.	Syntax NLP: Understanding the grammar and syntax of the sentence
Sarcasm Detection comes under Semantic NLP because it required understanding the meaning and emotion of a sentence. The Merriam-Webster dictionary defines sarcasm as “the use of words that mean the opposite of what you really want to say especially in order to insult someone, to show irritation, or to be funny.” 
It is known that the machine can learn almost everything humans can do but as we know it is sometimes difficult for even the humans to understand sarcasm which makes it more difficult to make the machines understand the same. A technique or a pattern needs to be found in sarcasm which can give a good enough accuracy to predict sarcasm.

Brief Idea: 
I have tried a different approach in identifying sarcasm which uses, Bi-gram generation, Bag of Words model (BOW) and Latent Dirichlet Algorithm (LDA) to generate different topics on which I try to predict if there is a “spin” in the sentence. 

Gathering data: 
I extracted all tweets with the word “sarcasm” in it. The idea being, a person uses the word “sarcasm” only two times in a tweets. Once while using it in a sentence or for explicitly stating that this statement is a sarcasm. We build two different corpuses where one contained all the regular twitter data (without the word sarcasm in it) and other contained all the sarcasm related data. This allowed me to perform proper classification between the two types of data.

Pre-processing: 
The tweets we extracted contained all types of unwanted text like URLs, smileys, special characters, stop words, etc. I performed the following pre-processing steps:
1.	Remove ordinal
2.	POS tagging: Performed POS tagging to identify grammatical meaning of every word like (Noun, Adjective, Verb, etc). The tags we used are 'JJ'(Adjective tagging), 'JJR', 'JJS', 'NN'(Noun), 'NNS', 'RB', 'RBR', 'RBS', 'VB', 'VBD', 'VBG', 'VBN', 'VBP', 'VBZ'[2]
3.	Token cleaning
4.	Removing punctuation
5.	Remove numbers
6.	Remove URLs
7.	Remove slash
8.	Remove Hyphen
9.	Remove small
10.	Normalise text
11.	Bigram generation

Topic modelling: 
The steps involved in working with topics are as follows:
1.	Dictionary formation: A dictionary object was formed which contains the frequency of all the words present in the pre-processed corpus along with frequencies of all the Bigrams generated which is then used to create a Bag of Words model. 
2.	Latent Dirichlet algorithm [4]: The above generate bag of words model is then fed to the LDA model to generate 100 different topics. LDA was performed using the predefined genism library [6] provided in Python. The model returns 100 different topics and the probabilities of the word that convey how likely is a particular word a part of that topic.
3.	Topic Modelling: After the topics were generated, it became important to understand that what sentences in the corpus comprise of what topics. Topic distribution is done here where sentences are examined over each of these topics to yield a probability of a sentence comprising of that topic.

Classification model:
The steps involved in building the classification model is as follows:
1.	Class encoding:

The twitter data is encoded so that I can recognise the tweets which are sarcasm and which are not. It’s similar to assigning class labels to the two types of data we have so that the classifier can build a model to predict sarcasm. The classes assigned to each type are (0 = Sarcasm, 1 = Regular).

2.	Random Forest Classification [3]: 

Random forest classification works as a large collection of decorrelated decision trees. Random forest model uses something called as bagging which is basically combining multiple models in order to increase the classification accuracy. Biased weights are provided for the classifier with 0.9 for Sarcasm and 0.1 for regular data because I am more interested in the sarcastic part of the data.

Results: 
I tried finding out various performance parameters for the model which I created. To understand how good my model was based on this idea we consider using F-score as measure. This is mainly because I have more number of samples in one category than another. 
F-score is a harmonic mean of precision and recall measure. I achieved an overall 0.793 Precision & 0.799 Recall. 
Overall F-Score 0.794

Pre-requisites: 
The following libraries are required to run the code.
1.	Nltk
2.	Scikit-learn
3.	Pickle
4.	Genism


How to Run:
1.	Extract all the content of the zip file at any location. 
2.	Open the command prompt and navigate the folder where everything is extracted.
3.	Type “python ModelRun.py”

References:
[1] Sarcasm as Contrast between a Positive Sentiment and Negative Situation Ellen Riloff, Ashequl Qadir, Prafulla Surve, Lalindra De Silva, Nathan Gilbert, Ruihong Huang, School Of Computing University of Utah
[2] http://stackoverflow.com/questions/15388831/what-are-all-possible-pos-tags-of-nltk
[3] https://en.wikipedia.org/wiki/Random_forest
[4] https://en.wikipedia.org/wiki/Latent_Dirichlet_allocation
[5] http://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html
[6] https://radimrehurek.com/gensim/models/ldamodel.html

