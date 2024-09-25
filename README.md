## **Nama Repository : TapTapStore**
## **Muhammad Ghathaf Fariz Abiyyu (2306210203)**

## TUGAS 2

### **1) Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step (bukan hanya sekadar mengikuti tutorial).**

**Checkpoint 1 : Membuat sebuah proyek Django baru**

1.  Pertama, saya membuat repository baru di Github bernama TapTapStore dan visibility di-set public.
2.  dilanjut dengan membuat sebuah direktory lokal baru bernama TapTapStore, sesuai nama repository
3.  Dalam direktory baru tersebut, buka command prompt
4.  Buat virtual enviroment dengan menggunakan command :

```bash
python -m venv env
```

5. Aktifkan virtual environement dengan command :

```bash
env\Scripts\activate
```

6.  Virtual environment aktif ditandai (env) di awal baris input terminal
7.  Kemudian saya membuat file dengan nama requirements.txt di dalam direktori yang sama, serra menambahkan beberapa dependencies berikut :

```bash
django
gunicorn
whitenoise
psycopg2-binary
requests
urllib3
```

8. Dilanjut dengan melakukan instalansi dependencies pada requirements.txt dengan command :

```bash
pip install -r requirements.txt
```
9.  Kemudian saya membuat proyek Django baru dengan nama TapTapStore dengan command :

```bash
django-admin startproject TapTapStore .
```
Note : Pastikan . tertulis dalam baris command

10.  Ubah isi variabel ALLOWED_HOSTS di file settings.py dengan menambahkan kode :

```python
...
ALLOWED_HOSTS = ["localhost", "127.0.0.1"]
...
```

11.  Pastikan juga terdapat file manage.py pada direktori yang aktif pada terminal saat ini. Kemudian, saya jalankan server Django dengan command :

```bash
python manage.py runserver
```

12.  Lanjut, buka link http://localhost:8000 pada browser dan saya pastikan muncul gambar roket yang menandakan bahwa Django telah berhasil diinstal.
13.  Lalu server saya hentikan dengan menekan Ctrl+C pada cmd.
14.  Dilanjut dengan me-nonaktifkan virtual environment (env) dengan command :

```bash
deactivate
```

**Checkpoint 2 : Membuat aplikasi dengan nama main pada proyek tersebut**

15. Pertama buat aplikasi baru dengan nama main dengan menjalankan perintah berikut :

```bash
python manage.py startapp main
```

16.  Buka berkas settings.py di dalam direktori proyek TapTapStore.
17.  Tambahkan 'main' ke dalam variabel INSTALLED_APPS seperti contoh berikut :

```python
INSTALLED_APPS = [
    ...,
    'main'
]
```

**Checkpoint 3 : Melakukan routing pada proyek agar dapat menjalankan aplikasi main**

18.  Buka berkas urls.py di dalam direktori proyek TapTapStore
19.  Lakukan perubahan pada isi berkas dengan memasukkan kode :

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('main.urls')),
]
```

**Checkpoint 4 : Membuat model pada aplikasi main dengan nama Product dan memiliki atibut wajib**

20.  Pada direktori main, buka berkas models.py
21.  Isi berkas models.py dengan kode :

```python
from django.db import models

class Product(models.Model):
    name = models.CharField(max_length=255)
    description = models.TextField()
    price = models.IntegerField()
    quantity = models.IntegerField()

    @property
    def is_available(self):
        return self.quantity > 0
```

22.  Lakukan migrasi model dengan menjalankan command :

```bash
python manage.py makemigrations
```

23.  Terapkan migrasi ke dalam basis data lokal dengan menjalankan command :

```bash
python manage.py migrate
```

**Checkpoint 5 : Membuat sebuah fungsi pada views.py untuk dikembalikan ke dalam sebuah template html yang menampilkan nama aplikasi serta nama dan kelas kamu**

24.  Buka berkas views.py yang terletak pada direktori main.
25.  Ganti isi berkas tersebut dengan kode :

```python
from django.shortcuts import render

