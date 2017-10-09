---
title: aaaAuto escalar un servicio de nube en el portal de hello | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola portal tooconfigure reglas de escalado automático para un rol web de servicio de nube o el rol de trabajo en Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 701d4404-5cc0-454b-999c-feb94c1685c0
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: 265f4c8ec5e1ec2f85585df25f18cd0d0c9946a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-portal"></a>Cómo tooconfigure Autoescala para un servicio de nube en el portal de Hola
> [!div class="op_single_selector"]
> * [Portal de Azure](cloud-services-how-to-scale-portal.md)
> * [Portal de Azure clásico](cloud-services-how-to-scale.md)

Las condiciones se pueden definir para un rol de trabajo de servicio en la nube que desencadene una operación de reducción horizontal y de escalabilidad horizontal. condiciones de Hello para el rol de hello pueden basarse en hello CPU, disco o de carga de red del rol de Hola. También puede establecer una condición basada en una métrica de Hola o de cola de mensajes de algún otro recurso de Azure asociado a la suscripción.

> [!NOTE]
> Este artículo se centra en los roles de trabajo y en los roles web de Servicio en la nube. Al crear una máquina virtual (clásica) directamente, esta se hospeda en un servicio en la nube. Puede escalar una máquina virtual estándar asociándola con un [conjunto de disponibilidad](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) y activándola o desactivándola manualmente.

## <a name="considerations"></a>Consideraciones
Debe considerar Hola siguiente información antes de configurar el escalado de la aplicación:

* El uso de núcleos afecta el escalado.

    Las instancias de rol más grandes usan más núcleos. Puede escalar una aplicación solo en el límite de Hola de núcleos de su suscripción. Por ejemplo, supongamos que su suscripción tiene un límite de 20 núcleos. Si ejecuta una aplicación con dos servicios en la nube de tamaño mediano (un total de 4 núcleos), solo puede aumentar otras implementaciones de servicio de nube en su suscripción por restantes 16 núcleos de Hola. Para obtener más información sobre los tamaños, consulte [Tamaños de los servicios en la nube](cloud-services-sizes-specs.md).

* Puede realizar una operación de escalabilidad basada en un umbral de mensajes de cola. Para obtener más información acerca de cómo toouse colas, consulte [cómo toouse Hola servicio de almacenamiento cola](../storage/queues/storage-dotnet-how-to-use-queues.md).

* También puede escalar otros recursos asociados a la suscripción.

* tooenable alta disponibilidad de la aplicación, debe asegurarse de que se implementa con dos o más instancias de rol. Para obtener más información, consulte [Contratos de nivel de servicio](https://azure.microsoft.com/support/legal/sla/).


## <a name="where-scale-is-located"></a>Ubicación de la escala
Después de seleccionar el servicio en la nube, debe tener la hoja de servicio de nube de hello visible.

1. En la hoja de servicio de nube de hello en hello **Roles e instancias** icono, el nombre de hello seleccione del servicio de nube de Hola.   
   **IMPORTANTE**: hacer seguro en la nube tooclick Hola rol de servicio y no Hola instancia de rol que está por debajo de la función de Hola.

    ![](./media/cloud-services-how-to-scale-portal/roles-instances.png)
2. Seleccione hello **escala** icono.

    ![](./media/cloud-services-how-to-scale-portal/scale-tile.png)

## <a name="automatic-scale"></a>Escala automática
Puede configurar la configuración de escala de un rol con estos dos modos: **Manual** o **Automático**. Manual es el método tal como se esperaría, Establece Hola absoluta recuento de instancias. Sin embargo, automático permite tooset reglas que rigen cómo y en qué cantidad se adaptarán.

Conjunto hello **escalar** opción demasiado**reglas de programación y rendimiento**.

![Configuración de escala de servicios en la nube con el perfil y la regla](./media/cloud-services-how-to-scale-portal/schedule-basics.png)

1. Un perfil existente.
2. Agregar una regla para el perfil de hello primario.
3. Agregue otro perfil.

Seleccione **Agregar perfil**. perfil Hello determina qué modo desea toouse para la escala de hello: **siempre**, **periodicidad**, **fecha fija**.

Después de haber configurado el perfil de Hola y reglas, seleccione hello **guardar** situado en la parte superior de Hola.

#### <a name="profile"></a>Perfil
mínimo de conjuntos de perfiles de Hola y escala el número máximo de instancias para hello y también cuando este intervalo de escala está activo.

* **Siempre**

    Mantenga siempre disponible este rango de instancias.  

    ![Servicio en la nube en el que siempre se realiza la operación de escala](./media/cloud-services-how-to-scale-portal/select-always.png)
* **Periodicidad**

    Elija un conjunto de días de hello semana tooscale.

    ![Escala de servicio en la nube con una programación de periodicidad](./media/cloud-services-how-to-scale-portal/select-recurrence.png)
* **Fecha fija**

    Un rol de hello tooscale del intervalo de fecha fija.

    ![Escala de servicio en la nube con una fecha fija](./media/cloud-services-how-to-scale-portal/select-fixed.png)

Después de haber configurado el perfil de hello, seleccione hello **Aceptar** situado en parte inferior de Hola de hoja de perfil de Hola.

#### <a name="rule"></a>Regla
Las reglas se agregan tooa perfil y representan una condición que desencadena la escala de Hola.

desencadenador de la regla de Hola se basa en una métrica de servicio en la nube hello (uso de CPU, la actividad del disco o actividad de red) toowhich puede agregar un valor condicional. Además puede tener el desencadenamiento de hello basándose en una métrica de Hola o de cola de mensajes de algún otro recurso de Azure asociado a la suscripción.

![](./media/cloud-services-how-to-scale-portal/rule-settings.png)

Después de haber configurado la regla de hello, seleccione hello **Aceptar** situado en parte inferior de Hola de hoja de la regla de Hola.

## <a name="back-toomanual-scale"></a>Escala de toomanual atrás
Navegue toohello [configuración de la escala](#where-scale-is-located) conjunto hello y **escalar** opción demasiado**un recuento de instancias que especifique manualmente**.

![Configuración de escala de servicios en la nube con el perfil y la regla](./media/cloud-services-how-to-scale-portal/manual-basics.png)

Esta opción quita escalado automatizadas de rol de hello y, a continuación, puede establecer recuento de instancias de hello directamente.

1. opción de escala (manuales o automatizadas) Hola.
2. Un Hola de tooset del control deslizante de instancia de rol tooscale para las instancias.
3. Instancias de hello rol tooscale a.

Después de configurar la configuración de escalado hello, seleccione hello **guardar** situado en la parte superior de Hola.
