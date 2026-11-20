<!DOCTYPE html>
<html lang="id" class="dark">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>DRAMA STUDIO AI – Studio Pembuat Serial Drama</title>
  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Google Fonts: Playfair Display, Plus Jakarta Sans & JetBrains Mono -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500&family=Playfair+Display:ital,wght@0,600;0,700;0,800;1,600&family=Plus+Jakarta+Sans:wght@400;500;600;700&display=swap" rel="stylesheet">
  <!-- Lucide Icons -->
  <script src="https://unpkg.com/lucide@latest"></script>

  <script>
    tailwind.config = {
      darkMode: 'class',
      theme: {
        extend: {
          fontFamily: {
            sans: ['"Plus Jakarta Sans"', 'sans-serif'],
            serif: ['"Playfair Display"', 'serif'],
            mono: ['"JetBrains Mono"', 'monospace'],
          },
          colors: {
            studio: {
              950: '#070A12',
              900: '#0D121F',
              850: '#131A2C',
              800: '#1A233A',
              700: '#273454',
            }
          }
        }
      }
    }
  </script>

  <style>
    /* Custom Scrollbar */
    ::-webkit-scrollbar {
      width: 6px;
      height: 6px;
    }
    ::-webkit-scrollbar-track {
      background: rgba(15, 23, 42, 0.2);
    }
    ::-webkit-scrollbar-thumb {
      background: rgba(245, 158, 11, 0.35);
      border-radius: 9999px;
    }
    ::-webkit-scrollbar-thumb:hover {
      background: rgba(245, 158, 11, 0.6);
    }

    /* Subtle animations */
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(8px); }
      to { opacity: 1; transform: translateY(0); }
    }
    .animate-fade-in {
      animation: fadeIn 0.35s ease-out forwards;
    }

    @keyframes pulseGlow {
      0%, 100% { box-shadow: 0 0 20px rgba(245, 158, 11, 0.15); }
      50% { box-shadow: 0 0 35px rgba(245, 158, 11, 0.35); }
    }
    .studio-glow {
      animation: pulseGlow 3.5s infinite ease-in-out;
    }

    /* Hide scrollbar for horizontal pill nav on mobile */
    .no-scrollbar::-webkit-scrollbar {
      display: none;
    }
    .no-scrollbar {
      -ms-overflow-style: none;
      scrollbar-width: none;
    }
  </style>
