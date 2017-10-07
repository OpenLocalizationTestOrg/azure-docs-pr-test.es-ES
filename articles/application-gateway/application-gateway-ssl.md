---
title: "aaaConfigure SSL descargar PowerShell - puerta de enlace de aplicaciones de Azure - clásico | Documentos de Microsoft"
description: "Este artículo proporciona instrucciones toocreate descargar usando una puerta de enlace de la aplicación con SSL Hola modelo de implementación clásico de Azure."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 63f28d96-9c47-410e-97dd-f5ca1ad1b8a4
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 5cb128015747ed4b71802cf751c80b60634601a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-classic-deployment-model"></a>Configurar una puerta de enlace de la aplicación para la descarga SSL mediante el modelo de implementación clásica de Hola

> [!div class="op_single_selector"]
> * [Portal de Azure](application-gateway-ssl-portal.md)
> * [PowerShell del Administrador de recursos de Azure](application-gateway-ssl-arm.md)
> * [Azure Classic PowerShell](application-gateway-ssl.md)
> * [CLI de Azure 2.0](application-gateway-ssl-cli.md)

Puerta de enlace de aplicación de Azure puede ser configurado tooterminate Hola Secure Sockets Layer (SSL) sesión en hello puerta de enlace tooavoid costoso SSL descifrado tareas toohappen en la granja de servidores de hello web. Descarga SSL también simplifica la administración de aplicación web de Hola y el programa de instalación del servidor front-end de Hola.

## <a name="before-you-begin"></a>Antes de empezar

