# 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi

**Semester**: Genap / Tahun Ajaran 2024–2025

**Nama**: Ismi Nur Fadilah

**NIM**: 240202868

**Modul yang Dikerjakan**:  Modul 1 – System Call dan Instrumentasi Kernel

---

## 📌 Deskripsi Singkat Tugas

Pada modul ini saya menambahkan dua buah system call baru ke dalam kernel xv6:

 * getpinfo(): untuk mengambil daftar proses aktif beserta informasi seperti PID, ukuran memori, dan nama proses.

 * getreadcount(): untuk menghitung jumlah pemanggilan fungsi read() sejak sistem boot.

Modul ini bertujuan agar mahasiswa memahami cara menambahkan system call, mengakses informasi kernel, dan membuat instrumen pengujian sendiri.

---

## 🛠️ Rincian Implementasi

  * Menambahkan dua system call baru di file sysproc.c dan mendaftarkannya di syscall.c

  * Menambahkan entri syscall baru di syscall.h, user.h, dan usys.S

  * Membuat struktur struct pinfo di proc.h untuk menyimpan informasi proses

  * Menambahkan variabel global readcount di kernel dan menginkrementasinya di sys_read() (sysfile.c)

  * Membuat dua program uji user-level: ptest.c untuk getpinfo() dan rtest.c untuk getreadcount()

---

## ✅ Uji Fungsionalitas

Program uji yang digunakan:

  * ptest: untuk menguji getpinfo() — menampilkan informasi proses yang sedang berjalan

  * rtest: untuk menguji getreadcount() — menampilkan jumlah pemanggilan fungsi read() sebelum dan sesudah input stdin

---

## 📷 Hasil Uji
Hasil Uji ptest:

```

$ ptest
Child 1 selesai
Child 2 selesai
Parent selesai
$

```

<img width="829" height="592" alt="modul2" src="https://github.com/user-attachments/assets/381d931d-eaa4-4b41-9e91-6b6814b456ba" />

---

## ⚠️ Kendala yang Dihadapi

Tuliskan kendala (jika ada), misalnya:

* Salah implementasi `page fault` menyebabkan panic
* Salah memetakan alamat shared memory ke USERTOP
* Proses biasa bisa akses audit log (belum ada validasi PID)

---

## 📚 Referensi

Tuliskan sumber referensi yang Anda gunakan, misalnya:

* Buku xv6 MIT: [https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf](https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf)
* Repositori xv6-public: [https://github.com/mit-pdos/xv6-public](https://github.com/mit-pdos/xv6-public)
* Stack Overflow, GitHub Issues, diskusi praktikum

---

