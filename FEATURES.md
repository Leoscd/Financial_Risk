# Variables y Características del Modelo

Este documento describe las variables utilizadas en el proyecto de Clasificación de Riesgo Financiero, incluyendo tanto las características originales como las creadas mediante ingeniería de características.

## Variables Originales

El conjunto de datos incluye información demográfica y financiera de los solicitantes de préstamos:

### Variables Demográficas

| Variable | Descripción | Tipo |
|----------|-------------|------|
| Age | Edad del solicitante | Numérico |
| Gender | Género del solicitante | Categórico |
| Education Level | Nivel educativo (Bachillerato, Universitario, Maestría, PhD) | Categórico |
| Marital Status | Estado civil (Soltero, Casado, Divorciado, Viudo) | Categórico |
| Number of Dependents | Número de personas a cargo | Numérico |
| Employment Status | Situación laboral (Empleado, Desempleado) | Categórico |
| Years at Current Job | Años en el empleo actual | Numérico |

### Variables Financieras

| Variable | Descripción | Tipo |
|----------|-------------|------|
| Income | Ingreso anual | Numérico |
| Credit Score | Puntaje crediticio | Numérico |
| Loan Amount | Monto del préstamo solicitado | Numérico |
| Loan Purpose | Propósito del préstamo (Vivienda, Auto, Personal, Negocio) | Categórico |
| Debt-to-Income Ratio | Proporción entre deuda e ingresos | Numérico |
| Assets Value | Valor total de activos | Numérico |
| Previous Defaults | Número de incumplimientos de pago anteriores | Numérico |
| Payment History | Historial de pagos (Bueno, Regular, Malo) | Categórico |
| Marital Status Change | Cambio reciente en estado civil | Numérico |

### Variable Objetivo

| Variable | Descripción | Tipo |
|----------|-------------|------|
| Risk Rating | Nivel de riesgo crediticio (Low, Medium, High) | Categórico |

## Características Creadas

Una de las partes más interesantes del proyecto fue la creación de nuevas características que capturan mejor el riesgo financiero. Estas son las principales:

### 1. Índice de Presión Financiera

```
financial_pressure_index = (Debt-to-Income Ratio) * log(Loan Amount / median(Loan Amount) + 1)
```

**¿Por qué es útil?** Este índice combina la carga de deuda relativa a los ingresos con el tamaño absoluto del préstamo. Captura no solo la proporción de deuda sino también el impacto del monto absoluto del préstamo, proporcionando una visión más completa de la presión financiera sobre el solicitante.

### 2. Índice de Estabilidad de Ingresos

```
income_stability_index = (Income / median(Income)) * (Years at Current Job / max(Years at Current Job))
```

**¿Por qué es útil?** Esta característica pondera los ingresos por la estabilidad laboral, reconociendo que un ingreso alto con empleo inestable puede representar mayor riesgo que un ingreso moderado con alta estabilidad laboral.

### 3. Ratio Préstamo-Activos

```
loan_to_assets_ratio = Loan Amount / (Assets Value + 1)
```

**¿Por qué es útil?** Esta proporción indica cuánto representa el préstamo solicitado en relación al patrimonio total del solicitante, proporcionando una medida de la capacidad de respaldo del préstamo.

### 4. Factor de Riesgo Crediticio

```
credit_risk_factor = (Credit Score / max(Credit Score)) * (1 - Previous Defaults/max(Previous Defaults))
```

**¿Por qué es útil?** Combina el puntaje crediticio con el historial de incumplimientos previos, proporcionando una visión más completa del comportamiento crediticio pasado.

## Importancia de las Características

Después de entrenar nuestros modelos, descubrimos que las características más importantes para predecir el riesgo financiero fueron:

1. **financial_pressure_index** (100%) - Nuestra característica engineered fue la más predictiva
2. **income_stability_index** (87%) - Otra característica creada con gran poder predictivo
3. **Credit Score** (76%) - Un indicador tradicional que sigue siendo relevante
4. **loan_to_assets_ratio** (72%) - Una proporción clave para evaluar capacidad de pago
5. **Years at Current Job** (65%) - La estabilidad laboral resultó ser un factor importante

## Lecciones sobre las Características

Este proyecto reafirmó la importancia de la ingeniería de características en ciencia de datos:

1. **Las relaciones importan más que los valores absolutos**: Las proporciones y relaciones entre variables (como deuda/ingreso) resultaron más predictivas que los valores brutos.

2. **El conocimiento del dominio es crucial**: Entender el contexto financiero nos permitió crear características que capturaran relaciones significativas en los datos.

3. **Menos puede ser más**: Reducimos de 30+ a 15 características y mejoramos el rendimiento, demostrando que la calidad supera a la cantidad.

4. **La interpretabilidad es clave**: Creamos características que no solo son predictivas sino también comprensibles para los stakeholders del negocio.

## Trabajo Futuro

Algunas ideas para mejorar aún más las características en futuras versiones:

1. Incorporar variables temporales (estacionalidad, tendencias)
2. Añadir variables geoespaciales que capturen diferencias regionales
3. Desarrollar indicadores que incorporen factores macroeconómicos
4. Crear características que capturen comportamientos de gasto

---

Si tienes preguntas sobre estas características o sugerencias para nuevas variables, ¡no dudes en contactarme!
