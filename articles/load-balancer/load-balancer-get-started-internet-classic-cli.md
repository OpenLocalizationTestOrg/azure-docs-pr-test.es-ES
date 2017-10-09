---
title: "aaaCreate una conexión a Internet cargar equilibrador - CLI de Azure clásico | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate un equilibrador de carga con conexión a Internet en el modelo de implementación clásica utilizando Hola CLI de Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: e433a824-4a8a-44d2-8765-a74f52d4e584
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: e6070cbc574f74bca0cccb960ff192847d6511bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-cli"></a>Empezar a crear un equilibrador de carga (clásica) en hello Azure CLI de Internet

> [!div class="op_single_selector"]
> * [Portal de Azure clásico](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [CLI de Azure](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Servicios en la nube de Azure](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Antes de trabajar con recursos de Azure, es importante toounderstand que Azure tiene dos modelos de implementación: Administrador de recursos de Azure y clásico. Asegúrese de que comprende los [modelos de implementación y las herramientas](../azure-classic-rm.md) antes de trabajar con recursos de Azure. Puede ver documentación de Hola de distintas herramientas, haga clic en las pestañas de hello en parte superior de Hola de este artículo. Este artículo trata el modelo de implementación clásica de Hola. También puede [Obtenga información acerca de cómo toocreate una conexión a Internet cargar equilibrador mediante Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="step-by-step-creating-an-internet-facing-load-balancer-using-cli"></a>Creación paso a paso de un equilibrador de carga orientado a Internet con la CLI

Esta guía muestra cómo se toocreate un equilibrador de carga de Internet basada en escenario de hello anterior.

1. Si nunca ha utilizado la CLI de Azure, consulte [instalar y configurar hello Azure CLI](../cli-install-nodejs.md) y siga las instrucciones de hello punto toohello donde seleccionar su cuenta de Azure y la suscripción.
2. Ejecute hello **modo de configuración de azure** tooswitch tooclassic modo de comandos, tal y como se muestra a continuación.

    ```azurecli
    azure config mode asm
    ```

    Resultado esperado:

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a>Crear punto de conexión y conjunto de equilibrador de carga

escenario de Hello asume hello las máquinas virtuales "web1" y "web2" se crearon.
Esta guía creará un conjunto de equilibrador de carga mediante el puerto 80 como puerto público y el puerto 80 como puerto local. También se configura un puerto de sondeo en el puerto 80 y equilibrador de carga con nombre hello establece "lbset".

### <a name="step-1"></a>Paso 1

Crear el primer punto de conexión de Hola y establecen a través del equilibrador de carga `azure network vm endpoint create` para la máquina virtual "web1".

```azurecli
azure vm endpoint create web1 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-2"></a>Paso 2

Agregue un segundo conjunto de equilibrador de carga de toohello de máquina virtual "web2".

```azurecli
azure vm endpoint create web2 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-3"></a>Paso 3

Compruebe la configuración de equilibrador de carga de hello utilizando `azure vm show` .

```azurecli
azure vm show web1
```

salida de Hello será:

    data:    DNSName "contoso.cloudapp.net"
    data:    Location "East US"
    data:    VMName "web1"
    data:    IPAddress "10.0.0.5"
    data:    InstanceStatus "ReadyRole"
    data:    InstanceSize "Standard_D1"
    data:    Image "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-2015
    6-en.us-127GB.vhd"
    data:    OSDisk hostCaching "ReadWrite"
    data:    OSDisk name "joaoma-1-web1-0-201509251804250879"
    data:    OSDisk mediaLink "https://XXXXXXXXXXXXXXX.blob.core.windows.
    /vhds/joaomatest-web1-2015-09-25.vhd"
    data:    OSDisk sourceImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Se
    r-2012-R2-20150916-en.us-127GB.vhd"
    data:    OSDisk operatingSystem "Windows"
    data:    OSDisk iOType "Standard"
    data:    ReservedIPName ""
    data:    VirtualIPAddresses 0 address "XXXXXXXXXXXXXXXX"
    data:    VirtualIPAddresses 0 name "XXXXXXXXXXXXXXXXXXXX"
    data:    VirtualIPAddresses 0 isDnsProgrammed true
    data:    Network Endpoints 0 loadBalancedEndpointSetName "lbset"
    data:    Network Endpoints 0 localPort 80
    data:    Network Endpoints 0 name "tcp-80-80"
    data:    Network Endpoints 0 port 80
    data:    Network Endpoints 0 loadBalancerProbe port 80
    data:    Network Endpoints 0 loadBalancerProbe protocol "tcp"
    data:    Network Endpoints 0 loadBalancerProbe intervalInSeconds 15
    data:    Network Endpoints 0 loadBalancerProbe timeoutInSeconds 31
    data:    Network Endpoints 0 protocol "tcp"
    data:    Network Endpoints 0 virtualIPAddress "XXXXXXXXXXXX"
    data:    Network Endpoints 0 enableDirectServerReturn false
    data:    Network Endpoints 1 localPort 5986
    data:    Network Endpoints 1 name "PowerShell"
    data:    Network Endpoints 1 port 5986
    data:    Network Endpoints 1 protocol "tcp"
    data:    Network Endpoints 1 virtualIPAddress "XXXXXXXXXXXX"
    data:    Network Endpoints 1 enableDirectServerReturn false
    data:    Network Endpoints 2 localPort 3389
    data:    Network Endpoints 2 name "Remote Desktop"
    data:    Network Endpoints 2 port 58081
    info:    vm show command OK

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a>Crear un punto de conexión de escritorio remoto para una máquina virtual

Puede crear un tráfico de red de tooforward de punto de conexión de escritorio remoto desde un puerto local tooa del puerto público para una máquina virtual específica mediante `azure vm endpoint create`.

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a>Quitar máquina virtual del equilibrador de carga

Tiene el conjunto de equilibrador de carga de la máquina virtual de hello toodelete Hola extremo asociado toohello. Una vez que se quita el punto de conexión de hello, máquina virtual de hello no pertenece equilibrador de carga de toohello ya establecido.

Utilizando el ejemplo de Hola anterior, puede quitar extremo de hello creado para la máquina virtual "web1" del equilibrador de carga "lbset" mediante el comando hello `azure vm endpoint delete`.

```azurecli
azure vm endpoint delete web1 tcp-80-80
```

> [!NOTE]
> Puede explorar más opciones toomanage puntos de conexión mediante el comando de Hola`azure vm endpoint --help`

## <a name="next-steps"></a>Pasos siguientes

[Introducción a la configuración de un equilibrador de carga interno](load-balancer-get-started-ilb-arm-ps.md)

[Configuración de un modo de distribución del equilibrador de carga](load-balancer-distribution-mode.md)

[Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga](load-balancer-tcp-idle-timeout.md)
