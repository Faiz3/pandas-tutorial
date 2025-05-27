# Summary Functions and Maps

## Pengantar
Pada tutorial sebelumnya, kita telah mempelajari cara memilih data yang relevan dari DataFrame atau Series. Mengambil data yang tepat dari representasi data kita sangat penting untuk menyelesaikan pekerjaan, seperti yang telah kita tunjukkan dalam latihan.

Namun, data tidak selalu keluar dari memori dalam format yang kita inginkan langsung. Terkadang kita harus melakukan beberapa pekerjaan lagi untuk memformat ulang data tersebut untuk tugas yang sedang dikerjakan. Tutorial ini akan membahas berbagai operasi yang dapat kita terapkan pada data kita untuk mendapatkan input yang "tepat".

Kami akan menggunakan data Majalah Wine untuk demonstrasi.


```python
import pandas as pd
pd.set_option('display.max_rows', 5)
import numpy as np
reviews = pd.read_csv("../winemag-data-130k-v2.csv", index_col=0)
```


```python
reviews
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>country</th>
      <th>description</th>
      <th>designation</th>
      <th>points</th>
      <th>price</th>
      <th>province</th>
      <th>region_1</th>
      <th>region_2</th>
      <th>taster_name</th>
      <th>taster_twitter_handle</th>
      <th>title</th>
      <th>variety</th>
      <th>winery</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Italy</td>
      <td>Aromas include tropical fruit, broom, brimston...</td>
      <td>Vulkà Bianco</td>
      <td>87</td>
      <td>NaN</td>
      <td>Sicily &amp; Sardinia</td>
      <td>Etna</td>
      <td>NaN</td>
      <td>Kerin O’Keefe</td>
      <td>@kerinokeefe</td>
      <td>Nicosia 2013 Vulkà Bianco  (Etna)</td>
      <td>White Blend</td>
      <td>Nicosia</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Portugal</td>
      <td>This is ripe and fruity, a wine that is smooth...</td>
      <td>Avidagos</td>
      <td>87</td>
      <td>15.0</td>
      <td>Douro</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Roger Voss</td>
      <td>@vossroger</td>
      <td>Quinta dos Avidagos 2011 Avidagos Red (Douro)</td>
      <td>Portuguese Red</td>
      <td>Quinta dos Avidagos</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>129969</th>
      <td>France</td>
      <td>A dry style of Pinot Gris, this is crisp with ...</td>
      <td>NaN</td>
      <td>90</td>
      <td>32.0</td>
      <td>Alsace</td>
      <td>Alsace</td>
      <td>NaN</td>
      <td>Roger Voss</td>
      <td>@vossroger</td>
      <td>Domaine Marcel Deiss 2012 Pinot Gris (Alsace)</td>
      <td>Pinot Gris</td>
      <td>Domaine Marcel Deiss</td>
    </tr>
    <tr>
      <th>129970</th>
      <td>France</td>
      <td>Big, rich and off-dry, this is powered by inte...</td>
      <td>Lieu-dit Harth Cuvée Caroline</td>
      <td>90</td>
      <td>21.0</td>
      <td>Alsace</td>
      <td>Alsace</td>
      <td>NaN</td>
      <td>Roger Voss</td>
      <td>@vossroger</td>
      <td>Domaine Schoffit 2012 Lieu-dit Harth Cuvée Car...</td>
      <td>Gewürztraminer</td>
      <td>Domaine Schoffit</td>
    </tr>
  </tbody>
</table>
<p>129971 rows × 13 columns</p>
</div>



## Summary functions
Pandas menyediakan banyak "fungsi ringkasan" sederhana (bukan nama resmi) yang merestrukturisasi data dengan cara yang berguna. Sebagai contoh, perhatikan metode describe():


```python
reviews.points.describe()
```




    count    129971.000000
    mean         88.447138
                 ...      
    75%          91.000000
    max         100.000000
    Name: points, Length: 8, dtype: float64



Metode ini menghasilkan ringkasan tingkat tinggi dari atribut-atribut kolom yang diberikan. Metode ini sadar tipe, yang berarti bahwa keluarannya berubah berdasarkan tipe data dari masukannya. Keluaran di atas hanya masuk akal untuk data numerik; untuk data string, inilah yang kita dapatkan:

Jika Anda ingin mendapatkan beberapa statistik ringkasan sederhana tertentu tentang kolom dalam DataFrame atau Series, biasanya ada fungsi pandas yang membantu untuk mewujudkannya.

Sebagai contoh, untuk melihat rata-rata dari poin yang diberikan (misalnya, seberapa baik nilai rata-rata anggur), kita dapat menggunakan fungsi mean():


```python
reviews.points.mean()
```




    np.float64(88.44713820775404)



Untuk melihat daftar nilai unik, kita dapat menggunakan fungsi `unique()`:


```python
reviews.taster_name.unique()
```




    array(['Kerin O’Keefe', 'Roger Voss', 'Paul Gregutt',
           'Alexander Peartree', 'Michael Schachner', 'Anna Lee C. Iijima',
           'Virginie Boone', 'Matt Kettmann', nan, 'Sean P. Sullivan',
           'Jim Gordon', 'Joe Czerwinski', 'Anne Krebiehl\xa0MW',
           'Lauren Buzzeo', 'Mike DeSimone', 'Jeff Jenssen',
           'Susan Kostrzewa', 'Carrie Dykes', 'Fiona Adams',
           'Christina Pickard'], dtype=object)



Untuk melihat daftar nilai unik dan seberapa sering nilai tersebut muncul dalam kumpulan data, kita dapat menggunakan metode `value_counts()`:


```python
reviews.taster_name.value_counts()
```




    taster_name
    Roger Voss           25514
    Michael Schachner    15134
                         ...  
    Fiona Adams             27
    Christina Pickard        6
    Name: count, Length: 19, dtype: int64



## Maps
Peta adalah istilah yang dipinjam dari matematika, untuk sebuah fungsi yang mengambil satu set nilai dan "memetakannya" ke set nilai lainnya. Dalam ilmu data, kita sering kali memiliki kebutuhan untuk membuat representasi baru dari data yang sudah ada, atau untuk mengubah data dari format yang ada saat ini ke format yang kita inginkan nantinya. Peta adalah yang menangani pekerjaan ini, menjadikannya sangat penting untuk menyelesaikan pekerjaan Anda!

Ada dua metode pemetaan yang akan sering Anda gunakan.

`map()` adalah yang pertama, dan sedikit lebih sederhana. Sebagai contoh, misalkan kita ingin mengubah nilai yang diterima wine menjadi 0. Kita dapat melakukan hal ini sebagai berikut:


```python
review_points_mean = reviews.points.mean()
reviews.points.map(lambda p: p - review_points_mean)
```




    0        -1.447138
    1        -1.447138
                ...   
    129969    1.552862
    129970    1.552862
    Name: points, Length: 129971, dtype: float64



Fungsi yang Anda berikan kepada map() harus mengharapkan satu nilai dari Series (nilai titik, dalam contoh di atas), dan mengembalikan versi transformasi dari nilai tersebut. map() mengembalikan Series baru di mana semua nilai telah ditransformasikan oleh fungsi Anda.

apply() adalah metode yang setara jika kita ingin mentransformasi seluruh DataFrame dengan memanggil metode khusus pada setiap baris.


```python
def remean_points(row):
    row.points = row.points - review_points_mean
    return row

