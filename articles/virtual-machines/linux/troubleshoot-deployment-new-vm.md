---
title: "implementación de VM de Linux-RM aaaTroubleshoot | Documentos de Microsoft"
description: "Solución de problemas de implementación de Resource Manager cuando crea una nueva máquina virtual de Linux en Azure"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue, azure-resource-manager
ms.assetid: 906a9c89-6866-496b-b4a4-f07fb39f990c
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/09/2016
ms.author: cjiang
ms.openlocfilehash: 2dd7f1855bba75d86eb90f88e6d573cd42fd8d87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-resource-manager-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a>Solución de problemas de la implementación de Resource Manager con la creación de una nueva máquina virtual de Linux en Azure
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a>Principales problemas
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

Para consultar otros problemas de implementación de máquinas virtuales y preguntas, vea [Troubleshoot deploying Linux virtual machine issues in Azure](troubleshoot-deploy-vm.md) (Solución de problemas de implementación de máquinas virtuales de Linux en Azure).
## <a name="collect-activity-logs"></a>Recopilación de registros de actividad
toostart solución de problemas, actividad hello recopilar registra el error de Hola de tooidentify asociada con el problema de Hola. Hello vínculos siguientes contienen información detallada sobre Hola proceso toofollow.

[Ver operaciones de implementación](../../azure-resource-manager/resource-manager-deployment-operations.md)

[Ver registros de actividad toomanage Azure recursos](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

**Y:** si Hola SO es Linux generalizado y se ha cargado ni capturado con hello generalizado configuración, no habrá errores. De forma similar, si Hola SO está especializado de Linux, y se ha cargado ni capturado con hello especializados configuración, a continuación, no habrá los errores.

**Errores de carga:**

**N<sup>1</sup>:** si Hola SO es Linux generalizado, y se carga como especializado, obtendrá un error de tiempo de espera de aprovisionamiento porque Hola VM está atascada en hello fase de aprovisionamiento.

**N<sup>2</sup>:** si hello SO es especializado de Linux y cargarlo como generalizado, obtendrá un error de aprovisionamiento porque hello nueva máquina virtual se está ejecutando con el nombre de equipo original de hello, username y password.

**Resolución:**

tooresolve ambos estos errores, cargar Hola VHD original, disponible en local, con Hola misma configuración que para hello OS (generalizado/especializado). tooupload como generalizado, recuerde toorun-desaprovisionar primero.

**Errores de captura:**

**N<sup>3</sup>:** si Hola SO es Linux generalizado, y se capturan como especializado, obtendrá un error de tiempo de espera de aprovisionamiento porque Hola original máquina virtual no se puede usar tal y como está marcado como generalizado.

**N<sup>4</sup>:** si hello SO es especializado de Linux, y se capturan como generalizado, obtendrá un error de aprovisionamiento porque hello nueva máquina virtual se está ejecutando con el nombre de equipo original de hello, username y password. Además, Hola original VM no es puede usar porque está marcado como especializadas.

**Resolución:**

tooresolve ambos estos errores, eliminar la imagen actual de Hola desde el portal de hello, y [capturar de hello VHD actual](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) con Hola la misma configuración que para hello OS (generalizado/especializado).

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a>Problema: Imagen de galería/marketplace/personalizada; error de asignación
Este error se produce en situaciones cuando la solicitud de máquina virtual nueva de hello es clúster tooa anclados que no es compatible con el tamaño de la máquina virtual de Hola que se solicita o no tiene espacio libre disponible tooaccommodate Hola solicitud.

**Causa 1:** no admiten clústeres de Hola Hola solicitado tamaño de máquina virtual.

**Resolución 1:**

* Vuelva a intentar la solicitud Hola con un tamaño más pequeño de la máquina virtual.
* Si hello tamaño de hello solicitada que no se puede cambiar la máquina virtual:
  * Detener todas las máquinas virtuales de hello en el conjunto de disponibilidad de Hola.
    Haga clic en **Grupos de recursos** > *su grupo de recursos* > **Recursos** > *su conjunto de disponibilidad* > **Virtual Machines** > *su máquina virtual* > **Detener**.
  * Después de que todos los hello detener las máquinas virtuales, crear Hola nueva máquina virtual en hello tamaño deseado.
  * Iniciar Hola nueva máquina virtual en primer lugar y, a continuación, seleccione cada uno de hello detiene las máquinas virtuales y haga clic en **iniciar**.

**Causa 2:** Hola clúster no tiene recursos libres.

**Resolución 2:**

* Vuelva a intentar la solicitud de hello en un momento posterior.
* Si puede hello nueva máquina virtual se establecer parte de una disponibilidad diferentes
  * Crear una nueva máquina virtual en un conjunto de disponibilidad diferentes (Hola misma región).
  * Agregar Hola nueva VM toohello misma red virtual.

## <a name="next-steps"></a>Pasos siguientes
Si tiene problemas al iniciar una máquina virtual Linux detenida o al cambiar el tamaño de una máquina virtual Linux existente en Azure, consulte [Solución de problemas de la implementación de Resource Manager con el reinicio o el cambio de tamaño de una máquina virtual de Linux existente en Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

