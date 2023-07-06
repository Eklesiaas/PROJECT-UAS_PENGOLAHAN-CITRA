Pengolahan citra adalah sebuah cabang dalam ilmu komputer yang bertujuan untuk menganalisis, memproses, dan memanipulasi gambar digital. Tujuannya adalah untuk mengubah gambar menjadi bentuk yang lebih bermanfaat, seperti meningkatkan kualitas gambar, mengidentifikasi objek, atau mengekstrak informasi penting dari gambar.

Salah satu aplikasi penting dari pengolahan citra adalah deteksi marka jalan. Marka jalan merujuk pada garis-garis atau tanda yang terdapat pada permukaan jalan yang memberikan petunjuk kepada pengemudi tentang batas jalan, peringatan, atau arah yang harus diikuti. Deteksi marka jalan menggunakan teknik pengolahan citra untuk mengenali dan melacak marka jalan pada gambar atau video jalan.

Marka jalan merupakan garis-garis atau tanda pada permukaan jalan yang bertujuan memberikan petunjuk kepada pengemudi mengenai batas jalan, peringatan, atau arah yang harus diikuti. Pengolahan citra memainkan peran penting dalam analisis dan deteksi marka jalan, dengan menggunakan berbagai metode dan teknik untuk mengenali, memisahkan, dan menganalisis marka jalan dalam gambar atau video jalan.

Dalam teori marka jalan dalam pengolahan citra, terdapat beberapa metode umum yang digunakan:

Pra-pemrosesan:
Tahap pra-pemrosesan merupakan langkah awal dalam analisis marka jalan. Pada tahap ini, gambar jalan disiapkan dengan melakukan serangkaian operasi untuk meningkatkan kualitas gambar dan menghilangkan noise yang tidak diinginkan. Beberapa teknik yang sering digunakan dalam pra-pemrosesan antara lain:

Penghilangan noise: Menggunakan teknik filter seperti filter Gaussian atau median untuk menghilangkan noise pada gambar jalan.
Peningkatan kontras: Menerapkan teknik kontras seperti histogram equalization atau kontras adaptif untuk meningkatkan perbedaan intensitas warna antara marka jalan dan latar belakang.
Normalisasi intensitas warna: Menormalkan intensitas warna gambar untuk mengurangi variasi pencahayaan yang tidak relevan.
Penekanan fitur yang tidak relevan: Menggunakan teknik seperti penghapusan bayangan atau penekanan tekstur latar belakang agar hanya marka jalan yang mendominasi gambar.
Segmentasi:
Tahap segmentasi bertujuan untuk memisahkan marka jalan dari latar belakang atau elemen lain dalam gambar. Beberapa metode segmentasi yang umum digunakan dalam analisis marka jalan adalah:

Pemrosesan berbasis ambang: Menggunakan ambang intensitas warna untuk memisahkan marka jalan berdasarkan perbedaan intensitas dengan latar belakang.
Pemrosesan berbasis wilayah: Menggunakan algoritma seperti pemrosesan berbasis wilayah (region-based) atau pemrosesan berbasis tekstur untuk mengidentifikasi wilayah yang mencirikan marka jalan.
Pemrosesan berbasis tepi: Menggunakan deteksi tepi untuk menemukan garis-garis marka jalan berdasarkan perbedaan kecuraman atau perbedaan intensitas tepi dengan latar belakang.
Deteksi Marka Jalan:
Setelah tahap segmentasi, deteksi marka jalan dilakukan dengan menggunakan berbagai algoritma dan teknik. Beberapa metode umum yang digunakan dalam deteksi marka jalan adalah:

Transformasi Hough: Menggunakan transformasi Hough untuk mendeteksi garis-garis marka jalan berdasarkan pola garis pada gambar.
Transformasi Fourier: Menggunakan transformasi Fourier untuk menganalisis spektrum frekuensi gambar dan mendeteksi pola garis marka jalan.
Pemrosesan morfologi: Menggunakan operasi morfologi seperti dilasi dan erosi untuk memperbaiki atau mempertahankan struktur garis marka jalan.
Metode pembelajaran mesin: Menggunakan teknik pembelajaran mesin seperti Convolutional Neural Network (CNN) untuk melatih model yang dapat mengidentifikasi dan mempelajari pola marka jalan dari data pelatihan.
Pemrosesan dan Analisis Hasil Deteksi:
Setelah deteksi marka jalan dilakukan, tahap terakhir adalah pemrosesan dan analisis hasil deteksi untuk menghasilkan informInformasi yang lebih bermanfaat. Beberapa langkah yang umum dilakukan dalam tahap ini adalah:

