---
title: Control de acceso basado en aaaRole con REST - Azure AD | Documentos de Microsoft
description: "Administración del control de acceso basado en roles con hello API de REST"
services: active-directory
documentationcenter: na
author: andredm7
manager: femila
editor: 
ms.assetid: 1f90228a-7aac-4ea7-ad82-b57d222ab128
ms.service: active-directory
ms.workload: multiple
ms.tgt_pltfrm: rest-api
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: andredm
ms.openlocfilehash: ccd402fd4fe4583288076cac23753dd067694681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-hello-rest-api"></a><span data-ttu-id="12f31-103">Administrar el Control de acceso basado en roles con hello API de REST</span><span class="sxs-lookup"><span data-stu-id="12f31-103">Manage Role-Based Access Control with hello REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="12f31-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="12f31-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="12f31-105">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="12f31-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="12f31-106">API DE REST</span><span class="sxs-lookup"><span data-stu-id="12f31-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="12f31-107">Control de acceso basado en roles (RBAC) en hello portal de Azure y API de Azure Resource Manager le ayuda a administrar la suscripción de tooyour de acceso y recursos en un nivel específico.</span><span class="sxs-lookup"><span data-stu-id="12f31-107">Role-Based Access Control (RBAC) in hello Azure portal and Azure Resource Manager API helps you manage access tooyour subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="12f31-108">Con esta característica, puede conceder acceso a los usuarios, grupos o entidades de servicio de Active Directory mediante la asignación de algunos toothem de roles en un ámbito determinado.</span><span class="sxs-lookup"><span data-stu-id="12f31-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles toothem at a particular scope.</span></span>

## <a name="list-all-role-assignments"></a><span data-ttu-id="12f31-109">Lista de todas las asignaciones de roles</span><span class="sxs-lookup"><span data-stu-id="12f31-109">List all role assignments</span></span>
<span data-ttu-id="12f31-110">Muestra todas las asignaciones de roles de hello en hello especificado ámbito y subscopes.</span><span class="sxs-lookup"><span data-stu-id="12f31-110">Lists all hello role assignments at hello specified scope and subscopes.</span></span>

<span data-ttu-id="12f31-111">las asignaciones de roles de toolist, debe tener acceso demasiado`Microsoft.Authorization/roleAssignments/read` operación en el ámbito de Hola.</span><span class="sxs-lookup"><span data-stu-id="12f31-111">toolist role assignments, you must have access too`Microsoft.Authorization/roleAssignments/read` operation at hello scope.</span></span> <span data-ttu-id="12f31-112">Todas las funciones integradas de Hola se conceden acceso toothis operación.</span><span class="sxs-lookup"><span data-stu-id="12f31-112">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="12f31-113">Para obtener más información sobre las asignaciones de roles y la administración del acceso a los recursos de Azure, consulte [Control de acceso basado en roles de Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="12f31-113">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="12f31-114">Solicitud</span><span class="sxs-lookup"><span data-stu-id="12f31-114">Request</span></span>
<span data-ttu-id="12f31-115">Hola de uso **obtener** método con hello siguiente URI:</span><span class="sxs-lookup"><span data-stu-id="12f31-115">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments?api-version={api-version}&$filter={filter}

<span data-ttu-id="12f31-116">Dentro de hello URI, realice Hola siguiendo las sustituciones toocustomize la solicitud:</span><span class="sxs-lookup"><span data-stu-id="12f31-116">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="12f31-117">Reemplace *{scope}* con ámbito de hello para el que desea toolist las asignaciones de roles de Hola.</span><span class="sxs-lookup"><span data-stu-id="12f31-117">Replace *{scope}* with hello scope for which you wish toolist hello role assignments.</span></span> <span data-ttu-id="12f31-118">Hello en los ejemplos siguientes muestra cómo toospecify Hola ámbito para los diferentes niveles:</span><span class="sxs-lookup"><span data-stu-id="12f31-118">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="12f31-119">Suscripción: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="12f31-119">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="12f31-120">Grupo de recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="12f31-120">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="12f31-121">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="12f31-121">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="12f31-122">Reemplace *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="12f31-122">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="12f31-123">Reemplace *{filter}* con la condición de Hola que desea que la lista de asignaciones de rol de tooapply toofilter Hola:</span><span class="sxs-lookup"><span data-stu-id="12f31-123">Replace *{filter}* with hello condition that you wish tooapply toofilter hello role assignment list:</span></span>

   * <span data-ttu-id="12f31-124">Lista de las asignaciones de roles para solo hello especifican ámbito, sin incluir las asignaciones de roles de hello en subscopes:`atScope()`</span><span class="sxs-lookup"><span data-stu-id="12f31-124">List role assignments for only hello specified scope, not including hello role assignments at subscopes: `atScope()`</span></span>    
   * <span data-ttu-id="12f31-125">Lista de las asignaciones de roles para solo un usuario, un grupo o una aplicación determinados: `principalId%20eq%20'{objectId of user, group, or service principal}'`</span><span class="sxs-lookup"><span data-stu-id="12f31-125">List role assignments for a specific user, group, or application: `principalId%20eq%20'{objectId of user, group, or service principal}'`</span></span>  
   * <span data-ttu-id="12f31-126">Lista de asignaciones de roles para un usuario específico, incluidas las heredadas de grupos | `assignedTo('{objectId of user}')`</span><span class="sxs-lookup"><span data-stu-id="12f31-126">List role assignments for a specific user, including ones inherited from groups | `assignedTo('{objectId of user}')`</span></span>

### <a name="response"></a><span data-ttu-id="12f31-127">Respuesta</span><span class="sxs-lookup"><span data-stu-id="12f31-127">Response</span></span>
<span data-ttu-id="12f31-128">Código de estado: 200</span><span class="sxs-lookup"><span data-stu-id="12f31-128">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7",
        "principalId": "2f9d4375-cbf1-48e8-83c9-2a0be4cb33fb",
        "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
        "createdOn": "2015-10-08T07:28:24.3905077Z",
        "updatedOn": "2015-10-08T07:28:24.3905077Z",
        "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
        "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleAssignments/baa6e199-ad19-4667-b768-623fde31aedd",
      "type": "Microsoft.Authorization/roleAssignments",
      "name": "baa6e199-ad19-4667-b768-623fde31aedd"
    }
  ],
  "nextLink": null
}

