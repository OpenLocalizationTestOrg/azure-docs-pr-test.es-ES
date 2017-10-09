---
title: plantilla de Azure Resource Manager aaaExport | Documentos de Microsoft
description: "Use Administración de recursos de Azure tooexport una plantilla a partir de un grupo de recursos existente."
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
ms.openlocfilehash: 94daa4812da2fec705044ca31c8e74e6d59bd53f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="export-an-azure-resource-manager-template-from-existing-resources"></a><span data-ttu-id="64f4b-103">Exportación de plantillas de Azure Resource Manager desde recursos existentes</span><span class="sxs-lookup"><span data-stu-id="64f4b-103">Export an Azure Resource Manager template from existing resources</span></span>
<span data-ttu-id="64f4b-104">En este artículo, aprenderá cómo tooexport una plantilla de administrador de recursos de los recursos existentes en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="64f4b-104">In this article, you learn how tooexport a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="64f4b-105">Puede usar ese toogain plantilla generada una mejor comprensión de la sintaxis de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="64f4b-105">You can use that generated template toogain a better understanding of template syntax.</span></span>

<span data-ttu-id="64f4b-106">Hay dos tooexport de formas de una plantilla:</span><span class="sxs-lookup"><span data-stu-id="64f4b-106">There are two ways tooexport a template:</span></span>

* <span data-ttu-id="64f4b-107">Puede exportar hello **plantilla real que se utiliza para la implementación**.</span><span class="sxs-lookup"><span data-stu-id="64f4b-107">You can export hello **actual template used for deployment**.</span></span> <span data-ttu-id="64f4b-108">plantilla exportada Hola incluye todas las variables y parámetros de hello exactamente tal y como aparecían en la plantilla original Hola.</span><span class="sxs-lookup"><span data-stu-id="64f4b-108">hello exported template includes all hello parameters and variables exactly as they appeared in hello original template.</span></span> <span data-ttu-id="64f4b-109">Este enfoque resulta útil si ha implementado los recursos a través del portal de Hola y desea toosee Hola plantilla toocreate esos recursos.</span><span class="sxs-lookup"><span data-stu-id="64f4b-109">This approach is helpful when you deployed resources through hello portal, and want toosee hello template toocreate those resources.</span></span> <span data-ttu-id="64f4b-110">Esta plantilla es fácil de usar.</span><span class="sxs-lookup"><span data-stu-id="64f4b-110">This template is readily usable.</span></span> 
* <span data-ttu-id="64f4b-111">Puede exportar un **genera plantilla que representa el estado actual de Hola Hola del grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="64f4b-111">You can export a **generated template that represents hello current state of hello resource group**.</span></span> <span data-ttu-id="64f4b-112">plantilla exportada Hello no se basa en cualquier plantilla que utiliza para la implementación.</span><span class="sxs-lookup"><span data-stu-id="64f4b-112">hello exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="64f4b-113">En su lugar, crea una plantilla que es una instantánea Hola del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="64f4b-113">Instead, it creates a template that is a snapshot of hello resource group.</span></span> <span data-ttu-id="64f4b-114">plantilla exportada Hello tiene muchos valores codificados de forma rígida y probablemente no tantos parámetros como normalmente tendría que definir.</span><span class="sxs-lookup"><span data-stu-id="64f4b-114">hello exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="64f4b-115">Este enfoque es útil cuando se ha modificado el grupo de recursos de hello después de la implementación.</span><span class="sxs-lookup"><span data-stu-id="64f4b-115">This approach is useful when you have modified hello resource group after deployment.</span></span> <span data-ttu-id="64f4b-116">Para poder usar esta plantilla, normalmente es preciso realizar ciertas modificaciones en ella.</span><span class="sxs-lookup"><span data-stu-id="64f4b-116">This template usually requires modifications before it is usable.</span></span>

<span data-ttu-id="64f4b-117">En este tema se muestra ambos enfoques a través del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="64f4b-117">This topic shows both approaches through hello portal.</span></span>

