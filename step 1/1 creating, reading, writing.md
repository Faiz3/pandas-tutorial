# Membuat, Membaca, dan Menulis
Anda tidak dapat bekerja dengan data jika tidak dapat membacanya. Mulailah di sini.

## Pengantar
Dalam kursus mikro ini, Anda akan mempelajari semua tentang panda, perpustakaan Python paling populer untuk analisis data.

Di sepanjang jalan, Anda akan menyelesaikan beberapa latihan langsung dengan data dunia nyata. Kami menyarankan Anda untuk mengerjakan latihan sambil membaca tutorial yang sesuai.

Untuk memulai latihan pertama, silakan klik di sini.

Dalam tutorial ini, Anda akan mempelajari cara membuat data Anda sendiri, serta cara bekerja dengan data yang sudah ada.



## Memulai
Untuk menggunakan pandas, Anda biasanya akan memulai dengan baris kode berikut.


```python
import pandas as pd
```

## Membuat data
Ada dua objek inti dalam pandas: DataFrame dan Series.

### DataFrame
DataFrame adalah sebuah tabel. Tabel ini berisi larik entri individual, yang masing-masing memiliki nilai tertentu. Setiap entri berhubungan dengan sebuah baris (atau record) dan kolom.

Sebagai contoh, perhatikan DataFrame sederhana berikut ini:


```python
pd.DataFrame({'Yes': [50, 21], 'No': [131, 2]})
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Yes</th>
      <th>No</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>50</td>
      <td>131</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>



Dalam contoh ini, entri "0, Tidak" memiliki nilai 131. Entri "0, Ya" memiliki nilai 50, dan seterusnya.

Entri DataFrame tidak terbatas pada bilangan bulat. Sebagai contoh, berikut adalah DataFrame yang nilainya berupa string:


```python
pd.DataFrame({'Bob': ['I liked it.', 'It was awful.'], 'Sue': ['Pretty good.', 'Bland.']})
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Bob</th>
      <th>Sue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>I liked it.</td>
      <td>Pretty good.</td>
    </tr>
    <tr>
      <th>1</th>
      <td>It was awful.</td>
      <td>Bland.</td>
    </tr>
  </tbody>
</table>
</div>



Kita menggunakan konstruktor `pd.DataFrame()` untuk menghasilkan objek-objek DataFrame. Sintaks untuk mendeklarasikan yang baru adalah sebuah kamus yang kuncinya adalah nama kolom (`Bob` dan `Sue` dalam contoh ini), dan nilai-nilainya adalah daftar entri. Ini adalah cara standar untuk membuat DataFrame baru, dan cara yang paling sering Anda temui.

Konstruktor dictionary-list memberikan nilai pada label kolom, tetapi hanya menggunakan hitungan menaik dari 0 (0, 1, 2, 3, ...) untuk label baris. Terkadang hal ini tidak masalah, namun seringkali kita ingin memberikan label-label ini sendiri.

Daftar label baris yang digunakan dalam sebuah DataFrame dikenal sebagai sebuah Index. Kita bisa memberikan nilai pada indeks dengan menggunakan parameter indeks dalam konstruktor kita:


