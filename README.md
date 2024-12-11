# Laporan Proyek Machine Learning - Raihan Khairul Rochman
# Deteksi Kualitas Udara Berdasarkan Parameter Zat Polutan

## Domain Proyek

Kualitas udara merupakan salah satu indikator utama dalam menilai tingkat kesehatan lingkungan dan dampaknya terhadap kesehatan manusia. Polusi udara yang dihasilkan dari aktivitas industri, transportasi, dan pembakaran bahan bakar fosil telah menjadi perhatian global karena berkontribusi pada berbagai penyakit pernapasan, kardiovaskular, hingga kematian dini.

Dalam projek ini, kami memanfaatkan data historis dari dataset *Air Quality and Pollutant Measurement* yang dipublikasikan di Kaggle. Dataset ini berfokus pada kualitas udara di berbagai daerah. Dataset ini mengandung tepat 5000 sampel atau baris yang mencakup faktor kritis lingkungan dan demografi yang berpengaruh terhadap tingkat polusi udara.

Dengan menggunakan pendekatan analisis prediktif, model *machine learning* dilatih untuk memahami pola dan tren yang ada pada dataset dan menghasilkan prediksi yang akurat untuk mengklasifikasikan tingkat kualitas udara di daerah tertentu. Analisis prediktif ini tidak hanya dapat membantu memantau kualitas udara secara efisien, tetapi juga memberikan peringatan dini bagi masyarakat dan pembuat kebijakan untuk mengambil tindakan preventif. 
  
<sup>1</sup>[Kurniawan, Agusta. "Pengukuran parameter kualitas udara (CO, NO2, SO2, O3 dan PM10) di Bukit Kototabang berbasis ISPU." Jurnal Teknosains 7.1 (2018): 1-13.](https://journal.ugm.ac.id/teknosains/article/view/34658) 

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
Dataset yang kami gunakan adalah Air Quality and Pollutant Measurement yang dipublikasikan di Kaggle. Data ini berfokus pada pengukuran kualitas udara di berbagai karaktetistik wilayah. Dataset ini mengandung tepat 5000 sampel atau baris dan mencakup faktor kritis lingkungan dan demografi yang berpengaruh terhadap tingkat polusi udara.

Fitur-fitur yang diliput dalam dataset ini mencakup suhu, kelembapan, konsentrasi PM2.5, PM10, NO2, SO2, CO, dan jarak ke daerah industri, serta kepadatan populasi. Variabel target dalam dataset ini merupakan kualitas udara yang dikategorikan ke dalam *good* (baik), *moderate* (sedang), *poor* (buruk), dan *hazardous* (berbahaya)
- [Kaggle-Air Quality and Pollutant Measurement](https://www.kaggle.com/api/v1/datasets/download/mujtabamatin/air-quality-and-pollution-assessment).

### Variabel-variabel pada *Air Quality and Pollutant Measurement dataset* adalah sebagai berikut:
**Fitur**
1. ***Temperature* (°C)**: Suhu rata-rata di wilayah tersebut.
2. ***Humidity* (%)**: Kelembapan relatif yang tercatat di wilayah tersebut.
3. **Konsentrasi PM2.5 (µg/m³)**: Tingkat partikel halus.
4. **Konsentrasi PM10 (µg/m³)**: Tingkat partikel kasar.
5. **Konsentrasi NO2 (ppb)**: Tingkat nitrogen dioksida.
6. **Konsentrasi SO2 (ppb)**: Tingkat sulfur dioksida.
7. **Konsentrasi CO (ppm)**: Tingkat karbon monoksida.
8. ***Proximity_to_Industrial_Areas* (km)**: Jarak ke daerah industri terdekat.
9. ***Population_Density* (jiwa/km²)**: Kepadatan penduduk; Jumlah jiwa per kilometer persegi di wilayah tersebut.
  
**Target**
1. ***Air Quality***: Kualitas udara dalam kategori sebagai berikut:
   1) *Good*: Udara bersih dengan tingkat polutan rendah
   2) *Moderate*: Adanya beberapa polutan namun masih dapat diterima
   3) *Poor*: Polusi tampak yang dapat menyebabkan gangguan kesehatan bagi kelompok sensitif.
   4) *Hazardous*: Udara sangat berpolusi yang dapat menimbulkan gangguan kesehatan serius bagi semua orang.


### Menangani Outliers

<img src="https://github.com/user-attachments/assets/9a6c5be5-ab3e-47ff-bbc6-ab41d27f9a58" width="32%"/>
<img src="https://github.com/user-attachments/assets/5941119e-013d-472e-80c1-f75407e657fc" width="32%"/>
<img src="https://github.com/user-attachments/assets/8ea3b524-4ec2-499e-b17c-6f1884f1fde8" width="32%"/>
<img src="https://github.com/user-attachments/assets/4174c2b2-c89e-443a-b35f-ffb8e80ab7fb" width="32%"/>
<img src="https://github.com/user-attachments/assets/93dba22e-8f59-4c30-8e24-a1857f7693fd" width="32%"/>

