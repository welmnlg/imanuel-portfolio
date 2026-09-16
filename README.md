# Portfolio Imanuel M.T. Manullang

Website portfolio statis (HTML/CSS biasa, tanpa framework/build step), jadi paling
gampang di-deploy ke Vercel dan paling mudah kamu edit langsung di VS Code.

## Struktur folder

```
portfolio/
├── index.html              ← halaman utama
├── styles.css              ← semua styling
├── images/                 ← screenshot project (sudah diekstrak & dikompres dari PDF kamu)
└── projects/
    ├── gocampus.html        ← halaman detail Go Campus (belum ada link live)
    ├── ambiverse.html        ← halaman detail AmbiVerse (repo: github.com/welmnlg/ambiverse)
    └── pandhu.html           ← halaman detail Pandhu (belum ada link live)
```

## Cara pakai di VS Code

1. Extract `portfolio.zip`, buka foldernya di VS Code.
2. Kalau mau preview lokal, install extension **Live Server** lalu klik kanan
   `index.html` → "Open with Live Server". Atau cukup buka file `index.html`
   langsung di browser (klik dua kali), karena semua path di sini relatif
   dan tidak butuh server khusus.
3. Edit apa saja langsung di `index.html` / `styles.css`. Semua teks (about,
   achievements, sertifikat, dll) ada di `index.html`, gampang dicari karena
   sudah dikasih section yang jelas (`<section id="projects">`, dst).

### Yang mungkin masih perlu kamu sesuaikan
- Ganti favicon kalau mau (sekarang belum ada, cuma pakai logo teks "IM").
- Ganti tahun di footer (`© 2026 ...`) kalau perlu.
- Kalau ada project baru, tinggal copy salah satu blok `<a class="project-card">`
   di `index.html`, ganti gambar + teksnya.

---

## Deploy ke Vercel (gratis)

Cara paling gampang: lewat GitHub, supaya setiap kamu `git push` nanti,
Vercel otomatis update sendiri:

1. **Push folder ini ke GitHub**
   - Buat repo baru di GitHub (misal `imanuel-portfolio`), lalu di folder
     `portfolio/` jalankan:
     ```
     git init
     git add .
     git commit -m "Initial portfolio"
     git branch -M main
     git remote add origin https://github.com/<username>/imanuel-portfolio.git
     git push -u origin main
     ```

2. **Import ke Vercel**
   - Buka [vercel.com](https://vercel.com) → login/daftar pakai akun GitHub.
   - Klik **Add New → Project**, pilih repo `imanuel-portfolio` yang baru kamu push.
   - Framework preset: pilih **"Other"** (karena ini HTML statis biasa, bukan
     Next.js/React). Build command & output directory biarkan kosong/default,
     Vercel otomatis serve semua file HTML apa adanya.
   - Klik **Deploy**. Tunggu ~30 detik, selesai: kamu akan dapat URL gratis
     seperti `imanuel-portfolio.vercel.app`.

3. **Update berikutnya**
   - Setiap kali kamu `git push` ke branch `main`, Vercel otomatis re-deploy.
     Tidak perlu upload manual lagi.

**Alternatif tanpa GitHub:** install Vercel CLI (`npm i -g vercel`), lalu di
dalam folder `portfolio/` jalankan `vercel` dan ikuti instruksinya. Cocok
untuk deploy cepat sekali tanpa setup repo, tapi update berikutnya harus
`vercel --prod` manual setiap kali ada perubahan, jadi cara GitHub di atas
lebih direkomendasikan untuk jangka panjang.

---

## Soal project yang belum di-hosting (Go Campus, AmbiVerse, Pandhu)

Kamu minta diarahkan soal ini, ada 3 opsi, dari yang paling simpel:

### Opsi A: Halaman internal (sudah diterapkan, tidak perlu langkah tambahan)
Tiga project itu sekarang linknya mengarah ke halaman detail di situs yang
sama (`/projects/gocampus.html`, dst) yang menampilkan screenshot lebih besar
dan deskripsi lengkap. Ini otomatis ikut ke-deploy bareng situs utama, tidak
butuh setup tambahan. Cocok kalau project itu memang tidak punya kode yang
mau kamu publish sebagai web hidup (misal Go Campus yang sifatnya tugas
kuliah dengan dataset di Protégé, bukan web yang "jalan").

### Opsi B: Deploy tiap project sebagai project Vercel terpisah (gratis, tanpa domain)
Kalau project itu benar-benar berupa kode web (misal AmbiVerse atau Pandhu
yang berbasis Laravel/PHP), kamu bisa deploy masing-masing sebagai project
Vercel sendiri:
- Push kode masing-masing project ke repo GitHub-nya sendiri.
- Import juga ke Vercel seperti langkah di atas.
- Vercel otomatis kasih URL gratis seperti `ambiverse-imanuel.vercel.app`.
- Lalu di `index.html` portfolio utama, ganti `href="projects/ambiverse.html"`
  jadi `href="https://ambiverse-imanuel.vercel.app"`.

  ⚠️ Catatan: Laravel/PHP butuh backend server (bukan cuma static file), dan
  Vercel secara default lebih cocok untuk static site / Next.js. Untuk deploy
  Laravel, biasanya lebih gampang pakai layanan seperti Railway, Render, atau
  Heroku (ada free tier), bukan Vercel. Nanti tinggal link URL-nya ke sini
  sama seperti Opsi B di atas.

### Opsi C: Subdomain asli (butuh custom domain)
"Subdomain" seperti `ambiverse.imanuelmanullang.com` hanya bisa terjadi kalau
kamu **punya domain sendiri** (bukan domain gratis `.vercel.app` bawaan).
Kalau nanti beli domain (misal di Niagahoster/Namecheap):
1. Tambahkan domain itu ke project Vercel utama kamu (Settings → Domains).
2. Untuk tiap project terpisah (dari Opsi B), tambahkan juga sebagai custom
   domain dengan subdomain berbeda, misal `ambiverse.imanuelmanullang.com`,
   lalu atur DNS record (CNAME) sesuai instruksi yang muncul di Vercel.

Untuk sekarang, karena masih di hosting gratisan, **Opsi A sudah paling
praktis**, dan kamu bisa upgrade ke Opsi B/C kapan pun tanpa perlu ubah
struktur situs utama, cukup ganti link `href` di kartu project-nya.
