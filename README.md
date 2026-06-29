# cil-dataset-equipo24

Dataset y notebook de entrenamiento del **Proyecto Final — Conditional Imitation Learning (CIL)**
(Navegación Autónoma · Maestría en IA Aplicada · Tec de Monterrey · **Equipo 24**).

## Contenido

```
cil-dataset-equipo24/
├── CIL_Entrenamiento_Equipo24.ipynb   # notebook de Colab (PilotNet + ramas Codevilla)
├── IMG/                                # imágenes de la cámara (se suben tras la recolección)
└── driving_log.csv                     # una fila por imagen: nombre_imagen, steering, comando
```

> El **dataset** (`IMG/` + `driving_log.csv`) se genera conduciendo manualmente en el Mundo #1 de
> Webots con el controlador `data_collector` y se sube aquí. La velocidad **no** se registra.

## Formato de `driving_log.csv`

| Columna | Tipo | Descripción |
|:--|:--|:--|
| `nombre_imagen` | str | ruta relativa, p. ej. `IMG/20260629_181530_000123.png` |
| `steering` | float | ángulo de dirección en **radianes, crudo** (se normaliza a `[-1,1]` en el notebook) |
| `comando` | int | comando CIL: `0`=FOLLOW_LANE, `1`=LEFT, `2`=STRAIGHT, `3`=RIGHT |

## Abrir el notebook en Google Colab

Directo desde GitHub (sin descargar):

<https://colab.research.google.com/github/A00820345/cil-dataset-equipo24/blob/main/CIL_Entrenamiento_Equipo24.ipynb>

La **primera celda** hace `!git clone` de este mismo repo y verifica la integridad del dataset
(conteo por comando, histograma de steering, imágenes faltantes) antes de entrenar.

## Reproducción

1. Sube el dataset recolectado (`IMG/` + `driving_log.csv`) a la raíz de este repo.
2. Abre el notebook en Colab (enlace de arriba), `Runtime → GPU` (o ejecútalo local con TF 2.16).
3. Entrena y exporta `model.h5` para el controlador del Mundo #2 (`cil_evaluator`).

> Meta: **> 10 000 imágenes** tras *data augmentation*. Recorridos en ambos sentidos, todas las
> rutas y maniobras de recuperación de deriva; balance por comando.
