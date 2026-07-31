# Sistema visual — herramientas navamkt

Referencia para mantener las ocho herramientas coherentes entre sí y con
`sitio 2/my-next-tailwind/app/[lang]/globals.css`.

Cada herramienta es un `index.html` autocontenido: el CSS va inline, sin build ni
dependencias. Esa decisión es a propósito — se sube a `public/` de cualquier sitio,
se abre desde el escritorio y sigue funcionando dentro de cinco años.

## Tokens

Los mismos nombres que el sitio, para que un bloque copiado de aquí allá no se rompa.

| Token | Oscuro (default) | Claro |
|---|---|---|
| `--bg` | `hsl(253 20% 4.5%)` | `hsl(40 30% 98.5%)` |
| `--srf` | `hsl(252 15% 7.5%)` | `hsl(0 0% 100%)` |
| `--srf2` | `hsl(252 13% 10.5%)` | `hsl(40 22% 95.5%)` |
| `--line` | `hsl(250 30% 90% / .09)` | `hsl(250 30% 15% / .11)` |
| `--ink` | `hsl(40 20% 95%)` | `hsl(250 20% 8%)` |
| `--mut` | `hsl(248 10% 62%)` | `hsl(248 8% 42%)` |
| `--acc` | `#8B5CF6` | `#8B5CF6` |
| `--ok` | `#34d399` | `#059669` |
| `--warn` | `#fbbf24` | `#b45309` |
| `--bad` | `#f87171` | `#dc2626` |

El acento no cambia entre temas. Los semáforos sí: en fondo claro los tonos
oscuros de `--ok`/`--warn`/`--bad` mantienen el contraste AA sobre blanco.

## Tipografía

- **Outfit** — display. Titulares, cifras grandes. `letter-spacing: -.03em`.
- **Plus Jakarta Sans** — cuerpo.
- **JetBrains Mono** — etiquetas, tablas numéricas, badges. 11px, `.16em`, mayúsculas.

Se cargan de Google Fonts con `display=swap` y pila de respaldo del sistema. Sin
red, la herramienta se ve peor pero funciona igual.

## Estructura de página

```
┌─ Barra superior: marca · selector de tema
├─ Encabezado: etiqueta mono · titular display · párrafo de contexto
├─ Panel de entrada (izquierda) + Panel de resultado (derecha)
├─ Bloque de método: de dónde salen los números
└─ Pie: CTA a navamkt + fecha de última revisión de datos
```

En móvil las dos columnas se apilan y el panel de resultado queda primero al
recalcular, para que el usuario no tenga que buscar el número.

## Reglas que no se rompen

1. **Ningún dato inventado.** Si un número depende de una tarifa que cambia
   (Meta, WhatsApp), es un campo editable con su fecha de referencia, no una
   constante escondida en el código.
2. **El veredicto va antes que el detalle.** Primero la respuesta, después cómo
   se calculó.
3. **Todo cálculo se puede auditar.** Cada herramienta muestra su fórmula.
4. **Cero recolección de datos.** No hay formularios de captura ni analytics
   dentro de la herramienta. El correo se pide después, si la persona quiere el
   reporte — nunca antes de darle el resultado.
5. **Sin dependencias externas.** Ni frameworks, ni CDN, ni librerías de gráficas.

La regla 4 es la que sostiene el resto: una herramienta que da el resultado sin
pedir nada a cambio se comparte sola.
