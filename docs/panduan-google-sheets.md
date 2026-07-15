# 📊 Panduan Setup: Rekod Keputusan ke Google Sheets

Backend ni guna **Google Apps Script** — percuma, takyah server, takyah bayar apa-apa. Setiap kali anak habis kuiz atau menang/kalah level game, satu baris data akan masuk automatik dalam Google Sheet anda.

**Masa setup: ± 5 minit**

---

## Langkah 1: Buat Google Sheet baru

1. Pergi ke [sheets.google.com](https://sheets.google.com) → buat spreadsheet baru
2. Namakan cth: **"Rekod Matematik Anak"**
3. Di baris pertama (Row 1), taip header ni ikut turutan:

| A | B | C | D | E | F | G | H | I |
|---|---|---|---|---|---|---|---|---|
| Tarikh | Nama | Mod | Tajuk | Markah | Jumlah | Peratus | Masa (saat) | Status/Level |

---

## Langkah 2: Buka Apps Script

1. Dalam Sheet tadi, klik menu **Extensions → Apps Script**
2. Padam semua kod contoh yang ada
3. Copy & paste kod di bawah ni:

```javascript
function doPost(e) {
  try {
    var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
    var d = JSON.parse(e.postData.contents);

    sheet.appendRow([
      d.tarikh    || new Date().toLocaleString(),
      d.nama      || '',
      d.mod       || '',
      d.tajuk     || '',
      d.markah,
      d.jumlah,
      d.peratus,
      d.masa_saat || '',
      d.status    || d.level || ''
    ]);

    return ContentService
      .createTextOutput(JSON.stringify({ok: true}))
      .setMimeType(ContentService.MimeType.JSON);
  } catch (err) {
    return ContentService
      .createTextOutput(JSON.stringify({ok: false, error: String(err)}))
      .setMimeType(ContentService.MimeType.JSON);
  }
}
```

4. Tekan ikon 💾 **Save** (namakan projek cth: "MathBlok Backend")

---

## Langkah 3: Deploy sebagai Web App

1. Klik butang **Deploy → New deployment**
2. Klik ikon gear ⚙️ di sebelah "Select type" → pilih **Web app**
3. Setting PENTING:
   - **Execute as:** Me (email anda)
   - **Who has access:** **Anyone** ← *wajib pilih "Anyone", kalau tak app tak boleh hantar data*
4. Klik **Deploy**
5. Google akan minta kebenaran → klik **Authorize access** → pilih akaun anda → klik **Advanced → Go to (nama projek)** → **Allow**
6. Copy **Web app URL** yang diberikan — bentuknya macam ni:
   `https://script.google.com/macros/s/AKfycb.../exec`

---

## Langkah 4: Sambungkan dalam app

1. Buka app **MathBlok** → tekan ikon ⚙️ (Tetapan)
2. Isi **nama anak**
3. Paste **Web app URL** tadi dalam ruangan URL
4. Tekan **💾 Simpan**
5. Tekan **🧪 Hantar Data Ujian ke Sheet** → semak Sheet anda — kalau ada baris baru masuk, siap! ✅

---

## 💡 Tips analysis untuk ibu bapa

Bila data dah terkumpul, boleh buat dalam Sheet:

- **Pivot table** (Insert → Pivot table): purata peratus ikut Tajuk → nampak terus tajuk mana anak lemah
- **Chart** markah vs tarikh untuk satu tajuk → nampak trend improvement
- **Filter** `Mod = Kuiz` untuk fokus keputusan ujian sahaja (asingkan dari game)
- Column **Masa (saat)** berguna: markah tinggi + masa makin pendek = dah masterI tajuk tu

---

## ❓ Troubleshooting

| Masalah | Punca biasa | Penyelesaian |
|---|---|---|
| Data tak masuk | "Who has access" bukan Anyone | Deploy semula, pilih **Anyone** |
| Data tak masuk | URL salah / tak lengkap | Pastikan URL berakhir dengan `/exec` |
| Ubah kod Apps Script tapi tak jalan | Deployment lama masih aktif | **Deploy → Manage deployments → Edit ✏️ → Version: New version → Deploy** |
| Nak sheet berasingan bulan baru | - | Buat tab baru & set sebagai active sheet, atau ubah kod guna `getSheetByName('NamaTab')` |

**Nota keselamatan:** URL ni membenarkan sesiapa yang ada URL untuk tambah baris ke sheet anda (tulis sahaja, tak boleh baca/padam data). Jangan kongsi URL ni secara terbuka.
