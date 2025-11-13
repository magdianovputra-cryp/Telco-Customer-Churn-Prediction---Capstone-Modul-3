### **Latar Belakang**

Manajemen  perusahaan telekomunikasi PT. Nusantara Telekomindo ingin mengurangi tingkat churn pelanggan mereka. Churn pelanggan adalah situasi di mana pelanggan berhenti menggunakan layanan perusahaan dan beralih ke penyedia lain. Tingkat churn yang tinggi dapat berdampak negatif pada pendapatan dan pertumbuhan perusahaan.

Selama ini perusahaan mengeluarkan biaya promosi ke seluruh pelanggan, tanpa mengetahui siapa saja pelanggan yang benar-benar berisiko untuk churn. Hal ini menyebabkan pemborosan anggaran promosi, karena promosi diberikan kepada pelanggan yang sebenarnya tidak berisiko untuk churn.

---

### **Problem Statement**
Saat ini perusahaan tidak memiliki suatu alat atau sistem yang mampu memprediksi pelanggan mana yang berisiko tinggi untuk churn. Oleh karena itu, perusahaan ingin mengembangkan model prediksi churn pelanggan yang dapat mengidentifikasi pelanggan yang berisiko tinggi untuk churn, sehingga perusahaan dapat fokus memberikan promosi kepada pelanggan tersebut.

Diperlukan suatu model machine learning yang dapat membantu perusahaan dalam:
1. Memprediksi pelanggan yang berisiko tinggi untuk churn.
2. Mengoptimalkan anggaran promosi dengan menargetkan pelanggan yang berisiko tinggi untuk churn.
3. Mengurangi pembengkakan biaya promosi yang tidak efektif.

---

### **Metric Evaluation**
- Cost FP (False Positive) = Biaya promosi yang diberikan kepada pelanggan yang tidak berisiko churn = $100
- Cost FN (False Negative) = Biaya kehilangan pelanggan yang berisiko churn = $500

Karena cost FN lebih besar daripada cost FP, maka model yang dikembangkan harus meminimalkan jumlah FN sebanyak mungkin, sambil tetap menjaga jumlah FP pada tingkat yang dapat diterima.

Metrik evaluasi yang akan digunakan dalam model ini adalah F2-score, agar kita memberi bobot lebih pada FN sambil tetap memerhatikan FP.

---

### **Goals**
1. Mengembangkan model machine learning yang bisa memprediksi pelanggan yang berisiko untuk churn berdasarkan data historis pelanggan.
2. Mengurangi kerugian biaya akibat churn pelanggan dengan menargetkan promosi kepada pelanggan yang berisiko untuk churn.
3. Meningkatkan efisiensi anggaran promosi dengan mengurangi pemborosan pada pelanggan yang tidak berisiko churn.

---

### **Data Overview**
1. Data terdiri dari 4930 baris dan 11 kolom.
2. Terdapat 10 fitur dan 1 fitur target (churn).
3. Fitur terdiri dari 2 data tipe numerik dan 9 data tipe kategorikal.

---

### **Penjelasan isi dari tiap Kolom**
---
##### **Features**
---
-	Dependents: menunjukkan apakah pelanggan memiliki tanggungan atau tidak.
    * Tipe data: **object** (kategorikal)
    * Nilai unik: **Yes**, **No**
    * **Yes** : Pelanggan memiliki tanggungan.
    * **No** : Tidak memiliki tanggungan.
---
-	Tenure: menunjukkan jumlah bulan pelanggan telah berlangganan dengan perusahaan.
    * Tipe data: **int64** (numerik)
    * Nilai unik contoh: **1**, **2**, **3**, ..., **72** (73 nilai unik)
    * Angka lebih besar menunjukkan pelanggan telah berlangganan lebih lama.
---
-	OnlineSecurity: menunjukkan apakah pelanggan memiliki keamanan online atau tidak.
    * Tipe data: **object** (kategorikal)
    * Nilai unik: **Yes**, **No**, **No internet service**
    * **Yes** : Pelanggan memiliki keamanan online.
    * **No** : Pelanggan memiliki keamanan online, tetapi tidak digunakan.
    * **No internet service** : Pelanggan tidak memiliki keamanan online.
---
-	OnlineBackup: menunjukkan apakah pelanggan memiliki layanan cadangan online atau tidak.
    * Tipe data: **object** (kategorikal)
    * Nilai unik: **Yes**, **No**, **No internet service**
    * **Yes** : Pelanggan memiliki layanan cadangan online.
    * **No** : Pelanggan memiliki layanan cadangan online, tetapi tidak digunakan.
    * **No internet service** : Pelanggan tidak memiliki layanan cadangan online.
---
-	InternetService: menunjukkan apakah pelanggan berlangganan layanan internet atau tidak.
    * Tipe data: **object** (kategorikal)
    * Nilai unik: **DSL**, **Fiber optic**, **No**
    * **DSL** : Pelanggan berlangganan layanan internet dengan teknologi DSL.
    * **Fiber optic** : Pelanggan berlangganan layanan internet dengan teknologi Fiber Optic.
    * **No** : Pelanggan tidak berlangganan layanan internet.
---
-	DeviceProtection: menunjukkan apakah pelanggan memiliki perlindungan perangkat atau tidak.
    * Tipe data: **object** (kategorikal)
    * Nilai unik: **Yes**, **No**, **No internet service**
    * **Yes** : Pelanggan memiliki perlindungan perangkat.
    * **No** : Pelanggan memiliki perlindungan perangkat, tetapi tidak digunakan.
    * **No internet service** : Pelanggan tidak memiliki perlindungan perangkat.
---
-	TechSupport: menunjukkan apakah pelanggan memiliki dukungan teknis atau tidak.
    * Tipe data: **object** (kategorikal)
    * Nilai unik: **Yes**, **No**, **No internet service**
    * **Yes** : Pelanggan memiliki dukungan teknis.
    * **No** : Pelanggan memiliki dukungan teknis, tetapi tidak digunakan.
    * **No internet service** : Pelanggan tidak memiliki dukungan teknis.
---
-	Contract: menunjukkan jenis kontrak berdasarkan durasi.
    * Tipe data: **object** (kategorikal)
    * Nilai unik: **Month-to-month**, **One year**, **Two year**
    * **Month-to-month** : Pelanggan memiliki kontrak bulanan.
    * **One year** : Pelanggan memiliki kontrak satu tahun.
    * **Two year** : Pelanggan memiliki kontrak dua tahun.
---
-	PaperlessBilling: menunjukkan apakah pelanggan menggunakan penagihan tanpa kertas atau tidak.
    * Tipe data: **object** (kategorikal)
    * Nilai unik: **Yes**, **No**
    * **Yes** : Pelanggan menggunakan penagihan tanpa kertas.
    * **No** : Pelanggan tidak menggunakan penagihan tanpa kertas.
---
-	MonthlyCharges: menunjukkan jumlah biaya untuk layanan setiap bulan.
    * Tipe data: **float64** (numerik)
    * Nilai unik contoh: **72.9**, **82.65** (1422 nilai unik)
    * Angka lebih besar menunjukkan biaya bulanan yang lebih tinggi.
---
##### **Target**
---
-	Churn: Menunjukkan apakah pelanggan berhenti berlangganan atau tidak.
    * Tipe data: **object** (kategorikal)
    * Nilai unik: **Yes**, **No**
    * **Yes** → Pelanggan berhenti berlangganan.
    * **No** → Pelanggan tetap berlangganan.

 ---

 
