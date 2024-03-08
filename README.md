# Laporan Proyek Machine Learning - Andi Irham

## Project Overview

Dewasa ini kemajuan teknologi mengalami perkembangan yang sangat peseat, selain itu di dunia bisnis teknologi mempunyai peranan yang sangat penting. Melalui media internet/website baik pelaku bisnis maupun konsumen dapat melakukan transaksi dengan cara *online* kapanpun dan di mana pun dengan orang-orang di seluruh duniap[^1]. Salah satu bentuk teknologi yang dapat dirasakan manfaatnya oleh banyak orang adalah dengan toko online yang dapat dijangkau dari semua kalangan. Meskipun  banyak muncul toko online baru, teteapi tidak banyak toko online yang mampu bertahan lama, karena persaingan yang sangat ketat. Banyaknya kesalahan dalam pemasaran produk oleh pemilik usaha sehingga mengeluarkan banyak biaya terhadap produk yang belum tentu diminati konsumen[^2]. Sistem rekomendasi dapat menjangkau pengguna yang memang membutuhkan produk dari pemilik usaha dengan mengetahui pola belanja konsumen, seperti preferensi masa lalu, riwayat pembelian dan informasi demografis[^3],[^4]. Dengan adanya sistem rekomendasi membuat produk yang ditawarkan pemilik akan dengan lebih mudah dijangkau oleh sasaran pengguna sehingga baik itu pemilik usaha dan konsumen diuntungkan.  

Dalam hal pengembangan model sistem rekomendasi, ada banyak faktor yang bisa menjadi bahan pertimbangan[^5]. Pada sistem rekomendasi produk , faktor-faktor yang dapat menjadi bahan pertimbangan antara lain seperti kategori, rating pengguna, dan review pengguna. Proyek ini menggunakan beberapa pendekatan sistem rekomendasi yaitu pendekatan basis konten (*Content-based Approach*) dan Pendekatan Kolaboratif (*Collaborative Approach*) yang selengkapnya akan dijelaskan pada tahap modeling. Tahapan pengembangan sistem rekomendasi mengikuti tahapan dari standar baku CRISP-DM atau *Cross-industry Standard Process for Data Mining*[^6] yang dijelaskan pada gambar 1 berikut ini:

<p align="center"><img src="https://github.com/Andi-IM/Amazon-Product-Recommendation-System/assets/21165698/94f45723-78da-4800-a8b7-9359a41f1c2c"></p>
<p align="center">Gambar 1. Alur Proyek Sistem Rekomendsasi</p>

Proses dimulai dari *Business Understanding*, yaitu tahapan memahami masalah bisnis dan kemudian mrancang solusi analitik berdasarkan data untuk menyelesaikan permasalahan tersebut. Tahapan yang dijelaskan pada tahapan ini meliputi *problem statement*, *goals*, dan *solution approach*. Setelah memahami masalah dan menentukan solusinya, tahapan berlanjut pada *Data Understanding* dengan melihat infromasi data dan menentukan kualitasnya. Pemahaman data sangat penting untuk menghindari masalah yang tidak terduga pada fase berikutnya, yaitu *Data Preparation*. *Data preparation* di proyek ini adalah melakukan *cleaning data* yang hilang dan meng-encode data sehingga dapat diproses model, lalu pada akhirnya membagi data menjadi training dan test sebelum melakukan pemodelan. Pada tahap pemodelan dan evaluasi, dilakukan proses trainng dan melihat ukuran performa dari model untuk menentukan apakah model tersebut baik atau kurang. 

## *Business Understanding*

Pengembangan model Sistem Rekomendasi Produk memeiliki potensi atau manfaat yang menjadi salah satu alat bantu dalam pengambilan keputusan oleh pengguna aplikasi e-commerce. Contoh potensi manfaat dari Sistem Rekomendasi Produk ini adalah membantu pengguna mendapatkan produk yang dibutuhkan tanpa tenaga ekstra.

### Problem Statements

Berdasarkan dari kondisi yang telah diuraikan sebelumnya, maka diperlukan sistem yang dapat memberikan rekomendasi terhadap pengguna dengan menjawab permasalahan berikut:

- Bagaimana distribusi produk untuk setiap kategori?
- Berapa rata-rata rating untuk setiap kategori produk?
- Kategori apa saja yang memiliki rating tertinggi?
- Apa hubungan antara rating dengan jumlah ulasan?  
- Bagaimana distribusi diskon untuk setiap kategori?
- Bagaimana mengolah *dataset* agar model sistem rekomendasi dapat berjalan dengan baik?
- Bagaimana membuat model sistem yang dapat memberikan rekomendasi produk?
- Bagaimana melakukan evaluasi untuk memastikan model yang dibagun dapat digunakan? 

### Goals
Berdasarkan *problem statement* di atas maka tujuan dari pengembangan sistem rekomendasi adalah sebagai berikut:

- Mengetahui distribusi produk untuk setiap kategori.
- Mengetahui dampak rating dengan keputusan pembelian produk di suatu kategori.
- Mengetahui dampak jumlah rating dan rating yang diberikan dengan keputusan membeli produk.
- Mengetahui dampak diskon dengan keputusan pembelian produk di suatu kategori.
- Mengetahui hubungan distribusi antara harga diskon dengan harga aslinya.
- Mengetahui perubahan rata-rata diskon di setiap kategori.
- Mempersiapkan data dengan memilih fitur, melakukan *encoding*, dan membagi data agar dapat dilatih dan memberikan rekomendasi.
- Mengembangkan model dengan metode *content-based filtering*, *collaborative filtering*, dan memanfaatkan keduanya sekaligus agar dapat memaksimalkan potensi dari kedua model.
- Menganalisa kemampuan dari kedua metode sistem rekomendasi dengan metrik evaluasi model.

### Solution Approach

Dari *Problem Statement* dan *Goals* yang telah dideskripsikan, maka didapatkan solusi sebagai berikut:

