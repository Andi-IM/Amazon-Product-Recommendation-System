# Laporan Proyek Machine Learning - Andi Irham

## Project Overview

Dewasa ini kemajuan teknologi mengalami perkembangan yang sangat peseat, selain itu di dunia bisnis teknologi mempunyai peranan yang sangat penting. Melalui media internet/website baik pelaku bisnis maupun konsumen dapat melakukan transaksi dengan cara *online* kapanpun dan di mana pun dengan orang-orang di seluruh duniap[^1]. Salah satu bentuk teknologi yang dapat dirasakan manfaatnya oleh banyak orang adalah dengan toko online yang dapat dijangkau dari semua kalangan. Meskipun  banyak muncul toko online baru, teteapi tidak banyak toko online yang mampu bertahan lama, karena persaingan yang sangat ketat. Banyaknya kesalahan dalam pemasaran produk oleh pemilik usaha sehingga mengeluarkan banyak biaya terhadap produk yang belum tentu diminati konsumen[^2]. Sistem rekomendasi dapat menjangkau pengguna yang memang membutuhkan produk dari pemilik usaha dengan mengetahui pola belanja konsumen, seperti preferensi masa lalu, riwayat pembelian dan informasi demografis[^3],[^4]. Dengan adanya sistem rekomendasi membuat produk yang ditawarkan pemilik akan dengan lebih mudah dijangkau oleh sasaran pengguna sehingga baik itu pemilik usaha dan konsumen diuntungkan.  

Dalam hal pengembangan model sistem rekomendasi, ada banyak faktor yang bisa menjadi bahan pertimbangan[^5]. Pada sistem rekomendasi produk , faktor-faktor yang dapat menjadi bahan pertimbangan antara lain seperti kategori, rating pengguna, dan review pengguna. Pada proyek ini hanya beberapa model saja yang akan digunakan seperti Model Cosine Similarity dan K-Nearest Neighbor.


## *Business Understanding*

Pengembangan model Sistem Rekomendasi Produk memeiliki potensi atau manfaat yang menjadi salah satu alat bantu dalam pengambilan keputusan oleh pengguna aplikasi e-commerce. Contoh potensi manfaat dari Sistem Rekomendasi Produk ini adalah membantu pengguna mendapatkan produk yang dibutuhkan tanpa tenaga ekstra.

### Problem Statements

Berdasarkan dari kondisi yang telah diuraikan sebelumnya, maka diperlukan sistem yang dapat memberikan rekomendasi terhadap pengguna dengan menjawab permasalahan berikut:

- Berapa rata-rata rating untuk setiap kategori produk?
- Produk apa yang memiliki jumlah rating terbanyak di setiap kategori?
- Bagaimana hubungan distribusi antara harga diskon dengan harganya aslinya?
- Bagaimana perubahan rata-rata diskon di setiap kategori?
- Produk apa yang paling populer?
- Apa keyword produk yang paling populer?
- Apa produk yang memiliki review paling populer?
- Apa kolerasi antara diskon produk dengan rating?
- 5 Kategori apa saja yang paling teratas dengan rating tertinggi?
- Bagaimana mengolah *dataset* agar model sistem rekomendasi dapat berjalan dengan baik?
- Bagaimana membuat model sistem rekomendasi cosine similarity dan K-Nearest Neighbor?
- Bagaimana mengukur performa model sistem rekomendasi yang telah dibangun? 

### Goals
Berdasarkan *problem statement* di atas maka tujuan dari pengembangan sistem rekomendasi adalah sebagai berikut:

- Mengetahui rata-rata rating untuk setiap kategori produk.
- Mengetahui produk yang memiliki jumlah rating terbanyak di setiap kategori.
- Mengetahui hubungan distribusi antara harga diskon dengan harga aslinya.
- Mengetahui perubahan rata-rata diskon di setiap kategori.

### Solution Approach

Dari *Problem Statement* dan *Goals* yang telah dideskripsikan, maka didapatkan solusi sebagai berikut:

- Mengekplorasi fitur yang terdapat pada dataset dengan menggunakan teknik analisis univariat dan multivariat. Analisis univariat digunakan untuk melihat hubungan data. Analisis multivariat untuk melihat hubungan antar fitur. Analisis univariat dan multivariat dapat dengan mudah dipaahami melalui visualisasi.
- Mempersiapkan data yang akan digunakan meliputi *Data Ingesting*, *Data Cleaning*, dan *Data Formating*.
- Mengekplorasi model rekomendasi sesuai dengan *behavior* rekomendasi yang diinginkan, dalam kasus ini menggunakan metode Content Based Filtering dan Colaborative Filtering.
- Mengevaluasi model yang telah dikembangkan dengan metrik evaluasi model.

## *Data Understanding*

