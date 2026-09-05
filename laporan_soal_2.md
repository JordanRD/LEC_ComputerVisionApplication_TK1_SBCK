# Laporan Soal 2 — Image Blending dan Chroma Keying

Implementasi pada `soal_2.ipynb` menggunakan `OpenCV`, `NumPy`, dan `Matplotlib`.

## a. Baca Dua Citra dengan OpenCV

- Citra dibaca dengan `cv2.imread()` dalam format BGR, lalu dikonversi ke RGB dengan `cv2.cvtColor(..., cv2.COLOR_BGR2RGB)` agar tampil benar di Matplotlib.
- Hasil:
  - Citra 1 (`assets/minion_green_screen.jpg`): shape `(1080, 1920, 3)` — objek Minion dengan latar hijau.
  - Citra 2 (`assets/monas_bg.jpeg`): shape `(667, 1000, 3)` — Monas sebagai latar pengganti.
- Kedua citra ditampilkan berdampingan dengan `plt.subplots(1, 2)`.

## b. Penggabungan Citra dengan `cv2.addWeighted`

- Karena ukuran berbeda, Citra 2 di-resize ke ukuran Citra 1 dengan `cv2.resize()`.
- Penggabungan memakai rumus:
  ```
  J = alpha * img1 + beta * img2 + gamma
  ```
  dengan `alpha = 0.7`, `beta = 0.3`, `gamma = 0`.
- Hasil blending menampilkan kedua citra secara transparan (overlay): Minion tetap dominan (70%), latar Monas terlihat samar (30%). Visualisasi 3 panel: Citra 1, Citra 2 (resized), Hasil Blending.

## c. Chroma Keying (Green Screen Matting)

Fungsi `chroma_key_green(img_rgb, background_rgb, a1=0.5)`:

1. Normalisasi kedua citra ke float `[0, 1]` dan resize background ke ukuran citra input.
2. Ekstrak kanal `R_I, G_I, B_I`.
3. Hitung alpha matte dengan asumsi latar hijau murni (`G_B = 1.0`):
   ```
   alpha = (B_I - a1 * (G_I - G_B)) / (a1 * G_B)
   ```
   lalu `clip` ke `[0, 1]`. Nilai `alpha ≈ 0` pada area hijau (latar), `≈ 1` pada objek foreground.
4. Koreksi kanal hijau foreground: `G_F = minimum(G_I, B_I / a1)` untuk menghilangkan sisa semburat hijau.
5. Kompositing dengan background:
   ```
   R_J = R_I + (1 - alpha) * Bg_R
   G_J = G_F + (1 - alpha) * Bg_G
   B_J = B_I + (1 - alpha) * Bg_B
   ```

- Output divisualisasikan 3 panel: Citra Asli (Green Screen), Alpha Matte (grayscale), Hasil Chroma Keying.
- Hasil: latar hijau Minion berhasil diganti dengan latar Monas secara bersih, objek Minion tetap utuh tanpa transparansi seperti pada `addWeighted`.
