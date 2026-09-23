---
id: prd-dashboard-spvr-v2
title: "PRD — Dashboard SPVR (Supervisor Regional) GriyaNet v2.0"
type: product-requirement-document
version: 2.0
date: 2026-09-22
owner: Supervisor Regional — GriyaNet
related:
  - "PRD-DASHBOARD-SPVR.md"
  - "Dashboard SPVR - CHECKLIST.md"
  - "BRD - ERP SPVR.docx"
status: active
tags: [prd, spvr, erp, griyanet, monitoring, v2]
---

# PRD — Dashboard SPVR (Supervisor Regional) GriyaNet v2.0

> Dokumen ini merupakan versi pembaruan (v2.0) dari `PRD-DASHBOARD-SPVR.md`. Dokumen ini mencatat seluruh penyelarasan arsitektur data, konsolidasi modul, dan eliminasi fitur/field yang belum didukung oleh ERP inti saat ini.

---

## Daftar Isi

- BAB 1 — Pendahuluan & Ringkasan Perubahan (Changelog v2.0)
- BAB 2 — Tujuan Produk & Sasaran
- BAB 3 — Kebutuhan Fungsional
- BAB 4 — Kebutuhan Non-Fungsional & Arsitektur Data
- BAB 5 — Desain Sistem & Integrasi
- BAB 6 — Rencana Implementasi
- BAB 7 — Risiko & Mitigasi
- BAB 8 — Lampiran (Peta Halaman Terkini)

---

## BAB 1 — Pendahuluan

### 1.1 Latar Belakang Pembaruan (v2.0)
Pada iterasi prototype sebelumnya (v1.0), implementasi dashboard masih menghadapi beberapa kendala teknis dan kesenjangan (gap) proses bisnis terhadap sistem ERP yang berjalan:
1. **Performa I/O Berat**: Sistem sebelumnya membaca 30 file CSV mentah via synchronous `XMLHttpRequest`, menimbulkan latensi dan potensi CORS error saat diakses offline/file protocol.
2. **Duplikasi Modul Area**: Modul `Coverage Area` (`open-area.html`) dan `Analisa Area Branch` (`analisa-area-branch.html`) memiliki overlapping informasi yang membingungkan alur navigasi SPVR.
3. **Data Target & Estimasi Belum Tersedia**: Fitur seperti Target Pembukaan Area dan Analisa Lifecycle Area belum tercatat dalam database ERP berjalan.
4. **Data Penyebab Isolir Belum Ada**: ERP berjalan hanya mencatat status pelanggan (Aktif, Isolir, Terminate) tanpa kategorisasi akar penyebab isolir.
5. **Redundansi Mode Navigasi**: Selector "Mode Dashboard" di sidebar tumpang tindih dengan fungsi filter global Branch di top bar.

### 1.2 Ringkasan Perubahan Utama (Changelog v2.0)

