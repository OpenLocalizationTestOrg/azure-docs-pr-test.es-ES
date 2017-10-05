---
title: " Administración de un servidor de procesos que se ejecuta en Azure (clásico) | Microsoft Docs"
description: "En este artículo se describe cómo configurar un servidor de procesos (clásico) de conmutación por recuperación en Azure."
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
ms.openlocfilehash: 479bbd207bcf715138c340f9e4d2634120bab85c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-process-server-running-in-azure-classic"></a><span data-ttu-id="08c16-103">Administración de un servidor de procesos que se ejecuta en Azure (clásico)</span><span class="sxs-lookup"><span data-stu-id="08c16-103">Manage a Process Server running in Azure (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="08c16-104">Azure clásico</span><span class="sxs-lookup"><span data-stu-id="08c16-104">Azure Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)
> * [<span data-ttu-id="08c16-105">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="08c16-105">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

<span data-ttu-id="08c16-106">Durante la conmutación por recuperación, se recomienda implementar el servidor de procesos en Azure si hay una latencia elevada entre la red virtual de Azure y la red local.</span><span class="sxs-lookup"><span data-stu-id="08c16-106">During failback, it is recommended to deploy Process Server in Azure if there is high latency between the Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="08c16-107">En este artículo se describe cómo instalar, configurar y administrar los servidores de procesos que se ejecutan en Azure.</span><span class="sxs-lookup"><span data-stu-id="08c16-107">This article describes how you can set up, configure, and manage the process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="08c16-108">Este artículo se utiliza si ha usado Clásico como modelo de implementación para las máquinas virtuales durante la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="08c16-108">This article is to be used if you used Classic as the deployment model for the virtual machines during failover.</span></span> <span data-ttu-id="08c16-109">Si ha usado el modelo Resource Manager como modelo de implementación, siga los pasos de [Administración de un servidor de procesos de conmutación por recuperación (Resource Manager)](./site-recovery-vmware-setup-azure-ps-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="08c16-109">If you used Resource Manager as the deployment model follow the steps in [How to set up & configure a Failback Process Server (Resource Manager)](./site-recovery-vmware-setup-azure-ps-resource-manager.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08c16-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="08c16-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prereq](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="08c16-111">Implementación de un servidor de procesos en Azure</span><span class="sxs-lookup"><span data-stu-id="08c16-111">Deploy a Process Server on Azure</span></span>

1. <span data-ttu-id="08c16-112">En Azure Marketplace, cree una máquina virtual utilizando el **servidor de procesos de Microsoft Azure Site Recovery V2**</span><span class="sxs-lookup"><span data-stu-id="08c16-112">In Azure Marketplace, create a virtual machine using the **Microsoft Azure Site Recovery Process Server V2**</span></span> </br>
    <span data-ttu-id="08c16-113">![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span><span class="sxs-lookup"><span data-stu-id="08c16-113">![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span></span>
2. <span data-ttu-id="08c16-114">Asegúrese de seleccionar **Clásico** como modelo de implementación.</span><span class="sxs-lookup"><span data-stu-id="08c16-114">Ensure that you select the deployment model as **Classic**</span></span> </br><span data-ttu-id="08c16-115">
  ![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span><span class="sxs-lookup"><span data-stu-id="08c16-115">
![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span></span>
3. <span data-ttu-id="08c16-116">En el Asistente para creación de máquina virtual > Configuración básica, asegúrese de activar la suscripción y ubicación en donde ha conmutado por error las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="08c16-116">In the Create virtual machine wizard > Basic Settings, ensure you select the Subscription and Location to where you failed over the virtual machines.</span></span></br><span data-ttu-id="08c16-117">
  ![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span><span class="sxs-lookup"><span data-stu-id="08c16-117">
![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span></span>
4. <span data-ttu-id="08c16-118">Asegúrese de que la máquina virtual está conectada a la red virtual de Azure a la que está conectada máquina virtual con conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="08c16-118">Ensure that the virtual machine is connected to the Azure Virtual Network to which the failed over virtual machine is connected.</span></span></br><span data-ttu-id="08c16-119">
  ![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span><span class="sxs-lookup"><span data-stu-id="08c16-119">
![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span></span>
5. <span data-ttu-id="08c16-120">Cuando se aprovisiona la máquina virtual del servidor de procesos, debe iniciar sesión y registrarlo con el servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="08c16-120">Once the Process Server virtual machine is provisioned, you need to log in and register it with the Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="08c16-121">Para poder usar este servidor de procesos para la conmutación por recuperación, hay que registrarlo con el servidor de configuración local.</span><span class="sxs-lookup"><span data-stu-id="08c16-121">To be able to use this Process Server for failback, you need to register it with the on-premises configuration server.</span></span>

## <a name="registering-the-process-server-running-in-azure-to-a-configuration-server-running-on-premises"></a><span data-ttu-id="08c16-122">Registro del servidor de procesos (que se ejecuta en Azure) en un servidor de configuración (que se ejecuta de forma local)</span><span class="sxs-lookup"><span data-stu-id="08c16-122">Registering the Process Server (running in Azure) to a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-the-process-server-to-latest-version"></a><span data-ttu-id="08c16-123">Actualización del servidor de procesos a la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="08c16-123">Upgrading the Process Server to latest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-the-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="08c16-124">Anulación del registro del servidor de procesos (que se ejecuta en Azure) desde un servidor de configuración (que se ejecuta de forma local)</span><span class="sxs-lookup"><span data-stu-id="08c16-124">Unregistering the Process Server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
