# CapstoneProjectM3_BankMarketingCampaign

# Table of Content
0. Import Libraries
1. Business Problem Understanding
2. Data Understanding
3. Exploratory Data Analysis (EDA)
4. Data Cleaning
5. Data Analysis
6. Modeling
7. Conclusion & Recommendation

# **`Business Problem Understanding`**
### **Context**

*Bank Marketing Campaign* merupakan strategi penting untuk meningkatkan jumlah nasabah dan keuntungan. Dalam konteks ini, fokus pada hasil dari campaign yang telah dilakukan dari tim marketing yang nantinya akan membantu kita memahami pola perilaku nasabah terkait keputusan untuk melakukan deposit. Upaya untuk menarik nasabah baru atau meningkatkan hubungan dengan nasabah yang sudah ada melalui berbagai saluran komunikasi, seperti seluler dan telepon. 

### **Problem Statement**

Bank ABC memiliki strategi untuk membuat para nasabahnya agar melakukan deposit dengan cara melakukan campaign. Namun, hasil dari campaign tersebut belum memberikan hasil yang memuaskan dikarenakan masih banyak nasabah yang belum tertarik untuk melakukan deposit. Oleh karena itu, Tim Marketing dari sebuah Bank ABC ingin membuat sistem yang dapat membantu dalam memprediksi apakah nasabah akan melakukan deposit atau tidak. 
Selain itu Bank ABC juga ingin memimalisir kesalahan prediksi terhadap nasabah yang aktualnya tidak deposit namun diprediksi deposit. Hal tersebut bertujuan untuk mengoptimalkan biaya pengeluaran campaign yang akan dilakukan kedepannya agar lebih efektif dan efisien.

### **Goals**

Dari permasalahan tersebut, tim marketing bertujuan untuk mengidentifikasi perilaku nasabah yang tertarik untuk melakukan deposito. Dengan demikian, upaya campaign dapat lebih efektif dengan diarahkan kepada nasabah yang memiliki potensi tinggi untuk melakukan penyetoran deposito. Untuk mencapai tujuan ini, bank akan menerapkan model machine learning yang mampu memprediksi kecenderungan nasabah untuk menyetorkan deposito. Hasil dari model ini akan memungkinkan bank untuk menargetkan segmen nasabah yang tepat, sehingga meningkatkan efisiensi dan keberhasilan kampanye marketing deposito berjangka (term deposit).

### **Analytics Approach**

Sebagai *Strategic Marketing Analyst*, yang akan kita lakukan yaitu membangun model yang dapat memprediksi apakah seorang nasabah akan melakukan deposit berdasarkan data dari *bank marketing campaign*. Dengan memahami faktor-faktor yang berpengaruh, tim marketing dapat mengarahkan strategi mereka secara lebih efektif dan meminimalisir biaya marketing. Dengan dataset yang kita punya, kita dapat  menganalisis informasi-informasi mengenai karakteristik nasabah yang melakukan deposit atau tidak. Selanjutnya, kita dapat menganalisis informasi tersebut dan dapat dilakukan pemodelan untuk Machine Learning nya.

### **Metrics Evaluation**

Karena fokus utama kita adalah nasabah yang tidak melakukan deposit, maka target yang kita tetapkan adalah sebagai berikut:

- 0 = Nasabah Deposit
- 1 = Nasabah Tidak Deposit

Type 1 error : False Positive (nasabah yang aktualnya deposit tetapi diprediksi tidak deposit)\
Konsekuensi: tidak efektifnya pemberian campaign

Type 2 error : False Negative (nasabah yang aktualnya tidak deposit tetapi diprediksi deposit)\
Konsekuensi: kehilangan nasabah

 Bank ingin berhasil memprediksi apakah nasabah akan melakukan deposit atau tidak, namun disini kita juga ingin meminimalisir kesalahan pada nasabah yang aktualnya tidak deposit namun diprediksi deposit. Hal tersebut juga dapat meminimalisir pengeluaran biaya terhadap machine learning dan memberikan keuntungan dari bertambahnya nasabah yang melakukan deposit.

