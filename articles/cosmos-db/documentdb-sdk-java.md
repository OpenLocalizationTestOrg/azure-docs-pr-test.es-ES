---
title: 'Azure Cosmos DB: API, SDK y recursos de Java para DocumentDB | Microsoft Docs'
description: "Infórmese acerca de hello SDK como fechas de inicio, fechas de retirada y los cambios realizados entre cada versión del SDK de Java de documentos de base de datos de Azure Cosmos hello y API de Java."
services: cosmos-db
documentationcenter: java
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 7861cadf-2a05-471a-9925-0fec0599351b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 07/11/2017
ms.author: khdang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8ef43ebeb7ae1bfc55512c4a7489c1b7930122d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-documentdb-java-sdk-release-notes-and-resources"></a>Azure Cosmos DB: notas de la versión y recursos del SDK de Java para DocumentDB
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

<tr><td>**Descarga del SDK**</td><td>[Maven](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-documentdb%22)</td></tr>

<tr><td>**Documentación de la API**</td><td>[Documentación de referencia de API](/java/api/com.microsoft.azure.documentdb)</td></tr>

<tr><td>**Contribuir tooSDK**</td><td>[GitHub](https://github.com/Azure/azure-documentdb-java/)</td></tr>

<tr><td>**Introducción**</td><td>[Empezar a trabajar con hello SDK de Java](documentdb-java-get-started.md)</td></tr>

<tr><td>**Tutorial de la aplicación web**</td><td>[Desarrollo de aplicaciones web con Azure Cosmos DB](documentdb-java-application.md)</td></tr>

<tr><td>**Tiempo de ejecución admitido actualmente**</td><td>[JDK 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)</td></tr>
</table></br>

## <a name="release-notes"></a>Notas de la versión

### <a name="a-name11201120"></a><a name="1.12.0"/>1.12.0
* Divide toorequest crítico correcciones de errores de procesamiento durante la partición.
* Se ha corregido un problema con hello seguro y niveles de coherencia de BoundedStaleness.

### <a name="a-name11101110"></a><a name="1.11.0"/>1.11.0
* Se agregó compatibilidad con un nuevo nivel de coherencia denominado ConsistentPrefix.
* Se ha corregido un error en la lectura de la colección en modo de sesión.

### <a name="a-name11001100"></a><a name="1.10.0"/>1.10.0
* Habilitada compatibilidad para las colecciones particionadas con al menos 2500 RU/s y aumentos de 100 RU/s.
* Se ha corregido un error en ensamblado nativo de hello, lo que puede producir la excepción NullRef en algunas consultas.

### <a name="a-name196196"></a><a name="1.9.6"/>1.9.6
* Se ha corregido un error en la configuración del motor de consulta de Hola que puede provocar excepciones para las consultas en modo de puerta de enlace.
* Se ha corregido algunos errores en el contenedor de la sesión de Hola que pueden provocar una excepción "Recurso de propietario no encontrado" para las solicitudes inmediatamente después de la creación de la colección.

### <a name="a-name195195"></a><a name="1.9.5"/>1.9.5
* Se agregó compatibilidad con consultas de agregación (COUNT, MIN, MAX, SUM y AVG). Consulte [Compatibilidad con agregación](documentdb-sql-query.md#Aggregates).
* Compatibilidad agregada para cambiar la fuente.
* Compatibilidad agregada para la recopilación de la información de cuota mediante RequestOptions.setPopulateQuotaInfo.
* Compatibilidad agregada para el registro de scripts de procedimiento almacenados mediante RequestOptions.setScriptLoggingEnabled.
* Se ha corregido un error en el que una consulta en modo DirectHttps puede bloquearse cuando se producen errores de limitación.
* Se ha corregido un error en modo de sesión de coherencia.
* Se ha corregido un error que puede causar una excepción NullReferenceException en HttpContext cuando la tasa de solicitudes es alta.
* Rendimiento mejorado del modo DirectHttps.

### <a name="a-name194194"></a><a name="1.9.4"/>1.9.4
* Con la API ConnectionPolicy.setProxy(), se ha agregado compatibilidad simple con proxy basada en instancias del cliente.
* Agregado DocumentClient.close() tooproperly apagado DocumentClient instancia de la API.
* Mejora del rendimiento en modo de conexión directa con derivando plan de consulta de Hola de ensamblados nativa de hello en lugar de hello puerta de enlace.
* Establecer FAIL_ON_UNKNOWN_PROPERTIES = false para los usuarios no necesitan toodefine JsonIgnoreProperties en su POJO.
* Registro refactorizado toouse SLF4J.
* Se han corregido otros errores en el lector de coherencia.

### <a name="a-name193193"></a><a name="1.9.3"/>1.9.3
* Se corrige un error en pérdidas de conexión de hello conexión administración tooprevent en modo de conexión directa.
* Corregido un error en la consulta TOP Hola donde pueden producir excepciones de NullReferenece.
* Mejorar el rendimiento reduciendo el número de Hola de llamada de red para las memorias caché interna de Hola.
* Se ha agregado código de estado, ActivityID y la URI de la solicitud en DocumentClientException para una mejor solución de problemas.

### <a name="a-name192192"></a><a name="1.9.2"/>1.9.2
* Se corrigió un problema en la administración de conexión de Hola de estabilidad.

### <a name="a-name191191"></a><a name="1.9.1"/>1.9.1
* Compatibilidad agregada con el nivel de coherencia BoundedStaleness.
* Se ha agregado compatibilidad con la conectividad directa de las colecciones particionadas.
* Se ha corregido un error al realizar consultas en una base de datos con SQL.
* Se ha corregido un error en caché de la sesión de Hola donde el token de sesión puede estar configurado incorrectamente.

### <a name="a-name190190"></a><a name="1.9.0"/>1.9.0
* Compatibilidad agregada con las consultas paralelas entre particiones.
* Se ha agregado compatibilidad con las consultas TOP y ORDER BY en las colecciones particionadas.
* Compatibilidad agregada con Coherencia fuerte.
* Se ha agregado compatibilidad con las solicitudes basadas en nombres al utilizar la conectividad directa.
* Toomake fijo ActivityId permanezca coherente entre todos los reintentos de solicitud.
* Se ha corregido un error relacionados con la caché de la sesión de toohello al volver a crear una colección con hello mismo nombre.
* Se han agregado los tipos de datos Polygon y LineString al especificar la directiva de indización de colecciones para las consultas espaciales de geovallado.
* Problemas corregidos con Java Doc para Java 1.8.

### <a name="a-name181181"></a><a name="1.8.1"/>1.8.1
* Se ha corregido un error en PartitionKeyDefinitionMap toocache colecciones de una sola partición y no hacer adicional capturar partición las solicitudes de clave.
* Se ha corregido un reintento de toonot de error cuando se proporciona un valor de clave de partición correcta.

### <a name="a-name180180"></a><a name="1.8.0"/>1.8.0
* Compatibilidad de hello agregada para cuentas de base de datos de varias regiones.
* Se agregó compatibilidad para el reintento automático en las solicitudes limitadas con hello de toocustomize opciones max reintentos y tiempo de espera de reintento max.  Consulte RetryOptions y ConnectionPolicy.getRetryOptions().
* Se ha dejado de utilizar el código de creación de particiones personalizado basado en IPartitionResolver. Utilice colecciones con particiones para conseguir un almacenamiento y un rendimiento más elevados.

### <a name="a-name171171"></a><a name="1.7.1"/>1.7.1
* Se ha agregado compatibilidad con la directiva de reintentos de la limitación.  

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
* Agregar compatibilidad en tiempo de toolive (TTL) para los documentos.

### <a name="a-name160160"></a><a name="1.6.0"/>1.6.0
* Se han implementado [colecciones particionadas](partition-data.md) y [niveles de rendimiento definidos por el usuario](performance-levels.md).

### <a name="a-name151151"></a><a name="1.5.1"/>1.5.1
* Se ha corregido un error en valores de hash de HashPartitionResolver toogenerate en toobe little-endian coherente con otros SDK de.

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0
* Agregar Hash & intervalo tooassist de resoluciones de partición con aplicaciones de particionamiento entre varias particiones.

### <a name="a-name140140"></a><a name="1.4.0"/>1.4.0
* Implementación de Upsert. Nuevos métodos de upsertXXX agregan toosupport Upsert característica.
* Se implementa el enrutamiento por identificador. Sin cambios en la API pública, todos los cambios son internos.

### <a name="a-name130130"></a><a name="1.3.0"/>1.3.0
* Versión omitió toobring el número de versión en consonancia con el resto de SDK

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* Compatible con índice geoespacial.
* Valida la propiedad id para todos los recursos. Los identificadores de recursos no pueden contener los caracteres ?, /, #, \, ni terminar con un espacio.
* Agrega el nuevo encabezado "curso de transformación de índice" tooResourceResponse.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* Implementación de la directiva de indexación V2

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* SDK de GA

## <a name="release--retirement-dates"></a>Fechas de lanzamiento y de retirada
Microsoft proporcionará la notificación al menos **12 meses** antes de retirar un SDK en la versión de más reciente admitida de orden toosmooth Hola transición tooa.

Nuevas características y funcionalidad y las optimizaciones se agregan solo toohello actual SDK, por lo tanto, es recomendable que se realice siempre la actualización toohello última versión del SDK tan pronto como sea posible.

Servicio de hello rechazará cualquier base de datos con un SDK retirado tooCosmos de solicitud.

> [!WARNING]
> Todas las versiones de hello DocumentDB SDK para Java anterior tooversion **1.0.0** se retirarán en **29 de febrero de 2016**.
> 
> 

<br/>

| Versión | Fecha de lanzamiento | Fecha de retirada |
| --- | --- | --- |
| [1.12.0](#1.12.0) |11 de julio de 2017 |--- |
| [1.11.0](#1.11.0) |10 de mayo de 2017 |--- |
| [1.10.0](#1.10.0) |11 de marzo de 2017 |--- |
| [1.9.6](#1.9.6) |21 de febrero de 2017 |--- |
| [1.9.5](#1.9.5) |31 de enero de 2017 |--- |
| [1.9.4](#1.9.4) |24 de noviembre de 2016 |--- |
| [1.9.3](#1.9.3) |30 de octubre de 2016 |--- |
| [1.9.2](#1.9.2) |28 de octubre de 2016 |--- |
| [1.9.1](#1.9.1) |26 de octubre de 2016 |--- |
| [1.9.0](#1.9.0) |03 de octubre de 2016 |--- |
| [1.8.1](#1.8.1) |30 de junio de 2016 |--- |
| [1.8.0](#1.8.0) |14 de junio de 2016 |--- |
| [1.7.1](#1.7.1) |30 de abril de 2016 |--- |
| [1.7.0](#1.7.0) |27 de abril de 2016 |--- |
| [1.6.0](#1.6.0) |29 de marzo de 2016 |--- |
| [1.5.1](#1.5.1) |31 de diciembre de 2015 |--- |
| [1.5.0](#1.5.0) |04 de diciembre de 2015 |--- |
| [1.4.0](#1.4.0) |05 de octubre de 2015 |--- |
| [1.3.0](#1.3.0) |05 de octubre de 2015 |--- |
| [1.2.0](#1.2.0) |05 de agosto de 2015 |--- |
| [1.1.0](#1.1.0) |09 de julio de 2015 |--- |
| [1.0.1](#1.0.1) |12 de mayo de 2015 |--- |
| [1.0.0](#1.0.0) |07 de abril de 2015 |--- |
| 0.9.5-prelease |09 de marzo de 2015 |29 de febrero de 2016 |
| 0.9.4-prelease |17 de febrero de 2015 |29 de febrero de 2016 |
| 0.9.3-prelease |13 de enero de 2015 |29 de febrero de 2016 |
| 0.9.2-prelease |19 de diciembre de 2014 |29 de febrero de 2016 |
| 0.9.1-prelease |19 de diciembre de 2014 |29 de febrero de 2016 |
| 0.9.0-prelease |10 de diciembre de 2014 |29 de febrero de 2016 |

## <a name="faq"></a>P+F
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>Otras referencias
toolearn más información acerca de la base de datos de Cosmos, consulte [base de datos de Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) página de servicio.