- Mengekplorasi fitur yang terdapat pada dataset dengan menggunakan teknik analisis univariat dan multivariat. Analisis univariat digunakan untuk melihat hubungan data. Analisis multivariat untuk melihat hubungan antar fitur. Analisis univariat dan multivariat dapat dengan mudah dipaahami melalui visualisasi.
- Mempersiapkan data yang akan digunakan meliputi *Data Ingesting*, *Data Cleaning*, dan *Data Formating*.
- Mengekplorasi model rekomendasi sesuai dengan *behavior* rekomendasi yang diinginkan, dalam kasus ini menggunakan metode *Content-based Filtering* dengan menggunakan pendekatan *cosine similarity* dan *Colaborative Filtering* menggunakan model *deep learning*.
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

Untuk dapat memahami data lebih jelas, maka dilakukan analisis data melalui metode statistik yang disebut sebagai Analisis Data Eksplanatori (Explanatory Data Analysis) atau disingkat EDA[^7]. Berikut ini adalah hasil EDA dengan menggunakan analisis multivariat.

#### Distribusi produk di setiap kategori

Fitur `category` dipecah menjadi `main_category` dan `sub_cateogry` untuk mempermudah analisis sehingga didapat insight seperti pada Gambar 1 dan 2. 

<p align="center"><img src="https://github.com/Andi-IM/Amazon-Product-Recommendation-System/assets/21165698/26574d3a-c31f-43f7-9395-db213734bb3a"></p>
<p align="center">Gambar 1. Distribusi produk pada kategori utama</p>

Dari Gambar 1 diperoleh beberapa insight:

- Tiga kategori teratas adalah `Electronics`, `Computer & Accessories`, dan `Home & Kitchen`. Hal ini memperlihatkan barang-barang tersebut adalah yang terpopuler di antara pelanggan.
- Jumlah produk di `main categories` lainnya cukup sedikit, menunjukkan bahwa kategori tersebut tidak sepopuler tiga kategori teratas.
- `Office Product`, `Musical Instruments`, `Home Improvement`, `Toys & Games`, `Car & Motorbike` dan `Health & Personal Care` memiliki jumlah produk yang sedikit yang berarti permintaan pada kategori tersebut juga sedikit.
- Secara keseluruhan, data ini dapat membantu pemahaman bisnis mengenai tren pasar dan mengenali peluang menguntungkan untuk perkembangan di kategori tertentu.

<p align="center"><img src="https://github.com/Andi-IM/Amazon-Product-Recommendation-System/assets/21165698/438914a9-c957-49d9-a064-4ee665a84dea"></p>
<p align="center">Gambar 2. Distribusi produk pada sub kategori</p>

Dari Gambar 2 diperoleh beberapa insight sebagai berikut:

- Enam subkategori teratas adalah `USB Cabels`, `Smartwatches`, `Smartphones`, `SmartTelevisions`, `In Ear`, dan `RemoteControls`. Subkategori tersebut merupakan yang terpopuler sehingga bisnis mungkin akan berfokus pada produk-produk tersebut.
- Subkategori terpopuler lainnya ada `MixerGrinders`, `HDMICables`, `DryIrons`, `Mice`, dan `InstantWaterHeaters`. Subkategori tersebut kurang populer jika dibandingkan dengan enam teratas, namun masih diminati dan ada kebutuhan dengan produk tersebut.
- Data di atas memperlihatkan keanekaramanan subkategori di 30 teratas meliputi peralatan dapur, barang elektronik rumah, dan aksesoris pribadi. INi memperlihatkan pentingnya untuk menyediakan produk-produk yang bervariasi untuk kebutuhan pelanggan yang berbeda-beda.
- Secara keseluruhan data tersebut membantu bisnis mengenali subkategori yang populer dan mengatur tawaran produk untuk menjangkau permintaan pelanggan. Dengan fokus pada subkategori tersebut akan membantu meningkatkan penjualan.

#### Distribusi rating pelanggan.

<p align="center"><img src="https://github.com/Andi-IM/Amazon-Product-Recommendation-System/assets/21165698/fbd70f96-5512-4289-9495-5d46b4d8a4a5"></p>
<p align="center">Gambar 3. Distribusi rating pelanggan</p>

Dari Gambar 3 dapat dilihat bahwa:

- Mayoritas pelanggan memberi rating dari 3-4 dan 4-5, dengan total 1453 ulasan.
- Terdapat peningkatan nyata dalam jumlah ulasan pada rentang 2-3 dibandingkan dengan rentang 0-1 dan 1-2 yang lebih rendah.
- Jumlah ulasan terendah terdapat pada rentang 0-1, yang menunjukkan bahwa mungkin masih ada ruang untuk perbaikan dalam hal kepuasan pelanggan.
- Secara keseluruhan, distribusi peringkat pelanggan menunjukkan bahwa sebagian besar pelanggan puas dengan produk, namun mungkin ada peluang perbaikan untuk meningkatkan jumlah peringkat positif.

#### Distribusi Rating Berdasarkan Kategori

Distribusi rating berdasarkan kategori utama dan subkategori untuk melihat pendapat pengalaman yang pengguna dapatkan dengan produk-produk pada kategori utama dan sub kategori.

<p align="center"><img src="https://github.com/Andi-IM/Amazon-Product-Recommendation-System/assets/21165698/5c379d13-542b-4113-bb84-044c37696550"></p>
<p align="center">Gambar 4. Distribusi rata-rata rating pelanggan di setiap kategori utama</p>

Pada Gambar 4 dapat diperoleh informasi:

- Dapat dilihat kategori utama diurutkan berdasarkan rating rata-ratanya.
- Kategori dengan rating tertinggi adalah `OfficeProducts`, `Toys&Games`, dan `HomeImprovement` dengan rating di atas 4. Ini menyatakan bahwa pelanggan secara umum suka dengan produk yang ditawarkan pada kategori tersebut.
- Di sisi lain, kategori utama dengan rating rendah ada `Car&Motorbike`, `MusicalInstruments`,  dan `Health&PersonalCare` dengan rating di bawah 4. Ini berarti perlu adanya perbaikan untuk dapat memenuhi ekspetasi pelanggan.

