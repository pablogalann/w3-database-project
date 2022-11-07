# W3 Project - Building mySQL Data-base 

![pp](https://github.com/pablogalann/w3-database-project/blob/main/imagenes/portada/claves-crear-buena-base-datos.jpg)


El objetivo del proyecto de esta semana consiste en crear una base de datos a partir de archivos csv, siendo esta misma fiable, consistente y con unas interraciones ajustadas a la idea de negocio. En este caso deducimos a partir de los datos proporcionados que se trata de un videoclub

## Planificación del ejercicio

1. Analisis de los datos proporcionados en .csv

2. Exploración y limpieza de datos, para lo obtención de tablas fiables y consistentes, mediante el uso de python

3. Exportacion de las tablas desde python a mySQL workbench

4. Creacion de una estructura fiable de interrelacion entre las diferentes tablas, representativa del negocio en cuestión

5. Consulta de datos en función de unos parametros determinados.


## Analisis de los datos proporcionados.

- Partiendo de los siete archivos .csv dados, establecemos que cada uno de ellos correspondera a una tabla asociada al nombre establecido y  que posteriormente se exportara a mySQL para la creación de la base de datos.

Los datos presentados son los siguientes:

- Actors: Tabla que representa el listado de actores, nombre, apellido y id
- Films: Tabla, muy completa, donde se incluye información propia de las peliculas, como es una breve descripcion, titulo, precio, duración del alquiler etc
- Categoría: Género
- Language: idioma 
- Inventory: inventario
- Rental: Aspectos relacionados con el alquiler de las peliculas
- Oldhdd: Tabla puente entre actores y peliculas, información mixta de ambos campos


## Exploración y limpieza


Para el desarrollo de esta actividad, utilizaremos siguientes procesos, empleandolos de la manera más adecuada en función de la necesidad de cada campo/tabla 

1. VISUALIZACION DE INFORMACION GENERAL: .head .info, .shape .columns
2. MODIFICACION TITULOS DE LAS COLUMNAS: Queremos evitar espacios y diferencias entre mayusculas y minusculas. 
3. LOCALIZACION VALORES NULOS, en el caso que nos compete no existen demasiados nulos
4. MODIFICACIÓN DE VALORES NULOS E INCONSISTENTES
5. LOCALIZACIÓN Y LIMPIEZA DE VALORES CONSTANTE, en el caso de nos compete existen varios columnas a los largo de las tablas con valor cte.

Es principalmente en el punto nº5 donde se concentra la mayor parte de esfuerzos de limpieza, por la existencia de numerosos valores constante que no aportan una información diferencial con respecto al resto. Un caso siginificativo es el caso de la tabla Film, como veremos a continuación, en el que se eliminan hasta 3 columnas

![limp](https://github.com/pablogalann/w3-database-project/blob/main/imagenes/capturas%20_limpieza/cte_film.PNG).

Pensando en las futuras relaciones entre tablas, tambien se busca la creacion de columnas comunes en aquellas que no tienen, buscando el nexo de unión en las columnas de _id, es el caso de la tabla old_hdd, donde se le añade la columna actor_id y film_id, para establecer una conexion directa con actores y film, utilizandola como puente entre ambas 

![limpo](https://github.com/pablogalann/w3-database-project/blob/main/imagenes/capturas%20_limpieza/old_hdd_nuevas.PNG).


## Exportación de los datos a mySQL y creacion de la base de datos 'videoclub'

La exportación de los datos se hace directamente desde python, utilizando el modulo sqlalchemy, donde cada data frame representará una de las tabla de la base de datos, previa conexion con el servidor.

    nombre_dataframe_pandas.to_sql(name='nombre_tabla_basedatos', con=cursor, if_exists='replace', index=False)

![imp](https://github.com/pablogalann/w3-database-project/blob/main/imagenes/capturas%20_limpieza/importacion.PNG).

Una vez introducidos los dataframe con sus datos limpios, la siguiente imagen en el diagrama EER es una serie de tablas con unas relaciones por definir, que pasaremos a realizarlas en el siguiente paso.

![pre](https://github.com/pablogalann/w3-database-project/blob/main/imagenes/relaciones/prerelaciones.PNG).


## Estructura relacional entre tablas de la base de datos 'videoclub'

A partir de la información obtenida durante los pasos anteriores, se procede a vincular las tablas entre ellas, de tal forma que represente una idea real del negocio, según todos los elementos que aparecen en él.

Con anterioridad se trato de incluir columnas de _ids para facilitar una unión fiable entre ellas, como se ve a continuación 

![pre](https://github.com/pablogalann/w3-database-project/blob/main/imagenes/relaciones/relaciones.PNG).


## Queries

Consultas realizadas, una vez establecida la base de datos.

¿Cúales son mas las peliculas más largas y mas caras?

![q1](https://github.com/pablogalann/w3-database-project/blob/main/imagenes/queries/Q1.PNG).

¿En que peliculas de terror aparece de la actriz Penelope Guinness?

![q2](https://github.com/pablogalann/w3-database-project/blob/main/imagenes/queries/Q2.PNG).

¿Para noche de Halloween cuantas peliculas de terror se alquilaron? *fecha ficticia sobra hay fechas de mayo

![q3](https://github.com/pablogalann/w3-database-project/blob/main/imagenes/queries/Q3.PNG).

¿Cual es la duración media de las peliculas del actor Bob fawcett?

![q4](https://github.com/pablogalann/w3-database-project/blob/main/imagenes/queries/Q4.PNG).

¿Que clientes alquilaron la pelicula 'Bucket brotherhood' en la tienda 2?

![q5](https://github.com/pablogalann/w3-database-project/blob/main/imagenes/queries/Q5.PNG).

¿Que peliculas baratas tienen mayor disponibilidad?

![q5](https://github.com/pablogalann/w3-database-project/blob/main/imagenes/queries/Q6.PNG).






