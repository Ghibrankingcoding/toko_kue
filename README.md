# 🍰 Project Database Toko Kue

Project ini merupakan implementasi database sederhana menggunakan MySQL / MariaDB pada XAMPP untuk sistem penjualan toko kue.

---

## 🗄️ Membuat Database

```sql
CREATE DATABASE toko_kue;
USE toko_kue;
```

---

# 📦 Struktur Tabel

## 🎂 Tabel `kue`

```sql
CREATE TABLE kue(
    id_kue INT AUTO_INCREMENT PRIMARY KEY,
    nama_kue VARCHAR(100),
    harga INT,
    stok INT
);
```

Menambahkan kolom kategori:

```sql
ALTER TABLE kue ADD kategori VARCHAR(50);
```

---

## 👤 Tabel `pelanggan`

```sql
CREATE TABLE pelanggan(
    id_pelanggan INT AUTO_INCREMENT PRIMARY KEY,
    nama_pelanggan VARCHAR(15),
    no_hp VARCHAR(15),
    alamat VARCHAR(100)
);
```

---

## 🧾 Tabel `transaksi`

```sql
CREATE TABLE transaksi(
    id_transaksi INT AUTO_INCREMENT PRIMARY KEY,
    id_kue INT,
    id_pelanggan INT,
    jumlah INT,
    tanggal DATE
);
```

---

# 📥 Insert Data

## Data Kue

```sql
INSERT INTO kue(nama_kue, harga, stok, kategori) VALUES
('Brownies',30000,20,'Coklat'),
('Donat',5000,50,'Goreng'),
('Tart',150000,10,'Ulang Tahun'),
('Cupcake',10000,30,'Mini Cake'),
('Lapis Legit',80000,15,'Premium');
```

### 🔎 Output

```text
+--------+-------------+--------+------+-------------+
| id_kue | nama_kue    | harga  | stok | kategori    |
+--------+-------------+--------+------+-------------+
|      1 | Brownies    |  30000 |   20 | Coklat      |
|      2 | Donat       |   5000 |   50 | Goreng      |
|      3 | Tart        | 150000 |   10 | Ulang Tahun |
|      4 | Cupcake     |  10000 |   30 | Mini Cake   |
|      5 | Lapis Legit |  80000 |   15 | Premium     |
+--------+-------------+--------+------+-------------+
```

---

## Data Pelanggan

```sql
INSERT INTO pelanggan(nama_pelanggan, no_hp, alamat) VALUES
('Andi','081234567890','Jakarta'),
('Siti','082345678901','Bekasi'),
('Budi','083456789012','Depok'),
('Rina','084567890123','Bogor'),
('Dewi','085678901234','Tangerang');
```

### 🔎 Output

```text
+--------------+----------------+--------------+-----------+
| id_pelanggan | nama_pelanggan | no_hp        | alamat    |
+--------------+----------------+--------------+-----------+
|            1 | Andi           | 081234567890 | Jakarta   |
|            2 | Siti           | 082345678901 | Bekasi    |
|            3 | Budi           | 083456789012 | Depok     |
|            4 | Rina           | 084567890123 | Bogor     |
|            5 | Dewi           | 085678901234 | Tangerang |
+--------------+----------------+--------------+-----------+
```

---

## Data Transaksi

```sql
INSERT INTO transaksi (id_kue, id_pelanggan, jumlah, tanggal) VALUES
(1,1,2,'2026-02-20'),
(2,2,5,'2026-02-21'),
(3,3,1,'2026-02-22'),
(4,4,3,'2026-02-23'),
(5,5,2,'2026-02-24');
```

### 🔎 Output

```text
+--------------+--------+--------------+--------+------------+
| id_transaksi | id_kue | id_pelanggan | jumlah | tanggal    |
+--------------+--------+--------------+--------+------------+
|            1 |      1 |            1 |      2 | 2026-02-20 |
|            2 |      2 |            2 |      5 | 2026-02-21 |
|            3 |      3 |            3 |      1 | 2026-02-22 |
|            4 |      4 |            4 |      3 | 2026-02-23 |
|            5 |      5 |            5 |      2 | 2026-02-24 |
+--------------+--------+--------------+--------+------------+
```

