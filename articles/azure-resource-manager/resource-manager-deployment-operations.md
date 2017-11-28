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
# <a name="view-deployment-operations-with-azure-resource-manager"></a><span data-ttu-id="93e0c-103">Visualización de operaciones de implementación con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="93e0c-103">View deployment operations with Azure Resource Manager</span></span>


<span data-ttu-id="93e0c-104">Puede ver las operaciones de Hola para una implementación a través de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="93e0c-104">You can view hello operations for a deployment through hello Azure portal.</span></span> <span data-ttu-id="93e0c-105">Es posible que más interesado en Ver operaciones de hello cuando haya recibido un error durante la implementación para que este artículo se centra en la visualización de las operaciones que se han producido un error.</span><span class="sxs-lookup"><span data-stu-id="93e0c-105">You may be most interested in viewing hello operations when you have received an error during deployment so this article focuses on viewing operations that have failed.</span></span> <span data-ttu-id="93e0c-106">portal de Hello proporciona una interfaz que permite errores de tooeasily buscar hello y determinar posibles correcciones.</span><span class="sxs-lookup"><span data-stu-id="93e0c-106">hello portal provides an interface that enables you tooeasily find hello errors and determine potential fixes.</span></span>

[!INCLUDE [resource-manager-troubleshoot-introduction](../../includes/resource-manager-troubleshoot-introduction.md)]

## <a name="portal"></a><span data-ttu-id="93e0c-107">Portal</span><span class="sxs-lookup"><span data-stu-id="93e0c-107">Portal</span></span>
<span data-ttu-id="93e0c-108">operaciones de implementación de hello toosee, usar hello pasos:</span><span class="sxs-lookup"><span data-stu-id="93e0c-108">toosee hello deployment operations, use hello following steps:</span></span>

1. <span data-ttu-id="93e0c-109">Para el grupo de recursos de hello implicado en la implementación de hello, observe el estado de Hola de última implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="93e0c-109">For hello resource group involved in hello deployment, notice hello status of hello last deployment.</span></span> <span data-ttu-id="93e0c-110">Puede seleccionar este estado tooget más detalles.</span><span class="sxs-lookup"><span data-stu-id="93e0c-110">You can select this status tooget more details.</span></span>
   
    ![Estado de la implementación](./media/resource-manager-deployment-operations/deployment-status.png)
2. <span data-ttu-id="93e0c-112">Ver historial de implementación reciente Hola.</span><span class="sxs-lookup"><span data-stu-id="93e0c-112">You see hello recent deployment history.</span></span> <span data-ttu-id="93e0c-113">Seleccione la implementación de Hola que dieron error.</span><span class="sxs-lookup"><span data-stu-id="93e0c-113">Select hello deployment that failed.</span></span>
   
    ![Estado de la implementación](./media/resource-manager-deployment-operations/select-deployment.png)
3. <span data-ttu-id="93e0c-115">Seleccione toosee de vínculo de Hola Hola de una descripción de por qué no se pudo implementar.</span><span class="sxs-lookup"><span data-stu-id="93e0c-115">Select hello link toosee a description of why hello deployment failed.</span></span> <span data-ttu-id="93e0c-116">En la imagen de hello siguiente, registro DNS de hello no es único.</span><span class="sxs-lookup"><span data-stu-id="93e0c-116">In hello image below, hello DNS record is not unique.</span></span>  
   
    ![ver la implementación con errores](./media/resource-manager-deployment-operations/view-error.png)
   
    <span data-ttu-id="93e0c-118">Este mensaje de error debe ser suficiente para la solución de problemas de toobegin.</span><span class="sxs-lookup"><span data-stu-id="93e0c-118">This error message should be enough for you toobegin troubleshooting.</span></span> <span data-ttu-id="93e0c-119">Sin embargo, si necesita más detalles sobre los que se hayan completado las tareas, puede ver las operaciones de hello tal y como se muestra en hello siguiendo los pasos.</span><span class="sxs-lookup"><span data-stu-id="93e0c-119">However, if you need more details about which tasks were completed, you can view hello operations as shown in hello following steps.</span></span>
