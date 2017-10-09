---
title: las conexiones salientes de aaaUnderstanding en Azure | Documentos de Microsoft
description: "Este artículo explica cómo Azure permite toocommunicate de máquinas virtuales con servicios de Internet pública."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
ms.assetid: 5f666f2a-3a63-405a-abcd-b2e34d40e001
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 5/31/2017
ms.author: kumud
ms.openlocfilehash: ffe59971b934a16c9f6f78e3b15869a0072320d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-outbound-connections-in-azure"></a>Comprender las conexiones salientes en Azure

Una máquina virtual (VM) de Azure puede comunicarse con puntos de conexión fuera de Azure en el espacio de direcciones IP públicas. Cuando una máquina virtual inicia un destino de tooa de flujo de salida en el espacio de direcciones IP públicas, Azure asigna privada tooa pública dirección IP la máquina virtual de hello y permite Hola de tráfico del retorno tooreach máquina virtual.

Azure proporciona tres métodos diferentes conectividad saliente tooachieve. Cada método tiene sus propias funcionalidades y restricciones. Revise cuidadosamente cada método toochoose que satisfaga sus necesidades.

| Escenario | Método | Nota: |
| --- | --- | --- |
| Máquina virtual independiente (ningún equilibrador de carga, ninguna dirección IP pública a nivel de instancia) |Valor predeterminado de SNAT |Azure asocia una dirección IP pública para SNAT |
| Máquina virtual de carga equilibrada (ninguna dirección IP pública a nivel de instancia en la máquina virtual) |SNAT usando Hola equilibrador de carga |Azure utiliza una dirección IP pública de hello equilibrador de carga para SNAT |
| Máquina virtual con dirección IP pública a nivel de instancia (con o sin equilibrador de carga) |No se utiliza SNAT |Azure utiliza Hola IP pública asignada toohello VM |

