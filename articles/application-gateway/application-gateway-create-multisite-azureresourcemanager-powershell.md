---
title: "una puerta de enlace de la aplicación para hospedar varios sitios aaaCreate | Documentos de Microsoft"
description: "Esta página proporcionan instrucciones toocreate, configure una puerta de enlace de la aplicación de Azure para hospedar varias aplicaciones web en hello misma puerta de enlace."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: b107d647-c9be-499f-8b55-809c4310c783
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/12/2016
ms.author: amsriva
ms.openlocfilehash: bad9a76be0a73a7026a770630fa7156f6e5940c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-for-hosting-multiple-web-applications"></a>Creación de una puerta de enlace de aplicaciones para hospedar varias aplicaciones web

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-create-multisite-portal.md)
> * [PowerShell del Administrador de recursos de Azure](application-gateway-create-multisite-azureresourcemanager-powershell.md)

Alojamiento de varios sitios permite toodeploy más de una aplicación web en hello misma puerta de enlace de la aplicación. Se basa en la presencia del encabezado de host en la solicitud HTTP entrante hello, toodetermine qué agente de escucha reciba tráfico. agente de escucha de Hello, a continuación, dirige el grupo de back-end de tráfico tooappropriate como está configurado en la definición de las reglas de Hola de puerta de enlace de Hola. En las aplicaciones web se ha habilitado SSL, puerta de enlace de aplicaciones se basa en hello indicación de nombre de servidor (SNI) extensión toochoose Hola correcto agente de escucha para el tráfico de web Hola. Un uso común de alojamiento de varios sitios es tooload equilibrar las solicitudes para grupos de servidor back-end de toodifferent de dominios de web diferente. De igual forma varios subdominios de hello también se puede hospedar el dominio raíz del mismo en Hola misma puerta de enlace de la aplicación.

## <a name="scenario"></a>Escenario

En el siguiente ejemplo de Hola, puerta de enlace de aplicaciones está atendiendo a tráfico para contoso.com y fabrikam.com con dos grupos de servidor back-end: contoso grupo de servidores y el grupo de servidores de fabrikam. El programa de instalación similar podría ser subdominios toohost usado como app.contoso.com y blog.contoso.com.

![imageURLroute](./media/application-gateway-create-multisite-azureresourcemanager-powershell/multisite.png)

## <a name="before-you-begin"></a>Antes de empezar

