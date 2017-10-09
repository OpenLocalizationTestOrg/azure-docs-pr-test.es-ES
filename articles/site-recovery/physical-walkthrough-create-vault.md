---
title: "aaaSet un almacén para tooAzure de replicación de servidor físico con Azure Site Recovery | Documentos de Microsoft"
description: "Resume los pasos de hello necesita tooset seguridad un tooAzure de almacén tooreplicate servidores físicos con Azure Site Recovery"
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
ms.openlocfilehash: 988928e3ece31116823f132cc39223fe44443468
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-a-vault-for-physical-server-replication-tooazure"></a><span data-ttu-id="6869f-103">Paso 6: Configurar un almacén para tooAzure de replicación del servidor físico</span><span class="sxs-lookup"><span data-stu-id="6869f-103">Step 6: Set up a vault for physical server replication tooAzure</span></span>


<span data-ttu-id="6869f-104">Este artículo se describe cómo tooset un almacén.</span><span class="sxs-lookup"><span data-stu-id="6869f-104">This article describes how tooset up a vault.</span></span> <span data-ttu-id="6869f-105">Crear almacén de Hola y especifique qué desea tooreplicate desde su tooAzure de ubicación local, mediante hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="6869f-105">You create hello vault, and specify what you want tooreplicate from your on-premises location tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="6869f-106">Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="6869f-106">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="6869f-107">Creación de un almacén de Recovery Services</span><span class="sxs-lookup"><span data-stu-id="6869f-107">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a><span data-ttu-id="6869f-108">Selección de un objetivo de protección</span><span class="sxs-lookup"><span data-stu-id="6869f-108">Select a protection goal</span></span>

<span data-ttu-id="6869f-109">Seleccione la acción que realizará tooreplicate, y donde quiera tooreplicate a.</span><span class="sxs-lookup"><span data-stu-id="6869f-109">Select what you want tooreplicate, and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="6869f-110">Haga clic en **Almacenes de Recovery Services** > almacén.</span><span class="sxs-lookup"><span data-stu-id="6869f-110">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="6869f-111">Hola recurso de menú, haga clic en **Site Recovery** > **preparar infraestructura** > **objetivo de protección**.</span><span class="sxs-lookup"><span data-stu-id="6869f-111">In hello Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="6869f-112">En **objetivo de protección**, seleccione **tooAzure** > **no virtualizados/otros**.</span><span class="sxs-lookup"><span data-stu-id="6869f-112">In **Protection goal**, select **tooAzure** > **Not virtualized/Other**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6869f-113">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6869f-113">Next steps</span></span>

<span data-ttu-id="6869f-114">Vaya demasiado[paso 7: configurar el origen y de destino](physical-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="6869f-114">Go too[Step 7: Set up source and target](physical-walkthrough-source-target.md)</span></span>
