# Volatility 3 Windows Commands — Cheat Sheet

> Format: **Command | Deskripsi | Cara penggunaan**
>
> Basis daftar command: command list yang terlihat pada screenshot Volatility 3 yang diberikan.
> Contoh penggunaan menggunakan pola Volatility 3 CLI yang umum. Jika suatu plugin tidak menerima opsi tertentu pada versi Volatility yang dipakai, cek `--help`.

## Cara baca sintaks

| Sintaks | Fungsi |
| --- | --- |
| `-f <file>` | Menentukan memory dump yang dianalisis |
| `--pid <PID>` | Membatasi analisis ke process ID tertentu, jika plugin mendukungnya |
| `\| grep <kata>` | Menyaring output berdasarkan teks |
| `grep -i <kata>` | `grep` tanpa membedakan huruf besar/kecil |
| `-h` / `--help` | Melihat opsi yang tersedia untuk plugin |
| `-q` | Quiet mode pada command tertentu/versi tertentu; jangan diasumsikan tersedia pada semua plugin |
| `-r <regex>` | Regex pada plugin yang mendukung pencarian/filter regex |

## Command dasar

| Command | Deskripsi | Cara penggunaan |
| --- | --- | --- |
| `windows.bigpools` | Menampilkan informasi Big Pool/kernel pool yang ditemukan di memory. Berguna untuk investigasi objek/alokasi kernel tertentu. | Dasar: `vol -f Memory.raw windows.bigpools`<br>Filter: `vol -f Memory.raw windows.bigpools \| grep -i "kata"` |
| `windows.callbacks` | Menampilkan callback kernel yang terdaftar. Berguna untuk mencari callback yang tidak biasa. | Dasar: `vol -f Memory.raw windows.callbacks`<br>Filter: `vol -f Memory.raw windows.callbacks \| grep -i "kata"` |
| `windows.cmdline` | Menampilkan command line proses. Berguna untuk mengetahui argumen yang digunakan saat proses dijalankan. | Dasar: `vol -f Memory.raw windows.cmdline`<br>PID: `vol -f Memory.raw windows.cmdline --pid 880`<br>Filter: `vol -f Memory.raw windows.cmdline \| grep -i "powershell"` |
| `windows.cmdscan` | Mencari command yang tersimpan di console command history/buffer Windows. | Dasar: `vol -f Memory.raw windows.cmdscan`<br>Filter: `vol -f Memory.raw windows.cmdscan \| grep -i "cmd"` |
| `windows.consoles` | Menampilkan informasi console Windows dan command yang berhubungan dengannya. | Dasar: `vol -f Memory.raw windows.consoles`<br>Filter: `vol -f Memory.raw windows.consoles \| grep -i "whoami"` |
| `windows.crashinfo` | Menampilkan informasi yang berkaitan dengan crash dump/header crash information jika tersedia. | `vol -f Memory.raw windows.crashinfo` |
| `windows.debugregisters` | Menampilkan debug registers proses/thread yang ditemukan di memory. | Dasar: `vol -f Memory.raw windows.debugregisters`<br>Filter: `vol -f Memory.raw windows.debugregisters \| grep -i "PID"` |
| `windows.deskscan` | Melakukan scan terhadap objek desktop Windows. | `vol -f Memory.raw windows.deskscan` |
| `windows.desktops` | Menampilkan objek desktop/window-station yang ditemukan. | `vol -f Memory.raw windows.desktops` |
| `windows.devicetree` | Menampilkan device tree Windows dan hubungan objek device. | `vol -f Memory.raw windows.devicetree` |
| `windows.dlllist` | Menampilkan DLL/module yang terhubung dengan proses melalui struktur loader. | Dasar: `vol -f Memory.raw windows.dlllist`<br>PID: `vol -f Memory.raw windows.dlllist --pid 880`<br>Filter: `vol -f Memory.raw windows.dlllist --pid 880 \| grep -i "dll"` |
| `windows.driverirp` | Menampilkan informasi IRP/function table pada driver. Berguna dalam analisis driver/kernel. | `vol -f Memory.raw windows.driverirp`<br>Filter: `vol -f Memory.raw windows.driverirp \| grep -i "driver"` |
| `windows.driverscan` | Melakukan scan memory untuk menemukan objek driver. | `vol -f Memory.raw windows.driverscan`<br>Filter: `vol -f Memory.raw windows.driverscan \| grep -i "sys"` |
| `windows.dumpfiles` | Mengekstrak file/cache object yang ditemukan dari memory. | Dasar: `vol -f Memory.raw windows.dumpfiles`<br>Output directory: `vol -f Memory.raw windows.dumpfiles -D dumped_files/`<br>Filter output: `vol -f Memory.raw windows.dumpfiles \| grep -i ".exe"` |
| `windows.envars` | Menampilkan environment variables proses. | Dasar: `vol -f Memory.raw windows.envars`<br>PID: `vol -f Memory.raw windows.envars --pid 880`<br>Filter: `vol -f Memory.raw windows.envars \| grep -i "PATH"` |
| `windows.etwpatch` | Memeriksa informasi/indikator patching pada ETW (Event Tracing for Windows). | `vol -f Memory.raw windows.etwpatch` |
| `windows.filescan` | Melakukan scan memory untuk menemukan objek file `_FILE_OBJECT`. | `vol -f Memory.raw windows.filescan`<br>Filter: `vol -f Memory.raw windows.filescan \| grep -i "str.sys"` |
| `windows.getservicesids` | Menampilkan pemetaan Service SID yang dapat ditemukan dari konfigurasi/registry terkait service. | `vol -f Memory.raw windows.getservicesids` |
| `windows.getsids` | Menampilkan SID yang terkait dengan proses/token. | Dasar: `vol -f Memory.raw windows.getsids`<br>PID: `vol -f Memory.raw windows.getsids --pid 880` |
| `windows.handles` | Menampilkan handle yang dimiliki proses ke object kernel seperti file, registry, process, thread, event, dan lainnya. | Dasar: `vol -f Memory.raw windows.handles`<br>PID: `vol -f Memory.raw windows.handles --pid 880`<br>Filter teks: `vol -f Memory.raw windows.handles --pid 880 \| grep -i "str.sys"` |
| `windows.iat` | Menganalisis Import Address Table (IAT) dari executable/module yang ditemukan. | `vol -f Memory.raw windows.iat` |
| `windows.info` | Menampilkan informasi dasar OS/kernel dari memory dump, seperti versi Windows dan build. | `vol -f Memory.raw windows.info` |
| `windows.joblinks` | Menampilkan hubungan job object dengan proses yang terkait. | `vol -f Memory.raw windows.joblinks` |
| `windows.kpcrs` | Menampilkan Kernel Processor Control Region (KPCR) yang ditemukan. | `vol -f Memory.raw windows.kpcrs` |
| `windows.malware.direct_system_calls` | Mencari indikasi direct system calls pada proses/module sebagai bagian dari analisis malware. | `vol -f Memory.raw windows.malware.direct_system_calls`<br>Jika plugin mendukung PID: `... --pid 880` |
| `windows.malware.drivermodule` | Menghubungkan/menganalisis module driver yang ditemukan pada memory. | `vol -f Memory.raw windows.malware.drivermodule` |
| `windows.malware.hollowprocesses` | Mencari indikasi process hollowing. | `vol -f Memory.raw windows.malware.hollowprocesses` |
| `windows.malware.indirect_system_calls` | Mencari indikasi indirect system calls yang dapat digunakan malware untuk menghindari pola API biasa. | `vol -f Memory.raw windows.malware.indirect_system_calls` |
| `windows.malware.ldrmodules` | Membandingkan daftar module dari beberapa linked list loader untuk menemukan module yang tidak terhubung/unlinked. Sangat berguna untuk indikasi DLL hiding. | Dasar: `vol -f Memory.raw windows.malware.ldrmodules`<br>PID: `vol -f Memory.raw windows.malware.ldrmodules --pid 880`<br>Filter: `vol -f Memory.raw windows.malware.ldrmodules --pid 880 \| grep -i "False"` |
| `windows.malware.malfind` | Mencari region memory yang mencurigakan, misalnya indikasi code injection. | Dasar: `vol -f Memory.raw windows.malware.malfind`<br>PID: `vol -f Memory.raw windows.malware.malfind --pid 880` |
| `windows.malware.pebmasquerade` | Mencari indikasi manipulasi/masquerading terhadap Process Environment Block (PEB). | `vol -f Memory.raw windows.malware.pebmasquerade` |
| `windows.malware.processghosting` | Mencari indikasi Process Ghosting. | `vol -f Memory.raw windows.malware.processghosting` |
| `windows.malware.psxview` | Membandingkan beberapa sumber enumerasi proses untuk menemukan proses yang mungkin disembunyikan. | Dasar: `vol -f Memory.raw windows.malware.psxview`<br>Filter: `vol -f Memory.raw windows.malware.psxview \| grep -i "False"` |
| `windows.malware.skeleton_key_check` | Memeriksa indikator teknik Skeleton Key pada Active Directory/domain environment. | `vol -f Memory.raw windows.malware.skeleton_key_check` |
| `windows.malware.suspicious_threads` | Mencari thread yang memiliki karakteristik mencurigakan. | `vol -f Memory.raw windows.malware.suspicious_threads`<br>Jika mendukung PID: `... --pid 880` |
| `windows.malware.svcdiff` | Membandingkan informasi service untuk menemukan perbedaan/anomali. | `vol -f Memory.raw windows.malware.svcdiff` |
| `windows.malware.unhooked_system_calls` | Mencari system call/API yang tampak tidak ter-hook atau memiliki indikasi anomali. | `vol -f Memory.raw windows.malware.unhooked_system_calls` |
| `windows.mbrscan` | Melakukan scan untuk Master Boot Record (MBR) signature/struktur yang ditemukan dalam memory. | `vol -f Memory.raw windows.mbrscan` |
| `windows.memmap` | Menampilkan pemetaan virtual address ke memory/physical mapping untuk suatu proses. Berguna untuk memahami region memory proses. | Dasar: `vol -f Memory.raw windows.memmap --pid 880`<br>Filter: `vol -f Memory.raw windows.memmap --pid 880 \| grep -i "980000"` |
| `windows.mftscan.ADS` | Mencari Alternate Data Streams (ADS) dari struktur NTFS/MFT yang ditemukan. | `vol -f Memory.raw windows.mftscan.ADS` |
| `windows.mftscan.MFTScan` | Melakukan scan untuk struktur Master File Table (MFT) NTFS. | `vol -f Memory.raw windows.mftscan.MFTScan`<br>Filter: `vol -f Memory.raw windows.mftscan.MFTScan \| grep -i ".exe"` |
| `windows.mftscan.ResidentData` | Mencari data resident yang tersimpan langsung di record MFT. | `vol -f Memory.raw windows.mftscan.ResidentData` |
| `windows.modscan` | Melakukan scan memory untuk menemukan kernel modules. | `vol -f Memory.raw windows.modscan`<br>Filter: `vol -f Memory.raw windows.modscan \| grep -i ".sys"` |
| `windows.modules` | Menampilkan kernel modules yang terdaftar/ditemukan. | `vol -f Memory.raw windows.modules`<br>Filter: `vol -f Memory.raw windows.modules \| grep -i "driver"` |
| `windows.mutantscan` | Melakukan scan untuk mutant/mutex objects Windows. Berguna untuk menemukan mutex yang mungkin berkaitan dengan malware. | `vol -f Memory.raw windows.mutantscan`<br>Filter: `vol -f Memory.raw windows.mutantscan \| grep -i "mutex"` |
| `windows.netscan` | Mencari network connection/socket artifacts dari memory. | Dasar: `vol -f Memory.raw windows.netscan`<br>Filter: `vol -f Memory.raw windows.netscan \| grep -i "ESTABLISHED"`<br>Filter PID: `vol -f Memory.raw windows.netscan \| grep "880"` |
| `windows.netstat` | Menampilkan informasi network state yang dapat direkonstruksi dari memory. | `vol -f Memory.raw windows.netstat`<br>Filter: `vol -f Memory.raw windows.netstat \| grep -i "ESTABLISHED"` |
| `windows.orphan_kernel_threads` | Mencari kernel thread yang tampak orphan/tidak memiliki hubungan normal. | `vol -f Memory.raw windows.orphan_kernel_threads` |
| `windows.pe_symbols` | Menampilkan/menganalisis PE symbols yang tersedia untuk executable/module. | `vol -f Memory.raw windows.pe_symbols` |
| `windows.pedump` | Mengekstrak PE image/module dari memory. Berguna untuk mengambil executable/DLL untuk analisis lanjutan. | Dasar: `vol -f Memory.raw windows.pedump`<br>Output directory: `vol -f Memory.raw windows.pedump -D dumped_pe/` |
| `windows.poolscanner` | Melakukan pool scan untuk menemukan objek kernel berdasarkan pool tag/signature. | `vol -f Memory.raw windows.poolscanner`<br>Filter: `vol -f Memory.raw windows.poolscanner \| grep -i "Process"` |
| `windows.privileges` | Menampilkan privilege/token privilege yang dimiliki proses. | Dasar: `vol -f Memory.raw windows.privileges`<br>PID: `vol -f Memory.raw windows.privileges --pid 880` |
| `windows.pslist` | Menampilkan proses yang terdaftar dalam process list Windows. | Dasar: `vol -f Memory.raw windows.pslist`<br>Filter: `vol -f Memory.raw windows.pslist \| grep -i "svchost"` |
| `windows.psscan` | Melakukan scan memory untuk menemukan process objects, termasuk proses yang mungkin sudah keluar/tersembunyi dari list normal. | `vol -f Memory.raw windows.psscan`<br>Filter: `vol -f Memory.raw windows.psscan \| grep -i "rootkit"` |
| `windows.pstree` | Menampilkan hubungan parent-child antar proses dalam bentuk tree. | Dasar: `vol -f Memory.raw windows.pstree`<br>Filter: `vol -f Memory.raw windows.pstree \| grep -i "cmd"` |
| `windows.registry.amcache` | Menganalisis AmCache dari registry untuk artefact aplikasi/executable. | `vol -f Memory.raw windows.registry.amcache`<br>Filter: `vol -f Memory.raw windows.registry.amcache \| grep -i ".exe"` |
| `windows.registry.cachedump` | Mengambil cached domain logon information dari registry memory artefacts. | `vol -f Memory.raw windows.registry.cachedump` |
| `windows.registry.certificates` | Menampilkan certificate information yang ditemukan pada registry. | `vol -f Memory.raw windows.registry.certificates` |
| `windows.registry.getcellroutine` | Menampilkan/menelusuri cell routine pada registry hive structures. | `vol -f Memory.raw windows.registry.getcellroutine` |
| `windows.registry.hashdump` | Mengekstrak password hash dari registry SAM/SYSTEM bila artefact yang dibutuhkan tersedia. | `vol -f Memory.raw windows.registry.hashdump` |
| `windows.registry.hivelist` | Menampilkan registry hive yang ditemukan dalam memory. | `vol -f Memory.raw windows.registry.hivelist` |
| `windows.registry.hivescan` | Melakukan scan memory untuk menemukan registry hive structures. | `vol -f Memory.raw windows.registry.hivescan` |
| `windows.registry.lsadump` | Mengekstrak informasi LSA secrets dari registry/memory artefacts. | `vol -f Memory.raw windows.registry.lsadump` |
| `windows.registry.printkey` | Membaca registry key/value tertentu. | Dasar: `vol -f Memory.raw windows.registry.printkey`<br>Untuk key tertentu gunakan opsi path/key yang tersedia pada `vol ... windows.registry.printkey --help` |
| `windows.registry.scheduled_tasks` | Menganalisis scheduled task yang tersimpan pada registry. | `vol -f Memory.raw windows.registry.scheduled_tasks`<br>Filter: `vol -f Memory.raw windows.registry.scheduled_tasks \| grep -i "task"` |
| `windows.registry.userassist` | Menampilkan UserAssist artefacts yang dapat menunjukkan aktivitas aplikasi melalui registry. | Dasar: `vol -f Memory.raw windows.registry.userassist`<br>Filter: `vol -f Memory.raw windows.registry.userassist \| grep -i "Brave"` |
| `windows.sessions` | Menampilkan session Windows yang ditemukan. | `vol -f Memory.raw windows.sessions` |
| `windows.shimcachemem` | Menganalisis ShimCache/AppCompatCache data yang berada di memory. | `vol -f Memory.raw windows.shimcachemem`<br>Filter: `vol -f Memory.raw windows.shimcachemem \| grep -i ".exe"` |
| `windows.ssdtscan` | Melakukan scan terhadap System Service Descriptor Table (SSDT). | `vol -f Memory.raw windows.ssdtscan` |
| `windows.statistics` | Menampilkan statistik tertentu yang dapat dikumpulkan dari memory/kernel structures. | `vol -f Memory.raw windows.statistics` |
| `windows.strings` | Mencari/memetakan string ke virtual address/process context. Berguna untuk menemukan URL, path, command, atau IOC. | Dasar: `vol -f Memory.raw windows.strings --strings-file strings.txt` jika opsi tersebut tersedia pada versi plugin.<br>Selalu cek: `vol ... windows.strings --help` |
| `windows.suspended_threads` | Menampilkan thread yang berada dalam kondisi suspended. | `vol -f Memory.raw windows.suspended_threads` |
| `windows.svclist` | Menampilkan Windows services yang ditemukan. | `vol -f Memory.raw windows.svclist`<br>Filter: `vol -f Memory.raw windows.svclist \| grep -i "service"` |
| `windows.svcscan` | Melakukan scan memory untuk menemukan Windows services, termasuk artefact service yang mungkin tidak muncul dari enumerasi normal. | `vol -f Memory.raw windows.svcscan`<br>Filter: `vol -f Memory.raw windows.svcscan \| grep -i "svchost"` |
| `windows.symlinkscan` | Melakukan scan untuk symbolic link objects Windows. | `vol -f Memory.raw windows.symlinkscan`<br>Filter: `vol -f Memory.raw windows.symlinkscan \| grep -i "link"` |
| `windows.thrdscan` | Melakukan scan memory untuk menemukan thread objects. | `vol -f Memory.raw windows.thrdscan`<br>Filter: `vol -f Memory.raw windows.thrdscan \| grep "880"` |
| `windows.threads` | Menampilkan thread yang terkait dengan proses. | Dasar: `vol -f Memory.raw windows.threads`<br>PID: `vol -f Memory.raw windows.threads --pid 880` |
| `windows.timers` | Menampilkan kernel timers yang ditemukan. Berguna untuk investigasi aktivitas kernel tertentu. | `vol -f Memory.raw windows.timers` |
| `windows.timedump` | Menampilkan timestamp/time-related dump information jika tersedia pada plugin/version yang digunakan. | `vol -f Memory.raw windows.timedump` |
| `windows.unloadedmodules` | Menampilkan module yang sudah di-unload tetapi artefact-nya masih dapat ditemukan. Berguna untuk investigasi module yang pernah aktif. | `vol -f Memory.raw windows.unloadedmodules`<br>Filter: `vol -f Memory.raw windows.unloadedmodules \| grep -i ".sys"` |
| `windows.vadinfo` | Menampilkan Virtual Address Descriptor (VAD) dan region virtual memory milik proses. | Dasar: `vol -f Memory.raw windows.vadinfo --pid 880`<br>Filter: `vol -f Memory.raw windows.vadinfo --pid 880 \| grep -i "PAGE_EXECUTE"` |
| `windows.vadregexscan` | Mencari pola/regex pada VAD memory regions. | Cek opsi dulu: `vol -f Memory.raw windows.vadregexscan --help`<br>Lalu gunakan opsi regex/pattern yang disediakan versi plugin |
| `windows.vadwalk` | Menelusuri struktur VAD tree suatu proses. | `vol -f Memory.raw windows.vadwalk --pid 880` |
| `windows.vadyarascan` | Melakukan YARA scan terhadap VAD memory regions. | Dasar: `vol -f Memory.raw windows.vadyarascan --pid 880 --yara-rules rule.yar`<br>Nama opsi dapat berbeda menurut versi; cek `--help` |
| `windows.verinfo` | Menampilkan version information dari PE/module yang ditemukan. | `vol -f Memory.raw windows.verinfo` |
| `windows.virtmap` | Menampilkan virtual memory mapping yang ditemukan. | `vol -f Memory.raw windows.virtmap` |
| `windows.windows` | Menampilkan window objects/window information yang ditemukan pada Windows GUI subsystem. | `vol -f Memory.raw windows.windows` |
| `windows.windowstations` | Menampilkan Windows Window Station objects dan informasi terkait. | `vol -f Memory.raw windows.windowstations` |

