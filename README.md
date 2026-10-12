# Smart Dashboard for Makan Bergizi Gratis (MBG) Distribution

## Overview
This project applies Average Linkage cluster analysis to identify priority regions for Indonesia's Free Nutritious Meal Program (Makan Bergizi Gratis, MBG), a government initiative that received a Rp 71 trillion allocation in the 2025 state budget. The clustering results are presented through a public, interactive dashboard designed to bridge the transparency gap between government implementation and public oversight. The work was submitted as Project for GAMMAFEST 2025, IPB University.

## Objectives
- Identify priority groups of regions for MBG distribution using Average Linkage cluster analysis.
- Develop an interactive dashboard as a transparency and accountability tool for MBG implementation.
- Provide recommendations to improve the effectiveness of MBG distribution based on the clustering results.

## Data
- 540 regencies/cities across 38 Indonesian provinces.
- Four variables: percentage of poor population (BPS, 2024), Food Security Index/IKP (National Food Agency, 2024), number of schools, and number of school-age children (DAPODIK, Ministry of Education, 2024).

## Methodology
1. Data validation and reconciliation: checked correlation structure, standardized all variables via z-score to place four differently scaled indicators on a comparable footing, and confirmed the absence of multicollinearity (VIF between 3.4 and 6.5, all below the threshold of 10).
2. Euclidean distance matrix computed across all 540 regions as the basis for clustering.
3. Four Hierarchical Clustering methods (single, complete, average, and Ward's linkage) were compared using silhouette scores; Average Linkage was selected for producing the most balanced, representative grouping (5 clusters, silhouette score 0.511 at k=5), even though Complete Linkage showed a marginally lower Sw/Sb ratio.
4. Cluster stability validated using multiscale bootstrap resampling (AU values above 95% for most hierarchy segments).
5. Regions ranked into five intervention-priority tiers based on cluster-level averages across all four indicators.
6. Results visualized in a public Streamlit dashboard with an interactive Folium map of Indonesia.

## Key Findings
- Average Linkage with 5 clusters was selected as optimal, balancing a reasonably low Sw/Sb ratio (0.298) with strong bootstrap-confirmed stability and alignment with the program's five-phase rollout design.
- Cluster 1 (469 regions) shows the highest poverty rate (10.42%) and lowest school density relative to student population, making it the top intervention priority.
- Cluster 5 (24 regions) has relatively low poverty (7.05%) but the lowest Food Security Index (70.01) and the largest school-age population (over 1.15 million children), placing it second priority due to food security risk.
- Cluster 4 (Tangerang alone) shows the most favorable profile, with the lowest poverty rate (6.55%) and solid food security, representing the lowest intervention priority.

## Business/Government Relevance
The five-tier priority framework gives the government a data-driven basis for phasing MBG rollout rather than distributing the Rp 71 trillion budget uniformly. Regions in Cluster 1 and Cluster 5, which combine high poverty or low food security with large student populations, can be prioritized first, while well-resourced regions like Cluster 4 can be treated as lower urgency. The public dashboard directly addresses the transparency gap identified in national surveys, where only 37% of Indonesians believe government assistance programs operate transparently, by giving citizens direct access to the same regional prioritization data used in policy discussions.

## Tools & Libraries
Python, SciPy/scikit-learn (hierarchical clustering, silhouette score), statsmodels (VIF), pandas, Streamlit (dashboard), Folium (interactive map).

## Live Dashboard
- https://clusteringmbg.streamlit.app/

## Repository Contents
- `MBG_regional_dataset_2024.csv` — dataset of 540 regencies/cities with the four clustering variables.
- `MBG_Dashboard.py` / notebook — full analysis and Streamlit dashboard code (preprocessing, clustering, validation, visualization).
- `README.md` — project documentation in English and Indonesian.

## Limitations
Cluster interpretation and prioritization rely on equally weighted indicators; a different weighting scheme reflecting specific policy priorities (e.g., emphasizing food security over school infrastructure) could shift regional rankings. The Average Linkage method, while chosen for practical and stability reasons, does not have the lowest Sw/Sb ratio among the methods tested, meaning some trade-off between statistical optimality and interpretability was accepted.