Gambar di atas merupakan visualisasi *box plot* untuk mencari *outliers* dalam data. Tampak ada banyak sekali *outliers* (titik-titik kecil) pada setiap kolom. *Outliers* merupakan sampel yang nilainya cukup jauh dari cakupan umum data dan kemunculannya cukup jarang. Dalam tahap ini, *outliers* yang ada akan dihapus untuk mempertahankan pola dan konsistensi pada data.

### Distribusi Data Variabel Fitur

![image](https://github.com/user-attachments/assets/c8809dd7-e2ea-4a83-a8e4-8e99e5b52893)

Berdasarkan gambar di atas, tampak variabel PM2.5, PM10, dan SO2 memiliki distribusi data miring ke kanan. Sedangkan, variabel NO2 memiliki distribusi data cenderung normal. Serta, variabel CO memiliki distribusi data bimodal yang ditunjukkan dengan adanya dua puncak.

### Distribusi Data Variabel Target

![Screenshot_20241211_231241_Chrome](https://github.com/user-attachments/assets/eefd110b-fcbc-4cd6-9e42-2461fc5753b4)

Pada gambar di atas terlihat jelas bahwa jumlah data untuk setiap kelas pada variabel target mengalamai ketidakseimbangan. Hal ini dampat berdampak pada pola yang akan dipelajari oleh model dan berpotensi menghasilkan bias. Oleh karena itu, kami menerapkan *oversampling* pada datazet untuk mempertahankan keseimbangan data.

### Rata-Rata Nilai pada Fitur Numerik

![image](https://github.com/user-attachments/assets/5c855ade-0c99-483e-8be4-a1dbc1fd755b)
![image](https://github.com/user-attachments/assets/d355680d-25e7-480c-ae70-f07a07267ed5)
![image](https://github.com/user-attachments/assets/1ba9310b-ca15-4c85-a0a6-c065f0238dde)
![image](https://github.com/user-attachments/assets/9f8ed4ad-2060-458f-bf3f-8c5c16a28d9d)
![image](https://github.com/user-attachments/assets/c81baa3a-b7a5-4316-b592-ded818748c9f)

Pada kelima gambar di atas dapat disimpulkan sebuah pola bahwa setiap faktor atau fitur cenderung memiliki nilai yang rendah untuk kategori *Good* berdasarkan nilai rata-ratanya pada fitur tersebut, diikuti oleh kategori *Moderate*, *Poor*, lalu *Hazardous*, yang secara bertahap memiliki rata-rata nilai yang semakin besar pada setiap fitur.

## Data Preparation

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

*K-Nearest Neighbors (KNN)* adalah sebuah algoritma sederhana dan intuitif yang dapat digunakan untuk regresi dan klasifikasi. Algoritma ini bekerja dengan mengidentifikasi *k* titik data dalam dataset pelatihan yang paling dekat dengan titik yang ingin diprediksi, berdasarkan metrik jarak seperti jarak Euclidean. Algoritma ini menetapkan kelas yang paling umum di ajtara tetangganya.

### 2. Random Forest (Classifier)

```py
random_forest = Pipeline([
    ('scaler', StandardScaler()),
    ('random_forest', RandomForestClassifier(n_estimators=50, max_depth=15))
])
```

### 3. Gradient Boosting (Classifier)

```py
gradient_boosting = Pipeline([
    ('scaler', StandardScaler()),
    ('gradient_boosting', GradientBoostingClassifier(learning_rate=.1, max_depth=3, n_estimators=100))
])
```

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan kelebihan dan kekurangan dari setiap algoritma yang digunakan.
- Jika menggunakan satu algoritma pada solution statement, lakukan proses improvement terhadap model dengan hyperparameter tuning. **Jelaskan proses improvement yang dilakukan**.
- Jika menggunakan dua atau lebih algoritma pada solution statement, maka pilih model terbaik sebagai solusi. **Jelaskan mengapa memilih model tersebut sebagai model terbaik**.

## Evaluation

Pada bagian ini anda perlu menyebutkan metrik evaluasi yang digunakan. Lalu anda perlu menjelaskan hasil proyek berdasarkan metrik evaluasi yang digunakan.

Sebagai contoh, Anda memiih kasus klasifikasi dan menggunakan metrik **akurasi, precision, recall, dan F1 score**. Jelaskan mengenai beberapa hal berikut:
- Penjelasan mengenai metrik yang digunakan
- Menjelaskan hasil proyek berdasarkan metrik evaluasi

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.
