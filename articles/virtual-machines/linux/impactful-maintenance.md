---
title: "aaaVM reiniciar mantenimiento para máquinas virtuales de Linux en Azure | Documentos de Microsoft"
description: "Mantenimiento de reinicio de máquina virtual para máquinas virtuales Linux."
services: virtual-machines-linux
documentationcenter: 
author: zivr
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: eb4b92d8-be0f-44f6-a6c3-f8f7efab09fe
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: zivr
ms.openlocfilehash: 41caa2e56740cdfa95d2ea67278e5c1d15a174c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="vm-restarting-maintenance"></a>Mantenimiento de reinicio de máquina virtual

Hay pocos casos en los que las máquinas virtuales se reinician debido tooplanned mantenimiento toohello infraestructura subyacente. Ser beneficiosas toothe disponibilidad de las máquinas virtuales hospedadas en Azure, siguiente Hola ahora está disponibles para toouse:

-   Al menos 30 días antes de que afecten Hola envía notificación.

-   Ventanas de mantenimiento de visibilidad toohello por cada máquina virtual.

-   Flexibilidad y control de configuración de la hora exacta de hello para el mantenimiento de afectar a las máquinas virtuales.

El mantenimiento de Microsoft Azure se programa en iteraciones. Iteraciones iniciales tienen el ámbito más pequeño en orden tooreduce Hola riesgo que conlleva en implementar capacidades y correcciones. Las iteraciones posteriores pueden abarcar varias regiones (nunca de hello mismo par de región). Se incluye una máquina virtual en una iteración de mantenimiento única. Si se anula una iteración, las máquinas virtuales restantes se incluyen en otra iteración futura.

mantenimiento planeado iteración Hello tiene dos fases: ventana de mantenimiento de Pre-emptive y una ventana de mantenimiento programada.

Hola **ventana de mantenimiento de Pre-emptive** proporciona mantenimiento de hello flexibilidad tooinitiate hello en las máquinas virtuales. Al hacerlo, puede determinar cuándo se vean afectadas las máquinas virtuales, hello secuencia de actualización de Hola y Hola tiempo que transcurre entre cada máquina virtual que se mantiene. Puede consultar cada toosee de máquina virtual si está previsto para el mantenimiento y comprobar el resultado de hello de la última solicitud de mantenimiento iniciadas.

Hola **ventana de mantenimiento programada** es cuando Azure ha programado las máquinas virtuales para el mantenimiento de Hola. Durante este período de tiempo, que sigue a la ventana de mantenimiento preventivo, puede consultar para la ventana de mantenimiento de hello, pero ya no estará tooorchestrate capaz de mantenimiento de Hola.

## <a name="availability-considerations-during-planned-maintenance"></a>Consideraciones sobre disponibilidad durante el mantenimiento planeado 

### <a name="paired-regions"></a>Regiones emparejadas

Cada región de Azure se empareja con otra región dentro de hello mismo geography, realizar juntos un par regional. Al ejecutar el mantenimiento, Azure solo actualizará las instancias de máquina Virtual de hello en una única región de su pareja. Por ejemplo, al actualizar Hola máquinas virtuales en Ee.uu. Central Norte, Azure no actualizará las máquinas virtuales de Ee.uu. Central sur en hello mismo tiempo. Se programarán a una hora independiente, lo que permitirá la conmutación por error o el equilibrio de carga entre regiones. Sin embargo, otras regiones como Europa del Norte puede estar en proceso de mantenimiento en Hola mismo tiempo como UU.
Más información sobre [Regiones emparejadas de Azure](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).

### <a name="single-instance-vms-vs-availability-set-or-vm-scale-set"></a>Máquinas virtuales de instancia única frente a conjunto de disponibilidad o conjunto de escalado de VM

Al implementar una carga de trabajo usando máquinas virtuales en Azure, puede crear hello las máquinas virtuales dentro de un conjunto de disponibilidad en aplicaciones de tooyour de orden tooprovide alta disponibilidad. Esta configuración garantiza que durante un corte de suministro o un evento de mantenimiento, al menos haya una máquina virtual disponible.

Dentro de un conjunto de disponibilidad, las máquinas virtuales individuales se reparten entre los dominios de actualización de too20. Durante el mantenimiento planeado, solo un dominio de actualización se ve afectado en un momento dado. orden de Hola de dominios de actualización que se ve afectado no puede continuar secuencialmente durante el mantenimiento planeado. Para un solo la instancia máquinas virtuales (que no forma parte del conjunto de disponibilidad), no hay ninguna manera toopredict o determinar qué y cómo muchas máquinas virtuales que se ven afectadas juntos.

Conjuntos de escalas de máquina virtual son un recurso de proceso de Azure que le permite toodeploy y administración un conjunto de máquinas virtuales idénticos como un único recurso.
conjunto de escalas de Hello proporciona garantías similares tooan conjunto de disponibilidad en el formulario de dominios de actualización. 