| Komponen / Modul | Kondisi v1.0 | Pembaruan v2.0 | Alasan Bisnis / Teknis |
|---|---|---|---|
| **Arsitektur Data** | 30 file CSV statis dimuat via sync XMLHttpRequest | Native In-Memory JS Object (`assets/js/data.js`) | Eliminasi beban I/O, render instan, bebas CORS di `file://` |
| **Rentang Waktu Data Dummy** | Terbatas pada kuartal awal 2026 | Ditambah periode **Agustus, September, Oktober 2026** | Simulasi tren operasional Q3-Q4 2026 yang lebih representatif |
| **Navigasi Scope** | Tombol Mode All/Branch di sidebar & filter top bar | Sidebar dibersihkan; fokus pada **Filter Branch Top Bar** + **Scope Badge** | Menghilangkan duplikasi UI; filter top bar sudah mencakup All vs Branch |
| **Modul Area** | Terpisah: `open-area.html` & `analisa-area-branch.html` | **Dilebur menjadi 1 halaman terpadu**: `pages/area/analisa-area-branch.html` | Menghilangkan redundansi halaman; donut komposisi diserap ke halaman analisa |
| **Target Area** | Komponen bar chart Target vs Realisasi di open-area | **Dihilangkan** | Data target pembukaan area tidak tersedia di ERP saat ini |
| **Lifecycle Area** | Field kategori New/Growth/Mature di tabel Area | **Dihilangkan** | Field tersebut belum didukung skema data ERP eksisting |
| **Penyebab Isolir** | Donut chart & kolom tabel "Penyebab Isolir" di Retention | **Dihilangkan** | ERP saat ini hanya mencatat status tanpa data penyebab |
| **Dashboard Utama (`index.html`)** | KPI card statis, tidak ada grafik tren, card navigasi modul statis | **KPI Clickable Drill-down** + **Grafik Tren 6 Bulan** + **Metrik Operasional Lintas Fitur** (Early Warning & card eksplorasi dihilangkan) | Fokus monitoring metrik operasional terpadu lintas modul yang dinamis per branch |
| **Dismantle Performance** | Tabel flat tanpa SLA overdue | **KPI Overdue (>14 Hari)** + **Panel Bottleneck Pengambilan Modem** | Membantu SPVR memprioritaskan aset tertahan |
| **Pipeline Penjualan** | Daftar prospect umum | **Kolom Aging & Flag SLA Overdue** | Mengetahui prospect yang stuck pada stage tertentu |

### 1.3 Pemangku Kepentingan (Stakeholder)

| Peran | Tanggung Jawab | Keterlibatan |
|---|---|---|
| Supervisor Regional (SPVR) | User utama monitoring operasional & sales regional | Validasi harian |
| Project Director / Direktur HRGA | Pemilik inisiatif & approval spesifikasi ERP | Sign-off |
| Bapak Samsut | Reviewer arsitektur fungsional & operasional lapangan | UAT & Final Review |
| Branch Manager | Pemantau kinerja cabang masing-masing | Verifikasi data cabang |
| Tim Engineering (FE/BE) | Pengembang implementasi ERP fase R1 | Eksekutor build |

---

## BAB 2 — Tujuan Produk & Sasaran

### 2.1 Visi Produk (Terkonsolidasi)
> *"Menyediakan satu pintu monitoring regional (Single Pane of Glass) bagi SPVR yang berbasis **indikator nyata dari ERP yang berjalan**, menekankan alur **Summary → Analysis → Early Warning → Drill-down**, tanpa menampilkan indikator spekulatif yang datanya belum tersedia."*

### 2.2 Metrik Keberhasilan
- **Waktu Load Halaman**: < 100ms di browser lokal (berkat in-memory dataset).
- **Zero Console Errors**: 100% halaman modul bebas error JS dan network timeout.
- **Konsistensi Lingkup Cabang**: 100% grafik, KPI, dan tabel otomatis merespons event `globalBranchChange`.
- **Ketepatan Lingkup ERP**: 0 field fiktif yang tidak bisa dipetakan ke sistem ERP eksisting.

---

## BAB 3 — Kebutuhan Fungsional (Tereduksi Sesuai Kapabilitas ERP)

### 3.1 Fitur Utama (MoSCoW Matrix v2.0)

