---
title: "aaaVM reiniciar o cambiar el tamaño de problemas | Documentos de Microsoft"
description: "Solución de problemas de la implementación clásica con el reinicio o el cambio de tamaño de una máquina virtual de Windows existente en Azure"
services: virtual-machines-windows
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: aa854fff-c057-4b8e-ad77-e4dbc39648cc
ms.service: virtual-machines-windows
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.workload: required
ms.date: 06/13/2017
ms.devlang: na
ms.author: delhan
ms.openlocfilehash: 3d00ba17d9558941a37a29034604cb15e0803e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-windows-virtual-machine-in-azure"></a>Solución de problemas de la implementación clásica con el reinicio o el cambio de tamaño de una máquina virtual de Windows existente en Azure
> [!div class="op_single_selector"]
> * [Clásico](virtual-machines-windows-classic-restart-resize-error-troubleshooting.md)
> * [Resource Manager](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
> 
> 

Cuando intente toostart una máquina Virtual de Azure (VM) detenida, o cambiar el tamaño de una máquina virtual de Azure existente, se produce de error común de hello es un error de asignación. Este error se produce cuando el clúster de Hola o región no tenga recursos disponibles o no se solicitó que Hola de soporte técnico de tamaño de máquina virtual.

> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../azure-resource-manager/resource-manager-deployment-model.md).  Este artículo incluye el uso de modelo de implementación clásica de Hola. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.
> 
> 

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a>Recopilación de registros de auditoría
toostart solución de problemas, auditoría de hello recopilar registra el error de Hola de tooidentify asociada con el problema de Hola.

Hola portal de Azure, haga clic en **examinar** > **máquinas virtuales** > *la máquina virtual de Windows*  >   **Configuración de** > **registros de auditoría**.

## <a name="issue-error-when-starting-a-stopped-vm"></a>Problema: Error al iniciar una máquina virtual detenida
Intente toostart una VM detenida pero obtendrá un error de asignación.

### <a name="cause"></a>Causa
solicitud de Hola Hola toostart detiene la máquina virtual tiene toobe vuelve a intentar cada clúster original Hola que aloja el servicio de nube de Hola. Sin embargo, el clúster de hello no tiene solicitud de espacio libre disponible toofulfill Hola.

### <a name="resolution"></a>Resolución
* Cree un nuevo servicio en la nube y asócielo con una región o con una red virtual basada en regiones, pero con no un grupo de afinidad.
* Eliminar Hola detiene la máquina virtual.
* Vuelva a crear Hola VM Hola nuevo servicio en nube mediante el uso de discos de Hola.
* Iniciar Hola vuelve a crea la máquina virtual.

Si se produce un error al tratar de toocreate un nuevo servicio de nube, ya sea a intentarlo más tarde o cambiar región Hola Hola servicio de nube.

> [!IMPORTANT]
> servicio de nube nuevo Hola tendrá un nuevo nombre y la dirección VIP, por lo que deberá toochange esa información para todas las dependencias de Hola que usan esa información de servicio en la nube Hola.
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a>Problema: error al reiniciar una máquina virtual existente
Intente tooresize una máquina virtual existente pero obtendrá un error de asignación.

### <a name="cause"></a>Causa
solicitud de Hola Hola tooresize VM tiene toobe intentaba ejecutar en clúster original Hola ese servicio de nube de Hola de hosts. Sin embargo, no es compatible con clúster de Hola Hola solicitado tamaño de máquina virtual.

### <a name="resolution"></a>Resolución
Reducir tamaño de máquina virtual solicita el Hola y Hola vuelva a intentar cambiar el tamaño de solicitud.

* Haga clic en **Examinar todo** > **Máquinas virtuales (clásico)** > *su máquina virtual* > **Configuración** > **Tamaño**. Para obtener instrucciones detalladas, consulte [cambiar el tamaño de máquina virtual de hello](https://msdn.microsoft.com/library/dn168976.aspx).

Si no es posible tooreduce Hola tamaño de máquina virtual, siga estos pasos:

* Crear un nuevo servicio de nube, asegurando que se no trata vinculado tooan grupo de afinidad y no asociada a una red virtual que está vinculado tooan grupo de afinidad.
* Cree una máquina virtual nueva y de mayor tamaño en dicho servicio.

Es posible consolidar todas las máquinas virtuales en hello mismo servicio en la nube. Si su servicio en la nube está asociado a una red virtual basada en la región, puede conectarse Hola nueva nube servicio toohello red virtual existente.

Si Hola existente en la nube servicio no está asociado a ninguna red virtual basadas en regiones, a continuación, tiene toodelete hello las máquinas virtuales en el servicio de nube existente de hello y volver a crearlos en hello nuevo servicio en la nube desde sus discos. Sin embargo, es importante tooremember que el servicio de nube nuevo de Hola tendrá un nuevo nombre y la dirección VIP, por lo que deberá tooupdate para todas las dependencias de Hola que actualmente utilizan esta información para servicio de nube existente de Hola.

## <a name="next-steps"></a>Pasos siguientes
Si se producen problemas al crear una máquina virtual con Windows en Azure, vea [Solución de problemas de implementación con la creación de una máquina virtual con Windows en Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

