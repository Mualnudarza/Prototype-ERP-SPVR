---
id: prd-dashboard-spvr
title: "PRD — Dashboard SPVR (Supervisor Regional)"
type: product-requirement-document
version: 1.0
date: 2026-09-03
owner: Supervisor Regional — GriyaNet
related:
  - "BRD - ERP SPVR.docx"
  - "Guidebook PRD.docx"
  - "Dashboard SPVR.md"
source_prototype: "https://github.com/Mualnudarza/Prototype-ERP-SPVR"
status: draft
tags: [prd, spvr, erp, griyanet, monitoring]
---

# PRD — Dashboard SPVR (Supervisor Regional) GriyaNet

> Dokumen ini disusun mengikuti struktur **Guidebook PRD** v1.0 (R. Billiyan Mulkan Ghifari, HRBA).
> Konten produk merujuk langsung pada prototype HTML statis di repositori `Prototype-ERP-SPVR` (vanilla HTML/CSS/JS, Bootstrap 5, Chart.js, dummy data CSV).

---

## Daftar Isi

- BAB 1 — Pendahuluan
- BAB 2 — Tujuan Produk & Sasaran
- BAB 3 — Kebutuhan Fungsional
- BAB 4 — Kebutuhan Non-Fungsional
- BAB 5 — Desain Sistem & Integrasi
- BAB 6 — Rencana Implementasi
- BAB 7 — Risiko & Strategi Mitigasi
- BAB 8 — Lampiran

---

## BAB 1 — Pendahuluan

### 1.1 Latar Belakang

GriyaNet beroperasi dengan banyak branch regional. **Supervisor Regional (SPVR)** membutuhkan satu pintu pantau (*single pane of glass*) yang menggabungkan indikator area, penjualan, operasional teknis, dan manpower untuk:

- Memvalidasi BRD Modul SPVR sebelum fitur built ke ERP inti.
- Memantau branch dalam cakupan regional (atau seluruh regional) tanpa berpindah-pindah modul.
- Mengakses data lintas-domain (area, sales, asset, infrastruktur, manpower) yang saat ini tersebar di beberapa halaman ERP existing.

Prototype ini menggunakan **dummy data** (CSV di `assets/data/`) untuk mensimulasikan kondisi nyata, sehingga validasi BRD bisa dilakukan tanpa menunggu backend tersedia.

### 1.2 Tujuan Proyek (SMART)

| # | Tujuan | Metrik |
|---|--------|--------|
| O1 | Menyediakan dashboard monitoring read-only bagi SPVR | ≥ 22 halaman prototype lulus visual review |
| O2 | Memvalidasi aturan bisnis (BRD) lewat dummy data | 100% rule utama tercermin di logika filter halaman |
| O3 | Mempercepat validasi UX sebelum masuk build ERP | Validasi selesai dalam 1 sprint (2 minggu) |
| O4 | Mempermudah diskusi lintas-role (SPVR, Branch, Tim Teknisi) | 1 layout konsisten (navbar + sidebar) di semua halaman |
| O5 | Menghilangkan ketergantungan pada server internal ERP existing | Style & data dilokalisasi di prototype |

### 1.3 Pemangku Kepentingan (Stakeholder)

| Peran | Tanggung Jawab | Akses Prototype |
|-------|----------------|-----------------|
| Project Director / Direktur HRGA | Approval akhir, sign-off PRD & BRD | Read |
| Supervisor Regional (SPVR) | User primer, validasi modul monitoring | Read |
| Branch Manager | Acuan cross-check data branch | Read |
| Account Executive & Tim Teknisi | Sumber data operasional | Read (data only) |
| Tim Produk (PM/PO) | Penulis & pemelihaga dokumen | Read/Write |
| Tim Engineering (FE/BE) | Kandidat implementer ERP | Read |
| Tim QA | Validasi acceptance criteria | Read |

### 1.4 Ruang Lingkup Produk

**In-Scope (Fase Prototype — Read-Only):**

- Dashboard utama (KPI ringkas).
- Modul **Area** (Coverage Area, Detail Area, Analisa Area Branch).
- Modul **Penjualan** (Retention, Customer Aktif, Pipeline, Performance AE).
- Modul **Operasional & Teknis** (PSB, Issue & TSO, Infrastruktur, Dismantle, Dismantle Performance, Distribution).
- Modul **Man Power Planning** (MPP).
- Modul **Implementasi Asset** (Perangkat, Modem, Kabel).
- Modul **Monitoring Infrastruktur** (Map Access, Monitor ODP, List Area Splitter, Progress Konfigurasi, Splitter No Config).
- Filter global branch, filter per-halaman (bulan/tahun/tanggal/status/area/tipe).
- Visualisasi (donut chart, KPI card, tabel dengan search + pagination + status badge).
- Modal read-only "Detail" untuk merepresentasikan halaman ERP existing.

