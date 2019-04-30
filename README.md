# House Prices: Análisis exploratorio de datos con Python

Previamente publicado en https://www.kaggle.com/abonaplata/analisis-exploratorio-de-datos-con-python/

El estudio previo de los datos o EDA es una etapa crítica en la ciencia de datos, y sin duda la que consume más tiempo.

Siguiendo los pasos de [Pedro Marcelino](https://www.kaggle.com/pmarcelino), que a su vez seguía el capítulo 'Examining your data' de [Hair et al. (2013)](https://www.amazon.com/gp/product/9332536503/), voy a realizar un completo análisis del conjunto de datos [House Prices: Advanced Regression Techniques](https://www.kaggle.com/c/house-prices-advanced-regression-techniques) de Kaggle, que espero que resulte útil a la comunidad.

Voy a dividir el análisis en los siguientes apartados:

1. Comprender el problema
2. Estudio univariable
3. Estudio multivariable
4. Limpieza básica de los datos
5. Comprobación de suposiciones

# 1. El problema

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