## <a name="deploy-resources"></a><span data-ttu-id="64f4b-118">Implementación de recursos</span><span class="sxs-lookup"><span data-stu-id="64f4b-118">Deploy resources</span></span>
<span data-ttu-id="64f4b-119">Empecemos por tooAzure de recursos que puede usar para exportar como una plantilla de implementación.</span><span class="sxs-lookup"><span data-stu-id="64f4b-119">Let's start by deploying resources tooAzure that you can use for exporting as a template.</span></span> <span data-ttu-id="64f4b-120">Si ya tiene un grupo de recursos en la suscripción que desea que la plantilla de tooa tooexport, puede omitir esta sección.</span><span class="sxs-lookup"><span data-stu-id="64f4b-120">If you already have a resource group in your subscription that you want tooexport tooa template, you can skip this section.</span></span> <span data-ttu-id="64f4b-121">resto de Hola de este artículo se da por supuesto que haya implementado la aplicación web de hello y solución de base de datos SQL que se muestra en esta sección.</span><span class="sxs-lookup"><span data-stu-id="64f4b-121">hello remainder of this article assumes you have deployed hello web app and SQL database solution shown in this section.</span></span> <span data-ttu-id="64f4b-122">Si utiliza una solución distinta, su experiencia podría ser un poco diferente, pero Hola pasos hello tooexport una plantilla son iguales.</span><span class="sxs-lookup"><span data-stu-id="64f4b-122">If you use a different solution, your experience might be a little different, but hello steps tooexport a template are hello same.</span></span> 

