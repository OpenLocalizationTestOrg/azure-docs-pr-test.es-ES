---
title: "aaaIntegrating almacén de Data Lake con otros servicios de Azure | Documentos de Microsoft"
description: "Descripción de cómo se integra el Almacén de Data Lake con otros servicios de Azure"
documentationcenter: 
services: data-lake-store
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 48a5d1f4-3850-4c22-bbc4-6d1d394fba8a
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 839689f04623f8225884e7aa9c0b533a09323e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-data-lake-store-with-other-azure-services"></a>Integración del Almacén de Data Lake con otros servicios de Azure
Almacén de Data Lake de Azure puede utilizarse junto con otro tooenable una gama más amplia de escenarios de servicios de Azure. Hello artículo siguiente enumera los servicios de Hola que se puede integrar con almacén de Data Lake.

## <a name="use-data-lake-store-with-azure-hdinsight"></a>Uso del Almacén de Data Lake con Azure HDInsight
Puede aprovisionar un [HDInsight de Azure](https://azure.microsoft.com/documentation/learning-paths/hdinsight-self-guided-hadoop-training/) clúster que utiliza el almacén de Data Lake como almacenamiento Hola conforme a HDFS. Para esta versión, para los clústeres Hadoop y Storm en Windows y Linux, puede usar el Almacén de Data Lake solo como almacenamiento adicional. Clústeres como éstos seguir usando el almacenamiento de Azure (WASB) como almacenamiento predeterminado de Hola. Sin embargo, para los clústeres de HBase en Windows y Linux, puede usar el almacén de Data Lake como almacenamiento predeterminado de hello, o almacenamiento adicional o ambos.

Para obtener instrucciones sobre cómo tooprovision una HDInsight de clúster con el almacén de Data Lake, vea:

* [Aprovisionamiento de un clúster de HDInsight con el Almacén de Data Lake mediante el Portal de Azure](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Aprovisionamiento de un clúster de HDInsight con Data Lake Store como almacenamiento predeterminado mediante Azure PowerShell](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [Aprovisionamiento de un clúster de HDInsight con Data Lake Store como almacenamiento adicional mediante Azure PowerShell](data-lake-store-hdinsight-hadoop-use-powershell.md)

## <a name="use-data-lake-store-with-azure-data-lake-analytics"></a>Uso del Almacén de Data Lake con Análisis de Data Lake de Azure
[Análisis de Azure Data Lake](../data-lake-analytics/data-lake-analytics-overview.md) permite toowork con grandes cantidades de datos a escala de nube. Dinámicamente aprovisiona recursos y le permite realizar análisis en terabytes o incluso exabytes de datos que pueden almacenarse en un número de orígenes de datos admitidos, siendo uno de ellos el Almacén de Data Lake. Análisis de Data Lake es especialmente optimizado toowork con almacén de Azure Data Lake - proporcionar el nivel más alto de Hola de rendimiento, el rendimiento y la ejecución en paralelo para las cargas de trabajo grandes cantidades de datos.

Para obtener instrucciones sobre cómo ver toouse análisis de Data Lake con el almacén de Data Lake [empezar a trabajar con análisis de Data Lake con almacén de Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md).

## <a name="use-data-lake-store-with-azure-data-factory"></a>Uso del Almacén de Data Lake con Factoría de datos de Azure
Puede usar [Data Factory de Azure](https://azure.microsoft.com/services/data-factory/) tooingest datos de tablas de Azure, base de datos de SQL Azure, almacenamiento de datos de SQL Azure, Blobs de almacenamiento de Azure y las bases de datos local. Ser un ciudadano de primera clase en hello ecosistema de Azure, Data Factory de Azure puede ser usado tooorchestrate Hola ingesta de datos de estos tooAzure origen almacén de Data Lake.

Para obtener instrucciones sobre cómo toouse factoría de datos de Azure con el almacén de Data Lake, consulte [mover tooand de datos de almacén de Data Lake con factoría de datos](../data-factory/data-factory-azure-datalake-connector.md).

## <a name="copy-data-from-azure-storage-blobs-into-data-lake-store"></a>Copia de datos de los blobs de Almacenamiento de Azure en el Almacén de Data Lake
Almacén de Data Lake de Azure proporciona una herramienta de línea de comandos, AdlCopy, que permite toocopy datos desde almacenamiento de blobs de Azure en una cuenta de almacén de Data Lake. Para obtener más información, consulte [copiar los datos de almacén de Blobs de Azure almacenamiento Lake tooData](data-lake-store-copy-data-azure-storage-blob.md).

## <a name="copy-data-between-azure-sql-database-and-data-lake-store"></a>Copia de datos entre Base de datos SQL de Azure y Almacén de Data Lake
Puede usar tooimport Sqoop de Apache y exportar datos entre la base de datos de SQL Azure y almacén de Data Lake. Para más información, consulte [Copia de datos entre Almacén de Data Lake y Base de datos SQL de Azure mediante Sqoop](data-lake-store-data-transfer-sql-sqoop.md).

## <a name="use-data-lake-store-with-stream-analytics"></a>Uso del Almacén de Data Lake con Análisis de transmisiones
Puede usar el almacén de Data Lake como uno de hello genera datos toostore que se transmiten mediante el análisis de transmisiones de Azure. Para más información, consulte [Transmisión de datos del blob de Almacenamiento de Azure al Almacén de Data Lake mediante el Análisis de transmisiones](data-lake-store-stream-analytics.md).

## <a name="use-data-lake-store-with-power-bi"></a>Uso del Almacén de Data Lake con Power BI
Puede usar datos de Power BI tooimport desde un tooanalyze de cuenta de almacén de Data Lake y visualizar datos Hola. Para más información, consulte [Análisis de datos en Almacén de Data Lake mediante Power BI](data-lake-store-power-bi.md).

## <a name="use-data-lake-store-with-data-catalog"></a>Uso de Almacén de Data Lake con Catálogo de datos
Puede registrar datos de almacén de Data Lake en datos de catálogo de datos de Azure toomake saludo reconocibles a lo largo de la organización de Hola Hola. Para más información, consulte [Registro de datos del Almacén de Data Lake en el Catálogo de datos de Azure](data-lake-store-with-data-catalog.md).

## <a name="use-data-lake-store-with-sql-server-integration-services-ssis"></a>Uso de Data Lake Store con SQL Server Integration Services (SSIS)
Puede usar el Administrador de conexiones de almacén de Azure Data Lake hello en SSIS tooconnect un paquete SSIS con el almacén de Azure Data Lake. Para más información, consulte [Uso de Data Lake Store con SSIS](https://docs.microsoft.com/sql/integration-services/connection-manager/azure-data-lake-store-connection-manager).

## <a name="use-data-lake-store-with-sql-data-warehouse"></a>Uso de Data Lake Store con SQL Data Warehouse
Puede usar datos de PolyBase tooload de almacén de Data Lake de Azure en almacenamiento de datos de SQL. Para más información, consulte [Uso de Data Lake Store con SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-load-from-azure-data-lake-store.md).

## <a name="see-also"></a>Consulte también
* [Información general del Almacén de Azure Data Lake](data-lake-store-overview.md)
* [Introducción al Almacén de Data Lake mediante el Portal](data-lake-store-get-started-portal.md)
* [Introducción al Almacén de Data Lake mediante PowerShell](data-lake-store-get-started-powershell.md)  

