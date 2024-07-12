# PCD_UAS_202231065_M-Rizky-Ramadhan
# import library 
```python
import cv2
import numpy as np
from matplotlib import pyplot as plt
```
Untuk mengimpor pustaka yang diperlukan untuk membaca, memanipulasi, dan menampilkan citra dalam Python. Kombinasi OpenCV, NumPy, dan Matplotlib sangat umum dalam aplikasi pemrosesan citra.. <br>
```python
image = cv2.imread('IMG_8494.jpg')
```
Fungsi ini untuk membaca citra dari file yang diberikan dan menyimpannya ke dalam variabel image untuk pemrosesan lebih lanjut. <br>
```python
# Median Filtering
median_filtered = cv2.medianBlur(image, 5)
```
Kode di atas berfungsi untuk menerapkan median filtering pada citra yang dibaca dan menyimpan hasilnya dalam variabel median_filtered untuk pemrosesan atau analisis lebih lanjut. <br>
```python
# Menampilkan hasil
plt.figure(figsize=(10, 5))
plt.subplot(1, 2, 1), plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB)), plt.title('citra asli')
plt.subplot(1, 2, 2), plt.imshow(cv2.cvtColor(median_filtered, cv2.COLOR_BGR2RGB)), plt.title('After Median Filtering')
plt.show()
```
Kode ini berfungsi untuk menampilkan dua citra secara berdampingan citra asli dan citra hasil dari proses median filtering. Ini memudahkan perbandingan visual antara citra sebelum dan sesudah median filtering, sehingga kita bisa melihat efek dari filtering tersebut pada citra. <br>
```python
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
```
Kode ini berfungsi untuk mengonversi citra berwarna yang dibaca dalam variabel image menjadi citra grayscale dan menyimpannya dalam variabel gray_image. Konversi ke grayscale sering dilakukan dalam banyak aplikasi pemrosesan citra karena citra grayscale lebih sederhana untuk diproses dan dianalisis dibandingkan dengan citra berwarna. <br>
```python
def mean_filter(image, kernel_size):
    # Mendapatkan dimensi gambar
    h, w = image.shape
    
    # Membuat padding untuk gambar
    pad_size = kernel_size // 2
    padded_image = cv2.copyMakeBorder(image, pad_size, pad_size, pad_size, pad_size, cv2.BORDER_CONSTANT, value=0)
    
    # Membuat hasil gambar kosong
    mean_filtered = np.zeros_like(image)
    
    # Melakukan mean filtering
    for i in range(h):
        for j in range(w):
            # Mengambil nilai dari kernel
            kernel = padded_image[i:i+kernel_size, j:j+kernel_size]
            mean_value = np.mean(kernel)
            mean_filtered[i, j] = mean_value
    
    return mean_filtered
```
Kode di atas berfungsi untuk mengiterasi setiap piksel dalam citra asli, mengambil kernel yang berpusat pada piksel tersebut, menghitung nilai rata-rata dari piksel dalam kernel, dan menetapkan nilai rata-rata ini ke piksel yang bersesuaian dalam citra hasil. Hasilnya adalah citra yang lebih halus dengan noise yang berkurang. <br>
```python
# Mean Filtering dengan kernel size 5
mean_filtered = mean_filter(gray_image, 5)
```
Kode di atas berfungsi untuk menerapkan mean filtering pada citra grayscale dengan kernel 5x5, menghasilkan citra yang lebih halus yang disimpan dalam variabel mean_filtered. <br>
```python
# Menampilkan hasil
plt.figure(figsize=(10, 5))
plt.subplot(1, 2, 1), plt.imshow(gray_image, cmap='gray'), plt.title('Original Image')
plt.subplot(1, 2, 2), plt.imshow(mean_filtered, cmap='gray'), plt.title('Mean Filtered')
plt.show()
```
Kode di atas digunakan untuk membandingkan visual antara citra asli dan citra yang telah diproses dengan mean filtering. Dengan cara ini, kita dapat melihat efek dari penghalusan citra yang diterapkan oleh mean filtering. <br>
