# PCD_Assignment01

## Down Sampling dan Up Sampling Citra


## Identitas : 
**Nama:** Muhammad Gauza Faliha  
**NIM:** 25/555851/PA/23315  
**Kelas:** KOM A (Ilmu Komputer)

## Deskripsi

Tugas ini nantinya membahas implementasi dan perbandingan metode *down sampling* serta *up sampling* pada citra digital. Pengolahan dilakukan secara manual menggunakan Python, NumPy, dan Matplotlib untuk memahami cara kerja setiap metode interpolasi dan reduksi resolusi.

Eksperimen/percobaan kali ini , saya menggunakan gambar dari kategori **forest**, **buildings**, dan **sea**. Setiap citra awal berukuran **150 x 150 piksel**. Citra diperkecil dengan faktor 2 menjadi **75 x 75 piksel**, kemudian diperbesar kembali menjadi **150 x 150 piksel**.

## Dataset

Dataset yang digunakan adalah **Intel Image Classification** dari Kaggle:

- Dataset: [Intel Image Classification](https://www.kaggle.com/datasets/puneet6060/intel-image-classification)
- Direktori data yang digunakan: `seg_train/seg_train`
- Kategori yang dianalisis: `forest`, `buildings`, dan `sea`

## Metode yang Digunakan

### Down Sampling

Down sampling mengurangi resolusi dengan merepresentasikan satu blok 2 x 2 piksel menjadi satu piksel.

| Metode | Prinsip kerja | Karakter hasil |
|---|---|---|
| Max Down Sampling | Mengambil nilai terbesar pada setiap blok 2 x 2 untuk tiap kanal RGB | Cenderung mempertahankan area terang dan meningkatkan kontras |
| Average Down Sampling | Menghitung rata-rata nilai empat piksel pada blok 2 x 2 | Hasil lebih halus dan warna lebih representatif |
| Median Down Sampling | Mengurutkan nilai piksel dalam blok lalu mengambil nilai tengah | Lebih tahan terhadap nilai ekstrem atau noise |

### Up Sampling

Up sampling memperbesar kembali citra hasil *Average Down Sampling* dari 75 x 75 menjadi 150 x 150 piksel.

| Metode | Prinsip kerja | Karakter hasil |
|---|---|---|
| Nearest Neighbor | Menyalin nilai piksel terdekat | Sangat cepat, tetapi tampak kotak-kotak (*pixelated*) |
| Bilinear | Menginterpolasi empat piksel tetangga | Lebih halus, namun tepi dapat sedikit blur |
| Bicubic | Menginterpolasi 16 piksel tetangga dengan kernel kubik | Umumnya paling halus dan paling mendekati kualitas visual citra asli |

## Alur Eksperimen

```text
Gambar asli (150 x 150)
        |
        v
Down Sampling faktor 2
        |
        v
Gambar kecil (75 x 75)
        |
        v
Up Sampling: NN / Bilinear / Bicubic
        |
        v
Gambar hasil (150 x 150)
```

## Hasil Analisis

- Down sampling menurunkan jumlah piksel dari **22.500** menjadi **5.625 piksel**, atau pengurangan sebesar **75%**.
- **Max Down Sampling** cenderung menghasilkan citra yang lebih terang pada area tertentu karena memilih nilai piksel terbesar.
- **Average Down Sampling** memberi hasil paling seimbang dan digunakan sebagai input tahap up sampling karena warna serta transisinya lebih stabil.
- **Median Down Sampling** dapat mengurangi pengaruh nilai ekstrem, tetapi implementasi median untuk blok berisi empat nilai idealnya menggunakan rata-rata dua nilai tengah.
- **Nearest Neighbor** adalah metode up sampling tercepat, tetapi menghasilkan blok piksel yang jelas.
- **Bilinear** menghasilkan peralihan warna lebih lembut dibanding nearest neighbor dan menjadi kompromi antara kualitas serta kecepatan.
- **Bicubic** memberi hasil visual terbaik secara umum, terutama untuk garis pada citra gedung dan gradasi warna pada citra laut, dengan konsekuensi waktu proses yang lebih lama.

## Kesimpulan

Kombinasi **Average Down Sampling** dan **Bicubic Up Sampling** memberikan hasil visual terbaik pada tugas ini. Average Down Sampling menjaga warna lokal tetap natural saat resolusi dikurangi, sementara Bicubic Up Sampling menghasilkan pembesaran yang lebih halus dibandingkan Nearest Neighbor dan Bilinear. Namun, up sampling tidak dapat memulihkan detail asli yang sudah hilang ketika proses down sampling dilakukan.

## Cara Menjalankan

1. Buka file notebook `Muhammad_Gauza_Faliha_Tugas_1_PCD_Down_Sampling_Up_Sampling.ipynb` menggunakan Google Colab atau Jupyter Notebook.
2. Pastikan dependensi tersedia:

   ```bash
   pip install kaggle numpy matplotlib
   ```

3. Siapkan autentikasi Kaggle melalui file `kaggle.json` atau *secret/environment variable*.
4. Jalankan sel secara berurutan, mulai dari pengunduhan dataset hingga visualisasi perbandingan hasil.

Disini saya juga lampirkan untuk link collab :


https://colab.research.google.com/github/gauzamf22/tugas1pcd/blob/main/PCD_Assignment01.ipynb

## Library

- Python
- NumPy
- Matplotlib
- Kaggle API

