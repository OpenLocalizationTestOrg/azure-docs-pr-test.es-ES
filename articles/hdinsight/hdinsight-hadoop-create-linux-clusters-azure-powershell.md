---
title: "clústeres de Hadoop de aaaCreate con PowerShell, HDInsight de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate Hadoop, HBase, tormenta o Spark clusters en Linux para HDInsight mediante Azure PowerShell."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4208deca-d64a-45e1-8948-2673d5d7678c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 53afe4702f6b61a0720ceda48a4a34d7fa8797d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-azure-powershell"></a>Crear clústeres basados en Linux en HDInsight con Azure PowerShell

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Azure PowerShell es un entorno de scripting eficaz que puede usar toocontrol y automatizar la implementación de Hola y administración de las cargas de trabajo en Microsoft Azure. Este documento proporciona información sobre cómo agrupar toocreate un HDInsight basados en Linux mediante el uso de PowerShell de Azure. También se incluye un script de ejemplo.

> [!NOTE]
> Azure PowerShell solo está disponible en clientes de Windows. Si utiliza un cliente de Mac OS X, Unix o Linux, consulte [crear un clúster de HDInsight basados en Linux mediante Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) para obtener información acerca del uso de hello Azure CLI toocreate un clúster.

## <a name="prerequisites"></a>Requisitos previos
Debe disponer de hello siguiente antes de iniciar este procedimiento:

* Una suscripción de Azure. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* [Azure PowerShell](/powershell/azure/install-azurerm-ps)

    > [!IMPORTANT]
    > La compatibilidad con Azure PowerShell para administrar recursos de HDInsight mediante Azure Service Manager está **en desuso** y dejó de estar disponible por completo el 1 de enero de 2017. Hola pasos de este documento use Hola nuevos cmdlets de HDInsight que funcionan con el Administrador de recursos de Azure.
    >
    > Siga los pasos de hello en [instale Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) versión más reciente de hello tooinstall de PowerShell de Azure. Si tiene scripts de ese toobe necesidad de modifica toouse Hola nuevos cmdlets que funcionan con el Administrador de recursos de Azure, consulte [tooAzure desarrollo basado en el Administrador de recursos de migración de las herramientas de clústeres de HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) para obtener más información.

## <a name="create-cluster"></a>Crear clúster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

toocreate un clúster de HDInsight mediante el uso de PowerShell de Azure, debe completar Hola procedimientos siguientes:

* Creación de un grupo de recursos de Azure
* Creación de una cuenta de almacenamiento de Azure
* Creación de un contenedor de blobs de Azure
* Creación de un clúster de HDInsight

Hello secuencia de comandos siguiente se muestra cómo toocreate un nuevo clúster:

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]

valores de Hello especificados para el inicio de sesión de hello clúster son toocreate usado Hola cuenta de usuario de Hadoop para clústeres de Hola. Utilice este tooservices de tooconnect cuenta hospedadas en clúster de hello como web API de REST o interfaces de usuario.

valores de Hello especificados para el usuario SSH de hello son usuario SSH de hello toocreate usado para clúster Hola. Utilice esta cuenta toostart una sesión SSH remoto en clúster de Hola y ejecutar trabajos. Para obtener más información, vea hello [utilizar SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.

> [!IMPORTANT]
> Si tiene previsto toouse más de 32 nodos de trabajador (en la creación del clúster o Hola escalado del clúster después de la creación), también debe especificar un tamaño de nodo principal con un mínimo de 8 núcleos y 14 GB de RAM.
>
> Para obtener más información acerca de los tamaños de nodo y los costos asociados, consulte [Precios de HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

Puede pasar hasta too20 minutos toocreate un clúster.

## <a name="create-cluster-configuration-object"></a>Creación de un clúster: objeto de configuración

También puede crear un objeto de configuración de HDInsight mediante el cmdlet `New-AzureRmHDInsightClusterConfig`. A continuación, puede modificar estas opciones de configuración adicionales de tooenable de objeto de configuración para el clúster. Por último, utilice hello `-Config` parámetro de hello `New-AzureRmHDInsightCluster` configuración de cmdlet toouse Hola.

Hello script siguiente crea un tooconfigure de objeto de configuración un servidor de R en el tipo de clúster de HDInsight. configuración de Hello permite a un nodo del borde, RStudio y una cuenta de almacenamiento adicional.

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]

> [!WARNING]
> No se admite el uso de una cuenta de almacenamiento en una ubicación diferente que el clúster de HDInsight de Hola. Cuando se usa en este ejemplo, crear cuenta de almacenamiento adicional de Hola Hola misma ubicación que el servidor de Hola.

## <a name="customize-clusters"></a>Personalización de los clústeres

* Consulte [Personalización de los clústeres de HDInsight con Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).
* Consulte [Personalización de clústeres de HDInsight mediante la acción de scripts](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="delete-hello-cluster"></a>Eliminar el clúster de Hola

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Solución de problemas

Si experimenta problemas con la creación de clústeres de HDInsight, consulte los [requisitos de control de acceso](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha creado correctamente un clúster de HDInsight, usar hello después cómo toolearn recursos toowork con el clúster.

### <a name="hadoop-clusters"></a>Clústeres Hadoop

* [Uso de Hive con HDInsight](hdinsight-use-hive.md)
* [Uso de Pig con HDInsight](hdinsight-use-pig.md)
* [Uso de MapReduce con HDInsight](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a>Clústeres HBase

* [Introducción a HBase en HDInsight](hdinsight-hbase-tutorial-get-started-linux.md)
* [Desarrollo de aplicaciones de Java para HBase en HDInsight](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a>Clústeres Storm

* [Desarrollo de topologías de Java para Storm en HDInsight](hdinsight-storm-develop-java-topology.md)
* [Uso de componentes de Python en Storm en HDInsight](hdinsight-storm-develop-python-topology.md)
* [Implementación y supervisión de topologías con Storm en HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a>Clústeres de Spark

* [Crear una aplicación independiente con Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy](hdinsight-apache-spark-livy-rest-interface.md)
* [Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark con aprendizaje automático: Use Spark en HDInsight toopredict de resultados de la inspección de alimentos](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real](hdinsight-apache-spark-eventhub-streaming.md)

