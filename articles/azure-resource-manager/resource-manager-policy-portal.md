---
title: portal de aaaAzure para las directivas de recursos | Documentos de Microsoft
description: "Describe cómo toouse toocreate de portal de Azure y administrar las directivas del Administrador de recursos. Se pueden aplicar directivas en grupos de suscripción o el recurso de Hola."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: tomfitz
ms.openlocfilehash: ce6413386317e532b63761a24458b85c996af4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-tooassign-and-manage-resource-policies"></a>Usar tooassign de portal de Azure y administrar las directivas de recursos
Hola portal de Azure permite las suscripciones y se tooassign directivas tooresource grupos de recursos. interfaz de usuario de Hello resulta fácil tooselect directiva de Hola que desee tooassign y especificar valores de parámetro para esa configuración de directiva de directiva toocustomize Hola. 

tooassign una directiva mediante el portal de hello, definición de directiva de hello ya debe existir en la suscripción. La suscripción tiene varias definiciones de directivas integradas que están listas para que los grupos de tooresource tooassign o suscripciones. Verá estas directivas integradas y directivas personalizadas que ha definido cuando mediante directivas de hello tooassign portal. Para una introducción toopolicies y cómo personalizar la directiva toodefine, consulte [información general de directivas de recursos](resource-manager-policy.md).

Todos los recursos secundarios heredan las directivas. Por lo tanto, si una directiva aplicada tooa grupo de recursos, es aplicable tooall recursos de hello en ese grupo de recursos. En este artículo, el término de hello **ámbito** hace referencia toohello grupo de recursos o suscripción que se asigna la directiva de Hola. 

Las directivas se evalúan al crear y actualizar los recursos (operaciones PUT y PATCH).

## <a name="assign-a-policy"></a>Asignación de una directiva

1. tooassign un tooeither directiva un grupo de recursos o suscripción, seleccione ese grupo de recursos o suscripción. En configuración de hello, seleccione **directivas**.

   ![seleccionar directivas](./media/resource-manager-policy-portal/select-policies.png)

2. Seleccione una asignación de directiva para este ámbito, toocreate **Agregar asignación de**.

   ![agregar asignación](./media/resource-manager-policy-portal/add-assignment.png)

3. Seleccione la directiva de hello desea tooassign. Incluso si no ha agregado ninguna suscripción de tooyour de definiciones de directivas, consulte directivas integradas de Hola que están disponibles para la asignación. Estas directivas integradas abarcan muchos escenarios comunes.

   ![seleccionar definición](./media/resource-manager-policy-portal/select-definition.png)

4. Después de seleccionar una directiva, verá una descripción de la directiva de Hola y los parámetros de la directiva. Por ejemplo, hello siguiente imagen muestra hello **permitido ubicaciones** parámetro, que es necesario para la directiva de Hola que restringe las ubicaciones disponibles Hola.

   ![mostrar parámetros](./media/resource-manager-policy-portal/show-parameters.png)

5. A través de la interfaz de usuario de hello, seleccione hello toospecify de valores para parámetros de la directiva de hello (por ejemplo, ubicaciones de Hola que pueden usarse para la implementación).

   ![seleccionar valores de parámetros](./media/resource-manager-policy-portal/select-parameters.png)

6. Proporcione valores de hello otros parámetros. ámbito de Hola se asigna automáticamente en función de hoja de Hola que seleccionó al iniciar la asignación de directiva de Hola. Seleccione **Aceptar** cuando haya terminado.

   ![definir parámetros](./media/resource-manager-policy-portal/define-parameters.png)

  Se ha asignado la directiva de hello toohello especifica el ámbito.

## <a name="view-policy-assignments"></a>Visualización de asignaciones de directiva

Después de asignar una directiva, se observa en la lista de Hola de directivas para ese ámbito. Hola **detalles** ficha muestra un resumen de la asignación de directivas Hola.

![mostrar detalles](./media/resource-manager-policy-portal/show-details.png)

Hola **regla de asignación** ficha muestra hello JSON para la definición de la directiva de Hola.

![mostrar regla de asignación](./media/resource-manager-policy-portal/show-assignment-rule.png)

## <a name="change-an-existing-policy-assignment"></a>Cambio de una asignación de directiva existente

toochange una directiva, seleccione **Editar asignación de** o **eliminar**

![editar o eliminar asignación](./media/resource-manager-policy-portal/edit-delete-policy.png)

## <a name="assign-custom-policies"></a>Asignación de directivas personalizadas

Si ha definido las directivas personalizadas en su suscripción, esas directivas están disponibles para la asignación mediante el portal de Hola. Delante de dichas políticas aparece **[Custom]**

![directivas personalizadas](./media/resource-manager-policy-portal/show-custom-policy.png)

## <a name="next-steps"></a>Pasos siguientes
* toolearn acerca de la sintaxis JSON de Hola para definir las directivas, consulte [información general de directivas de recursos](resource-manager-policy.md).
* Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).
* esquema de la directiva de Hola se publica en [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json). 

