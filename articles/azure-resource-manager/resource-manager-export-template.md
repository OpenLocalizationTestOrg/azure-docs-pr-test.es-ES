---
title: "Exportación de plantillas de Azure Resource Manager | Microsoft Docs"
description: Use Azure Resource Manager para exportar una plantilla desde un grupo de recursos existente.
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
ms.openlocfilehash: 1801ef47e5b182e0bcd5b23970a2999633b4a852
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="export-an-azure-resource-manager-template-from-existing-resources"></a><span data-ttu-id="06985-103">Exportación de plantillas de Azure Resource Manager desde recursos existentes</span><span class="sxs-lookup"><span data-stu-id="06985-103">Export an Azure Resource Manager template from existing resources</span></span>
<span data-ttu-id="06985-104">En este artículo, aprenderá a exportar una plantilla de Resource Manager desde los recursos existentes en la suscripción.</span><span class="sxs-lookup"><span data-stu-id="06985-104">In this article, you learn how to export a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="06985-105">Puede usar la plantilla generada para conocer mejor de la sintaxis de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="06985-105">You can use that generated template to gain a better understanding of template syntax.</span></span>

<span data-ttu-id="06985-106">Hay dos maneras de exportar una plantilla:</span><span class="sxs-lookup"><span data-stu-id="06985-106">There are two ways to export a template:</span></span>

* <span data-ttu-id="06985-107">Se puede exportar la **plantilla real que se usó para una implementación**.</span><span class="sxs-lookup"><span data-stu-id="06985-107">You can export the **actual template used for deployment**.</span></span> <span data-ttu-id="06985-108">La plantilla exportada incluye todos los parámetros y variables exactamente como aparecían en la plantilla original.</span><span class="sxs-lookup"><span data-stu-id="06985-108">The exported template includes all the parameters and variables exactly as they appeared in the original template.</span></span> <span data-ttu-id="06985-109">Este enfoque es útil cuando se implementan recursos a través del portal y se desea ver la plantilla para crearlos.</span><span class="sxs-lookup"><span data-stu-id="06985-109">This approach is helpful when you deployed resources through the portal, and want to see the template to create those resources.</span></span> <span data-ttu-id="06985-110">Esta plantilla es fácil de usar.</span><span class="sxs-lookup"><span data-stu-id="06985-110">This template is readily usable.</span></span> 
* <span data-ttu-id="06985-111">Puede exportar una **plantilla generada que representa el estado actual del grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="06985-111">You can export a **generated template that represents the current state of the resource group**.</span></span> <span data-ttu-id="06985-112">La plantilla exportada no se basa en ninguna plantilla que usara para la implementación.</span><span class="sxs-lookup"><span data-stu-id="06985-112">The exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="06985-113">Al contrario, crea una plantilla que es una instantánea del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="06985-113">Instead, it creates a template that is a snapshot of the resource group.</span></span> <span data-ttu-id="06985-114">La plantilla exportada tiene muchos valores codificados de forma rígida y es probable que no tenga tantos parámetros como normalmente se definirían.</span><span class="sxs-lookup"><span data-stu-id="06985-114">The exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="06985-115">Este enfoque resulta útil si el grupo de recursos se ha modificado después de la implementación.</span><span class="sxs-lookup"><span data-stu-id="06985-115">This approach is useful when you have modified the resource group after deployment.</span></span> <span data-ttu-id="06985-116">Para poder usar esta plantilla, normalmente es preciso realizar ciertas modificaciones en ella.</span><span class="sxs-lookup"><span data-stu-id="06985-116">This template usually requires modifications before it is usable.</span></span>

<span data-ttu-id="06985-117">En este tema se muestran ambos métodos a través del portal.</span><span class="sxs-lookup"><span data-stu-id="06985-117">This topic shows both approaches through the portal.</span></span>

