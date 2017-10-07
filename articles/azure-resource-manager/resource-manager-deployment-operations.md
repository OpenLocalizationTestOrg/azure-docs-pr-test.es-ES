---
title: operaciones de aaaDeployment con el Administrador de recursos de Azure | Documentos de Microsoft
description: "Describe cómo las operaciones de implementación de Azure Resource Manager tooview con Hola portal, PowerShell, CLI de Azure y API de REST."
services: azure-resource-manager,virtual-machines
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: infrastructure
ms.date: 01/13/2017
ms.author: tomfitz
ms.openlocfilehash: ba4823ca73caca83dfc07c99d736344ef8b7b54d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="view-deployment-operations-with-azure-resource-manager"></a>Visualización de operaciones de implementación con Azure Resource Manager


Puede ver las operaciones de Hola para una implementación a través de hello portal de Azure. Es posible que más interesado en Ver operaciones de hello cuando haya recibido un error durante la implementación para que este artículo se centra en la visualización de las operaciones que se han producido un error. portal de Hello proporciona una interfaz que permite errores de tooeasily buscar hello y determinar posibles correcciones.

[!INCLUDE [resource-manager-troubleshoot-introduction](../../includes/resource-manager-troubleshoot-introduction.md)]

## <a name="portal"></a>Portal
operaciones de implementación de hello toosee, usar hello pasos:

1. Para el grupo de recursos de hello implicado en la implementación de hello, observe el estado de Hola de última implementación de Hola. Puede seleccionar este estado tooget más detalles.
   
    ![Estado de la implementación](./media/resource-manager-deployment-operations/deployment-status.png)
2. Ver historial de implementación reciente Hola. Seleccione la implementación de Hola que dieron error.
   
    ![Estado de la implementación](./media/resource-manager-deployment-operations/select-deployment.png)
3. Seleccione toosee de vínculo de Hola Hola de una descripción de por qué no se pudo implementar. En la imagen de hello siguiente, registro DNS de hello no es único.  
   
    ![ver la implementación con errores](./media/resource-manager-deployment-operations/view-error.png)
   
    Este mensaje de error debe ser suficiente para la solución de problemas de toobegin. Sin embargo, si necesita más detalles sobre los que se hayan completado las tareas, puede ver las operaciones de hello tal y como se muestra en hello siguiendo los pasos.
4. Puede ver todas las operaciones de implementación de Hola Hola **implementación** hoja. Seleccione cualquier operación toosee más detalles.
   
    ![ver operaciones](./media/resource-manager-deployment-operations/view-operations.png)
   
    En este caso, verá que la cuenta de almacenamiento de hello, red virtual y conjunto de disponibilidad se crearon correctamente. Error de dirección IP pública de Hello y no se han intentado otros recursos.
5. Puede ver los eventos para la implementación de hello seleccionando **eventos**.
   
    ![ver eventos](./media/resource-manager-deployment-operations/view-events.png)
6. Ver todos los eventos de hello para la implementación de Hola y seleccionar uno para obtener más detalles. Tenga en cuenta demasiado Hola identificador de correlación. Este valor puede ser útil cuando se trabaja con el soporte técnico tootroubleshoot una implementación.
   
    ![consultar eventos](./media/resource-manager-deployment-operations/see-all-events.png)

## <a name="powershell"></a>PowerShell
1. tooget Hola estado general de una implementación, use hello **Get AzureRmResourceGroupDeployment** comando. 

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup
  ```

   O bien, puede filtrar los resultados de Hola para solo las implementaciones que se han producido un error.

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup | Where-Object ProvisioningState -eq Failed
  ```
   
2. Cada implementación incluye varias operaciones. Cada operación representa un paso en el proceso de implementación de Hola. toodiscover lo que ha producido un error con una implementación, suele ser preciso toosee detalles acerca de las operaciones de implementación de Hola. Puede ver el estado de Hola de operaciones de hello con **AzureRmResourceGroupDeploymentOperation Get**.

  ```powershell 
  Get-AzureRmResourceGroupDeploymentOperation -ResourceGroupName ExampleGroup -DeploymentName vmDeployment
  ```

    Que devuelve varias operaciones con cada uno de ellos en hello siguiendo el formato:

  ```powershell
  Id             : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.Resources/deployments/Microsoft.Template/operations/A3EB2DA598E0A780
  OperationId    : A3EB2DA598E0A780
  Properties     : @{provisioningOperation=Create; provisioningState=Succeeded; timestamp=2016-06-14T21:55:15.0156208Z;
                   duration=PT23.0227078S; trackingId=11d376e8-5d6d-4da8-847e-6f23c6443fbf;
                   serviceRequestId=0196828d-8559-4bf6-b6b8-8b9057cb0e23; statusCode=OK; targetResource=}
  PropertiesText : {duration:PT23.0227078S, provisioningOperation:Create, provisioningState:Succeeded,
                   serviceRequestId:0196828d-8559-4bf6-b6b8-8b9057cb0e23...}
  ```

