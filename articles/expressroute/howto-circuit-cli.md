---
title: "Creación y modificación de un circuito Azure ExpressRoute: CLI | Microsoft Docs"
description: "Este artículo describe cómo toocreate, aprovisionar, compruebe, actualizar, eliminar y cancelar el aprovisionamiento de un circuito de ExpressRoute con CLI."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: anzaman;cherylmc
ms.openlocfilehash: 396e325658a59afadb209bb525cbb59ac775ae6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-cli"></a>Creación y modificación de un circuito ExpressRoute mediante la CLI


Este artículo describe cómo toocreate un circuito de ExpressRoute de Azure mediante el uso de Hola interfaz de línea de comandos (CLI). Este artículo también muestra cómo actualizar, estado de hello toocheck, o elimine y cancelar el aprovisionamiento de un circuito. Si desea toouse una toowork otro método con circuitos ExpressRoute, puede seleccionar artículo Hola de hello lista siguiente:

> [!div class="op_single_selector"]
> * [Portal de Azure](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [CLI de Azure](howto-circuit-cli.md)
> * [Vídeo: Azure Portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (clásico)](expressroute-howto-circuit-classic.md)
> 

## <a name="before-you-begin"></a>Antes de empezar

* Antes de comenzar, instalar la versión más reciente de Hola de comandos de CLI de hello (2.0 o posteriores). Para obtener información acerca de cómo instalar los comandos de CLI de hello, consulte [instalar Azure CLI 2.0](/cli/azure/install-azure-cli) y [empezar a trabajar con Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).
* Hola de revisión [requisitos previos](expressroute-prerequisites.md) y [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.

## <a name="create-and-provision-an-expressroute-circuit"></a>Creación y aprovisionamiento de un circuito ExpressRoute

### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a>1. Inicie sesión en tooyour cuenta de Azure y seleccione su suscripción

toobegin la configuración, el inicio de sesión tooyour cuenta de Azure. Usar hello después toohelp ejemplos que conectarse:

```azurecli
az login
```

Compruebe las suscripciones de hello para la cuenta de hello.

```azurecli
az account list
```

Seleccione la suscripción de hello para el que desea toocreate un circuito ExpressRoute.

```azurecli
az account set --subscription "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a>2. Obtener lista de Hola de proveedores compatibles, las ubicaciones y anchos de banda

Antes de crear un circuito ExpressRoute, necesita Hola lista de proveedores admitidos conectividad, ubicaciones y opciones de ancho de banda. Hola CLI comando 'az red express route lista de proveedores de servicios' devuelve esta información, que usará en pasos posteriores:

```azurecli
az network express-route list-service-providers
```

respuesta de Hello es similar toohello siguiente ejemplo:

```azurecli
[
  {
    "bandwidthsOffered": [
      {
        "offerName": "50Mbps",
        "valueInMbps": 50
      },
      {
        "offerName": "100Mbps",
        "valueInMbps": 100
      },
      {
        "offerName": "200Mbps",
        "valueInMbps": 200
      },
      {
        "offerName": "500Mbps",
        "valueInMbps": 500
      },
      {
        "offerName": "1Gbps",
        "valueInMbps": 1000
      },
      {
        "offerName": "2Gbps",
        "valueInMbps": 2000
      },
      {
        "offerName": "5Gbps",
        "valueInMbps": 5000
      },
      {
        "offerName": "10Gbps",
        "valueInMbps": 10000
      }
    ],
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/expressRouteServiceProviders/",
    "location": null,
    "name": "AARNet",
    "peeringLocations": [
      "Melbourne",
      "Sydney"
    ],
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "tags": null,
    "type": "Microsoft.Network/expressRouteServiceProviders"
  },
```

Compruebe Hola respuesta toosee si aparece el proveedor de conectividad. Tome nota de hello después de obtener información, que tendrá cuando se crea un circuito:

* Nombre
* PeeringLocations
* BandwidthsOffered

Ahora está listo toocreate un circuito ExpressRoute.

### <a name="3-create-an-expressroute-circuit"></a>3. Creación de un circuito ExpressRoute

> [!IMPORTANT]
> El circuito de ExpressRoute se factura desde el momento de Hola que se emite una clave de servicio. Realizar esta operación cuando proveedor de conectividad de hello circuito de hello tooprovision listo.
> 
> 

Si todavía no tiene un grupo de recursos, debe crear uno antes de crear ExpressRoute. Puede crear un grupo de recursos mediante la ejecución de hello siguiente comando:

```azurecli
az group create -n ExpressRouteResourceGroup -l "West US"
```

Hola de ejemplo siguiente muestra cómo el circuito toocreate una ExpressRoute de 200 Mbps a través de Equinix en Silicon Valley. Si usa otro proveedor y otra configuración, sustituya esa información al realizar la solicitud. 

Asegúrese de que se especifique nivel correcto de la SKU de Hola y familia de SKU:

* El nivel de SKU determina si está habilitado un complemento estándar o premium de ExpressRoute. Puede especificar 'Estándar' hello tooget SKU estándar o 'Premium' para el complemento de hello premium.
* Familia de SKU determina el tipo de facturación de Hola. Puede seleccionar "Metereddata" para el plan de datos limitado y "Unlimiteddata" para el plan de datos ilimitado. Puede cambiar el tipo de facturación de Hola de ' Metereddata 'too'Unlimiteddata', pero no puede cambiar tipo hello de 'Unlimiteddata' too'Metereddata'.


El circuito de ExpressRoute se factura desde el momento de Hola que se emite una clave de servicio. Hola siguiente ejemplo es una solicitud de una nueva clave de servicio:

```azurecli
az network express-route create --bandwidth 200 -n MyCircuit --peering-location "Silicon Valley" -g ExpressRouteResourceGroup --provider "Equinix" -l "West US" --sku-family MeteredData --sku-tier Standard
```

respuesta de Hello contiene la clave de servicio de Hola.

### <a name="4-list-all-expressroute-circuits"></a>4. Lista de todos los circuitos ExpressRoute

tooget una lista de todos los circuitos ExpressRoute de Hola que ha creado, ejecute 'hello az red express route mostrar' (comando). Puede recuperar esta información en cualquier momento con este comando. toolist todos los circuitos, realizar Hola llamada sin parámetros.

```azurecli
az network express-route list
```

La clave del servicio aparece en hello *ServiceKey* campo de respuesta de Hola.

```azurecli
"allowClassicOperations": false,
"authorizations": [],
"circuitProvisioningState": "Enabled",
"etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
"gatewayManagerEtag": null,
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
"location": "westus",
"name": "MyCircuit",
"peerings": [],
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup",
"serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
"serviceProviderNotes": null,
"serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
},
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

Puede obtener una descripción detallada de todos los parámetros de hello ejecutando el comando hello mediante hello '-h' parámetro.

```azurecli
az network express-route list -h
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>5. Enviar el proveedor de conectividad de tooyour clave de servicio de hello para el aprovisionamiento

'ServiceProviderProvisioningState' proporciona información sobre el estado actual de Hola de aprovisionamiento en el lado del proveedor de servicios de Hola. estado de Hello proporciona estado hello en hello side de Microsoft. Para obtener más información, vea hello [artículo de flujos de trabajo](expressroute-workflows.md#expressroute-circuit-provisioning-states).

Cuando se crea un nuevo circuito de ExpressRoute, circuito hello es Hola siguiente estado:

```azurecli
"serviceProviderProvisioningState": "NotProvisioned"
"circuitProvisioningState": "Enabled"
```

Hola circuito cambios toohello siguiente estado cuando el proveedor de conectividad de hello está en proceso de Hola de habilitarla para:

```azurecli
"serviceProviderProvisioningState": "Provisioning"
"circuitProvisioningState": "Enabled"
```

Para toobe pueda toouse un circuito ExpressRoute, debe estar en hello siguiente estado:

```azurecli
"serviceProviderProvisioningState": "Provisioned"
"circuitProvisioningState": "Enabled
```

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>6. Comprobar periódicamente el estado de Hola y el estado de Hola de clave de circuito de Hola

Comprobación de estado de Hola y el estado de Hola de clave de circuito de hello le permite saber si el proveedor ha habilitado el circuito. Una vez configurado el circuito de hello, 'ServiceProviderProvisioningState' aparece como "Aprovisionado", como se muestra en el siguiente ejemplo de Hola:

```azurecli
az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
```

respuesta de Hello es similar toohello siguiente ejemplo:

```azurecli
"allowClassicOperations": false,
"authorizations": [],
"circuitProvisioningState": "Enabled",
"etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
"gatewayManagerEtag": null,
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
"location": "westus",
"name": "MyCircuit",
"peerings": [],
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup",
"serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
"serviceProviderNotes": null,
"serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
},
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

### <a name="7-create-your-routing-configuration"></a>7. Creación de la configuración de enrutamiento

Para obtener instrucciones detalladas, consulte hello [circuito de ExpressRoute de configuración de enrutamiento](howto-routing-cli.md) artículo toocreate y modificar los emparejamientos de circuito.

> [!IMPORTANT]
> Estas instrucciones aplican solo toocircuits que se crean con proveedores de servicios que ofrecen servicios de conectividad de 2 niveles. Si usa un proveedor de servicios que ofrece servicios administrados de nivel 3 (normalmente VPN IP, como MPLS), el mismo proveedor de conectividad configura y administra el enrutamiento.
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a>8. Vincular un circuito de ExpressRoute de tooan de red virtual

A continuación, vincular un circuito de ExpressRoute de tooyour de red virtual. Hola de uso [vinculación virtual redes tooExpressRoute circuitos](howto-linkvnet-cli.md) artículo.

## <a name="modify"></a>Modificación de un circuito ExpressRoute

Puede modificar determinadas propiedades de un circuito ExpressRoute sin afectar a la conectividad. Puede realizar Hola después cambios sin tiempo de inactividad:

* Puede habilitar o deshabilitar el complemento ExpressRoute Premium en su circuito ExpressRoute.
* Puede aumentar el ancho de banda de Hola del circuito de ExpressRoute siempre hay capacidad disponible en el puerto de Hola. Sin embargo, no se admite la degradación de ancho de banda de Hola de un circuito. 
* Puede cambiar el plan de disponibilidad de Hola de tooUnlimited datos limitados de datos. Sin embargo, cambiar Hola plan desde tooMetered ilimitados datos que no se admiten datos de disponibilidad.
* Puede habilitar y deshabilitar *Allow Classic Operations*(Permitir operaciones clásicas).

Para obtener más información sobre los límites y limitaciones, vea hello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md).

