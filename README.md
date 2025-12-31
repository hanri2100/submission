# Linux Foundation Assignment

NAMA: HANRINOV KAEMPE  
NIM: 1003250023  

# Activity
## 1. SYSTEM INFORMATION & HOSTNAME<br>
Command :

```bash
uname -a

sudo hostnamectl set-hostname hanri-lab

hostname
```
Screenshot :

<img src="/screenshots/1-System-Information-uname-a_Hostname-Change.png" width="800">

## 2. DIRECTORY & FILE MANAGEMENT**<br>
### a. Create directory
Command :

```bash
mkdir -p ~/security_lab/scans/results
ls -la
```
Screenshot :

<img src="/screenshots/2-a-ls-la.png" width="500">

### b. Create 3 files
Command :

```bash
touch report.txt targets.txt notes.md

nano report.txt
nano targets.txt
nano notes.md

cat report.txt
cat targets.txt
cat notes.md
```
Screenshot :

<img src="/screenshots/2-b-touch-nano-cat.png" width="500">

### c. Copy, rename, move operations
Command :

```bash
mkdir -p ~/security_lab/archive

cp report.txt report_backup.txt

mv targets.txt lab_target.txt

mv report_backup.txt ~/security_lab/archive/

ls -laR ~/security_lab
```
Screenshot :

<img src="/screenshots/2-c-cp-mv-mv-ls-laR.png" width="500">

### d. File content operations
Command :

```bash
cat report.txt

head lab_target.txt

tail notes.md

wc lab_target.txt
```
Screenshot :

<img src="/screenshots/2-d-cat-head-tail-wc.png" width="500">

### e. Permission management (bonus understanding)
Command :

```bash
chmod 600 report.txt

ls -la report.txt
```
Screenshot :

<img src="/screenshots/2-e-chmod-600.png" width="500">
Apa arti dari 600 yang terdapat perintah chmod tersebut?<br>
  - Digit pertama (6) adalah untuk User/Owner: 4 (Read) + 2 (Write) = 6. Artinya user bisa baca dan tulis.<br>
  - Digit kedua (0) adalah untuk Group: Tidak ada akses.<br>
  - Digit ketiga (0) adalah untuk Others: Tidak ada akses.<br>
Jadi, 600 menjamin privasi total file tersebut hanya untuk pemiliknya.<br>

## 3. TEXT PROCESSING & SEARCHING<br>

### a. GREP practice
Command :

```bash
echo "# Ini adalah file target security scan" >> lab_targets.txt

grep -n "security" lab_targets.txt

grep -i "SECURITY" lab_targets.txt

grep -v "security" lab_targets.txt
```
Screenshot :

<img src="/screenshots/3-a-grep-n-i-v.png" width="500">

### b. CUT & AWK practice
Command :

```bash
nano lab_targets.txt #untuk membuat formatnya menjadi "192.168.22.1:open"

cut -d: -f1 lab_targets.txt

awk -F ":" '{print $1}' lab_targets.txt
```
Screenshot :

<img src="/screenshots/3-b-cut-awk.png" width="500">

### c. SORT & UNIQ
Command :

```bash
cat lab_targets.txt

sort lab_targets.txt | uniq

sort lab_targets.txt | uniq | wc -l
```
Screenshot :

<img src="/screenshots/3-c-sort-uniq-wc-l.png" width="500">

### d. PIPELINE practice
Command :

```bash
cat lab_targets.txt #untuk perbadingan hasil saja dengan command yang di combine

cat lab_targets.txt | grep "open" | sort | uniq
```
Screenshot :

<img src="/screenshots/3-d-combine-cat-grep-sort-uniq.png" width="500">

**Penjelasan kombinasi command `cat lab_targets.txt | grep "open" | sort | uniq`**