3. tooget más detalles sobre las operaciones con errores, recuperar las propiedades de Hola para operaciones con **error** estado.

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object ProvisioningState -eq Failed
  ```
   
    Que devuelve que todos Hola operaciones con errores con cada una de ellas en hello siguiendo el formato:

  ```powershell
  provisioningOperation : Create
  provisioningState     : Failed
  timestamp             : 2016-06-14T21:54:55.1468068Z
  duration              : PT3.1449887S
  trackingId            : f4ed72f8-4203-43dc-958a-15d041e8c233
  serviceRequestId      : a426f689-5d5a-448d-a2f0-9784d14c900a
  statusCode            : BadRequest
  statusMessage         : @{error=}
  targetResource        : @{id=/subscriptions/{guid}/resourceGroups/ExampleGroup/providers/
                          Microsoft.Network/publicIPAddresses/myPublicIP;
                          resourceType=Microsoft.Network/publicIPAddresses; resourceName=myPublicIP}
  ```

    Tenga en cuenta serviceRequestId Hola y Hola ID para la operación de Hola. Hola serviceRequestId puede resultar útil cuando se trabaja con el soporte técnico tootroubleshoot una implementación. Usará ID de hello en hello siguiente paso toofocus en una operación determinada.
4. mensaje de estado de hello tooget de una determinada operación con errores, Hola de uso siguiente comando:

  ```powershell
  ((Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object trackingId -eq f4ed72f8-4203-43dc-958a-15d041e8c233).StatusMessage.error
  ```

    Que devuelve:

  ```powershell
  code           message                                                                        details
  ----           -------                                                                        -------
  DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. {}
  ```
4. Cada operación de implementación en Azure incluye el contenido de la solicitud y de la respuesta. contenido de la solicitud de Hello es lo que se envían tooAzure durante la implementación (por ejemplo, crear una máquina virtual, disco del sistema operativo y otros recursos). contenido de la respuesta de Hello es lo que Azure envía desde la solicitud de implementación. Durante la implementación, puede usar **DeploymentDebugLogLevel** toospecify de parámetro que Hola solicitud o respuesta se conservan en el registro de hello. 

  Obtener esa información de registro de hello y guardar localmente mediante Hola siga los comandos de PowerShell:

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.request | ConvertTo-Json |  Out-File -FilePath <PathToFile>

  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.response | ConvertTo-Json |  Out-File -FilePath <PathToFile>
  ```

## <a name="azure-cli"></a>CLI de Azure

1. Obtener Hola estado general de una implementación con hello **mostrar de la implementación de grupo de azure** comando.

  ```azurecli
  azure group deployment show --resource-group ExampleGroup --name ExampleDeployment --json
  ```
  
  Uno de los valores devuelto de hello es hello **correlationId**. Este valor se utiliza tootrack relacionados con eventos, y puede ser útil al trabajar con tootroubleshoot de soporte técnico de una implementación.

  ```azurecli
  "properties": {
    "provisioningState": "Failed",
    "correlationId": "4002062a-a506-4b5e-aaba-4147036b771a",
  ```

2. operaciones de hello toosee para una implementación, use:

  ```azurecli
  azure group deployment operation list --resource-group ExampleGroup --name ExampleDeployment --json
  ```

## <a name="rest"></a>REST

1. Obtener información acerca de una implementación con hello [obtener información acerca de una implementación de plantilla](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) operación.

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}?api-version={api-version}
  ```

    En la respuesta de hello, tenga en cuenta en particular hello **provisioningState**, **correlationId**, y **error** elementos. Hola **correlationId** se utiliza tootrack relacionados con eventos, y puede ser útil al trabajar con tootroubleshoot de soporte técnico de una implementación.

  ```json
  { 
    ...
    "properties": {
      "provisioningState":"Failed",
      "correlationId":"d5062e45-6e9f-4fd3-a0a0-6b2c56b15757",
      ...
      "error":{
        "code":"DeploymentFailed","message":"At least one resource deployment operation failed. Please list deployment operations for details. Please see http://aka.ms/arm-debug for usage details.",
        "details":[{"code":"Conflict","message":"{\r\n  \"error\": {\r\n    \"message\": \"Conflict\",\r\n    \"code\": \"Conflict\"\r\n  }\r\n}"}]
      }  
    }
  }
  ```

2. Obtener información sobre las operaciones de implementación con hello [enumerar todas las operaciones de implementación de plantilla](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) operación. 

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}/operations?$skiptoken={skiptoken}&api-version={api-version}
  ```
   
    respuesta de Hello incluye información de solicitud o respuesta según lo especificado en hello **debugSetting** propiedad durante la implementación.

  ```json
  {
    ...
    "properties": 
    {
      ...
      "request":{
        "content":{
          "location":"West US",
          "properties":{
            "accountType": "Standard_LRS"
          }
        }
      },
      "response":{
        "content":{
          "error":{
            "message":"Conflict","code":"Conflict"
          }
        }
      }
    }
  }
  ```


## <a name="next-steps"></a>Pasos siguientes
* Para obtener ayuda con la resolución de errores de implementación específicos, consulte [resolver errores comunes al implementar tooAzure de recursos con el Administrador de recursos de Azure](resource-manager-common-deployment-errors.md).
* toolearn sobre el uso de actividad hello registra toomonitor otros tipos de acciones, vea [toomanage Azure de registros de actividad de la vista recursos](resource-group-audit.md).
* toovalidate la implementación antes de ejecutarlo, consulte [implementar un grupo de recursos con la plantilla de Azure Resource Manager](resource-group-template-deploy.md).

