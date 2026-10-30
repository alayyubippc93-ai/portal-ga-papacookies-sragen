
# Portal GA - PAPACOOKIES Sragen - 4 CV 10 Toko

Dashboard dark-mode modern (background #0a0a0a) replika screenshot Antrean Promo, untuk General Affair.

## Struktur CV & Toko
1. CV Sifon Mas Sukowati - Sragen Kota
2. CV Amanah Utama Karya - Sragen Kota (Pesanan), Cantel, Sukodono
3. CV Sejahtera Seiring Sejalan - Masaran, Batu Jamus, Taman Asri
4. CV Gotangrejo - Gondang, Sambirejo, Tangen

## Cara Jalan
```
npm install
npm run dev
```
Buka http://localhost:3000

## Login Admin
Username: admin
Password: admin123
-> Untuk kelola database dan hapus/edit tiket.

## Integrasi Google Sheet (Gratis)
1. Buat Google Sheet baru: "DB GA PAPACOOKIES"
   Kolom: ID | Antrean | Toko | CV | Pelapor | Judul | Kategori | Prioritas | Status | Tanggal | FotoLink

2. Extensions > Apps Script > Paste code ini:

```javascript
function doPost(e){
  const sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  const data = JSON.parse(e.postData.contents);
  sheet.appendRow([data.id, data.antrean, data.tokoNama, data.cv, data.pelapor, data.judul, data.kategori, data.prioritas, data.status, data.tanggal, data.foto]);
  return ContentService.createTextOutput(JSON.stringify({ok:true})).setMimeType(ContentService.MimeType.JSON);
}
function doGet(){ 
  const sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  const rows = sheet.getDataRange().getValues();
  const headers = rows[0];
  const data = rows.slice(1).map(r=>{let o={}; headers.forEach((h,i)=>o[h]=r[i]); return o;});
  return ContentService.createTextOutput(JSON.stringify(data)).setMimeType(ContentService.MimeType.JSON);
}
```

3. Deploy > New Deployment > Web App > Anyone can access > Copy URL
4. Di app/page.tsx ganti fetch URL ke URL Apps Script kamu.

Setiap buat tiket otomatis masuk Sheet 10 toko.

## Deploy ke Vercel
- Push ke GitHub
- Import di Vercel.com
- Done.

Footer: © 2026 General Affair & Finance PAPACOOKIES Sragen
