# Proyek Kedua Movies Recommendation System
###### Disusun Oleh : Muhammad Dhoni Apriyadi

## Domain Proyek
### Latar Belakang
Film adalah salah satu media hiburan yang populer di masyarakat. Banyaknya judul-judul yang telah rilis membuat masyarakat kesulitan untuk menemukan film mana yang mereka ingin tonton. Untuk mengatasi masalah tersebut, perlu adanya informasi mengenai film yang akan memudahkan masyarakat untuk menemukan film yang cocok dengan preferensi user, oleh sebab itu user perlu sebuah sistem yang dapat memberikan rekomendasi film. Sistem rekomendasi adalah sistem yang mampu memberikan rekomendasi item-item yang mungkin disukai oleh pengguna. 
Permasalahan yang dapat diselesaikan dalam sistem rekomendasi ini adalah pelanggan dapat dengan mudah mendapatkan rekomendasi film berdasarkan genre dari judul film yang dicari atau yang telah diinput sebelumnya. Metode sistem rekomendasi judul film berdasarkan genre ini menggunakan metode _content-based filtering._ [[1]](https://https://j-ptiik.ub.ac.id/index.php/j-ptiik/article/view/9163)

## Business Understanding

Proyek yang akan dijalankan adalah sistem rekomendasi yang dapat memprediksi judul film yang mungkin pelanggan suka berdasarkan genre dari judul film yang diinput metode yang akan digunakan yaitu teknik _content-based filtering_ dengan _simlarty measure_ yang digunakan adalah _Cosine Similarity_, dengan alur sebagai berikut.

### Problem Statements
Bagaimana memberikan rekomendasi judul film berdasarkan genre pada setiap judul film yang pelanggan input sehingga dapat memberikan referensi yang sesuai pelanggan inginkan?

### Goals
Membuat pelanggan lebih mudah menemukan judul film yang tepat dengan bantuan sistem rekomendasi judul film berdasarkan genre yang dibuat.

### Solution approach
Metode yang digunakan adalah _Content Based Filtering._ _Content Based Filtering_ adalah rekomendasi berbasis konten yang merekomendasikan item yang memiliki kemiripan dengan item yang disukai/di*input* pengguna sebelumnya.

_Content-based filtering_ mempelajari profil minat pengguna baru berdasarkan data dari objek yang telah dinilai pengguna. Metode ini bekerja dengan menyarankan item serupa yang pernah disukai sebelumnya atau sedang dilihat sekarang kepada pengguna berdasrakan kategori tertentu dari item yang dinilai oleh pengguna.

Kelebihan dan Kekurangan dari _Content-based Filtering_
1. Kelebihan
    - _User Independence_ \
    Tidak bergantung kepada user lain dalam memberikan rekomendasi yang ada.
    - _New Item_ \
    Mampu merekomendasikan item yang belum dinilai oleh setiap pengguna.
2. Kekurangan
    - _New User_ \
    Sistem tidak dapat memberikan rekomendasi yang dapat diandalkan pada pengguna baru, karena membutuhkan penelusuran terlebih dahulu pada preferensi pengguna.

## Data Understanding
Pada Proyek kali ini dataset yang digunakan dalam proyek ini merupakan data harga sewa rumah dengan berbagai karakteristik di India. Dataset ini dapat diunduh di [Kaggle The Movies Dataset](https://www.kaggle.com/datasets/rounakbanik/the-movies-dataset) dataset ini merupakan dataset mengenai film yang dirilis pada atau sebelum Juli 2017 yang berisi lebih dari 45.000 film. 26 juta peringkat dari lebih dari 270.000 pengguna.

Di dalam The Movie Dataset datasets ini berisi data Movies Meta Data, credits, links, ratings, dan keywords dengan kolom antara lain sebagai berikut.
- adult : mengkategorikan jenis film dewasa atau tidak
- budget : berisi budget yang digunakan dalam pembuatan film
- genres : berisi kategori genre film
- id : berisi id
- imbd_id : berisi id film
- original_language : berisi bahas yang digunakan
- original_title : berisi judul film
- popularity : berisi popularitas film
- production_companies : berisi produksi film
- ratings : berisi ratings fim
- release_date : berisi waktu rilis film


Variabel-variabel The Movie Dataset yang digunakan adalah sebagai berikut.
- Original_title : Berisi judul asli dari film
- genres : berisi satu atau lebih genre dari setiap judul film 

## Data Preparation
Teknik yang digunakan pada tahapan Data Preparation adalah vektorisasi fungsi CountVectorizer dari library scikit-learn. CountVectorizer digunakan untuk mengubah teks yang diberikan menjadi vektor berdasarkan frekuensi (jumlah) setiap kata yang muncul di seluruh teks. [[2]](https://https://www.academia.edu/40113601/Collaborative_Filtering_Recommender_Systems)

CountVectorizer membuat matriks di mana setiap kata unik diwakili oleh kolom matriks, dan setiap sampel teks dari dokumen adalah baris dalam matriks. Nilai setiap sel tidak lain adalah jumlah kata dalam sampel teks tertentu.

Pada proses vektorisasi ini, digunakan metode sebagai berikut. 
1. fit metode berfungsi untuk melakukan perhitungan idf pada data
2. get_feature berfungsi untuk melakukan mapping array dari fitur index integer ke fitur nama
3. fit_transform berfungsi untuk mempelajari kosa kata dan Inverse Document Frequency (IDF) dengan memberikan nilai return berupa *document-term matrix*
4. todense berfungsi untuk mengubah vektor tf-idf dalam bentuk matriks

## Modeling
Model machine learning yang digunakan pada sistem rekomendasi ini adalah model _content-based filtering_ dengan _simlarty measure_ yang digunakan adalah _Cosine Similarity_.

Model _content-based filtering_ ini bekerja dengan mempelajari profil minat pengguna baru berdasarkan data dari objek yang telah dinilai pengguna. Metode ini bekerja dengan menyarankan item serupa yang pernah disukai sebelumnya atau sedang dilihat sekarang kepada pengguna berdasrakan kategori tertentu dari item yang dinilai oleh pengguna dengan menggunakan _similarity_ tertentu.

Sedangkan _cosine similarity_ adalah salah satu teknik mengukur kesamaan yang bekerja dengan mengukur kesamaan antara dua vektor dan menentukan apakah kedua vektor tersebut menunjuk ke arah yang sama dengan menghitung sudut cosinus antara dua vektor. Semakin kecil sudut cosinus, semakin besar nilai _cosine similarity_.

Dalam pemanggilan rekomendasi judul film digunakan function yang dibuat dengan code sebagai berikut.

Sebuah sistem rekomendasi berdasarkan judul film  ini bekerja dengan memberikan rekomendasi berdasarkan kemiripan atribut dari item atau barang yang disukai. Kemudian mengambil skor  dan mengurutkannya berdasarkan kemiripan dengan judul film yang diinputkan. Selanjutnya, Sistem akan mengurutkan 10 skor kemiripan dengan  urutan *index* dari 1-10 dan sistem akan menampilkan 10 rekomendasi berdasarkan skor *index* tersebut.


 Berikut adalah tahapan yang dilakukan pada fungsi tersebut sebagai berikut.
1. Mengambil indeks dari judul film yang telah didefinisikan sebelumnnya
2. Mengambil skor kemiripan dengan semua film
3. Mengurutkan film berdasarkan skor kemiripan
4. Mengambil 10 skor kemiripan dari 1-10 karena urutan 0 memberikan indeks yang sama dengan judul film yang diinput
5. Mengambil judul film dari skor kemiripan
6. Mengembalikan 10 rekomendasi judul film dari kemiripan skor yang telah diurutkan dan menampilkan genre dari 10 rekomendasi film tersebut

Berikut _top_-10 _recommemdation_ berdasarkan genre dari judul film "*The American President*"
    
        judul                       genre
        The American President	    [Comedy, Drama, Romance]

Rekomendasi film

        judul	                    genre
    0	Nueba Yol	                [Comedy, Drama, Romance]
    1	飲食男女	                [Comedy, Drama, Romance]
    2	Only You	                [Comedy, Drama, Romance]
    3	Muriel's Wedding	        [Drama, Comedy, Romance]
    4	The Favor	                [Drama, Comedy, Romance]
    5	The Inkwell	                [Comedy, Drama, Romance]
    6	Meet John Doe	            [Drama, Comedy, Romance]
    7	The Pompatus of Love	    [Comedy, Romance, Drama]
    8	Jerry Maguire	            [Comedy, Drama, Romance]
    9	Roseanna's Grave	        [Comedy, Romance, Drama]

Dari hasil yang diberikan di atas berdasarkan judul film "*The American President*" dengan genre [Comedy, Drama, Romance] di dapatkan 10 rekomendasi judul film dengan genre yang serupa ataupun mirip.

## Evaluation
*Metric* yang digunakan pada sistem rekomendasi judul film berdasarkan genre adalah *accuracy precision*. *Precision* adalah metrik yang membandingkan rasio prediksi benar atau positif dengan keseluruhan hasil yang diprediksi positif dengan rumus
        
    Precission = (TP) / (TP+FP).
        
    keterangan:
    TP = True Positif (prediksi positif dan hal tersebut benar)
    FP = False Negatif (prediksi positif dan hal tersebut salah)

Alasan _accuracy Precision_ dipilih adalah karena metrik ini dapat membandingkan rasio prediksi benar atau positif dengan keseluruhan hasil yang diprediksi positif. Dalam hal ini adalah rasio item yang direkomendasikan memiliki genre yang mirip atau serupa dibandingkan dengan genre dari judul film yang diinput.



Dari output tersebut dihitung _accuracy precision_ nya adalah
```py
#jumlah prediksi benar untuk genre yang mirip atau serupa
TP = 10

#jumlah prediksi salah untuk genre yang mirip atau serupa
FP = 0 

Precision = TP/(TP+FP)
print("{0:.0%}".format(Precision))
```
_output_

        100%

### Kesimpulan 
Dari model yang telah dibangun bahwasannya model yang dibangun telah berjalan dengan baik dan dapat menampilkan rekomendasi yang sangat mirip atau serupa dengan genre dari judul yang diinputkan. Dari Uji atau evaluasi model juga dapat dilihat bahwasannya model menampilkan prediksi 10 indeks film berdasarkan genre yang sangat sesuai atau serupa dengan film yang pernah ditonton oleh pengguna. Akan tetapi, Model yang digunakan masih terdapat sedikit kelemahan sehingga memang masih perlu dikaji ulang. Salah satunya adalah tidak dapat memberikan saran atau rekomendasi kepada pengguna baru yang belum menonton karena model hanya mengandalkan saran melalui film yang telah ditonton oleh pengguna.

## Referensi 
[1] Fajriansyah, M., Adikara, P., & Widodo, A. Sistem Rekomendasi Film Menggunakan Content Based Filtering. Jurnal Pengembangan Teknologi Informasi dan Ilmu Komputer, vol. 5, no. 6, p. 2188-2199, mei 2021. ISSN 2548-964X. 

[2]Schafer, J.B., Frankowski, D.,Herlocker,J. dan Sen, S. “Collaborative Filtering Recommender System”. Springer-Verlag, Berlin, Heidelbeg, 2007