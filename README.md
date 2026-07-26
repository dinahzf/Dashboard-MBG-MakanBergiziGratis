# Smart Dashboard untuk Distribusi Program Makan Bergizi Gratis (MBG)

## Ringkasan
Proyek ini menerapkan analisis cluster Average Linkage untuk mengidentifikasi wilayah prioritas penerima Program Makan Bergizi Gratis (MBG), sebuah inisiatif pemerintah yang menerima alokasi dana sebesar Rp 71 triliun dalam APBN 2025. Hasil clustering disajikan melalui dashboard interaktif publik yang dirancang untuk menjembatani kesenjangan transparansi antara pelaksanaan pemerintah dan pengawasan publik. Karya ini disusun sebagai Project 6 (ESC25004) untuk GAMMAFEST 2025, IPB University.

## Tujuan
- Mengidentifikasi kelompok wilayah prioritas penerima Program MBG menggunakan metode analisis cluster average linkage.
- Mengembangkan dashboard interaktif sebagai alat transparansi dan akuntabilitas dalam pelaksanaan program MBG.
- Memberikan rekomendasi untuk meningkatkan efektivitas distribusi Program MBG berdasarkan hasil analisis cluster.

## Data
- 540 wilayah kabupaten/kota di 38 provinsi di Indonesia.
- Empat variabel: persentase penduduk miskin (BPS, 2024), Indeks Ketahanan Pangan/IKP (Badan Pangan Nasional, 2024), jumlah sekolah, dan jumlah anak usia sekolah (DAPODIK, Kemendikbudristek, 2024).

## Metodologi
1. Validasi dan reconciliation data: memeriksa struktur korelasi, menstandarisasi seluruh variabel menggunakan z-score untuk menyetarakan empat indikator dengan skala berbeda, dan mengonfirmasi tidak adanya multikolinearitas (VIF antara 3,4 hingga 6,5, seluruhnya di bawah ambang batas 10).
2. Perhitungan matriks jarak Euclidean di seluruh 540 wilayah sebagai dasar clustering.
3. Empat metode Hierarchical Clustering (single, complete, average, dan ward's linkage) dibandingkan menggunakan silhouette score; Average Linkage dipilih karena menghasilkan pengelompokan yang paling seimbang dan representatif (5 cluster, silhouette score 0,511 pada k=5), meskipun Complete Linkage menunjukkan rasio Sw/Sb yang sedikit lebih rendah.
4. Stabilitas cluster divalidasi menggunakan multiscale bootstrap resampling (nilai AU di atas 95% untuk mayoritas segmen hierarki).
5. Wilayah diberi peringkat ke dalam lima tingkat prioritas intervensi berdasarkan rata-rata tiap cluster pada keempat indikator.
6. Hasil divisualisasikan dalam dashboard Streamlit publik dengan peta interaktif Indonesia menggunakan Folium.

## Temuan Utama
- Average Linkage dengan 5 cluster dipilih sebagai yang optimal, menyeimbangkan rasio Sw/Sb yang cukup rendah (0,298) dengan stabilitas kuat yang dikonfirmasi bootstrap serta keselarasan dengan desain peluncuran program lima fase.
- Cluster 1 (469 wilayah) menunjukkan tingkat kemiskinan tertinggi (10,42%) dan kepadatan sekolah terendah relatif terhadap populasi siswa, menjadikannya prioritas intervensi utama.
- Cluster 5 (24 wilayah) memiliki kemiskinan relatif rendah (7,05%) namun Indeks Ketahanan Pangan terendah (70,01) dan populasi anak usia sekolah terbesar (lebih dari 1,15 juta anak), menempatkannya sebagai prioritas kedua karena risiko ketahanan pangan.
- Cluster 4 (hanya Tangerang) menunjukkan profil paling baik, dengan tingkat kemiskinan terendah (6,55%) dan ketahanan pangan yang solid, menjadikannya prioritas intervensi terendah.

## Relevansi Bisnis/Pemerintahan
Kerangka prioritas lima tingkat memberikan pemerintah dasar berbasis data untuk membertahapkan peluncuran MBG, alih-alih mendistribusikan anggaran Rp 71 triliun secara seragam. Wilayah pada Cluster 1 dan Cluster 5, yang menggabungkan kemiskinan tinggi atau ketahanan pangan rendah dengan populasi siswa yang besar, dapat diprioritaskan lebih dahulu, sementara wilayah dengan sumber daya baik seperti Cluster 4 dapat diperlakukan dengan urgensi lebih rendah. Dashboard publik ini secara langsung menjawab kesenjangan transparansi yang teridentifikasi dalam survei nasional, di mana hanya 37% masyarakat Indonesia percaya program bantuan pemerintah berjalan transparan, dengan memberikan masyarakat akses langsung terhadap data prioritisasi wilayah yang sama dengan yang digunakan dalam diskusi kebijakan.

## Tools & Libraries
Python, SciPy/scikit-learn (hierarchical clustering, silhouette score), statsmodels (VIF), pandas, Streamlit (dashboard), Folium (peta interaktif).

## Dashboard Live
- https://clusteringmbg.streamlit.app/

## Isi Repository
- `MBG_regional_dataset_2024.csv` — dataset 540 wilayah kabupaten/kota dengan empat variabel clustering.
- `MBG_Dashboard.py` / notebook — kode analisis lengkap dan dashboard Streamlit (preprocessing, clustering, validasi, visualisasi).
- `README.md` — dokumentasi proyek dalam bahasa Inggris dan Indonesia.

## Keterbatasan
Interpretasi dan prioritisasi cluster mengandalkan pembobotan indikator yang sama rata; skema pembobotan yang berbeda sesuai prioritas kebijakan tertentu (misalnya menekankan ketahanan pangan dibanding infrastruktur sekolah) dapat menggeser peringkat wilayah. Metode Average Linkage, meskipun dipilih karena alasan praktis dan stabilitas, tidak memiliki rasio Sw/Sb terendah di antara metode yang diuji, yang berarti terdapat trade-off antara optimalitas statistik dan interpretabilitas yang diterima.

---------------------------------------------------------------------------------

# Smart Dashboard for Makan Bergizi Gratis (MBG) Distribution

## Overview
This project applies Average Linkage cluster analysis to identify priority regions for Indonesia's Free Nutritious Meal Program (Makan Bergizi Gratis, MBG), a government initiative that received a Rp 71 trillion allocation in the 2025 state budget. The clustering results are presented through a public, interactive dashboard designed to bridge the transparency gap between government implementation and public oversight. The work was submitted as Project 6 (ESC25004) for GAMMAFEST 2025, IPB University.

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
