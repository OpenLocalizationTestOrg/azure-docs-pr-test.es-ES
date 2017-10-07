---
title: "salida de aaaJSON para análisis de transmisiones | Documentos de Microsoft"
description: "Obtenga información sobre cómo Stream Analytics puede tener como destino Azure Cosmos DB para la salida de JSON, para el archivado de datos y las consultas de latencia baja en datos de JSON no estructurados."
keywords: Salida de JSON
documentationcenter: 
services: stream-analytics,documentdb
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 5d2a61a6-0dbf-4f1b-80af-60a80eb25dd1
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: fa717818c839ecd7a60fcee33d22011990fd5878
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="target-azure-cosmos-db-for-json-output-from-stream-analytics"></a>Tener como destino Azure Cosmos DB para la salida de JSON de Stream Analytics
Stream Analytics puede tener como destino [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) para la salida de JSON, habilitando el archivado de datos y las consultas de latencia baja en datos de JSON no estructurados. En este documento tratan algunas prácticas recomendadas para implementar esta configuración.

Para aquellos que no estén familiarizados con la base de datos de Cosmos, eche un vistazo a [ruta de acceso de aprendizaje de Azure Cosmos DB](https://azure.microsoft.com/documentation/learning-paths/documentdb/) tooget iniciado. 

Nota: las colecciones de Cosmos DB basadas en Mongo DB API no se admiten actualmente. 

## <a name="basics-of-cosmos-db-as-an-output-target"></a>Aspectos básicos de Cosmos DB como destino de salida
Hola salida de la base de datos de Azure Cosmos en análisis de transmisiones permite escribir la secuencia de resultados se procesan como salida JSON en sus colecciones de base de datos de Cosmos. Análisis de transmisiones no crear colecciones en la base de datos en su lugar, lo que requiere toocreate ellos por adelantado. Esto es para que los costes de facturación de Hola de colecciones de base de datos de Cosmos están tooyou transparente y, por lo que puede optimizar el rendimiento de hello, Hola coherencia y la capacidad de las colecciones directamente mediante [API de base de datos de Cosmos](https://msdn.microsoft.com/library/azure/dn781481.aspx). Se recomienda utilizar una base de datos de base de datos de Cosmos por streaming trabajo toologically independiente las colecciones para un trabajo de streaming.

A continuación se detallan algunas de las opciones de recopilación de Cosmos DB Hola.

## <a name="tune-consistency-availability-and-latency"></a>Ajustar la coherencia, la disponibilidad y la latencia
toomatch los requisitos de aplicación, base de datos de Cosmos permite base de datos de toofine ajustar hello y colecciones y asegúrese de ventajas y desventajas de coherencia, la disponibilidad y la latencia. En función de los niveles de coherencia de lectura que requiera su situación en comparación con la latencia de lectura y escritura, puede elegir un nivel de coherencia u otro en la cuenta de base de datos. También de forma predeterminada, Cosmos DB permite la indización sincrónico en cada colección de tooyour la operación CRUD. Se trata de Hola de toocontrol de otra opción útil rendimiento en la base de datos de Cosmos de lectura/escritura. Para obtener más información acerca de este tema, revise hello [cambiar los niveles de coherencia de base de datos y consultas](../documentdb/documentdb-consistency-levels.md) artículo.

## <a name="upserts-from-stream-analytics"></a>Upserts de Análisis de transmisiones
Integración del análisis de transmisiones con DB Cosmos permite tooinsert o actualizar registros en la colección de base de datos de Cosmos tomando como base una columna de identificador de documento determinada. Esto también es tooas que se hace referencia una *Upsert*.

Análisis de transmisiones usa un enfoque Upsert optimista, donde las actualizaciones solo se realizan cuando se produce un error en la inserción debido a conflictos de identificador de documento tooa. Esta actualización se realiza mediante el análisis de transmisiones como una revisión, por lo que hace que el documento de toohello actualizaciones parciales, es decir, la adición de nuevas propiedades o reemplazar que una propiedad existente se realiza de forma incremental. Tenga en cuenta que debido a cambios en valores de hello de propiedades de la matriz en el documento JSON en obtener sobrescribe toda matriz de hello, es decir, no se combina la matriz de Hola.

## <a name="data-partitioning-in-cosmos-db"></a>Creación de particiones de datos en Cosmos DB
COSMOS DB [particiones colecciones](../cosmos-db/partition-data.md) son Hola recomendada enfoque para crear particiones de los datos. 

Para las colecciones de base de datos de Cosmos únicas, análisis de transmisiones aún permite toopartition los datos se basan en patrones de consulta de Hola y necesidades de rendimiento de la aplicación. Cada colección puede contener una too10GB de datos (máximo) y actualmente que no hay ningún tooscale forma una (o desbordamiento) una colección. Para escalar horizontalmente, análisis de transmisiones permite toowrite toomultiple colecciones con un prefijo determinado (consulte los detalles de uso siguiente). Análisis de transmisiones usa Hola coherente [resolución de la partición de Hash](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.partitioning.hashpartitionresolver.aspx) estrategia basada en usuario Hola proporciona PartitionKey columna toopartition sus registros de salida. Hello número de colecciones con hello al Hola hora de inicio del trabajo de transmisión por secuencias proporcionadas prefijo se utiliza como recuento de particiones de salida de hello, trabajo de hello toowhich escribe tooin paralelo (colecciones de base de datos de Cosmos = particiones de salida). En el caso de una sola colección con una indexación diferida que realiza solo operaciones de inserción, se puede esperar en torno a 0,4 MB/s de rendimiento de escritura. El uso de varias colecciones permite tooachieve un mayor rendimiento y una mayor capacidad.

Si piensa recuento de particiones de tooincrease Hola Hola futuras, deberá toostop su trabajo, volver a particionar Hola datos de las colecciones existentes con nuevas recopilaciones y, a continuación, trabajo de análisis de transmisiones de Hola de reinicio. Se incluirá más información sobre el uso de PartitionResolver y la nueva creación de particiones junto con código de ejemplo en una publicación posterior. artículo de Hello [particiones y ajuste de escala en la base de datos de Cosmos](../documentdb/documentdb-partition-data.md) también proporciona detalles sobre esto.

## <a name="cosmos-db-settings-for-json-output"></a>Configuración de Cosmos DB para salida de JSON
La creación de Cosmos DB como una salida en Stream Analytics genera una solicitud de información, tal como se muestra a continuación. En esta sección se ofrece una explicación de la definición de propiedades de Hola.

Colección particionada | Varias colecciones de partición única
---|---
![pantalla de salida de análisis de transmisiones de documentdb](media/stream-analytics-documentdb-output/stream-analytics-documentdb-output-1.png) |  ![pantalla de salida de análisis de transmisiones de documentdb](media/stream-analytics-documentdb-output/stream-analytics-documentdb-output-2.png)


  
> [!NOTE]
> Hola **varias colecciones de "Única partición"** escenario requiere una clave de partición y es una configuración admitida. 

* **Alias de salida** – un toorefer alias este resultado de la consulta ASA  
* **Nombre de cuenta** : nombre de Hola o extremo URI de hello cuenta de base de datos de Cosmos.  
* **Clave de cuenta** : clave de acceso compartido de Hola para hello cuenta de base de datos de Cosmos.  
* **Base de datos** : nombre de base de datos de base de datos de Cosmos Hola.  
* **Patrón de nombre de colección** : nombre de la colección de Hola o su patrón de hello colecciones toobe usa. formato de nombre de colección de Hello puede crearse mediante token {partition} opcional de hello, donde se inician las particiones desde 0. Las siguientes entradas de ejemplo son válidas:  
  1\) MyCollection: debe existir una colección denominada "MyCollection".  
  2\) MyCollection{partición}: deben existir esas colecciones: "MyCollection0", "MyCollection1", "MyCollection2", etc.  
* **Clave de partición**: opcional. Solo es necesario si usa un token {partition} en el patrón de nombre de la colección. nombre de Hello del campo de hello en toospecify Hola clave de salida eventos que se usa para crear particiones de salida de todas las colecciones. Para una salida de colección sencilla, se puede utilizar cualquier columna de salida arbitraria (por ejemplo, PartitionId).  
* **Identificador de documento** : opcional. nombre de Hola de campo de hello en los eventos de salida utiliza la clave principal de toospecify hello en las instrucciones insert o update se basan las operaciones.  
