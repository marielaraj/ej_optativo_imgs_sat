# Ejercicio optativo

En este ejercicio vamos a estar trabajando con una imagen satelital obtenida por sensores a bordo del satélite Landsat8. La imagen original fue bajada de la página https://earthexplorer.gov. En esa página se pueden bajar imágenes con distinto nivel de pre-procesamiento. Para este ejercicio bajamos una imagen de nivel de procesamiento 2, esto quiere decir que los valores de los pixeles representan la reflectancia en superficie en distintas longitudes de onda. En https://www.usgs.gov/media/files/landsat-8-collection-1-land-surface-reflectance-code-product-guide pueden encontrar el manual de estas imagenes donde les detallan la descripcion tanto de los nombres de lor archivos como de los preprocesamiento que tienen realizados. Para este ejercicio hemos realizado un clip de cada una de las bandas originales de la imagen y, además, multiplicamos a cada una de las bandas por el factor de escala indicado en el manual (0,0001).

Las longitudes de onda y la resolución espacial asociada a las bandas que utilizaremos en este ejercicio se describen a continuación:

$`\sqrt{2}`$

| Banda                        | Longitud de onda (nanómetros) | Resolución espacial (metros) |
| ---------------------------- | ----------------------------- | ---------------------------- |
| Banda 1 - Aerosoles          | 430 - 450                       | 30                           |
| Banda 2 - Azul               | 450 - 510                       | 30                           |
| Banda 3 - Verde              | 530 - 590                       | 30                           |
| Banda 4 - Rojo               | 640 - 670                       | 30                           |
| Banda 5 - Infrarrojo cercano | 850 - 880                       | 30                           |
| Banda 5 - Infrarrojo medio 1 | 1570 - 1650                   | 30                           |
| Banda 7 - Infrarrojo medio 2 | 2110 - 2290                   | 30                           |

Si desean abrir los datos de la imagen original en Python deberán bajar algunas librerías específicas para la manipulación de datos satelitales, por ejemplo: **gdal**. Pueden encontrar un tutorial de los primeros pasos  en https://www.github.com/marielaraj/pycon_tallerimgssat.

En la carpeta *clip* encontrarán los datos que necesitará para realizar los ejercicios, cada clip se encuentra en formato .npy


## Ejercicio 1

a) Utilizando **numpy**, levantar cada una de las bandas y utilizando **matplotlib** visualizarlas.
¿Se ven correctamente? ¿Cómo podría solucionarlo?
Sugerencia: leer la documentación de la función **imshow** ¿Hay algún parámetro que le sirva?


b) Utilizando la librerías **glob**, **numpy** y **matplotlib** crear una función que, dada una carpeta y un número de banda, muestre la imagen de dicha banda y la guarde en formato .png. Asegúrese de incorporar el "colobar" al lado de cada imagen. Llame a la función *crear_img_png*.
Tenga en cuenta el punto a) al realizar esta función. Es decir, asegúrese que la función genere la correcta visualización de la imagen.



## Ejercicio 2

a) Utilizando la librerías **glob**, **numpy** y **matplotlib** crear una función que dada una carpeta, un número de banda y una cantidad de bins, muestre el histograma (con la cantidad de bins seleccionados) de los valores de dicha banda y la guarde en formato .png. Llame a la función *crear_hist_png*.


## Ejercicio 3

a) Utilice las funciones *crear_img_png* y *crear_hist_png* obtenidas en los puntos anteriores para generar las imágenes e histogramas de cada banda.

b) ¿Qué banda o bandas parecieran distinguir mejor aquellos pixeles que representan el agua del resto de los pixeles? Elija una banda y observando el histograma y la imagen de dicha banda, seleccione un umbral que le permita distinguir el agua. Luego cree una máscara de agua / no agua. Es decir, un array del mismo tamaño de la banda donde a cada píxel le corresponda un 1 o un 0, 1 si es agua y 0 si no.

## Ejercicio 4

Para este ejercicio trabajaremos con un índice: el Índice de Vegetación de Diferencia Normalizada, también conocido como NDVI por sus siglas en inglés. Este índice se utiliza para estimar la cantidad, calidad y desarrollo de la vegetación con base a la medición de la intensidad de la radiación de ciertas bandas del espectro electromagnético que la vegetación emite o refleja.

Para calcular el NDVI se utilizan las bandas espectrales Roja e Infrarroja, el cálculo se hace mediante la siguiente fórmula:

$$ \frac{INFRARROJO CERCANO-ROJO}{INFRARROJO CERCANO+ROJO} $$


a) Calcular el NDVI.
b) Categorizar los valores obtenidos en cada pixel de acuerdo a clases que no sean más útiles y fáciles de interpretar. La tabla a continuación muestra las categorías que consideraremos en este estudio:



| Valor de NDVI    | Nombre de la clase  | Identificador de Clase | color       |
| ---------------- | ------------------- | ---------------------- | ----------- |
| < 0              | No vegetada         | 0                      | black       |
| entre 0 y 0.1    | Área desnuda        | 1                      | y           |
| entre 0.1 y 0.25 | Vegetación baja     | 2                      | yellowgreen |
| entre 0.25 y 0.4 | Vegetación moderada | 3                      | g           |
| >0.4             | Vegetación densa    | 4                      | darkgreen   |


Crear un np.array que le asigne a cada píxel el número dado por el "identificador de categoría" correspondiente según la tabla. Llame *ndvi_clases* al np.array obtenido.

c) Utilizando *matplotlib* realizar una visualización del ndvi_clases.

d) Crear un colorMap para lograr asignarle a cada clase el color sugerido en la tabla. Para esto debemos utilizar la función ListedColormap  incluida en **matplotlib.colors**  cree un  colorMap (cmap).

e) Crear una leyenda que indique el nombre de cada clase con el color asignado, para eso sugerimos utilizar la función **mpatches** que se encuentra en **matplotlib.patches**. Para que puedan orientarse, mostramos a continuación un ejemplo de resultado esperado:


![](https://i.imgur.com/TybP2a9.png)

