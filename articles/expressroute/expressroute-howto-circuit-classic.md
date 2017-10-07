---
title: "Creación y modificación de un circuito ExpressRoute mediante Powershell y Azure clásico | Microsoft Docs"
description: "En este artículo le guiará por los pasos de Hola para crear y aprovisionar un circuito ExpressRoute. Este artículo también muestra cómo actualizar, estado de hello toocheck, o eliminar y desaprovisionar el circuito."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0134d242-6459-4dec-a2f1-4657c3bc8b23
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 9897c88776a2153ba22aa9ff328becb9f12b660b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell-classic"></a>Creación y modificación de un circuito ExpressRoute mediante PowerShell (clásica)
> [!div class="op_single_selector"]
> * [Portal de Azure](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [CLI de Azure](howto-circuit-cli.md)
> * [Vídeo: Azure Portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (clásico)](expressroute-howto-circuit-classic.md)
>

Este artículo le guiará a través de hello pasos toocreate un circuito ExpressRoute de Azure utilizando el modelo de implementación clásica de hello y cmdlets de PowerShell. Este artículo también muestra cómo actualizar, toocheck estado de hello, o eliminar y cancelar el aprovisionamiento de un circuito de ExpressRoute.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]


**Información sobre los modelos de implementación de Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-you-begin"></a>Antes de empezar
### <a name="step-1-review-hello-prerequisites-and-workflow-articles"></a>Paso 1. Revisar los requisitos previos de Hola y artículos de flujo de trabajo
Asegúrese de que ha revisado hello [requisitos previos](expressroute-prerequisites.md) y [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.  

### <a name="step-2-install-hello-latest-versions-of-hello-azure-service-management-sm-powershell-modules"></a>Paso 2: Instalar versiones más recientes de Hola de módulos de administración de servicio de Azure (SM) PowerShell Hola
Siga las instrucciones de hello en [Introducción a cmdlets de PowerShell de Azure](/powershell/azure/overview) para obtener instrucciones paso a paso acerca de cómo tooconfigure los módulos de PowerShell de Azure de equipo toouse Hola.

### <a name="step-3-log-in-tooyour-azure-account-and-select-a-subscription"></a>Paso 3: Inicie sesión en tooyour cuenta de Azure y seleccione una suscripción
1. Abra la consola de PowerShell con derechos elevados y conectar con tooyour cuenta. Usar hello después toohelp de ejemplo que se conecta:

        Login-AzureRmAccount

2. Compruebe las suscripciones de hello para la cuenta de hello.

        Get-AzureRmSubscription

3. Si tiene más de una suscripción, seleccione Hola suscripción que desea toouse.

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. A continuación, usar hello siguiente cmdlet tooadd su tooPowerShell de suscripción de Azure para el modelo de implementación clásica de Hola.

        Add-AzureAccount

## <a name="create-and-provision-an-expressroute-circuit"></a>Creación y aprovisionamiento de un circuito ExpressRoute
### <a name="step-1-import-hello-powershell-modules-for-expressroute"></a>Paso 1. Importar módulos de PowerShell de Hola para ExpressRoute
 Si no lo ha hecho ya, debe importar los módulos de Azure y ExpressRoute de hello en la sesión de PowerShell de hello en toostart orden mediante cmdlets de ExpressRoute Hola. Importar módulos de Hola de hello ubicación que se encontraban instalado tooon el equipo local. Según el método hello usa módulos de hello tooinstall, ubicación de hello puede ser diferente de hello siguiente ejemplo se muestra. Modificar el ejemplo de Hola si es necesario.  

    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'

### <a name="step-2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a>Paso 2: Obtener lista de Hola de proveedores compatibles, las ubicaciones y anchos de banda
Antes de crear un circuito ExpressRoute, necesita Hola lista de proveedores admitidos conectividad, ubicaciones y opciones de ancho de banda.

Hola cmdlet de PowerShell `Get-AzureDedicatedCircuitServiceProvider` devuelve esta información, que usará en pasos posteriores:

    Get-AzureDedicatedCircuitServiceProvider

Compruebe toosee si aparece el proveedor de conectividad. Tome nota de hello siguiente información porque lo necesitará más adelante cuando se crea un circuito:

* Nombre
* PeeringLocations
* BandwidthsOffered

Ahora está listo toocreate un circuito ExpressRoute.         

### <a name="step-3-create-an-expressroute-circuit"></a>Paso 3: Creación de un circuito ExpressRoute
Hola de ejemplo siguiente muestra cómo el circuito toocreate una ExpressRoute de 200 Mbps a través de Equinix en Silicon Valley. Si usa otro proveedor y otra configuración, sustituya esa información al realizar la solicitud.

> [!IMPORTANT]
> El circuito de ExpressRoute se cobrará desde el momento de Hola que se emite una clave de servicio. Asegúrese de que lleva a cabo esta operación cuando proveedor de conectividad de hello circuito de hello tooprovision listo.
> 
> 

Hola te mostramos una solicitud de ejemplo para una nueva clave de servicio:

    $Bandwidth = 200
    $CircuitName = "MyTestCircuit"
    $ServiceProvider = "Equinix"
    $Location = "Silicon Valley"

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Standard -BillingType MeteredData

O bien, si desea que toocreate un circuito de ExpressRoute con el complemento de hello premium, use Hola siguiente ejemplo. Consulte toohello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md) para obtener más información sobre el complemento de hello premium.

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Premium - BillingType MeteredData


