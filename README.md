# LeetCode Notes

Sistema personal de notas para consolidar aprendizajes de LeetCode.

## Cómo usar

1. Escribe tus notas del día en `inbox/` en cualquier formato — sucio está bien
2. Abre Claude Code en este directorio
3. Di: **"procesa el inbox"**
4. Claude organiza todo en `reviewed/` y mueve tus archivos a `inbox/processed/`

## Qué escribir en inbox

No hay formato obligatorio. Puedes incluir:
- Qué problemas resolviste hoy
- Cuánto tiempo tardaste
- Qué aprendiste (conceptos, STL, patrones)
- Qué errores cometiste
- Cómo te sentiste
- El código de tu solución (opcional)
- Links a los problemas

**Ejemplo de entrada válida:**

```
hoy resolví basic calculator, me tardé como 3 horas pero llegué a la solución canónica
aprendí que puedo convertir string a int con num = num * 10 + digit
el stack guarda el signo acumulado, no el total
me trabé mucho con los signos negativos unarios pero al final el manejo de signos ya lo resuelve solo
código: [pegar código aquí]
```

## Estructura

```
inbox/          ← tus notas en sucio
inbox/processed/ ← archivos ya procesados (no tocar)
reviewed/diario/ ← entradas organizadas por día
reviewed/temas/  ← notas por tema (stack, linked-list, etc.)
reviewed/problemas/ ← notas por problema
```
