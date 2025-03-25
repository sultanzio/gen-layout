# Generator Layout for Design

## 🔎 Ringkasan Fitur
- **Checklist Blok**: Pilih blok mana saja yang ditampilkan (3 required, 6 optional)  
- **Generate Layout Baru**: Mengacak posisi blok dalam grid  
- **Aspect Ratio**: Ubah rasio lebar‑tinggi container tanpa mengacak ulang layout  
- **Grid Gap**: Sesuaikan jarak antar‑blok (visual saja)  
- **Grid Overlay**: Garis pemisah antar‑sel berdasarkan gap  
- **Save as Image / PDF**: Ekspor hasil layout ke PNG atau PDF  

---

## 📊 Logika Layout & Hitungan Matematika

| Parameter | Definisi | Rumus / Penjelasan |
|-----------|----------|--------------------|
| columns | Jumlah kolom | Math.floor(Math.random()*4)+2 → integer antara 2–5 |
| visibleBlocks | Blok terpilih | Array hasil getSelectedBlocks() |
| rows | Jumlah baris minimal | max(3, ceil(visibleBlocks.length/columns) + rand(0–2)) |
| effectiveCellWidth | Lebar tiap sel | (containerWidth − gap*(columns−1)) ÷ columns |
| effectiveCellHeight | Tinggi tiap sel | (containerHeight − gap*(rows−1)) ÷ rows |
| gridGap | Jarak antar‑sel (px) | Nilai slider gapRange |
| aspectRatio | Rasio container | CSS aspect-ratio: width/height |

### Overlay Lines
- Vertical: xᵢ = i * effectiveCellWidth + (i − 0.5) * gap (i = 1…columns−1)  
- Horizontal: yⱼ = j * effectiveCellHeight + (j − 0.5) * gap (j = 1…rows−1)

---

## ⚙️ Alur GenerateRandomLayout()
1. Tentukan columns & kumpulkan visibleBlocks  
2. Hitung rows minimal  
3. Buat gridAreas[rows][columns]  
4. Tempatkan footer di baris terakhir; brand & CTA di atasnya  
5. Acak & tempatkan blok lain pakai isAreaFree()  
6. Terapkan grid-area ke CSS container  
7. Beri warna latar acak  
8. Simpan currentColumns & currentRows → drawOverlay()

---

## 💾 Ekspor
- **Save as Image**: html2canvas → PNG  
- **Save as PDF**: html2canvas + jsPDF → PDF  

---

## 📋 Checklist Blok

| Blok | Status |
|-------|---------|
| Brand / Logo | ✅ Required |
| Main CTA | ✅ Required |
| Footer | ✅ Required |
| Tagline | ☐ Optional |
| Visual Hook | ☐ Optional |
| Main Image | ☐ Optional |
| Main Text | ☐ Optional |
| Sub Text | ☐ Optional |
| Secondary CTA | ☐ Optional |
