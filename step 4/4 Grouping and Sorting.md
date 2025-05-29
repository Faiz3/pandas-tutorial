## Pendahuluan
Peta memungkinkan kita untuk mengubah data dalam DataFrame atau Seri satu per satu untuk seluruh kolom. Namun, sering kali kita ingin mengelompokkan data kita, dan kemudian melakukan sesuatu yang spesifik pada kelompok data tersebut.

Seperti yang akan Anda pelajari, kita melakukan hal ini dengan operasi groupby(). Kita juga akan membahas beberapa topik tambahan, seperti cara yang lebih kompleks untuk mengindeks DataFrame Anda, serta cara mengurutkan data Anda.

## Groupwise analysis

Salah satu fungsi yang sering kita gunakan sejauh ini adalah fungsi value_counts(). Kita dapat meniru apa yang dilakukan oleh value_counts() dengan melakukan hal berikut:


```python
import pandas as pd
reviews = pd.read_csv("../winemag-data-130k-v2.csv", index_col=0)
pd.set_option("display.max_rows", 5)
```


```python
reviews.groupby('points').points.count()
```




    points
    80     397
    81     692
          ... 
    99      33
    100     19
    Name: points, Length: 21, dtype: int64



groupby() membuat sebuah grup ulasan yang memberikan nilai poin yang sama untuk wine yang diberikan. Kemudian, untuk setiap kelompok ini, kita mengambil kolom points() dan menghitung berapa kali muncul. value_counts() hanyalah jalan pintas untuk operasi groupby() ini.

Kita dapat menggunakan fungsi ringkasan yang telah kita gunakan sebelumnya dengan data ini. Sebagai contoh, untuk mendapatkan anggur termurah di setiap kategori nilai poin, kita dapat melakukan hal berikut:


```python
reviews.groupby('points').price.min()
```




    points
    80      5.0
    81      5.0
           ... 
    99     44.0
    100    80.0
    Name: price, Length: 21, dtype: float64



Anda dapat membayangkan setiap kelompok yang kita hasilkan sebagai potongan dari DataFrame yang hanya berisi data dengan nilai yang cocok. DataFrame ini dapat diakses oleh kita secara langsung dengan menggunakan metode apply(), dan kita kemudian dapat memanipulasi data dengan cara apa pun yang kita inginkan. Sebagai contoh, berikut ini salah satu cara untuk memilih nama wine pertama yang ditinjau dari setiap kilang wine dalam dataset:


