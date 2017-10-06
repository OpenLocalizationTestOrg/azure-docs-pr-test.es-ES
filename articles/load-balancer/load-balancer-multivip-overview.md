---
title: aaaMultiple VIP de equilibrador de carga de Azure | Documentos de Microsoft
description: "Información general de varias IP virtuales para Azure Load Balancer"
services: load-balancer
documentationcenter: na
author: chkuhtz
manager: narayan
editor: 
ms.assetid: 748e50cd-3087-4c2e-a9e1-ac0ecce4f869
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/11/2016
ms.author: chkuhtz
ms.openlocfilehash: e186e1248e7d187e7efd0668dc3244465ce3e156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="multiple-vips-for-azure-load-balancer"></a>Varias IP virtuales para Azure Load Balancer

Equilibrador de carga de Azure le permite equilibrar los servicios tooload en varios puertos, varias direcciones IP o ambos. Puede usar flujos de equilibrio de carga públicos e internos equilibrador definiciones tooload a través de un conjunto de máquinas virtuales.

Este artículo describe los fundamentos de Hola de esta capacidad, conceptos importantes y las restricciones. Si solo piensa tooexpose servicios en una dirección IP, puede encontrar instrucciones simplificadas para [público](load-balancer-get-started-internet-portal.md) o [interno](load-balancer-get-started-ilb-arm-portal.md) las configuraciones de equilibrador de carga. Agregar varias VIP es incremental tooa una sola configuración de VIP. Con los conceptos de hello en este artículo, puede expandir una configuración simplificada en cualquier momento.

Al definir un Azure Load Balancer, las configuraciones front-end y back-end están conectadas con reglas. sondeo de estado al que hace referencia la regla de Hola Hola es usado toodetermine cómo el nuevo flujos se envían tooa nodo en el grupo back-end de Hola. Hola front-end se define mediante una IP Virtual (VIP), que es una tupla de 3 consta de una dirección IP (pública o interna), un protocolo de transporte (UDP o TCP) y un número de puerto. Una DIP es que una dirección IP en una NIC virtual Azure adjunta tooa máquina virtual en el grupo de back-end de Hola.

Hello en la tabla siguiente contiene algunas configuraciones de front-end de ejemplo:

| IP virtual | Dirección IP | protocolo | puerto |
| --- | --- | --- | --- |
| 1 |65.52.0.1 |TCP |80 |
| 2 |65.52.0.1 |TCP |*8080* |
| 3 |65.52.0.1 |*UDP* |80 |
| 4 |*65.52.0.2* |TCP |80 |

tabla de Hola muestran cuatro de front-ends diferentes. Los front-end 1, 2 y 3 son una sola dirección IP virtual con varias reglas. Hello misma dirección IP se usa pero protocolo o puerto de hello es diferente para cada servidor front-end. Front-ends #1 y #4 son un ejemplo de varias VIP, donde hello mismo puerto y protocolo de front-end se reutilizan a través de varias VIP.

Equilibrador de carga de Azure proporciona flexibilidad para definir las reglas de equilibrio de carga de Hola. Una regla declara una dirección y el puerto en el servidor front-end de hello forma asignada toohello dirección de destino y el puerto en hello back-end. Si no se reutilizan puertos back-end a través de las reglas depende de tipo de Hola de regla de Hola. Cada tipo de regla tiene requisitos específicos que pueden afectar al diseño del sondeo y a la configuración del host. Existen dos tipos de reglas:

1. volver a usar regla predeterminada de Hello con ningún puerto de back-end
2. regla de dirección IP flotante Hola donde se reutilizan puertos back-end

Equilibrador de carga de Azure permite toomix ambos tipos de reglas en Hola la misma configuración de equilibrador de carga. equilibrador de carga de Hello utilizarlas al mismo tiempo en una máquina virtual determinada, o cualquier combinación, mientras cumplir las restricciones de Hola de regla de Hola. Qué tipo de regla que elija depende de los requisitos de hello su complejidad hello y aplicación de ser compatible con esa configuración. Debe evaluar qué tipos de reglas son mejores para su escenario.

