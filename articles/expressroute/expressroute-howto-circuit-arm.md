---
title: "Creación y modificación de un circuito ExpressRoute mediante Powershell y Azure Resource Manager | Microsoft Docs"
description: "Este artículo describe cómo toocreate, aprovisionar, compruebe, actualizar, eliminar y cancelar el aprovisionamiento de un circuito de ExpressRoute."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f997182e-9b25-4a7a-b079-b004221dadcc
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 8d76c577a9cffdd393abac1b76cccc27d92e9e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell"></a>Creación y modificación de un circuito ExpressRoute mediante PowerShell
> [!div class="op_single_selector"]
> * [Portal de Azure](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [CLI de Azure](howto-circuit-cli.md)
> * [Vídeo: Azure Portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (clásico)](expressroute-howto-circuit-classic.md)
>

Este artículo describe cómo el circuito toocreate una ExpressRoute de Azure utilizando el modelo de implementación de Azure Resource Manager de hello y cmdlets de PowerShell. Este artículo también muestra cómo actualizarlo, estado de hello toocheck del circuito de hello, o eliminar y Cancelar.

## <a name="before-you-begin"></a>Antes de empezar
* Instalar versión más reciente de Hola de hello cmdlets de PowerShell del Administrador de recursos de Azure. Para obtener más información, consulte la [Overview of Azure PowerShell](/powershell/azure/overview) (Introducción a Azure PowerShell).
* Hola de revisión [requisitos previos](expressroute-prerequisites.md) y [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.


## <a name="create-and-provision-an-expressroute-circuit"></a>Creación y aprovisionamiento de un circuito ExpressRoute
### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a>1. Inicie sesión en tooyour cuenta de Azure y seleccione su suscripción
toobegin la configuración, el inicio de sesión tooyour cuenta de Azure. Usar hello después toohelp ejemplos que conectarse:

```powershell
Login-AzureRmAccount
```

Compruebe las suscripciones de hello para la cuenta de hello:

```powershell
Get-AzureRmSubscription
```

Seleccione la suscripción de Hola que desea toocreate una ExpressRoute de circuito para:

```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a>2. Obtener lista de Hola de proveedores compatibles, las ubicaciones y anchos de banda
Antes de crear un circuito ExpressRoute, necesita Hola lista de proveedores admitidos conectividad, ubicaciones y opciones de ancho de banda.

Hola cmdlet de PowerShell **AzureRmExpressRouteServiceProvider Get** devuelve esta información, que usará en pasos posteriores:

```powershell
Get-AzureRmExpressRouteServiceProvider
```

Compruebe toosee si aparece el proveedor de conectividad. Tome nota de hello siguiente información. La necesitará más adelante cuando cree un circuito.

* Nombre
* PeeringLocations
* BandwidthsOffered

Ahora está listo toocreate un circuito ExpressRoute.   

### <a name="3-create-an-expressroute-circuit"></a>3. Creación de un circuito ExpressRoute
Si todavía no tiene un grupo de recursos, debe crear uno antes de crear ExpressRoute. Puede hacerlo ejecutando el siguiente comando de hello:

```powershell
New-AzureRmResourceGroup -Name "ExpressRouteResourceGroup" -Location "West US"
```


Hola de ejemplo siguiente muestra cómo el circuito toocreate una ExpressRoute de 200 Mbps a través de Equinix en Silicon Valley. Si usa otro proveedor y otra configuración, sustituya esa información al realizar la solicitud. Hola te mostramos una solicitud de ejemplo para una nueva clave de servicio:

```powershell
New-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup" -Location "West US" -SkuTier Standard -SkuFamily MeteredData -ServiceProviderName "Equinix" -PeeringLocation "Silicon Valley" -BandwidthInMbps 200
```

Asegúrese de que se especifique nivel correcto de la SKU de Hola y familia de SKU:

* El nivel de SKU determina si está habilitado un complemento estándar o premium de ExpressRoute. Puede especificar *estándar* tooget Hola SKU estándar o *Premium* para el complemento de hello premium.
* Familia de SKU determina el tipo de facturación de Hola. Puede seleccionar *Metereddata* para el plan de datos limitado y *Unlimiteddata* para el plan de datos ilimitado. Se puede cambiar el tipo de facturación de Hola de *Metereddata* demasiado*Unlimiteddata*, pero no se puede cambiar tipo hello de *Unlimiteddata* demasiado*Metereddata* .

> [!IMPORTANT]
> El circuito de ExpressRoute se cobrará desde el momento de Hola que se emite una clave de servicio. Asegúrese de que lleva a cabo esta operación cuando proveedor de conectividad de hello circuito de hello tooprovision listo.
> 
> 

respuesta de Hello contiene la clave de servicio de Hola. Puede obtener una descripción detallada de todos los parámetros de hello ejecutando Hola siguiente comando:

```powershell
get-help New-AzureRmExpressRouteCircuit -detailed
```


### <a name="4-list-all-expressroute-circuits"></a>4. Lista de todos los circuitos ExpressRoute
tooget Hola de una lista de todos los circuitos ExpressRoute que ha creado, ejecute hello **Get AzureRmExpressRouteCircuit** comando:

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```

respuesta de Hello tendrá un aspecto similar toohello siguiente ejemplo:

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                          }
    CircuitProvisioningState          : Enabled
    ServiceProviderProvisioningState  : NotProvisioned
    ServiceProviderNotes              :
    ServiceProviderProperties         : {
                                          "ServiceProviderName": "Equinix",
                                          "PeeringLocation": "Silicon Valley",
                                          "BandwidthInMbps": 200
                                        }
    ServiceKey                        : **************************************
    Peerings                          : []

Puede recuperar esta información en cualquier momento mediante hello `Get-AzureRmExpressRouteCircuit` cmdlet. Realizar Hola llamada sin parámetros, enumera todos los circuitos de Hola. La clave del servicio se enumerarán en hello *ServiceKey* campo:

```powershell
Get-AzureRmExpressRouteCircuit
```


respuesta de Hello tendrá un aspecto similar toohello siguiente ejemplo:

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                          }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : NotProvisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


