1. Jelaskan apa perbedaan complex view dan simple view
Complex view : digunakan untuk query kompleks yang membutuhkan agregasi, join atau operasi kompleks lainnya. Dibuat dari satu atau lebih tabel dasar
Simple view : digunakan untuk query sederhana yang hanya membutuhkan beberapa kolom dari satu tabel. Dibuat dari satu tabel dasar

2. Buatlah dua tabel berikut dalam oracle! 

Table Buku
 ---------------------------------------------------------------------------
|Book_ID (PK) | Judul                | Penulis       | Genre     |  Harga   |
|------------ |----------------------|---------------|-----------|----------|
| 101         | The Great Gatsby     | F. Scott      | Fiction   | 100.000  |
| 201         | Harry Potter         | J.K. Rowling  | Fantasy   | 200.000  |
| 103         | To Kill a Mockingbird| Harper Lee    | Fiction   | 180.000  |
| 404         | 1984                 | George Orwell | Dystopian | 120.000  |
----------------------------------------------------------------------------

Table Inventory
 -----------------------------------
|Invent_ID (PK)|Book_ID (FK)| Stok  | 
|--------------|------------|-------|
| 113          | 103        | 10    |
| 111          | 101        | 15    |
| 211          | 201        | 8     |
| 414          | 404        | 9     |
------------------------------------

- Jadikan kolom Book_ID dan Invent_ID sebagai PRIMARY KEY (PK) dan 
kolom Book_ID pada table Inventory menjadi FOREIGN KEY (FK)
- Buatlah sebuah view dengan nama v_inventory_npm yang menampilkan 
judul buku, penulis, genre, harga, dan stok. 

CREATE TABLE Buku ( 
Book_ID NUMBER(4) PRIMARY KEY,
  Judul VARCHAR(50),
  Penulis VARCHAR(30),
  Genre VARCHAR(20),
  Harga NUMBER(10,2) NOT NULL
);
Langkah pertama adalah membuat table buku (create table)
Primary key digunakan untuk mendefinisikan kolom menjadi kunci utama table buku

INSERT INTO Buku VALUES (101, 'The Great Gatsby', 'F. Scott', 'Fiction', 100000);
INSERT INTO Buku VALUES (201, 'Harry Potter', 'J.K. Rowling', 'Fantasy', 200000);
INSERT INTO Buku VALUES (103, 'To Kill a Mockingbird', 'Harper Lee', 'Fiction', 180000);
INSERT INTO Buku VALUES (404, '1984', 'George Orwell', 'Dystopian', 120000);
Langkah berikutnya adalah memasukan data ke dalam tabel buku dengan menggunakan INSERT INTO Buku VALUES

SELECT * FROM BUKU;
Select digunakan untuk melihat tabel yang sudah dibuat

CREATE TABLE Inventory (
  Invent_ID NUMBER(4) PRIMARY KEY,
  Book_ID NUMBER(4),
  Stok NUMBER(4),
  FOREIGN KEY (Book_ID) REFERENCES Buku(Book_ID)
);
Membuat tabel baru inventory dengan menggunakan CREATE TABLE
Primary key sebagai kunci utama tabel
Foreign key digunakan untuk menghubungkan tabel yang akan dibuat (inventory) ke tabel sebelumnya (tabel buku)

INSERT INTO Inventory VALUES (113, 103, 10);
INSERT INTO Inventory VALUES (111, 101, 15);
INSERT INTO Inventory VALUES (211, 201, 8);
INSERT INTO Inventory VALUES (414, 404, 9);
Memasukan data ke dalam tabel inventory menggunakan INSERT INTO Inventory VAKLUES

SELECT * FROM Inventory;
Untuk melihat tabel inventory digunakan SELECT * FROM inventory

CREATE OR REPLACE VIEW v_inventory_10122101 AS
SELECT
  b.Judul,
  b.Penulis,
  b.Genre,
  b.Harga,
  i.Stok
FROM Buku b
JOIN Inventory i ON b.Book_ID = i.Book_ID;
Langkah selanjutnya adalah membuat table view untuk memudahkan mengakses data
CREATE OR REPLACE VIEW digunakan untuk membuat view baru atau mengganti view yang sudah ada
JOIN digunakan untuk menggabungkan data dari dua table berdasarkan kolom yang sama

SELECT * FROM V_INVENTORY_10122101;
digunakan untuk melihat tabel view

