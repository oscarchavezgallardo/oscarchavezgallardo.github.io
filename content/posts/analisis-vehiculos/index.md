---
title: "Análisis exploratorio de datos: comparaciones"
description: "Comparaciones entre grupos, medias y tendencias temporales con pandas y seaborn."
date: 2026-10-01
tags: ["data-science-ml"]
---

La magia de matplotlib `matplotlib notebook`, es muy util para hacer plots mas visibles, pero es un poco complicada de usar ya que requiere el cerrar cada plot para poder continuar.

Alternativamente, se puede usar la magia `%matplotlib inline`, que es más sencilla ya que simplemente muestra el gráfico original en el jupyter notebook. Para modificar el tamaño de los plots en este caso basta con cambiar el parámetro general de matplotlib `figure.figsize` al tamaño de gráfico deseado  (en pulgadas)


```python
%matplotlib inline

plt.rcParams['figure.figsize'] = (10,10) # 10 pulgadas de ancho y 10 de alto para todos los plots
```

### Lectura de datos


```python
vehiculos = pd.read_pickle("../data/vehiculos.3.variables_agrupadas.pkl")
```


```python
vehiculos.dtypes
```




    fabricante                object
    modelo                    object
    year                       int64
    desplazamiento           float64
    cilindros                float64
    transmision               object
    traccion                  object
    clase                     object
    combustible               object
    consumo                    int64
    co2                      float64
    clase_tipo              category
    traccion_tipo           category
    transmision_tipo        category
    combustible_tipo        category
    tamano_motor_tipo       category
    consumo_tipo            category
    co2_tipo                category
    consumo_litros_milla     float64
    dtype: object



Vemos que al leer de un dataframe pickled, pandas no tiene que averiguar de nuevo que tipo de dato es cada columna, lo carga todo en memoria directamente.


```python
vehiculos.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>fabricante</th>
      <th>modelo</th>
      <th>year</th>
      <th>desplazamiento</th>
      <th>cilindros</th>
      <th>transmision</th>
      <th>traccion</th>
      <th>clase</th>
      <th>combustible</th>
      <th>consumo</th>
      <th>co2</th>
      <th>clase_tipo</th>
      <th>traccion_tipo</th>
      <th>transmision_tipo</th>
      <th>combustible_tipo</th>
      <th>tamano_motor_tipo</th>
      <th>consumo_tipo</th>
      <th>co2_tipo</th>
      <th>consumo_litros_milla</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>AM General</td>
      <td>DJ Po Vehicle 2WD</td>
      <td>1984</td>
      <td>2.5</td>
      <td>4.0</td>
      <td>Automatic 3-spd</td>
      <td>2-Wheel Drive</td>
      <td>Special Purpose Vehicle 2WD</td>
      <td>Regular</td>
      <td>17</td>
      <td>522.764706</td>
      <td>Vehículos Especiales</td>
      <td>dos</td>
      <td>Automatica</td>
      <td>Normal</td>
      <td>pequeño</td>
      <td>alto</td>
      <td>alto</td>
      <td>0.222671</td>
    </tr>
    <tr>
      <th>1</th>
      <td>AM General</td>
      <td>FJ8c Post Office</td>
      <td>1984</td>
      <td>4.2</td>
      <td>6.0</td>
      <td>Automatic 3-spd</td>
      <td>2-Wheel Drive</td>
      <td>Special Purpose Vehicle 2WD</td>
      <td>Regular</td>
      <td>13</td>
      <td>683.615385</td>
      <td>Vehículos Especiales</td>
      <td>dos</td>
      <td>Automatica</td>
      <td>Normal</td>
      <td>grande</td>
      <td>muy alto</td>
      <td>muy alto</td>
      <td>0.291185</td>
    </tr>
    <tr>
      <th>2</th>
      <td>AM General</td>
      <td>Post Office DJ5 2WD</td>
      <td>1985</td>
      <td>2.5</td>
      <td>4.0</td>
      <td>Automatic 3-spd</td>
      <td>Rear-Wheel Drive</td>
      <td>Special Purpose Vehicle 2WD</td>
      <td>Regular</td>
      <td>16</td>
      <td>555.437500</td>
      <td>Vehículos Especiales</td>
      <td>dos</td>
      <td>Automatica</td>
      <td>Normal</td>
      <td>pequeño</td>
      <td>alto</td>
      <td>alto</td>
      <td>0.236588</td>
    </tr>
    <tr>
      <th>3</th>
      <td>AM General</td>
      <td>Post Office DJ8 2WD</td>
      <td>1985</td>
      <td>4.2</td>
      <td>6.0</td>
      <td>Automatic 3-spd</td>
      <td>Rear-Wheel Drive</td>
      <td>Special Purpose Vehicle 2WD</td>
      <td>Regular</td>
      <td>13</td>
      <td>683.615385</td>
      <td>Vehículos Especiales</td>
      <td>dos</td>
      <td>Automatica</td>
      <td>Normal</td>
      <td>grande</td>
      <td>muy alto</td>
      <td>muy alto</td>
      <td>0.291185</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ASC Incorporated</td>
      <td>GNX</td>
      <td>1987</td>
      <td>3.8</td>
      <td>6.0</td>
      <td>Automatic 4-spd</td>
      <td>Rear-Wheel Drive</td>
      <td>Midsize Cars</td>
      <td>Premium</td>
      <td>16</td>
      <td>555.437500</td>
      <td>Coches Medianos</td>
      <td>dos</td>
      <td>Automatica</td>
      <td>Premium</td>
      <td>grande</td>
      <td>alto</td>
      <td>alto</td>
      <td>0.236588</td>
    </tr>
  </tbody>
</table>
</div>




```python
from ipywidgets import interact, fixed
```

### Recuento por multiples grupos


```python
def pivot_recuento(df, rows, columns, calc_field):
    df_pivot = df.pivot_table(values=calc_field, 
                              index=rows, 
                              columns=columns, 
                              aggfunc=np.size
                             ).dropna(axis=0, how='all')
    return df_pivot
