

# Modelo Lineal (Estimador de Minimos Cuadrados Ordinarios)

La siguiente sección muestra los pasos y procesos para crear un Modelo
lineal en Python.

Previamente, se debe precargar la función `statsmodels.formula.afi` con un nombre
definido, para este caso como `smf`. De aqui en adelante la función se conocerá como `sfm.función`. A continuación se muestra como opera la función:

```
import statsmodels.formula.api as smf
```
Se puede apreciar que se llama la función `statsmodels.formula.api` fue renombrada, y para usar un modelo lineal se requiere la función `smf.ols`, como se muestra a continuación: 

```
model = smf.ols(formula = 'y ~ x1 + x2', data = datos)
result = model.fit()
result.summary()
```

Donde `model` es un objeto que identifica el resultado de la función, `smf.ols` es la función que crea un modelo linal, `formula =` es la función interna que solicita una función lineal en el orden de la variable endogena "Y" y despues involucrar las variables exogenas "X", `data` es la función interna que solicita el nombre del objeto de los datos previamente cargados y que el modelo pueda operar.

## Extraer información del modelo

Una vez creado el modelo se puede extraer la información del modelo con los siguientes comandos:

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
