---
title: la descarga de SSL aaaConfigure - puerta de enlace de aplicaciones de Azure - PowerShell | Documentos de Microsoft
description: "Esta página proporciona toocreate instrucciones la descarga de una puerta de enlace de la aplicación con SSL con el Administrador de recursos de Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 3c3681e0-f928-4682-9d97-567f8e278e13
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: c2855d8d3caaa97ec05475c67ff0f8dce72ef2a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a>Configuración de una puerta de enlace de aplicaciones para la descarga SSL mediante Azure Resource Manager

> [!div class="op_single_selector"]
> * [Portal de Azure](application-gateway-ssl-portal.md)
> * [PowerShell del Administrador de recursos de Azure](application-gateway-ssl-arm.md)
> * [Azure Classic PowerShell](application-gateway-ssl.md)
> * [CLI de Azure 2.0](application-gateway-ssl-cli.md)

Puerta de enlace de aplicación de Azure puede ser configurado tooterminate Hola Secure Sockets Layer (SSL) sesión en hello puerta de enlace tooavoid costoso SSL descifrado tareas toohappen en la granja de servidores de hello web. Descarga SSL también simplifica la administración de aplicación web de Hola y el programa de instalación del servidor front-end de Hola.

## <a name="before-you-begin"></a>Antes de empezar

