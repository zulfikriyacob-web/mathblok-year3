# ✖️ MathBlok — Matematik Tahun 3, Jadi Satu Pengembaraan

Aplikasi pembelajaran Matematik Tahun 3 (KSSR) yang dwibahasa (BM/EN), penuh dengan infografik interaktif, sistem mastery sifir, permainan RPG bertema blok, dan laporan progress terus ke Google Sheets untuk ibu bapa.

Tiada backend server, tiada build step — 100% HTML/CSS/JS tulen, jalan terus dalam pelayar, sesuai untuk GitHub Pages.

**[🚀 Lihat demo langsung →](https://YOUR-USERNAME.github.io/mathblok/)**

---

## 📦 Apa yang ada dalam repo ini

```
mathblok-site/
├── index.html                    ← Landing page (produk showcase)
├── app/
│   └── index.html                ← Aplikasi utama MathBlok
├── games/
│   └── kembara-angkasa/
│       └── index.html            ← Bonus mini-game (Matematik + Sains)
├── docs/
│   ├── index.html                ← Panduan setup Google Sheets (versi web)
│   └── panduan-google-sheets.md  ← Panduan sama, versi Markdown
└── README.md
```

## ✨ Ciri-ciri

- **8 tajuk penuh** ikut silibus KSSR Tahun 3 — Nombor, Operasi Asas, Pecahan/Perpuluhan/Peratus, Wang, Masa, Ukuran, Geometri, Pengurusan Data
- **Infografik swipe-to-learn** — 48 kad visual (pizza pecahan, jam analog, neraca, poligon, carta) merentasi semua topik
- **Dojo Sifir** — sistem mastery 3 peringkat (Latih → Cabaran → Ujian Master bermasa) dengan "Cikgu Blok" yang jejak & ulang fakta lemah anak
- **BlokQuest** — permainan RPG 20 level; jawapan betul = serang raksasa, salah = hilang hati
- **Kedai Gear** — kumpul koin, upgrade avatar dengan topi/pedang/pet/aura yang memberi kesan sebenar (bukan cosmetic je)
- **Dwibahasa BM ⇄ EN** — satu butang, seluruh app (nota, soalan, tip, game) tukar bahasa serta-merta
- **Laporan Google Sheets** — setiap kuiz/sifir/game hantar automatik ke Google Sheet peribadi (bukan server pihak ketiga)
- **Bonus game** — Kembara Angkasa: perjalanan 5 planet menggabung Matematik + Sains untuk sesi cepat

## 🚀 Cara Deploy ke GitHub Pages

### Pilihan A — Upload terus melalui web (paling senang)

1. Buat repo baru di GitHub (cth: `mathblok`) — boleh public atau private (tapi GitHub Pages percuma perlukan public untuk repo biasa)
2. Buka repo → **Add file → Upload files**
3. Seret **kesemua fail & folder** dalam pek ini ke dalam kotak upload (kekalkan struktur folder — pelayar moden support drag folder terus)
4. Commit terus ke branch `main`
5. Pergi ke **Settings → Pages**
6. Bawah **Source**, pilih branch `main`, folder `/ (root)` → **Save**
7. Tunggu 1-2 minit, GitHub akan bagi URL macam `https://username.github.io/mathblok/`

### Pilihan B — Guna Git command line

```bash
cd mathblok-site
git init
git add .
git commit -m "Initial commit: MathBlok"
git branch -M main
git remote add origin https://github.com/USERNAME/mathblok.git
git push -u origin main
```

Kemudian aktifkan GitHub Pages macam Langkah 5-6 di atas.

### Nak host di subdomain sendiri (cth: mathblok.zuldevlab.my)?

1. Dalam repo, buat fail `CNAME` (tiada extension) kandungan: `mathblok.zuldevlab.my`
2. Di pembekal domain anda, tambah rekod DNS jenis **CNAME** menghala `mathblok` → `username.github.io`
3. Dalam **Settings → Pages**, masukkan custom domain yang sama, tunggu pengesahan DNS (boleh ambil sehingga 24 jam)

## 📊 Setup Rekod Google Sheets (untuk ibu bapa)

Rujuk `docs/index.html` (atau `docs/panduan-google-sheets.md`) — langkah penuh guna Google Apps Script, ± 5 minit setup, tiada kos.

## 🛠️ Nak edit / lanjutkan

Semua fail adalah HTML tulen dengan CSS + JavaScript vanilla terbenam (tiada build step, tiada `npm install`). Buka je fail dalam editor kod (VS Code dsb.) dan edit terus:

- Soalan/kandungan matematik → cari objek `GEN` dan `IG` dalam `app/index.html`
- Warna & tema → cari `:root { --sky: ... }` di bahagian atas `<style>`
- Tambah tajuk baru → tambah entri dalam array `TOPICS` + fungsi `GEN.tN()` dan `IG.tN()`

## 📄 Lesen

Percuma untuk kegunaan pendidikan peribadi. Dibina sepenuhnya dengan bantuan [Claude](https://claude.ai).

---

Dibina dengan 💙 · [zuldevlab.my](https://zuldevlab.my)
