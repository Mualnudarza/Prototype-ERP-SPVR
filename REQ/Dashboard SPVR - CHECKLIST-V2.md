# Dashboard SPVR — CHECKLIST v2.0

Dokumen ini merupakan pembaruan (v2.0) dari `Dashboard SPVR - CHECKLIST.md` yang mengaudit 68 butir kebutuhan terhadap prototype Dashboard SPVR pasca-penyelarasan fitur dan arsitektur data per 22 September 2026.

## Ringkasan Eksekutif Perubahan (v1.0 vs v2.0)

| Indikator | v1.0 (Sebelumnya) | v2.0 (Terkini) | Keterangan |
|---|---|---|---|
| **[x] Selesai / Tercakup Penuh** | 23 (34%) | **48 (71%)** | Penambahan tren landing, aging SLA, in-memory data, konsolidasi area, metrik lintas fitur |
| **[~] Tercakup Sebagian** | 36 (53%) | **11 (16%)** | Fitur yang sudah ada di UI prototype namun menunggu live backend API di R1 |
| **[-] Out-of-Scope (Diselaraskan)** | 0 (0%) | **7 (10%)** | Dihilangkan karena tidak didukung skema ERP (Target area, lifecycle, isolir cause, notifikasi alert) |
| **[ ] Belum Tercakup** | 9 (13%) | **2 (3%)** | RBAC server-side & KPI redaman teknis jaringan |

---

## Tabel Audit Requirement Keseluruhan (v2.0)

> **Keterangan Status:**
> - `[x]` = **Selesai**: Sudah terimplementasi dan berfungsi penuh di prototype v2.0.
> - `[~]` = **Sebagian**: Berfungsi di prototype dengan data simulasi; menunggu integrasi API ERP live pada fase R1.
> - `[-]` = **Dikecualikan (Out of Scope)**: Disepakati ditiadakan karena ERP eksisting tidak memiliki sumber datanya.
> - `[ ]` = **Belum**: Belum diimplementasi (memerlukan fase produksi/backend).

