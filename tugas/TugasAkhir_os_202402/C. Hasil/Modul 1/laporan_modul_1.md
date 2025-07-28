# 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi

**Semester**: Genap / Tahun Ajaran 2024–2025

**Nama**: Ismi Nur Fadilah

**NIM**: 240202868

**Modul yang Dikerjakan**:
Modul 1 – System Call dan Instrumentasi Kernel

---

## 📌 Deskripsi Singkat Tugas

* **Modul 1 – System Call dan Instrumentasi Kernel**:
* 
  Pada Modul 1 ini, diminta untuk memodifikasi kernel xv6-public dengan menambahkan dua buah system call baru, yaitu:

getpinfo(struct pinfo *ptable)
→ Mengembalikan informasi proses yang sedang aktif, termasuk PID, ukuran memori, dan nama proses.

getreadcount()
→ Mengembalikan total jumlah pemanggilan fungsi read() sejak sistem boot.

Tugas ini melatih pemahaman mahasiswa dalam memodifikasi kernel, menambahkan system call, serta mengakses dan memanipulasi informasi proses di tingkat kernel. Selain itu, mahasiswa juga diminta membuat program uji pada level user untuk menguji kedua system call yang telah dibuat.

## 🛠️ Rincian Implementasi

* Menambahkan dua system call baru (getpinfo dan getreadcount) di file sysproc.c dan mendaftarkannya di syscall.c

* Menambahkan nomor syscall di syscall.h, serta deklarasinya di user.h dan usys.S

* Membuat struktur struct pinfo di proc.h untuk menyimpan info proses aktif

* Menambahkan variabel global readcount di sysproc.c dan menginkrementasinya di fungsi sys_read() (sysfile.c)

* Membuat dua program uji user-level: ptest.c untuk getpinfo dan rtest.c untuk getreadcount

---

## ✅ Uji Fungsionalitas

Program uji yang digunakan pada Modul 1:

* ptest → untuk menguji system call getpinfo(), menampilkan daftar proses aktif beserta PID, ukuran memori, dan nama proses.

* rtest → untuk menguji system call getreadcount(), memastikan jumlah pemanggilan read() bertambah setelah melakukan input dari stdin.

---

## 📷 Hasil Uji

Output modul 1

<img width="831" height="541" alt="modul1" src="https://github.com/user-attachments/assets/a03466ba-aa16-4b2c-9c62-b6e0261f3ee0" />


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