<p align="center"><img src="https://github.com/Andi-IM/Amazon-Product-Recommendation-System/assets/21165698/8451131e-0387-4503-97f8-d8818b0b76cd"></p>
<p align="center">Gambar 5. Distribusi rata-rata rating pelanggan di setiap sub kategori</p>

Dari Gambar 5 dapat diperoleh informasi bahwa:

- Dari tabel dapat dilihat rating dari sub kategori dari atas hingga bawah.
- Produk "tablet", merupakan subkategori teratas dengan rating 4.6 yang berarti pelanggan puas dengan pembeliannya.
- Namun, subkategori terbawah seperti "Dustcovers" dan "ElectricGrinders", memiliki rating terendah,yang berarti pelanggan tidak begitu puas dengan produk tersebut.
- Wawasan seperti ini dapat membantu bisnis fokus pada peningkatan kualitas produk mereka dan meningkatkan pengalaman pelanggan secara keseluruhan. Penting untuk melacak umpan balik pelanggan untuk mengidentifikasi area yang perlu ditingkatkan dan terus memenuhi kebutuhan dan harapan mereka.

#### Produk dengan rating terbanyak

Tabel 1. Daftar Produk dengan Rating terbanyak.

|index|main\_category|sub\_category|rating|rating\_count|rating\_weighted|
|---|---|---|---|---|---|
|0|Computers&Accessories|Webcams|4\.3|20398\.0|87711\.4|
|1|Computers&Accessories|PCMicrophones|3\.9|14969\.0|58379\.1|
|2|Computers&Accessories|Webcams|4\.1|10976\.0|45001\.6|
|3|Computers&Accessories|PCSpeakers|4\.0|7352\.0|29408\.0|
|4|Computers&Accessories|PCHeadsets|3\.5|7222\.0|25277\.0|
|5|Computers&Accessories|PCSpeakers|4\.1|5195\.0|21299\.499999999996|
|6|Computers&Accessories|USBtoUSBAdapters|4\.3|4426\.0|19031\.8|
|7|Computers&Accessories|PCMicrophones|3\.3|2804\.0|9253\.199999999999|
|8|Computers&Accessories|USBtoUSBAdapters|4\.0|1540\.0|6160\.0|
|9|Car&Motorbike|AirPurifiers&Ionizers|3\.8|1118\.0|4248\.4|

Tabel 1 memberikan informasi bahwa:

- Suatu produk dapat populer dengan kategorinya berdasarkan `jumlah rating` yang banyak, membuat pengguna tertarik dan ingin melihat.
- Daftar produk yang  memiliki `rating di atas 3.5` mengidikasikan pengalaman pengguna yang positif.
- Produk dengan `jumlah review` tertinggi di kategorinya berpotensi menjadi top seller meskipun tanpa melalui data penjualan secara langsung.

#### Persentase Diskon di Setiap Kategori

<p align="center"><img src="https://github.com/Andi-IM/Amazon-Product-Recommendation-System/assets/21165698/4bbefbc3-a081-4d60-8cda-a473f214c8ac"></p>
<p align="center">Gambar 6. Persentase diskon berdasarkan kategori utama</p>

Dari Gambar 6 Dapat dilihat bahwa:

- Kategori `Toys&games` memiliki permintaan yang cukup tinggi dimana penjual tidak perlu secara signifikan memberikan diskon untuk penjualan produk di kategori ini.
- `Home&Kitchen` dan `Car&Motorbike` mempunyai rata-rata persentase diskon yang serupa, dengan nilai 40% - 42%. Ini menunjukkan bahwa level kompetisi yang sama dengan sensitivitas harga di kedua kategori tersebut.
- Kategori dengan rata-rata diskon tertinggi adalah `HomeImprovement`, `Computer&Accessories`, dan `Elektronik` dengan nilai 57%, 54%, dan 51%. Ini mengindikasikan bahwa di kategori tersebut memiliki harga sangat sensitif, dan penjual harus lebih aktraktif dalam memberikan diskon untuk dapat berkompetisi lebih efektif.
- Juga menarik untuk dilihat bahwa, `OfficeProducts` dan `Health&PersonalCare` punya rata-rata diskon 12% dan 53%, yang berarti di antara kedua kategori tersebut merupakan rata-rata diskon terendah dan tertinggi. Hal ini menunjukkan bahwa kategori-kategori ini mungkin memiliki tingkat sensitivitas harga tertentu, namun tidak pada tingkat yang sama dengan `HomeImprovement`, `Computers&Accessories`, dan `Electronics`.

<p align="center"><img src="https://github.com/Andi-IM/Amazon-Product-Recommendation-System/assets/21165698/4bbefbc3-a081-4d60-8cda-a473f214c8ac"></p>
<p align="center">Gambar 7. Persentase diskon berdasarkan subkategori</p>

Dari grafik di atas dilihat bahwa:

- Tabel diatas memperlihatkan rata-rata diskon tiap subkategori diurutkan secara mundur.
- Subkategori yang memiliki rata-rata diskon rendah adalah `Basic`, dengan nilai 0.0. Hal ini menyatakan bahwa produk ini adalah produk dengan harga murah dan sederhana, pemberian diskon tidak memberikan efek apa-apa pada produk ini.
- `BatteryChargers`, `3DGlasses`, dan `BasicMobiles` adalah contoh subkategori dengan persentase diskon rata-rata sedang, dengan nilai antara 0.18 dan 0.25. Hal ini menunjukkan bahwa produk-produk ini mungkin sensitif terhadap harga, namun tidak pada tingkat yang sama dengan produk-produk dalam subkategori persentase diskon rata-rata yang lebih tinggi.
- `BluetoothSpeakers`, `Bedstand&DeskMounts` dan `BasicCases` adalah contoh subkategori dengan persentase diskon rata-rata tinggi, dengan nilai antara 0.485 dan 0.745. Hal ini menunjukkan bahwa produk-produk ini mungkin lebih sensitif terhadap harga, dan pengecer mungkin perlu menawarkan diskon menarik untuk bersaing secara efektif dalam subkategori ini.
- Subkategori dengan persentase mean diskon tertinggi adalah Subkategori `Adapter` dengan nilai sebesar 0,803333. Hal ini menunjukkan bahwa persaingan untuk produk-produk tersebut tinggi, dan pengecer harus menawarkan diskon yang signifikan untuk menarik pembeli.