1. Instalar versión más reciente de Hola de cmdlets de PowerShell de Azure de hello mediante Hola instalador de plataforma Web. Puede descargar e instalar la versión más reciente de Hola de hello **Windows PowerShell** sección de hello [página de descargas](https://azure.microsoft.com/downloads/).
2. se agregaron servidores de Hello debe existir la puerta de enlace de la aplicación de Hola de toohello grupo back-end toouse o han creado sus puntos de conexión en red virtual de hello en una subred independiente o con una dirección IP pública/VIP asignada.

## <a name="requirements"></a>Requisitos

* **Grupo de servidores de back-end:** Hola lista de direcciones IP de servidores de back-end de Hola. direcciones IP en Hello lista deben pertenecer o subred de red virtual toohello o deben ser una dirección IP pública/VIP. También puede utilizarse el FQDN.
* **Configuración del grupo de servidores back-end:** cada grupo tiene una configuración en la que se incluye el puerto, el protocolo y la afinidad basada en cookies. Esta configuración está ligada tooa grupo y son servidores de tooall aplicados en el grupo de Hola.
* **Puerto front-end:** este puerto es Hola pública que se abre en la puerta de enlace de aplicaciones de Hola. Tráfico llega a este puerto y, a continuación, obtiene redirigido tooone de servidores de back-end de Hola.
* **Agente de escucha:** agente de escucha de hello tiene un puerto front-end, un protocolo (Http o Https, estos valores distinguen mayúsculas de minúsculas) y el nombre del certificado SSL hello (si se descarga la configuración de SSL). En el caso de las puertas de enlace de aplicaciones con sitios múltiples habilitados, también se agregan el nombre de host y los indicadores de SNI.
* **Regla:** regla Hola enlaza el agente de escucha de hello, grupo de servidores de back-end de Hola y define qué tráfico de Hola de grupo de servidor back-end debe ser dirigido toowhen llega a un agente de escucha determinado. Las reglas se procesan en orden de hello aparecen y se dirigirá el tráfico a través de la regla primera Hola que coincida con independientemente de especificidad. Por ejemplo, si tiene una regla mediante un agente de escucha básico y una regla mediante una escucha de varios sitio ambos en hello misma regla de puerto, Hola con el agente de escucha de hello multisitio debe aparecer antes de la regla de hello con un agente de escucha básico de hello en orden para hello toofunction de regla de multisitio como se esperaba.

## <a name="create-an-application-gateway"></a>Creación de una puerta de enlace de aplicaciones

siguiente Hola es pasos de hello necesarios toocreate una puerta de enlace de la aplicación:

1. Cree un grupo de recursos para Resource Manager.
2. Crear una red virtual, subredes y dirección IP pública para puerta de enlace de aplicación Hola.
3. Cree un objeto de configuración de la puerta de enlace de aplicaciones.
4. Cree un recurso de Application Gateway.

## <a name="create-a-resource-group-for-resource-manager"></a>Creación de un grupo de recursos para el Administrador de recursos

Asegúrese de que está utilizando la versión más reciente de Hola de PowerShell de Azure. En [Uso de Windows PowerShell con Resource Manager](../powershell-azure-resource-manager.md), encontrará más información al respecto.

### <a name="step-1"></a>Paso 1

Inicie sesión en tooAzure

```powershell
Login-AzureRmAccount
```
Son tooauthenticate solicitada con sus credenciales.

### <a name="step-2"></a>Paso 2

Compruebe las suscripciones de hello para la cuenta de hello.

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a>Paso 3

Elija qué su toouse de las suscripciones de Azure.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>Paso 4

Cree un grupo de recursos (omita este paso si usa uno existente).

```powershell
New-AzureRmResourceGroup -Name appgw-RG -location "West US"
```

También puede crear etiquetas para un grupo de recursos de la puerta de enlace de aplicaciones:

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway multiple site"}
```

Azure Resource Manager requiere que todos los grupos de recursos especifiquen una ubicación. Esta ubicación se utiliza como ubicación predeterminada de Hola para recursos de ese grupo de recursos. Asegúrese de que todos los comandos toocreate un Hola de uso de puerta de enlace de aplicación mismo grupo de recursos.

En el ejemplo de Hola anterior, hemos creado un grupo de recursos denominado **appgw RG** con una ubicación de **West US**.

> [!NOTE]
> Si necesita tooconfigure un sondeo personalizado para la puerta de enlace de aplicaciones, consulte [crear una puerta de enlace de aplicaciones con sondeos personalizados mediante PowerShell](application-gateway-create-probe-ps.md). Para más información, consulte [Información general sobre la supervisión de estado de la puerta de enlace de aplicaciones](application-gateway-probe-overview.md).

## <a name="create-a-virtual-network-and-subnets"></a>Creación una red virtual y subredes

Hola siguiente ejemplo se muestra cómo toocreate una red virtual mediante el Administrador de recursos. En este paso, se crean dos subredes. primera subred de Hello es para la puerta de enlace de aplicaciones de hello propio. Puerta de enlace de aplicaciones requiere su propio toohold subred sus instancias. En dicha subred solo se pueden implementar otras puertas de enlace de aplicaciones. segunda subred de Hello es servidores de back-end de aplicación de hello toohold usado.

### <a name="step-1"></a>Paso 1

Asignar Hola dirección intervalo 10.0.0.0/24 toohello subred toobe variable toohold usado Hola aplicación puerta de enlace.

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -AddressPrefix 10.0.0.0/24
```
### <a name="step-2"></a>Paso 2

Asignar subred2 Hola dirección intervalo 10.0.1.0/24 toohello variable toobe utilizado para grupos de back-end de Hola.

```powershell
$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -AddressPrefix 10.0.1.0/24
```

### <a name="step-3"></a>Paso 3

Crear una red virtual denominada **appgwvnet** en grupo de recursos **appgw rg** de región de hello oeste de Estados Unidos con hello prefijo 10.0.0.0/16 subred 10.0.0.0/24 y 10.0.1.0/24.

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet,$subnet2
```

### <a name="step-4"></a>Paso 4

Asignar una variable de subred para los pasos siguientes de hello, que crea una puerta de enlace de la aplicación.

```powershell
$appgatewaysubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -VirtualNetwork $vnet
$backendsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Crear una dirección IP pública para la configuración de front-end de Hola

Crear un recurso IP público **publicIP01** en grupo de recursos **appgw rg** de región del oeste de Estados Unidos de Hola.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

Una dirección IP se asigna la puerta de enlace de toohello aplicación cuando se inicia el servicio de Hola.

## <a name="create-application-gateway-configuration"></a>Creación de una configuración de puerta de enlace de aplicaciones

Tener tooset seguridad de todos los elementos de configuración antes de crear la puerta de enlace de aplicaciones de Hola. Hello pasos siguientes crean Hola elementos de configuración que son necesarios para un recurso de puerta de enlace de la aplicación.

### <a name="step-1"></a>Paso 1

Cree una configuración de IP de puerta de enlace de aplicaciones denominada **gatewayIP01**. Cuando se inicia la puerta de enlace de aplicaciones, toma una dirección IP de subred Hola configurado y enrutar las direcciones IP de toohello de tráfico de red en el grupo de direcciones IP de back-end de Hola. Tenga en cuenta que cada instancia toma una dirección IP.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $appgatewaysubnet
```

### <a name="step-2"></a>Paso 2

Configurar el grupo de direcciones IP Hola back-end denominado **pool01** y **pool2** con direcciones IP **134.170.185.46**, **134.170.188.221**, **134.170.185.50** para **pool1** y **134.170.186.46**, **134.170.189.221**, **134.170.186.50**  para **pool2**.

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.0.1.100, 10.0.1.101, 10.0.1.102
$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 10.0.1.103, 10.0.1.104, 10.0.1.105
```

En este ejemplo, hay dos grupos de back-end tooroute el tráfico de red basado en sitio solicitado Hola. Un grupo recibe el tráfico del sitio "contoso.com" y otro lo recibe del sitio "fabrikam.com". Tener hello tooreplace anterior tooadd de direcciones IP a sus propios extremos de dirección IP de aplicación. En lugar de las direcciones IP internas, también se pueden usar direcciones IP públicas, el nombre de dominio completo o la NIC de una máquina virtual para las instancias de back-end. toospecify FQDN en lugar de direcciones IP en PowerShell, use "-BackendFQDNs" parámetro.

### <a name="step-3"></a>Paso 3

Configuración de puerta de enlace de aplicaciones **poolsetting01** y **poolsetting02** para tráfico con equilibrio de carga de red de hello en grupo back-end de Hola. En este ejemplo, se configura otro grupo back-end para grupos de back-end de Hola. Cada grupo de back-end puede tener su propia configuración de grupo de back-end.

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120
$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a>Paso 4

Configurar IP de front-end de hello con punto de conexión IP pública.

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a>Paso 5

Configurar puerto front-end de Hola para una puerta de enlace de la aplicación.

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 443
```

### <a name="step-6"></a>Paso 6

Configurar dos certificados SSL para los sitios Web de hello dos vamos toosupport en este ejemplo. Un certificado es para el tráfico de contoso.com y Hola otro es para el tráfico de fabrikam.com. Deben ser certificados emitidos por una entidad de certificación para sus sitios web. Los certificados autofirmados se admiten, pero no se recomiendan para el tráfico de producción.

```powershell
$cert01 = New-AzureRmApplicationGatewaySslCertificate -Name contosocert -CertificateFile <file path> -Password <password>
$cert02 = New-AzureRmApplicationGatewaySslCertificate -Name fabrikamcert -CertificateFile <file path> -Password <password>
```

### <a name="step-7"></a>Paso 7

Configurar dos agentes de escucha para los sitios web de dos hello en este ejemplo. Este paso configura los agentes de escucha de Hola por dirección IP, puerto y host pública utilizan tooreceive el tráfico entrante. Parámetro de nombre de host es necesario para la compatibilidad con múltiples sitios y debe ser el sitio de Web de conjunto toohello adecuado para qué Hola se recibe el tráfico. Parámetro RequireServerNameIndication debe establecerse tootrue para sitios Web que necesita compatibilidad con SSL en un escenario de host múltiple. Si se requiere compatibilidad con SSL, también necesitará toospecify Hola SSL certificado que se tráfico toosecure usado para esa aplicación web. combinación de Hola de FrontendIPConfiguration, FrontendPort y nombre de host debe ser tooa único agente de escucha. Cada agente de escucha puede admitir solo un certificado.

```powershell
$listener01 = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "contoso11.com" -RequireServerNameIndication true  -SslCertificate $cert01
$listener02 = New-AzureRmApplicationGatewayHttpListener -Name "listener02" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "fabrikam11.com" -RequireServerNameIndication true -SslCertificate $cert02
```

### <a name="step-8"></a>Paso 8

Crear dos reglas establecer para hello dos aplicaciones web en este ejemplo. Una regla une los agentes de escucha, los grupos de back-end y la configuración de http. Este paso configura Hola aplicación puerta de enlace toouse básica regla de enrutamiento, uno para cada sitio Web. Sitio Web de tooeach de tráfico recibe su agente de escucha configurado y, a continuación, se dirige tooits configurado grupo back-end, con propiedades de hello especificadas en hello BackendHttpSettings.

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule01" -RuleType Basic -HttpListener $listener01 -BackendHttpSettings $poolSetting01 -BackendAddressPool $pool1
$rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule02" -RuleType Basic -HttpListener $listener02 -BackendHttpSettings $poolSetting02 -BackendAddressPool $pool2
```

### <a name="step-9"></a>Paso 9:

Configurar el número de Hola de instancias y el tamaño de la puerta de enlace de aplicaciones de Hola.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Medium" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a>Creación de una puerta de enlace de aplicaciones

Crear una puerta de enlace de la aplicación con todos los objetos de configuración de hello pasos anteriores.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener01, $listener02 -RequestRoutingRules $rule01, $rule02 -Sku $sku -SslCertificates $cert01, $cert02
```

> [!IMPORTANT]
> Aprovisionamiento de puerta de enlace de aplicaciones es una operación larga y puede tardar algún tiempo toocomplete.
> 
> 

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

Obtenga información acerca de cómo tooprotect sus sitios Web con [puerta de enlace de aplicaciones - servidor de aplicaciones Web](application-gateway-webapplicationfirewall-overview.md)

