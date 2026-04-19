# Cuentitas — Especificaciones del Proyecto

---

## Qué es Cuentitas

Cuentitas es una funcionalidad dentro de **Deuna Negocios** que convierte los datos de transacciones de un comercio en información clara, visual y accionable para el dueño del negocio. No requiere formación financiera ni conocimiento tecnológico avanzado para usarse.

La propuesta tiene dos capas:

**Capa 1 — Dashboard proactivo:** muestra automáticamente los datos más importantes del negocio cada vez que el dueño abre la app, sin que tenga que buscar ni preguntar nada.

**Capa 2 — Asistente conversacional:** disponible cuando el dueño quiere profundizar en algo específico que no está cubierto por el dashboard.

---

## El problema que resuelve

Los dueños de micronegocios que usan Deuna tienen toda la información de su negocio en la app, pero no la pueden leer. El historial de transacciones muestra montos, cuentas de origen y fechas — datos crudos que no dicen nada por sí solos a alguien sin formación contable.

Como resultado, el dueño toma decisiones por intuición (conta la caja a mano, recuerda a sus clientes mentalmente, no sabe cuál es su hora más activa). Cuentitas reemplaza ese esfuerzo manual con información automática, clara y en el idioma del comerciante.

---

## Usuario objetivo

Dueños de micronegocios ecuatorianos que usan Deuna Negocios como medio de cobro. Perfil: adultos con uso básico de tecnología, sin formación financiera, con preguntas recurrentes sobre ventas, clientes y desempeño de su negocio.

---

## Los 3 negocios del dataset (casos de uso)

El proyecto opera sobre un dataset sintético de 3 comercios con 12 meses de historia transaccional (abril 2025 — marzo 2026):

**Tienda de Carmita (NEG001)**  
Negocio estable y consolidado. Clientes muy fieles. Pico claro al mediodía. Tiene 2 vendedores registrados. Representa el caso base del comercio ecuatoriano típico.

**Cafetería Don Roberto (NEG002)**  
Negocio en crecimiento sostenido. Crece mes a mes desde que arrancó. Pico en la mañana (7–9am). Trabaja solo, sin vendedores. Representa el negocio que está escalando.

**Bazar de Lucía (NEG003)**  
Negocio con caída progresiva. Muy dependiente de fines de semana. Ha ido perdiendo clientes en los últimos meses. Tres vendedores pero uno domina las ventas. Representa el caso donde Cuentitas puede generar una alerta de valor real.

---

## Capa 1 — Dashboard "Mis Cuentitas"

### Qué ve el dueño al abrir la app

Lo primero que aparece es una **alerta proactiva** en el header de la pantalla. Sin que el dueño pregunte nada, Cuentitas le dice algo relevante de su negocio. Ejemplo: *"Ayer fue tu mejor martes del mes. Entraron $127 — pico a las 12pm"*.

### Los 4 módulos del dashboard

**1. Resumen del día**
- Cuánto dinero entró hoy en total
- Cuántos cobros se hicieron
- Comparación con el día anterior en lenguaje natural ("$12 más que ayer")
- Gráfica de barras de los últimos 7 días, con el día de hoy resaltado

**2. Hora pico**
- En qué franja horaria se concentran más ventas
- Cuántos cobros se hicieron en esa franja
- Gráfica de barras horizontales por franja horaria, con el pico resaltado

**3. Ranking de clientes del mes**
- Top 3 clientes por monto total pagado en el mes
- Nombre, número de visitas y total en dólares por cada uno
- Formato de lista rankeada (como un marcador deportivo)

**4. Ranking de vendedores del mes**
- Top 3 vendedores por ventas generadas en el mes
- Solo aparece si el negocio tiene 2 o más vendedores registrados en Deuna Negocios
- Mismo formato que el ranking de clientes

### Botón "Pregúntame algo"
Al final del scroll, un botón que abre el asistente conversacional para cuando el dueño quiere saber algo específico que no está en las tarjetas.

---

## Capa 2 — Asistente conversacional

El asistente entra en juego cuando el dashboard no alcanza. Está diseñado para responder preguntas específicas del dueño sobre su negocio, en español natural y en menos de 5 segundos.

### Cuándo se usa el asistente (no el dashboard)

El dashboard responde preguntas universales — datos que cualquier comerciante necesita ver. El asistente responde preguntas personales — cuando el dueño tiene curiosidad sobre algo concreto que varía según el momento.

Casos de uso claros para el asistente:
- Detalles de un cliente específico ("¿cuánto me compraba Luis normalmente?")
- Explicación de una anomalía que el dueño ve en el dashboard ("¿por qué bajé tanto esta semana?")
- Preguntas sobre períodos muy específicos ("¿cómo me fue el fin de semana del feriado?")