### <a name="tooenable-hello-expressroute-premium-add-on"></a>complemento de tooenable hello ExpressRoute premium

Puede habilitar complemento de hello ExpressRoute premium para el circuito existente mediante Hola siguiente comando:

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Premium
```

circuito de Hello tiene ahora hello ExpressRoute complemento las características premium habilitadas. Empezaremos facturación para la capacidad de complemento de hello premium tan pronto como comando de Hola se ha ejecutado correctamente.

### <a name="toodisable-hello-expressroute-premium-add-on"></a>complemento de toodisable hello ExpressRoute premium

> [!IMPORTANT]
> Esta operación puede producir un error si usa recursos que son mayores que lo que está permitido para el circuito de hello estándar.
> 
> 

Antes de deshabilitar el complemento de hello ExpressRoute premium, comprender Hola siguiendo criterios:

* Antes de degradar de toostandard premium, debe asegurarse de que dispone de menos de 10 redes virtuales vinculadas toohello circuito. Si tiene más de diez, se produce una solicitud de actualización y se le factura con las tarifas de nivel Premium.
* Tiene que desvincular todas las redes virtuales en otras regiones geopolíticas. Si no lo hace, se produce un error en la solicitud de actualización y se le factura con las tarifas de nivel Premium.
* La tabla de enrutamiento tiene que tener menos de 4.000 rutas para el emparejamiento entre pares privados. Si el tamaño de la tabla de ruta es mayor que 4000 rutas, quita la sesión BGP Hola. No volver a habilitar la sesión de Hello hasta que el número de Hola de los prefijos anunciados es inferior a 4.000.

Puede deshabilitar el complemento de premium de ExpressRoute de hello para el circuito de hello existente utilizando el siguiente ejemplo de Hola:

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Standard
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a>ancho de banda de circuito de ExpressRoute de tooupdate Hola

Para hello admitida opciones de ancho de banda para el proveedor, consulte hello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md). Puede elegir cualquier tamaño mayor que el tamaño de Hola de su circuito existente.

> [!IMPORTANT]
> Si no hay capacidad inadecuada en el puerto existente de hello, habrá circuito de ExpressRoute de toorecreate Hola. No puede actualizar el circuito de hello si no hay ninguna capacidad adicional disponible en esa ubicación.
>
> No se puede reducir el ancho de banda de Hola de un circuito de ExpressRoute sin interrupciones. Degradar de ancho de banda requiere toodeprovision Hola circuito ExpressRoute y, a continuación, vuelva a aprovisionar un nuevo circuito de ExpressRoute.
>

Una vez decidido el tamaño de Hola que sea necesario, utilice Hola después comando tooresize el circuito:

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --bandwidth 1000
```