Exploramos aún más estos escenarios empezando por el comportamiento predeterminado de Hola.

## <a name="rule-type-1-no-backend-port-reuse"></a>Tipo de regla 1: No reutilización de puerto back-end

![Ilustración de varias IP virtuales](./media/load-balancer-multivip-overview/load-balancer-multivip.png)

En este escenario, Hola front-end VIP se configuran como se indica a continuación:

| IP virtual | Dirección IP | protocolo | puerto |
| --- | --- | --- | --- |
| ![IP virtual](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |
| ![IP virtual](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |*65.52.0.2* |TCP |80 |

Hola DIP constituye el destino de Hola de hello flujo de entrada. En el grupo de back-end de hello, cada máquina virtual expone servicio Hola deseado en un puerto único en una DIP. Este servicio está asociado con hello front-end a través de una definición de regla.

Se definen dos reglas:

| Regla | Asignación de front-end | grupo de toobackend |
| --- | --- | --- |
| 1 |![IP virtual](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) VIP1:80 |![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) DIP1:80, ![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) DIP2:80 |
| 2 |![IP virtual](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) VIP2:80 |![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) DIP1:81, ![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) DIP2:81 |

Hola asignación completa en el equilibrador de carga de Azure ahora es la siguiente:

| Regla | Dirección IP de IP virtual | protocolo | puerto | Destino | puerto |
| --- | --- | --- | --- | --- | --- |
| ![Regla](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |Dirección IP de DIP |80 |
| ![Regla](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |65.52.0.2 |TCP |80 |Dirección IP de DIP |81 |

Cada regla debe generar un flujo con una combinación única de dirección IP de destino y puerto de destino. Puerto de destino Hola distintos de flujo de hello, varias reglas pueden entregar flujos toohello mismo DIP en puertos diferentes.

Sondeo de estado siempre es toohello dirigido DIP de una máquina virtual. Debe asegurarse de que el sondeo refleja mantenimiento Hola de hello máquina virtual.

## <a name="rule-type-2-backend-port-reuse-by-using-floating-ip"></a>Tipo de regla 2: reutilización de puerto back-end mediante IP flotante

Equilibrador de carga de Azure proporciona flexibilidad de hello puerto front-end de tooreuse hello en varias VIP independientemente del tipo de regla de hello usa. Además, algunos escenarios de aplicación prefieren o requieren el mismo número de puerto toobe usada varias instancias de aplicación en una sola máquina virtual en el grupo de back-end de Hola de Hola. Entre los ejemplos comunes de reutilización de puertos se incluyen la agrupación en clústeres para alta disponibilidad, dispositivos de red virtuales y la exposición de varios puntos de conexión TLS sin volver a cifrar.

Si desea puerto de back-end de hello tooreuse a través de varias reglas, debe habilitar IP flotante en la definición de la regla de Hola.

La IP flotante es una parte de lo que se conoce como Direct Server Return (DSR). DSR consta de dos partes: una topología de flujo y un esquema de asignación de direcciones IP. En un nivel de plataforma, Azure Load Balancer siempre funciona en una topología de flujo DSR independientemente de si la dirección IP flotante está habilitada o no. Esto significa que parte de salida de hello de un flujo es siempre ha vuelto a escribir correctamente tooflow toohello directamente atrás origen.

Con el tipo de regla de Hola de forma predeterminada, Azure expone una esquema de asignación de direcciones IP para facilitar su uso de equilibrio de carga tradicional. Habilitar dirección IP flotante cambia hello tooallow de esquema de asignación de direcciones IP para una flexibilidad adicional como se explica a continuación.

Hola siguiente diagrama ilustra esta configuración:

![Ilustración de varias IP virtuales](./media/load-balancer-multivip-overview/load-balancer-multivip-dsr.png)

En este escenario, cada máquina virtual en el grupo de back-end de hello tiene tres interfaces de red:

* DIP: una NIC Virtual asociado con hello VM (configuración de IP de recursos de formación de Azure)
* VIP1: una interfaz de bucle invertido en el SO invitado que se configura con la dirección IP de VIP1
* VIP2: una interfaz de bucle invertido en el SO invitado que se configura con la dirección IP de VIP2

> [!IMPORTANT]
> configuración de Hola de interfaces lógicas Hola se realiza en el sistema operativo invitado de Hola. Esta configuración no se ejecuta ni administra en Azure. Sin esta configuración, las reglas de hello no funcionará. Las definiciones de sondeo de estado usar hello DIP de hello VM en lugar de Hola a VIP lógico. Por lo tanto, el servicio debe proporcionar respuestas de sondeo en un puerto DIP que indican el estado de Hola de servicio de hello ofrecido en hello lógico VIP.

Supongamos que Hola misma configuración de front-end como en el escenario anterior hello:

| IP virtual | Dirección IP | protocolo | puerto |
| --- | --- | --- | --- |
| ![IP virtual](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |
| ![IP virtual](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |*65.52.0.2* |TCP |80 |

Se definen dos reglas:

| Regla | Asignación de front-end | grupo de toobackend |
| --- | --- | --- |
| 1 |![Regla](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) VIP1:80 |![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) VIP1:80 (en VM1 y VM2) |
| 2 |![Regla](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) VIP2:80 |![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) VIP2:80 (en VM1 y VM2) |

Hello en la tabla siguiente muestra la asignación completa de hello en el equilibrador de carga de hello:

| Regla | Dirección IP de IP virtual | protocolo | puerto | Destino | puerto |
| --- | --- | --- | --- | --- | --- |
| ![IP virtual](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |igual que la dirección VIP (65.52.0.1) |igual que la dirección VIP (80) |
| ![IP virtual](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |65.52.0.2 |TCP |80 |igual que la dirección VIP (65.52.0.2) |igual que la dirección VIP (80) |

destino de Hola de hello flujo entrante es la dirección de hello VIP en la interfaz de bucle invertido de Hola Hola máquina virtual. Cada regla debe generar un flujo con una combinación única de dirección IP de destino y puerto de destino. Por distintos Hola dirección IP de destino del flujo de hello, es posible en reutilización del puerto Hola misma máquina virtual. El servicio está expuesto toohello equilibrador de carga mediante el enlace de dirección IP y el puerto de interfaz de bucle invertido respectivos hello toohello de la dirección VIP.

Tenga en cuenta que este ejemplo no cambia el puerto de destino de Hola. Aunque se trata de un escenario de dirección IP flotante, equilibrador de carga de Azure también admite la definición de un puerto de destino de back-end de regla toorewrite hello y toomake diferente del puerto de destino de hello front-end.

Hola tipo de regla de dirección IP flotante es foundation Hola de varias formas de configuración de equilibrador de carga. Un ejemplo que está disponible actualmente es hello [AlwaysOn de SQL con varios agentes de escucha](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md) configuración. Con el tiempo, se documentarán varios de estos escenarios.

## <a name="limitations"></a>Limitaciones

* Solo se admiten varias configuraciones de IP virtual con máquinas virtuales de IaaS.
* Con la regla de dirección IP flotante hello, la aplicación debe utilizar Hola DIP para los flujos de salida. Si la aplicación enlaza dirección VIP de toohello configurado en la interfaz de bucle invertido de hello en el sistema operativo invitado de hello, a continuación, SNAT no es flujo de salida de hello toorewrite disponible y se produce un error en el flujo de Hola.
* Las direcciones IP públicas repercuten en la facturación. Para obtener más información, vea [Precios de las direcciones IP](https://azure.microsoft.com/pricing/details/ip-addresses/)
* Se aplican los límites de suscripción. Para más información, vea los [límites de servicio](../azure-subscription-service-limits.md#networking-limits) .
