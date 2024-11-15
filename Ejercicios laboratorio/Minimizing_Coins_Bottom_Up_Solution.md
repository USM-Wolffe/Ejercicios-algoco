
# Solución "Bottom-Up" para el Problema de Minimizing Coins

Este archivo describe el enfoque "bottom-up" para resolver el problema de Minimizing Coins usando programación dinámica. 
El objetivo es minimizar el número de monedas necesarias para alcanzar una suma específica.

## Enunciado del Problema

Dado un conjunto de monedas de distintos valores, queremos encontrar la cantidad mínima de monedas necesarias para formar 
una suma específica, `x`. Si no es posible formar la suma, retornamos `-1`.

## Enfoque "Bottom-Up"

El enfoque "bottom-up" consiste en construir la solución a partir de los casos base hacia el objetivo, llenando un 
vector de DP que almacena el número mínimo de monedas necesarias para cada suma desde `0` hasta `x`.

### Definiciones

- **Estado de DP (`dp[i]`):** `dp[i]` representa el número mínimo de monedas necesarias para obtener la suma `i`.
- **Transición:** Para cada moneda `c` y cada valor de `i` de `1` a `x`, si `i - c >= 0`, actualizamos `dp[i]` como 
  `dp[i] = min(dp[i], dp[i - c] + 1)`.

### Código en C++

A continuación, presentamos el código en C++ que implementa este enfoque "bottom-up".

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int main() {
    int n, x;
    cin >> n >> x;

    vector<int> coins(n);
    for (int i = 0; i < n; i++) {
        cin >> coins[i];
    }

    // Inicialización del vector dp
    vector<int> dp(x + 1, x + 1); // Inicializamos con x + 1 (un valor alto)
    dp[0] = 0; // Base: para una suma de 0, no necesitamos monedas

    // Llenado de dp (algoritmo "bottom-up")
    for (int i = 1; i <= x; i++) {
        for (int coin : coins) {
            if (i >= coin) {
                dp[i] = min(dp[i], dp[i - coin] + 1);
            }
        }
    }

    // Resultado final
    cout << (dp[x] == x + 1 ? -1 : dp[x]) << endl;

    return 0;
}
```

### Explicación Paso a Paso

1. **Lectura de Entradas:** 
   - Leemos el número de monedas `n` y la suma deseada `x`.
   - Leemos los valores de cada moneda en el vector `coins`.

2. **Inicialización del Vector `dp`:**
   - Creamos un vector `dp` de tamaño `x + 1` e inicializamos cada posición con `x + 1`, que es un valor alto. 
     Esto representa un número de monedas que no se puede alcanzar, lo cual nos ayuda a buscar el mínimo.
   - `dp[0] = 0` porque no se necesita ninguna moneda para formar una suma de `0`.

3. **Llenado de `dp` ("Bottom-Up"):**
   - Para cada suma `i` desde `1` hasta `x`, revisamos todas las monedas.
   - Si `i - coin >= 0`, actualizamos `dp[i]` con el mínimo entre su valor actual y `dp[i - coin] + 1`, 
     lo que significa que estamos considerando usar una moneda `coin` adicional para formar la suma `i`.

4. **Impresión del Resultado:**
   - Si `dp[x]` es igual a `x + 1`, significa que no es posible formar la suma `x`, así que imprimimos `-1`.
   - De lo contrario, imprimimos el valor de `dp[x]`, que es el número mínimo de monedas necesarias.

### Análisis de Complejidad

- **Tiempo:** \( O(n 	imes x) \), donde \( n \) es el número de monedas y \( x \) es la suma deseada. Para cada suma desde `1` hasta `x`, 
  iteramos sobre todas las monedas.
- **Espacio:** \( O(x) \), ya que solo usamos un vector `dp` de tamaño `x + 1`.

### Resumen

Este enfoque "bottom-up" es eficiente y adecuado para competencias de programación, ya que evita la recursión y 
controla explícitamente el orden en el que se construyen las soluciones. Es especialmente útil en problemas con límites grandes.
