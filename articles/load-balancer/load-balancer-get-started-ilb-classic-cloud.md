---
title: aaaCreate un equilibrador de carga interno para servicios de nube de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate un interno cargar equilibrador de usar PowerShell en el modelo de implementación clásica de Hola"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 57966056-0f46-4f95-a295-483ca1ad135d
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: fe7975bca7bec3248626b0ad0fad6823e278ade2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-for-cloud-services"></a>Introducción a la creación de un equilibrador de carga interno (clásico) para servicios en la nube

> [!div class="op_single_selector"]
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [CLI de Azure](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [Cloud Services](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).  Este artículo incluye el uso de modelo de implementación clásica de Hola. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. Obtenga información acerca de cómo demasiado[realizar estos pasos con el modelo del Administrador de recursos de hello](load-balancer-get-started-ilb-arm-ps.md).

## <a name="configure-internal-load-balancer-for-cloud-services"></a>Configuración del equilibrador de carga interno para los servicios en la nube

El equilibrador de carga interno es compatible tanto con las máquinas virtuales como con los servicios en la nube. Un punto de conexión del equilibrador de carga interno creado en un servicio de nube que está fuera de una red virtual regional será accesible únicamente dentro de servicio en la nube Hola.

configuración de equilibrador de carga interno de Hello tiene toobe estableció durante la creación de hello de primera implementación de Hola Hola del servicio en nube, como se muestra en el siguiente ejemplo de Hola.

> [!IMPORTANT]
> Un requisito previo toorun Hola estos pasos es una red virtual ya creada para la implementación de nube de hello toohave. Necesitará Hola red virtual nombre y la subred nombre toocreate Hola equilibrio de carga interno.

### <a name="step-1"></a>Paso 1

Abra el archivo de configuración de servicio de hello (.cscfg) para la implementación de nube en Visual Studio y agregue Hola después Hola de toocreate sección Equilibrio de carga interno en hello última "`</Role>`" elemento de configuración de red de Hola.

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="name of hello load balancer">
        <FrontendIPConfiguration type="private" subnet="subnet-name" staticVirtualNetworkIPAddress="static-IP-address"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

Vamos a agregar valores de hello para el archivo de configuración de hello red tooshow aspecto que tendrá. En el ejemplo de Hola, suponga que crea una red virtual denominada "test_vnet" con una subred 10.0.0.0/24 denominados test_subnet y una dirección IP estática 10.0.0.4. equilibrador de carga de Hola se denominará PruebaCL.

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="testLB">
        <FrontendIPConfiguration type="private" subnet="test_subnet" staticVirtualNetworkIPAddress="10.0.0.4"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

Para obtener más información acerca del esquema de equilibrador de carga de hello, consulte [agregar equilibrador de carga](https://msdn.microsoft.com/library/azure/dn722411.aspx).

### <a name="step-2"></a>Paso 2

Cambiar los puntos de conexión Hola servicio (.csdef) de la definición archivo tooadd toohello equilibrio de carga interno. momento de Hola que se crea una instancia de rol, archivo de definición de servicio de hello agregará toohello de instancias de rol Hola equilibrio de carga interno.

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancer="load-balancer-name" />
    </Endpoints>
</WorkerRole>
```

Después de hello mismo los valores de ejemplo de Hola anterior, vamos a agregar archivo de definición de servicio de hello valores toohello.

```xml
<WorkerRole name="WorkerRole1" vmsize="A7" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="endpoint1" protocol="http" localPort="80" port="80" loadBalancer="testLB" />
    </Endpoints>
</WorkerRole>
```

tráfico de red de Hello será carga equilibrada con el equilibrador de carga de hello PruebaCL utilizando el puerto 80 para las solicitudes entrantes, enviar tooworker instancias de rol también en el puerto 80.

## <a name="next-steps"></a>Pasos siguientes

[Configurar un modo de distribución del equilibrador de carga mediante la afinidad IP de origen](load-balancer-distribution-mode.md)

[Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga](load-balancer-tcp-idle-timeout.md)

