# Laporan Proyek Machine Learning - Andi Irham

## Project Overview

Dewasa ini kemajuan teknologi mengalami perkembangan yang sangat peseat, selain itu di dunia bisnis teknologi mempunyai peranan yang sangat penting. Melalui media internet/website baik pelaku bisnis maupun konsumen dapat melakukan transaksi dengan cara *online* kapanpun dan di mana pun dengan orang-orang di seluruh duniap[^1]. Salah satu bentuk teknologi yang dapat dirasakan manfaatnya oleh banyak orang adalah dengan toko online yang dapat dijangkau dari semua kalangan. Meskipun  banyak muncul toko online baru, teteapi tidak banyak toko online yang mampu bertahan lama, karena persaingan yang sangat ketat. Banyaknya kesalahan dalam pemasaran produk oleh pemilik usaha sehingga mengeluarkan banyak biaya terhadap produk yang belum tentu diminati konsumen[^2]. Sistem rekomendasi dapat menjangkau pengguna yang memang membutuhkan produk dari pemilik usaha dengan mengetahui pola belanja konsumen, seperti preferensi masa lalu, riwayat pembelian dan informasi demografis[^3],[^4]. Dengan adanya sistem rekomendasi membuat produk yang ditawarkan pemilik akan dengan lebih mudah dijangkau oleh sasaran pengguna sehingga baik itu pemilik usaha dan konsumen diuntungkan.  

Dalam hal pengembangan model sistem rekomendasi, ada banyak faktor yang bisa menjadi bahan pertimbangan[^5]. Pada sistem rekomendasi produk , faktor-faktor yang dapat menjadi bahan pertimbangan antara lain seperti kategori, rating pengguna, dan review pengguna. Proyek ini menggunakan beberapa pendekatan sistem rekomendasi yaitu pendekatan basis konten (*Content-based Approach*) dan Pendekatan Kolaboratif (*Collaborative Approach*) yang selengkapnya akan dijelaskan pada tahap modeling. Tahapan pengembangan sistem rekomendasi mengikuti tahapan dari standar baku CRISP-DM atau *Cross-industry Standard Process for Data Mining*[6] yang dijelaskan pada gambar 1 berikut ini:

<p align="center"><img src="https://github.com/Andi-IM/Amazon-Product-Recommendation-System/assets/21165698/94f45723-78da-4800-a8b7-9359a41f1c2c"></p>
<p align="center">Gambar 1. Alur Proyek Sistem Rekomendsasi</p>

Proses dimulai dari Business Understanding, yaitu tahapan memahami masalah bisnis dan kemudian mrancang solusi analitik berdasarkan data untuk menyelesaikan permasalahan tersebut. Tahapan yang dijelaskan pada tahapan ini meliputi problem statement, goals, dan solution approach. Setelah memahami masalah dan menentukan solusinya, tahapan berlanjut pada Data Understanding dengan melihat infromasi data dan menentukan kualitasnya. Pemahaman data sangat penting untuk menghindari masalah yang tidak terduga pada fase berikutnya, yaitu Data Preparation. Data preparation di proyek ini adalah melakukan cleaning data yang hilang, memeriksa outlier, meng-encode data sehingga dapat diproses model, lalu pada akhirnya membagi data menjadi training dan test sebelum melakukan pemodelan. Pada tahap pemodelan dan evaluasi, dilakukan proses trainng dan melihat ukuran performa dari model untuk menentukan apakah model tersebut baik atau kurang. 

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
- `product_link` - Link resmi produk.

### *Explanatory Data Analysis* (EDA)

Untuk dapat memahami data lebih jelas, maka dilakukan analisis data melalui metode statistik yang disebut sebagai Analisis Data Eksplanatori (Explanatory Data Analysis) atau disingkat EDA[^6]. Berikut ini adalah hasil EDA dengan menggunakan analisis multivariat.

#### Hubungan antara Harga Asli dan Rating

