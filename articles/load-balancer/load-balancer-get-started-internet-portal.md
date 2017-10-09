---
title: "equilibrador de carga de aaaCreate una conexión a Internet: portal de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una conexión a Internet de equilibrador de carga en el Administrador de recursos en Hola portal de Azure"
services: load-balancer
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: aa9d26ca-3d8a-4a99-83b7-c410dd20b9d0
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: annahar
ms.openlocfilehash: 390ba8ec1474c54cf2c0022c4a3c219d21b1a659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-hello-azure-portal"></a>Creación de un equilibrador de carga a través de Internet mediante Hola portal de Azure

> [!div class="op_single_selector"]
> * [Portal](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [CLI de Azure](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Plantilla](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Este artículo trata el modelo de implementación del Administrador de recursos de Hola. También puede [Obtenga información acerca de cómo el equilibrador mediante la implementación clásica de la carga de toocreate una conexión a Internet](load-balancer-get-started-internet-classic-portal.md)

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

Esto cubre secuencia Hola de tareas individuales que tienen toocreate toobe realiza un equilibrador de carga y se explica con detalle lo que está realizando el objetivo de hello tooaccomplish.

## <a name="what-is-required-toocreate-an-internet-facing-load-balancer"></a>¿Qué es toocreate requiere un equilibrador de carga a través de Internet?

Se necesita toocreate y configura Hola después objetos toodeploy un equilibrador de carga.

* Configuración de direcciones IP de front-end: contiene direcciones IP públicas para el tráfico de red entrante.
* Grupo de direcciones de back-end - contiene interfaces de red (NIC) de tráfico de red de tooreceive de máquinas virtuales de Hola Hola equilibrador de carga.
* Reglas de equilibrio de carga - contiene reglas de asignación de un puerto público en tooport de equilibrador de carga de hello en el grupo de direcciones de back-end de Hola.
* Reglas NAT de entrada: contiene las reglas de asignación de un puerto público en el puerto de tooa de equilibrador de carga de Hola para una máquina virtual específica en el grupo de direcciones de back-end de Hola.
* Sondea: contiene toocheck disponibilidad de sondeos que se usan de mantenimiento de instancias de máquinas virtuales en el grupo de direcciones de back-end de Hola.

Puede obtener más información sobre los componentes del equilibrador de carga con Azure Resource Manager en [Compatibilidad de Azure Resource Manager con Load Balancer](load-balancer-arm.md).

## <a name="set-up-a-load-balancer-in-azure-portal"></a>Configuración de un equilibrador de carga en Azure Portal

> [!IMPORTANT]
> En este ejemplo se supone que tiene una red virtual denominada **myVNet**. Consulte demasiado[crear red virtual](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) toodo esto. También se supone hay una subred dentro de **myVNet** llama **LB subred ser** y dos máquinas virtuales que se llama **web1** y **web2** respectivamente en Hola mismo conjunto llamado de disponibilidad **myAvailSet** en **myVNet**. Consulte demasiado[este vínculo](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toocreate máquinas virtuales.

1. Desde un explorador, navegue toohello portal de Azure: [http://portal.azure.com](http://portal.azure.com) e inicie sesión con su cuenta de Azure.
2. En el lado izquierdo superior de Hola de pantalla de bienvenida, seleccione **New** > **red** > **equilibrador de carga.**
3. Hola **equilibrador de carga de crear** hoja, escriba un nombre para el equilibrador de carga. En este caso, se llama **myLoadBalancer**.
4. En **Tipo**, seleccione **Público**.
5. En **Dirección IP pública**, cree una nueva dirección IP pública denominada **myPublicIP**.
6. En Grupo de recursos, seleccione **myRG**. A continuación, seleccione una **ubicación** adecuada y haga clic en **Aceptar**. equilibrador de carga de Hello, a continuación, iniciará toodeploy y tardará unos minutos toosuccessfully de implementación completa.

    ![Actualización de grupo de recursos de equilibrador de carga](./media/load-balancer-get-started-internet-portal/1-load-balancer.png)

## <a name="create-a-back-end-address-pool"></a>Creación del grupo de direcciones de back-end

1. Una vez que se ha implementado correctamente el equilibrador de carga, selecciónelo entre sus recursos. En configuración, seleccione Grupos de back-end. Escriba un nombre para el grupo de back-end. A continuación, haga clic en hello **agregar** botón hacia la parte superior de Hola de hoja de Hola que se muestra.
2. Haga clic en **agrega una máquina virtual** en hello **Agregar grupo back-end** hoja.  Seleccione **Elegir un conjunto de disponibilidad** en **Conjunto de disponibilidad** y seleccione **myAvailSet**. A continuación, seleccione **elegir máquinas virtuales de hello** en Hola sección máquinas virtuales en la hoja de Hola y haga clic en **web1** y **web2**, Hola dos máquinas virtuales que se creó para el equilibrio de carga. Asegúrese de que ambos tienen toohello de marcas de verificación azul deja tal como se muestra en la imagen de hello siguiente. A continuación, haga clic en **seleccione** en esa hoja seguida Aceptar Hola **máquinas virtuales elija** hoja y, a continuación, **Aceptar** en hello **Agregar grupo back-end** hoja.

    ![Agregar grupo de direcciones de back-end de toohello- ](./media/load-balancer-get-started-internet-portal/3-load-balancer-backend-02.png)

3. Comprobar toomake seguro de las notificaciones de lista desplegable tiene una actualización con respecto a Guardar grupo de back-end de equilibradores de carga de hello en la interfaz de red de suma tooupdating Hola para ambos Hola máquinas virtuales **web1** y **web2**.

## <a name="create-a-probe-lb-rule-and-nat-rules"></a>Creación de un sondeo, una regla de equilibrador de carga y reglas NAT

1. Cree un sondeo de estado.

    En la sección Configuración del equilibrador de carga, seleccione Sondeos. A continuación, haga clic en **agregar** situado en la parte superior de Hola de hoja de Hola.

    Hay un sondeo a tooconfigure de dos maneras: HTTP o TCP. En este ejemplo se muestra HTTP, pero TCP puede configurarse de forma similar.
    Actualizar la información necesaria de Hola. Como se mencionó, **myLoadBalancer** equilibrará la carga del tráfico en el puerto 80. ruta de acceso de Hello seleccionado es HealthProbe.aspx, intervalo es de 15 segundos y umbral incorrecto es 2. Cuando termine, haga clic en **Aceptar** sondeo de hello toocreate.

    Desplace el puntero sobre hello 'i' icono toolearn más información acerca de estas configuraciones individuales y cómo pueden ser modificadas toocater tooyour requisitos.

    ![Incorporación de un sondeo](./media/load-balancer-get-started-internet-portal/4-load-balancer-probes.png)

2. Cree una regla de equilibrador de carga.

    Haga clic en reglas de Hola de equilibrio de carga de la sección de configuración de un equilibrador de carga. En la nueva hoja de hello, haga clic en **agregar**. Ponga un nombre a la regla. En este caso, HTTP. Elegir puerto de front-end de Hola y puerto back-end. En este caso, se elige 80 para ambos. Elija **back-end de LB** como su hello creado anteriormente y el grupo back-end **HealthProbe** como Hola sondeo. Otras configuraciones se pueden establecer según los requisitos de tooyour. A continuación, haga clic en regla de equilibrio de carga de hello toosave Aceptar.

    ![Incorporación de una regla de equilibrio de carga](./media/load-balancer-get-started-internet-portal/5-load-balancing-rules.png)

3. Creación de reglas NAT de entrada

    Haga clic en reglas de NAT de entrada en la sección de configuración de Hola de un equilibrador de carga. En hello nueva hoja, haga clic en **agregar**. Luego ponga un nombre a la regla NAT de entrada. Aquí se llama **inboundNATrule1**. destino de Hello debe ser Hola que IP pública creado anteriormente. Seleccione personalizado mediante el servicio y le gustaría toouse de protocolo de Hola. Aquí se selecciona TCP. Escriba el puerto de hello, 3441 y Hola 3389 de puerto de destino, en este caso. a continuación, haga clic en Aceptar toosave, esta regla.

    Una vez que se crea la primera regla de hello, repita este paso para hello segunda regla NAT de entrada llamado inboundNATrule2 desde 3442 tooTarget puerto 3389.

    ![Incorporación de una regla NAT entrante](./media/load-balancer-get-started-internet-portal/6-load-balancer-inbound-nat-rules.png)

## <a name="remove-a-load-balancer"></a>Eliminación de un equilibrador de carga

desea tooremove de equilibrador de carga de un equilibrador de carga, seleccione hello toodelete. Hola *equilibrador de carga* hoja, haga clic en **eliminar** situado en la parte superior de Hola de hoja de Hola. A continuación, seleccione **Sí** cuando se le solicite.

## <a name="next-steps"></a>Pasos siguientes

[Introducción a la configuración de un equilibrador de carga interno](load-balancer-get-started-ilb-arm-cli.md)

[Configuración de un modo de distribución del equilibrador de carga](load-balancer-distribution-mode.md)

[Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga](load-balancer-tcp-idle-timeout.md)
