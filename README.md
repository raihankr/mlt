# Laporan Proyek Machine Learning - Raihan Khairul Rochman
# Deteksi Kualitas Udara Berdasarkan Parameter Zat Polutan

## Domain Proyek

Kualitas udara merupakan salah satu indikator utama dalam menilai tingkat kesehatan lingkungan dan dampaknya terhadap kesehatan manusia. Polusi udara yang dihasilkan dari aktivitas industri, transportasi, dan pembakaran bahan bakar fosil telah menjadi perhatian global karena berkontribusi pada berbagai penyakit pernapasan, kardiovaskular, hingga kematian dini.

Pengukuran kualitas udara dapat dilakukan dengan mengamati faktor-faktor zat polutan yang mencakup PM2.5, PM10, NO2, SO2, dan CO. Menurut Agusta Kurniawan (2018)<sup>1</sup>, dengan pengukuran indeks ISPU, pengaruh zat polutan tersebup pada nilai ISPU lebih dari 100 dapat menicu berbagai gangguan pernapasan dan kardiovaskular. 

Dalam projek ini, kami memanfaatkan data historis dari dataset *Air Quality and Pollutant Measurement* yang dipublikasikan di Kaggle. Dataset ini berfokus pada kualitas udara di berbagai daerah. Dataset ini mengandung tepat 5000 sampel atau baris yang mencakup faktor kritis lingkungan dan demografi yang berpengaruh terhadap tingkat polusi udara.

Dengan menggunakan pendekatan analisis prediktif, model *machine learning* dilatih untuk memahami pola dan tren yang ada pada dataset dan menghasilkan prediksi yang akurat untuk mengklasifikasikan tingkat kualitas udara di daerah tertentu. Analisis prediktif ini tidak hanya dapat membantu memantau kualitas udara secara efisien, tetapi juga memberikan peringatan dini bagi masyarakat dan pembuat kebijakan untuk mengambil tindakan preventif. 
  
<sup>1</sup> [Kurniawan, Agusta. "Pengukuran parameter kualitas udara (CO, NO2, SO2, O3 dan PM10) di Bukit Kototabang berbasis ISPU." Jurnal Teknosains 7.1 (2018): 1-13.](https://journal.ugm.ac.id/teknosains/article/view/34658) 

## Business Understanding

Kualitas udara yang buruk berdampak signifikan pada kesehatan manusia dan lingkungan. Oleh karena itu, pemerintah, industri, dan masyarakat membutuhkan cara yang efisien untuk memantau, menganalisis, dan memprediksi kualitas udara guna mengambil langkah mitigasi yang tepat.

### Problem Statements

- Bagaimana hubungan antara masing-masing parameter terhadap tingkat kualitas udara?
- Bagaimana tingkat kualitas udara di daerah dengan karakteristik tertentu?

### Goals

- Mengetahui hubungan antara masing-masing parameter terhadap tingkat kualitas udara.
- Membuat model machine learning untuk memprediksi tingkat kualitas udara berdasarkan parameter yang diberikan.

### Solution statements
- Membangun model klasifikasi dengan variabel *Air Quality* (kualitas udara) sebagai target.
- Membangun 3 model dengan algoritma yang berbeda dan mengevaluasi masing-masing model dengan metrik akurasi, presisi, *recall*, dan *f1 score*, serta *confusion matrix*.

## Data Understanding
Dataset yang kami gunakan adalah Air Quality and Pollutant Measurement yang dipublikasikan di Kaggle. Data ini berfokus pada pengukuran kualitas udara di berbagai karaktetistik wilayah. Dataset ini mengandung **tepat 5000 sampel** atau baris dan mencakup faktor kritis lingkungan dan demografi yang berpengaruh terhadap tingkat polusi udara.

Fitur-fitur yang diliput dalam dataset ini mencakup **suhu, kelembapan, konsentrasi PM2.5, PM10, NO2, SO2, CO, dan jarak ke daerah industri, serta kepadatan populasi**. Variabel target dalam dataset ini merupakan kualitas udara yang dikategorikan ke dalam *good* (baik), *moderate* (sedang), *poor* (buruk), dan *hazardous* (berbahaya)

- [Kaggle-Air Quality and Pollutant Measurement](https://www.kaggle.com/api/v1/datasets/download/mujtabamatin/air-quality-and-pollution-assessment).

### Variabel-variabel pada *Air Quality and Pollutant Measurement dataset* adalah sebagai berikut:

1. **Konsentrasi PM2.5 (µg/m³)**: Tingkat partikel halus.
2. **Konsentrasi PM10 (µg/m³)**: Tingkat partikel kasar.
3. **Konsentrasi NO2 (ppb)**: Tingkat nitrogen dioksida.
4. **Konsentrasi SO2 (ppb)**: Tingkat sulfur dioksida.
5. **Konsentrasi CO (ppm)**: Tingkat karbon monoksida.
6. ***Temperature* (°C)**: Suhu rata-rata.
7. ***Humidity* (%)**: Tingkat kelembapan.
8. ***Proximity_to_Industrial_Areas* (km)**: Jarak ke area industri terdekat.
9. ***Population_Density* (jiwa/km²)**: Kepadatan penduduk.
10. ***Air Quality***: Kualitas udara dalam kategori sebagai berikut:
    1) *Good*: Udara bersih dengan tingkat polutan rendah
    2) *Moderate*: Adanya beberapa polutan namun masih dapat diterima
    3) *Poor*: Polusi tampak yang dapat menyebabkan gangguan kesehatan bagi kelompok sensitif.
    4) *Hazardous*: Udara sangat berpolusi yang dapat menimbulkan gangguan kesehatan serius bagi semua orang.

