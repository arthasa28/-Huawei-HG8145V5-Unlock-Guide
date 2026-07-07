# Huawei HG8145V5 & EG8145V5 Unlock Guide

Panduan ini menjelaskan langkah-langkah untuk membuka (unlock) modem **Huawei HG8145V5** dan **EG8145V5** yang masih terkunci oleh provider sehingga menu seperti **WAN** dan **Software Upgrade** dapat digunakan kembali.

> ⚠️ **Peringatan**
>
> Panduan ini hanya untuk keperluan edukasi dan teknisi yang memahami risiko modifikasi firmware. Kesalahan saat proses upgrade atau downgrade dapat menyebabkan modem gagal menyala (brick). Lakukan backup konfigurasi modem sebelum memulai.

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

> **Sangat disarankan melakukan pengecekan berikut sebelum menjalankan proses unlock.**

## 1. Pastikan Telnet Client Sudah Aktif

Huawei PON Tools membutuhkan fitur **Telnet Client** pada Windows.

### Cara Mengecek

1. Tekan **Windows + R**
2. Ketik:

```text
optionalfeatures
```

3. Tekan **Enter**
4. Cari **Telnet Client**
5. Pastikan dalam keadaan **✔ Centang (Enabled)**

Jika belum aktif:

- Centang **Telnet Client**
- Klik **OK**
- Tunggu proses instalasi selesai.

---

## 2. Jalankan Semua Tools Sebagai Administrator

Semua aplikasi berikut **WAJIB** dijalankan menggunakan hak akses **Administrator**.

- Panda Flasher
- Huawei-Downgrade-Tools.exe
- Huawei-PON-Tools-HG8145V5.exe

Cara menjalankan:

> Klik kanan file → **Run as administrator**

Hal ini untuk menghindari kegagalan akses Telnet, Firewall, maupun hak akses jaringan.

---

## 3. Gunakan IP DHCP Terlebih Dahulu

Sebelum menghubungkan laptop ke modem, pastikan adapter Ethernet menggunakan:

```text
Obtain an IP address automatically (DHCP)
```

Jika status Ethernet masih muncul:

```text
Identifying...
```

atau

```text
Unidentified Network
```

Gunakan IP Static sementara, misalnya:

| Pengaturan | Nilai |
|------------|--------|
| IP Address | 192.168.100.100 |
| Subnet Mask | 255.255.255.0 |
| Gateway | 192.168.100.1 |

> **Catatan:** Sesuaikan dengan IP default modem apabila berbeda.

---

## 4. Jika Panda Flasher Tidak Menampilkan Progress

Gejala yang biasanya muncul:

- Tidak ada status upload
- Progress tetap 0%
- Tidak ada respon sama sekali

Silakan **sementara nonaktifkan Windows Defender Firewall**.

Cara cepat:

```
Windows Security
↓
Firewall & Network Protection
↓
Turn Windows Defender Firewall Off
```

Setelah proses unlock selesai, **aktifkan kembali Firewall** demi keamanan komputer.

---

## 5. Gunakan Kabel LAN yang Baik

Disarankan menggunakan:

- Kabel LAN Cat5e/Cat6
- Sambungkan langsung dari Laptop ke Port LAN Modem
- Jangan melalui Switch atau Router

---

## 6. Nonaktifkan VPN

Pastikan VPN seperti berikut tidak sedang aktif:

- Cloudflare WARP
- ZeroTier
- Tailscale
- OpenVPN
- WireGuard

VPN dapat mengganggu komunikasi antara tools dengan modem.

---

# Langkah 1 — Upload File Konfigurasi

Login ke modem menggunakan salah satu akun berikut.

| Username | Password |
|----------|----------|
| telecomadmin | admintelecom |
| Support | theworldinyourhand |
| Admin | admin |

Masuk ke menu **Configuration File**, kemudian upload file:

```text
2Config-DEFAULT.xml
```

Tunggu hingga proses selesai.

---

# Langkah 2 — Upload File Shell

Upload file berikut:

```text
R022.bin
```

melalui menu:

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
- Tampilan halaman berubah menjadi **Merah**.
- Menu **Firmware Upgrade** akan muncul.

### Untuk HG8145V5

Upload firmware:

```text
HG8145V5-R020-212.bin
```

Tunggu modem restart.

---

### Untuk EG8145V5

Upload firmware:

```text
EG8145V5-R021-210.bin
```

Tunggu modem restart.

---

## Jika IP Modem Berubah

Pada beberapa modem **EG8145V5**, alamat modem berubah menjadi:

```text
192.168.18.1
```

Login menggunakan:

| Username | Password |
|----------|----------|
| Epadmin | adminEp |

Kemudian upload kembali:

```text
2Config-DEFAULT.xml
```

---

# Langkah 4 — Jalankan Huawei PON Tools

Buka:

```text
Huawei-PON-Tools-HG8145V5.exe
```

Lakukan langkah berikut secara berurutan.

1. Klik tombol **1**
2. Klik tombol **2**
3. Tunggu modem restart
4. Setelah lampu **LAN menyala**, tunggu sekitar **10–20 detik**
5. Klik tombol **3**
6. Klik tombol **4**
7. Pilih mode:

- GPON
- EPON
- XPON

8. Klik tombol **5**

Modem akan restart kembali.

---

# Langkah 5 — Rollback Firmware (Opsional)

Jika ingin mengembalikan firmware ke versi asli **R022**, jalankan:

```text
RollBackCommand.bat
```

Rollback hanya mengembalikan firmware ke versi semula.

---

# Hasil Setelah Unlock Berhasil

Apabila seluruh proses berhasil:

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
Cek Laptop
│
├── Telnet Client Enabled
├── Run Administrator
├── DHCP / Static IP
├── Firewall (Jika Diperlukan)
└── Kabel LAN

        │
        ▼

Login Modem
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

Huawei PON Tools
        │
        ▼

Pilih GPON / EPON / XPON
        │
        ▼

Modem Restart
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

## Panda Flasher Tidak Berjalan

- Jalankan sebagai **Administrator**
- Matikan sementara Windows Defender Firewall
- Gunakan kabel LAN yang baik
- Pastikan IP Laptop sudah benar

---

## Menu Software Upgrade Tidak Muncul

Gunakan **Panda Flasher** untuk meng-upload file:

```text
R022.bin
```

---

## Huawei PON Tools Tidak Bisa Connect

Periksa:

- Telnet Client sudah aktif
- Firewall dimatikan sementara
- Jalankan sebagai Administrator
- Laptop mendapat IP dari modem
- VPN tidak aktif

---

## Setelah Downgrade Modem Tidak Bisa Diakses

Coba akses:

```text
http://192.168.18.1
```

Login:

```text
Username : Epadmin
Password : adminEp
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
**Version:** 2.0  
**Last Update:** July 2026
