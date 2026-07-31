# ¿Tu presupuesto de pauta alcanza?

Calculadora de presupuesto mínimo para Meta y Google Ads. Dice si tu inversión da
para que las campañas salgan de fase de aprendizaje — y cuántos conjuntos de anuncios
sostiene de verdad.

**En vivo:** `https://navamkt.com/herramientas/presupuesto-minimo-ads`

---

## Por qué existe

Meta pide alrededor de 50 eventos de optimización por conjunto de anuncios en una
ventana móvil de 7 días. Debajo de eso el conjunto entra en *Learning Limited* y la
plataforma reduce la entrega. Google Smart Bidding pide del orden de 50 conversiones o
3 ciclos de conversión.

Son números públicos y llevan años ahí. Aun así, el error más caro en pauta para pymes
sigue siendo el mismo: repartir un presupuesto chico entre seis campañas, ninguna llega
al umbral, y a los tres meses se concluye que "la publicidad no funciona".

El caso que esta herramienta hace visible: **CPA de $500 y presupuesto de $10,000 son 20
conversiones al mes.** Ese cliente va a fracasar con cualquier agencia. Conviene decirlo
antes de firmar, no en el mes tres.

## Qué calcula

- Conversiones al mes que compra tu presupuesto
- Conversiones por conjunto dentro de la ventana de la plataforma
- **Cuántos conjuntos sostiene el presupuesto** — el número accionable
- Presupuesto mínimo para la configuración actual, y el CPA al que sí convergería
- Tabla de repartos alternos con el mismo dinero

Si no conoces tu CPA, lo deriva de CPC y tasa de conversión de la landing.

## El cálculo

```
conv/mes   = presupuesto ÷ CPA
conv/día   = conv/mes ÷ 30.44
por unidad = conv/día × ventana ÷ unidades

Meta   → ventana de 7 días
Google → ventana de 30 días
```

Presupuesto mínimo es la operación al revés: `50 × CPA × unidades` por ventana.

## Lo que la herramienta también enseña

Incluye la lista de lo que reinicia la fase de aprendizaje: cambios de presupuesto
mayores al 20%, creativo nuevo, cambio del evento de optimización, movimientos grandes
de audiencia, pausar y reactivar, y mover el tCPA o tROAS más de 15-20%.

Sirve para una conversación difícil que se repite en todos los onboardings: explicar
que *no tocar nada durante una semana* es trabajo, no abandono. Mejor que lo lea en una
herramienta antes del kickoff.

## Montarla

```bash
cp index.html "../../sitio 2/my-next-tailwind/public/herramientas/presupuesto-minimo-ads/index.html"
```

Un archivo, sin dependencias.

## Notas de mantenimiento

El umbral de 50 está en la constante `UMBRAL`. Es estable en Meta desde hace años;
en Google varía según la estrategia de puja y la herramienta lo advierte en el bloque
de método. Si Meta cambia la ventana de 7 días, se toca en `ventana()`.
