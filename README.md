# 🍰 Project Database Toko Kue

Project ini merupakan implementasi database sederhana menggunakan MySQL / MariaDB pada XAMPP untuk sistem penjualan toko kue.

Database ini mencakup:
- Manajemen data kue
- Data pelanggan
- Transaksi penjualan
- Query JOIN
- Fungsi agregasi
- View laporan penjualan

---

## 🛠️ Tools yang Digunakan

- XAMPP
- MariaDB 10.4.32
- MySQL Command Line

---

## 🗄️ Membuat Database

```sql
CREATE DATABASE toko_kue;
USE toko_kue;
```

---

## 📦 Struktur Tabel

### 🎂 Tabel `kue`

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

### 👤 Tabel `pelanggan`

```sql
CREATE TABLE pelanggan(
    id_pelanggan INT AUTO_INCREMENT PRIMARY KEY,
    nama_pelanggan VARCHAR(15),
    no_hp VARCHAR(15),
    alamat VARCHAR(100)
);
```

---

### 🧾 Tabel `transaksi`

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

## 📥 Insert Data

### Data Kue

```sql
INSERT INTO kue(nama_kue, harga, stok, kategori) VALUES
('Brownies',30000,20,'Coklat'),
('Donat',5000,50,'Goreng'),
('Tart',150000,10,'Ulang Tahun'),
('Cupcake',10000,30,'Mini Cake'),
('Lapis Legit',80000,15,'Premium');
```

---

### Data Pelanggan

```sql
INSERT INTO pelanggan(nama_pelanggan, no_hp, alamat) VALUES
('Andi','081234567890','Jakarta'),
('Siti','082345678901','Bekasi'),
('Budi','083456789012','Depok'),
('Rina','084567890123','Bogor'),
('Dewi','085678901234','Tangerang');
```

---

### Data Transaksi

```sql
INSERT INTO transaksi (id_kue, id_pelanggan, jumlah, tanggal) VALUES
(1,1,2,'2026-02-20'),
(2,2,5,'2026-02-21'),
(3,3,1,'2026-02-22'),
(4,4,3,'2026-02-23'),
(5,5,2,'2026-02-24');
```

---

## 🔎 Query JOIN

### INNER JOIN

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

---

### LEFT JOIN

```sql
SELECT pelanggan.nama_pelanggan,
       transaksi.jumlah,
       transaksi.tanggal
FROM pelanggan
LEFT JOIN transaksi 
ON pelanggan.id_pelanggan = transaksi.id_pelanggan;
```

---

## 📊 Fungsi Agregasi

### Total Kue Terjual

```sql
SELECT SUM(jumlah) AS total_terjual 
FROM transaksi;
```

### Rata-rata Harga Kue

```sql
SELECT AVG(harga) AS rata_rata_harga 
FROM kue;
```

### Jumlah Pelanggan yang Bertransaksi

```sql
SELECT COUNT(DISTINCT id_pelanggan) AS jumlah_pelanggan 
FROM transaksi;
```

---

## 📑 View Laporan Penjualan

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

Menampilkan view:

```sql
SELECT * FROM view_laporan_penjualan;
```

---

## 📌 Fitur yang Diimplementasikan

- CREATE DATABASE  
- CREATE TABLE  
- ALTER TABLE  
- INSERT DATA  
- UPDATE DATA  
- SELECT  
- INNER JOIN  
- LEFT JOIN  
- Aggregate Function (SUM, AVG, COUNT)  
- VIEW  

---

## 🎯 Kesimpulan

Project ini menunjukkan implementasi dasar sistem penjualan menggunakan relational database dengan relasi antar tabel dan pembuatan laporan menggunakan VIEW.

Cocok untuk:
- Latihan Database Dasar
- Tugas Sekolah / Kuliah
- Simulasi Sistem Kasir Sederhana
