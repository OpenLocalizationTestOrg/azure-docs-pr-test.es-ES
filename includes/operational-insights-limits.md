
>[!NOTE]
>Anteriormente Log Analytics se denominaba Operational Insights.
>
>

Hola siguiendo los límites aplica los recursos de análisis de tooLog por suscripción:

| Recurso | Límite predeterminado | Comentarios
| --- | --- | --- |
| Número de áreas de trabajo gratuitas por suscripción | 10 | Este límite no puede aumentarse. |
| Número de áreas de trabajo de pago por suscripción | N/D | Está limitado por el número de Hola de recursos dentro de un grupo de recursos y el número de grupos de recursos por suscripción | 


Hola siguiendo los límites aplica área de trabajo de análisis de registros de tooeach:

|  | Gratuito | Estándar | Premium | Independiente | OMS |
| --- | --- | --- | --- | --- | --- |
| Volumen de datos recopilado por día |500 MB<sup>1</sup> |None |None | None | None
| Período de retención de datos |7 días |1 mes |12 meses | 1 mes<sup>2</sup> | 1 mes<sup>2</sup>|

<sup>1</sup> cuando los clientes alcanzan su límite de transferencia de datos diario de 500 MB, análisis de datos se detiene y se reanuda en el inicio de Hola de hello día siguiente. Un día se basa en UTC.

<sup>2</sup> período de retención de datos de hello hello independiente y planes de precios de OMS puede ser mayor too730 días.

| Categoría | Límites | Comentarios
| --- | --- | --- |
| API de recopilador de datos | El tamaño máximo de una sola publicación es 30 MB<br>El tamaño máximo de los valores de campo es 32 KB | Dividir volúmenes más grandes en varias publicaciones<br>Los campos de más de 32 KB se truncan. |
| API de búsqueda | 5000 registros devueltos para los datos no agregados<br>500 000 registros para los datos agregados | Datos agregados están una búsqueda que incluya hello `measure` comando
 
