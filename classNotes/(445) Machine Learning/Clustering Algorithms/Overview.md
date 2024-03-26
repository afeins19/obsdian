k-means is a **clustering** algorithm. 
# Clustering
a set of techniques for partitioning data into groups and clustering.
clustering is unsupervised where is classification is supervised. 

there are many different approaches and types of clustering. Some important factors to clustering include the features of the dataset, the number of outliers, and the number of data points. 
# Partitional Clustering
literally just dividing the data into non-overlapping groups. No object can be a member of more than 1 cluster.
- requires the user to specify the number of clusters given by some variable k
- k-means and k-medoids 
### Strengths 
- work well with spherically shaped clusters
- scalable with respect to algorithm compllexity
### Weaknesses
- not well suited fro clusters with complex shapes and different sizes 
- break down when used with clusters of different densities 
# Heirarchical Clustering 
determines a cluster assignment by building hierarchy 
- either a bottom-up or top-down approach
### Agglomerative Clustering
- bottom up approach
- merge 2 points that are the most similar
### Divisive approach 
- top down approach
- start with all points in one cluster and splitting the least similar clusters at each step 
- based on a tree hierarchy called a dendrogram 
# Density Based Clustering 
based on the density of data points in a region
- clusters are assigned where there are high densities of data points separated by low density regions
- density-based spatial clustering applications with noise (DBSCAN)
- ordering points to identify the clustering structure (OPTICS) 
### DBSCAN 
clustering to identify clusters of any shape in a data set containing noise and outliers
- clusters are defined as dense regions in the data space, separated by regions of lower density of points 
- for each point of a cluster, the neighborhood of a given radius has to contain at least a minimum number of points 

##### The Algorithm
- parameters: epsilon (eps) and minimum points (MinPts)
- epsilon defines the radius of neighborhood around a point x ($\epsilon-neighborhood$ )

- a **core point** is a point x in the data set with a neighbor count greater than or equal to MinPts. 
- a **border point** x is any point belonging to an $\epsilon -neighborhood$ of some core point with a neighbor count less than MinPts
- a **noise point** a point thats neither a border point or a core point

```
1. computer neighbbors of each point and identify core points 
2. join neighboring core points into clusters 

for each non-dense point:
	add to neighbboring cluster if possible (if its a core point)
	otherwise, its noise 
```


