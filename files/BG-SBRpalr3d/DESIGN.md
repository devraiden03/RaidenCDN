# DESIGN.md — VF Market (Etalase Kaca · palet "Kaca Malam")

Sumber kebenaran: `public/css/vf-tokens.css` proyek. Dokumen ini hanya merangkumnya untuk agen desain.

## 1. Tema & suasana
- Toko digital otomatis (nokos/OTP, panel Pterodactyl, script bot, APK premium, SMM).
- Metafora "etalase kaca di malam hari": permukaan kaca tipis, satu garis cahaya (LED) di tepi atas, bayangan nyaris tidak ada.
- Mobile-first (pengguna mayoritas HP). Padat informasi tetapi tenang. Mode gelap = bawaan; mode terang setara, bukan turunan.

## 2. Palet warna & peran
| Peran | Gelap (bawaan) | Terang | Fungsi |
|---|---|---|---|
| bg | #0a1220 | #eef2f8 | latar halaman |
| surface | #131d30 | #ffffff | kartu, sheet |
| surface-2 | #1a2740 | #f6f8fc | tombol sekunder, catatan |
| text | #eaf1fb | #0c1628 | teks utama |
| text-muted | #a7b6cc | #45526a | teks pendukung (lolos 4.5:1) |
| primary | #4c9bff | #1e5fd6 | aksi utama (Beli, Deposit), fokus |
| primary-contrast | #04142b | #ffffff | teks di atas primary |
| accent / warning | #ffc247 | #a35f00 | promo, pengumuman, lencana Upgrade |
| success | #3ddc97 | #0f7a4c | stok tersedia, server normal |
| danger | #ff8a8a | #c0262d | stok habis, server mati, Keluar |
| border | text 11% | text 12% | garis kartu |
| border-strong | text 34% | text 45% | input, tombol sekunder |
Status tidak boleh dibedakan oleh warna saja: tambah teks/bentuk (titik penuh vs cincin).

## 3. Tipografi
- UI & angka: Plus Jakarta Sans 400–800, `font-variant-numeric: tabular-nums` untuk harga.
- Judul/display: Bricolage Grotesque 700–800.
- Kode/terminal: JetBrains Mono 500.
- Skala (px): 12 · 13 · 14 · 15 (dasar) · 17 · 20 · 24 · 30. Input minimal 16px di HP (cegah zoom iOS).

## 4. Komponen
- **Kartu produk**: padding 8, radius 16–18; gambar **1:1 penuh, tidak dipotong** (contain + latar blur); nama maks 2 baris; harga tebal 17px (atau "Harga sesuai layanan" / "mulai Rp…"); baris stok + terjual; aksi: Detail (ikon 44px) + Beli (primary). Status: normal, populer, promo (harga coret), mulai dari, habis (abu, tombol nonaktif bergaris putus), segera hadir, tanpa gambar (ikon kategori), memuat (skeleton).
- **Dialog detail**: bottom sheet HP / dialog tengah 460px desktop; alas gambar **16:9** — foto 16:9 penuh, gambar 1:1 setinggi alas di atas latar blur; tombol Tutup + Beli sekarang menempel di bawah.
- **Chip kategori**: tinggi 40–44, aktif = isi warna teks (inverse) + ikon centang; tampilkan jumlah produk.
- **Tombol**: utama (primary), sekunder (surface-2 + border-strong), nonaktif (transparan + garis putus). Radius 12–14.
- **Topbar** lengket, **bottom nav** mengambang 5 item (Beranda, Riwayat, Deposit, CS, Masuk/Profil), **laci menu** HP dengan jebakan fokus + Esc.

## 5. Tata letak
- Spasi: 4 · 8 · 12 · 16 · 20 · 24 · 32 · 40.
- Radius: 12 (sm) · 14 (kontrol) · 16 (md) · 22 (lg) · 999 (pil).
- Grid produk: 2 kolom (<640px), 3 kolom (≥640), auto-fill min 176px di desktop. CSS Grid untuk makro, Flexbox untuk mikro.
- Desktop: sidebar setinggi halaman penuh + konten max-width ±1180px.

## 6. Kedalaman & elevasi
- Kaca: `surface` 74% + `inset 0 1px 0` cahaya (sheen). Bayangan hanya untuk sheet/dialog (`0 18px 48px`).
- Hormati `prefers-reduced-transparency` (kaca → solid).

## 7. Boleh & jangan
- BOLEH: data nyata atau placeholder `[...]`; ikon garis (Bootstrap Icons di proyek); target sentuh ≥44px; fokus `:focus-visible` 2px primary offset 2px.
- JANGAN: gradien berlebihan, kartu bergaris kiri, emoji sebagai ikon, angka karangan, memotong gambar produk, animasi width/height/margin/top/left, overlay a11y.

## 8. Responsif
- Breakpoint: 640px (3 kolom), 1024px (sidebar desktop, laci ditutup otomatis).
- HP lebar acuan 390px (uji juga 320 & 430). Kolom HP dibatasi 600px di layar ≥640 bila memakai tata letak HP.

## 9. Panduan prompt agen
- Durasi gerak: tekan 100ms · umpan balik 150 · status 180 · masuk 240 · keluar 180. Easing keluar `cubic-bezier(.23,1,.32,1)`, sheet `cubic-bezier(.32,.72,0,1)`.
- Gerak hanya `transform`/`opacity`, dibungkus `@media (prefers-reduced-motion: no-preference)`.
- Aksesibilitas WCAG 2.1 AA: kontras teks 4.5:1, aria lengkap, navigasi keyboard penuh.
- Output kode harus cocok dengan stack: Express + EJS + CSS biasa (token `--color-*` di atribut `[data-vf]`), tanpa framework JS.
