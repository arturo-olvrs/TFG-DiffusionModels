# Dudas tras el verano

### Dudas generales

- ¿Qué es la verosimilitud? ¿Es siempre sinónimo de probabilidad? Se refiere a $p(x)$? ¿A $p(x|z)$? ¿A $p(z|x)$? ¿A otra cosa?
- Qué es la distribución a posteriori? ¿Es la que se deduce de la Regla de Bayes? ¿Es decir, dado $p(x|z)$, deducir $p(z|x)$?

### Ejercicio 1. Notebook de Jupyter y PPCA

#### PCA

De PCA antes, yo tan solo sabía que era un método de reducción de dimensionalidad, pero no entendía cómo se aplicaba a los datos. Tras leer un poco más sobre el tema, he visto que se emplea una matriz $W$ y un sesgo $b$ para proyectar los datos a un espacio de menor dimensión. De forma que los datos proyectados $z$ se obtienen mediante la ecuación:
$$ z = Wx + b $$

Sobre el proceso de obtención de $W$ y $b$ tan sólo sé que es mediante valores propios, pero no he profundizado en ello, puesto que creo que no era el objetivo (si me recomendáis que lo haga, puedo hacerlo).

#### PPCA

Sobre PPCA, he visto que es un paso intermedio entre PCA y un VAE, puesto que el espacio latente tiene estructura probabilística. En el VAE, los parámetros de la distribución latente se obtienen mediante una red neuronal, mientras que en PPCA hay varios métodos para obtenerlos:
1. **Mediante Inferencia Variacional**, que es el método que se emplea en los VAE. Maximizando el ELBO (o, en este caso, minimizando su opuesto), se obtienen los parámetros del PPCA. En este método no hay red neuronal ninguna, sino una simple optimización de los parámetros (que también se podría haber calculado teóricamente sin usar ningún método numérico).

    Este es el método que he empleado en el notebook de Jupyter.

2. **Mediante la ecuación de máxima verosimilitud**, que es un método directo por el que se obtienen los parámetros de la distribución latente que maximizan la probabilidad de los datos observados.

    Este método, aunque explicado ne el PDF que me ha pasado Rafa, he entendido que no era el objetivo del ejercicio, por lo que no he profundizado en por qué se llegan a esos resultados. Tan solo los he empleado para comprobar que los resultados obtenidos mediante el método de Inferencia Variacional eran correctos.