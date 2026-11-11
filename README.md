# Práctica 4.2 – Encuesta "¿Compras local o global?"

**Instituto Tecnológico de Mazatlán** · Ingeniería en Sistemas Computacionales
**Asignatura:** Desarrollo Sustentable (ACD-0908) · **Unidad 4:** Escenario económico
**Tema:** 4.2 Economía global vs economía local y PIB
**Alumno:** Christian Paul Lizárraga Oronia
**Profesor:** Miguel Ángel Barrón Hernández

---

## 🎥 Video

[▶ Ver el video de la práctica en YouTube](https://www.youtube.com/watch?v=PEGA_AQUI_EL_ID_DEL_VIDEO)

## 🌐 Página publicada

[Abrir la encuesta en GitHub Pages](https://christiac507.github.io/P4.2-Encuesta_local_o_global/C%C3%B3digo/)

---

## Objetivo

Identificar los hábitos de compra local y global de la comunidad, relacionarlos con la economía regional y el PIB, y construir un sistema de encuesta con análisis automático cuyos resultados se puedan verificar.

## ¿Cómo funciona?

```
Página web (index.html)
   │  POST con URLSearchParams
   ▼
Webhook de Make ── Router
   ├── Ruta 1 (accion = respuesta) → Google Sheets: Add a Row → Webhook Response
   └── Ruta 2 (accion = reporte)   → Google Sheets: Search Rows → Text aggregator
                                     → Make AI Agent → Webhook Response (reporte)
```

1. La persona contesta 6 preguntas anónimas y presiona **Enviar respuesta**.
2. Make guarda la respuesta en la hoja `Encuesta_Equipo#`, pestaña `Respuestas`.
3. El botón **Generar reporte** junta todas las respuestas y el Make AI Agent devuelve porcentajes, análisis y conclusiones.
4. Los porcentajes de la IA se verifican en Sheets con `COUNTIF`.

## Tecnologías

- HTML, CSS y JavaScript (un solo archivo, sin librerías externas)
- Make: Webhooks, Router, Google Sheets, Text aggregator, Make AI Agent, Webhook Response
- Google Sheets
- GitHub Pages

## Estructura del repositorio

| Carpeta | Contenido |
|---------|-----------|
| `Código/` | `index.html` (la encuesta) y `configuracion_make.md` (módulos, filtros e instrucciones de la IA) |
| `Imágenes/` | Capturas del escenario de Make, la hoja de Sheets, la página y el reporte |
| `Video/` | Video de la práctica (enlace arriba) |
| `Resultados/` | Informe en PDF con investigación, resultados y preguntas |

## Preguntas de la encuesta

| Campo | Pregunta |
|-------|----------|
| comida | ¿Dónde compras la mayor parte de tu comida? |
| ropa | ¿Dónde compras tu ropa? |
| apps | ¿Con qué frecuencia compras en apps internacionales? |
| criterio | ¿Qué pesa más al comprar? |
| origen | ¿Sabes de dónde viene lo que compras? |
| edad | Rango de edad |

## Resultados

La encuesta se aplicó a 20 personas de la comunidad. El reporte de la IA y la comparación con las fórmulas de Sheets están en [`Resultados/`](Resultados/).
