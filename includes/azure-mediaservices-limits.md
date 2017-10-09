>[!NOTE]
>Para los recursos que no son fijos, se puede pedir Hola cuotas toobe generado, abriendo una incidencia de soporte técnico. Hacer **no** cree cuentas de servicios multimedia de Azure adicionales en un intento de tooobtain los límites superiores.

| Recurso | Límite predeterminado | 
| --- | --- | 
| Cuentas de Servicios multimedia de Azure (AMS) en una única suscripción | 25 (fijo) |
| Unidades reservadas de multimedia (RU) por cuenta de AMS |25 (S1, S2)<br/>10 (S3) <sup>(1)</sup> | 
| Trabajos por cuenta de AMS | 50,000<sup>(2)</sup> |
| Tareas encadenadas por trabajo | 30 (fijo) |
| Recursos por cuenta de AMS | 1 000 000|
| Recursos por tarea. | 50 |
| Recursos por trabajo | 100 |
| Localizadores únicos asociados a un recurso al mismo tiempo | 5<sup>(4)</sup> |
| Canales activos por cuenta de AMS |5|
| Programas en estado detenido por canal  |50|
| Programas en estado de ejecución por canal  |3|
| Extremos de streaming en estado de ejecución por cuenta de ASM|2|
| Unidades de streaming por extremo de streaming |10 |
| Cuentas de almacenamiento | 1000 <sup>(5)</sup> (fijo) |
| Directivas | 1 000 000<sup>(6)</sup> |
| Tamaño de archivo| En algunos escenarios hay un límite de tamaño máximo de archivo de hello admitido para el procesamiento de los servicios multimedia. <sup>7</sup> |
  
<sup>1</sup> Las RU S3 no están disponibles en India occidental. Hola max RU límites restablecería si cambia de cliente de Hola Hola tipo (por ejemplo, de tooS1 S2). 

<sup>2</sup> Este número incluye los trabajos en cola, terminados, activos y cancelados. No incluye los trabajos eliminados. Puede eliminar los trabajos antiguos Hola con **IJob.Delete** o hello **eliminar** solicitud HTTP.

A partir del 1 de abril de 2017, cualquier registro de trabajo en su cuenta de más de 90 días se eliminarán automáticamente, junto con sus registros de tarea asociados, incluso si el número total de Hola de registros está por debajo de la cuota máxima de Hola. Si necesita información de trabajo o tarea hello tooarchive, puede usar código de hello descrito [aquí](../articles/media-services/media-services-dotnet-manage-entities.md).

<sup>3</sup> al realizar una solicitud de entidades de trabajo toolist, se devolverá un máximo de 1.000 por solicitud. Si necesita realizar un seguimiento de tookeep de todos los envían trabajos, puede utilizar top/skip tal y como se describe en [opciones de consulta de sistema de OData](http://msdn.microsoft.com/library/gg309461.aspx).

<sup>4</sup> Los localizadores no están diseñados para administrar el control de acceso por usuario. usuarios de tooindividual de derechos de acceso diferentes toogive, usar soluciones de administración de derechos digitales (DRM). Para obtener más información, consulte [esta](../articles/media-services/media-services-content-protection-overview.md) sección.

<sup>5</sup> cuentas de almacenamiento de hello deben provenir de hello misma suscripción de Azure.

<sup>6</sup> hay un límite de 1 000 000 directivas para diferentes directivas de AMS (por ejemplo, para la directiva de localizador o ContentKeyAuthorizationPolicy). 

>[!NOTE]
> Debe usar hello mismo Id. de directiva si utilizas siempre Hola mismo días / permisos de acceso / etcetera. Para obtener información y un ejemplo, consulte [esta](../articles/media-services/media-services-dotnet-manage-entities.md#limit-access-policies) sección.

<sup>7</sup>si va a cargar tooan contenido activo en Azure Media Services con tooprocess intención de hello con uno de los procesadores de multimedia de hello en nuestro servicio (es decir, los codificadores como motores Media Encoder estándar y flujo de trabajo de Premium de codificación de medios o análisis a continuación, al igual que el Detector de caras), debe conocer de restricción de hello en el tamaño máximo de Hola. 

A partir del 15 de mayo de 2017, tamaño máximo de hello admitido para un único blob es TB 195 - con largers de archivo que este límite, se producirá un error en la tarea. Estamos trabajando un tooaddress corrección este límite. Además, Hola restricción de tamaño máximo de Hola de hello Asset es como sigue.

| Tipo de unidad reservada de medios | Tamaño máximo de entrada (GB)| 
| --- | --- | 
|S1 | 325|
|S2 | 640|
|S3 | 260|
