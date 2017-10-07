---
title: "implementación de máquina virtual de Windows en Azure aaaTroubleshoot | Documentos de Microsoft"
description: "Solución de problemas de implementación de Resource Manager cuando crea una nueva máquina virtual de Windows en Azure"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.assetid: afc6c1a4-2769-41f6-bbf9-76f9f23bcdf4
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: cjiang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c27d4f63b67db2d1c9f117f05a2eba9ef130ef37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-when-creating-a-new-windows-vm-in-azure"></a>Solución de problemas de implementación al crear una nueva máquina virtual Windows en Azure
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a>Principales problemas
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

Para consultar otros problemas de implementación de máquinas virtuales y preguntas, vea [Troubleshoot deploying Linux virtual machine issues in Azure](troubleshoot-deploy-vm.md) (Solución de problemas de implementación de máquinas virtuales de Windows en Azure).

## <a name="collect-activity-logs"></a>Recopilación de registros de actividad
toostart solución de problemas, actividad hello recopilar registra el error de Hola de tooidentify asociada con el problema de Hola. Hello vínculos siguientes contienen información detallada sobre Hola proceso toofollow.

[Ver operaciones de implementación](../../azure-resource-manager/resource-manager-deployment-operations.md)

[Ver registros de actividad toomanage Azure recursos](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-windows-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-windows-troubleshoot-deployment-new-vm-table.md)]

**Y:** si Hola sistema operativo es Windows generalizado y se ha cargado ni capturado con hello generalizado configuración, no habrá errores. Del mismo modo, si Hola sistema operativo es Windows especializado, y se ha cargado ni capturado con hello especializados configuración, a continuación, no habrá errores.

**Errores de carga:**

**N<sup>1</sup>:** si Hola sistema operativo es Windows generalizado, y se carga como especializado, obtendrá un error de tiempo de espera aprovisionamiento con hello VM atascada en pantalla de bienvenida OOBE.

**N<sup>2</sup>:** si hello sistema operativo es Windows especializados y cargarlo como generalizado, obtendrá un error de aprovisionamiento con hello VM atascada en pantalla de bienvenida OOBE porque hello nueva máquina virtual se está ejecutando con el equipo original de Hola nombre, nombre de usuario y contraseña.

**Resolución**

tooresolve ambos estos errores, utilice [tooupload AzureRmVhd agregar Hola VHD original](https://msdn.microsoft.com/library/mt603554.aspx), de forma local, con hello misma configuración que para hello OS (generalizado/especializado). tooupload como generalizado, recuerde toorun sysprep en primer lugar.

**Errores de captura:**

**N<sup>3</sup>:** si Hola sistema operativo es Windows generalizado, y se capturan como especializado, obtendrá un error de tiempo de espera de aprovisionamiento porque Hola original máquina virtual no se puede usar tal y como está marcado como generalizado.

**N<sup>4</sup>:** si hello sistema operativo es Windows especializada y se capturan como generalizado, obtendrá un error de aprovisionamiento porque hello nueva máquina virtual se está ejecutando con el nombre de equipo original de hello, username y password. Además, Hola original VM no es puede usar porque está marcado como especializadas.

**Resolución**

tooresolve ambos estos errores, eliminar la imagen actual de Hola desde el portal de hello, y [capturar de hello VHD actual](create-vm-specialized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) con Hola la misma configuración que para hello OS (generalizado/especializado).

## <a name="issue-customgallerymarketplace-image-allocation-failure"></a>Problema: Imagen de galería/marketplace/personalizada; error de asignación
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
Si tiene problemas al iniciar una máquina virtual Windows detenida o al cambiar el tamaño de una máquina virtual Windows existente en Azure, consulte [Solución de problemas de la implementación de Resource Manager con el reinicio o el cambio de tamaño de una máquina virtual de Windows existente en Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