#### Analisis Sentimen

<p align="center"><img src="https://github.com/Andi-IM/Amazon-Product-Recommendation-System/assets/21165698/a84bc75d-6740-4d28-b39d-4c71b024f36c"></p>
<p align="center">Gambar 8. Hasil analisis sentimen dari review produk</p>

Secara garis besar review produk yang diberikan oleh pelanggan positif, namun bukan berarti rating yang tinggi berimplikasi pada review yang baik seperti yang ditampilkan pada tabel 2.

Tabel 2. Sampel sentimen yang diberikan pelanggan terhadap produk yang mereka beli.

|index|Sentiment|Review|Rating|
|---|---|---|---|
|0|Positive|Looks durable Charging is fine tooNo complains,Charging is really fast, good product\.,Till now satisfied with the quality\.,This is a good product \. The charging speed is slower than the original iPhone cable,Good quality, would recommend,https://m\.media-amazon\.com/images/W/WEBP\_402378-T1/images/I/81---F1ZgHL\.\_SY88\.jpg,Product had worked well till date and was having no issue\.Cable is also sturdy enough\.\.\.Have asked for replacement and company is doing the same\.\.\.,Value for money|4\.2|
|1|Neutral|I am posting this after a few weeks of using the product\.Usage: Continuous, OTT only, no Cable/Dish operator\.Average daily usage: 6-8 hours\.The TV is a great value-for-money product\.Installation: The installation was simple and Amazon assisted installation was smooth, timely and hassle-free\.Picture: The picture quality is not great when compared with the smoothness of a Sony, LG and Samsung with these kind of specs\. Movies and especially hi-res TV series experience was somewhat diluted as most of the times, the output, while in hi-res , wouldn't look like a movie quality which we are used to of watching in the likes of Sony, Samsung LG etc however, with time, you get used to it and only realize the difference when you see the same movie at someone else's better TV\.Sound: Sound output is decent\. You wouldn't need additional support to enhance the volume as such\...|4\.2|
|2|Negative|Overall good\.,TV picture ok smart betterSound very low another brand,Service provider refuse install my TV, bad service and samsung, I am calling 3 times service provider\. Not meet my home address\.why ? Bad bad,They product did not come with the support stand or wall hanging hook to install the Tv,Picture quality is very poor in cables,Floor stand does not come with it \.\.\. You have to buy it seperately\. Request Amazon to cleary mention it in the add \. You will have to pay seperate charges for the installation guy to buy the floor mount \.,Good,|4\.3|

Dapat dilihat produk yang memiliki review negatif tetap diberikan rating 4.3.


## *Data Preparation*

*Data preparation* atau *data preprocessing* adalah teknik digunakan untuk mengubah data mendah ke dalam format yang berguna dan efisien[^7]. Fungsi utama dari *data preparation* adalah untuk memastikan bahwa data mentah yang akan diproses sudah akurat yang berimplikasi pada hasil analitik yang valid. Proses *data preparation* dilakukan empat tahap persiapan data, yaitu *Data Ingestion*, *Data Cleaning*, dan *Data Formating*. Pada tahap *Data Ingestion*, berikut beberapa pengecekan yang dilakukan:

- Mengimpor data dari format csv ke bentuk DataFrame dengan library Pandas.
- Membaca informasi data.
- Mencari duplikasi data.
- Mencari *missing value* atau nilai yang hilang.

Pada tahap *Data Cleaning*, ada beberapa metode yang digunakan yaitu:

- Membuang data yang memiliki nilai-nilai yang hilang (*Dropping*)
- Mengisi nilai-nilai yang hilang (*Imputation*)
- Interpolasi menghasilkan titik-titik data baru dalam janngkauan suatu data.

Ketika menggunakan fungsi `isna().sum()` terdapat 2 baris data yang hilang, yaitu pada fitur rating_count.

Tabel 3. Data yang hilang

|index|rating\_count|
|---|---|
|282|NaN|
|324|NaN|

Data yang hilang ini dapat dihapus dengan menggunakan fungsi `drop` agar tidak mengganggu analisa data. Selain pada fitur rating_count, data yang hilang juga terdapat pada fitur rating.

```
4.1    244
4.3    230
4.2    228
4.0    129
3.9    123
4.4    123
3.8     86
4.5     75
4       52
3.7     42
3.6     35
3.5     26
4.6     17
3.3     16
3.4     10
4.7      6
3.1      4
4.8      3
3.2      2
2.8      2
3.0      2
5.0      2
2.3      1
|        1
2        1
3        1
2.6      1
2.9      1
Name: rating, dtype: int64
```

Data dengan nilai yang aneh juga dihilangkan dengan mengeliminasi baris yang memiliki nilai yang aneh. Dengan membersihkan data dan memahami pola data yang disajikan maka dapat dilakukan seleksi fitur, *encoding* dan dimulai pengembangan model pada tahap selanjutnya. 

## *Modeling and Result*

Seperti yang dijelaskan sebelumnya, model sistem rekomendasi dibangun dengan pendekatan Content-based filtering dan Collaborative filtering. Pada content-based filtering, algoritma akan memberikan rekomendasi berdasarkan hal yang serupa dengan konten yang disukai oleh pengguna di masa lalu. Sebagai contoh, misalkan ada seorang pengguna yang menonton film "The Avengers" melalui platform streaming online, lalu algoritma ini akan memberikan rekomendasi film yang memiliki genre yang sama, katakanlah genre Action. Informasi yang didapatkan akan disimpan berdasarkan vektor. Vektor ini berisi kebiasaan pengguna, seperti film yang disuka dan tidak disuka dan rating yang diberikan. Vektor ini dinamakan vektor profil. Semua informasi disimpan dalam vektor lain disebut sebagai vektor item. Vektor tersebut dikalkuklasikan dengan persamaan cosine similarity berikut:

