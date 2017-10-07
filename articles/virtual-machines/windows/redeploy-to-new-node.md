---
title: "máquinas virtuales de Windows aaaRedeploy en Azure | Documentos de Microsoft"
description: "Cómo Windows tooredeploy virtual máquinas en Azure toomitigate RDP problemas de conexión."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: genlin
manager: timlt
tags: azure-resource-manager,top-support-issue
ms.assetid: 0ee456ee-4595-4a14-8916-72c9110fc8bd
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 903d9d5bf241075931ee4b746690c553d808a58f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-windows-virtual-machine-toonew-azure-node"></a><span data-ttu-id="42a4c-103">Volver a implementar toonew de máquina virtual de Windows Azure nodo</span><span class="sxs-lookup"><span data-stu-id="42a4c-103">Redeploy Windows virtual machine toonew Azure node</span></span>
<span data-ttu-id="42a4c-104">Si ha estado enfrentando dificultades solución de problemas de escritorio remoto (RDP) conexión o la aplicación acceder a tooWindows-based Azure máquina virtual (VM), volver a implementar Hola puede ayudar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="42a4c-104">If you have been facing difficulties troubleshooting Remote Desktop (RDP) connection or application access tooWindows-based Azure virtual machine (VM), redeploying hello VM may help.</span></span> <span data-ttu-id="42a4c-105">Cuando se vuelve a implementar una máquina virtual, se desplaza Hola VM tooa nuevo nodo dentro de hello infraestructura de Azure y, a continuación, lo enciende volver, conservando todas las opciones de configuración y recursos asociados.</span><span class="sxs-lookup"><span data-stu-id="42a4c-105">When you redeploy a VM, it moves hello VM tooa new node within hello Azure infrastructure and then powers it back on, retaining all your configuration options and associated resources.</span></span> <span data-ttu-id="42a4c-106">Este artículo muestra cómo tooredeploy una máquina virtual con Azure PowerShell o hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="42a4c-106">This article shows you how tooredeploy a VM using Azure PowerShell or hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="42a4c-107">Después de volver a implementar una máquina virtual, se perderá disco temporal de Hola y direcciones IP dinámicas asociadas con la interfaz de red virtual se actualizan.</span><span class="sxs-lookup"><span data-stu-id="42a4c-107">After you redeploy a VM, hello temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 


## <a name="using-azure-powershell"></a><span data-ttu-id="42a4c-108">Uso de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="42a4c-108">Using Azure PowerShell</span></span>
<span data-ttu-id="42a4c-109">Asegúrese de que haya Hola más reciente de PowerShell de Azure 1.x instalados en su equipo.</span><span class="sxs-lookup"><span data-stu-id="42a4c-109">Make sure you have hello latest Azure PowerShell 1.x installed on your machine.</span></span> <span data-ttu-id="42a4c-110">Para obtener más información, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="42a4c-110">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="42a4c-111">Hello en el ejemplo siguiente se implementa Hola máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="42a4c-111">hello following example deploys hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```powershell
Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
```


[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="42a4c-112">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="42a4c-112">Next steps</span></span>
<span data-ttu-id="42a4c-113">Si tiene problemas para conectarse tooyour VM, puede buscar ayuda específica en [solución de problemas de las conexiones RDP](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) o [detallan los pasos para solucionar problemas de RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="42a4c-113">If you are having issues connecting tooyour VM, you can find specific help on [troubleshooting RDP connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [detailed RDP troubleshooting steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="42a4c-114">También puede leer sobre la [solución de problemas de aplicaciones](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) si no puede acceder a una aplicación que se ejecuta en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="42a4c-114">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

