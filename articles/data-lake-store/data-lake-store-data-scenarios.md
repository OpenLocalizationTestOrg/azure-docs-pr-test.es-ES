---
title: "escenarios de aaaData relacionadas con el almacén de Data Lake | Documentos de Microsoft"
description: "Comprender Hola diferentes escenarios y herramientas con los datos que se pueden ingestión, procesar, descargado y visualizarán en un almacén de Data Lake"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 37409a71-a563-4bb7-bc46-2cbd426a2ece
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: caaa3979b8a2532089778c3e3db3c711714d3c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-data-lake-store-for-big-data-requirements"></a>Uso del Almacén de Azure Data Lake para requisitos de macrodatos
Hay cuatro fases principales en el procesamiento de macrodatos:

* Introducción de grandes cantidades de datos en un almacén de datos, en tiempo real o por lotes
* Procesamiento de datos de Hola
* Descarga de datos de Hola
* Visualización de los datos de Hola

En este artículo, nos centramos en estas fases con sentido tooAzure almacén de Data Lake toounderstand Hola opciones y herramientas disponible toomeet sus necesidades de grandes cantidades de datos.

## <a name="ingest-data-into-data-lake-store"></a>Introducción de datos en el Almacén de Data Lake
Esta sección resalta Hola orígenes diferentes de hello y datos de varias maneras en que pueden ser ingestión esos datos en una cuenta de almacén de Data Lake.

![Ingesta de datos en Data Lake Store](./media/data-lake-store-data-scenarios/ingest-data.png "Ingesta de datos en Data Lake Store")

### <a name="ad-hoc-data"></a>Datos ad-hoc
Representan conjuntos de datos más pequeños que se utilizan para la creación de un prototipo de una aplicación de macrodatos. Hay distintas formas de datos ad hoc ingesta según origen de Hola de datos de Hola.

| Origen de datos | Introducir mediante |
| --- | --- |
| Equipo local |<ul> <li>[Portal de Azure](/data-lake-store-get-started-portal.md)</li> <li>[Azure PowerShell](data-lake-store-get-started-powershell.md)</li> <li>[CLI multiplataforma de Azure 2.0](data-lake-store-get-started-cli-2.0.md)</li> <li>[Usar herramientas de Data Lake para Visual Studio](../data-lake-analytics/data-lake-analytics-data-lake-tools-get-started.md) </li></ul> |
| Blob de almacenamiento de Azure |<ul> <li>[Factoría de datos de Azure](../data-factory/data-factory-azure-datalake-connector.md)</li> <li>[herramienta AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)</li><li>[DistCp ejecutándose en un clúster de HDInsight](data-lake-store-copy-data-wasb-distcp.md)</li> </ul> |

### <a name="streamed-data"></a>Datos de streaming
Representa los datos que se pueden generar por diversos orígenes, como aplicaciones, dispositivos o sensores, entre otros. Estos datos los pueden introducir distintas herramientas en un Almacén de Data Lake. Estas herramientas normalmente se capturar y procesar los datos de hello en forma de evento por evento en tiempo real y, a continuación, escribir eventos de Hola en lotes en el almacén de Data Lake para que pueden procesarse aún más.

A continuación, se muestran las herramientas que se pueden usar:

* [Análisis de transmisiones de Azure](../stream-analytics/stream-analytics-data-lake-output.md) -eventos ingeridos en centros de eventos se pueden escribir tooAzure Data Lake con una salida de almacén de Azure Data Lake.
* [Aluvión de Azure HDInsight](../hdinsight/hdinsight-storm-write-data-lake-store.md) -pueda escribir datos directamente tooData Lake almacén de Hola clúster de Storm.
* [EventProcessorHost](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md) : puede recibir eventos de centros de eventos y, a continuación, escribir, tooData Lake almacén con hello [SDK de .NET de almacén de Data Lake](data-lake-store-get-started-net-sdk.md).

### <a name="relational-data"></a>Datos relacionales
También se pueden originar datos desde bases de datos relacionales. Durante un tiempo, las bases de datos relacionales recopilan grandes cantidades de datos que pueden proporcionar información clave si se procesan a través de una canalización de macrodatos. Puede usar Hola después herramientas toomove estos datos en el almacén de Data Lake.

* [Apache Sqoop](data-lake-store-data-transfer-sql-sqoop.md)
* [Factoría de datos de Azure](../data-factory/data-factory-data-movement-activities.md)