## <a name="deploy-resources"></a><span data-ttu-id="06985-118">Implementación de recursos</span><span class="sxs-lookup"><span data-stu-id="06985-118">Deploy resources</span></span>
<span data-ttu-id="06985-119">Para empezar, vamos a implementar en Azure recursos que se pueden utilizar para exportarlos como una plantilla.</span><span class="sxs-lookup"><span data-stu-id="06985-119">Let's start by deploying resources to Azure that you can use for exporting as a template.</span></span> <span data-ttu-id="06985-120">Si en la suscripción ya tiene un grupo de recursos que desee exportar a una plantilla, puede omitir esta sección.</span><span class="sxs-lookup"><span data-stu-id="06985-120">If you already have a resource group in your subscription that you want to export to a template, you can skip this section.</span></span> <span data-ttu-id="06985-121">En el resto de este artículo se da por supuesto que se ha implementado la aplicación web y la solución de base de datos SQL que se muestran en esta sección.</span><span class="sxs-lookup"><span data-stu-id="06985-121">The remainder of this article assumes you have deployed the web app and SQL database solution shown in this section.</span></span> <span data-ttu-id="06985-122">Si utiliza otra solución, puede que el conjunto del proceso sea un poco diferente, pero los pasos para exportar una plantilla son los mismos.</span><span class="sxs-lookup"><span data-stu-id="06985-122">If you use a different solution, your experience might be a little different, but the steps to export a template are the same.</span></span> 