```

## <a name="get-information-about-a-role-assignment"></a><span data-ttu-id="12f31-129">Obtención de información sobre una asignación de roles</span><span class="sxs-lookup"><span data-stu-id="12f31-129">Get information about a role assignment</span></span>
<span data-ttu-id="12f31-130">Obtiene información sobre una asignación de roles única especificada por el identificador de asignación de rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="12f31-130">Gets information about a single role assignment specified by hello role assignment identifier.</span></span>

<span data-ttu-id="12f31-131">tooget obtener información acerca de una asignación de roles, debe tener acceso demasiado`Microsoft.Authorization/roleAssignments/read` operación.</span><span class="sxs-lookup"><span data-stu-id="12f31-131">tooget information about a role assignment, you must have access too`Microsoft.Authorization/roleAssignments/read` operation.</span></span> <span data-ttu-id="12f31-132">Todas las funciones integradas de Hola se conceden acceso toothis operación.</span><span class="sxs-lookup"><span data-stu-id="12f31-132">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="12f31-133">Para obtener más información sobre las asignaciones de roles y la administración del acceso a los recursos de Azure, consulte [Control de acceso basado en roles de Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="12f31-133">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="12f31-134">Solicitud</span><span class="sxs-lookup"><span data-stu-id="12f31-134">Request</span></span>
<span data-ttu-id="12f31-135">Hola de uso **obtener** método con hello siguiente URI:</span><span class="sxs-lookup"><span data-stu-id="12f31-135">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="12f31-136">Dentro de hello URI, realice Hola siguiendo las sustituciones toocustomize la solicitud:</span><span class="sxs-lookup"><span data-stu-id="12f31-136">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="12f31-137">Reemplace *{scope}* con ámbito de hello para el que desea toolist las asignaciones de roles de Hola.</span><span class="sxs-lookup"><span data-stu-id="12f31-137">Replace *{scope}* with hello scope for which you wish toolist hello role assignments.</span></span> <span data-ttu-id="12f31-138">Hello en los ejemplos siguientes muestra cómo toospecify Hola ámbito para los diferentes niveles:</span><span class="sxs-lookup"><span data-stu-id="12f31-138">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="12f31-139">Suscripción: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="12f31-139">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="12f31-140">Grupo de recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="12f31-140">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="12f31-141">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="12f31-141">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="12f31-142">Reemplace *{role-assignment-id}* con identificador GUID de Hola Hola de asignación de roles.</span><span class="sxs-lookup"><span data-stu-id="12f31-142">Replace *{role-assignment-id}* with hello GUID identifier of hello role assignment.</span></span>
3. <span data-ttu-id="12f31-143">Reemplace *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="12f31-143">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="12f31-144">Respuesta</span><span class="sxs-lookup"><span data-stu-id="12f31-144">Response</span></span>
<span data-ttu-id="12f31-145">Código de estado: 200</span><span class="sxs-lookup"><span data-stu-id="12f31-145">Status code: 200</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/b24988ac-6180-42a0-ab88-20f7382dd24c",
    "principalId": "672f1afa-526a-4ef6-819c-975c7cd79022",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "createdOn": "2015-10-05T08:36:26.4014813Z",
    "updatedOn": "2015-10-05T08:36:26.4014813Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleAssignments/196965ae-6088-4121-a92a-f1e33fdcc73e",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "196965ae-6088-4121-a92a-f1e33fdcc73e"
}

```

## <a name="create-a-role-assignment"></a><span data-ttu-id="12f31-146">Creación de una asignación de roles</span><span class="sxs-lookup"><span data-stu-id="12f31-146">Create a Role Assignment</span></span>
<span data-ttu-id="12f31-147">Crear una función de asignación en hello especificado ámbito para hello especifica la concesión Hola especificado rol principal.</span><span class="sxs-lookup"><span data-stu-id="12f31-147">Create a role assignment at hello specified scope for hello specified principal granting hello specified role.</span></span>

<span data-ttu-id="12f31-148">toocreate una asignación de roles, debe tener acceso demasiado`Microsoft.Authorization/roleAssignments/write` operación.</span><span class="sxs-lookup"><span data-stu-id="12f31-148">toocreate a role assignment, you must have access too`Microsoft.Authorization/roleAssignments/write` operation.</span></span> <span data-ttu-id="12f31-149">De hello funciones integradas solo *propietario* y *Administrador de acceso de usuario* se conceden acceso toothis operación.</span><span class="sxs-lookup"><span data-stu-id="12f31-149">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="12f31-150">Para obtener más información sobre las asignaciones de roles y la administración del acceso a los recursos de Azure, consulte [Control de acceso basado en roles de Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="12f31-150">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="12f31-151">Solicitud</span><span class="sxs-lookup"><span data-stu-id="12f31-151">Request</span></span>
<span data-ttu-id="12f31-152">Hola de uso **colocar** método con hello siguiente URI:</span><span class="sxs-lookup"><span data-stu-id="12f31-152">Use hello **PUT** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="12f31-153">Dentro de hello URI, realice Hola siguiendo las sustituciones toocustomize la solicitud:</span><span class="sxs-lookup"><span data-stu-id="12f31-153">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="12f31-154">Reemplace *{scope}* con ámbito de hello en el que desea toocreate las asignaciones de roles de Hola.</span><span class="sxs-lookup"><span data-stu-id="12f31-154">Replace *{scope}* with hello scope at which you wish toocreate hello role assignments.</span></span> <span data-ttu-id="12f31-155">Cuando se crea una asignación de roles en un ámbito primario, todos los ámbitos secundarios heredan Hola misma asignación de roles.</span><span class="sxs-lookup"><span data-stu-id="12f31-155">When you create a role assignment at a parent scope, all child scopes inherit hello same role assignment.</span></span> <span data-ttu-id="12f31-156">Hello en los ejemplos siguientes muestra cómo toospecify Hola ámbito para los diferentes niveles:</span><span class="sxs-lookup"><span data-stu-id="12f31-156">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="12f31-157">Suscripción: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="12f31-157">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="12f31-158">Grupo de recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="12f31-158">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>   
   * <span data-ttu-id="12f31-159">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="12f31-159">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="12f31-160">Reemplace *{role-assignment-id}* con un nuevo GUID, que se convierte en identificador GUID de Hola Hola nuevas de asignación de roles.</span><span class="sxs-lookup"><span data-stu-id="12f31-160">Replace *{role-assignment-id}* with a new GUID, which becomes hello GUID identifier of hello new role assignment.</span></span>
3. <span data-ttu-id="12f31-161">Reemplace *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="12f31-161">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="12f31-162">En el cuerpo de solicitud de hello, proporcionar valores de hello en hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="12f31-162">For hello request body, provide hello values in hello following format:</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b"
  }
}

