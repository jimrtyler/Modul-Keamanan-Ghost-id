# 👻 Modul Keamanan Ghost
**Alat Pengerasan Keamanan Windows & Azure Berbasis PowerShell**

> **Pengerasan keamanan proaktif untuk endpoint Windows dan lingkungan Azure.** Ghost menyediakan fungsi pengerasan berbasis PowerShell yang dapat membantu mengurangi vektor serangan umum dengan menonaktifkan layanan dan protokol yang tidak perlu.

## ⚠️ Peringatan Penting

**PENGUJIAN DIPERLUKAN**: Selalu uji Ghost di lingkungan non-produksi terlebih dahulu. Menonaktifkan layanan dapat berdampak pada fungsi bisnis yang sah.

**TIDAK ADA JAMINAN**: Meskipun Ghost menargetkan vektor serangan umum, tidak ada alat keamanan yang dapat mencegah semua serangan. Ini adalah satu komponen dari strategi keamanan komprehensif.

**DAMPAK OPERASIONAL**: Beberapa fungsi dapat mempengaruhi fungsionalitas sistem. Tinjau setiap pengaturan dengan hati-hati sebelum penerapan.

**PENILAIAN PROFESIONAL**: Untuk lingkungan produksi, konsultasikan dengan profesional keamanan untuk memastikan pengaturan selaras dengan kebutuhan organisasi Anda.

## 📊 Lanskap Keamanan

Kerugian ransomware mencapai **$57 miliar pada tahun 2025**, dengan penelitian menunjukkan bahwa banyak serangan yang berhasil mengeksploitasi layanan Windows dasar dan konfigurasi yang salah. Vektor serangan umum meliputi:

- **90% insiden ransomware** melibatkan eksploitasi RDP
- **Kerentanan SMBv1** memungkinkan serangan seperti WannaCry dan NotPetya  
- **Makro dokumen** tetap menjadi metode utama pengiriman malware
- **Serangan berbasis USB** terus menargetkan jaringan yang terisolasi
- **Penyalahgunaan PowerShell** telah meningkat secara signifikan dalam beberapa tahun terakhir

## 🛡️ Fungsi Keamanan Ghost

Ghost menyediakan **16 fungsi pengerasan Windows** plus **integrasi keamanan Azure**:

### Pengerasan Endpoint Windows

| Fungsi | Tujuan | Pertimbangan |
|----------|---------|----------------|
| `Set-RDP` | Mengelola akses Remote Desktop | Dapat berdampak pada administrasi jarak jauh |
| `Set-SMBv1` | Mengontrol protokol SMB legacy | Diperlukan untuk sistem sangat lama |
| `Set-AutoRun` | Mengontrol AutoPlay/AutoRun | Dapat berdampak pada kenyamanan pengguna |
| `Set-USBStorage` | Membatasi perangkat penyimpanan USB | Dapat berdampak pada penggunaan USB yang sah |
| `Set-Macros` | Mengontrol eksekusi makro Office | Dapat berdampak pada dokumen yang menggunakan makro |
| `Set-PSRemoting` | Mengelola PowerShell remoting | Dapat berdampak pada manajemen jarak jauh |
| `Set-WinRM` | Mengontrol Windows Remote Management | Dapat mempengaruhi administrasi jarak jauh |
| `Set-LLMNR` | Mengelola protokol resolusi nama | Biasanya aman untuk dinonaktifkan |
| `Set-NetBIOS` | Mengontrol NetBIOS over TCP/IP | Dapat mempengaruhi aplikasi legacy |
| `Set-AdminShares` | Mengelola administrative shares | Dapat berdampak pada akses file jarak jauh |
| `Set-Telemetry` | Mengontrol pengumpulan data | Dapat mempengaruhi kemampuan diagnostik |
| `Set-GuestAccount` | Mengelola akun Guest | Biasanya aman untuk dinonaktifkan |
| `Set-ICMP` | Mengontrol respons ping | Dapat mempengaruhi diagnostik jaringan |
| `Set-RemoteAssistance` | Mengelola Remote Assistance | Dapat berdampak pada operasi help desk |
| `Set-NetworkDiscovery` | Mengontrol network discovery | Dapat mempengaruhi browsing jaringan |
| `Set-Firewall` | Mengelola Windows Firewall | Kritis untuk keamanan jaringan |

