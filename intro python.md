# Rapida Introducción a Colab

Para trabajar en Colab y usar las herramientas de Python, se requiere en primera instancia crear o tener una cuenta de google activa. Para ingresar a Colaboratory se requiere acceder al siguiente link: <https://colab.research.google.com>. 

Para abrir un nuevo cuaderno, se ingresa a archivo / nuevo cuaderno y se abre un documento que por defecto se puede llamar "untitled0.ipynb". Este documento ya esta listo para codificar.

En la pagina de codificación se puede apreciar un par de botones llamados `+codigo` y `+texto`. Si se presiona `+codigo`se abre una nueva sección de código para trabajar, así mismo si se presiona `+texto`, se da espacio para redactar observaciones de código o procedimientos.

## Antes de comenzar, instale los siguientes paquetes para Econometría

Para realizar con comodidad las operaciones habituales de Econometría financiera se recomienda instalar las siguientes dependencias:

```markdown
!pip install --upgrade quandl
!pip install numpy pandas matplotlib scipy statmodels pandas_datareader
```
Algunas dependencias como `quandl`no están preinstaladas virtualmente en colab, por tanto, se hace necesario instalarlas con la función `!pip install --`.  Una vez resueltas instale los siguientes paquetes.

```markdown
#bases de importación
import json
import quandl
import pandas as pd
import pandas_datareader as pdr
import datetime as dt
import numpy as np
import scipy.stats as stats
import statsmodels.formula.api as smf
import statsmodels.api as sm
import statsmodels.stats.api as sms
import statsmodels.tsa.api as smt
import statsmodels.tsa.seasonal as sdc
import matplotlib.pyplot as plt

#bases de función
from statsmodels.compat import lzip
from statsmodels.graphics.tsaplots import plot_acf, plot_pacf
from statsmodels.tsa.stattools import adfuller, kpss
from statsmodels.stats.diagnostic import acorr_ljungbox
from statsmodels.tsa.arima.model import ARIMA
```

## Algunas consideraciones...

- Colab trabaja en un entorno de compilación que requiere mostrar los resultados con la función `print()`, esto puede ser un poco engorroso y por tanto se hace diferente en la forma de mostrar los resultados de R o de STATA.
- La compilación puede ser mas cómoda, pero a su vez no todos los códigos son intuitivos.
- La muestra de resultados puede ser visualmente mas agradable que en R.
- El uso del manejo de datos se debe realizar en .csv.
- El manejo de Colab es muy cómodo para los estudiantes y sus equipos, no requieren instalar programas o aplicaciones adicionales. Solo se requiere tener conexión a internet.
- Colab esta basado en Jupyter (otra plataforma virtual muy usada para Python), por tanto el entorno y el manejo es idéntico y no causaría problemas en caso de migración de entorno.
- Existen paquetes en R que permiten trabajar en compilación python y que en entorno R-Studio se hacen mas prácticos, pero requieren de instalación de R lo cual seria poco provechoso.

## Comandos básicos para ingresar datos y lectura de base de datos

### Como cargar una base de datos:

Como se indicó anteriormente, Python es mas eficiente usando .csv (esto realmente no es una limitante, es mas un requerimiento de programa que R tiene mas depurado al usar texto plano o archivos mas graficos como .xls). 

Para ello se usará el comando que abre la pestaña de pregunta de documento, que permite importar una base de datos: 

```
from google.colab import files
uploaded = files.upload()
data = "nombre del archivo cargado"
```

En caso de utilizar otro software y un método mas directo de importación, se sugiere usar:

```
df=pd.read_csv(r'ruta del archivo en directorio',sep="\t")
data=pd.DataFrame(df)
```

### Convertir la base de datos en serie de tiempo

Para convertir una serie de información que dependa del tiempo, se puede utilizar el comando `pd.to_datetime` y señalar la columna de información de la base de datos para que reconozca que dicha columna representa una serie temporal y que las demas columnas están atadas a estas fechas.
```
data['date'] = pd.to_datetime(data['date'])
data = data.set_index('date')
```
### Manipular las columnas

En caso de requerir manipular columnas de información se pueden utilizar los siguientes:
```
data['gm']
data[['gm','nflx']]
data[['gm','nflx','nyse']]

#or

data.iloc[:,0]
data.iloc[:,[0,1]]
data.iloc[:,[0,1,2]]
```
.iloc es un codigo que permite rastrear en una matriz de información las columnas o filas.

### Estadística básica
Así como en R, Python ofrece alternativas de obtener información estadística descriptiva básica con el siguiente código:
```
data.describe()
```
