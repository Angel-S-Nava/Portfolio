# ¿Qué deberías arreglar primero?

Diagnóstico de madurez en 18 preguntas sobre 6 áreas. Devuelve puntaje por área y un
plan ordenado por **dependencias**, no por puntaje.

**En vivo:** `https://navamkt.com/herramientas/diagnostico-madurez`

---

## Por qué existe

Es la pieza de entrada del conjunto: la que alguien contesta sin saber qué necesita, y
que lo manda a la herramienta específica que le toca.

Pero la razón de fondo es otra. Casi todos los diagnósticos de madurez devuelven la lista
completa de todo lo que está mal, ordenada de peor a mejor. Eso no sirve: si tu medición
está rota, arreglar la parrilla de redes no cambia nada, y ponerlas en la misma lista
sugiere que son opciones equivalentes.

**Este ordena por dependencias.** Y por eso a veces el área con peor puntaje no aparece
primero.

## La cadena

```
Medición → Sitio que convierte → Tráfico → Atención → Retención
```

Los dos errores de secuencia más caros que existen:

1. **Invertir en pauta antes de que el tracking funcione.** No es que rinda menos: es que
   no vas a saber si rindió. Tres meses después la conversación es "gastamos X y no sé
   qué pasó", y la conclusión es que la publicidad no sirve.
2. **Llevar tráfico pagado a un sitio que no convierte.** Cada peso de pauta multiplica
   lo que ya tienes. Multiplicar un 0.5% sale caro.

CRO va al final aunque suene a lo más sofisticado: sin volumen de conversiones no hay
test que cierre. Y GEO sin presencia básica es optimizar para que te citen cuando
todavía no hay nada que citar.

## Verificado

Dos escenarios corridos contra el motor de reglas:

**Caso A** — invierte en pauta, medición en 0, sitio en 0:

```
1. Instrumenta la medición antes de gastar un peso más
2. Arregla el sitio antes de subirle a la pauta
3. Revisa si tu presupuesto alcanza para salir de aprendizaje
```

**Caso B** — medición 100, sitio 67, pauta 78, atención 100, orgánica 44, retención 0:

```
1. Levanta tu baseline de presencia en IA
2. Antes de contratar CRO, revisa si tienes volumen para testear
3. Empieza a medir satisfacción
4. Ponle estructura a lo que publicas
```

Nótese el caso B: **retención está en 0, el área más baja de las seis, y no aparece
primero.** Las reglas de secuencia mandan sobre el puntaje. Ese es el comportamiento que
distingue esta herramienta de un cuestionario ordenado de peor a mejor.

## Cómo enlaza con el resto

Cada paso del plan enlaza a la herramienta que resuelve ese frente. Las rutas se
construyen con una sola línea al inicio del script:

```js
const RUTA = slug => `../${slug}/index.html`;
```

Funciona con las carpetas hermanas tal como están. Si publicas con otra estructura de
URLs, esa línea es lo único que hay que tocar.

## Montarla

```bash
cp index.html "../../sitio 2/my-next-tailwind/public/herramientas/diagnostico-madurez/index.html"
```

Ojo: si cambias los nombres de carpeta al publicar, actualiza `RUTA` o los enlaces del
plan van a romperse.

## Notas de mantenimiento

Las preguntas viven en `AREAS`, las reglas de secuencia en `reglas()`. Las reglas se
evalúan en orden y la primera que aplica es el paso 1 — agregar una regla nueva es
insertarla en la posición donde corresponda su prioridad, no al final.
