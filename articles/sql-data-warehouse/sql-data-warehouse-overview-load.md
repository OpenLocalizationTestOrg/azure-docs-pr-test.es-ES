---
title: datos de aaaLoad en almacenamiento de datos de SQL de Azure | Documentos de Microsoft
description: "Obtenga información acerca de escenarios comunes de Hola de carga en el almacén de datos SQL de datos. Estos incluyen el uso de PolyBase, el almacenamiento de blobs de Azure, archivos planos y el envío de discos. También puede usar herramientas de otros fabricantes."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 2253bf46-cf72-4de7-85ce-f267494d55fa
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: d1a5063f484e9bd95f854e27a4baed512148aad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-azure-sql-data-warehouse"></a>Carga de datos en Almacenamiento de datos SQL de Azure
Resumen de opciones de escenario de Hola y recomendaciones para cargar datos en almacenamiento de datos SQL.

la parte más difícil de Hello de la carga de datos normalmente es preparar los datos de Hola para carga Hola. Azure simplifica la carga mediante el uso de almacenamiento de blobs de Azure como almacén de datos común para muchos de los servicios de Hola y con Data Factory de Azure Hola tooorchestrate comunicación y movimiento de datos entre los servicios de Azure. Estos procesos se integran con la tecnología de PolyBase que utiliza el procesamiento en paralelo masivamente datos de tooload (MPP) en paralelo desde el almacenamiento de blobs de Azure en almacenamiento de datos de SQL. 

Para ver tutoriales que cargan bases de datos de ejemplo, vea [Carga de datos de ejemplo en SQL Data Warehouse][Load sample databases].

## <a name="load-from-azure-blob-storage"></a>Carga desde el almacenamiento de blobs de Azure
datos de tooimport de manera más rápidos de saludo en almacenamiento de datos de SQL están toouse datos de tooload de PolyBase de almacenamiento de blobs de Azure. PolyBase usa almacenamiento de datos SQL procesamiento en paralelo masivamente datos en tooload de diseño (MPP) en paralelo desde el almacenamiento de blobs de Azure. toouse PolyBase, puede usar comandos de T-SQL o una canalización del generador de datos de Azure.

### <a name="1-use-polybase-and-t-sql"></a>1. Usar PolyBase y T-SQL
Resumen del proceso de carga:

1. Mover el almacenamiento de blobs de tooAzure de datos o el almacén de Azure Data Lake y almacenar en archivos de texto.
2. Configurar objetos externos en la ubicación de almacenamiento de datos SQL toodefine Hola y el formato de datos de Hola
3. Ejecutar una instrucción T-SQL comando tooload Hola de datos en paralelo en una nueva tabla de base de datos.

<!-- 5. Schedule and run a loading job. --> 

Para obtener un tutorial, vea [cargar datos desde almacenamiento de blobs de Azure tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].

### <a name="2-use-azure-data-factory"></a>2. Usar Data Factory de Azure
Para una forma más sencilla toouse PolyBase, puede crear una canalización del generador de datos de Azure que utiliza datos de tooload de PolyBase de almacenamiento de blobs de Azure en almacenamiento de datos de SQL. Se trata de tooconfigure rápida puesto que no necesita objetos de T-SQL toodefine Hola. Si tiene datos externos de hello tooquery sin importarlo, usar T-SQL. 

Resumen del proceso de carga:

1. Mover el almacenamiento de blobs de datos tooAzure y almacenar en archivos de texto. Azure Data Factory no admite actualmente la conectividad de ADLS con PolyBase.
2. Crear una canalización de factoría de datos de Azure tooingest Hola datos. Use la opción de PolyBase de Hola.
4. Programar y ejecutar la canalización de Hola.

Para obtener un tutorial, vea [cargar datos desde almacenamiento de blobs de Azure tooSQL Data Warehouse (factoría de datos de Azure)][Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)].

## <a name="load-from-sql-server"></a>Carga desde SQL Server
datos tooload de SQL Server tooSQL almacenamiento de datos se pueden utilizar Integration Services (SSIS), transferencia de archivos planos o distribuir tooMicrosoft de discos. Siga leyendo toosee un resumen de hello diferente carga tootutorials procesos y vínculos.

tooplan una migración completa de los datos de SQL Server tooSQL almacenamiento de datos, vea hello [Introducción a la migración][Migration overview]. 

### <a name="use-integration-services-ssis"></a>Uso de Integration Services (SSIS)
Si ya usas tooload de paquetes de Integration Services (SSIS) en SQL Server, puede actualizar su toouse de paquetes SQL Server como origen de Hola y de almacenamiento de datos de SQL como destino de Hola. Esto es muy rápido y fácil toodo, y es una buena elección si no está tratando de toomigrate su carga procesar datos toouse ya se encuentran en la nube de Hola. contrapartida de Hello es carga Hola será más lento que usar PolyBase ya este SSIS no realiza la carga de hello en paralelo.

Resumen del proceso de carga:

