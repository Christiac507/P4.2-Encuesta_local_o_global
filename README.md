# Práctica 4.2 – Encuesta "¿Compras local o global?"

**Instituto Tecnológico de Mazatlán** · Ingeniería en Sistemas Computacionales
**Asignatura:** Desarrollo Sustentable (ACD-0908) · **Unidad 4:** Escenario económico
**Tema:** 4.2 Economía global vs economía local y PIB
**Alumno:** Christian Paul Lizárraga Oronia
**Profesor:** Miguel Ángel Barrón Hernández

---

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
| `Código/` | `index.html` (la encuesta), `Encuesta_Equipo#.blueprint.json` (blueprint exportado de Make) y `configuracion_make.md` (módulos, filtros e instrucciones de la IA) |
| `Imágenes/` | Capturas del escenario de Make, la hoja de Sheets, la página y el reporte |
| `Video/` | Enlace al video de la práctica |
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

**Resumen de resultados (20 respuestas):** comida en supermercado 50 %, tienda de barrio 30 %, mercado o tianguis 20 %; ropa en negocio local 45 %, tienda departamental 25 %, segunda mano 20 %, app internacional 10 %; compras en apps internacionales: nunca 45 %, una vez al mes 30 %, varias veces al mes 25 %. Al verificar con `COUNTIF`, la IA acertó en comida, ropa, criterio y origen, pero se equivocó en la pregunta de apps internacionales.

## Preguntas de reflexión

**1. ¿El consumo de su comunidad es más local o más global? ¿En qué productos se nota más?**

Según la encuesta, el 50% compra su comida en mercado, tianguis o tienda de barrio y el otro 50% en supermercado; nadie la compra en línea. En general, la comida sigue siendo el producto más local: en Mazatlán es común comprar mariscos, frutas y verduras en el mercado o con vendedores de la colonia, porque son frescos y están cerca. La ropa es donde el consumo se vuelve más global, ya que muchas personas, sobre todo jóvenes, compran en tiendas departamentales de cadenas internacionales o en apps como Shein y Temu por sus precios bajos. Con nuestros datos esto fue menor de lo esperado: solo el 10% compra ropa en una app internacional, mientras que el 45% la compra en negocio local y el 20% de segunda mano. Donde sí se nota lo global es en la frecuencia: el 55% compra en apps internacionales al menos una vez al mes. Además, el 50% no sabe de dónde viene lo que compra y para el 45% el precio es lo que más pesa, lo que favorece a las cadenas y plataformas que venden más barato. Por eso concluimos que el consumo de la comunidad es mixto: la comida se reparte entre lo local y los supermercados, la ropa es mayormente local y lo global aparece sobre todo en las compras frecuentes por apps.

**2. ¿Qué efecto tiene en el PIB y en el empleo de Mazatlán que las personas compren en apps internacionales?**

Cuando una persona compra en una app internacional, el producto se fabricó en otro país, así que esa producción suma al PIB de ese país y en México se registra como una importación. Del dinero gastado, solo una parte pequeña se queda aquí (la entrega de la paquetería y algunos impuestos). En cambio, una compra en un negocio local paga el sueldo del vendedor, la renta del local y a proveedores de la región, y ese dinero se vuelve a gastar en Mazatlán. Si muchas personas cambian sus compras de ropa, calzado o electrónicos a plataformas extranjeras, los comercios del centro y de las plazas venden menos, contratan a menos personas o cierran. A largo plazo esto reduce el empleo formal en el comercio, que es uno de los sectores que más trabajo da en la ciudad junto con el turismo.

**3. ¿Qué impacto ambiental tiene el transporte y el empaque de lo que se compra en línea desde otro país?**

Un producto comprado en línea desde Asia recorre miles de kilómetros: primero viaja de la fábrica al almacén, luego en avión o barco hasta México y al final en camionetas de paquetería hasta la casa. Cada etapa quema combustibles fósiles y genera emisiones de CO₂. Los envíos por avión, que son los más rápidos, son también los que más contaminan por kilogramo transportado. Además, cada pedido llega en bolsas de plástico, cajas y rellenos que casi nunca se reciclan y terminan en el basurón o en el mar. Como muchas compras son de productos baratos y de poca duración, se repite el ciclo y se acumula más basura. Una compra local recorre distancias cortas y muchas veces no necesita empaque.

**4. ¿Coincidieron los porcentajes de la IA con los de Sheets? ¿Qué aprendieron sobre verificar a la IA?**

Coincidieron en parte. En comida (Supermercado 50%, Tienda de barrio 30%, Mercado o tianguis 20%), ropa, criterio de compra y origen, los porcentajes de la IA fueron iguales a los de COUNTIF. Pero en la pregunta de apps internacionales la IA falló: escribió “App internacional 20.0%; No aplica”, mezclando una opción de la pregunta de ropa, cuando Sheets muestra Nunca 45%, Una vez al mes 30%, Varias veces al mes 25% y Cada semana 0%. Tampoco calculó los porcentajes de edad y su análisis tiene errores de escritura (“comería”, “tiaanguis”). Las IA generan texto prediciendo palabras, no hacen conteos exactos como una hoja de cálculo, así que pueden equivocarse al contar, redondear de forma rara o hacer que los porcentajes no sumen 100%. Por eso es importante revisar sus resultados con una herramienta confiable, como las fórmulas COUNTIF y COUNTA. Aprendimos que la IA es útil para redactar el análisis y las conclusiones de forma rápida, pero que los números se deben comprobar antes de usarlos en un informe o en una decisión.

**5. ¿Qué acción concreta propondrían para impulsar el consumo local en su colonia?**

Proponemos organizar un “Mercadito de la colonia” una vez al mes, en una cancha o parque, donde los vecinos que hacen comida, ropa, artesanías o productos de limpieza puedan vender sin pagar renta. Para difundirlo usaríamos un grupo de WhatsApp o una página de Facebook de la colonia, con un catálogo de negocios locales y sus números de contacto, para que la gente sepa qué puede comprar cerca antes de pedirlo en una app. También pediríamos a los vendedores que acepten pago con transferencia y que eviten bolsas de plástico. Así el dinero se queda en la comunidad, se reducen envíos y empaques, y los pequeños negocios ganan clientes.
