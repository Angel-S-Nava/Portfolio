# Una parrilla editorial de un mes en cinco minutos

Generador de calendario editorial. Defines pilares con peso, formatos y días de
publicación; sale un mes completo con formato y ángulo asignados por espacio.

**En vivo:** `https://navamkt.com/herramientas/parrilla-editorial`

---

## Por qué existe

Publicar sin pilares definidos produce un feed que no acumula nada: cada post empieza de
cero y la audiencia nunca llega a asociarte con un tema. Tres a cinco pilares es el rango
donde el feed empieza a construir una idea reconocible — la herramienta avisa cuando te
pasas de cinco.

El otro problema que resuelve es el desequilibrio, que solo se nota cuando el mes ya
pasó: cuatro posts de producto seguidos, o el pilar educativo abandonado desde la segunda
semana.

## Qué genera

Cada espacio del calendario trae tres cosas: **pilar**, **formato** y **ángulo**.

El ángulo es lo que evita que los cinco posts del pilar "servicios" sean el mismo post
cinco veces. Rota entre diez enfoques — cómo se hace, error común, antes y después,
pregunta frecuente, detrás de cámaras, resultado de cliente, mito vs realidad,
comparativa, consejo rápido, historia del negocio.

Exporta a CSV con columnas de gancho y estado, listo para trabajarse en una hoja
compartida con el cliente.

## El detalle técnico que importa

Los pilares tienen peso de 1 a 3. Un pilar en 3 debe aparecer el triple que uno en 1.

La primera versión repartía desde una bolsa barajada una sola vez y recorrida en ciclo.
Con 13 espacios y una bolsa de 8, el sobrante caía siempre sobre las mismas posiciones y
el reparto se desviaba del peso configurado — 46% observado donde tocaba 37.5%.

Ahora la bolsa se rebaraja en cada vuelta. Verificado sobre 200 regeneraciones:

| Pilar | Peso | Esperado | Promedio real |
|---|---|---|---|
| Servicio o producto | 2 | 25% | 24.5% |
| Educativo del sector | 3 | 37.5% | 38.2% |
| Prueba social | 2 | 25% | 24.8% |
| Detrás de cámaras | 1 | 12.5% | 12.1% |

En un mes suelto siempre habrá desviación por el sobrante — son 13 espacios, no 1,300.
Lo que se arregló es que la desviación ya no favorece sistemáticamente al mismo pilar.

El generador usa un PRNG con semilla (mulberry32), así que "Regenerar" da un reparto
distinto pero reproducible.

## Lo que no hace, a propósito

No escribe los copies ni inventa los ganchos. Un calendario lleno de texto generado se
nota, y en redes eso cuesta más caro que publicar menos.

Lo que resuelve es la página en blanco de "¿de qué publico este mes?" y el desequilibrio
invisible. El gancho lo pone quien conoce el negocio.

## Lo que va incluido y no es la herramienta

Tres acuerdos que hay que cerrar antes de publicar nada, y que casi nunca se ponen por
escrito:

1. **Quién responde los mensajes**, en qué horario y qué pasa fuera de él. Es la fuente
   de conflicto número uno en social media.
2. **Aprobación por lotes quincenales**, no post por post. Aprobar uno por uno consume
   más horas que producirlos.
3. **Quién genera el material crudo.** Sin esa tarea asignada, la parrilla se llena de
   gráficos genéricos en la segunda semana.

## Montarla

```bash
cp index.html "../../sitio 2/my-next-tailwind/public/herramientas/parrilla-editorial/index.html"
```

## Notas de mantenimiento

`ANGULOS` y `FORMATOS_BASE` al inicio del script. Si aparece un formato nuevo relevante,
se agrega a la lista y los toggles se ajustan solos.
