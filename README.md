# Sumador/Restador de 4 bits 

Este proyecto consiste en el diseño e implementación de un **Sumador/Restador de 4 bits en paralelo** utilizando la arquitectura de **Complemento a 2**. El circuito fue diseñado originalmente para el módulo de Hardware Digital (ISF-215) de la Universidad de Valparaíso.

La simulación y validación funcional del sistema se realizaron de manera lógica y abstracta a través de la plataforma **CircuitVerse**.

## 🚀 Características del Módulo

* **Entradas:** * Número $A$ de 4 bits ($A_3, A_2, A_1, A_0$)
  * Número $B$ de 4 bits ($B_3, B_2, B_1, B_0$)
  * Selector de operación `Subtract/Add` ($0$ para Sumar, $1$ para Restar).
* **Salidas:** * Resultado $S$ de 4 bits ($S_3, S_2, S_1, S_0$)
  * Acarreo de salida final ($C_{out}$).
* **Optimización de Hardware:** Implementa inversores condicionales mediante compuertas XOR para unificar ambas operaciones aritméticas en un único bloque sumador central en paralelo, evitando la duplicación de componentes físicos.

---

## 📊 Fundamento Teórico

El circuito se basa en la estructura repetitiva de un **Sumador Completo (Full Adder)** de 1 bit.

### Tabla de Verdad (Celda genérica - Bit $i$)

| $A_i$ | $B_i^*$ | $C_i$ | Resultado ($S_i$) | Acarreo Saliente ($C_{i+1}$) |
| :---: | :---: | :---: | :---: | :---: |
|   0   |   0   |   0   |       0       |               0               |
|   0   |   0   |   1   |       1       |               0               |
|   0   |   1   |   0   |       1       |               0               |
|   0   |   1   |   1   |       0       |               1               |
|   1   |   0   |   0   |       1       |               0               |
|   1   |   0   |   1   |       0       |               1               |
|   1   |   1   |   0   |       0       |               1               |
|   1   |   1   |   1   |       1       |               1               |

*Nota: $B_i^*$ representa el bit del Número $B$ condicionado por el control de operación ($B_i^* = B_i \oplus \text{Ctrl}$).*

### Ecuaciones Booleanas Simplificadas

A partir del análisis por Mapas de Karnaugh de la tabla anterior, se deducen las expresiones que rigen el comportamiento del bloque lógico:

* **Resultado ($S_i$):** $$S_i = A_i \oplus B_i^* \oplus C_i$$
* **Acarreo Saliente ($C_{i+1}$):** $$C_{i+1} = (A_i \cdot B_i^*) + (C_i \cdot (A_i \oplus B_i^*))$$

---

## 💻 Diagrama e Implementación

El diseño final fue montado utilizando los bloques lógicos modulares de **CircuitVerse**. 

### Pruebas de Validación Ejecutadas:
1. **Suma Básica ($3 + 2$):** Con `Ctrl = 0`, ingresando $A = 0011$ y $B = 0010$, las salidas reflejan de forma correcta el binario `0101` ($5$ en decimal).
2. **Resta Básica ($3 - 2$):** Con `Ctrl = 1`, las compuertas XOR aplican el complemento a 1 sobre el canal $B$ e ingresan un acarreo inicial $C_{in} = 1$, completando de forma automática el Complemento a 2. La salida cambia a `0001` ($1$ en decimal).
3. **Resta con Resultado Cero ($2 - 2$):** Con `Ctrl = 1`, ingresando valores idénticos en ambos canales, el sistema apaga todos los LEDs de resultado (`0000`) y activa el pin $C_{out}$, validando la aritmética modular de la resta.

---

## 🛠️ Tecnologías Utilizadas

* **Simulador Lógico:** CircuitVerse
* **Documentación:** Markdown & $\LaTeX$ para ecuaciones.

## 🧑‍💻 Autor

* **Juan** - Estudiante de Ingeniería, Universidad de Valparaíso.

* 1. Descarga el archivo `tu_archivo.cv` de este repositorio.
2. Ve al simulador web de 1. Descarga el archivo `tu_archivo.cv` de este repositorio.
2. Ve al simulador web de [CircuitVerse](https://circuitverse.org).
3. En el menú superior, haz clic en **Project** (Proyecto) > **Import Project** (Importar Proyecto).
4. Selecciona el archivo descargado para cargar el diseño..
5. o link directo para ver: https://circuitverse.org/users/436935/projects/tarea-4-modulo-avanzado-sumador-restador-de-bytes
3. En el menú superior, haz clic en **Project** (Proyecto) > **Import Project** (Importar Proyecto).
4. Selecciona el archivo descargado para cargar el diseño.
