---
title: aaaAzure Cosmos DB Node.js API, SDK y recursos | Documentos de Microsoft
description: "Infórmese acerca de hello Node.js API y SDK, incluidas las fechas de lanzamiento y fechas de retirada, los cambios realizados entre cada versión de SDK de Node.js de base de datos de Azure Cosmos Hola."
services: cosmos-db
documentationcenter: nodejs
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 9d5621fa-0e11-4619-a28b-a19d872bcf37
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/14/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d450b9a9ea7b0f4717ddae8940121fc458ea3744
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-nodejs-sdk-release-notes-and-resources"></a>SDK de Node.js para Azure Cosmos DB: notas de la versión y recursos
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

<tr><td>**Descargar SDK**</td><td>[NPM](https://www.npmjs.com/package/documentdb)</td></tr>

<tr><td>**Documentación de la API**</td><td>[Documentación de referencia de la API de Node.js](http://azure.github.io/azure-documentdb-node/DocumentClient.html)</td></tr>

<tr><td>**Instrucciones de instalación del SDK**</td><td>[Instrucciones de instalación](http://azure.github.io/azure-documentdb-node/)</td></tr>

<tr><td>**Contribuir tooSDK**</td><td>[GitHub](https://github.com/Azure/azure-documentdb-node/tree/master/source)</td></tr>

<tr><td>**Ejemplos**</td><td>[Ejemplos de código Node.js](documentdb-nodejs-samples.md)</td></tr>

<tr><td>**Tutorial introductorio**</td><td>[Empezar a trabajar con hello SDK de Node.js](documentdb-nodejs-get-started.md)</td></tr>

<tr><td>**Tutorial de la aplicación web**</td><td>[Creación de una aplicación web de Node.js con Azure Cosmos DB](documentdb-nodejs-application.md)</td></tr>

<tr><td>**Plataforma admitida actualmente**</td><td> 
[Node.js v6.x](https://nodejs.org/en/blog/release/v6.10.3/)<br/> 
[Node.js v4.2.0](https://nodejs.org/en/blog/release/v4.2.0/)<br/> 
[Node.js v0.12](https://nodejs.org/en/blog/release/v0.12.0/)<br/> 
[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</td></tr>
</table></br>

## <a name="release-notes"></a>Notas de la versión

### <a name="1.12.2"/>1.12.2</a>
*   Documentación de NPM corregida.

### <a name="1.12.1"/>1.12.1</a>
* Se ha corregido un error en executeStoredProcedure en el que los documentos implicados tenían caracteres especiales de Unicode (LS, PS).
* Se ha corregido un error en el control de documentos con caracteres Unicode en la clave de partición de Hola.
* Compatibilidad fijo para crear colecciones con medios de nombre de Hola. Problema de GitHub n.º 114.
* Se ha corregido el problema de compatibilidad con el token de autorización de permiso. Problema de GitHub n.º 178.

### <a name="1.12.0"/>1.12.0</a>
* Se agregó compatibilidad con un nuevo [nivel de coherencia](consistency-levels.md) denominado ConsistentPrefix.
* Se agregó compatibilidad con UriFactory.
* Se ha corregido un error de compatibilidad con Unicode. Problema de GitHub n.º 171.

### <a name="1.11.0"/>1.11.0</a>
* Compatibilidad de hello agregados para consultas de agregación (COUNT, MIN, MAX, SUM y AVG).
* Opción de hello agregada para controlar el grado de paralelismo para entre las consultas de partición.
* Opción de hello agregada para deshabilitar la comprobación de SSL cuando se ejecuta en el emulador de base de datos de Azure Cosmos.
* Reducir el rendimiento mínimo en las colecciones particionadas de 10,100 RU/s too2500 RU/s.
* Error de token de continuación de hello fijo para la recopilación de una única partición. Problema de GitHub n.º 107.
* Error de executeStoredProcedure Hola fijo en el control de 0 como parámetro único. Problema de GitHub n.º 155.

### <a name="1.10.2"/>1.10.2</a>
* Versión del agente de usuario fijo encabezado tooinclude Hola SDK.
* Limpieza menor de código.

### <a name="1.10.1"/>1.10.1</a>
* Deshabilitar la comprobación de SSL al usar Hola SDK tootarget hello emulator(hostname=localhost).
* Se ha agregado compatibilidad para habilitar el registro de scripts durante la ejecución de procedimientos almacenados.

### <a name="1.10.0"/>1.10.0</a>
* Compatibilidad agregada con las consultas paralelas entre particiones.
* Se ha agregado compatibilidad con las consultas TOP y ORDER BY en las colecciones particionadas.

### <a name="1.9.0"/>1.9.0</a>
* Se ha agregado compatibilidad de la directiva de reintentos con las solicitudes de limitación. (Las solicitudes limitadas reciben una excepción demasiado grande de la tasa de solicitudes, código de error 429). De forma predeterminada, base de datos de Azure Cosmos reintenta nueve veces para cada solicitud cuando se encuentra el código de error 429, teniendo en cuenta el tiempo de retryAfter de hello en el encabezado de respuesta de Hola. Un tiempo de intervalo de reintento fijo ahora pueden establecer como parte del programa Hola propiedad RetryOptions en hello ConnectionPolicy objeto si desea tooignore hello retryAfter tiempo devuelto por servidor entre los reintentos de Hola. Base de datos de Azure Cosmos ahora espera durante un máximo de 30 segundos para cada solicitud que se está limitando (independientemente del número de reintentos) y devuelve la respuesta de hello con código de error 429. Esta vez también puede invalidarse en hello RetryOptions propiedad ConnectionPolicy objeto.
* COSMOS DB ahora devuelve x-ms-acelerador--número de reintentos y x-ms-throttle-retry-wait-time-ms como encabezados de respuesta de hello en cada Acelerador de saludo de solicitud toodenote tiempo de reintento hello y recuento acumulado Hola solicitar esperado entre reintentos de Hola.
* Hola RetryOptions clase se ha agregado, exposición hello RetryOptions propiedad en una clase ConnectionPolicy Hola que puede ser utilizado toooverride algunos predeterminado Hola opciones de reintento.

### <a name="1.8.0"/>1.8.0</a>
* Compatibilidad de hello agregada para cuentas de base de datos de varias regiones.

### <a name="1.7.0"/>1.7.0</a>
* Hola agregado compatibilidad con característica de tooLive(TTL) de tiempo para los documentos.

### <a name="1.6.0"/>1.6.0</a>
* Se han implementado [colecciones particionadas](partition-data.md) y [niveles de rendimiento definidos por el usuario](performance-levels.md).

### <a name="1.5.6"/>1.5.6</a>
* Corregido el error RangePartitionResolver.resolveForRead donde no devolvían vínculos debido tooa concat incorrecta de resultados.

### <a name="1.5.5"/>1.5.5</a>
* Valor hashParitionResolver resolveForRead() fijo: cuando ninguna clave de partición proporcionada lanzó una excepción, en lugar de devolver una lista de todos los vínculos registrados.

### <a name="1.5.4"/>1.5.4</a>
* Corrige el problema [&#100;](https://github.com/Azure/azure-documentdb-node/issues/100) -agente de HTTPS dedicado: evitar modificar global de los agentes Hola para fines de base de datos de Azure Cosmos. Usar a un agente dedicado para todas las solicitudes de lib Hola.

### <a name="1.5.3"/>1.5.3</a>
* Corrige el problema [81](https://github.com/Azure/azure-documentdb-node/issues/81) : controla correctamente guiones en identificadores de medios.

### <a name="1.5.2"/>1.5.2</a>
* Corrige el problema [95](https://github.com/Azure/azure-documentdb-node/issues/95) : advertencia de pérdida de escucha de EventEmitter.

### <a name="1.5.1"/>1.5.1</a>
* Corrige el problema [&#92;](https://github.com/Azure/azure-documentdb-node/issues/90) -cambiar el nombre de carpeta toohash de Hash para los sistemas entre mayúsculas y minúsculas.

### <a name="1.5.0"/>1.5.0</a>
* Se implementa la compatibilidad con el particionamiento, para lo que se agregan resolvedores de hash y de particiones de intervalo.

### <a name="1.4.0"/>1.4.0</a>
* Implementación de Upsert. Se han agregado nuevos métodos upsertXXX en documentClient.

### <a name="1.3.0"/>1.3.0</a>
* Omite los números de versión de toobring en consonancia con el resto de SDK.

### <a name="1.2.2"/>1.2.2</a>
* Preguntas de división promete repositorio toonew de contenedor.
* Actualizar toopackage archivo de registro de npm.

### <a name="1.2.1"/>1.2.1</a>
* Se implementa el enrutamiento por identificador.
* Corrige el problema [49](https://github.com/Azure/azure-documentdb-node/issues/49) : la propiedad current entra en conflicto con el método current().

### <a name="1.2.0"/>1.2.0</a>
* Se agregó compatibilidad con índice geoespacial.
* Valida la propiedad id para todos los recursos. Los identificadores de recursos no pueden contener los caracteres ?, /, #, &#47;&#47;, ni terminar con un espacio.
* Agrega el nuevo encabezado "curso de transformación de índice" tooResourceResponse.

### <a name="1.1.0"/>1.1.0</a>
* Implementación de la directiva de indexación V2.

### <a name="1.0.3"/>1.0.3</a>
* Problema [&#40;](https://github.com/Azure/azure-documentdb-node/issues/40) : implementa eslint y grunt configuraciones en el núcleo de Hola y promesa SDK.

### <a name="1.0.2"/>1.0.2</a>
* Problema [#45](https://github.com/Azure/azure-documentdb-node/issues/45) : el contenedor de objetos promise no incluye el encabezado con el error.

### <a name="1.0.1"/>1.0.1</a>
* Implementa tooquery capacidad si hay conflictos agregando readConflicts, readConflictAsync y queryConflicts.
* Documentación de la API actualizada.
* Problema [41](https://github.com/Azure/azure-documentdb-node/issues/41) : error client.createDocumentAsync.

### <a name="1.0.0"/>1.0.0</a>
* SDK de GA.

## <a name="release--retirement-dates"></a>Fechas de lanzamiento y de retirada
Microsoft proporciona una notificación al menos **12 meses** antes de retirar un SDK en la versión de más reciente admitida de orden toosmooth Hola transición tooa.

Nuevas características y funcionalidad y las optimizaciones se agregan solo toohello actual SDK, como por ejemplo, se recomienda que se realice siempre la actualización toohello última versión del SDK tan pronto como sea posible.

Cualquier solicitud tooCosmos base de datos con un SDK retirado es ser rechazados por el servicio de Hola.

<br/>

| Versión | Fecha de lanzamiento | Fecha de retirada |
| --- | --- | --- |
| [1.12.2](#1.12.2) |10 de agosto de 2017 |--- |
| [1.12.1](#1.12.1) |10 de agosto de 2017 |--- |
| [1.12.0](#1.12.0) |10 de mayo de 2017 |--- |
| [1.11.0](#1.11.0) |16 de marzo de 2017 |--- |
| [1.10.2](#1.10.2) |27 de enero de 2017 |--- |
| [1.10.1](#1.10.1) |22 de diciembre de 2016 |--- |
| [1.10.0](#1.10.0) |03 de octubre de 2016 |--- |
| [1.9.0](#1.9.0) |7 de julio de 2016 |--- |
| [1.8.0](#1.8.0) |14 de junio de 2016 |--- |
| [1.7.0](#1.7.0) |26 de abril de 2016 |--- |
| [1.6.0](#1.6.0) |29 de marzo de 2016 |--- |
| [1.5.6](#1.5.6) |8 de marzo de 2016 |--- |
| [1.5.5](#1.5.5) |2 de febrero de 2016 |--- |
| [1.5.4](#1.5.4) |1 de febrero de 2016 |--- |
| [1.5.2](#1.5.2) |26 de enero de 2016 |--- |
| [1.5.2](#1.5.2) |22 de enero de 2016 |--- |
| [1.5.1](#1.5.1) |4 de enero de 2016 |--- |
| [1.5.0](#1.5.0) |31 de diciembre de 2015 |--- |
| [1.4.0](#1.4.0) |6 de octubre de 2015 |--- |
| [1.3.0](#1.3.0) |6 de octubre de 2015 |--- |
| [1.2.2](#1.2.2) |10 de septiembre de 2015 |--- |
| [1.2.1](#1.2.1) |15 de agosto de 2015 |--- |
| [1.2.0](#1.2.0) |05 de agosto de 2015 |--- |
| [1.1.0](#1.1.0) |09 de julio de 2015 |--- |
| [1.0.3](#1.0.3) |4 de junio de 2015 |--- |
| [1.0.2](#1.0.2) |23 de mayo de 2015 |--- |
| [1.0.1](#1.0.1) |15 de mayo de 2015 |--- |
| [1.0.0](#1.0.0) |08 de abril de 2015 |--- |

## <a name="faq"></a>Preguntas más frecuentes
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>Otras referencias
toolearn más información acerca de la base de datos de Cosmos, consulte [base de datos de Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) página de servicio.