respuesta de Hello contendrá la clave de servicio de Hola. Puede obtener una descripción detallada de todos los parámetros de hello ejecutando Hola siguiente:

    get-help new-azurededicatedcircuit -detailed

### <a name="step-4-list-all-hello-expressroute-circuits"></a>Paso 4 Lista de todos los circuitos ExpressRoute de Hola
Puede ejecutar hello `Get-AzureDedicatedCircuit` comando Hola de tooget una lista de todos los circuitos ExpressRoute que ha creado:

    Get-AzureDedicatedCircuit

respuesta de Hello será algo similar toohello siguiente ejemplo:

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

Puede recuperar esta información en cualquier momento mediante hello `Get-AzureDedicatedCircuit` cmdlet. Realizar Hola llamada sin ningún parámetro, enumera todos los circuitos de Hola. La clave del servicio se enumerarán en hello *ServiceKey* campo.

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

Puede obtener una descripción detallada de todos los parámetros de hello ejecutando Hola siguiente:

    get-help get-azurededicatedcircuit -detailed

### <a name="step-5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>Paso 5. Enviar el proveedor de conectividad de tooyour clave de servicio de hello para el aprovisionamiento
*ServiceProviderProvisioningState* proporciona información sobre el estado actual de Hola de aprovisionamiento en el lado del proveedor de servicios de Hola. *Estado* proporciona el estado de hello en hello side de Microsoft. Para obtener más información acerca de los Estados de aprovisionamiento del circuito, vea hello [flujos de trabajo](expressroute-workflows.md#expressroute-circuit-provisioning-states) artículo.

Cuando se crea un nuevo circuito de ExpressRoute, circuito Hola estará en hello siguiente estado:

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


circuito Hola irá toohello siguiente estado cuando el proveedor de conectividad de hello está en proceso de Hola de habilitarla para:

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

Un circuito ExpressRoute debe estar en hello después de estado para toobe pueda toouse lo:

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled


### <a name="step-6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>Paso 6. Comprobar periódicamente el estado de Hola y el estado de Hola de clave de circuito de Hola
Esto le permitirá saber cuándo ha habilitado el circuito el proveedor. Una vez configurado el circuito de hello, *ServiceProviderProvisioningState* se mostrará como *aprovisionado* tal y como se muestra en el siguiente ejemplo de Hola:

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

### <a name="step-7-create-your-routing-configuration"></a>Paso 7. Creación de la configuración de enrutamiento
Consulte toohello [circuito de ExpressRoute de configuración de enrutamiento (crear y modificar los emparejamientos de circuito)](expressroute-howto-routing-classic.md) artículo para obtener instrucciones paso a paso.

> [!IMPORTANT]
> Estas instrucciones aplican solo toocircuits que se crean con proveedores de servicios que ofrecen servicios de conectividad de 2 niveles. Si usa un proveedor de servicios que ofrece servicios administrados de nivel 3 (normalmente VPN IP, como MPLS), el mismo proveedor de conectividad configurará y administrará el enrutamiento.
> 
> 

### <a name="step-8-link-a-virtual-network-tooan-expressroute-circuit"></a>Paso 8. Vincular un circuito de ExpressRoute de tooan de red virtual
A continuación, vincular un circuito de ExpressRoute de tooyour de red virtual. Consulte demasiado[ExpressRoute vinculación circuitos toovirtual redes](expressroute-howto-linkvnet-classic.md) para obtener instrucciones paso a paso. Si necesita una red virtual con el modelo de implementación clásica de Hola para ExpressRoute toocreate, consulte [crear una red virtual para ExpressRoute](expressroute-howto-vnet-portal-classic.md).

## <a name="getting-hello-status-of-an-expressroute-circuit"></a>Obtener el estado de saludo de un circuito ExpressRoute
Puede recuperar esta información en cualquier momento mediante hello `Get-AzureCircuit` cmdlet. Realizar Hola llamada sin ningún parámetro, enumera todos los circuitos de Hola.

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

    Bandwidth                        : 1000
    CircuitName                      : MyAsiaCircuit
    Location                         : Singapore
    ServiceKey                       : #################################
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

Puede obtener información sobre un circuito de ExpressRoute concreto pasando la clave de servicio de hello como una llamada a toohello de parámetro.

    Get-AzureDedicatedCircuit -ServiceKey "*********************************"

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled


Puede obtener una descripción detallada de todos los parámetros de hello ejecutando el siguiente ejemplo de Hola:

    get-help get-azurededicatedcircuit -detailed

## <a name="modifying-an-expressroute-circuit"></a>Modificación de un circuito ExpressRoute
Puede modificar determinadas propiedades de un circuito ExpressRoute sin afectar a la conectividad.

Puede hacer Hola sigue sin tiempo de inactividad:

* Habilitar o deshabilitar el complemento ExpressRoute Premium en su circuito ExpressRoute.
* Ancho de banda de Hola de aumento de su circuito de ExpressRoute proporciona hay capacidad disponible en el puerto de Hola. Tenga en cuenta que no se admite la degradación de ancho de banda de Hola de un circuito. 
* Cambiar Hola plan desde tooUnlimited datos limitados de datos de disponibilidad. Tenga en cuenta ese plan de disponibilidad de hello cambiante de tooMetered datos ilimitados que datos no se admiten.
* Puede habilitar y deshabilitar *Allow Classic Operations*(Permitir operaciones clásicas).

Consulte toohello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md) para obtener más información sobre los límites y limitaciones.

