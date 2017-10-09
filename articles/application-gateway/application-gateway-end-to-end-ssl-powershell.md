---
title: aaaConfigure final tooend SSL con la puerta de enlace de aplicaciones de Azure | Documentos de Microsoft
description: "Este artículo describe cómo tooconfigure finalizar tooend SSL con la puerta de enlace de aplicaciones con el Administrador de recursos de Azure PowerShell"
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
ms.openlocfilehash: 7c280478e143d309e7665219441cbee8c81d9a80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-end-tooend-ssl-with-application-gateway-using-powershell"></a>Configurar final tooend SSL con la puerta de enlace de aplicaciones con PowerShell

## <a name="overview"></a>Información general

Admite aplicaciones de puerta de enlace finaliza tooend cifrado de tráfico. Puerta de enlace de aplicación lo hace al terminar la conexión de SSL de hello en la puerta de enlace de aplicaciones de Hola. puerta de enlace de Hello, a continuación, aplica reglas de enrutamiento de hello toohello tráfico, vuelve a cifrar el paquete de saludo y reenvía Hola paquete toohello adecuado back-end basado en reglas de enrutamiento de hello definidas. Las posibles respuestas del servidor web de hello atraviesa Hola mismo proceso de usuario de toohello back-end.

Otra característica que admite Application Gateway es la definición de opciones SSL personalizadas. Puerta de enlace de aplicaciones admite Hola deshabilitar después de la versión de protocolo; **TLSv1.0**, **TLSv1.1**, y **TLSv1.2** también definir hello que conjuntos toouse y Hola el orden de preferencia de cifrado.  toolearn más información acerca de opciones configurables de SSL, visite [Introducción a la directiva de SSL](application-gateway-SSL-policy-overview.md).

> [!NOTE]
> SSL 2.0 y SSL 3.0 están deshabilitados de manera predeterminada y no se pueden habilitar. Se consideran no seguras y no están toobe puede usar con la puerta de enlace de aplicaciones.

![imagen de escenario][scenario]

## <a name="scenario"></a>Escenario

En este escenario, aprenderá cómo toocreate una puerta de enlace de aplicaciones con finalizar tooend SSL mediante PowerShell.

En este escenario:

* Creará un grupo de recursos llamado **appgw-rg**.
* Creará una red virtual denominada **appgwvnet** con un espacio de direcciones de 10.0.0.0/16.
* Creará dos subredes llamadas **appgwsubnet** y **appsubnet**.
* Crear un pequeña aplicación puerta de enlace auxiliares final tooend cifrado SSL que las versiones de protocolos SSL de límites y los conjuntos de cifrado.

## <a name="before-you-begin"></a>Antes de empezar

tooconfigure final tooend SSL con una puerta de enlace de la aplicación, un certificado es necesario para la puerta de enlace de Hola y se necesitan certificados para servidores de back-end de Hola. certificado de puerta de enlace de Hello es usado tooencrypt y descifrar Hola el tráfico enviado tooit mediante SSL. certificado de puerta de enlace de Hello debe toobe en formato de intercambio de información Personal (pfx). Este formato de archivo permite Hola privada toobe clave exportado que requiere Hola aplicación puerta de enlace tooperform Hola cifrado y descifrado de tráfico.

Para final tooend SSL cifrado Hola back-end debe ser la lista de permitidos con puerta de enlace de aplicaciones. Para ello, cargar certificado público de Hola de puerta de enlace de hello back-ends toohello aplicación. Esto garantiza que esa puerta de enlace de la aplicación hello sólo se comunica con instancias de conocidos back-end. Esto protege aún más comunicación tooend de hello final.

Este proceso se describe en hello pasos:

## <a name="create-hello-resource-group"></a>Crear grupo de recursos de hello

Esta sección explica cómo crear un grupo de recursos, que contiene la puerta de enlace de aplicaciones de Hola.

### <a name="step-1"></a>Paso 1

Inicie sesión en tooyour cuenta de Azure.

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>Paso 2

Seleccione hello toouse de suscripción para este escenario.

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a>Paso 3

Cree un grupo de recursos (omita este paso si usa uno existente).

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Crear una red virtual y una subred de puerta de enlace de aplicación Hola

Hello en el ejemplo siguiente se crea una red virtual y dos subredes. Una subred es la puerta de enlace de aplicaciones de uso toohold Hola. Hola se usa otra subred para aplicación de web de hospedaje de back-ends de Hola Hola.

