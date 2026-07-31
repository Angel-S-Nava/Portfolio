# Herramientas · navamkt

Ocho calculadoras y diagnósticos de marketing. **Existen en dos formas**, y conviene
tener clara la diferencia:

| | Dónde | Qué es |
|---|---|---|
| **Producción** | `sitio 2/my-next-tailwind` | Componentes React en `/[lang]/tools/[slug]`. Bilingües, con metadata, JSON-LD y sitemap. Es lo que ve un cliente |
| **Portafolio** | esta carpeta | Un HTML autocontenido por herramienta. Sin build ni dependencias, se abre con doble clic. Es lo que va a GitHub |

Las dos versiones comparten la lógica y los umbrales. La de esta carpeta es mejor
pieza de portafolio justamente porque no necesita nada para correr.

**Índice local:** [`index.html`](index.html) · **En el sitio:** `/es/tools`

---

## Las herramientas

| # | Herramienta | Área | En el sitio | Autocontenida |
|---|---|---|---|---|
| 01 | ¿Qué deberías arreglar primero? | Diagnóstico general | `/es/tools/diagnostico-madurez-marketing-digital` | [`08-diagnostico-madurez`](08-diagnostico-madurez/index.html) |
| 02 | ¿Tu presupuesto de pauta alcanza? | Paid Media | `/es/tools/calculadora-presupuesto-minimo-google-meta-ads` | [`02-presupuesto-minimo-ads`](02-presupuesto-minimo-ads/index.html) |
| 03 | Cuánto cuesta la API de WhatsApp | IA Conversacional | `/es/tools/calculadora-costo-whatsapp-business-api` | [`03-costos-whatsapp-api`](03-costos-whatsapp-api/index.html) |
| 04 | ¿Tu sitio puede hacer A/B testing? | CRO | `/es/tools/calculadora-viabilidad-ab-testing` | [`01-viabilidad-ab-testing`](01-viabilidad-ab-testing/index.html) |
| 05 | ¿Te menciona la IA? | SEO + GEO | `/es/tools/medir-menciones-de-marca-en-ia` | [`05-baseline-geo`](05-baseline-geo/index.html) |
| 06 | Diseña una encuesta NPS | CX | `/es/tools/calculadora-nps-encuesta-satisfaccion` | [`06-encuesta-nps`](06-encuesta-nps/index.html) |
| 07 | ¿Por qué tus correos caen en spam? | Outbound | `/es/tools/auditoria-entregabilidad-correo-frio` | [`04-auditoria-entregabilidad`](04-auditoria-entregabilidad/index.html) |
| 08 | Parrilla editorial de un mes | Social Media | `/es/tools/generador-parrilla-contenido-redes` | [`07-parrilla-editorial`](07-parrilla-editorial/index.html) |

> La numeración de la primera columna es el orden editorial del sitio. Los nombres de
> carpeta conservan la numeración original con la que se construyeron — por eso no
> coinciden. El registro que une ambas cosas es `lib/tools-data.ts`.

Cada carpeta tiene su propio README con el porqué de la herramienta, las fórmulas y
las notas de mantenimiento. Ojo: la sección "Montarla" de esos README describe el plan
original de copiarlas a `public/`, que quedó descartado — ver abajo.

## Cómo están hechas

Cinco reglas, en `_marca/sistema-visual.md`. Las tres que importan de verdad:

**El resultado va primero.** Ninguna pide un dato antes de dar el número, y ninguna
manda nada a ningún servidor — todo se calcula en el navegador. Es una decisión
comercial, no una concesión: una herramienta que da el resultado sin pedir nada a
cambio se comparte sola.

**Ningún dato inventado.** Cuando un número depende de una tarifa que cambia —Meta,
WhatsApp, tipo de cambio— es un campo editable con su fecha de referencia, no una
constante escondida en el código. El tarifario de WhatsApp cambió dos veces en doce
meses; cualquier calculadora que dé un costo fijo sin dejar editarlo miente por
omisión.

**Varias venden en contra.** La de A/B testing le dice a la mayoría de los sitios que
no contrate CRO. La de pauta, que con ese presupuesto ninguna agencia va a poder
optimizar. La de GEO incluye que `llms.txt` hoy no sirve para que los modelos te citen,
que es un argumento de venta cómodo del que muchos no querrían prescindir.

Eso es el punto: un prospecto informado verifica esas cosas, y sale más barato que las
lea aquí.

## Por qué NO van en `public/`

Era el plan original y no funciona en este sitio. `proxy.ts` trata cualquier ruta de un
solo segmento que no esté en `KNOWN_PAGES` como enlace de seguimiento:

```
/tools/calculadora     → sin punto → entra al proxy → redirige a /es/tools/…
                         → esa ruta no existiría → 404
/tools/                → un segmento, desconocido → se reescribe a /api/track/tools
/tools/calc.html       → tiene punto → el proxy lo ignora → sirve, con URL fea
                         y fuera del sitemap
```