```


```python
consumo_combustible = pivot_recuento(vehiculos,"combustible_tipo","consumo_tipo", "year")
consumo_combustible
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>consumo_tipo</th>
      <th>muy bajo</th>
      <th>bajo</th>
      <th>moderado</th>
      <th>alto</th>
      <th>muy alto</th>
    </tr>
    <tr>
      <th>combustible_tipo</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Hibrido</th>
      <td>61.0</td>
      <td>6.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Normal</th>
      <td>5686.0</td>
      <td>4931.0</td>
      <td>5736.0</td>
      <td>3158.0</td>
      <td>4567.0</td>
    </tr>
    <tr>
      <th>Otros tipos de combustible</th>
      <td>521.0</td>
      <td>340.0</td>
      <td>508.0</td>
      <td>482.0</td>
      <td>586.0</td>
    </tr>
    <tr>
      <th>Premium</th>
      <td>1386.0</td>
      <td>2211.0</td>
      <td>3836.0</td>
      <td>1146.0</td>
      <td>1627.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
def heatmap_recuento_tipos(df, col1, col2):
    pivot_table = pivot_recuento(df,col1, col2, "year")
    sns.heatmap(pivot_table, annot=True, fmt='g')
    sns.plt.ylabel(col1)
    sns.plt.xlabel(col2)
    plt.show()
```


```python
interact(heatmap_recuento_tipos, col1=vehiculos.columns, col2=vehiculos.columns, df=fixed(vehiculos));
```



### Conclusiones

- Hay mas vehiculos de dos ruedas de bajo consumo que de traccion a las 4 ruedas
- Los fabricantes se concentran mas en vehiculos de motor pequeño/bajo consumo y motor muy grande/alto consumo
- La mayor parte de coches tienen transmision automatica, con los coches pequeños teniendo valores similares de coches automaticos y manuales
- Hay una cantidad de camionetas que son mas contaminantes que cualquier otro tipo de coche

### Medias por variables categóricas


```python
def medias_por_categoria(col_grupo, col_calculo):
    vehiculos.groupby(col_grupo)[col_calculo].mean().plot.barh()
    plt.ylabel(col_grupo)
    plt.xlabel('Valores medios de {}'.format(col_calculo))
    plt.show()
