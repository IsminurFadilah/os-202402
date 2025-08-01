# 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi

**Semester**: Genap / Tahun Ajaran 2024–2025

**Nama**: Ismi Nur Fadilah

**NIM**: 240202868

**Modul yang Dikerjakan**: Modul 1 – System Call dan Instrumentasi Kernel

---

## 📌 Deskripsi Singkat Tugas

* **Modul 1 – System Call dan Instrumentasi Kernel**:
  
  Pada Modul 1 ini, diminta untuk memodifikasi kernel xv6-public dengan menambahkan dua buah system call baru, yaitu:

  * `getpinfo(struct pinfo *ptable)`
    → Mengembalikan informasi proses yang sedang aktif, termasuk PID, ukuran memori, dan nama proses.

  * `getreadcount()`
    → Mengembalikan total jumlah pemanggilan fungsi `read()` sejak sistem boot.

Tugas ini melatih pemahaman dalam memodifikasi kernel, menambahkan system call, serta mengakses dan memanipulasi informasi proses di tingkat kernel. Selain itu, juga membuat program uji pada level user untuk menguji kedua system call yang telah dibuat.

## 🛠️ Rincian Implementasi

* Menambahkan dua system call baru `(getpinfo dan getreadcount)` di file `sysproc.c` dan mendaftarkannya di `syscall.c`

* Menambahkan nomor syscall di `syscall.h`, serta deklarasinya di `user.h` dan `usys.S`

* Membuat struktur struct pinfo di `proc.h` untuk menyimpan info proses aktif

* Menambahkan variabel global `readcount` di `sysproc.c` dan menginkrementasinya di fungsi `sys_read()` `(sysfile.c)`

* Membuat dua program uji user-level: `ptest.c` untuk `getpinfo` dan `rtest.c` untuk `getreadcount`

---

## ✅ Uji Fungsionalitas

Program uji yang digunakan pada Modul 1:

* `ptest` → untuk menguji system call `getpinfo()`, menampilkan daftar proses aktif beserta PID, ukuran memori, dan nama proses.

* `rtest` → untuk menguji system call `getreadcount()`, memastikan jumlah pemanggilan `read()` bertambah setelah melakukan input dari stdin.

---

## 📷 Hasil Uji

## Output ptest:
```
$ ptest
PID	MEM	NAME
1	12288 init
2	16384	sh
3	12288	ptest

```

## Output rtest:
```
$ rtest
Read Count Sebelum: 12
hello
Read Count Setelah: 13
```

Screenshoot Output modul 1:

<img width="946" height="534" alt="modul1_" src="https://github.com/user-attachments/assets/35c2a55c-e608-44fd-9192-2dba5be7e3c3" />

---

## ⚠️ Kendala yang Dihadapi

* Perlu memastikan struktur pinfo di file user `(ptest.c)` sama persis dengan yang didefinisikan di kernel `(proc.h)`, agar data tidak korup saat dikembalikan       dari `syscall`.
  
* Pada versi xv6-public, ptable_lock mungkin tidak didefinisikan, sehingga perlu menggunakan `ptable.lock` atau mengimplementasikan `spinlock` baru.
  
* Salah menaruh  `readcount++` di awal fungsi `sys_read()`
---

## 📚 Referensi

Tuliskan sumber referensi yang Anda gunakan, misalnya:

* Buku xv6 MIT: [https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf](https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf)
* Repositori xv6-public: [https://github.com/mit-pdos/xv6-public](https://github.com/mit-pdos/xv6-public)
* Stack Overflow, GitHub Issues, diskusi praktikum

---

