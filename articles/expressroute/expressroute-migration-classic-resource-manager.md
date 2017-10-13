---
title: "Migración de las redes virtuales asociadas de ExpressRoute del modelo clásico a Azure Resource Manager: PowerShell | Microsoft Docs"
description: "En esta página se describe cómo migrar las redes virtuales asociadas a Resource Manager después de mover el circuito."
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
ms.openlocfilehash: 336f68308f7d4b4dd3c7476a4fabd793939e9e85
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/11/2017
---
# <a name="migrate-expressroute-associated-virtual-networks-from-classic-to-resource-manager"></a>Migración de las redes virtuales asociadas de ExpressRoute del portal clásico a Resource Manager

En este artículo se explica cómo migrar las redes virtuales asociadas de Azure ExpressRoute desde el modelo de implementación clásica al modelo de implementación de Azure Resource Manager después de mover el circuito de ExpressRoute. 


## <a name="before-you-begin"></a>Antes de empezar
* Compruebe que dispone de la versión más reciente de los módulos de Azure PowerShell. Para más información, vea [Instalación y configuración de Azure PowerShell](/powershell/azure/overview).
* Asegúrese de haber revisado los [requisitos previos](expressroute-prerequisites.md), los [requisitos de enrutamiento](expressroute-routing.md) y los [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.
* Revise la información que se proporciona en [Transición de un circuito ExpressRoute desde la implementación clásica a la implementación de Resource Manager](expressroute-move.md). Asegúrese de que comprende perfectamente los límites y restricciones.
* Compruebe que el circuito está totalmente operativo en el modelo de implementación clásica.
* Asegúrese de tener un grupo de recursos creado en el modelo de implementación de Resource Manager.
* Revise la siguiente documentación de migración de recursos:

    * [Migración compatible con la plataforma de recursos de IaaS del modelo clásico al de Azure Resource Manager](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
    * [Profundización técnica en la migración compatible con la plataforma de la implementación clásica a la de Azure Resource Manager](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
    * [FAQs: Platform-supported migration of IaaS resources from classic to Azure Resource Manager](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md) (Preguntas frecuentes: Migración compatible con la plataforma de recursos de IaaS desde el modelo de implementación clásica a Azure Resource Manager)
    * [Revisión de los errores y mitigaciones más comunes en la migración](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="supported-and-unsupported-scenarios"></a>Escenarios admitidos y no admitidos

* Un circuito ExpressRoute se puede mover desde el modelo de implementación clásica al entorno de Resource Manager sin tiempo de inactividad. Puede mover un circuito ExpressRoute del entorno clásico al entorno de Resource Manager sin tiempo de inactividad. Siga las instrucciones sobre [cómo mover circuitos ExpressRoute del modelo de implementación clásica a Resource Manager mediante PowerShell](expressroute-howto-move-arm.md). Este es un requisito previo para mover recursos conectados a la red virtual.
* Las redes virtuales, las puertas de enlace y las implementaciones asociadas dentro de la red virtual que están conectadas a un circuito ExpressRoute de la misma suscripción se pueden migrar al entorno de Resource Manager sin tiempo de inactividad. Puede seguir los pasos descritos más adelante para migrar recursos, como redes virtuales, puertas de enlace y máquinas virtuales implementadas dentro de la red virtual. Debe asegurarse de que las redes virtuales estén configuradas correctamente antes de la migración. 
* Las redes virtuales, las puertas de enlace y las implementaciones asociadas dentro de la red virtual que no estén en la misma suscripción que el circuito ExpressRoute requerirán algún tiempo de inactividad para completar la migración. En la última sección del documento se describen los pasos que se deben seguir para migrar los recursos.
* No se puede migrar una red virtual con la puerta de enlace de ExpressRoute y VPN Gateway.

## <a name="move-an-expressroute-circuit-from-classic-to-resource-manager"></a>Movimiento de un circuito ExpressRoute del modelo clásico a Resource Manager
Deberá mover un circuito ExpressRoute del entorno clásico a Resource Manager antes de intentar migrar los recursos que están conectados al circuito ExpressRoute. Para realizar esta tarea, consulte los siguientes artículos:

* Revise la información que se proporciona en [Transición de un circuito ExpressRoute desde la implementación clásica a la implementación de Resource Manager](expressroute-move.md).
* [Transición de los circuitos ExpressRoute desde el modelo de implementación clásica al modelo de implementación de Resource Manager mediante Azure PowerShell](expressroute-howto-move-arm.md).
* Use el portal de Azure Service Management. Puede seguir el flujo de trabajo para [crear un nuevo circuito ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) y seleccionar la opción de importación. 

Esta operación no requiere tiempo de inactividad. Puede continuar transfiriendo datos entre el entorno local y Microsoft mientras la migración está en curso.

## <a name="migrate-virtual-networks-gateways-and-associated-deployments"></a>Migración de redes virtuales, puertas de enlace e implementaciones asociadas

Los pasos que siga para migrar dependen de si los recursos están en la misma suscripción, en distintas suscripciones o en ambos casos.

### <a name="migrate-virtual-networks-gateways-and-associated-deployments-in-the-same-subscription-as-the-expressroute-circuit"></a>Migración de redes virtuales, puertas de enlace e implementaciones asociadas en la misma suscripción que el circuito ExpressRoute
En esta sección se describen los pasos que se deben seguir para migrar una red virtual, una puerta de enlace y las implementaciones asociadas en la misma suscripción que el circuito ExpressRoute. No hay tiempo de inactividad asociado a esta migración. Puede seguir usando todos los recursos a través del proceso de migración. El plano de administración se bloquea mientras la migración está en curso. 

1. Asegúrese de que el circuito ExpressRoute se ha movido del entorno clásico al entorno de Resource Manager.
2. Asegúrese de que la red virtual se ha preparado correctamente para la migración.
3. Registre la suscripción para la migración de recursos. Para registrar la suscripción para la migración de recursos, use el siguiente fragmento de código de PowerShell:

  ```powershell 
  Select-AzureRmSubscription -SubscriptionName <Your Subscription Name>
  Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  ```
4. Valide, prepare y migre. Para mover la red virtual, use el siguiente fragmento de código de PowerShell:

  ```powershell
  Move-AzureVirtualNetwork -Validate -VirtualNetworkName $vnetName
  Move-AzureVirtualNetwork -Prepare -VirtualNetworkName $vnetName
  Move-AzureVirtualNetwork -Commit -VirtualNetworkName $vnetName
  ```

  También puede cancelar la migración mediante la ejecución del siguiente cmdlet de PowerShell:

  ```powershell
  Move-AzureVirtualNetwork -Abort $vnetName
  ```

## <a name="next-steps"></a>Pasos siguientes
* [Migración compatible con la plataforma de recursos de IaaS del modelo clásico al de Azure Resource Manager](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
* [Profundización técnica en la migración compatible con la plataforma de la implementación clásica a la de Azure Resource Manager](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
* [FAQs: Platform-supported migration of IaaS resources from classic to Azure Resource Manager](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md) (Preguntas frecuentes: Migración compatible con la plataforma de recursos de IaaS desde el modelo de implementación clásica a Azure Resource Manager)
* [Revisión de los errores y mitigaciones más comunes en la migración](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