## Pola penggunaan yang paling sering dipakai

### 1. Analisis satu PID

```bash
vol -f Memory.raw windows.dlllist --pid 880
```

Pola:

```text
vol -f <memory> <plugin> --pid <PID>
```

Contoh plugin yang umum memakai pendekatan PID:

```text
windows.dlllist
windows.cmdline
windows.envars
windows.handles
windows.malware.malfind
windows.malware.ldrmodules
windows.memmap
windows.privileges
windows.threads
windows.vadinfo
windows.vadwalk
```

> Tidak semua plugin menerima `--pid`. Selalu cek `--help`.

### 2. Filter output dengan grep

```bash
vol -f Memory.raw windows.pslist | grep -i "svchost"
```

Pola:

```text
<command> | grep -i "<kata>"
```

Contoh:

```bash
vol -f Memory.raw windows.netscan | grep -i "ESTABLISHED"
vol -f Memory.raw windows.dlllist --pid 880 | grep -i "msxml"
vol -f Memory.raw windows.filescan | grep -i "str.sys"
```

### 3. Melihat opsi lengkap plugin

```bash
vol -f Memory.raw windows.dlllist --help
```

Ini penting karena **opsi setiap plugin tidak selalu sama**.

### 4. Dump output/file

Untuk plugin yang memang mendukung directory output:

```bash
vol -f Memory.raw windows.dumpfiles -D dumped_files/
```

atau:

```bash
vol -f Memory.raw windows.pedump -D dumped_pe/
```

## Alur belajar DFIR yang praktis

```text
windows.info
      ↓
windows.pslist / windows.pstree
      ↓
windows.psscan
      ↓
windows.cmdline
      ↓
windows.dlllist
      ↓
windows.handles
      ↓
windows.netscan
      ↓
windows.vadinfo
      ↓
windows.memmap
      ↓
windows.malware.malfind
      ↓
windows.malware.ldrmodules
      ↓
windows.dumpfiles / windows.pedump
```

### Contoh hubungan dengan kasus PID 880

```text
pslist
  ↓
PID 880 svchost.exe
  ↓
malfind
  ↓
PAGE_EXECUTE_READWRITE + MZ
  ↓
ldrmodules
  ↓
msxml3r.dll = False / False / False
  ↓
indikasi DLL unlinked/hidden
```

> **Catatan:** daftar di atas mengikuti command yang tampak pada screenshot. Untuk opsi command yang spesifik, terutama plugin malware/YARA/registry yang berubah antarversi Volatility 3, gunakan `--help` pada versi yang sedang dipakai.
