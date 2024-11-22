
# Solución para el Problema de Book Shop

Este archivo describe la solución para el problema de maximizar el número de páginas que puedes comprar en una tienda 
de libros, dado un presupuesto limitado. Es una variación del clásico problema de la mochila.

## Enunciado del Problema

Tienes una lista de \( n \) libros, donde cada libro tiene un precio \( h[i] \) y un número de páginas \( s[i] \). 
Debes decidir cuáles libros comprar de manera que el costo total sea como máximo \( x \) y la suma de las páginas 
sea máxima.

## Enfoque

El problema se resuelve utilizando **programación dinámica**, similar al problema de la mochila. Usamos un arreglo `dp` 
para almacenar el máximo número de páginas que se pueden obtener con diferentes presupuestos.

### Algoritmo

1. **Definición del Estado de DP**:
   - `dp[j]` será el número máximo de páginas que podemos obtener con un presupuesto de exactamente \( j \).

2. **Transición**:
   - Para cada libro, si lo compramos (si el presupuesto lo permite), actualizamos:
     \[ dp[j] = \max(dp[j], dp[j - h[i]] + s[i]) \]
   - Aquí, \( h[i] \) es el precio del libro \( i \) y \( s[i] \) es el número de páginas del libro \( i \).

3. **Inicialización**:
   - `dp[0] = 0`, porque con un presupuesto de 0, no podemos comprar nada.
   - Inicializamos el resto de `dp` con 0.

4. **Resultado Final**:
   - La respuesta estará en `dp[x]`, que será el máximo número de páginas que podemos comprar con un presupuesto de hasta \( x \).

### Código en C++

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n, x;
    cin >> n >> x;

    vector<int> h(n), s(n);
    for (int i = 0; i < n; i++) cin >> h[i];
    for (int i = 0; i < n; i++) cin >> s[i];

    vector<int> dp(x + 1, 0);

    for (int i = 0; i < n; i++) {
        for (int j = x; j >= h[i]; j--) {
            dp[j] = max(dp[j], dp[j - h[i]] + s[i]);
        }
    }

    cout << dp[x] << endl;

    return 0;
}
```

### Explicación del Código

1. **Lectura de Entrada:**
   - Leemos el número de libros \( n \) y el presupuesto máximo \( x \).
   - Leemos los precios de los libros en el array `h`.
   - Leemos las páginas de los libros en el array `s`.

2. **Inicialización:**
   - Creamos el array `dp` de tamaño \( x + 1 \) e inicializamos con 0.

3. **Transición:**
   - Recorremos cada libro.
   - Para cada presupuesto \( j \), desde \( x \) hacia abajo (para evitar usar el mismo libro más de una vez), actualizamos `dp[j]`.

4. **Resultado:**
   - Imprimimos el valor en `dp[x]`, que contiene el máximo número de páginas que se pueden obtener con el presupuesto \( x \).

### Análisis de Complejidad

**Tiempo:**
1. **Bucle Externo:** Recorremos \( n \) libros (\( O(n) \)).
2. **Bucle Interno:** Para cada libro, recorremos presupuestos desde \( x \) hacia abajo (\( O(x) \)).
3. **Complejidad Total:** \( O(n 	imes x) \).

**Espacio:**
- Usamos un vector `dp` de tamaño \( x + 1 \), por lo que la complejidad espacial es \( O(x) \).

### Ejemplo de Ejecución

#### Entrada:
```
4 10
4 8 5 3
5 12 8 1
```

#### Salida:
```
13
```

**Explicación:**
- Seleccionamos los libros 1 y 3, cuyos precios son \( 4 + 5 = 9 \) y sus páginas son \( 5 + 8 = 13 \).

### Resumen

Este enfoque asegura que el problema se resuelve de manera eficiente incluso para los límites superiores (\( n = 1000 \), \( x = 10^5 \)).
El uso de programación dinámica permite maximizar el número de páginas sin exceder el presupuesto.
