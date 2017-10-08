---
title: puerta de enlace de aplicaciones de Azure con el equilibrador de carga interno - PowerShell aaaUsing | Documentos de Microsoft
description: "Esta página proporciona instrucciones toocreate, configurar, iniciar y eliminar una puerta de enlace de la aplicación de Azure con el equilibrador de carga interno (ILB) para el Administrador de recursos de Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 75cfd5a2-e378-4365-99ee-a2b2abda2e0d
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: dd0d7e954b1fa219ae6ebe42cb4b479dbcf08653
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb-by-using-azure-resource-manager"></a>Creación de una puerta de enlace de aplicaciones con un equilibrador de carga interno (ILB) mediante el Administrador de recursos de Azure

> [!div class="op_single_selector"]
> * [Azure Classic PowerShell](application-gateway-ilb.md)
> * [PowerShell del Administrador de recursos de Azure](application-gateway-ilb-arm.md)

Puerta de enlace de aplicación de Azure puede configurarse con una VIP accesible desde Internet o con un extremo interno que no está expuesta toohello Internet, también conocido como un punto de conexión de (ILB) de equilibrador de carga interno. Configurar puerta de enlace de hello con un ILB es útil para aplicaciones de línea de negocio internas que no están expuesta toohello Internet. También es útil para los servicios y niveles dentro de una aplicación de varios nivel que se colocan en un límite de seguridad que no está expuesta toohello Internet pero que aún requieren round robin cargar distribución, adherencia de sesión o de finalización de la capa de Sockets seguros (SSL).

Este artículo le guiará a través de hello pasos tooconfigure una puerta de enlace de la aplicación con un ILB.

## <a name="before-you-begin"></a>Antes de empezar