| Step | Command | Fungsi & Penjelasan |
| :--- | :--- | :--- |
| **1** | `cat lab_targets.txt` | **Membaca file.** Menampilkan seluruh isi file `lab_targets.txt`. |
| **2** | `\|` (Pipe) | **Penyambung.** Mengalirkan output dari kiri menjadi input ke kanan. |
| **3** | `grep "open"` | **Filter.** Hanya mengambil baris yang mengandung kata "open". |
| **4** | `\|` (Pipe) | Mengalirkan data hasil saringan `grep "open"` ke `sort`. |
| **5** | `sort` | **Pengurutan.** Mengurutkan data (A-Z). *Penting: `uniq` butuh data urut.* |
| **6** | `\|` (Pipe) | Mengalirkan data yang sudah urut oleh `sort` ke `uniq`. |
| **7** | `uniq` | **Hapus Duplikat.** Menghapus baris yang sama persis agar tidak berulang. |
| **End**| **Hasil Akhir** | Daftar target unik yang port-nya terbuka ("open"). |

## 4. PACKAGE INSTALLATION & VERIFICATION<br>

### a. Update system
Command :

```bash
sudo apt update

apt list --upgradable

sudo apt upgrade -y

awk '$1" "$2 >= "2025-12-29 13:40" && $1" "$2 <= "2025-12-29 13:51" && $3=="upgrade"' /var/log/dpkg.log
```
Screenshot before upgrade :

<img src="/screenshots/4-a-before-upgrade.png" width="500">

Terdapat 8 paket yang dapat ada di list upgrade

Screenshot after upgrade:

<img src="/screenshots/4-a-after-upgrade.png" width="800">

Namun setelah command upgrade dieksekusi hanya 7 paket yang diupgrade dan yang paket 1 tidak diupgrade karena masalah dependensi

### b. Install security tools
Command :

```bash
sudo apt install nmap wireshark tcpdump aircrack-ng burpsuite -y

apt list --installed 2>/dev/null | grep -E "\b(nmap|wireshark|tcpdump|aircrack-ng|burpsuite)\b"
```
Screenshot :

<img src="/screenshots/4-b-install-sectools.png" width="800">

### c. Verify each tool
Command :

```bash
nmap --version
tcpdump --version
which aircrack-ng
which burpsuite
wireshark --version
```
Screenshot :

<img src="/screenshots/4-c-verify-sectools.png" width="800">

### d. Create installation_log.txt
Command :

```bash
grep " install " /var/log/dpkg.log* | grep -E " (nmap|wireshark|tcpdump|aircrack-ng|burpsuite):" > installation_log.txt
```

## 5. NETWORK & CONNECTIVITY SETUP<br>

### a. Network information
Command :

```bash
{ ifconfig eth0 | awk '/inet / {print "IP: " $2 "\nNetmask: " $4}'; ip route | awk '/default/ {print "Gateway: " $3}'; } > network_info.txt
```
Screenshot :

<img src="/screenshots/5-a-ifconfig-ip-route.png" width="800">

### b. Port discovery
Command :

```bash
sudo netstat -tuln | grep LISTEN
```
Screenshot :

<img src="/screenshots/5-b-netstat-tuln.png" width="500">
tidak ada port yang sedang LISTEN

### c. SSH setup & connectivity test
Command :

```bash
sudo systemctl enable ssh

sudo systemctl start ssh

sudo systemctl status ssh
```
Screenshot :

<img src="/screenshots/5-c-ssh.png" width="500">


## 6. LINUX CONFIGURATION & SERVICES<br>

### a. systemctl service management
Command :

```bash
systemctl status ssh

systemctl is-enabled ssh

systemctl list-units --type=service
```
Screenshot :

<img src="/screenshots/6-a-systemctl-service-management.png" width="500">

### b. SSH Configuration Understanding
Command :

```bash
cat /etc/ssh/sshd_config
```
Screenshot :

<img src="/screenshots/6-b-ssh-config.png" width="800">

Konfigurasi berikut diterapkan pada file `/etc/ssh/sshd_config` untuk meningkatkan keamanan server:

* **`Port 22`**
    * **Penjelasan:** Port standar (default) untuk layanan SSH.
    * **Rekomendasi:** Sangat disarankan untuk diubah ke port non-standar (misalnya `2022` atau `2200`) guna menghindari *brute-force attack* dan *scanning* otomatis dari bot internet.

