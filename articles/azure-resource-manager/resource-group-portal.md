---
title: aaaUse toomanage portal Azure recursos de Azure | Documentos de Microsoft
description: "Usar el portal de Azure y administración de recursos de Azure toomanage los recursos. Muestra cómo toowork con recursos de toomonitor de paneles."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 0725bbf2-5913-4c07-af6e-24e11d957fbc
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 0c89a197a31c5b6dd03ba457cb4d1fdf9f6d00f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-resources-through-portal"></a>Administración de los recursos de Azure a través del Portal
> [!div class="op_single_selector"]
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [CLI de Azure](xplat-cli-azure-resource-manager.md)
> * [Portal](resource-group-portal.md) 
> * [API DE REST](resource-manager-rest-api.md)
> 
> 

Este tema se muestra cómo hello toouse [portal de Azure](https://portal.azure.com) con [Azure Resource Manager](resource-group-overview.md) toomanage los recursos de Azure. toolearn acerca de cómo implementar los recursos a través del portal de hello, consulte [implementar los recursos con plantillas de administrador de recursos y el portal de Azure](resource-group-template-deploy-portal.md).

Actualmente, no todos los servicios es compatible con el portal de Hola o administrador de recursos. Para esos servicios, deberá hello toouse [portal clásico](https://manage.windowsazure.com). Para el estado de Hola de cada servicio, consulte [gráfico de disponibilidad de portal de Azure](https://azure.microsoft.com/features/azure-portal/availability/).

## <a name="manage-resource-groups"></a>Administración de grupos de recursos

Un grupo de recursos es un contenedor que almacena los recursos relacionados con una solución de Azure. grupo de recursos de Hello puede incluir todos los recursos de hello para la solución de hello, o sólo aquellos recursos que desea toomanage como un grupo. Decida cómo desea que los recursos de tooallocate tooresource grupos basan en lo que le resulte hello más conveniente para su organización. Por lo general, agregar recursos que comparten Hola mismo toohello de ciclo de vida mismo recurso de grupo para fácilmente puede implementar, actualizar y eliminar como un grupo. 

grupo de recursos de Hello almacena metadatos acerca de los recursos de Hola. Por lo tanto, cuando se especifica una ubicación para el grupo de recursos de hello, está especificando donde se almacenan los metadatos. Por motivos de cumplimiento, puede que necesite tooensure que se almacenan los datos en una región determinada.

1. toosee todos los grupos de recursos de hello en su suscripción, seleccione **grupos de recursos**.
   
    ![buscar grupos de recursos](./media/resource-group-portal/browse-groups.png)
2. Seleccione un grupo de recursos vacío, toocreate **agregar**.
   
    ![agregar grupo de recursos](./media/resource-group-portal/add-resource-group.png)
3. Proporcione un nombre y ubicación para el nuevo grupo de recursos Hola. Seleccione **Crear**.
   
    ![Creación de un grupo de recursos](./media/resource-group-portal/create-empty-group.png)
4. Puede que necesite tooselect **actualizar** grupo de recursos de toosee Hola creado recientemente.
   
    ![actualizar grupo de recursos](./media/resource-group-portal/refresh-resource-groups.png)
5. toocustomize Hola muestre la información de los grupos de recursos, seleccione **columnas**.
   
    ![personalizar columnas](./media/resource-group-portal/select-columns.png)
6. Seleccione Hola columnas tooadd y, a continuación, seleccione **actualización**.
   
    ![agregar columnas](./media/resource-group-portal/add-columns.png)
7. toolearn acerca de cómo implementar recursos tooyour nuevo grupo de recursos, consulte [implementar los recursos con plantillas de administrador de recursos y el portal de Azure](resource-group-template-deploy-portal.md).
8. Para el grupo de recursos de tooa de acceso rápido, puede anclar panel tooyour de hello hoja.
   
    ![anclar un grupo de recursos](./media/resource-group-portal/pin-group.png)
9. panel de Hello muestra el grupo de recursos de Hola y sus recursos. Puede seleccionar los grupos de recursos de Hola o cualquiera de sus elementos de toohello toonavigate de recursos.
   
    ![anclar un grupo de recursos](./media/resource-group-portal/show-resource-group-dashboard.png)

## <a name="tag-resources"></a>Etiquetado de recursos
Puede aplicar etiquetas tooresource grupos y recursos toologically organizar sus recursos. Para obtener información sobre cómo trabajar con etiquetas, consulte [mediante etiquetas tooorganize los recursos de Azure](resource-group-using-tags.md).

[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]

## <a name="monitor-resources"></a>Supervisión de recursos
Cuando seleccione un recurso, hoja de recursos de hello presenta predeterminado gráficos y tablas para la supervisión de ese tipo de recurso.

1. Seleccione un recurso y observe hello **supervisión** sección. Incluye gráficos que son el tipo de recurso toohello relevante. Hello siguiente imagen muestra la Hola predeterminada datos de supervisión de una cuenta de almacenamiento.
   
    ![mostrar supervisión](./media/resource-group-portal/show-monitoring.png)
2. Puede anclar una sección del panel de hello hoja tooyour seleccionando puntos suspensivos de hello (...) por encima de la sección de Hola. También puede personalizar la sección de Hola Hola tamaño en la hoja de Hola o quitarlo completamente. Hello siguiente imagen muestra cómo personalizar toopin, o quitar la sección de memoria y CPU Hola.
   
    ![anclar sección](./media/resource-group-portal/pin-cpu-section.png)
3. Después de anclar el panel de toohello sección hello, verá Hola resumen en el panel de Hola. Y, si lo selecciona inmediatamente tardarán toomore detalles acerca de los datos de Hola.
   
    ![ver panel](./media/resource-group-portal/view-startboard.png)
4. toocompletely personalizar datos de Hola para supervisar a través del portal de hello, vaya a Panel de tooyour predeterminado y seleccione **nuevo panel**.
   
    ![dashboard](./media/resource-group-portal/dashboard.png)
5. Asigne un nombre a su nuevo panel y arrastre iconos de panel Hola. Hola mosaicos se filtran por distintas opciones.
   
    ![dashboard](./media/resource-group-portal/create-dashboard.png)
   
     toolearn acerca de cómo trabajar con los paneles, consulte [crear y compartir paneles en el portal de Azure hello](../azure-portal/azure-portal-dashboards.md).

## <a name="manage-resources"></a>Administración de recursos
En la hoja de Hola para un recurso, verá opciones de Hola para administrar recursos de Hola. portal de Hello presenta opciones de administración para ese tipo de recurso determinado. Vea los comandos de administración de Hola a través de la parte superior de Hola de hoja de recursos de Hola y en el lado izquierdo de Hola.

![Administración de recursos](./media/resource-group-portal/manage-resources.png)

En estas opciones, puede realizar operaciones como iniciar y detener una máquina virtual o volver a configurar las propiedades de Hola de máquina virtual de Hola.

## <a name="move-resources"></a>Traslado de recursos
Si tiene otra suscripción o grupo de recursos de toomove recursos tooanother, consulte [Mover grupo de recursos de toonew de recursos o suscripción](resource-group-move-resources.md).

## <a name="lock-resources"></a>Bloqueo de recursos
Se pueden bloquear una suscripción, el grupo de recursos o el recurso tooprevent otros usuarios de su organización accidentalmente eliminen o modifiquen los recursos críticos. Para obtener más información, consulte [Bloqueo de recursos con el Administrador de recursos de Azure](resource-group-lock-resources.md).

[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="view-your-subscription-and-costs"></a>Consulta de sus datos de suscripción y costos
Puede ver información acerca de su suscripción y los costos de hello consolidadas para todos los recursos. Seleccione **suscripciones** y suscripción de Hola que desea toosee. Solo tendrá una tooselect de suscripción.

![suscripción](./media/resource-group-portal/select-subscription.png)

En la hoja de la suscripción de hello, verá una tasa de avance.

![tasa de evolución](./media/resource-group-portal/burn-rate.png)

Y un desglose de costos por tipo de recurso.

![costo de recursos](./media/resource-group-portal/cost-by-resource.png)

## <a name="export-template"></a>Exportación de la plantilla
Después de configurar el grupo de recursos, puede que desee plantilla de administrador de recursos de tooview Hola Hola para grupo de recursos. Exportar plantilla Hola ofrece dos ventajas:

1. Puede automatizar fácilmente las futuras implementaciones de soluciones de hello como plantilla de hello contiene toda la infraestructura de hello todos los.
2. Familiarícese con la sintaxis de plantilla examinando Hola JavaScript Object Notation (JSON) que representa la solución.

Para obtener instrucciones detalladas, consulte [Exportación de plantillas de Azure Resource Manager desde recursos existentes](resource-manager-export-template.md).

## <a name="delete-resource-group-or-resources"></a>Eliminación de los recursos o grupos de recursos
Eliminar un grupo de recursos, elimina todos los recursos de hello incluidos en él. También puede eliminar recursos individuales de un grupo de recursos. Desea tooexercise cuidado al eliminar un grupo de recursos porque podría haber recursos en otros grupos de recursos que están vinculado tooit. El Administrador de recursos no se eliminan los recursos vinculados, pero no pueden funcionar correctamente sin recursos Hola esperado.

![eliminar grupo](./media/resource-group-portal/delete-group.png)

## <a name="next-steps"></a>Pasos siguientes
* registros de actividad de tooview, consulte [auditoría de las operaciones con el Administrador de recursos](resource-group-audit.md).
* tooview obtener información detallada acerca de una implementación, vea [ver las operaciones de implementación](resource-manager-deployment-operations.md).
* toodeploy recursos a través del portal de hello, consulte [implementar los recursos con plantillas de administrador de recursos y el portal de Azure](resource-group-template-deploy-portal.md).
* toomanage tooresources de acceso, consulte [usar recursos de suscripción de Azure de rol asignaciones toomanage acceso tooyour](../active-directory/role-based-access-control-configure.md).
* Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).

