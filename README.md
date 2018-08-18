## Dealing with unlabeled data (Semi-supervised learning)
### Case Study (MNIST-Fashion dataset)
### by Mehmet Solmaz, August 2018

#### Problem definition: Given a huge dataset, only a small part of which is assigned a known label (out of a set of N), and also given a human labeler that comes at a cost. How to build a classifier while minimizing the cost?
#### In other words, formally given: <br> (1) A small dataset with (x,y) pairs,<br> (2) Large dataset with (x,) pairs. <br> Our goal is to find a better classifier than from just the labeled data alone. 

Firstly, this problem is between Supervised and Unsupervised Learning algorithms (Semi-supervised). We only have certain amount of labeled data. In the case of Big Data, the percentage of labeled data could be less than 1%. Even if we get a human labeler at a certain cost, we might not be able to label each data point.<br>
Here are some approaches to be considered:

1- First approach could be using the small subset of data for training, and use it to label the rest of the unlabeled data. Then use it to retrain the whole dataset and build a model <br>
2- Second approach could be using Clustering on the dataset. We can decide the class by looking at the majority of labeled data points in that cluster. 

In this notebook, I have tried to simulate the first approach on an MNIST-Fashion image dataset. Image dataset was chosen because they require a human labeler for classification purposes.<br>

MNIST-Fashion dataset comes with all the data labeled. To mimick a semi-supervised learning problem, I have deliberately removed certain percentages (99%, 95%, 90%, and 80%) of data and built classifiers with minimal data. That is, I have built classifiers with 1%, 5%, 10%, 20% of the initial data while randomly removing the rest. At each time, I have predicted the labels of unused data using the ML model, and compared with the Ground Truth (already labeled data). I have also built a classifier using 100% of the data and obtained performance metrics. 

For each classifier, I recorded the f1-scores, which were later used in Curve-Fitting to obtain a trend between Used Data Percentage and f1-score. The fitted function (logarithmic) reveals that there is a inflexion point where the increase in f1-score slows down. In this experiment, the inflexion point is around 15%. This point can be used as the minimum performance point to be reached via the help of human labelers. 

To sum up, to minimize the cost associated with human labelers, they should be used to add labels to the dataset only in the large performance increment regime. If the performance of the classifier starts slowing down at consecutive increments, this is the point to stop human labeling because there may not be any substantial improvement in classification performance.

__Footnote__: Another dataset may not show the same behavior as MNIST. From what I have gathered from the literature, datasets with high quality labels are more suitable for this approach. MNIST is one of them. 
