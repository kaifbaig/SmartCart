# SmartCart Customer Segmentation

An unsupervised machine learning project that segments e-commerce customers based on purchasing behavior, engagement, and customer characteristics to support targeted marketing and customer retention.

## Objective

The goal of this project is to identify meaningful customer segments from historical SmartCart customer data using unsupervised machine learning.

Multiple clustering algorithms (K-Means, Agglomerative Clustering, and DBSCAN) are evaluated to identify the most suitable approach for broad customer segmentation.

## Dataset & Setup

- **Original Records:** 2,240 customers
- **Cleaned Analysis Records:** 2,236 customers (after removing 4 demographic/income outliers: 3 records with age > 90 and 1 extreme income outlier > 600,000)
- **Original Attributes:** 22
- **Domain:** E-commerce customer behavior
- **Key Features:** Income, Recency, spending, purchase channels, website activity, demographics, campaign response, and customer tenure
- **Dataset File:** `smartcart_customers.csv` (included directly in the repository)

### Setup & Execution

Install the project dependencies and run the Jupyter notebook:

```bash
pip install -r requirements.txt
jupyter notebook SmartCart.ipynb
```

## Approach

1. Data preprocessing and missing-value handling
2. Feature engineering (Age, Customer Tenure, Total Spending, Total Children)
3. Exploratory data analysis
4. Outlier detection and data refinement
5. Categorical encoding
6. Feature standardization
7. K-Means clustering and evaluation (Elbow & Silhouette analysis)
8. Agglomerative clustering with dendrogram analysis
9. DBSCAN clustering and parameter selection (K-distance plot)
10. Clustering algorithm comparison
11. 3D PCA cluster visualization
12. Cluster characterization and business recommendations

## Clustering Results

Three clustering algorithms were evaluated on the standardized feature space:

| Algorithm | Clusters | Noise Points | Silhouette Score |
|---|---:|---:|---:|
| **K-Means** | **2** | 0 | **0.1844** |
| Agglomerative | 2 | 0 | 0.1497 |
| DBSCAN | 13 | 105 | 0.1331* |

> **\*Note on DBSCAN Evaluation:**
> DBSCAN identified 105 observations as noise points (`label = -1`). Its silhouette score (0.1331) was computed strictly on the non-noise clustered observations (`mask = labels_dbscan != -1`). Consequently, its silhouette score is not directly computed over the exact same set of observations as K-Means or Agglomerative Clustering (which cluster all 2,236 customers). Even when evaluated solely on its clustered subset, DBSCAN formed 13 fragmented micro-clusters and achieved a lower silhouette score than K-Means.

K-Means was selected as the final clustering approach because it produced the highest Silhouette Score among the evaluated methods and provided a clear, interpretable two-cluster customer segmentation.

The Elbow Method and Kneed algorithm were also evaluated during K selection. Kneed identified an elbow point at K=3, while the peak Silhouette Score was achieved at K=2. K=2 was selected based on overall evaluation and practical interpretability, providing a clean distinction between lower-value and higher-value customer groups.

## Customer Segments

### Cluster 0 – Low-Value Customers (1,263 customers, ~56.5%)

- **Average Income:** Approximately $37,352
- **Average Total Spending:** Approximately $165
- **Channel Activity:** Lower purchases across web (~2.8), catalog (~0.8), and store (~3.7) channels
- **Website Behavior:** Higher monthly website visits (~6.5 visits/month) but lower conversion
- **Campaign Response:** Lower campaign response rate (~9.7%)
- **Household:** Higher average number of children (~1.27)

### Cluster 1 – High-Value Customers (973 customers, ~43.5%)

- **Average Income:** Approximately $70,905
- **Average Total Spending:** Approximately $1,178
- **Channel Activity:** Higher purchases across store (~8.5), web (~5.7), and catalog (~5.1) channels
- **Website Behavior:** Fewer monthly website visits (~3.7 visits/month) with higher direct purchasing
- **Campaign Response:** Higher campaign response rate (~21.7%)
- **Household:** Lower average number of children (~0.54)

## Business Recommendations

### Cluster 0 (Lower Value / Price Sensitive)
- Use targeted discounts, promotional bundles, and introductory offers to incentivize first purchases.
- Retarget high-frequency web visitors with personalized email campaigns to improve conversion and repeat purchases.
- Highlight value-oriented and family-friendly products.

### Cluster 1 (Higher Value / Premium Shoppers)
- Focus on customer retention through exclusive loyalty programs, early access to new arrivals, and VIP benefits.
- Provide personalized catalog and premium product recommendations (e.g., wines, gourmet products).
- Offer premium customer support and omnichannel engagement.

These segments enable SmartCart to design targeted marketing and retention strategies instead of using a one-size-fits-all approach.

## Visualizations

### Correlation Heatmap

![Correlation Heatmap](images/correlation_heatmap.png)

### K-Means Evaluation

![K-Means Evaluation](images/kmeans_evaluation.png)

### Agglomerative Clustering

![Dendrogram](images/dendrogram.png)

### DBSCAN Parameter Selection

![K-Distance Plot](images/k_distance_plot.png)

### PCA Cluster Visualization

![3D PCA Visualization](images/pca_3d_clusters.png)

### Customer Segmentation

![Income vs Total Spending](images/income_vs_spending_clusters.png)

## Tech Stack

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- SciPy
- Kneed
- Jupyter Notebook

## Project Structure

```text
SmartCart/
│
├── smartcart_customers.csv
├── SmartCart.ipynb
├── README.md
├── requirements.txt
├── .gitignore
│
└── images/
    ├── correlation_heatmap.png
    ├── dendrogram.png
    ├── income_vs_spending_clusters.png
    ├── k_distance_plot.png
    ├── kmeans_evaluation.png
    └── pca_3d_clusters.png
```

## Conclusion

The SmartCart customer dataset was analyzed using unsupervised machine learning to identify meaningful customer segments based on purchasing behavior, engagement, and customer characteristics.

After data cleaning, feature engineering, categorical encoding, and standardization, K-Means, Agglomerative Clustering, and DBSCAN were evaluated and compared.

K-Means with two clusters provided the most suitable broad segmentation, cleanly identifying lower-value price-sensitive customers and higher-value omnichannel shoppers. These segments provide SmartCart with actionable guidance for targeted marketing, engagement, and retention strategies.