def show_main(request):
context = {
    'npm' : '2306210203',
    'name': 'Muhammad Ghathaf Fariz Abiyyu',
    'class': 'PBP B'
}

    return render(request, "main.html", context)
```

26.  Buat direktori baru bernama templates di dalam direktori main.
27.  Di dalam direktori templates, buat berkas baru dengan nama main.html, kemudian isi berkas tersebut dengan kode :

```bash
<h1>{{ app }}</h1>

<h5>Name:</h5>
<p>{{ name }}</p>
<p></p>
<h5>Class:</h5>
<p>{{ class }}</p>
<p></p>
```

**Checkpoint 6 : Membuat sebuah routing pada urls.py aplikasi main untuk memetakan fungsi yang telah dibuat pada views.py**

28.  Buat berkas baru bernama urls.py di dalam direktori main.
29.  Kemudian isi berkas tersebut dengan kode :

```python
from django.urls import path
from main.views import show_main

app_name = 'main'

urlpatterns = [
    path('', show_main, name='show_main'),
]
```

**Checkpoint 7: Membuat deployment ke PWS terhadap aplikasi yang sudah dibuat sehingga nantinya dapat diakses oleh teman-teman**

Untuk add, commit dan push ke GITHUB :
30.  Pertama, saya lakukan inisiasi direktori lokal TapTapStore sebagai repositori git dengan menjalankan perintah :

```bash
git init
```

31.  Kemudian, tandai semua file yang berada pada direktori tersebut sebagai file yang akan di-commit dengan command :

```bash
git add .
```

32.  Dilanjut dengan membuat pesan commit yang sesuai dengan perubahan yang dilakukan dengan command :

```bash
git commit -m "<PESAN KAMU>"
```

33.  Kemudian saya memastikan saat ini berada pada branch main dengan menjalankan command :

```bash
git branch -M main
```

34.  Dilanjut dengan menghubungkan repositori lokal dengan repositori di Github dengan command :

```bash
git remote add origin <URL_REPO>
```

Note : ubah <URL_REPO> dengan url github yang baru kamu buat.

35.  Kemudian, push seluruh berkas ke repositori github dengan command :

```bash
git push -u origin main
```

**Untuk proses PWSnya :**

36.  Akses halaman PWS di https://pbp.cs.ui.ac.id/ , lalu buat akun baru atau daftar dengan menggunakan akun SSO.
37.  Setelah membuat akun baru, lakukan login menggunakan akun yang baru saja dibuat.
38.  Buat proyek baru dengan mengklik tombol Create New Project, layar akan berpindah ke halaman untuk membuat proyek baru. Masukkan Project Name dengan "TapTapStore". Setelah itu, tekan tombol Create New Project
39.  Simpan informasi Project Credentials dengan aman dan jangan sampai hilang atau lupa, karena penting dan akan digunakan di langkah selanjutnya.
40.  Perbarui berkas settings.py di proyek Django, tambahkan URL deployment PWS pada variabel ALLOWED_HOSTS dengan kode :

```python
...
ALLOWED_HOSTS = ["localhost", "127.0.0.1", <NAMA DEPAN>-<NAMA TENGAH>-taptapstore.pbp.cs.ui.ac.id]
...
```

Note : ganti <NAMA DEPAN> dan <NAMA TENGAH> sesuai akun SSO kamu. Dalam kasus saya : muhammad-ghathaf-taptapstore.pbp.cs.ui.ac.id .
41.  Saya menjalankan perintah berikut untuk melakukan push repositori lokal ke PWS :

```bash
git remote add pws http://pbp.cs.ui.ac.id/<USERNAME PWS>/taptapstore

git branch -M master

