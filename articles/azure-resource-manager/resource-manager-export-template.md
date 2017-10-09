---
title: plantilla de Azure Resource Manager aaaExport | Documentos de Microsoft
description: "Use Administración de recursos de Azure tooexport una plantilla a partir de un grupo de recursos existente."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 5f5ca940-eef8-4125-b6a0-f44ba04ab5ab
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/06/2017
ms.author: tomfitz
ms.openlocfilehash: 94daa4812da2fec705044ca31c8e74e6d59bd53f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="export-an-azure-resource-manager-template-from-existing-resources"></a>Exportación de plantillas de Azure Resource Manager desde recursos existentes
En este artículo, aprenderá cómo tooexport una plantilla de administrador de recursos de los recursos existentes en su suscripción. Puede usar ese toogain plantilla generada una mejor comprensión de la sintaxis de la plantilla.

Hay dos tooexport de formas de una plantilla:

* Puede exportar hello **plantilla real que se utiliza para la implementación**. plantilla exportada Hola incluye todas las variables y parámetros de hello exactamente tal y como aparecían en la plantilla original Hola. Este enfoque resulta útil si ha implementado los recursos a través del portal de Hola y desea toosee Hola plantilla toocreate esos recursos. Esta plantilla es fácil de usar. 
* Puede exportar un **genera plantilla que representa el estado actual de Hola Hola del grupo de recursos**. plantilla exportada Hello no se basa en cualquier plantilla que utiliza para la implementación. En su lugar, crea una plantilla que es una instantánea Hola del grupo de recursos. plantilla exportada Hello tiene muchos valores codificados de forma rígida y probablemente no tantos parámetros como normalmente tendría que definir. Este enfoque es útil cuando se ha modificado el grupo de recursos de hello después de la implementación. Para poder usar esta plantilla, normalmente es preciso realizar ciertas modificaciones en ella.

En este tema se muestra ambos enfoques a través del portal de Hola.

## <a name="deploy-resources"></a>Implementación de recursos
Empecemos por tooAzure de recursos que puede usar para exportar como una plantilla de implementación. Si ya tiene un grupo de recursos en la suscripción que desea que la plantilla de tooa tooexport, puede omitir esta sección. resto de Hola de este artículo se da por supuesto que haya implementado la aplicación web de hello y solución de base de datos SQL que se muestra en esta sección. Si utiliza una solución distinta, su experiencia podría ser un poco diferente, pero Hola pasos hello tooexport una plantilla son iguales. 