**Out-of-Scope (Fase Saat Ini):**

- Create / Update / Delete transaksi (prototype read-only).
- Backend, database, API (semua data berasal dari CSV statis).
- Autentikasi & otorisasi pengguna.
- Notifikasi real-time / integrasi WhatsApp.
- Mobile-native app (prototype web responsif saja).
- Pelaporan PDF/Excel otomatis.
- Integrasi payment gateway.

### 1.5 Definisi Istilah & Referensi

| Istilah | Definisi |
|---------|----------|
| SPVR | Supervisor Regional — user primer dashboard |
| BRD | Business Requirement Document (acuan: `BRD - ERP SPVR.docx`) |
| PRD | Dokumen ini |
| Area Primary | Area yang dibuka oleh branch (`is_primary = 1`) — dihitung sebagai pembukaan area |
| Area Overlay | Area yang dijangkau branch tetapi dibuka branch lain (`is_primary = 0`) |
| PSB | Pemasangan Sambungan Baru |
| TSO | Trouble Shoot / teknisi onsite untuk gangguan |
| WO | Work Order |
| MPP | Man Power Planning — ketersediaan AE/Teknisi per branch |
| Fasum | Fasilitas Umum — kategori khusus pelanggan aktif |
| Dummy Data | Data simulasi di `assets/data/*.csv` |
| Read-only | Mode tampilan tanpa mutation; tombol "Detail" membuka modal/halaman informasi |

**Referensi:**

- BRD: `E:\WORKSPACE\PROJECT\WEB-APPS\DASHBOARD-SPVR\REQ\BRD - ERP SPVR.docx`
- Guidebook PRD: `E:\WORKSPACE\PROJECT\WEB-APPS\DASHBOARD-SPVR\REQ\Guidebook PRD.docx`
- Catatan desain dashboard: `E:\WORKSPACE\PROJECT\WEB-APPS\DASHBOARD-SPVR\REQ\Dashboard SPVR.md`
- Source prototype: <https://github.com/Mualnudarza/Prototype-ERP-SPVR>

---

## BAB 2 — Tujuan Produk & Sasaran

### 2.1 Visi Produk

> "Satu dashboard regional yang membuat SPVR dapat **memvalidasi**, **memonitor**, dan **mengambil keputusan** lintas-modul (area, sales, operasional, manpower, asset, infrastruktur) dalam satu tampilan konsisten tanpa akses tulis ke ERP inti."

### 2.2 Tujuan & Manfaat Produk

**Tujuan:**

- Mengonsolidasikan 22+ halaman monitoring regional.
- Menjamin konsistensi filter branch di seluruh modul.
- Menyediakan chart & KPI real-time berbasis dummy data untuk validasi UX.

**Manfaat:**

| Stakeholder | Manfaat |
|-------------|---------|
| SPVR | Akses cepat ke kondisi branch tanpa login multi-modul |
| Branch Manager | Benchmark antar branch via KPI dan tabel |
| Tim Produk | Validasi BRD sebelum biaya implementasi |
| Tim Engineering | Referensi UI/UX dan alur yang sudah disetujui |

### 2.3 Metrik Keberhasilan (KPIs)

| KPI | Baseline | Target (Pasca-Implementasi) |
|-----|----------|------------------------------|
| Jumlah modul monitoring aktif | 4 (Area, Sales, Op, MPP) | 6 (+ Asset, Infra) |
| Halaman prototype yang konsisten dengan layout | 0 | 22/22 |
| Rule BRD yang terefleksi di logika filter | 0% | 100% rule inti |
| Beban pikiran saat cross-modul check (skala 1-5) | 4 | 1 |
| Adoptasi SPVR terhadap dashboard | 0% aktif | ≥ 90% aktif mingguan |
| Kepuasan SPVR (NPS internal) | n/a | ≥ 40 |

### 2.4 Target Pengguna & User Persona

**Persona Utama — Supervisor Regional (SPVR)**