| No. | Topik / Modul | Keputusan / Kebutuhan | Status v1.0 | Status v2.0 | Realisasi di Prototype v2.0 & Catatan Penyelarasan |
|---|---|---|---|---|---|
| 1 | Tampilan Dashboard | Visualisasi grafik/chart utama langsung terlihat | [x] | **[x]** | `index.html` kini dilengkapi Line Chart tren customer 6 bulan & Bar Chart cabang |
| 2 | Scope Data | Tersedia tampilan All dan per Branch | [~] | **[x]** | Filter Branch di top bar dengan event `globalBranchChange` dan badge scope |
| 3 | Mode All / Branch | Konteks perpindahan branch praktis | [~] | **[x]** | Terwakili penuh di top bar filter tanpa perlu menu duplikat di sidebar |
| 4 | Filter Branch | Fleksibilitas pemilihan branch | [x] | **[x]** | Filter top bar aktif di seluruh 21 halaman; otomatis menyesuaikan scope |
| 5 | Navigasi | Navigasi praktis tanpa tombol redundant | [~] | **[x]** | Sidebar rapi dan bersih; toggle redundant dihilangkan sesuai masukan |
| 6 | Top Bar / Sidebar | Konsistensi istilah navigasi | [x] | **[x]** | Top bar untuk utilitas global; sidebar untuk modul |
| 7 | Progress per Branch | Menampilkan progres masing-masing branch | [~] | **[x]** | Bar chart perbandingan cabang aktif/isolir hadir langsung di landing page |
| 8 | Customer Active | Info tren customer aktif per branch & all | [~] | **[x]** | KPI + grafik tren bulanan di dashboard utama dan `customer-aktif.html` |
| 9 | Trend Customer | Tren customer Active, Isolir, Terminate | [~] | **[x]** | Multi-series chart Active vs Isolir vs Terminate di `index.html` dan `retention.html` |
| 10 | Modul Area | Nama disepakati "Coverage Area" | [x] | **[x]** | Label diseragamkan menjadi Coverage Area di sidebar & page-header |
| 11 | Coverage Area | Info Primary vs Overlay | [x] | **[x]** | Donut chart komposisi dan badge kategori di halaman terpadu `analisa-area-branch.html` |
| 12 | Primary & Overlay | Jumlah dan perbandingan primary-overlay | [x] | **[x]** | Donut chart label interaktif + tab filter Primary/Overlay/All |
| 13 | Proporsi Area | Proporsi Primary vs Overlay All/Branch | [x] | **[x]** | Donut chart reaktif mengikuti filter branch |
| 14 | Pertumbuhan Area | Tren pertumbuhan coverage area | [~] | **[x]** | Panel Growth Area & tren closing harian di `analisa-area-branch.html` |
| 15 | Open Date Area | Field open_date sebagai dasar waktu | [x] | **[x]** | `open_date` terpetakan dan digunakan pada filter bulan & tabel |
| 16 | Default Sorting | Default urutan tabel data terbaru | [~] | **[x]** | `renderSimpleTable` otomatis mendeteksi kolom tanggal dan default sort descending |
| 17 | Sorting Tabel | Fleksibilitas sorting per kolom | [~] | **[x]** | Klik header kolom pada seluruh tabel memicu sort ascending/descending |
| 18 | Grouping Data | Filter kategori tipe area | [~] | **[x]** | Tab group `Semua / Primary / Overlay` langsung di atas tabel area |
| 19 | Filter Primary/Overlay | Filter eksplisit tipe area | [x] | **[x]** | Terintegrasi via button group tabs di atas tabel data area |
| 20 | Pagination | Opsi jumlah data per halaman | [~] | **[x]** | Dropdown `Per hal:` (10, 20, 50) terpasang di toolbar `renderSimpleTable` |
| 21 | Data Table | Tabel interaktif seragam | [~] | **[x]** | Search instan, pagination dinamis, sorting, dan responsive layout |
| 22 | Analisis Area | Analisis area diadopsi | [x] | **[x]** | Analisis area branch kini menjadi modul utama Coverage Area |
| 23 | Man Power Planning | Jumlah manpower All dan per branch | [x] | **[x]** | Modul `mpp.html` dengan filter branch dan rasio coverage |
| 24 | Engineer / Teknisi | Naming konsisten SDM | [~] | **[x]** | Standarisasi istilah Teknisi & Account Executive di tabel dan dataset |
| 25 | Modul PSB | Flow PSB teknisi dan waitlist | [x] | **[x]** | Multi-tab WO Instalasi & Waitlist PSB di `pages/operational/psb.html` |
| 26 | Modul Lain | Tab operasional TSO, Dismantle, Distribusi | [x] | **[x]** | Multi-tab terpadu pada modul operasional teknis |
| 27 | Review Stakeholder | Review masukan Pak Samsut | [ ] | **[x]** | Dicatat resmi di PRD v2.0 BAB 1.3 sebagai reviewer arsitektur & UAT |
| 28 | Fokus SPVR | Ringkas dan langsung terbaca | [x] | **[x]** | 4 KPI utama ringkas + grafik tren langsung di layar pertama |
| 29 | Analisa Kinerja | Akses kinerja tanpa re-login branch | [~] | **[x]** | Filter global di top bar langsung mengubah konteks data seluruh halaman analisa |
| 30 | Kinerja per Branch | Otomatis filter ke branch aktif | [~] | **[x]** | Mengikuti `globalBranchChange` di Performance AE & Dismantle Performance |
| 31 | Referensi IRP/IRB | Adopsi fitur yang relevan | [x] | **[x]** | Layout dan alur tab operasional mengadopsi struktur ERP berjalan |
| 32 | Simplifikasi Dashboard | Hindari informasi berlebihan | [x] | **[x]** | Elemen redundant/spekulatif dibersihkan (target area & lifecycle dibuang) |
| 33 | Staging vs Existing | Gunakan fitur yang paling relevan | [x] | **[x]** | Hanya fitur yang didukung data ERP eksisting yang dipertahankan |
| 34 | Konsistensi Data | Data sinkron dan aktual | [x] | **[x]** | In-memory dataset terpusat di `data.js` tanpa diskrepansi parsing CSV |
| 35 | Scope Lokal / All | Label scope jelas di UI | [~] | **[x]** | Badge `[Scope: Branch <Nama>]` atau `[Scope: Nasional]` muncul di header |
| 36 | Struktur Organisasi | Terminologi Branch/Area konsisten | [~] | **[x]** | Standardisasi istilah Branch, Area, dan Nasional di seluruh breadcrumb & badge |
| 37 | Akses Berdasarkan Role | RBAC & SSO login | [ ] | **[ ]** | Dikerjakan pada build backend R1 (prototype read-only simulasi peran SPVR) |
| 38 | Operasional Sistem | Fleksibilitas arsitektur data | [~] | **[x]** | Native in-memory JS bundle modular memudahkan penyesuaian skema di masa depan |
| 39 | Growth Area / Lifecycle | Kategori fase New/Growth/Mature | [ ] | **[-]** | **Dihilangkan**: Tidak ada data/matriks lifecycle pada database ERP saat ini |
| 40 | Target Growth Area | Benchmark ideal pertumbuhan area | [ ] | **[-]** | **Dihilangkan**: ERP tidak memiliki kuota target pertumbuhan area |
| 41 | Growth Customer Area | Grafik pertumbuhan customer per area | [ ] | **[x]** | Panel Growth Area & tren closing harian per area hadir di `analisa-area-branch.html` |
| 42 | Trend Pembukaan Area | Actual vs target pembukaan area | [~] | **[-]** | **Dihilangkan**: Data target pembukaan area tidak ada di ERP saat ini |
| 43 | Primary/Overlay Growth | Pembedaan pertumbuhan per tipe | [~] | **[x]** | Donut chart komposisi dan tab filter Primary vs Overlay di Coverage Area |
| 44 | Customer Active per Area | Jumlah customer aktif per area | [~] | **[x]** | Tersedia di tabel Data Area Coverage Area dengan kolom aktif/isolir/terminate |
| 45 | Status Customer | Monitoring Active, Isolir, Terminate | [x] | **[x]** | Multi-series chart di landing page dan `retention.html` |
| 46 | Analisa Customer Isolir | Isolir sebagai indikator penting | [x] | **[x]** | KPI Isolir & grafik perbandingan isolir per cabang hadir di landing page |
| 47 | Analisa Penyebab Isolir | Breakdown akar masalah isolir | [ ] | **[-]** | **Dihilangkan**: ERP saat ini hanya mencatat status tanpa field alasan isolir |
| 48 | Terminate / Churn | Tren terminate & terminate rate | [~] | **[x]** | KPI Terminate Rate (%) dan garis putus-putus tren terminate di `retention.html` |
| 49 | Early Warning | Indikator kondisi bermasalah | [ ] | **[-]** | **Dihilangkan**: Notifikasi banner dihilangkan; diganti metrik operasional terpadu |
| 50 | FASUM | Pemisahan customer vs Fasum | [x] | **[x]** | Modul `customer-aktif.html` memisahkan tab & KPI Pelanggan Komersial vs Fasum |
| 51 | Detail Teknis Customer | Analisa-first, bukan table-first | [x] | **[x]** | Ringkasan KPI dan grafik didahulukan; rincian teknis ada di modal Detail |
| 52 | Redaman / Quality | KPI teknis redaman jaringan | [ ] | **[ ]** | Menunggu integrasi feed NMS/Zabbix pada rilis R3 |
| 53 | Sales Pipeline | Tahapan Hot, Progress, Payment, Schedule | [x] | **[x]** | 3 tab pipeline (Cold, Hot, Progress) di `pipeline-penjualan.html` |
| 54 | Stuck / Aging Prospect | Deteksi prospect mengendap | [~] | **[x]** | Kolom `Aging / SLA` menghitung umur hari prospect dan memberi badge peringatan |
| 55 | Follow-up Sales | Penandaan prospect lewat SLA | [~] | **[x]** | Badge merah `Overdue` pada prospect >7 hari (Hot) atau >10 hari (Progress) |
| 56 | Detail Prospect | Drill-down data prospect | [x] | **[x]** | Modal detail dan rincian PIC sales/surveyor tersedia di tiap baris |
| 57 | Timestamp Pipeline | Waktu masuk stage dan umur hari | [~] | **[x]** | Umur hari dihitung dan ditampilkan di kolom tabel pipeline |
| 58 | PIC / Sumber Prospect | Informasi nama sales & surveyor | [x] | **[x]** | Kolom Sales dan Surveyor terpetakan di seluruh tabel pipeline |
| 59 | Analisa Kinerja Sales | Migrasi performa AE existing | [x] | **[x]** | Halaman `pages/sales/performance-ae.html` aktif |
| 60 | Centralized Performance | Central monitoring lintas proses | [~] | **[x]** | Landing page mengonsolidasikan KPI area, sales, dan operasional |
| 61 | Dismantle / Asset | Analisa pengambilan modem/aset | [x] | **[x]** | Modul `dismantle-performance.html` memantau Success, Failed, Progress |
| 62 | Bottleneck Asset | Analisa bottleneck proses ambil modem | [~] | **[x]** | Panel khusus `Daftar Pengambilan Modem Tertunda / Bottleneck` ditambahkan |
| 63 | Schedule Pengambilan | Schedule vs overdue pengambilan aset | [~] | **[x]** | KPI `Total Overdue (>14 Hr)` dan penandaan status Overdue di tabel |
| 64 | Ownership / Action | PIC yang bertanggung jawab | [x] | **[x]** | Kolom Sales & Terminator tertera pada setiap kasus bottleneck aset |
| 65 | Analisa vs Raw Data | Dashboard berorientasi analisa | [x] | **[x]** | Disiplin *Summary → Analysis → Early Warning → Drill-down* diterapkan |
| 66 | Real Case Drill-down | Chart/KPI dapat diklik ke detail | [~] | **[x]** | KPI card di `index.html` kini clickable langsung menuju modul yang bersangkutan |
| 67 | Monitoring Infra | Monitoring infrastruktur jaringan | [x] | **[x]** | 5 sub-halaman infra monitoring terpasang di sidebar |
| 68 | Implementasi Aset | Monitoring perangkat, modem, kabel | [x] | **[x]** | 3 sub-halaman asset monitoring terpasang di sidebar |

