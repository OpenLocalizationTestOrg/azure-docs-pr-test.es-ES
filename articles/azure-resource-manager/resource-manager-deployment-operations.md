---
title: "Operaciones de implementación con Azure Resource Manager | Microsoft Docs"
description: "Se describe cómo ver las operaciones de implementación de Azure Resource Manager con el portal, PowerShell, CLI de Azure y API de REST."
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
ms.openlocfilehash: fb6b3b357fd1f66184e480115a9c863ba31ac193
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="view-deployment-operations-with-azure-resource-manager"></a><span data-ttu-id="79ae3-103">Visualización de operaciones de implementación con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="79ae3-103">View deployment operations with Azure Resource Manager</span></span>


<span data-ttu-id="79ae3-104">Puede ver las operaciones de una implementación mediante el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="79ae3-104">You can view the operations for a deployment through the Azure portal.</span></span> <span data-ttu-id="79ae3-105">Es posible que le resulte más interesante ver las operaciones si ha recibido un error durante la implementación; por ello, este artículo se centrará en la visualización de las operaciones en las que se han producido errores.</span><span class="sxs-lookup"><span data-stu-id="79ae3-105">You may be most interested in viewing the operations when you have received an error during deployment so this article focuses on viewing operations that have failed.</span></span> <span data-ttu-id="79ae3-106">El portal proporciona una interfaz que permite buscar los errores y determinar posibles correcciones con facilidad.</span><span class="sxs-lookup"><span data-stu-id="79ae3-106">The portal provides an interface that enables you to easily find the errors and determine potential fixes.</span></span>

[!INCLUDE [resource-manager-troubleshoot-introduction](../../includes/resource-manager-troubleshoot-introduction.md)]

## <a name="portal"></a><span data-ttu-id="79ae3-107">Portal</span><span class="sxs-lookup"><span data-stu-id="79ae3-107">Portal</span></span>
<span data-ttu-id="79ae3-108">Para ver las operaciones de implementación, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="79ae3-108">To see the deployment operations, use the following steps:</span></span>

1. <span data-ttu-id="79ae3-109">En el grupo de recursos implicado en la implementación, examine el estado de la última implementación.</span><span class="sxs-lookup"><span data-stu-id="79ae3-109">For the resource group involved in the deployment, notice the status of the last deployment.</span></span> <span data-ttu-id="79ae3-110">Puede seleccionar este estado para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="79ae3-110">You can select this status to get more details.</span></span>
   
    ![Estado de la implementación](./media/resource-manager-deployment-operations/deployment-status.png)
2. <span data-ttu-id="79ae3-112">Ve el historial de implementación reciente.</span><span class="sxs-lookup"><span data-stu-id="79ae3-112">You see the recent deployment history.</span></span> <span data-ttu-id="79ae3-113">Seleccione la implementación en la que se produjo un error.</span><span class="sxs-lookup"><span data-stu-id="79ae3-113">Select the deployment that failed.</span></span>
   
    ![Estado de la implementación](./media/resource-manager-deployment-operations/select-deployment.png)
3. <span data-ttu-id="79ae3-115">Seleccione el vínculo para ver una descripción del motivo del error de la implementación.</span><span class="sxs-lookup"><span data-stu-id="79ae3-115">Select the link to see a description of why the deployment failed.</span></span> <span data-ttu-id="79ae3-116">En la imagen siguiente, el registro de DNS no es único.</span><span class="sxs-lookup"><span data-stu-id="79ae3-116">In the image below, the DNS record is not unique.</span></span>  
   
    ![ver la implementación con errores](./media/resource-manager-deployment-operations/view-error.png)
   
    <span data-ttu-id="79ae3-118">Este mensaje de error debería ser suficiente para que comience la solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="79ae3-118">This error message should be enough for you to begin troubleshooting.</span></span> <span data-ttu-id="79ae3-119">Sin embargo, si necesita más detalles acerca de las tareas que se han completado, puede ver las operaciones como se muestra en los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="79ae3-119">However, if you need more details about which tasks were completed, you can view the operations as shown in the following steps.</span></span>
