---
title: "las aplicaciones móviles de aaaBuild con Xamarin y base de datos de Azure Cosmos | Documentos de Microsoft"
description: "Tutorial que permite crear una aplicación de Xamarin iOS, Android o Forms mediante Azure Cosmos DB. Azure Cosmos DB es una base de datos de nube, a escala mundial y rápida para aplicaciones móviles."
services: cosmos-db
documentationcenter: .net
author: arramac
manager: monicar
editor: 
ms.assetid: ff97881a-b41a-499d-b7ab-4f394df0e153
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: arramac
ms.openlocfilehash: 362a0e239a61e1309e1cf720c23151760952cf69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="build-mobile-applications-with-xamarin-and-azure-cosmos-db"></a>Creación de aplicaciones móviles con Xamarin y Azure Cosmos DB
Aplicaciones móviles más necesitan toostore datos en la nube de Hola y base de datos de Azure Cosmos es una base de datos en la nube para las aplicaciones móviles. Tiene todo lo que un desarrollador de aplicaciones móviles puede necesitar. Es una base de datos como servicio completamente administrada que se escala a petición. Puede poner la aplicación de tooyour de datos de forma transparente, siempre que los usuarios se encuentran en todo el mundo Hola. Mediante el uso de hello [Azure Cosmos DB .NET Core SDK](documentdb-sdk-dotnet-core.md), puede habilitar toointeract de aplicaciones móviles de Xamarin directamente con Azure Cosmos DB, sin un nivel intermedio.

En este artículo, se proporciona un tutorial para crear aplicaciones móviles con Xamarin y Azure Cosmos DB. Puede encontrar el código fuente completo de hello para el tutorial de hello en [Xamarin y base de datos de Azure Cosmos en GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin), incluida la forma toomanage usuarios y permisos.

## <a name="azure-cosmos-db-capabilities-for-mobile-apps"></a>Funcionalidades de Azure Cosmos DB para aplicaciones móviles
Base de datos de Azure Cosmos proporciona Hola sigue capacidades clave para los desarrolladores de aplicaciones móviles:

![Funcionalidades de Azure Cosmos DB para aplicaciones móviles](media/mobile-apps-with-xamarin/documentdb-for-mobile.png)

