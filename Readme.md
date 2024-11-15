# **Linking and Navigating Next.js**

## **Apa Itu Navigation**

Dalam pengembangan aplikasi web, navigasi antar halaman adalah salah satu fitur utama. Next.js memudahkan navigasi dengan komponen `Link` yang dioptimalkan untuk performa. Mari kita bahas cara menggunakan komponen `Link`, pengaturan rute, serta teknik navigasi lanjutan.

- [`<Link>` Components](https://www.notion.so/Linking-and-Navigating-Next-js-13ea257572738034bc48c4d80a561024?pvs=21)
- `useRouter` [hook (ClienComponents)](https://www.notion.so/Linking-and-Navigating-Next-js-13ea257572738034bc48c4d80a561024?pvs=21)
- [`redirect` Function (Server Components)](https://www.notion.so/Linking-and-Navigating-Next-js-13ea257572738034bc48c4d80a561024?pvs=21)
- [Bagaimana Routing dan Navigasi Bekerja di Next.js](https://www.notion.so/Linking-and-Navigating-Next-js-13ea257572738034bc48c4d80a561024?pvs=21)

## Ada berberapa cara untuk melakukan navigasi antar Route di NextJS :

1. `<Link>` Components
    
    ### Apa itu `<Link>`?
    
    Dalam aplikasi web, kita sering kali perlu pindah dari satu halaman ke halaman lain. Biasanya, di HTML kita pakai tag `<a href="/halaman-lain">Klik di sini</a>` untuk membuat link. Tapi di Next.js, kita punya komponen `<Link>` khusus yang dirancang untuk melakukan navigasi secara mulus dan cepat tanpa reload halaman penuh. Komponen Ini merupakan bawaan yang memperluas tag HTML `<a>` untuk menyediakan prefetching dan navigasi client-side antar route.
    
    ### Cara Kerja `<Link>`
    
    Pada dasarnya, `<Link>` bekerja mirip dengan tag HTML `<a>`, tapi di Next.js, dia melakukan beberapa hal tambahan untuk meningkatkan performa aplikasi, yaitu:
    
    1. **Client-Side Routing**:
        - Ketika kita klik `<Link>`, Next.js menggunakan sistem "client-side routing." Ini artinya halaman tidak akan reload penuh. Sebagai gantinya, Next.js akan memuat konten halaman baru langsung di dalam browser, jadi pergantian halaman terasa lebih cepat.
        - Dengan cara ini, `<Link>` membantu membuat aplikasi terasa seperti aplikasi single-page application (SPA), di mana pengguna tetap berada di halaman yang sama tanpa mengalami "flash" atau delay karena reload.
    2. **Prefetching Otomatis**:
        - Next.js otomatis melakukan prefetching untuk halaman tujuan `<Link>` saat halaman utama selesai dimuat. Prefetching ini berarti halaman yang ditautkan diambil lebih awal di background, jadi saat pengguna benar-benar mengklik link tersebut, halaman tujuan sudah siap ditampilkan dengan cepat.
        - Prefetching dilakukan hanya ketika `<Link>` terlihat di viewport (area tampilan browser). Jadi, kalau halaman tujuan link belum terlihat oleh pengguna, Next.js tidak akan memulai prefetching sampai pengguna scroll ke arah link tersebut.
    3. **Mendukung Navigasi Dinamis**:
        - `<Link>` juga mendukung path dinamis. Misalnya, jika kamu memiliki URL `yang` bervariasi (seperti `/product/[id]`), kamu bisa gunakan `href` dinamis dalam `<Link>`, contohnya:
        
        ```jsx
        <Link href={`/product/${product.id}`}>Lihat Produk</Link>
        ```
        
    
    ### Cara Pakai `<Link>`
    
    Menggunakan `<Link>` di Next.js sangat mudah. Kamu hanya perlu mengimpor komponen ini dari `next/link`, dan memberi `href` (alamat tujuan) seperti ini:
    
    ```jsx
    import Link from 'next/link'
     
    export default function Page() {
      return <Link href="/dashboard">Dashboard</Link>
    }
    ```
    
    ### Kapan `<Link>` Cocok Digunakan?
    
    `<Link>` paling cocok buat navigasi antar halaman dalam aplikasi Next.js yang tidak memerlukan aksi khusus. Misalnya, kalau kamu ingin membuat link sederhana untuk berpindah ke halaman lain, `<Link>` adalah pilihan yang tepat
    
2. `useRouter` hook (ClienComponents)
    
    ### Apa itu `useRouter`?
    
    `useRouter` adalah hook bawaan dari Next.js yang super berguna untuk menangani navigasi di dalam aplikasi, terutama ketika kita ingin pindah halaman karena suatu aksi atau kondisi (misalnya setelah submit form, klik tombol, atau selesai mengisi data).
    
    Bayangkan `useRouter` ini sebagai navigator pribadi yang tahu arah dan bisa mengantar kita ke mana saja di aplikasi Next.js, tanpa harus reload halaman. Dengan ini, kita bisa bikin pengalaman pengguna jadi lebih lancar dan cepat.
    
    ### Cara Kerja `useRouter`
    
    Saat kita pakai `useRouter`, kita mendapatkan akses ke “router” dari Next.js, yang berisi banyak info tentang halaman yang sedang dilihat dan juga beberapa metode buat navigasi. Beberapa hal yang bisa kita lakukan dengan `useRouter`:
    
    - **Ambil informasi halaman** seperti pathname (URL) yang sedang diakses.
    - **Pindah halaman secara programatis** tanpa refresh halaman.
    
    ### Kapan `useRouter` Cocok Digunakan?
    
    `useRouter` ideal banget buat navigasi berbasis aksi. Misalnya, kalau kamu mau arahkan pengguna ke halaman lain setelah mereka mengklik tombol atau menyelesaikan proses, `useRouter` adalah teman yang tepat!
    
    ### Cara Pakai `useRouter`
    
    1. **Import** `useRouter` dari `next/router`.
    2. **Panggil** `useRouter` di dalam komponen untuk dapatkan akses ke router-nya.
    3. **Gunakan** metode seperti `push` atau `replace` buat navigasi ke halaman lain.
    
    Mari kita lihat contoh penggunaannya.
    
    ### Contoh Sederhana dengan `push`
    
    Misalkan kamu punya halaman Dashboard, dan di situ ada tombol “Lihat Profil.” Saat tombol diklik, kita ingin pengguna diarahkan ke halaman profil.
    
    ```jsx
    import { useRouter } from 'next/router';
    
    export default function Dashboard() {
      // Dapatkan router dari useRouter
      const router = useRouter();
    
      // Fungsi buat navigasi ke halaman profil
      const goToProfile = () => {
        router.push('/profile'); // Mengarahkan ke halaman /profile
      };
    
      return (
        <div>
          <h1>Dashboard</h1>
          <button onClick={goToProfile}>Lihat Profil</button>
        </div>
      );
    }
    
    ```
    
    Nah, dalam contoh di atas, saat `goToProfile` dipanggil (ketika tombol diklik), pengguna langsung diarahkan ke halaman `/profile` tanpa refresh halaman. Mantap, kan?
    
    ### Beberapa Metode Penting di `useRouter`
    
    Selain `push`, ada metode lain yang bisa kita manfaatkan:
    
    | Fungsi | Deskripsi | Penggunaan |
    | --- | --- | --- |
    | `router.push()` | Navigasi ke rute tertentu dengan menambahkan ke riwayat browser. | Navigasi umum saat pengguna bisa kembali ke halaman sebelumnya. |
    | `router.replace()` | Navigasi ke rute tanpa menambah ke riwayat browser. | Navigasi yang tidak membutuhkan pengguna kembali ke halaman sebelumnya, seperti setelah login. |
    | `router.refresh()` | Menyegarkan halaman dengan permintaan baru ke server dan re-render Server Components. | Menyegarkan data pada halaman tanpa reload penuh. |
    | `router.prefetch()` | Prefetch rute tertentu untuk mempercepat transisi halaman. | Prefetch halaman yang kemungkinan akan dikunjungi pengguna berikutnya, meningkatkan performa. |
    | `router.back()` | Kembali ke halaman sebelumnya di riwayat browser. | Membuat tombol “Kembali” untuk pengguna. |
    | `router.forward()` | Maju ke halaman berikutnya di riwayat browser. | Membuat tombol “Maju” jika pengguna perlu maju di riwayat browser. |
    
3. `redirect` Function (Server Components)

    
    ### Apa itu `redirect`?
    
    `redirect` adalah fungsi yang digunakan untuk mengarahkan pengguna ke halaman lain pada sisi server. Hal ini sangat berguna untuk melakukan pengalihan berdasarkan logika tertentu sebelum halaman dikirimkan ke klien.
    
    ## `redirect` di Next.js: Memahami Cara Kerjanya
    
    Fungsi `redirect` di Next.js memungkinkan Kamu untuk mengarahkan pengguna ke URL lain secara langsung. Fungsi ini dapat digunakan di dalam:
    
    1. **Server Components**
    2. **Route Handlers**
    3. **Server Actions**
    
    Redirect ini sangat berguna dalam berbagai situasi seperti kontrol akses, pengalihan setelah aksi tertentu, atau mengelola jalur alur pengguna berdasarkan kondisi server.
    
    ### Bagaimana `redirect` Bekerja di Berbagai Konteks?
    
    1. **Di Server Components**: `redirect` bekerja dengan menghentikan proses render halaman saat ini dan langsung mengarahkan pengguna ke halaman lain.
    2. **Di Route Handlers**: Jika digunakan di sini, `redirect` mengeluarkan respons HTTP 307 untuk pengalihan sementara (atau HTTP 308 jika menggunakan `permanentRedirect`).
    3. **Di Server Actions**: Ketika dipanggil di konteks aksi server, `redirect` akan mengeluarkan respons HTTP 303.
    
    Jika halaman yang diminta pengguna tidak ada, Anda bisa menggunakan fungsi `notFound` sebagai alternatif yang lebih sesuai untuk menampilkan halaman 404.
    
    ### Contoh Penggunaan `redirect`
    
    ### Mengarahkan Pengguna dari Server Component
    
    Ketika `redirect` digunakan di dalam Server Component, ia mengeluarkan error bertipe `NEXT_REDIRECT`, menghentikan rendering halaman, dan langsung mengarahkan pengguna ke halaman tujuan.
    
    Misalnya, kita punya halaman profil tim, tapi jika tim dengan ID tertentu tidak ditemukan, kita ingin mengarahkan pengguna ke halaman login.
    
    ```jsx
    import { redirect } from 'next/navigation';
     
    async function fetchTeam(id) {
      const res = await fetch(`https://api.example.com/team/${id}`);
      if (!res.ok) return undefined;
      return res.json();
    }
     
    export default async function Profile({ params }) {
      const team = await fetchTeam(params.id);
      
      if (!team) {
        redirect('/login'); // Mengarahkan pengguna ke halaman login jika tim tidak ditemukan
      }
     
      return (
        <div>
          <h1>Profil Tim</h1>
          {/* Detail tim akan ditampilkan di sini jika data tim tersedia */}
        </div>
      );
    }
    
    ```
    
    **Catatan Penting**:
    
    - `redirect` tidak memerlukan `return redirect()` karena menggunakan tipe `never` yang otomatis menghentikan fungsi tanpa perlu nilai balik.
    
    ### Parameter yang Digunakan dalam `redirect`
    
    Fungsi `redirect` menerima dua parameter:
    
    1. **`path` (string)**: URL tujuan redirect. Bisa berupa path relatif atau path absolut.
    2. **`type` (opsional)**: Tipe pengalihan. Terdapat dua opsi:
        - `'replace'`: Mengganti URL saat ini di history tanpa menambah entry baru. Ini adalah nilai default di luar Server Actions.
        - `'push'`: Menambah URL ke history, seperti halnya navigasi biasa. Ini adalah default di Server Actions.
    
    **Catatan**:
    
    - Parameter `type` tidak memiliki efek saat `redirect` digunakan di dalam Server Components.
    

## Bagaimana Routing dan Navigasi Bekerja di Next.js

Next.js menggunakan pendekatan hybrid untuk routing dan navigasi. Artinya, di server, kode aplikasi secara otomatis dibagi menjadi bagian-bagian kecil berdasarkan rute. Di sisi klien, Next.js melakukan prefetching dan caching untuk segmen-segmen rute tersebut. Ini memungkinkan pengalaman navigasi yang lebih cepat tanpa memuat ulang halaman, hanya segmen-segmen yang berubah yang dirender ulang. Berikut adalah cara kerja routing dan navigasi di Next.js yang bisa membuat aplikasi Anda lebih cepat dan efisien.

### 1. **Code Splitting (Pembagian Kode)**

Code splitting adalah teknik untuk membagi aplikasi menjadi beberapa bagian yang lebih kecil, sehingga hanya bagian yang dibutuhkan yang dimuat saat pengguna mengunjungi halaman tertentu. Ini mengurangi waktu muat dan ukuran data yang perlu ditransfer.

Di Next.js, setiap rute atau segmen rute secara otomatis dipecah menjadi bagian-bagian kecil menggunakan **Server Components**. Artinya, hanya kode untuk rute yang sedang aktif yang dimuat, bukan seluruh aplikasi. Ini mengurangi penggunaan bandwidth dan meningkatkan kinerja.

### 2. **Prefetching (Pemuatan di Latar Belakang)**

Prefetching adalah teknik untuk memuat data untuk rute tertentu di latar belakang sebelum pengguna mengaksesnya. Dengan prefetching, navigasi antar halaman menjadi lebih cepat karena data sudah dimuat sebelumnya.

Ada dua cara utama prefetching bekerja di Next.js:

- **Menggunakan komponen `<Link>`**: Ketika link terlihat oleh pengguna di halaman (misalnya, melalui scrolling), Next.js akan otomatis memuat data untuk halaman tersebut di latar belakang.
- **Menggunakan `router.prefetch()`**: Anda bisa memuat data untuk rute tertentu secara manual menggunakan `useRouter` hook.

Pada mode pengembangan, prefetching tidak aktif, tetapi di **produksi**, ini aktif dan dapat membantu mempercepat waktu muat halaman.

**Contoh penggunaan prefetching dengan `<Link>`:**

```jsx
import Link from 'next/link';

function HomePage() {
  return (
    <div>
      <h1>Selamat datang di halaman utama!</h1>
      <Link href="/about">Ke halaman tentang</Link>
    </div>
  );
}

```

Ketika pengguna scroll dan melihat link ke halaman `/about`, Next.js akan memuat halaman tersebut di latar belakang.

### 3. **Caching (Penyimpanan Cache)**

Next.js menggunakan **Router Cache** di sisi klien untuk menyimpan data yang telah dimuat atau diprefetch sebelumnya. Artinya, jika pengguna sudah mengunjungi rute tertentu, Next.js tidak perlu mengambil data lagi dari server. Data yang telah ada di cache akan digunakan kembali, yang mengurangi waktu muat dan permintaan ke server.

### 4. **Partial Rendering (Render Sebagian)**

**Partial rendering** berarti hanya bagian dari halaman yang berubah yang akan dirender ulang, bukan seluruh halaman. Jika Anda berpindah antara dua rute, misalnya dari `/dashboard/settings` ke `/dashboard/analytics`, hanya bagian yang berubah (misalnya pengaturan atau analitik) yang dirender ulang, sementara elemen lain seperti sidebar atau navbar tetap ada. Ini menghemat waktu rendering dan data yang perlu ditransfer.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/f44d4c92-4dfe-4def-a9d4-a1c00e79ee2a/1e5d893d-0c1e-425a-9d9d-c4398e421e80/image.png)

Tanpa partial rendering, setiap navigasi akan menyebabkan seluruh halaman dirender ulang, yang dapat mengurangi kinerja.

### 5. **Soft Navigation (Navigasi Halus)**

Pada umumnya, saat berpindah halaman, browser melakukan **hard navigation**, di mana seluruh halaman dimuat ulang. Di Next.js, **soft navigation** memastikan hanya segmen yang berubah yang dirender ulang. Ini menjaga agar state klien, seperti scroll position, tidak hilang saat berpindah antar halaman.

Misalnya, jika pengguna sedang mengisi formulir di halaman tertentu, soft navigation memastikan data formulir tetap ada meskipun pengguna berpindah ke halaman lain di dalam aplikasi.

### 6. Back and Forward Navigation (**Navigasi Mundur dan Maju)**

Saat pengguna menavigasi mundur atau maju antar halaman, Next.js akan mempertahankan **posisi scroll** mereka dan menghindari memuat ulang data yang sudah ada di cache. Ini menciptakan pengalaman pengguna yang lebih mulus dan mengurangi waktu muat.

### 7. **Routing antara `/pages/` dan `/app/`**

Jika Anda berencana untuk berpindah secara bertahap dari folder `pages/` ke folder `app/` di Next.js, framework ini akan menangani transisi antar keduanya dengan **hard navigation**. Namun, jika Anda ingin mengelola routing secara manual, Anda dapat menonaktifkan pengelolaan otomatis ini dengan mengubah pengaturan di file `next.config.js`.

Jika transisi dari `pages/` ke `app/` menghasilkan kesalahan atau masalah, Anda bisa menyesuaikan pengaturan **client router filter** untuk mengurangi kemungkinan kesalahan deteksi (false positive).