---
title: "aaaOverview de escalado automático en las aplicaciones Web, servicios en la nube y máquinas virtuales de Microsoft Azure | Documentos de Microsoft"
description: "Información general sobre el escalado automático en Microsoft Azure. Se aplica tooVirtual máquinas, servicios en la nube y aplicaciones Web."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 74bf03be-e658-4239-a214-c12424b53e4c
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2016
ms.author: robb
ms.openlocfilehash: ef68b722ea22c4149a7d7a89c5855ba761db9247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-autoscale-in-microsoft-azure-virtual-machines-cloud-services-and-web-apps"></a>Información general de la funcionalidad de escalado automático de Microsoft Azure Virtual Machines, Cloud Services y Web Apps
Este artículo describe qué escalado automático de Microsoft Azure es, sus ventajas, y cómo tooget a usarlo.  

Azure escalado automático de Monitor se aplica solo demasiado[conjuntos de escalas de máquina Virtual](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [servicios en la nube](https://azure.microsoft.com/services/cloud-services/), y [servicio de aplicaciones: aplicaciones Web](https://azure.microsoft.com/services/app-service/web/).

> [!NOTE]
> Azure tiene dos métodos de escalado automático. Una versión anterior de escalado automático aplica tooVirtual máquinas (conjuntos de disponibilidad). Esta característica proporciona una compatibilidad limitada y se recomienda migrar escalas de máquina toovirtual establece para soporte de escalado automático más rápidas y confiables. En este artículo se incluye un vínculo en cómo toouse Hola tecnología más antigua.  
>
>

## <a name="what-is-autoscale"></a>¿Qué es el escalado automático?
Escalado automático permite la cantidad correcta de hello toohave de recursos de ejecución toohandle Hola carga en su aplicación. Permite tooadd recursos toohandle los aumentos de cargan y también ahorren dinero mediante la eliminación de recursos que esté inactivo. Especificar el número mínimo y máximo de instancias toorun y agregar o quitar máquinas virtuales automáticamente en función de un conjunto de reglas. Tener un mínimo garantiza la ejecución de la aplicación aunque no exista carga. Tener un máximo limita el posible costo total por hora. Se escala automáticamente entre estos dos extremos en función de las reglas que se creen.

 ![Explicación del escalado automático. Agregar y quitar máquinas virtuales](./media/monitoring-overview-autoscale/AutoscaleConcept.png)

Cuando se cumplen las condiciones de las reglas, se desencadenan una o varias acciones de escalado automático. Puede agregar y quitar máquinas virtuales o realizar otras acciones. Hello diagrama conceptual siguiente muestra este proceso.  

 ![Diagrama de flujo de escalado automático](./media/monitoring-overview-autoscale/Autoscale_Overview_v4.png)

Hello explicación siguiente aplica toohello piezas del diagrama anterior Hola.   

## <a name="resource-metrics"></a>Métricas de los recursos
Los recursos generan métricas, que procesan posteriormente las reglas. Las métricas proceden de métodos diferentes.
Conjuntos de escalas de máquina virtual usar datos de telemetría de agentes de diagnósticos de Azure, mientras que la telemetría para las aplicaciones Web y servicios en la nube procede directamente de hello infraestructura de Azure. Algunas de las estadísticas que se utilizan frecuentemente son el uso de CPU, el uso de memoria, el número de subprocesos, la longitud de la cola y el uso del disco. Para ver una lista de los datos de telemetría que se pueden utilizar, consulte [Métricas comunes de escalado automático de Azure Insights](insights-autoscale-common-metrics.md).

## <a name="custom-metrics"></a>Métricas personalizadas
También puede usar métricas personalizadas que las aplicaciones pueden generar. Si ha configurado su tooApplication de métricas de aplicaciones toosend visión pueden aprovechar esas decisiones toomake de métricas si tooscale o no. 

## <a name="time"></a>Hora
Las reglas basadas en programaciones emplean el huso horario UTC. Debe establecer la zona horaria correctamente al configurar las reglas.  

## <a name="rules"></a>Reglas
diagrama de Hello muestra una única regla de escalado automático, pero puede tener muchas de ellas. Puede crear reglas complejas de superposición según su situación.  Estos son algunos de los tipos de reglas:  

* **Basadas en métricas** : por ejemplo, realizar esta acción cuando el uso de CPU sea superior al 50 %.
* **Basadas en tiempo** : por ejemplo, desencadenar un webhook todos los sábados a las 8:00 en una zona horaria determinada.

Las reglas basadas en métricas miden la carga de la aplicación y agregan o quitan máquinas virtuales en función de ella. Las reglas basadas en programación permiten tooscale al ver patrones de tiempo en su carga y desea tooscale antes de un aumento de carga posible o disminución se produce.  

## <a name="actions-and-automation"></a>Acciones y escalado automático
Las reglas pueden desencadenar uno o varios tipos de acciones.

* **Escalar** : escalar o reducir horizontalmente máquinas virtuales
* **Correo electrónico** -enviar correo electrónico toosubscription administradores, coadministradores o dirección de correo electrónico adicionales que especifique
* **Automate via webhooks** (Automatizar mediante webhooks): llamar a webhooks, que pueden desencadenar varias acciones dentro o fuera de Azure. Dentro de Azure, puede iniciar runbooks de Azure Automation, Azure Function o Azure Logic Apps. La dirección URL de terceros de ejemplo fuera de Azure incluye servicios como Slack y Twilio.

## <a name="autoscale-settings"></a>Configuración de escalado automático
Escalado automático utilice siguiente de hello terminología y la estructura.

- Un **configuración de escalado automático** lee toodetermine de motor de escalado automático de hello si tooscale hacia arriba o hacia abajo. Contiene uno o más perfiles, información sobre el recurso de destino de Hola y configuración de notificaciones.

    - Un **perfil de escalado automático** es una combinación de:

        - **configuración de capacidad**, que indica Hola mínimo, máximo y valores predeterminados de número de instancias.
        - Un **conjunto de reglas**, cada una de las cuales incluye un desencadenador (tiempo o métrica) y una acción de escalado (escalado o reducción vertical).
        - Una **periodicidad**, que indica cuándo el escalado automático debe hacer entrar en vigor el perfil.

        Puede tener varios perfiles, que le permiten tootake atención distintos requisitos que se superponen. Puede tener perfiles de escalado automático diferentes para distintos momentos del día o días de la semana de hello, por ejemplo.

    - A **configuración de la notificación** define qué notificaciones deben aparecer cuando un evento de escalado automático se produce en función de que satisfacen los criterios de Hola de uno de los perfiles de configuración de escalado automático de Hola. Escalado automático puede notificar a una o varias direcciones de correo electrónico o realizar llamadas tooone o webhooks más.


![Configuración, perfil y estructura de las reglas de escalado automático de Azure](./media/monitoring-overview-autoscale/AzureResourceManagerRuleStructure3.png)

Hello lista completa de campos configurables y descripciones está disponible en hello [API de REST de escalado automático](https://msdn.microsoft.com/library/dn931928.aspx).

Para ver ejemplos de código, consulte los siguientes artículos:

* [Configuración avanzada de escalado automático con plantillas de Resource Manager para conjuntos de escala de máquina virtual](insights-advanced-autoscale-virtual-machine-scale-sets.md)  
* [API de REST de escalado automático](https://msdn.microsoft.com/library/dn931953.aspx)

## <a name="horizontal-vs-vertical-scaling"></a>Escalado horizontal frente a escalado vertical
Escalado automático solo se escala horizontalmente, que es un aumento ("out") o una disminución ("") en el número de Hola de instancias de máquina virtual.  Horizontal es más flexible en una situación en la nube, ya que permite toorun potencialmente miles de máquinas virtuales toohandle carga.

En contraste, el escalado vertical es diferente. Se mantiene Hola el mismo número de máquinas virtuales, pero hace Hola máquinas virtuales más ("arriba") o menos ("abajo") eficaces. La potencia se mide en memoria, velocidad de CPU, espacio en disco, etc.  El escalado vertical tiene más limitaciones, Es dependiente de la disponibilidad de Hola de hardware más grande, lo que rápidamente alcanza un límite superior y puede variar según la región. Vertical escalado también normalmente requiere una toostop de máquina virtual y reinicie.

Para obtener más información, consulte [Escalado vertical de máquinas virtuales de Azure con Automatización de Azure](../virtual-machines/linux/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="methods-of-access"></a>Métodos de acceso
Puede configurar el escalado automático en los siguientes lugares:

* [Portal de Azure](insights-how-to-scale.md)
* [PowerShell](insights-powershell-samples.md#create-and-manage-autoscale-settings)
* [Interfaz de línea de comandos (CLI) multiplataforma](insights-cli-samples.md#autoscale)
* [API de REST de Azure Monitor](https://msdn.microsoft.com/library/azure/dn931953.aspx)

## <a name="supported-services-for-autoscale"></a>Servicios compatibles con el escalado automático
| Servicio | Esquema y documentos |
| --- | --- |
| Aplicaciones web |[Escalado en Web Apps](insights-how-to-scale.md) |
| Servicios en la nube |[Escalado automático de un servicio en la nube](../cloud-services/cloud-services-how-to-scale.md) |
| Virtual Machines: clásico |[Escalado de conjuntos de disponibilidad clásicos de máquina virtual](https://blogs.msdn.microsoft.com/kaevans/2015/02/20/autoscaling-azurevirtual-machines/) |
| Virtual Machines: conjuntos de escalado de Windows |[Escalado de conjuntos de escalado de máquinas virtuales en Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) |
| Virtual Machines : conjuntos de escalado de Linux |[Escalado de conjuntos de escalado de máquinas virtuales en Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) |
| Virtual Machines: ejemplo de Windows |[Configuración avanzada de escalado automático con plantillas de Resource Manager para conjuntos de escala de máquina virtual](insights-advanced-autoscale-virtual-machine-scale-sets.md) |

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de escalado automático, use hello Autoscale Walkthroughs indicadas anteriormente o que consulte toohello recursos siguientes:

* [Métricas comunes de escalado automático de Azure Monitor](insights-autoscale-common-metrics.md)
* [Procedimientos recomendados de escalado automático en Azure Monitor](insights-autoscale-best-practices.md)
* [Usar el escalado automático acciones toosend correo electrónico y webhook notificaciones de alerta](insights-autoscale-to-webhook-email.md)
* [API de REST de escalado automático](https://msdn.microsoft.com/library/dn931953.aspx)
* [Solución de problemas de escalado automático de conjuntos de escalado de máquinas virtuales](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)