$$ sim(A, B) = cos(\theta) = \frac{A . B}{||A||||B||} $$

Dimana:

- A, B menyatakan produk titik dari vektor A dan B
- ||A|| mewakili norma Euclidean (magnitude) dari vektor A.
- ||B|| mewakili norma Euclidean (magnitude) dari vektor B.

Sistem rekomendasi dengan model collaborative filtering memiliki kelebihan dengan kemampuannya memberikan rekomendasi yang personal, namun juga memiliki kelemahan untuk memberikan rekomendasi item yang sangat berbeda dari yang telah disukai pengguna.

Pada collaborative filtering, algoritma berfokus pada pendapat komunitas pengguna. Pada *user-based collaborative filtering*, algoritma akan melihat kesamaan selera pengguna. Katakanlah Galih dan Ratna memberikan rating tertinggi untuk sejumlah film action. Jika Galih menyukai film The Avengers, Ratna juga kemungkinan akan menyukai film tersebut. 

<p align="center"><img src="https://dicoding-web-img.sgp1.cdn.digitaloceanspaces.com/original/academy/dos:4234dba104aca84b9b1f2affdb625b8c20210912135018.png"></p>
<p align="center">Gambar 9. User-based Collaborative Filtering</p>

Sistem rekomendasi dengan collaborative filtering memiliki kemampuan untuk menjangkau produk yang beragam, namun akan menjadi masalah jika menerapkan sistem rekomendasi ini pada tahap awal pengembangan produk. Sehingga solusi dari permasalahan ini adalah menggunakan pendekatan *hybrid*. Pendekatan content-based filtering dan collaborative filtering dikombinasikan atau pendekatan *hybrid* akan meberikan hasil rekomendasi yang baik tanpa khawatir dengan keandalan sistem untuk awal pengembangan. 

<p align="center"><img src="https://github.com/Andi-IM/Amazon-Product-Recommendation-System/assets/21165698/d51d2a22-4051-4696-b243-e013fdca4994"></p>
<p align="center">Gambar 10. Sistem Rekomendasi Hybrid</p>

Sistem rekomendasi akan memfilter berdasarkan produk yang pelanggan suka dan mengurutkannya berdasarkan rating yang diberikan. Kedua model akan diuji dengan data produk sampel dengan id `B07JW9H4J1` untuk dilihat kemampuannya seperti yang dapat dilihat pada Tabel 3 berikut ini.

**Tabel 4. Produk dengan ID `B07JW9H4J1`**

|index|product\_id|product\_name|category|sub\_category|
|---|---|---|---|---|
|0|B07JW9H4J1|Wayona Nylon Braided USB to Lightning Fast Charging and Data Sync Cable Compatible for iPhone 13, 12,11, X, 8, 7, 6, 5, iPad Air, Pro, Mini \(3 FT Pack of 1, Grey\)|Computers&Accessories&#124;Accessories&Peripherals&#124;Cables&Accessories&#124;Cables&#124;USBCables|USBCables|
|369|B07JW9H4J1|Wayona Nylon Braided USB to Lightning Fast Charging and Data Sync Cable Compatible for iPhone 13, 12,11, X, 8, 7, 6, 5, iPad Air, Pro, Mini \(3 FT Pack of 1, Grey\)|Computers&Accessories&#124;Accessories&Peripherals&#124;Cables&Accessories&#124;Cables&#124;USBCables|USBCables|
|614|B07JW9H4J1|Wayona Nylon Braided USB to Lightning Fast Charging and Data Sync Cable Compatible for iPhone 13, 12,11, X, 8, 7, 6, 5, iPad Air, Pro, Mini \(3 FT Pack of 1, Grey\)|Computers&Accessories&#124;Accessories&Peripherals&#124;Cables&Accessories&#124;Cables&#124;USBCables|USBCables|

Model rekomendasi *Content-based Filtering* akan memberikan rekomendasi berdasarkan kategori seperti tabel 3 berikut ini.

Tabel 5. Produk hasil rekomendasi dengan metode *Content-based Filtering*