Pengukuran posisi marka jalan: Menggunakan teknik pengolahan citra untuk mengukur posisi relatif marka jalan terhadap jalan atau kendaraan.
Klasifikasi jenis marka jalan: Menggunakan metode pengenalan pola atau algoritma pembelajaran mesin untuk mengklasifikasikan jenis marka jalan, seperti garis putus-putus, garis ganda, atau marka jalan peringatan.
Prediksi perilaku pengemudi: Menggunakan informasi marka jalan untuk memprediksi perilaku pengemudi, seperti mengenali marka jalan yang menunjukkan belokan atau marka jalan peringatan yang memerlukan reaksi pengemudi.
Dalam keseluruhan proses, pengolahan citra memainkan peran penting dalam analisis dan deteksi marka jalan. Metode dan teknik yang digunakan dalam teori marka jalan dalam pengolahan citra membantu mengidentifikasi, memisahkan, dan menganalisis marka jalan dalam gambar atau video jalan. Dengan penerapan teknik pengolahan citra yang tepat, deteksi marka jalan dapat dilakukan dengan efisiensi dan akurasi yang tinggi, yang berkontribusi pada peningkatan keamanan dan keselamatan lalu lintas jalan.

Metode deteksi marka jalan dapat dikombinasikan atau disesuaikan tergantung pada kompleksitas dan karakteristik citra jalan yang akan diproses. Pemilihan metode yang tepat tergantung pada kondisi jalan, kualitas citra, lingkungan, dan tujuan penggunaan deteksi marka jalan tersebut.

### Deteksi Marka Jalan Menggunakan Bahasa Python 
import cv2
import numpy as np
from matplotlib import pyplot as plt

img=cv2.imread('markajalan.jpg')
cv2.imshow('Image', img)
cv2.waitKey()
cv2.destroyAllWindows()

gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
edges = cv2.Canny(img, 100, 150)

fig, axs = plt.subplots(1,2, figsize =(10,10))
ax = axs.ravel()
ax[0].imshow(gray, cmap= 'gray')
ax[0].set_title('Gambar Asli')
ax[1].imshow(edges, cmap ='gray')
ax[1].set_title('Gambar Edges')

blur = cv2.GaussianBlur(gray, (5, 5), 0)

edges = cv2.Canny(blur, 50, 150)

mask = np.zeros_like(edges)

height, width = img.shape[:2]
roi_vertices = [(0, height), (width/1, height/1), (width, height)]
mask_color = 255
cv2.fillPoly(mask, np.array([roi_vertices], dtype=np.int32), mask_color)
masked_edges = cv2.bitwise_and(edges, mask)

lines = cv2.HoughLinesP(masked_edges, rho=1, theta=np.pi/180, threshold=400, minLineLength=40, maxLineGap=40)
Canny_image = cv2.Canny(gray, 200, 400)

#Menampilkan plot
plt.imshow(final_img)
plt.show()

#### Penjelasan source code 

Pertama, kita mengimpor library terlebih dahulu menggunakan cv2, numpy as np yang sering digunakan dalam pemrosesan gambar untuk melakukan operasi matematika pada array gambar, dan matpoltib import pyplot as plt yang digunakan untuk membuat visualisasi grafik dan plot.

Pada line berikutnya, pada awalnya, kode tersebut digunakan untuk membaca gambar dengan nama file "markajalan.jpg" menggunakan fungsi cv2.imread(). Gambar tersebut kemudian ditampilkan dalam sebuah jendela tampilan menggunakan fungsi cv2.imshow(), dengan judul jendela "Image". Setelah gambar ditampilkan, program akan berhenti sementara dan menunggu aksi dari pengguna. Aksi tersebut berupa menekan tombol apa pun pada keyboard. Pengguna dapat melihat gambar dengan detail dan melakukan aksi apapun sebelum melanjutkan eksekusi program. Setelah pengguna menekan tombol pada keyboard, semua jendela tampilan yang dibuka oleh OpenCV akan ditutup menggunakan fungsi cv2.destroyAllWindows(). Hal ini dilakukan untuk memastikan bahwa program berakhir dengan bersih dan tidak ada jendela tampilan yang terbuka setelah program selesai dieksekusi.

di line ketiga, Pada kode tersebut, terdapat dua proses pemrosesan gambar setelah membaca gambar "markajalan.jpg". Pertama, dilakukan konversi gambar menjadi citra abu-abu menggunakan fungsi cv2.cvtColor() dengan parameter cv2.COLOR_BGR2GRAY. Hasil konversi disimpan dalam variabel gray. Kedua, dilakukan deteksi tepi menggunakan algoritma Canny menggunakan fungsi cv2.Canny() dengan parameter threshold lower (100) dan threshold upper (150). Hasil deteksi tepi disimpan dalam variabel edges. Dengan demikian, kode tersebut menghasilkan citra abu-abu (gray) dan citra tepi (edges) dari gambar asli.

Selanjutnya, pada line berikutnya kode tersebut menggunakan plt.subplots() untuk membuat subplot dengan dua gambar. Pada subplot pertama, gambar abu-abu (gray) ditampilkan dengan imshow() dan diberi judul "Gambar Asli". Pada subplot kedua, gambar tepi (edges) ditampilkan dengan imshow() dan diberi judul "Gambar Edges". Dengan demikian, kita dapat membandingkan hasil pemrosesan gambar dalam satu tampilan subplot yang jelas dan ringkas.

berikutnya kita menggunakan fungsi cv2.GaussianBlur(), citra abu-abu (gray) akan mengalami proses pengaburan menggunakan filter Gaussian dengan ukuran kernel (5, 5) dan standar deviasi 0. Hasilnya, kita mendapatkan gambar yang lebih halus dan mengurangi detail atau noise yang tidak diinginkan dalam gambar.