reviews.apply(remean_points, axis='columns')
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>country</th>
      <th>description</th>
      <th>designation</th>
      <th>points</th>
      <th>price</th>
      <th>province</th>
      <th>region_1</th>
      <th>region_2</th>
      <th>taster_name</th>
      <th>taster_twitter_handle</th>
      <th>title</th>
      <th>variety</th>
      <th>winery</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Italy</td>
      <td>Aromas include tropical fruit, broom, brimston...</td>
      <td>Vulkà Bianco</td>
      <td>-1.447138</td>
      <td>NaN</td>
      <td>Sicily &amp; Sardinia</td>
      <td>Etna</td>
      <td>NaN</td>
      <td>Kerin O’Keefe</td>
      <td>@kerinokeefe</td>
      <td>Nicosia 2013 Vulkà Bianco  (Etna)</td>
      <td>White Blend</td>
      <td>Nicosia</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Portugal</td>
      <td>This is ripe and fruity, a wine that is smooth...</td>
      <td>Avidagos</td>
      <td>-1.447138</td>
      <td>15.0</td>
      <td>Douro</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Roger Voss</td>
      <td>@vossroger</td>
      <td>Quinta dos Avidagos 2011 Avidagos Red (Douro)</td>
      <td>Portuguese Red</td>
      <td>Quinta dos Avidagos</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>129969</th>
      <td>France</td>
      <td>A dry style of Pinot Gris, this is crisp with ...</td>
      <td>NaN</td>
      <td>1.552862</td>
      <td>32.0</td>
      <td>Alsace</td>
      <td>Alsace</td>
      <td>NaN</td>
      <td>Roger Voss</td>
      <td>@vossroger</td>
      <td>Domaine Marcel Deiss 2012 Pinot Gris (Alsace)</td>
      <td>Pinot Gris</td>
      <td>Domaine Marcel Deiss</td>
    </tr>
    <tr>
      <th>129970</th>
      <td>France</td>
      <td>Big, rich and off-dry, this is powered by inte...</td>
      <td>Lieu-dit Harth Cuvée Caroline</td>
      <td>1.552862</td>
      <td>21.0</td>
      <td>Alsace</td>
      <td>Alsace</td>
      <td>NaN</td>
      <td>Roger Voss</td>
      <td>@vossroger</td>
      <td>Domaine Schoffit 2012 Lieu-dit Harth Cuvée Car...</td>
      <td>Gewürztraminer</td>
      <td>Domaine Schoffit</td>
    </tr>
  </tbody>
