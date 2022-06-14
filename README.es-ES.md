# UNet para la segmentación de venas

<p align="center">
  <a href="README.md">English</a> |
  <span>Español</span>
</p>

Implementación de una red UNet en Keras para la segmentación de venas en imágenes de retina.

Proyecto desarrollado para la asignatura Visión por Computador del máster MUIARFID (UPV).

Se ha utilizado como base el código proporcionado por [RParedesPalacios](https://github.com/RParedesPalacios/ComputerVisionLab/blob/master/src/segmen.py) para este propósito.

El dataset se compone de únicamente 20 imágenes por lo que usaremos 19 imágenes para training y 1 imagen para test.

A continuación se muestra una segmentación inferida por el modelo al final del entrenamiento sobre la única imagen de test.

![Máscara inferida a partir de una imagen de test.[\[long\]]{#long
label="long"}](imgs/predicted.png)

# Preprocesamiento

Hemos implementado un generador que combinamos con la librería
[Albumentations](https://github.com/albumentations-team/albumentations) para implementar aumentado de datos para imágenes y máscaras.

Dado que todas las imágenes del dataset están posicionadas de la misma manera, con la misma escala y la misma rotación, hemos evitado usar este tipo de transformaciones. En su lugar, hemos utilizado un cambio de contraste aleatorio dado que en las imágenes del dataset sí que cambia el contraste entre ellas. Esta transformación afecta al color pero no a la máscara, por lo que esta se aplica sólo sobre la imagen.

La siguiente imagen ejemplifica las transformaciones elegidas.

![Data augmentation.[\[long\]]{#long
label="long"}](imgs/augmentation.png)

# Modelo

La UNet implementada está constituida por 5 bloques encoder con 2 capas convolucionales cada uno y 4 bloques decoder, 3 de ellos con 2 capas convolucionales cada uno.

La última capa convolucional convierte la salida a una imagen de 1 filtro con función de activación sigmoide donde cada pixel nos indicará si ese píxel es vena o no.

La función de pérdida utilizada es el error cuadrático medio entre el mapa de segmentación obtenido y el esperado (MSE).

A continuación se muestra el modelo utilizado (simplificado para mayor claridad).

![UNet empleada para segmentación.[\[long\]]{#long
label="long"}](imgs/model_simple.png)

# Entrenamiento

El modelo converge lentamente y después de 200 epochs logra
segmentar correctamente la imagen de test. El error desciende de forma consistente durante la mayor parte del entrenamiento, como se aprecia en la imagen.

![Evolución del error (MSE).[\[long\]]{#long
label="long"}](imgs/loss.png)

# Licencia

[MIT](LICENSE)