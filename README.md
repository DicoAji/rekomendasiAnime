## Business Understanding

### Problem Statements

1. Bagaimana sistem memprediksi anime berdasarkan pilihan anime yang dipilih sebelumnya?
2. Bagaimana membuat metode pendekatan content base filtering dalam sistem rekomendasi anime?

### Goals

1. Menampilkan rekomendasi anime berdasarkan anime yang dipilih sebelumnya.
2. Membuat metode pendekatan content base filtering dalam sistem rekomendasi anime.

### Solution statements

Pengerjaan menggunakan algoritma Content Base Filtering. Content Base Filtering adalah pemfilteran berbasis konten di mana sistem ini memberikan rekomendasi untuk menebak apa yang disukai pengguna berdasarkan aktivitas pengguna tersebut. Pemfilteran berbasis konten menggunakan kesamaan dalam produk, layanan, atau fitur konten, serta akumulasi informasi tentang pengguna untuk membuat rekomendasi

## Data Understanding

Dataset: [Anime Recommendations Database](https://www.kaggle.com/datasets/CooperUnion/anime-recommendations-database)
![img](https://i.postimg.cc/sxxDfNzQ/Screenshot-2022-10-16-181622.png)
Data ini berisi informasi tentang data preferensi pengguna dari 73.516 pengguna di 12.294 anime. Setiap pengguna dapat menambahkan anime ke daftar lengkap mereka dan memberikan peringkat dan kumpulan data ini adalah kompilasi dari peringkat tersebut.

## Data Preparation

- Mengatasi masalah data yang kosong pada kolom rating dengan melakukan pengecekan terlebih dahulu lalu menggantinya dengan nilai rata-rata.
- Pada kolom genre dan type terdapat beberapa value yang kosong alhasil saya hapus baris menggunakan dropna().
- Mengubah karakter (,) menjadi karakter (|) pada kolom genre
- Mengurutkan anime berdasarkan anime_id.
- Mengatasi duplicate data dengan menghapus data duplicate dengan drop_duplicates() berdasarkan anime_id.
- Konversi data menjadi list.
- Membuat dictionary untuk menentukan pasangan key-value pada data movie_id, movie_name, dan movie_genre yang telah disiapkan sebelumnya.
- Menggunakan TfidfVectorizer : untuk melakukan pembobotan.
- melakukan preprocessing : untuk menghilangkan permasalahan-permasalahan yang dapat mengganggu hasil daripada proses data
- mapping data : untuk memetakan data

## Modeling and Result

Solusi permasalahan saya memilih pendekatan berikut Content-based Filtering.

content-based recommender systems pada dasarnya dengan cara mencocokkan atribut profil pengguna terhadap atribut dari objek konten, hasil tersebut berdasarkan penilaian relevansi yang mewakili tingkat pengguna minat dalam objek itu.

Kelebihan Content-based Filtering:

- USER INDEPENDENCE
  Tidak tergantung user lain, content based filtering membangun profil dengan cara mengeksploitasi berdasarkan penilaian yang disediakan oleh pengguna aktif.
- TRANSPARENCY
  Terdapat perincian cara kerja system rekomendasi dalam memunculkan item yang relevan berdasarkan fitur konten.
- NEW ITEM
  Mampu merekomendasikan item belum dinilai oleh setiap pengguna.

Kekurangan Content-based Filtering:

- LIMITED CONTENT ANALYSIS
  Memiliki keterbatasan dalam jumlah, jenis fitur yang terkait, apakah secara otomatis atau manual, begitupula dengan item-item yang disarankan.
- OVER-SPECIALIZATION
  Content based filtering tidak memiliki metode yang melekat untuk menemukan sesuatu yang tidak terduga. Sistem hanya akan menunjukkan item yang nilainya tinggi untuk dicocokkan dengan profil pengguna, maka pengguna akan selalu menemukan item serupa dengan yang sudah direkomendasikan sebelumnya.
  Kelemahan ini juga disebut masalah item yang dihasilkan secara kebetulan (serendipity), kecenderungan untuk menghasilkan rekomendasi dengan tingkat yang terbatas dalam menghasilkan kebaruan.
- NEW USER
  Sistem akan tidak dapat memberikan rekomendasi yang dapat diandalkan pada pengguna baru, karena membutuhkan penelusuran terlebih dahulu pada preferensi pengguna.

#### TF-IDF

TF-IDF atau Term Frequency - Inverse Document Frequency, Bahasa adalah ukuran statistik yang menggambarkan pentingnya istilah dalam dokumen dalam kumpulan atau korpus. Metrik ini biasanya digunakan sebagai faktor pembobotan untuk pencarian informasi, penambangan teks, dan pemodelan pengguna. Nilai TF-IDF meningkat secara linier dengan jumlah kemunculan suatu term dan bergantung pada jumlah dokumen dalam korpus yang memuat term tersebut.TF-IDF digunakan pada sistem rekomendasi anime untuk menentukan representasi fitur penting dari setiap genre anime.

Mendapatkan rekomendasi anime yang mirip dengan Gintama.

|     | **id** | **anime_name** | **genre**                                                  |
| --- | ------ | -------------- | ---------------------------------------------------------- |
| 833 | 918    | Gintama        | Action, Comedy, Histical, Parody, Samurai, Sci-Fi, Shounen |

Dari hasil di atas dapat dilihat bahwa pengguna menyukai anime yang berjudul Gintama yang bergenre Action, Comedy, Histical, Parody, Samurai, Sci-Fi, Shounen.

Hasil top 5 rekomendasi berdasarkan algoritma conten based filtering adalah sebagai berikut :  
| | **anime_name** | **genre** |
| - | --------------------------------------------- | -------------------------------------------------------------------------------- |
| 0 | Gintama (2017) | Action, Comedy, Histical, Parody, Samurai, Sci-Fi, Shounen |
| 1 | Gintama: Yorinuki Gintama-san on Theater 2D | Action, Comedy, Histical, Parody, Samurai, Sci-Fi, Shounen |
| 2 | Gintama° | Action, Comedy, Histical, Parody, Samurai, Sci-Fi, Shounen |
| 3 | Gintama: Shinyaku Benizakura-hen | Action, Comedy, Histical, Parody, Samurai, Sci-Fi, Shounen |
| 4 | Gintama Movie: Shinyaku Benizakura-hen | Action, Comedy, Histical, Parody, Samurai, Sci-Fi, Shounen |

Anime yang bergenre antar Action, Comedy, Histical, Parody, Samurai, Sci-Fi, Shounen menjadi yang direkomendasikan oleh sistem. Hal ini didasarkan pada kesukaan penonton atau pengguna pada masa lalu.

## Evaluation

Hasil Evaluasi untuk Content Based Filtering
Teknik Evaluasi di atas adalah dengan menggunakan precission. Presisi di k adalah proporsi item yang direkomendasikan dalam set top-k yang relevan. Misalkan presisi saya pada 10 dalam masalah rekomendasi 10 teratas adalah 80%. Ini berarti bahwa 80% dari rekomendasi yang saya buat relevan dengan pengguna.
Rumus dari teknik ini adalah :
$${Precision@k} =  {of recommended items @k that are relevant \over of recommended items @k}$$

## References:

[1] Jena, A., Jaiswal, A., Lal, D., Rao, S., Ayubi, A., & Sachdeva, N. (2022). Recommendation System For Anime Using Machine Learning Algorithms. Available at SSRN 4121831.
