---
title: "aaaSet seguridad Hola origen y de destino para tooAzure de replicación de servidor físico con Azure Site Recovery | Documentos de Microsoft"
description: "Resume Hola pasos tooset la configuración de origen y de destino para la replicación de almacenamiento de tooAzure de servidores físicos con hello servicio Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 2e3d03bc-4e53-4590-8a01-f702d3cc9500
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: e75ef23174d77509bf54380eba8f251a7337a45f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-hello-source-and-target-for-physical-server-replication-tooazure"></a><span data-ttu-id="dd85a-103">Paso 7: Configurar origen de Hola y de destino para tooAzure de replicación del servidor físico</span><span class="sxs-lookup"><span data-stu-id="dd85a-103">Step 7: Set up hello source and target for physical server replication tooAzure</span></span>

<span data-ttu-id="dd85a-104">Este artículo describe cómo tooconfigure de configuración de origen y de destino cuando se replican de manera local tooAzure de servidores físicos, mediante hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="dd85a-104">This article describes how tooconfigure source and target settings when replicating on-premises physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="dd85a-105">Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="dd85a-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="dd85a-106">Configurar el entorno de origen Hola</span><span class="sxs-lookup"><span data-stu-id="dd85a-106">Set up hello source environment</span></span>

<span data-ttu-id="dd85a-107">Configurar el servidor de configuración de hello, registrar en el almacén de Hola y detectar máquinas.</span><span class="sxs-lookup"><span data-stu-id="dd85a-107">Set up hello configuration server, register it in hello vault, and discover machines.</span></span>

1. <span data-ttu-id="dd85a-108">Haga clic en **Site Recovery** > **Paso 1: Preparar la infraestructura** > **Origen**.</span><span class="sxs-lookup"><span data-stu-id="dd85a-108">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="dd85a-109">Si no tiene un servidor de configuración, haga clic en **+Servidor de configuración**.</span><span class="sxs-lookup"><span data-stu-id="dd85a-109">If you don’t have a configuration server, click **+Configuration server**.</span></span>
3. <span data-ttu-id="dd85a-110">En **Agregar servidor**, compruebe que aparezca **Servidor de configuración** en **Tipo de servidor**.</span><span class="sxs-lookup"><span data-stu-id="dd85a-110">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="dd85a-111">Descargue el archivo de instalación de configuración de Site Recovery unificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd85a-111">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="dd85a-112">Descargue la clave de registro del almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd85a-112">Download hello vault registration key.</span></span> <span data-ttu-id="dd85a-113">Se le solicitará cuando ejecute la instalación unificada.</span><span class="sxs-lookup"><span data-stu-id="dd85a-113">You need this when you run Unified Setup.</span></span> <span data-ttu-id="dd85a-114">clave de Hello es válida durante cinco días después de generarlo.</span><span class="sxs-lookup"><span data-stu-id="dd85a-114">hello key is valid for five days after you generate it.</span></span>

   ![Configurar origen](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a><span data-ttu-id="dd85a-116">Registrar el servidor de configuración de hello en el almacén de Hola</span><span class="sxs-lookup"><span data-stu-id="dd85a-116">Register hello configuration server in hello vault</span></span>

<span data-ttu-id="dd85a-117">Realice la siguiente Hola antes de iniciar después ejecutar el programa de instalación unificada tooinstall servidor de configuración de hello, servidor de procesos de Hola y servidor de destino maestro Hola.</span><span class="sxs-lookup"><span data-stu-id="dd85a-117">Do hello following before you start, then run Unified Setup tooinstall hello configuration server, hello process server, and hello master target server.</span></span> <span data-ttu-id="dd85a-118">Hola vídeo describe cómo configurar los componentes de hello para la replicación de VM de VMware tooAzure.</span><span class="sxs-lookup"><span data-stu-id="dd85a-118">hello video describes setting up hello components for VMware VM tooAzure replication.</span></span> <span data-ttu-id="dd85a-119">Sin embargo, hello mismo proceso es válido para la replicación de tooAzure de servidor físico.</span><span class="sxs-lookup"><span data-stu-id="dd85a-119">However, hello same process is valid for physical server tooAzure replication.</span></span>

- <span data-ttu-id="dd85a-120">En la máquina virtual del servidor de configuración de hello, asegúrese de que el reloj del sistema de Hola se sincroniza con un [servidor horario](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span><span class="sxs-lookup"><span data-stu-id="dd85a-120">On hello configuration server VM, make sure that hello system clock is synchronized with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="dd85a-121">Deben ser iguales.</span><span class="sxs-lookup"><span data-stu-id="dd85a-121">It should match.</span></span> <span data-ttu-id="dd85a-122">Si hay una diferencia de 15 minutos, antes o después, se podría producir un error en la instalación.</span><span class="sxs-lookup"><span data-stu-id="dd85a-122">If it's 15 minutes in front or behind, setup might fail.</span></span>
- <span data-ttu-id="dd85a-123">Ejecute el programa de instalación como administrador Local en el equipo del servidor de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd85a-123">Run setup as a Local Administrator on hello configuration server machine.</span></span>
- <span data-ttu-id="dd85a-124">Asegúrese de que TLS 1.0 está habilitado en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="dd85a-124">Make sure TLS 1.0 is enabled on hello VM.</span></span>


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="dd85a-125">También se puede instalar el servidor de configuración de Hello [desde la línea de comandos de hello](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="dd85a-125">hello configuration server can also be installed [from hello command line](http://aka.ms/installconfigsrv).</span></span>




## <a name="set-up-hello-target-environment"></a><span data-ttu-id="dd85a-126">Configurar el entorno de destino de Hola</span><span class="sxs-lookup"><span data-stu-id="dd85a-126">Set up hello target environment</span></span>

<span data-ttu-id="dd85a-127">Antes de configurar el entorno de destino de hello, asegúrese de que tiene una cuenta de almacenamiento de Azure y la configuración de red virtual.</span><span class="sxs-lookup"><span data-stu-id="dd85a-127">Before you set up hello target environment, make sure you have an Azure storage account and virtual network set up.</span></span>

1. <span data-ttu-id="dd85a-128">Haga clic en **preparar infraestructura** > **destino**, y seleccione Hola desea toouse de suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="dd85a-128">Click **Prepare infrastructure** > **Target**, and select hello Azure subscription you want toouse.</span></span>
2. <span data-ttu-id="dd85a-129">Especifique si el modelo de implementación de destino está basado en Resource Manager o si es el clásico.</span><span class="sxs-lookup"><span data-stu-id="dd85a-129">Specify whether your target deployment model is Resource Manager-based, or classic.</span></span>
3. <span data-ttu-id="dd85a-130">Site Recovery comprueba que tiene una o más cuentas de almacenamiento y redes compatibles.</span><span class="sxs-lookup"><span data-stu-id="dd85a-130">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![Destino](./media/physical-walkthrough-source-target/gs-target.png)

4. <span data-ttu-id="dd85a-132">Si no ha creado una cuenta de almacenamiento o red, haga clic en **+ cuenta de almacenamiento** o **+ red**, toocreate un administrador de recursos cuenta o red en línea.</span><span class="sxs-lookup"><span data-stu-id="dd85a-132">If you haven't created a storage account or network, click **+Storage account** or **+Network**, toocreate a Resource Manager account or network inline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd85a-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dd85a-133">Next steps</span></span>

<span data-ttu-id="dd85a-134">Vaya demasiado[paso 8: configurar una directiva de replicación](physical-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="dd85a-134">Go too[Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>
