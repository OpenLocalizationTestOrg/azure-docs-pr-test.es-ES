---
title: "clústeres de Hadoop de aaaCreate mediante la línea de comandos - Hola HDInsight de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo los clústeres de HDInsight de toocreate con Hola multiplataforma Azure CLI 1.0."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 50b01483-455c-4d87-b754-2229005a8ab9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 5295b01054b8c23df0e3b75a3e0e8c933ac48b3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-using-hello-azure-cli"></a>Crear clústeres de HDInsight con hello CLI de Azure

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Hola pasos de este tutorial de documento creación de un clúster de HDInsight 3.5 con hello 1.0 de CLI de Azure.

> [!IMPORTANT]
> Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).


## <a name="prerequisites"></a>Requisitos previos

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **Una suscripción de Azure**. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

* **CLI de Azure** pasos de Hello en este documento se han probado última con CLI de Azure versión 0.10.14.

    > [!IMPORTANT]
    > pasos de Hello en este documento no funcionan con Azure CLI 2.0. La CLI de Azure 2.0 no admite la creación de un clúster de HDInsight.

## <a name="log-in-tooyour-azure-subscription"></a>Inicie sesión en tooyour suscripción de Azure

Siga los pasos de hello documentados en [conectarse tooan suscripción de Azure desde hello Azure interfaz de línea de comandos (CLI de Azure)](../xplat-cli-connect.md) y conectar suscripción tooyour con hello **inicio de sesión** método.

## <a name="create-a-cluster"></a>Crear un clúster

Hola pasos debe realizarse desde una línea de comandos, como PowerShell o Bash.

1. Usar hello después comando tooauthenticate tooyour suscripción de Azure:

        azure login

    Se está tooprovide solicitada su nombre y contraseña. Si tiene varias suscripciones de Azure, use `azure account set <subscriptionname>` use comandos de suscripción de hello tooset que Hola CLI de Azure.

2. Cambiar el modo de administrador de recursos de tooAzure con hello siguiente comando:

        azure config mode arm

3. Cree un grupo de recursos. Este grupo de recursos contiene el clúster de HDInsight de Hola y asociados de cuenta de almacenamiento.

        azure group create groupname location

    * Reemplace `groupname` con un nombre único para el grupo de Hola.

    * Reemplace `location` con la región geográfica de Hola que desee toocreate hello en.

       Para obtener una lista de ubicaciones válidas, usar hello `azure location list` comando y, a continuación, utilice una de las ubicaciones de Hola de hello `Name` columna.

4. Cree una cuenta de almacenamiento. Esta cuenta de almacenamiento se utiliza como almacenamiento predeterminado de hello para el clúster de HDInsight Hola.

        azure storage account create -g groupname --sku-name RAGRS -l location --kind Storage storagename

    * Reemplace `groupname` con el nombre de hello del grupo de hello creado en el paso anterior de Hola.

    * Reemplace `location` con la misma ubicación que se utilizó en el paso anterior de Hola de Hola.

    * Reemplace `storagename` con un nombre único para la cuenta de almacenamiento de Hola.

        > [!NOTE]
        > Para obtener más información sobre los parámetros de hello utilizados en este comando, use `azure storage account create -h` tooview ayuda para este comando.

5. Recuperar la cuenta de almacenamiento de Hola Hola clave tooaccess usado.

        azure storage account keys list -g groupname storagename

    * Reemplace `groupname` con el nombre de grupo de recursos de Hola.
    * Reemplace `storagename` con el nombre de Hola de cuenta de almacenamiento de Hola.

     En datos de Hola que se devuelven, guardar hello `key` valor `key1`.

6. Cree un clúster de HDInsight.

        azure hdinsight cluster create -g groupname -l location -y Linux --clusterType Hadoop --defaultStorageAccountName storagename.blob.core.windows.net --defaultStorageAccountKey storagekey --defaultStorageContainer clustername --workerNodeCount 3 --userName admin --password httppassword --sshUserName sshuser --sshPassword sshuserpassword clustername

    * Reemplace `groupname` con el nombre de grupo de recursos de Hola.

    * Reemplace `Hadoop` con el tipo de clúster de Hola que desea toocreate. Por ejemplo, `Hadoop`, `HBase`, `Kafka`, `Spark` o `Storm`.

     > [!IMPORTANT]
     > HDInsight clústeres proceden de diversos tipos, que corresponden a cargas de trabajo de toohello o tecnología de Hola clúster se optimiza para. No hay ningún toocreate método admitido para un clúster que combina varios tipos, como Storm y HBase en un clúster.

    * Reemplace `location` con hello misma ubicación que se usa en los pasos anteriores.

    * Reemplace `storagename` con el nombre de cuenta de almacenamiento de Hola.

    * Reemplace `storagekey` con clave de hello obtenido en el paso anterior de Hola.

    * Para hello `--defaultStorageContainer` parámetro, Hola uso mismo nombre que se utilizan para clúster Hola.

    * Reemplace `admin` y `httppassword` con hello nombre y la contraseña que se va toouse al tener acceso a los clústeres de Hola a través de HTTPS.

    * Reemplace `sshuser` y `sshuserpassword` con hello username y password desea toouse al tener acceso a clúster de hello mediante SSH

    > [!IMPORTANT]
    > En este ejemplo se crea un clúster con dos nodos de trabajo. También puede cambiar número de Hola de nodos de trabajo después de la creación de clúster mediante la realización de operaciones de escala. Si planea usar más de 32 nodos de trabajo, tiene que seleccionar un tamaño de nodo principal con al menos 8 núcleos y 14 GB de RAM. Puede establecer el tamaño del nodo principal de hello mediante hello `--headNodeSize` parámetro durante la creación del clúster.
    >
    > Para obtener más información acerca de los tamaños de nodo y los costos asociados, consulte [Precios de HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

    Puede tardar varios minutos para toofinish de proceso de creación de clúster de Hola. de creación del clúster.

## <a name="troubleshoot"></a>Solución de problemas

Si experimenta problemas con la creación de clústeres de HDInsight, consulte los [requisitos de control de acceso](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha creado correctamente un clúster de HDInsight con hello CLI de Azure, use Hola sigue toolearn cómo toowork con el clúster:

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
