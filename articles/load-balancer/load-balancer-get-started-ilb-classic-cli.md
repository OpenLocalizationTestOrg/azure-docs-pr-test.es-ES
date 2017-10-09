---
title: "aaaCreate un interno cargar equilibrador - CLI de Azure clásico | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate un equilibrador de carga interno utilizando Hola CLI de Azure en el modelo de implementación clásica de Hola"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: becbbbde-a118-4269-9444-d3153f00bf34
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: ef29dfda5f7a75a411bbabe8b688a31c6bf81113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-hello-azure-cli"></a>Empezar a crear un equilibrador de carga interno (clásico) mediante Hola CLI de Azure

> [!div class="op_single_selector"]
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [CLI de Azure](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [Cloud Services](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).  Este artículo incluye el uso de modelo de implementación clásica de Hola. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. Obtenga información acerca de cómo demasiado[realizar estos pasos con el modelo del Administrador de recursos de hello](load-balancer-get-started-ilb-arm-cli.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="toocreate-an-internal-load-balancer-set-for-virtual-machines"></a>toocreate un equilibrador de carga interno establecido para las máquinas virtuales

toocreate un equilibrador de carga interno establecido y Hola servidores que enviarán su tráfico tooit, debe hacer los siguiente hello:

1. Cree una instancia de interno equilibrio de carga que será el punto de conexión de Hola de carga de toobe tráfico entrante están equilibrada en los servidores de Hola de un conjunto con equilibrio de carga.
2. Agregue extremos correspondientes máquinas virtuales de toohello que va a recibir el tráfico entrante Hola.
3. Configure los servidores de Hola que van a enviar equilibrio de carga de hello tráfico toobe toosend su tráfico toohello dirección IP virtual (VIP) de instancia de equilibrio de carga interno de Hola.

## <a name="step-by-step-creating-an-internal-load-balancer-using-cli"></a>Creación paso a paso de un equilibrador de carga interno mediante la CLI

Esta guía muestra cómo se toocreate un equilibrador de carga interno basada en escenario de hello anterior.

1. Si nunca ha utilizado la CLI de Azure, consulte [instalar y configurar hello Azure CLI](../cli-install-nodejs.md) y siga las instrucciones de hello punto toohello donde seleccionar su cuenta de Azure y la suscripción.
2. Ejecute hello **modo de configuración de azure** tooswitch tooclassic modo de comandos, tal y como se muestra a continuación.

    ```azurecli
    azure config mode asm
    ```

    Resultado esperado:

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a>Crear punto de conexión y conjunto de equilibrador de carga

escenario de Hello supone Hola máquinas "DB1" y "DB2" en un servicio de nube denominado "mytestcloud". Ambas máquinas virtuales usan una red virtual denominada mi "testvnet" con la subred "subnet-1".

Esta guía creará un conjunto de equilibrador de carga interno mediante el puerto 1433 como puerto privado y 1433 como puerto local.

Se trata de un escenario común donde haya máquinas virtuales de SQL sobre el uso de back-end de hello que no se expondrá un servidores de bases de datos de carga interno equilibrador tooguarantee Hola directamente mediante una dirección IP pública.

### <a name="step-1"></a>Paso 1

Crear un conjunto de equilibrador de carga interno mediante `azure network service internal-load-balancer add`.

```azurecli
azure service internal-load-balancer add --serviceName mytestcloud --internalLBName ilbset --subnet-name subnet-1 --static-virtualnetwork-ipaddress 192.168.2.7
```

Para obtener más información, consulte `azure service internal-load-balancer --help` .

Puede comprobar las propiedades de equilibrador de carga interno de hello mediante comandos de hello `azure service internal-load-balancer list` *nombre de servicio de nube*.

Sigue aquí un ejemplo de salida de hello:

    azure service internal-load-balancer list my-testcloud
    info:    Executing command service internal-load-balancer list
    + Getting cloud service deployment
    data:    Name    Type     SubnetName  StaticVirtualNetworkIPAddress
    data:    ------  -------  ----------  -----------------------------
    data:    ilbset  Private  subnet-1    192.168.2.7
    info:    service internal-load-balancer list command OK


### <a name="step-2"></a>Paso 2

Configure el equilibrador de carga interno de hello establecido cuando se agrega el primer punto de conexión de Hola. Se asociará Hola extremo, la máquina virtual y sondeo puerto toohello equilibrador de carga interno establecido en este paso.

```azurecli
azure vm endpoint create db1 1433 --local-port 1433 --protocol tcp --probe-port 1433 --probe-protocol tcp --probe-interval 300 --probe-timeout 600 --internal-load-balancer-name ilbset
```

### <a name="step-3"></a>Paso 3

Compruebe la configuración de equilibrador de carga de hello con `azure vm show` *nombre de máquina virtual*

```azurecli
azure vm show DB1
```

salida de Hello será:

    azure vm show DB1
    info:    Executing command vm show
    + Getting virtual machines
    data:    DNSName "mytestcloud.cloudapp.net"
    data:    Location "East US 2"
    data:    VMName "DB1"
    data:    IPAddress "192.168.2.4"
    data:    InstanceStatus "ReadyRole"
    data:    InstanceSize "Standard_D1"
    data:    Image "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-20151022-en.us-127GB.vhd"
    data:    OSDisk hostCaching "ReadWrite"
    data:    OSDisk name "db1-DB1-0-201511120457370846"
    data:    OSDisk mediaLink "https://XXXX.blob.core.windows.net/vhd"
    data:    OSDisk sourceImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-20151022-en.us-127GB.vhd"
    data:    OSDisk operatingSystem "Windows"
    data:    OSDisk iOType "Standard"
    data:    ReservedIPName ""
    data:    VirtualIPAddresses 0 address "137.116.64.107"
    data:    VirtualIPAddresses 0 name "db1ContractContract"
    data:    VirtualIPAddresses 0 isDnsProgrammed true
    data:    VirtualIPAddresses 1 address "192.168.2.7"
    data:    VirtualIPAddresses 1 name "ilbset"
    data:    Network Endpoints 0 localPort 5986
    data:    Network Endpoints 0 name "PowerShell"
    data:    Network Endpoints 0 port 5986
    data:    Network Endpoints 0 protocol "tcp"
    data:    Network Endpoints 0 virtualIPAddress "137.116.64.107"
    data:    Network Endpoints 0 enableDirectServerReturn false
    data:    Network Endpoints 1 localPort 3389
    data:    Network Endpoints 1 name "Remote Desktop"
    data:    Network Endpoints 1 port 60173
    data:    Network Endpoints 1 protocol "tcp"
    data:    Network Endpoints 1 virtualIPAddress "137.116.64.107"
    data:    Network Endpoints 1 enableDirectServerReturn false
    data:    Network Endpoints 2 localPort 1433
    data:    Network Endpoints 2 name "tcp-1433-1433"
    data:    Network Endpoints 2 port 1433
    data:    Network Endpoints 2 loadBalancerProbe port 1433
    data:    Network Endpoints 2 loadBalancerProbe protocol "tcp"
    data:    Network Endpoints 2 loadBalancerProbe intervalInSeconds 300
    data:    Network Endpoints 2 loadBalancerProbe timeoutInSeconds 600
    data:    Network Endpoints 2 protocol "tcp"
    data:    Network Endpoints 2 virtualIPAddress "192.168.2.7"
    data:    Network Endpoints 2 enableDirectServerReturn false
    data:    Network Endpoints 2 loadBalancerName "ilbset"
    info:    vm show command OK

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a>Crear un punto de conexión de escritorio remoto para una máquina virtual

Puede crear un tráfico de red de tooforward de punto de conexión de escritorio remoto desde un puerto local tooa del puerto público para una máquina virtual específica mediante `azure vm endpoint create`.

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a>Quitar máquina virtual del equilibrador de carga

Puede quitar una máquina virtual de un equilibrador de carga interno establecido mediante la eliminación de punto de conexión de hello asociado. Una vez que se quita el punto de conexión de hello, máquina virtual de hello no pertenecen equilibrador de carga de toohello ya establecido.

Utilizando el ejemplo de Hola anterior, puede quitar extremo de hello creado para la máquina virtual "DB1" de equilibrador de carga interno "ilbset" mediante el comando de hello `azure vm endpoint delete`.

```azurecli
azure vm endpoint delete DB1 tcp-1433-1433
```

Para obtener más información, consulte `azure vm endpoint --help` .

## <a name="next-steps"></a>Pasos siguientes

[Configurar un modo de distribución del equilibrador de carga mediante la afinidad IP de origen](load-balancer-distribution-mode.md)

[Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga](load-balancer-tcp-idle-timeout.md)
