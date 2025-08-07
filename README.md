# Simulación del Problema de los Tres Cuerpos: Júpiter, Saturno y Urano

Este proyecto simula el movimiento gravitacional de tres cuerpos: **Júpiter, Saturno y Urano**, utilizando un modelo numérico basado en ecuaciones diferenciales. La simulación se realiza en un entorno tridimensional con la biblioteca `scipy.integrate.solve_ivp`.

---

## 📌 Objetivo

Analizar el comportamiento dinámico del sistema formado por los planetas Júpiter, Saturno y Urano, considerando sus **masas reales relativas** y aplicando las **leyes del movimiento de Newton** y la **ley de gravitación universal**.

---

## ⚙️ Modelo Matemático

### 1. Ley de Gravitación Universal

La fuerza gravitacional que un cuerpo \( j \) ejerce sobre otro cuerpo \( i \) está dada por:

$
\mathbf{F}_{ij} = G \cdot \frac{m_i m_j}{|\mathbf{r}_j - \mathbf{r}_i|^3} (\mathbf{r}_j - \mathbf{r}_i)
$

Donde:
- \( \mathbf{r}_i, \mathbf{r}_j \) son las posiciones de los cuerpos.
- \( m_i, m_j \) son sus masas.
- \( G \) es la constante gravitacional (se normaliza a \( G = 1 \)).

---

### 2. Segunda Ley de Newton

Cada cuerpo cumple:

\[
m_i \cdot \frac{d^2 \mathbf{r}_i}{dt^2} = \sum_{j \ne i} \mathbf{F}_{ij}
\]

La aceleración \( \mathbf{a}_i \) de cada cuerpo es la suma de las fuerzas ejercidas por los otros cuerpos, dividida por su masa.

---

### 3. Sistema de Ecuaciones Diferenciales

Para tres cuerpos en el espacio 3D, se generan 18 ecuaciones diferenciales de primer orden:

- 3 posiciones (x, y, z) por cuerpo → \( 3 \times 3 = 9 \) ecuaciones
- 3 velocidades por cuerpo → \( 3 \times 3 = 9 \) ecuaciones

**Total: 18 EDOs**

---

## 🧮 Datos utilizados

### Masas relativas

| Planeta  | Masa (kg)             | Masa relativa (respecto a Júpiter) |
|----------|------------------------|------------------------------------|
| Júpiter  | \(1.898 \times 10^{27}\) | 1.0                                |
| Saturno  | \(5.683 \times 10^{26}\) | 0.2993                             |
| Urano    | \(8.681 \times 10^{25}\) | 0.0457                             |

> Nota: Se utiliza una escala relativa para facilitar la simulación con \( G = 1 \).

### Posiciones iniciales

Se colocan los cuerpos en los vértices de un triángulo equilátero en el plano XY, con coordenadas tridimensionales.

### Velocidades iniciales

Las velocidades están orientadas tangencialmente al triángulo, de forma similar a la solución de Lagrange (pero el sistema no es estable con masas diferentes).

---

## 🧪 Implementación

### Lenguaje y bibliotecas

- Python 3
- `numpy` para operaciones vectoriales
- `scipy.integrate.solve_ivp` para resolver las EDOs
- `matplotlib` para visualización 3D

### Método de integración

Se utiliza el método de Runge-Kutta de orden 5 (`RK45`) con alta precisión:

```python
solve_ivp(..., rtol=1e-9, atol=1e-9)