* **`PermitRootLogin prohibit-password`**
    * **Penjelasan:** Konfigurasi ini **melarang** user `root` login menggunakan password teks biasa.
    * **Keamanan:** User `root` hanya diizinkan masuk jika menggunakan **SSH Key** (Public/Private Key). Ini mencegah penyerang menebak password administrator.

* **`MaxAuthTries 6`**
    * **Penjelasan:** Batas toleransi kesalahan input kredensial.
    * **Mekanisme:** Jika user gagal login sebanyak 6 kali berturut-turut, server akan memutus koneksi secara paksa. Ini memperlambat upaya pembobolan password.

* **`PubkeyAuthentication yes`**
    * **Penjelasan:** Mengaktifkan metode autentikasi berbasis Kunci Kriptografi (*Public Key Infrastructure*).
    * **Benefit:** Metode ini jauh lebih aman dan kebal terhadap serangan tebak password (*dictionary attack*).

* **`PasswordAuthentication yes`**
    * **Penjelasan:** Mengizinkan metode login konvensional menggunakan password.
    * **Catatan:** Jika semua user sudah memiliki SSH Key, opsi ini sebaiknya diubah menjadi `no` untuk keamanan maksimal.

### c. /etc/hosts file configuration
Command :

```bash
ping -c 4 kali-lab
```
Screenshot :

<img src="/screenshots/6-c-ping-kali-lab.png" width="500">

### d. Network configuration
Command :

```bash
sudo cat /etc/netplan/50-cloud-init.yaml

ip addr show

ip route show

cat /etc/resolv.conf
```
Screenshot :

<img src="/screenshots/6-d1-cat-50-cloud-init-ip-addr.png" width="500">

<img src="/screenshots/6-d2-ip-route-cat-resolv.png" width="500">

### e. Firewall (ufw/firewalld)
Command :

```bash
sudo ufw status

sudo ufw enable

sudo ufw allow 22/tcp

sudo ufw show added
```
Screenshot :

<img src="/screenshots/6-e-activate-firewall-allow-22tcpport.png" width="500">


## KENDALA DAN SOLUSI<br>

### ⚠️ Kendala & Solusi

**Kendala:**
Gagal melakukan koneksi SSH dari Host (Windows) ke Guest OS (Kali Linux) pada VirtualBox. Hal ini terjadi karena secara default VirtualBox menggunakan mode **NAT**, yang bertindak sebagai firewall dan mencegah koneksi masuk secara langsung dari Host ke VM.

**Solusi 1: Port Forwarding (Tetap dalam Mode NAT)**
Solusi ini sangat berguna jika Anda ingin menjaga VM tetap terisolasi namun membuka satu jalur khusus untuk SSH.
* **Langkah:** Buka *Settings VM > Network > Advanced > Port Forwarding*. Tambahkan aturan: `TCP`, Host Port `2222`, Guest Port `22`.
* **Cara Akses:** `ssh user@127.0.0.1 -p 2222`

**Solusi 2: Host-Only Adapter (Jaringan Privat Host-to-VM)**
Solusi terbaik untuk koneksi stabil antara Windows dan Kali Linux tanpa tergantung pada koneksi internet atau router luar.
* **Langkah:**
  1. Buka *File > Tools > Network Manager* di VirtualBox untuk memastikan *Host-only Network* sudah ada.
  2. Di *Settings VM > Network*, ubah "Attached to" menjadi **Host-Only Adapter**.
* **Kelebihan:** Memberikan IP statis/khusus yang hanya bisa diakses oleh komputer Host. Sangat aman dan stabil untuk keperluan lab lokal.

**Solusi 3: Bridged Adapter (Jaringan Terbuka/Publik)**
Solusi ini membuat VM seolah-olah menjadi perangkat fisik terpisah di dalam jaringan WiFi/LAN yang sama.
* **Langkah:** Di *Settings VM > Network*, ubah "Attached to" menjadi **Bridged Adapter**.
* **Cara Akses:** Gunakan IP lokal yang didapatkan VM dari router (misal: `192.168.1.xx`).
* **Catatan:** Bergantung pada ketersediaan DHCP dari router atau hotspot yang Anda gunakan.
