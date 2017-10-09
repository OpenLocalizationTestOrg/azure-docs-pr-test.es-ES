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
# <a name="manage-hadoop-clusters-in-hdinsight-using-hello-azure-cli"></a><span data-ttu-id="c6e52-104">Administrar clústeres de Hadoop en HDInsight con hello CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="c6e52-104">Manage Hadoop clusters in HDInsight using hello Azure CLI</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="c6e52-105">Obtenga información acerca de cómo hello toouse [interfaz de línea de comandos de Azure](../cli-install-nodejs.md) clústeres de toomanage Hadoop en HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="c6e52-105">Learn how toouse hello [Azure Command-line Interface](../cli-install-nodejs.md) toomanage Hadoop clusters in Azure HDInsight.</span></span> <span data-ttu-id="c6e52-106">Hola CLI de Azure se implementa en Node.js.</span><span class="sxs-lookup"><span data-stu-id="c6e52-106">hello Azure CLI is implemented in Node.js.</span></span> <span data-ttu-id="c6e52-107">y se puede usar en cualquier plataforma compatible con Node.js, entre las que se incluyen Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="c6e52-107">It can be used on any platform that supports Node.js, including Windows, Mac, and Linux.</span></span>

<span data-ttu-id="c6e52-108">Este artículo se tratan únicamente con hello CLI de Azure con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c6e52-108">This article covers only using hello Azure CLI with HDInsight.</span></span> <span data-ttu-id="c6e52-109">Para obtener una guía general acerca de cómo toouse CLI de Azure, consulte [instalar y configurar Azure CLI][azure-command-line-tools].</span><span class="sxs-lookup"><span data-stu-id="c6e52-109">For a general guide on how toouse Azure CLI, see [Install and configure Azure CLI][azure-command-line-tools].</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

