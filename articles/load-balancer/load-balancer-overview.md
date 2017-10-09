---
title: "información general del equilibrador de carga de aaaAzure | Documentos de Microsoft"
description: "Información general sobre las características, la arquitectura y la implementación del Equilibrador de carga de Azure Obtenga información acerca de cómo funciona el equilibrador de carga de Hola y aprovechar en nube Hola."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
ms.assetid: 0f313dc0-f007-4cee-b2b9-f542357925a3
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 2376a02f7cbbbed6a90f216419c0c3d30f594272
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-load-balancer-overview"></a>Información general sobre el Equilibrador de carga de Azure

Equilibrador de carga de Azure ofrece alta disponibilidad y rendimiento de red tooyour aplicaciones. Se trata de un equilibrador de carga de nivel 4 (TCP y UDP) que distribuye el tráfico entrante entre las instancias de servicio correctas de los servicios que se definen en un conjunto de carga equilibrada.

Azure Load Balancer puede configurarse para lo siguiente:

* La carga de máquinas de toovirtual de Internet entrantes de equilibrar el tráfico. Esta configuración se conoce como " [equilibrio de carga con conexión a Internet](load-balancer-internet-overview.md)".
* Equilibrar la carga del tráfico entre máquinas virtuales de una red virtual, entre máquinas virtuales de servicios en la nube o entre equipos locales y máquinas virtuales de una red virtual entre entornos locales. Esta configuración se conoce como " [equilibrio de carga interno](load-balancer-internal-overview.md)".
* Máquina virtual específica a reenvíe el tráfico externo tooa.

Todos los recursos de nube de hello necesitan una toobe de dirección IP pública accesible desde Internet Hola. infraestructura de nube de Hello en Azure usa direcciones IP no enrutables para sus recursos. Azure utiliza traducción de direcciones de red (NAT) con toohello de toocommunicate de direcciones IP pública Internet.

## <a name="azure-deployment-models"></a>Modelos de implementación de Azure

Es importante toounderstand diferencias de hello entre hello Azure clásico y Administrador de recursos [modelos de implementación](../azure-resource-manager/resource-manager-deployment-model.md). ya que Azure Load Balancer se configura de forma diferente en cada uno de ellos.

### <a name="azure-classic-deployment-model"></a>modelo de implementación clásica de Azure

Máquinas virtuales implementadas dentro de un límite de servicio de nube puede ser agrupado toouse un equilibrador de carga. En este modelo una dirección IP pública y un nombre de dominio completo, (FQDN) se asignan tooa servicio en la nube. equilibrador de carga de Hello puerto traducción y equilibra la carga de tráfico de red de hello mediante el uso de la dirección IP pública Hola Hola servicio de nube.

El tráfico de carga equilibrada lo definen los puntos de conexión. Los extremos de traducción de puerto tienen una relación uno a uno entre el puerto asignado por el público Hola de dirección IP pública de Hola y puerto local de hello asignado toohello servicio en una máquina virtual específica. Extremos de equilibrio de carga tienen una relación de uno a varios entre la dirección IP pública Hola y Hola local puertos asignados toohello servicios en máquinas virtuales de Hola Hola del servicio en nube.

![Equilibrador de carga de Azure en el modelo de implementación clásica de Hola](./media/load-balancer-overview/asm-lb.png)

Figura 1 - Azure equilibrador de carga en el modelo de implementación clásica de Hola

etiqueta de dominio de Hello para la dirección IP pública Hola Hola usos de equilibrador de carga para este modelo de implementación es \<nombre de servicio de nube\>. cloudapp.net. Hello gráfico siguiente muestra hello equilibrador de carga de Azure en este modelo.

### <a name="azure-resource-manager-deployment-model"></a>modelo de implementación de Azure Resource Manager

En el modelo de implementación del Administrador de recursos de hello no hay ninguna necesidad de toocreate un servicio de nube. equilibrador de carga de Hola se crea tooexplicitly enrutar el tráfico entre varias máquinas virtuales.

Una dirección IP pública es un recurso individual que tiene una etiqueta de dominio (nombre DNS). la dirección IP pública Hola está asociada con el recurso de equilibrador de carga de Hola. Reglas del equilibrador de carga y reglas NAT de entrada utilizan la dirección IP pública hello como Hola de punto de conexión de Internet para los recursos de Hola que reciben tráfico con equilibrio de carga de red.

Se asigna a una dirección IP pública o privada toohello red interfaz recurso adjuntado tooa virtual machine. Una vez que una interfaz de red se agrega el grupo de direcciones IP de back-end del equilibrador de carga de tooa, equilibrador de carga de hello es toosend capaz de equilibrio de carga red tráfico basado en reglas Hola con equilibrio de carga que se crean.

