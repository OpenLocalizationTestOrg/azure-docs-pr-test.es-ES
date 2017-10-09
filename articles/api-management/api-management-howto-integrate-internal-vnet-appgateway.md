---
title: "aaaHow toouse administración de API de Azure en red Virtual con la puerta de enlace de aplicaciones | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toosetup y configurar la administración de API de Azure en red Virtual interna con aplicación de puerta de enlace (WAFS) como front-end"
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: antonba
ms.assetid: a8c982b2-bca5-4312-9367-4a0bbc1082b1
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/16/2017
ms.author: sasolank
ms.openlocfilehash: 74303a2ee8a10db633ab1740ec7267728eacb473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-api-management-in-an-internal-vnet-with-application-gateway"></a>Integración de API Management en una red virtual interna con Application Gateway 

##<a name="overview"></a> Información general
 
Hola servicio de administración de API se puede configurar en una red Virtual en modo interno que hace que sea accesible únicamente desde dentro de hello red Virtual. Azure Application Gateway es un servicio de PAAS que proporciona un equilibrador de carga de nivel 7. Actúa como un servicio de proxy inverso y proporciona entre su oferta un firewall de aplicaciones web (WAF).

Combinar aprovisionado en una red virtual interna con front-end de hello puerta de enlace de aplicaciones de administración de API permite Hola los escenarios siguientes:

* Use Hola mismo recurso de administración de API para su uso por los consumidores internos y externo a los consumidores.
* Utilizar un único recurso de API Management y tener definido un subconjunto de API en API Management disponible para los consumidores externos.
* Proporcionar una manera de preparada tooswitch acceso tooAPI administración de hello Internet pública y desactivar. 

##<a name="scenario"></a> Escenario
En este artículo se tratan cómo toouse una única API de administración de servicio para los consumidores tanto internos como externos y hacer que actúe como un único servidor front-end para ambos local y las API en la nube. También verá cómo tooexpose solo un subconjunto de las API (en el ejemplo de Hola que están resaltados en verde) para su uso externo con funcionalidad de PathBasedRouting de hello disponible en la puerta de enlace de aplicaciones.

En el ejemplo de Hola primero el programa de instalación se administran todas las API sólo desde dentro de la red Virtual. Los consumidores internos (resaltados en color naranja) pueden tener acceso a todas las API internas y externas. Tráfico no sale nunca tooInternet que se entrega un alto rendimiento a través de circuitos Expressroute.

![ruta de dirección URL](./media/api-management-howto-integrate-internal-vnet-appgateway/api-management-howto-integrate-internal-vnet-appgateway.png)

## <a name="before-you-begin"></a> Antes de empezar