4. <span data-ttu-id="93e0c-120">Puede ver todas las operaciones de implementación de Hola Hola **implementación** hoja.</span><span class="sxs-lookup"><span data-stu-id="93e0c-120">You can view all hello deployment operations in hello **Deployment** blade.</span></span> <span data-ttu-id="93e0c-121">Seleccione cualquier operación toosee más detalles.</span><span class="sxs-lookup"><span data-stu-id="93e0c-121">Select any operation toosee more details.</span></span>
   
    ![ver operaciones](./media/resource-manager-deployment-operations/view-operations.png)
   
    <span data-ttu-id="93e0c-123">En este caso, verá que la cuenta de almacenamiento de hello, red virtual y conjunto de disponibilidad se crearon correctamente.</span><span class="sxs-lookup"><span data-stu-id="93e0c-123">In this case, you see that hello storage account, virtual network, and availability set were successfully created.</span></span> <span data-ttu-id="93e0c-124">Error de dirección IP pública de Hello y no se han intentado otros recursos.</span><span class="sxs-lookup"><span data-stu-id="93e0c-124">hello public IP address failed, and other resources were not attempted.</span></span>
5. <span data-ttu-id="93e0c-125">Puede ver los eventos para la implementación de hello seleccionando **eventos**.</span><span class="sxs-lookup"><span data-stu-id="93e0c-125">You can view events for hello deployment by selecting **Events**.</span></span>
   
    ![ver eventos](./media/resource-manager-deployment-operations/view-events.png)
6. <span data-ttu-id="93e0c-127">Ver todos los eventos de hello para la implementación de Hola y seleccionar uno para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="93e0c-127">You see all hello events for hello deployment and select any one for more details.</span></span> <span data-ttu-id="93e0c-128">Tenga en cuenta demasiado Hola identificador de correlación.</span><span class="sxs-lookup"><span data-stu-id="93e0c-128">Notice too hello correlation IDs.</span></span> <span data-ttu-id="93e0c-129">Este valor puede ser útil cuando se trabaja con el soporte técnico tootroubleshoot una implementación.</span><span class="sxs-lookup"><span data-stu-id="93e0c-129">This value can be helpful when working with technical support tootroubleshoot a deployment.</span></span>
   
    ![consultar eventos](./media/resource-manager-deployment-operations/see-all-events.png)

## <a name="powershell"></a><span data-ttu-id="93e0c-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="93e0c-131">PowerShell</span></span>
1. <span data-ttu-id="93e0c-132">tooget Hola estado general de una implementación, use hello **Get AzureRmResourceGroupDeployment** comando.</span><span class="sxs-lookup"><span data-stu-id="93e0c-132">tooget hello overall status of a deployment, use hello **Get-AzureRmResourceGroupDeployment** command.</span></span> 

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup
  ```

   <span data-ttu-id="93e0c-133">O bien, puede filtrar los resultados de Hola para solo las implementaciones que se han producido un error.</span><span class="sxs-lookup"><span data-stu-id="93e0c-133">Or, you can filter hello results for only those deployments that have failed.</span></span>

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup | Where-Object ProvisioningState -eq Failed
  ```
   
2. <span data-ttu-id="93e0c-134">Cada implementación incluye varias operaciones.</span><span class="sxs-lookup"><span data-stu-id="93e0c-134">Each deployment includes multiple operations.</span></span> <span data-ttu-id="93e0c-135">Cada operación representa un paso en el proceso de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="93e0c-135">Each operation represents a step in hello deployment process.</span></span> <span data-ttu-id="93e0c-136">toodiscover lo que ha producido un error con una implementación, suele ser preciso toosee detalles acerca de las operaciones de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="93e0c-136">toodiscover what went wrong with a deployment, you usually need toosee details about hello deployment operations.</span></span> <span data-ttu-id="93e0c-137">Puede ver el estado de Hola de operaciones de hello con **AzureRmResourceGroupDeploymentOperation Get**.</span><span class="sxs-lookup"><span data-stu-id="93e0c-137">You can see hello status of hello operations with **Get-AzureRmResourceGroupDeploymentOperation**.</span></span>

  ```powershell 
  Get-AzureRmResourceGroupDeploymentOperation -ResourceGroupName ExampleGroup -DeploymentName vmDeployment
  ```

    <span data-ttu-id="93e0c-138">Que devuelve varias operaciones con cada uno de ellos en hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="93e0c-138">Which returns multiple operations with each one in hello following format:</span></span>

  ```powershell
  Id             : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.Resources/deployments/Microsoft.Template/operations/A3EB2DA598E0A780
  OperationId    : A3EB2DA598E0A780
  Properties     : @{provisioningOperation=Create; provisioningState=Succeeded; timestamp=2016-06-14T21:55:15.0156208Z;
                   duration=PT23.0227078S; trackingId=11d376e8-5d6d-4da8-847e-6f23c6443fbf;
                   serviceRequestId=0196828d-8559-4bf6-b6b8-8b9057cb0e23; statusCode=OK; targetResource=}
  PropertiesText : {duration:PT23.0227078S, provisioningOperation:Create, provisioningState:Succeeded,
                   serviceRequestId:0196828d-8559-4bf6-b6b8-8b9057cb0e23...}
  ```

