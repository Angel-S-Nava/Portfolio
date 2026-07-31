# ¿Por qué tus correos en frío caen en spam?

Auditoría de 20 puntos sobre infraestructura, lista, envío y contenido. Devuelve un
puntaje y una lista de hallazgos **ordenada por impacto**, no por orden de aparición.

**En vivo:** `https://navamkt.com/herramientas/auditoria-entregabilidad`

---

## Por qué existe

Esta es la única herramienta del conjunto que sale de haberme equivocado yo.

Hicimos el diagnóstico completo sobre 814 correos propios. El resultado: 0.25% de
respuesta, entre 13 y 34 veces por debajo del promedio de mercado. La conclusión
intuitiva era "el copy está mal". Era falsa.

El test de colocación mandó tres correos reales a Gmail. Los tres cayeron en spam,
incluido un control sin `List-Unsubscribe`. SPF, DKIM y DMARC pasaban. Ninguna de las 24
IPs de salida aparecía en seis listas negras. Mail-tester le dio **10/10** al mismo
correo que Gmail mandaba a spam.

Con 100% de colocación en spam, esa tasa de respuesta no medía la calidad de la
plantilla. Medía cuánta gente revisa su carpeta de spam.

El otro hallazgo, el que más me costó: el escáner de rebotes leía solo `INBOX` y
reportaba **0.00% estructural**. El buzón real tenía 1 mensaje en INBOX y 41 en la
papelera — todo se leía y borraba desde el móvil antes de que el script pasara. Al
arreglarlo aparecieron 14 rebotes: 3.43%, por encima del umbral en el que la
recomendación estándar es dejar de enviar. Se habían quemado 44 envíos en 17
direcciones inexistentes.

Esa pregunta está en la auditoría (chequeo 16) porque a mí me costó meses encontrarla.

## Cómo puntúa

Veinte chequeos con peso propio, sumando 127 puntos. El puntaje es porcentaje sobre lo
respondido, así que da retroalimentación desde la primera respuesta sin fingir que
evaluó lo que aún no contestas.

| Peso | Chequeos |
|---|---|
| 12 | Dominio de envío separado del de marca |
| 10 | Proveedor de salida · calentamiento de 4-6 semanas |
| 8 | Verificación de lista · tasa de rebote · personalización real |
| 7 | Supresión de rebotes duros |
| 6 | Direcciones de rol · volumen diario · carpetas que lee el escáner |
| 5 | SPF · DKIM · DMARC · dedupe · tope de por vida · palabras gatillo |
| 4 | Postmaster Tools · List-Unsubscribe · longitud · links |

Bandas: **85+** infraestructura sólida · **65-84** con fugas · **40-64** en riesgo ·
**menos de 40** vas a spam.

Los hallazgos se ordenan por puntos perdidos, que es lo mismo que ordenarlos por
impacto. Si la primera línea dice "sales desde tu dominio principal", ninguna de las
otras diecinueve importa hasta que eso se resuelva.

## Verificado

Peor caso: 0/100 con los 20 hallazgos. Opción "No tengo escáner de rebotes": penaliza
correctamente aunque sea la última de su lista.

## Montarla

```bash
cp index.html "../../sitio 2/my-next-tailwind/public/herramientas/auditoria-entregabilidad/index.html"
```

El botón "Copiar diagnóstico" pone el resultado en el portapapeles como texto plano,
listo para pegar en un correo. Es la ruta natural para que alguien te lo mande.

## Notas de mantenimiento

Todo el contenido vive en el array `AUDIT` al inicio del script: agregar un chequeo es
agregar un objeto con su peso y el texto del hallazgo. El resto —puntaje, orden,
severidades, exportación— se recalcula solo.

Lo único que caduca es el umbral de one-click unsubscribe de Gmail (hoy, 5,000
correos diarios). Está en el texto del chequeo 15.
