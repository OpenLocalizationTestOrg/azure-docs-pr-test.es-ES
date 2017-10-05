---
title: "Introducción a las plantillas privadas | Microsoft Docs"
description: Agregue, administre y comparta plantillas privadas con el Portal de Azure, con la CLI de Azure o con PowerShell.
services: marketplace-customer
documentationcenter: 
author: VybavaRamadoss
manager: asimm
editor: 
tags: marketplace, azure-resource-manager
keywords: 
ms.assetid: 6ec20778-b578-4885-acb5-104b0e51ea1a
ms.service: marketplace
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: vybavar
ms.openlocfilehash: 01657619cbe579c6818a790cc3ab95a33936a565
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-private-templates-on-the-azure-portal"></a><span data-ttu-id="171fb-103">Introducción a las plantillas privadas del Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="171fb-103">Get started with private Templates on the Azure Portal</span></span>
<span data-ttu-id="171fb-104">Las plantillas de [Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) son plantillas declarativas que se utilizan para definir la implementación.</span><span class="sxs-lookup"><span data-stu-id="171fb-104">An [Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) template is a declarative template used to define your deployment.</span></span> <span data-ttu-id="171fb-105">Puede definir los recursos que se van a implementar en una solución y especificar parámetros y variables que le permitan especificar valores de entrada para diferentes entornos.</span><span class="sxs-lookup"><span data-stu-id="171fb-105">You can define the resources to deploy for a solution, and specify parameters and variables that enable you to input values for different environments.</span></span> <span data-ttu-id="171fb-106">La plantilla consta de JSON y expresiones que puede usar para generar valores para su implementación.</span><span class="sxs-lookup"><span data-stu-id="171fb-106">The template consists of JSON and expressions which you can use to construct values for your deployment.</span></span>

