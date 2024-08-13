CREATE DATABASE data_penjualan;
USE data_penjualan;
CREATE TABLE users(
  user_id INTEGER PRIMARY KEY,
  email VARCHAR(50) NOT NULL,
  password VARCHAR(20) NOT NULL,
  address TEXT(100) NOT NULL,
  role VARCHAR(10) NOT NULL,
  status VARCHAR(10) NOT NULL,
  created_at TIMESTAMP,
  updated_at TIMESTAMP,
);

CREATE TABLE products(
  id INTEGER PRIMARY KEY,
  category_id INTEGER NOT NULL,
  user_id INTEGER NOT NULL,
  code VARCHAR(20) NOT NULL,
  name VARCHAR(100) NOT NULL,
  slug VARCHAR(20) NOT NULL,
  description LONGTEXT NOT NULL,
  photo VARCHAR(30) NOT NULL,
  qty DOUBLE NOT NULL,
  unit VARCHAR(20) NOT NULL,
  price DOUBLE NOT NULL,
  status VARCHAR(10) NOT NULL,
);

CREATE TABLE categories(
  id INTEGER PRIMARY KEY,
  user_id INTEGER NOT NULL,
  code VARCHAR(20) NOT NULL,
  name VARCHAR(100) NOT NULL,
  slug VARCHAR(20) NOT NULL,
  description TEXT NOT NULL,
  status VARCHAR(10) NOT NULL,
  photo VARCHAR(30) NOT NULL,
);

INSERT INTO `categories` (`id`, `user_id`, `code`, `name`, `slug`, `description`, `status`, `photo`) VALUES ('1', '1', 'be21', 'Mainan', 'mainan-anak', 'mainan anak dibawah 5 tahun', 'baru', 'mainan.png'), ('2', '2', 'bc31', 'Aksesoris Perempuan', 'aksesoris-perempuan', 'Aksesoris perempuan dewasa', 'baru', 'aksesoris-perempuan.png');

INSERT INTO `products` (`id`, `category_id`, `user_id`, `code`, `name`, `slug`, `description`, `photo`, `qty`, `unit`, `price`, `status`) VALUES ('1', '1', '1', 'cda1', 'Mobil Truk', 'mobil-truk', 'Mobil truk pengangkut pasir', 'mobil-truk-pasir.png', '30', '10', '30000', 'baru'), ('2', '2', '1', 'ksk1', 'Anting Bulat', 'anting-bulat', 'Anting bulat aksesoris perempuan dewasa', 'anting-bulat.png', '15', '20', '25000', 'baru'), ('3', '1', '2', 'ksdkj1', 'Tembakan Laras Panjang', 'tembakan-laras-panjang', 'Tembakan laras panjang anak', 'tembakan.png', '20', '30', '30000', 'baru'), ('4', '2', '2', 'sdj2', 'Gelang karet rambut', 'gelang-karet-rambut', 'Gelang karet ikat rambut', 'gelang-ikat-rambut', '20', '23', '5000', 'baru');

INSERT INTO `users` (`id`, `email`, `password`, `address`, `role`, `status`, `created_at`, `updated_at`) VALUES ('1', 'satu@gmail.com', 'satu1', 'Jalan Prambanan I', 'admin', 'admin', NULL, NULL), ('2', 'dua@gmail.com', 'dua2', 'Jalan Prambanan II', 'admin', 'admin', NULL, NULL);

ALTER TABLE `categories` ADD FOREIGN KEY (`user_id`) REFERENCES `users`(`id`) ON DELETE RESTRICT ON UPDATE RESTRICT;

ALTER TABLE `products` ADD FOREIGN KEY (`user_id`) REFERENCES `users`(`id`) ON DELETE RESTRICT ON UPDATE RESTRICT;
ALTER TABLE `products` ADD FOREIGN KEY (`category_id`) REFERENCES `categories`(`id`) ON DELETE RESTRICT ON UPDATE RESTRICT;

SELECT categories.name, users.id
FROM categories
LEFT JOIN users ON categories.id = users.id
ORDER BY categories.name;