---
title: "Configuración de SSL de extremo a extremo con Azure Application Gateway | Microsoft Docs"
description: "En este artículo se describe cómo configurar SSL de extremo a extremo con Application Gateway mediante PowerShell para Azure Resource Manager"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: e6d80a33-4047-4538-8c83-e88876c8834e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: 6d969d6a0c649c263e1d5bb99bdbceec484cb9a3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="configure-end-to-end-ssl-with-application-gateway-using-powershell"></a>Configuración de SSL de extremo a extremo con Application Gateway mediante PowerShell

## <a name="overview"></a>Información general

Application Gateway admite el cifrado de extremo a extremo del tráfico. Para ello, lo que hace es terminar la conexión SSL en la puerta de enlace de aplicaciones. La puerta de enlace aplica entonces las reglas de enrutamiento al tráfico, vuelve a cifrar el paquete y lo reenvía al back-end adecuado según las reglas de enrutamiento definidas. Cualquier respuesta del servidor web pasa por el mismo proceso en su regreso al usuario final.

Otra característica que admite Application Gateway es la definición de opciones SSL personalizadas. Application Gateway admite deshabilitar la siguiente versión de protocolo; **TLSv1.0**, **TLSv1.1**, y **TLSv1.2** así como definir qué conjuntos de cifrado usar y el orden de preferencia.  Para más información sobre las opciones configurables de SSL, visite la [introducción a la directiva SSL](application-gateway-SSL-policy-overview.md).

> [!NOTE]
> SSL 2.0 y SSL 3.0 están deshabilitados de manera predeterminada y no se pueden habilitar. Se considera que no son seguros y no se pueden usar con Application Gateway.

![imagen de escenario][scenario]

## <a name="scenario"></a>Escenario

En este escenario, aprenderá a crear una puerta de enlace de aplicaciones mediante SSL de extremo a extremo con PowerShell.

En este escenario:

* Creará un grupo de recursos llamado **appgw-rg**.
* Creará una red virtual denominada **appgwvnet** con un espacio de direcciones de 10.0.0.0/16.
* Creará dos subredes llamadas **appgwsubnet** y **appsubnet**.
* Creará una puerta de enlace de aplicaciones pequeña que admite el cifrado SSL de extremo a extremo que limita las versiones de protocolos SSL y los conjuntos de cifrado.

## <a name="before-you-begin"></a>Antes de empezar

Para configurar SSL de extremo a extremo con una puerta de enlace de aplicaciones, hacen falta certificados para la puerta de enlace y los servidores back-end. El certificado de la puerta de enlace se usa para cifrar y descifrar el tráfico que se le envía mediante SSL. El certificado de puerta de enlace debe estar en formato de Intercambio de información personal (.pfx). Este formato de archivo permite la exportación de la clave privada, necesaria para que la puerta de enlace de aplicaciones realice el cifrado y descifrado del tráfico.

Para el cifrado SSL de extremo a extremo, el back-end debe estar en la lista de permitidos junto con la puerta de enlace de aplicaciones. Para ello, se carga el certificado público de los back-ends en la puerta de enlace de aplicaciones. Así se garantiza que la puerta de enlace de aplicaciones solo se comunica con instancias de back-end conocidas, lo que protege aún más la comunicación de un extremo a otro.

Este proceso se describe en los pasos siguientes:

## <a name="create-the-resource-group"></a>Crear el grupo de recursos

Esta sección le lleva por la creación de un grupo de recursos que contiene la puerta de enlace de aplicaciones.

### <a name="step-1"></a>Paso 1

Inicie sesión en la cuenta de Azure.

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>Paso 2

Seleccione la suscripción que se usará en este escenario.

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a>Paso 3

Cree un grupo de recursos (omita este paso si usa uno existente).

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a>Creación de una red virtual y una subred para la puerta de enlace de aplicaciones

En el ejemplo siguiente se crea una red virtual y dos subredes. Una subred se usa para alojar la puerta de enlace de aplicaciones. La otra se usa para los back-ends que hospedan la aplicación web.

### <a name="step-1"></a>Paso 1

Asigne un intervalo de direcciones para la subred de la puerta de enlace de aplicaciones propiamente dicha.

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> Las subredes configuradas para la puerta de enlace de aplicaciones deben tener el tamaño correcto. Las puertas de enlace de aplicaciones se puede configurar para un máximo de diez instancias. Cada instancia toma una dirección IP de la subred. Una subred demasiado pequeña puede afectar negativamente el escalado horizontal de una puerta de enlace de aplicaciones.
> 
> 

