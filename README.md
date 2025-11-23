# Assignment: Vue.js – Simple To-Do List
## Identitas
- Nama : Nurul Qalbi Zahrani
- NIM : F1D022150
---
## Deskripsi Tugas
Pada tugas ini saya membuat aplikasi To-Do List sederhana menggunakan Vue.js.
Aplikasi memiliki fitur:
- Menambah tugas
- Menghapus tugas
- Menampilkan pesan saat daftar kosong
- Menggunakan reaktifitas dengan `ref()`

Selain itu, saya juga menambahkan beberapa fitur tambahan yang saya ambil berdasarkan materi Vue dasar, yaitu:
- Timer untuk fitur pomodoro (untuk materi onMounted dan onUnmounted)
- Fitur Login
- User Profile
- Menambahkan Catatan
---

## Hasil
### 1. Screenshot Hasil Program
#### a. Landing Page
![alt text](results/landingPage.png)

#### b. User Profile
![alt text](results/userprofile.png)

#### c. Fitur Edit Kota
![alt text](results/resultEditCity.png)

#### d. Timer dan To Do List Saat Tidak ada Tugas
![alt text](results/timerdantodolist.png)

#### e. Fitur Tambah Tugas
![alt text](results/addtodolist.png)

#### f. Fitur Hapus Tugas
![alt text](results/deletetugas.png)

#### g. Fitur Tambah Pengingat Hari Deadline
![alt text](results/tambahHari.png)

#### h. Fitur Reset Hari Deadline
![alt text](results/resetHari.png)

#### h. Fitur Kurangi Hari Deadline
![alt text](results/kurangHari.png)

#### h. Fitur Tambahkan Catatan
![alt text](results/tambahCatatan.png)
### 2. Penjelasan Singkat
Jelaskan bagian penting, misalnya:
- cara kerja `addTask()` adalah menggunakan ref() dengan bentuk array tasks. Variabel tasks menyimpan daftar tugas, sementara newTask menampung input dari user. Saat user menambahkan tugas melalui form, fungsi addTask() akan mengecek apakah input tidak kosong, lalu menambahkan objek tugas baru ke dalam tasks.value. Setelah itu input dikosongkan supaya siap untuk tugas berikutnya.

- Kemudian, untuk tampilan list tasksnya, Daftar tugas ditampilkan menggunakan v-for, yang memungkinkan setiap tugas di-loop secara otomatis ke dalam elemen list di halaman. 

- Setiap tugas juga memiliki tombol hapus yang memanggil deleteTask(index); sebelum dihapus, user akan diminta konfirmasi melalui window.confirm. Jika dikonfirmasi, tugas dihapus dari array menggunakan splice(), dan karena tasks reaktif, perubahan langsung terlihat di UI. Untuk menangani kasus daftar kosong, aplikasi menggunakan conditional rendering dengan v-if dan v-else, sehingga jika tidak ada tugas yang tersisa, akan muncul pesan “Tidak ada tugas”.



- cara kerja reactive() User Profile
Reactive ini saya pake untuk fitur profil user, khususnya bagian mengedit kota dari user, karena profil ini terdiri dari beberapa list data, sehingga lebih mudah menggunakan reactive yang cocok untuk data kompleks.

- cara kerja Conditional Rendering 
disini saya memanfaatkan conditional rendering untuk login berupa dia akan menyembunyikan elemen lainnya terlebih dahulu sebelum pengguna login, menggunakan kondisi boolean dengan v-if dan v-else.
- cara kerja Lifecycle Hooks Timer: disini saya gunakan untuk fitur Pomodoro Timer yang akan mulai tepat setelah pengguna menekan Login pada Landing Page. disini saya memanfaatkan materi Lifecycle Hooks yang memungkinkan kita mengeksekusi fungsi pada fase tertentu dalam siklus hidup komponen (dibuat, ditampilkan, diperbarui, dihapus).
 yang dipake utama itu: 
 onMounted -> Setelah komponen di-mount (paling sering digunakan)
onUnmounted -> Setelah komponen dihapus