- **Nama:** Rina W.
- **Latar:** 8 tahun di GriyaNet, mengawasi 6 branch regional.
- **Tujuan:** Memantau KPI branch, mendeteksi anomali operasional, melakukan validasi data.
- **Tantangan:** Berpindah modul ERP, sulit membandingkan data lintas branch, tidak ada ringkasan default.
- **Perilaku:** Buka dashboard tiap pagi, drill-down ke modul operasional saat ada anomali.

**Persona Sekunder — Branch Manager**

- **Nama:** Andi P.
- **Latar:** Branch Manager 3 tahun.
- **Tujuan:** Membandingkan kinerja branch-nya dengan branch lain.
- **Perilaku:** Buka modul spesifik (Area, MPP, Dismantle) sesuai fokus mingguan.

**Persona Sekunder — Tim Engineering / QA**

- **Tujuan:** Mengacu pada prototype sebagai acuan UX sebelum build ERP.
- **Perilaku:** Membandingkan rule BRD dengan logika filter prototype.

---

## BAB 3 — Kebutuhan Fungsional

### 3.1 Fitur Utama (MoSCoW)

| Kode | Fitur | Prioritas |
|------|-------|-----------|
| F-A1 | Dashboard utama + 4 KPI ringkas (Branch, Customer Aktif, Isolir, Wait List Operasional) | **Must** |
| F-A2 | Modul Area — Coverage Area (filter Bulan/Tahun, tab Primary/Overlay/All, donut chart, tabel) | **Must** |
| F-A3 | Modul Area — Detail Area per branch (filter Primary/Overlay, aksi lihat poligon) | **Must** |
| F-A4 | Modul Area — Analisa Area Branch | **Should** |
| F-S1 | Modul Penjualan — Retention (Monitoring Customer Regional) | **Must** |
| F-S2 | Modul Penjualan — Customer Aktif & Fasum | **Must** |
| F-S3 | Modul Penjualan — Pipeline Penjualan | **Should** |
| F-S4 | Modul Penjualan — Performance AE (Cold Prospect) | **Should** |
| F-O1 | Modul Operasional — PSB (WO Instalasi & Wait List PSB, 4 status) | **Must** |
| F-O2 | Modul Operasional — Issue & TSO (WO TSO, Wait List TSO, 4 status) | **Must** |
| F-O3 | Modul Operasional — Infrastruktur | **Should** |
| F-O4 | Modul Operasional — Dismantle (WO + Wait List) | **Must** |
| F-O5 | Modul Operasional — Dismantle Performance | **Should** |
| F-O6 | Modul Operasional — Distribution (WO Distribution + Wait List Distribution, Splitter belum terkonfigurasi) | **Should** |
| F-M1 | Modul Man Power Planning — ketersediaan AE & Teknisi | **Should** |
| F-X1 | Modul Implementasi Asset — Perangkat | **Could** |
| F-X2 | Modul Implementasi Asset — Modem | **Could** |
| F-X3 | Modul Implementasi Asset — Kabel | **Could** |
| F-N1 | Modul Monitoring Infrastruktur — Map Access | **Could** |
| F-N2 | Modul Monitoring Infrastruktur — Monitor ODP | **Could** |
| F-N3 | Modul Monitoring Infrastruktur — List Area Splitter | **Could** |
| F-N4 | Modul Monitoring Infrastruktur — Progress Konfigurasi | **Could** |
| F-N5 | Modul Monitoring Infrastruktur — Splitter No Config | **Could** |
| F-C1 | Layout konsisten: navbar gelap + sidebar (Bootstrap 5, Material Icons) di semua halaman | **Must** |
| F-C2 | Filter global branch — event `globalBranchChange` memicu re-render semua halaman | **Must** |
| F-C3 | Tabel seragam: search + pagination + status badge (`assets/js/common.js`) | **Must** |
| F-C4 | Modal read-only "Detail" merepresentasikan halaman ERP existing | **Must** |
| F-C5 | Bullet chart & donut chart (`assets/js/common.js`, Chart.js) | **Should** |
| F-C6 | Breadcrumb + page header di setiap sub-halaman | **Should** |
| F-C7 | Multi-tab pada halaman Operasional (PSB/TSO/Dismantle/Distribution) | **Should** |

**Won't Have (Fase Ini):** otentikasi, write action, integrasi payment, notifikasi WA, export PDF/Excel, mobile-native.

### 3.2 User Stories / Use Cases

