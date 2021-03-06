# A6:2017 Kesalahan Konfigurasi Keamanan

| Agen ancaman / vektor serangan | Kelemahan Keamanan           | Dampak             |
| -- | -- | -- |
| Akses Lvl : Exploitasi 3 | Prevalensi 3 : Deteksi 3 | Teknik 2 : Bisnis |
| Penyerang akan sering mencoba untuk mengeksploitasi kelemahan yang tidak ditonton atau mengakses akun default, halaman yang tidak digunakan, file dan direktori yang tidak dilindungi, dll untuk mendapatkan akses yang tidak sah atau pengetahuan tentang sistem.|Kesalahan konfigurasi keamanan dapat terjadi di semua tingkat tumpukan aplikasi, termasuk layanan jaringan, platform, server web, server aplikasi, database, kerangka kerja, kode kustom, dan mesin, wadah, atau penyimpanan virtual pra-instal, wadah, atau penyimpanan. Pemindai otomatis berguna untuk mendeteksi kesalahan konfigurasi, penggunaan akun atau konfigurasi default, layanan yang tidak perlu, opsi lawas, dll.|Kelemahan seperti itu sering memberi penyerang akses tidak sah ke beberapa data sistem atau fungsionalitas. Kadang-kadang, kelemahan tersebut menghasilkan kompromi sistem yang lengkap. Dampak bisnis tergantung pada kebutuhan perlindungan aplikasi dan data.|

## Apakah Aplikasi itu Rentan?

Aplikasi mungkin rentan jika aplikasi tersebut adalah:

* Tidak ada pengerasan keamanan yang sesuai di seluruh bagian dari tumpukan aplikasi, atau izin yang tidak dikonfigurasi dengan benar pada layanan cloud.
* Fitur yang tidak perlu diaktifkan atau diinstal (mis. Port, layanan, halaman, akun, atau hak istimewa yang tidak perlu).
* Akun default dan kata sandi mereka masih diaktifkan dan tidak berubah.
* Menangani kesalahan mengungkapkan jejak tumpukan atau pesan kesalahan yang terlalu informatif kepada pengguna.
* Untuk sistem yang ditingkatkan, fitur keamanan terbaru dinonaktifkan atau tidak dikonfigurasi dengan aman.
* Pengaturan keamanan di server aplikasi, kerangka kerja aplikasi (mis. Struts, Spring, ASP.NET),libraries, databases, etc. Tidak disetting secara aman.
* Server tidak mengirim security headers atau arahan keamanan atau tidak diatur untuk mengamankan nilai dari sisi backend.
* Software telah out of date atau diketahui rentan (lihat **A9:2017-Using Components with Known Vulnerabilities**).

Tanpa proses konfigurasi keamanan aplikasi yang diintegrasikan dan dilakukan secara berkala, sistem berisiko lebih tinggi.

## How To Prevent

Secure installation processes should be implemented, including:

* A repeatable hardening process that makes it fast and easy to deploy another environment that is properly locked down. Development, QA, and production environments should all be configured identically, with different credentials used in each environment. This process should be automated to minimize the effort required to setup a new secure environment.
* A minimal platform without any unnecessary features, components, documentation, and samples. Remove or do not install unused features and frameworks.
* A task to review and update the configurations appropriate to all security notes, updates and patches as part of the patch management process (see **A9:2017-Using Components with Known Vulnerabilities**). In particular, review cloud storage permissions (e.g. S3 bucket permissions).
* A segmented application architecture that provides effective, secure separation between components or tenants, with segmentation, containerization, or cloud security groups (ACLs).
* Sending security directives to clients, e.g. [Security Headers](https://www.owasp.org/index.php/OWASP_Secure_Headers_Project).
* An automated process to verify the effectiveness of the configurations and settings in all environments.

## Example Attack Scenarios

**Scenario #1**: The application server comes with sample applications that are not removed from the production server. These sample applications have known security flaws attackers use to compromise the server. If one of these applications is the admin console, and default accounts weren't changed the attacker logs in with default passwords and takes over.

**Scenario #2**: Directory listing is not disabled on the server. An attacker discovers they can simply list directories. The attacker finds and downloads the compiled Java classes, which they decompile and reverse engineer to view the code. The attacker then finds a serious access control flaw in the application.

**Scenario #3**: The application server's configuration allows detailed error messages, e.g. stack traces, to be returned to users. This potentially exposes sensitive information or underlying flaws such as component versions that are known to be vulnerable.

**Scenario #4**: A cloud service provider has default sharing permissions open to the Internet by other CSP users. This allows sensitive data stored within cloud storage to be accessed.

## References

### OWASP

* [OWASP Testing Guide: Configuration Management](https://www.owasp.org/index.php/Testing_for_configuration_management)
* [OWASP Testing Guide: Testing for Error Codes](https://www.owasp.org/index.php/Testing_for_Error_Code_(OWASP-IG-006))
* [OWASP Security Headers Project](https://www.owasp.org/index.php/OWASP_Secure_Headers_Project)

For additional requirements in this area, see the Application Security Verification Standard [V19 Configuration](https://www.owasp.org/index.php/ASVS_V19_Configuration).

### External

* [NIST Guide to General Server Hardening](https://csrc.nist.gov/publications/detail/sp/800-123/final)
* [CWE-2: Environmental Security Flaws](https://cwe.mitre.org/data/definitions/2.html)
* [CWE-16: Configuration](https://cwe.mitre.org/data/definitions/16.html)
* [CWE-388: Error Handling](https://cwe.mitre.org/data/definitions/388.html)
* [CIS Security Configuration Guides/Benchmarks](https://www.cisecurity.org/cis-benchmarks/)
* [Amazon S3 Bucket Discovery and Enumeration](https://blog.websecurify.com/2017/10/aws-s3-bucket-discovery.html)
