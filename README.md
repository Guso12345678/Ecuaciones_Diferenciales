# Sistema de Lorenz 83 — Análisis y Visualización en MATLAB
 
Proyecto de la asignatura **Ecuaciones Diferenciales** (IMAT — Comillas ICAI).  
Análisis completo del sistema caótico de Lorenz 83: cálculo simbólico de puntos críticos, estudio de estabilidad mediante eigenvalores y visualización del atractor en 3D.
 
---
 
## Descripción
 
El **sistema de Lorenz 83** es un modelo de ecuaciones diferenciales ordinarias no lineales que describe la dinámica atmosférica simplificada. Es conocido por exhibir comportamiento caótico y por generar atractores extraños en el espacio de fases.
 
El sistema queda definido por las ecuaciones:
 
```
dx/dt = -A·x - y² - z² + A·F
dy/dt = -y + x·y - B·x·z + G
dz/dt = -z + B·x·y + x·z
```
 
Con los parámetros:
 
| Parámetro | Valor |
|---|---|
| A | 0.95 |
| B | 7.91 |
| F | 4.83 |
| G | 4.66 |
 
---
 
## Estructura del proyecto
 
```
lorenz83/
├── lorenz82.mlx                  # Análisis: puntos críticos y estabilidad
├── visualizaciondelorenz.mlx     # Simulación numérica y atractor 3D
└── README.md
```
 
| Archivo | Descripción |
|---|---|
| `lorenz82.mlx` | Resolución simbólica, jacobiana, eigenvalores y clasificación de estabilidad |
| `visualizaciondelorenz.mlx` | Integración numérica con `ode45` y visualización del atractor |
 
---
 
## Cómo ejecutar
 
**Requisitos:** MATLAB R2020a o superior con el Symbolic Math Toolbox.
 
Abrir cada archivo `.mlx` en MATLAB y ejecutar con **Run** o `Ctrl+Enter` sección a sección.
 
---
 
## Contenido de cada script
 
### `lorenz82.mlx` — Análisis de estabilidad
 
1. Define las constantes y variables simbólicas del sistema.
2. Resuelve el sistema igualado a cero para encontrar los **puntos críticos** (equilibrios).
3. Calcula la **matriz jacobiana** del sistema.
4. Evalúa la jacobiana en cada punto crítico y calcula sus **eigenvalores**.
5. Clasifica cada punto según su estabilidad:
```matlab
function stability = determine_stability(eigenvalues)
    if all(real(eigenvalues) < 0)
        stability = 'Estable';
    elseif all(real(eigenvalues) > 0)
        stability = 'Inestable';
    else
        stability = 'Silla';
    end
end
```
 
**Criterio de clasificación:**
 
| Eigenvalores | Tipo de punto |
|---|---|
| Todos con parte real < 0 | Estable (atractor) |
| Todos con parte real > 0 | Inestable (repulsor) |
| Signos mixtos | Punto de silla |
 
### `visualizaciondelorenz.mlx` — Simulación y atractor
 
1. Define el sistema como función anónima en MATLAB.
2. Establece las condiciones iniciales `(-0.2, 2.82, 2.71)`.
3. Integra numéricamente en el intervalo `t ∈ [0, 100]` con el solucionador **`ode45`** (Runge-Kutta de orden 4-5 adaptativo).
4. Genera la gráfica 3D del **atractor de Lorenz 83** con `plot3`.
```matlab
lorenz83 = @(t, xyz) [
    -A * xyz(1) - xyz(2)^2 - xyz(3)^2 + A * F;
    -xyz(2) + xyz(1)*xyz(2) - B*xyz(1)*xyz(3) + G;
    -xyz(3) + B*xyz(1)*xyz(2) + xyz(1)*xyz(3)
];
 
[t, xyz] = ode45(lorenz83, [0 100], [-0.2, 2.82, 2.71]);
plot3(xyz(:,1), xyz(:,2), xyz(:,3));
```
 
---
 
## Conceptos aplicados
 
- Sistemas de EDOs autónomos no lineales
- Puntos de equilibrio y análisis de estabilidad lineal
- Matrices jacobianas y cálculo simbólico
- Eigenvalores y clasificación de puntos críticos
- Integración numérica adaptativa (método Runge-Kutta `ode45`)
- Comportamiento caótico y atractores extraños
---
 
## Tecnologías
 
- MATLAB (Live Scripts `.mlx`)
- Symbolic Math Toolbox — resolución simbólica y jacobiana
- `ode45` — integración numérica de EDOs
- `plot3` — visualización 3D del atractor
---
 
## Autor
 
**Guzman Ignacio Perez Ibarz**
 
Proyecto de Ecuaciones Diferenciales — Grado en Ingeniería Matemática e Inteligencia Artificial (IMAT), Comillas ICAI.
