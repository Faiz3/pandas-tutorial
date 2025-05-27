# pengantar
Memilih nilai tertentu dari DataFrame atau Series pandas untuk dikerjakan adalah langkah implisit dalam hampir semua operasi data yang akan Anda jalankan, jadi salah satu hal pertama yang perlu Anda pelajari dalam bekerja dengan data di Python adalah cara memilih titik data yang relevan bagi Anda dengan cepat dan efektif.




```python
import pandas as pd
reviews = pd.read_csv("../winemag-data-130k-v2.csv", index_col=0)
pd.set_option('display.max_rows', 5)
```

# Pengakses asli
Objek-objek asli Python menyediakan cara yang baik untuk mengindeks data. Pandas membawa semua ini, yang membantu membuatnya mudah untuk memulai.

Perhatikan DataFrame ini:


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



Dalam Python, kita dapat mengakses properti sebuah objek dengan mengaksesnya sebagai atribut. Objek buku, misalnya, mungkin memiliki properti judul, yang dapat kita akses dengan memanggil book.title. Kolom dalam DataFrame pandas bekerja dengan cara yang hampir sama.

Oleh karena itu, untuk mengakses properti negara dari ulasan dapat kita gunakan:


```python
reviews.country
```




    0            Italy
    1         Portugal
                ...   
    129969      France
    129970      France
    Name: country, Length: 129971, dtype: object



Jika kita memiliki kamus Python, kita dapat mengakses nilai-nilainya dengan menggunakan operator pengindeksan ([]). Kita dapat melakukan hal yang sama dengan kolom dalam DataFrame:


```python
reviews['country']
```




    0            Italy
    1         Portugal
                ...   
    129969      France
    129970      France
    Name: country, Length: 129971, dtype: object



Ini adalah dua cara untuk memilih Seri tertentu dari DataFrame. Tidak satu pun dari keduanya yang lebih atau kurang valid secara sintaksis daripada yang lain, tetapi operator pengindeksan [] memiliki keuntungan bahwa ia dapat menangani nama kolom dengan karakter yang dicadangkan di dalamnya (mis. jika kita memiliki kolom pemeliharaan negara, reviews.country providence tidak akan berfungsi).

Bukankah rangkaian panda terlihat seperti sebuah kamus yang mewah? Memang seperti itu, jadi tidak mengherankan jika untuk menelusuri satu nilai tertentu, kita hanya perlu menggunakan operator pengindeksan [] sekali lagi:


```python
reviews['country'][0]
```




    'Italy'



# Indexing in pandas
The indexing operator and attribute selection are nice because they work just like they do in the rest of the Python ecosystem. As a novice, this makes them easy to pick up and use. However, pandas has its own accessor operators, loc and iloc. For more advanced operations, these are the ones you're supposed to be using.

# Pengindeksan di pandas
Operator pengindeksan dan pemilihan atribut sangat bagus karena mereka bekerja seperti yang mereka lakukan di ekosistem Python lainnya. Sebagai seorang pemula, hal ini membuat mereka mudah untuk dipahami dan digunakan. Namun, pandas memiliki operator pengaksesnya sendiri, yaitu loc dan iloc. Untuk operasi yang lebih canggih, kedua operator inilah yang seharusnya Anda gunakan.

## Seleksi berbasis indeks
Pengindeksan pandas bekerja dengan salah satu dari dua paradigma. Yang pertama adalah seleksi berbasis indeks: memilih data berdasarkan posisi numeriknya di dalam data. iloc mengikuti paradigma ini.

Untuk memilih baris pertama dari data dalam sebuah DataFrame, kita bisa menggunakan yang berikut ini:


```python
reviews.iloc[0]
```




    country                                                    Italy
    description    Aromas include tropical fruit, broom, brimston...
                                         ...                        
    variety                                              White Blend
    winery                                                   Nicosia
    Name: 0, Length: 13, dtype: object



Baik loc dan iloc adalah baris-pertama, kolom-kedua. Ini adalah kebalikan dari apa yang kita lakukan di Python asli, yaitu kolom-pertama, baris-kedua.

