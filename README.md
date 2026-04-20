# Dokumentasi API Simkatmawa

## Ringkasan
Dokumentasi ini menjelaskan endpoint API Simkatmawa untuk proses autentikasi dan pengiriman data:

- Login
- Prestasi Mandiri
- Sertifikasi
- Rekognisi

---

## Base URL

```text
https://simkatmawa.kemdiktisaintek.go.id/api
```

---

## Daftar Isi

1. [Login](#1-login)
2. [Prestasi Mandiri](#2-prestasi-mandiri)
3. [Sertifikasi](#3-sertifikasi)
4. [Rekognisi](#4-rekognisi)

---

## 1. Login

Autentikasi user menggunakan email dan password untuk mendapatkan token, di mana token akan digunakan untuk melakukan request API pada aplikasi.

### Endpoint

```text
https://simkatmawa.kemdiktisaintek.go.id/api/login
```

### Method

```text
POST
```

### Headers

```text
Content-Type: application/json
```

### Request

```json
{
  "email": "xxxxx@xxxx.com",
  "password": "xxxxxxx"
}
```

### Response

**Successful status:** `200 OK`

```json
{
  "success": true,
  "kode_pt": "999999",
  "token": "eyJ0eXsdfssdsfsadfsdfsdfdfOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ..."
}
```

---

## 2. Prestasi Mandiri

Menyimpan data prestasi mandiri beserta daftar mahasiswa dan dosen pembimbing atau pendamping.

### Endpoint

```text
https://simkatmawa.kemdiktisaintek.go.id/api/prestasi-mandiri
```

### Method

```text
POST
```

### Authentication

```text
Authorization: Bearer {{access_token}}
```

### Request Body

```json
{
  "level": "NAS",
  "kategori": "RISNOV",
  "lomba": "National Programming Contest",
  "cabang": "Matematika Lanjut",
  "penyelenggara": "PT. LOMBA",
  "peringkat": "JUARA1",
  "jumlah_unit_peserta": "3",
  "kelompok_prestasi": "KELOMPOK",
  "bentuk": "DARING",
  "url_peserta": "http://wwww.test.com",
  "url_sertifikat": "http://wwww.test.com",
  "tgl_sertifikat": "2025-05-01",
  "url_foto_upp": "http://wwww.test.com",
  "url_dokumen_undangan": "http://wwww.test.com",
  "keterangan": "Catatan",
  "mahasiswa": [
    {
      "nim": "51422001",
      "nama": "Budi Santoso"
    },
    {
      "nim": "51422002",
      "nama": "Siti Aminah"
    }
  ],
  "dosen": [
    {
      "nuptk": "511111422001",
      "nama": "Budi Santoso",
      "url_surat_tugas": "http://www.dokument.com"
    }
  ]
}
```

### Deskripsi Field

- `level` (`string`): level prestasi, contoh: `NAS`. Pilihan yang disediakan:
  - `KAB`: Kabupaten
  - `PROV`: Provinsi
  - `NAS`: Nasional
  - `INT`: Internasional

- `kategori` (`string`): kategori prestasi, contoh: `RISNOV`. Pilihan yang disediakan:
  - `RISNOV`: Riset dan Inovasi STEM
  - `RISNOVSSH`: Riset dan Inovasi SSH
  - `SENBUD`: Seni dan Budaya
  - `OLAHRAGA`: Olahraga
  - `MINAT`: Minat Khusus

- `lomba` (`string`): nama lomba, kompetisi, atau kegiatan.
- `cabang` (`string`): cabang atau bidang lomba.
- `penyelenggara` (`string`): institusi atau penyelenggara kegiatan.
- `peringkat` (`string`): peringkat atau juara, contoh: `JUARA1`. Pilihan isian yang disediakan:
  - `JUARA1`: Juara 1
  - `JUARA2`: Juara 2
  - `JUARA3`: Juara 3
  - `HARAPAN1`: Harapan 1
  - `HARAPAN2`: Harapan 2
  - `HARAPAN3`: Harapan 3
  - `APRESIASI`: Apresiasi Kejuaraan / Penghargaan Tambahan / Juara Umum
  - `PESERTA`: Peserta

- `jumlah_unit_peserta` (`string/number`): jumlah unit peserta, misalnya jumlah PT untuk level nasional atau jumlah negara untuk level internasional.
- `kelompok_prestasi` (`string`): jenis prestasi, contoh: `INDIVIDU` / `KELOMPOK` / lainnya yang merepresentasikan hal yang sama.
- `bentuk` (`string`): mode pelaksanaan, contoh: `DARING` / `LURING` / `HYBRID`.
- `url_peserta` (`string`, URL): link kejuaraan.
- `url_sertifikat` (`string`, URL): link sertifikat.
- `tgl_sertifikat` (`string`, date `YYYY-MM-DD`): tanggal sertifikat.
- `url_foto_upp` (`string`, URL): link foto atau berkas UPP.
- `url_dokumen_undangan` (`string`, URL): link undangan atau dokumen pendukung lainnya.
- `keterangan` (`string`): catatan tambahan.

- `mahasiswa` (`array<object>`): daftar mahasiswa yang terlibat.
  - `mahasiswa[].nim` (`string`): NIM mahasiswa.
  - `mahasiswa[].nama` (`string`): nama mahasiswa.

- `dosen` (`array<object>`): daftar dosen pendamping atau pembimbing.
  - `dosen[].nuptk` (`string`): NUPTK/NIDN/identifier dosen sesuai sistem.
  - `dosen[].nama` (`string`): nama dosen.
  - `dosen[].url_surat_tugas` (`string`, URL): link surat tugas.

### Response

**Successful status:** `200 OK`

```json
{
  "status": true,
  "message": "Prestasi berhasil disimpan",
  "data": {
    "level": "NAS",
    "kategori": "RISNOV",
    "lomba": "National Programming Contest",
    "cabang": "Matematika Lanjut",
    "peringkat": "JUARA1",
    "bentuk": "DARING",
    "kelompok_prestasi": "KELOMPOK",
    "penyelenggara": "PT. LOMBA",
    "keterangan": "Catatan",
    "jumlah_unit_peserta": "3",
    "url_peserta": "http://wwww.test.com",
    "url_sertifikat": "http://wwww.test.com",
    "tgl_sertifikat": "2025-05-01",
    "url_foto_upp": "http://wwww.test.com",
    "url_dokumen_undangan": "http://wwww.test.com",
    "kode_pt": "000000",
    "tahun": "2026",
    "updated_at": "2026-03-05T17:58:14.000000Z",
    "created_at": "2026-03-05T17:58:14.000000Z",
    "id": 518023
  }
}
```

### Catatan

- Simpan response sebagai bukti yang sah dari hasil integrasi ini.

---

## 3. Sertifikasi

Menyimpan data sertifikasi beserta daftar mahasiswa dan dosen pembimbing atau pendamping.

### Endpoint

```text
https://simkatmawa.kemdiktisaintek.go.id/api/sertifikasi
```

### Method

```text
POST
```

### Authentication

```text
Authorization: Bearer {{access_token}}
```

### Request

```json
{
  "level": "NAS",
  "nama": "Sertifikasi Mengetik",
  "penyelenggara": "LPP NASIONAL",
  "url_peserta": "http://wwww.test.com",
  "url_sertifikat": "http://wwww.test.com",
  "tgl_sertifikat": "2025-05-01",
  "url_foto_upp": "http://wwww.test.com",
  "url_dokumen_undangan": "http://wwww.test.com",
  "keterangan": "Catatan",
  "mahasiswa": [
    {
      "nim": "51422001",
      "nama": "Budi Santoso"
    },
    {
      "nim": "51422002",
      "nama": "Siti Aminah"
    }
  ],
  "dosen": [
    {
      "nuptk": "511111422001",
      "nama": "Budi Santoso",
      "url_surat_tugas": "http://www.dokument.com"
    }
  ]
}
```

### Deskripsi

- `level` (`string`): level prestasi, contoh: `NAS`. Pilihan yang disediakan:
  - `KAB`: Kabupaten
  - `PROV`: Provinsi
  - `NAS`: Nasional
  - `INT`: Internasional

- `nama` (`string`): nama lomba, kompetisi, atau kegiatan.
- `penyelenggara` (`string`): institusi atau penyelenggara kegiatan.
- `url_peserta` (`string`, URL): link kejuaraan.
- `url_sertifikat` (`string`, URL): link sertifikat.
- `tgl_sertifikat` (`string`, date `YYYY-MM-DD`): tanggal sertifikat.
- `url_foto_upp` (`string`, URL): link foto atau berkas UPP.
- `url_dokumen_undangan` (`string`, URL): link undangan atau dokumen pendukung lainnya.
- `keterangan` (`string`): catatan tambahan.

- `mahasiswa` (`array<object>`): daftar mahasiswa yang terlibat.
  - `mahasiswa[].nim` (`string`): NIM mahasiswa.
  - `mahasiswa[].nama` (`string`): nama mahasiswa.

- `dosen` (`array<object>`): daftar dosen pendamping atau pembimbing.
  - `dosen[].nuptk` (`string`): NUPTK/NIDN/identifier dosen sesuai sistem.
  - `dosen[].nama` (`string`): nama dosen.
  - `dosen[].url_surat_tugas` (`string`, URL): link surat tugas.

### Response

**Successful status:** `200 OK`

```json
{
  "status": true,
  "message": "Sertifikasi berhasil disimpan",
  "data": {
    "level": "NAS",
    "nama": "Sertifikasi Mengetik",
    "penyelenggara": "LPP NASIONAL",
    "url_peserta": "http://wwww.test.com",
    "url_sertifikat": "http://wwww.test.com",
    "tgl_sertifikat": "2025-05-01",
    "url_foto_upp": "http://wwww.test.com",
    "url_dokumen_undangan": "http://wwww.test.com",
    "kode_pt": "000000",
    "tahun": "2026",
    "updated_at": "2026-03-05T19:05:14.000000Z",
    "created_at": "2026-03-05T19:05:14.000000Z",
    "id": 83491
  }
}
```

---

## 4. Rekognisi

Menyimpan data rekognisi beserta daftar mahasiswa dan dosen pembimbing atau pendamping.

### Endpoint

```text
https://simkatmawa.kemdiktisaintek.go.id/api/rekognisi
```

### Method

```text
POST
```

### Authentication

```text
Authorization: Bearer {{access_token}}
```

### Request

```json
{
  "level": "NAS",
  "nama": "Sertifikasi Mengetik",
  "jenis": "SERKOM",
  "penyelenggara": "Lembaga Ketik",
  "url_peserta": "http://wwww.test.com",
  "url_sertifikat": "http://wwww.test.com",
  "tgl_sertifikat": "2025-05-01",
  "url_foto_upp": "http://wwww.test.com",
  "url_dokumen_undangan": "http://wwww.test.com",
  "keterangan": "Catatan",
  "mahasiswa": [
    {
      "nim": "51422001",
      "nama": "Budi Santoso"
    },
    {
      "nim": "51422002",
      "nama": "Siti Aminah"
    }
  ],
  "dosen": [
    {
      "nuptk": "511111422001",
      "nama": "Budi Santoso",
      "url_surat_tugas": "http://www.dokument.com"
    }
  ]
}
```

### Deskripsi

- `level` (`string`): level prestasi, contoh: `NAS`. Pilihan yang disediakan:
  - `KAB`: Kabupaten
  - `PROV`: Provinsi
  - `NAS`: Nasional
  - `INT`: Internasional

- `nama` (`string`): nama lomba, kompetisi, atau kegiatan.
- `jenis` (`string`): jenis rekognisi. Pilihan yang disediakan:
  - `SERKOM`: Sertifikat Kompetensi
  - `JURIOR`: Juri/Pelatih/Wasit Olahraga
  - `JURINOR`: Juri/Pelatih/Wasit Non Olahraga
  - `KEYCONF`: Keynote speaker conference
  - `KEYWORK`: Keynote speaker workshop/pelatihan/bimbingan teknis
  - `PAMERAN`: Pameran karya seni
  - `KARYA`: Karya cipta lagu dan/atau seni tari
  - `BUKU`: Penulis buku
  - `PATEN`: Paten/Paten Sederhana
  - `PUB`: Publikasi artikel ilmiah
  - `DUTA`: Duta (Brand Ambassador)
  - `PTG`: Produk Teknologi Tepat Guna
  - `PSB`: Produk Seni dan Budaya
  - `PKD`: Produk Kreatif Dunia Usaha dan Industri

- `penyelenggara` (`string`): institusi atau penyelenggara kegiatan.
- `url_peserta` (`string`, URL): link kejuaraan.
- `url_sertifikat` (`string`, URL): link sertifikat.
- `tgl_sertifikat` (`string`, date `YYYY-MM-DD`): tanggal sertifikat.
- `url_foto_upp` (`string`, URL): link foto atau berkas UPP.
- `url_dokumen_undangan` (`string`, URL): link undangan atau dokumen pendukung lainnya.
- `keterangan` (`string`): catatan tambahan.

- `mahasiswa` (`array<object>`): daftar mahasiswa yang terlibat.
  - `mahasiswa[].nim` (`string`): NIM mahasiswa.
  - `mahasiswa[].nama` (`string`): nama mahasiswa.

- `dosen` (`array<object>`): daftar dosen pendamping atau pembimbing.
  - `dosen[].nuptk` (`string`): NUPTK/NIDN/identifier dosen sesuai sistem.
  - `dosen[].nama` (`string`): nama dosen.
  - `dosen[].url_surat_tugas` (`string`, URL): link surat tugas.

### Response

**Successful status:** `200 OK`

```json
{
  "status": true,
  "message": "Rekognisi berhasil disimpan",
  "data": {
    "level": "NAS",
    "jenis": "SERKOM",
    "nama": "Sertifikasi Mengetik",
    "penyelenggara": "Lembaga Ketik",
    "url_peserta": "http://wwww.test.com",
    "url_sertifikat": "http://wwww.test.com",
    "tgl_sertifikat": "2025-05-01",
    "url_foto_upp": "http://wwww.test.com",
    "url_dokumen_undangan": "http://wwww.test.com",
    "kode_pt": "000000",
    "tahun": "2026",
    "updated_at": "2026-03-05T19:20:25.000000Z",
    "created_at": "2026-03-05T19:20:25.000000Z",
    "id": 2
  }
}
```
