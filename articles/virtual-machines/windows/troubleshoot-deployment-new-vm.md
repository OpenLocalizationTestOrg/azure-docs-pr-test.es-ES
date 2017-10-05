---
title: "Solución de problemas de implementación de máquinas virtuales Windows en Azure | Microsoft Docs"
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
ms.openlocfilehash: 86795ba6eab3505a3d539e4fc4e032bdeecc2e78
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-deployment-issues-when-creating-a-new-windows-vm-in-azure"></a>Solución de problemas de implementación al crear una nueva máquina virtual Windows en Azure
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a>Principales problemas
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

Para consultar otros problemas de implementación de máquinas virtuales y preguntas, vea [Troubleshoot deploying Linux virtual machine issues in Azure](troubleshoot-deploy-vm.md) (Solución de problemas de implementación de máquinas virtuales de Windows en Azure).

## <a name="collect-activity-logs"></a>Recopilación de registros de actividad
Para iniciar la solución de problemas, recopile los registros de actividad para identificar el error asociado con el problema. Los vínculos siguientes contienen información detallada sobre el proceso que se debe seguir.

[Ver operaciones de implementación](../../azure-resource-manager/resource-manager-deployment-operations.md)

[Ver registros de actividad para administrar recursos de Azure](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-windows-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-windows-troubleshoot-deployment-new-vm-table.md)]

**Y:** si el sistema operativo es Windows generalizado y se carga o captura con la configuración generalizada, no habrá errores. De forma similar, si el sistema operativo es Windows especializado y se carga o captura con la configuración especializada, no habrá errores.

**Errores de carga:**

**N<sup>1</sup>:** si el sistema operativo es Windows generalizado y se carga como especializado, aparecerá un error de tiempo de espera de aprovisionamiento con la máquina virtual bloqueada en la pantalla de OOBE.

**N<sup>2</sup>:** si el sistema operativo es Windows especializado y se carga como generalizado, recibirá un error de aprovisionamiento con la máquina virtual bloqueada en la pantalla de OOBE porque la nueva máquina virtual se ejecuta con el nombre del equipo, el nombre de usuario y la contraseña originales.

**Resolución**

Para resolver estos errores, use [Add-AzureRmVhd para cargar el disco duro virtual original](https://msdn.microsoft.com/library/mt603554.aspx), disponible en el entorno local, con la misma configuración que para el sistema operativo (generalizada o especializada). Para cargar como generalizado, no olvide ejecutar sysprep antes.

**Errores de captura:**

**N<sup>3</sup>:** si el sistema operativo es Windows generalizado y se captura como especializado, recibirá un error de tiempo de espera de aprovisionamiento porque la máquina virtual original no se puede utilizar, ya que está marcada como generalizada.

**N<sup>4</sup>:** si el sistema operativo es Windows especializado y se captura como generalizado, recibirá un error de aprovisionamiento porque la nueva máquina virtual se está ejecutando con el nombre del equipo, el nombre de usuario y la contraseña originales. Además, no se puede utilizar la máquina virtual original ya que está marcada como especializada.

**Resolución**

Para resolver estos errores, elimine la imagen actual del portal y [vuelva a capturarla desde los discos duros virtuales actuales](create-vm-specialized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) con la misma configuración que para el sistema operativo (generalizada o especializada).

## <a name="issue-customgallerymarketplace-image-allocation-failure"></a>Problema: Imagen de galería/marketplace/personalizada; error de asignación
Este error se produce en situaciones en las que la nueva solicitud de máquina virtual está anclada en un clúster que no admite el tamaño de la máquina virtual que se solicita o no tiene espacio libre disponible para alojar la solicitud.

**Causa 1:** el clúster no admite el tamaño de la máquina virtual solicitada.

**Resolución 1:**

* Vuelva a intentar la solicitud con un tamaño de máquina virtual menor.
* Si no se puede cambiar el tamaño de la máquina virtual solicitada:
  * Detenga todas las máquinas virtuales en el conjunto de disponibilidad.
    Haga clic en **Grupos de recursos** > *su grupo de recursos* > **Recursos** > *su conjunto de disponibilidad* > **Virtual Machines** > *su máquina virtual* > **Detener**.
  * Después de detener todas las máquinas virtuales, cree la nueva máquina virtual con el tamaño deseado.
  * Inicie la nueva máquina virtual en primer lugar y luego seleccione cada una de las máquinas virtuales detenidas y haga clic en **Iniciar**.

**Causa 2:** el clúster no tiene recursos disponibles.

**Resolución 2:**

* Vuelva a intentar la solicitud más tarde.
* Si la nueva máquina virtual puede formar parte de un conjunto de disponibilidad diferente
  * Cree una nueva máquina virtual en un conjunto de disponibilidad diferente (en la misma región).
  * Agregue la nueva máquina virtual a la misma red virtual.

## <a name="next-steps"></a>Pasos siguientes
Si tiene problemas al iniciar una máquina virtual Windows detenida o al cambiar el tamaño de una máquina virtual Windows existente en Azure, consulte [Solución de problemas de la implementación de Resource Manager con el reinicio o el cambio de tamaño de una máquina virtual de Windows existente en Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

