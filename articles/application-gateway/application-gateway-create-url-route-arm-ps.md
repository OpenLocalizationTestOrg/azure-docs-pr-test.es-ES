---
title: "reglas de una puerta de enlace de la aplicación mediante el enrutamiento de direcciones URL de aaaCreate | Documentos de Microsoft"
description: "Esta página proporcionan instrucciones toocreate, configure una puerta de enlace de la aplicación de Azure mediante las reglas de enrutamiento de direcciones URL"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d141cfbb-320a-4fc9-9125-10001c6fa4cf
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: 54fcccc39e48a933576968ce3d8160518c0d0b7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing"></a>Creación de una puerta de enlace de aplicaciones mediante enrutamiento basado en rutas de acceso

> [!div class="op_single_selector"]
> * [Portal de Azure](application-gateway-create-url-route-portal.md)
> * [PowerShell de Azure Resource Manager](application-gateway-create-url-route-arm-ps.md)
> * [CLI de Azure 2.0](application-gateway-create-url-route-cli.md)

Enrutamiento basado en la ruta de acceso de direcciones URL permite tooassociate rutas basándose en la ruta de acceso de dirección URL de Hola de una solicitud Http. Comprueba si hay un grupo de back-end de ruta tooa configurado para URL de hello presentado en hello Application Gateway. A continuación, envía toohello de tráfico de red de hello definido grupo back-end. Un uso común de enrutamiento basado en la dirección URL es tooload equilibrar las solicitudes para grupos de servidor back-end de toodifferent de diferentes tipos de contenido.

Enrutamiento basado en dirección URL, presenta una puerta de enlace de tooapplication de tipo de regla nueva. Application Gateway tiene dos tipos de reglas: básicas y PathBasedRouting. Tipo de regla básica proporciona servicio round robin para hello back-end grupos al PathBasedRouting además de la distribución competitiva tooround, también tiene modelo de ruta de acceso de dirección URL de solicitud de hello en cuenta al elegir grupo back-end de Hola.

## <a name="scenario"></a>Escenario

En el siguiente ejemplo de Hola, puerta de enlace de aplicaciones está atendiendo a tráfico para contoso.com con dos grupos de servidor back-end: grupo de servidores de vídeo y el grupo de servidores de la imagen.

Las solicitudes de http://contoso.com/image * se enrutan se enrutan y grupo de servidores de tooimage (pool1) http://contoso.com/video * toovideo grupo de servidores (pool2). Si ninguno de los patrones de ruta de acceso de hello coinciden, se selecciona un grupo de servidores de forma predeterminada (pool1).

![ruta de dirección URL](./media/application-gateway-create-url-route-arm-ps/figure1.png)

## <a name="before-you-begin"></a>Antes de empezar

