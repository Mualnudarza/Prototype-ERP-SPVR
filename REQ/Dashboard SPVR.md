# Dashboard SPVR

Dokumen ini merangkum keseluruhan hasil pembahasan terkait dashboard SPVR, Coverage Area, Customer, Man Power Planning, Sales Pipeline, Analisa Kinerja, Asset/Dismantle, serta konsep mode dan navigasi.

## Tabel Requirement Keseluruhan

| No. | Topik / Modul | Pembahasan | Keputusan / Kebutuhan | Tindak Lanjut |
|---|---|---|---|---|
| 1 | Tampilan Dashboard | Dashboard diharapkan lebih mudah dipahami tanpa terlalu banyak eksplorasi manual. | Tampilan lebih diarahkan ke **chart/grafik** agar informasi utama langsung terlihat. | Tambahkan visualisasi tren dan komposisi pada tiap modul. |
| 2 | Scope Data | User perlu melihat data secara keseluruhan maupun per branch. | Harus tersedia tampilan **All** dan **per Branch**. | Terapkan konsep mode/scope data. |
| 3 | Mode All / Branch | Saat ini perpindahan konteks branch dianggap terlalu bergantung pada filter atau akun/login. | Buat **mode All** dan **mode per Branch** yang dinaungi user. | Mode dapat dipilih dari navigasi/sidebar dan langsung memengaruhi data dashboard. |
| 4 | Filter Branch | Walaupun sudah ada mode branch, filter masih dianggap berguna untuk fleksibilitas. | Pada **mode All**, filter branch tetap tersedia. Pada **mode branch tertentu**, data otomatis fokus ke branch tersebut. | Sesuaikan behavior filter dengan mode aktif. |
| 5 | Navigasi | Perpindahan mode diharapkan lebih praktis daripada logout/login atau filter berulang. | Pilihan mode sebaiknya ditempatkan di **sidebar/navigation**. | Tambahkan selector mode pada sidebar. |
| 6 | Top Bar / Sidebar | Ada pembahasan istilah navigasi. | Navigasi atas disebut **top bar**, navigasi samping disebut **sidebar**. | Sesuaikan istilah pada desain/dokumentasi. |
| 7 | Progress per Branch | SPVR perlu mengetahui perkembangan masing-masing branch yang dinaungi. | Dashboard harus dapat menampilkan **performance/progress per branch**. | Buat chart atau summary per branch. |
| 8 | Customer Active | Data customer active saat ini mencakup seluruh data. | Perlu informasi jumlah/tren customer aktif **per branch** maupun keseluruhan. | Tambahkan chart customer aktif per branch. |
| 9 | Trend Customer | SPVR perlu melihat perkembangan customer. | Tampilkan tren customer seperti **Active, Isolir, Terminate** sesuai data yang tersedia. | Buat grafik tren customer, mengacu pada data yang saat ini ada di Superset/BI. |
| 10 | Modul Area | Nama modul awalnya disebut Area. | Nama modul disepakati menjadi **Coverage Area**. | Ubah label modul menjadi Coverage Area. |
| 11 | Coverage Area | SPVR perlu mengetahui luas/komposisi area yang ditangani. | Coverage Area berisi informasi **Primary Area** dan **Overlay Area**. | Buat summary dan detail primary vs overlay. |
| 12 | Primary & Overlay | Ada target pembukaan primary area dan kebutuhan mengetahui overlay area. | SPVR harus dapat melihat jumlah **Primary**, **Overlay**, dan total area. | Tambahkan KPI dan perbandingan primary-overlay. |
| 13 | Proporsi Area | Dibutuhkan pemahaman komposisi area per branch maupun seluruh area yang dinaungi. | Tampilkan proporsi Primary vs Overlay secara **All/per Branch**. | Gunakan chart komposisi seperti bar/donut sesuai desain. |
| 14 | Pertumbuhan Area | Tidak hanya kondisi saat ini, tetapi perkembangan area juga perlu diketahui. | Tambahkan **trend pertumbuhan Coverage Area**. | Gunakan tanggal opening area untuk grafik tren. |
| 15 | Open Date Area | Sebelumnya sempat dianggap tidak tersedia, tetapi ternyata terdapat data opening area di staging. | Gunakan field **Open Date / tanggal open area** sebagai dasar sorting/trend. | Validasi field tanggal pada staging dan production. |
| 16 | Default Sorting | User ingin data terbaru muncul lebih dahulu. | Default urutan tabel adalah **data terbaru**. | Sort default berdasarkan Open Date descending. |
| 17 | Sorting Tabel | Selain default terbaru, user membutuhkan fleksibilitas. | Tabel harus bisa di-sort berdasarkan beberapa kolom. | Aktifkan sorting kolom seperti tanggal open, kode area, dll. |
| 18 | Grouping Data | Ada kebutuhan melihat data berdasarkan kategori tertentu. | Data dapat dikelompokkan berdasarkan kategori, misalnya **tanggal open**, kode area, atau tipe area. | Evaluasi fitur grouping/filter pada data table. |
| 19 | Filter Primary / Overlay | Walaupun tipe dapat dikenali dari kode area, user ingin lebih eksplisit. | Sediakan filter **All / Primary / Overlay**. | Tambahkan filter tipe area. |
| 20 | Pagination | Jumlah data per halaman dibahas sekitar 20 data. | Default dapat menggunakan **20 record per halaman**, tetapi sebaiknya fleksibel. | Tambahkan opsi jumlah data per halaman. |
| 21 | Data Table | Untuk kemudahan eksplorasi data, tabel standar dinilai lebih fleksibel. | Gunakan **data table** yang mendukung sorting/filter/pagination. | Implementasikan tabel interaktif. |
| 22 | Analisis Area | Coverage Area sebaiknya tidak hanya menampilkan daftar area. | Tambahkan **analisis area** seperti yang sudah ada di IRP/IRB jika relevan. | Review analisis area pada sistem existing untuk diadaptasi. |
| 23 | Man Power Planning | MPP berkaitan dengan jumlah SDM/teknisi/engineer. | Dashboard perlu menunjukkan jumlah manpower secara **All dan per branch**. | Buat summary/chart manpower per branch. |
| 24 | Engineer / Teknisi | Ada pembahasan terminologi SDM yang ditampilkan. | Gunakan istilah yang konsisten sesuai data, misalnya **Engineer/Teknisi**. | Konfirmasi naming final dengan stakeholder. |
| 25 | Modul PSB | Ada pembahasan PSB khususnya terkait teknisi dan perubahan flow. | Modul PSB masih dalam proses review/perubahan flow teknisi. | Lanjutkan review flow PSB. |
| 26 | Modul Lain | Disebutkan beberapa area seperti PSB, TSO, Dismantle, Distribusi. | Dashboard nantinya dapat memberikan insight/tren pada masing-masing modul. | Tentukan KPI dan chart utama per modul. |
| 27 | Review Stakeholder | Desain belum dibahas dengan Pak Samson. | Masukan dari Pak Samson perlu dikumpulkan sebelum finalisasi. | Review desain dengan Pak Samson lalu lakukan penyesuaian. |
| 28 | Fokus SPVR | Dashboard ditujukan agar SPVR mendapat pengetahuan kondisi area tanpa harus terlalu banyak melakukan filter. | Informasi utama harus langsung terbaca saat membuka dashboard. | Prioritaskan KPI summary, chart tren, dan komposisi. |
| 29 | Analisa Kinerja | Analisa kinerja yang tersedia saat ini tidak dapat langsung diakses dari mode/admin tertentu dan perlu masuk/login ke branch terlebih dahulu. | **Analisa Kinerja sebaiknya dapat diakses lebih langsung**, tanpa harus berpindah login ke branch secara manual. | Integrasikan akses Analisa Kinerja dengan konsep **Mode All / Mode Branch**. |
| 30 | Analisa Kinerja per Branch | Saat berada di mode admin/all, kebutuhan analisa branch tetap ada tetapi aksesnya kurang praktis. | Ketika user memilih **Mode Branch**, halaman Analisa Kinerja otomatis menampilkan data branch tersebut. | Hubungkan mode yang aktif dengan scope data Analisa Kinerja. |
| 31 | Referensi IRP/IRB | Beberapa fitur atau analisa disebut sudah tersedia di sistem sebelumnya. | Tidak perlu membuat ulang seluruh fitur apabila analisa yang sudah ada memang mencukupi. | Review fitur Analisa Kinerja yang sudah tersedia di IRP/IRB dan pilih bagian yang relevan untuk diadopsi. |
| 32 | Simplifikasi Dashboard | Ada kecenderungan agar dashboard tidak diisi terlalu banyak informasi atau fitur yang tidak terlalu dibutuhkan. | Fokus hanya pada **informasi yang benar-benar berguna untuk monitoring SPVR**, bukan menyalin semua informasi dari sistem lama. | Kurasi KPI, chart, dan analisa sebelum dimasukkan ke dashboard baru. |
| 33 | Staging vs Existing Feature | Disebutkan agar tidak sekadar mengambil seluruh tampilan/fitur staging. | Gunakan fitur atau komponen yang sudah paling matang/relevan sebagai referensi. | Bandingkan staging dengan versi existing/production sebelum menentukan desain final. |
| 34 | Konsistensi Data Terbaru | Ada pembahasan mengenai informasi/data terbaru yang sudah muncul di sistem sebelumnya. | Dashboard baru harus menggunakan **data paling aktual** dan sinkron dengan sumber data utama. | Pastikan sumber data dan refresh data konsisten antara aplikasi baru dan sistem existing. |
| 35 | Scope Lokal / Nasional | Dalam percakapan muncul kebutuhan membedakan konteks informasi lokal dan nasional. | Scope data harus jelas: apakah data merupakan **branch/lokal, regional, atau keseluruhan/nasional**. | Tambahkan definisi scope pada mode/filter dan label dashboard agar tidak ambigu. |
| 36 | Struktur Organisasi / Cabang | Ada pembahasan mengenai penggunaan istilah cabang/regional dan cakupan wilayah. | Naming organisasi perlu konsisten agar user memahami apakah suatu data mengacu pada **branch, regional, atau area**. | Standardisasi terminology Branch, Regional, Area, dan All pada UI dan dokumentasi. |
| 37 | Akses Berdasarkan Role | Keterbatasan akses Analisa Kinerja menunjukkan bahwa hak akses masih terkait akun/role tertentu. | Mode tampilan tidak boleh mengabaikan **hak akses user**, tetapi navigasinya perlu dibuat lebih praktis. | Terapkan role-based access sekaligus scope branch yang dinaungi user. |
| 38 | Operasional Sistem | Disebutkan bahwa sistem akan mengalami perubahan operasional. | Desain dashboard perlu cukup fleksibel untuk menyesuaikan perubahan proses operasional ke depan. | Hindari desain yang terlalu hard-coded terhadap struktur/proses saat ini. |
| 39 | Growth Area | Perlu diketahui bagaimana suatu area dikategorikan mulai tumbuh, berkembang, sampai masuk fase retention berdasarkan umur area sejak tanggal open. | Tambahkan analisa **Growth Area / Lifecycle Area** berdasarkan tanggal pembukaan area. | Definisikan fase area: New/Start → Growth → Mature/Retention. |
| 40 | Target Growth Area | Belum ada standar ideal pertumbuhan suatu area per bulan dan kapan area dapat dianggap mencapai goal. | Perlu menentukan **benchmark pertumbuhan ideal per bulan** untuk tiap area. | Tentukan target customer/growth berdasarkan umur area. |
| 41 | Growth Customer Area | Dari suatu area dibuka sampai bulan berjalan perlu terlihat pertumbuhan jumlah customer-nya. | Tambahkan grafik **Growth Customer per Area** secara bulanan. | X-axis = bulan/umur area, Y-axis = jumlah customer. |
| 42 | Trend Pembukaan Area | Pembukaan area perlu dibandingkan dengan kebijakan/target pembukaan area setiap bulan. Jika grafik datar atau terlambat berarti target tidak tercapai. | Tampilkan **actual vs target pembukaan area**. | Buat grafik kumulatif/monthly opening area dibanding target. |
| 43 | Primary / Overlay Growth | Tidak hanya total area, perkembangan jumlah overlay maupun primary perlu diketahui. | Growth Coverage Area perlu dapat dibedakan menjadi **Primary dan Overlay**. | Tambahkan series/filter Primary, Overlay, dan All. |
| 44 | Customer Active per Area | SPVR perlu mengetahui customer aktif yang terdapat pada masing-masing area setiap bulan. | Tampilkan jumlah dan tren **Customer Active per Area**. | Integrasikan dengan Growth Customer Area. |
| 45 | Status Customer | Fokus monitoring customer mengarah pada **Active, Isolir, dan Terminate**. | Dashboard sebaiknya menampilkan tren ketiga status tersebut, bukan hanya daftar customer. | Buat grafik tren Active vs Isolir vs Terminate. |
| 46 | Analisa Customer Isolir | Jumlah isolir dianggap penting karena dapat menunjukkan masalah dari proses sebelumnya, termasuk PSB, input, sistem, maupun follow-up. | **Isolir menjadi indikator early warning** bagi SPVR/Kepala Regional. | Tampilkan jumlah, tren, perubahan, dan area/branch dengan isolir tinggi. |
| 47 | Analisa Penyebab Isolir | SPVR diharapkan dapat menggunakan data isolir untuk berdiskusi dengan BL/PL mengenai apakah penyebabnya proses, sistem, atau human error. | Dashboard perlu membantu identifikasi **anomali/pola isolir**, tidak hanya menampilkan angka. | Sediakan breakdown penyebab apabila data tersedia. |
| 48 | Terminate / Churn | Terminate dipandang mirip dengan isolir sebagai indikator yang perlu ditekan. | Tambahkan **trend terminate/churn** sebagai indikator kesehatan customer. | Buat KPI Terminate Rate dan grafik trennya. |
| 49 | Early Warning | Ketika tren isolir atau terminate meningkat, SPVR seharusnya langsung aware dan melakukan komunikasi/tindak lanjut. | Dashboard perlu menonjolkan kondisi yang membutuhkan perhatian. | Tambahkan indikator kenaikan/anomali pada chart atau KPI. |
| 50 | FASUM | Ada kebutuhan membedakan customer normal dengan FASUM, termasuk perpindahan customer menjadi FASUM. | Tambahkan klasifikasi/summary **Customer vs FASUM** jika datanya sudah valid. | Validasi definisi serta sumber data FASUM. |
| 51 | Detail Teknis Customer | Detail teknis yang terlalu granular dinilai tidak selalu perlu sampai level SPVR. | Dashboard SPVR lebih fokus pada **analisa dan indikator**, bukan seluruh detail teknis. | Kurangi informasi teknis yang tidak menghasilkan action langsung. |
| 52 | Redaman / Quality Indicator | Informasi teknis seperti redaman disebut lebih relevan ketika dapat menunjukkan masalah kualitas atau kebutuhan refreshment tim. | Bila dimasukkan, tampilkan sebagai **indikator/summary**, bukan raw detail seluruh customer. | Tentukan KPI teknis yang benar-benar actionable bagi SPVR. |
| 53 | Sales Pipeline | SPVR perlu mengetahui jumlah customer pada tahapan seperti **Hot Prospect, Progress, Waiting Payment, dan Scheduling**. | Tambahkan monitoring **Sales Pipeline**. | Buat summary jumlah customer per stage. |
| 54 | Stuck / Aging Prospect | Customer yang terlalu lama berada di progress/waiting payment/scheduling harus dapat diketahui agar segera di-follow-up. | Dashboard perlu menunjukkan **pipeline yang mengendap**. | Tambahkan aging berdasarkan timestamp/status duration. |
| 55 | Follow-up Sales | Data pipeline digunakan SPVR untuk berkomunikasi dengan PL/BL jika prospect tidak segera ditindaklanjuti. | Informasi harus mendukung **action/follow-up**, bukan hanya monitoring. | Tandai prospect yang melewati SLA/umur ideal. |
| 56 | Detail Prospect | Selain total, disebutkan kebutuhan mengetahui customer/prospect mana yang berada pada status bermasalah. | Summary dapat dilengkapi **drill-down/list** ke customer terkait. | Dari chart/KPI arahkan ke daftar customer sesuai status. |
| 57 | Timestamp Pipeline | Timestamp penting untuk mengetahui berapa lama sebuah prospect berada dalam proses tertentu. | Simpan/tampilkan **waktu masuk stage dan aging**. | Tambahkan kolom timestamp atau duration pada detail pipeline. |
| 58 | PIC / Sumber Prospect | Untuk validasi diperlukan informasi asal data/prospect dan siapa sales/PIC terkait. | Detail pipeline perlu mempunyai informasi **PIC/Sales/Branch** jika tersedia. | Pastikan mapping user/sales/branch tersedia pada source data. |
| 59 | Analisa Kinerja Sales | Analisa performa existing dianggap perlu dibawa ke sistem/dashboard user. | Prioritaskan migrasi **analisa kinerja/performance** yang sudah berguna daripada membuat analisa baru dari nol. | Adopsi analisa existing terlebih dahulu kemudian tambahkan add-on. |
| 60 | Centralized Performance | Perkembangan proses di masing-masing ERP/branch diharapkan dapat dikolektifkan menjadi satu tampilan. | Dashboard user menjadi **central monitoring** lintas branch/proses sesuai kewenangan. | Integrasikan data masing-masing branch ke tampilan All/Branch Mode. |
| 61 | Dismantle / Asset Retrieval | Ada kondisi aset/modem dengan status sukses terambil, gagal terambil, dan masih progress. | Tambahkan analisa performa **pengambilan aset/modem**. | Buat KPI Success, Failed, dan In Progress. |
| 62 | Bottleneck Asset | Banyak aset yang masih dalam status progress perlu diketahui penyebabnya agar segera menjadi success/failed. | Fokus analisa pada **bottleneck proses pengambilan modem**. | Tambahkan aging dan alasan kegagalan/progress jika tersedia. |
| 63 | Schedule Pengambilan Aset | Setelah dijadwalkan, masih terdapat aktivitas yang belum dilaksanakan. | Dashboard perlu menunjukkan **schedule vs execution** pengambilan aset. | Buat indikator Scheduled, Completed, Overdue. |
| 64 | Ownership / Action | Beberapa kondisi membutuhkan action dari BL/BM/AE, bukan hanya diketahui oleh SPVR. | Analisa harus memperjelas **siapa yang perlu melakukan action** terhadap case bermasalah. | Tambahkan PIC/owner pada drill-down case. |
| 65 | Analisa vs Raw Data | Arah dashboard disebut lebih banyak berisi analisa daripada data mentah. | Dashboard SPVR dibuat **analysis-first**, bukan table-first. | Prioritaskan KPI, chart, alert, dan exception monitoring. |
| 66 | Real Case Drill-down | Walaupun dashboard fokus analisa, beberapa kasus nyata tetap perlu dapat dibuka untuk tindak lanjut. | Gunakan konsep **summary → analysis → drill-down case**. | Chart/KPI dapat diklik menuju data detail terkait. |
| 67 | Monitoring Infrastruktur | Monitoring infrastruktur disebut sebagai salah satu area yang tetap perlu diperbarui. | Modul monitoring infrastruktur tetap masuk ruang lingkup dashboard. | Review KPI infrastruktur yang relevan untuk SPVR. |
| 68 | Implementasi Aset | Implementasi/pengelolaan aset juga disebut sebagai bagian yang perlu diperbarui. | Tambahkan monitoring implementasi/aset yang berorientasi progress dan exception. | Tentukan status utama dan bottleneck yang perlu ditampilkan. |