### <a name="web-server-log-data-upload-using-custom-applications"></a>Datos de registro de servidor web (carga mediante aplicaciones personalizadas)
Este tipo de conjunto de datos es especialmente importante, ya análisis de datos de registro de servidor web es un caso de uso común para las aplicaciones de grandes cantidades de datos y requiere grandes volúmenes de toobe de archivos de registro cargan toohello almacén de Data Lake. Puede usar cualquiera de hello después herramientas toowrite su propio tooupload scripts o aplicaciones dichos datos.

* [CLI multiplataforma de Azure 2.0](data-lake-store-get-started-cli-2.0.md)
* [Azure PowerShell](data-lake-store-get-started-powershell.md)
* [SDK para .NET del Almacén de Azure Data Lake](data-lake-store-get-started-net-sdk.md)
* [Factoría de datos de Azure](../data-factory/data-factory-data-movement-activities.md)

Para cargar los datos de registro de servidor web y también para cargar otros tipos de datos (por ejemplo, datos de mensajes sociales), es un buen enfoque toowrite sus propias secuencias de comandos o aplicaciones personalizadas porque ofrece Hola flexibilidad tooinclude los datos de componente como parte de carga de la aplicación de grandes cantidades de datos más grande. En algunos casos este código puede tener formato de Hola de una secuencia de comandos o la utilidad de línea de comandos simple. En otros casos, el código de hello puede ser usado toointegrate de procesamiento de datos grande en una aplicación de negocios o solución.

### <a name="data-associated-with-azure-hdinsight-clusters"></a>Datos asociados con los clústeres de HDInsight de Azure
La mayoría de los tipos de clúster de HDInsight (Hadoop, HBase, Storm) admiten el Almacén de Data Lake como un repositorio de almacenamiento de datos. Los clústeres de HDInsight acceden a los datos de blobs de Almacenamiento de Azure (WASB). Para mejorar el rendimiento, puede copiar datos de Hola de WASB en una cuenta de almacén de Data Lake asociada Hola clúster. Puede usar Hola herramientas toocopy Hola datos siguientes.

* [Apache DistCp](data-lake-store-copy-data-wasb-distcp.md)
* [Servicio de AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)
* [Factoría de datos de Azure](../data-factory/data-factory-azure-datalake-connector.md)

### <a name="data-stored-in-on-premises-or-iaas-hadoop-clusters"></a>Datos almacenados en clústeres locales o de IaaS de Hadoop
Es posible que haya grandes cantidades de datos almacenados en clústeres de Hadoop existentes, de forma local en los equipos mediante HDFS. clústeres de Hadoop de Hello pueden estar en una implementación local o pueden estar dentro de un clúster de IaaS en Azure. Podría haber requisitos toocopy tal datos tooAzure almacén de Data Lake un enfoque de uso único o de forma periódica. Hay varias opciones que puede usar tooachieve esto. A continuación se muestra una lista de alternativas y Hola asociadas ventajas e inconvenientes.

| Enfoque | Detalles | Ventajas | Consideraciones |
| --- | --- | --- | --- |
| Usar datos de toocopy de factoría de datos de Azure (ADF) directamente desde el almacén de Hadoop clústeres tooAzure Data Lake |[ADF admite HDFS como origen de datos](../data-factory/data-factory-hdfs-connector.md) |ADF proporciona compatibilidad inmediata con HDFS, así como una supervisión y administración integrales y de primera clase. |Requiere la implementación de Data Management Gateway toobe local o en clúster de IaaS de Hola |
| Exportar datos desde Hadoop como archivos. A continuación, copie Hola archivos tooAzure almacén de Data Lake mediante mecanismo adecuado. |Puede copiar archivos tooAzure almacén de Data Lake mediante: <ul><li>[Azure PowerShell para SO Windows](data-lake-store-get-started-powershell.md)</li><li>[CLI multiplataforma de Azure 2.0 para sistemas operativos distintos de Windows](data-lake-store-get-started-cli-2.0.md)</li><li>Aplicación personalizada con cualquier SDK de Data Lake Store</li></ul> |Se inició el tooget rápido. Se pueden usar cargas personalizadas. |Proceso de varios pasos en el que participan varias tecnologías. Administración y supervisión crecerá toobe un desafío sobre la naturaleza de saludo personalizado de tiempo proporcionado de herramientas de Hola |
| Usar datos de toocopy de Distcp de Hadoop tooAzure almacenamiento. A continuación, copie datos almacenamiento tooData Lake del almacén de Azure mediante el mecanismo adecuado. |Puede copiar los datos de almacén de Azure almacenamiento tooData Lake utilizando: <ul><li>[Factoría de datos de Azure](../data-factory/data-factory-data-movement-activities.md)</li><li>[herramienta AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)</li><li>[Apache DistCp ejecutándose en clústeres de HDInsight](data-lake-store-copy-data-wasb-distcp.md)</li></ul> |Puede usar herramientas de código abierto. |Proceso de varios pasos en el que participan varias tecnologías. |

