---
title: aaaUse toodeploy portal Azure recursos de Azure | Documentos de Microsoft
description: "Usar el portal de Azure y administración de recursos de Azure toodeploy los recursos."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 2c98a4aa-8d9f-4a0a-b764-214dbe8ed009
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 5a5217f94c8dfc0c1ebd613903ea3dcbe1197bfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a>Implementación de recursos con las plantillas de Resource Manager y el Portal de Azure
> [!div class="op_single_selector"]
> * [PowerShell](resource-group-template-deploy.md)
> * [CLI de Azure](resource-group-template-deploy-cli.md)
> * [Portal](resource-group-template-deploy-portal.md)
> * [API DE REST](resource-group-template-deploy-rest.md)
> 
> 

Este tema se muestra cómo hello toouse [portal de Azure](https://portal.azure.com) con [Azure Resource Manager](resource-group-overview.md) toodeploy los recursos de Azure. toolearn acerca de cómo administrar los recursos, consulte [recursos de Azure administrar a través del portal de](resource-group-portal.md).

Actualmente, no todos los servicios es compatible con el portal de Hola o administrador de recursos. Para esos servicios, deberá hello toouse [portal clásico](https://manage.windowsazure.com). Para el estado de Hola de cada servicio, consulte [gráfico de disponibilidad de portal de Azure](https://azure.microsoft.com/features/azure-portal/availability/).

## <a name="create-resource-group"></a>Creación de un grupo de recursos
1. Seleccione un grupo de recursos vacío, toocreate **New** > **administración** > **grupo de recursos**.
   
    ![crear un grupo de recursos vacío](./media/resource-group-template-deploy-portal/create-empty-group.png)
2. Asígnele un nombre y una ubicación y, si es necesario, seleccione una suscripción. Debe tooprovide una ubicación para el grupo de recursos de hello porque el grupo de recursos de hello almacena metadatos acerca de los recursos de Hola. Por motivos de cumplimiento, puede que desee toospecify donde se almacenan los metadatos. Por lo general, se recomienda especificar una ubicación en la que vayan a residir la mayoría de los recursos. Usar Hola mismo ubicación puede simplificar la plantilla.
   
    ![establecer valores de grupo](./media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a>Implementación de recursos desde Marketplace
Después de crear un grupo de recursos, puede implementar tooit de recursos de hello Marketplace. Hola Marketplace proporciona soluciones predefinidas para los escenarios comunes.

1. toostart una implementación, seleccione **New** y el tipo de saludo de recurso le gustaría toodeploy. A continuación, busque versión concreta de Hola de recursos de hello le gustaría toodeploy.
   
    ![implementar recursos](./media/resource-group-template-deploy-portal/deploy-resource.png)
2. Si no ve la solución concreta Hola le gustaría toodeploy, puede buscar Hola Marketplace para él.
   
    ![buscar en Marketplace](./media/resource-group-template-deploy-portal/search-resource.png)
3. Según el tipo de saludo de recursos seleccionado, tendrá una colección de propiedades relevantes tooset antes de la implementación. Estas opciones no se muestran aquí, dado que varía según el tipo de recurso. Para todos los tipos, debe seleccionar un grupo de recursos de destino. Hola imagen siguiente se muestra cómo toocreate una aplicación web e implementarlo toohello grupo de recursos que ha creado.
   
    ![Creación de un grupo de recursos](./media/resource-group-template-deploy-portal/select-existing-group.png)
   
    Como alternativa, puede decidir toocreate un grupo de recursos al implementar los recursos. Seleccione **crear nuevo** y asigne un nombre de grupo de recursos de Hola.
   
    ![crear nuevo grupo de recursos.](./media/resource-group-template-deploy-portal/select-new-group.png)
4. Comenzará la implementación. implementación de Hello podría tardar unos minutos. Cuando haya terminado la implementación de hello, verá una notificación.
   
    ![ver notificación](./media/resource-group-template-deploy-portal/view-notification.png)
5. Después de implementar los recursos, puede agregar el grupo de recursos de más recursos toohello mediante el uso de hello **agregar** comando hoja del grupo de recursos de Hola.
   
    ![agregar recurso](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a>Implementación de recursos desde plantilla personalizada
Si desea tooexecute una implementación pero no usar cualquiera de las plantillas de Hola Hola Marketplace, puede crear una plantilla personalizada que define la infraestructura de Hola para su solución. toolearn acerca de cómo crear plantillas, consulte [plantillas del Administrador de recursos de Azure de creación](resource-group-authoring-templates.md).

1. Seleccione una plantilla personalizada a través del portal de hello, toodeploy **nuevo**y empezar a buscar **implementación de plantilla** hasta que pueda seleccionar opciones de Hola.
   
    ![buscar implementación de plantilla](./media/resource-group-template-deploy-portal/search-template.png)
2. Seleccione **implementación de plantilla** de recursos disponibles Hola.
   
    ![seleccionar implementación de plantillas](./media/resource-group-template-deploy-portal/select-template.png)
3. Después de iniciar la implementación de la plantilla de hello, abra la plantilla en blanco de Hola que está disponible para personalizar.
   
    ![crear plantilla](./media/resource-group-template-deploy-portal/show-custom-template.png)
   
    En el editor de hello, agregar sintaxis de JSON de Hola que define los recursos de Hola que vaya toodeploy. Seleccione **Guardar** cuando haya terminado. Para obtener instrucciones sobre cómo escribir sintaxis de JSON de hello, consulte [tutorial de la plantilla de administrador de recursos](resource-manager-template-walkthrough.md).
   
    ![editar plantilla](./media/resource-group-template-deploy-portal/edit-template.png)
4. O bien, puede seleccionar una plantilla existente de hello [plantillas de inicio rápido de Azure](https://azure.microsoft.com/documentation/templates/). Estas plantillas se aportan por la Comunidad de Hola. Explican muchos escenarios comunes y alguien puede haber agregado una plantilla que sea similar toowhat está tratando de toodeploy. Puede buscar Hola plantillas toofind algo que coincida con su escenario.
   
    ![seleccionar plantilla de inicio rápido](./media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    Puede ver la plantilla seleccionada hello en el editor de Hola.
5. Después de proporcionar Hola todos los otros valores, seleccione **crear** plantilla de hello toodeploy. 
   
    ![implementar plantilla](./media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-tooyour-account"></a>Implementar los recursos de una plantilla guardado tooyour cuenta
Hola portal permite toosave una cuenta de Azure tooyour de plantilla y volver a implementarlo más adelante. Para obtener más información acerca de cómo trabajar con estos guardar plantillas, [empezar a trabajar con plantillas privadas en el portal de Azure hello](../marketplace-consumer/mytemplates-getstarted.md).

1. toofind las plantillas de guardado, seleccione **examinar** > **plantillas**.
   
    ![examinar plantillas](./media/resource-group-template-deploy-portal/browse-templates.png)
2. En lista de Hola de plantillas guardadas tooyour cuenta, seleccione Hola que desea toowork en.
   
    ![plantillas guardadas](./media/resource-group-template-deploy-portal/saved-templates.png)
3. Seleccione **implementar** tooredeploy Esto guarda la plantilla.
   
    ![implementar plantilla guardada](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a>Pasos siguientes
* Consulte los registros de auditoría tooview, [auditoría de las operaciones con el Administrador de recursos](resource-group-audit.md).
* errores de implementación de tootroubleshoot, consulte [ver las operaciones de implementación](resource-manager-deployment-operations.md).
* tooretrieve una plantilla de una implementación o el grupo de recursos, consulte [exportar Azure Resource Manager plantilla de recursos existentes](resource-manager-export-template.md).
* Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).