Dataset yang digunakan dalam analisis kali ini adalah [Amazon Sales Dataset](https://www.kaggle.com/datasets/karkavelrajaj/amazon-sales-dataset/data) yang merupakan  1000 data penjualan produk Amazon beserta Rating dan Review yang diberikan pengguna yang terdokumentasi melalui platform [kaggle](https://www.kaggle.com/).

Detail dari dataset ini adalah sebagai berikut:

- Dataset terdiri dari 1464 *records* dengan 16 fitur.
- Dataset terdiri dari 11 data kategori dan 5 data numerik.
- Data kurang bersih karena ada data yagn seharusnya bertipe data numerik tetapi ditetapkan sebagai kategorikal.
- Perlu untuk proses pembersihan data.

### Dataset memiliki fitur-fitur sebagai berikut:

- `product_id` - ID produk
- `product_name` - Nama produk
- `category` - Kategori produk
- `discounted_price` - Harga produk setelah diskon.
- `actual_price` - Harga produk sebelum diskon.
- `discount_percentage` - Besaran diskon dalam persen
- `rating` - Rating produk
- `rating_count` - Jumlah rating yang diberikan kepada produk
- `about_product` - Deskripsi tentang produk
- `user_id` - ID user yang memberikan review terhadap produk.
- `user_name` - Nama user yang telah memberikan rating terhadap produk
- `review_id` - ID review user
- `review_title` Review singkat
- `review_content` - Review panjang
- `img_link` - Link gambar produk
- `product_linki` - Link resmi produk.

### *Explanatory Data Analysis* (EDA)

Untuk dapat memahami data lebih jelas, maka dilakukan analisis data melalui metode statistik yang disebut sebagai Analisis Data Eksplanatori (Explanatory Data Analysis) atau disingkat EDA[^6]. 


## *Data Preparation*

*Data preparation* atau *data preprocessing* adalah teknik digunakan untuk mengubah data mendah ke dalam format yang berguna dan efisien[^7]. Fungsi utama dari *data preparation* adalah untuk memastikan bahwa data mentah yang akan diproses sudah akurat yang berimplikasi pada hasil analitik yang valid. Proses *data preparation* dilakukan empat tahap persiapan data, yaitu Data Ingestion, Data Cleaning, dan Data Formating. Pada tahap *Data Ingestion*, berikut beberapa pengecekan yang dilakukan:

- Mengimpor data dari format csv ke bentuk DataFrame dengan library Pandas.
- Membaca informasi data.
- Mencari duplikasi data.
- Mencari *missing value* atau nilai yang hilang.

Pada tahap *Data Cleaning*, ada beberapa metode yang digunakan yaitu:

- Membuang data yang memiliki nilai-nilai yang hilang (*Dropping*)
- Mengisi niali-nilai yang hilang (*Imputation*)
- Interpolasi menghasilkan titik-titik data baru dalam janngkauan suatu data.



## *Modeling*

## *Evaluation*

## Kesimpulan

## *References*

[^1]: Henry Februariyanti *"Implementasi Metode Collaborative Filtering untuk Sistem Rekomendasi Penjualan pada Toko Mebel"* 2021, 43-50, doi: [tautan](https://doi.org/10.31294/jki.v9i1.9859.g4873)

[^2]: Esha Alma'arif, dkk. *"Implementasi Algoritma Apriori Untuk Rekomendasi Produk Pada Toko Online"*, Citec Journal, 2020

[^3]: Munawar dkk "Sistem Rekomendasi Hibrid Menggunakan Algoritma Apriori Mining Asosiasi", TEMATIK -Jurnal Teknologi Informasi Dan Komunikasi, 8(1), 69–80. 2021, doi: [tautan](https://doi.org/10.38204/tematik.v8i1.567)

[^4]: Munawar dkk/ *"Meningkatkan Rekomendasi Menggunakan Algoritma Perbedaan Topik"* . J-SIKA| Jurnal Sistem Informasi Karya Anak Bangsa, 02(02), 17–26. Diambil dari [tautan](https://ejournal.unibba.ac.id/index.php/j-sika/article/view/378).

[^5]: Mohamed, Marwa & Khafagy, Mohamed & Ibrahim, Mohamed. (2019). Recommender Systems Challenges and Solutions Survey. 10.1109/ITCE.2019.8646645.

[^6]: C. Chatfield, “Exploratory data analysis,” European Journal of Operational Research, vol. 23, no. 1, pp. 5–13, Jan. 1986, doi: https://doi.org/10.1016/0377-2217(86)90209-2.

[^7]: Laraswati. (2022). Tahapan Data Preparation agar Data Lebih Mudah Diproses, diakses pada tanggal 28 Februari 2024, https://blog.algorit.ma/data-preparation/ 



