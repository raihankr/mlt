# Laporan Proyek Machine Learning - Raihan Khairul Rochman
# Deteksi Kualitas Udara

## Domain Proyek

Kualitas udara merupakan salah satu indikator utama dalam menilai tingkat kesehatan lingkungan dan dampaknya terhadap kesehatan manusia. Polusi udara yang dihasilkan dari aktivitas industri, transportasi, dan pembakaran bahan bakar fosil telah menjadi perhatian global karena berkontribusi pada berbagai penyakit pernapasan, kardiovaskular, hingga kematian dini.

Dalam projek ini, kami memanfaatkan data historis dari dataset *Air Quality and Pollutant Measurement* yang dipublikasikan di Kaggle. Dataset ini berfokus pada kualitas udara di berbagai daerah. Dataset ini mengandung tepat 5000 sampel atau baris yang mencakup faktor kritis lingkungan dan demografi yang berpengaruh terhadap tingkat polusi udara.

Dengan menggunakan pendekatan analisis prediktif, model *machine learning* dilatih untuk memahami pola dan tren yang ada pada dataset dan menghasilkan prediksi yang akurat untuk mengklasifikasikan tingkat kualitas udara di daerah tertentu. Analisis prediktif ini tidak hanya dapat membantu memantau kualitas udara secara efisien, tetapi juga memberikan peringatan dini bagi masyarakat dan pembuat kebijakan untuk mengambil tindakan preventif. 

**Rubrik/Kriteria Tambahan (Opsional)**:
- Menyertakan hasil riset terkait atau referensi. Referensi yang diberikan harus berasal dari sumber yang kredibel dan author yang jelas.
  
  Format Referensi: [Judul Referensi](https://scholar.google.com/) 

## Business Understanding

Kualitas udara yang buruk berdampak signifikan pada kesehatan manusia dan lingkungan. Oleh karena itu, pemerintah, industri, dan masyarakat membutuhkan cara yang efisien untuk memantau, menganalisis, dan memprediksi kualitas udara guna mengambil langkah mitigasi yang tepat.

### Problem Statements

Menjelaskan pernyataan masalah latar belakang:
- Bagaimana hubungan antara masing-masing parameter terhadap tingkat kualitas udara?
- Bagaimana tingkat kualitas udara di daerah dengan karakteristik tertentu?

### Goals

Menjelaskan tujuan dari pernyataan masalah:
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
<img src="https://github.com/user-attachments/assets/d38d7710-51d8-42dc-a4e4-5675186e845e" width="32%"/>
<img src="https://github.com/user-attachments/assets/93dba22e-8f59-4c30-8e24-a1857f7693fd" width="32%"/>
<img src="https://github.com/user-attachments/assets/4174c2b2-c89e-443a-b35f-ffb8e80ab7fb" width="32%"/>
<img src="https://github.com/user-attachments/assets/8ea3b524-4ec2-499e-b17c-6f1884f1fde8" width="32%"/>
<img src="https://github.com/user-attachments/assets/5941119e-013d-472e-80c1-f75407e657fc" width="32%"/>
<img src="https://github.com/user-attachments/assets/9a6c5be5-ab3e-47ff-bbc6-ab41d27f9a58" width="32%"/>
<img src="https://github.com/user-attachments/assets/cdbb6b05-1704-425d-b777-6f469fcf316d" width="32%"/>
<img src="https://github.com/user-attachments/assets/314140e1-1b19-41c7-ba13-5437f47f9eea" width="32%"/>
<img src="https://github.com/user-attachments/assets/8f2ac10e-4bf1-4ca1-b423-9bdcafb06a9b" width="32%"/>

Gambar di atas merupakan visualisasi *box plot* untuk mencari *outliers* dalam data. Tampak ada banyak sekali *outliers* (titik-titik kecil) pada setiap kolom. *Outliers* merupakan sampel yang nilainya cukup jauh dari cakupan umum data dan kemunculannya cukup jarang. Dalam tahap ini, *outliers* yang ada akan dihapus untuk mempertahankan pola dan konsistensi pada data.

### 

## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

## Modeling
Tahapan ini membahas mengenai model machine learning yang digunakan untuk menyelesaikan permasalahan. Anda perlu menjelaskan tahapan dan parameter yang digunakan pada proses pemodelan.

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
