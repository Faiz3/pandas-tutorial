# Data Types and Missing Values

## Introduction

Dalam tutorial ini, Anda akan mempelajari cara menyelidiki tipe data di dalam DataFrame atau Series. Anda juga akan mempelajari cara menemukan dan mengganti entri.

## Dtypes
Tipe data untuk kolom dalam DataFrame atau Series dikenal sebagai dtype.

Anda dapat menggunakan properti dtype untuk mengambil tipe kolom tertentu. Sebagai contoh, kita bisa mendapatkan dtype dari kolom harga di DataFrame ulasan:


```python
import pandas as pd

reviews = pd.read_csv('../winemag-data-130k-v2.csv')
```


```python
reviews.price.dtype
```




    dtype('float64')



Sebagai alternatif, properti dtypes mengembalikan dtype dari setiap kolom dalam DataFrame:


```python
reviews.dtypes
```




    Unnamed: 0                 int64
    country                   object
    description               object
    designation               object
    points                     int64
    price                    float64
    province                  object
    region_1                  object
    region_2                  object
    taster_name               object
    taster_twitter_handle     object
    title                     object
    variety                   object
    winery                    object
    dtype: object



Tipe data memberi tahu kita tentang bagaimana pandas menyimpan data secara internal. float64 berarti bahwa ia menggunakan angka floating point 64-bit; int64 berarti bilangan bulat yang berukuran sama, dan seterusnya.

Satu keunikan yang perlu diingat (dan ditampilkan dengan sangat jelas di sini) adalah bahwa kolom yang seluruhnya terdiri dari string tidak mendapatkan tipe mereka sendiri; mereka diberi tipe objek.

Anda dapat mengkonversi sebuah kolom dari satu tipe ke tipe yang lain di mana pun konversi tersebut masuk akal dengan menggunakan fungsi astype(). Sebagai contoh, kita dapat mengubah kolom poin dari tipe data int64 yang sudah ada menjadi tipe data float64:


```python
reviews.points.astype('float64')
```




    0         87.0
    1         87.0
    2         87.0
    3         87.0
    4         87.0
              ... 
    129966    90.0
    129967    90.0
    129968    90.0
    129969    90.0
    129970    90.0
    Name: points, Length: 129971, dtype: float64



Indeks DataFrame atau Series juga memiliki dtype sendiri:


```python
reviews.index.dtype
```




    dtype('int64')



Panda juga mendukung tipe data yang lebih eksotis, seperti data kategorikal dan data deret waktu. Karena tipe data ini lebih jarang digunakan, kita akan mengabaikannya hingga bagian selanjutnya dari tutorial ini.

## Missing data
Entri yang nilainya tidak ada diberi nilai NaN, kependekan dari "Not a Number". Untuk alasan teknis, nilai NaN ini selalu bertipe float64.

Pandas menyediakan beberapa metode khusus untuk data yang hilang. Untuk memilih entri NaN, Anda bisa menggunakan pd.isnull() (atau pendampingnya pd.notnull()). Ini dimaksudkan untuk digunakan dengan demikian:


```python
reviews[pd.isnull(reviews.country)]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
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
      <th>913</th>
      <td>913</td>
      <td>NaN</td>
      <td>Amber in color, this wine has aromas of peach ...</td>
      <td>Asureti Valley</td>
      <td>87</td>
      <td>30.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Mike DeSimone</td>
      <td>@worldwineguys</td>
      <td>Gotsa Family Wines 2014 Asureti Valley Chinuri</td>
      <td>Chinuri</td>
      <td>Gotsa Family Wines</td>
    </tr>
    <tr>
      <th>3131</th>
      <td>3131</td>
      <td>NaN</td>
      <td>Soft, fruity and juicy, this is a pleasant, si...</td>
      <td>Partager</td>
      <td>83</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Roger Voss</td>
      <td>@vossroger</td>
      <td>Barton &amp; Guestier NV Partager Red</td>
      <td>Red Blend</td>
      <td>Barton &amp; Guestier</td>
    </tr>
    <tr>
      <th>4243</th>
      <td>4243</td>
      <td>NaN</td>
      <td>Violet-red in color, this semisweet wine has a...</td>
      <td>Red Naturally Semi-Sweet</td>
      <td>88</td>
      <td>18.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Mike DeSimone</td>
      <td>@worldwineguys</td>
      <td>Kakhetia Traditional Winemaking 2012 Red Natur...</td>
      <td>Ojaleshi</td>
      <td>Kakhetia Traditional Winemaking</td>
    </tr>
    <tr>
      <th>9509</th>
      <td>9509</td>
      <td>NaN</td>
      <td>This mouthwatering blend starts with a nose of...</td>
      <td>Theopetra Malagouzia-Assyrtiko</td>
      <td>92</td>
      <td>28.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Susan Kostrzewa</td>
      <td>@suskostrzewa</td>
      <td>Tsililis 2015 Theopetra Malagouzia-Assyrtiko W...</td>
      <td>White Blend</td>
      <td>Tsililis</td>
    </tr>
    <tr>
      <th>9750</th>
      <td>9750</td>
      <td>NaN</td>
      <td>This orange-style wine has a cloudy yellow-gol...</td>
      <td>Orange Nikolaevo Vineyard</td>
      <td>89</td>
      <td>28.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Jeff Jenssen</td>
      <td>@worldwineguys</td>
      <td>Ross-idi 2015 Orange Nikolaevo Vineyard Chardo...</td>
      <td>Chardonnay</td>
      <td>Ross-idi</td>
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
      <td>...</td>
    </tr>
    <tr>
      <th>124176</th>
      <td>124176</td>
      <td>NaN</td>
      <td>This Swiss red blend is composed of four varie...</td>
      <td>Les Romaines</td>
      <td>90</td>
      <td>30.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Jeff Jenssen</td>
      <td>@worldwineguys</td>
      <td>Les Frères Dutruy 2014 Les Romaines Red</td>
      <td>Red Blend</td>
      <td>Les Frères Dutruy</td>
    </tr>
    <tr>
      <th>129407</th>
      <td>129407</td>
      <td>NaN</td>
      <td>Dry spicy aromas of dusty plum and tomato add ...</td>
      <td>Reserve</td>
      <td>89</td>
      <td>22.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Michael Schachner</td>
      <td>@wineschach</td>
      <td>El Capricho 2015 Reserve Cabernet Sauvignon</td>
      <td>Cabernet Sauvignon</td>
      <td>El Capricho</td>
    </tr>
    <tr>
      <th>129408</th>
      <td>129408</td>
      <td>NaN</td>
      <td>El Capricho is one of Uruguay's more consisten...</td>
      <td>Reserve</td>
      <td>89</td>
      <td>22.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Michael Schachner</td>
      <td>@wineschach</td>
      <td>El Capricho 2015 Reserve Tempranillo</td>
      <td>Tempranillo</td>
      <td>El Capricho</td>
    </tr>
    <tr>
      <th>129590</th>
      <td>129590</td>
      <td>NaN</td>
      <td>A blend of 60% Syrah, 30% Cabernet Sauvignon a...</td>
      <td>Shah</td>
      <td>90</td>
      <td>30.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Mike DeSimone</td>
      <td>@worldwineguys</td>
      <td>Büyülübağ 2012 Shah Red</td>
      <td>Red Blend</td>
      <td>Büyülübağ</td>
    </tr>
    <tr>
      <th>129900</th>
      <td>129900</td>
      <td>NaN</td>
      <td>This wine offers a delightful bouquet of black...</td>
      <td>NaN</td>
      <td>91</td>
      <td>32.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Mike DeSimone</td>
      <td>@worldwineguys</td>
      <td>Psagot 2014 Merlot</td>
      <td>Merlot</td>
      <td>Psagot</td>
    </tr>
  </tbody>
</table>
<p>63 rows × 14 columns</p>
</div>



Mengganti nilai yang hilang adalah operasi yang umum dilakukan. Pandas menyediakan metode yang sangat berguna untuk masalah ini: fillna(). fillna() menyediakan beberapa strategi yang berbeda untuk mengurangi data tersebut. Sebagai contoh, kita bisa mengganti setiap NaN dengan "Unknown":


```python
reviews.region_2.fillna("Unknown")
```




    0                   Unknown
    1                   Unknown
    2         Willamette Valley
    3                   Unknown
    4         Willamette Valley
                    ...        
    129966              Unknown
    129967         Oregon Other
    129968              Unknown
    129969              Unknown
    129970              Unknown
    Name: region_2, Length: 129971, dtype: object



Atau kita dapat mengisi setiap nilai yang hilang dengan nilai non-null pertama yang muncul beberapa saat setelah record yang diberikan dalam database. Ini dikenal sebagai strategi pengisian ulang.

Atau, kita mungkin memiliki nilai bukan nol yang ingin kita ganti. Sebagai contoh, misalkan sejak kumpulan data ini diterbitkan, pengulas Kerin O'Keefe telah mengubah pegangan Twitter-nya dari @kerinokeefe menjadi @kerino. Salah satu cara untuk merefleksikan hal ini di dalam dataset adalah dengan menggunakan metode replace():


```python
reviews.taster_twitter_handle.replace("@kerinokeefe", "@kerino")
```




    0             @kerino
    1          @vossroger
    2         @paulgwine 
    3                 NaN
    4         @paulgwine 
                 ...     
    129966            NaN
    129967    @paulgwine 
    129968     @vossroger
    129969     @vossroger
    129970     @vossroger
    Name: taster_twitter_handle, Length: 129971, dtype: object



Metode replace() perlu disebutkan di sini karena metode ini berguna untuk mengganti data yang hilang yang diberi semacam nilai sentinel dalam kumpulan data: hal-hal seperti "Tidak diketahui", "Dirahasiakan", "Tidak valid", dan seterusnya.


```python

```
