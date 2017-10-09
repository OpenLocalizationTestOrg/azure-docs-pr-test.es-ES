---
title: "aaaTroubleshoot los errores comunes de la implementación de Azure | Documentos de Microsoft"
description: "Describe cómo tooresolve errores comunes al implementar tooAzure de recursos con el Administrador de recursos de Azure."
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "error de implementación, implementación de azure, implementar tooazure"
ms.assetid: c002a9be-4de5-4963-bd14-b54aa3d8fa59
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: tomfitz
ms.openlocfilehash: 8571e9941879eb5586e4258a785b6a09247da771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-azure-deployment-errors-with-azure-resource-manager"></a><span data-ttu-id="5cdd1-104">Solución de errores comunes de implementación de Azure con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5cdd1-104">Troubleshoot common Azure deployment errors with Azure Resource Manager</span></span>
<span data-ttu-id="5cdd1-105">En este tema se describe cómo resolver algunos errores comunes con los que puede encontrarse al realizar una implementación de Azure.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-105">This topic describes how you can resolve some common Azure deployment errors you may encounter.</span></span>

<span data-ttu-id="5cdd1-106">Hola siguientes códigos de error se describe en este tema:</span><span class="sxs-lookup"><span data-stu-id="5cdd1-106">hello following error codes are described in this topic:</span></span>