```python
reviews.groupby('winery').apply(lambda df: df.title.iloc[0],include_groups=False)
```




    winery
    1+1=3                          1+1=3 NV Rosé Sparkling (Cava)
    10 Knots                 10 Knots 2010 Viognier (Paso Robles)
                                      ...                        
    àMaurice    àMaurice 2013 Fred Estate Syrah (Walla Walla V...
    Štoka                         Štoka 2009 Izbrani Teran (Kras)
    Length: 16757, dtype: object




```python
reviews.groupby(['country', 'province']).apply(lambda df: df.loc[df.points.idxmax()],include_groups=False)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>description</th>
      <th>designation</th>
      <th>points</th>
      <th>price</th>
      <th>region_1</th>
      <th>region_2</th>
      <th>taster_name</th>
      <th>taster_twitter_handle</th>
      <th>title</th>
      <th>variety</th>
      <th>winery</th>
    </tr>
    <tr>
      <th>country</th>
      <th>province</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">Argentina</th>
      <th>Mendoza Province</th>
      <td>If the color doesn't tell the full story, the ...</td>
      <td>Nicasia Vineyard</td>
      <td>97</td>
      <td>120.0</td>
      <td>Mendoza</td>
      <td>NaN</td>
      <td>Michael Schachner</td>
      <td>@wineschach</td>
      <td>Bodega Catena Zapata 2006 Nicasia Vineyard Mal...</td>
      <td>Malbec</td>
      <td>Bodega Catena Zapata</td>
    </tr>
    <tr>
      <th>Other</th>
      <td>Take note, this could be the best wine Colomé ...</td>
      <td>Reserva</td>
      <td>95</td>
      <td>90.0</td>
      <td>Salta</td>
      <td>NaN</td>
      <td>Michael Schachner</td>
      <td>@wineschach</td>
      <td>Colomé 2010 Reserva Malbec (Salta)</td>
      <td>Malbec</td>
      <td>Colomé</td>
    </tr>
    <tr>
      <th>...</th>
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
    </tr>
    <tr>
      <th rowspan="2" valign="top">Uruguay</th>
      <th>San Jose</th>
      <td>Baked, sweet, heavy aromas turn earthy with ti...</td>
      <td>El Preciado Gran Reserva</td>
      <td>87</td>
      <td>50.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Michael Schachner</td>
      <td>@wineschach</td>
      <td>Castillo Viejo 2005 El Preciado Gran Reserva R...</td>
      <td>Red Blend</td>
      <td>Castillo Viejo</td>
    </tr>
    <tr>
      <th>Uruguay</th>
      <td>Cherry and berry aromas are ripe, healthy and ...</td>
      <td>Blend 002 Limited Edition</td>
      <td>91</td>
      <td>22.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Michael Schachner</td>
      <td>@wineschach</td>
      <td>Narbona NV Blend 002 Limited Edition Tannat-Ca...</td>
      <td>Tannat-Cabernet Franc</td>
      <td>Narbona</td>
    </tr>
  </tbody>
</table>
<p>425 rows × 11 columns</p>
</div>



Metode groupby() lain yang perlu disebutkan adalah agg(), yang memungkinkan Anda menjalankan banyak fungsi yang berbeda pada DataFrame secara bersamaan. Sebagai contoh, kita dapat menghasilkan ringkasan statistik sederhana dari dataset sebagai berikut:


```python
reviews.groupby(['country']).price.agg([len, 'min', 'max'])
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>len</th>
      <th>min</th>
      <th>max</th>
    </tr>
    <tr>
      <th>country</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Argentina</th>
      <td>3800</td>
      <td>4.0</td>
      <td>230.0</td>
    </tr>
    <tr>
      <th>Armenia</th>
      <td>2</td>
      <td>14.0</td>
      <td>15.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Ukraine</th>
      <td>14</td>
      <td>6.0</td>
      <td>13.0</td>
    </tr>
    <tr>
      <th>Uruguay</th>
      <td>109</td>
      <td>10.0</td>
      <td>130.0</td>
    </tr>
  </tbody>
</table>
<p>43 rows × 3 columns</p>
</div>



Penggunaan groupby() yang efektif akan memungkinkan Anda untuk melakukan banyak hal yang sangat hebat dengan dataset Anda.

## Multi-indexes
Dalam semua contoh yang telah kita lihat sejauh ini, kita telah bekerja dengan objek DataFrame atau Series dengan indeks label tunggal. groupby() sedikit berbeda karena, tergantung pada operasi yang kita jalankan, terkadang akan menghasilkan apa yang disebut multi-indeks.

Multi-indeks berbeda dengan indeks biasa karena memiliki banyak level. Sebagai contoh:


```python
countries_reviewed = reviews.groupby(['country', 'province']).description.agg([len])
countries_reviewed
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>len</th>
    </tr>
    <tr>
      <th>country</th>
      <th>province</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">Argentina</th>
      <th>Mendoza Province</th>
      <td>3264</td>
    </tr>
    <tr>
      <th>Other</th>
      <td>536</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Uruguay</th>
      <th>San Jose</th>
      <td>3</td>
    </tr>
    <tr>
      <th>Uruguay</th>
      <td>24</td>
    </tr>
  </tbody>
</table>
<p>425 rows × 1 columns</p>
</div>




```python
mi = countries_reviewed.index
type(mi)
print(mi)
```

    RangeIndex(start=0, stop=425, step=1)
    

Multi-indeks memiliki beberapa metode untuk menangani struktur berjenjang yang tidak dimiliki oleh indeks tingkat tunggal. Indeks ini juga membutuhkan dua tingkat label untuk mengambil nilai. Berurusan dengan output multi-indeks adalah "kendala" yang umum bagi pengguna yang baru mengenal pandas.

Kasus penggunaan untuk multi-indeks dirinci bersama dengan instruksi untuk menggunakannya di bagian MultiIndex / Advanced Selection pada dokumentasi pandas.

Namun, secara umum metode multi-indeks yang paling sering Anda gunakan adalah metode untuk mengubah kembali ke indeks biasa, yaitu metode reset_index():


```python
countries_reviewed.reset_index()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>country</th>
      <th>province</th>
      <th>len</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Argentina</td>
      <td>Mendoza Province</td>
      <td>3264</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Argentina</td>
      <td>Other</td>
      <td>536</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>423</th>
      <td>Uruguay</td>
      <td>San Jose</td>
      <td>3</td>
    </tr>
    <tr>
      <th>424</th>
      <td>Uruguay</td>
      <td>Uruguay</td>
      <td>24</td>
    </tr>
  </tbody>
</table>
<p>425 rows × 3 columns</p>
</div>



## Sorting
Melihat kembali ke countries_reviewed, kita dapat melihat bahwa pengelompokan mengembalikan data dalam urutan indeks, bukan dalam urutan nilai. Dengan kata lain, ketika mengeluarkan hasil dari groupby, urutan baris tergantung pada nilai dalam indeks, bukan pada data.

Untuk mendapatkan data dalam urutan yang diinginkan, kita dapat mengurutkannya sendiri. Metode sort_values() sangat berguna untuk hal ini.


```python
countries_reviewed = countries_reviewed.reset_index()
countries_reviewed.sort_values(by='len')
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>country</th>
      <th>province</th>
      <th>len</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>386</th>
      <td>Turkey</td>
      <td>Elazığ-Diyarbakir</td>
      <td>1</td>
    </tr>
    <tr>
      <th>389</th>
      <td>Turkey</td>
      <td>Urla-Thrace</td>
      <td>1</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>415</th>
      <td>US</td>
      <td>Washington</td>
      <td>8639</td>
    </tr>
    <tr>
      <th>392</th>
      <td>US</td>
      <td>California</td>
      <td>36247</td>
    </tr>
  </tbody>
</table>
<p>425 rows × 3 columns</p>
</div>



sort_values() secara default menggunakan pengurutan menaik, di mana nilai terendah didahulukan. Namun, seringkali kita menginginkan pengurutan menurun, di mana angka yang lebih tinggi didahulukan. Hal ini dapat dilakukan dengan cara demikian:


```python
countries_reviewed.sort_values(by='len', ascending=False)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>country</th>
      <th>province</th>
      <th>len</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>392</th>
      <td>US</td>
      <td>California</td>
      <td>36247</td>
    </tr>
    <tr>
      <th>415</th>
      <td>US</td>
      <td>Washington</td>
      <td>8639</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>395</th>
      <td>US</td>
      <td>Hawaii</td>
      <td>1</td>
    </tr>
    <tr>
      <th>399</th>
      <td>US</td>
      <td>Kentucky</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>425 rows × 3 columns</p>
</div>




```python
countries_reviewed.sort_index()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>country</th>
      <th>province</th>
      <th>len</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Argentina</td>
      <td>Mendoza Province</td>
      <td>3264</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Argentina</td>
      <td>Other</td>
      <td>536</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>423</th>
      <td>Uruguay</td>
      <td>San Jose</td>
      <td>3</td>
    </tr>
    <tr>
      <th>424</th>
      <td>Uruguay</td>
      <td>Uruguay</td>
      <td>24</td>
    </tr>
  </tbody>
</table>
<p>425 rows × 3 columns</p>
</div>



Terakhir, ketahuilah bahwa Anda dapat mengurutkan berdasarkan lebih dari satu kolom sekaligus:


```python
countries_reviewed.sort_values(by=['country', 'len'])
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>country</th>
      <th>province</th>
      <th>len</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Argentina</td>
      <td>Other</td>
      <td>536</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Argentina</td>
      <td>Mendoza Province</td>
      <td>3264</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>424</th>
      <td>Uruguay</td>
      <td>Uruguay</td>
      <td>24</td>
    </tr>
    <tr>
      <th>419</th>
      <td>Uruguay</td>
      <td>Canelones</td>
      <td>43</td>
    </tr>
  </tbody>
</table>
<p>425 rows × 3 columns</p>
</div>


