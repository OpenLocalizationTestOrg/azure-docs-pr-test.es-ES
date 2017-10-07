---
title: "aaaCreate un clásico de PowerShell de sondeo personalizado - puerta de enlace de aplicaciones de Azure - | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate personalizado de sondeo para puerta de enlace de aplicaciones mediante el uso de PowerShell en el modelo de implementación clásica de Hola"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 338a7be1-835c-48e9-a072-95662dc30f5e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 68332367c99328bd6456b0c339923765637be986
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-classic-by-using-powershell"></a>Creación de un sondeo personalizado para la Puerta de enlace de aplicaciones de Azure (clásica) mediante PowerShell

> [!div class="op_single_selector"]
> * [Portal de Azure](application-gateway-create-probe-portal.md)
> * [PowerShell de Azure Resource Manager](application-gateway-create-probe-ps.md)
> * [Azure Classic PowerShell](application-gateway-create-probe-classic-ps.md)

En este artículo, se agregará un sondeo personalizado tooan aplicación puerta de enlace existente con PowerShell. Sondeos personalizados son útiles para las aplicaciones que tienen una página de comprobación de mantenimiento específico o para aplicaciones que no proporcionan una respuesta correcta en la aplicación web de hello predeterminada.

> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. Obtenga información acerca de cómo demasiado[realizar estos pasos con el modelo del Administrador de recursos de hello](application-gateway-create-probe-ps.md).

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway"></a>Creación de una puerta de enlace de aplicaciones

toocreate una puerta de enlace de la aplicación:

1. Cree un recurso de Application Gateway.
2. Cree un archivo de configuración XML o un objeto de configuración.
3. Confirmar Hola configuración toohello recién creado recursos de puerta de enlace de aplicaciones.

### <a name="create-an-application-gateway-resource-with-a-custom-probe"></a>Creación de un recurso de puerta de enlace de aplicaciones con un sondeo personalizado

puerta de enlace de toocreate hello, use hello `New-AzureApplicationGateway` cmdlet, reemplazando los valores de hello por los suyos propios. La facturación de puerta de enlace de hello no se inicia en este momento. Facturación comienza en un paso posterior, cuando la puerta de enlace de Hola se ha iniciado correctamente.

Hello en el ejemplo siguiente se crea una puerta de enlace de la aplicación mediante el uso de una red virtual denominada "testvnet1" y una subred denominada "subred-1".

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

se creó toovalidate que Hola puerta de enlace, puede usar hello `Get-AzureApplicationGateway` cmdlet.

```powershell
Get-AzureApplicationGateway AppGwTest
```

> [!NOTE]
> Hola valor predeterminado de *InstanceCount* es 2, con un valor máximo de 10. Hola valor predeterminado de *GatewaySize* es Medium. Puede elegir entre Pequeño, Mediano y Grande.
> 
> 

*VirtualIPs* y *DnsName* se muestran como en blanco porque no se inició aún la puerta de enlace de Hola. Estos valores se crean una vez que la puerta de enlace de hello está en estado de ejecución de Hola.

### <a name="configure-an-application-gateway-by-using-xml"></a>Configuración de una puerta de enlace de aplicaciones mediante XML

En el siguiente ejemplo de Hola, utilice un tooconfigure de archivo XML todos los valores de puerta de enlace de la aplicación y, a continuación, confirmarlos toohello de recursos de puerta de enlace de aplicación.  

Copie Hola después tooNotepad de texto.