### Keamanan Cloud Azure

| Fungsi | Tujuan | Persyaratan |
|----------|---------|--------------|
| `Set-AzureSecurityDefaults` | Mengaktifkan keamanan dasar Azure AD | Izin Microsoft Graph |
| `Set-AzureConditionalAccess` | Mengkonfigurasi kebijakan akses | Lisensi Azure AD P1/P2 |
| `Set-AzurePrivilegedUsers` | Mengaudit akun berotorisasi | Izin Global Admin |

### Opsi Penerapan Enterprise

| Metode | Kasus Penggunaan | Persyaratan |
|--------|----------|--------------|
| **Eksekusi Langsung** | Pengujian, lingkungan kecil | Hak admin lokal |
| **Group Policy** | Lingkungan domain | Admin domain, manajemen GP |
| **Microsoft Intune** | Perangkat yang dikelola cloud | Lisensi Intune, Graph API |

## 🚀 Mulai Cepat

### Penilaian Keamanan
```powershell
# Muat modul Ghost
IEX(Invoke-WebRequest 'https://raw.githubusercontent.com/jimrtyler/Ghost/main/Ghost.ps1')

# Periksa postur keamanan saat ini
Get-Ghost
```

### Pengerasan Dasar (Uji Terlebih Dahulu)
```powershell
# Pengerasan esensial - uji di lingkungan lab terlebih dahulu
Set-Ghost -SMBv1 -AutoRun -Macros

# Tinjau perubahan
Get-Ghost
```

### Penerapan Enterprise
```powershell
# Penerapan Group Policy (lingkungan domain)
Set-Ghost -SMBv1 -AutoRun -GroupPolicy

# Penerapan Intune (perangkat yang dikelola cloud)
Set-Ghost -SMBv1 -RDP -USBStorage -Intune
```

## 📋 Metode Instalasi

### Opsi 1: Download Langsung (Pengujian)
```powershell
IEX(Invoke-WebRequest 'https://raw.githubusercontent.com/jimrtyler/Ghost/main/Ghost.ps1')
```

### Opsi 2: Instalasi Modul
```powershell
# Install dari PowerShell Gallery (ketika tersedia)
Install-Module Ghost -Scope CurrentUser
Import-Module Ghost
```

### Opsi 3: Penerapan Enterprise
```powershell
# Salin ke lokasi jaringan untuk penerapan Group Policy
# Konfigurasi skrip PowerShell Intune untuk penerapan cloud
```

## 💼 Contoh Kasus Penggunaan

### Usaha Kecil
```powershell
# Perlindungan dasar dengan dampak minimal
Set-Ghost -SMBv1 -AutoRun -Macros -ICMP
```

### Lingkungan Kesehatan
```powershell
# Pengerasan yang berfokus pada HIPAA
Set-Ghost -SMBv1 -RDP -USBStorage -AdminShares -Telemetry
```

### Layanan Keuangan
```powershell
# Konfigurasi keamanan tinggi
Set-Ghost -RDP -SMBv1 -AutoRun -USBStorage -Macros -PSRemoting -AdminShares
```

### Organisasi Cloud-First
```powershell
# Penerapan yang dikelola Intune
Connect-IntuneGhost -Interactive
Set-Ghost -SMBv1 -RDP -AutoRun -Macros -Intune
```

## 🔍 Detail Fungsi

### Fungsi Pengerasan Inti

#### Layanan Jaringan
- **RDP**: Memblokir akses remote desktop atau merandomisasi port
- **SMBv1**: Menonaktifkan protokol file sharing legacy
- **ICMP**: Mencegah respons ping untuk reconnaissance
- **LLMNR/NetBIOS**: Memblokir protokol resolusi nama legacy

#### Keamanan Aplikasi  
- **Makro**: Menonaktifkan eksekusi makro di aplikasi Office
- **AutoRun**: Mencegah eksekusi otomatis dari media yang dapat dilepas

