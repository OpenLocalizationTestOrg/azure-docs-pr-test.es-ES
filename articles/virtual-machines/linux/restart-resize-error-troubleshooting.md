---
title: "Problemas de reinicio o cambio de tamaño de las máquinas virtuales de Azure | Microsoft Docs"
description: "Solución de problemas de la implementación de Resource Manager con el reinicio o el cambio de tamaño de una máquina virtual de Linux existente en Azure"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 51f1610c-0290-464a-97d4-c2e485c7ae7f
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.workload: required
ms.date: 01/10/2017
ms.author: delhan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e49322dbccf4ec1157bc7e3a109175869b53518d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-linux-vm-in-azure"></a>Solución de problemas de implementación con el reinicio o el cambio de tamaño de una máquina virtual Linux existente en Azure
Al intentar iniciar una máquina virtual de Azure detenida o cambiar el tamaño de una máquina virtual de Azure existente, es común encontrarse un error de asignación. Dicho error se produce cuando el clúster o la región no tienen recursos disponibles o no admiten el tamaño de máquina virtual solicitado.

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a>Recopilación de registros de actividad
Para iniciar la solución de problemas, recopile los registros de actividad para identificar el error asociado con el problema. Los vínculos siguientes contienen información detallada sobre el proceso:

[Ver operaciones de implementación](../../azure-resource-manager/resource-manager-deployment-operations.md)

[Ver registros de actividad para administrar recursos de Azure](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a>Problema: Error al iniciar una máquina virtual detenida
Intenta iniciar una máquina virtual detenida, pero obtiene un error de asignación.

### <a name="cause"></a>Causa
La solicitud de iniciar la máquina virtual detenida se debe intentar en el clúster original que hospeda el servicio en la nube. Sin embargo, el clúster no tiene espacio libre disponible para responder a la solicitud.

### <a name="resolution"></a>Resolución
* Detenga todas las máquinas virtuales del conjunto de disponibilidad y reinicie las máquinas virtuales.
  
  1. Haga clic en **Grupos de recursos** > *su grupo de recursos* > **Recursos** > *su conjunto de disponibilidad* > **Virtual Machines** > *su máquina virtual* > **Detener**.
  2. Después de detener todas las máquinas virtuales, selecciónelas y haga clic en Iniciar.
* Vuelva a intentar solicitar el reinicio más tarde.

## <a name="issue-error-when-resizing-an-existing-vm"></a>Problema: error al reiniciar una máquina virtual existente
Intenta cambiar el tamaño de una máquina virtual existente, pero obtiene un error de asignación.

### <a name="cause"></a>Causa
La solicitud de cambiar el tamaño de la máquina virtual se debe realizar en el clúster original que alberga el servicio en la nube. Sin embargo, el clúster no admite el tamaño de máquina virtual solicitado.

### <a name="resolution"></a>Resolución
* Vuelva a intentar la solicitud con un tamaño de máquina virtual menor.
* Si no se puede cambiar el tamaño de la máquina virtual solicitada:
  
  1. Detenga todas las máquinas virtuales en el conjunto de disponibilidad.
     
     * Haga clic en **Grupos de recursos** > *su grupo de recursos* > **Recursos** > *su conjunto de disponibilidad* > **Virtual Machines** > *su máquina virtual* > **Detener**.
  2. Después de detener todas las máquinas virtuales, aumente el tamaño de la máquina virtual que quiera.
  3. Seleccione la máquina virtual cuyo tamaño ha cambiado, haga clic en **Iniciar**e inicie las máquinas virtuales detenidas.

## <a name="next-steps"></a>Pasos siguientes
Si surgen problemas al crear una nueva máquina virtual Linux en Azure, consulte [Solución de problemas de la implementación de Resource Manager con la creación de una nueva máquina virtual de Linux en Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

