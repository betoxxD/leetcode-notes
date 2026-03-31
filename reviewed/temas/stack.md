# Stack

## Conceptos clave
- Estructura LIFO (Last In, First Out)
- En C++: `std::stack<T>` del header `<stack>`
- Operaciones principales: `push()`, `pop()`, `top()`, `empty()`, `size()`

## Patrones recurrentes
- **Lazy deletion**: no modificar el heap/stack directamente, insertar versión nueva y validar al leer
- **Signo acumulado**: guardar el signo contextual en el stack al entrar a paréntesis, no el total
- **Monotonic stack**: mantener el stack en orden creciente o decreciente para problemas de "siguiente mayor elemento"

## Código de referencia

```cpp
// Conversión de string a entero sin stoi (dígito a dígito)
unsigned int num = 0;
for (char c : s) {
    if (isdigit(c)) {
        num = num * 10 + (c - '0');
    }
}

// Manejo de signos con stack (Basic Calculator pattern)
int sign = 1;
int total = 0;
stack<int> backSign;
backSign.push(1);

// Al encontrar '(': acumular signo en stack
backSign.push(backSign.top() * sign);
sign = 1;

// Al encontrar ')': sumar y restaurar
total += num * sign * backSign.top();
backSign.pop();
sign = 1;
num = 0;
```

## Errores comunes
- Usar `stoi` con números que pueden hacer overflow → usar `stoll` o acumular con `num * 10 + digit`
- Intentar modificar el tope del stack directamente en lazy deletion → siempre insertar entrada nueva
- No manejar el último número al final del string (fuera del loop) → siempre procesar `num` después del loop

## Problemas relacionados
- Min Stack — Medium
- Evaluate Reverse Polish Notation — Medium
- [[basic-calculator|Basic Calculator]] — Hard
- Simplify Path — Medium
