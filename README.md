# Experiment 2.1

**Penjelasan Singkat:**
Eksperimen ini menjalankan kode dasar aplikasi *broadcast chat* berbasis *websocket* yang dibangun dengan `tokio` dan `tokio-websockets`. Proyek ini memiliki dua *binary*: 

1. **Server:** Bertugas menerima koneksi masuk, menerima pesan dari *client*, dan mengirim ulang (*broadcast*) pesan tersebut ke seluruh *client* yang terhubung menggunakan `tokio::sync::broadcast`.

2. **Client:** Bertugas membaca input dari pengguna (via `stdin`) untuk dikirim ke *server*, sekaligus membaca pesan yang datang dari *server* untuk ditampilkan ke layar.

**Cara Menjalankan:**
1. Buka satu terminal (berperan sebagai *host*) dan jalankan *server* dengan perintah:
```bash
cargo run --bin server
```

2. Buka dua atau lebih terminal baru dan jalankan client di masing-masing terminal dengan perintah:

```bash
cargo run --bin client
```

## Observasi (Apa yang Terjadi?):
Ketika saya mengetikkan pesan (misalnya "test") di salah satu terminal client lalu menekan Enter, pesan tersebut akan dikirim melalui websocket ke server.

Di dalam server, blok tokio::select! menangkap pesan tersebut dan melemparkannya ke broadcast channel. Channel ini kemudian mendistribusikan pesan ke semua subscriber (koneksi client lain). Hasilnya, pesan yang saya ketik langsung muncul seketika di semua terminal client yang sedang aktif.

Screenshot Hasil Eksekusi:


## Terminal 1
cargo run --bin server :
![alt text](image.png)

## Terminal 2
cargo run --bin client :
![alt text](image-1.png)

## Terminal 3
cargo run --bin client :
![alt text](image-2.png)