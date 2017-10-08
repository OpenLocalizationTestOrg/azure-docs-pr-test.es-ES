---
title: recursos de aaaDeploy con API de REST y plantilla | Documentos de Microsoft
description: Use el Administrador de recursos de Azure y API de REST del Administrador de recursos toodeploy un tooAzure de recursos. recursos de Hola se definen en una plantilla de administrador de recursos.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 1d8fbd4c-78b0-425b-ba76-f2b7fd260b45
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: tomfitz
ms.openlocfilehash: 347ad3bdb604429e7291297d448688204af69b46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-resource-manager-rest-api"></a><span data-ttu-id="34e99-104">Implementación de recursos con las plantillas de Resource Manager y la API de REST de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="34e99-104">Deploy resources with Resource Manager templates and Resource Manager REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="34e99-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="34e99-105">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="34e99-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="34e99-106">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="34e99-107">Portal</span><span class="sxs-lookup"><span data-stu-id="34e99-107">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="34e99-108">API DE REST</span><span class="sxs-lookup"><span data-stu-id="34e99-108">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="34e99-109">Este artículo explica cómo toouse Hola API de REST del Administrador de recursos con el Administrador de recursos plantillas toodeploy su tooAzure de recursos.</span><span class="sxs-lookup"><span data-stu-id="34e99-109">This article explains how toouse hello Resource Manager REST API with Resource Manager templates toodeploy your resources tooAzure.</span></span>  

> [!TIP]
> <span data-ttu-id="34e99-110">Para obtener ayuda con la depuración de un error durante la implementación, consulte:</span><span class="sxs-lookup"><span data-stu-id="34e99-110">For help with debugging an error during deployment, see:</span></span>
> 
> * <span data-ttu-id="34e99-111">[Ver las operaciones de implementación](resource-manager-deployment-operations.md) toolearn sobre cómo obtener la información que le ayude a solucionar el error</span><span class="sxs-lookup"><span data-stu-id="34e99-111">[View deployment operations](resource-manager-deployment-operations.md) toolearn about getting information that helps you troubleshoot your error</span></span>
> * <span data-ttu-id="34e99-112">[Solucionar errores comunes al implementar tooAzure de recursos con el Administrador de recursos de Azure](resource-manager-common-deployment-errors.md) toolearn cómo tooresolve errores comunes de implementación</span><span class="sxs-lookup"><span data-stu-id="34e99-112">[Troubleshoot common errors when deploying resources tooAzure with Azure Resource Manager](resource-manager-common-deployment-errors.md) toolearn how tooresolve common deployment errors</span></span>
> 
> 

<span data-ttu-id="34e99-113">La plantilla puede ser un archivo local o en un archivo externo que está disponible a través de un identificador URI.</span><span class="sxs-lookup"><span data-stu-id="34e99-113">Your template can be either a local file or an external file that is available through a URI.</span></span> <span data-ttu-id="34e99-114">Cuando la plantilla reside en una cuenta de almacenamiento, puede restringir la plantilla de toohello de acceso y proporcionar un token de firma (SAS) de acceso compartido durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="34e99-114">When your template resides in a storage account, you can restrict access toohello template and provide a shared access signature (SAS) token during deployment.</span></span>

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