```python
pd.DataFrame({'Bob': ['I liked it.', 'It was awful.'], 
              'Sue': ['Pretty good.', 'Bland.']},
             index=['Product A', 'Product B'])
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Bob</th>
      <th>Sue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Product A</th>
      <td>I liked it.</td>
      <td>Pretty good.</td>
    </tr>
    <tr>
      <th>Product B</th>
      <td>It was awful.</td>
      <td>Bland.</td>
    </tr>
  </tbody>
</table>
</div>



### Series
Sebaliknya, Series adalah urutan nilai data. Jika DataFrame adalah sebuah tabel, Series adalah sebuah daftar. Dan pada kenyataannya Anda dapat membuatnya dengan tidak lebih dari sebuah daftar:


```python
pd.Series([1, 2, 3, 4, 5])
```




    0    1
    1    2
    2    3
    3    4
    4    5
    dtype: int64



Pada dasarnya, sebuah Series adalah sebuah kolom tunggal dari sebuah DataFrame. Jadi, Anda dapat menetapkan label baris ke Series dengan cara yang sama seperti sebelumnya, menggunakan parameter indeks. Namun, Series tidak memiliki nama kolom, ia hanya memiliki satu nama keseluruhan:

Series dan DataFrame sangat erat kaitannya. Akan sangat membantu jika kita membayangkan sebuah DataFrame sebagai sekumpulan Series yang "direkatkan". Kita akan melihat lebih banyak tentang hal ini di bagian selanjutnya dari tutorial ini.

## Membaca file data
Mampu membuat DataFrame atau Seri secara manual sangat berguna. Namun, sebagian besar waktu, kita tidak akan benar-benar membuat data kita sendiri secara manual. Sebaliknya, kita akan bekerja dengan data yang sudah ada.

Data dapat disimpan dalam berbagai bentuk dan format. Sejauh ini yang paling dasar adalah file CSV yang sederhana. Ketika Anda membuka file CSV, Anda akan mendapatkan tampilan seperti ini:

```csv
Product A,Product B,Product C,
30,21,9,
35,34,1,
41,11,11
```

Jadi, file CSV adalah tabel nilai yang dipisahkan oleh koma. Oleh karena itu namanya: "Nilai yang Dipisahkan dengan Koma(Comma-Separated Values)", atau CSV.

Sekarang mari kita sisihkan dataset mainan kita dan melihat seperti apa dataset yang sebenarnya ketika kita membacanya ke dalam DataFrame. Kita akan menggunakan fungsi pd.read_csv() untuk membaca data ke dalam DataFrame. Hal ini berjalan seperti ini:


```python
import pandas as pd
wine_reviews = pd.read_csv("../winemag-data-130k-v2.csv")
```

Kita dapat menggunakan atribut shape untuk memeriksa seberapa besar DataFrame yang dihasilkan:


```python
wine_reviews.shape
```




    (129971, 14)



Jadi DataFrame baru kami memiliki 130.000 catatan yang terbagi dalam 14 kolom yang berbeda. Itu hampir 2 juta entri!

Kita dapat memeriksa isi dari DataFrame yang dihasilkan dengan menggunakan perintah head(), yang mengambil lima baris pertama:


```python
wine_reviews.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
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
      <th>0</th>
      <td>0</td>
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
      <td>1</td>
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
      <th>2</th>
      <td>2</td>
      <td>US</td>
      <td>Tart and snappy, the flavors of lime flesh and...</td>
      <td>NaN</td>
      <td>87</td>
      <td>14.0</td>
      <td>Oregon</td>
      <td>Willamette Valley</td>
      <td>Willamette Valley</td>
      <td>Paul Gregutt</td>
      <td>@paulgwine</td>
      <td>Rainstorm 2013 Pinot Gris (Willamette Valley)</td>
      <td>Pinot Gris</td>
      <td>Rainstorm</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>US</td>
      <td>Pineapple rind, lemon pith and orange blossom ...</td>
      <td>Reserve Late Harvest</td>
      <td>87</td>
      <td>13.0</td>
      <td>Michigan</td>
      <td>Lake Michigan Shore</td>
      <td>NaN</td>
      <td>Alexander Peartree</td>
      <td>NaN</td>
      <td>St. Julian 2013 Reserve Late Harvest Riesling ...</td>
      <td>Riesling</td>
      <td>St. Julian</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>US</td>
      <td>Much like the regular bottling from 2012, this...</td>
      <td>Vintner's Reserve Wild Child Block</td>
      <td>87</td>
      <td>65.0</td>
      <td>Oregon</td>
      <td>Willamette Valley</td>
      <td>Willamette Valley</td>
      <td>Paul Gregutt</td>
      <td>@paulgwine</td>
      <td>Sweet Cheeks 2012 Vintner's Reserve Wild Child...</td>
      <td>Pinot Noir</td>
      <td>Sweet Cheeks</td>
    </tr>
  </tbody>
</table>
</div>



Fungsi `pd.read_csv()` sangat lengkap, dengan lebih dari 30 parameter opsional yang dapat Anda tentukan. Sebagai contoh, Anda dapat melihat dalam dataset ini bahwa file CSV memiliki indeks bawaan, yang tidak dapat ditangkap oleh pandas secara otomatis. Untuk membuat pandas menggunakan kolom tersebut untuk indeks (daripada membuat indeks baru dari awal), kita dapat menentukan `index_col`.


```python
wine_reviews = pd.read_csv("../winemag-data-130k-v2.csv", index_col=0)
wine_reviews.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
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
      <th>2</th>
      <td>US</td>
      <td>Tart and snappy, the flavors of lime flesh and...</td>
      <td>NaN</td>
      <td>87</td>
      <td>14.0</td>
      <td>Oregon</td>
      <td>Willamette Valley</td>
      <td>Willamette Valley</td>
      <td>Paul Gregutt</td>
      <td>@paulgwine</td>
      <td>Rainstorm 2013 Pinot Gris (Willamette Valley)</td>
      <td>Pinot Gris</td>
      <td>Rainstorm</td>
    </tr>
    <tr>
      <th>3</th>
      <td>US</td>
      <td>Pineapple rind, lemon pith and orange blossom ...</td>
      <td>Reserve Late Harvest</td>
      <td>87</td>
      <td>13.0</td>
      <td>Michigan</td>
      <td>Lake Michigan Shore</td>
      <td>NaN</td>
      <td>Alexander Peartree</td>
      <td>NaN</td>
      <td>St. Julian 2013 Reserve Late Harvest Riesling ...</td>
      <td>Riesling</td>
      <td>St. Julian</td>
    </tr>
    <tr>
      <th>4</th>
      <td>US</td>
      <td>Much like the regular bottling from 2012, this...</td>
      <td>Vintner's Reserve Wild Child Block</td>
      <td>87</td>
      <td>65.0</td>
      <td>Oregon</td>
      <td>Willamette Valley</td>
      <td>Willamette Valley</td>
      <td>Paul Gregutt</td>
      <td>@paulgwine</td>
      <td>Sweet Cheeks 2012 Vintner's Reserve Wild Child...</td>
      <td>Pinot Noir</td>
      <td>Sweet Cheeks</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