|index|product\_name|category|sub\_category|
|---|---|---|---|
|614|Wayona Nylon Braided USB to Lightning Fast Charging and Data Sync Cable Compatible for iPhone 13, 12,11, X, 8, 7, 6, 5, iPad Air, Pro, Mini \(3 FT Pack of 1, Grey\)|Computers&Accessories&#124;Accessories&Peripherals&#124;Cables&Accessories&#124;Cables&#124;USBCables|USBCables|
|369|Wayona Nylon Braided USB to Lightning Fast Charging and Data Sync Cable Compatible for iPhone 13, 12,11, X, 8, 7, 6, 5, iPad Air, Pro, Mini \(3 FT Pack of 1, Grey\)|Computers&Accessories&#124;Accessories&Peripherals&#124;Cables&Accessories&#124;Cables&#124;USBCables|USBCables|
|220|Wayona Nylon Braided Usb Syncing And Charging Cable Sync And Charging Cable For Iphone, Ipad \(3 Ft, Black\) - Pack Of 2|Computers&Accessories&#124;Accessories&Peripherals&#124;Cables&Accessories&#124;Cables&#124;USBCables|USBCables|
|42|Wayona Nylon Braided 3A Lightning to USB A Syncing and Fast Charging Data Cable for iPhone, Ipad \(3 FT Pack of 1, Black\)|Computers&Accessories&#124;Accessories&Peripherals&#124;Cables&Accessories&#124;Cables&#124;USBCables|USBCables|
|89|Wayona Nylon Braided \(2 Pack\) Lightning Fast Usb Data Cable Fast Charger Cord For Iphone, Ipad Tablet \(3 Ft Pack Of 2, Grey\)|Computers&Accessories&#124;Accessories&Peripherals&#124;Cables&Accessories&#124;Cables&#124;USBCables|USBCables|
|80|Wayona Usb Nylon Braided Data Sync And Charging Cable For Iphone, Ipad Tablet \(Red, Black\)|Computers&Accessories&#124;Accessories&Peripherals&#124;Cables&Accessories&#124;Cables&#124;USBCables|USBCables|
|106|Wayona Nylon Braided 2M / 6Ft Fast Charge Usb To Lightning Data Sync And Charging Cable For Iphone, Ipad Tablet \(6 Ft Pack Of 1, Grey\)|Computers&Accessories&#124;Accessories&Peripherals&#124;Cables&Accessories&#124;Cables&#124;USBCables|USBCables|
|166|Wayona Nylon Braided Lightning USB Data Sync & 3A Charging Cable for iPhones, iPad Air, iPad Mini, iPod Nano and iPod Touch \(3 FT Pack of 1, Grey\)|Computers&Accessories&#124;Accessories&Peripherals&#124;Cables&Accessories&#124;Cables&#124;USBCables|USBCables|
|208|MYVN LTG to USB for Fast Charging & Data Sync USB Cable Compatible for iPhone 5/5s/6/6S/7/7+/8/8+/10/11, iPad Air/Mini, iPod and iOS Devices \(1 M\)|Computers&Accessories&#124;Accessories&Peripherals&#124;Cables&Accessories&#124;Cables&#124;USBCables|USBCables|
|78|SWAPKART Fast Charging Cable and Data Sync USB Cable Compatible for iPhone 6/6S/7/7+/8/8+/10/11, 12, 13 Pro max iPad Air/Mini, iPod and iOS Devices \(White\)|Computers&Accessories&#124;Accessories&Peripherals&#124;Cables&Accessories&#124;Cables&#124;USBCables|USBCables|

Dapat dilihat, produk dengan subkategori `USB Cable` menjadi rekomendasi karena kategori pada produk dengan id `B07JW9H4J1` juga merupakan produk dengan kategori yang sama.

Berikut ini juga merupakan hasil rekomendasi dengan metode *Collaborative Filtering*:

Tabel 6 Hasil rekomendasi metode *Collaborative Filtering*

|index|product\_name|category|sub\_category|rating|
|---|---|---|---|---|
|174|Syncwire LTG to USB Cable for Fast Charging Compatible with Phone 5/ 5C/ 5S/ 6/ 6S/ 7/8/ X/XR/XS Max/ 11/12/ 13 Series and Pad Air/Mini, Pod & Other Devices \(1\.1 Meter, White\)|Computers&Accessories&#124;Accessories&Peripherals&#124;Cables&Accessories&#124;Cables&#124;USBCables|USBCables|5\.0|
|249|Sony Bravia 164 cm \(65 inches\) 4K Ultra HD Smart LED Google TV KD-65X74K \(Black\)|Electronics&#124;HomeTheater,TV&Video&#124;Televisions&#124;SmartTelevisions|SmartTelevisions|4\.7|
|459|Spigen EZ Fit Tempered Glass Screen Protector for iPhone 14 Pro Max - 2 Pack \(Sensor Protection\)|Electronics&#124;Mobiles&Accessories&#124;MobileAccessories&#124;Maintenance,Upkeep&Repairs&#124;ScreenProtectors|ScreenProtectors|4\.7|
|775|Amazon Basics Wireless Mouse &#124; 2\.4 GHz Connection, 1600 DPI &#124; Type - C Adapter &#124; Upto 12 Months of Battery Life &#124; Ambidextrous Design &#124; Suitable for PC/Mac/Laptop|Computers&Accessories&#124;Accessories&Peripherals&#124;Keyboards,Mice&InputDevices&#124;Mice|Mice|5\.0|
|820|Redgear MP35 Speed-Type Gaming Mousepad \(Black/Red\)|Computers&Accessories&#124;Accessories&Peripherals&#124;PCGamingPeripherals&#124;Gamepads|Gamepads|4\.6|
|886|Logitech M331 Silent Plus Wireless Mouse, 2\.4GHz with USB Nano Receiver, 1000 DPI Optical Tracking, 3 Buttons, 24 Month Life Battery, PC/Mac/Laptop - Black|Computers&Accessories&#124;Accessories&Peripherals&#124;Keyboards,Mice&InputDevices&#124;Mice|Mice|4\.6|
|1201|Oratech Coffee Frother electric, milk frother electric, coffee beater, cappuccino maker, Coffee Foamer, Mocktail Mixer, Coffee Foam Maker, coffee whisker electric, Froth Maker, coffee stirrers electric, coffee frothers, Coffee Blender, \(6 Month Warranty\) \(Multicolour\)|Home&Kitchen&#124;Kitchen&HomeAppliances&#124;SmallKitchenAppliances&#124;HandBlenders|HandBlenders|4\.8|
|1223|FIGMENT Handheld Milk Frother Rechargeable, 3-Speed Electric Frother for Coffee with 2 Whisks and Coffee Decoration Tool, Coffee Frother Mixer, CRESCENT ENTERPRISES VRW0\.50BK \(A1\)|Home&Kitchen&#124;Kitchen&HomeAppliances&#124;SmallKitchenAppliances&#124;HandBlenders|HandBlenders|4\.7|
|1299|Instant Pot Air Fryer, Vortex 2QT, Touch Control Panel, 360° EvenCrisp™ Technology, Uses 95 % less Oil, 4-in-1 Appliance: Air Fry, Roast, Bake, Reheat \(Vortex 1\.97Litre, Black\)|Home&Kitchen&#124;Kitchen&HomeAppliances&#124;SmallKitchenAppliances&#124;DeepFatFryers&#124;AirFryers|AirFryers|4\.8|
|1388|Campfire Spring Chef Prolix Instant Portable Water Heater Geyser 1Ltr\. for Use Home Stainless Steel Baking Rack &#124; Restaurant &#124; Office &#124; Labs &#124; Clinics &#124; Saloon &#124; with Installation Kit \(With MCB\)|Home&Kitchen&#124;Heating,Cooling&AirQuality&#124;WaterHeaters&Geysers&#124;InstantWaterHeaters|InstantWaterHeaters|4\.7|