1. Instalar versión más reciente de Hola de cmdlets de PowerShell de Azure de hello mediante Hola instalador de plataforma Web. Puede descargar e instalar la versión más reciente de Hola de hello **Windows PowerShell** sección de hello [página de descargas](https://azure.microsoft.com/downloads/).
2. Crear una red virtual y una subred de puerta de enlace de aplicación Hola. Asegúrese de que no hay máquinas virtuales o las implementaciones de nube están usando la subred de Hola. La puerta de enlace de aplicaciones debe encontrarse en una subred de una red virtual.
3. deben existir servidores Hola configurar puerta de enlace de aplicaciones de toouse Hola o han creado sus puntos de conexión de red virtual de Hola o con una dirección IP pública/VIP asignada.

## <a name="what-is-required-toocreate-an-application-gateway"></a>¿Qué es necesario toocreate una puerta de enlace de la aplicación?

* **Grupo de servidores de back-end:** Hola lista de direcciones IP de servidores de back-end de Hola. direcciones IP en Hello lista deben pertenecer o subred de red virtual toohello o deben ser una dirección IP pública/VIP.
* **Configuración del grupo de servidores back-end:** cada grupo tiene una configuración en la que se incluye el puerto, el protocolo y la afinidad basada en cookies. Esta configuración está ligada tooa grupo y son servidores de tooall aplicados en el grupo de Hola.
* **Puerto front-end:** este puerto es Hola pública que se abre en la puerta de enlace de aplicaciones de Hola. Tráfico llega a este puerto y, a continuación, obtiene redirigido tooone de servidores de back-end de Hola.
* **Agente de escucha:** agente de escucha de hello tiene un puerto front-end, un protocolo (Http o Https, estos valores distinguen mayúsculas de minúsculas) y el nombre del certificado SSL hello (si se descarga la configuración de SSL).
* **Regla:** regla Hola enlaza el agente de escucha de Hola y el grupo de servidores de back-end de Hola y define qué tráfico de Hola de grupo de servidor back-end debe ser dirigido toowhen llega a un agente de escucha determinado. Actualmente, solo Hola *básico* se admite la regla. Hola *básica* regla es la distribución de carga round robin.

**Notas de configuración adicionales**

Para la configuración de certificados SSL, Hola protocolo en **HttpListener** debe cambiar también*Https* (con distinción entre mayúsculas y minúsculas). Hola **SslCertificate** elemento se agrega demasiado**HttpListener** con valor de la variable Hola configurado para el certificado SSL de Hola. puerto front-end de Hello deben too443 actualizada.

**tooenable basado en cookies afinidad**: una puerta de enlace de la aplicación puede ser configurado tooensure que una solicitud de una sesión de cliente siempre está dirigido toohello misma máquina virtual en la granja de servidores de hello web. Este escenario se realiza mediante la inyección de una cookie de sesión que permita el tráfico de toodirect de puerta de enlace de hello adecuadamente. establece la afinidad basado en cookies tooenable, **CookieBasedAffinity** demasiado*habilitado* en hello **BackendHttpSettings** elemento.

## <a name="create-an-application-gateway"></a>Creación de una puerta de enlace de aplicaciones

diferencia de Hello entre utilizar el modelo de implementación de Azure clásico de Hola y el Administrador de recursos de Azure es orden de Hola que creas un elementos de hello y puerta de enlace de aplicaciones que requieren toobe configurado.

Con el Administrador de recursos, todos los componentes de una puerta de enlace de aplicaciones se configuran individualmente y, a continuación, colocar junto toocreate un recurso de puerta de enlace de la aplicación.

Estos es Hola pasos necesarios toocreate una puerta de enlace de la aplicación:

1. Creación de un grupo de recursos para el Administrador de recursos
2. Crear red virtual, subred y dirección IP pública para puerta de enlace de aplicación Hola
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

Cree un grupo de recursos (omita este paso si usa uno existente).

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

Azure Resource Manager requiere que todos los grupos de recursos especifiquen una ubicación. Esta configuración se utiliza como ubicación predeterminada de Hola para recursos de ese grupo de recursos. Asegúrese de que todos los toocreate de comandos utiliza una puerta de enlace de la aplicación Hola mismo grupo de recursos.

En el ejemplo de Hola anterior, hemos creado un grupo de recursos denominado **appgw RG** y la ubicación **West US**.

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Crear una red virtual y una subred de puerta de enlace de aplicación Hola

Hola siguiente ejemplo se muestra cómo toocreate una red virtual mediante el Administrador de recursos:

### <a name="step-1"></a>Paso 1

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

Este ejemplo asigna Hola dirección intervalo 10.0.0.0/24 tooa subred toobe variable utiliza toocreate una red virtual.

### <a name="step-2"></a>Paso 2

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

Este ejemplo crea una red virtual denominada **appgwvnet** en grupo de recursos **appgw rg** de región de oeste de Estados Unidos de hello con hello prefijo 10.0.0.0/16 subred 10.0.0.0/24.

### <a name="step-3"></a>Paso 3

```powershell
$subnet = $vnet.Subnets[0]
```

Este ejemplo asigna Hola subred objeto toovariable $subnet para obtener instrucciones de Hola.

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Crear una dirección IP pública para la configuración de front-end de Hola

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

Este ejemplo crea un recurso IP público **publicIP01** en grupo de recursos **appgw rg** de región del oeste de Estados Unidos de Hola.

## <a name="create-an-application-gateway-configuration-object"></a>Creación de un objeto de configuración de la Puerta de enlace de aplicaciones

### <a name="step-1"></a>Paso 1

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

En este ejemplo se crea una configuración de la IP de la puerta de enlace de aplicaciones denominada **gatewayIP01**. Cuando se inicia la puerta de enlace de aplicaciones, toma una dirección IP de subred Hola configurado y enrutar las direcciones IP de toohello de tráfico de red en el grupo de direcciones IP de back-end de Hola. Tenga en cuenta que cada instancia toma una dirección IP.

### <a name="step-2"></a>Paso 2

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

Este ejemplo configura el grupo de direcciones IP Hola back-end denominado **pool01** con direcciones IP **134.170.185.46**, **134.170.188.221**, **134.170.185.50** . Esos valores son direcciones IP de Hola que reciben tráfico de red de Hola que provienen de extremo IP de front-end de Hola. Reemplazar las direcciones IP Hola Hola anterior ejemplo con direcciones IP de Hola de los extremos de la aplicación web.

### <a name="step-3"></a>Paso 3

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

Este ejemplo configura la configuración de puerta de enlace de aplicaciones **poolsetting01** tooload equilibrada de tráfico de red en el grupo de back-end de Hola.

### <a name="step-4"></a>Paso 4

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

Este ejemplo configura el puerto IP front-end Hola denominado **frontendport01** para punto de conexión IP pública Hola.

### <a name="step-5"></a>Paso 5

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

Este ejemplo configura el certificado de hello usado para la conexión SSL. certificado de Hello debe toobe en formato .pfx y Hola contraseña debe tener entre 4 too12 caracteres.

### <a name="step-6"></a>Paso 6

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

Este ejemplo crea la configuración de IP front-end de hello denominado **fipconfig01** y asocia Hola la dirección IP pública con la configuración de IP de front-end de Hola.

### <a name="step-7"></a>Paso 7

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

Este ejemplo crea el nombre de agente de escucha de hello **listener01** y asocia Hola configuración de IP de front-end de puerto front-end toohello y el certificado.

### <a name="step-8"></a>Paso 8

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

Este ejemplo crea Hola regla equilibrador de carga enrutamiento denominado **rule01** que configura el comportamiento de equilibrador de carga de Hola.

### <a name="step-9"></a>Paso 9:

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

Este ejemplo configura el tamaño de la instancia de puerta de enlace de aplicación Hola Hola.

> [!NOTE]
> Hola valor predeterminado de *InstanceCount* es 2, con un valor máximo de 10. Hola valor predeterminado de *GatewaySize* es Medium. Se puede elegir entre Standard_Small, Standard_Medium y Standard_Large.

### <a name="step-10"></a>Paso 10

```powershell
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
```

Este paso define en puerta de enlace de aplicación Hola Hola SSL directiva toouse. Visite [versiones de directivas de configurar SSL y conjuntos de cifrado en la puerta de enlace de aplicaciones](application-gateway-configure-ssl-policy-powershell.md) toolearn más.

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a>Creación de una puerta de enlace de aplicaciones con New-AzureApplicationGateway

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

Este ejemplo crea una puerta de enlace de la aplicación con todos los elementos de configuración de hello pasos anteriores. En el ejemplo de Hola, se denomina puerta de enlace de aplicaciones de hello **appgwtest**.

## <a name="get-application-gateway-dns-name"></a>Obtención del nombre DNS de una puerta de enlace de aplicaciones

Una vez creada la puerta de enlace de hello, Hola siguiente paso es front-end de Hola de tooconfigure para la comunicación. Cuando se utiliza una dirección IP pública, la puerta de enlace de aplicaciones requiere un nombre DNS asignado dinámicamente, que no es descriptivo. los usuarios finales de tooensure puede llegar a puerta de enlace de aplicaciones de hello, un registro CNAME puede ser usado toopoint toohello extremo público de puerta de enlace de aplicación Hola. [Configuración de un nombre de dominio personalizado en Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). toodo, detalles de recuperación de puerta de enlace de aplicaciones de Hola y su nombre IP/DNS asociado con puerta de enlace de hello PublicIPAddress elemento adjunto toohello aplicación. nombre DNS de Hello aplicación la puerta de enlace debe ser toocreate usa un registro CNAME, qué nombre DNS puntos Hola dos web aplicaciones toothis. no se recomienda el uso de Hola de registros de un puesto que puede cambiar Hola VIP en el reinicio de puerta de enlace de aplicaciones.


```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : appgw-RG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/applicationGateways/appgwtest/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="next-steps"></a>Pasos siguientes

Si desea tooconfigure una toouse de puerta de enlace de la aplicación con un equilibrador de carga interno (ILB), consulte [crear una puerta de enlace de la aplicación con un equilibrador de carga interno (ILB)](application-gateway-ilb.md).

Si desea obtener más información acerca de opciones de equilibrio de carga en general, vea:

* [Equilibrador de carga de Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