#### Manajemen Jarak Jauh
- **PSRemoting**: Menonaktifkan sesi PowerShell jarak jauh
- **WinRM**: Menghentikan Windows Remote Management
- **Remote Assistance**: Memblokir koneksi remote assistance

#### Kontrol Akses
- **Admin Shares**: Menonaktifkan shares C$, ADMIN$
- **Guest Account**: Menonaktifkan akses akun Guest
- **USB Storage**: Membatasi penggunaan perangkat USB

### Integrasi Azure
```powershell
# Terhubung ke tenant Azure
Connect-AzureGhost -Interactive

# Aktifkan default keamanan
Set-AzureSecurityDefaults -Enable

# Konfigurasi akses bersyarat
Set-AzureConditionalAccess -BlockLegacyAuth -RequireMFA

# Audit pengguna berotorisasi
Set-AzurePrivilegedUsers -AuditOnly
```

### Integrasi Intune (Baru di v2)
```powershell
# Terhubung ke Intune
Connect-IntuneGhost -Interactive

# Deploy melalui kebijakan Intune
Set-IntuneGhost -Settings @{
    RDP = $true
    SMBv1 = $true
    USBStorage = $true
    Macros = $true
}
```

## ⚠️ Pertimbangan Penting

### Persyaratan Pengujian
- **Lingkungan Lab**: Uji semua pengaturan di lingkungan terisolasi terlebih dahulu
- **Penerapan Bertahap**: Roll out secara bertahap untuk mengidentifikasi masalah
- **Rencana Rollback**: Pastikan Anda dapat membalikkan perubahan jika diperlukan
- **Dokumentasi**: Catat pengaturan mana yang berfungsi untuk lingkungan Anda

### Dampak Potensial
- **Produktivitas Pengguna**: Beberapa pengaturan dapat mempengaruhi alur kerja harian
- **Aplikasi Legacy**: Sistem lama mungkin memerlukan protokol tertentu
- **Akses Jarak Jauh**: Pertimbangkan dampak pada administrasi jarak jauh yang sah
- **Proses Bisnis**: Verifikasi bahwa pengaturan tidak merusak fungsi kritis

### Keterbatasan Keamanan
- **Defense in Depth**: Ghost adalah satu lapisan keamanan, bukan solusi lengkap
- **Manajemen Berkelanjutan**: Keamanan memerlukan pemantauan dan pembaruan berkelanjutan
- **Pelatihan Pengguna**: Kontrol teknis harus dipasangkan dengan kesadaran keamanan
- **Evolusi Ancaman**: Metode serangan baru dapat melewati perlindungan saat ini

## 🎯 Contoh Skenario Serangan

Sementara Ghost menargetkan vektor serangan umum, pencegahan spesifik tergantung pada implementasi dan pengujian yang tepat:

### Serangan Gaya WannaCry
- **Mitigasi**: `Set-Ghost -SMBv1` menonaktifkan protokol yang rentan
- **Pertimbangan**: Pastikan tidak ada sistem legacy yang memerlukan SMBv1

### Ransomware Berbasis RDP
- **Mitigasi**: `Set-Ghost -RDP` memblokir akses remote desktop
- **Pertimbangan**: Mungkin memerlukan metode akses jarak jauh alternatif

### Malware Berbasis Dokumen
- **Mitigasi**: `Set-Ghost -Macros` menonaktifkan eksekusi makro
- **Pertimbangan**: Dapat berdampak pada dokumen yang menggunakan makro secara sah

### Ancaman yang Dibawa USB
- **Mitigasi**: `Set-Ghost -USBStorage -AutoRun` membatasi fungsionalitas USB
- **Pertimbangan**: Dapat berdampak pada penggunaan perangkat USB yang sah

## 🏢 Fitur Enterprise

### Dukungan Group Policy
```powershell
# Terapkan pengaturan melalui registry Group Policy
Set-Ghost -SMBv1 -RDP -AutoRun -GroupPolicy

# Pengaturan berlaku di seluruh domain setelah refresh GP
gpupdate /force
```

### Integrasi Microsoft Intune
```powershell
# Buat kebijakan Intune untuk pengaturan Ghost
Set-IntuneGhost -Settings $GhostSettings -Interactive

# Kebijakan deploy ke perangkat yang dikelola secara otomatis
```

