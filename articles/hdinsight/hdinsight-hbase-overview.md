---
title: "¿aaaWhat es HBase en HDInsight de Azure? | Microsoft Docs"
description: "Un tooApache Introducción HBase en HDInsight, una base de datos NoSQL compilar en Hadoop. Obtenga información acerca de los casos de uso y comparar los clústeres de Hadoop de HBase tooother."
keywords: "bigtable, nosql, qué es hbase, apache hbase, hbase, información general hbase,"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: d2a76d53-133a-4849-a30c-88d9c794391c
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 0d28378d07b1a168e38748548578be11310d2228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hbase-in-hdinsight-a-nosql-database-that-provides-bigtable-like-capabilities-for-hadoop"></a>Qué es HBase en HDInsight: una base de datos NoSQL que proporciona funciones de tipo BigTable para Hadoop
Apache HBase es una base de datos NoSQL de código abierto que se compila en Hadoop y se modela después de Google BigTable. HBase proporciona acceso aleatorio y enorme coherencia para grandes cantidades de datos no estructurados y semiestructurados en una base de datos sin esquemas organizada por familias de columnas.

Datos se almacenan en filas Hola de una tabla y los datos dentro de una fila se agrupan por familia de columna. HBase es una base de datos schemaless en sentido Hola ninguno Hola columnas ni el tipo de saludo de los datos almacenados en ellas necesita toobe definido antes de usarlos. código de código abierto de Hello escala linealmente toohandle petabytes de datos en miles de nodos. Puede depender de redundancia de datos, procesamiento por lotes y otras características que se proporcionan con aplicaciones distribuidas en el ecosistema de Hadoop de Hola.

## <a name="how-is-hbase-implemented-in-azure-hdinsight"></a>¿Cómo se implementa HBase en HDInsight de Azure?
HBase para HDInsight se ofrece como un clúster administrado que se integra en hello entorno de Azure. clústeres de Hello son toostore configurado datos directamente en [el almacenamiento de Azure](./hdinsight-hadoop-use-blob-storage.md) o [almacén de Azure Data Lake](./hdinsight-hadoop-use-data-lake-store.md), lo que proporciona baja latencia y mayor flexibilidad en las opciones de rendimiento y costo. Esto permite que los clientes toobuild sitios Web interactivos que trabaja con grandes conjuntos de datos, servicios de toobuild que almacenan los datos de sensor y telemetría de millones de puntos finales y tooanalyze estos datos con los trabajos de Hadoop. HBase y Hadoop son buenos puntos de partida para el proyecto de grandes cantidades de datos en Azure; en concreto, también puede permitir que las aplicaciones en tiempo real toowork con grandes conjuntos de datos.

implementación de HDInsight de Hello aprovecha la arquitectura de escalabilidad horizontal de Hola de HBase tooprovide automática particionamiento de tablas, homogeneidad de lecturas y escrituras y conmutación automática por error. Se mejora el rendimiento mediante el almacenamiento en caché de memoria para lecturas y streaming de alto rendimiento para escrituras. Se puede crear un clúster de HBase dentro de la red virtual. Para obtener detalles, consulte [Creación de clústeres de HBase en Azure Virtual Network][hbase-provision-vnet].

## <a name="how-is-data-managed-in-hdinsight-hbase"></a>¿Cómo se administran los datos en HBase de HDInsight?
Datos pueden administrarse en HBase mediante el uso de hello `create`, `get`, `put`, y `scan` comandos de shell de HBase Hola. Datos se escriben toohello base de datos mediante el uso de `put` y leer mediante `get`. Hola `scan` comando es tooobtain usa datos de varias filas en una tabla. También se pueden administrar datos con hello HBase API de C#, que proporciona una biblioteca de cliente en la parte superior Hola API de REST de HBase. Asimismo, una base de datos de HBase se puede consultar usando Hive. Para una toothese Introducción modelos de programación, vea [empezar a utilizar HBase con Hadoop en HDInsight][hbase-get-started]. Coprocesadores también están disponibles, que permiten el procesamiento de datos en nodos de Hola esa base de datos de Hola de host.

> [!NOTE]
> Thrift no es compatible con HBase en HDInsight.
>

## <a name="scenarios-use-cases-for-hbase"></a>Escenarios: Casos de uso de HBase
Hello caso de uso canónica para qué BigTable (y por extensión, HBase) se creó era la búsqueda en la web. Los motores de búsqueda generan índices que se asignan páginas web de términos toohello que los contienen. Sin embargo, hay muchos otros casos de uso a los que se adapta HBase, varios de los cuales se muestran en esta sección.

* almacén de pares clave-valor
  
    HBase se puede usar como almacén de pares clave-valor y es adecuado para la administración de sistemas de mensajes. Facebook usa HBase para su sistema de mensajería y es ideal para almacenar y administrar comunicaciones de Internet. WebTable usa toosearch de HBase para y administrar las tablas que se extraen de las páginas Web.
* datos del sensor
  
    HBase es útil para capturar datos que se recopilan cada vez más a partir de diversas fuentes. Entre estos se incluyen análisis sociales, serie temporal, actualización de paneles interactivos con tendencias y contadores y administración de sistemas de registro de auditoría. Algunos ejemplos son Bloomberg comerciales terminal y Hola tiempo serie bases de datos abiertos (OpenTSDB), que almacena y proporciona acceso toometrics recopilada sobre el estado de Hola de sistemas de servidor.
* consulta en tiempo real
  
    [Phoenix](http://phoenix.apache.org/) es un motor de consultas SQL para HBase Apache. Se obtiene acceso a él como controlador de JDBC y permite consultar y administrar tablas de HBase usando SQL.
* HBase como plataforma
  
    Las aplicaciones pueden ejecutarse en de HBase usándolo como almacén de datos. Entre los ejemplos se incluyen Phoenix, OpenTSDB, Kiji y Titan. Las aplicaciones también pueden integrarse con HBase. Entre los ejemplos se incluyen Hive, Pig, Solr, Storm, Flume, Impala, Spark, Ganglia y Drill.

## <a name="next-steps"></a>Pasos siguientes
* [Introducción al uso de HBase con Hadoop en HDInsight][hbase-get-started]
* [Creación de clústeres de HBase en Azure Virtual Network][hbase-provision-vnet]
* [Configuración de la replicación geográfica de HBase en HDInsight](hdinsight-hbase-replication.md)
* [Análisis de opiniones de Twitter con HBase en HDInsight][hbase-twitter-sentiment]
* [Utilizar aplicaciones de Java de toobuild de Maven que usan HBase con HDInsight (Hadoop)][hbase-build-java-maven]

## <a name="see-also"></a>Otras referencias
* [Apache HBase](https://hbase.apache.org/)
* [Bigtable: un sistema de almacenamiento distribuido para datos estructurados](http://research.google.com/archive/bigtable.html)

[hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md

[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hbase-build-java-maven]: hdinsight-hbase-build-java-maven.md

[hdinsight-use-hive]: hdinsight-use-hive.md

[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md

[hbase-get-started]: http://azure.microsoft.com/documentation/articles/hdinsight-hbase-get-started/

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
