# Panduan Setup HTTPS Lokal dengan mkcert di macOS

## 📋 UNTUK TUTORIAL VERSI MacOS ADA DI readme.md

Ini adalah panduan langkah demi langkah untuk menyiapkan environment development lokal yang menggunakan HTTPS di macOS dengan `mkcert`. Ini memungkinkan Anda untuk mengakses proyek lokal seperti `https://pemweb.test` langsung di browser tanpa peringatan keamanan.

## Prasyarat

-   [Homebrew](https://brew.sh/) terinstall di macOS Anda.

## Langkah-langkah Instalasi

### 1. Install `mkcert` di macOS

Gunakan Homebrew untuk menginstall `mkcert`. Jika Anda menggunakan browser Firefox, disarankan juga untuk menginstall `nss`.

```bash
brew install mkcert
brew install nss # Opsional, hanya jika Anda menggunakan Firefox
```

### 2. Install Root Certificate Authority (CA) Lokal

Langkah ini hanya perlu dilakukan **sekali saja**. `mkcert` akan membuat *Certificate Authority* (CA) lokal dan menginstalnya di *system trust store* macOS (dan juga di trust store Firefox jika `nss` terinstall).

```bash
mkcert -install
```

### 3. Generate Sertifikat untuk Domain Lokal

Buat direktori untuk menyimpan sertifikat Anda, lalu generate sertifikat untuk domain lokal yang Anda inginkan (contoh: `pemweb.test`).

```bash
# Buat dan masuk ke direktori SSL (misalnya di dalam folder Documents)
mkdir ssl
cd ssl

# Generate sertifikat untuk pemweb.test
mkcert pemweb.test
```

Perintah di atas akan menghasilkan dua file di direktori `~/Documents/ssl`:
-   `pemweb.test.pem` (file sertifikat)
-   `pemweb.test-key.pem` (file private key)

### 4. Tambahkan Domain Lokal ke `/etc/hosts`

Agar komputer Anda tahu bahwa `pemweb.test` harus mengarah ke server lokal Anda (127.0.0.1), tambahkan entri baru di file `/etc/hosts`.

1.  Buka file `/etc/hosts` dengan editor teks seperti `nano` (membutuhkan hak akses superuser).

    ```bash
    sudo nano /etc/hosts
    ```

2.  Tambahkan baris berikut di akhir file:

    ```
    127.0.0.1 pemweb.test
    ```

3.  Simpan dan tutup file. Jika menggunakan `nano`:
    -   Tekan `CTRL + X`
    -   Tekan `Y` untuk konfirmasi penyimpanan
    -   Tekan `ENTER` untuk menutup

---

## ✅ Langkah Selanjutnya: Konfigurasi Web Server

# Copy 2 kodingan sertif SSL yang ada ke kodingan laravelnya.
