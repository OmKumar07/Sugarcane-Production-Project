---
## Sugarcane Production Analysis
---

::: {#736ddc32-39eb-44ae-a054-16056d0f1ad8 .cell .code execution_count="98"}
``` python
import pandas as pd
import seaborn as sns
from matplotlib import pyplot as plt
```
:::

::: {#4675e2ca-8c03-4a24-a700-7f6315b287a7 .cell .code execution_count="185"}
``` python
df = pd.read_csv("List of Countries by Sugarcane Production.csv",index_col=0)
```
:::

::: {#d748b66c-ba2c-4002-8d21-adc6407cc0be .cell .code execution_count="187"}
``` python
df.shape
```

::: {.output .execute_result execution_count="187"}
    (103, 6)
:::
:::

::: {#792eb9c4-d05e-4fcc-983f-6120ca3e0c37 .cell .code execution_count="189"}
``` python
df.head()
```

::: {.output .execute_result execution_count="189"}
```{=html}
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
      <th>Country</th>
      <th>Continent</th>
      <th>Production (Tons)</th>
      <th>Production per Person (Kg)</th>
      <th>Acreage (Hectare)</th>
      <th>Yield (Kg / Hectare)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Brazil</td>
      <td>South America</td>
      <td>768.678.382</td>
      <td>3.668,531</td>
      <td>10.226.205</td>
      <td>75.167,5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>India</td>
      <td>Asia</td>
      <td>348.448.000</td>
      <td>260721</td>
      <td>4.950.000</td>
      <td>70.393,5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>China</td>
      <td>Asia</td>
      <td>123.059.739</td>
      <td>88287</td>
      <td>1.675.215</td>
      <td>73.459,1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Thailand</td>
      <td>Asia</td>
      <td>87.468.496</td>
      <td>1.264,303</td>
      <td>1.336.575</td>
      <td>65.442,2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Pakistan</td>
      <td>Asia</td>
      <td>65.450.704</td>
      <td>324219</td>
      <td>1.130.820</td>
      <td>57.879</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {#a8c0a028-1710-4516-a371-7824bd8b571e .cell .markdown}
# Data Cleaning
:::

::: {#2b8d1228-2520-4a24-8a94-7da55c8aecd4 .cell .code execution_count="192"}
``` python
df["Production (Tons)"] = df["Production (Tons)"].str.replace(".","")
df["Production per Person (Kg)"] = df["Production per Person (Kg)"].str.replace(".","").str.replace(",",".")
df["Acreage (Hectare)"] = df["Acreage (Hectare)"].str.replace(".","")
df["Yield (Kg / Hectare)"]= df["Yield (Kg / Hectare)"].str.replace(".","").str.replace(",",".")
```
:::

::: {#3cde1b8e-8407-4138-bc12-7c500939b3e2 .cell .code execution_count="194"}
``` python
df.head()
```

::: {.output .execute_result execution_count="194"}
```{=html}
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
      <th>Country</th>
      <th>Continent</th>
      <th>Production (Tons)</th>
      <th>Production per Person (Kg)</th>
      <th>Acreage (Hectare)</th>
      <th>Yield (Kg / Hectare)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Brazil</td>
      <td>South America</td>
      <td>768678382</td>
      <td>3668.531</td>
      <td>10226205</td>
      <td>75167.5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>India</td>
      <td>Asia</td>
      <td>348448000</td>
      <td>260721</td>
      <td>4950000</td>
      <td>70393.5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>China</td>
      <td>Asia</td>
      <td>123059739</td>
      <td>88287</td>
      <td>1675215</td>
      <td>73459.1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Thailand</td>
      <td>Asia</td>
      <td>87468496</td>
      <td>1264.303</td>
      <td>1336575</td>
      <td>65442.2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Pakistan</td>
      <td>Asia</td>
      <td>65450704</td>
      <td>324219</td>
      <td>1130820</td>
      <td>57879</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {#28c060ae-981d-4009-bfdc-ec0eb96b3705 .cell .code execution_count="196"}
``` python
df.rename(columns= {"Production (Tons)": "Production(Tons)"}, inplace = True)
df.rename(columns= {"Production per Person (Kg)": "Production_per_person(Kg)"}, inplace = True)
df.rename(columns= {"Acreage (Hectare)": "Acreage(Hectare)"}, inplace = True)
df.rename(columns= {"Yield (Kg / Hectare)": "Yield(Kg/Hectare)"}, inplace = True)
```
:::

::: {#b21108c3-4bc8-47f0-9821-323989778609 .cell .code execution_count="198"}
``` python
df.head()
```

::: {.output .execute_result execution_count="198"}
```{=html}
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
      <th>Country</th>
      <th>Continent</th>
      <th>Production(Tons)</th>
      <th>Production_per_person(Kg)</th>
      <th>Acreage(Hectare)</th>
      <th>Yield(Kg/Hectare)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Brazil</td>
      <td>South America</td>
      <td>768678382</td>
      <td>3668.531</td>
      <td>10226205</td>
      <td>75167.5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>India</td>
      <td>Asia</td>
      <td>348448000</td>
      <td>260721</td>
      <td>4950000</td>
      <td>70393.5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>China</td>
      <td>Asia</td>
      <td>123059739</td>
      <td>88287</td>
      <td>1675215</td>
      <td>73459.1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Thailand</td>
      <td>Asia</td>
      <td>87468496</td>
      <td>1264.303</td>
      <td>1336575</td>
      <td>65442.2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Pakistan</td>
      <td>Asia</td>
      <td>65450704</td>
      <td>324219</td>
      <td>1130820</td>
      <td>57879</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {#36c48c2c-8856-40a4-8812-e2eead9a7325 .cell .code execution_count="200"}
``` python
df.isna().sum()
```

::: {.output .execute_result execution_count="200"}
    Country                      0
    Continent                    0
    Production(Tons)             0
    Production_per_person(Kg)    0
    Acreage(Hectare)             1
    Yield(Kg/Hectare)            1
    dtype: int64
:::
:::

::: {#d8f1eb16-d5b3-4f7e-b515-3b8ccf2ef03d .cell .code execution_count="202"}
``` python
df[df["Acreage(Hectare)"].isnull()]
```

::: {.output .execute_result execution_count="202"}
```{=html}
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
      <th>Country</th>
      <th>Continent</th>
      <th>Production(Tons)</th>
      <th>Production_per_person(Kg)</th>
      <th>Acreage(Hectare)</th>
      <th>Yield(Kg/Hectare)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>99</th>
      <td>Djibouti</td>
      <td>Africa</td>
      <td>53</td>
      <td>51</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {#e70946e7-0308-4ec5-8556-592929bf3fc4 .cell .code execution_count="204"}
``` python
df = df.dropna().reset_index().drop("index", axis = 1)
```
:::

::: {#e0643f34-091c-4ecf-9e9a-8be718fa40d5 .cell .code execution_count="206"}
``` python
df
```

::: {.output .execute_result execution_count="206"}
```{=html}
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
      <th>Country</th>
      <th>Continent</th>
      <th>Production(Tons)</th>
      <th>Production_per_person(Kg)</th>
      <th>Acreage(Hectare)</th>
      <th>Yield(Kg/Hectare)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Brazil</td>
      <td>South America</td>
      <td>768678382</td>
      <td>3668.531</td>
      <td>10226205</td>
      <td>75167.5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>India</td>
      <td>Asia</td>
      <td>348448000</td>
      <td>260721</td>
      <td>4950000</td>
      <td>70393.5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>China</td>
      <td>Asia</td>
      <td>123059739</td>
      <td>88287</td>
      <td>1675215</td>
      <td>73459.1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Thailand</td>
      <td>Asia</td>
      <td>87468496</td>
      <td>1264.303</td>
      <td>1336575</td>
      <td>65442.2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Pakistan</td>
      <td>Asia</td>
      <td>65450704</td>
      <td>324219</td>
      <td>1130820</td>
      <td>57879</td>
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
      <th>97</th>
      <td>Spain</td>
      <td>Europe</td>
      <td>394</td>
      <td>8</td>
      <td>9</td>
      <td>43596.5</td>
    </tr>
    <tr>
      <th>98</th>
      <td>Lebanon</td>
      <td>Asia</td>
      <td>97</td>
      <td>16</td>
      <td>3</td>
      <td>28386.4</td>
    </tr>
    <tr>
      <th>99</th>
      <td>Singapore</td>
      <td>Asia</td>
      <td>50</td>
      <td>9</td>
      <td>2</td>
      <td>25</td>
    </tr>
    <tr>
      <th>100</th>
      <td>Samoa</td>
      <td>Oceania</td>
      <td>12</td>
      <td>6</td>
      <td>1</td>
      <td>11949.8</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Syria</td>
      <td>Asia</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>83034.2</td>
    </tr>
  </tbody>
</table>
<p>102 rows × 6 columns</p>
</div>
```
:::
:::

::: {#2640d3a6-064e-4c24-b2be-7593618919c0 .cell .code execution_count="208"}
``` python
df.nunique()
```

::: {.output .execute_result execution_count="208"}
    Country                      102
    Continent                      6
    Production(Tons)             102
    Production_per_person(Kg)    101
    Acreage(Hectare)             101
    Yield(Kg/Hectare)            102
    dtype: int64
:::
:::

::: {#0d7ba548-d73e-403d-8b58-b6c07e3c913c .cell .code execution_count="210"}
``` python
df.dtypes
```

::: {.output .execute_result execution_count="210"}
    Country                      object
    Continent                    object
    Production(Tons)             object
    Production_per_person(Kg)    object
    Acreage(Hectare)             object
    Yield(Kg/Hectare)            object
    dtype: object
:::
:::

::: {#c4747364-791d-4d51-bf82-40397dd72ae0 .cell .code execution_count="212"}
``` python
df["Production(Tons)"] = df["Production(Tons)"].astype(float)
df["Production_per_person(Kg)"] = df["Production_per_person(Kg)"].astype(float)
df["Acreage(Hectare)"] = df["Acreage(Hectare)"].astype(float)
df["Yield(Kg/Hectare)"] = df["Yield(Kg/Hectare)"].astype(float)
```
:::

::: {#444bc27f-b954-4103-9174-4647aec606e3 .cell .code execution_count="214"}
``` python
df.dtypes
```

::: {.output .execute_result execution_count="214"}
    Country                       object
    Continent                     object
    Production(Tons)             float64
    Production_per_person(Kg)    float64
    Acreage(Hectare)             float64
    Yield(Kg/Hectare)            float64
    dtype: object
:::
:::

::: {#1e0e9a36-9ece-491b-97fd-f25de1b712bd .cell .markdown}
# Univariate Analysis
:::

::: {#04b603dc-0fb9-4351-a5a4-7ec441ed4a3d .cell .code execution_count="217"}
``` python
df.head()
```

::: {.output .execute_result execution_count="217"}
```{=html}
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
      <th>Country</th>
      <th>Continent</th>
      <th>Production(Tons)</th>
      <th>Production_per_person(Kg)</th>
      <th>Acreage(Hectare)</th>
      <th>Yield(Kg/Hectare)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Brazil</td>
      <td>South America</td>
      <td>768678382.0</td>
      <td>3668.531</td>
      <td>10226205.0</td>
      <td>75167.5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>India</td>
      <td>Asia</td>
      <td>348448000.0</td>
      <td>260721.000</td>
      <td>4950000.0</td>
      <td>70393.5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>China</td>
      <td>Asia</td>
      <td>123059739.0</td>
      <td>88287.000</td>
      <td>1675215.0</td>
      <td>73459.1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Thailand</td>
      <td>Asia</td>
      <td>87468496.0</td>
      <td>1264.303</td>
      <td>1336575.0</td>
      <td>65442.2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Pakistan</td>
      <td>Asia</td>
      <td>65450704.0</td>
      <td>324219.000</td>
      <td>1130820.0</td>
      <td>57879.0</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {#f4d45606-babc-4d0f-ad7b-725dbe61bc53 .cell .markdown}
## Howmany countries produce sugarcane from each continent?
:::

::: {#75eedc0d-c7e4-4aaa-89ae-96bb48515e76 .cell .code execution_count="220"}
``` python
df["Continent"].value_counts()
```

::: {.output .execute_result execution_count="220"}
    Continent
    Africa           38
    Asia             25
    North America    22
    South America    11
    Oceania           4
    Europe            2
    Name: count, dtype: int64
:::
:::

::: {#52e6a1f4-6bd3-4cf6-a6dc-dc413a892bb7 .cell .code execution_count="222"}
``` python
df["Continent"].value_counts().plot(kind = "bar")
```

::: {.output .execute_result execution_count="222"}
    <Axes: xlabel='Continent'>
:::

::: {.output .display_data}
![](vertopal_49c98fc2481b4248b76bce5ad9c45918/55d4db27b6c12cb0b9ca8006e8df1864826b6c82.png)
:::
:::

::: {#b1704b97-485d-46bf-ba28-3d1cdc69d0aa .cell .code execution_count="224"}
``` python
df.describe()
```

::: {.output .execute_result execution_count="224"}
```{=html}
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
      <th>Production(Tons)</th>
      <th>Production_per_person(Kg)</th>
      <th>Acreage(Hectare)</th>
      <th>Yield(Kg/Hectare)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>1.020000e+02</td>
      <td>102.000000</td>
      <td>1.020000e+02</td>
      <td>102.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>1.850372e+07</td>
      <td>112952.435755</td>
      <td>2.498981e+05</td>
      <td>52628.078431</td>
    </tr>
    <tr>
      <th>std</th>
      <td>8.419149e+07</td>
      <td>176651.341929</td>
      <td>1.137003e+06</td>
      <td>30504.676683</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.000000e+00</td>
      <td>0.000000</td>
      <td>0.000000e+00</td>
      <td>10.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>6.251875e+04</td>
      <td>3671.910000</td>
      <td>1.104000e+03</td>
      <td>29072.025000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>1.440044e+06</td>
      <td>25572.500000</td>
      <td>1.655800e+04</td>
      <td>54108.950000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>6.426824e+06</td>
      <td>146384.750000</td>
      <td>8.047400e+04</td>
      <td>73282.700000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>7.686784e+08</td>
      <td>951087.000000</td>
      <td>1.022620e+07</td>
      <td>129049.300000</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {#90ca3044-984b-45ad-80e9-2dcdfca19db6 .cell .markdown}
## Checking Outliers
:::

::: {#2f84bbaf-dc74-4544-80e7-b23fab143016 .cell .code execution_count="227"}
``` python
plt.figure(figsize = (10,8))
plt.subplot(2,2,1)
sns.boxplot(df["Production(Tons)"])
plt.title("Production(Tons)")
plt.subplot(2,2,2)
sns.boxplot(df["Production_per_person(Kg)"])
plt.title("Production_per_person(Kg)")
plt.subplot(2,2,3)
sns.boxplot(df["Acreage(Hectare)"])
plt.title("Acreage(Hectare)")
plt.subplot(2,2,4)
sns.boxplot(df["Yield(Kg/Hectare)"])
plt.title("Yield(Kg/Hectare)")
plt.show()
```

::: {.output .display_data}
![](vertopal_49c98fc2481b4248b76bce5ad9c45918/38a051c9b5ba5ae48a41e7c37ab3e91e43b6652c.png)
:::
:::

::: {#5fa06fdf-f653-482f-a300-8740388dbb59 .cell .markdown}
## Distribution of the columns
:::

::: {#f54542f6-daec-4e71-900f-23edc30e82e0 .cell .code execution_count="229"}
``` python
plt.figure(figsize = (10,10))
plt.subplot(2,2,1)
sns.distplot(df["Production(Tons)"])
plt.title("Production(Tons)")
plt.subplot(2,2,2)
sns.distplot(df["Production_per_person(Kg)"])
plt.title("Production_per_person(Kg)")
plt.subplot(2,2,3)
sns.distplot(df["Acreage(Hectare)"])
plt.title("Acreage(Hectare)")
plt.subplot(2,2,4)
sns.distplot(df["Yield(Kg/Hectare)"])
plt.title("Yield(Kg/Hectare)")
plt.show()
```

::: {.output .stream .stderr}
    C:\Users\KIIT\AppData\Local\Temp\ipykernel_9332\1909675950.py:3: UserWarning: 

    `distplot` is a deprecated function and will be removed in seaborn v0.14.0.

    Please adapt your code to use either `displot` (a figure-level function with
    similar flexibility) or `histplot` (an axes-level function for histograms).

    For a guide to updating your code to use the new functions, please see
    https://gist.github.com/mwaskom/de44147ed2974457ad6372750bbe5751

      sns.distplot(df["Production(Tons)"])
    C:\Users\KIIT\AppData\Local\Temp\ipykernel_9332\1909675950.py:6: UserWarning: 

    `distplot` is a deprecated function and will be removed in seaborn v0.14.0.

    Please adapt your code to use either `displot` (a figure-level function with
    similar flexibility) or `histplot` (an axes-level function for histograms).

    For a guide to updating your code to use the new functions, please see
    https://gist.github.com/mwaskom/de44147ed2974457ad6372750bbe5751

      sns.distplot(df["Production_per_person(Kg)"])
    C:\Users\KIIT\AppData\Local\Temp\ipykernel_9332\1909675950.py:9: UserWarning: 

    `distplot` is a deprecated function and will be removed in seaborn v0.14.0.

    Please adapt your code to use either `displot` (a figure-level function with
    similar flexibility) or `histplot` (an axes-level function for histograms).

    For a guide to updating your code to use the new functions, please see
    https://gist.github.com/mwaskom/de44147ed2974457ad6372750bbe5751

      sns.distplot(df["Acreage(Hectare)"])
    C:\Users\KIIT\AppData\Local\Temp\ipykernel_9332\1909675950.py:12: UserWarning: 

    `distplot` is a deprecated function and will be removed in seaborn v0.14.0.

    Please adapt your code to use either `displot` (a figure-level function with
    similar flexibility) or `histplot` (an axes-level function for histograms).

    For a guide to updating your code to use the new functions, please see
    https://gist.github.com/mwaskom/de44147ed2974457ad6372750bbe5751

      sns.distplot(df["Yield(Kg/Hectare)"])
:::

::: {.output .display_data}
![](vertopal_49c98fc2481b4248b76bce5ad9c45918/c0fca12d6712f83be84e8e7e8fdb45e8bc98f073.png)
:::
:::

::: {#03672736-085e-4fca-953b-90b5b65b4b5a .cell .code execution_count="231"}
``` python
plt.figure(figsize = (10,10))
plt.subplot(2,2,1)
sns.violinplot(df["Production(Tons)"])
plt.title("Production(Tons)")
plt.subplot(2,2,2)
sns.violinplot(df["Production_per_person(Kg)"])
plt.title("Production_per_person(Kg)")
plt.subplot(2,2,3)
sns.violinplot(df["Acreage(Hectare)"])
plt.title("Acreage(Hectare)")
plt.subplot(2,2,4)
sns.violinplot(df["Yield(Kg/Hectare)"])
plt.title("Yield(Kg/Hectare)")
```

::: {.output .execute_result execution_count="231"}
    Text(0.5, 1.0, 'Yield(Kg/Hectare)')
:::

::: {.output .display_data}
![](vertopal_49c98fc2481b4248b76bce5ad9c45918/81f7119125821a61b559c081dd014431e12c2114.png)
:::
:::

::: {#4c4f8b61-5223-45b5-866f-8519d8141d33 .cell .markdown}
# Bivariate Analysis
:::

::: {#757f8495-d064-4f3a-959e-3eb99afc09c6 .cell .code execution_count="234"}
``` python
df.head()
```

::: {.output .execute_result execution_count="234"}
```{=html}
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
      <th>Country</th>
      <th>Continent</th>
      <th>Production(Tons)</th>
      <th>Production_per_person(Kg)</th>
      <th>Acreage(Hectare)</th>
      <th>Yield(Kg/Hectare)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Brazil</td>
      <td>South America</td>
      <td>768678382.0</td>
      <td>3668.531</td>
      <td>10226205.0</td>
      <td>75167.5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>India</td>
      <td>Asia</td>
      <td>348448000.0</td>
      <td>260721.000</td>
      <td>4950000.0</td>
      <td>70393.5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>China</td>
      <td>Asia</td>
      <td>123059739.0</td>
      <td>88287.000</td>
      <td>1675215.0</td>
      <td>73459.1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Thailand</td>
      <td>Asia</td>
      <td>87468496.0</td>
      <td>1264.303</td>
      <td>1336575.0</td>
      <td>65442.2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Pakistan</td>
      <td>Asia</td>
      <td>65450704.0</td>
      <td>324219.000</td>
      <td>1130820.0</td>
      <td>57879.0</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {#ab641156-2602-48c6-8cc8-9d920b5d853c .cell .markdown}
## Which country produces maximum sugarcane?
:::

::: {#cedea2fa-47a1-47a0-b333-c80e440e4122 .cell .code execution_count="238"}
``` python
df_new = df[["Country","Production(Tons)"]].set_index("Country")
```
:::

::: {#4e415bd3-0308-4796-be92-31a23cadb2af .cell .code execution_count="240"}
``` python
df_new
```

::: {.output .execute_result execution_count="240"}
```{=html}
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
      <th>Production(Tons)</th>
    </tr>
    <tr>
      <th>Country</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Brazil</th>
      <td>768678382.0</td>
    </tr>
    <tr>
      <th>India</th>
      <td>348448000.0</td>
    </tr>
    <tr>
      <th>China</th>
      <td>123059739.0</td>
    </tr>
    <tr>
      <th>Thailand</th>
      <td>87468496.0</td>
    </tr>
    <tr>
      <th>Pakistan</th>
      <td>65450704.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>Spain</th>
      <td>394.0</td>
    </tr>
    <tr>
      <th>Lebanon</th>
      <td>97.0</td>
    </tr>
    <tr>
      <th>Singapore</th>
      <td>50.0</td>
    </tr>
    <tr>
      <th>Samoa</th>
      <td>12.0</td>
    </tr>
    <tr>
      <th>Syria</th>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
<p>102 rows × 1 columns</p>
</div>
```
:::
:::

::: {#4a66d5a8-1a5b-488c-a17b-a2ee3f90bb05 .cell .code execution_count="242"}
``` python
df_new["Production(Tons)_percent"] = df_new["Production(Tons)"]*100/df_new["Production(Tons)"].sum()
```
:::

::: {#b1e2f867-feb7-40bb-a278-95eb544b2e1d .cell .code execution_count="244"}
``` python
df_new
```

::: {.output .execute_result execution_count="244"}
```{=html}
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
      <th>Production(Tons)</th>
      <th>Production(Tons)_percent</th>
    </tr>
    <tr>
      <th>Country</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Brazil</th>
      <td>768678382.0</td>
      <td>4.072729e+01</td>
    </tr>
    <tr>
      <th>India</th>
      <td>348448000.0</td>
      <td>1.846200e+01</td>
    </tr>
    <tr>
      <th>China</th>
      <td>123059739.0</td>
      <td>6.520138e+00</td>
    </tr>
    <tr>
      <th>Thailand</th>
      <td>87468496.0</td>
      <td>4.634389e+00</td>
    </tr>
    <tr>
      <th>Pakistan</th>
      <td>65450704.0</td>
      <td>3.467809e+00</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Spain</th>
      <td>394.0</td>
      <td>2.087551e-05</td>
    </tr>
    <tr>
      <th>Lebanon</th>
      <td>97.0</td>
      <td>5.139401e-06</td>
    </tr>
    <tr>
      <th>Singapore</th>
      <td>50.0</td>
      <td>2.649176e-06</td>
    </tr>
    <tr>
      <th>Samoa</th>
      <td>12.0</td>
      <td>6.358022e-07</td>
    </tr>
    <tr>
      <th>Syria</th>
      <td>1.0</td>
      <td>5.298352e-08</td>
    </tr>
  </tbody>
</table>
<p>102 rows × 2 columns</p>
</div>
```
:::
:::

::: {#43478619-af08-4780-8387-c251c6650c13 .cell .code execution_count="246"}
``` python
df_new["Production(Tons)_percent"].plot(kind = "pie", autopct = "%.2f")
```

::: {.output .execute_result execution_count="246"}
    <Axes: ylabel='Production(Tons)_percent'>
:::

::: {.output .display_data}
![](vertopal_49c98fc2481b4248b76bce5ad9c45918/54f7c3aae8399d7d9fe603e92ce33980367f22b7.png)
:::
:::

::: {#924d518a-8d26-4d94-8743-b1151112f272 .cell .code execution_count="247"}
``` python
df[["Country","Production(Tons)"]].set_index("Country").sort_values("Production(Tons)", ascending = False).head(15).plot(kind = "bar")
```

::: {.output .execute_result execution_count="247"}
    <Axes: xlabel='Country'>
:::

::: {.output .display_data}
![](vertopal_49c98fc2481b4248b76bce5ad9c45918/c2c826f942eec94289366961960f26ce25d8f838.png)
:::
:::

::: {#e8d1dd41-912a-4d60-9bb9-a5eab7937cc8 .cell .code execution_count="250"}
``` python
ax = sns.barplot(data = df.head(15),  x= "Country", y = "Production(Tons)")
ax.set_xticklabels(ax.get_xticklabels(),rotation =90)
plt.show()
```

::: {.output .stream .stderr}
    C:\Users\KIIT\AppData\Local\Temp\ipykernel_9332\2823669880.py:2: UserWarning: set_ticklabels() should only be used with a fixed number of ticks, i.e. after set_ticks() or using a FixedLocator.
      ax.set_xticklabels(ax.get_xticklabels(),rotation =90)
:::

::: {.output .display_data}
![](vertopal_49c98fc2481b4248b76bce5ad9c45918/f8a875fcac9060b3ef52089f4ba22f6f186abab3.png)
:::
:::

::: {#25864b28-bd6e-4827-a64c-89cecf273e27 .cell .markdown}
## Which Country Has Highhest Land
:::

::: {#104ebd09-53e3-4b03-b602-5bfcf435b83c .cell .code execution_count="253"}
``` python
df_acr = df.sort_values("Acreage(Hectare)", ascending = False).head(15)
ax = sns.barplot(data = df_acr,  x= "Country", y = "Acreage(Hectare)")
ax.set_xticklabels(ax.get_xticklabels(),rotation =90)
plt.show()
```

::: {.output .stream .stderr}
    C:\Users\KIIT\AppData\Local\Temp\ipykernel_9332\2973715568.py:3: UserWarning: set_ticklabels() should only be used with a fixed number of ticks, i.e. after set_ticks() or using a FixedLocator.
      ax.set_xticklabels(ax.get_xticklabels(),rotation =90)
:::

::: {.output .display_data}
![](vertopal_49c98fc2481b4248b76bce5ad9c45918/ed245bdb8952ebc0919216ac712cd5cbabdf759d.png)
:::
:::

::: {#11cf7b33-b653-4bdd-b63a-90bd58f23c0a .cell .markdown}
## Which country has highest yield per hectare?
:::

::: {#ad80165f-f123-46a4-90ae-9c480113bfcc .cell .code execution_count="256"}
``` python
df_yield = df.sort_values("Yield(Kg/Hectare)", ascending = False).head(15)
ax = sns.barplot(data = df_yield,  x= "Country", y = "Yield(Kg/Hectare)")
ax.set_xticklabels(ax.get_xticklabels(),rotation =90)
plt.show()
```

::: {.output .stream .stderr}
    C:\Users\KIIT\AppData\Local\Temp\ipykernel_9332\2860594357.py:3: UserWarning: set_ticklabels() should only be used with a fixed number of ticks, i.e. after set_ticks() or using a FixedLocator.
      ax.set_xticklabels(ax.get_xticklabels(),rotation =90)
:::

::: {.output .display_data}
![](vertopal_49c98fc2481b4248b76bce5ad9c45918/1a913220d5a7b5d868a55475d4ea81525efbbd6b.png)
:::
:::

::: {#30c291a4-1a79-4fcc-bee0-0f542924a371 .cell .markdown}
## Which country has highest yield per hectare? {#which-country-has-highest-yield-per-hectare}
:::

::: {#04a41055-49c7-456b-8ec3-b377b309d38c .cell .code execution_count="259"}
``` python
df_yield = df.sort_values("Production_per_person(Kg)", ascending = False).head(15)
ax = sns.barplot(data = df_yield,  x= "Country", y = "Production_per_person(Kg)")
ax.set_xticklabels(ax.get_xticklabels(),rotation =90)
plt.show()
```

::: {.output .stream .stderr}
    C:\Users\KIIT\AppData\Local\Temp\ipykernel_9332\328127327.py:3: UserWarning: set_ticklabels() should only be used with a fixed number of ticks, i.e. after set_ticks() or using a FixedLocator.
      ax.set_xticklabels(ax.get_xticklabels(),rotation =90)
:::

::: {.output .display_data}
![](vertopal_49c98fc2481b4248b76bce5ad9c45918/6ec3ab1bb141349a4f60e385d6a41156cd4626ba.png)
:::
:::

::: {#163951d2-77d5-43f4-9902-eac2ec31d362 .cell .markdown}
## Which country has highest production?
:::

::: {#70da4dfa-6c3f-46d4-9d57-0b3b6f83c3b5 .cell .code execution_count="262"}
``` python
df_yield = df.sort_values("Production_per_person(Kg)", ascending = False).head(15)
ax = sns.barplot(data = df_yield,  x= "Country", y = "Production_per_person(Kg)")
ax.set_xticklabels(ax.get_xticklabels(),rotation =90)
plt.show()
```

::: {.output .stream .stderr}
    C:\Users\KIIT\AppData\Local\Temp\ipykernel_9332\328127327.py:3: UserWarning: set_ticklabels() should only be used with a fixed number of ticks, i.e. after set_ticks() or using a FixedLocator.
      ax.set_xticklabels(ax.get_xticklabels(),rotation =90)
:::

::: {.output .display_data}
![](vertopal_49c98fc2481b4248b76bce5ad9c45918/6ec3ab1bb141349a4f60e385d6a41156cd4626ba.png)
:::
:::

::: {#c349375c-4fbc-4af8-8b80-2b2a85fc3962 .cell .markdown}
# Correlation
:::

::: {#b63e4cc8-8a84-4042-b751-34fac7807c6b .cell .code execution_count="265"}
``` python
df.corr(numeric_only = True)
```

::: {.output .execute_result execution_count="265"}
```{=html}
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
      <th>Production(Tons)</th>
      <th>Production_per_person(Kg)</th>
      <th>Acreage(Hectare)</th>
      <th>Yield(Kg/Hectare)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Production(Tons)</th>
      <td>1.000000</td>
      <td>0.015000</td>
      <td>0.997550</td>
      <td>0.132812</td>
    </tr>
    <tr>
      <th>Production_per_person(Kg)</th>
      <td>0.015000</td>
      <td>1.000000</td>
      <td>0.012557</td>
      <td>0.017999</td>
    </tr>
    <tr>
      <th>Acreage(Hectare)</th>
      <td>0.997550</td>
      <td>0.012557</td>
      <td>1.000000</td>
      <td>0.113433</td>
    </tr>
    <tr>
      <th>Yield(Kg/Hectare)</th>
      <td>0.132812</td>
      <td>0.017999</td>
      <td>0.113433</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {#fda97e93-dcc4-4ae4-b899-34ff45c26132 .cell .markdown}
## Do countries with highest land produce more sugarcane?
:::

::: {#b73d04ac-6ec0-45f9-afdf-546bf32da1f2 .cell .code execution_count="268"}
``` python
sns.heatmap(df.corr(numeric_only = True), annot = True, cmap="Greens")
```

::: {.output .execute_result execution_count="268"}
    <Axes: >
:::

::: {.output .display_data}
![](vertopal_49c98fc2481b4248b76bce5ad9c45918/35b16bf1cbbf515d710831e9dfeac7804302596e.png)
:::
:::

::: {#886afa2f-52bc-44fe-a74e-1c45de7c963b .cell .code execution_count="270"}
``` python
sns.scatterplot(data = df, x = "Acreage(Hectare)", y = "Production(Tons)", hue = "Continent" )
```

::: {.output .execute_result execution_count="270"}
    <Axes: xlabel='Acreage(Hectare)', ylabel='Production(Tons)'>
:::

::: {.output .display_data}
![](vertopal_49c98fc2481b4248b76bce5ad9c45918/51f61ebf7d5aa61f71ca6b46245bc8d564adf878.png)
:::
:::

::: {#ca484442-38fd-4421-b84c-b9a5c2b9c1af .cell .markdown}
## Do countries which yield more sugarcane per hectare produces more sugarcane in total?
:::

::: {#a76ef2f7-31f2-42b7-827a-a1a171b37300 .cell .code execution_count="273"}
``` python
sns.scatterplot(data = df, x = "Yield(Kg/Hectare)" , y = "Production(Tons)", hue = "Continent")
```

::: {.output .execute_result execution_count="273"}
    <Axes: xlabel='Yield(Kg/Hectare)', ylabel='Production(Tons)'>
:::

::: {.output .display_data}
![](vertopal_49c98fc2481b4248b76bce5ad9c45918/e71cae0698b4d913c3fa36a22e10eb6a4ff2739e.png)
:::
:::

::: {#39d85d87-3ea7-4f3e-8117-9630790fc3fc .cell .markdown}
# Analysis for Continent
:::

::: {#470663c2-6ab7-4c0d-a19a-c9389a61d7e4 .cell .code execution_count="289"}
``` python
df_continent = df.groupby("Continent").sum()
```
:::

::: {#793366fd-9e0d-47e0-b94c-8fdef8f4f93f .cell .code execution_count="293"}
``` python
df_continent
```

::: {.output .execute_result execution_count="293"}
```{=html}
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
      <th>Country</th>
      <th>Production(Tons)</th>
      <th>Production_per_person(Kg)</th>
      <th>Acreage(Hectare)</th>
      <th>Yield(Kg/Hectare)</th>
    </tr>
    <tr>
      <th>Continent</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Africa</th>
      <td>EgyptSouth AfricaKenyaSwazilandSudanZambiaMaur...</td>
      <td>89681472.0</td>
      <td>2332636.293</td>
      <td>1439089.0</td>
      <td>2142107.5</td>
    </tr>
    <tr>
      <th>Asia</th>
      <td>IndiaChinaThailandPakistanIndonesiaPhilippines...</td>
      <td>721930425.0</td>
      <td>1857769.303</td>
      <td>10608319.0</td>
      <td>1171871.4</td>
    </tr>
    <tr>
      <th>Europe</th>
      <td>PortugalSpain</td>
      <td>5823.0</td>
      <td>536.000</td>
      <td>71.0</td>
      <td>131870.9</td>
    </tr>
    <tr>
      <th>North America</th>
      <td>MexicoGuatemalaUnited States of AmericaCubaEl ...</td>
      <td>173995947.0</td>
      <td>3796081.508</td>
      <td>1581983.0</td>
      <td>1082602.4</td>
    </tr>
    <tr>
      <th>Oceania</th>
      <td>AustraliaFijiPapua New GuineaSamoa</td>
      <td>36177574.0</td>
      <td>28593.605</td>
      <td>490909.0</td>
      <td>162419.1</td>
    </tr>
    <tr>
      <th>South America</th>
      <td>BrazilColombiaArgentinaPeruEcuadorBoliviaParag...</td>
      <td>865588126.0</td>
      <td>3505531.738</td>
      <td>11369236.0</td>
      <td>677192.7</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {#2b2ee371-a23b-4e1d-909e-0628e988042e .cell .code execution_count="299"}
``` python
df_continent["number_of_countries"] = df.groupby("Continent").count()["Country"]
```
:::

::: {#6a4b99e8-bfdd-4b54-baa3-9618bee56a32 .cell .code execution_count="301"}
``` python
df_continent
```

::: {.output .execute_result execution_count="301"}
```{=html}
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
      <th>Country</th>
      <th>Production(Tons)</th>
      <th>Production_per_person(Kg)</th>
      <th>Acreage(Hectare)</th>
      <th>Yield(Kg/Hectare)</th>
      <th>number_of_countries</th>
    </tr>
    <tr>
      <th>Continent</th>
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
      <th>Africa</th>
      <td>EgyptSouth AfricaKenyaSwazilandSudanZambiaMaur...</td>
      <td>89681472.0</td>
      <td>2332636.293</td>
      <td>1439089.0</td>
      <td>2142107.5</td>
      <td>38</td>
    </tr>
    <tr>
      <th>Asia</th>
      <td>IndiaChinaThailandPakistanIndonesiaPhilippines...</td>
      <td>721930425.0</td>
      <td>1857769.303</td>
      <td>10608319.0</td>
      <td>1171871.4</td>
      <td>25</td>
    </tr>
    <tr>
      <th>Europe</th>
      <td>PortugalSpain</td>
      <td>5823.0</td>
      <td>536.000</td>
      <td>71.0</td>
      <td>131870.9</td>
      <td>2</td>
    </tr>
    <tr>
      <th>North America</th>
      <td>MexicoGuatemalaUnited States of AmericaCubaEl ...</td>
      <td>173995947.0</td>
      <td>3796081.508</td>
      <td>1581983.0</td>
      <td>1082602.4</td>
      <td>22</td>
    </tr>
    <tr>
      <th>Oceania</th>
      <td>AustraliaFijiPapua New GuineaSamoa</td>
      <td>36177574.0</td>
      <td>28593.605</td>
      <td>490909.0</td>
      <td>162419.1</td>
      <td>4</td>
    </tr>
    <tr>
      <th>South America</th>
      <td>BrazilColombiaArgentinaPeruEcuadorBoliviaParag...</td>
      <td>865588126.0</td>
      <td>3505531.738</td>
      <td>11369236.0</td>
      <td>677192.7</td>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {#35824d3f-7798-46b9-a580-1edd814a545e .cell .code execution_count="297"}
``` python
df_continent["Production(Tons)"].sort_values(ascending =  False).plot(kind = "bar")
```

::: {.output .execute_result execution_count="297"}
    <Axes: xlabel='Continent'>
:::

::: {.output .display_data}
![](vertopal_49c98fc2481b4248b76bce5ad9c45918/9601eabe61552769272b9dd09efe3dd57c647d34.png)
:::
:::

::: {#dcd881a3-5aec-4726-992a-c005e3dc296a .cell .markdown}
## Do number of countries in a Continent effects production of sugarcane?
:::

::: {#846ceaf3-a55d-4bae-bc47-7ba73a2ce72b .cell .code execution_count="304"}
``` python
continent_names = df_continent.index.to_list()
sns.lineplot(data = df_continent,x = "number_of_countries", y= "Production(Tons)" )
plt.xticks(df_continent["number_of_countries"], continent_names, rotation =90)
plt.show()
```

::: {.output .display_data}
![](vertopal_49c98fc2481b4248b76bce5ad9c45918/f9a32c1f135ff267da7e217a768139768022b767.png)
:::
:::

::: {#db05eaa5-44a8-4828-a945-2982ba93134a .cell .markdown}
## Do continent with highest land produces more sugarcane?
:::

::: {#eaefcd52-2025-42bc-8e54-cf1153812411 .cell .code execution_count="307"}
``` python
sns.lineplot(data = df_continent,x = "Acreage(Hectare)", y= "Production(Tons)" )
```

::: {.output .execute_result execution_count="307"}
    <Axes: xlabel='Acreage(Hectare)', ylabel='Production(Tons)'>
:::

::: {.output .display_data}
![](vertopal_49c98fc2481b4248b76bce5ad9c45918/6b23ac3255a76f0871e5c72dbd334a5d921bd14d.png)
:::
:::

::: {#65ec7735-b863-4607-9e43-4f8a357d1c13 .cell .markdown}
## Production distribution by continent
:::

::: {#0ccf712c-22df-4873-b436-849bf1fc7be2 .cell .code execution_count="311"}
``` python
df_continent["Production(Tons)"].plot(kind = "pie", autopct = "%.2f%%")
plt.title('Production Distribution by Continent')
plt.show()
```

::: {.output .display_data}
![](vertopal_49c98fc2481b4248b76bce5ad9c45918/6a6a13fd9643af827b7caf415f04ba3a52431814.png)
:::
:::

::: {#26d85c91-25fe-4d8f-84fc-c660ccd4a79e .cell .markdown}
## Correlation for continent
:::

::: {#8c7cfb96-15a8-49ee-9f15-df7b2c102192 .cell .code execution_count="316"}
``` python
df_continent.corr(numeric_only=True)
```

::: {.output .execute_result execution_count="316"}
```{=html}
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
      <th>Production(Tons)</th>
      <th>Production_per_person(Kg)</th>
      <th>Acreage(Hectare)</th>
      <th>Yield(Kg/Hectare)</th>
      <th>number_of_countries</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Production(Tons)</th>
      <td>1.000000</td>
      <td>0.522211</td>
      <td>0.994897</td>
      <td>0.091201</td>
      <td>0.109244</td>
    </tr>
    <tr>
      <th>Production_per_person(Kg)</th>
      <td>0.522211</td>
      <td>1.000000</td>
      <td>0.463215</td>
      <td>0.542961</td>
      <td>0.540086</td>
    </tr>
    <tr>
      <th>Acreage(Hectare)</th>
      <td>0.994897</td>
      <td>0.463215</td>
      <td>1.000000</td>
      <td>0.111166</td>
      <td>0.132817</td>
    </tr>
    <tr>
      <th>Yield(Kg/Hectare)</th>
      <td>0.091201</td>
      <td>0.542961</td>
      <td>0.111166</td>
      <td>1.000000</td>
      <td>0.989712</td>
    </tr>
    <tr>
      <th>number_of_countries</th>
      <td>0.109244</td>
      <td>0.540086</td>
      <td>0.132817</td>
      <td>0.989712</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {#4a967380-1c37-49de-ae97-d5c802c40fa9 .cell .code execution_count="318"}
``` python
sns.heatmap(df_continent.corr(numeric_only = True), annot = True, cmap="Greens")
```

::: {.output .execute_result execution_count="318"}
    <Axes: >
:::

::: {.output .display_data}
![](vertopal_49c98fc2481b4248b76bce5ad9c45918/e2359d6c3041fbc353349020b6412090ed5e64e7.png)
:::
:::

::: {#12cf017a-2ab2-40f0-9fa0-696308133af4 .cell .code}
``` python
```
:::
