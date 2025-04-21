#Proyek: Penerjemah Bahasa Isyarat Tangan

1.	Pendahuluan
Deteksi gerakan tangan adalah salah satu penerapan computer vision yang semakin populer dalam berbagai bidang. Teknologi ini digunakan untuk menciptakan antarmuka pengguna yang lebih alami, mengendalikan perangkat melalui isyarat tangan, hingga membantu pengembangan teknologi assistive bagi penyandang disabilitas. Di sini, deteksi gestur tangan berbasis kamera memegang peranan penting dalam mengenali pola gerakan tangan dan menerjemahkannya menjadi perintah yang dipahami oleh sistem.

Finite State Automata (FSA) dapat digunakan sebagai model dalam sistem deteksi gerakan tangan untuk mengatur alur proses dari inisialisasi hingga pengenalan gestur. FSA bekerja dengan cara berpindah dari satu state ke state lainnya berdasarkan input yang diterima, seperti hasil deteksi jari atau perintah untuk menghentikan program. Artikel ini akan menjelaskan analisis kebutuhan, proses pengumpulan data, dan studi literatur yang terkait dengan penggunaan FSA dalam sistem deteksi gerakan tangan berbasis kamera.

2.	Analisis Kebutuhan dan Pengumpulan Data

2.1	Analisis Kebutuhan

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

2.2	Pengumpulan Data

Untuk mengembangkan sistem ini, beberapa data dan perangkat lunak yang dibutuhkan meliputi:

•	Dataset Landmark Tangan: Data ini diperlukan untuk mendeteksi posisi jari secara akurat. MediaPipe Hands adalah salah satu dataset yang menyediakan landmark untuk setiap sendi tangan dan jari, yang sangat berguna dalam proses pengenalan gestur.
•	Framework dan Library:
o	MediaPipe Hands: Library ini menyediakan deteksi landmark tangan secara real- time menggunakan deep learning, yang cocok untuk pengembangan sistem ini.
o	OpenCV: Digunakan untuk menangkap video dari kamera dan memproses frame secara langsung, termasuk membalik (flipping) frame untuk orientasi yang sesuai.

3.	Studi Literatur

3.1	Deteksi Gerakan Tangan dan Pendeteksian Landmark

Deteksi gerakan tangan dengan menggunakan landmark merupakan salah satu teknik utama dalam computer vision. Pendekatan ini sering menggunakan deep learning untuk mendeteksi posisi jari dan tangan dari gambar atau video. MediaPipe Hands adalah salah satu model deep learning yang telah dioptimalkan untuk pendeteksian landmark tangan secara real-time. Model
 
ini dapat mendeteksi hingga 21 landmark tangan dengan efisiensi tinggi, sehingga cocok untuk perangkat dengan kapasitas komputasi terbatas seperti laptop atau ponsel.

Referensi:
John dan Sherif (2022), dalam penelitian mereka "Hand landmark-based sign language recognition using deep learning," membahas penggunaan deep learning untuk mendeteksi landmark tangan dan implementasinya dalam pengenalan gestur.

3.2	Implementasi Sistem Real-Time untuk Pendeteksian Tangan

Sistem real-time biasanya menggunakan OpenCV untuk menangkap dan memproses citra secara langsung. OpenCV merupakan library populer yang mendukung berbagai operasi citra, mulai dari menangkap frame hingga preprocessing seperti flipping atau cropping. Dalam pengembangan sistem deteksi gerakan tangan, OpenCV menjadi alat penting untuk mengolah data video dari kamera secara real-time.

Referensi:
Bradski (2000) menjelaskan dalam "The OpenCV Library" tentang peran penting OpenCV dalam pemrosesan gambar, khususnya dalam aplikasi deteksi gerakan tangan.

3.3	Finite State Automata (FSA) dalam Pengenalan Gestur

Finite State Automata (FSA) sering digunakan dalam sistem pengenalan pola, termasuk pengenalan gestur. FSA memodelkan sistem sebagai kumpulan state yang dihubungkan oleh transisi, yang terjadi berdasarkan input yang diterima. Dalam sistem deteksi gerakan tangan, FSA dapat mengatur transisi dari deteksi landmark, pengenalan gestur, hingga penghentian proses ketika pengguna keluar.

Referensi:
Rabiner dan Juang (1986) dalam "An Introduction to Hidden Markov Models" menjelaskan bagaimana FSA dan model automata digunakan dalam pengenalan pola, yang dapat diterapkan dalam sistem pengenalan gestur.
 
3.4	Aplikasi Pengenalan Gestur untuk Teknologi Assistive

Pengenalan gestur berbasis deteksi gerakan tangan memiliki potensi besar dalam teknologi assistive, terutama dalam membantu penyandang disabilitas. Misalnya, penerjemah bahasa isyarat menggunakan deteksi gerakan tangan untuk mengenali simbol tangan yang kemudian diterjemahkan ke dalam teks atau suara, membantu individu dengan keterbatasan bicara atau pendengaran.

Referensi:
Nikam dan Ambekar (2016, November) dalam "Sign Language Recognition Using Image Based Hand Gesture Recognition" membahas bagaimana teknologi pengenalan gestur diterapkan dalam penerjemahan bahasa isyarat, yang berpotensi untuk diterapkan dalam berbagai teknologi assistive lainnya.