</head>
<body class="bg-slate-50 text-slate-900 dark:bg-studio-950 dark:text-slate-100 font-sans antialiased selection:bg-amber-500/30 selection:text-amber-300 min-h-screen flex flex-col">

  <!-- ===================================================================== -->
  <!-- TOP HEADER BAR                                                        -->
  <!-- ===================================================================== -->
  <header class="sticky top-0 z-40 backdrop-blur-xl bg-white/85 dark:bg-studio-900/85 border-b border-slate-200 dark:border-slate-800/80">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 h-16 flex items-center justify-between gap-3">
      <!-- Brand Logo -->
      <button onclick="navigateTo('dashboard')" class="flex items-center gap-3 text-left group focus:outline-none">
        <div class="w-10 h-10 rounded-xl bg-gradient-to-br from-amber-400 via-amber-500 to-orange-600 p-0.5 shadow-lg shadow-amber-500/20 group-hover:scale-105 transition-transform">
          <div class="w-full h-full bg-studio-950 rounded-[10px] flex items-center justify-center">
            <!-- Custom SVG Film Clapper + AI Spark Logo -->
            <svg class="w-6 h-6 text-amber-400" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8">
              <path d="M4 11v8a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2v-8H4Z" />
              <path d="m4 11-.88-2.87a2 2 0 0 1 1.33-2.5l11.48-3.5a2 2 0 0 1 2.5 1.32l.87 2.87L4 11Z" />
              <path d="m6.6 4.99 3.38 4.2" />
              <path d="m11.86 3.38 3.38 4.2" />
              <path d="M12 14l.6 1.4 1.4.6-1.4.6-.6 1.4-.6-1.4-1.4-.6 1.4-.6.6-1.4z" fill="currentColor" stroke="none"/>
            </svg>
          </div>
        </div>
        <div>
          <div class="flex items-center gap-2">
            <span class="font-serif font-bold text-base sm:text-lg tracking-wide bg-gradient-to-r from-amber-500 to-orange-500 dark:from-amber-300 dark:to-amber-500 bg-clip-text text-transparent">
              DRAMA STUDIO AI
            </span>
            <span class="hidden sm:inline-block text-[10px] font-semibold uppercase tracking-widest px-2 py-0.5 rounded-full bg-amber-500/15 text-amber-600 dark:text-amber-300 border border-amber-500/30">
              Pro Studio
            </span>
          </div>
          <p class="text-[11px] text-slate-500 dark:text-slate-400 hidden sm:block">Studio Pembuat Serial Drama Otomatis</p>
        </div>
      </button>

      <!-- Active Project Pill & Actions -->
      <div class="flex items-center gap-2 sm:gap-3">
        <!-- Active Project Indicator -->
        <div id="active-project-badge" class="hidden md:flex items-center gap-2 px-3 py-1.5 rounded-xl bg-slate-100 dark:bg-studio-800 border border-slate-200 dark:border-slate-700/80 text-xs">
          <span class="w-2 h-2 rounded-full bg-emerald-400 animate-pulse"></span>
          <span class="text-slate-500 dark:text-slate-400">Proyek Aktif:</span>
          <span id="header-project-title" class="font-semibold text-slate-800 dark:text-amber-300 max-w-[180px] truncate">Senja di Pelabuhan Sunda</span>
        </div>

        <!-- User Guide Quick Button -->
        <button onclick="openUserGuideModal()" title="Petunjuk Penggunaan & Langkah-Langkah" class="flex items-center gap-1.5 px-3 py-2 rounded-xl bg-slate-100 hover:bg-slate-200 dark:bg-studio-800 dark:hover:bg-studio-700 text-slate-700 dark:text-amber-300 border border-slate-200 dark:border-slate-700 font-semibold text-xs sm:text-sm transition-colors">
          <i data-lucide="help-circle" class="w-4 h-4"></i>
          <span class="hidden sm:inline">Panduan</span>
        </button>

        <!-- New Drama Quick Button -->
        <button onclick="openNewProjectModal()" class="flex items-center gap-1.5 px-3 py-2 rounded-xl bg-amber-500 hover:bg-amber-400 text-slate-950 font-semibold text-xs sm:text-sm transition-all shadow-md shadow-amber-500/20">
          <i data-lucide="plus" class="w-4 h-4"></i>
          <span class="hidden sm:inline">Drama Baru</span>
        </button>

        <!-- Export Project Button -->
        <button onclick="openExportModal()" title="Ekspor Serial Drama" class="p-2.5 rounded-xl bg-slate-100 hover:bg-slate-200 dark:bg-studio-800 dark:hover:bg-studio-700 text-slate-700 dark:text-slate-200 border border-slate-200 dark:border-slate-700 transition-colors">
          <i data-lucide="download" class="w-4 h-4"></i>
        </button>

        <!-- Theme Toggle -->
        <button onclick="toggleTheme()" title="Ubah Tema Terang/Gelap" class="p-2.5 rounded-xl bg-slate-100 hover:bg-slate-200 dark:bg-studio-800 dark:hover:bg-studio-700 text-slate-700 dark:text-slate-200 border border-slate-200 dark:border-slate-700 transition-colors">
          <i id="theme-icon" data-lucide="sun" class="w-4 h-4"></i>
        </button>
      </div>
    </div>

    <!-- Studio Workflow Navigation Tabs -->
    <nav class="bg-slate-100/80 dark:bg-studio-950/90 border-t border-slate-200/80 dark:border-slate-800/80">
      <div class="max-w-7xl mx-auto px-3 sm:px-6 flex items-center gap-1.5 overflow-x-auto no-scrollbar py-2" id="main-nav-tabs">
        <!-- Rendered dynamically by JS -->
      </div>
    </nav>
  </header>

  <!-- ===================================================================== -->
  <!-- MAIN CONTENT WORKSPACE                                                -->
  <!-- ===================================================================== -->
  <main id="app-content" class="flex-1 max-w-7xl w-full mx-auto px-4 sm:px-6 py-6 sm:py-8">
    <!-- Dynamic Views Injected Here -->
  </main>

  <!-- ===================================================================== -->
  <!-- FOOTER                                                                -->
  <!-- ===================================================================== -->
  <footer class="border-t border-slate-200 dark:border-slate-800/80 bg-white/50 dark:bg-studio-900/50 py-5 mt-12">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 flex flex-col sm:flex-row items-center justify-between gap-3 text-xs text-slate-500 dark:text-slate-400">
      <div class="flex items-center gap-2">
        <span class="font-serif font-bold text-amber-500">DRAMA STUDIO AI</span>
        <span>•</span>
        <span>Studio Kreatif Pembuat Serial Drama & Naskah Sinematik</span>
      </div>
      <div>
        <span>Gunakan ikon Unduh di atas untuk mengekspor naskah & cadangan proyek Anda.</span>
      </div>
    </div>
  </footer>

  <!-- ===================================================================== -->
  <!-- GLOBAL MODALS & TOAST NOTIFICATIONS                                   -->
  <!-- ===================================================================== -->

  <!-- Toast Container -->
  <div id="toast-container" class="fixed bottom-5 right-5 z-50 flex flex-col gap-2.5 max-w-sm w-full pointer-events-none px-4 sm:px-0"></div>

  <!-- Fullscreen AI Loading Overlay -->
  <div id="ai-loading-overlay" class="fixed inset-0 z-50 hidden items-center justify-center bg-slate-950/80 backdrop-blur-md p-4">
    <div class="bg-white dark:bg-studio-900 border border-amber-500/30 rounded-3xl p-6 sm:p-8 max-w-md w-full text-center shadow-2xl studio-glow">
      <div class="relative w-16 h-16 mx-auto mb-5">
        <div class="absolute inset-0 rounded-full border-4 border-amber-500/20"></div>
        <div class="absolute inset-0 rounded-full border-4 border-amber-500 border-t-transparent animate-spin"></div>
        <div class="absolute inset-0 flex items-center justify-center text-amber-500">
          <i data-lucide="sparkles" class="w-6 h-6"></i>
        </div>
      </div>
      <h3 id="loading-title" class="font-serif font-bold text-xl text-slate-900 dark:text-white mb-2">Meracik Cerita Drama...</h3>
      <p id="loading-subtitle" class="text-sm text-slate-600 dark:text-slate-300 leading-relaxed">AI Sutradara & Penulis Skenario sedang bekerja menyusun detail dramatis untuk serial Anda.</p>
    </div>
  </div>

  <!-- Custom Modal Container -->
  <div id="custom-modal-backdrop" onclick="if(event.target === this) closeModal()" class="fixed inset-0 z-50 hidden items-center justify-center bg-slate-950/75 backdrop-blur-sm p-4 overflow-y-auto">
    <div id="custom-modal-box" class="bg-white dark:bg-studio-900 border border-slate-200 dark:border-slate-700 rounded-3xl max-w-2xl w-full p-6 shadow-2xl my-auto animate-fade-in">
      <!-- Modal content injected dynamically -->
    </div>
  </div>

  <!-- ===================================================================== -->
  <!-- JAVASCRIPT APPLICATION LOGIC                                          -->
  <!-- ===================================================================== -->
  <script>
    /**
     * =========================================================================
     * 1. KONFIGURASI API & DATA REFERENSI STUDIO
     * =========================================================================
     */
    const apiKey = ""; // Disediakan otomatis oleh environment saat runtime

    // Daftar 15 Genre Utama + Kartu Visual
    const GENRE_LIST = [
      { id: 'keluarga', name: 'Drama keluarga', desc: 'Konflik hangat, pengorbanan orang tua, rahasia warisan, dan ikatan darah.', gradient: 'from-amber-600 to-orange-800', icon: 'home' },
      { id: 'percintaan', name: 'Drama percintaan', desc: 'Kisah cinta penuh rintangan, pertemuan takdir, dan dilema perasaan.', gradient: 'from-rose-600 to-pink-800', icon: 'heart' },
      { id: 'persahabatan', name: 'Drama persahabatan', desc: 'Kesetiaan, pengkhianatan, dan perjalanan tumbuh dewasa bersama sahabat.', gradient: 'from-sky-600 to-indigo-800', icon: 'users' },
      { id: 'guru', name: 'Drama kehidupan guru', desc: 'Dedikasi pendidik di pelosok maupun kota dalam mengubah masa depan murid.', gradient: 'from-emerald-600 to-teal-800', icon: 'book-open' },
      { id: 'masyarakat', name: 'Drama kehidupan masyarakat', desc: 'Potret nyata dinamika warga, gotong royong, dan persoalan sehari-hari.', gradient: 'from-orange-600 to-amber-800', icon: 'globe' },
      { id: 'pendidikan', name: 'Drama pendidikan', desc: 'Perjuangan meraih mimpi di bangku sekolah atau kampus penuh tantangan.', gradient: 'from-blue-600 to-cyan-800', icon: 'graduation-cap' },
      { id: 'perjuangan', name: 'Drama perjuangan hidup', desc: 'Bangkit dari keterpurukan ekonomi dan kerasnya realita demi martabat.', gradient: 'from-yellow-600 to-amber-900', icon: 'flame' },
      { id: 'komedi', name: 'Drama komedi', desc: 'Situasi kocak penuh kehangatan yang menyentuh hati sekaligus mengundang tawa.', gradient: 'from-lime-600 to-emerald-800', icon: 'smile' },
      { id: 'religi', name: 'Drama religi dan inspirasi', desc: 'Pencarian makna spiritual, keikhlasan, taubat, dan keteguhan iman.', gradient: 'from-teal-600 to-emerald-900', icon: 'sun' },
      { id: 'misteri', name: 'Drama misteri', desc: 'Teka-teki masa lalu, hilangnya seseorang, dan petunjuk penuh ketegangan.', gradient: 'from-violet-700 to-slate-900', icon: 'search' },
      { id: 'sejarah', name: 'Drama sejarah', desc: 'Kisah heroik dan kemanusiaan di tengah peristiwa penting masa lampau.', gradient: 'from-stone-600 to-amber-950', icon: 'landmark' },
      { id: 'horor', name: 'Drama horor', desc: 'Teror supranatural yang berakar pada kutukan keluarga dan rahasia kelam.', gradient: 'from-red-900 to-slate-950', icon: 'ghost' },
      { id: 'kerajaan', name: 'Drama kerajaan', desc: 'Intrik takhta, kesetiaan panglima, dan cinta terlarang di balik istana.', gradient: 'from-purple-700 to-amber-900', icon: 'crown' },
      { id: 'desa', name: 'Drama kehidupan desa', desc: 'Kearifan lokal, tradisi adat, dan ketenangan desa yang diuji perubahan zaman.', gradient: 'from-green-700 to-emerald-950', icon: 'trees' },
      { id: 'sosial', name: 'Drama sosial dan konflik masyarakat', desc: 'Ketimpangan keadilan, suara rakyat kecil, dan benturan kepentingan.', gradient: 'from-slate-700 to-zinc-900', icon: 'scale' }
    ];

    // Pilihan Gaya Visual untuk Generator Gambar AI
    const VISUAL_STYLES = [
      { id: 'film_realistis', name: 'Realistis seperti film layar lebar', prompt: 'Photorealistic live-action cinema still, shot on 35mm anamorphic lens, dramatic natural lighting, shallow depth of field, movie color grading, ultra-detailed skin texture, authentic Indonesian cinema aesthetic' },
      { id: 'sinematik_kdrama', name: 'Sinematik Drama Asia / K-Drama', prompt: 'High-budget cinematic Asian drama photography, warm emotional golden hour lighting, soft lens flare, crisp 8k resolution, expressive film look' },
      { id: 'anime_modern', name: 'Ilustrasi Anime & Webtoon Sinematik', prompt: 'High-end modern anime film key visual, detailed cel-shading, atmospheric volumetric lighting, Makoto Shinkai inspired sky and background details' },
      { id: 'lukisan_klasik', name: 'Lukisan Klasik & Artistik', prompt: 'Masterpiece dramatic oil painting on canvas, rich chiaroscuro lighting, expressive brushwork, museum-grade classical storytelling art' },
      { id: 'noir_dramatis', name: 'Noir & Dramatis Kontras Tinggi', prompt: 'Moody neo-noir cinematography, high contrast shadows, rain reflections, atmospheric fog, deep dramatic tension' },
      { id: 'cat_air', name: 'Cat Air Lembut & Puitis', prompt: 'Poetic watercolor and gouache illustration, warm nostalgic palette, delicate ink linework, emotional storybook atmosphere' }
    ];

    // Navigasi Tab Utama
    const NAV_TABS = [
      { id: 'dashboard', label: 'Halaman Utama', icon: 'layout-dashboard' },
      { id: 'setup', label: '1. Genre & Cerita', icon: 'clapperboard' },
      { id: 'characters', label: '2. Karakter', icon: 'users' },
      { id: 'plot', label: '3. Alur Serial', icon: 'git-branch' },
      { id: 'script', label: '4. Naskah Episode', icon: 'file-text' },
      { id: 'visuals', label: '5. Studio Visual AI', icon: 'image' }
    ];

    /**
     * =========================================================================
     * 2. STATE APLIKASI & DATA CONTOH BAWAAN
     * =========================================================================
     */
    function createSampleProject() {
      return {
        id: 'proj_sunda_01',
        updatedAt: new Date().toISOString(),
        genre: 'Drama keluarga',
        customGenre: '',
        settings: {
          title: 'Senja di Pelabuhan Sunda',
          theme: 'Pengorbanan, Rahasia Masa Lalu, dan Rekonsiliasi Keluarga Nelayan',
          synopsis: 'Setelah 12 tahun merantau menjadi arsitek kapal di luar negeri, Arka pulang ke pelabuhan tua tempat ia dibesarkan setelah ayahnya, Pak Darmawan, jatuh sakit. Kepulangan Arka justru membuka rahasia besar tentang tenggelamnya kapal layar warisan keluarga dan hutang budi yang memisahkan ia dengan adiknya, Sekar.',
          settingPlace: 'Pelabuhan Tua Sunda Kelapa & Kampung Pesisir Utara Jakarta',
          era: 'Masa Kini (2026)',
          mood: 'Hangat, Melankolis & Penuh Ketegangan Emosional',
          audience: 'Semua Umur / Keluarga',
          episodeCount: 5,
          episodeDuration: '45 Menit (Standar TV/Streaming)',
          narrativeStyle: 'Alur Maju dengan Kilas Balik Emosional',
          moralMessage: 'Sejauh apa pun ombak membawa kita pergi, keluarga adalah dermaga tempat hati selalu pulang dan saling memaafkan.'
        },
        characters: [
          {
            id: 'char_1',
            name: 'Arka Wijaya',
            age: '31 Tahun',
            gender: 'Laki-laki',
            role: 'Protagonis Utama',
            personality: 'Perfeksionis, pendiam, memendam rasa bersalah, namun sangat penyayang dan bertanggung jawab.',
            background: 'Anak sulung yang meninggalkan rumah 12 tahun lalu demi mengejar beasiswa teknik perkapalan dan membuktikan diri.',
            relationships: 'Anak kandung Pak Darmawan; kakak kandung Sekar yang sempat renggang; mantan kekasih Laras.',
            physicalTraits: 'Wajah tegas khas pria pesisir Indonesia, kulit sawo matang, rambut hitam bergelombang sedikit berantakan, tatapan mata tajam penuh beban.',
            clothingStyle: 'Kemeja linen biru dongker lengan digulung, celana chino krem, jam tangan kulit cokelat tua.',
            imageUrl: ''
          },
          {
            id: 'char_2',
            name: 'Pak Darmawan',
            age: '62 Tahun',
            gender: 'Laki-laki',
            role: 'Tokoh Sentral / Ayah',
            personality: 'Keras kepala, berwibawa, bijaksana dalam diam, menjunjung tinggi harga diri pelaut.',
            background: 'Pembuat kapal pinisi legendaris yang menolak menjual galangan kapalnya kepada pengembang pelabuhan modern.',
            relationships: 'Ayah dari Arka dan Sekar; sahabat lama almarhum ayah Laras.',
            physicalTraits: 'Wajah berkerut bijaksana dengan kumis dan janggut tipis memutih, postur tegap meski mulai menua, mata teduh.',
            clothingStyle: 'Kaos kerah katun abu-abu pudar, rompi kerja kanvas cokelat, dan sarung tenun sederhana saat di rumah.',
            imageUrl: ''
          },
          {
            id: 'char_3',
            name: 'Sekar Ayu',
            age: '25 Tahun',
            gender: 'Perempuan',
            role: 'Deuteragonis / Adik',
            personality: 'Tangguh, blak-blakan, setia merawat ayah, menyimpan luka karena merasa ditinggalkan kakaknya.',
            background: 'Mengelola pembukuan galangan kapal kecil milik ayahnya sambil membuka kedai kopi sederhana di tepi dermaga.',
            relationships: 'Adik kandung Arka; putri kesayangan Pak Darmawan; sahabat dekat Laras.',
            physicalTraits: 'Wajah oval manis dengan lesung pipi, kulit kuning langsat hangat, rambut hitam panjang diikat ekor kuda rendah.',
            clothingStyle: 'Blus katun motif lurik modern warna terakota, celemek kanvas saat bekerja, celana kulot hitam.',
            imageUrl: ''
          }
        ],
        storyArc: {
          storyIdea: 'Kepulangan seorang arsitek kapal ke galangan tua ayahnya memicu konflik warisan, pengambilalihan lahan pesisir, dan terungkapnya misteri tragedi laut 12 tahun silam.',
          fullSynopsis: 'Arka Wijaya kembali ke pelabuhan tua setelah menerima kabar kondisi jantung ayahnya, Pak Darmawan, melemah. Namun kepulangannya disambut dingin oleh adiknya, Sekar, yang merasa berjuang sendirian merawat ayah mereka. Di saat bersamaan, perusahaan konglomerat maritim menekan Pak Darmawan untuk menyerahkan sertifikat tanah galangan kapal karena sebuah surat perjanjian lama yang ditandatangani saat tragedi tenggelamnya kapal Phinisi Nusantara 12 tahun lalu. Arka dan Sekar harus mengesampingkan ego mereka untuk menyelamatkan warisan keluarga sekaligus menyembuhkan luka masa lalu.',
          mainConflict: 'Upaya mempertahankan galangan kapal keluarga dari ancaman penyitaan akibat perjanjian lama, di tengah retaknya kepercayaan antara Arka, Sekar, dan Pak Darmawan.',
          subConflicts: 'Dilema cinta lama antara Arka dan Laras yang kini bekerja sebagai pengacara perusahaan pengembang; rahasia penyebab sebenarnya tenggelamnya kapal 12 tahun lalu.',
          climax: 'Malam badai di dermaga saat dokumen asli perjanjian ditemukan di dalam lambung kapal tua yang sedang direstorasi, tepat sebelum eksekusi lahan dilakukan keesokan paginya.',
          plotTwist: 'Pak Darmawan sengaja menyuruh Arka pergi 12 tahun lalu bukan karena mengusirnya, melainkan untuk melindungi Arka dari tuduhan kelalaian pelayaran yang sebenarnya dilakukan oleh rekan bisnis ayah mereka.',
          resolution: 'Galangan kapal berhasil diselamatkan menjadi pusat edukasi maritim tradisional, dan keluarga Pak Darmawan kembali utuh menyambut matahari terbit di dermaga.',
          characterDynamics: 'Arka dan Sekar bergerak dari saling menyalahkan menjadi rekan seperjuangan; Pak Darmawan belajar melepaskan beban rahasianya kepada anak-anaknya.',
          episodes: [
            {
              episodeNumber: 1,
              title: 'Kepulangan yang Terlambat',
              summary: 'Arka tiba di pelabuhan saat senja, mendapati ayahnya dirawat dan adiknya bersikap dingin. Surat peringatan penyitaan galangan kapal datang tanpa diduga.',
              connectionToMainArc: 'Memperkenalkan seluruh tokoh utama, luka lama kepergian Arka 12 tahun lalu, serta pemicu konflik utama berupa surat sengketa galangan kapal.',
              cliffhanger: 'Arka menemukan foto lama ayahnya bersama direktur perusahaan pengembang di laci meja kerja Pak Darmawan.'
            },
            {
              episodeNumber: 2,
              title: 'Jejak di Lambung Kapal',
              summary: 'Arka mulai memeriksa kondisi galangan dan bertemu kembali dengan Laras. Sekar mengungkapkan kemarahannya atas bertahun-tahun tanpa kabar dari Arka.',
              connectionToMainArc: 'Memperdalam konflik antara Arka dan Sekar sekaligus membuka subplot hubungan Arka-Laras yang berada di pihak berseberangan.',
              cliffhanger: 'Seorang pekerja tua galangan membisikkan bahwa kapal Phinisi Nusantara tidak tenggelam karena cuaca buruk.'
            },
            {
              episodeNumber: 3,
              title: 'Surat dari Masa Lalu',
              summary: 'Penyelidikan Arka dan Sekar mengarah pada kotak kayu terkunci di gudang layar. Kondisi kesehatan Pak Darmawan kembali menurun saat rahasia mulai terkuak.',
              connectionToMainArc: 'Menghubungkan misteri tragedi 12 tahun lalu dengan alasan kenapa sertifikat galangan tergadaikan.',
              cliffhanger: 'Laras datang membawa berkas pembatalan sepihak dan memperingatkan Arka bahwa ayahnya bisa dipidanakan.'
            },
            {
              episodeNumber: 4,
              title: 'Badai di Dermaga Tua',
              summary: 'Terungkapnya pengorbanan Pak Darmawan selama 12 tahun demi melindungi masa depan Arka. Badai besar menghantam kapal yang tengah diperbaiki.',
              connectionToMainArc: 'Menjadi titik balik emosional (Plot Twist) yang menyatukan kembali keluarga sebelum klimaks.',
              cliffhanger: 'Di tengah hujan deras, Arka menyelam ke ruang mesin kapal tua untuk menyelamatkan bukti terakhir sebelum tenggelam.'
            },
            {
              episodeNumber: 5,
              title: 'Fajar di Ujung Laut',
              summary: 'Dengan bukti asli di tangan dan dukungan warga pesisir, Arka dan Sekar menghadapi sidang mediasi terakhir. Pak Darmawan akhirnya berdamai dengan masa lalunya.',
              connectionToMainArc: 'Menyelesaikan seluruh konflik utama, konflik tambahan, serta mewujudkan pesan moral tentang keluarga.',
              cliffhanger: 'Epilog hangat: Peluncuran kapal baru karya bersama Pak Darmawan, Arka, dan Sekar menyongsong fajar.'
            }
          ]
        },
        scripts: {
          1: {
            episodeNumber: 1,
            title: 'Kepulangan yang Terlambat',
            summary: 'Setelah 12 tahun merantau, Arka kembali ke pelabuhan tua dengan membawa penyesalan. Namun kepulangannya langsung disambut dingin oleh Sekar dan ancaman penyitaan galangan kapal keluarga.',
            openingHook: 'Suara deburan ombak senja berpadu dengan ketukan palu kayu di galangan kapal tua. Kamera menyorot tangan berkerut Pak Darmawan yang gemetar memegang pahat kayu sebelum ia jatuh terduduk memegangi dadanya.',
            scenes: [
              {
                sceneNumber: 1,
                heading: 'INT. GALANGAN KAPAL TUA - SENJA',
                locationDesc: 'Bangunan kayu luas beratap seng tinggi di tepi dermaga. Kerangka kapal pinisi raksasa berdiri megah diterangi cahaya matahari terbenam yang masuk dari celah dinding papan.',
                charactersPresent: ['Pak Darmawan', 'Sekar Ayu'],
                narration: 'Waktu seolah berhenti di galangan tua ini, namun tubuh Pak Darmawan tak lagi sekuat kayu jati yang selalu ia ukir.',
                dialogue: [
                  { character: 'Sekar Ayu', emotion: 'Panik & Cemas', line: 'Ayah! Sudah Sekar bilang jangan memaksakan diri memahat bagian haluan sendirian!' },
                  { character: 'Pak Darmawan', emotion: 'Menahan sakit, tetap tegar', line: 'Kapal ini harus selesai bulan depan, Kar... Ayah tidak mau mati meninggalkan janji yang belum lunas.' },
                  { character: 'Sekar Ayu', emotion: 'Mata berkaca-kaca', line: 'Ayah bicara apa sih? Kita ke klinik sekarang, titik!' }
                ],
                cameraDirection: 'Medium Close-Up pada wajah Pak Darmawan yang berkeringat dingin, lalu kamera bergerak cepat (handheld tracking) mengikuti Sekar yang berlari memapah ayahnya.',
                visualDesc: 'Siluet dua figur di depan lambung kapal kayu raksasa dengan debu kayu beterbangan terkena sinar oranye senja.',
                musicAmbience: 'Dentingan piano pelan dan suara angin laut pelabuhan.'
              },
              {
                sceneNumber: 2,
                heading: 'EXT. DERMAGA PELABUHAN SUNDA - MALAM',
                locationDesc: 'Dermaga batu basah dengan lampu-lampu kapal nelayan yang berkelip di kejauhan. Bau garam laut dan solar terasa kental.',
                charactersPresent: ['Arka Wijaya', 'Sekar Ayu'],
                narration: 'Dua belas tahun adalah waktu yang cukup untuk mengubah seorang anak muda menjadi asing di tanah kelahirannya sendiri.',
                dialogue: [
                  { character: 'Arka Wijaya', emotion: 'Ragu & Penuh Sesal', line: 'Sekar... bagaimana keadaan Ayah di dalam?' },
                  { character: 'Sekar Ayu', emotion: 'Dingin & Menahan Amarah', line: 'Baru ingat jalan pulang, Mas? Dua belas tahun Ayah masuk keluar klinik, ke mana saja kamu?' },
                  { character: 'Arka Wijaya', emotion: 'Suara bergetar', line: 'Mas kirim uang setiap bulan, Kar. Mas kira—' },
                  { character: 'Sekar Ayu', emotion: 'Tegas & Terluka', line: 'Ayah tidak butuh transferan uangmu! Ayah cuma ingin anaknya pulang sebelum semuanya terlambat!' }
                ],
                cameraDirection: 'Over-the-Shoulder shot bergantian antara wajah Arka yang tertunduk dan tatapan tajam Sekar, diakhiri Wide Shot yang memperlihatkan jarak fisik di antara keduanya.',
                visualDesc: 'Arka berdiri memegang koper kulit di bawah lampu jalan dermaga yang temaram, sementara Sekar berdiri di ambang pintu rumah kayu.',
                musicAmbience: 'Suara jangkrik malam pesisir dan gesekan biola bernada rendah.'
              }
            ],
            closingCliffhanger: 'Saat Sekar masuk merawat ayah mereka, Arka duduk di meja kerja tua Pak Darmawan. Sebuah amplop merah berstempel pengadilan jatuh dari balik buku catatan kapal—dan di dalamnya terselip foto lama Pak Darmawan berjabat tangan dengan direktur perusahaan pengembang pelabuhan.'
          }
        },
        gallery: [
          {
            id: 'img_sample_poster',
            category: 'Poster utama serial',
            title: 'Poster Resmi: Senja di Pelabuhan Sunda',
            styleName: 'Realistis seperti film layar lebar',
            prompt: 'Poster sinematik drama keluarga Indonesia di pelabuhan tua saat senja dengan kapal pinisi kayu megah',
            imageUrl: '',
            isPlaceholderArt: true,
            createdAt: new Date().toISOString()
          }
        ]
      };
    }

    // State Global In-Memory
    let appState = {
      activeTab: 'dashboard',
      theme: 'dark',
      projects: [],
      activeProjectId: null,
      selectedEpisodeNumber: 1,
      isEditingScript: false,
      audioBlobUrl: null,
      selectedVoice: 'Kore',
      showDashboardGuide: true
    };

    /**
     * =========================================================================
     * 3. MANAJEMEN STATE, NAVIGASI, TEMA & UTILITAS UI
     * =========================================================================
     */
    function initState() {
      const sample = createSampleProject();
      appState.projects = [sample];
      appState.activeProjectId = sample.id;
      appState.selectedEpisodeNumber = 1;
      applyThemeClass();
    }

    function saveState() {
      const proj = getActiveProject();
      if (proj) {
        proj.updatedAt = new Date().toISOString();
      }
    }

    function getActiveProject() {
      if (!appState.projects || appState.projects.length === 0) {
        const sample = createSampleProject();
        appState.projects = [sample];
        appState.activeProjectId = sample.id;
      }
      let proj = appState.projects.find(p => p.id === appState.activeProjectId);
      if (!proj) {
        proj = appState.projects[0];
        appState.activeProjectId = proj.id;
      }
      return proj;
    }

    function escapeHtml(value) {
      return String(value ?? '')
        .replace(/&/g, '&amp;')
        .replace(/</g, '&lt;')
        .replace(/>/g, '&gt;')
        .replace(/"/g, '&quot;')
        .replace(/'/g, '&#39;');
    }

    function navigateTo(tabId) {
      appState.activeTab = tabId;
      appState.isEditingScript = false;
      renderApp();
      window.scrollTo({ top: 0, behavior: 'smooth' });
    }

    function applyThemeClass() {
      const htmlEl = document.documentElement;
      if (appState.theme === 'dark') {
        htmlEl.classList.add('dark');
      } else {
        htmlEl.classList.remove('dark');
      }
    }

    function toggleTheme() {
      appState.theme = appState.theme === 'dark' ? 'light' : 'dark';
      applyThemeClass();
      updateHeaderAndNav();
      if (typeof lucide !== 'undefined') {
        lucide.createIcons();
      }
    }

    function updateHeaderAndNav() {
      const proj = getActiveProject();
      const titleEl = document.getElementById('header-project-title');
      if (titleEl && proj) {
        titleEl.textContent = proj.settings.title || 'Serial Tanpa Judul';
      }

      const themeIcon = document.getElementById('theme-icon');
      if (themeIcon) {
        themeIcon.setAttribute('data-lucide', appState.theme === 'dark' ? 'sun' : 'moon');
      }

      const navContainer = document.getElementById('main-nav-tabs');
      if (navContainer) {
        navContainer.innerHTML = NAV_TABS.map(tab => {
          const isActive = appState.activeTab === tab.id;
          return `
            <button onclick="navigateTo('${tab.id}')"
              class="px-3.5 py-2 rounded-xl text-xs sm:text-sm font-semibold whitespace-nowrap flex items-center gap-2 transition-all ${
                isActive
                  ? 'bg-amber-500 text-slate-950 shadow-sm shadow-amber-500/20'
                  : 'text-slate-600 dark:text-slate-300 hover:bg-slate-200/70 dark:hover:bg-studio-800'
              }">
              <i data-lucide="${tab.icon}" class="w-4 h-4"></i>
              <span>${tab.label}</span>
            </button>
          `;
        }).join('');
      }
    }

    function setLoading(show, title = 'Memproses dengan AI...', subtitle = 'Mohon tunggu sebentar, studio sedang bekerja.') {
      const overlay = document.getElementById('ai-loading-overlay');
      const titleEl = document.getElementById('loading-title');
      const subEl = document.getElementById('loading-subtitle');
      if (!overlay) return;

      if (show) {
        if (titleEl) titleEl.textContent = title;
        if (subEl) subEl.textContent = subtitle;
        overlay.classList.remove('hidden');
        overlay.classList.add('flex');
        if (typeof lucide !== 'undefined') lucide.createIcons();
      } else {
        overlay.classList.add('hidden');
        overlay.classList.remove('flex');
      }
    }

    function showToast(message, type = 'info') {
      const container = document.getElementById('toast-container');
      if (!container) return;

      const styles = {
        success: 'bg-emerald-950/95 border-emerald-500/50 text-emerald-100',
        error: 'bg-rose-950/95 border-rose-500/50 text-rose-100',
        warning: 'bg-amber-950/95 border-amber-500/50 text-amber-100',
        info: 'bg-slate-900/95 border-slate-700 text-slate-100'
      };
      const icons = {
        success: 'check-circle-2',
        error: 'alert-octagon',
        warning: 'alert-triangle',
        info: 'info'
      };

      const toast = document.createElement('div');
      toast.className = `pointer-events-auto flex items-start gap-2.5 px-4 py-3 rounded-2xl border shadow-xl backdrop-blur-md text-xs sm:text-sm animate-fade-in ${styles[type] || styles.info}`;
      toast.innerHTML = `
        <i data-lucide="${icons[type] || 'info'}" class="w-4 h-4 shrink-0 mt-0.5 text-amber-400"></i>
        <span class="flex-1 leading-snug">${escapeHtml(message)}</span>
      `;
      container.appendChild(toast);
      if (typeof lucide !== 'undefined') lucide.createIcons();

      setTimeout(() => {
        toast.style.opacity = '0';
        toast.style.transition = 'opacity 0.3s ease';
        setTimeout(() => toast.remove(), 300);
      }, 4000);
    }

    function openModal(htmlContent) {
      const backdrop = document.getElementById('custom-modal-backdrop');
      const box = document.getElementById('custom-modal-box');
      if (!backdrop || !box) return;

      box.innerHTML = htmlContent;
      backdrop.classList.remove('hidden');
      backdrop.classList.add('flex');
      if (typeof lucide !== 'undefined') lucide.createIcons();
    }

    function closeModal() {
      const backdrop = document.getElementById('custom-modal-backdrop');
      if (!backdrop) return;
      backdrop.classList.add('hidden');
      backdrop.classList.remove('flex');
    }

    function copyTextToClipboard(text) {
      try {
        const ta = document.createElement('textarea');
        ta.value = text;
        ta.style.position = 'fixed';
        ta.style.left = '-9999px';
        document.body.appendChild(ta);
        ta.select();
        document.execCommand('copy');
        document.body.removeChild(ta);
        showToast('Teks berhasil disalin ke clipboard!', 'success');
      } catch (err) {
        showToast('Gagal menyalin teks.', 'error');
      }
    }

    /**
     * =========================================================================
     * 4. KONEKTOR GEMINI AI (TEKS TERSTRUKTUR, GAMBAR & SUARA TTS)
     * =========================================================================
     */
    async function fetchWithBackoff(url, options, maxRetries = 3) {
      let delay = 1000;
      for (let attempt = 0; attempt <= maxRetries; attempt++) {
        try {
          const response = await fetch(url, options);
          if (response.ok) {
            return await response.json();
          }
          if ((response.status === 429 || response.status >= 500) && attempt < maxRetries) {
            await new Promise(res => setTimeout(res, delay));
            delay *= 2;
            continue;
          }
          const errText = await response.text();
          throw new Error(`HTTP ${response.status}: ${errText.slice(0, 180)}`);
        } catch (err) {
          if (attempt < maxRetries) {
            await new Promise(res => setTimeout(res, delay));
            delay *= 2;
            continue;
          }
          throw err;
        }
      }
    }

    async function callGeminiText({ systemPrompt, userPrompt, responseSchema }) {
      const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-3-flash-preview:generateContent?key=${apiKey}`;
      const payload = {
        contents: [{ parts: [{ text: userPrompt }] }],
        systemInstruction: {
          parts: [{ text: systemPrompt }]
        },
        generationConfig: {
          responseMimeType: "application/json",
          responseSchema: responseSchema
        }
      };

      const result = await fetchWithBackoff(apiUrl, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(payload)
      });

      const rawText = result?.candidates?.[0]?.content?.parts?.[0]?.text;
      if (!rawText) {
        throw new Error('AI tidak mengembalikan respons teks.');
      }

      const cleanJson = rawText.replace(/^```json\s*/i, '').replace(/```\s*$/i, '').trim();
      return JSON.parse(cleanJson);
    }

    function compressDataUrlForReference(dataUrl, maxDim = 512) {
      return new Promise((resolve) => {
        if (!dataUrl || typeof dataUrl !== 'string' || !dataUrl.startsWith('data:image/')) {
          resolve(null);
          return;
        }
        const img = new Image();
        img.onload = () => {
          try {
            let w = img.width || maxDim;
            let h = img.height || maxDim;
            if (w > maxDim || h > maxDim) {
              if (w >= h) {
                h = Math.round((h * maxDim) / w);
                w = maxDim;
              } else {
                w = Math.round((w * maxDim) / h);
                h = maxDim;
              }
            }
            const canvas = document.createElement('canvas');
            canvas.width = w;
            canvas.height = h;
            const ctx = canvas.getContext('2d');
            ctx.drawImage(img, 0, 0, w, h);
            resolve(canvas.toDataURL('image/jpeg', 0.82));
          } catch (e) {
            resolve(dataUrl);
          }
        };
        img.onerror = () => resolve(null);
        img.src = dataUrl;
      });
    }

    function extractImageDataUrlFromResult(result) {
      const candidate = result?.candidates?.[0];
      const parts = candidate?.content?.parts || [];
      const imageParts = parts.filter(p => p.inlineData && p.inlineData.data);
      const imgPart = imageParts.length > 0 ? imageParts[imageParts.length - 1] : null;
      if (imgPart) {
        return `data:${imgPart.inlineData.mimeType || 'image/png'};base64,${imgPart.inlineData.data}`;
      }
      const textMsg = parts.find(p => p.text)?.text;
      if (textMsg) {
        throw new Error(textMsg.slice(0, 160));
      }
      if (candidate?.finishReason && candidate.finishReason !== 'STOP') {
        throw new Error(`Permintaan visual dibatasi oleh filter keamanan (${candidate.finishReason}). Coba perhalus deskripsi adegan.`);
      }
      return null;
    }

    async function callGeminiImage({ prompt, referenceImages = [], aspectRatio = '3:4', useAdvanced = true }) {
      const safePrompt = `${prompt}\nProduction guideline: PG-13 cinematic drama artwork, safe for general audience, artistic cinematography, no graphic violence or gore.`;

      const compressedRefs = [];
      for (const rawUrl of (referenceImages || []).slice(0, 2)) {
        const comp = await compressDataUrlForReference(rawUrl, 512);
        if (comp) compressedRefs.push(comp);
      }

      const refParts = [];
      compressedRefs.forEach(dataUrl => {
        const match = dataUrl.match(/^data:(image\/[a-zA-Z0-9+.-]+);base64,(.+)$/);
        if (match) {
          refParts.push({
            inlineData: {
              mimeType: match[1],
              data: match[2]
            }
          });
        }
      });

      const attempts = [];
      if (useAdvanced) {
        attempts.push({
          model: 'gemini-3.1-flash-image',
          payload: {
            contents: [{ role: 'user', parts: [{ text: safePrompt }, ...refParts] }],
            generationConfig: {
              responseModalities: ['TEXT', 'IMAGE'],
              imageConfig: { aspectRatio }
            }
          }
        });
        if (refParts.length > 0) {
          attempts.push({
            model: 'gemini-3.1-flash-image',
            payload: {
              contents: [{ role: 'user', parts: [{ text: safePrompt }] }],
              generationConfig: {
                responseModalities: ['TEXT', 'IMAGE'],
                imageConfig: { aspectRatio }
              }
            }
          });
        }
      }

      attempts.push({
        model: 'gemini-3.1-flash-lite-image',
        payload: {
          contents: [{ parts: [{ text: safePrompt }] }],
          generationConfig: {
            responseModalities: ['TEXT', 'IMAGE']
          }
        }
      });

      let lastError = null;
      for (const attempt of attempts) {
        try {
          const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/${attempt.model}:generateContent?key=${apiKey}`;
          const result = await fetchWithBackoff(apiUrl, {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify(attempt.payload)
          }, 1);

          const extractedUrl = extractImageDataUrlFromResult(result);
          if (extractedUrl) {
            return extractedUrl;
          }
        } catch (err) {
          lastError = err;
        }
      }

      throw lastError || new Error('Gambar tidak dihasilkan oleh AI. Silakan coba lagi.');
    }

    /**
     * =========================================================================
     * 5. KONVERSI & PEMUTAR AUDIO TTS (GEMINI TTS + CADANGAN BROWSER)
     * =========================================================================
     */
    function base64ToArrayBuffer(base64) {
      const cleanBase64 = String(base64 || '').replace(/\s+/g, '');
      const binaryString = window.atob(cleanBase64);
      const len = binaryString.length;
      const bytes = new Uint8Array(len);
      for (let i = 0; i < len; i++) {
        bytes[i] = binaryString.charCodeAt(i);
      }
      return bytes.buffer;
    }

    function pcmToWavBlob(pcmBuffer, sampleRate = 24000, numChannels = 1) {
      const dataLength = pcmBuffer.byteLength;
      const buffer = new ArrayBuffer(44 + dataLength);
      const view = new DataView(buffer);

      function writeString(offset, str) {
        for (let i = 0; i < str.length; i++) {
          view.setUint8(offset + i, str.charCodeAt(i));
        }
      }

      writeString(0, 'RIFF');
      view.setUint32(4, 36 + dataLength, true);
      writeString(8, 'WAVE');
      writeString(12, 'fmt ');
      view.setUint32(16, 16, true);
      view.setUint16(20, 1, true);
      view.setUint16(22, numChannels, true);
      view.setUint32(24, sampleRate, true);
      view.setUint32(28, sampleRate * numChannels * 2, true);
      view.setUint16(32, numChannels * 2, true);
      view.setUint16(34, 16, true);
      writeString(36, 'data');
      view.setUint32(40, dataLength, true);

      const pcmBytes = new Uint8Array(pcmBuffer);
      const wavBytes = new Uint8Array(buffer, 44);
      wavBytes.set(pcmBytes);

      return new Blob([buffer], { type: 'audio/wav' });
    }

    function speakWithBrowserFallback(text) {
      if (!('speechSynthesis' in window)) {
        showToast('Browser Anda tidak mendukung pemutaran suara cadangan.', 'error');
        return;
      }
      window.speechSynthesis.cancel();
      const utterance = new SpeechSynthesisUtterance(text);
      utterance.lang = 'id-ID';
      utterance.rate = 0.96;
      const voices = window.speechSynthesis.getVoices();
      const idVoice = voices.find(v => v.lang && v.lang.toLowerCase().includes('id'));
      if (idVoice) utterance.voice = idVoice;
      window.speechSynthesis.speak(utterance);
      showToast('Memutar pembacaan naskah dengan suara Bahasa Indonesia perangkat.', 'info');
    }

    async function generateEpisodeAudio(epNum) {
      const proj = getActiveProject();
      const script = proj.scripts?.[epNum];
      if (!script) {
        showToast('Naskah episode belum tersedia.', 'warning');
        return;
      }

      const lines = [
        `Episode ${script.episodeNumber}: ${script.title}.`,
        script.summary || '',
        ...(script.scenes || []).slice(0, 3).flatMap(sc => [
          sc.narration || '',
          ...(sc.dialogue || []).map(d => `${d.character}: ${d.line}`)
        ])
      ].filter(Boolean);

      const spokenText = lines.join(' ').slice(0, 2200);
      const voiceName = appState.selectedVoice || 'Kore';

      setLoading(true, 'Menyiapkan Sulih Suara AI...', `Merender pembacaan dramatis Episode ${epNum} dengan suara ${voiceName}.`);
      try {
        const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-tts:generateContent?key=${apiKey}`;
        const payload = {
          contents: [{
            parts: [{
              text: `Bacakan naskah drama Bahasa Indonesia berikut secara ekspresif, hangat, dan sinematik:\n\n${spokenText}`
            }]
          }],
          generationConfig: {
            responseModalities: ['AUDIO'],
            speechConfig: {
              voiceConfig: {
                prebuiltVoiceConfig: { voiceName }
              }
            }
          }
        };

        const result = await fetchWithBackoff(apiUrl, {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify(payload)
        }, 1);

        const parts = result?.candidates?.[0]?.content?.parts || [];
        const audioPart = parts.find(p => p.inlineData && p.inlineData.data);
        if (!audioPart) {
          throw new Error('Data audio tidak ditemukan.');
        }

        const mimeType = audioPart.inlineData.mimeType || '';
        const rateMatch = mimeType.match(/rate=(\d+)/);
        const sampleRate = rateMatch ? parseInt(rateMatch[1], 10) : 24000;

        const arrayBuf = base64ToArrayBuffer(audioPart.inlineData.data);
        const wavBlob = mimeType.includes('wav')
          ? new Blob([arrayBuf], { type: 'audio/wav' })
          : pcmToWavBlob(arrayBuf, sampleRate, 1);

        if (appState.audioBlobUrl) {
          URL.revokeObjectURL(appState.audioBlobUrl);
        }
        appState.audioBlobUrl = URL.createObjectURL(wavBlob);
        renderApp();
        showToast('Audio naskah berhasil dibuat! Silakan tekan tombol Putar pada pemutar audio.', 'success');
      } catch (err) {
        speakWithBrowserFallback(spokenText);
      } finally {
        setLoading(false);
      }
    }

    function downloadEpisodeAudioWav(epNum) {
      if (!appState.audioBlobUrl) {
        showToast('Silakan buat audio naskah terlebih dahulu.', 'warning');
        return;
      }
      const proj = getActiveProject();
      const slug = (proj.settings.title || 'drama').toLowerCase().replace(/[^a-z0-9]+/g, '_');
      const a = document.createElement('a');
      a.href = appState.audioBlobUrl;
      a.download = `${slug}_episode_${epNum}.wav`;
      document.body.appendChild(a);
      a.click();
      document.body.removeChild(a);
      showToast('Mengunduh file audio (.WAV)...', 'success');
    }

    /**
     * =========================================================================
     * 6. FUNGSI GENERATOR AI UNTUK CERITA, KARAKTER, ALUR & NASKAH
     * =========================================================================
     */
    async function aiAutoFillStorySettings() {
      const proj = getActiveProject();
      const activeGenre = proj.customGenre.trim() || proj.genre || 'Drama keluarga';
      const currentIdea = proj.settings.synopsis || proj.settings.title || '';

      setLoading(true, 'Merancang Konsep Serial Drama...', `AI sedang mengembangkan ide cerita untuk genre "${activeGenre}".`);
      try {
        const schema = {
          type: "OBJECT",
          properties: {
            title: { type: "STRING" },
            theme: { type: "STRING" },
            synopsis: { type: "STRING" },
            settingPlace: { type: "STRING" },
            era: { type: "STRING" },
            mood: { type: "STRING" },
            audience: { type: "STRING" },
            narrativeStyle: { type: "STRING" },
            moralMessage: { type: "STRING" }
          },
          required: ["title", "theme", "synopsis", "settingPlace", "era", "mood", "audience", "narrativeStyle", "moralMessage"]
        };

        const data = await callGeminiText({
          systemPrompt: 'Anda adalah Showrunner & Kepala Penulis Skenario Serial Drama profesional Indonesia. Buat konsep serial drama yang emosional, kuat, logis, dan menarik dalam Bahasa Indonesia.',
          userPrompt: `Buatkan konsep pengaturan cerita serial drama lengkap untuk genre: "${activeGenre}".
Jumlah episode: ${proj.settings.episodeCount} episode (${proj.settings.episodeDuration}).
Catatan awal pengguna (jika ada): "${currentIdea}".`,
          responseSchema: schema
        });

        proj.settings = {
          ...proj.settings,
          ...data
        };
        saveState();
        renderApp();
        showToast('Konsep & pengaturan cerita berhasil dibuat oleh AI!', 'success');
      } catch (err) {
        showToast('Gagal membuat konsep cerita: ' + err.message, 'error');
      } finally {
        setLoading(false);
      }
    }

    async function aiGenerateCharacters() {
      const proj = getActiveProject();
      const activeGenre = proj.customGenre.trim() || proj.genre;

      setLoading(true, 'Menciptakan Karakter Serial...', 'AI sedang merancang profil tokoh beserta ciri fisik & gaya pakaian yang konsisten.');
      try {
        const schema = {
          type: "OBJECT",
          properties: {
            characters: {
              type: "ARRAY",
              items: {
                type: "OBJECT",
                properties: {
                  name: { type: "STRING" },
                  age: { type: "STRING" },
                  gender: { type: "STRING" },
                  role: { type: "STRING" },
                  personality: { type: "STRING" },
                  background: { type: "STRING" },
                  relationships: { type: "STRING" },
                  physicalTraits: { type: "STRING" },
                  clothingStyle: { type: "STRING" }
                },
                required: ["name", "age", "gender", "role", "personality", "background", "relationships", "physicalTraits", "clothingStyle"]
              }
            }
          },
          required: ["characters"]
        };

        const data = await callGeminiText({
          systemPrompt: 'Anda adalah Casting Director & Perancang Karakter Serial Drama Indonesia. Buat 4 hingga 5 karakter utama dan pendukung yang saling terhubung secara dramatis. Berikan deskripsi ciri fisik dan gaya pakaian yang spesifik agar konsisten di semua episode.',
          userPrompt: `Judul Serial: "${proj.settings.title}"
Genre: "${activeGenre}"
Tema: "${proj.settings.theme}"
Sinopsis: "${proj.settings.synopsis}"
Latar Tempat & Zaman: "${proj.settings.settingPlace}" (${proj.settings.era})`,
          responseSchema: schema
        });

        const existingImages = {};
        (proj.characters || []).forEach(c => {
          if (c.imageUrl) existingImages[c.name.toLowerCase()] = c.imageUrl;
        });

        proj.characters = (data.characters || []).map((c, idx) => ({
          id: 'char_' + Date.now() + '_' + idx,
          ...c,
          imageUrl: existingImages[c.name.toLowerCase()] || ''
        }));

        saveState();
        renderApp();
        showToast(`${proj.characters.length} karakter berhasil dibuat!`, 'success');
      } catch (err) {
        showToast('Gagal membuat karakter: ' + err.message, 'error');
      } finally {
        setLoading(false);
      }
    }

    async function aiGenerateSingleCharacterPortrait(charId) {
      const proj = getActiveProject();
      const char = (proj.characters || []).find(c => c.id === charId);
      if (!char) return;

      const prompt = `Close-up cinematic character portrait for Indonesian drama series "${proj.settings.title}".
Character: ${char.name}, ${char.age}, ${char.gender}, role: ${char.role}.
Physical appearance (MUST BE EXACT): ${char.physicalTraits}.
Signature clothing: ${char.clothingStyle}.
Setting background hint: ${proj.settings.settingPlace} (${proj.settings.era}).
Style: ${VISUAL_STYLES[0].prompt}.`;

      setLoading(true, `Membuat Foto Referensi ${char.name}...`, 'Foto ini akan menjadi acuan konsistensi wajah & pakaian di semua episode.');
      try {
        const imageUrl = await callGeminiImage({
          prompt,
          referenceImages: char.imageUrl ? [char.imageUrl] : [],
          aspectRatio: '3:4',
          useAdvanced: true
        });

        char.imageUrl = imageUrl;
        proj.gallery = (proj.gallery || []).filter(g => !g.isPlaceholderArt);
        proj.gallery.unshift({
          id: 'img_' + Date.now(),
          category: 'Foto setiap karakter',
          title: `Referensi Karakter: ${char.name}`,
          styleName: 'Realistis seperti film layar lebar',
          prompt,
          imageUrl,
          createdAt: new Date().toISOString()
        });

        saveState();
        renderApp();
        showToast(`Foto referensi ${char.name} berhasil dibuat!`, 'success');
      } catch (err) {
        showToast('Gagal membuat foto karakter: ' + err.message, 'error');
      } finally {
        setLoading(false);
      }
    }

    async function aiGenerateStoryArc() {
      const proj = getActiveProject();
      const activeGenre = proj.customGenre.trim() || proj.genre;
      const epCount = Math.max(1, Math.min(30, parseInt(proj.settings.episodeCount, 10) || 5));
      const charSummary = (proj.characters || [])
        .map(c => `- ${c.name} (${c.role}, ${c.age}): ${c.personality}. Hubungan: ${c.relationships}`)
        .join('\n');

      setLoading(true, `Menyusun Alur Serial (${epCount} Episode)...`, 'AI memastikan setiap episode saling terhubung dari awal hingga akhir.');
      try {
        const schema = {
          type: "OBJECT",
          properties: {
            storyIdea: { type: "STRING" },
            fullSynopsis: { type: "STRING" },
            mainConflict: { type: "STRING" },
            subConflicts: { type: "STRING" },
            climax: { type: "STRING" },
            plotTwist: { type: "STRING" },
            resolution: { type: "STRING" },
            characterDynamics: { type: "STRING" },
            episodes: {
              type: "ARRAY",
              items: {
                type: "OBJECT",
                properties: {
                  episodeNumber: { type: "INTEGER" },
                  title: { type: "STRING" },
                  summary: { type: "STRING" },
                  connectionToMainArc: { type: "STRING" },
                  cliffhanger: { type: "STRING" }
                },
                required: ["episodeNumber", "title", "summary", "connectionToMainArc", "cliffhanger"]
              }
            }
          },
          required: ["storyIdea", "fullSynopsis", "mainConflict", "subConflicts", "climax", "plotTwist", "resolution", "characterDynamics", "episodes"]
        };

        const data = await callGeminiText({
          systemPrompt: 'Anda adalah Kepala Penulis Serial Drama televisi & OTT. Rancang alur cerita serial bersambung yang utuh. PENTING: Semua episode harus saling terhubung dari Episode 1 sampai Episode terakhir. Jangan membuat episode yang berdiri sendiri tanpa kaitan dengan konflik utama.',
          userPrompt: `Judul: "${proj.settings.title}"
Genre: "${activeGenre}"
Tema: "${proj.settings.theme}"
Sinopsis Awal: "${proj.settings.synopsis}"
Latar: "${proj.settings.settingPlace}" (${proj.settings.era}), Suasana: "${proj.settings.mood}"
Pesan Moral: "${proj.settings.moralMessage}"
Jumlah Episode WAJIB: TEPAT ${epCount} episode.
Daftar Tokoh:
${charSummary || 'Belum ada daftar tokoh khusus, silakan sesuaikan dengan cerita.'}`,
          responseSchema: schema
        });

        proj.storyArc = data;
        saveState();
        renderApp();
        showToast(`Alur cerita berseri ${data.episodes.length} episode berhasil disusun!`, 'success');
      } catch (err) {
        showToast('Gagal menyusun alur cerita: ' + err.message, 'error');
      } finally {
        setLoading(false);
      }
    }

    const SCRIPT_SCHEMA = {
      type: "OBJECT",
      properties: {
        episodeNumber: { type: "INTEGER" },
        title: { type: "STRING" },
        summary: { type: "STRING" },
        openingHook: { type: "STRING" },
        scenes: {
          type: "ARRAY",
          items: {
            type: "OBJECT",
            properties: {
              sceneNumber: { type: "INTEGER" },
              heading: { type: "STRING" },
              locationDesc: { type: "STRING" },
              charactersPresent: { type: "ARRAY", items: { type: "STRING" } },
              narration: { type: "STRING" },
              dialogue: {
                type: "ARRAY",
                items: {
                  type: "OBJECT",
                  properties: {
                    character: { type: "STRING" },
                    emotion: { type: "STRING" },
                    line: { type: "STRING" }
                  },
                  required: ["character", "emotion", "line"]
                }
              },
              cameraDirection: { type: "STRING" },
              visualDesc: { type: "STRING" },
              musicAmbience: { type: "STRING" }
            },
            required: ["sceneNumber", "heading", "locationDesc", "charactersPresent", "narration", "dialogue", "cameraDirection", "visualDesc", "musicAmbience"]
          }
        },
        closingCliffhanger: { type: "STRING" }
      },
      required: ["episodeNumber", "title", "summary", "openingHook", "scenes", "closingCliffhanger"]
    };

    async function aiGenerateEpisodeScript(epNum) {
      const proj = getActiveProject();
      const epOutline = (proj.storyArc?.episodes || []).find(e => e.episodeNumber === epNum);
      const prevScript = proj.scripts?.[epNum - 1];
      const charContext = (proj.characters || [])
        .map(c => `${c.name} (${c.role}, sifat: ${c.personality}, fisik: ${c.physicalTraits}, pakaian: ${c.clothingStyle})`)
        .join('\n');

      setLoading(true, `Menulis Naskah Episode ${epNum}...`, 'AI sedang menyusun adegan pembuka, dialog penuh emosi, arahan kamera, dan cliffhanger.');
      try {
        const data = await callGeminiText({
          systemPrompt: 'Anda adalah Penulis Naskah Drama Sinematik profesional Indonesia. Tulis naskah episode lengkap yang terhubung erat dengan episode sebelumnya dan alur utama serial. Gunakan dialog alami berbahasa Indonesia yang menyentuh dan kuat.',
          userPrompt: `Judul Serial: "${proj.settings.title}" (${proj.customGenre.trim() || proj.genre})
Sinopsis Utama: "${proj.storyArc?.fullSynopsis || proj.settings.synopsis}"
Konflik Utama: "${proj.storyArc?.mainConflict || ''}"
Plot Twist Serial: "${proj.storyArc?.plotTwist || ''}"
Karakter & Ciri Konsisten:
${charContext}

Target Penulisan: EPISODE ${epNum} dari ${proj.settings.episodeCount}
Judul Episode: "${epOutline?.title || `Episode ${epNum}`}"
Ringkasan Alur Episode ${epNum}: "${epOutline?.summary || ''}"
Keterkaitan dengan Cerita Utama: "${epOutline?.connectionToMainArc || ''}"
Target Cliffhanger Akhir Episode: "${epOutline?.cliffhanger || ''}"
${prevScript ? `Ringkasan & Cliffhanger Episode ${epNum - 1} sebelumnya (lanjutkan secara mulus): "${prevScript.closingCliffhanger}"` : 'Ini adalah Episode 1 (pembuka serial).'}

Buat minimal 4 sampai 6 adegan yang kaya detail visual, arahan kamera, dan dialog mendalam.`,
          responseSchema: SCRIPT_SCHEMA
        });

        data.episodeNumber = epNum;
        if (!proj.scripts) proj.scripts = {};
        proj.scripts[epNum] = data;
        appState.selectedEpisodeNumber = epNum;
        appState.isEditingScript = false;
        saveState();
        renderApp();
        showToast(`Naskah Episode ${epNum}: "${data.title}" selesai dibuat!`, 'success');
      } catch (err) {
        showToast('Gagal menulis naskah episode: ' + err.message, 'error');
      } finally {
        setLoading(false);
      }
    }

    async function aiModifyEpisodeScript(epNum, mode) {
      const proj = getActiveProject();
      const existingScript = proj.scripts?.[epNum];
      if (!existingScript) {
        await aiGenerateEpisodeScript(epNum);
        return;
      }

      const modeInstructions = {
        dialog: {
          title: 'Membuat Ulang Dialog Episode...',
          sub: 'AI sedang mempertajam emosi, subteks, dan kealamian dialog antar karakter.',
          instruction: 'Pertahankan struktur adegan dan alur cerita episode ini, namun TULIS ULANG seluruh dialog agar jauh lebih emosional, tajam, alami, dan menyentuh hati.'
        },
        extend: {
          title: 'Memperpanjang Cerita Episode...',
          sub: 'AI sedang menambahkan adegan baru dan memperdalam konflik emosional.',
          instruction: 'PERPANJANG cerita episode ini dengan menambahkan 2 hingga 3 adegan baru yang memperkaya dinamika antar tokoh, memperdalam latar belakang, dan memperpanjang durasi dialog tanpa merusak kesinambungan dengan episode berikutnya.'
        },
        conflict: {
          title: 'Mengubah & Mempertajam Konflik...',
          sub: 'AI sedang menyuntikkan ketegangan dramatis dan dilema baru.',
          instruction: 'UBAH DAN PERTAJAM konflik dalam episode ini agar taruhannya lebih tinggi, lebih mengejutkan, dan membuat dilema karakter semakin sulit namun tetap terhubung ke alur utama serial.'
        }
      };

      const cfg = modeInstructions[mode] || modeInstructions.dialog;
      setLoading(true, cfg.title, cfg.sub);
      try {
        const data = await callGeminiText({
          systemPrompt: 'Anda adalah Script Doctor & Penulis Skenario Serial Drama Indonesia. Revisi naskah episode berikut sesuai instruksi dengan tetap menjaga konsistensi karakter dan kesinambungan serial.',
          userPrompt: `Instruksi Revisi: ${cfg.instruction}

Naskah Episode ${epNum} Saat Ini:
${JSON.stringify(existingScript)}`,
          responseSchema: SCRIPT_SCHEMA
        });

        data.episodeNumber = epNum;
        proj.scripts[epNum] = data;
        saveState();
        renderApp();
        showToast(`Naskah Episode ${epNum} berhasil diperbarui!`, 'success');
      } catch (err) {
        showToast('Gagal memodifikasi naskah: ' + err.message, 'error');
      } finally {
        setLoading(false);
      }
    }

    /**
     * =========================================================================
     * 7. GENERATOR GAMBAR AI & UNDUH GAMBAR RAMAH HP
     * =========================================================================
     */
    async function aiGenerateVisualAsset() {
      const proj = getActiveProject();
      const category = document.getElementById('vis-category')?.value || 'Poster utama serial';
      const styleId = document.getElementById('vis-style')?.value || VISUAL_STYLES[0].id;
      const targetVal = document.getElementById('vis-target')?.value || '';
      const aspectRatio = document.getElementById('vis-aspect')?.value || '3:4';
      const customNote = document.getElementById('vis-custom-note')?.value || '';

      const styleObj = VISUAL_STYLES.find(s => s.id === styleId) || VISUAL_STYLES[0];
      const chars = proj.characters || [];
      const refImages = chars.map(c => c.imageUrl).filter(Boolean);
      const charConsistencyText = chars.map(c =>
        `${c.name} (${c.role}): ${c.physicalTraits}, wearing ${c.clothingStyle}`
      ).join('; ');

      let subjectPrompt = '';
      let displayTitle = `${category} - ${proj.settings.title}`;

      if (category === 'Poster utama serial') {
        subjectPrompt = `Official theatrical & streaming series key art poster for Indonesian drama "${proj.settings.title}" (${proj.customGenre.trim() || proj.genre}).
Theme: ${proj.settings.theme}.
Setting: ${proj.settings.settingPlace} (${proj.settings.era}), mood: ${proj.settings.mood}.
Main cast featured prominently (keep consistent faces & outfits): ${charConsistencyText}.
Include subtle atmospheric title typography space at top or bottom.`;
        displayTitle = `Poster Utama: ${proj.settings.title}`;
      } else if (category === 'Foto setiap karakter') {
        const charId = targetVal.replace('char:', '');
        const char = chars.find(c => c.id === charId) || chars[0];
        if (!char) {
          showToast('Silakan buat atau pilih karakter terlebih dahulu.', 'warning');
          return;
        }
        subjectPrompt = `Character portrait & costume reference sheet for Indonesian drama "${proj.settings.title}".
Character: ${char.name}, ${char.age}, ${char.gender}, ${char.role}.
Exact Physical Appearance: ${char.physicalTraits}.
Exact Clothing Style: ${char.clothingStyle}.
Background setting: ${proj.settings.settingPlace} (${proj.settings.era}).`;
        displayTitle = `Potret Karakter: ${char.name}`;
      } else if (category === 'Ilustrasi setiap adegan') {
        const [epStr, scStr] = targetVal.replace('scene:', '').split(':');
        const epNum = parseInt(epStr, 10) || appState.selectedEpisodeNumber || 1;
        const scIdx = parseInt(scStr, 10) || 0;
        const scene = proj.scripts?.[epNum]?.scenes?.[scIdx];
        if (!scene) {
          showToast('Adegan naskah tidak ditemukan. Buat naskah episode terlebih dahulu.', 'warning');
          return;
        }
        subjectPrompt = `Cinematic film scene still for "${proj.settings.title}" Episode ${epNum} Scene ${scene.sceneNumber}.
Location: ${scene.locationDesc} (${proj.settings.era}).
Visual Action: ${scene.visualDesc}.
Camera Framing: ${scene.cameraDirection}.
Characters present (keep exact face & clothing consistency): ${charConsistencyText}.`;
        displayTitle = `Ep ${epNum} Adegan ${scene.sceneNumber}: ${scene.heading}`;
      } else if (category === 'Background lokasi') {
        subjectPrompt = `Empty cinematic establishing shot background environment for Indonesian drama "${proj.settings.title}".
Location: ${proj.settings.settingPlace}, Era: ${proj.settings.era}, Atmosphere: ${proj.settings.mood}.
Rich architectural & environmental storytelling details, no people in foreground.`;
        displayTitle = `Latar Lokasi: ${proj.settings.settingPlace}`;
      } else {
        const epNum = parseInt(targetVal.replace('ep:', ''), 10) || 1;
        const epOutline = (proj.storyArc?.episodes || []).find(e => e.episodeNumber === epNum);
        subjectPrompt = `${category} for Indonesian drama series "${proj.settings.title}", Episode ${epNum}: "${epOutline?.title || 'Episode ' + epNum}".
Episode Story: ${epOutline?.summary || proj.settings.synopsis}.
Setting: ${proj.settings.settingPlace} (${proj.settings.era}).
Characters (consistent appearance): ${charConsistencyText}.`;
        displayTitle = `${category} - Ep ${epNum}: ${epOutline?.title || ''}`;
      }

      const fullPrompt = `${subjectPrompt}
${customNote ? `Additional Director Note: ${customNote}` : ''}
Visual Style: ${styleObj.prompt}.`;

      setLoading(true, `Membuat ${category}...`, 'AI Sinematografer sedang merender visual berkualitas tinggi.');
      try {
        const imageUrl = await callGeminiImage({
          prompt: fullPrompt,
          referenceImages: refImages,
          aspectRatio,
          useAdvanced: true
        });

        if (category === 'Foto setiap karakter' && targetVal.startsWith('char:')) {
          const cId = targetVal.split(':')[1];
          const char = chars.find(c => c.id === cId);
          if (char) char.imageUrl = imageUrl;
        }

        proj.gallery = (proj.gallery || []).filter(g => !g.isPlaceholderArt);
        proj.gallery.unshift({
          id: 'img_' + Date.now(),
          category,
          title: displayTitle,
          styleName: styleObj.name,
          prompt: fullPrompt,
          imageUrl,
          createdAt: new Date().toISOString()
        });

        saveState();
        renderApp();
        showToast(`${category} berhasil dibuat dan ditambahkan ke galeri!`, 'success');
      } catch (err) {
        showToast('Gagal membuat gambar AI: ' + err.message, 'error');
      } finally {
        setLoading(false);
      }
    }

    async function aiGenerateSceneIllustration(epNum, sceneIdx) {
      const proj = getActiveProject();
      const script = proj.scripts?.[epNum];
      const scene = script?.scenes?.[sceneIdx];
      if (!scene) return;

      const charsInScene = (proj.characters || []).filter(c =>
        (scene.charactersPresent || []).some(name =>
          name.toLowerCase().includes(c.name.toLowerCase()) ||
          c.name.toLowerCase().includes(name.toLowerCase())
        )
      );

      const refImages = charsInScene.map(c => c.imageUrl).filter(Boolean);
      const charLockText = charsInScene.map(c =>
        `${c.name}: ${c.physicalTraits}, wearing ${c.clothingStyle}`
      ).join('; ');

      const prompt = `Cinematic film scene illustration for Indonesian drama series "${proj.settings.title}", Episode ${epNum} Scene ${scene.sceneNumber || sceneIdx + 1}.
Location: ${scene.locationDesc} (${proj.settings.era}).
Camera & Composition: ${scene.cameraDirection}.
Visual Action: ${scene.visualDesc}.
Characters in scene (keep exact face, hair, and outfit consistency): ${charLockText || (scene.charactersPresent || []).join(', ')}.
Style: ${VISUAL_STYLES[0].prompt}.`;

      setLoading(true, `Membuat Ilustrasi Adegan ${sceneIdx + 1}...`, 'Menggunakan referensi karakter konsisten untuk memvisualisasikan adegan naskah.');
      try {
        const imageUrl = await callGeminiImage({
          prompt,
          referenceImages: refImages,
          aspectRatio: '16:9',
          useAdvanced: true
        });

        const createdImgId = 'img_' + Date.now();
        proj.gallery = (proj.gallery || []).filter(g => !g.isPlaceholderArt);
        proj.gallery.unshift({
          id: createdImgId,
          category: 'Ilustrasi setiap adegan',
          title: `Ep ${epNum} - Adegan ${sceneIdx + 1}: ${scene.heading}`,
          styleName: 'Realistis seperti film layar lebar',
          prompt,
          imageUrl,
          createdAt: new Date().toISOString()
        });

        saveState();
        showToast('Ilustrasi adegan berhasil dibuat!', 'success');
        openImagePreviewModal(createdImgId);
      } catch (err) {
        showToast('Gagal membuat ilustrasi adegan: ' + err.message, 'error');
      } finally {
        setLoading(false);
      }
    }

    function dataUrlToBlob(dataUrl) {
      const parts = dataUrl.split(',');
      const mimeMatch = parts[0].match(/:(.*?);/);
      const mime = mimeMatch ? mimeMatch[1] : 'image/png';
      const binary = atob(parts[1]);
      const len = binary.length;
      const u8arr = new Uint8Array(len);
      for (let i = 0; i < len; i++) {
        u8arr[i] = binary.charCodeAt(i);
      }
      return new Blob([u8arr], { type: mime });
    }

    function downloadImageById(imgId) {
      const proj = getActiveProject();
      const item = (proj.gallery || []).find(g => g.id === imgId);
      if (!item || !item.imageUrl) {
        showToast('Gambar belum tersedia untuk diunduh.', 'warning');
        return;
      }

      try {
        const blob = dataUrlToBlob(item.imageUrl);
        const blobUrl = URL.createObjectURL(blob);
        const safeName = (item.title || 'drama_visual').toLowerCase().replace(/[^a-z0-9]+/g, '_');

        const link = document.createElement('a');
        link.href = blobUrl;
        link.download = `${safeName}.png`;
        link.rel = 'noopener';
        document.body.appendChild(link);
        link.click();
        document.body.removeChild(link);

        setTimeout(() => {
          URL.revokeObjectURL(blobUrl);
        }, 12000);

        showToast('Gambar sedang diunduh ke perangkat Anda!', 'success');
      } catch (err) {
        showToast('Gagal mengunduh gambar. Coba gunakan tombol Simpan / Bagikan.', 'error');
      }
    }

    async function shareImageById(imgId) {
      const proj = getActiveProject();
      const item = (proj.gallery || []).find(g => g.id === imgId);
      if (!item || !item.imageUrl) return;

      try {
        const blob = dataUrlToBlob(item.imageUrl);
        const safeName = (item.title || 'drama_visual').toLowerCase().replace(/[^a-z0-9]+/g, '_') + '.png';
        const file = new File([blob], safeName, { type: 'image/png' });

        if (navigator.canShare && navigator.canShare({ files: [file] })) {
          await navigator.share({
            files: [file],
            title: item.title,
            text: `Visual Serial Drama: ${proj.settings.title}`
          });
          showToast('Gambar berhasil dibagikan / disimpan!', 'success');
        } else {
          downloadImageById(imgId);
        }
      } catch (err) {
        if (err.name !== 'AbortError') {
          downloadImageById(imgId);
        }
      }
    }

    function deleteGalleryItem(imgId) {
      const proj = getActiveProject();
      proj.gallery = (proj.gallery || []).filter(g => g.id !== imgId);
      saveState();
      closeModal();
      renderApp();
      showToast('Visual dihapus dari galeri.', 'info');
    }

    function openImagePreviewModal(imgId) {
      const proj = getActiveProject();
      const item = (proj.gallery || []).find(g => g.id === imgId);
      if (!item) return;

      openModal(`
        <div class="flex items-center justify-between mb-3">
          <div>
            <span class="text-[11px] font-semibold uppercase tracking-wider text-amber-500">${escapeHtml(item.category)}</span>
            <h3 class="font-serif font-bold text-lg text-slate-900 dark:text-white">${escapeHtml(item.title)}</h3>
          </div>
          <button onclick="closeModal()" class="p-2 rounded-xl hover:bg-slate-100 dark:hover:bg-studio-800 text-slate-400">
            <i data-lucide="x" class="w-5 h-5"></i>
          </button>
        </div>

        <div class="rounded-2xl overflow-hidden bg-slate-950 border border-slate-800 mb-4 flex items-center justify-center max-h-[62vh]">
          ${item.imageUrl
            ? `<img src="${item.imageUrl}" alt="${escapeHtml(item.title)}" class="max-h-[62vh] w-auto object-contain" />`
            : `<div class="p-10 text-center text-slate-400 text-sm">Belum ada gambar AI. Silakan klik tombol Buat Gambar AI di Studio Visual.</div>`
          }
        </div>

        <div class="text-xs text-slate-500 dark:text-slate-400 mb-4">
          <span class="font-semibold text-slate-700 dark:text-slate-300">Gaya Visual:</span> ${escapeHtml(item.styleName)}
        </div>

        <div class="flex flex-wrap items-center justify-between gap-2">
          <button onclick="deleteGalleryItem('${item.id}')" class="px-3.5 py-2.5 rounded-xl bg-rose-500/10 hover:bg-rose-500/20 text-rose-500 text-xs font-semibold flex items-center gap-1.5">
            <i data-lucide="trash-2" class="w-4 h-4"></i>
            <span>Hapus</span>
          </button>
          <div class="flex flex-wrap items-center gap-2">
            ${item.imageUrl ? `
              <button onclick="shareImageById('${item.id}')" class="px-4 py-2.5 rounded-xl bg-slate-200 dark:bg-studio-800 hover:bg-slate-300 dark:hover:bg-studio-700 text-xs font-semibold flex items-center gap-1.5">
                <i data-lucide="share-2" class="w-4 h-4"></i>
                <span>Simpan / Bagikan</span>
              </button>
              <button onclick="downloadImageById('${item.id}')" class="px-4 py-2.5 rounded-xl bg-amber-500 hover:bg-amber-400 text-slate-950 text-xs font-bold flex items-center gap-1.5">
                <i data-lucide="download" class="w-4 h-4"></i>
                <span>Unduh PNG</span>
              </button>
            ` : ''}
          </div>
        </div>
      `);
    }

    /**
     * =========================================================================
     * 8. MANAJEMEN PROYEK, KARAKTER CRUD & PANDUAN PENGGUNA
     * =========================================================================
     */
    function selectProject(projectId) {
      appState.activeProjectId = projectId;
      appState.selectedEpisodeNumber = 1;
      saveState();
      renderApp();
      showToast('Proyek serial berhasil dibuka!', 'success');
    }

    function openNewProjectModal() {
      openModal(`
        <div class="flex items-center justify-between mb-4">
          <div class="flex items-center gap-2.5">
            <div class="w-9 h-9 rounded-xl bg-amber-500/15 text-amber-500 flex items-center justify-center">
              <i data-lucide="clapperboard" class="w-5 h-5"></i>
            </div>
            <div>
              <h3 class="font-serif font-bold text-xl">Mulai Proyek Serial Drama Baru</h3>
              <p class="text-xs text-slate-500 dark:text-slate-400">Masukkan judul atau ide singkat untuk memulai studio baru</p>
            </div>
          </div>
          <button onclick="closeModal()" class="p-1.5 rounded-lg hover:bg-slate-100 dark:hover:bg-studio-800 text-slate-400">
            <i data-lucide="x" class="w-5 h-5"></i>
          </button>
        </div>

        <div class="space-y-4">
          <div>
            <label class="block text-xs font-semibold mb-1.5">Judul Sementara Serial Drama</label>
            <input id="new-proj-title" type="text" placeholder="Contoh: Cahaya di Ujung Rindu" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-100 dark:bg-studio-800 border border-slate-200 dark:border-slate-700 text-sm focus:outline-none focus:border-amber-500" />
          </div>
          <div>
            <label class="block text-xs font-semibold mb-1.5">Pilih Genre Utama</label>
            <select id="new-proj-genre" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-100 dark:bg-studio-800 border border-slate-200 dark:border-slate-700 text-sm focus:outline-none focus:border-amber-500">
              ${GENRE_LIST.map(g => `<option value="${escapeHtml(g.name)}">${escapeHtml(g.name)}</option>`).join('')}
            </select>
          </div>
          <div>
            <label class="block text-xs font-semibold mb-1.5">Jumlah Episode</label>
            <select id="new-proj-eps" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-100 dark:bg-studio-800 border border-slate-200 dark:border-slate-700 text-sm focus:outline-none focus:border-amber-500">
              <option value="3">3 Episode (Mini Seri)</option>
              <option value="5" selected>5 Episode (Standar)</option>
              <option value="10">10 Episode (Musim Penuh)</option>
              <option value="15">15 Episode</option>
              <option value="20">20 Episode</option>
            </select>
          </div>
        </div>

        <div class="flex justify-end gap-2.5 mt-6">
          <button onclick="closeModal()" class="px-4 py-2.5 rounded-xl bg-slate-200 dark:bg-studio-800 text-xs sm:text-sm font-semibold">Batal</button>
          <button onclick="confirmCreateNewProject()" class="px-5 py-2.5 rounded-xl bg-amber-500 hover:bg-amber-400 text-slate-950 text-xs sm:text-sm font-bold flex items-center gap-1.5">
            <i data-lucide="sparkles" class="w-4 h-4"></i>
            <span>Buat & Masuk Studio</span>
          </button>
        </div>
      `);
    }

    function confirmCreateNewProject() {
      const titleInput = document.getElementById('new-proj-title')?.value.trim() || 'Serial Drama Tanpa Judul';
      const genreInput = document.getElementById('new-proj-genre')?.value || 'Drama keluarga';
      const epsInput = parseInt(document.getElementById('new-proj-eps')?.value, 10) || 5;

      const newProj = {
        id: 'proj_' + Date.now(),
        updatedAt: new Date().toISOString(),
        genre: genreInput,
        customGenre: '',
        settings: {
          title: titleInput,
          theme: '',
          synopsis: '',
          settingPlace: 'Indonesia',
          era: 'Masa Kini (2026)',
          mood: 'Emosional & Sinematik',
          audience: 'Semua Umur / Keluarga',
          episodeCount: epsInput,
          episodeDuration: '45 Menit (Standar TV/Streaming)',
          narrativeStyle: 'Alur Maju Dramatis',
          moralMessage: ''
        },
        characters: [],
        storyArc: null,
        scripts: {},
        gallery: []
      };

      appState.projects.unshift(newProj);
      appState.activeProjectId = newProj.id;
      appState.selectedEpisodeNumber = 1;
      closeModal();
      navigateTo('setup');
      showToast(`Proyek "${titleInput}" berhasil dibuat!`, 'success');
    }

    function openCharacterModal(charId = null) {
      const proj = getActiveProject();
      const existing = charId ? (proj.characters || []).find(c => c.id === charId) : null;

      openModal(`
        <div class="flex items-center justify-between mb-4">
          <h3 class="font-serif font-bold text-xl">${existing ? 'Edit Profil Karakter' : 'Tambah Karakter Baru'}</h3>
          <button onclick="closeModal()" class="p-1.5 rounded-lg hover:bg-slate-100 dark:hover:bg-studio-800 text-slate-400">
            <i data-lucide="x" class="w-5 h-5"></i>
          </button>
        </div>

        <div class="grid grid-cols-1 sm:grid-cols-2 gap-3.5 max-h-[65vh] overflow-y-auto pr-1">
          <div>
            <label class="block text-xs font-semibold mb-1">Nama Karakter *</label>
            <input id="char-name" type="text" value="${escapeHtml(existing?.name || '')}" placeholder="Contoh: Raka Pratama" class="w-full px-3 py-2 rounded-xl bg-slate-100 dark:bg-studio-800 border border-slate-200 dark:border-slate-700 text-sm" />
          </div>
          <div>
            <label class="block text-xs font-semibold mb-1">Usia</label>
            <input id="char-age" type="text" value="${escapeHtml(existing?.age || '')}" placeholder="Contoh: 28 Tahun" class="w-full px-3 py-2 rounded-xl bg-slate-100 dark:bg-studio-800 border border-slate-200 dark:border-slate-700 text-sm" />
          </div>
          <div>
            <label class="block text-xs font-semibold mb-1">Jenis Kelamin</label>
            <select id="char-gender" class="w-full px-3 py-2 rounded-xl bg-slate-100 dark:bg-studio-800 border border-slate-200 dark:border-slate-700 text-sm">
              <option value="Laki-laki" ${existing?.gender === 'Laki-laki' ? 'selected' : ''}>Laki-laki</option>
              <option value="Perempuan" ${existing?.gender === 'Perempuan' ? 'selected' : ''}>Perempuan</option>
            </select>
          </div>
          <div>
            <label class="block text-xs font-semibold mb-1">Peran dalam Cerita</label>
            <input id="char-role" type="text" value="${escapeHtml(existing?.role || '')}" placeholder="Protagonis / Antagonis / Mentor" class="w-full px-3 py-2 rounded-xl bg-slate-100 dark:bg-studio-800 border border-slate-200 dark:border-slate-700 text-sm" />
          </div>
          <div class="sm:col-span-2">
            <label class="block text-xs font-semibold mb-1">Sifat dan Kepribadian</label>
            <textarea id="char-personality" rows="2" class="w-full px-3 py-2 rounded-xl bg-slate-100 dark:bg-studio-800 border border-slate-200 dark:border-slate-700 text-sm">${escapeHtml(existing?.personality || '')}</textarea>
          </div>
          <div class="sm:col-span-2">
            <label class="block text-xs font-semibold mb-1">Latar Belakang Kehidupan</label>
            <textarea id="char-background" rows="2" class="w-full px-3 py-2 rounded-xl bg-slate-100 dark:bg-studio-800 border border-slate-200 dark:border-slate-700 text-sm">${escapeHtml(existing?.background || '')}</textarea>
          </div>
          <div class="sm:col-span-2">
            <label class="block text-xs font-semibold mb-1">Hubungan dengan Karakter Lain</label>
            <input id="char-relationships" type="text" value="${escapeHtml(existing?.relationships || '')}" class="w-full px-3 py-2 rounded-xl bg-slate-100 dark:bg-studio-800 border border-slate-200 dark:border-slate-700 text-sm" />
          </div>
          <div class="sm:col-span-2">
            <label class="block text-xs font-semibold mb-1 text-amber-500">Ciri Fisik (Kunci Konsistensi Visual AI)</label>
            <textarea id="char-physical" rows="2" placeholder="Bentuk wajah, warna kulit, gaya rambut, postur..." class="w-full px-3 py-2 rounded-xl bg-slate-100 dark:bg-studio-800 border border-amber-500/40 text-sm">${escapeHtml(existing?.physicalTraits || '')}</textarea>
          </div>
          <div class="sm:col-span-2">
            <label class="block text-xs font-semibold mb-1 text-amber-500">Gaya Pakaian (Kunci Konsistensi Visual AI)</label>
            <textarea id="char-clothing" rows="2" placeholder="Pakaian khas yang dikenakan karakter di serial..." class="w-full px-3 py-2 rounded-xl bg-slate-100 dark:bg-studio-800 border border-amber-500/40 text-sm">${escapeHtml(existing?.clothingStyle || '')}</textarea>
          </div>
        </div>

        <div class="flex justify-end gap-2.5 mt-5">
          <button onclick="closeModal()" class="px-4 py-2.5 rounded-xl bg-slate-200 dark:bg-studio-800 text-xs sm:text-sm font-semibold">Batal</button>
          <button onclick="saveCharacterForm('${existing ? existing.id : ''}')" class="px-5 py-2.5 rounded-xl bg-amber-500 hover:bg-amber-400 text-slate-950 text-xs sm:text-sm font-bold">Simpan Karakter</button>
        </div>
      `);
    }

    function saveCharacterForm(charId) {
      const name = document.getElementById('char-name')?.value.trim();
      if (!name) {
        showToast('Nama karakter wajib diisi.', 'warning');
        return;
      }

      const proj = getActiveProject();
      const payload = {
        name,
        age: document.getElementById('char-age')?.value.trim() || '25 Tahun',
        gender: document.getElementById('char-gender')?.value || 'Laki-laki',
        role: document.getElementById('char-role')?.value.trim() || 'Tokoh Pendukung',
        personality: document.getElementById('char-personality')?.value.trim() || '',
        background: document.getElementById('char-background')?.value.trim() || '',
        relationships: document.getElementById('char-relationships')?.value.trim() || '',
        physicalTraits: document.getElementById('char-physical')?.value.trim() || '',
        clothingStyle: document.getElementById('char-clothing')?.value.trim() || ''
      };

      if (charId) {
        const idx = (proj.characters || []).findIndex(c => c.id === charId);
        if (idx !== -1) {
          proj.characters[idx] = { ...proj.characters[idx], ...payload };
        }
      } else {
        proj.characters.push({
          id: 'char_' + Date.now(),
          ...payload,
          imageUrl: ''
        });
      }

      saveState();
      closeModal();
      renderApp();
      showToast(`Karakter "${name}" berhasil disimpan!`, 'success');
    }

    function deleteCharacter(charId) {
      const proj = getActiveProject();
      proj.characters = (proj.characters || []).filter(c => c.id !== charId);
      saveState();
      renderApp();
      showToast('Karakter dihapus.', 'info');
    }

    function toggleDashboardGuide() {
      appState.showDashboardGuide = !appState.showDashboardGuide;
      renderApp();
    }

    function openUserGuideModal() {
      const steps = [
        {
          step: 'Langkah 1',
          title: 'Pilih Genre & Pengaturan Cerita',
          desc: 'Pilih dari 15 kartu genre drama atau tulis genre sendiri. Tentukan judul, tema, latar tempat, zaman, suasana, pesan moral, serta jumlah episode (3 hingga 20 episode). Gunakan tombol "Isi Otomatis dengan AI" jika butuh inspirasi cepat.',
          tab: 'setup',
          btnText: 'Buka Genre & Cerita'
        },
        {
          step: 'Langkah 2',
          title: 'Buat Karakter & Kunci Visual',
          desc: 'Klik "Buat Karakter Otomatis AI" atau tambah manual. Setiap tokoh memiliki ciri fisik, gaya pakaian, dan foto referensi AI agar wajah & busana tetap konsisten di semua episode.',
          tab: 'characters',
          btnText: 'Buka Studio Karakter'
        },
        {
          step: 'Langkah 3',
          title: 'Susun Alur Cerita Berseri',
          desc: 'AI akan merangkai sinopsis lengkap, konflik utama, konflik tambahan, klimaks, plot twist, dan ringkasan Episode 1 sampai Episode terakhir yang saling terhubung.',
          tab: 'plot',
          btnText: 'Buka Alur Serial'
        },
        {
          step: 'Langkah 4',
          title: 'Tulis & Edit Naskah Episode',
          desc: 'Buat naskah lengkap per episode berisi adegan pembuka, dialog beremosi, gerakan kamera, musik latar, serta cliffhanger. Anda juga dapat memutar sulih suara AI atau mengedit naskah.',
          tab: 'script',
          btnText: 'Buka Naskah Episode'
        },
        {
          step: 'Langkah 5',
          title: 'Buat Poster, Ilustrasi & Ekspor',
          desc: 'Hasilkan poster utama serial, potret karakter, dan ilustrasi adegan dalam 6 pilihan gaya visual, lalu unduh hasilnya atau ekspor seluruh naskah produksi.',
          tab: 'visuals',
          btnText: 'Buka Studio Visual AI'
        }
      ];

      openModal(`
        <div class="flex items-center justify-between mb-4">
          <div class="flex items-center gap-2.5">
            <div class="w-10 h-10 rounded-xl bg-amber-500/15 text-amber-500 flex items-center justify-center">
              <i data-lucide="book-open-check" class="w-5 h-5"></i>
            </div>
            <div>
              <h3 class="font-serif font-bold text-xl">Petunjuk Penggunaan DRAMA STUDIO AI</h3>
              <p class="text-xs text-slate-500 dark:text-slate-400">Ikuti 5 langkah mudah berikut untuk memproduksi serial drama Anda</p>
            </div>
          </div>
          <button onclick="closeModal()" class="p-1.5 rounded-lg hover:bg-slate-100 dark:hover:bg-studio-800 text-slate-400">
            <i data-lucide="x" class="w-5 h-5"></i>
          </button>
        </div>

        <div class="space-y-3 max-h-[65vh] overflow-y-auto pr-1">
          ${steps.map(s => `
            <div class="p-4 rounded-2xl bg-slate-100/80 dark:bg-studio-800/80 border border-slate-200 dark:border-slate-700/80 flex flex-col sm:flex-row sm:items-center justify-between gap-3">
              <div class="space-y-1">
                <span class="inline-block text-[10px] font-bold uppercase tracking-wider px-2 py-0.5 rounded-md bg-amber-500/20 text-amber-600 dark:text-amber-300">${s.step}</span>
                <h4 class="font-bold text-sm text-slate-900 dark:text-white">${s.title}</h4>
                <p class="text-xs text-slate-600 dark:text-slate-300 leading-relaxed">${s.desc}</p>
              </div>
              <button onclick="closeModal(); navigateTo('${s.tab}')" class="shrink-0 px-3.5 py-2 rounded-xl bg-amber-500 hover:bg-amber-400 text-slate-950 font-bold text-xs transition-colors">
                ${s.btnText}
              </button>
            </div>
          `).join('')}
        </div>
      `);
    }

    /**
     * =========================================================================
     * 9. RENDER HALAMAN UTAMA (DASHBOARD)
     * =========================================================================
     */
    function renderDashboardView() {
      const proj = getActiveProject();
      const allChars = proj.characters || [];
      const allPosters = (proj.gallery || []).filter(g => g.category === 'Poster utama serial' || g.imageUrl);
      const episodesList = proj.storyArc?.episodes || [];

      return `
        <div class="space-y-8 animate-fade-in">
          <!-- Hero Banner -->
          <section class="relative overflow-hidden rounded-3xl bg-gradient-to-br from-slate-900 via-studio-900 to-amber-950/60 border border-amber-500/25 p-6 sm:p-10 text-white shadow-2xl">
            <div class="absolute -top-24 -right-24 w-72 h-72 rounded-full bg-amber-500/15 blur-3xl pointer-events-none"></div>
            <div class="relative z-10 max-w-3xl space-y-4">
              <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-amber-500/15 border border-amber-500/30 text-amber-300 text-xs font-semibold">
                <i data-lucide="sparkles" class="w-3.5 h-3.5"></i>
                <span>DRAMA STUDIO AI • STUDIO KREATIF SERIAL DRAMA</span>
              </div>
              <h1 class="font-serif font-extrabold text-2xl sm:text-4xl lg:text-5xl leading-tight tracking-tight">
                Wujudkan Ide Ceritamu Menjadi Serial Drama.
              </h1>
              <p class="text-sm sm:text-base text-slate-300 leading-relaxed max-w-2xl">
                Rancang konsep serial drama lengkap mulai dari pemilihan genre, karakter dengan konsistensi visual, alur cerita berseri yang saling terhubung, naskah dialog siap produksi, hingga poster sinematik dalam satu studio terpadu.
              </p>
              <div class="flex flex-wrap items-center gap-3 pt-2">
                <button onclick="openNewProjectModal()" class="px-5 py-3 rounded-2xl bg-amber-500 hover:bg-amber-400 text-slate-950 font-bold text-sm flex items-center gap-2 shadow-lg shadow-amber-500/25 transition-all">
                  <i data-lucide="clapperboard" class="w-4 h-4"></i>
                  <span>Mulai Membuat Drama</span>
                </button>
                <button onclick="navigateTo('setup')" class="px-5 py-3 rounded-2xl bg-white/10 hover:bg-white/20 text-white border border-white/15 font-semibold text-sm flex items-center gap-2 backdrop-blur-md transition-all">
                  <i data-lucide="play" class="w-4 h-4 text-amber-400"></i>
                  <span>Lanjutkan Proyek (${escapeHtml(proj.settings.title)})</span>
                </button>
                <button onclick="openUserGuideModal()" class="px-4 py-3 rounded-2xl bg-slate-800/80 hover:bg-slate-800 text-amber-300 border border-slate-700 font-semibold text-sm flex items-center gap-2 transition-all">
                  <i data-lucide="help-circle" class="w-4 h-4"></i>
                  <span>Cara Penggunaan</span>
                </button>
              </div>
            </div>
          </section>

          <!-- Langkah-Langkah Penggunaan Studio -->
          <section class="rounded-3xl bg-white dark:bg-studio-900 border border-slate-200 dark:border-slate-800 p-5 sm:p-6 shadow-sm">
            <div class="flex items-center justify-between gap-3 mb-4">
              <div class="flex items-center gap-2.5">
                <div class="w-9 h-9 rounded-xl bg-amber-500/15 text-amber-500 flex items-center justify-center">
                  <i data-lucide="compass" class="w-5 h-5"></i>
                </div>
                <div>
                  <h2 class="font-serif font-bold text-lg sm:text-xl">Langkah-Langkah Membuat Serial Drama</h2>
                  <p class="text-xs text-slate-500 dark:text-slate-400">Alur kerja studio dari ide mentah menjadi naskah & visual siap produksi</p>
                </div>
              </div>
              <button onclick="toggleDashboardGuide()" class="text-xs font-semibold text-amber-500 hover:underline">
                ${appState.showDashboardGuide ? 'Sembunyikan' : 'Tampilkan Langkah'}
              </button>
            </div>

            ${appState.showDashboardGuide ? `
              <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-5 gap-3">
                ${[
                  { no: '01', title: 'Genre & Cerita', desc: 'Pilih 15 genre atau tulis sendiri, lalu atur sinopsis & jumlah episode.', tab: 'setup' },
                  { no: '02', title: 'Buat Karakter', desc: 'Rancang tokoh beserta ciri fisik & pakaian konsisten.', tab: 'characters' },
                  { no: '03', title: 'Alur Serial', desc: 'Susun konflik utama, plot twist, dan alur tiap episode terhubung.', tab: 'plot' },
                  { no: '04', title: 'Naskah Episode', desc: 'Hasilkan dialog beremosi, arahan kamera, dan audio suara AI.', tab: 'script' },
                  { no: '05', title: 'Studio Visual AI', desc: 'Buat poster serial, foto tokoh, dan ilustrasi setiap adegan.', tab: 'visuals' }
                ].map(item => `
                  <button onclick="navigateTo('${item.tab}')" class="text-left p-4 rounded-2xl bg-slate-50 dark:bg-studio-850 hover:border-amber-500/50 border border-slate-200 dark:border-slate-800 transition-all group">
                    <div class="flex items-center justify-between mb-2">
                      <span class="font-mono text-xs font-bold px-2 py-0.5 rounded-md bg-amber-500/15 text-amber-500">LANGKAH ${item.no}</span>
                      <i data-lucide="arrow-up-right" class="w-4 h-4 text-slate-400 group-hover:text-amber-500 transition-colors"></i>
                    </div>
                    <h3 class="font-bold text-sm mb-1 group-hover:text-amber-500 transition-colors">${item.title}</h3>
                    <p class="text-xs text-slate-500 dark:text-slate-400 leading-relaxed">${item.desc}</p>
                  </button>
                `).join('')}
              </div>
            ` : ''}
          </section>

          <!-- Drama yang Pernah Dibuat -->
          <section class="space-y-4">
            <div class="flex items-center justify-between">
              <h2 class="font-serif font-bold text-xl flex items-center gap-2">
                <i data-lucide="film" class="w-5 h-5 text-amber-500"></i>
                <span>Drama yang Pernah Dibuat</span>
              </h2>
              <button onclick="openNewProjectModal()" class="text-xs font-semibold text-amber-500 hover:underline">+ Tambah Proyek</button>
            </div>
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
              ${appState.projects.map(p => {
                const isSelected = p.id === proj.id;
                return `
                  <div class="rounded-3xl bg-white dark:bg-studio-900 border ${isSelected ? 'border-amber-500/60 ring-1 ring-amber-500/30' : 'border-slate-200 dark:border-slate-800'} p-5 flex flex-col justify-between gap-4 shadow-sm">
                    <div class="space-y-2">
                      <div class="flex items-center justify-between gap-2">
                        <span class="text-[11px] font-semibold px-2.5 py-0.5 rounded-full bg-amber-500/15 text-amber-600 dark:text-amber-300">
                          ${escapeHtml(p.customGenre || p.genre)}
                        </span>
                        <span class="text-[11px] text-slate-400">${p.settings.episodeCount} Episode</span>
                      </div>
                      <h3 class="font-serif font-bold text-lg text-slate-900 dark:text-white">${escapeHtml(p.settings.title)}</h3>
                      <p class="text-xs text-slate-600 dark:text-slate-400 line-clamp-3 leading-relaxed">
                        ${escapeHtml(p.settings.synopsis || 'Belum ada sinopsis cerita.')}
                      </p>
                    </div>
                    <div class="flex items-center justify-between pt-3 border-t border-slate-100 dark:border-slate-800">
                      <span class="text-[11px] text-slate-400">${(p.characters || []).length} Karakter • ${Object.keys(p.scripts || {}).length} Naskah</span>
                      <button onclick="selectProject('${p.id}'); navigateTo('setup');" class="px-3.5 py-1.5 rounded-xl bg-amber-500 hover:bg-amber-400 text-slate-950 font-bold text-xs transition-colors">
                        Lanjutkan Proyek
                      </button>
                    </div>
                  </div>
                `;
              }).join('')}
            </div>
          </section>

          <!-- Grid 3 Kolom: Koleksi Karakter, Koleksi Poster, Episode Terbaru -->
          <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
            <!-- Koleksi Karakter -->
            <section class="rounded-3xl bg-white dark:bg-studio-900 border border-slate-200 dark:border-slate-800 p-5 space-y-4">
              <div class="flex items-center justify-between">
                <h2 class="font-serif font-bold text-lg flex items-center gap-2">
                  <i data-lucide="users" class="w-4 h-4 text-amber-500"></i>
                  <span>Koleksi Karakter</span>
                </h2>
                <button onclick="navigateTo('characters')" class="text-xs font-semibold text-amber-500 hover:underline">Kelola</button>
              </div>
              <div class="space-y-3">
                ${allChars.length === 0
                  ? `<p class="text-xs text-slate-500 py-4 text-center">Belum ada karakter pada proyek ini.</p>`
                  : allChars.slice(0, 4).map(c => `
                    <div onclick="navigateTo('characters')" class="flex items-center gap-3 p-2.5 rounded-2xl bg-slate-50 dark:bg-studio-850 hover:border-amber-500/40 border border-transparent cursor-pointer transition-all">
                      ${c.imageUrl
                        ? `<img src="${c.imageUrl}" alt="${escapeHtml(c.name)}" class="w-12 h-12 rounded-xl object-cover shrink-0 border border-amber-500/30" />`
                        : `<div class="w-12 h-12 rounded-xl bg-gradient-to-br from-amber-500/20 to-orange-600/20 text-amber-500 font-serif font-bold text-lg flex items-center justify-center shrink-0">${escapeHtml(c.name.charAt(0))}</div>`
                      }
                      <div class="min-w-0 flex-1">
                        <h4 class="font-bold text-sm truncate">${escapeHtml(c.name)}</h4>
                        <p class="text-[11px] text-amber-500 font-medium truncate">${escapeHtml(c.role)} • ${escapeHtml(c.age)}</p>
                        <p class="text-[11px] text-slate-500 dark:text-slate-400 truncate">${escapeHtml(c.personality)}</p>
                      </div>
                    </div>
                  `).join('')
                }
              </div>
            </section>

            <!-- Koleksi Poster -->
            <section class="rounded-3xl bg-white dark:bg-studio-900 border border-slate-200 dark:border-slate-800 p-5 space-y-4">
              <div class="flex items-center justify-between">
                <h2 class="font-serif font-bold text-lg flex items-center gap-2">
                  <i data-lucide="image" class="w-4 h-4 text-amber-500"></i>
                  <span>Koleksi Poster</span>
                </h2>
                <button onclick="navigateTo('visuals')" class="text-xs font-semibold text-amber-500 hover:underline">Studio Visual</button>
              </div>
              <div class="grid grid-cols-2 gap-3">
                ${allPosters.slice(0, 4).map(item => `
                  <div onclick="${item.imageUrl ? `openImagePreviewModal('${item.id}')` : `navigateTo('visuals')`}" class="group relative rounded-2xl overflow-hidden aspect-[3/4] bg-gradient-to-br from-amber-900/50 via-studio-850 to-slate-950 border border-slate-700/60 cursor-pointer">
                    ${item.imageUrl
                      ? `<img src="${item.imageUrl}" alt="${escapeHtml(item.title)}" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-300" />`
                      : `<div class="w-full h-full p-3 flex flex-col justify-between">
                          <span class="text-[10px] uppercase tracking-wider text-amber-400 font-bold">Konsep Poster</span>
                          <div>
                            <p class="font-serif font-bold text-xs text-white leading-snug mb-1">${escapeHtml(proj.settings.title)}</p>
                            <span class="inline-block text-[10px] px-2 py-0.5 rounded bg-amber-500 text-slate-950 font-bold">Render AI</span>
                          </div>
                        </div>`
                    }
                  </div>
                `).join('')}
              </div>
            </section>

            <!-- Episode Terbaru -->
            <section class="rounded-3xl bg-white dark:bg-studio-900 border border-slate-200 dark:border-slate-800 p-5 space-y-4">
              <div class="flex items-center justify-between">
                <h2 class="font-serif font-bold text-lg flex items-center gap-2">
                  <i data-lucide="list-video" class="w-4 h-4 text-amber-500"></i>
                  <span>Episode Terbaru</span>
                </h2>
                <button onclick="navigateTo('script')" class="text-xs font-semibold text-amber-500 hover:underline">Buka Naskah</button>
              </div>
              <div class="space-y-2.5">
                ${episodesList.length === 0
                  ? `<p class="text-xs text-slate-500 py-4 text-center">Belum ada daftar episode. Susun alur serial terlebih dahulu.</p>`
                  : episodesList.slice(0, 5).map(ep => {
                    const hasScript = Boolean(proj.scripts?.[ep.episodeNumber]);
                    return `
                      <div onclick="appState.selectedEpisodeNumber = ${ep.episodeNumber}; navigateTo('script');" class="p-3 rounded-2xl bg-slate-50 dark:bg-studio-850 hover:border-amber-500/40 border border-transparent cursor-pointer transition-all">
                        <div class="flex items-center justify-between gap-2 mb-1">
                          <span class="text-[11px] font-bold text-amber-500">EPISODE ${ep.episodeNumber}</span>
                          <span class="text-[10px] px-2 py-0.5 rounded-full ${hasScript ? 'bg-emerald-500/15 text-emerald-400' : 'bg-slate-200 dark:bg-studio-800 text-slate-400'}">
                            ${hasScript ? 'Naskah Siap' : 'Garis Besar'}
                          </span>
                        </div>
                        <h4 class="font-bold text-xs sm:text-sm truncate">${escapeHtml(ep.title)}</h4>
                        <p class="text-[11px] text-slate-500 dark:text-slate-400 line-clamp-1 mt-0.5">${escapeHtml(ep.summary)}</p>
                      </div>
                    `;
                  }).join('')
                }
              </div>
            </section>
          </div>
        </div>
      `;
    }

    /**
     * =========================================================================
     * 10. RENDER PILIHAN GENRE & PENGATURAN CERITA
     * =========================================================================
     */
    function selectGenre(genreName) {
      const proj = getActiveProject();
      proj.genre = genreName;
      proj.customGenre = '';
      saveState();
      renderApp();
    }

    function updateCustomGenre(val) {
      const proj = getActiveProject();
      proj.customGenre = val;
      saveState();
    }

    function updateSettingField(field, value) {
      const proj = getActiveProject();
      if (field === 'episodeCount') {
        proj.settings[field] = Math.max(1, Math.min(50, parseInt(value, 10) || 5));
      } else {
        proj.settings[field] = value;
      }
      saveState();
      if (field === 'title') {
        updateHeaderAndNav();
      }
    }

    function renderSetupView() {
      const proj = getActiveProject();
      const s = proj.settings;
      const presetCounts = [3, 5, 10, 15, 20];
      const isCustomCount = !presetCounts.includes(Number(s.episodeCount));

      return `
        <div class="space-y-8 animate-fade-in">
          <!-- Header Section -->
          <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4">
            <div>
              <span class="text-xs font-bold uppercase tracking-wider text-amber-500">Tahap 1 • Fondasi Kreatif</span>
              <h1 class="font-serif font-bold text-2xl sm:text-3xl">Pilihan Genre & Pengaturan Cerita</h1>
              <p class="text-xs sm:text-sm text-slate-500 dark:text-slate-400 mt-1">Pilih nuansa drama yang Anda inginkan, lalu lengkapi parameter produksi serial.</p>
            </div>
            <button onclick="aiAutoFillStorySettings()" class="px-4 py-3 rounded-2xl bg-gradient-to-r from-amber-500 to-orange-500 hover:from-amber-400 hover:to-orange-400 text-slate-950 font-bold text-xs sm:text-sm flex items-center justify-center gap-2 shadow-lg shadow-amber-500/20">
              <i data-lucide="sparkles" class="w-4 h-4"></i>
              <span>Isi Otomatis Konsep Cerita AI</span>
            </button>
          </div>

          <!-- B. PILIHAN GENRE DRAMA (15 Kartu Bergambar + Genre Sendiri) -->
          <section class="space-y-4">
            <h2 class="font-serif font-bold text-lg flex items-center gap-2">
              <i data-lucide="layers" class="w-5 h-5 text-amber-500"></i>
              <span>Pilih Genre Drama</span>
            </h2>

            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-5 gap-3">
              ${GENRE_LIST.map(g => {
                const isSelected = !proj.customGenre && proj.genre === g.name;
                return `
                  <button onclick="selectGenre('${escapeHtml(g.name)}')"
                    class="text-left rounded-2xl overflow-hidden border transition-all flex flex-col justify-between ${
                      isSelected
                        ? 'border-amber-400 ring-2 ring-amber-500/40 scale-[1.01]'
                        : 'border-slate-200 dark:border-slate-800 hover:border-amber-500/40'
                    } bg-white dark:bg-studio-900">
                    <div class="h-16 bg-gradient-to-br ${g.gradient} p-3 flex items-center justify-between text-white">
                      <div class="w-8 h-8 rounded-xl bg-white/15 backdrop-blur-sm flex items-center justify-center">
                        <i data-lucide="${g.icon}" class="w-4 h-4"></i>
                      </div>
                      ${isSelected ? `<span class="text-[10px] font-bold px-2 py-0.5 rounded-full bg-amber-400 text-slate-950">Dipilih</span>` : ''}
                    </div>
                    <div class="p-3.5 flex-1">
                      <h3 class="font-bold text-xs sm:text-sm text-slate-900 dark:text-white mb-1">${escapeHtml(g.name)}</h3>
                      <p class="text-[11px] text-slate-500 dark:text-slate-400 leading-snug">${escapeHtml(g.desc)}</p>
                    </div>
                  </button>
                `;
              }).join('')}
            </div>

            <!-- Buat Genre Sendiri -->
            <div class="p-4 rounded-2xl bg-white dark:bg-studio-900 border border-slate-200 dark:border-slate-800 flex flex-col sm:flex-row sm:items-center gap-3">
              <div class="flex items-center gap-2 shrink-0">
                <i data-lucide="pen-tool" class="w-4 h-4 text-amber-500"></i>
                <span class="text-xs sm:text-sm font-bold">Buat Genre Sendiri:</span>
              </div>
              <input type="text" value="${escapeHtml(proj.customGenre)}" oninput="updateCustomGenre(this.value)"
                placeholder="Tulis kombinasi genre unik Anda, misal: Drama Misteri Kuliner Nusantara..."
                class="flex-1 px-3.5 py-2 rounded-xl bg-slate-100 dark:bg-studio-800 border border-slate-200 dark:border-slate-700 text-xs sm:text-sm focus:outline-none focus:border-amber-500" />
            </div>
          </section>

          <!-- C. PENGATURAN CERITA -->
          <section class="rounded-3xl bg-white dark:bg-studio-900 border border-slate-200 dark:border-slate-800 p-5 sm:p-7 space-y-5">
            <h2 class="font-serif font-bold text-lg flex items-center gap-2">
              <i data-lucide="sliders" class="w-5 h-5 text-amber-500"></i>
              <span>Pengaturan Detail Cerita</span>
            </h2>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
              <div>
                <label class="block text-xs font-semibold mb-1.5">Judul Drama</label>
                <input type="text" value="${escapeHtml(s.title)}" oninput="updateSettingField('title', this.value)" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-100 dark:bg-studio-800 border border-slate-200 dark:border-slate-700 text-sm focus:outline-none focus:border-amber-500" />
              </div>
              <div>
                <label class="block text-xs font-semibold mb-1.5">Tema Utama</label>
                <input type="text" value="${escapeHtml(s.theme)}" oninput="updateSettingField('theme', this.value)" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-100 dark:bg-studio-800 border border-slate-200 dark:border-slate-700 text-sm focus:outline-none focus:border-amber-500" />
              </div>
              <div class="md:col-span-2">
                <label class="block text-xs font-semibold mb-1.5">Sinopsis Cerita</label>
                <textarea rows="3" oninput="updateSettingField('synopsis', this.value)" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-100 dark:bg-studio-800 border border-slate-200 dark:border-slate-700 text-sm focus:outline-none focus:border-amber-500">${escapeHtml(s.synopsis)}</textarea>
              </div>
              <div>
                <label class="block text-xs font-semibold mb-1.5">Latar Tempat</label>
                <input type="text" value="${escapeHtml(s.settingPlace)}" oninput="updateSettingField('settingPlace', this.value)" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-100 dark:bg-studio-800 border border-slate-200 dark:border-slate-700 text-sm focus:outline-none focus:border-amber-500" />
              </div>
              <div>
                <label class="block text-xs font-semibold mb-1.5">Zaman Cerita</label>
                <input type="text" value="${escapeHtml(s.era)}" oninput="updateSettingField('era', this.value)" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-100 dark:bg-studio-800 border border-slate-200 dark:border-slate-700 text-sm focus:outline-none focus:border-amber-500" />
              </div>
              <div>
                <label class="block text-xs font-semibold mb-1.5">Suasana Cerita</label>
                <input type="text" value="${escapeHtml(s.mood)}" oninput="updateSettingField('mood', this.value)" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-100 dark:bg-studio-800 border border-slate-200 dark:border-slate-700 text-sm focus:outline-none focus:border-amber-500" />
              </div>
              <div>
                <label class="block text-xs font-semibold mb-1.5">Target Penonton</label>
                <select onchange="updateSettingField('audience', this.value)" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-100 dark:bg-studio-800 border border-slate-200 dark:border-slate-700 text-sm focus:outline-none focus:border-amber-500">
                  ${['Semua Umur / Keluarga', 'Remaja (13+)', 'Dewasa Muda (17+)', 'Dewasa (21+)'].map(opt =>
                    `<option value="${opt}" ${s.audience === opt ? 'selected' : ''}>${opt}</option>`
                  ).join('')}
                </select>
              </div>

              <!-- Pilihan Jumlah Episode: 3, 5, 10, 15, 20, atau Custom -->
              <div>
                <label class="block text-xs font-semibold mb-1.5">Jumlah Episode</label>
                <div class="flex flex-wrap items-center gap-2">
                  ${presetCounts.map(cnt => `
                    <button type="button" onclick="updateSettingField('episodeCount', ${cnt}); renderApp();"
                      class="px-3 py-2 rounded-xl text-xs font-bold border transition-all ${
                        Number(s.episodeCount) === cnt
                          ? 'bg-amber-500 text-slate-950 border-amber-500'
                          : 'bg-slate-100 dark:bg-studio-800 border-slate-200 dark:border-slate-700'
                      }">
                      ${cnt} Ep
                    </button>
                  `).join('')}
                  <div class="flex items-center gap-1.5">
                    <span class="text-xs text-slate-400">Custom:</span>
                    <input type="number" min="1" max="50" value="${s.episodeCount}" onchange="updateSettingField('episodeCount', this.value); renderApp();"
                      class="w-16 px-2.5 py-2 rounded-xl bg-slate-100 dark:bg-studio-800 border ${isCustomCount ? 'border-amber-500' : 'border-slate-200 dark:border-slate-700'} text-xs font-bold text-center" />
                  </div>
                </div>
              </div>

              <div>
                <label class="block text-xs font-semibold mb-1.5">Durasi Setiap Episode</label>
                <select onchange="updateSettingField('episodeDuration', this.value)" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-100 dark:bg-studio-800 border border-slate-200 dark:border-slate-700 text-sm focus:outline-none focus:border-amber-500">
                  ${['3–5 Menit (Drama Vertikal / Web Short)', '15 Menit (Web Series)', '30 Menit (Sitkom / Drama Pendek)', '45 Menit (Standar TV/Streaming)', '60 Menit (Drama Premium)'].map(opt =>
                    `<option value="${opt}" ${s.episodeDuration === opt ? 'selected' : ''}>${opt}</option>`
                  ).join('')}
                </select>
              </div>

              <div>
                <label class="block text-xs font-semibold mb-1.5">Gaya Penceritaan</label>
                <input type="text" value="${escapeHtml(s.narrativeStyle)}" oninput="updateSettingField('narrativeStyle', this.value)" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-100 dark:bg-studio-800 border border-slate-200 dark:border-slate-700 text-sm focus:outline-none focus:border-amber-500" />
              </div>
              <div>
                <label class="block text-xs font-semibold mb-1.5">Pesan Moral</label>
                <input type="text" value="${escapeHtml(s.moralMessage)}" oninput="updateSettingField('moralMessage', this.value)" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-100 dark:bg-studio-800 border border-slate-200 dark:border-slate-700 text-sm focus:outline-none focus:border-amber-500" />
              </div>
            </div>

            <div class="pt-3 flex justify-end">
              <button onclick="navigateTo('characters')" class="px-5 py-3 rounded-2xl bg-amber-500 hover:bg-amber-400 text-slate-950 font-bold text-sm flex items-center gap-2">
                <span>Lanjut ke Pembuatan Karakter</span>
                <i data-lucide="arrow-right" class="w-4 h-4"></i>
              </button>
            </div>
          </section>
        </div>
      `;
    }

    /**
     * =========================================================================
     * 11. RENDER PEMBUATAN KARAKTER & KONSISTENSI VISUAL
     * =========================================================================
     */
    function renderCharactersView() {
      const proj = getActiveProject();
      const chars = proj.characters || [];

      return `
        <div class="space-y-6 animate-fade-in">
          <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4">
            <div>
              <span class="text-xs font-bold uppercase tracking-wider text-amber-500">Tahap 2 • Pemeran & Konsistensi Wajah</span>
              <h1 class="font-serif font-bold text-2xl sm:text-3xl">Pembuatan Karakter Serial</h1>
              <p class="text-xs sm:text-sm text-slate-500 dark:text-slate-400 mt-1">Setiap karakter memiliki ciri fisik, gaya pakaian, dan foto referensi yang dikunci konsisten di seluruh episode.</p>
            </div>
            <div class="flex flex-wrap items-center gap-2.5">
              <button onclick="openCharacterModal()" class="px-4 py-2.5 rounded-2xl bg-slate-200 dark:bg-studio-800 hover:bg-slate-300 dark:hover:bg-studio-700 text-xs sm:text-sm font-bold flex items-center gap-1.5">
                <i data-lucide="user-plus" class="w-4 h-4"></i>
                <span>Tambah Karakter</span>
              </button>
              <button onclick="aiGenerateCharacters()" class="px-4 py-2.5 rounded-2xl bg-amber-500 hover:bg-amber-400 text-slate-950 text-xs sm:text-sm font-bold flex items-center gap-1.5 shadow-lg shadow-amber-500/20">
                <i data-lucide="sparkles" class="w-4 h-4"></i>
                <span>Buat Karakter Otomatis AI</span>
              </button>
            </div>
          </div>

          <!-- Banner Konsistensi Karakter -->
          <div class="p-4 rounded-2xl bg-amber-500/10 border border-amber-500/30 flex items-start gap-3 text-xs sm:text-sm">
            <i data-lucide="shield-check" class="w-5 h-5 text-amber-500 shrink-0 mt-0.5"></i>
            <div>
              <span class="font-bold text-amber-600 dark:text-amber-300">Sistem Konsistensi Visual Aktif:</span>
              <span class="text-slate-700 dark:text-slate-300"> Klik <strong>"Buat Foto Referensi AI"</strong> pada setiap karakter. Wajah, ciri fisik, dan gaya pakaian karakter akan otomatis dijadikan acuan visual saat membuat ilustrasi adegan di semua episode.</span>
            </div>
          </div>

          ${chars.length === 0 ? `
            <div class="rounded-3xl bg-white dark:bg-studio-900 border border-slate-200 dark:border-slate-800 p-10 text-center space-y-3">
              <i data-lucide="users" class="w-10 h-10 text-amber-500 mx-auto"></i>
              <h3 class="font-serif font-bold text-xl">Belum Ada Karakter</h3>
              <p class="text-xs sm:text-sm text-slate-500 max-w-md mx-auto">Klik tombol "Buat Karakter Otomatis AI" agar AI merancang jajaran pemeran yang sesuai dengan cerita Anda.</p>
            </div>
          ` : `
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-5">
              ${chars.map(c => `
                <div class="rounded-3xl bg-white dark:bg-studio-900 border border-slate-200 dark:border-slate-800 overflow-hidden flex flex-col justify-between shadow-sm">
                  <div>
                    <!-- Header Foto / Referensi Karakter -->
                    <div class="relative aspect-[4/3] bg-gradient-to-br from-slate-800 to-studio-950 flex items-center justify-center overflow-hidden">
                      ${c.imageUrl
                        ? `<img src="${c.imageUrl}" alt="${escapeHtml(c.name)}" class="w-full h-full object-cover" />`
                        : `<div class="text-center p-4">
                            <div class="w-16 h-16 rounded-2xl bg-amber-500/20 text-amber-400 font-serif font-bold text-3xl flex items-center justify-center mx-auto mb-2">${escapeHtml(c.name.charAt(0))}</div>
                            <span class="text-[11px] text-slate-400">Belum ada foto referensi AI</span>
                          </div>`
                      }
                      <div class="absolute top-3 left-3 flex items-center gap-1.5">
                        <span class="text-[10px] font-bold px-2.5 py-1 rounded-full bg-slate-950/80 text-amber-300 backdrop-blur-md border border-amber-500/30">
                          ${escapeHtml(c.role)}
                        </span>
                      </div>
                      <div class="absolute top-3 right-3 flex items-center gap-1.5">
                        <button onclick="openCharacterModal('${c.id}')" title="Edit Karakter" class="p-2 rounded-xl bg-slate-950/80 hover:bg-slate-900 text-white backdrop-blur-md">
                          <i data-lucide="pencil" class="w-3.5 h-3.5"></i>
                        </button>
                        <button onclick="deleteCharacter('${c.id}')" title="Hapus Karakter" class="p-2 rounded-xl bg-rose-950/80 hover:bg-rose-900 text-rose-200 backdrop-blur-md">
                          <i data-lucide="trash-2" class="w-3.5 h-3.5"></i>
                        </button>
                      </div>
                    </div>

                    <!-- Detail Profil Karakter -->
                    <div class="p-5 space-y-3">
                      <div>
                        <h3 class="font-serif font-bold text-xl">${escapeHtml(c.name)}</h3>
                        <p class="text-xs text-slate-500 dark:text-slate-400">${escapeHtml(c.age)} • ${escapeHtml(c.gender)}</p>
                      </div>

                      <div class="space-y-2 text-xs">
                        <div>
                          <span class="font-bold text-slate-700 dark:text-slate-200">Sifat & Kepribadian:</span>
                          <p class="text-slate-600 dark:text-slate-400">${escapeHtml(c.personality)}</p>
                        </div>
                        <div>
                          <span class="font-bold text-slate-700 dark:text-slate-200">Latar Belakang:</span>
                          <p class="text-slate-600 dark:text-slate-400">${escapeHtml(c.background)}</p>
                        </div>
                        <div>
                          <span class="font-bold text-slate-700 dark:text-slate-200">Hubungan Tokoh:</span>
                          <p class="text-slate-600 dark:text-slate-400">${escapeHtml(c.relationships)}</p>
                        </div>
                        <div class="p-2.5 rounded-xl bg-amber-500/5 border border-amber-500/20 space-y-1">
                          <p><span class="font-bold text-amber-500">Ciri Fisik:</span> <span class="text-slate-600 dark:text-slate-300">${escapeHtml(c.physicalTraits)}</span></p>
                          <p><span class="font-bold text-amber-500">Gaya Pakaian:</span> <span class="text-slate-600 dark:text-slate-300">${escapeHtml(c.clothingStyle)}</span></p>
                        </div>
                      </div>
                    </div>
                  </div>

                  <div class="p-4 pt-0">
                    <button onclick="aiGenerateSingleCharacterPortrait('${c.id}')" class="w-full py-2.5 px-3 rounded-xl bg-amber-500/15 hover:bg-amber-500 hover:text-slate-950 text-amber-600 dark:text-amber-300 border border-amber-500/30 font-bold text-xs flex items-center justify-center gap-1.5 transition-all">
                      <i data-lucide="camera" class="w-3.5 h-3.5"></i>
                      <span>${c.imageUrl ? 'Perbarui Foto Referensi AI' : 'Buat Foto Referensi AI'}</span>
                    </button>
                  </div>
                </div>
              `).join('')}
            </div>
          `}

          <div class="flex justify-end pt-2">
            <button onclick="navigateTo('plot')" class="px-5 py-3 rounded-2xl bg-amber-500 hover:bg-amber-400 text-slate-950 font-bold text-sm flex items-center gap-2">
              <span>Lanjut ke Generator Alur Cerita</span>
              <i data-lucide="arrow-right" class="w-4 h-4"></i>
            </button>
          </div>
        </div>
      `;
    }

    /**
     * =========================================================================
     * 12. RENDER GENERATOR ALUR CERITA BERSERI
     * =========================================================================
     */
    function renderPlotView() {
      const proj = getActiveProject();
      const arc = proj.storyArc;

      return `
        <div class="space-y-6 animate-fade-in">
          <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4">
            <div>
              <span class="text-xs font-bold uppercase tracking-wider text-amber-500">Tahap 3 • Struktur Dramatik Berseri</span>
              <h1 class="font-serif font-bold text-2xl sm:text-3xl">Generator Alur Cerita Serial</h1>
              <p class="text-xs sm:text-sm text-slate-500 dark:text-slate-400 mt-1">Alur cerita saling terhubung erat dari Episode 1 hingga Episode ${proj.settings.episodeCount}.</p>
            </div>
            <button onclick="aiGenerateStoryArc()" class="px-4 py-3 rounded-2xl bg-amber-500 hover:bg-amber-400 text-slate-950 font-bold text-xs sm:text-sm flex items-center justify-center gap-2 shadow-lg shadow-amber-500/20">
              <i data-lucide="sparkles" class="w-4 h-4"></i>
              <span>Buat Alur Cerita Lengkap AI (${proj.settings.episodeCount} Ep)</span>
            </button>
          </div>

          ${!arc ? `
            <div class="rounded-3xl bg-white dark:bg-studio-900 border border-slate-200 dark:border-slate-800 p-10 text-center space-y-3">
              <i data-lucide="git-branch" class="w-10 h-10 text-amber-500 mx-auto"></i>
              <h3 class="font-serif font-bold text-xl">Alur Serial Belum Disusun</h3>
              <p class="text-xs sm:text-sm text-slate-500 max-w-md mx-auto">Klik tombol di atas agar AI menyusun konflik utama, klimaks, plot twist, dan rincian alur tiap episode.</p>
            </div>
          ` : `
            <!-- Struktur Inti Serial -->
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
              <div class="md:col-span-2 rounded-3xl bg-white dark:bg-studio-900 border border-slate-200 dark:border-slate-800 p-5 space-y-2">
                <span class="text-xs font-bold text-amber-500 uppercase tracking-wider">Ide Cerita & Sinopsis Lengkap</span>
                <p class="font-semibold text-sm text-slate-900 dark:text-white">${escapeHtml(arc.storyIdea)}</p>
                <p class="text-xs sm:text-sm text-slate-600 dark:text-slate-300 leading-relaxed">${escapeHtml(arc.fullSynopsis)}</p>
              </div>

              ${[
                { label: 'Konflik Utama', val: arc.mainConflict, icon: 'zap' },
                { label: 'Konflik Tambahan (Subplot)', val: arc.subConflicts, icon: 'layers' },
                { label: 'Klimaks Puncak', val: arc.climax, icon: 'flame' },
                { label: 'Plot Twist Mengejutkan', val: arc.plotTwist, icon: 'shuffle' },
                { label: 'Penyelesaian Cerita', val: arc.resolution, icon: 'check-circle' },
                { label: 'Dinamika & Hubungan Antar Tokoh', val: arc.characterDynamics, icon: 'users' }
              ].map(box => `
                <div class="rounded-2xl bg-white dark:bg-studio-900 border border-slate-200 dark:border-slate-800 p-4 space-y-1.5">
                  <div class="flex items-center gap-2 text-amber-500 font-bold text-xs uppercase tracking-wider">
                    <i data-lucide="${box.icon}" class="w-4 h-4"></i>
                    <span>${box.label}</span>
                  </div>
                  <p class="text-xs sm:text-sm text-slate-600 dark:text-slate-300 leading-relaxed">${escapeHtml(box.val)}</p>
                </div>
              `).join('')}
            </div>

            <!-- Timeline Alur Tiap Episode -->
            <div class="space-y-3 pt-2">
              <h2 class="font-serif font-bold text-xl flex items-center gap-2">
                <i data-lucide="list-ordered" class="w-5 h-5 text-amber-500"></i>
                <span>Alur Cerita Setiap Episode (Saling Terhubung)</span>
              </h2>
              <div class="space-y-3">
                ${(arc.episodes || []).map(ep => {
                  const hasScript = Boolean(proj.scripts?.[ep.episodeNumber]);
                  return `
                    <div class="rounded-2xl bg-white dark:bg-studio-900 border border-slate-200 dark:border-slate-800 p-4 sm:p-5 flex flex-col lg:flex-row lg:items-center justify-between gap-4">
                      <div class="space-y-1.5 flex-1">
                        <div class="flex flex-wrap items-center gap-2">
                          <span class="px-2.5 py-0.5 rounded-lg bg-amber-500 text-slate-950 font-bold text-xs">Episode ${ep.episodeNumber}</span>
                          <h3 class="font-serif font-bold text-base sm:text-lg">${escapeHtml(ep.title)}</h3>
                        </div>
                        <p class="text-xs sm:text-sm text-slate-600 dark:text-slate-300 leading-relaxed">${escapeHtml(ep.summary)}</p>
                        <div class="grid grid-cols-1 sm:grid-cols-2 gap-2 pt-1 text-[11px]">
                          <div class="p-2 rounded-xl bg-slate-50 dark:bg-studio-850 text-slate-600 dark:text-slate-400">
                            <span class="font-bold text-amber-500">Benang Merah Utama:</span> ${escapeHtml(ep.connectionToMainArc)}
                          </div>
                          <div class="p-2 rounded-xl bg-slate-50 dark:bg-studio-850 text-slate-600 dark:text-slate-400">
                            <span class="font-bold text-rose-400">Cliffhanger Akhir:</span> ${escapeHtml(ep.cliffhanger)}
                          </div>
                        </div>
                      </div>
                      <div class="shrink-0">
                        <button onclick="appState.selectedEpisodeNumber = ${ep.episodeNumber}; navigateTo('script'); ${hasScript ? '' : `aiGenerateEpisodeScript(${ep.episodeNumber});`}"
                          class="w-full lg:w-auto px-4 py-2.5 rounded-xl ${hasScript ? 'bg-emerald-500/15 text-emerald-400 border border-emerald-500/30' : 'bg-amber-500 text-slate-950 font-bold'} text-xs font-semibold flex items-center justify-center gap-1.5">
                          <i data-lucide="${hasScript ? 'file-check' : 'pen-tool'}" class="w-4 h-4"></i>
                          <span>${hasScript ? 'Buka Naskah Episode' : 'Buat Naskah Episode'}</span>
                        </button>
                      </div>
                    </div>
                  `;
                }).join('')}
              </div>
            </div>
          `}
        </div>
      `;
    }

    /**
     * =========================================================================
     * 13. RENDER GENERATOR NASKAH EPISODE + EDIT + AUDIO AI
     * =========================================================================
     */
    function selectEpisodeTab(epNum) {
      appState.selectedEpisodeNumber = epNum;
      appState.isEditingScript = false;
      if (appState.audioBlobUrl) {
        URL.revokeObjectURL(appState.audioBlobUrl);
        appState.audioBlobUrl = null;
      }
      renderApp();
    }

    function toggleEditScriptMode() {
      appState.isEditingScript = !appState.isEditingScript;
      renderApp();
    }

    function saveManualScriptEdits(epNum) {
      const proj = getActiveProject();
      const script = proj.scripts?.[epNum];
      if (!script) return;

      script.title = document.getElementById('edit-ep-title')?.value || script.title;
      script.summary = document.getElementById('edit-ep-summary')?.value || script.summary;
      script.openingHook = document.getElementById('edit-ep-opening')?.value || script.openingHook;
      script.closingCliffhanger = document.getElementById('edit-ep-closing')?.value || script.closingCliffhanger;

      (script.scenes || []).forEach((sc, idx) => {
        const headingEl = document.getElementById(`edit-sc-heading-${idx}`);
        const locEl = document.getElementById(`edit-sc-loc-${idx}`);
        const narEl = document.getElementById(`edit-sc-nar-${idx}`);
        const camEl = document.getElementById(`edit-sc-cam-${idx}`);
        const visEl = document.getElementById(`edit-sc-vis-${idx}`);
        const musEl = document.getElementById(`edit-sc-mus-${idx}`);

        if (headingEl) sc.heading = headingEl.value;
        if (locEl) sc.locationDesc = locEl.value;
        if (narEl) sc.narration = narEl.value;
        if (camEl) sc.cameraDirection = camEl.value;
        if (visEl) sc.visualDesc = visEl.value;
        if (musEl) sc.musicAmbience = musEl.value;

        (sc.dialogue || []).forEach((dlg, dIdx) => {
          const emoEl = document.getElementById(`edit-dlg-emo-${idx}-${dIdx}`);
          const lineEl = document.getElementById(`edit-dlg-line-${idx}-${dIdx}`);
          if (emoEl) dlg.emotion = emoEl.value;
          if (lineEl) dlg.line = lineEl.value;
        });
      });

      appState.isEditingScript = false;
      saveState();
      renderApp();
      showToast(`Perubahan naskah Episode ${epNum} berhasil disimpan!`, 'success');
    }

    function goToNextEpisode(currentEp) {
      const proj = getActiveProject();
      const totalEps = Math.max(1, parseInt(proj.settings.episodeCount, 10) || 5);
      if (currentEp < totalEps) {
        selectEpisodeTab(currentEp + 1);
      } else {
        showToast('Anda sudah berada di episode terakhir serial ini!', 'info');
      }
    }

    function renderScriptView() {
      const proj = getActiveProject();
      const totalEps = Math.max(1, parseInt(proj.settings.episodeCount, 10) || 5);
      const epNum = Math.min(totalEps, Math.max(1, appState.selectedEpisodeNumber || 1));
      appState.selectedEpisodeNumber = epNum;

      const script = proj.scripts?.[epNum];
      const epOutline = (proj.storyArc?.episodes || []).find(e => e.episodeNumber === epNum);

      return `
        <div class="space-y-6 animate-fade-in">
          <!-- Episode Selector Pills -->
          <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-3">
            <div>
              <span class="text-xs font-bold uppercase tracking-wider text-amber-500">Tahap 4 • Ruang Penulis Skenario</span>
              <h1 class="font-serif font-bold text-2xl sm:text-3xl">Generator Naskah Episode</h1>
            </div>
            <div class="flex items-center gap-1.5 overflow-x-auto no-scrollbar pb-1">
              ${Array.from({ length: totalEps }, (_, i) => i + 1).map(n => {
                const isCurr = n === epNum;
                const done = Boolean(proj.scripts?.[n]);
                return `
                  <button onclick="selectEpisodeTab(${n})"
                    class="px-3.5 py-2 rounded-xl text-xs font-bold whitespace-nowrap flex items-center gap-1.5 border transition-all ${
                      isCurr
                        ? 'bg-amber-500 text-slate-950 border-amber-500'
                        : 'bg-white dark:bg-studio-900 border-slate-200 dark:border-slate-800 hover:border-amber-500/40'
                    }">
                    <span>Ep ${n}</span>
                    ${done ? `<span class="w-1.5 h-1.5 rounded-full ${isCurr ? 'bg-slate-950' : 'bg-emerald-400'}"></span>` : ''}
                  </button>
                `;
              }).join('')}
            </div>
          </div>

          <!-- Action Toolbar Naskah -->
          <div class="p-4 rounded-2xl bg-white dark:bg-studio-900 border border-slate-200 dark:border-slate-800 flex flex-wrap items-center gap-2">
            <button onclick="aiGenerateEpisodeScript(${epNum})" class="px-3.5 py-2 rounded-xl bg-amber-500 hover:bg-amber-400 text-slate-950 font-bold text-xs flex items-center gap-1.5">
              <i data-lucide="sparkles" class="w-3.5 h-3.5"></i>
              <span>Buat Episode</span>
            </button>
            <button onclick="aiModifyEpisodeScript(${epNum}, 'dialog')" class="px-3.5 py-2 rounded-xl bg-slate-100 dark:bg-studio-800 hover:bg-slate-200 dark:hover:bg-studio-700 text-xs font-semibold flex items-center gap-1.5">
              <i data-lucide="message-square-refresh" class="w-3.5 h-3.5 text-amber-500"></i>
              <span>Buat Ulang Dialog</span>
            </button>
            <button onclick="aiModifyEpisodeScript(${epNum}, 'extend')" class="px-3.5 py-2 rounded-xl bg-slate-100 dark:bg-studio-800 hover:bg-slate-200 dark:hover:bg-studio-700 text-xs font-semibold flex items-center gap-1.5">
              <i data-lucide="plus-circle" class="w-3.5 h-3.5 text-amber-500"></i>
              <span>Perpanjang Cerita</span>
            </button>
            <button onclick="aiModifyEpisodeScript(${epNum}, 'conflict')" class="px-3.5 py-2 rounded-xl bg-slate-100 dark:bg-studio-800 hover:bg-slate-200 dark:hover:bg-studio-700 text-xs font-semibold flex items-center gap-1.5">
              <i data-lucide="zap" class="w-3.5 h-3.5 text-amber-500"></i>
              <span>Ubah Konflik</span>
            </button>
            <button onclick="toggleEditScriptMode()" class="px-3.5 py-2 rounded-xl ${appState.isEditingScript ? 'bg-emerald-500 text-slate-950 font-bold' : 'bg-slate-100 dark:bg-studio-800 hover:bg-slate-200 dark:hover:bg-studio-700 font-semibold'} text-xs flex items-center gap-1.5">
              <i data-lucide="edit-3" class="w-3.5 h-3.5"></i>
              <span>${appState.isEditingScript ? 'Batal Edit' : 'Edit Naskah'}</span>
            </button>
            <button onclick="goToNextEpisode(${epNum})" class="px-3.5 py-2 rounded-xl bg-slate-100 dark:bg-studio-800 hover:bg-slate-200 dark:hover:bg-studio-700 text-xs font-semibold flex items-center gap-1.5 ml-auto">
              <span>Lanjutkan ke Episode Berikutnya</span>
              <i data-lucide="arrow-right" class="w-3.5 h-3.5 text-amber-500"></i>
            </button>
          </div>

          <!-- Pemutar Audio Naskah AI -->
          ${script ? `
            <div class="p-4 rounded-2xl bg-slate-100/90 dark:bg-studio-900 border border-slate-200 dark:border-slate-800 flex flex-col md:flex-row md:items-center justify-between gap-3">
              <div class="flex flex-wrap items-center gap-2.5">
                <div class="flex items-center gap-1.5 text-xs font-bold text-amber-500">
                  <i data-lucide="volume-2" class="w-4 h-4"></i>
                  <span>Sulih Suara Naskah AI:</span>
                </div>
                <select onchange="appState.selectedVoice = this.value" class="px-2.5 py-1.5 rounded-xl bg-white dark:bg-studio-800 border border-slate-200 dark:border-slate-700 text-xs font-semibold">
                  ${['Kore', 'Aoede', 'Puck', 'Charon'].map(v =>
                    `<option value="${v}" ${appState.selectedVoice === v ? 'selected' : ''}>Suara ${v}</option>`
                  ).join('')}
                </select>
                <button onclick="generateEpisodeAudio(${epNum})" class="px-3.5 py-1.5 rounded-xl bg-amber-500 hover:bg-amber-400 text-slate-950 font-bold text-xs flex items-center gap-1.5">
                  <i data-lucide="play" class="w-3.5 h-3.5"></i>
                  <span>Dengarkan Naskah</span>
                </button>
                ${appState.audioBlobUrl ? `
                  <button onclick="downloadEpisodeAudioWav(${epNum})" class="px-3 py-1.5 rounded-xl bg-slate-200 dark:bg-studio-800 text-xs font-semibold flex items-center gap-1">
                    <i data-lucide="download" class="w-3.5 h-3.5"></i>
                    <span>Unduh .WAV</span>
                  </button>
                ` : ''}
              </div>
              ${appState.audioBlobUrl ? `
                <audio controls src="${appState.audioBlobUrl}" class="h-9 w-full md:w-72"></audio>
              ` : ''}
            </div>
          ` : ''}

          <!-- Isi Naskah Episode -->
          ${!script ? `
            <div class="rounded-3xl bg-white dark:bg-studio-900 border border-slate-200 dark:border-slate-800 p-8 sm:p-12 text-center space-y-4">
              <span class="px-3 py-1 rounded-full bg-amber-500/15 text-amber-500 text-xs font-bold">EPISODE ${epNum}</span>
              <h3 class="font-serif font-bold text-2xl">${escapeHtml(epOutline?.title || `Episode ${epNum}`)}</h3>
              <p class="text-xs sm:text-sm text-slate-500 dark:text-slate-400 max-w-xl mx-auto leading-relaxed">
                ${escapeHtml(epOutline?.summary || 'Naskah untuk episode ini belum ditulis. Klik tombol "Buat Episode" untuk menghasilkan naskah lengkap.')}
              </p>
              <button onclick="aiGenerateEpisodeScript(${epNum})" class="px-6 py-3 rounded-2xl bg-amber-500 hover:bg-amber-400 text-slate-950 font-bold text-sm inline-flex items-center gap-2 shadow-lg shadow-amber-500/20">
                <i data-lucide="sparkles" class="w-4 h-4"></i>
                <span>Buat Naskah Episode ${epNum} Sekarang</span>
              </button>
            </div>
          ` : appState.isEditingScript ? `
            <!-- MODE EDIT MANUAL NASKAH -->
            <div class="rounded-3xl bg-white dark:bg-studio-900 border border-amber-500/40 p-5 sm:p-7 space-y-5">
              <div class="flex items-center justify-between">
                <h3 class="font-serif font-bold text-xl text-amber-500">Mode Edit Naskah Episode ${epNum}</h3>
                <button onclick="saveManualScriptEdits(${epNum})" class="px-5 py-2.5 rounded-xl bg-emerald-500 hover:bg-emerald-400 text-slate-950 font-bold text-xs sm:text-sm">Simpan Perubahan</button>
              </div>
              <div class="space-y-3">
                <div>
                  <label class="block text-xs font-bold mb-1">Judul Episode</label>
                  <input id="edit-ep-title" type="text" value="${escapeHtml(script.title)}" class="w-full px-3.5 py-2 rounded-xl bg-slate-100 dark:bg-studio-800 text-sm" />
                </div>
                <div>
                  <label class="block text-xs font-bold mb-1">Ringkasan Episode</label>
                  <textarea id="edit-ep-summary" rows="2" class="w-full px-3.5 py-2 rounded-xl bg-slate-100 dark:bg-studio-800 text-sm">${escapeHtml(script.summary)}</textarea>
                </div>
                <div>
                  <label class="block text-xs font-bold mb-1">Adegan Pembuka (Opening Hook)</label>
                  <textarea id="edit-ep-opening" rows="2" class="w-full px-3.5 py-2 rounded-xl bg-slate-100 dark:bg-studio-800 text-sm">${escapeHtml(script.openingHook)}</textarea>
                </div>
                ${(script.scenes || []).map((sc, idx) => `
                  <div class="p-4 rounded-2xl bg-slate-50 dark:bg-studio-850 border border-slate-200 dark:border-slate-700 space-y-2.5">
                    <input id="edit-sc-heading-${idx}" type="text" value="${escapeHtml(sc.heading)}" class="w-full px-3 py-1.5 rounded-lg bg-white dark:bg-studio-800 font-mono text-xs font-bold" />
                    <textarea id="edit-sc-loc-${idx}" rows="2" class="w-full px-3 py-1.5 rounded-lg bg-white dark:bg-studio-800 text-xs">${escapeHtml(sc.locationDesc)}</textarea>
                    <textarea id="edit-sc-nar-${idx}" rows="2" class="w-full px-3 py-1.5 rounded-lg bg-white dark:bg-studio-800 text-xs">${escapeHtml(sc.narration)}</textarea>
                    <div class="space-y-2">
                      ${(sc.dialogue || []).map((d, dIdx) => `
                        <div class="grid grid-cols-1 sm:grid-cols-3 gap-2">
                          <div class="text-xs font-bold py-1.5">${escapeHtml(d.character)}</div>
                          <input id="edit-dlg-emo-${idx}-${dIdx}" type="text" value="${escapeHtml(d.emotion)}" class="px-2.5 py-1.5 rounded-lg bg-white dark:bg-studio-800 text-xs" />
                          <input id="edit-dlg-line-${idx}-${dIdx}" type="text" value="${escapeHtml(d.line)}" class="px-2.5 py-1.5 rounded-lg bg-white dark:bg-studio-800 text-xs" />
                        </div>
                      `).join('')}
                    </div>
                    <input id="edit-sc-cam-${idx}" type="text" value="${escapeHtml(sc.cameraDirection)}" class="w-full px-3 py-1.5 rounded-lg bg-white dark:bg-studio-800 text-xs" />
                    <input id="edit-sc-vis-${idx}" type="text" value="${escapeHtml(sc.visualDesc)}" class="w-full px-3 py-1.5 rounded-lg bg-white dark:bg-studio-800 text-xs" />
                    <input id="edit-sc-mus-${idx}" type="text" value="${escapeHtml(sc.musicAmbience)}" class="w-full px-3 py-1.5 rounded-lg bg-white dark:bg-studio-800 text-xs" />
                  </div>
                `).join('')}
                <div>
                  <label class="block text-xs font-bold mb-1">Adegan Penutup (Cliffhanger)</label>
                  <textarea id="edit-ep-closing" rows="2" class="w-full px-3.5 py-2 rounded-xl bg-slate-100 dark:bg-studio-800 text-sm">${escapeHtml(script.closingCliffhanger)}</textarea>
                </div>
              </div>
              <div class="flex justify-end">
                <button onclick="saveManualScriptEdits(${epNum})" class="px-5 py-2.5 rounded-xl bg-emerald-500 hover:bg-emerald-400 text-slate-950 font-bold text-xs sm:text-sm">Simpan Perubahan</button>
              </div>
            </div>
          ` : `
            <!-- TAMPILAN BACA NASKAH PROFESIONAL -->
            <article class="rounded-3xl bg-white dark:bg-studio-900 border border-slate-200 dark:border-slate-800 p-5 sm:p-8 space-y-6 shadow-sm">
              <div class="border-b border-slate-200 dark:border-slate-800 pb-5 space-y-2">
                <div class="flex flex-wrap items-center justify-between gap-2">
                  <span class="px-3 py-1 rounded-full bg-amber-500/15 text-amber-500 font-bold text-xs">EPISODE ${script.episodeNumber}</span>
                  <button onclick="copyTextToClipboard(compileEpisodeText(${epNum}))" class="text-xs font-semibold text-slate-500 hover:text-amber-500 flex items-center gap-1">
                    <i data-lucide="copy" class="w-3.5 h-3.5"></i>
                    <span>Salin Naskah Episode</span>
                  </button>
                </div>
                <h2 class="font-serif font-extrabold text-2xl sm:text-3xl">${escapeHtml(script.title)}</h2>
                <p class="text-xs sm:text-sm text-slate-600 dark:text-slate-300 leading-relaxed">${escapeHtml(script.summary)}</p>
              </div>

              <!-- Adegan Pembuka -->
              <div class="p-4 rounded-2xl bg-amber-500/10 border border-amber-500/25 space-y-1">
                <span class="text-[11px] font-bold uppercase tracking-wider text-amber-500">Adegan Pembuka yang Menarik (Opening Hook)</span>
                <p class="text-xs sm:text-sm text-slate-800 dark:text-slate-200 leading-relaxed">${escapeHtml(script.openingHook)}</p>
              </div>

              <!-- Pembagian Adegan -->
              <div class="space-y-6">
                ${(script.scenes || []).map((sc, idx) => `
                  <div class="rounded-2xl bg-slate-50 dark:bg-studio-850 border border-slate-200 dark:border-slate-800 p-4 sm:p-6 space-y-4">
                    <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-2 border-b border-slate-200 dark:border-slate-700/70 pb-3">
                      <div>
                        <span class="font-mono text-xs font-bold text-amber-500">ADEGAN ${sc.sceneNumber || idx + 1} • ${escapeHtml(sc.heading)}</span>
                        <p class="text-xs text-slate-500 dark:text-slate-400 mt-0.5">${escapeHtml(sc.locationDesc)}</p>
                      </div>
                      <button onclick="aiGenerateSceneIllustration(${epNum}, ${idx})" class="shrink-0 px-3 py-1.5 rounded-xl bg-amber-500/15 hover:bg-amber-500 hover:text-slate-950 text-amber-600 dark:text-amber-300 border border-amber-500/30 font-bold text-xs flex items-center gap-1.5 transition-all">
                        <i data-lucide="image" class="w-3.5 h-3.5"></i>
                        <span>Ilustrasi Adegan AI</span>
                      </button>
                    </div>

                    <div class="flex flex-wrap items-center gap-1.5 text-[11px]">
                      <span class="font-bold text-slate-500">Karakter Tampil:</span>
                      ${(sc.charactersPresent || []).map(ch => `<span class="px-2 py-0.5 rounded-md bg-slate-200 dark:bg-studio-800 font-semibold">${escapeHtml(ch)}</span>`).join('')}
                    </div>

                    ${sc.narration ? `
                      <p class="text-xs sm:text-sm italic text-slate-600 dark:text-slate-300 border-l-2 border-amber-500 pl-3">
                        "${escapeHtml(sc.narration)}"
                      </p>
                    ` : ''}

                    <!-- Dialog Lengkap -->
                    <div class="space-y-2.5">
                      ${(sc.dialogue || []).map(d => `
                        <div class="p-3 rounded-xl bg-white dark:bg-studio-900/90 border border-slate-200/80 dark:border-slate-800">
                          <div class="flex items-center gap-2 mb-1">
                            <span class="font-bold text-xs sm:text-sm text-amber-600 dark:text-amber-400">${escapeHtml(d.character)}</span>
                            <span class="text-[11px] italic text-slate-400">(${escapeHtml(d.emotion)})</span>
                          </div>
                          <p class="text-xs sm:text-sm text-slate-800 dark:text-slate-100 leading-relaxed">${escapeHtml(d.line)}</p>
                        </div>
                      `).join('')}
                    </div>

                    <!-- Arahan Teknis Sutradara -->
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-2.5 pt-2 text-[11px]">
                      <div class="p-2.5 rounded-xl bg-white dark:bg-studio-900 border border-slate-200/70 dark:border-slate-800">
                        <span class="font-bold text-sky-400 block mb-0.5">Gerakan Kamera:</span>
                        <span class="text-slate-600 dark:text-slate-300">${escapeHtml(sc.cameraDirection)}</span>
                      </div>
                      <div class="p-2.5 rounded-xl bg-white dark:bg-studio-900 border border-slate-200/70 dark:border-slate-800">
                        <span class="font-bold text-emerald-400 block mb-0.5">Deskripsi Visual:</span>
                        <span class="text-slate-600 dark:text-slate-300">${escapeHtml(sc.visualDesc)}</span>
                      </div>
                      <div class="p-2.5 rounded-xl bg-white dark:bg-studio-900 border border-slate-200/70 dark:border-slate-800">
                        <span class="font-bold text-purple-400 block mb-0.5">Musik & Suasana:</span>
                        <span class="text-slate-600 dark:text-slate-300">${escapeHtml(sc.musicAmbience)}</span>
                      </div>
                    </div>
                  </div>
                `).join('')}
              </div>

              <!-- Adegan Penutup Cliffhanger -->
              <div class="p-4 rounded-2xl bg-rose-500/10 border border-rose-500/30 space-y-1">
                <span class="text-[11px] font-bold uppercase tracking-wider text-rose-400">Adegan Penutup (Cliffhanger Penasaran)</span>
                <p class="text-xs sm:text-sm text-slate-800 dark:text-slate-200 leading-relaxed">${escapeHtml(script.closingCliffhanger)}</p>
              </div>
            </article>
          `}
        </div>
      `;
    }

    /**
     * =========================================================================
     * 14. RENDER GENERATOR GAMBAR AI (STUDIO VISUAL)
     * =========================================================================
     */
    function renderVisualsView() {
      const proj = getActiveProject();
      const chars = proj.characters || [];
      const episodes = proj.storyArc?.episodes || [];
      const gallery = (proj.gallery || []).filter(g => g.imageUrl);

      const sceneOptions = [];
      Object.entries(proj.scripts || {}).forEach(([epKey, scObj]) => {
        (scObj.scenes || []).forEach((sc, idx) => {
          sceneOptions.push({
            val: `scene:${epKey}:${idx}`,
            label: `Ep ${epKey} - Adegan ${sc.sceneNumber || idx + 1}: ${sc.heading}`
          });
        });
      });

      return `
        <div class="space-y-6 animate-fade-in">
          <div>
            <span class="text-xs font-bold uppercase tracking-wider text-amber-500">Tahap 5 • Sinematografi & Poster</span>
            <h1 class="font-serif font-bold text-2xl sm:text-3xl">Generator Gambar AI Studio</h1>
            <p class="text-xs sm:text-sm text-slate-500 dark:text-slate-400 mt-1">Buat poster serial, foto karakter konsisten, ilustrasi adegan, latar lokasi, thumbnail, dan sampul episode.</p>
          </div>

          <!-- Form Studio Visual -->
          <div class="rounded-3xl bg-white dark:bg-studio-900 border border-slate-200 dark:border-slate-800 p-5 sm:p-6 space-y-4">
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4">
              <div>
                <label class="block text-xs font-semibold mb-1.5">Jenis Gambar Visual</label>
                <select id="vis-category" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-100 dark:bg-studio-800 border border-slate-200 dark:border-slate-700 text-xs sm:text-sm">
                  <option value="Poster utama serial">Poster utama serial</option>
                  <option value="Foto setiap karakter">Foto setiap karakter</option>
                  <option value="Ilustrasi setiap adegan">Ilustrasi setiap adegan</option>
                  <option value="Background lokasi">Background lokasi</option>
                  <option value="Gambar thumbnail episode">Gambar thumbnail episode</option>
                  <option value="Sampul setiap episode">Sampul setiap episode</option>
                </select>
              </div>

              <div>
                <label class="block text-xs font-semibold mb-1.5">Gaya Visual Sinematik</label>
                <select id="vis-style" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-100 dark:bg-studio-800 border border-slate-200 dark:border-slate-700 text-xs sm:text-sm">
                  ${VISUAL_STYLES.map(st => `<option value="${st.id}">${escapeHtml(st.name)}</option>`).join('')}
                </select>
              </div>

              <div>
                <label class="block text-xs font-semibold mb-1.5">Target Karakter / Episode / Adegan</label>
                <select id="vis-target" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-100 dark:bg-studio-800 border border-slate-200 dark:border-slate-700 text-xs sm:text-sm">
                  <option value="series">Seluruh Serial (${escapeHtml(proj.settings.title)})</option>
                  ${chars.map(c => `<option value="char:${c.id}">Karakter: ${escapeHtml(c.name)}</option>`).join('')}
                  ${episodes.map(ep => `<option value="ep:${ep.episodeNumber}">Episode ${ep.episodeNumber}: ${escapeHtml(ep.title)}</option>`).join('')}
                  ${sceneOptions.map(so => `<option value="${so.val}">${escapeHtml(so.label)}</option>`).join('')}
                </select>
              </div>

              <div>
                <label class="block text-xs font-semibold mb-1.5">Rasio Bingkai (Aspect Ratio)</label>
                <select id="vis-aspect" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-100 dark:bg-studio-800 border border-slate-200 dark:border-slate-700 text-xs sm:text-sm">
                  <option value="3:4">3:4 (Poster & Potret Karakter)</option>
                  <option value="16:9">16:9 (Layar Lebar & Thumbnail)</option>
                  <option value="9:16">9:16 (Vertikal / Story / Reels)</option>
                  <option value="1:1">1:1 (Persegi / Sampul)</option>
                </select>
              </div>
            </div>

            <div class="flex flex-col sm:flex-row gap-3">
              <input id="vis-custom-note" type="text" placeholder="Arahan tambahan sutradara (opsional), misal: Hujan rintik malam hari dengan cahaya lampu dermaga..."
                class="flex-1 px-3.5 py-2.5 rounded-xl bg-slate-100 dark:bg-studio-800 border border-slate-200 dark:border-slate-700 text-xs sm:text-sm" />
              <button onclick="aiGenerateVisualAsset()" class="px-6 py-2.5 rounded-xl bg-amber-500 hover:bg-amber-400 text-slate-950 font-bold text-xs sm:text-sm flex items-center justify-center gap-2 shadow-lg shadow-amber-500/20 shrink-0">
                <i data-lucide="sparkles" class="w-4 h-4"></i>
                <span>Buat Gambar AI</span>
              </button>
            </div>
          </div>

          <!-- Galeri Hasil Visual -->
          <section class="space-y-4">
            <h2 class="font-serif font-bold text-xl flex items-center gap-2">
              <i data-lucide="gallery-thumbnails" class="w-5 h-5 text-amber-500"></i>
              <span>Galeri Visual Produksi (${gallery.length})</span>
            </h2>

            ${gallery.length === 0 ? `
              <div class="rounded-3xl bg-white dark:bg-studio-900 border border-slate-200 dark:border-slate-800 p-10 text-center space-y-2">
                <i data-lucide="image" class="w-10 h-10 text-amber-500 mx-auto"></i>
                <h3 class="font-serif font-bold text-lg">Galeri Visual Masih Kosong</h3>
                <p class="text-xs text-slate-500 max-w-md mx-auto">Pilih jenis gambar dan gaya visual di atas, lalu klik "Buat Gambar AI" untuk merender poster atau ilustrasi adegan.</p>
              </div>
            ` : `
              <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-5">
                ${gallery.map(item => `
                  <div class="rounded-3xl bg-white dark:bg-studio-900 border border-slate-200 dark:border-slate-800 overflow-hidden flex flex-col justify-between shadow-sm">
                    <div onclick="openImagePreviewModal('${item.id}')" class="relative aspect-[4/3] bg-slate-950 overflow-hidden cursor-pointer group">
                      <img src="${item.imageUrl}" alt="${escapeHtml(item.title)}" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-300" />
                      <span class="absolute top-3 left-3 text-[10px] font-bold px-2.5 py-1 rounded-full bg-slate-950/80 text-amber-300 backdrop-blur-md">
                        ${escapeHtml(item.category)}
                      </span>
                    </div>
                    <div class="p-4 space-y-3">
                      <div>
                        <h3 class="font-bold text-sm line-clamp-1">${escapeHtml(item.title)}</h3>
                        <p class="text-[11px] text-slate-500 dark:text-slate-400">${escapeHtml(item.styleName)}</p>
                      </div>
                      <div class="flex items-center gap-2">
                        <button onclick="openImagePreviewModal('${item.id}')" class="flex-1 py-2 px-3 rounded-xl bg-slate-100 dark:bg-studio-800 hover:bg-slate-200 dark:hover:bg-studio-700 text-xs font-semibold">
                          Pratinjau
                        </button>
                        <button onclick="downloadImageById('${item.id}')" class="flex-1 py-2 px-3 rounded-xl bg-amber-500 hover:bg-amber-400 text-slate-950 text-xs font-bold flex items-center justify-center gap-1">
                          <i data-lucide="download" class="w-3.5 h-3.5"></i>
                          <span>Unduh</span>
                        </button>
                      </div>
                    </div>
                  </div>
                `).join('')}
              </div>
            `}
          </section>
        </div>
      `;
    }

    /**
     * =========================================================================
     * 15. EKSPOR DOKUMEN SERIAL & ROUTER UTAMA
     * =========================================================================
     */
    function compileEpisodeText(epNum) {
      const proj = getActiveProject();
      const sc = proj.scripts?.[epNum];
      if (!sc) return '';

      let out = `EPISODE ${sc.episodeNumber}: ${sc.title.toUpperCase()}\n`;
      out += `Ringkasan: ${sc.summary}\n`;
      out += `Adegan Pembuka: ${sc.openingHook}\n\n`;

      (sc.scenes || []).forEach((s, idx) => {
        out += `--- ADEGAN ${s.sceneNumber || idx + 1}: ${s.heading} ---\n`;
        out += `Lokasi: ${s.locationDesc}\n`;
        out += `Karakter: ${(s.charactersPresent || []).join(', ')}\n`;
        if (s.narration) out += `Narasi: ${s.narration}\n`;
        (s.dialogue || []).forEach(d => {
          out += `${d.character.toUpperCase()} (${d.emotion}): ${d.line}\n`;
        });
        out += `[Kamera: ${s.cameraDirection} | Visual: ${s.visualDesc} | Musik: ${s.musicAmbience}]\n\n`;
      });

      out += `Adegan Penutup (Cliffhanger): ${sc.closingCliffhanger}\n`;
      return out;
    }

    function compileFullSeriesDocument() {
      const proj = getActiveProject();
      const s = proj.settings;
      let doc = `====================================================\n`;
      doc += `DRAMA STUDIO AI – PAKET PRODUKSI SERIAL DRAMA\n`;
      doc += `====================================================\n\n`;
      doc += `JUDUL SERIAL : ${s.title}\n`;
      doc += `GENRE        : ${proj.customGenre || proj.genre}\n`;
      doc += `TEMA UTAMA   : ${s.theme}\n`;
      doc += `LATAR & ZAMAN: ${s.settingPlace} (${s.era})\n`;
      doc += `SUASANA      : ${s.mood}\n`;
      doc += `JUMLAH EP    : ${s.episodeCount} Episode (${s.episodeDuration})\n`;
      doc += `PESAN MORAL  : ${s.moralMessage}\n\n`;
      doc += `SINOPSIS CERITA:\n${s.synopsis}\n\n`;

      doc += `====================================================\n`;
      doc += `DAFTAR KARAKTER & KONSISTENSI VISUAL\n`;
      doc += `====================================================\n`;
      (proj.characters || []).forEach((c, i) => {
        doc += `${i + 1}. ${c.name} (${c.age}, ${c.gender}) - ${c.role}\n`;
        doc += `   Sifat      : ${c.personality}\n`;
        doc += `   Latar      : ${c.background}\n`;
        doc += `   Hubungan   : ${c.relationships}\n`;
        doc += `   Ciri Fisik : ${c.physicalTraits}\n`;
        doc += `   Pakaian    : ${c.clothingStyle}\n\n`;
      });

      if (proj.storyArc) {
        doc += `====================================================\n`;
        doc += `ALUR CERITA SERIAL BERSERI\n`;
        doc += `====================================================\n`;
        doc += `Konflik Utama   : ${proj.storyArc.mainConflict}\n`;
        doc += `Konflik Tambahan: ${proj.storyArc.subConflicts}\n`;
        doc += `Klimaks         : ${proj.storyArc.climax}\n`;
        doc += `Plot Twist      : ${proj.storyArc.plotTwist}\n`;
        doc += `Penyelesaian    : ${proj.storyArc.resolution}\n\n`;
        (proj.storyArc.episodes || []).forEach(ep => {
          doc += `Episode ${ep.episodeNumber} - ${ep.title}: ${ep.summary}\n`;
        });
        doc += `\n`;
      }

      doc += `====================================================\n`;
      doc += `NASKAH EPISODE YANG TELAH DIBUAT\n`;
      doc += `====================================================\n\n`;
      Object.keys(proj.scripts || {}).sort((a, b) => Number(a) - Number(b)).forEach(epKey => {
        doc += compileEpisodeText(Number(epKey)) + `\n`;
      });

      return doc;
    }

    function downloadFullSeriesTxt() {
      const proj = getActiveProject();
      const text = compileFullSeriesDocument();
      const blob = new Blob([text], { type: 'text/plain;charset=utf-8' });
      const url = URL.createObjectURL(blob);
      const safeName = (proj.settings.title || 'serial_drama').toLowerCase().replace(/[^a-z0-9]+/g, '_');

      const a = document.createElement('a');
      a.href = url;
      a.download = `${safeName}_produksi_lengkap.txt`;
      document.body.appendChild(a);
      a.click();
      document.body.removeChild(a);
      setTimeout(() => URL.revokeObjectURL(url), 5000);
      showToast('Dokumen lengkap serial berhasil diunduh (.TXT)!', 'success');
    }

    function copyFullSeriesText() {
      copyTextToClipboard(compileFullSeriesDocument());
    }

    function openExportModal() {
      const proj = getActiveProject();
      openModal(`
        <div class="flex items-center justify-between mb-4">
          <div class="flex items-center gap-2.5">
            <div class="w-9 h-9 rounded-xl bg-amber-500/15 text-amber-500 flex items-center justify-center">
              <i data-lucide="download" class="w-5 h-5"></i>
            </div>
            <div>
              <h3 class="font-serif font-bold text-xl">Ekspor Paket Produksi Serial</h3>
              <p class="text-xs text-slate-500 dark:text-slate-400">${escapeHtml(proj.settings.title)}</p>
            </div>
          </div>
          <button onclick="closeModal()" class="p-1.5 rounded-lg hover:bg-slate-100 dark:hover:bg-studio-800 text-slate-400">
            <i data-lucide="x" class="w-5 h-5"></i>
          </button>
        </div>
        <p class="text-xs sm:text-sm text-slate-600 dark:text-slate-300 mb-5 leading-relaxed">
          Unduh atau salin seluruh dokumen serial drama Anda (meliputi sinopsis, profil karakter lengkap, alur episode, serta seluruh naskah dialog yang telah dibuat).
        </p>
        <div class="flex flex-col sm:flex-row justify-end gap-2.5">
          <button onclick="copyFullSeriesText()" class="px-4 py-2.5 rounded-xl bg-slate-200 dark:bg-studio-800 hover:bg-slate-300 dark:hover:bg-studio-700 text-xs sm:text-sm font-semibold flex items-center justify-center gap-1.5">
            <i data-lucide="copy" class="w-4 h-4"></i>
            <span>Salin Semua Naskah</span>
          </button>
          <button onclick="downloadFullSeriesTxt()" class="px-5 py-2.5 rounded-xl bg-amber-500 hover:bg-amber-400 text-slate-950 text-xs sm:text-sm font-bold flex items-center justify-center gap-1.5">
            <i data-lucide="file-down" class="w-4 h-4"></i>
            <span>Unduh Dokumen (.TXT)</span>
          </button>
        </div>
      `);
    }

    function renderApp() {
      updateHeaderAndNav();
      const container = document.getElementById('app-content');
      if (!container) return;

      switch (appState.activeTab) {
        case 'dashboard':
          container.innerHTML = renderDashboardView();
          break;
        case 'setup':
          container.innerHTML = renderSetupView();
          break;
        case 'characters':
          container.innerHTML = renderCharactersView();
          break;
        case 'plot':
          container.innerHTML = renderPlotView();
          break;
        case 'script':
          container.innerHTML = renderScriptView();
          break;
        case 'visuals':
          container.innerHTML = renderVisualsView();
          break;
        default:
          container.innerHTML = renderDashboardView();
      }

      if (typeof lucide !== 'undefined') {
        lucide.createIcons();
      }
    }

    // Boot Application
    window.addEventListener('DOMContentLoaded', () => {
      initState();
      renderApp();
    });
  </script>
</body>
</html>