* [<span data-ttu-id="5cdd1-107">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="5cdd1-107">AccountNameInvalid</span></span>](#accountnameinvalid)
* [<span data-ttu-id="5cdd1-108">Error de autorización</span><span class="sxs-lookup"><span data-stu-id="5cdd1-108">Authorization failed</span></span>](#authorization-failed)
* [<span data-ttu-id="5cdd1-109">BadRequest</span><span class="sxs-lookup"><span data-stu-id="5cdd1-109">BadRequest</span></span>](#badrequest)
* [<span data-ttu-id="5cdd1-110">DeploymentFailed</span><span class="sxs-lookup"><span data-stu-id="5cdd1-110">DeploymentFailed</span></span>](#deploymentfailed)
* [<span data-ttu-id="5cdd1-111">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="5cdd1-111">DisallowedOperation</span></span>](#disallowedoperation)
* [<span data-ttu-id="5cdd1-112">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="5cdd1-112">InvalidContentLink</span></span>](#invalidcontentlink)
* [<span data-ttu-id="5cdd1-113">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="5cdd1-113">InvalidTemplate</span></span>](#invalidtemplate)
* [<span data-ttu-id="5cdd1-114">MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="5cdd1-114">MissingSubscriptionRegistration</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="5cdd1-115">NotFound</span><span class="sxs-lookup"><span data-stu-id="5cdd1-115">NotFound</span></span>](#notfound)
* [<span data-ttu-id="5cdd1-116">NoRegisteredProviderFound</span><span class="sxs-lookup"><span data-stu-id="5cdd1-116">NoRegisteredProviderFound</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="5cdd1-117">OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="5cdd1-117">OperationNotAllowed</span></span>](#quotaexceeded)
* [<span data-ttu-id="5cdd1-118">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="5cdd1-118">ParentResourceNotFound</span></span>](#parentresourcenotfound)
* [<span data-ttu-id="5cdd1-119">QuotaExceeded</span><span class="sxs-lookup"><span data-stu-id="5cdd1-119">QuotaExceeded</span></span>](#quotaexceeded)
* [<span data-ttu-id="5cdd1-120">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="5cdd1-120">RequestDisallowedByPolicy</span></span>](#requestdisallowedbypolicy)
* [<span data-ttu-id="5cdd1-121">ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="5cdd1-121">ResourceNotFound</span></span>](#notfound)
* [<span data-ttu-id="5cdd1-122">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="5cdd1-122">SkuNotAvailable</span></span>](#skunotavailable)
* [<span data-ttu-id="5cdd1-123">StorageAccountAlreadyExists</span><span class="sxs-lookup"><span data-stu-id="5cdd1-123">StorageAccountAlreadyExists</span></span>](#storagenamenotunique)
* [<span data-ttu-id="5cdd1-124">StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="5cdd1-124">StorageAccountAlreadyTaken</span></span>](#storagenamenotunique)

## <a name="deploymentfailed"></a><span data-ttu-id="5cdd1-125">DeploymentFailed</span><span class="sxs-lookup"><span data-stu-id="5cdd1-125">DeploymentFailed</span></span>

<span data-ttu-id="5cdd1-126">Este código de error indica un error de implementación general, pero no es código de error de Hola que necesita toostart solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-126">This error code indicates a general deployment error, but it is not hello error code you need toostart troubleshooting.</span></span> <span data-ttu-id="5cdd1-127">código de error de Hola que realmente le ayuda a resolver el problema de hello suele ser un nivel por debajo de este error.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-127">hello error code that actually helps you resolve hello issue is usually one level below this error.</span></span> <span data-ttu-id="5cdd1-128">Por ejemplo, hello siguiente imagen muestra hello **RequestDisallowedByPolicy** código de error que está por debajo del error de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-128">For example, hello following image shows hello **RequestDisallowedByPolicy** error code that is under hello deployment error.</span></span>

![Visualización del código de error](./media/resource-manager-common-deployment-errors/error-code.png)

## <a name="skunotavailable"></a><span data-ttu-id="5cdd1-130">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="5cdd1-130">SkuNotAvailable</span></span>

<span data-ttu-id="5cdd1-131">Al implementar un recurso (normalmente una máquina virtual), puede recibir Hola mensaje de error y de código de error siguiente:</span><span class="sxs-lookup"><span data-stu-id="5cdd1-131">When deploying a resource (typically a virtual machine), you may receive hello following error code and error message:</span></span>

```
Code: SkuNotAvailable
Message: hello requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy tooa different location.
```

<span data-ttu-id="5cdd1-132">Recibirá este error cuando el recurso de hello SKU que seleccionó (por ejemplo, el tamaño de máquina virtual) no está disponible para la ubicación de Hola que seleccionó.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-132">You receive this error when hello resource SKU you have selected (such as VM size) is not available for hello location you have selected.</span></span> <span data-ttu-id="5cdd1-133">tooresolve este problema, necesita toodetermine que SKU están disponibles en una región.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-133">tooresolve this issue, you need toodetermine which SKUs are available in a region.</span></span> <span data-ttu-id="5cdd1-134">También puede usar PowerShell, portal de Hola o un toofind de operación de resto SKU disponibles.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-134">You can use PowerShell, hello portal, or a REST operation toofind available SKUs.</span></span>

- <span data-ttu-id="5cdd1-135">Para PowerShell, use [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) y filtre por ubicación.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-135">For PowerShell, use [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) and filter by location.</span></span> <span data-ttu-id="5cdd1-136">Debe tener la versión más reciente de Hola de PowerShell para este comando.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-136">You must have hello latest version of PowerShell for this command.</span></span>

  ```powershell
  Get-AzureRmComputeResourceSku | where {$_.Locations.Contains("southcentralus")}
  ```

  <span data-ttu-id="5cdd1-137">resultados de Hello incluyen una lista de SKU para la ubicación de Hola y las restricciones para esa SKU.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-137">hello results include a list of SKUs for hello location and any restrictions for that SKU.</span></span>

  ```powershell
  ResourceType                Name      Locations Restriction                      Capability Value
  ------------                ----      --------- -----------                      ---------- -----
  availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
  availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
  virtualMachines      Standard_A0 southcentralus
  virtualMachines      Standard_A1 southcentralus
  virtualMachines      Standard_A2 southcentralus
  ```

- <span data-ttu-id="5cdd1-138">Hola toouse [portal](https://portal.azure.com), inicie sesión en el portal de toohello y agregue un recurso a través de la interfaz de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-138">toouse hello [portal](https://portal.azure.com), log in toohello portal and add a resource through hello interface.</span></span> <span data-ttu-id="5cdd1-139">Cuando se establecen valores de hello, vea Hola SKU disponibles para ese recurso.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-139">As you set hello values, you see hello available SKUs for that resource.</span></span> <span data-ttu-id="5cdd1-140">No es necesario toocomplete implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-140">You do not need toocomplete hello deployment.</span></span>

    ![SKU disponibles](./media/resource-manager-common-deployment-errors/view-sku.png)

- <span data-ttu-id="5cdd1-142">Hola toouse API de REST para máquinas virtuales, enviar Hola después de solicitud:</span><span class="sxs-lookup"><span data-stu-id="5cdd1-142">toouse hello REST API for virtual machines, send hello following request:</span></span>

  ```HTTP 
  GET
  https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
  ```

  <span data-ttu-id="5cdd1-143">Devuelve disponible SKU y regiones en hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="5cdd1-143">It returns available SKUs and regions in hello following format:</span></span>

  ```json
  {
    "value": [
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A0",
        "tier": "Standard",
        "size": "A0",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A1",
        "tier": "Standard",
        "size": "A1",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      ...
    ]
  }    
  ```

<span data-ttu-id="5cdd1-144">Si no se puede toofind una SKU adecuada en dicha región o una región alternativa que satisfaga sus necesidades empresariales, enviar un [solicitud SKU](https://aka.ms/skurestriction) tooAzure soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-144">If you are unable toofind a suitable SKU in that region or an alternative region that meets your business needs, submit a [SKU request](https://aka.ms/skurestriction) tooAzure Support.</span></span>

## <a name="disallowedoperation"></a><span data-ttu-id="5cdd1-145">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="5cdd1-145">DisallowedOperation</span></span>

```
Code: DisallowedOperation
Message: hello current subscription type is not permitted tooperform operations on any provider 
namespace. Please use a different subscription.
```

<span data-ttu-id="5cdd1-146">Si recibe este error, usa una suscripción que no está permitido tooaccess los servicios de Azure que no sea de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-146">If you receive this error, you are using a subscription that is not permitted tooaccess any Azure services other than Azure Active Directory.</span></span> <span data-ttu-id="5cdd1-147">Cuando se necesita el portal clásico de hello tooaccess pero no se permiten toodeploy recursos tendrá este tipo de suscripción.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-147">You might have this type of subscription when you need tooaccess hello classic portal but are not permitted toodeploy resources.</span></span> <span data-ttu-id="5cdd1-148">tooresolve este problema, debe usar una suscripción que disponga de permisos de los recursos toodeploy.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-148">tooresolve this issue, you must use a subscription that has permission toodeploy resources.</span></span>  

<span data-ttu-id="5cdd1-149">tooview las suscripciones disponibles con PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="5cdd1-149">tooview your available subscriptions with PowerShell, use:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="5cdd1-150">Y suscripción actual tooset hello, use:</span><span class="sxs-lookup"><span data-stu-id="5cdd1-150">And, tooset hello current subscription, use:</span></span>

```powershell
Set-AzureRmContext -SubscriptionName {subscription-name}
```

<span data-ttu-id="5cdd1-151">tooview las suscripciones disponibles con CLI de Azure 2.0, use:</span><span class="sxs-lookup"><span data-stu-id="5cdd1-151">tooview your available subscriptions with Azure CLI 2.0, use:</span></span>

```azurecli
az account list
```

<span data-ttu-id="5cdd1-152">Y suscripción actual tooset hello, use:</span><span class="sxs-lookup"><span data-stu-id="5cdd1-152">And, tooset hello current subscription, use:</span></span>

```azurecli
az account set --subscription {subscription-name}
```

## <a name="invalidtemplate"></a><span data-ttu-id="5cdd1-153">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="5cdd1-153">InvalidTemplate</span></span>
<span data-ttu-id="5cdd1-154">Este error puede tener distintos orígenes.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-154">This error can result from several different types of errors.</span></span>

- <span data-ttu-id="5cdd1-155">Error de sintaxis</span><span class="sxs-lookup"><span data-stu-id="5cdd1-155">Syntax error</span></span>

   <span data-ttu-id="5cdd1-156">Si recibe un mensaje de error que indica la validación de la plantilla no se pudo de hello, puede tener un problema de sintaxis en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-156">If you receive an error message that indicates hello template failed validation, you may have a syntax problem in your template.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed
  ```

   <span data-ttu-id="5cdd1-157">Este error es fácil toomake porque las expresiones de plantilla pueden ser complejas.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-157">This error is easy toomake because template expressions can be intricate.</span></span> <span data-ttu-id="5cdd1-158">Por ejemplo, hello siguiente asignación de nombre de una cuenta de almacenamiento contiene un conjunto de corchetes, tres funciones, tres conjuntos de paréntesis, un conjunto de comillas simples y una propiedad:</span><span class="sxs-lookup"><span data-stu-id="5cdd1-158">For example, hello following name assignment for a storage account contains one set of brackets, three functions, three sets of parentheses, one set of single quotes, and one property:</span></span>

  ```json
  "name": "[concat('storage', uniqueString(resourceGroup().id))]",
  ```

   <span data-ttu-id="5cdd1-159">Si no proporciona la sintaxis de coincidencia de hello, plantilla de hello genera un valor que es diferente de su intención.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-159">If you do not provide hello matching syntax, hello template produces a value that is different than your intention.</span></span>

   <span data-ttu-id="5cdd1-160">Cuando reciba este tipo de error, revise cuidadosamente la sintaxis de expresiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-160">When you receive this type of error, carefully review hello expression syntax.</span></span> <span data-ttu-id="5cdd1-161">Considere la posibilidad de utilizar un editor JSON como [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) o [Visual Studio Code](resource-manager-vs-code.md) que puede avisarlo de los errores de sintaxis.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-161">Consider using a JSON editor like [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) or [Visual Studio Code](resource-manager-vs-code.md), which can warn you about syntax errors.</span></span>

- <span data-ttu-id="5cdd1-162">Longitudes de segmentos incorrectas</span><span class="sxs-lookup"><span data-stu-id="5cdd1-162">Incorrect segment lengths</span></span>

   <span data-ttu-id="5cdd1-163">Cuando el nombre del recurso de hello no está en formato correcto de hello, se produce otro error de plantilla no válido.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-163">Another invalid template error occurs when hello resource name is not in hello correct format.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed: 'hello template resource {resource-name}'
  for type {resource-type} has incorrect segment lengths.
  ```

   <span data-ttu-id="5cdd1-164">Un recurso de nivel de raíz debe tener un segmento de menos en nombre de Hola que en el tipo de recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-164">A root level resource must have one less segment in hello name than in hello resource type.</span></span> <span data-ttu-id="5cdd1-165">Cada segmento se distingue por una barra diagonal.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-165">Each segment is differentiated by a slash.</span></span> <span data-ttu-id="5cdd1-166">En el siguiente ejemplo de Hola, tipo de hello tiene dos segmentos y nombre de hello tiene un segmento, por lo que es un **nombre válido**.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-166">In hello following example, hello type has two segments and hello name has one segment, so it is a **valid name**.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="5cdd1-167">Pero es el siguiente ejemplo de Hola **no es un nombre válido** porque tiene Hola tantos segmentos como tipo hello.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-167">But hello next example is **not a valid name** because it has hello same number of segments as hello type.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "appPlan/myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="5cdd1-168">Para obtener recursos secundarios, tipo de Hola y el nombre tienen Hola mismo número de segmentos.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-168">For child resources, hello type and name have hello same number of segments.</span></span> <span data-ttu-id="5cdd1-169">Este número de segmentos tiene sentido porque el nombre completo de Hola y el tipo secundario Hola incluye el tipo y el nombre del elemento primario de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-169">This number of segments makes sense because hello full name and type for hello child includes hello parent name and type.</span></span> <span data-ttu-id="5cdd1-170">Por lo tanto, nombre completo de hello aún tiene un segmento de menos de tipo completo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-170">Therefore, hello full name still has one less segment than hello full type.</span></span>

  ```json
  "resources": [
      {
          "type": "Microsoft.KeyVault/vaults",
          "name": "contosokeyvault",
          ...
          "resources": [
              {
                  "type": "secrets",
                  "name": "appPassword",
                  ...
              }
          ]
      }
  ]
  ```

   <span data-ttu-id="5cdd1-171">Al obtener segmentos Hola derecho pueden ser complicadas con tipos de administrador de recursos que se aplican a través de proveedores de recursos.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-171">Getting hello segments right can be tricky with Resource Manager types that are applied across resource providers.</span></span> <span data-ttu-id="5cdd1-172">Por ejemplo, aplicar un sitio web de recurso bloqueo tooa requiere un tipo con cuatro segmentos.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-172">For example, applying a resource lock tooa web site requires a type with four segments.</span></span> <span data-ttu-id="5cdd1-173">Por lo tanto, el nombre de hello es tres segmentos:</span><span class="sxs-lookup"><span data-stu-id="5cdd1-173">Therefore, hello name is three segments:</span></span>

  ```json
  {
      "type": "Microsoft.Web/sites/providers/locks",
      "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
      ...
  }
  ```

- <span data-ttu-id="5cdd1-174">Copy index is not expected (Índice de copia no esperado)</span><span class="sxs-lookup"><span data-stu-id="5cdd1-174">Copy index is not expected</span></span>

   <span data-ttu-id="5cdd1-175">Esto ocurre **InvalidTemplate** error cuando se haya aplicado hello **copia** tooa parte del elemento de plantilla de Hola que no admite este elemento.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-175">You encounter this **InvalidTemplate** error when you have applied hello **copy** element tooa part of hello template that does not support this element.</span></span> <span data-ttu-id="5cdd1-176">Sólo puede aplicar el tipo de recurso de hello copiar elemento tooa.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-176">You can only apply hello copy element tooa resource type.</span></span> <span data-ttu-id="5cdd1-177">No se puede aplicar copia tooa propiedad dentro de un tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-177">You cannot apply copy tooa property within a resource type.</span></span> <span data-ttu-id="5cdd1-178">Por ejemplo, aplicar copia tooa virtual machine, pero no se puede aplicar toohello OS discos para una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-178">For example, you apply copy tooa virtual machine, but you cannot apply it toohello OS disks for a virtual machine.</span></span> <span data-ttu-id="5cdd1-179">En algunos casos, puede convertir un recurso de primario de secundarios recursos tooa toocreate un bucle de copia.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-179">In some cases, you can convert a child resource tooa parent resource toocreate a copy loop.</span></span> <span data-ttu-id="5cdd1-180">Para más información sobre cómo usar este elemento, consulte [Creación de varias instancias de recursos en Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="5cdd1-180">For more information about using copy, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

- <span data-ttu-id="5cdd1-181">El parámetro no es válido</span><span class="sxs-lookup"><span data-stu-id="5cdd1-181">Parameter is not valid</span></span>

   <span data-ttu-id="5cdd1-182">Si plantilla Hola especifica los valores permitidos para un parámetro y proporciona un valor que no es uno de esos valores, recibirá un toohello similar de mensaje siguiente error:</span><span class="sxs-lookup"><span data-stu-id="5cdd1-182">If hello template specifies permitted values for a parameter, and you provide a value that is not one of those values, you receive a message similar toohello following error:</span></span>

  ```
  Code=InvalidTemplate;
  Message=Deployment template validation failed: 'hello provided value {parameter value}
  for hello template parameter {parameter name} is not valid. hello parameter value is not
  part of hello allowed values
  ``` 

   <span data-ttu-id="5cdd1-183">Vuelve a revisar Hola valores permitidos en la plantilla de Hola y proporcionar una durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-183">Double check hello allowed values in hello template, and provide one during deployment.</span></span>

- <span data-ttu-id="5cdd1-184">Se detectó una dependencia circular</span><span class="sxs-lookup"><span data-stu-id="5cdd1-184">Circular dependency detected</span></span>

   <span data-ttu-id="5cdd1-185">Recibirá este error cuando recursos dependen de ellos de forma que impide la implementación de Hola se inicie.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-185">You receive this error when resources depend on each other in a way that prevents hello deployment from starting.</span></span> <span data-ttu-id="5cdd1-186">Una combinación de interdependencias hace que dos o más recursos esperen otros recursos que también están esperando.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-186">A combination of interdependencies makes two or more resource wait for other resources that are also waiting.</span></span> <span data-ttu-id="5cdd1-187">Por ejemplo, resource1 depende de resource3, resource2 depende de resource1 y resource3 depende de resource2.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-187">For example, resource1 depends on resource3, resource2 depends on resource1, and resource3 depends on resource2.</span></span> <span data-ttu-id="5cdd1-188">Para resolver este problema, normalmente se eliminan las dependencias innecesarias.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-188">You can usually solve this problem by removing unnecessary dependencies.</span></span> 

<a id="notfound" />
### <a name="notfound-and-resourcenotfound"></a><span data-ttu-id="5cdd1-189">NotFound y ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="5cdd1-189">NotFound and ResourceNotFound</span></span>
<span data-ttu-id="5cdd1-190">Cuando la plantilla incluye nombre Hola de un recurso que no se puede resolver, recibirá un error similar al:</span><span class="sxs-lookup"><span data-stu-id="5cdd1-190">When your template includes hello name of a resource that cannot be resolved, you receive an error similar to:</span></span>

```
Code=NotFound;
Message=Cannot find ServerFarm with name exampleplan.
```

<span data-ttu-id="5cdd1-191">Si estás intentando hello toodeploy falta el recurso de plantilla de hello, compruebe si tiene una dependencia de tooadd.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-191">If you are attempting toodeploy hello missing resource in hello template, check whether you need tooadd a dependency.</span></span> <span data-ttu-id="5cdd1-192">Cuando es posible, Resource Manager optimiza la implementación mediante la creación de recursos en paralelo.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-192">Resource Manager optimizes deployment by creating resources in parallel, when possible.</span></span> <span data-ttu-id="5cdd1-193">Si un recurso se debe implementar después de otro recurso, necesita hello toouse **dependsOn** Hola de elemento en su toocreate plantilla una dependencia en otro recurso.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-193">If one resource must be deployed after another resource, you need toouse hello **dependsOn** element in your template toocreate a dependency on hello other resource.</span></span> <span data-ttu-id="5cdd1-194">Por ejemplo, al implementar una aplicación web, debe existir Hola plan de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-194">For example, when deploying a web app, hello App Service plan must exist.</span></span> <span data-ttu-id="5cdd1-195">Si no ha especificado Hola plan de servicio de aplicaciones depende de dicha aplicación Hola, Administrador de recursos crea los recursos en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-195">If you have not specified that hello web app depends on hello App Service plan, Resource Manager creates both resources at hello same time.</span></span> <span data-ttu-id="5cdd1-196">Recibirá un error que indica que hello no se encuentra el recurso de plan de servicio de aplicaciones, porque no existe todavía al intentar tooset una propiedad en la aplicación web de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-196">You receive an error stating that hello App Service plan resource cannot be found, because it does not exist yet when attempting tooset a property on hello web app.</span></span> <span data-ttu-id="5cdd1-197">Evitar este error estableciendo la dependencia de hello en hello web app.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-197">You prevent this error by setting hello dependency in hello web app.</span></span>

```json
{
  "apiVersion": "2015-08-01",
  "type": "Microsoft.Web/sites",
  "dependsOn": [
    "[variables('hostingPlanName')]"
  ],
  ...
}
```

<span data-ttu-id="5cdd1-198">Para obtener sugerencias sobre cómo solucionar los errores de dependencia, consulte [Comprobación de la secuencia de implementación](#check-deployment-sequence).</span><span class="sxs-lookup"><span data-stu-id="5cdd1-198">For suggestions on troubleshooting dependency errors, see [Check deployment sequence](#check-deployment-sequence).</span></span>

<span data-ttu-id="5cdd1-199">También verá este error al recurso de hello existe en otro grupo de recursos que Hola uno está implementando en el.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-199">You also see this error when hello resource exists in a different resource group than hello one being deployed to.</span></span> <span data-ttu-id="5cdd1-200">En ese caso, use hello [función resourceId](resource-group-template-functions-resource.md#resourceid) nombre completo de hello tooget del recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-200">In that case, use hello [resourceId function](resource-group-template-functions-resource.md#resourceid) tooget hello fully qualified name of hello resource.</span></span>

```json
"properties": {
    "name": "[parameters('siteName')]",
    "serverFarmId": "[resourceId('plangroup', 'Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
}
```

<span data-ttu-id="5cdd1-201">Si intentas hello toouse [referencia](resource-group-template-functions-resource.md#reference) o [listKeys](resource-group-template-functions-resource.md#listkeys) funciones con un recurso que no se puede resolver, recibirá Hola siguiente error:</span><span class="sxs-lookup"><span data-stu-id="5cdd1-201">If you attempt toouse hello [reference](resource-group-template-functions-resource.md#reference) or [listKeys](resource-group-template-functions-resource.md#listkeys) functions with a resource that cannot be resolved, you receive hello following error:</span></span>

```
Code=ResourceNotFound;
Message=hello Resource 'Microsoft.Storage/storageAccounts/{storage name}' under resource
group {resource group name} was not found.
```

<span data-ttu-id="5cdd1-202">Busque una expresión que incluya hello **referencia** función.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-202">Look for an expression that includes hello **reference** function.</span></span> <span data-ttu-id="5cdd1-203">Compruebe que los valores de parámetro hello son correctos.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-203">Double check that hello parameter values are correct.</span></span>

## <a name="parentresourcenotfound"></a><span data-ttu-id="5cdd1-204">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="5cdd1-204">ParentResourceNotFound</span></span>

<span data-ttu-id="5cdd1-205">Cuando un recurso es un recurso de tooanother primario, recurso primario de hello debe existir antes de crear el recurso de hello secundario.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-205">When one resource is a parent tooanother resource, hello parent resource must exist before creating hello child resource.</span></span> <span data-ttu-id="5cdd1-206">Si aún no existe, recibirá Hola siguiente error:</span><span class="sxs-lookup"><span data-stu-id="5cdd1-206">If it does not yet exist, you receive hello following error:</span></span>

```
Code=ParentResourceNotFound;
Message=Can not perform requested operation on nested resource. Parent resource 'exampleserver' not found."
```

<span data-ttu-id="5cdd1-207">Hola nombre de recurso de hello secundario incluye Hola primario.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-207">hello name of hello child resource includes hello parent name.</span></span> <span data-ttu-id="5cdd1-208">Por ejemplo, se podría definir una base de datos SQL como:</span><span class="sxs-lookup"><span data-stu-id="5cdd1-208">For example, a SQL Database might be defined as:</span></span>

```json
{
  "type": "Microsoft.Sql/servers/databases",
  "name": "[concat(variables('databaseServerName'), '/', parameters('databaseName'))]",
  ...
```

<span data-ttu-id="5cdd1-209">Sin embargo, si no especifica una dependencia en el recurso primario de hello, pueden obtener implementar recursos secundarios de hello antes que la primaria Hola.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-209">But, if you do not specify a dependency on hello parent resource, hello child resource may get deployed before hello parent.</span></span> <span data-ttu-id="5cdd1-210">tooresolve este error incluyen una dependencia.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-210">tooresolve this error, include a dependency.</span></span>

```json
"dependsOn": [
    "[variables('databaseServerName')]"
]
```

<a id="storagenamenotunique" />

## <a name="storageaccountalreadyexists-and-storageaccountalreadytaken"></a><span data-ttu-id="5cdd1-211">StorageAccountAlreadyExists y StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="5cdd1-211">StorageAccountAlreadyExists and StorageAccountAlreadyTaken</span></span>
<span data-ttu-id="5cdd1-212">Las cuentas de almacenamiento, debe proporcionar un nombre para el recurso de Hola que es único en Azure.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-212">For storage accounts, you must provide a name for hello resource that is unique across Azure.</span></span> <span data-ttu-id="5cdd1-213">Si no lo hace, recibirá un error como el siguiente:</span><span class="sxs-lookup"><span data-stu-id="5cdd1-213">If you do not provide a unique name, you receive an error like:</span></span>

```
Code=StorageAccountAlreadyTaken
Message=hello storage account named mystorage is already taken.
```

<span data-ttu-id="5cdd1-214">Puede crear un nombre único mediante la concatenación de la convención de nomenclatura con el resultado de hello de hello [uniqueString](resource-group-template-functions-string.md#uniquestring) (función).</span><span class="sxs-lookup"><span data-stu-id="5cdd1-214">You can create a unique name by concatenating your naming convention with hello result of hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span>

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

<span data-ttu-id="5cdd1-215">Si implementa una cuenta de almacenamiento con hello el mismo nombre como una cuenta de almacenamiento existente en su suscripción, pero proporciona una ubicación diferente, recibirá un error en la cuenta de almacenamiento de Hola que indica que ya existe en una ubicación diferente.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-215">If you deploy a storage account with hello same name as an existing storage account in your subscription, but provide a different location, you receive an error indicating hello storage account already exists in a different location.</span></span> <span data-ttu-id="5cdd1-216">Elimine la cuenta de almacenamiento existente de hello, o proporcione Hola misma ubicación como Hola cuenta de almacenamiento existente.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-216">Either delete hello existing storage account, or provide hello same location as hello existing storage account.</span></span>

## <a name="accountnameinvalid"></a><span data-ttu-id="5cdd1-217">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="5cdd1-217">AccountNameInvalid</span></span>
<span data-ttu-id="5cdd1-218">Vea hello **AccountNameInvalid** error al intentar toogive un almacenamiento cuenta un nombre que incluya caracteres prohibidos.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-218">You see hello **AccountNameInvalid** error when attempting toogive a storage account a name that includes prohibited characters.</span></span> <span data-ttu-id="5cdd1-219">Los nombres de cuentas de almacenamiento deben tener entre 3 y 24 caracteres, y usar solo números y letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-219">Storage account names must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span> <span data-ttu-id="5cdd1-220">Hola [uniqueString](resource-group-template-functions-string.md#uniquestring) función devuelve 13 caracteres.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-220">hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function returns 13 characters.</span></span> <span data-ttu-id="5cdd1-221">Si concatenar un prefijo toohello **uniqueString** como resultado, proporcione un prefijo que es de 11 caracteres o menos.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-221">If you concatenate a prefix toohello **uniqueString** result, provide a prefix that is 11 characters or less.</span></span>

## <a name="badrequest"></a><span data-ttu-id="5cdd1-222">BadRequest</span><span class="sxs-lookup"><span data-stu-id="5cdd1-222">BadRequest</span></span>

<span data-ttu-id="5cdd1-223">Puede encontrar un estado BadRequest al proporcionar un valor no válido para una propiedad.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-223">You may encounter a BadRequest status when you provide an invalid value for a property.</span></span> <span data-ttu-id="5cdd1-224">Por ejemplo, si proporciona un valor incorrecto de SKU para una cuenta de almacenamiento, se produce un error en implementación Hola.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-224">For example, if you provide an incorrect SKU value for a storage account, hello deployment fails.</span></span> <span data-ttu-id="5cdd1-225">toodetermine los valores válidos para la propiedad, mire hello [API de REST](/rest/api) para tipo de recurso de Hola que va a implementar.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-225">toodetermine valid values for property, look at hello [REST API](/rest/api) for hello resource type you are deploying.</span></span>

<a id="noregisteredproviderfound" />

## <a name="noregisteredproviderfound-and-missingsubscriptionregistration"></a><span data-ttu-id="5cdd1-226">NoRegisteredProviderFound y MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="5cdd1-226">NoRegisteredProviderFound and MissingSubscriptionRegistration</span></span>
<span data-ttu-id="5cdd1-227">Al implementar el recurso, puede recibir Hola siguiente código de error y de mensajes:</span><span class="sxs-lookup"><span data-stu-id="5cdd1-227">When deploying resource, you may receive hello following error code and message:</span></span>

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

<span data-ttu-id="5cdd1-228">O bien, puede recibir un mensaje similar que indica:</span><span class="sxs-lookup"><span data-stu-id="5cdd1-228">Or, you may receive a similar message that states:</span></span>

```
Code: MissingSubscriptionRegistration
Message: hello subscription is not registered toouse namespace {resource-provider-namespace}
```

<span data-ttu-id="5cdd1-229">Recibirá estos errores por uno de estos tres motivos:</span><span class="sxs-lookup"><span data-stu-id="5cdd1-229">You receive these errors for one of three reasons:</span></span>

1. <span data-ttu-id="5cdd1-230">no se ha registrado el proveedor de recursos de Hello para la suscripción</span><span class="sxs-lookup"><span data-stu-id="5cdd1-230">hello resource provider has not been registered for your subscription</span></span>
2. <span data-ttu-id="5cdd1-231">Versión de API que no se admite para el tipo de recurso de Hola</span><span class="sxs-lookup"><span data-stu-id="5cdd1-231">API version not supported for hello resource type</span></span>
3. <span data-ttu-id="5cdd1-232">No se admite para el tipo de recurso de Hola de ubicación</span><span class="sxs-lookup"><span data-stu-id="5cdd1-232">Location not supported for hello resource type</span></span>

<span data-ttu-id="5cdd1-233">mensaje de error de Hello debe proporcionarle sugerencias para ubicaciones de hello compatible y versiones de API.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-233">hello error message should give you suggestions for hello supported locations and API versions.</span></span> <span data-ttu-id="5cdd1-234">Puede cambiar su tooone plantilla de hello valores sugeridos.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-234">You can change your template tooone of hello suggested values.</span></span> <span data-ttu-id="5cdd1-235">Mayoría de los proveedores se registra automáticamente por hello Azure interfaz de línea de comandos de portal o hello usa, pero no todas.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-235">Most providers are registered automatically by hello Azure portal or hello command-line interface you are using, but not all.</span></span> <span data-ttu-id="5cdd1-236">Si no ha utilizado un proveedor de recursos determinado antes, deberá tooregister ese proveedor.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-236">If you have not used a particular resource provider before, you may need tooregister that provider.</span></span> <span data-ttu-id="5cdd1-237">Puede obtener más información sobre los proveedores de recursos a través de PowerShell o la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-237">You can discover more about resource providers through PowerShell or Azure CLI.</span></span>

<span data-ttu-id="5cdd1-238">**Portal**</span><span class="sxs-lookup"><span data-stu-id="5cdd1-238">**Portal**</span></span>

<span data-ttu-id="5cdd1-239">Puede ver el estado de registro de hello y registrar un espacio de nombres de proveedor de recursos a través del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-239">You can see hello registration status and register a resource provider namespace through hello portal.</span></span>

1. <span data-ttu-id="5cdd1-240">Para la suscripción, seleccione **Proveedores de recursos**.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-240">For your subscription, select **Resource providers**.</span></span>

   ![seleccionar proveedores de recursos](./media/resource-manager-common-deployment-errors/select-resource-provider.png)

2. <span data-ttu-id="5cdd1-242">Mire Hola lista de proveedores de recursos y, si es necesario, seleccione hello **registrar** proveedor de recursos de vínculo tooregister Hola de tipo hello que estamos toodeploy.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-242">Look at hello list of resource providers, and if necessary, select hello **Register** link tooregister hello resource provider of hello type you are trying toodeploy.</span></span>

   ![Enumeración de proveedores de recursos](./media/resource-manager-common-deployment-errors/list-resource-providers.png)

<span data-ttu-id="5cdd1-244">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="5cdd1-244">**PowerShell**</span></span>

<span data-ttu-id="5cdd1-245">toosee el estado de registro, use **AzureRmResourceProvider Get**.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-245">toosee your registration status, use **Get-AzureRmResourceProvider**.</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

<span data-ttu-id="5cdd1-246">tooregister un proveedor, utilice **AzureRmResourceProvider Register** y proporcione el nombre de Hola de proveedor de recursos de hello desea tooregister.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-246">tooregister a provider, use **Register-AzureRmResourceProvider** and provide hello name of hello resource provider you wish tooregister.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

<span data-ttu-id="5cdd1-247">ubicaciones de hello admite tooget para un determinado tipo de recurso, use:</span><span class="sxs-lookup"><span data-stu-id="5cdd1-247">tooget hello supported locations for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="5cdd1-248">Hola tooget admite versiones de API para un determinado tipo de recurso, use:</span><span class="sxs-lookup"><span data-stu-id="5cdd1-248">tooget hello supported API versions for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

<span data-ttu-id="5cdd1-249">**CLI de Azure**</span><span class="sxs-lookup"><span data-stu-id="5cdd1-249">**Azure CLI**</span></span>

<span data-ttu-id="5cdd1-250">toosee si se registra el proveedor de hello, usar hello `azure provider list` comando.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-250">toosee whether hello provider is registered, use hello `azure provider list` command.</span></span>

```azurecli
az provider list
```

<span data-ttu-id="5cdd1-251">tooregister un proveedor de recursos, utilice hello `azure provider register` comando y especifique hello *espacio de nombres* tooregister.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-251">tooregister a resource provider, use hello `azure provider register` command, and specify hello *namespace* tooregister.</span></span>

```azurecli
az provider register --namespace Microsoft.Cdn
```

<span data-ttu-id="5cdd1-252">ubicaciones de hello admite toosee y versiones de API para un tipo de recurso, use:</span><span class="sxs-lookup"><span data-stu-id="5cdd1-252">toosee hello supported locations and API versions for a resource type, use:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

<a id="quotaexceeded" />

## <a name="quotaexceeded-and-operationnotallowed"></a><span data-ttu-id="5cdd1-253">QuotaExceeded y OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="5cdd1-253">QuotaExceeded and OperationNotAllowed</span></span>
<span data-ttu-id="5cdd1-254">Podría tener problemas cuando una implementación supera una cuota, lo que podría suceder por grupo de recursos, suscripciones, cuentas y otros ámbitos.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-254">You might have issues when deployment exceeds a quota, which could be per resource group, subscriptions, accounts, and other scopes.</span></span> <span data-ttu-id="5cdd1-255">Por ejemplo, puede ser su suscripción configurado toolimit Hola número de núcleos de una región.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-255">For example, your subscription may be configured toolimit hello number of cores for a region.</span></span> <span data-ttu-id="5cdd1-256">Si intentas toodeploy una máquina virtual con más núcleos que permiten la cantidad de hello, recibirá un error que se superó la cuota de Hola que indica.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-256">If you attempt toodeploy a virtual machine with more cores than hello permitted amount, you receive an error stating hello quota has been exceeded.</span></span>
<span data-ttu-id="5cdd1-257">Para obtener información completa de las cuotas, consulte [Límites, cuotas y restricciones de suscripción y servicios de Microsoft Azure](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="5cdd1-257">For complete quota information, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="5cdd1-258">tooexamine las cuotas de suscripción para núcleos, puede usar hello `azure vm list-usage` comando hello CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-258">tooexamine your subscription's quotas for cores, you can use hello `azure vm list-usage` command in hello Azure CLI.</span></span> <span data-ttu-id="5cdd1-259">Hola de ejemplo siguiente muestra esa cuota de núcleos de Hola para una cuenta de evaluación gratuita es 4:</span><span class="sxs-lookup"><span data-stu-id="5cdd1-259">hello following example illustrates that hello core quota for a free trial account is 4:</span></span>

```azurecli
az vm list-usage --location "South Central US"
```

<span data-ttu-id="5cdd1-260">Que devuelve:</span><span class="sxs-lookup"><span data-stu-id="5cdd1-260">Which returns:</span></span>

```azurecli
[
  {
    "currentValue": 0,
    "limit": 2000,
    "name": {
      "localizedValue": "Availability Sets",
      "value": "availabilitySets"
    }
  },
  ...
]
```

<span data-ttu-id="5cdd1-261">Si implementa una plantilla que crea más de cuatro núcleos en la región del oeste de Estados Unidos de hello, obtendrá un error de implementación que el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="5cdd1-261">If you deploy a template that creates more than four cores in hello West US region, you get a deployment error that looks like:</span></span>

```
Code=OperationNotAllowed
Message=Operation results in exceeding quota limits of Core.
Maximum allowed: 4, Current in use: 4, Additional requested: 2.
```

<span data-ttu-id="5cdd1-262">O bien en PowerShell, puede usar hello **AzureRmVMUsage Get** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-262">Or in PowerShell, you can use hello **Get-AzureRmVMUsage** cmdlet.</span></span>

```powershell
Get-AzureRmVMUsage
```

<span data-ttu-id="5cdd1-263">Que devuelve:</span><span class="sxs-lookup"><span data-stu-id="5cdd1-263">Which returns:</span></span>

```powershell
...
CurrentValue : 0
Limit        : 4
Name         : {
                 "value": "cores",
                 "localizedValue": "Total Regional Cores"
               }
Unit         : null
...
```

<span data-ttu-id="5cdd1-264">En estos casos, debe ir toohello portal y archivo un tooraise de problema de soporte técnico de su cuota de región de hello en el que desea toodeploy.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-264">In these cases, you should go toohello portal and file a support issue tooraise your quota for hello region into which you want toodeploy.</span></span>

> [!NOTE]
> <span data-ttu-id="5cdd1-265">Recuerde que para los grupos de recursos, cuota de hello es para cada región individual, no para la suscripción completa de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-265">Remember that for resource groups, hello quota is for each individual region, not for hello entire subscription.</span></span> <span data-ttu-id="5cdd1-266">Si necesita toodeploy 30 núcleos zona horaria del Pacífico occidental, deberá tooask para 30 núcleos de administrador de recursos zona horaria del Pacífico occidental.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-266">If you need toodeploy 30 cores in West US, you have tooask for 30 Resource Manager cores in West US.</span></span> <span data-ttu-id="5cdd1-267">Si necesita toodeploy 30 núcleos en cualquiera de hello regiones toowhich tiene acceso, deberá solicitar 30 núcleos de administrador de recursos en todas las regiones.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-267">If you need toodeploy 30 cores in any of hello regions toowhich you have access, you should ask for 30 Resource Manager cores in all regions.</span></span>
>
>

## <a name="invalidcontentlink"></a><span data-ttu-id="5cdd1-268">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="5cdd1-268">InvalidContentLink</span></span>
<span data-ttu-id="5cdd1-269">Cuando reciba mensajes de bienvenida del error:</span><span class="sxs-lookup"><span data-stu-id="5cdd1-269">When you receive hello error message:</span></span>

```
Code=InvalidContentLink
Message=Unable toodownload deployment content from ...
```

<span data-ttu-id="5cdd1-270">Probablemente ha intentado toolink tooa plantillas anidadas que no está disponible.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-270">You have most likely attempted toolink tooa nested template that is not available.</span></span> <span data-ttu-id="5cdd1-271">Vuelve a revisar hello URI proporcionado para plantillas anidadas Hola.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-271">Double check hello URI you provided for hello nested template.</span></span> <span data-ttu-id="5cdd1-272">Si existe en la plantilla de hello en una cuenta de almacenamiento, asegúrese de hello URI es accesible.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-272">If hello template exists in a storage account, make sure hello URI is accessible.</span></span> <span data-ttu-id="5cdd1-273">Puede que necesite toopass un token de SAS.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-273">You may need toopass a SAS token.</span></span> <span data-ttu-id="5cdd1-274">Para más información, consulte [Uso de plantillas vinculadas con el Administrador de recursos de Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5cdd1-274">For more information, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="requestdisallowedbypolicy"></a><span data-ttu-id="5cdd1-275">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="5cdd1-275">RequestDisallowedByPolicy</span></span>
<span data-ttu-id="5cdd1-276">Recibirá este error cuando la suscripción incluye una directiva de recursos que impide que una acción que está intentando tooperform durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-276">You receive this error when your subscription includes a resource policy that prevents an action you are trying tooperform during deployment.</span></span> <span data-ttu-id="5cdd1-277">En el mensaje de error de hello, busque el identificador de directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-277">In hello error message, look for hello policy identifier.</span></span>

```
Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'
```

<span data-ttu-id="5cdd1-278">En **PowerShell**, proporcionar ese identificador de directiva como hello **identificador** detalles del parámetro tooretrieve acerca de la directiva de Hola que bloquea la implementación.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-278">In **PowerShell**, provide that policy identifier as hello **Id** parameter tooretrieve details about hello policy that blocked your deployment.</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

<span data-ttu-id="5cdd1-279">En **Azure CLI**, proporcione Hola nombre de definición de directiva de hello:</span><span class="sxs-lookup"><span data-stu-id="5cdd1-279">In **Azure CLI**, provide hello name of hello policy definition:</span></span>

```azurecli
az policy definition show --name regionPolicyAssignment
```

<span data-ttu-id="5cdd1-280">Para obtener más información, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="5cdd1-280">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="5cdd1-281">Error RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="5cdd1-281">RequestDisallowedByPolicy error</span></span>](resource-manager-policy-requestdisallowedbypolicy-error.md)
- <span data-ttu-id="5cdd1-282">[Usar Directiva toomanage recursos y controlar el acceso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="5cdd1-282">[Use Policy toomanage resources and control access](resource-manager-policy.md).</span></span>

## <a name="authorization-failed"></a><span data-ttu-id="5cdd1-283">Error de autorización</span><span class="sxs-lookup"><span data-stu-id="5cdd1-283">Authorization failed</span></span>
<span data-ttu-id="5cdd1-284">Puede recibir un error durante la implementación porque hello cuenta o intentar recursos de hello toodeploy entidad de servicio no tiene acceso tooperform esas acciones.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-284">You may receive an error during deployment because hello account or service principal attempting toodeploy hello resources does not have access tooperform those actions.</span></span> <span data-ttu-id="5cdd1-285">Azure Active Directory permite a usted o su toocontrol administrador qué identidades pueden tener acceso a los recursos con un alto grado de precisión.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-285">Azure Active Directory enables you or your administrator toocontrol which identities can access what resources with a great degree of precision.</span></span> <span data-ttu-id="5cdd1-286">Por ejemplo, si su cuenta se asigna el rol de lector toohello, no está toocreate capaz de recursos.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-286">For example, if your account is assigned toohello Reader role, you are not able toocreate resources.</span></span> <span data-ttu-id="5cdd1-287">En ese caso, debería ver un mensaje de error que indica que hubo un error de autorización.</span><span class="sxs-lookup"><span data-stu-id="5cdd1-287">In that case, you see an error message indicating that authorization failed.</span></span>

<span data-ttu-id="5cdd1-288">Para más información sobre el control de acceso basado en roles, consulte [Control de acceso basado en roles de Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="5cdd1-288">For more information about role-based access control, see [Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="5cdd1-289">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5cdd1-289">Next steps</span></span>
* <span data-ttu-id="5cdd1-290">toolearn acerca de la auditoría de acciones, vea [auditoría de las operaciones con el Administrador de recursos](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="5cdd1-290">toolearn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="5cdd1-291">toolearn acerca de los errores de hello toodetermine de acciones durante la implementación, consulte [ver las operaciones de implementación](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="5cdd1-291">toolearn about actions toodetermine hello errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
