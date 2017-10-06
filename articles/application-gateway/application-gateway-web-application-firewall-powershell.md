---
title: "firewall de aplicación web de aaaConfigure: puerta de enlace de aplicaciones de Azure | Documentos de Microsoft"
description: "Este artículo proporciona instrucciones sobre cómo usar toostart web servidor de aplicaciones en una puerta de enlace de aplicación nueva o existente."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 670b9732-874b-43e6-843b-d2585c160982
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: gwallace
ms.openlocfilehash: bd2a69901f0ec0d6551d633e2588b74c3ab59a71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a>Configuración del firewall de aplicaciones web en una puerta de enlace de aplicaciones nueva o existente

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [CLI de Azure](application-gateway-web-application-firewall-cli.md)

Obtenga información acerca de cómo toocreate un servidor de seguridad de la aplicación web habilita la puerta de enlace de aplicaciones o agregar tooan de firewall de aplicación web existente de la puerta de enlace de aplicaciones.

servidor de aplicaciones web Hello (WAFS) en la puerta de enlace de aplicaciones de Azure protege las aplicaciones web de ataques basados en web comunes como la inyección de código SQL, ataques XSS y apropiaciones de sesión.

Azure Application Gateway es un equilibrador de carga de nivel 7. Proporciona conmutación por error, enrutamiento de rendimiento de las solicitudes HTTP entre diferentes servidores, independientemente de si están en la nube de Hola o de forma local. Application Gateway proporciona numerosas características del controlador de entrega de aplicaciones (ADC), entre las que se incluyen el equilibrio de carga HTTP, la afinidad de sesiones basada en cookies, la descarga SSL (Capa de sockets seguros), los sondeos personalizados sobre el estado, la compatibilidad con multisitio, y muchas más. toofind una lista completa de las características admitidas, visite: [información general de Application Gateway](application-gateway-introduction.md).

