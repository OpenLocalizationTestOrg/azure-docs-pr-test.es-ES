---
title: "errores de implementación de Azure aaaUnderstand | Documentos de Microsoft"
description: "Describe cómo toolearn sobre los errores de implementación de Azure."
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "error de implementación, implementación de azure, implementar tooazure"
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: tomfitz
ms.openlocfilehash: a335e121e9b908a763374907e34b1f6e823d6e96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-deployment-errors"></a>Información sobre los errores de implementación de Azure
En este tema se describen los errores de implementación y cómo obtener más información sobre un error. Para errores de implementación de las soluciones toocommon, vea [solucionar errores comunes de implementación de Azure con el Administrador de recursos de Azure](resource-manager-common-deployment-errors.md).

## <a name="two-types-of-errors"></a>Dos tipos de errores
Hay dos tipos de errores que puede recibir:

* Errores de validación
* Errores de implementación

Hola después de la imagen muestra el registro de actividad de Hola para una suscripción. Representa dos implementaciones. En la misma implementación, plantilla de hello, no pudo validar (**validar**) y no. En Hola otra implementación, plantilla Hola pasó la validación pero no se pudo al crear recursos de hello (**escribir implementaciones**). 

![Visualización del código de error](./media/resource-manager-troubleshoot-tips/show-activity-log.png)

Los errores de validación que provienen de escenarios que se pueden determinar antes de la implementación Incluyen errores de sintaxis en la plantilla o tratar de recursos de toodeploy que se superen las cuotas de suscripción. Errores de implementación provengan de condiciones que se producen durante el proceso de implementación de Hola. Incluyen intentar tooaccess un recurso que se va a implementar en paralelo.

Ambos tipos de errores devuelve un código de error que utiliza la implementación de hello tootroubleshoot. Ambos tipos de errores aparecen en hello [registro de actividad](resource-group-audit.md). Sin embargo, los errores de validación no aparecen en el historial de implementación porque se ha iniciado nunca implementación Hola.

## <a name="determine-error-code"></a>Determinación del código de error

Puede obtener información acerca de un error, mire el mensaje de error de Hola y código de error de Hola. Hola [solucionar errores comunes de implementación de Azure con el Administrador de recursos de Azure](resource-manager-common-deployment-errors.md) artículo enumeran las soluciones por código de error. Este tema muestra cómo toouse Hola código de error de hello toodiscover de portal de Azure.

### <a name="validation-errors"></a>Errores de validación

Cuando se implementa a través del portal de hello, verá un error de validación después de enviar sus valores.

![vista del error de validación en el portal](./media/resource-manager-troubleshoot-tips/validation-error.png)

Seleccione el mensaje de Hola para obtener más detalles. Hola después de la imagen, verá un **InvalidTemplateDeployment** error y un mensaje que indica que una directiva esté bloqueado implementación.

![vista de los detalles de validación](./media/resource-manager-troubleshoot-tips/validation-details.png)

### <a name="deployment-errors"></a>Errores de implementación

Cuando la operación de hello pasa la validación, pero se produce un error durante la implementación, consulte error hello en las notificaciones de Hola. Seleccione la notificación de Hola.

![notificación de error](./media/resource-manager-troubleshoot-tips/notification.png)

Consulte más detalles acerca de la implementación de Hola. Seleccione Hola opción toofind obtener más información sobre el error de Hola.

![error de implementación](./media/resource-manager-troubleshoot-tips/deployment-failed.png)

Consulte códigos de error y de mensaje de error de Hola. Observe que hay dos códigos de error. Hola primer código de error (**implementación**) es un error general que no proporciona detalles hello tiene errores de hello toosolve. Hola segundo código de error (**StorageAccountNotFound**) proporciona detalles de Hola que necesita. 

![detalles del error](./media/resource-manager-troubleshoot-tips/error-details.png)

## <a name="enable-debug-logging"></a>Habilitación del registro de depuración
En ciertas ocasiones necesitará obtener más información sobre toodiscover de solicitud y respuesta de hello qué salió mal. Mediante el uso de PowerShell o la CLI de Azure, puede solicitar que se registre información adicional durante la implementación.

- PowerShell

   En PowerShell, establezca hello **DeploymentDebugLogLevel** parámetro tooAll, ResponseContent o RequestContent.

  ```powershell
  New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile c:\Azure\Templates\storage.json -DeploymentDebugLogLevel All
  ```

   Examine el contenido de la solicitud de hello con hello siguiente cmdlet:

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.request | ConvertTo-Json
  ```

   O bien, Hola respuesta contenida con:

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.response | ConvertTo-Json
  ```

   Esta información puede ayudarle a determinar si un valor en la plantilla de Hola se establece incorrectamente.