### Tipos de preguntas que el asistente debe responder

El asistente debe soportar al menos estos 10 tipos de consulta:

1. ¿Cuánto vendí hoy / esta semana / este mes?
2. ¿Cómo me fue esta semana comparado con la anterior?
3. ¿Cuál fue mi mejor día de la semana?
4. ¿A qué hora vendo más?
5. ¿Quiénes son mis mejores clientes?
6. ¿Quién no ha vuelto en los últimos días?
7. ¿Cuánto ha gastado [nombre de cliente] este mes?
8. ¿Cuál es la tendencia de mis ventas este mes?
9. ¿Cómo va mi equipo de vendedores este mes? *(si aplica)*
10. ¿Cómo me fue comparado con el mes pasado?

### Reglas del asistente

- Responde siempre en español neutro, sin términos financieros técnicos
- Nunca inventa datos: si la respuesta no está en el dataset, lo dice claramente
- Cuando el dato tiene contexto visual útil, muestra una gráfica simple junto a la respuesta
- Las respuestas deben ser cortas — un número grande + una línea de contexto es suficiente la mayoría de las veces
- Si la pregunta está fuera del alcance del dataset, redirige amablemente a algo que sí puede responder

---

## Alerta proactiva — El diferenciador principal

Además del dashboard y el chat, el sistema debe generar al menos **una alerta proactiva automática** por día, sin que el dueño la solicite.

La alerta aparece en el header de la pantalla al abrir la app. Debe:
- Ser positiva o neutral en tono (nunca alarmista)
- Contener un dato concreto y accionable
- Tener máximo 2 líneas de texto
- Adaptarse al negocio y al momento del día

Ejemplos de alertas válidas:
- *"Ayer fue tu mejor martes del mes. Entraron $127 — pico a las 12pm"*
- *"Esta semana tus ventas subieron un 15% vs la semana pasada"*
- *"María Ruiz lleva 3 semanas sin volver — era tu cliente más frecuente"*
- *"El viernes pasado fue tu día más alto del mes"*

---

## Criterios de éxito del proyecto

Estos son los requisitos mínimos que la solución debe cumplir para considerarse funcional:

- El asistente responde correctamente al menos el 80% de las preguntas de prueba definidas
- El tiempo de respuesta promedio del asistente es inferior a 5 segundos
- Las respuestas son comprensibles para un adulto sin formación financiera, sin necesidad de explicación adicional
- El dashboard muestra datos correctos y actualizados al dataset
- La alerta proactiva se genera automáticamente y es relevante para el negocio

---

## Lo que está fuera del alcance de este MVP

Estas funcionalidades quedan fuera del proyecto para mantener el foco:

- Información sobre inventario o productos (Deuna no tiene esos datos)
- Balance de proveedores (el campo descripción en transferencias es opcional y casi nadie lo llena)
- Proyecciones del mes (requieren datos más completos para no generar números falsos)
- Integración con datos reales de Deuna (el proyecto usa el dataset sintético)
- Despliegue en producción o infraestructura escalable

---

## Entregables del proyecto

Para la presentación final se necesita:

1. **Agente conversacional funcional** con interfaz de chat
2. **Dashboard "Mis Cuentitas"** con los 4 módulos y alerta proactiva
3. **Set de 15 preguntas de prueba** con respuestas esperadas y obtenidas
4. **Documentación técnica breve** del enfoque y arquitectura
5. **Pitch de 5 minutos** con demo en vivo del asistente

---

## Recursos disponibles

| Recurso | Descripción |
|---|---|
| `cuentitas.db` | Base de datos SQLite con 6,598 transacciones de 3 negocios |
| `transactions.csv` | Todas las transacciones en formato CSV |
| `transactions_carmita.csv` | Solo Tienda de Carmita (2,084 txns) |
| `transactions_roberto.csv` | Solo Cafetería Don Roberto (2,618 txns) |
| `transactions_lucia.csv` | Solo Bazar de Lucía (1,896 txns) |
| `SPECS.md` | Este documento |
| `cuentitas-specs.md` | Especificaciones de diseño UI detalladas |
| Figma | Diseño de la pantalla "Mis Cuentitas" |

---

## Diseño de referencia

El diseño de la pantalla "Mis Cuentitas" está disponible en Figma:  
`https://www.figma.com/design/m5XFlK9fPAkaMsPBSJpOkv`

Las especificaciones detalladas de colores, tipografías, gráficas y comportamiento de cada módulo están en `cuentitas-specs.md`.
