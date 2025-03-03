# Modelado y Simulacion

Repositorio de la asignatura ***Modelado y Simulacion***, talleres, tabajos, proyectos

### **Edward Fabian Goyeneche Velandia**
### **Universidad Nacional de Colombia- Sede Manizales**
### **2024-II**


------------------------


## **Aplicacion Real**:


En este caso se va tomar los valores reales de los que pasa en  a un  formula 1 en una carrea real en una recta que va por un tiempo y velocidad en especifico.

- **Coeficiente de arrastre aerodinámico ($C_d$)**= $0.7$ (más alto que un automóvil normal debido a la carga aerodinámica).


- **Densidad del aire ($\rho$)**= $1.225$, $\text{kg/m}^3$ (a nivel del mar).  


- **Área frontal ($A$)**= $1.5$ $\text{m}^2$ 


- **Masa del coche ($m$)**= $800$ $\text{kg}$ (incluyendo al piloto).  


- **Velocidad inicial ($v_0$)**: $80  \text{m/s}$ (equivalente a $ 288  \text{km/h}$.)



La ecuación es:  

$$ \frac{dv}{dt} = - \frac{C_d \rho A}{2m} v^2 $$


### Cálculo del coeficiente (\(k\)):

$$k = \frac{C_d \rho A}{2m}$$

Sustituyendo los valores:  

$$k = \frac{0.7 \cdot 1.225 \cdot 1.5}{2 \cdot 800}$$

Calculamos:  

$$k = \frac{1.28625}{1600} \approx 0.000804 \, \text{s}^{-1}.$$


La ecuación queda:  

$$\frac{dv}{dt} = - 0.000804 v^2$$

```python
import numpy as np
import matplotlib.pyplot as plt

# Parámetros
C_d = 0.7
rho = 1.225
A = 1.5
m = 800
v0 = 80  # Velocidad inicial en m/s
k = (C_d * rho * A) / (2 * m)

# Función que describe la ecuación diferencial
def dvdt(v, t):
    return -k * v**2

# Tiempo de simulación
t = np.linspace(0, 50, 500)  # 50 segundos, 500 puntos

# Solución numérica de la ecuación diferencial
from scipy.integrate import odeint
v = odeint(dvdt, v0, t)

# Graficar los resultados
plt.plot(t, v)
plt.xlabel('Tiempo (s)')
plt.ylabel('Velocidad (m/s)')
plt.title('Simulación de la velocidad de un coche de F1 en una recta')
plt.grid(True)
plt.show()
```