```


```python
columnas_numericas = vehiculos.select_dtypes(['int', 'float']).columns
columnas_categoricas = vehiculos.select_dtypes(['object', 'category']).columns
columnas_tipo = [col for col in vehiculos.columns if col.endswith("_tipo")]
```


```python
interact(medias_por_categoria, col_grupo=columnas_categoricas, col_calculo=columnas_numericas);
```



#### Conclusiones

- Vehiculos con transmision automatica tienen valores de co2 y consumo ligeramente más altos

- Furgonetas y camionetas tienen el consumo más alto (alrededor de 0.25 litros/milla). Por otra parte, los coches familiares y pequeños tienen el menor consumo de gasolina (~0.15 litros/milla)

- Los vehículos híbridos emiten menos de la mitad de CO2 que el resto de vehiculos (que tienen similares emisiones)

### Medias por multiples tipos


```python
def pivot_media(rows, columns, calc_field):
    df_pivot = vehiculos.pivot_table(values=calc_field, 
                              index=rows, 
                              columns=columns, 
                              aggfunc=np.mean
                             ).dropna(axis=0, how='all')
    return df_pivot
```


```python
pivot_media("combustible_tipo","clase_tipo", "co2")
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>clase_tipo</th>
      <th>Camionetas</th>
      <th>Coche Familiar</th>
      <th>Coches Grandes</th>
      <th>Coches Medianos</th>
      <th>Coches pequeños</th>
      <th>Deportivos</th>
      <th>Furgoneta</th>
      <th>Vehículos Especiales</th>
    </tr>
    <tr>
      <th>combustible_tipo</th>
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
      <th>Hibrido</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>221.875000</td>
      <td>127.380952</td>
      <td>149.645161</td>
      <td>260.222222</td>
      <td>106.000000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Normal</th>
      <td>560.216673</td>
      <td>399.493604</td>
      <td>461.726146</td>
      <td>409.673286</td>
      <td>384.393158</td>
      <td>476.788251</td>
      <td>590.807827</td>
      <td>543.838453</td>
    </tr>
    <tr>
      <th>Otros tipos de combustible</th>
      <td>552.958788</td>
      <td>391.161924</td>
      <td>447.490631</td>
      <td>412.662543</td>
      <td>348.957271</td>
      <td>520.672914</td>
      <td>602.867693</td>
      <td>559.031182</td>
    </tr>
    <tr>
      <th>Premium</th>
      <td>644.975464</td>
      <td>439.247746</td>
      <td>520.511823</td>
      <td>479.033374</td>
      <td>467.943014</td>
      <td>515.605886</td>
      <td>547.793508</td>
      <td>599.268790</td>
    </tr>
  </tbody>
</table>
</div>




```python
def heatmap_medias_tipos(col1, col2, col3):
    pivot_table = pivot_media(col1, col2, col3)
    sns.heatmap(pivot_table, annot=True, fmt='g')
    sns.plt.ylabel(col1)
    sns.plt.xlabel(col2)
    plt.show()
```


```python
interact(heatmap_medias_tipos, col1=vehiculos.columns, col2=vehiculos.columns, col3=columnas_numericas);
```



#### Conclusiones

- Camionentas de gasolina Premium consumen un 38% más que vehiculos pequeños que usan el mismo tipo de gasolina

### Comparacion de tendencias (temporales)

En este dataset en particular, tenemos una variable temporal `year`. A la cual echamos un vistazo en un apartado anterior pero que conviene observar de nuevo. Podemos considerarla una variable ordinal (ya que no es una variable continua). 

Para la cual tiene sentido ver la evolución. Para ello graficos de linea son lo ideal.


```python
vehiculos_pre_2017 = vehiculos.query("year<2017")
```


```python
vehiculos_pre_2017.groupby('year')['co2'].mean().plot()
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7f2cec6fab70>




    
![png](index_files/index_30_1.png)
    


Vemos que en general la emisión de co2 se ha reducido bastante con el tiempo


```python
def evolución_medias(col_calculo):
    vehiculos_pre_2017.groupby('year')[col_calculo].mean().plot()
    plt.show()
```


```python
interact(evolución_medias, col_calculo=columnas_numericas);
```



Vemos que históricamente se ha ido aumentando la cilindrada (y desplazamiento). en los vehiculos fabricados, pero a partir de 2010 esta tendencia se invierte. Vemos que ambas variables estan linealmente relacionadas.

Tambien vemos que el consumo y emision de co2 ha ido bajando a lo largo de los años, y dicha tendencia se acentuó a partir de 2006 (¿Cambio climatico?, la emisión de [Una Verdad Incomoda](http://www.imdb.com/title/tt0497116/)?)


```python
vehiculos.plot.scatter(x="cilindros",y="desplazamiento")
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7ff364dd0ba8>




    
![png](index_files/index_35_1.png)
    



