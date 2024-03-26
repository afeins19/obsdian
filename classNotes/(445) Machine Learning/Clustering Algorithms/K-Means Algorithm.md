- randomly select k-centroids where k is equal to the number of clusters you choose 
	- centroids are data points representing the center of a cluster 
- Expectation-maximization
	- the expectation step assigns each data point to its nearest centroid
	- the maximization step computes the mean of all the points for each cluster and sets the new centroid 

```
k = number of clusters to assign
randomlly initialize k centroids 

while centroid positions change from last iteration:
	expectation: assign each point to its closest centroid
	maximization: compute the new centroid of each cluster 
```

### Quality of the cluster assignments 
defined as the SSE (sum squared error) of the Euclidean distance between each point and its centroid 
- k-means tries to minimize this SSE so it tries to select centroids that minimize these distances 

### Choosing the Appropriate Number of Clusters 
- elbow method 
- silhouette coefficient 
- complementary evaluation techniques rather than one being preferred over the other 


the elbow method: run k-means several times and increment k with each iteration and plot the SSE. an **Elbow point** is the sweet-spot where the SSE curve starts to bend - a reasonable tradeoff between error and numbers of clusters.
![[Screen Shot 2024-03-15 at 2.05.50 PM.png]]

**Sillhoutte Coefficient**  $$S(i)=\frac{b(i)-a(i)}{max{a(i),b(i)}}$$
- S(i) is the silhoutte coefficient of the data point i
- a(i) is the average distance between ia and all the other data points in the cluster to which I belongs
- b(i) is the average distance from i to all clusters to which i does not belong

as S(i) -> 1  implies that its a good approximation of a set of points and S(i) -> 0 implies it is not good. 

![[Screen Shot 2024-03-15 at 2.11.16 PM.png]]

### Choosing the Appropriate number of Clusters 
we can use this coefficient to see how well this coefficient responds to the number of clusters we set k equal to
![[Screen Shot 2024-03-15 at 2.10.51 PM.png]]

