# Optimasi Parameter Proses Fermentasi Bioetanol Menggunakan Algoritma Metaheuristik

**Project by:** Ardiansyah (Process Engineer)  
**Status:** Completed (Milestone 1)

---

## 1. Laporan Teknis Proyek

### a. Ringkasan Singkat (Executive Summary)
Proyek ini bertujuan untuk mengoptimalkan proses fermentasi bioetanol dengan menyeimbangkan dua tujuan yang saling bertentangan: memaksimalkan **Ethanol Yield (g/L)** dan meminimalkan **Energy Consumption (kWh)**. Menggunakan pendekatan *Data-Driven*, kami melatih model Machine Learning sebagai fungsi tujuan (fitness function) dan membandingkan empat algoritma metaheuristik: GA, PSO, GWO, dan ACO.

**Hasil Utama:** Algoritma **Ant Colony Optimization (ACO)** terbukti menjadi metode pencarian solusi terbaik dengan skor fitness tertinggi (**47.22**), mengungguli algoritma lainnya dalam menemukan titik operasi yang paling efisien.

### b. Pendahuluan dan Latar Belakang
Dalam industri bioteknologi, biaya produksi bioetanol sangat dipengaruhi oleh konsumsi energi (listrik untuk agitasi dan kontrol suhu) serta efisiensi konversi substrat. Tantangan utamanya adalah fenomena non-linear di mana peningkatan *yield* seringkali membutuhkan input energi yang tidak proporsional. Oleh karena itu, diperlukan optimasi parameter operasional (Suhu, pH, Waktu, Substrat, Agitasi) untuk mencapai profitabilitas maksimum.

### c. Analisis Data (Exploratory Data Analysis - EDA)
Berdasarkan analisis dataset historis fermentasi:
* **Distribusi Data:** Variabel *Ethanol Yield* menunjukkan distribusi yang dipengaruhi oleh kondisi ekstrem (outlier), mengindikasikan sensitivitas proses terhadap perubahan parameter.
* **Korelasi:** Teridentifikasi korelasi positif kuat antara *Substrate Concentration* dan *Yield* hingga titik jenuh tertentu. Sebaliknya, *Agitation Speed* memiliki korelasi linear terhadap *Energy Consumption*.
* **Sweet Spot:** Scatter plot multivariat menunjukkan zona optimal enzimatis berada pada rentang suhu dan pH spesifik yang sempit, yang menjadi batasan ruang pencarian optimasi.

### d. Pemodelan Machine Learning dan Validasi
Model regresi dibangun untuk memprediksi *output* fermentasi berdasarkan 5 variabel input. Model ini digunakan sebagai *surrogate model* untuk mengevaluasi fungsi fitness dalam algoritma optimasi.
* **Input:** Temperature, pH, Fermentation Time, Substrate Concentration, Agitation Speed.
* **Output:** Ethanol Yield, Energy Consumption.
* **Metode:** Ensemble Learning (Random Forest / Gradient Boosting) dipilih karena akurasi tinggi dalam menangkap pola non-linear.

### e. Optimasi Metaheuristik dan Perbandingan Algoritma
Kami melakukan eksperimen komputasi menggunakan 4 algoritma populernya untuk mencari parameter global optimum. Berikut adalah rekapitulasi hasil kinerja (berdasarkan fungsi fitness gabungan):

| Peringkat | Algoritma | Fitness Score | Keterangan |
| :--- | :--- | :--- | :--- |
| **1** | **Ant Colony Optimization (ACO)** | **47.22** | **Best Performance (Winner)** |
| 2 | Grey Wolf Optimizer (GWO) | 45.50 | Runner-up, konvergensi cepat |
| 3 | Genetic Algorithm (GA) | 45.00 | Stabil namun terjebak lokal optima |
| 4 | Particle Swarm Opt. (PSO) | 34.59 | Performa terendah pada kasus ini |

### f. Pembahasan Hasil
ACO unggul dalam kasus ini kemungkinan karena kemampuannya dalam mengeksplorasi ruang pencarian yang kompleks (fermentasi memiliki banyak *local optima*) melalui mekanisme *pheromone trail*. Algoritma ini berhasil menemukan kombinasi parameter yang memberikan *yield* tinggi tanpa lonjakan konsumsi energi yang berlebihan, yang gagal ditemukan oleh PSO (fitness 34.59).

### g. Link Google Colab (Reproducible)
Seluruh kode, mulai dari EDA, pemodelan, hingga simulasi optimasi dapat dijalankan ulang melalui link berikut:
[🔗 **Buka Notebook di Google Colab**](PASTE_LINK_COLAB_KAMU_DISINI)

---

## 2. Rekomendasi Operasi Optimal
Berdasarkan hasil simulasi terbaik menggunakan algoritma **ACO**, berikut adalah set parameter operasi (Setpoint) yang direkomendasikan untuk diterapkan di lantai produksi (Plant Floor):

| Parameter | Simbol | Nilai Rekomendasi (Setpoint) | Satuan |
| :--- | :---: | :---: | :---: |
| **Temperature** | $T$ | **31.2** | °C |
| **Fermentation Time** | $t$ | **59.7** | Jam |
| **Substrate Conc.** | $S$ | **65.76** | g/L |
| **Energy** | $kwh$ | **4635.47** | Kwh |

> *Catatan: Nilai di atas adalah hasil konvergensi terbaik yang memberikan keseimbangan optimal antara produktivitas dan biaya energi.*

---

## 3. Kesimpulan Manajerial (Business Decision)

### a. Analisis Cost-Benefit (Produktivitas vs Energi)
Penerapan parameter hasil ACO diproyeksikan memberikan peningkatan efisiensi total (Fitness Score 47.22). Secara kuantitatif:
* Dibandingkan rata-rata historis (baseline), solusi ini **memaksimalkan konversi bahan baku** menjadi etanol.
* Menahan laju **konsumsi energi** agar tidak melonjak (mencegah *over-agitation* atau *over-heating* yang tidak perlu).
* Potensi penghematan OPEX (Operating Expense) signifikan dari pengurangan tagihan listrik per batch tanpa mengorbankan volume produksi.

### b. Algoritma Terpilih untuk Sistem Kontrol
Direkomendasikan untuk mengintegrasikan logika **Ant Colony Optimization (ACO)** ke dalam sistem *Decision Support System* (DSS) pabrik. ACO terbukti paling stabil (robust) dan memiliki skor fitness tertinggi dibanding GA, PSO, dan GWO dalam menangani dinamika proses fermentasi ini.

### c. Langkah Strategis Penerapan (Next Steps)
1.  **Pilot Test:** Lakukan uji coba parameter rekomendasi pada satu bioreaktor skala kecil (5-10L) untuk validasi fisik.
2.  **SOP Update:** Perbarui *Standard Operating Procedure* (SOP) operator berdasarkan setpoint suhu dan pH baru.
3.  **Monitoring:** Implementasikan *dashboard* monitoring real-time untuk memastikan parameter aktual tidak menyimpang lebih dari 5% dari setpoint rekomendasi ACO.

---
*Repository ini disusun untuk memenuhi deliverables Milestone 1 - Process Engineering Optimization Project.*# optimasi-metaheuristik