Por eso están integradas como rutas reales. Eso además habilita metadata con hreflang,
JSON-LD, breadcrumbs y enlazado interno, que un archivo suelto no tiene.

## Lo que se tocó en el sitio

| Archivo | Qué hace |
|---|---|
| `lib/tools-data.ts` | Registro bilingüe: slugs por idioma, FAQs, intros y metadata |
| `app/[lang]/tools/page.tsx` | Índice con `CollectionPage` + `ItemList` |
| `app/[lang]/tools/[slug]/page.tsx` | Página de cada herramienta: `WebApplication` + `FAQPage` + `BreadcrumbList` |
| `components/tools/ToolKit.tsx` | Piezas compartidas, sobre los tokens de `globals.css` |
| `components/tools/registry.ts` | Mapa id → componente. Define qué rutas existen |
| `components/tools/*.tsx` | Las ocho herramientas |
| `app/sitemap.ts` | 18 entradas nuevas con hreflang cruzado |
| `proxy.ts` | `tools` agregado a `KNOWN_PAGES` |
| `components/navbar.tsx` + `i18n/locales/*.json` | Enlace "Herramientas" en el menú |
| `.vercelignore` | Excluye el `.bak` de la guía retirada. **Reemplaza a `.gitignore`, no lo complementa** |

### Agregar una herramienta nueva

1. Un objeto en `toolsData` de `lib/tools-data.ts`
2. Su componente en `components/tools/`
3. Una línea en `REGISTRY`

Índice, sitemap, hreflang y breadcrumbs se actualizan solos.

## Verificación

Lo que se comprobó, por herramienta:

| # | Comprobación |
|---|---|
| 01 | Tabla de muestras reproduce los valores de referencia sobre base del 3%: 53,208 visitas/variante para +10%, 24,190 para +15%, 13,911 para +20%, 6,451 para +30%. En +50% muestra 3,334 en vez de los 2,514 de la fórmula, porque ahí manda el piso de 100 conversiones por variante — es el comportamiento correcto |
| 02 | Presupuesto mínimo con CPA $350 y ventana de 7 días da $76,100/mes para un solo conjunto |
| 03 | Desglose de 800 entrantes + 400 utility + 300 marketing cuadra en USD y MXN |
| 04 | Peor caso 0/100 con los 20 hallazgos; "no tengo escáner" penaliza aunque sea la última opción de su lista |
| 05 | Con 4 celdas corridas: cobertura 7%, mención 75%, cita 25%, brecha 3.0×; los deltas del historial salen correctos |
| 06 | NPS 55/30/15 → +40 con intervalo ±14.5 (de 26 a 54), coincidente con la fórmula publicada de Genroe y MeasuringU |
| 07 | Reparto por pilar converge al peso configurado sobre 200 regeneraciones (24.5 / 38.2 / 24.8 / 12.1 contra 25 / 37.5 / 25 / 12.5) |
| 08 | Dos escenarios de secuencia: con pauta activa y medición en 0, el plan empieza por medición; con base sana y retención en 0, retención **no** aparece primero |

Verificado a nivel de lógica y de DOM ejecutando cada archivo en el navegador.

### De la versión del sitio

Contra el servidor de desarrollo, las 12 rutas probadas responden **200** con su `<h1>`
correcto y JSON-LD presente. `tsc --noEmit` y `next build` en exit 0, con 18 rutas
prerenderizadas. La reactividad se comprobó en la calculadora de pauta: cambiar de Meta
a Google mueve la ventana de 7 a 30 días, y subir el presupuesto a $300,000 voltea el
veredicto a "sales de aprendizaje en 8 días", que es el número correcto.

**Falta la revisión visual.** El panel de vista previa nunca compuso frames, así que
verifiqué estructura y comportamiento, no apariencia. Vale la pena abrir `/es/tools` y
recorrer las ocho — sobre todo la matriz de GEO y el calendario, que son las dos con
tabla ancha en móvil.

## Mantenimiento

Lo que caduca, y cuándo revisarlo:

| Qué | Dónde | Cada |
|---|---|---|
| Tarifas de WhatsApp y tipo de cambio | 03, valores por defecto del HTML | 6 meses |
| Umbral de one-click unsubscribe de Gmail | 04, chequeo 15 | 12 meses |
| Estado de `llms.txt` y qué mueve las citas | 05, bloque de método | 6 meses |
| Marco legal de datos personales | 06, bloque final | si hay reglamento nuevo |
| Fecha "Datos revisados" del pie | los 8 archivos | con cada revisión |

Esa última fila es la importante: si actualizas un dato y dejas la fecha vieja, o al
revés, la herramienta miente. Muévelas juntas.

Los umbrales estadísticos de 01 y los de fase de aprendizaje de 02 no caducan: son
constantes de método y de plataforma, no tarifas.
