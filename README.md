# Proyek Deploy Aplikasi Profile

##Buat Bucket
1. Navigation Menu → Cloud Storage → Buckets → Create Buckets
2. Beri nama bucket sesuai keinginan → continue
3. Pilih region → asia-southeast2 (Jakarta) → continue
4. Storage class biarkan saja → continue
5. Hapus centang pada “Enforce public access prevention on this bucket” → pilih fine-grained → continue
6. Create

### Tampilan ketika masuk ke bucket
1. Upload files
2. Pilih semua **gambar** yang digunakan project
3. Masuk ke menu **PERMISSIONS**

#### Permissions
1. Grant Access
2. New Principals → isi dengan allUsers
3. Role → Storage Object Viewer
4. **Save → Allow Public Access**
5. Kembali ke bucket details
6. Copy URL pada salah satu file
7. Paste link tersebut pada incognito tab, pastikan menampilkan gambar yang diinginkan
8. Jika gambar tidak tampil atau terdapat pesan error maka ulangi pada bagian langkah **Grant Access**

## Masukkan URL gambar ke dalam code
Sebelumnya code pada project : 
```
<img src="img/me.png" alt="Iqbal Image">
```
Sesudah gambar dimasukan dalam storage/bucket :
```
<img src="https://storage.googleapis.com/web-portofolio-iqbal/me.png" alt="Iqbal Image">
```
Lakukan ini terhadap line code yang digunakan untuk menampilkan gambar

*URL gambar didapatkan dari **Copy URL** dari bucket

## Buat app.yaml di dalam folder project anda
### Masukkan code di bawah ini ke dalam app.yaml
```
runtime: python27
api_version: 1
threadsafe: true

handlers:
- url: /
  static_files: index.html
  upload: index.html

- url: /(.*)
  static_files: \1
  upload: (.*)
```

### Pilih salah satu

- Push ke repository github
    - Jika memilih push ke github maka perlu melakukan perintah **git clone** menggunakan **cloud shell**
        
        git clone <link repository>
        
- Upload folder melalui cloud shell

### Masukkan perintah ini ke cloud shell

1. cd <nama folder>
2. gcloud app create --region=asia-southeast2
3. gcloud app deploy

Jika sudah selesai di deploy

1. gcloud app browse
2. Klik link yang ditampilkan
3. Ini adalah link web yang sudah dideploy

Atau dapat masuk ke App Engine → pojok kanan atas terdapat URL web yang sudah dideploy
