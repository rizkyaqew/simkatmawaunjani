# 🚀 Dokumentasi REST-API SIMKATMAWA RISTEKDIKTI

![API Version](https://img.shields.io/badge/Version-1.0-blue)
![Status](https://img.shields.io/badge/Status-Active-brightgreen)

Dokumentasi ini berisi panduan integrasi REST-API **SIMKATMAWA** dari RISTEKDIKTI untuk sinkronisasi data prestasi, sertifikasi, dan rekognisi mahasiswa.

---

## 📌 Daftar Isi
1. [Konfigurasi Base URL](#-konfigurasi-base-url)
2. [Autentikasi (Bearer Token)](#-autentikasi-bearer-token)
3. [API Prestasi Mandiri](#-api-prestasi-mandiri)
4. [API Sertifikasi](#-api-sertifikasi)
5. [API Rekognisi](#-api-rekognisi)

---

## 🌐 Konfigurasi Base URL

Gunakan Base URL berikut untuk semua permintaan API:
```http
https://simkatmawa.kemdiktisaintek.go.id
```

---

## 🔐 Autentikasi (Bearer Token)

Sebelum mengakses endpoint data, Anda harus mendapatkan token akses menggunakan kredensial email dan password institusi.

### **Login Endpoint**
* **Method:** `POST`
* **URL:** `/api/login`
* **Header:** `Content-Type: application/json`

**Request Body:**
| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `email` | `string` | Yes | Email resmi institusi (PT) |
| `password` | `string` | Yes | Password akun SIMKATMAWA |

**Contoh Request:**
```json
{
  "email": "admin_pt@unjani.ac.id",
  "password": "password_rahasia"
}
```

**Respon Sukses:**
```json
{
  "success": true,
  "kode_pt": "999999",
  "token": "eyJ0eX..."
}
```

> [!IMPORTANT]  
> Gunakan token yang diterima untuk request selanjutnya pada header:  
> `Authorization: Bearer {{token}}`

---

## 🏆 API Prestasi Mandiri

Digunakan untuk menyimpan data prestasi hasil kompetisi atau lomba.

* **URL:** `/api/prestasi-mandiri`
* **Method:** `POST`

### **Parameter Utama**
| Field | Type | Opsi / Deskripsi |
| :--- | :--- | :--- |
| `level` | `string` | `KAB`, `PROV`, `NAS`, `INT` |
| `kategori` | `string` | `RISNOV`, `RISNOVSSH`, `SENBUD`, `OLAHRAGA`, `MINAT` |
| `peringkat` | `string` | `JUARA1`, `JUARA2`, `JUARA3`, `HARAPAN1`, `HARAPAN2`, `HARAPAN3`, `APRESIASI`, `PESERTA` |
| `kelompok_prestasi` | `string` | `INDIVIDU`, `KELOMPOK` |
| `bentuk` | `string` | `DARING`, `LURING` |

### **Contoh Request Body**
```json
{
  "level": "NAS",
  "kategori": "RISNOV",
  "lomba": "National Programming Contest",
  "cabang": "Matematika Lanjut",
  "penyelenggara": "PT. LOMBA",
  "peringkat": "JUARA1",
  "jumlah_unit_peserta": "3",
  "kelompok_prestasi":"KELOMPOK",
  "bentuk":"DARING",
  "url_peserta":"http://wwww.test.com",
  "url_sertifikat":"http://wwww.test.com",
  "tgl_sertifikat": "2025-05-01",
  "url_foto_upp":"http://wwww.test.com",
  "url_dokumen_undangan":"http://wwww.test.com",
  "keterangan":"Catatan Internal",
  "mahasiswa": [
    { "nim": "51422001", "nama": "Budi Santoso" },
    { "nim": "51422002", "nama": "Siti Aminah" }
  ],
  "dosen": [
    {
      "nuptk": "511111422001",
      "nama": "Dr. Ahmad Yani",
      "url_surat_tugas":"http://www.dokument.com"
    }
  ]
}
```

---

## 📜 API Sertifikasi

Digunakan untuk menyimpan data sertifikasi kompetensi/profesi mahasiswa.

* **URL:** `/api/sertifikasi`
* **Method:** `POST`

### **Contoh Request Body**
```json
{
  "level": "NAS",
  "nama": "Sertifikasi Mengetik",
  "penyelenggara": "LPP NASIONAL",
  "url_peserta":"http://wwww.test.com",
  "url_sertifikat":"http://wwww.test.com",
  "tgl_sertifikat": "2025-05-01",
  "url_foto_upp":"http://wwww.test.com",
  "url_dokumen_undangan":"http://wwww.test.com",
  "keterangan":"Catatan",
  "mahasiswa": [
    { "nim": "51422001", "nama": "Budi Santoso" }
  ],
  "dosen": [
    { "nuptk": "511111422001", "nama": "Dosen Pendamping", "url_surat_tugas":"http://www.dokument.com" }
  ]
}
```

---

## 🏅 API Rekognisi

Digunakan untuk menyimpan data pengakuan/rekognisi mahasiswa (seperti Juri, Penulis, HKI).

* **URL:** `/api/rekognisi`
* **Method:** `POST`

### **Opsi Tipe Rekognisi (`jenis`)**
| Kode | Deskripsi | Kode | Deskripsi |
| :--- | :--- | :--- | :--- |
| `SERKOM` | Sertifikat Kompetensi | `PATEN` | Paten / Paten Sederhana |
| `JURIOR` | Juri/Pelatih Olahraga | `PUB` | Publikasi Artikel Ilmiah |
| `JURINOR`| Juri/Pelatih Non-Olahraga | `DUTA` | Brand Ambassador |
| `KEYCONF`| Keynote Speaker (Conf) | `PTG` | Produk Teknologi Tepat Guna |
| `BUKU`   | Penulis Buku | `PKD` | Produk Kreatif Dunia Usaha |

### **Contoh Request Body**
```json
{
  "level": "NAS",
  "nama": "Sertifikasi Mengetik",
  "jenis": "SERKOM",
  "penyelenggara": "Lembaga Ketik",
  "url_sertifikat":"http://wwww.test.com",
  "tgl_sertifikat": "2025-05-01",
  "mahasiswa": [
    { "nim": "51422001", "nama": "Budi Santoso" }
  ],
  "dosen": [
    { "nuptk": "511111422001", "nama": "Budi Santoso", "url_surat_tugas":"http://www.dokument.com" }
  ]
}
```

---

## 📢 API Responses (Standard)

| Status Code | Message | Deskripsi |
| :--- | :--- | :--- |
| `200 OK` | `Success` | Data berhasil disimpan di server pusat. |
| `401 Unauthorized` | `Unauthorized` | Token tidak valid atau sesi berakhir. |
| `422 Unprocessable`| `Validation Error`| Cek kembali format field atau kelengkapan URL. |
| `500 Server Error` | `Error` | Terjadi gangguan pada server RISTEKDIKTI. |

---
© 2026 **SIMKATMAWA RISTEKDIKTI Support**. Bidang 4 Kemahasiswaan Unjani.
