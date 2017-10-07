---
title: aaaCreate, iniciar o eliminar una puerta de enlace de aplicaciones | Documentos de Microsoft
description: "Esta página proporciona instrucciones toocreate, configurar, iniciar y eliminar una puerta de enlace de la aplicación de Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 577054ca-8368-4fbf-8d53-a813f29dc3bc
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 3efef5b49880c9efdafad8b88d4bce5b749b82af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-start-or-delete-an-application-gateway-with-powershell"></a>Creación, inicio o eliminación de una puerta de enlace de aplicaciones con PowerShell 

> [!div class="op_single_selector"]
> * [Portal de Azure](application-gateway-create-gateway-portal.md)
> * [PowerShell de Azure Resource Manager](application-gateway-create-gateway-arm.md)
> * [Azure Classic PowerShell](application-gateway-create-gateway.md)
> * [Plantilla del Administrador de recursos de Azure](application-gateway-create-gateway-arm-template.md)
> * [CLI de Azure](application-gateway-create-gateway-cli.md)

Azure Application Gateway es un equilibrador de carga de nivel 7. Proporciona conmutación por error, enrutamiento de rendimiento de las solicitudes HTTP entre diferentes servidores, independientemente de si están en la nube de Hola o de forma local. Application Gateway proporciona numerosas características del Controlador de entrega de aplicaciones (ADC), entre las que se incluyen el equilibrio de carga HTTP, la afinidad de sesiones basada en cookies, la descarga SSL (Capa de sockets seguros), los sondeos personalizados sobre el estado, la compatibilidad con multisitio, etc. toofind una lista completa de las características admitidas, visite [información general sobre la puerta de enlace de aplicaciones](application-gateway-introduction.md)

Este artículo le guiará a través de hello pasos toocreate, configurar, iniciar y eliminar una puerta de enlace de la aplicación.

## <a name="before-you-begin"></a>Antes de empezar

