---
title: "aaaSet una directiva de replicación para tooAzure de replicación de servidor físico con Azure Site Recovery | Documentos de Microsoft"
description: "Resume los pasos de hello necesita tooset una directiva de replicación al replicar locales almacenamiento de tooAzure de servidores físicos mediante el servicio de Azure Site Recovery Hola"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d7874bd8-6626-4668-9ec9-dbd2d26f8f81
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: d6bdeeffc24ffc8eaba24311f7c76452edb65648
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-a-replication-policy-for-physical-server-replication-tooazure"></a><span data-ttu-id="1c8e5-103">Paso 8: Configurar una directiva de replicación para tooAzure de replicación del servidor físico</span><span class="sxs-lookup"><span data-stu-id="1c8e5-103">Step 8: Set up a replication policy for physical server replication tooAzure</span></span>


<span data-ttu-id="1c8e5-104">Este artículo se describe cómo tooset una directiva de replicación al replicar tooAzure de servidores físicos de Windows/Linux con hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="1c8e5-104">This article describes how tooset up a replication policy when you're replicating Windows/Linux physical servers tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="1c8e5-105">Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="1c8e5-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="configure-a-policy"></a><span data-ttu-id="1c8e5-106">Configuración de una directiva</span><span class="sxs-lookup"><span data-stu-id="1c8e5-106">Configure a policy</span></span>

1. <span data-ttu-id="1c8e5-107">Haga clic en **Site Recovery Infrastructure (Infraestructura de Site Recovery)** > **Directivas de replicación** > **+Directiva de replicación**.</span><span class="sxs-lookup"><span data-stu-id="1c8e5-107">Click **Site Recovery infrastructure** > **Replication Policies** > **+Replication Policy**.</span></span>
2. <span data-ttu-id="1c8e5-108">En **Crear directiva de replicación**, especifique un nombre de directiva.</span><span class="sxs-lookup"><span data-stu-id="1c8e5-108">In **Create replication policy**, specify a policy name.</span></span>
3. <span data-ttu-id="1c8e5-109">En **umbral de RPO**, especifique el límite RPO de Hola.</span><span class="sxs-lookup"><span data-stu-id="1c8e5-109">In **RPO threshold**, specify hello RPO limit.</span></span> <span data-ttu-id="1c8e5-110">Este valor indica la frecuencia con que se crean puntos de recuperación de datos.</span><span class="sxs-lookup"><span data-stu-id="1c8e5-110">This value indicates how often data recovery points are created.</span></span> <span data-ttu-id="1c8e5-111">Se genera una alerta cuando la replicación continua supera este límite.</span><span class="sxs-lookup"><span data-stu-id="1c8e5-111">An alert is generated if continuous replication exceeds this limit.</span></span>
4. <span data-ttu-id="1c8e5-112">En **retención de punto de recuperación**, especifique cuánto tiempo (en horas) es el período de retención de Hola para cada punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="1c8e5-112">In **Recovery point retention**, specify (in hours) how long hello retention window is for each recovery point.</span></span> <span data-ttu-id="1c8e5-113">Máquinas virtuales replicadas se pueden recuperar tooany punto en una ventana.</span><span class="sxs-lookup"><span data-stu-id="1c8e5-113">Replicated VMs can be recovered tooany point in a window.</span></span> <span data-ttu-id="1c8e5-114">Seguridad too24 retención de horas es compatible con máquinas replicadas toopremium almacenamiento y 72 horas para el almacenamiento estándar.</span><span class="sxs-lookup"><span data-stu-id="1c8e5-114">Up too24 hours retention is supported for machines replicated toopremium storage, and 72 hours for standard storage.</span></span>
5. <span data-ttu-id="1c8e5-115">En **Frecuencia de instantánea coherente con la aplicación**especifique la frecuencia (en minutos) con la que se crearán puntos de recuperación que contengan las instantáneas coherentes con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1c8e5-115">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="1c8e5-116">Haga clic en **Aceptar** toocreate directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="1c8e5-116">Click **OK** toocreate hello policy.</span></span>

    ![Directiva de replicación](./media/physical-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="1c8e5-118">Cuando se crea una nueva directiva automáticamente está asociada con el servidor de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="1c8e5-118">When you create a new policy it's automatically associated with hello configuration server.</span></span> <span data-ttu-id="1c8e5-119">De forma predeterminada, se crea automáticamente una directiva correspondiente para la conmutación por recuperación.</span><span class="sxs-lookup"><span data-stu-id="1c8e5-119">By default, a matching policy is automatically created for failback.</span></span> <span data-ttu-id="1c8e5-120">Por ejemplo, si hello directiva de replicación es **rep-policy** será la directiva de conmutación por recuperación de hello **rep-directiva de conmutación por recuperación**.</span><span class="sxs-lookup"><span data-stu-id="1c8e5-120">For example, if hello replication policy is **rep-policy** then hello failback policy will be **rep-policy-failback**.</span></span> <span data-ttu-id="1c8e5-121">Esta directiva no se usa hasta que se inicie una conmutación por recuperación desde Azure.</span><span class="sxs-lookup"><span data-stu-id="1c8e5-121">This policy isn't used until you initiate a failback from Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c8e5-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1c8e5-122">Next steps</span></span>

<span data-ttu-id="1c8e5-123">Vaya demasiado[paso 9: instalar el servicio de movilidad de Hola](physical-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="1c8e5-123">Go too[Step 9: Install hello Mobility service](physical-walkthrough-install-mobility.md)</span></span>
