---
title: "aaaHow toodelete un clúster de HDInsight - Azure | Documentos de Microsoft"
description: "Obtener información sobre Hola distintas formas que puede eliminar un clúster de HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 55f7838b-9786-47ff-96db-1b64437bd0bb
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 5b9d9a09eecfdcfaed7a1f5ebab440e13bd358b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="delete-an-hdinsight-cluster-using-your-browser-powershell-or-hello-azure-cli"></a><span data-ttu-id="fe29c-103">Eliminar un clúster de HDInsight con el explorador, PowerShell u Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="fe29c-103">Delete an HDInsight cluster using your browser, PowerShell, or hello Azure CLI</span></span>

<span data-ttu-id="fe29c-104">La facturación de clúster de HDInsight empieza cuando un clúster se crea y se detiene cuando se elimina el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="fe29c-104">HDInsight cluster billing starts once a cluster is created and stops when hello cluster is deleted.</span></span> <span data-ttu-id="fe29c-105">Se facturan por minuto realizando una prorrata, por lo que siempre debe eliminar aquellos que ya no se estén utilizando.</span><span class="sxs-lookup"><span data-stu-id="fe29c-105">Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use.</span></span> <span data-ttu-id="fe29c-106">En este documento, aprenderá cómo toodelete un clúster con Hola portal de Azure y Azure PowerShell, Hola 1.0 de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="fe29c-106">In this document, you learn how toodelete a cluster using hello Azure portal, Azure PowerShell, and hello Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fe29c-107">Eliminación de un clúster de HDInsight no elimina las cuentas de almacenamiento de Azure de Hola o almacén de Data Lake asociado con el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="fe29c-107">Deleting an HDInsight cluster does not delete hello Azure Storage accounts or Data Lake Store associated with hello cluster.</span></span> <span data-ttu-id="fe29c-108">Puede volver a usar los datos almacenados en esos servicios Hola futuras.</span><span class="sxs-lookup"><span data-stu-id="fe29c-108">You can reuse data stored in those services in hello future.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="fe29c-109">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="fe29c-109">Azure portal</span></span>

1. <span data-ttu-id="fe29c-110">Inicie sesión en toohello [portal de Azure](https://portal.azure.com) y seleccione el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fe29c-110">Log in toohello [Azure portal](https://portal.azure.com) and select your HDInsight cluster.</span></span> <span data-ttu-id="fe29c-111">Si su clúster de HDInsight no está anclado toohello panel, puede buscarlo por nombre mediante el campo de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="fe29c-111">If your HDInsight cluster is not pinned toohello dashboard, you can search for it by name using hello search field.</span></span>
   
    ![búsqueda del portal](./media/hdinsight-delete-cluster/navbar.png)

2. <span data-ttu-id="fe29c-113">Una vez que abre hoja hello para el clúster de hello, seleccione hello **eliminar** icono.</span><span class="sxs-lookup"><span data-stu-id="fe29c-113">Once hello blade opens for hello cluster, select hello **Delete** icon.</span></span> <span data-ttu-id="fe29c-114">Cuando se le pida, seleccione **Sí** clúster de hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="fe29c-114">When prompted, select **Yes** toodelete hello cluster.</span></span>
   
    ![eliminar icono](./media/hdinsight-delete-cluster/deletecluster.png)

## <a name="azure-powershell"></a><span data-ttu-id="fe29c-116">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fe29c-116">Azure PowerShell</span></span>

<span data-ttu-id="fe29c-117">Desde un símbolo del sistema de PowerShell, use Hola después de clúster de hello toodelete de comando:</span><span class="sxs-lookup"><span data-stu-id="fe29c-117">From a PowerShell prompt, use hello following command toodelete hello cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName CLUSTERNAME

<span data-ttu-id="fe29c-118">Reemplace **CLUSTERNAME** con el nombre de Hola de su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fe29c-118">Replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>

## <a name="azure-cli-10"></a><span data-ttu-id="fe29c-119">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="fe29c-119">Azure CLI 1.0</span></span>

<span data-ttu-id="fe29c-120">Desde un símbolo del sistema, use Hola después de clúster de Hola toodelete:</span><span class="sxs-lookup"><span data-stu-id="fe29c-120">From a prompt, use hello following toodelete hello cluster:</span></span>

    azure hdinsight cluster delete CLUSTERNAME

<span data-ttu-id="fe29c-121">Reemplace **CLUSTERNAME** con el nombre de Hola de su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fe29c-121">Replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="fe29c-122">CLI de Azure 2.0 no admite la eliminación de clústeres de HDInsight en la actualidad (31 de julio de 2017).</span><span class="sxs-lookup"><span data-stu-id="fe29c-122">Azure CLI 2.0 does not support deleting HDInsight clusters at this time (July 31, 2017).</span></span>