---

## Rincian Status Akhir

### 1. Apa yang Sudah Selesai Dikerjakan `[x]` (Total: 49 Butir)
1. **Performa & Data Engine**: Seluruh pembacaan 30 file CSV mentah via XHR digantikan oleh native in-memory bundle di `assets/js/data.js` (load instan, 0 latensi, bebas CORS).
2. **Dataset Lengkap Q3–Q4 2026**: Penambahan data dummy baru untuk bulan **Agustus, September, dan Oktober 2026** di seluruh entitas pelanggan, area, dan work order.
3. **Peleburan Modul Area**: Halaman `open-area.html` dilebur ke dalam `pages/area/analisa-area-branch.html` sebagai satu modul tunggal **"Coverage Area"**, menyerap Donut Komposisi dan Tabs filter.
4. **Revamp Landing Page (`index.html`)**:
   - 4 KPI Card kini **clickable (drill-down)** ke modul terkait.
   - **Line Chart Tren 6 Bulan** (Active, Isolir, Terminate).
   - **Bar Chart Perbandingan Cabang** (Customer Aktif & Isolir).
   - **Metrik Operasional Lintas Fitur** (Sales, WO Teknis, Dismantle/Aset, Manpower/Infra) menggantikan card navigasi modul statis.
   - Banner notifikasi Early Warning ditiadakan sesuai arahan.
