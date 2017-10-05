---
title: "Configurar un almacén para la replicación de Hyper-V (con System Center VMM) en Azure con Azure Site Recovery | Microsoft Docs"
description: "Resume los pasos necesarios para configurar un almacén para la replicación de Hyper-V (con VMM) en Azure con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: b3cd6f03-c33c-406d-91d4-5cba69f79abd
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: af453ec27ba15ad8c59cf9f544584ad18dc0f74a
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2017
---
# <a name="step-7-set-up-a-vault-for-hyper-v-replication"></a><span data-ttu-id="715f7-103">Paso 7: configuración de un almacén para la replicación de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="715f7-103">Step 7: Set up a vault for Hyper-V replication</span></span>

<span data-ttu-id="715f7-104">Este artículo describe cómo configurar un almacén y especificar qué se desea replicar desde la ubicación local en Azure mediante el servicio [Azure Site Recovery](site-recovery-overview.md) en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="715f7-104">This article describes how to set up a vault, and specify what you want to replicate from your on-premises location, to Azure using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="715f7-105">Publique cualquier comentario o pregunta en la parte inferior de este artículo, o bien en el [foro de Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="715f7-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="715f7-106">Creación de un almacén de Servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="715f7-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]



## <a name="select-a-protection-goal"></a><span data-ttu-id="715f7-107">Selección de un objetivo de protección</span><span class="sxs-lookup"><span data-stu-id="715f7-107">Select a protection goal</span></span>

<span data-ttu-id="715f7-108">Seleccione aquello que desea replicar y la ubicación donde se va a realizar la replicación.</span><span class="sxs-lookup"><span data-stu-id="715f7-108">Select what you want to replicate, and where you want to replicate to.</span></span>

1. <span data-ttu-id="715f7-109">Haga clic en **Almacenes de Recovery Services** > almacén.</span><span class="sxs-lookup"><span data-stu-id="715f7-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="715f7-110">En el menú de recursos, haga clic en **Site Recovery** > **Preparar la infraestructura** > **Objetivo de protección**.</span><span class="sxs-lookup"><span data-stu-id="715f7-110">In the Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="715f7-111">En **Objetivo de protección**, seleccione **En Azure** > **Sí, con Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="715f7-111">In **Protection goal**, select **To Azure** > **Yes, with Hyper-V**.</span></span> <span data-ttu-id="715f7-112">Seleccione **Sí** para confirmar que usa VMM.</span><span class="sxs-lookup"><span data-stu-id="715f7-112">Select **Yes** to confirm you're nusing VMM.</span></span> 

     ![Elegir objetivos](./media/vmm-to-azure-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a><span data-ttu-id="715f7-114">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="715f7-114">Next steps</span></span>

<span data-ttu-id="715f7-115">Vaya al [paso 8: configuración de los valores de origen y destino](vmm-to-azure-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="715f7-115">Go to [Step 8: Set up source and target](vmm-to-azure-walkthrough-source-target.md)</span></span>
