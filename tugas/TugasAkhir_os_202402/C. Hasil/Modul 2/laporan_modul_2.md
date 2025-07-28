# 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi

**Semester**: Genap / Tahun Ajaran 2024–2025

**Nama**: Ismi Nur Fadilah

**NIM**: 240202868

**Modul yang Dikerjakan**:  Modul 2 – Penjadwalan CPU Lanjutan

---

## 📌 Deskripsi Singkat Tugas

Mengubah algoritma penjadwalan bawaan xv6 dari Round Robin menjadi Non-Preemptive Priority Scheduling, di mana proses dengan prioritas numerik lebih kecil akan dipilih untuk dijalankan terlebih dahulu. Selain itu, ditambahkan system call `set_priority(int)` agar proses dapat mengatur prioritasnya sendiri.

---

## 🛠️ Rincian Implementasi

  * Menambahkan field int priority ke dalam struktur proc di `proc.h`

  * Menginisialisasi priority dengan nilai default `(misal 60)` di `allocproc()` `(proc.c)`

  * Menambahkan system call `set_priority()`:

      * Tambah deklarasi di `user.h` dan `syscall.h`

      * Tambah entri syscall di `usys.S` dan `syscall.c`

      * Implementasi fungsi `sys_set_priority()` di `sysproc.c`

  * Memodifikasi fungsi `scheduler()` di `proc.c` agar memilih proses `RUNNABLE` dengan prioritas tertinggi

  * Menyusun program uji user-level `(prio_test.c)` untuk menunjukkan bahwa proses dengan prioritas lebih tinggi dijalankan lebih awal

---

## ✅ Uji Fungsionalitas

Program uji yang digunakan:

  * `prio_test`: menguji `set_priority()` dan membuktikan bahwa proses dengan prioritas lebih tinggi dieksekusi terlebih dahulu

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
Screenshoot Output Modul 2:

<img width="829" height="592" alt="modul2" src="https://github.com/user-attachments/assets/381d931d-eaa4-4b41-9e91-6b6814b456ba" />

---

## ⚠️ Kendala yang Dihadapi

Tuliskan kendala (jika ada), misalnya:

  * Salah dalam memodifikasi `scheduler()` menyebabkan kernel tidak menjadwalkan proses apapun (infinite loop)

  * Lupa menambahkan validasi nilai prioritas pada system call `set_priority()` (harus 0–100)

  * `set_priority()` bekerja tetapi tidak berdampak karena prioritas tidak digunakan dalam `scheduler()` secara benar

  * Kesulitan membedakan kapan proses dianggap `RUNNABLE` atau sedang menunggu, menyebabkan pemilihan proses tidak akurat

---

## 📚 Referensi

Tuliskan sumber referensi yang Anda gunakan, misalnya:

* Buku xv6 MIT: [https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf](https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf)
* Repositori xv6-public: [https://github.com/mit-pdos/xv6-public](https://github.com/mit-pdos/xv6-public)
* Stack Overflow, GitHub Issues, diskusi praktikum

---

