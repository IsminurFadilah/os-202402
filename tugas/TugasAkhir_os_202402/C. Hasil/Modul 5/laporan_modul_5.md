# 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi
**Semester**: Genap / Tahun Ajaran 2024–2025
**Nama**: Ismi Nur Fadilah
**NIM**: 240202868
**Modul yang Dikerjakan**: Modul 5 – Audit dan Keamanan Sistem

---

## 📌 Deskripsi Singkat Tugas

Modul 5 – Audit dan Keamanan Sistem:
Melakukan perluasan terhadap kernel xv6 untuk merekam setiap system call yang dijalankan oleh proses, serta menyediakan system call `get_audit_log()` yang memungkinkan proses dengan PID 1 untuk membaca log system call tersebut.

---

## 🛠️ Rincian Implementasi

  ## Audit Log System Call
  
  * Menambahkan struktur `audit_entry` dan array `audit_log[]` di `syscall.c` untuk menyimpan log.

  * Menambahkan kode logging di dalam fungsi `syscall()` agar setiap system call valid dicatat `(PID, nomor syscall, dan tick)`.

  * Menambahkan system call baru `get_audit_log()` untuk membaca isi log secara terbatas.

  ## System Call get_audit_log()
  
  * Menambahkan deklarasi syscall di:

    * `user.h`: termasuk juga definisi ulang `struct audit_entry`

    * `usys.S`: `SYSCALL(get_audit_log)`

    * `syscall.c`: pendaftaran di array `syscalls[]`

  * Mengimplementasikan fungsi `sys_get_audit_log()` di `sysproc.c`:

  ## Integrasi Build & Testing

  * Menambahkan file uji `audit.c` untuk membaca dan menampilkan log

  * Menambahkan `_audit\` di bagian `UPROGS` Makefile

---

## ✅ Uji Fungsionalitas

`audit`	Menampilkan semua system call yang tercatat di log

---

## 📷 Hasil Uji

### 📍 Output jika dijalankan sebagai PID ≠ 1:

```
Access denied or error.

```
Hasil Screenshoot:

<img width="1220" height="791" alt="modul5A" src="https://github.com/user-attachments/assets/21d31ad0-6e0c-48b0-b308-5be8e3783933" />

### 📍 Output jika dijalankan sebagai PID = 1 (init):

```
=== Audit Log ===  
[0] PID=1 SYSCALL=7 TICK=7 
[1] PID=1 SYSCALL=15 TICK=19  
[2] PID=1 SYSCALL=17 TICK=22
...  

```
Hasil Screenshoot:

<img width="878" height="952" alt="modul5B" src="https://github.com/user-attachments/assets/da76ffa1-541e-40a6-be9d-f3a879757e6f" />

## ⚠️ Kendala yang Dihadapi

  * Ukuran log tetap terbatas (maks. 128 entri), perlu manajemen rotasi untuk log besar

  * Struktur `audit_entry` perlu disamakan di kernel dan user (duplikasi di user.h)

  * `audit.c` harus dijalankan sebagai proses pertama (init), sehingga perlu mengubah `init.c`



---

## 📚 Referensi

Tuliskan sumber referensi yang Anda gunakan, misalnya:

* Buku xv6 MIT: [https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf](https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf)
* Repositori xv6-public: [https://github.com/mit-pdos/xv6-public](https://github.com/mit-pdos/xv6-public)
* Stack Overflow, GitHub Issues, diskusi praktikum

---