```

| <span data-ttu-id="12f31-163">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="12f31-163">Element Name</span></span> | <span data-ttu-id="12f31-164">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="12f31-164">Required</span></span> | <span data-ttu-id="12f31-165">Tipo</span><span class="sxs-lookup"><span data-stu-id="12f31-165">Type</span></span> | <span data-ttu-id="12f31-166">Description</span><span class="sxs-lookup"><span data-stu-id="12f31-166">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="12f31-167">roleDefinitionId</span><span class="sxs-lookup"><span data-stu-id="12f31-167">roleDefinitionId</span></span> |<span data-ttu-id="12f31-168">Sí</span><span class="sxs-lookup"><span data-stu-id="12f31-168">Yes</span></span> |<span data-ttu-id="12f31-169">String</span><span class="sxs-lookup"><span data-stu-id="12f31-169">String</span></span> |<span data-ttu-id="12f31-170">identificador de Hello del rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="12f31-170">hello identifier of hello role.</span></span> <span data-ttu-id="12f31-171">formato de Hola de identificador hello es:`{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span><span class="sxs-lookup"><span data-stu-id="12f31-171">hello format of hello identifier is: `{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span></span> |
| <span data-ttu-id="12f31-172">principalId</span><span class="sxs-lookup"><span data-stu-id="12f31-172">principalId</span></span> |<span data-ttu-id="12f31-173">Sí</span><span class="sxs-lookup"><span data-stu-id="12f31-173">Yes</span></span> |<span data-ttu-id="12f31-174">String</span><span class="sxs-lookup"><span data-stu-id="12f31-174">String</span></span> |<span data-ttu-id="12f31-175">Id. de objeto de entidad de seguridad de hello Azure AD (usuario, grupo o entidad de servicio) se asigna el rol de hello toowhich.</span><span class="sxs-lookup"><span data-stu-id="12f31-175">objectId of hello Azure AD principal (user, group, or service principal) toowhich hello role is assigned.</span></span> |

### <a name="response"></a><span data-ttu-id="12f31-176">Response</span><span class="sxs-lookup"><span data-stu-id="12f31-176">Response</span></span>
<span data-ttu-id="12f31-177">Código de estado: 201</span><span class="sxs-lookup"><span data-stu-id="12f31-177">Status code: 201</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND",
    "createdOn": "2015-12-16T00:27:19.6447515Z",
    "updatedOn": "2015-12-16T00:27:19.6447515Z",
    "createdBy": null,
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleAssignments/2e9e86c8-0e91-4958-b21f-20f51f27bab2",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "2e9e86c8-0e91-4958-b21f-20f51f27bab2"
}

```

## <a name="delete-a-role-assignment"></a><span data-ttu-id="12f31-178">Eliminación de una asignación de roles</span><span class="sxs-lookup"><span data-stu-id="12f31-178">Delete a Role Assignment</span></span>
<span data-ttu-id="12f31-179">Eliminar una asignación de roles en hello especifica ámbito.</span><span class="sxs-lookup"><span data-stu-id="12f31-179">Delete a role assignment at hello specified scope.</span></span>

<span data-ttu-id="12f31-180">toodelete una asignación de roles, debe tener acceso toohello `Microsoft.Authorization/roleAssignments/delete` operación.</span><span class="sxs-lookup"><span data-stu-id="12f31-180">toodelete a role assignment, you must have access toohello `Microsoft.Authorization/roleAssignments/delete` operation.</span></span> <span data-ttu-id="12f31-181">De hello funciones integradas solo *propietario* y *Administrador de acceso de usuario* se conceden acceso toothis operación.</span><span class="sxs-lookup"><span data-stu-id="12f31-181">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="12f31-182">Para obtener más información sobre las asignaciones de roles y la administración del acceso a los recursos de Azure, consulte [Control de acceso basado en roles de Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="12f31-182">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="12f31-183">Solicitud</span><span class="sxs-lookup"><span data-stu-id="12f31-183">Request</span></span>
<span data-ttu-id="12f31-184">Hola de uso **eliminar** método con hello siguiente URI:</span><span class="sxs-lookup"><span data-stu-id="12f31-184">Use hello **DELETE** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="12f31-185">Dentro de hello URI, realice Hola siguiendo las sustituciones toocustomize la solicitud:</span><span class="sxs-lookup"><span data-stu-id="12f31-185">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="12f31-186">Reemplace *{scope}* con ámbito de hello en el que desea toocreate las asignaciones de roles de Hola.</span><span class="sxs-lookup"><span data-stu-id="12f31-186">Replace *{scope}* with hello scope at which you wish toocreate hello role assignments.</span></span> <span data-ttu-id="12f31-187">Hello en los ejemplos siguientes muestra cómo toospecify Hola ámbito para los diferentes niveles:</span><span class="sxs-lookup"><span data-stu-id="12f31-187">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="12f31-188">Suscripción: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="12f31-188">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="12f31-189">Grupo de recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="12f31-189">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="12f31-190">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="12f31-190">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="12f31-191">Reemplace *{role-assignment-id}* con el Id. de asignación de rol de hello GUID.</span><span class="sxs-lookup"><span data-stu-id="12f31-191">Replace *{role-assignment-id}* with hello role assignment id GUID.</span></span>
3. <span data-ttu-id="12f31-192">Reemplace *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="12f31-192">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="12f31-193">Respuesta</span><span class="sxs-lookup"><span data-stu-id="12f31-193">Response</span></span>
<span data-ttu-id="12f31-194">Código de estado: 200</span><span class="sxs-lookup"><span data-stu-id="12f31-194">Status code: 200</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND",
    "createdOn": "2015-12-17T23:21:40.8921564Z",
    "updatedOn": "2015-12-17T23:21:40.8921564Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleAssignments/5eec22ee-ea5c-431e-8f41-82c560706fd2",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "5eec22ee-ea5c-431e-8f41-82c560706fd2"
}

```

## <a name="list-all-roles"></a><span data-ttu-id="12f31-195">Lista de todos los roles</span><span class="sxs-lookup"><span data-stu-id="12f31-195">List all Roles</span></span>
<span data-ttu-id="12f31-196">Enumera todos los roles de Hola que están disponibles para la asignación en hello especificada ámbito.</span><span class="sxs-lookup"><span data-stu-id="12f31-196">Lists all hello roles that are available for assignment at hello specified scope.</span></span>

<span data-ttu-id="12f31-197">roles de toolist, debe tener acceso demasiado`Microsoft.Authorization/roleDefinitions/read` operación en el ámbito de Hola.</span><span class="sxs-lookup"><span data-stu-id="12f31-197">toolist roles, you must have access too`Microsoft.Authorization/roleDefinitions/read` operation at hello scope.</span></span> <span data-ttu-id="12f31-198">Todas las funciones integradas de Hola se conceden acceso toothis operación.</span><span class="sxs-lookup"><span data-stu-id="12f31-198">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="12f31-199">Para obtener más información sobre las asignaciones de roles y la administración del acceso a los recursos de Azure, consulte [Control de acceso basado en roles de Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="12f31-199">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="12f31-200">Solicitud</span><span class="sxs-lookup"><span data-stu-id="12f31-200">Request</span></span>
<span data-ttu-id="12f31-201">Hola de uso **obtener** método con hello siguiente URI:</span><span class="sxs-lookup"><span data-stu-id="12f31-201">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions?api-version={api-version}&$filter={filter}

<span data-ttu-id="12f31-202">Dentro de hello URI, realice Hola siguiendo las sustituciones toocustomize la solicitud:</span><span class="sxs-lookup"><span data-stu-id="12f31-202">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="12f31-203">Reemplace *{scope}* con ámbito de hello para el que desea toolist roles Hola.</span><span class="sxs-lookup"><span data-stu-id="12f31-203">Replace *{scope}* with hello scope for which you wish toolist hello roles.</span></span> <span data-ttu-id="12f31-204">Hello en los ejemplos siguientes muestra cómo toospecify Hola ámbito para los diferentes niveles:</span><span class="sxs-lookup"><span data-stu-id="12f31-204">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="12f31-205">Suscripción: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="12f31-205">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="12f31-206">Grupo de recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="12f31-206">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="12f31-207">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="12f31-207">Resource /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="12f31-208">Reemplace *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="12f31-208">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="12f31-209">Reemplace *{filter}* con condición de Hola que tooapply toofilter Hola mi lista de deseos de roles:</span><span class="sxs-lookup"><span data-stu-id="12f31-209">Replace *{filter}* with hello condition that you wish tooapply toofilter hello list of roles:</span></span>

   * <span data-ttu-id="12f31-210">Lista de roles disponibles para la asignación en hello especifica ámbito y cualquiera de sus ámbitos secundarios:`atScopeAndBelow()`</span><span class="sxs-lookup"><span data-stu-id="12f31-210">List roles available for assignment at hello specified scope and any of its child scopes: `atScopeAndBelow()`</span></span>
   * <span data-ttu-id="12f31-211">Buscar un rol con un nombre para mostrar exacto: `roleName%20eq%20'{role-display-name}'`.</span><span class="sxs-lookup"><span data-stu-id="12f31-211">Search for a role using exact display name: `roleName%20eq%20'{role-display-name}'`.</span></span> <span data-ttu-id="12f31-212">Usar la forma de codificación de dirección URL de Hola de hello exacta DisplayName del rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="12f31-212">Use hello URL encoded form of hello exact display name of hello role.</span></span> <span data-ttu-id="12f31-213">Por ejemplo, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span><span class="sxs-lookup"><span data-stu-id="12f31-213">For instance, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span></span>

### <a name="response"></a><span data-ttu-id="12f31-214">Respuesta</span><span class="sxs-lookup"><span data-stu-id="12f31-214">Response</span></span>
<span data-ttu-id="12f31-215">Código de estado: 200</span><span class="sxs-lookup"><span data-stu-id="12f31-215">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access toothem, and not hello virtual network or storage account they\u2019re connected to.",
        "assignableScopes": [
          "/"
        ],
        "permissions": [
          {
            "actions": [
              "Microsoft.Authorization/*/read",
              "Microsoft.Compute/availabilitySets/*",
              "Microsoft.Compute/locations/*",
              "Microsoft.Compute/virtualMachines/*",
              "Microsoft.Compute/virtualMachineScaleSets/*",
              "Microsoft.Insights/alertRules/*",
              "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatRules/join/action",
              "Microsoft.Network/loadBalancers/read",
              "Microsoft.Network/locations/*",
              "Microsoft.Network/networkInterfaces/*",
              "Microsoft.Network/networkSecurityGroups/join/action",
              "Microsoft.Network/networkSecurityGroups/read",
              "Microsoft.Network/publicIPAddresses/join/action",
              "Microsoft.Network/publicIPAddresses/read",
              "Microsoft.Network/virtualNetworks/read",
              "Microsoft.Network/virtualNetworks/subnets/join/action",
              "Microsoft.Resources/deployments/*",
              "Microsoft.Resources/subscriptions/resourceGroups/read",
              "Microsoft.Storage/storageAccounts/listKeys/action",
              "Microsoft.Storage/storageAccounts/read",
              "Microsoft.Support/*"
            ],
            "notActions": []
          }
        ],
        "createdOn": "2015-06-02T00:18:27.3542698Z",
        "updatedOn": "2015-12-08T03:16:55.6170255Z",
        "createdBy": null,
        "updatedBy": null
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
      "type": "Microsoft.Authorization/roleDefinitions",
      "name": "9980e02c-c2be-4d73-94e8-173b1dc7cf3c"
    }
  ],
  "nextLink": null
}

```

## <a name="get-information-about-a-role"></a><span data-ttu-id="12f31-216">Obtención de información sobre un rol</span><span class="sxs-lookup"><span data-stu-id="12f31-216">Get information about a Role</span></span>
<span data-ttu-id="12f31-217">Obtiene información sobre un solo rol especificado por el identificador de definición de rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="12f31-217">Gets information about a single role specified by hello role definition identifier.</span></span> <span data-ttu-id="12f31-218">tooget información acerca de una única función utilizando su nombre para mostrar, consulte [enumera todos los roles](role-based-access-control-manage-access-rest.md#list-all-roles).</span><span class="sxs-lookup"><span data-stu-id="12f31-218">tooget information about a single role using its display name, see [List all roles](role-based-access-control-manage-access-rest.md#list-all-roles).</span></span>

<span data-ttu-id="12f31-219">tooget obtener información acerca de una función, debe tener acceso demasiado`Microsoft.Authorization/roleDefinitions/read` operación.</span><span class="sxs-lookup"><span data-stu-id="12f31-219">tooget information about a role, you must have access too`Microsoft.Authorization/roleDefinitions/read` operation.</span></span> <span data-ttu-id="12f31-220">Todas las funciones integradas de Hola se conceden acceso toothis operación.</span><span class="sxs-lookup"><span data-stu-id="12f31-220">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="12f31-221">Para obtener más información sobre las asignaciones de roles y la administración del acceso a los recursos de Azure, consulte [Control de acceso basado en roles de Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="12f31-221">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="12f31-222">Solicitud</span><span class="sxs-lookup"><span data-stu-id="12f31-222">Request</span></span>
<span data-ttu-id="12f31-223">Hola de uso **obtener** método con hello siguiente URI:</span><span class="sxs-lookup"><span data-stu-id="12f31-223">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="12f31-224">Dentro de hello URI, realice Hola siguiendo las sustituciones toocustomize la solicitud:</span><span class="sxs-lookup"><span data-stu-id="12f31-224">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="12f31-225">Reemplace *{scope}* con ámbito de hello para el que desea toolist las asignaciones de roles de Hola.</span><span class="sxs-lookup"><span data-stu-id="12f31-225">Replace *{scope}* with hello scope for which you wish toolist hello role assignments.</span></span> <span data-ttu-id="12f31-226">Hello en los ejemplos siguientes muestra cómo toospecify Hola ámbito para los diferentes niveles:</span><span class="sxs-lookup"><span data-stu-id="12f31-226">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="12f31-227">Suscripción: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="12f31-227">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="12f31-228">Grupo de recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="12f31-228">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="12f31-229">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="12f31-229">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="12f31-230">Reemplace *{identificador de definición de rol}* con identificador GUID de Hola Hola de definición del rol.</span><span class="sxs-lookup"><span data-stu-id="12f31-230">Replace *{role-definition-id}* with hello GUID identifier of hello role definition.</span></span>
3. <span data-ttu-id="12f31-231">Reemplace *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="12f31-231">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="12f31-232">Respuesta</span><span class="sxs-lookup"><span data-stu-id="12f31-232">Response</span></span>
<span data-ttu-id="12f31-233">Código de estado: 200</span><span class="sxs-lookup"><span data-stu-id="12f31-233">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access toothem, and not hello virtual network or storage account they\u2019re connected to.",
        "assignableScopes": [
          "/"
        ],
        "permissions": [
          {
            "actions": [
              "Microsoft.Authorization/*/read",
              "Microsoft.Compute/availabilitySets/*",
              "Microsoft.Compute/locations/*",
              "Microsoft.Compute/virtualMachines/*",
              "Microsoft.Compute/virtualMachineScaleSets/*",
              "Microsoft.Insights/alertRules/*",
              "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatRules/join/action",
              "Microsoft.Network/loadBalancers/read",
              "Microsoft.Network/locations/*",
              "Microsoft.Network/networkInterfaces/*",
              "Microsoft.Network/networkSecurityGroups/join/action",
              "Microsoft.Network/networkSecurityGroups/read",
              "Microsoft.Network/publicIPAddresses/join/action",
              "Microsoft.Network/publicIPAddresses/read",
              "Microsoft.Network/virtualNetworks/read",
              "Microsoft.Network/virtualNetworks/subnets/join/action",
              "Microsoft.Resources/deployments/*",
              "Microsoft.Resources/subscriptions/resourceGroups/read",
              "Microsoft.Storage/storageAccounts/listKeys/action",
              "Microsoft.Storage/storageAccounts/read",
              "Microsoft.Support/*"
            ],
            "notActions": []
          }
        ],
        "createdOn": "2015-06-02T00:18:27.3542698Z",
        "updatedOn": "2015-12-08T03:16:55.6170255Z",
        "createdBy": null,
        "updatedBy": null
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
      "type": "Microsoft.Authorization/roleDefinitions",
      "name": "9980e02c-c2be-4d73-94e8-173b1dc7cf3c"
    }
  ],
  "nextLink": null
}