### <a name="tooenable-hello-expressroute-premium-add-on"></a>complemento de tooenable hello ExpressRoute premium
Puede habilitar complemento de hello ExpressRoute premium para el circuito existente mediante Hola siguiente cmdlet de PowerShell:

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Premium

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Premium
    Status                           : Enabled

El circuito tendrán ahora hello ExpressRoute complemento las características premium habilitadas. Tenga en cuenta que se iniciará de facturación para la capacidad de complemento de hello premium tan pronto como comando de Hola se ha ejecutado correctamente.

### <a name="toodisable-hello-expressroute-premium-add-on"></a>complemento de toodisable hello ExpressRoute premium
> [!IMPORTANT]
> Esta operación puede producir un error si usa recursos que son mayores que lo que está permitido para el circuito de hello estándar.
> 
> 

#### <a name="considerations"></a>Consideraciones

* Debe asegurarse de que el número de Hola de redes virtuales vinculadas toohello circuito es menor que 10 antes de cambiar de premium toostandard. Si no lo hace, se producirá un error en la solicitud de actualización y le tarifas de facturación Hola.
* Tiene que desvincular todas las redes virtuales en otras regiones geopolíticas. Si no lo hace, se producirá un error en la solicitud de actualización y le tarifas de facturación Hola.
* La tabla de enrutamiento tiene que tener menos de 4.000 rutas para el emparejamiento entre pares privados. Si el tamaño de la tabla de ruta es mayor que 4000 rutas, sesión BGP Hola se quitará y no volver a habilitar hasta que el número de Hola de los prefijos anunciados esté por debajo de 4.000.