```python
def evolución_recuento(col_calculo):
    for categoria in vehiculos_pre_2017[col_calculo].unique():
        n_vehiculos_categoria_ano = vehiculos_pre_2017[vehiculos_pre_2017[col_calculo]==categoria].groupby(
            'year').apply(np.size)
        plt.plot(
            n_vehiculos_categoria_ano.index,
            n_vehiculos_categoria_ano,
            label=categoria
        )
        plt.legend()
```


```python
evolución_recuento("clase_tipo")
```


    
![png](index_files/index_37_0.png)
    


Una vez hemos terminado el análisis, el paso final es compilar toda la información obtenida en un documento. Dicho documento tiene dos objetivos principales:

- Informar a aquellas personas interesadas de los descubrimientos encontrados. ¿Esto nos incluye a nosotros mismos en el futuro!
- Facilitar la replicación del análisis por otros Data Scientists.


# Conclusiones del análisis


#### Descripción

El dataset consiste en información relativa a vehículos vendidos en USA desde 1985. Dicha información incluye detalles técnicos (cilindrada, tipo de transmisión) y detalles medioambientales (consumo de gasolina, emisiones de CO2)

El archivo original está en: https://www.fueleconomy.gov/feg/epadata/vehicles.csv.zip
El archivo que vamos a usar es una versión modificada (con menos columnas)

Descripcion del dataset Original
http://www.fueleconomy.gov/feg/ws/index.shtml#ft7

Las entidades de las que consta dicho dataset son:

* fabricante
* fabricante-modelo
* fabricante-model-año
* fabricante-año

Las variables que existen en dicho dataset son:

```
fabricante         categorica
modelo             categorica
year               ordinal/numérica
desplazamiento     numérica
cilindros          numérica
transmision        categorica
traccion           categorica
clase              categorica
combustible        categorica
consumo            numérica
co2                numérica
```

#### QA

- Las variables desplazamiento, cilindros, transmision y traccion tienen valores inexistentes
- hay un outlier en las variables `co2` y `consumo`
- Hay coches hibridos y coches electricos (hemos removido estos ultimos ya que no contaminan).
- La variable `consumo` esta definida en millas por galon y la variable `co2` está definida como gramos por milla. Dado que el co2 es la variable principal del dataset, hemos creado la variable `consumo_litros_milla` definida como litros por milla para poder comparar con `co2`

#### Distribución de variables

- Ninguna variable numérica sigue una distribución normal

- la variable numérica `cilindros` tiene una distribución de valores discretos no balanceada (cilindrada de 2 y 4 y 8 suman el 95% de los vehiculos). Podria agruparse como variable categórica (2, 4 , 8 y otro)

- El fabricante con la mayor cantidad de modelos es Chevrolet (10% del total)

- 65% de los vehiculos usan gasolina normal

- La distribución de tamaños de motor y de consumo y co2 está equilibrada en todo el rango

- 70% de los vehiculos usan traccion a las dos ruedas

- dos tercios de los coches tienen transmision automática

- La clase mayoritaria de vehiculos es la de coches pequeños (35% del total)

- Existen relaciones lineales entre cilindros/desplazamiento y co2/consumo_litros_milla

#### Comparaciones

- Hay mas vehiculos de dos ruedas de bajo consumo que de traccion a las 4 ruedas
- Los fabricantes se concentran mas en vehiculos de motor pequeño/bajo consumo y motor muy grande/alto consumo
- La mayor parte de coches tienen transmision automatica, con los coches pequeños teniendo valores similares de coches automaticos y manuales
- Hay una cantidad de camionetas que son mas contaminantes que cualquier otro tipo de coche
- Vehiculos con transmision automatica tienen valores de co2 y consumo ligeramente más altos
- Furgonetas y camionetas tienen el consumo más alto (alrededor de 0.25 litros/milla). Por otra parte, los coches familiares y pequeños tienen el menor consumo de gasolina (~0.15 litros/milla)
- los valores de co2 son similares  independientemente del tipo de gasolina empleado
- Camionentas de gasolina Premium consumen un 38% más que vehiculos pequeños que usan el mismo tipo de gasolina
- El consumo y emisión de co2 han ido bajando de forma continuada desde 1985
- Históricamente se ha ido aumentando la cilindrada en los vehiculos fabricados, pero a partir de 2010 esta tendencia se invierte


```python

```