<span data-ttu-id="171fb-107">Puede usar la nueva funcionalidad **Plantillas** de [Azure Portal](https://portal.azure.com) junto con el proveedor de recursos **Microsoft.Gallery** como una extensión de [Azure Marketplace](https://azure.microsoft.com/marketplace/) para que los usuarios puedan crear, administrar e implementar plantillas privadas procedentes de una biblioteca personal.</span><span class="sxs-lookup"><span data-stu-id="171fb-107">You can use the new **Templates** capability in the [Azure Portal](https://portal.azure.com) along with the **Microsoft.Gallery** resource provider as an extension of the [Azure Marketplace](https://azure.microsoft.com/marketplace/) to enable users to create, manage and deploy private templates from a personal library.</span></span>

<span data-ttu-id="171fb-108">En este documento, se explica paso a paso cómo agregar, administrar y compartir una **plantilla** privada mediante el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="171fb-108">This document walks you through adding, managing and sharing a private **Template** using the Azure Portal.</span></span>

## <a name="guidance"></a><span data-ttu-id="171fb-109">Guía</span><span class="sxs-lookup"><span data-stu-id="171fb-109">Guidance</span></span>
<span data-ttu-id="171fb-110">Las sugerencias siguientes le ayudarán a sacar el máximo provecho de las **plantillas** cuando trabaje en sus soluciones:</span><span class="sxs-lookup"><span data-stu-id="171fb-110">The following suggestions will help you take full advantage of **Templates** when working with your solutions:</span></span>

* <span data-ttu-id="171fb-111">Una **plantilla** en un recurso de encapsulamiento que contiene una plantilla de Resource Manager y otros metadatos.</span><span class="sxs-lookup"><span data-stu-id="171fb-111">A **Template** is an encapsulating resource that contains an Resource Manager template and additional metadata.</span></span> <span data-ttu-id="171fb-112">Su comportamiento es muy similar al de los elementos de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="171fb-112">It behaves very similarly to an item in the Marketplace.</span></span> <span data-ttu-id="171fb-113">La principal diferencia es que se trata de un elemento privado, mientras que los elementos de Marketplace son públicos.</span><span class="sxs-lookup"><span data-stu-id="171fb-113">The key difference is that it is a private item as opposed to the public Marketplace items.</span></span>
* <span data-ttu-id="171fb-114">La biblioteca **Plantillas** resulta muy útil para los usuarios que necesitan personalizar sus implementaciones.</span><span class="sxs-lookup"><span data-stu-id="171fb-114">The **Templates** library works well for users who need to customize their deployments.</span></span>
* <span data-ttu-id="171fb-115">**plantillas** son apropiadas para los usuarios que necesitan disponer de un repositorio sencillo dentro de Azure.</span><span class="sxs-lookup"><span data-stu-id="171fb-115">**Templates** work well for users who need a simple repository within Azure.</span></span>
* <span data-ttu-id="171fb-116">Para empezar, utilice una plantilla de Resource Manager existente.</span><span class="sxs-lookup"><span data-stu-id="171fb-116">Start with an existing Resource Manager template.</span></span> <span data-ttu-id="171fb-117">Para buscar plantillas, utilice [github](https://github.com/Azure/azure-quickstart-templates) o [Exportar plantilla](../azure-resource-manager/resource-manager-export-template.md) desde un grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="171fb-117">Find templates in [github](https://github.com/Azure/azure-quickstart-templates) or [Export template](../azure-resource-manager/resource-manager-export-template.md) from an existing resource group.</span></span>
* <span data-ttu-id="171fb-118">**plantillas** están vinculadas al usuario que las publica.</span><span class="sxs-lookup"><span data-stu-id="171fb-118">**Templates** are tied to the user who publishes them.</span></span> <span data-ttu-id="171fb-119">Cualquier persona que tenga acceso podrá ver el nombre del publicador.</span><span class="sxs-lookup"><span data-stu-id="171fb-119">The publisher name is visible to everyone who has read access to it.</span></span>
* <span data-ttu-id="171fb-120">**plantillas** son recursos de Resource Manager y, una vez publicadas, su nombre no se puede modificar.</span><span class="sxs-lookup"><span data-stu-id="171fb-120">**Templates** are Resource Manager resources and cannot be renamed once published.</span></span>

## <a name="add-a-template-resource"></a><span data-ttu-id="171fb-121">Adición de un recurso de plantilla</span><span class="sxs-lookup"><span data-stu-id="171fb-121">Add a Template resource</span></span>
<span data-ttu-id="171fb-122">Existen dos formas de crear un recurso de **plantilla** en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="171fb-122">There are two ways to create a **Template** resource in the Azure portal.</span></span>

### <a name="method-1--create-a-new-template-resource-from-a-running-resource-group"></a><span data-ttu-id="171fb-123">Método 1: Creación de un nuevo recurso de plantilla a partir de un grupo de recursos en funcionamiento</span><span class="sxs-lookup"><span data-stu-id="171fb-123">Method 1 : Create a new Template resource from a running resource group</span></span>
1. <span data-ttu-id="171fb-124">Acceda a un grupo de recursos existente del Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="171fb-124">Navigate to an existing resource group on the Azure Portal.</span></span> <span data-ttu-id="171fb-125">En **Configuración**, seleccione **Exportar plantilla**.</span><span class="sxs-lookup"><span data-stu-id="171fb-125">Select **Export template** in **Settings**.</span></span>
2. <span data-ttu-id="171fb-126">Cuando la plantilla de Resource Manager se haya exportado, utilice el botón **Guardar plantilla** para guardarla en el repositorio **Plantillas**.</span><span class="sxs-lookup"><span data-stu-id="171fb-126">Once the Resource Manager template is exported, use the **Save Template** button to save it to the **Templates** repository.</span></span> <span data-ttu-id="171fb-127">Para más detalles sobre la exportación de plantillas, haga clic [aquí](../azure-resource-manager/resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="171fb-127">Find complete details for Export template [here](../azure-resource-manager/resource-manager-export-template.md).</span></span>
   <br /><br /><span data-ttu-id="171fb-128">
   ![Exportación de grupo de recursos](media/rg-export-portal1.PNG)</span><span class="sxs-lookup"><span data-stu-id="171fb-128">
![Resource group export](media/rg-export-portal1.PNG)</span></span>  <br />
3. <span data-ttu-id="171fb-129">Seleccione el botón de comando **Guardar plantilla** .</span><span class="sxs-lookup"><span data-stu-id="171fb-129">Select the **Save to Template** command button.</span></span>
   <br /><br />
4. <span data-ttu-id="171fb-130">Escriba la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="171fb-130">Enter the following information:</span></span>
   
   * <span data-ttu-id="171fb-131">Nombre: nombre del objeto de plantilla (NOTA: El nombre debe ajustarse a las especificaciones de Azure Resource Manager,</span><span class="sxs-lookup"><span data-stu-id="171fb-131">Name – Name of the template object (NOTE: This is an Azure Resource Manager based name.</span></span> <span data-ttu-id="171fb-132">por lo que se aplicarán todas las restricciones de nomenclatura, y no se puede cambiar una vez creado).</span><span class="sxs-lookup"><span data-stu-id="171fb-132">All naming restrictions apply and it cannot be changed once created).</span></span>
   * <span data-ttu-id="171fb-133">Descripción: resumen rápido de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="171fb-133">Description – Quick summary about the template.</span></span>
     
     ![Guardar plantilla](media/save-template-portal1.PNG)  <br />
5. <span data-ttu-id="171fb-135">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="171fb-135">Click **Save**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="171fb-136">Si la plantilla de Resource Manager exportada contiene errores, aparecerán notificaciones en la hoja Exportar plantilla; sin embargo, a pesar de los errores, podrá guardarla en Plantillas.</span><span class="sxs-lookup"><span data-stu-id="171fb-136">The Export template blade shows notifications when the exported Resource Manager template has errors, but you will still be able to save this Resource Manager template to the Templates.</span></span> <span data-ttu-id="171fb-137">No olvide comprobar y corregir los problemas antes de volver a implementar la plantilla de Resource Manager exportada.</span><span class="sxs-lookup"><span data-stu-id="171fb-137">Ensure that you check and fix any Resource Manager template issues before redeploying the exported Resource Manager template.</span></span>
   > 
   > 

### <a name="method-2--add-a-new-template-resource-from-browse"></a><span data-ttu-id="171fb-138">Método 2 : Agregar un nuevo recurso de plantilla desde Examinar</span><span class="sxs-lookup"><span data-stu-id="171fb-138">Method 2 : Add a new Template resource from browse</span></span>
<span data-ttu-id="171fb-139">También puede agregar una nueva **plantilla** desde el principio utilizando el botón de comando +Agregar de **Examinar > Plantillas**.</span><span class="sxs-lookup"><span data-stu-id="171fb-139">You can also add a new **Template** from scratch using the +Add command button in **Browse > Templates**.</span></span> <span data-ttu-id="171fb-140">Tendrá que especificar un nombre, una descripción y el JSON de la plantilla de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="171fb-140">You will need to provide a Name, Description and the Resource Manager template JSON.</span></span>

![Agregar plantilla](media/add-template-portal1.PNG)  <br />

> [!NOTE]
> <span data-ttu-id="171fb-142">Microsoft.Gallery es un proveedor de recursos de Azure basado en un inquilino.</span><span class="sxs-lookup"><span data-stu-id="171fb-142">Microsoft.Gallery is a Tenant based Azure resource provider.</span></span> <span data-ttu-id="171fb-143">El recurso de plantilla está vinculado al usuario que lo creó.</span><span class="sxs-lookup"><span data-stu-id="171fb-143">The Template resource is tied to the user who created it.</span></span> <span data-ttu-id="171fb-144">No está asociado a ninguna suscripción específica.</span><span class="sxs-lookup"><span data-stu-id="171fb-144">It is not tied to any specific subscription.</span></span> <span data-ttu-id="171fb-145">Al implementar una plantilla, es necesario elegir una suscripción.</span><span class="sxs-lookup"><span data-stu-id="171fb-145">A subscription needs to be chosen only when deploying a Template.</span></span>
> 
> 

## <a name="view-template-resources"></a><span data-ttu-id="171fb-146">Consulta de los recursos de plantilla</span><span class="sxs-lookup"><span data-stu-id="171fb-146">View Template resources</span></span>
<span data-ttu-id="171fb-147">Puede ver todas las **plantillas** disponibles en **Examinar > Plantillas**.</span><span class="sxs-lookup"><span data-stu-id="171fb-147">All **Templates** available to you can be seen at **Browse > Templates**.</span></span> <span data-ttu-id="171fb-148">Aquí encontrará las **plantillas** que ha creado, así como las plantillas que han compartido con usted y que tienen distintos niveles de permisos.</span><span class="sxs-lookup"><span data-stu-id="171fb-148">This includes **Templates** you have created as well as ones that have been shared with you with varying levels of permissions.</span></span> <span data-ttu-id="171fb-149">Para más detalles, consulte más adelante la sección [Control de acceso](#access-control-for-a-tenant-resource-provider) .</span><span class="sxs-lookup"><span data-stu-id="171fb-149">More details in the [access control](#access-control-for-a-tenant-resource-provider) section below.</span></span>

![Ver plantilla](media/view-template-portal1.PNG)  <br />

<span data-ttu-id="171fb-151">Para ver los detalles de una **plantilla** , haga clic en un elemento de la lista.</span><span class="sxs-lookup"><span data-stu-id="171fb-151">You can view the details of a **Template** by clicking into an item in the list.</span></span>

![Ver plantilla](media/view-template-portal2c.png)  <br />

## <a name="edit-a-template-resource"></a><span data-ttu-id="171fb-153">Edición de un recurso de plantilla</span><span class="sxs-lookup"><span data-stu-id="171fb-153">Edit a Template resource</span></span>
<span data-ttu-id="171fb-154">Para iniciar el flujo de edición de una **plantilla** , haga clic con el botón derecho en el elemento de la lista o seleccione el botón de comando Editar.</span><span class="sxs-lookup"><span data-stu-id="171fb-154">You can initiate the edit flow for a **Template** by right clicking the item on the Browse list or by choosing the Edit command button.</span></span>

![Editar plantilla](media/edit-template-portal1a.PNG)  <br />

<span data-ttu-id="171fb-156">Puede editar la descripción o el texto de la plantilla de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="171fb-156">You can edit the description or Resource Manager template text.</span></span> <span data-ttu-id="171fb-157">No obstante, el nombre no se puede modificar, ya que se trata de un nombre de recurso de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="171fb-157">You cannot edit the name since it is an Resource Manager resource name.</span></span> <span data-ttu-id="171fb-158">Cuando edite el JSON de la plantilla de Resource Manager, realizaremos las comprobaciones pertinentes para garantizar que se trata de un JSON válido.</span><span class="sxs-lookup"><span data-stu-id="171fb-158">When you edit the Resource Manager template JSON we will validate to ensure that it is valid JSON.</span></span> <span data-ttu-id="171fb-159">Elija **Aceptar** y **Guardar** para guardar la plantilla actualizada.</span><span class="sxs-lookup"><span data-stu-id="171fb-159">Choose **OK** and then **Save** to save your updated template.</span></span>

![Editar plantilla](media/edit-template-portal2a.PNG)  <br />

<span data-ttu-id="171fb-161">Cuando haya guardado la **plantilla** , aparecerá una notificación de confirmación.</span><span class="sxs-lookup"><span data-stu-id="171fb-161">Once the **Template** is saved you will see a confirmation notification.</span></span>

![Editar plantilla](media/edit-template-portal3b.png)  <br />

## <a name="deploy-a-template-resource"></a><span data-ttu-id="171fb-163">Implementación de un recurso de plantilla</span><span class="sxs-lookup"><span data-stu-id="171fb-163">Deploy a Template resource</span></span>
<span data-ttu-id="171fb-164">Puede implementar cualquier **plantilla** en la que tenga permisos de **lectura**.</span><span class="sxs-lookup"><span data-stu-id="171fb-164">You can deploy any **Template** that you have **Read** permissions on.</span></span> <span data-ttu-id="171fb-165">El flujo de implementación abre la hoja de implementación de plantillas estándar de Azure.</span><span class="sxs-lookup"><span data-stu-id="171fb-165">The deployment flow launches the standard Azure Template deployment blade.</span></span> <span data-ttu-id="171fb-166">Rellene los valores de los parámetros de la plantilla de Resource Manager para continuar con la implementación.</span><span class="sxs-lookup"><span data-stu-id="171fb-166">Fill out the values for the Resource Manager template parameters to proceed with the deployment.</span></span>

![Implementar plantilla](media/deploy-template-portal1b.png)  <br />

## <a name="share-a-template-resource"></a><span data-ttu-id="171fb-168">Uso compartido de un recurso de plantilla</span><span class="sxs-lookup"><span data-stu-id="171fb-168">Share a Template resource</span></span>
<span data-ttu-id="171fb-169">Puede compartir con sus compañeros los recursos de **plantilla** .</span><span class="sxs-lookup"><span data-stu-id="171fb-169">A **Template** resource can be shared with your peers.</span></span> <span data-ttu-id="171fb-170">El proceso de uso compartido es similar a la [asignación de roles en recursos de Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="171fb-170">Sharing behaves similarly to [role assignment for any resource on Azure](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="171fb-171">El propietario de la **plantilla** proporciona permisos a otros usuarios para que puedan interactuar con el recurso de plantilla.</span><span class="sxs-lookup"><span data-stu-id="171fb-171">The **Template** owner provides permissions to other users who can interact with a Template resource.</span></span> <span data-ttu-id="171fb-172">La persona o el grupo de personas con los que se comparte la **plantilla** pueden ver la plantilla de Resource Manager y las propiedades de la galería.</span><span class="sxs-lookup"><span data-stu-id="171fb-172">The person or group of people you share the **Template** with will be able to see the Resource Manager template and its gallery properties.</span></span>

### <a name="access-control-for-the-microsoftgallery-resources"></a><span data-ttu-id="171fb-173">Control de acceso en los recursos de Microsoft.Gallery</span><span class="sxs-lookup"><span data-stu-id="171fb-173">Access control for the Microsoft.Gallery resources</span></span>
| <span data-ttu-id="171fb-174">Rol</span><span class="sxs-lookup"><span data-stu-id="171fb-174">Role</span></span> | <span data-ttu-id="171fb-175">Permisos</span><span class="sxs-lookup"><span data-stu-id="171fb-175">Permissions</span></span> |
| --- | --- |
| <span data-ttu-id="171fb-176">Propietario</span><span class="sxs-lookup"><span data-stu-id="171fb-176">Owner</span></span> |<span data-ttu-id="171fb-177">Tiene todo el control sobre el recurso de plantilla, por lo que puede compartirlo.</span><span class="sxs-lookup"><span data-stu-id="171fb-177">Allows full control on the Template resource including Share</span></span> |
| <span data-ttu-id="171fb-178">Lector</span><span class="sxs-lookup"><span data-stu-id="171fb-178">Reader</span></span> |<span data-ttu-id="171fb-179">Tiene permiso de lectura y ejecución (implementación) en el recurso de plantilla.</span><span class="sxs-lookup"><span data-stu-id="171fb-179">Allows Read and Execute(Deploy) on the Template resource</span></span> |
| <span data-ttu-id="171fb-180">Colaborador</span><span class="sxs-lookup"><span data-stu-id="171fb-180">Contributor</span></span> |<span data-ttu-id="171fb-181">Tiene permiso de edición y eliminación en el recurso de plantilla.</span><span class="sxs-lookup"><span data-stu-id="171fb-181">Allows Edit and Delete permission on the Template resource.</span></span> <span data-ttu-id="171fb-182">El usuario no puede compartir la plantilla con otras personas.</span><span class="sxs-lookup"><span data-stu-id="171fb-182">User cannot Share the Template with others</span></span> |

<span data-ttu-id="171fb-183">Seleccione **Compartir** haciendo clic con el botón derecho en el elemento de la lista o en la hoja de vista de un elemento específico.</span><span class="sxs-lookup"><span data-stu-id="171fb-183">Select **Share** on the browse item by right clicking or on the view blade of a specific item.</span></span> <span data-ttu-id="171fb-184">De este modo, se iniciará un proceso que le permitirá compartir el recurso de plantilla.</span><span class="sxs-lookup"><span data-stu-id="171fb-184">This launches a Share experience.</span></span>

![Compartir plantilla](media/share-template-portal1a.png)  <br />

 <span data-ttu-id="171fb-186">Ahora, puede elegir un rol y un usuario o grupo para concederles acceso a una determinada **plantilla**.</span><span class="sxs-lookup"><span data-stu-id="171fb-186">You can now choose a role and a user or group to provide access to a particular **Template**.</span></span> <span data-ttu-id="171fb-187">Los roles disponibles son Propietario, Lector y Colaborador.</span><span class="sxs-lookup"><span data-stu-id="171fb-187">The available roles are Owner, Reader and Contributor.</span></span> <span data-ttu-id="171fb-188">Para más detalles, consulte la sección [Control de acceso](#access-control-for-a-tenant-resource-provider) que apareció anteriormente.</span><span class="sxs-lookup"><span data-stu-id="171fb-188">More details in the [access control](#access-control-for-a-tenant-resource-provider) section above.</span></span>

![Compartir plantilla](media/share-template-portal2b.png)  <br />

![Compartir plantilla](media/share-template-portal3b.png)  <br />

<span data-ttu-id="171fb-191">Haga clic en **Seleccionar** y en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="171fb-191">Click **Select** and **Ok**.</span></span> <span data-ttu-id="171fb-192">Ahora, puede ver los usuarios o grupos que ha agregado al recurso.</span><span class="sxs-lookup"><span data-stu-id="171fb-192">You can now see the users or groups you added to the resource.</span></span>

![Compartir plantilla](media/share-template-portal4b.png)  <br />

> [!NOTE]
> <span data-ttu-id="171fb-194">Las plantillas solo se pueden compartir con usuarios y grupos del mismo inquilino de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="171fb-194">A Template can only be shared with users and groups in the same Azure Active Directory tenant.</span></span> <span data-ttu-id="171fb-195">Si comparte una plantilla con una dirección de correo electrónico que no se encuentra en el inquilino, se enviará una invitación al usuario para que se una a este inquilino como invitado.</span><span class="sxs-lookup"><span data-stu-id="171fb-195">If you share a Template with an email address that is not in your tenant, an invitation will be sent asking the user to join the tenant as a guest.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="171fb-196">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="171fb-196">Next steps</span></span>
* <span data-ttu-id="171fb-197">Para más información sobre la creación de plantillas de Resource Manager, consulte [Creación de plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="171fb-197">To learn about creating Resource Manager templates, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="171fb-198">Para conocer las funciones que puede usar en la plantilla de Resource Manager, consulte [Funciones de plantilla de Azure Resource Manager](../azure-resource-manager/resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="171fb-198">To understand the functions you can use in an Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md)</span></span>
* <span data-ttu-id="171fb-199">Para obtener instrucciones sobre cómo diseñar las plantillas, consulte [Prácticas recomendadas para diseñar plantillas del Administrador de recursos de Azure](../azure-resource-manager/best-practices-resource-manager-design-templates.md)</span><span class="sxs-lookup"><span data-stu-id="171fb-199">For guidance on designing your templates, see [Best practices for designing Azure Resource Manager templates](../azure-resource-manager/best-practices-resource-manager-design-templates.md)</span></span>