* Consultas completas sobre datos sin esquema. Azure Cosmos DB almacena datos como documentos JSON sin esquema en colecciones heterogéneas. Ofrece [consultas enriquecidas y rápidas](documentdb-sql-query.md) sin Hola que tooworry sobre esquemas o índices.
* Rendimiento rápido. Tarda solo unos pocos milisegundos tooread y escribir documentos con la base de datos de Azure Cosmos. Los desarrolladores pueden especificar que necesitan el rendimiento de Hola y base de datos de Azure Cosmos se respeta con SLA del 99,99%.
* Escala ilimitada. Las colecciones de Azure Cosmos DB [crecen a medida que la aplicación crece](partition-data.md). Puede empezar con un tamaño de datos pequeño y el rendimiento de cientos de solicitudes por segundo. Las colecciones pueden crecer toopetabytes de datos y el rendimiento arbitrariamente grande con centenares de millones de solicitudes por segundo.
* Distribución global. Aplicación móvil de los usuarios están en hello vaya, a menudo a través de Hola a todos. Azure Cosmos DB es una [base de datos distribuida globalmente](distribute-data-globally.md). Haga clic en hello mapa toomake los usuarios de tooyour puede tener acceso de datos.
* Autorización completa integrada. Con Azure Cosmos DB, puede implementar fácilmente patrones conocidos como [datos por usuario](https://aka.ms/documentdb-xamarin-todouser) o datos compartidos por varios usuarios sin un código de autorización personalizado complejo.
* Consultas geoespaciales. Muchas aplicaciones móviles ofrecen en la actualidad experiencias en contexto geográfico. Con el soporte de primera clase para [geospatial tipos](geospatial.md), facilita la base de datos de Azure Cosmos creación estos tooaccomplish fácil experiencias.
* Datos adjuntos binarios. Los datos de aplicaciones a menudo incluyen blobs binarios. Compatibilidad nativa para los datos adjuntos hace más fácil toouse base de datos de Azure Cosmos como una tienda integral para los datos de aplicación.

## <a name="azure-cosmos-db-and-xamarin-tutorial"></a>Tutorial sobre Xamarin y Azure Cosmos DB
Hola siguiendo el tutorial se muestra cómo una aplicación móvil con Xamarin y base de datos de Azure Cosmos toobuild. Puede encontrar el código fuente completo de hello para el tutorial de hello en [Xamarin y base de datos de Azure Cosmos en GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin).

### <a name="get-started"></a>Primeros pasos
Es fácil tooget a trabajar con la base de datos de Azure Cosmos. Vaya toohello portal de Azure y crear una nueva cuenta de base de datos de Azure Cosmos. Haga clic en hello **inicio rápido** ficha. Descarga Xamarin Forms tareas lista muestra de Hola que ya está había conectado tooyour cuenta de base de datos de Azure Cosmos. 

![Inicio rápido de Azure Cosmos DB para aplicaciones móviles](media/mobile-apps-with-xamarin/cosmos-db-quickstart.png)

O bien si tiene una aplicación Xamarin existente, puede agregar hello [paquete NuGet de base de datos de Azure Cosmos](documentdb-sdk-dotnet-core.md). Azure Cosmos DB admite bibliotecas compartidas de Xamarin.IOS, Xamarin.Android y Xamarin Forms.

### <a name="work-with-data"></a>Trabajar con datos
Los registros de datos se almacenan en Azure Cosmos DB como documentos JSON sin esquema en colecciones heterogéneas. Puede almacenar documentos con distintas estructuras en hello misma colección:

```cs
    var result = await client.CreateDocumentAsync(collectionLink, todoItem);
```

En sus proyectos de Xamarin puede usar Language-Integrated Queries sobre datos sin esquema:

```cs
    var query = await client.CreateDocumentQuery<ToDoItem>(collectionLink)
                    .Where(todoItem => todoItem.Complete == false)
                    .AsDocumentQuery();

    Items = new List<TodoItem>();
    while (query.HasMoreResults) {
        Items.AddRange(await query.ExecuteNextAsync<TodoItem>());
    }
```
### <a name="add-users"></a>Agregar usuarios
Al igual que muchas obtener ejemplos de introducción, ejemplo de Hola a base de datos de Azure Cosmos descargó autentica toohello servicio mediante el uso de una clave maestra codificado en el código de la aplicación hello. Este valor predeterminado no es una buena práctica para una aplicación que piensa toorun en cualquier lugar excepto en el emulador local. Si un usuario no autorizado obtenido la clave maestra de hello, todos los datos de hello en la cuenta de base de datos de Azure Cosmos pudieron verse comprometidos. En su lugar, desea que su aplicación tooaccess Hola solo registros de usuario que inició sesión Hola. Base de datos de Azure Cosmos permite a los desarrolladores toogrant aplicación de lectura o lectura/escritura tooa colección de permisos, un conjunto de documentos agrupados por una clave de partición o un documento específico. 

Siga estos pasos toomodify Hola tareas lista aplicación tooa tareas multiusuario lista de aplicaciones: 

  1. Agregar aplicación de tooyour de inicio de sesión con Facebook, Active Directory o cualquier otro proveedor.

  2. Crear una colección de Azure Cosmos DB UserItems con **/userId** como clave de partición de Hola. Especificar clave de partición de hello para la colección permite tooscale de base de datos de Azure Cosmos infinitamente como número de Hola de los usuarios de aplicación aumenta, mientras continúa toooffer rápido consultas.

  3. Agregue Resource Token Broker de Azure Cosmos DB. Esta API Web simple autentica a los usuarios y emite tokens de corta duración toosigned en los usuarios con acceso a documentos de toohello solo dentro de su partición. En este ejemplo, Resource Token Broker está hospedado en App Service.

  4. Modificar Hola aplicación tooauthenticate tooResource Broker Token con Facebook y solicitar tokens de recursos de Hola Hola firmado en Facebook a los usuarios. A continuación, puede tener acceso a sus datos en hello UserItems colección.  

Puede encontrar un código de ejemplo completo de este patrón en [Resource Token Broker en Github](http://aka.ms/documentdb-xamarin-todouser). Este diagrama muestra la solución de hello:

![Agente de permisos y usuarios de Azure Cosmos DB](media/mobile-apps-with-xamarin/documentdb-resource-token-broker.png)

Si desea que dos usuarios toohave acceso toohello misma lista de tareas pendientes, puede agregar token de acceso de toohello de permisos adicionales en el agente de Token de recurso.

### <a name="scale-on-demand"></a>Escalado a petición
Azure Cosmos DB es una base de datos como servicio administrada. A medida que crece su base de usuarios, no es necesario tooworry sobre el aprovisionamiento de máquinas virtuales o un aumento núcleos. Todo lo que necesita tootell base de datos de Azure Cosmos es necesario de la aplicación de cuántas operaciones por segundo (rendimiento). Puede especificar el rendimiento a través de Hola Hola **escala** ficha mediante el uso de una medida de rendimiento denominado unidades de solicitud (RUs) por segundo. Por ejemplo, una operación de lectura en un documento de 1 KB requiere 1 RU. También puede agregar alertas toohello **rendimiento** toomonitor métrica Hola aumento del tráfico y cambiar mediante programación el rendimiento de hello como alertas de incendios.

![Rendimiento a gran escala de Azure Cosmos DB a petición](media/mobile-apps-with-xamarin/cosmos-db-xamarin-scale.png)

### <a name="go-planet-scale"></a>Escala a nivel mundial
Como la popularidad de mejoras de aplicación, podría obtener los usuarios en todo el mundo de Hola. O tal vez desee toobe preparado para eventos imprevistos. Vaya toohello portal de Azure y abrir la cuenta de base de datos de Azure Cosmos. Haga clic en hello mapa toomake el número de tooany continuamente replicar datos de regiones a través de Hola a todos. Esta funcionalidad permite que los datos estén disponibles siempre que los usuarios lo estén. También puede agregar toobe de directivas de conmutación por error preparado para contingencias.

![Azure Cosmos DB escala en regiones geográficas](media/mobile-apps-with-xamarin/cosmos-db-xamarin-replicate.png)

¡Enhorabuena! Se ha completado la solución de Hola y dispongan de una aplicación móvil con Xamarin y base de datos de Azure Cosmos. Siga las aplicaciones de Cordova de toobuild pasos similares mediante Hola SDK de JavaScript de base de datos de Azure Cosmos y aplicaciones nativas de iOS y Android mediante el uso de API de REST de base de datos de Azure Cosmos.

## <a name="next-steps"></a>Pasos siguientes
* Ver código fuente de Hola de [Xamarin y base de datos de Azure Cosmos en GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin).
* Descargar hello [Azure Cosmos DB .NET Core SDK](documentdb-sdk-dotnet-core.md).
* Encuentre más ejemplos de código para [aplicaciones .NET](documentdb-dotnet-samples.md).
* Aprenda sobre las [funcionalidades de consultas completas de Azure Cosmos DB](documentdb-sql-query.md).
* Aprenda sobre la [compatibilidad geoespacial en Azure Cosmos DB](geospatial.md).