</table>
<p>129971 rows × 13 columns</p>
</div>



Jika kita telah memanggil reviews.apply() dengan axis = 'index', maka alih-alih mengoper sebuah fungsi untuk mentransformasi setiap baris, kita perlu memberikan sebuah fungsi untuk mentransformasi setiap kolom.

Perhatikan bahwa map() dan apply() masing-masing mengembalikan Series dan DataFrame baru yang telah ditransformasi. Fungsi-fungsi tersebut tidak mengubah data asli yang dipanggil. Jika kita lihat pada baris pertama dari ulasan, kita dapat melihat bahwa data tersebut masih memiliki nilai poin aslinya.


```python
reviews.head(1)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>country</th>
      <th>description</th>
      <th>designation</th>
      <th>points</th>
      <th>price</th>
      <th>province</th>
      <th>region_1</th>
      <th>region_2</th>
      <th>taster_name</th>
      <th>taster_twitter_handle</th>
      <th>title</th>
      <th>variety</th>
      <th>winery</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Italy</td>
      <td>Aromas include tropical fruit, broom, brimston...</td>
      <td>Vulkà Bianco</td>
      <td>87</td>
      <td>NaN</td>
      <td>Sicily &amp; Sardinia</td>
      <td>Etna</td>
      <td>NaN</td>
      <td>Kerin O’Keefe</td>
      <td>@kerinokeefe</td>
      <td>Nicosia 2013 Vulkà Bianco  (Etna)</td>
      <td>White Blend</td>
      <td>Nicosia</td>
    </tr>
  </tbody>
</table>
</div>



Pandas menyediakan banyak operasi pemetaan umum sebagai fitur bawaan. Sebagai contoh, berikut ini adalah cara yang lebih cepat untuk mengurutkan ulang kolom poin kita:


```python
review_points_mean = reviews.points.mean()
reviews.points - review_points_mean
```




    0        -1.447138
    1        -1.447138
                ...   
    129969    1.552862
    129970    1.552862
    Name: points, Length: 129971, dtype: float64



Dalam kode ini, kita melakukan operasi antara banyak nilai di sisi kiri (semua yang ada di dalam deret) dan satu nilai di sisi kanan (nilai rata-rata). Pandas melihat ekspresi ini dan mengetahui bahwa kita bermaksud mengurangi nilai rata-rata tersebut dari setiap nilai dalam kumpulan data.

Pandas juga akan memahami apa yang harus dilakukan jika kita melakukan operasi ini di antara deret yang sama panjangnya. Sebagai contoh, cara mudah untuk menggabungkan informasi negara dan wilayah dalam dataset adalah dengan melakukan hal berikut:


```python
reviews.country + " - " + reviews.region_1
```




    0            Italy - Etna
    1                     NaN
                   ...       
    129969    France - Alsace
    129970    France - Alsace
    Length: 129971, dtype: object



Operator-operator ini lebih cepat daripada map() atau apply() karena mereka menggunakan kecepatan yang dibangun ke dalam panda. Semua operator Python standar (>, <, ==, dan seterusnya) bekerja dengan cara ini.

Namun, operator-operator tersebut tidak sefleksibel map() atau apply(), yang dapat melakukan hal-hal yang lebih canggih, seperti menerapkan logika bersyarat, yang tidak dapat dilakukan hanya dengan penjumlahan dan pengurangan.


```python

```