4. <span data-ttu-id="79ae3-120">Puede ver todas las operaciones de implementación en la hoja **Implementación** .</span><span class="sxs-lookup"><span data-stu-id="79ae3-120">You can view all the deployment operations in the **Deployment** blade.</span></span> <span data-ttu-id="79ae3-121">Seleccione la operación que desea ver con mayor detalle.</span><span class="sxs-lookup"><span data-stu-id="79ae3-121">Select any operation to see more details.</span></span>
   
    ![ver operaciones](./media/resource-manager-deployment-operations/view-operations.png)
   
    <span data-ttu-id="79ae3-123">En este caso, puede ver que la cuenta de almacenamiento, la red virtual y el conjunto de disponibilidad se crearon correctamente.</span><span class="sxs-lookup"><span data-stu-id="79ae3-123">In this case, you see that the storage account, virtual network, and availability set were successfully created.</span></span> <span data-ttu-id="79ae3-124">Se produjo un error en la dirección IP pública y no se han intentado otros recursos.</span><span class="sxs-lookup"><span data-stu-id="79ae3-124">The public IP address failed, and other resources were not attempted.</span></span>
5. <span data-ttu-id="79ae3-125">Puede ver los eventos de la implementación seleccionando **Eventos**.</span><span class="sxs-lookup"><span data-stu-id="79ae3-125">You can view events for the deployment by selecting **Events**.</span></span>
   
    ![ver eventos](./media/resource-manager-deployment-operations/view-events.png)
6. <span data-ttu-id="79ae3-127">Puede ver todos los eventos de la implementación y seleccionar cualquiera de ellos para más información.</span><span class="sxs-lookup"><span data-stu-id="79ae3-127">You see all the events for the deployment and select any one for more details.</span></span> <span data-ttu-id="79ae3-128">Observe también los identificadores de correlación.</span><span class="sxs-lookup"><span data-stu-id="79ae3-128">Notice too the correlation IDs.</span></span> <span data-ttu-id="79ae3-129">Este valor puede resultar útil al trabajar con el soporte técnico para solucionar un problema de implementación.</span><span class="sxs-lookup"><span data-stu-id="79ae3-129">This value can be helpful when working with technical support to troubleshoot a deployment.</span></span>
   
    ![consultar eventos](./media/resource-manager-deployment-operations/see-all-events.png)

## <a name="powershell"></a><span data-ttu-id="79ae3-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="79ae3-131">PowerShell</span></span>
1. <span data-ttu-id="79ae3-132">Para obtener el estado general de una implementación, use el comando **Get-AzureRmResourceGroupDeployment** .</span><span class="sxs-lookup"><span data-stu-id="79ae3-132">To get the overall status of a deployment, use the **Get-AzureRmResourceGroupDeployment** command.</span></span> 

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup
  ```

   <span data-ttu-id="79ae3-133">O bien, puede filtrar los resultados para obtener únicamente las implementaciones en las que se han producido errores.</span><span class="sxs-lookup"><span data-stu-id="79ae3-133">Or, you can filter the results for only those deployments that have failed.</span></span>

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup | Where-Object ProvisioningState -eq Failed
  ```
   
2. <span data-ttu-id="79ae3-134">Cada implementación incluye varias operaciones.</span><span class="sxs-lookup"><span data-stu-id="79ae3-134">Each deployment includes multiple operations.</span></span> <span data-ttu-id="79ae3-135">Cada operación representa un paso del proceso de implementación.</span><span class="sxs-lookup"><span data-stu-id="79ae3-135">Each operation represents a step in the deployment process.</span></span> <span data-ttu-id="79ae3-136">Para detectar qué salió mal con una implementación, normalmente es necesario ver los detalles de las operaciones de implementación.</span><span class="sxs-lookup"><span data-stu-id="79ae3-136">To discover what went wrong with a deployment, you usually need to see details about the deployment operations.</span></span> <span data-ttu-id="79ae3-137">Puede ver el estado de las operaciones con **Get-AzureRmResourceGroupDeploymentOperation**.</span><span class="sxs-lookup"><span data-stu-id="79ae3-137">You can see the status of the operations with **Get-AzureRmResourceGroupDeploymentOperation**.</span></span>

  ```powershell 
  Get-AzureRmResourceGroupDeploymentOperation -ResourceGroupName ExampleGroup -DeploymentName vmDeployment
  ```

    <span data-ttu-id="79ae3-138">Que devuelve varias operaciones con cada una de ellas en el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="79ae3-138">Which returns multiple operations with each one in the following format:</span></span>

  ```powershell
  Id             : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.Resources/deployments/Microsoft.Template/operations/A3EB2DA598E0A780
  OperationId    : A3EB2DA598E0A780
  Properties     : @{provisioningOperation=Create; provisioningState=Succeeded; timestamp=2016-06-14T21:55:15.0156208Z;
                   duration=PT23.0227078S; trackingId=11d376e8-5d6d-4da8-847e-6f23c6443fbf;
                   serviceRequestId=0196828d-8559-4bf6-b6b8-8b9057cb0e23; statusCode=OK; targetResource=}
  PropertiesText : {duration:PT23.0227078S, provisioningOperation:Create, provisioningState:Succeeded,
                   serviceRequestId:0196828d-8559-4bf6-b6b8-8b9057cb0e23...}
  ```

