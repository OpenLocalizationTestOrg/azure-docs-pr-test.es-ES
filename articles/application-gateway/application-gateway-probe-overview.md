---
title: "aaaHealth información general de supervisión para la puerta de enlace de aplicaciones de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de hello las funciones de puerta de enlace de aplicaciones de Azure de seguimiento"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7eeba328-bb2d-4d3e-bdac-7552e7900b7f
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: gwallace
ms.openlocfilehash: 5091d80394a354ff849ce7ccee8cc9d2fd0456db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-health-monitoring-overview"></a>Información general sobre la supervisión de estado de la puerta de enlace de aplicaciones

Azure puerta de enlace de aplicaciones de forma predeterminada se supervisa el estado de Hola de todos los recursos de su grupo back-end y se quita automáticamente cualquier recurso que se considera incorrecto del grupo de Hola. Puerta de enlace de aplicación continúa instancias toomonitor hello en mal estado y se agregan hacer copia de grupo de back-end de toohello correcto una vez que estén disponibles y responden toohealth sondeos. Puerta de enlace de aplicación envía Hola sondeos de estado con hello mismo puerto que se define en la configuración de HTTP de back-end de Hola. Esta configuración garantiza que sondeo Hola está probando Hola mismo número de puerto que los clientes sería utilizar back-end de tooconnect toohello.

![ejemplo de sondeo de Application Gateway][1]

En suma toousing predeterminado sondeo supervisión de estado, también puede personalizar toosuit de sondeo de estado de hello requisitos de su aplicación. En este artículo trataremos ambos sondeos de estado: el personalizado y el predeterminado.

> [!NOTE]
> Si hay un NSG de subred de puerta de enlace de aplicaciones, intervalos de puertos 65503-65534 deben abrirse en la subred de puerta de enlace de aplicación hello para el tráfico entrante. Estos puertos son necesarios para toowork de API de mantenimiento de hello back-end.

## <a name="default-health-probe"></a>Sondeo de estado predeterminado

Una puerta de enlace de aplicaciones configura automáticamente un sondeo de estado predeterminado cuando no hay ningún sondeo personalizado configurado. Hola supervisión comportamiento funciona convirtiendo que resuelve una dirección IP toohello de solicitud HTTP configurados para el grupo de back-end de Hola. Para los sondeos de forma predeterminada si Hola back-end http se configura para HTTPS, sondeo hello usa HTTPS como tootest y mantenimiento de hello back-ends.

Por ejemplo: configurar la aplicación puerta de enlace toouse servidores back-end A, B y C tooreceive HTTP tráfico de red en el puerto 80. supervisión de estado de saludo predeterminado comprueba tres servidores de hello cada 30 segundos para una respuesta HTTP correcto. Una respuesta HTTP correcta tiene un [código de estado](https://msdn.microsoft.com/library/aa287675.aspx) entre 200 y 399.

Si se produce un error en la comprobación de sondeo de hello predeterminada para que el servidor, puerta de enlace de aplicaciones de Hola quita de su grupo back-end y el tráfico de red deje de fluir toothis server. sondeo de Hello predeterminado conservará toocheck para servidor un cada 30 segundos. Cuando el servidor A responde correctamente tooone solicitud de un sondeo de estado de manera predeterminada, se agrega nuevo como grupo de back-end de toohello correcto y comienza a tráfico fluir toohello servidor nuevo.

### <a name="default-health-probe-settings"></a>Configuración de sondeo de estado predeterminado

| Propiedad de sondeo | Valor | Description |
| --- | --- | --- |
| Dirección URL de sondeo |http://127.0.0.1:\<puerto\>/ |Ruta de acceso URL |
| Intervalo |30 |Intervalo de sondeo en segundos |
| Tiempo de espera |30 |Tiempo de espera del sondeo en segundos |
| Umbral incorrecto |3 |Número de reintentos de sondeo. servidor de back-end de Hola está marcado después de recuento de errores de sondeo consecutivos Hola alcanza el umbral de estado incorrecto de Hola. |

> [!NOTE]
> Hello puerto es Hola mismo puerto como configuración de HTTP de back-end de Hola.

sondeo de Hello predeterminado solo examina http://127.0.0.1:\<puerto\> toodetermine estado de mantenimiento. Si necesita tooconfigure Hola mantenimiento sondeo toogo tooa dirección URL personalizada o modificar las opciones de configuración, debe usar sondeos personalizados como se describe en hello pasos:

## <a name="custom-health-probe"></a>Sondeo de estado personalizado

Sondeos personalizados le permiten toohave un control más granular sobre supervisión de estado de Hola. Cuando se usa sondeos personalizados, puede configurar intervalo de sondeo de saludo, tootest de dirección URL y la ruta de acceso de Hola y cuántos tooaccept de respuestas error antes de marcar la instancia de grupo de servidores de back-end de hello como en mal estado.

### <a name="custom-health-probe-settings"></a>Configuración de sondeo de estado personalizado

Hello tabla siguiente proporciona las definiciones de propiedades de Hola de un sondeo de estado personalizado.

| Propiedad de sondeo | Description |
| --- | --- |
| Nombre |Nombre del sondeo de Hola. También se denomina sondeo de toohello toorefer usado en la configuración de HTTP de back-end. |
| Protocol |Usa el protocolo de sondeo de hello toosend. sondeo de Hello usa el protocolo de hello definido en la configuración de HTTP de back-end de Hola |
| Host |Sondeo de Hola de toosend de nombre de host. Solo se puede aplicar cuando se ha configurado un entorno multisitio en Application Gateway; de lo contrario hay que usar '127.0.0.1'. Este valor es distinto del nombre de host de máquina virtual. |
| Ruta de acceso |Ruta de acceso relativa del sondeo de Hola. ruta de acceso válida de Hola se inicia desde '/'. |
| Intervalo |Intervalo de sondeo en segundos. Este valor es el intervalo de tiempo de hello entre dos sondeos consecutivos. |
| Tiempo de espera |Tiempo de espera del sondeo en segundos. Si no se recibe una respuesta válida dentro de este período de tiempo de espera, el sondeo de Hola se marcará como incorrecta.  |
| Umbral incorrecto |Número de reintentos de sondeo. servidor de back-end de Hola está marcado después de recuento de errores de sondeo consecutivos Hola alcanza el umbral de estado incorrecto de Hola. |

> [!IMPORTANT]
> Si la puerta de enlace de aplicaciones está configurada para un único sitio, por hello predeterminado Host nombre debe especificarse como "127.0.0.1", a menos que en caso contrario, se configura en sondeo personalizado.
> Como referencia un sondeo personalizado se envía demasiado\<protocolo\>://\<host\>:\<puerto\>\<ruta de acceso\>. Hello puerto utilizado será Hola mismo puerto, tal como se define en la configuración de HTTP de back-end de Hola.

## <a name="next-steps"></a>Pasos siguientes
Después de aprendizaje sobre la supervisión de estado de puerta de enlace de aplicaciones, puede configurar un [sondeo de estado personalizado](application-gateway-create-probe-portal.md) Hola portal de Azure o un [sondeo de estado personalizado](application-gateway-create-probe-ps.md) con PowerShell y hello Azure Resource Manager modelo de implementación.

[1]: ./media/application-gateway-probe-overview/appgatewayprobe.png