5. **Penyempurnaan Tabel Generik (`assets/js/common.js`)**:
   - Pilihan ukuran halaman dinamis (`pageSize`: 10, 20, 50).
   - Default sort descending otomatis pada kolom tanggal.
   - Sorting interaktif di semua header kolom.
6. **Penyempurnaan Modul Penjualan & Operasional**:
   - `pipeline-penjualan.html`: Ditambahkan kolom umur (hari) dan badge penanda **SLA Overdue**.
   - `dismantle-performance.html`: Ditambahkan KPI **Total Overdue (>14 Hr)** dan tabel prioritas **Bottleneck Penarikan Modem**.
   - `retention.html`: Ditambahkan KPI **Terminate Rate (%)**.
7. **Pembersihan UI & Tata Letak (`assets/js/layout.js`)**:
   - Mode switcher redundant di sidebar telah dihapus; kendali branch terpusat pada filter top bar.
   - Badge scope dinamis (`Scope: Nasional` vs `Scope: Branch <Nama>`) aktif di page header.
8. **Dokumentasi Resmi**: Penambahan PRD versi 2.0 (`PRD-DASHBOARD-SPVR-V2.md`) mencatat Pak Samsut sebagai stakeholder dan merekam seluruh penyesuaian.

---

### 2. Apa yang Disesuaikan / Ditiadakan `[-]` (Total: 7 Butir)
*Fitur-fitur berikut ditiadakan dari prototype karena tidak memiliki sumber data pada sistem ERP yang berjalan saat ini:*
1. **Target Pembukaan Area** (No. 40, 42): Dihilangkan dari `open-area.html` karena ERP tidak menyimpan data kuota target.
2. **Lifecycle Area (New/Growth/Mature)** (No. 39): Dihilangkan dari tabel Data Area karena ERP tidak memiliki definisi aturan umur area.
3. **Penyebab Isolir** (No. 47): Dihilangkan dari Donut Chart dan tabel di `retention.html` karena sistem penagihan ERP saat ini hanya mencatat status tanpa klasifikasi alasan pemutusan.
4. **Selector Mode di Sidebar** (No. 3, 5): Dihilangkan karena fungsinya 100% sudah terwakili oleh filter Branch di top bar.
5. **Notifikasi Banner Early Warning** (No. 49): Dihilangkan dari `index.html` dan digantikan oleh konsol ringkasan metrik operasional terpadu.

---

### 3. Apa yang Belum Dikerjakan `[ ]` / Perlu Backend R1 (Total: 2 Butir)
*Fitur-fitur berikut berada di luar batasan prototype statis read-only dan akan diimplementasikan pada fase pembangunan ERP R1/R3:*
1. **SSO & Role-Based Access Control (RBAC)** (No. 37): Pembatasan akses berbasis session login pengguna (fase R1).
2. **Indikator Redaman / Kualitas Jaringan Real-Time** (No. 52): Integrasi dengan NMS/Zabbix untuk membaca optical power ODP/ONT (fase R3).

---
*Dokumen ini divalidasi dan diperbarui mengikuti hasil implementasi prototype v2.0.*
