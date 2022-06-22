
# Procesos de Bondad de Ajuste de un modelo Lineal

La siguiente sección muestra los pasos y procesos para leer los resultados de un modelo lineal y conocer su eficiencia.

Una vez estimado el modelo lineal si bien el resumen estadistico se muestra en los resultados del objeto que se definio para la función `smf.ols` (recuerde que para la sección anterior se llamo al objeto de modelo lineal como `model`) se pueden extraer:

## Obtención de los valores de $$\hat Y_i$$ y los residuales 

Para obtener los resultados de los valores estimados se puede utilizar: 
```
yest = result.fittedvalues
```

Y para obtener los resultados de los residuales del modelo se requiere: 

```
errorv1 = result.resid
errorv2 = data['gm']-yest
```
Se puede apreciar que existen dos formas de obtener los mismos residuales, en la versión 1 se puede utilizar una función directa `result.resid`, o usar la diferencia entre los datos y los valores estimados $$e_i = y_i- \hat y_i$$, como se muestra en la versión 2.

## Obtención de los valores de las sumatorias al cuadrado.

Para obtener los resultados de la sumatoria al cuadrado de los residuales (SSE), la sumatoria al cuadrado de los explicados (SSR) y la sumatoria al cuadrado de los totales (SST) se pueden utilizar los siguientes: 

```
ssev2 = np.sum((errorv2)**2)
ssrv2 = np.sum((yest-(np.mean(yest)))**2)
sst = ssev2 + ssrv2
sstv2 = np.sum((data.iloc[:,0]-(np.mean(data.iloc[:,0])))**2)
```

## Obtener o extraer los valores de $$R^2$$ y $$R^2_{Adj}$$

Para obtener el valor del coeficiente de determinación y el coeficiente de determi nación ajustado se puede obtener realizando la relación entre la sumatoria al cuadrado de los explicados (SSR) y la sumatoria al cuadrado de los totales (SST), tal que $$R^2 = SSR/SST$$ o por su simil con la sumatoria al cuadrado de los residuales (SSE) $$R^2 = 1-{SSE/SST}$$.
```
r21 = ssrv2/sstv2
r21 = 1-(ssev2/sstv2)
```

Recuerde que el valor ajustado del $$R^2$$, se requiere el uso de grados de libertad $gl = (N-K)$, para ello se requiere usar la función `.shape[0]` para extraer la cantidad de datos de una columna (en este caso la primera de ellas). Como se aprecia, se usa en dos formas, `datos.shape[0]` y `b.shape[0]` que cuenta la cantidad de datos de la primera columna de información de la serie `datos` y la segunda cuenta el vector columna de parámetros calculados de un objeto b (recuerde que este se obtuvo en la sección anterior).
```
gl = datos.shape[0]-b.shape[0]
r2a = 1-((data.shape[0]-1)/gl)*(1-r21)
```

## Hallar los valores de $$t_c$$ y $$t_t$$

Siguiendo el proceso de obtención según la formula $$t_c = \sigma*(X^TX)^{-1}$$ se puede recolver el proceso usando: 

```
varcov = result.cov_params()
ser = np.sqrt(np.diag(varcov)).T
tc = b/ser
```

Aqui se puede apreciar el uso de `np.sqrt` como función para usar la raíz cuadrada de la función `np.diag` (recuerde que `np.` es una función que nace de la función `numpy`, vea la sección introducción al python para verificar).

Por su parte, el valor teórico o critico se puede obtener de: 

```
alpha = 0.05
tt = stats.t.ppf(1-alpha/2,gl)
```

Donde `stats.t.ppf` es la función de distribución t-student (recuerde que `stats.` es una función que nace de la función `scipy.stats`, vea la sección introducción al python para verificar).

Para el caso de evaluar la significancia global se puede utilizar un similar con la siguientes funciones: 

```
fc = (r2/(1-r2)*(gl/b.shape[0]-1))
ft = stats.f.ppf(1-alpha,b.shape[0],datos.shape[0])
```
## Obtener los valores probabilisticos

Para los valores de significancia individual se pueden obtener a traves de la función `stats.t` con la subfunción `.cdf`, para obtener el valor de la distribución acumulada. Respecto a la significancia global puede usarse `stats.f`
```
pv = 2*stats.t.cdf(-abs(tc),gl)
fpv = 1-stats.f.cdf(fc,b.shape[0],datos.shape[0])
```
