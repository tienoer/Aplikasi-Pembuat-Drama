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

    // Daftar 15 Genre Utama + Kartu Visual SVG / Gradien
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
      { id: 'sosial', name: 'Drama sosial dan konflik masyarakat', desc: 'Ketimpangan keadilan, suara rakyat kecil, dan benturan kepentingan.', gradient: 'from-slate-700 to-zinc-900', icon: 'scale' },
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
      currentAudio: null,
      audioPlayer: null,
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

    async function callGeminiImage({ prompt, referenceImages = [], aspectRatio = '3:4', useAdvanced = true }) {
      const modelName = useAdvanced ? 'gemini-3.1-flash-image' : 'gemini-3.1-flash-lite-image';
      const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/${modelName}:generateContent?key=${apiKey}`;

      const parts = [{ text: prompt }];
      (referenceImages || []).forEach(dataUrl => {
        if (typeof dataUrl === 'string' && dataUrl.startsWith('data:image/')) {
          const match = dataUrl.match(/^data:(image\/[a-zA-Z0-9+.-]+);base64,(.+)$/);
          if (match) {
            parts.push({
              inlineData: {
                mimeType: match[1],
                data: match[2]
              }
            });
          }
        }
      });

      const payload = {
        contents: [{ role: 'user', parts }],
        generationConfig: {
          responseModalities: ['IMAGE'],
          imageConfig: { aspectRatio }
        }
      };

      const result = await fetchWithBackoff(apiUrl, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(payload)
      });

      const imgPart = result?.candidates?.[0]?.content?.parts?.find(p => p.inlineData);
      if (!imgPart || !imgPart.inlineData?.data) {
        throw new Error('Gambar tidak dihasilkan oleh AI.');
      }
      return `data:${imgPart.inlineData.mimeType || 'image/png'};base64,${imgPart.inlineData.data}`;
    }

    function base64ToArrayBuffer(base64) {
      const sanitized = String(base64 || '')
        .replace(/-/g, '+')
        .replace(/_/g, '/')
        .replace(/\s+/g, '');
      const binaryString = atob(sanitized);
      const len = binaryString.length;
      const bytes = new Uint8Array(len);
      for (let i = 0; i < len; i++) {
        bytes[i] = binaryString.charCodeAt(i);
      }
      return bytes.buffer;
    }

    function pcmToWav(pcm16, sampleRate = 24000) {
      const numChannels = 1;
      const bytesPerSample = 2;
      const blockAlign = numChannels * bytesPerSample;
      const byteRate = sampleRate * blockAlign;
      const dataSize = pcm16.length * bytesPerSample;
      const buffer = new ArrayBuffer(44 + dataSize);
      const view = new DataView(buffer);

      function writeStr(offset, str) {
        for (let i = 0; i < str.length; i++) {
          view.setUint8(offset + i, str.charCodeAt(i));
        }
      }

      writeStr(0, 'RIFF');
      view.setUint32(4, 36 + dataSize, true);
      writeStr(8, 'WAVE');
      writeStr(12, 'fmt ');
      view.setUint32(16, 16, true);
      view.setUint16(20, 1, true);
      view.setUint16(22, numChannels, true);
      view.setUint32(24, sampleRate, true);
      view.setUint32(28, byteRate, true);
      view.setUint16(32, blockAlign, true);
      view.setUint16(34, 16, true);
      writeStr(36, 'data');
      view.setUint32(40, dataSize, true);

      let offset = 44;
      for (let i = 0; i < pcm16.length; i++, offset += 2) {
        view.setInt16(offset, pcm16[i], true);
      }

      return new Blob([buffer], { type: 'audio/wav' });
    }

    async function callGeminiTTS(text, voiceName = 'Kore') {
      const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-tts:generateContent?key=${apiKey}`;
      const cleanText = String(text || '').replace(/\s+/g, ' ').trim().slice(0, 1200);
      const payload = {
        contents: [{
          parts: [{ text: `Bacakan naskah drama Indonesia berikut dengan intonasi emosional dan dramatis: ${cleanText}` }]
        }],
        generationConfig: {
          responseModalities: ["AUDIO"],
          speechConfig: {
            voiceConfig: {
              prebuiltVoiceConfig: { voiceName }
            }
          }
        },
        model: "gemini-2.5-flash-preview-tts"
      };

      const result = await fetchWithBackoff(apiUrl, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(payload)
      });

      const parts = result?.candidates?.[0]?.content?.parts || [];
      const part = parts.find(p => p.inlineData && p.inlineData.data);
      const audioData = part?.inlineData?.data;
      const mimeType = part?.inlineData?.mimeType || 'audio/L16;rate=24000';

      if (!audioData) {
        throw new Error('Data audio tidak ditemukan dalam respons AI.');
      }

      const rateMatch = mimeType.match(/rate=(\d+)/);
      const sampleRate = rateMatch ? parseInt(rateMatch[1], 10) : 24000;
      const pcmBuffer = base64ToArrayBuffer(audioData);
      const evenByteLength = pcmBuffer.byteLength - (pcmBuffer.byteLength % 2);
      const pcm16 = new Int16Array(pcmBuffer, 0, evenByteLength / 2);
      const wavBlob = pcmToWav(pcm16, sampleRate);
      return URL.createObjectURL(wavBlob);
    }

    /**
     * =========================================================================
     * 5. MANAJEMEN PROYEK & PANDUAN PENGGUNAAN
     * =========================================================================
     */
    function switchProject(projectId) {
      appState.activeProjectId = projectId;
      appState.selectedEpisodeNumber = 1;
      appState.isEditingScript = false;
      saveState();
      renderApp();
      showToast('Proyek berhasil dibuka.', 'info');
    }

    function openNewProjectModal() {
      openModal(`
        <div class="flex items-center justify-between mb-4">
          <div class="flex items-center gap-2.5">
            <div class="w-9 h-9 rounded-xl bg-amber-500/15 text-amber-500 flex items-center justify-center">
              <i data-lucide="clapperboard" class="w-5 h-5"></i>
            </div>
            <div>
              <h3 class="font-serif font-bold text-xl">Mulai Serial Drama Baru</h3>
              <p class="text-xs text-slate-500 dark:text-slate-400">Tulis ide singkat atau langsung minta AI merancangnya</p>
            </div>
          </div>
          <button onclick="closeModal()" class="p-1.5 rounded-lg hover:bg-slate-100 dark:hover:bg-studio-800 text-slate-400">
            <i data-lucide="x" class="w-5 h-5"></i>
          </button>
        </div>

        <div class="space-y-4 text-sm">
          <div>
            <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1">Judul Drama (Opsional)</label>
            <input id="np-title" type="text" placeholder="Contoh: Cahaya di Balik Awan, Rahasia Rumah Kayu..."
              class="w-full px-4 py-2.5 rounded-xl bg-slate-50 dark:bg-studio-850 border border-slate-300 dark:border-slate-700 focus:outline-none focus:border-amber-500" />
          </div>

          <div class="grid grid-cols-1 sm:grid-cols-2 gap-3.5">
            <div>
              <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1">Pilih Genre Utama</label>
              <select id="np-genre" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-50 dark:bg-studio-850 border border-slate-300 dark:border-slate-700">
                ${GENRE_LIST.map(g => `<option value="${g.name}">${g.name}</option>`).join('')}
              </select>
            </div>
            <div>
              <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1">Jumlah Episode</label>
              <select id="np-episodes" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-50 dark:bg-studio-850 border border-slate-300 dark:border-slate-700">
                <option value="3">3 Episode (Mini Seri)</option>
                <option value="5" selected>5 Episode (Standar)</option>
                <option value="10">10 Episode (Serial Penuh)</option>
                <option value="15">15 Episode</option>
                <option value="20">20 Episode</option>
              </select>
            </div>
          </div>

          <div>
            <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 mb-1">Ide Cerita Singkat / Premis</label>
            <textarea id="np-idea" rows="3" placeholder="Contoh: Seorang guru muda ditugaskan di desa terpencil dan harus meyakinkan warga agar anak-anak mereka tetap bersekolah..."
              class="w-full px-4 py-2.5 rounded-xl bg-slate-50 dark:bg-studio-850 border border-slate-300 dark:border-slate-700 focus:outline-none focus:border-amber-500"></textarea>
          </div>
        </div>

        <div class="mt-6 pt-4 border-t border-slate-200 dark:border-slate-800 flex flex-col sm:flex-row justify-end gap-2.5">
          <button onclick="createNewProject(false)" class="px-4 py-2.5 rounded-xl bg-slate-200 dark:bg-studio-800 hover:bg-slate-300 dark:hover:bg-studio-700 font-semibold text-xs sm:text-sm">
            Buat Proyek Kosong
          </button>
          <button onclick="createNewProject(true)" class="px-5 py-2.5 rounded-xl bg-gradient-to-r from-amber-500 to-orange-500 hover:from-amber-400 hover:to-orange-400 text-slate-950 font-bold text-xs sm:text-sm flex items-center justify-center gap-1.5 shadow-lg shadow-amber-500/20">
            <i data-lucide="sparkles" class="w-4 h-4"></i>
            <span>Buat & Rancang Otomatis (AI)</span>
          </button>
        </div>
      `);
    }

    async function createNewProject(autoFillWithAI) {
      const titleInput = document.getElementById('np-title').value.trim();
      const genreInput = document.getElementById('np-genre').value;
      const epCount = parseInt(document.getElementById('np-episodes').value, 10) || 5;
      const ideaInput = document.getElementById('np-idea').value.trim();

      const newProj = {
        id: 'proj_' + Date.now(),
        updatedAt: new Date().toISOString(),
        genre: genreInput,
        customGenre: '',
        settings: {
          title: titleInput || 'Serial Drama Baru',
          theme: '',
          synopsis: ideaInput,
          settingPlace: 'Indonesia',
          era: 'Masa Kini (2026)',
          mood: 'Dramatis & Menyentuh Hati',
          audience: 'Semua Umur / Keluarga',
          episodeCount: epCount,
          episodeDuration: '45 Menit (Standar TV/Streaming)',
          narrativeStyle: 'Alur Maju Kronologis',
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

      if (autoFillWithAI) {
        await aiAutoFillStorySettings(ideaInput || titleInput);
      } else {
        showToast('Proyek baru siap diatur!', 'success');
      }
    }

    function toggleDashboardGuide() {
      appState.showDashboardGuide = !appState.showDashboardGuide;
      renderApp();
    }

    function openUserGuideModal() {
      const steps = [
        {
          num: '01',
          title: 'Mulai Proyek & Atur Genre Cerita',
          tab: 'setup',
          tabLabel: 'Buka Tahap 1',
          details: [
            'Klik tombol <strong>Mulai Membuat Drama</strong> atau <strong>Drama Baru</strong> di bagian atas.',
            'Pilih salah satu dari <strong>15 kartu genre</strong> (seperti Drama keluarga, percintaan, misteri, kerajaan) atau ketik genre unik Anda sendiri.',
            'Isi judul, sinopsis, latar tempat, zaman, dan jumlah episode (3, 5, 10, 15, 20, atau custom). Klik <strong>Sempurnakan & Isi Otomatis dengan AI</strong> jika ingin AI merancangnya.'
          ]
        },
        {
          num: '02',
          title: 'Buat Karakter & Kunci Konsistensi Wajah',
          tab: 'characters',
          tabLabel: 'Buka Tahap 2',
          details: [
            'Klik <strong>Buat Karakter Otomatis (AI)</strong> agar AI menciptakan pemeran utama dan pendukung beserta latar belakangnya.',
            'Anda juga bisa menambah, mengedit, atau menghapus karakter secara manual.',
            '<strong>Tips Penting:</strong> Klik tombol <strong>Foto Karakter AI</strong> pada setiap kartu tokoh. Foto dan ciri pakaian ini akan dikunci sebagai referensi agar wajah tokoh tetap konsisten di semua episode.'
          ]
        },
        {
          num: '03',
          title: 'Rancang Alur Cerita Berseri',
          tab: 'plot',
          tabLabel: 'Buka Tahap 3',
          details: [
            'Klik <strong>Buat Alur Cerita & Outline Episode (AI)</strong>.',
            'AI akan menyusun konflik utama, konflik tambahan, klimaks, <em>plot twist</em>, penyelesaian, serta ringkasan Episode 1 hingga tamat yang saling terhubung.'
          ]
        },
        {
          num: '04',
          title: 'Tulis & Poles Naskah Setiap Episode',
          tab: 'script',
          tabLabel: 'Buka Tahap 4',
          details: [
            'Pilih nomor episode (Ep 1, Ep 2, dst.) lalu klik <strong>Buat Episode</strong> untuk menghasilkan naskah lengkap berisi pembukaan, pembagian adegan, lokasi, dialog beremosi, arahan kamera, musik latar, dan <em>cliffhanger</em>.',
            'Gunakan tombol kreatif seperti <strong>Buat Ulang Dialog</strong>, <strong>Perpanjang Cerita</strong>, <strong>Ubah Konflik</strong>, atau <strong>Edit Naskah</strong>.',
            'Klik <strong>Dengarkan Pembacaan AI</strong> untuk mendengar sulih suara dramatis atau <strong>Lanjutkan ke Episode Berikutnya</strong>.'
          ]
        },
        {
          num: '05',
          title: 'Buat Poster Utama & Ilustrasi Adegan',
          tab: 'visuals',
          tabLabel: 'Buka Tahap 5',
          details: [
            'Buka tab <strong>5. Studio Visual AI</strong> atau klik tombol <strong>Ilustrasi Adegan AI</strong> langsung di dalam naskah.',
            'Pilih jenis gambar (<em>Poster utama serial, Foto karakter, Ilustrasi adegan, Background lokasi, Thumbnail,</em> atau <em>Sampul episode</em>) dan gaya visual favorit Anda.',
            'Terakhir, klik ikon <strong>Unduh (Ekspor)</strong> di pojok kanan atas untuk menyimpan seluruh paket naskah drama ke format <code>.TXT</code>.'
          ]
        }
      ];

      openModal(`
        <div class="flex items-center justify-between pb-4 mb-4 border-b border-slate-200 dark:border-slate-800">
          <div class="flex items-center gap-2.5">
            <div class="w-9 h-9 rounded-xl bg-amber-500/15 text-amber-500 flex items-center justify-center">
              <i data-lucide="book-open" class="w-5 h-5"></i>
            </div>
            <div>
              <h3 class="font-serif font-bold text-lg sm:text-xl text-slate-900 dark:text-white">Petunjuk Penggunaan Drama Studio AI</h3>
              <p class="text-xs text-slate-500 dark:text-slate-400">Panduan praktis 5 langkah mewujudkan ide menjadi serial drama lengkap</p>
            </div>
          </div>
          <button onclick="closeModal()" class="p-1.5 rounded-lg hover:bg-slate-100 dark:hover:bg-studio-800 text-slate-400">
            <i data-lucide="x" class="w-5 h-5"></i>
          </button>
        </div>

        <div class="space-y-4 max-h-[68vh] overflow-y-auto pr-1">
          ${steps.map(st => `
            <div class="p-4 rounded-2xl bg-slate-50 dark:bg-studio-850 border border-slate-200/80 dark:border-slate-800">
              <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-2 mb-2.5">
                <div class="flex items-center gap-2.5">
                  <span class="px-2.5 py-1 rounded-lg bg-amber-500 text-slate-950 font-mono font-bold text-xs">LANGKAH ${st.num}</span>
                  <h4 class="font-serif font-bold text-base text-slate-900 dark:text-white">${st.title}</h4>
                </div>
                <button onclick="closeModal(); navigateTo('${st.tab}');"
                  class="px-3 py-1.5 rounded-xl bg-amber-500/15 hover:bg-amber-500 text-amber-600 dark:text-amber-300 hover:text-slate-950 font-semibold text-xs flex items-center gap-1 transition-colors self-start sm:self-auto">
                  <span>${st.tabLabel}</span>
                  <i data-lucide="arrow-right" class="w-3.5 h-3.5"></i>
                </button>
              </div>
              <ul class="space-y-1.5 text-xs sm:text-sm text-slate-600 dark:text-slate-300 list-disc pl-5 leading-relaxed">
                ${st.details.map(d => `<li>${d}</li>`).join('')}
              </ul>
            </div>
          `).join('')}
        </div>

        <div class="mt-5 pt-4 border-t border-slate-200 dark:border-slate-800 flex justify-end gap-2">
          <button onclick="closeModal()" class="px-5 py-2.5 rounded-xl bg-amber-500 hover:bg-amber-400 text-slate-950 font-bold text-xs sm:text-sm">
            Mengerti, Mulai Berkarya!
          </button>
        </div>
      `);
    }

    /**
     * =========================================================================
     * 6. RENDER HALAMAN A: DASHBOARD STUDIO UTAMA
     * =========================================================================
     */
    function renderDashboardView() {
      const activeProj = getActiveProject();
      const allCharacters = [];
      const allPosters = [];
      const recentEpisodes = [];

      (appState.projects || []).forEach(p => {
        (p.characters || []).forEach(c => {
          allCharacters.push({ ...c, projectId: p.id, projectTitle: p.settings.title });
        });
        (p.gallery || []).forEach(g => {
          if (g.category.toLowerCase().includes('poster')) {
            allPosters.push({ ...g, projectId: p.id, projectTitle: p.settings.title });
          }
        });
        Object.values(p.scripts || {}).forEach(sc => {
          recentEpisodes.push({ ...sc, projectId: p.id, projectTitle: p.settings.title });
        });
      });

      return `
        <div class="space-y-8 animate-fade-in">
          <!-- HERO STUDIO BANNER -->
          <section class="relative rounded-3xl overflow-hidden bg-gradient-to-br from-studio-900 via-studio-850 to-slate-950 border border-amber-500/25 p-6 sm:p-10 text-white shadow-2xl">
            <div class="absolute -right-24 -top-24 w-80 h-80 rounded-full bg-amber-500/15 blur-3xl pointer-events-none"></div>
            <div class="absolute -left-24 -bottom-24 w-72 h-72 rounded-full bg-indigo-500/15 blur-3xl pointer-events-none"></div>

            <div class="relative z-10 max-w-3xl">
              <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-amber-500/15 border border-amber-400/30 text-amber-300 text-xs font-semibold mb-4">
                <i data-lucide="film" class="w-3.5 h-3.5"></i>
                <span>DRAMA STUDIO AI • STUDIO PRODUKSI SERIAL DIGITAL</span>
              </div>

              <h1 class="font-serif font-extrabold text-3xl sm:text-5xl leading-tight tracking-tight mb-4">
                Wujudkan Ide Ceritamu Menjadi <span class="bg-gradient-to-r from-amber-300 via-amber-400 to-orange-400 bg-clip-text text-transparent">Serial Drama.</span>
              </h1>

              <p class="text-sm sm:text-base text-slate-300 leading-relaxed mb-7 max-w-2xl">
                Rancang serial drama berseri dari satu kalimat ide menjadi karakter dengan wajah konsisten, alur cerita saling terhubung, dialog penuh emosi, poster resmi, hingga naskah video siap produksi.
              </p>

              <div class="flex flex-wrap items-center gap-3 sm:gap-4">
                <button onclick="openNewProjectModal()" class="px-6 py-3.5 rounded-2xl bg-gradient-to-r from-amber-400 to-orange-500 hover:from-amber-300 hover:to-orange-400 text-slate-950 font-bold text-sm sm:text-base shadow-xl shadow-amber-500/25 flex items-center gap-2.5 transition-transform active:scale-95">
                  <i data-lucide="sparkles" class="w-5 h-5"></i>
                  <span>Mulai Membuat Drama</span>
                </button>

                ${activeProj ? `
                  <button onclick="navigateTo('setup')" class="px-5 py-3.5 rounded-2xl bg-white/10 hover:bg-white/15 border border-white/15 text-white font-semibold text-sm sm:text-base flex items-center gap-2.5 transition-colors">
                    <i data-lucide="play-circle" class="w-5 h-5 text-amber-400"></i>
                    <span>Lanjutkan Proyek: ${escapeHtml(activeProj.settings.title)}</span>
                  </button>
                ` : ''}

                <button onclick="openUserGuideModal()" class="px-4 py-3.5 rounded-2xl bg-amber-500/15 hover:bg-amber-500/25 border border-amber-400/30 text-amber-300 font-semibold text-sm flex items-center gap-2 transition-colors">
                  <i data-lucide="book-open" class="w-4 h-4"></i>
                  <span>Petunjuk Penggunaan</span>
                </button>
              </div>
            </div>
          </section>

          <!-- PETUNJUK PENGGUNAAN & LANGKAH-LANGKAH (UNTUK PEMULA) -->
          <section class="rounded-3xl bg-white dark:bg-studio-900 border border-slate-200 dark:border-slate-800 overflow-hidden shadow-sm">
            <div class="px-5 sm:px-6 py-4 bg-gradient-to-r from-amber-500/10 via-orange-500/5 to-transparent border-b border-slate-200/80 dark:border-slate-800 flex flex-wrap items-center justify-between gap-3">
              <div class="flex items-center gap-3">
                <div class="w-9 h-9 rounded-xl bg-amber-500 text-slate-950 flex items-center justify-center shrink-0">
                  <i data-lucide="compass" class="w-5 h-5"></i>
                </div>
                <div>
                  <h2 class="font-serif font-bold text-base sm:text-lg text-slate-900 dark:text-white">Petunjuk Penggunaan & Langkah-Langkah Membuat Serial</h2>
                  <p class="text-xs text-slate-500 dark:text-slate-400">Ikuti 5 langkah berurutan di bawah ini untuk menghasilkan serial drama lengkap dari nol</p>
                </div>
              </div>
              <div class="flex items-center gap-2">
                <button onclick="openUserGuideModal()" class="px-3 py-1.5 rounded-xl bg-amber-500/15 hover:bg-amber-500/25 text-amber-600 dark:text-amber-300 text-xs font-semibold transition-colors">
                  Panduan Detail
                </button>
                <button onclick="toggleDashboardGuide()" class="px-3 py-1.5 rounded-xl bg-slate-100 dark:bg-studio-800 hover:bg-slate-200 dark:hover:bg-studio-700 text-xs font-semibold flex items-center gap-1 transition-colors">
                  <span>${appState.showDashboardGuide ? 'Sembunyikan' : 'Tampilkan'}</span>
                  <i data-lucide="${appState.showDashboardGuide ? 'chevron-up' : 'chevron-down'}" class="w-3.5 h-3.5"></i>
                </button>
              </div>
            </div>

            ${appState.showDashboardGuide ? `
              <div class="p-5 sm:p-6">
                <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-5 gap-3.5">
                  ${[
                    {
                      step: 'Langkah 1',
                      title: 'Pilih Genre & Cerita',
                      desc: 'Klik "Mulai Membuat Drama", pilih dari 15+ genre, lalu isi pengaturan cerita atau gunakan tombol Isi Otomatis AI.',
                      tab: 'setup',
                      icon: 'clapperboard'
                    },
                    {
                      step: 'Langkah 2',
                      title: 'Buat Karakter Konsisten',
                      desc: 'Generate karakter otomatis dan klik "Foto Karakter AI" agar wajah & pakaian tokoh tetap konsisten di semua episode.',
                      tab: 'characters',
                      icon: 'users'
                    },
                    {
                      step: 'Langkah 3',
                      title: 'Susun Alur Berseri',
                      desc: 'Generate konflik utama, klimaks, plot twist, serta ringkasan Episode 1 sampai tamat yang saling terhubung.',
                      tab: 'plot',
                      icon: 'git-branch'
                    },
                    {
                      step: 'Langkah 4',
                      title: 'Tulis Naskah Episode',
                      desc: 'Buat dialog lengkap, arahan kamera, dan musik. Gunakan tombol Ubah Konflik, Perpanjang Cerita, atau Audio AI.',
                      tab: 'script',
                      icon: 'file-text'
                    },
                    {
                      step: 'Langkah 5',
                      title: 'Poster, Visual & Ekspor',
                      desc: 'Ciptakan poster resmi dan ilustrasi adegan multi-gaya, lalu unduh paket naskah lengkap (.TXT) di pojok kanan atas.',
                      tab: 'visuals',
                      icon: 'image'
                    }
                  ].map(item => `
                    <button onclick="navigateTo('${item.tab}')" class="p-4 rounded-2xl bg-slate-50 dark:bg-studio-850 border border-slate-200/80 dark:border-slate-800 hover:border-amber-500/60 text-left transition-all group flex flex-col justify-between">
                      <div>
                        <div class="flex items-center justify-between mb-2">
                          <span class="px-2 py-0.5 rounded-md bg-amber-500/15 text-[10px] font-bold uppercase tracking-wider text-amber-600 dark:text-amber-400">${item.step}</span>
                          <i data-lucide="${item.icon}" class="w-4 h-4 text-slate-400 group-hover:text-amber-400 transition-colors"></i>
                        </div>
                        <div class="font-bold text-sm text-slate-900 dark:text-white mb-1.5 group-hover:text-amber-500 transition-colors">${item.title}</div>
                        <p class="text-xs text-slate-600 dark:text-slate-400 leading-relaxed mb-3">${item.desc}</p>
                      </div>
                      <div class="text-[11px] font-semibold text-amber-600 dark:text-amber-400 flex items-center gap-1 pt-2 border-t border-slate-200/60 dark:border-slate-800">
                        <span>Mulai tahap ini</span>
                        <i data-lucide="arrow-right" class="w-3 h-3 group-hover:translate-x-0.5 transition-transform"></i>
                      </div>
                    </button>
                  `).join('')}
                </div>
              </div>
            ` : ''}
          </section>

          <!-- DRAMA YANG PERNAH DIBUAT -->
          <section>
            <div class="flex items-center justify-between mb-4">
              <div>
                <h2 class="font-serif font-bold text-xl sm:text-2xl text-slate-900 dark:text-white">Drama yang Pernah Dibuat</h2>
                <p class="text-xs sm:text-sm text-slate-500 dark:text-slate-400">Pilih serial drama untuk melanjutkan penulisan atau produksi visual.</p>
              </div>
              <button onclick="openNewProjectModal()" class="text-xs sm:text-sm font-semibold text-amber-600 dark:text-amber-400 hover:underline flex items-center gap-1">
                <i data-lucide="plus" class="w-4 h-4"></i> Tambah Proyek
              </button>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-5">
              ${appState.projects.map(proj => {
                const isSelected = proj.id === activeProj?.id;
                const scriptCount = Object.keys(proj.scripts || {}).length;
                const poster = (proj.gallery || []).find(g => g.imageUrl && g.category.toLowerCase().includes('poster'));
                return `
                  <div class="rounded-3xl bg-white dark:bg-studio-900 border ${isSelected ? 'border-amber-500 ring-2 ring-amber-500/20' : 'border-slate-200 dark:border-slate-800'} overflow-hidden flex flex-col shadow-sm hover:shadow-xl transition-all">
                    <div class="h-40 relative bg-gradient-to-br from-slate-800 via-studio-850 to-amber-950 p-5 flex flex-col justify-between overflow-hidden">
                      ${poster ? `<img src="${poster.imageUrl}" alt="${escapeHtml(proj.settings.title)}" class="absolute inset-0 w-full h-full object-cover opacity-55">` : ''}
                      <div class="absolute inset-0 bg-gradient-to-t from-studio-950 via-studio-950/40 to-transparent"></div>
                      <div class="relative z-10 flex items-center justify-between">
                        <span class="px-2.5 py-1 rounded-full text-[11px] font-semibold bg-amber-500/20 text-amber-300 border border-amber-400/30 backdrop-blur-md">
                          ${escapeHtml(proj.customGenre || proj.genre)}
                        </span>
                        ${isSelected ? `<span class="px-2.5 py-0.5 rounded-full text-[10px] font-bold bg-emerald-500 text-slate-950">AKTIF</span>` : ''}
                      </div>
                      <div class="relative z-10">
                        <h3 class="font-serif font-bold text-lg text-white line-clamp-1">${escapeHtml(proj.settings.title)}</h3>
                        <p class="text-xs text-slate-300">${proj.settings.episodeCount} Episode • ${escapeHtml(proj.settings.episodeDuration)}</p>
                      </div>
                    </div>

                    <div class="p-5 flex-1 flex flex-col justify-between gap-4">
                      <p class="text-xs sm:text-sm text-slate-600 dark:text-slate-300 line-clamp-3 leading-relaxed">
                        ${escapeHtml(proj.settings.synopsis || 'Belum ada sinopsis. Klik lanjutkan untuk mulai merancang cerita.')}
                      </p>

                      <div class="flex items-center justify-between text-xs text-slate-500 dark:text-slate-400 pt-3 border-t border-slate-100 dark:border-slate-800">
                        <span>${(proj.characters || []).length} Karakter</span>
                        <span>${scriptCount}/${proj.settings.episodeCount} Naskah</span>
                      </div>

                      <div class="flex items-center gap-2">
                        <button onclick="switchProject('${proj.id}'); navigateTo('setup');" class="flex-1 py-2.5 px-4 rounded-xl bg-amber-500 hover:bg-amber-400 text-slate-950 font-semibold text-xs sm:text-sm transition-colors flex items-center justify-center gap-1.5">
                          <span>Lanjutkan Proyek</span>
                          <i data-lucide="arrow-right" class="w-4 h-4"></i>
                        </button>
                      </div>
                    </div>
                  </div>
                `;
              }).join('')}
            </div>
          </section>

          <!-- KOLEKSI KARAKTER, POSTER & EPISODE TERBARU -->
          <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
            <!-- KOLEKSI KARAKTER -->
            <section class="rounded-3xl bg-white dark:bg-studio-900 border border-slate-200 dark:border-slate-800 p-5">
              <div class="flex items-center justify-between mb-4">
                <h3 class="font-serif font-bold text-lg flex items-center gap-2">
                  <i data-lucide="users" class="w-5 h-5 text-amber-500"></i>
                  <span>Koleksi Karakter</span>
                </h3>
                <button onclick="navigateTo('characters')" class="text-xs font-semibold text-amber-500 hover:underline">Kelola</button>
              </div>
              <div class="space-y-3">
                ${allCharacters.length === 0 ? `<p class="text-xs text-slate-500">Belum ada karakter dibuat.</p>` :
                  allCharacters.slice(0, 4).map(c => `
                    <div onclick="switchProject('${c.projectId}'); navigateTo('characters');" class="flex items-center gap-3 p-2.5 rounded-2xl bg-slate-50 dark:bg-studio-850 hover:bg-amber-500/10 cursor-pointer transition-colors border border-slate-200/70 dark:border-slate-800">
                      ${c.imageUrl
                        ? `<img src="${c.imageUrl}" alt="${escapeHtml(c.name)}" class="w-12 h-12 rounded-xl object-cover border border-amber-500/30 shrink-0">`
                        : `<div class="w-12 h-12 rounded-xl bg-gradient-to-br from-amber-500/20 to-indigo-500/20 border border-amber-500/30 flex items-center justify-center font-serif font-bold text-amber-400 shrink-0">${escapeHtml(c.name.charAt(0))}</div>`
                      }
                      <div class="min-w-0 flex-1">
                        <div class="font-bold text-sm truncate">${escapeHtml(c.name)}</div>
                        <div class="text-xs text-amber-600 dark:text-amber-400 truncate">${escapeHtml(c.role)}</div>
                        <div class="text-[11px] text-slate-500 truncate">${escapeHtml(c.projectTitle)}</div>
                      </div>
                    </div>
                  `).join('')
                }
              </div>
            </section>

            <!-- KOLEKSI POSTER -->
            <section class="rounded-3xl bg-white dark:bg-studio-900 border border-slate-200 dark:border-slate-800 p-5">
              <div class="flex items-center justify-between mb-4">
                <h3 class="font-serif font-bold text-lg flex items-center gap-2">
                  <i data-lucide="image" class="w-5 h-5 text-amber-500"></i>
                  <span>Koleksi Poster</span>
                </h3>
                <button onclick="navigateTo('visuals')" class="text-xs font-semibold text-amber-500 hover:underline">Studio Visual</button>
              </div>
              <div class="grid grid-cols-2 gap-3">
                ${allPosters.slice(0, 4).map(p => `
                  <div onclick="switchProject('${p.projectId}'); navigateTo('visuals');" class="group relative aspect-[3/4] rounded-2xl overflow-hidden bg-gradient-to-br from-amber-900 via-studio-900 to-slate-950 border border-slate-700 cursor-pointer">
                    ${p.imageUrl
                      ? `<img src="${p.imageUrl}" alt="${escapeHtml(p.title)}" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-300">`
                      : `<div class="w-full h-full p-3 flex flex-col justify-between bg-gradient-to-b from-amber-500/10 to-studio-950">
                          <span class="text-[9px] uppercase tracking-widest text-amber-400 font-bold">POSTER SERIAL</span>
                          <div>
                            <div class="font-serif font-bold text-xs text-white leading-snug mb-1">${escapeHtml(p.projectTitle)}</div>
                            <span class="text-[10px] text-amber-300 underline">Klik buat gambar AI</span>
                          </div>
                        </div>`
                    }
                  </div>
                `).join('')}
              </div>
            </section>

            <!-- EPISODE TERBARU -->
            <section class="rounded-3xl bg-white dark:bg-studio-900 border border-slate-200 dark:border-slate-800 p-5">
              <div class="flex items-center justify-between mb-4">
                <h3 class="font-serif font-bold text-lg flex items-center gap-2">
                  <i data-lucide="film" class="w-5 h-5 text-amber-500"></i>
                  <span>Episode Terbaru</span>
                </h3>
                <button onclick="navigateTo('script')" class="text-xs font-semibold text-amber-500 hover:underline">Buka Naskah</button>
              </div>
              <div class="space-y-3">
                ${recentEpisodes.length === 0 ? `<p class="text-xs text-slate-500">Belum ada naskah episode ditulis.</p>` :
                  recentEpisodes.slice(0, 4).map(ep => `
                    <div onclick="switchProject('${ep.projectId}'); appState.selectedEpisodeNumber=${ep.episodeNumber}; navigateTo('script');" class="p-3 rounded-2xl bg-slate-50 dark:bg-studio-850 hover:bg-amber-500/10 border border-slate-200/70 dark:border-slate-800 cursor-pointer transition-colors">
                      <div class="flex items-center justify-between mb-1">
                        <span class="text-[11px] font-bold text-amber-600 dark:text-amber-400">EPISODE ${ep.episodeNumber}</span>
                        <span class="text-[10px] text-slate-400">${escapeHtml(ep.projectTitle)}</span>
                      </div>
                      <div class="font-bold text-sm mb-1">${escapeHtml(ep.title)}</div>
                      <p class="text-xs text-slate-500 dark:text-slate-400 line-clamp-2">${escapeHtml(ep.summary)}</p>
                    </div>
                  `).join('')
                }
              </div>
            </section>
          </div>
        </div>
      `;
    }

    /**
     * =========================================================================
     * 7. RENDER HALAMAN B & C: PILIHAN GENRE & PENGATURAN CERITA
     * =========================================================================
     */
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
              <span class="text-xs font-bold uppercase tracking-wider text-amber-500">Tahap 1 • Konsep & Pondasi Cerita</span>
              <h1 class="font-serif font-bold text-2xl sm:text-3xl mt-1">Pilihan Genre & Pengaturan Serial</h1>
            </div>
            <button onclick="aiAutoFillStorySettings()" class="px-5 py-3 rounded-2xl bg-gradient-to-r from-amber-500 to-orange-500 hover:from-amber-400 hover:to-orange-400 text-slate-950 font-bold text-xs sm:text-sm shadow-lg shadow-amber-500/20 flex items-center justify-center gap-2">
              <i data-lucide="wand-2" class="w-4 h-4"></i>
              <span>Sempurnakan & Isi Otomatis dengan AI</span>
            </button>
          </div>

          <!-- B. PILIHAN GENRE DRAMA (15 KARTU BERGAMBAR + GENRE KUSTOM) -->
          <section class="rounded-3xl bg-white dark:bg-studio-900 border border-slate-200 dark:border-slate-800 p-5 sm:p-6">
            <h2 class="font-serif font-bold text-xl mb-1">B. Pilih Genre Drama</h2>
            <p class="text-xs sm:text-sm text-slate-500 dark:text-slate-400 mb-5">Pilih salah satu dari 15 genre drama unggulan atau ciptakan genre unik Anda sendiri.</p>

            <div class="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-5 gap-3 sm:gap-4 mb-5">
              ${GENRE_LIST.map(g => {
                const isSelected = !proj.customGenre && proj.genre === g.name;
                return `
                  <button onclick="selectGenre('${g.name}')"
                    class="group relative rounded-2xl overflow-hidden text-left border-2 transition-all flex flex-col justify-between h-36 sm:h-40 p-3.5 ${
                      isSelected
                        ? 'border-amber-400 ring-4 ring-amber-500/20 scale-[1.02]'
                        : 'border-transparent hover:border-amber-500/50'
                    }">
                    <div class="absolute inset-0 bg-gradient-to-br ${g.gradient} opacity-90 group-hover:opacity-100 transition-opacity"></div>
                    <svg class="absolute -right-4 -bottom-4 w-24 h-24 text-white/10" viewBox="0 0 100 100" fill="currentColor">
                      <circle cx="50" cy="50" r="45"/>
                    </svg>

                    <div class="relative z-10 flex items-center justify-between">
                      <div class="w-8 h-8 rounded-xl bg-black/25 backdrop-blur-sm flex items-center justify-center text-white">
                        <i data-lucide="${g.icon}" class="w-4 h-4"></i>
                      </div>
                      ${isSelected ? `<span class="w-6 h-6 rounded-full bg-amber-400 text-slate-950 flex items-center justify-center"><i data-lucide="check" class="w-3.5 h-3.5"></i></span>` : ''}
                    </div>

                    <div class="relative z-10">
                      <div class="font-bold text-xs sm:text-sm text-white leading-snug mb-1">${g.name}</div>
                      <p class="text-[10px] text-white/80 line-clamp-2 leading-tight">${g.desc}</p>
                    </div>
                  </button>
                `;
              }).join('')}
            </div>

            <!-- Custom Genre Input -->
            <div class="p-4 rounded-2xl bg-slate-50 dark:bg-studio-850 border border-slate-200 dark:border-slate-700/80 flex flex-col sm:flex-row sm:items-center gap-3">
              <div class="flex items-center gap-2 text-sm font-semibold text-amber-600 dark:text-amber-400 shrink-0">
                <i data-lucide="sparkles" class="w-4 h-4"></i>
                <span>Atau Buat Genre Sendiri:</span>
              </div>
              <input type="text" id="input-custom-genre" value="${escapeHtml(proj.customGenre || '')}"
                oninput="updateCustomGenre(this.value)"
                placeholder="Contoh: Drama Kuliner & Warisan Keluarga, Drama Sci-Fi Nusantara..."
                class="flex-1 px-4 py-2.5 rounded-xl bg-white dark:bg-studio-900 border border-slate-300 dark:border-slate-700 text-sm focus:outline-none focus:border-amber-500" />
            </div>
          </section>

          <!-- C. PENGATURAN CERITA -->
          <section class="rounded-3xl bg-white dark:bg-studio-900 border border-slate-200 dark:border-slate-800 p-5 sm:p-6">
            <h2 class="font-serif font-bold text-xl mb-1">C. Pengaturan Cerita & Bible Serial</h2>
            <p class="text-xs sm:text-sm text-slate-500 dark:text-slate-400 mb-6">Tentukan identitas, latar dunia, dan struktur episode serial drama Anda.</p>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-5">
              <!-- Judul Drama -->
              <div>
                <label class="block text-xs font-semibold uppercase tracking-wider text-slate-500 dark:text-slate-400 mb-1.5">Judul Drama</label>
                <input type="text" value="${escapeHtml(s.title)}" onchange="updateSetting('title', this.value)"
                  placeholder="Masukkan judul serial drama..."
                  class="w-full px-4 py-3 rounded-xl bg-slate-50 dark:bg-studio-850 border border-slate-300 dark:border-slate-700 text-sm font-semibold focus:outline-none focus:border-amber-500" />
              </div>

              <!-- Tema Utama -->
              <div>
                <label class="block text-xs font-semibold uppercase tracking-wider text-slate-500 dark:text-slate-400 mb-1.5">Tema Utama</label>
                <input type="text" value="${escapeHtml(s.theme)}" onchange="updateSetting('theme', this.value)"
                  placeholder="Contoh: Pengorbanan seorang ibu, Kesetiaan di tengah ujian..."
                  class="w-full px-4 py-3 rounded-xl bg-slate-50 dark:bg-studio-850 border border-slate-300 dark:border-slate-700 text-sm focus:outline-none focus:border-amber-500" />
              </div>

              <!-- Sinopsis Cerita (Full Width) -->
              <div class="md:col-span-2">
                <label class="block text-xs font-semibold uppercase tracking-wider text-slate-500 dark:text-slate-400 mb-1.5">Sinopsis Cerita</label>
                <textarea rows="4" onchange="updateSetting('synopsis', this.value)"
                  placeholder="Tuliskan premis atau ringkasan cerita serial drama Anda..."
                  class="w-full px-4 py-3 rounded-xl bg-slate-50 dark:bg-studio-850 border border-slate-300 dark:border-slate-700 text-sm leading-relaxed focus:outline-none focus:border-amber-500">${escapeHtml(s.synopsis)}</textarea>
              </div>

              <!-- Latar Tempat -->
              <div>
                <label class="block text-xs font-semibold uppercase tracking-wider text-slate-500 dark:text-slate-400 mb-1.5">Latar Tempat</label>
                <input type="text" value="${escapeHtml(s.settingPlace)}" onchange="updateSetting('settingPlace', this.value)"
                  placeholder="Contoh: Desa Lereng Merapi, Jakarta, Pelabuhan Tua..."
                  class="w-full px-4 py-3 rounded-xl bg-slate-50 dark:bg-studio-850 border border-slate-300 dark:border-slate-700 text-sm focus:outline-none focus:border-amber-500" />
              </div>

              <!-- Zaman Cerita -->
              <div>
                <label class="block text-xs font-semibold uppercase tracking-wider text-slate-500 dark:text-slate-400 mb-1.5">Zaman Cerita</label>
                <input type="text" value="${escapeHtml(s.era)}" onchange="updateSetting('era', this.value)"
                  placeholder="Contoh: Masa Kini, Tahun 1998, Era Kerajaan Majapahit..."
                  class="w-full px-4 py-3 rounded-xl bg-slate-50 dark:bg-studio-850 border border-slate-300 dark:border-slate-700 text-sm focus:outline-none focus:border-amber-500" />
              </div>

              <!-- Suasana Cerita -->
              <div>
                <label class="block text-xs font-semibold uppercase tracking-wider text-slate-500 dark:text-slate-400 mb-1.5">Suasana Cerita</label>
                <input type="text" value="${escapeHtml(s.mood)}" onchange="updateSetting('mood', this.value)"
                  placeholder="Contoh: Hangat & Mengharukan, Tegang & Misterius..."
                  class="w-full px-4 py-3 rounded-xl bg-slate-50 dark:bg-studio-850 border border-slate-300 dark:border-slate-700 text-sm focus:outline-none focus:border-amber-500" />
              </div>

              <!-- Target Penonton -->
              <div>
                <label class="block text-xs font-semibold uppercase tracking-wider text-slate-500 dark:text-slate-400 mb-1.5">Target Penonton</label>
                <select onchange="updateSetting('audience', this.value)"
                  class="w-full px-4 py-3 rounded-xl bg-slate-50 dark:bg-studio-850 border border-slate-300 dark:border-slate-700 text-sm focus:outline-none focus:border-amber-500">
                  ${['Semua Umur / Keluarga', 'Remaja & Dewasa Muda (15+)', 'Dewasa (18+)', 'Anak & Keluarga'].map(opt =>
                    `<option value="${opt}" ${s.audience === opt ? 'selected' : ''}>${opt}</option>`
                  ).join('')}
                </select>
              </div>

              <!-- Jumlah Episode (3, 5, 10, 15, 20, atau Custom) -->
              <div>
                <label class="block text-xs font-semibold uppercase tracking-wider text-slate-500 dark:text-slate-400 mb-1.5">Jumlah Episode</label>
                <div class="flex flex-wrap items-center gap-2">
                  ${presetCounts.map(num => `
                    <button type="button" onclick="updateSetting('episodeCount', ${num}); renderApp();"
                      class="px-3.5 py-2.5 rounded-xl text-xs font-bold border transition-all ${
                        Number(s.episodeCount) === num
                          ? 'bg-amber-500 text-slate-950 border-amber-500'
                          : 'bg-slate-50 dark:bg-studio-850 border-slate-300 dark:border-slate-700 hover:border-amber-500'
                      }">
                      ${num} Ep
                    </button>
                  `).join('')}
                  <div class="flex items-center gap-1.5">
                    <input type="number" min="1" max="50" value="${s.episodeCount}"
                      onchange="updateSetting('episodeCount', Math.max(1, Math.min(50, parseInt(this.value) || 5))); renderApp();"
                      class="w-20 px-3 py-2.5 rounded-xl bg-slate-50 dark:bg-studio-850 border ${isCustomCount ? 'border-amber-500' : 'border-slate-300 dark:border-slate-700'} text-xs font-bold text-center focus:outline-none focus:border-amber-500"
                      title="Custom jumlah episode" />
                    <span class="text-xs text-slate-400">Custom</span>
                  </div>
                </div>
              </div>

              <!-- Durasi Setiap Episode -->
              <div>
                <label class="block text-xs font-semibold uppercase tracking-wider text-slate-500 dark:text-slate-400 mb-1.5">Durasi Setiap Episode</label>
                <select onchange="updateSetting('episodeDuration', this.value)"
                  class="w-full px-4 py-3 rounded-xl bg-slate-50 dark:bg-studio-850 border border-slate-300 dark:border-slate-700 text-sm focus:outline-none focus:border-amber-500">
                  ${['10 Menit (Web Series Pendek)', '20 Menit', '30 Menit', '45 Menit (Standar TV/Streaming)', '60 Menit (Drama Panjang)'].map(opt =>
                    `<option value="${opt}" ${s.episodeDuration === opt ? 'selected' : ''}>${opt}</option>`
                  ).join('')}
                </select>
              </div>

              <!-- Gaya Penceritaan -->
              <div>
                <label class="block text-xs font-semibold uppercase tracking-wider text-slate-500 dark:text-slate-400 mb-1.5">Gaya Penceritaan</label>
                <select onchange="updateSetting('narrativeStyle', this.value)"
                  class="w-full px-4 py-3 rounded-xl bg-slate-50 dark:bg-studio-850 border border-slate-300 dark:border-slate-700 text-sm focus:outline-none focus:border-amber-500">
                  ${[
                    'Alur Maju Kronologis',
                    'Alur Maju dengan Kilas Balik Emosional',
                    'Multi-Perspektif Antar Tokoh',
                    'Narasi Puitis & Kontemplatif',
                    'Cepat, Intens & Penuh Kejutan'
                  ].map(opt =>
                    `<option value="${opt}" ${s.narrativeStyle === opt ? 'selected' : ''}>${opt}</option>`
                  ).join('')}
                </select>
              </div>

              <!-- Pesan Moral -->
              <div>
                <label class="block text-xs font-semibold uppercase tracking-wider text-slate-500 dark:text-slate-400 mb-1.5">Pesan Moral</label>
                <input type="text" value="${escapeHtml(s.moralMessage)}" onchange="updateSetting('moralMessage', this.value)"
                  placeholder="Nilai kehidupan yang ingin disampaikan kepada penonton..."
                  class="w-full px-4 py-3 rounded-xl bg-slate-50 dark:bg-studio-850 border border-slate-300 dark:border-slate-700 text-sm focus:outline-none focus:border-amber-500" />
              </div>
            </div>

            <div class="mt-7 pt-5 border-t border-slate-200 dark:border-slate-800 flex flex-col sm:flex-row items-center justify-between gap-3">
              <span class="text-xs text-slate-500">Lanjutkan ke tahap pembuatan karakter setelah mengatur cerita.</span>
              <button onclick="navigateTo('characters')" class="w-full sm:w-auto px-6 py-3 rounded-2xl bg-amber-500 hover:bg-amber-400 text-slate-950 font-bold text-sm flex items-center justify-center gap-2 transition-colors">
                <span>Lanjut ke Studio Karakter</span>
                <i data-lucide="arrow-right" class="w-4 h-4"></i>
              </button>
            </div>
          </section>
        </div>
      `;
    }

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

    function updateSetting(key, val) {
      const proj = getActiveProject();
      proj.settings[key] = val;
      saveState();
      updateHeaderAndNav();
    }

    async function aiAutoFillStorySettings(seedIdea = '') {
      const proj = getActiveProject();
      const activeGenre = proj.customGenre || proj.genre;
      const currentIdea = seedIdea || proj.settings.synopsis || proj.settings.title;

      setLoading(true, 'Merancang Konsep Serial Drama...', 'AI sedang menyusun judul, sinopsis, latar tempat, suasana, dan pesan moral yang kuat.');
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
            moralMessage: { type: "STRING" }
          },
          required: ["title", "theme", "synopsis", "settingPlace", "era", "mood", "moralMessage"]
        };

        const data = await callGeminiText({
          systemPrompt: 'Kamu adalah Showrunner dan Penulis Utama serial drama Indonesia pemenang penghargaan. Buat konsep serial drama yang menyentuh, autentik, dan memikat dalam bahasa Indonesia.',
          userPrompt: `Buatkan konsep lengkap serial drama dengan genre "${activeGenre}". Ide awal/referensi: "${currentIdea || 'Buat ide orisinal yang sangat menyentuh'}". Jumlah episode direncanakan: ${proj.settings.episodeCount} episode.`,
          responseSchema: schema
        });

        proj.settings.title = data.title;
        proj.settings.theme = data.theme;
        proj.settings.synopsis = data.synopsis;
        proj.settings.settingPlace = data.settingPlace;
        proj.settings.era = data.era;
        proj.settings.mood = data.mood;
        proj.settings.moralMessage = data.moralMessage;

        saveState();
        renderApp();
        showToast('Konsep & pengaturan cerita berhasil dirancang oleh AI!', 'success');
      } catch (err) {
        showToast('Gagal merancang konsep: ' + err.message, 'error');
      } finally {
        setLoading(false);
      }
    }

    /**
     * =========================================================================
     * 8. RENDER HALAMAN D: PEMBUATAN KARAKTER (DENGAN KONSISTENSI VISUAL)
     * =========================================================================
     */
    function renderCharactersView() {
      const proj = getActiveProject();
      const chars = proj.characters || [];

      return `
        <div class="space-y-6 animate-fade-in">
          <!-- Header -->
          <div class="flex flex-col md:flex-row md:items-center justify-between gap-4">
            <div>
              <span class="text-xs font-bold uppercase tracking-wider text-amber-500">Tahap 2 • Pemeran & Referensi Visual Konsisten</span>
              <h1 class="font-serif font-bold text-2xl sm:text-3xl mt-1">Studio Pembuatan Karakter</h1>
            </div>
            <div class="flex flex-wrap items-center gap-2.5">
              <button onclick="openCharacterFormModal()" class="px-4 py-2.5 rounded-xl bg-slate-200 dark:bg-studio-800 hover:bg-slate-300 dark:hover:bg-studio-700 font-semibold text-xs sm:text-sm flex items-center gap-2 transition-colors">
                <i data-lucide="user-plus" class="w-4 h-4"></i>
                <span>Tambah Manual</span>
              </button>
              <button onclick="aiGenerateCharacters()" class="px-5 py-2.5 rounded-xl bg-gradient-to-r from-amber-500 to-orange-500 hover:from-amber-400 hover:to-orange-400 text-slate-950 font-bold text-xs sm:text-sm shadow-lg shadow-amber-500/20 flex items-center gap-2">
                <i data-lucide="sparkles" class="w-4 h-4"></i>
                <span>Buat Karakter Otomatis (AI)</span>
              </button>
            </div>
          </div>

          <!-- Visual Consistency Banner -->
          <div class="p-4 rounded-2xl bg-amber-500/10 border border-amber-500/30 flex items-start gap-3">
            <i data-lucide="shield-check" class="w-5 h-5 text-amber-500 shrink-0 mt-0.5"></i>
            <div class="text-xs sm:text-sm text-slate-700 dark:text-slate-200 leading-relaxed">
              <strong class="text-amber-600 dark:text-amber-300">Sistem Konsistensi Visual Karakter Aktif:</strong>
              Setiap karakter memiliki <em>Ciri Fisik</em>, <em>Gaya Pakaian</em>, dan <em>Foto Referensi AI</em> yang terkunci. Saat Anda membuat ilustrasi adegan atau thumbnail di episode mana pun, AI akan otomatis menggunakan wajah, fitur fisik, dan pakaian karakter ini agar tetap konsisten dari episode pertama hingga terakhir.
            </div>
          </div>

          <!-- Character Cards Grid -->
          ${chars.length === 0 ? `
            <div class="rounded-3xl bg-white dark:bg-studio-900 border border-dashed border-slate-300 dark:border-slate-700 p-10 text-center">
              <div class="w-14 h-14 rounded-2xl bg-amber-500/15 text-amber-500 flex items-center justify-center mx-auto mb-4">
                <i data-lucide="users" class="w-7 h-7"></i>
              </div>
              <h3 class="font-serif font-bold text-lg mb-2">Belum Ada Karakter dalam Serial Ini</h3>
              <p class="text-sm text-slate-500 dark:text-slate-400 max-w-md mx-auto mb-5">
                Klik tombol di bawah agar AI menciptakan jajaran tokoh lengkap sesuai genre dan sinopsis serial Anda.
              </p>
              <button onclick="aiGenerateCharacters()" class="px-6 py-3 rounded-2xl bg-amber-500 hover:bg-amber-400 text-slate-950 font-bold text-sm inline-flex items-center gap-2">
                <i data-lucide="sparkles" class="w-4 h-4"></i>
                <span>Generate Karakter Otomatis</span>
              </button>
            </div>
          ` : `
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
              ${chars.map(c => `
                <div class="rounded-3xl bg-white dark:bg-studio-900 border border-slate-200 dark:border-slate-800 overflow-hidden shadow-sm flex flex-col">
                  <!-- Top Portrait & Basic Identity -->
                  <div class="p-5 flex flex-col sm:flex-row gap-4 border-b border-slate-100 dark:border-slate-800">
                    <div class="w-full sm:w-32 h-40 sm:h-36 rounded-2xl bg-gradient-to-br from-slate-800 to-studio-950 border border-amber-500/30 overflow-hidden relative shrink-0 group">
                      ${c.imageUrl
                        ? `<img src="${c.imageUrl}" alt="${escapeHtml(c.name)}" class="w-full h-full object-cover">`
                        : `<div class="w-full h-full flex flex-col items-center justify-center p-2 text-center">
                            <span class="font-serif font-bold text-3xl text-amber-400 mb-1">${escapeHtml(c.name.charAt(0))}</span>
                            <span class="text-[10px] text-slate-400">Belum ada foto AI</span>
                          </div>`
                      }
                      <button onclick="aiGenerateCharacterPortrait('${c.id}')"
                        class="absolute inset-x-1.5 bottom-1.5 py-1.5 px-2 rounded-xl bg-slate-950/85 hover:bg-amber-500 text-white hover:text-slate-950 text-[10px] font-bold backdrop-blur-md flex items-center justify-center gap-1 transition-colors">
                        <i data-lucide="camera" class="w-3 h-3"></i>
                        <span>${c.imageUrl ? 'Buat Ulang Foto' : 'Foto Karakter AI'}</span>
                      </button>
                    </div>

                    <div class="flex-1 min-w-0">
                      <div class="flex items-start justify-between gap-2">
                        <div>
                          <span class="inline-block px-2.5 py-0.5 rounded-full text-[11px] font-bold bg-amber-500/15 text-amber-600 dark:text-amber-300 mb-1">
                            ${escapeHtml(c.role)}
                          </span>
                          <h3 class="font-serif font-bold text-xl text-slate-900 dark:text-white">${escapeHtml(c.name)}</h3>
                          <p class="text-xs text-slate-500 dark:text-slate-400">${escapeHtml(c.age)} • ${escapeHtml(c.gender)}</p>
                        </div>

                        <div class="flex items-center gap-1">
                          <button onclick="openCharacterFormModal('${c.id}')" title="Edit Karakter" class="p-2 rounded-xl bg-slate-100 dark:bg-studio-800 hover:text-amber-500 transition-colors">
                            <i data-lucide="pencil" class="w-4 h-4"></i>
                          </button>
                          <button onclick="confirmDeleteCharacter('${c.id}')" title="Hapus Karakter" class="p-2 rounded-xl bg-slate-100 dark:bg-studio-800 hover:text-rose-500 transition-colors">
                            <i data-lucide="trash-2" class="w-4 h-4"></i>
                          </button>
                        </div>
                      </div>

                      <div class="mt-3 text-xs text-slate-600 dark:text-slate-300 space-y-1">
                        <div><strong class="text-slate-800 dark:text-slate-200">Sifat:</strong> ${escapeHtml(c.personality)}</div>
                        <div><strong class="text-slate-800 dark:text-slate-200">Hubungan:</strong> ${escapeHtml(c.relationships)}</div>
                      </div>
                    </div>
                  </div>

                  <!-- Detailed Background & Visual Consistency Locks -->
                  <div class="p-5 space-y-3 text-xs flex-1 bg-slate-50/50 dark:bg-studio-950/30">
                    <div>
                      <span class="font-bold uppercase tracking-wider text-[10px] text-slate-400 block mb-0.5">Latar Belakang Kehidupan</span>
                      <p class="text-slate-700 dark:text-slate-300 leading-relaxed">${escapeHtml(c.background)}</p>
                    </div>
                    <div class="p-3 rounded-xl bg-white dark:bg-studio-850 border border-slate-200/80 dark:border-slate-800 space-y-2">
                      <div class="flex items-center gap-1.5 text-[10px] font-bold uppercase tracking-wider text-amber-600 dark:text-amber-400">
                        <i data-lucide="lock" class="w-3 h-3"></i>
                        <span>Kunci Konsistensi Visual Semua Episode</span>
                      </div>
                      <p class="text-slate-700 dark:text-slate-300"><strong>Ciri Fisik:</strong> ${escapeHtml(c.physicalTraits)}</p>
                      <p class="text-slate-700 dark:text-slate-300"><strong>Gaya Pakaian:</strong> ${escapeHtml(c.clothingStyle)}</p>
                    </div>
                  </div>
                </div>
              `).join('')}
            </div>
          `}

          <div class="pt-4 flex justify-end">
            <button onclick="navigateTo('plot')" class="px-6 py-3 rounded-2xl bg-amber-500 hover:bg-amber-400 text-slate-950 font-bold text-sm flex items-center gap-2 transition-colors">
              <span>Lanjut ke Generator Alur Cerita</span>
              <i data-lucide="arrow-right" class="w-4 h-4"></i>
            </button>
          </div>
        </div>
      `;
    }

    async function aiGenerateCharacters() {
      const proj = getActiveProject();
      const s = proj.settings;
      const genre = proj.customGenre || proj.genre;

      setLoading(true, 'Menciptakan Jajaran Pemeran Drama...', 'AI sedang merancang karakter utama & pendukung dengan latar belakang serta ciri visual konsisten.');
      try {
        const schema = {
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
        };

        const generated = await callGeminiText({
          systemPrompt: 'Kamu adalah Casting Director dan Penulis Karakter serial drama Indonesia. Buat 4 karakter utama dan pendukung yang memiliki dinamika konflik kuat, manusiawi, serta deskripsi fisik dan pakaian yang sangat spesifik agar mudah digambar secara konsisten di semua episode.',
          userPrompt: `Buatkan 4 karakter untuk serial drama berjudul "${s.title}" dengan genre "${genre}". Sinopsis: "${s.synopsis}". Latar tempat: "${s.settingPlace}", Zaman: "${s.era}".`,
          responseSchema: schema
        });

        proj.characters = generated.map((c, idx) => ({
          id: 'char_' + Date.now() + '_' + idx,
          ...c,
          imageUrl: ''
        }));

        saveState();
        renderApp();
        showToast(`${proj.characters.length} karakter berhasil dibuat oleh AI!`, 'success');
      } catch (err) {
        showToast('Gagal membuat karakter: ' + err.message, 'error');
      } finally {
        setLoading(false);
      }
    }

    async function aiGenerateCharacterPortrait(charId) {
      const proj = getActiveProject();
      const char = proj.characters.find(c => c.id === charId);
      if (!char) return;

      setLoading(true, `Membuat Foto Referensi: ${char.name}...`, 'AI sedang menghasilkan potret karakter resmi sebagai acuan visual di seluruh episode.');
      try {
        const prompt = `Character reference portrait photography for an Indonesian drama series titled "${proj.settings.title}" (${proj.settings.era}, ${proj.settings.settingPlace}).
Character Name: ${char.name}, ${char.age}, ${char.gender}.
Physical Features: ${char.physicalTraits}.
Signature Outfit: ${char.clothingStyle}.
Expression & Personality: ${char.personality}.
Style: Photorealistic 35mm cinema character portrait, chest-up medium close-up, dramatic studio & natural lighting, clear facial features, neutral atmospheric background, high detail.`;

        const imageUrl = await callGeminiImage({
          prompt,
          aspectRatio: '3:4',
          useAdvanced: true
        });

        char.imageUrl = imageUrl;
        proj.gallery.unshift({
          id: 'img_' + Date.now(),
          category: 'Foto setiap karakter',
          title: `Potret Referensi: ${char.name}`,
          styleName: 'Realistis seperti film layar lebar',
          prompt,
          imageUrl,
          createdAt: new Date().toISOString()
        });

        saveState();
        renderApp();
        showToast(`Foto referensi ${char.name} berhasil dibuat & dikunci!`, 'success');
      } catch (err) {
        showToast('Gagal membuat foto karakter: ' + err.message, 'error');
      } finally {
        setLoading(false);
      }
    }

    function openCharacterFormModal(charId = null) {
      const proj = getActiveProject();
      const existing = charId ? proj.characters.find(c => c.id === charId) : null;
      const c = existing || {
        name: '', age: '', gender: 'Perempuan', role: 'Karakter Pendukung',
        personality: '', background: '', relationships: '', physicalTraits: '', clothingStyle: ''
      };

      openModal(`
        <div class="flex items-center justify-between mb-4">
          <h3 class="font-serif font-bold text-xl">${existing ? 'Edit Karakter' : 'Tambah Karakter Baru'}</h3>
          <button onclick="closeModal()" class="p-1.5 rounded-lg hover:bg-slate-100 dark:hover:bg-studio-800 text-slate-400">
            <i data-lucide="x" class="w-5 h-5"></i>
          </button>
        </div>
        <div class="grid grid-cols-1 sm:grid-cols-2 gap-3.5 text-sm max-h-[70vh] overflow-y-auto pr-1">
          <div>
            <label class="block text-xs font-semibold text-slate-500 mb-1">Nama Karakter *</label>
            <input id="cf-name" type="text" value="${escapeHtml(c.name)}" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-50 dark:bg-studio-850 border border-slate-300 dark:border-slate-700" />
          </div>
          <div>
            <label class="block text-xs font-semibold text-slate-500 mb-1">Peran dalam Cerita</label>
            <input id="cf-role" type="text" value="${escapeHtml(c.role)}" placeholder="Protagonis, Antagonis, Mentor..." class="w-full px-3.5 py-2.5 rounded-xl bg-slate-50 dark:bg-studio-850 border border-slate-300 dark:border-slate-700" />
          </div>
          <div>
            <label class="block text-xs font-semibold text-slate-500 mb-1">Usia</label>
            <input id="cf-age" type="text" value="${escapeHtml(c.age)}" placeholder="Contoh: 28 Tahun" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-50 dark:bg-studio-850 border border-slate-300 dark:border-slate-700" />
          </div>
          <div>
            <label class="block text-xs font-semibold text-slate-500 mb-1">Jenis Kelamin</label>
            <select id="cf-gender" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-50 dark:bg-studio-850 border border-slate-300 dark:border-slate-700">
              <option value="Laki-laki" ${c.gender === 'Laki-laki' ? 'selected' : ''}>Laki-laki</option>
              <option value="Perempuan" ${c.gender === 'Perempuan' ? 'selected' : ''}>Perempuan</option>
            </select>
          </div>
          <div class="sm:col-span-2">
            <label class="block text-xs font-semibold text-slate-500 mb-1">Sifat dan Kepribadian</label>
            <input id="cf-personality" type="text" value="${escapeHtml(c.personality)}" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-50 dark:bg-studio-850 border border-slate-300 dark:border-slate-700" />
          </div>
          <div class="sm:col-span-2">
            <label class="block text-xs font-semibold text-slate-500 mb-1">Latar Belakang Kehidupan</label>
            <textarea id="cf-background" rows="2" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-50 dark:bg-studio-850 border border-slate-300 dark:border-slate-700">${escapeHtml(c.background)}</textarea>
          </div>
          <div class="sm:col-span-2">
            <label class="block text-xs font-semibold text-slate-500 mb-1">Hubungan dengan Karakter Lain</label>
            <input id="cf-relationships" type="text" value="${escapeHtml(c.relationships)}" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-50 dark:bg-studio-850 border border-slate-300 dark:border-slate-700" />
          </div>
          <div class="sm:col-span-2">
            <label class="block text-xs font-semibold text-amber-500 mb-1">Ciri Fisik (Acuan Konsistensi Wajah)</label>
            <input id="cf-physical" type="text" value="${escapeHtml(c.physicalTraits)}" placeholder="Wajah oval, kulit sawo matang, rambut ikal sebahu, tatapan lembut..." class="w-full px-3.5 py-2.5 rounded-xl bg-slate-50 dark:bg-studio-850 border border-amber-500/40" />
          </div>
          <div class="sm:col-span-2">
            <label class="block text-xs font-semibold text-amber-500 mb-1">Gaya Pakaian (Acuan Konsistensi Kostum)</label>
            <input id="cf-clothing" type="text" value="${escapeHtml(c.clothingStyle)}" placeholder="Kebaya kutubaru modern warna biru laut, selendang batik..." class="w-full px-3.5 py-2.5 rounded-xl bg-slate-50 dark:bg-studio-850 border border-amber-500/40" />
          </div>
        </div>
        <div class="flex justify-end gap-2 mt-5 pt-4 border-t border-slate-200 dark:border-slate-800">
          <button onclick="closeModal()" class="px-4 py-2.5 rounded-xl bg-slate-200 dark:bg-studio-800 text-sm font-semibold">Batal</button>
          <button onclick="saveCharacterForm('${charId || ''}')" class="px-5 py-2.5 rounded-xl bg-amber-500 hover:bg-amber-400 text-slate-950 text-sm font-bold">Simpan Karakter</button>
        </div>
      `);
    }

    function saveCharacterForm(charId) {
      const name = document.getElementById('cf-name').value.trim();
      if (!name) {
        showToast('Nama karakter wajib diisi.', 'warning');
        return;
      }
      const proj = getActiveProject();
      const updatedData = {
        name,
        role: document.getElementById('cf-role').value.trim() || 'Karakter Pendukung',
        age: document.getElementById('cf-age').value.trim() || 'Dewasa',
        gender: document.getElementById('cf-gender').value,
        personality: document.getElementById('cf-personality').value.trim(),
        background: document.getElementById('cf-background').value.trim(),
        relationships: document.getElementById('cf-relationships').value.trim(),
        physicalTraits: document.getElementById('cf-physical').value.trim(),
        clothingStyle: document.getElementById('cf-clothing').value.trim()
      };

      if (charId) {
        const idx = proj.characters.findIndex(c => c.id === charId);
        if (idx !== -1) {
          proj.characters[idx] = { ...proj.characters[idx], ...updatedData };
        }
      } else {
        proj.characters.push({
          id: 'char_' + Date.now(),
          ...updatedData,
          imageUrl: ''
        });
      }

      closeModal();
      saveState();
      renderApp();
      showToast('Data karakter berhasil disimpan!', 'success');
    }

    function confirmDeleteCharacter(charId) {
      const proj = getActiveProject();
      const char = proj.characters.find(c => c.id === charId);
      if (!char) return;
      openModal(`
        <h3 class="font-serif font-bold text-lg mb-2">Hapus Karakter "${escapeHtml(char.name)}"?</h3>
        <p class="text-sm text-slate-500 dark:text-slate-400 mb-5">Karakter akan dihapus dari daftar pemeran proyek ini.</p>
        <div class="flex justify-end gap-2">
          <button onclick="closeModal()" class="px-4 py-2 rounded-xl bg-slate-200 dark:bg-studio-800 text-sm font-semibold">Batal</button>
          <button onclick="deleteCharacter('${charId}')" class="px-4 py-2 rounded-xl bg-rose-600 hover:bg-rose-500 text-white text-sm font-bold">Ya, Hapus</button>
        </div>
      `);
    }

    function deleteCharacter(charId) {
      const proj = getActiveProject();
      proj.characters = proj.characters.filter(c => c.id !== charId);
      closeModal();
      saveState();
      renderApp();
      showToast('Karakter dihapus.', 'info');
    }

    /**
     * =========================================================================
     * 9. RENDER HALAMAN E: GENERATOR ALUR CERITA BERSERI
     * =========================================================================
     */
    function renderPlotView() {
      const proj = getActiveProject();
      const arc = proj.storyArc;

      return `
        <div class="space-y-6 animate-fade-in">
          <div class="flex flex-col md:flex-row md:items-center justify-between gap-4">
            <div>
              <span class="text-xs font-bold uppercase tracking-wider text-amber-500">Tahap 3 • Struktur Dramatik & Kontinuitas</span>
              <h1 class="font-serif font-bold text-2xl sm:text-3xl mt-1">Generator Alur Cerita Berseri</h1>
            </div>
            <button onclick="aiGenerateStoryArc()" class="px-5 py-3 rounded-2xl bg-gradient-to-r from-amber-500 to-orange-500 hover:from-amber-400 hover:to-orange-400 text-slate-950 font-bold text-xs sm:text-sm shadow-lg shadow-amber-500/20 flex items-center justify-center gap-2">
              <i data-lucide="sparkles" class="w-4 h-4"></i>
              <span>${arc ? 'Buat Ulang Seluruh Alur Serial' : 'Buat Alur Cerita & Outline Episode (AI)'}</span>
            </button>
          </div>

          ${!arc ? `
            <div class="rounded-3xl bg-white dark:bg-studio-900 border border-dashed border-slate-300 dark:border-slate-700 p-10 text-center">
              <div class="w-14 h-14 rounded-2xl bg-amber-500/15 text-amber-500 flex items-center justify-center mx-auto mb-4">
                <i data-lucide="git-branch" class="w-7 h-7"></i>
              </div>
              <h3 class="font-serif font-bold text-lg mb-2">Alur Serial Belum Dirancang</h3>
              <p class="text-sm text-slate-500 dark:text-slate-400 max-w-lg mx-auto mb-5">
                AI akan menyusun konflik utama, konflik tambahan, klimaks, plot twist, penyelesaian cerita, hubungan antar tokoh, serta alur Episode 1 sampai ${proj.settings.episodeCount} yang saling terhubung erat.
              </p>
              <button onclick="aiGenerateStoryArc()" class="px-6 py-3 rounded-2xl bg-amber-500 hover:bg-amber-400 text-slate-950 font-bold text-sm inline-flex items-center gap-2">
                <i data-lucide="sparkles" class="w-4 h-4"></i>
                <span>Rancang Alur Cerita Sekarang</span>
              </button>
            </div>
          ` : `
            <!-- Series Master Blueprint -->
            <div class="grid grid-cols-1 lg:grid-cols-3 gap-5">
              <div class="lg:col-span-2 rounded-3xl bg-white dark:bg-studio-900 border border-slate-200 dark:border-slate-800 p-6 space-y-5">
                <div>
                  <span class="text-[11px] font-bold uppercase tracking-wider text-amber-500">Ide Cerita & Premis Inti</span>
                  <p class="font-serif font-bold text-lg sm:text-xl text-slate-900 dark:text-white mt-1 leading-snug">"${escapeHtml(arc.storyIdea)}"</p>
                </div>

                <div>
                  <span class="text-[11px] font-bold uppercase tracking-wider text-slate-400">Sinopsis Lengkap Serial</span>
                  <p class="text-sm text-slate-700 dark:text-slate-300 mt-1 leading-relaxed">${escapeHtml(arc.fullSynopsis)}</p>
                </div>

                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 pt-2">
                  <div class="p-4 rounded-2xl bg-rose-500/10 border border-rose-500/25">
                    <div class="text-xs font-bold text-rose-600 dark:text-rose-400 uppercase tracking-wider mb-1">Konflik Utama</div>
                    <p class="text-xs sm:text-sm text-slate-700 dark:text-slate-200 leading-relaxed">${escapeHtml(arc.mainConflict)}</p>
                  </div>
                  <div class="p-4 rounded-2xl bg-indigo-500/10 border border-indigo-500/25">
                    <div class="text-xs font-bold text-indigo-600 dark:text-indigo-400 uppercase tracking-wider mb-1">Konflik Tambahan (Subplot)</div>
                    <p class="text-xs sm:text-sm text-slate-700 dark:text-slate-200 leading-relaxed">${escapeHtml(arc.subConflicts)}</p>
                  </div>
                </div>
              </div>

              <!-- Climax, Twist, Resolution & Dynamics -->
              <div class="rounded-3xl bg-white dark:bg-studio-900 border border-slate-200 dark:border-slate-800 p-6 space-y-4">
                <div>
                  <span class="text-[11px] font-bold uppercase tracking-wider text-amber-500 flex items-center gap-1.5">
                    <i data-lucide="zap" class="w-3.5 h-3.5"></i> Klimaks Serial
                  </span>
                  <p class="text-xs sm:text-sm text-slate-700 dark:text-slate-300 mt-1 leading-relaxed">${escapeHtml(arc.climax)}</p>
                </div>

                <div class="p-3.5 rounded-2xl bg-amber-500/10 border border-amber-500/30">
                  <span class="text-[11px] font-bold uppercase tracking-wider text-amber-600 dark:text-amber-300 flex items-center gap-1.5">
                    <i data-lucide="shuffle" class="w-3.5 h-3.5"></i> Plot Twist Besar
                  </span>
                  <p class="text-xs sm:text-sm text-slate-800 dark:text-slate-200 mt-1 leading-relaxed">${escapeHtml(arc.plotTwist)}</p>
                </div>

                <div>
                  <span class="text-[11px] font-bold uppercase tracking-wider text-emerald-500 flex items-center gap-1.5">
                    <i data-lucide="check-circle" class="w-3.5 h-3.5"></i> Penyelesaian Cerita
                  </span>
                  <p class="text-xs sm:text-sm text-slate-700 dark:text-slate-300 mt-1 leading-relaxed">${escapeHtml(arc.resolution)}</p>
                </div>

                <div class="pt-3 border-t border-slate-100 dark:border-slate-800">
                  <span class="text-[11px] font-bold uppercase tracking-wider text-slate-400">Dinamika Hubungan Antar Tokoh</span>
                  <p class="text-xs text-slate-600 dark:text-slate-300 mt-1 leading-relaxed">${escapeHtml(arc.characterDynamics)}</p>
                </div>
              </div>
            </div>

            <!-- Serialized Episode-by-Episode Timeline -->
            <section class="rounded-3xl bg-white dark:bg-studio-900 border border-slate-200 dark:border-slate-800 p-6">
              <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-2 mb-6">
                <div>
                  <h2 class="font-serif font-bold text-xl">Alur Cerita Setiap Episode (Saling Terhubung)</h2>
                  <p class="text-xs text-slate-500 dark:text-slate-400">Setiap episode dirancang sebagai mata rantai berkelanjutan menuju klimaks dan penyelesaian serial.</p>
                </div>
              </div>

              <div class="space-y-4">
                ${(arc.episodes || []).map(ep => {
                  const hasScript = Boolean(proj.scripts?.[ep.episodeNumber]);
                  return `
                    <div class="p-5 rounded-2xl bg-slate-50 dark:bg-studio-850 border border-slate-200/80 dark:border-slate-800 hover:border-amber-500/40 transition-all">
                      <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-3 mb-2">
                        <div class="flex items-center gap-3">
                          <span class="px-3 py-1 rounded-xl bg-amber-500 text-slate-950 font-bold text-xs">
                            EPISODE ${ep.episodeNumber}
                          </span>
                          <h3 class="font-serif font-bold text-lg text-slate-900 dark:text-white">${escapeHtml(ep.title)}</h3>
                        </div>
                        <button onclick="appState.selectedEpisodeNumber=${ep.episodeNumber}; navigateTo('script');"
                          class="px-4 py-2 rounded-xl ${hasScript ? 'bg-emerald-500/15 text-emerald-600 dark:text-emerald-300 border border-emerald-500/30' : 'bg-amber-500/15 text-amber-600 dark:text-amber-300 border border-amber-500/30'} hover:bg-amber-500 hover:text-slate-950 font-semibold text-xs flex items-center gap-1.5 transition-colors self-start sm:self-auto">
                          <i data-lucide="file-text" class="w-3.5 h-3.5"></i>
                          <span>${hasScript ? 'Buka Naskah Episode' : 'Tulis Naskah Episode'}</span>
                        </button>
                      </div>

                      <p class="text-sm text-slate-700 dark:text-slate-300 leading-relaxed mb-3">${escapeHtml(ep.summary)}</p>

                      <div class="grid grid-cols-1 md:grid-cols-2 gap-3 text-xs">
                        <div class="p-3 rounded-xl bg-white dark:bg-studio-900 border border-slate-200/70 dark:border-slate-800">
                          <span class="font-bold text-sky-600 dark:text-sky-400">Benang Merah Cerita Utama:</span>
                          <span class="text-slate-600 dark:text-slate-300"> ${escapeHtml(ep.connectionToMainArc)}</span>
                        </div>
                        <div class="p-3 rounded-xl bg-white dark:bg-studio-900 border border-slate-200/70 dark:border-slate-800">
                          <span class="font-bold text-amber-600 dark:text-amber-400">Cliffhanger Penutup:</span>
                          <span class="text-slate-600 dark:text-slate-300"> ${escapeHtml(ep.cliffhanger)}</span>
                        </div>
                      </div>
                    </div>
                  `;
                }).join('')}
              </div>
            </section>
          `}
        </div>
      `;
    }

    async function aiGenerateStoryArc() {
      const proj = getActiveProject();
      const s = proj.settings;
      const genre = proj.customGenre || proj.genre;
      const charSummary = (proj.characters || []).map(c => `${c.name} (${c.role}: ${c.personality})`).join('; ');

      setLoading(true, 'Menyusun Alur Cerita Berseri...', `AI sedang merangkai ${s.episodeCount} episode yang saling terhubung dengan konflik utama, klimaks, dan plot twist.`);
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

        const arcData = await callGeminiText({
          systemPrompt: 'Kamu adalah Kepala Penulis Skenario Serial Drama (Showrunner). Buat alur cerita serial drama yang sangat terstruktur dan saling bersambung dari episode 1 hingga episode terakhir. JANGAN membuat episode berdiri sendiri tanpa kaitan dengan cerita utama.',
          userPrompt: `Buatkan alur cerita lengkap untuk serial drama "${s.title}" (Genre: ${genre}).
Tema: ${s.theme}. Sinopsis awal: ${s.synopsis}. Latar: ${s.settingPlace} (${s.era}). Suasana: ${s.mood}. Gaya penceritaan: ${s.narrativeStyle}. Pesan moral: ${s.moralMessage}.
Karakter yang terlibat: ${charSummary || 'Buat karakter pendukung yang relevan'}.
Jumlah episode yang wajib dibuat: tepat ${s.episodeCount} episode (nomor 1 sampai ${s.episodeCount}).`,
          responseSchema: schema
        });

        proj.storyArc = arcData;
        saveState();
        renderApp();
        showToast('Alur cerita berseri berhasil dirancang!', 'success');
      } catch (err) {
        showToast('Gagal membuat alur cerita: ' + err.message, 'error');
      } finally {
        setLoading(false);
      }
    }

    /**
     * =========================================================================
     * 10. RENDER HALAMAN F: GENERATOR NASKAH EPISODE
     * =========================================================================
     */
    function renderScriptView() {
      const proj = getActiveProject();
      const totalEps = Number(proj.settings.episodeCount) || 5;
      const epNum = Math.min(Math.max(1, appState.selectedEpisodeNumber || 1), totalEps);
      appState.selectedEpisodeNumber = epNum;

      const script = proj.scripts?.[epNum];
      const outline = proj.storyArc?.episodes?.find(e => Number(e.episodeNumber) === epNum);

      return `
        <div class="space-y-6 animate-fade-in">
          <!-- Header & Episode Selector -->
          <div class="flex flex-col lg:flex-row lg:items-center justify-between gap-4">
            <div>
              <span class="text-xs font-bold uppercase tracking-wider text-amber-500">Tahap 4 • Ruang Penulisan Skenario</span>
              <h1 class="font-serif font-bold text-2xl sm:text-3xl mt-1">Generator Naskah Episode</h1>
            </div>

            <!-- Episode Pills -->
            <div class="flex items-center gap-1.5 overflow-x-auto no-scrollbar pb-1">
              ${Array.from({ length: totalEps }, (_, i) => i + 1).map(num => {
                const isSelected = num === epNum;
                const isWritten = Boolean(proj.scripts?.[num]);
                return `
                  <button onclick="appState.selectedEpisodeNumber=${num}; appState.isEditingScript=false; renderApp();"
                    class="px-3.5 py-2 rounded-xl text-xs font-bold whitespace-nowrap flex items-center gap-1.5 border transition-all ${
                      isSelected
                        ? 'bg-amber-500 text-slate-950 border-amber-500 shadow-md shadow-amber-500/20'
                        : isWritten
                          ? 'bg-emerald-500/10 text-emerald-600 dark:text-emerald-300 border-emerald-500/30 hover:border-amber-500'
                          : 'bg-white dark:bg-studio-900 text-slate-600 dark:text-slate-300 border-slate-200 dark:border-slate-800 hover:border-amber-500'
                    }">
                    <span>Ep ${num}</span>
                    ${isWritten ? `<span class="w-1.5 h-1.5 rounded-full ${isSelected ? 'bg-slate-950' : 'bg-emerald-400'}"></span>` : ''}
                  </button>
                `;
              }).join('')}
            </div>
          </div>

          <!-- Outline Context Banner if Available -->
          ${outline ? `
            <div class="p-4 rounded-2xl bg-slate-100/80 dark:bg-studio-900 border border-slate-200 dark:border-slate-800 flex flex-col sm:flex-row sm:items-center justify-between gap-3">
              <div class="text-xs sm:text-sm">
                <span class="font-bold text-amber-600 dark:text-amber-400">Panduan Alur Episode ${epNum} (${escapeHtml(outline.title)}):</span>
                <span class="text-slate-600 dark:text-slate-300"> ${escapeHtml(outline.summary)}</span>
              </div>
            </div>
          ` : ''}

          <!-- ACTION BUTTONS BAR -->
          <div class="p-4 rounded-3xl bg-white dark:bg-studio-900 border border-slate-200 dark:border-slate-800 flex flex-wrap items-center gap-2.5">
            <button onclick="aiGenerateEpisodeScript(${epNum})"
              class="px-4 py-2.5 rounded-xl bg-gradient-to-r from-amber-500 to-orange-500 hover:from-amber-400 hover:to-orange-400 text-slate-950 font-bold text-xs sm:text-sm shadow-md shadow-amber-500/20 flex items-center gap-2">
              <i data-lucide="sparkles" class="w-4 h-4"></i>
              <span>Buat Episode</span>
            </button>

            <button onclick="aiRefineEpisodeScript(${epNum}, 'dialogue')" ${!script ? 'disabled' : ''}
              class="px-3.5 py-2.5 rounded-xl bg-slate-100 dark:bg-studio-800 hover:bg-amber-500/15 disabled:opacity-40 text-xs sm:text-sm font-semibold flex items-center gap-1.5 transition-colors">
              <i data-lucide="message-square-quote" class="w-4 h-4 text-amber-500"></i>
              <span>Buat Ulang Dialog</span>
            </button>

            <button onclick="aiRefineEpisodeScript(${epNum}, 'extend')" ${!script ? 'disabled' : ''}
              class="px-3.5 py-2.5 rounded-xl bg-slate-100 dark:bg-studio-800 hover:bg-amber-500/15 disabled:opacity-40 text-xs sm:text-sm font-semibold flex items-center gap-1.5 transition-colors">
              <i data-lucide="plus-circle" class="w-4 h-4 text-sky-500"></i>
              <span>Perpanjang Cerita</span>
            </button>

            <button onclick="openChangeConflictModal(${epNum})" ${!script ? 'disabled' : ''}
              class="px-3.5 py-2.5 rounded-xl bg-slate-100 dark:bg-studio-800 hover:bg-amber-500/15 disabled:opacity-40 text-xs sm:text-sm font-semibold flex items-center gap-1.5 transition-colors">
              <i data-lucide="flame" class="w-4 h-4 text-rose-500"></i>
              <span>Ubah Konflik</span>
            </button>

            <button onclick="toggleEditScriptMode()" ${!script ? 'disabled' : ''}
              class="px-3.5 py-2.5 rounded-xl ${appState.isEditingScript ? 'bg-emerald-500 text-slate-950 font-bold' : 'bg-slate-100 dark:bg-studio-800 hover:bg-amber-500/15 font-semibold'} disabled:opacity-40 text-xs sm:text-sm flex items-center gap-1.5 transition-colors">
              <i data-lucide="${appState.isEditingScript ? 'check' : 'edit-3'}" class="w-4 h-4"></i>
              <span>${appState.isEditingScript ? 'Selesai Edit' : 'Edit Naskah'}</span>
            </button>

            ${epNum < totalEps ? `
              <button onclick="continueToNextEpisode(${epNum})"
                class="ml-auto px-4 py-2.5 rounded-xl bg-indigo-600 hover:bg-indigo-500 text-white font-bold text-xs sm:text-sm flex items-center gap-1.5 transition-colors">
                <span>Lanjutkan ke Episode Berikutnya</span>
                <i data-lucide="arrow-right" class="w-4 h-4"></i>
              </button>
            ` : ''}
          </div>

          <!-- SCRIPT DISPLAY OR EMPTY STATE -->
          ${!script ? `
            <div class="rounded-3xl bg-white dark:bg-studio-900 border border-dashed border-slate-300 dark:border-slate-700 p-10 text-center">
              <div class="w-14 h-14 rounded-2xl bg-amber-500/15 text-amber-500 flex items-center justify-center mx-auto mb-4">
                <i data-lucide="file-text" class="w-7 h-7"></i>
              </div>
              <h3 class="font-serif font-bold text-xl mb-2">Naskah Episode ${epNum} Belum Dibuat</h3>
              <p class="text-sm text-slate-500 dark:text-slate-400 max-w-lg mx-auto mb-6">
                Klik tombol <strong>Buat Episode</strong> agar AI menyusun naskah lengkap meliputi adegan pembuka yang memikat, pembagian adegan, deskripsi lokasi, dialog beremosi, arahan gerakan kamera, musik pendukung, dan cliffhanger penutup.
              </p>
              <button onclick="aiGenerateEpisodeScript(${epNum})" class="px-6 py-3.5 rounded-2xl bg-amber-500 hover:bg-amber-400 text-slate-950 font-bold text-sm inline-flex items-center gap-2 shadow-lg shadow-amber-500/20">
                <i data-lucide="sparkles" class="w-4 h-4"></i>
                <span>Buat Episode ${epNum} Sekarang</span>
              </button>
            </div>
          ` : appState.isEditingScript ? renderScriptEditor(script, epNum) : renderScriptReader(script, epNum)}
        </div>
      `;
    }

    function renderScriptReader(script, epNum) {
      const activeAudio = appState.audioPlayer && appState.audioPlayer.epNum === epNum ? appState.audioPlayer : null;
      return `
        <div class="rounded-3xl bg-white dark:bg-studio-900 border border-slate-200 dark:border-slate-800 overflow-hidden shadow-sm">
          <!-- Screenplay Cover Header -->
          <div class="p-6 sm:p-8 bg-gradient-to-r from-studio-900 via-studio-850 to-slate-900 text-white border-b border-slate-800">
            <div class="flex flex-wrap items-center justify-between gap-3 mb-3">
              <span class="px-3 py-1 rounded-full bg-amber-500/20 border border-amber-400/30 text-amber-300 text-xs font-bold tracking-wider">
                EPISODE ${script.episodeNumber}
              </span>
              <div class="flex flex-wrap items-center gap-2">
                <select onchange="appState.selectedVoice = this.value" title="Pilih Karakter Suara AI"
                  class="px-2.5 py-1.5 rounded-xl bg-white/10 border border-white/15 text-xs text-white focus:outline-none">
                  <option value="Kore" class="text-slate-900" ${appState.selectedVoice === 'Kore' ? 'selected' : ''}>Suara: Kore (Dramatis)</option>
                  <option value="Aoede" class="text-slate-900" ${appState.selectedVoice === 'Aoede' ? 'selected' : ''}>Suara: Aoede (Lembut)</option>
                  <option value="Puck" class="text-slate-900" ${appState.selectedVoice === 'Puck' ? 'selected' : ''}>Suara: Puck (Ekspresif)</option>
                  <option value="Charon" class="text-slate-900" ${appState.selectedVoice === 'Charon' ? 'selected' : ''}>Suara: Charon (Berwibawa)</option>
                </select>
                <button onclick="playEpisodeAudioPreview(${epNum})" class="px-3.5 py-1.5 rounded-xl bg-amber-500 hover:bg-amber-400 text-slate-950 text-xs font-bold flex items-center gap-1.5 transition-colors">
                  <i data-lucide="volume-2" class="w-3.5 h-3.5"></i>
                  <span>Dengarkan Pembacaan AI</span>
                </button>
                <button onclick="copyEpisodeScriptText(${epNum})" class="px-3.5 py-1.5 rounded-xl bg-white/10 hover:bg-white/20 text-xs font-semibold flex items-center gap-1.5 transition-colors">
                  <i data-lucide="copy" class="w-3.5 h-3.5 text-amber-400"></i>
                  <span>Salin Naskah</span>
                </button>
              </div>
            </div>

            ${activeAudio ? `
              <div class="mb-4 p-3.5 rounded-2xl bg-slate-950/80 border border-amber-400/40 flex flex-col sm:flex-row sm:items-center justify-between gap-3">
                <div class="flex items-center gap-2.5 text-xs">
                  <span class="w-2.5 h-2.5 rounded-full bg-amber-400 animate-ping"></span>
                  <div>
                    <div class="font-bold text-amber-300">Pemutar Suara Naskah Episode ${epNum}</div>
                    <div class="text-slate-400 text-[11px]">${activeAudio.isFallback ? 'Mode Sulih Suara Browser (Bahasa Indonesia)' : 'Audio HD Gemini TTS (' + escapeHtml(activeAudio.voiceName) + ')'}</div>
                  </div>
                </div>
                <div class="flex items-center gap-2 flex-1 sm:justify-end">
                  ${activeAudio.audioUrl ? `
                    <audio id="episode-tts-audio" controls autoplay src="${activeAudio.audioUrl}" class="h-9 max-w-full sm:w-72 rounded-lg"></audio>
                    <a href="${activeAudio.audioUrl}" download="Audio_Episode_${epNum}.wav" title="Unduh Audio WAV" class="p-2 rounded-xl bg-white/10 hover:bg-amber-500 hover:text-slate-950 transition-colors">
                      <i data-lucide="download" class="w-4 h-4"></i>
                    </a>
                  ` : `
                    <button onclick="playBrowserSpeechFallback(${epNum})" class="px-3 py-1.5 rounded-xl bg-amber-500 text-slate-950 font-bold text-xs">Putar Ulang</button>
                  `}
                  <button onclick="stopEpisodeAudio()" title="Tutup Pemutar" class="p-2 rounded-xl bg-white/10 hover:bg-rose-500/80 transition-colors">
                    <i data-lucide="x" class="w-4 h-4"></i>
                  </button>
                </div>
              </div>
            ` : ''}

            <h2 class="font-serif font-bold text-2xl sm:text-3xl mb-3">${escapeHtml(script.title)}</h2>
            <p class="text-sm text-slate-300 leading-relaxed mb-5">${escapeHtml(script.summary)}</p>

            <!-- Adegan Pembuka yang Menarik -->
            <div class="p-4 rounded-2xl bg-amber-500/10 border border-amber-400/30">
              <div class="text-[11px] font-bold uppercase tracking-wider text-amber-300 mb-1 flex items-center gap-1.5">
                <i data-lucide="clapperboard" class="w-3.5 h-3.5"></i>
                <span>Adegan Pembuka yang Menarik (Cold Open / Hook)</span>
              </div>
              <p class="text-xs sm:text-sm text-slate-200 leading-relaxed">${escapeHtml(script.openingHook)}</p>
            </div>
          </div>

          <!-- Pembagian Adegan -->
          <div class="p-6 sm:p-8 space-y-8">
            ${(script.scenes || []).map((scene, sIdx) => `
              <div class="rounded-2xl border border-slate-200 dark:border-slate-800 bg-slate-50/60 dark:bg-studio-950/40 overflow-hidden">
                <!-- Scene Heading Bar -->
                <div class="px-5 py-3.5 bg-slate-200/70 dark:bg-studio-850 border-b border-slate-200 dark:border-slate-800 flex flex-col sm:flex-row sm:items-center justify-between gap-2">
                  <div class="font-mono font-bold text-xs sm:text-sm text-slate-900 dark:text-amber-300">
                    ADEGAN ${scene.sceneNumber || sIdx + 1} • ${escapeHtml(scene.heading)}
                  </div>
                  <button onclick="aiGenerateSceneIllustration(${epNum}, ${sIdx})"
                    class="px-3 py-1.5 rounded-xl bg-amber-500 hover:bg-amber-400 text-slate-950 font-bold text-xs flex items-center gap-1.5 self-start sm:self-auto transition-colors">
                    <i data-lucide="image" class="w-3.5 h-3.5"></i>
                    <span>Ilustrasi Adegan AI</span>
                  </button>
                </div>

                <div class="p-5 space-y-4">
                  <!-- Metadata Grid -->
                  <div class="grid grid-cols-1 md:grid-cols-2 gap-3 text-xs">
                    <div class="p-3 rounded-xl bg-white dark:bg-studio-900 border border-slate-200/70 dark:border-slate-800">
                      <span class="font-bold text-slate-400 uppercase block text-[10px] mb-0.5">Deskripsi Lokasi</span>
                      <span class="text-slate-700 dark:text-slate-300">${escapeHtml(scene.locationDesc)}</span>
                    </div>
                    <div class="p-3 rounded-xl bg-white dark:bg-studio-900 border border-slate-200/70 dark:border-slate-800">
                      <span class="font-bold text-slate-400 uppercase block text-[10px] mb-0.5">Karakter yang Tampil</span>
                      <div class="flex flex-wrap gap-1.5 mt-1">
                        ${(scene.charactersPresent || []).map(cName => `
                          <span class="px-2 py-0.5 rounded-md bg-amber-500/15 text-amber-700 dark:text-amber-300 font-semibold">${escapeHtml(cName)}</span>
                        `).join('')}
                      </div>
                    </div>
                    <div class="p-3 rounded-xl bg-white dark:bg-studio-900 border border-slate-200/70 dark:border-slate-800">
                      <span class="font-bold text-sky-500 uppercase block text-[10px] mb-0.5">Arahan Gerakan Kamera & Visual</span>
                      <span class="text-slate-700 dark:text-slate-300">${escapeHtml(scene.cameraDirection)} — ${escapeHtml(scene.visualDesc)}</span>
                    </div>
                    <div class="p-3 rounded-xl bg-white dark:bg-studio-900 border border-slate-200/70 dark:border-slate-800">
                      <span class="font-bold text-purple-500 uppercase block text-[10px] mb-0.5">Musik & Suasana Pendukung</span>
                      <span class="text-slate-700 dark:text-slate-300">${escapeHtml(scene.musicAmbience)}</span>
                    </div>
                  </div>

                  <!-- Narasi -->
                  ${scene.narration ? `
                    <div class="p-3.5 rounded-xl bg-amber-500/5 border-l-4 border-amber-500 italic text-xs sm:text-sm text-slate-700 dark:text-slate-300">
                      <strong class="not-italic text-amber-600 dark:text-amber-400 text-xs uppercase mr-1">Narasi:</strong>
                      ${escapeHtml(scene.narration)}
                    </div>
                  ` : ''}

                  <!-- Dialog Lengkap Setiap Tokoh -->
                  <div class="space-y-3 pt-2">
                    <div class="text-[11px] font-bold uppercase tracking-wider text-slate-400">Dialog & Ekspresi Tokoh</div>
                    ${(scene.dialogue || []).map(d => `
                      <div class="pl-4 sm:pl-8 pr-2 py-2 rounded-xl bg-white dark:bg-studio-900/90 border border-slate-100 dark:border-slate-800/80">
                        <div class="flex flex-wrap items-center gap-2 mb-1">
                          <span class="font-mono font-bold text-xs sm:text-sm uppercase text-slate-900 dark:text-amber-300">${escapeHtml(d.character)}</span>
                          <span class="text-[11px] italic px-2 py-0.5 rounded-full bg-slate-100 dark:bg-studio-800 text-slate-500 dark:text-slate-400">
                            (${escapeHtml(d.emotion)})
                          </span>
                        </div>
                        <p class="text-sm text-slate-800 dark:text-slate-100 leading-relaxed">"${escapeHtml(d.line)}"</p>
                      </div>
                    `).join('')}
                  </div>
                </div>
              </div>
            `).join('')}

            <!-- Adegan Penutup -->
            <div class="p-5 rounded-2xl bg-gradient-to-r from-rose-950/90 to-studio-900 border border-rose-500/35 text-white">
              <div class="text-xs font-bold uppercase tracking-wider text-rose-300 mb-1.5 flex items-center gap-1.5">
                <i data-lucide="alert-circle" class="w-4 h-4"></i>
                <span>Adegan Penutup (Cliffhanger Penasaran)</span>
              </div>
              <p class="text-sm text-slate-200 leading-relaxed">${escapeHtml(script.closingCliffhanger)}</p>
            </div>
          </div>
        </div>
      `;
    }

    function renderScriptEditor(script, epNum) {
      return `
        <div class="rounded-3xl bg-white dark:bg-studio-900 border-2 border-amber-500 p-6 space-y-5">
          <div class="flex items-center justify-between border-b border-slate-200 dark:border-slate-800 pb-4">
            <h3 class="font-serif font-bold text-xl text-amber-500">Mode Edit Naskah Langsung — Episode ${epNum}</h3>
            <button onclick="saveEditedScript(${epNum})" class="px-5 py-2.5 rounded-xl bg-emerald-500 hover:bg-emerald-400 text-slate-950 font-bold text-xs sm:text-sm flex items-center gap-1.5">
              <i data-lucide="save" class="w-4 h-4"></i>
              <span>Simpan Perubahan</span>
            </button>
          </div>

          <div class="grid grid-cols-1 gap-4 text-sm">
            <div>
              <label class="block text-xs font-bold text-slate-400 mb-1">Judul Episode</label>
              <input id="edit-ep-title" type="text" value="${escapeHtml(script.title)}" class="w-full px-4 py-2.5 rounded-xl bg-slate-50 dark:bg-studio-850 border border-slate-300 dark:border-slate-700 font-bold" />
            </div>
            <div>
              <label class="block text-xs font-bold text-slate-400 mb-1">Ringkasan Episode</label>
              <textarea id="edit-ep-summary" rows="2" class="w-full px-4 py-2.5 rounded-xl bg-slate-50 dark:bg-studio-850 border border-slate-300 dark:border-slate-700">${escapeHtml(script.summary)}</textarea>
            </div>
            <div>
              <label class="block text-xs font-bold text-slate-400 mb-1">Adegan Pembuka (Hook)</label>
              <textarea id="edit-ep-hook" rows="2" class="w-full px-4 py-2.5 rounded-xl bg-slate-50 dark:bg-studio-850 border border-slate-300 dark:border-slate-700">${escapeHtml(script.openingHook)}</textarea>
            </div>
          </div>

          <div class="space-y-4">
            ${(script.scenes || []).map((sc, sIdx) => `
              <div class="p-4 rounded-2xl bg-slate-50 dark:bg-studio-850 border border-slate-200 dark:border-slate-700 space-y-3">
                <div class="font-bold text-xs text-amber-500">ADEGAN ${sIdx + 1}</div>
                <input id="edit-sc-head-${sIdx}" type="text" value="${escapeHtml(sc.heading)}" class="w-full px-3 py-2 rounded-xl bg-white dark:bg-studio-900 border border-slate-300 dark:border-slate-700 text-xs font-mono" />
                <textarea id="edit-sc-narr-${sIdx}" rows="2" placeholder="Narasi..." class="w-full px-3 py-2 rounded-xl bg-white dark:bg-studio-900 border border-slate-300 dark:border-slate-700 text-xs">${escapeHtml(sc.narration || '')}</textarea>
                <div class="space-y-2">
                  ${(sc.dialogue || []).map((d, dIdx) => `
                    <div class="grid grid-cols-1 sm:grid-cols-4 gap-2">
                      <input id="edit-dlg-char-${sIdx}-${dIdx}" type="text" value="${escapeHtml(d.character)}" class="px-3 py-2 rounded-xl bg-white dark:bg-studio-900 border border-slate-300 dark:border-slate-700 text-xs font-bold" />
                      <input id="edit-dlg-emo-${sIdx}-${dIdx}" type="text" value="${escapeHtml(d.emotion)}" class="px-3 py-2 rounded-xl bg-white dark:bg-studio-900 border border-slate-300 dark:border-slate-700 text-xs italic" />
                      <input id="edit-dlg-line-${sIdx}-${dIdx}" type="text" value="${escapeHtml(d.line)}" class="sm:col-span-2 px-3 py-2 rounded-xl bg-white dark:bg-studio-900 border border-slate-300 dark:border-slate-700 text-xs" />
                    </div>
                  `).join('')}
                </div>
              </div>
            `).join('')}
          </div>

          <div>
            <label class="block text-xs font-bold text-rose-400 mb-1">Adegan Penutup (Cliffhanger)</label>
            <textarea id="edit-ep-cliff" rows="2" class="w-full px-4 py-2.5 rounded-xl bg-slate-50 dark:bg-studio-850 border border-slate-300 dark:border-slate-700 text-sm">${escapeHtml(script.closingCliffhanger)}</textarea>
          </div>
        </div>
      `;
    }

    function toggleEditScriptMode() {
      appState.isEditingScript = !appState.isEditingScript;
      renderApp();
    }

    function saveEditedScript(epNum) {
      const proj = getActiveProject();
      const script = proj.scripts?.[epNum];
      if (!script) return;

      script.title = document.getElementById('edit-ep-title').value;
      script.summary = document.getElementById('edit-ep-summary').value;
      script.openingHook = document.getElementById('edit-ep-hook').value;
      script.closingCliffhanger = document.getElementById('edit-ep-cliff').value;

      (script.scenes || []).forEach((sc, sIdx) => {
        const headEl = document.getElementById(`edit-sc-head-${sIdx}`);
        const narrEl = document.getElementById(`edit-sc-narr-${sIdx}`);
        if (headEl) sc.heading = headEl.value;
        if (narrEl) sc.narration = narrEl.value;

        (sc.dialogue || []).forEach((d, dIdx) => {
          const charEl = document.getElementById(`edit-dlg-char-${sIdx}-${dIdx}`);
          const emoEl = document.getElementById(`edit-dlg-emo-${sIdx}-${dIdx}`);
          const lineEl = document.getElementById(`edit-dlg-line-${sIdx}-${dIdx}`);
          if (charEl) d.character = charEl.value;
          if (emoEl) d.emotion = emoEl.value;
          if (lineEl) d.line = lineEl.value;
        });
      });

      appState.isEditingScript = false;
      saveState();
      renderApp();
      showToast('Perubahan naskah berhasil disimpan!', 'success');
    }

    const SCRIPT_JSON_SCHEMA = {
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
      const s = proj.settings;
      const genre = proj.customGenre || proj.genre;
      const outline = proj.storyArc?.episodes?.find(e => Number(e.episodeNumber) === epNum);
      const prevScript = epNum > 1 ? proj.scripts?.[epNum - 1] : null;
      const charList = (proj.characters || []).map(c => `${c.name} (${c.role}, sifat: ${c.personality})`).join('; ');

      setLoading(true, `Menulis Naskah Episode ${epNum}...`, 'AI sedang menyusun adegan pembuka, dialog beremosi, arahan kamera, musik, dan cliffhanger.');
      try {
        const scriptData = await callGeminiText({
          systemPrompt: 'Kamu adalah Penulis Skenario & Sutradara serial drama profesional Indonesia. Tulis naskah episode yang hidup, emosional, sinematik, dengan pembagian adegan jelas, arahan kamera, dan dialog natural.',
          userPrompt: `Tulis naskah lengkap untuk Episode ${epNum} dari total ${s.episodeCount} episode serial drama "${s.title}" (Genre: ${genre}).
Latar tempat: ${s.settingPlace} (${s.era}). Suasana: ${s.mood}. Durasi target: ${s.episodeDuration}.
Karakter tersedia: ${charList || 'Gunakan tokoh utama yang sesuai cerita'}.
${outline ? `Panduan Alur Episode ${epNum}: Judul "${outline.title}", Ringkasan: ${outline.summary}, Cliffhanger: ${outline.cliffhanger}.` : `Sinopsis Serial: ${s.synopsis}.`}
${prevScript ? `Kelanjutan dari Episode ${epNum - 1} yang ditutup dengan: "${prevScript.closingCliffhanger}".` : 'Ini adalah episode perdana yang harus langsung memikat penonton.'}
Buat minimal 3 hingga 4 adegan lengkap beserta dialog, ekspresi emosi, gerakan kamera, dan musik suasana.`,
          responseSchema: SCRIPT_JSON_SCHEMA
        });

        scriptData.episodeNumber = epNum;
        proj.scripts[epNum] = scriptData;
        appState.isEditingScript = false;
        saveState();
        renderApp();
        showToast(`Naskah Episode ${epNum} berhasil dibuat!`, 'success');
      } catch (err) {
        showToast('Gagal membuat naskah episode: ' + err.message, 'error');
      } finally {
        setLoading(false);
      }
    }

    async function aiRefineEpisodeScript(epNum, mode, customInstruction = '') {
      const proj = getActiveProject();
      const currentScript = proj.scripts?.[epNum];
      if (!currentScript) return;

      const modeDescriptions = {
        dialogue: 'Memperdalam dialog agar lebih emosional, puitis, tajam, dan berkarakter tanpa mengubah alur utama.',
        extend: 'Memperpanjang cerita dengan menambahkan 2 adegan baru yang memperkaya pengembangan karakter dan ketegangan emosional.',
        conflict: `Mengubah dan mempertajam konflik dalam episode ini sesuai arahan: "${customInstruction}".`
      };

      setLoading(true, 'Menyempurnakan Naskah Episode...', modeDescriptions[mode]);
      try {
        const refined = await callGeminiText({
          systemPrompt: 'Kamu adalah Script Doctor & Penulis Skenario Drama senior. Revisi naskah yang diberikan sesuai instruksi dengan menjaga konsistensi nama tokoh, latar, dan keterkaitan cerita.',
          userPrompt: `Revisi naskah Episode ${epNum} berikut ini.
Tugas Revisi: ${modeDescriptions[mode]}
Naskah Saat Ini (JSON):
${JSON.stringify(currentScript)}`,
          responseSchema: SCRIPT_JSON_SCHEMA
        });

        refined.episodeNumber = epNum;
        proj.scripts[epNum] = refined;
        saveState();
        renderApp();
        showToast('Naskah episode berhasil diperbarui oleh AI!', 'success');
      } catch (err) {
        showToast('Gagal merevisi naskah: ' + err.message, 'error');
      } finally {
        setLoading(false);
      }
    }

    function openChangeConflictModal(epNum) {
      openModal(`
        <h3 class="font-serif font-bold text-xl mb-2">Ubah Konflik Episode ${epNum}</h3>
        <p class="text-xs sm:text-sm text-slate-500 dark:text-slate-400 mb-4">
          Jelaskan arah konflik baru atau kejutan dramatis yang ingin Anda masukkan ke dalam episode ini.
        </p>
        <textarea id="conflict-custom-input" rows="3" placeholder="Contoh: Tambahkan pengkhianatan dari sahabat dekat tokoh utama, atau munculnya rahasia surat wasiat yang memicu pertengkaran hebat..."
          class="w-full px-4 py-3 rounded-xl bg-slate-50 dark:bg-studio-850 border border-slate-300 dark:border-slate-700 text-sm mb-4"></textarea>
        <div class="flex justify-end gap-2">
          <button onclick="closeModal()" class="px-4 py-2 rounded-xl bg-slate-200 dark:bg-studio-800 text-sm font-semibold">Batal</button>
          <button onclick="submitChangeConflict(${epNum})" class="px-5 py-2 rounded-xl bg-amber-500 hover:bg-amber-400 text-slate-950 text-sm font-bold">Terapkan Konflik Baru</button>
        </div>
      `);
    }

    async function submitChangeConflict(epNum) {
      const val = document.getElementById('conflict-custom-input').value.trim();
      if (!val) {
        showToast('Tuliskan arah konflik baru terlebih dahulu.', 'warning');
        return;
      }
      closeModal();
      await aiRefineEpisodeScript(epNum, 'conflict', val);
    }

    async function continueToNextEpisode(currentEpNum) {
      const proj = getActiveProject();
      const nextEp = currentEpNum + 1;
      if (nextEp > Number(proj.settings.episodeCount)) return;

      appState.selectedEpisodeNumber = nextEp;
      saveState();
      if (!proj.scripts?.[nextEp]) {
        await aiGenerateEpisodeScript(nextEp);
      } else {
        renderApp();
        showToast(`Berpindah ke Episode ${nextEp}.`, 'info');
      }
    }

    function stopEpisodeAudio() {
      if (appState.currentAudio) {
        try {
          appState.currentAudio.pause();
        } catch (e) {}
        appState.currentAudio = null;
      }
      if ('speechSynthesis' in window) {
        try {
          window.speechSynthesis.cancel();
        } catch (e) {}
      }
      if (appState.audioPlayer?.audioUrl) {
        try {
          URL.revokeObjectURL(appState.audioPlayer.audioUrl);
        } catch (e) {}
      }
      appState.audioPlayer = null;
      renderApp();
    }

    function playBrowserSpeechFallback(epNum) {
      const proj = getActiveProject();
      const script = proj.scripts?.[epNum];
      if (!script || !('speechSynthesis' in window)) return;

      window.speechSynthesis.cancel();
      const firstScene = script.scenes?.[0];
      const sampleDialogue = firstScene?.dialogue?.slice(0, 3).map(d => `${d.character}. ${d.line}`).join('. ') || '';
      const textToRead = `Episode ${epNum}: ${script.title}. ${script.openingHook}. ${sampleDialogue}`;

      const utterance = new SpeechSynthesisUtterance(textToRead);
      utterance.lang = 'id-ID';
      utterance.rate = 0.96;
      const voices = window.speechSynthesis.getVoices();
      const idVoice = voices.find(v => v.lang && v.lang.toLowerCase().includes('id'));
      if (idVoice) utterance.voice = idVoice;
      window.speechSynthesis.speak(utterance);
    }

    async function playEpisodeAudioPreview(epNum) {
      const proj = getActiveProject();
      const script = proj.scripts?.[epNum];
      if (!script) return;

      stopEpisodeAudio();

      const firstScene = script.scenes?.[0];
      const sampleDialogue = firstScene?.dialogue?.slice(0, 3).map(d => `${d.character}: ${d.line}`).join('. ') || '';
      const textToRead = `Episode ${epNum}: ${script.title}. ${script.openingHook}. ${sampleDialogue}`;
      const chosenVoice = appState.selectedVoice || 'Kore';

      setLoading(true, 'Menyiapkan Pembacaan Dramatis (AI Voice)...', 'Sedang menghasilkan audio narasi dan cuplikan dialog pembuka.');
      try {
        const audioUrl = await callGeminiTTS(textToRead, chosenVoice);
        appState.audioPlayer = {
          epNum,
          title: script.title,
          audioUrl,
          voiceName: chosenVoice,
          isFallback: false
        };
        setLoading(false);
        renderApp();

        const audioEl = document.getElementById('episode-tts-audio');
        if (audioEl) {
          appState.currentAudio = audioEl;
          audioEl.play().catch(() => {
            showToast('Audio siap! Tekan tombol Play pada pemutar di atas jika browser menahan putar otomatis.', 'info');
          });
        }
        showToast('Audio pembacaan naskah siap diputar!', 'success');
      } catch (err) {
        setLoading(false);
        if ('speechSynthesis' in window) {
          appState.audioPlayer = {
            epNum,
            title: script.title,
            audioUrl: '',
            voiceName: 'Browser ID',
            isFallback: true
          };
          renderApp();
          playBrowserSpeechFallback(epNum);
          showToast('Memutar pembacaan naskah menggunakan suara Bahasa Indonesia perangkat Anda.', 'info');
        } else {
          showToast('Audio tidak dapat diputar di perangkat ini: ' + err.message, 'error');
        }
      }
    }

    function copyEpisodeScriptText(epNum) {
      const proj = getActiveProject();
      const s = proj.scripts?.[epNum];
      if (!s) return;
      let text = `${proj.settings.title.toUpperCase()}\nEPISODE ${s.episodeNumber}: ${s.title}\n\nRINGKASAN:\n${s.summary}\n\nADEGAN PEMBUKA:\n${s.openingHook}\n\n`;
      (s.scenes || []).forEach(sc => {
        text += `----------------------------------------\nADEGAN ${sc.sceneNumber} - ${sc.heading}\nLokasi: ${sc.locationDesc}\nKarakter: ${(sc.charactersPresent || []).join(', ')}\nKamera & Visual: ${sc.cameraDirection} | ${sc.visualDesc}\nMusik: ${sc.musicAmbience}\n\nNarasi: ${sc.narration}\n\n`;
        (sc.dialogue || []).forEach(d => {
          text += `${d.character.toUpperCase()} (${d.emotion}):\n"${d.line}"\n\n`;
        });
      });
      text += `----------------------------------------\nADEGAN PENUTUP (CLIFFHANGER):\n${s.closingCliffhanger}`;
      copyTextToClipboard(text);
    }

    /**
     * =========================================================================
     * 11. RENDER HALAMAN G: GENERATOR GAMBAR AI & STUDIO VISUAL
     * =========================================================================
     */
    function renderVisualsView() {
      const proj = getActiveProject();
      const chars = proj.characters || [];
      const totalEps = Number(proj.settings.episodeCount) || 5;
      const gallery = proj.gallery || [];

      return `
        <div class="space-y-8 animate-fade-in">
          <div>
            <span class="text-xs font-bold uppercase tracking-wider text-amber-500">Tahap 5 • Visualisasi Sinematik & Poster Resmi</span>
            <h1 class="font-serif font-bold text-2xl sm:text-3xl mt-1">Generator Gambar AI & Studio Poster</h1>
          </div>

          <!-- GENERATOR CONTROLS CARD -->
          <section class="rounded-3xl bg-white dark:bg-studio-900 border border-slate-200 dark:border-slate-800 p-6">
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-5">
              <!-- Jenis Gambar -->
              <div>
                <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 dark:text-slate-400 mb-1.5">1. Pilih Kategori Gambar</label>
                <select id="vis-category" onchange="handleVisualCategoryChange()"
                  class="w-full px-4 py-3 rounded-xl bg-slate-50 dark:bg-studio-850 border border-slate-300 dark:border-slate-700 text-sm font-semibold focus:outline-none focus:border-amber-500">
                  <option value="Poster utama serial">Poster utama serial</option>
                  <option value="Foto setiap karakter">Foto setiap karakter</option>
                  <option value="Ilustrasi setiap adegan">Ilustrasi setiap adegan</option>
                  <option value="Background lokasi">Background lokasi</option>
                  <option value="Gambar thumbnail episode">Gambar thumbnail episode</option>
                  <option value="Sampul setiap episode">Sampul setiap episode</option>
                </select>
              </div>

              <!-- Gaya Visual -->
              <div>
                <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 dark:text-slate-400 mb-1.5">2. Pilih Gaya Visual</label>
                <select id="vis-style"
                  class="w-full px-4 py-3 rounded-xl bg-slate-50 dark:bg-studio-850 border border-slate-300 dark:border-slate-700 text-sm font-semibold focus:outline-none focus:border-amber-500">
                  ${VISUAL_STYLES.map(st => `<option value="${st.id}">${st.name}</option>`).join('')}
                </select>
              </div>

              <!-- Rasio Aspek -->
              <div>
                <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 dark:text-slate-400 mb-1.5">3. Rasio & Format Frame</label>
                <select id="vis-ratio"
                  class="w-full px-4 py-3 rounded-xl bg-slate-50 dark:bg-studio-850 border border-slate-300 dark:border-slate-700 text-sm font-semibold focus:outline-none focus:border-amber-500">
                  <option value="3:4">3:4 (Poster / Sampul Vertikal)</option>
                  <option value="16:9">16:9 (Layar Lebar / Adegan / Thumbnail)</option>
                  <option value="1:1">1:1 (Persegi / Profil Karakter)</option>
                  <option value="9:16">9:16 (Vertical Story / Reels)</option>
                </select>
              </div>

              <!-- Sub-pilihan Konteks -->
              <div id="vis-context-wrapper">
                <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 dark:text-slate-400 mb-1.5">Target Karakter / Episode</label>
                <select id="vis-target-select"
                  class="w-full px-4 py-3 rounded-xl bg-slate-50 dark:bg-studio-850 border border-slate-300 dark:border-slate-700 text-sm focus:outline-none focus:border-amber-500">
                  <option value="all">Seluruh Tokoh Utama Serial</option>
                  ${chars.map(c => `<option value="char:${c.id}">Karakter: ${escapeHtml(c.name)}</option>`).join('')}
                  ${Array.from({ length: totalEps }, (_, i) => i + 1).map(n => `<option value="ep:${n}">Episode ${n}</option>`).join('')}
                </select>
              </div>

              <!-- Deskripsi Tambahan -->
              <div class="md:col-span-2">
                <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 dark:text-slate-400 mb-1.5">Arahan Adegan / Detail Visual Tambahan</label>
                <input id="vis-custom-prompt" type="text"
                  placeholder="Contoh: Dua tokoh berdiri di dermaga saat hujan senja dengan tatapan penuh haru..."
                  class="w-full px-4 py-3 rounded-xl bg-slate-50 dark:bg-studio-850 border border-slate-300 dark:border-slate-700 text-sm focus:outline-none focus:border-amber-500" />
              </div>
            </div>

            <div class="mt-6 pt-5 border-t border-slate-200 dark:border-slate-800 flex flex-col sm:flex-row sm:items-center justify-between gap-4">
              <div class="flex items-center gap-2 text-xs text-slate-500 dark:text-slate-400">
                <i data-lucide="user-check" class="w-4 h-4 text-amber-500 shrink-0"></i>
                <span>Referensi wajah & pakaian karakter aktif akan disertakan otomatis untuk konsistensi visual.</span>
              </div>
              <button onclick="executeCustomVisualGeneration()"
                class="px-6 py-3.5 rounded-2xl bg-gradient-to-r from-amber-500 to-orange-500 hover:from-amber-400 hover:to-orange-400 text-slate-950 font-bold text-sm shadow-lg shadow-amber-500/20 flex items-center justify-center gap-2">
                <i data-lucide="sparkles" class="w-4 h-4"></i>
                <span>Generate Gambar AI</span>
              </button>
            </div>
          </section>

          <!-- GALLERY KOLEKSI VISUAL SERIAL -->
          <section>
            <div class="flex items-center justify-between mb-4">
              <h2 class="font-serif font-bold text-xl">Galeri Karya Visual Serial (${gallery.length})</h2>
            </div>

            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
              ${gallery.map(item => `
                <div class="rounded-3xl bg-white dark:bg-studio-900 border border-slate-200 dark:border-slate-800 overflow-hidden shadow-sm flex flex-col">
                  <div class="aspect-video relative bg-slate-900 overflow-hidden group">
                    ${item.imageUrl
                      ? `<img src="${item.imageUrl}" alt="${escapeHtml(item.title)}" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-300">`
                      : `<div class="w-full h-full p-5 flex flex-col justify-between bg-gradient-to-br from-amber-900/50 via-studio-900 to-slate-950">
                          <span class="text-[10px] font-bold uppercase tracking-widest text-amber-400">${escapeHtml(item.category)}</span>
                          <div>
                            <div class="font-serif font-bold text-base text-white mb-2">${escapeHtml(item.title)}</div>
                            <button onclick="executeCustomVisualGeneration()" class="px-3 py-1.5 rounded-xl bg-amber-500 text-slate-950 font-bold text-xs">
                              Generate Visual AI Sekarang
                            </button>
                          </div>
                        </div>`
                    }
                    <span class="absolute top-3 left-3 px-2.5 py-1 rounded-full text-[10px] font-bold bg-slate-950/80 text-amber-300 backdrop-blur-md border border-amber-500/30">
                      ${escapeHtml(item.category)}
                    </span>
                  </div>

                  <div class="p-4 flex-1 flex flex-col justify-between gap-3">
                    <div>
                      <h3 class="font-bold text-sm text-slate-900 dark:text-white mb-0.5">${escapeHtml(item.title)}</h3>
                      <p class="text-[11px] text-amber-600 dark:text-amber-400">${escapeHtml(item.styleName || '')}</p>
                    </div>

                    ${item.imageUrl ? `
                      <div class="flex items-center gap-2 pt-2 border-t border-slate-100 dark:border-slate-800">
                        <button onclick="downloadGalleryImage('${item.id}')"
                          class="flex-1 py-2 px-3 rounded-xl bg-slate-100 dark:bg-studio-800 hover:bg-amber-500 hover:text-slate-950 text-xs font-semibold text-center transition-colors flex items-center justify-center gap-1.5">
                          <i data-lucide="download" class="w-3.5 h-3.5"></i>
                          <span>Unduh Gambar</span>
                        </button>
                        <button onclick="shareGalleryImage('${item.id}')" class="p-2 rounded-xl bg-slate-100 dark:bg-studio-800 hover:text-amber-500 transition-colors" title="Simpan ke Galeri / Bagikan di HP">
                          <i data-lucide="share-2" class="w-4 h-4"></i>
                        </button>
                        <button onclick="previewImageFullscreen('${item.id}')" class="p-2 rounded-xl bg-slate-100 dark:bg-studio-800 hover:text-amber-500 transition-colors" title="Perbesar">
                          <i data-lucide="maximize-2" class="w-4 h-4"></i>
                        </button>
                      </div>
                    ` : ''}
                  </div>
                </div>
              `).join('')}
            </div>
          </section>
        </div>
      `;
    }

    function dataUrlToBlob(dataUrl) {
      if (!dataUrl || typeof dataUrl !== 'string') {
        throw new Error('Sumber gambar tidak valid.');
      }
      if (!dataUrl.startsWith('data:')) {
        throw new Error('Format gambar bukan data URL.');
      }
      const commaIndex = dataUrl.indexOf(',');
      if (commaIndex === -1) {
        throw new Error('Data gambar tidak lengkap.');
      }
      const header = dataUrl.slice(0, commaIndex);
      const base64Body = dataUrl.slice(commaIndex + 1).replace(/\s+/g, '');
      const mimeMatch = header.match(/data:([^;]+)/i);
      const mimeType = mimeMatch ? mimeMatch[1] : 'image/png';

      const binaryStr = atob(base64Body);
      const len = binaryStr.length;
      const bytes = new Uint8Array(len);
      for (let i = 0; i < len; i++) {
        bytes[i] = binaryStr.charCodeAt(i);
      }
      return new Blob([bytes], { type: mimeType });
    }

    function sanitizeImageFilename(rawTitle, mimeType = 'image/png') {
      const ext = mimeType.includes('jpeg') || mimeType.includes('jpg') ? 'jpg' : 'png';
      const clean = String(rawTitle || 'DramaStudioAI_Visual')
        .replace(/[^a-zA-Z0-9_-]+/g, '_')
        .replace(/^_+|_+$/g, '')
        .slice(0, 60) || 'DramaStudioAI_Visual';
      return `${clean}.${ext}`;
    }

    function downloadDataUrlImage(dataUrl, rawFilename) {
      try {
        const blob = dataUrlToBlob(dataUrl);
        const filename = sanitizeImageFilename(rawFilename, blob.type);
        const blobUrl = URL.createObjectURL(blob);

        const link = document.createElement('a');
        link.style.display = 'none';
        link.href = blobUrl;
        link.download = filename;
        link.rel = 'noopener';
        document.body.appendChild(link);
        link.click();

        setTimeout(() => {
          if (link.parentNode) {
            document.body.removeChild(link);
          }
          URL.revokeObjectURL(blobUrl);
        }, 60000);

        showToast('Mengunduh gambar... Jika di HP tidak otomatis tersimpan, tekan tombol Bagikan atau tekan lama pada gambar.', 'success');
      } catch (err) {
        showToast('Gagal menyiapkan unduhan gambar: ' + err.message, 'error');
      }
    }

    async function shareDataUrlImage(dataUrl, rawFilename, titleText = 'Visual Drama Studio AI') {
      try {
        const blob = dataUrlToBlob(dataUrl);
        const filename = sanitizeImageFilename(rawFilename, blob.type);
        const file = new File([blob], filename, { type: blob.type });

        if (navigator.share && navigator.canShare && navigator.canShare({ files: [file] })) {
          await navigator.share({
            files: [file],
            title: titleText,
            text: `Visual dari DRAMA STUDIO AI: ${titleText}`
          });
          showToast('Berhasil membuka menu simpan/bagikan HP!', 'success');
        } else {
          downloadDataUrlImage(dataUrl, rawFilename);
        }
      } catch (err) {
        if (err && err.name !== 'AbortError') {
          downloadDataUrlImage(dataUrl, rawFilename);
        }
      }
    }

    function downloadGalleryImage(imgId) {
      const proj = getActiveProject();
      const item = (proj.gallery || []).find(g => g.id === imgId);
      if (!item || !item.imageUrl) {
        showToast('Gambar belum tersedia untuk diunduh.', 'warning');
        return;
      }
      downloadDataUrlImage(item.imageUrl, item.title);
    }

    function shareGalleryImage(imgId) {
      const proj = getActiveProject();
      const item = (proj.gallery || []).find(g => g.id === imgId);
      if (!item || !item.imageUrl) return;
      shareDataUrlImage(item.imageUrl, item.title, item.title);
    }

    function handleVisualCategoryChange() {
      const cat = document.getElementById('vis-category').value;
      const ratioEl = document.getElementById('vis-ratio');
      if (cat === 'Poster utama serial' || cat === 'Sampul setiap episode' || cat === 'Foto setiap karakter') {
        ratioEl.value = '3:4';
      } else {
        ratioEl.value = '16:9';
      }
    }

    async function executeCustomVisualGeneration() {
      const proj = getActiveProject();
      const s = proj.settings;
      const category = document.getElementById('vis-category').value;
      const styleId = document.getElementById('vis-style').value;
      const aspectRatio = document.getElementById('vis-ratio').value;
      const targetVal = document.getElementById('vis-target-select').value;
      const customNote = document.getElementById('vis-custom-prompt').value.trim();

      const styleObj = VISUAL_STYLES.find(st => st.id === styleId) || VISUAL_STYLES[0];
      const chars = proj.characters || [];

      let refImages = [];
      let characterConsistencyDesc = '';
      let displayTitle = `${category}: ${s.title}`;

      if (targetVal.startsWith('char:')) {
        const cId = targetVal.split(':')[1];
        const char = chars.find(c => c.id === cId);
        if (char) {
          displayTitle = `${category} - ${char.name}`;
          characterConsistencyDesc = `Main Character featured: ${char.name} (${char.age}, ${char.gender}), Physical features: ${char.physicalTraits}, Wearing exact outfit: ${char.clothingStyle}.`;
          if (char.imageUrl) refImages.push(char.imageUrl);
        }
      } else if (targetVal.startsWith('ep:')) {
        const epNum = Number(targetVal.split(':')[1]);
        const epOutline = proj.storyArc?.episodes?.find(e => Number(e.episodeNumber) === epNum);
        displayTitle = `${category} - Ep ${epNum}${epOutline ? ': ' + epOutline.title : ''}`;
        characterConsistencyDesc = chars.slice(0, 2).map(c => {
          if (c.imageUrl) refImages.push(c.imageUrl);
          return `${c.name} (${c.physicalTraits}, wearing ${c.clothingStyle})`;
        }).join('; ');
      } else {
        characterConsistencyDesc = chars.slice(0, 3).map(c => {
          if (c.imageUrl) refImages.push(c.imageUrl);
          return `${c.name} (${c.physicalTraits}, wearing ${c.clothingStyle})`;
        }).join('; ');
      }

      let prompt = '';
      if (category === 'Poster utama serial') {
        prompt = `Official theatrical drama series poster for "${s.title}".
Genre: ${proj.customGenre || proj.genre}. Setting: ${s.settingPlace} (${s.era}). Mood: ${s.mood}.
Characters shown with consistent faces and outfits: ${characterConsistencyDesc}.
${customNote ? 'Additional composition details: ' + customNote : ''}
Include elegant cinematic Indonesian title typography "${s.title}" prominently on the poster.
Visual Style: ${styleObj.prompt}.`;
      } else if (category === 'Sampul setiap episode') {
        prompt = `Official episode cover artwork for drama series "${s.title}", ${displayTitle}.
Characters consistent visual reference: ${characterConsistencyDesc}.
Setting: ${s.settingPlace}. ${customNote}.
Include clean dramatic title typography "${displayTitle}".
Visual Style: ${styleObj.prompt}.`;
      } else if (category === 'Background lokasi') {
        prompt = `Cinematic establishing environment background without people for drama series "${s.title}".
Location: ${s.settingPlace}, Era: ${s.era}, Mood: ${s.mood}. ${customNote}.
Visual Style: ${styleObj.prompt}.`;
      } else {
        prompt = `${category} for Indonesian drama series "${s.title}".
Setting: ${s.settingPlace} (${s.era}), Mood: ${s.mood}.
Maintain strict facial, physical, and clothing consistency with the provided character references: ${characterConsistencyDesc}.
Scene action & details: ${customNote || s.synopsis}.
Visual Style: ${styleObj.prompt}.`;
      }

      setLoading(true, `Membuat ${category}...`, 'AI sedang melukis visual sinematik dengan menjaga konsistensi karakter serial Anda.');
      try {
        const imageUrl = await callGeminiImage({
          prompt,
          referenceImages: refImages,
          aspectRatio,
          useAdvanced: true
        });

        if (category === 'Foto setiap karakter' && targetVal.startsWith('char:')) {
          const cId = targetVal.split(':')[1];
          const char = chars.find(c => c.id === cId);
          if (char) char.imageUrl = imageUrl;
        }

        proj.gallery.unshift({
          id: 'img_' + Date.now(),
          category,
          title: displayTitle,
          styleName: styleObj.name,
          prompt,
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
        (scene.charactersPresent || []).some(name => name.toLowerCase().includes(c.name.toLowerCase()) || c.name.toLowerCase().includes(name.toLowerCase()))
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

        proj.gallery.unshift({
          id: 'img_' + Date.now(),
          category: 'Ilustrasi setiap adegan',
          title: `Ep ${epNum} - Adegan ${sceneIdx + 1}: ${scene.heading}`,
          styleName: 'Realistis seperti film layar lebar',
          prompt,
          imageUrl,
          createdAt: new Date().toISOString()
        });

        saveState();
        const createdImgId = 'img_' + Date.now();
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
        showToast('Ilustrasi adegan berhasil dibuat! Menampilkan hasil...', 'success');

        openModal(`
          <div class="flex items-center justify-between mb-3">
            <h3 class="font-serif font-bold text-lg">Ilustrasi Adegan ${sceneIdx + 1} (Ep ${epNum})</h3>
            <button onclick="closeModal()" class="p-1.5 rounded-lg hover:bg-slate-100 dark:hover:bg-studio-800 text-slate-400">
              <i data-lucide="x" class="w-5 h-5"></i>
            </button>
          </div>
          <img src="${imageUrl}" alt="Ilustrasi Adegan" class="w-full rounded-2xl border border-slate-700 mb-2">
          <p class="text-[11px] text-slate-400 mb-4">Tips HP: Anda dapat menekan tombol Unduh, Bagikan ke Galeri, atau tekan lama langsung pada gambar di atas.</p>
          <div class="flex flex-wrap justify-between items-center gap-2">
            <button onclick="closeModal(); navigateTo('visuals');" class="px-4 py-2 rounded-xl bg-slate-200 dark:bg-studio-800 text-xs font-semibold">Lihat di Galeri Visual</button>
            <div class="flex items-center gap-2">
              <button onclick="shareGalleryImage('${createdImgId}')" class="px-3.5 py-2 rounded-xl bg-slate-200 dark:bg-studio-800 text-xs font-bold flex items-center gap-1.5">
                <i data-lucide="share-2" class="w-3.5 h-3.5"></i>
                <span>Simpan / Bagikan</span>
              </button>
              <button onclick="downloadGalleryImage('${createdImgId}')" class="px-4 py-2 rounded-xl bg-amber-500 text-slate-950 text-xs font-bold flex items-center gap-1.5">
                <i data-lucide="download" class="w-3.5 h-3.5"></i>
                <span>Unduh Gambar</span>
              </button>
            </div>
          </div>
        `);
      } catch (err) {
        showToast('Gagal membuat ilustrasi adegan: ' + err.message, 'error');
      } finally {
        setLoading(false);
      }
    }

    function previewImageFullscreen(imgId) {
      const proj = getActiveProject();
      const item = proj.gallery.find(g => g.id === imgId);
      if (!item || !item.imageUrl) return;

      openModal(`
        <div class="flex items-center justify-between mb-3">
          <div>
            <span class="text-[10px] font-bold uppercase text-amber-500">${escapeHtml(item.category)}</span>
            <h3 class="font-serif font-bold text-lg">${escapeHtml(item.title)}</h3>
          </div>
          <button onclick="closeModal()" class="p-1.5 rounded-lg hover:bg-slate-100 dark:hover:bg-studio-800 text-slate-400">
            <i data-lucide="x" class="w-5 h-5"></i>
          </button>
        </div>
        <img src="${item.imageUrl}" alt="${escapeHtml(item.title)}" class="w-full max-h-[68vh] object-contain rounded-2xl bg-black mb-2">
        <p class="text-[11px] text-slate-400 mb-4">Tips HP: Jika browser memblokir unduhan otomatis, tekan tombol <strong>Simpan / Bagikan</strong> atau tekan tahan pada gambar di atas lalu pilih <em>Simpan Gambar</em>.</p>
        <div class="flex flex-wrap justify-end gap-2">
          <button onclick="shareGalleryImage('${item.id}')" class="px-4 py-2.5 rounded-xl bg-slate-200 dark:bg-studio-800 text-xs font-bold flex items-center gap-1.5">
            <i data-lucide="share-2" class="w-4 h-4"></i>
            <span>Simpan / Bagikan ke HP</span>
          </button>
          <button onclick="downloadGalleryImage('${item.id}')" class="px-5 py-2.5 rounded-xl bg-amber-500 hover:bg-amber-400 text-slate-950 text-xs font-bold flex items-center gap-1.5">
            <i data-lucide="download" class="w-4 h-4"></i>
            <span>Unduh Resolusi Penuh</span>
          </button>
        </div>
      `);
    }

    function compileFullSeriesDocument() {
      const p = getActiveProject();
      const s = p.settings;
      let doc = `====================================================================\n`;
      doc += `DRAMA STUDIO AI – PAKET PRODUKSI SERIAL DRAMA\n`;
      doc += `====================================================================\n\n`;
      doc += `JUDUL SERIAL   : ${s.title}\n`;
      doc += `GENRE          : ${p.customGenre || p.genre}\n`;
      doc += `TEMA UTAMA     : ${s.theme}\n`;
      doc += `LATAR & ZAMAN  : ${s.settingPlace} (${s.era})\n`;
      doc += `SUASANA        : ${s.mood}\n`;
      doc += `TARGET PENONTON: ${s.audience}\n`;
      doc += `FORMAT         : ${s.episodeCount} Episode (${s.episodeDuration}/episode)\n`;
      doc += `GAYA CERITA    : ${s.narrativeStyle}\n`;
      doc += `PESAN MORAL    : ${s.moralMessage}\n\n`;
      doc += `SINOPSIS SERIAL:\n${s.synopsis}\n\n`;

      doc += `--------------------------------------------------------------------\n`;
      doc += `DAFTAR KARAKTER & REFERENSI VISUAL\n`;
      doc += `--------------------------------------------------------------------\n`;
      (p.characters || []).forEach((c, idx) => {
        doc += `${idx + 1}. ${c.name} (${c.age}, ${c.gender}) — ${c.role}\n`;
        doc += `   Sifat         : ${c.personality}\n`;
        doc += `   Latar Belakang: ${c.background}\n`;
        doc += `   Hubungan      : ${c.relationships}\n`;
        doc += `   Ciri Fisik    : ${c.physicalTraits}\n`;
        doc += `   Gaya Pakaian  : ${c.clothingStyle}\n\n`;
      });

      if (p.storyArc) {
        doc += `--------------------------------------------------------------------\n`;
        doc += `ALUR CERITA BERSERI\n`;
        doc += `--------------------------------------------------------------------\n`;
        doc += `Konflik Utama   : ${p.storyArc.mainConflict}\n`;
        doc += `Konflik Tambahan: ${p.storyArc.subConflicts}\n`;
        doc += `Klimaks         : ${p.storyArc.climax}\n`;
        doc += `Plot Twist      : ${p.storyArc.plotTwist}\n`;
        doc += `Penyelesaian    : ${p.storyArc.resolution}\n\n`;
        (p.storyArc.episodes || []).forEach(ep => {
          doc += `Episode ${ep.episodeNumber}: ${ep.title}\nRingkasan: ${ep.summary}\nKaitan Utama: ${ep.connectionToMainArc}\nCliffhanger: ${ep.cliffhanger}\n\n`;
        });
      }

      doc += `--------------------------------------------------------------------\n`;
      doc += `NASKAH EPISODE\n`;
      doc += `--------------------------------------------------------------------\n\n`;
      Object.values(p.scripts || {}).forEach(sc => {
        doc += `*** EPISODE ${sc.episodeNumber}: ${sc.title.toUpperCase()} ***\n`;
        doc += `Ringkasan: ${sc.summary}\nAdegan Pembuka: ${sc.openingHook}\n\n`;
        (sc.scenes || []).forEach(scene => {
          doc += `ADEGAN ${scene.sceneNumber} - ${scene.heading}\nLokasi: ${scene.locationDesc}\nKarakter: ${(scene.charactersPresent || []).join(', ')}\nKamera: ${scene.cameraDirection}\nVisual: ${scene.visualDesc}\nMusik: ${scene.musicAmbience}\nNarasi: ${scene.narration}\n\n`;
          (scene.dialogue || []).forEach(d => {
            doc += `${d.character.toUpperCase()} (${d.emotion}): "${d.line}"\n`;
          });
          doc += `\n`;
        });
        doc += `Adegan Penutup: ${sc.closingCliffhanger}\n\n====================================================================\n\n`;
      });

      return doc;
    }

    function downloadFullSeriesTxt() {
      const proj = getActiveProject();
      const content = compileFullSeriesDocument();
      const blob = new Blob([content], { type: 'text/plain;charset=utf-8' });
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a');
      a.href = url;
      a.download = `${(proj.settings.title || 'Serial_Drama').replace(/\s+/g, '_')}_DramaStudioAI.txt`;
      document.body.appendChild(a);
      a.click();
      document.body.removeChild(a);
      URL.revokeObjectURL(url);
      showToast('File naskah lengkap berhasil diunduh!', 'success');
    }

    function copyFullSeriesText() {
      copyTextToClipboard(compileFullSeriesDocument());
    }

    /**
     * =========================================================================
     * 13. MAIN RENDER ROUTER & INITIALIZATION
     * =========================================================================
     */
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
