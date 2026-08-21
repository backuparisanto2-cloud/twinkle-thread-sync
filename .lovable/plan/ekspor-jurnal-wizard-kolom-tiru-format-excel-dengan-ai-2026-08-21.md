# Ekspor Jurnal: Wizard Kolom + Tiru Format Excel dengan AI

Menambahkan alur ekspor bertahap pada halaman Jurnal Umum: pilih periode, atur kolom, opsional unggah contoh format Excel agar AI menirunya, lalu unduh.

## Alur wizard (dialog 3 langkah)

Tombol "Ekspor Jurnal" membuka dialog:

1. **Periode** — preset (Bulan ini, Bulan lalu, Tahun ini, Semua) atau rentang tanggal kustom (dari–sampai), terpisah dari filter tabel sehingga bisa mengekspor periode lain tanpa mengubah tampilan. Menampilkan jumlah transaksi dan total pendapatan/pengeluaran/saldo untuk periode terpilih.
2. **Kolom** — daftar kolom jurnal yang bisa:
   - diurutkan naik/turun,
   - diganti nama header,
   - dihapus dari ekspor dan ditambahkan kembali,
   - disimpan/muat sebagai preset (tersimpan di perangkat).
   Kolom tersedia: Tanggal, Keterangan, Jenis, Kategori, Sumber, Metode/Lokasi, Catatan, Pendapatan (Debit), Pengeluaran (Kredit), Nominal, Saldo Berjalan, Nomor Urut.
3. **Format & unduh** — opsi judul laporan, sertakan baris total, sertakan rekap bulanan, lalu pilih Excel (.xlsx), CSV, atau PDF.

## Tiru format Excel lewat gambar (AI)

Di langkah 2 ada panel "Tiru format Excel". Pengguna mengunggah tangkapan layar / foto jurnal Excel yang biasa dipakai. AI membaca gambar dan mengembalikan:

- daftar header kolom sesuai urutan pada gambar beserta perkiraan pemetaan ke data jurnal,
- judul laporan dan baris kop bila terbaca,
- gaya dasar: ada/tidaknya baris total, format angka rupiah, dan perataan kolom.

Hasilnya langsung mengisi editor kolom (nama + urutan + kolom aktif) sehingga masih bisa dikoreksi manual sebelum ekspor. Kolom yang tidak bisa dipetakan ditandai agar pengguna memilih sumber datanya. Bila AI gagal atau kredit habis, muncul pesan jelas dan susunan kolom saat ini tetap dipakai.

## Hasil file

- **Excel**: kop judul + periode, baris ringkasan, tabel sesuai susunan kolom, format Rupiah pada kolom nominal, baris total, dan sheet kedua "Rekap Bulanan" bila dipilih.
- **CSV**: struktur sama dalam teks.
- **PDF**: memakai gaya laporan yang sudah dipakai aplikasi (kop, garis, footer halaman).

## Catatan teknis

- `src/lib/journal-columns.ts` baru: definisi `JournalColumnKey`, label default, tipe nilai (teks/tanggal/mata uang), dan pembacaan nilai dari `JournalEntry` + saldo berjalan.
- `src/lib/journal-export.ts` baru: `exportJournalExcel`, `exportJournalCsv`, `exportJournalPdf` (memakai `xlsx`, `jspdf`, `jspdf-autotable` yang sudah terpasang) dengan bentuk meta mirip `src/lib/report-export.ts`.
- Preset kolom disimpan lewat pola `src/lib/report-presets.ts` dengan kunci penyimpanan terpisah untuk jurnal.
- `src/lib/journal-format-ai.functions.ts` baru: `createServerFn` POST yang mengirim gambar (data URL) ke Lovable AI Gateway (`google/gemini-2.5-flash`, blok `image_url`) dan mengembalikan JSON `{ title?, columns: [{ header, mapTo|null }], includeTotals, currencyFormat }`, mengikuti pola dan penanganan error 402/429 pada `src/lib/expense-ai.functions.ts`.
- Komponen baru `src/components/JournalExportDialog.tsx` (wizard) dan `src/components/JournalColumnEditor.tsx` (editor kolom, meniru pola `ReportColumnManager`).
- `src/routes/jurnal.tsx` hanya diubah untuk memasang tombol dan dialog; logika jurnal yang ada tidak berubah.
