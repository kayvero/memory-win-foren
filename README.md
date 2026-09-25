# Volatility 3 Windows Commands --- Cheat Sheet

> Format: **Command \| Deskripsi \| Cara penggunaan**
>
> Basis daftar command: command list yang terlihat pada screenshot
> Volatility 3 yang diberikan.\
> Contoh penggunaan menggunakan pola Volatility 3 CLI yang umum. Jika
> suatu plugin tidak menerima opsi tertentu pada versi Volatility yang
> dipakai, cek `--help`.

## Cara baca sintaks

  -----------------------------------------------------------------------
  Sintaks                             Fungsi
  ----------------------------------- -----------------------------------
  `-f <file>`                         Menentukan memory dump yang
                                      dianalisis

  `--pid <PID>`                       Membatasi analisis ke process ID
                                      tertentu, jika plugin mendukungnya

  `| grep <kata>`                     Menyaring output berdasarkan teks

  `grep -i <kata>`                    `grep` tanpa membedakan huruf
                                      besar/kecil

  `-h` / `--help`                     Melihat opsi yang tersedia untuk
                                      plugin

  `-q`                                Quiet mode pada command
                                      tertentu/versi tertentu; jangan
                                      diasumsikan tersedia pada semua
                                      plugin

  `-r <regex>`                        Regex pada plugin yang mendukung
                                      pencarian/filter regex
  -----------------------------------------------------------------------

