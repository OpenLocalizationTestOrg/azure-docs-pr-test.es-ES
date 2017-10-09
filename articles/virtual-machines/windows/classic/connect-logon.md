---
title: "aaaLog en tooa VM de Azure clásico | Documentos de Microsoft"
description: "Usar hello toolog de portal de Azure en la máquina virtual de tooa Windows creada con el modelo de implementación clásica de Hola."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 3c1239ed-07dc-48b8-8b3d-dc8c5f0ab20e
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 2e32b7036c2538e73b46580e0f5f8f4979e8a685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="log-on-tooa-windows-virtual-machine-using-hello-azure-portal"></a><span data-ttu-id="bd180-103">Inicie sesión en tooa máquina virtual de Windows con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="bd180-103">Log on tooa Windows virtual machine using hello Azure portal</span></span>
<span data-ttu-id="bd180-104">Hola portal de Azure, use hello **conectar** botón toostart una sesión de escritorio remoto y tooa VM de Windows de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="bd180-104">In hello Azure portal, you use hello **Connect** button toostart a Remote Desktop session and log on tooa Windows VM.</span></span>

<span data-ttu-id="bd180-105">¿Desea tooconnect tooa VM de Linux?</span><span class="sxs-lookup"><span data-stu-id="bd180-105">Do you want tooconnect tooa Linux VM?</span></span> <span data-ttu-id="bd180-106">Vea [cómo toolog en la máquina virtual de tooa ejecutan Linux](../../linux/mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="bd180-106">See [How toolog on tooa virtual machine running Linux](../../linux/mac-create-ssh-keys.md).</span></span>

<!--
Deleting, but not 100% sure
Learn how too[perform these steps using new Azure portal](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

> [!IMPORTANT]
> <span data-ttu-id="bd180-107">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="bd180-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="bd180-108">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="bd180-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="bd180-109">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd180-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="bd180-110">Para obtener información acerca de cómo toolog sobre el uso de la máquina virtual de tooa Hola Administrador de recursos del modelo, vea [aquí](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bd180-110">For information about how toolog on tooa VM using hello Resource Manager model, see [here](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="bd180-111">Conectar máquina virtual de toohello</span><span class="sxs-lookup"><span data-stu-id="bd180-111">Connect toohello virtual machine</span></span>
1. <span data-ttu-id="bd180-112">Inicie sesión en toohello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="bd180-112">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="bd180-113">Haga clic en la máquina virtual de Hola que desea tooaccess.</span><span class="sxs-lookup"><span data-stu-id="bd180-113">Click on hello virtual machine that you want tooaccess.</span></span> <span data-ttu-id="bd180-114">Hola nombre aparece en hello **todos los recursos** panel.</span><span class="sxs-lookup"><span data-stu-id="bd180-114">hello name is listed in hello **All resources** pane.</span></span>

    ![Virtual-machine-locations](./media/connect-logon/azureportaldashboard.png)

3. <span data-ttu-id="bd180-116">Haga clic en **conectar** en la barra de comandos de hello encima del panel de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd180-116">Click **Connect** on hello command bar atop hello virtual machine dashboard.</span></span>

    ![Icono de la máquina virtual de hello Connect](./media/connect-logon/virtualmachine_dashboard_connect.png)

<!-- Don't know if this still applies
     I think we can zap this.
> [!TIP]
> If hello **Connect** button isn't available, see hello troubleshooting tips at hello end of this article.
>
>
-->

## <a name="log-on-toohello-virtual-machine"></a><span data-ttu-id="bd180-118">Inicie sesión en la máquina virtual de toohello</span><span class="sxs-lookup"><span data-stu-id="bd180-118">Log on toohello virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="bd180-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bd180-119">Next steps</span></span>
* <span data-ttu-id="bd180-120">Si hello **conectar** botón está inactivo o tiene otros problemas con conexión a Escritorio remoto hello, pruebe a restablecer la configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd180-120">If hello **Connect** button is inactive or you are having other problems with hello Remote Desktop connection, try resetting hello configuration.</span></span> <span data-ttu-id="bd180-121">Haga clic en **restablecer el acceso remoto** desde el panel de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd180-121">click **Reset remote access** from hello virtual machine dashboard.</span></span>

    ![Reset-remote-access](./media/connect-logon/virtualmachine_dashboard_reset_remote_access.png)

* <span data-ttu-id="bd180-123">Si experimenta problemas con la contraseña, intente restablecerla.</span><span class="sxs-lookup"><span data-stu-id="bd180-123">For problems with your password, try resetting it.</span></span> <span data-ttu-id="bd180-124">Haga clic en **de restablecimiento de contraseña** a lo largo de hello borde izquierdo del panel de la máquina virtual, en **soporte técnico y solución de problemas**.</span><span class="sxs-lookup"><span data-stu-id="bd180-124">Click **Reset password** along hello left edge of virtual machine dashboard, under **Support + Troubleshooting**.</span></span>

    ![Reset-password](./media/connect-logon/virtualmachine_dashboard_reset_password.png)

<span data-ttu-id="bd180-126">Si las sugerencias no funcionan o no son lo que necesita, consulte [tooa de conexiones de escritorio remoto solucionar problemas de máquina Virtual de Azure basado en Windows](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bd180-126">If those tips don't work or aren't what you need, see [Troubleshoot Remote Desktop connections tooa Windows-based Azure Virtual Machine](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="bd180-127">En este artículo se le guiará a través del diagnóstico y la resolución de problemas comunes.</span><span class="sxs-lookup"><span data-stu-id="bd180-127">This article walks you through diagnosing and resolving common problems.</span></span>