1. <span data-ttu-id="06985-123">En [Azure Portal](https://portal.azure.com), seleccione **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="06985-123">In the [Azure portal](https://portal.azure.com), select **New**.</span></span>
   
      ![seleccionar Nuevo](./media/resource-manager-export-template/new.png)
2. <span data-ttu-id="06985-125">Busque **Aplicación web + SQL** y selecciónelo.</span><span class="sxs-lookup"><span data-stu-id="06985-125">Search for **web app + SQL** and select it from the available options.</span></span>
   
      ![buscar aplicación web y SQL](./media/resource-manager-export-template/webapp-sql.png)

3. <span data-ttu-id="06985-127">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="06985-127">Select **Create**.</span></span>

      ![seleccionar crear](./media/resource-manager-export-template/create.png)

4. <span data-ttu-id="06985-129">Proporcione los valores requeridos para la aplicación web y la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="06985-129">Provide the required values for the web app and SQL database.</span></span> <span data-ttu-id="06985-130">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="06985-130">Select **Create**.</span></span>

      ![proporcionar valor de web y SQL](./media/resource-manager-export-template/provide-web-values.png)

<span data-ttu-id="06985-132">La implementación puede tardar un momento.</span><span class="sxs-lookup"><span data-stu-id="06985-132">The deployment may take a minute.</span></span> <span data-ttu-id="06985-133">Una vez que finaliza la implementación, la suscripción contiene la solución.</span><span class="sxs-lookup"><span data-stu-id="06985-133">After the deployment finishes, your subscription contains the solution.</span></span>

## <a name="view-template-from-deployment-history"></a><span data-ttu-id="06985-134">Visualización de una plantilla desde el historial de implementaciones</span><span class="sxs-lookup"><span data-stu-id="06985-134">View template from deployment history</span></span>
1. <span data-ttu-id="06985-135">Vaya a la hoja del grupo de recursos que ha creado.</span><span class="sxs-lookup"><span data-stu-id="06985-135">Go to the resource group blade for your new resource group.</span></span> <span data-ttu-id="06985-136">Observe que la hoja muestra el resultado de la última implementación.</span><span class="sxs-lookup"><span data-stu-id="06985-136">Notice that the blade shows the result of the last deployment.</span></span> <span data-ttu-id="06985-137">Seleccione este vínculo.</span><span class="sxs-lookup"><span data-stu-id="06985-137">Select this link.</span></span>
   
      ![Hoja del grupo de recursos](./media/resource-manager-export-template/select-deployment.png)
2. <span data-ttu-id="06985-139">Se ve un historial de implementaciones para el grupo.</span><span class="sxs-lookup"><span data-stu-id="06985-139">You see a history of deployments for the group.</span></span> <span data-ttu-id="06985-140">En su caso, es probable que la hoja solo muestre una implementación.</span><span class="sxs-lookup"><span data-stu-id="06985-140">In your case, the blade probably lists only one deployment.</span></span> <span data-ttu-id="06985-141">Selecciónela.</span><span class="sxs-lookup"><span data-stu-id="06985-141">Select this deployment.</span></span>
   
     ![última implementación](./media/resource-manager-export-template/select-history.png)
3. <span data-ttu-id="06985-143">La hoja muestra un resumen de la implementación.</span><span class="sxs-lookup"><span data-stu-id="06985-143">The blade displays a summary of the deployment.</span></span> <span data-ttu-id="06985-144">El resumen incluye el estado de la implementación y sus operaciones, además de los valores que proporcionó para los parámetros.</span><span class="sxs-lookup"><span data-stu-id="06985-144">The summary includes the status of the deployment and its operations and the values that you provided for parameters.</span></span> <span data-ttu-id="06985-145">Para ver la plantilla que se usó para la implementación, seleccione **Ver plantilla**.</span><span class="sxs-lookup"><span data-stu-id="06985-145">To see the template that you used for the deployment, select **View template**.</span></span>
   
     ![Ver el resumen de la implementación](./media/resource-manager-export-template/view-template.png)
4. <span data-ttu-id="06985-147">Resource Manager recupera los siete archivos siguientes:</span><span class="sxs-lookup"><span data-stu-id="06985-147">Resource Manager retrieves the following seven files for you:</span></span>
   
   1. <span data-ttu-id="06985-148">**Plantilla** : la plantilla que define la infraestructura de la solución.</span><span class="sxs-lookup"><span data-stu-id="06985-148">**Template** - The template that defines the infrastructure for your solution.</span></span> <span data-ttu-id="06985-149">Cuando creó la cuenta de almacenamiento por medio del portal, Resource Manager usó una plantilla para implementarla y la guardó para futura referencia.</span><span class="sxs-lookup"><span data-stu-id="06985-149">When you created the storage account through the portal, Resource Manager used a template to deploy it and saved that template for future reference.</span></span>
   2. <span data-ttu-id="06985-150">**Parámetros**: un archivo de parámetros que puede usar para pasar valores durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="06985-150">**Parameters** - A parameter file that you can use to pass in values during deployment.</span></span> <span data-ttu-id="06985-151">Contiene los valores que proporcionó en la primera implementación.</span><span class="sxs-lookup"><span data-stu-id="06985-151">It contains the values that you provided during the first deployment.</span></span> <span data-ttu-id="06985-152">Todos estos valores se pueden cambiar al volver a implementar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="06985-152">You can change any of these values when you redeploy the template.</span></span>
   3. <span data-ttu-id="06985-153">**CLI**: un archivo de script de la interfaz de la línea de comandos (CLI) de Azure que puede usar para implementar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="06985-153">**CLI** - An Azure command-line-interface (CLI) script file that you can use to deploy the template.</span></span>
   3. <span data-ttu-id="06985-154">**CLI 2.0**: archivo de script de la interfaz de línea de comandos (CLI) de Azure que puede usar para implementar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="06985-154">**CLI 2.0** - An Azure command-line-interface (CLI) script file that you can use to deploy the template.</span></span>
   4. <span data-ttu-id="06985-155">**PowerShell** : un archivo de script de Azure PowerShell que puede usar para implementar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="06985-155">**PowerShell** - An Azure PowerShell script file that you can use to deploy the template.</span></span>
   5. <span data-ttu-id="06985-156">**.NET** : una clase .NET que puede utilizar para implementar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="06985-156">**.NET** - A .NET class that you can use to deploy the template.</span></span>
   6. <span data-ttu-id="06985-157">**Ruby** : una clase Ruby que puede utilizar para implementar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="06985-157">**Ruby** - A Ruby class that you can use to deploy the template.</span></span>
      
      <span data-ttu-id="06985-158">Los archivos están disponibles mediante vínculos en la hoja.</span><span class="sxs-lookup"><span data-stu-id="06985-158">The files are available through links across the blade.</span></span> <span data-ttu-id="06985-159">De forma predeterminada, la hoja muestra la plantilla.</span><span class="sxs-lookup"><span data-stu-id="06985-159">By default, the blade displays the template.</span></span>
      
       ![Ver plantilla](./media/resource-manager-export-template/see-template.png)
      
<span data-ttu-id="06985-161">Esta plantilla es la que se usó para crear la aplicación web y la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="06985-161">This template is the actual template used to create your web app and SQL database.</span></span> <span data-ttu-id="06985-162">Observe que contiene parámetros que le permiten proporcionar distintos valores en la implementación.</span><span class="sxs-lookup"><span data-stu-id="06985-162">Notice it contains parameters that enable you to provide different values during deployment.</span></span> <span data-ttu-id="06985-163">Para aprender más sobre la estructura de una plantilla, consulte [Creación de plantillas de Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="06985-163">To learn more about the structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

## <a name="export-the-template-from-resource-group"></a><span data-ttu-id="06985-164">Exportación de la plantilla desde el grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="06985-164">Export the template from resource group</span></span>
<span data-ttu-id="06985-165">Si ha cambiado los recursos o ha agregado recursos en varias implementaciones manualmente, la recuperación de una plantilla desde el historial de implementaciones no refleja el estado actual del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="06985-165">If you have manually changed your resources or added resources in multiple deployments, retrieving a template from the deployment history does not reflect the current state of the resource group.</span></span> <span data-ttu-id="06985-166">En esta sección se muestra cómo exportar una plantilla que refleja el estado actual del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="06985-166">This section shows you how to export a template that reflects the current state of the resource group.</span></span> 

> [!NOTE]
> <span data-ttu-id="06985-167">No se puede exportar una plantilla a un grupo de recursos que tenga más de doscientos recursos.</span><span class="sxs-lookup"><span data-stu-id="06985-167">You cannot export a template for a resource group that has more than 200 resources.</span></span>
> 
> 

1. <span data-ttu-id="06985-168">Para ver la plantilla de un grupo de recursos, seleccione **Script de automatización**.</span><span class="sxs-lookup"><span data-stu-id="06985-168">To view the template for a resource group, select **Automation script**.</span></span>
   
      ![exportar grupo de recursos](./media/resource-manager-export-template/select-automation.png)
   
     <span data-ttu-id="06985-170">Resource Manager evalúa los recursos del grupo de recursos y genera una plantilla para ellos.</span><span class="sxs-lookup"><span data-stu-id="06985-170">Resource Manager evaluates the resources in the resource group, and generates a template for those resources.</span></span> <span data-ttu-id="06985-171">No todos los tipos de recursos admiten la función de exportación de plantilla.</span><span class="sxs-lookup"><span data-stu-id="06985-171">Not all resource types support the export template function.</span></span> <span data-ttu-id="06985-172">Puede ver un error que indica que hay un problema con la exportación.</span><span class="sxs-lookup"><span data-stu-id="06985-172">You may see an error stating that there is a problem with the export.</span></span> <span data-ttu-id="06985-173">Puede aprender más sobre cómo resolver estos problemas en la sección [Solución de problemas de exportación](#fix-export-issues) .</span><span class="sxs-lookup"><span data-stu-id="06985-173">You learn how to handle those issues in the [Fix export issues](#fix-export-issues) section.</span></span>
2. <span data-ttu-id="06985-174">De nuevo ve los seis archivos que puede usar para volver a implementar la solución.</span><span class="sxs-lookup"><span data-stu-id="06985-174">You again see the six files that you can use to redeploy the solution.</span></span> <span data-ttu-id="06985-175">Sin embargo, esta vez la plantilla es algo diferente.</span><span class="sxs-lookup"><span data-stu-id="06985-175">However, this time the template is a little different.</span></span> <span data-ttu-id="06985-176">Observe que la plantilla generada contiene menos parámetros que la plantilla de la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="06985-176">Notice that the generated template contains fewer parameters than the template in previous section.</span></span> <span data-ttu-id="06985-177">Además, muchos de los valores (como los de ubicación y SKU) se codifican de forma rígida en esta plantilla, en lugar de aceptar un valor de parámetro.</span><span class="sxs-lookup"><span data-stu-id="06985-177">Also, many of the values (like location and SKU values) are hard-coded in this template rather than accepting a parameter value.</span></span> <span data-ttu-id="06985-178">Antes de volver a usar esta plantilla, puede editarla para hacer un mejor uso de los parámetros.</span><span class="sxs-lookup"><span data-stu-id="06985-178">Before reusing this template, you might want to edit the template to make better use of parameters.</span></span> 
   
3. <span data-ttu-id="06985-179">Tiene dos opciones para continuar trabajando con esta plantilla.</span><span class="sxs-lookup"><span data-stu-id="06985-179">You have a couple of options for continuing to work with this template.</span></span> <span data-ttu-id="06985-180">Puede descargar la plantilla y trabajar en ella localmente con un editor de JSON.</span><span class="sxs-lookup"><span data-stu-id="06985-180">You can either download the template and work on it locally with a JSON editor.</span></span> <span data-ttu-id="06985-181">O bien, puede guardar la plantilla en la biblioteca y trabajar en ella a través del portal.</span><span class="sxs-lookup"><span data-stu-id="06985-181">Or, you can save the template to your library and work on it through the portal.</span></span>
   
     <span data-ttu-id="06985-182">Si está familiarizado con el uso de un editor de JSON como [VS Code](https://code.visualstudio.com/) o [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), es posible que prefiera descargar la plantilla localmente y usar ese editor.</span><span class="sxs-lookup"><span data-stu-id="06985-182">If you are comfortable using a JSON editor like [VS Code](https://code.visualstudio.com/) or [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), you might prefer downloading the template locally and using that editor.</span></span> <span data-ttu-id="06985-183">Para trabajar de forma local, seleccione **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="06985-183">To work locally, select **Download**.</span></span>
   
      ![Descargar plantilla](./media/resource-manager-export-template/download-template.png)
   
     <span data-ttu-id="06985-185">Si no lo está, es preferible editar la plantilla a través del portal.</span><span class="sxs-lookup"><span data-stu-id="06985-185">If you are not set up with a JSON editor, you might prefer editing the template through the portal.</span></span> <span data-ttu-id="06985-186">En el resto de este tema se supone que ha guardado la plantilla en la biblioteca en el portal.</span><span class="sxs-lookup"><span data-stu-id="06985-186">The remainder of this topic assumes you have saved the template to your library in the portal.</span></span> <span data-ttu-id="06985-187">No obstante, tendrá que realizar los mismos cambios de sintaxis en la plantilla tanto si trabaja localmente con un editor de JSON o a través del portal.</span><span class="sxs-lookup"><span data-stu-id="06985-187">However, you make the same syntax changes to the template whether working locally with a JSON editor or through the portal.</span></span> <span data-ttu-id="06985-188">Para trabajar a través del portal, seleccione **Agregar a la biblioteca**.</span><span class="sxs-lookup"><span data-stu-id="06985-188">To work through the portal, select **Add to library**.</span></span>
   
      ![agregar a la biblioteca](./media/resource-manager-export-template/add-to-library.png)
   
     <span data-ttu-id="06985-190">Al agregar una plantilla a la biblioteca, asigne a la plantilla un nombre y una descripción.</span><span class="sxs-lookup"><span data-stu-id="06985-190">When adding a template to the library, give the template a name and description.</span></span> <span data-ttu-id="06985-191">Después, seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="06985-191">Then, select **Save**.</span></span>
   
     ![establecer valores de plantilla](./media/resource-manager-export-template/save-library-template.png)
4. <span data-ttu-id="06985-193">Para ver una plantilla guardada en la biblioteca, seleccione **Más servicios**, escriba **Plantillas** para filtrar los resultados y seleccione **Plantillas**.</span><span class="sxs-lookup"><span data-stu-id="06985-193">To view a template saved in your library, select **More services**, type **Templates** to filter results, select **Templates**.</span></span>
   
      ![buscar plantillas](./media/resource-manager-export-template/find-templates.png)
5. <span data-ttu-id="06985-195">Seleccione la plantilla con el nombre que se guardó.</span><span class="sxs-lookup"><span data-stu-id="06985-195">Select the template with the name you saved.</span></span>
   
      ![seleccionar plantilla](./media/resource-manager-export-template/select-saved-template.png)

## <a name="customize-the-template"></a><span data-ttu-id="06985-197">Personalización de la plantilla</span><span class="sxs-lookup"><span data-stu-id="06985-197">Customize the template</span></span>
<span data-ttu-id="06985-198">La plantilla exportada funciona bien si desea crear la misma aplicación web y base de datos cuenta SQL en todas las implementaciones.</span><span class="sxs-lookup"><span data-stu-id="06985-198">The exported template works fine if you want to create the same web app and SQL database for every deployment.</span></span> <span data-ttu-id="06985-199">No obstante, Resource Manager proporciona opciones para que pueda implementar plantillas con mucha más flexibilidad.</span><span class="sxs-lookup"><span data-stu-id="06985-199">However, Resource Manager provides options so that you can deploy templates with a lot more flexibility.</span></span> <span data-ttu-id="06985-200">En este artículo se muestra cómo agregar parámetros para el nombre y la contraseña del administrador de base de datos.</span><span class="sxs-lookup"><span data-stu-id="06985-200">This article shows you how to add parameters for the database administrator name and password.</span></span> <span data-ttu-id="06985-201">Este mismo método se puede usar para dar más flexibilidad a otros valores de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="06985-201">You can use this same approach to add more flexibility for other values in the template.</span></span>

1. <span data-ttu-id="06985-202">Seleccione **Editar** para personalizar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="06985-202">To customize the template, select **Edit**.</span></span>
   
     ![mostrar plantilla](./media/resource-manager-export-template/select-edit.png)
2. <span data-ttu-id="06985-204">Seleccione la plantilla.</span><span class="sxs-lookup"><span data-stu-id="06985-204">Select the template.</span></span>
   
     ![editar plantilla](./media/resource-manager-export-template/select-added-template.png)
3. <span data-ttu-id="06985-206">Para poder pasar los valores que desea especificar durante la implementación, agregue los dos parámetros siguientes a la sección **parameters** de la plantilla:</span><span class="sxs-lookup"><span data-stu-id="06985-206">To be able to pass the values that you might want to specify during deployment, add the following two parameters to the **parameters** section in the template:</span></span>

   ```json
   "administratorLogin": {
       "type": "String"
   },
   "administratorLoginPassword": {
       "type": "SecureString"
   },
   ```

4. <span data-ttu-id="06985-207">Para usar los nuevos parámetros, reemplace la definición del servidor de SQL Server en la sección **resources**.</span><span class="sxs-lookup"><span data-stu-id="06985-207">To use the new parameters, replace the SQL server definition in the **resources** section.</span></span> <span data-ttu-id="06985-208">Tenga en cuenta que **administratorLogin** y **administratorLoginPassword** ahora usan los valores de los parámetros.</span><span class="sxs-lookup"><span data-stu-id="06985-208">Notice that **administratorLogin** and **administratorLoginPassword** now use parameter values.</span></span>

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

6. <span data-ttu-id="06985-209">Seleccione **Aceptar** cuando haya terminado la edición de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="06985-209">Select **OK** when you are done editing the template.</span></span>
7. <span data-ttu-id="06985-210">Seleccione **Guardar** para guardar los cambios en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="06985-210">Select **Save** to save the changes to the template.</span></span>
   
     ![guardar plantilla](./media/resource-manager-export-template/save-template.png)
8. <span data-ttu-id="06985-212">Para volver a implementar la plantilla actualizada, seleccione **Implementar**.</span><span class="sxs-lookup"><span data-stu-id="06985-212">To redeploy the updated template, select **Deploy**.</span></span>
   
     ![implementar plantilla](./media/resource-manager-export-template/redeploy-template.png)
9. <span data-ttu-id="06985-214">Proporcione valores de parámetro y seleccione el grupo de recursos en el que se van a implementar los recursos.</span><span class="sxs-lookup"><span data-stu-id="06985-214">Provide parameter values, and select a resource group to deploy the resources to.</span></span>


## <a name="fix-export-issues"></a><span data-ttu-id="06985-215">Solución de problemas de exportación</span><span class="sxs-lookup"><span data-stu-id="06985-215">Fix export issues</span></span>
<span data-ttu-id="06985-216">No todos los tipos de recursos admiten la función de exportación de plantilla.</span><span class="sxs-lookup"><span data-stu-id="06985-216">Not all resource types support the export template function.</span></span> <span data-ttu-id="06985-217">Para evitar este problema, agregue manualmente los recursos que faltan a la plantilla.</span><span class="sxs-lookup"><span data-stu-id="06985-217">To resolve this issue, manually add the missing resources back into your template.</span></span> <span data-ttu-id="06985-218">El mensaje de error incluye los tipos de recursos que no se puede exportar.</span><span class="sxs-lookup"><span data-stu-id="06985-218">The error message includes the resource types that cannot be exported.</span></span> <span data-ttu-id="06985-219">Busque el tipo de recurso en [Referencia de plantilla](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="06985-219">Find that resource type in [Template reference](/azure/templates/).</span></span> <span data-ttu-id="06985-220">Por ejemplo, para agregar manualmente una puerta de enlace de red virtual, consulte [Microsoft.Network/virtualNetworkGateways template reference](/azure/templates/microsoft.network/virtualnetworkgateways) (Referencia de plantilla Microsoft.Network/virtualNetworkGateways).</span><span class="sxs-lookup"><span data-stu-id="06985-220">For example, to manually add a virtual network gateway, see [Microsoft.Network/virtualNetworkGateways template reference](/azure/templates/microsoft.network/virtualnetworkgateways).</span></span>

> [!NOTE]
> <span data-ttu-id="06985-221">Solo se encuentran problemas de exportación si se exporta desde un grupo de recursos en lugar de desde el historial de implementación.</span><span class="sxs-lookup"><span data-stu-id="06985-221">You only encounter export issues when exporting from a resource group rather than from your deployment history.</span></span> <span data-ttu-id="06985-222">Si su última implementación representa con precisión el estado actual del grupo de recursos, debe exportar la plantilla desde el historial de implementación en lugar de desde el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="06985-222">If your last deployment accurately represents the current state of the resource group, you should export the template from the deployment history rather than from the resource group.</span></span> <span data-ttu-id="06985-223">Exporte solo desde un grupo de recursos si ha realizado cambios en el grupo de recursos que no están definidos en una única plantilla.</span><span class="sxs-lookup"><span data-stu-id="06985-223">Only export from a resource group when you have made changes to the resource group that are not defined in a single template.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="06985-224">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="06985-224">Next steps</span></span>
<span data-ttu-id="06985-225">Ha aprendido a exportar una plantilla desde recursos creados en el portal.</span><span class="sxs-lookup"><span data-stu-id="06985-225">You have learned how to export a template from resources that you created in the portal.</span></span>

* <span data-ttu-id="06985-226">Puede implementar una plantilla mediante [PowerShell](resource-group-template-deploy.md), [CLI de Azure](resource-group-template-deploy-cli.md), o [API de REST](resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="06985-226">You can deploy a template through [PowerShell](resource-group-template-deploy.md), [Azure CLI](resource-group-template-deploy-cli.md), or [REST API](resource-group-template-deploy-rest.md).</span></span>
* <span data-ttu-id="06985-227">Para ver cómo exportar una plantilla mediante PowerShell, consulte [Uso de Azure PowerShell con Azure Resource Manager](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="06985-227">To see how to export a template through PowerShell, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="06985-228">Para ver cómo exportar una plantilla mediante la CLI de Azure, consulte [Uso de la CLI de Azure para Mac, Linux y Windows con Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="06985-228">To see how to export a template through Azure CLI, see [Use the Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>