Ini berarti sedikit lebih mudah untuk mengambil baris, dan sedikit lebih sulit untuk mengambil kolom. Untuk mendapatkan kolom dengan iloc, kita dapat melakukan hal berikut:


```python
reviews.iloc[:, 0]
```




    0            Italy
    1         Portugal
                ...   
    129969      France
    129970      France
    Name: country, Length: 129971, dtype: object



Dengan sendirinya, operator :, yang juga berasal dari bahasa pemrograman Python asli, berarti "semuanya". Namun, jika dikombinasikan dengan penyeleksi lain, operator ini dapat digunakan untuk menunjukkan rentang nilai. Misalnya, untuk memilih kolom negara hanya dari baris pertama, kedua, dan ketiga, kita bisa melakukannya:


```python
reviews.iloc[:3, 0]
```




    0       Italy
    1    Portugal
    2          US
    Name: country, dtype: object



Atau, untuk memilih entri kedua dan ketiga saja, kami akan melakukannya:


```python
reviews.iloc[1:3, 0]
```




    1    Portugal
    2          US
    Name: country, dtype: object



Anda juga dapat melewatkan daftar:


```python
reviews.iloc[[0, 1, 2], 0]
```




    0       Italy
    1    Portugal
    2          US
    Name: country, dtype: object



Terakhir, perlu diketahui bahwa angka negatif dapat digunakan dalam seleksi. Ini akan mulai menghitung maju dari akhir nilai. Jadi, sebagai contoh, berikut ini adalah lima elemen terakhir dari kumpulan data.


```python
reviews.iloc[-5:]
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
      <th>129966</th>
      <td>Germany</td>
      <td>Notes of honeysuckle and cantaloupe sweeten th...</td>
      <td>Brauneberger Juffer-Sonnenuhr Spätlese</td>
      <td>90</td>
      <td>28.0</td>
      <td>Mosel</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Anna Lee C. Iijima</td>
      <td>NaN</td>
      <td>Dr. H. Thanisch (Erben Müller-Burggraef) 2013 ...</td>
      <td>Riesling</td>
      <td>Dr. H. Thanisch (Erben Müller-Burggraef)</td>
    </tr>
    <tr>
      <th>129967</th>
      <td>US</td>
      <td>Citation is given as much as a decade of bottl...</td>
      <td>NaN</td>
      <td>90</td>
      <td>75.0</td>
      <td>Oregon</td>
      <td>Oregon</td>
      <td>Oregon Other</td>
      <td>Paul Gregutt</td>
      <td>@paulgwine</td>
      <td>Citation 2004 Pinot Noir (Oregon)</td>
      <td>Pinot Noir</td>
      <td>Citation</td>
    </tr>
    <tr>
      <th>129968</th>
      <td>France</td>
      <td>Well-drained gravel soil gives this wine its c...</td>
      <td>Kritt</td>
      <td>90</td>
      <td>30.0</td>
      <td>Alsace</td>
      <td>Alsace</td>
      <td>NaN</td>
      <td>Roger Voss</td>
      <td>@vossroger</td>
      <td>Domaine Gresser 2013 Kritt Gewurztraminer (Als...</td>
      <td>Gewürztraminer</td>
      <td>Domaine Gresser</td>
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
</div>



## Seleksi berbasis label¶
Paradigma kedua untuk pemilihan atribut adalah paradigma yang diikuti oleh operator loc: pemilihan berbasis label. Dalam paradigma ini, yang penting adalah nilai indeks data, bukan posisinya.

Sebagai contoh, untuk mendapatkan entri pertama dalam ulasan, kita akan melakukan hal berikut:


```python
reviews.loc[0, 'country']
```




    'Italy'



iloc secara konseptual lebih sederhana daripada loc karena mengabaikan indeks dataset. Ketika kita menggunakan iloc, kita memperlakukan dataset seperti sebuah matriks besar (daftar daftar), yang harus diindeks berdasarkan posisinya. loc, sebaliknya, menggunakan informasi dalam indeks untuk melakukan tugasnya. Karena dataset Anda biasanya memiliki indeks yang berarti, biasanya lebih mudah untuk melakukan sesuatu dengan menggunakan loc. Sebagai contoh, berikut adalah satu operasi yang jauh lebih mudah menggunakan loc:


```python
reviews.loc[:, ['taster_name', 'taster_twitter_handle', 'points']]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>taster_name</th>
      <th>taster_twitter_handle</th>
      <th>points</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Kerin O’Keefe</td>
      <td>@kerinokeefe</td>
      <td>87</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Roger Voss</td>
      <td>@vossroger</td>
      <td>87</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>129969</th>
      <td>Roger Voss</td>
      <td>@vossroger</td>
      <td>90</td>
    </tr>
    <tr>
      <th>129970</th>
      <td>Roger Voss</td>
      <td>@vossroger</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
