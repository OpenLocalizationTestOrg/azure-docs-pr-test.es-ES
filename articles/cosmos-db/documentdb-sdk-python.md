---
title: aaaAzure Cosmos DB Python API, SDK y recursos | Documentos de Microsoft
description: "Infórmese acerca de hello Python API y SDK, incluidas las fechas de lanzamiento y fechas de retirada, los cambios realizados entre cada versión de hello Azure Cosmos DB Python SDK."
services: cosmos-db
documentationcenter: python
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 3ac344a9-b2fa-4a3f-a4cc-02d287e05469
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/24/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1a164b72d2bd819de87df0229357b82e2177af2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-python-sdk-release-notes-and-resources"></a>SDK de Python para Azure Cosmos DB: notas de la versión y recursos
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

<tr><td>**Descargar SDK**</td><td>[PyPI](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td>**Documentación de la API**</td><td>[Documentación de referencia de la API de Python](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.html)</td></tr>

<tr><td>**Instrucciones de instalación del SDK**</td><td>[Instrucciones de instalación del SDK de Python](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td>**Contribuir tooSDK**</td><td>[GitHub](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td>**Introducción**</td><td>[Empezar a trabajar con hello SDK de Python](documentdb-python-application.md)</td></tr>

<tr><td>**Plataforma admitida actualmente**</td><td>[Python 2.7](https://www.python.org/downloads/) y [Python 3.5](https://www.python.org/downloads/)</td></tr>
</table></br>

## <a name="release-notes"></a>Notas de la versión
### <a name="a-name220220"></a><a name="2.2.0"/>2.2.0
* Se agregó compatibilidad con un nuevo nivel de coherencia denominado ConsistentPrefix.


### <a name="a-name210210"></a><a name="2.1.0"/>2.1.0
* Se agregó compatibilidad con consultas de agregación (COUNT, MIN, MAX, SUM y AVG).
* Se agregó una opción para deshabilitar la comprobación de SSL cuando se ejecuta en el emulador de Cosmos DB.
* Quitar restricción de Hola de las solicitudes dependientes módulo toobe 2.10.0 exactamente.
* Reducir el rendimiento mínimo en las colecciones particionadas de 10,100 RU/s too2500 RU/s.
* Se ha agregado compatibilidad para habilitar el registro de scripts durante la ejecución de procedimientos almacenados.
* Versión de API de REST demasiado incrementará ' 2017-01-19' con esta versión.

### <a name="a-name201201"></a><a name="2.0.1"/>2.0.1
* Realiza los cambios editoriales toodocumentation comentarios.

### <a name="a-name200200"></a><a name="2.0.0"/>2.0.0
* Compatibilidad agregada para Python 3.5.
* Compatibilidad agregada para agrupaciones de conexiones con un módulo de solicitudes.
* Compatibilidad agregada para la coherencia de la sesión.
* Compatibilidad agregada para consultas TOP/ORDERBY para colecciones particionadas.

### <a name="a-name190190"></a><a name="1.9.0"/>1.9.0
* Se ha agregado compatibilidad de la directiva de reintentos con las solicitudes de limitación. (Las solicitudes limitadas reciben una excepción demasiado grande de la tasa de solicitudes, código de error 429). De forma predeterminada, base de datos de Azure Cosmos reintenta nueve veces para cada solicitud cuando se encuentra el código de error 429, teniendo en cuenta el tiempo de retryAfter de hello en el encabezado de respuesta de Hola. Un tiempo de intervalo de reintento fijo ahora pueden establecer como parte del programa Hola propiedad RetryOptions en hello ConnectionPolicy objeto si desea tooignore hello retryAfter tiempo devuelto por servidor entre los reintentos de Hola. Base de datos de Azure Cosmos ahora espera durante un máximo de 30 segundos para cada solicitud que se está limitando (independientemente del número de reintentos) y devuelve la respuesta de hello con código de error 429. Esta vez también puede ser reemplazada en hello RetryOptions propiedad ConnectionPolicy objeto.
* COSMOS DB ahora devuelve x-ms-acelerador--número de reintentos y x-ms-throttle-retry-wait-time-ms como encabezados de respuesta de hello en cada Acelerador de saludo de solicitud toodenote tiempo de reintento hello y recuento cummulative Hola solicitar esperado entre reintentos de Hola.
* Clase de RetryPolicy de hello quitado y la propiedad correspondiente de hello (retry_policy) exponen en clase document_client de hello e introdujeron en su lugar una clase RetryOptions exposición hello RetryOptions propiedad en una clase ConnectionPolicy que puede ser utilizado toooverride Algunos predeterminado Hola opciones de reintento.

### <a name="a-name180180"></a><a name="1.8.0"/>1.8.0
* Compatibilidad de hello agregada para cuentas de base de datos de varias regiones.

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
* Hola agregado compatibilidad con característica de tooLive(TTL) de tiempo para los documentos.

### <a name="a-name161161"></a><a name="1.6.1"/>1.6.1
* Correcciones de errores relacionados con lado tooserver particiones tooallow caracteres especiales en la ruta de acceso de partitionkey.

### <a name="a-name160160"></a><a name="1.6.0"/>1.6.0
* Se han implementado [colecciones particionadas](partition-data.md) y [niveles de rendimiento definidos por el usuario](performance-levels.md). 

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0
* Agregar Hash & intervalo tooassist de resoluciones de partición con aplicaciones de particionamiento entre varias particiones.

### <a name="a-name142142"></a><a name="1.4.2"/>1.4.2
* Implementación de Upsert. Nuevos métodos de UpsertXXX agregan toosupport Upsert característica.
* Se implementa el enrutamiento por identificador. Sin cambios en la API pública, todos los cambios son internos.

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* Compatible con índice geoespacial.
* Valida la propiedad id para todos los recursos. Los identificadores de recursos no pueden contener los caracteres ?, /, #, \, ni terminar con un espacio.
* Agrega el nuevo encabezado "curso de transformación de índice" tooResourceResponse.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* Implementación de la directiva de indexación V2.

### <a name="a-name101101"></a><a name="1.0.1"/>1.0.1
* Compatibilidad con conexión de proxy.

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* SDK de GA.

## <a name="release--retirement-dates"></a>Fechas de lanzamiento y retirada
Microsoft proporcionará la notificación al menos **12 meses** antes de retirar un SDK en la versión de más reciente admitida de orden toosmooth Hola transición tooa.

Nuevas características y funcionalidad y las optimizaciones se agregan solo toohello actual SDK, por lo tanto, es recomendable que se realice siempre la actualización toohello última versión del SDK tan pronto como sea posible. 

Servicio de hello rechazará cualquier base de datos con un SDK retirado tooCosmos de solicitud.

> [!WARNING]
> Todas las versiones de hello documentos de Azure SDK para Python anterior tooversion **1.0.0** se retirarán en **29 de febrero de 2016**. 
> 
> 

<br/>

| Versión | Fecha de lanzamiento | Fecha de retirada |
| --- | --- | --- |
| [2.2.0](#2.2.0) |10 de mayo de 2017 |--- |
| [2.1.0](#2.1.0) |1 de mayo de 2017 |--- |
| [2.0.1](#2.0.1) |30 de octubre de 2016 |--- |
| [2.0.0](#2.0.0) |29 de septiembre de 2016 |--- |
| [1.9.0](#1.9.0) |7 de julio de 2016 |--- |
| [1.8.0](#1.8.0) |14 de junio de 2016 |--- |
| [1.7.0](#1.7.0) |26 de abril de 2016 |--- |
| [1.6.1](#1.6.1) |08 de abril de 2016 |--- |
| [1.6.0](#1.6.0) |29 de marzo de 2016 |--- |
| [1.5.0](#1.5.0) |3 de enero de 2016 |--- |
| [1.4.2](#1.4.2) |6 de octubre de 2015 |--- |
| [1.4.1](#1.4.1) |6 de octubre de 2015 |--- |
| [1.2.0](#1.2.0) |6 de agosto de 2015 |--- |
| [1.1.0](#1.1.0) |09 de julio de 2015 |--- |
| [1.0.1](#1.0.1) |25 de mayo de 2015 |--- |
| [1.0.0](#1.0.0) |07 de abril de 2015 |--- |
| 0.9.4-prelease |14 de enero de 2015 |29 de febrero de 2016 |
| 0.9.3-prelease |9 de diciembre de 2014 |29 de febrero de 2016 |
| 0.9.2-prelease |25 de noviembre de 2014 |29 de febrero de 2016 |
| 0.9.1-prelease |23 de septiembre de 2014 |29 de febrero de 2016 |
| 0.9.0-prelease |21 de agosto de 2014 |29 de febrero de 2016 |

## <a name="faq"></a>P+F
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>Otras referencias
toolearn más información acerca de la base de datos de Cosmos, consulte [base de datos de Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) página de servicio. 

