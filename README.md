# Autoencoders nad Generative Deep Learning

<a target="_blank" href="https://cookiecutter-data-science.drivendata.org/">
    <img src="https://img.shields.io/badge/CCDS-Project%20template-328F97?logo=cookiecutter" />
</a>

# Deblur CelebA

Proyecto de autoencoder convolucional para reconstrucción (deblurring) de imágenes faciales usando el dataset **CelebA-faces (Hugging Face)**.

---

## Objetivo

Entrenar un modelo que reciba una imagen borrosa y reconstruya su versión original.

---

## Dataset

- Fuente: CelebA-faces
- 8,000 imágenes descargadas  
- 7,000 utilizadas inicialmente  
- 1,721 usadas para el entrenamiento final (<1% del dataset original)


---

## Preprocesamiento

- Redimensionamiento y normalización
- Generación de versión borrosa (input)
- Split 80/20 (train/test)
- Guardado en `.npy`:
  - `X_train.npy`
  - `X_test.npy`
  - `y_train.npy`
  - `y_test.npy`

Input: imagen borrosa  
Target: imagen original  

---

## Modelo

Framework: TensorFlow

Tipo: Autoencoder convolucional (U-Net simplificado)

### Arquitectura

Encoder:
- Conv2D + ReLU
- MaxPooling
- Filtros: 64 → 128 → 256

Decoder:
- UpSampling
- Skip connections
- Conv2D
- Capa final sigmoid

---

## Entrenamiento

- Optimizador: Adam
- 10 épocas
- Batch size: 32
- 20% validación interna
- Métricas: MSE (principal), MAE

### Resultados en test

- Test MSE: 0.0026  
- Test MAE: 0.0320  

Modelo guardado en `models/`.

---

## Inference

El modelo permite:

- Cargar imágenes nuevas
- Aplicar el mismo preprocesamiento
- Generar versión deblurred
- Visualizar resultados

Carpeta usada con GPU:  
https://drive.google.com/drive/folders/1XfnhNWLeX2JVZ-zOivKGdzQdtZNI1a3L?usp=drive_link

--- 

Estructura siguiendo formato Cookiecutter Data Science:


```
├── LICENSE            <- Open-source license if one is chosen
├── Makefile           <- Makefile with convenience commands like `make data` or `make train`
├── README.md          <- The top-level README for developers using this project.
├── data
│   ├── processed      <- The final, canonical data sets for modeling.
│   └── raw            <- The original, immutable data dump.
│
├── docs               <- A default mkdocs project; see www.mkdocs.org for details
│
├── models             <- Trained and serialized models, model predictions, or model summaries
│
├── notebooks          <- Jupyter notebooks. Naming convention is a number (for ordering),
│                         the creator's initials, and a short `-` delimited description, e.g.
│                         `1.0-jqp-initial-data-exploration`.
│
├── pyproject.toml     <- Project configuration file with package metadata for 
│                         test1 and configuration for tools like black
│
├── references         <- Data dictionaries, manuals, and all other explanatory materials.
│
├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
│   └── figures        <- Generated graphics and figures to be used in reporting
│
├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
│                         generated with `pip freeze > requirements.txt`
│
├── setup.cfg          <- Configuration file for flake8
│
└── test1   <- Source code for use in this project.
    │
    ├── __init__.py             <- Makes test1 a Python module
    │
    ├── config.py               <- Store useful variables and configuration
    │
    ├── dataset.py              <- Scripts to download or generate data
    │
    ├── features.py             <- Code to create features for modeling
    │
    ├── modeling                
    │   ├── __init__.py 
    │   ├── predict.py          <- Code to run model inference with trained models          
    │   └── train.py            <- Code to train models
    │
    └── plots.py                <- Code to create visualizations
```

--------

