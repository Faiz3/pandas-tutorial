# Pendahuluan
Langkah pertama dalam sebagian besar proyek analisis data adalah membaca file data. Dalam latihan ini, Anda akan membuat objek Series dan DataFrame, baik secara manual maupun dengan membaca file data.

Jalankan sel kode di bawah ini untuk memuat pustaka yang Anda perlukan (termasuk kode untuk memeriksa jawaban Anda).


```python
import pandas as pd
pd.set_option('display.max_rows', 5)
```

## 1.

Pada sel di bawah ini, buatlah DataFrame `buah` yang terlihat seperti ini:

![](Ax3pp2A.png)


```python
# Kode Anda ada di sini. Buat sebuah dataframe yang sesuai dengan diagram di atas dan tetapkan ke variabel buah.
fruits = ___
```


```python
fruits
```

output:


<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Apple</th>
      <th>Bananas</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>30</td>
      <td>21</td>
    </tr>
  </tbody>
</table>
</div>



## 2.

Buatlah sebuah dataframe `fruit_sales` yang sesuai dengan diagram di bawah ini:

![](CHPn7ZF.png)


```python
fruit_sales = ___

fruit_sales
```

output:


<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Apples</th>
      <th>Bananas</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2017 Sales</th>
      <td>35</td>
      <td>21</td>
    </tr>
    <tr>
      <th>2018 Sales</th>
      <td>41</td>
      <td>34</td>
    </tr>
  </tbody>
</table>
</div>



## 3.

Membuat variabel `ingredients` dengan Series yang terlihat seperti:

```
Flour     4 cups
Milk       1 cup
Eggs     2 large
Spam       1 can
Name: Dinner, dtype: object
```


```python
ingredients = ___

ingredients
```
output:



    Flour     4 cups
    Milk      1 cups
    Eggs     2 large
    Spam       1 can
    Name: Dinnner, dtype: object



## 4.

Baca kumpulan data csv ulasan anggur berikut ke dalam DataFrame bernama `reviews`:

![](74RCZtU.png)

Jalur file ke file csv adalah `../input/wine-reviews/winemag-data_first150k.csv`. Beberapa baris pertama terlihat seperti:

```
,country,description,designation,points,price,province,region_1,region_2,variety,winery
0,US,"This tremendous 100% varietal wine[...]",Martha's Vineyard,96,235.0,California,Napa Valley,Napa,Cabernet Sauvignon,Heitz
1,Spain,"Ripe aromas of fig, blackberry and[...]",Carodorum Selección Especial Reserva,96,110.0,Northern Spain,Toro,,Tinta de Toro,Bodega Carmen Rodríguez
```


```python
reviews = ___

reviews
```

output:


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
      <th>variety</th>
      <th>winery</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>US</td>
      <td>This tremendous 100% varietal wine hails from ...</td>
      <td>Martha's Vineyard</td>
      <td>96</td>
      <td>235.0</td>
      <td>California</td>
      <td>Napa Valley</td>
      <td>Napa</td>
      <td>Cabernet Sauvignon</td>
      <td>Heitz</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Spain</td>
      <td>Ripe aromas of fig, blackberry and cassis are ...</td>
      <td>Carodorum Selección Especial Reserva</td>
      <td>96</td>
      <td>110.0</td>
      <td>Northern Spain</td>
      <td>Toro</td>
      <td>NaN</td>
      <td>Tinta de Toro</td>
      <td>Bodega Carmen Rodríguez</td>
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
    </tr>
    <tr>
      <th>150928</th>
      <td>France</td>
      <td>A perfect salmon shade, with scents of peaches...</td>
      <td>Grand Brut Rosé</td>
      <td>90</td>
      <td>52.0</td>
      <td>Champagne</td>
      <td>Champagne</td>
      <td>NaN</td>
      <td>Champagne Blend</td>
      <td>Gosset</td>
    </tr>
    <tr>
      <th>150929</th>
      <td>Italy</td>
      <td>More Pinot Grigios should taste like this. A r...</td>
      <td>NaN</td>
      <td>90</td>
      <td>15.0</td>
      <td>Northeastern Italy</td>
      <td>Alto Adige</td>
      <td>NaN</td>
      <td>Pinot Grigio</td>
      <td>Alois Lageder</td>
    </tr>
  </tbody>
</table>
<p>150930 rows × 10 columns</p>
</div>



## 5.

Jalankan sel di bawah ini untuk membuat dan menampilkan DataFrame bernama `animals`:


```python
animals = ___
animals
```

output:


<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Cows</th>
      <th>Goats</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Year 1</th>
      <td>12</td>
      <td>22</td>
    </tr>
    <tr>
      <th>Year 2</th>
      <td>20</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>



Pada sel di bawah ini, tulis kode untuk menyimpan DataFrame ini ke disk sebagai file csv dengan nama `cows_and_goats.csv`.


```python
# Kode Anda ada di sini
animals.to_csv('cows_and_goats.csv')
```


```python

```
