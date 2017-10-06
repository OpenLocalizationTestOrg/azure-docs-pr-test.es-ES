---
title: "Mover los circuitos ExpressRoute de tooResource clásico Manager: PowerShell: Azure | Documentos de Microsoft"
description: "Esta página describe cómo toomove una toohello de circuito clásico implementación del Administrador de recursos del modelo mediante PowerShell."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 08152836-23e7-42d1-9a56-8306b341cd91
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/03/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 8dcadafca5e4f40773902cec5786eba1dbe133eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-expressroute-circuits-from-hello-classic-toohello-resource-manager-deployment-model-using-powershell"></a>Mover los circuitos ExpressRoute de modelo de implementación de administrador de recursos hello toohello clásico con PowerShell

toouse un circuito de ExpressRoute para hello clásico y modelos de implementación del Administrador de recursos, debe mover el modelo de implementación de hello circuito toohello el Administrador de recursos. Hello las secciones siguientes se ayuda a adoptar el circuito usando PowerShell.

## <a name="before-you-begin"></a>Antes de empezar

* Compruebe que tiene la versión más reciente de Hola de módulos de PowerShell de Azure de hello (al menos la versión 1.0). Para obtener más información, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).
* Asegúrese de que ha revisado hello [requisitos previos](expressroute-prerequisites.md), [requisitos de enrutamiento](expressroute-routing.md), y [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.
* Revise la información de Hola que se proporciona en [mover un circuito de ExpressRoute de tooResource clásico Manager](expressroute-move.md). Asegúrese de que entiende totalmente Hola límites y limitaciones.
* Compruebe que el circuito de hello es totalmente operativo en el modelo de implementación clásica de Hola.
* Asegúrese de que tiene un grupo de recursos que se creó en el modelo de implementación del Administrador de recursos de Hola.

## <a name="move-an-expressroute-circuit"></a>Movimiento de un circuito ExpressRoute

### <a name="step-1-gather-circuit-details-from-hello-classic-deployment-model"></a>Paso 1: Recopilar detalles del circuito de modelo de implementación clásica de Hola

Inicie sesión en toohello el entorno clásico de Azure y obtener la clave de servicio de Hola.

1. Inicie sesión en tooyour cuenta de Azure.

  ```powershell
  Add-AzureAccount
  ```

2. Seleccione la suscripción a Azure apropiada Hola.

  ```powershell
  Select-AzureSubscription "<Enter Subscription Name here>"
  ```

3. Importar módulos de PowerShell de Hola de Azure y ExpressRoute.

  ```powershell
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
  ```

4. Usa el cmdlet Hola de claves para el servicio hello tooget para todos los circuitos ExpressRoute. Después de recuperar las claves de hello, copie hello **clave de servicio** de circuito de Hola que desea que el modelo de implementación de toomove toohello el Administrador de recursos.

  ```powershell
  Get-AzureDedicatedCircuit
  ```

### <a name="step-2-sign-in-and-create-a-resource-group"></a>Paso 2: Inicio de sesión y creación de un grupo de recursos

Inicie sesión en el entorno de administrador de recursos de toohello y crear un nuevo grupo de recursos.

1. Inicie sesión en el entorno de Azure Resource Manager tooyour.

  ```powershell
  Login-AzureRmAccount
  ```

2. Seleccione la suscripción a Azure apropiada Hola.

  ```powershell
  Get-AzureRmSubscription -SubscriptionName "<Enter Subscription Name here>" | Select-AzureRmSubscription
  ```

3. Modificar fragmento de código de hello debajo toocreate un nuevo grupo de recursos si aún no tiene un grupo de recursos.

  ```powershell
  New-AzureRmResourceGroup -Name "DemoRG" -Location "West US"
  ```

### <a name="step-3-move-hello-expressroute-circuit-toohello-resource-manager-deployment-model"></a>Paso 3: Mover el modelo de implementación de administrador de recursos de toohello circuito de ExpressRoute de Hola

Se está ahora listo toomove el circuito de ExpressRoute de modelo de implementación de administrador de recursos de toohello modelo de implementación clásica de Hola. Antes de continuar, revise la información Hola proporcionada en [mover un circuito ExpressRoute de modelo de implementación de administrador de recursos de hello toohello clásico](expressroute-move.md).

toomove el circuito, modifique y ejecute hello siguiente fragmento de código:

```powershell
Move-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "DemoRG" -Location "West US" -ServiceKey "<Service-key>"
```

> [!NOTE]
> Cuando haya finalizado el movimiento de hello, nombre nuevo de Hola que aparece en el cmdlet anterior Hola será usado tooaddress Hola recursos. Básicamente se cambiará el circuito de Hola.
> 

## <a name="modify-circuit-access"></a>Modificación del acceso al circuito

### <a name="tooenable-expressroute-circuit-access-for-both-deployment-models"></a>tooenable acceso de circuito de ExpressRoute para ambos modelos de implementación

Después de mover el modelo de implementación en el Administrador de recursos de clásico ExpressRoute circuito toohello, puede habilitar los modelos de implementación de acceso tooboth. Ejecute hello después de modelos de implementación de cmdlets tooenable acceso tooboth:

1. Obtener detalles del circuito Hola.

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. Establecer tooTRUE "Permitir operaciones clásico".

  ```powershell
  $ckt.AllowClassicOperations = $true
  ```

3. Actualizar circuito Hola. Cuando esta operación ha finalizado correctamente, será capaz de tooview circuito de hello en el modelo de implementación clásica de Hola.

  ```powershell
  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

4. Ejecute hello cmdlet tooget Hola detalla de hello circuito de ExpressRoute. Debe ser toosee capaz de clave del servicio Hola enumerado.

  ```powershell
  get-azurededicatedcircuit
  ```

5. Ahora puede administrar el circuito de ExpressRoute de toohello vínculos mediante comandos de modelo de implementación clásica de Hola para redes virtuales clásicas y comandos del Administrador de recursos de hello para el Administrador de recursos VNets. Hello artículos siguientes ayudarán a administrar vínculos toohello circuito de ExpressRoute:

    * [Vincular el circuito de ExpressRoute en el modelo de implementación del Administrador de recursos de hello tooyour de red virtual](expressroute-howto-linkvnet-arm.md)
    * [Vincular el circuito de ExpressRoute en el modelo de implementación clásica de hello tooyour de red virtual](expressroute-howto-linkvnet-classic.md)

### <a name="toodisable-expressroute-circuit-access-toohello-classic-deployment-model"></a>modelo de implementación clásica de toohello de acceso circuito de ExpressRoute de toodisable

Ejecute hello siguiendo el modelo de implementación clásica de cmdlets toodisable acceso toohello.

1. Obtener detalles de hello circuito de ExpressRoute.

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. Establecer tooFALSE "Permitir operaciones clásico".

  ```powershell
  $ckt.AllowClassicOperations = $false
  ```

3. Actualizar circuito Hola. Después de esta operación ha finalizado correctamente, no será capaz de tooview circuito de hello en el modelo de implementación clásica de Hola.

  ```powershell
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

## <a name="next-steps"></a>Pasos siguientes

* [Crear y modificar el enrutamiento para el circuito ExpressRoute](expressroute-howto-routing-arm.md)
* [Vincular el circuito de ExpressRoute de tooyour de red virtual](expressroute-howto-linkvnet-arm.md)
