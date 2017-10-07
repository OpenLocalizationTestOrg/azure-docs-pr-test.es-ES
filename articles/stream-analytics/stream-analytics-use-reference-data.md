---
title: "tablas de búsqueda y datos de referencia de aaaUse en análisis de transmisiones | Documentos de Microsoft"
description: "Uso de datos de referencia en una consulta de Análisis de transmisiones"
keywords: "tabla de búsqueda, datos de referencia"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 06103be5-553a-4da1-8a8d-3be9ca2aff54
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: fb1d18fba920db5e097d0c95d333e8e8390d1589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-reference-data-or-lookup-tables-in-a-stream-analytics-input-stream"></a>Uso de datos de referencia o tablas de consulta en una transmisión de entrada de Análisis de transmisiones
Datos de referencia (también conocido como una tabla de búsqueda) están un conjunto finito de datos que es estático o mermando cambiar por naturaleza, usó tooperform una búsqueda o toocorrelate con el flujo de datos. uso de toomake de datos de referencia en el trabajo de análisis de transmisiones de Azure, generalmente utilizará un [Join de datos de referencia](https://msdn.microsoft.com/library/azure/dn949258.aspx) en la consulta. Análisis de transmisiones usa almacenamiento de blobs de Azure como capa de almacenamiento de Hola para datos de referencia y con la referencia de la factoría de datos de Azure pueden ser almacenamiento de blobs de tooAzure transformado o copiado, para utilizarlos como datos de referencia, datos de [cualquier número de basado en la nube y almacenes de datos local](../data-factory/data-factory-data-movement-activities.md). Los datos de referencia se modelan como una secuencia de blobs (definidos en la configuración de entrada de Hola) en orden ascendente de hello fecha y hora especificado en nombre de blob de Hola. Se **sólo** admite la adición de toohello final de secuencia de hello mediante el uso de una fecha y hora **mayor** de Hola especificada en último blob de hello en secuencia Hola.

Análisis de transmisiones tiene un **límite de 100 MB por blob** pero trabajos pueden procesar varios blobs de referencia mediante hello **patrón de ruta de acceso** propiedad.


## <a name="configuring-reference-data"></a>Configuración de datos de referencia
tooconfigure los datos de referencia, primero debe toocreate una entrada que es de tipo **datos de referencia**. tabla de Hello siguiente explica cada propiedad que debe tooprovide al crear la entrada de datos de referencia de hello con su descripción:


<table>
<tbody>
<tr>
<td>Nombre de propiedad</td>
<td>Description</td>
</tr>
<tr>
<td>Alias de entrada</td>
<td>Un nombre descriptivo que se utilizarán en hello trabajo consulta tooreference esta entrada.</td>
</tr>
<tr>
<td>Cuenta de almacenamiento</td>
<td>nombre de Hola de cuenta de almacenamiento de Hola donde se encuentran los blobs. Si se encuentra en hello misma suscripción que su trabajo de análisis de secuencia, puede seleccionarlo en Hola de lista desplegable.</td>
</tr>
<tr>
<td>Clave de cuenta de almacenamiento</td>
<td>clave secreta de Hello asociado a la cuenta de almacenamiento de Hola. Esto se rellena automáticamente si es de cuenta de almacenamiento de Hola Hola misma suscripción que el trabajo de análisis de transmisiones.</td>
</tr>
<tr>
<td>Contenedor de almacenamiento</td>
<td>Los contenedores proporcionan una agrupación lógica para los blobs almacenados en hello servicio de blobs de Microsoft Azure. Al cargar un servicio de blob toohello, debe especificar un contenedor para dicho blob.</td>
</tr>
<tr>
<td>Patrón de la ruta de acceso</td>
<td>ruta de acceso de Hello usa toolocate los blobs en el contenedor especificado de Hola. En la ruta de acceso de hello, puede elegir toospecify una o más instancias de hello siguientes 2 variables:<BR>{date}, {time}<BR>Ejemplo 1: products/{date}/{time}/product-list.csv<BR>Ejemplo 2: products/{date}/product-list.csv
</tr>
<tr>
<td>Formato de fecha [opcional]</td>
<td>Si ha usado {date} en hello patrón de ruta de acceso especificada, puede seleccionar el formato de fecha de hello en el que se organizan los blobs en Hola de lista desplegable de los formatos admitidos.<BR>Ejemplo: AAAA/MM/DD, MM/DD/AAAA, etc.</td>
</tr>
<tr>
<td>Formato de hora [opcional]</td>
<td>Si ha usado {time} en hello patrón de ruta de acceso especificada, puede seleccionar el formato de hora de hello en el que se organizan los blobs en Hola de lista desplegable de los formatos admitidos.<BR>Ejemplo: HH, HH/mm o HH: mm</td>
</tr>
<tr>
<td>Formato de serialización de eventos</td>
<td>toomake seguro de que las consultas funcionan de forma de Hola que espera, análisis de transmisiones necesita tooknow el formato de serialización que está usando para las secuencias de datos entrantes. Para datos de referencia, los formatos de hello admitido son CSV y JSON.</td>
</tr>
<tr>
<td>Codificación</td>
<td>UTF-8 es Hola solo admite el formato de codificación en este momento</td>
</tr>
</tbody>
</table>

## <a name="generating-reference-data-on-a-schedule"></a>Generación de datos de referencia en una programación
Si los datos de referencia están un conjunto de datos de variación lenta, compatibilidad con la actualización de datos de referencia se habilita especificando un patrón de ruta de acceso en la configuración de entrada de hello mediante Hola {date} y tokens de sustitución de {time}. Análisis de transmisiones recoge las definiciones de datos de referencia Hola actualiza en función de este patrón de ruta de acceso. Por ejemplo, un patrón de `sample/{date}/{time}/products.csv` con un formato de fecha **"Aaaa-MM-DD"** y un formato de hora de **"HH: mm"** indica toopick de análisis de transmisiones de blob de hello actualiza `sample/2015-04-16/17-30/products.csv` a las 5:30 P.M. de abril zona horaria de 16, 2015 UTC.

> [!NOTE]
> Actualmente los trabajos de análisis de transmisiones buscan actualización de blob de Hola solo cuando el tiempo de máquina de hello adelanta el tiempo de toohello codificado en nombre de blob de Hola. Por ejemplo, buscará trabajo hello `sample/2015-04-16/17-30/products.csv` tan pronto como sea posible pero no antes de las 5:30 P.M. el 16 de abril de 2015 UTC zona horaria. Hará lo siguiente *nunca* busque un blob con un tiempo codificado anteriores a Hola última de ellas se detecta.
> 
> Por ejemplo, una vez que el trabajo Hola busca blob hello `sample/2015-04-16/17-30/products.csv` omitirá los archivos con una fecha codificado antes de las 5:30 P.M. el 16 de abril de 2015 por lo que si un tiempo de ejecución que llegan `sample/2015-04-16/17-25/products.csv` blob se crea en Hola mismo trabajo Hola de contenedor no se usará.
> 
> Del mismo modo si `sample/2015-04-16/17-30/products.csv` solo se genera a las 10:03 P.M. el 16 de abril de 2015, pero ningún blob con una fecha anterior está presente en el contenedor de hello, trabajo Hola usará este archivo a partir de 10:03 P.M. el 16 de abril de 2015 y utilizar datos de referencia anterior de hello hasta ese momento.
> 
> Un toothis de excepción es cuando trabajo Hola necesite toore procesar los datos en un momento o cuando se inicia por primera vez el trabajo de Hola. Al iniciar trabajo de temporizador Hola está buscando blob más reciente de Hola a producir antes de tiempo especificado de inicio del trabajo de Hola. Esto se hace tooensure que hay un **no vacía** referencia de conjunto de datos cuando se inicia el trabajo de Hola. Si no se encuentra uno, el trabajo de hello muestra hello después de diagnóstico: `Initializing input without a valid reference data blob for UTC time <start time>`.
> 
> 

[Factoría de datos de Azure](https://azure.microsoft.com/documentation/services/data-factory/) puede ser usado tooorchestrate Hola tarea de creación de blobs de hello actualizado requeridos por las definiciones de datos de referencia de análisis de transmisiones tooupdate. Factoría de datos es un servicio de integración de datos en la nube que organiza y automatiza el movimiento de Hola y la transformación de datos. Factoría de datos admite [conectar tooa muchos basado en la nube y almacenes de datos local](../data-factory/data-factory-data-movement-activities.md) y mover fácilmente los datos según una programación regular que especifique. Para obtener más información e instrucciones paso a paso sobre cómo tooset una una factoría de datos de canalización toogenerate los datos de referencia para el análisis de transmisiones que se actualiza según una programación predefinida, desproteja este [GitHub ejemplo](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ReferenceDataRefreshForASAJobs).

## <a name="tips-on-refreshing-your-reference-data"></a>Sugerencias sobre cómo actualizar los datos de referencia
1. Sobrescribiendo el BLOB de datos de referencia no provocará el análisis de transmisiones tooreload Hola blob y en algunos casos puede provocar hello toofail de trabajo. Hola recomienda datos de referencia de manera toochange es tooadd un nuevo blob mediante el mismo patrón de contenedor y ruta de acceso definido en la entrada de trabajo de Hola de Hola y use una fecha y hora **mayor** de Hola especificada en último blob de hello en secuencia Hola.
2. Los blobs de datos de referencia son **no** ordenados por hora "Última modificación" del blob de Hola pero solo por fecha especificada en nombre de blob de hello mediante Hola {date} y las sustituciones de {time} y Hola.
3. En algunas ocasiones, un trabajo debe retroceder en el tiempo, por lo que los blobs de datos de referencia no se deben modificar ni eliminar.

## <a name="get-help"></a>Obtener ayuda
Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Pasos siguientes
Ha estado tooStream se ha introducido el análisis, un servicio administrado para analizar los datos de Internet de las cosas Hola de transmisión por secuencias. toolearn más información acerca de este servicio, vea:

* [Introducción al uso de Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalación de trabajos de Análisis de transmisiones de Azure](stream-analytics-scale-jobs.md)
* [Referencia del lenguaje de consulta de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.get.started]: stream-analytics-get-started.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