Hasil rekomendasi dengan collaborative filtering akan memberikan rekomendasi berdasarkan rating yang diberikan oleh seseorang, sehingga memberikan rekomendasi dengan rating yang mirip atau lebih baik.

Sementara itu, gabungan dari metode ini akan menghasilkan rekomendasi seperti apda tabel 7 berikut ini:

Tabel 7. Hasil rekomendasi dengan menggunakan kedua metode

|index|product\_id|product\_name|category|sub\_category|rating|
|---|---|---|---|---|---|
|777|B016XVRKZM|APC Back-UPS BX600C-IN 600VA / 360W, 230V, UPS System, an Ideal Power Backup & Protection for Home Office, Desktop PC & Home Electronics|Computers&Accessories&#124;Accessories&Peripherals&#124;UninterruptedPowerSupplies|UninterruptedPowerSupplies|3\.9|
|1302|B009UORDX4|Philips Hi113 1000-Watt Plastic Body Ptfe Coating Dry Iron, Pack of 1|Home&Kitchen&#124;Kitchen&HomeAppliances&#124;Vacuum,Cleaning&Ironing&#124;Irons,Steamers&Accessories&#124;Irons&#124;DryIrons|DryIrons|4\.3|
|166|B07JPJJZ2H|Wayona Nylon Braided Lightning USB Data Sync & 3A Charging Cable for iPhones, iPad Air, iPad Mini, iPod Nano and iPod Touch \(3 FT Pack of 1, Grey\)|Computers&Accessories&#124;Accessories&Peripherals&#124;Cables&Accessories&#124;Cables&#124;USBCables|USBCables|4\.2|
|42|B07JW1Y6XV|Wayona Nylon Braided 3A Lightning to USB A Syncing and Fast Charging Data Cable for iPhone, Ipad \(3 FT Pack of 1, Black\)|Computers&Accessories&#124;Accessories&Peripherals&#124;Cables&Accessories&#124;Cables&#124;USBCables|USBCables|4\.2|
|174|B0BP7XLX48|Syncwire LTG to USB Cable for Fast Charging Compatible with Phone 5/ 5C/ 5S/ 6/ 6S/ 7/8/ X/XR/XS Max/ 11/12/ 13 Series and Pad Air/Mini, Pod & Other Devices \(1\.1 Meter, White\)|Computers&Accessories&#124;Accessories&Peripherals&#124;Cables&Accessories&#124;Cables&#124;USBCables|USBCables|5\.0|
|1203|B07NKNBTT3|Pick Ur Needs® Lint Remover for Clothes High Range Rechargeable Lint Shaver for All Types of Clothes, Fabrics, Blanket with 1 Extra Blade Multicolor \(Rechargeable\)|Home&Kitchen&#124;Kitchen&HomeAppliances&#124;Vacuum,Cleaning&Ironing&#124;Irons,Steamers&Accessories&#124;LintShavers|LintShavers|4\.1|
|822|B00MUTWLW4|Logitech K480 Wireless Multi-Device Keyboard for Windows, macOS, iPadOS, Android or Chrome OS, Bluetooth, Compact, Compatible with PC, Mac, Laptop, Smartphone, Tablet - Black|Computers&Accessories&#124;Accessories&Peripherals&#124;Keyboards,Mice&InputDevices&#124;Keyboards|Keyboards|4\.4|
|1225|B09SZ5TWHW|Swiss Military VC03 Wireless Car Vacuum Cleaner &#124; Wireless Vacuum Cleaner for Home, Car, Living Room &#124; Wireless Vacuum Cleaner Dust Collection/Lighting Car Pet Hair Vacuum with Powerful Motor|Home&Kitchen&#124;Kitchen&HomeAppliances&#124;Vacuum,Cleaning&Ironing&#124;Vacuums&FloorCare&#124;Vacuums&#124;HandheldVacuums|HandheldVacuums|3\.9|
|461|B0971DWFDT|Portronics CarPower Mini Car Charger with Dual Output, Fast Charging \(Type C PD 18W + QC 3\.0A\) Compatible with All Smartphones\(Black\)|Electronics&#124;Mobiles&Accessories&#124;MobileAccessories&#124;Chargers&#124;AutomobileChargers|AutomobileChargers|4\.2|
|78|B0B2DJDCPX|SWAPKART Fast Charging Cable and Data Sync USB Cable Compatible for iPhone 6/6S/7/7+/8/8+/10/11, 12, 13 Pro max iPad Air/Mini, iPod and iOS Devices \(White\)|Computers&Accessories&#124;Accessories&Peripherals&#124;Cables&Accessories&#124;Cables&#124;USBCables|USBCables|3\.9|

Model ini akan memberikan rekomendasi berdasarkan kategori dan rating yang sesuai dengan yang pengguna berikan sebelumnya. 


## *Evaluation*

Pengukuran performa dari model sistem rekomendasi bergantung pada jenis sistem rekomendasi yang digunakan. Untuk model dengan *Content-based Filtering*, performa akan dihitung berdasarkan seberapa cocok produk yang direokmendasikan dengan kategorinya. Sedangkan *Collaborative filtering* akan menggunakan metrik pengukuran *model based*, contohnya RMSE. Untuk pendekatan *hybrid* tidak dilakukan pengecekan karena metode ini gabungan dari keduanya, jika keduanya memiliki hasil yang bagus, maka model *hybrid* akan memberikan rekomendasi bagus pula. 

### Pengujian Model *Content Based Filtering*