git push pws master
```

42.  Akan diminta username dan password, saya gunakan Project Credentials yang telah  disimpan sebelumnya.
43.  Setelah menjalankan perintah tersebut, saya kembalikan branch ke main dengan command :

```bash
git branch -M main
```

44.  Cek status project di laman pws. Jika status Building maka tunggu beberapa saat hingga status berubah menjadi Running.
45.  Ketika sudah Running, tekan tombol View Project lalu copy linknya.
46.  Kemudian buka pada Google Chrome. Pastikan juga bahwa https:// diganti dengan http:// pada link tersebut.

### **2)  Bagan request client ke web pada Django**

Gambar di atas menjelaskan siklus request-response dalam aplikasi web Django. Berikut penjelasan tentang bagaimana urls.py, views.py, models.py, dan file HTML saling terhubung dalam proses ini:

1.  Client Request : Proses dimulai dari pengguna (misalnya, melalui browser) yang mengirim permintaan ke server.
2.  urls.py : File ini seperti "pemandu lalu lintas" dalam aplikasi Django. Ia yang menentukan URL mana yang harus diambil dan view mana yang bertugas menangani permintaan tersebut. Jadi, ketika ada permintaan masuk, Django akan mencocokkannya dengan daftar URL yang ada di urls.py.
3.  views.py : Setelah urls.py tahu view mana yang perlu menangani permintaan, selanjutnya tugas diambil alih oleh view, yang bisa berupa fungsi atau kelas di views.py. Di sini, view akan memproses data yang diperlukan dan menyiapkan respons untuk dikirim balik ke pengguna. Kadang-kadang, ini melibatkan mengambil data dari database lewat models.py.
4.  models.py : View bisa terhubung ke models.py untuk mengambil data yang diperlukan dari database. Models.py ini mendefinisikan bagaimana struktur data disimpan di database dan mengelola query, seperti menambah atau mengambil data.
5.  Database : Database menyimpan data yang nantinya bisa diambil atau ditambahkan oleh models.py.
6.  models.py ke views.py : Setelah data diambil dari database, models.py akan mengembalikannya ke views.py.
7.  views.py : Setelah view menerima data dari models, ia akan mengolahnya dan menyiapkan konten (biasanya berupa file HTML) untuk dikirim kembali ke pengguna.
8.  HTML Template : File HTML ini diisi dengan data atau konteks yang telah disiapkan oleh view, lalu di-render menjadi HTML lengkap yang siap dikirim.
9.  Client Response : HTML yang sudah di-render tadi kemudian dikirim ke pengguna sebagai respons dari permintaan mereka.

### **3)  Fungsi git dalam pengembangan perangkat lunak**

Git adalah alat yang dipakai developer untuk mengelola versi kode dalam pengembangan software. Dibuat oleh Linus Torvalds tahun 2005, Git membantu menyimpan dan mengatur perubahan kode dengan mudah.
Beberapa fungsi Git dalam pengembangan software adalah :

1.  Kontrol Versi : Git menyimpan berbagai versi proyek, sehingga memudahkan developer untuk kembali ke versi lama jika ada masalah di versi terbaru.
2.  Kolaborasi : Git memungkinkan banyak developer bekerja di proyek yang sama tanpa saling mengganggu, dan bisa menggabungkan pekerjaan mereka secara efisien.
3.  Pelacakan Perubahan : Setiap perubahan pada kode tercatat, termasuk siapa yang mengubahnya, kapan, dan apa yang diubah.
4.  Pengembangan Paralel : Dengan fitur cabang (branches), developer bisa mengembangkan fitur baru tanpa mengganggu kode utama, lalu menggabungkannya setelah selesai.
5.  Pemulihan : Kalau ada kesalahan, developer bisa mengembalikan kode ke versi sebelumnya dengan mudah.
6.  Kemudahan Penggunaan : Meski punya banyak fitur, Git dirancang agar mudah digunakan oleh developer.
7.  Integrasi : Git bisa terhubung dengan berbagai platform lain seperti GitHub, GitLab, dan Bitbucket.
8.  Kinerja Tinggi : Git tetap cepat dan efisien, bahkan untuk proyek besar.

Singkatnya, Git sangat membantu developer dalam mengelola dan mengembangkan software secara efisien, terutama dalam kolaborasi dan kontrol versi.

### **4)  Alasan framework Django dijadikan permulaan pembelajaran pengembangan perangkat lunak**

Menurut saya, Django jadi pilihan utama karena kita sudah belajar Python di semester 1, jadi tidak perlu mulai dari nol lagi. Django punya struktur yang rapi dengan pola "Model-View-Template" (MVT), yang bikin kita lebih mudah memahami cara kerja aplikasi web, seperti interaksi dengan database dan logika aplikasi. Selain itu, Django juga punya library lengkap dan fitur bawaan seperti sistem autentikasi dan formulir, jadi kita nggak perlu menulis semuanya dari awal.

### **5)  Mengapa model pada Django disebut sebagai ORM ?**

Model di Django disebut ORM (Object-Relational Mapping), yang memungkinkan developer berinteraksi dengan database pakai kode Python, bukan SQL langsung.

Kenapa disebut ORM? 

1.  Abstraksi : ORM bikin kita bisa kerja dengan objek Python tanpa pusing sama SQL, jadi lebih fokus ke konsep Python.
2.  Manajemen Data : Dengan ORM, kita bisa buat, baca, update, dan hapus data di database tanpa perlu nulis kueri SQL.
3.  Portabilitas : Kode dengan ORM lebih fleksibel, jadi bisa ganti database dengan sedikit perubahan.
4.  Keamanan : ORM membantu mencegah serangan SQL injection karena kuerinya lebih terstruktur dan aman.
5.  Efisiensi : ORM bikin pengembangan lebih cepat, mengurangi jumlah kode, dan menjaga kode tetap bersih serta mudah dipahami.

## TUGAS 3

### **1)  Jelaskan mengapa kita memerlukan data delivery dalam pengimplementasian sebuah platform ?**

Pengiriman data sangat penting bagi platform karena data adalah inti dari interaksi dan layanan. Beberapa alasan utamanya adalah :

1.  Akses Pengguna : Pengiriman data memastikan pengguna bisa mendapatkan layanan atau informasi dengan cepat dan tanpa jeda.
2.  Keputusan Berbasis Data : Data yang cepat dan akurat membantu platform membuat keputusan real-time yang lebih baik, seperti di media sosial atau e-commerce.
3.  Pengalaman Pengguna : Kecepatan pengiriman data mempengaruhi pengalaman pengguna, seperti di platform streaming, di mana keterlambatan akan menyebabkan buffering.
4.  Konektivitas Antar Komponen : Pada platform terdistribusi, komponen-komponen saling bergantung pada pengiriman data yang andal untuk menjaga kelancaran operasional.
5.  Keamanan : Pengiriman data yang aman dengan enkripsi menjaga kerahasiaan dan memastikan kepatuhan terhadap aturan seperti GDPR.

### **2)  Menurutmu, mana yang lebih baik antara XML dan JSON? Mengapa JSON lebih populer dibandingkan XML ?**

Saya menganggap JSON lebih baik dari XML untuk pengembangan web dan pertukaran data antara klien dan server. Berikut beberapa keunggulannya:

1.  Mudah Dibaca : JSON menggunakan format pasangan kunci-nilai yang mirip objek JavaScript, jadi lebih gampang dipahami.
2.  Ukuran Lebih Kecil : Tanpa tag pembuka dan penutup seperti XML, JSON lebih ringan dan efisien untuk dikirim.
3.  Terintegrasi dengan JavaScript : Karena JSON adalah bagian dari JavaScript, mudah digunakan di browser tanpa perlu parsing manual.
4.  Parsing Lebih Cepat : Banyak bahasa pemrograman punya library bawaan untuk parsing JSON, sedangkan parsing XML lebih kompleks dan bisa memperlambat.
5.  Struktur Sederhana : Format JSON lebih simpel dibanding XML yang bergantung pada hierarki tag, jadi lebih mudah diolah.

### **3)  Jelaskan fungsi dari method 'is_valid()' pada form Django dan mengapa kita membutuhkan method tersebut ?**

Metode `is_valid()` pada form Django dipakai untuk memastikan data yang dimasukkan sudah sesuai dengan validasi yang ditentukan. Perannya penting karena :

1.  Cek Validitas Input : `is_valid()` memeriksa apakah semua input sesuai dengan aturan (misalnya email valid, angka dalam rentang tertentu). Jika lolos, akan mengembalikan nilai `True` yang berarti data valid.
2.  Menangani Data Valid : Jika valid, data bersih disimpan di `cleaned_data`, siap untuk digunakan lebih lanjut, seperti menyimpan ke database.
3.  Menangani Kesalahan : Jika ada kesalahan, `is_valid()` mengembalikan `False`, dan kesalahan bisa dilihat melalui atribut error, sehingga pengguna bisa tahu apa yang perlu diperbaiki.

Singkatnya, `is_valid()` penting untuk memastikan data form aman dan sesuai, serta memberikan feedback jika ada kesalahan.

### **4)  Mengapa kita membutuhkan csrf_token saat membuat form di Django? Apa yang dapat terjadi jika kita tidak menambahkan csrf_token pada form Django? Bagaimana hal tersebut dapat dimanfaatkan oleh penyerang ?**

Untuk melindungi aplikasi dari serangan Cross-Site Request Forgery (CSRF), form Django butuh `csrf_token`. CSRF adalah serangan di mana penyerang mencoba membuat pengguna mengirimkan permintaan tanpa izin ke server.

Kenapa `csrf_token` dibutuhkan ?  
Setiap sesi pengguna mendapat token unik yang disisipkan di form. Saat form dikirim, server mengecek token ini untuk memastikan permintaan berasal dari sumber yang sah.

Apa yang terjadi tanpa `csrf_token` ?
Tanpa token ini, aplikasi nggak bisa bedakan permintaan asli dari yang dibuat oleh pihak ketiga, sehingga bisa saja terjadi perubahan data atau transaksi tanpa izin.

Bagaimana serangan ini bisa terjadi ?  
Browser otomatis mengirim cookie otentikasi, jadi penyerang bisa memanfaatkan link atau kode berbahaya untuk membuat korban tanpa sadar mengirim permintaan yang nggak diinginkan, seperti transfer uang ilegal atau mengubah profil.

Jadi, `csrf_token` sangat penting untuk melindungi form dari serangan CSRF dan menjaga keamanan aplikasi Django.

### **5)  Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step (bukan hanya sekadar mengikuti tutorial).**

**Checkpoint 1 : Membuat input form untuk menambahkan objek model pada app sebelumnya**

Menambah line "from main.models import Product" Jadi, keseluruhan program forms.py sebagai berikut :

```python
from django.forms import ModelForm
from main.models import Product

