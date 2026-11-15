# korpus-pusat

Korpus peraturan perundang-undangan tingkat pusat untuk keperluan pemeriksaan BPK (Badan Pemeriksa Keuangan). Korpus ini menjadi sumber bagi skill cari-kriteria, yaitu skill pencari kriteria pemeriksaan sampai level pasal.

Repositori ini hanya berisi teks peraturan publik dan metadatanya. Catatan penugasan, nama entitas yang diperiksa, data entitas, dan kredensial tidak boleh ditulis ke file, laporan, nama file, maupun pesan commit.

## Struktur

```
indeks/<jenis>/<ID>.md   satu file per peraturan, dipecah per pasal
katalog.csv              satu baris per peraturan
tag.csv                  daftar tag isu (dipakai juga oleh korpus-daerah)
laporan/AAAA-BB.md       laporan berkala
```

Nilai `<jenis>`: `uu`, `perppu`, `pp`, `perpres`, `permen`, `peraturan-lembaga`, `kepmen`, `se`.

Jenis yang diterima:

| Jenis | Kepanjangan |
|---|---|
| UU | Undang-Undang |
| Perppu | Peraturan Pemerintah Pengganti Undang-Undang |
| PP | Peraturan Pemerintah |
| Perpres | Peraturan Presiden |
| Permen | Peraturan Menteri |
| Peraturan Lembaga | Peraturan lembaga negara/pemerintah |
| Kepmen | Keputusan Menteri |
| SE | Surat Edaran |

Jenis di luar daftar ini tidak dimasukkan tanpa persetujuan pemilik korpus.

## Konvensi penamaan

- ID peraturan sekaligus menjadi nama file: `<ID>.md` di repositori, `<ID>.pdf` di Google Drive.
- ID ditulis huruf kapital dengan garis bawah sebagai pemisah: `<JENIS>_<NOMOR>_<TAHUN>`.
- Untuk Permen, Kepmen, Peraturan Lembaga, dan SE, `<JENIS>` memuat singkatan penerbit agar unik: `PERMEN<PENERBIT>`, `KEPMEN<PENERBIT>`, `PER<LEMBAGA>`, `SE<PENERBIT>`.
- Singkatan penerbit yang belum pernah dipakai di katalog mengikuti singkatan yang tertulis di naskah atau di JDIH (Jaringan Dokumentasi dan Informasi Hukum) penerbitnya.
- Tanggal ditulis `AAAA-BB-HH`.

## katalog.csv

Kolom, berurutan:

| Kolom | Isi |
|---|---|
| id | ID peraturan sesuai konvensi |
| jenis | Jenis peraturan |
| nomor | Nomor peraturan |
| tahun | Tahun peraturan |
| judul | Judul lengkap |
| penerbit | Lembaga penetap |
| status | `berlaku`, `diubah`, atau `dicabut` |
| berlaku_sejak | Tanggal mulai berlaku menurut ketentuan penutup naskah |
| berlaku_sampai | Tanggal mulai berlakunya peraturan pencabut; kosong bila masih berlaku |
| diubah_dicabut_oleh | ID peraturan pengubah atau pencabut; beberapa ID dipisah titik koma |
| tautan_sumber | Tautan resmi (JDIH penerbit atau Pasal.id); kosong bila tidak ditemukan |
| tautan_pdf_drive | Tautan PDF di Google Drive, bila disimpan |
| tag_isu | Tag dari tag.csv, dipisah titik koma |
| tag_jenis_pemeriksaan | `keuangan`, `kinerja`, `pdtt` (Pemeriksaan Dengan Tujuan Tertentu); boleh lebih dari satu |
| tanggal_verifikasi | Tanggal terakhir status dicek ke sumber luar |
| status_review | `lolos-otomatis`, `perlu-dicek`, atau `terverifikasi` |
| catatan_cek | Alasan singkat bila `perlu-dicek` |

Nilai yang mengandung koma diapit tanda kutip ganda. Urutan dan nama kolom tidak diubah tanpa persetujuan pemilik korpus.

Peraturan yang dicabut tidak dihapus. Masa berlakunya dicatat di katalog karena kriteria dipilih berdasarkan periode yang diperiksa.

## Format file indeks

```
---
id: <ID>
jenis: <jenis>
nomor: <nomor>
tahun: <tahun>
judul: <judul lengkap>
sumber_teks: teks-digital | ocr
---
# <judul lengkap>
## Pembukaan
## BAB I - <JUDUL BAB>
### Pasal 1
## Penjelasan
### Penjelasan Pasal 1
## Lampiran
```

- Bunyi pasal disalin apa adanya. Perbaikan hanya untuk galat OCR (Optical Character Recognition) yang jelas, tanpa mengubah kata.
- Setiap pasal mendapat satu heading `### Pasal N`. Bagian dan Paragraf ditulis sebagai baris tebal di bawah heading BAB.
- Peraturan perubahan disimpan sebagai naskah tersendiri sesuai bunyinya (Pasal I, Pasal II beserta angka perubahannya). Tidak ada versi konsolidasi.
- SK dan SE yang tidak berpasal memakai heading sesuai diktum (KESATU, KEDUA) atau angka butirnya.
- Tabel lampiran yang tidak terekstrak rapi cukup dicatat judulnya dengan keterangan "lihat PDF".

## Pemeriksaan otomatis dan status_review

Setiap naskah yang masuk melewati enam pemeriksaan: (1) identitas, (2) naskah final, (3) mutu OCR, (4) urutan pasal, (5) duplikat, (6) masa berlaku.

- Semua lulus: `lolos-otomatis`.
- Ada yang gagal: `perlu-dicek`; `catatan_cek` memuat nomor pemeriksaan yang gagal dan alasannya.
- `terverifikasi` hanya diberikan setelah teks pasal dicocokkan dengan PDF.

## tag.csv

Kolom: `tag`, `definisi`. Tag ditulis huruf kecil dengan tanda hubung. Tag baru ditambahkan hanya setelah disetujui pemilik korpus.

## Laporan

`laporan/AAAA-BB.md` berisi lima bagian tetap: naskah masuk, perubahan status, perlu dicek, usulan tag baru, dan kendala akses. Laporan bulan yang sama diperbarui dengan menambah, bukan menimpa.

## Pesan commit

```
tambah: <ID> - <judul singkat> [<status_review>]
status: <ID> <status lama> -> <status baru> oleh <ID pengubah>
katalog: <perubahan metadata dan alasannya>
laporan: AAAA-BB
skema: <perubahan yang disetujui>
```