\* Pada model ini saya hanya akan menggunakan fitur-fitur konsentrasi zat polutan (PM2.5, PM10, NO2, SO2, dan CO) serta *Air Quality* sebagai targetnya.

### *Missing Values*

Dataset yang saya digunakan dalam projek memiliki 5000 sampel dengan data yang lengkap. Tidak ada satupun *missing value* ditemukan pada sampel. 

### *Outliers*

<img src="https://github.com/user-attachments/assets/9a6c5be5-ab3e-47ff-bbc6-ab41d27f9a58" width="32%"/>
<img src="https://github.com/user-attachments/assets/5941119e-013d-472e-80c1-f75407e657fc" width="32%"/>
<img src="https://github.com/user-attachments/assets/8ea3b524-4ec2-499e-b17c-6f1884f1fde8" width="32%"/>
<img src="https://github.com/user-attachments/assets/4174c2b2-c89e-443a-b35f-ffb8e80ab7fb" width="32%"/>
<img src="https://github.com/user-attachments/assets/93dba22e-8f59-4c30-8e24-a1857f7693fd" width="32%"/>

Gambar di atas merupakan visualisasi *box plot* untuk mencari *outliers* dalam data. Tampak ada banyak sekali *outliers* (titik-titik kecil) pada setiap kolom. *Outliers* merupakan sampel yang nilainya cukup jauh dari cakupan umum data dan kemunculannya cukup jarang. 

### (*Univariate Analysis*) Distribusi Data Variabel Fitur

