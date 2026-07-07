# Huawei HG8145V5 & EG8145V5 Unlock Guide

Panduan ini menjelaskan langkah-langkah untuk membuka (unlock) modem **Huawei HG8145V5** yang masih terkunci oleh provider sehingga menu seperti **WAN** dan **Software Upgrade** dapat digunakan kembali.

> ⚠️ **Peringatan**
>
> Panduan ini hanya untuk keperluan edukasi dan teknisi yang memahami risiko modifikasi firmware. Kesalahan saat proses upgrade atau downgrade dapat menyebabkan modem gagal menyala (brick).

---

# Informasi Modem

| Item | Keterangan |
|------|------------|
| Device | HG8145V5 |
| Hardware Version | 26AD.A |
| Software Version | V5R022C10S197 |
| Provider | Telkom Indonesia |

### Kondisi Awal

- ❌ Menu WAN tidak tersedia
- ❌ Menu Software Upgrade tidak tersedia
- ✅ Masih dapat mengunggah (upload) file konfigurasi

---

# Persiapan

Pastikan Anda sudah memiliki file berikut:

```
2Config-DEFAULT.xml
R022.bin
Huawei-Downgrade-Tools.exe
HG8145V5-R020-212.bin
EG8145V5-R021-210.bin
Huawei-PON-Tools-HG8145V5.exe
RollBackCommand.bat
```

---

# Langkah 1 — Upload File Konfigurasi

Login ke modem menggunakan akun berikut:

| Username | Password |
|----------|----------|
| telecomadmin | admintelecom |
| Support | theworldinyourhand |
| Admin | admin |

Masuk ke menu **Configuration File** kemudian upload file:

```
2Config-DEFAULT.xml
```

Tunggu hingga proses selesai.

---

# Langkah 2 — Upload File Shell

Upload file berikut:

```
R022.bin
```

Melalui menu:

```
Software Upgrade
```

### Jika menu Software Upgrade tidak tersedia

Gunakan aplikasi:

```
Panda Flasher
```

untuk melakukan upload file tersebut.

---

# Langkah 3 — Downgrade Firmware

> **Catatan**
>
> Jika firmware modem masih **R021** atau versi yang lebih lama, langkah ini dapat dilewati.

Jalankan aplikasi:

```
Huawei-Downgrade-Tools.exe
```

Modem akan melakukan restart.

Setelah modem hidup kembali:

- Login kembali ke halaman modem.
- Tampilan halaman akan berubah menjadi **warna merah**.
- Akan muncul menu **Firmware Upgrade**.

### Untuk tipe HG

Upload firmware:

```
HG8145V5-R020-212.bin
```

Tunggu modem restart.

---

### Untuk tipe EG

Upload firmware:

```
EG8145V5-R021-210.bin
```

Tunggu modem restart.

---

### Jika IP modem berubah

Pada beberapa tipe **EG**, setelah downgrade alamat modem berubah menjadi:

```
192.168.18.1
```

Login menggunakan:

| Username | Password |
|----------|----------|
| Epadmin | adminEp |

Kemudian upload kembali file:

```
2Config-DEFAULT.xml
```

---

# Langkah 4 — Jalankan Huawei PON Tools

Buka aplikasi:

```
Huawei-PON-Tools-HG8145V5.exe
```

Kemudian lakukan langkah berikut secara berurutan:

1. Klik tombol **1**
2. Klik tombol **2**
3. Modem akan restart
4. Tunggu sekitar **10–20 detik** setelah lampu LAN menyala
5. Klik tombol **3**
6. Klik tombol **4**
7. Pilih mode yang sesuai:
   - GPON
   - EPON
   - XPON
8. Klik tombol **5**

Modem akan restart kembali.

---

# Langkah 5 — Rollback (Opsional)

Jika ingin mengembalikan firmware ke versi bawaan (R022), jalankan:

```
RollBackCommand.bat
```

Langkah ini hanya mengembalikan firmware ke versi asli setelah proses unlock selesai.

---

# Hasil Setelah Berhasil Unlock

Jika seluruh proses berhasil, maka:

- ✅ Tampilan web berubah menjadi **warna biru**
- ✅ Informasi provider berubah menjadi **COMMON**
- ✅ Menu WAN muncul
- ✅ Menu Software Upgrade muncul
- ✅ Vendor Lock berhasil dihapus

---

# Update Program

## Update 08 Maret 2026

Versi:

```
Huawei-PON-Tools-HG8145V5-20260328.exe
```

Perubahan:

- Menghapus Vendor Lock GPON (PTCL/Pakistan)
- Memperbaiki masalah lampu GPON berkedip setiap 2–5 menit

---

## Update 14 April 2026

Versi:

```
Huawei-PON-Tools-HG8145V5-20260414.exe
```

Perubahan:

- Memperbaiki bug pilihan mode EPON
- Menambahkan penghapusan Vendor Lock pada mode XPON

---

# Ringkasan Proses

```text
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
Jalankan Huawei PON Tools
      │
      ▼
Pilih GPON / EPON / XPON
      │
      ▼
Modem Restart
      │
      ▼
Selesai Unlock
      │
      ▼
(Opsional)
Rollback ke Firmware Asli
```

---

# Troubleshooting

## Menu Software Upgrade tidak muncul

- Gunakan **Panda Flasher** untuk mengunggah file `R022.bin`.

---

## Setelah downgrade modem tidak dapat diakses

Coba akses:

```
http://192.168.18.1
```

Login menggunakan:

```
Username : Epadmin
Password : adminEp
```

---

## Huawei PON Tools berhenti di tengah proses

- Pastikan modem sudah selesai restart.
- Tunggu hingga lampu LAN menyala sebelum melanjutkan ke langkah berikutnya.
- Jalankan aplikasi sebagai **Administrator**.

---

# Disclaimer

Dokumen ini dibuat hanya sebagai panduan teknis. Segala risiko yang timbul akibat proses upgrade, downgrade, atau modifikasi firmware menjadi tanggung jawab pengguna. Selalu lakukan pencadangan (backup) konfigurasi modem sebelum memulai proses.

---

**Author:** Your Name  
**Version:** 1.0  
**Last Update:** July 2026
