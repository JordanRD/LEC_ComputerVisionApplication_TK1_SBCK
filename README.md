# Computer Vision - TK1

Proyek tugas kuliah Computer Vision (TK1).

---

## 📋 Prasyarat

- **Python**: `>= 3.14` (atau versi yang kompatibel)
- **Package Manager**: [`uv`](https://docs.astral.sh/uv/) (direkomendasikan) atau `pip`

---

## 🚀 Setup & Instalasi

### 1. Membuat Virtual Environment (Jika Belum Ada)

Jika folder `.venv` belum dibuat:

**Menggunakan `uv` (Direkomendasikan):**

```bash
uv venv
```

**Menggunakan `python` bawaan:**

```bash
python -m venv .venv
```

---

### 2. Mengaktifkan Virtual Environment (`venv`)

Pilih perintah aktivasi sesuai dengan sistem operasi dan terminal yang digunakan:

- **Windows (PowerShell):**

  ```powershell
  .venv\Scripts\Activate.ps1
  ```

  > **Tips**: Jika muncul kendala _Execution Policy_ di PowerShell, jalankan:
  >
  > ```powershell
  > Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope Process
  > ```

- **Windows (Command Prompt / CMD):**

  ```cmd
  .venv\Scripts\activate.bat
  ```

- **Linux / macOS (Bash / Zsh):**
  ```bash
  source .venv/bin/activate
  ```

---

### 3. Menginstall Dependencies

Setelah virtual environment aktif, instal seluruh dependensi proyek:

**Menggunakan `uv` (Direkomendasikan):**

```bash
uv sync
```

**Menggunakan `pip`:**

```bash
pip install -e .
```

_Atau instal dependensi secara langsung:_

```bash
pip install matplotlib numpy opencv-python
```

#### Dependensi yang Digunakan:

- **`opencv-python`**: Library utama pengolahan gambar dan Computer Vision
- **`numpy`**: Komputasi numerik dan manipulasi array matriks gambar
- **`matplotlib`**: Visualisasi data dan plotting gambar

---