## <a name="prerequisites"></a><span data-ttu-id="c6e52-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c6e52-110">Prerequisites</span></span>
<span data-ttu-id="c6e52-111">Antes de comenzar este artículo, debe tener el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="c6e52-111">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="c6e52-112">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="c6e52-112">**An Azure subscription**.</span></span> <span data-ttu-id="c6e52-113">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="c6e52-113">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="c6e52-114">**CLI de Azure** -vea [instalar y configurar hello Azure CLI](../cli-install-nodejs.md) para obtener información de instalación y configuración.</span><span class="sxs-lookup"><span data-stu-id="c6e52-114">**Azure CLI** - See [Install and configure hello Azure CLI](../cli-install-nodejs.md) for installation and configuration information.</span></span>
* <span data-ttu-id="c6e52-115">**Conectar tooAzure**con Hola comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="c6e52-115">**Connect tooAzure**, using hello following command:</span></span>
  
        azure login
  
    <span data-ttu-id="c6e52-116">Para obtener más información acerca de cómo autenticar con una cuenta profesional o educativa, consulte [conectarse tooan suscripción de Azure desde hello Azure CLI](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="c6e52-116">For more information on authenticating using a work or school account, see [Connect tooan Azure subscription from hello Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="c6e52-117">**Modo del conmutador toohello Azure Resource Manager**con Hola comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="c6e52-117">**Switch toohello Azure Resource Manager mode**, using hello following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="c6e52-118">Ayuda de tooget, usar hello **-h** cambiar.</span><span class="sxs-lookup"><span data-stu-id="c6e52-118">tooget help, use hello **-h** switch.</span></span>  <span data-ttu-id="c6e52-119">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c6e52-119">For example:</span></span>

    azure hdinsight cluster create -h

## <a name="create-clusters-with-hello-cli"></a><span data-ttu-id="c6e52-120">Crear clústeres con hello CLI</span><span class="sxs-lookup"><span data-stu-id="c6e52-120">Create clusters with hello CLI</span></span>
<span data-ttu-id="c6e52-121">Vea [crear clústeres de HDInsight utilizando hello Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c6e52-121">See [Create clusters in HDInsight using hello Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span></span>

## <a name="list-and-show-cluster-details"></a><span data-ttu-id="c6e52-122">Enumeración y visualización de los detalles del clúster</span><span class="sxs-lookup"><span data-stu-id="c6e52-122">List and show cluster details</span></span>
<span data-ttu-id="c6e52-123">Usar hello después a toolist de comandos y mostrar los detalles del clúster:</span><span class="sxs-lookup"><span data-stu-id="c6e52-123">Use hello following commands toolist and show cluster details:</span></span>

    azure hdinsight cluster list
    azure hdinsight cluster show <Cluster Name>

<span data-ttu-id="c6e52-124">![Vista de línea de comandos de la lista de clústeres][image-cli-clusterlisting]</span><span class="sxs-lookup"><span data-stu-id="c6e52-124">![Command-line view of cluster list][image-cli-clusterlisting]</span></span>

## <a name="delete-clusters"></a><span data-ttu-id="c6e52-125">Eliminación de clústeres</span><span class="sxs-lookup"><span data-stu-id="c6e52-125">Delete clusters</span></span>
<span data-ttu-id="c6e52-126">Usar hello después comando toodelete un clúster:</span><span class="sxs-lookup"><span data-stu-id="c6e52-126">Use hello following command toodelete a cluster:</span></span>

    azure hdinsight cluster delete <Cluster Name>

<span data-ttu-id="c6e52-127">También puede eliminar un clúster mediante la eliminación de grupo de recursos de Hola que contiene el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6e52-127">You can also delete a cluster by deleting hello resource group that contains hello cluster.</span></span> <span data-ttu-id="c6e52-128">Tenga en cuenta, se eliminarán todos los recursos de hello en grupo de hello incluidas cuenta de almacenamiento predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6e52-128">Please note, this will delete all hello resources in hello group including hello default storage account.</span></span>

    azure group delete <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="c6e52-129">Escalado de clústeres</span><span class="sxs-lookup"><span data-stu-id="c6e52-129">Scale clusters</span></span>
<span data-ttu-id="c6e52-130">Hola toochange tamaño de clúster de Hadoop:</span><span class="sxs-lookup"><span data-stu-id="c6e52-130">toochange hello Hadoop cluster size:</span></span>

    azure hdinsight cluster resize [options] <clusterName> <Target Instance Count>


## <a name="enabledisable-http-access-for-a-cluster"></a><span data-ttu-id="c6e52-131">Habilitar/deshabilitar el acceso HTTP para un clúster</span><span class="sxs-lookup"><span data-stu-id="c6e52-131">Enable/disable HTTP access for a cluster</span></span>
    azure hdinsight cluster enable-http-access [options] <Cluster Name> <userName> <password>
    azure hdinsight cluster disable-http-access [options] <Cluster Name>

## <a name="enabledisable-rdp-access-for-a-cluster"></a><span data-ttu-id="c6e52-132">Habilitar/deshabilitar el acceso RDP para un clúster</span><span class="sxs-lookup"><span data-stu-id="c6e52-132">Enable/disable RDP access for a cluster</span></span>
      azure hdinsight cluster enable-rdp-access [options] <Cluster Name> <rdpUserName> <rdpPassword> <rdpExpiryDate>
      azure hdinsight cluster disable-rdp-access [options] <Cluster Name>


## <a name="next-steps"></a><span data-ttu-id="c6e52-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c6e52-133">Next steps</span></span>
<span data-ttu-id="c6e52-134">En este artículo, ha aprendido cómo tooperform diferentes HDInsight clúster tareas administrativas.</span><span class="sxs-lookup"><span data-stu-id="c6e52-134">In this article, you have learned how tooperform different HDInsight cluster administrative tasks.</span></span> <span data-ttu-id="c6e52-135">toolearn más información, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="c6e52-135">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="c6e52-136">[Administrar HDInsight mediante Hola Portal de Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="c6e52-136">[Administer HDInsight by using hello Azure Portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="c6e52-137">[Administración de HDInsight con Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="c6e52-137">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="c6e52-138">[Introducción a Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="c6e52-138">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="c6e52-139">[¿Cómo toouse Hola CLI de Azure][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="c6e52-139">[How toouse hello Azure CLI][azure-command-line-tools]</span></span>

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
