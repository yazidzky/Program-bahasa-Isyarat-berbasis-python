# Proyek: Penerjemah Bahasa Isyarat Tangan

## 1.	Pendahuluan
Deteksi gerakan tangan adalah salah satu penerapan computer vision yang semakin populer dalam berbagai bidang. Teknologi ini digunakan untuk menciptakan antarmuka pengguna yang lebih alami, mengendalikan perangkat melalui isyarat tangan, hingga membantu pengembangan teknologi assistive bagi penyandang disabilitas. Di sini, deteksi gestur tangan berbasis kamera memegang peranan penting dalam mengenali pola gerakan tangan dan menerjemahkannya menjadi perintah yang dipahami oleh sistem.

Finite State Automata (FSA) dapat digunakan sebagai model dalam sistem deteksi gerakan tangan untuk mengatur alur proses dari inisialisasi hingga pengenalan gestur. FSA bekerja dengan cara berpindah dari satu state ke state lainnya berdasarkan input yang diterima, seperti hasil deteksi jari atau perintah untuk menghentikan program. Artikel ini akan menjelaskan analisis kebutuhan, proses pengumpulan data, dan studi literatur yang terkait dengan penggunaan FSA dalam sistem deteksi gerakan tangan berbasis kamera.

## 2.	Analisis Kebutuhan dan Pengumpulan Data

### 2.1	Analisis Kebutuhan

Dalam perancangan sistem deteksi gerakan tangan berbasis kamera, ada beberapa kebutuhan fungsional dan non-fungsional yang harus dipenuhi:

Kebutuhan Fungsional:

•	Sistem harus mampu menginisialisasi kamera dan menangkap video secara real-time.
•	Sistem harus mendeteksi landmark tangan menggunakan teknik computer vision atau machine learning.
•	Sistem harus mampu menghitung jumlah jari yang terangkat berdasarkan landmark yang terdeteksi.
•	Sistem perlu mengenali gestur tangan seperti "Saya" (satu jari), "Kamu" (dua jari), dan "Cinta" (tiga jari) dari jumlah jari yang terangkat.
 
•	Hasil pengenalan harus ditampilkan kepada pengguna, dan sistem harus memberikan opsi keluar dari program melalui tombol ‘q’.
•	Sistem harus menutup kamera dan menghentikan proses ketika pengguna memilih keluar.

Kebutuhan Non-Fungsional:

•	Sistem harus bekerja secara real-time tanpa latensi yang signifikan.
•	Sistem harus kompatibel dengan perangkat keras yang umum (laptop atau desktop dengan webcam) dan tidak membutuhkan spesifikasi tinggi.
•	Antarmuka pengguna harus mudah dipahami dan dioperasikan.
•	Sistem harus dirancang dengan efisiensi sumber daya, baik dalam hal memori maupun penggunaan CPU.

#### 2.2	Pengumpulan Data

Untuk mengembangkan sistem ini, beberapa data dan perangkat lunak yang dibutuhkan meliputi:

•	Dataset Landmark Tangan: Data ini diperlukan untuk mendeteksi posisi jari secara akurat. MediaPipe Hands adalah salah satu dataset yang menyediakan landmark untuk setiap sendi tangan dan jari, yang sangat berguna dalam proses pengenalan gestur.
•	Framework dan Library:
o	MediaPipe Hands: Library ini menyediakan deteksi landmark tangan secara real- time menggunakan deep learning, yang cocok untuk pengembangan sistem ini.
o	OpenCV: Digunakan untuk menangkap video dari kamera dan memproses frame secara langsung, termasuk membalik (flipping) frame untuk orientasi yang sesuai.

## 3.	Studi Literatur

### 3.1	Deteksi Gerakan Tangan dan Pendeteksian Landmark

