# Introduction

Jalankan sel berikut ini untuk memuat data Anda dan beberapa fungsi utilitas.


```python
import pandas as pd

reviews = pd.read_csv("../winemag-data-130k-v2.csv", index_col=0)
```

# Exercises

Lihat beberapa baris pertama dari data Anda dengan menjalankan sel di bawah ini:


```python
reviews.head()
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



## 1.
`region_1` dan `region_2` adalah nama yang kurang informatif untuk kolom lokal di dalam set data. Buat salinan `reviews` dengan kolom-kolom ini masing-masing diganti namanya menjadi `region` dan `locale`.


```python
reviews.rename(columns={'region_1': 'region', 'region_2': 'locale'})
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
      <th>region</th>
      <th>locale</th>
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
<p>129971 rows × 13 columns</p>
</div>



## 2.
Tetapkan nama indeks dalam set data ke `wines`.


```python
reindexed = reviews.rename_axis("wines", axis='rows').rename_axis("fields", axis='columns')
```


```python
reindexed
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
<p>129971 rows × 13 columns</p>
</div>



## 3.
Dataset [Things on Reddit](https://www.kaggle.com/residentmario/things-on-reddit/data) mencakup tautan produk dari pilihan forum peringkat teratas ("subreddits") di reddit.com. Jalankan sel di bawah ini untuk memuat DataFrame produk yang disebutkan di subreddit */r/gaming* dan DataFrame lain untuk produk yang disebutkan di subreddit *r//movies*.


```python
gaming_products = pd.read_csv("../gaming.csv")
gaming_products['subreddit'] = "r/gaming"
movie_products = pd.read_csv("../movies.csv")
movie_products['subreddit'] = "r/movies"
```

Buat `DataFrame` dari produk yang disebutkan di *salah satu* subreddit.


```python
combined_products = pd.concat([gaming_products, movie_products])
```


```python
combined_products
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>category</th>
      <th>amazon_link</th>
      <th>total_mentions</th>
      <th>subreddit_mentions</th>
      <th>subreddit</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>BOOMco Halo Covenant Needler Blaster</td>
      <td>Toys &amp; Games</td>
      <td>https://www.amazon.com/BOOMco-Halo-Covenant-Ne...</td>
      <td>4.0</td>
      <td>4</td>
      <td>r/gaming</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Raspberry PI 3 Model B 1.2GHz 64-bit quad-core...</td>
      <td>Electronics</td>
      <td>https://www.amazon.com/Raspberry-Model-A1-2GHz...</td>
      <td>19.0</td>
      <td>3</td>
      <td>r/gaming</td>
    </tr>
    <tr>
      <th>2</th>
      <td>CanaKit 5V 2.5A Raspberry Pi 3 Power Supply / ...</td>
      <td>Electronics</td>
      <td>https://www.amazon.com/CanaKit-Raspberry-Suppl...</td>
      <td>7.0</td>
      <td>3</td>
      <td>r/gaming</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Panasonic K-KJ17MCA4BA Advanced Individual Cel...</td>
      <td>Electronics</td>
      <td>https://www.amazon.com/Panasonic-Advanced-Indi...</td>
      <td>29.0</td>
      <td>2</td>
      <td>r/gaming</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Mayflash GameCube Controller Adapter for Wii U...</td>
      <td>Electronics</td>
      <td>https://www.amazon.com/GameCube-Controller-Ada...</td>
      <td>24.0</td>
      <td>2</td>
      <td>r/gaming</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>298</th>
      <td>Welcome to Night Vale CD: A Novel</td>
      <td>Books</td>
      <td>https://www.amazon.com/Welcome-Night-Vale-CD-N...</td>
      <td>1.0</td>
      <td>1</td>
      <td>r/movies</td>
    </tr>
    <tr>
      <th>299</th>
      <td>Ran (StudioCanal Collection) [Blu-ray]</td>
      <td>Movies &amp; TV</td>
      <td>https://www.amazon.com/StudioCanal-Collection-...</td>
      <td>1.0</td>
      <td>1</td>
      <td>r/movies</td>
    </tr>
    <tr>
      <th>300</th>
      <td>The Art of John Alvin</td>
      <td>Books</td>
      <td>https://www.amazon.com/Art-John-Alvin-Andrea/d...</td>
      <td>1.0</td>
      <td>1</td>
      <td>r/movies</td>
    </tr>
    <tr>
      <th>301</th>
      <td>Apocalypto [Blu-ray]</td>
      <td>Movies &amp; TV</td>
      <td>https://www.amazon.com/Apocalypto-Blu-ray-Rudy...</td>
      <td>1.0</td>
      <td>1</td>
      <td>r/movies</td>
    </tr>
    <tr>
      <th>302</th>
      <td>Cinelinx: A Card Game for People Who Love Movi...</td>
      <td>Toys &amp; Games</td>
      <td>https://www.amazon.com/Cinelinx-Card-Game-Peop...</td>
      <td>1.0</td>
      <td>1</td>
      <td>r/movies</td>
    </tr>
  </tbody>