### <a name="step-2"></a>Paso 2

Asigne un intervalo de direcciones para el grupo de direcciones de back-end.

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a>Paso 3

Cree una red virtual con las subredes definidas en los pasos anteriores.

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a>Paso 4

Recupere el recurso de red virtual y los recursos de subred que se usarán en los pasos siguientes:

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a>Creación de una dirección IP pública para la configuración del front-end

Cree un recurso de IP pública para la puerta de enlace de aplicaciones. Esta dirección IP pública se usa en un paso posterior.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> Application Gateway no admite el uso de una dirección IP pública creada con una etiqueta de dominio definida. Solo se admite una dirección IP pública con una etiqueta de dominio creada dinámicamente. Si necesita un nombre DNS descriptivo para la puerta de enlace de aplicaciones, se recomienda usar un registro CNAME como alias.

## <a name="create-an-application-gateway-configuration-object"></a>Creación de un objeto de configuración de la Puerta de enlace de aplicaciones

Se deben establecer todos los elementos de configuración antes de crear la puerta de enlace de aplicaciones. En los pasos siguientes, se crean los elementos de configuración necesarios para un recurso de puerta de enlace de aplicaciones.

### <a name="step-1"></a>Paso 1

Cree una configuración de IP de puerta de enlace de aplicaciones. Esta configuración determina la subred que usará Application Gateway. Cuando se inicia Application Gateway, elige una dirección IP de la subred configurada y redirige el tráfico de red a las direcciones IP en el grupo IP de back-end. Tenga en cuenta que cada instancia toma una dirección IP.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a>Paso 2

Cree una configuración IP de front-end. Esta configuración asigna una dirección IP pública o privada al front-end de la puerta de enlace de aplicaciones. El paso siguiente asocia la dirección IP pública del paso anterior con la configuración IP de front-end.

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a>Paso 3

Configure el grupo de direcciones IP de back-end con las direcciones IP de los servidores web de back-end. Estas direcciones IP son las direcciones que reciben el tráfico de red procedente del punto de conexión de la IP del front-end. Reemplazará las siguientes direcciones IP para agregar sus propios puntos de conexión de dirección IP de la aplicación.

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> Un nombre de dominio completo (FQDN) es también un valor válido, en lugar de una dirección IP, para los servidores back-end mediante el modificador -BackendFqdns. 

### <a name="step-4"></a>Paso 4

Configure el puerto IP de front-end para el punto de conexión de IP pública. Este puerto es el puerto al que se conectan los usuarios finales.

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a>Paso 5

Configure el certificado de la puerta de enlace de aplicaciones. Este certificado se usa para descifrar y volver a cifrar el tráfico de la puerta de enlace de aplicaciones.

```powershell
$cert = New-AzureRmApplicationGatewaySSLCertificate -Name cert01 -CertificateFile <full path to .pfx file> -Password <password for certificate file>
```

> [!NOTE]
> En este ejemplo se configura el certificado que se usa para la conexión SSL. Es preciso que el certificado tenga el formato .pfx y que la contraseña tenga entre 4 y 12 caracteres.

### <a name="step-6"></a>Paso 6

