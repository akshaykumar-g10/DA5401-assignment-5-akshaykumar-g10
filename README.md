# DA5401 Assignment 5: Visualizing Data Veracity Challenges in Multi-Label Classification
- AKSHAY KUMAR G
- ME22B044

  
## **Objective**  
To analyze **gene expression data** from the **Yeast Dataset** and explore **data quality issues** using **dimensionality reduction techniques** (t-SNE and Isomap). The goal is to understand challenges for a multi-label classifier caused by:
- Noisy or ambiguous labels  
- Outliers in gene expression  
- Hard-to-learn samples in mixed regions
  
## **Problem Statement**
The **Yeast Dataset** contains:
- **Features (X):** 103 gene expression levels per experiment  
- **Targets (Y):** 14 functional categories (multi-label)  

Tasks:
1. Visualize data structure using **t-SNE** and **Isomap**.  
2. Identify noisy labels, outliers, and ambiguous regions.  
3. Simplify visualization using the **two most frequent single-label classes** and the **most frequent multi-label combination**, labeling all others as “Other”.  


## **2. Tasks & Solutions**

### Part A: Preprocessing

1. **Data Loading**  
   - Loaded features (`X`) and multi-label targets (`Y`) from ARFF/CSV files.  

2. **Dimensionality Check**  
   - 103 features, 2417 data points.  

3. **Label Selection for Visualization**  
   - Selected **two most frequent single-label classes** and the **top multi-label combination** for coloring.  
   - All remaining data points labeled as “Other”.  
   - Counts of each category printed for verification.  

4. **Scaling**  
   - Standardized features to mean=0, variance=1.  
   - Required because distance-based methods (t-SNE, Isomap) are sensitive to feature scales.  

### Part B: t-SNE and Veracity Inspection

1. **t-SNE Implementation**  
   - Applied t-SNE to reduce `X_scaled` to 2 dimensions.  
   - Tested **perplexities**: [5, 10, 20, 30, 40, 50, 60, 70, 80] 
   - Observed effects on cluster separation and noise.  

**Observations:**
- Dark clusters indicate **distinct, learnable groups**.  
- Light-gray/blue points correspond to **ambiguous or noisy samples**.  
- Perplexity ~30 provides a balance between local and global structure.
<img width="882" height="590" alt="image" src="https://github.com/user-attachments/assets/fd6d74cc-14c7-4a5b-b95b-88336fffa45c" />


### Part C: Isomap and Manifold Learning

1. **Isomap Implementation**  
   - Applied Isomap on `X_scaled` to reduce to 2 dimensions.  
   - Explored **different `n_neighbors` values**: 5, 10, 15, 20.  

**Observations:**
- Isomap preserves **global manifold structure**.  
- Helps identify **clusters and overall geometry**, but less sensitive to local neighborhood density than t-SNE.  
- Dark clusters represent well-defined functional categories; light-blue points reveal ambiguous regions.

<img width="882" height="590" alt="image" src="https://github.com/user-attachments/assets/eef7295e-d164-43e1-9d1e-9472789da05a" />


## Conclusion

- t-SNE highlights **local anomalies** and **hard-to-learn samples** in ambiguous regions.  
- Isomap provides insight into **global manifold structure** and cluster relationships.  
- Label simplification (top 2 single-labels + top multi-label combo) makes plots interpretable.  
- Combined, these methods help **understand challenges for multi-label classification** in yeast gene expression data.  

---
