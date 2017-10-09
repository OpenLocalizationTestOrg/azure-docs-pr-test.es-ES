---
title: "aaaCreate una máquina virtual con una dirección pública estática de IP - portal de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una máquina virtual con una estática pública IP dirección utilizando Hola portal de Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e9546bcc-f300-428f-b94a-056c5bd29035
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f74d2132785f06148757409ee0a44b98d1e4b98e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-portal"></a><span data-ttu-id="fca43-103">Crear una máquina virtual con una dirección IP pública estática con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="fca43-103">Create a VM with a static public IP address using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="fca43-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="fca43-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="fca43-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fca43-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="fca43-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="fca43-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="fca43-107">Plantilla</span><span class="sxs-lookup"><span data-stu-id="fca43-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="fca43-108">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="fca43-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="fca43-109">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="fca43-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="fca43-110">Este artículo incluye el uso de modelo de implementación de administrador de recursos de hello, que Microsoft recomienda para la mayoría de las nueva implementaciones en lugar del modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="fca43-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="create-a-vm-with-a-static-public-ip"></a><span data-ttu-id="fca43-111">Creación de una máquina virtual con una IP pública estática</span><span class="sxs-lookup"><span data-stu-id="fca43-111">Create a VM with a static public IP</span></span>

<span data-ttu-id="fca43-112">toocreate una máquina virtual con una dirección IP pública estática de las direcciones de hello portal de Azure, Hola completa pasos:</span><span class="sxs-lookup"><span data-stu-id="fca43-112">toocreate a VM with a static public IP address in hello Azure portal, complete hello following steps:</span></span>

1. <span data-ttu-id="fca43-113">Desde un explorador, navegue toohello [portal de Azure](https://portal.azure.com) y, si es necesario, inicie sesión con su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="fca43-113">From a browser, navigate toohello [Azure portal](https://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="fca43-114">En la esquina superior izquierda de hello del portal de hello, haga clic en **New**>>**proceso**>**Windows Server 2012 R2 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="fca43-114">On hello top left hand corner of hello portal, click **New**>>**Compute**>**Windows Server 2012 R2 Datacenter**.</span></span>
3. <span data-ttu-id="fca43-115">Hola **seleccionar un modelo de implementación** seleccione **el Administrador de recursos** y haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="fca43-115">In hello **Select a deployment model** list, select **Resource Manager** and click **Create**.</span></span>
4. <span data-ttu-id="fca43-116">Hola **Fundamentos** hoja, escriba la información de la máquina virtual de hello tal y como se muestra a continuación y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="fca43-116">In hello **Basics** blade, enter hello VM information as shown below, and then click **OK**.</span></span>
   
    ![Portal de Azure: conceptos básicos](./media/virtual-network-deploy-static-pip-arm-portal/figure1.png)
5. <span data-ttu-id="fca43-118">Hola **elegir un tamaño de** hoja, haga clic en **estándar A1** tal y como se muestra a continuación y, a continuación, haga clic en **seleccione**.</span><span class="sxs-lookup"><span data-stu-id="fca43-118">In hello **Choose a size** blade, click **A1 Standard** as shown below, and then click **Select**.</span></span>
   
    ![Portal de Azure: elegir un tamaño](./media/virtual-network-deploy-static-pip-arm-portal/figure2.png)
6. <span data-ttu-id="fca43-120">Hola **configuración** hoja, haga clic en **dirección IP pública**, a continuación, en hello **Crear dirección IP pública** hoja, en **asignación**, haga clic en **Estático** tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="fca43-120">In hello **Settings** blade, click **Public IP address**, then in hello **Create public IP address** blade, under **Assignment**, click **Static** as shown below.</span></span> <span data-ttu-id="fca43-121">A continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="fca43-121">And then click **OK**.</span></span>
   
    ![Portal de Azure: crear la dirección IP pública](./media/virtual-network-deploy-static-pip-arm-portal/figure3.png)
7. <span data-ttu-id="fca43-123">Hola **configuración** hoja, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="fca43-123">In hello **Settings** blade, click **OK**.</span></span>
8. <span data-ttu-id="fca43-124">Hola de revisión **resumen** hoja, tal y como se muestra a continuación y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="fca43-124">Review hello **Summary** blade, as shown below, and then click **OK**.</span></span>
   
    ![Portal de Azure: crear la dirección IP pública](./media/virtual-network-deploy-static-pip-arm-portal/figure4.png)
9. <span data-ttu-id="fca43-126">Observe el nuevo icono de hello en el panel.</span><span class="sxs-lookup"><span data-stu-id="fca43-126">Notice hello new tile in your dashboard.</span></span>
   
    ![Portal de Azure: crear la dirección IP pública](./media/virtual-network-deploy-static-pip-arm-portal/figure5.png)
10. <span data-ttu-id="fca43-128">Una vez que se crea Hola VM, Hola **configuración** hoja se mostrarán tal y como se muestra a continuación</span><span class="sxs-lookup"><span data-stu-id="fca43-128">Once hello VM is created, hello **Settings** blade will be displayed as shown below</span></span>
    
    ![Portal de Azure: crear la dirección IP pública](./media/virtual-network-deploy-static-pip-arm-portal/figure6.png)

