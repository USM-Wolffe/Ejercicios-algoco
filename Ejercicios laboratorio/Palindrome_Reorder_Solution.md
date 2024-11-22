
# Solución para el Problema de Palindrome Reorder

Este archivo describe la solución para el problema de reorganizar las letras de un string para formar un palíndromo.
El objetivo es verificar si es posible formar un palíndromo y, en caso afirmativo, construir uno.

## Enunciado del Problema

Dado un string de longitud \( n \), queremos reorganizar sus letras para que forme un palíndromo, es decir, que se lea 
igual hacia adelante y hacia atrás. Si no es posible, se debe imprimir "NO SOLUTION".

## Enfoque

El problema se puede resolver contando las frecuencias de las letras en el string. Un palíndromo solo es posible si:

1. **Cuando \( n \) es par:** Todas las letras deben aparecer un número par de veces.
2. **Cuando \( n \) es impar:** Solo una letra puede aparecer un número impar de veces; el resto debe tener frecuencias pares.

### Algoritmo

1. **Ordenar el String:** Ordenamos las letras para procesarlas en orden lexicográfico.
2. **Construcción del Palíndromo:** Usamos una cola para almacenar la mitad izquierda y una pila para la mitad derecha.
   - Cada vez que una letra aparece dos veces consecutivas, una se agrega a la cola y otra a la pila.
   - Si hay una letra con frecuencia impar, se almacena como el carácter central del palíndromo.
3. **Construir el Resultado Final:** Combinamos la cola (mitad izquierda), el carácter central (si existe) y la pila (mitad derecha).

### Código en C++

A continuación, presentamos el código en C++:

```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

int main() {
    string linea;
    cin >> linea;

    queue<char> cola;
    stack<char> pila;
    string ans1 = "";
    char solo;

    sort(linea.begin(), linea.end());
    for (int i = 0; i < linea.size(); i++) {
        if (linea[i] == linea[i + 1]) {
            cola.push(linea[i]);
            pila.push(linea[i]);
            i += 1;
        } else {
            solo = linea[i];
        }
    }

    while (!cola.empty()) {
        ans1 += cola.front();
        cola.pop();
    }

    if (linea.size() % 2 == 1) {
        ans1 += solo;
        while (!pila.empty()) {
            ans1 += pila.top();
            pila.pop();
        }
    } else {
        while (!pila.empty()) {
            ans1 += pila.top();
            pila.pop();
        }
    }

    if (ans1.size() == linea.size()) {
        cout << ans1;
    } else {
        cout << "NO SOLUTION";
    }

    return 0;
}
```

### Explicación del Código

1. **Lectura de Entrada:**
   - Leemos el string de entrada `linea`.

2. **Ordenar el String:**
   - Ordenamos el string para que las letras queden en orden lexicográfico, lo que facilita la agrupación de caracteres iguales.

3. **Construcción del Palíndromo:**
   - Procesamos cada carácter del string.
   - Si encontramos dos letras consecutivas iguales, una se almacena en la cola (mitad izquierda) y otra en la pila (mitad derecha).
   - Si hay una letra que no tiene pareja, se almacena como `solo`, el carácter central.

4. **Construcción del Resultado Final:**
   - Agregamos los caracteres de la cola al string `ans1`.
   - Si el tamaño del string es impar, agregamos el carácter central `solo` al resultado.
   - Finalmente, agregamos los caracteres de la pila al string `ans1`.

5. **Verificación y Resultado:**
   - Si el tamaño de `ans1` coincide con el del string original, imprimimos `ans1`.
   - En caso contrario, imprimimos "NO SOLUTION".

### Análisis de Complejidad

**Tiempo:**
1. **Ordenar el String:** Ordenar el string toma \( O(n \log n) \), donde \( n \) es la longitud del string.
2. **Construcción del Palíndromo:**
   - Procesar los caracteres es \( O(n) \), ya que recorremos el string una vez para agrupar las letras.
   - Manejar la cola y la pila también es \( O(n) \), ya que cada operación de inserción o eliminación es constante.
3. **Construcción del Resultado Final:** Combinar las mitades izquierda y derecha, junto con el carácter central, es \( O(n) \).

**Espacio:**
- Usamos una cola y una pila, ambas de tamaño proporcional a \( n/2 \) en el peor caso. Esto da un uso espacial de \( O(n) \).
- El espacio total es \( O(n) \).

**Complejidad Total:**
- Tiempo: \( O(n \log n) \), dominado por el ordenamiento.
- Espacio: \( O(n) \), para almacenar la cola, la pila y el string intermedio.

### Resumen

Este enfoque asegura que el problema se resuelve de manera eficiente incluso para los límites superiores (\( n = 10^6 \)). La clave está en el uso de estructuras auxiliares (cola y pila) y el ordenamiento para manejar las letras del string de manera controlada.
