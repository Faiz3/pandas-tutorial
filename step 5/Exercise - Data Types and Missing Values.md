# Exercise: Data Types and Missing Values

## Introduction

Jalankan sel berikut ini untuk memuat data Anda dan beberapa fungsi utilitas.


```python
import pandas as pd

reviews = pd.read_csv("../winemag-data-130k-v2.csv", index_col=0)
```

# Exercises

## 1.
Apa tipe data dari kolom `points` dalam kumpulan data?


```python
# Your code here
dtype = reviews.points.dtype
```


```python
dtype
```




    dtype('int64')



## 2. 
Buat Seri dari entri di kolom `points`, tetapi ubah entri menjadi string. Petunjuk: string adalah `str` dalam Python asli.


```python
point_strings = reviews.points.astype('str')
point_strings
```




    0         87
    1         87
    2         87
    3         87
    4         87
              ..
    129966    90
    129967    90
    129968    90
    129969    90
    129970    90
    Name: points, Length: 129971, dtype: object



## 3.
Terkadang kolom harga adalah nol. Berapa banyak ulasan dalam dataset yang tidak memiliki harga?


```python
missing_price_reviews = reviews[reviews.price.isnull()]
n_missing_prices = len(missing_price_reviews)
n_missing_prices
```




    8996



## 4.
Wilayah mana yang paling banyak memproduksi wine? Buat Series yang menghitung berapa kali setiap nilai muncul di bidang `region_1`. Kolom ini sering kali tidak memiliki data, jadi ganti nilai yang hilang dengan `unknown`. Urutkan dalam urutan menurun.  Output Anda akan terlihat seperti ini:

```
Unknown                    21247
Napa Valley                 4480
                           ...  
Bardolino Superiore            1
Primitivo del Tarantino        1
Name: region_1, Length: 1230, dtype: int64
```


```python
reviews_per_region = reviews.region_1.fillna('Unknown').value_counts().sort_values(ascending=False)
```


```python
reviews_per_region
```




    region_1
    Unknown                               21247
    Napa Valley                            4480
    Columbia Valley (WA)                   4124
    Russian River Valley                   3091
    California                             2629
                                          ...  
    Sonoma-Santa Barbara-Mendocino            1
    Sonoma County-Santa Barbara County        1
    Del Veneto                                1
    Bardolino Superiore                       1
    Paestum                                   1
    Name: count, Length: 1230, dtype: int64




```python

```