1. Instalar versión más reciente de Hola de cmdlets de PowerShell de Azure de hello mediante Hola instalador de plataforma Web. Puede descargar e instalar la versión más reciente de Hola de hello **Windows PowerShell** sección de hello [página de descargas](https://azure.microsoft.com/downloads/).
2. Si tiene una red virtual existente, seleccione una subred vacía existente o crear una nueva subred en la red virtual existente únicamente para su uso por la puerta de enlace de aplicaciones de Hola. No se puede implementar Hola aplicación puerta de enlace tooa red virtual diferente que los recursos de hello piensa toodeploy detrás de la puerta de enlace de aplicación Hola a menos que se utiliza el intercambio de tráfico de red virtual. toolearn más visite [intercambio de tráfico de red virtual](../virtual-network/virtual-network-peering-overview.md)
3. Compruebe que tiene una red virtual de trabajo con una subred válida. Asegúrese de que no hay máquinas virtuales o las implementaciones de nube están usando la subred de Hola. puerta de enlace de aplicaciones de Hello debe ser por sí solo en una subred de red virtual.
4. deben existir servidores Hola configurar la puerta de enlace de aplicaciones de toouse Hola o tener asignados de sus puntos de conexión creados en la red virtual de Hola o con una dirección IP pública/VIP.

## <a name="what-is-required-toocreate-an-application-gateway"></a>¿Qué es necesario toocreate una puerta de enlace de la aplicación?

Cuando usas hello `New-AzureApplicationGateway` comando toocreate Hola aplicación puerta de enlace, no se ha configurado en este momento y recursos Hola recién creada se configuran mediante XML o un objeto de configuración.

los valores de Hello son:

* **Grupo de servidores de back-end:** Hola lista de direcciones IP de servidores de back-end de Hola. direcciones IP en Hello lista deben pertenecer o subred de red virtual toohello o deben ser una dirección IP pública/VIP.
* **Configuración del grupo de servidores back-end:** cada grupo tiene una configuración en la que se incluye el puerto, el protocolo y la afinidad basada en cookies. Esta configuración está ligada tooa grupo y son servidores de tooall aplicados en el grupo de Hola.
* **Puerto front-end:** este puerto es Hola pública que se abre en la puerta de enlace de aplicaciones de Hola. Tráfico llega a este puerto y, a continuación, obtiene redirigido tooone de servidores de back-end de Hola.
* **Agente de escucha:** agente de escucha de hello tiene un puerto front-end, un protocolo (Http o Https, estos valores distinguen mayúsculas de minúsculas) y el nombre del certificado SSL hello (si se descarga la configuración de SSL).
* **Regla:** regla Hola enlaza el agente de escucha de Hola y el grupo de servidores de back-end de Hola y define qué tráfico de Hola de grupo de servidor back-end debe ser dirigido toowhen llega a un agente de escucha determinado.

## <a name="create-an-application-gateway"></a>Creación de una puerta de enlace de aplicaciones

toocreate una puerta de enlace de la aplicación:

1. Cree un recurso de Application Gateway.
2. Cree un archivo de configuración XML o un objeto de configuración.
3. Confirmar Hola configuración toohello recién creado recursos de puerta de enlace de aplicaciones.

> [!NOTE]
> Si necesita tooconfigure un sondeo personalizado para la puerta de enlace de aplicaciones, consulte [crear una puerta de enlace de aplicaciones con sondeos personalizados mediante PowerShell](application-gateway-create-probe-classic-ps.md). Para más información, consulte [Información general sobre la supervisión de estado de la puerta de enlace de aplicaciones](application-gateway-probe-overview.md) .

![Escenario de ejemplo][scenario]

### <a name="create-an-application-gateway-resource"></a>Crear un recurso de la puerta de enlace de aplicaciones

puerta de enlace de toocreate hello, use hello `New-AzureApplicationGateway` cmdlet, reemplazando los valores de hello por los suyos propios. La facturación de puerta de enlace de hello no se inicia en este momento. Facturación comienza en un paso posterior, cuando la puerta de enlace de Hola se ha iniciado correctamente.

Hello en el ejemplo siguiente se crea una puerta de enlace de la aplicación mediante el uso de una red virtual denominada "testvnet1" y una subred denominada "subred-1":

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

*Description*, *InstanceCount* y *GatewaySize* son parámetros opcionales.

se creó toovalidate que Hola puerta de enlace, puede usar hello `Get-AzureApplicationGateway` cmdlet.

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Stopped
VirtualIPs    : {}
DnsName       :
```

> [!NOTE]
> Hola valor predeterminado de *InstanceCount* es 2, con un valor máximo de 10. Hola valor predeterminado de *GatewaySize* es Medium. Puede elegir entre Pequeño, Mediano y Grande.

*VirtualIPs* y *DnsName* se muestran como en blanco porque no se inició aún la puerta de enlace de Hola. Estos se crean una vez que la puerta de enlace de hello está en estado de ejecución de Hola.

## <a name="configure-hello-application-gateway"></a>Configurar la puerta de enlace de aplicaciones de Hola

Puede configurar la puerta de enlace de aplicaciones de hello mediante el uso de XML o un objeto de configuración.

### <a name="configure-hello-application-gateway-by-using-xml"></a>Configurar la puerta de enlace de aplicaciones de hello mediante XML

En el siguiente ejemplo de Hola, utilice un tooconfigure de archivo XML todos los valores de puerta de enlace de la aplicación y, a continuación, confirmarlos toohello de recursos de puerta de enlace de aplicación.  

#### <a name="step-1"></a>Paso 1

Copie Hola después tooNotepad de texto.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>(name-of-your-frontend-port)</Name>
            <Port>(port number)</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>(name-of-your-backend-pool)</Name>
            <IPAddresses>
                <IPAddress>(your-IP-address-for-backend-pool)</IPAddress>
                <IPAddress>(your-second-IP-address-for-backend-pool)</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>(backend-setting-name-to-configure-rule)</Name>
            <Port>80</Port>
            <Protocol>[Http|Https]</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>(name-of-the-listener)</Name>
            <FrontendPort>(name-of-your-frontend-port)</FrontendPort>
            <Protocol>[Http|Https]</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>(name-of-load-balancing-rule)</Name>
            <Type>basic</Type>
            <BackendHttpSettings>(backend-setting-name-to-configure-rule)</BackendHttpSettings>
            <Listener>(name-of-the-listener)</Listener>
            <BackendAddressPool>(name-of-your-backend-pool)</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

Editar valores de hello entre paréntesis Hola Hola elementos de configuración. Guarde el archivo hello con extensión .xml.

> [!IMPORTANT]
> elemento de Hello protocolo Http o Https distingue mayúsculas de minúsculas.

Hola de ejemplo siguiente muestra cómo toouse una configuración de archivo tooset de puerta de enlace de aplicación Hola. carga de ejemplo de Hola equilibra el tráfico HTTP en el puerto público 80 y envía el tráfico de red en el puerto 80 de final de tooback entre dos direcciones IP.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>80</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>BackendPool1</Name>
            <IPAddresses>
                <IPAddress>10.0.0.1</IPAddress>
                <IPAddress>10.0.0.2</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>BackendSetting1</Name>
            <Port>80</Port>
            <Protocol>Http</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>HTTPListener1</Name>
            <FrontendPort>FrontendPort1</FrontendPort>
            <Protocol>Http</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>HttpLBRule1</Name>
            <Type>basic</Type>
            <BackendHttpSettings>BackendSetting1</BackendHttpSettings>
            <Listener>HTTPListener1</Listener>
            <BackendAddressPool>BackendPool1</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

#### <a name="step-2"></a>Paso 2

A continuación, establezca la puerta de enlace de aplicaciones de Hola. Hola de uso `Set-AzureApplicationGatewayConfig` cmdlet con un archivo de configuración XML.

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile "D:\config.xml"
```

### <a name="configure-hello-application-gateway-by-using-a-configuration-object"></a>Configurar la puerta de enlace de aplicaciones de hello mediante el uso de un objeto de configuración

Hola de ejemplo siguiente muestra cómo tooconfigure Hola puerta de enlace de aplicaciones mediante el uso de objetos de configuración. Todos los elementos de configuración deben configurarse individualmente y, a continuación, agregar objeto de configuración de puerta de enlace de tooan aplicación. Después de crear el objeto de configuración de hello, usar hello `Set-AzureApplicationGateway` comando toocommit Hola configuración toohello creado anteriormente recursos de puerta de enlace de aplicaciones.

> [!NOTE]
> Antes de asignar un objeto de configuración de tooeach de valor, debe toodeclare qué tipo de objeto de PowerShell que se usa para el almacenamiento. elementos individuales de Hello primera línea toocreate Hola define qué `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` se usan.

#### <a name="step-1"></a>Paso 1

Cree todos los elementos de configuración individuales.

Cree la IP de front-end de hello tal y como se muestra en el siguiente ejemplo de Hola.

```powershell
$fip = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration
$fip.Name = "fip1"
$fip.Type = "Private"
$fip.StaticIPAddress = "10.0.0.5"
```

Crear puertos front-end de hello tal y como se muestra en el siguiente ejemplo de Hola.

```powershell
$fep = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort
$fep.Name = "fep1"
$fep.Port = 80
```

Crear grupo de servidores de back-end de Hola.

Define las direcciones IP Hola que se agregan el grupo de servidores de back-end de toohello tal y como se muestra en el siguiente ejemplo de Hola.

```powershell
$servers = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendServerCollection
$servers.Add("10.0.0.1")
$servers.Add("10.0.0.2")
```

Utilice Hola $server object tooadd Hola valores toohello grupo back-end (objeto) ($pool).

```powershell
$pool = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool
$pool.BackendServers = $servers
$pool.Name = "pool1"
```

Crear configuración de grupo de servidor back-end de Hola.

```powershell
$setting = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings
$setting.Name = "setting1"
$setting.CookieBasedAffinity = "enabled"
$setting.Port = 80
$setting.Protocol = "http"
```

Crear Agente de escucha de Hola.

```powershell
$listener = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener
$listener.Name = "listener1"
$listener.FrontendPort = "fep1"
$listener.FrontendIP = "fip1"
$listener.Protocol = "http"
$listener.SslCert = ""
```

Crear regla de Hola.

```powershell
$rule = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule
$rule.Name = "rule1"
$rule.Type = "basic"
$rule.BackendHttpSettings = "setting1"
$rule.Listener = "listener1"
$rule.BackendAddressPool = "pool1"
```

#### <a name="step-2"></a>Paso 2

Asignar todas las configuración individual elementos tooan aplicación puerta de enlace configuración objeto ($appgwconfig).

Agregar configuración de toohello IP front-end de Hola.

```powershell
$appgwconfig = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.ApplicationGatewayConfiguration
$appgwconfig.FrontendIPConfigurations = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration]"
$appgwconfig.FrontendIPConfigurations.Add($fip)
```

Agregar configuración de toohello de hello puerto front-end.

```powershell
$appgwconfig.FrontendPorts = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort]"
$appgwconfig.FrontendPorts.Add($fep)
```
Agregar configuración de toohello del grupo de servidor back-end de Hola.

```powershell
$appgwconfig.BackendAddressPools = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool]"
$appgwconfig.BackendAddressPools.Add($pool)
```

Agregue la configuración de toohello de configuración del grupo de back-end de Hola.

```powershell
$appgwconfig.BackendHttpSettingsList = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings]"
$appgwconfig.BackendHttpSettingsList.Add($setting)
```

Agregar configuración de toohello de agente de escucha de Hola.

```powershell
$appgwconfig.HttpListeners = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener]"
$appgwconfig.HttpListeners.Add($listener)
```

Agregar configuración de la regla toohello Hola.

```powershell
$appgwconfig.HttpLoadBalancingRules = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule]"
$appgwconfig.HttpLoadBalancingRules.Add($rule)
```

### <a name="step-3"></a>Paso 3
Confirmar el recurso de puerta de enlace de aplicaciones de toohello objeto de configuración de hello utilizando `Set-AzureApplicationGatewayConfig`.

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -Config $appgwconfig
```

## <a name="start-hello-gateway"></a>Iniciar la puerta de enlace de Hola

Una vez que se ha configurado la puerta de enlace de hello, usar hello `Start-AzureApplicationGateway` puerta de enlace de cmdlet toostart Hola. La facturación de una puerta de enlace de la aplicación comienza después de puerta de enlace de Hola se ha iniciado correctamente.

> [!NOTE]
> Hola `Start-AzureApplicationGateway` cmdlet podría tardar hasta toofinish too15-20 minutos.

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a>Comprobar el estado de la puerta de enlace de Hola

Hola de uso `Get-AzureApplicationGateway` estado de cmdlet toocheck Hola de puerta de enlace de Hola. Si `Start-AzureApplicationGateway` se realizó correctamente en el paso anterior de hello, *estado* debe estar en ejecución, y *Vip* y *DnsName* debe tener las entradas válidas.

Hello en el ejemplo siguiente se muestra una puerta de enlace de la aplicación que está en funcionamiento y en ejecución, y tootake listo tráfico destinado `http://<generated-dns-name>.cloudapp.net`.

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 8:09:28 PM - Begin Operation: Get-AzureApplicationGateway
VERBOSE: 8:09:30 PM - Completed Operation: Get-AzureApplicationGateway
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
Vip           : 138.91.170.26
DnsName       : appgw-1b8402e8-3e0d-428d-b661-289c16c82101.cloudapp.net
```

## <a name="delete-hello-application-gateway"></a>Eliminar puerta de enlace de aplicación Hola

puerta de enlace de aplicaciones de Hola toodelete:

1. Hola de uso `Stop-AzureApplicationGateway` puerta de enlace de cmdlet toostop Hola.
2. Hola de uso `Remove-AzureApplicationGateway` puerta de enlace de cmdlet tooremove Hola.
3. Compruebe dicha puerta de enlace de Hola se ha eliminado mediante el uso de hello `Get-AzureApplicationGateway` cmdlet.

Hello en el ejemplo siguiente se muestra hello `Stop-AzureApplicationGateway` cmdlet en la primera línea hello, seguido de la salida de hello.

```powershell
Stop-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

Una vez que la puerta de enlace de aplicaciones de hello está en estado detenido, use hello `Remove-AzureApplicationGateway` servicio de cmdlet tooremove Hola.

```powershell
Remove-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

se ha quitado tooverify que Hola servicio, puede usar hello `Get-AzureApplicationGateway` cmdlet. Este paso no es necesario.

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
.....
```

## <a name="next-steps"></a>Pasos siguientes

Si desea que tooconfigure la descarga de SSL, consulte [configurar una puerta de enlace de la aplicación para la descarga SSL](application-gateway-ssl.md).

Si desea tooconfigure una toouse de puerta de enlace de la aplicación con un equilibrador de carga interno, consulte [crear una puerta de enlace de la aplicación con un equilibrador de carga interno (ILB)](application-gateway-ilb.md).

Si desea obtener más información acerca de opciones de equilibrio de carga en general, vea:

* [Equilibrador de carga de Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

[scenario]: ./media/application-gateway-create-gateway/scenario.png
