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
# <a name="understand-azure-deployment-errors"></a><span data-ttu-id="12502-104">Información sobre los errores de implementación de Azure</span><span class="sxs-lookup"><span data-stu-id="12502-104">Understand Azure deployment errors</span></span>
<span data-ttu-id="12502-105">En este tema se describen los errores de implementación y cómo obtener más información sobre un error.</span><span class="sxs-lookup"><span data-stu-id="12502-105">This topic describes deployment errors and how you can discover more information about an error.</span></span> <span data-ttu-id="12502-106">Para errores de implementación de las soluciones toocommon, vea [solucionar errores comunes de implementación de Azure con el Administrador de recursos de Azure](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="12502-106">For resolutions toocommon deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="two-types-of-errors"></a><span data-ttu-id="12502-107">Dos tipos de errores</span><span class="sxs-lookup"><span data-stu-id="12502-107">Two types of errors</span></span>
<span data-ttu-id="12502-108">Hay dos tipos de errores que puede recibir:</span><span class="sxs-lookup"><span data-stu-id="12502-108">There are two types of errors you can receive:</span></span>

* <span data-ttu-id="12502-109">Errores de validación</span><span class="sxs-lookup"><span data-stu-id="12502-109">validation errors</span></span>
* <span data-ttu-id="12502-110">Errores de implementación</span><span class="sxs-lookup"><span data-stu-id="12502-110">deployment errors</span></span>

<span data-ttu-id="12502-111">Hola después de la imagen muestra el registro de actividad de Hola para una suscripción.</span><span class="sxs-lookup"><span data-stu-id="12502-111">hello following image shows hello activity log for a subscription.</span></span> <span data-ttu-id="12502-112">Representa dos implementaciones.</span><span class="sxs-lookup"><span data-stu-id="12502-112">It represents two deployments.</span></span> <span data-ttu-id="12502-113">En la misma implementación, plantilla de hello, no pudo validar (**validar**) y no.</span><span class="sxs-lookup"><span data-stu-id="12502-113">In one deployment, hello template failed validation (**Validate**) and did not proceed.</span></span> <span data-ttu-id="12502-114">En Hola otra implementación, plantilla Hola pasó la validación pero no se pudo al crear recursos de hello (**escribir implementaciones**).</span><span class="sxs-lookup"><span data-stu-id="12502-114">In hello other deployment, hello template passed validation but failed when creating hello resources (**Write Deployments**).</span></span> 

![Visualización del código de error](./media/resource-manager-troubleshoot-tips/show-activity-log.png)

<span data-ttu-id="12502-116">Los errores de validación que provienen de escenarios que se pueden determinar antes de la implementación</span><span class="sxs-lookup"><span data-stu-id="12502-116">Validation errors arise from scenarios that can be determined before deployment.</span></span> <span data-ttu-id="12502-117">Incluyen errores de sintaxis en la plantilla o tratar de recursos de toodeploy que se superen las cuotas de suscripción.</span><span class="sxs-lookup"><span data-stu-id="12502-117">They include syntax errors in your template, or trying toodeploy resources that would exceed your subscription quotas.</span></span> <span data-ttu-id="12502-118">Errores de implementación provengan de condiciones que se producen durante el proceso de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="12502-118">Deployment errors arise from conditions that occur during hello deployment process.</span></span> <span data-ttu-id="12502-119">Incluyen intentar tooaccess un recurso que se va a implementar en paralelo.</span><span class="sxs-lookup"><span data-stu-id="12502-119">They include trying tooaccess a resource that is being deployed in parallel.</span></span>

<span data-ttu-id="12502-120">Ambos tipos de errores devuelve un código de error que utiliza la implementación de hello tootroubleshoot.</span><span class="sxs-lookup"><span data-stu-id="12502-120">Both types of errors return an error code that you use tootroubleshoot hello deployment.</span></span> <span data-ttu-id="12502-121">Ambos tipos de errores aparecen en hello [registro de actividad](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="12502-121">Both types of errors appear in hello [activity log](resource-group-audit.md).</span></span> <span data-ttu-id="12502-122">Sin embargo, los errores de validación no aparecen en el historial de implementación porque se ha iniciado nunca implementación Hola.</span><span class="sxs-lookup"><span data-stu-id="12502-122">However, validation errors do not appear in your deployment history because hello deployment never started.</span></span>

## <a name="determine-error-code"></a><span data-ttu-id="12502-123">Determinación del código de error</span><span class="sxs-lookup"><span data-stu-id="12502-123">Determine error code</span></span>

<span data-ttu-id="12502-124">Puede obtener información acerca de un error, mire el mensaje de error de Hola y código de error de Hola.</span><span class="sxs-lookup"><span data-stu-id="12502-124">You can learn about an error by looking at hello error message and hello error code.</span></span> <span data-ttu-id="12502-125">Hola [solucionar errores comunes de implementación de Azure con el Administrador de recursos de Azure](resource-manager-common-deployment-errors.md) artículo enumeran las soluciones por código de error.</span><span class="sxs-lookup"><span data-stu-id="12502-125">hello [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md) article lists resolutions by error code.</span></span> <span data-ttu-id="12502-126">Este tema muestra cómo toouse Hola código de error de hello toodiscover de portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="12502-126">This topic shows how toouse hello Azure portal toodiscover hello error code.</span></span>

### <a name="validation-errors"></a><span data-ttu-id="12502-127">Errores de validación</span><span class="sxs-lookup"><span data-stu-id="12502-127">Validation errors</span></span>

<span data-ttu-id="12502-128">Cuando se implementa a través del portal de hello, verá un error de validación después de enviar sus valores.</span><span class="sxs-lookup"><span data-stu-id="12502-128">When deploying through hello portal, you see a validation error after submitting your values.</span></span>

![vista del error de validación en el portal](./media/resource-manager-troubleshoot-tips/validation-error.png)

<span data-ttu-id="12502-130">Seleccione el mensaje de Hola para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="12502-130">Select hello message for more details.</span></span> <span data-ttu-id="12502-131">Hola después de la imagen, verá un **InvalidTemplateDeployment** error y un mensaje que indica que una directiva esté bloqueado implementación.</span><span class="sxs-lookup"><span data-stu-id="12502-131">In hello following image, you see an **InvalidTemplateDeployment** error and a message that indicates a policy blocked deployment.</span></span>

![vista de los detalles de validación](./media/resource-manager-troubleshoot-tips/validation-details.png)

### <a name="deployment-errors"></a><span data-ttu-id="12502-133">Errores de implementación</span><span class="sxs-lookup"><span data-stu-id="12502-133">Deployment errors</span></span>

<span data-ttu-id="12502-134">Cuando la operación de hello pasa la validación, pero se produce un error durante la implementación, consulte error hello en las notificaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="12502-134">When hello operation passes validation, but fails during deployment, you see hello error in hello notifications.</span></span> <span data-ttu-id="12502-135">Seleccione la notificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="12502-135">Select hello notification.</span></span>

![notificación de error](./media/resource-manager-troubleshoot-tips/notification.png)

<span data-ttu-id="12502-137">Consulte más detalles acerca de la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="12502-137">You see more details about hello deployment.</span></span> <span data-ttu-id="12502-138">Seleccione Hola opción toofind obtener más información sobre el error de Hola.</span><span class="sxs-lookup"><span data-stu-id="12502-138">Select hello option toofind more information about hello error.</span></span>

![error de implementación](./media/resource-manager-troubleshoot-tips/deployment-failed.png)

<span data-ttu-id="12502-140">Consulte códigos de error y de mensaje de error de Hola.</span><span class="sxs-lookup"><span data-stu-id="12502-140">You see hello error message and error codes.</span></span> <span data-ttu-id="12502-141">Observe que hay dos códigos de error.</span><span class="sxs-lookup"><span data-stu-id="12502-141">Notice there are two error codes.</span></span> <span data-ttu-id="12502-142">Hola primer código de error (**implementación**) es un error general que no proporciona detalles hello tiene errores de hello toosolve.</span><span class="sxs-lookup"><span data-stu-id="12502-142">hello first error code (**DeploymentFailed**) is a general error that does not provide hello details you need toosolve hello error.</span></span> <span data-ttu-id="12502-143">Hola segundo código de error (**StorageAccountNotFound**) proporciona detalles de Hola que necesita.</span><span class="sxs-lookup"><span data-stu-id="12502-143">hello second error code (**StorageAccountNotFound**) provides hello details you need.</span></span> 

![detalles del error](./media/resource-manager-troubleshoot-tips/error-details.png)

## <a name="enable-debug-logging"></a><span data-ttu-id="12502-145">Habilitación del registro de depuración</span><span class="sxs-lookup"><span data-stu-id="12502-145">Enable debug logging</span></span>
<span data-ttu-id="12502-146">En ciertas ocasiones necesitará obtener más información sobre toodiscover de solicitud y respuesta de hello qué salió mal.</span><span class="sxs-lookup"><span data-stu-id="12502-146">Sometimes you need more information about hello request and response toodiscover what went wrong.</span></span> <span data-ttu-id="12502-147">Mediante el uso de PowerShell o la CLI de Azure, puede solicitar que se registre información adicional durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="12502-147">By using PowerShell or Azure CLI, you can request that additional information is logged during a deployment.</span></span>

- <span data-ttu-id="12502-148">PowerShell</span><span class="sxs-lookup"><span data-stu-id="12502-148">PowerShell</span></span>

   <span data-ttu-id="12502-149">En PowerShell, establezca hello **DeploymentDebugLogLevel** parámetro tooAll, ResponseContent o RequestContent.</span><span class="sxs-lookup"><span data-stu-id="12502-149">In PowerShell, set hello **DeploymentDebugLogLevel** parameter tooAll, ResponseContent, or RequestContent.</span></span>

  ```powershell
  New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile c:\Azure\Templates\storage.json -DeploymentDebugLogLevel All
  ```

   <span data-ttu-id="12502-150">Examine el contenido de la solicitud de hello con hello siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="12502-150">Examine hello request content with hello following cmdlet:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.request | ConvertTo-Json
  ```

   <span data-ttu-id="12502-151">O bien, Hola respuesta contenida con:</span><span class="sxs-lookup"><span data-stu-id="12502-151">Or, hello response content with:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.response | ConvertTo-Json
  ```

   <span data-ttu-id="12502-152">Esta información puede ayudarle a determinar si un valor en la plantilla de Hola se establece incorrectamente.</span><span class="sxs-lookup"><span data-stu-id="12502-152">This information can help you determine whether a value in hello template is being incorrectly set.</span></span>

- <span data-ttu-id="12502-153">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="12502-153">Azure CLI</span></span>

   <span data-ttu-id="12502-154">Examine las operaciones de implementación de hello con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="12502-154">Examine hello deployment operations with hello following command:</span></span>

  ```azurecli
  az group deployment operation list --resource-group ExampleGroup --name vmlinux
  ```

- <span data-ttu-id="12502-155">Plantilla anidada</span><span class="sxs-lookup"><span data-stu-id="12502-155">Nested template</span></span>

   <span data-ttu-id="12502-156">toolog información de depuración para una plantilla anidada, use hello **debugSetting** elemento.</span><span class="sxs-lookup"><span data-stu-id="12502-156">toolog debug information for a nested template, use hello **debugSetting** element.</span></span>

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


## <a name="create-a-troubleshooting-template"></a><span data-ttu-id="12502-157">Creación de una plantilla de solución de problemas</span><span class="sxs-lookup"><span data-stu-id="12502-157">Create a troubleshooting template</span></span>
<span data-ttu-id="12502-158">En algunos casos, Hola tootroubleshoot de manera más fácil la plantilla es tootest partes de él.</span><span class="sxs-lookup"><span data-stu-id="12502-158">In some cases, hello easiest way tootroubleshoot your template is tootest parts of it.</span></span> <span data-ttu-id="12502-159">Puede crear una plantilla simplificada que le permite toofocus por parte de Hola que cree que está provocando el error de Hola.</span><span class="sxs-lookup"><span data-stu-id="12502-159">You can create a simplified template that enables you toofocus on hello part that you believe is causing hello error.</span></span> <span data-ttu-id="12502-160">Por ejemplo, supongamos que se recibe un error al hacer referencia a un recurso.</span><span class="sxs-lookup"><span data-stu-id="12502-160">For example, suppose you are receiving an error when referencing a resource.</span></span> <span data-ttu-id="12502-161">En lugar de tratar directamente con una plantilla de toda, crear una plantilla que devuelve parte de Hola que puedan estar causando el problema.</span><span class="sxs-lookup"><span data-stu-id="12502-161">Rather than dealing with an entire template, create a template that returns hello part that may be causing your problem.</span></span> <span data-ttu-id="12502-162">Puede ayudarle a determinar si se pasa en parámetros correctos de hello, mediante las funciones de plantilla correctamente, y obtener recursos de Hola que espera.</span><span class="sxs-lookup"><span data-stu-id="12502-162">It can help you determine whether you are passing in hello right parameters, using template functions correctly, and getting hello resource you expect.</span></span>

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

<span data-ttu-id="12502-163">O bien, supongamos que se están produciendo errores de implementación que cree que están relacionados con tooincorrectly establezca las dependencias.</span><span class="sxs-lookup"><span data-stu-id="12502-163">Or, suppose you are encountering deployment errors that you believe are related tooincorrectly set dependencies.</span></span> <span data-ttu-id="12502-164">Pruebe la plantilla dividiéndola en plantillas simplificadas.</span><span class="sxs-lookup"><span data-stu-id="12502-164">Test your template by breaking it into simplified templates.</span></span> <span data-ttu-id="12502-165">En primer lugar, cree una plantilla que implemente solo un único recurso (por ejemplo, un servidor SQL Server).</span><span class="sxs-lookup"><span data-stu-id="12502-165">First, create a template that deploys only a single resource (like a SQL Server).</span></span> <span data-ttu-id="12502-166">Cuando esté seguro de que tiene dicho recurso definido correctamente, agregue un recurso que dependa de él (por ejemplo, una base de datos SQL).</span><span class="sxs-lookup"><span data-stu-id="12502-166">When you are sure you have that resource correctly defined, add a resource that depends on it (like a SQL Database).</span></span> <span data-ttu-id="12502-167">Cuando esos dos recursos se definan correctamente, agregue otros recursos dependientes (por ejemplo, las directivas de auditoría).</span><span class="sxs-lookup"><span data-stu-id="12502-167">When you have those two resources correctly defined, add other dependent resources (like auditing policies).</span></span> <span data-ttu-id="12502-168">Entre cada implementación de prueba, elimine Hola recursos toomake seguro de prueba adecuadamente hello las dependencias del grupo.</span><span class="sxs-lookup"><span data-stu-id="12502-168">In between each test deployment, delete hello resource group toomake sure you adequately testing hello dependencies.</span></span> 

## <a name="check-deployment-sequence"></a><span data-ttu-id="12502-169">Comprobación de la secuencia de implementación</span><span class="sxs-lookup"><span data-stu-id="12502-169">Check deployment sequence</span></span>

<span data-ttu-id="12502-170">Muchos errores de implementación se producen cuando los recursos se implementan en una secuencia inesperada.</span><span class="sxs-lookup"><span data-stu-id="12502-170">Many deployment errors happen when resources are deployed in an unexpected sequence.</span></span> <span data-ttu-id="12502-171">Estos errores se producen cuando las dependencias no se han establecido correctamente.</span><span class="sxs-lookup"><span data-stu-id="12502-171">These errors arise when dependencies are not correctly set.</span></span> <span data-ttu-id="12502-172">Cuando falta una dependencia necesaria, un recurso intenta toouse que aún no existe ningún valor para otro recurso pero Hola otro.</span><span class="sxs-lookup"><span data-stu-id="12502-172">When you are missing a needed dependency, one resource attempts toouse a value for another resource but hello other does not yet exist.</span></span> <span data-ttu-id="12502-173">Recibirá un error que indica que no se encuentra el recurso.</span><span class="sxs-lookup"><span data-stu-id="12502-173">You get an error stating that a resource is not found.</span></span> <span data-ttu-id="12502-174">Puede encontrar este tipo de error de forma intermitente porque el tiempo de implementación de Hola para cada recurso puede variar.</span><span class="sxs-lookup"><span data-stu-id="12502-174">You may encounter this type of error intermittently because hello deployment time for each resource can vary.</span></span> <span data-ttu-id="12502-175">Por ejemplo, la primera toodeploy de intento de los recursos se realiza correctamente debido a un recurso necesario aleatoriamente finaliza en el tiempo.</span><span class="sxs-lookup"><span data-stu-id="12502-175">For example, your first attempt toodeploy your resources succeeds because a required resource randomly completes in time.</span></span> <span data-ttu-id="12502-176">Sin embargo, se produce un error en el segundo intento porque Hola requiere recursos no se completó en el tiempo.</span><span class="sxs-lookup"><span data-stu-id="12502-176">However, your second attempt fails because hello required resource did not complete in time.</span></span> 

<span data-ttu-id="12502-177">Sin embargo, desea tooavoid configurar las dependencias que no son necesarios.</span><span class="sxs-lookup"><span data-stu-id="12502-177">But, you want tooavoid setting dependencies that are not needed.</span></span> <span data-ttu-id="12502-178">Cuando hay dependencias innecesarias, prolongar la duración de Hola de implementación de hello al impedir que los recursos que no son dependientes entre sí se implementen en paralelo.</span><span class="sxs-lookup"><span data-stu-id="12502-178">When you have unnecessary dependencies, you prolong hello duration of hello deployment by preventing resources that are not dependent on each other from being deployed in parallel.</span></span> <span data-ttu-id="12502-179">Además, puede crear dependencias circulares que bloquean la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="12502-179">In addition, you may create circular dependencies that block hello deployment.</span></span> <span data-ttu-id="12502-180">Hola [referencia](resource-group-template-functions-resource.md#reference) función crea una dependencia implícita en el recurso de hello al que hace referencia, cuando ese recurso se implementa en hello misma plantilla.</span><span class="sxs-lookup"><span data-stu-id="12502-180">hello [reference](resource-group-template-functions-resource.md#reference) function creates an implicit dependency on hello referenced resource, when that resource is deployed in hello same template.</span></span> <span data-ttu-id="12502-181">Por lo tanto, puede tener más dependencias de las dependencias de hello especificadas en hello **dependsOn** propiedad.</span><span class="sxs-lookup"><span data-stu-id="12502-181">Therefore, you may have more dependencies than hello dependencies specified in hello **dependsOn** property.</span></span> <span data-ttu-id="12502-182">Hola [resourceId](resource-group-template-functions-resource.md#resourceid) función no crea una dependencia implícita ni validar la existencia de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="12502-182">hello [resourceId](resource-group-template-functions-resource.md#resourceid) function does not create an implicit dependency or validate that hello resource exists.</span></span>

<span data-ttu-id="12502-183">Cuando se encuentran problemas de dependencia, necesita una visión general de toogain en orden de Hola de implementación de los recursos.</span><span class="sxs-lookup"><span data-stu-id="12502-183">When you encounter dependency problems, you need toogain insight into hello order of resource deployment.</span></span> <span data-ttu-id="12502-184">orden de hello tooview de las operaciones de implementación:</span><span class="sxs-lookup"><span data-stu-id="12502-184">tooview hello order of deployment operations:</span></span>

1. <span data-ttu-id="12502-185">Seleccione el historial de implementación de hello para el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="12502-185">Select hello deployment history for your resource group.</span></span>

   ![seleccionar el historial de implementaciones](./media/resource-manager-troubleshoot-tips/select-deployment.png)

2. <span data-ttu-id="12502-187">Seleccione una implementación de historial de Hola y seleccione **eventos**.</span><span class="sxs-lookup"><span data-stu-id="12502-187">Select a deployment from hello history, and select **Events**.</span></span>

   ![seleccionar eventos de implementación](./media/resource-manager-troubleshoot-tips/select-deployment-events.png)

3. <span data-ttu-id="12502-189">Examine la secuencia de Hola de eventos para cada recurso.</span><span class="sxs-lookup"><span data-stu-id="12502-189">Examine hello sequence of events for each resource.</span></span> <span data-ttu-id="12502-190">Estado de toohello de atención de cada operación del pago.</span><span class="sxs-lookup"><span data-stu-id="12502-190">Pay attention toohello status of each operation.</span></span> <span data-ttu-id="12502-191">Por ejemplo, hello siguiente imagen muestra tres cuentas de almacenamiento que se implementan en paralelo.</span><span class="sxs-lookup"><span data-stu-id="12502-191">For example, hello following image shows three storage accounts that deployed in parallel.</span></span> <span data-ttu-id="12502-192">Tenga en cuenta que Hola tres cuentas de almacenamiento se inician en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="12502-192">Notice that hello three storage accounts are started at hello same time.</span></span>

   ![implementación paralela](./media/resource-manager-troubleshoot-tips/deployment-events-parallel.png)

   <span data-ttu-id="12502-194">imagen de Hello siguiente muestra tres cuentas de almacenamiento que no se implementan en paralelo.</span><span class="sxs-lookup"><span data-stu-id="12502-194">hello next image shows three storage accounts that are not deployed in parallel.</span></span> <span data-ttu-id="12502-195">cuenta de almacenamiento segundo Hola depende de la primera cuenta de almacenamiento hello y depende de la cuenta de almacenamiento de terceros de Hola Hola segunda cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="12502-195">hello second storage account depends on hello first storage account, and hello third storage account depends on hello second storage account.</span></span> <span data-ttu-id="12502-196">Por lo tanto, primera cuenta de almacenamiento Hola se inicia, acepta y completar antes de que se inicia Hola junto.</span><span class="sxs-lookup"><span data-stu-id="12502-196">Therefore, hello first storage account is started, accepted, and completed before hello next is started.</span></span>

   ![implementación secuencial](./media/resource-manager-troubleshoot-tips/deployment-events-sequence.png)

<span data-ttu-id="12502-198">Incluso para los escenarios más complicados, puede usar Hola mismo toodiscover técnica cuando la implementación se inicia y se completa para cada recurso.</span><span class="sxs-lookup"><span data-stu-id="12502-198">Even for more complicated scenarios, you can use hello same technique toodiscover when deployment is started and completed for each resource.</span></span> <span data-ttu-id="12502-199">Examine la toosee de eventos de implementación si la secuencia de hello es diferente que se esperaría.</span><span class="sxs-lookup"><span data-stu-id="12502-199">Look through your deployment events toosee if hello sequence is different than you would expect.</span></span> <span data-ttu-id="12502-200">Si es así, vuelva a evaluar las dependencias de Hola para este recurso.</span><span class="sxs-lookup"><span data-stu-id="12502-200">If so, reevaluate hello dependencies for this resource.</span></span>

<span data-ttu-id="12502-201">Resource Manager identifica dependencias circulares durante la validación de plantillas.</span><span class="sxs-lookup"><span data-stu-id="12502-201">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="12502-202">y devuelve un mensaje de error que indica específicamente que existe una dependencia circular.</span><span class="sxs-lookup"><span data-stu-id="12502-202">It returns an error message that specifically states a circular dependency exists.</span></span> <span data-ttu-id="12502-203">toosolve una dependencia circular:</span><span class="sxs-lookup"><span data-stu-id="12502-203">toosolve a circular dependency:</span></span>

1. <span data-ttu-id="12502-204">En la plantilla, encuentra el recurso de hello identificada una dependencia circular Hola.</span><span class="sxs-lookup"><span data-stu-id="12502-204">In your template, find hello resource identified in hello circular dependency.</span></span> 
2. <span data-ttu-id="12502-205">Para ese recurso, examine hello **dependsOn** propiedad y todos los usos de hello **referencia** toosee qué recursos depende de función.</span><span class="sxs-lookup"><span data-stu-id="12502-205">For that resource, examine hello **dependsOn** property and any uses of hello **reference** function toosee which resources it depends on.</span></span> 
3. <span data-ttu-id="12502-206">Examine los toosee de recursos los recursos que dependen.</span><span class="sxs-lookup"><span data-stu-id="12502-206">Examine those resources toosee which resources they depend on.</span></span> <span data-ttu-id="12502-207">Siga las dependencias de hello hasta que observe un recurso que depende del recurso de hello original.</span><span class="sxs-lookup"><span data-stu-id="12502-207">Follow hello dependencies until you notice a resource that depends on hello original resource.</span></span>
5. <span data-ttu-id="12502-208">Para obtener recursos Hola implicados en una dependencia circular hello, examine con cuidado todos los usos de hello **dependsOn** propiedad tooidentify todas las dependencias que no son necesarios.</span><span class="sxs-lookup"><span data-stu-id="12502-208">For hello resources involved in hello circular dependency, carefully examine all uses of hello **dependsOn** property tooidentify any dependencies that are not needed.</span></span> <span data-ttu-id="12502-209">Quite esas dependencias.</span><span class="sxs-lookup"><span data-stu-id="12502-209">Remove those dependencies.</span></span> <span data-ttu-id="12502-210">Si no está seguro de si una dependencia es necesaria, pruebe a quitarla.</span><span class="sxs-lookup"><span data-stu-id="12502-210">If you are unsure that a dependency is needed, try removing it.</span></span> 
6. <span data-ttu-id="12502-211">Volver a implementar la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="12502-211">Redeploy hello template.</span></span>

<span data-ttu-id="12502-212">Cómo quitar valores de hello **dependsOn** propiedad puede producir errores cuando se implementa plantilla Hola.</span><span class="sxs-lookup"><span data-stu-id="12502-212">Removing values from hello **dependsOn** property can cause errors when you deploy hello template.</span></span> <span data-ttu-id="12502-213">Si se produce un error, agregue la dependencia de hello en plantilla Hola.</span><span class="sxs-lookup"><span data-stu-id="12502-213">If you encounter an error, add hello dependency back into hello template.</span></span> 

<span data-ttu-id="12502-214">Si este enfoque no soluciona una dependencia circular hello, considere la posibilidad de mover parte de la lógica de implementación a recursos secundarios (por ejemplo, extensiones o valores de configuración).</span><span class="sxs-lookup"><span data-stu-id="12502-214">If that approach does not solve hello circular dependency, consider moving part of your deployment logic into child resources (such as extensions or configuration settings).</span></span> <span data-ttu-id="12502-215">Configurar los toodeploy de recursos secundarios después de recursos de hello implicados en una dependencia circular Hola.</span><span class="sxs-lookup"><span data-stu-id="12502-215">Configure those child resources toodeploy after hello resources involved in hello circular dependency.</span></span> <span data-ttu-id="12502-216">Por ejemplo, suponga que va a implementar dos máquinas virtuales pero debe establecer las propiedades en cada uno de ellos que hacen referencia toohello otro.</span><span class="sxs-lookup"><span data-stu-id="12502-216">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer toohello other.</span></span> <span data-ttu-id="12502-217">Puede implementarlos en hello siguiente orden:</span><span class="sxs-lookup"><span data-stu-id="12502-217">You can deploy them in hello following order:</span></span>

1. <span data-ttu-id="12502-218">vm1</span><span class="sxs-lookup"><span data-stu-id="12502-218">vm1</span></span>
2. <span data-ttu-id="12502-219">vm2</span><span class="sxs-lookup"><span data-stu-id="12502-219">vm2</span></span>
3. <span data-ttu-id="12502-220">La extensión en vm1 depende de vm1 y vm2.</span><span class="sxs-lookup"><span data-stu-id="12502-220">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="12502-221">extensión de Hello establece valores en vm1 que obtiene de vm2.</span><span class="sxs-lookup"><span data-stu-id="12502-221">hello extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="12502-222">La extensión en vm2 depende de vm1 y vm2.</span><span class="sxs-lookup"><span data-stu-id="12502-222">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="12502-223">extensión de Hello establece valores en vm2 que obtiene de vm1.</span><span class="sxs-lookup"><span data-stu-id="12502-223">hello extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="12502-224">Hola mismo enfoque funciona para las aplicaciones de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="12502-224">hello same approach works for App Service apps.</span></span> <span data-ttu-id="12502-225">Considere la posibilidad de mover los valores de configuración a un recurso secundario del recurso de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="12502-225">Consider moving configuration values into a child resource of hello app resource.</span></span> <span data-ttu-id="12502-226">Puede implementar dos aplicaciones web en hello siguiente orden:</span><span class="sxs-lookup"><span data-stu-id="12502-226">You can deploy two web apps in hello following order:</span></span>

1. <span data-ttu-id="12502-227">webapp1</span><span class="sxs-lookup"><span data-stu-id="12502-227">webapp1</span></span>
2. <span data-ttu-id="12502-228">webapp2</span><span class="sxs-lookup"><span data-stu-id="12502-228">webapp2</span></span>
3. <span data-ttu-id="12502-229">La configuración de webapp1 depende de webapp1 y webapp2.</span><span class="sxs-lookup"><span data-stu-id="12502-229">config for webapp1 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="12502-230">Contiene la configuración de aplicación con valores de webapp2.</span><span class="sxs-lookup"><span data-stu-id="12502-230">It contains app settings with values from webapp2.</span></span>
4. <span data-ttu-id="12502-231">La configuración de webapp2 depende de webapp1 y webapp2.</span><span class="sxs-lookup"><span data-stu-id="12502-231">config for webapp2 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="12502-232">Contiene la configuración de aplicación con valores de webapp1.</span><span class="sxs-lookup"><span data-stu-id="12502-232">It contains app settings with values from webapp1.</span></span>


## <a name="next-steps"></a><span data-ttu-id="12502-233">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="12502-233">Next steps</span></span>
* <span data-ttu-id="12502-234">Para errores de implementación de las soluciones toocommon, vea [solucionar errores comunes de implementación de Azure con el Administrador de recursos de Azure](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="12502-234">For resolutions toocommon deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="12502-235">toolearn acerca de la auditoría de acciones, vea [auditoría de las operaciones con el Administrador de recursos](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="12502-235">toolearn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="12502-236">toolearn acerca de los errores de hello toodetermine de acciones durante la implementación, consulte [ver las operaciones de implementación](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="12502-236">toolearn about actions toodetermine hello errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
