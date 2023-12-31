# House-Rental-Price-Prediction

#### Disusun oleh : Dian Rizqi Saputra

Selamat datang di proyek House Rental Price Prediction, sebuah inisiatif untuk membangun masa depan yang lebih cerdas dan efisien dalam industri real estat. Mengembangkan model machine learning yang dapat memprediksi harga sewa rumah dan apartemen dengan akurasi yang cukup baik.

## Domain Proyek

### Latar Belakang

Tempat tinggal seperti rumah atau apartemen adalah kebutuhan primer bagi manusia untuk berlindung dan hidup menetap. Tempat tinggal ini memiliki nilai tergantung dari karakteristik yang dimiliki seperti lokasi, luas, jumlah kamar, jumlah kamar mandi, perabotan, serta fitur lainnya.

<br>

<div><img src="https://i.pinimg.com/originals/30/b1/92/30b1926a95ac6b820690458e848e8162.jpg" width="1000"/></div>

[Referensi gambar](https://pinterest.com)

<br>

Harga dari setiap rumah diukur dari nilai yang dimiliki oleh rumah tersebut. Namun, harga ini tidak selalu pasti dan sulit untuk melakukan prediksi akurat secara manual. Faktor ketidakpastian perlu dikurangi oleh perusahaan sewa dengan membangun sistem prediksi yang dapat menentukan berapa harga sewa yang pantas untuk karakteristik rumah tertentu.

Dalam mencapai hal tersebut, maka dilakukan penelitian untuk memprediksi harga sewa rumah menggunakan model machine learning. Diharapkan model ini mampu memprediksi harga sewa yang sesuai dengan harga pasar. Prediksi ini nantinya dijadikan acuan bagi perusahaan dalam menyewa rumah dengan harga yang dapat mendatangkan profit bagi perusahaan.

Referensi : [Analisis Prediksi Harga Rumah Sesuai Spesifikasi Menggunakan Multiple Linear Regression](https://ejournal.upnvj.ac.id/index.php/informatik/article/download/3635/1498)

## Business Understanding

Proyek ini dibangun untuk perusahaan dengan karakteristik bisnis sebagai berikut :

+ Perusahaan memiliki atau membeli rumah dan apartemen kemudian menyewanya ke konsumen.
+ Perusahaan membuka jasa konsultasi harga sewa rumah dan apartemen ke konsumen.

### Problem Statement

1. Fitur apa yang paling berpengaruh terhadap harga sewa rumah atau apartemen?
2. Bagaimana cara memproses data agar dapat dilatih dengan baik oleh model?
3. Berapa harga sewa rumah di pasaran berdasarkan karakteristik tertentu?

### Goals

1. Mengetahui fitur yang paling berpengaruh pada harga sewa rumah atau apartemen.
2. Melakukan persiapan data untuk dapat dilatih oleh model.
3. Membuat model machine learning yang dapat memprediksi harga sewa rumah seakurat mungkin berdasarkan karakteristik tertentu.

### Solution Statement

1. Menganalisis data dengan melakukan univariate analysis dan multivariate analysis. Memahami data juga dapat dilakukan dengan visualisasi. Memahami data dapat membantu untuk mengetahui kolerasi antar fitur dan mendeteksi outlier.
2. Menyiapkan data agar bisa digunakan dalam membangun model.
3. Melakukan hyperparameter tuning menggunakan grid search dan membangun model regresi yang dapat memprediksi bilangan kontinu. ALgoritma yang dipakai dalam proyek ini adalah K-Nearest Neighbour, Random Forest, dan AdaBoost.

## Data Understanding & Removing Outlier

Dataset yang digunakan dalam proyek ini merupakan data harga sewa rumah dengan berbagai karakteristik di India. Dataset ini dapat diunduh di [Kaggle : House Rent Prediction Dataset](https://www.kaggle.com/datasets/iamsouravbanerjee/house-rent-prediction-dataset).

Berikut informasi pada dataset :

+ Dataset memiliki format CSV (Comma-Seperated Values).
+ Dataset memiliki 4746 sample dengan 12 fitur.
+ Dataset memiliki 4 fitur bertipe int64 dan 8 fitur bertipe object.
+ Tidak ada missing value dalam dataset.

### Variable - variable pada dataset

+ Posted On: Tanggal data diposting.
+ BHK: Jumlah dari kamar tidur, aula, dan dapur.
+ Rent: Harga sewa dari rumah/apartemen.
+ Size: Luas dari rumah/apartemen dalam square feet (sqft).
+ Floor: Letak dan jumlah lantai rumah/apartemen.
+ Area Type: Ukuran dari rumah dalam kategori Super Area atau Carpet Area atau Build Area.
+ Area Locality: Lokasi rumah/apartemen.
+ City: Kota dimana rumah/apartemen berada.
+ Furnishing Status: Status perabotan rumah/apartemen, baik Furnished atau Semi-Furnished atau Unfurnished.
+ Tenant Preferred: Jenis penyewa yang diutamakan pemilik atau agen.
+ Bathroom: Jumlah kamar mandi.
+ Point of Contact: Kontak yang dihubungi untuk informasi lebih lanjut mengenai rumah/apartemen.

Dari ke 12 fitur dapat dilihat bahwa fitur Point of Contract dan Posted On tidak mempengaruhi harga sewa rumah sehingga akan dihapus. Hal ini dikarenakan kedua fitur tersebut tidak diperlukan dalam membangun model prediksi harga sewa.

### Univariate Analysis

Univariate Analysis adalah menganalisis setiap fitur secara terpisah.

#### Analisis jumlah nilai unique pada setiap fitur kategorik

Fitur kategorik City, Furnishing Status, dan Tenant Preferred memiliki sebaran sample yang cukup merata.
<div><img src="https://github.com/dianrizqisaputra/House-Rental-Price-Prediction/assets/91761759/f0ae7504-5206-4859-89f5-29f283381e60" width="220"/></div> <div><img src="https://github.com/dianrizqisaputra/House-Rental-Price-Prediction/assets/91761759/28b7171a-d732-4242-9df4-73cbc858400a" width="220"/></div> <div><img src="https://github.com/dianrizqisaputra/House-Rental-Price-Prediction/assets/91761759/b3bf8945-1ca2-4b6e-8a18-d74b9e7a77f9" width="220"/></div><br />

Berikut adalah fitur dengan sample yang tidak merata :

+ Area Type
  <div><img src="https://github.com/dianrizqisaputra/House-Rental-Price-Prediction/assets/91761759/8dfe8049-457c-4c31-8a7b-a11c8c6112f9" width="220"/></div>
  Hanya terdapat 2 sample Built Area pada fitur Area Type. Untuk menghindari high dimensional data, maka kedua sample ini akan dihapus.

+ Floor dan Area Locality
  <div><img src="https://github.com/dianrizqisaputra/House-Rental-Price-Prediction/assets/91761759/eddb89f7-6bd7-4051-99a3-5239a98af408" width="220"/></div>
   <div><img src="https://github.com/dianrizqisaputra/House-Rental-Price-Prediction/assets/91761759/ec4849d7-a95a-49bf-9ee6-8958674b0e8d" width="220"/></div>
  Fitur Floor dan Area Locality memiliki banyak sekali nilai unique. Untuk menghindari high dimensional data, maka kedua fitur ini akan dihapus.

#### Analisis sebaran pada setiap fitur numerik

<div><img src="https://github.com/dianrizqisaputra/House-Rental-Price-Prediction/assets/91761759/d8f1cb01-7726-4239-b32f-b6edfc097b6e" width="450"/></div><br />
Berikut analisis dari grafik di atas :

+ Sebagian besar rumah memiliki 1 sampai 3 BHK dan 1 sampai 3 kamar mandi.
+ Sebagian besar rumah memiliki luas di bawah 2000 sqft.
+ Rentang harga sewa cukup tinggi, yaitu dari 1200 hingga 3500000. Namun, rata-rata harga rumah hanya 35003. Distribusi harga yang kurang bagus seperti ini dapat berimplikasi pada model.

### Multivariate Analysis

Multivariate Analysis menunjukkan hubungan antara dua atau lebih fitur dalam data.

#### Analisis fitur numerik

+ Fitur Size dan BHK (Menghapus BHK Outlier)
  Kedua fitur ini dianalisis karena tidak biasa untuk rumah dengan 1 BHK memiliki luas 100 sqft. Untuk itu ditentukan treshold atau batas 300 sqft/bhk. Data yang berada di bawah batas akan dihapus. Hal ini menyebabkan berkurangnya jumlah sample sebesar 548.

+ Fitur Size dan Rent (Menghapus Price per sqft Outlier)
  Untuk memudahkan dalam mendeteksi outlier, maka dibuat fitur baru 'Price_per_sqft' dari kedua fitur tersebut untuk menganalisis harga sewa per luas sqft.
  <div><img src="https://github.com/dianrizqisaputra/House-Rental-Price-Prediction/assets/91761759/6f3b04f4-ca21-4935-a590-bcd698bde6ed" width="220"/></div>
  Dari sini dapat terlihat bahwa harga 571 per sqft sangat rendah dan harga 1400000 per sqft sangat tinggi. Untuk itu penghapusan outlier price per sqft outlier dengan mean dan one standard deviation yang telah dikelompokkan berdasarkan kota. Hal ini menyebabkan berkurangnya jumlah sample sebesar 497.

+ Fitur Bathroom dan BHK (Menghapus Bathroom Outlier)
  Kedua fitur ini dianalisis karena tidak biasa untuk rumah dengan 2 BHK memiliki 4 kamar mandi. Untuk itu ditentukan batas bahwa jumlah kamar mandi tidak boleh melebihi jumlah BHK + 2. Hal ini menyebabkan berkurangnya sample sebesar 3.
  
+ Melihat kolerasi antara semua fitur numerik
  <div><img src="https://github.com/dianrizqisaputra/House-Rental-Price-Prediction/assets/91761759/6daf094b-f719-459d-85d0-f10f33b1d854" width="350"/></div>
  Fitur BHK, Size, dan Bathroom berkorelasi tidak signifikan dengan fitur target (Rent). Hal ini mungkin   disebabkan oleh kurangnya data dalam penelitian ini.Fitur BHK dan Bathroom berkolerasi signifikan dengan fitur size. Hal ini sudah sesuai harapan dari penghapusan outlier yang sudah dilakukan sebelumnya.

#### Analisis fitur kategorik

Analisis ini dilakukan untuk melihat kolerasi antara fitur kategorik dengan fitur target (Rent).

+ Fitur Area Type
  <div><img src="https://github.com/dianrizqisaputra/House-Rental-Price-Prediction/assets/91761759/4d441369-da97-47b6-823d-8c0f8cb29e3e" width="500"/></div>
  Fitur Area Type memiliki pengaruh yang kecil terhadap rata-rata harga sewa.

+ Fitur City
  <div><img src="https://github.com/dianrizqisaputra/House-Rental-Price-Prediction/assets/91761759/6d512542-5e34-48b3-a7dd-a236ef565266" width="500"/></div>
  Fitur City memiliki pengaruh cukup besar terhadap rata-rata harga sewa, terutama jika rumah berada di kota Mumbai. Hal ini dibuktikan dengan sebaran rumah yang mencapai harga tertinggi di kota Mumbai. Mumbai merupakan kota paling mahal di India untuk ditinggali, diikuti dengan Delhi.

  Referensi : [Ini Adalah Kota Termahal Untuk Hidup Di India](https://id.yourtripagent.com/these-are-most-expensive-cities-to-live-in-india-4734)

+ Fitur Furnishing Status
  <div><img src="https://github.com/dianrizqisaputra/House-Rental-Price-Prediction/assets/91761759/82a75a20-b797-4598-b3fd-cbf1dbc5166a" width="500"/></div>
  Fitur Furnishing Status memiliki pengaruh cukup besar terhadap rata-rata harga sewa. Merupakan hal biasa bila rumah yang memiliki perabotan lengkap akan diberi harga sewa lebih tinggi daripada rumah tanpa perabotan.

+ Fitur Tenant Preferred
  <div><img src="https://github.com/dianrizqisaputra/House-Rental-Price-Prediction/assets/91761759/48c23012-665d-49c8-a175-cc0ab705736e" width="500"/></div>
  Fitur Tenant Preferred memiliki pengaruh yang lumayan terhadap rata-rata harga sewa. Dari grafik dapat terlihat bahwa rumah yang sangat disarankan untuk disewa oleh keluarga memiliki rata-rata harga sewa yang lebih mahal dibanding lainnya.

## Data preparation

+ One Hot Encoding

  One hot encoding adalah teknik mengubah data kategorik menjadi data numerik dimana setiap kategori menjadi kolom baru dengan nilai 0 atau 1. Fitur yang akan diubah menjadi numerik pada proyek ini adalah Area Type, City, Furnishing Status, dan Tenant Preferred.
  
+ Train Test Split

  Train test split aja proses membagi data menjadi data latih dan data uji. Data latih akan digunakan untuk membangun model, sedangkan data uji akan digunakan untuk menguji performa model. Pada proyek ini dataset sebesar 3696 dibagi menjadi 3511 untuk data latih dan 185 untuk data uji.
  
+ Normalization

  Algoritma machine learning akan memiliki performa lebih baik dan bekerja lebih cepat jika dimodelkan dengan data seragam yang memiliki skala relatif sama. Salah satu teknik normalisasi yang digunakan pada proyek ini adalah Standarisasi dengan sklearn.preprocessing.StandardScaler.

## Modeling

+ Algoritma
  Penelitian ini melakukan pemodelan dengan 3 algoritma, yaitu K-Nearest Neighbour, Random Forest, dan
  + K-Nearest Neighbour
    K-Nearest Neighbour bekerja dengan membandingkan jarak satu sampel ke sampel pelatihan lain dengan memilih sejumlah k tetangga terdekat. Proyek ini menggunakan [sklearn.neighbors.KNeighborsRegressor](https://scikit-learn.org/stable/modules/generated/sklearn.neighbors.KNeighborsRegressor.html) dengan memasukkan X_train dan y_train dalam membangun model. Parameter yang digunakan pada proyek ini adalah :
    + `n_neighbors` = Jumlah k tetangga tedekat.

  + Random Forest
    Algoritma random forest adalah teknik dalam machine learning dengan metode ensemble. Teknik ini beroperasi dengan membangun banyak decision tree pada waktu pelatihan. Proyek ini menggunakan [sklearn.ensemble.RandomForestRegressor](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestRegressor.html) dengan memasukkan X_train dan y_train dalam membangun model. Parameter yang digunakan pada proyek ini adalah :
    + `n_estimators` = Jumlah maksimum estimator di mana boosting dihentikan.
    + `max_depth` = Kedalaman maksimum setiap tree.
    + `random_state` = Mengontrol seed acak yang diberikan pada setiap base_estimator pada setiap iterasi boosting.

  + Adaboost
    AdaBoost juga disebut Adaptive Boosting adalah teknik dalam machine learning dengan metode ensemble.  Algoritma yang paling umum digunakan dengan AdaBoost adalah pohon keputusan (decision trees) satu tingkat yang berarti memiliki pohon Keputusan dengan hanya 1 split. Pohon-pohon ini juga disebut Decision Stumps. Algoritma ini bertujuan untuk meningkatkan performa atau akurasi prediksi dengan cara menggabungkan beberapa model sederhana dan dianggap lemah (weak learners) secara berurutan sehingga membentuk suatu model yang kuat (strong ensemble learner). Proyek ini menggunakan [sklearn.ensemble.AdaBoostRegressor](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.AdaBoostRegressor.html) dengan memasukkan X_train dan y_train dalam membangun model. Parameter yang digunakan pada proyek ini adalah :
    + `n_estimators` = Jumlah maksimum estimator di mana boosting dihentikan.
    + `learning_rate` = Learning rate memperkuat kontribusi setiap regressor.
    + `random_state` = Mengontrol seed acak yang diberikan pada setiap base_estimator pada setiap iterasi boosting.

+ Hyperparameter Tuning (Grid Search)
  Hyperparameter tuning adalah cara untuk mendapatkan parameter terbaik dari algoritma dalam membangun model. Salah satu teknik dalam hyperparameter tuning yang digunakan dalam proyek ini adalah grid search. Berikut adalah hasil dari Grid Search pada proyek ini :
  | model    | best_params                                                     |
  |----------|-----------------------------------------------------------------|
  | knn      | {'n_neighbors': 7}                                              |
  | boosting | {'learning_rate': 0.1, 'n_estimators': 100, 'random_state': 11} |
  | rf       | {'max_depth': 8, 'n_estimators': 25, 'random_stste': 11}        |

## Evaluation

Metrik evaluasi yang digunakan pada proyek ini adalah akurasi dan mean squared error (MSE). Akurasi menentukan tingkat kemiripan antara hasil prediksi dengan nilai yang sebenarnya (y_test). Mean squared error (MSE) mengukur error dalam model statistik dengan cara menghitung rata-rata error dari kuadrat hasil aktual dikurang hasil prediksi. Berikut formulan MSE :
<div><img src="https://github.com/dianrizqisaputra/House-Rental-Price-Prediction/assets/91761759/b73a76c6-7339-495e-b108-ab1c9f211125" width="300"/></div>

Berikut hasil evaluasi pada proyek ini :

+ Akurasi
  | model    | accuracy |
  |----------|----------|
  | knn      | 0.726775 |
  | boosting | 0.898556 |
  | rf       | 0.932057 |

+ Mean Squared Error (MSE)
  <div><img src="https://github.com/dianrizqisaputra/House-Rental-Price-Prediction/assets/91761759/b17c1bb5-5323-490b-871f-de1c001b83df" width="300"/></div>

Dari hasil evaluasi dapat dilihat bahwa model dengan algoritma Random Forest memiliki akurasi lebih tinggi tinggi dan tingkat error lebih kecil dibandingkan algoritma lainnya dalam proyek ini.
