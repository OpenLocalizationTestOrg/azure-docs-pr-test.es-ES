---
title: aaaAzure Cosmos DB .NET Core API, SDK y recursos | Documentos de Microsoft
description: "Infórmese acerca de hello .NET Core API y SDK, incluidas las fechas de lanzamiento y fechas de retirada, los cambios realizados entre cada versión de hello Azure Cosmos DB .NET Core SDK."
services: cosmos-db
documentationcenter: .net
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: f899b314-26ac-4ddb-86b2-bfdf05c2abf2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/11/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1269cafe0ea1caaa871404d507b12632dbb3ed82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-net-core-sdk-release-notes-and-resources"></a>SDK de .NET Core para Azure Cosmos DB: notas de la versión y recursos
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

<tr><td>**Descarga del SDK**</td><td>[NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/)</td></tr>

<tr><td>**Documentación de la API**</td><td>[Documentación de referencia de API de .NET](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td>**Ejemplos**</td><td>[Ejemplos de código de .NET](documentdb-dotnet-samples.md)</td></tr>

<tr><td>**Introducción**</td><td>[Empezar a trabajar con hello Azure Cosmos DB .NET Core SDK](documentdb-dotnetcore-get-started.md)</td></tr>

<tr><td>**Tutorial de la aplicación web**</td><td>[Desarrollo de aplicaciones web con Azure Cosmos DB](documentdb-dotnet-application.md)</td></tr>

<tr><td>**Plataforma admitida actualmente**</td><td>[.NET Standard 1.6 y .NET Standard 1.5](https://www.nuget.org/packages/NETStandard.Library)</td></tr>
</table></br>

## <a name="release-notes"></a>Notas de la versión

Hello Azure Cosmos DB .NET Core SDK tiene una paridad de características con la versión más reciente de Hola de hello [SDK de .NET de base de datos de Azure Cosmos](documentdb-sdk-dotnet.md).

> [!NOTE] 
> Hello Azure Cosmos DB .NET Core SDK todavía no es compatible con aplicaciones de la plataforma Universal de Windows (UWP). Si está interesado en hello .NET Core SDK que admite las aplicaciones UWP, enviar correo electrónico demasiado[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0 

* Se agregó compatibilidad para PartitionKeyRangeId como un FeedOption para definir el ámbito de valor de intervalo de claves de consulta resultados tooa partición específica. 
* Se agregó compatibilidad para StartTime como un toostart ChangeFeedOption buscando cambios Hola después de ese tiempo. 

### <a name="a-name141141"></a><a name="1.4.1"/>1.4.1

*   Se corrigió un problema en hello clase JsonSerializable que podría provocar una excepción de desbordamiento de pila.

### <a name="a-name140140"></a><a name="1.4.0"/>1.4.0

*   Se agregó compatibilidad con la especificación de JsonSerializerSettings personalizado al crear una instancia de [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet).

### <a name="a-name132132"></a><a name="1.3.2"/>1.3.2

*   Se admiten 1.5 estándar de .NET como uno de los marcos de destino de Hola.

### <a name="a-name131131"></a><a name="1.3.1"/>1.3.1

*   Se corrigió un problema que afectaba a las máquinas x64 que no admiten instrucciones SSE4 y que producía una excepción SEHException al ejecutar consultas de Azure Cosmos DB.

### <a name="a-name130130"></a><a name="1.3.0"/>1.3.0

*   Se agregó compatibilidad con un nuevo nivel de coherencia denominado ConsistentPrefix.
*   Se agregó compatibilidad con métricas de consulta para particiones individuales.
*   Se agregó compatibilidad para limitar el tamaño de Hola Hola de token de continuación para las consultas.
*   Se agregó compatibilidad para un seguimiento más detallado de las solicitudes con error.
*   Realizado algunas mejoras de rendimiento en hello SDK.

### <a name="a-name122122"></a><a name="1.2.2"/>1.2.2

* Se ha corregido un problema que omite el valor de PartitionKey de hello proporcionado en FeedOptions para consultas de agregado.
* Se ha corregido un problema en el control transparente de administración de particiones durante la ejecución entre particiones de la consulta Order By.

### <a name="a-name121121"></a><a name="1.2.1"/>1.2.1

* Se ha corregido un problema que provocó interbloqueos en algunos de hello async API cuando se usa dentro del contexto ASP.NET.

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0

* Corrige toomake SDK más resistente tooautomatic conmutación por error en determinadas condiciones.

### <a name="a-name112112"></a><a name="1.1.2"/>1.1.2

* Corrección para un problema que en ocasiones, provoca una excepción WebException: no se pudo resolver el nombre remoto Hola.
* Hola agregado compatibilidad para leer un documento mecanografiado directamente mediante la adición de nuevas sobrecargas tooReadDocumentAsync API.

### <a name="a-name111111"></a><a name="1.1.1"/>1.1.1

* Se agregó compatibilidad con consultas de agregación para LINQ (COUNT, MIN, MAX, SUM y AVG).
* Corregir un problema de pérdida de memoria para el objeto de ConnectionPolicy Hola causado por el uso de Hola de controlador de eventos.
* Se corrigió un problema por el que UpsertAttachmentAsync no funcionaba cuando se usaba el valor ETag.
* Se corrigió un problema por el que la continuación de la consulta order-by en la partición cruzada no funcionaba cuando se ordenaba por un campo de cadena.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0

* Se agregó compatibilidad con consultas de agregación (COUNT, MIN, MAX, SUM y AVG). Consulte [Compatibilidad con agregación](documentdb-sql-query.md#Aggregates).
* Reducir el rendimiento mínimo en las colecciones particionadas de 10,100 RU/s too2500 RU/s.

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0

Hello Azure Cosmos DB .NET Core SDK permite toobuild rápidos, multiplataforma [ASP.NET Core](https://www.asp.net/core) y [.NET Core](https://www.microsoft.com/net/core#windows) toorun de aplicaciones en Windows, Mac y Linux. Hola versión más reciente de hello Azure Cosmos DB .NET Core SDK es totalmente [Xamarin](https://www.xamarin.com) compatible y aplicaciones usados toobuild destinados a iOS, Android y Mono (Linux).  

### <a name="a-name010-preview010-preview"></a><a name="0.1.0-preview"/>0.1.0-preview

Hola SDK de vista previa de Azure Cosmos DB .NET Core le permite toobuild rápidos, multiplataforma [ASP.NET Core](https://www.asp.net/core) y [.NET Core](https://www.microsoft.com/net/core#windows) toorun de aplicaciones en Windows, Mac y Linux.

Hola SDK de Azure Cosmos DB .NET Core Preview tiene una paridad de características con la versión más reciente de Hola de hello [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md) y es compatible con hello siguientes:
* Todos los [modos de conexión](performance-tips.md#networking): modo de puerta de enlace, TCP directo y HTTPS directo. 
* Todos los [niveles de coherencia](consistency-levels.md): fuerte, sesión, obsolescencia limitada y ocasional.
* [Colecciones con particiones](partition-data.md). 
* [Cuentas de base de datos de varias regiones y replicación geográfica](distribute-data-globally.md).

Si tiene preguntas relacionadas toothis SDK, registrar demasiado[StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), archivo o un problema en hello [repositorio de github](https://github.com/Azure/azure-documentdb-dotnet/issues). 

## <a name="release--retirement-dates"></a>Fechas de lanzamiento y de retirada

| Versión | Fecha de lanzamiento | Fecha de retirada |
| --- | --- | --- |
| [1.5.0](#1.5.0) |10 de agosto de 2017 |--- | 
| [1.4.1](#1.4.1) |7 de agosto de 2017 |--- |
| [1.4.0](#1.4.0) |2 de agosto de 2017 |--- |
| [1.3.2](#1.3.2) |12 de junio de 2017 |--- |
| [1.3.1](#1.3.1) |23 de mayo de 2017 |--- |
| [1.3.0](#1.3.0) |10 de mayo de 2017 |--- |
| [1.2.2](#1.2.2) |19 de abril de 2017 |--- |
| [1.2.1](#1.2.1) |29 de marzo de 2017 |--- |
| [1.2.0](#1.2.0) |25 de marzo de 2017 |--- |
| [1.1.2](#1.1.2) |20 de marzo de 2017 |--- |
| [1.1.1](#1.1.1) |14 de marzo de 2017 |--- |
| [1.1.0](#1.1.0) |16 de febrero de 2017 |--- |
| [1.0.0](#1.0.0) |21 de diciembre de 2016 |--- |
| [0.1.0-preview](#0.1.0-preview) |15 de noviembre de 2016 |31 de diciembre de 2016 |

## <a name="see-also"></a>Otras referencias
toolearn más información acerca de la base de datos de Cosmos, consulte [base de datos de Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) página de servicio. 