#### <a name="disable-hello-premium-add-on"></a>Deshabilitar complemento de hello premium
Puede deshabilitar complemento de hello ExpressRoute premium para el circuito existente mediante el uso de hello siguiente cmdlet de PowerShell:

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Standard

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled



### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a>ancho de banda de circuito de ExpressRoute de tooupdate Hola
Comprobar hello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md) para admite opciones de ancho de banda para el proveedor. Puede elegir cualquier tamaño que es mayor que el tamaño de Hola de su circuito existente como Hola puerto físico (en el que se creó el circuito) permite.

> [!IMPORTANT]
> Puede tener circuito de ExpressRoute de hello toorecreate si hay capacidad inadecuada en el puerto existente Hola. No puede actualizar el circuito de hello si no hay ninguna capacidad adicional disponible en esa ubicación.
>
> No se puede reducir el ancho de banda de Hola de un circuito de ExpressRoute sin interrupciones. Degradar de ancho de banda requiere circuito de ExpressRoute de toodeprovision hello y, a continuación, vuelva a aprovisionar un nuevo circuito de ExpressRoute.
> 
> 

#### <a name="resize-a-circuit"></a>Cambio del tamaño de un circuito

Después de decidir qué tamaño que sea necesario, puede usar Hola después comando tooresize el circuito:

    Set-AzureDedicatedCircuitProperties -ServiceKey ********************************* -Bandwidth 1000

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

El circuito ha habrá tamaño en lado de Microsoft de Hola. Debe ponerse en contacto con las configuraciones de tooupdate de proveedor de conectividad en su lado toomatch este cambio. Tenga en cuenta que se iniciará factura para hello actualiza la opción de ancho de banda desde este punto en.

Si ve Hola tras error al aumentar el ancho de banda de circuito de hello, significa que no hay queda no hay suficiente ancho de banda en el puerto físico Hola donde se crea el circuito existente. Toodelete este circuito y cree un nuevo circuito de tamaño Hola que sea necesario. 

    Set-AzureDedicatedCircuitProperties : InvalidOperation : Insufficient bandwidth available tooperform this circuit
    update operation
    At line:1 char:1
    + Set-AzureDedicatedCircuitProperties -ServiceKey ********************* ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Set-AzureDedicatedCircuitProperties], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.SetAzureDedicatedCircuitPropertiesCommand


## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Desaprovisionamiento y eliminación de un circuito ExpressRoute

### <a name="considerations"></a>Consideraciones

* Debe desvincular todas las redes virtuales de hello circuito de ExpressRoute para esta operación toosucceed. Comprobar toosee si dispone de las redes virtuales que están vinculados toohello circuito si se produce un error en esta operación.
* Si es el proveedor de servicios del circuito de ExpressRoute de hello estado de aprovisionamiento **Provisioning** o **aprovisionado** debe trabajar con el circuito de Hola de toodeprovision de proveedor de servicio en uno de su lados. Se continuará tooreserve recursos y facturar hasta que el proveedor de servicios de hello finaliza desaprovisionamiento circuito de Hola y notifica a nosotros.
* Si el proveedor de servicios de Hola se canceló el aprovisionamiento de circuito de hello (proveedor de servicios de hello estado de aprovisionamiento se establece demasiado**no aprovisionado**), a continuación, puede eliminar el circuito de Hola. Esto detendrá la facturación para el circuito de Hola.

#### <a name="delete-a-circuit"></a>Eliminación de un circuito

Puede eliminar el circuito de ExpressRoute ejecutando Hola siguiente comando:

    Remove-AzureDedicatedCircuit -ServiceKey "*********************************"



## <a name="next-steps"></a>Pasos siguientes
Después de crear el circuito, asegúrese de que Hola siguientes:

* [Crear y modificar el enrutamiento para el circuito ExpressRoute](expressroute-howto-routing-classic.md)
* [Vincular el circuito de ExpressRoute de tooyour de red virtual](expressroute-howto-linkvnet-classic.md)

