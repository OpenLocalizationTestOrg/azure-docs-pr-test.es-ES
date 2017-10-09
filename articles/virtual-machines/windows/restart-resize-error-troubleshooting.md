---
title: "problemas de aaaVM reiniciar o cambiar el tamaño en Azure | Documentos de Microsoft"
description: "Solución de problemas de la implementación de Resource Manager con el reinicio o el cambio de tamaño de una máquina virtual de Windows existente en Azure"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 0756b52d-4f5a-4503-ae45-c00a6a2edcdf
ms.service: virtual-machines-windows
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.workload: required
ms.date: 06/13/2017
ms.author: delhan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2cf7c2d19bf5f79fab4ffc0eff9ccc1182d601c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-windows-vm-in-azure"></a>Solución de problemas de implementación con el reinicio o el cambio de tamaño de una máquina virtual Windows existente en Azure
Cuando intente toostart una máquina Virtual de Azure (VM) detenida, o cambiar el tamaño de una máquina virtual de Azure existente, se produce de error común de hello es un error de asignación. Este error se produce cuando el clúster de Hola o región no tenga recursos disponibles o no se solicitó que Hola de soporte técnico de tamaño de máquina virtual.

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a>Recopilación de registros de actividad
toostart solución de problemas, actividad hello recopilar registra el error de Hola de tooidentify asociada con el problema de Hola. Hola siguientes vínculos contiene información detallada sobre el proceso de hello:

[Ver operaciones de implementación](../../azure-resource-manager/resource-manager-deployment-operations.md)

[Ver registros de actividad toomanage Azure recursos](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a>Problema: Error al iniciar una máquina virtual detenida
Intente toostart una VM detenida pero obtendrá un error de asignación.

### <a name="cause"></a>Causa
solicitud de Hola Hola toostart detiene la máquina virtual tiene toobe vuelve a intentar cada clúster original Hola que aloja el servicio de nube de Hola. Sin embargo, el clúster de hello no tiene solicitud de espacio libre disponible toofulfill Hola.

### <a name="resolution"></a>Resolución
* Detener Hola todas las máquinas virtuales en la disponibilidad de Hola establecerán y, a continuación, reinicie cada máquina virtual.
  
  1. Haga clic en **Grupos de recursos** > *su grupo de recursos* > **Recursos** > *su conjunto de disponibilidad* > **Virtual Machines** > *su máquina virtual* > **Detener**.
  2. Después de que todos Hola detener las máquinas virtuales, seleccione cada una de las máquinas virtuales de hello detenido y haga clic en Inicio.
* Vuelva a intentar la solicitud de reinicio de hello en un momento posterior.

## <a name="issue-error-when-resizing-an-existing-vm"></a>Problema: error al reiniciar una máquina virtual existente
Intente tooresize una máquina virtual existente pero obtendrá un error de asignación.

### <a name="cause"></a>Causa
solicitud de Hola Hola tooresize VM tiene toobe intentaba ejecutar en clúster original Hola ese servicio de nube de Hola de hosts. Sin embargo, no es compatible con clúster de Hola Hola solicitado tamaño de máquina virtual.

### <a name="resolution"></a>Resolución
* Vuelva a intentar la solicitud Hola con un tamaño más pequeño de la máquina virtual.
* Si hello tamaño de hello solicitada que no se puede cambiar la máquina virtual:
  
  1. Detener todas las máquinas virtuales de hello en el conjunto de disponibilidad de Hola.
     
     * Haga clic en **Grupos de recursos** > *su grupo de recursos* > **Recursos** > *su conjunto de disponibilidad* > **Virtual Machines** > *su máquina virtual* > **Detener**.
  2. Después de que todos Hola detener las máquinas virtuales, cambie el tamaño deseado de hello VM tooa mayor tamaño.
  3. Cambiar el tamaño Hola seleccione máquina virtual y haga clic en **iniciar**, y, a continuación, inicie cada Hola detiene máquinas virtuales.

## <a name="next-steps"></a>Pasos siguientes
Si surgen problemas al crear una nueva máquina virtual Windows en Azure, consulte [Solución de problemas de implementación de Resource Manager con la creación de una máquina virtual de Windows en Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

