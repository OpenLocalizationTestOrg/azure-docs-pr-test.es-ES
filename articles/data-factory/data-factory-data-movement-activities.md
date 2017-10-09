---
title: aaaMove datos mediante el uso de la actividad de copia | Documentos de Microsoft
description: "Aprenda sobre el movimiento de datos en las canalizaciones de Data Factory: migración de datos entre almacenes en la nube, entre un almacén de datos local y un almacén de datos en la nube. Utilice la actividad de copia."
keywords: "copiar datos, movimiento de datos, migración de datos, transferir datos"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 67543a20-b7d5-4d19-8b5e-af4c1fd7bc75
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: 29b74154b9006795ead3b0ee9638a3dbf2c5d831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-by-using-copy-activity"></a>Movimiento de datos con la actividad de copia
## <a name="overview"></a>Información general
En Data Factory de Azure, puede usar datos de actividad de copia toocopy entre local y nube almacenes de datos. Después de copiar los datos de hello, se puede obtener más transformar y analizan. También puede utilizar la transformación de toopublish de actividad de copia y resultados del análisis para business intelligence (BI) y consumo de la aplicación.

![Rol de actividad de copia](media/data-factory-data-movement-activities/copy-activity.png)

La actividad de copia se basa en un [servicio globalmente disponible](#global)que es seguro, confiable y escalable. Este artículo proporciona detalles sobre el movimiento de datos en Data Factory y en la actividad de copia.

En primer lugar, veamos cómo se produce la migración de datos entre dos almacenes de datos en la nube, entre un almacén de datos local y un almacén de datos en la nube.

> [!NOTE]
> en general, vea toolearn acerca de las actividades [descripción canalizaciones y actividades](data-factory-create-pipelines.md).
>
>

### <a name="copy-data-between-two-cloud-data-stores"></a>Copia de datos entre dos almacenes de datos en la nube
Cuando almacenes de datos de origen y receptor se encuentran en la nube hello, actividad de copia se pasa por hello siguientes datos toocopy de fases de receptor de hello origen toohello. servicio de Hola que alimenta actividad de copia:

1. Lee los datos de almacén de datos de origen de Hola.
2. Realiza procesos de serialización y deserialización, compresión y descompresión, asignación de columnas, y conversión de tipos. Hace que estas operaciones basadas en configuraciones de Hola de conjunto de datos de entrada de hello, conjunto de datos de salida y la actividad de copia.
3. Escribe datos toohello almacén de datos de destino.

servicio de Hello elige automáticamente el movimiento de datos de hello región óptimo tooperform Hola. Esta región suele ser Hola uno más cercano toohello receptor almacén de datos.

![Copia de la nube a la nube](./media/data-factory-data-movement-activities/cloud-to-cloud.png)

### <a name="copy-data-between-an-on-premises-data-store-and-a-cloud-data-store"></a>Copia de datos entre un almacén de datos local y un almacén de datos en la nube
toosecurely mover datos entre un almacén de datos local y un almacén de datos en la nube, instalar Data Management Gateway en su equipo local. Data Management Gateway es un agente que permite procesar y mover datos híbridos. Puede instalarlo en hello mismo equipo como el propio almacén de datos de hello, o en un equipo independiente que tenga acceso a los datos toohello almacenar.

En este escenario, Data Management Gateway lleva a cabo Hola serialización/deserialización, la compresión y descompresión, la asignación de columna y conversión de tipos. Datos no fluyen a través de hello servicio Data Factory de Azure. En su lugar, Data Management Gateway se escriben directamente en almacén de destino de hello datos toohello.

![Copia de entorno local a la nube](./media/data-factory-data-movement-activities/onprem-to-cloud.png)

Consulte [Movimiento de datos entre orígenes locales y la nube con Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) para ver una introducción y un tutorial. Consulte el artículo sobre [Data Management Gateway](data-factory-data-management-gateway.md) para obtener información detallada sobre esta agente.

También puede mover datos desde / almacenes de datos de toosupported que se hospedan en máquinas virtuales de IaaS de Azure (VM) mediante el uso de Data Management Gateway. En este caso, puede instalar Data Management Gateway en Hola misma máquina virtual como el propio almacén de datos de hello, o en una máquina virtual independiente que tenga acceso a los datos toohello almacenar.

## <a name="supported-data-stores-and-formats"></a>Almacenes de datos y formatos que se admiten
Actividad de copia de factoría de datos copia datos de un almacén de datos de origen datos almacén tooa receptor. Factoría de datos admite Hola siguientes almacenes de datos. Se pueden escribir datos de cualquier origen tooany receptor. Haga clic en un toolearn de almacén de datos cómo toocopy tooand de datos de ese almacén.

> [!NOTE] 
> Si necesita datos de toomove hacia/desde un almacén de datos que no es compatible con actividad de copia, utilice un **actividad personalizada** de factoría de datos con su propia lógica para copiar o mover los datos. Consulte el artículo [Uso de actividades personalizadas en una canalización de Data Factory de Azure](data-factory-use-custom-activities.md)para obtener más información sobre la creación y el uso de una actividad personalizada.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> Almacenes de datos con * puede ser local o en IaaS de Azure y requieren tooinstall [Data Management Gateway](data-factory-data-management-gateway.md) en una máquina de IaaS en local o de Azure.

### <a name="supported-file-formats"></a>Formatos de archivos admitidos
Puede usar la actividad de copia demasiado**copiar archivos como-es** entre los almacenes de datos basados en archivos de dos, puede omitir hello [formato sección](data-factory-create-datasets.md) en Hola entrada tanto las definiciones de conjunto de datos de salida. datos de Hola se copian de forma eficaz sin ninguna serialización/deserialización.

Actividad de copia también lee y escribe toofiles en formatos especificados: **texto, JSON, Avro, ORC y Parquet**y un códec de compresión **GZip, Deflate, BZip2 y ZipDeflate** son compatibles. Consulte [Formatos de archivo y de compresión admitidos](data-factory-supported-file-and-compression-formats.md) para más información.

Por ejemplo, puede hacer siguiente Hola copia actividades:

* Copiar datos en el servidor local de SQL y escribir tooAzure almacén de Data Lake en formato ORC.
* Copiar archivos en formato de texto (CSV) de sistema de archivos local y escribir tooAzure Blob en el formato Avro.
* Copiar archivos comprimidos de sistema de archivos local y descomprimir y dirigirán tooAzure almacén de Data Lake.
* Copiar datos en formato de texto comprimido (CSV) de GZip de Blob de Azure y escribir tooAzure base de datos SQL.

## <a name="global"></a>Movimiento de datos disponible globalmente
Factoría de datos de Azure solo está disponible en hello oeste de EE. UU, regiones y Europa del Norte. Sin embargo, el servicio de Hola que alimenta actividad de copia está disponible globalmente en hello siguiendo las regiones y zonas geográficas. topología disponibles globalmente Hola garantiza el movimiento de datos eficaz que normalmente evita saltos entre regiones. Consulte la sección [Servicios por región](https://azure.microsoft.com/regions/#services) para conocer la disponibilidad de Data Factory y el movimiento de datos en una región.

### <a name="copy-data-between-cloud-data-stores"></a>Copia de datos entre almacenes de datos en la nube
Cuando los almacenes de datos de origen y el receptor en la nube de hello, factoría de datos utiliza una implementación de servicio de región de Hola que es más cercano receptor toohello Hola mismos datos de geography toomove Hola. Consulte toohello para la asignación en la tabla siguiente:

| Geography de almacenes de datos de destino de Hola | Región del almacén de datos de destino de Hola | Región usada para el movimiento de datos |
|:--- |:--- |:--- |
| Estados Unidos | Este de EE. UU. | Este de EE. UU. |
| &nbsp; | Este de EE. UU. 2 | Este de EE. UU. 2 |
| &nbsp; | Central EE. UU.: | Central EE. UU.: |
| &nbsp; | Centro-Norte de EE. UU | Centro-Norte de EE. UU |
| &nbsp; | Centro-Sur de EE. UU | Centro-Sur de EE. UU |
| &nbsp; | Centro occidental de EE.UU. | Centro occidental de EE.UU. |
| &nbsp; | Oeste de EE. UU. | Oeste de EE. UU. |
| &nbsp; | Oeste de EE. UU. 2 | Oeste de EE. UU. |
| Canadá | Este de Canadá | Centro de Canadá |
| &nbsp; | Centro de Canadá | Centro de Canadá |
| Brasil | Sur de Brasil | Sur de Brasil |
| Europa | Europa del Norte | Europa del Norte |
| &nbsp; | Europa occidental | Europa occidental |
| Reino Unido | Oeste de Reino Unido | Sur del Reino Unido |
| &nbsp; | Sur del Reino Unido | Sur del Reino Unido |
| Asia Pacífico | Sudeste asiático | Sudeste asiático |
| &nbsp; | Asia oriental | Sudeste asiático |
| Australia | Australia Oriental | Australia Oriental |
| &nbsp; | Sudeste de Australia | Sudeste de Australia |
| Japón | Este de Japón | Este de Japón |
| &nbsp; | Oeste de Japón | Este de Japón |
| India | India Central | India Central |
| &nbsp; | Oeste de la India | India Central |
| &nbsp; | Sur de la India | India Central |

Como alternativa, puede indicar explícitamente región Hola de toobe de servicio de factoría de datos usa tooperform Hola copia mediante la especificación de `executionLocation` propiedad en la actividad de copia `typeProperties`. Los valores admitidos para esta propiedad se muestran en la columna **Región usada para el movimiento de datos** anterior. Tenga en cuenta que los datos atraviesa dicha región a lo largo cable de Hola durante la copia. Por ejemplo, toocopy entre Azure almacena en Corea, puede especificar `"executionLocation": "Japan East"` tooroute a través de la región de Japón (vea [JSON de ejemplo](#by-using-json-scripts) como referencia).

> [!NOTE]
> Si la región Hola Hola destino del almacén de datos no está en la lista anterior o no detectables, de forma predeterminada actividad de copia se produce un error en lugar de pasar a través de una región alternativa, a menos que `executionLocation` se especifica. lista de regiones de Hello admitida se expandirán con el tiempo.
>

### <a name="copy-data-between-an-on-premises-data-store-and-a-cloud-data-store"></a>Copia de datos entre un almacén de datos local y un almacén de datos en la nube
Cuando se copian datos entre almacenes locales (o IaaS o máquinas virtuales de Azure) y almacenes en la nube, [Data Management Gateway](data-factory-data-management-gateway.md) realiza movimientos de datos en una máquina local o virtual. Hola datos no fluyen a través del servicio en nube de hello, Hola a menos que utilice hello [provisionalmente copia](data-factory-copy-activity-performance.md#staged-copy) capacidad. En este caso, los datos fluyan a través de hello almacenamiento de blobs de Azure de almacenamiento provisional antes de que se escriban en el almacén de datos del receptor de Hola.

## <a name="create-a-pipeline-with-copy-activity"></a>Creación de una canalización con actividad de copia
Puede crear una canalización con actividad de copia de dos maneras:

### <a name="by-using-hello-copy-wizard"></a>Mediante el uso de hello Asistente para copiar
Hola Asistente para copiar de factoría de datos le ayuda a toocreate una canalización con la actividad de copia. Esta canalización permite toocopy datos desde orígenes compatibles toodestinations *sin escribir JSON* definiciones de servicios vinculados, conjuntos de datos y las canalizaciones. Vea [Asistente para copiar de factoría de datos](data-factory-copy-wizard.md) para obtener más información acerca del Asistente para saludo.  

### <a name="by-using-json-scripts"></a>Mediante scripts de JSON
Puede usar el Editor de generador de datos en hello portal de Azure, Visual Studio o PowerShell de Azure toocreate una definición de JSON de una canalización (mediante la actividad de copia). A continuación, puede implementar canalización de hello toocreate de factoría de datos. Consulte [Tutorial: Uso de la actividad de copia en una canalización de Azure Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso.    

Las propiedades JSON (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades. Propiedades que están disponibles en hello `typeProperties` sección de actividad hello varían con cada tipo de actividad.

Para la actividad de copia, Hola `typeProperties` sección varía en función de tipos de Hola de orígenes y receptores. Haga clic en un origen/receptor Hola [admite orígenes y receptores](#supported-data-stores-and-formats) toolearn de la sección acerca de las propiedades de tipo que admite la actividad de copia de ese almacén de datos.

Este es un ejemplo de definición de JSON:

```json
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from Azure blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [
          {
            "name": "InputBlobTable"
          }
        ],
        "outputs": [
          {
            "name": "OutputSQLTable"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink"
          },
          "executionLocation": "Japan East"          
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2016-07-12T00:00:00Z",
    "end": "2016-07-13T00:00:00Z"
  }
}
```
conjunto de datos determina cuándo se ejecuta la actividad hello de salida de programación de Hola que se define en hello (por ejemplo: **diaria**, frecuencia como **día**y el intervalo como **1**). Hello actividad copia datos de un conjunto de datos de entrada (**origen**) conjunto de datos de salida de tooan (**receptor**).

Puede especificar más de un conjunto de datos de entrada tooCopy actividad. Únicamente son dependencias de hello tooverify usado antes de ejecuta la actividad hello. Sin embargo, solo los datos de Hola de hello primer conjunto de datos están el conjunto de datos de toohello copiada destino. Para obtener más información, vea [Programación y ejecución](data-factory-scheduling-and-execution.md).  

## <a name="performance-and-tuning"></a>Rendimiento y optimización
Vea hello [actividad de copia Guía de rendimiento y optimización](data-factory-copy-activity-performance.md), que describe los factores claves que afectan al rendimiento de Hola de movimiento de datos (actividad de copia) de factoría de datos de Azure. También se muestran Hola observado rendimiento durante las pruebas internas y se describe el rendimiento de Hola de toooptimize de varias maneras de actividad de copia.

## <a name="fault-tolerance"></a>Tolerancia a errores
De forma predeterminada, la actividad de copia detendrá copiar datos y devolver un error cuando se encuentran datos incompatibles entre el origen y el receptor; Aunque puede configurar explícitamente tooskip y las filas de registro Hola incompatible y solo copia los copia de datos compatibles toomake Hola se realizó correctamente. Vea hello [tolerancia de actividad de copia](data-factory-copy-activity-fault-tolerance.md) en más detalles.

## <a name="security-considerations"></a>Consideraciones sobre la seguridad
Vea hello [consideraciones de seguridad](data-factory-data-movement-security-considerations.md), que describe la infraestructura de seguridad que los servicios de movimiento de datos de Data Factory de Azure usan toosecure los datos.

## <a name="scheduling-and-sequential-copy"></a>Programación y copia secuencial
Consulte [Programación y ejecución](data-factory-scheduling-and-execution.md) para obtener información detallada sobre cómo funciona la programación y la ejecución en Data Factory. Es posible toorun varias operaciones de copia uno tras otro de forma secuencial/ordenados. Vea hello [copiar secuencialmente](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) sección.

## <a name="type-conversions"></a>Conversiones de tipos
Los diferentes almacenes de datos tienen sistemas con distintos tipos nativos. Actividad de copia realiza conversiones de tipos automática de tipos de toosink de tipos de origen con hello enfoque de dos pasos:

1. Convertir del tipo de .NET de tooa de tipos de origen nativo.
2. Convertir de un tipo de receptor nativo de tooa de tipo. NET.

asignación de Hola de un tipo de .NET de tooa de sistema de tipo nativo para un almacén de datos es en el artículo de almacén de datos respectivos Hola. (Haga clic en vínculo específico de Hola Hola [admite almacenes de datos](#supported-data-stores) tabla). Puede usar estos tipos de asignaciones toodetermine adecuados al crear las tablas, para que la actividad de copia se realiza conversiones de derecho de Hola.

## <a name="next-steps"></a>Pasos siguientes
* toolearn sobre Hola actividad de copia más, consulte [copiar los datos de almacenamiento de blobs de Azure tooAzure base de datos SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
* toolearn acerca de cómo mover datos desde un almacén de datos local datos almacén tooa en la nube, consulte [mover los datos de almacenes de datos local toocloud](data-factory-move-data-between-onprem-and-cloud.md).
