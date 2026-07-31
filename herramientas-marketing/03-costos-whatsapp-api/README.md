# Cuánto cuesta de verdad la API de WhatsApp

Estimador de costos variables de WhatsApp Business API, desglosado por categoría de
mensaje. Con las tarifas editables, porque cambian cada trimestre.

**En vivo:** `https://navamkt.com/herramientas/costos-whatsapp-api`

---

## Por qué existe

WhatsApp dejó de cobrar por conversación en julio de 2025. Ahora cobra **por mensaje de
plantilla entregado**, y el precio depende de la categoría. Casi nadie que cotiza un
chatbot sabe esto, y el resultado son dos errores opuestos:

- Cotizar de más, porque se asume que cada conversación cuesta.
- Cotizar de menos, porque se ignora que las campañas de difusión sí se cobran caro.

La distinción que importa: **un bot que responde a quien escribe primero opera casi todo
dentro de la ventana de servicio de 24 horas, que es gratis.** El costo aparece cuando el
negocio inicia la conversación. Esa sola frase cambia la cotización de un proyecto.

## Las cuatro categorías

| Categoría | Costo | Dónde aparece |
|---|---|---|
| Servicio | Gratis | Todo lo que respondes dentro de las 24 h que abre el cliente |
| Utility | ~10-20% del precio de marketing, con descuento por volumen | Confirmaciones, avisos de envío, recordatorios |
| Marketing | El caro, sin descuentos por volumen | Promociones y difusión |
| Click-to-WhatsApp | Gratis las primeras 72 h | Conversaciones nacidas de un anuncio |

La última es la palanca de costo más grande disponible para un negocio que ya invierte
en pauta, y prácticamente nadie la usa a propósito.

## La decisión de diseño que importa

**Las tarifas son campos editables, no constantes en el código.**

Meta cambió su tarifario dos veces en doce meses y la última actualización entró en
vigor el 1 de julio de 2026. Las fuentes públicas reportan entre USD $0.0305 y $0.0436
por mensaje de marketing en México según la fecha del rate card que consultes, y encima
un BSP suma entre $0.003 y $0.010.

Cualquier número que se hornee en el código va a estar viejo en un trimestre. La
herramienta carga valores de partida, dice de cuándo son, y pide explícitamente que se
verifiquen contra el tarifario vivo de Meta. Es lo contrario de lo que hace casi
cualquier calculadora de agencia, y es justo lo que la vuelve usable el año que viene.

## Qué más incluye

Requisitos previos al trámite (2FA obligatorio, nombre aprobado, documentación idéntica
al registro legal), tiempos reales de verificación (2-5 días hábiles si todo coincide,
hasta 14 si no), y la nota sobre **Coexistence** — Meta ya permite conservar el número
que el negocio venía usando en la app de WhatsApp Business. Ese dato solo evita muchas
llamadas incómodas pidiendo una línea nueva.

## Montarla

```bash
cp index.html "../../sitio 2/my-next-tailwind/public/herramientas/costos-whatsapp-api/index.html"
```

## Notas de mantenimiento

Los `value` por defecto de `tMkt`, `tUtil`, `tBsp` y `tc` en el HTML son de julio de
2026. Actualízalos cada seis meses y mueve la fecha del pie y del bloque de advertencia
en el mismo commit — si una de las dos cosas se queda atrás, la herramienta miente.
