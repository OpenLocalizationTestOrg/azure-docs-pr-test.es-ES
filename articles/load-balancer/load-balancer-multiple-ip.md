---
title: aaaLoad equilibrio en varias configuraciones de IP en Azure | Documentos de Microsoft
description: Equilibrio de carga entre las configuraciones de IP principales y secundarias.
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: na
ms.assetid: 244907cd-b275-4494-aaf7-dcfc4d93edfe
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: 8619493b8102e9d158d428fe6c59ecf3f32edc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-hello-azure-portal"></a>Equilibrio de carga en varias configuraciones de IP mediante Hola portal de Azure

> [!div class="op_single_selector"]
> * [Portal](load-balancer-multiple-ip.md)
> * [PowerShell](load-balancer-multiple-ip-powershell.md)
> * [CLI](load-balancer-multiple-ip-cli.md)

Este artículo describe cómo aborda toouse equilibrador de carga de Azure con varias IP en una interfaz de red secundaria (NIC). En este escenario, tenemos dos máquinas virtuales que ejecutan Windows, cada uno con un elemento principal y una NIC secundaria. Cada uno de hello secundaria NIC tienen dos configuraciones de IP. Cada máquina virtual hospeda dos sitios web: contoso.com y fabrikam.com. Cada sitio Web está enlazado tooone Hola de configuraciones de IP en la NIC de hello secundaria. Utilizamos el equilibrador de carga Azure tooexpose dos front-end direcciones IP, una para cada sitio Web, toodistribute tráfico toohello respectivo configuración IP para el sitio Web de Hola. Este escenario utiliza Hola el mismo número de puerto a través de front-ends, así como las direcciones IP de back-end del grupo.