3. <span data-ttu-id="93e0c-139">tooget más detalles sobre las operaciones con errores, recuperar las propiedades de Hola para operaciones con **error** estado.</span><span class="sxs-lookup"><span data-stu-id="93e0c-139">tooget more details about failed operations, retrieve hello properties for operations with **Failed** state.</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object ProvisioningState -eq Failed
  ```
   
    <span data-ttu-id="93e0c-140">Que devuelve que todos Hola operaciones con errores con cada una de ellas en hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="93e0c-140">Which returns all hello failed operations with each one in hello following format:</span></span>

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

    <span data-ttu-id="93e0c-141">Tenga en cuenta serviceRequestId Hola y Hola ID para la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="93e0c-141">Note hello serviceRequestId and hello trackingId for hello operation.</span></span> <span data-ttu-id="93e0c-142">Hola serviceRequestId puede resultar útil cuando se trabaja con el soporte técnico tootroubleshoot una implementación.</span><span class="sxs-lookup"><span data-stu-id="93e0c-142">hello serviceRequestId can be helpful when working with technical support tootroubleshoot a deployment.</span></span> <span data-ttu-id="93e0c-143">Usará ID de hello en hello siguiente paso toofocus en una operación determinada.</span><span class="sxs-lookup"><span data-stu-id="93e0c-143">You will use hello trackingId in hello next step toofocus on a particular operation.</span></span>
4. <span data-ttu-id="93e0c-144">mensaje de estado de hello tooget de una determinada operación con errores, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="93e0c-144">tooget hello status message of a particular failed operation, use hello following command:</span></span>

  ```powershell
  ((Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object trackingId -eq f4ed72f8-4203-43dc-958a-15d041e8c233).StatusMessage.error
  ```

    <span data-ttu-id="93e0c-145">Que devuelve:</span><span class="sxs-lookup"><span data-stu-id="93e0c-145">Which returns:</span></span>

  ```powershell
  code           message                                                                        details
  ----           -------                                                                        -------
  DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. {}
  ```
4. <span data-ttu-id="93e0c-146">Cada operación de implementación en Azure incluye el contenido de la solicitud y de la respuesta.</span><span class="sxs-lookup"><span data-stu-id="93e0c-146">Every deployment operation in Azure includes request and response content.</span></span> <span data-ttu-id="93e0c-147">contenido de la solicitud de Hello es lo que se envían tooAzure durante la implementación (por ejemplo, crear una máquina virtual, disco del sistema operativo y otros recursos).</span><span class="sxs-lookup"><span data-stu-id="93e0c-147">hello request content is what you sent tooAzure during deployment (for example, create a VM, OS disk, and other resources).</span></span> <span data-ttu-id="93e0c-148">contenido de la respuesta de Hello es lo que Azure envía desde la solicitud de implementación.</span><span class="sxs-lookup"><span data-stu-id="93e0c-148">hello response content is what Azure sent back from your deployment request.</span></span> <span data-ttu-id="93e0c-149">Durante la implementación, puede usar **DeploymentDebugLogLevel** toospecify de parámetro que Hola solicitud o respuesta se conservan en el registro de hello.</span><span class="sxs-lookup"><span data-stu-id="93e0c-149">During deployment, you can use **DeploymentDebugLogLevel** paramenter toospecify that hello request and/or response are retained in hello log.</span></span> 

  <span data-ttu-id="93e0c-150">Obtener esa información de registro de hello y guardar localmente mediante Hola siga los comandos de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="93e0c-150">You get that information from hello log, and save it locally by using hello following PowerShell commands:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.request | ConvertTo-Json |  Out-File -FilePath <PathToFile>

  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.response | ConvertTo-Json |  Out-File -FilePath <PathToFile>
  ```

## <a name="azure-cli"></a><span data-ttu-id="93e0c-151">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="93e0c-151">Azure CLI</span></span>

1. <span data-ttu-id="93e0c-152">Obtener Hola estado general de una implementación con hello **mostrar de la implementación de grupo de azure** comando.</span><span class="sxs-lookup"><span data-stu-id="93e0c-152">Get hello overall status of a deployment with hello **azure group deployment show** command.</span></span>

  ```azurecli
  azure group deployment show --resource-group ExampleGroup --name ExampleDeployment --json
  ```
  
  <span data-ttu-id="93e0c-153">Uno de los valores devuelto de hello es hello **correlationId**.</span><span class="sxs-lookup"><span data-stu-id="93e0c-153">One of hello returned values is hello **correlationId**.</span></span> <span data-ttu-id="93e0c-154">Este valor se utiliza tootrack relacionados con eventos, y puede ser útil al trabajar con tootroubleshoot de soporte técnico de una implementación.</span><span class="sxs-lookup"><span data-stu-id="93e0c-154">This value is used tootrack related events, and can be helpful when working with technical support tootroubleshoot a deployment.</span></span>

  ```azurecli
  "properties": {
    "provisioningState": "Failed",
    "correlationId": "4002062a-a506-4b5e-aaba-4147036b771a",
  ```

2. <span data-ttu-id="93e0c-155">operaciones de hello toosee para una implementación, use:</span><span class="sxs-lookup"><span data-stu-id="93e0c-155">toosee hello operations for a deployment, use:</span></span>

  ```azurecli
  azure group deployment operation list --resource-group ExampleGroup --name ExampleDeployment --json
  ```

## <a name="rest"></a><span data-ttu-id="93e0c-156">REST</span><span class="sxs-lookup"><span data-stu-id="93e0c-156">REST</span></span>

1. <span data-ttu-id="93e0c-157">Obtener información acerca de una implementación con hello [obtener información acerca de una implementación de plantilla](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) operación.</span><span class="sxs-lookup"><span data-stu-id="93e0c-157">Get information about a deployment with hello [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) operation.</span></span>

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}?api-version={api-version}
  ```

    <span data-ttu-id="93e0c-158">En la respuesta de hello, tenga en cuenta en particular hello **provisioningState**, **correlationId**, y **error** elementos.</span><span class="sxs-lookup"><span data-stu-id="93e0c-158">In hello response, note in particular hello **provisioningState**, **correlationId**, and **error** elements.</span></span> <span data-ttu-id="93e0c-159">Hola **correlationId** se utiliza tootrack relacionados con eventos, y puede ser útil al trabajar con tootroubleshoot de soporte técnico de una implementación.</span><span class="sxs-lookup"><span data-stu-id="93e0c-159">hello **correlationId** is used tootrack related events, and can be helpful when working with technical support tootroubleshoot a deployment.</span></span>

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

2. <span data-ttu-id="93e0c-160">Obtener información sobre las operaciones de implementación con hello [enumerar todas las operaciones de implementación de plantilla](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) operación.</span><span class="sxs-lookup"><span data-stu-id="93e0c-160">Get information about deployment operations with hello [List all template deployment operations](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) operation.</span></span> 

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}/operations?$skiptoken={skiptoken}&api-version={api-version}
  ```
   
    <span data-ttu-id="93e0c-161">respuesta de Hello incluye información de solicitud o respuesta según lo especificado en hello **debugSetting** propiedad durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="93e0c-161">hello response includes request and/or response information based on what you specified in hello **debugSetting** property during deployment.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="93e0c-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="93e0c-162">Next steps</span></span>
* <span data-ttu-id="93e0c-163">Para obtener ayuda con la resolución de errores de implementación específicos, consulte [resolver errores comunes al implementar tooAzure de recursos con el Administrador de recursos de Azure](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="93e0c-163">For help with resolving particular deployment errors, see [Resolve common errors when deploying resources tooAzure with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="93e0c-164">toolearn sobre el uso de actividad hello registra toomonitor otros tipos de acciones, vea [toomanage Azure de registros de actividad de la vista recursos](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="93e0c-164">toolearn about using hello activity logs toomonitor other types of actions, see [View activity logs toomanage Azure resources](resource-group-audit.md).</span></span>
* <span data-ttu-id="93e0c-165">toovalidate la implementación antes de ejecutarlo, consulte [implementar un grupo de recursos con la plantilla de Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="93e0c-165">toovalidate your deployment before executing it, see [Deploy a resource group with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

