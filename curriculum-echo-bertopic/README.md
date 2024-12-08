# **Technical Report: Analisis Kurikulum Merdeka Menggunakan Clustering dan BERTopic**

---

## **1. Overview**

Proyek ini bertujuan untuk menganalisis persepsi netizen terhadap Kurikulum Merdeka di Indonesia melalui data yang diambil dari Twitter menggunakan hashtag terkait. Solusi ini menerapkan *topic modeling* menggunakan **BERTopic** untuk menemukan pola dan topik dominan dalam diskusi online. Hasil analisis ini diharapkan memberikan wawasan mendalam bagi pemangku kebijakan pendidikan dan pihak terkait untuk memahami persepsi publik terhadap Kurikulum Merdeka.

---

## **2. Motivation**

Kurikulum Merdeka merupakan inisiatif besar dalam sistem pendidikan Indonesia yang bertujuan meningkatkan kualitas pembelajaran. Namun, pemahaman masyarakat tentang efektivitas dan implementasi kurikulum ini masih beragam. Dengan meningkatnya penggunaan media sosial, analisis persepsi netizen terhadap kebijakan pendidikan menjadi lebih relevan dari sebelumnya. Proyek ini bertujuan untuk menyediakan wawasan berdasarkan data aktual untuk membantu perbaikan kebijakan pendidikan di masa mendatang.

---

## **3. Success Metrics**

- **Kualitas Clustering**: Diukur menggunakan **silhouette score** untuk memastikan topik yang dihasilkan representatif dan terstruktur dengan baik.
- **Jumlah Topik yang Relevan**: Mengidentifikasi topik utama yang signifikan terkait Kurikulum Merdeka.
- **Wawasan yang Dihasilkan**: Jumlah dan kualitas wawasan yang dapat membantu pemangku kebijakan dalam memahami persepsi publik.
- **Akurasi Evaluasi**: Menilai efektivitas metode embedding dan algoritma clustering yang digunakan setelah *hyperparameter tuning*.

---

## **4. Requirements & Constraints**

### **4.1 Functional Requirements**

1. **Pengumpulan Data**: Mengambil data dari Twitter dengan hashtag seperti `#kurikulummerdeka` dan `#pendidikanIndonesia`.
2. **Preprocessing Data**: Membersihkan data (menghapus *stopwords*, emoji, dan data yang tidak relevan).
3. **Topic Modeling**: Menggunakan BERTopic untuk menemukan dan memvisualisasikan topik.
4. **Evaluasi Model**: Menggunakan **silhouette score** dan *hyperparameter tuning* untuk meningkatkan akurasi model.
5. **Dashboard Visualisasi**: Menyediakan visualisasi hasil clustering menggunakan **Power BI**.

### **4.2 Non-Functional Requirements**

1. **Performa**: Proses clustering harus selesai dalam waktu yang wajar, dengan target p99 latency < 2 menit untuk analisis kumpulan data besar.
2. **Biaya**: Mengoptimalkan penggunaan sumber daya untuk mengurangi biaya pemrosesan cloud (GCP Cloud Run).
3. **Keamanan**: Data harus diolah sesuai kebijakan privasi (data publik dari Twitter).
4. **Skalabilitas**: Sistem harus dapat menangani peningkatan jumlah data (hingga 50.000 tweet).

### **4.3 Constraints**

- **Teknis**: Penggunaan algoritma clustering seperti HDBSCAN, KMeans, atau Agglomerative sesuai dengan performa terbaik setelah *hyperparameter tuning*.
- **Waktu Pemrosesan**: Batas pemrosesan data maksimal 5 menit.
- **Biaya Infrastruktur**: Anggaran terbatas untuk penggunaan layanan cloud.

### **4.4 What's In-Scope & Out-of-Scope**

- **In-Scope**:  
  - Analisis topik dari data Twitter.  
  - Visualisasi hasil menggunakan Power BI.  
  - *Hyperparameter tuning* untuk BERTopic.  

- **Out-of-Scope**:  
  - Analisis sentimen mendalam.  
  - Penggunaan data dari sumber selain Twitter.  
  - Penyempurnaan model real-time.

---

## **5. Methodology**

### **5.1 Problem Statement**

Masalah ini diformulasikan sebagai **unsupervised learning problem** menggunakan *topic modeling* untuk menemukan dan mengelompokkan topik terkait Kurikulum Merdeka dari percakapan netizen di Twitter.

### **5.2 Data**

- **Sumber Data**: Data Twitter yang diambil menggunakan hashtag `#kurikulummerdeka` dan `#pendidikanIndonesia`.  
- **Jumlah Data**: Sekitar 15.000 sampel teks dari hasil scraping.  
- **Preprocessing**:  
  - Pembersihan teks (stopwords, emoji, URL).  
  - Tokenisasi.  
  - Stemming (opsional).

### **5.3 Techniques**

1. **Embedding Methods**:  
   - **SBERT**  
   - **IndoBERT**  
   - Evaluasi performa embedding dengan *hyperparameter tuning* menggunakan **Optuna**.

2. **Clustering Algorithms**:  
   - **HDBSCAN**  
   - **KMeans**  
   - **Agglomerative Clustering**  
   - Pemilihan algoritma terbaik berdasarkan **silhouette score**.

3. **Dimensionality Reduction**:  
   - **UMAP**  
   - **PCA**  
   - **t-SNE**  
   - Menggunakan Optuna untuk *hyperparameter tuning*.
