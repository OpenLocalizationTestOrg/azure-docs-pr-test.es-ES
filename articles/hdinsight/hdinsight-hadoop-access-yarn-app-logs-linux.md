---
title: "inicia sesión aaaAccess aplicación YARN de Hadoop en HDInsight basados en Linux: Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooaccess YARN aplicación registra el en un clúster de HDInsight basados en Linux (Hadoop) mediante un explorador web y línea de comandos de saludo."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 3ec08d20-4f19-4a8e-ac86-639c04d2f12e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 0bab356e3b97114abbb05712c8e7b21a194f2508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="access-yarn-application-logs-on-linux-based-hdinsight"></a>Acceso a registros de aplicación de YARN en HDInsight basado en Linux

Obtenga información acerca de cómo tooaccess Hola registros para las aplicaciones de YARN (aún otro recurso negociador) en un clúster de Hadoop en HDInsight de Azure.

> [!IMPORTANT]
> pasos de Hello en este documento requieren un clúster de HDInsight que usa Linux. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Para obtener más información, consulte el artículo relativo al [control de versiones de componentes de HDInsight](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="YARNTimelineServer"></a>Servidor de escala de tiempo de YARN

Hola [YARN escala de tiempo de servidor](http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html) proporciona información genérica sobre aplicaciones completadas y de información de la aplicación específica del marco a través de dos interfaces diferentes. Concretamente:

* Se ha habilitado el almacenamiento y la recuperación de información de aplicaciones genéricas en clústeres de HDInsight con la versión 3.1.1.374 o superiores.
* componente de información de aplicación específica del marco de Hola de hello escala de tiempo de servidor no está disponible actualmente en clústeres de HDInsight.

Obtener información general sobre aplicaciones incluye Hola después del tipo de datos:

* Identificador de la aplicación Hello, un identificador único de una aplicación
* usuario de Hola que inició la aplicación hello
* Obtener información acerca de intentos realizados aplicación de hello toocomplete
* contenedores de Hello utilizados por cualquier intento de aplicación determinada

## <a name="YARNAppsAndLogs"></a>Registros y aplicaciones de YARN

YARN admite varios modelos de programación (MapReduce es uno de ellos) al desacoplar la administración de recursos de la programación/supervisión de aplicaciones. Así, usa una instancia de *Resource Manager* (RM) global por nodo de trabajo *NodeManagers* (NM) y por aplicación *ApplicationMasters* (AM). Hello por aplicación AM negocia recursos (CPU, memoria, disco, red) para ejecutar la aplicación con RM de Hola. Hola RM funciona con NMs toogrant estos recursos, que se le conceden como *contenedores*. Hola AM es responsable de seguimiento del progreso de Hola de hello tooit de contenedores asignados por RM de Hola. Una aplicación puede requerir muchos contenedores según la naturaleza de Hola de aplicación hello.

Cada aplicación puede constar de varios *intentos de aplicación*. Si se produce un error en una aplicación, se puede reintentar como un nuevo intento. Cada intento se ejecuta en un contenedor. En un sentido, un contenedor proporciona el contexto de hello para la unidad básica del trabajo realizado por una aplicación de YARN. Todo el trabajo que se realiza en contexto de Hola de un contenedor se realiza en el nodo de trabajo único de hello en qué Hola se asignó el contenedor. Consulte [Conceptos de YARN][YARN-concepts] como referencia adicional.

Registros de aplicación (y registros de contenedor de hello asociado) son fundamentales en la depuración de aplicaciones de Hadoop problemáticas. YARN proporciona un marco "nice" para recopilar, agregar y almacenar los registros de aplicación con hello [registro agregación] [ log-aggregation] característica. función de agregación de registro de Hello hace acceso a registros de aplicaciones más determinista. Esta característica agrega los registros en todos los contenedores de un nodo de trabajo y los almacena como un archivo de registros agregados por cada nodo de trabajo. registro de Hello se almacena en el sistema de archivos predeterminado de hello cuando una aplicación finaliza. La aplicación puede usar cientos o miles de contenedores, pero registros para todos los contenedores que se ejecute en un nodo de trabajo único siempre son agregado tooa archivos únicos. Por tanto, solo hay un registro por nodo de trabajo usado por la aplicación. La agregación de registros está habilitada de forma predeterminada en los clústeres de HDInsight de la versión 3.0 y superior. Registros agregados se encuentran en almacenamiento predeterminado para el clúster de Hola. Hola siguiendo la ruta de acceso es Hola HDFS ruta de acceso toohello registros:

    /app-logs/<user>/logs/<applicationId>

En la ruta de acceso de hello, `user` es Hola nombre de usuario de Hola que inició la aplicación hello. Hola `applicationId` es aplicación de tooan Hola identificador único asignado por RM de hello YARN.

Hello registros agregados no son directamente legibles, tal y como se escriben un [TFile][T-file], [formato binario] [ binary-format] indizado por contenedor. Usar Hola que YARN ResourceManager registra o CLI herramientas tooview estos registros como texto sin formato para las aplicaciones o contenedores de interés.

## <a name="yarn-cli-tools"></a>Herramientas de la CLI de YARN

herramientas de toouse hello YARN CLI, debe conectarse primero a clúster de HDInsight de toohello mediante SSH. Para más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

Puede ver estos registros como texto sin formato al ejecutar uno de hello siguientes comandos:

    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application>
    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application> -containerId <containerId> -nodeAddress <worker-node-address>

Especificar hello &lt;applicationId >, &lt;usuario que-iniciado-la aplicación >, &lt;containerId >, y &lt;dirección de nodo de trabajo > obtener información sobre cómo ejecutar estos comandos.

## <a name="yarn-resourcemanager-ui"></a>Interfaz de usuario de ResourceManager de YARN

Hola YARN ResourceManager UI se ejecuta en el nodo principal del clúster de Hola. Se tiene acceso a través de la interfaz de usuario de web de hello Ambari. Hola uso siguiendo los pasos tooview hello YARN registra:

1. En el explorador web, vaya toohttps://CLUSTERNAME.azurehdinsight.net. Reemplace CLUSTERNAME por nombre de Hola de su clúster de HDInsight.
2. En la lista hello de servicios de hello izquierda, seleccione **YARN**.

    ![Servicio de YARN seleccionado](./media/hdinsight-hadoop-access-yarn-app-logs-linux/yarnservice.png)
3. De hello **vínculos rápidos** de lista desplegable, seleccione uno de los nodos principales del clúster de hello y, a continuación, seleccione **ResourceManager registro**.

    ![Vínculos rápidos de YARN](./media/hdinsight-hadoop-access-yarn-app-logs-linux/yarnquicklinks.png)

    Se le presentará una lista de vínculos tooYARN registros.

[YARN-timeline-server]:http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html
[log-aggregation]:http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/
[T-file]:https://issues.apache.org/jira/secure/attachment/12396286/TFile%20Specification%2020081217.pdf
[binary-format]:https://issues.apache.org/jira/browse/HADOOP-3315
[YARN-concepts]:http://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/
