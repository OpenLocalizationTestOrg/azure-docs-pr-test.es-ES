---
title: 'Conectar la red virtual tooanother red virtual: CLI de Azure | Documentos de Microsoft'
description: "Este artículo le guía por la conexión de redes virtuales entre sí por medio de Azure Resource Manager y la CLI de Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0683c664-9c03-40a4-b198-a6529bf1ce8b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 70113914bcae03c80f9ad133ff081d1cf37fc309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-azure-cli"></a>Configuración de una conexión de puerta de enlace de VPN de red virtual a red virtual mediante la CLI de Azure

Este artículo muestra cómo toocreate una conexión de puerta de enlace VPN entre redes virtuales. Hello redes virtuales pueden estar en Hola mismo o en distintas regiones y de Hola iguales o distintas suscripciones. Al conectar redes virtuales de distintas suscripciones, las suscripciones de hello no es necesario toobe asociada Hola a mismo inquilino de Active Directory. 

pasos de Hello en este artículo aplican el modelo de implementación del Administrador de recursos de toohello y utilizar CLI de Azure. También puede crear esta configuración con una herramienta de implementación diferentes o un modelo de implementación seleccionando una opción diferente de hello lista siguiente:

> [!div class="op_single_selector"]
> * [Portal de Azure](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [CLI de Azure](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Portal de Azure clásico](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Conexión de diferentes modelos de implementación - Azure Portal](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Conexión de diferentes modelos de implementación - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

Conectar una red virtual (VNet a VNet) tooanother de red virtual es similar tooconnecting una ubicación de sitio de red virtual tooan local. Ambos tipos de conectividad usan un tooprovide de puerta de enlace VPN un túnel seguro mediante IPsec/IKE. Si sus redes virtuales están en hello misma región, puede que desee tooconsider conectándolos mediante el intercambio de tráfico de red virtual. El emparejamiento de VNET no usa VPN Gateway. Para más información, consulte [Emparejamiento de VNET](../virtual-network/virtual-network-peering-overview.md).

Se puede combinar la comunicación entre redes virtuales con configuraciones de varios sitios. Esto le permite establecer topologías de red que combinen la conectividad entre entornos con conectividad entre redes virtuales, como se muestra en hello siguiente diagrama:

![Acerca de las conexiones](./media/vpn-gateway-howto-vnet-vnet-cli/aboutconnections.png)

### <a name="why"></a>¿Por qué debería conectarse a redes virtuales?

Puede que desee tooconnect las redes virtuales para hello siguientes motivos:

* **Presencia geográfica y redundancia geográfica entre regiones**

  * Puede configurar su propia replicación geográfica o sincronización con conectividad segura sin recurrir a los puntos de conexión a Internet.
  * Con el Equilibrador de carga y el Administrador de tráfico de Azure, puede configurar cargas de trabajo de alta disponibilidad con redundancia geográfica en varias regiones de Azure. Por ejemplo, puede tooset seguridad SQL Always On con grupos de disponibilidad a través de varias regiones de Azure.
* **Aplicaciones regionales de niveles múltiples con aislamiento o un límite administrativo**

  * Hola dentro mismo región, puede configurar aplicaciones de varios niveles con varias redes virtuales conectadas entre sí debido tooisolation o requisitos administrativos.

Para obtener más información acerca de las conexiones de red virtual a red virtual, vea hello [P+F de red virtual a red virtual](#faq) final Hola de este artículo.

### <a name="which-set-of-steps-should-i-use"></a>¿Qué serie de pasos debo seguir?

En este artículo, verá dos conjuntos de pasos diferentes. Un conjunto de pasos para [redes virtuales que residen en Hola misma suscripción](#samesub)y otro para [redes virtuales que residen en distintas suscripciones](#difsub).

## <a name="samesub"></a>Conectar redes virtuales que se encuentran en hello misma suscripción

![diagrama de v2v](./media/vpn-gateway-howto-vnet-vnet-cli/v2vrmps.png)

### <a name="before-you-begin"></a>Antes de empezar

Antes de comenzar, instalar la versión más reciente de Hola de comandos de CLI de hello (2.0 o posteriores). Para obtener información acerca de cómo instalar los comandos de CLI de hello, consulte [instalar Azure CLI 2.0](/cli/azure/install-azure-cli).

### <a name="Plan"></a>Planeamiento de los intervalos de direcciones IP

Hola pasos, se crea dos redes virtuales junto con sus subredes correspondientes de la puerta de enlace y las configuraciones. Creamos, a continuación, una conexión VPN entre Hola dos redes virtuales. Es importante tooplan intervalos de direcciones IP de hello para la configuración de red. Tenga en cuenta que hay que asegurarse de que ninguno de los intervalos de VNet o intervalos de red local se solapen. En estos ejemplos, no se incluye ningún servidor DNS. Si desea disponer de resolución de nombres en las redes virtuales, consulte [Resolución de nombres](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

Utilizamos Hola después los valores en los ejemplos de hello:

**Valores para TestVNet1:**

* Nombre de red virtual: TestVNet1
* Grupo de recursos: TestRG1
* Ubicación: Este de EE. UU.
* TestVNet1: 10.11.0.0/16 y 10.12.0.0/16
* FrontEnd: 10.11.0.0/24
* Backend: 10.12.0.0/24
* GatewaySubnet: 10.12.255.0/27
* GatewayName: VNet1GW
* Dirección IP pública: VNet1GWIP
* VPNType: RouteBased
* Connection(1to4): VNet1toVNet4
* Connection(1to5): VNet1toVNet5
* ConnectionType: VNet2VNet

**Valores para TestVNet4:**

* Nombre de red virtual: TestVNet4
* TestVNet2: 10.41.0.0/16 y 10.42.0.0/16
* FrontEnd: 10.41.0.0/24
* Backend: 10.42.0.0/24
* GatewaySubnet: 10.42.255.0/27
* Grupo de recursos: TestRG4
* Ubicación: Oeste de EE. UU.
* GatewayName: VNet4GW
* Dirección IP pública: VNet4GWIP
* VPNType: RouteBased
* Conexión: VNet4toVNet1
* ConnectionType: VNet2VNet


### <a name="Connect"></a>Paso 1: conectar tooyour suscripción

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-numbers-include.md)]

### <a name="TestVNet1"></a>Paso 2: Creación y configuración de TestVNet1

1. Cree un grupo de recursos.

  ```azurecli
  az group create -n TestRG1  -l eastus
  ```
2. Crear subredes hello y TestVNet1 para TestVNet1. En este ejemplo se crea una red virtual denominada TestVNet1 y una subred llamada FrontEnd.

  ```azurecli
  az network vnet create -n TestVNet1 -g TestRG1 --address-prefix 10.11.0.0/16 -l eastus --subnet-name FrontEnd --subnet-prefix 10.11.0.0/24
  ```
3. Crear un espacio de direcciones adicionales para la subred de back-end de Hola. Tenga en cuenta que en este paso, se especifique tanto espacio de direcciones de Hola que hemos creado con anterioridad y Hola espacio de direcciones adicional que deseamos tooadd. Esto es porque hello [actualizar la red virtual de red az](https://docs.microsoft.com/cli/azure/network/vnet#update) comando sobrescribe la configuración anterior Hola. Asegúrese de toospecify seguro todos Hola prefijos de dirección cuando se usa este comando.

  ```azurecli
  az network vnet update -n TestVNet1 --address-prefixes 10.11.0.0/16 10.12.0.0/16 -g TestRG1
  ```
4. Crear una subred de back-end de Hola.
  
  ```azurecli
  az network vnet subnet create --vnet-name TestVNet1 -n BackEnd -g TestRG1 --address-prefix 10.12.0.0/24 
  ```
5. Crear una subred de puerta de enlace de Hola. Tenga en cuenta que esa subred de puerta de enlace de hello es denominada "GatewaySubnet". Este nombre es obligatorio. En este ejemplo, la subred de puerta de enlace de hello está usando un /27. Aunque es posible toocreate una subred de puerta de enlace tan pequeña como /29, le recomendamos que cree una subred mayor que incluye direcciones más si se selecciona al menos /28 o /27. Esto le permitirá suficientes direcciones tooaccommodate posibles configuraciones adicionales que puede querer en hello futuras.

  ```azurecli 
  az network vnet subnet create --vnet-name TestVNet1 -n GatewaySubnet -g TestRG1 --address-prefix 10.12.255.0/27
  ```
6. Solicitar una pública dirección toobe toohello asignado puerta de enlace IP que creará para la red virtual. Tenga en cuenta que hello AllocationMethod es dinámico. No se puede especificar la dirección IP de Hola que desee toouse. Es puerta de enlace de tooyour asignada dinámicamente.

  ```azurecli
  az network public-ip create -n VNet1GWIP -g TestRG1 --allocation-method Dynamic
  ```
7. Crear puerta de enlace de red virtual de Hola para TestVNet1. Las configuraciones VNet a VNet requieren un VpnType RouteBased. Si ejecuta este comando usando hello '--sin - wait' parámetro, no ve los comentarios o la salida. Hello '--sin - wait' parámetro permite toocreate de puerta de enlace de hello en segundo plano de Hola. No significa que esa puerta de enlace VPN de hello finaliza la creación de inmediatamente. Crear una puerta de enlace a menudo puede tardar 45 minutos o más, en función de puerta de enlace de hello SKU que usar.

  ```azurecli
  az network vnet-gateway create -n VNet1GW -l eastus --public-ip-address VNet1GWIP -g TestRG1 --vnet TestVNet1 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="TestVNet4"></a>Paso 3: Creación y configuración de TestVNet4

1. Cree un grupo de recursos.

  ```azurecli
  az group create -n TestRG4  -l westus
  ```
2. Cree TestVNet4.

  ```azurecli
  az network vnet create -n TestVNet4 -g TestRG4 --address-prefix 10.41.0.0/16 -l westus --subnet-name FrontEnd --subnet-prefix 10.41.0.0/24
  ```

3. Cree subredes adicionales para TestVNet4.

  ```azurecli
  az network vnet update -n TestVNet4 --address-prefixes 10.41.0.0/16 10.42.0.0/16 -g TestRG4 
  az network vnet subnet create --vnet-name TestVNet4 -n BackEnd -g TestRG4 --address-prefix 10.42.0.0/24 
  ```
4. Crear una subred de puerta de enlace de Hola.

  ```azurecli
   az network vnet subnet create --vnet-name TestVNet4 -n GatewaySubnet -g TestRG4 --address-prefix 10.42.255.0/27
  ```
5. Solicite una dirección IP pública.

  ```azurecli
  az network public-ip create -n VNet4GWIP -g TestRG4 --allocation-method Dynamic
  ```
6. Crear puerta de enlace de red virtual de hello TestVNet4.

  ```azurecli
  az network vnet-gateway create -n VNet4GW -l westus --public-ip-address VNet4GWIP -g TestRG4 --vnet TestVNet4 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="createconnect"></a>Paso 4: crear conexiones de Hola

Ahora tiene dos redes virtuales con puertas de enlace de VPN. Hola siguiente paso es toocreate las conexiones de puerta de enlace VPN entre puertas de enlace de red virtual de Hola. Si ha utilizado ejemplos de hello anteriores, las puertas de enlace de red virtual se encuentran en distintos grupos de recursos. Cuando las puertas de enlace están en distintos grupos de recursos, es necesario tooidentify y especifique el Id. de recurso de Hola para cada puerta de enlace al establecer una conexión. Si sus redes virtuales están en hello mismo grupo de recursos, puede usar hello [segundo conjunto de instrucciones](#samerg) porque no necesita Id. de recurso de hello toospecify.

### <a name="diffrg"></a>tooconnect redes virtuales que residen en distintos grupos de recursos

1. Obtener Id. de recurso de VNet1GW Hola de salida de hello de hello siguiente comando:

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  En la salida de hello, encontrar Hola "Id.:" línea. los valores de Hello entre comillas Hola son necesarios toocreate Hola conexión en la sección siguiente de Hola. Copie estos editor de texto tooa de valores, como el Bloc de notas, para que pueda pegarlos fácilmente al crear la conexión.

  Salida de ejemplo:

  ```
  "activeActive": false, 
  "bgpSettings": { 
    "asn": 65515, 
    "bgpPeeringAddress": "10.12.255.30", 
    "peerWeight": 0 
   }, 
  "enableBgp": false, 
  "etag": "W/\"ecb42bc5-c176-44e1-802f-b0ce2962ac04\"", 
  "gatewayDefaultSite": null, 
  "gatewayType": "Vpn", 
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW", 
  "ipConfigurations":
  ```

  Copiar valores de hello después **"id":** entre comillas Hola.

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
 ```

2. Obtener Hola Id. de recurso de VNet4GW y copie Hola valores tooa editor de texto.

  ```azurecli
  az network vnet-gateway show -n VNet4GW -g TestRG4
  ```

3. Crear hello TestVNet1 tooTestVNet4 conexión. En este paso, se crea la conexión de Hola de TestVNet1 tooTestVNet4. No hay una clave compartida que se hace referencia en los ejemplos de hello. Puede utilizar sus propios valores de clave compartida de Hola. Hola importante que es esa clave compartida de hello debe coincidir en las dos conexiones. Crear una conexión, toma un valor bajo al toocomplete.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW 
  ```
4. Crear hello TestVNet4 tooTestVNet1 conexión. Este paso es similar toohello uno anterior, salvo que va a crear la conexión Hola de TestVNet4 tooTestVNet1. Asegúrese de que coincide con las claves de hello compartido. Tarda unos minutos en conexión de hello tooestablish.

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG4 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW -l westus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1G
  ```
5. Compruebe las conexiones. Consulte [Comprobación de las conexiones](#verify).

### <a name="samerg"></a>tooconnect redes virtuales que residen en hello mismo grupo de recursos

1. Crear hello TestVNet1 tooTestVNet4 conexión. En este paso, se crea la conexión de Hola de TestVNet1 tooTestVNet4. Grupos de recursos de Hola de aviso se Hola igual en los ejemplos de hello. También verá una clave compartida que se hace referencia en los ejemplos de hello. Puede utilizar sus propios valores de clave compartida de hello, sin embargo, debe coincidir con una clave compartida hello para ambas conexiones. Crear una conexión, toma un valor bajo al toocomplete.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet4GW
  ```
2. Crear hello TestVNet4 tooTestVNet1 conexión. Este paso es similar toohello uno anterior, salvo que va a crear la conexión Hola de TestVNet4 tooTestVNet1. Asegúrese de que coincide con las claves de hello compartido. Tarda unos minutos en conexión de hello tooestablish.

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG1 --vnet-gateway1 VNet4GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet1GW
  ```
3. Compruebe las conexiones. Consulte [Comprobación de las conexiones](#verify).

## <a name="difsub"></a>Conexión de redes virtuales que están en suscripciones diferentes

![diagrama de v2v](./media/vpn-gateway-howto-vnet-vnet-cli/v2vdiffsub.png)

En este escenario, conectaremos TestVNet1 y TestVNet5. Hola redes virtuales residen distintas suscripciones. las suscripciones de Hello no es necesario toobe asociado con hello mismo inquilino de Active Directory. pasos de Hola para esta configuración de agregan una conexión de red virtual a red virtual adicional en orden tooconnect TestVNet1 tooTestVNet5.

### <a name="TestVNet1diff"></a>Paso 5: Creación y configuración de TestVNet1

Seguir estas instrucciones de los pasos de hello en secciones anteriores de Hola. Debe completar [paso 1](#Connect) y [paso 2](#TestVNet1) toocreate TestVNet1 y configurar hello puerta de enlace VPN para TestVNet1. Para esta configuración, no es necesario toocreate TestVNet4 desde la sección anterior de hello, aunque si lo creó, no estará en conflicto con estos pasos. Cuando haya completado el paso 1 y el 2, continúe con el paso 6 (a continuación).

### <a name="verifyranges"></a>Paso 6: comprobar los intervalos de direcciones IP de Hola

Al crear conexiones adicionales, es importante tooverify que espacio de direcciones IP de saludo de la nueva red virtual de hello no se superponga con ninguno de los otros intervalos de VNet o intervalos de puerta de enlace de red local. Para este ejercicio, puede usar Hola después de valores de hello TestVNet5:

**Valores para TestVNet5:**

* Nombre de red virtual: TestVNet5
* Grupo de recursos: TestRG5
* Ubicación: Japón Oriental
* TestVNet5: 10.51.0.0/16 y 10.52.0.0/16
* FrontEnd: 10.51.0.0/24
* Backend: 10.52.0.0/24
* GatewaySubnet: 10.52.255.0.0/27
* GatewayName: VNet5GW
* Dirección IP pública: VNet5GWIP
* VPNType: RouteBased
* Conexión: VNet5toVNet1
* ConnectionType: VNet2VNet

### <a name="TestVNet5"></a>Paso 7: Creación y configuración de TestVNet5

Este paso debe realizarse en el contexto de Hola de nueva suscripción hello, 5 de suscripción. Administrador de hello en otra organización que posee la suscripción de hello puede realizar esta parte. tooswitch entre el uso de suscripciones ' lista de cuentas de az--todos los ' toolist Hola cuenta tooyour disponibles de las suscripciones y luego use ' az cuenta conjunto--suscripción <subscriptionID>' tooswitch toohello suscripción que desea toouse.

1. Asegúrese de que está conectado tooSubscription 5 y luego crea un grupo de recursos.

  ```azurecli
  az group create -n TestRG5  -l japaneast
  ```
2. Cree TestVNet5.

  ```azurecli
  az network vnet create -n TestVNet5 -g TestRG5 --address-prefix 10.51.0.0/16 -l japaneast --subnet-name FrontEnd --subnet-prefix 10.51.0.0/24
  ```

3. Agregue subredes.

  ```azurecli
  az network vnet update -n TestVNet5 --address-prefixes 10.51.0.0/16 10.52.0.0/16 -g TestRG5
  az network vnet subnet create --vnet-name TestVNet5 -n BackEnd -g TestRG5 --address-prefix 10.52.0.0/24
  ```

4. Agregar subred de puerta de enlace de Hola.

  ```azurecli
  az network vnet subnet create --vnet-name TestVNet5 -n GatewaySubnet -g TestRG5 --address-prefix 10.52.255.0/27
  ```

5. Pida una dirección IP pública.

  ```azurecli
  az network public-ip create -n VNet5GWIP -g TestRG5 --allocation-method Dynamic
  ```
6. Crear puerta de enlace de hello TestVNet5

  ```azurecli
  az network vnet-gateway create -n VNet5GW -l japaneast --public-ip-address VNet5GWIP -g TestRG5 --vnet TestVNet5 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="connections5"></a>Paso 8: crear conexiones de Hola

Dividiremos este paso en dos sesiones CLI marcados como **[1 suscripción]**, y **[suscripción 5]** porque son puertas de enlace de hello en distintas suscripciones de Hola. tooswitch entre el uso de suscripciones ' lista de cuentas de az--todos los ' toolist Hola cuenta tooyour disponibles de las suscripciones y luego use ' az cuenta conjunto--suscripción <subscriptionID>' tooswitch toohello suscripción que desea toouse.

1. **[Suscripción 1]**  Iniciar sesión y conectarse tooSubscription 1. Siguiente ejecución Hola de comandos de nombre de hello tooget y el identificador del programa Hola a puerta de enlace de salida de hello:

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  Copiar el resultado de hello para "Id.:". Enviar identificador de Hola y el nombre de Hola de hello red virtual (VNet1GW) de la puerta de enlace toohello Administrador de 5 de la suscripción a través de correo electrónico u otro método.

  Salida de ejemplo:

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
  ```

2. **[Suscripción 5]**  Iniciar sesión y conectarse tooSubscription 5. Siguiente ejecución Hola de comandos de nombre de hello tooget y el identificador del programa Hola a puerta de enlace de salida de hello:

  ```azurecli
  az network vnet-gateway show -n VNet5GW -g TestRG5
  ```

  Copiar el resultado de hello para "Id.:". Enviar identificador de Hola y el nombre de Hola de hello red virtual (VNet5GW) de la puerta de enlace toohello Administrador de suscripción: 1 a través de correo electrónico u otro método.

3. **[Suscripción 1]**  En este paso, crear conexión Hola de TestVNet1 tooTestVNet5. Puede utilizar sus propios valores de clave compartida de hello, sin embargo, debe coincidir con una clave compartida hello para ambas conexiones. Crear una conexión puede tardar un poco al toocomplete. Asegúrese de que se conecta tooSubscription 1.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet5 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```

4. **[Suscripción 5]**  Este paso es toohello similar uno anterior, excepto que va a crear la conexión Hola de TestVNet5 tooTestVNet1. Asegúrese de que ese Hola compartidos coincidencia de claves y se conecta tooSubscription 5.

  ```azurecli
  az network vpn-connection create -n VNet5ToVNet1 -g TestRG5 --vnet-gateway1 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW -l japaneast --shared-key "eeffgg" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```

## <a name="verify"></a>Compruebe las conexiones de Hola
[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections v2v cli](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

## <a name="faq"></a>P+F sobre conexiones de red virtual a red virtual
[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a>Pasos siguientes

* Una vez completada la conexión, puede agregar redes virtuales de máquinas virtuales tooyour. Para obtener más información, vea hello [documentación de máquinas virtuales](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).
* Para obtener información sobre BGP, consulte hello [información general de BGP](vpn-gateway-bgp-overview.md) y [cómo tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