Model ini hanya menggunakan metrik Precision untuk mengetahui seberapa baik perforam model tersebut. Presisi adalah metrik yang biasa digunakan untuk mengevaluasi kinerja model pengelompokan. Metrik ini menghitung rasio antara nilai *ground truth* (nilai sebenarnya) dengan nilai prediksi yang positf. Perhitungan rasio ini dijabarkan melalui rumus di bawah ini:

$$ Precision = \frac{TP}{TP + FP} $$

Dimana:

- TP (*True Positive*), jumlah kejadian positif yang diprediksi dengan benar.
- FP (*False Positive*), jumlah kejadian positif yang diprediksi dengan salah.

Berdasarkan hasil yang dikeluarkan berdasarkan tabel 5 dapat dilihat bahwasanya besar presisi jika dihitung adalah 10/10 untuk rekomendasi Top-10. Ini menunjukan sistem mampu memberikan rekomendasi sesuai dengan kategorinya.  

### Pengujian Model *Collaborative Filtering*

Evaluasi metrik yang dapat digunakan untuk mengukur kinerja model ini adalah metrik RMSE (*Root Mean Squared Error*). RMSE adalah metode pengukuran dengan mengukur perbedaan nilai dari prediksi sebuah model sebagai estimasi atas nilai yang diobservasi [^9]. RMSE dapat dijabarkan melalui pendekatan rumus berikut ini

$$ RMSE =  \sqrt{\frac{\sum_{t=1}^{n}(A_t - F_t)^2}{n}} $$

Dimana:

- $A_t$ : Nilai aktual
- $F_t$ : Nilai hasil prediksi
- n: Banyak data

Collaborative Filtering dengan model RecommenderNet memberikan hasil training yang divisualisasikan melalui gambar di bawah ini: 

<p align="center"><img src="https://github.com/Andi-IM/Amazon-Product-Recommendation-System/assets/21165698/f119f22c-b5e5-49bb-9c0d-ab17bd180667"></p>
<p align="center">Gambar 11. Hasil Evaluasi Model RecommenderNet</p>

Dengan epoch sebanyak 100, model ini memberikan nilai error akhir 0.3 untuk training dan 0.19 untuk test. 

## Kesimpulan

Dari hasil evaluasi di atas, maka dapat disimpulkan bahwa:

- Kategori produk yang populer adalah `Electronics`, `Computer&Accessories`, `Home&Kitchen` dengan subkategorinya, `USB Cabels`, `Smartwatches`, `Smartphones`, `SmartTelevisions`, `InEar` dan `RemoteControls` yang berimpikasi bahwa produk-produk pada kategori tersebut merupakan produk yang paling banyak dicari dan dibeli oleh pelanggan.
- Rating yang diberikan terhadap produk terbanyak adalah 4-4.5 yang berarti produk yang ditawarkan memberikan kepuasan bagi pelanggan yang membelinya.
- Secara garis besar, produk yang memilki rating di atas 4 merupakan produk yang berasal dari kategori `OfficeProduk`, `Toys&Games` dan `HomeImprovement` dan jika ditelusur lebih dalam, produk yang memiliki rating di atas 4 rata dari subkategori `Tablets` yang terbanyak.
- Produk dengan jumlah rating yang diberikan akan membuat pelanggan tertarik dan berminat untuk membeli ataupun tidak membeli produk tersebut selain dengan nilai rating itu sendiri.
- Sebagian besar review dari produk yang ditawarkan memiliki sentimen positif.
- Dataset memiliki beberapa data yang hilang dan tidak sesuai dengan tipe datanya sehingga diperlukan perbaikan terlebih dahulu sebelum diproses lebih lanjut.
- Model dengan pendekatan *content-based filtering* memiliki performa yang baik dengan tingkat presisi 100%. Selain itu dengan pendekatan *collaborative filtering* memiliki nilai metrik RMSE 0.3 untuk *training* dan 0.19 untuk *testing*.   

## *References*

[^1]: Henry Februariyanti *"Implementasi Metode Collaborative Filtering untuk Sistem Rekomendasi Penjualan pada Toko Mebel"* 2021, 43-50, doi: [tautan](https://doi.org/10.31294/jki.v9i1.9859.g4873)

[^2]: Esha Alma'arif, dkk. *"Implementasi Algoritma Apriori Untuk Rekomendasi Produk Pada Toko Online"*, Citec Journal, 2020

[^3]: Munawar dkk "Sistem Rekomendasi Hibrid Menggunakan Algoritma Apriori Mining Asosiasi", TEMATIK -Jurnal Teknologi Informasi Dan Komunikasi, 8(1), 69–80. 2021, doi: [tautan](https://doi.org/10.38204/tematik.v8i1.567)

[^4]: Munawar dkk/ *"Meningkatkan Rekomendasi Menggunakan Algoritma Perbedaan Topik"* . J-SIKA| Jurnal Sistem Informasi Karya Anak Bangsa, 02(02), 17–26. Diambil dari [tautan](https://ejournal.unibba.ac.id/index.php/j-sika/article/view/378).

[^5]: Mohamed, Marwa & Khafagy, Mohamed & Ibrahim, Mohamed. (2019). Recommender Systems Challenges and Solutions Survey. 10.1109/ITCE.2019.8646645.

[^6]: Huber, S. (2018). A holistic extension to the CRISP-DM model. Science Direct, (12th CIRP Conference on Intelligent Computation in Manufacturing Engineering, 18-20 July 2018, Gulf of Naples, Italy).

[^7]: C. Chatfield, “Exploratory data analysis,” European Journal of Operational Research, vol. 23, no. 1, pp. 5–13, Jan. 1986, doi: https://doi.org/10.1016/0377-2217(86)90209-2.

[^8]: Laraswati. (2022). Tahapan Data Preparation agar Data Lebih Mudah Diproses, diakses pada tanggal 28 Februari 2024, https://blog.algorit.ma/data-preparation/ 

[^9]: Zach, "How to Interpret Root Mean Square Error (RMSE)" (2021) Diambil dari [tautan](https://www.statology.org/how-to-interpret-rmse/)



