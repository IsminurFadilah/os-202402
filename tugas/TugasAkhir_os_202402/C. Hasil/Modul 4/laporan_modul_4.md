# 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi

**Semester**: Genap / Tahun Ajaran 2024–2025

**Nama**: Ismi Nur Fadilah

**NIM**: 240202868

**Modul yang Dikerjakan**: Modul 4 – Subsistem Kernel Alternatif `(chmod()` `syscall` dan `/dev/random` device)

---

## 📌 Deskripsi Singkat Tugas

  Pada modul ini dilakukan dua modifikasi besar terhadap kernel xv6, yaitu:

* Menambahkan `system call` `chmod(path, mode)` untuk mengatur mode file menjadi read-only atau read-write.

* Menambahkan driver pseudo-device `/dev/random` yang menyediakan byte acak ketika dibaca.
  
---

## 🛠️ Rincian Implementasi

## System Call chmod(path, mode)

  * Menambahkan field `short mode` pada `struct inode@ di `fs.h`, tanpa menyimpan ke disk (hanya di memori).

  * Menambahkan `syscall sys_chmod()` di `sysfile.c`, menggunakan `ilock()` dan `iunlock()` untuk mengubah `inode->mode`.

  * Menambahkan definisi `syscall chmod` di:

    * `syscall.h` → `#define SYS_chmod 27`

    * `user.h` → `int chmod(char *path, int mode);`

    * `usys.S` → `SYSCALL(chmod)`

    * `syscall.c` → `extern int sys_chmod(void);` dan mapping pada `syscalls[]`

  * Memodifikasi `file.c`, tepatnya fungsi `filewrite()` agar menolak write jika `inode->mode == 1` (read-only)

## Device Driver /dev/random

  * Membuat file baru `random.c` berisi fungsi `randomread()` untuk menghasilkan byte acak menggunakan LCG (Linear Congruential Generator)

  * Mendaftarkan device di `file.c:`

    * Tambahkan deklarasi `extern int randomread(...)`

    * Tambahkan entri di array devsw[]: [3] = { randomread, 0 }

  * Menambahkan pemanggilan `mknod("/dev/random", 1, 3);` di `init.c` untuk membuat device node `/dev/random`

  * Menambahkan `random.c` ke dalam build xv6

## ✅ Uji Fungsionalitas

Tuliskan program uji apa saja yang Anda gunakan, misalnya:

* `ptest`: untuk menguji `getpinfo()`
* `rtest`: untuk menguji `getReadCount()`
* `cowtest`: untuk menguji fork dengan Copy-on-Write
* `shmtest`: untuk menguji `shmget()` dan `shmrelease()`
* `chmodtest`: untuk memastikan file `read-only` tidak bisa ditulis
* `audit`: untuk melihat isi log system call (jika dijalankan oleh PID 1)

---

## 📷 Hasil Uji

`chmodtest`	Menguji system call chmod()

`randomtest`	Membaca data acak dari /dev/random

### 📍 Output `chmodtest`:

```
Write blocked as expected
```
Hasil Screenshoot:

<img width="966" height="747" alt="modul4_" src="https://github.com/user-attachments/assets/e478e693-872d-4130-96ef-39eab1f31e97" />

### 📍Output randomtest:
```
159 114 41 116 67 198 109 232 
```

Hasil Screenshoot:

<img width="1452" height="554" alt="modul4__" src="https://github.com/user-attachments/assets/58bb1d1a-85e8-4942-a2a1-d7b11ae2d221" />


## ⚠️ Kendala yang Dihadapi

  * Salah index di array `devsw[]` menyebabkan error saat mengakses `/dev/random`

  * Lupa mengatur mode file pada inode menyebabkan `chmod` tidak berfungsi

  * `filewrite()` masih bisa menulis jika tidak dicegah eksplisit di `file.c`

  * Masalah saat `mknod()` dipanggil terlalu awal sebelum sistem file siap


---

## 📚 Referensi

Tuliskan sumber referensi yang Anda gunakan, misalnya:

* Buku xv6 MIT: [https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf](https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf)
* Repositori xv6-public: [https://github.com/mit-pdos/xv6-public](https://github.com/mit-pdos/xv6-public)
* Stack Overflow, GitHub Issues, diskusi praktikum

---