Sebagai contoh gambaran untuk melihat dampaknya, mari kita hitung biaya yang timbul berdasarkan asumsi berikut:

 - Jumlah yang tidak melakukan deposito: 4081 nasabah
 - Jumlah yang melakukan deposito: 3.732 nasabah 
 - Rata-rata biaya campaign marketing bank adalah 3.65% dari pendapatan [(sumber)](https://emiboston.com/leading-u-s-banks-boosted-marketing-spend-in-2022/)
 - Setoran minimum melakukan deposito per nasabah sekitar $1000 [(sumber)](https://www.forbes.com/advisor/banking/bank-account-minimum-deposit-minimum-balance-requirements/)
 - Rata-rata suku bunga deposito: 5,36% [(sumber)](https://www.bankrate.com/banking/cds/cd-rates/)
 - Rata-rata suku bunga pinjaman: 8,5% [(sumber)](https://www.ceicdata.com/en/indicator/united-states/bank-lending-rate#:~:text=United%20States%20Bank%20Lending%20Rate%20was%20reported%20at%208.500%20%25%20pa,May%202024%2C%20with%2025130%20observations.)
 - Dengan demikian, pendapatan dari Deposit 3.732 x $1.000 = $3.732.000
 - Biaya marketing campaign adalah 1% dari $3.732.000, yaitu $37.320

Biaya campaign per nasabah:
$$\ \text{Biaya Campaign per Nasabah} = \frac{Total Biaya Campaign}{Total Nasabah} \$$
$$\ \text{Biaya Campaign per Nasabah} = \frac{37320}{7813} = \text {4.77}\ \$$

Profit per nasabah:
$$\ \text{Profit per Nasabah} = \frac{\text{Pendapatan Deposito - Biaya Campaign}}{\text{Total Nasabah yang Deposit}} \$$
$$\ \text{Profit per Nasabah} = \frac{\text{200035 - 37320}}{\text{3732}} = \text {43.59}\ \$$

 - Biaya Campaign per nasabah: **$ 4,77** 
 - Profit per nasabah: **$ 43,59** 

Dalam evaluasi metrik untuk pengolahan data marketing campaign bank ini, F1 Score menjadi tolok ukur yang penting. Dalam konteks ini, F1 Score mengukur keseimbangan antara presisi (keakuratan prediksi positif) dan recall (ketepatan deteksi) dalam mengidentifikasi calon nasabah yang kemungkinan besar akan melakukan deposito. Dengan menggunakan F1 Score, bank dapat mengevaluasi model machine learning mereka dengan lebih baik, mengoptimalkan efisiensi marketing campaign, dan meningkatkan kesuksesan dalam menarik nasabah potensial untuk melakukan deposito.


# **`Data Understanding`**

- Dataset menggambarkan 7.800 data nasabah.
- Setiap baris merepresentasikan informasi/karakteristik dari individu seperti usia, profesi, saldo, dan lainnya beserta informasi apakah marketing campaign yang dilakukan berhasil atau tidak.

### **Informasi Kolom**

Dataset ini memiliki 7813 baris dan 11 kolom, dimana tiap barisnya menampilkan data informasi nasabah yang melakukan Term Deposit (deposito berjangka) kepada bank. 

**Profil Nasabah:**
| Kolom | Tipe Data | Deskripsi |
| --- | --- | --- | 
|`age` |Integer | Umur nasabah |
|`job` |Text | Profesi nasabah |
|`balance` |Integer | Saldo nasabah |
|`housing` |Text | Pinjaman KPR (cicilan rumah) |
|`loan` |Text | Pinjaman selain KPR |

**Data Bank (marketing):**
| Kolom | Tipe Data | Deskripsi |
| --- | --- | --- | 
|`contact` |Text | Jenis kontak komunikasi dengan nasabah |
|`month` |Text | Bulan terakhir komunikasi dengan nasabah |
|`campaign` |Integer | Jumlah kontak untuk campaign yang diberikan kepada nasabah |
|`pdays` |Integer | Jumlah hari setelah nasabah dihubungi dari campaign sebelumnya |
|`poutcome` |Text | Hasil dari marketing campaign sebelumnya |

**Hasil/Target:**
| Kolom | Tipe Data | Deskripsi |
| --- | --- | --- | 
|`deposit` |Text | Nasabah melakukan deposit atau tidak |

Informasi (range dan nilai unik) pada Feature dataset:
- **age**: 18 s/d 95 tahun 
- **balance**: -$6,847 s/d $66,653
- **campaign**: 1 s/d 63 kali
- **pdays**: -1 s/d 854 hari
- **job**: admin, self-employed, services, housemaid, technician, management, student, blue-collar, entrepreneur, retired, unemployed, unknwon
- **housing**: yes, no   
- **loan**: yes, no
- **contact**: cellular, telephone, unknown
- **month**: jun, apr, may, nov, jan, sep, feb, mar, aug, jul, oct, dec
- **iscontact**: yes, no
- **poutcome**: success, failure, other, unknown
- **deposit**: yes, no


## **Data Preparation**

>**Handling Outliers**

- Untuk handling outliers pada kolom `age`, `balance`, dan `campaign` nantinya akan kita coba menggunakan `winsorizing` agar mempertahankan distribusi data dan mengurangi dampak dari nilai ekstrem yang dapat mendistorsi model machine learning
- Pada proses ini kita menggunakan winsorizer, dikarenakan Winsorisasi atau winorization merupakan transformasi statistik dengan membatasi nilai ekstrem dalam data statistik untuk mengurangi pengaruh kemungkinan outlier palsu. [Sumber](https://en.wikipedia.org/wiki/Winsorizing)

>**Encoding**

- Nantinya kita akan melakukan encoding pada kolom housing, loan, contact, iscontacted, dan poutcome menggunakan `One Hot Encoding` karena fitur-fitur tersebut tidak memiliki urutan/tidak ordinal, dan juga jumlah unique datanya hanya sedikit
- untuk kolom job menggunakan `Binary Encoding`, karena fitur ini tidak memiliki urutan/tidak ordinal, namun jumlah unique datanya banyak
- untuk kolom month menggunakan `Ordinal Encoding`, karena fitur ini memiliki urutan.

>**Scaling**

- Kita akan menggunakan `Robust Scaler` karena data kita memiliki outlier dan Robust Scaler tidak akan terpengaruh oleh outlier. Kita dapat mengatur ulang scaler nantinya untuk mendapatkan scaler terbaik.

>**Balance Data**

- Seperti yang sudah kita ketahui, proporsi target pada dataset ini sudah cukup seimbang (balance), hal tersebut memudahkan kita untuk proses kedepannya. Kita tidak ada kebutuhan mendesak untuk melakukan oversampling maupun undersampling.


# **`Modeling`**

- Terlampir pada File


# **`Conclusion & Recommendation`**

#### **Conclusion**

>**Model**

- Metric utama yang kita guanakan adalah f1_score, karena kita mementingkan nilai rata-rata harmonik dari hasil akurasi recall dan precision,
- Berdasarkan hyperparameter tuning, parameter terbaik yang dapat digunakan untuk benchmark model GradientBoostingClassifier adalah :
    - {model__n_estimators': 100, 'model__min_samples_split': 10, 'model__min_samples_leaf': 4, 'model__max_features': 'sqrt', 'model__max_depth': 6, 'model__learning_rate': 0.001}
- Berdasarkan Feature Importance yang dihasilkan oleh model, berikut merupakan feature yang penting untuk model ini:
    - poutcome
    - contact
    - month
    - housing
    - age
    - iscontacted (pdays)
    - balance
    - campaign
- Model berhasil meminimalisir kesalahan prediksi terhadap nasabah yang diprediksi deposit padahal aktualnya tidak deposit. 

>**Interpretation Result**
 - **poutcome**: Nasabah yang berhasil dalam campaign sebelumnya lebih mungkin melakukan deposit saat ini, menunjukkan pentingnya data historis.
 - **contact**: Metode kontak selain telepon atau seluler mengurangi kemungkinan deposit, menekankan pentingnya metode kontak yang efektif.
 - **housing**: Nasabah dengan pinjaman perumahan juga sedikit lebih mungkin melakukan deposit, mungkin karena kebutuhan pengelolaan keuangan yang lebih hati-hati.
 - **loan**: Nasabah dengan pinjaman pribadi sedikit kurang mungkin melakukan deposit, menunjukkan beban finansial yang mengurangi kemampuan menambah deposit.
 - **iscontacted**: Nasabah yang belum pernah dihubungi lebih mungkin melakukan deposit, menunjukkan efektivitas targeting nasabah baru.
 - **balance**: Nasabah dengan saldo tinggi sedikit kurang mungkin melakukan deposit, mungkin karena merasa sudah memiliki cukup dana.
 - **month**: Campaign antara Juni dan Agustus lebih mungkin berhasil, menunjukkan waktu tertentu dalam setahun lebih kondusif untuk campaign.

>**Cost Benefit Result**

 **Type I**

 - **Tanpa Model**: Biaya campaign yang dihabiskan untuk nasabah yang tidak melakukan deposit adalah $3544.11.
 - **Dengan Model**: Biaya yang terbuang untuk campaign berkurang menjadi $1826.91.
 - **Pengurangan Biaya**: Menggunakan model mengurangi biaya campaign yang terbuang sebesar $1717.20, yang setara dengan pengurangan biaya sekitar 48.50%.

 **Type II**

 - **Tanpa Model**: Potensi kerugian keuntungan dari nasabah yang tidak melakukan deposit adalah $32,387.37.
 - **Dengan Model**: Potensi kerugian berkurang menjadi $15,692.40.
 - **Pengurangan Biaya**: Menggunakan model mengurangi potensi kerugian keuntungan sebesar $16,694.97, yang setara dengan pengurangan biaya sekitar 51.54%.

>**Model Limitiation**

 Feature yang valid dalam model ini:
 - **age**: 22 sampai dengan 77 tahun 
 - **balance**: 0 sampai dengan $13,578
 - **campaign**: 1 sampai dengan 13 kali
 - **job**: admin, self-employed, services, housemaid, technician, management, student, blue-collar, entrepreneur, retired, unemployed
 - **housing**: yes, no   
 - **loan**: yes, no
 - **contact**: cellular, telephone, unknown
 - **month**: jun, apr, may, nov, jan, sep, feb, mar, aug, jul, oct, dec
 - **iscontacted**: yes, no
 - **poutcome**: success, failure, unknown

 Target yang valid pada model ini:
 - **deposit**: 0 -> yes, 1 -> no

#### **Recommendation**

>**Model Machine Learning**:

Rekomendasi yang bisa diberikan terhadap model untuk mengembangkan Machine Learning agar lebih baik lagi diantaranya:
 - Lakukan pembaharuan, dikarenakan nilai deposit interest rate dan kurs selalu berubah-ubah seiring berkembangnya zaman,
 - Eksplorasi algoritma model yang berbeda untuk mengembangkan model,
 - Menambahkan fitur baru berupa segmentasi user/nasabah (misalnya segmentasi usia, status nikah, jenis kelamin, dan lain-lain)

>**Bank**:

Rekomendasi yang bisa diberikan terhadap Bank ABC untuk mengembangkan campaign agar lebih baik lagi diantaranya:

 - **Data Historis Campaign**: Memanfaatkan data hasil campaign sebelumnya, terutama kesuksesan, adalah kunci dalam memprediksi dan meningkatkan respons positif.
 - **Metode Kontak**: Memilih metode kontak yang efektif sangat penting. Menghindari metode kontak yang kurang efektif dapat meningkatkan kemungkinan keberhasilan.
 - **Profil Keuangan Nasabah**: Memahami beban finansial nasabah, seperti pinjaman KPR atau pribadi, serta saldo rekening, dapat membantu dalam menargetkan nasabah yang lebih mungkin melakukan deposit.
 - **Waktu Campaign**: Melakukan campaign pada periode tertentu yang lebih kondusif dapat meningkatkan keberhasilan.
 - **Saldo Nasabah**: Fokuskan upaya campaign pada nasabah dengan saldo yang lebih tinggi karena mereka menunjukkan sedikit kecenderungan lebih besar untuk melakukan deposit.
 - **Frekuensi kontak**: Hindari menghubungi nasabah terlalu sering, karena ini bisa berdampak negatif. Lebih baik melakukan interaksi yang lebih bermakna dan relevan.
 - **Usia**: Karena usia tidak memiliki pengaruh yang signifikan, campaign dapat lebih disesuaikan dengan preferensi keuangan dan perilaku nasabah daripada usia mereka.
 - **Status Campaign**: Fokus dan lebih diperhatikan lagi status campaign yang telah dilakukan apakah berhasil atau tidak.


# **`gradboost_for_deposit.sav`**
- file model GradientBoost yang sudah disimpan melalui pickle