1. Hola [portal de Azure](https://portal.azure.com), seleccione **nuevo**.
   
      ![seleccionar Nuevo](./media/resource-manager-export-template/new.png)
2. Busque **web app + SQL** y selecciónelo en las opciones disponibles de Hola.
   
      ![buscar aplicación web y SQL](./media/resource-manager-export-template/webapp-sql.png)

3. Seleccione **Crear**.

      ![seleccionar crear](./media/resource-manager-export-template/create.png)

4. Proporcionar valores de hello necesario para la aplicación web de hello y base de datos SQL. Seleccione **Crear**.

      ![proporcionar valor de web y SQL](./media/resource-manager-export-template/provide-web-values.png)

implementación de Hello puede tardar un minuto. Una vez finalizada la implementación de hello, su suscripción contiene solución Hola.

## <a name="view-template-from-deployment-history"></a>Visualización de una plantilla desde el historial de implementaciones
1. Vaya toohello hoja de grupo de recursos para el nuevo grupo de recursos. Tenga en cuenta que esa hoja hello muestra el resultado de hello de última implementación de Hola. Seleccione este vínculo.
   
      ![Hoja del grupo de recursos](./media/resource-manager-export-template/select-deployment.png)
2. Ver un historial de las implementaciones para el grupo de Hola. En su caso, hoja de hello probablemente muestra solo una implementación. Selecciónela.
   
     ![última implementación](./media/resource-manager-export-template/select-history.png)
3. hoja de Hello muestra un resumen de implementación de Hola. Hola resumen incluye el estado de Hola de implementación de Hola y sus operaciones y los valores de hello proporcionada para los parámetros. plantilla de hello toosee que usó para la implementación de hello, seleccione **plantilla de vista**.
   
     ![Ver el resumen de la implementación](./media/resource-manager-export-template/view-template.png)
4. El Administrador de recursos recupera Hola siguientes siete archivos automáticamente:
   
   1. **Plantilla** -plantilla de Hola que define la infraestructura de Hola para su solución. Cuando crea la cuenta de almacenamiento de Hola a través del portal de Hola, Administrador de recursos usa una plantilla toodeploy y guarda dicha plantilla para futuras referencias.
   2. **Parámetros** -un archivo de parámetros que puede utilizar toopass en valores durante la implementación. Contiene valores de hello que proporcionó durante la primera implementación de Hola. Puede cambiar cualquiera de estos valores al volver a implementar la plantilla de Hola.
   3. **CLI** -archivo de script de Azure comandos línea interfaz (CLI) que puede usar la plantilla de hello toodeploy.
   3. **CLI 2.0** -archivo de script de Azure comandos línea interfaz (CLI) que puede usar la plantilla de hello toodeploy.
   4. **PowerShell** -PowerShell de Azure un archivo de script que puede usar la plantilla de hello toodeploy.
   5. **.NET** -clase A .NET que puede usar la plantilla de hello toodeploy.
   6. **Ruby** -clase A Ruby que puede usar la plantilla de hello toodeploy.
      
      archivos de Hello están disponibles a través de vínculos a través de la hoja de Hola. De forma predeterminada, hoja de hello muestra la plantilla de Hola.
      
       ![Ver plantilla](./media/resource-manager-export-template/see-template.png)
      
Esta plantilla es plantilla real de hello usa toocreate su aplicación web y la base de datos SQL. Tenga en cuenta que contiene parámetros que permiten valores diferentes tooprovide durante la implementación. toolearn más información acerca de la estructura de Hola de una plantilla, consulte [plantillas del Administrador de recursos de Azure de creación](resource-group-authoring-templates.md).

## <a name="export-hello-template-from-resource-group"></a>Exportar plantilla Hola del grupo de recursos
Si manualmente ha cambiado los recursos o agregado recursos en varias implementaciones, la recuperación de una plantilla de historial de implementación de hello no refleja estado actual de Hola Hola del grupo de recursos. Esta sección muestra cómo tooexport una plantilla que refleja Hola estado actual del grupo de recursos de Hola. 

> [!NOTE]
> No se puede exportar una plantilla a un grupo de recursos que tenga más de doscientos recursos.
> 
> 

1. plantilla de hello tooview para un grupo de recursos, seleccione **script de automatización**.
   
      ![exportar grupo de recursos](./media/resource-manager-export-template/select-automation.png)
   
     Administrador de recursos se evalúa como recursos de hello en el grupo de recursos de Hola y genera una plantilla para esos recursos. No todos los tipos de recursos admiten la función de plantilla de exportación de Hola. Puede ver un error que indica que hay un problema con la exportación de Hola. Obtener información sobre cómo toohandle los problemas en hello [problemas de exportación de corrección](#fix-export-issues) sección.
2. Nuevo, verá seis archivos de Hola que puede usar la solución de hello tooredeploy. Sin embargo, esta plantilla en tiempo de hello es algo diferente. Tenga en cuenta que Hola plantilla generada contiene menos parámetros de plantilla de hello en la sección anterior. Además, muchos de los valores de hello (por ejemplo, ubicación y los valores SKU) están codificados en esta plantilla, en lugar de aceptar un valor de parámetro. Antes de volver a usar esta plantilla, puede ser conveniente tooedit Hola plantilla toomake un mejor uso de parámetros. 
   
3. Tiene dos opciones para continuar toowork con esta plantilla. Puede descargar la plantilla de Hola y trabajar con ella localmente con un editor de JSON. O bien, puede guardar la biblioteca de plantillas tooyour de Hola y trabajar con ella a través del portal de Hola.
   
     Si está familiarizado con un editor de JSON como [VS Code](https://code.visualstudio.com/) o [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), podría ser preferible Descargar plantilla de hello localmente y usar ese editor. toowork localmente, seleccione **descargar**.
   
      ![Descargar plantilla](./media/resource-manager-export-template/download-template.png)
   
     Si no se configuran con un editor de JSON, quizá prefiera Editar plantilla de Hola a través del portal de Hola. resto de Hola de este tema se da por supuesto que ha guardado tooyour biblioteca de plantillas de hello en el portal de Hola. Sin embargo, asegúrese de Hola mismo cambios de sintaxis toohello plantilla si trabajar localmente con un editor de JSON o a través del portal de Hola. Seleccione toowork a través del portal de hello, **agregar toolibrary**.
   
      ![Agregar toolibrary](./media/resource-manager-export-template/add-to-library.png)
   
     Al agregar una biblioteca de plantillas de toohello, asigne el libro de hello un nombre y una descripción. Después, seleccione **Guardar**.
   
     ![establecer valores de plantilla](./media/resource-manager-export-template/save-library-template.png)
4. tooview una plantilla que se guardan en la biblioteca, seleccione **más servicios**, tipo **plantillas** toofilter resultados, seleccionados **plantillas**.
   
      ![buscar plantillas](./media/resource-manager-export-template/find-templates.png)
5. Seleccione la plantilla de hello con nombre hello guardó.
   
      ![seleccionar plantilla](./media/resource-manager-export-template/select-saved-template.png)

## <a name="customize-hello-template"></a>Personalizar la plantilla de Hola
plantilla de Hola exportado funciona bien que si desea toocreate Hola mismo web de aplicación y base de datos SQL para cada implementación. No obstante, Resource Manager proporciona opciones para que pueda implementar plantillas con mucha más flexibilidad. Este artículo muestra cómo la base de parámetros de tooadd para hello datos nombre de administrador y la contraseña. Puede utilizar este mismo tooadd enfoque más flexibilidad para otros valores en plantilla Hola.

1. plantilla de toocustomize hello, seleccione **editar**.
   
     ![mostrar plantilla](./media/resource-manager-export-template/select-edit.png)
2. Seleccione la plantilla de Hola.
   
     ![editar plantilla](./media/resource-manager-export-template/select-added-template.png)
3. valores de hello toopass capaz de toobe que puede querer toospecify durante la implementación, agregan Hola siguiendo dos toohello parámetros **parámetros** sección en la plantilla de hello:

   ```json
   "administratorLogin": {
       "type": "String"
   },
   "administratorLoginPassword": {
       "type": "SecureString"
   },
   ```

4. toouse Hola nuevos parámetros, reemplace la definición de SQL server de Hola Hola **recursos** sección. Tenga en cuenta que **administratorLogin** y **administratorLoginPassword** ahora usan los valores de los parámetros.

   ```json
   {
       "comments": "Generalized from resource: '/subscriptions/{subscription-id}/resourceGroups/exportsite/providers/Microsoft.Sql/servers/tfserverexport'.",
       "type": "Microsoft.Sql/servers",
       "kind": "v12.0",
       "name": "[parameters('servers_tfserverexport_name')]",
       "apiVersion": "2014-04-01-preview",
       "location": "South Central US",
       "scale": null,
       "properties": {
           "administratorLogin": "[parameters('administratorLogin')]",
           "administratorLoginPassword": "[parameters('administratorLoginPassword')]",
           "version": "12.0"
       },
       "dependsOn": []
   },
   ```

6. Seleccione **Aceptar** cuando termine de editar plantillas de Hola.
7. Seleccione **guardar** plantilla toohello cambios hello en toosave.
   
     ![guardar plantilla](./media/resource-manager-export-template/save-template.png)
8. plantilla de tooredeploy Hola actualizado, seleccione **implementar**.
   
     ![implementar plantilla](./media/resource-manager-export-template/redeploy-template.png)
9. Proporcionar valores de parámetros y seleccione un grupo toodeploy Hola de recursos a.


## <a name="fix-export-issues"></a>Solución de problemas de exportación
No todos los tipos de recursos admiten la función de plantilla de exportación de Hola. tooresolve manualmente este problema vuelva a agregar los recursos que faltan de Hola a la plantilla. mensaje de error de Hello incluye tipos de recursos de Hola que no se puede exportar. Busque el tipo de recurso en [Referencia de plantilla](/azure/templates/). Por ejemplo, toomanually agregar una puerta de enlace de red virtual, vea [referencia de plantillas de Microsoft.Network/virtualNetworkGateways](/azure/templates/microsoft.network/virtualnetworkgateways).

> [!NOTE]
> Solo se encuentran problemas de exportación si se exporta desde un grupo de recursos en lugar de desde el historial de implementación. Si la última implementación representa con precisión el estado actual de Hola Hola del grupo de recursos, debe exportar plantilla Hola de historial de implementación de hello en lugar de grupo de recursos de Hola. Exportar sólo desde un grupo de recursos cuando haya realizado el grupo de recursos de toohello de cambios que no estén definidos en una única plantilla.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
Ha aprendido cómo tooexport una plantilla de recursos que creó en el portal de Hola.

* Puede implementar una plantilla mediante [PowerShell](resource-group-template-deploy.md), [CLI de Azure](resource-group-template-deploy-cli.md), o [API de REST](resource-group-template-deploy-rest.md).
* toosee tooexport una plantilla a través de PowerShell, vea [con Azure PowerShell con el Administrador de recursos de Azure](powershell-azure-resource-manager.md).
* toosee tooexport una plantilla mediante la CLI de Azure, vea [Hola Utilice CLI de Azure para Mac, Linux y Windows con el Administrador de recursos de Azure](xplat-cli-azure-resource-manager.md).

