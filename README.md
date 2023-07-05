# PA_04_202131054_E

Nama : Bayu Alif Pratikno
Nim : 202131054
Matakuliah = Pengolahan Citra

Untuk mendeteksi buah pada gambar menggunakan Jupyter Notebook,dapat menggunakan beberapa library komputer vision populer seperti OpenCV atau TensorFlow. Di bawah ini adalah contoh praktek hasil menggunakan OpenCV:

1. Instalasi Libraries:
   Pastikan Python dan Jupyter Notebook terinstal di pc. Selanjutnya, instal library OpenCV dengan menjalankan perintah berikut di command prompt atau terminal:

   pip install opencv-python
  
2. Persiapan Gambar:
   gunakan gambar buah buahan yang telah di photo tadi. nama file photo buah yang saya gunakan   IMG20230705135355.jpg

3. Import Libraries dan Memuat Gambar:
   dimulai dengan mengimport library yang dibutuhkan dan memuat gambar ke dalam notebook. dengan menjalankan code berikut di Jupyter Notebook:

   import cv2
   import numpy as np
   from matplotlib import pyplot as plt

   # Memuat gambar
   img = cv2.imread('IMG20230705135355.jpg')

4. Deteksi Buah:
   Selanjutnya, untuk menggunakan metode pengolahan citra seperti segmentasi atau deteksi objek untuk mendeteksi buah pada gambar. Di sini, menggunakan segmentasi berdasarkan warna untuk memisahkan buah-buah dari latar belakang.

   # Konversi gambar ke skala warna HSV
   hsv_image = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)

   # Definisikan rentang warna untuk setiap buah
lower_orange = np.array([0, 50, 50])
upper_orange = np.array([20, 255, 255])

lower_red = np.array([160, 50, 50])
upper_red = np.array([179, 255, 255])

lower_green = np.array([21, 50, 50])  
upper_green = np.array([35, 255, 255])

   # Segmentasi berdasarkan warna
mask_orange = cv2.inRange(hsv_img, lower_orange, upper_orange)
mask_red = cv2.inRange(hsv_img, lower_red, upper_red)
mask_green = cv2.inRange(hsv_img, lower_green, upper_green)

   # Penghasilan gambar akan dipisah dengan background
result_orange = cv2.bitwise_and(img, img, mask=mask_orange)
result_red = cv2.bitwise_and(img, img, mask=mask_red)
result_green = cv2.bitwise_and(img, img, mask=mask_green)

   # Membersihkan dan menyatukan warna sesuai perintah
kernel = cv2.getStructuringElement(cv2.MORPH_ELLIPSE, (5, 5))
cleaned_mask_orange = cv2.morphologyEx(mask_orange, cv2.MORPH_OPEN, kernel)
cleaned_mask_red = cv2.morphologyEx(mask_red, cv2.MORPH_OPEN, kernel)
cleaned_mask_green = cv2.morphologyEx(mask_green, cv2.MORPH_OPEN, kernel)  

contours_orange, _ = cv2.findContours(cleaned_mask_orange, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
contours_red, _ = cv2.findContours(cleaned_mask_red, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
contours_green, _ = cv2.findContours(cleaned_mask_green, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)

   Setelah langkah ini,berisi gambar dengan buah-buah yang tersegmentasi dari latar belakang.

5. Visualisasi Hasil:
   Terakhir, memvisualisasikan gambar hasil segmentasi menggunakan matplotlib.

   # Menampilkan gambar asli dan hasil segmentasi
fig, axs = plt.subplots(2, 2, figsize=(10, 10)) 

axs[0, 0].imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
axs[0, 0].set_title('Gambar Asli')

axs[0, 1].imshow(cv2.cvtColor(result_orange, cv2.COLOR_BGR2RGB))
axs[0, 1].set_title('Jeruk')

axs[1, 0].imshow(cv2.cvtColor(result_red, cv2.COLOR_BGR2RGB))
axs[1, 0].set_title('Apel')

axs[1, 1].imshow(cv2.cvtColor(result_green, cv2.COLOR_BGR2RGB))
axs[1, 1].set_title('Mangga')

plt.tight_layout()

plt.show()
   plt.show()

   Jalankan semua code di Jupyter Notebook, dan Anda akan melihat empat gambar, yaitu gambar asli , gambar jeruk , gambar apel , dan gambar mangga.

