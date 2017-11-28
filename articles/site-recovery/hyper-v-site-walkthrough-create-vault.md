---
title: "Configurar un almacén para la replicación de Hyper-V (sin System Center VMM) en Azure con Azure Site Recovery | Microsoft Docs"
description: "Resume los pasos necesarios para configurar un almacén para la replicación de Hyper-V en Azure con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a936b3e2-0dbe-47ac-a98e-5285d96dc786
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 8212ff011633c3a89d3310e828b6d5f1cda6ce3f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="step-7-set-up-a-vault-for-hyper-v-replication"></a><span data-ttu-id="50251-103">Paso 7: configuración de un almacén para la replicación de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="50251-103">Step 7: Set up a vault for Hyper-V replication</span></span>

<span data-ttu-id="50251-104">Este artículo describe cómo configurar un almacén y especificar qué se desea replicar desde la ubicación local en Azure mediante el servicio [Azure Site Recovery](site-recovery-overview.md) en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="50251-104">This article describes how to set up a vault, and specify what you want to replicate from your on-premises location, to Azure using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="50251-105">Publique cualquier comentario o pregunta en la parte inferior de este artículo, o bien en el [foro de Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="50251-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="50251-106">Creación de un almacén de Servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="50251-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]



## <a name="select-a-protection-goal"></a><span data-ttu-id="50251-107">Selección de un objetivo de protección</span><span class="sxs-lookup"><span data-stu-id="50251-107">Select a protection goal</span></span>

<span data-ttu-id="50251-108">Seleccione aquello que desea replicar y la ubicación donde se va a realizar la replicación.</span><span class="sxs-lookup"><span data-stu-id="50251-108">Select what you want to replicate, and where you want to replicate to.</span></span>

1. <span data-ttu-id="50251-109">Haga clic en **Almacenes de Recovery Services** > almacén.</span><span class="sxs-lookup"><span data-stu-id="50251-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="50251-110">En el menú de recursos, haga clic en **Site Recovery** > **Preparar la infraestructura** > **Objetivo de protección**.</span><span class="sxs-lookup"><span data-stu-id="50251-110">In the Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="50251-111">En **Objetivo de protección**, seleccione **En Azure** > **Sí, con Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="50251-111">In **Protection goal**, select **To Azure** > **Yes, with Hyper-V**.</span></span> <span data-ttu-id="50251-112">Seleccione **No** para confirmar que no usa VMM.</span><span class="sxs-lookup"><span data-stu-id="50251-112">Select **No** to confirm you're not using VMM.</span></span> 

    ![Elegir objetivos](./media/hyper-v-site-walkthrough-create-vault/choose-goals2.png)



## <a name="next-steps"></a><span data-ttu-id="50251-114">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="50251-114">Next steps</span></span>

<span data-ttu-id="50251-115">Vaya al [paso 8: configuración de los valores de origen y destino](hyper-v-site-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="50251-115">Go to [Step 8: Set up source and target](hyper-v-site-walkthrough-source-target.md)</span></span>