#### US-01 Dashboard
> Sebagai **SPVR**, saya ingin melihat **ringkasan total branch, customer aktif, isolir, dan wait list** di satu layar, sehingga saya dapat **langsung menilai kondisi regional** saat pertama membuka dashboard.

#### US-02 Filter Branch Global
> Sebagai **SPVR**, saya ingin memilih **branch tertentu** dan seluruh halaman modul mengikuti filter tersebut, sehingga saya dapat **fokus pada satu branch tanpa berpindah halaman**.

#### US-03 Coverage Area
> Sebagai **SPVR**, saya ingin memfilter **area dibuka per bulan/tahun** dan memisahkan tab **Primary vs Overlay**, sehingga saya dapat **memvalidasi aturan hanya Primary yang dihitung sebagai pembukaan area**.

#### US-04 Detail Area
> Sebagai **SPVR**, saya ingin membuka **detail area** dan melihat aksi **lihat poligon**, sehingga saya dapat **mengecek coverage geografis per branch**.

#### US-05 Retention
> Sebagai **SPVR**, saya ingin memonitor **customer aktif, isolir, dan terminate regional**, sehingga saya dapat **menilai efektivitas retensi**.

#### US-06 PSB
> Sebagai **SPVR**, saya ingin melihat **WO Instalasi hari ini dan Wait List PSB** dengan filter status (Menunggu Teknisi, Dalam Proses, Selesai, Gagal Instalasi), sehingga saya dapat **memantau progres instalasi**.

#### US-07 TSO
> Sebagai **SPVR**, saya ingin melihat **WO TSO Aktif dan Wait List TSO** dengan filter 4 status, sehingga saya dapat **mengawasi SLA penyelesaian gangguan**.

#### US-08 Dismantle
> Sebagai **SPVR**, saya ingin melihat **WO Disantle hari ini, menunggu penjadwalan, selesai, dan berjalan**, sehingga saya dapat **memantau eksekusi terminasi**.

#### US-09 Distribution
> Sebagai **SPVR**, saya ingin melihat **splitter belum terkonfigurasi, progress konfigurasi, splitter ready-to-WO, dan WO Distribution**, sehingga saya dapat **menilai kesiapan jaringan**.

#### US-10 MPP
> Sebagai **SPVR**, saya ingin melihat **ketersediaan AE dan Teknisi per branch**, sehingga saya dapat **mengalokasikan manpower**.

#### US-11 Modal Detail
> Sebagai **SPVR**, saya ingin menekan tombol **"Detail"** dan mendapatkan **popup read-only berisi seluruh field baris**, sehingga saya dapat **membandingkan perilaku tombol dengan ERP existing**.

#### US-12 Asset & Infra Monitoring (opsional fase lanjut)
> Sebagai **SPVR**, saya ingin memantau **perangkat, Modem, Kabel, ODP, Splitter, dan Konfigurasi** sehingga saya dapat **menilai utilisasi aset jaringan**.

**Identifikasi peran:** SPVR (primer), Branch Manager (sekunder), tim Engineering (konsultasi).

**Tujuan & manfaat:** setiap story berakhir dengan outcome keputusan (validasi, alokasi, deteksi anomali).

### 3.3 Alur Pengguna (User Flow)

**Flow 1 — Daily Monitoring SPVR**

```
Login ke ERP → Buka Dashboard SPVR
   ├─ Lihat 4 KPI (Branch / Customer Aktif / Isolir / Wait List)
   ├─ Pilih branch via filter global
   └─ Klik kartu modul:
        ├─ Modul Area → Coverage → Detail Area → (Lihat Poligon)
        ├─ Modul Sales → Retention → Customer Aktif → Pipeline
        ├─ Modul Operasional → Tab PSB/TSO/Dismantle/Distribution → Detail WO (modal)
        ├─ Modul MPP
        ├─ Modul Asset (Perangkat/Modem/Kabel)
        └─ Modul Infrastruktur (Map/ODP/Splitter)
```

**Flow 2 — Drill-Down Anomali**

```
Dashboard → KPI Wait List naik → Buka Modul Operasional
   → Tab PSB / TSO / Dismantle
   → Filter status "Gagal Instalasi" atau "Menunggu Pembayaran"
   → Klik "Detail" → Modal read-only tampilkan data lengkap
```

### 3.4 Wireframe / Mockup

Prototype sudah tersedia di `Prototype-ERP-SPVR/` (HTML statis). Tautan:

