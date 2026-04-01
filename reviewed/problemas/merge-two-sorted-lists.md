# Merge Two Sorted Lists

**Dificultad:** Easy
**Tema(s):** [[linked-list|Linked List]], two pointers
**Tiempo invertido:** 30 minutos (15 min solución rápida, 15 min solución canónica)
**URL:** https://leetcode.com/problems/merge-two-sorted-lists/description/
**Diario:** [[reviewed/diario/2026-03-31]]

## Descripción breve
Dadas las cabezas de dos linked lists ordenadas, fusionarlas en una sola lista ordenada y retornar su cabeza.

## Enfoque de solución
**Dummy head + two pointers**: crear un nodo centinela y un puntero `dummy`. Comparar los valores de ambas listas en cada paso, enlazar el nodo menor al `dummy`, avanzar el puntero de esa lista. Al terminar un de las listas, enlazar directamente el resto de la otra (no hace falta iterar el resto).

## Código final

```cpp
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        ListNode sorted;
        ListNode* dummy = &sorted;

        while (list1 && list2) {
            if (list2->val < list1->val) {
                dummy->next = list2;
                dummy = list2;
                list2 = list2->next;
            } else {
                dummy->next = list1;
                dummy = list1;
                list1 = list1->next;
            }
        }

        dummy->next = list1 ? list1 : list2;

        return sorted.next;
    }
};
```

## Errores cometidos
- Tratar la linked list como un arreglo (acceso por índice)
- Completar el ciclo hasta el final en lugar de cortar cuando una lista se agota y enlazar el resto directamente

## Aprendizajes clave
- `if(p1)` es equivalente a `if(p1 != nullptr)` — se puede omitir la comparación explícita con `nullptr`
- Cuando una lista se agota, se puede reutilizar sus nodos restantes haciendo `dummy->next = nodoExistente` en lugar de seguir iterando
- Patrón dummy head: el nodo centinela se declara en el stack (`ListNode sorted;`) y se trabaja con un puntero `dummy` que lo referencia

## Notas adicionales
- Complejidad: O(n + m) tiempo, O(1) espacio (se reutilizan los nodos existentes)
- Variante: Merge K Sorted Lists — misma idea pero con un heap/priority queue