---

# 🔎 Query JOIN

## INNER JOIN

```sql
SELECT pelanggan.nama_pelanggan,
       kue.nama_kue,
       transaksi.jumlah,
       transaksi.tanggal
FROM transaksi
INNER JOIN pelanggan 
ON transaksi.id_pelanggan = pelanggan.id_pelanggan
INNER JOIN kue 
ON transaksi.id_kue = kue.id_kue;
```

### 🔎 Output

```text
+----------------+-------------+--------+------------+
| nama_pelanggan | nama_kue    | jumlah | tanggal    |
+----------------+-------------+--------+------------+
| Andi           | Brownies    |      2 | 2026-02-20 |
| Siti           | Donat       |      5 | 2026-02-21 |
| Budi           | Tart        |      1 | 2026-02-22 |
| Rina           | Cupcake     |      3 | 2026-02-23 |
| Dewi           | Lapis Legit |      2 | 2026-02-24 |
+----------------+-------------+--------+------------+
```

---

## LEFT JOIN

```sql
SELECT pelanggan.nama_pelanggan,
       transaksi.jumlah,
       transaksi.tanggal
FROM pelanggan
LEFT JOIN transaksi 
ON pelanggan.id_pelanggan = transaksi.id_pelanggan;
```

### 🔎 Output

```text
+----------------+--------+------------+
| nama_pelanggan | jumlah | tanggal    |
+----------------+--------+------------+
| Andi           |      2 | 2026-02-20 |
| Siti           |      5 | 2026-02-21 |
| Budi           |      1 | 2026-02-22 |
| Rina           |      3 | 2026-02-23 |
| Dewi           |      2 | 2026-02-24 |
+----------------+--------+------------+
```

---

# 📊 Fungsi Agregasi

## Total Kue Terjual

```sql
SELECT SUM(jumlah) AS total_terjual FROM transaksi;
```

### 🔎 Output

```text
+---------------+
| total_terjual |
+---------------+
|            13 |
+---------------+
```

---

## Rata-rata Harga Kue

```sql
SELECT AVG(harga) AS rata_rata_harga FROM kue;
```

### 🔎 Output

```text
+-----------------+
| rata_rata_harga |
+-----------------+
|      55000.0000 |
+-----------------+
```

---

## Jumlah Pelanggan yang Bertransaksi

```sql
SELECT COUNT(DISTINCT id_pelanggan) AS jumlah_pelanggan 
FROM transaksi;
```

### 🔎 Output

```text
+------------------+
| jumlah_pelanggan |
+------------------+
|                5 |
+------------------+
```

---

# 📑 View Laporan Penjualan

```sql
CREATE VIEW view_laporan_penjualan AS
SELECT pelanggan.nama_pelanggan,
       kue.nama_kue,
       transaksi.jumlah,
       kue.harga,
       (kue.harga * transaksi.jumlah) AS total_harga
FROM transaksi
JOIN pelanggan 
ON transaksi.id_pelanggan = pelanggan.id_pelanggan
JOIN kue 
ON transaksi.id_kue = kue.id_kue;
```

Menampilkan View:

```sql
SELECT * FROM view_laporan_penjualan;
```

### 🔎 Output

```text
+----------------+-------------+--------+--------+-------------+
| nama_pelanggan | nama_kue    | jumlah | harga  | total_harga |
+----------------+-------------+--------+--------+-------------+
| Andi           | Brownies    |      2 |  30000 |       60000 |
| Siti           | Donat       |      5 |   5000 |       25000 |
| Budi           | Tart        |      1 | 150000 |      150000 |
| Rina           | Cupcake     |      3 |  10000 |       30000 |
| Dewi           | Lapis Legit |      2 |  80000 |      160000 |
+----------------+-------------+--------+--------+-------------+
```

---

# 🎯 Kesimpulan

Project ini menunjukkan implementasi dasar sistem penjualan menggunakan relational database dengan:

- Relasi antar tabel
- JOIN (INNER & LEFT)
- Fungsi agregasi (SUM, AVG, COUNT)
- VIEW untuk laporan penjualan

Cocok untuk latihan database dasar dan simulasi sistem kasir sederhana.