<p align="center"><img src="https://github.com/Andi-IM/Amazon-Product-Recommendation-System/assets/21165698/8ba42a25-1b08-4b38-b88b-3e190176f01f"></p>
<p align="center">Gambar 1. Scattterplot persebaran harga produk dengan diskon yang diberikan</p>

Dari gambar di atas dapat dilihat distribusi harga merapat dari 0 hingga 80000 rupee memiliki rating terbanyak di sekitaran 4.0 hingga 4.5

#### Distribusi harga produk

<p align="center"><img src="https://github.com/Andi-IM/Amazon-Product-Recommendation-System/assets/21165698/1a0bbbc3-f9b3-4097-8e1d-b032edbd3a07"></p>
<p align="center">Gambar 2. Distribusi persebaran harga produk</p>

Dari gambar 2 dapat dilihat bahwa produk yang ditayangkan tergolong produk murah di bawah 20000 rupee.

## Rata-rata rating untuk setiap produk

Tabel 1. Rata-rata rating untuk setiap produk.

|index|category|rating|
|---|---|---|
|0|Car&Motorbike&#124;CarAccessories&#124;InteriorAccessories&#124;AirPurifiers&Ionizers|3\.8|
|1|Computers&Accessories&#124;Accessories&Peripherals&#124;Adapters&#124;USBtoUSBAdapters|4\.15|
|2|Computers&Accessories&#124;Accessories&Peripherals&#124;Audio&VideoAccessories&#124;PCHeadsets|3\.5|
|3|Computers&Accessories&#124;Accessories&Peripherals&#124;Audio&VideoAccessories&#124;PCMicrophones|3\.5999999999999996|
|4|Computers&Accessories&#124;Accessories&Peripherals&#124;Audio&VideoAccessories&#124;PCSpeakers|4\.05|
|5|Computers&Accessories&#124;Accessories&Peripherals&#124;Audio&VideoAccessories&#124;Webcams&VoIPEquipment&#124;Webcams|4\.199999999999999|
|6|Computers&Accessories&#124;Accessories&Peripherals&#124;Cables&Accessories&#124;CableConnectionProtectors|4\.033333333333333|
|7|Computers&Accessories&#124;Accessories&Peripherals&#124;Cables&Accessories&#124;Cables&#124;DVICables|4\.4|
|8|Computers&Accessories&#124;Accessories&Peripherals&#124;Cables&Accessories&#124;Cables&#124;EthernetCables|4\.4|
|9|Computers&Accessories&#124;Accessories&Peripherals&#124;Cables&Accessories&#124;Cables&#124;SATACables|3\.9|

Dari tabel 1 dapat dilihat bahwa sebagian besar produk memiliki rating positif di atas 3.5. Namun juga terdapat beberapa yang memiliki rating rendah dan memungkinkan untuk evaluasi seperti pemberian diskon atau promo tertentu.

#### Produk dengan rating terbanyak tiap kategori

Tabel 2. Produk dengan rating terbanyak tiap kategori.

|index|product\_id|category|rating|rating\_count|
|---|---|---|---|---|
|0|B0912WJ87V|Car&Motorbike&#124;CarAccessories&#124;InteriorAccessories&#124;AirPurifiers&Ionizers|3\.8|1118\.0|
|1|B097C564GC|Computers&Accessories&#124;Accessories&Peripherals&#124;Adapters&#124;USBtoUSBAdapters|4\.3|4426\.0|
|2|B094DQWV9B|Computers&Accessories&#124;Accessories&Peripherals&#124;Adapters&#124;USBtoUSBAdapters|4\.0|1540\.0|
|3|B009LJ2BXA|Computers&Accessories&#124;Accessories&Peripherals&#124;Audio&VideoAccessories&#124;PCHeadsets|3\.5|7222\.0|
|4|B08SCCG9D4|Computers&Accessories&#124;Accessories&Peripherals&#124;Audio&VideoAccessories&#124;PCMicrophones|3\.9|14969\.0|
|5|B08HD7JQHX|Computers&Accessories&#124;Accessories&Peripherals&#124;Audio&VideoAccessories&#124;PCMicrophones|3\.3|2804\.0|
|6|B08K9PX15C|Computers&Accessories&#124;Accessories&Peripherals&#124;Audio&VideoAccessories&#124;PCSpeakers|4\.0|7352\.0|
|7|B08SBH499M|Computers&Accessories&#124;Accessories&Peripherals&#124;Audio&VideoAccessories&#124;PCSpeakers|4\.1|5195\.0|
|8|B008QS9J6Y|Computers&Accessories&#124;Accessories&Peripherals&#124;Audio&VideoAccessories&#124;Webcams&VoIPEquipment&#124;Webcams|4\.3|20398\.0|
|9|B09P22HXH6|Computers&Accessories&#124;Accessories&Peripherals&#124;Audio&VideoAccessories&#124;Webcams&VoIPEquipment&#124;Webcams|4\.1|10976\.0|