class ProductForm(ModelForm):
    class Meta:
        model = Product
        fields = ["name", "price", "description", "quantity"]
```
**Checkpoint 2 : Tambahkan 4 fungsi views baru untuk melihat objek yang sudah ditambahkan dalam format XML, JSON, XML by ID, dan JSON by ID.**

Menambahkan 4 fungsi pada views.py sebagai berikut :

```python
def show_xml(request):
data = Product.objects.all()
return HttpResponse(serializers.serialize("xml", data), content_type= "application/xml" )

def show_json(request):
    data = Product.objects.all()
    return HttpResponse(serializers.serialize("json", data), content_type= "application/json")

def show_xml_by_id(request, id):
    data = Product.objects.filter(pk=id)
    return HttpResponse(serializers.serialize("xml", data), content_type="application/xml")

def show_json_by_id(request, id):
    data = Product.objects.filter(pk=id)
    return HttpResponse(serializers.serialize("json", data), content_type="application/json")
```

**Checkpoint 3 : Membuat routing URL untuk masing-masing views yang telah ditambahkan pada poin 2.**

Menambah urlpatterns pada urls.py sebagai berikut:

```python
path('json/', show_json, name = "show_json"),
path('xml/', show_xml, name = "show_xml"),
path('json/<int:id>/', show_json_by_id, name = "show_json_by_id"),
path('xml/<int:id>/', show_xml_by_id, name = "show_xml_by_id"),
```

## TUGAS 4

### **1)  Perbedaan antara HttpResponseRedirect() dan redirect()**

HttpResponseRedirect() dan redirect() di Django sama-sama mengarahkan pengguna ke URL lain, tapi ada beberapa perbedaannya:

HttpResponseRedirect():
Ini adalah kelas respons HTTP yang mengirimkan pengalihan (status code 302) ke URL tertentu. Kita harus memberikan URL string sebagai argumen, baik absolut maupun relatif.

from django.http import HttpResponseRedirect
return HttpResponseRedirect('/some-url/')

redirect():
Ini adalah shortcut yang lebih fleksibel karena bisa menerima URL string, model, atau nama pola URL. Django akan mengonversinya ke URL yang tepat.

from django.shortcuts import redirect
return redirect('/some-url/')

Kesimpulannya, HttpResponseRedirect() hanya menerima URL string, sedangkan redirect() lebih fleksibel dan bisa menerima pola URL, model, atau URL string.

### **2)  Cara kerja penghubungan model 'Product' dan 'User'**

Berikut cara menghubungkan model 'Product' dengan 'User':

1.  Impor Model User :  

Di `models.py`, kita impor model `User` dari Django :

```python
from django.contrib.auth.models import User
```

2.  Tambahkan Relasi di Model Product :  

Setiap produk dikaitkan dengan pengguna menggunakan `ForeignKey`:

```python
class Product(models.Model):
   user = models.ForeignKey(User, on_delete=models.CASCADE)