Puede obtener una descripción detallada de todos los parámetros de hello ejecutando Hola siguiente comando:

```powershell
get-help Get-AzureRmExpressRouteCircuit -detailed
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>5. Enviar el proveedor de conectividad de tooyour clave de servicio de hello para el aprovisionamiento
*ServiceProviderProvisioningState* proporciona información sobre el estado actual de Hola de aprovisionamiento en el lado del proveedor de servicios de Hola. Estado proporciona el estado de Hola en hello side de Microsoft. Para obtener más información acerca de los Estados de aprovisionamiento del circuito, vea hello [flujos de trabajo](expressroute-workflows.md#expressroute-circuit-provisioning-states) artículo.

Cuando se crea un nuevo circuito de ExpressRoute, circuito Hola estará en hello siguiente estado:

    ServiceProviderProvisioningState : NotProvisioned
    CircuitProvisioningState         : Enabled



circuito Hola cambiará toohello siguiente estado cuando el proveedor de conectividad de hello está en proceso de Hola de habilitarla para:

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

Para toobe pueda toouse un circuito ExpressRoute, debe estar en hello siguiente estado:

    ServiceProviderProvisioningState : Provisioned
    CircuitProvisioningState         : Enabled

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>6. Comprobar periódicamente el estado de Hola y el estado de Hola de clave de circuito de Hola
Comprobación de estado de Hola y el estado de Hola de clave de circuito de hello le permite saber si el proveedor ha habilitado el circuito. Una vez configurado el circuito de hello, *ServiceProviderProvisioningState* aparece como *aprovisionado*, tal y como se muestra en el siguiente ejemplo de Hola:

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


respuesta de Hello tendrá un aspecto similar toohello siguiente ejemplo:

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                       }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                       }
    ServiceKey                       : **************************************
    Peerings                         : []

### <a name="7-create-your-routing-configuration"></a>7. Creación de la configuración de enrutamiento
Para obtener instrucciones detalladas, consulte hello [circuito de ExpressRoute de configuración de enrutamiento](expressroute-howto-routing-arm.md) artículo toocreate y modificar los emparejamientos de circuito.

> [!IMPORTANT]
> Estas instrucciones aplican solo toocircuits que se crean con proveedores de servicios que ofrecen servicios de conectividad de 2 niveles. Si usa un proveedor de servicios que ofrece servicios administrados de nivel 3 (normalmente VPN IP, como MPLS), el mismo proveedor de conectividad configurará y administrará el enrutamiento.
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a>8. Vincular un circuito de ExpressRoute de tooan de red virtual
A continuación, vincular un circuito de ExpressRoute de tooyour de red virtual. Hola de uso [vinculación virtual redes tooExpressRoute circuitos](expressroute-howto-linkvnet-arm.md) artículo cuando se trabaja con el modelo de implementación del Administrador de recursos de Hola.

## <a name="getting-hello-status-of-an-expressroute-circuit"></a>Obtener el estado de saludo de un circuito ExpressRoute
Puede recuperar esta información en cualquier momento mediante hello **AzureRmExpressRouteCircuit Get** cmdlet. Realizar Hola llamada sin parámetros, enumera todos los circuitos de Hola.

```powershell
Get-AzureRmExpressRouteCircuit
```


respuesta de Hello será similar toohello siguiente ejemplo:

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                       }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                            "ServiceProviderName": "Equinix",
                                            "PeeringLocation": "Silicon Valley",
                                            "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


Puede obtener información sobre un circuito de ExpressRoute concreto pasando el nombre del grupo de recursos de Hola y el nombre de circuito como una llamada a toohello de parámetro:

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


respuesta de Hello tendrá un aspecto similar toohello siguiente ejemplo:

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                            "Tier": "Standard",
                                            "Family": "MeteredData"
                                          }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


Puede obtener una descripción detallada de todos los parámetros de hello ejecutando Hola siguiente comando:

```powershell
get-help get-azurededicatedcircuit -detailed
```

## <a name="modify"></a>Modificación de un circuito ExpressRoute
Puede modificar determinadas propiedades de un circuito ExpressRoute sin afectar a la conectividad.

Puede hacer Hola sigue sin tiempo de inactividad:

* Habilitar o deshabilitar el complemento ExpressRoute Premium en su circuito ExpressRoute.
* Ancho de banda de Hola de aumento de su circuito de ExpressRoute proporciona hay capacidad disponible en el puerto de Hola. No se admite la degradación de ancho de banda de Hola de un circuito. 
* Cambiar Hola plan desde tooUnlimited datos limitados de datos de disponibilidad. Cambiar Hola plan desde tooMetered ilimitados datos que no se admiten datos de disponibilidad.
* Puede habilitar y deshabilitar *Allow Classic Operations*(Permitir operaciones clásicas).

Para obtener más información sobre los límites y limitaciones, consulte toohello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md).

### <a name="tooenable-hello-expressroute-premium-add-on"></a>complemento de tooenable hello ExpressRoute premium
Puede habilitar complemento de hello ExpressRoute premium para el circuito existente mediante Hola siguiente fragmento de código de PowerShell:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Premium"
$ckt.sku.Name = "Premium_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

circuito Hola tendrán ahora hello ExpressRoute complemento las características premium habilitadas. Comenzaremos facturación para la capacidad de complemento de hello premium tan pronto como comando de Hola se ha ejecutado correctamente.

### <a name="toodisable-hello-expressroute-premium-add-on"></a>complemento de toodisable hello ExpressRoute premium
> [!IMPORTANT]
> Esta operación puede producir un error si usa recursos que son mayores que lo que está permitido para el circuito de hello estándar.
> 
> 

Tenga en cuenta los siguiente hello:

* Antes de degradar de toostandard premium, debe asegurarse de ese número de Hola de redes virtuales que están vinculadas toohello circuito es menor que 10. Si no lo hace, se producirá un error en la solicitud de actualización y se le facturará con las tarifas de nivel Premium.
* Tiene que desvincular todas las redes virtuales en otras regiones geopolíticas. Si no lo hace, se producirá un error en la solicitud de actualización y se le facturará con las tarifas de nivel Premium.
* La tabla de enrutamiento tiene que tener menos de 4.000 rutas para el emparejamiento entre pares privados. Si el tamaño de la tabla de ruta es mayor que 4000 rutas, sesión BGP de hello quita y no volver a habilitar hasta que el número de Hola de los prefijos anunciados esté por debajo de 4.000.

Puede deshabilitar el complemento de hello ExpressRoute premium para el circuito existente hello mediante Hola siguiente cmdlet de PowerShell:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Standard"
$ckt.sku.Name = "Standard_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a>ancho de banda de circuito de ExpressRoute de tooupdate Hola
Para ver opciones de ancho de banda admitido para el proveedor, compruebe hello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md). Puede elegir cualquier tamaño mayor que el tamaño de Hola de su circuito existente.

> [!IMPORTANT]
> Puede tener circuito de ExpressRoute de hello toorecreate si hay capacidad inadecuada en el puerto existente Hola. No puede actualizar el circuito de hello si no hay ninguna capacidad adicional disponible en esa ubicación.
>
> No se puede reducir el ancho de banda de Hola de un circuito de ExpressRoute sin interrupciones. Degradar de ancho de banda requiere circuito de ExpressRoute de toodeprovision hello y, a continuación, vuelva a aprovisionar un nuevo circuito de ExpressRoute.
> 

Después de decidir qué tamaño que sea necesario, utilice Hola después comando tooresize el circuito:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.ServiceProviderProperties.BandwidthInMbps = 1000

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```


