## Bienvenidos a Econometria Financiera en Python

Esta pagina esta dedicada a la creación del curso de Econometría Financiera en Python para el programa de Ingenieria Financiera del Instituto Tecnológico Metropolitano de Medellín (ITM).

En esta pagina encontrará los siguientes temas:

- Introducción a colab
- 
- Modelo lineal (Estimador de Minimos Cuadrados Ordinarios)
- Analisis de bondad de ajuste a modelos lineales
- Variables Categoricas
- Modelos de respuesta cualitativa (Modelos Logit, Probit y MLP)

- Introducción a series de tiempo
- Descomposición de series de tiempo
- Modelos ARIMA 
- Modelos SARIMA
- Modelos ARCH-GARCH
- Modelos ARIMA ARCH GARCH

# Introducción a Colab


```markdown
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



from statsmodels.compat import lzip
from statsmodels.graphics.tsaplots import plot_acf, plot_pacf
from statsmodels.tsa.stattools import adfuller, kpss
from statsmodels.stats.diagnostic import acorr_ljungbox
from statsmodels.tsa.arima.model import ARIMA
```


# Modelo Lineal (Estimador de Minimos Cuadrados Ordinarios)

La siguiente sección muestra los pasos y procesos para crear un Modelo
lineal en Python.

Previamente, se debe precargar la función statsmodels.formula.afi con un nombre
definido, para este caso como `smf`. De aqui en adelante la 
función se conocerá como sfm.

```
import statsmodels.formula.api as smf
```
Para aplicar un modelo lineal, se requiere la función `smf.ols`

```
model = smf.ols(formula = 'y ~ x1 + x2', data = data)
result = model.fit()
result.summary()
```
## Extraer información del modelo

Una vez creado el modelo se puede extraer la información del 
modelo con los siguientes comandos:

### Obtener los parámetros del modelo

```
b = result.params
```

### Obtener los errores estandar del modelo
```
se = result.bse
```
### Obtener t valores del modelo
```
tval = result.tvalues
```
### Obtener P valores del modelo
```
pval = result.pvalues
```
### Obtener la sumatoria al cuadrado de los residuales
```
sse = result.ssr
```
### Obtener el coeficiente de determinación (y el ajustado)
```
r2 = result.rsquared
r2a = result.rsquared_adj
```
## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/DavRodEcon/econometriapythonitm/edit/gh-pages/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [Basic writing and formatting syntax](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/DavRodEcon/econometriapythonitm/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
