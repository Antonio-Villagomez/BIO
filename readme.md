# 🧬 Algoritmos Bioinspirados y Cómputo Evolutivo

Repositorio dedicado al estudio, implementación y aplicación de algoritmos bioinspirados y técnicas de cómputo evolutivo. Este espacio contiene prácticas y códigos desarrollados durante el curso de **Licenciatura en Ciencia de Datos**.

---

## Contenido del Repositorio

* **`📂 pso`**: Implementación en Python (utilizando NumPy) del algoritmo de **Optimización por Enjambre de Partículas (PSO)** aplicado sobre la compleja **Función de Rastrigin** de 10, 20 y hasta 30  dimensiones, junto a diversas experimentaciones con sus parametros.

---

## ¿Qué es PSO (Particle Swarm Optimization)?
En este caso definido como:

$V_i^t= V_i^{t-1} w +c_2r_2  ( pbest_i^{t-1}-x_i^{t-1})+ c_1r_1(rbest-x_i^{t-1})$

El PSO es un algoritmo de optimización estocástica basado en población, inspirado en el comportamiento social de las bandadas de aves o bancos de peces. Cada solución candidata se denomina **partícula**, la cual se desplaza a través del espacio de búsqueda ajustando su velocidad en función de:
1. Su propia experiencia histórica (**pBest**).
2. La mejor experiencia global encontrada por todo el enjambre (**gBest**).

---

## 🚀 Implementación: PSO 
Durante los experimentos se busca resolver la siguiente función:
$\sum_{i=1}^{n=10} x^2-10\cos(2π x_i)+10$