1. Instalar versión más reciente de Hola de cmdlets de PowerShell de Azure de hello mediante Hola instalador de plataforma Web. Puede descargar e instalar la versión más reciente de Hola de hello **Windows PowerShell** sección de hello [página de descargas](https://azure.microsoft.com/downloads/).
2. Tendrá que crear una red virtual y una subred para Puerta de enlace de aplicaciones. Asegúrese de que no hay máquinas virtuales o las implementaciones de nube están usando la subred de Hola. La puerta de enlace de aplicaciones debe encontrarse en una subred de una red virtual.
3. deben existir servidores Hola configurar la puerta de enlace de aplicaciones de toouse Hola o tener asignados de sus puntos de conexión creados en la red virtual de Hola o con una dirección IP pública/VIP.

## <a name="what-is-required-toocreate-an-application-gateway"></a>¿Qué es necesario toocreate una puerta de enlace de la aplicación?

* **Grupo de servidores de back-end:** Hola lista de direcciones IP de servidores de back-end de Hola. Hello direcciones IP mostradas deben o bien pertenecer toohello de red virtual, pero en una subred diferente para la puerta de enlace de aplicaciones de Hola o debe ser una dirección IP pública/VIP.
* **Configuración del grupo de servidores back-end:** cada grupo tiene una configuración en la que se incluye el puerto, el protocolo y la afinidad basada en cookies. Esta configuración está ligada tooa grupo y son servidores de tooall aplicados en el grupo de Hola.
* **Puerto front-end:** este puerto es Hola pública que se abre en la puerta de enlace de aplicaciones de Hola. Tráfico llega a este puerto y, a continuación, obtiene redirigido tooone de servidores de back-end de Hola.
* **Agente de escucha:** agente de escucha de hello tiene un puerto front-end, un protocolo (Http o Https, estos distinguen mayúsculas de minúsculas) y el nombre del certificado SSL hello (si se descarga la configuración de SSL).
* **Regla:** regla Hola enlaza el agente de escucha de Hola y el grupo de servidores de back-end de Hola y define qué tráfico de Hola de grupo de servidor back-end debe ser dirigido toowhen llega a un agente de escucha determinado. Actualmente, solo Hola *básico* se admite la regla. Hola *básica* regla es la distribución de carga round robin.

## <a name="create-an-application-gateway"></a>Creación de una puerta de enlace de aplicaciones

diferencia de Hello entre el uso de Azure clásico y el Administrador de recursos de Azure es orden de hello en el que crear puerta de enlace de aplicaciones de Hola y elementos de Hola que necesitan toobe configurado.
Con el Administrador de recursos, todos los elementos que conforman una puerta de enlace de la aplicación se configura individualmente y, a continuación, reunir toocreate de recursos de puerta de enlace de aplicación Hola.

Estos son los pasos de Hola que son necesario toocreate una puerta de enlace de la aplicación:

1. Creación de un grupo de recursos para el Administrador de recursos
2. Crear una red virtual y una subred de puerta de enlace de aplicación Hola
3. Creación de un objeto de configuración de la Puerta de enlace de aplicaciones
4. Crear un recurso de la puerta de enlace de aplicaciones

## <a name="create-a-resource-group-for-resource-manager"></a>Creación de un grupo de recursos para el Administrador de recursos

Asegúrese de que cambia el modo toouse hello Azure Resource Manager cmdlets de PowerShell. Hay más información disponible en [Uso de Windows PowerShell con Resource Manager](../powershell-azure-resource-manager.md).

### <a name="step-1"></a>Paso 1

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>Paso 2

Compruebe las suscripciones de hello para la cuenta de hello.

```powershell
Get-AzureRmSubscription
```

Son tooauthenticate solicitada con sus credenciales.

### <a name="step-3"></a>Paso 3

Elija qué su toouse de las suscripciones de Azure.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>Paso 4

Cree un grupo de recursos nuevo (omita este paso si usa uno existente).

```powershell
New-AzureRmResourceGroup -Name appgw-rg -location "West US"
```

Azure Resource Manager requiere que todos los grupos de recursos especifiquen una ubicación. Esto se utiliza como ubicación predeterminada de Hola para recursos de ese grupo de recursos. Asegúrese de que todos los toocreate de comandos utiliza una puerta de enlace de la aplicación Hola mismo grupo de recursos.

En el anterior ejemplo de Hola, hemos creado un grupo de recursos denominado "Appgw-rg" y la ubicación "West US".

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Crear una red virtual y una subred de puerta de enlace de aplicación Hola

Hola siguiente ejemplo se muestra cómo toocreate una red virtual mediante el Administrador de recursos:

### <a name="step-1"></a>Paso 1

```powershell
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

Este paso asigna Hola dirección intervalo 10.0.0.0/24 tooa subred toobe variable utiliza toocreate una red virtual.

### <a name="step-2"></a>Paso 2

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnetconfig
```

Este paso crea una red virtual denominada "appgwvnet" en recurso grupo "appgw-rg" de región de oeste de Estados Unidos de hello con hello prefijo 10.0.0.0/16 subred 10.0.0.0/24.

### <a name="step-3"></a>Paso 3

```powershell
$subnet = $vnet.subnets[0]
```

Este paso asigna Hola subred objeto toovariable $subnet para obtener instrucciones de Hola.

## <a name="create-an-application-gateway-configuration-object"></a>Creación de un objeto de configuración de la Puerta de enlace de aplicaciones

### <a name="step-1"></a>Paso 1

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

Este paso crea una configuración de la IP de la puerta de enlace de aplicaciones denominada "gatewayIP01". Cuando se inicia la puerta de enlace de aplicaciones, toma una dirección IP de subred Hola configurado y enrutar las direcciones IP de toohello de tráfico de red en el grupo de direcciones IP de back-end de Hola. Tenga en cuenta que cada instancia toma una dirección IP.

### <a name="step-2"></a>Paso 2

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.1.1.8,10.1.1.9,10.1.1.10
```

Este paso configura el grupo de direcciones IP Hola back-end denominado "pool01" con la dirección IP se refiere a "10.1.1.8, 10.1.1.9, 10.1.1.10". Esos son direcciones IP de Hola que reciben tráfico de red de Hola que provienen de extremo IP de front-end de Hola. Reemplace Hola anterior tooadd de direcciones IP de sus propios extremos de dirección IP de aplicación.

### <a name="step-3"></a>Paso 3

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

Este paso configura el tráfico de red de puerta de enlace configuración "poolsetting01" para la carga de hello equilibrada de aplicación en el grupo de back-end de Hola.

### <a name="step-4"></a>Paso 4

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80
```

Este paso configura el puerto IP front-end Hola denominado "frontendport01" para hello ILB.

### <a name="step-5"></a>Paso 5

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -Subnet $subnet
```

Este paso crea Hola la configuración de IP front-end denominada "fipconfig01" y lo asocia con una dirección de IP privada de la subred de red virtual de hello actual.

### <a name="step-6"></a>Paso 6

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp
```

Este paso crea el agente de escucha de hello denominado "listener01" y asocia la configuración de IP front-end de hello puerto front-end toohello.

### <a name="step-7"></a>Paso 7

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

Este paso crea Hola regla equilibrador de carga enrutamiento denominado "rule01" que configura el comportamiento de equilibrador de carga de Hola.

### <a name="step-8"></a>Paso 8

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

Este paso configura el tamaño de la instancia de puerta de enlace de aplicación Hola Hola.

> [!NOTE]
> Hola valor predeterminado de *InstanceCount* es 2, con un valor máximo de 10. Hola valor predeterminado de *GatewaySize* es Medium. Se puede elegir entre Standard_Small, Standard_Medium y Standard_Large.

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a>Creación de una puerta de enlace de aplicaciones con New-AzureApplicationGateway

Crea una puerta de enlace de la aplicación con todos los elementos de configuración de hello pasos anteriores. En este ejemplo, la puerta de enlace de aplicaciones de Hola se denomina "appgwtest".

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

Este paso crea una puerta de enlace de la aplicación con todos los elementos de configuración de hello pasos anteriores. En el ejemplo de Hola, puerta de enlace de aplicaciones de Hola se denomina "appgwtest".

## <a name="delete-an-application-gateway"></a>Eliminación de una puerta de enlace de aplicaciones

toodelete una puerta de enlace de la aplicación, necesita hello toodo siguiendo los pasos en orden:

1. Hola de uso `Stop-AzureRmApplicationGateway` puerta de enlace de cmdlet toostop Hola.
2. Hola de uso `Remove-AzureRmApplicationGateway` puerta de enlace de cmdlet tooremove Hola.
3. Compruebe dicha puerta de enlace de Hola se ha eliminado mediante el uso de hello `Get-AzureApplicationGateway` cmdlet.

### <a name="step-1"></a>Paso 1

Obtener el objeto de puerta de enlace de aplicación hello y asócielo variable tooa "$getgw".

```powershell
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

### <a name="step-2"></a>Paso 2

Use `Stop-AzureRmApplicationGateway` puerta de enlace de aplicaciones de toostop Hola. Este ejemplo muestra hello `Stop-AzureRmApplicationGateway` cmdlet en la primera línea hello, seguido de la salida de hello.

```powershell
Stop-AzureRmApplicationGateway -ApplicationGateway $getgw  
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

Una vez que la puerta de enlace de aplicaciones de hello está en estado detenido, use hello `Remove-AzureRmApplicationGateway` servicio de cmdlet tooremove Hola.

```powershell
Remove-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Force
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

> [!NOTE]
> Hola **-forzar** conmutador puede ser el mensaje de confirmación de toosuppress usado Hola remove.

se ha quitado tooverify que Hola servicio, puede usar hello `Get-AzureRmApplicationGateway` cmdlet. Este paso no es necesario.

```powershell
Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
```

## <a name="next-steps"></a>Pasos siguientes

Si desea que tooconfigure la descarga de SSL, consulte [configurar una puerta de enlace de la aplicación para la descarga SSL](application-gateway-ssl.md).

Si desea tooconfigure una toouse de puerta de enlace de la aplicación con un ILB, vea [crear una puerta de enlace de la aplicación con un equilibrador de carga interno (ILB)](application-gateway-ilb.md).

Si desea obtener más información acerca de opciones de equilibrio de carga en general, vea:

* [Equilibrador de carga de Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

