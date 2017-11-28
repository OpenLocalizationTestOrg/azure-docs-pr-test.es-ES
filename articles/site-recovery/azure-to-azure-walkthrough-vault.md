---
title: "Configuración de un almacén para la replicación de VM de Azure entre regiones con Azure Site Recovery | Microsoft Docs"
description: "Se resumen los pasos que hay que seguir para configurar un almacén para la replicación de Azure entre regiones de Azure con Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 40472189-3d80-4963-b175-8bddcbc2f61f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: e03d17992ee0b12049636e40188950bcc4a6f31e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="step-4-set-up-a-vault-for-azure-to-azure-replication"></a><span data-ttu-id="3ee17-103">Paso 4: Configuración de un almacén de Azure para realizar la replicación de Azure</span><span class="sxs-lookup"><span data-stu-id="3ee17-103">Step 4: Set up a vault for Azure to Azure replication</span></span>

<span data-ttu-id="3ee17-104">Después de [planear redes](azure-to-azure-walkthrough-network.md), use este artículo para configurar un almacén para máquinas virtuales (VM) de Azure que realizan la replicación en otra región de Azure mediante el servicio [Azure Site Recovery](site-recovery-overview.md) en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3ee17-104">After [planning networks](azure-to-azure-walkthrough-network.md), use this article to set up a vault, for Azure virtual machines (VMs) replicating to another Azure region, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

- <span data-ttu-id="3ee17-105">Cuando termine el artículo, debe tener un almacén de Recovery Services configurado.</span><span class="sxs-lookup"><span data-stu-id="3ee17-105">When you finish the article, you should have a Recovery Services vault set up.</span></span>
- <span data-ttu-id="3ee17-106">Publique cualquier comentario en la parte inferior de este artículo, o bien en el [foro de Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="3ee17-106">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



>[!NOTE]
>
> <span data-ttu-id="3ee17-107">La replicación de VM de Azure se encuentra en una versión preliminar en este momento.</span><span class="sxs-lookup"><span data-stu-id="3ee17-107">Azure VM replication is currently in preview.</span></span>




## <a name="create-a-vault"></a><span data-ttu-id="3ee17-108">Creación de un almacén</span><span class="sxs-lookup"><span data-stu-id="3ee17-108">Create a vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="3ee17-109">Le recomendamos que cree el almacén de Recovery Services en la ubicación donde quiere que se repliquen las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="3ee17-109">We recommend that you create the Recovery Services vault in the location where you want your VMs to replicate.</span></span> <span data-ttu-id="3ee17-110">Por ejemplo, si la ubicación de destino está en el centro de EE. UU., crear el almacén en **Centro de EE. UU**.</span><span class="sxs-lookup"><span data-stu-id="3ee17-110">For example, if your target location is the central US, create the vault in **Central US**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3ee17-111">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3ee17-111">Next steps</span></span>

<span data-ttu-id="3ee17-112">Vaya a [Paso 5: Habilitación de la replicación](azure-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="3ee17-112">Go to [Step 5: Enable replication](azure-to-azure-walkthrough-enable-replication.md)</span></span>