Deteksi gerakan tangan dengan menggunakan landmark merupakan salah satu teknik utama dalam computer vision. Pendekatan ini sering menggunakan deep learning untuk mendeteksi posisi jari dan tangan dari gambar atau video. MediaPipe Hands adalah salah satu model deep learning yang telah dioptimalkan untuk pendeteksian landmark tangan secara real-time. Model
 
ini dapat mendeteksi hingga 21 landmark tangan dengan efisiensi tinggi, sehingga cocok untuk perangkat dengan kapasitas komputasi terbatas seperti laptop atau ponsel.

Referensi:
John dan Sherif (2022), dalam penelitian mereka "Hand landmark-based sign language recognition using deep learning," membahas penggunaan deep learning untuk mendeteksi landmark tangan dan implementasinya dalam pengenalan gestur.

### 3.2	Implementasi Sistem Real-Time untuk Pendeteksian Tangan

Sistem real-time biasanya menggunakan OpenCV untuk menangkap dan memproses citra secara langsung. OpenCV merupakan library populer yang mendukung berbagai operasi citra, mulai dari menangkap frame hingga preprocessing seperti flipping atau cropping. Dalam pengembangan sistem deteksi gerakan tangan, OpenCV menjadi alat penting untuk mengolah data video dari kamera secara real-time.

Referensi:
Bradski (2000) menjelaskan dalam "The OpenCV Library" tentang peran penting OpenCV dalam pemrosesan gambar, khususnya dalam aplikasi deteksi gerakan tangan.

### 3.3	Finite State Automata (FSA) dalam Pengenalan Gestur

Finite State Automata (FSA) sering digunakan dalam sistem pengenalan pola, termasuk pengenalan gestur. FSA memodelkan sistem sebagai kumpulan state yang dihubungkan oleh transisi, yang terjadi berdasarkan input yang diterima. Dalam sistem deteksi gerakan tangan, FSA dapat mengatur transisi dari deteksi landmark, pengenalan gestur, hingga penghentian proses ketika pengguna keluar.

Referensi:
Rabiner dan Juang (1986) dalam "An Introduction to Hidden Markov Models" menjelaskan bagaimana FSA dan model automata digunakan dalam pengenalan pola, yang dapat diterapkan dalam sistem pengenalan gestur.
 
### 3.4	Aplikasi Pengenalan Gestur untuk Teknologi Assistive

Pengenalan gestur berbasis deteksi gerakan tangan memiliki potensi besar dalam teknologi assistive, terutama dalam membantu penyandang disabilitas. Misalnya, penerjemah bahasa isyarat menggunakan deteksi gerakan tangan untuk mengenali simbol tangan yang kemudian diterjemahkan ke dalam teks atau suara, membantu individu dengan keterbatasan bicara atau pendengaran.

Referensi:
Nikam dan Ambekar (2016, November) dalam "Sign Language Recognition Using Image Based Hand Gesture Recognition" membahas bagaimana teknologi pengenalan gestur diterapkan dalam penerjemahan bahasa isyarat, yang berpotensi untuk diterapkan dalam berbagai teknologi assistive lainnya.

## 4.	Perancangan dan Implementasi Finite State Automata(FSA) untuk Deteksi Gerakan Tangan

Finite State Automata (FSA) bisa digunakan untuk memodelkan transisi antar proses dalam algoritma deteksi gestur tangan. Di sini, sistem mendeteksi jumlah jari yang terangkat dan mengenali gestur yang ditampilkan. Berikut adalah perancangan dan implementasi FSA untuk algoritma deteksi gestur tangan menggunakan Python.

### 4.1	Definisi State

•	State Mulai: Kondisi awal ketika sistem diinisialisasi.
•	State Inisialisasi Kamera: Sistem memulai kamera dan inisialisasi pendeteksi tangan.
•	State Tangkap Frame: Sistem menangkap gambar dari kamera (webcam).
•	State Flip Frame: Proses membalik gambar untuk memastikan orientasi yang benar (mirror).
•	State Deteksi Landmark: Sistem mendeteksi landmark tangan dalam frame.
•	State Hitung Jari: Sistem menghitung jumlah jari yang terangkat dari landmark tangan yang terdeteksi.
 