## Ringkasan Keputusan Utama

| Area | Keputusan |
|---|---|
| **Mode Dashboard** | Tersedia **Mode All** dan **Mode per Branch** sesuai branch yang dinaungi user. |
| **Filter** | Filter tetap tersedia untuk fleksibilitas, terutama pada Mode All. |
| **Navigasi** | Selector mode ditempatkan di **sidebar** agar perpindahan konteks cepat. |
| **Hak Akses** | Data tetap mengikuti role serta branch yang menjadi kewenangan user. |
| **Analisa Kinerja** | Dapat diakses berdasarkan mode aktif tanpa perlu logout/login ulang ke branch. |
| **Visualisasi** | Dashboard lebih fokus pada **chart, KPI, trend, dan insight** daripada tabel mentah. |
| **Coverage Area** | Menampilkan Primary, Overlay, total area, proporsi, pertumbuhan, dan lifecycle area. |
| **Customer** | Menampilkan Active, Isolir, Terminate serta Growth Customer per Area. |
| **Man Power Planning** | Menampilkan jumlah Engineer/Teknisi/Manpower secara All maupun per Branch. |
| **Sales Pipeline** | Menampilkan Hot Prospect, Progress, Waiting Payment, Scheduling, aging, dan stuck case. |
| **Dismantle / Asset** | Menampilkan success, failed, progress, overdue, dan bottleneck pengambilan aset/modem. |
| **Referensi Existing** | Fitur existing di IRP/IRB/Superset yang sudah relevan diadopsi terlebih dahulu. |
| **Scope Data** | Harus jelas apakah data berada pada level All, Regional, Branch, atau Area. |
| **Data Terbaru** | Dashboard harus menggunakan data aktual dan konsisten dengan sumber data utama. |
| **Prinsip Desain** | Simple, informatif, fleksibel, analysis-first, dan mendukung action/follow-up. |

