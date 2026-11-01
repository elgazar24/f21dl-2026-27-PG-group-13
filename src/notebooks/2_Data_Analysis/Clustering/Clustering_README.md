# Clustering

Checks whether DS1 patients form natural groups without using the labels, and whether those groups match CKD vs not CKD.

## Notebook

`DS1_Clustering.ipynb` uses the processed DS1 training set (320 rows, 24 features). Run `../Data_Preprocessing/DS1_Data_Preprocessing.ipynb` first.

## Methods

| Method | Idea | Setting |
|---|---|---|
| k-means | Groups around a centre | k from 2 to 8 |
| Hierarchical (Ward) | Tree of merges | Dendrogram, k from 2 to 8 |
| Gaussian mixture | Soft, oval groups | Diagonal covariance, k from 2 to 8 |
| DBSCAN | Dense regions, outliers as noise | min_samples 5, eps from 5-NN distance percentiles |

Clusters are compared with the labels using the Adjusted Rand index (ARI): 1 is a perfect match, 0 is random.

## Results

| | DS1 |
|---|---|
| PCA components for 90% variance | 12 of 24 |
| Best silhouette | 0.24 |
| ARI, k-means | 0.42 |
| ARI, hierarchical | 0.95 |
| ARI, Gaussian mixture | 0.21 |
| ARI, DBSCAN (best eps) | 0.66 |
| ARI, hierarchical, without 0/1 features | 0.90 |
| ARI, hierarchical, continuous only | 0.21 |
| ARI, hierarchical, 0/1 features only | 0.74 |

## Summary

- Hierarchical clustering recovers CKD vs not CKD almost exactly without seeing the labels
- k-means and the Gaussian mixture split by severity rather than diagnosis
- Silhouette alone would pick k-means, so clusters are also checked against the labels

## Limitations

- Euclidean distance on mixed 0/1 and numeric features
- 0/1 features are not scaled, so they count less in the distance
- Gaussian mixture assumes bell-shaped features
- Number of clusters chosen to match the labels (2)