Para obtener más información acerca de cómo configurar las máquinas virtuales de alta disponibilidad, vea [ *administrar Hola disponibilidad de las máquinas virtuales de Windows*](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="scheduled-events"></a>Eventos programados

Azure Metadata Service le permite toodiscover información acerca de la máquina Virtual hospedada en Azure. Eventos, una de las categorías de hello expuesto, información de superficies sobre próximos eventos programados (por ejemplo, reiniciar) para la aplicación pueda preparar para ellos y limitar la interrupción.

Para obtener más información acerca de los eventos programados, consulte demasiado[servicio de metadatos de Azure - eventos programados](../virtual-machines-scheduled-events.md).

## <a name="maintenance-discovery-and-notifications"></a>Detección y notificaciones de mantenimiento

Programación de mantenimiento es toocustomers visible en el nivel de Hola de máquinas virtuales individuales. Puede usar Azure portal, tooquery API, PowerShell o CLI para las ventanas de mantenimiento preventivo y programada. Además, se espera recibir una notificación (correo electrónico) en caso de Hola que uno (o más) de las máquinas virtuales se ven afectadas durante el proceso de Hola.

Las fases de mantenimiento programado y de mantenimiento preferente comienzan con una notificación. Esperar tooreceive una única notificación por suscripción de Azure. notificación de Hola se envía la suscripción toohello admin y Coadministrador de forma predeterminada. También puede configurar la audiencia de hello para la notificación de mantenimiento.

### <a name="view-hello-maintenance-window-in-hello-portal"></a>Ventana de mantenimiento de Hola de vista en el portal de Hola 

Puede usar hello portal de Azure y busque las máquinas virtuales un mantenimiento programadas.

1.  Inicie sesión en toohello portal de Azure.

2.  Haga clic en y abra hello **máquinas virtuales** hoja.

3.  Haga clic en hello **columnas** lista de botones de hello tooopen de toochoose de columnas disponibles de

4.  Seleccionar y agregar hello **ventana de mantenimiento** columnas. Las máquinas virtuales que están programadas para mantenimiento tienen ventanas de mantenimiento de hello aparece. Una vez que se completa o se anula el mantenimiento, la ventana de mantenimiento desaparece.

### <a name="query-maintenance-details-using-hello-azure-api"></a>Detalles de mantenimiento de consulta mediante Hola API de Azure

Hola de uso [obtener información de máquina virtual API](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-get) y busque Hola vista toodiscover Hola mantenimiento detalles de las instancias en una máquina virtual individual. respuesta de Hello incluye Hola siguientes elementos:

  - isCustomerInitiatedMaintenanceAllowed: indica si puede ahora iniciar preferente volver a implementar en VM de Hola.

  - preMaintenanceWindowStartTime: Hola hora de inicio de la ventana de mantenimiento preventivo hello.

  - preMaintenanceWindowEndTime: Hola hora de finalización de la ventana de mantenimiento preventivo hello. Transcurrido ese tiempo, ya no podrás tooinitiate capaz de mantenimiento en esta máquina virtual.
    
  - maintenanceWindowStartTime: Hola hora de inicio de ventana de mantenimiento programada de hello cuando la máquina virtual se ven afectadas.

  - maintenanceWindowEndTime: Hola hora de finalización de la ventana de mantenimiento programada Hola.
  
  - lastOperationResultCode: Hola resultado de la última operación de volver a implementar de mantenimiento.
 
  - lastOperationMessage: mensaje que describe resultado de hello de la última operación de volver a implementar de mantenimiento.


## <a name="pre-emptive-redeploy"></a>Reimplementación preferente

Acción de preferentes volver a implementar proporciona Hola flexibilidad toocontrol Hola hora mantenimiento tooyour aplicado las máquinas virtuales en Azure. Mantenimiento planeado comienza con una ventana de mantenimiento preventivo donde puede decidir hora exacta de Hola para cada uno de los toobe máquinas virtuales que se reinicia. Estos son casos de uso en los que esta funcionalidad resulta útil:

-   Mantenimiento necesario toobe coordinada con cliente de hello final.

-   ventana de mantenimiento programada de Hola que ofrece Azure no es suficiente.
    Es posible que ventana hello tiene lugar toobe en tiempo de más ocupado hello de la semana o es demasiado largo.

-   Para varias instancias o aplicaciones de varios niveles, necesita suficiente tiempo entre dos máquinas virtuales o un determinado toofollow de secuencia.

Cuando se llama para preferente volver a implementar en una máquina virtual, mueve Hola VM tooan ya actualizado nodo y, a continuación, lo enciende volver, conservando todas las opciones de configuración y recursos asociados. Al hacerlo, el disco temporal de Hola se pierde y direcciones IP dinámicas asociadas con la interfaz de red virtual se actualizan.

La reimplementación preferente se habilita una vez por máquina virtual. Si se produce un error durante el proceso de hello, se anula la operación de hello, Hola VM no se ve afectada y se excluye de la iteración de mantenimiento de hello planeada. Se había conectado en un momento posterior a una nueva programación y se ofrece una nueva oportunidad tooschedule y secuencia Hola impacto en las máquinas virtuales.
