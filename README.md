# DukunAds — file unduhan

Repo ini tempat nyimpen file yang diunduh app **DukunAds**. Kode app-nya nggak ada di sini (repo kodenya
private). Yang ada di sini cuma rilis file unduhan, plus script kecil dan workflow GitHub Actions buat nyalin
runtime AI dan model dari sumber resminya.

| Rilis | Isi |
|---|---|
| `components-v<N>` | runtime AI (llama.cpp) dan salinan cadangan model AI yang diunduh app di layar Setup. Rilis pertama nyusul di Sprint 2. |
| `app-v<versi>` | installer app. Nyusul pas DukunAds rilis. |

## Komponen app (`components-v<N>`)

- **Runtime AI** diunduh app dari rilis ini.
- **Model AI** diunduh app langsung dari Hugging Face: alamatnya dikunci ke satu commit, dan tiap file dicek
  SHA-256-nya. Salinan di rilis ini cuma cadangan, dipakai kalau sumber di Hugging Face hilang atau gagal.
- **File di atas 2 GiB** (batas GitHub per file rilis) dipotong jadi beberapa bagian `<nama>.part<N>`, masing-masing
  di bawah 2 GiB. App nyambung lagi bagian-bagian itu, lalu ngecek SHA-256 file utuhnya.
- **Isi rilis yang udah jadi nggak pernah diubah.** Komponen baru = rilis baru.

### Keamanan

- Rilis dibikin GitHub Actions yang **cuma bisa dijalanin manual** (`workflow_dispatch`) oleh pemilik repo. Nggak
  ada pemicu dari push, pull request, atau fork.
- Sebelum diupload, tiap file dicek SHA-256-nya dan **harus sama persis dengan yang dikunci di app**. Beda satu
  byte = nggak diupload, dan workflow-nya gagal.
- Ukuran dan SHA-256 semua file, termasuk tiap potongan, dicatat di `components-v<N>.lock.json`.

## Lisensi

Tiap rilis bawa teks lisensi file-filenya, dan halaman rilisnya nyebut lisensi tiap file. Model AI cuma dipakai
kalau lisensinya ngebolehin dipakai di produk berbayar dan disebar ulang.
