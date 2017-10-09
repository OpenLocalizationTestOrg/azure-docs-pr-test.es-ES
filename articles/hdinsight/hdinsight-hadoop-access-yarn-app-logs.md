---
title: "aaaAccess aplicación YARN de Hadoop mediante programación - registros de Azure | Documentos de Microsoft"
description: "La aplicación de Access se registra mediante programación en un clúster de Hadoop en HDInsight."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0198d6c9-7767-4682-bd34-42838cf48fc5
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 064efee1ea6a864c29ab897692ead0152c926c0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="access-yarn-application-logs-on-windows-based-hdinsight"></a>Acceso a registros de aplicación de YARN en HDInsight basado en Windows
Este tema explica cómo tooaccess Hola registros para las aplicaciones de YARN (aún otro negociador de recursos) que se hayan terminado en un clúster basado en Windows Hadoop en HDInsight de Azure

> [!IMPORTANT]
> información de Hello en este documento aplica según tooWindows solo clústeres de HDInsight. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). Para obtener información sobre cómo acceder a registros de YARN en clústeres de HDInsight basados en Linux, vea [Acceso a registros de aplicación de YARN en Hadoop basado en Linux en HDInsight](hdinsight-hadoop-access-yarn-app-logs-linux.md)
>


### <a name="prerequisites"></a>Requisitos previos
* Un clúster de HDInsight basado en Windows  Consulte [Creación de clústeres de Hadoop basados en Windows en HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="yarn-timeline-server"></a>Servidor de escala de tiempo de YARN
Hola <a href="http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html" target="_blank">YARN escala de tiempo de servidor</a> proporciona información genérica sobre aplicaciones completadas, así como framework información específica de la aplicación a través de dos interfaces diferentes. Concretamente:

* Se ha habilitado el almacenamiento y la recuperación de información de aplicaciones genéricas en clústeres de HDInsight con la versión 3.1.1.374 o superiores.
* componente de información de aplicación específica del marco de Hola de hello escala de tiempo de servidor no está disponible actualmente en clústeres de HDInsight.

Obtener información general sobre aplicaciones incluye Hola siguientes a tipos de datos:

* Identificador de la aplicación Hello, un identificador único de una aplicación
* usuario de Hola que inició la aplicación hello
* Obtener información acerca de intentos realizados aplicación de hello toocomplete
* contenedores de Hello utilizados por cualquier intento de aplicación determinada

En los clústeres de HDInsight, esta información se almacenarán en tienda de Azure Resource Manager tooa historial en contenedor de hello predeterminado de la cuenta de almacenamiento de Azure de forma predeterminada. Estos datos genéricos sobre aplicaciones completadas se pueden recuperar a través de una API de REST:

    GET on https://<cluster-dns-name>.azurehdinsight.net/ws/v1/applicationhistory/apps


## <a name="yarn-applications-and-logs"></a>Registros y aplicaciones de YARN
YARN admite varios modelos de programación (MapReduce es uno de ellos) al desacoplar la administración de recursos de la programación/supervisión de aplicaciones. Esto se realiza mediante un *Resource Manager* (RM) global, por nodo de trabajo *Administradores de nodos* (NM) y por aplicación *Maestros de aplicación* (AM). Hello por aplicación AM negocia recursos (CPU, memoria, disco, red) para ejecutar la aplicación con RM de Hola. Hola RM funciona con NMs toogrant estos recursos, que se le conceden como *contenedores*. Hola AM es responsable de seguimiento del progreso de Hola de hello tooit de contenedores asignados por RM de Hola. Una aplicación puede requerir muchos contenedores según la naturaleza de Hola de aplicación hello.

Además, cada aplicación puede constar de varios *aplicación intentos* en orden toofinish en presencia de Hola de bloqueos o toohello pérdida de comunicación entre un AM y un RM. Por lo tanto, los contenedores se conceden tooa intento específico de una aplicación. En un sentido, un contenedor proporciona el contexto de hello para la unidad básica del trabajo realizado por una aplicación de YARN y todo el trabajo que se realiza en contexto de Hola de un contenedor se realiza en el nodo de trabajo único de hello en qué Hola se asignó el contenedor. Consulte [Conceptos de YARN][YARN-concepts] como referencia adicional.

Registros de aplicación (y registros de contenedor de hello asociado) son fundamentales en la depuración de aplicaciones de Hadoop problemáticas. YARN proporciona un marco "nice" para recopilar, agregar y almacenar los registros de aplicación con hello [registro agregación] [ log-aggregation] característica. función de agregación de registro de Hello hace acceso a registros de aplicaciones más determinista, ya que agrega registros en todos los contenedores en un nodo de trabajo y almacena como un archivo registro agregado por nodo de trabajo en el sistema de archivos predeterminado de hello una vez finalizada una aplicación. La aplicación puede usar cientos o miles de contenedores, pero registros para todos los contenedores que se ejecute en un nodo de trabajo único siempre será tooa agregado archivos únicos, lo que da lugar a un archivo de registro por cada nodo de trabajo utilizado por la aplicación. Agregación de registro está habilitado de forma predeterminada en los clústeres de HDInsight (versión 3.0 y versiones posteriores), y registros agregados pueden encontrarse en el contenedor de hello predeterminado del clúster en hello ubicación siguiente:

    wasb:///app-logs/<user>/logs/<applicationId>

En esa ubicación, *usuario* es Hola nombre de usuario de Hola que inició la aplicación hello, y *applicationId* es el identificador único de Hola de una aplicación tal como lo asignó hello YARN RM

Hello registros agregados no son directamente legibles, tal y como se escriben un [TFile][T-file], [formato binario] [ binary-format] indizado por contenedor. YARN proporciona CLI herramientas toodump estos registros como texto sin formato para las aplicaciones o contenedores de interés. Puede ver estos registros como texto sin formato, ejecute uno de hello siga los comandos YARN directamente en nodos de clúster de hello (después de conectarse tooit a través de RDP):

    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application>
    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application> -containerId <containerId> -nodeAddress <worker-node-address>


## <a name="yarn-resourcemanager-ui"></a>Interfaz de usuario de ResourceManager de YARN
Hola YARN ResourceManager UI se ejecuta en el nodo principal del clúster de Hola y son accesibles a través de hello Azure panel del portal:

1. Inicie sesión en demasiado[portal de Azure](https://portal.azure.com/).
2. En el menú de la izquierda hello, haga clic en **examinar**, haga clic en **clústeres de HDInsight**, haga clic en un clúster basado en Windows que desea tooaccess Hola YARN registros de la aplicación.
3. En el menú superior de hello, haga clic en **panel**. Verá una página abierta en una nueva pestaña del explorador denominada **Consola de consultas de HDInsight**.
4. Desde **Consola de consultas de HDInsight**, haga clic en **IU de YARN**.

[YARN-timeline-server]:http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html
[log-aggregation]:http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/
[T-file]:https://issues.apache.org/jira/secure/attachment/12396286/TFile%20Specification%2020081217.pdf
[binary-format]:https://issues.apache.org/jira/browse/HADOOP-3315
[YARN-concepts]:http://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/
