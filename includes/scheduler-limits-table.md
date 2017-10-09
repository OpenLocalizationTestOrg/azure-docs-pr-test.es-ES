Hello en la tabla siguiente describe cada una de las principales cuotas de hello, límites, valores predeterminados y limitaciones de Azure Scheduler.

| Recurso | Descripción de límites |
| --- | --- |
| **Tamaño del trabajo** |El tamaño máximo del trabajo es 16 K. Si una solicitud PUT o PATCH produce un trabajo mayor que estos límites, se devuelve un código de estado 400 Solicitud incorrecta. |
| **Tamaño de la dirección URL de la solicitud** |Tamaño máximo de la dirección URL de solicitud de hello es de 2048 caracteres. |
| **Tamaño del encabezado de agregado** |El tamaño máximo del encabezado de agregado es de 4096 caracteres. |
| **Recuento de encabezados** |El recuento máximo de encabezados es de 50 encabezados. |
| **Tamaño del cuerpo** |El tamaño máximo del cuerpo es de 8192 caracteres. |
| **Intervalo de periodicidad** |El intervalo máximo de periodicidad es de 18 meses. |
| **Tiempo de toostart** |"Hora toostart horario" máximo es de 18 meses. |
| **Historial de trabajos** |El tamaño máximo del cuerpo de la respuesta que se almacena en el historial de trabajos es de 2048 bytes. |
| **Frecuencia** |cuota de frecuencia máxima de Hello predeterminada es 1 hora en una colección de trabajos gratuitas y 1 minuto en una colección de trabajos estándar. frecuencia máxima de Hello es configurable en un toobe de colección de trabajo inferior Hola máximo. Todos los trabajos en la colección de trabajos de hello son valor limitado Hola establecer en la colección de trabajos de Hola. Si intentas toocreate un trabajo con una frecuencia mayor que la frecuencia máxima de hello en la colección de trabajos de hello solicitud dará error con un código de estado 409 conflicto. |
| **Trabajos** |cuota de trabajos máxima predeterminada de Hello es de 5 trabajos en una colección de trabajos gratuitas y 50 trabajos en una colección de trabajos estándar. Hola número máximo de trabajos es configurable en una colección de trabajos. Todos los trabajos en la colección de trabajos de hello son valor limitado Hola establecer en la colección de trabajos de Hola. Si intentas toocreate más trabajos que cuota máxima de trabajos de hello, solicitud de hello produce un error con un código de estado 409 conflicto. |
| **Colecciones de trabajos** |El número máximo de colecciones de trabajos por suscripción es 200 000. |
| **Retención de historial de trabajos** |Historial de trabajos se conserva durante los meses de too2 o la toohello último 1000 ejecuciones. |
| **Retención de trabajos completados y con errores** |Los trabajos completados y con errores se conservan durante 60 días. |
| **Tiempo de espera** |Hay un tiempo de espera de solicitud estático (no configurable) de 60 segundos para las acciones de HTTP. Para las operaciones de ejecución más largas, siga los protocolos HTTP asincrónicos; Por ejemplo, devolver inmediatamente un 202 pero seguir trabajando en segundo plano de Hola. |

