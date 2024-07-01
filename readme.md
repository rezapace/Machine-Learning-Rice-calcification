# Deskripsi
Proyek ini adalah implementasi deteksi jenis beras menggunakan model pembelajaran mesin. Dataset yang digunakan terdiri dari tiga bagian utama: train, test, dan val. Proyek ini bertujuan untuk mengklasifikasikan gambar beras ke dalam dua kategori: Arborio dan Jasmine.

# Kegunaan
Proyek ini berguna untuk:
- Melatih model pembelajaran mesin untuk mengenali dan mengklasifikasikan jenis beras berdasarkan gambar.
- Menguji performa model untuk memastikan akurasi dan keandalannya.
- Memvalidasi model untuk mengevaluasi kinerja pada data yang belum pernah dilihat sebelumnya.

# Fungsi
Fungsi utama dari proyek ini adalah:
- Menyediakan dataset yang diperlukan untuk pelatihan, pengujian, dan validasi model.
- Mengimplementasikan model pembelajaran mesin menggunakan TensorFlow dan Keras.
- Melatih model dengan data yang telah disediakan.
- Mengevaluasi model untuk mendapatkan metrik performa seperti akurasi dan confusion matrix.

# Bagaimana Menjalankan
Untuk menjalankan proyek ini, ikuti langkah-langkah berikut:

1. **Persiapan Lingkungan:**
   - Pastikan Anda memiliki Python dan Jupyter Notebook terinstal.
   - Instal paket yang diperlukan dengan menjalankan perintah berikut:
     ```python
     !pip install tensorflow scikit-learn matplotlib
     ```

2. **Unduh dan Ekstrak Dataset:**
   - Unduh dataset dari repositori dan ekstrak ke direktori yang sesuai:
     ```python
     !apt install unzip
     !unzip -q "/content/Rice_Image_Dataset.zip"
     ```

3. **Kloning Repositori:**
   - Kloning repositori yang berisi kode proyek:
     ```python
     !apt install git
     !git clone "https://github.com/rezapace/Machine-Learning-Rice-calcification"
     ```

4. **Definisikan Jalur Dataset:**
   - Tentukan jalur dataset dalam kode:
     ```python
     DATASET_PATH = "/content/Rice_Image_Dataset/"
     TRAIN_DIR = os.path.join(DATASET_PATH, 'train')
     VAL_DIR = os.path.join(DATASET_PATH, 'val')
     TEST_DIR = os.path.join(DATASET_PATH, 'test')
     SAVED_MODEL_DIR = "/content/Rice_Image_Dataset"
     ```

5. **Periksa Direktori:**
   - Pastikan direktori dataset ada:
     ```python
     def check_directory(path):
         if not os.path.exists(path):
             raise FileNotFoundError(f"Directory not found: {path}")

     try:
         check_directory(TRAIN_DIR)
         check_directory(VAL_DIR)
         check_directory(TEST_DIR)
         check_directory(SAVED_MODEL_DIR)
     except FileNotFoundError as e:
         print(e)
         raise
     ```

6. **Buat dan Latih Model:**
   - Definisikan dan latih model:
     ```python
     model = Sequential([
         Conv2D(16, (3,3), activation='relu', input_shape=(224, 224, 3)),
         MaxPooling2D(2, 2),
         Conv2D(32, (3, 3), activation='relu'),
         MaxPooling2D(2, 2),
         Conv2D(64, (3, 3), activation='relu'),
         MaxPooling2D(2, 2),
         Conv2D(256, (5,5), activation='relu'),
         MaxPooling2D(2,2),
         Flatten(),
         Dense(256, activation='relu'),
         Dense(2, activation='softmax')
     ])
     model.compile(loss="categorical_crossentropy", optimizer=RMSprop(learning_rate=1e-4, momentum=0.9), metrics=['accuracy'])

     history = model.fit(train_set, epochs=20, validation_data=val_set, callbacks=[reduce_lr, checkpoint_cb, early_stop_cb], verbose=2)
     model.save(os.path.join(SAVED_MODEL_DIR, 'final_model.h5'))
     ```

7. **Evaluasi Model:**
   - Evaluasi model menggunakan dataset pengujian:
     ```python
     best_model = load_model(os.path.join(SAVED_MODEL_DIR, "best_model.h5"))
     evaluate_model(best_model, test_set)
     ```

# Kesimpulan
Proyek ini menyediakan solusi untuk mengklasifikasikan jenis beras menggunakan model pembelajaran mesin. Dengan dataset yang terstruktur dan kode yang jelas, pengguna dapat dengan mudah melatih, menguji, dan memvalidasi model untuk mencapai hasil yang optimal. Proyek ini juga memberikan metrik performa yang membantu dalam mengevaluasi keandalan model.

urutan isi dari dataset
    - train 1-50
- test 51-100
- val 101-150

