---
title: "Eliminación de un clúster de HDInsight - Azure | Microsoft Docs"
description: "Información sobre las distintas formas de eliminar un clúster de HDInsight."
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
ms.openlocfilehash: 65dac529df15d2dd43eec17673d82a2832f7692e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="delete-an-hdinsight-cluster-using-your-browser-powershell-or-the-azure-cli"></a><span data-ttu-id="df487-103">Eliminación de un clúster de HDInsight con el explorador, PowerShell o la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="df487-103">Delete an HDInsight cluster using your browser, PowerShell, or the Azure CLI</span></span>

<span data-ttu-id="df487-104">La facturación del clúster de HDInsight se inicia una vez creado el clúster y solo se detiene cuando se elimina.</span><span class="sxs-lookup"><span data-stu-id="df487-104">HDInsight cluster billing starts once a cluster is created and stops when the cluster is deleted.</span></span> <span data-ttu-id="df487-105">Se facturan por minuto realizando una prorrata, por lo que siempre debe eliminar aquellos que ya no se estén utilizando.</span><span class="sxs-lookup"><span data-stu-id="df487-105">Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use.</span></span> <span data-ttu-id="df487-106">En este documento, aprenderá a eliminar un clúster mediante el portal de Azure, Azure PowerShell y la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="df487-106">In this document, you learn how to delete a cluster using the Azure portal, Azure PowerShell, and the Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="df487-107">Al eliminar un clúster de HDInsight, no se eliminan las cuentas de Azure Storage o Data Lake Store asociadas a este.</span><span class="sxs-lookup"><span data-stu-id="df487-107">Deleting an HDInsight cluster does not delete the Azure Storage accounts or Data Lake Store associated with the cluster.</span></span> <span data-ttu-id="df487-108">Puede volver a usar los datos almacenados en esos servicios en el futuro.</span><span class="sxs-lookup"><span data-stu-id="df487-108">You can reuse data stored in those services in the future.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="df487-109">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="df487-109">Azure portal</span></span>

1. <span data-ttu-id="df487-110">Inicie sesión en [Azure Portal](https://portal.azure.com) y seleccione su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="df487-110">Log in to the [Azure portal](https://portal.azure.com) and select your HDInsight cluster.</span></span> <span data-ttu-id="df487-111">Si este no está anclado al panel, puede buscarlo por su nombre utilizando el campo de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="df487-111">If your HDInsight cluster is not pinned to the dashboard, you can search for it by name using the search field.</span></span>
   
    ![búsqueda del portal](./media/hdinsight-delete-cluster/navbar.png)

2. <span data-ttu-id="df487-113">Una vez que se abra la hoja para el clúster, seleccione el icono **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="df487-113">Once the blade opens for the cluster, select the **Delete** icon.</span></span> <span data-ttu-id="df487-114">Cuando se le pida, seleccione **Sí** para eliminar el clúster.</span><span class="sxs-lookup"><span data-stu-id="df487-114">When prompted, select **Yes** to delete the cluster.</span></span>
   
    ![eliminar icono](./media/hdinsight-delete-cluster/deletecluster.png)

## <a name="azure-powershell"></a><span data-ttu-id="df487-116">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="df487-116">Azure PowerShell</span></span>

<span data-ttu-id="df487-117">Desde un símbolo del sistema de PowerShell, utilice el siguiente comando para eliminar el clúster:</span><span class="sxs-lookup"><span data-stu-id="df487-117">From a PowerShell prompt, use the following command to delete the cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName CLUSTERNAME

<span data-ttu-id="df487-118">Reemplace **CLUSTERNAME** por el nombre del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="df487-118">Replace **CLUSTERNAME** with the name of your HDInsight cluster.</span></span>

## <a name="azure-cli-10"></a><span data-ttu-id="df487-119">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="df487-119">Azure CLI 1.0</span></span>

<span data-ttu-id="df487-120">Desde un símbolo del sistema, utilice el siguiente comando para eliminar el clúster:</span><span class="sxs-lookup"><span data-stu-id="df487-120">From a prompt, use the following to delete the cluster:</span></span>

    azure hdinsight cluster delete CLUSTERNAME

<span data-ttu-id="df487-121">Reemplace **CLUSTERNAME** por el nombre del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="df487-121">Replace **CLUSTERNAME** with the name of your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="df487-122">CLI de Azure 2.0 no admite la eliminación de clústeres de HDInsight en la actualidad (31 de julio de 2017).</span><span class="sxs-lookup"><span data-stu-id="df487-122">Azure CLI 2.0 does not support deleting HDInsight clusters at this time (July 31, 2017).</span></span>