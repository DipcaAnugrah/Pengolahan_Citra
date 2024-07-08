# Image Segmentation using K-Means Clustering with Streamlit

|  |  |  |
|-----|------|-----|
|Nama|Muhammad Rizqi Maulana|
|NIM|312210360|
|Kelas|TI.22.A.4|
|Mata Kuliah|Pengolahan Citra|
|Dosen Pengampu|Muhammad Fatchan, S.Kom., M.Kom., MTCNA.|

Repositori ini berisi aplikasi web Streamlit untuk melakukan segmentasi gambar menggunakan clustering K-Means. Segmentasi gambar adalah teknik untuk mempartisi suatu gambar menjadi beberapa segmen untuk menyederhanakan representasi suatu gambar atau membuatnya lebih bermakna untuk dianalisis.

## Tampilan

https://github.com/rizqimaulana04/UAS_PengolahanCitra/assets/115638135/fc854cde-1147-4530-abd7-1f999df548f0



## Features

- **Upload Images:** Upload JPEG or PNG images to perform segmentation.
- **K-Means Clustering:** Choose the number of clusters (`k`) to segment the image colors.
- **Visualize Segmentation:** Display both the original and segmented images.
- **Color Clusters:** View the dominant colors extracted by K-Means clustering.

## Requirements

- Python 3.x
- Streamlit
- NumPy
- Matplotlib
- OpenCV (cv2)
- Pillow (PIL)

## Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/rizqimaulana04/UAS_PengolahanCitra.git
   cd UAS_PengolahanCitra
   ```

2. Install dependencies:

    ```bash
    pip install -r requirements.txt
    ```

3. Run the Streamlit app:
    
    ```bash
    streamlit run app.py
    ```

## Penggunaan
- Unggah satu atau beberapa gambar.
- Sesuaikan jumlah cluster (k) untuk clustering K-Means.
- Jelajahi gambar asli dan tersegmentasi.
- Lihat warna dominan yang diekstraksi oleh setiap cluster.