| Kode | Fitur | Prioritas | Catatan v2.0 |
|---|---|---|---|
| **F-D1** | Executive Summary Dashboard (`index.html`) | **Must** | 4 KPI clickable, chart tren 6 bulan (Active/Isolir/Terminate), Early Warning |
| **F-D2** | Filter Global Branch & Scope Badge | **Must** | Terletak di sticky top bar; scope badge reaktif di page-header |
| **F-A1** | Modul Coverage Area Terpadu | **Must** | Peleburan open-area & analisa-branch: Donut komposisi, Closing harian, Data Area |
| **F-A2** | Modul Detail Area per Branch | **Must** | Poligon & rincian teknis per area (`detail.html`) |
| **F-S1** | Monitoring Customer Retention | **Must** | Active/Isolir/Terminate, tren 6 bulan, Terminate Rate (tanpa penyebab isolir) |
| **F-S2** | Customer Aktif & Fasum | **Must** | Pemisahan customer komersial vs fasilitas umum |
| **F-S3** | Pipeline Penjualan & SLA Overdue | **Should** | Cold, Hot, Progress prospect dengan tracking hari/aging |
| **F-S4** | Performance AE | **Should** | Kinerja prospect per Account Executive |
| **F-O1** | Monitoring Work Order (PSB, TSO, Distribution) | **Must** | Multi-tab WO operasional dan waitlist terkait |
| **F-O2** | Dismantle Performance & Bottleneck Aset | **Must** | KPI Overdue >14 hari & panel daftar penundaan penarikan modem |
| **F-M1** | Man Power Planning (MPP) | **Should** | Rasio teknisi & AE per branch |
| **F-X1** | Monitoring Implementasi Aset (Perangkat, Modem, Kabel) | **Could** | Status stok dan riwayat mutasi aset |
| **F-N1** | Monitoring Infrastruktur (ODP, Splitter, Map Access) | **Could** | Status konfigurasi dan jaringan fisik |

### 3.2 Fitur yang Dikeluarkan dari Ruang Lingkup (Out-of-Scope v2.0)
1. **Target Pembukaan Area Bulanan**: Dikeluarkan karena ERP tidak menyimpan kuota target area per cabang.
2. **Analisis Lifecycle Area (New/Growth/Mature)**: Dikeluarkan karena umur area belum memiliki matriks threshold resmi di ERP.
3. **Breakdown Penyebab Isolir**: Dikeluarkan karena sistem tiket/billing belum mengklasifikasikan alasan pemutusan sementara.
4. **Mode Switcher Sidebar**: Dihapus karena tumpang tindih dengan filter top bar.

---

## BAB 4 — Kebutuhan Non-Fungsional & Arsitektur Data

### 4.1 Arsitektur Data In-Memory
- **Penyimpanan**: Seluruh dataset dimuat melalui `assets/js/data.js` sebagai objek global `window.*` (`window.BRANCHES`, `window.CUSTOMER_DATA`, `window.AREA_DATA`, `window.WO_DISMANTLE`, dll.).
- **Format Tanggal Baku**: `subscribe_date` dan `open_date` menggunakan format teks `DD-MMM-YY`, dipetakan secara dinamis ke string ISO `YYYY-MM-DD` untuk keperluan filter bulanan/tahunan.
- **Dukungan Periode Data**: Dataset mencakup transaksi dari Januari 2026 hingga **Oktober 2026** (mencakup data Q3–Q4: Agustus, September, Oktober 2026).

### 4.2 Kebutuhan Komponen Tabel & UI
- **Pagination Fleksibel**: Komponen `renderSimpleTable` di `assets/js/common.js` mendukung pemilihan ukuran halaman (`pageSize`: 10, 20, 50).
- **Default Sorting Cerdas**: Otomatis melakukan sort descending pada kolom bertipe tanggal transaksi (`open_date`, `created_at`, `expired_date`).

---

## BAB 5 — Desain Sistem & Integrasi Halaman

### 5.1 Struktur Alur Halaman (Page Hierarchy)

```
[Dashboard Utama (index.html)]
  │
  ├── [Area] ────────► Coverage Area (pages/area/analisa-area-branch.html)
  │                      └── Detail Area (pages/area/detail.html)
  │
  ├── [Sales] ───────► Customer Retention (pages/sales/retention.html)
  │                   ├── Customer Aktif & Fasum (pages/sales/customer-aktif.html)
  │                   ├── Pipeline Penjualan (pages/sales/pipeline-penjualan.html)
  │                   └── Performance AE (pages/sales/performance-ae.html)
  │
  ├── [Operasional] ─► Monitoring WO PSB/TSO/Distribusi (pages/operational/psb.html)
  │                   └── Dismantle Performance (pages/operational/dismantle-performance.html)
  │
  ├── [Manpower] ────► Modul MPP (pages/manpower/mpp.html)
  │
  ├── [Aset] ────────► Perangkat, Modem, Kabel (pages/asset-monitoring/*)
  │
  └── [Infra] ───────► Monitor ODP, Splitter, Map Access (pages/infra-monitoring/*)
```