### <a name="really-large-datasets"></a>Conjuntos de datos realmente grandes
Para cargar los conjuntos de datos que varían en varios terabytes, mediante métodos de hello descritos anteriormente a veces puede lenta y costosa. En tales casos, puede usar opciones de hello siguientes.

* **Uso de Azure ExpressRoute**. Azure ExpressRoute permite crear conexiones privadas entre los centros de datos de Azure y la infraestructura de un entorno local. Esto ofrece una opción confiable para transferir grandes cantidades de datos. Para obtener más información, consulte la [documentación de Azure ExpressRoute](../expressroute/expressroute-introduction.md).
* **Carga "sin conexión" de los datos**. Si mediante ExpressRoute de Azure no es factible por cualquier motivo, puede usar [servicio de importación y exportación de Azure](../storage/common/storage-import-export-service.md) tooship unidades de disco duro con su centro de datos de Azure de tooan de datos. Los datos están la primera tooAzure cargado almacenamiento de Blobs. A continuación, puede usar [Data Factory de Azure](../data-factory/data-factory-azure-datalake-connector.md) o [AdlCopy herramienta](data-lake-store-copy-data-azure-storage-blob.md) datos toocopy almacenamiento de Blobs tooData Lake del almacén de Azure.

  > [!NOTE]
  > Mientras utilizando hello servicio de importación/exportación, tamaños de archivo de hello en hello del centro de discos que incluyen datos tooAzure no debe mayores 195 GB.
  >
  >

## <a name="process-data-stored-in-data-lake-store"></a>Procesamiento de los datos almacenados en el Almacén de Data Lake
Una vez que los datos de hello están disponibles en el almacén de Data Lake puede ejecutar análisis en que los datos mediante Hola admiten aplicaciones de grandes cantidades de datos. Actualmente, se pueden utilizar trabajos de análisis de datos toorun HDInsight de Azure y análisis de Azure Data Lake en datos de hello almacenados en el almacén de Data Lake.

![Análisis de datos en Data Lake Store](./media/data-lake-store-data-scenarios/analyze-data.png "Análisis de datos en Data Lake Store")

Puede mirar hello en los ejemplos siguientes.

* [Creación de un clúster de HDInsight con Almacén de Data Lake como almacenamiento](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Uso de Análisis de Azure Data Lake con el Almacén de Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md)

## <a name="download-data-from-data-lake-store"></a>Descarga de datos del Almacén de Data Lake
También puede tener toodownload o mover los datos de almacén de Azure Data Lake para escenarios como:

* Mover datos tooother repositorios toointerface con sus canalizaciones de procesamiento de datos existente. Por ejemplo, conviene toomove datos de almacén de Data Lake tooAzure base de datos SQL o SQL Server local.
* Descargar ordenador tooyour datos para su procesamiento en entornos de IDE durante la creación de prototipos de aplicación.

![Salida de datos de Data Lake Store](./media/data-lake-store-data-scenarios/egress-data.png "Salida de datos de Data Lake Store")

En tales casos, puede usar cualquiera de las siguientes opciones de hello:

* [Apache Sqoop](data-lake-store-data-transfer-sql-sqoop.md)
* [Factoría de datos de Azure](../data-factory/data-factory-data-movement-activities.md)
* [Apache DistCp](data-lake-store-copy-data-wasb-distcp.md)

También puede utilizar Hola siguiendo métodos toowrite sus propios datos de aplicación o script toodownload de almacén de Data Lake.

* [CLI multiplataforma de Azure 2.0](data-lake-store-get-started-cli-2.0.md)
* [Azure PowerShell](data-lake-store-get-started-powershell.md)
* [SDK para .NET del Almacén de Azure Data Lake](data-lake-store-get-started-net-sdk.md)

## <a name="visualize-data-in-data-lake-store"></a>Visualización de datos en el Almacén de Data Lake
Puede usar una mezcla de representaciones visuales de toocreate de servicios de datos almacenados en el almacén de Data Lake.

![Visualización de datos de Data Lake Store](./media/data-lake-store-data-scenarios/visualize-data.png "Visualización de datos de Data Lake Store")

* Puede iniciar mediante [datos de toomove Data Factory de Azure desde el almacén de Data Lake tooAzure almacenamiento de datos SQL](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats)
* Después de eso, también puede [integrar Power BI con almacenamiento de datos de SQL Azure](../sql-data-warehouse/sql-data-warehouse-integrate-power-bi.md) toocreate representación visual de los datos de Hola.
