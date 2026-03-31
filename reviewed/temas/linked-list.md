# Linked List

## Conceptos clave
- Estructura de nodos donde cada nodo tiene un valor y un puntero al siguiente
- En C++: generalmente `struct ListNode { int val; ListNode *next; }`
- Acceso secuencial — no hay acceso aleatorio como en arrays
- Se navega avanzando punteros, no con índices

## Puntero vs Referencia (C++)
- **Puntero**: apunta a una dirección de memoria, se puede reasignar y reutilizar (`ListNode* p = head; p = p->next;`)
- **Referencia**: alias de una variable, no se puede reasignar ni reutilizar (`ListNode& r = *head;`)

## Patrones recurrentes
- **Dos punteros (slow/fast)**: útil para detectar ciclos, encontrar el medio, etc.
- **Algoritmo de Floyd (liebre/tortuga)**: `slow` avanza 1, `fast` avanza 2. Si hay ciclo se encuentran.
- **Dummy head**: nodo ficticio al inicio para simplificar edge cases en inserciones/eliminaciones

## Código de referencia

```cpp
// Validación de head antes de operar
if (head == nullptr) return false;

// Patrón slow/fast — Floyd's cycle detection
ListNode *slow = head, *fast = head;
while (fast->next != nullptr && fast->next->next != nullptr) {
    slow = slow->next;
    fast = fast->next->next;
    if (slow == fast) return true; // ciclo detectado
}
```

## Errores comunes
- No validar `head == nullptr` antes de iterar → crash o TLE
- Avanzar `fast` sin validar `fast->next` y `fast->next->next` → null pointer dereference

## Problemas relacionados
- [[linked-list-cycle|Linked List Cycle]] — Easy
- Linked List Cycle II — Medium
- Middle of the Linked List — Easy
- Merge Two Sorted Lists — Easy
