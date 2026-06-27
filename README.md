# K-means-Clustering-Evaluation

## Palmer Penguins K-means Clustering Analysis

This notebook performs K-means clustering on the Palmer Penguins dataset to identify natural groupings among the penguins based on their physical attributes. The analysis covers data loading, preprocessing, optimal K determination, clustering, and interpretation.

## Dataset Overview

The **Palmer Penguins dataset** contains measurements for three species of penguins (Adelie, Chinstrap, Gentoo) collected from three islands in the Palmer Archipelago, Antarctica. For this unsupervised clustering task, we focused solely on the numerical physical attributes to discover inherent structures within the data without relying on the known species labels.

**Key Features Used:**
*   `bill_length_mm`: Length of the culmen (bill) in millimeters.
*   `bill_depth_mm`: Depth of the culmen (bill) in millimeters.
*   `flipper_length_mm`: Flipper length in millimeters.
*   `body_mass_g`: Body mass in grams.

## Preprocessing Choices

1.  **Categorical Variable Removal:** The original dataset includes categorical variables (`species`, `island`, `sex`). For this unsupervised K-means clustering task, these were removed to ensure the clustering is solely based on numerical morphological features and to avoid biasing the algorithm with pre-existing labels.
2.  **Missing Value Handling:** Rows containing any missing values (`NaN`) across the numerical features were removed from the dataset. This resulted in a cleaned dataset of 342 entries.
3.  **Feature Scaling:** K-means is a distance-based algorithm, making it sensitive to the scale of features. To ensure that all features contribute equally to the distance calculations, the numerical features (`bill_length_mm`, `bill_depth_mm`, `flipper_length_mm`, `body_mass_g`) were scaled using `StandardScaler`. This transforms the data such that each feature has a mean of 0 and a standard deviation of 1.

## Justification for Selected K Value (k=3)

Determining the optimal number of clusters (`k`) is a critical step in K-means. Two methods were employed:

*   **Elbow Method:** This method plots the Sum of Squared Distances (Inertia) against the number of clusters. The 'elbow' point, where the rate of decrease in inertia significantly slows down, suggests a suitable `k`. For this dataset, an elbow was observed at `k=3`.
*   **Silhouette Score:** This metric measures how similar an object is to its own cluster compared to other clusters, with higher scores indicating better-defined clusters. The Silhouette Score plot showed the highest score at `k=2`, with `k=3` also yielding a reasonably good score.

**Decision for k=3:** While the Silhouette Score suggested `k=2` as optimal, a deeper comparison of the cluster characteristics for `k=2` vs. `k=3` revealed that `k=3` provided a more granular and biologically meaningful segmentation. Given the original dataset comprises three distinct penguin species, choosing `k=3` allows for the potential discovery of these species through clustering. The subsequent interpretation confirmed that `k=3` indeed mapped very well to the three known species.

## Key Clustering Insights

After applying K-means with `k=3` and analyzing the cluster centroids (mean feature values for each cluster), the following insights were gained:

*   **Cluster 0 (Gentoo-like):** Characterized by penguins with moderately long bills, relatively shallow bill depths, long flippers, and heavy body mass. This cluster strongly aligns with the characteristics of **Gentoo penguins**, which are typically the largest species.

*   **Cluster 1 (Adelie-like):** Comprises penguins with the shortest bill lengths, deepest bill depths, shortest flipper lengths, and lightest body mass. This profile is highly consistent with **Adelie penguins**, which are generally smaller.

*   **Cluster 2 (Chinstrap-like):** Represents penguins with the longest bills, intermediate bill depths, intermediate flipper lengths, and intermediate body mass. These characteristics closely match those of **Chinstrap penguins**.

Visualizations (Pairplots and PCA 2D scatter plots) further confirmed these distinctions, showing clear separation of the three clusters across the feature space, particularly when examining combinations of flipper length, body mass, and bill dimensions. The clustering successfully identified the three main groups corresponding to the different penguin species based solely on their physical measurements.

## Limitations and Next Steps

### Limitations:
*   **K-means Assumptions:** K-means assumes spherical clusters of similar size and density, which might not always hold true for biological data.
*   **Sensitivity to Outliers:** The algorithm can be sensitive to extreme values.
*   **Pre-specification of K:** Determining `k` often involves subjective interpretation, as seen with the Elbow and Silhouette methods.

### Potential Next Steps:
*   **Validate with Species Data:** Integrate the original `species` column to quantitatively evaluate the purity and accuracy of the clusters.
*   **Explore Other Algorithms:** Apply alternative clustering methods (e.g., DBSCAN, Hierarchical Clustering, Gaussian Mixture Models) to compare results and potentially uncover different patterns.
*   **Advanced Visualization:** Utilize t-SNE or UMAP for even richer low-dimensional visualizations if the number of features were higher.
*   **Incorporate Categorical Features:** Investigate techniques for including categorical features (`island`, `sex`) in the clustering process.

This analysis demonstrates the effectiveness of K-means clustering in uncovering latent structures in data, successfully differentiating penguin species based on their morphological characteristics.
