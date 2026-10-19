# UTS Graf Sains Data: Neo4j dan Sistem Rekomendasi (RetailRocket)

Mata kuliah Graf Sains Data, Prodi S1 Sains Data, Universitas Negeri Surabaya (Gasal 2026/2027).

## Isi repositori
| File | Isi |
|---|---|
| `01_Soal_Pendahuluan.ipynb` | Tugas pendahuluan 1.1 s.d. 1.3 (environment, driver Neo4j, impor data) |
| `02_Soal_UTS.ipynb` | Soal UTS 2.1 (Wrangling dan EDA) dan 2.2 (Analytics) |
| `data/events_p1.csv` | Data interaksi periode P1 (training) |
| `data/events_p2.csv` | Data interaksi periode P2 (testing / ground truth) |
| `img/` | Gambar hasil notebook (dibuat saat notebook dijalankan) |
| `requirements.txt` | Dependensi Python |

`events.csv` asli (RetailRocket, Kaggle: retailrocket/ecommerce-dataset) tidak diunggah karena ukurannya besar.

## Periode yang dipilih
| | Periode | Jumlah event |
|---|---|---|
| P1 (training) | 15 s.d. 28 Mei 2015 | 304.718 |
| P2 (testing) | 29 Mei s.d. 4 Juni 2015 | 145.321 |

Timestamp dataset adalah unix epoch milidetik dan diperlakukan sebagai UTC.

## Cara menjalankan
1. Jalankan Neo4j (Neo4j Desktop), buat instance, dan catat password.
2. `python -m venv myenv`, aktifkan, lalu `pip install -r requirements.txt`.
3. Letakkan `events.csv` dan ubah variabel `SRC` pada sel konfigurasi `02_Soal_UTS.ipynb`.
4. Buka notebook di VS Code, pilih kernel `myenv`, lalu *Restart* dan *Run All*. Password Neo4j diminta lewat kotak input.

## Ringkasan metode
- **Graf:** `(:Visitor)-[:VIEWED | :ADDED_TO_CART | :BOUGHT]->(:Item)`.
- **VSM:** matriks user x item dengan bobot view = 1, addtocart = 3, transaction = 5; kemiripan memakai cosine.
- **Proyeksi:** Item-Item dipilih (lebih ringkas dan cocok untuk rekomendasi item).
- **Rekomendasi:** item-based KNN (k = 5), top-5 untuk evaluasi, 3 teratas diiklankan.
- **Evaluasi:** Hit@5 dan NDCG@5; ground truth = item baru yang diinteraksikan user di P2.
- **Reproducibility:** pemilihan user acak memakai `numpy.random.default_rng(42)`.
