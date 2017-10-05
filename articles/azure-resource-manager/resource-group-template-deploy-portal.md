---
title: Uso de Azure Portal para implementar los recursos de Azure | Microsoft Docs
description: Utilice el Portal de Azure y Azure Resource Manager para implementar los recursos.
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
ms.openlocfilehash: a4cac5834c667976b0a2d1f2748e4309a166d16a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a>Implementación de recursos con las plantillas de Resource Manager y el Portal de Azure
> [!div class="op_single_selector"]
> * [PowerShell](resource-group-template-deploy.md)
> * [CLI de Azure](resource-group-template-deploy-cli.md)
> * [Portal](resource-group-template-deploy-portal.md)
> * [API DE REST](resource-group-template-deploy-rest.md)
> 
> 

En este tema se muestra cómo utilizar [Azure Portal](https://portal.azure.com) con [Azure Resource Manager](resource-group-overview.md) para implementar los recursos de Azure. Para obtener más información sobre cómo administrar los recursos, consulte [Administración de los recursos de Azure a través del Portal](resource-group-portal.md).

Actualmente, no todos los servicios son compatibles con el portal o con el Administrador de recursos. Para esos servicios, deberá usar el [portal clásico](https://manage.windowsazure.com). Para obtener más información sobre el estado de cada servicio, consulte [Tabla de disponibilidad de los portales de Azure](https://azure.microsoft.com/features/azure-portal/availability/).

## <a name="create-resource-group"></a>Creación de un grupo de recursos
1. Para crear un grupo de recursos vacío, seleccione **Nuevo** > **Administración** > **Grupo de recursos**.
   
    ![crear un grupo de recursos vacío](./media/resource-group-template-deploy-portal/create-empty-group.png)
2. Asígnele un nombre y una ubicación y, si es necesario, seleccione una suscripción. Debe proporcionar una ubicación para el grupo de recursos porque este almacena metadatos sobre los recursos. Por motivos de cumplimiento, debería especificar dónde se almacenan esos metadatos. Por lo general, se recomienda especificar una ubicación en la que vayan a residir la mayoría de los recursos. Si usa la misma ubicación, puede simplificar la plantilla.
   
    ![establecer valores de grupo](./media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a>Implementación de recursos desde Marketplace
Una vez creado el grupo de recursos, puede implementar recursos en él desde Marketplace. Marketplace proporciona soluciones predefinidas para escenarios habituales.

1. Para iniciar la implementación, seleccione **Nuevo** y el tipo de recurso que quiere implementar. A continuación, busque la versión concreta del recurso que le gustaría implementar.
   
    ![implementar recursos](./media/resource-group-template-deploy-portal/deploy-resource.png)
2. Si no ve la solución específica que gustaría implementar, búsquela en Marketplace.
   
    ![buscar en Marketplace](./media/resource-group-template-deploy-portal/search-resource.png)
3. Según el tipo del recurso seleccionado, tiene una colección de propiedades pertinentes que debe establecer antes de la implementación. Estas opciones no se muestran aquí, dado que varía según el tipo de recurso. Para todos los tipos, debe seleccionar un grupo de recursos de destino. En la imagen siguiente se muestra cómo crear una aplicación web e implementarla en el grupo de recursos que ha creado.
   
    ![Creación de un grupo de recursos](./media/resource-group-template-deploy-portal/select-existing-group.png)
   
    Como alternativa, puede decidir crear un nuevo grupo de recursos al implementar estos últimos. Seleccione **Crear nuevo** y asígnele un nombre al grupo de recursos.
   
    ![crear nuevo grupo de recursos.](./media/resource-group-template-deploy-portal/select-new-group.png)
4. Comenzará la implementación. Esta puede tardar unos minutos. Cuando haya terminado la implementación, verá una notificación.
   
    ![ver notificación](./media/resource-group-template-deploy-portal/view-notification.png)
5. Después de implementar los recursos, puede agregar más recursos al grupo de recursos mediante el comando **Agregar** de la hoja del grupo de recursos.
   
    ![agregar recurso](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a>Implementación de recursos desde plantilla personalizada
Si desea ejecutar una implementación sin usar las plantillas de Marketplace, puede crear una plantilla personalizada que defina la infraestructura para la solución. Para obtener más información sobre la creación de plantillas, vea [Creación de plantillas del Administrador de recursos de Azure](resource-group-authoring-templates.md).

1. Para implementar una plantilla personalizada a través del portal, seleccione **Nuevo** y busque **Implementación de plantillas** hasta que pueda seleccionarla entre las opciones.
   
    ![buscar implementación de plantilla](./media/resource-group-template-deploy-portal/search-template.png)
2. Seleccione **Implementación de plantillas** en los recursos disponibles.
   
    ![seleccionar implementación de plantillas](./media/resource-group-template-deploy-portal/select-template.png)
3. Después de iniciar la implementación de la plantilla, abra la plantilla en blanco que está disponible para la personalización.
   
    ![crear plantilla](./media/resource-group-template-deploy-portal/show-custom-template.png)
   
    En el editor, agregue la sintaxis JSON que define los recursos que desea implementar. Seleccione **Guardar** cuando haya terminado. Para obtener instrucciones sobre cómo escribir la sintaxis JSON, consulte el [Tutorial de la plantilla de Resource Manager](resource-manager-template-walkthrough.md).
   
    ![editar plantilla](./media/resource-group-template-deploy-portal/edit-template.png)
4. O bien puede seleccionar una plantilla existente en [Plantillas de inicio rápido de Azure](https://azure.microsoft.com/documentation/templates/). Estas plantillas son aportaciones de la comunidad. Abarcan muchos escenarios comunes y puede que alguien haya agregado una plantilla que sea similar a lo que desea implementar. Puede buscar las plantillas para encontrar alguna que coincida con su escenario.
   
    ![seleccionar plantilla de inicio rápido](./media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    Puede ver la plantilla seleccionada en el editor.
5. Después de proporcionar todos los demás valores, seleccione **Crear** para implementar la plantilla. 
   
    ![implementar plantilla](./media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-to-your-account"></a>Implementación de los recursos desde una plantilla guardada en la cuenta
El portal permite guardar una plantilla en su cuenta de Azure y volver a implementarla más adelante. Para obtener más información sobre cómo trabajar con estas plantillas guardadas, consulte [Introducción a las plantillas privadas del Portal de Azure](../marketplace-consumer/mytemplates-getstarted.md).

1. Para buscar las plantillas guardadas, seleccione **Examinar** > **Plantillas**.
   
    ![examinar plantillas](./media/resource-group-template-deploy-portal/browse-templates.png)
2. En la lista de plantillas guardadas en su cuenta, seleccione aquella en la que desea trabajar.
   
    ![plantillas guardadas](./media/resource-group-template-deploy-portal/saved-templates.png)
3. Seleccione **Implementar** para volver a implementar esta plantilla guardada.
   
    ![implementar plantilla guardada](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a>Pasos siguientes
* Para ver los registros de auditoría, consulte [Operaciones de auditoría con Resource Manager](resource-group-audit.md).
* Para solucionar errores de implementación, vea [View deployment operations](resource-manager-deployment-operations.md) (Ver operaciones de implementación).
* Para recuperar una plantilla de una implementación o un grupo de recursos, consulte [Exportación de plantillas de Azure Resource Manager desde recursos existentes](resource-manager-export-template.md).
* Para obtener instrucciones sobre cómo las empresas pueden utilizar Resource Manager para administrar eficazmente las suscripciones, vea [Scaffold empresarial de Azure: Gobierno de suscripción prescriptivo](resource-manager-subscription-governance.md).

