# Halaman Jurnal Umum

Satu halaman baru yang menggabungkan seluruh transaksi keuangan aplikasi ke dalam satu buku jurnal, dan tersambung ke navigasi global.

## Sumber data (tanpa tabel baru)

Jurnal membaca data yang sudah ada:

- Pendapatan sewa kamar (tabel pemasukan tenant) → kategori **Pendapatan**
- Pendapatan lain-lain → kategori **Pendapatan**
- Semua pengeluaran (Belanja, Service/Perbaikan, Jasa, Iuran, Lain-lain) → kategori **Pengeluaran**

Setiap transaksi ditampilkan sebagai satu baris jurnal dengan: tanggal, keterangan, sumber (Sewa Kamar / Pendapatan Lain / nama kategori pengeluaran), metode/lokasi, dan nilai pada kolom Pendapatan atau Pengeluaran.

## Isi halaman `/jurnal`

- Kartu ringkasan: Total Pendapatan, Total Pengeluaran, Saldo (selisih) untuk rentang yang dipilih.
- Filter: rentang tanggal (bulan ini / bulan lalu / tahun ini / kustom), jenis (Semua, Pendapatan, Pengeluaran), kategori, dan pencarian teks.
- Tabel jurnal urut tanggal (terbaru dulu) dengan kolom Pendapatan, Pengeluaran, dan Saldo berjalan.
- Rekap per bulan: pendapatan, pengeluaran, laba/rugi bulanan.
- Ekspor CSV/Excel dan PDF memakai util ekspor yang sudah ada.
- Klik baris membuka detail transaksi asal (dialog ringkas berisi catatan, metode bayar, lampiran).

## Sinkronisasi global

- Menu "Jurnal Umum" ditambahkan ke navigasi utama (desktop + menu mobile) di AppShell.
- Halaman Ringkasan mendapat ringkasan singkat Pendapatan / Pengeluaran / Saldo dengan tautan ke Jurnal.
- Data memakai query key yang sama dengan halaman Pendapatan & Pengeluaran, sehingga penambahan/edit di halaman mana pun langsung memperbarui jurnal.

## Catatan teknis

- Route baru `src/routes/jurnal.tsx` + helper `src/lib/journal.ts` yang menormalkan `incomes`, `other_incomes`, dan `expenses` menjadi tipe `JournalEntry { id, date, description, kind: "pendapatan" | "pengeluaran", category, source, method, amount, refId }`.
- Pengambilan data lewat `useQuery` dengan `incomesQuery`, `otherIncomesQuery`, `expensesQuery` yang sudah ada; tidak ada migrasi database.
- `head()` sendiri untuk judul/deskripsi halaman jurnal.
