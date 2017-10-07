---
title: "¿Cómo tooconfigure enrutamiento por un circuito ExpressRoute de Azure: CLI | Documentos de Microsoft"
description: "En este artículo le ayuda a crear y aprovisionar Hola privado, público y emparejamiento de Microsoft de un circuito de ExpressRoute. Este artículo también muestra cómo toocheck estado de hello, actualizar o eliminar emparejamientos para el circuito."
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
ms.date: 07/31/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 33130af050045527cdb316e77821c6d101b6a82a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-routing-for-an-expressroute-circuit-using-cli"></a>Creación y modificación del enrutamiento de un circuito ExpressRoute mediante la CLI

En este artículo le ayuda a crear y administrar la configuración de enrutamiento para un circuito ExpressRoute en modelo de implementación del Administrador de recursos Hola con CLI. También puede comprobar el estado de hello, update o delete y desaprovisionar los emparejamientos de un circuito de ExpressRoute. Si desea toouse una toowork otro método con el circuito, seleccione un artículo de hello lista siguiente:

> [!div class="op_single_selector"]
> * [Portal de Azure](expressroute-howto-routing-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-routing-arm.md)
> * [CLI de Azure](howto-routing-cli.md)
> * [Vídeo: pares privados](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [Vídeo: pares públicos](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [Vídeo: emparejamiento de Microsoft](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [PowerShell (clásico)](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a>Requisitos previos de configuración

* Antes de comenzar, instalar la versión más reciente de Hola de comandos de CLI de hello (2.0 o posteriores). Para obtener información acerca de cómo instalar los comandos de CLI de hello, consulte [instalar Azure CLI 2.0](/cli/azure/install-azure-cli).
* Asegúrese de que ha revisado hello [requisitos previos](expressroute-prerequisites.md), [requisitos de enrutamiento](expressroute-routing.md), y [flujo de trabajo](expressroute-workflows.md) páginas antes de comenzar la configuración.
* Tiene que tener un circuito ExpressRoute activo. Siga las instrucciones de hello demasiado[crear un circuito ExpressRoute](howto-circuit-cli.md) y tener circuito de hello habilitada por el proveedor de conectividad antes de continuar. Hola circuito de ExpressRoute debe estar en un estado habilitado y aprovisionado para que los comandos de toobe toorun capaz de hello en este artículo.

Estas instrucciones aplican solo toocircuits creado con proveedores de servicios que ofrece servicios de conectividad de nivel 2. Si usa un proveedor de servicios que ofrece servicios administrados de nivel 3 (normalmente VPN IP, como MPLS), el mismo proveedor de conectividad configurará y administrará el enrutamiento.

Puede configurar una, dos o las tres configuraciones entre pares (Azure privado, Azure público y Microsoft) para un circuito ExpressRoute. Puede establecer las configuraciones entre pares en cualquier orden. Sin embargo, debe asegurarse de completar configuración de Hola de cada uno de ellos emparejamiento a la vez.

## <a name="azure-private-peering"></a>Configuración entre pares privados de Azure

En esta sección le ayuda a crear, obtener, actualizar y eliminar hello Azure configuración privada de emparejamiento de un circuito de ExpressRoute.

### <a name="toocreate-azure-private-peering"></a>toocreate emparejamiento privado de Azure

1. Instale la versión más reciente de Hola de CLI de Azure. Debe usar la versión más reciente de Hola de hello interfaz de línea de comandos (CLI) de Azure. * Hola revisión [requisitos previos](expressroute-prerequisites.md) y [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.

  ```azurecli
  az login
  ```

  Seleccionar suscripción Hola desea toocreate circuito de ExpressRoute

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. Crear un circuito ExpressRoute. Siga Hola instrucciones toocreate una [circuito de ExpressRoute](howto-circuit-cli.md) y hacer que se aprovisiona proveedor de conectividad de Hola.

  Si el proveedor de conectividad ofrece servicios administrados de capa 3, puede solicitar su tooenable de proveedor de conectividad Azure privada emparejamiento para usted. En ese caso, no necesitará toofollow instrucciones que se indican en las secciones siguientes se Hola. Sin embargo, si el proveedor de conectividad no administra el enrutamiento para usted, después de crear el circuito, continuar la configuración mediante los pasos siguientes de Hola.
3. Compruebe hello toomake de circuito de ExpressRoute seguro de que esté aprovisionado y también habilitado. Utilice el siguiente ejemplo de Hola:

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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. Configurar Azure intercambio de tráfico privado para el circuito de Hola. Asegúrese de que dispone de hello siguientes elementos antes de continuar con los pasos siguientes de hello:

  * / 30 subred para el vínculo principal Hola. subred de Hello no debe formar parte de cualquier espacio de direcciones reservada para las redes virtuales.
  * / 30 subred para el vínculo secundario Hola. subred de Hello no debe formar parte de cualquier espacio de direcciones reservada para las redes virtuales.
  * Un tooestablish de Id. de VLAN válido este emparejamiento correctamente. No Asegúrese de que ningún otro emparejamiento en el circuito de hello usa Hola mismo identificador de VLAN.
  * Número de sistema autónomo (AS) para la configuración entre pares. Puede usar 2 bytes o 4 bytes como números AS. Puede usar un número AS privado para esta configuración entre pares. Asegúrese de que no usa 65515.
  * **Opcional:** un hash MD5 si elige toouse uno.

  Usar hello después tooconfigure Azure privada de emparejamiento para el circuito de ejemplo:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering
  ```

  Si elige toouse un hash MD5, use Hola siguiente ejemplo:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > Asegúrese de especificar su número AS como ASN de configuración entre pares, no como cliente ASN.
  > 
  > 

### <a name="tooview-azure-private-peering-details"></a>tooview privada emparejamiento detalles de Azure

Puede obtener detalles de configuración mediante el siguiente ejemplo de Hola:

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

Hola de salida es similar toohello siguiente ejemplo:

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePrivatePeering",
  "ipv6PeeringConfig": null,
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePrivatePeering",
  "peerAsn": 7671,
  "peeringType": "AzurePrivatePeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate configuración de emparejamiento privada de Azure

Puede actualizar cualquier parte de la configuración de hello mediante el siguiente ejemplo de Hola. En este ejemplo, Id. de VLAN del circuito de Hola Hola se está actualizando desde too500 100.

```azurecli
az network express-route peering update --vlan-id 500 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

### <a name="toodelete-azure-private-peering"></a>toodelete emparejamiento privado de Azure

Puede quitar la configuración de emparejamiento ejecutando el siguiente ejemplo de Hola:

> [!WARNING]
> También debe asegurarse de que todas las redes virtuales se desvincula de hello circuito de ExpressRoute antes de ejecutar este ejemplo. 
> 
> 

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

## <a name="azure-public-peering"></a>Configuración entre pares públicos de Azure

En esta sección le ayuda a crear, obtener, actualizar y eliminar hello Azure configuración de emparejamiento público de un circuito de ExpressRoute.

### <a name="toocreate-azure-public-peering"></a>toocreate pares públicos de Azure

1. Instale la versión más reciente de Hola de CLI de Azure. Debe usar la versión más reciente de Hola de hello interfaz de línea de comandos (CLI) de Azure. * Hola revisión [requisitos previos](expressroute-prerequisites.md) y [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.

  ```azurecli
  az login
  ```

  Seleccione la suscripción de hello para el que desea toocreate circuito de ExpressRoute.

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. Crear un circuito ExpressRoute.  Siga Hola instrucciones toocreate una [circuito de ExpressRoute](howto-circuit-cli.md) y hacer que se aprovisiona proveedor de conectividad de Hola.

  Si su proveedor de conectividad ofrece servicios administrados de nivel 3, puede solicitarle que habilite la configuración entre pares privados de Azure. En ese caso, no necesitará toofollow instrucciones que se indican en las secciones siguientes se Hola. Sin embargo, si el proveedor de conectividad no administra el enrutamiento para usted, después de crear el circuito, continuar la configuración mediante los pasos siguientes de Hola.
3. Compruebe tooensure de circuito de ExpressRoute Hola está aprovisionado y también está habilitado. Utilice el siguiente ejemplo de Hola:

  ```azurecli
  az network express-route list
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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. Configure pares públicos de Azure para el circuito de Hola. Asegúrese de que dispone de hello siguiente información antes de continuar.

  * / 30 subred para el vínculo principal Hola. Tiene que ser un prefijo IPv4 público válido.
  * / 30 subred para el vínculo secundario Hola. Tiene que ser un prefijo IPv4 público válido.
  * Un tooestablish de Id. de VLAN válido este emparejamiento correctamente. No Asegúrese de que ningún otro emparejamiento en el circuito de hello usa Hola mismo identificador de VLAN.
  * Número de sistema autónomo (AS) para la configuración entre pares. Puede usar 2 bytes o 4 bytes como números AS.
  * **Opcional:** un hash MD5 si elige toouse uno.

  Ejecute hello después tooconfigure Azure pública de emparejamiento para el circuito de ejemplo:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering
  ```

  Si elige toouse un hash MD5, use Hola siguiente ejemplo:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > Asegúrese de especificar su número AS como ASN de configuración entre pares, no como cliente ASN.

### <a name="tooview-azure-public-peering-details"></a>tooview Azure pública emparejamiento detalles

Puede obtener detalles de configuración mediante el siguiente ejemplo de Hola:

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

Hola de salida es similar toohello siguiente ejemplo:

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePublicPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePublicPeering",
  "peerAsn": 7671,
  "peeringType": "AzurePublicPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-public-peering-configuration"></a>tooupdate configuración de interconexión pública de Azure

Puede actualizar cualquier parte de la configuración de hello mediante el siguiente ejemplo de Hola. En este ejemplo, Id. de VLAN del circuito de Hola Hola se está actualizando desde too600 200.

```azurecli
az network express-route peering update --vlan-id 600 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

### <a name="toodelete-azure-public-peering"></a>toodelete pares públicos de Azure

Puede quitar la configuración de emparejamiento ejecutando el siguiente ejemplo de Hola:

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

## <a name="microsoft-peering"></a>Emparejamiento de Microsoft

En esta sección le ayuda a crear, obtener, actualizar y eliminar la configuración de emparejamiento de Microsoft de Hola por un circuito ExpressRoute.

> [!IMPORTANT]
> Emparejamiento de Microsoft de circuitos ExpressRoute que estaban configurados anterior tooAugust 1, 2017 tendrá todos los prefijos de servicio implementados a través de emparejamiento de Microsoft hello, incluso si no se definen los filtros de ruta. Emparejamiento de Microsoft de circuitos ExpressRoute configurados en o después del 1 de agosto de 2017 no tendrá todos los prefijos anunciados hasta que se conecte un filtro de ruta toohello circuito. Para más información, consulte [Configuración de un filtro de ruta para el emparejamiento de Microsoft](how-to-routefilter-powershell.md).
> 
> 

### <a name="toocreate-microsoft-peering"></a>emparejamiento de Microsoft toocreate

1. Instale la versión más reciente de Hola de CLI de Azure. Usar versión más reciente de Hola de hello interfaz de línea de comandos (CLI) de Azure. * Hola revisión [requisitos previos](expressroute-prerequisites.md) y [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.

  ```azurecli
  az login
  ```

  Seleccione la suscripción de hello para el que desea toocreate circuito de ExpressRoute.

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. Crear un circuito ExpressRoute. Siga Hola instrucciones toocreate una [circuito de ExpressRoute](howto-circuit-cli.md) y hacer que se aprovisiona proveedor de conectividad de Hola.

  Si el proveedor de conectividad ofrece servicios administrados de capa 3, puede solicitar su tooenable de proveedor de conectividad Azure privada emparejamiento para usted. En ese caso, no necesitará toofollow instrucciones que se indican en las secciones siguientes se Hola. Sin embargo, si el proveedor de conectividad no administra el enrutamiento para usted, después de crear el circuito, continuar la configuración mediante los pasos siguientes de Hola.

3. Compruebe hello toomake de circuito de ExpressRoute seguro de que esté aprovisionado y también habilitado. Utilice el siguiente ejemplo de Hola:

  ```azurecli
  az network express-route list
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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. Configurar Microsoft emparejamiento para el circuito de Hola. Asegúrese de que haya Hola siguiente información antes de continuar.

  * / 30 subred para el vínculo principal Hola. Debe ser un prefijo de IPv4 público válido que sea de su propiedad y esté registrado en un Registro regional de Internet (RIR) o un Registro de enrutamiento de Internet (IRR).
  * / 30 subred para el vínculo secundario Hola. Debe ser un prefijo de IPv4 público válido que sea de su propiedad y esté registrado en un Registro regional de Internet (RIR) o un Registro de enrutamiento de Internet (IRR).
  * Un tooestablish de Id. de VLAN válido este emparejamiento correctamente. No Asegúrese de que ningún otro emparejamiento en el circuito de hello usa Hola mismo identificador de VLAN.
  * Número de sistema autónomo (AS) para la configuración entre pares. Puede usar 2 bytes o 4 bytes como números AS.
  * Anuncian prefijos: debe proporcionar una lista de todos los prefijos piensa tooadvertise en las sesiones BGP Hola. Se aceptan solo prefijos de direcciones IP públicas. Si tiene previsto toosend un conjunto de prefijos, puede enviar una lista separada por comas. Estos prefijos deben ser tooyou registrado en un RIR / IRR.
  * **Opcional:** cliente ASN: si es que los prefijos de publicidad que no están registrado toohello emparejamiento como número, puede especificar hello como número toowhich están registrados.
  * Nombre del enrutamiento del registro: Puede especificar Hola RIR / IRR en qué hello como número y los prefijos registrados.
  * **Opcional:** un hash MD5 si elige toouse uno.

   Ejecute hello siguiendo la emparejamiento de Microsoft tooconfigure de ejemplo para el circuito:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 123.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 123.0.0.4/30 --vlan-id 300 --peering-type MicrosoftPeering --advertised-public-prefixes 123.1.0.0/24
  ```

### <a name="tooget-microsoft-peering-details"></a>detalles de emparejamiento de Microsoft tooget

Puede obtener detalles de configuración mediante el siguiente ejemplo de Hola:

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzureMicrosoftPeering
```

Hola de salida es similar toohello siguiente ejemplo:

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzureMicrosoftPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": {
    "advertisedPublicPrefixes": [
        ""
      ],
     "advertisedPublicPrefixesState": "",
     "customerASN": ,
     "routingRegistryName": ""
  }
  "name": "AzureMicrosoftPeering",
  "peerAsn": ,
  "peeringType": "AzureMicrosoftPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-microsoft-peering-configuration"></a>configuración de emparejamiento de Microsoft tooupdate

Puede actualizar cualquier parte de la configuración de Hola. Hola anuncia prefijos del circuito de Hola se están actualizando desde 123.1.0.0/24 too124.1.0.0/24 en el siguiente ejemplo de Hola:

```azurecli
az network express-route peering update --circuit-name MyCircuit -g ExpressRouteResourceGroup --peering-type MicrosoftPeering --advertised-public-prefixes 124.1.0.0/24
```

### <a name="toodelete-microsoft-peering"></a>emparejamiento de Microsoft toodelete

Puede quitar la configuración de emparejamiento ejecutando el siguiente ejemplo de Hola:

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name MicrosoftPeering
```

## <a name="next-steps"></a>Pasos siguientes

Siguiente paso, [vincular un circuito de ExpressRoute de red virtual tooan](howto-linkvnet-cli.md).

* Para más información sobre los flujos de trabajo de ExpressRoute, vea [Flujos de trabajo de ExpressRoute](expressroute-workflows.md).
* Para más información sobre el emparejamiento de circuitos, vea [Circuitos y dominios de enrutamiento de ExpressRoute](expressroute-circuit-peerings.md).
* Para más información sobre redes virtuales, vea [Información general sobre redes virtuales](../virtual-network/virtual-networks-overview.md).