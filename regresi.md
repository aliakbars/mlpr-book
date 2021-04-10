# Regresi Linear

Dalam kasus **regresi**, nilai $y$ yang digunakan bersifat **kontinu**. Di sisi lain, dalam kasus **klasifikasi**, nilai $y$ yang digunakan bersifat **diskrit**. Kali ini, kita akan berfokus pada kasus regresi dan bagaimana menghasilkan model yang dapat mengerjakan tugas tersebut. Materi tentang klasifikasi akan diulas pada pertemuan berikutnya.

## Ordinary Least Squares

Dalam bentuk yang paling sederhana, kita dapat mencocokkan garis lurus ke $\mathcal{D}_{train}$ yang mengikuti fungsi:

$$
y = w_0 + w_1 x_1
$$

dengan $w_0$ disebut juga sebagai bias (terkadang ditulis juga dalam simbol $b$) dan $w_1$ adalah *slope* atau gradien yang menentukan kemiringan garis lurus tersebut. Metode *ordinary least squares* mencoba mencari garis yang menghasilkan nilai kuadrat error terkecil atau

$$
\arg \min_{w_0, w_1} \frac{1}{|\mathcal{D}_{train}|} \sum_{(x,y) \in \mathcal{D}_{train}} \ell(y,x,w_0,w_1)
$$

dengan nilai $\ell(y,x,w_0,w_1)$ dapat dirumuskan sebagai

$$
\{y - (w_0 + w_1 x)\}^2
$$

Sebagai ilustrasi, garis berwarna kuning pada {numref}`fb-reg` adalah fungsi linear yang meminimalkan rata-rata error atau residu dari semua titik merah. Dalam kasus tersebut, $x$ adalah jumlah *share* dan $y$ adalah jumlah *like*. Bagaimana jika kita ingin memetakan lebih banyak masukan?

```{figure} images/fb-reg.png
  :name: fb-reg

Prediksi jumlah *share* dari jumlah *like*
```

## Regresi Linear Multidimensi

Anda diberikan sekumpulan foto dari Facebook. Tugas Anda adalah membuat sebuah *regressor* yang dapat memprediksi jumlah *like* yang akan didapatkan foto tersebut jika diberikan gambarnya dan beberapa statistiknya, e.g. jumlah *share*, jumlah komentar, dan profil pengepos. Bagaimana cara Anda dapat menghasilkan model yang dapat melakukan prediksi tersebut?

Hal pertama yang harus dilakukan adalah mengekstraksi fitur dari gambar atau statistik yang diberikan. Untuk mempermudah penjelasan saat ini, maka kita akan menggunakan fitur dari statistik foto tersebut saja.

Untuk masukan $x$, vektor fiturnya adalah:

$$
\mathbf{x} = [x_1,...,x_D].
$$

Kita dapat melihat $\mathbf{x} \in \mathbb{R}^d$ sebagai sebuah titik di ruang berdimensi tinggi. Dengan demikian, fungsi regresi linear untuk multidimensi menjadi

$$
y = w_0 x_0 + w_1 x_1 + w_2 x_2 + ... + w_D x_D = \sum_{j=0}^{D} w_j x_j = \mathbf{w}^T\mathbf{x}
$$

Sebagai contoh, fitur dari statistik sebuah foto dapat direpresentasikan dalam vektor:

| fitur      | nilai |
| ---------- | ----- |
| *share*    | 49 |
| *comment*  | 19 |
| *paid*     | 0  |

Seandainya kita hanya menggunakan dua fitur: *share* dan *comment*, maka yang dihasilkan oleh *least squares regression* akan berbentuk bidang alih-alih garis seperti dapat dilihat pada {numref}`mv-reg`. Untuk dimensi yang lebih tinggi, hasilnya akan berbentuk *hyperplane*. Pertanyaannya, bagaimana mendapatkan nilai $\mathbf{w}$ yang akan membentuk *hyperplane* ini?

```{figure} images/mv-reg.png
  :name: mv-reg

Hasil *least squares regression* dengan $\mathbf{x} \in \mathbb{R}^2$
```

## Meminimalkan Error

Seperti yang disinggung saat membahas *ordinary least squares* di atas, tujuan kita adalah menghasilkan nilai kuadrat error terkecil yang dapat didefinisikan sebagai

$$
E(\mathbf{w}) = \frac{1}{N} \sum_{i=1}^{N} (y_i - \mathbf{w}^T\mathbf{x}_i)^2
$$

dengan $N$ adalah jumlah data yang ada pada $\mathcal{D}_{train}$. Perhatikan bahwa indeks $i$ di sini merujuk kepada data ke-$i$, sedangkan indeks $j$ di atas merujuk pada dimensi ke-$j$. Untuk lebih menyingkat notasi, penjumlahan untuk tiap data (bagian $\sum_{i=1}^N$) dapat diganti dengan notasi matriks-vektor pula sehingga bentuknya akan menjadi

$$
E(\mathbf{w}) = \frac{1}{N}(\mathbf{y} - X \mathbf{w})^T(\mathbf{y} - X \mathbf{w})
$$

dengan vektor $\mathbf{y}$ adalah vektor yang berisi semua label dan $X$ adalah matriks berisi semua data dari semua atribut.

Nilai $E(\mathbf{w})$ dapat diminimalkan dengan mencari turunan pertama, lalu mengatur nilainya menjadi 0, i.e. $\nabla_{\mathbf{w}} E(\mathbf{w}) = 0$.[^optimum] Persamaan ini akan menghasilkan solusi tertutup[^solusi]:

$$
\hat{\mathbf{w}} = (X^T X)^{-1} X^T \mathbf{y}
$$

Perhatikan bahwa persamaan tersebut menggunakan $X$ dan $\mathbf{y}$ yang berarti matriks dan vektor, secara berturut-turut. Bagian $(X^T X)^{-1} X^T$ dikenal sebagai *pseudo-inverse* karena tidak mungkin untuk mencari langsung nilai invers dari $X$.

[^optimum]: Ingat kembali cara mencari titik puncak dari sebuah fungsi pada saat pelajaran kalkulus dulu.
[^solusi]: Silakan buktikan persamaan ini sebagai latihan lebih lanjut.