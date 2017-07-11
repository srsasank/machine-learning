# Machine Learning Engineer Nanodegree
## Capstone Proposal
Sarath Sasank 
July 11, 2017

## Proposal


### Domain Background


Quora is a place to gain and share knowledge—about anything. It’s a platform to ask questions and connect with people who contribute unique insights and quality answers. This empowers people to learn from each other and to better understand the world.

Over 100 million people visit Quora every month, so it's no surprise that many people ask similarly worded questions. Multiple questions with the same intent can cause seekers to spend more time finding the best answer to their question, and make writers feel they need to answer multiple versions of the same question. Quora values canonical questions because they provide a better experience to active seekers and writers, and offer more value to both of these groups in the long term. The problem here is to identify duplicate questions using Natural Language Processing and machine learning. The issue here is that similar sentences may have different meaning since the semantic similarity has to be checked

http://www.sciencedirect.com/science/article/pii/0888613X87900156

The link for a fuzzy matching algorithm study is given above. My idea is to use fuzzy matching techniques to identify similarity among sentences. This problem inspires me because Natural Language Processing is a huge step forward in machine learning due to the pain points of ambiguity of language and context related meaning changes.


### Problem Statement


In this section, clearly describe the problem that is to be solved. The problem described should be well defined and should have at least one relevant potential solution. Additionally, describe the problem thoroughly such that it is clear that the problem is quantifiable (the problem can be expressed in mathematical or logical terms) , measurable (the problem can be measured by some metric and clearly observed), and replicable (the problem can be reproduced and occurs more than once).


Given two pair of questions we need to identify if these two questions have same semantic meaning. The intent of the two questions should be same for the pair to be flagged as duplicates and if not it is not a duplicate. We can measure the log loss.Log Loss quantifies the accuracy of a classifier by penalising false classifications. Minimising the Log Loss is basically equivalent to maximising the accuracy of the classifier, but there is a subtle twist which we’ll get to in a moment. In order to calculate Log Loss the classifier must assign a probability to each class rather than simply yielding the most likely class. 

### Datasets and Inputs


In this section, the dataset(s) and/or input(s) being considered for the project should be thoroughly described, such as how they relate to the problem and why they should be used. Information such as how the dataset or input is (was) obtained, and the characteristics of the dataset or input, should be included with relevant references and citations as necessary It should be clear how the dataset(s) or input(s) will be used in the project and whether their use is appropriate given the context of the problem.

The input consists of train.csv and test.csv which has the following data fields. The field 'is_duplicate' is only present in train.csv and not in test.csv. Both these files can be downloaded from Kaggle
https://www.kaggle.com/c/quora-question-pairs/data

Data fields

id - the id of a training set question pair
qid1, qid2 - unique ids of each question (only available in train.csv)
question1, question2 - the full text of each question
is_duplicate - the target variable, set to 1 if question1 and question2 have essentially the same meaning, and 0 otherwise.

### Solution Statement



The solution is to identify key features and use them to predict whether a pair is a duplicate or not. The three features considered are word shared between two questions, jaccard similarity between n grams and the damareau levenshtein distance between the questions. We extract these three features from the text and then XGBoost is used to classify the pair into duplicates or not. The final answer is measured by comparing the predictions and actual values using log loss function.

### Benchmark Model


The benchmark model used here is by using only the words shared between the pair as feature and then classification is done on that. The drawback of the model is that there is no involvement of fuzzy matching algorithm to compare the sentences.

### Evaluation Metrics


Logarithmic loss (related to cross-entropy) measures the performance of a classification model where the prediction input is a probability value between 0 and 1. The goal of our machine learning models is to minimize this value. A perfect model would have a log loss of 0. Log loss increases as the predicted probability diverges from the actual label. So predicting a probability of .012 when the actual observation label is 1 would be bad and result in a high log loss.

### Project Design

There are three parts in the project. They are
1. Preprocessing
  The text is processed so that the unigrams and bigrams are extracted. Then tf idf is computed to get the word shares between the question pair. Stopwords should also be removed from the text and this should be used for the next steps.
  
2. Feature generation
   Features such as word share, unigram share count, bigram share count, jaccard similarity and damareau levenshtein distance are calculated from the text and these features are used as input to the classification model.
   
3. Modeling
    These features are used to create a classification algorithm and predict whether a pair is duplicate or not. XGBoost is used for classification and the parameters are used in such a way that we dont overfit.

-----------