<p>129971 rows × 3 columns</p>
</div>



## Memilih antara loc dan iloc
Ketika memilih atau bertransisi antara loc dan iloc, ada satu hal yang perlu diingat, yaitu bahwa kedua metode ini menggunakan skema pengindeksan yang sedikit berbeda.

iloc menggunakan skema pengindeksan stdlib Python, di mana elemen pertama dari suatu rentang disertakan dan elemen terakhir tidak disertakan. Jadi 0:10 akan memilih entri 0,...,9. Sementara itu, loc mengindeks secara inklusif. Jadi 0:10 akan memilih entri 0,...,10.

Mengapa ada perubahan? Ingatlah bahwa loc dapat mengindeks semua tipe stdlib: string, misalnya. Jika kita memiliki sebuah DataFrame dengan nilai indeks Apples,..., Potatoes,..., dan kita ingin memilih "semua pilihan buah menurut abjad antara Apples dan Potatoes", maka akan jauh lebih mudah untuk mengindeks df.loc['Apples':'Potatoes'] dibandingkan dengan mengindeks sesuatu seperti df.loc['Apples', 'Potatoet'] (t muncul setelah s pada abjad).

Hal ini sangat membingungkan ketika indeks DataFrame adalah daftar numerik sederhana, misalnya 0,...,1000. Dalam kasus ini df.iloc[0:1000] akan mengembalikan 1000 entri, sementara df.loc[0:1000] mengembalikan 1001 entri! Untuk mendapatkan 1000 elemen menggunakan loc, Anda harus turun satu tingkat lebih rendah dan meminta df.loc[0:999].

Jika tidak, semantik dari penggunaan loc sama dengan yang digunakan untuk iloc.

# Memanipulasi indeks¶
Seleksi berbasis label mendapatkan kekuatannya dari label dalam indeks. Yang penting, indeks yang kita gunakan tidak dapat diubah. Kita dapat memanipulasi indeks dengan cara apa pun yang kita inginkan.

Metode set_index() dapat digunakan untuk melakukan pekerjaan tersebut. Berikut adalah apa yang terjadi ketika kita set_index ke bidang judul:


