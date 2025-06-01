# Renaming and Combining

## Introduction
Sering kali data datang kepada kita dengan nama kolom, nama indeks, atau konvensi penamaan lain yang tidak kita sukai. Dalam hal ini, Anda akan belajar bagaimana menggunakan fungsi pandas untuk mengubah nama-nama entri yang tidak sesuai menjadi lebih baik.

Anda juga akan menjelajahi cara menggabungkan data dari beberapa DataFrame dan/atau Series.

## Renaming
Fungsi pertama yang akan kami perkenalkan di sini adalah rename(), yang memungkinkan Anda mengubah nama indeks dan/atau nama kolom. Sebagai contoh, untuk mengubah kolom poin dalam kumpulan data kita menjadi skor, kita akan melakukannya:


```python
import pandas as pd
pd.set_option('display.max_rows', 5)
reviews = pd.read_csv("../winemag-data-130k-v2.csv", index_col=0)
```


```python
reviews.rename(columns={'points': 'score'})
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>country</th>
      <th>description</th>
      <th>designation</th>
      <th>score</th>
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



rename() memungkinkan Anda mengganti nama indeks atau nilai kolom dengan menentukan parameter kata kunci indeks atau kolom. Fungsi ini mendukung berbagai format input, tetapi biasanya kamus Python adalah yang paling nyaman. Berikut ini adalah contoh penggunaannya untuk mengganti nama beberapa elemen indeks.


```python
reviews.rename(index={0: 'firstEntry', 1: 'secondEntry'})
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
      <th>firstEntry</th>
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
      <th>secondEntry</th>
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



Anda mungkin akan sering mengganti nama kolom, tetapi sangat jarang mengganti nilai indeks. Untuk itu, set_index() biasanya lebih mudah digunakan.

Baik indeks baris maupun indeks kolom dapat memiliki atribut nama sendiri. Metode rename_axis() dapat digunakan untuk mengubah nama-nama ini. Sebagai contoh:


```python
reviews.rename_axis("wines", axis='rows').rename_axis("fields", axis='columns')
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>fields</th>
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
    <tr>
      <th>wines</th>
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
      <th></th>
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



## Combining
Ketika melakukan operasi pada sebuah dataset, terkadang kita perlu menggabungkan DataFrame dan/atau Series yang berbeda dengan cara yang tidak sepele. Pandas memiliki tiga metode inti untuk melakukan hal ini. Dalam urutan kompleksitas yang semakin meningkat, metode-metode tersebut adalah concat(), join(), dan merge(). Sebagian besar dari apa yang bisa dilakukan oleh merge() juga bisa dilakukan secara lebih sederhana dengan join(), jadi kita akan mengabaikannya dan fokus pada dua fungsi pertama di sini.

Metode penggabungan yang paling sederhana adalah concat(). Diberikan sebuah daftar elemen, fungsi ini akan menggabungkan elemen-elemen tersebut di sepanjang sumbu.

Hal ini berguna ketika kita memiliki data dalam objek DataFrame atau Series yang berbeda namun memiliki field (kolom) yang sama. Salah satu contoh: kumpulan data Video YouTube, yang membagi data berdasarkan negara asal (misalnya Kanada dan Inggris, dalam contoh ini). Jika kita ingin mempelajari beberapa negara secara bersamaan, kita dapat menggunakan concat() untuk menggabungkannya:


```python
canadian_youtube = pd.read_csv("../CAvideos.csv")
british_youtube = pd.read_csv("../GBvideos.csv")