El circuito tiene un tamaño lado de Microsoft de Hola. A continuación, debe ponerse en contacto con las configuraciones de tooupdate de proveedor de conectividad en su lado toomatch este cambio. Después de realizar esta notificación, empezaremos facturación para la opción de ancho de banda de hello actualizado.

### <a name="toomove-hello-sku-from-metered-toounlimited"></a>Hola toomove SKU de uso medido toounlimited

Puede cambiar Hola SKU de un circuito ExpressRoute mediante el siguiente ejemplo de Hola:

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-family UnlimitedData
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a>clásico de toocontrol acceso toohello y entornos de administrador de recursos

Revisar las instrucciones de Hola de [circuitos ExpressRoute mover de modelo de implementación de administrador de recursos de hello toohello clásico](expressroute-howto-move-arm.md).

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Desaprovisionamiento y eliminación de un circuito ExpressRoute

toodeprovision y eliminar un circuito ExpressRoute, asegúrese de comprender Hola siguiendo criterios:

* Debe desvincular todas las redes virtuales de hello circuito de ExpressRoute. Si se produce un error en esta operación, compruebe toosee si las redes virtuales están vinculados toohello circuito.
* Si es el proveedor de servicios del circuito de ExpressRoute de hello estado de aprovisionamiento **Provisioning** o **aprovisionado**, debe trabajar con el circuito de Hola de toodeprovision de proveedor de servicio en uno de su lados. Hemos continuar tooreserve recursos y facturar hasta que el proveedor de servicios de hello finaliza desaprovisionamiento circuito de Hola y notifica a nosotros.
* Puede eliminar el circuito de hello si el proveedor de servicios de Hola se canceló el aprovisionamiento de circuito de Hola. Cuando se desaprovisiona un circuito, estado de aprovisionamiento de proveedor de servicios de Hola se establece demasiado**no aprovisionado**. Esto deja de facturación para el circuito de Hola.

Puede eliminar el circuito de ExpressRoute ejecutando Hola siguiente comando:

```azurecli
az network express-route delete  -n MyCircuit -g ExpressRouteResourceGroup
```

## <a name="next-steps"></a>Pasos siguientes

Después de crear el circuito, asegúrese de que hello las siguientes tareas:

* [Crear y modificar el enrutamiento para el circuito ExpressRoute](howto-routing-cli.md)
* [Vincular el circuito de ExpressRoute de tooyour de red virtual](howto-linkvnet-cli.md)
