# 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi

**Semester**: Genap / Tahun Ajaran 2024–2025

**Nama**: Ismi Nur Fadilah

**NIM**: 240202868

**Modul yang Dikerjakan**: Modul 3 – Manajemen Memori Tingkat Lanjut (Copy-on-Write dan Shared Memory)

---

## 📌 Deskripsi Singkat Tugas

Melakukan modifikasi kernel xv6 untuk mengimplementasikan:

  * Copy-on-Write Fork (CoW): Optimalisasi fork agar tidak langsung menyalin seluruh memori, melainkan hanya menyalin saat halaman diubah (write).

  * Shared Memory: Menambahkan syscall `shmget()` dan `shmrelease()` agar dua proses dapat berbagi satu halaman memori, mirip dengan System V Shared Memory.

---

## 🛠️ Rincian Implementasi

  ## Copy-on-Write (CoW)
  
* Menambahkan array `ref_count[]` dan fungsi `incref()` / `decref()` di `vm.c`

* Menambahkan flag `PTE_COW` di `mmu.h` untuk menandai halaman CoW

* Membuat fungsi `cowuvm()` di `vm.c` sebagai pengganti `copyuvm()`

* Mengubah `fork()` di `proc.c` agar menggunakan `cowuvm()`

* Menangani page fault dengan memeriksa `PTE_COW` di `trap.c`

* Mengubah semua `kalloc()`/ `kfree()` agar menggunakan reference counting yang sesuai

  ## Shared Memory ala System V
  
* Menambahkan struktur global `shmtab[]` di `vm.c` untuk menyimpan shared memory (maks. 16 entri)

* Membuat syscall `sys_shmget()` dan `sys_shmrelease()` di `sysproc.c`

* Menambahkan `syscall` number baru di `syscall.h`

* Menambahkan deklarasi syscall di `user.h` dan `usys.S`

---

## ✅ Uji Fungsionalitas

`cowtest`	Menguji fork() dengan teknik Copy-on-Write

`shmtest`	Menguji shmget() dan shmrelease() antar proses

---

## 📷 Hasil Uji

Lampirkan hasil uji berupa screenshot atau output terminal. Contoh:

### 📍 Output `cowtest`:

```
Child sees: Y
Parent sees: X
```

### 📍 Output `shmtest`:

```
Child reads: A
Parent reads: B
```
Hasil Screenshoot (Output `cowtest`) :

<img width="1478" height="540" alt="modul3a" src="https://github.com/user-attachments/assets/bbfaf676-cf9c-4971-b0cc-c58349ec787f" />

```
Hasil Screenshoot (Output `shmtest`) :

<img width="1471" height="723" alt="modul3b (2)" src="https://github.com/user-attachments/assets/050ac905-4db0-4b4a-b87e-1aeee156838f" />

```

## ⚠️ Kendala yang Dihadapi

  * Salah implementasi penanganan page fault menyebabkan panic kernel saat `fork()`

  * Lupa menghapus flag `PTE_COW` saat membuat salinan halaman menyebabkan infinite fault loop

  * Kesalahan pemetaan `shmget()` ke USERTOP menyebabkan proses menimpa stack

  * Refcount tidak dikurangi pada `exit()`, menyebabkan kebocoran memori (memory leak)


---

## 📚 Referensi

Tuliskan sumber referensi yang Anda gunakan, misalnya:

* Buku xv6 MIT: [https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf](https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf)
* Repositori xv6-public: [https://github.com/mit-pdos/xv6-public](https://github.com/mit-pdos/xv6-public)
* Stack Overflow, GitHub Issues, diskusi praktikum

---

