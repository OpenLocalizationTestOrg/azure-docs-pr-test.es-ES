---
title: aaaAzure Cosmos DB .NET SDK & recursos | Documentos de Microsoft
description: "Infórmese acerca de hello API de .NET y el SDK como fechas de inicio, fechas de retirada y los cambios realizados entre cada versión de hello Azure Cosmos DB .NET SDK."
services: cosmos-db
documentationcenter: .net
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 8e239217-9085-49f5-b0a7-58d6e6b61949
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/11/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0ec30e0130067a9b8d4c9176cf7465bac8925bf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-net-sdk-download-and-release-notes"></a>SDK de .NET para Azure Cosmos DB: descarga y notas de la versión
> [!div class="op_single_selector"]
> * [.NET](documentdb-sdk-dotnet.md)
> * [Fuente de cambios de .NET](documentdb-sdk-dotnet-changefeed.md)
> * [.NET Core](documentdb-sdk-dotnet-core.md)
> * [Node.js](documentdb-sdk-node.md)
> * [Java](documentdb-sdk-java.md)
> * [Python](documentdb-sdk-python.md)
> * [REST](https://docs.microsoft.com/rest/api/documentdb/)
> * [Proveedor de recursos de REST](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [SQL](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td>**Descarga del SDK**</td><td>[NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/)</td></tr>

<tr><td>**Documentación de la API**</td><td>[Documentación de referencia de API de .NET](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td>**Ejemplos**</td><td>[Ejemplos de código de .NET](documentdb-dotnet-samples.md)</td></tr>

<tr><td>**Introducción**</td><td>[Empezar a trabajar con hello Azure Cosmos DB .NET SDK](documentdb-get-started.md)</td></tr>

<tr><td>**Tutorial de la aplicación web**</td><td>[Desarrollo de aplicaciones web con Azure Cosmos DB](documentdb-dotnet-application.md)</td></tr>

<tr><td>**Plataforma admitida actualmente**</td><td>[Microsoft .NET 4.5 Framework](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr>
</table></br>

## <a name="release-notes"></a>Notas de la versión

### <a name="a-name11701170"></a><a name="1.17.0"/>1.17.0 

* Se agregó compatibilidad para PartitionKeyRangeId como un FeedOption para definir el ámbito de valor de intervalo de claves de consulta resultados tooa partición específica. 
* Se agregó compatibilidad para StartTime como un toostart ChangeFeedOption buscando cambios Hola después de ese tiempo.

### <a name="a-name11611161"></a><a name="1.16.1"/>1.16.1
* Se corrigió un problema en hello clase JsonSerializable que podría provocar una excepción de desbordamiento de pila.

### <a name="a-name11601160"></a><a name="1.16.0"/>1.16.0
*   Se corrigió un problema que requiere volver a compilar de aplicación Hola debido toohello introducción de JsonSerializerSettings como un parámetro opcional en el constructor de DocumentClient Hola.
* Hola marcada DocumentClient constructor obsoleta que precisan JsonSerializerSettings como Hola última tooallow de parámetro para los valores predeterminados de parámetros ConnectionPolicy y ConsistencyLevel al pasar en el parámetro JsonSerializerSettings.

### <a name="a-name11501150"></a><a name="1.15.0"/>1.15.0
*   Se agregó compatibilidad con la especificación de JsonSerializerSettings personalizado al crear instancias de [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet).

### <a name="a-name11411141"></a><a name="1.14.1"/>1.14.1
*   Se ha corregido un problema que afectaba a los equipos x64 que no admiten instrucciones SSE4 y que producía una excepción SEHException al ejecutar consultas de la API de DocumentDB de Azure Cosmos DB.

### <a name="a-name11401140"></a><a name="1.14.0"/>1.14.0
*   Se agregó compatibilidad con un nuevo nivel de coherencia denominado ConsistentPrefix.
*   Se agregó compatibilidad con métricas de consulta para particiones individuales.
*   Se agregó compatibilidad para limitar el tamaño de Hola Hola de token de continuación para las consultas.
*   Se agregó compatibilidad para un seguimiento más detallado de las solicitudes con error.
*   Realizado algunas mejoras de rendimiento en hello SDK.

### <a name="a-name11341134"></a><a name="1.13.4"/>1.13.4
* Funcionalmente es igual a 1.13.3. Se hicieron algunos cambios internos.

### <a name="a-name11331133"></a><a name="1.13.3"/>1.13.3
* Funcionalmente es igual a 1.13.2. Se hicieron algunos cambios internos.

### <a name="a-name11321132"></a><a name="1.13.2"/>1.13.2
* Se ha corregido un problema que omite el valor de PartitionKey de hello proporcionado en FeedOptions para consultas de agregado.
* Se ha corregido un problema en el control transparente de administración de particiones durante la ejecución entre particiones de la consulta Order By.

### <a name="a-name11311131"></a><a name="1.13.1"/>1.13.1
* Se ha corregido un problema que provocó interbloqueos en algunos de hello async API cuando se usa dentro del contexto ASP.NET.

### <a name="a-name11301130"></a><a name="1.13.0"/>1.13.0
* Corrige toomake SDK más resistente tooautomatic conmutación por error en determinadas condiciones.

### <a name="a-name11221122"></a><a name="1.12.2"/>1.12.2
* Corrección para un problema que en ocasiones, provoca una excepción WebException: no se pudo resolver el nombre remoto Hola.
* Hola agregado compatibilidad para leer un documento mecanografiado directamente mediante la adición de nuevas sobrecargas tooReadDocumentAsync API.

### <a name="a-name11211121"></a><a name="1.12.1"/>1.12.1
* Se agregó compatibilidad con consultas de agregación para LINQ (COUNT, MIN, MAX, SUM y AVG).
* Corregir un problema de pérdida de memoria para el objeto de ConnectionPolicy Hola causado por el uso de Hola de controlador de eventos.
* Se corrigió un problema por el que UpsertAttachmentAsync no funcionaba cuando se usaba el valor ETag.
* Se corrigió un problema por el que la continuación de la consulta order-by en la partición cruzada no funcionaba cuando se ordenaba por un campo de cadena.

### <a name="a-name11201120"></a><a name="1.12.0"/>1.12.0
* Se agregó compatibilidad con consultas de agregación (COUNT, MIN, MAX, SUM y AVG). Consulte [Compatibilidad con agregación](documentdb-sql-query.md#Aggregates).
* Reducir el rendimiento mínimo en las colecciones particionadas de 10,100 RU/s too2500 RU/s.

### <a name="a-name11141114"></a><a name="1.11.4"/>1.11.4
* Corrección para un problema en el que algunas de las consultas entre particiones de Hola se producía un error en el proceso de host de 32 bits de Hola.
* Corrección para un problema en el que contenedor de la sesión de hello no se se actualizó con símbolo (token) de Hola para solicitudes con error en el modo de puerta de enlace.
* Corrección para un problema por el cual una consulta con llamadas UDF en proyección daba error en algunos casos.
* Revisiones de rendimiento de lado cliente para aumentar Hola leerán y escribir el rendimiento de las solicitudes de Hola.

### <a name="a-name11131113"></a><a name="1.11.3"/>1.11.3
* Corrección para un problema en el que contenedor de la sesión de hello no se se actualizó con símbolo (token) de Hola para solicitudes con error.
* Se agregó compatibilidad para toowork SDK de hello en un proceso de host de 32 bits. Tenga en cuenta que si utiliza consultas entre particiones, se recomienda el procesamiento de host de 64 bits para obtener un mejor rendimiento.
* Se mejoró el rendimiento en escenarios con consultas que tienen un número elevado de valores de clave de partición en una expresión IN.
* Rellena diversas estadísticas de cuota de recursos en hello ResourceResponse para las solicitudes de lectura de colección de documentos cuando se establece la opción de solicitud de PopulateQuotaInfo.

### <a name="a-name11111111"></a><a name="1.11.1"/>1.11.1
* Corrección de rendimiento menores de hello API CreateDocumentCollectionIfNotExistsAsync introducidas en 1.11.0.
* Corrección de rendimiento en hello SDK en escenarios que implican un grado elevado de solicitudes simultáneas.

### <a name="a-name11101110"></a><a name="1.11.0"/>1.11.0
* Compatibilidad con nuevos hello tooprocess de clases y métodos [Cambiar fuente](change-feed.md) de documentos dentro de una colección.
* Compatibilidad con la continuación de consultas entre particiones y algunas mejoras de rendimiento para las consultas entre particiones.
* Adición de métodos CreateDatabaseIfNotExistsAsync y CreateDocumentCollectionIfNotExistsAsync.
* Compatibilidad de LINQ para las funciones del sistema: IsDefined, IsNull e IsPrimitive.
* Corregir para binplacing automática de la carpeta bin del Microsoft.Azure.Documents.ServiceInterop.dll y DocumentDB.Spatial.Sql.dll ensamblados tooapplication cuando se usa el paquete de Nuget Hola con proyectos que tienen herramientas de project.json.
* Compatibilidad con la emisión de los seguimientos de ETW de lado cliente que podrían resultar útiles en escenarios de depuración.

### <a name="a-name11001100"></a><a name="1.10.0"/>1.10.0
* Se agregó compatibilidad de conectividad directa con colecciones con particiones.
* Mejor rendimiento para el nivel de coherencia Bounded Staleness Hola.
* Se han agregado los tipos de datos Polygon y LineString al especificar la directiva de indización de colecciones para las consultas espaciales de geovallado.
* Se agregó compatibilidad de LINQ con StringEnumConverter, IsoDateTimeConverter y UnixDateTimeConverter, a la vez que se traducen los predicados.
* Se corrigieron varios errores de SDK.

### <a name="a-name195195"></a><a name="1.9.5"/>1.9.5
* Se corrigió un problema que Hola iniciada después NotFoundException: Hola lee sesión no está disponible para el token de sesión de entrada de Hola. Se produjo esta excepción en algunos casos al consultar Hola regiones de lectura de una cuenta distribuidos geográficamente.
* Expone la propiedad de ResponseStream Hola Hola ResourceResponse clase, lo que permite la secuencia subyacente de toohello de acceso directo de una respuesta.

### <a name="a-name194194"></a><a name="1.9.4"/>1.9.4
* Hola modificado ResourceResponse, FeedResponse, StoredProcedureResponse y MediaResponse clases tooimplement hello correspondiente interfaz pública para que pueden simuladas para pruebas controladas por implementación (TDD).
* Se ha corregido un problema que generaba un encabezado de clave de partición con formato incorrecto al usar un objeto JsonSerializerSettings personalizado para serializar los datos.

### <a name="a-name193193"></a><a name="1.9.3"/>1.9.3
* Se corrigió un problema que provocó toofail de las consultas de larga ejecución con error: token de autorización no es válida en hello hora actual.
* Fijo un problema que quitan Hola SqlParameterCollection original de cross consultas top y order by de la partición.

### <a name="a-name192192"></a><a name="1.9.2"/>1.9.2
* Se ha agregado compatibilidad con las consultas paralelas en las colecciones particionadas.
* Se ha agregado compatibilidad con las consultas ORDER BY y TOP entre particiones en las colecciones particionadas.
* Hola fijo que faltan referencias tooDocumentDB.Spatial.Sql.dll y Microsoft.Azure.Documents.ServiceInterop.dll que son necesarios cuando se hace referencia a un proyecto de base de datos de Azure Cosmos con un paquete de Nuget de base de datos de Azure Cosmos toohello de referencia.
* Se ha corregido la capacidad de Hola toouse parámetros de tipos diferentes al utilizar funciones definidas por el usuario en LINQ. 
* Se corrige un error para las cuentas replicados a nivel mundial donde Upsert llamadas se están dirigido tooread ubicaciones en lugar de ubicaciones de escritura.
* Interfaz IDocumentClient de toohello nuevos métodos que no estaban presentes: 
  * El método UpsertAttachmentAsync que toma mediaStream y opciones como parámetros
  * El método CreateAttachmentAsync que toma opciones como un parámetro
  * El método CreateOfferQuery que toma querySpec como un parámetro
* Clases públicas no selladas que se exponen en la interfaz de IDocumentClient Hola.

### <a name="a-name180180"></a><a name="1.8.0"/>1.8.0
* Compatibilidad de hello agregada para cuentas de base de datos de varias regiones.
* Se ha agregado compatibilidad con el reintento en solicitudes limitadas.  Usuario puede personalizar el número de Hola de reintentos y max Hola de tiempo de espera mediante la configuración de propiedad de ConnectionPolicy.RetryOptions Hola.
* Agrega una nueva interfaz IDocumentClient que define las firmas de Hola de todos los métodos y propiedades de DocumenClient.  Como parte de este cambio, cambiar también los métodos de extensión que crean toomethods IQueryable y IOrderedQueryable en hello propia clase DocumentClient.
* Agrega el saludo de tooset de opción de configuración ServicePoint.ConnectionLimit para un punto de conexión de base de datos de Azure Cosmos Uri determinado.  Usar valor predeterminado de ConnectionPolicy.MaxConnectionLimit toochange hello, que se establece too50.
* Se ha dejado de utilizar IPartitionResolver y su implementación.  La compatibilidad con IPartitionResolver está ahora obsoleta. Se recomienda usar colecciones con particiones para conseguir un almacenamiento y un rendimiento más elevados.

### <a name="a-name171171"></a><a name="1.7.1"/>1.7.1
* Agrega que un tooUri sobrecarga según el método ExecuteStoredProcedureAsync que toma RequestOptions como un parámetro.

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
* Agregar compatibilidad en tiempo de toolive (TTL) para los documentos.

### <a name="a-name163163"></a><a name="1.6.3"/>1.6.3
* Se corrige un error en el paquete de Nuget del SDK de .NET para empaquetarlo como parte de una solución de servicio en la nube de Azure.

### <a name="a-name162162"></a><a name="1.6.2"/>1.6.2
* Se han implementado [colecciones particionadas](partition-data.md) y [niveles de rendimiento definidos por el usuario](performance-levels.md). 

### <a name="a-name153153"></a><a name="1.5.3"/>1.5.3
* **[Fija]**  Inicia el punto de conexión de base de datos de consulta Azure Cosmos: ' System.Net.Http.HttpRequestException: Error al copiar la secuencia de contenido tooa'.

### <a name="a-name152152"></a><a name="1.5.2"/>1.5.2
* Compatibilidad de LINQ ampliada, incluidos nuevos operadores de paginación, expresiones condicionales y comparación de intervalos.
  * Tomar operador tooenable comportamiento SELECT TOP en LINQ
  * Comparaciones de intervalo de CompareTo operador tooenable cadenas
  * Operadores conditional (?) y coalesce (??)
* **[Corregido]** ArgumentOutOfRangeException al combinar la proyección Model en la consulta Where-In de LINQ. [81](https://github.com/Azure/azure-documentdb-dotnet/issues/81)

### <a name="a-name151151"></a><a name="1.5.1"/>1.5.1
* **[Fija]**  Si seleccione no está Hola Hola de expresión último proveedor LINQ no supone ninguna proyección y generan SELECT * incorrectamente.  [#58](https://github.com/Azure/azure-documentdb-dotnet/issues/58)

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0
* Upsert implementada, métodos de UpsertXXXAsync agregados
* Mejoras de rendimiento para todas las solicitudes
* Compatibilidad del proveedor LINQ con los métodos condicionales, de fusión y CompareTo para cadenas
* **[Fija]**  Proveedor LINQ--> implemente contiene el método en la lista toogenerate Hola SQL mismo como en IEnumerable y matriz
* **[Fija]**  BackoffRetryUtility usa Hola mismo HttpRequestMessage nuevo en lugar de crear uno nuevo en el reintento
* **[Obsoleto]** UriFactory.CreateCollection--&gt; debería usar ahora UriFactory.CreateDocumentCollection

### <a name="a-name141141"></a><a name="1.4.1"/>1.4.1
* **[Corregido]** Problemas de localización al usar la información de referencia cultural diferente de EN como nl-NL etc. 

### <a name="a-name140140"></a><a name="1.4.0"/>1.4.0
* Se agregó el enrutamiento basado en identificador
  * Nueva tooassist UriFactory auxiliar con la creación de vínculos de recursos basado en el Id.
  * Nuevas sobrecargas en DocumentClient tootake en URI
* Se agregaron IsValid() y IsValidDetailed() en LINQ para geoespaciales
* Compatibilidad mejorada con el proveedor LINQ:
  * **Math** : Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate
  * **String** : Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper
  * **Array** : Concat, Contains, Count
  * **IN**

### <a name="a-name130130"></a><a name="1.3.0"/>1.3.0
* Se agregó compatibilidad para la modificación de las directivas de indexación.
  * Nuevo método de ReplaceDocumentCollectionAsync en DocumentClient
  * Nueva propiedad IndexTransformationProgress en ResourceResponse<T> para el seguimiento del porcentaje de progreso de cambios de la directiva de índice
  * DocumentCollection.IndexingPolicy ahora es mutable
* Se agregó compatibilidad para consulta e indexación espacial.
  * Nuevo espacio de nombres Microsoft.Azure.Documents.Spatial para serializar y deserializar tipos espaciales como punto y polígono
  * Nueva clase de SpatialIndex para la indexación de datos GeoJSON almacenados en Cosmos DB
* **[Corregido]** Consulta SQL incorrecta generada a partir de la expresión LINQ [n.º 38](https://github.com/Azure/azure-documentdb-net/issues/38).

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* Se agregó una dependencia de Newtonsoft.Json v5.0.7.
* Cambios realizados toosupport Order By:
  
  * Compatibilidad del proveedor LINQ para OrderBy() u OrderByDescending()
  * IndexingPolicy toosupport Order By 
    
    **Posible cambio importante** 
    
    Si tiene código existente que recopilaciones de disposiciones con una directiva de indexación personalizada, su toobe de necesidades de código existentes actualiza clase toosupport Hola de nuevo IndexingPolicy. Si no tiene ninguna directiva de indexación personalizada, este cambio no le afectará.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* Se agregó compatibilidad para crear particiones de datos mediante las clases nuevas de HashPartitionResolver y RangePartitionResolver Hola y Hola IPartitionResolver.
* Se agregó serialización de DataContract.
* Se agregó compatibilidad con GUID en el proveedor LINQ.
* Se agregó compatibilidad con UDF en LINQ.

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* SDK de GA

## <a name="release--retirement-dates"></a>Fechas de lanzamiento y de retirada
Microsoft proporciona una notificación al menos **12 meses** antes de retirar un SDK en la versión de más reciente admitida de orden toosmooth Hola transición tooa.

Nuevas características y funcionalidad y las optimizaciones se agregan solo toohello actual SDK, como por ejemplo, se recomienda que se realice siempre la actualización toohello última versión del SDK tan pronto como sea posible. 

Cualquier base de datos de Cosmos con un SDK de retirada de solicitudes tooAzure son rechazados por el servicio de Hola.

<br/>

| Versión | Fecha de lanzamiento | Fecha de retirada |
| --- | --- | --- |
| [1.17.0](#1.17.0) |10 de agosto de 2017 |--- |
| [1.16.1](#1.16.1) |7 de agosto de 2017 |--- |
| [1.16.0](#1.16.0) |2 de agosto de 2017 |--- |
| [1.15.0](#1.15.0) |30 de junio de 2017 |--- |
| [1.14.1](#1.14.1) |23 de mayo de 2017 |--- |
| [1.14.0](#1.14.0) |10 de mayo de 2017 |--- |
| [1.13.4](#1.13.4) |09 de mayo de 2017 |--- |
| [1.13.3](#1.13.3) |06 de mayo de 2017 |--- |
| [1.13.2](#1.13.2) |19 de abril de 2017 |--- |
| [1.13.1](#1.13.1) |29 de marzo de 2017 |--- |
| [1.13.0](#1.13.0) |24 de marzo de 2017 |--- |
| [1.12.2](#1.12.2) |20 de marzo de 2017 |--- |
| [1.12.1](#1.12.1) |14 de marzo de 2017 |--- |
| [1.12.0](#1.12.0) |15 de febrero de 2017 |--- |
| [1.11.4](#1.11.4) |06 de febrero de 2017 |--- |
| [1.11.3](#1.11.3) |26 de enero de 2017 |--- |
| [1.11.1](#1.11.1) |21 de diciembre de 2016 |--- |
| [1.11.0](#1.11.0) |08 de diciembre de 2016 |--- |
| [1.10.0](#1.10.0) |27 de septiembre de 2016 |--- |
| [1.9.5](#1.9.5) |01 de septiembre de 2016 |--- |
| [1.9.4](#1.9.4) |24 de agosto de 2016 |--- |
| [1.9.3](#1.9.3) |15 de agosto de 2016 |--- |
| [1.9.2](#1.9.2) |23 de julio de 2016 |--- |
| [1.8.0](#1.8.0) |14 de junio de 2016 |--- |
| [1.7.1](#1.7.1) |06 de mayo de 2016 |--- |
| [1.7.0](#1.7.0) |26 de abril de 2016 |--- |
| [1.6.3](#1.6.3) |08 de abril de 2016 |--- |
| [1.6.2](#1.6.2) |29 de marzo de 2016 |--- |
| [1.5.3](#1.5.3) |19 de febrero de 2016 |--- |
| [1.5.2](#1.5.2) |14 de diciembre de 2015 |--- |
| [1.5.1](#1.5.1) |23 de noviembre de 2015 |--- |
| [1.5.0](#1.5.0) |05 de octubre de 2015 |--- |
| [1.4.1](#1.4.1) |25 de agosto de 2015 |--- |
| [1.4.0](#1.4.0) |13 de agosto de 2015 |--- |
| [1.3.0](#1.3.0) |05 de agosto de 2015 |--- |
| [1.2.0](#1.2.0) |06 de julio de 2015 |--- |
| [1.1.0](#1.1.0) |30 de abril de 2015 |--- |
| [1.0.0](#1.0.0) |08 de abril de 2015 |--- |


## <a name="faq"></a>Preguntas más frecuentes
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>Otras referencias
toolearn más información acerca de la base de datos de Cosmos, consulte [base de datos de Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) página de servicio. 

