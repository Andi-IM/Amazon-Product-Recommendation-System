# Laporan Proyek Machine Learning - Andi Irham

## Project Overview

Dewasa ini kemajuan teknologi mengalami perkembangan yang sangat peseat, selain itu di dunia bisnis teknologi mempunyai peranan yang sangat penting. Melalui media internet/website baik pelaku bisnis maupun konsumen dapat melakukan transaksi dengan cara *online* kapanpun dan di mana pun dengan orang-orang di seluruh duniap[^1]. Salah satu bentuk teknologi yang dapat dirasakan manfaatnya oleh banyak orang adalah dengan toko online yang dapat dijangkau dari semua kalangan. Meskipun  banyak muncul toko online baru, teteapi tidak banyak toko online yang mampu bertahan lama, karena persaingan yang sangat ketat. Banyaknya kesalahan dalam pemasaran produk oleh pemilik usaha sehingga mengeluarkan banyak biaya terhadap produk yang belum tentu diminati konsumen[^2]. Sistem rekomendasi dapat menjangkau pengguna yang memang membutuhkan produk dari pemilik usaha dengan mengetahui pola belanja konsumen, seperti preferensi masa lalu, riwayat pembelian dan informasi demografis[^3],[^4].

Dalam hal pengembangan model sistem rekomendasi, ada banyak faktor yang bisa menjadi bahan pertimbangan[^5]. Pada sistem rekomendasi produk , faktor-faktor yang dapat menjadi bahan pertimbangan antara lain seperti kategori, rating pengguna, dan review pengguna. Pada proyek ini hanya beberapa model saja yang akan digunakan seperti Model Cosine Similaryty dan K-Nearest Neighbor.


## *Business Understanding*

## *Data Understanding*

## *Data Preparation*

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


## *Modeling*

## *Evaluation*

## Kesimpulan

## *References*

[^1]: Henry Februariyanti *"Implementasi Metode Collaborative Filtering untuk Sistem Rekomendasi Penjualan pada Toko Mebel"* 2021, 43-50, doi: [tautan](https://doi.org/10.31294/jki.v9i1.9859.g4873)

[^2]: Esha Alma'arif, dkk. *"Implementasi Algoritma Apriori Untuk Rekomendasi Produk Pada Toko Online"*, Citec Journal, 2020

[^3]: Munawar dkk "Sistem Rekomendasi Hibrid Menggunakan Algoritma Apriori Mining Asosiasi", TEMATIK -Jurnal Teknologi Informasi Dan Komunikasi, 8(1), 69–80. 2021, doi: [tautan](https://doi.org/10.38204/tematik.v8i1.567)

[^4]: Munawar dkk/ *"Meningkatkan Rekomendasi Menggunakan Algoritma Perbedaan Topik"* . J-SIKA| Jurnal Sistem Informasi Karya Anak Bangsa, 02(02), 17–26. Diambil dari [tautan](https://ejournal.unibba.ac.id/index.php/j-sika/article/view/378).

[^5]: Mohamed, Marwa & Khafagy, Mohamed & Ibrahim, Mohamed. (2019). Recommender Systems Challenges and Solutions Survey. 10.1109/ITCE.2019.8646645.

