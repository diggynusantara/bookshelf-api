# Bookshelf API
Testing Bookshelf API using Postman

## Data

API ini akan menyimpan data buku dengan atribut sebagai berikut:

```json
  {
    "id": "Qbax5Oy7L8WKf74l",
    "name": "Buku A",
    "year": 2010,
    "author": "John Doe",
    "summary": "Lorem ipsum dolor sit amet",
    "publisher": "Dicoding Indonesia",
    "pageCount": 100,
    "readPage": 25,
    "finished": false,
    "reading": false,
    "insertedAt": "2021-03-04T09:11:44.598Z",
    "updatedAt": "2021-03-04T09:11:44.598Z"
  }
```

## API Endpoints

### 1. Menambahkan Buku Baru

```raml
/books
  post:
    description: Menambahkan buku baru
    request:
      body:
        application/json:
          example: |
            {
              "name": "Buku A",
              "year": 2010,
              "author": "John Doe",
              "summary": "Lorem ipsum dolor sit amet",
              "publisher": "Dicoding Indonesia",
              "pageCount": 100,
              "readPage": 25,
              "reading": false
            }
    responses:
      201:
        body:
          application/json:
            example: |
              {
                "status": "success",
                "message": "Buku berhasil ditambahkan",
                "data": {
                  "bookId": "Qbax5Oy7L8WKf74l",
                }
              }
      400:
        description: properti `name` kosong
        body:
          application/json:
            example: |
              {
                "status": "fail",
                "message": "Gagal menambahkan buku. Mohon isi nama buku",
              }
      400:
        description: properti `readPage` lebih besar dari `pageCount`
        body:
          application/json:
            example: |
              {
                "status": "fail",
                "message": "Gagal menambahkan buku. readPage tidak boleh lebih besar dari pageCount",
              }
      500:
        description: generic error
        body:
          application/json:
            example: |
              {
                "status": "error",
                "message": "Buku gagal ditambahkan",
              }
```

### 2. Menampilkan semua buku

```raml
/books
  get:
    description: Menampilkan semua buku
    responses:
      200:
        body:
          application/json:
            example: |
              {
                "status": "success",
                "data": [
                  {
                    "id": "Qbax5Oy7L8WKf74l",
                    "name": "Buku A",
                    "publisher": "Dicoding Indonesia",
                  },
                  {
                    "id": "1L7ZtDUFeGs7VlEt",
                    "name": "Buku B",
                    "publisher": "Dicoding Indonesia",
                  }
                ]
              }
```

### 3. Menampilkan detail buku

```raml
/books/{bookId}
  get:
    description: Menampilkan detail buku
    responses:
      200:
        body:
          application/json:
            example: |
              {
                "status": "success",
                "data": {
                  "id": "Qbax5Oy7L8WKf74l",
                  "name": "Buku A",
                  "year": 2010,
                  "author": "John Doe",
                  "summary": "Lorem ipsum dolor sit amet",
                  "publisher": "Dicoding Indonesia",
                  "pageCount": 100,
                  "readPage": 25,
                  "finished": false,
                  "reading": false,
                  "insertedAt": "2021-03-04T09:11:44.598Z",
                  "updatedAt": "2021-03-04T09:11:44.598Z"
                }
              }
      404:
        description: buku tidak ditemukan
        body:
          application/json:
            example: |
              {
                "status": "fail",
                "message": "Buku tidak ditemukan",
              }
```

### 4. Mengubah detail buku

```raml
/books/{bookId}
  put:
    description: Mengubah detail buku
    request:
      body:
        application/json:
          example: |
            {
              "name": "Buku A",
              "year": 2010,
              "author": "John Doe",
              "summary": "Lorem ipsum dolor sit amet",
              "publisher": "Dicoding Indonesia",
              "pageCount": 100,
              "readPage": 25,
              "reading": false
            }
    responses:
      200:
        body:
          application/json:
            example: |
              {
                "status": "success",
                "message": "Buku berhasil diperbarui",
              }
      400:
        description: properti `name` kosong
        body:
          application/json:
            example: |
              {
                "status": "fail",
                "message": "Gagal memperbarui buku. Mohon isi nama buku",
              }
      400:
        description: properti `readPage` lebih besar dari `pageCount`
        body:
          application/json:
            example: |
              {
                "status": "fail",
                "message": "Gagal memperbarui buku. readPage tidak boleh lebih besar dari pageCount",
              }
      404:
        description: `id` buku tidak ditemukan
        body:
          application/json:
            example: |
              {
                "status": "fail",
                "message": "Gagal memperbarui buku. Id tidak ditemukan",
              }
```

### 5. Menghapus buku

```raml
/books/{bookId}
  delete:
    description: Menghapus buku
    responses:
      200:
        body:
          application/json:
            example: |
              {
                "status": "success",
                "message": "Buku berhasil dihapus",
              }
      404:
        description: `id` buku tidak ditemukan
        body:
          application/json:
            example: |
              {
                "status": "fail",
                "message": "Buku gagal dihapus. Id tidak ditemukan",
              }
```


## Menjalankan Server

### 1. Jalankan server

Untuk menjalankan secara standar atau di lingkungan **pengembangan (*development*)**, gunakan perintah:

```bash
$ npm run start atau $ npm run start:dev 
```

### 2. Testing dengan Postman
- Buka aplikasi Postman, lalu klik Import pada workspace.
- Pilih file dan import semua file yang ada dalam folder BookshelfAPITestCollectionAndEnvironment ke dalam workspace.
- Jalankan test dengan cara set active pada menu Environments.
- Lalu buka menu Collections, buka Bookshelf API Test, dan klik Send pada setiap testing yang ingin anda jalankan.
- Lihat di bagian Response (di bawah), apakah sudah berhasil sesuai yang anda harapkan.
