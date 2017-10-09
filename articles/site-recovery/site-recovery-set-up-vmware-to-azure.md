---
title: Configurar el entorno de origen hello (VMware tooAzure) | Documentos de Microsoft
description: "Este artículo describe cómo tooset seguridad su toostart del entorno local replicar VMware virtual máquinas tooAzure."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: cbeeffc1061b11223e12ff3e237fa7e55b999aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-vmware-tooazure"></a><span data-ttu-id="9af4c-103">Configurar el entorno de origen hello (tooAzure de VMware)</span><span class="sxs-lookup"><span data-stu-id="9af4c-103">Set up hello source environment (VMware tooAzure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9af4c-104">TooAzure de VMware</span><span class="sxs-lookup"><span data-stu-id="9af4c-104">VMware tooAzure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="9af4c-105">TooAzure físico</span><span class="sxs-lookup"><span data-stu-id="9af4c-105">Physical tooAzure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="9af4c-106">Este artículo describe cómo ejecutar los equipos de tooset seguridad su toostart del entorno local replicar virtual de VMware tooAzure.</span><span class="sxs-lookup"><span data-stu-id="9af4c-106">This article describes how tooset up your on-premises environment toostart replicating virtual machines running on VMware tooAzure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9af4c-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9af4c-107">Prerequisites</span></span>

