---
title: "Requisitos previos para replicación de servidor físico en Azure con Azure Site Recovery | Microsoft Docs"
description: "Resume los pasos necesarios para configurar un almacén para la replicación de servidores físicos en Azure con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99f2605-f417-4995-be77-5323136b814f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: deb5ad0495edc969b374795eeb2698326dd4ff4d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="step-6-set-up-a-vault-for-physical-server-replication-to-azure"></a><span data-ttu-id="9b426-103">Paso 6: Configuración de un almacén para la replicación de servidor físico en Azure</span><span class="sxs-lookup"><span data-stu-id="9b426-103">Step 6: Set up a vault for physical server replication to Azure</span></span>


<span data-ttu-id="9b426-104">En este artículo se describe cómo configurar un almacén.</span><span class="sxs-lookup"><span data-stu-id="9b426-104">This article describes how to set up a vault.</span></span> <span data-ttu-id="9b426-105">Cree un almacén y especifique qué se desea replicar desde la ubicación local en Azure mediante el servicio [Azure Site Recovery](site-recovery-overview.md) en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="9b426-105">You create the vault, and specify what you want to replicate from your on-premises location to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="9b426-106">Publique cualquier comentario o pregunta en la parte inferior de este artículo, o bien en el [foro de Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="9b426-106">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="9b426-107">Creación de un almacén de Servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="9b426-107">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a><span data-ttu-id="9b426-108">Selección de un objetivo de protección</span><span class="sxs-lookup"><span data-stu-id="9b426-108">Select a protection goal</span></span>

<span data-ttu-id="9b426-109">Seleccione aquello que desea replicar y la ubicación donde se va a realizar la replicación.</span><span class="sxs-lookup"><span data-stu-id="9b426-109">Select what you want to replicate, and where you want to replicate to.</span></span>

1. <span data-ttu-id="9b426-110">Haga clic en **Almacenes de Recovery Services** > almacén.</span><span class="sxs-lookup"><span data-stu-id="9b426-110">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="9b426-111">En el menú de recursos, haga clic en **Site Recovery** > **Preparar la infraestructura** > **Objetivo de protección**.</span><span class="sxs-lookup"><span data-stu-id="9b426-111">In the Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="9b426-112">En **Objetivo de protección**, seleccione **En Azure** > **No virtualizado/Otro**.</span><span class="sxs-lookup"><span data-stu-id="9b426-112">In **Protection goal**, select **To Azure** > **Not virtualized/Other**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="9b426-113">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9b426-113">Next steps</span></span>

<span data-ttu-id="9b426-114">Vaya a [Paso 7: Configuración de los valores de origen y destino](physical-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="9b426-114">Go to [Step 7: Set up source and target](physical-walkthrough-source-target.md)</span></span>
