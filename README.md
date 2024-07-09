# Pengolahan Citra Project UTS dan UAS

## Anggota Kelompok:

| No  | Nama                      | NIM       | Kelas     | Akun Github                                                  |
| --- | ------------------------- | --------- | --------- | ------------------------------------------------------------ |
| 1   |  Muhamad Rizqi Maulana | 312210360 | TI.22.A.4 | [@rizqimaulana04](https://github.com/rizqimaulana04)         |
| 2   | Dipca Anugrah     | 312210666 | TI.22.A.4 | [@DipcaAnugrah](https://github.com/DipcaAnugrah) |
| 3   | Hasbi Assidiki          | 312210448 | TI.22.A.4 | [@HasbiAssidiki](https://github.com/HasbiAssidiki)         |
| 4   | Maulana Zidan Perdana          | 312210463 | TI.22.A.4 | [@zidanperdana](https://github.com/zidanperdana)         |
## Daftar Isi

**[Project UTS](#project-uts)** <br>
**[Project UAS](#project-uas)**

## Paper Pengolahan Citra
> **Jurnal:** [Penerapan Algoritma _K-Means Clustering_ dan _Elbow Method_ untuk Segmentasi Citra Digital pada Berbagai Jenis Gambar](https://docs.google.com/document/d/1ZGCDCNelKymmnbvPHMWHaNhUQwwNXcfH1jZPuTMdp1c/edit?usp=sharing)

## Project UTS

### Face Eye Detection Camera & Uploaded Photos

This application uses Haar Cascades to detect faces and eyes in real-time from a webcam or from uploaded photos.

### Screenshot
![Screenshot 2024-07-05 183520](https://github.com/rizqimaulana04/Face_Eye_Detection/assets/115638135/47a58df0-fce5-41fd-a40e-ca1dc9aa74a3)  

### Prerequisites

Before you begin, ensure you have met the following requirements:
- Python 3.6 or higher
- `pip` package manager

### Installation

1. **Clone the repository:**

    ```sh
    git clone <repository_url>
    cd <repository_directory>
    ```

2. **Create a virtual environment (optional but recommended):**

    ```sh
    python -m venv venv
    source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
    ```

3. **Install the required packages:**

    ```sh
    pip install streamlit opencv-python-headless pillow numpy
    ```

4. **Download the Haar Cascade XML files:**

    Download the required Haar Cascade XML files for face and eye detection from the OpenCV repository:
    - [haarcascade_frontalface_default.xml](https://github.com/opencv/opencv/blob/master/data/haarcascades/haarcascade_frontalface_default.xml)
    - [haarcascade_eye.xml](https://github.com/opencv/opencv/blob/master/data/haarcascades/haarcascade_eye.xml)

    Save these files into a folder named `models` within your project directory.

5. **Create the Python script:**

    Save the following code in a file named `app.py`:

    ```python
    import cv2
    import streamlit as st
    import numpy as np
    from PIL import Image

    face_cascade = cv2.CascadeClassifier('models/haarcascade_frontalface_default.xml')
    eye_cascade = cv2.CascadeClassifier('models/haarcascade_eye.xml')

    def main():
        st.title("Face and Eye Detection App")
        st.write("Aplikasi ini menggunakan Haar Cascades untuk mendeteksi wajah dan mata secara real-time dari kamera video atau dari foto yang diunggah.")

        option = st.selectbox("Choose input source", ("Laptop Camera", "Upload Photo"))

        if option == "Laptop Camera":
            start_button = st.button("Start Camera")
            if start_button:
                run_camera_detection()

        elif option == "Upload Photo":
            uploaded_file = st.file_uploader("Choose an image...", type=["jpg", "jpeg", "png"])
            if uploaded_file is not None:
                image = Image.open(uploaded_file)
                image_np = np.array(image)

                gray = cv2.cvtColor(image_np, cv2.COLOR_RGB2GRAY)
                
                faces = face_cascade.detectMultiScale(gray, scaleFactor=1.1, minNeighbors=5, minSize=(30, 30))
                
                num_faces = len(faces)
                message_faces = f"Detected {num_faces} face(s) in the image."
                st.write(message_faces)

                for (x, y, w, h) in faces:
                    cv2.rectangle(image_np, (x, y), (x + w, y + h), (255, 0, 0), 2)  # Blue rectangle for faces
                    roi_gray = gray[y:y + h, x:x + w]
                    roi_color = image_np[y:y + h, x:x + w]
                    eyes = eye_cascade.detectMultiScale(roi_gray)
                    for (ex, ey, ew, eh) in eyes:
                        cv2.rectangle(roi_color, (ex, ey), (ex + ew, ey + eh), (0, 255, 0), 2)  # Green rectangle for eyes

                st.image(image_np, channels="RGB")

    def run_camera_detection():
        cap = cv2.VideoCapture(0)

        while True:
            ret, frame = cap.read()

            if not ret:
                break

            gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)

            faces = face_cascade.detectMultiScale(gray, scaleFactor=1.1, minNeighbors=5, minSize=(30, 30))

            for (x, y, w, h) in faces:
                cv2.rectangle(frame, (x, y), (x + w, y + h), (255, 0, 0), 2)  # Blue rectangle for faces
                roi_gray = gray[y:y + h, x:x + w]
                roi_color = frame[y:y + h, x:x + w]
                eyes = eye_cascade.detectMultiScale(roi_gray)
                for (ex, ey, ew, eh) in eyes:
                    cv2.rectangle(roi_color, (ex, ey), (ex + ew, ey + eh), (0, 255, 0), 2)  # Green rectangle for eyes

            cv2.imshow('Face and Eye Detection', frame)

            if cv2.waitKey(1) & 0xFF == ord('q'):
                break

        cap.release()
        cv2.destroyAllWindows()

    if __name__ == "__main__":
        main()
    ```

## Running the App

1. **Run the Streamlit app:**

    ```sh
    streamlit run app.py
    ```

2. **Interact with the app:**

    - **Laptop Camera:** Click "Start Camera" to begin real-time face and eye detection using your laptop's webcam.
    - **Upload Photo:** Upload a photo to detect faces and eyes within the image.

3. **Stop the app:**
    
    To stop the real-time detection from the webcam, press `q` in the displayed window.


## Project UAS

### Image Segmentation using K-Means Clustering with Streamlit

Repositori ini berisi aplikasi web Streamlit untuk melakukan segmentasi gambar menggunakan clustering K-Means. Segmentasi gambar adalah teknik untuk mempartisi suatu gambar menjadi beberapa segmen untuk menyederhanakan representasi suatu gambar atau membuatnya lebih bermakna untuk dianalisis.

### Tampilan

https://github.com/rizqimaulana04/UAS_PengolahanCitra/assets/115638135/fc854cde-1147-4530-abd7-1f999df548f0    


### Features

- **Upload Images:** Upload JPEG or PNG images to perform segmentation.
- **K-Means Clustering:** Choose the number of clusters (`k`) to segment the image colors.
- **Visualize Segmentation:** Display both the original and segmented images.
- **Color Clusters:** View the dominant colors extracted by K-Means clustering.

### Requirements

- Python 3.x
- Streamlit
- NumPy
- Matplotlib
- OpenCV (cv2)
- Pillow (PIL)

### Installation

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

### Penggunaan
- Unggah satu atau beberapa gambar.
- Sesuaikan jumlah cluster (k) untuk clustering K-Means.
- Jelajahi gambar asli dan tersegmentasi.
- Lihat warna dominan yang diekstraksi oleh setiap cluster.

<hr>

**[-> Back to Daftar isi](#daftar-isi)**