```

## <a name="create-a-custom-role"></a><span data-ttu-id="12f31-234">Creación de un rol personalizado</span><span class="sxs-lookup"><span data-stu-id="12f31-234">Create a Custom Role</span></span>
<span data-ttu-id="12f31-235">Cree un rol personalizado.</span><span class="sxs-lookup"><span data-stu-id="12f31-235">Create a custom role.</span></span>

<span data-ttu-id="12f31-236">toocreate un rol personalizado, debe tener acceso demasiado`Microsoft.Authorization/roleDefinitions/write` operación en todos los hello `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="12f31-236">toocreate a custom role, you must have access too`Microsoft.Authorization/roleDefinitions/write` operation on all hello `AssignableScopes`.</span></span> <span data-ttu-id="12f31-237">De hello funciones integradas solo *propietario* y *Administrador de acceso de usuario* se conceden acceso toothis operación.</span><span class="sxs-lookup"><span data-stu-id="12f31-237">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="12f31-238">Para obtener más información sobre las asignaciones de roles y la administración del acceso a los recursos de Azure, consulte [Control de acceso basado en roles de Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="12f31-238">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="12f31-239">Solicitud</span><span class="sxs-lookup"><span data-stu-id="12f31-239">Request</span></span>
<span data-ttu-id="12f31-240">Hola de uso **colocar** método con hello siguiente URI:</span><span class="sxs-lookup"><span data-stu-id="12f31-240">Use hello **PUT** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="12f31-241">Dentro de hello URI, realice Hola siguiendo las sustituciones toocustomize la solicitud:</span><span class="sxs-lookup"><span data-stu-id="12f31-241">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="12f31-242">Reemplace *{scope}* con hello primera *AssignableScope* de roles personalizados de Hola.</span><span class="sxs-lookup"><span data-stu-id="12f31-242">Replace *{scope}* with hello first *AssignableScope* of hello custom role.</span></span> <span data-ttu-id="12f31-243">Hello en los ejemplos siguientes muestra cómo toospecify Hola ámbito para los diferentes niveles.</span><span class="sxs-lookup"><span data-stu-id="12f31-243">hello following examples show how toospecify hello scope for different levels.</span></span>

   * <span data-ttu-id="12f31-244">Suscripción: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="12f31-244">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="12f31-245">Grupo de recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="12f31-245">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="12f31-246">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="12f31-246">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="12f31-247">Reemplace *{identificador de definición de rol}* con un nuevo GUID, que se convierte en identificador GUID de Hola de nuevo rol personalizado de Hola.</span><span class="sxs-lookup"><span data-stu-id="12f31-247">Replace *{role-definition-id}* with a new GUID, which becomes hello GUID identifier of hello new custom role.</span></span>
3. <span data-ttu-id="12f31-248">Reemplace *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="12f31-248">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="12f31-249">En el cuerpo de solicitud de hello, proporcionar valores de hello en hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="12f31-249">For hello request body, provide hello values in hello following format:</span></span>

```
{
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "properties": {
    "roleName": "Virtual Machine Operator",
    "description": "Lets you monitor virtual machines and restart them.",
    "type": "CustomRole",
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
  }
}

```

| <span data-ttu-id="12f31-250">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="12f31-250">Element Name</span></span> | <span data-ttu-id="12f31-251">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="12f31-251">Required</span></span> | <span data-ttu-id="12f31-252">Tipo</span><span class="sxs-lookup"><span data-stu-id="12f31-252">Type</span></span> | <span data-ttu-id="12f31-253">Description</span><span class="sxs-lookup"><span data-stu-id="12f31-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="12f31-254">name</span><span class="sxs-lookup"><span data-stu-id="12f31-254">name</span></span> |<span data-ttu-id="12f31-255">Sí</span><span class="sxs-lookup"><span data-stu-id="12f31-255">Yes</span></span> |<span data-ttu-id="12f31-256">String</span><span class="sxs-lookup"><span data-stu-id="12f31-256">String</span></span> |<span data-ttu-id="12f31-257">Identificador GUID de rol personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="12f31-257">GUID identifier of hello custom role.</span></span> |
| <span data-ttu-id="12f31-258">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="12f31-258">properties.roleName</span></span> |<span data-ttu-id="12f31-259">Sí</span><span class="sxs-lookup"><span data-stu-id="12f31-259">Yes</span></span> |<span data-ttu-id="12f31-260">String</span><span class="sxs-lookup"><span data-stu-id="12f31-260">String</span></span> |<span data-ttu-id="12f31-261">Nombre para mostrar del rol personalizado Hola.</span><span class="sxs-lookup"><span data-stu-id="12f31-261">Display name of hello custom role.</span></span> <span data-ttu-id="12f31-262">Tamaño máximo: 128 caracteres.</span><span class="sxs-lookup"><span data-stu-id="12f31-262">Maximum size 128 characters.</span></span> |
| <span data-ttu-id="12f31-263">properties.description</span><span class="sxs-lookup"><span data-stu-id="12f31-263">properties.description</span></span> |<span data-ttu-id="12f31-264">No</span><span class="sxs-lookup"><span data-stu-id="12f31-264">No</span></span> |<span data-ttu-id="12f31-265">String</span><span class="sxs-lookup"><span data-stu-id="12f31-265">String</span></span> |<span data-ttu-id="12f31-266">Descripción del rol personalizado Hola.</span><span class="sxs-lookup"><span data-stu-id="12f31-266">Description of hello custom role.</span></span> <span data-ttu-id="12f31-267">Tamaño máximo: 1024 caracteres.</span><span class="sxs-lookup"><span data-stu-id="12f31-267">Maximum size 1024 characters.</span></span> |
| <span data-ttu-id="12f31-268">properties.type</span><span class="sxs-lookup"><span data-stu-id="12f31-268">properties.type</span></span> |<span data-ttu-id="12f31-269">Sí</span><span class="sxs-lookup"><span data-stu-id="12f31-269">Yes</span></span> |<span data-ttu-id="12f31-270">String</span><span class="sxs-lookup"><span data-stu-id="12f31-270">String</span></span> |<span data-ttu-id="12f31-271">Establecer demasiado "CustomRole."</span><span class="sxs-lookup"><span data-stu-id="12f31-271">Set too"CustomRole."</span></span> |
| <span data-ttu-id="12f31-272">properties.permissions.actions</span><span class="sxs-lookup"><span data-stu-id="12f31-272">properties.permissions.actions</span></span> |<span data-ttu-id="12f31-273">yes</span><span class="sxs-lookup"><span data-stu-id="12f31-273">Yes</span></span> |<span data-ttu-id="12f31-274">String[]</span><span class="sxs-lookup"><span data-stu-id="12f31-274">String[]</span></span> |<span data-ttu-id="12f31-275">Una matriz de acción cadenas especificando las operaciones de hello concedidas por roles personalizados de Hola.</span><span class="sxs-lookup"><span data-stu-id="12f31-275">An array of action strings specifying hello operations granted by hello custom role.</span></span> |
| <span data-ttu-id="12f31-276">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="12f31-276">properties.permissions.notActions</span></span> |<span data-ttu-id="12f31-277">No</span><span class="sxs-lookup"><span data-stu-id="12f31-277">No</span></span> |<span data-ttu-id="12f31-278">String[]</span><span class="sxs-lookup"><span data-stu-id="12f31-278">String[]</span></span> |<span data-ttu-id="12f31-279">Una matriz de cadenas de acción especificar Hola operaciones tooexclude de las operaciones de hello concedidos por roles personalizados de Hola.</span><span class="sxs-lookup"><span data-stu-id="12f31-279">An array of action strings specifying hello operations tooexclude from hello operations granted by hello custom role.</span></span> |
| <span data-ttu-id="12f31-280">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="12f31-280">properties.assignableScopes</span></span> |<span data-ttu-id="12f31-281">yes</span><span class="sxs-lookup"><span data-stu-id="12f31-281">Yes</span></span> |<span data-ttu-id="12f31-282">String[]</span><span class="sxs-lookup"><span data-stu-id="12f31-282">String[]</span></span> |<span data-ttu-id="12f31-283">Una matriz de ámbitos en qué Hola se puede usar el rol personalizado.</span><span class="sxs-lookup"><span data-stu-id="12f31-283">An array of scopes in which hello custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="12f31-284">Response</span><span class="sxs-lookup"><span data-stu-id="12f31-284">Response</span></span>
<span data-ttu-id="12f31-285">Código de estado: 201</span><span class="sxs-lookup"><span data-stu-id="12f31-285">Status code: 201</span></span>

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-18T00:10:51.4662695Z",
    "updatedOn": "2015-12-18T00:10:51.4662695Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7"
}