El circuito se dimensionarán en lado de Microsoft de Hola. A continuación, debe ponerse en contacto con las configuraciones de tooupdate de proveedor de conectividad en su lado toomatch este cambio. Después de realizar esta notificación, empezaremos a facturación para la opción de ancho de banda de hello actualizado.

### <a name="toomove-hello-sku-from-metered-toounlimited"></a>Hola toomove SKU de uso medido toounlimited
Puede cambiar Hola SKU de un circuito ExpressRoute mediante Hola siguiente fragmento de código de PowerShell:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Family = "UnlimitedData"
$ckt.sku.Name = "Premium_UnlimitedData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a>clásico de toocontrol acceso toohello y entornos de administrador de recursos
Revisar las instrucciones de Hola de [circuitos ExpressRoute mover de modelo de implementación de administrador de recursos de hello toohello clásico](expressroute-howto-move-arm.md).  

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Desaprovisionamiento y eliminación de un circuito ExpressRoute
Tenga en cuenta los siguiente hello:

* Debe desvincular todas las redes virtuales de hello circuito de ExpressRoute. Si se produce un error en esta operación, compruebe toosee si las redes virtuales están vinculados toohello circuito.
* Si es el proveedor de servicios del circuito de ExpressRoute de hello estado de aprovisionamiento **Provisioning** o **aprovisionado** debe trabajar con el circuito de Hola de toodeprovision de proveedor de servicio en uno de su lados. Se continuará tooreserve recursos y facturar hasta que el proveedor de servicios de hello finaliza desaprovisionamiento circuito de Hola y notifica a nosotros.
* Si el proveedor de servicios de Hola se canceló el aprovisionamiento de circuito de hello (proveedor de servicios de hello estado de aprovisionamiento se establece demasiado**no aprovisionado**), a continuación, puede eliminar el circuito de Hola. Se detendrá la facturación para el circuito de Hola

Puede eliminar el circuito de ExpressRoute ejecutando Hola siguiente comando:

```powershell
Remove-AzureRmExpressRouteCircuit -ResourceGroupName "ExpressRouteResourceGroup" -Name "ExpressRouteARMCircuit"
```

## <a name="next-steps"></a>Pasos siguientes

Después de crear el circuito, asegúrese de que Hola siguientes:

* [Crear y modificar el enrutamiento para el circuito ExpressRoute](expressroute-howto-routing-arm.md)
* [Vincular el circuito de ExpressRoute de tooyour de red virtual](expressroute-howto-linkvnet-arm.md)
