# ConnectaTel-analysis

# Análisis Exploratorio y Segmentación de Clientes — ConnectaTel

## 🎯 Objetivo del Proyecto
Realizar un análisis exploratorio de datos (EDA) y una segmentación de clientes para **ConnectaTel**, evaluando la distribución de la edad (`age`), el tipo de plan (*Basico* / *Premium*) y el comportamiento de uso (`cant_mensajes`, `cant_llamadas`, `cant_minutos_llamada`). El propósito es detectar problemas de calidad de datos, analizar valores atípicos (*outliers*) mediante el método IQR, construir segmentos accionables y entregar conclusiones ejecutivas para *stakeholders*.

---

## 📂 Datasets Utilizados
Los datos de entrada se cargan desde `/datasets/` mediante tres archivos CSV:

1. **`plans` (`/datasets/plans.csv`)**: Catálogo o información de planes disponibles.
2. **`users` (`/datasets/users_latam.csv`)**: Información demográfica y de suscripción de usuarios en Latinoamérica (incluyendo `age` y `plan`: *Basico* / *Premium*).
3. **`usage` (`/datasets/usage.csv`)**: Métricas de actividad de los usuarios (`cant_mensajes`, `cant_llamadas`, `cant_minutos_llamada`).

En el flujo de integración, los datos se consolidan en el dataframe `user_profile` (con `3,999` registros válidos en las métricas de uso).

---

## 🔄 Etapas del Análisis Realizadas
1. **Carga y Preparación de Datos**: Importación de librerías y carga de `plans.csv`, `users_latam.csv` y `usage.csv` para construir la base consolidada `user_profile`.
2. **Análisis Exploratorio de Distribuciones (Histogramas y KDE)**: Comparación de la distribución de mensajes, llamadas y minutos de llamada entre los planes *Basico* y *Premium*, observando asimetría positiva (sesgo a la derecha) en las métricas de uso y mayor volumen de usuarios en el plan *Basico*.
3. **Identificación y Evaluación de Outliers (Boxplots e IQR)**:
   - Generación automática de *boxplots* para `age`, `cant_mensajes`, `cant_llamadas` y `cant_minutos_llamada`.
   - `age` no presenta *outliers* visuales.
   - `cant_mensajes` (hasta `17`), `cant_llamadas` (hasta `15`) y `cant_minutos_llamada` (hasta `155.69`) presentan *outliers* superiores.
   - Cálculo de límites mediante IQR y decisión de **mantener** los *outliers* superiores por corresponder a comportamiento legítimo de usuarios con mayor consumo (*heavy users*).
4. **Segmentación de Clientes**:
   - **`grupo_uso`**: Clasificación en `'Bajo uso'` (`llamadas < 5` y `mensajes < 5`), `'Uso medio'` (`llamadas < 10` y `mensajes < 10`) y `'Alto uso'` para el resto de casos.
   - **`grupo_edad`**: Clasificación en `'Joven'` (`age < 30`), `'Adulto'` (`age < 60`) y `'Adulto Mayor'` para el resto de casos.
   - Visualización de ambos segmentos mediante gráficos de conteo (`countplot`).
5. **Insight Ejecutivo para Stakeholders**: Síntesis de problemas detectados en los datos, comportamiento por edad y nivel de uso, y recomendaciones comerciales para planes, *upselling* y retención.

---

## 🛠️ Tecnologías y Librerías
- **Python 3**
- **`pandas` (`pd`)**: Lectura de CSV y manipulación de datos tabulares.
- **`numpy` (`np`)**: Operaciones numéricas y evaluación condicional de segmentos.
- **`seaborn` (`sns`) y `matplotlib.pyplot` (`plt`)**: Histogramas, *boxplots* y gráficos de conteo.
- **Jupyter Notebook / Google Colab**

---

## 🚀 Cómo Ejecutar el Notebook y Guía de Reproducción

### Opción 1: Google Colab
1. Abre el notebook (`.ipynb`) en **Google Colab**.
2. Coloca `plans.csv`, `users_latam.csv` y `usage.csv` en la ruta `/datasets/` del entorno (o actualiza las rutas en `pd.read_csv(...)` según dónde los cargues).
3. Ejecuta las celdas en orden secuencial o selecciona **Entorno de ejecución > Ejecutar todas**.

### Opción 2: Entorno Local (Jupyter Notebook / VS Code)
1. Descarga o clona el proyecto en tu equipo y ubica los archivos CSV en `/datasets/` (o ajusta la ruta en el código).
2. Instala las librerías necesarias:
   ```bash
   pip install pandas numpy seaborn matplotlib jupyter