```

## <a name="update-a-custom-role"></a><span data-ttu-id="12f31-286">Actualización de un rol personalizado</span><span class="sxs-lookup"><span data-stu-id="12f31-286">Update a Custom Role</span></span>
<span data-ttu-id="12f31-287">Modifique un rol personalizado.</span><span class="sxs-lookup"><span data-stu-id="12f31-287">Modify a custom role.</span></span>

<span data-ttu-id="12f31-288">toomodify un rol personalizado, debe tener acceso demasiado`Microsoft.Authorization/roleDefinitions/write` operación en todos los hello `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="12f31-288">toomodify a custom role, you must have access too`Microsoft.Authorization/roleDefinitions/write` operation on all hello `AssignableScopes`.</span></span> <span data-ttu-id="12f31-289">De hello funciones integradas solo *propietario* y *Administrador de acceso de usuario* se conceden acceso toothis operación.</span><span class="sxs-lookup"><span data-stu-id="12f31-289">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="12f31-290">Para obtener más información sobre las asignaciones de roles y la administración del acceso a los recursos de Azure, consulte [Control de acceso basado en roles de Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="12f31-290">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="12f31-291">Solicitud</span><span class="sxs-lookup"><span data-stu-id="12f31-291">Request</span></span>
<span data-ttu-id="12f31-292">Hola de uso **colocar** método con hello siguiente URI:</span><span class="sxs-lookup"><span data-stu-id="12f31-292">Use hello **PUT** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="12f31-293">Dentro de hello URI, realice Hola siguiendo las sustituciones toocustomize la solicitud:</span><span class="sxs-lookup"><span data-stu-id="12f31-293">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="12f31-294">Reemplace *{scope}* con hello primera *AssignableScope* de roles personalizados de Hola.</span><span class="sxs-lookup"><span data-stu-id="12f31-294">Replace *{scope}* with hello first *AssignableScope* of hello custom role.</span></span> <span data-ttu-id="12f31-295">Hello en los ejemplos siguientes muestra cómo toospecify Hola ámbito para los diferentes niveles:</span><span class="sxs-lookup"><span data-stu-id="12f31-295">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="12f31-296">Suscripción: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="12f31-296">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="12f31-297">Grupo de recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="12f31-297">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="12f31-298">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="12f31-298">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="12f31-299">Reemplace *{identificador de definición de rol}* con identificador GUID de Hola de roles personalizados de Hola.</span><span class="sxs-lookup"><span data-stu-id="12f31-299">Replace *{role-definition-id}* with hello GUID identifier of hello custom role.</span></span>
3. <span data-ttu-id="12f31-300">Reemplace *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="12f31-300">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="12f31-301">En el cuerpo de solicitud de hello, proporcionar valores de hello en hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="12f31-301">For hello request body, provide hello values in hello following format:</span></span>

```
{
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "properties": {
    "roleName": "Virtual Machine Operator",
    "description": "Lets you monitor virtual machines and restart them.",
    "type": "CustomRole",
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
  }
}

```

| <span data-ttu-id="12f31-302">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="12f31-302">Element Name</span></span> | <span data-ttu-id="12f31-303">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="12f31-303">Required</span></span> | <span data-ttu-id="12f31-304">Tipo</span><span class="sxs-lookup"><span data-stu-id="12f31-304">Type</span></span> | <span data-ttu-id="12f31-305">Description</span><span class="sxs-lookup"><span data-stu-id="12f31-305">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="12f31-306">name</span><span class="sxs-lookup"><span data-stu-id="12f31-306">name</span></span> |<span data-ttu-id="12f31-307">Sí</span><span class="sxs-lookup"><span data-stu-id="12f31-307">Yes</span></span> |<span data-ttu-id="12f31-308">String</span><span class="sxs-lookup"><span data-stu-id="12f31-308">String</span></span> |<span data-ttu-id="12f31-309">Identificador GUID de rol personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="12f31-309">GUID identifier of hello custom role.</span></span> |
| <span data-ttu-id="12f31-310">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="12f31-310">properties.roleName</span></span> |<span data-ttu-id="12f31-311">Sí</span><span class="sxs-lookup"><span data-stu-id="12f31-311">Yes</span></span> |<span data-ttu-id="12f31-312">String</span><span class="sxs-lookup"><span data-stu-id="12f31-312">String</span></span> |<span data-ttu-id="12f31-313">Nombre para mostrar de hello rol personalizado actualizó.</span><span class="sxs-lookup"><span data-stu-id="12f31-313">Display name of hello updated custom role.</span></span> |
| <span data-ttu-id="12f31-314">properties.description</span><span class="sxs-lookup"><span data-stu-id="12f31-314">properties.description</span></span> |<span data-ttu-id="12f31-315">No</span><span class="sxs-lookup"><span data-stu-id="12f31-315">No</span></span> |<span data-ttu-id="12f31-316">String</span><span class="sxs-lookup"><span data-stu-id="12f31-316">String</span></span> |<span data-ttu-id="12f31-317">Descripción de hello rol personalizado actualizó.</span><span class="sxs-lookup"><span data-stu-id="12f31-317">Description of hello updated custom role.</span></span> |
| <span data-ttu-id="12f31-318">properties.type</span><span class="sxs-lookup"><span data-stu-id="12f31-318">properties.type</span></span> |<span data-ttu-id="12f31-319">Sí</span><span class="sxs-lookup"><span data-stu-id="12f31-319">Yes</span></span> |<span data-ttu-id="12f31-320">String</span><span class="sxs-lookup"><span data-stu-id="12f31-320">String</span></span> |<span data-ttu-id="12f31-321">Establecer demasiado "CustomRole."</span><span class="sxs-lookup"><span data-stu-id="12f31-321">Set too"CustomRole."</span></span> |
| <span data-ttu-id="12f31-322">properties.permissions.actions</span><span class="sxs-lookup"><span data-stu-id="12f31-322">properties.permissions.actions</span></span> |<span data-ttu-id="12f31-323">yes</span><span class="sxs-lookup"><span data-stu-id="12f31-323">Yes</span></span> |<span data-ttu-id="12f31-324">String[]</span><span class="sxs-lookup"><span data-stu-id="12f31-324">String[]</span></span> |<span data-ttu-id="12f31-325">Una matriz de cadenas de acción especificar Hola Hola de toowhich de operaciones había actualizado concede acceso de roles personalizados.</span><span class="sxs-lookup"><span data-stu-id="12f31-325">An array of action strings specifying hello operations toowhich hello updated custom role grants access.</span></span> |
| <span data-ttu-id="12f31-326">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="12f31-326">properties.permissions.notActions</span></span> |<span data-ttu-id="12f31-327">No</span><span class="sxs-lookup"><span data-stu-id="12f31-327">No</span></span> |<span data-ttu-id="12f31-328">String[]</span><span class="sxs-lookup"><span data-stu-id="12f31-328">String[]</span></span> |<span data-ttu-id="12f31-329">Una matriz de acción cadenas especificando Hola operaciones tooexclude de las operaciones de hello qué Hola actualiza concesiones de roles personalizados.</span><span class="sxs-lookup"><span data-stu-id="12f31-329">An array of action strings specifying hello operations tooexclude from hello operations which hello updated custom role grants.</span></span> |
| <span data-ttu-id="12f31-330">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="12f31-330">properties.assignableScopes</span></span> |<span data-ttu-id="12f31-331">yes</span><span class="sxs-lookup"><span data-stu-id="12f31-331">Yes</span></span> |<span data-ttu-id="12f31-332">String[]</span><span class="sxs-lookup"><span data-stu-id="12f31-332">String[]</span></span> |<span data-ttu-id="12f31-333">Una matriz de ámbitos en qué Hola se puede usar el rol personalizado actualizado.</span><span class="sxs-lookup"><span data-stu-id="12f31-333">An array of scopes in which hello updated custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="12f31-334">Response</span><span class="sxs-lookup"><span data-stu-id="12f31-334">Response</span></span>
<span data-ttu-id="12f31-335">Código de estado: 201</span><span class="sxs-lookup"><span data-stu-id="12f31-335">Status code: 201</span></span>

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-18T00:10:51.4662695Z",
    "updatedOn": "2015-12-18T00:10:51.4662695Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7"
}