Si no desea que un toocommunicate VM con puntos de conexión fuera de Azure en el espacio de direcciones IP públicas, puede usar acceso tooblock de grupos de seguridad de red (NSG). El uso de estos grupos se describe con más detalle en [Prevención de las conexiones públicas](#preventing-public-connectivity).

## <a name="standalone-vm-with-no-instance-level-public-ip-address"></a>Máquina virtual independiente con ninguna dirección IP pública a nivel de instancia

En este escenario, Hola VM no forma parte de un grupo de equilibrador de carga de Azure y no tiene una dirección pública IP de instancia nivel (ILPIP) asignada tooit. Cuando Hola VM crea un flujo de salida, Azure traduce la dirección IP de origen privada de Hola de dirección IP de origen pública de tooa de flujo de salida de hello. dirección IP pública Hola utilizada para este flujo de salida no es configurable y no cuentan para el límite de recurso IP pública de la suscripción de Hola. Azure usa esta función de traducción de direcciones de red de origen (SNAT) tooperform. Puertos efímeros de dirección IP pública de hello son flujos individuales toodistinguish usado por hello VM que se originó. SNAT asigna dinámicamente puertos efímeros cuando se crean flujos. En este contexto, puertos efímeros Hola utilizados para SNAT son puertos SNAT tooas que se hace referencia.

Los puertos SNAT son un recurso finito que puede agotarse. Es importante toounderstand cómo se utilizan. Un puerto SNAT es consumido por dirección IP de flujo tooa único destino. Para varios toohello flujos misma dirección IP de destino, cada flujo consume un solo puerto SNAT. Esto garantiza que Hola flujos sean único cuando se ha originado Hola mismo toohello de dirección IP pública misma dirección IP de destino. Varios flujos, cada dirección IP de destino diferente de tooa utilizan un único puerto SNAT por cada destino. dirección IP de destino de Hello, que fluye de hello será único.

Puede usar [análisis de registros para el equilibrador de carga](load-balancer-monitor-log.md) y [toomonitor de registros de eventos de alertas para los mensajes de agotamiento de puertos SNAT](load-balancer-monitor-log.md#alert-event-log). Cuando se agotan los recursos de los puertos SNAT, los flujos de salida generan errores hasta que los flujos ya existentes liberan otros puertos SNAT. Load Balancer utiliza un tiempo de espera de inactividad de 4 minutos para reclamar puertos SNAT.

## <a name="load-balanced-vm-with-no-instance-level-public-ip-address"></a>Máquina virtual de carga equilibrada sin ninguna dirección IP pública a nivel de instancia

En este escenario, Hola VM es parte de un grupo de equilibrador de carga de Azure.  Hola VM no tiene una dirección IP pública asignada tooit. Hola recurso de equilibrador de carga se debe configurar con un regla toolink Hola IP front-end pública con el grupo de back-end de Hola.  Si no se completan esta configuración, el comportamiento de hello es como se describe en la sección de hello anterior para [Standalone VM con ninguna IP pública de nivel de instancia](load-balancer-outbound-connections.md#standalone-vm-with-no-instance-level-public-ip-address).

Cuando hello VM de equilibrio de carga crea un flujo de salida, Azure traduce la dirección IP de origen privada Hola de hello flujo saliente toohello dirección IP pública de front-end pública equilibrador de carga de Hola. Azure usa esta función de traducción de direcciones de red de origen (SNAT) tooperform. Puertos efímeros de la dirección IP pública del equilibrador de carga de hello son flujos individuales toodistinguish usado por hello VM que se originó. SNAT asigna dinámicamente puertos efímeros cuando se crean flujos de salida. En este contexto, puertos efímeros Hola utilizados para SNAT son puertos SNAT tooas que se hace referencia.

Los puertos SNAT son un recurso finito que puede agotarse. Es importante toounderstand cómo se utilizan. Un puerto SNAT es consumido por dirección IP de flujo tooa único destino. Para varios toohello flujos misma dirección IP de destino, cada flujo consume un solo puerto SNAT. Esto garantiza que Hola flujos sean único cuando se ha originado Hola mismo toohello de dirección IP pública misma dirección IP de destino. Varios flujos, cada dirección IP de destino diferente de tooa utilizan un único puerto SNAT por cada destino. dirección IP de destino de Hello, que fluye de hello será único.

Puede usar [análisis de registros para el equilibrador de carga](load-balancer-monitor-log.md) y [toomonitor de registros de eventos de alertas para los mensajes de agotamiento de puertos SNAT](load-balancer-monitor-log.md#alert-event-log). Cuando se agotan los recursos de los puertos SNAT, los flujos de salida generan errores hasta que los flujos ya existentes liberan otros puertos SNAT. Load Balancer utiliza un tiempo de espera de inactividad de 4 minutos para reclamar puertos SNAT.

## <a name="vm-with-an-instance-level-public-ip-address-with-or-without-load-balancer"></a>Máquina virtual con dirección IP pública a nivel de instancia (con o sin Load Balancer)

En este escenario, Hola VM tiene una instancia nivel pública IP (ILPIP) asignado tooit. No importa si Hola VM tiene una carga equilibrada o no. Cuando se usa una ILPIP, no se utiliza la traducción de direcciones de red de origen (SNAT). Hola VM usa hello ILPIP para todos los flujos de salida. Si su aplicación inicia muchos flujos de salida y experimenta agotamiento SNAT, considere la posibilidad de asignar una tooavoid ILPIP restricciones SNAT.

## <a name="discovering-hello-public-ip-used-by-a-given-vm"></a>Detección de dirección IP pública de hello utilizado por una máquina virtual determinada

Hay muchas maneras toodetermine Hola pública dirección IP de origen una conexión de salida. OpenDNS proporciona un servicio que puede mostrar Hola dirección IP pública de la máquina virtual. Usar el comando de nslookup de hello, puede enviar una consulta DNS para resolución de hello nombre myip.opendns.com toohello OpenDNS. servicio de Hello devuelve la dirección IP de origen de Hola que se consulta de hello toosend usado. Cuando se ejecuta después de consulta de la máquina virtual de hello, respuesta de hello es hello IP pública que se utiliza para esa máquina virtual.

    nslookup myip.opendns.com resolver1.opendns.com

## <a name="preventing-public-connectivity"></a>Prevención de las conexiones públicas

A veces es deseable para una máquina virtual toobe permite toocreate un flujo de salida o puede haber un toomanage requisito qué destinos pueden ponerse en contacto con los flujos de salida. En este caso, utilice [grupos de seguridad de red (NSG)](../virtual-network/virtual-networks-nsg.md) toomanage Hola destinos ese Hola puede llegar la máquina virtual. Al aplicar un NSG tooa con equilibrio de carga VM, deberá toopay atención toohello [predeterminado etiquetas](../virtual-network/virtual-networks-nsg.md#default-tags) y [reglas predeterminadas](../virtual-network/virtual-networks-nsg.md#default-rules).

Debe asegurarse de que esa máquina virtual de hello puede recibir solicitudes de sondeo de estado de equilibrador de carga de Azure. Si un NSG bloques sondeo solicitudes de mantenimiento de hello etiqueta AZURE_LOADBALANCER de forma predeterminada, se produce un error en el sondeo de estado de la máquina virtual y se marca Hola VM hacia abajo. Equilibrador de carga deja de enviar toothat de flujos nueva máquina virtual.

## <a name="limitations"></a>Limitaciones

Si hay [varias direcciones IP (públicas) asociadas a un equilibrador de carga](load-balancer-multivip-overview.md), ninguna de estas direcciones IP públicas serán candidatas para los flujos de salida.

Azure utiliza un número de Hola de toodetermine algoritmo de puertos SNAT disponibles basándose en hello tamaño de bloque de Hola.  Esto no es configurable en este momento.

Es importante toorememember que Hola número de puertos SNAT disponibles no traduce directamente toonumber de conexiones. Consulte más arriba para obtener información específica sobre cuándo y cómo se asignan los puertos SNAT y cómo toomanage este recurso agotable.