4.	Perancangan dan Implementasi Finite State Automata(FSA) untuk Deteksi Gerakan Tangan

Finite State Automata (FSA) bisa digunakan untuk memodelkan transisi antar proses dalam algoritma deteksi gestur tangan. Di sini, sistem mendeteksi jumlah jari yang terangkat dan mengenali gestur yang ditampilkan. Berikut adalah perancangan dan implementasi FSA untuk algoritma deteksi gestur tangan menggunakan Python.

4.1	Definisi State

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

4.2	Transisi Antar State

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
 


4.3	Implementasi FSA

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

Pendekatan Klasifikasi Berbasis Kelompok untuk Peningkatan Akurasi
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
Proses Prediksi dan Klasifikasi
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

Proses Implementasi

Penggunaan CNN
1.	CNN digunakan untuk memproses gambar tangan pengguna, mengekstraksi fitur visual, dan mengenali gerakan tangan. Model dilatih menggunakan dataset gambar tangan dengan berbagai latar belakang dan kondisi pencahayaan untuk memastikan akurasi tinggi dalam lingkungan yang berbeda.

2.	Pengembangan GUI
GUI dirancang menggunakan Python Tkinter untuk memberikan antarmuka yang intuitif bagi pengguna. Komponen yang diimplementasikan meliputi:

•	Tampilan live feed dari kamera.
•	Area hasil prediksi yang menampilkan huruf dan kalimat.
•	Tombol untuk aksi seperti "Hapus" dan pilihan saran huruf.

Hasil Pengujian
Sistem berhasil mengenali huruf alfabet dan beberapa fungsi tambahan seperti "Backspace" dan "Next" dengan akurasi hingga 97%.
Pada kondisi pencahayaan yang optimal dan latar belakang yang bersih, akurasi meningkat hingga 99%.
GUI membantu membuat proses prediksi lebih mulus dengan saran huruf alternatif yang memungkinkan pengguna untuk melakukan koreksi secara manual jika diperlukan.

Penjelasan Tombol "Hapus" dan "Perkiraan"
Pada implementasi sistem penerjemah bahasa isyarat tangan ini, dua fitur penting ditambahkan untuk meningkatkan kemudahan penggunaan, yaitu tombol "Hapus" dan bagian "Perkiraan".
1. Tombol "Hapus"
Fungsi:
Tombol ini dirancang untuk menghapus seluruh kalimat yang sedang ditampilkan.
•	Ketika pengguna merasa bahwa hasil prediksi huruf atau kalimat tidak sesuai, mereka dapat menggunakan tombol ini untuk menghapus semua teks yang telah terakumulasi.
•	Tombol ini memberikan kemudahan untuk memulai proses prediksi dari awal tanpa harus menutup atau me-restart aplikasi.
Cara Kerja:
•	Saat tombol ditekan, program mengosongkan variabel atau buffer tempat kalimat sementara disimpan.
•	Setelah penghapusan, area Kalimat dalam GUI akan kosong, memberikan ruang bagi pengguna untuk memulai kembali proses prediksi.
2. Bagian "Perkiraan"
Fungsi:
Bagian ini menampilkan saran huruf lain berdasarkan hasil analisis model CNN.
•	Karena model tidak selalu 100% akurat, terutama jika gestur tangan ambigu atau tidak jelas, fitur "Perkiraan" memberikan opsi tambahan kepada pengguna.
•	Saran ini memungkinkan pengguna untuk memilih huruf yang mereka maksud jika prediksi utama kurang tepat.
Cara Kerja:
•	Model CNN menghasilkan daftar kemungkinan huruf berdasarkan probabilitas prediksi.
•	Huruf dengan probabilitas tertinggi ditampilkan di bagian Huruf, sedangkan beberapa opsi lain dengan probabilitas tinggi ditampilkan di bagian Perkiraan.
•	Pengguna dapat memilih salah satu opsi dari Perkiraan untuk mengganti huruf yang ditampilkan.
Contoh Kasus: Jika pengguna menunjukkan gestur untuk huruf "Y", tetapi sistem salah mengenali sebagai "V", huruf "Y" mungkin muncul di daftar Perkiraan. Pengguna cukup mengklik huruf "Y" untuk memperbaiki hasil.
Manfaat Kedua Fitur Ini
1.	Tombol "Hapus":
o	Membantu memperbaiki keseluruhan teks dengan cepat tanpa perlu proses manual yang memakan waktu.
o	Memudahkan pengguna untuk memulai ulang jika terjadi kesalahan.
2.	Bagian "Perkiraan":
o	Memberikan fleksibilitas kepada pengguna untuk mengatasi kesalahan prediksi model.
o	Meningkatkan pengalaman pengguna dengan memberikan opsi koreksi langsung.
Fitur ini menambah nilai praktis pada sistem, memastikan bahwa pengguna mendapatkan hasil yang sesuai dengan harapan mereka, terlepas dari kondisi pencahayaan atau latar belakang yang mungkin memengaruhi akurasi prediksi.


