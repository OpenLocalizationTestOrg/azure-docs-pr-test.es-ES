---
title: "clústeres de Hadoop de aaaManage mediante Azure CLI - HDInsight de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo los clústeres de toomanage de interfaz de línea de comandos de Azure de hello toouse Hadoop en HDInsight de Azure. Hola CLI de Azure funciona en Windows, Mac y Linux."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: 4f26c79f-8540-44bd-a470-84722a9e4eca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 03b0cff9331c1c581095b80cc6d1177d843ffa83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-using-hello-azure-cli"></a>Administrar clústeres de Hadoop en HDInsight con hello CLI de Azure
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Obtenga información acerca de cómo hello toouse [interfaz de línea de comandos de Azure](../cli-install-nodejs.md) clústeres de toomanage Hadoop en HDInsight de Azure. Hola CLI de Azure se implementa en Node.js. y se puede usar en cualquier plataforma compatible con Node.js, entre las que se incluyen Windows, Mac y Linux.

Este artículo se tratan únicamente con hello CLI de Azure con HDInsight. Para obtener una guía general acerca de cómo toouse CLI de Azure, consulte [instalar y configurar Azure CLI][azure-command-line-tools].

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

## <a name="prerequisites"></a>Requisitos previos
Antes de comenzar este artículo, debe tener el siguiente hello:

* **Una suscripción de Azure**. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **CLI de Azure** -vea [instalar y configurar hello Azure CLI](../cli-install-nodejs.md) para obtener información de instalación y configuración.
* **Conectar tooAzure**con Hola comando siguiente:
  
        azure login
  
    Para obtener más información acerca de cómo autenticar con una cuenta profesional o educativa, consulte [conectarse tooan suscripción de Azure desde hello Azure CLI](../xplat-cli-connect.md).
* **Modo del conmutador toohello Azure Resource Manager**con Hola comando siguiente:
  
        azure config mode arm

Ayuda de tooget, usar hello **-h** cambiar.  Por ejemplo:

    azure hdinsight cluster create -h

## <a name="create-clusters-with-hello-cli"></a>Crear clústeres con hello CLI
Vea [crear clústeres de HDInsight utilizando hello Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).

## <a name="list-and-show-cluster-details"></a>Enumeración y visualización de los detalles del clúster
Usar hello después a toolist de comandos y mostrar los detalles del clúster:

    azure hdinsight cluster list
    azure hdinsight cluster show <Cluster Name>

![Vista de línea de comandos de la lista de clústeres][image-cli-clusterlisting]

## <a name="delete-clusters"></a>Eliminación de clústeres
Usar hello después comando toodelete un clúster:

    azure hdinsight cluster delete <Cluster Name>

También puede eliminar un clúster mediante la eliminación de grupo de recursos de Hola que contiene el clúster de Hola. Tenga en cuenta, se eliminarán todos los recursos de hello en grupo de hello incluidas cuenta de almacenamiento predeterminada de Hola.

    azure group delete <Resource Group Name>

## <a name="scale-clusters"></a>Escalado de clústeres
Hola toochange tamaño de clúster de Hadoop:

    azure hdinsight cluster resize [options] <clusterName> <Target Instance Count>


## <a name="enabledisable-http-access-for-a-cluster"></a>Habilitar/deshabilitar el acceso HTTP para un clúster
    azure hdinsight cluster enable-http-access [options] <Cluster Name> <userName> <password>
    azure hdinsight cluster disable-http-access [options] <Cluster Name>

## <a name="enabledisable-rdp-access-for-a-cluster"></a>Habilitar/deshabilitar el acceso RDP para un clúster
      azure hdinsight cluster enable-rdp-access [options] <Cluster Name> <rdpUserName> <rdpPassword> <rdpExpiryDate>
      azure hdinsight cluster disable-rdp-access [options] <Cluster Name>


## <a name="next-steps"></a>Pasos siguientes
En este artículo, ha aprendido cómo tooperform diferentes HDInsight clúster tareas administrativas. toolearn más información, vea Hola siguientes artículos:

* [Administrar HDInsight mediante Hola Portal de Azure][hdinsight-admin-portal]
* [Administración de HDInsight con Azure PowerShell][hdinsight-admin-powershell]
* [Introducción a Azure HDInsight][hdinsight-get-started]
* [¿Cómo toouse Hola CLI de Azure][azure-command-line-tools]

[azure-command-line-tools]: ../cli-install-nodejs.md
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/


[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[image-cli-account-download-import]: ./media/hdinsight-administer-use-command-line/HDI.CLIAccountDownloadImport.png
[image-cli-clustercreation]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreation.png
[image-cli-clustercreation-config]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreationConfig.png
[image-cli-clusterlisting]: ./media/hdinsight-administer-use-command-line/command-line-list-of-clusters.png "Enumeración y visualización de clústeres"
