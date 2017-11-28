---
title: " Administración de un servidor de procesos que se ejecuta en Azure (clásico) | Microsoft Docs"
description: "Este artículo se describe cómo tooset la una conmutación por recuperación Server(Classic) del proceso de Azure."
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
ms.openlocfilehash: eadcc0236c77c9ebbbc885c4a7ee81098f1f4e72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-classic"></a><span data-ttu-id="1255f-103">Administración de un servidor de procesos que se ejecuta en Azure (clásico)</span><span class="sxs-lookup"><span data-stu-id="1255f-103">Manage a Process Server running in Azure (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1255f-104">Azure clásico</span><span class="sxs-lookup"><span data-stu-id="1255f-104">Azure Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)
> * [<span data-ttu-id="1255f-105">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1255f-105">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

<span data-ttu-id="1255f-106">Durante la conmutación por recuperación, se recomienda toodeploy servidor de procesos en Azure si no hay una latencia elevada entre Hola red Virtual de Azure y la red local.</span><span class="sxs-lookup"><span data-stu-id="1255f-106">During failback, it is recommended toodeploy Process Server in Azure if there is high latency between hello Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="1255f-107">Este artículo describe cómo instalar, configurar y administrar servidores de procesos de hello ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="1255f-107">This article describes how you can set up, configure, and manage hello process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="1255f-108">Este artículo es toobe si utiliza clásico como modelo de implementación de Hola para las máquinas virtuales de Hola durante la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="1255f-108">This article is toobe used if you used Classic as hello deployment model for hello virtual machines during failover.</span></span> <span data-ttu-id="1255f-109">Si utiliza el Administrador de recursos como Hola pasos de implementación modelo seguimiento hello en [cómo tooset una copia de seguridad y configurar un servidor de procesos de conmutación por recuperación (Administrador de recursos)](./site-recovery-vmware-setup-azure-ps-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="1255f-109">If you used Resource Manager as hello deployment model follow hello steps in [How tooset up & configure a Failback Process Server (Resource Manager)](./site-recovery-vmware-setup-azure-ps-resource-manager.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1255f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1255f-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prereq](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="1255f-111">Implementación de un servidor de procesos en Azure</span><span class="sxs-lookup"><span data-stu-id="1255f-111">Deploy a Process Server on Azure</span></span>

1. <span data-ttu-id="1255f-112">En Azure Marketplace, cree una máquina virtual mediante hello **recuperación de sitio de Microsoft Azure proceso servidor V2**</span><span class="sxs-lookup"><span data-stu-id="1255f-112">In Azure Marketplace, create a virtual machine using hello **Microsoft Azure Site Recovery Process Server V2**</span></span> </br>
    <span data-ttu-id="1255f-113">![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span><span class="sxs-lookup"><span data-stu-id="1255f-113">![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span></span>
2. <span data-ttu-id="1255f-114">Asegúrese de seleccionar el modelo de implementación de hello como **clásico**</span><span class="sxs-lookup"><span data-stu-id="1255f-114">Ensure that you select hello deployment model as **Classic**</span></span> </br><span data-ttu-id="1255f-115">
  ![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span><span class="sxs-lookup"><span data-stu-id="1255f-115">
![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span></span>
3. <span data-ttu-id="1255f-116">En el Asistente para la máquina virtual de creación de hello > configuración básica, asegúrese de seleccionar toowhere de suscripción y la ubicación de hello conmutado hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="1255f-116">In hello Create virtual machine wizard > Basic Settings, ensure you select hello Subscription and Location toowhere you failed over hello virtual machines.</span></span></br><span data-ttu-id="1255f-117">
  ![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span><span class="sxs-lookup"><span data-stu-id="1255f-117">
![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span></span>
4. <span data-ttu-id="1255f-118">Asegúrese de que está conectada a esa máquina virtual de Hola Hola de toowhich de red Virtual de Azure toohello conmutado por máquina virtual está conectado.</span><span class="sxs-lookup"><span data-stu-id="1255f-118">Ensure that hello virtual machine is connected toohello Azure Virtual Network toowhich hello failed over virtual machine is connected.</span></span></br><span data-ttu-id="1255f-119">
  ![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span><span class="sxs-lookup"><span data-stu-id="1255f-119">
![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span></span>
5. <span data-ttu-id="1255f-120">Cuando se aprovisiona la máquina virtual de servidor de procesos de hello, toolog en es necesario y registrarlo con un servidor de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="1255f-120">Once hello Process Server virtual machine is provisioned, you need toolog in and register it with hello Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="1255f-121">toobe puede toouse este servidor de procesos de conmutación por recuperación, deberá tooregister con el servidor de configuración de hello en local.</span><span class="sxs-lookup"><span data-stu-id="1255f-121">toobe able toouse this Process Server for failback, you need tooregister it with hello on-premises configuration server.</span></span>

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a><span data-ttu-id="1255f-122">Registrar hello tooa de servidor de proceso (que se ejecuta en Azure) servidor de configuración (ejecutando de forma local)</span><span class="sxs-lookup"><span data-stu-id="1255f-122">Registering hello Process Server (running in Azure) tooa Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a><span data-ttu-id="1255f-123">Actualización de versión de toolatest del servidor de procesos de Hola.</span><span class="sxs-lookup"><span data-stu-id="1255f-123">Upgrading hello Process Server toolatest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="1255f-124">Hola al anular el registro de servidor de proceso (que se ejecuta en Azure) desde un servidor de configuración (ejecutando de forma local)</span><span class="sxs-lookup"><span data-stu-id="1255f-124">Unregistering hello Process Server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