### Pelaporan Kepatuhan
```powershell
# Generate laporan penilaian keamanan
Get-Ghost | Export-Csv -Path "SecurityAudit-$(Get-Date -Format 'yyyy-MM-dd').csv"

# Laporan postur keamanan Azure
Get-AzureGhost | Out-File "AzureSecurityReport.txt"
```

## 📚 Praktik Terbaik

### Pra-Penerapan
1. **Dokumentasikan Status Saat Ini**: Jalankan `Get-Ghost` sebelum perubahan
2. **Uji Secara Menyeluruh**: Validasi di lingkungan non-produksi
3. **Rencanakan Rollback**: Ketahui cara membalikkan setiap pengaturan
4. **Tinjauan Stakeholder**: Pastikan unit bisnis menyetujui perubahan

### Selama Penerapan
1. **Pendekatan Bertahap**: Deploy ke grup pilot terlebih dahulu
2. **Monitor Dampak**: Perhatikan keluhan pengguna atau masalah sistem
3. **Dokumentasikan Masalah**: Catat masalah apa pun untuk referensi masa depan
4. **Komunikasikan Perubahan**: Informasikan pengguna tentang peningkatan keamanan

### Pasca-Penerapan
1. **Penilaian Rutin**: Jalankan `Get-Ghost` secara berkala untuk verifikasi pengaturan
2. **Perbarui Dokumentasi**: Jaga konfigurasi keamanan tetap terkini
3. **Tinjau Efektivitas**: Monitor insiden keamanan
4. **Perbaikan Berkelanjutan**: Sesuaikan pengaturan berdasarkan lanskap ancaman

## 🔧 Pemecahan Masalah

### Masalah Umum
- **Error Izin**: Pastikan sesi PowerShell elevated
- **Dependensi Layanan**: Beberapa layanan mungkin memiliki dependensi
- **Kompatibilitas Aplikasi**: Uji dengan aplikasi bisnis
- **Konektivitas Jaringan**: Verifikasi akses jarak jauh masih berfungsi

### Opsi Pemulihan
```powershell
# Aktifkan kembali layanan tertentu jika diperlukan
Set-RDP -Enable
Set-SMBv1 -Enable
Set-AutoRun -Enable
Set-Macros -Enable
```

## 👨‍💻 Tentang Penulis

**Jim Tyler** - Microsoft MVP untuk PowerShell
- **YouTube**: [@PowerShellEngineer](https://youtube.com/@PowerShellEngineer) (10.000+ subscriber)
- **Newsletter**: [PowerShell.News](https://powershell.news) - Intelijen keamanan mingguan
- **Penulis**: "PowerShell for Systems Engineers"
- **Pengalaman**: Puluhan tahun otomasi PowerShell dan keamanan Windows

## 📄 Lisensi & Penafian

### Lisensi MIT
Ghost disediakan di bawah Lisensi MIT untuk penggunaan, modifikasi, dan distribusi gratis.

### Penafian Keamanan
- **Tanpa Jaminan**: Ghost disediakan "apa adanya" tanpa jaminan apa pun
- **Pengujian Diperlukan**: Selalu uji di lingkungan non-produksi terlebih dahulu
- **Panduan Profesional**: Konsultasikan dengan profesional keamanan untuk penerapan produksi
- **Dampak Operasional**: Penulis tidak bertanggung jawab atas gangguan operasional apa pun
- **Keamanan Komprehensif**: Ghost adalah satu komponen dari strategi keamanan lengkap

### Dukungan
- **GitHub Issues**: [Laporkan bug atau minta fitur](https://github.com/jimrtyler/Ghost/issues)
- **Dokumentasi**: Gunakan `Get-Help <function> -Full` untuk bantuan terperinci
- **Komunitas**: Forum komunitas PowerShell dan keamanan

---

**🔒 Perkuat postur keamanan Anda dengan Ghost - tetapi selalu uji terlebih dahulu.**

```powershell
# Mulai dengan penilaian, bukan asumsi
Get-Ghost
```

**⭐ Beri bintang repository ini jika Ghost membantu meningkatkan postur keamanan Anda!**