### <a name="step-1"></a>Paso 1

Asignar un intervalo de direcciones de subred de hello usará para hello aplicación puerta de enlace.

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> Las subredes configuradas para la puerta de enlace de aplicaciones deben tener el tamaño correcto. Una puerta de enlace de aplicaciones puede configurarse para instancias de too10. Cada instancia tiene una dirección IP de subred Hola. Una subred demasiado pequeña puede afectar negativamente el escalado horizontal de una puerta de enlace de aplicaciones.
> 
> 

### <a name="step-2"></a>Paso 2

Asignar un toobe de intervalo de direcciones utilizado para el grupo de direcciones de back-end de Hola.

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a>Paso 3

Crear una red virtual con subredes Hola definidos en hello pasos anteriores.

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a>Paso 4

Recuperar Hola red virtual recursos y subred recursos toobe usa Hola pasos:

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Crear una dirección IP pública para la configuración de front-end de Hola

Crear un toobe de recurso IP pública utilizado para la puerta de enlace de aplicación Hola. Esta dirección IP pública se usa en un paso posterior.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> Puerta de enlace de aplicaciones no admite el uso de Hola de una dirección IP pública que se creó con una etiqueta de dominio definida. Solo se admite una dirección IP pública con una etiqueta de dominio creada dinámicamente. Si necesita un nombre descriptivo de dns para puerta de enlace de aplicaciones de hello, se recomienda toouse un CNAME se registre como un alias.

## <a name="create-an-application-gateway-configuration-object"></a>Creación de un objeto de configuración de la Puerta de enlace de aplicaciones

Todos los elementos de configuración se establecen antes de crear la puerta de enlace de aplicaciones de Hola. Hello pasos siguientes crean Hola elementos de configuración que son necesarios para un recurso de puerta de enlace de la aplicación.

### <a name="step-1"></a>Paso 1

Crear una configuración de IP de puerta de enlace de aplicaciones, esta configuración define qué aplicación de puerta de enlace de subred hello usa. Cuando se inicia la puerta de enlace de aplicaciones, toma una dirección IP de subred Hola configurado y enruta las direcciones IP de toohello de tráfico de red en el grupo de direcciones IP de back-end de Hola. Tenga en cuenta que cada instancia toma una dirección IP.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a>Paso 2

Crear una configuración de IP de front-end, esta configuración asigna un ip pública o privada dirección toohello front-end de puerta de enlace de aplicación Hola. Hola siguiendo el paso asocia la dirección IP pública de Hola Hola anterior paso con la configuración de IP de front-end de Hola.

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a>Paso 3

Configurar grupo de direcciones IP de hello back-end con las direcciones IP de servidores web de back-end de Hola Hola. Estas direcciones IP son direcciones IP de Hola que reciben tráfico de red de Hola que provienen de extremo IP de front-end de Hola. Reemplace Hola después tooadd de direcciones IP de sus propios extremos de dirección IP de aplicación.

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> Un nombre de dominio completo (FQDN) también es un valor válido en lugar de una dirección ip para servidores de back-end de hello mediante hello - BackendFqdns conmutador. 

### <a name="step-4"></a>Paso 4

Configurar puerto IP front-end de hello para el punto de conexión IP pública Hola. Este puerto es Hola que se conectan a los usuarios finales a.

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a>Paso 5

Configurar certificado de Hola para puerta de enlace de aplicaciones de Hola. Este certificado es toodecrypt usado y volver a cifrar el tráfico de hello en puerta de enlace de aplicación Hola.

```powershell
$cert = New-AzureRmApplicationGatewaySSLCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

> [!NOTE]
> Este ejemplo configura el certificado de hello usado para la conexión SSL. certificado de Hello debe toobe en formato .pfx y Hola contraseña debe tener entre 4 too12 caracteres.

### <a name="step-6"></a>Paso 6

Crear Agente de escucha HTTP de Hola para puerta de enlace de aplicación Hola. Asignar la configuración de ip de front-end de hello, puerto y toouse del certificado SSL.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SSLCertificate $cert
```

### <a name="step-7"></a>Paso 7

Cargar certificado de hello toobe usado en hello SSL habilitado recursos del grupo back-end.