1. Instalar versión más reciente de Hola de cmdlets de PowerShell de Azure de hello mediante Hola instalador de plataforma Web. Puede descargar e instalar la versión más reciente de Hola de hello **Windows PowerShell** sección de hello [página de descargas](https://azure.microsoft.com/downloads/).
2. Tendrá que crear una red virtual y subred para Application Gateway. Asegúrese de que no hay máquinas virtuales o las implementaciones de nube están usando la subred de Hola. puerta de enlace de aplicaciones de Hello debe ser por sí solo en una subred de red virtual.
3. se agregaron servidores de Hello debe existir la puerta de enlace de la aplicación de Hola de toohello grupo back-end toouse o han creado sus puntos de conexión de red virtual de Hola o con una dirección IP pública/VIP asignada.

## <a name="what-is-required-toocreate-an-application-gateway"></a>¿Qué es necesario toocreate una puerta de enlace de la aplicación?

* **Grupo de servidores de back-end:** Hola lista de direcciones IP de servidores de back-end de Hola. direcciones IP en Hello lista deben pertenecer o subred de red virtual toohello o deben ser una dirección IP pública/VIP.
* **Configuración del grupo de servidores back-end:** cada grupo tiene una configuración en la que se incluye el puerto, el protocolo y la afinidad basada en cookies. Esta configuración está ligada tooa grupo y son servidores de tooall aplicados en el grupo de Hola.
* **Puerto front-end:** este puerto es Hola pública que se abre en la puerta de enlace de aplicaciones de Hola. Tráfico llega a este puerto y, a continuación, obtiene redirigido tooone de servidores de back-end de Hola.
* **Agente de escucha:** agente de escucha de hello tiene un puerto front-end, un protocolo (Http o Https, estos valores distinguen mayúsculas de minúsculas) y el nombre del certificado SSL hello (si se descarga la configuración de SSL).
* **Regla:** regla Hola enlaza el agente de escucha de hello, grupo de servidores de back-end de Hola y define qué tráfico de Hola de grupo de servidor back-end debe ser dirigido toowhen llega a un agente de escucha determinado.

## <a name="create-an-application-gateway"></a>Creación de una puerta de enlace de aplicaciones

diferencia de Hello entre el uso de Azure clásico y el Administrador de recursos de Azure es orden de hello en el que crear puerta de enlace de aplicaciones de Hola y elementos de Hola que necesitan toobe configurado.

Con el Administrador de recursos, todos los elementos que conforman una puerta de enlace de aplicaciones se configuran individualmente y, a continuación, reunir toocreate de recursos de puerta de enlace de aplicación Hola.

Estos son los pasos de Hola que son necesario toocreate una puerta de enlace de la aplicación:

1. Cree un grupo de recursos para Resource Manager.
2. Crear una red virtual, subred y dirección IP pública para puerta de enlace de aplicación Hola.
3. Cree un objeto de configuración de la puerta de enlace de aplicaciones.
4. Cree un recurso de Application Gateway.

## <a name="create-a-resource-group-for-resource-manager"></a>Creación de un grupo de recursos para el Administrador de recursos

Asegúrese de que está utilizando la versión más reciente de Hola de PowerShell de Azure. Hay más información disponible en [Uso de Windows PowerShell con Resource Manager](../powershell-azure-resource-manager.md).

### <a name="step-1"></a>Paso 1

Inicie sesión en tooAzure

```powershell
Login-AzureRmAccount
```

Son tooauthenticate solicitada con sus credenciales.<BR>

### <a name="step-2"></a>Paso 2

Compruebe las suscripciones de hello para la cuenta de hello.

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a>Paso 3

Elija qué su toouse de las suscripciones de Azure. <BR>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>Paso 4

Cree un grupo de recursos (omita este paso si usa uno existente).

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US"
```

También puede crear etiquetas para un grupo de recursos de la puerta de enlace de aplicaciones:

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway URL routing"} 
```

Azure Resource Manager requiere que todos los grupos de recursos especifiquen una ubicación. Este grupo de recursos se utiliza como ubicación predeterminada de Hola para recursos de ese grupo de recursos. Asegúrese de que todos los comandos toocreate un Hola de uso de puerta de enlace de aplicación mismo grupo de recursos.

En el ejemplo de Hola anterior, hemos creado un grupo de recursos denominado "appgw-RG" y la ubicación "West US".

> [!NOTE]
> Si necesita tooconfigure un sondeo personalizado para la puerta de enlace de aplicaciones, consulte [crear una puerta de enlace de aplicaciones con sondeos personalizados mediante PowerShell](application-gateway-create-probe-ps.md). Para más información, consulte [Información general sobre la supervisión de estado de la puerta de enlace de aplicaciones](application-gateway-probe-overview.md) .
> 
> 

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Crear una red virtual y una subred de puerta de enlace de aplicación Hola

Hola siguiente ejemplo se muestra cómo toocreate una red virtual mediante el Administrador de recursos. Este ejemplo crea una red virtual para hello Application Gateway. Puerta de enlace de aplicaciones requiere su propia subred, por este motivo subred Hola creado para hello Application Gateway es menor que Hola espacio de direcciones de red virtual. Esto permite que otros recursos, incluidos pero sin limitarse tooweb servidores toobe Hola misma configuración red virtual.

### <a name="step-1"></a>Paso 1

Asignar Hola dirección intervalo 10.0.0.0/24 toohello subred toobe variable utiliza toocreate una red virtual.  Esto crea el objeto de configuración de subred de Hola para puerta de enlace de aplicaciones, que se utiliza en el ejemplo siguiente se Hola Hola.

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

### <a name="step-2"></a>Paso 2

Crear una red virtual denominada **appgwvnet** en grupo de recursos **appgw rg** de región de oeste de Estados Unidos de hello con hello prefijo 10.0.0.0/16 subred 10.0.0.0/24. Esto completa la configuración de Hola de hello red virtual con una sola subred para hello tooreside de puerta de enlace de aplicaciones.

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

### <a name="step-3"></a>Paso 3

Asignar pasos de variable de subred de Hola para hello, este argumento se pasa toohello `New-AzureRMApplicationGateway` cmdlet en un paso posterior.

```powershell
$subnet=$vnet.Subnets[0]
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Crear una dirección IP pública para la configuración de front-end de Hola

Crear un recurso IP público **publicIP01** en grupo de recursos **appgw rg** de región del oeste de Estados Unidos de Hola. Puerta de enlace de aplicación puede usar una dirección IP pública, la dirección IP interna o ambas solicitudes tooreceive para equilibrar la carga.  En este ejemplo, solo se usa una dirección IP pública. En el siguiente ejemplo de Hola, ningún nombre DNS está configurado para la creación de la dirección IP pública Hola.  Application Gateway no admite nombres DNS personalizados en direcciones IP públicas.  Si se requiere para el punto de conexión público Hola un nombre personalizado, se debe crear un registro CNAME toopoint toohello generada automáticamente nombre DNS para la dirección IP pública Hola.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

Una dirección IP se asigna la puerta de enlace de toohello aplicación cuando se inicia el servicio de Hola.

## <a name="create-application-gateway-configuration"></a>Creación de una configuración de puerta de enlace de aplicaciones

Todos los elementos de configuración deben estar configurados antes de crear la puerta de enlace de aplicaciones de Hola. Hello pasos siguientes crean Hola elementos de configuración que son necesarios para un recurso de puerta de enlace de la aplicación.

### <a name="step-1"></a>Paso 1

Cree una configuración de IP de puerta de enlace de aplicaciones denominada **gatewayIP01**. Cuando se inicia la puerta de enlace de aplicaciones, toma una dirección IP de subred Hola configurado y enrutar las direcciones IP de toohello de tráfico de red en el grupo de direcciones IP de back-end de Hola. Tenga en cuenta que cada instancia toma una dirección IP.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

### <a name="step-2"></a>Paso 2

Configurar el grupo de direcciones IP Hola back-end denominado **pool01** y **pool2** con direcciones IP para **pool1** y **pool2**. Estas direcciones IP son direcciones IP de Hola de recursos de Hola que hospedan toobe de aplicación web de hello protegido por la puerta de enlace de aplicaciones de Hola. Estos miembros del grupo back-end son todos los toobe validado correcto por sondeos sean sondeos básicos o personalizados sondeos.  A continuación, se enruta el tráfico toothem cuando las solicitudes procedan en la puerta de enlace de aplicaciones de Hola. Grupos back-end pueden utilizarse en varias reglas dentro de hello aplicación puerta de enlace, lo que significa un grupo back-end podría usarse para varias aplicaciones web que se encuentren en hello mismo host.

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 134.170.186.47, 134.170.189.222, 134.170.186.51
```

En este ejemplo, hay dos grupos de back-end tooroute el tráfico de red en función de la ruta de acceso de dirección URL de Hola. Un grupo recibe el tráfico de la ruta de dirección URL "/video" y otro lo recibe de la ruta "/image". Reemplace Hola anterior tooadd de direcciones IP a sus propios extremos de dirección IP de aplicación. 

### <a name="step-3"></a>Paso 3

Configuración de puerta de enlace de aplicaciones **poolsetting01** y **poolsetting02** para tráfico con equilibrio de carga de red de hello en grupo back-end de Hola. En este ejemplo, se configura otro grupo back-end para grupos de back-end de Hola. Cada grupo de back-end puede tener su propia configuración de grupo de back-end.  Configuración de HTTP de back-end se usa por miembros del grupo de reglas tooroute tráfico toohello correcta back-end. Esto determina el protocolo de Hola y el puerto que se usa al enviar tráfico toohello los miembros del grupo back-end. Configuración de HTTP de back-end de hello también dependen de las sesiones basado en cookies.  Si está habilitada, la afinidad de sesión basado en cookies envía tráfico toohello mismo back-end como solicitudes anteriores para cada paquete.

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a>Paso 4

Configurar IP de front-end de hello con punto de conexión IP pública. objeto de configuración de IP de front-end de Hello usa un hello toorelate de agente de escucha exterior orientada hacia la dirección IP con el agente de escucha de Hola.

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a>Paso 5

Configurar puerto front-end de Hola para una puerta de enlace de la aplicación. objeto de configuración de puerto front-end de Hello utiliza un agente de escucha toodefine qué puerto de escucha de puerta de enlace de aplicación hello para el tráfico en el agente de escucha de Hola.

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 80
```

### <a name="step-6"></a>Paso 6

Configurar el agente de escucha de Hola. Este paso configura el agente de escucha de hello para la dirección IP pública hello y utiliza el puerto tooreceive tráfico de red entrante. Hola siguiente ejemplo toma la configuración de IP de front-end de hello configurado previamente, la configuración de puerto front-end y un protocolo (http o https) y configura el agente de escucha de Hola. En este ejemplo, el agente de escucha de hello escucha tooHTTP tráfico en el puerto 80 en la dirección IP pública Hola que creó anteriormente.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Http -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01
```

### <a name="step-7"></a>Paso 7

Configurar rutas de acceso de regla de dirección URL para grupos de back-end de Hola. Este paso configura Hola ruta de acceso relativa utilizado por la puerta de enlace de aplicaciones y define Hola asignación entre la ruta de acceso de dirección URL de Hola y Hola un grupo back-end se asigna el tráfico entrante de toohandle Hola.

> [!IMPORTANT]
> Cada ruta de acceso debe comenzar con / hello solo lugar y un "\*" está permitida, está al final de Hola. Algunos ejemplos válidos son /xyz, /xyz* o /xyz/*. Hello cadena fed buscador de coincidencias de ruta de acceso de toohello no incluye cualquier texto después de hello primero "?" o "#" y los caracteres no se permiten. 

Hello en el ejemplo siguiente se crea dos reglas: uno para el enrutamiento de ruta de acceso "/ imágenes /" tráfico tooback-end "pool1" y otra para "/ vídeo /" ruta de acceso de enrutamiento de tráfico tooback-end "pool2." Estas reglas aseguran de que el tráfico para cada conjunto de direcciones URL es toohello enrutado back-end. Por ejemplo, http://contoso.com/image/figure1.jpg va toopool1 y http://contoso.com/video/example.mp4 va toopool2.

```powershell
$imagePathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule1" -Paths "/image/*" -BackendAddressPool $pool1 -BackendHttpSettings $poolSetting01

$videoPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule2" -Paths "/video/*" -BackendAddressPool $pool2 -BackendHttpSettings $poolSetting02
```

Si la ruta de acceso de hello no coincide con ninguna de las reglas de ruta de acceso definida previamente hello, configuración del mapa de ruta de acceso de regla de hello también configura un grupo de direcciones de back-end de manera predeterminada. Por ejemplo, http://contoso.com/shoppingcart/test.html va toopool1 tal y como se define como grupo predeterminado de hello para el tráfico no coincidente.

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $videoPathRule, $imagePathRule -DefaultBackendAddressPool $pool1 -DefaultBackendHttpSettings $poolSetting02
```

### <a name="step-8"></a>Paso 8

Creación de una configuración de regla Este paso configura el enrutamiento basado en la ruta de acceso de hello aplicación puerta de enlace toouse dirección URL. Hola `$urlPathMap` variable definida en hello paso anterior es ahora usa toocreate Hola ruta de acceso una regla de. En este paso, asociamos de regla de hello con un agente de escucha y la asignación de ruta de acceso de dirección url de hello creado anteriormente.

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-9"></a>Paso 9:

Configurar el número de Hola de instancias y el tamaño de la puerta de enlace de aplicaciones de Hola.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Small" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a>Creación de una puerta de enlace de aplicaciones

Crear una puerta de enlace de la aplicación con todos los objetos de configuración de hello pasos anteriores.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku
```

## <a name="get-application-gateway-dns-name"></a>Obtención del nombre DNS de una puerta de enlace de aplicaciones

Una vez creada la puerta de enlace de hello, Hola siguiente paso es front-end de Hola de tooconfigure para la comunicación. Cuando se utiliza una dirección IP pública, la puerta de enlace de aplicaciones requiere un nombre DNS asignado dinámicamente, que no es descriptivo. los usuarios finales de tooensure puede llegar a puerta de enlace de aplicaciones de hello, un registro CNAME puede ser usado toopoint toohello extremo público de puerta de enlace de aplicación Hola. [Configuración de un nombre de dominio personalizado en Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). front-end de tooconfigure Hola un registro CNAME de IP, recuperar los detalles de puerta de enlace de aplicaciones de Hola y su nombre IP/DNS asociado con puerta de enlace de hello PublicIPAddress elemento adjunto toohello aplicación. nombre DNS de Hello aplicación la puerta de enlace debe ser toocreate usa un registro CNAME. no se recomienda el uso de Hola de registros de un puesto que puede cambiar Hola VIP en el reinicio de puerta de enlace de aplicaciones.

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

Si desea que toolearn la descarga de capa de Sockets seguros (SSL), consulte [configurar una puerta de enlace de la aplicación para la descarga SSL](application-gateway-ssl-arm.md).

