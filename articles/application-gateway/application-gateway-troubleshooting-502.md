---
title: "errores de aplicación de Azure puerta de enlace Gateway incorrecta (502) aaaTroubleshoot | Documentos de Microsoft"
description: "Obtenga información acerca de cómo errores tootroubleshoot 502 de puerta de enlace de aplicaciones"
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 1d431ead-d318-47d8-b3ad-9c69f7e08813
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: a50f736ac157256a53f6fbe3a208f0c11dd58f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-bad-gateway-errors-in-application-gateway"></a>Solución de errores de puerta de enlace incorrecta en el servicio Puerta de enlace de aplicaciones

Obtenga información acerca de cómo tootroubleshoot (502) (errores) puerta de enlace errónea reciben al usar la puerta de enlace de aplicaciones.

## <a name="overview"></a>Información general

Después de configurar una puerta de enlace de aplicaciones, uno de los errores de Hola que los usuarios pueden encontrar es "Error de servidor: 502: el servidor Web recibió una respuesta no válida mientras actuaba como un servidor de puerta de enlace o proxy". Este error puede ocurrir debido toohello siguiente razones principales:

* [El grupo back-end de la instancia de Azure Application Gateway no está configurado o está vacío](#empty-backendaddresspool).
* Ninguna de las máquinas virtuales de Hola o instancias de [conjunto de escalado de máquinas virtuales están en buen estado](#unhealthy-instances-in-backendaddresspool).
* Máquinas virtuales o instancias del conjunto de escalado de VM de back-end son [no responde sondeo de estado predeterminado de toohello](#problems-with-default-health-probe.md).
* [La configuración de las sondas de estado personalizadas](#problems-with-custom-health-probe.md) no es válida o adecuada.
* [El tiempo de espera de solicitud se superó o hay problemas de conectividad](#request-time-out) con las solicitudes de usuario.

## <a name="empty-backendaddresspool"></a>Valor de BackendAddressPool vacío

### <a name="cause"></a>Causa

Si Hola puerta de enlace de aplicaciones no tiene ninguna máquina virtual o conjunto de escalado de VM configurada en el grupo de direcciones de back-end de hello, no se pueden enrutar cualquier solicitud de cliente y genera un error de puerta de enlace errónea.

### <a name="solution"></a>Solución

Asegúrese de que el grupo de direcciones de back-end de hello no está vacía. Puede hacerlo mediante PowerShell, la CLI o el Portal.

```powershell
Get-AzureRmApplicationGateway -Name "SampleGateway" -ResourceGroupName "ExampleResourceGroup"
```

salida de Hello de hello anterior cmdlet debe contener grupo de direcciones de back-end no está vacío. A continuación, se muestra un ejemplo en el que se devuelven dos grupos que están configurados con direcciones IP o FQDN de máquinas virtuales de back-end. Hola estado de aprovisionamiento de hello BackendAddressPool debe ser "realizado."

BackendAddressPoolsText:

```json
[{
    "BackendAddresses": [{
        "ipAddress": "10.0.0.10",
        "ipAddress": "10.0.0.11"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool01",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool01"
}, {
    "BackendAddresses": [{
        "Fqdn": "xyx.cloudapp.net",
        "Fqdn": "abc.cloudapp.net"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool02",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool02"
}]
```

## <a name="unhealthy-instances-in-backendaddresspool"></a>Instancias incorrectas en BackendAddressPool

### <a name="cause"></a>Causa

Si todas las instancias de Hola de BackendAddressPool tienen un estado incorrecto, puerta de enlace de aplicaciones no tendría cualquier solicitud de usuario tooroute de back-end. También pueden caso hello cuando instancias de back-end están en buen Estados, pero no tiene la aplicación hello necesario implementada.

### <a name="solution"></a>Solución

Asegúrese de que las instancias de hello están en buen estadas y aplicación hello está configurado correctamente. Compruebe si hay instancias de back-end de hello toorespond pueda tooa ping desde otra máquina virtual de Hola misma red virtual. Si se configura con un punto de conexión público, asegúrese de que una aplicación web de explorador solicitud toohello es reparables por.

## <a name="problems-with-default-health-probe"></a>Problemas con la sonda de estado predeterminada

### <a name="cause"></a>Causa

502 (errores) también pueden ser indicadores frecuentes que Hola de sondeo de estado predeterminado es no se puede tooreach máquinas virtuales de back-end. Cuando se aprovisiona una instancia de puerta de enlace de aplicaciones, se configura automáticamente un sondeo de estado predeterminado tooeach BackendAddressPool mediante las propiedades de hello BackendHttpSetting. Ningún usuario de entrada se tooset requiere este sondeo. En concreto, cuando se configura una regla de equilibrio de carga, se crea una asociación entre un elemento BackendHttpSetting y otro BackendAddressPool. Un sondeo predeterminado está configurado para cada una de estas asociaciones y una instancia de tooeach de conexión de comprobación de estado periódicas en Hola BackendAddressPool en hello el puerto especificado en el elemento de hello BackendHttpSetting inicia la puerta de enlace de aplicaciones. Tabla siguiente enumera los valores de hello asociados de sondeo de estado de hello predeterminado.

| Propiedad de sondeo | Valor | Description |
| --- | --- | --- |
| Dirección URL de sondeo |http://127.0.0.1/ |Ruta de acceso URL |
| Intervalo |30 |Intervalo de sondeo en segundos |
| Tiempo de espera |30 |Tiempo de espera del sondeo en segundos |
| Umbral incorrecto |3 |Número de reintentos de sondeo. servidor de back-end de Hola está marcado después de recuento de errores de sondeo consecutivos Hola alcanza el umbral de estado incorrecto de Hola. |

### <a name="solution"></a>Solución

* Asegúrese de que se ha configurado un sitio predeterminado y de que está escuchando en 127.0.0.1.
* Si BackendHttpSetting especifica un puerto distinto del 80, sitio predeterminado de hello debe ser toolisten configurado en ese puerto.
* Hello toohttp://127.0.0.1:port de llamada debe devolver un código de resultado HTTP 200. Esto se debe devolver en tiempo de espera de 30 seg Hola.
* Asegúrese de que el puerto configurado está abierto y que no existen reglas de firewall ni grupos de seguridad de red de Azure, que bloquee el tráfico entrante o saliente en el puerto de hello configurado.
* Si se usa máquinas virtuales de Azure clásicas o servicio en la nube con el FQDN o una dirección IP pública, asegúrese de que Hola correspondiente [extremo](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) se abre.
* Si Hola máquina virtual se configura a través del Administrador de recursos de Azure y está fuera de la red virtual donde se implementa la puerta de enlace de aplicaciones, Hola [grupo de seguridad de red](../virtual-network/virtual-networks-nsg.md) debe configurarse acceso tooallow en hello deseado puerto.

## <a name="problems-with-custom-health-probe"></a>Problemas con la sonda de estado personalizada

### <a name="cause"></a>Causa

Sondeo de estado personalizados permite comportamiento de búsqueda predeterminadas de toohello de flexibilidad adicional. Cuando se usa sondeos personalizados, los usuarios pueden configurar intervalo de sondeo de saludo, dirección URL de hello y tootest de ruta de acceso y cuántos tooaccept de respuestas error antes de marcar la instancia de grupo de servidores de back-end de hello como en mal estado. Hola propiedades adicionales siguientes se agrega.

| Propiedad de sondeo | Description |
| --- | --- |
| Nombre |Nombre del sondeo de Hola. También se denomina sondeo de toohello toorefer usado en la configuración de HTTP de back-end. |
| Protocol |Usa el protocolo de sondeo de hello toosend. sondeo de Hello usa el protocolo de hello definido en la configuración de HTTP de back-end de Hola |
| Host |Sondeo de Hola de toosend de nombre de host. Solo es aplicable cuando se ha configurado un entorno multisitio en Puerta de enlace de aplicaciones. Es diferente al nombre de host de máquina virtual. |
| Ruta de acceso |Ruta de acceso relativa del sondeo de Hola. ruta de acceso válida de Hola se inicia desde '/'. sondeo de Hola se envía demasiado\<protocolo\>://\<host\>:\<puerto\>\<ruta de acceso\> |
| Intervalo |Intervalo de sondeo en segundos. Se trata de un intervalo de tiempo de hello entre dos sondeos consecutivos. |
| Tiempo de espera |Tiempo de espera del sondeo en segundos. Si no se recibe una respuesta válida dentro de este período de tiempo de espera, el sondeo de Hola se marcará como incorrecta. |
| Umbral incorrecto |Número de reintentos de sondeo. servidor de back-end de Hola está marcado después de recuento de errores de sondeo consecutivos Hola alcanza el umbral de estado incorrecto de Hola. |

### <a name="solution"></a>Solución

Validar ese Hola que sondeo de estado personalizado está configurado correctamente como Hola tabla anterior. Además toohello anterior pasos, asegúrese también de siguiente hello:

* Asegúrese de que sondeo Hola se ha especificado correctamente según hello [guía](application-gateway-create-probe-ps.md).
* Si la puerta de enlace de aplicaciones está configurada para un único sitio, por hello predeterminado Host nombre debe especificarse como "127.0.0.1", a menos que en caso contrario, se configura en sondeo personalizado.
* Asegúrese de que una llamada toohttp: / /\<host\>:\<puerto\>\<ruta de acceso\> devuelve un código de resultado HTTP 200.
* Asegúrese de intervalo de tiempo de espera y UnhealtyThreshold dentro de los intervalos de hello aceptable.
* Si el sondeo de uso de HTTPS, asegúrese de que ese servidor de back-end de hello no requiere SNI mediante la configuración de un certificado fallback en el propio servidor de back-end Hola. 
* Asegúrese de que intervalo y tiempo de espera, UnhealtyThreshold dentro de los intervalos de hello aceptable.

## <a name="request-time-out"></a>Tiempo de solicitud superado

### <a name="cause"></a>Causa

Cuando se recibe una solicitud de usuario, Application Gateway aplica Hola configurado reglas toohello solicitud y lo enruta la instancia de grupo de servidores de back-end de tooa. Espera un intervalo de tiempo una respuesta de la instancia de back-end de hello configurable. De forma predeterminada, este intervalo es de **30 segundos**. Si la instancia de Application Gateway no recibe una respuesta de una aplicación back-end en este intervalo, la solicitud de usuario generaría un error 502.

### <a name="solution"></a>Solución

Puerta de enlace de aplicaciones permite a usuarios tooconfigure esta configuración a través de BackendHttpSetting, que puede ser, a continuación, aplica toodifferent grupos. Estos grupos back-end pueden tener distintos elementos BackendHttpSetting y, por tanto, diferentes valores configurados para el tiempo de solicitud superado.

```powershell
    New-AzureRmApplicationGatewayBackendHttpSettings -Name 'Setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 60
```

## <a name="next-steps"></a>Pasos siguientes

Si hello pasos anteriores no resuelven Hola problema, abra un [incidencia de soporte técnico](https://azure.microsoft.com/support/options/).

