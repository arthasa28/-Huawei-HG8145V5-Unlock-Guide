# Huawei HG8145V5 & EG8145V5 Unlock Guide

Panduan ini menjelaskan langkah-langkah untuk membuka (unlock) modem **Huawei HG8145V5** dan **EG8145V5** yang masih terkunci oleh provider sehingga menu seperti **WAN** dan **Software Upgrade** dapat digunakan kembali.

> ⚠️ **Peringatan**
>
> Panduan ini hanya untuk keperluan edukasi dan teknisi yang memahami risiko modifikasi firmware. Kesalahan saat proses upgrade, downgrade, atau modifikasi firmware dapat menyebabkan modem gagal menyala (*brick*). Selalu lakukan backup konfigurasi modem sebelum memulai.

---

# Informasi Modem

| Item | Keterangan |
|------|------------|
| Device | HG8145V5 / EG8145V5 |
| Hardware Version | 26AD.A |
| Software Version | V5R022C10S197 |
| Provider | Telkom Indonesia |

### Kondisi Awal

- ❌ Menu WAN tidak tersedia
- ❌ Menu Software Upgrade tidak tersedia
- ✅ Masih dapat mengunggah (Upload) file konfigurasi

---

# Persiapan

Pastikan Anda sudah memiliki file berikut:

```text
2Config-DEFAULT.xml
R022.bin
Huawei-Downgrade-Tools.exe
HG8145V5-R020-212.bin
EG8145V5-R021-210.bin
Huawei-PON-Tools-HG8145V5.exe
RollBackCommand.bat
```

---

# Persiapan Laptop (Windows 10 & Windows 11)

Sebelum memulai proses unlock, lakukan pengecekan berikut.

## 1. Aktifkan Telnet Client

Huawei PON Tools menggunakan Telnet untuk berkomunikasi dengan modem.

### Cara Mengaktifkan

1. Tekan **Windows + R**
2. Ketik:

```text
optionalfeatures
```

3. Tekan **Enter**
4. Cari **Telnet Client**
5. Beri tanda centang (**✔**)
6. Klik **OK**
7. Tunggu proses instalasi selesai

---

## 2. Jalankan Semua Tools Sebagai Administrator

Semua aplikasi berikut **WAJIB** dijalankan menggunakan **Run as Administrator**.

- Panda Flasher
- Huawei-Downgrade-Tools.exe
- Huawei-PON-Tools-HG8145V5.exe
- RollBackCommand.bat

Caranya:

> Klik kanan aplikasi → **Run as administrator**

---

## 3. Gunakan DHCP Terlebih Dahulu

Pastikan adapter Ethernet menggunakan:

```text
Obtain an IP address automatically (DHCP)
```

Jika Ethernet tetap muncul:

```text
Identifying...
```

atau

```text
Unidentified Network
```

Gunakan IP Static sementara.

Contoh:

| Pengaturan | Nilai |
|------------|--------|
| IP Address | 192.168.100.100 |
| Subnet Mask | 255.255.255.0 |
| Gateway | 192.168.100.1 |

---

## 4. Jika Panda Flasher Tidak Menampilkan Progress

Apabila Panda Flasher:

- Tidak ada progress
- Tidak muncul status upload
- Berhenti di 0%

Silakan **matikan sementara Windows Defender Firewall**.

Setelah proses selesai, aktifkan kembali Firewall.

---

## 5. Gunakan Kabel LAN Langsung

Disarankan:

- Kabel Cat5e atau Cat6
- Hubungkan Laptop langsung ke Modem
- Jangan melalui Router atau Switch

---

## 6. Nonaktifkan VPN

Pastikan VPN berikut tidak aktif.

- Cloudflare WARP
- ZeroTier
- Tailscale
- OpenVPN
- WireGuard

---

# Akses Halaman Konfigurasi Modem

Sebelum melakukan upload file konfigurasi, pastikan Anda dapat mengakses halaman WebUI modem.

## HG8145V5

Buka browser kemudian akses:

```text
http://192.168.100.1
```

Login menggunakan salah satu akun berikut.

| Username | Password |
|----------|----------|
| telecomadmin | admintelecom |
| Support | theworldinyourhand |
| Admin | admin |

---

## EG8145V5

Sebagian besar modem **EG8145V5** menggunakan alamat IP:

```text
http://192.168.18.1
```

Login menggunakan:

| Username | Password |
|----------|----------|
| Epadmin | adminEp |

> **Catatan**
>
> Apabila halaman login tidak dapat dibuka:
>
> - Pastikan Laptop terhubung langsung ke modem.
> - Gunakan DHCP terlebih dahulu.
> - Jika masih belum mendapatkan IP, gunakan IP Static sesuai subnet modem.

---

## Setelah Berhasil Login

Apabila halaman konfigurasi Huawei sudah berhasil terbuka, lanjutkan ke proses berikutnya.

---

# Langkah 1 — Upload File Konfigurasi

Masuk ke menu **Configuration File** kemudian upload file berikut:

```text
2Config-DEFAULT.xml
```

Tunggu hingga modem selesai memproses upload.

---

# Langkah 2 — Upload File Shell

Upload file berikut.

```text
R022.bin
```

Melalui menu:

```text
Software Upgrade
```

## Jika Menu Software Upgrade Tidak Ada

Gunakan aplikasi:

```text
Panda Flasher
```

untuk mengunggah file tersebut.

