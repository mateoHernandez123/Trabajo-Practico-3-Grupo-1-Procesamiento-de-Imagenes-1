# Trabajo práctico — Procesamiento por umbrales y segmentación (Grupo 1)

Repositorio público: [github.com/mateoHernandez123/Trabajo-Practico-3-Grupo-1-Procesamiento-de-Imagenes-1](https://github.com/mateoHernandez123/Trabajo-Practico-3-Grupo-1-Procesamiento-de-Imagenes-1)

**Materia:** Procesamiento de imágenes I  
**Participantes (alumnos):** Mateo Hernandez, Felipe Lucero

**Respuesta del TP:** todo el trabajo (enunciado, desarrollo, resultados y respuestas) está en **`tp_umbrales.ipynb`**; es el único archivo donde se responde y se resuelve el TP completo.

Este repositorio contiene el **cuaderno Jupyter** del trabajo sobre **operadores puntuales y umbrales**: imagen binaria, Otsu, procesamiento en escala de grises y en color (HSV/BGR), umbral global y por intervalo, extensión de rango, reducción de niveles de gris, adición y sustracción entre imágenes, planos de bits (“rodaja”) y **eliminación del fondo verde** para aislar la pelota.

## Estructura del proyecto

| Ruta                | Descripción                                                                    |
| ------------------- | ------------------------------------------------------------------------------ |
| `entrada/`          | Imagen de trabajo (`pelota.jpg`).                                              |
| `salida/`           | Carpeta para salidas opcionales (exportaciones, capturas).                    |
| `tp_umbrales.ipynb` | Cuaderno principal: consigna, implementación, figuras y respuestas integradas. |
| `doc-info.md`       | Notas técnicas, uso de librerías y decisiones de implementación.               |
| `requirements.txt`  | NumPy, OpenCV, Matplotlib, Jupyter.                                            |
| `.gitignore`        | Entornos virtuales, checkpoints de Jupyter, caché de Python.                   |

## Requisitos

- **Python 3.10** o superior recomendado.
- Dependencias: ver `requirements.txt` (`numpy`, `opencv-python`, `matplotlib`, `jupyter`).

## Qué librería usamos y para qué

| Herramienta    | Uso que le damos en este TP                                                                                                            |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| **NumPy**      | Arreglos de imagen, máscaras booleanas y operaciones puntuales vectorizadas.                                                           |
| **OpenCV**     | Lectura BGR, conversiones de color, Otsu, `inRange` en HSV, morfología, componentes conexas en la parte de segmentación césped/pelota. |
| **Matplotlib** | Gráficos e `imshow` en el notebook a partir de arreglos ya calculados.                                                                 |
| **Jupyter**    | Ejecución del cuaderno por celdas.                                                                                                     |

El detalle y la comparación con el enfoque del TP2 están en **`doc-info.md`**, sección 3.

## Instalación y ejecución (otra máquina)

Desde la carpeta raíz del proyecto:

```bash
python -m venv .venv
```

Activá el entorno (en Windows PowerShell: `.\.venv\Scripts\Activate.ps1`; en bash: `source .venv/bin/activate`), luego:

```bash
pip install -r requirements.txt
jupyter notebook tp_umbrales.ipynb
```

Abrí el archivo `tp_umbrales.ipynb` y ejecutá las celdas en orden (la primera parte carga `entrada/pelota.jpg` y define `grayscale_image` y variables en color).

Para más detalle teórico y de implementación, ver **`doc-info.md`**. Recordá que **la respuesta de todo el TP** está en **`tp_umbrales.ipynb`**.