```

- Jika pengguna dihapus, produk terkait juga ikut terhapus.

3.  Menghubungkan User Saat Menyimpan Produk :  

Di `views.py`, saat membuat produk baru, kita hubungkan produk dengan user yang sedang login:

```python
def create_product(request):
form = ProductForm(request.POST or None)

if form.is_valid() and request.method == "POST":
    product = form.save(commit=False)
    product.user = request.user  # Menghubungkan produk dengan user yang login
    product.save()
    return redirect('main:show_main')

context = {'form': form}
return render(request, "create_product.html", context)
   ```

4.  Menampilkan Produk Berdasarkan User :  

Untuk menampilkan produk yang hanya dimiliki pengguna yang login, kita gunakan filter:

```python
   def show_main(request):
    # Program lain ...
    product_entries = Product.objects.filter(user = request.user)
    context = {
        'name': request.user.username,
        'product_entries': product_entries,
        # Program lain ...
    }
       }
```

5.  Migrasi Perubahan :  

Setelah mengubah model, jalankan :
   ```bash
python manage.py makemigrations
python manage.py migrate
   ```

6.  Pengaturan Debug untuk Production : 

Tambahkan pengaturan berikut di `settings.py` untuk mode produksi :

```python
import os
PRODUCTION = os.getenv("PRODUCTION", False)
DEBUG = not PRODUCTION
```

Dengan langkah-langkah ini, produk dapat terhubung dengan user dan hanya ditampilkan sesuai dengan pengguna yang sedang login.

### **3)  Perbedaan antara authentication dan authorization, serta penjelasan mengenai pengimplementasian pada django**

Perbedaan utama antara autentikasi dan otorisasi adalah:

Autentikasi: Memastikan pengguna adalah benar-benar yang mereka klaim (verifikasi identitas).
Otorisasi: Menentukan apa yang boleh dilakukan pengguna setelah mereka berhasil login (hak akses).

Apa yang terjadi setelah login?

Autentikasi: Sistem memverifikasi username dan password. Jika cocok, pengguna dianggap terautentikasi, dan sesi login dibuat.
Otorisasi: Setelah login, sistem menentukan hak akses pengguna. Contohnya, pengguna biasa mungkin hanya bisa mengedit profil, sedangkan admin bisa mengelola pengguna lain dan pengaturan penting.

Implementasi di Django:

1.  Autentikasi: Django menggunakan middleware sesi untuk autentikasi. Saat pengguna login lewat form bawaan Django, kredensial diperiksa dengan authenticate() dan sesi login dibuat dengan login() jika cocok. Contoh :

```python
from django.contrib.auth import authenticate, login

