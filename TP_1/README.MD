# TP de Regresión — Aprendizaje Automático 1

Trabajo práctico de predicción de precios de viviendas de Boston mediante regresión lineal múltiple.

**Facultad de Ciencias Exactas, Ingeniería y Agrimensura (FCEIA) — Universidad Nacional de Rosario**
**Tecnicatura Universitaria en Inteligencia Artificial — Aprendizaje Automático 1**

**Integrantes:** Gimbatti, Longo, Paredes

## Contenido del repositorio

| Archivo | Descripción |
|---|---|
| `TP-regresion-AA1.ipynb` | Notebook con el desarrollo completo del trabajo |
| `house-prices-tp.csv` | Dataset provisto por la cátedra (556 registros, 14 variables) |
| `requirements.txt` | Dependencias necesarias para ejecutar el notebook |

## Cómo ejecutarlo

```bash
python -m venv venv
venv\Scripts\activate          # en Linux o macOS: source venv/bin/activate
pip install -r requirements.txt
jupyter notebook TP-regresion-AA1.ipynb
```

El notebook se ejecuta de principio a fin sin intervención manual (*Kernel → Restart & Run All*). La semilla está fijada en `RANDOM_STATE = 42`, de modo que todos los resultados son reproducibles.

En Google Colab funciona igual: la primera celda instala CatBoost, que no viene preinstalado.

## Estructura del notebook

| Secciones | Contenido |
|---|---|
| 1 – 2 | Configuración del entorno y carga del dataset |
| 3 | Gestión de datos: nulos, duplicados, consistencia de dominio y criterios de eliminación |
| 4 | División train / test |
| 5 | Imputación: KNN para variables numéricas y CatBoost para las categóricas |
| 6 – 9 | Análisis exploratorio: descriptivo, normalidad, correlaciones y outliers |
| 10 | Control de coherencia lógica del dataset imputado |
| 11 | Efecto de la eliminación sobre el análisis exploratorio |
| 12 – 13 | Transformación logarítmica y escalado robusto |
| 14 – 16 | Regresión lineal, gradiente descendente y regularización |
| 17 – 19 | Comparación de modelos y elección del modelo final |
| 20 | Conclusiones |

## Resumen de resultados

- El dataset original tenía 556 registros. Tras aplicar criterios de calidad, imputar los registros recuperables y validar su coherencia, quedaron **506 registros completos** (407 de entrenamiento y 99 de prueba).
- Las variables más relacionadas con el precio son `LSTAT` (−0,75) y `RM` (+0,71). `RAD` y `TAX` son colineales (*r* = 0,91).
- **Modelo final: Ridge** (α ≈ 0,93), con R² de test 0,64 y RMSE de test 4,74 (miles de dólares).
- Los cinco modelos evaluados dan resultados equivalentes dentro del margen de error de la validación cruzada: el límite no está en el algoritmo sino en la forma funcional lineal y en la censura de la variable objetivo.