3. Labsi membuka pendaftaran asisten baru dengan kapasistas 12 orang, 
setiap mahasiswa yang ingin mendaftar wajib memasukkan data berupa id NAMA, NPM, Semester, dan IPK. 
mahasiswa yang mendaftar adalah 12 orang, setelah data sudah dimasukkan semua ada 3 orang mengundurkan diri yaitu zahra, saskya, putri. 
Dari 9 mahasiswa ini akan diseleksi lagi dengan kriteria IPK harus lebih dari 3.5 dan semester harus diatas 2, buatkan database untuk mengatur pendaftaran pada labsi

berikut data mahasiswa yang mendaftar
 ---------------------------------------------------------------------------------------------------------------
|ID             | Nama			| NPM			| Semester		| IPK			|
|---------------------------------------------------------------------------------------------------------------|
|1              |bayu			| 10121301		| 4			| 3.2			|
|2              |putra			| 10121302		| 2			| 3.7			|
|3              |rihana			| 10121303		| 3			| 3.8			|
|4              |gilang			| 10121304		| 1			| 3.1			|
|5              |maulana		| 10121305		| 2			| 3.2			|
|6              |richard		| 10121306		| 5			| 3.5			|
|7              |alfira			| 10121307		| 6			| 3.0			|
|8              |hakim			| 10121308		| 3			| 3.4			|
|9              |rozan			| 10121309		| 4			| 3.3			|
|10             |putri			| 10121310		| 4			| 3.9			|
|11             |saskya			| 10121311		| 2			| 3.8			|
|12             |zahra			| 10121312		| 5			| 3.1			|
 ---------------------------------------------------------------------------------------------------------------

CREATE TABLE ujian_aisyahnasywa (
  kode_id INT PRIMARY KEY,
  nama VARCHAR(50),
  npm VARCHAR(10),
  semester INT,
  ipk DECIMAL(2,1)
);
Langkah pertama adalah membuat tabel yaitu dengan menggunakan CREATE TABLE
kode_id sebagai primary key (sebagai kunci utama tabel)

INSERT INTO ujian_aisyahnasywa VALUES(1, 'Bayu', '10121301', 4, 3.2);
INSERT INTO ujian_aisyahnasywa VALUES(2, 'Putra', '10121302', 2, 3.7);
INSERT INTO ujian_aisyahnasywa VALUES(3, 'Rihana', '10121303', 3, 3.8);
INSERT INTO ujian_aisyahnasywa VALUES(4, 'Gilang', '10121304', 1, 3.1);
INSERT INTO ujian_aisyahnasywa VALUES(5, 'Maulana', '10121305', 2, 3.2);
INSERT INTO ujian_aisyahnasywa VALUES(6, 'Richard', '10121306', 5, 3.5);
INSERT INTO ujian_aisyahnasywa VALUES(7, 'Alfira', '10121307', 6, 3.0);
INSERT INTO ujian_aisyahnasywa VALUES(8, 'Hakim', '10121308', 3, 3.4);
INSERT INTO ujian_aisyahnasywa VALUES(9, 'Rozan', '10121309', 4, 3.3);
selanjutnya adalah memasukan data mahasiswa dengan menggunakan INSERT INTO ujian_aisyahnasywa VALUES

SAVEPOINT save1;
Melakukan savepoint sebelum memasukan data selnjutnya seperti yang tertera pada soal

INSERT INTO ujian_aisyahnasywa VALUES(10, 'Putri', '10121310', 4, 3.9);
INSERT INTO ujian_aisyahnasywa VALUES(11, 'Saskya', '10121311', 2, 3.8);
INSERT INTO ujian_aisyahnasywa VALUES(12, 'Zahra', '10121312', 5, 3.1);
memasukkan data setelah melakukan savepoint dengan menggunakan INSERT INTO ujian_aisyahnasywa VALUES

SELECT * FROM UJIAN_AISYAHNASYWA
WHERE ipk > 3.5 AND semester > 2;
untuk melihat tabel ujian_aisyahnasywa secara keseluruhan menggunakan SELECT * FROM UJIAN_AISYAHNASYWA, sedangkan untuk melihat mahasiswa yang mempunyai ipk diatas 3,5 dan diatas semester 2 seperti yang tertera pada soal dengan menggunakan where > 3,5 AND semester 2