pd.concat([canadian_youtube, british_youtube])
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>video_id</th>
      <th>trending_date</th>
      <th>title</th>
      <th>channel_title</th>
      <th>category_id</th>
      <th>publish_time</th>
      <th>tags</th>
      <th>views</th>
      <th>likes</th>
      <th>dislikes</th>
      <th>comment_count</th>
      <th>thumbnail_link</th>
      <th>comments_disabled</th>
      <th>ratings_disabled</th>
      <th>video_error_or_removed</th>
      <th>description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>n1WpP7iowLc</td>
      <td>17.14.11</td>
      <td>Eminem - Walk On Water (Audio) ft. Beyoncé</td>
      <td>EminemVEVO</td>
      <td>10</td>
      <td>2017-11-10T17:00:03.000Z</td>
      <td>Eminem|"Walk"|"On"|"Water"|"Aftermath/Shady/In...</td>
      <td>17158579</td>
      <td>787425</td>
      <td>43420</td>
      <td>125882</td>
      <td>https://i.ytimg.com/vi/n1WpP7iowLc/default.jpg</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>Eminem's new track Walk on Water ft. Beyoncé i...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0dBIkQ4Mz1M</td>
      <td>17.14.11</td>
      <td>PLUSH - Bad Unboxing Fan Mail</td>
      <td>iDubbbzTV</td>
      <td>23</td>
      <td>2017-11-13T17:00:00.000Z</td>
      <td>plush|"bad unboxing"|"unboxing"|"fan mail"|"id...</td>
      <td>1014651</td>
      <td>127794</td>
      <td>1688</td>
      <td>13030</td>
      <td>https://i.ytimg.com/vi/0dBIkQ4Mz1M/default.jpg</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>STill got a lot of packages. Probably will las...</td>
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
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>38914</th>
      <td>-DRsfNObKIQ</td>
      <td>18.14.06</td>
      <td>Eleni Foureira - Fuego - Cyprus - LIVE - First...</td>
      <td>Eurovision Song Contest</td>
      <td>24</td>
      <td>2018-05-08T20:32:32.000Z</td>
      <td>Eurovision Song Contest|"2018"|"Lisbon"|"Cypru...</td>
      <td>14317515</td>
      <td>151870</td>
      <td>45875</td>
      <td>26766</td>
      <td>https://i.ytimg.com/vi/-DRsfNObKIQ/default.jpg</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>Eleni Foureira represented Cyprus at the first...</td>
    </tr>
    <tr>
      <th>38915</th>
      <td>4YFo4bdMO8Q</td>
      <td>18.14.06</td>
      <td>KYLE - Ikuyo feat.  2 Chainz &amp; Sophia Black [A...</td>
      <td>SuperDuperKyle</td>
      <td>10</td>
      <td>2018-05-11T04:06:35.000Z</td>
      <td>Kyle|"SuperDuperKyle"|"Ikuyo"|"2 Chainz"|"Soph...</td>
      <td>607552</td>
      <td>18271</td>
      <td>274</td>
      <td>1423</td>
      <td>https://i.ytimg.com/vi/4YFo4bdMO8Q/default.jpg</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>Debut album 'Light of Mine' out now: http://ky...</td>
    </tr>
  </tbody>
</table>
<p>79797 rows × 16 columns</p>
</div>



Penggabung paling menengah dalam hal kompleksitas adalah join(). join() memungkinkan Anda menggabungkan beberapa objek DataFrame yang berbeda yang memiliki indeks yang sama. Sebagai contoh, untuk menarik video yang kebetulan menjadi tren pada hari yang sama di Kanada dan Inggris, kita dapat melakukan hal berikut:


```python
left = canadian_youtube.set_index(['title', 'trending_date'])
right = british_youtube.set_index(['title', 'trending_date'])

left.join(right, lsuffix='_CAN', rsuffix='_UK')
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>video_id_CAN</th>
      <th>channel_title_CAN</th>
      <th>category_id_CAN</th>
      <th>publish_time_CAN</th>
      <th>tags_CAN</th>
      <th>views_CAN</th>
      <th>likes_CAN</th>
      <th>dislikes_CAN</th>
      <th>comment_count_CAN</th>
      <th>thumbnail_link_CAN</th>
      <th>...</th>
      <th>tags_UK</th>
      <th>views_UK</th>
      <th>likes_UK</th>
      <th>dislikes_UK</th>
      <th>comment_count_UK</th>
      <th>thumbnail_link_UK</th>
      <th>comments_disabled_UK</th>
      <th>ratings_disabled_UK</th>
      <th>video_error_or_removed_UK</th>
      <th>description_UK</th>
    </tr>
    <tr>
      <th>title</th>
      <th>trending_date</th>
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
      <th>Eminem - Walk On Water (Audio) ft. Beyoncé</th>
      <th>17.14.11</th>
      <td>n1WpP7iowLc</td>
      <td>EminemVEVO</td>
      <td>10</td>
      <td>2017-11-10T17:00:03.000Z</td>
      <td>Eminem|"Walk"|"On"|"Water"|"Aftermath/Shady/In...</td>
      <td>17158579</td>
      <td>787425</td>
      <td>43420</td>
      <td>125882</td>
      <td>https://i.ytimg.com/vi/n1WpP7iowLc/default.jpg</td>
      <td>...</td>
      <td>Eminem|"Walk"|"On"|"Water"|"Aftermath/Shady/In...</td>
      <td>17158579.0</td>
      <td>787420.0</td>
      <td>43420.0</td>
      <td>125882.0</td>
      <td>https://i.ytimg.com/vi/n1WpP7iowLc/default.jpg</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>Eminem's new track Walk on Water ft. Beyoncé i...</td>
    </tr>
    <tr>
      <th>PLUSH - Bad Unboxing Fan Mail</th>
      <th>17.14.11</th>
      <td>0dBIkQ4Mz1M</td>
      <td>iDubbbzTV</td>
      <td>23</td>
      <td>2017-11-13T17:00:00.000Z</td>
      <td>plush|"bad unboxing"|"unboxing"|"fan mail"|"id...</td>
      <td>1014651</td>
      <td>127794</td>
      <td>1688</td>
      <td>13030</td>
      <td>https://i.ytimg.com/vi/0dBIkQ4Mz1M/default.jpg</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
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
      <th>Trump Advisor Grovels To Trudeau</th>
      <th>18.14.06</th>
      <td>lbMKLzQ4cNQ</td>
      <td>The Young Turks</td>
      <td>25</td>
      <td>2018-06-13T04:00:05.000Z</td>
      <td>180612__TB02SorryExcuse|"News"|"Politics"|"The...</td>
      <td>115225</td>
      <td>2115</td>
      <td>182</td>
      <td>1672</td>
      <td>https://i.ytimg.com/vi/lbMKLzQ4cNQ/default.jpg</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>【完整版】遇到恐怖情人該怎麼辦？2018.06.13小明星大跟班</th>
      <th>18.14.06</th>
      <td>POTgw38-m58</td>
      <td>我愛小明星大跟班</td>
      <td>24</td>
      <td>2018-06-13T16:00:03.000Z</td>
      <td>吳宗憲|"吳姍儒"|"小明星大跟班"|"Sandy"|"Jacky wu"|"憲哥"|"中天...</td>
      <td>107392</td>
      <td>300</td>
      <td>62</td>
      <td>251</td>
      <td>https://i.ytimg.com/vi/POTgw38-m58/default.jpg</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>40900 rows × 28 columns</p>
</div>



Parameter lsuffix dan rsuffix diperlukan di sini karena data memiliki nama kolom yang sama di set data Inggris dan Kanada. Jika hal ini tidak benar (karena, katakanlah, kita telah mengganti namanya sebelumnya) kita tidak akan membutuhkannya.


```python

```
