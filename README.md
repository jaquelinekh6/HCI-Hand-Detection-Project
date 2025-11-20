# Sistema de Reconocimiento de Gestos Manuales (HCI)

## Descripción del Proyecto
Este proyecto implementa un sistema de visión artificial en MATLAB para el reconocimiento de gestos numéricos (del 0 al 5) realizados con la mano. El objetivo es desarrollar técnicas de Interacción Humano-Ordenador (HCI) robustas mediante el procesamiento de imágenes.

El desarrollo se divide en dos fases principales: detección de piel y conteo de dedos, utilizando dos bases de datos con distintos niveles de complejidad (fondos uniformes y complejos).

---

## Fase 1: Detección de Piel
El objetivo de esta fase es segmentar la mano del fondo utilizando el color de la piel. Se modela la crominancia de la piel mediante histogramas en un espacio de color específico (ej. YCrCv, HSV).

### Scripts Principales
* **`algo1.m` (Entrenamiento):** Analiza las imágenes de entrenamiento para generar un histograma modelo de los píxeles de piel.
* **`algo2.m` (Segmentación):** Función que toma una imagen arbitraria y genera una máscara binaria (blanco/negro) indicando qué píxeles corresponden a piel basándose en el modelo generado.
* **`algo3.m` (Procesamiento por lotes):** Script que aplica `algo2` a un conjunto completo de imágenes ubicadas en el directorio `Images` y guarda los resultados en el directorio `Masks`.
* **`algo4.m` (Evaluación):** Compara las máscaras generadas con las máscaras ideales (Ground Truth) ubicadas en `Masks-Ideal`. Calcula la métrica **F-Score** (media armónica de Precision y Recall) para cuantificar la calidad de la segmentación.

---

## Fase 2: Detección y Conteo de Dedos
En esta fase se procesan las máscaras binarias obtenidas para identificar cuántos dedos está mostrando el usuario (0-5).

### Scripts Principales
* **`algo2bis.m` (Opcional):** Versión mejorada de `algo2` para perfeccionar la detección de piel y reducir ruido antes del conteo.
* **`algo5.m` (Conteo):** Función que implementa el algoritmo de visión para contar los dedos en la máscara de la mano. Se basa en análisis de contornos, convexidad o transformación de distancia.
* **`algo6.m` (Ejecución completa):** Script que combina la detección de piel (`algo2`/`algo2bis`) y el conteo (`algo5`) para procesar todas las imágenes. Genera:
    * Máscaras en la carpeta `Masks`.
    * Archivos de texto con el número detectado en la carpeta `Finger`.
* **`algo7.m` (Evaluación Final):** Compara el número de dedos estimado con el real (indicado en el nombre del archivo). Calcula el **F-Score** promedio y la **Exactitud (Accuracy)** del sistema.

---

## Estructura de Carpetas
El proyecto espera la siguiente organización de archivos para funcionar correctamente:

* `/src`: Scripts de MATLAB (`algo1.m` - `algo7.m`).
* `/Images`: Imágenes de entrada (Dataset I y II).
* `/Masks`: Resultados de la segmentación (generado automáticamente).
* `/Masks-Ideal`: Máscaras correctas para validación.
* `/Finger`: Resultados del conteo de dedos (generado automáticamente).

## Requisitos
* MATLAB (R202X).
* Image Processing Toolbox.

## Licencia
Este proyecto es de uso académico para la asignatura de Procesado de Imagen y Video.
