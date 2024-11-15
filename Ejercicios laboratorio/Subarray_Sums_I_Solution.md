
# Solución para el Problema de Subarray Sums I usando el Método de Dos Punteros

Este archivo describe el enfoque "Two Pointers" o "Sliding Window" para resolver el problema de encontrar la 
cantidad de subarreglos que suman exactamente a un valor objetivo `x`. Esta técnica es eficiente para problemas de 
sumas de subarreglos y cumple con los requisitos de tiempo para los límites dados.

## Enunciado del Problema

Dado un arreglo de `n` enteros positivos, queremos contar la cantidad de subarreglos que tienen una suma exactamente igual a `x`.

## Enfoque

El enfoque "Two Pointers" consiste en utilizar dos punteros para crear una ventana que se expande y contrae a medida 
que movemos el puntero derecho (o "fin") a través del arreglo, y ajustamos el puntero izquierdo (o "inicio") según sea 
necesario para cumplir con la suma objetivo.

### Descripción del Algoritmo

1. **Inicializamos dos punteros** `start` y `end` al principio del arreglo, y una variable `current_sum` en 0.
2. **Expandimos la ventana** sumando el valor de `end` a `current_sum` mientras movemos `end` hacia la derecha.
3. **Ajustamos la ventana** moviendo `start` hacia la derecha cuando `current_sum` supera `x`. Restamos el valor de 
   `start` de `current_sum` cada vez que movemos `start`.
4. **Contamos subarreglos** cada vez que `current_sum` es igual a `x`.

### Código en C++

A continuación, presentamos el código en C++ que implementa este enfoque:

```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {
    int n, x;
    cin >> n >> x;

    vector<int> arr(n);
    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }

    int start = 0, current_sum = 0, count = 0;

    for (int end = 0; end < n; end++) {
        current_sum += arr[end];

        // Ajustamos el puntero start hasta que la suma sea <= x
        while (current_sum > x && start <= end) {
            current_sum -= arr[start];
            start++;
        }

        // Contamos el subarreglo si la suma es exactamente x
        if (current_sum == x) {
            count++;
        }
    }

    cout << count << endl;

    return 0;
}
```

### Explicación Paso a Paso

1. **Lectura de Entradas:** 
   - Leemos el tamaño del arreglo `n` y el objetivo de suma `x`.
   - Leemos el contenido del arreglo `arr`.

2. **Inicialización de Variables:**
   - `start`: puntero izquierdo de la ventana, inicialmente en 0.
   - `current_sum`: almacena la suma de la ventana actual.
   - `count`: contador de subarreglos que cumplen la condición.

3. **Expansión de la Ventana (Bucle de `end`):**
   - Recorremos el arreglo con `end`, sumando `arr[end]` a `current_sum` en cada paso.

4. **Ajuste de la Ventana (Bucle `while`):**
   - Si `current_sum` supera `x`, movemos el puntero `start` hacia la derecha, restando `arr[start]` de `current_sum` 
     hasta que `current_sum <= x`.

5. **Contar Subarreglos:**
   - Cada vez que `current_sum` es igual a `x`, incrementamos `count`.

6. **Impresión del Resultado:**
   - Imprimimos `count`, que representa la cantidad de subarreglos cuya suma es igual a `x`.

### Análisis de Complejidad

- **Tiempo:** \( O(n) \), ya que `start` y `end` solo avanzan hacia la derecha sin retroceder, lo que garantiza una 
  complejidad lineal.
- **Espacio:** \( O(1) \), ya que solo utilizamos variables adicionales y no estructuras de datos proporcionales al tamaño del arreglo.

### Resumen

Este enfoque "Two Pointers" es óptimo para este tipo de problema de suma de subarreglos, ya que evita recalcular sumas 
de subarreglos múltiples veces y logra resolver el problema en tiempo lineal. Esta técnica es muy común en competencias 
de programación para problemas de sumas en subarreglos.