Hello gráfico siguiente muestra hello equilibrador de carga de Azure en este modelo:

![Azure Load Balancer en Resource Manager](./media/load-balancer-overview/arm-lb.png)

Ilustración 2: Azure Load Balancer en Resource Manager

equilibrador de carga de Hello puede administrarse a través de plantillas se basan en el Administrador de recursos, API y herramientas. toolearn más acerca de administrador de recursos, vea hello [Introducción al administrador de recursos](../azure-resource-manager/resource-group-overview.md).

## <a name="load-balancer-features"></a>Características del equilibrador de carga

* Distribución basada en hash

    El Equilibrador de carga de Azure usa un algoritmo de distribución basado en hash. De forma predeterminada, usa un hash de tupla de 5 formado por dirección IP de origen, puerto de origen, dirección IP de destino, puerto de destino y servidores de protocolo tipo toomap tráfico tooavailable. Dicho algoritmo solo proporciona adherencia *dentro* de una sesión de transporte. Los paquetes de saludo será la misma sesión TCP o UDP dirigen toohello mismo instancia detrás de extremo con equilibrio de carga de Hola. Cuando el cliente de Hola se cierra y vuelve a abrir la conexión de Hola o inicia una nueva sesión de Hola misma IP de origen, los cambios del puerto origen Hola. Esto puede provocar Hola tráfico toogo tooa puntos de conexión diferentes en un centro de datos diferente.

    Para obtener más detalles, consulte [Modo de distribución del equilibrador de carga (afinidad de IP de origen)](load-balancer-distribution-mode.md). Hello gráfico siguiente muestra hello basado en hash distribución:

    ![Distribución basada en hash](./media/load-balancer-overview/load-balancer-distribution.png)

    Ilustración 3: Distribución basada en Hash

* Enrutamiento de puerto

    El Equilibrador de carga de Azure le permite controlar cómo se administra la comunicación entrante. Estas comunicación incluye tráfico iniciado desde hosts de Internet o máquinas virtuales de otros servicios en la nube o redes virtuales. Este control se representa mediante un punto de conexión (también conocido como punto de conexión de entrada).

    Un extremo de entrada escucha en un puerto público y reenvía el tráfico de puerto interno tooan. Solo se puede asignar Hola mismo puertos para un extremo interno o externo o utilizar un puerto diferente para ellos. Por ejemplo, puede tener un tooport de toolisten de servidor configurado web 81 mientras asignación de punto de conexión público de hello es el puerto 80. creación de Hello de un extremo público desencadena la creación de hello de una instancia de equilibrador de carga.

    Cuando creadas con hello portal de Azure, portal de hello crea automáticamente los puntos de conexión toohello virtual machine para hello protocolo de escritorio remoto (RDP) y tráfico de la sesión de Windows PowerShell remoto. Puede utilizar estos extremos tooremotely administrar máquinas virtuales de Hola a través de Internet de Hola.

* Reconfiguración automática

    El Equilibrador de carga de Azure se reconfigura inmediatamente al escalar instancias horizontalmente o reducirlas verticalmente. Por ejemplo, este cambio de configuración puede ocurrir al aumentar Hola recuento de instancias para los roles de web y de trabajo en un servicio de nube o al agregar máquinas virtuales adicionales en hello establecer igual con equilibrio de carga.

