---
title: " Administración de un servidor de procesos que se ejecuta en Azure (Resource Manager) | Microsoft Docs"
description: "Este artículo describe cómo tooset la una conmutación por recuperación proceso server (Administrador de recursos) en Azure."
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
ms.openlocfilehash: 70426b96095cc42befff6c4114fb56536284a667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-resource-manager"></a><span data-ttu-id="fa933-103">Administración de un servidor de procesos que se ejecuta en Azure (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="fa933-103">Manage a process server running in Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fa933-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fa933-104">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)
> * [<span data-ttu-id="fa933-105">Clásico</span><span class="sxs-lookup"><span data-stu-id="fa933-105">Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)

<span data-ttu-id="fa933-106">Durante la conmutación por recuperación, se recomienda toodeploy el servidor de procesos en Azure si no hay una latencia elevada entre Hola red Virtual de Azure y la red local.</span><span class="sxs-lookup"><span data-stu-id="fa933-106">During failback, it is recommended toodeploy process server in Azure if there is high latency between hello Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="fa933-107">Este artículo describe cómo instalar, configurar y administrar servidores de procesos de hello ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="fa933-107">This article describes how you can set up, configure, and manage hello process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="fa933-108">Este artículo es toobe si utiliza **el Administrador de recursos** como modelo de implementación de Hola para las máquinas virtuales de Hola durante la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="fa933-108">This article is toobe used if you used **Resource Manager** as hello deployment model for hello virtual machines during failover.</span></span> <span data-ttu-id="fa933-109">Si ha usado **clásico** como modelo de implementación de hello, siga los pasos de hello en [cómo tooset una copia de seguridad y configurar un servidor de procesos de conmutación por recuperación (clásico)](./site-recovery-vmware-setup-azure-ps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="fa933-109">If you used **Classic** as hello deployment model, follow hello steps in [How tooset up & configure a Failback process server (Classic)](./site-recovery-vmware-setup-azure-ps-classic.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa933-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fa933-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prerequ](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="fa933-111">Implementación de un servidor de procesos en Azure</span><span class="sxs-lookup"><span data-stu-id="fa933-111">Deploy a process server on Azure</span></span>
1. <span data-ttu-id="fa933-112">Hola almacén > **infraestructura del sitio de recuperación** (bajo el encabezado de "Manage" hello) > **servidores de configuración** (bajo el encabezado "Para VMware y máquinas físicas"), seleccione el servidor de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="fa933-112">In hello Vault > **Site Recovery Infrastructure** (under hello "Manage" heading) > **Configuration Servers** (under "For VMware and Physical Machines" heading), select hello configuration server.</span></span>
2. <span data-ttu-id="fa933-113">En la página de detalles del servidor de configuración Hola que se abre, haga clic en "+ servidor de procesos"</span><span class="sxs-lookup"><span data-stu-id="fa933-113">In hello Configuration Server details page that opens click "+ Process server"</span></span>

  ![Adición de una galería del servidor de procesos](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps.png)

3.  <span data-ttu-id="fa933-115">En hello **Agregar servidor de proceso** seleccione Hola después de los valores de la página</span><span class="sxs-lookup"><span data-stu-id="fa933-115">On hello **Add process server** page, select hello following values</span></span>

  ![Adición de un elemento de la galería del servidor de procesos](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-1.png)
|<span data-ttu-id="fa933-117">**Nombre del campo**</span><span class="sxs-lookup"><span data-stu-id="fa933-117">**Field Name**</span></span>|<span data-ttu-id="fa933-118">**Valor**</span><span class="sxs-lookup"><span data-stu-id="fa933-118">**Value**</span></span>|
|-|-|
|<span data-ttu-id="fa933-119">Elegir dónde quiere toodeploy el servidor de procesos</span><span class="sxs-lookup"><span data-stu-id="fa933-119">Choose where you want toodeploy your process server</span></span>|<span data-ttu-id="fa933-120">Seleccione el valor de hello **implementar un servidor de procesos de conmutación por recuperación de Azure**</span><span class="sxs-lookup"><span data-stu-id="fa933-120">Select hello value **Deploy a failback process server in Azure**</span></span> |
|<span data-ttu-id="fa933-121">La suscripción</span><span class="sxs-lookup"><span data-stu-id="fa933-121">Subscription</span></span>|<span data-ttu-id="fa933-122">Seleccione la suscripción de Azure que ha conmutado por error máquinas virtuales de Hola Hola</span><span class="sxs-lookup"><span data-stu-id="fa933-122">Select hello Azure Subscription where you failed over hello virtual machines</span></span>|
|<span data-ttu-id="fa933-123">Grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="fa933-123">Resource Group</span></span>|<span data-ttu-id="fa933-124">Puede crear un grupo de recursos toodeploy este servidor de procesos o elegir servidor de procesos de hello toodeploy en un grupo de recursos existente</span><span class="sxs-lookup"><span data-stu-id="fa933-124">You can create a Resource Group toodeploy this process server or choose toodeploy hello process server in an existing Resource Group</span></span>|
|<span data-ttu-id="fa933-125">Ubicación</span><span class="sxs-lookup"><span data-stu-id="fa933-125">Location</span></span>|<span data-ttu-id="fa933-126">Seleccione el centro de datos de Azure de hello en las máquinas virtuales que Hola donde conmutación por error en</span><span class="sxs-lookup"><span data-stu-id="fa933-126">Select hello Azure Data Center into which hello virtual machines where failed over into</span></span>|
|<span data-ttu-id="fa933-127">Red de Azure</span><span class="sxs-lookup"><span data-stu-id="fa933-127">Azure Network</span></span>|<span data-ttu-id="fa933-128">Seleccione hello Network(VNet) Virtual de Azure que Hola máquinas virtuales donde conmutación por error en.</span><span class="sxs-lookup"><span data-stu-id="fa933-128">Select hello Azure Virtual Network(VNet) that hello virtual machines where failed over into.</span></span> <span data-ttu-id="fa933-129">Si ha conmutado por error máquinas virtuales en varias redes virtuales de Azure, necesita un servidor de proceso implementado por red virtual.</span><span class="sxs-lookup"><span data-stu-id="fa933-129">If you failed over virtual machines into multiple Azure VNets, then you need a process server deployed per VNet</span></span>|

4. <span data-ttu-id="fa933-130">Rellene Hola resto de propiedades de hello en servidor de procesos de Hola</span><span class="sxs-lookup"><span data-stu-id="fa933-130">Fill in hello rest of hello properties for hello process server</span></span>

  ![Adición de un resumen del servidor de procesos](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-2.png)
|<span data-ttu-id="fa933-132">**Nombre del campo**</span><span class="sxs-lookup"><span data-stu-id="fa933-132">**Field Name**</span></span>|<span data-ttu-id="fa933-133">**Valor**</span><span class="sxs-lookup"><span data-stu-id="fa933-133">**Value**</span></span>|
|-|-|
|<span data-ttu-id="fa933-134">Nombre del servidor</span><span class="sxs-lookup"><span data-stu-id="fa933-134">Server Name</span></span>|<span data-ttu-id="fa933-135">Nombre para mostrar o nombre de host para la máquina virtual del servidor de procesos</span><span class="sxs-lookup"><span data-stu-id="fa933-135">Display name & Host name for your process server virtual machine</span></span>|
| <span data-ttu-id="fa933-136">User Name</span><span class="sxs-lookup"><span data-stu-id="fa933-136">User Name</span></span>|<span data-ttu-id="fa933-137">Nombre de usuario que se convierte en un administrador de esa máquina virtual</span><span class="sxs-lookup"><span data-stu-id="fa933-137">A user name that becomes an Administrator on that virtual machine</span></span>|
|<span data-ttu-id="fa933-138">Cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="fa933-138">Storage Account</span></span>|<span data-ttu-id="fa933-139">Nombre de cuenta de almacenamiento donde se coloca del disco virtual de la máquina virtual Hola Hola</span><span class="sxs-lookup"><span data-stu-id="fa933-139">Name of hello Storage Account where hello virtual machine's virtual disk's are placed</span></span>|
|<span data-ttu-id="fa933-140">Subred</span><span class="sxs-lookup"><span data-stu-id="fa933-140">Subnet</span></span>|<span data-ttu-id="fa933-141">Hola subred de máquina virtual de hello red virtual de Azure toowhich Hola está conectada</span><span class="sxs-lookup"><span data-stu-id="fa933-141">hello subnet of hello Azure VNet toowhich hello virtual machine is connected</span></span>|
| <span data-ttu-id="fa933-142">Dirección IP</span><span class="sxs-lookup"><span data-stu-id="fa933-142">IP Address</span></span>|<span data-ttu-id="fa933-143">Dirección IP que desearía Hola proceso servidor tooassume una vez que se inician</span><span class="sxs-lookup"><span data-stu-id="fa933-143">IP Address that you would like hello process server tooassume once it boots up</span></span>|
5. <span data-ttu-id="fa933-144">Haga clic en hello botón Aceptar toostart implementación de máquina virtual de hello proceso servidor.</span><span class="sxs-lookup"><span data-stu-id="fa933-144">Click hello OK button toostart deploying hello process server virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="fa933-145">toobe puede toouse este servidor de procesos de conmutación por recuperación, deberá tooregister con el servidor de configuración de hello en local.</span><span class="sxs-lookup"><span data-stu-id="fa933-145">toobe able toouse this process server for failback, you need tooregister it with hello on-premises configuration server.</span></span>

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a><span data-ttu-id="fa933-146">Registrar Hola proceso servidor (que se ejecuta en Azure) tooa servidor de configuración (ejecutando de forma local)</span><span class="sxs-lookup"><span data-stu-id="fa933-146">Registering hello process server (running in Azure) tooa Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a><span data-ttu-id="fa933-147">Actualizando Hola proceso toolatest versión del servidor.</span><span class="sxs-lookup"><span data-stu-id="fa933-147">Upgrading hello process server toolatest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="fa933-148">Al anular el registro de servidor de proceso de hello (que se ejecuta en Azure) desde un servidor de configuración (ejecutando de forma local)</span><span class="sxs-lookup"><span data-stu-id="fa933-148">Unregistering hello process server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-unregister-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