</table>
<p>796 rows × 6 columns</p>
</div>



## 4.
Kumpulan data [Database Angkat Besi](https://www.kaggle.com/open-powerlifting/powerlifting-database) di Kaggle meliputi satu tabel CSV untuk pertandingan angkat besi dan tabel terpisah untuk kompetitor angkat besi. Jalankan sel di bawah ini untuk memuat set data ini ke dalam dataframe:


```python
powerlifting_meets = pd.read_csv("../meets.csv")
powerlifting_competitors = pd.read_csv("../openpowerlifting.csv")
```


```python
powerlifting_meets.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>MeetID</th>
      <th>MeetPath</th>
      <th>Federation</th>
      <th>Date</th>
      <th>MeetCountry</th>
      <th>MeetState</th>
      <th>MeetTown</th>
      <th>MeetName</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>365strong/1601</td>
      <td>365Strong</td>
      <td>2016-10-29</td>
      <td>USA</td>
      <td>NC</td>
      <td>Charlotte</td>
      <td>2016 Junior &amp; Senior National Powerlifting Cha...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>365strong/1602</td>
      <td>365Strong</td>
      <td>2016-11-19</td>
      <td>USA</td>
      <td>MO</td>
      <td>Ozark</td>
      <td>Thanksgiving Powerlifting Classic</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>365strong/1603</td>
      <td>365Strong</td>
      <td>2016-07-09</td>
      <td>USA</td>
      <td>NC</td>
      <td>Charlotte</td>
      <td>Charlotte Europa Games</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>365strong/1604</td>
      <td>365Strong</td>
      <td>2016-06-11</td>
      <td>USA</td>
      <td>SC</td>
      <td>Rock Hill</td>
      <td>Carolina Cup Push Pull Challenge</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>365strong/1605</td>
      <td>365Strong</td>
      <td>2016-04-10</td>
      <td>USA</td>
      <td>SC</td>
      <td>Rock Hill</td>
      <td>Eastern USA Challenge</td>
    </tr>
  </tbody>
</table>
</div>




```python
powerlifting_competitors.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>MeetID</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Equipment</th>
      <th>Age</th>
      <th>Division</th>
      <th>BodyweightKg</th>
      <th>WeightClassKg</th>
      <th>Squat4Kg</th>
      <th>BestSquatKg</th>
      <th>Bench4Kg</th>
      <th>BestBenchKg</th>
      <th>Deadlift4Kg</th>
      <th>BestDeadliftKg</th>
      <th>TotalKg</th>
      <th>Place</th>
      <th>Wilks</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Angie Belk Terry</td>
      <td>F</td>
      <td>Wraps</td>
      <td>47.0</td>
      <td>Mst 45-49</td>
      <td>59.60</td>
      <td>60</td>
      <td>NaN</td>
      <td>47.63</td>
      <td>NaN</td>
      <td>20.41</td>
      <td>NaN</td>
      <td>70.31</td>
      <td>138.35</td>
      <td>1</td>
      <td>155.05</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>Dawn Bogart</td>
      <td>F</td>
      <td>Single-ply</td>
      <td>42.0</td>
      <td>Mst 40-44</td>
      <td>58.51</td>
      <td>60</td>
      <td>NaN</td>
      <td>142.88</td>
      <td>NaN</td>
      <td>95.25</td>
      <td>NaN</td>
      <td>163.29</td>
      <td>401.42</td>
      <td>1</td>
      <td>456.38</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>Dawn Bogart</td>
      <td>F</td>
      <td>Single-ply</td>
      <td>42.0</td>
      <td>Open Senior</td>
      <td>58.51</td>
      <td>60</td>
      <td>NaN</td>
      <td>142.88</td>
      <td>NaN</td>
      <td>95.25</td>
      <td>NaN</td>
      <td>163.29</td>
      <td>401.42</td>
      <td>1</td>
      <td>456.38</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>Dawn Bogart</td>
      <td>F</td>
      <td>Raw</td>
      <td>42.0</td>
      <td>Open Senior</td>
      <td>58.51</td>
      <td>60</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>95.25</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>95.25</td>
      <td>1</td>
      <td>108.29</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>Destiny Dula</td>
      <td>F</td>
      <td>Raw</td>
      <td>18.0</td>
      <td>Teen 18-19</td>
      <td>63.68</td>
      <td>67.5</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>31.75</td>
      <td>NaN</td>
      <td>90.72</td>
      <td>122.47</td>
      <td>1</td>
      <td>130.47</td>
    </tr>
  </tbody>
</table>
</div>



Kedua tabel tersebut menyertakan referensi ke `MeetID`, sebuah kunci unik untuk setiap pertemuan (kompetisi) yang ada di dalam database. Dengan menggunakan ini, buatlah kumpulan data yang menggabungkan kedua tabel menjadi satu.


```python
powerlifting_combined = powerlifting_meets.set_index('MeetID').join(powerlifting_competitors.set_index('MeetID'))
```


```python
powerlifting_combined
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>MeetPath</th>
      <th>Federation</th>
      <th>Date</th>
      <th>MeetCountry</th>
      <th>MeetState</th>
      <th>MeetTown</th>
      <th>MeetName</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Equipment</th>
      <th>...</th>
      <th>WeightClassKg</th>
      <th>Squat4Kg</th>
      <th>BestSquatKg</th>
      <th>Bench4Kg</th>
      <th>BestBenchKg</th>
      <th>Deadlift4Kg</th>
      <th>BestDeadliftKg</th>
      <th>TotalKg</th>
      <th>Place</th>
      <th>Wilks</th>
    </tr>
    <tr>
      <th>MeetID</th>
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
      <th>0</th>
      <td>365strong/1601</td>
      <td>365Strong</td>
      <td>2016-10-29</td>
      <td>USA</td>
      <td>NC</td>
      <td>Charlotte</td>
      <td>2016 Junior &amp; Senior National Powerlifting Cha...</td>
      <td>Angie Belk Terry</td>
      <td>F</td>
      <td>Wraps</td>
      <td>...</td>
      <td>60</td>
      <td>NaN</td>
      <td>47.63</td>
      <td>NaN</td>
      <td>20.41</td>
      <td>NaN</td>
      <td>70.31</td>
      <td>138.35</td>
      <td>1</td>
      <td>155.05</td>
    </tr>
    <tr>
      <th>0</th>
      <td>365strong/1601</td>
      <td>365Strong</td>
      <td>2016-10-29</td>
      <td>USA</td>
      <td>NC</td>
      <td>Charlotte</td>
      <td>2016 Junior &amp; Senior National Powerlifting Cha...</td>
      <td>Dawn Bogart</td>
      <td>F</td>
      <td>Single-ply</td>
      <td>...</td>
      <td>60</td>
      <td>NaN</td>
      <td>142.88</td>
      <td>NaN</td>
      <td>95.25</td>
      <td>NaN</td>
      <td>163.29</td>
      <td>401.42</td>
      <td>1</td>
      <td>456.38</td>
    </tr>
    <tr>
      <th>0</th>
      <td>365strong/1601</td>
      <td>365Strong</td>
      <td>2016-10-29</td>
      <td>USA</td>
      <td>NC</td>
      <td>Charlotte</td>
      <td>2016 Junior &amp; Senior National Powerlifting Cha...</td>
      <td>Dawn Bogart</td>
      <td>F</td>
      <td>Single-ply</td>
      <td>...</td>
      <td>60</td>
      <td>NaN</td>
      <td>142.88</td>
      <td>NaN</td>
      <td>95.25</td>
      <td>NaN</td>
      <td>163.29</td>
      <td>401.42</td>
      <td>1</td>
      <td>456.38</td>
    </tr>
    <tr>
      <th>0</th>
      <td>365strong/1601</td>
      <td>365Strong</td>
      <td>2016-10-29</td>
      <td>USA</td>
      <td>NC</td>
      <td>Charlotte</td>
      <td>2016 Junior &amp; Senior National Powerlifting Cha...</td>
      <td>Dawn Bogart</td>
      <td>F</td>
      <td>Raw</td>
      <td>...</td>
      <td>60</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>95.25</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>95.25</td>
      <td>1</td>
      <td>108.29</td>
    </tr>
    <tr>
      <th>0</th>
      <td>365strong/1601</td>
      <td>365Strong</td>
      <td>2016-10-29</td>
      <td>USA</td>
      <td>NC</td>
      <td>Charlotte</td>
      <td>2016 Junior &amp; Senior National Powerlifting Cha...</td>
      <td>Destiny Dula</td>
      <td>F</td>
      <td>Raw</td>
      <td>...</td>
      <td>67.5</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>31.75</td>
      <td>NaN</td>
      <td>90.72</td>
      <td>122.47</td>
      <td>1</td>
      <td>130.47</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>8481</th>
      <td>xpc/2017-finals</td>
      <td>XPC</td>
      <td>2017-03-03</td>
      <td>USA</td>
      <td>OH</td>
      <td>Columbus</td>
      <td>2017 XPC Finals</td>
      <td>William Barabas</td>
      <td>M</td>
      <td>Multi-ply</td>
      <td>...</td>
      <td>125</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>347.50</td>
      <td>347.50</td>
      <td>2</td>
      <td>202.60</td>
    </tr>
    <tr>
      <th>8481</th>
      <td>xpc/2017-finals</td>
      <td>XPC</td>
      <td>2017-03-03</td>
      <td>USA</td>
      <td>OH</td>
      <td>Columbus</td>
      <td>2017 XPC Finals</td>
      <td>Justin Zottl</td>
      <td>M</td>
      <td>Multi-ply</td>
      <td>...</td>
      <td>125</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>322.50</td>
      <td>322.50</td>
      <td>3</td>
      <td>185.77</td>
    </tr>
    <tr>
      <th>8481</th>
      <td>xpc/2017-finals</td>
      <td>XPC</td>
      <td>2017-03-03</td>
      <td>USA</td>
      <td>OH</td>
      <td>Columbus</td>
      <td>2017 XPC Finals</td>
      <td>Jake Anderson</td>
      <td>M</td>
      <td>Multi-ply</td>
      <td>...</td>
      <td>125</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>367.50</td>
      <td>367.50</td>
      <td>1</td>
      <td>211.17</td>
    </tr>
    <tr>
      <th>8481</th>
      <td>xpc/2017-finals</td>
      <td>XPC</td>
      <td>2017-03-03</td>
      <td>USA</td>
      <td>OH</td>
      <td>Columbus</td>
      <td>2017 XPC Finals</td>
      <td>Jeff Bumanglag</td>
      <td>M</td>
      <td>Multi-ply</td>
      <td>...</td>
      <td>140</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>320.00</td>
      <td>320.00</td>
      <td>3</td>
      <td>181.85</td>
    </tr>
    <tr>
      <th>8481</th>
      <td>xpc/2017-finals</td>
      <td>XPC</td>
      <td>2017-03-03</td>
      <td>USA</td>
      <td>OH</td>
      <td>Columbus</td>
      <td>2017 XPC Finals</td>
      <td>Shane Hammock</td>
      <td>M</td>
      <td>Multi-ply</td>
      <td>...</td>
      <td>140</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>362.50</td>
      <td>362.50</td>
      <td>2</td>
      <td>205.18</td>
    </tr>
  </tbody>
</table>
<p>386414 rows × 23 columns</p>
</div>




```python

```
