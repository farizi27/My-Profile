# TM-1 — Peta Routing Pribadi

## Entity yang Dipilih

Entity yang digunakan dalam pemetaan routing ini adalah **Course**, karena Course merupakan salah satu entity utama pada aplikasi microcredential/training. Pemetaan dilakukan dari endpoint API, route SvelteKit, route ATLAS SPA, hingga halaman pada Flutter.

## Peta Routing Course

| US    | METHOD + API                 | SvelteKit File                          | ATLAS SPA           | Flutter Name + Args    | Authorization             |
| ----- | ---------------------------- | --------------------------------------- | ------------------- | ---------------------- | ------------------------- |
| US-01 | `GET /api/v1/courses`        | `routes/courses/+page.svelte`           | `/courses`          | `CourseListPage()`     | `canAccess()`             |
| US-02 | `GET /api/v1/courses/:id`    | `routes/courses/[id]/+page.svelte`      | `/courses/:id`      | `CourseDetailPage(id)` | `canAccess()`             |
| US-03 | `POST /api/v1/courses`       | `routes/courses/baru/+page.svelte`      | `/courses/baru`     | `CourseCreatePage()`   | `authorize('instructor')` |
| US-04 | `PUT /api/v1/courses/:id`    | `routes/courses/[id]/edit/+page.svelte` | `/courses/:id/edit` | `CourseEditPage(id)`   | `authorize('instructor')` |
| US-05 | `DELETE /api/v1/courses/:id` | `routes/courses/[id]/+page.svelte`      | `/courses/:id`      | `CourseDetailPage(id)` | `authorize('instructor')` |

## Penjelasan Routing

### 1. Menampilkan seluruh Course

Endpoint:

```http
GET /api/v1/courses
```

Digunakan untuk mengambil daftar seluruh course yang tersedia. Pada SvelteKit, halaman tersebut berada pada:

```text
routes/courses/+page.svelte
```

Route pada ATLAS SPA adalah:

```text
/courses
```

Sedangkan pada Flutter digunakan halaman:

```text
CourseListPage()
```

Akses halaman menggunakan pemeriksaan `canAccess()` karena pengguna yang memiliki akses dapat melihat daftar course.

### 2. Menampilkan detail Course

Endpoint:

```http
GET /api/v1/courses/:id
```

Digunakan untuk mengambil satu course berdasarkan ID.

Contoh:

```http
GET /api/v1/courses/10
```

Pada SvelteKit digunakan dynamic route:

```text
routes/courses/[id]/+page.svelte
```

Route ATLAS SPA:

```text
/courses/:id
```

Flutter:

```text
CourseDetailPage(id)
```

Penggunaan `[id]` menunjukkan bahwa halaman tersebut digunakan untuk course yang sudah tersedia berdasarkan identitas atau ID course.

### 3. Membuat Course Baru

Endpoint:

```http
POST /api/v1/courses
```

Digunakan untuk membuat course baru.

Halaman SvelteKit:

```text
routes/courses/baru/+page.svelte
```

Route ATLAS SPA:

```text
/courses/baru
```

Flutter:

```text
CourseCreatePage()
```

Pembuatan course hanya dapat dilakukan oleh pengguna dengan role instructor sehingga membutuhkan:

```text
authorize('instructor')
```

### 4. Mengubah Course

Endpoint:

```http
PUT /api/v1/courses/:id
```

Digunakan untuk memperbarui data course yang sudah ada.

Contoh:

```http
PUT /api/v1/courses/10
```

Halaman SvelteKit:

```text
routes/courses/[id]/edit/+page.svelte
```

Route ATLAS SPA:

```text
/courses/:id/edit
```

Flutter:

```text
CourseEditPage(id)
```

Operasi perubahan course membutuhkan hak akses instructor:

```text
authorize('instructor')
```

### 5. Menghapus Course

Endpoint:

```http
DELETE /api/v1/courses/:id
```

Digunakan untuk menghapus course berdasarkan ID.

Contoh:

```http
DELETE /api/v1/courses/10
```

Operasi dilakukan melalui halaman detail course:

```text
routes/courses/[id]/+page.svelte
```

Route ATLAS SPA:

```text
/courses/:id
```

Flutter:

```text
CourseDetailPage(id)
```

Operasi penghapusan membutuhkan otorisasi instructor:

```text
authorize('instructor')
```

## Catatan Penting

Pada routing Course terdapat perbedaan antara `[id]` dan `baru`.

`[id]` digunakan untuk mengakses **Course yang sudah ada**, misalnya:

```text
/courses/10
```

Sedangkan `baru` digunakan untuk halaman **pembuatan Course baru**:

```text
/courses/baru
```

Dengan demikian, `baru` tidak diperlakukan sebagai nilai `id`.

Seluruh endpoint API menggunakan prefix:

```text
/api/v1
```

sehingga endpoint Course ditulis sebagai:

```text
/api/v1/courses
```

dan:

```text
/api/v1/courses/:id
```

Pemetaan ini menunjukkan hubungan antara kontrak API dengan routing pada SvelteKit, ATLAS SPA, dan Flutter sehingga setiap fitur Course memiliki jalur yang konsisten pada setiap platform.
