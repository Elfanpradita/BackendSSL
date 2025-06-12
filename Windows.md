# 🛠️ Panduan Setup HTTPS Lokal dengan mkcert di Windows

## 📋 Prasyarat

Sebelum memulai, pastikan Anda memenuhi persyaratan berikut:

1.  **PowerShell sebagai Administrator**
    Semua perintah dalam panduan ini harus dijalankan di **PowerShell dengan hak akses Administrator**.

2.  **Instalasi Chocolatey (Package Manager)**
    Chocolatey adalah package manager untuk Windows yang mempermudah instalasi `mkcert`.

    * **Cek Execution Policy**
        Jalankan perintah ini untuk melihat kebijakan eksekusi skrip Anda:
        ```powershell
        Get-ExecutionPolicy
        ```
        Jika hasilnya adalah `Restricted`, ubah menjadi `AllSigned` atau `Bypass` untuk sesi ini.
        ```powershell
        # Opsi 1: Mengizinkan skrip yang ditandatangani (lebih aman)
        Set-ExecutionPolicy AllSigned

        # Opsi 2: Bypass hanya untuk proses saat ini (paling umum untuk instalasi)
        Set-ExecutionPolicy Bypass -Scope Process -Force
        ```

    * **Instal Chocolatey**
        Jalankan perintah berikut untuk mengunduh dan menginstal Chocolatey:
        ```powershell
        [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('[https://community.chocolatey.org/install.ps1](https://community.chocolatey.org/install.ps1)'))
        ```

    * **Verifikasi Instalasi**
        Setelah instalasi selesai, **tutup dan buka kembali PowerShell sebagai Administrator**. Lalu, verifikasi dengan perintah:
        ```powershell
        choco
        ```
        Jika Chocolatey terinstal dengan benar, Anda akan melihat versinya.

---

## 🔧 Langkah-langkah Konfigurasi

### Langkah 1: Instalasi `mkcert`

Anda bisa menginstal `mkcert` menggunakan Chocolatey atau secara manual.

* **Opsi A: Melalui Chocolatey (Disarankan)**
    ```powershell
    choco install mkcert
    ```
### Langkah 2: Generate Sertifikat untuk Domain Lokal

Buat sertifikat untuk domain lokal yang Anda inginkan (misalnya, `pemweb.test`).

```powershell
# Buat folder khusus untuk menyimpan sertifikat (opsional tapi rapi)
mkdir C:\ssl
cd C:\ssl

# Generate sertifikat untuk satu atau lebih domain
# Ganti pemweb.test dengan domain yang Anda inginkan
mkcert pemweb.test
```
### Langkah 4: Tambahkan Domain ke File `hosts`
Agar domain lokal Anda (`pemweb.test`) mengarah ke `127.0.0.1` (komputer Anda), edit file `hosts`.

1.  Buka **Notepad** (atau editor teks lain) **sebagai Administrator**.
2.  Buka file yang berlokasi di:
    ```
    C:\Windows\System32\drivers\etc\hosts
    ```
3.  Tambahkan baris berikut di akhir file dan simpan:
    ```
    127.0.0.1  pemweb.test
    ```

---

## ✅ Langkah Selanjutnya: Konfigurasi Web Server

# Copy 2 kodingan yang ada ke kodingan laravelnya
