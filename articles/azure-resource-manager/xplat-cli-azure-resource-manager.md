---
title: recursos de aaaManage con hello CLI de Azure | Documentos de Microsoft
description: "Usar toomanage de interfaz de línea de comandos (CLI) de Azure de hello Azure recursos y grupos"
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
ms.openlocfilehash: 3df70e123d14d3bbf2648c71970bac1db4afc025
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cli-toomanage-azure-resources-and-resource-groups"></a><span data-ttu-id="d9ad8-103">Usar hello Azure CLI toomanage Azure y grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="d9ad8-103">Use hello Azure CLI toomanage Azure resources and resource groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d9ad8-104">Portal</span><span class="sxs-lookup"><span data-stu-id="d9ad8-104">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="d9ad8-105">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="d9ad8-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="d9ad8-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9ad8-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="d9ad8-107">API DE REST</span><span class="sxs-lookup"><span data-stu-id="d9ad8-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="d9ad8-108">Hola interfaz de línea de comandos de Azure (Azure CLI) es una de las diversas herramientas puede usar toodeploy y administrar recursos con el Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-108">hello Azure Command-Line Interface (Azure CLI) is one of several tools you can use toodeploy and manage resources with Resource Manager.</span></span> <span data-ttu-id="d9ad8-109">Este artículo detallan comunes formas toomanage Azure y grupos de recursos mediante el uso de Hola CLI de Azure en el modo de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-109">This article introduces common ways toomanage Azure resources and resource groups by using hello Azure CLI in Resource Manager mode.</span></span> <span data-ttu-id="d9ad8-110">Para obtener información sobre el uso de recursos de toodeploy de hello CLI, consulte [implementar los recursos con plantillas de administrador de recursos y la CLI de Azure](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d9ad8-110">For information about using hello CLI toodeploy resources, see [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> <span data-ttu-id="d9ad8-111">Para obtener información acerca de los recursos de Azure y el Administrador de recursos, visite hello [Azure Resource Manager Overview](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d9ad8-111">For background about Azure resources and Resource Manager, visit hello [Azure Resource Manager Overview](resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d9ad8-112">toomanage Azure recursos con hello CLI de Azure, que necesita demasiado[instalar hello Azure CLI](../cli-install-nodejs.md), y [sesión tooAzure](../xplat-cli-connect.md) mediante el uso de hello `azure login` comando.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-112">toomanage Azure resources with hello Azure CLI, you need too[install hello Azure CLI](../cli-install-nodejs.md), and [log in tooAzure](../xplat-cli-connect.md) by using hello `azure login` command.</span></span> <span data-ttu-id="d9ad8-113">Asegúrese de hello seguro CLI está en modo de administrador de recursos (ejecutar `azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="d9ad8-113">Make sure hello CLI is in Resource Manager mode (run `azure config mode arm`).</span></span> <span data-ttu-id="d9ad8-114">Si lo ha hecho, está listo toogo.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-114">If you've done these things, you're ready toogo.</span></span>
> 
> 

## <a name="get-resource-groups-and-resources"></a><span data-ttu-id="d9ad8-115">Obtención de recursos y grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="d9ad8-115">Get resource groups and resources</span></span>
### <a name="resource-groups"></a><span data-ttu-id="d9ad8-116">Grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="d9ad8-116">Resource groups</span></span>
<span data-ttu-id="d9ad8-117">tooget una lista de todos los grupos de recursos en su suscripción y sus ubicaciones, ejecute este comando.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-117">tooget a list of all resource groups in your subscription and their locations, run this command.</span></span>

    azure group list


### <a name="resources"></a><span data-ttu-id="d9ad8-118">Recursos</span><span class="sxs-lookup"><span data-stu-id="d9ad8-118">Resources</span></span>
 <span data-ttu-id="d9ad8-119">el nombre de todos los recursos de un grupo, por ejemplo, uno con toolist *testRG*, usar hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="d9ad8-119">toolist all resources in a group, such as one with name *testRG*, use hello following command:</span></span>

    azure resource list testRG

<span data-ttu-id="d9ad8-120">un recurso individual en el grupo de hello, como una máquina virtual denominada tooview *MyUbuntuVM*, utilizar un comando como Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="d9ad8-120">tooview an individual resource within hello group, such as a VM named *MyUbuntuVM*, use a command like hello following:</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="d9ad8-121">Hola aviso **Microsoft.Compute/virtualMachines** parámetro.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-121">Notice hello **Microsoft.Compute/virtualMachines** parameter.</span></span> <span data-ttu-id="d9ad8-122">Este parámetro indica el tipo hello del recurso de Hola que solicita información en.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-122">This parameter indicates hello type of hello resource you are requesting information on.</span></span>

> [!NOTE]
> <span data-ttu-id="d9ad8-123">Cuando se usa hello **recursos de azure** comandos que no sean de hello **lista** de comandos, debe especificar versión de Hola API de recursos de hello con hello **-o** parámetro.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-123">When using hello **azure resource** commands other than hello **list** command, you must specify hello API version of hello resource with hello **-o** parameter.</span></span> <span data-ttu-id="d9ad8-124">Si no está seguro acerca de la versión de la API de hello, consulte el archivo de plantilla de hello y encontrar el campo de valor apiVersion de hello para el recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-124">If you're unsure about hello API version, consult hello template file and find hello apiVersion field for hello resource.</span></span> <span data-ttu-id="d9ad8-125">Para más información acerca de las versiones de API de Resource Manager, vea [Tipos y proveedores de recursos](resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="d9ad8-125">For more about API versions in Resource Manager, see [Resource providers and types](resource-manager-supported-services.md).</span></span>
> 
> 

<span data-ttu-id="d9ad8-126">Al ver los detalles en un recurso, a menudo resulta útil toouse hello `--json` parámetro.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-126">When viewing details on a resource, it is often useful toouse hello `--json` parameter.</span></span> <span data-ttu-id="d9ad8-127">Este parámetro hace que los resultados Hola sea más legible, porque algunos de los valores son estructuras anidadas o colecciones.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-127">This parameter makes hello output more readable, because some values are nested structures, or collections.</span></span> <span data-ttu-id="d9ad8-128">Hello en el ejemplo siguiente se muestra devolver resultados Hola de hello **mostrar** comando como un documento JSON.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-128">hello following example demonstrates returning hello results of hello **show** command as a JSON document.</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json

> [!NOTE]
> <span data-ttu-id="d9ad8-129">Si lo desea, guarde Hola JSON datos toofile mediante el uso de hello &gt; archivo de tooa de salida de caracteres toodirect Hola.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-129">If you want, save hello JSON data toofile by using hello &gt; character toodirect hello output tooa file.</span></span> <span data-ttu-id="d9ad8-130">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d9ad8-130">For example:</span></span>
> 
> `azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json > myfile.json`
> 
> 

### <a name="tags"></a><span data-ttu-id="d9ad8-131">Etiquetas</span><span class="sxs-lookup"><span data-stu-id="d9ad8-131">Tags</span></span>
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="manage-resources"></a><span data-ttu-id="d9ad8-132">Administración de recursos</span><span class="sxs-lookup"><span data-stu-id="d9ad8-132">Manage resources</span></span>
<span data-ttu-id="d9ad8-133">tooadd un recurso como un grupo de recursos tooa de cuenta de almacenamiento, ejecute un comando similar al:</span><span class="sxs-lookup"><span data-stu-id="d9ad8-133">tooadd a resource such as a storage account tooa resource group, run a command similar to:</span></span>

    azure resource create testRG MyStorageAccount "Microsoft.Storage/storageAccounts" "westus" -o "2015-06-15" -p "{\"accountType\": \"Standard_LRS\"}"

<span data-ttu-id="d9ad8-134">Además toospecifying Hola versión de API de recurso de hello con hello **-o** parámetro, use hello **-p** toopass formato JSON de la cadena de parámetros con cualquier necesario o propiedades adicionales.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-134">In addition toospecifying hello API version of hello resource with hello **-o** parameter, use hello **-p** parameter toopass a JSON-formatted string with any required or additional properties.</span></span>

<span data-ttu-id="d9ad8-135">toodelete un recurso existente como un recurso de la máquina virtual, use un comando como Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="d9ad8-135">toodelete an existing resource such as a virtual machine resource, use a command like hello following:</span></span>

    azure resource delete testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="d9ad8-136">existente toomove grupo de recursos de tooanother de recursos o suscripción, utilice hello **mover recursos de azure** comando.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-136">toomove existing resources tooanother resource group or subscription, use hello **azure resource move** command.</span></span> <span data-ttu-id="d9ad8-137">Hola siguiente ejemplo se muestra cómo toomove caché en Redis tooa nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-137">hello following example shows how toomove a Redis Cache tooa new resource group.</span></span> <span data-ttu-id="d9ad8-138">Hola **-i** parámetro, proporcione una lista separada por comas de toomove del Id. de recurso Hola.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-138">In hello **-i** parameter, provide a comma-separated list of hello resource id's toomove.</span></span>

    azure resource move -i "/subscriptions/{guid}/resourceGroups/OldRG/providers/Microsoft.Cache/Redis/examplecache" -d "NewRG"

## <a name="control-access-tooresources"></a><span data-ttu-id="d9ad8-139">Tooresources de acceso de control</span><span class="sxs-lookup"><span data-stu-id="d9ad8-139">Control access tooresources</span></span>
<span data-ttu-id="d9ad8-140">Puede usar hello toocreate de CLI de Azure y administrar directivas toocontrol acceso tooAzure recursos.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-140">You can use hello Azure CLI toocreate and manage policies toocontrol access tooAzure resources.</span></span> <span data-ttu-id="d9ad8-141">Para obtener información acerca de las definiciones de directiva y asignar tooresources de directivas, consulte [usar Directiva toomanage recursos y controlar el acceso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="d9ad8-141">For background about policy definitions and assigning policies tooresources, see [Use policy toomanage resources and control access](resource-manager-policy.md).</span></span>

<span data-ttu-id="d9ad8-142">Por ejemplo, definir Hola después directiva toodeny todas las solicitudes donde la ubicación no es oeste de Estados Unidos o Ee.uu. Central Norte y guardar policy.json de archivo de definición de directiva de toohello:</span><span class="sxs-lookup"><span data-stu-id="d9ad8-142">For example, define hello following policy toodeny all requests where location is not West US or North Central US, and save it toohello policy definition file policy.json:</span></span>

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

<span data-ttu-id="d9ad8-143">A continuación, ejecute hello **Crear definición de directiva** comando:</span><span class="sxs-lookup"><span data-stu-id="d9ad8-143">Then run hello **policy definition create** command:</span></span>

    azure policy definition create MyPolicy -p c:\temp\policy.json

<span data-ttu-id="d9ad8-144">Este comando muestra la siguiente toohello similar de salida:</span><span class="sxs-lookup"><span data-stu-id="d9ad8-144">This command shows output similar toohello following:</span></span>

    + <span data-ttu-id="d9ad8-145">Creación de definición de directiva MyPolicy datos:    PolicyName:             MyPolicy datos:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span><span class="sxs-lookup"><span data-stu-id="d9ad8-145">Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span></span>

    <span data-ttu-id="d9ad8-146">datos:    PolicyType:             Custom datos:    DisplayName:            undefined datos:    Description:            undefined datos:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span><span class="sxs-lookup"><span data-stu-id="d9ad8-146">data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span></span>

 <span data-ttu-id="d9ad8-147">una directiva en el ámbito de Hola que desee, use hello tooassign **PolicyDefinitionId** devueltos por el comando anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-147">tooassign a policy at hello scope you want, use hello **PolicyDefinitionId** returned from hello previous command.</span></span> <span data-ttu-id="d9ad8-148">En el siguiente ejemplo de Hola, este ámbito es suscripción hello, pero puede establecer el ámbito tooresource grupos o recursos individuales:</span><span class="sxs-lookup"><span data-stu-id="d9ad8-148">In hello following example, this scope is hello subscription, but you can scope tooresource groups or individual resources:</span></span>

    <span data-ttu-id="d9ad8-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span><span class="sxs-lookup"><span data-stu-id="d9ad8-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span></span>

<span data-ttu-id="d9ad8-150">Puede obtener, cambiar o quitar las definiciones de directivas mediante hello **mostrar de la definición de directiva**, **conjunto de definiciones de directiva**, y **eliminar la definición de directiva** comandos.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-150">You can get, change, or remove policy definitions by using hello **policy definition show**, **policy definition set**, and **policy definition delete** commands.</span></span>

<span data-ttu-id="d9ad8-151">De forma similar, puede obtener, cambiar o quitar las asignaciones de directivas mediante hello **mostrar de la asignación de directiva**, **conjunto de asignación de directiva**, y **Eliminar asignación de directiva** comandos .</span><span class="sxs-lookup"><span data-stu-id="d9ad8-151">Similarly, you can get, change, or remove policy assignments by using hello **policy assignment show**, **policy assignment set**, and **policy assignment delete** commands.</span></span>

## <a name="export-a-resource-group-as-a-template"></a><span data-ttu-id="d9ad8-152">Exportación de un grupo de recursos como una plantilla</span><span class="sxs-lookup"><span data-stu-id="d9ad8-152">Export a resource group as a template</span></span>
<span data-ttu-id="d9ad8-153">Para un grupo de recursos existente, puede ver la plantilla de administrador de recursos de Hola Hola para grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-153">For an existing resource group, you can view hello Resource Manager template for hello resource group.</span></span> <span data-ttu-id="d9ad8-154">Exportar plantilla Hola ofrece dos ventajas:</span><span class="sxs-lookup"><span data-stu-id="d9ad8-154">Exporting hello template offers two benefits:</span></span>

1. <span data-ttu-id="d9ad8-155">Puede automatizar fácilmente las futuras implementaciones de soluciones de hello porque toda la infraestructura de Hola se define en la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-155">You can easily automate future deployments of hello solution because all hello infrastructure is defined in hello template.</span></span>
2. <span data-ttu-id="d9ad8-156">Familiarícese con la sintaxis de plantilla examinando Hola JSON que representa la solución.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-156">You can become familiar with template syntax by looking at hello JSON that represents your solution.</span></span>

<span data-ttu-id="d9ad8-157">Con hello CLI de Azure, se puede exportar una plantilla que representa el estado actual de Hola de su grupo de recursos, o descargar plantilla de Hola que se usó para una implementación concreta.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-157">Using hello Azure CLI, you can either export a template that represents hello current state of your resource group, or download hello template that was used for a particular deployment.</span></span>

* <span data-ttu-id="d9ad8-158">**Exportar plantilla Hola para un grupo de recursos** -Esto resulta útil cuando realiza cambios tooa grupo de recursos y necesita tooretrieve Hola representación JSON de su estado actual.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-158">**Export hello template for a resource group** - This is helpful when you made changes tooa resource group, and need tooretrieve hello JSON representation of its current state.</span></span> <span data-ttu-id="d9ad8-159">Sin embargo, plantilla generada hello contiene solo un número mínimo de parámetros y no hay ninguna variable.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-159">However, hello generated template contains only a minimal number of parameters and no variables.</span></span> <span data-ttu-id="d9ad8-160">La mayoría de los valores de hello en plantilla Hola está codificados.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-160">Most of hello values in hello template are hard-coded.</span></span> <span data-ttu-id="d9ad8-161">Antes de implementar la plantilla de hello generado, es recomendable tooconvert varios de los valores de hello en los parámetros para que pueda personalizar la implementación de Hola para diferentes entornos.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-161">Before deploying hello generated template, you may wish tooconvert more of hello values into parameters so you can customize hello deployment for different environments.</span></span>
  
    <span data-ttu-id="d9ad8-162">plantilla de hello tooexport para un recurso grupo tooa directorio local, ejecute hello `azure group export` comando tal como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-162">tooexport hello template for a resource group tooa local directory, run hello `azure group export` command as shown in hello following example.</span></span> <span data-ttu-id="d9ad8-163">(Sustituya un directorio local adecuado para su entorno de sistema operativo).</span><span class="sxs-lookup"><span data-stu-id="d9ad8-163">(Substitute a local directory appropriate for your operating system environment.)</span></span>
  
        azure group export testRG ~/azure/templates/
* <span data-ttu-id="d9ad8-164">**Descargar plantilla de Hola para una implementación concreta** : Esto es útil cuando necesita tooview Hola real de la plantilla que usa toodeploy recursos.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-164">**Download hello template for a particular deployment** -- This is helpful when you need tooview hello actual template that was used toodeploy resources.</span></span> <span data-ttu-id="d9ad8-165">plantilla de Hello incluye todos los parámetros y las variables definidas para la implementación original de Hola.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-165">hello template includes all parameters and variables defined for hello original deployment.</span></span> <span data-ttu-id="d9ad8-166">Sin embargo, si alguien de su organización realiza grupo de recursos de toohello de cambios fuera de la definición de hello en plantilla hello, esta plantilla no representa el estado actual de Hola Hola del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-166">However, if someone in your organization made changes toohello resource group outside of hello definition in hello template, this template doesn't represent hello current state of hello resource group.</span></span>
  
    <span data-ttu-id="d9ad8-167">plantilla de hello toodownload utilizada para un implementación determinada tooa directorio local, ejecute hello `azure group deployment template download` comando.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-167">toodownload hello template used for a particular deployment tooa local directory, run hello `azure group deployment template download` command.</span></span> <span data-ttu-id="d9ad8-168">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d9ad8-168">For example:</span></span>
  
        azure group deployment template download TestRG testRGDeploy ~/azure/templates/downloads/

> [!NOTE]
> <span data-ttu-id="d9ad8-169">La exportación de plantillas es una versión preliminar y no todos los tipos de recursos admiten actualmente la exportación de una plantilla.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-169">Template export is in preview, and not all resource types currently support exporting a template.</span></span> <span data-ttu-id="d9ad8-170">Al intentar tooexport una plantilla, verá un error que indica que algunos recursos no se exportaron.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-170">When attempting tooexport a template, you may see an error that states some resources were not exported.</span></span> <span data-ttu-id="d9ad8-171">Si es necesario, defina manualmente estos recursos en la plantilla después de descargarla.</span><span class="sxs-lookup"><span data-stu-id="d9ad8-171">If needed, manually define these resources in your template after downloading it.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="d9ad8-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d9ad8-172">Next steps</span></span>
* <span data-ttu-id="d9ad8-173">detalles de tooget de las operaciones de implementación y solucionar errores de implementación con hello CLI de Azure, consulte [ver las operaciones de implementación](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="d9ad8-173">tooget details of deployment operations and troubleshoot deployment errors with hello Azure CLI, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="d9ad8-174">Si desea toouse Hola CLI tooset una aplicación o recursos de script tooaccess, consulte [toocreate de CLI de Azure Use una entidad de servicio tooaccess recursos](resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d9ad8-174">If you want toouse hello CLI tooset up an application or script tooaccess resources, see [Use Azure CLI toocreate a service principal tooaccess resources](resource-group-authenticate-service-principal-cli.md).</span></span>
* <span data-ttu-id="d9ad8-175">Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="d9ad8-175">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

