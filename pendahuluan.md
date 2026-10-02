# Pendahuluan

## 1. Perbedaan /posts/1 dan /users/1

- `/posts/1` berisi data satu postingan: userId, id, title, dan body.
- `/users/1` berisi data satu pengguna: id, name, username, email, address, phone, website, dan company.
- Jadi, `/posts/1` berfokus pada konten postingan, sedangkan `/users/1` berfokus pada informasi pengguna.

## 2. Analisa Resource

### /posts

| Field | Tipe Data | Fungsi |
|---|---|---|
| userId | Integer | ID user yang membuat post |
| id | Integer | ID unik post |
| title | String | Judul post |
| body | String | Isi post |

### /users

| Field | Tipe Data | Fungsi |
|---|---|---|
| id | Integer | ID unik user |
| name | String | Nama lengkap |
| username | String | Nama pengguna |
| email | String | Email |
| address | Object | Informasi alamat |
| phone | String | Nomor telepon |
| website | String | Website |
| company | Object | Informasi perusahaan |

## 3. Hubungan URL, Method, dan Data

- **URL** menentukan resource yang diakses, misalnya `/posts`.
- **Method** menentukan tindakan, seperti GET untuk mengambil atau POST untuk mengirim data.
- **Data** yang dikembalikan bergantung pada resource dan method yang digunakan.

Contoh: `GET /posts` mengembalikan daftar postingan.

## 4. /posts/1 vs ?userId=1

- `/posts/1` mengambil satu post berdasarkan ID post.
- `/posts?userId=1` mengambil semua post milik user dengan ID 1.
- Jadi, `/posts/1` menggunakan ID resource, sedangkan `?userId=1` menggunakan query parameter untuk filtering.

## 5. GET, POST, PUT, PATCH, DELETE

| Method | Fungsi | Status Umum | Data |
|---|---|---|---|
| GET | Mengambil data | 200 | Data dikembalikan |
| POST | Membuat data | 201 | Data baru dikembalikan |
| PUT | Mengganti seluruh data | 200 | Data hasil perubahan dikembalikan |
| PATCH | Mengubah sebagian data | 200 | Data hasil perubahan dikembalikan |
| DELETE | Menghapus data | 200 | Data dianggap terhapus |