```python
reviews.set_index("title")
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
      <th>variety</th>
      <th>winery</th>
    </tr>
    <tr>
      <th>title</th>
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
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Nicosia 2013 Vulkà Bianco  (Etna)</th>
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
      <td>White Blend</td>
      <td>Nicosia</td>
    </tr>
    <tr>
      <th>Quinta dos Avidagos 2011 Avidagos Red (Douro)</th>
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
    </tr>
    <tr>
      <th>Domaine Marcel Deiss 2012 Pinot Gris (Alsace)</th>
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
      <td>Pinot Gris</td>
      <td>Domaine Marcel Deiss</td>
    </tr>
    <tr>
      <th>Domaine Schoffit 2012 Lieu-dit Harth Cuvée Caroline Gewurztraminer (Alsace)</th>
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
      <td>Gewürztraminer</td>
      <td>Domaine Schoffit</td>
    </tr>
  </tbody>
</table>
<p>129971 rows × 12 columns</p>
</div>



Ini berguna jika Anda dapat menghasilkan indeks untuk kumpulan data yang lebih baik daripada yang sekarang.

# Pemilihan bersyarat¶
Sejauh ini kita telah mengindeks berbagai langkah data, menggunakan properti struktural dari DataFrame itu sendiri. Namun, untuk melakukan hal-hal yang menarik dengan data, kita sering kali perlu mengajukan pertanyaan berdasarkan kondisi.

Sebagai contoh, misalkan kita tertarik secara khusus pada anggur yang lebih baik dari rata-rata yang diproduksi di Italia.

Kita bisa mulai dengan memeriksa apakah setiap anggur berasal dari Italia atau tidak:


```python
reviews.country == 'Italy'
```




    0          True
    1         False
              ...  
    129969    False
    129970    False
    Name: country, Length: 129971, dtype: bool



Operasi ini menghasilkan serangkaian boolean Benar/Salah berdasarkan negara dari setiap catatan. Hasil ini kemudian dapat digunakan di dalam loc untuk memilih data yang relevan:


```python
reviews.loc[reviews.country == 'Italy']
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
      <th>6</th>
      <td>Italy</td>
      <td>Here's a bright, informal red that opens with ...</td>
      <td>Belsito</td>
      <td>87</td>
      <td>16.0</td>
      <td>Sicily &amp; Sardinia</td>
      <td>Vittoria</td>
      <td>NaN</td>
      <td>Kerin O’Keefe</td>
      <td>@kerinokeefe</td>
      <td>Terre di Giurfo 2013 Belsito Frappato (Vittoria)</td>
      <td>Frappato</td>
      <td>Terre di Giurfo</td>
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
      <th>129961</th>
      <td>Italy</td>
      <td>Intense aromas of wild cherry, baking spice, t...</td>
      <td>NaN</td>
      <td>90</td>
      <td>30.0</td>
      <td>Sicily &amp; Sardinia</td>
      <td>Sicilia</td>
      <td>NaN</td>
      <td>Kerin O’Keefe</td>
      <td>@kerinokeefe</td>
      <td>COS 2013 Frappato (Sicilia)</td>
      <td>Frappato</td>
      <td>COS</td>
    </tr>
    <tr>
      <th>129962</th>
      <td>Italy</td>
      <td>Blackberry, cassis, grilled herb and toasted a...</td>
      <td>Sàgana Tenuta San Giacomo</td>
      <td>90</td>
      <td>40.0</td>
      <td>Sicily &amp; Sardinia</td>
      <td>Sicilia</td>
      <td>NaN</td>
      <td>Kerin O’Keefe</td>
      <td>@kerinokeefe</td>
      <td>Cusumano 2012 Sàgana Tenuta San Giacomo Nero d...</td>
      <td>Nero d'Avola</td>
      <td>Cusumano</td>
    </tr>
  </tbody>
</table>
<p>19540 rows × 13 columns</p>
</div>



DataFrame ini memiliki ~20.000 baris. Data aslinya memiliki ~130.000. Itu berarti sekitar 15% wine berasal dari Italia.

Kami juga ingin tahu mana yang lebih baik dari rata-rata. Wine ditinjau dalam skala 80 hingga 100 poin, jadi ini bisa berarti wine yang memperoleh setidaknya 90 poin.

Kita dapat menggunakan tanda ampersand (&) untuk menyatukan kedua pertanyaan tersebut:


