---
title: puerta de enlace de aplicaciones de Azure con el equilibrador de carga interno aaaUsing | Documentos de Microsoft
description: "Esta página proporcionan instrucciones tooconfigure una puerta de enlace de aplicaciones de Azure con un extremo con equilibrio de carga interno"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 7403d28e-909f-46a2-b282-43a8e942f53c
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 272ef84a02f92a8521c35aad6f1d9f9bf1675718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb"></a>Creación de una puerta de enlace de aplicaciones con un equilibrador de carga interno (ILB)

> [!div class="op_single_selector"]
> * [Azure Classic PowerShell](application-gateway-ilb.md)
> * [PowerShell del Administrador de recursos de Azure](application-gateway-ilb-arm.md)

Puerta de enlace de aplicaciones puede configurarse con un orientado a dirección IP virtual de internet o con un extremo interno no expuesta toohello internet, también conocido como punto de conexión de equilibrador de carga interno (ILB). Configurar puerta de enlace de hello con un ILB es útil para aplicaciones de línea de negocio internas no expuestas toointernet. También es útil para los niveles de servicio/dentro de una aplicación de varios niveles, que se encuentra en un toointernet no expuesto el límite de seguridad, pero aún requieren la distribución de la carga de round robin, adherencia de sesión o terminación SSL. Este artículo le guiará a través de hello pasos tooconfigure una puerta de enlace de la aplicación con un ILB.

## <a name="before-you-begin"></a>Antes de empezar