Dari tabel 2 dapat dilihat:

- Suatu produk dapat populer dengan kategorinya berdasarkan `jumlah rating terbanyak`, membuat pengguna tertarik dan ingin melihat.
- Jumlah review dari `q ke 15867`, menyiratkan berbagai level atensi dan umpan balik terhadap suatu produk.
- Daftar produk yang memililki `rating di atas 3.5` mengindikasikan pengalmaan pengguna yang positif.
- Produk dengan `julmah review` tertinggi di kategorinya berpotensi menjadi top seller meskipun tanpa melalui data penjualan secara langsung.

#### Distribusi antara harga diskon dengan harga aslinya

<p align="center"><img src="https://github.com/Andi-IM/Amazon-Product-Recommendation-System/assets/21165698/6b301de5-ab8e-4020-9917-8819266c01e8"></p>
<p align="center">Gambar 3. Distribusi persebaran harga produk</p>

Berdasarkan gambar 3 dapat dilihat bahwa:

- Harga diskon secara umum lebih rendah dari harga asliny, dengan median harga diskon 200 rupee dan harga asli 400 rupee.
- Distribusi persentase diskon miring ke kiri (left-skewed), dengan produk yang terbanyak diberi diskon sebesar 30% atau lebih rendah.
- Output menyarankan untuk lebih berpeluang untung dengan meningkatkan persentase diskon atau harga diskon untuk mendatangkan lebih banyak pelanggan.



## *Data Preparation*

*Data preparation* atau *data preprocessing* adalah teknik digunakan untuk mengubah data mendah ke dalam format yang berguna dan efisien[^7]. Fungsi utama dari *data preparation* adalah untuk memastikan bahwa data mentah yang akan diproses sudah akurat yang berimplikasi pada hasil analitik yang valid. Proses *data preparation* dilakukan empat tahap persiapan data, yaitu Data Ingestion, Data Cleaning, dan Data Formating. Pada tahap *Data Ingestion*, berikut beberapa pengecekan yang dilakukan:

- Mengimpor data dari format csv ke bentuk DataFrame dengan library Pandas.
- Membaca informasi data.
- Mencari duplikasi data.
- Mencari *missing value* atau nilai yang hilang.

Pada tahap *Data Cleaning*, ada beberapa metode yang digunakan yaitu:

- Membuang data yang memiliki nilai-nilai yang hilang (*Dropping*)
- Mengisi nilai-nilai yang hilang (*Imputation*)
- Interpolasi menghasilkan titik-titik data baru dalam janngkauan suatu data.



## *Modeling*