<span data-ttu-id="9af4c-108">artículo de Hola se supone que ya ha creado:</span><span class="sxs-lookup"><span data-stu-id="9af4c-108">hello article assumes that you have already created:</span></span>
- <span data-ttu-id="9af4c-109">Un almacén de servicios de recuperación de hello [portal de Azure](http://portal.azure.com "portal de Azure").</span><span class="sxs-lookup"><span data-stu-id="9af4c-109">A Recovery Services Vault in hello [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="9af4c-110">Una cuenta dedicada en el vCenter de VMware que se puede usar para [detección automática](./site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="9af4c-110">A dedicated account in your VMware vCenter that can be used for [automatic discovery](./site-recovery-vmware-to-azure.md).</span></span>
- <span data-ttu-id="9af4c-111">Una máquina virtual en el servidor de configuración de tooinstall Hola.</span><span class="sxs-lookup"><span data-stu-id="9af4c-111">A virtual machine on which tooinstall hello configuration server.</span></span>

## <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="9af4c-112">Requisitos mínimos del servidor de configuración</span><span class="sxs-lookup"><span data-stu-id="9af4c-112">Configuration server minimum requirements</span></span>
<span data-ttu-id="9af4c-113">software de servidor de configuración de Hello debe implementarse en una máquina virtual de VMware alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="9af4c-113">hello configuration server software should be deployed on a highly available VMware virtual machine.</span></span> <span data-ttu-id="9af4c-114">Hello en la tabla siguiente enumera Hola mínimos de hardware, software y requisitos de red para un servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="9af4c-114">hello following table lists hello minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="9af4c-115">No se admiten servidores proxy basada en HTTPS al servidor de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="9af4c-115">HTTPS-based proxy servers are not supported by hello configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="9af4c-116">Selección de los objetivos de protección</span><span class="sxs-lookup"><span data-stu-id="9af4c-116">Choose your protection goals</span></span>

1. <span data-ttu-id="9af4c-117">Hola portal de Azure, vaya toohello **servicios de recuperación** hoja del almacén y seleccione el almacén.</span><span class="sxs-lookup"><span data-stu-id="9af4c-117">In hello Azure portal, go toohello **Recovery Services** vault blade and select your vault.</span></span>
2. <span data-ttu-id="9af4c-118">En el menú de recursos de Hola de almacén de hello, que se vaya demasiado**Introducción** > **Site Recovery** > **paso 1: preparar la infraestructura**  >  **Objetivo de protección**.</span><span class="sxs-lookup"><span data-stu-id="9af4c-118">On hello resource menu of hello vault, go too**Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![Elegir objetivos](./media/site-recovery-set-up-vmware-to-azure/choose-goals.png)
3. <span data-ttu-id="9af4c-120">En **objetivo de protección**, seleccione **tooAzure**y elija **Sí, con el hipervisor de VMware vSphere**.</span><span class="sxs-lookup"><span data-stu-id="9af4c-120">In **Protection goal**, select **tooAzure**, and choose **Yes, with VMware vSphere Hypervisor**.</span></span> <span data-ttu-id="9af4c-121">y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9af4c-121">Then click **OK**.</span></span>

    ![Elegir objetivos](./media/site-recovery-set-up-vmware-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a><span data-ttu-id="9af4c-123">Configurar el entorno de origen Hola</span><span class="sxs-lookup"><span data-stu-id="9af4c-123">Set up hello source environment</span></span>
<span data-ttu-id="9af4c-124">Configurar el entorno de origen Hola implica dos actividades principales:</span><span class="sxs-lookup"><span data-stu-id="9af4c-124">Setting up hello source environment involves two main activities:</span></span>

- <span data-ttu-id="9af4c-125">Instale y registre un servidor de configuración con Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="9af4c-125">Install and register a configuration server with Site Recovery.</span></span>
- <span data-ttu-id="9af4c-126">Descubra las máquinas virtuales de local mediante la conexión de Site Recovery tooyour local vCenter o vSphere EXSi hosts de VMware.</span><span class="sxs-lookup"><span data-stu-id="9af4c-126">Discover your on-premises virtual machines by connecting Site Recovery tooyour on-premises VMware vCenter or vSphere EXSi hosts.</span></span>

### <a name="step-1-install-and-register-a-configuration-server"></a><span data-ttu-id="9af4c-127">Paso 1: Instalar y registrar un servidor de configuración</span><span class="sxs-lookup"><span data-stu-id="9af4c-127">Step 1: Install and register a configuration server</span></span>

1. <span data-ttu-id="9af4c-128">Haga clic en **Paso 1: Preparar la infraestructura** > **Origen**.</span><span class="sxs-lookup"><span data-stu-id="9af4c-128">Click **Step 1: Prepare Infrastructure** > **Source**.</span></span> <span data-ttu-id="9af4c-129">En **preparar origen**, si no tiene un servidor de configuración, haga clic en **+ servidor de configuración** tooadd uno.</span><span class="sxs-lookup"><span data-stu-id="9af4c-129">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** tooadd one.</span></span>

    ![Configurar origen](./media/site-recovery-set-up-vmware-to-azure/set-source1.png)
2. <span data-ttu-id="9af4c-131">En hello **Agregar servidor** hoja, compruebe que **servidor de configuración** aparece en **tipo de servidor**.</span><span class="sxs-lookup"><span data-stu-id="9af4c-131">On hello **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="9af4c-132">Descargue el archivo de instalación de configuración de Site Recovery unificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="9af4c-132">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="9af4c-133">Descargue la clave de registro del almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="9af4c-133">Download hello vault registration key.</span></span> <span data-ttu-id="9af4c-134">Se necesita la clave de registro de hello al ejecutar el programa de instalación unificada.</span><span class="sxs-lookup"><span data-stu-id="9af4c-134">You need hello registration key when you run Unified Setup.</span></span> <span data-ttu-id="9af4c-135">clave de Hello es válida durante cinco días después de generarlo.</span><span class="sxs-lookup"><span data-stu-id="9af4c-135">hello key is valid for five days after you generate it.</span></span>

    ![Configurar origen](./media/site-recovery-set-up-vmware-to-azure/set-source2.png)
6. <span data-ttu-id="9af4c-137">En el equipo de Hola que utilice como servidor de configuración de hello, ejecute **instalación unificada de Azure Site Recovery** servidor de configuración de tooinstall Hola, servidor de procesos de Hola y Hola maestro servidor de destino.</span><span class="sxs-lookup"><span data-stu-id="9af4c-137">On hello machine you’re using as hello configuration server, run **Azure Site Recovery Unified Setup** tooinstall hello configuration server, hello process server, and hello master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="9af4c-138">Ejecución de la instalación unificada de Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="9af4c-138">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="9af4c-139">Se produce un error en el registro del servidor de configuración si la hora de hello en el reloj del sistema del equipo difiere de la hora local en más de cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="9af4c-139">Configuration server registration fails if hello time on your computer's system clock differs from local time by more than five minutes.</span></span> <span data-ttu-id="9af4c-140">Sincronizar el reloj del sistema con un [servidor horario](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) antes de iniciar la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="9af4c-140">Synchronize your system clock with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting hello installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="9af4c-141">servidor de configuración de Hello puede instalarse a través de la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="9af4c-141">hello configuration server can be installed via command line.</span></span> <span data-ttu-id="9af4c-142">Para obtener más información, consulte [instalar servidor de configuración de hello mediante herramientas de línea de comandos](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="9af4c-142">For more information, see [Installing hello configuration server using Command-line tools](http://aka.ms/installconfigsrv).</span></span>

#### <a name="add-hello-vmware-account-for-automatic-discovery"></a><span data-ttu-id="9af4c-143">Agregar cuenta de VMware de hello para la detección automática</span><span class="sxs-lookup"><span data-stu-id="9af4c-143">Add hello VMware account for automatic discovery</span></span>

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="step-2-add-a-vcenter"></a><span data-ttu-id="9af4c-144">Paso 2: Agregar un vCenter</span><span class="sxs-lookup"><span data-stu-id="9af4c-144">Step 2: Add a vCenter</span></span>
<span data-ttu-id="9af4c-145">tooallow Azure Site Recovery toodiscover máquinas virtuales que ejecutan en su entorno local, debe tooconnect el servidor VMware vCenter o hosts de ESXi vSphere con Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="9af4c-145">tooallow Azure Site Recovery toodiscover virtual machines running in your on-premises environment, you need tooconnect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span></span>

<span data-ttu-id="9af4c-146">Seleccione **+ vCenter** toostart conectar un servidor VMware vCenter o un host de VMware vSphere ESXi.</span><span class="sxs-lookup"><span data-stu-id="9af4c-146">Select **+vCenter** toostart connecting a VMware vCenter server or a VMware vSphere ESXi host.</span></span>

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]


## <a name="common-issues"></a><span data-ttu-id="9af4c-147">Problemas comunes</span><span class="sxs-lookup"><span data-stu-id="9af4c-147">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="9af4c-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9af4c-148">Next steps</span></span>
<span data-ttu-id="9af4c-149">[Configure el entorno de destino](./site-recovery-prepare-target-vmware-to-azure.md) en Azure.</span><span class="sxs-lookup"><span data-stu-id="9af4c-149">[Set up your target environment](./site-recovery-prepare-target-vmware-to-azure.md) in Azure.</span></span>