def user_login(request):
    username = request.POST['username']
    password = request.POST['password']
    user = authenticate(request, username=username, password=password)
    if user is not None:
        login(request, user)
        # Pengguna berhasil login
    else:
        # Kredensial tidak valid
```

2.  Otorisasi: Django memiliki sistem permissions dan groups bawaan untuk mengelola hak akses. Setiap model bisa diatur hak aksesnya (seperti tambah, edit, hapus, lihat). Django juga mendukung peran pengguna melalui groups, di mana pengguna dalam grup tertentu memiliki hak akses tertentu. Contoh :

```python
from django.contrib.auth.decorators import login_required, permission_required

@login_required
@permission_required('app_name.add_model_name', raise_exception=True)
def add_object(request):
    # Hanya pengguna yang terautentikasi dan memiliki izin untuk menambah objek yang dapat mengakses fungsi ini
```

@login_required: Membatasi akses hanya untuk pengguna yang login.
@permission_required: Membatasi akses berdasarkan izin tertentu, misalnya izin untuk menambah objek.

### **4)  Bagaimana Django mengingat pengguna yang telah login? Jelaskan kegunaan lain dari cookies dan apakah semua cookies aman digunakan ?**

Django mengingat pengguna yang login menggunakan **session management** dan **cookies**.

a.  **Sesi Django** : 
Saat pengguna login, Django membuat sesi untuk melacak info pengguna di setiap permintaan HTTP. ID sesi ini disimpan di browser sebagai cookie.

b.  **Cookies** :
Django menyimpan ID sesi pengguna dalam cookie bernama `sessionid`, yang dikirimkan kembali ke server setiap kali pengguna mengakses halaman lain. ID ini membantu Django mengenali pengguna yang sedang login.

**Kegunaan lain dari cookies** :
1.  **Menyimpan preferensi** : Misalnya, pilihan bahasa atau tema situs.
2.  **Mempermudah pengguna** : Pengguna tidak perlu login berulang kali jika cookie masih aktif.
3.  **Pelacakan** : Pengiklan menggunakan cookies untuk melacak aktivitas pengguna di beberapa situs.
4.  **Token autentikasi** : Cookies bisa menyimpan token seperti JWT untuk verifikasi identitas.

**Apakah semua cookies aman?**:
1.  **Cookie aman (Secure)** : Hanya dikirim lewat HTTPS, mencegah bocor di koneksi tidak aman.
2.  **Cookie HttpOnly** : Tidak bisa diakses oleh JavaScript, mencegah pencurian lewat serangan XSS.
3.  **Cookie SameSite** : Melindungi dari serangan CSRF dengan mengatur kapan cookie boleh dikirim.
4.  **Expiration** : Cookies harus punya waktu kadaluarsa untuk menghindari penyalahgunaan.
5.  **Third-party cookies** : Cookies dari pengiklan sering melacak pengguna tanpa izin, yang bisa mengancam privasi.
    