![Imagen del escenario de equilibrio de carga](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

##<a name="prerequisites"></a>Requisitos previos
En este ejemplo se da por supuesto que tiene un grupo de recursos denominado *contosofabrikam* con hello siguiente configuración:
 -  incluye una red virtual denominada *myVNet*, dos máquinas virtuales que se llama *VM1* y *VM2* respectivamente en Hola mismo conjunto con nombre de disponibilidad *myAvailset*. 
 - Cada máquina virtual tiene una NIC principal y otra secundaria. Hola principal se denominan NIC *VM1NIC1* y *VM2NIC1* y base de datos secundaria Hola NIC se denominan *VM1NIC2* y *VM2NIC2*. Para más información sobre la creación de máquinas virtuales con varias NIC, consulte [Creación de una máquina virtual con varias NIC mediante PowerShell](../virtual-network/virtual-network-deploy-multinic-arm-ps.md).

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a>Saldo de tooload de pasos en varias configuraciones de IP

Siga estos pasos a continuación del escenario de hello tooachieve descrito en este artículo:

### <a name="step-1-configure-hello-secondary-nics-for-each-vm"></a>PASO 1: Configurar Hola NIC secundarias para cada máquina virtual

Para cada máquina virtual en la red virtual, agregue el conjunto de configuración de IP para Hola NIC secundaria como sigue:  

1. Desde un explorador, navegue toohello portal de Azure: http://portal.azure.com e inicie sesión con su cuenta de Azure.
2. En hello superior izquierda de la pantalla de bienvenida, haga clic en el icono de grupo de recursos de hello y, a continuación, haga clic en Hola Hola de grupo de recursos se encuentran las máquinas virtuales en (por ejemplo, *contosofabrikam*). Hola **grupos de recursos** ahora se muestra la hoja que enumera todos los recursos de hello junto con interfaces de red de Hola para hello las máquinas virtuales.
3. toohello secundaria NIC de cada máquina virtual, agregue una configuración de IP, tal como sigue:
    1. Seleccione la interfaz de red de hello que desea tooadd Hola IP configuración.
    2. En la hoja de Hola que aparece para hello NIC que ha seleccionado, haga clic en **configuraciones IP**. A continuación, haga clic en **agregar** hacia la parte superior de Hola de hoja de Hola que se muestra.
    3. Hola **configuraciones IP agregar** hoja, agregue un segundo toohello de configuración de IP NIC como sigue: 
        1. Escriba un nombre para la configuración de IP secundaria (por ejemplo, para el VM1 y VM2 nombre hello las configuraciones de IP como *VM1NIC2 ipconfig2* y *VM2NIC2 ipconfig2* respectivamente).
        2. Para **Dirección IP privada**, en **Asignación**, seleccione **Estática**.
        3. Haga clic en **Aceptar**.
        4. Cuando Hola segunda configuración de IP Hola NIC secundaria se completa, se muestra en hello **configuraciones IP** hoja de configuración para hello dado NIC.

### <a name="step-2-create-a-load-balancer"></a>PASO 2: Creación de un equilibrador de carga

Cree un equilibrador de carga de la manera siguiente:

1. Desde un explorador, navegue toohello portal de Azure: http://portal.azure.com e inicie sesión con su cuenta de Azure.
2. En hello superior izquierda de la pantalla de bienvenida, haga clic en **New** > **red** > **equilibrador de carga**. A continuación, haga clic en **Crear**.
3. Hola **equilibrador de carga de crear** hoja, escriba un nombre para el equilibrador de carga. Aquí se denomina *mylb*.
4. En Dirección IP pública, cree una nueva dirección IP pública denominada **PublicIP1**.
5. En el grupo de recursos, seleccione Hola grupo de recursos existente de las máquinas virtuales (por ejemplo, *contosofabrikam*). A continuación, seleccione una ubicación adecuada y haga clic en **Aceptar**. equilibrador de carga de Hello, a continuación, iniciará toodeploy y tardará unos minutos toosuccessfully de implementación completa.
6. Una vez implementado, equilibrador de carga de Hola se muestra como un recurso en el grupo de recursos.

### <a name="step-3-configure-hello-frontend-ip-pool"></a>PASO 3: Configurar el grupo de direcciones IP de front-end de Hola

Configure el grupo de direcciones IP del front-end para cada sitio web (contoso y fabrikam) de la manera siguiente:

1. En el portal de hello, haga clic en **más servicios** > tipo **dirección IP pública** en Hola cuadro Filtro y, a continuación, haga clic en **direcciones IP públicas**. Haga clic en **agregar** hacia la parte superior de Hola de hoja de Hola que se muestra.
2. Configure dos direcciones IP públicas (*PublicIP1* y *PublicIP2*) para ambos sitios web (contoso y fabrikam), como se indica a continuación:
    1. Escriba un nombre para la dirección IP de front-end.
    2. Para **grupo de recursos**, seleccione Hola grupo de recursos existente del programa Hola a las máquinas virtuales (por ejemplo, *contosofabrikam*).
    3. Para **ubicación**, seleccione Hola misma ubicación como Hola máquinas virtuales.
    4. Haga clic en **Aceptar**.
    5. Una vez que se crean Hola dos direcciones de IP públicas, se muestran en hello **IP pública** hoja de direcciones.
3. En el portal de hello, haga clic en **más servicios** > tipo **equilibrador de carga** en Hola cuadro Filtro y, a continuación, haga clic en **equilibrador de carga**.  
4. Seleccione el equilibrador de carga de hello (*mylb*) que desea que el grupo IP de front-end tooadd Hola a.
5. En **Configuración**, seleccione **Frontend Pools** (Grupos de servidores front-end). A continuación, haga clic en **agregar** hacia la parte superior de Hola de hoja de Hola que se muestra.
6. Escriba un nombre para la dirección IP de front-end (*farbikamfe* o **contosofe*).
7. Haga clic en **dirección IP** y en hello **dirección IP pública elija** hoja, direcciones IP de select hello para el front-end (*PublicIP1* o *PublicIP2*).
8. Repita los pasos 3 too7 dentro de esta sección toocreate Hola segunda front-end dirección IP.
9. Cuando se completa la configuración de grupo IP de front-end de hello, ambas direcciones IP de front-end se muestran en hello **grupo de direcciones IP de front-end** hoja de un equilibrador de carga. 
    
### <a name="step-4-configure-hello-backend-pool"></a>PASO 4: Configurar grupo de back-end de Hola   
Configurar grupos de direcciones de back-end de hello en el equilibrador de carga para cada sitio Web (Contoso y Fabrikam) como se indica a continuación:
        
1. En el portal de hello, haga clic en **más servicios** > escriba equilibrador de carga en el cuadro de filtro de hello y, a continuación, haga clic en **equilibrador de carga**.  
2. Seleccione el equilibrador de carga de hello (*mylb*) que desea que grupos de back-end de hello tooadd a.
3. En **Configuración**, seleccione **Grupos de back-end**. Escriba un nombre para el grupo de back-end (por ejemplo, *contosopool* o *fabrikampool*). A continuación, haga clic en hello **agregar** botón hacia la parte superior de Hola de hoja de Hola que se muestra. 
4. En **Asociado a**, seleccione **Conjunto de disponibilidad**.
5. En **Conjunto de disponibilidad**, seleccione **myAvailset**.
6. Agregue las configuraciones de IP de la red de destino para ambas máquinas virtuales de la manera siguiente (consulte la figura 2):  
    1. Para **Máquina Virtual de destino**, seleccione Hola VM que desea que el grupo de back-end de toohello tooadd (por ejemplo, VM1 o VM2).
    2. Para **configuración de red IP**, seleccione Configuración de IP de la NIC secundaria de Hola para esa máquina virtual (por ejemplo, VM1NIC2 ipconfig2 o VM2NIC2 ipconfig2).
    ![Imagen del escenario de equilibrio de carga](./media/load-balancer-multiple-ip/lb-backendpool.PNG)
            
        **Figura 2**: configuración de equilibrador de carga de hello con grupos back-end  
7. Haga clic en **Aceptar**.
8. Cuando se completa la configuración del grupo back-end de hello, ambos grupos de direcciones de back-end se muestran en hello **hoja de grupo back-end** de un equilibrador de carga.

### <a name="step-5-configure-a-health-probe-for-your-load-balancer"></a>PASO 5: Configuración de un sondeo de estado para el equilibrador de carga
Configure un sondeo de estado para el equilibrador de carga de la manera siguiente:
    1. En el portal de hello, haga clic en servicios más > escriba equilibrador de carga en el cuadro de filtro de hello y, a continuación, haga clic en **equilibrador de carga**.  
    2. Seleccione el equilibrador de carga de Hola que desea que grupos de back-end de hello tooadd a.
    3. En **Configuración**, seleccione **Sondeo de estado**. A continuación, haga clic en **agregar** hacia la parte superior de Hola de hoja de Hola que se muestra.
    4. Escriba un nombre para el sondeo de estado de hello (por ejemplo, HTTP) y haga clic en **Aceptar**.

### <a name="step-6-configure-load-balancing-rules"></a>PASO 6: Configuración de las reglas de equilibrio de carga
Configure reglas de equilibrio de carga (*HTTPc* y *HTTPf*) para cada sitio web como se indica a continuación:
    
1. En **Configuración**, seleccione **Sondeo de estado**. A continuación, haga clic en **agregar** hacia la parte superior de Hola de hoja de Hola que se muestra.
2. Para **nombre**, escriba un nombre para la regla de equilibrio de carga de hello (por ejemplo, *HTTPc* para Contoso, o *HTTPf* para Fabrikam)
3. Para dirección Frontend IP, seleccione dirección IP de Hola Hola front-end (por ejemplo *Contosofe* o *Fabrikamfe*)
4. Para **puerto** y **puerto back-end**, mantenga el valor predeterminado de hello **80**.
5. En **IP flotante (Direct Server Return)**, haga clic en **Habilitado**.
6. Haga clic en **Aceptar**.
7. Repita los pasos del 1 too6 dentro de esta sección toocreate Hola segundo equilibrador de carga de reglas.
8. Al equilibrio de carga de hello reglas de configuración está completa, ambas reglas ((*HTTPc* y *HTTPf*) se muestran en hello **reglas de equilibrio de carga** hoja de un equilibrador de carga.

### <a name="step-7-configure-dns-records"></a>PASO 7: Configuración de los registros DNS
Por último, debe configurar el dirección IP de DNS recursos registros toopoint toohello respectivos front-end del equilibrador de carga de Hola. Puede hospedar los dominios en Azure DNS. Para más información sobre el uso de Azure DNS con Load Balancer, consulte [Uso de Azure DNS con otros servicios de Azure](../dns/dns-for-azure-services.md).

## <a name="next-steps"></a>Pasos siguientes
- Obtener más información acerca de cómo Equilibrio de carga de toocombine services en Azure en [con servicios de equilibrio de carga en Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).
- Obtenga información acerca de cómo puede usar varios tipos de registros de Azure toomanage y solucionar problemas de equilibrador de carga en [análisis de registros para el equilibrador de carga de Azure](../load-balancer/load-balancer-monitor-log.md).
