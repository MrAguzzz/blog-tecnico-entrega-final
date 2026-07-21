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

---

## Acciones realizadas

- Revisión de logs del servidor.
- Simulación de compras con diferentes usuarios.
- Verificación de la API del proveedor de pagos.
- Comparación con versiones anteriores del sistema.
- Corrección de la configuración de autenticación.

---

## Resumen (Problema - Accion - impacto)

### Problema

Los pedidos no podían completarse.

### Acción

Se detectó que una credencial utilizada para comunicarse con el proveedor de pagos había expirado. Se actualizó la configuración y se realizaron pruebas funcionales para validar la solución.

### Impacto

- Los usuarios pudieron finalizar compras nuevamente.
- Se redujeron los reclamos al soporte.
- El sistema volvió a operar normalmente.

---

# Post-Mortem Constructivo

## ¿Qué ocurrió?

Una credencial vencida impedía la comunicación entre la aplicación y el proveedor de pagos.

## Causa raíz

No existía un mecanismo que alertara sobre el vencimiento de las credenciales utilizadas por el sistema.

## Acciones correctivas

- Actualizar las credenciales.
- Verificar la configuración del servicio.
- Validar nuevamente todo el flujo de compra.

## Acciones preventivas

- Implementar alertas antes del vencimiento de las credenciales.
- Incorporar pruebas automáticas del proceso de compra.
- Documentar las configuraciones críticas del sistema.

---

## Aprendizajes

Este incidente demostró la importancia de monitorear servicios externos y mantener documentadas las configuraciones críticas.

También reforzó la necesidad de validar los componentes externos antes de asumir que el problema se encuentra dentro del código de la aplicación.

---

## Evidencia de control de versiones

Repositorio:
https://github.com/mraguzzz/blog-tecnico-entrega-final

Historial de commits:
https://github.com/mraguzzz/blog-tecnico-entrega-final/commits/main

---

## Reflexión sobre feedback radicalmente sincero

Durante la investigación, un compañero comentó que el equipo estaba enfocando el análisis únicamente en la base de datos y no estaba considerando los servicios externos.

En lugar de descartar esa observación, decidimos ampliar la investigación y revisar el servicio de procesamiento de pagos. Gracias a ese cambio de enfoque identificamos la causa real del incidente en menor tiempo.

Esta experiencia reforzó la importancia de aceptar comentarios honestos y bien fundamentados, ya que permiten cuestionar supuestos, mejorar la toma de decisiones y resolver problemas de manera más eficiente.