1. Instalar versión más reciente de Hola de cmdlets de PowerShell de Azure de hello mediante Hola instalador de plataforma Web. Puede descargar e instalar la versión más reciente de Hola de hello **Windows PowerShell** sección de hello [página de descargas](https://azure.microsoft.com/downloads/).
2. Cree una red virtual y subredes independientes para API Management y Application Gateway. 
3. Si tiene previsto toocreate un servidor DNS personalizado para hello red Virtual, debe hacerlo antes de iniciar la implementación de Hola. Vuelve a revisar funciona que garantiza una máquina virtual creada en una subred nueva en hello red Virtual puede resolver y acceder a todos los extremos de servicio de Azure.

## <a name="what-is-required-toocreate-an-integration-between-api-management-and-application-gateway"></a>¿Qué es necesario toocreate una integración entre administración de API y la puerta de enlace de aplicaciones?

* **Grupo de servidores de back-end:** se trata de dirección IP virtual interna del Hola de hello servicio de administración de API.
* **Configuración del grupo de servidores back-end:** cada grupo tiene una configuración en la que se incluye el puerto, el protocolo y la afinidad basada en cookies. Estos valores son servidores tooall aplicados en el grupo de Hola.
* **Puerto front-end:** es Hola puerto público que se abre en la puerta de enlace de aplicaciones de Hola. Tráfico alcanzando obtiene tooone redirigida de hello servidores back-end.
* **Agente de escucha:** agente de escucha de hello tiene un puerto front-end, un protocolo (Http o Https, estos valores distinguen mayúsculas de minúsculas) y el nombre del certificado SSL hello (si se descarga la configuración de SSL).
* **Regla:** regla Hola enlaza un grupo de servidor back-end de tooa de agente de escucha.
* **Sondeo de estado personalizado:** puerta de enlace de la aplicación, de forma predeterminada, usa toofigure de sondeos basados en direcciones IP a qué servidores en hello BackendAddressPool están activas. Hola servicio de administración de API sólo responde toorequests que tienen el encabezado de host correcto de hello, por lo tanto, un error Hola predeterminado sondeos. Un sondeo de estado personalizado necesita toobe definido puerta de enlace de aplicaciones de toohelp determinar que el servicio de Hola esté activo, y deben reenviar las solicitudes.
* **Certificado de dominio personalizado:** tooaccess administración de API de hello necesita toocreate una asignación de CNAME de su nombre DNS front-end de nombre de host toohello puerta de enlace de aplicaciones de internet. Esto garantiza que, encabezado de nombre de host de Hola y el certificado enviado tooApplication puerta de enlace que se reenvía a tooAPI administración sea una que APIM pueda reconocer como válido.

## <a name="overview-steps"></a> Pasos necesarios para integrar API Management y Application Gateway 

1. Cree un grupo de recursos para Resource Manager.
2. Crear una red Virtual, subred y dirección IP pública para hello Application Gateway. Cree otra subred para API Management.
3. Crear un servicio de administración de API dentro de la subred de red virtual de hello creado anteriormente y asegúrese de que se utiliza el modo de hello interno.
4. Configurar nombre de dominio personalizado de Hola Hola servicio de administración de API.
5. Cree un objeto de configuración de Application Gateway.
6. Cree un recurso de Application Gateway.
7. Crear un CNAME de nombre DNS público de hello del nombre del servidor proxy de administración de API de hello Application Gateway toohello.

## <a name="create-a-resource-group-for-resource-manager"></a>Creación de un grupo de recursos para el Administrador de recursos

Asegúrese de que está utilizando la versión más reciente de Hola de PowerShell de Azure. Hay más información disponible en [Uso de Windows PowerShell con Resource Manager](../powershell-azure-resource-manager.md).

### <a name="step-1"></a>Paso 1

Inicie sesión en tooAzure

```powershell
Login-AzureRmAccount
```

Autentíquese con sus credenciales.<BR>

### <a name="step-2"></a>Paso 2

Compruebe las suscripciones de hello para la cuenta de hello y selecciónelo.

```powershell
Get-AzureRmSubscription -Subscriptionid "GUID of subscription" | Select-AzureRmSubscription
```

### <a name="step-3"></a>Paso 3

Cree un grupo de recursos (omita este paso si usa uno existente).

```powershell
New-AzureRmResourceGroup -Name "apim-appGw-RG" -Location "West US"
```
Azure Resource Manager requiere que todos los grupos de recursos especifiquen una ubicación. Esto se utiliza como ubicación predeterminada de Hola para recursos de ese grupo de recursos. Asegúrese de que todos los comandos toocreate un Hola de uso de puerta de enlace de aplicación mismo grupo de recursos.

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Crear una red Virtual y una subred de puerta de enlace de aplicación Hola

Hola de ejemplo siguiente muestra cómo Hola a toocreate una red Virtual con el Administrador de recursos.

### <a name="step-1"></a>Paso 1

Asignar la subred Hola dirección intervalo 10.0.0.0/24 toohello variable toobe usará para puerta de enlace de aplicaciones mientras se crea una red Virtual.

```powershell
$appgatewaysubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim01" -AddressPrefix "10.0.0.0/24"
```

### <a name="step-2"></a>Paso 2

Asignar la subred Hola dirección intervalo 10.0.1.0/24 toohello variable toobe usará para la administración de API mientras se crea una red Virtual.

```powershell
$apimsubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim02" -AddressPrefix "10.0.1.0/24"
```

### <a name="step-3"></a>Paso 3

Crear una red Virtual denominado **appgwvnet** en grupo de recursos **apim-appGw-RG** para región de oeste de Estados Unidos de hello mediante Hola prefijo 10.0.0.0/16 con subredes 10.0.0.0/24 y 10.0.1.0/24.

```powershell
$vnet = New-AzureRmVirtualNetwork -Name "appgwvnet" -ResourceGroupName "apim-appGw-RG" -Location "West US" -AddressPrefix "10.0.0.0/16" -Subnet $appgatewaysubnet,$apimsubnet
```

### <a name="step-4"></a>Paso 4

Asignar una variable de subred para los pasos siguientes Hola

```powershell
$appgatewaysubnetdata=$vnet.Subnets[0]
$apimsubnetdata=$vnet.Subnets[1]
```
## <a name="create-an-api-management-service-inside-a-vnet-configured-in-internal-mode"></a>Cree un servicio de API Management dentro de una red virtual configurada en modo interno.

Hello en el ejemplo siguiente se muestra cómo toocreate un servicio de administración de API en una red virtual configurado para el acceso interno solo.

### <a name="step-1"></a>Paso 1
Cree un objeto de red Virtual de administración de API con la subred de hello $apimsubnetdata creado anteriormente.

```powershell
$apimVirtualNetwork = New-AzureRmApiManagementVirtualNetwork -Location "West US" -SubnetResourceId $apimsubnetdata.Id
```
### <a name="step-2"></a>Paso 2
Crear un servicio de administración de API dentro de hello red Virtual.

```powershell
$apimService = New-AzureRmApiManagement -ResourceGroupName "apim-appGw-RG" -Location "West US" -Name "ContosoApi" -Organization "Contoso" -AdminEmail "admin@contoso.com" -VirtualNetwork $apimVirtualNetwork -VpnType "Internal" -Sku "Developer"
```
Después de hello por encima del comando se ejecuta correctamente, consulte demasiado[tooaccess servicio de administración de API de red virtual interna requiere una configuración de DNS](api-management-using-with-internal-vnet.md#apim-dns-configuration) tooaccess lo.

## <a name="set-up-a-custom-domain-name-in-api-management"></a>Configuración de un nombre de dominio personalizado en API Management

### <a name="step-1"></a>Paso 1
Cargar Hola certificado con clave privada para el dominio de Hola. En este ejemplo es `*.contoso.net`. 

```powershell
$certUploadResult = Import-AzureRmApiManagementHostnameCertificate -ResourceGroupName "apim-appGw-RG" -Name "ContosoApi" -HostnameType "Proxy" -PfxPath <full path too.pfx file> -PfxPassword <password for certificate file> -PassThru
```

### <a name="step-2"></a>Paso 2
Una vez cargado el certificado de hello, crear un objeto de configuración de nombre de host para el proxy de hello con un nombre de host de `api.contoso.net`, tal y como certificado de ejemplo de Hola proporciona autoridad para hello `*.contoso.net` dominio. 

```powershell
$proxyHostnameConfig = New-AzureRmApiManagementHostnameConfiguration -CertificateThumbprint $certUploadResult.Thumbprint -Hostname "api.contoso.net"
$result = Set-AzureRmApiManagementHostnames -Name "ContosoApi" -ResourceGroupName "apim-appGw-RG" -ProxyHostnameConfiguration $proxyHostnameConfig
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Crear una dirección IP pública para la configuración de front-end de Hola

Crear un recurso IP público **publicIP01** en grupo de recursos **apim-appGw-RG** de región del oeste de Estados Unidos de Hola.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -name "publicIP01" -location "West US" -AllocationMethod Dynamic
```

Una dirección IP se asigna la puerta de enlace de toohello aplicación cuando se inicia el servicio de Hola.

## <a name="create-application-gateway-configuration"></a>Creación de una configuración de puerta de enlace de aplicaciones

Todos los elementos de configuración deben estar configurados antes de crear la puerta de enlace de aplicaciones de Hola. Hello pasos siguientes crean Hola elementos de configuración que son necesarios para un recurso de puerta de enlace de la aplicación.

### <a name="step-1"></a>Paso 1

Cree una configuración de IP de puerta de enlace de aplicaciones denominada **gatewayIP01**. Cuando se inicia la puerta de enlace de aplicaciones, toma una dirección IP de subred Hola configurado y enrutar las direcciones IP de toohello de tráfico de red en el grupo de direcciones IP de back-end de Hola. Tenga en cuenta que cada instancia toma una dirección IP.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name "gatewayIP01" -Subnet $appgatewaysubnetdata
```

### <a name="step-2"></a>Paso 2

Configurar puerto IP front-end de hello para el punto de conexión IP pública Hola. Este puerto es Hola que se conectan a los usuarios finales a.

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "port01"  -Port 443
```
### <a name="step-3"></a>Paso 3

Configurar IP de front-end de hello con punto de conexión IP pública.

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-4"></a>Paso 4

Configurar certificado Hola de puerta de enlace de aplicaciones, hello usa toodecrypt y volver a cifrar el tráfico de hello pasan a través.

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name "cert01" -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

### <a name="step-5"></a>Paso 5

Crear Agente de escucha HTTP de Hola para hello Application Gateway. Asignar configuración de IP de front-end de hello, puerto y tooit del certificado ssl.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol "Https" -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -SslCertificate $cert
```

### <a name="step-6"></a>Paso 6

Crear un servicio de administración de API de sondeo personalizado toohello `ContosoApi` extremo proxy de dominio. ruta de acceso de Hello `/status-0123456789abcdef` es un extremo de estado predeterminado hospedado en todos los servicios de administración de API de Hola. Establecer `api.contoso.net` como un toosecure de nombre de host de sondeo personalizado con el certificado SSL.

> [!NOTE]
> Hola hostname `contosoapi.azure-api.net` es el nombre de host de hello predeterminado proxy configurado cuando un servicio denominado `contosoapi` se crea en Azure pública. 
> 

```powershell
$apimprobe = New-AzureRmApplicationGatewayProbeConfig -Name "apimproxyprobe" -Protocol "Https" -HostName "api.contoso.net" -Path "/status-0123456789abcdef" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
```

### <a name="step-7"></a>Paso 7

Cargar certificado de hello toobe usado en los recursos de grupo habilitado para SSL de back-end de Hola. Se trata de hello mismo certificado que proporciona en el paso 4 anterior.

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name "whitelistcert1" -CertificateFile <full path too.cer file>
```

### <a name="step-8"></a>Paso 8

La configuración de back-end HTTP de hello Application Gateway. Esto incluye el establecimiento de un límite de tiempo de espera para la solicitud de back-end después del cual se cancela. Este valor es diferente de tiempo de espera de sondeo de Hola.

```powershell
$apimPoolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "apimPoolSetting" -Port 443 -Protocol "Https" -CookieBasedAffinity "Disabled" -Probe $apimprobe -AuthenticationCertificates $authcert -RequestTimeout 180
```

### <a name="step-9"></a>Paso 9:

Configurar un grupo de direcciones IP de back-end denominado **apimbackend** con dirección IP virtual interna Hola dirección del servicio de administración de API de Hola creada anteriormente.

```powershell
$apimProxyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "apimbackend" -BackendIPAddresses $apimService.StaticIPs[0]
```

### <a name="step-10"></a>Paso 10

Cree una configuración para un back-end ficticio (inexistente). Rutas de acceso de solicitudes tooAPI que deseamos tooexpose de la API de administración a través de puerta de enlace de aplicaciones se alcanza este back-end y se devolverá 404.

Configurar opciones de HTTP de back-end ficticio de Hola.

```powershell
$dummyBackendSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "dummySetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

Configurar un back-end ficticio **dummyBackendPool**, que señala la dirección de FQDN tooa **dummybackend.com**. Esta dirección FQDN no existe en la red virtual de Hola.

```powershell
$dummyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "dummyBackendPool" -BackendFqdns "dummybackend.com"
```

Crear una regla de configuración que Hola puerta de enlace de aplicación utilizará de forma predeterminada que señala el back-end de toohello inexistente **dummybackend.com** Hola red Virtual.

```powershell
$dummyPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "nonexistentapis" -Paths "/*" -BackendAddressPool $dummyBackendPool -BackendHttpSettings $dummyBackendSetting
```

### <a name="step-11"></a>Paso 11

Configurar rutas de acceso de regla de dirección URL para grupos de back-end de Hola. Esto permite seleccionar solo algunas de hello las API de administración de API para que se va a exponen toohello público. Por ejemplo, en el caso de encontrar `Echo API` (/echo/), `Calculator API` (/calc/), etc., haga que solo `Echo API` resulte accesible desde Internet. 

Hello en el ejemplo siguiente se crea una regla sencilla para hello "/ eco /" ruta de acceso enrutamiento tráfico toohello back-end "apimProxyBackendPool".

```powershell
$echoapiRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "externalapis" -Paths "/echo/*" -BackendAddressPool $apimProxyBackendPool -BackendHttpSettings $apimPoolSetting
```

Si no coincide con la ruta de acceso de Hola queremos tooenable de la administración de API, configuración de mapa de ruta de acceso también configura un grupo de direcciones de back-end de manera predeterminada con el nombre de regla de Hola de reglas de ruta de acceso de hello **dummyBackendPool**. Por ejemplo, http://api.contoso.net/calc/ * va demasiado**dummyBackendPool** tal y como se define como grupo predeterminado de hello para el tráfico no coincidente.

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $echoapiRule, $dummyPathRule -DefaultBackendAddressPool $dummyBackendPool -DefaultBackendHttpSettings $dummyBackendSetting
```

Hola encima paso garantiza que sólo las solicitudes de ruta de acceso de Hola "/ echo" se permiten a través de hello Application Gateway. Tooother solicitudes que API configuradas en administración de API producirá 404 errores de puerta de enlace de aplicaciones cuando se tiene acceso desde Internet Hola. 

### <a name="step-12"></a>Paso 12

Cree una configuración de regla para hello Application Gateway toouse basado en ruta enrutamiento de direcciones URL.

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-13"></a>Paso 13

Configurar el número de Hola de instancias y el tamaño de hello Application Gateway. Aquí usamos hello [WAFS SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) para aumentar la seguridad del programa Hola a recursos de administración de API.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "WAF_Medium" -Tier "WAF" -Capacity 2
```

### <a name="step-14"></a>Paso 14

Configurar WAFS toobe en modo de "Prevención".
```powershell
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"
```

## <a name="create-application-gateway"></a>Creación de una puerta de enlace de aplicaciones

Crear una puerta de enlace de la aplicación con todos los objetos de configuración de Hola de hello pasos anteriores.

```powershell
$appgw = New-AzureRmApplicationGateway -Name $applicationGatewayName -ResourceGroupName $resourceGroupName  -Location $location -BackendAddressPools $apimProxyBackendPool, $dummyBackendPool -BackendHttpSettingsCollection $apimPoolSetting, $dummyBackendSetting  -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert -Probes $apimprobe
```

## <a name="cname-hello-api-management-proxy-hostname-toohello-public-dns-name-of-hello-application-gateway-resource"></a>CNAME Hola administración de API proxy hostname toohello nombre DNS público del programa Hola a recursos de la puerta de enlace de aplicaciones

Una vez creada la puerta de enlace de hello, Hola siguiente paso es front-end de Hola de tooconfigure para la comunicación. Cuando se usa una IP pública, puerta de enlace de aplicación requiere un nombre DNS asignado dinámicamente, que no puede ser fácil toouse. 

Hello nombre DNS de la puerta de enlace de aplicaciones debe ser toocreate usa un registro CNAME que señala el nombre de host de hello APIM proxy (por ejemplo, `api.contoso.net` en los ejemplos de hello anteriores) toothis nombre DNS. front-end de tooconfigure Hola un registro CNAME de IP, recuperar detalles de Hola de Hola puerta de enlace de aplicación y su nombre IP/DNS asociado usando el elemento de hello PublicIPAddress. no se recomienda el uso de Hola de registros de un puesto que puede cambiar Hola VIP en el reinicio de puerta de enlace.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -Name "publicIP01"
```

##<a name="summary"></a>Resumen
Administración de API de Azure configurado en una red virtual proporciona una interfaz de puerta de enlace único para todas las API configuradas, independientemente de si están hospedados en local o en la nube de Hola. Integración de puerta de enlace de aplicaciones con la API de administración proporciona la flexibilidad de Hola de habilitación selectiva determinado toobe API accesible en Internet de hello, así como proporcionar un servidor de aplicaciones Web como una instancia de administración de API de tooyour de front-end.

##<a name="next-steps"></a> Pasos siguientes
* Obtenga más información sobre Azure Application Gateway.
  * [Introducción a Puerta de enlace de aplicaciones](../application-gateway/application-gateway-introduction.md)
  * [Firewall de aplicaciones web de Application Gateway](../application-gateway/application-gateway-webapplicationfirewall-overview.md)
  * [Application Gateway mediante enrutamiento basado en rutas de acceso](../application-gateway/application-gateway-create-url-route-arm-ps.md)
* Más información acerca de API Management y redes virtuales
  * [Utilizando la API de administración disponibles solo en hello red virtual](api-management-using-with-internal-vnet.md)
  * [Usar Azure API Management con redes virtuales](api-management-using-with-vnet.md)
