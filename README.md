# Chayote Freshness Clustering Using K-Means

Mengelompokkan (clustering) citra buah labu siam (chayote) berdasarkan fitur warna (RGB, HSV) dan tekstur (Local Binary Pattern) menggunakan K-Means, sebagai eksplorasi awal untuk melihat apakah karakteristik visual buah dapat membentuk kelompok yang berbeda.

> Project ini dikerjakan sebagai tugas mata kuliah Data Mining Lanjut pada semester 7, dikerjakan secara berkelompok.

## Latar Belakang

Kesegaran buah labu siam dapat memengaruhi kualitas dan daya jualnya. Secara visual, buah yang lebih segar dan yang mulai layu/rusak seringkali memiliki perbedaan warna dan tekstur permukaan yang dapat diekstraksi dari citra.

## Rumusan Masalah

- Apakah fitur warna (RGB, HSV) dan tekstur (LBP) yang diekstraksi dari citra buah labu siam dapat membentuk kelompok (cluster) yang berbeda secara visual?
- Berapa jumlah cluster yang paling optimal untuk mengelompokkan data ini?

## Tujuan Project

1. Mengekstraksi fitur warna dan tekstur dari kumpulan citra buah labu siam.
2. Melakukan clustering menggunakan K-Means untuk mengelompokkan citra berdasarkan fitur tersebut.
3. Mengevaluasi kualitas hasil clustering menggunakan Silhouette Score dan Davies-Bouldin Index.

## Catatan Penting Mengenai Pendekatan

Dataset citra pada project ini belum memiliki label ground-truth kesegaran (misalnya kategori "Segar" vs "Tidak Segar" yang ditentukan manual/pakar). Karena itu, pendekatan yang digunakan adalah **clustering (unsupervised)**, bukan klasifikasi (supervised). Hasil cluster yang terbentuk merepresentasikan pengelompokan berdasarkan kemiripan fitur visual, dan belum tentu berkorespondensi langsung dengan tingkat kesegaran sebenarnya tanpa verifikasi manual lebih lanjut.

## Dataset

Dataset terdiri dari **2069 foto buah labu siam**, gabungan dari 4 anggota kelompok (masing-masing memotret dengan kamera/HP sendiri), yang kemudian digabungkan menjadi satu folder sebelum diproses.

## Metodologi

1. Menghubungkan ke Google Drive - dataset gabungan disimpan di Google Drive
2. Konversi Format Citra - mengonversi foto HEIC ke JPEG agar dapat diproses dengan OpenCV
3. Ekstraksi Fitur Citra - resize, segmentasi buah dari background (thresholding HSV), ekstraksi fitur warna (RGB, HSV) dan tekstur (Local Binary Pattern)
4. Data Understanding - statistik deskriptif fitur yang diekstraksi
5. Preprocessing - standarisasi fitur (StandardScaler)
6. Menentukan Jumlah Cluster Optimal - pengujian beberapa nilai k menggunakan Silhouette Score
7. Clustering dengan K-Means - menggunakan seluruh fitur warna dan tekstur
8. Eksperimen Pembanding - clustering tanpa fitur mean_r dan mean_b, untuk melihat apakah fitur HSV saja sudah cukup
9. Evaluasi - perbandingan Silhouette Score dan Davies-Bouldin Index antar eksperimen
10. Kesimpulan dan Keterbatasan

## Hasil Utama

| Eksperimen | Silhouette Score | Davies-Bouldin Index |
|---|---|---|
| Seluruh Fitur | 0.3886 | 1.1219 |
| Tanpa mean_r & mean_b | 0.3921 | 1.2104 |

Jumlah cluster optimal: **k=2** (dipilih berdasarkan Silhouette Score tertinggi dari pengujian k=2 hingga k=6).

## Keterbatasan

- Belum ada label ground-truth kesegaran, sehingga cluster yang terbentuk adalah pengelompokan berdasarkan kemiripan visual, bukan validasi langsung terhadap tingkat kesegaran.
- Karena foto berasal dari 4 kamera/HP berbeda, ada kemungkinan variasi pencahayaan dan white balance antar sumber foto turut memengaruhi fitur warna yang diekstraksi, bukan semata-mata karena perbedaan tingkat kesegaran buah.

## Tech Stack

- Python
- OpenCV (cv2) - pemrosesan citra dan segmentasi
- scikit-image - ekstraksi fitur tekstur (Local Binary Pattern)
- Pillow, pyheif - konversi format citra HEIC ke JPEG
- Pandas, NumPy - manipulasi data
- Matplotlib - visualisasi
- Scikit-learn - StandardScaler, K-Means, PCA, Silhouette Score, Davies-Bouldin Index

## Project Structure

```
Chayote_Freshness_Clustering.ipynb   - Notebook analisis lengkap
```

Catatan: dataset citra (2069 foto) disimpan di Google Drive karena ukurannya tidak praktis untuk disertakan langsung di repository.

## Cara Menjalankan

Notebook ini dirancang untuk dijalankan di Google Colab karena menggunakan `google.colab.drive` untuk mengakses dataset citra di Google Drive.

1. Buka notebook di Google Colab
2. Siapkan folder dataset di Google Drive dengan struktur folder per anggota kelompok
3. Jalankan seluruh cell secara berurutan dari atas ke bawah

## Pengembangan Selanjutnya

- Mengumpulkan label kesegaran (misalnya dari penilaian visual manual/pakar atau berdasarkan waktu penyimpanan buah) untuk setiap citra, agar project ini dapat dikembangkan menjadi model klasifikasi supervised (KNN, Random Forest, dll.) yang benar-benar memprediksi tingkat kesegaran.
- Melakukan standarisasi kondisi pengambilan foto (pencahayaan, jarak, latar belakang) di pengumpulan data berikutnya, agar variasi antar sumber foto tidak memengaruhi hasil ekstraksi fitur warna.
- Mengeksplorasi fitur tambahan (misalnya tekstur GLCM atau deep feature dari CNN pretrained) untuk menangkap karakteristik visual yang lebih kaya.

## Tim

Project ini dikerjakan secara berkelompok:

| Nama |
|---|
| Mochammad Irsyad Kurniawan |
| Muhammad Ilza Batistuta |
| **Muhammad Danu Setiawan** |

> Catatan: sesuaikan daftar anggota di atas jika komposisi kelompok untuk project ini berbeda.

## Lisensi

Project ini bersifat open source dan tersedia untuk keperluan pembelajaran.