## Command dasar

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------
  Command                                   Deskripsi                    Cara penggunaan
  ----------------------------------------- ---------------------------- ------------------------------------------------------------------------------------------
  `windows.bigpools`                        Menampilkan informasi Big    Dasar: `vol -f Memory.raw windows.bigpools``<br>`{=html}Filter output:
                                            Pool/kernel pool yang        `vol -f Memory.raw windows.bigpools \| grep -i "kata"`
                                            ditemukan di memory. Berguna 
                                            untuk investigasi            
                                            objek/alokasi kernel         
                                            tertentu.                    

  `windows.callbacks`                       Menampilkan callback kernel  Dasar: `vol -f Memory.raw windows.callbacks``<br>`{=html}Filter:
                                            yang terdaftar. Berguna      `vol -f Memory.raw windows.callbacks \| grep -i "kata"`
                                            untuk mencari callback yang  
                                            tidak biasa.                 

  `windows.cmdline`                         Menampilkan command line     Dasar: `vol -f Memory.raw windows.cmdline``<br>`{=html}PID:
                                            proses. Berguna untuk        `vol -f Memory.raw windows.cmdline --pid 880``<br>`{=html}Filter:
                                            mengetahui argumen yang      `vol -f Memory.raw windows.cmdline \| grep -i "powershell"`
                                            digunakan saat proses        
                                            dijalankan.                  

  `windows.cmdscan`                         Mencari command yang         Dasar: `vol -f Memory.raw windows.cmdscan``<br>`{=html}Filter:
                                            tersimpan di console command `vol -f Memory.raw windows.cmdscan \| grep -i "cmd"`
                                            history/buffer Windows.      

  `windows.consoles`                        Menampilkan informasi        Dasar: `vol -f Memory.raw windows.consoles``<br>`{=html}Filter:
                                            console Windows dan command  `vol -f Memory.raw windows.consoles \| grep -i "whoami"`
                                            yang berhubungan dengannya.  

  `windows.crashinfo`                       Menampilkan informasi yang   `vol -f Memory.raw windows.crashinfo`
                                            berkaitan dengan crash       
                                            dump/header crash            
                                            information jika tersedia.   

  `windows.debugregisters`                  Menampilkan debug registers  Dasar: `vol -f Memory.raw windows.debugregisters``<br>`{=html}Filter:
                                            proses/thread yang ditemukan `vol -f Memory.raw windows.debugregisters \| grep -i "PID"`
                                            di memory.                   

  `windows.deskscan`                        Melakukan scan terhadap      `vol -f Memory.raw windows.deskscan`
                                            objek desktop Windows.       

  `windows.desktops`                        Menampilkan objek            `vol -f Memory.raw windows.desktops`
                                            desktop/window-station yang  
                                            ditemukan.                   

  `windows.devicetree`                      Menampilkan device tree      `vol -f Memory.raw windows.devicetree`
                                            Windows dan hubungan objek   
                                            device.                      

  `windows.dlllist`                         Menampilkan DLL/module yang  Dasar: `vol -f Memory.raw windows.dlllist``<br>`{=html}PID:
                                            terhubung dengan proses      `vol -f Memory.raw windows.dlllist --pid 880``<br>`{=html}Filter:
                                            melalui struktur loader.     `vol -f Memory.raw windows.dlllist --pid 880 \| grep -i "dll"`

  `windows.driverirp`                       Menampilkan informasi        `vol -f Memory.raw windows.driverirp``<br>`{=html}Filter:
                                            IRP/function table pada      `vol -f Memory.raw windows.driverirp \| grep -i "driver"`
                                            driver. Berguna dalam        
                                            analisis driver/kernel.      

  `windows.driverscan`                      Melakukan scan memory untuk  `vol -f Memory.raw windows.driverscan``<br>`{=html}Filter:
                                            menemukan objek driver.      `vol -f Memory.raw windows.driverscan \| grep -i "sys"`

  `windows.dumpfiles`                       Mengekstrak file/cache       Dasar: `vol -f Memory.raw windows.dumpfiles``<br>`{=html}Output directory:
                                            object yang ditemukan dari   `vol -f Memory.raw windows.dumpfiles -D dumped_files/``<br>`{=html}Filter output:
                                            memory.                      `vol -f Memory.raw windows.dumpfiles \| grep -i ".exe"`

  `windows.envars`                          Menampilkan environment      Dasar: `vol -f Memory.raw windows.envars``<br>`{=html}PID:
                                            variables proses.            `vol -f Memory.raw windows.envars --pid 880``<br>`{=html}Filter:
                                                                         `vol -f Memory.raw windows.envars \| grep -i "PATH"`

  `windows.etwpatch`                        Memeriksa                    `vol -f Memory.raw windows.etwpatch`
                                            informasi/indikator patching 
                                            pada ETW (Event Tracing for  
                                            Windows).                    

  `windows.filescan`                        Melakukan scan memory untuk  `vol -f Memory.raw windows.filescan``<br>`{=html}Filter:
                                            menemukan objek file         `vol -f Memory.raw windows.filescan \| grep -i "str.sys"`
                                            `_FILE_OBJECT`.              

  `windows.getservicesids`                  Menampilkan pemetaan Service `vol -f Memory.raw windows.getservicesids`
                                            SID yang dapat ditemukan     
                                            dari konfigurasi/registry    
                                            terkait service.             

  `windows.getsids`                         Menampilkan SID yang terkait Dasar: `vol -f Memory.raw windows.getsids``<br>`{=html}PID:
                                            dengan proses/token.         `vol -f Memory.raw windows.getsids --pid 880`

  `windows.handles`                         Menampilkan handle yang      Dasar: `vol -f Memory.raw windows.handles``<br>`{=html}PID:
                                            dimiliki proses ke object    `vol -f Memory.raw windows.handles --pid 880``<br>`{=html}Filter teks:
                                            kernel seperti file,         `vol -f Memory.raw windows.handles --pid 880 \| grep -i "str.sys"`
                                            registry, process, thread,   
                                            event, dan lainnya.          

  `windows.iat`                             Menganalisis Import Address  `vol -f Memory.raw windows.iat`
                                            Table (IAT) dari             
                                            executable/module yang       
                                            ditemukan.                   

  `windows.info`                            Menampilkan informasi dasar  `vol -f Memory.raw windows.info`
                                            OS/kernel dari memory dump,  
                                            seperti versi Windows dan    
                                            build.                       

  `windows.joblinks`                        Menampilkan hubungan job     `vol -f Memory.raw windows.joblinks`
                                            object dengan proses yang    
                                            terkait.                     

  `windows.kpcrs`                           Menampilkan Kernel Processor `vol -f Memory.raw windows.kpcrs`
                                            Control Region (KPCR) yang   
                                            ditemukan.                   

  `windows.malware.direct_system_calls`     Mencari indikasi direct      `vol -f Memory.raw windows.malware.direct_system_calls``<br>`{=html}Jika plugin mendukung
                                            system calls pada            PID: `... --pid 880`
                                            proses/module sebagai bagian 
                                            dari analisis malware.       

  `windows.malware.drivermodule`            Menghubungkan/menganalisis   `vol -f Memory.raw windows.malware.drivermodule`
                                            module driver yang ditemukan 
                                            pada memory.                 

  `windows.malware.hollowprocesses`         Mencari indikasi process     `vol -f Memory.raw windows.malware.hollowprocesses`
                                            hollowing.                   

  `windows.malware.indirect_system_calls`   Mencari indikasi indirect    `vol -f Memory.raw windows.malware.indirect_system_calls`
                                            system calls yang dapat      
                                            digunakan malware untuk      
                                            menghindari pola API biasa.  

  `windows.malware.ldrmodules`              Membandingkan daftar module  Dasar: `vol -f Memory.raw windows.malware.ldrmodules``<br>`{=html}PID:
                                            dari beberapa linked list    `vol -f Memory.raw windows.malware.ldrmodules --pid 880``<br>`{=html}Filter:
                                            loader untuk menemukan       `vol -f Memory.raw windows.malware.ldrmodules --pid 880 \| grep -i "False"`
                                            module yang tidak            
                                            terhubung/unlinked. Sangat   
                                            berguna untuk indikasi DLL   
                                            hiding.                      

  `windows.malware.malfind`                 Mencari region memory yang   Dasar: `vol -f Memory.raw windows.malware.malfind``<br>`{=html}PID:
                                            mencurigakan, misalnya       `vol -f Memory.raw windows.malware.malfind --pid 880`
                                            indikasi code injection.     

  `windows.malware.pebmasquerade`           Mencari indikasi             `vol -f Memory.raw windows.malware.pebmasquerade`
                                            manipulasi/masquerading      
                                            terhadap Process Environment 
                                            Block (PEB).                 

  `windows.malware.processghosting`         Mencari indikasi Process     `vol -f Memory.raw windows.malware.processghosting`
                                            Ghosting.                    

  `windows.malware.psxview`                 Membandingkan beberapa       Dasar: `vol -f Memory.raw windows.malware.psxview``<br>`{=html}Filter:
                                            sumber enumerasi proses      `vol -f Memory.raw windows.malware.psxview \| grep -i "False"`
                                            untuk menemukan proses yang  
                                            mungkin disembunyikan.       

  `windows.malware.skeleton_key_check`      Memeriksa indikator teknik   `vol -f Memory.raw windows.malware.skeleton_key_check`
                                            Skeleton Key pada Active     
                                            Directory/domain             
                                            environment.                 

  `windows.malware.suspicious_threads`      Mencari thread yang memiliki `vol -f Memory.raw windows.malware.suspicious_threads``<br>`{=html}Jika mendukung PID:
                                            karakteristik mencurigakan.  `... --pid 880`

  `windows.malware.svcdiff`                 Membandingkan informasi      `vol -f Memory.raw windows.malware.svcdiff`
                                            service untuk menemukan      
                                            perbedaan/anomali.           

  `windows.malware.unhooked_system_calls`   Mencari system call/API yang `vol -f Memory.raw windows.malware.unhooked_system_calls`
                                            tampak tidak ter-hook atau   
                                            memiliki indikasi anomali.   

  `windows.mbrscan`                         Melakukan scan untuk Master  `vol -f Memory.raw windows.mbrscan`
                                            Boot Record (MBR)            
                                            signature/struktur yang      
                                            ditemukan dalam memory.      

  `windows.memmap`                          Menampilkan pemetaan virtual Dasar: `vol -f Memory.raw windows.memmap --pid 880``<br>`{=html}Filter:
                                            address ke memory/physical   `vol -f Memory.raw windows.memmap --pid 880 \| grep -i "980000"`
                                            mapping untuk suatu proses.  
                                            Berguna untuk memahami       
                                            region memory proses.        

  `windows.mftscan.ADS`                     Mencari Alternate Data       `vol -f Memory.raw windows.mftscan.ADS`
                                            Streams (ADS) dari struktur  
                                            NTFS/MFT yang ditemukan.     

  `windows.mftscan.MFTScan`                 Melakukan scan untuk         `vol -f Memory.raw windows.mftscan.MFTScan``<br>`{=html}Filter:
                                            struktur Master File Table   `vol -f Memory.raw windows.mftscan.MFTScan \| grep -i ".exe"`
                                            (MFT) NTFS.                  

  `windows.mftscan.ResidentData`            Mencari data resident yang   `vol -f Memory.raw windows.mftscan.ResidentData`
                                            tersimpan langsung di record 
                                            MFT.                         

  `windows.modscan`                         Melakukan scan memory untuk  `vol -f Memory.raw windows.modscan``<br>`{=html}Filter:
                                            menemukan kernel modules.    `vol -f Memory.raw windows.modscan \| grep -i ".sys"`

  `windows.modules`                         Menampilkan kernel modules   `vol -f Memory.raw windows.modules``<br>`{=html}Filter:
                                            yang terdaftar/ditemukan.    `vol -f Memory.raw windows.modules \| grep -i "driver"`

  `windows.mutantscan`                      Melakukan scan untuk         `vol -f Memory.raw windows.mutantscan``<br>`{=html}Filter:
                                            mutant/mutex objects         `vol -f Memory.raw windows.mutantscan \| grep -i "mutex"`
                                            Windows. Berguna untuk       
                                            menemukan mutex yang mungkin 
                                            berkaitan dengan malware.    

  `windows.netscan`                         Mencari network              Dasar: `vol -f Memory.raw windows.netscan``<br>`{=html}Filter:
                                            connection/socket artifacts  `vol -f Memory.raw windows.netscan \| grep -i "ESTABLISHED"``<br>`{=html}Filter PID:
                                            dari memory.                 `vol -f Memory.raw windows.netscan \| grep "880"`

  `windows.netstat`                         Menampilkan informasi        `vol -f Memory.raw windows.netstat``<br>`{=html}Filter:
                                            network state yang dapat     `vol -f Memory.raw windows.netstat \| grep -i "ESTABLISHED"`
                                            direkonstruksi dari memory.  

  `windows.orphan_kernel_threads`           Mencari kernel thread yang   `vol -f Memory.raw windows.orphan_kernel_threads`
                                            tampak orphan/tidak memiliki 
                                            hubungan normal.             

  `windows.pe_symbols`                      Menampilkan/menganalisis PE  `vol -f Memory.raw windows.pe_symbols`
                                            symbols yang tersedia untuk  
                                            executable/module.           

  `windows.pedump`                          Mengekstrak PE image/module  Dasar: `vol -f Memory.raw windows.pedump``<br>`{=html}Output directory:
                                            dari memory. Berguna untuk   `vol -f Memory.raw windows.pedump -D dumped_pe/`
                                            mengambil executable/DLL     
                                            untuk analisis lanjutan.     

  `windows.poolscanner`                     Melakukan pool scan untuk    `vol -f Memory.raw windows.poolscanner``<br>`{=html}Filter:
                                            menemukan objek kernel       `vol -f Memory.raw windows.poolscanner \| grep -i "Process"`
                                            berdasarkan pool             
                                            tag/signature.               

  `windows.privileges`                      Menampilkan privilege/token  Dasar: `vol -f Memory.raw windows.privileges``<br>`{=html}PID:
                                            privilege yang dimiliki      `vol -f Memory.raw windows.privileges --pid 880`
                                            proses.                      

  `windows.pslist`                          Menampilkan proses yang      Dasar: `vol -f Memory.raw windows.pslist``<br>`{=html}Filter:
                                            terdaftar dalam process list `vol -f Memory.raw windows.pslist \| grep -i "svchost"`
                                            Windows.                     

  `windows.psscan`                          Melakukan scan memory untuk  `vol -f Memory.raw windows.psscan``<br>`{=html}Filter:
                                            menemukan process objects,   `vol -f Memory.raw windows.psscan \| grep -i "rootkit"`
                                            termasuk proses yang mungkin 
                                            sudah keluar/tersembunyi     
                                            dari list normal.            

  `windows.pstree`                          Menampilkan hubungan         Dasar: `vol -f Memory.raw windows.pstree``<br>`{=html}Filter:
                                            parent-child antar proses    `vol -f Memory.raw windows.pstree \| grep -i "cmd"`
                                            dalam bentuk tree.           

  `windows.registry.amcache`                Menganalisis AmCache dari    `vol -f Memory.raw windows.registry.amcache``<br>`{=html}Filter:
                                            registry untuk artefact      `vol -f Memory.raw windows.registry.amcache \| grep -i ".exe"`
                                            aplikasi/executable.         

  `windows.registry.cachedump`              Mengambil cached domain      `vol -f Memory.raw windows.registry.cachedump`
                                            logon information dari       
                                            registry memory artefacts.   

  `windows.registry.certificates`           Menampilkan certificate      `vol -f Memory.raw windows.registry.certificates`
                                            information yang ditemukan   
                                            pada registry.               

  `windows.registry.getcellroutine`         Menampilkan/menelusuri cell  `vol -f Memory.raw windows.registry.getcellroutine`
                                            routine pada registry hive   
                                            structures.                  

  `windows.registry.hashdump`               Mengekstrak password hash    `vol -f Memory.raw windows.registry.hashdump`
                                            dari registry SAM/SYSTEM     
                                            bila artefact yang           
                                            dibutuhkan tersedia.         

  `windows.registry.hivelist`               Menampilkan registry hive    `vol -f Memory.raw windows.registry.hivelist`
                                            yang ditemukan dalam memory. 

  `windows.registry.hivescan`               Melakukan scan memory untuk  `vol -f Memory.raw windows.registry.hivescan`
                                            menemukan registry hive      
                                            structures.                  

  `windows.registry.lsadump`                Mengekstrak informasi LSA    `vol -f Memory.raw windows.registry.lsadump`
                                            secrets dari registry/memory 
                                            artefacts.                   

  `windows.registry.printkey`               Membaca registry key/value   Dasar: `vol -f Memory.raw windows.registry.printkey``<br>`{=html}Untuk key tertentu
                                            tertentu.                    gunakan opsi path/key yang tersedia pada `vol ... windows.registry.printkey --help`

  `windows.registry.scheduled_tasks`        Menganalisis scheduled task  `vol -f Memory.raw windows.registry.scheduled_tasks``<br>`{=html}Filter:
                                            yang tersimpan pada          `vol -f Memory.raw windows.registry.scheduled_tasks \| grep -i "task"`
                                            registry.                    

  `windows.registry.userassist`             Menampilkan UserAssist       Dasar: `vol -f Memory.raw windows.registry.userassist``<br>`{=html}Filter:
                                            artefacts yang dapat         `vol -f Memory.raw windows.registry.userassist \| grep -i "Brave"`
                                            menunjukkan aktivitas        
                                            aplikasi melalui registry.   

  `windows.sessions`                        Menampilkan session Windows  `vol -f Memory.raw windows.sessions`
                                            yang ditemukan.              

  `windows.shimcachemem`                    Menganalisis                 `vol -f Memory.raw windows.shimcachemem``<br>`{=html}Filter:
                                            ShimCache/AppCompatCache     `vol -f Memory.raw windows.shimcachemem \| grep -i ".exe"`
                                            data yang berada di memory.  

  `windows.ssdtscan`                        Melakukan scan terhadap      `vol -f Memory.raw windows.ssdtscan`
                                            System Service Descriptor    
                                            Table (SSDT).                

  `windows.statistics`                      Menampilkan statistik        `vol -f Memory.raw windows.statistics`
                                            tertentu yang dapat          
                                            dikumpulkan dari             
                                            memory/kernel structures.    

  `windows.strings`                         Mencari/memetakan string ke  Dasar: `vol -f Memory.raw windows.strings --strings-file strings.txt` jika opsi tersebut
                                            virtual address/process      tersedia pada versi plugin.`<br>`{=html}Selalu cek: `vol ... windows.strings --help`
                                            context. Berguna untuk       
                                            menemukan URL, path,         
                                            command, atau IOC.           

  `windows.suspended_threads`               Menampilkan thread yang      `vol -f Memory.raw windows.suspended_threads`
                                            berada dalam kondisi         
                                            suspended.                   

  `windows.svclist`                         Menampilkan Windows services `vol -f Memory.raw windows.svclist``<br>`{=html}Filter:
                                            yang ditemukan.              `vol -f Memory.raw windows.svclist \| grep -i "service"`

  `windows.svcscan`                         Melakukan scan memory untuk  `vol -f Memory.raw windows.svcscan``<br>`{=html}Filter:
                                            menemukan Windows services,  `vol -f Memory.raw windows.svcscan \| grep -i "svchost"`
                                            termasuk artefact service    
                                            yang mungkin tidak muncul    
                                            dari enumerasi normal.       

  `windows.symlinkscan`                     Melakukan scan untuk         `vol -f Memory.raw windows.symlinkscan``<br>`{=html}Filter:
                                            symbolic link objects        `vol -f Memory.raw windows.symlinkscan \| grep -i "link"`
                                            Windows.                     

  `windows.thrdscan`                        Melakukan scan memory untuk  `vol -f Memory.raw windows.thrdscan``<br>`{=html}Filter:
                                            menemukan thread objects.    `vol -f Memory.raw windows.thrdscan \| grep "880"`

  `windows.threads`                         Menampilkan thread yang      Dasar: `vol -f Memory.raw windows.threads``<br>`{=html}PID:
                                            terkait dengan proses.       `vol -f Memory.raw windows.threads --pid 880`

  `windows.timers`                          Menampilkan kernel timers    `vol -f Memory.raw windows.timers`
                                            yang ditemukan. Berguna      
                                            untuk investigasi aktivitas  
                                            kernel tertentu.             

  `windows.timedump`                        Menampilkan                  `vol -f Memory.raw windows.timedump`
                                            timestamp/time-related dump  
                                            information jika tersedia    
                                            pada plugin/version yang     
                                            digunakan.                   

  `windows.unloadedmodules`                 Menampilkan module yang      `vol -f Memory.raw windows.unloadedmodules``<br>`{=html}Filter:
                                            sudah di-unload tetapi       `vol -f Memory.raw windows.unloadedmodules \| grep -i ".sys"`
                                            artefact-nya masih dapat     
                                            ditemukan. Berguna untuk     
                                            investigasi module yang      
                                            pernah aktif.                

  `windows.vadinfo`                         Menampilkan Virtual Address  Dasar: `vol -f Memory.raw windows.vadinfo --pid 880``<br>`{=html}Filter:
                                            Descriptor (VAD) dan region  `vol -f Memory.raw windows.vadinfo --pid 880 \| grep -i "PAGE_EXECUTE"`
                                            virtual memory milik proses. 

  `windows.vadregexscan`                    Mencari pola/regex pada VAD  Cek opsi dulu: `vol -f Memory.raw windows.vadregexscan --help``<br>`{=html}Lalu gunakan
                                            memory regions.              opsi regex/pattern yang disediakan versi plugin

  `windows.vadwalk`                         Menelusuri struktur VAD tree `vol -f Memory.raw windows.vadwalk --pid 880`
                                            suatu proses.                

  `windows.vadyarascan`                     Melakukan YARA scan terhadap Dasar:
                                            VAD memory regions.          `vol -f Memory.raw windows.vadyarascan --pid 880 --yara-rules rule.yar``<br>`{=html}Nama
                                                                         opsi dapat berbeda menurut versi; cek `--help`

  `windows.verinfo`                         Menampilkan version          `vol -f Memory.raw windows.verinfo`
                                            information dari PE/module   
                                            yang ditemukan.              

  `windows.virtmap`                         Menampilkan virtual memory   `vol -f Memory.raw windows.virtmap`
                                            mapping yang ditemukan.      

  `windows.windows`                         Menampilkan window           `vol -f Memory.raw windows.windows`
                                            objects/window information   
                                            yang ditemukan pada Windows  
                                            GUI subsystem.               

  `windows.windowstations`                  Menampilkan Windows Window   `vol -f Memory.raw windows.windowstations`
                                            Station objects dan          
                                            informasi terkait.           
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------

