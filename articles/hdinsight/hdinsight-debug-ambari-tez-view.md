---
title: aaaUse Ambari Tez vista con HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse hello Ambari Tez ver trabajos de Tez toodebug en HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 9c39ea56-670b-4699-aba0-0f64c261e411
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 5d61bd0403c98284c86982073af91468ae62ac60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-ambari-views-toodebug-tez-jobs-on-hdinsight"></a>Usar vistas de Ambari toodebug Tez trabajos en HDInsight

Hola Ambari Web UI para HDInsight contiene una vista de Tez que puede ser utilizados trabajos toounderstand y depuración que utilizan Tez. Hola Tez vista le permite toovisualize trabajo de hello, como un gráfico de elementos conectados, profundizar en cada elemento y recuperar las estadísticas y la información de registro.

> [!IMPORTANT]
> pasos de Hello en este documento requieren un clúster de HDInsight que usa Linux. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Para obtener más información, consulte el artículo relativo al [control de versiones de componentes de HDInsight](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="prerequisites"></a>Requisitos previos

* Un clúster de HDInsight basado en Linux Para conocer la forma de crear un clúster, consulte el [artículo de introducción al uso de HDInsight basado en Linux](hdinsight-hadoop-linux-tutorial-get-started.md).
* Un explorador web moderno que sea compatible con HTML5.

## <a name="understanding-tez"></a>Descripción de Tez

Tez es un marco de trabajo extensible para el procesamiento de datos en Hadoop que proporciona una mayor velocidad que el procesamiento tradicional de MapReduce. Para los clústeres de HDInsight basados en Linux, es motor predeterminado de Hola de Hive.

Tez crea un dirigen acíclico gráfico (DAG) que describe el orden de Hola de acciones requeridas por los trabajos. Acciones individuales se denominan vértices y ejecutar una parte del programa Hola trabajo completo. ejecución real de Hola de trabajo de hello descrita por un vértice se denomina una tarea y se puede distribuir en varios nodos de clúster de Hola.

### <a name="understanding-hello-tez-view"></a>Hola descripción Tez vista

Hola Tez vista proporciona información histórica y obtener información acerca de procesos que se ejecutan. Esta información muestra la distribución de un trabajo a través de los clústeres, También muestra los contadores que se usan las tareas y los vértices y toohello trabajos relacionados con la información de error. Puede ofrecer información útil en hello los escenarios siguientes:

* Supervisión de los procesos de larga ejecución, ver progreso de asignación de Hola y reduzcan las tareas.
* Analizar datos históricos para procesos correctos o con error toolearn cómo se puede mejorar el procesamiento o por qué se produjo un error.

## <a name="generate-a-dag"></a>Generar un DAG

Hola Tez vista solo contiene datos si un trabajo que utiliza Hola Tez motor está actualmente se está ejecutando o se ha ejecutado anteriormente. Las consultas simples de Hive pueden resolverse sin necesidad de usar Tez. Para aquellas consultas más complejas que realizan filtrados, agrupaciones, ordenaciones, combinaciones, etc., Use hello Tez motor.

Usar hello siguiendo los pasos toorun una consulta de Hive que usa Tez:

1. En un explorador web, vaya toohttps://CLUSTERNAME.azurehdinsight.net, donde **CLUSTERNAME** es Hola nombre de su clúster de HDInsight.

2. En menú de hello al principio de Hola de página de hello, seleccione hello **vistas** icono. Este icono tiene el aspecto de un conjunto de cuadrados. En la lista desplegable de Hola que aparece, seleccione **Hive vista**.

    ![Seleccionar la vista de Hive](./media/hdinsight-debug-ambari-tez-view/selecthive.png)

3. Cuando se carga Hola vista Hive, siguiente de hello pegar consultas en el Editor de consultas de hello y, a continuación, haga clic en **ejecutar**.

        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;

    Cuando haya completado el trabajo de hello, debería ver el resultado de hello muestra de Hola **resultados del proceso de consulta** sección. resultados de Hello deberían ser similar toohello siguiente texto:

        market  state       country
        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica

4. Seleccione hello **registro** ficha. Vea información toohello similar siguiente texto:

        INFO : Session is already open
        INFO :

        INFO : Status: Running (Executing on YARN cluster with App id application_1454546500517_0063)

    Guardar hello **Id. de aplicación** valor, tal como este valor se utiliza en la sección siguiente Hola.

## <a name="use-hello-tez-view"></a>Usar hello Tez vista

1. En menú de hello al principio de Hola de página de hello, seleccione hello **vistas** icono. En la lista desplegable de Hola que aparece, seleccione **Tez vista**.

    ![Seleccionar la vista de Tez](./media/hdinsight-debug-ambari-tez-view/selecttez.png)

2. Cuando se cargue hello Tez vista, verá una lista de consultas de hive que se están ejecutando actualmente, o bien haber ejecutado en clúster de Hola.

    ![Todos los DAG](./media/hdinsight-debug-ambari-tez-view/tez-view-home.png)

3. Si tiene sólo una entrada, es de consulta de Hola que se ejecutó en la sección anterior de Hola. Si tiene varias entradas, puede buscar mediante campos hello en parte superior de Hola de página Hola.

4. Seleccione hello **identificador de la consulta** para una consulta de Hive. Se muestra información sobre la consulta de Hola.

    ![Detalles del DAG](./media/hdinsight-debug-ambari-tez-view/query-details.png)

5. pestañas de Hello en esta página le permiten hello tooview siguiente información:

    * **Detalles de la consulta**: obtener detalles acerca de la consulta de Hive Hola.
    * **Escala de tiempo**: información sobre cuánto tiempo ha tardado cada fase de procesamiento.
    * **Las configuraciones de**: configuración de hello utilizado para esta consulta.

    De __detalles de la consulta__ puede utilizar Hola vínculos toofind información acerca de hello __aplicación__ o hello __DAG__ para esta consulta.
    
    * Hola __aplicación__ vínculo muestra información acerca de hello aplicación YARN para esta consulta. Desde aquí puede tener acceso a registros de la aplicación hello YARN.
    * Hola __DAG__ vínculo muestra información acerca de gráfico acíclico dirigido Hola para esta consulta. Desde aquí puede ver una representación gráfica de hello DAG. También puede encontrar información sobre los vértices de hello en hello DAG.

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha aprendido cómo ver hello toouse Tez, obtenga más información sobre [utilizando Hive en HDInsight](hdinsight-use-hive.md).

Para obtener más información técnica sobre Tez, consulte hello [Tez página en Hortonworks](http://hortonworks.com/hadoop/tez/).

Para obtener más información sobre el uso de Ambari con HDInsight, vea [administrar clústeres de HDInsight con hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md)
