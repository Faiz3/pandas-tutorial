# Introduction

Sekarang Anda siap untuk mendapatkan pemahaman yang lebih dalam tentang data Anda.

Jalankan sel berikut untuk memuat data Anda dan beberapa fungsi utilitas (termasuk kode untuk memeriksa jawaban Anda).


```python
import pandas as pd
pd.set_option("display.max_rows", 5)
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



# Exercises

## 1.

Berapa nilai tengah dari kolom `points` di DataFrame `reviews`?


```python
median_points = ___

median_points
```




    np.float64(88.0)



## 2. 
Negara mana saja yang diwakili dalam dataset? (Jawaban Anda tidak boleh ada yang ganda).


```python
countries = ___

countries
```




    array(['Italy', 'Portugal', 'US', 'Spain', 'France', 'Germany',
           'Argentina', 'Chile', 'Australia', 'Austria', 'South Africa',
           'New Zealand', 'Israel', 'Hungary', 'Greece', 'Romania', 'Mexico',
           'Canada', nan, 'Turkey', 'Czech Republic', 'Slovenia',
           'Luxembourg', 'Croatia', 'Georgia', 'Uruguay', 'England',
           'Lebanon', 'Serbia', 'Brazil', 'Moldova', 'Morocco', 'Peru',
           'India', 'Bulgaria', 'Cyprus', 'Armenia', 'Switzerland',
           'Bosnia and Herzegovina', 'Ukraine', 'Slovakia', 'Macedonia',
           'China', 'Egypt'], dtype=object)



## 3.
Seberapa sering setiap negara muncul dalam dataset? Buat Seri `reviews_per_country` yang memetakan negara ke jumlah ulasan wine dari negara tersebut.


```python
reviews_per_country = ___
```


```python
reviews_per_country
```




    country
    US        54504
    France    22093
              ...  
    China         1
    Egypt         1
    Name: count, Length: 43, dtype: int64



## 4.
Buat variabel `centered_price` yang berisi versi dari kolom `price` dengan harga rata-rata yang telah dikurangi.

(Catatan: transformasi 'pemusatan' ini merupakan langkah preprocessing yang umum dilakukan sebelum menerapkan berbagai algoritma machine learning).


```python
centered_price = ___

centered_price
```




    np.float64(35.363389129985535)



## 5.
Saya adalah pembeli wine yang ekonomis. Wine mana yang merupakan "penawaran terbaik"? Buat variabel `bargain_wine` dengan judul wine dengan rasio poin-ke-harga tertinggi dalam dataset.


```python
bargain_wine = ___
bargain_wine
```




    'Bandit NV Merlot (California)'



## 6.
Hanya ada begitu banyak kata yang dapat Anda gunakan saat mendeskripsikan sebotol wine. Apakah wine lebih cenderung "tropis" atau "buah"? Buat Seri `descriptor_counts` yang menghitung berapa kali masing-masing dari kedua kata ini muncul di kolom `description` dalam set data. (Untuk mempermudah, mari kita abaikan versi huruf besar dari kata-kata ini).


```python
descriptor_counts = ___
```


```python
descriptor_counts
```




    tropical    3607
    fruity      9090
    dtype: int64



## 7.
Kami ingin menampilkan ulasan wine ini di situs web kami, tetapi sistem penilaian yang berkisar antara 80 hingga 100 poin terlalu sulit untuk dipahami - kami ingin menerjemahkannya ke dalam peringkat bintang yang sederhana. Skor 95 atau lebih tinggi dianggap sebagai 3 bintang, skor minimal 85 tetapi kurang dari 95 adalah 2 bintang. Skor lainnya adalah 1 bintang.

Selain itu, Canadian Vintners Association membeli banyak iklan di situs ini, jadi wine apa pun dari Kanada secara otomatis akan mendapatkan 3 bintang, berapa pun nilainya.

Buatlah seri `star_ratings` dengan jumlah bintang yang sesuai dengan setiap ulasan dalam kumpulan data.


```python
star_ratings = ___
```




    0    2
    1    2
    2    2
    3    2
    4    2
    dtype: int64




```python

```
