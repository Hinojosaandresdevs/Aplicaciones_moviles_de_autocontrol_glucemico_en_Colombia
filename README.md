# Selección de aplicaciones de registro glucémico y legibilidad de sus políticas de datos

Código de apoyo para la monografía de grado de **Andres Hinojosa** — Ingeniería de Sistemas, Corporación Universitaria de Ciencia y Desarrollo (UNICIENCIA), Bucaramanga, Colombia.

El notebook hace dos cosas: selecciona, a partir de un corpus de Google Play Colombia, las aplicaciones de registro glucémico que cumplen los criterios de popularidad y valoración del estudio, y calcula el **índice de legibilidad Flesch-Szigriszt** de sus políticas de privacidad, clasificándolo según la **escala INFLESZ**.

[![Abrir en Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/USUARIO/REPOSITORIO/blob/main/seleccion_y_legibilidad_inflesz.ipynb)

## Metodología

**Corpus.** Búsqueda en Google Play (país `co`, idioma `es`) con los términos *glucosa*, *registro de glucosa*, *diabetes control*, *azúcar en sangre* y *glucemia*, usando `google-play-scraper`. Cuando Colombia no devuelve métricas, se completan con México y Estados Unidos. Por defecto el notebook trabaja sobre el Excel ya generado, que es la foto del corpus documentada en la monografía; con `EJECUTAR_SCRAPING = True` se descarga de nuevo y las cifras cambiarán.

**Selección.** Se conserva una aplicación si su puntuación es mayor que 4,0 y tiene más de 1.000 calificaciones. Las que no tienen métricas en ningún país se descartan, y las exclusiones manuales (apps que pasan el filtro pero no son de registro glucémico) quedan documentadas en el diccionario `EXCLUSIONES` con su motivo. El resultado se verifica contra las filas resaltadas en amarillo del Excel de trabajo.

**Legibilidad.** IFSZ = 206,835 − 62,3 × (sílabas / palabras) − (palabras / frases), según Szigriszt-Pazos (1993). El conteo de sílabas distingue diptongos e hiatos del español, y el de frases ignora abreviaturas frecuentes en textos legales. Los tramos siguen a Barrio-Cantalejo et al. (2008): menos de 40 muy difícil, 40–55 algo difícil, 55–65 normal, 65–80 bastante fácil y más de 80 muy fácil. Un texto que no parece estar en español se marca como no válido.

## Resultados

De 56 aplicaciones en el corpus, 17 cumplen el filtro numérico y 15 forman la selección final tras las exclusiones manuales. Doce de las quince políticas quedan por debajo de 55 (una *muy difícil* y once *algo difícil*), dos quedan en *normal* y la única que puntúa como *bastante fácil* no está en español, por lo que su índice no es válido. El detalle por aplicación está en las salidas guardadas del notebook.

## Cómo ejecutarlo

En **Google Colab**, abre el notebook con el botón de arriba y ejecuta las celdas en orden; cada paso que necesita archivos muestra un botón de subida.

En **local**:

```bash
git clone https://github.com/USUARIO/REPOSITORIO.git
cd REPOSITORIO
pip install -r requirements.txt
jupyter notebook seleccion_y_legibilidad_inflesz.ipynb
```

Fuera de Colab, el notebook lee los archivos desde la carpeta `datos/` (ver `datos/README.md`).

## Estructura

```
├── seleccion_y_legibilidad_inflesz.ipynb   Notebook principal
├── requirements.txt
├── datos/
│   ├── README.md                           Qué archivos poner aquí
│   └── politicas/                          Textos de las políticas (no se versionan)
└── LICENSE
```

## Recursos

- Video con la explicación del código: https://www.youtube.com/watch?v=go1DBq3NmMQ
- Matriz de criterios: https://docs.google.com/spreadsheets/d/13hBCNM9ypLzG1FgXfya7Nqy5dfeFlcZSXm6TGItAJMA/edit?usp=sharing

## Referencias

- Barrio-Cantalejo, I. M., Simón-Lorda, P., Melguizo, M., Escalona, I., Marijuán, M. I., & Hernando, P. (2008). Validación de la Escala INFLESZ para evaluar la legibilidad de los textos dirigidos a pacientes. *Anales del Sistema Sanitario de Navarra, 31*(2), 135–152.
- Szigriszt-Pazos, F. (1993). *Sistemas predictivos de legibilidad del mensaje escrito: fórmula de perspicuidad* [Tesis doctoral]. Universidad Complutense de Madrid.

## Licencia

El código se publica bajo licencia MIT. Las políticas de privacidad pertenecen a sus respectivos desarrolladores y no se incluyen en el repositorio.
