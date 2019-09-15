# Mapa-de-profundidad-con-ML
Resumen: Repositorio creado para participar en el reto DotCSV. La idea fue crear un modelo de aprendizaje para obtener el mapa de profundidad de un rostro a partir de una única fotografía. Los resultados no fueron lo suficientemente buenos, pero de todas maneras decidí compartir mi iniciativa.

Motivación: La idea principal fue que apartir de una fotografia real reconstruir la imagen simulando un ambiente de luz distinto. El modelo debía aprender los patrones necesarios para saber como reconstruir la imagen simulando el comportamiento de la luz. Por ejemplo

Imagen de entrada:
![Rotro 1](https://raw.githubusercontent.com/Metecko/Mapa-de-profundidad-con-ML/master/imgreadme/rostro1.png)

Imagen de salidad:
![Rotro 2](https://raw.githubusercontent.com/Metecko/Mapa-de-profundidad-con-ML/master/imgreadme/rostro2.png)

Para lo anterior supuse que lo mejor era realizar lo siguiente:

![Proceso](https://raw.githubusercontent.com/Metecko/Mapa-de-profundidad-con-ML/master/imgreadme/proceso.png)

Pero por poca experiencia y tiempo solo pude realizar el mapa de profundidad, que ademas no funciona correctamente con rostros reales.

# Datos utilizados

Se crearon decenas de rotros a partir de un software de generación de rostros automaticos (https://facegen.com/). Cada rotro tiene 18 direcciones y 8 angulos distintos de luz. Con solo 15 rostros se renderizaron más de 2000 fotogramas en Blender.

![Rostros](https://raw.githubusercontent.com/Metecko/Mapa-de-profundidad-con-ML/master/imgreadme/rostros.png)

Los rostros target para el modelo:

![RostrosTar](https://raw.githubusercontent.com/Metecko/Mapa-de-profundidad-con-ML/master/imgreadme/rostrostar.png)

# Método utilizado
Como existen muchas imagenes que deben tener el mismo target (ya que el angulo de la luz no influye en el mapa de profundidad), decidi modificar ligeramente la red. Para el Generator incluí un total de 8 inputs, uno para cada angulo de la luz. Por ejemplo, estas 3 imagenes deben tener el mismo target:

![Angulos](https://raw.githubusercontent.com/Metecko/Mapa-de-profundidad-con-ML/master/imgreadme/distintosangulos.png)

Para no darle siempre mucha informacion a la red, decidi setear las entradas de manera aleatoria. Es decir, de vez en cuando darle una pura imagen, o hasta a veces los 8 angulos. Significa que la entrada a la red es una lista de 8 elementos, con al menos uno de ellos la imagen de entrada, los demás se rellenan con tensores nulos (tf.zeros([1, 256, 256, 3], tf.float32))

Los resultados para una cara real es el siguiente (para 20 epocas):

![MImetodo](https://raw.githubusercontent.com/Metecko/Mapa-de-profundidad-con-ML/master/imgreadme/mimetodo.png)

A medida que aumentan las epocas empeoran los resultados.
