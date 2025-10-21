# 🧠 Control de Horno mediante Programación Genética (DEAP)

Este proyecto implementa un **controlador evolutivo** usando **Programación Genética (PG)** con la librería [DEAP](https://deap.readthedocs.io/en/master/).  
El objetivo es que el algoritmo encuentre **automáticamente la expresión matemática (ley de control)** que minimice el error de temperatura en un horno con la siguiente dinámica:

\[
T_{nueva} = T + G \cdot P - k_p \cdot (T - T_{amb})
\]

donde:
- \( T \): temperatura actual del horno
- \( G \): ganancia del calentador
- \( P \): potencia aplicada por el controlador
- \( k_p \): coeficiente de pérdida térmica
- \( T_{amb} \): temperatura ambiente

---

## 🚀 Objetivo

Evolucionar una función \( P = f(error, error\_prev, P\_prev, T) \) que controle el horno y minimice el **error promedio** con respecto a una referencia de temperatura \( T_{ref} \).

El algoritmo busca automáticamente expresiones matemáticas que actúen como controladores tipo P, PI, PID o incluso más complejos.

---

## 🧩 Características principales

- Implementación basada en **DEAP** y **gp.PrimitiveTree**
- Entradas del controlador: `error`, `error_prev`, `P_prev`, `T`
- Operadores genéticos: selección por torneo, cruce de un punto, mutación uniforme
- Constantes evolutivas aleatorias (simulan Kp, Ki, etc.)
- Visualización de temperatura y potencia a lo largo del tiempo
- Registro estadístico de la evolución (`gen`, `min`, `avg`)

---

## 📁 Estructura

```
├── control_horno_gp.py     # Código principal
├── README.md               # Este archivo
└── requirements.txt         # Librerías necesarias
```

---

## ⚙️ Requisitos

Instala las dependencias necesarias ejecutando:

```bash
pip install deap matplotlib numpy
```

---

## ▶️ Ejecución

Ejecuta el archivo principal:

```bash
python control_horno_gp.py
```

Durante la ejecución verás un log como el siguiente:

```
gen nevals min avg
0   150   27.12 167.24
1   93    27.12 153.24
...
60  90    24.80 42.57
```

Y al final:

```
🏆 Mejor controlador evolutivo encontrado:
(add (mul 1.27 error) (mul 0.43 error_prev))
Aptitud (error promedio): 2.134
```

Esto representa una **ley de control evolutiva** similar a un controlador PI:

\[ P = 1.27 \cdot error + 0.43 \cdot error_{prev} \]

---

## 📊 Resultados

Se generan dos gráficos:
1. **Temperatura vs tiempo** (en azul) con la referencia deseada (en rojo).
2. **Potencia aplicada** por el controlador evolutivo.

Ejemplo:

![example](https://i.imgur.com/Yh4gV7n.png)

---

## 🧠 Conceptos clave

| Término | Descripción |
|----------|--------------|
| `gen` | Número de generación evolutiva |
| `nevals` | Número de individuos evaluados en esa generación |
| `min` | Mejor valor de aptitud (error más bajo) |
| `avg` | Promedio de error de la población |

---

## 🔧 Parámetros del algoritmo

| Parámetro | Valor | Descripción |
|------------|--------|-------------|
| `n` | 150 | Tamaño de la población |
| `cxpb` | 0.5 | Probabilidad de cruce |
| `mutpb` | 0.3 | Probabilidad de mutación |
| `ngen` | 60 | Número de generaciones |
| `tournsize` | 3 | Tamaño del torneo de selección |

Puedes ajustar estos valores para explorar el desempeño del algoritmo.

---

## 📚 Referencias

- Martínez, J. J. *Programación Genética – Conceptos Básicos* (UNAL, 2025)
- Koza, J. (1992). *Genetic Programming: On the Programming of Computers by Means of Natural Selection.* MIT Press.
- DEAP Documentation: [https://deap.readthedocs.io](https://deap.readthedocs.io)

---

## 🧾 Licencia

Este proyecto es de libre uso educativo. Creado con fines didácticos para demostrar la aplicación de **Programación Genética** en **control de sistemas dinámicos**.

---

✨ *Desarrollado con Python 3 y DEAP – Ejemplo de IA Evolutiva aplicada al Control de Procesos.*