![image](https://github.com/user-attachments/assets/0a973a29-a7c1-4684-9780-6923d0b07625)

Berdasarkan gambar di atas, tampak variabel PM2.5, PM10, dan SO2 memiliki distribusi data miring ke kanan. Sedangkan, variabel NO2 memiliki distribusi data cenderung normal. Serta, variabel CO memiliki distribusi data bimodal yang ditunjukkan dengan adanya dua puncak.

### (*Univariate Analysis*) Distribusi Data Variabel Target

![image](https://github.com/user-attachments/assets/667d49a1-139f-49a4-937c-5b2e835eb1e9)

Pada gambar di atas terlihat jelas bahwa jumlah data untuk setiap kelas pada variabel target mengalamai ketidakseimbangan. Hal ini dampat berdampak pada pola yang akan dipelajari oleh model dan berpotensi menghasilkan bias. Oleh karena itu, kami menerapkan *oversampling* pada datazet untuk mempertahankan keseimbangan data.

### (*Multivariate Analysis*) Rata-Rata Nilai pada Fitur Numerik

![image](https://github.com/user-attachments/assets/5c855ade-0c99-483e-8be4-a1dbc1fd755b)
![image](https://github.com/user-attachments/assets/d355680d-25e7-480c-ae70-f07a07267ed5)
![image](https://github.com/user-attachments/assets/1ba9310b-ca15-4c85-a0a6-c065f0238dde)
![image](https://github.com/user-attachments/assets/9f8ed4ad-2060-458f-bf3f-8c5c16a28d9d)
![image](https://github.com/user-attachments/assets/c81baa3a-b7a5-4316-b592-ded818748c9f)

Pada kelima gambar di atas dapat disimpulkan sebuah pola bahwa setiap faktor atau fitur cenderung memiliki nilai yang rendah untuk kategori *Good* berdasarkan nilai rata-ratanya pada fitur tersebut, diikuti oleh kategori *Moderate*, *Poor*, lalu *Hazardous*, yang secara bertahap memiliki rata-rata nilai yang semakin besar pada setiap fitur.

## Data Preparation

### Menghapus Fitur yang Kurang Relevan

Kolom-kolom yang akan digunakan pada pelatihan model hanya fitur zat polutan yang mencakup konsentrasi PM2.5, PM10, NO2, SO2, dan CO, serta target "Kualitas Udara" (Air Quality). Selain kolom-kolom tersebut akan dihapus karena kurang relevan dan dapat menggangu konsistensi serta akurasi model.

### Menangani Outliers

Pada tahap ini, semua *outliers*, seperti yang ditunjukkan oleh boxplot pada bagian [*Outliers*](#Outliers), akan dihapus dari dataset dengan menggunakan metode IQR. Dalam metode ini, *outliers* diidentifikasi sebagai nilai pada 1.5 QR di atas Q3 atau 1.5 QR di bawah Q1.

```
Batas bawah = Q1 - 1.5 * IQR
Batas atas = Q3 + 1.5 * IQR
```

Dengan batasan tersebut, kita dapat mengidentifikasi nilai-nilai di luar batas sebagai *outliers* dan menghapusnya dari dataset.

### Oversampling

```py
oversampler = RandomOverSampler(random_state=1)
X_resampled, y_resampled = oversampler.fit_resample(X, y)
```

Pada tahap ini, seperti sudah diketahui sebelumnya pada tahap EDA, bahwa dataset kami memiliki ketidakseimbangan distribusi kelas yang berpotensi menghasilkan bias ketika jumlah data pada satu kelas lebih banyak dari yang lainnya. Dengan melakukan *oversampling*, ketidakseimbangan distribusi data akan ditangani dengan ditambahkannya sampel baru secara acak berdasarkan sampel yang sudah ada sebelumnya. Hal ini akan membuat jumlah data untuk setiap kelas seimbang dan tentu akan memperbanyak jumlah keseluruhan sampel data. Tahap ini membantu mencegah terjadinya bias dalam prediksi model.

### Pembagian Uji-Latih

```py
X_train, X_test, y_train, y_test = train_test_split(X_resampled, y_resampled, train_size=.8, random_state=1)
```

Pembagian uji-latih bekerja dengan membagi keseluruhan dataset awal menjadi dua bagian--uji dan latih. Proporsi yang digunakan dapat beragam, namun untuk model kami kali ini menggunakan proporsi 80% untuk data latih dan 20% untuk data uji. Pembagian ini berfungsi untuk mencegah model mempelajari semua data dan mengevaluasi performa model pada data yang tidak terlihat. Hal ini mencegah terjadinya *overfitting* di mana model terlanjur menghafalkan keseluruhan data latih sehingga tidak mampu untuk meprediksi data yang tidak terlihat.

## Modeling

Kami menggunakan tiga model dengan algoritma yang berbeda untuk pelatihan. Ketiga algoritma yang saya gunakan untuk model-model saya adalah *K-Nearest Neighbord*, *RandomForest*, serta *GradientBoosting*. Setiap algoritma atau *estimator* yang kami gunakan dimasukkan ke dalam *pipeline* bersama dengan sebuah *transformer StandarScaler*. Dengan memasukkan *transformer* untuk tahap *preprocessing* dan *estimator* ke dalam sebuah *pipeline*, kami tidak perlu secara manual menstandardisasi setiap data yang akan diproses oleh model. *Pipeline* yang kami rancang akan secara otomatis menstandardisasi data yang akan diproses untuk pelatihan maupun untuk evaluasi dan prediksi.

### 1. K-Nearest Neighbors (Classifier)

```py
knn = Pipeline([
    ('scaler', StandardScaler()),
    ('knn', KNeighborsClassifier(n_neighbors=4, weights='uniform'))
])
```

*K-Nearest Neighbors (KNN)* adalah sebuah algoritma sederhana yang bekerja dengan mengidentifikasi *k* titik data dalam dataset pelatihan yang paling dekat dengan titik yang ingin diprediksi, berdasarkan metrik jarak seperti jarak Euclidean.

Parameter `n_neighbors` menentukan berapa banyak tetangga yang akan dipertimbangkan untuk membuat prediksi. Sedangkan, parameter `weights='uniform'` menentukan bahwa semua tetangga yang dipilih memiliki bobot yang sama.

- **Kelebihan**: Mudah diimplementasikan dan tidak memerlukan fase pelatihan model secara eksplisit, sehingga efektif untuk dataset kecil.
- **Kekurangan**: Dapat memakan banyak sumber daya untuk dataset yang besar dan sensitif terhadap data yang tidak relevan.

### 2. Random Forest (Classifier)

```py
random_forest = Pipeline([
    ('scaler', StandardScaler()),
    ('random_forest', RandomForestClassifier(n_estimators=50, max_depth=15))
])
```

*Random Forest* adalah sebuah algoritma *ensemble* yang menggabungkan beberapa *decision tree* untuk meningkatkan akurasi prediksi dan menangani *overfitting*.

Parameter `n_estimators` menentukan jumlah *Decision Tree* yang akan dibuat. Sedangkan, parameter `max_depth` menentukan kedalaman maksimum setiap *Decision Tree* dalam *ensemble*.

- **Kelebihan**: Mengurangi *overfitting* dan meningkatkan generalisasi dibandingkan *Decision Tree*; dapat menangani nilai yang hilang dengan baik dan efektif dalam menangani hubungan non-linear dalam data.
- **Kekurangan**: Interpretabilitasnya menurun seiring bertambahnya jumlah pohon, dan proses pelatihan serta prediksi bisa lebih lambat untuk dataset yang sangat besar.

### 3. Gradient Boosting (Classifier)

```py
gradient_boosting = Pipeline([
    ('scaler', StandardScaler()),
    ('gradient_boosting', GradientBoostingClassifier(learning_rate=.1, max_depth=3, n_estimators=100))
])
```

*Gradient Boosting* adalah sebuah algoritma yang membangun model secara berurutan, di mana setiap model baru berfokus pada kesalahan residu (perbedaan antara nilai prediksi dan aktual) dari model sebelumnya.

Parameter `learning_rate` menentukan besaran kontribusi untuk setiap "pohon" terhadap prediksi akhir. Parameter `mas_depth` menentukan kedalaman maksimum setiap *Decision Tree* dalam *ensemble*. Sedangkan, parameter `n_estimators` menentukan berapa banyak *Decision Tree* yang akan dibangun secara berurutan dalam *ensemble*.

- **Kelebihan**: Mengurangi bias dan variasi, cocok untuk data yang kompleks
- **Kekurangan**: Rentan terhadap *overfitting*; Membutuhkan sumber daya yang banyak; lebih lambat dibandingkan Random Forest

---

Berdasarkan hasil evaluasi sederhana, diperoleh nilai akurasi sebagai berikut untuk setiap model:
- KNN:
  - Akurasi *Training*: ~95%
  - Akurasi *Testing*: ~93%
- Random Forest:
  - Akurasi *Training*: ~99%
  - Akurasi *Testing*L ~97%
- Gradient Boosting:
  - Akurasi *Training*: ~94%
  - Akurasi *Testing*: ~92%
Berdasarkan perolehan nilai akurasi ini, model Random Forest menunjukkan hasil yang lebih unggul dibandingkan kedua model lainnya yang dibuktikan dengan nilai akurasi pelatihan dan pengujian yang relatif lebih tinggi dibandingkan dengan kedua model lainnya. Oleh karena itu, model Random Forest dipilih sebagai model terbaik diantara ketiga model tersebut.

## Evaluation

Untuk evaluasi akhir, kami menggunakan beberapa metriks, yaitu:
- Akurasi: Perbandingan nilai prediksi yang benar dari keseluruhan prediksi.
  Rumus:
  - `Jumlah prediksi benar` / `Jumlah prediksi total`; atau,
  - (TP + TN) / (TP + FP + TN + FN)
- Presisi: Perbandingan nilai *true positive*--prediksi yang benar dari kategori positif--dari keseluruhan prediksi positif.
  Rumus:
  - TP / (TP + FP)
- *Recall*: Perbandingan nilai *true positive* dari keseluruhan jumlah positif yang ada.
  Rumus:
  - TP / (TP + FN)
- *F1 Score*: Gabungan dari nilai presisi dan *recall*.
  Rumus:
  - 2 * (`Presisi` * `Recall`) / (`Presisi` + `Recall`)
- *Confusion Matrix*: Diagram yang membandingkan jumlah prediksi dengan jumlah data yang ada untuk setiap kategori; jumlah prediksi yang benar dan salah untuk setiap kategori.

Note untuk rumus:
  TP = True Positive
  FP = False Positive
  TN = True Negative
  FN = False Negative

![image](https://github.com/user-attachments/assets/5381de82-e099-46a4-8ca1-e3c97b17274d)
![image](https://github.com/user-attachments/assets/e23d8cc1-5596-46d3-8518-f64b898b698b)

Kedua gambar di atas menunjukkan bahwa hasil evaluasi untuk model adalah sangat baik dengan rata-rata nilai untuk setiap metriknya di atas 97%. Diagram *confusion matrix* juga menunjukkan bahwa hanya sedikit sekali prediksi model yang salah. Hal ini menunjukkan bahwa performa model sudah cukup optimal.

Selanjutnya, model diuji dengan 4 sampel data kustom untuk diprediksi tingkat kualitas udaranya.
- Data yang pertama menunjukkan konsentrasi zat polutan yang relatif sedikit. Target: Good
- Data yang kedua memiliki sedikit peningkatan pada konsentrasi jumlah polutan secara keseluruhan. Target: Moderate
- Data yang ketiga memiliki peningkatan yang cukup signifikan pada konsentrasi PM10. Target: Poor
- Data yang keempat memiliki peningkatan pada NO2 yang sangat melebihi ambang batas dibandingkan data ke-3. Target: Hazardous

Hasil prediksi:
![image](https://github.com/user-attachments/assets/c0f20b5f-a216-44db-ba99-60690f7f5f73)

Kesimpulan: Sejauh evaluasi, model menunjukkan performa yang baik dari keseluruhan metrik, menunjukkan bahwa model dapat memprediksi dengan akurat. Model juga dapat memprediksi tingkat kualitas udara dari parameter atau kriteria zat polutan di wilayah tertentu.