## Pola penggunaan yang paling sering dipakai

### 1. Analisis satu PID

``` bash
vol -f Memory.raw windows.dlllist --pid 880
```

Pola:

``` text
vol -f <memory> <plugin> --pid <PID>
```

Contoh plugin yang umum memakai pendekatan PID:

``` text
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

``` bash
vol -f Memory.raw windows.pslist | grep -i "svchost"
```

Pola:

``` text
<command> | grep -i "<kata>"
```

Contoh:

``` bash
vol -f Memory.raw windows.netscan | grep -i "ESTABLISHED"
vol -f Memory.raw windows.dlllist --pid 880 | grep -i "msxml"
vol -f Memory.raw windows.filescan | grep -i "str.sys"
```

### 3. Melihat opsi lengkap plugin

``` bash
vol -f Memory.raw windows.dlllist --help
```

Ini penting karena **opsi setiap plugin tidak selalu sama**.

### 4. Dump output/file

Untuk plugin yang memang mendukung directory output:

``` bash
vol -f Memory.raw windows.dumpfiles -D dumped_files/
```

atau:

``` bash
vol -f Memory.raw windows.pedump -D dumped_pe/
```

## Alur belajar DFIR yang praktis

``` text
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

``` text
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

> **Catatan:** daftar di atas mengikuti command yang tampak pada
> screenshot. Untuk opsi command yang spesifik, terutama plugin
> malware/YARA/registry yang berubah antarversi Volatility 3, gunakan
> `--help` pada versi yang sedang dipakai.