1. Revise la instancia de SQL Server Integration Services paquete toopoint toohello para el origen de Hola y base de datos de almacenamiento de datos SQL de Hola para destino de Hola.
2. Migrar el almacenamiento de datos, de esquema tooSQL si no está ya.
3. Cambiar la asignación de hello en los paquetes utilizan Hola de solo los tipos de datos que es compatibles con el almacenamiento de datos SQL.
4. Programar y ejecutar paquetes de saludo.

Para obtener un tutorial, vea [cargar datos de SQL Server tooAzure almacenamiento de datos de SQL (SSIS)][Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)].

### <a name="use-azcopy-recommended-for--10-tb-data"></a>Uso de AZCopy (recomendado para datos de menos de 10 TB)
Si el tamaño de datos es < 10 TB, puede exportar datos de Hola desde los archivos de tooflat de SQL Server, copie el almacenamiento de blobs de hello archivos tooAzure y, a continuación, utilizar datos de PolyBase tooload hello en almacenamiento de datos de SQL

Resumen del proceso de carga:

1. Usar datos de tooexport de utilidad de línea de comandos de hello bcp de archivos de tooflat de SQL Server.
2. Usar hello AZCopy utilidad de línea de comandos toocopy datos desde almacenamiento de blobs de tooAzure de archivos sin formato.
3. Use PolyBase tooload en almacenamiento de datos de SQL.

Para obtener un tutorial, vea [cargar datos desde almacenamiento de blobs de Azure tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].

### <a name="use-bcp"></a>Uso de bcp
Si tiene una pequeña cantidad de datos puede usar bcp tooload directamente en el almacenamiento de datos de SQL Azure.

Resumen del proceso de carga:

1. Usar datos de tooexport de utilidad de línea de comandos de hello bcp de archivos de tooflat de SQL Server.
2. Usar bcp tooload datos de plano directamente archivos tooSQL almacenamiento de datos.

Para obtener un tutorial, vea [cargar datos de SQL Server tooAzure almacenamiento de datos de SQL (bcp)][Load data from SQL Server tooAzure SQL Data Warehouse (bcp)].

### <a name="use-importexport-recommended-for--10-tb-data"></a>Uso de importación/exportación (recomendado para datos de menos de 10 TB)
Si el tamaño de los datos es > 10 TB y desea toomove se tooAzure, se recomienda que utilice nuestro servicio de envío de disco [importación/exportación][Import/Export]. 

Resumen del proceso de carga

1. Usar datos de tooexport de utilidad de línea de comandos de hello bcp de archivos de SQL Server tooflat en discos transferibles.
2. Hola Ship discos tooMicrosoft.
3. Microsoft carga los datos de hello en almacenamiento de datos SQL

## <a name="load-from-hdinsight"></a>Carga desde HDInsight
El Almacenamiento de datos SQL admite la carga de datos desde HDInsight a través de PolyBase. proceso de Hello es Hola igual a la carga de datos desde almacenamiento de blobs de Azure: usar PolyBase tooconnect tooHDInsight tooload datos. 

### <a name="1-use-polybase-and-t-sql"></a>1. Usar PolyBase y T-SQL
Resumen del proceso de carga:

1. Mover el tooHDInsight de datos y almacenarla en archivos de texto, formato ORC o Parquet.
2. Configure los objetos externos en la ubicación de almacenamiento de datos SQL toodefine Hola y el formato de datos de Hola.
3. Ejecutar una instrucción T-SQL comando tooload Hola de datos en paralelo en una nueva tabla de base de datos.

Para obtener un tutorial, vea [cargar datos desde almacenamiento de blobs de Azure tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].

## <a name="recommendations"></a>Recomendaciones
Muchos de nuestros asociados tienen soluciones de carga. toofind más información, consulte una lista de nuestros [socios de soluciones de][solution partners]. 

Si los datos provienen de un origen no relacionales y desea tooload en datos de SQL de almacenamiento se necesitará tootransform en filas y columnas antes de cargarlos. no es necesario datos de Hello transforman toobe almacenado en una base de datos, pueden almacenarse en archivos de texto.

Cree estadísticas de los datos recién cargados. Almacenamiento de datos SQL de Azure todavía no permite crear ni actualizar automáticamente las estadísticas.  En orden tooget Hola un mejor rendimiento de las consultas, es importante toocreate estadísticas en todas las columnas de todas las tablas después de hello cargar por primera vez o se producen cambios sustanciales en datos Hola.  Para más información, vea las [estadísticas][Statistics].

## <a name="next-steps"></a>Pasos siguientes
Para más sugerencias de desarrollo, vea hello [Introducción al desarrollo de][development overview].

<!--Image references-->

<!--Article references-->
[Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md
[Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)]: ./sql-data-warehouse-load-from-sql-server-with-integration-services.md
[Load data from SQL Server tooAzure SQL Data Warehouse (bcp)]: ./sql-data-warehouse-load-from-sql-server-with-bcp.md
[Load data from SQL Server tooAzure SQL Data Warehouse (AZCopy)]: ./sql-data-warehouse-load-from-sql-server-with-azcopy.md

[Load sample databases]: ./sql-data-warehouse-load-sample-databases.md
[Migration overview]: ./sql-data-warehouse-overview-migrate.md
[solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->

<!--Other Web references-->
[Import/Export]: https://azure.microsoft.com/documentation/articles/storage-import-export-service/