3. <span data-ttu-id="79ae3-139">Para más información acerca de las operaciones con errores, recupere las propiedades de aquellas operaciones con el estado **Error** .</span><span class="sxs-lookup"><span data-stu-id="79ae3-139">To get more details about failed operations, retrieve the properties for operations with **Failed** state.</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object ProvisioningState -eq Failed
  ```
   
    <span data-ttu-id="79ae3-140">Que devuelve todas las operaciones con error con cada una de ellas en el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="79ae3-140">Which returns all the failed operations with each one in the following format:</span></span>

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

    <span data-ttu-id="79ae3-141">Tenga en cuenta los valores serviceRequestId y trackingId de la operación.</span><span class="sxs-lookup"><span data-stu-id="79ae3-141">Note the serviceRequestId and the trackingId for the operation.</span></span> <span data-ttu-id="79ae3-142">serviceRequestId puede resultar útil cuando se trabaja con el soporte técnico para solucionar un problema de implementación.</span><span class="sxs-lookup"><span data-stu-id="79ae3-142">The serviceRequestId can be helpful when working with technical support to troubleshoot a deployment.</span></span> <span data-ttu-id="79ae3-143">Utilizará trackingId en el paso siguiente para centrarse en una operación determinada.</span><span class="sxs-lookup"><span data-stu-id="79ae3-143">You will use the trackingId in the next step to focus on a particular operation.</span></span>
4. <span data-ttu-id="79ae3-144">Para obtener el mensaje de estado de una operación con error determinada, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="79ae3-144">To get the status message of a particular failed operation, use the following command:</span></span>

  ```powershell
  ((Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object trackingId -eq f4ed72f8-4203-43dc-958a-15d041e8c233).StatusMessage.error
  ```

    <span data-ttu-id="79ae3-145">Que devuelve:</span><span class="sxs-lookup"><span data-stu-id="79ae3-145">Which returns:</span></span>

  ```powershell
  code           message                                                                        details
  ----           -------                                                                        -------
  DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. {}
  ```
4. <span data-ttu-id="79ae3-146">Cada operación de implementación en Azure incluye el contenido de la solicitud y de la respuesta.</span><span class="sxs-lookup"><span data-stu-id="79ae3-146">Every deployment operation in Azure includes request and response content.</span></span> <span data-ttu-id="79ae3-147">El contenido de la solicitud es lo que se envía a Azure durante la implementación (por ejemplo, crear una máquina virtual, un disco del sistema operativo y otros recursos).</span><span class="sxs-lookup"><span data-stu-id="79ae3-147">The request content is what you sent to Azure during deployment (for example, create a VM, OS disk, and other resources).</span></span> <span data-ttu-id="79ae3-148">El contenido de la respuesta es lo que Azure devolvió de la solicitud de implementación.</span><span class="sxs-lookup"><span data-stu-id="79ae3-148">The response content is what Azure sent back from your deployment request.</span></span> <span data-ttu-id="79ae3-149">Durante la implementación, se puede usar el parámetro **DeploymentDebugLogLevel** para especificar que la solicitud o la respuesta se conserven en el registro.</span><span class="sxs-lookup"><span data-stu-id="79ae3-149">During deployment, you can use **DeploymentDebugLogLevel** paramenter to specify that the request and/or response are retained in the log.</span></span> 

  <span data-ttu-id="79ae3-150">Esa información se obtiene del registro y se guarda localmente mediante los siguientes comandos de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="79ae3-150">You get that information from the log, and save it locally by using the following PowerShell commands:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.request | ConvertTo-Json |  Out-File -FilePath <PathToFile>

  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.response | ConvertTo-Json |  Out-File -FilePath <PathToFile>
  ```

## <a name="azure-cli"></a><span data-ttu-id="79ae3-151">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="79ae3-151">Azure CLI</span></span>

1. <span data-ttu-id="79ae3-152">Obtenga el estado general de una implementación con el comando **azure group deployment show** .</span><span class="sxs-lookup"><span data-stu-id="79ae3-152">Get the overall status of a deployment with the **azure group deployment show** command.</span></span>

  ```azurecli
  azure group deployment show --resource-group ExampleGroup --name ExampleDeployment --json
  ```
  
  <span data-ttu-id="79ae3-153">Uno de los valores devueltos es **correlationId**.</span><span class="sxs-lookup"><span data-stu-id="79ae3-153">One of the returned values is the **correlationId**.</span></span> <span data-ttu-id="79ae3-154">Este valor se usa para realizar un seguimiento de eventos relacionados, y puede ser útil al colaborar con el soporte técnico para solucionar un problema de implementación.</span><span class="sxs-lookup"><span data-stu-id="79ae3-154">This value is used to track related events, and can be helpful when working with technical support to troubleshoot a deployment.</span></span>

  ```azurecli
  "properties": {
    "provisioningState": "Failed",
    "correlationId": "4002062a-a506-4b5e-aaba-4147036b771a",
  ```

2. <span data-ttu-id="79ae3-155">Para ver las operaciones para una implementación, use:</span><span class="sxs-lookup"><span data-stu-id="79ae3-155">To see the operations for a deployment, use:</span></span>

  ```azurecli
  azure group deployment operation list --resource-group ExampleGroup --name ExampleDeployment --json
  ```

## <a name="rest"></a><span data-ttu-id="79ae3-156">REST</span><span class="sxs-lookup"><span data-stu-id="79ae3-156">REST</span></span>

1. <span data-ttu-id="79ae3-157">Obtenga información sobre la implementación con la operación [Obtener información sobre una implementación de plantilla](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) .</span><span class="sxs-lookup"><span data-stu-id="79ae3-157">Get information about a deployment with the [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) operation.</span></span>

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}?api-version={api-version}
  ```

    <span data-ttu-id="79ae3-158">En la respuesta, observe en particular los elementos **provisioningState**, **correlationId** y **error**.</span><span class="sxs-lookup"><span data-stu-id="79ae3-158">In the response, note in particular the **provisioningState**, **correlationId**, and **error** elements.</span></span> <span data-ttu-id="79ae3-159">**correlationId** se usa para realizar un seguimiento de eventos relacionados y puede ser útil al colaborar con el soporte técnico para solucionar un problema de implementación.</span><span class="sxs-lookup"><span data-stu-id="79ae3-159">The **correlationId** is used to track related events, and can be helpful when working with technical support to troubleshoot a deployment.</span></span>

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

2. <span data-ttu-id="79ae3-160">Obtenga información sobre las operaciones de implementación con la operación [Enumerar todas las operaciones de implementación de plantilla](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) .</span><span class="sxs-lookup"><span data-stu-id="79ae3-160">Get information about deployment operations with the [List all template deployment operations](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) operation.</span></span> 

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}/operations?$skiptoken={skiptoken}&api-version={api-version}
  ```
   
    <span data-ttu-id="79ae3-161">La respuesta incluye información de la solicitud o la respuesta según lo especificado en la propiedad **debugSetting** durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="79ae3-161">The response includes request and/or response information based on what you specified in the **debugSetting** property during deployment.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="79ae3-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="79ae3-162">Next steps</span></span>
* <span data-ttu-id="79ae3-163">Para obtener ayuda con la resolución de errores de implementación concretos, consulte [Solución de problemas comunes al implementar recursos en Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="79ae3-163">For help with resolving particular deployment errors, see [Resolve common errors when deploying resources to Azure with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="79ae3-164">Para obtener información sobre cómo usar los registros de actividad para supervisar otros tipos de acciones, vea [View activity logs to manage Azure resources](resource-group-audit.md) (Ver registros de actividad para administrar recursos de Azure).</span><span class="sxs-lookup"><span data-stu-id="79ae3-164">To learn about using the activity logs to monitor other types of actions, see [View activity logs to manage Azure resources](resource-group-audit.md).</span></span>
* <span data-ttu-id="79ae3-165">Para validar la implementación antes de ejecutarla, consulte [Implementación de recursos con las plantillas de Resource Manager y Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="79ae3-165">To validate your deployment before executing it, see [Deploy a resource group with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

