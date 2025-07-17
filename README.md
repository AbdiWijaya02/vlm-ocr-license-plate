**# OCR License Plate Recognition with Visual Language Model (VLM)**



Proyek ini melakukan Optical Character Recognition (OCR) pada gambar plat nomor kendaraan menggunakan Visual Language Model (VLM) seperti `llava-phi-3-mini`, yang dijalankan melalui LM Studio dan diintegrasikan menggunakan bahasa pemrograman Python.



**# Deskripsi Proyek**



\- Mengirim gambar dari dataset ke LM Studio melalui HTTP API

\- Menggunakan model multimodal seperti `llava-phi-3-mini`

\- Prompt yang dikirim ke model:

&nbsp; > "What is the license plate number shown in this image? Respond only with the plate number."

\- Model membalas dengan hasil prediksi plat nomor

\- Hasil disimpan dalam format CSV dengan kolom:

&nbsp; - `image`, `ground\_truth`, `prediction`, `CER\_formula`, `CER\_score`

\- Evaluasi dilakukan dengan menghitung Character Error Rate (CER)





**# Struktur Folder**



```bash

Indonesian License Plate Recognition Dataset/

├── main.py                        # Script untuk kirim gambar ke LM Studio dan hasilkan hasil\_prediksi.csv

├── generate\_ground\_truth\_csv.py  # Script untuk ubah label .txt menjadi ground\_truth.csv

├── test/

│   ├── test001\_1.jpg             # Gambar plat nomor

│   ├── test001\_1.txt             # Label ground truth

│   └── ground\_truth.csv          # CSV berisi hasil penggabungan label

├── hasil\_prediksi.csv            # File output hasil OCR + evaluasi CER

├── requirement.txt

└── README.md



**# Instalasi \& Persiapan**

**1. Install LM Studio**

Unduh dan install dari:

&nbsp;https://lmstudio.ai/



Setelah itu, load model multimodal, contohnya yang saya pakai:

llava-phi-3-mini-gguf



**2. Jalankan Server LM Studio**

Buka terminal (Command Prompt):

cmd /c %USERPROFILE%/.lmstudio/bin/lms.exe bootstrap

lms server start

Jika berhasil, akan muncul:

Success! Server is now running on port 1234



**3. Install Library Python**

pip install -r requirements.txt



**# Eksekusi Program**

**1. Persiapan Dataset**

Pastikan folder test/ berisi gambar .jpg dan file .txt untuk label.



Contoh isi ground\_truth.csv:

image,ground\_truth

test001\_1.jpg,B9140BCD

test001\_2.jpg,B2407UZO

Gunakan generate\_ground\_truth\_csv.py untuk membuat file ground\_truth.csv secara otomatis dari file .txt.



**2. Jalankan Program Utama**

python main.py

Program akan melakukan:

Encode gambar ke Base64

Kirim ke LM Studio + prompt

Terima hasil prediksi

Hitung CER berdasarkan ground truth

Simpan hasil ke hasil\_prediksi.csv



\# Evaluasi: Character Error Rate (CER)

Rumus:

**CER = (S + D + I) / N**

Keterangan:

S: Jumlah karakter salah (substitusi)

D: Jumlah karakter dihapus (deletion)

I: Jumlah karakter disisipkan (insertion)

N: Jumlah karakter pada ground truth



Nilai CER menunjukkan seberapa jauh prediksi model dibandingkan label asli.



**# Contoh Output hasil\_prediksi.csv**

image,ground\_truth,prediction,CER\_formula,CER\_score

test001\_1.jpg,B9140BCD,B914OBCD,CER = (1 + 0 + 0) / 8,0.125

test001\_2.jpg,B2407UZO,B2407UZO,CER = (0 + 0 + 0) / 8,0.0



**# Upload ke GitHub**

**1. Buat Repository Baru**

Buka: https://github.com/new

Nama misalnya: vlm-ocr-license-plate



**2. Upload via Git**

cd path/ke/folder/Indonesian License Plate Recognition Dataset



git init

git remote add origin https://github.com/YOUR\_USERNAME/vlm-ocr-license-plate.git

git add .

git commit -m "Initial commit: OCR with VLM"

git branch -M main

git push -u origin main

Ganti YOUR\_USERNAME dengan username GitHub kamu.



**# Catatan Penting**

Pastikan LM Studio sudah menjalankan model multimodal saat menjalankan main.py



Jika terjadi error connection refused, pastikan LM Studio server sudah aktif dan port-nya sesuai (1234)



**Selesai**

Jika semua langkah dilakukan dengan benar, kamu akan mendapatkan file hasil\_prediksi.csv yang berisi hasil OCR + nilai akurasi dalam bentuk CER.

