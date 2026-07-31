# Baseline GEO: ¿te menciona la IA?

Matriz de registro para medir presencia de marca en ChatGPT, Perplexity, Gemini, Claude
y AI Overviews. Guarda cortes mensuales y muestra el movimiento entre ellos.

**En vivo:** `https://navamkt.com/herramientas/baseline-geo`

---

## Por qué existe

No hay Search Console para modelos de lenguaje. No hay panel, no hay API de posiciones,
no hay export. La única forma de medir es correr las mismas preguntas cada mes y
registrar qué pasó, con capturas fechadas.

Eso convierte al baseline en un problema de disciplina, no de herramientas. Y los
problemas de disciplina se resuelven con un formato que haga fácil lo correcto: la misma
matriz, las mismas preguntas, el mismo día del mes.

## La distinción que casi nadie hace

**Mención no es cita.** Los datos de 2026 apuntan a que ChatGPT menciona marcas del
orden de tres veces más de lo que las cita con liga.

Un cliente puede estar ganando presencia real y no ver un solo clic de referral. Si esa
diferencia no se explica desde el día uno, en el mes tres llega la pregunta por el
tráfico — y es una pregunta justa. Por eso la matriz tiene cuatro estados y no dos:

| Estado | Qué significa |
|---|---|
| · | Sin correr |
| ✕ | No apareces |
| M | Mencionada, sin liga |
| C | Citada con liga |

La herramienta calcula la brecha mención→cita y la compara contra el ~3× típico.

## Qué más hace

- **Tasa por motor**, en barras apiladas de cita sobre mención
- **Share of voice de competidores**: contador manual de quién aparece en tu lugar
- **Historial de cortes** con deltas mes a mes, guardado en el navegador
- **Exportación CSV** para llevarlo a un reporte

Nada se envía a ningún servidor. Todo vive en `localStorage`.

## La parte incómoda que va incluida

La herramienta dice, dentro de su propio contenido, que **ningún motor de IA importante
usa `llms.txt` hoy**. John Mueller lo dijo públicamente en junio de 2025, Google lo
reiteró en su guía de junio de 2026, y un análisis de 137,000 sitios encontró que el 97%
de esos archivos no recibió ni una sola petición en mayo de 2026.

Es un argumento de venta cómodo y renunciar a él cuesta. Va incluido de todas formas,
por dos razones: es verdad, y es mucho más barato decirlo aquí que dejar que un
prospecto informado lo verifique y lo saque en una junta.

Lo que sí correlaciona con ser citado son las **menciones de marca en sitios de
terceros** — correlación reportada del orden de 0.66, contra 0.22 de los backlinks.
Reddit aparece como la fuente más citada de forma transversal y Wikipedia pesa mucho en
ChatGPT. La consecuencia práctica para un plan de trabajo es grande: las horas van a PR
digital, comunidades y consistencia de entidad, no a tocar archivos del sitio.

## El protocolo

1. De 15 a 20 preguntas reales de compra, no keywords
2. Las mismas cinco superficies cada vez
3. Sesión limpia, sin historial ni personalización
4. Captura fechada de cada respuesta
5. El mismo set cada mes — cambiar las preguntas destruye la comparabilidad

Vienen 12 plantillas cargadas con huecos para marca, categoría y ciudad. Se editan en
línea y se agregan las que falten.

## Verificado

Con 4 celdas corridas (1 cita, 2 menciones, 1 ausencia): cobertura 7%, mención 75%,
cita 25%, brecha 3.0×. Dos cortes consecutivos muestran los deltas correctos.

## Montarla

```bash
cp index.html "../../sitio 2/my-next-tailwind/public/herramientas/baseline-geo/index.html"
```

## Notas de mantenimiento

`MOTORES` al inicio del script define las columnas — si aparece una superficie nueva, se
agrega ahí y la matriz se ajusta sola. Las plantillas de preguntas están en
`PLANTILLAS`.

Si un motor empieza a publicar datos de citación propios, este enfoque manual deja de
ser necesario para ese motor. Vale la pena revisarlo cada seis meses.
