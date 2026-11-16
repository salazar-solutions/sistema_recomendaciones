# 🎬 Sistema de Recomendación de Películas

Sistema de recomendación progresivo (tema *6. Sistemas recomendadores*): recomendador simple por popularidad, recomendadores basados en contenido, técnicas de NLP y un recomendador mejorado con actores, director, palabras clave y géneros. Usa ~45,000 películas del dataset *The Movies Dataset*.

## 📋 Contenido

| Archivo | Qué contiene |
|---------|--------------|
| `01_fundamentos.ipynb` | Tipos de recomendadores, análisis exploratorio y **recomendador simple** con la media ponderada de IMDB (top 15). |
| `02_content_based.ipynb` | **Basado en contenido**: TF-IDF sobre sinopsis, similitud coseno y "metadata soup". |
| `03_nlp_tecnicas.ipynb` | NLP: tokenización, stemming, lematización, Bag of Words vs TF-IDF, wordclouds, coseno vs euclidiana. |
| `04_recomendador_mejorado.ipynb` | **Recomendador mejorado** con `credits.csv` (3 actores + director + keywords + géneros), `CountVectorizer`, comparación con el de sinopsis y filtro de popularidad. Usa *The Dark Knight Rises* y *The Godfather*. |
| `utils.py` | Funciones compartidas por los notebooks 01-03. |
| `data/` | `movies_metadata.csv`, `keywords.csv` y `credits.csv`. |
| `output/` | Gráficas generadas por los notebooks. |

Los notebooks se entregan **ya ejecutados**, con sus resultados visibles.

## 🚀 Instalación y ejecución

Probado con **Python 3.12** (Linux/WSL).

```bash
git clone <url-del-repo>
cd sistema_recomendaciones
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt

# Datos de NLTK (solo para 03_nlp_tecnicas.ipynb)
python -c "import nltk; nltk.download('punkt_tab'); nltk.download('stopwords'); nltk.download('wordnet')"

# Abrir los notebooks (VS Code, JupyterLab, etc.) en este orden: 01, 02, 03, 04
```

Para ejecutar un notebook desde la terminal:

```bash
python -m jupyter nbconvert --to notebook --execute --inplace 04_recomendador_mejorado.ipynb
```

### Datos

Los tres CSV deben estar en `data/`. `credits.csv` (~181 MB) **no está en este repositorio** (supera el límite de 100 MB de GitHub, por eso está en `.gitignore`) ni viene en el material del tema; descárgalo del dataset original de Kaggle **"The Movies Dataset"** (Rounak Banik). Sin él no se puede ejecutar el notebook 04.

### ⚠️ Memoria RAM

- `04_recomendador_mejorado.ipynb` calcula la similitud solo de la película consultada, por lo que usa poca memoria.
- `02_content_based.ipynb` calcula las **matrices completas** de similitud (45,000 × 45,000, varios GB cada una) y puede necesitar **más de 25 GB de RAM**. Ejecútalo en un equipo con memoria suficiente.

## 📊 Qué se aprende

- **Recomendador simple:** media ponderada de IMDB, `WR = v/(v+m)·R + m/(v+m)·C`, con `m` = percentil 90 de votos.
- **Basado en contenido:** vectorizar texto (TF-IDF o conteo) y comparar películas con la similitud coseno.
- **Metadata soup:** unir actores, director, keywords y géneros (en minúsculas y sin espacios) para capturar más información que la sinopsis.
- **NLP:** pipeline de preprocesamiento y comparación de representaciones vectoriales.

## 🛠️ Tecnologías

pandas · NumPy · scikit-learn · NLTK · matplotlib · wordcloud · Jupyter

## 📄 Licencia

MIT