## Struktur Dashboard yang Disarankan

| Layer Dashboard | Isi |
|---|---|
| **1. Executive Summary** | KPI utama All/Branch: Customer, Coverage Area, Manpower, Sales Pipeline, Isolir, Terminate, Aset |
| **2. Growth & Trend** | Growth Area, Growth Customer, pembukaan Primary/Overlay, Active/Isolir/Terminate |
| **3. Performance Analysis** | Analisa kinerja Sales, PSB/proses operasional, Dismantle, Asset Retrieval |
| **4. Bottleneck / Early Warning** | Prospect mengendap, isolir meningkat, terminate meningkat, area tidak mencapai target, pengambilan modem overdue |
| **5. Drill-down** | Customer/prospect/area/aset yang menyebabkan indikator bermasalah |
| **6. Action Context** | Branch, PIC/BL/PL/AE terkait, umur case, timestamp, dan status terakhir |

## Prinsip Utama Dashboard SPVR

Dashboard diarahkan bukan hanya untuk **melihat data**, tetapi untuk membantu SPVR:

- mengetahui **apa yang tumbuh**;
- mengetahui **apa yang tertinggal**;
- mendeteksi **apa yang bermasalah**;
- menemukan **bottleneck proses**;
- mengetahui **branch/area/PIC mana yang membutuhkan perhatian**;
- dan menentukan **tindak lanjut yang perlu dilakukan**.

Dengan demikian, pendekatan utama dashboard adalah:

**Summary → Analysis → Early Warning → Drill-down → Action**