* Supervisión de servicios

    Equilibrador de carga de Azure puede sondear estado Hola de hello varias instancias del servidor. Cuando un sondeo se produce un error toorespond, equilibrador de carga de hello deja de enviar nuevas conexiones toohello instancias en mal estado. Las conexiones existentes no se ven afectadas.

    Se admiten tres tipos de sondeos:

    + **Sondeo del agente invitado (en la plataforma como un servicio de máquinas virtuales solo):** equilibrador de carga de hello utiliza el agente de invitado Hola dentro de la máquina virtual de Hola. escucha Hello agente invitado y responde con una respuesta HTTP 200 OK solo cuando hello instancia está en estado listo hello (es decir, Hola instancia no está en un estado como ocupado, reciclaje o detener). Si el agente de hello no toorespond con un HTTP 200 OK, marcas de equilibrador de carga de Hola Hola instancia no responde y deja de enviar la instancia de toothat de tráfico. equilibrador de carga de Hello continúa la instancia de hello tooping. Si el agente de invitado Hola responde con un HTTP 200, equilibrador de carga de hello enviará instancia toothat de tráfico de nuevo. Cuando se usa un rol web, el código de sitio Web normalmente se ejecuta en w3wp.exe, que no está supervisado por hello tejido de Azure o el agente de invitado. Esto significa que los errores en w3wp.exe (por ejemplo, las respuestas de error HTTP 500) no estará incluido toohello agente de invitado y equilibrador de carga de hello no sabrá tootake esa instancia fuera de la rotación.
    + **Sondeo HTTP personalizado:** este sondeo invalida el sondeo de hello predeterminado (agente de invitado). Puede usar toocreate su propio estado de hello toodetermine lógica personalizada de instancia de rol de Hola. equilibrador de carga de Hello realizarán un sondeo con regularidad el punto de conexión (cada 15 segundos, de forma predeterminada). instancia de Hola se considera toobe de rotación si responde con un ACK de TCP o HTTP 200 dentro del período de tiempo de espera de hello (valor predeterminado de segundos 31). Esto es útil para implementar sus propias instancias de tooremove de lógica de la rotación del equilibrador de carga de Hola. Por ejemplo, puede configurar Hola instancia tooreturn un estado no es 200 si las instancias de hello es por encima del 90% de la CPU. Para los roles de web que utilizan w3wp.exe, también obtendrá automática de supervisión del sitio Web, puesto que los errores en el código de sitio Web devuelven un sondeo de estado no es 200 toohello.
    + **Sondeo TCP personalizado:** este sondeo se basa en el puerto de sondeo de tooa definido establecimiento de sesión TCP correcta.

    Para obtener más información, vea hello [esquema LoadBalancerProbe](https://msdn.microsoft.com/library/azure/jj151530.aspx).

* NAT de origen

    Todos los toohello el tráfico saliente se somete Internet que se origina en el servicio de origen NAT (SNAT) mediante el uso de Hola la misma dirección VIP como Hola tráfico entrante. SNAT proporciona ventajas importantes:

    + Hace fácil actualización y recuperación ante desastres de servicios, puesto que Hola que VIP puede ser dinámicamente asignada tooanother instancia del servicio de Hola.
    + Facilita la administración de la lista de control de acceso (ACL). Las ACL que se expresan en términos de VIP no cambian cuando los servicios se escalan verticalmente, se reducen horizontalmente o se vuelven a implementar.

    configuración de equilibrador de carga de Hello admite cono completo NAT para UDP. Cono completo NAT es un tipo de NAT que puerto Hola permite las conexiones entrantes desde cualquier host externo (en la solicitud de respuesta tooan saliente).

    Para cada nueva conexión saliente que inicia una máquina virtual, un puerto de salida también se asigna al equilibrador de carga de Hola. host externo de Hello ve tráfico con un puerto asignado a la dirección VIP de IP virtual. Para escenarios que requieren un gran número de conexiones salientes, se recomienda toouse [IP pública de nivel de instancia](../virtual-network/virtual-networks-instance-level-public-ip.md) direcciones para que las máquinas virtuales de hello tienen una dirección IP de salida dedicada para SNAT. Esto reduce el riesgo de Hola de agotamiento de puertos.

    Consulte el artículo sobre [conexiones salientes](load-balancer-outbound-connections.md) para obtener más información acerca de este tema.

### <a name="support-for-multiple-load-balanced-ip-addresses-for-virtual-machines"></a>Compatibilidad con varias direcciones IP con equilibrio de carga para máquinas virtuales
Puede asignar más de una carga equilibrada públicos tooa conjunto de direcciones IP de máquinas virtuales. Con esta capacidad, puede hospedar varios sitios Web SSL o varios agentes de escucha de grupo de disponibilidad AlwaysOn de SQL Server en el mismo conjunto de máquinas virtuales de Hola. Para obtener más información, consulte [Varias direcciones VIP por servicio en la nube](load-balancer-multivip.md).

[!INCLUDE [load-balancer-compare-tm-ag-lb-include.md](../../includes/load-balancer-compare-tm-ag-lb-include.md)]

## <a name="limitations"></a>Limitaciones

Los grupos de back-end de Load Balancer pueden contener cualquier SKU de máquina virtual, excepto nivel Básico.

## <a name="next-steps"></a>Pasos siguientes

- Más información sobre el [equilibrador de carga accesible desde Internet](load-balancer-internet-overview.md)

- Para más información, consulte [Información general sobre el equilibrador de carga interno](load-balancer-internal-overview.md)

- Cree un [equilibrador de carga accesible desde Internet](load-balancer-get-started-internet-portal.md)

- Obtener información sobre algunas de hello otra clave [capacidades de red](../networking/networking-overview.md) de Azure