---

## BAB 6 — Rencana Implementasi

### 6.1 Status Rilis Prototype

| Rilis | Status | Deskripsi |
|---|---|---|
| **v1.0 (Legacy)** | Superseded | Prototype 22 halaman dengan file CSV terpisah dan komponen spekulatif |
| **v2.0 (Current)** | **Live / Approved** | In-memory dataset, integrasi Coverage Area, penyesuaian gap ERP, Q3-Q4 data |
| **R1 (ERP Build)** | Planned | Migrasi UI prototype ke framework frontend ERP resmi (React/Vue) dan integrasi REST API |

---

## BAB 7 — Risiko & Mitigasi

| # | Risiko | Tingkat | Strategi Mitigasi v2.0 |
|---|---|---|---|
| **R-01** | Ekspektasi user terhadap fitur target & lifecycle | Sedang | Penjelasan eksplisit di PRD v2.0 bahwa data target belum tersedia di database ERP |
| **R-02** | Isolir melonjak tanpa diketahui penyebabnya | Sedang | SPVR diarahkan langsung membedah daftar kontak pelanggan di retention untuk verifikasi manual |
| **R-03** | Inkonsistensi link paska penghapusan `open-area.html` | Rendah | Semua referensi di `layout.js`, `index.html`, dan `detail.html` telah dialihkan ke `analisa-area-branch.html` |

---

## BAB 8 — Lampiran

### 8.1 Peta Modul & Halaman Terkini (Total 21 Halaman)

| Modul | Halaman Aktif | Fungsi Utama |
|---|---|---|
| **Dashboard** | `index.html` | Executive summary, KPI clickable, tren 6 bulan |
| **Area** | `pages/area/analisa-area-branch.html` | **Coverage Area terpadu** (komposisi, growth, closing, tabel) |
| | `pages/area/detail.html` | Rincian area spesifik & visualisasi poligon |
| **Sales** | `pages/sales/retention.html` | Monitoring pelanggan Aktif, Isolir, Terminate |
| | `pages/sales/customer-aktif.html` | Daftar pelanggan aktif & Fasum |
| | `pages/sales/pipeline-penjualan.html` | Pipeline prospek (Cold/Hot/Progress) & SLA Overdue |
| | `pages/sales/performance-ae.html` | Evaluasi kinerja prospek Account Executive |
| **Operasional** | `pages/operational/psb.html` | Monitoring WO PSB, TSO, Dismantle, Distribusi |
| | `pages/operational/dismantle-performance.html` | Performa pembongkaran & bottleneck aset |
| | `pages/operational/issue-tso.html` | Tiket gangguan teknis |
| | `pages/operational/dismantle.html` | Penjadwalan penarikan perangkat |
| | `pages/operational/infrastruktur.html` | Monitoring infrastruktur teknis |
| **Manpower** | `pages/manpower/mpp.html` | Ketersediaan teknisi & AE per cabang |
| **Aset** | `pages/asset-monitoring/perangkat.html` | Stok & mutasi perangkat |
| | `pages/asset-monitoring/modem.html` | Monitoring modem pelanggan |
| | `pages/asset-monitoring/kabel.html` | Pemakaian & sisa rol kabel |
| **Infrastruktur** | `pages/infra-monitoring/monitor-odp.html` | Status kapasitas ODP |
| | `pages/infra-monitoring/list-area-splitter.html` | Pembagian splitter area |
| | `pages/infra-monitoring/splitter-no-config.html` | Splitter belum terkonfigurasi |
| | `pages/infra-monitoring/progress-konfigurasi.html` | Progres aktivasi splitter |
| | `pages/infra-monitoring/map-access.html` | Pemetaan akses jaringan |

---
*Dokumen ini disusun sebagai versi resmi (v2.0) menggantikan PRD v1.0, mencerminkan seluruh penyesuaian fungsional dan teknis pada prototype Dashboard SPVR.*
