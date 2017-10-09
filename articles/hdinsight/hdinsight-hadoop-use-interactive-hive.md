---
title: aaaUse interactivo de Hive en HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse interactivo Hive (Hive en LLAP) en HDInsight."
keywords: 
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0957643c-4936-48a3-84a3-5dc83db4ab1a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 9e751a08091d18bc1b3d070468feef87f6828c61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-interactive-hive-in-hdinsight-preview"></a>Uso de Interactive Hive en HDInsight (versión preliminar)
Interactive Hive (también conocido como "[Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP))" es un nuevo [tipo de clúster](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) de HDInsight.  Interactive Hive permite el almacenamiento en caché en memoria, con lo que las consultas de Hive serán mucho más interactivas y rápidas. Esta nueva característica permite HDInsight uno de hello soluciones del mundo mayoría eficiente, flexibles y abiertas grandes cantidades de datos en la nube de hello con cachés en memoria (con Hive y Spark) y advanced analytics a través de la integración con R Services. 

clúster de Hive interactivo de Hello es diferente del clúster de Hadoop de Hola. Solo contiene servicio de Hive Hola. 

> [!NOTE]
> MapReduce, Pig, Sqoop, Oozie y otros servicios se quitarán pronto de este tipo de clúster.
> Hola subárbol servicio en clúster de Hive interactivo de hello solo es accesible a través de hello vista del subárbol de Ambari, Beeline y Hive ODBC. No se puede acceder mediante la consola de Hive, Templeton, la CLI de Azure y Azure PowerShell. 
> 
> 

## <a name="create-an-interactive-hive-cluster"></a>Creación de un clúster de Interactive Hive
El clúster de Interactive Hive solo es compatible con los clústeres basados en Linux. Para obtener más información sobre cómo crear clústeres de HDInsight, consulte [Creación de clústeres de Hadoop basados en Linux en HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="execute-hive-from-interactive-hive"></a>Ejecución de Hive desde Interactive Hive
Hay diferentes opciones en lo que respecta a cómo ejecutar consultas de Hive:

* Ejecutar Hive con hello Ambari Hive vista
  
    Para obtener información de hello acerca del uso de hello Hive vista, consulte [Hola Use vista Hive con Hadoop en HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).
* Ejecución de Hive mediante Beeline
  
    Para obtener información sobre el uso de Beeline en HDInsight hello, consulte [uso de Hive con Hadoop en HDInsight con Beeline](hdinsight-hadoop-use-hive-beeline.md).
  
    Utilice Beeline desde el nodo principal de Hola o un nodo del borde vacío.  Se recomienda usar Beeline en un nodo perimetral vacío.  Para obtener información sobre cómo crear un clúster de HDInsight con un nodo perimetral vacío, consulte [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md) (Uso de nodos perimetrales vacíos en HDInsight).
* Ejecución de Hive mediante Hive ODBC
  
    Encontrará información sobre el uso de Hive ODBC hello [tooHadoop Excel conectarse con el controlador de Microsoft ODBC Hive hello](hdinsight-connect-excel-hive-odbc-driver.md).

**Hola toofind cadena de conexión de JDBC:**

1. Inicio de sesión tooAmbari con hello después de la dirección URL: https://<ClusterName>. AzureHDInsight.net.
2. Haga clic en **Hive** desde el menú de la izquierda Hola.
3. Haga clic en la dirección URL de hello resaltado icono toocopy Hola:
   
   ![Cadena de conexión de JDBC para Interactive Hive con LLAP (Hadoop de HDInsight)](./media/hdinsight-hadoop-use-interactive-hive/hdinsight-hadoop-use-interactive-hive-jdbc.png)

## <a name="see-also"></a>Otras referencias
* [Crear clústeres de Linux-based Hadoop en HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Obtenga información acerca de cómo los clústeres de toocreate interactivo de Hive en HDInsight.
* [Usar el subárbol con Hadoop en HDInsight con Beeline](hdinsight-hadoop-use-hive-beeline.md): Obtenga información acerca de cómo las consultas de Hive de toouse Beeline toosubmit.
* [Conectar Excel tooHadoop con hello Hive controlador ODBC de Microsoft](hdinsight-connect-excel-hive-odbc-driver.md): Obtenga información acerca de cómo tooconnect tooHive de Excel.

