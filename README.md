# Financial Transaction Reconciliation — Belajar dari Nol

Project ini akan dibangun bertahap agar setiap keputusan datanya dapat dipahami, bukan sekadar menjalankan pipeline yang sudah jadi.

## Studi kasus

Kita akan membandingkan:

- **Internal ledger:** nilai barang dan ongkir yang seharusnya ditagihkan.
- **Payment gateway:** nilai pembayaran yang benar-benar tercatat.

Dataset Olist tidak memiliki bank statement asli. Karena itu `order_payments` digunakan sebagai proxy payment-gateway. Kita tidak akan mengklaim anomaly sebagai fraud tanpa bukti tambahan.

## Roadmap

| Tahap | Hasil | Status |
|---|---|---|
| 1. Data profiling | Memahami schema, key, grain, missing value, dan kualitas amount | Sedang dikerjakan |
| 2. Data preparation | Memilih 50.000 order dan membersihkan sumber | Belum |
| 3. Reconciliation | Internal vs gateway pada grain satu order | Belum |
| 4. SQL layer | SQLite tables dan reporting views | Belum |
| 5. Power BI | Executive Overview dan Exception Detail | Belum |

Kita hanya melanjutkan tahap berikutnya setelah hasil tahap sebelumnya sudah dipahami dan tervalidasi.

## Environment

Jalankan dari PowerShell:

```powershell
cd D:\Course\Porto\Scratch
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
jupyter lab
```

Jika memakai kernel Python yang sudah memiliki pandas dan Jupyter, pembuatan virtual environment boleh dilewati.

## Tahap yang sedang dikerjakan

Buka dan jalankan cell secara berurutan:

```text
notebooks/01_data_profiling.ipynb
```

Checkpoint yang diharapkan:

- orders: 99.441 baris;
- items: 112.650 baris;
- payments: 103.886 baris;
- duplicate primary/composite key: 0;
- order dengan lebih dari satu payment row: 2.961;
- zero-value payment rows: 9.

Jangan membuat join atau reconciliation sebelum memahami mengapa `order_id` tidak unik di tabel items dan payments.
