---
title: Control de acceso basado en rol con REST de Azure AD | Microsoft Docs
description: "Administración del control de acceso basado en rol con la API de REST"
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
ms.openlocfilehash: a5c19fd87ce1ae3e199bf1dfc8cf82f5653baac2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="manage-role-based-access-control-with-the-rest-api"></a><span data-ttu-id="b57f9-103">Administración del control de acceso basado en rol con la API de REST</span><span class="sxs-lookup"><span data-stu-id="b57f9-103">Manage Role-Based Access Control with the REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b57f9-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b57f9-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="b57f9-105">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="b57f9-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="b57f9-106">API DE REST</span><span class="sxs-lookup"><span data-stu-id="b57f9-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="b57f9-107">El control de acceso basado en roles (RBAC) de Azure Portal y la API de Azure Resource Manager le ayudan a administrar el acceso a su suscripción y sus recursos en un nivel específico.</span><span class="sxs-lookup"><span data-stu-id="b57f9-107">Role-Based Access Control (RBAC) in the Azure portal and Azure Resource Manager API helps you manage access to your subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="b57f9-108">Con esta característica, puede conceder acceso a usuarios, grupos o entidades de seguridad de servicio de Active Directory asignándoles roles en un ámbito determinado.</span><span class="sxs-lookup"><span data-stu-id="b57f9-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles to them at a particular scope.</span></span>

## <a name="list-all-role-assignments"></a><span data-ttu-id="b57f9-109">Lista de todas las asignaciones de roles</span><span class="sxs-lookup"><span data-stu-id="b57f9-109">List all role assignments</span></span>
<span data-ttu-id="b57f9-110">Proporciona una lista todas las asignaciones de roles en el ámbito y los ámbitos secundarios especificados.</span><span class="sxs-lookup"><span data-stu-id="b57f9-110">Lists all the role assignments at the specified scope and subscopes.</span></span>

