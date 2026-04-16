# Trabajo práctico 3 — Notas técnicas y decisiones

**Respuesta de todo el TP:** está en **`tp_umbrales.ipynb`**, el archivo donde se responde y se desarrolla la consigna completa. Este `doc-info.md` solo complementa con notas técnicas (librerías, rutas, segmentación).

## 1. Objetivo del cuaderno

Implementar y visualizar **operadores puntuales basados en umbrales** sobre una imagen fija (`entrada/pelota.jpg`: pelota sobre césped), en **grises** y en **color**, incluyendo binarización (Otsu), umbrales por intervalo, extensiones de rango, reducción de niveles, operaciones aritméticas entre imágenes, planos de bits y **segmentación del fondo verde** para aislar la pelota.

## 2. Estructura del repositorio (alineada al TP2)

| Ruta | Descripción |
|------|-------------|
| `entrada/` | Imagen de trabajo (`pelota.jpg`). |
| `salida/` | Reservada para exportaciones opcionales (capturas, PNG, etc.). |
| `tp_umbrales.ipynb` | Cuaderno principal con teoría, código y gráficos. |
| `requirements.txt` | Dependencias Python. |
| `doc-info.md` | Este archivo: decisiones y uso de librerías. |

## 3. Librerías y rol de cada una

| Herramienta | Por qué está | Uso en este TP |
|-------------|--------------|----------------|
| **NumPy** | Arreglos de imagen y máscaras lógicas vectorizadas. | Indexación, umbrales por comparación, operaciones puntuales, planos de bits. |
| **OpenCV (`cv2`)** | Conversiones de color eficientes, `inRange`, morfología, componentes conexas, Otsu. | `cvtColor`, `threshold` (Otsu), `inRange` en HSV, `morphologyEx`, `connectedComponentsWithStats`, `imread`. |
| **Matplotlib** | Visualización en el cuaderno. | `imshow`, títulos y disposición de figuras (no reemplaza las definiciones teóricas de umbrales). |
| **Jupyter** | Entorno del notebook. | Ejecución interactiva por celdas. |

En el **TP2** el cátedra pedía implementar gran parte del pipeline “a mano” con NumPy y reservar OpenCV casi solo a la lectura. En el **TP3** el enfoque es distinto: se trabaja **explícitamente** con utilidades de OpenCV para umbrales en color (HSV), morfología y etiquetado de regiones, coherente con consignas típicas de umbralización y segmentación en laboratorio.

## 4. Carga de `pelota.jpg`

La función `_ruta_pelota` en el notebook busca, en orden:

1. `entrada/pelota.jpg` relativo a la carpeta del `.ipynb` (VS Code / Cursor).
2. `entrada/pelota.jpg` y luego `pelota.jpg` en el directorio de trabajo y ancestros (útil al abrir el repo desde la raíz o en Colab con rutas alternativas).

Así se mantiene la carpeta **`entrada/`** como convención del proyecto sin romper ejecuciones que dejen el JPEG junto al notebook.

## 5. Segmentación césped / pelota (fondo verde)

La máscara de césped combina:

- **HSV** con matiz verde acotado (escala de matiz de OpenCV 0–179), saturación y valor mínimos.
- **Dominancia del canal verde** en BGR (`G` claramente mayor que `R` y `B`).
- **Exclusiones** para no clasificar como césped blancos/grises claros de la pelota ni el rojo del diseño.

La **morfología** es deliberadamente **suave** (kernels moderados y pocas iteraciones): un cierre muy grande y repetido tiende a **cerrar también el interior de la pelota** y deja la máscara de césped cubriendo casi toda la imagen; entonces el primer plano (`not máscara`) queda vacío y la salida se ve negra.

Tras obtener el primer plano, se conserva la **mayor componente conexa** (la pelota) y se aplica un recorte adicional de píxeles **verdosos** residuales en el blob.

## 6. Ejecución

Desde la raíz del repositorio:

```bash
pip install -r requirements.txt
jupyter notebook tp_umbrales.ipynb
```

(o `jupyter lab`, o abrir el `.ipynb` en VS Code / Cursor con kernel Python).

## 7. Consigna y respuestas

El enunciado, el desarrollo práctico y las respuestas asociadas están integrados en **`tp_umbrales.ipynb`** (celdas de texto y de código). Este archivo (`doc-info.md`) complementa solo con notas técnicas y de librerías.