- Dashboard: `index.html`
- Modul Area: `pages/area/open-area.html`, `detail.html`, `analisa-area-branch.html`
- Modul Sales: `pages/sales/retention.html`, `customer-aktif.html`, `pipeline-penjualan.html`, `performance-ae.html`
- Modul Operasional: `pages/operational/psb.html`, `issue-tso.html`, `dismantle.html`, `dismantle-performance.html`, `infrastruktur.html`
- Modul MPP: `pages/manpower/mpp.html`
- Asset: `pages/asset-monitoring/perangkat.html`, `modem.html`, `kabel.html`
- Infrastruktur: `pages/infra-monitoring/map-access.html`, `monitor-odp.html`, `list-area-splitter.html`, `progress-konfigurasi.html`, `splitter-no-config.html`

Catatan: seluruh halaman sudah Bootstrap 5 + Inter font + Material Icons (CDN publik), dengan CSS lokal di `assets/css/style.css` agar mandiri.

---

## BAB 4 — Kebutuhan Non-Fungsional

### 4.1 Performa & Skalabilitas

- Prototype: muat penuh < 3 s di broadband 4G; semua aset via CDN + lokal CSS.
- Target produksi ERP: response time < 2 s untuk 90% request pada 1000 concurrent user per regional (rencana awal).
- Skalabilitas: arsitektur horizontal, load balancing di layer frontend, auto-scale backend.

### 4.2 Keamanan & Privasi Data

- **Prototype saat ini tidak menangani data sensitif nyata** (semua dummy CSV lokal).
- Standar acuan (fase lanjut): ISO 27001, NIST CSF.
- Enkripsi data at-rest dan in-transit (TLS 1.3).
- RBAC sesuai peran (SPVR, Branch Manager, Admin, Viewer).
- Audit log untuk akses modul finansial (Retention, Disantle Performance).
- Privasi: patuhi UU PDP (Indonesia) — hak akses, retensi, dan pemusnahan data.

### 4.3 Kepatuhan Regulasi

- **UU PDP** (Pelindungan Data Pribadi).
- **UU ITE** untuk data elektronik.
- Standar industri ISP Indonesia (Bakti/BRTI bila relevan untuk SLA jaringan).

### 4.4 Ketersediaan & Keandalan

- Target uptime ERP hasil build: 99.9% (8.76 jam downtime/tahun).
- RTO < 4 jam, RPO < 1 jam untuk data operasional.
- Monitoring: uptime check, alert otomatis untuk response time > 3 s atau error rate > 1%.

### 4.5 Pemeliharaan & Operasional

- Prototype: perbarui CSV di `assets/data/` lalu refresh halaman; tidak ada build step.
- ERP hasil build: pipeline CI/CD, rollback otomatis, release notes per-PR.

---

## BAB 5 — Desain Sistem & Integrasi

### 5.1 Gambaran Umum Arsitektur (Prototype)

```
┌──────────────────────────────────────────────────────┐
│ Browser (statis, tanpa server)                       │
│ ┌──────────────────────────────────────────────────┐ │
│ │ index.html + pages/**/*.html                     │ │
│ │   └─ Bootstrap 5 (CDN)                           │ │
│ │   └─ Chart.js (CDN)                              │ │
│ │   └─ Material Icons (CDN)                        │ │
│ │   └─ assets/css/style.css (lokal)                │ │
│ │   └─ assets/js/data.js   (CSV → JS array)        │ │
│ │   └─ assets/js/common.js (tabel, badge, modal)   │ │
│ │   └─ assets/js/layout.js (navbar + sidebar)      │ │
│ └──────────────────────────────────────────────────┘ │
│              ▲                                        │
│              │ fetch CSV (otomatis dimuat)             │
│              ▼                                        │
│ assets/data/*.csv (dummy data statis)                 │
└──────────────────────────────────────────────────────┘
```

### 5.2 Komponen Utama

| Komponen | Lokasi Prototype | Tanggung Jawab |
|----------|------------------|----------------|
| Navbar | `assets/js/layout.js` (selector `#app-navbar`) | Header gelap + identitas user (default `ROLE_VIEW="spvr"`) |
| Sidebar | `assets/js/layout.js` (selector `#app-sidebar`) | Menu modul sesuai `ACTIVE_MENU` per halaman |
| Halaman modul | `pages/<modul>/*.html` | Render KPI + tabel + chart + modal |
| Data layer | `assets/data/*.csv` | Sumber data statis |
| Common helper | `assets/js/common.js` | `renderSimpleTable`, `badge`, bullet chart |
| Layout helper | `assets/js/layout.js` | `getGlobalBranch`, render navbar/sidebar |

