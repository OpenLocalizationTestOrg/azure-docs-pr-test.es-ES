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
# <a name="redeploy-windows-virtual-machine-toonew-azure-node"></a>Volver a implementar toonew de máquina virtual de Windows Azure nodo
Si ha estado enfrentando dificultades solución de problemas de escritorio remoto (RDP) conexión o la aplicación acceder a tooWindows-based Azure máquina virtual (VM), volver a implementar Hola puede ayudar la máquina virtual. Cuando se vuelve a implementar una máquina virtual, se desplaza Hola VM tooa nuevo nodo dentro de hello infraestructura de Azure y, a continuación, lo enciende volver, conservando todas las opciones de configuración y recursos asociados. Este artículo muestra cómo tooredeploy una máquina virtual con Azure PowerShell o hello portal de Azure.

> [!NOTE]
> Después de volver a implementar una máquina virtual, se perderá disco temporal de Hola y direcciones IP dinámicas asociadas con la interfaz de red virtual se actualizan. 


## <a name="using-azure-powershell"></a>Uso de Azure PowerShell
Asegúrese de que haya Hola más reciente de PowerShell de Azure 1.x instalados en su equipo. Para obtener más información, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).

Hello en el ejemplo siguiente se implementa Hola máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup`:

```powershell
Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
```


[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a>Pasos siguientes
Si tiene problemas para conectarse tooyour VM, puede buscar ayuda específica en [solución de problemas de las conexiones RDP](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) o [detallan los pasos para solucionar problemas de RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). También puede leer sobre la [solución de problemas de aplicaciones](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) si no puede acceder a una aplicación que se ejecuta en la máquina virtual.