Cree el agente de escucha HTTP para la puerta de enlace de aplicaciones. Asigne la configuración IP de front-end, el puerto y el certificado SSL que se usarán.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SSLCertificate $cert
```

### <a name="step-7"></a>Paso 7

Cargue el certificado que se usará en los recursos del grupo de back-end habilitado para SSL.

> [!NOTE]
> El sondeo predeterminado obtiene la clave pública del enlace SSL **predeterminado** en la dirección IP del back-end y compara el valor de la clave pública que recibe con el valor de la clave pública que se proporciona aquí. Es posible que la clave pública recuperada no sea necesariamente el sitio previsto al que el tráfico fluirá **si** se usan encabezados de host y SNI en el back-end. En caso de duda, visite https://127.0.0.1/ en los back-ends para confirmar qué certificado se usa para el enlace SSL **predeterminado**. Utilice la clave pública de dicha solicitud en esta sección. Si usa encabezados de host y SNI en enlaces HTTPS y no recibe una respuesta y un certificado de una solicitud manual de un explorador a https://127.0.0.1/ en los back-ends, debe configurar un enlace SSL de forma predeterminada en los back-ends. Si no lo hace, se producirán errores en los sondeos y el back-end no estará en la lista de permitidos.

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> El certificado proporcionado en este paso debe ser la clave pública del certificado pfx presente en el back-end. Exporte el certificado (no el certificado raíz) instalado en el servidor backend en formato .CER y utilícelo en este paso. En este paso se coloca el back-end en la lista de permitidos con la puerta de enlace de aplicaciones.

### <a name="step-8"></a>Paso 8

Configure los valores HTTP de back-end de la puerta de enlace de aplicaciones. Asigne el certificado cargado en el paso anterior a la configuración HTTP.

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a>Paso 9:

Cree una regla de enrutamiento del equilibrador de carga que configure el comportamiento del equilibrador de carga. En este ejemplo, se crea una regla básica de operaciones por turnos.

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a>Paso 10

Configure el tamaño de la instancia de la puerta de enlace de aplicaciones.  Los tamaños disponibles son **Standard\_Small**, **Standard\_Medium** y **Standard\_Large**.  Para la capacidad, los valores disponibles son de 1 a 10.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> Para las pruebas se puede elegir 1 en Número de instancias. Es importante saber que el SLA no cubre ningún número de instancias que esté por debajo de las dos instancias y, por consiguiente, no se recomienda. Las puertas de enlace pequeñas se deben usar para pruebas de desarrollo, no con fines de producción.

### <a name="step-11"></a>Paso 11

Configure la directiva SSL que se usará en la puerta de enlace de aplicaciones. Application Gateway admite la posibilidad de establecer una versión mínima para las versiones del protocolo SSL.

Los valores siguientes son una lista de versiones de protocolo que se pueden definir.

* **TLSv1_0**
* **TLSv1_1**
* **TLSv1_2**

Establece la versión mínima del protocolo en **TLSv1_2** y solo habilita **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384** y solo **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256**.

```powershell
$SSLPolicy = New-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-the-application-gateway"></a>Creación de Application Gateway

Con todos los pasos anteriores, cree la puerta de enlace de aplicaciones. La creación de la puerta de enlace de aplicaciones es un proceso de ejecución largo.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SSLCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SSLPolicy $SSLPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="limit-ssl-protocol-versions-on-an-existing-application-gateway"></a>Límite de las versiones de protocolo SSL en una instancia de Application Gateway existente

Los pasos anteriores le llevan por la creación de una aplicación con SSL de extremo a extremo y la deshabilitación de determinadas versiones del protocolo SSL. En el ejemplo siguiente se deshabilitan determinadas directivas SSL en una puerta de enlace de aplicaciones existente.

### <a name="step-1"></a>Paso 1

Recupere la puerta de enlace de aplicaciones que se actualizará.

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a>Paso 2

Defina una directiva SSL. En el ejemplo siguiente, se deshabilitan TLSv1.0 y TLSv1.1 y los conjuntos de cifrado **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384** y **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** son los únicos permitidos.

```powershell
Set-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion -PolicyType Custom -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256" -ApplicationGateway $gw

```

### <a name="step-3"></a>Paso 3

Por último, actualice la puerta de enlace. Es importante tener en cuenta que este último paso es una tarea de ejecución prolongada. Una vez terminado, SSL de extremo a extremo está configurado en la puerta de enlace de aplicaciones.

```powershell
$gw | Set-AzureRmApplicationGateway
```

## <a name="get-application-gateway-dns-name"></a>Obtención del nombre DNS de una puerta de enlace de aplicaciones

Una vez creada la puerta de enlace, el siguiente paso es configurar el front-end para la comunicación. Cuando se utiliza una dirección IP pública, la puerta de enlace de aplicaciones requiere un nombre DNS asignado dinámicamente, que no es descriptivo. Para asegurarse de que los usuarios finales puedan llegar a la Application Gateway, se puede utilizar un registro CNAME para que apunte al punto de conexión público de la Application Gateway. [Configuración de un nombre de dominio personalizado en Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). Para ello, recupere los detalles de la puerta de enlace de aplicaciones y su nombre DNS o IP asociados mediante el elemento PublicIPAddress asociado a la puerta de enlace de aplicaciones. El nombre DNS de la puerta de enlace de aplicaciones se debe utilizar para crear un registro CNAME, que apunta las dos aplicaciones web a este nombre DNS. No se recomienda el uso de registros A, ya que la VIP puede cambiar al reiniciarse la puerta de enlace de aplicaciones.

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

Aprenda sobre la protección de la seguridad de las aplicaciones web con el firewall de aplicaciones web mediante Application Gateway en [Información general sobre el firewall de aplicaciones web](application-gateway-webapplicationfirewall-overview.md)

[scenario]: ./media/application-gateway-end-to-end-SSL-powershell/scenario.png
