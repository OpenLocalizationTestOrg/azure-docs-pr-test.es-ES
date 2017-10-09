---
title: "clúster de Hadoop aaaCreate con cuentas de almacenamiento de transferencia segura de HDInsight de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo los clústeres de HDInsight de toocreate con transferencia segura habilita las cuentas de almacenamiento de Azure."
keywords: "introducción a hadoop,hadoop linux,inicio rápido de hadoop,transferencia segura,cuenta de almacenamiento de azure"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: jgao
ms.openlocfilehash: 0acb8814ad0d5d5b5652d930b2e3da90f9d7978d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-cluster-with-secure-transfer-storage-accounts-in-azure-hdinsight"></a>Creación de un clúster de Hadoop con cuentas de almacenamiento de transferencia segura en Azure HDInsight

Hola [proteger la transferencia se necesitan](../storage/common/storage-require-secure-transfer.md) característica mejora la seguridad de saludo de la cuenta de almacenamiento de Azure mediante la aplicación de todas las solicitudes tooyour cuenta a través de una conexión segura. Este esquema wasbs hello y la característica solo son compatibles con la versión de clúster de HDInsight 3,6 o versiones más reciente. 

## <a name="prerequisites"></a>Requisitos previos
Antes de empezar este tutorial, debe contar con lo siguiente:

* **Suscripción de Azure**: toocreate una cuenta de evaluación gratuita de un mes, examinar demasiado[azure.microsoft.com/free](https://azure.microsoft.com/free).
* **Una cuenta de Azure Storage habilitada para transferencia segura**. Para obtener instrucciones de hello, consulte [crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account) y [exigir la transferencia segura](../storage/common/storage-require-secure-transfer.md).
* **Un contenedor de blobs en la cuenta de almacenamiento de hello**. 
## <a name="create-cluster"></a>Crear clúster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]


En esta sección, se crea un clúster de Hadoop en HDInsight mediante una [plantilla de Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md). plantilla de Hola se encuentra en [Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/). No es necesario tener experiencia en el uso de la plantilla de Resource Manager para seguir este tutorial. Para otros métodos de creación del clúster y la comprensión de propiedades de hello usados en este tutorial, vea [HDInsight crear clústeres](hdinsight-hadoop-provision-linux-clusters.md).

1. Haga clic en hello siguientes toosign de imagen en tooAzure y plantilla de administrador de recursos abiertos Hola Hola portal de Azure. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-existing-default-storage-account%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. Sigue las instrucciones de hello toocreate clúster de hello con hello siguiendo las especificaciones: 

    - Especifique la versión 3.6 de HDInsight.  versión predeterminada de Hello es 3.5. Se requiere la versión 3.6 o posterior.
    - Especifique una cuenta de almacenamiento habilitada para transferencia.
    - Utilice el nombre corto para la cuenta de almacenamiento de Hola.
    - Cuenta de almacenamiento de Hola y el contenedor de blobs de hello deben crearse con antelación. 

    Para obtener instrucciones de hello, consulte [crear un clúster](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster). 

Si usas tooprovide de acción de secuencia de comandos en sus propios archivos de configuración, debe utilizar wasbs Hola después de configuración:

- fs.defaultFS (sitio principal)
- spark.eventLog.dir 
- spark.history.fs.logDirectory

## <a name="add-additional-storage-accounts"></a>Adición de cuentas de almacenamiento adicionales

Hay varias opciones tooadd transferencia segura adicional habilitada almacenamiento cuentas:

- Modificar plantilla de Azure Resource Manager hello en la última sección de Hola.
- Crear un clúster mediante hello [portal de Azure](https://portal.azure.com) y especifique la cuenta de almacenamiento vinculada.
- Usar script acción tooadd adicional segura habilitado para transferencia de clúster de HDInsight existente de tooan de cuentas de almacenamiento.  Para obtener más información, consulte [agregar almacenamiento adicional cuentas tooHDInsight](hdinsight-hadoop-add-storage.md).

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha aprendido cómo toocreate un clúster de HDInsight y habilitar seguro de transferencia de las cuentas de almacenamiento de toohello.

toolearn más información acerca de análisis de datos con HDInsight, vea Hola siguientes artículos:

* toolearn más sobre el uso de Hive con HDInsight, incluido cómo las consultas tooperform Hive desde Visual Studio, vea [uso de Hive con HDInsight][hdinsight-use-hive].
* toolearn sobre Pig, datos tootransform de usar un idioma, vea [uso de Pig con HDInsight][hdinsight-use-pig].
* toolearn sobre MapReduce, una manera toowrite los programas que procesan datos en Hadoop, vea [MapReduce de uso con HDInsight][hdinsight-use-mapreduce].
* toolearn sobre el uso de herramientas de HDInsight de Hola para los datos de Visual Studio tooanalyze en HDInsight, vea [Introducción al uso de Hadoop de Visual Studio tools para HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).

más información acerca de cómo HDInsight almacena datos toolearn o datos tooget en HDInsight, vea Hola siguientes artículos:

* Para más información sobre cómo HDInsight usa Azure Storage, consulte [Uso de Azure Storage con HDInsight](hdinsight-hadoop-use-blob-storage.md).
* Para obtener información acerca de cómo tooupload tooHDInsight de datos, vea [cargar datos tooHDInsight][hdinsight-upload-data].

toolearn más información acerca de crear o administrar un clúster de HDInsight, vea Hola siguientes artículos:

* toolearn acerca de cómo administrar el clúster de HDInsight basados en Linux, consulte [HDInsight administrar clústeres con Ambari](hdinsight-hadoop-manage-ambari.md).
* toolearn más información acerca de las opciones de Hola que puede seleccionar al crear un clúster de HDInsight, vea [HDInsight crear en Linux con opciones personalizadas](hdinsight-hadoop-provision-linux-clusters.md).
* Si está familiarizado con Linux y Hadoop, pero desea tooknow detalles acerca de Hadoop en HDInsight de hello, consulte [trabajar con HDInsight en Linux](hdinsight-hadoop-linux-information.md). Este artículo proporciona información como:
  
  * Direcciones URL para los servicios hospedados en clúster de hello, por ejemplo, Ambari y WebHCat
  * ubicación de Hola de ejemplos en el sistema de archivos local de Hola y archivos de Hadoop
  * uso de Hola de Azure Storage (WASB) en lugar de HDFS como almacén de datos predeterminado de Hola

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


