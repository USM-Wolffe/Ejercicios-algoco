
# Solución para el Problema de Road Reparation usando Union-Find y Kruskal

Este archivo describe la solución para el problema de encontrar el costo total mínimo para conectar todas las ciudades 
usando el algoritmo de Kruskal y una estructura de datos Union-Find (disjoint-set). Si no es posible conectar todas 
las ciudades, se imprime "IMPOSSIBLE".

## Enunciado del Problema

Dado un conjunto de ciudades conectadas por caminos con costos de reparación asociados, queremos encontrar una manera 
de reparar los caminos de modo que todas las ciudades estén conectadas con el costo total mínimo.

## Enfoque

El problema se resuelve utilizando el algoritmo de Kruskal para encontrar el árbol de expansión mínima (Minimum Spanning Tree, MST). 
Esto asegura que todas las ciudades estén conectadas con el menor costo posible.

### Algoritmo de Kruskal

1. **Ordenar las Aristas:** Ordenamos todos los caminos por su costo en orden ascendente.
2. **Usar Union-Find:** Utilizamos una estructura Union-Find para evitar ciclos al agregar caminos al MST.
3. **Seleccionar Caminos:** Recorremos los caminos en orden ascendente de costo. Si dos ciudades aún no están conectadas, 
   las conectamos y agregamos el costo al resultado.
4. **Verificar Conexión Completa:** Si después de procesar todas las aristas, no se han conectado todas las ciudades, 
   imprimimos "IMPOSSIBLE".

### Código en C++

A continuación, se presenta el código en C++:

```cpp
#include <bits/stdc++.h>

using namespace std;

using ll = long long;

struct edge {
    ll from, to, weight;
};

struct union_find {
    vector<int> e;
    union_find(int n) { e.assign(n, -1); }
    int findSet (int x) { 
        return (e[x] < 0 ? x : e[x] = findSet(e[x]));
    }
    bool sameSet (int x, int y) { return findSet(x) == findSet(y); }
    int size (int x) { return -e[findSet(x)]; }
    bool unionSet (int x, int y) {
        x = findSet(x), y = findSet(y);
        if (x == y) return 0;
        if (e[x] > e[y]) swap(x, y);
        e[x] += e[y], e[y] = x;
        return 1;
    }
};

int main() {
    ll n, m;
    cin >> n >> m;

    vector<edge> graph(m);
    for (ll i = 0; i < m; i++) {
        cin >> graph[i].from >> graph[i].to >> graph[i].weight;
    }

    sort(graph.begin(), graph.end(), [](edge a, edge b){
        return a.weight < b.weight;
    });

    union_find dsu(n+1);
    ll ans = 0, cnt = 0;
    for (edge e : graph) {
        if (dsu.sameSet(e.from, e.to)) continue;
        dsu.unionSet(e.from, e.to);
        ans += e.weight;
        cnt++;
    }

    if (cnt == n-1)
        cout << ans << endl;
    else cout << "IMPOSSIBLE" << endl;
    return 0;
}
```

### Explicación del Código

1. **Definición de la Estructura `edge`:**
   - Representa un camino entre dos ciudades (`from` y `to`) con un costo asociado (`weight`).

2. **Estructura Union-Find:**
   - **`findSet`:** Encuentra el representante del conjunto al que pertenece un nodo con compresión de caminos para optimizar futuras consultas.
   - **`sameSet`:** Verifica si dos nodos están en el mismo conjunto.
   - **`unionSet`:** Une dos conjuntos. La unión se realiza por tamaño para minimizar la profundidad del árbol.

3. **Ordenar las Aristas:**
   - Ordenamos las aristas por costo utilizando una función lambda en `sort`.

4. **Construcción del MST:**
   - Recorremos las aristas ordenadas y usamos `unionSet` para incluir una arista en el MST si conecta dos conjuntos diferentes.
   - Acumulamos el costo de las aristas seleccionadas en la variable `ans`.

5. **Verificación del Resultado:**
   - Si el número de aristas seleccionadas (`cnt`) es igual a `n - 1`, imprimimos el costo total del MST.
   - Si no es posible conectar todas las ciudades, imprimimos "IMPOSSIBLE".

### Análisis de Complejidad

- **Tiempo:**
  - Ordenar las aristas: \( O(m \log m) \), donde \( m \) es el número de caminos.
  - Operaciones de Union-Find: \( O(lpha(n)) \) por operación, donde \( lpha \) es la inversa de la función de Ackermann (muy pequeña, aproximadamente constante).
  - Complejidad total: \( O(m \log m + m \cdot lpha(n)) \), que se aproxima a \( O(m \log m) \).

- **Espacio:**
  - \( O(n + m) \): para almacenar las aristas y la estructura Union-Find.

### Resumen

Este enfoque con Union-Find y Kruskal es eficiente y adecuado para límites grandes como los del problema. La estructura Union-Find optimiza las operaciones de conjunto, haciendo que el algoritmo sea rápido y escalable.
