---
title: "aaaTroubleshoot clásico de implementación de VM de Linux | Documentos de Microsoft"
description: "Solución de problemas de implementación clásica al crear una nueva máquina virtual de Linux en Azure"
services: virtual-machines-linux
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: c8a963fa-6b2a-4c7a-a1f4-7793adb02b19
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: cjiang
ms.openlocfilehash: a642bfd9a543cd6d2104b03fe04193d9352ccae1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a>Solución de problemas de la implementación clásica con la creación de una máquina virtual de Linux en Azure
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-selectors](../../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-selectors-include.md)]

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

> [!IMPORTANT] 
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. Para la versión del Administrador de recursos de Hola de este artículo, consulte [aquí](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a>Recopilación de registros de auditoría
toostart solución de problemas, auditoría de hello recopilar registra el error de Hola de tooidentify asociada con el problema de Hola.

Hola portal de Azure, haga clic en **examinar** > **máquinas virtuales** > *la máquina virtual de Windows*  >   **Configuración de** > **registros de auditoría**.

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

**Y:** si Hola SO es Linux generalizado y se ha cargado ni capturado con hello generalizado configuración, no habrá errores. De forma similar, si Hola SO está especializado de Linux, y se ha cargado ni capturado con hello especializados configuración, a continuación, no habrá los errores.

**Errores de carga:**

**N<sup>1</sup>:** si Hola SO es Linux generalizado, y se carga como especializado, obtendrá un error de tiempo de espera de aprovisionamiento porque Hola VM está atascada en hello fase de aprovisionamiento.

**N<sup>2</sup>:** si hello SO es especializado de Linux y cargarlo como generalizado, obtendrá un error de aprovisionamiento porque hello nueva máquina virtual se está ejecutando con el nombre de equipo original de hello, username y password.

**Resolución:**

tooresolve ambos estos errores, cargar Hola VHD original, disponible en local, con Hola misma configuración que para hello OS (generalizado/especializado). tooupload como generalizado, recuerde toorun-desaprovisionar primero. Vea [crear y cargar un disco duro Virtual que Hola Contains sistema operativo Linux](create-upload-vhd.md) para obtener más información.

**Errores de captura:**

**N<sup>3</sup>:** si Hola SO es Linux generalizado, y se capturan como especializado, obtendrá un error de tiempo de espera de aprovisionamiento porque Hola original máquina virtual no se puede usar tal y como está marcado como generalizado.

**N<sup>4</sup>:** si hello SO es especializado de Linux, y se capturan como generalizado, obtendrá un error de aprovisionamiento porque hello nueva máquina virtual se está ejecutando con el nombre de equipo original de hello, username y password. Además, Hola original VM no es puede usar porque está marcado como especializadas.

**Resolución:**

tooresolve ambos estos errores, eliminar la imagen actual de Hola desde el portal de hello, y [capturar de hello VHD actual](capture-image.md) con Hola la misma configuración que para hello OS (generalizado/especializado).

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a>Problema: Imagen de galería/marketplace/personalizada; error de asignación
Este error se produce en situaciones cuando se envía una solicitud de máquina virtual nueva de hello tooa clúster que no tengan solicitud de hello tooaccommodate de espacio libre disponible, o no es compatible con el tamaño de la máquina virtual de Hola que se solicita. No es posible toomix distintas series de máquinas virtuales en hello mismo servicio en la nube. Por lo que si desea toocreate una nueva máquina virtual de un tamaño distinto de lo que puede admitir el servicio en la nube, solicitud de proceso de Hola se producirá un error.

Dependiendo de las restricciones de hello del servicio de nube de hello usar toocreate Hola nueva máquina virtual, podría encontrar un error provocado por una de dos situaciones.

**Causa 1:** servicio en la nube hello es tooa anclados específico, o en clúster es grupo de afinidad de tooan vinculado y por lo tanto, anclado tooa clúster concreto por cuestiones de diseño. Por lo que solicita el nuevo recurso de proceso en ese grupo de afinidad se prueban en hello mismo clúster donde se hospedan los recursos existentes de Hola. Sin embargo, hello mismo clúster puede no Hola de soporte técnico de tamaño de máquina virtual solicitado o tiene suficiente espacio disponible, lo que produce un error de asignación. Esto es cierto si Hola nuevos recursos se crean a través de un nuevo servicio de nube o un servicio de nube existente.

**Resolución 1:**

* Cree un nuevo servicio en la nube y asócielo a una región o a una red virtual basada en regiones.
* Crear una nueva máquina virtual en el servicio de nube nuevo Hola.
  Si se produce un error al tratar de toocreate un nuevo servicio de nube, vuelva a intentarlo más tarde o cambiar región Hola Hola servicio de nube.

> [!IMPORTANT]
> Si se tratara de toocreate una nueva máquina virtual en un servicio de nube existente pero no se pudo y tenía toocreate un nuevo servicio de nube para la nueva máquina virtual, puede elegir tooconsolidate todas las máquinas virtuales en hello mismo servicio en la nube. por lo tanto, toodo eliminar máquinas virtuales de Hola Hola existente del servicio en nube y capturarlos desde sus discos Hola nuevo servicio en nube. Sin embargo, es importante tooremember que el servicio de nube nuevo de Hola tendrá un nuevo nombre y la dirección VIP, por lo que deberá tooupdate para todas las dependencias de Hola que actualmente utilizan esta información para servicio de nube existente de Hola.
> 
> 

**Causa 2:** servicio de nube de hello está asociado a una red virtual que esté vinculado tooan grupo de afinidad, por lo que es tooa anclados clúster concreto por cuestiones de diseño. Todas las nuevas solicitudes de recursos de proceso en ese grupo de afinidad, por tanto, se prueban en hello mismo clúster donde se hospedan los recursos existentes de Hola. Sin embargo, hello mismo clúster puede no Hola de soporte técnico de tamaño de máquina virtual solicitado o tiene suficiente espacio disponible, lo que produce un error de asignación. Esto es cierto si Hola nuevos recursos se crean a través de un nuevo servicio de nube o un servicio de nube existente.

**Resolución 2:**

* Cree una nueva red virtual regional.
* Crear nueva máquina virtual en la nueva red virtual de Hola de Hola.
* [Conectar su red virtual existente](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/) toohello nueva red virtual. Consulte más información sobre las [redes virtuales regionales](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/). Como alternativa, puede [migrar la red virtual de red virtual basado en el grupo de afinidad tooa regional](https://azure.microsoft.com/blog/2014/11/26/migrating-existing-services-to-regional-scope/)y, a continuación, crear Hola nueva máquina virtual.

## <a name="next-steps"></a>Pasos siguientes
Si tiene problemas al iniciar una máquina virtual Linux detenida o al cambiar el tamaño de una máquina virtual Linux existente en Azure, consulte [Solución de problemas de la implementación clásica con el reinicio o el cambio de tamaño de una máquina virtual con Linux existente en Azure](restart-resize-error-troubleshooting.md).

