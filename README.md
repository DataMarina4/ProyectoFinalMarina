# ProyectoFinalMarina

## Fuentes de datos: 

Se obtuvo una base de datos públicos construida sobre datos del ranking internacional de Forbes a través de Kaggle y dos bases de datos de 2010 y 2020 para hacer una comparación general.
La base de datos incluye datos exclusivamente relativos al ranking Forbes (puesto, valor total, nombre de la fortuna), datos personales (edad, sexo, fecha de nacimiento) e información geopolítica (país, datos económicos y sociales del país, etc.) que nos permitirán crear un contexto socio económico alrededor de cada fortuna.


## Hipótesis:

Originalmente se pretendía demostrar que la distribución de edad de los millonarios estaba decreciendo, pero al tomar como referencia los promedios de edad de 2010 (61,57 años) y 2020 (64,18 años) se observó que la tendencia era en aumento. Por lo que comprobaremos la continuidad de esta tendencia y analizaremos factores que nos permitan una visión más amplia ya que esta base es más completa que las ediciones anteriores.
Se pretende desarrollar un análisis demográfico, geográfico y comercial de los billonarios.
Demostrando lo siguiente:


A- La edad promedio de los millonarios continúa en aumento.
B- Hay una mayoría de hombres por sobre las mujeres en el ranking, si se comprueba estudiar la distribución por edad y el coeficiente selfmade.
C- La distribución geografía de los millonarios se centra en los países con mayor nivel de desarrollo
D- Tecnología y Finanzas son las industrias con más millonarios




