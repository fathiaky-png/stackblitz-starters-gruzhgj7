Claude


App · JSX
import React, { useState } from 'react';
import {
  BarChart3,
  FileText,
  CheckCircle2,
  HelpCircle,
  Sparkles,
  TrendingUp,
  ShieldCheck,
  ChevronRight,
  Calculator,
  Zap,
  Menu,
  X,
  Smile,
  Frown,
  Loader2,
} from 'lucide-react';
 
// Palet warna:
// Barley: #FFF5D1 | Light Olive: #B4BD62 | Neptune: #8EBD9D | Rhino: #0D3243
 
const NAV_LINKS = [
  { href: '#beranda', label: 'Beranda' },
  { href: '#fitur', label: 'Fitur Utama' },
  { href: '#dashboard', label: 'Dashboard' },
  { href: '#paspor', label: 'Paspor SLIKU' },
  { href: '#pricing', label: 'Harga' },
  { href: '#simulasi', label: 'Cek Kesiapan' },
  { href: '#maskot', label: 'Maskot Ciku', badge: 'Imut' },
  { href: '#kontak', label: 'Kontak' },
];
 
const POSE_BUTTONS = [
  { key: 'happy', label: 'Pose Berhasil / Happy', Icon: Smile, iconColor: 'text-[#B4BD62]' },
  { key: 'loading', label: 'Pose Loading / Bingung', Icon: HelpCircle, iconColor: 'text-[#B4BD62]' },
  { key: 'error', label: 'Pose Error / Sedih', Icon: Frown, iconColor: 'text-red-400' },
];
 