1. Instale la versión más reciente de los cmdlets de PowerShell de Azure de hello usan Hola instalador de plataforma Web. Puede descargar e instalar la versión más reciente de Hola de hello **Windows PowerShell** sección de hello [página de descarga](https://azure.microsoft.com/downloads/).
2. Compruebe que tiene una red virtual que funciona con una subred válida.
3. Compruebe que dispone de servidores back-end en la red virtual de hello, o con una dirección IP pública/VIP asignada.

toocreate una puerta de enlace de aplicaciones, realizar Hola pasos en orden de hello indicado. 

1. [Creación de una puerta de enlace de aplicaciones](#create-a-new-application-gateway)
2. [Configurar la puerta de enlace de Hola](#configure-the-gateway)
3. [Configuración de puerta de enlace de Hola de conjunto](#set-the-gateway-configuration)
4. [Iniciar la puerta de enlace de Hola](#start-the-gateway)
5. [Compruebe la puerta de enlace de Hola](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a>Creación de una puerta de enlace de aplicaciones:

**puerta de enlace de hello toocreate**, usar hello `New-AzureApplicationGateway` cmdlet, reemplazando los valores de hello por los suyos propios. Tenga en cuenta que la facturación de puerta de enlace de hello no se inicia en este momento. Facturación comienza en un paso posterior, cuando la puerta de enlace de Hola se ha iniciado correctamente.

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

```
VERBOSE: 4:31:35 PM - Begin Operation: New-AzureApplicationGateway 
VERBOSE: 4:32:37 PM - Completed Operation: New-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   55ef0460-825d-2981-ad20-b9a8af41b399
```

**toovalidate** que se creó la puerta de enlace de hello, puede usar hello `Get-AzureApplicationGateway` cmdlet. 

En el ejemplo de Hola, *descripción*, *InstanceCount*, y *GatewaySize* son parámetros opcionales. Hola valor predeterminado de *InstanceCount* es 2, con un valor máximo de 10. Hola valor predeterminado de *GatewaySize* es Medium. Small y Large son otros valores disponibles. *VIP* y *DnsName* se muestran como en blanco porque no se inició aún la puerta de enlace de Hola. Estos se crean una vez que la puerta de enlace de hello está en estado de ejecución de Hola. 

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 4:39:39 PM - Begin Operation:
Get-AzureApplicationGateway VERBOSE: 4:39:40 PM - Completed 
Operation: Get-AzureApplicationGateway
Name: AppGwTest    
Description: 
VnetName: testvnet1 
Subnets: {Subnet-1} 
InstanceCount: 2 
GatewaySize: Medium 
State: Stopped 
VirtualIPs: 
DnsName:
```

## <a name="configure-hello-gateway"></a>Configurar la puerta de enlace de Hola
Una configuración de puerta de enlace de aplicaciones consta de varios valores. se pueden acumular los valores de Hello configuración de hello tooconstruct juntos.

los valores de Hello son:

* **Grupo de servidores de back-end:** Hola lista de direcciones IP de servidores de back-end de Hola. direcciones IP en Hello lista deben pertenecer o subred de red virtual toohello o deben ser una dirección IP pública/VIP. 
* **Configuración del grupo de servidores back-end** : cada grupo tiene una configuración como el puerto, el protocolo y la afinidad basada en cookies. Esta configuración está ligada tooa grupo y son servidores de tooall aplicados en el grupo de Hola.
* **Puerto de front-end:** este puerto es el puerto público Hola abierto en la puerta de enlace de aplicaciones de Hola. Tráfico llega a este puerto y, a continuación, obtiene redirigida tooone de servidores de back-end de Hola.
* **Agente de escucha:** agente de escucha de hello tiene un puerto de front-end, un protocolo (Http o Https, estos distinguen mayúsculas de minúsculas) y el nombre del certificado SSL hello (si se descarga la configuración de SSL). 
* **Regla:** regla Hola enlaza el agente de escucha de Hola y de grupo de servidores de back-end de Hola y define qué tráfico de hello del grupo de servidor back-end debe ser dirigido toowhen llega a un agente de escucha determinado. Actualmente, solo Hola *básico* se admite la regla. Hola *básica* regla es la distribución de carga round robin.

Puede llevar a cabo la configuración mediante la creación de un objeto de configuración o usando un archivo XML de configuración. tooconstruct la configuración mediante el uso de un archivo XML de configuración, use Hola de ejemplo a continuación.

Tenga en cuenta los siguiente hello:

* Hola *FrontendIPConfigurations* elemento describe hello ILB detalles pertinentes para configurar la puerta de enlace de aplicaciones con un ILB. 
* IP de front-end Hello *tipo* debe establecerse too'Private'
* Hola *StaticIPAddress* debe establecerse en qué Hola puerta de enlace recibe el tráfico IP interna toohello deseado. Tenga en cuenta que hello *StaticIPAddress* elemento es opcional. Si no es así conjunto, se elige una IP interna disponible de la subred de hello implementado. 
* Hola valo hello *nombre* especificado en el elemento *FrontendIPConfiguration* debe usarse en hello HTTPListener *FrontendIP* toohello toorefer de elemento FrontendIPConfiguration.
  
  **Ejemplo XML de configuración**
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations>
        <FrontendIPConfiguration>
            <Name>fip1</Name> 
            <Type>Private</Type> 
            <StaticIPAddress>10.0.0.10</StaticIPAddress> 
        </FrontendIPConfiguration>
    </FrontendIPConfigurations>
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
            <FrontendIP>fip1</FrontendIP>
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


## <a name="set-hello-gateway-configuration"></a>Configuración de puerta de enlace de Hola de conjunto
A continuación, se establecerá la puerta de enlace de aplicaciones de Hola. Puede usar hello `Set-AzureApplicationGatewayConfig` cmdlet con un objeto de configuración, o con un archivo XML de configuración. 

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

```
VERBOSE: 7:54:59 PM - Begin Operation: Set-AzureApplicationGatewayConfig 
VERBOSE: 7:55:32 PM - Completed Operation: Set-AzureApplicationGatewayConfig
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   9b995a09-66fe-2944-8b67-9bb04fcccb9d
```

## <a name="start-hello-gateway"></a>Iniciar la puerta de enlace de Hola

Una vez que se ha configurado la puerta de enlace de hello, usar hello `Start-AzureApplicationGateway` puerta de enlace de cmdlet toostart Hola. La facturación de una puerta de enlace de la aplicación comienza después de puerta de enlace de Hola se ha iniciado correctamente. 

> [!NOTE]
> Hola `Start-AzureApplicationGateway` cmdlet podría tardar hasta toocomplete too15-20 minutos. 
> 
> 

```powershell
Start-AzureApplicationGateway AppGwTest 
```

```
VERBOSE: 7:59:16 PM - Begin Operation: Start-AzureApplicationGateway 
VERBOSE: 8:05:52 PM - Completed Operation: Start-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   fc592db8-4c58-2c8e-9a1d-1c97880f0b9b
```

## <a name="verify-hello-gateway-status"></a>Comprobar el estado de la puerta de enlace de Hola

Hola de uso `Get-AzureApplicationGateway` estado de cmdlet toocheck Hola de puerta de enlace. Si `Start-AzureApplicationGateway` se realizó correctamente en el paso anterior de hello, estado de hello debería ser *ejecuta*, Hola Vip y DnsName debe tener las entradas válidas. Ejemplo hello cmdlet muestra en la primera línea hello, seguido de salida de hello. En este ejemplo, puerta de enlace de hello está ejecutando y está listo tootake tráfico. 

> [!NOTE]
> se configura la puerta de enlace de aplicaciones de Hello tooaccept tráfico en hello configurado extremo ILB de 10.0.0.10 en este ejemplo.

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
VirtualIPs    : {10.0.0.10}
DnsName       : appgw-b2a11563-2b3a-4172-a4aa-226ee4c23eed.cloudapp.net
```

## <a name="next-steps"></a>Pasos siguientes
Si desea obtener más información acerca de opciones de equilibrio de carga en general, vea:

* [Equilibrador de carga de Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

