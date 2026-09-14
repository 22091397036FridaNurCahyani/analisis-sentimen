# Analisis Sentimen Berita Harga Menggunakan BERT

## 📌 Deskripsi

Project ini merupakan implementasi **analisis sentimen pada data berita terkait harga** menggunakan pendekatan **Natural Language Processing (NLP)** dan model **BERT (Bidirectional Encoder Representations from Transformers)**.

Model yang digunakan adalah **`bert-base-multilingual-uncased`** yang di-fine-tune untuk melakukan klasifikasi teks ke dalam tiga kategori sentimen, yaitu:

* **Negative** — Sentimen negatif
* **Neutral** — Sentimen netral
* **Positive** — Sentimen positif

Project ini mencakup tahapan mulai dari persiapan dataset, eksplorasi data, preprocessing teks, tokenisasi menggunakan BERT, pembagian dataset, fine-tuning model, hingga evaluasi performa model.

---

## 🎯 Tujuan

Tujuan project ini adalah membangun model NLP yang mampu mengidentifikasi sentimen dari teks berita yang berkaitan dengan harga ke dalam tiga kategori sentimen:

> **Negative, Neutral, dan Positive**

Hasil klasifikasi dapat digunakan untuk memahami kecenderungan sentimen yang terdapat dalam data berita.

---

## 📊 Dataset

Dataset yang digunakan adalah:

**`gold-dataset-sinha-khandait.csv`**

Dataset dimuat secara langsung melalui Google Colab dan kemudian diproses menggunakan Pandas.

Pada tahap persiapan data:

* Kolom `News` diubah menjadi `news`
* Kolom `Price Sentiment` diubah menjadi `sentiment`
* Data dengan label `none` dihapus
* Label sentimen dikonversi menjadi nilai numerik:

| Sentimen | Label |
| -------- | ----- |
| Negative | 0     |
| Neutral  | 1     |
| Positive | 2     |

Setelah data dengan label `none` dihapus, terdapat **8.602 data** yang digunakan dalam proses preprocessing.

---

## 🔄 Tahapan Preprocessing

Sebelum digunakan oleh model BERT, data teks melalui beberapa tahapan preprocessing:

1. Mengubah teks menjadi lowercase
2. Menghapus HTML tags
3. Menghapus karakter beraksen
4. Melakukan contraction expansion
5. Menghapus karakter selain huruf, angka, dan spasi
6. Menghapus spasi berlebih
7. Melakukan tokenisasi menggunakan NLTK
8. Menghapus stopwords bahasa Inggris

Tahapan tersebut dilakukan untuk menghasilkan teks yang lebih bersih sebelum masuk ke proses tokenisasi BERT.

---

## 🤖 Model

Model yang digunakan adalah:

**BERT — `bert-base-multilingual-uncased`**

Model diimplementasikan menggunakan library **Hugging Face Transformers** dengan `BertForSequenceClassification`.

Konfigurasi klasifikasi:

* Model: `bert-base-multilingual-uncased`
* Jumlah kelas: **3**
* Maximum sequence length: **256 token**
* Batch size: **32**
* Optimizer: **AdamW**
* Learning rate: **2e-5**
* Epsilon: **1e-8**
* Epoch: **5**
* Scheduler: **Linear**
* Random seed: **42**

Model kemudian di-fine-tune menggunakan dataset yang telah diproses.

---

## 📚 Pembagian Dataset

Dataset dibagi menjadi tiga bagian:

| Dataset    | Jumlah Data |
| ---------- | ----------: |
| Training   |       6.966 |
| Validation |         775 |
| Testing    |         861 |
| **Total**  |   **8.602** |

Setiap teks ditokenisasi dengan panjang maksimum **256 token**.

---

## ⚙️ Training

Proses training dilakukan menggunakan **Google Colab** dengan GPU:

**NVIDIA Tesla T4**

Model dilatih selama **5 epoch**.

Hasil validation accuracy pada setiap epoch:

| Epoch | Training Loss | Validation Accuracy |
| ----: | ------------: | ------------------: |
|     1 |          0.66 |              82.11% |
|     2 |          0.35 |          **86.05%** |
|     3 |          0.28 |              84.61% |
|     4 |          0.23 |              85.50% |
|     5 |          0.20 |              84.68% |

Validation accuracy tertinggi diperoleh pada **epoch 2**, yaitu sekitar **86.05%**.

---

## 📈 Evaluasi Model

Setelah proses training selesai, model digunakan untuk melakukan prediksi terhadap **861 data testing**.

Evaluasi dilakukan menggunakan dua metrik:

### Accuracy

Accuracy digunakan untuk mengukur proporsi prediksi model yang sesuai dengan label sebenarnya.

**Hasil:**

> **87.0%**

### Matthews Correlation Coefficient (MCC)

MCC digunakan sebagai metrik tambahan untuk mengevaluasi kualitas klasifikasi berdasarkan hubungan antara prediksi dan label aktual.

**Hasil:**

> **0.753**

### Hasil Akhir

| Metric   |     Score |
| -------- | --------: |
| Accuracy | **0.870** |
| MCC      | **0.753** |

Berdasarkan hasil evaluasi pada dataset testing, model memperoleh **accuracy sebesar 87.0%** dan **MCC sebesar 0.753**.

---

## 🛠️ Tools & Technologies

Project ini menggunakan beberapa tools dan library berikut:

### Programming Language

* Python

### Machine Learning & NLP

* PyTorch
* Hugging Face Transformers
* Scikit-learn
* NLTK

### Data Processing

* Pandas
* NumPy
* BeautifulSoup
* Contractions

### Visualization

* Matplotlib
* Seaborn

### Environment

* Google Colab
* NVIDIA Tesla T4 GPU

---
