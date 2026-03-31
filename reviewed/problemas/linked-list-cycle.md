# Linked List Cycle

**Dificultad:** Easy
**Tema(s):** [[linked-list|Linked List]], algoritmo de Floyd (liebre/tortuga)
**Tiempo invertido:** 1 hora (15 min solución simple, 45 min solución óptima)
**URL:** https://leetcode.com/problems/linked-list-cycle
**Diario:** [[2026-03-31]]

## Descripción breve
Dado el `head` de una linked list, determinar si la lista contiene un ciclo (algún nodo apunta a un nodo anterior).

## Enfoque de solución
Dos approaches:
1. **Hash set**: guardar punteros a nodos visitados. Si se vuelve a ver uno, hay ciclo. O(n) tiempo, O(n) espacio.
2. **Floyd / liebre-tortuga**: dos punteros, `slow` avanza 1 paso y `fast` avanza 2. Si hay ciclo, eventualmente se encuentran. O(n) tiempo, O(1) espacio.

## Código final

```cpp
class Solution {
public:
    bool hasCycle(ListNode* head) {
        ListNode *slow, *fast;

        if (head == nullptr) {
            return false;
        }

        slow = head;
        fast = head;

        while (fast->next != nullptr && fast->next->next != nullptr) {
            fast = fast->next->next;
            if (slow == fast) {
                return true;
            }
            slow = slow->next;
        }

        return false;
    }
};
```

## Errores cometidos
- No validar `head == nullptr` al inicio → TLE

## Aprendizajes clave
- Siempre validar `head` antes de iterar sobre una linked list
- El algoritmo de Floyd funciona porque si hay ciclo, `fast` alcanza a `slow` dentro del ciclo (demostrable matemáticamente)
- **Puntero vs referencia en C++**: el puntero apunta a una dirección de memoria y se puede reasignar; la referencia es un alias y no se puede reasignar ni reutilizar

## Notas adicionales
- Complejidad Floyd: O(n) tiempo, O(1) espacio
- Variante: Linked List Cycle II — pide el nodo donde empieza el ciclo (Floyd extendido con dos fases)
