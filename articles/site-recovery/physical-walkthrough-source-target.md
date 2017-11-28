---
title: "Configuración del origen y el destino para la replicación del servidor físico en Azure con Azure Site Recovery | Microsoft Docs"
description: "Se resumen los pasos para configurar los valores de origen y de destino para la replicación de servidores físicos en Azure Storage con el servicio Azure Site Recovery"
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
ms.openlocfilehash: e89bbf5a2c1d71852e49da43d3106a05ebfc28a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="step-7-set-up-the-source-and-target-for-physical-server-replication-to-azure"></a><span data-ttu-id="64fc6-103">Paso 7: Configuración del origen y el destino para la replicación del servidor físico en Azure</span><span class="sxs-lookup"><span data-stu-id="64fc6-103">Step 7: Set up the source and target for physical server replication to Azure</span></span>

<span data-ttu-id="64fc6-104">En este artículo se describe cómo configurar las opciones de origen y de destino al replicar servidores físicos locales en Azure mediante el servicio [Azure Site Recovery](site-recovery-overview.md) en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="64fc6-104">This article describes how to configure source and target settings when replicating on-premises physical servers to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="64fc6-105">Publique cualquier comentario o pregunta en la parte inferior de este artículo, o bien en el [foro de Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="64fc6-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-the-source-environment"></a><span data-ttu-id="64fc6-106">Configuración del entorno de origen</span><span class="sxs-lookup"><span data-stu-id="64fc6-106">Set up the source environment</span></span>

<span data-ttu-id="64fc6-107">Configure el servidor de configuración, regístrelo en el almacén y detecte las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="64fc6-107">Set up the configuration server, register it in the vault, and discover machines.</span></span>

1. <span data-ttu-id="64fc6-108">Haga clic en **Site Recovery** > **Paso 1: Preparar la infraestructura** > **Origen**.</span><span class="sxs-lookup"><span data-stu-id="64fc6-108">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="64fc6-109">Si no tiene un servidor de configuración, haga clic en **+Servidor de configuración**.</span><span class="sxs-lookup"><span data-stu-id="64fc6-109">If you don’t have a configuration server, click **+Configuration server**.</span></span>
3. <span data-ttu-id="64fc6-110">En **Agregar servidor**, compruebe que aparezca **Servidor de configuración** en **Tipo de servidor**.</span><span class="sxs-lookup"><span data-stu-id="64fc6-110">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="64fc6-111">Descargue el archivo de instalación unificada de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="64fc6-111">Download the Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="64fc6-112">Descargue la clave de registro del almacén.</span><span class="sxs-lookup"><span data-stu-id="64fc6-112">Download the vault registration key.</span></span> <span data-ttu-id="64fc6-113">Se le solicitará cuando ejecute la instalación unificada.</span><span class="sxs-lookup"><span data-stu-id="64fc6-113">You need this when you run Unified Setup.</span></span> <span data-ttu-id="64fc6-114">La clave será válida durante cinco días a partir del momento en que se genera.</span><span class="sxs-lookup"><span data-stu-id="64fc6-114">The key is valid for five days after you generate it.</span></span>

   ![Configurar origen](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-the-configuration-server-in-the-vault"></a><span data-ttu-id="64fc6-116">Registro del servidor de configuración en el almacén</span><span class="sxs-lookup"><span data-stu-id="64fc6-116">Register the configuration server in the vault</span></span>

<span data-ttu-id="64fc6-117">Haga lo siguiente antes de empezar y, después, ejecute la instalación unificada para instalar el servidor de configuración, el servidor de procesos y el servidor de destino maestro.</span><span class="sxs-lookup"><span data-stu-id="64fc6-117">Do the following before you start, then run Unified Setup to install the configuration server, the process server, and the master target server.</span></span> <span data-ttu-id="64fc6-118">En el vídeo se describe cómo configurar los componentes de la máquina virtual de VMware para la replicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="64fc6-118">The video describes setting up the components for VMware VM to Azure replication.</span></span> <span data-ttu-id="64fc6-119">Pero este proceso también es válido para la replicación de Azure de un servidor físico.</span><span class="sxs-lookup"><span data-stu-id="64fc6-119">However, the same process is valid for physical server to Azure replication.</span></span>

- <span data-ttu-id="64fc6-120">En la máquina virtual del servidor de configuración, asegúrese de que el reloj del sistema está sincronizado con un [servidor horario](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span><span class="sxs-lookup"><span data-stu-id="64fc6-120">On the configuration server VM, make sure that the system clock is synchronized with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="64fc6-121">Deben ser iguales.</span><span class="sxs-lookup"><span data-stu-id="64fc6-121">It should match.</span></span> <span data-ttu-id="64fc6-122">Si hay una diferencia de 15 minutos, antes o después, se podría producir un error en la instalación.</span><span class="sxs-lookup"><span data-stu-id="64fc6-122">If it's 15 minutes in front or behind, setup might fail.</span></span>
- <span data-ttu-id="64fc6-123">Ejecute la instalación como Administrador local en la máquina del servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="64fc6-123">Run setup as a Local Administrator on the configuration server machine.</span></span>
- <span data-ttu-id="64fc6-124">Asegúrese de que TLS 1.0 está habilitada en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="64fc6-124">Make sure TLS 1.0 is enabled on the VM.</span></span>


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="64fc6-125">El servidor de configuración también se puede instalar [desde la línea de comandos](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="64fc6-125">The configuration server can also be installed [from the command line](http://aka.ms/installconfigsrv).</span></span>




## <a name="set-up-the-target-environment"></a><span data-ttu-id="64fc6-126">Configuración del entorno de destino</span><span class="sxs-lookup"><span data-stu-id="64fc6-126">Set up the target environment</span></span>

<span data-ttu-id="64fc6-127">Antes de configurar el entorno de destino, asegúrese de tener una cuenta de Azure Storage y una red virtual configurada.</span><span class="sxs-lookup"><span data-stu-id="64fc6-127">Before you set up the target environment, make sure you have an Azure storage account and virtual network set up.</span></span>

1. <span data-ttu-id="64fc6-128">Haga clic en **Preparar infraestructura** > **Destino** y seleccione la suscripción de Azure que quiere usar.</span><span class="sxs-lookup"><span data-stu-id="64fc6-128">Click **Prepare infrastructure** > **Target**, and select the Azure subscription you want to use.</span></span>
2. <span data-ttu-id="64fc6-129">Especifique si el modelo de implementación de destino está basado en Resource Manager o si es el clásico.</span><span class="sxs-lookup"><span data-stu-id="64fc6-129">Specify whether your target deployment model is Resource Manager-based, or classic.</span></span>
3. <span data-ttu-id="64fc6-130">Site Recovery comprueba que tiene una o más cuentas de almacenamiento y redes compatibles.</span><span class="sxs-lookup"><span data-stu-id="64fc6-130">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![Destino](./media/physical-walkthrough-source-target/gs-target.png)

4. <span data-ttu-id="64fc6-132">Si no ha creado una cuenta de almacenamiento ni una red, haga clic en **+Cuenta de almacenamiento** o **+Red** para crear una cuenta o red de Resource Manager en línea.</span><span class="sxs-lookup"><span data-stu-id="64fc6-132">If you haven't created a storage account or network, click **+Storage account** or **+Network**, to create a Resource Manager account or network inline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64fc6-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="64fc6-133">Next steps</span></span>

<span data-ttu-id="64fc6-134">Vaya al [Paso 8: Configuración de una directiva de replicación](physical-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="64fc6-134">Go to [Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>
