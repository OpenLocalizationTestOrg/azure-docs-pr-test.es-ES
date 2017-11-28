---
title: "Requisitos previos para replicación de VMware en Azure con Azure Site Recovery | Microsoft Docs"
description: "Se resumen los pasos que hay que seguir para habilitar la replicación en Azure de máquinas virtuales VMware con el servicio Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8bce940e-f19f-4418-8360-aee7b073519a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: dca95ad46b8de587140c3573ba6ed5702a122032
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="step-7-set-up-a-vault-for-vmware-replication-to-azure"></a><span data-ttu-id="51c6a-103">Paso 7: Configuración de un almacén para la replicación de VMware en Azure</span><span class="sxs-lookup"><span data-stu-id="51c6a-103">Step 7: Set up a vault for VMware replication to Azure</span></span>


<span data-ttu-id="51c6a-104">En este artículo, se describe cómo configurar un almacén y especificar lo que se quiere replicar en la ubicación local en Azure con el servicio [Azure Site Recovery](site-recovery-overview.md) en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="51c6a-104">This article describes how to set up a vault, and specify what you want to replicate from your on-premises location, to Azure using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="51c6a-105">Publique cualquier comentario o pregunta en la parte inferior de este artículo, o bien en el [foro de Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="51c6a-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="51c6a-106">Creación de un almacén de Servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="51c6a-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a><span data-ttu-id="51c6a-107">Selección de un objetivo de protección</span><span class="sxs-lookup"><span data-stu-id="51c6a-107">Select a protection goal</span></span>

<span data-ttu-id="51c6a-108">Seleccione aquello que desea replicar y la ubicación donde se va a realizar la replicación.</span><span class="sxs-lookup"><span data-stu-id="51c6a-108">Select what you want to replicate, and where you want to replicate to.</span></span>

1. <span data-ttu-id="51c6a-109">Haga clic en **Almacenes de Recovery Services** > almacén.</span><span class="sxs-lookup"><span data-stu-id="51c6a-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="51c6a-110">En el menú de recursos, haga clic en **Site Recovery** > **Preparar la infraestructura** > **Objetivo de protección**.</span><span class="sxs-lookup"><span data-stu-id="51c6a-110">In the Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="51c6a-111">En **Objetivo de protección**, seleccione **To Azure (En Azure)** > **Yes, with VMware vSphere Hypervisor** (Sí, con VMware vSphere Hypervisor).</span><span class="sxs-lookup"><span data-stu-id="51c6a-111">In **Protection goal**, select **To Azure** > **Yes, with VMware vSphere Hypervisor**.</span></span>



## <a name="next-steps"></a><span data-ttu-id="51c6a-112">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="51c6a-112">Next steps</span></span>

<span data-ttu-id="51c6a-113">Vaya al [paso 8: configuración de los valores de origen y destino](vmware-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="51c6a-113">Go to [Step 8: Set up source and target](vmware-walkthrough-source-target.md)</span></span>
