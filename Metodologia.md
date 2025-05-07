# Metodología del Proyecto

Este documento explica el enfoque y los métodos utilizados en el proyecto de Clasificación de Riesgo Financiero de manera accesible y transparente.

## ¿Qué queríamos resolver?

El desafío principal era desarrollar un sistema que pudiera clasificar a los solicitantes de préstamos en tres categorías de riesgo (Bajo, Medio, Alto) con especial énfasis en identificar correctamente a los clientes de alto riesgo. Este problema tiene relevancia directa en el mundo financiero, donde predecir el riesgo crediticio es fundamental para:

- Minimizar pérdidas por incumplimiento de pago
- Ofrecer tasas justas basadas en el riesgo real
- Tomar decisiones de préstamo consistentes y objetivas
- Cumplir con requisitos regulatorios

## Nuestro enfoque paso a paso

### 1. Entendiendo y limpiando los datos

**¿Qué teníamos?** Un conjunto de datos con información de 15,000 solicitantes de préstamos, incluyendo datos demográficos y financieros.

**¿Qué problemas encontramos?**
- Aproximadamente 15% de valores faltantes en 6 variables numéricas
- Presencia de outliers en variables como Edad, Puntaje Crediticio y Montos de Préstamo
- Desbalance significativo en la variable objetivo, con predominio de la categoría "Bajo Riesgo"

**¿Cómo los resolvimos?**
- Utilizamos la mediana para imputar valores faltantes (más robusta que la media ante outliers)
- Decidimos conservar los outliers ya que representaban escenarios financieros válidos
- Implementamos técnicas de balanceo para manejar el desbalance de clases

### 2. Explorando y visualizando los datos

Creamos visualizaciones para entender mejor las relaciones entre variables:

- **Distribuciones univariadas** para entender cada variable individualmente
- **Gráficos de caja** para ver cómo se distribuían variables numéricas por nivel de riesgo
- **Gráficos de barras** para analizar la relación entre variables categóricas y riesgo
- **Matrices de correlación** para identificar relaciones entre variables

**Hallazgos clave:**
- Las variables demográficas mostraban patrones interesantes pero con poder predictivo limitado
- Las variables financieras tenían mayor relación con el nivel de riesgo
- La mayoría de variables numéricas mostraban baja correlación entre sí (poca multicolinealidad)

### 3. Ingeniería de características

Esta fue la parte más creativa y donde aportamos mayor valor al proyecto:

**¿Qué hicimos?** Creamos nuevas variables que capturan mejor el riesgo financiero:

1. **Índice de Presión Financiera**: Combina el ratio deuda-ingreso con el tamaño del préstamo
2. **Índice de Estabilidad de Ingresos**: Pondera el ingreso por la estabilidad laboral
3. **Ratio Préstamo-Activos**: Relación entre el préstamo y el valor total de activos
4. **Factor de Riesgo Crediticio**: Combina puntaje crediticio con historial de incumplimientos

**Resultado:** Estas nuevas características resultaron ser más predictivas que las variables originales, demostrando la importancia del conocimiento del dominio en la ciencia de datos.

### 4. Modelado y evaluación

Implementamos y comparamos tres algoritmos diferentes:

- **Árbol de Decisión**: Por su interpretabilidad y capacidad para capturar relaciones no lineales
- **Random Forest**: Por su robustez y precisión general
- **Red Neuronal MLP**: Para comparar con un enfoque más complejo

**Estrategia de validación:**
- División 70-30 para entrenamiento y prueba
- Muestreo estratificado para mantener la distribución de clases
- Validación cruzada con 5 folds para ajuste de hiperparámetros

**Métricas prioritarias:**
1. **Recall para la clase "Alto Riesgo"**: Fundamental identificar correctamente clientes riesgosos
2. **Precisión general**: Para asegurar un buen rendimiento global
3. **F1-Score macro**: Para evaluar el rendimiento balanceado entre todas las clases

### 5. Optimización

Para mejorar el desempeño de nuestros modelos:

- **Ajuste de hiperparámetros** utilizando RandomizedSearchCV para explorar eficientemente el espacio de parámetros
- **Técnicas de balanceo de clases** para abordar el desbalance en la variable objetivo
- **Selección de características** para quedarnos con el subconjunto más predictivo (15 de 30+ variables)
- **Ponderación de clases** para penalizar más fuertemente la clasificación incorrecta de clientes de alto riesgo

### 6. Resultados y conclusiones

**Resultados principales:**
- Mejoramos la precisión general en un 29%
- Aumentamos el F1-Score en un 23%
- Mantuvimos un alto recall para la clase "Alto Riesgo"
- Logramos un modelo más simple (15 características) que funcionaba mejor que uno más complejo

**Aprendizajes clave:**
1. La ingeniería de características basada en conocimiento del dominio fue más impactante que la elección del algoritmo
2. Los árboles de decisión proporcionaron un buen balance entre rendimiento e interpretabilidad
3. El enfoque en métricas relevantes para el negocio (recall para alto riesgo) fue fundamental para guiar la optimización

## Reflexión metodológica

Este proyecto refuerza varias lecciones importantes sobre la ciencia de datos aplicada:

1. **El contexto de negocio debe guiar las decisiones técnicas**: Priorizamos el recall para alto riesgo porque es más costoso aprobar préstamos a clientes riesgosos que rechazar clientes seguros.

2. **La interpretabilidad es tan importante como el rendimiento**: Optamos por modelos más interpretables porque en aplicaciones financieras, entender el "por qué" de una predicción es casi tan importante como la predicción misma.

3. **La ingeniería de características es un arte y una ciencia**: Combinar conocimiento del dominio con análisis de datos produjo características superiores a las variables originales.

4. **La simplicidad tiene valor**: Reducir de 30+ a 15 características no solo mantuvo sino que mejoró el rendimiento, demostrando que "menos es más" cuando las características son de alta calidad.

## Trabajo futuro

Para futuras iteraciones del proyecto, consideraríamos:

1. **Técnicas avanzadas de balanceo**: Explorar alternativas como SMOTE para preservar más información
2. **Ensamblaje de modelos**: Combinar predicciones de múltiples modelos para mejorar el rendimiento
3. **Optimización multiobjetivo**: Desarrollar una función de pérdida personalizada que priorice el recall para alto riesgo
4. **Validación más robusta**: Implementar validación cruzada estratificada para asegurar resultados consistentes
5. **Variables adicionales**: Incluir variables temporales o geoespaciales que podrían mejorar la capacidad predictiva

---

*Si tienes preguntas sobre la metodología o sugerencias para mejorarla, ¡me encantaría escucharlas!*
