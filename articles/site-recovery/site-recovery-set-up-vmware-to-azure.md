---
title: "Configuración del entorno de origen (VMware a Azure) | Microsoft Docs"
description: "En este artículo se describe cómo configurar el entorno local para comenzar a replicar máquinas virtuales de VMware en Azure."
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
ms.openlocfilehash: a2fabc56463c8cbf0b8a76b7a84369ed8e535486
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="set-up-the-source-environment-vmware-to-azure"></a><span data-ttu-id="361dd-103">Configuración del entorno de origen (VMware a Azure)</span><span class="sxs-lookup"><span data-stu-id="361dd-103">Set up the source environment (VMware to Azure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="361dd-104">VMware a Azure</span><span class="sxs-lookup"><span data-stu-id="361dd-104">VMware to Azure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="361dd-105">Físico en Azure</span><span class="sxs-lookup"><span data-stu-id="361dd-105">Physical to Azure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="361dd-106">En este artículo se describe cómo configurar el entorno local para comenzar a replicar máquinas virtuales que se ejecutan en VMware en Azure.</span><span class="sxs-lookup"><span data-stu-id="361dd-106">This article describes how to set up your on-premises environment to start replicating virtual machines running on VMware to Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="361dd-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="361dd-107">Prerequisites</span></span>

<span data-ttu-id="361dd-108">En este artículo se supone que ya creó:</span><span class="sxs-lookup"><span data-stu-id="361dd-108">The article assumes that you have already created:</span></span>
- <span data-ttu-id="361dd-109">Un almacén de Recovery Services en [Azure Portal](http://portal.azure.com "Azure Portal").</span><span class="sxs-lookup"><span data-stu-id="361dd-109">A Recovery Services Vault in the [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="361dd-110">Una cuenta dedicada en el vCenter de VMware que se puede usar para [detección automática](./site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="361dd-110">A dedicated account in your VMware vCenter that can be used for [automatic discovery](./site-recovery-vmware-to-azure.md).</span></span>
- <span data-ttu-id="361dd-111">Una máquina virtual en donde instalar el servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="361dd-111">A virtual machine on which to install the configuration server.</span></span>

## <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="361dd-112">Requisitos mínimos del servidor de configuración</span><span class="sxs-lookup"><span data-stu-id="361dd-112">Configuration server minimum requirements</span></span>
<span data-ttu-id="361dd-113">El software del servidor de configuración se debe implementar en una máquina virtual de VMware de alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="361dd-113">The configuration server software should be deployed on a highly available VMware virtual machine.</span></span> <span data-ttu-id="361dd-114">En la siguiente tabla se muestran los requisitos mínimos de hardware, software y red para un servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="361dd-114">The following table lists the minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="361dd-115">El servidor de configuración no admite los servidores proxy basados en HTTPS.</span><span class="sxs-lookup"><span data-stu-id="361dd-115">HTTPS-based proxy servers are not supported by the configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="361dd-116">Selección de los objetivos de protección</span><span class="sxs-lookup"><span data-stu-id="361dd-116">Choose your protection goals</span></span>

1. <span data-ttu-id="361dd-117">En Azure Portal, vaya a la hoja de los almacenes de **Recovery Services** y seleccione su almacén.</span><span class="sxs-lookup"><span data-stu-id="361dd-117">In the Azure portal, go to the **Recovery Services** vault blade and select your vault.</span></span>
2. <span data-ttu-id="361dd-118">En el menú de recursos del almacén, haga clic en **Introducción** > **Site Recovery** > **Paso 1: Preparar la infraestructura** > **Objetivo de protección**.</span><span class="sxs-lookup"><span data-stu-id="361dd-118">On the resource menu of the vault, go to **Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![Elegir objetivos](./media/site-recovery-set-up-vmware-to-azure/choose-goals.png)
3. <span data-ttu-id="361dd-120">En **Objetivo de protección**, seleccione **To Azure** (En Azure) y **Yes, with VMware vSphere Hypervisor** (Sí, con VMware vSphere Hypervisor).</span><span class="sxs-lookup"><span data-stu-id="361dd-120">In **Protection goal**, select **To Azure**, and choose **Yes, with VMware vSphere Hypervisor**.</span></span> <span data-ttu-id="361dd-121">y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="361dd-121">Then click **OK**.</span></span>

    ![Elegir objetivos](./media/site-recovery-set-up-vmware-to-azure/choose-goals2.png)

## <a name="set-up-the-source-environment"></a><span data-ttu-id="361dd-123">Configuración del entorno de origen</span><span class="sxs-lookup"><span data-stu-id="361dd-123">Set up the source environment</span></span>
<span data-ttu-id="361dd-124">Configurar el entorno de origen implica dos actividades principales:</span><span class="sxs-lookup"><span data-stu-id="361dd-124">Setting up the source environment involves two main activities:</span></span>

- <span data-ttu-id="361dd-125">Instale y registre un servidor de configuración con Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="361dd-125">Install and register a configuration server with Site Recovery.</span></span>
- <span data-ttu-id="361dd-126">Detecte sus máquinas virtuales locales a través de la conexión de Site Recovery con los hosts EXSi de vSphere o vCenter de VMware locales.</span><span class="sxs-lookup"><span data-stu-id="361dd-126">Discover your on-premises virtual machines by connecting Site Recovery to your on-premises VMware vCenter or vSphere EXSi hosts.</span></span>

### <a name="step-1-install-and-register-a-configuration-server"></a><span data-ttu-id="361dd-127">Paso 1: Instalar y registrar un servidor de configuración</span><span class="sxs-lookup"><span data-stu-id="361dd-127">Step 1: Install and register a configuration server</span></span>

1. <span data-ttu-id="361dd-128">Haga clic en **Paso 1: Preparar la infraestructura** > **Origen**.</span><span class="sxs-lookup"><span data-stu-id="361dd-128">Click **Step 1: Prepare Infrastructure** > **Source**.</span></span> <span data-ttu-id="361dd-129">En **Preparar origen**, si no tiene un servidor de configuración, haga clic en **+Servidor de configuración** para agregar uno.</span><span class="sxs-lookup"><span data-stu-id="361dd-129">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** to add one.</span></span>

    ![Configurar origen](./media/site-recovery-set-up-vmware-to-azure/set-source1.png)
2. <span data-ttu-id="361dd-131">En la hoja **Agregar servidor**, compruebe que **Servidor de configuración** aparezca en **Tipo de servidor**.</span><span class="sxs-lookup"><span data-stu-id="361dd-131">On the **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="361dd-132">Descargue el archivo de instalación unificada de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="361dd-132">Download the Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="361dd-133">Descargue la clave de registro del almacén.</span><span class="sxs-lookup"><span data-stu-id="361dd-133">Download the vault registration key.</span></span> <span data-ttu-id="361dd-134">Necesita la clave de registro cuando ejecuta la instalación unificada.</span><span class="sxs-lookup"><span data-stu-id="361dd-134">You need the registration key when you run Unified Setup.</span></span> <span data-ttu-id="361dd-135">La clave será válida durante cinco días a partir del momento en que se genera.</span><span class="sxs-lookup"><span data-stu-id="361dd-135">The key is valid for five days after you generate it.</span></span>

    ![Configurar origen](./media/site-recovery-set-up-vmware-to-azure/set-source2.png)
6. <span data-ttu-id="361dd-137">En la máquina que usa como el servidor de configuración, ejecute la **instalación unificada de Azure Site Recovery** para instalar el servidor de configuración, el servidor de procesos y el servidor de destino maestro.</span><span class="sxs-lookup"><span data-stu-id="361dd-137">On the machine you’re using as the configuration server, run **Azure Site Recovery Unified Setup** to install the configuration server, the process server, and the master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="361dd-138">Ejecución de la instalación unificada de Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="361dd-138">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="361dd-139">El registro del servidor de configuración presenta errores si la hora del reloj del sistema de su equipo difiere más de cinco minutos con respecto a la hora local.</span><span class="sxs-lookup"><span data-stu-id="361dd-139">Configuration server registration fails if the time on your computer's system clock differs from local time by more than five minutes.</span></span> <span data-ttu-id="361dd-140">Sincronice el reloj del sistema con un [servidor horario](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) antes de comenzar la instalación.</span><span class="sxs-lookup"><span data-stu-id="361dd-140">Synchronize your system clock with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting the installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="361dd-141">El servidor de configuración se puede instalar a través de la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="361dd-141">The configuration server can be installed via command line.</span></span> <span data-ttu-id="361dd-142">Para más información, consulte [Instalación del servidor de configuración con herramientas de línea de comandos](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="361dd-142">For more information, see [Installing the configuration server using Command-line tools](http://aka.ms/installconfigsrv).</span></span>

#### <a name="add-the-vmware-account-for-automatic-discovery"></a><span data-ttu-id="361dd-143">Incorporación de la cuenta de VMware para detección automática</span><span class="sxs-lookup"><span data-stu-id="361dd-143">Add the VMware account for automatic discovery</span></span>

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="step-2-add-a-vcenter"></a><span data-ttu-id="361dd-144">Paso 2: Agregar un vCenter</span><span class="sxs-lookup"><span data-stu-id="361dd-144">Step 2: Add a vCenter</span></span>
<span data-ttu-id="361dd-145">Para permitir que Azure Site Recovery detecte las máquinas virtuales que se ejecutan en el entorno local, debe conectar los hosts ESXi de vSphere o servidor vCenter de VMware con Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="361dd-145">To allow Azure Site Recovery to discover virtual machines running in your on-premises environment, you need to connect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span></span>

<span data-ttu-id="361dd-146">Seleccione **+vCenter** para comenzar a conectar un servidor vCenter de VMware o un host ESXi de vSphere de VMware.</span><span class="sxs-lookup"><span data-stu-id="361dd-146">Select **+vCenter** to start connecting a VMware vCenter server or a VMware vSphere ESXi host.</span></span>

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]


## <a name="common-issues"></a><span data-ttu-id="361dd-147">Problemas comunes</span><span class="sxs-lookup"><span data-stu-id="361dd-147">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="361dd-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="361dd-148">Next steps</span></span>
<span data-ttu-id="361dd-149">[Configure el entorno de destino](./site-recovery-prepare-target-vmware-to-azure.md) en Azure.</span><span class="sxs-lookup"><span data-stu-id="361dd-149">[Set up your target environment](./site-recovery-prepare-target-vmware-to-azure.md) in Azure.</span></span>
