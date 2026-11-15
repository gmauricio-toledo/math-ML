# Proyecto: Predicción de permanencia en tendencias de YouTube

El objetivo de este proyecto es modelar un problema de aprendizaje supervisado (regresión) para predecir cuántos días permanecerá un video en la lista de tendencias de YouTube, utilizando datos tabulares y de texto del dataset Trending YouTube Video Statistics.

## 1. Preparación de datos y prevención de fuga de información

1. Selección de países: Elige un país principal para entrenar, validar y probar tus modelos (por ejemplo, `USvideos.csv` o `MXvideos.csv`). Selecciona un segundo país que utilizarás en la etapa final de evaluación.
2. Definición de entidad única: En los archivos CSV, un mismo video aparece en múltiples filas (una por cada día que estuvo en tendencias). Cada video único (`video_id`) debe constituir una sola observación en tu dataset final:
   - Variable objetivo (y): El número total de días que el video apareció en la lista de tendencias.
   - Variables predictoras (X): Deben construirse con la información disponible en su primera aparición (la `trending_date` más antigua de ese video). Utilizar métricas de días posteriores introduce fuga de información del futuro (data leakage).

3. Ingeniería de características: Extrae variables relevantes de la primera aparición: estadísticas de interacción (vistas, likes, dislikes, comentarios), tasas relativas (por ejemplo, `likes / views`), categoría del video (`category_id` cruzado con el archivo JSON correspondiente) y variables temporales (hora de publicación, día de la semana, tiempo transcurrido entre `publish_time` y `trending_date`).
4. Partición de datos: Divide el conjunto de videos únicos en entrenamiento, validación y prueba. Justifica si la partición debe ser aleatoria o respetar el orden cronológico.

## 2. Representación de texto y preprocesamiento

1. Incorporación de texto: Integra el título (`title`) y las etiquetas (`tags`) como variables predictoras.
2. Comparación de representaciones: Evalúa al menos dos enfoques para convertir el texto en vectores numéricos:
   - Un método basado en frecuencias de palabras (Bag-of-Words o TF-IDF, acompañado de reducción de dimensionalidad como TruncatedSVD).
   - Un método basado en representaciones densas preentrenadas (por ejemplo, modelos de Sentence-Transformers).
3. Transformación de variables.

## 3. Métrica de evaluación y línea base

1. Selecciona una única métrica de evaluación para comparar todos tus modelos en el conjunto de prueba.
2. Selecciona la función de pérdida utilizada durante el entrenamiento en los casos que corresponda.
3. Modelo base (baseline): Implementa un predictor sencillo (por ejemplo, DummyRegressor o regresión lineal sobre las variables numéricas solamente) para establecer un punto de referencia.

## 4. Modelado: ML clásico y Deep Learning

1. Modelos clásicos: Entrena y ajusta hiperparámetros de al menos dos familias distintas de aprendizaje automático clásico.
2. Red neuronal (MLP): Diseña, entrena y regulariza un perceptrón multicapa (MLP) utilizando PyTorch o TensorFlow. Experimenta con la arquitectura, funciones de activación, tasa de aprendizaje y técnicas de regularización (Dropout, decaimiento de pesos o Early Stopping).
3. Reporta el mejor modelo de ML clásico y el mejor modelo de DL, evalúa ambos sobre el conjunto de prueba.

## 5. Evaluación en otro país

1. Toma el mejor modelo clásico y el mejor modelo de DL entrenados en el país original y evalúalos sobre los datos del segundo país que elegiste al inicio (aplicando las mismas transformaciones ajustadas con los datos de entrenamiento del primer país). **No entrenes nuevamente**
2. Compara el error obtenido frente al del país original y explica los motivos de la diferencia de rendimiento.