---

# Langkah 3 — Downgrade Firmware

> **Catatan**
>
> Jika firmware modem masih **R021** atau lebih lama, langkah ini dapat dilewati.

Jalankan:

```text
Huawei-Downgrade-Tools.exe
```

Modem akan restart.

Setelah modem menyala kembali:

- Login kembali ke WebUI.
- Tampilan Web berubah menjadi **Merah**.
- Akan muncul menu **Firmware Upgrade**.

## Untuk HG8145V5

Upload firmware:

```text
HG8145V5-R020-212.bin
```

Tunggu modem restart.

---

## Untuk EG8145V5

Upload firmware:

```text
EG8145V5-R021-210.bin
```

Tunggu modem restart.

> **Catatan**
>
> Pada beberapa modem **EG8145V5**, setelah proses downgrade selesai, alamat IP modem akan kembali menjadi:
>
> ```text
> http://192.168.18.1
> ```
>
> Login kembali menggunakan:
>
> | Username | Password |
> |----------|----------|
> | Epadmin | adminEp |
>
> Setelah berhasil masuk ke halaman konfigurasi Huawei, **upload kembali file berikut**:
>
> ```text
> 2Config-DEFAULT.xml
> ```

---

# Langkah 4 — Jalankan Huawei PON Tools

Buka:

```text
Huawei-PON-Tools-HG8145V5.exe
```

Lakukan secara berurutan.

1. Klik tombol **1**
2. Klik tombol **2**
3. Modem akan restart
4. Tunggu sekitar **10–20 detik** setelah lampu LAN menyala
5. Klik tombol **3**
6. Klik tombol **4**
7. Pilih salah satu mode:
   - GPON
   - EPON
   - XPON
8. Klik tombol **5**

Modem akan restart kembali.

---

# Langkah 5 — Rollback Firmware (Opsional)

Jika ingin mengembalikan firmware ke versi asli (**R022**), jalankan:

```text
RollBackCommand.bat
```

Firmware akan kembali ke versi bawaan, namun hasil unlock tetap dipertahankan.

---

# Hasil Setelah Unlock Berhasil

Apabila seluruh proses berhasil, maka:

- ✅ Tampilan WebUI berubah menjadi **Biru**
- ✅ Provider berubah menjadi **COMMON**
- ✅ Menu WAN muncul
- ✅ Menu Software Upgrade muncul
- ✅ Vendor Lock berhasil dihapus

---

# Update Program

## Update 08 Maret 2026

Versi:

```text
Huawei-PON-Tools-HG8145V5-20260328.exe
```

Perubahan:

- Remove Vendor Lock GPON (PTCL/Pakistan)
- Memperbaiki GPON Blink setiap 2–5 menit

---

## Update 14 April 2026

Versi:

```text
Huawei-PON-Tools-HG8145V5-20260414.exe
```

Perubahan:

- Perbaikan pilihan mode EPON
- Penambahan Remove Vendor Lock pada XPON

---

# Ringkasan Proses

```text
Persiapan Laptop
│
├── Enable Telnet Client
├── Run as Administrator
├── DHCP / Static IP
├── Disable Firewall (Jika Diperlukan)
└── Nonaktifkan VPN
        │
        ▼
Akses WebUI Modem
        │
        ▼
Login
        │
        ▼
Upload 2Config-DEFAULT.xml
        │
        ▼
Upload R022.bin
        │
        ▼
Downgrade Firmware (Jika R022)
        │
        ▼
Upload Config Lagi (Khusus EG Jika Diminta)
        │
        ▼
Huawei PON Tools
        │
        ▼
Pilih GPON / EPON / XPON
        │
        ▼
Restart
        │
        ▼
Unlock Berhasil
        │
        ▼
(Optional)
Rollback Firmware
```

---

# Troubleshooting

## Panda Flasher Tidak Ada Progress

- Jalankan sebagai Administrator
- Matikan sementara Windows Defender Firewall
- Gunakan kabel LAN langsung
- Pastikan IP Laptop sudah benar

---

## Menu Software Upgrade Tidak Muncul

Gunakan:

```text
Panda Flasher
```

untuk meng-upload:

```text
R022.bin
```

---

## Huawei PON Tools Tidak Bisa Connect

Periksa kembali:

- ✔ Telnet Client sudah aktif
- ✔ Firewall dimatikan sementara
- ✔ Jalankan sebagai Administrator
- ✔ Laptop mendapat IP dari modem
- ✔ VPN tidak aktif

---

## Setelah Downgrade Tidak Bisa Login

Untuk modem **EG8145V5**, coba akses:

```text
http://192.168.18.1
```

Login menggunakan:

```text
Username : Epadmin
Password : adminEp
```

Kemudian upload kembali:

```text
2Config-DEFAULT.xml
```

---

## Huawei PON Tools Berhenti di Tengah Proses

- Tunggu modem selesai restart
- Pastikan lampu LAN sudah menyala
- Tunggu sekitar 10–20 detik sebelum klik langkah berikutnya

---

# Disclaimer

Dokumen ini dibuat sebagai panduan teknis. Seluruh risiko akibat proses upgrade, downgrade, maupun modifikasi firmware menjadi tanggung jawab pengguna. Disarankan melakukan backup konfigurasi modem sebelum memulai.

---

**Author:** Artha Syarif Athaya  
**Version:** 2.1  
**Last Update:** July 2026
