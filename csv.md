Uno de los usos más frecuentes de la biblioteca Pandas es la lectura de datos a partir de archivos CSV o hojas de cálculo (como Excel). Muchas empresas almacenan sus datos en estos formatos. En esta clase aprenderás cómo leer un archivo CSV y convertirlo en un DataFrame de Pandas, para después convertirlo a un Document de LangChain.

Para el seguimiento de la clase utiliza la Notebook 2 del curso en la sección CSV a Pandas DataFrame.

Instalación de Pandas

Primero, necesitaremos instalar la biblioteca de Pandas, si aún no está instalada en tu entorno. Puedes hacer esto descomentando y ejecutando la siguiente celda:


# !pip install pandas
Lectura de archivos CSV

Una vez que tengas instalada la biblioteca Pandas, podemos empezar a leer archivos CSV. Para esto, utilizaremos el método read_csv() proporcionado por Pandas.

Supongamos que tenemos un archivo CSV llamado repos_cairo.csv. Descarga este archivo en este enlace.

Podemos leer el archivo de la siguiente manera:


import pandas as pd

df = pd.read_csv('repos_cairo.csv')
df es ahora un DataFrame de Pandas que contiene los datos de nuestro archivo CSV. Podemos visualizar las primeras líneas de nuestro DataFrame utilizando el método head.


df.head()
Cargando datos de un DataFrame a Langchain

A continuación, vamos a utilizar la clase DataFrameLoader de LangChain para cargar los datos de nuestro DataFrame.


from langchain.document_loaders import DataFrameLoader

loader = DataFrameLoader(df, page_content_column="repo_name")
data = loader.load()
Finalmente, vamos a imprimir el tipo y la longitud de nuestros datos cargados.


print(f"El archivo es de tipo {type(data)} y tiene una longitud de {len(data)} debido a la cantidad de observaciones en el CSV.")
Y vamos a imprimir las primeras 5 líneas de nuestros datos.


from pprint import pprint

pprint(data[:5])
Como ves es bastante similar a cargar un PDF a LangChain. Te recuerdo que en la documentación de Document Loaders de LangChain, puedes ver todas las integraciones para cargar diferentes tipos de archivos.