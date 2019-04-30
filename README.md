# House Prices: Análisis exploratorio de datos con Python

Previamente publicado en [Kaggle Kernels](https://www.kaggle.com/abonaplata/analisis-exploratorio-de-datos-con-python/).

El estudio previo de los datos o EDA es una etapa crítica en la ciencia de datos, y sin duda la que consume más tiempo.

Siguiendo los pasos de [Pedro Marcelino](https://www.kaggle.com/pmarcelino), que a su vez seguía el capítulo 'Examining your data' de [Hair et al. (2013)](https://www.amazon.com/gp/product/9332536503/), voy a realizar un completo análisis del conjunto de datos [House Prices: Advanced Regression Techniques](https://www.kaggle.com/c/house-prices-advanced-regression-techniques) de Kaggle, que espero que resulte útil a la comunidad.

Voy a dividir el análisis en los siguientes apartados:

1. Comprender el problema
2. Estudio univariable
3. Estudio multivariable
4. Limpieza básica de los datos
5. Comprobación de suposiciones

## 1. El problema

Para entender realmente el conjunto de datos, voy a estudiar el significado y la relevancia de cada variable con respecto al problema. Intentaré responder a diversas cuestiones sobre ellas, como:

* La relevancia de la variable en la compra de una casa.
* La importancia de la variable.
* Solapamiento con otras variables.

En la competición de Kaggle 'House prices' se indica que el problema es la predicción del precio de las viviendas, por lo que la variable objetivo es 'SalePrice'. Las demás variables se describen de la siguiente manera:

* <b>MSSubClass</b>: clase de construcción
* <b>MSZoning</b>: clasificación de la zona
* <b>LotFrontage</b>: pies lineales de calle de la parcela
* <b>LotArea</b>: tamaño de la parcela en pies cuadrados
* <b>Street</b>: tipo de acceso por carretera
* <b>Alley</b>: tipo de acceso al callejón
* <b>LotShape</b>: forma de la parcela
* <b>LandContour</b>: planitud de la parcela
* <b>Utilities</b>: servicios públicos disponibles
* <b>LotConfig</b>: Configuración de parcela
* <b>LandSlope</b>: pendiente de la parcela
* <b>Neighborhood</b>: ubicación física dentro de los límites de la ciudad de Ames
* <b>Condition1</b>: proximidad a la carretera principal o al ferrocarril
* <b>Condition2</b>: proximidad a la carretera principal o al ferrocarril (si hay un segundo)
* <b>BldgType</b>: tipo de vivienda
* <b>HouseStyle</b>: estilo de vivienda
* <b>OverallQual</b>: calidad general del material y del acabado
* <b>OverallCond</b>: condición general
* <b>YearBuilt</b>: fecha original de construcción
* <b>YearRemodAdd</b>: fecha de remodelación
* <b>RoofStyle</b>: tipo de cubierta
* <b>RoofMatl</b>: material del techo
* <b>Exterior1st</b>: revestimiento exterior de la casa
* <b>Exterior2nd</b>: revestimiento exterior de la casa (si hay más de un material)
* <b>MasVnrType</b>: tipo de revestimiento de mampostería
* <b>MasVnrArea</b>: área de revestimiento de mampostería en pies cuadrados
* <b>ExterQual</b>: calidad del material exterior
* <b>ExterCond</b>: estado del material en el exterior
* <b>Foundation</b>: tipo de cimentación
* <b>BsmtQual</b>: altura del sótano
* <b>BsmtCond</b>: estado general del sótano
* <b>BsmtExposure</b>: paredes del sótano a nivel de calle o de jardín
* <b>BsmtFinType1</b>: calidad del área acabada del sótano
* <b>BsmtFinSF1</b>: pies cuadrados de la superficie acabada tipo 1
* <b>BsmtFinType2</b>: calidad de la segunda superficie acabada (si existe)
* <b>BsmtFinSF2</b>: Pies cuadrados de la superficie acabada tipo 2
* <b>BsmtUnfSF</b>: pies cuadrados del área sin terminar del sótano
* <b>TotalBsmtSF</b>: pies cuadrados totales del sótano
* <b>Heating</b>: tipo de calefacción
* <b>HeatingQC</b>: calidad y estado de la calefacción
* <b>CentralAir</b>: aire acondicionado central
* <b>Electrical</b>: sistema eléctrico
* <b>1erFlrSF</b>: área en pies cuadrados de la primera planta (o planta baja)
* <b>2ndFlrSF</b>: área en pies cuadrados de la segunda planta
* <b>LowQualFinSF</b>: pies cuadrados acabados de baja calidad (todos los pisos)
* <b>GrLivArea</b>: superficie habitable por encima del nivel del suelo en pies cuadrados
* <b>BsmtFullBath</b>: cuartos de baño completos en el sótano
* <b>BsmtHalfBath</b>: medio baño del sótano
* <b>FullBath</b>: baños completos sobre el nivel del suelo
* <b>HalfBath</b>: medios baños sobre el nivel del suelo
* <b>Bedroom</b>: número de dormitorios por encima del nivel del sótano
* <b>Kitchen</b>: número de cocinas
* <b>KitchenQual</b>: calidad de la cocina
* <b>TotRmsAbvGrd</b>: total de habitaciones por encima del nivel del suelo (no incluye baños)
* <b>Functional</b>: valoración de la funcionalidad de la vivienda
* <b>Fireplaces</b>: número de chimeneas
* <b>FireplaceQu</b>: calidad de la chimenea
* <b>GarageType</b>: ubicación del garaje
* <b>GarageYrBlt</b>: año de construcción del garaje
* <b>GarageFinish</b>: acabado interior del garaje
* <b>GarageCars</b>: tamaño del garaje en capacidad de coches
* <b>GarageArea</b>: tamaño del garaje en pies cuadrados
* <b>GarageQual</b>: calidad de garaje
* <b>GarageCond</b>: condición de garaje
* <b>PavedDrive</b>: calzada asfaltada
* <b>WoodDeckSF</b>: area de plataforma de madera en pies cuadrados
* <b>OpenPorchSF</b>: área de porche abierto en pies cuadrados
* <b>EnclosedPorch</b>: área de porche cerrada en pies cuadrados
* <b>3SsnPorch</b>: área de porche de tres estaciones en pies cuadrados
* <b>ScreenPorch</b>: superficie acristalada del porche en pies cuadrados
* <b>PoolArea</b>: área de la piscina en pies cuadrados
* <b>PoolQC</b>: calidad de la piscina
* <b>Fence</b>: calidad de la valla
* <b>MiscFeature</b>: característica miscelánea no cubierta en otras categorías
* <b>MiscVal</b>: valor en dólares de la característica miscelánea
* <b>MoSold</b>: mes de venta
* <b>YrSold</b>: año de venta
* <b>SaleType</b>: tipo de venta
* <b>SaleCondition</b>: Condiciones de venta

## 2. Análisis univariable: 'SalePrice'

La variable 'SalePrice' es la variable objetivo de este conjunto de datos. En pasos posteriores a este análisis exploratorio de datos se realizaría una predicción del valor de esta variable, por lo que voy a estudiarla con mayor detenimiento. A simple vista se pueden apreciar:

* Una desviación con respecto a la distribución normal.
* Una asimetría positiva.
* Algunos picos.

### Resumiendo:

* 'GrLivArea' y 'TotalBsmtSF' mantienen una relación lineal positiva con 'SalePrice', aumentando en el mismo sentido. En el caso de 'TotalBsmtSF', la pendiente de esta relación es muy acentuada.
* 'OverallQual' y 'YearBuilt' también parecen relacionadas con 'SalePrice' (más fuerte en el primer caso), tal y como se puede observar en los diagramas de cajas.

Sólo he explorado cuatro variables, pero hay muchas otras a analizar.


## 3. Análisis multivariable

Hasta ahora sólo me he dejado llevar por la intuición para el análisis de las variables que he creído importantes. Es hora de un análisis más objetivo.

Para ello voy a realizar las siguientes pruebas de correlación:
* Matriz de correlación general: El mapa de calor es una forma visual muy útil para para conocer las variables y sus relaciones. A primera vista hay dos variables que llaman la atención: 'TotalBsmtSF' y '1stFlrSF', seguidas por las variables 'Garage*X*'. En ambos casos parece haber una correlación significativa; en realidad es tan fuerte que podría indicar multicolinealidad, es decir, que básicamente ofrecen la misma información. Con respecto a las correlaciones de la variable 'SalePrice', destacan las vistas anteriormente ('GrLivArea', 'TotalBsmtSF' y 'OverallQual'), pero hay otras que también deberían ser tenidas en cuenta.
* Matriz de correlación centrada en la variable 'SalePrice': En estas matrices de correlación se puede observar:
** 'OverallQual', 'GrLivArea' y 'TotalBsmtSF' están fuertemente correladas con 'SalePrice'.
** 'GarageCars' y 'GarageArea' también están fuertemente correladas pero, como he comentado anteriormente, el número de coches que se pueden aparcar en un garaje es una consecuencia de su superficie. Es por esto que sólo voy a mantener una de estas variables en el análisis, 'GarageCars', ya que está más correlada con 'SalePrice'.
** 'TotalBsmtSF' y '1stFloor' plantean la misma situación. En este caso mantendré 'TotalBsmtSF'.
** 'FullBath' también está correlada con 'SalePrice'. Parece que a la gente le gusta darse un baño en casa...
** 'TotRmsAbvGrd' y 'GrLivArea', otro caso de multicolinealidad.
** 'YearBuilt' también está ligeramente correlada con 'SalePrice'. 
* Diagramas de dispersión entre las variables más correladas.


## 4. Limpieza de datos

### Datos desaparecidos

Antes de tratar los datos faltantes o missing values, es importante determinar su prevalencia y su aleatoriedad, ya que pueden implicar una reducción del tamaño de la muestra. También hay que asegurarse que la gestión de los datos desaparecidos no esté sesgada o esconda una verdad incómoda.

Por razones prácticas voy a eliminar las variables con más de un 15% de datos faltantes (p.ej. 'PoolQC', 'MiscFeature', 'Alley', etc.); no creo que las echemos de menos, no parecen aspectos importantes a considerar al comprar una casa.

Con respecto a las variables 'Garage*X*', observo el mismo número de datos desaparecidos, hecho que quizás habría que estudiar con más detenimiento. Pero, dado que la información más relevante en cuanto al garaje ya está recogida por la variable 'GarageCars', y que sólo se trata de un 5% de datos faltantes, borraré las citadas variables 'Garage*X*', además de las 'Bsmt*X*' bajo la misma lógica.

En cuanto a las variables 'MasVnrArea' y 'MasVnrType', se puede decir que no son esenciales y que, incluso, tienen una fuerte correlación con 'YearBuilt' y 'OverallQual'. No parece que se vaya a perder mucha información si elimino 'MasVnrArea' and 'MasVnrType'.

Para finalizar, encuentro un dato faltante en la variable 'Electrical'. Ya que sólo se trata de una observación, voy a borrarla y a mantener la variable.

En resumen, voy a borrar todas las variables con datos desaparecidos, excepto la variable 'Electrical'; en este caso sólo voy a borrar la observación con el dato faltante.

### Datos atípicos

Los datos atípicos u outliers pueden afectar marcadamente el modelo, además de suponer una fuente de información en sí misma. Su tratamiento es un asunto complejo que requiere más atención; por ahora sólo voy a hacer un análisis rápido a través de la desviación estándar de la variable 'SalePrice' y a realizar un par de diagramas de dispersión.

#### Análisis univariable

La primera tarea en este caso es establecer un umbral que defina una observación como valor atípico. Para ello voy a estandarizar los datos, es decir, transformar los valores datos para que tengan una media de 0 y una desviación estándar de 1.

* Los valores bajos son similares y no muy alejados del 0.
* Los valores altos están muy alejados del 0. Los valores superiores a 7 están realmente fuera de rango.

#### Análisis bivariable

Este diagrama de dispersión muestra un par de cosas interesantes:

* Los dos valores más altos de la variable 'GrLivArea' resultan extraños. Sólo puedo especular, pero podría tratarse de terrenos agrícolas o muy degradados, algo que explicaría su bajo precio. Lo que está claro es que estos dos puntos son atípicos, por lo que voy a proceder a eliminarlos.
* Las dos observaciones más altas de la variable 'SalePrice' se corresponden con las que observamos en el análisis univariable anterior. Son casos especiales, pero parece que siguen la tendencia general, por lo que voy a mantenerlas.

Aunque se pueden observar algunos valores bastante extremos (p.ej. TotalBsmtSF > 3000), parece que conservan la tendencia, por lo que voy a mantenerlos.


## 5. Comprobación de normalidad

Ya he realizado cierta limpieza de datos y estudiado la variable 'SalePrice'. Ahora voy a comprobar si 'SalePrice' cumple las asunciones estadísticas que nos permiten aplicar las técnicas del análisis multivariable.

De acuerdo con [Hair et al. (2013)](https://www.amazon.com/gp/product/9332536503/), hay que comprobar cuatro suposiciones fundamentales:

* <b>Normalidad</b> - Cuando hablamos de normalidad lo que queremos decir es que los datos deben parecerse a una distribución normal. Es importante porque varias pruebas estadísticas se basan en esta suposición. Sólo voy a comprobar la normalidad de la variable 'SalePrice', aunque resulte un tanto limitado ya que no asegura la normalidad multivariable. Además, si resolvemos la normalidad evitamos otros problemas, como la homocedasticidad.

* <b>Homocedasticidad</b> - La homocedasticidad se refiere a la suposición de que las variables dependientes tienen el mismo nivel de varianza en todo el rango de las variables predictoras, según [(Hair et al., 2013)](https://www.amazon.com/gp/product/9332536503/). La homocedasticidad es deseable porque queremos que el término de error sea el mismo en todos los valores de las variables independientes.

* <b>Linealidad</b>- La forma más común de evaluar la linealidad es examinar los diagramas de dispersión y buscar patrones lineales. Si los patrones no son lineales, valdría la pena explorar las transformaciones de datos. Sin embargo, no voy a entrar en esto porque la mayoría de los gráficos de dispersión que hemos visto parecen tener relaciones lineales.

* <b>Ausencia de errores correlacionados</b> - Esto ocurre a menudo en series temporales, donde algunos patrones están relacionados en el tiempo. Tampoco voy a tocar este asunto.

### En búsqueda de la normalidad

El objetivo es estudiar la variable 'SalePrice' de forma fácil, comprobando:

* <b>Histograma</b> - Curtosis y asimetría.
* <b>Gráfica de probabilidad normal</b> - La distribución de los datos debe ajustarse a la diagonal que representa la distribución normal.

De estos gráficos se desprende que 'SalePrice' no conforma una distribución normal. Muestra picos, asimetría positiva y no sigue la línea diagonal; aunque una simple transformación de datos puede resolver el problema. 

Terminado el trabajo con 'SalePrice', voy a seguir con 'GrLivArea'. La variable 'GrLivArea' muestra asimetría.

Prosigo con el estudio de la variable 'TotalBsmtSF'. Estos gráficos nos muestran que la variable 'TotalBsmtSF':

* Presenta asimetrías.
* Hay un número significativo de observaciones con valor cero (casas sin sótano).
* El valor cero no nos permite hacer transformaciones logarítmicas.

Para aplicar una transformación logarítmica, crearé una variable binaria (tener o no tener sótano). Después, aplicaré la transformación logarítmica a todas las observaciones que no sean cero, ignorando aquellas con valor cero. De esta manera podré transformar los datos, sin perder el efecto de tener o no sótano.

### En búsqueda de la homocedasticidad

El mejor método para probar la homocedasticidad para dos variables métricas es de forma gráfica. Las desviaciones de una dispersión uniforme se muestran mediante formas tales como conos (pequeña dispersión a un lado del gráfico, gran dispersión en el lado opuesto) o diamantes (un gran número de puntos en el centro de la distribución).

Empiezo por 'SalePrice' y 'GrLivArea'. Las anteriores versiones de este gráfico de dispersión (antes de las transformaciones logarítmicas), tenían una forma cónica. Como puede apreciarse, el gráfico actual ya no tiene una forma cónica. Tan solo asegurando la normalidad en algunas variables, hemos resuelto el problema de la homocedasticidad.

Ahora vamos a comprobar 'SalePrice' con 'TotalBsmtSF'. Podemos decir que, en general, la variable 'SalePrice' muestra niveles equivalentes de varianza en todo el rango de 'TotalBsmtSF'.

Convierto las variables categóricas en variables ficticias o dummies.


## Conclusión

A lo largo de este kernel he puesto en práctica muchas de las estrategias propuestas por [Hair et al. (2013)](https://www.amazon.com/gp/product/9332536503/). He estudiado las variables, analizado 'SalePrice' a solas y con las variables más correladas, he lidiado con datos faltantes y valores atípicos, he probado algunos de los supuestos estadísticos fundamentales e incluso he transformado variables categoriales en variables dummy. Todo un abanico de técnicas en Python, usando las librerías [Pandas](https://pandas.pydata.org/), [Matplotlib](https://matplotlib.org/), [Seaborn](https://seaborn.pydata.org/), [NumPy](https://www.numpy.org/), [SciPy](https://www.scipy.org/) y [Scikit-learn](https://scikit-learn.org/stable/).

Se han quedado algunos asuntos en el tintero, pero no ha estado mal para empezar.

No quiero finalizar este ejercicio sin dar antes las gracias públicamente a Pedro Marcelino por su magnífico trabajo, del que éste es poco más que una traducción y retoque.


## Referencias
* [Pedro Marcelino](https://www.kaggle.com/pmarcelino)
* [Hair et al., 2013, Multivariate Data Analysis, 7th Edition](https://www.amazon.com/gp/product/9332536503/)


