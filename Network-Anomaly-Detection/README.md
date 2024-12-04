# Network Anomaly Detection

The exponential growth of network traffic has led to an increase in network anomalies, such as cyber attacks, network failures, and hardware malfunctions. Network anomaly detection is a critical task for maintaining the security and stability of computer networks. The objective of this project is to implement clustering algorithms from scratch such as K-mean, Spectral Clustering, Hierarchical Clustering and DBSCAN. All of those clustering algorithms can be used for network anomaly detection.

## Table of Contents
- [Newtork Anomaly Detection](#network-anomaly-detection)
  - [Dataset](#dataset)
    - [Data Preprocessing](#data-preprocessing)
  - [Algorithms](#algorithms)
    - [K-mean](#k-mean)
        - [Pseudocode](#pseudocode)
    - [Spectral Clustering](#spectral-clustering)
        - [Pseudocode](#pseudocode-1)
    - [Hierarchical Clustering](#hierarchical-clustering)
        - [Pseudocode](#pseudocode-2)
    - [DBSCAN](#dbscan)
        - [Pseudocode](#pseudocode-3)
  - [Results](#results)
  - [Contributors](#contributors)


## Dataset
For this project, we will use the ["KDD Cup 1999" dataset](https://kdd.ics.uci.edu/databases/kddcup99/kddcup99.html?fbclid=IwAR2W62F9o8T5fllzvL-7mkA6amNjo8shdGi3QNfqCak86BEtBdLZUh-h8UI), which is a widely used benchmark dataset for network anomaly detection. This dataset contains network traffic data collected from a simulated environment, including features such as protocol type, service, source and destination IP addresses, source and destination ports, and attack types.

### Data Preprocessing
- The dataset contains 41 features, three of which are categorical (protocol_type, service, and flag) and the rest are numerical. We will use one-hot encoding to convert the categorical features into numerical features. We will also normalize the numerical features to have zero mean and unit variance.

- For spectral clustering, hierarchical clustering and DBSCAN, we will use only 0.00025% as the train set. The same data used in training will be also used in testing.

## Algorithms
- We will use 4 clustering algorithms for network anomaly detection: K-mean, Spectral Clustering, Hierarchical Clustering and DBSCAN. We will use the following metrics to evaluate the model: accuracy, precision, recall, F1 score, and conditional Entropy.

### K-mean

- The k-means algorithm is a method of clustering data points into k groups based on their similarity. 
Some advantages of k-means are:

1. Simple to implement and understand
2. It scales to large data sets and is efficient in terms of computation.
3. It can warm-start the positions of centroids and adapt to new examples.

- The k-means algorithm tries to minimize the within-cluster sum of squares (WCSS), which is the sum of squared distances between each data point and its cluster centroid. The algorithm is simple and fast, but it has some drawbacks, such as:

1. It requires the number of clusters k to be specified in advance, which may not be easy to determine.
2. It is sensitive to the initial choice of centroids, which may affect the final clustering result.
3. It may converge to a local optimum, which may not be the best possible clustering solution.
4. It assumes that the clusters are spherical and have similar sizes, which may not be true for some data sets.

#### Pseudocode
```python
Initialize k means with random values

--> Loop until convergence or for a given number of iterations:
    
    --> Iterate through items:
    
        --> Calculate the euclidean distance between item and all means
        
        --> Assign the item to closest mean
        
    --> Update means by calculating the average of all items belonging to the mean's cluster
```
### Spectral Clustering
  - Spectral clustering is an unsupervised machine learning technique that involves grouping data points into clusters based on their similarity in a high-dimensional space. This approach involves first transforming the data points into a lower-dimensional space using a spectral embedding technique, which retains the most important features of the data. Next, a clustering algorithm is applied to the transformed data points to group them into clusters.


  - Spectral clustering has several advantages, including its ability to handle non-linearly separable data, its ability to detect clusters of different shapes and sizes, and its robustness to noise. It is commonly used in various fields, such as image segmentation, social network analysis, and bioinformatics.

  - Furthermore, the performance of spectral clustering largely depends on the selection of appropriate parameters, such as the similarity measure, the number of clusters, and the spectral embedding technique. Therefore, careful parameter tuning is necessary for achieving optimal clustering results. Despite its advantages and wide applicability, spectral clustering may not be suitable for datasets with extremely large numbers of data points, as it involves computing the eigenvectors of the Laplacian matrix, which can be computationally expensive.

#### Pseudocode
```python
def spectral_clustering(data):
  1- Given a dataset with n data points and a desired 
  number of clusters k

  2- Construct a similarity matrix W where each element W[i,j] represents the similarity between data point i and j
  
  3- Construct a diagonal matrix D where D[i,i] is equal to the sum of the i-th row of the similarity matrix W

  4- Compute the Laplacian matrix L = D - W

  5- Compute the first k eigenvectors of the Laplacian matrix L and stack them to form a matrix V

  6- Normalize the rows of the matrix V to have unit length

  7- Perform k-means clustering on the rows of the normalized matrix V to obtain the final clustering result

```





### Hierarchical Clustering
- Hierarchical clustering is a type of unsupervised machine learning algorithm that groups similar data points together based on a distance or similarity measure. It creates a hierarchy of clusters, which can be visualized using a dendrogram. There are two main types of hierarchical clustering: agglomerative and divisive.

- Agglomerative hierarchical clustering starts by assigning each data point to its own cluster and then iteratively merges the two closest clusters until all the data points are in a single cluster. Divisive hierarchical clustering, on the other hand, starts with all data points in a single cluster and recursively splits it into smaller clusters until each data point is in its own cluster. This project only implements Agglomerative hierarchical clustering.

- Hierarchical clustering is extremely useful when we want to visualize the hierarchy between points, the dendrogram can help visualize the clustering structure and can be used to identify the optimal number of clusters. However, it's worth noting that selecting the optimal number of clusters can still be a subjective and challenging task, as there may be multiple valid ways to interpret the dendrogram and the optimal number of clusters may depend on the domain of the data.

- There are some potential drawbacks to hierarchical clustering. Firstly, it can be computationally expensive for large datasets, as the algorithm needs to compute a distance matrix between all pairs of data points. Secondly, the clustering results can be sensitive to the choice of distance metric and linkage method, which can significantly affect the resulting clusters. Finally, hierarchical clustering can be susceptible to the so-called chaining effect, where nearby clusters are merged into a single cluster even if they do not belong together, leading to suboptimal clustering results.

#### Pseudocode
```python
AGNES(D, k)
  C = {c1, c2, ..., cN} where ci = {xi}
  while |C| > k
    find a pair of clusters {ci, cj} that minimizes d(ci, cj)
    merge {ci, cj} into a new cluster {ci, cj}
    remove ci and cj from C
    add {ci, cj} to C
  return C
```

### DBSCAN
- DBSCAN is a density-based clustering algorithm where given a set of points in some space, it groups together points that are closely packed together (points with many nearby neighbors), marking as outliers points that lie alone in low-density regions (whose nearest neighbors are too far away). It is one of the most common clustering algorithms and also one of the most versatile, able to find clusters of any shape, as long as they are dense enough. It is also one of the most used clustering algorithms in real-world applications.

- One of the advantages of DBSCAN is that it does not require the number of clusters to be specified beforehand, unlike some other clustering algorithms. Additionally, DBSCAN can handle non-linearly separable data and is robust to outliers.

- However, there are some potential drawbacks to DBSCAN. Firstly, the choice of parameters, such as the neighborhood radius(eps) and minimum density threshold(n_neighbors), can significantly affect the resulting clusters, and determining the optimal parameters for a given dataset can be challenging. Secondly, the algorithm can struggle with datasets that have varying densities or irregular shapes, as the density threshold may not capture all the relevant structures in the data. Finally, DBSCAN can be computationally expensive for large datasets, as it requires a distance matrix computation and multiple passes through the data.

#### Pseudocode
```python
DBSCAN(D, eps, MinPts)
  C = 0
  for each unvisited point P in dataset D
    mark P as visited
    NeighborPts = regionQuery(P, eps)
    if sizeof(NeighborPts) < MinPts
      mark P as NOISE
    else
      C = next cluster
      expandCluster(P, NeighborPts, C, eps, MinPts)
```

## Results

- The results for each algorithm and the evaulation are explained in details in each notebook. [K-means](k-means-clustering.ipynb), [Spectral Clustering](spectralClustering.ipynb), [Hierarchical Clustering](hierarchicalClustering.ipynb) and [DBSCAN](DBSCAN.ipynb).
 
## Contributors

- [Yousef Kotp](https://github.com/yousefkotp)

- [Mohamed Farid](https://github.com/MohamedFarid612)

- [Adham Mohamed](https://github.com/adhammohamed1)