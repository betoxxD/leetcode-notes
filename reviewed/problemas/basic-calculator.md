# Basic Calculator

**Dificultad:** Hard
**Tema(s):** [[stack|Stack]], parsing de expresiones, manejo de signos
**Tiempo invertido:** ~3 horas (3 versiones)
**URL:** https://leetcode.com/problems/basic-calculator/
**Diario:** [[2026-03-30]]

## Descripción breve
Evaluar una expresión matemática dada como string con `+`, `-`, paréntesis y espacios. Solo suma y resta, sin multiplicación ni división.

## Enfoque de solución
Usar un stack para guardar el **signo acumulado** al entrar a cada paréntesis (no el total ni el signo anterior). Como solo hay suma y resta, el orden de evaluación no importa — se puede sumar al total en cualquier momento. El signo efectivo de un número es `sign * backSign.top()`.

- Al encontrar `(`: push del signo acumulado (`backSign.top() * sign`), reset `sign = 1`
- Al encontrar `)`: sumar el número pendiente y hacer pop
- Al encontrar `+` o `-`: sumar el número pendiente, actualizar `sign`
- Al final del loop: sumar el último número pendiente

## Código final

```cpp
class Solution {
public:
    int calculate(string s) {
        int sign = 1;
        int total = 0;
        stack<int> backSign;
        backSign.push(1);
        unsigned int num = 0;
        for (int i = 0; i < s.size(); i++) {
            if (s[i] == ' ') continue;
            if (isdigit(s[i])) {
                num = num * 10 + (s[i] - '0');
            } else if (s[i] == '(') {
                backSign.push(backSign.top() * sign);
                sign = 1;
            } else if (s[i] == ')') {
                total += num * sign * backSign.top();
                backSign.pop();
                sign = 1;
                num = 0;
            } else {
                total += num * sign * backSign.top();
                sign = (s[i] == '+') ? 1 : -1;
                num = 0;
            }
        }
        total += num * sign * backSign.top();
        return total;
    }
};
```

## Errores cometidos
- Primera versión: modificaba el string antes del loop para manejar negativos unarios — parche innecesario
- Segunda versión: usaba `stoi`, tronaba con overflow en números grandes, parcheado con `stoll`
- No vio desde el inicio que el signo acumulado era lo que necesitaba guardar en el stack

## Aprendizajes clave
- Guardar el **signo acumulado** en el stack, no el total ni el signo anterior
- Los signos negativos unarios se resuelven solos con el stack de signos — no necesitan manejo especial
- Acumular dígitos con `num = num * 10 + (c - '0')` evita overflow y dependencia de `stoi`/`stoll`
- Representar signos como enteros (1 y -1) y multiplicar es más limpio que manejar chars
- Hacer `continue` en espacios dentro del loop — no limpiar el string antes

## Notas adicionales
- Complejidad: O(n) tiempo, O(n) espacio por el stack
- Para Basic Calculator II (sin paréntesis, con `*` y `/`) el approach cambia — el stack guarda operandos, no signos
