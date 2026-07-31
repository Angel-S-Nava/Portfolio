# Diseña una encuesta NPS que sí puedas leer

Calcula cuántas respuestas vas a obtener, qué puedes concluir con ellas, y cuál es el
intervalo de confianza real de tu NPS. Incluye un revisor de redacción de la pregunta.

**En vivo:** `https://navamkt.com/herramientas/encuesta-nps`

---

## Por qué existe

Un NPS de 42 con 38 respuestas tiene un margen de alrededor de ±20 puntos. Significa que
el valor real está en algún lugar entre 22 y 62, y que el mes que viene puede "subir a
55" sin que haya pasado absolutamente nada.

Ese número se presenta en juntas todo el tiempo, sin intervalo, como si fuera un hecho.
Y encima se usa para decidir cosas.

El problema no es el NPS: es presentarlo desnudo. Esta herramienta lo viste.

## Qué calcula

**Alcance.** Envíos al mes × tasa de respuesta del tipo de encuesta → respuestas
esperadas, con el margen de error del NPS proyectado sobre ese volumen.

| Tipo | Rango típico |
|---|---|
| NPS transaccional | 25-40% |
| NPS relacional | 15-25% |
| General por correo | ~12% |

**Qué puedes afirmar con ese n.** Una lista de cinco afirmaciones que se marcan como
posibles o imposibles según el volumen: leer un NPS global (30+), comparar contra el mes
anterior (100+), abrir en dos segmentos (200+), en cuatro (400+), analizar por
colaborador (800+).

Es la parte que evita la conversación incómoda del mes tres. Si el plan son 200 envíos
al mes, van a llegar entre 50 y 80 respuestas: alcanza para tendencias generales, no
para comparar sucursales. Mejor decirlo en la propuesta.

**El intervalo del NPS.** Con la fórmula correcta, que no es la de una proporción simple:

```
Var(NPS) = [pP + pD − (pP − pD)²] / (n − 1)
IC 95%   = NPS ± 1.96 · √Var · 100
```

Con 55 promotores, 30 pasivos y 15 detractores: NPS +40, ±14.5, intervalo de 26 a 54.

El divisor es `n − 1` y no `n` a propósito: es varianza muestral, la convención de
las referencias publicadas de NPS. Verificado contra la fórmula de Genroe y MeasuringU,
que expresan lo mismo en su forma larga:

```
SE = √[ ((100−NPS)²·P + (0−NPS)²·Pa + (−100−NPS)²·D) / (n(n−1)) ]
```

Ambas dan 7.386 de error estándar para ese caso. Con n grande la diferencia contra
dividir entre `n` es despreciable; en el rango de 30 a 100 respuestas —justo el que
esta herramienta atiende— se nota, y por eso se usa la versión correcta.

## El detalle de honestidad

El selector de "momento de envío" **no aplica un multiplicador inventado**. El dato
verificado es que enviar dentro de las 2 horas posteriores a la interacción obtiene
alrededor de 32% más respuestas completas. Convertir eso en un factor sobre una tasa
base sería inventar precisión que no existe.

Lo que hace es posicionar la estimación dentro del rango publicado: enviar pronto te
ubica en la parte alta, enviar tarde en la baja. La herramienta lo dice con esas
palabras en pantalla.

## El revisor de redacción

Cinco heurísticas sobre los defectos más comunes: lenguaje que induce, pregunta doble,
más de 20 palabras, negación dentro de la pregunta, y falta de signo de interrogación.

Probado con *"¿Qué tan increíble fue nuestra atención y el producto que te entregamos?"*
— detecta las dos fallas. Está etiquetado como heurística, no como validación: cierra
diciendo que la leas en voz alta, porque eso encuentra cosas que ningún regex encuentra.

## La nota legal que va incluida

México tiene una **nueva LFPDPPP** desde el 21 de marzo de 2025. El INAI desapareció y
la definición de "responsable" se amplió a cualquiera que realice tratamiento de datos.
El escudo de "yo solo soy el encargado" ya no protege igual.

Cualquiera que maneje bases de clientes de terceros —encuestas de CX incluidas— tiene
probablemente obligaciones propias. Va en la herramienta porque el momento de enterarse
es antes del primer envío, no después.

## Montarla

```bash
cp index.html "../../sitio 2/my-next-tailwind/public/herramientas/encuesta-nps/index.html"
```

## Notas de mantenimiento

Los rangos de respuesta están en `RANGOS`, las heurísticas de redacción en `REGLAS`.
Lo único que puede caducar es el marco legal del bloque final — revísalo si hay
reglamento nuevo de la LFPDPPP.