## <a name="deploy-with-hello-rest-api"></a><span data-ttu-id="34e99-115">Implementar con hello API de REST</span><span class="sxs-lookup"><span data-stu-id="34e99-115">Deploy with hello REST API</span></span>
1. <span data-ttu-id="34e99-116">Establezca los [encabezados y parámetros comunes](https://docs.microsoft.com/rest/api/index), incluidos los tokens de autenticación.</span><span class="sxs-lookup"><span data-stu-id="34e99-116">Set [common parameters and headers](https://docs.microsoft.com/rest/api/index), including authentication tokens.</span></span>
2. <span data-ttu-id="34e99-117">Si no tiene un grupo de recursos existente, puede crear uno.</span><span class="sxs-lookup"><span data-stu-id="34e99-117">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="34e99-118">Proporcionar el Id. de suscripción, el nombre de Hola de nuevo grupo de recursos de Hola y la ubicación que necesite para su solución.</span><span class="sxs-lookup"><span data-stu-id="34e99-118">Provide your subscription ID, hello name of hello new resource group, and location that you need for your solution.</span></span> <span data-ttu-id="34e99-119">Para obtener más información, consulte [Crear un grupo de recursos](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="34e99-119">For more information, see [Create a resource group](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).</span></span>
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>?api-version=2015-01-01
          <common headers>
          {
            "location": "West US",
            "tags": {
               "tagname1": "tagvalue1"
            }
          }
3. <span data-ttu-id="34e99-120">Validación de la implementación antes de ejecutarlo mediante la ejecución de hello [validar una implementación de plantilla](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) operación.</span><span class="sxs-lookup"><span data-stu-id="34e99-120">Validate your deployment before executing it by running hello [Validate a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) operation.</span></span> <span data-ttu-id="34e99-121">Al probar la implementación de hello, proporcionar parámetros exactamente como lo haría al ejecutar la implementación de hello (que se muestra en el paso siguiente de hello).</span><span class="sxs-lookup"><span data-stu-id="34e99-121">When testing hello deployment, provide parameters exactly as you would when executing hello deployment (shown in hello next step).</span></span>
4. <span data-ttu-id="34e99-122">Cree una implementación.</span><span class="sxs-lookup"><span data-stu-id="34e99-122">Create a deployment.</span></span> <span data-ttu-id="34e99-123">Proporcione el identificador de suscripción, nombre Hola Hola del grupo de recursos, nombre de Hola de implementación de hello y una plantilla de tooyour de vínculo.</span><span class="sxs-lookup"><span data-stu-id="34e99-123">Provide your subscription ID, hello name of hello resource group, hello name of hello deployment, and a link tooyour template.</span></span> <span data-ttu-id="34e99-124">Para obtener información sobre el archivo de plantilla de hello, consulte [archivo de parámetros](#parameter-file).</span><span class="sxs-lookup"><span data-stu-id="34e99-124">For information about hello template file, see [Parameter file](#parameter-file).</span></span> <span data-ttu-id="34e99-125">Para obtener más información acerca de la API de REST de hello toocreate un grupo de recursos, consulte [crear una implementación de plantilla](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="34e99-125">For more information about hello REST API toocreate a resource group, see [Create a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate).</span></span> <span data-ttu-id="34e99-126">Hola aviso **modo** se establece demasiado**Incremental**.</span><span class="sxs-lookup"><span data-stu-id="34e99-126">Notice hello **mode** is set too**Incremental**.</span></span> <span data-ttu-id="34e99-127">establece una implementación completa, toorun **modo** demasiado**completar**.</span><span class="sxs-lookup"><span data-stu-id="34e99-127">toorun a complete deployment, set **mode** too**Complete**.</span></span> <span data-ttu-id="34e99-128">Tenga cuidado al utilizar el modo completo de hello tal y como se puede eliminar accidentalmente los recursos que no están en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="34e99-128">Be careful when using hello complete mode as you can inadvertently delete resources that are not in your template.</span></span>
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
          <common headers>
          {
            "properties": {
              "templateLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
                "contentVersion": "1.0.0.0"
              },
              "mode": "Incremental",
              "parametersLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/parameters.json",
                "contentVersion": "1.0.0.0"
              }
            }
          }
   
      <span data-ttu-id="34e99-129">Si desea el contenido de la respuesta de toolog, contenido de la solicitud o ambos, incluir **debugSetting** en solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="34e99-129">If you want toolog response content, request content, or both, include **debugSetting** in hello request.</span></span>
   
        "debugSetting": {
          "detailLevel": "requestContent, responseContent"
        }
   
      <span data-ttu-id="34e99-130">Puede configurar su toouse de cuenta de almacenamiento un token de firma (SAS) de acceso compartido.</span><span class="sxs-lookup"><span data-stu-id="34e99-130">You can set up your storage account toouse a shared access signature (SAS) token.</span></span> <span data-ttu-id="34e99-131">Para obtener más información, consulte [Delegating Access with a Shared Access Signature](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature)(Delegación del acceso con una firma de acceso compartido).</span><span class="sxs-lookup"><span data-stu-id="34e99-131">For more information, see [Delegating Access with a Shared Access Signature](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).</span></span>
5. <span data-ttu-id="34e99-132">Obtener estado de Hola de implementación de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="34e99-132">Get hello status of hello template deployment.</span></span> <span data-ttu-id="34e99-133">Para obtener más información, consulte [Obtener información acerca de una implementación de plantilla](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span><span class="sxs-lookup"><span data-stu-id="34e99-133">For more information, see [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span></span>
   
          GET https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
           <common headers>

## <a name="parameter-file"></a><span data-ttu-id="34e99-134">Archivo de parámetros</span><span class="sxs-lookup"><span data-stu-id="34e99-134">Parameter file</span></span>

[!INCLUDE [resource-manager-parameter-file](../../includes/resource-manager-parameter-file.md)]

## <a name="next-steps"></a><span data-ttu-id="34e99-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="34e99-135">Next steps</span></span>
* <span data-ttu-id="34e99-136">toolearn sobre el control de operaciones asincrónicas de REST, consulte [realizar un seguimiento de las operaciones asincrónicas de Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="34e99-136">toolearn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
* <span data-ttu-id="34e99-137">Para obtener un ejemplo de la implementación de los recursos a través de la biblioteca de cliente de .NET de hello, consulte [implementar usando las bibliotecas de .NET y una plantilla de recursos](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="34e99-137">For an example of deploying resources through hello .NET client library, see [Deploy resources using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="34e99-138">toodefine parámetros de plantilla, vea [crear plantillas](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="34e99-138">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="34e99-139">Para obtener instrucciones sobre la implementación de los entornos de toodifferent de solución, vea [entornos de desarrollo y prueba en Microsoft Azure](solution-dev-test-environments.md).</span><span class="sxs-lookup"><span data-stu-id="34e99-139">For guidance on deploying your solution toodifferent environments, see [Development and test environments in Microsoft Azure](solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="34e99-140">Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="34e99-140">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

