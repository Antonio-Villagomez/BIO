# ⚙️ Hiperparámetros en PSO: ¿Valores Fijos o Dinámicos?

En la Optimización por Enjambre de Partículas (PSO), el comportamiento del enjambre está dictado enteramente por la ecuación de actualización de velocidad. El éxito del algoritmo para resolver un problema depende de tres hiperparámetros clave:

1. **La Inercia ($w$)**
2. **El Coeficiente Cognitivo ($c1$)**
3. **El Coeficiente Social ($c2$)**

Decidir si estos valores deben ser **fijos** durante toda la ejecución o **dinámicos** (que cambien con el tiempo) es fundamental para equilibrar dos conceptos críticos en inteligencia artificial: **Exploración** (buscar en nuevas áreas) vs. **Explotación** (refinar una buena solución encontrada).

---

## 1. El Peso de Inercia ($w$)
Controla qué tanto conserva una partícula su velocidad y dirección anterior.

### ¿Cuándo usar un valor FIJO?
* **Cuándo:** En problemas muy sencillos, unimodales (un solo mínimo, como la función Esfera) o cuando se requiere una solución rápida sin mucha carga computacional.
* **Valores típicos:** Se suele fijar entre `0.7` y `0.8` para mantener un balance constante.
* **El riesgo:** Si $w$ es muy alto, el enjambre nunca converge (se la pasa rebotando). Si es muy bajo, las partículas se detienen rápido y pueden quedar atrapadas en un mínimo local.

### ¿Cuándo usar un valor DINÁMICO?
* **Cuándo:** En problemas multimodales complejos (como la función Rastrigin) o al entrenar modelos de Machine Learning.
* **El concepto:** Implementar una **Inercia Lineal Decreciente** (Linear Decreasing Inertia Weight).
* **Cómo funciona:**
  * **Inicio de iteraciones ($w \approx 0.9$):** Alta inercia. Las partículas ignoran un poco a sus compañeras y dan pasos largos. **Fase de Exploración Global.**
  * **Fin de iteraciones ($w \approx 0.4$):** Baja inercia. Las partículas frenan y se dejan atraer fuertemente por el mejor global. **Fase de Explotación Local.**

---

## 2. Los Coeficientes de Aceleración ($c1$ y $c2$)
Controlan la atracción de la partícula hacia su mejor memoria ($c1$, cognitivo) y hacia la mejor memoria del enjambre ($c2$, social).

### ¿Cuándo usar valores FIJOS?
* **Cuándo:** Es el enfoque estándar y más utilizado. Funciona muy bien para la gran mayoría de los problemas de optimización general.
* **Valores típicos:** Históricamente, se usaba $c1 = 2.0$ y $c2 = 2.0$. Hoy en día, valores alrededor de `1.5` para ambos han demostrado ser más estables para evitar que las partículas aceleren infinitamente.
* **El significado:** Mantener un balance equitativo (`50/50`) entre lo que la partícula cree que es correcto y lo que el grupo le dice.

### ¿Cuándo usar valores DINÁMICOS?
* **Cuándo:** Cuando el algoritmo sufre de convergencia prematura (todo el enjambre colapsa en un mal punto muy rápido) o cuando el espacio de búsqueda es extremadamente irregular.
* **El concepto:** Se conoce como **TVAC (Time-Varying Acceleration Coefficients)**. Consiste en cruzar los valores a lo largo de las iteraciones.
* **Cómo funciona:**
  * **Al inicio (Exploración):** $c1$ alto (ej. `2.5`) y $c2$ bajo (ej. `0.5`). Las partículas confían mucho en su propio instinto y casi no le hacen caso al líder. Se dispersan por todo el mapa.
  * **Al final (Convergencia):** $c1$ baja (ej. `0.5`) y $c2$ sube (ej. `2.5`). Las partículas dejan de buscar individualmente y todas corren juntas hacia el punto que demostró ser el mejor.

---

## 📊 Tabla Resumen de Decisión

| Estrategia | Escenario de Uso | Pros | Contras |
| :--- | :--- | :--- | :--- |
| **Todo Fijo** | Problemas simples, pruebas base rápidas. | Fácil de programar, menor costo de cómputo. | Propenso a estancarse en mínimos locales. |
| **$w$ Dinámico + $c1, c2$ Fijos** | Estándar actual de la industria para algoritmos bioinspirados. | Excelente balance, resuelve el 80% de los problemas complejos. | Requiere afinar bien $w_{max}$ y $w_{min}$. |
| **Todo Dinámico (Inercia + TVAC)** | Funciones de alta complejidad, optimización de redes neuronales profundas. | Búsqueda exhaustiva casi perfecta, evita convergencia prematura. | Agrega cálculos matemáticos extra en cada iteración del bucle. |