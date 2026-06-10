# 📦 Агуулахын бүртгэл

Офлайн-first барааны бүртгэл апп. Зураг авна → AI нэр таньна → IndexedDB-д хадгална → Google Sheets-д синк хийнэ.

## Онцлог
- 📷 Камер + галерейгаас зураг авах
- 🤖 AI-р нэр, ангилал автомат таних
- 📴 Офлайн ажиллана (IndexedDB)
- ☁ Google Drive + Sheets синк
- 📊 Excel (.xlsx) + HTML тайлан татах
- 📱 PWA — гар утасны дэлгэц дээр суулгах

---

## GitHub Pages-д тавих

```bash
# 1. Repository үүсгэх
git init
git add .
git commit -m "first commit"
git remote add origin https://github.com/ТАНЫ_НЭР/inventory-app.git
git push -u origin main

# 2. GitHub → Settings → Pages → Source: main branch → Save
# URL: https://ТАНЫ_НЭР.github.io/inventory-app/
```

---

## Google Cloud Console тохиргоо

### 1. Project үүсгэх
1. https://console.cloud.google.com → New Project
2. **APIs & Services → Enable APIs** дарж:
   - Google Drive API ✓
   - Google Sheets API ✓

### 2. OAuth Client ID үүсгэх
1. **APIs & Services → Credentials → Create Credentials → OAuth Client ID**
2. Application type: **Web application**
3. Authorized JavaScript origins:
   ```
   https://ТАНЫ_НЭР.github.io
   ```
4. Client ID-г хуулж аппын **Тохиргоо** хэсэгт оруулна

### 3. OAuth Consent Screen
1. **APIs & Services → OAuth consent screen**
2. User Type: **External**
3. App name, email оруулна
4. Scopes: `drive.file`, `spreadsheets`
5. Test users-т өөрийн Gmail нэмнэ

### 4. Google Sheets бэлдэх
1. https://sheets.google.com → Шинэ хүснэгт үүсгэх
2. URL-с ID хуулна: `https://docs.google.com/spreadsheets/d/**ЭНД_ID**/edit`
3. Аппын **Тохиргоо** хэсэгт оруулна

---

## Ашиглах дараалал

1. **Тохиргоо** → Client ID + Spreadsheet ID оруулна → Google-т нэвтэрнэ
2. **Бүртгэх** → Камер нээнэ → Зураг авна → AI нэр таньна → Нэмэх
3. Интернэттэй болоход → **Синк** → Drive-д зураг, Sheets-д мэдээлэл очно
4. **Гаргах** → Excel эсвэл HTML татна

---

## Техникийн бүтэц

```
index.html   — бүтэн апп (vanilla JS, IndexedDB, Google API)
sw.js        — Service Worker (офлайн кэш)
manifest.json — PWA тохиргоо
```

**Өгөгдөл хадгалалт:**
- Бүх бараа + зураг (base64) → браузерын IndexedDB
- Синк хийсний дараа зураг → Google Drive, мэдээлэл → Google Sheets
- Sheets-ийн зургийн баганад `=IMAGE("drive_url")` томъёо

**Хязгаар:**
- 500-1000 бараанд IndexedDB хангалттай (зургийн хэмжээнээс хамаарч ~200-800 MB)
- Нэг синк дээр олон зураг нэгэн зэрэг Drive-д upload хийнэ (дараалалтай)