```python
reviews.loc[(reviews.country == 'Italy') & (reviews.points >= 90)]
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
      <th>120</th>
      <td>Italy</td>
      <td>Slightly backward, particularly given the vint...</td>
      <td>Bricco Rocche Prapó</td>
      <td>92</td>
      <td>70.0</td>
      <td>Piedmont</td>
      <td>Barolo</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Ceretto 2003 Bricco Rocche Prapó  (Barolo)</td>
      <td>Nebbiolo</td>
      <td>Ceretto</td>
    </tr>
    <tr>
      <th>130</th>
      <td>Italy</td>
      <td>At the first it was quite muted and subdued, b...</td>
      <td>Bricco Rocche Brunate</td>
      <td>91</td>
      <td>70.0</td>
      <td>Piedmont</td>
      <td>Barolo</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Ceretto 2003 Bricco Rocche Brunate  (Barolo)</td>
      <td>Nebbiolo</td>
      <td>Ceretto</td>
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
      <th>129961</th>
      <td>Italy</td>
      <td>Intense aromas of wild cherry, baking spice, t...</td>
      <td>NaN</td>
      <td>90</td>
      <td>30.0</td>
      <td>Sicily &amp; Sardinia</td>
      <td>Sicilia</td>
      <td>NaN</td>
      <td>Kerin O’Keefe</td>
      <td>@kerinokeefe</td>
      <td>COS 2013 Frappato (Sicilia)</td>
      <td>Frappato</td>
      <td>COS</td>
    </tr>
    <tr>
      <th>129962</th>
      <td>Italy</td>
      <td>Blackberry, cassis, grilled herb and toasted a...</td>
      <td>Sàgana Tenuta San Giacomo</td>
      <td>90</td>
      <td>40.0</td>
      <td>Sicily &amp; Sardinia</td>
      <td>Sicilia</td>
      <td>NaN</td>
      <td>Kerin O’Keefe</td>
      <td>@kerinokeefe</td>
      <td>Cusumano 2012 Sàgana Tenuta San Giacomo Nero d...</td>
      <td>Nero d'Avola</td>
      <td>Cusumano</td>
    </tr>
  </tbody>
</table>
<p>6648 rows × 13 columns</p>
</div>



Misalkan kita akan membeli wine apa pun yang dibuat di Italia atau yang memiliki kualitas di atas rata-rata. Untuk ini, kita menggunakan pipa (|):


```python
reviews.loc[(reviews.country == 'Italy') | (reviews.points >= 90)]
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
      <th>6</th>
      <td>Italy</td>
      <td>Here's a bright, informal red that opens with ...</td>
      <td>Belsito</td>
      <td>87</td>
      <td>16.0</td>
      <td>Sicily &amp; Sardinia</td>
      <td>Vittoria</td>
      <td>NaN</td>
      <td>Kerin O’Keefe</td>
      <td>@kerinokeefe</td>
      <td>Terre di Giurfo 2013 Belsito Frappato (Vittoria)</td>
      <td>Frappato</td>
      <td>Terre di Giurfo</td>
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
<p>61937 rows × 13 columns</p>
</div>



Pandas dilengkapi dengan beberapa selektor bersyarat bawaan, dua di antaranya akan kami soroti di sini.

Yang pertama adalah isin. isin memungkinkan Anda memilih data yang nilainya "ada di dalam" daftar nilai. Sebagai contoh, berikut ini cara menggunakannya untuk memilih anggur yang hanya berasal dari Italia atau Prancis:


```python
reviews.loc[reviews.country.isin(['Italy', 'France'])]
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
      <th>6</th>
      <td>Italy</td>
      <td>Here's a bright, informal red that opens with ...</td>
      <td>Belsito</td>
      <td>87</td>
      <td>16.0</td>
      <td>Sicily &amp; Sardinia</td>
      <td>Vittoria</td>
      <td>NaN</td>
      <td>Kerin O’Keefe</td>
      <td>@kerinokeefe</td>
      <td>Terre di Giurfo 2013 Belsito Frappato (Vittoria)</td>
      <td>Frappato</td>
      <td>Terre di Giurfo</td>
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
<p>41633 rows × 13 columns</p>
</div>



Yang kedua adalah isnull (dan pendampingnya notnull). Metode-metode ini memungkinkan Anda menyorot nilai yang (atau tidak) kosong (NaN). Misalnya, untuk menyaring wine yang tidak memiliki label harga dalam kumpulan data, inilah yang akan kita lakukan:


```python
reviews.loc[reviews.price.notnull()]
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
<p>120975 rows × 13 columns</p>
</div>



# Assigning data¶
Sebaliknya, menugaskan data ke DataFrame sangatlah mudah. Anda dapat menetapkan nilai konstan:


```python
reviews['critic'] = 'everyone'
reviews['critic']
```




    0         everyone
    1         everyone
                ...   
    129969    everyone
    129970    everyone
    Name: critic, Length: 129971, dtype: object



Atau dengan nilai yang dapat diulang:


```python
reviews['index_backwards'] = range(len(reviews), 0, -1)
reviews['index_backwards']
```




    0         129971
    1         129970
               ...  
    129969         2
    129970         1
    Name: index_backwards, Length: 129971, dtype: int64




```python

```