1. <span data-ttu-id="64f4b-123">Hola [portal de Azure](https://portal.azure.com), seleccione **nuevo**.</span><span class="sxs-lookup"><span data-stu-id="64f4b-123">In hello [Azure portal](https://portal.azure.com), select **New**.</span></span>
   
      ![seleccionar Nuevo](./media/resource-manager-export-template/new.png)
2. <span data-ttu-id="64f4b-125">Busque **web app + SQL** y selecciónelo en las opciones disponibles de Hola.</span><span class="sxs-lookup"><span data-stu-id="64f4b-125">Search for **web app + SQL** and select it from hello available options.</span></span>
   
      ![buscar aplicación web y SQL](./media/resource-manager-export-template/webapp-sql.png)

3. <span data-ttu-id="64f4b-127">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="64f4b-127">Select **Create**.</span></span>

      ![seleccionar crear](./media/resource-manager-export-template/create.png)

4. <span data-ttu-id="64f4b-129">Proporcionar valores de hello necesario para la aplicación web de hello y base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="64f4b-129">Provide hello required values for hello web app and SQL database.</span></span> <span data-ttu-id="64f4b-130">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="64f4b-130">Select **Create**.</span></span>

      ![proporcionar valor de web y SQL](./media/resource-manager-export-template/provide-web-values.png)

<span data-ttu-id="64f4b-132">implementación de Hello puede tardar un minuto.</span><span class="sxs-lookup"><span data-stu-id="64f4b-132">hello deployment may take a minute.</span></span> <span data-ttu-id="64f4b-133">Una vez finalizada la implementación de hello, su suscripción contiene solución Hola.</span><span class="sxs-lookup"><span data-stu-id="64f4b-133">After hello deployment finishes, your subscription contains hello solution.</span></span>

## <a name="view-template-from-deployment-history"></a><span data-ttu-id="64f4b-134">Visualización de una plantilla desde el historial de implementaciones</span><span class="sxs-lookup"><span data-stu-id="64f4b-134">View template from deployment history</span></span>
1. <span data-ttu-id="64f4b-135">Vaya toohello hoja de grupo de recursos para el nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="64f4b-135">Go toohello resource group blade for your new resource group.</span></span> <span data-ttu-id="64f4b-136">Tenga en cuenta que esa hoja hello muestra el resultado de hello de última implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="64f4b-136">Notice that hello blade shows hello result of hello last deployment.</span></span> <span data-ttu-id="64f4b-137">Seleccione este vínculo.</span><span class="sxs-lookup"><span data-stu-id="64f4b-137">Select this link.</span></span>
   
      ![Hoja del grupo de recursos](./media/resource-manager-export-template/select-deployment.png)
2. <span data-ttu-id="64f4b-139">Ver un historial de las implementaciones para el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="64f4b-139">You see a history of deployments for hello group.</span></span> <span data-ttu-id="64f4b-140">En su caso, hoja de hello probablemente muestra solo una implementación.</span><span class="sxs-lookup"><span data-stu-id="64f4b-140">In your case, hello blade probably lists only one deployment.</span></span> <span data-ttu-id="64f4b-141">Selecciónela.</span><span class="sxs-lookup"><span data-stu-id="64f4b-141">Select this deployment.</span></span>
   
     ![última implementación](./media/resource-manager-export-template/select-history.png)
3. <span data-ttu-id="64f4b-143">hoja de Hello muestra un resumen de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="64f4b-143">hello blade displays a summary of hello deployment.</span></span> <span data-ttu-id="64f4b-144">Hola resumen incluye el estado de Hola de implementación de Hola y sus operaciones y los valores de hello proporcionada para los parámetros.</span><span class="sxs-lookup"><span data-stu-id="64f4b-144">hello summary includes hello status of hello deployment and its operations and hello values that you provided for parameters.</span></span> <span data-ttu-id="64f4b-145">plantilla de hello toosee que usó para la implementación de hello, seleccione **plantilla de vista**.</span><span class="sxs-lookup"><span data-stu-id="64f4b-145">toosee hello template that you used for hello deployment, select **View template**.</span></span>
   
     ![Ver el resumen de la implementación](./media/resource-manager-export-template/view-template.png)
4. <span data-ttu-id="64f4b-147">El Administrador de recursos recupera Hola siguientes siete archivos automáticamente:</span><span class="sxs-lookup"><span data-stu-id="64f4b-147">Resource Manager retrieves hello following seven files for you:</span></span>
   
   1. <span data-ttu-id="64f4b-148">**Plantilla** -plantilla de Hola que define la infraestructura de Hola para su solución.</span><span class="sxs-lookup"><span data-stu-id="64f4b-148">**Template** - hello template that defines hello infrastructure for your solution.</span></span> <span data-ttu-id="64f4b-149">Cuando crea la cuenta de almacenamiento de Hola a través del portal de Hola, Administrador de recursos usa una plantilla toodeploy y guarda dicha plantilla para futuras referencias.</span><span class="sxs-lookup"><span data-stu-id="64f4b-149">When you created hello storage account through hello portal, Resource Manager used a template toodeploy it and saved that template for future reference.</span></span>
   2. <span data-ttu-id="64f4b-150">**Parámetros** -un archivo de parámetros que puede utilizar toopass en valores durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="64f4b-150">**Parameters** - A parameter file that you can use toopass in values during deployment.</span></span> <span data-ttu-id="64f4b-151">Contiene valores de hello que proporcionó durante la primera implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="64f4b-151">It contains hello values that you provided during hello first deployment.</span></span> <span data-ttu-id="64f4b-152">Puede cambiar cualquiera de estos valores al volver a implementar la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="64f4b-152">You can change any of these values when you redeploy hello template.</span></span>
   3. <span data-ttu-id="64f4b-153">**CLI** -archivo de script de Azure comandos línea interfaz (CLI) que puede usar la plantilla de hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="64f4b-153">**CLI** - An Azure command-line-interface (CLI) script file that you can use toodeploy hello template.</span></span>
   3. <span data-ttu-id="64f4b-154">**CLI 2.0** -archivo de script de Azure comandos línea interfaz (CLI) que puede usar la plantilla de hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="64f4b-154">**CLI 2.0** - An Azure command-line-interface (CLI) script file that you can use toodeploy hello template.</span></span>
   4. <span data-ttu-id="64f4b-155">**PowerShell** -PowerShell de Azure un archivo de script que puede usar la plantilla de hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="64f4b-155">**PowerShell** - An Azure PowerShell script file that you can use toodeploy hello template.</span></span>
   5. <span data-ttu-id="64f4b-156">**.NET** -clase A .NET que puede usar la plantilla de hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="64f4b-156">**.NET** - A .NET class that you can use toodeploy hello template.</span></span>
   6. <span data-ttu-id="64f4b-157">**Ruby** -clase A Ruby que puede usar la plantilla de hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="64f4b-157">**Ruby** - A Ruby class that you can use toodeploy hello template.</span></span>
      
      <span data-ttu-id="64f4b-158">archivos de Hello están disponibles a través de vínculos a través de la hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="64f4b-158">hello files are available through links across hello blade.</span></span> <span data-ttu-id="64f4b-159">De forma predeterminada, hoja de hello muestra la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="64f4b-159">By default, hello blade displays hello template.</span></span>
      
       ![Ver plantilla](./media/resource-manager-export-template/see-template.png)
      
<span data-ttu-id="64f4b-161">Esta plantilla es plantilla real de hello usa toocreate su aplicación web y la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="64f4b-161">This template is hello actual template used toocreate your web app and SQL database.</span></span> <span data-ttu-id="64f4b-162">Tenga en cuenta que contiene parámetros que permiten valores diferentes tooprovide durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="64f4b-162">Notice it contains parameters that enable you tooprovide different values during deployment.</span></span> <span data-ttu-id="64f4b-163">toolearn más información acerca de la estructura de Hola de una plantilla, consulte [plantillas del Administrador de recursos de Azure de creación](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="64f4b-163">toolearn more about hello structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

## <a name="export-hello-template-from-resource-group"></a><span data-ttu-id="64f4b-164">Exportar plantilla Hola del grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="64f4b-164">Export hello template from resource group</span></span>
<span data-ttu-id="64f4b-165">Si manualmente ha cambiado los recursos o agregado recursos en varias implementaciones, la recuperación de una plantilla de historial de implementación de hello no refleja estado actual de Hola Hola del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="64f4b-165">If you have manually changed your resources or added resources in multiple deployments, retrieving a template from hello deployment history does not reflect hello current state of hello resource group.</span></span> <span data-ttu-id="64f4b-166">Esta sección muestra cómo tooexport una plantilla que refleja Hola estado actual del grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="64f4b-166">This section shows you how tooexport a template that reflects hello current state of hello resource group.</span></span> 

> [!NOTE]
> <span data-ttu-id="64f4b-167">No se puede exportar una plantilla a un grupo de recursos que tenga más de doscientos recursos.</span><span class="sxs-lookup"><span data-stu-id="64f4b-167">You cannot export a template for a resource group that has more than 200 resources.</span></span>
> 
> 

1. <span data-ttu-id="64f4b-168">plantilla de hello tooview para un grupo de recursos, seleccione **script de automatización**.</span><span class="sxs-lookup"><span data-stu-id="64f4b-168">tooview hello template for a resource group, select **Automation script**.</span></span>
   
      ![exportar grupo de recursos](./media/resource-manager-export-template/select-automation.png)
   
     <span data-ttu-id="64f4b-170">Administrador de recursos se evalúa como recursos de hello en el grupo de recursos de Hola y genera una plantilla para esos recursos.</span><span class="sxs-lookup"><span data-stu-id="64f4b-170">Resource Manager evaluates hello resources in hello resource group, and generates a template for those resources.</span></span> <span data-ttu-id="64f4b-171">No todos los tipos de recursos admiten la función de plantilla de exportación de Hola.</span><span class="sxs-lookup"><span data-stu-id="64f4b-171">Not all resource types support hello export template function.</span></span> <span data-ttu-id="64f4b-172">Puede ver un error que indica que hay un problema con la exportación de Hola.</span><span class="sxs-lookup"><span data-stu-id="64f4b-172">You may see an error stating that there is a problem with hello export.</span></span> <span data-ttu-id="64f4b-173">Obtener información sobre cómo toohandle los problemas en hello [problemas de exportación de corrección](#fix-export-issues) sección.</span><span class="sxs-lookup"><span data-stu-id="64f4b-173">You learn how toohandle those issues in hello [Fix export issues](#fix-export-issues) section.</span></span>
2. <span data-ttu-id="64f4b-174">Nuevo, verá seis archivos de Hola que puede usar la solución de hello tooredeploy.</span><span class="sxs-lookup"><span data-stu-id="64f4b-174">You again see hello six files that you can use tooredeploy hello solution.</span></span> <span data-ttu-id="64f4b-175">Sin embargo, esta plantilla en tiempo de hello es algo diferente.</span><span class="sxs-lookup"><span data-stu-id="64f4b-175">However, this time hello template is a little different.</span></span> <span data-ttu-id="64f4b-176">Tenga en cuenta que Hola plantilla generada contiene menos parámetros de plantilla de hello en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="64f4b-176">Notice that hello generated template contains fewer parameters than hello template in previous section.</span></span> <span data-ttu-id="64f4b-177">Además, muchos de los valores de hello (por ejemplo, ubicación y los valores SKU) están codificados en esta plantilla, en lugar de aceptar un valor de parámetro.</span><span class="sxs-lookup"><span data-stu-id="64f4b-177">Also, many of hello values (like location and SKU values) are hard-coded in this template rather than accepting a parameter value.</span></span> <span data-ttu-id="64f4b-178">Antes de volver a usar esta plantilla, puede ser conveniente tooedit Hola plantilla toomake un mejor uso de parámetros.</span><span class="sxs-lookup"><span data-stu-id="64f4b-178">Before reusing this template, you might want tooedit hello template toomake better use of parameters.</span></span> 
   
3. <span data-ttu-id="64f4b-179">Tiene dos opciones para continuar toowork con esta plantilla.</span><span class="sxs-lookup"><span data-stu-id="64f4b-179">You have a couple of options for continuing toowork with this template.</span></span> <span data-ttu-id="64f4b-180">Puede descargar la plantilla de Hola y trabajar con ella localmente con un editor de JSON.</span><span class="sxs-lookup"><span data-stu-id="64f4b-180">You can either download hello template and work on it locally with a JSON editor.</span></span> <span data-ttu-id="64f4b-181">O bien, puede guardar la biblioteca de plantillas tooyour de Hola y trabajar con ella a través del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="64f4b-181">Or, you can save hello template tooyour library and work on it through hello portal.</span></span>
   
     <span data-ttu-id="64f4b-182">Si está familiarizado con un editor de JSON como [VS Code](https://code.visualstudio.com/) o [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), podría ser preferible Descargar plantilla de hello localmente y usar ese editor.</span><span class="sxs-lookup"><span data-stu-id="64f4b-182">If you are comfortable using a JSON editor like [VS Code](https://code.visualstudio.com/) or [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), you might prefer downloading hello template locally and using that editor.</span></span> <span data-ttu-id="64f4b-183">toowork localmente, seleccione **descargar**.</span><span class="sxs-lookup"><span data-stu-id="64f4b-183">toowork locally, select **Download**.</span></span>
   
      ![Descargar plantilla](./media/resource-manager-export-template/download-template.png)
   
     <span data-ttu-id="64f4b-185">Si no se configuran con un editor de JSON, quizá prefiera Editar plantilla de Hola a través del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="64f4b-185">If you are not set up with a JSON editor, you might prefer editing hello template through hello portal.</span></span> <span data-ttu-id="64f4b-186">resto de Hola de este tema se da por supuesto que ha guardado tooyour biblioteca de plantillas de hello en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="64f4b-186">hello remainder of this topic assumes you have saved hello template tooyour library in hello portal.</span></span> <span data-ttu-id="64f4b-187">Sin embargo, asegúrese de Hola mismo cambios de sintaxis toohello plantilla si trabajar localmente con un editor de JSON o a través del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="64f4b-187">However, you make hello same syntax changes toohello template whether working locally with a JSON editor or through hello portal.</span></span> <span data-ttu-id="64f4b-188">Seleccione toowork a través del portal de hello, **agregar toolibrary**.</span><span class="sxs-lookup"><span data-stu-id="64f4b-188">toowork through hello portal, select **Add toolibrary**.</span></span>
   
      ![Agregar toolibrary](./media/resource-manager-export-template/add-to-library.png)
   
     <span data-ttu-id="64f4b-190">Al agregar una biblioteca de plantillas de toohello, asigne el libro de hello un nombre y una descripción.</span><span class="sxs-lookup"><span data-stu-id="64f4b-190">When adding a template toohello library, give hello template a name and description.</span></span> <span data-ttu-id="64f4b-191">Después, seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="64f4b-191">Then, select **Save**.</span></span>
   
     ![establecer valores de plantilla](./media/resource-manager-export-template/save-library-template.png)
4. <span data-ttu-id="64f4b-193">tooview una plantilla que se guardan en la biblioteca, seleccione **más servicios**, tipo **plantillas** toofilter resultados, seleccionados **plantillas**.</span><span class="sxs-lookup"><span data-stu-id="64f4b-193">tooview a template saved in your library, select **More services**, type **Templates** toofilter results, select **Templates**.</span></span>
   
      ![buscar plantillas](./media/resource-manager-export-template/find-templates.png)
5. <span data-ttu-id="64f4b-195">Seleccione la plantilla de hello con nombre hello guardó.</span><span class="sxs-lookup"><span data-stu-id="64f4b-195">Select hello template with hello name you saved.</span></span>
   
      ![seleccionar plantilla](./media/resource-manager-export-template/select-saved-template.png)

## <a name="customize-hello-template"></a><span data-ttu-id="64f4b-197">Personalizar la plantilla de Hola</span><span class="sxs-lookup"><span data-stu-id="64f4b-197">Customize hello template</span></span>
<span data-ttu-id="64f4b-198">plantilla de Hola exportado funciona bien que si desea toocreate Hola mismo web de aplicación y base de datos SQL para cada implementación.</span><span class="sxs-lookup"><span data-stu-id="64f4b-198">hello exported template works fine if you want toocreate hello same web app and SQL database for every deployment.</span></span> <span data-ttu-id="64f4b-199">No obstante, Resource Manager proporciona opciones para que pueda implementar plantillas con mucha más flexibilidad.</span><span class="sxs-lookup"><span data-stu-id="64f4b-199">However, Resource Manager provides options so that you can deploy templates with a lot more flexibility.</span></span> <span data-ttu-id="64f4b-200">Este artículo muestra cómo la base de parámetros de tooadd para hello datos nombre de administrador y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="64f4b-200">This article shows you how tooadd parameters for hello database administrator name and password.</span></span> <span data-ttu-id="64f4b-201">Puede utilizar este mismo tooadd enfoque más flexibilidad para otros valores en plantilla Hola.</span><span class="sxs-lookup"><span data-stu-id="64f4b-201">You can use this same approach tooadd more flexibility for other values in hello template.</span></span>

1. <span data-ttu-id="64f4b-202">plantilla de toocustomize hello, seleccione **editar**.</span><span class="sxs-lookup"><span data-stu-id="64f4b-202">toocustomize hello template, select **Edit**.</span></span>
   
     ![mostrar plantilla](./media/resource-manager-export-template/select-edit.png)
2. <span data-ttu-id="64f4b-204">Seleccione la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="64f4b-204">Select hello template.</span></span>
   
     ![editar plantilla](./media/resource-manager-export-template/select-added-template.png)
3. <span data-ttu-id="64f4b-206">valores de hello toopass capaz de toobe que puede querer toospecify durante la implementación, agregan Hola siguiendo dos toohello parámetros **parámetros** sección en la plantilla de hello:</span><span class="sxs-lookup"><span data-stu-id="64f4b-206">toobe able toopass hello values that you might want toospecify during deployment, add hello following two parameters toohello **parameters** section in hello template:</span></span>

   ```json
   "administratorLogin": {
       "type": "String"
   },
   "administratorLoginPassword": {
       "type": "SecureString"
   },
   ```

4. <span data-ttu-id="64f4b-207">toouse Hola nuevos parámetros, reemplace la definición de SQL server de Hola Hola **recursos** sección.</span><span class="sxs-lookup"><span data-stu-id="64f4b-207">toouse hello new parameters, replace hello SQL server definition in hello **resources** section.</span></span> <span data-ttu-id="64f4b-208">Tenga en cuenta que **administratorLogin** y **administratorLoginPassword** ahora usan los valores de los parámetros.</span><span class="sxs-lookup"><span data-stu-id="64f4b-208">Notice that **administratorLogin** and **administratorLoginPassword** now use parameter values.</span></span>

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

6. <span data-ttu-id="64f4b-209">Seleccione **Aceptar** cuando termine de editar plantillas de Hola.</span><span class="sxs-lookup"><span data-stu-id="64f4b-209">Select **OK** when you are done editing hello template.</span></span>
7. <span data-ttu-id="64f4b-210">Seleccione **guardar** plantilla toohello cambios hello en toosave.</span><span class="sxs-lookup"><span data-stu-id="64f4b-210">Select **Save** toosave hello changes toohello template.</span></span>
   
     ![guardar plantilla](./media/resource-manager-export-template/save-template.png)
8. <span data-ttu-id="64f4b-212">plantilla de tooredeploy Hola actualizado, seleccione **implementar**.</span><span class="sxs-lookup"><span data-stu-id="64f4b-212">tooredeploy hello updated template, select **Deploy**.</span></span>
   
     ![implementar plantilla](./media/resource-manager-export-template/redeploy-template.png)
9. <span data-ttu-id="64f4b-214">Proporcionar valores de parámetros y seleccione un grupo toodeploy Hola de recursos a.</span><span class="sxs-lookup"><span data-stu-id="64f4b-214">Provide parameter values, and select a resource group toodeploy hello resources to.</span></span>


## <a name="fix-export-issues"></a><span data-ttu-id="64f4b-215">Solución de problemas de exportación</span><span class="sxs-lookup"><span data-stu-id="64f4b-215">Fix export issues</span></span>
<span data-ttu-id="64f4b-216">No todos los tipos de recursos admiten la función de plantilla de exportación de Hola.</span><span class="sxs-lookup"><span data-stu-id="64f4b-216">Not all resource types support hello export template function.</span></span> <span data-ttu-id="64f4b-217">tooresolve manualmente este problema vuelva a agregar los recursos que faltan de Hola a la plantilla.</span><span class="sxs-lookup"><span data-stu-id="64f4b-217">tooresolve this issue, manually add hello missing resources back into your template.</span></span> <span data-ttu-id="64f4b-218">mensaje de error de Hello incluye tipos de recursos de Hola que no se puede exportar.</span><span class="sxs-lookup"><span data-stu-id="64f4b-218">hello error message includes hello resource types that cannot be exported.</span></span> <span data-ttu-id="64f4b-219">Busque el tipo de recurso en [Referencia de plantilla](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="64f4b-219">Find that resource type in [Template reference](/azure/templates/).</span></span> <span data-ttu-id="64f4b-220">Por ejemplo, toomanually agregar una puerta de enlace de red virtual, vea [referencia de plantillas de Microsoft.Network/virtualNetworkGateways](/azure/templates/microsoft.network/virtualnetworkgateways).</span><span class="sxs-lookup"><span data-stu-id="64f4b-220">For example, toomanually add a virtual network gateway, see [Microsoft.Network/virtualNetworkGateways template reference](/azure/templates/microsoft.network/virtualnetworkgateways).</span></span>

> [!NOTE]
> <span data-ttu-id="64f4b-221">Solo se encuentran problemas de exportación si se exporta desde un grupo de recursos en lugar de desde el historial de implementación.</span><span class="sxs-lookup"><span data-stu-id="64f4b-221">You only encounter export issues when exporting from a resource group rather than from your deployment history.</span></span> <span data-ttu-id="64f4b-222">Si la última implementación representa con precisión el estado actual de Hola Hola del grupo de recursos, debe exportar plantilla Hola de historial de implementación de hello en lugar de grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="64f4b-222">If your last deployment accurately represents hello current state of hello resource group, you should export hello template from hello deployment history rather than from hello resource group.</span></span> <span data-ttu-id="64f4b-223">Exportar sólo desde un grupo de recursos cuando haya realizado el grupo de recursos de toohello de cambios que no estén definidos en una única plantilla.</span><span class="sxs-lookup"><span data-stu-id="64f4b-223">Only export from a resource group when you have made changes toohello resource group that are not defined in a single template.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="64f4b-224">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="64f4b-224">Next steps</span></span>
<span data-ttu-id="64f4b-225">Ha aprendido cómo tooexport una plantilla de recursos que creó en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="64f4b-225">You have learned how tooexport a template from resources that you created in hello portal.</span></span>

* <span data-ttu-id="64f4b-226">Puede implementar una plantilla mediante [PowerShell](resource-group-template-deploy.md), [CLI de Azure](resource-group-template-deploy-cli.md), o [API de REST](resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="64f4b-226">You can deploy a template through [PowerShell](resource-group-template-deploy.md), [Azure CLI](resource-group-template-deploy-cli.md), or [REST API](resource-group-template-deploy-rest.md).</span></span>
* <span data-ttu-id="64f4b-227">toosee tooexport una plantilla a través de PowerShell, vea [con Azure PowerShell con el Administrador de recursos de Azure](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="64f4b-227">toosee how tooexport a template through PowerShell, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="64f4b-228">toosee tooexport una plantilla mediante la CLI de Azure, vea [Hola Utilice CLI de Azure para Mac, Linux y Windows con el Administrador de recursos de Azure](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="64f4b-228">toosee how tooexport a template through Azure CLI, see [Use hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>