```

## <a name="delete-a-custom-role"></a><span data-ttu-id="12f31-336">Eliminación de un rol personalizado</span><span class="sxs-lookup"><span data-stu-id="12f31-336">Delete a Custom Role</span></span>
<span data-ttu-id="12f31-337">Elimine un rol personalizado.</span><span class="sxs-lookup"><span data-stu-id="12f31-337">Delete a custom role.</span></span>

<span data-ttu-id="12f31-338">toodelete un rol personalizado, debe tener acceso demasiado`Microsoft.Authorization/roleDefinitions/delete` operación en todos los hello `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="12f31-338">toodelete a custom role, you must have access too`Microsoft.Authorization/roleDefinitions/delete` operation on all hello `AssignableScopes`.</span></span> <span data-ttu-id="12f31-339">De hello funciones integradas solo *propietario* y *Administrador de acceso de usuario* se conceden acceso toothis operación.</span><span class="sxs-lookup"><span data-stu-id="12f31-339">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="12f31-340">Para obtener más información sobre las asignaciones de roles y la administración del acceso a los recursos de Azure, consulte [Control de acceso basado en roles de Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="12f31-340">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="12f31-341">Solicitud</span><span class="sxs-lookup"><span data-stu-id="12f31-341">Request</span></span>
<span data-ttu-id="12f31-342">Hola de uso **eliminar** método con hello siguiente URI:</span><span class="sxs-lookup"><span data-stu-id="12f31-342">Use hello **DELETE** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="12f31-343">Dentro de hello URI, realice Hola siguiendo las sustituciones toocustomize la solicitud:</span><span class="sxs-lookup"><span data-stu-id="12f31-343">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="12f31-344">Reemplace *{scope}* con ámbito de hello en el que desea definición de roles de toodelete Hola.</span><span class="sxs-lookup"><span data-stu-id="12f31-344">Replace *{scope}* with hello scope at which you wish toodelete hello role definition.</span></span> <span data-ttu-id="12f31-345">Hello en los ejemplos siguientes muestra cómo toospecify Hola ámbito para los diferentes niveles:</span><span class="sxs-lookup"><span data-stu-id="12f31-345">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="12f31-346">Suscripción: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="12f31-346">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="12f31-347">Grupo de recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="12f31-347">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="12f31-348">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="12f31-348">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="12f31-349">Reemplace *{identificador de definición de rol}* con identificación de definición de rol de hello GUID de rol personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="12f31-349">Replace *{role-definition-id}* with hello GUID role definition id of hello custom role.</span></span>
3. <span data-ttu-id="12f31-350">Reemplace *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="12f31-350">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="12f31-351">Respuesta</span><span class="sxs-lookup"><span data-stu-id="12f31-351">Response</span></span>
<span data-ttu-id="12f31-352">Código de estado: 200</span><span class="sxs-lookup"><span data-stu-id="12f31-352">Status code: 200</span></span>

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-16T00:07:02.9236555Z",
    "updatedOn": "2015-12-16T00:07:02.9236555Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/0bd62a70-e1b8-4e0b-a7c2-75cab365c95b",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "0bd62a70-e1b8-4e0b-a7c2-75cab365c95b"
}

```

## <a name="next-steps"></a><span data-ttu-id="12f31-353">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="12f31-353">Next steps</span></span>

[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]
