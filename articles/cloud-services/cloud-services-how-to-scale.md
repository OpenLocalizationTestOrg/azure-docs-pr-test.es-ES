---
title: "aaaAuto escalar un servicio de nube en el portal clásico de hello | Documentos de Microsoft"
description: "(clásico) Obtenga información acerca de cómo toouse Hola tooconfigure portal clásico reglas de escalado automático para un rol web de servicio de nube o el rol de trabajo en Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: eb167d70-4eba-42a4-b157-d8d0688abf4b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: ddb5816d4d22192c6d2f51d7508e390779742078
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-classic-portal"></a>Cómo tooconfigure Autoescala para un servicio de nube en el portal clásico de Hola
> [!div class="op_single_selector"]
> * [Portal de Azure](cloud-services-how-to-scale-portal.md)
> * [Portal de Azure clásico](cloud-services-how-to-scale.md)

En página de escala de Hola de hello portal de Azure clásico, puede configurar la configuración de escalado automático para el rol web o el rol de trabajo. También puede configurar el escalado manual en lugar del escalado automático basado en reglas.

> [!NOTE]
> Este artículo se centra en los roles de trabajo y en los roles web de Servicio en la nube. Al crear una máquina virtual (clásica) directamente, esta se hospeda en un servicio en la nube. Parte de esta información se aplica tipos de toothese de máquinas virtuales. Ajuste de escala en un conjunto de disponibilidad de máquinas virtuales es simplemente va a cerrar ellos activar y desactivar en función de las reglas de la escala de Hola que configure. Para obtener más información sobre máquinas virtuales y los conjuntos de disponibilidad, consulte [administrar Hola disponibilidad de máquinas virtuales](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

Debe considerar Hola siguiente información antes de configurar el escalado de la aplicación:

* El uso de núcleos afecta el escalado.

    Las instancias de rol más grandes usan más núcleos. Puede escalar una aplicación solo en el límite de Hola de núcleos de su suscripción. Por ejemplo, supongamos que su suscripción tiene un límite de 20 núcleos. Si ejecuta una aplicación con dos servicios en la nube de tamaño mediano (un total de 4 núcleos), solo puede aumentar otras implementaciones de servicio de nube en su suscripción por restantes 16 núcleos de Hola. Para obtener más información sobre los tamaños, consulte [Tamaños de los servicios en la nube](cloud-services-sizes-specs.md).

* Debe crear una cola y asociarla con un rol para poder escalar una aplicación según el umbral de un mensaje. Para obtener más información, consulte [cómo toouse Hola servicio de almacenamiento cola](../storage/queues/storage-dotnet-how-to-use-queues.md).

* Puede escalar los recursos que están vinculado tooyour servicio en la nube. Para obtener más información acerca de la vinculación de recursos, consulte [Cómo: vincular un servicio de nube de recursos tooa](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).

* tooenable alta disponibilidad de la aplicación, debe asegurarse de que se implementa con dos o más instancias de rol. Para obtener más información, consulte [Contratos de nivel de servicio](https://azure.microsoft.com/support/legal/sla/).

## <a name="schedule-scaling"></a>Programar escalado
De forma predeterminada, todos los roles no siguen una programación específica. Por lo tanto, de aplicarse cualquier configuración cambiado tooall veces y todos los días a lo largo del año de Hola. Si lo desea, puede configurar el ajuste de escala manual o automática para uno de los siguientes modos de hello:

* Días laborables
* Fines de semana
* Noches entre semana
* Mañanas entre semana
* Fechas específicas
* Intervalos de fechas específicas

Hello programación se establece en hello [portal de Azure clásico](https://manage.windowsazure.com/) en hello  
**Cloud Services** > **\[Su servicio en la nube\]** > **Escala** > **\[Producción y almacenamiento provisional\]**.

Haga clic en hello **configurar horas de programación** botón para cada rol que desee toochange.

![Escalado automático en un servicio en la nube basado en una programación][scale_schedules]

## <a name="manual-scale"></a>Escala manual
En hello **escala** página, puede manualmente aumentar o reducir el número de Hola de instancias en ejecución en un servicio de nube. Esta opción se configura para cada programación que haya creado o un tiempo de tooall si no ha creado una programación.

1. Hola [portal de Azure clásico](https://manage.windowsazure.com/), haga clic en **servicios en la nube**y, a continuación, haga clic en nombre de Hola Hola nube tooopen Hola de panel de servicio.
   
   > [!TIP]
   > Si no ve el servicio en la nube, puede que necesite toochange de **producción** demasiado**ensayo** o viceversa.

2. Haga clic en **Escalar**.
3. Seleccione la programación de hello desea toochange opciones para de escalado. *Ya no las horas programadas* es predeterminado de hello si no tienes ninguna programación definida.
4. Buscar hello **escalar por métrica** sección y seleccione **NONE**. Este valor es el predeterminado de Hola para todos los roles.
5. Cada función hello del servicio en nube tiene un control deslizante para cambiar el número de Hola de toouse de instancias.
   
    ![Escalar manualmente un rol de servicio en la nube][manual_scale]
   
    Si tiene varias instancias, puede que tenga hello toochange [tamaño de máquina virtual de servicio de nube](cloud-services-sizes-specs.md).
6. Haga clic en **Guardar**.  
   Las instancias de rol se agregan o quitan según las selecciones realizadas.

> [!TIP]
> Siempre que vea ![][tip_icon] mover su tooit de mouse (ratón) y también puede obtener ayuda acerca de una configuración específica de qué hace.

## <a name="automatic-scale---cpu"></a>Escala automática: CPU
Este modo de escala si deja de porcentaje medio de hello del uso de CPU por encima o por debajo de los umbrales especificados. Las instancias de rol se crean o eliminan cuando esto ocurre.

1. Hola [portal de Azure clásico](https://manage.windowsazure.com/), haga clic en **servicios en la nube**y, a continuación, haga clic en nombre de Hola Hola nube tooopen Hola de panel de servicio.
   
   > [!TIP]
   > Si no ve el servicio en la nube, puede que necesite toochange de **producción** demasiado**ensayo** o viceversa.

2. Haga clic en **Escalar**.
3. Seleccione la programación de hello desea toochange opciones para de escalado. *Ya no las horas programadas* es predeterminado de hello si no tienes ninguna programación definida.
4. Buscar hello **escalar por métrica** sección y seleccione **CPU**.
5. Ahora puede configurar un intervalo mínimo y máximo de instancias de roles, el uso de CPU de destino de hello (tootrigger una ampliación vertical) y cuántas instancias tooscale hacia arriba y hacia abajo por.

![Escalar un rol de servicio en la nube con la carga de la CPU][cpu_scale]

> [!TIP]
> Siempre que vea ![][tip_icon] mover su tooit de mouse (ratón) y también puede obtener ayuda acerca de una configuración específica de qué hace.

## <a name="automatic-scale---queue"></a>Escala automática: Cola
Este modo se escala automáticamente si número Hola de mensajes en una cola pasa por encima o por debajo del umbral especificado. Las instancias de rol se crean o eliminan cuando esto ocurre.

1. Hola [portal de Azure clásico](https://manage.windowsazure.com/), haga clic en **servicios en la nube**y, a continuación, haga clic en nombre de Hola Hola nube tooopen Hola de panel de servicio.
   
   > [!TIP]
   > Si no ve el servicio en la nube, puede que necesite toochange de **producción** demasiado**ensayo** o viceversa.

2. Haga clic en **Escalar**.
3. Buscar hello **escalar por métrica** sección y seleccione **cola**.
4. Ahora puede configurar un intervalo mínimo y máximo de instancias de roles, cola de Hola y el número de cola mensajes tooprocess para cada instancia y cuántos tooscale de instancias avanzar y retroceder por.

![Escalar un rol de servicio en la nube con una cola de mensajes][queue_scale]

> [!TIP]
> Siempre que vea ![][tip_icon] mover su tooit de mouse (ratón) y también puede obtener ayuda acerca de una configuración específica de qué hace.

## <a name="scale-linked-resources"></a>Escalado de recursos vinculados
A menudo, cuando escalar un rol, es la base de datos de Hola de tooscale beneficioso aplicación hello usa también. Si vincula el servicio en la nube toohello Hola base de datos, puede tener acceso a Hola ajuste de escala en configuración para ese recurso haciendo clic en el vínculo apropiado de Hola.

1. Hola [portal de Azure clásico](https://manage.windowsazure.com/), haga clic en **servicios en la nube**y, a continuación, haga clic en nombre de Hola Hola nube tooopen Hola de panel de servicio.
   
   > [!TIP]
   > Si no ve el servicio en la nube, puede que necesite toochange de **producción** demasiado**ensayo** o viceversa.

2. Haga clic en **Escalar**.
3. Buscar hello **recursos vinculados** sección y haga clic en **administrar el escalado de esta base de datos**.
   
   > [!NOTE]
   > Si no ve la sección **recursos vinculados** , probablemente no tenga ningún recurso vinculado.

![][linked_resource]

[manual_scale]: ./media/cloud-services-how-to-scale/manual-scale.png
[queue_scale]: ./media/cloud-services-how-to-scale/queue-scale.png
[cpu_scale]: ./media/cloud-services-how-to-scale/cpu-scale.png
[tip_icon]: ./media/cloud-services-how-to-scale/tip.png
[scale_schedules]: ./media/cloud-services-how-to-scale/schedules.png
[scale_popup]: ./media/cloud-services-how-to-scale/schedules-dialog.png
[linked_resource]: ./media/cloud-services-how-to-scale/linked-resources.png