## Preparación del dataset:
### Flujo de datos:

 ![image](https://github.com/DataMarina4/ProyectoFinalMarina/assets/96702261/93b3789d-5ac4-41ca-81dd-216ab67a40ea)


Antes de prepararlo subí una versión del Raw a BigQuery (capa bronce) para tenerla de respaldo.
Para preparar los datos para consumo realice los siguientes pasos. 

1- Hice una carga  previa en PowerQuery para visualizar la calidad de los datos y detecte que había datos faltantes que eran accesibles, valiéndome información pública de algunos países que no se encontraba correctamente completa y era fácilmente accesible.
También detecte que había mas registros únicos de los esperados en el campo country, por lo que al mirar en detalle encontré que territorios no independientes del reino unido (Islas vírgenes, Guernesey, etc.) que al carecer de datos acerca de las variables económicas territoriales decidí unificar a Reino unido. 
Complete con Excel la información faltante en el dataset y cambie los valores antes mencionados afectando a los siguientes campos:

•	country
•	cpi_country
•	cpi_change_country
•	gdp_country
•	gross_tertiary_education_enrollment
•	gross_primary_education_enrollment_country
•	life_expectancy_country
•	tax_revenue_country_country
•	total_tax_rate_country

2 – Cargue del csv actualizado a BigQuery.
3 – Limpie campos que no se utilizaran y cree una tabla adicional de referencias para el campo Status.
•	Date (fecha del ranking) era el mismo para todos.
•	State, solo estaba completo para USA.
•	Residence State reg, solo estaba completo para USA.
•	Birth Date, no es relevante.
•	Birth Month, no es relevante.
•	Birth Day, no es relevante.
•	Birth Year
•	Latitude country, no lo utilizaremos.
•	Longitude country, no lo utilizaremos.
•	Title, demasiado incompleto.

![image](https://github.com/DataMarina4/ProyectoFinalMarina/assets/96702261/204550e5-9b0c-40b3-a2a8-3e81f59122a0)


 
### Conecte BigQuery con PowerBI e importe el dataset.

### Modelo de datos:

![image](https://github.com/DataMarina4/ProyectoFinalMarina/assets/96702261/be4f53c0-8318-4070-aa0b-60e15bc2790d)

   
En este paso realice las adaptaciones para distribuir la información en tablas de hechos y dimensiones en PowerQuery, segmentación de la información y creación de relaciones, de acuerdo al modelo de datos.

### •	Facts
![image](https://github.com/DataMarina4/ProyectoFinalMarina/assets/96702261/b93971cd-2564-40eb-bbfa-1abc115080b7)

 
### •	Dim_Country
 ![image](https://github.com/DataMarina4/ProyectoFinalMarina/assets/96702261/baaf0a1f-ea98-4723-b8b1-2269cb79ba55)
![image](https://github.com/DataMarina4/ProyectoFinalMarina/assets/96702261/99a38785-993d-4cd6-9140-d019e66b5b93)

### •	Dim_Person
 ![image](https://github.com/DataMarina4/ProyectoFinalMarina/assets/96702261/9a6d0781-4165-451a-b216-b3995980b037)

### •	Dim_Status
 ![image](https://github.com/DataMarina4/ProyectoFinalMarina/assets/96702261/f54e2618-6a8e-4f23-a29f-24a8a19975de)

### •	Dim_Wealth
![image](https://github.com/DataMarina4/ProyectoFinalMarina/assets/96702261/f62f5ef7-a7bc-43eb-a774-2f87c9677adc)

 ## Para finalizar la capa Gold:
 
 Creación de columnas y ajuste de datos en PowerQuery
•	índice Wealth_ID (permite sortear que el ranking tiene posiciones compartidas)
•	Décadas (valor auxiliar para facilitar legibilidad de gráfico)
•	Cambio de valores en gdp_country para facilitar la muestra de unidades.
Creación de columnas dinámicas para apoyar a los gráficos
•	NombreCompleto
•	Rank_NombreCompleto
•	RealWorth para facilitar expresar unidades correctamente.

### Finalmente genére los  gráficos, medidas y reportes definidos por el plan de métricas.

![image](https://github.com/DataMarina4/ProyectoFinalMarina/assets/96702261/98e139db-fcdc-43ca-b86a-3396328fcd8e)
 ![image](https://github.com/DataMarina4/ProyectoFinalMarina/assets/96702261/6aa8dac0-222a-4e10-ba5a-40c6c73d8c47)

 
## Capturas de Dashbord y relaciones de datos en Power BI
 
![image](https://github.com/DataMarina4/ProyectoFinalMarina/assets/96702261/4bfbb2fb-210f-4901-8f2e-2574a8b7c30d)

![image](https://github.com/DataMarina4/ProyectoFinalMarina/assets/96702261/9f616c2b-0c1c-4e5f-b9ec-616095f8df40)

 ![image](https://github.com/DataMarina4/ProyectoFinalMarina/assets/96702261/e6c1780a-16f2-4597-b50f-10e9b1555399)

 ![image](https://github.com/DataMarina4/ProyectoFinalMarina/assets/96702261/73e47c63-5789-4b09-92e8-869972217bc8)

 ![image](https://github.com/DataMarina4/ProyectoFinalMarina/assets/96702261/9ce1b5d3-6645-414f-b55a-21c2206c6f04)
   
 ![image](https://github.com/DataMarina4/ProyectoFinalMarina/assets/96702261/6794c10c-549d-4664-94a2-46c5df8b7843)

 ![image](https://github.com/DataMarina4/ProyectoFinalMarina/assets/96702261/8bacbc09-a437-4652-a284-8de9ee7b415f)

![image](https://github.com/DataMarina4/ProyectoFinalMarina/assets/96702261/bfc7e3d9-0f1e-473b-8a2a-fb75eb400c9d)


## Conclusiones Generales: 

Se comprobó la primera hipótesis con respecto a la edad, continua aumentando la edad promedio en el ranking de billonarios ya que mantiene una tendencia creciente en comparación con las medidas anteriores.
También se corroboró la segunda hipótesis la cual afirmaba que existen más hombres que mujeres en el ranking, pero no hay diferencia significativa en las edades promedio (menor al 5%), si la hay en el coeficiente de selfmade, se visualiza una gran cantidad de hombres en la categoría selfmade.
Los países que lideran en cantidad de millonarios son los mismos que lo hacen en valor total, con marcada diferencia a favor de Estados unidos, China, la tendencia general indica que los países con mayor nivel de desarrollo tienen más millonarios y un mayor valor.
China se presenta como un caso excepcional con un valor total bajo en relación con su cantidad de billonarios, mientras que Francia hace el caso inverso.
Se corrobora parcialmente la última hipótesis. Las principales industrias que concentran la mayor cantidad de millonarios incluyen a finanzas y tecnología, pero quedan relegadas en cuanto a valor total. Otras áreas como el Juego, la Industria Automotriz, Textil-Retail y la Logística, generan más riqueza (en promedio).

# Enlace al dashboard:

https://app.powerbi.com/view?r=eyJrIjoiNWZlMzlkODYtMmMzMC00YTA0LTk3MDMtNzU1ZTM3YjVmNjY3IiwidCI6IjE4ZmMxNWE2LWM4YWYtNGY4Yy1hNWZhLTU3YWQ1ODBjYmRhZiIsImMiOjl9&pageName=ReportSection