export default function App() {
  const [mobileMenuOpen, setMobileMenuOpen] = useState(false);
 
  // State kalkulator
  const [omzet, setOmzet] = useState(15000000);
  const [transaksiCount, setTransaksiCount] = useState(45);
  const [lamaUsaha, setLamaUsaha] = useState(12);
  const [isCalculating, setIsCalculating] = useState(false);
  const [result, setResult] = useState(null);
 
  // State maskot: 'happy' | 'loading' | 'error'
  const [mascotState, setMascotState] = useState('happy');
 
  const handleCalculate = (e) => {
    e.preventDefault();
    setIsCalculating(true);
    setMascotState('loading');
 
    setTimeout(() => {
      setIsCalculating(false);
 
      let score = 0;
      if (omzet >= 10000000) score += 35;
      else if (omzet >= 5000000) score += 20;
      else score += 10;
 
      if (transaksiCount >= 30) score += 35;
      else if (transaksiCount >= 15) score += 20;
      else score += 10;
 
      if (lamaUsaha >= 12) score += 30;
      else if (lamaUsaha >= 6) score += 20;
      else score += 10;
 
      if (score >= 70) {
        setMascotState('happy');
        setResult({
          score,
          status: 'Sangat Siap (Grade A)',
          desc: 'Selamat! Pembukuan dan jejak transaksi usaha Anda sudah sangat sehat dan siap diterbitkan Paspor SLIKU untuk pengajuan pembiayaan.',
          color: 'bg-[#B4BD62]/30 text-[#0D3243] border-[#B4BD62]',
        });
      } else if (score >= 50) {
        setMascotState('happy');
        setResult({
          score,
          status: 'Cukup Siap (Grade B)',
          desc: 'Usaha Anda dalam jalur yang baik! Tingkatkan konsistensi catatan transaksi 1-2 bulan lagi untuk skor maksimal.',
          color: 'bg-[#8EBD9D]/30 text-[#0D3243] border-[#8EBD9D]',
        });
      } else {
        setMascotState('error');
        setResult({
          score,
          status: 'Perlu Perbaikan (Grade C)',
          desc: 'Pencatatan transaksi masih belum cukup konsisten. Ciku sarankan rutin rapikan transaksi harian di SLIKU ya!',
          color: 'bg-red-100 text-red-800 border-red-300',
        });
      }
    }, 1000);
  };
 
  const closeMenu = () => setMobileMenuOpen(false);
 
  return (
    <div className="min-h-screen font-sans bg-[#FFF5D1]/30 text-[#0D3243] antialiased scroll-smooth">
      {/* Animasi fadeIn untuk hasil simulasi */}
      <style>{`
        html { scroll-behavior: smooth; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(8px); } to { opacity: 1; transform: translateY(0); } }
        .animate-fadeIn { animation: fadeIn 0.5s ease-out both; }
      `}</style>
 
      {/* HEADER */}
      <header className="sticky top-0 z-50 bg-[#FFF5D1]/90 backdrop-blur-md border-b border-[#8EBD9D]/30">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
          {/* Logo */}
          <div className="flex items-center gap-3">
            <div className="w-12 h-12 rounded-2xl bg-gradient-to-tr from-[#0D3243] via-[#8EBD9D] to-[#B4BD62] p-0.5 shadow-md hover:scale-105 transition-transform cursor-pointer">
              <div className="w-full h-full bg-[#FFF5D1] rounded-[14px] flex items-center justify-center relative overflow-hidden">
                <svg className="w-8 h-8 text-[#0D3243]" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2.5" strokeLinecap="round" strokeLinejoin="round">
                  <path d="M4 19c2-3 6-3 8-6 2-3 1-5 4-5 3 0 4 2 4 4 0 4-5 4-7 8" />
                  <path d="M3 13h4v8H3z" fill="#8EBD9D" fillOpacity="0.4" />
                  <path d="M17 11h4v10h-4z" fill="#B4BD62" fillOpacity="0.5" />
                </svg>
              </div>
            </div>
            <div>
              <span className="text-2xl font-black tracking-wider text-[#0D3243]">SLIKU</span>
              <span className="block text-[10px] font-bold text-[#0D3243]/70 uppercase tracking-widest">Sistem Informasi Kesehatan Usaha</span>
            </div>
          </div>
 
          {/* Navigasi Desktop */}
          <nav className="hidden md:flex items-center gap-6 font-medium text-sm">
            {NAV_LINKS.map((link) => (
              <a key={link.href} href={link.href} className="hover:text-[#B4BD62] transition-colors flex items-center gap-1">
                <span>{link.label}</span>
                {link.badge && (
                  <span className="bg-[#B4BD62] text-[#0D3243] text-[10px] font-bold px-2 py-0.5 rounded-full">{link.badge}</span>
                )}
              </a>
            ))}
          </nav>
 
          {/* CTA */}
          <div className="hidden md:flex items-center gap-4">
            <a
              href="#simulasi"
              className="px-6 py-2.5 rounded-xl bg-[#0D3243] text-[#FFF5D1] font-semibold text-sm hover:bg-[#0D3243]/90 hover:shadow-lg transition-all transform hover:-translate-y-0.5 flex items-center gap-2"
            >
              <span>Coba Sekarang</span>
              <ChevronRight className="w-4 h-4" />
            </a>
          </div>
 
          {/* Tombol menu mobile */}
          <button
            onClick={() => setMobileMenuOpen(!mobileMenuOpen)}
            className="md:hidden p-2 rounded-lg text-[#0D3243] hover:bg-[#8EBD9D]/20"
            aria-label="Buka menu"
          >
            {mobileMenuOpen ? <X className="w-6 h-6" /> : <Menu className="w-6 h-6" />}
          </button>
        </div>
 
        {/* Menu mobile */}
        {mobileMenuOpen && (
          <div className="md:hidden bg-[#FFF5D1] border-b border-[#8EBD9D]/40 px-4 pt-2 pb-6 space-y-1">
            {NAV_LINKS.map((link) => (
              <a key={link.href} href={link.href} onClick={closeMenu} className="block py-2 text-base font-medium hover:text-[#B4BD62]">
                {link.label}
              </a>
            ))}
            <a
              href="#simulasi"
              onClick={closeMenu}
              className="w-full text-center mt-2 px-6 py-3 rounded-xl bg-[#0D3243] text-[#FFF5D1] font-semibold text-sm block"
            >
              Coba Sekarang
            </a>
          </div>
        )}
      </header>
 
      {/* HERO */}
      <section id="beranda" className="relative pt-12 pb-20 md:pt-20 md:pb-32 overflow-hidden">
        <div className="absolute top-1/4 left-10 w-72 h-72 bg-[#8EBD9D]/20 rounded-full blur-3xl -z-10 pointer-events-none"></div>
        <div className="absolute bottom-10 right-10 w-96 h-96 bg-[#B4BD62]/20 rounded-full blur-3xl -z-10 pointer-events-none"></div>
 
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="grid lg:grid-cols-12 gap-12 items-center">
            {/* Kiri */}
            <div className="lg:col-span-7 space-y-6 text-center lg:text-left">
              <div className="inline-flex items-center gap-2 px-4 py-2 rounded-full bg-[#8EBD9D]/30 border border-[#8EBD9D] text-[#0D3243] text-xs md:text-sm font-semibold">
                <Sparkles className="w-4 h-4 text-[#0D3243]" />
                <span>Solusi Akses Pembiayaan Mudah untuk UMKM</span>
              </div>
 
              <h1 className="text-4xl sm:text-5xl lg:text-6xl font-extrabold tracking-tight text-[#0D3243] leading-tight">
                Ubah Catatan Sederhana Jadi{' '}
                <span className="underline decoration-[#B4BD62] decoration-wavy underline-offset-8">Paspor SLIKU</span>
              </h1>
 
              <p className="text-lg md:text-xl text-[#0D3243]/80 leading-relaxed max-w-2xl mx-auto lg:mx-0">
                SLIKU (Sistem Informasi Kesehatan Usaha) membantu UMKM mengubah pembukuan harian &amp; jejak transaksi menjadi{' '}
                <strong>Laporan Kesiapan Usaha</strong> yang disukai oleh perbankan dan lembaga keuangan.
              </p>
 
              <div className="flex flex-col sm:flex-row items-center justify-center lg:justify-start gap-4 pt-4">
                <a
                  href="#simulasi"
                  className="w-full sm:w-auto px-8 py-4 rounded-2xl bg-[#0D3243] text-[#FFF5D1] font-bold text-base hover:bg-[#0D3243]/90 shadow-lg hover:shadow-xl transition-all transform hover:-translate-y-1 flex items-center justify-center gap-3"
                >
                  <Calculator className="w-5 h-5" />
                  <span>Simulasi Paspor Sekarang</span>
                </a>
                <a
                  href="#fitur"
                  className="w-full sm:w-auto px-8 py-4 rounded-2xl bg-[#FFF5D1] text-[#0D3243] font-bold text-base border-2 border-[#8EBD9D] hover:bg-[#8EBD9D]/20 transition-all flex items-center justify-center gap-2"
                >
                  <span>Pelajari Fitur</span>
                </a>
              </div>
 
              <div className="pt-8 border-t border-[#8EBD9D]/30 grid grid-cols-3 gap-4 text-center lg:text-left">
                <div>
                  <h4 className="text-xl md:text-2xl font-black text-[#0D3243]">100%</h4>
                  <p className="text-xs md:text-sm text-[#0D3243]/70">Mudah Digunakan</p>
                </div>
                <div>
                  <h4 className="text-xl md:text-2xl font-black text-[#0D3243]">Rapi &amp; Valid</h4>
                  <p className="text-xs md:text-sm text-[#0D3243]/70">Format Lembaga Keuangan</p>
                </div>
                <div>
                  <h4 className="text-xl md:text-2xl font-black text-[#0D3243]">Skor Kesiapan</h4>
                  <p className="text-xs md:text-sm text-[#0D3243]/70">Analisis Otomatis</p>
                </div>
              </div>
            </div>
 
            {/* Kanan: mockup */}
            <div className="lg:col-span-5 relative">
              <div className="relative mx-auto max-w-md lg:max-w-none">
                <div className="absolute inset-0 bg-gradient-to-tr from-[#B4BD62] to-[#8EBD9D] rounded-3xl transform rotate-3 scale-105 opacity-60 blur-sm"></div>
 
                <div className="relative bg-[#FFF5D1] border-2 border-[#0D3243] rounded-3xl p-6 md:p-8 shadow-2xl space-y-6">
                  <div className="flex items-center justify-between pb-4 border-b border-[#8EBD9D] gap-2">
                    <div className="flex items-center gap-3">
                      <div className="w-10 h-10 rounded-xl bg-[#0D3243] text-[#FFF5D1] flex items-center justify-center text-xl">
                        🐿️
                      </div>
                      <div>
                        <h3 className="font-extrabold text-base text-[#0D3243]">Paspor SLIKU Digital</h3>
                        <p className="text-xs text-[#0D3243]/70">ID Usaha: #SLK-2026-UMKM</p>
                      </div>
                    </div>
                    <span className="bg-[#B4BD62] text-[#0D3243] text-xs font-bold px-3 py-1 rounded-full border border-[#0D3243] text-center">
                      Grade A (Siap Pembiayaan)
                    </span>
                  </div>
 
                  <div className="space-y-3">
                    <div className="flex justify-between text-sm">
                      <span className="text-[#0D3243]/70">Nama Usaha:</span>
                      <span className="font-bold">Kopi Kerajinan Berkah</span>
                    </div>
                    <div className="flex justify-between text-sm">
                      <span className="text-[#0D3243]/70">Indeks Kesehatan:</span>
                      <span className="font-bold text-[#0D3243] flex items-center gap-1">
                        <TrendingUp className="w-4 h-4 text-[#B4BD62]" /> 92/100 (Sangat Sehat)
                      </span>
                    </div>
                    <div className="flex justify-between text-sm">
                      <span className="text-[#0D3243]/70">Kelayakan Kredit:</span>
                      <span className="font-semibold text-emerald-700 bg-emerald-100 px-2 py-0.5 rounded">Direkomendasikan</span>
                    </div>
                  </div>
 
                  <div className="bg-[#8EBD9D]/20 p-4 rounded-xl border border-[#8EBD9D]/40 space-y-2">
                    <div className="flex justify-between text-xs font-bold text-[#0D3243]">
                      <span>Arus Kas 6 Bulan</span>
                      <span>Stabil &amp; Positif</span>
                    </div>
                    <div className="flex items-end gap-2 h-16 pt-2">
                      <div className="flex-1 bg-[#8EBD9D] rounded-t-md h-8"></div>
                      <div className="flex-1 bg-[#8EBD9D] rounded-t-md h-10"></div>
                      <div className="flex-1 bg-[#B4BD62] rounded-t-md h-12"></div>
                      <div className="flex-1 bg-[#B4BD62] rounded-t-md h-14"></div>
                      <div className="flex-1 bg-[#0D3243] rounded-t-md h-full"></div>
                    </div>
                  </div>
 
                  <div className="bg-[#0D3243] text-[#FFF5D1] p-3 rounded-xl flex items-center justify-between text-xs font-medium">
                    <div className="flex items-center gap-2">
                      <span className="text-xl">🐿️</span>
                      <span>Diverifikasi oleh <strong>Ciku</strong></span>
                    </div>
                    <CheckCircle2 className="w-4 h-4 text-[#B4BD62]" />
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>
 
      {/* MASKOT */}
      <section id="maskot" className="py-16 bg-[#8EBD9D]/20 border-y border-[#8EBD9D]/30">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="text-center max-w-3xl mx-auto mb-12 space-y-3">
            <div className="inline-block px-4 py-1 rounded-full bg-[#FFF5D1] border border-[#B4BD62] text-xs font-bold text-[#0D3243] uppercase tracking-wider">
              Kenalan Yuk!
            </div>
            <h2 className="text-3xl sm:text-4xl font-extrabold text-[#0D3243]">
              Maskot Kita: <span className="underline decoration-[#B4BD62]">CIKU</span> si Tupai Cerdas
            </h2>
            <p className="text-[#0D3243]/80">
              Seperti tupai yang rajin dan teliti mengumpulkan biji ek untuk masa depan, <strong>Ciku</strong> bertugas membantu UMKM mengumpulkan &amp; merapikan setiap detail transaksi harian menjadi aset finansial bernilai!
            </p>
          </div>
 
          <div className="max-w-4xl mx-auto bg-[#FFF5D1] border-2 border-[#0D3243] rounded-3xl p-6 md:p-8 shadow-lg">
            <div className="text-center mb-6">
              <span className="text-sm font-bold text-[#0D3243]/70">Pilih Ekspresi Ciku Saat Mendampingi Aplikasi:</span>
            </div>
 
            <div className="flex flex-wrap justify-center gap-3 mb-8">
              {POSE_BUTTONS.map(({ key, label, Icon, iconColor }) => (
                <button
                  key={key}
                  type="button"
                  onClick={() => setMascotState(key)}
                  className={`px-5 py-2.5 rounded-xl font-bold text-sm transition-all flex items-center gap-2 border-2 ${
                    mascotState === key
                      ? 'bg-[#0D3243] text-[#FFF5D1] border-[#0D3243] shadow-md'
                      : 'bg-white text-[#0D3243] border-[#8EBD9D] hover:bg-[#8EBD9D]/20'
                  }`}
                >
                  <Icon className={`w-4 h-4 ${iconColor}`} />
                  <span>{label}</span>
                </button>
              ))}
            </div>
 
            <div className="grid md:grid-cols-12 gap-8 items-center bg-[#8EBD9D]/10 p-6 rounded-2xl border border-[#8EBD9D]/40">
              {/* Avatar */}
              <div className="md:col-span-5 flex justify-center">
                <div className="relative w-48 h-48 md:w-56 md:h-56 bg-[#FFF5D1] rounded-full border-4 border-[#0D3243] flex items-center justify-center shadow-xl overflow-hidden">
                  {mascotState === 'happy' && (
                    <div className="text-center animate-bounce">
                      <div className="text-6xl mb-2">🐿️✨</div>
                      <div className="bg-[#B4BD62] text-[#0D3243] font-black text-xs px-3 py-1 rounded-full border border-[#0D3243]">
                        Yeay! Berhasil! 🎉
                      </div>
                    </div>
                  )}
 
                  {mascotState === 'loading' && (
                    <div className="text-center">
                      <div className="text-6xl mb-2 animate-pulse">🐿️❓</div>
                      <div className="bg-[#FFF5D1] text-[#0D3243] font-black text-xs px-3 py-1 rounded-full border border-[#0D3243] flex items-center gap-1 justify-center">
                        <Loader2 className="w-3 h-3 animate-spin text-[#0D3243]" />
                        <span>Sedang Menghitung...</span>
                      </div>
                    </div>
                  )}
 
                  {mascotState === 'error' && (
                    <div className="text-center">
                      <div className="text-6xl mb-2">🐿️🥺</div>
                      <div className="bg-red-200 text-red-900 font-black text-xs px-3 py-1 rounded-full border border-red-400">
                        Ups, Ada Kendala! 😟
                      </div>
                    </div>
                  )}
                </div>
              </div>
 
              {/* Deskripsi */}
              <div className="md:col-span-7 space-y-4 text-left">
                {mascotState === 'happy' && (
                  <div>
                    <h4 className="text-2xl font-black text-[#0D3243] flex flex-wrap items-center gap-2">
                      <span>Ciku Senang Banget!</span>
                      <span className="text-sm font-normal bg-[#B4BD62] px-2 py-0.5 rounded-md text-[#0D3243]">Status: Fitur Sukses</span>
                    </h4>
                    <p className="text-[#0D3243]/80 mt-2 leading-relaxed">
                      "Hore! Laporan Paspor SLIKU kamu sudah selesai dibuat dan nilainya sangat sehat! Sekarang kamu bisa langsung bagikan laporan ini ke pihak bank atau lembaga pembiayaan."
                    </p>
                  </div>
                )}
 
                {mascotState === 'loading' && (
                  <div>
                    <h4 className="text-2xl font-black text-[#0D3243] flex flex-wrap items-center gap-2">
                      <span>Ciku Lagi Mikir Cermat...</span>
                      <span className="text-sm font-normal bg-[#8EBD9D] px-2 py-0.5 rounded-md text-[#0D3243]">Status: Memproses Data</span>
                    </h4>
                    <p className="text-[#0D3243]/80 mt-2 leading-relaxed">
                      "Tunggu sebentar ya... Ciku sedang menghitung arus kas, frekuensi transaksi, dan indeks stabilitas usaha kamu. Jangan ditutup dulu halamannya!"
                    </p>
                  </div>
                )}
 
                {mascotState === 'error' && (
                  <div>
                    <h4 className="text-2xl font-black text-red-900 flex flex-wrap items-center gap-2">
                      <span>Aduh, Ciku Sedih Kendala Sistem...</span>
                      <span className="text-sm font-normal bg-red-100 px-2 py-0.5 rounded-md text-red-800">Status: Error / Disconnect</span>
                    </h4>
                    <p className="text-[#0D3243]/80 mt-2 leading-relaxed">
                      "Waduh! Koneksi terputus atau ada data yang belum lengkap diisi nih. Yuk coba periksa jaringan internet kamu atau klik tombol muat ulang di bawah!"
                    </p>
                  </div>
                )}
 
                <div className="pt-2">
                  <div className="inline-flex items-center gap-2 text-xs font-bold text-[#0D3243] bg-[#B4BD62]/40 px-3 py-1.5 rounded-lg border border-[#B4BD62]">
                    <span>💡 Nama Maskot: <strong>CIKU</strong> (Chipmunk InformatiK Usaha)</span>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>
 
      {/* DASHBOARD */}
      <section id="dashboard" className="py-20 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div className="text-center max-w-3xl mx-auto mb-16 space-y-3">
          <span className="text-xs font-bold uppercase tracking-widest text-[#0D3243] bg-[#8EBD9D] px-3 py-1 rounded-full inline-block">
            Pratinjau Sistem
          </span>
          <h2 className="text-3xl sm:text-4xl font-black text-[#0D3243]">Dashboard Kesehatan Usaha UMKM</h2>
          <p className="text-[#0D3243]/80 text-lg">
            Pantau arus kas harian, catatan transaksi masuk, dan status kelayakan pembiayaan Anda dalam satu tampilan interaktif yang bersih dan mudah dipahami.
          </p>
        </div>
 
        <div className="bg-[#0D3243] text-[#FFF5D1] rounded-3xl p-6 md:p-10 border-4 border-[#B4BD62] shadow-2xl space-y-8">
          <div className="flex flex-col md:flex-row md:items-center justify-between gap-4 pb-6 border-b border-[#8EBD9D]/30">
            <div className="flex items-center gap-3">
              <div className="w-12 h-12 bg-[#B4BD62] rounded-xl flex items-center justify-center text-[#0D3243] text-2xl font-black">
                📊
              </div>
              <div>
                <h3 className="text-xl font-bold">Dashboard Toko Berkah Jaya</h3>
                <p className="text-xs text-[#FFF5D1]/70">Periode: Bulan Berjalan — Dipandu oleh Ciku 🐿️</p>
              </div>
            </div>
            <div className="flex flex-wrap items-center gap-3">
              <span className="bg-[#8EBD9D]/30 border border-[#8EBD9D] text-[#FFF5D1] text-xs px-3 py-1.5 rounded-xl font-semibold">
                Status: Sinkronisasi Otomatis Aktif
              </span>
              <button type="button" className="bg-[#B4BD62] text-[#0D3243] text-xs font-bold px-4 py-2 rounded-xl hover:bg-[#B4BD62]/90 transition-colors">
                + Catat Transaksi Baru
              </button>
            </div>
          </div>
 
          <div className="grid sm:grid-cols-2 lg:grid-cols-4 gap-6">
            <div className="bg-[#FFF5D1]/10 border border-[#8EBD9D]/40 p-5 rounded-2xl space-y-2">
              <span className="text-xs text-[#FFF5D1]/70 block uppercase font-bold">Total Omzet Bulan Ini</span>
              <div className="text-2xl font-black text-[#B4BD62]">Rp 18.450.000</div>
              <span className="text-[11px] text-emerald-400 font-semibold flex items-center gap-1">
                <TrendingUp className="w-3 h-3" /> +14.2% dari bulan lalu
              </span>
            </div>
 
            <div className="bg-[#FFF5D1]/10 border border-[#8EBD9D]/40 p-5 rounded-2xl space-y-2">
              <span className="text-xs text-[#FFF5D1]/70 block uppercase font-bold">Total Transaksi</span>
              <div className="text-2xl font-black text-[#FFF5D1]">128 Transaksi</div>
              <span className="text-[11px] text-[#8EBD9D]">Rata-rata 4 transaksi/hari</span>
            </div>
 
            <div className="bg-[#FFF5D1]/10 border border-[#8EBD9D]/40 p-5 rounded-2xl space-y-2">
              <span className="text-xs text-[#FFF5D1]/70 block uppercase font-bold">Indeks Kesehatan Usaha</span>
              <div className="text-2xl font-black text-[#B4BD62]">88 / 100</div>
              <span className="text-[11px] text-[#B4BD62]">Kategori: Sangat Sehat</span>
            </div>
 
            <div className="bg-[#FFF5D1]/10 border border-[#8EBD9D]/40 p-5 rounded-2xl space-y-2">
              <span className="text-xs text-[#FFF5D1]/70 block uppercase font-bold">Kesiapan Paspor SLIKU</span>
              <div className="text-xl font-black text-emerald-300">Siap Ajukan Bank</div>
              <span className="text-[11px] text-[#FFF5D1]/70">Diverifikasi Ciku</span>
            </div>
          </div>
 
          <div className="grid lg:grid-cols-12 gap-6">
            <div className="lg:col-span-8 bg-[#FFF5D1]/5 border border-[#8EBD9D]/30 p-6 rounded-2xl space-y-4">
              <div className="flex justify-between items-center">
                <h4 className="font-bold text-sm">Grafik Arus Kas &amp; Tren Pendapatan UMKM</h4>
                <span className="text-xs text-[#B4BD62]">Update Real-time</span>
              </div>
 
              <div className="h-48 flex items-end gap-3 pt-4 border-b border-[#FFF5D1]/10">
                <div className="flex-1 bg-[#8EBD9D]/60 hover:bg-[#8EBD9D] rounded-t-lg h-24 flex items-end justify-center pb-2 text-[10px] font-bold">Minggu 1</div>
                <div className="flex-1 bg-[#8EBD9D]/80 hover:bg-[#8EBD9D] rounded-t-lg h-32 flex items-end justify-center pb-2 text-[10px] font-bold">Minggu 2</div>
                <div className="flex-1 bg-[#B4BD62] hover:bg-[#B4BD62]/80 rounded-t-lg h-40 flex items-end justify-center pb-2 text-[10px] font-bold text-[#0D3243]">Minggu 3</div>
                <div className="flex-1 bg-[#B4BD62] hover:bg-[#B4BD62]/80 rounded-t-lg h-full flex items-end justify-center pb-2 text-[10px] font-bold text-[#0D3243]">Minggu 4</div>
              </div>
              <p className="text-xs text-[#FFF5D1]/70">
                *Catatan transaksi harian Anda otomatis dirangkum ke dalam grafik di atas untuk memudahkan verifikasi lembaga keuangan.
              </p>
            </div>
 
            <div className="lg:col-span-4 bg-[#FFF5D1] text-[#0D3243] p-6 rounded-2xl flex flex-col justify-between space-y-4">
              <div className="space-y-3">
                <div className="flex items-center gap-2">
                  <span className="text-2xl">🐿️</span>
                  <span className="font-black text-sm">Pesan Ciku Hari Ini</span>
                </div>
                <p className="text-xs leading-relaxed text-[#0D3243]/80">
                  "Hebat! Catatan transaksi minggu ini sangat konsisten. Rasio kas masuk dan pengeluaran operasional sudah memenuhi syarat emas perbankan. Siap-siap terbitkan Paspor SLIKU ya!"
                </p>
              </div>
 
              <a
                href="#paspor"
                className="w-full py-3 rounded-xl bg-[#0D3243] text-[#FFF5D1] text-xs font-bold text-center block hover:bg-[#0D3243]/90 transition-colors"
              >
                Unduh Paspor SLIKU Sekarang
              </a>
            </div>
          </div>
        </div>
      </section>
 
      {/* FITUR */}
      <section id="fitur" className="py-20 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div className="text-center max-w-3xl mx-auto mb-16 space-y-3">
          <span className="text-xs font-bold uppercase tracking-widest text-[#0D3243] bg-[#B4BD62] px-3 py-1 rounded-full inline-block">
            Fitur Unggulan
          </span>
          <h2 className="text-3xl sm:text-4xl font-black text-[#0D3243]">Solusi Lengkap Kesehatan Finansial UMKM</h2>
          <p className="text-[#0D3243]/80 text-lg">
            SLIKU menjembatani celah antara pencatatan pembukuan sederhana UMKM dengan standar kriteria penilaian lembaga pembiayaan.
          </p>
        </div>
 
        <div className="grid md:grid-cols-3 gap-8">
          <div className="bg-[#FFF5D1] border-2 border-[#0D3243] p-8 rounded-3xl hover:shadow-xl transition-all hover:-translate-y-1 space-y-4">
            <div className="w-14 h-14 bg-[#B4BD62] rounded-2xl border-2 border-[#0D3243] flex items-center justify-center text-[#0D3243] shadow-md">
              <FileText className="w-7 h-7" />
            </div>
            <h3 className="text-xl font-black text-[#0D3243]">1. Pencatatan Sederhana &amp; Praktis</h3>
            <p className="text-[#0D3243]/80 text-sm leading-relaxed">
              Input transaksi harian penjualan dan pengeluaran tanpa perlu paham istilah akuntansi yang rumit. Didukung antarmuka ramah pengguna.
            </p>
          </div>
 
          <div className="bg-[#FFF5D1] border-2 border-[#0D3243] p-8 rounded-3xl hover:shadow-xl transition-all hover:-translate-y-1 space-y-4">
            <div className="w-14 h-14 bg-[#8EBD9D] rounded-2xl border-2 border-[#0D3243] flex items-center justify-center text-[#0D3243] shadow-md">
              <BarChart3 className="w-7 h-7" />
            </div>
            <h3 className="text-xl font-black text-[#0D3243]">2. Analisis Kesehatan Usaha</h3>
            <p className="text-[#0D3243]/80 text-sm leading-relaxed">
              Sistem SLIKU secara otomatis menganalisis rasio kesehatan bisnis, kestabilan omzet harian, serta pola pertumbuhan modal usaha Anda.
            </p>
          </div>
 
          <div className="bg-[#FFF5D1] border-2 border-[#0D3243] p-8 rounded-3xl hover:shadow-xl transition-all hover:-translate-y-1 space-y-4">
            <div className="w-14 h-14 bg-[#0D3243] rounded-2xl border-2 border-[#0D3243] flex items-center justify-center shadow-md">
              <ShieldCheck className="w-7 h-7 text-[#B4BD62]" />
            </div>
            <h3 className="text-xl font-black text-[#0D3243]">3. Paspor Kesiapan Usaha</h3>
            <p className="text-[#0D3243]/80 text-sm leading-relaxed">
              Hasilkan dokumen resume resmi "Paspor SLIKU" yang siap diunduh dan dibagikan langsung kepada bank / perbankan sebelum pengajuan kredit modal.
            </p>
          </div>
        </div>
      </section>
 
      {/* PASPOR */}
      <section id="paspor" className="py-16 bg-[#0D3243] text-[#FFF5D1]">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="grid lg:grid-cols-2 gap-12 items-center">
            <div className="space-y-6">
              <span className="text-xs font-extrabold uppercase tracking-widest text-[#0D3243] bg-[#B4BD62] px-3 py-1 rounded-full inline-block">
                Inovasi Utama
              </span>
              <h2 className="text-3xl sm:text-4xl font-extrabold text-[#FFF5D1] leading-tight">Apa itu Paspor SLIKU?</h2>
              <p className="text-[#FFF5D1]/80 text-base leading-relaxed">
                Paspor SLIKU adalah dokumen ringkasan kesiapan finansial usaha yang diterbitkan oleh sistem kami. Dokumen ini mengubah tumpukan nota dan catatan sederhana Anda menjadi format laporan terstandar yang mudah dibaca oleh analisis kredit perbankan.
              </p>
 
              <div className="space-y-3 pt-2">
                {[
                  'Menampilkan Skor Kesehatan Usaha secara objektif & transparan.',
                  'Mempercepat proses kurasi dan verifikasi dari pihak lembaga pembiayaan.',
                  'Meningkatkan kepercayaan kreditur terhadap profil keandalan UMKM Anda.',
                ].map((text) => (
                  <div key={text} className="flex items-start gap-3">
                    <CheckCircle2 className="w-5 h-5 text-[#B4BD62] shrink-0 mt-0.5" />
                    <p className="text-sm">{text}</p>
                  </div>
                ))}
              </div>
            </div>
 
            <div className="bg-[#FFF5D1] text-[#0D3243] border-4 border-[#B4BD62] rounded-3xl p-6 sm:p-8 shadow-2xl relative overflow-hidden">
              <div className="absolute top-0 right-0 bg-[#B4BD62] text-[#0D3243] font-black text-xs px-4 py-2 rounded-bl-2xl uppercase tracking-wider">
                Official Document Preview
              </div>
 
              <div className="space-y-6 pt-6">
                <div className="flex items-center gap-4">
                  <div className="w-16 h-16 rounded-2xl bg-[#0D3243] text-[#FFF5D1] flex items-center justify-center text-3xl font-black">
                    S
                  </div>
                  <div>
                    <h3 className="text-2xl font-black">PASPOR SLIKU</h3>
                    <p className="text-xs font-bold text-[#0D3243]/70">Laporan Kesiapan Pembiayaan Usaha</p>
                  </div>
                </div>
 
                <div className="grid grid-cols-2 gap-4 bg-[#8EBD9D]/20 p-4 rounded-2xl border border-[#8EBD9D]">
                  <div>
                    <span className="text-xs text-[#0D3243]/70 block">Tingkat Kesehatan:</span>
                    <span className="text-lg font-black text-[#0D3243]">Sangat Sehat</span>
                  </div>
                  <div>
                    <span className="text-xs text-[#0D3243]/70 block">Rekomendasi Plafon:</span>
                    <span className="text-lg font-black text-[#0D3243]">Rp 25.000.000+</span>
                  </div>
                </div>
 
                <div className="space-y-2">
                  <span className="text-xs font-bold text-[#0D3243]/70 uppercase">Indikator Penilaian:</span>
                  <div className="space-y-2 text-xs font-semibold">
                    <div>
                      <div className="flex justify-between mb-1">
                        <span>Konsistensi Arus Kas</span>
                        <span>95%</span>
                      </div>
                      <div className="w-full bg-[#0D3243]/10 h-2 rounded-full overflow-hidden">
                        <div className="bg-[#0D3243] h-full w-[95%]"></div>
                      </div>
                    </div>
                    <div>
                      <div className="flex justify-between mb-1">
                        <span>Ketertiban Catatan Transaksi</span>
                        <span>88%</span>
                      </div>
                      <div className="w-full bg-[#0D3243]/10 h-2 rounded-full overflow-hidden">
                        <div className="bg-[#B4BD62] h-full w-[88%]"></div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>
 
      {/* HARGA */}
      <section id="pricing" className="py-20 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div className="text-center max-w-3xl mx-auto mb-16 space-y-3">
          <span className="text-xs font-bold uppercase tracking-widest text-[#0D3243] bg-[#B4BD62] px-3 py-1 rounded-full inline-block">
            Paket Layanan
          </span>
          <h2 className="text-3xl sm:text-4xl font-black text-[#0D3243]">Pilihan Paket SLIKU untuk UMKM Anda</h2>
          <p className="text-[#0D3243]/80 text-lg">
            Mulai dari pencatatan gratis hingga penerbitan Paspor SLIKU resmi untuk akses pembiayaan bank.
          </p>
        </div>
 
        <div className="grid md:grid-cols-3 gap-8 items-stretch">
          {/* Paket 1 */}
          <div className="bg-[#FFF5D1] border-2 border-[#0D3243] rounded-3xl p-8 flex flex-col justify-between shadow-lg">
            <div className="space-y-4">
              <span className="text-xs font-bold uppercase tracking-wider bg-[#8EBD9D]/40 px-3 py-1 rounded-full text-[#0D3243] inline-block">
                Pemula / UMKM Baru
              </span>
              <h3 className="text-2xl font-black text-[#0D3243]">Paket Rintisan</h3>
              <div className="text-3xl font-extrabold text-[#0D3243]">
                Gratis <span className="text-xs font-normal text-[#0D3243]/70">/ selamanya</span>
              </div>
              <p className="text-xs text-[#0D3243]/80 leading-relaxed">
                Cocok untuk usaha mikro yang baru mulai membiasakan pencatatan transaksi harian sederhana.
              </p>
              <ul className="space-y-3 text-xs font-medium pt-4 border-t border-[#8EBD9D]/40">
                <li className="flex items-center gap-2"><CheckCircle2 className="w-4 h-4 text-[#B4BD62]" /> Pencatatan transaksi harian</li>
                <li className="flex items-center gap-2"><CheckCircle2 className="w-4 h-4 text-[#B4BD62]" /> Pendampingan maskot Ciku</li>
                <li className="flex items-center gap-2"><CheckCircle2 className="w-4 h-4 text-[#B4BD62]" /> Rekap arus kas bulanan dasar</li>
              </ul>
            </div>
            <a href="#simulasi" className="mt-8 w-full py-3 rounded-xl bg-[#0D3243] text-[#FFF5D1] font-bold text-sm text-center block hover:bg-[#0D3243]/90 transition-colors">
              Mulai Gratis
            </a>
          </div>
 
          {/* Paket 2 */}
          <div className="bg-[#0D3243] text-[#FFF5D1] border-4 border-[#B4BD62] rounded-3xl p-8 flex flex-col justify-between shadow-2xl relative transform md:-translate-y-2">
            <div className="absolute top-0 right-0 bg-[#B4BD62] text-[#0D3243] text-xs font-black px-4 py-1.5 rounded-bl-2xl uppercase">
              Paling Populer ⭐
            </div>
            <div className="space-y-4 pt-4">
              <span className="text-xs font-bold uppercase tracking-wider bg-[#B4BD62] px-3 py-1 rounded-full text-[#0D3243] inline-block">
                UMKM Siap Pembiayaan
              </span>
              <h3 className="text-2xl font-black text-[#FFF5D1]">Paspor SLIKU Pro</h3>
              <div className="text-3xl font-extrabold text-[#B4BD62]">
                Rp 49.000 <span className="text-xs font-normal text-[#FFF5D1]/70">/ bulan</span>
              </div>
              <p className="text-xs text-[#FFF5D1]/80 leading-relaxed">
                Solusi lengkap untuk menerbitkan dokumen resmi Paspor SLIKU yang siap dibagikan ke lembaga keuangan.
              </p>
              <ul className="space-y-3 text-xs font-medium pt-4 border-t border-[#8EBD9D]/30">
                <li className="flex items-center gap-2"><CheckCircle2 className="w-4 h-4 text-[#B4BD62]" /> Semua fitur Paket Rintisan</li>
                <li className="flex items-center gap-2"><CheckCircle2 className="w-4 h-4 text-[#B4BD62]" /> Analisis kesehatan usaha mendalam</li>
                <li className="flex items-center gap-2"><CheckCircle2 className="w-4 h-4 text-[#B4BD62]" /> Penerbitan resmi Dokumen Paspor SLIKU</li>
                <li className="flex items-center gap-2"><CheckCircle2 className="w-4 h-4 text-[#B4BD62]" /> Format khusus kurasi perbankan</li>
              </ul>
            </div>
            <a href="#simulasi" className="mt-8 w-full py-3.5 rounded-xl bg-[#B4BD62] text-[#0D3243] font-bold text-sm text-center block hover:bg-[#B4BD62]/90 transition-colors shadow-lg">
              Pilih Paket Pro
            </a>
          </div>
 
          {/* Paket 3 */}
          <div className="bg-[#FFF5D1] border-2 border-[#0D3243] rounded-3xl p-8 flex flex-col justify-between shadow-lg">
            <div className="space-y-4">
              <span className="text-xs font-bold uppercase tracking-wider bg-[#8EBD9D]/40 px-3 py-1 rounded-full text-[#0D3243] inline-block">
                Kolektif / Pendamping
              </span>
              <h3 className="text-2xl font-black text-[#0D3243]">Paket Komunitas / Dinas</h3>
              <div className="text-3xl font-extrabold text-[#0D3243]">Hubungi Kami</div>
              <p className="text-xs text-[#0D3243]/80 leading-relaxed">
                Dirancang khusus untuk inkubator bisnis, koperasi, atau dinas UMKM yang membina banyak pelaku usaha sekaligus.
              </p>
              <ul className="space-y-3 text-xs font-medium pt-4 border-t border-[#8EBD9D]/40">
                <li className="flex items-center gap-2"><CheckCircle2 className="w-4 h-4 text-[#B4BD62]" /> Manajemen multi-akun UMKM</li>
                <li className="flex items-center gap-2"><CheckCircle2 className="w-4 h-4 text-[#B4BD62]" /> Laporan rekap kesehatan kolektif</li>
                <li className="flex items-center gap-2"><CheckCircle2 className="w-4 h-4 text-[#B4BD62]" /> Pendampingan khusus &amp; pelatihan Ciku</li>
              </ul>
            </div>
            <a href="#kontak" className="mt-8 w-full py-3 rounded-xl bg-[#0D3243] text-[#FFF5D1] font-bold text-sm text-center block hover:bg-[#0D3243]/90 transition-colors">
              Hubungi Tim Kami
            </a>
          </div>
        </div>
      </section>
 
      {/* KALKULATOR */}
      <section id="simulasi" className="py-20 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div className="bg-[#FFF5D1] border-2 border-[#0D3243] rounded-3xl p-6 sm:p-10 shadow-xl">
          <div className="text-center max-w-2xl mx-auto mb-10 space-y-2">
            <span className="text-xs font-bold uppercase tracking-widest text-[#0D3243] bg-[#8EBD9D] px-3 py-1 rounded-full inline-block">
              Kalkulator Interaktif
            </span>
            <h2 className="text-3xl font-black text-[#0D3243]">Cek Kesiapan Paspor SLIKU Anda</h2>
            <p className="text-[#0D3243]/80 text-sm">
              Coba masukkan estimasi data sederhana usaha Anda di bawah ini untuk melihat gambaran skor kesiapan Paspor SLIKU!
            </p>
          </div>
 
          <div className="grid lg:grid-cols-12 gap-8 items-start">
            <form onSubmit={handleCalculate} className="lg:col-span-7 bg-white p-6 rounded-2xl border-2 border-[#0D3243] space-y-5">
              <div>
                <label className="block text-xs font-bold text-[#0D3243] uppercase mb-2">
                  Estimasi Omzet Penjualan Bulanan (Rp)
                </label>
                <input
                  type="number"
                  min="0"
                  value={omzet}
                  onChange={(e) => setOmzet(Number(e.target.value))}
                  className="w-full px-4 py-3 rounded-xl border-2 border-[#8EBD9D] focus:outline-none focus:border-[#0D3243] font-bold text-[#0D3243]"
                  placeholder="Contoh: 15000000"
                  required
                />
                <span className="text-[11px] text-[#0D3243]/60 mt-1 block">Rata-rata pemasukan usaha dalam 1 bulan.</span>
              </div>
 
              <div>
                <label className="block text-xs font-bold text-[#0D3243] uppercase mb-2">
                  Jumlah Transaksi Penjualan per Bulan
                </label>
                <input
                  type="number"
                  min="0"
                  value={transaksiCount}
                  onChange={(e) => setTransaksiCount(Number(e.target.value))}
                  className="w-full px-4 py-3 rounded-xl border-2 border-[#8EBD9D] focus:outline-none focus:border-[#0D3243] font-bold text-[#0D3243]"
                  placeholder="Contoh: 45"
                  required
                />
                <span className="text-[11px] text-[#0D3243]/60 mt-1 block">Berapa kali nota/transaksi terjadi dalam sebulan.</span>
              </div>
 
              <div>
                <label className="block text-xs font-bold text-[#0D3243] uppercase mb-2">
                  Lama Usaha Berjalan (Bulan)
                </label>
                <input
                  type="number"
                  min="0"
                  value={lamaUsaha}
                  onChange={(e) => setLamaUsaha(Number(e.target.value))}
                  className="w-full px-4 py-3 rounded-xl border-2 border-[#8EBD9D] focus:outline-none focus:border-[#0D3243] font-bold text-[#0D3243]"
                  placeholder="Contoh: 12"
                  required
                />
              </div>
 
              <button
                type="submit"
                disabled={isCalculating}
                className="w-full py-4 rounded-xl bg-[#0D3243] text-[#FFF5D1] font-bold text-base hover:bg-[#0D3243]/90 transition-all flex items-center justify-center gap-2 shadow-md disabled:opacity-70 disabled:cursor-not-allowed"
              >
                {isCalculating ? (
                  <>
                    <Loader2 className="w-5 h-5 animate-spin text-[#B4BD62]" />
                    <span>Ciku Sedang Menghitung...</span>
                  </>
                ) : (
                  <>
                    <Zap className="w-5 h-5 text-[#B4BD62]" />
                    <span>Hitung Skor Kesiapan Usaha</span>
                  </>
                )}
              </button>
            </form>
 
            <div className="lg:col-span-5 bg-[#8EBD9D]/20 p-6 rounded-2xl border-2 border-[#8EBD9D] min-h-[340px] flex flex-col justify-center items-center text-center">
              {result ? (
                <div className="space-y-4 w-full animate-fadeIn">
                  <div className="w-16 h-16 rounded-full bg-[#FFF5D1] border-2 border-[#0D3243] flex items-center justify-center text-3xl mx-auto shadow-md">
                    🐿️
                  </div>
 
                  <div className={`p-4 rounded-2xl border-2 ${result.color}`}>
                    <span className="text-xs font-bold uppercase tracking-wider block">Hasil Skor Kesiapan:</span>
                    <h3 className="text-3xl font-black mt-1">{result.score} / 100</h3>
                    <p className="text-sm font-extrabold mt-1">{result.status}</p>
                  </div>
 
                  <p className="text-xs text-[#0D3243]/80 leading-relaxed px-2">{result.desc}</p>
 
                  <button
                    type="button"
                    className="w-full py-2.5 rounded-xl bg-[#B4BD62] text-[#0D3243] font-bold text-xs hover:bg-[#B4BD62]/80 transition-all border border-[#0D3243]"
                  >
                    Unduh Draf Paspor SLIKU (PDF)
                  </button>
                </div>
              ) : (
                <div className="space-y-3">
                  <div className="w-16 h-16 rounded-full bg-[#FFF5D1] border-2 border-dashed border-[#0D3243] flex items-center justify-center text-3xl mx-auto opacity-70">
                    📊
                  </div>
                  <h4 className="font-bold text-[#0D3243]">Belum Ada Hasil Simulasi</h4>
                  <p className="text-xs text-[#0D3243]/70 max-w-xs mx-auto">
                    Isi form estimasi usaha di sebelah kiri lalu klik tombol "Hitung Skor Kesiapan Usaha" untuk melihat analisa dari Ciku!
                  </p>
                </div>
              )}
            </div>
          </div>
        </div>
      </section>
 
      {/* KONTAK */}
      <section id="kontak" className="py-20 bg-[#8EBD9D]/20 border-t border-[#8EBD9D]/40">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="grid lg:grid-cols-12 gap-12 items-center">
            <div className="lg:col-span-6 space-y-6">
              <span className="text-xs font-bold uppercase tracking-widest text-[#0D3243] bg-[#B4BD62] px-3 py-1 rounded-full inline-block">
                Hubungi Kami
              </span>
              <h2 className="text-3xl sm:text-4xl font-black text-[#0D3243]">Punya Pertanyaan Seputar Paspor SLIKU?</h2>
              <p className="text-[#0D3243]/80 leading-relaxed">
                Tim SLIKU dan maskot imut kami, Ciku, siap membantu UMKM Anda naik kelas dan siap mendapatkan pembiayaan dari lembaga keuangan. Kirimkan pesan Anda melalui formulir di samping!
              </p>
 
              <div className="space-y-3 pt-2">
                <div className="flex items-center gap-3 text-sm font-semibold text-[#0D3243]">
                  <div className="w-10 h-10 rounded-xl bg-[#FFF5D1] border border-[#0D3243] flex items-center justify-center">📧</div>
                  <span>halo@sliku.id / support@sliku.id</span>
                </div>
                <div className="flex items-center gap-3 text-sm font-semibold text-[#0D3243]">
                  <div className="w-10 h-10 rounded-xl bg-[#FFF5D1] border border-[#0D3243] flex items-center justify-center">📞</div>
                  <span>0812-SLIKU-PASPOR (Layanan WhatsApp UMKM)</span>
                </div>
              </div>
            </div>
 
            <div className="lg:col-span-6 bg-[#FFF5D1] border-2 border-[#0D3243] p-8 rounded-3xl shadow-xl">
              <form
                onSubmit={(e) => {
                  e.preventDefault();
                  alert('Terima kasih! Pesan Anda telah terkirim kepada tim SLIKU.');
                  e.target.reset();
                }}
                className="space-y-4"
              >
                <div>
                  <label className="block text-xs font-bold uppercase text-[#0D3243] mb-1">Nama Lengkap / Pemilik Usaha</label>
                  <input type="text" placeholder="Contoh: Budi Santoso" className="w-full px-4 py-3 rounded-xl border border-[#8EBD9D] bg-white text-[#0D3243] font-medium focus:outline-none focus:border-[#0D3243]" required />
                </div>
                <div>
                  <label className="block text-xs font-bold uppercase text-[#0D3243] mb-1">Nama Usaha UMKM</label>
                  <input type="text" placeholder="Contoh: Kedip Kopi Nusantara" className="w-full px-4 py-3 rounded-xl border border-[#8EBD9D] bg-white text-[#0D3243] font-medium focus:outline-none focus:border-[#0D3243]" required />
                </div>
                <div>
                  <label className="block text-xs font-bold uppercase text-[#0D3243] mb-1">Pesan / Kendala Usaha</label>
                  <textarea rows={4} placeholder="Ceritakan kebutuhan atau pertanyaan Anda di sini..." className="w-full px-4 py-3 rounded-xl border border-[#8EBD9D] bg-white text-[#0D3243] font-medium focus:outline-none focus:border-[#0D3243]" required></textarea>
                </div>
                <button type="submit" className="w-full py-4 rounded-xl bg-[#0D3243] text-[#FFF5D1] font-bold hover:bg-[#0D3243]/90 transition-colors shadow-md">
                  Kirim Pesan ke Tim SLIKU
                </button>
              </form>
            </div>
          </div>
        </div>
      </section>
 
      {/* FOOTER */}
      <footer className="bg-[#0D3243] text-[#FFF5D1] pt-16 pb-12 border-t-4 border-[#B4BD62]">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="grid md:grid-cols-4 gap-8 pb-12 border-b border-[#8EBD9D]/30">
            <div className="md:col-span-2 space-y-4">
              <div className="flex items-center gap-3">
                <div className="w-10 h-10 rounded-xl bg-[#FFF5D1] text-[#0D3243] flex items-center justify-center font-black">S</div>
                <span className="text-2xl font-black tracking-wider text-[#FFF5D1]">SLIKU</span>
              </div>
              <p className="text-sm text-[#FFF5D1]/80 max-w-sm leading-relaxed">
                Sistem Informasi Kesehatan Usaha &amp; Paspor UMKM. Mengubah pembukuan sederhana menjadi jembatan pembiayaan formal yang terpercaya.
              </p>
            </div>
 
            <div className="space-y-3">
              <h4 className="text-sm font-bold uppercase tracking-wider text-[#B4BD62]">Navigasi Cepat</h4>
              <ul className="space-y-2 text-xs text-[#FFF5D1]/80">
                <li><a href="#beranda" className="hover:text-[#B4BD62]">Beranda Utama</a></li>
                <li><a href="#fitur" className="hover:text-[#B4BD62]">Fitur Kesehatan Usaha</a></li>
                <li><a href="#paspor" className="hover:text-[#B4BD62]">Tentang Paspor SLIKU</a></li>
                <li><a href="#maskot" className="hover:text-[#B4BD62]">Maskot Ciku</a></li>
              </ul>
            </div>
 
            <div className="space-y-3">
              <h4 className="text-sm font-bold uppercase tracking-wider text-[#B4BD62]">Kontak &amp; Bantuan</h4>
              <ul className="space-y-2 text-xs text-[#FFF5D1]/80">
                <li>Email: halo@sliku.id</li>
                <li>Layanan UMKM: 0812-SLIKU-PASPOR</li>
                <li>Jakarta, Indonesia</li>
              </ul>
            </div>
          </div>
 
          <div className="pt-8 flex flex-col sm:flex-row items-center justify-between text-xs text-[#FFF5D1]/60 gap-4">
            <p>© {new Date().getFullYear()} SLIKU (Sistem Informasi Kesehatan Usaha). Hak Cipta Dilindungi.</p>
            <div className="flex gap-6">
              <a href="#" className="hover:text-[#B4BD62]">Kebijakan Privasi</a>
              <a href="#" className="hover:text-[#B4BD62]">Syarat &amp; Ketentuan</a>
            </div>
          </div>
        </div>
      </footer>
    </div>
  );
}