Seperti yang dijelaskan sebelumnya, model sistem rekomendasi dibangun dengan pendekatan Content-based filtering dan Collaborative filtering. Pada content-based filtering, algoritma akan memberikan rekomendasi berdasarkan hal yang serupa dengan konten yang disukai oleh pengguna di masa lalu. Sebagai contoh, misalkan ada seorang pengguna yang menonton film "The Avengers" melalui platform streaming online, lalu algoritma ini akan memberikan rekomendasi film yang memiliki genre yang sama, katakanlah genre Action. Informasi yang didapatkan akan disimpan berdasarkan vektor. Vektor ini berisi kebiasaan pengguna, seperti film yang disuka dan tidak disuka dan rating yang diberikan. Vektor ini dinamakan vektor profil. Semua informasi disimpan dalam vektor lain disebut sebagai vektor item. Vektor tersebut dikalkuklasikan dengan persamaan cosine similarity berikut:

$$ sim(A, B) = cos(\theta) = \frac{A . B}{||A||||B||} $$

Pada collaborative filtering, algoritma berfokus pada pendapat komunitas penggujna. Pada *user-based collaborative filtering*, algoritma akan melihat kesamaan selera pengguna. Katakanlah Galih dan Ratna memberikan rating tertinggi untuk sejumlah film action. Jika Galih menyukai film The Avengers, Ratna juga kemungkinan akan menyukai film tersebut. 

<p align="center"><img src="https://dicoding-web-img.sgp1.cdn.digitaloceanspaces.com/original/academy/dos:4234dba104aca84b9b1f2affdb625b8c20210912135018.png"></p>
<p align="center">Gambar X. User-based Collaborative Filtering</p>

Pendekatan content-based filtering dan collaborative filtering dikombinasikan dan dinamakan sebagai sistem rekomendasi pendekatan hybrid. 

<p align="center"><img src="https://github.com/Andi-IM/Amazon-Product-Recommendation-System/assets/21165698/d51d2a22-4051-4696-b243-e013fdca4994"></p>
<p align="center">Gambar XI. Sistem Rekomendasi Hybrid</p>

Sistem rekomendasi akan memfilter berdasarkan produk yang pelanggan suka dan mengurutkannya berdasarkan rating yang diberikan. 


## *Evaluation*



## Kesimpulan

Dari hasil evaluasi di atas, maka dapat disimpulkan bahwa:

## *References*

[^1]: Henry Februariyanti *"Implementasi Metode Collaborative Filtering untuk Sistem Rekomendasi Penjualan pada Toko Mebel"* 2021, 43-50, doi: [tautan](https://doi.org/10.31294/jki.v9i1.9859.g4873)

[^2]: Esha Alma'arif, dkk. *"Implementasi Algoritma Apriori Untuk Rekomendasi Produk Pada Toko Online"*, Citec Journal, 2020

[^3]: Munawar dkk "Sistem Rekomendasi Hibrid Menggunakan Algoritma Apriori Mining Asosiasi", TEMATIK -Jurnal Teknologi Informasi Dan Komunikasi, 8(1), 69–80. 2021, doi: [tautan](https://doi.org/10.38204/tematik.v8i1.567)

[^4]: Munawar dkk/ *"Meningkatkan Rekomendasi Menggunakan Algoritma Perbedaan Topik"* . J-SIKA| Jurnal Sistem Informasi Karya Anak Bangsa, 02(02), 17–26. Diambil dari [tautan](https://ejournal.unibba.ac.id/index.php/j-sika/article/view/378).

[^5]: Mohamed, Marwa & Khafagy, Mohamed & Ibrahim, Mohamed. (2019). Recommender Systems Challenges and Solutions Survey. 10.1109/ITCE.2019.8646645.

[^6]: Huber, S. (2018). A holistic extension to the CRISP-DM model. Science Direct, (12th CIRP Conference on Intelligent Computation in Manufacturing Engineering, 18-20 July 2018, Gulf of Naples, Italy).

[^7]: C. Chatfield, “Exploratory data analysis,” European Journal of Operational Research, vol. 23, no. 1, pp. 5–13, Jan. 1986, doi: https://doi.org/10.1016/0377-2217(86)90209-2.

[^8]: Laraswati. (2022). Tahapan Data Preparation agar Data Lebih Mudah Diproses, diakses pada tanggal 28 Februari 2024, https://blog.algorit.ma/data-preparation/ 



