# ¿Tu sitio puede hacer A/B testing?

Calculadora de tamaño de muestra y duración para tests A/B. Metes tráfico y tasa de
conversión, y te dice cuántas semanas tardaría el test — o que no se puede hacer.

**En vivo:** `https://navamkt.com/herramientas/viabilidad-ab-testing`

---

## Por qué existe

CRO se vende como si cualquier sitio pudiera hacerlo. No es cierto, y el cálculo que
lo demuestra cabe en una servilleta.

Un sitio con 100 conversiones al mes necesita cerca de cuatro meses para detectar una
mejora del 30%, y más de ocho para una del 20%. Los dos números se pasan del máximo de
6-8 semanas que aguanta un test antes de que la estacionalidad y la pérdida de cookies
ensucien el resultado. Ese sitio no puede hacer A/B testing. Puede hacer otras cosas
—y varias son más rentables— pero no testing.

Vender lo contrario produce un cliente decepcionado en el mes dos. Esta herramienta
pone el número enfrente antes de que nadie firme nada.

## Qué calcula

- Visitas y conversiones necesarias **por variante**
- Duración en semanas contra el techo de 8
- Tabla de sensibilidad: qué mejoras sí caben en 8 semanas con ese tráfico
- Plan alterno cuando el veredicto es rojo

Dos topes que casi ninguna calculadora pública aplica y que aquí sí están:

| Tope | Valor | Por qué |
|---|---|---|
| Piso de conversiones | 100 por variante | Debajo de eso, un ganador es ruido aunque la muestra "alcance" |
| Techo de duración | 8 semanas | Más allá, el resultado mezcla estacionalidad y cookies perdidas |

Cuando el piso de conversiones manda sobre la fórmula, la herramienta lo dice en
lugar de esconderlo.

## El cálculo

Prueba de dos proporciones a dos colas:

```
n = (Zα/2 + Zβ)² · [p₁(1−p₁) + p₂(1−p₂)] / (p₂ − p₁)²
```

Con `p₁` = 3%, α = 0.05 bilateral y potencia 80%, la fórmula devuelve 53,208 visitas por
variante para una mejora del 10% y 2,514 para una del 50%. Son los mismos números que
sacan las calculadoras de Evan Miller, Optimizely y VWO.

Pero la herramienta muestra **3,334** en el caso del 50%, no 2,514: ahí manda el piso de
conversiones (100 ÷ 0.03). Es el comportamiento correcto y la razón por la que existe el
piso — con 2,514 visitas por variante juntarías apenas 75 conversiones, y un ganador
leído sobre 75 conversiones es ruido aunque la fórmula diga que la muestra alcanzó.
Cuando el piso manda, la herramienta lo dice en pantalla en lugar de esconderlo.

**Lo que no hace, y está escrito dentro de la herramienta:** no corrige por
comparaciones múltiples, así que con 3 o 4 variantes la tasa real de falsos positivos
queda por encima del α elegido. Tampoco cubre tests secuenciales ni métodos bayesianos.

## Montarla

Un solo archivo, sin dependencias ni build.

```bash
cp index.html "../../sitio 2/my-next-tailwind/public/herramientas/viabilidad-ab-testing/index.html"
```

Next.js sirve `public/` tal cual, así que queda disponible en
`/herramientas/viabilidad-ab-testing/` sin tocar el router. Para verla en local basta
con abrir el archivo en el navegador.

Las fuentes vienen de Google Fonts. Sin conexión se ve peor y funciona igual.

## Notas de mantenimiento

Nada aquí caduca: son constantes estadísticas, no tarifas de plataforma. Lo único
discutible es el techo de 8 semanas, que es criterio de industria y no una ley. Si
algún día lo cambias, está en `TECHO` al inicio del script.