1. Instalar versión más reciente de Hola de cmdlets de PowerShell de Azure de hello mediante Hola instalador de plataforma Web. Puede descargar e instalar la versión más reciente de Hola de hello **Windows PowerShell** sección de hello [página de descargas](https://azure.microsoft.com/downloads/).
2. Compruebe que tiene una red virtual de trabajo con una subred válida. Asegúrese de que no hay máquinas virtuales o las implementaciones de nube están usando la subred de Hola. puerta de enlace de aplicaciones de Hello debe ser por sí solo en una subred de red virtual.
3. deben existir servidores Hola configurar la puerta de enlace de aplicaciones de toouse Hola o tener asignados de sus puntos de conexión creados en la red virtual de Hola o con una dirección IP pública/VIP.

tooconfigure SSL descargar en una puerta de enlace de aplicaciones, Hola siguiendo los pasos en orden de hello mostrado:

1. [Creación de una puerta de enlace de aplicaciones](#create-an-application-gateway)
2. [Carga de certificados SSL](#upload-ssl-certificates)
3. [Configurar la puerta de enlace de Hola](#configure-the-gateway)
4. [Configuración de puerta de enlace de Hola de conjunto](#set-the-gateway-configuration)
5. [Iniciar la puerta de enlace de Hola](#start-the-gateway)
6. [Comprobar el estado de la puerta de enlace de Hola](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a>Creación de una puerta de enlace de aplicaciones

puerta de enlace de toocreate hello, use hello `New-AzureApplicationGateway` cmdlet, reemplazando los valores de hello por los suyos propios. La facturación de puerta de enlace de hello no se inicia en este momento. Facturación comienza en un paso posterior, cuando la puerta de enlace de Hola se ha iniciado correctamente.

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

se creó toovalidate que Hola puerta de enlace, puede usar hello `Get-AzureApplicationGateway` cmdlet.

En el ejemplo de Hola, *descripción*, *InstanceCount*, y *GatewaySize* son parámetros opcionales. Hola valor predeterminado de *InstanceCount* es 2, con un valor máximo de 10. Hola valor predeterminado de *GatewaySize* es Medium. Small y Large son otros valores disponibles. *VirtualIPs* y *DnsName* se muestran como en blanco porque no se inició aún la puerta de enlace de Hola. Estos valores se crean una vez que la puerta de enlace de hello está en estado de ejecución de Hola.

```powershell
Get-AzureApplicationGateway AppGwTest
```

## <a name="upload-ssl-certificates"></a>Carga de certificados SSL

Use `Add-AzureApplicationGatewaySslCertificate` certificado de servidor hello tooupload en *pfx* puerta de enlace de aplicaciones de toohello de formato. nombre del certificado Hello es un nombre elegido por el usuario y debe ser único dentro de la puerta de enlace de aplicaciones de Hola. Este certificado es tooby que se hace referencia este nombre en todas las operaciones de administración de certificados en la puerta de enlace de aplicaciones de Hola.

Este ejemplo siguiente muestra el cmdlet de hello, reemplazar valores de hello en el ejemplo de Hola por los suyos propios.

```powershell
Add-AzureApplicationGatewaySslCertificate  -Name AppGwTest -CertificateName GWCert -Password <password> -CertificateFile <full path toopfx file>
```

A continuación, validar la carga del certificado de Hola. Hola de uso `Get-AzureApplicationGatewayCertificate` cmdlet.

Ejemplo hello cmdlet muestra en la primera línea hello, seguido de salida de hello.

```powershell
Get-AzureApplicationGatewaySslCertificate AppGwTest
```

```
VERBOSE: 5:07:54 PM - Begin Operation: Get-AzureApplicationGatewaySslCertificate
VERBOSE: 5:07:55 PM - Completed Operation: Get-AzureApplicationGatewaySslCertificate
Name           : SslCert
SubjectName    : CN=gwcert.app.test.contoso.com
Thumbprint     : AF5ADD77E160A01A6......EE48D1A
ThumbprintAlgo : sha1RSA
State..........: Provisioned
```

> [!NOTE]
> contraseña del certificado Hello tiene toobe entre 4 too12 caracteres, letras o números. No se aceptan caracteres especiales.

## <a name="configure-hello-gateway"></a>Configurar la puerta de enlace de Hola

Una configuración de puerta de enlace de aplicaciones consta de varios valores. se pueden acumular los valores de Hello configuración de hello tooconstruct juntos.

los valores de Hello son:

* **Grupo de servidores de back-end:** Hola lista de direcciones IP de servidores de back-end de Hola. direcciones IP en Hello lista deben pertenecer o subred de red virtual toohello o deben ser una dirección IP pública/VIP.
* **Configuración del grupo de servidores back-end:** cada grupo tiene una configuración en la que se incluye el puerto, el protocolo y la afinidad basada en cookies. Esta configuración está ligada tooa grupo y son servidores de tooall aplicados en el grupo de Hola.
* **Puerto front-end:** este puerto es Hola pública que se abre en la puerta de enlace de aplicaciones de Hola. Tráfico llega a este puerto y, a continuación, obtiene redirigido tooone de servidores de back-end de Hola.
* **Agente de escucha:** agente de escucha de hello tiene un puerto front-end, un protocolo (Http o Https, estos valores distinguen mayúsculas de minúsculas) y el nombre del certificado SSL hello (si se descarga la configuración de SSL).
* **Regla:** regla Hola enlaza el agente de escucha de Hola y el grupo de servidores de back-end de Hola y define qué tráfico de Hola de grupo de servidor back-end debe ser dirigido toowhen llega a un agente de escucha determinado. Actualmente, solo Hola *básico* se admite la regla. Hola *básica* regla es la distribución de carga round robin.

**Notas de configuración adicionales**

Para la configuración de certificados SSL, Hola protocolo en **HttpListener** debe cambiar también*Https* (con distinción entre mayúsculas y minúsculas). Hola **SslCert** elemento se agrega demasiado**HttpListener** con hello valor establecido toohello mismo nombre tal y como se utiliza en la carga de Hola de sección de certificados SSL anterior. puerto front-end de Hello deben too443 actualizada.

**tooenable basado en cookies afinidad**: una puerta de enlace de la aplicación puede ser configurado tooensure que una solicitud de una sesión de cliente siempre está dirigido toohello misma máquina virtual en la granja de servidores de hello web. Este escenario se realiza mediante la inyección de una cookie de sesión que permita el tráfico de toodirect de puerta de enlace de hello adecuadamente. establece la afinidad basado en cookies tooenable, **CookieBasedAffinity** demasiado*habilitado* en hello **BackendHttpSettings** elemento.

Puede llevar a cabo la configuración mediante la creación de un objeto de configuración o usando un archivo XML de configuración.
usar la configuración mediante el uso de una archivo XML de configuración de tooconstruct Hola siguiente ejemplo:

**Ejemplo XML de configuración**

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations />
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>443</Port>
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
            <Protocol>Https</Protocol>
            <SslCert>GWCert</SslCert>
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

A continuación, configure la puerta de enlace de aplicaciones de Hola. Puede usar hello `Set-AzureApplicationGatewayConfig` cmdlet con un objeto de configuración o con un archivo XML de configuración.

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

## <a name="start-hello-gateway"></a>Iniciar la puerta de enlace de Hola

Una vez que se ha configurado la puerta de enlace de hello, usar hello `Start-AzureApplicationGateway` puerta de enlace de cmdlet toostart Hola. La facturación de una puerta de enlace de la aplicación comienza después de puerta de enlace de Hola se ha iniciado correctamente.

> [!NOTE]
> Hola `Start-AzureApplicationGateway` cmdlet podría tardar hasta toofinish too15-20 minutos.
>
>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a>Comprobar el estado de la puerta de enlace de Hola

Hola de uso `Get-AzureApplicationGateway` estado de cmdlet toocheck Hola de puerta de enlace de Hola. Si `Start-AzureApplicationGateway` se realizó correctamente en el paso anterior de hello, *estado* debe estar en ejecución, y *VirtualIPs* y *DnsName* debe tener las entradas válidas.

Este ejemplo muestra una puerta de enlace de la aplicación que está activo, ejecutando y un tráfico tootake listo.

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest2
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
VirtualIPs    : {23.96.22.241}
DnsName       : appgw-4c960426-d1e6-4aae-8670-81fd7a519a43.cloudapp.net
```

## <a name="next-steps"></a>Pasos siguientes

Si desea obtener más información acerca de opciones de equilibrio de carga en general, vea:

* [Equilibrador de carga de Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

