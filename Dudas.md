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


### Ejercicio 2. Demostrar que la divergencia KL es no negativa

Sin problema, lo he podido demostrar bien.

### Ejercicio 3. Probar con distintos estimadores de la log-likelihood

En el repositorio del MNIST (disponible [aquí](https://github.com/arturo-olvrs/VAE-MNIST)), he añadido la última gráfica que se puede ver abajo. En el notebook en sí, abajo del todo, se explican en detalle los 4 métodos que he empleado para estimar la log-likelihood.

Una pregunta que me surge es:
- Si decidimos aproximar la log-likelihood mediante Importance Sampling, podemos olvidarnos de $q(z|x)$ y emplear directamente $p(z|x)$, no? Aunque sea más lento, ¿no generaría mejores resultados? 
    - Sin programarlo, pienso que no. Para poder obtener $p(x)$ mediante Importance Sampling, necesitamos muestrear de $q(z|x)$ (que en nuestro caso reemplazaríamos por $p(z|x)$). Pero para obtener $p(z|x)$ necesitamos obtener $p(x)$. Por tanto, se requieren mutuamente. No podemos prescindir de $q(z|x)$.
    - Se me ocurre que podríamos emplear mi segundo método ($z\sim p_{prior}(z)$) para obtener $p(x)$. No obstante, tardaría mucho mucho más, puesto que requiere una gran cantidad de muestras para que la estimación sea buena.