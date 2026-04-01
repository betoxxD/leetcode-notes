# Add Two Numbers

**Dificultad:** Medium
**Tema(s):** [[linked-list|Linked List]], aritmética con carry
**Tiempo invertido:** 40 minutos (20 min solución sucia, 20 min solución canónica)
**URL:** https://leetcode.com/problems/add-two-numbers/description/
**Diario:** [[reviewed/diario/2026-03-31]]

## Descripción breve
Dadas dos linked lists que representan números en orden inverso, retornar su suma también como linked list en orden inverso.

## Enfoque de solución
**Dummy head**: crear un nodo centinela (`sentinel`) y un puntero `dummy` que lo referencia. Se itera sobre ambas listas sumando dígito a dígito con carry. El `dummy` va avanzando para construir la lista resultado. Al final se retorna `sentinel->next`.

La clave es entender que al hacer `dummy = newNode`, no se modifica el contenido de `sentinel`, solo se reasigna el puntero local `dummy`. Así el centinela siempre apunta al inicio de la lista.

## Código final

```cpp
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode* result = new ListNode();
        ListNode *newNode, *dummy;
        int n1, n2, total, carry = 0;

        dummy = result;

        while (l1 != nullptr || l2 != nullptr) {
            n1 = l1 != nullptr ? l1->val : 0;
            n2 = l2 != nullptr ? l2->val : 0;
            total = n1 + n2 + carry;

            if (total >= 10) {
                total %= 10;
                carry = 1;
            } else {
                carry = 0;
            }

            newNode = new ListNode(total);
            dummy->next = newNode;
            dummy = newNode;

            if (l1 != nullptr) l1 = l1->next;
            if (l2 != nullptr) l2 = l2->next;
        }

        if (carry) {
            dummy->next = new ListNode(carry);
        }

        return result->next;
    }
};
```

## Errores cometidos
- Usar `while(true)` con control de flujo mediante `if/break` interno → solución funciona pero es ilegible
- Lógica de asignación sobrecomplicada: inicializar `current = result`, agregar el total y crear el nodo en el mismo bloque → generaba un nodo extra al final
- El carry sobrante se manejaba dentro del ciclo con el `break`, en lugar de después del ciclo

## Aprendizajes clave
- **Dummy head / nodo centinela**: patrón clásico para construir linked lists. Se crea un nodo ficticio, se itera con un puntero separado, y al final se retorna `sentinel->next`
- **Reasignación de punteros en C++**: `Object *a; Object *b; a = b;` hace que `a` apunte a la misma dirección que `b`, no modifica el contenido. Si luego haces `a = c`, cambias a dónde apunta `a`, pero `b` sigue igual
- El carry sobrante después del último dígito debe manejarse **fuera** del ciclo principal

## Notas adicionales
- Complejidad: O(max(n, m)) tiempo, O(max(n, m)) espacio
- Variante: Add Two Numbers II — los números están en orden normal (requiere revertir las listas o usar stacks)