- CLI de Azure

   Examine las operaciones de implementación de hello con hello siguiente comando:

  ```azurecli
  az group deployment operation list --resource-group ExampleGroup --name vmlinux
  ```

- Plantilla anidada

   toolog información de depuración para una plantilla anidada, use hello **debugSetting** elemento.

  ```json
  {
      "apiVersion": "2016-09-01",
      "name": "nestedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
          "mode": "Incremental",
          "templateLink": {
              "uri": "{template-uri}",
              "contentVersion": "1.0.0.0"
          },
          "debugSetting": {
             "detailLevel": "requestContent, responseContent"
          }
      }
  }
  ```


## <a name="create-a-troubleshooting-template"></a>Creación de una plantilla de solución de problemas
En algunos casos, Hola tootroubleshoot de manera más fácil la plantilla es tootest partes de él. Puede crear una plantilla simplificada que le permite toofocus por parte de Hola que cree que está provocando el error de Hola. Por ejemplo, supongamos que se recibe un error al hacer referencia a un recurso. En lugar de tratar directamente con una plantilla de toda, crear una plantilla que devuelve parte de Hola que puedan estar causando el problema. Puede ayudarle a determinar si se pasa en parámetros correctos de hello, mediante las funciones de plantilla correctamente, y obtener recursos de Hola que espera.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageName": {
        "type": "string"
    },
    "storageResourceGroup": {
        "type": "string"
    }
  },
  "variables": {},
  "resources": [],
  "outputs": {
    "exampleOutput": {
        "value": "[reference(resourceId(parameters('storageResourceGroup'), 'Microsoft.Storage/storageAccounts', parameters('storageName')), '2016-05-01')]",
        "type" : "object"
    }
  }
}
```

O bien, supongamos que se están produciendo errores de implementación que cree que están relacionados con tooincorrectly establezca las dependencias. Pruebe la plantilla dividiéndola en plantillas simplificadas. En primer lugar, cree una plantilla que implemente solo un único recurso (por ejemplo, un servidor SQL Server). Cuando esté seguro de que tiene dicho recurso definido correctamente, agregue un recurso que dependa de él (por ejemplo, una base de datos SQL). Cuando esos dos recursos se definan correctamente, agregue otros recursos dependientes (por ejemplo, las directivas de auditoría). Entre cada implementación de prueba, elimine Hola recursos toomake seguro de prueba adecuadamente hello las dependencias del grupo. 

## <a name="check-deployment-sequence"></a>Comprobación de la secuencia de implementación

Muchos errores de implementación se producen cuando los recursos se implementan en una secuencia inesperada. Estos errores se producen cuando las dependencias no se han establecido correctamente. Cuando falta una dependencia necesaria, un recurso intenta toouse que aún no existe ningún valor para otro recurso pero Hola otro. Recibirá un error que indica que no se encuentra el recurso. Puede encontrar este tipo de error de forma intermitente porque el tiempo de implementación de Hola para cada recurso puede variar. Por ejemplo, la primera toodeploy de intento de los recursos se realiza correctamente debido a un recurso necesario aleatoriamente finaliza en el tiempo. Sin embargo, se produce un error en el segundo intento porque Hola requiere recursos no se completó en el tiempo. 

Sin embargo, desea tooavoid configurar las dependencias que no son necesarios. Cuando hay dependencias innecesarias, prolongar la duración de Hola de implementación de hello al impedir que los recursos que no son dependientes entre sí se implementen en paralelo. Además, puede crear dependencias circulares que bloquean la implementación de Hola. Hola [referencia](resource-group-template-functions-resource.md#reference) función crea una dependencia implícita en el recurso de hello al que hace referencia, cuando ese recurso se implementa en hello misma plantilla. Por lo tanto, puede tener más dependencias de las dependencias de hello especificadas en hello **dependsOn** propiedad. Hola [resourceId](resource-group-template-functions-resource.md#resourceid) función no crea una dependencia implícita ni validar la existencia de recursos de Hola.

Cuando se encuentran problemas de dependencia, necesita una visión general de toogain en orden de Hola de implementación de los recursos. orden de hello tooview de las operaciones de implementación:

1. Seleccione el historial de implementación de hello para el grupo de recursos.

   ![seleccionar el historial de implementaciones](./media/resource-manager-troubleshoot-tips/select-deployment.png)

2. Seleccione una implementación de historial de Hola y seleccione **eventos**.

   ![seleccionar eventos de implementación](./media/resource-manager-troubleshoot-tips/select-deployment-events.png)

3. Examine la secuencia de Hola de eventos para cada recurso. Estado de toohello de atención de cada operación del pago. Por ejemplo, hello siguiente imagen muestra tres cuentas de almacenamiento que se implementan en paralelo. Tenga en cuenta que Hola tres cuentas de almacenamiento se inician en hello mismo tiempo.

   ![implementación paralela](./media/resource-manager-troubleshoot-tips/deployment-events-parallel.png)

   imagen de Hello siguiente muestra tres cuentas de almacenamiento que no se implementan en paralelo. cuenta de almacenamiento segundo Hola depende de la primera cuenta de almacenamiento hello y depende de la cuenta de almacenamiento de terceros de Hola Hola segunda cuenta de almacenamiento. Por lo tanto, primera cuenta de almacenamiento Hola se inicia, acepta y completar antes de que se inicia Hola junto.

   ![implementación secuencial](./media/resource-manager-troubleshoot-tips/deployment-events-sequence.png)

Incluso para los escenarios más complicados, puede usar Hola mismo toodiscover técnica cuando la implementación se inicia y se completa para cada recurso. Examine la toosee de eventos de implementación si la secuencia de hello es diferente que se esperaría. Si es así, vuelva a evaluar las dependencias de Hola para este recurso.

Resource Manager identifica dependencias circulares durante la validación de plantillas. y devuelve un mensaje de error que indica específicamente que existe una dependencia circular. toosolve una dependencia circular:

1. En la plantilla, encuentra el recurso de hello identificada una dependencia circular Hola. 
2. Para ese recurso, examine hello **dependsOn** propiedad y todos los usos de hello **referencia** toosee qué recursos depende de función. 
3. Examine los toosee de recursos los recursos que dependen. Siga las dependencias de hello hasta que observe un recurso que depende del recurso de hello original.
5. Para obtener recursos Hola implicados en una dependencia circular hello, examine con cuidado todos los usos de hello **dependsOn** propiedad tooidentify todas las dependencias que no son necesarios. Quite esas dependencias. Si no está seguro de si una dependencia es necesaria, pruebe a quitarla. 
6. Volver a implementar la plantilla de Hola.

Cómo quitar valores de hello **dependsOn** propiedad puede producir errores cuando se implementa plantilla Hola. Si se produce un error, agregue la dependencia de hello en plantilla Hola. 

Si este enfoque no soluciona una dependencia circular hello, considere la posibilidad de mover parte de la lógica de implementación a recursos secundarios (por ejemplo, extensiones o valores de configuración). Configurar los toodeploy de recursos secundarios después de recursos de hello implicados en una dependencia circular Hola. Por ejemplo, suponga que va a implementar dos máquinas virtuales pero debe establecer las propiedades en cada uno de ellos que hacen referencia toohello otro. Puede implementarlos en hello siguiente orden:

1. vm1
2. vm2
3. La extensión en vm1 depende de vm1 y vm2. extensión de Hello establece valores en vm1 que obtiene de vm2.
4. La extensión en vm2 depende de vm1 y vm2. extensión de Hello establece valores en vm2 que obtiene de vm1.

Hola mismo enfoque funciona para las aplicaciones de servicio de aplicaciones. Considere la posibilidad de mover los valores de configuración a un recurso secundario del recurso de aplicación Hola. Puede implementar dos aplicaciones web en hello siguiente orden:

1. webapp1
2. webapp2
3. La configuración de webapp1 depende de webapp1 y webapp2. Contiene la configuración de aplicación con valores de webapp2.
4. La configuración de webapp2 depende de webapp1 y webapp2. Contiene la configuración de aplicación con valores de webapp1.


## <a name="next-steps"></a>Pasos siguientes
* Para errores de implementación de las soluciones toocommon, vea [solucionar errores comunes de implementación de Azure con el Administrador de recursos de Azure](resource-manager-common-deployment-errors.md).
* toolearn acerca de la auditoría de acciones, vea [auditoría de las operaciones con el Administrador de recursos](resource-group-audit.md).
* toolearn acerca de los errores de hello toodetermine de acciones durante la implementación, consulte [ver las operaciones de implementación](resource-manager-deployment-operations.md).