<span data-ttu-id="b57f9-111">Para obtener una lista de las asignaciones de roles, debe tener acceso a la operación `Microsoft.Authorization/roleAssignments/read` en el ámbito.</span><span class="sxs-lookup"><span data-stu-id="b57f9-111">To list role assignments, you must have access to `Microsoft.Authorization/roleAssignments/read` operation at the scope.</span></span> <span data-ttu-id="b57f9-112">Se concede acceso a esta operación a todos los roles integrados.</span><span class="sxs-lookup"><span data-stu-id="b57f9-112">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="b57f9-113">Para obtener más información sobre las asignaciones de roles y la administración del acceso a los recursos de Azure, consulte [Control de acceso basado en roles de Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b57f9-113">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="b57f9-114">Solicitud</span><span class="sxs-lookup"><span data-stu-id="b57f9-114">Request</span></span>
<span data-ttu-id="b57f9-115">Use el método **GET** con el identificador URI siguiente:</span><span class="sxs-lookup"><span data-stu-id="b57f9-115">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments?api-version={api-version}&$filter={filter}

<span data-ttu-id="b57f9-116">Dentro del URI, realice las sustituciones siguientes para personalizar la solicitud:</span><span class="sxs-lookup"><span data-stu-id="b57f9-116">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="b57f9-117">Reemplace *{scope}* por el ámbito cuya lista de asignaciones de roles quiere obtener.</span><span class="sxs-lookup"><span data-stu-id="b57f9-117">Replace *{scope}* with the scope for which you wish to list the role assignments.</span></span> <span data-ttu-id="b57f9-118">En los ejemplos siguientes, se muestra cómo especificar el ámbito para los distintos niveles:</span><span class="sxs-lookup"><span data-stu-id="b57f9-118">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="b57f9-119">Suscripción: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="b57f9-119">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="b57f9-120">Grupo de recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="b57f9-120">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="b57f9-121">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="b57f9-121">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="b57f9-122">Reemplace *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="b57f9-122">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="b57f9-123">Reemplace *{filter}* por la condición que quiere aplicar para filtrar la lista de asignación de roles:</span><span class="sxs-lookup"><span data-stu-id="b57f9-123">Replace *{filter}* with the condition that you wish to apply to filter the role assignment list:</span></span>

   * <span data-ttu-id="b57f9-124">Lista de las asignaciones de roles únicamente para el ámbito especificado, sin incluir las asignaciones de roles en ámbitos secundarios: `atScope()`</span><span class="sxs-lookup"><span data-stu-id="b57f9-124">List role assignments for only the specified scope, not including the role assignments at subscopes: `atScope()`</span></span>    
   * <span data-ttu-id="b57f9-125">Lista de las asignaciones de roles para solo un usuario, un grupo o una aplicación determinados: `principalId%20eq%20'{objectId of user, group, or service principal}'`</span><span class="sxs-lookup"><span data-stu-id="b57f9-125">List role assignments for a specific user, group, or application: `principalId%20eq%20'{objectId of user, group, or service principal}'`</span></span>  
   * <span data-ttu-id="b57f9-126">Lista de asignaciones de roles para un usuario específico, incluidas las heredadas de grupos | `assignedTo('{objectId of user}')`</span><span class="sxs-lookup"><span data-stu-id="b57f9-126">List role assignments for a specific user, including ones inherited from groups | `assignedTo('{objectId of user}')`</span></span>

### <a name="response"></a><span data-ttu-id="b57f9-127">Respuesta</span><span class="sxs-lookup"><span data-stu-id="b57f9-127">Response</span></span>
<span data-ttu-id="b57f9-128">Código de estado: 200</span><span class="sxs-lookup"><span data-stu-id="b57f9-128">Status code: 200</span></span>

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

## <a name="get-information-about-a-role-assignment"></a><span data-ttu-id="b57f9-129">Obtención de información sobre una asignación de roles</span><span class="sxs-lookup"><span data-stu-id="b57f9-129">Get information about a role assignment</span></span>
<span data-ttu-id="b57f9-130">Obtiene información sobre una única asignación de roles especificada por el identificador de asignación de roles.</span><span class="sxs-lookup"><span data-stu-id="b57f9-130">Gets information about a single role assignment specified by the role assignment identifier.</span></span>

<span data-ttu-id="b57f9-131">Para obtener información sobre una asignación de roles, debe tener acceso a la operación `Microsoft.Authorization/roleAssignments/read` .</span><span class="sxs-lookup"><span data-stu-id="b57f9-131">To get information about a role assignment, you must have access to `Microsoft.Authorization/roleAssignments/read` operation.</span></span> <span data-ttu-id="b57f9-132">Se concede acceso a esta operación a todos los roles integrados.</span><span class="sxs-lookup"><span data-stu-id="b57f9-132">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="b57f9-133">Para obtener más información sobre las asignaciones de roles y la administración del acceso a los recursos de Azure, consulte [Control de acceso basado en roles de Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b57f9-133">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="b57f9-134">Solicitud</span><span class="sxs-lookup"><span data-stu-id="b57f9-134">Request</span></span>
<span data-ttu-id="b57f9-135">Use el método **GET** con el identificador URI siguiente:</span><span class="sxs-lookup"><span data-stu-id="b57f9-135">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="b57f9-136">Dentro del URI, realice las sustituciones siguientes para personalizar la solicitud:</span><span class="sxs-lookup"><span data-stu-id="b57f9-136">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="b57f9-137">Reemplace *{scope}* por el ámbito cuya lista de asignaciones de roles quiere obtener.</span><span class="sxs-lookup"><span data-stu-id="b57f9-137">Replace *{scope}* with the scope for which you wish to list the role assignments.</span></span> <span data-ttu-id="b57f9-138">En los ejemplos siguientes, se muestra cómo especificar el ámbito para los distintos niveles:</span><span class="sxs-lookup"><span data-stu-id="b57f9-138">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="b57f9-139">Suscripción: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="b57f9-139">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="b57f9-140">Grupo de recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="b57f9-140">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="b57f9-141">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="b57f9-141">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="b57f9-142">Reemplace *{role-assignment-id}* por el identificador GUID de la asignación de roles.</span><span class="sxs-lookup"><span data-stu-id="b57f9-142">Replace *{role-assignment-id}* with the GUID identifier of the role assignment.</span></span>
3. <span data-ttu-id="b57f9-143">Reemplace *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="b57f9-143">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="b57f9-144">Respuesta</span><span class="sxs-lookup"><span data-stu-id="b57f9-144">Response</span></span>
<span data-ttu-id="b57f9-145">Código de estado: 200</span><span class="sxs-lookup"><span data-stu-id="b57f9-145">Status code: 200</span></span>

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

## <a name="create-a-role-assignment"></a><span data-ttu-id="b57f9-146">Creación de una asignación de roles</span><span class="sxs-lookup"><span data-stu-id="b57f9-146">Create a Role Assignment</span></span>
<span data-ttu-id="b57f9-147">Cree una asignación de roles en el ámbito especificado para la entidad de seguridad especificada que concede el rol especificado.</span><span class="sxs-lookup"><span data-stu-id="b57f9-147">Create a role assignment at the specified scope for the specified principal granting the specified role.</span></span>

<span data-ttu-id="b57f9-148">Para crear una asignación de roles, debe tener acceso a la operación `Microsoft.Authorization/roleAssignments/write` .</span><span class="sxs-lookup"><span data-stu-id="b57f9-148">To create a role assignment, you must have access to `Microsoft.Authorization/roleAssignments/write` operation.</span></span> <span data-ttu-id="b57f9-149">Entre los roles integrados, solo se concede acceso a esta operación a *Propietario* y *Administrador de acceso de usuario*.</span><span class="sxs-lookup"><span data-stu-id="b57f9-149">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="b57f9-150">Para obtener más información sobre las asignaciones de roles y la administración del acceso a los recursos de Azure, consulte [Control de acceso basado en roles de Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b57f9-150">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="b57f9-151">Solicitud</span><span class="sxs-lookup"><span data-stu-id="b57f9-151">Request</span></span>
<span data-ttu-id="b57f9-152">Use el método **PUT** con el URI siguiente:</span><span class="sxs-lookup"><span data-stu-id="b57f9-152">Use the **PUT** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="b57f9-153">Dentro del URI, realice las sustituciones siguientes para personalizar la solicitud:</span><span class="sxs-lookup"><span data-stu-id="b57f9-153">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="b57f9-154">Reemplace *{scope}* por el ámbito en el que quiere crear las asignaciones de roles.</span><span class="sxs-lookup"><span data-stu-id="b57f9-154">Replace *{scope}* with the scope at which you wish to create the role assignments.</span></span> <span data-ttu-id="b57f9-155">Cuando se crea una asignación de roles en un ámbito primario, todos los ámbitos secundarios heredan la misma asignación de roles.</span><span class="sxs-lookup"><span data-stu-id="b57f9-155">When you create a role assignment at a parent scope, all child scopes inherit the same role assignment.</span></span> <span data-ttu-id="b57f9-156">En los ejemplos siguientes, se muestra cómo especificar el ámbito para los distintos niveles:</span><span class="sxs-lookup"><span data-stu-id="b57f9-156">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="b57f9-157">Suscripción: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="b57f9-157">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="b57f9-158">Grupo de recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="b57f9-158">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>   
   * <span data-ttu-id="b57f9-159">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="b57f9-159">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="b57f9-160">Reemplace *{role-assignment-id}* por un nuevo GUID, que se convierte en el GUID de la nueva asignación de roles.</span><span class="sxs-lookup"><span data-stu-id="b57f9-160">Replace *{role-assignment-id}* with a new GUID, which becomes the GUID identifier of the new role assignment.</span></span>
3. <span data-ttu-id="b57f9-161">Reemplace *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="b57f9-161">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="b57f9-162">Para el cuerpo de la solicitud, proporcione los valores en el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="b57f9-162">For the request body, provide the values in the following format:</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b"
  }
}

```

| <span data-ttu-id="b57f9-163">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="b57f9-163">Element Name</span></span> | <span data-ttu-id="b57f9-164">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="b57f9-164">Required</span></span> | <span data-ttu-id="b57f9-165">Tipo</span><span class="sxs-lookup"><span data-stu-id="b57f9-165">Type</span></span> | <span data-ttu-id="b57f9-166">Description</span><span class="sxs-lookup"><span data-stu-id="b57f9-166">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b57f9-167">roleDefinitionId</span><span class="sxs-lookup"><span data-stu-id="b57f9-167">roleDefinitionId</span></span> |<span data-ttu-id="b57f9-168">Sí</span><span class="sxs-lookup"><span data-stu-id="b57f9-168">Yes</span></span> |<span data-ttu-id="b57f9-169">String</span><span class="sxs-lookup"><span data-stu-id="b57f9-169">String</span></span> |<span data-ttu-id="b57f9-170">Identificador del rol.</span><span class="sxs-lookup"><span data-stu-id="b57f9-170">The identifier of the role.</span></span> <span data-ttu-id="b57f9-171">El formato del identificador es: `{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span><span class="sxs-lookup"><span data-stu-id="b57f9-171">The format of the identifier is: `{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span></span> |
| <span data-ttu-id="b57f9-172">principalId</span><span class="sxs-lookup"><span data-stu-id="b57f9-172">principalId</span></span> |<span data-ttu-id="b57f9-173">Sí</span><span class="sxs-lookup"><span data-stu-id="b57f9-173">Yes</span></span> |<span data-ttu-id="b57f9-174">String</span><span class="sxs-lookup"><span data-stu-id="b57f9-174">String</span></span> |<span data-ttu-id="b57f9-175">objectId de la entidad de seguridad de Azure AD (usuario, grupo o entidad de servicio) a la que se va a asignar el rol.</span><span class="sxs-lookup"><span data-stu-id="b57f9-175">objectId of the Azure AD principal (user, group, or service principal) to which the role is assigned.</span></span> |

### <a name="response"></a><span data-ttu-id="b57f9-176">Respuesta</span><span class="sxs-lookup"><span data-stu-id="b57f9-176">Response</span></span>
<span data-ttu-id="b57f9-177">Código de estado: 201</span><span class="sxs-lookup"><span data-stu-id="b57f9-177">Status code: 201</span></span>

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

## <a name="delete-a-role-assignment"></a><span data-ttu-id="b57f9-178">Eliminación de una asignación de roles</span><span class="sxs-lookup"><span data-stu-id="b57f9-178">Delete a Role Assignment</span></span>
<span data-ttu-id="b57f9-179">Elimine una asignación de roles en el ámbito especificado.</span><span class="sxs-lookup"><span data-stu-id="b57f9-179">Delete a role assignment at the specified scope.</span></span>

<span data-ttu-id="b57f9-180">Para eliminar una asignación de roles, debe tener acceso a la operación `Microsoft.Authorization/roleAssignments/delete` .</span><span class="sxs-lookup"><span data-stu-id="b57f9-180">To delete a role assignment, you must have access to the `Microsoft.Authorization/roleAssignments/delete` operation.</span></span> <span data-ttu-id="b57f9-181">Entre los roles integrados, solo se concede acceso a esta operación a *Propietario* y *Administrador de acceso de usuario*.</span><span class="sxs-lookup"><span data-stu-id="b57f9-181">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="b57f9-182">Para obtener más información sobre las asignaciones de roles y la administración del acceso a los recursos de Azure, consulte [Control de acceso basado en roles de Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b57f9-182">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="b57f9-183">Solicitud</span><span class="sxs-lookup"><span data-stu-id="b57f9-183">Request</span></span>
<span data-ttu-id="b57f9-184">Use el método **DELETE** con el URI siguiente:</span><span class="sxs-lookup"><span data-stu-id="b57f9-184">Use the **DELETE** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="b57f9-185">Dentro del URI, realice las sustituciones siguientes para personalizar la solicitud:</span><span class="sxs-lookup"><span data-stu-id="b57f9-185">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="b57f9-186">Reemplace *{scope}* por el ámbito en el que quiere crear las asignaciones de roles.</span><span class="sxs-lookup"><span data-stu-id="b57f9-186">Replace *{scope}* with the scope at which you wish to create the role assignments.</span></span> <span data-ttu-id="b57f9-187">En los ejemplos siguientes, se muestra cómo especificar el ámbito para los distintos niveles:</span><span class="sxs-lookup"><span data-stu-id="b57f9-187">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="b57f9-188">Suscripción: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="b57f9-188">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="b57f9-189">Grupo de recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="b57f9-189">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="b57f9-190">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="b57f9-190">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="b57f9-191">Reemplace *{role-assignment-id}* por el identificador GUID de la asignación de roles.</span><span class="sxs-lookup"><span data-stu-id="b57f9-191">Replace *{role-assignment-id}* with the role assignment id GUID.</span></span>
3. <span data-ttu-id="b57f9-192">Reemplace *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="b57f9-192">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="b57f9-193">Respuesta</span><span class="sxs-lookup"><span data-stu-id="b57f9-193">Response</span></span>
<span data-ttu-id="b57f9-194">Código de estado: 200</span><span class="sxs-lookup"><span data-stu-id="b57f9-194">Status code: 200</span></span>

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

## <a name="list-all-roles"></a><span data-ttu-id="b57f9-195">Lista de todos los roles</span><span class="sxs-lookup"><span data-stu-id="b57f9-195">List all Roles</span></span>
<span data-ttu-id="b57f9-196">Proporciona una lista de todos los roles disponibles para asignarse en el ámbito especificado.</span><span class="sxs-lookup"><span data-stu-id="b57f9-196">Lists all the roles that are available for assignment at the specified scope.</span></span>

<span data-ttu-id="b57f9-197">Para obtener una lista de roles, debe tener acceso a la operación `Microsoft.Authorization/roleDefinitions/read` en el ámbito.</span><span class="sxs-lookup"><span data-stu-id="b57f9-197">To list roles, you must have access to `Microsoft.Authorization/roleDefinitions/read` operation at the scope.</span></span> <span data-ttu-id="b57f9-198">Se concede acceso a esta operación a todos los roles integrados.</span><span class="sxs-lookup"><span data-stu-id="b57f9-198">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="b57f9-199">Para obtener más información sobre las asignaciones de roles y la administración del acceso a los recursos de Azure, consulte [Control de acceso basado en roles de Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b57f9-199">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="b57f9-200">Solicitud</span><span class="sxs-lookup"><span data-stu-id="b57f9-200">Request</span></span>
<span data-ttu-id="b57f9-201">Use el método **GET** con el identificador URI siguiente:</span><span class="sxs-lookup"><span data-stu-id="b57f9-201">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions?api-version={api-version}&$filter={filter}

<span data-ttu-id="b57f9-202">Dentro del URI, realice las sustituciones siguientes para personalizar la solicitud:</span><span class="sxs-lookup"><span data-stu-id="b57f9-202">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="b57f9-203">Reemplace *{scope}* por el ámbito cuya lista de roles quiere obtener.</span><span class="sxs-lookup"><span data-stu-id="b57f9-203">Replace *{scope}* with the scope for which you wish to list the roles.</span></span> <span data-ttu-id="b57f9-204">En los ejemplos siguientes, se muestra cómo especificar el ámbito para los distintos niveles:</span><span class="sxs-lookup"><span data-stu-id="b57f9-204">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="b57f9-205">Suscripción: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="b57f9-205">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="b57f9-206">Grupo de recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="b57f9-206">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="b57f9-207">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="b57f9-207">Resource /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="b57f9-208">Reemplace *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="b57f9-208">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="b57f9-209">Reemplace *{filter}* por la condición que quiere aplicar para filtrar la lista de roles:</span><span class="sxs-lookup"><span data-stu-id="b57f9-209">Replace *{filter}* with the condition that you wish to apply to filter the list of roles:</span></span>

   * <span data-ttu-id="b57f9-210">Enumerar los roles disponibles para asignar en el ámbito especificado y cualquiera de sus ámbitos secundarios: `atScopeAndBelow()`</span><span class="sxs-lookup"><span data-stu-id="b57f9-210">List roles available for assignment at the specified scope and any of its child scopes: `atScopeAndBelow()`</span></span>
   * <span data-ttu-id="b57f9-211">Buscar un rol con un nombre para mostrar exacto: `roleName%20eq%20'{role-display-name}'`.</span><span class="sxs-lookup"><span data-stu-id="b57f9-211">Search for a role using exact display name: `roleName%20eq%20'{role-display-name}'`.</span></span> <span data-ttu-id="b57f9-212">Use la forma con codificación URL del nombre para mostrar exacto del rol.</span><span class="sxs-lookup"><span data-stu-id="b57f9-212">Use the URL encoded form of the exact display name of the role.</span></span> <span data-ttu-id="b57f9-213">Por ejemplo, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span><span class="sxs-lookup"><span data-stu-id="b57f9-213">For instance, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span></span>

### <a name="response"></a><span data-ttu-id="b57f9-214">Respuesta</span><span class="sxs-lookup"><span data-stu-id="b57f9-214">Response</span></span>
<span data-ttu-id="b57f9-215">Código de estado: 200</span><span class="sxs-lookup"><span data-stu-id="b57f9-215">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access to them, and not the virtual network or storage account they\u2019re connected to.",
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

## <a name="get-information-about-a-role"></a><span data-ttu-id="b57f9-216">Obtención de información sobre un rol</span><span class="sxs-lookup"><span data-stu-id="b57f9-216">Get information about a Role</span></span>
<span data-ttu-id="b57f9-217">Obtiene información sobre un único rol especificado por el identificador de la definición de roles.</span><span class="sxs-lookup"><span data-stu-id="b57f9-217">Gets information about a single role specified by the role definition identifier.</span></span> <span data-ttu-id="b57f9-218">Para obtener información sobre un solo rol utilizando su nombre para mostrar, consulte [Lista de todos los roles](role-based-access-control-manage-access-rest.md#list-all-roles).</span><span class="sxs-lookup"><span data-stu-id="b57f9-218">To get information about a single role using its display name, see [List all roles](role-based-access-control-manage-access-rest.md#list-all-roles).</span></span>

<span data-ttu-id="b57f9-219">Para obtener información sobre un rol, debe tener acceso a la operación `Microsoft.Authorization/roleDefinitions/read` .</span><span class="sxs-lookup"><span data-stu-id="b57f9-219">To get information about a role, you must have access to `Microsoft.Authorization/roleDefinitions/read` operation.</span></span> <span data-ttu-id="b57f9-220">Se concede acceso a esta operación a todos los roles integrados.</span><span class="sxs-lookup"><span data-stu-id="b57f9-220">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="b57f9-221">Para obtener más información sobre las asignaciones de roles y la administración del acceso a los recursos de Azure, consulte [Control de acceso basado en roles de Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b57f9-221">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="b57f9-222">Solicitud</span><span class="sxs-lookup"><span data-stu-id="b57f9-222">Request</span></span>
<span data-ttu-id="b57f9-223">Use el método **GET** con el identificador URI siguiente:</span><span class="sxs-lookup"><span data-stu-id="b57f9-223">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="b57f9-224">Dentro del URI, realice las sustituciones siguientes para personalizar la solicitud:</span><span class="sxs-lookup"><span data-stu-id="b57f9-224">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="b57f9-225">Reemplace *{scope}* por el ámbito cuya lista de asignaciones de roles quiere obtener.</span><span class="sxs-lookup"><span data-stu-id="b57f9-225">Replace *{scope}* with the scope for which you wish to list the role assignments.</span></span> <span data-ttu-id="b57f9-226">En los ejemplos siguientes, se muestra cómo especificar el ámbito para los distintos niveles:</span><span class="sxs-lookup"><span data-stu-id="b57f9-226">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="b57f9-227">Suscripción: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="b57f9-227">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="b57f9-228">Grupo de recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="b57f9-228">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="b57f9-229">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="b57f9-229">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="b57f9-230">Reemplace *{role-definition-id}* por el identificador GUID de la definición de roles.</span><span class="sxs-lookup"><span data-stu-id="b57f9-230">Replace *{role-definition-id}* with the GUID identifier of the role definition.</span></span>
3. <span data-ttu-id="b57f9-231">Reemplace *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="b57f9-231">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="b57f9-232">Respuesta</span><span class="sxs-lookup"><span data-stu-id="b57f9-232">Response</span></span>
<span data-ttu-id="b57f9-233">Código de estado: 200</span><span class="sxs-lookup"><span data-stu-id="b57f9-233">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access to them, and not the virtual network or storage account they\u2019re connected to.",
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

## <a name="create-a-custom-role"></a><span data-ttu-id="b57f9-234">Creación de un rol personalizado</span><span class="sxs-lookup"><span data-stu-id="b57f9-234">Create a Custom Role</span></span>
<span data-ttu-id="b57f9-235">Cree un rol personalizado.</span><span class="sxs-lookup"><span data-stu-id="b57f9-235">Create a custom role.</span></span>

<span data-ttu-id="b57f9-236">Para crear un rol personalizado, debe tener acceso a la operación `Microsoft.Authorization/roleDefinitions/write` en todos sus `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="b57f9-236">To create a custom role, you must have access to `Microsoft.Authorization/roleDefinitions/write` operation on all the `AssignableScopes`.</span></span> <span data-ttu-id="b57f9-237">Entre los roles integrados, solo se concede acceso a esta operación a *Propietario* y *Administrador de acceso de usuario*.</span><span class="sxs-lookup"><span data-stu-id="b57f9-237">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="b57f9-238">Para obtener más información sobre las asignaciones de roles y la administración del acceso a los recursos de Azure, consulte [Control de acceso basado en roles de Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b57f9-238">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="b57f9-239">Solicitud</span><span class="sxs-lookup"><span data-stu-id="b57f9-239">Request</span></span>
<span data-ttu-id="b57f9-240">Use el método **PUT** con el URI siguiente:</span><span class="sxs-lookup"><span data-stu-id="b57f9-240">Use the **PUT** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="b57f9-241">Dentro del URI, realice las sustituciones siguientes para personalizar la solicitud:</span><span class="sxs-lookup"><span data-stu-id="b57f9-241">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="b57f9-242">Reemplace *{scope}* por el primer elemento *AssignableScope* del rol personalizado.</span><span class="sxs-lookup"><span data-stu-id="b57f9-242">Replace *{scope}* with the first *AssignableScope* of the custom role.</span></span> <span data-ttu-id="b57f9-243">En los ejemplos siguientes, se muestra cómo especificar el ámbito para los distintos niveles.</span><span class="sxs-lookup"><span data-stu-id="b57f9-243">The following examples show how to specify the scope for different levels.</span></span>

   * <span data-ttu-id="b57f9-244">Suscripción: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="b57f9-244">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="b57f9-245">Grupo de recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="b57f9-245">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="b57f9-246">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="b57f9-246">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="b57f9-247">Reemplace *{role-definition-id}* por un nuevo GUID, que se convierte en el GUID del nuevo rol personalizado.</span><span class="sxs-lookup"><span data-stu-id="b57f9-247">Replace *{role-definition-id}* with a new GUID, which becomes the GUID identifier of the new custom role.</span></span>
3. <span data-ttu-id="b57f9-248">Reemplace *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="b57f9-248">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="b57f9-249">Para el cuerpo de la solicitud, proporcione los valores en el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="b57f9-249">For the request body, provide the values in the following format:</span></span>

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

| <span data-ttu-id="b57f9-250">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="b57f9-250">Element Name</span></span> | <span data-ttu-id="b57f9-251">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="b57f9-251">Required</span></span> | <span data-ttu-id="b57f9-252">Tipo</span><span class="sxs-lookup"><span data-stu-id="b57f9-252">Type</span></span> | <span data-ttu-id="b57f9-253">Description</span><span class="sxs-lookup"><span data-stu-id="b57f9-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b57f9-254">name</span><span class="sxs-lookup"><span data-stu-id="b57f9-254">name</span></span> |<span data-ttu-id="b57f9-255">Sí</span><span class="sxs-lookup"><span data-stu-id="b57f9-255">Yes</span></span> |<span data-ttu-id="b57f9-256">String</span><span class="sxs-lookup"><span data-stu-id="b57f9-256">String</span></span> |<span data-ttu-id="b57f9-257">Identificador GUID del rol personalizado.</span><span class="sxs-lookup"><span data-stu-id="b57f9-257">GUID identifier of the custom role.</span></span> |
| <span data-ttu-id="b57f9-258">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="b57f9-258">properties.roleName</span></span> |<span data-ttu-id="b57f9-259">Sí</span><span class="sxs-lookup"><span data-stu-id="b57f9-259">Yes</span></span> |<span data-ttu-id="b57f9-260">String</span><span class="sxs-lookup"><span data-stu-id="b57f9-260">String</span></span> |<span data-ttu-id="b57f9-261">Nombre para mostrar del rol personalizado.</span><span class="sxs-lookup"><span data-stu-id="b57f9-261">Display name of the custom role.</span></span> <span data-ttu-id="b57f9-262">Tamaño máximo: 128 caracteres.</span><span class="sxs-lookup"><span data-stu-id="b57f9-262">Maximum size 128 characters.</span></span> |
| <span data-ttu-id="b57f9-263">properties.description</span><span class="sxs-lookup"><span data-stu-id="b57f9-263">properties.description</span></span> |<span data-ttu-id="b57f9-264">No</span><span class="sxs-lookup"><span data-stu-id="b57f9-264">No</span></span> |<span data-ttu-id="b57f9-265">String</span><span class="sxs-lookup"><span data-stu-id="b57f9-265">String</span></span> |<span data-ttu-id="b57f9-266">Descripción del rol personalizado.</span><span class="sxs-lookup"><span data-stu-id="b57f9-266">Description of the custom role.</span></span> <span data-ttu-id="b57f9-267">Tamaño máximo: 1024 caracteres.</span><span class="sxs-lookup"><span data-stu-id="b57f9-267">Maximum size 1024 characters.</span></span> |
| <span data-ttu-id="b57f9-268">properties.type</span><span class="sxs-lookup"><span data-stu-id="b57f9-268">properties.type</span></span> |<span data-ttu-id="b57f9-269">Sí</span><span class="sxs-lookup"><span data-stu-id="b57f9-269">Yes</span></span> |<span data-ttu-id="b57f9-270">String</span><span class="sxs-lookup"><span data-stu-id="b57f9-270">String</span></span> |<span data-ttu-id="b57f9-271">Establézcalo en "CustomRole".</span><span class="sxs-lookup"><span data-stu-id="b57f9-271">Set to "CustomRole."</span></span> |
| <span data-ttu-id="b57f9-272">properties.permissions.actions</span><span class="sxs-lookup"><span data-stu-id="b57f9-272">properties.permissions.actions</span></span> |<span data-ttu-id="b57f9-273">yes</span><span class="sxs-lookup"><span data-stu-id="b57f9-273">Yes</span></span> |<span data-ttu-id="b57f9-274">String[]</span><span class="sxs-lookup"><span data-stu-id="b57f9-274">String[]</span></span> |<span data-ttu-id="b57f9-275">Matriz de cadenas de acción que especifica las operaciones a las que el rol personalizado concede acceso.</span><span class="sxs-lookup"><span data-stu-id="b57f9-275">An array of action strings specifying the operations granted by the custom role.</span></span> |
| <span data-ttu-id="b57f9-276">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="b57f9-276">properties.permissions.notActions</span></span> |<span data-ttu-id="b57f9-277">No</span><span class="sxs-lookup"><span data-stu-id="b57f9-277">No</span></span> |<span data-ttu-id="b57f9-278">String[]</span><span class="sxs-lookup"><span data-stu-id="b57f9-278">String[]</span></span> |<span data-ttu-id="b57f9-279">Matriz de cadenas de acción que especifica las operaciones a las que el rol personalizado no concede acceso.</span><span class="sxs-lookup"><span data-stu-id="b57f9-279">An array of action strings specifying the operations to exclude from the operations granted by the custom role.</span></span> |
| <span data-ttu-id="b57f9-280">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="b57f9-280">properties.assignableScopes</span></span> |<span data-ttu-id="b57f9-281">yes</span><span class="sxs-lookup"><span data-stu-id="b57f9-281">Yes</span></span> |<span data-ttu-id="b57f9-282">String[]</span><span class="sxs-lookup"><span data-stu-id="b57f9-282">String[]</span></span> |<span data-ttu-id="b57f9-283">Matriz de ámbitos en los que se puede usar el rol personalizado.</span><span class="sxs-lookup"><span data-stu-id="b57f9-283">An array of scopes in which the custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="b57f9-284">Respuesta</span><span class="sxs-lookup"><span data-stu-id="b57f9-284">Response</span></span>
<span data-ttu-id="b57f9-285">Código de estado: 201</span><span class="sxs-lookup"><span data-stu-id="b57f9-285">Status code: 201</span></span>

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

## <a name="update-a-custom-role"></a><span data-ttu-id="b57f9-286">Actualización de un rol personalizado</span><span class="sxs-lookup"><span data-stu-id="b57f9-286">Update a Custom Role</span></span>
<span data-ttu-id="b57f9-287">Modifique un rol personalizado.</span><span class="sxs-lookup"><span data-stu-id="b57f9-287">Modify a custom role.</span></span>

<span data-ttu-id="b57f9-288">Para modificar un rol personalizado, debe tener acceso a la operación `Microsoft.Authorization/roleDefinitions/write` en todos sus `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="b57f9-288">To modify a custom role, you must have access to `Microsoft.Authorization/roleDefinitions/write` operation on all the `AssignableScopes`.</span></span> <span data-ttu-id="b57f9-289">Entre los roles integrados, solo se concede acceso a esta operación a *Propietario* y *Administrador de acceso de usuario*.</span><span class="sxs-lookup"><span data-stu-id="b57f9-289">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="b57f9-290">Para obtener más información sobre las asignaciones de roles y la administración del acceso a los recursos de Azure, consulte [Control de acceso basado en roles de Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b57f9-290">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="b57f9-291">Solicitud</span><span class="sxs-lookup"><span data-stu-id="b57f9-291">Request</span></span>
<span data-ttu-id="b57f9-292">Use el método **PUT** con el URI siguiente:</span><span class="sxs-lookup"><span data-stu-id="b57f9-292">Use the **PUT** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="b57f9-293">Dentro del URI, realice las sustituciones siguientes para personalizar la solicitud:</span><span class="sxs-lookup"><span data-stu-id="b57f9-293">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="b57f9-294">Reemplace *{scope}* por el primer elemento *AssignableScope* del rol personalizado.</span><span class="sxs-lookup"><span data-stu-id="b57f9-294">Replace *{scope}* with the first *AssignableScope* of the custom role.</span></span> <span data-ttu-id="b57f9-295">En los ejemplos siguientes, se muestra cómo especificar el ámbito para los distintos niveles:</span><span class="sxs-lookup"><span data-stu-id="b57f9-295">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="b57f9-296">Suscripción: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="b57f9-296">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="b57f9-297">Grupo de recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="b57f9-297">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="b57f9-298">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="b57f9-298">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="b57f9-299">Reemplace *{role-definition-id}* por el identificador GUID del rol personalizado.</span><span class="sxs-lookup"><span data-stu-id="b57f9-299">Replace *{role-definition-id}* with the GUID identifier of the custom role.</span></span>
3. <span data-ttu-id="b57f9-300">Reemplace *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="b57f9-300">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="b57f9-301">Para el cuerpo de la solicitud, proporcione los valores en el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="b57f9-301">For the request body, provide the values in the following format:</span></span>

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

| <span data-ttu-id="b57f9-302">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="b57f9-302">Element Name</span></span> | <span data-ttu-id="b57f9-303">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="b57f9-303">Required</span></span> | <span data-ttu-id="b57f9-304">Tipo</span><span class="sxs-lookup"><span data-stu-id="b57f9-304">Type</span></span> | <span data-ttu-id="b57f9-305">Description</span><span class="sxs-lookup"><span data-stu-id="b57f9-305">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b57f9-306">name</span><span class="sxs-lookup"><span data-stu-id="b57f9-306">name</span></span> |<span data-ttu-id="b57f9-307">Sí</span><span class="sxs-lookup"><span data-stu-id="b57f9-307">Yes</span></span> |<span data-ttu-id="b57f9-308">String</span><span class="sxs-lookup"><span data-stu-id="b57f9-308">String</span></span> |<span data-ttu-id="b57f9-309">Identificador GUID del rol personalizado.</span><span class="sxs-lookup"><span data-stu-id="b57f9-309">GUID identifier of the custom role.</span></span> |
| <span data-ttu-id="b57f9-310">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="b57f9-310">properties.roleName</span></span> |<span data-ttu-id="b57f9-311">Sí</span><span class="sxs-lookup"><span data-stu-id="b57f9-311">Yes</span></span> |<span data-ttu-id="b57f9-312">String</span><span class="sxs-lookup"><span data-stu-id="b57f9-312">String</span></span> |<span data-ttu-id="b57f9-313">Nombre para mostrar del rol personalizado actualizado.</span><span class="sxs-lookup"><span data-stu-id="b57f9-313">Display name of the updated custom role.</span></span> |
| <span data-ttu-id="b57f9-314">properties.description</span><span class="sxs-lookup"><span data-stu-id="b57f9-314">properties.description</span></span> |<span data-ttu-id="b57f9-315">No</span><span class="sxs-lookup"><span data-stu-id="b57f9-315">No</span></span> |<span data-ttu-id="b57f9-316">String</span><span class="sxs-lookup"><span data-stu-id="b57f9-316">String</span></span> |<span data-ttu-id="b57f9-317">Descripción del rol personalizado actualizado.</span><span class="sxs-lookup"><span data-stu-id="b57f9-317">Description of the updated custom role.</span></span> |
| <span data-ttu-id="b57f9-318">properties.type</span><span class="sxs-lookup"><span data-stu-id="b57f9-318">properties.type</span></span> |<span data-ttu-id="b57f9-319">Sí</span><span class="sxs-lookup"><span data-stu-id="b57f9-319">Yes</span></span> |<span data-ttu-id="b57f9-320">String</span><span class="sxs-lookup"><span data-stu-id="b57f9-320">String</span></span> |<span data-ttu-id="b57f9-321">Establézcalo en "CustomRole".</span><span class="sxs-lookup"><span data-stu-id="b57f9-321">Set to "CustomRole."</span></span> |
| <span data-ttu-id="b57f9-322">properties.permissions.actions</span><span class="sxs-lookup"><span data-stu-id="b57f9-322">properties.permissions.actions</span></span> |<span data-ttu-id="b57f9-323">yes</span><span class="sxs-lookup"><span data-stu-id="b57f9-323">Yes</span></span> |<span data-ttu-id="b57f9-324">String[]</span><span class="sxs-lookup"><span data-stu-id="b57f9-324">String[]</span></span> |<span data-ttu-id="b57f9-325">Matriz de cadenas de acción que especifica las operaciones a las que el rol personalizado actualizado concede acceso.</span><span class="sxs-lookup"><span data-stu-id="b57f9-325">An array of action strings specifying the operations to which the updated custom role grants access.</span></span> |
| <span data-ttu-id="b57f9-326">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="b57f9-326">properties.permissions.notActions</span></span> |<span data-ttu-id="b57f9-327">No</span><span class="sxs-lookup"><span data-stu-id="b57f9-327">No</span></span> |<span data-ttu-id="b57f9-328">String[]</span><span class="sxs-lookup"><span data-stu-id="b57f9-328">String[]</span></span> |<span data-ttu-id="b57f9-329">Matriz de cadenas de acción que especifica las operaciones a las que el rol personalizado actualizado no concede acceso.</span><span class="sxs-lookup"><span data-stu-id="b57f9-329">An array of action strings specifying the operations to exclude from the operations which the updated custom role grants.</span></span> |
| <span data-ttu-id="b57f9-330">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="b57f9-330">properties.assignableScopes</span></span> |<span data-ttu-id="b57f9-331">yes</span><span class="sxs-lookup"><span data-stu-id="b57f9-331">Yes</span></span> |<span data-ttu-id="b57f9-332">String[]</span><span class="sxs-lookup"><span data-stu-id="b57f9-332">String[]</span></span> |<span data-ttu-id="b57f9-333">Matriz de ámbitos en los que se puede usar el rol personalizado actualizado.</span><span class="sxs-lookup"><span data-stu-id="b57f9-333">An array of scopes in which the updated custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="b57f9-334">Respuesta</span><span class="sxs-lookup"><span data-stu-id="b57f9-334">Response</span></span>
<span data-ttu-id="b57f9-335">Código de estado: 201</span><span class="sxs-lookup"><span data-stu-id="b57f9-335">Status code: 201</span></span>

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

## <a name="delete-a-custom-role"></a><span data-ttu-id="b57f9-336">Eliminación de un rol personalizado</span><span class="sxs-lookup"><span data-stu-id="b57f9-336">Delete a Custom Role</span></span>
<span data-ttu-id="b57f9-337">Elimine un rol personalizado.</span><span class="sxs-lookup"><span data-stu-id="b57f9-337">Delete a custom role.</span></span>

<span data-ttu-id="b57f9-338">Para eliminar un rol personalizado, debe tener acceso a la operación `Microsoft.Authorization/roleDefinitions/delete` en todos sus `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="b57f9-338">To delete a custom role, you must have access to `Microsoft.Authorization/roleDefinitions/delete` operation on all the `AssignableScopes`.</span></span> <span data-ttu-id="b57f9-339">Entre los roles integrados, solo se concede acceso a esta operación a *Propietario* y *Administrador de acceso de usuario*.</span><span class="sxs-lookup"><span data-stu-id="b57f9-339">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="b57f9-340">Para obtener más información sobre las asignaciones de roles y la administración del acceso a los recursos de Azure, consulte [Control de acceso basado en roles de Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b57f9-340">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="b57f9-341">Solicitud</span><span class="sxs-lookup"><span data-stu-id="b57f9-341">Request</span></span>
<span data-ttu-id="b57f9-342">Use el método **DELETE** con el URI siguiente:</span><span class="sxs-lookup"><span data-stu-id="b57f9-342">Use the **DELETE** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="b57f9-343">Dentro del URI, realice las sustituciones siguientes para personalizar la solicitud:</span><span class="sxs-lookup"><span data-stu-id="b57f9-343">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="b57f9-344">Reemplace *{scope}* por el ámbito en el que quiere eliminar la definición de roles.</span><span class="sxs-lookup"><span data-stu-id="b57f9-344">Replace *{scope}* with the scope at which you wish to delete the role definition.</span></span> <span data-ttu-id="b57f9-345">En los ejemplos siguientes, se muestra cómo especificar el ámbito para los distintos niveles:</span><span class="sxs-lookup"><span data-stu-id="b57f9-345">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="b57f9-346">Suscripción: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="b57f9-346">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="b57f9-347">Grupo de recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="b57f9-347">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="b57f9-348">Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="b57f9-348">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="b57f9-349">Reemplace *{role-definition-id}* por el identificador GUID de definición de rol del rol personalizado.</span><span class="sxs-lookup"><span data-stu-id="b57f9-349">Replace *{role-definition-id}* with the GUID role definition id of the custom role.</span></span>
3. <span data-ttu-id="b57f9-350">Reemplace *{api-version}* por 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="b57f9-350">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="b57f9-351">Respuesta</span><span class="sxs-lookup"><span data-stu-id="b57f9-351">Response</span></span>
<span data-ttu-id="b57f9-352">Código de estado: 200</span><span class="sxs-lookup"><span data-stu-id="b57f9-352">Status code: 200</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b57f9-353">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b57f9-353">Next steps</span></span>

[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]