```xml
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
<FrontendIPConfigurations>
    <FrontendIPConfiguration>
        <Name>fip1</Name>
        <Type>Private</Type>
    </FrontendIPConfiguration>
</FrontendIPConfigurations>
<FrontendPorts>
    <FrontendPort>
        <Name>port1</Name>
        <Port>80</Port>
    </FrontendPort>
</FrontendPorts>
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
    </Probes>
    <BackendAddressPools>
    <BackendAddressPool>
        <Name>pool1</Name>
        <IPAddresses>
            <IPAddress>1.1.1.1</IPAddress>
            <IPAddress>2.2.2.2</IPAddress>
        </IPAddresses>
    </BackendAddressPool>
</BackendAddressPools>
<BackendHttpSettingsList>
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
</BackendHttpSettingsList>
<HttpListeners>
    <HttpListener>
        <Name>listener1</Name>
        <FrontendIP>fip1</FrontendIP>
    <FrontendPort>port1</FrontendPort>
        <Protocol>Http</Protocol>
    </HttpListener>
</HttpListeners>
<HttpLoadBalancingRules>
    <HttpLoadBalancingRule>
        <Name>lbrule1</Name>
        <Type>basic</Type>
        <BackendHttpSettings>setting1</BackendHttpSettings>
        <Listener>listener1</Listener>
        <BackendAddressPool>pool1</BackendAddressPool>
    </HttpLoadBalancingRule>
</HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

Editar valores de hello entre paréntesis Hola Hola elementos de configuración. Guarde el archivo hello con extensión .xml.

Hello en el ejemplo siguiente se muestra cómo toouse una tooset de archivo de configuración de tooload de puerta de enlace de aplicación Hola equilibrar el tráfico HTTP en el puerto público 80 y enviar tráfico de red en el puerto 80 de final de tooback entre dos direcciones IP mediante el uso de un sondeo personalizado.

> [!IMPORTANT]
> elemento de Hello protocolo Http o Https distingue mayúsculas de minúsculas.

Un nuevo elemento de configuración \<sondeo\> se agrega tooconfigure personalizado sondeos.

parámetros de configuración de Hello son:

|Parámetro|Descripción|
|---|---|
|**Name** |Nombre de referencia del sondeo personalizado. |
* **Protocol** | Protocolo usado (los valores posibles son HTTP o HTTPS).|
| **Host** y **Path** | Escriba la ruta de acceso de dirección URL que se invoca con el estado hello toodetermine de puerta de enlace de aplicaciones de Hola de instancia de Hola. Por ejemplo, si tiene un sitio Web http://contoso.com/, a continuación, el sondeo personalizado Hola puede configurarse para "http://contoso.com/path/custompath.htm" para la sonda comprueba toohave una respuesta HTTP correcta.|
| **Intervalo** | Configura las comprobaciones de intervalo de sondeo de hello en segundos.|
| **Tiempo de espera** | Define el tiempo de espera de sondeo de Hola para una comprobación de la respuesta HTTP.|
| **UnhealthyThreshold** | Hola número de respuestas error HTTP necesario tooflag Hola back-end de la instancia como *incorrecto*.|

nombre del sondeo Hola se hace referencia en hello \<BackendHttpSettings\> tooassign configuración qué grupo back-end utiliza la configuración de sondeo personalizado.

## <a name="add-a-custom-probe-tooan-existing-application-gateway"></a>Agregar un sondeo personalizado tooan aplicación puerta de enlace existente

Cambiar la configuración actual Hola de una puerta de enlace de la aplicación requiere tres pasos: obtener el archivo de configuración XML actual hello, modificar toohave un sondeo personalizado y configurar puerta de enlace de aplicaciones de hello con una nueva configuración de XML Hola.

1. Obtener el archivo XML de hello mediante `Get-AzureApplicationGatewayConfig`. Esta toobe XML de configuración de cmdlet exportaciones Hola había modificado tooadd una configuración de sondeo.

  ```powershell
  Get-AzureApplicationGatewayConfig -Name "<application gateway name>" -Exporttofile "<path toofile>"
  ```

1. Abra el archivo XML de hello en un editor de texto. Agregue una sección `<probe>` después de `<frontendport>`.

  ```xml
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
</Probes>
  ```

  En sección de backendHttpSettings de Hola de hello XML, agregue el nombre del sondeo de hello tal y como se muestra en el siguiente ejemplo de Hola:

  ```xml
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
  ```

  Guarde el archivo XML de hello.

1. Configuración de puerta de enlace de la aplicación de actualización Hola con el nuevo archivo XML hello mediante el uso de `Set-AzureApplicationGatewayConfig`. Este cmdlet actualiza la puerta de enlace de la aplicación con una nueva configuración de Hola.

```powershell
Set-AzureApplicationGatewayConfig -Name "<application gateway name>" -Configfile "<path toofile>"
```

## <a name="next-steps"></a>Pasos siguientes

Si desea que tooconfigure la descarga de capa de Sockets seguros (SSL), consulte [configurar una puerta de enlace de la aplicación para la descarga SSL](application-gateway-ssl.md).

Si desea tooconfigure una toouse de puerta de enlace de la aplicación con un equilibrador de carga interno, consulte [crear una puerta de enlace de la aplicación con un equilibrador de carga interno (ILB)](application-gateway-ilb.md).