> [!NOTE]
> sondeo de Hello predeterminado Obtiene la clave pública de Hola de hello **predeterminado** enlace SSL dirección IP de Hola back-end de y compara Hola valor de clave pública que recibe el valor de clave pública toohello que proporciona aquí. Hello recuperado clave pública no será necesariamente flujos de tráfico de hello pensado sitio toowhich **si** usa encabezados de host y SNI en hello back-end. En caso de duda, visite https://127.0.0.1/ en tooconfirm de back-end de hello qué certificado se usa para hello **predeterminado** enlace SSL. Use una clave pública Hola desde esa solicitud de esta sección. Si usa encabezados de host y SNI en enlaces HTTPS y no recibe una respuesta y un certificado desde un explorador manual solicitud toohttps://127.0.0.1/ en hello back-end, debe configurar un enlace de SSL predeterminado en hello back-end. Si no lo hace, producirá un error de sondeos y Hola back-end no está permitido.

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> certificado de Hello proporcionado en este paso debe ser clave pública de Hola de certificados pfx de hello presente en hello back-end. Exporte el certificado de hello (no el certificado de raíz hello) instalado en el servidor de back-end de hello en. CER formatear y usar en este paso. Este paso, las listas blancas Hola back-end con puerta de enlace de aplicación Hola.

### <a name="step-8"></a>Paso 8

Definir la configuración de http de back-end de puerta de enlace de aplicación Hola. Asignar certificado Hola cargado en hello anterior paso toohello http configuración.

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a>Paso 9:

Crear una regla de enrutamiento de equilibrador de carga que configura el comportamiento de equilibrador de carga de Hola. En este ejemplo, se crea una regla básica de operaciones por turnos.

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a>Paso 10

Configurar el tamaño de la instancia de puerta de enlace de aplicación Hola Hola.  los tamaños disponibles de Hello son **estándar\_pequeño**, **estándar\_medio**, y **estándar\_grande**.  La capacidad, los valores disponibles de hello van de 1 a 10.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> Para las pruebas se puede elegir 1 en Número de instancias. Es importante tooknow que cualquier instancia de recuento de instancias en dos no está cubierto por hello SLA y, por tanto, se recomienda que no. Las puertas de enlace pequeños son toobe utilizado para pruebas de desarrollo y no para fines de producción.

### <a name="step-11"></a>Paso 11

Configurar Hola SSL directiva toobe usado en hello Application Gateway. Puerta de enlace de aplicaciones admite Hola capacidad tooset una versión mínima de versiones del protocolo SSL.

Hello los valores siguientes son una lista de versiones del protocolo que se pueden definir.

* **TLSv1_0**
* **TLSv1_1**
* **TLSv1_2**

Conjuntos de Hola versión del protocolo mínimo demasiado**TLSv1_2** y permite **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_ SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**y **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** solo.

```powershell
$SSLPolicy = New-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-hello-application-gateway"></a>Crear hello puerta de enlace de aplicaciones

Con hello todos los pasos anteriores, cree Hola Application Gateway. creación de Hello de puerta de enlace de hello es un proceso de ejecución prolongada.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SSLCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SSLPolicy $SSLPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="limit-ssl-protocol-versions-on-an-existing-application-gateway"></a>Límite de las versiones de protocolo SSL en una instancia de Application Gateway existente

Hello pasos anteriores para ir a través de la creación de una aplicación con final tooend SSL y deshabilitar determinadas versiones del protocolo SSL. Hello en el ejemplo siguiente se deshabilita determinadas directivas SSL a una puerta de enlace de la aplicación existente.

### <a name="step-1"></a>Paso 1

Recuperar tooupdate de puerta de enlace de aplicación Hola.

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a>Paso 2

Defina una directiva SSL. En el siguiente ejemplo de Hola, TLSv1.0 y TLSv1.1 están deshabilitados y Hola conjuntos de cifrado **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256** , **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, y  **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** es Hola únicos que permiten.

```powershell
Set-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion -PolicyType Custom -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256" -ApplicationGateway $gw

```

### <a name="step-3"></a>Paso 3

Por último, actualice la puerta de enlace de Hola. Es importante toonote que este último paso es una tarea de ejecución prolongada. Cuando termine, finalizar tooend que SSL está configurado en la puerta de enlace de aplicaciones de Hola.

```powershell
$gw | Set-AzureRmApplicationGateway
```

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

Obtenga información sobre cómo reforzar la seguridad de Hola de las aplicaciones web con el servidor de aplicaciones Web a través de puerta de enlace de aplicaciones visitando [información general sobre el servidor de seguridad de aplicaciones Web](application-gateway-webapplicationfirewall-overview.md)

[scenario]: ./media/application-gateway-end-to-end-SSL-powershell/scenario.png