•	State Kenali Gestur: Sistem mengidentifikasi gestur berdasarkan jumlah jari yang terangkat.
•	State Tampilkan Gestur: Sistem menampilkan hasil pengenalan gestur seperti "Saya" (untuk satu jari terangkat), "Kamu" (dua jari), "Cinta" (tiga jari), dan seterusnya.
•	State Tekan 'q' untuk Keluar: Sistem memonitor apakah pengguna menekan 'q' untuk menghentikan proses.
•	State Tutup Kamera & Window: Sistem menutup kamera dan menutup jendela tampilan setelah selesai.
•	State Selesai: Sistem berhenti dan keluar.

### 4.2	Transisi Antar State

•	Mulai ke Inisialisasi Kamera: Terjadi ketika sistem dimulai dan kamera serta pendeteksi tangan diinisialisasi.
•	Inisialisasi Kamera ke Tangkap Frame: Setelah inisialisasi selesai, sistem mulai menangkap frame dari kamera.
•	Tangkap Frame ke Flip Frame: Setelah frame ditangkap, sistem membalik gambar untuk orientasi yang sesuai.
•	Flip Frame ke Deteksi Landmark: Sistem mendeteksi landmark tangan dalam frame yang sudah di-flip.
•	Deteksi Landmark ke Hitung Jari: Jika landmark tangan terdeteksi, sistem menghitung jumlah jari yang terangkat.
•	Hitung Jari ke Kenali Gestur: Berdasarkan jumlah jari yang terangkat, sistem mengidentifikasi gestur yang sesuai.
•	Kenali Gestur ke Tampilkan Gestur: Setelah gestur dikenali, sistem menampilkan hasilnya (misalnya, "Saya", "Kamu", atau "Cinta").
•	Tampilkan Gestur ke Tekan 'q' untuk Keluar: Setelah gestur ditampilkan, sistem memeriksa apakah pengguna menekan 'q' untuk keluar.
•	Tekan 'q' untuk Keluar ke Tutup Kamera & Window: Jika 'q' ditekan, sistem menutup kamera dan jendela tampilan.
•	Tutup Kamera & Window ke Selesai: Setelah kamera dan jendela tampilan ditutup, sistem berhenti dan selesai.
 


### 4.3	Implementasi FSA

Berikut adalah representasi visual dari FSA untuk sistem deteksi gerakan tangan: Dalam bentuk Flowchart:

![image](https://github.com/user-attachments/assets/847c8507-c50f-4260-ae4d-93fe7f722532)

Dalam bentuk Diagram state:

![image](https://github.com/user-attachments/assets/b183fe8e-a90b-4fc4-b209-e0be0e0719a2)



1.	State Mulai:
o	Sistem diinisialisasi dan langsung menuju Inisialisasi Kamera.
2.	Inisialisasi Kamera:
o	Sistem membuka kamera dan menyiapkan pendeteksi landmark tangan.
o	Setelah berhasil, transisi ke Tangkap Frame.
3.	Tangkap Frame:
o	Sistem menangkap gambar dari kamera.
o	Setelah frame ditangkap, sistem beralih ke Flip Frame.
4.	Flip Frame:
o	Gambar dibalik (mirror) untuk memastikan orientasi yang sesuai.
o	Kemudian, sistem berlanjut ke Deteksi Landmark.
5.	Deteksi Landmark:


o	Sistem memindai frame untuk mendeteksi landmark tangan.
o	Jika landmark tangan ditemukan, sistem transisi ke Hitung Jari.
o	Jika tidak ditemukan, sistem kembali menampilkan frame dan memeriksa ulang.
6.	Hitung Jari:
o	Berdasarkan landmark tangan, sistem menghitung jumlah jari yang terangkat.
o	Setelah menghitung, sistem berpindah ke Kenali Gestur.
7.	Kenali Gestur:
o	Sistem mengidentifikasi gestur berdasarkan jumlah jari yang terangkat.
o	Setelah gestur dikenali, sistem bergerak ke Tampilkan Gestur.
8.	Tampilkan Gestur:
o	Sistem menampilkan atau memvokalisasi hasil pengenalan gestur.
o	Setelah itu, sistem memeriksa apakah pengguna menekan 'q' untuk keluar.
9.	Tekan 'q' untuk Keluar:
o	Sistem menunggu input dari pengguna.
o	Jika 'q' ditekan, sistem beralih ke Tutup Kamera & Window.
o	Jika tidak ditekan, sistem kembali menampilkan frame dan memulai deteksi ulang.
10.	Tutup Kamera & Window:
o	Sistem menutup kamera dan jendela tampilan.
o	Setelah semua proses selesai, sistem masuk ke Selesai.
11.	Selesai:
o	Sistem berhenti dan keluar.

## Pendekatan Klasifikasi Berbasis Kelompok untuk Peningkatan Akurasi
Dalam pengembangan sistem pengenalan bahasa isyarat tangan, tantangan utama adalah akurasi rendah saat mengklasifikasikan 26 kelas alfabet yang berbeda sekaligus. Untuk mengatasi masalah ini, kami mengimplementasikan strategi pengelompokan alfabet berdasarkan kemiripan bentuk atau pola isyarat tangan.
Pembagian Kelas Alfabet
Seluruh alfabet [a-z] dibagi ke dalam 8 kelas utama, di mana setiap kelas berisi alfabet yang memiliki pola isyarat tangan serupa. Berikut adalah rincian pembagian kelas:
1.	[y, j]
   
 ![image](https://github.com/user-attachments/assets/b90e5cc3-830f-41cd-ba68-8d339256eba7)

Gamabar 1:

o	Alfabet ini memiliki kemiripan pola dengan isyarat menggunakan ibu jari dan jari kelingking.
2.	[c, o]

 ![image](https://github.com/user-attachments/assets/f46a1034-9ac9-4091-9f1a-308bfa865ac1)

Gambar 2:

o	Alfabet ini memiliki pola melingkar pada gestur tangan.
3.	[g, h]

 ![image](https://github.com/user-attachments/assets/a3257b70-15be-46f8-93de-9b1004cc82da)

Gambar 3:

o	Isyarat tangan untuk alfabet ini melibatkan posisi jari telunjuk dan jari tengah yang menyerupai garis lurus.
4.	[b, d, f, i, u, v, k, r, w]

 ![image](https://github.com/user-attachments/assets/e278e493-54bc-448c-b4c5-10c3ac398f0a)

Gambar 4:

o	Alfabet dalam kelas ini memiliki pola beragam tetapi cenderung melibatkan kombinasi jari yang terpisah atau membentuk pola "V".
5.	[p, q, z]
 ![image](https://github.com/user-attachments/assets/2daa795b-dabe-4ad8-9e45-e86e06f3956e)

Gambar 5:

o	Isyarat tangan dalam kelas ini umumnya melibatkan jari-jari membentuk pola lengkungan ke bawah atau silang.
6.	[a, e, m, n, s, t]
 ![image](https://github.com/user-attachments/assets/52852d18-04f3-4cf8-a98b-3ec48b30a1da)

Gambar 6:

o	Kelas ini terdiri dari alfabet dengan pola tangan yang lebih kompleks tetapi memiliki fitur serupa, seperti posisi jari tertutup.

## Proses Prediksi dan Klasifikasi
1. Klasifikasi Awal (Kelompok Besar):
•	Model CNN digunakan untuk mengklasifikasikan gestur tangan ke salah satu dari 8 kelas utama.
•	Prediksi dilakukan berdasarkan probabilitas tertinggi yang dihasilkan oleh model.
2. Klasifikasi Lanjutan (Spesifik Alfabet):
•	Setelah gestur diklasifikasikan ke dalam kelompok besar, langkah berikutnya adalah memproses gestur untuk menentukan alfabet spesifik.
•	Pada tahap ini, dilakukan operasi matematis pada landmark tangan untuk menganalisis posisi dan orientasi jari secara lebih mendetail.
•	Contoh: Jika model mengklasifikasikan gestur ke kelas [a, e, m, n, s, t], operasi matematis seperti sudut antara jari atau jarak antar titik pada landmark akan digunakan untuk membedakan a dari e, atau m dari n.
Manfaat Pendekatan Ini
1.	Mengurangi Kompleksitas:
o	Dengan membagi alfabet ke dalam kelas besar, model hanya perlu mempelajari pola dalam kelompok kecil terlebih dahulu, yang lebih sederhana dan kurang ambigu.
2.	Meningkatkan Akurasi:
o	Mengelompokkan alfabet yang mirip mempermudah model dalam mengenali pola.
o	Klasifikasi lanjutan menggunakan operasi matematis meningkatkan presisi prediksi alfabet spesifik.
3.	Skalabilitas:
Strategi ini memungkinkan integrasi lebih mudah dengan fitur atau bahasa isyarat lainnya, karena model hanya perlu menyesuaikan kelompok besar tanpa perlu merancang ulang seluruh sistem.

Fungsi dan Hasil Implementasi

![image](https://github.com/user-attachments/assets/a46887fc-5576-40f7-8b48-a7b1ebc3340e)

Backspace Functionality (Gambar 1)

Pengguna menunjukkan gerakan tangan yang diprogram untuk melakukan aksi "Backspace".
Sistem mengenali gerakan dengan benar dan menampilkan "Huruf: Backspace", yang secara otomatis menghapus huruf terakhir dari kalimat yang sedang dibuat.

![image](https://github.com/user-attachments/assets/21f0ca69-0d4f-4db3-b763-d86b37d4caf2)

Pengenalan Huruf contoh :"Y" (Gambar 2)

Pengguna memberikan gestur tangan untuk huruf "Y".
Sistem berhasil mengenali huruf ini dan menambahkannya ke dalam kalimat ("Kalimat: VY").
Sistem juga memberikan saran huruf lain seperti "BY" untuk memungkinkan koreksi jika prediksi tidak sesuai.

![image](https://github.com/user-attachments/assets/694b9267-b195-4b61-8722-23ff1e7b5e58)

Next Functionality (Gambar 3)

Sistem mendeteksi gestur tangan yang menandakan aksi "Next".
Fungsi ini memungkinkan pengguna untuk menyelesaikan proses prediksi huruf dan melanjutkan ke tahapan berikutnya. Sistem terus memperbarui kalimat sesuai dengan huruf yang telah dikenali.

## Proses Implementasi

Proyek ini bertujuan untuk menerjemahkan bahasa isyarat tangan (Alphabet A-Z) ke dalam teks menggunakan *Computer Vision* dan *Deep Learning*. Sistem ini menggunakan kamera untuk menangkap gambar tangan, mendeteksi posisi jari, membentuk *skeleton* tangan, lalu memprediksi huruf berdasarkan model CNN yang telah dilatih.

Terdapat beberapa modul utama dalam proyek ini:
- `data_binary.py`: Mengambil citra tangan dan mengolahnya menjadi format biner atau grayscale.
- `data_final.py`: Menangkap skeleton tangan dan menyimpannya ke dalam dataset.
- `prediksi.py`: Memprediksi huruf dari gestur tangan secara real-time menggunakan model CNN.
- `utama.py` dan `tempCodeRunnerFile.py`: Antarmuka GUI untuk menampilkan hasil prediksi dan menyusun kalimat dari hasil huruf-huruf prediksi.

---

### 2. Penjelasan Kode Tiap Baris (Contoh: `data_binary.py`)

```python
capture = cv2.VideoCapture(0)  # Mengaktifkan webcam
hd = HandDetector(maxHands=1)  # Inisialisasi detektor tangan dari cvzone
```

```python
hands = hd.findHands(frame, draw=False, flipType=True)  # Mendeteksi tangan
if hands:
    hand = hands[0]
    x, y, w, h = hand['bbox']  # Mendapatkan koordinat bounding box tangan
```

```python
gray = cv2.cvtColor(roi, cv2.COLOR_BGR2GRAY)  # Mengubah gambar ke grayscale
blur = cv2.GaussianBlur(gray, (1, 1), 2)  # Menghaluskan noise gambar
```

```python
th3 = cv2.adaptiveThreshold(..., cv2.THRESH_BINARY_INV, ...)  # Konversi ke biner
```

```python
img_final = np.ones((400, 400), np.uint8) * 255
img_final[((400 - h) // 2):...+h, ((400 - w) // 2):...+w] = test_image
# Menempatkan gambar hasil threshold ke dalam canvas putih 400x400
```

```python
cv2.imshow("binary", img_final)  # Menampilkan hasil akhir di window
```

Kode lainnya memiliki struktur dan fungsi serupa, hanya dengan tambahan logika klasifikasi dan GUI.

---

### 3. Analogi Sederhana Algoritma

Bayangkan kamu sedang main tebak huruf dengan teman. Temanmu membentuk huruf dengan tangan, kamu melihat posisi jari-jari mereka, menggambar ulang bentuk tangan mereka, lalu mencoba menebak huruf apa itu berdasarkan contoh-contoh yang pernah kamu pelajari sebelumnya.

Begitu juga sistem ini:
- Melihat posisi jari (deteksi tangan)
- Menggambar ulang dalam bentuk skeleton (cv2 line & circle)
- Memasukkan ke "otak" (model CNN)
- Menebak hurufnya (klasifikasi)
- Lalu menampilkan hasilnya ke layar

---

### 4. Cara Penggunaan

1. **Persiapan**
   - Pastikan semua dependency sudah terinstal, seperti:
     ```bash
     pip install opencv-python cvzone keras numpy pyttsx3 pillow enchant
     ```
   - Siapkan file model CNN (`cnn8grps_rad1_model.h5`) di direktori yang sama.

2. **Menjalankan Program**
   - Untuk mengumpulkan data:
     ```bash
     python data_final.py
     ```
     Tekan `a` untuk mulai menyimpan data dan `n` untuk pindah ke huruf berikutnya.

   - Untuk melihat preprocessing citra:
     ```bash
     python data_binary.py
     ```

   - Untuk menjalankan prediksi secara real-time:
     ```bash
     python prediksi.py
     ```

   - Untuk membuka GUI penerjemah:
     ```bash
     python utama.py
     ```

3. **Navigasi di GUI**
   - Kamera akan otomatis mendeteksi tangan.
   - Huruf hasil prediksi akan tampil di bawah label "Huruf".
   - Kalimat akan disusun otomatis.
   - Tersedia tombol koreksi hasil prediksi (kata yang disarankan).
   - Tombol "Hapus" untuk mengosongkan kalimat.

---

### 5. Kesimpulan

Proyek ini merupakan implementasi nyata dari penggabungan *Computer Vision*, *Machine Learning*, dan *GUI* untuk menyelesaikan masalah nyata: membantu komunikasi bahasa isyarat. 

Dengan struktur modular:
- `data_binary.py` → preprocessing data
- `data_final.py` → dataset builder
- `prediksi.py` → real-time prediction
- `utama.py` → aplikasi GUI

Proyek ini bisa dikembangkan lebih lanjut ke bahasa isyarat penuh, voice output, atau penerjemahan kalimat penuh. Cocok untuk digunakan dalam pendidikan, inklusi disabilitas, dan komunikasi.

---

> Untuk dokumentasi lebih mendetail tiap file, kamu bisa buat README terpisah atau dokumentasi inline (komentar dalam kode).