Hello siguiente artículo se muestra cómo demasiado[agregar tooan de firewall de aplicación web existente de la puerta de enlace de aplicaciones](#add-web-application-firewall-to-an-existing-application-gateway) y [crear una puerta de enlace de la aplicación que utiliza el servidor de aplicaciones web](#create-an-application-gateway-with-web-application-firewall).

![imagen de escenario][scenario]

## <a name="waf-configuration-differences"></a>Diferencias de configuración de WAF

Si ha leído [crear una puerta de enlace de la aplicación con PowerShell](application-gateway-create-gateway-arm.md), comprender Hola SKU configuración tooconfigure al crear una puerta de enlace de la aplicación. WAFS proporciona toodefine de opciones de configuración adicionales al configurar Hola SKU en una puerta de enlace de la aplicación. No hay ningún otro cambio que realice en hello aplicación puerta de enlace.

| **Configuración** | **Detalles**
|---|---|
|**SKU** |Una instancia de Application Gateway normal sin WAF admite los tamaños **Standard\_Small**, **Standard\_Medium** y **Standard\_Large**. Con la introducción de Hola de WAFS, hay dos SKU adicionales, **WAFS\_medio** y **WAFS\_grande**. No se admite WAF en instancias de Application Gateway de pequeño tamaño.|
|**Nivel** | Hola los valores disponibles son **estándar** o **WAFS**. Cuando se usa el firewall de aplicaciones web, se debe seleccionar **WAF**.|
|**Modo** | Esta opción es modo de saludo de WAFS. Los valores permitidos son **Detección** y **Prevención**. Cuando WAF está configurado en modo de detección, todas las amenazas se almacenan en un archivo de registro. En el modo de prevención, todavía se registran eventos pero atacante Hola recibe una respuesta no autorizado 403 Hola Application Gateway.|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a>Agregar tooan de firewall de aplicación web existente de la puerta de enlace de aplicaciones

Asegúrese de que está utilizando la versión más reciente de Hola de PowerShell de Azure. Hay más información disponible en [Uso de Windows PowerShell con Resource Manager](../powershell-azure-resource-manager.md).

1. Inicie sesión en tooyour cuenta de Azure.

    ```powershell
    Login-AzureRmAccount
    ```

2. Seleccione hello toouse de suscripción para este escenario.

    ```powershell
    Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
    ```

3. Recuperar la puerta de enlace de Hola que va a agregar el servidor de aplicaciones web a.

    ```powershell
    $gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
    ```

1. Configurar la aplicación firewall sku de hello web. los tamaños disponibles de Hello son **WAFS\_grande** y **WAFS\_medio**. Cuando se usa firewall de aplicación web debe ser el nivel de hello **WAFS**, capacidad de Hola se debe confirmar al establecer Hola sku.

    ```powershell
    $gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
    ```

1. Configurar opciones de hello WAFS tal como se define en el siguiente ejemplo de Hola:

   Para **FirewallMode**, valores disponibles de hello son la detección y prevención.

    ```powershell
    $gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
    ```

1. Actualizar Hola puerta de enlace de aplicaciones con valores de hello definidos en hello anterior paso.

    ```powershell
    Set-AzureRmApplicationGateway -ApplicationGateway $gw
    ```

Este comando actualiza Hola puerta de enlace de aplicación con el servidor de aplicaciones web. Visite [diagnóstico de puerta de enlace de aplicaciones](application-gateway-diagnostics.md) toounderstand cómo tooview registros para la puerta de enlace de la aplicación. Debido a toohello la naturaleza de seguridad de WAFS, registros necesidad toobe revisarse periódicamente postura de seguridad de hello toounderstand de las aplicaciones web.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>Creación de una puerta de enlace de aplicaciones con el firewall de aplicaciones web

Hello pasos siguientes le conducen por proceso completo de Hola desde principio tooend para crear una puerta de enlace de la aplicación con el servidor de aplicaciones web.

Asegúrese de que está utilizando la versión más reciente de Hola de PowerShell de Azure. Hay más información disponible en [Uso de Windows PowerShell con Resource Manager](../powershell-azure-resource-manager.md).

1. Inicie sesión en tooAzure ejecutando `Login-AzureRmAccount`, son tooauthenticate solicitada con sus credenciales.

1. Compruebe las suscripciones de hello para la cuenta de hello ejecutando`Get-AzureRmSubscription`

1. Elija qué su toouse de las suscripciones de Azure.

    ```powershell
    Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
    ```

### <a name="create-a-resource-group"></a>Crear un grupo de recursos

Crear un grupo de recursos para hello Application Gateway.

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

Azure Resource Manager requiere que todos los grupos de recursos especifiquen una ubicación. Esta ubicación se utiliza como ubicación predeterminada de Hola para recursos de ese grupo de recursos. Asegúrese de que todos los comandos que utiliza toocreate una puerta de enlace de aplicación Hola mismo grupo de recursos.

En el anterior ejemplo de Hola, hemos creado un grupo de recursos denominado "Appgw-RG" y la ubicación "oeste de Estados Unidos."

> [!NOTE]
> Si necesita tooconfigure un sondeo personalizado para la puerta de enlace de aplicaciones, consulte [crear una puerta de enlace de aplicaciones con sondeos personalizados mediante PowerShell](application-gateway-create-probe-ps.md). Para más información, consulte [Información general sobre la supervisión de estado de la puerta de enlace de aplicaciones](application-gateway-probe-overview.md) .

### <a name="configure-virtual-network"></a>Configuración de una red virtual

Azure Application Gateway requiere su propia subred. En este paso, creará una red virtual con un espacio de direcciones de 10.0.0.0/16 y dos subredes, uno para la puerta de enlace de aplicación hello y otro para los miembros del grupo back-end.

```powershell
# Create a subnet configuration object for hello Application Gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in hello subnet for Application Gateway instances. With a smaller subnet, you may not be able tooadd more instance of your Application Gateway in hello future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for hello backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create hello virtual network with hello previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="configure-public-ip-address"></a>Configuración de direcciones IP públicas

En solicitudes externas de orden toohandle, puerta de enlace de aplicaciones requiere una dirección IP pública. Esta dirección IP pública no debe tener un `DomainNameLabel` definido toobe usa Hola Application Gateway.

```powershell
# Create a public IP address for use with hello Application Gateway. Defining hello domainnamelabel during creation is not supported for use with Application Gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

### <a name="configure-hello-application-gateway"></a>Configurar la puerta de enlace de aplicación Hola

```powershell
# Create a IP configuration. This configures what subnet hello Application Gateway uses. When Application Gateway starts, it picks up an IP address from hello subnet configured and routes network traffic toohello IP addresses in hello back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet

# Create a backend pool toohold hello addresses or NICs for hello application that Application Gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Upload hello authenication certificate that will be used toocommunicate with hello backend servers
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile <full path too.cer file>

# Conifugre hello backend HTTP settings toobe used toodefine how traffic is routed toohello backend pool. hello authenication certificate used in hello previous step is added toohello backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert

# Create a frontend port toobe used by hello listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443

# Create a frontend IP configuration tooassociate hello public IP address with hello Application Gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Configure hello certificate for hello Application Gateway. This certificate is used toodecrypt and re-encrypt hello traffic on hello Application Gateway.
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>

# Create hello HTTP listener for hello Application Gateway. Assign hello front-end ip configuration, port, and ssl certificate toouse.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert

#Create a load balancer routing rule that configures hello load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure hello SKU of hello Application Gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Define hello SSL policy toouse
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S

#Configure hello waf configuration settings.
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"

# Create hello Application Gateway utilizing all hello previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert
```

> [!NOTE]
> Las puertas de enlace de aplicaciones creadas con la configuración del firewall de aplicación de hello web básico se configuran con CRS 3.0 para protección.

## <a name="get-application-gateway-dns-name"></a>Obtención del nombre DNS de una instancia de Application Gateway

Una vez creada la puerta de enlace de hello, Hola siguiente paso es front-end de Hola de tooconfigure para la comunicación. Cuando se utiliza una dirección IP pública, la instancia de Application Gateway requiere un nombre DNS asignado dinámicamente, que no es descriptivo. los usuarios finales de tooensure puede llegar a Hola puerta de enlace de aplicaciones, un registro CNAME puede ser usado toopoint toohello extremo público de hello Application Gateway. [Configuración de un nombre de dominio personalizado en Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). tooconfigure un alias, recuperar los detalles de hello puerta de enlace de aplicaciones y su nombre IP/DNS asociado mediante hello PublicIPAddress elemento adjunta toohello Application Gateway. nombre DNS de Hello aplicación la puerta de enlace debe ser toocreate usa un registro CNAME, qué nombre DNS puntos Hola dos web aplicaciones toothis. no se recomienda el uso de Hola de registros de un puesto que Hola VIP puede cambiar en el reinicio de puerta de enlace de aplicaciones.

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

Obtenga información acerca de cómo tooconfigure el registro de diagnóstico, eventos de hello toolog si se detecta o prevenir con servidor de aplicaciones web visitando [diagnóstico de puerta de enlace de aplicaciones](application-gateway-diagnostics.md)

[scenario]: ./media/application-gateway-web-application-firewall-powershell/scenario.png
