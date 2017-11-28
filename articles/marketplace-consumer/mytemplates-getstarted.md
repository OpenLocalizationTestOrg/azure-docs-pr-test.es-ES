---
title: aaaGet a trabajar con plantillas privadas | Documentos de Microsoft
description: Agregar, administrar y compartir sus plantillas privadas con hello portal de Azure, hello Azure CLI o PowerShell.
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
ms.openlocfilehash: 1fe2c6422f62a98f7ae9ba5c61b9639d993f0bca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-private-templates-on-hello-azure-portal"></a><span data-ttu-id="b93bb-103">Empezar a trabajar con plantillas privadas en hello Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="b93bb-103">Get started with private Templates on hello Azure Portal</span></span>
<span data-ttu-id="b93bb-104">Un [Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) plantilla es una plantilla declarativa usa toodefine la implementación.</span><span class="sxs-lookup"><span data-stu-id="b93bb-104">An [Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) template is a declarative template used toodefine your deployment.</span></span> <span data-ttu-id="b93bb-105">Puede definir hello toodeploy de recursos para una solución y especificar los parámetros y variables que le permiten tooinput valores para diferentes entornos.</span><span class="sxs-lookup"><span data-stu-id="b93bb-105">You can define hello resources toodeploy for a solution, and specify parameters and variables that enable you tooinput values for different environments.</span></span> <span data-ttu-id="b93bb-106">Hello plantilla consta de JSON y expresiones que se pueden utilizar valores de tooconstruct para su implementación.</span><span class="sxs-lookup"><span data-stu-id="b93bb-106">hello template consists of JSON and expressions which you can use tooconstruct values for your deployment.</span></span>

