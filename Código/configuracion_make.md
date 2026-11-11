# Configuración del escenario en Make: `Encuesta_Equipo#`

Flujo: **Página web → Webhook → Router → Ruta 1 (guardar en Sheets) / Ruta 2 (reporte con IA)**

## Hoja de Google Sheets

- Archivo: `Encuesta_Equipo#`
- Pestaña: `Respuestas`
- Encabezados en la fila 1: `Fecha | Comida | Ropa | Apps | Criterio | Origen | Edad`

## Módulos

| # | Módulo | Configuración |
|---|--------|---------------|
| 1 | Webhooks → Custom webhook | Crear uno nuevo, copiar la URL y pegarla en `WEBHOOK_URL` de `index.html`. Con *Run once* enviar una respuesta de prueba para que detecte los 7 campos (`accion`, `comida`, `ropa`, `apps`, `criterio`, `origen`, `edad`). |
| 2 | Flow Control → Router | Dos rutas. |

### Ruta 1: guardar cada respuesta

| Módulo | Configuración |
|--------|---------------|
| Google Sheets → Add a Row | Archivo `Encuesta_Equipo#`, pestaña `Respuestas`. Fecha = `{{formatDate(now; "DD/MM/YYYY HH:mm")}}`; Comida = `comida`, Ropa = `ropa`, Apps = `apps`, Criterio = `criterio`, Origen = `origen`, Edad = `edad`. |
| Webhooks → Webhook Response | Status `200`. Body: `Respuesta registrada. Gracias por participar.` Headers: `Content-Type` = `text/plain; charset=utf-8` y `Access-Control-Allow-Origin` = `*`. |
| Filtro (llave inglesa de la ruta) | Configurarlo **después** de agregar los módulos: `accion` *Equal to* `respuesta`. |

### Ruta 2: generar el reporte con IA

| Módulo | Configuración |
|--------|---------------|
| Google Sheets → Search Rows | Misma hoja y pestaña. Maximum number of returned rows: `200`. |
| Tools → Text aggregator | Source Module: Search Rows. Text: `{{Comida}} \| {{Ropa}} \| {{Apps}} \| {{Criterio}} \| {{Origen}} \| {{Edad}}` (mapear cada columna desde el panel). |
| Make AI Agent | Connection: Make's AI Provider. Input: `Respuestas de la encuesta (comida \| ropa \| apps \| criterio \| origen \| edad):` seguido del texto del agregador. Instructions: ver abajo. |
| Webhooks → Webhook Response | Status `200`. Body = respuesta del AI Agent. Mismos dos headers de la ruta 1. |
| Filtro de la ruta | `accion` *Equal to* `reporte`. |

Guardar y activar el escenario con **Immediately as data arrives**.

## Instructions del Make AI Agent

```
Eres un analista de economia local para alumnos de Desarrollo Sustentable del TecNM en Mazatlan, Sinaloa.
Recibiras las respuestas de una encuesta, una por linea, con el formato: comida | ropa | apps | criterio | origen | edad.
Usa UNICAMENTE esas respuestas; no inventes datos.
Responde en texto plano (sin asteriscos, sin markdown), en espanol, con este formato:

TOTAL DE RESPUESTAS: [numero]

RESULTADOS
Comida: [cada opcion con su porcentaje]
Ropa: [...]
Apps internacionales: [...]
Criterio de compra: [...]
Conoce el origen: [...]

ANALISIS
[4 lineas maximo: que tan local o global es el consumo de esta comunidad y que diferencias hay por edad]

CONCLUSIONES
1. [efecto en la economia local]
2. [efecto ambiental por transporte y empaques]
3. [una accion concreta para impulsar el consumo local]
```

## Fórmulas para verificar a la IA (en Sheets)

Poner en otra pestaña o en celdas libres:

```
=COUNTIF(Respuestas!B:B, "Mercado o tianguis") / COUNTA(Respuestas!B2:B)
=COUNTIF(Respuestas!B:B, "Tienda de barrio") / COUNTA(Respuestas!B2:B)
=COUNTIF(Respuestas!B:B, "Supermercado") / COUNTA(Respuestas!B2:B)
=COUNTIF(Respuestas!B:B, "En línea") / COUNTA(Respuestas!B2:B)

=COUNTIF(Respuestas!D:D, "Nunca") / COUNTA(Respuestas!D2:D)
=COUNTIF(Respuestas!D:D, "Una vez al mes") / COUNTA(Respuestas!D2:D)
=COUNTIF(Respuestas!D:D, "Varias veces al mes") / COUNTA(Respuestas!D2:D)
=COUNTIF(Respuestas!D:D, "Cada semana") / COUNTA(Respuestas!D2:D)
```

Dar formato de porcentaje a las celdas y comparar con lo que dio la IA.
