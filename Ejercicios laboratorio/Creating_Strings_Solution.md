
# Solución para el Problema de Creating Strings usando Permutaciones

Este archivo describe la solución para el problema de crear todas las permutaciones únicas de un string dado, 
mostrando el número total de permutaciones y cada una de ellas en orden alfabético.

## Enunciado del Problema

Dado un string de longitud `n` compuesto por letras entre `a` y `z`, queremos encontrar todas las permutaciones 
únicas posibles del string, imprimir el número total de permutaciones y luego imprimir cada permutación en orden alfabético.

## Enfoque

El enfoque utiliza la función `next_permutation` de la biblioteca estándar de C++ para generar todas las permutaciones únicas 
en orden lexicográfico. Este enfoque es eficiente y fácil de implementar para el rango de valores permitido (`n` entre 1 y 8).

### Descripción del Algoritmo

1. **Ordenar el String**: Ordenamos el string de entrada para asegurar que las permutaciones se generen en orden lexicográfico.
2. **Generar Permutaciones Únicas**: Utilizamos un bucle `do-while` con `next_permutation` para generar cada permutación única.
3. **Contar y Almacenar**: Contamos cada permutación generada y la almacenamos en un vector para imprimirla después.
4. **Imprimir el Resultado**: Primero imprimimos el número total de permutaciones y luego cada permutación almacenada.

### Código en C++

A continuación, presentamos el código en C++:

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    string a;
    cin >> a;
    vector<string> combinaciones;
    sort(a.begin(), a.end()); // Ordenar el string para obtener permutaciones en orden lexicográfico
    int cont = 0;

    // Generar todas las permutaciones únicas
    do {
        string comb;
        for (char l : a) {
            comb += l;
        }
        combinaciones.push_back(comb);
        cont++;
    } while (next_permutation(a.begin(), a.end()));

    // Imprimir el número total de permutaciones
    cout << cont << endl;

    // Imprimir cada permutación en orden
    for (string s : combinaciones) {
        cout << s << endl;
    }

    return 0;
}
```

### Explicación Paso a Paso

1. **Lectura de Entrada**:
   - Leemos el string `a` de la entrada estándar.

2. **Ordenar el String**:
   - Usamos `sort(a.begin(), a.end())` para ordenar el string inicialmente, de modo que `next_permutation` genere las 
     permutaciones en orden lexicográfico.

3. **Generar y Almacenar Permutaciones**:
   - En el bucle `do-while`, generamos cada permutación única del string `a` y la almacenamos en el vector `combinaciones`.
   - Contamos cada permutación usando la variable `cont`.

4. **Impresión de Resultados**:
   - Imprimimos `cont`, que representa el número total de permutaciones únicas.
   - Luego, imprimimos cada permutación en `combinaciones`, que ya están en orden lexicográfico.

### Análisis de Complejidad

- **Tiempo:** Para `n <= 8`, el número de permutaciones únicas es manejable. La complejidad es aproximadamente \( O(n! \cdot n) \) 
  debido a las permutaciones y a la impresión de cada una.
- **Espacio:** \( O(n!) \), ya que almacenamos todas las permutaciones en el vector `combinaciones`.

### Resumen

Este enfoque basado en `next_permutation` es directo y adecuado para el rango de valores dado. Permite generar y listar todas 
las permutaciones de forma eficiente, asegurando que se mantenga el orden lexicográfico.
