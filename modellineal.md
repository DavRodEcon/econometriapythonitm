
# Modelo Lineal (Estimador de Minimos Cuadrados Ordinarios)

La siguiente sección muestra los pasos y procesos para crear un Modelo
lineal en Python.

Previamente, se debe precargar la función statsmodels.formula.afi con un nombre
definido, para este caso como `smf`. De aqui en adelante la 
función se conocerá como sfm.

```
import statsmodels.formula.api as smf
```
Para aplicar un modelo lineal, se requiere la función smf.ols 

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



## Related

Here are some related projects

[Awesome README](https://github.com/matiassingers/awesome-readme)


## 🔗 Links
[![portfolio](https://img.shields.io/badge/my_portfolio-000?style=for-the-badge&logo=ko-fi&logoColor=white)](https://katherinempeterson.com/)
[![linkedin](https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/)
[![twitter](https://img.shields.io/badge/twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white)](https://twitter.com/)

