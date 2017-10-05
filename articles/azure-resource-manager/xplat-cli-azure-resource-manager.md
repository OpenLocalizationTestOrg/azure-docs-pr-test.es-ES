---
title: "Administración de recursos con la CLI de Azure | Microsoft Docs"
description: "Utilice la interfaz de línea de comandos (CLI) de Azure para administrar recursos y grupos de Azure"
editor: 
manager: timlt
documentationcenter: 
author: tfitzmac
services: azure-resource-manager
ms.assetid: bb0af466-4f65-4559-ac3a-43985fa096ff
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: tomfitz
ms.openlocfilehash: 3ad4e68b90979fd7f9d3ddf5278e65e19cb07152
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-azure-cli-to-manage-azure-resources-and-resource-groups"></a><span data-ttu-id="e2ac9-103">Uso de la CLI de Azure para administrar los recursos y grupos de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="e2ac9-103">Use the Azure CLI to manage Azure resources and resource groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e2ac9-104">Portal</span><span class="sxs-lookup"><span data-stu-id="e2ac9-104">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="e2ac9-105">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="e2ac9-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="e2ac9-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2ac9-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="e2ac9-107">API DE REST</span><span class="sxs-lookup"><span data-stu-id="e2ac9-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="e2ac9-108">La interfaz de línea de comandos de Azure (CLI de Azure) es una de las diversas herramientas que puede usar para implementar y administrar recursos con Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-108">The Azure Command-Line Interface (Azure CLI) is one of several tools you can use to deploy and manage resources with Resource Manager.</span></span> <span data-ttu-id="e2ac9-109">En este artículo se describen formas habituales de administrar los recursos y los grupos de recursos de Azure con la CLI de Azure en el modo Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-109">This article introduces common ways to manage Azure resources and resource groups by using the Azure CLI in Resource Manager mode.</span></span> <span data-ttu-id="e2ac9-110">Para información sobre el uso de la CLI para implementar recursos, consulte [Implementación de recursos con plantillas de Azure Resource Manager y la CLI de Azure](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="e2ac9-110">For information about using the CLI to deploy resources, see [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> <span data-ttu-id="e2ac9-111">Para información sobre el Administrador de recursos de Azure, consulte [Información general de Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e2ac9-111">For background about Azure resources and Resource Manager, visit the [Azure Resource Manager Overview](resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e2ac9-112">Para administrar recursos de Azure con la CLI de Azure, necesitará [instalar la CLI de Azure](../cli-install-nodejs.md) e [iniciar sesión en Azure](../xplat-cli-connect.md) mediante el comando `azure login`.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-112">To manage Azure resources with the Azure CLI, you need to [install the Azure CLI](../cli-install-nodejs.md), and [log in to Azure](../xplat-cli-connect.md) by using the `azure login` command.</span></span> <span data-ttu-id="e2ac9-113">Asegúrese de que la CLI está en modo de Resource Manager (ejecute `azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="e2ac9-113">Make sure the CLI is in Resource Manager mode (run `azure config mode arm`).</span></span> <span data-ttu-id="e2ac9-114">Si ha realizado estas acciones, ya está preparado para comenzar.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-114">If you've done these things, you're ready to go.</span></span>
> 
> 

## <a name="get-resource-groups-and-resources"></a><span data-ttu-id="e2ac9-115">Obtención de recursos y grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="e2ac9-115">Get resource groups and resources</span></span>
### <a name="resource-groups"></a><span data-ttu-id="e2ac9-116">Grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="e2ac9-116">Resource groups</span></span>
<span data-ttu-id="e2ac9-117">Para obtener una lista de todos los grupos de recursos de la suscripción y sus ubicaciones, ejecute este comando.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-117">To get a list of all resource groups in your subscription and their locations, run this command.</span></span>

    azure group list


### <a name="resources"></a><span data-ttu-id="e2ac9-118">Recursos</span><span class="sxs-lookup"><span data-stu-id="e2ac9-118">Resources</span></span>
 <span data-ttu-id="e2ac9-119">Para ver todos los recursos de un grupo, como el denominado *testRG*, utilice el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="e2ac9-119">To list all resources in a group, such as one with name *testRG*, use the following command:</span></span>

    azure resource list testRG

<span data-ttu-id="e2ac9-120">Para ver un recurso individual dentro del grupo, como la máquina virtual denominada *MyUbuntuVM*, use un comando similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="e2ac9-120">To view an individual resource within the group, such as a VM named *MyUbuntuVM*, use a command like the following:</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="e2ac9-121">Observe el parámetro **Microsoft.Compute/virtualMachines**.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-121">Notice the **Microsoft.Compute/virtualMachines** parameter.</span></span> <span data-ttu-id="e2ac9-122">Este parámetro indica el tipo del recurso sobre el que solicita información.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-122">This parameter indicates the type of the resource you are requesting information on.</span></span>

> [!NOTE]
> <span data-ttu-id="e2ac9-123">Cuando use los comandos **azure resource** distintos del comando **list**, debe especificar la versión de API del recursos con el parámetro **-o**.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-123">When using the **azure resource** commands other than the **list** command, you must specify the API version of the resource with the **-o** parameter.</span></span> <span data-ttu-id="e2ac9-124">Si no está seguro sobre la versión de API, consulte el archivo de plantilla y busque el campo apiVersion correspondiente al recurso.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-124">If you're unsure about the API version, consult the template file and find the apiVersion field for the resource.</span></span> <span data-ttu-id="e2ac9-125">Para más información acerca de las versiones de API de Resource Manager, vea [Tipos y proveedores de recursos](resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="e2ac9-125">For more about API versions in Resource Manager, see [Resource providers and types](resource-manager-supported-services.md).</span></span>
> 
> 

<span data-ttu-id="e2ac9-126">Cuando se consultan los detalles de un recurso, generalmente resulta útil usar el parámetro `--json`.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-126">When viewing details on a resource, it is often useful to use the `--json` parameter.</span></span> <span data-ttu-id="e2ac9-127">Este parámetro hace que el resultado sea más legible, ya que algunos valores son estructuras anidadas o colecciones.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-127">This parameter makes the output more readable, because some values are nested structures, or collections.</span></span> <span data-ttu-id="e2ac9-128">El siguiente ejemplo demuestra los resultados obtenidos con el comando **show** como un documento JSON.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-128">The following example demonstrates returning the results of the **show** command as a JSON document.</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json

> [!NOTE]
> <span data-ttu-id="e2ac9-129">Si lo desea, guarde los datos JSON en un archivo con el carácter &gt; para dirigir la salida a un archivo.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-129">If you want, save the JSON data to file by using the &gt; character to direct the output to a file.</span></span> <span data-ttu-id="e2ac9-130">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e2ac9-130">For example:</span></span>
> 
> `azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json > myfile.json`
> 
> 

### <a name="tags"></a><span data-ttu-id="e2ac9-131">Etiquetas</span><span class="sxs-lookup"><span data-stu-id="e2ac9-131">Tags</span></span>
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="manage-resources"></a><span data-ttu-id="e2ac9-132">Administración de recursos</span><span class="sxs-lookup"><span data-stu-id="e2ac9-132">Manage resources</span></span>
<span data-ttu-id="e2ac9-133">Para agregar un recurso como una cuenta de almacenamiento a un grupo de recursos, ejecute un comando similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="e2ac9-133">To add a resource such as a storage account to a resource group, run a command similar to:</span></span>

    azure resource create testRG MyStorageAccount "Microsoft.Storage/storageAccounts" "westus" -o "2015-06-15" -p "{\"accountType\": \"Standard_LRS\"}"

<span data-ttu-id="e2ac9-134">Además de especificar la versión de API del recurso con el parámetro **-o**, use el parámetro **-p** que pasa una cadena con formato JSON con cualquier propiedad necesaria o adicional.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-134">In addition to specifying the API version of the resource with the **-o** parameter, use the **-p** parameter to pass a JSON-formatted string with any required or additional properties.</span></span>

<span data-ttu-id="e2ac9-135">Para eliminar un recurso existente, como un recurso de máquina virtual, use un comando como el siguiente:</span><span class="sxs-lookup"><span data-stu-id="e2ac9-135">To delete an existing resource such as a virtual machine resource, use a command like the following:</span></span>

    azure resource delete testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="e2ac9-136">Para trasladar recursos existentes a otro grupo de recursos o a otra suscripción, use el comando **azure resource move**.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-136">To move existing resources to another resource group or subscription, use the **azure resource move** command.</span></span> <span data-ttu-id="e2ac9-137">En el siguiente ejemplo se muestra cómo trasladar una Caché de Redis a un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-137">The following example shows how to move a Redis Cache to a new resource group.</span></span> <span data-ttu-id="e2ac9-138">En el parámetro **-i**, ofrezca una lista separada por comas del identificador de recurso que se va a trasladar.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-138">In the **-i** parameter, provide a comma-separated list of the resource id's to move.</span></span>

    azure resource move -i "/subscriptions/{guid}/resourceGroups/OldRG/providers/Microsoft.Cache/Redis/examplecache" -d "NewRG"

## <a name="control-access-to-resources"></a><span data-ttu-id="e2ac9-139">Control de acceso a los recursos</span><span class="sxs-lookup"><span data-stu-id="e2ac9-139">Control access to resources</span></span>
<span data-ttu-id="e2ac9-140">Puede utilizar la CLI de Azure para crear y administrar directivas para controlar el acceso a los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-140">You can use the Azure CLI to create and manage policies to control access to Azure resources.</span></span> <span data-ttu-id="e2ac9-141">Para más información acerca de las definiciones de directivas y de la asignación de directivas a los recursos, consulte [Uso de directivas para administrar los recursos y controlar el acceso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="e2ac9-141">For background about policy definitions and assigning policies to resources, see [Use policy to manage resources and control access](resource-manager-policy.md).</span></span>

<span data-ttu-id="e2ac9-142">Por ejemplo, defina la siguiente directiva para denegar todas las solicitudes cuya ubicación no sea oeste de Estados Unidos o centro-norte de Estados Unidos y guardarla en el archivo de definición de directivas policy.json:</span><span class="sxs-lookup"><span data-stu-id="e2ac9-142">For example, define the following policy to deny all requests where location is not West US or North Central US, and save it to the policy definition file policy.json:</span></span>

    {
    "if" : {
        "not" : {
        "field" : "location",
        "in" : ["westus" ,  "northcentralus"]
        }
    },
    "then" : {
        "effect" : "deny"
    }
    }

<span data-ttu-id="e2ac9-143">A continuación, ejecute el comando **policy definition create**:</span><span class="sxs-lookup"><span data-stu-id="e2ac9-143">Then run the **policy definition create** command:</span></span>

    azure policy definition create MyPolicy -p c:\temp\policy.json

<span data-ttu-id="e2ac9-144">Este comando muestra una salida similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="e2ac9-144">This command shows output similar to the following:</span></span>

    + <span data-ttu-id="e2ac9-145">Creación de definición de directiva MyPolicy datos:    PolicyName:             MyPolicy datos:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span><span class="sxs-lookup"><span data-stu-id="e2ac9-145">Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span></span>

    <span data-ttu-id="e2ac9-146">datos:    PolicyType:             Custom datos:    DisplayName:            undefined datos:    Description:            undefined datos:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span><span class="sxs-lookup"><span data-stu-id="e2ac9-146">data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span></span>

 <span data-ttu-id="e2ac9-147">Para asignar una directiva en el ámbito que desee, utilice el atributo **PolicyDefinitionId** devuelto por el comando anterior.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-147">To assign a policy at the scope you want, use the **PolicyDefinitionId** returned from the previous command.</span></span> <span data-ttu-id="e2ac9-148">En el ejemplo siguiente, este ámbito es la suscripción, pero puede restringir el ámbito a recursos individuales o a grupos de recursos:</span><span class="sxs-lookup"><span data-stu-id="e2ac9-148">In the following example, this scope is the subscription, but you can scope to resource groups or individual resources:</span></span>

    <span data-ttu-id="e2ac9-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span><span class="sxs-lookup"><span data-stu-id="e2ac9-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span></span>

<span data-ttu-id="e2ac9-150">Puede obtener, cambiar o quitar definiciones de directivas mediante los comandos **policy definition show**, **policy definition set** y **policy definition delete**.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-150">You can get, change, or remove policy definitions by using the **policy definition show**, **policy definition set**, and **policy definition delete** commands.</span></span>

<span data-ttu-id="e2ac9-151">De igual forma, puede obtener, cambiar o quitar asignaciones de directivas mediante los comandos **policy assignment show**, **policy assignment set** y **policy assignment delete**.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-151">Similarly, you can get, change, or remove policy assignments by using the **policy assignment show**, **policy assignment set**, and **policy assignment delete** commands.</span></span>

## <a name="export-a-resource-group-as-a-template"></a><span data-ttu-id="e2ac9-152">Exportación de un grupo de recursos como una plantilla</span><span class="sxs-lookup"><span data-stu-id="e2ac9-152">Export a resource group as a template</span></span>
<span data-ttu-id="e2ac9-153">Para un grupo de recursos existente, puede ver la plantilla de Resource Manager para el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-153">For an existing resource group, you can view the Resource Manager template for the resource group.</span></span> <span data-ttu-id="e2ac9-154">Exportar la plantilla ofrece dos ventajas:</span><span class="sxs-lookup"><span data-stu-id="e2ac9-154">Exporting the template offers two benefits:</span></span>

1. <span data-ttu-id="e2ac9-155">Puede automatizar fácilmente las futuras implementaciones de la solución porque toda la infraestructura está definida en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-155">You can easily automate future deployments of the solution because all the infrastructure is defined in the template.</span></span>
2. <span data-ttu-id="e2ac9-156">Para familiarizarse con la sintaxis de la plantilla, consulte el JSON que representa la solución.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-156">You can become familiar with template syntax by looking at the JSON that represents your solution.</span></span>

<span data-ttu-id="e2ac9-157">Con la CLI de Azure, puede exportar una plantilla que representa el estado actual de su grupo de recursos o descargar la plantilla que se usó para una implementación determinada.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-157">Using the Azure CLI, you can either export a template that represents the current state of your resource group, or download the template that was used for a particular deployment.</span></span>

* <span data-ttu-id="e2ac9-158">**Exportar la plantilla para un grupo de recursos**: resulta útil cuando se han realizado cambios en un grupo de recursos y necesita recuperar la representación JSON del estado actual.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-158">**Export the template for a resource group** - This is helpful when you made changes to a resource group, and need to retrieve the JSON representation of its current state.</span></span> <span data-ttu-id="e2ac9-159">Sin embargo, la plantilla generada contiene solo un número mínimo de parámetros y ninguna variable.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-159">However, the generated template contains only a minimal number of parameters and no variables.</span></span> <span data-ttu-id="e2ac9-160">La mayoría de los valores de la plantilla está codificados.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-160">Most of the values in the template are hard-coded.</span></span> <span data-ttu-id="e2ac9-161">Antes de implementar la plantilla generada, quizás desee convertir más valores en parámetros para poder personalizar la implementación para distintos entornos.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-161">Before deploying the generated template, you may wish to convert more of the values into parameters so you can customize the deployment for different environments.</span></span>
  
    <span data-ttu-id="e2ac9-162">Para exportar la plantilla para un grupo de recursos en un directorio local, ejecute el comando `azure group export` como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-162">To export the template for a resource group to a local directory, run the `azure group export` command as shown in the following example.</span></span> <span data-ttu-id="e2ac9-163">(Sustituya un directorio local adecuado para su entorno de sistema operativo).</span><span class="sxs-lookup"><span data-stu-id="e2ac9-163">(Substitute a local directory appropriate for your operating system environment.)</span></span>
  
        azure group export testRG ~/azure/templates/
* <span data-ttu-id="e2ac9-164">**Descargar la plantilla para una implementación concreta**: resulta útil si necesita ver la plantilla real que se usó para implementar recursos.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-164">**Download the template for a particular deployment** -- This is helpful when you need to view the actual template that was used to deploy resources.</span></span> <span data-ttu-id="e2ac9-165">La plantilla incluye todos los parámetros y las variables definidas para la implementación original.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-165">The template includes all parameters and variables defined for the original deployment.</span></span> <span data-ttu-id="e2ac9-166">Sin embargo, si alguien de su organización realiza cambios en el grupo de recursos fuera de lo que se define en la plantilla, esta plantilla no representa el estado actual del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-166">However, if someone in your organization made changes to the resource group outside of the definition in the template, this template doesn't represent the current state of the resource group.</span></span>
  
    <span data-ttu-id="e2ac9-167">Para descargar la plantilla usada para una implementación concreta en un directorio local, ejecute el comando `azure group deployment template download`.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-167">To download the template used for a particular deployment to a local directory, run the `azure group deployment template download` command.</span></span> <span data-ttu-id="e2ac9-168">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e2ac9-168">For example:</span></span>
  
        azure group deployment template download TestRG testRGDeploy ~/azure/templates/downloads/

> [!NOTE]
> <span data-ttu-id="e2ac9-169">La exportación de plantillas es una versión preliminar y no todos los tipos de recursos admiten actualmente la exportación de una plantilla.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-169">Template export is in preview, and not all resource types currently support exporting a template.</span></span> <span data-ttu-id="e2ac9-170">Al intentar exportar una plantilla, verá un error que indica que algunos recursos no se han exportado.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-170">When attempting to export a template, you may see an error that states some resources were not exported.</span></span> <span data-ttu-id="e2ac9-171">Si es necesario, defina manualmente estos recursos en la plantilla después de descargarla.</span><span class="sxs-lookup"><span data-stu-id="e2ac9-171">If needed, manually define these resources in your template after downloading it.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e2ac9-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e2ac9-172">Next steps</span></span>
* <span data-ttu-id="e2ac9-173">Para obtener detalles de las operaciones de implementación y solucionar los errores de implementación con la CLI de Azure, consulte [View deployment operations](resource-manager-deployment-operations.md) (Visualización de operaciones de implementación).</span><span class="sxs-lookup"><span data-stu-id="e2ac9-173">To get details of deployment operations and troubleshoot deployment errors with the Azure CLI, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="e2ac9-174">Si desea usar la CLI para configurar una aplicación o un script con objeto de obtener acceso a los recursos, consulte [Uso de la CLI de Azure para crear a una entidad de servicio para acceder a recursos](resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="e2ac9-174">If you want to use the CLI to set up an application or script to access resources, see [Use Azure CLI to create a service principal to access resources](resource-group-authenticate-service-principal-cli.md).</span></span>
* <span data-ttu-id="e2ac9-175">Para obtener instrucciones sobre cómo las empresas pueden utilizar Resource Manager para administrar eficazmente las suscripciones, vea [Scaffold empresarial de Azure: Gobierno de suscripción prescriptivo](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="e2ac9-175">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

