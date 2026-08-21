# Impor repo thread-twinkle-sync ke proyek ini

Repo `backuparisanto2-cloud/thread-twinkle-sync` bersifat publik dan memakai stack yang sama dengan proyek ini (TanStack Start + React + Tailwind + shadcn + Supabase/Lovable Cloud), jadi kodenya bisa disalin langsung tanpa konversi.

Isi aplikasi: manajemen kos/properti — halaman Kamar, Tenant, Denah, Fasilitas, Pendapatan, Pengeluaran, Laporan (ekspor PDF), splash screen, dan upload foto.

## Yang akan dilakukan

1. **Unduh isi repo** (arsip publik dari GitHub) ke sandbox dan salin ke proyek ini: `src/components`, `src/lib`, `src/routes`, `src/hooks`, `src/styles.css`, `src/router.tsx`, `src/start.ts`, `src/server.ts`, `public/`, `components.json`.
2. **Samakan dependensi**: baca `package.json` repo dan pasang paket yang belum ada (radix-ui, react-hook-form, zod, recharts, sonner, date-fns, pdf/jsPDF, dll).
3. **Aktifkan Lovable Cloud** di proyek ini (backend belum aktif di sini) lalu jalankan ulang 5 file migrasi SQL dari `supabase/migrations/` beserta `sql/tenant-profile.sql` supaya tabel, RLS, grant, dan storage bucket ikut terbentuk. File `src/integrations/supabase/*` dari repo diselaraskan dengan integrasi baru (URL/key proyek ini, bukan milik repo lama).
4. **Aset gambar**: file di `public/assets` (denah lantai, splash) ikut tersalin apa adanya. File `src/assets/*.asset.json` adalah penunjuk aset milik proyek lama; akan saya coba unduh dan unggah ulang ke proyek ini, dan jika gagal, referensinya diarahkan ke versi di `public/assets`.
5. **Cek jalan**: buka setiap rute di preview, perbaiki error impor/tipe, dan pastikan `/` menampilkan halaman utama aplikasi (bukan placeholder).

## Catatan teknis

- Repo memuat file `.env` berisi kredensial proyek Supabase lama — file itu **tidak** akan disalin. Proyek ini memakai environment Cloud sendiri.
- Data (isi tabel) tidak ikut terbawa, hanya struktur database. Kalau butuh data lama, perlu ekspor/impor terpisah dari proyek asal.
- Kunci API pihak ketiga (mis. fitur AI pada `expense-ai.functions.ts`) memakai Lovable AI Gateway proyek ini.