### 5.3 Integrasi dengan Sistem Lain (Rencana Fase Lanjut)

| Sistem | Arah | Protokol |
|--------|------|----------|
| ERP GriyaNet inti | Read-only fetch data branch, customer, WO | REST/JSON |
| Billing system | Read status pembayaran untuk Retention | REST |
| Ticketing/Complaint | Read WO TSO & wait list | REST/Webhook |
| Network monitoring (Zabbix/LibreNMS) | Read status ODP/splitter | SNMP → API |
| SSO internal | OIDC | OIDC |

### 5.4 Batasan Teknologi & Asumsi Teknis

- Prototype: **tanpa build step** (langsung buka via `python -m http.server` atau file://).
- Frontend ERP hasil: React/Vue + TypeScript (alternatif dievaluasi saat build).
- Backend: Node.js/Go + PostgreSQL + Redis cache.
- Infrastruktur: Docker + Kubernetes + CI/CD GitHub Actions.
- Asumsi data: data dummy mewakili volume 6 branch × ±500 customer × ±100 WO/bulan.
- Asumsi jaringan: CDN publik (jsdelivr, fonts.googleapis.com) selalu tersedia untuk prototype; untuk produksi gunakan mirror internal.

---

## BAB 6 — Rencana Implementasi

### 6.1 Prioritas Fitur (Rilis)

| Rilis | Cakupan | Catatan |
|-------|---------|---------|
| **R0 (saat ini)** | Prototype HTML statis read-only 22 halaman | Sudah selesai |
| **R1 — MVP Build ERP** | F-A1, F-A2, F-A3, F-S1, F-S2, F-O1, F-O2, F-O4, F-C1..C4 | Backend read-only + filter global |
| **R2 — Pelengkap** | F-A4, F-S3, F-S4, F-O3, F-O5, F-O6, F-M1, F-C5..C7 | Chart lanjutan + MPP |
| **R3 — Aset & Infra** | F-X1..F-X3, F-N1..F-N5 | Integrasi network monitoring |

### 6.2 Peta Jalan & Linimasa Tingkat Tinggi

| Fase | Durasi | Deliverable |
|------|--------|-------------|
| Discovery & validasi prototype | 2 minggu | Sign-off PRD + keputusan prioritas R1 |
| Build MVP (R1) | 6-8 minggu | Dashboard + 4 modul utama + filter global |
| UAT & rilis R1 | 2 minggu | Migrasi SPVR ke ERP baru |
| R2 (pelengkap) | 4-6 minggu | Chart + MPP + dismantle performance |
| R3 (aset + infra) | 6-8 minggu | Integrasi network monitoring |

### 6.3 Dependensi & Ketergantungan

- **Backend API siap** (read-only endpoints) sebelum R1.
- **Tim Data** menyediakan seed data produksi yang mirip struktur CSV dummy.
- **Tim Network** menyediakan feed untuk modul Asset & Infrastruktur (R3).
- **Tim DevOps** menyediakan environment staging yang identik dengan produksi.

---

## BAB 7 — Risiko & Strategi Mitigasi

| # | Risiko | Dampak | Probabilitas | Strategi Mitigasi |
|---|--------|--------|--------------|-------------------|
| R-01 | Aturan BRD berubah setelah build | Sedang | Sedang | Prototype sebagai *living spec*; review PRD tiap sprint |
| R-02 | Volume data produksi jauh lebih besar dari dummy CSV | Tinggi | Tinggi | Lakukan *load test* dengan data masking setara produksi 10x sebelum R1 |
| R-03 | SPVR tidak adopsi dashboard baru | Tinggi | Sedang | Onboarding + champion per branch + monitoring NPS internal |
| R-04 | CDN publik tidak tersedia saat prototype demo | Rendah | Rendah | Mirror aset ke `assets/` lokal; sediakan fallback |
| R-05 | Inkonsistensi layout antar halaman | Sedang | Rendah | `layout.js` sebagai single source of navbar/sidebar; cek visual tiap PR |
| R-06 | Data dummy keliru dianggap data nyata | Sedang | Sedang | Banner "Dummy Data" di setiap halaman + label `[PROTOTYPE]` di judul tab |
| R-07 | Integrasi network monitoring tertunda | Sedang | Tinggi | R3 ditunda; sediakan data CSV manual untuk modul Asset/Infra |
| R-08 | Scope creep (tambah write-action) | Tinggi | Sedang | Komite produk kawal scope R1 sesuai BAB 1.4 |

---

## BAB 8 — Lampiran

### 8.1 Peta Modul ↔ Halaman Prototype

| Modul | Halaman |
|-------|---------|
| Dashboard | `index.html` |
| Area | `pages/area/open-area.html`, `detail.html`, `analisa-area-branch.html` |
| Penjualan | `pages/sales/retention.html`, `customer-aktif.html`, `pipeline-penjualan.html`, `performance-ae.html` |
| Operasional & Teknis | `pages/operational/psb.html` (PSB/TSO/Dismantle/Distribution), `issue-tso.html`, `dismantle.html`, `dismantle-performance.html`, `infrastruktur.html` |
| Man Power Planning | `pages/manpower/mpp.html` |
| Implementasi Asset | `pages/asset-monitoring/perangkat.html`, `modem.html`, `kabel.html` |
| Monitoring Infrastruktur | `pages/infra-monitoring/map-access.html`, `monitor-odp.html`, `list-area-splitter.html`, `progress-konfigurasi.html`, `splitter-no-config.html` |

### 8.2 Daftar Dataset Dummy (CSV)

`assets/data/`: `ae_data.csv`, `area_targets.csv`, `areas.csv`, `branches.csv`, `customers.csv`, `histori_dismantle.csv`, `histori_tso.csv`, `history_batch_modem.csv`, `history_cable.csv`, `modem.csv`, `olts.csv`, `packages.csv`, `purchase_history.csv`, `replace_modem.csv`, `return_modem.csv`, `routers.csv`, `sisa_kabel.csv`, `sisa_kabel_close.csv`, `stock_cable.csv`, `team_monitoring.csv`, `teams.csv`, `terminate_modem.csv`, `vlans.csv`, `waitlist_distribution.csv`, `waitlist_psb.csv`, `waitlist_tso.csv`, `wo_dismantle.csv`, `wo_distribution.csv`, `wo_instalasi.csv`, `wo_tso.csv`.

### 8.3 Aturan Bisnis Kunci (Refleksi di Prototype)

1. Hanya area `is_primary = 1` dihitung sebagai pembukaan area (lihat `pages/area/open-area.html`).
2. Filter global branch konsisten di seluruh halaman via `globalBranchChange` event.
3. Dismantle: hanya `is_primary` branch yang mengusulkan terminasi.
4. PSB: status `Selesai` menandai WO instalasi tuntas dan customer berpindah ke aktif.
5. TSO: 4 status (Wait List, Penjadwalan, Dalam Proses, Selesai).
6. Distribution: Splitter tanpa konfigurasi menjadi sumber WO Distribution; fase `Dalam Proses` sampai `Selesai`.
7. MPP: AE & Teknisi dipantau per branch dengan rasio coverage.

### 8.4 Acceptance Criteria Prototype (Read-Only)

- [ ] 22 halaman dapat dibuka tanpa error konsol.
- [ ] Filter global branch mengubah minimal 1 KPI di dashboard.
- [ ] Setiap modul utama menampilkan tabel dengan search + pagination + badge status.
- [ ] Tombol "Detail" pada WO membuka modal berisi semua field baris.
- [ ] Chart (donut/bullet) muncul tanpa error.
- [ ] Layout (header gelap + sidebar) konsisten di semua halaman.
- [ ] Tidak ada panggilan API backend; data sepenuhnya dari CSV lokal.

### 8.5 Catatan Desain

- Style mengikuti template ERP existing (Bootstrap 5, warna netral, hover tabel, card).
- CSS orisinil ERP (`dashboard.css`, `sidebar.css`) tidak tersedia di domain internal sehingga direplikasi di `assets/css/style.css` agar prototype berdiri sendiri.
- Setiap halaman read-only (monitoring & validasi), tidak ada create/update/delete.
- Tombol "Detail" merepresentasikan halaman ERP existing sesuai catatan BRD.

---

*Dokumen ini mengikuti struktur 8 BAB dari Guidebook PRD v1.0 (HRBA, 1 September 2025). Konten produk spesifik untuk Dashboard SPVR GriyaNet, dirujuk langsung dari prototype HTML statis `Prototype-ERP-SPVR`.*