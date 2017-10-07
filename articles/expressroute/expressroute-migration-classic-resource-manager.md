---
title: "Migrar las redes virtuales asociado de ExpressRoute de tooResource clásico Manager: Azure: PowerShell | Documentos de Microsoft"
description: "Esta página describe cómo toomigrate había asociado redes virtuales tooResource Manager después de mover el circuito."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: e64506c6909296f98c5dd23b1437bc0b81f31c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-expressroute-associated-virtual-networks-from-classic-tooresource-manager"></a>Migrar las redes virtuales asociado de ExpressRoute de tooResource clásico Manager

Este artículo explica cómo toomigrate ExpressRoute de Azure había asociado redes virtuales de modelo de implementación de Azure Resource Manager de toohello modelo de implementación clásica de hello después de mover el circuito de ExpressRoute. 


## <a name="before-you-begin"></a>Antes de empezar
* Compruebe que dispone de versión más reciente de Hola de módulos de PowerShell de Azure de Hola. Para obtener más información, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).
* Asegúrese de que ha revisado hello [requisitos previos](expressroute-prerequisites.md), [requisitos de enrutamiento](expressroute-routing.md), y [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.
* Revise la información de Hola que se proporciona en [mover un circuito de ExpressRoute de tooResource clásico Manager](expressroute-move.md). Asegúrese de que entiende totalmente Hola límites y limitaciones.
* Compruebe que el circuito de hello es totalmente operativo en el modelo de implementación clásica de Hola.
* Asegúrese de que tiene un grupo de recursos que se creó en el modelo de implementación del Administrador de recursos de Hola.
* Revisar Hola siguiendo documentación de migración del recurso:

    * [Migración admitida por la plataforma de recursos de IaaS de tooAzure clásico Administrador de recursos](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
    * [Técnica de fondo admitida por la plataforma de migración de clásico tooAzure el Administrador de recursos](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
    * [Preguntas más frecuentes: Admitida por la plataforma de migración de los recursos de IaaS de tooAzure clásico Administrador de recursos](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
    * [Revisión de los errores y mitigaciones más comunes en la migración](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="supported-and-unsupported-scenarios"></a>Escenarios admitidos y no admitidos

* Un circuito ExpressRoute puede mover desde el entorno de administrador de recursos de hello toohello clásico sin tiempo de inactividad. Puede mover cualquier circuito de ExpressRoute de hello clásico toohello entorno de administrador de recursos sin tiempo de inactividad. Siga las instrucciones de hello en [mover circuitos ExpressRoute de modelo de implementación de administrador de recursos hello toohello clásico mediante PowerShell](expressroute-howto-move-arm.md). Se trata de una red virtual de requisitos previos toomove recursos toohello conectado.
* Redes virtuales, puertas de enlace y las implementaciones asociadas dentro de la red virtual de Hola que están conectado tooan circuito de ExpressRoute en hello puede ser la misma suscripción migran toohello entorno de administrador de recursos sin tiempo de inactividad. Puede seguir Hola pasos se describe más adelante toomigrate recursos tales como redes virtuales, las puertas de enlace y máquinas virtuales implementadas dentro de la red virtual de Hola. Debe asegurarse de que las redes virtuales Hola estén configuradas correctamente antes de su migración. 
* Redes virtuales, las puertas de enlace e implementaciones asociadas dentro de la red virtual de Hola que no están en Hola misma suscripción como Hola circuito ExpressRoute requieren algunos migración de hello toocomplete de tiempo de inactividad. Hola última sección de hello documento describe Hola pasos toobe seguido toomigrate recursos.
* No se puede migrar una red virtual con la puerta de enlace de ExpressRoute y VPN Gateway.

## <a name="move-an-expressroute-circuit-from-classic-tooresource-manager"></a>Mover un circuito de ExpressRoute de tooResource clásico Manager
Debe mover un circuito de ExpressRoute de hello clásico toohello entorno de administrador de recursos antes de intentar toomigrate recursos que están conectados toohello circuito de ExpressRoute. tooaccomplish esta tarea, vea Hola siguientes artículos:

* Revise la información de Hola que se proporciona en [mover un circuito de ExpressRoute de tooResource clásico Manager](expressroute-move.md).
* [Mover un circuito de tooResource clásico administrador mediante Azure PowerShell](expressroute-howto-move-arm.md).
* Usar el portal de administración de servicios de Azure de Hola. Puede seguir el flujo de trabajo de hello demasiado[crear un nuevo circuito de ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) y seleccione la opción de importación de Hola. 

Esta operación no requiere tiempo de inactividad. Puede continuar tootransfer datos entre las instalaciones locales y Microsoft mientras la migración de hello está en curso.

## <a name="migrate-virtual-networks-gateways-and-associated-deployments"></a>Migración de redes virtuales, puertas de enlace e implementaciones asociadas

Hello pasos que seguir toomigrate dependen de si los recursos están en hello misma suscripción, distintas suscripciones o ambos.

### <a name="migrate-virtual-networks-gateways-and-associated-deployments-in-hello-same-subscription-as-hello-expressroute-circuit"></a>Migrar las redes virtuales, las puertas de enlace, y las implementaciones asociadas en Hola misma suscripción como Hola circuito de ExpressRoute
Esta sección describen Hola pasos toobe seguido toomigrate una red virtual, puerta de enlace y las implementaciones asociadas en Hola misma suscripción como Hola circuito de ExpressRoute. No hay tiempo de inactividad asociado a esta migración. Puede continuar toouse todos los recursos a través del proceso de migración de Hola. plano de administración de Hola se bloquea mientras la migración de hello está en curso. 

1. Asegúrese de que se ha movido el circuito de ExpressRoute de hello del entorno de administrador de recursos de hello toohello clásico.
2. Asegúrese de que red virtual Hola se preparó correctamente para la migración de Hola.
3. Registre la suscripción para la migración de recursos. tooregister su suscripción para la migración de recursos, Hola de uso siguiente fragmento de código de PowerShell:

  ```powershell 
  Select-AzureRmSubscription -SubscriptionName <Your Subscription Name>
  Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  ```
4. Valide, prepare y migre. toomove Hola red virtual, Hola de uso siguiente fragmento de código de PowerShell:

  ```powershell
  Move-AzureVirtualNetwork -Prepare $vnetName  
  Move-AzureVirtualNetwork -Commit $vnetName
  ```

  También puede anular la migración mediante la ejecución de hello siguiente cmdlet de PowerShell:

  ```powershell
  Move-AzureVirtualNetwork -Abort $vnetName
  ```

## <a name="next-steps"></a>Pasos siguientes
* [Migración admitida por la plataforma de recursos de IaaS de tooAzure clásico Administrador de recursos](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
* [Técnica de fondo admitida por la plataforma de migración de clásico tooAzure el Administrador de recursos](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
* [Preguntas más frecuentes: Admitida por la plataforma de migración de los recursos de IaaS de tooAzure clásico Administrador de recursos](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
* [Revisión de los errores y mitigaciones más comunes en la migración](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