lalu kita menggunakan fungsi cv2.Canny(), citra yang telah di-blur akan diproses untuk mendeteksi tepi dengan menggunakan nilai ambang bawah 50 dan nilai ambang atas 150. Hasilnya adalah citra yang menunjukkan lokasi tepi dalam gambar tersebut.

Kemudian, Dengan menggunakan np.zeros_like(edges), kita membuat matriks mask yang berisi nol dengan ukuran yang sama seperti citra tepi. Matriks ini nantinya dapat digunakan untuk menandai area di mana garis-garis deteksi akan digambar atau diaplikasikan.

di line 13, Pada kode tersebut, langkah-langkah berikut diimplementasikan untuk menghasilkan citra tepi yang terbatas pada area tertentu: Pertama, kita mendapatkan tinggi (height) dan lebar (width) citra asli (img) menggunakan atribut shape. Informasi ini akan digunakan dalam pembuatan poligon region of interest (ROI). Selanjutnya, kita mendefinisikan titik-titik (roi_vertices) yang membentuk poligon ROI. Poligon ini terdiri dari tiga titik, yaitu titik kiri bawah (0, height), titik tengah atas (width/2, height/2), dan titik kanan bawah (width, height). Setelah itu, kita inisialisasi matriks mask dengan nilai awal 0 dan tipe data yang sama dengan edges. Selanjutnya, kita menggunakan fungsi cv2.fillPoly() untuk mengisi poligon ROI dengan warna putih (mask_color) pada matriks mask. Terakhir, kita melakukan operasi bitwise AND antara citra tepi (edges) dan mask menggunakan fungsi cv2.bitwise_and(). Hasilnya disimpan dalam variabel masked_edges, yang merupakan citra tepi yang terbatas pada area ROI. Dengan langkah-langkah tersebut, kita memperoleh citra masked_edges yang merupakan hasil dari citra tepi (edges) yang terbatas hanya pada area ROI yang ditentukan.

Di line berikutnya, operasi pertama menggunakan fungsi cv2.HoughLinesP() untuk mendeteksi garis pada citra tepi (edges) menggunakan transformasi Hough Probabilistik. Transformasi Hough Probabilistik digunakan untuk mendeteksi garis lurus dalam citra berdasarkan pemilih (votes) yang melewati ambang batas tertentu. Pada operasi ini, kita menggunakan nilai rho=1 yang menandakan resolusi jarak adalah 1 piksel, theta=np.pi/180 yang menandakan resolusi sudut adalah 1 derajat, threshold=400 yang menandakan bahwa setiap garis dengan pemilih di atas 400 akan diterima, minLineLength=40 yang menandakan panjang garis minimum yang diterima adalah 40 piksel, dan maxLineGap=40 yang menandakan jarak maksimum antara segmen garis yang dihubungkan menjadi satu garis penuh adalah 40 piksel. Operasi kedua menggunakan fungsi cv2.Canny() untuk menghasilkan citra tepi menggunakan algoritma Canny pada citra abu-abu (gray). Algoritma Canny digunakan untuk mengidentifikasi tepi dalam citra dengan menghitung gradien intensitas piksel. Pada operasi ini, kita menggunakan nilai 200 sebagai threshold lower yang menentukan batas bawah untuk deteksi tepi, dan 400 sebagai threshold upper yang menentukan batas atas untuk deteksi tepi.

Berikutnya, di line 15 dalam kode di atas, kita membuat citra kosong dengan ukuran yang sama seperti gambar asli. Kemudian, melalui loop for, kita mengiterasi setiap garis yang terdeteksi dalam variabel lines. Dalam setiap iterasi, koordinat titik awal dan titik akhir garis diambil dari setiap elemen dalam lines. Menggunakan fungsi cv2.line(), garis tersebut digambar pada citra kosong. Warna garis ditentukan sebagai hijau (0, 255, 0), dan ketebalannya ditetapkan sebagai 10. Melalui proses ini, garis-garis yang terdeteksi akan digambar pada citra kosong, sehingga menciptakan gambar baru yang menampilkan garis-garis tersebut.

Pada bagian berikutnya, Fungsi cv2.addWeighted() digunakan untuk menggabungkan dua gambar dengan bobot tertentu. Parameter pertama adalah gambar asli dengan bobot 0.8, sedangkan parameter kedua adalah gambar yang berisi garis-garis dengan bobot 1. Hasil penggabungan gambar disimpan dalam variabel final_img, yang menampilkan gambar asli dengan garis-garis yang terdeteksi. Dengan penggabungan ini, garis-garis terdeteksi akan terlihat pada gambar asli dengan bobot tertentu, sehingga menciptakan gambar yang menggabungkan informasi garis-garis dengan gambar asli.

Kemudian, kita menggunakan imshow untuk menampilkan final image dari gambar yang telah terdeteksi garisnya. 


### Web sebagai referensi
https://j-ptiik.ub.ac.id/index.php/j-ptiik/article/download/5604/2654/










