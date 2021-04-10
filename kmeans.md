# K-Means

## Unsupervised Learning

Anda telah belajar tentang *supervised learning* yang membutuhkan label untuk dapat melatih model. Dalam notasi matematis, Anda ingin menghasilkan:

$$
f: \mathcal{X} \rightarrow \mathcal{Y}
$$

Namun, ada kalanya Anda butuh metode untuk dapat menemukan kelompok atau subpopulasi dalam data. Dengan kata lain, Anda perlu mencari **objek yang serupa** dalam data Anda. Apa yang menjadi kesamaan objek-objek tersebut? Untuk mengerjakan hal ini, kita dapat menggunakan ide yang telah dipelajari dalam materi k-Nearest Neighbours, yaitu konsep kedekatan antarobjek.

Sebagai contoh, Anda ingin mengelompokkan mahasiswa teknik informatika di suatu universitas. Maka, Anda dapat mengelompokkannya berdasarkan kesamaan kelas yang diambil, tapi bisa juga dilihat dari sisi usianya. Ketika Anda telah menemukan kelompok-kelompok tersebut, maka ada kemungkinan untuk menemukan **pencilan** dalam data yang Anda punya. Bisa jadi, pencilan ini adalah mahasiswa yang usianya masih sangat muda karena kelas akselarasi. Namun, bisa juga dia menjadi pencilan karena IPK-nya jauh di atas teman-teman yang lainnya. Jadi, perlu diingat bahwa dalam proses pengelompokan atau ***clustering*** tersebut, Anda boleh jadi menggunakan lebih dari satu dimensi.

Contoh yang lain: Jika dalam bidang Cartesian Anda mendapatkan data seperti pada {numref}`blob`, menurut Anda, berapa subpopulasi yang Anda bisa temukan?

```{figure} images/clustering/clusters.png
  :name: blob

Contoh data dalam dua dimensi
```

Sebagian besar orang mungkin akan melihat ada empat subpopulasi dalam data tersebut seperti pada {numref}`kmeans`. Namun, bagaimana kalau misalnya kita melihat data yang di tengah menjadi satu kelompok sehingga ada tiga subpopulasi? Bukankah tidak ada cara pengelompokan yang pasti?

```{figure} images/clustering/k-means.png
  :name: kmeans

Contoh data yang telah dikelompokkan menjadi empat
```

Hal inilah yang menyebabkan *clustering* menjadi salah satu cabang dari ***unsupervised learning***. Pada akhirnya, kelompok yang Anda hasilkan tersebut *tidak memerlukan label*. Anda hanya tahu bahwa kelompok tersebut punya kesamaan dari fitur atau atribut yang ada.

## Expectation-Maximization (EM)

Algoritma k-Means adalah salah satu cara untuk melakukan *clustering* dengan memanfaatkan konsep **centroid**. Centroid adalah titik pusat yang merupakan rata-rata dari nilai objek dalam tiap dimensi. Dalam algoritma k-Means, ada sejumlah $k$ centroid yang dapat kita tetapkan di awal. Nilainya untuk tiap dimensi diinisialisasi secara acak. Lalu, nilai centroid ini selalu dimutakhirkan sesuai dengan objek yang paling dekat dengan centroid tersebut. Kumpulan objek terdekat dengan centroid tersebutlah yang kemudian dianggap sebagai satu *cluster*. Untuk melakukan hal ini, k-Means memanfaatkan algoritma umum yang dikenal juga sebagai **Expectation-Maximization (EM)**.

```
Inisialisasi centroid secara acak
while not konvergen
    E-step: Masukkan tiap titik/objek ke centroid terdekat
    M-step: Ubah nilai centroid menjadi rata-rata dari tiap titik/objek
    for all a:
        $c_j(a) = \frac{1}{n_j} \sum_{x_i \rightarrow c_j} x_i(a)$
```

Pada {numref}`em`, nilai $a$ adalah dimensi yang digunakan, $c_j$ adalah *cluster* ke-$j$, $x_i$ adalah titik/objek dalam data, dan $n_j$ adalah jumlah titik/objek yang masuk ke dalam *cluster* $j$. Seperti halnya pada algoritma k-NN, kita dapat menggunakan Euclidean distance sebagai metode untuk menghitung $D(x_i, c_j)$. Algoritma EM dapat divisualisasikan seperti pada {numref}`em`.

```{figure} images/clustering/em.png
  :name: em

Konvergensi *cluster* tercapai hanya dalam tiga iterasi
```