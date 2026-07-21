# blog-tecnico-entrega-final
Blog técnico con análisis post-mortem y documentación de un desafío técnico.

## Contexto

Durante el desarrollo de una tienda online, varios usuarios comenzaron a reportar que podían agregar productos al carrito, pero al intentar confirmar la compra recibían un mensaje de error y el pedido nunca se registraba.

El incidente afectaba directamente la experiencia del usuario y las ventas del sitio, por lo que fue tratado como una incidencia de alta prioridad.

---

## Problema

Los usuarios podían navegar normalmente por el sitio, iniciar sesión y agregar productos al carrito, pero el botón **Finalizar compra** devolvía un error inesperado.

No existía pérdida de información, aunque ninguna compra podía completarse correctamente.

---

## Evidencias

- Incremento de reportes en soporte.
- Registros del servidor con errores HTTP 500.
- No se registraban nuevos pedidos en la base de datos.
- El problema ocurría únicamente durante el proceso de pago.

---

## Hipótesis

1. Error en la conexión con la base de datos.
2. Problema con el servicio de procesamiento de pagos.
3. Error de programación en el backend al guardar el pedido.

---

## Priorización

| Hipótesis | Probabilidad | Impacto | Puntaje |
|-----------|-------------|---------|---------|
| Servicio de pagos | Alta | Alto | 9 |
| Error backend | Media | Alto | 7 |
| Base de datos | Baja | Alto | 5 |
