---
title: "equilibrador de carga de aaaCreate una conexión a Internet para los servicios de nube de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una conexión a Internet equilibrador de carga de modelo de implementación clásica para servicios en la nube"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 0bb16f96-56a6-429f-88f5-0de2d0136756
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: d93cf76d417cbfc744cf07ba48c43a63cc14df69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-for-cloud-services"></a>Introducción a la creación de un equilibrador de carga orientado a Internet para servicios en la nube

> [!div class="op_single_selector"]
> * [Portal de Azure clásico](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [CLI de Azure](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Servicios en la nube de Azure](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Antes de trabajar con recursos de Azure, es importante toounderstand que Azure tiene dos modelos de implementación: Administrador de recursos de Azure y clásico. Asegúrese de que comprende los [modelos de implementación y las herramientas](../azure-classic-rm.md) antes de trabajar con recursos de Azure. Puede ver documentación de Hola de distintas herramientas, haga clic en las pestañas de hello en parte superior de Hola de este artículo. Este artículo trata el modelo de implementación clásica de Hola. También puede [Obtenga información acerca de cómo toocreate una conexión a Internet cargar equilibrador mediante Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).

Servicios en la nube se configuran automáticamente con un equilibrador de carga y se pueden personalizar mediante el modelo de servicio de Hola.

## <a name="create-a-load-balancer-using-hello-service-definition-file"></a>Crear un equilibrador de carga con el archivo de definición de servicio de Hola

Puede aprovechar hello Azure SDK para .NET 2.5 tooupdate su servicio en la nube. Configuración de punto de conexión de servicios en la nube se realiza en hello [definición del servicio](https://msdn.microsoft.com/library/azure/gg557553.aspx) archivo .csdef.

Hello en el ejemplo siguiente se muestra cómo se configura un archivo servicedefinition.csdef para una implementación de nube:

La comprobación de fragmento de código de hello hello .csdef archivo generado por una implementación de nube, puede ver Hola extremo externo configurado toouse puertos HTTP en el puerto 10000 y 10001, 10002.

```xml
<ServiceDefinition name=“Tenant“>
    <WorkerRole name=“FERole” vmsize=“Small“>
<Endpoints>
    <InputEndpoint name=“FE_External_Http” protocol=“http” port=“10000“ />
    <InputEndpoint name=“FE_External_Tcp“  protocol=“tcp“  port=“10001“ />
    <InputEndpoint name=“FE_External_Udp“  protocol=“udp“  port=“10002“ />

    <InputEndpointname=“HTTP_Probe” protocol=“http” port=“80” loadBalancerProbe=“MyProbe“ />

    <InstanceInputEndpoint name=“InstanceEP” protocol=“tcp” localPort=“80“>
        <AllocatePublicPortFrom>
            <FixedPortRange min=“10110” max=“10120“  />
        </AllocatePublicPortFrom>
    </InstanceInputEndpoint>
    <InternalEndpoint name=“FE_InternalEP_Tcp” protocol=“tcp“ />
</Endpoints>
    </WorkerRole>
</ServiceDefinition>
```

## <a name="check-load-balancer-health-status-for-cloud-services"></a>Comprobación del estado de mantenimiento del equilibrador de carga para servicios en la nube

Hola te mostramos un ejemplo de un sondeo de estado:

```xml
<LoadBalancerProbes>
    <LoadBalancerProbe name=“MyProbe” protocol=“http” path=“Probe.aspx” intervalInSeconds=“5” timeoutInSeconds=“100“ />
</LoadBalancerProbes>
```

Hello equilibrador de carga combina información de Hola de punto de conexión de Hola y Hola de hello sondeo toocreate una dirección URL en forma de Hola de `http://{DIP of VM}:80/Probe.aspx` que puede ser usado tooquery Hola mantenimiento del servicio de Hola.

Hello servicio detecta las comprobaciones periódicas de hello misma dirección IP. Se trata de una solicitud de sondeo de estado de hello procedentes de host de hello del nodo de Hola donde se ejecuta la máquina virtual de Hola. servicio de Hello tiene toorespond con un código de estado HTTP 200 para tooassume de equilibrador de carga de Hola que Hola servicio es correcto. Cualquier otro código de estado HTTP de código (por ejemplo 503) directamente toma Hola máquina virtual fuera de la rotación.

definición de sondeo de Hello también controla la frecuencia de Hola de sondeo de Hola. En nuestro caso anterior, el equilibrador de carga de hello es sondeo extremo Hola cada 5 segundos. Si no se recibe ninguna respuesta positiva de 10 segundos (dos intervalos de sondeo), se supone que el sondeo de hello hacia abajo, y máquina virtual de Hola se realiza fuera de la rotación. De forma similar, si el servicio de hello está fuera de la rotación y se recibe una respuesta positiva, servicio de Hola se vuelve a colocar toorotation inmediatamente. Si el servicio de hello fluctúa entre correcto y negativa, equilibrador de carga de hello puede decidir reintroducción hello toodelay de hello servicio back-toorotation hasta que ha sido correcto durante un número de sondeos.

Compruebe el esquema de definición de servicio de Hola para hello [sondeo de estado](https://msdn.microsoft.com/library/azure/jj151530.aspx) para obtener más información.

## <a name="next-steps"></a>Pasos siguientes

[Introducción a la configuración de un equilibrador de carga interno](load-balancer-get-started-ilb-arm-ps.md)

[Configuración de un modo de distribución del equilibrador de carga](load-balancer-distribution-mode.md)

[Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga](load-balancer-tcp-idle-timeout.md)