<span data-ttu-id="b93bb-107">Puede usar nueva hello **plantillas** capacidad en hello [Portal de Azure](https://portal.azure.com) junto con hello **Microsoft.Gallery** proveedor de recursos como una extensión de hello [ Azure Marketplace](https://azure.microsoft.com/marketplace/) tooenable toocreate de los usuarios, administrar e implementar plantillas privadas desde una biblioteca personal.</span><span class="sxs-lookup"><span data-stu-id="b93bb-107">You can use hello new **Templates** capability in hello [Azure Portal](https://portal.azure.com) along with hello **Microsoft.Gallery** resource provider as an extension of hello [Azure Marketplace](https://azure.microsoft.com/marketplace/) tooenable users toocreate, manage and deploy private templates from a personal library.</span></span>

<span data-ttu-id="b93bb-108">Este documento le guía a través de agregar, administrar y compartir una privada **plantilla** utilizando Hola Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b93bb-108">This document walks you through adding, managing and sharing a private **Template** using hello Azure Portal.</span></span>

## <a name="guidance"></a><span data-ttu-id="b93bb-109">Guía</span><span class="sxs-lookup"><span data-stu-id="b93bb-109">Guidance</span></span>
<span data-ttu-id="b93bb-110">Hello las sugerencias siguientes le ayudará a sacar el máximo de **plantillas** cuando se trabaja con las soluciones:</span><span class="sxs-lookup"><span data-stu-id="b93bb-110">hello following suggestions will help you take full advantage of **Templates** when working with your solutions:</span></span>

* <span data-ttu-id="b93bb-111">Una **plantilla** en un recurso de encapsulamiento que contiene una plantilla de Resource Manager y otros metadatos.</span><span class="sxs-lookup"><span data-stu-id="b93bb-111">A **Template** is an encapsulating resource that contains an Resource Manager template and additional metadata.</span></span> <span data-ttu-id="b93bb-112">Se comporta de forma muy similar tooan elemento Hola Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b93bb-112">It behaves very similarly tooan item in hello Marketplace.</span></span> <span data-ttu-id="b93bb-113">diferencia clave Hello es que es un elemento privado como elementos de Marketplace de toohello lugar públicos.</span><span class="sxs-lookup"><span data-stu-id="b93bb-113">hello key difference is that it is a private item as opposed toohello public Marketplace items.</span></span>
* <span data-ttu-id="b93bb-114">Hola **plantillas** biblioteca funciona bien para los usuarios que necesitan toocustomize sus implementaciones.</span><span class="sxs-lookup"><span data-stu-id="b93bb-114">hello **Templates** library works well for users who need toocustomize their deployments.</span></span>
* <span data-ttu-id="b93bb-115">**plantillas** son apropiadas para los usuarios que necesitan disponer de un repositorio sencillo dentro de Azure.</span><span class="sxs-lookup"><span data-stu-id="b93bb-115">**Templates** work well for users who need a simple repository within Azure.</span></span>
* <span data-ttu-id="b93bb-116">Para empezar, utilice una plantilla de Resource Manager existente.</span><span class="sxs-lookup"><span data-stu-id="b93bb-116">Start with an existing Resource Manager template.</span></span> <span data-ttu-id="b93bb-117">Para buscar plantillas, utilice [github](https://github.com/Azure/azure-quickstart-templates) o [Exportar plantilla](../azure-resource-manager/resource-manager-export-template.md) desde un grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="b93bb-117">Find templates in [github](https://github.com/Azure/azure-quickstart-templates) or [Export template](../azure-resource-manager/resource-manager-export-template.md) from an existing resource group.</span></span>
* <span data-ttu-id="b93bb-118">**Plantillas de** toohello relacionados para usuarios que publica.</span><span class="sxs-lookup"><span data-stu-id="b93bb-118">**Templates** are tied toohello user who publishes them.</span></span> <span data-ttu-id="b93bb-119">nombre del publicador Hello es tooeveryone visible que tiene acceso de lectura tooit.</span><span class="sxs-lookup"><span data-stu-id="b93bb-119">hello publisher name is visible tooeveryone who has read access tooit.</span></span>
* <span data-ttu-id="b93bb-120">**plantillas** son recursos de Resource Manager y, una vez publicadas, su nombre no se puede modificar.</span><span class="sxs-lookup"><span data-stu-id="b93bb-120">**Templates** are Resource Manager resources and cannot be renamed once published.</span></span>

## <a name="add-a-template-resource"></a><span data-ttu-id="b93bb-121">Adición de un recurso de plantilla</span><span class="sxs-lookup"><span data-stu-id="b93bb-121">Add a Template resource</span></span>
<span data-ttu-id="b93bb-122">Hay dos toocreate formas un **plantilla** recursos Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b93bb-122">There are two ways toocreate a **Template** resource in hello Azure portal.</span></span>

### <a name="method-1--create-a-new-template-resource-from-a-running-resource-group"></a><span data-ttu-id="b93bb-123">Método 1: Creación de un nuevo recurso de plantilla a partir de un grupo de recursos en funcionamiento</span><span class="sxs-lookup"><span data-stu-id="b93bb-123">Method 1 : Create a new Template resource from a running resource group</span></span>
1. <span data-ttu-id="b93bb-124">Navegar por grupo de recursos existente tooan en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b93bb-124">Navigate tooan existing resource group on hello Azure Portal.</span></span> <span data-ttu-id="b93bb-125">En **Configuración**, seleccione **Exportar plantilla**.</span><span class="sxs-lookup"><span data-stu-id="b93bb-125">Select **Export template** in **Settings**.</span></span>
2. <span data-ttu-id="b93bb-126">Una vez que se exporta la plantilla de administrador de recursos de hello, usar hello **Guardar plantilla** toosave de botón toohello **plantillas** repositorio.</span><span class="sxs-lookup"><span data-stu-id="b93bb-126">Once hello Resource Manager template is exported, use hello **Save Template** button toosave it toohello **Templates** repository.</span></span> <span data-ttu-id="b93bb-127">Para más detalles sobre la exportación de plantillas, haga clic [aquí](../azure-resource-manager/resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="b93bb-127">Find complete details for Export template [here](../azure-resource-manager/resource-manager-export-template.md).</span></span>
   <br /><br /><span data-ttu-id="b93bb-128">
   ![Exportación de grupo de recursos](media/rg-export-portal1.PNG)</span><span class="sxs-lookup"><span data-stu-id="b93bb-128">
![Resource group export](media/rg-export-portal1.PNG)</span></span>  <br />
3. <span data-ttu-id="b93bb-129">Seleccione hello **guardar tooTemplate** botón de comando.</span><span class="sxs-lookup"><span data-stu-id="b93bb-129">Select hello **Save tooTemplate** command button.</span></span>
   <br /><br />
4. <span data-ttu-id="b93bb-130">Escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="b93bb-130">Enter hello following information:</span></span>
   
   * <span data-ttu-id="b93bb-131">Nombre: nombre del objeto de plantilla de hello (Nota: se trata de un nombre según el Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="b93bb-131">Name – Name of hello template object (NOTE: This is an Azure Resource Manager based name.</span></span> <span data-ttu-id="b93bb-132">por lo que se aplicarán todas las restricciones de nomenclatura, y no se puede cambiar una vez creado).</span><span class="sxs-lookup"><span data-stu-id="b93bb-132">All naming restrictions apply and it cannot be changed once created).</span></span>
   * <span data-ttu-id="b93bb-133">Descripción: resumen rápido acerca de la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="b93bb-133">Description – Quick summary about hello template.</span></span>
     
     ![Guardar plantilla](media/save-template-portal1.PNG)  <br />
5. <span data-ttu-id="b93bb-135">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="b93bb-135">Click **Save**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b93bb-136">Hello hoja de plantilla de exportación muestra notificaciones cuando hello plantilla exportada del Administrador de recursos tiene errores, pero se seguirá toosave capaz de este toohello de plantilla plantillas de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="b93bb-136">hello Export template blade shows notifications when hello exported Resource Manager template has errors, but you will still be able toosave this Resource Manager template toohello Templates.</span></span> <span data-ttu-id="b93bb-137">Asegúrese de comprobar y corregir problemas de las plantillas de cualquier administrador de recursos antes de volver a implementar Hola exporta plantilla del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="b93bb-137">Ensure that you check and fix any Resource Manager template issues before redeploying hello exported Resource Manager template.</span></span>
   > 
   > 

### <a name="method-2--add-a-new-template-resource-from-browse"></a><span data-ttu-id="b93bb-138">Método 2 : Agregar un nuevo recurso de plantilla desde Examinar</span><span class="sxs-lookup"><span data-stu-id="b93bb-138">Method 2 : Add a new Template resource from browse</span></span>
<span data-ttu-id="b93bb-139">También puede agregar un nuevo **plantilla** desde cero mediante Hola + Agregar botón de comando en **examinar > plantillas**.</span><span class="sxs-lookup"><span data-stu-id="b93bb-139">You can also add a new **Template** from scratch using hello +Add command button in **Browse > Templates**.</span></span> <span data-ttu-id="b93bb-140">Deberá tooprovide un nombre, descripción y Hola plantilla JSON del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="b93bb-140">You will need tooprovide a Name, Description and hello Resource Manager template JSON.</span></span>

![Agregar plantilla](media/add-template-portal1.PNG)  <br />

> [!NOTE]
> <span data-ttu-id="b93bb-142">Microsoft.Gallery es un proveedor de recursos de Azure basado en un inquilino.</span><span class="sxs-lookup"><span data-stu-id="b93bb-142">Microsoft.Gallery is a Tenant based Azure resource provider.</span></span> <span data-ttu-id="b93bb-143">Hello recurso de plantilla es usuario toohello relacionados que lo creó.</span><span class="sxs-lookup"><span data-stu-id="b93bb-143">hello Template resource is tied toohello user who created it.</span></span> <span data-ttu-id="b93bb-144">No es tooany relacionados de suscripción específica.</span><span class="sxs-lookup"><span data-stu-id="b93bb-144">It is not tied tooany specific subscription.</span></span> <span data-ttu-id="b93bb-145">Una suscripción debe toobe elegido solo cuando se implementa una plantilla.</span><span class="sxs-lookup"><span data-stu-id="b93bb-145">A subscription needs toobe chosen only when deploying a Template.</span></span>
> 
> 

## <a name="view-template-resources"></a><span data-ttu-id="b93bb-146">Consulta de los recursos de plantilla</span><span class="sxs-lookup"><span data-stu-id="b93bb-146">View Template resources</span></span>
<span data-ttu-id="b93bb-147">Todos los **plantillas** tooyou disponible puede verse en **examinar > plantillas**.</span><span class="sxs-lookup"><span data-stu-id="b93bb-147">All **Templates** available tooyou can be seen at **Browse > Templates**.</span></span> <span data-ttu-id="b93bb-148">Aquí encontrará las **plantillas** que ha creado, así como las plantillas que han compartido con usted y que tienen distintos niveles de permisos.</span><span class="sxs-lookup"><span data-stu-id="b93bb-148">This includes **Templates** you have created as well as ones that have been shared with you with varying levels of permissions.</span></span> <span data-ttu-id="b93bb-149">Para obtener más detalles en hello [el control de acceso](#access-control-for-a-tenant-resource-provider) sección más adelante.</span><span class="sxs-lookup"><span data-stu-id="b93bb-149">More details in hello [access control](#access-control-for-a-tenant-resource-provider) section below.</span></span>

![Ver plantilla](media/view-template-portal1.PNG)  <br />

<span data-ttu-id="b93bb-151">Puede ver detalles de Hola de un **plantilla** haciendo clic en un elemento de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="b93bb-151">You can view hello details of a **Template** by clicking into an item in hello list.</span></span>

![Ver plantilla](media/view-template-portal2c.png)  <br />

## <a name="edit-a-template-resource"></a><span data-ttu-id="b93bb-153">Edición de un recurso de plantilla</span><span class="sxs-lookup"><span data-stu-id="b93bb-153">Edit a Template resource</span></span>
<span data-ttu-id="b93bb-154">Puede iniciar flujo de edición de Hola para un **plantilla** haga clic en el elemento de hello en la lista de examinación de Hola o eligiendo el botón de comando de edición de Hola.</span><span class="sxs-lookup"><span data-stu-id="b93bb-154">You can initiate hello edit flow for a **Template** by right clicking hello item on hello Browse list or by choosing hello Edit command button.</span></span>

![Editar plantilla](media/edit-template-portal1a.PNG)  <br />

<span data-ttu-id="b93bb-156">Puede editar la descripción de Hola o texto de la plantilla de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="b93bb-156">You can edit hello description or Resource Manager template text.</span></span> <span data-ttu-id="b93bb-157">No se puede editar el nombre de hello ya que es un nombre de recursos del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="b93bb-157">You cannot edit hello name since it is an Resource Manager resource name.</span></span> <span data-ttu-id="b93bb-158">Al editar plantilla de administrador de recursos de hello JSON se validará tooensure que es un valor JSON válido.</span><span class="sxs-lookup"><span data-stu-id="b93bb-158">When you edit hello Resource Manager template JSON we will validate tooensure that it is valid JSON.</span></span> <span data-ttu-id="b93bb-159">Elija **Aceptar** y, a continuación, **guardar** toosave la plantilla actualizada.</span><span class="sxs-lookup"><span data-stu-id="b93bb-159">Choose **OK** and then **Save** toosave your updated template.</span></span>

![Editar plantilla](media/edit-template-portal2a.PNG)  <br />

<span data-ttu-id="b93bb-161">Una vez Hola **plantilla** se guarda, verá una notificación de confirmación.</span><span class="sxs-lookup"><span data-stu-id="b93bb-161">Once hello **Template** is saved you will see a confirmation notification.</span></span>

![Editar plantilla](media/edit-template-portal3b.png)  <br />

## <a name="deploy-a-template-resource"></a><span data-ttu-id="b93bb-163">Implementación de un recurso de plantilla</span><span class="sxs-lookup"><span data-stu-id="b93bb-163">Deploy a Template resource</span></span>
<span data-ttu-id="b93bb-164">Puede implementar cualquier **plantilla** en la que tenga permisos de **lectura**.</span><span class="sxs-lookup"><span data-stu-id="b93bb-164">You can deploy any **Template** that you have **Read** permissions on.</span></span> <span data-ttu-id="b93bb-165">flujo de implementación de Hello inicia la hoja de implementación de plantilla de Azure estándar Hola.</span><span class="sxs-lookup"><span data-stu-id="b93bb-165">hello deployment flow launches hello standard Azure Template deployment blade.</span></span> <span data-ttu-id="b93bb-166">Rellene los valores de hello para tooproceed de parámetros de plantilla de hello Administrador de recursos con la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="b93bb-166">Fill out hello values for hello Resource Manager template parameters tooproceed with hello deployment.</span></span>

![Implementar plantilla](media/deploy-template-portal1b.png)  <br />

## <a name="share-a-template-resource"></a><span data-ttu-id="b93bb-168">Uso compartido de un recurso de plantilla</span><span class="sxs-lookup"><span data-stu-id="b93bb-168">Share a Template resource</span></span>
<span data-ttu-id="b93bb-169">Puede compartir con sus compañeros los recursos de **plantilla** .</span><span class="sxs-lookup"><span data-stu-id="b93bb-169">A **Template** resource can be shared with your peers.</span></span> <span data-ttu-id="b93bb-170">Uso compartido se comporta del mismo modo demasiado[asignación de roles para cualquier recurso de Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b93bb-170">Sharing behaves similarly too[role assignment for any resource on Azure](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="b93bb-171">Hola **plantilla** propietario proporciona permisos a los usuarios de tooother que pueden interactuar con un recurso de plantilla.</span><span class="sxs-lookup"><span data-stu-id="b93bb-171">hello **Template** owner provides permissions tooother users who can interact with a Template resource.</span></span> <span data-ttu-id="b93bb-172">Hola persona o grupo de personas compartir hello **plantilla** con será plantilla de administrador de recursos de toosee capaz de Hola y sus propiedades de la galería.</span><span class="sxs-lookup"><span data-stu-id="b93bb-172">hello person or group of people you share hello **Template** with will be able toosee hello Resource Manager template and its gallery properties.</span></span>

### <a name="access-control-for-hello-microsoftgallery-resources"></a><span data-ttu-id="b93bb-173">Control de acceso para los recursos de hello Microsoft.Gallery</span><span class="sxs-lookup"><span data-stu-id="b93bb-173">Access control for hello Microsoft.Gallery resources</span></span>
| <span data-ttu-id="b93bb-174">Rol</span><span class="sxs-lookup"><span data-stu-id="b93bb-174">Role</span></span> | <span data-ttu-id="b93bb-175">Permisos</span><span class="sxs-lookup"><span data-stu-id="b93bb-175">Permissions</span></span> |
| --- | --- |
| <span data-ttu-id="b93bb-176">Propietario</span><span class="sxs-lookup"><span data-stu-id="b93bb-176">Owner</span></span> |<span data-ttu-id="b93bb-177">Permite el control total en el recurso de plantilla de hello incluidos los recursos compartidos</span><span class="sxs-lookup"><span data-stu-id="b93bb-177">Allows full control on hello Template resource including Share</span></span> |
| <span data-ttu-id="b93bb-178">Lector</span><span class="sxs-lookup"><span data-stu-id="b93bb-178">Reader</span></span> |<span data-ttu-id="b93bb-179">Permite leer y Execute(Deploy) en hello recurso de plantilla</span><span class="sxs-lookup"><span data-stu-id="b93bb-179">Allows Read and Execute(Deploy) on hello Template resource</span></span> |
| <span data-ttu-id="b93bb-180">Colaborador</span><span class="sxs-lookup"><span data-stu-id="b93bb-180">Contributor</span></span> |<span data-ttu-id="b93bb-181">Permite editar y eliminar permiso en hello recurso de plantilla.</span><span class="sxs-lookup"><span data-stu-id="b93bb-181">Allows Edit and Delete permission on hello Template resource.</span></span> <span data-ttu-id="b93bb-182">Usuario no puede compartir Hola plantilla con otros usuarios</span><span class="sxs-lookup"><span data-stu-id="b93bb-182">User cannot Share hello Template with others</span></span> |

<span data-ttu-id="b93bb-183">Seleccione **recurso compartido** en elemento de exploración de hello haciendo clic o en la hoja de la vista de Hola de un elemento específico.</span><span class="sxs-lookup"><span data-stu-id="b93bb-183">Select **Share** on hello browse item by right clicking or on hello view blade of a specific item.</span></span> <span data-ttu-id="b93bb-184">De este modo, se iniciará un proceso que le permitirá compartir el recurso de plantilla.</span><span class="sxs-lookup"><span data-stu-id="b93bb-184">This launches a Share experience.</span></span>

![Compartir plantilla](media/share-template-portal1a.png)  <br />

 <span data-ttu-id="b93bb-186">Ahora puede elegir un rol y un tooa de acceso de tooprovide usuario o grupo determinado **plantilla**.</span><span class="sxs-lookup"><span data-stu-id="b93bb-186">You can now choose a role and a user or group tooprovide access tooa particular **Template**.</span></span> <span data-ttu-id="b93bb-187">roles disponibles Hola son lector, Colaborador y propietario.</span><span class="sxs-lookup"><span data-stu-id="b93bb-187">hello available roles are Owner, Reader and Contributor.</span></span> <span data-ttu-id="b93bb-188">Para obtener más detalles en hello [el control de acceso](#access-control-for-a-tenant-resource-provider) sección anterior.</span><span class="sxs-lookup"><span data-stu-id="b93bb-188">More details in hello [access control](#access-control-for-a-tenant-resource-provider) section above.</span></span>

![Compartir plantilla](media/share-template-portal2b.png)  <br />

![Compartir plantilla](media/share-template-portal3b.png)  <br />

<span data-ttu-id="b93bb-191">Haga clic en **Seleccionar** y en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b93bb-191">Click **Select** and **Ok**.</span></span> <span data-ttu-id="b93bb-192">Ahora puede ver Hola usuarios o grupos que agregó toohello recursos.</span><span class="sxs-lookup"><span data-stu-id="b93bb-192">You can now see hello users or groups you added toohello resource.</span></span>

![Compartir plantilla](media/share-template-portal4b.png)  <br />

> [!NOTE]
> <span data-ttu-id="b93bb-194">Una plantilla solo puede compartirse con usuarios y grupos en hello mismo inquilino de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b93bb-194">A Template can only be shared with users and groups in hello same Azure Active Directory tenant.</span></span> <span data-ttu-id="b93bb-195">Si comparte una plantilla con una dirección de correo electrónico que no está en su inquilino, se enviará una invitación pidiendo a inquilino de Hola Hola usuario toojoin como invitado.</span><span class="sxs-lookup"><span data-stu-id="b93bb-195">If you share a Template with an email address that is not in your tenant, an invitation will be sent asking hello user toojoin hello tenant as a guest.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b93bb-196">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b93bb-196">Next steps</span></span>
* <span data-ttu-id="b93bb-197">toolearn acerca de cómo crear plantillas de administrador de recursos, consulte [creación de plantillas](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="b93bb-197">toolearn about creating Resource Manager templates, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="b93bb-198">funciones de hello toounderstand se pueden usar en una plantilla de administrador de recursos, consulte [funciones de plantilla](../azure-resource-manager/resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="b93bb-198">toounderstand hello functions you can use in an Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md)</span></span>
* <span data-ttu-id="b93bb-199">Para obtener instrucciones sobre cómo diseñar las plantillas, consulte [Prácticas recomendadas para diseñar plantillas del Administrador de recursos de Azure](../azure-resource-manager/best-practices-resource-manager-design-templates.md)</span><span class="sxs-lookup"><span data-stu-id="b93bb-199">For guidance on designing your templates, see [Best practices for designing Azure Resource Manager templates](../azure-resource-manager/best-practices-resource-manager-design-templates.md)</span></span>

