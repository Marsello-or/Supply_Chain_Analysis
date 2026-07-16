# End-to-End Supply Chain Optimization: Data Science & Operations Research Approach

[Looker Studio Dashboard](https://datastudio.google.com/reporting/47855884-ecd8-408f-86cb-616b5b1dfab5) | [Kaggle Dataset Source](https://www.kaggle.com/datasets/harshsingh2209/supply-chain-analysis)

## 1. Problem Statement & Objectives
Proyek ini bertujuan untuk menjawab tantangan operasional utama PT XYZ melalui pendekatan kuantitatif terpadu. Secara spesifik, sasaran strategis dari proyek analitik ini adalah:
1. **Inventory Optimization**: Menyeimbangkan tingkat ketersediaan produk dan meminimalkan probabilitas kehabisan stok melalui kalkulasi safety stock dan reorder point (ROP) yang dinamis.
2. **Quality Risk & COPQ Mitigation**: Memetakan performa vendor untuk mengidentifikasi pembengkakan biaya akibat cacat produksi melalui analisis Cost of Poor Quality (COPQ).
3. **Strategic Logistics Allocation**: Merancang skenario alokasi rute, kurir, dan volume pasokan yang menghasilkan biaya logistik paling minimum dengan menggunakan pemodelan matematika linear programming.
4. **Executive Data Storytelling**: Menerjemahkan hasil keputusan optimal ke dalam bentuk executive dashboard interaktif untuk membandingkan performa sebelum versus sesudah optimasi.

---

## 2. Tech Stack & Libraries
* **Language**: Python 3.8+
* **Data Manipulation**: pandas, numpy
* **Machine Learning / Clustering**: scikit-learn (K-Means)
* **Mathematical Optimization**: PuLP (Linear Programming Solver)
* **Statistical Simulation**: scipy.stats (Monte Carlo Simulation)
* **Visualization**: matplotlib, seaborn, Google Looker Studio

---

## 3. Methodology & Core Analysis

### A. Machine Learning Layer: K-Means Clustering (k=4)
Mengelompokkan 100 SKU ke dalam 4 kuadran risiko portofolio berdasarkan dimensi Revenue generated dan Defect rates.
* **Star Products**: High Revenue, Low Defect.
* **Quality Risk**: High Revenue, High Defect (Fokus audit penahanan COPQ).
* **Operational Burden**: Low Revenue, High Defect (Efisiensi ekstrem).
* **Sleeper Products**: Low Revenue, Low Defect.

### B. Simulation Layer: Monte Carlo Simulation & Technical Engineering (SS & ROP)
* Melakukan 10.000 iterasi simulasi untuk menguji variabilitas Lead Times dan Daily Demand menggunakan Distribusi Normal. Hasil awal membuktikan 95% - 100% probabilitas stockout pada sistem inventaris eksisting.
* Mengimplementasikan rumus variansi ganda untuk menghitung tingkat pengaman stok (Safety Stock) ideal dan Reorder Point (ROP) dengan target 95% Service Level guna mengeliminasi insiden lost sales.

### C. Operations Research Layer: Linear Programming (PuLP)
Merumuskan fungsi tujuan minimalisasi biaya logistik global dengan batasan kapasitas produksi pabrik (Supply Constraints) dan kebutuhan pasar (Demand Constraints). 
* Konversi biaya menggunakan skala Tarif Pengiriman per Unit Produk:
  Minimize Z = Sum(Volume_ijmc * Tarif_Per_Unit_ijmc)

---

## 4. Key Performance Indicators (KPI) Results

| Metric Indicators | Before Optimization | After Optimization | Delta / Impact |
| :--- | :---: | :---: | :---: |
| **Total Logistics Cost** | Rupee 554.81 | Rupee 125.54 | **-77.37% (Saved)** |
| **Stockout Risk Probability** | 95% - 100% (Critical) | < 5.00% (Controlled) | **Risk Eliminated** |
| **Logistics Allocation** | Scattered / Unstandardized | Carrier Consolidated (Road) | **Optimal Supply Network** |

---

## 5. Dashboarding & Insights Integration
Hasil optimasi dari skrip Python diekstraksi ke dalam bentuk berkas terstandardisasi untuk dikonsumsi oleh Google Looker Studio. 

* **Halaman 1: Inventory Control & Quality Risk**: Menyajikan peta zonasi K-Means individual per SKU, tabel status kesehatan inventaris (Restock Now vs Safe), dan deteksi Value Class (ABC Analysis).
* **Halaman 2: Logistics Matrix & Cost Optimization**: Menyajikan perbandingan side-by-side biaya pengiriman per rute serta visualisasi pergeseran pangsa pasar kurir (Carrier Consolidation).

[Akses Dashboard Looker Studio Interaktif di Sini](https://datastudio.google.com/reporting/47855884-ecd8-408f-86cb-616b5b1dfab5)

---

## 6. How to Run the Project
1. Clone repository ini:
```bash
git clone [https://github.com/username/supply-chain-optimization.git](https://github.com/username/supply-chain-optimization.git)
```
2. Unduh dataset asli dari Kaggle Dataset dan simpan di folder direktori kerja kamu.
3. Install library yang dibutuhkan:
```bash
pip install pandas numpy scikit-learn pulp scipy matplotlib seaborn
```
4. Jalankan Jupyter Notebook / Google Colab script secara berurutan untuk memproduksi file .csv hasil optimasi.
