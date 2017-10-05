---
title: "Protección de registros y zonas DNS | Microsoft Docs"
description: "Cómo proteger conjuntos de registros y zonas DNS en DNS de Microsoft Azure."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 190e69eb-e820-4fc8-8e9a-baaf0b3fb74a
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/20/2016
ms.author: jonatul
ms.openlocfilehash: 0b7040d6273b3a6b85cd55850d596807226b87fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-protect-dns-zones-and-records"></a><span data-ttu-id="4cf11-103">Cómo proteger registros y zonas DNS</span><span class="sxs-lookup"><span data-stu-id="4cf11-103">How to protect DNS zones and records</span></span>

<span data-ttu-id="4cf11-104">Los registros y las zonas DNS son recursos críticos.</span><span class="sxs-lookup"><span data-stu-id="4cf11-104">DNS zones and records are critical resources.</span></span> <span data-ttu-id="4cf11-105">Si se elimina una zona DNS o incluso tan solo un registro DNS puede provocar una interrupción total del servicio.</span><span class="sxs-lookup"><span data-stu-id="4cf11-105">Deleting a DNS zone or even just a single DNS record can result in a total service outage.</span></span>  <span data-ttu-id="4cf11-106">Por consiguiente, es importante proteger las zonas y los registros DNS críticos contra cambios accidentales o no autorizados.</span><span class="sxs-lookup"><span data-stu-id="4cf11-106">It is therefore important that critical DNS zones and records are protected against unauthorized or accidental changes.</span></span>

<span data-ttu-id="4cf11-107">En este artículo se explica cómo DNS de Azure le permite proteger sus zonas y registros DNS de dichos cambios.</span><span class="sxs-lookup"><span data-stu-id="4cf11-107">This article explains how Azure DNS enables you to protect your DNS zones and records against such changes.</span></span>  <span data-ttu-id="4cf11-108">Aplicamos dos eficaces características de seguridad que proporciona Azure Resource Manager: [control de acceso basado en rol](../active-directory/role-based-access-control-what-is.md) y [bloqueos de recursos](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="4cf11-108">We apply two powerful security features provided by Azure Resource Manager: [role-based access control](../active-directory/role-based-access-control-what-is.md) and [resource locks](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

## <a name="role-based-access-control"></a><span data-ttu-id="4cf11-109">Control de acceso basado en rol</span><span class="sxs-lookup"><span data-stu-id="4cf11-109">Role-based access control</span></span>

<span data-ttu-id="4cf11-110">El control de acceso basado en rol (RBAC) de Azure permite realizar una administración detallada del acceso de usuarios, grupos y recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="4cf11-110">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure users, groups, and resources.</span></span> <span data-ttu-id="4cf11-111">Con RBAC, puede conceder de forma precisa el grado de acceso que los usuarios necesiten para realizar sus trabajos.</span><span class="sxs-lookup"><span data-stu-id="4cf11-111">Using RBAC, you can grant precisely the amount of access that users need to perform their jobs.</span></span> <span data-ttu-id="4cf11-112">Para más información sobre cómo RBAC ayuda a administrar el acceso, vea [Introducción a la administración de acceso en Azure Portal](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="4cf11-112">For more information about how RBAC helps you manage access, see [What is Role-Based Access Control](../active-directory/role-based-access-control-what-is.md).</span></span>

### <a name="the-dns-zone-contributor-role"></a><span data-ttu-id="4cf11-113">Rol "DNS Zone Contributor" (Colaborador de zona DNS)</span><span class="sxs-lookup"><span data-stu-id="4cf11-113">The 'DNS Zone Contributor' role</span></span>

<span data-ttu-id="4cf11-114">Se trata de un rol integrado que ofrece Azure para administrar recursos DNS.</span><span class="sxs-lookup"><span data-stu-id="4cf11-114">The 'DNS Zone Contributor' role is a built-in role provided by Azure for managing DNS resources.</span></span>  <span data-ttu-id="4cf11-115">Al asignar permisos de colaborador de zona DNS a un usuario o grupo permite que ese grupo administre recursos DNS, pero no recursos de ningún otro tipo.</span><span class="sxs-lookup"><span data-stu-id="4cf11-115">Assigning DNS Zone Contributor permissions to a user or group enables that group to manage DNS resources, but not resources of any other type.</span></span>

<span data-ttu-id="4cf11-116">Por ejemplo, supongamos que el grupo de recursos "myzones" contiene cinco zonas de Contoso Corporation.</span><span class="sxs-lookup"><span data-stu-id="4cf11-116">For example, suppose the resource group 'myzones' contains five zones for Contoso Corporation.</span></span> <span data-ttu-id="4cf11-117">Cuando se conceden permisos "DNS Zone Contributor" (Colaborador de zona DNS) de administrador de DNS a ese grupo de recursos, se permite el control total sobre esas zonas DNS.</span><span class="sxs-lookup"><span data-stu-id="4cf11-117">Granting the DNS administrator 'DNS Zone Contributor' permissions to that resource group, enables full control over those DNS zones.</span></span> <span data-ttu-id="4cf11-118">También se evita la concesión de permisos innecesarios, por ejemplo el administrador de DNS no puede crear ni detener máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="4cf11-118">It also avoids granting unnecessary permissions, for example the DNS administrator cannot create or stop Virtual Machines.</span></span>

<span data-ttu-id="4cf11-119">La manera más sencilla de asignar permisos RBAC es [a través de Azure Portal](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="4cf11-119">The simplest way to assign RBAC permissions is [via the Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>  <span data-ttu-id="4cf11-120">Abra la hoja "Control de acceso (IAM)" del grupo de recursos, haga clic en "Agregar" y luego seleccione el rol "DNS Zone Contributor" (Colaborador de zona DNS) y los usuarios o grupos a los que necesita concederle permisos.</span><span class="sxs-lookup"><span data-stu-id="4cf11-120">Open the 'Access control (IAM)' blade for the resource group, then click 'Add', then select the 'DNS Zone Contributor' role and select the required users or groups to grant permissions.</span></span>

![RBAC de nivel de grupo de recursos a través de Azure Portal](./media/dns-protect-zones-recordsets/rbac1.png)

<span data-ttu-id="4cf11-122">Los permisos también se pueden [conceder mediante Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="4cf11-122">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions to all zones in a resource group
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="4cf11-123">El comando equivalente también está [disponible a través de la CLI de Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="4cf11-123">The equivalent command is also [available via the Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions to all zones in a resource group
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --resourceGroup "<resource group name>"
```

### <a name="zone-level-rbac"></a><span data-ttu-id="4cf11-124">RBAC de nivel de zona</span><span class="sxs-lookup"><span data-stu-id="4cf11-124">Zone level RBAC</span></span>

<span data-ttu-id="4cf11-125">Las reglas de RBAC de Azure pueden aplicarse a una suscripción, a un grupo de recursos o a un recurso individual.</span><span class="sxs-lookup"><span data-stu-id="4cf11-125">Azure RBAC rules can be applied to a subscription, a resource group or to an individual resource.</span></span> <span data-ttu-id="4cf11-126">En el caso de DNS de Azure, ese recurso puede ser una zona DNS individual o incluso un conjunto de registros individual.</span><span class="sxs-lookup"><span data-stu-id="4cf11-126">In the case of Azure DNS, that resource can be an individual DNS zone, or even an individual record set.</span></span>

<span data-ttu-id="4cf11-127">Por ejemplo, supongamos que el grupo de recursos "myzones" contiene la zona "contoso.com" y una subzona "customers.contoso.com" en la que se crean registros CNAME para cada cuenta de cliente.</span><span class="sxs-lookup"><span data-stu-id="4cf11-127">For example, suppose the resource group 'myzones' contains the zone 'contoso.com' and a subzone 'customers.contoso.com' in which CNAME records are created for each customer account.</span></span>  <span data-ttu-id="4cf11-128">La cuenta que se use para administrar estos registros CNAME solo debe tener permisos para crear registros en la zona "customers.contoso.com", no debe tener acceso a otras zonas.</span><span class="sxs-lookup"><span data-stu-id="4cf11-128">The account used to manage these CNAME records should be assigned permissions to create records in the 'customers.contoso.com' zone only, it should not have access to the other zones.</span></span>

<span data-ttu-id="4cf11-129">Los permisos RBAC de nivel de zona se pueden conceder a través de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="4cf11-129">Zone-level RBAC permissions can be granted via the Azure portal.</span></span>  <span data-ttu-id="4cf11-130">Abra la hoja "Control de acceso (IAM)" de la zona, haga clic en "Agregar" y luego seleccione el rol "DNS Zone Contributor" (Colaborador de zona DNS) y los usuarios o grupos a los que necesita concederle permisos.</span><span class="sxs-lookup"><span data-stu-id="4cf11-130">Open the 'Access control (IAM)' blade for the zone, then click 'Add', then select the 'DNS Zone Contributor' role and select the required users or groups to grant permissions.</span></span>

![RBAC de nivel de zona DNS a través de Azure Portal](./media/dns-protect-zones-recordsets/rbac2.png)

<span data-ttu-id="4cf11-132">Los permisos también se pueden [conceder mediante Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="4cf11-132">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions to a specific zone
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>" -ResourceName "<zone name>" -ResourceType Microsoft.Network/DNSZones
```

<span data-ttu-id="4cf11-133">El comando equivalente también está [disponible a través de la CLI de Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="4cf11-133">The equivalent command is also [available via the Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions to a specific zone
azure role assignment create --signInName <user email address> --roleName "DNS Zone Contributor" --resource-name <zone name> --resource-type Microsoft.Network/DNSZones --resource-group <resource group name>
```

### <a name="record-set-level-rbac"></a><span data-ttu-id="4cf11-134">RBAC de nivel de conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="4cf11-134">Record set level RBAC</span></span>

<span data-ttu-id="4cf11-135">Podemos ir más lejos.</span><span class="sxs-lookup"><span data-stu-id="4cf11-135">We can go one step further.</span></span> <span data-ttu-id="4cf11-136">Tenga en cuenta que el administrador de correo de Contoso Corporation debe tener acceso a los registros MX y TXT que se encuentran en la cúspide de la zona "contoso.com".</span><span class="sxs-lookup"><span data-stu-id="4cf11-136">Consider the mail administrator for Contoso Corporation, who needs access to the MX and TXT records at the apex of the 'contoso.com' zone.</span></span>  <span data-ttu-id="4cf11-137">No necesita acceder a ningún otro registro MX ni TXT ni a registros de ningún otro tipo.</span><span class="sxs-lookup"><span data-stu-id="4cf11-137">She doesn't need access to any other MX or TXT records, or to any records of any other type.</span></span>  <span data-ttu-id="4cf11-138">DNS de Azure le permite asignar permisos en el nivel de conjunto de registros exactamente a los registros que el administrador de correo tenga que acceder.</span><span class="sxs-lookup"><span data-stu-id="4cf11-138">Azure DNS allows you to assign permissions at the record set level, to precisely the records that the mail administrator needs access to.</span></span>  <span data-ttu-id="4cf11-139">Al administrador de correo se le concede exactamente el control que necesita, no puede realizar otros cambios.</span><span class="sxs-lookup"><span data-stu-id="4cf11-139">The mail administrator is granted precisely the control she needs, and is unable to make any other changes.</span></span>

<span data-ttu-id="4cf11-140">Los permisos RBAC de nivel de conjunto de registros pueden configurarse a través de Azure Portal, mediante el botón "Usuarios" de la hoja del conjunto de registros:</span><span class="sxs-lookup"><span data-stu-id="4cf11-140">Record-set level RBAC permissions can be configured via the Azure portal, using the 'Users' button in the record set blade:</span></span>

![RBAC de nivel de conjunto de registros a través de Azure Portal](./media/dns-protect-zones-recordsets/rbac3.png)

<span data-ttu-id="4cf11-142">Los permisos RBAC de nivel de conjunto de registros también se pueden [conceder mediante Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="4cf11-142">Record-set level RBAC permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant permissions to a specific record set
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -Scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

<span data-ttu-id="4cf11-143">El comando equivalente también está [disponible a través de la CLI de Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="4cf11-143">The equivalent command is also [available via the Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant permissions to a specific record set
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

### <a name="custom-roles"></a><span data-ttu-id="4cf11-144">Roles personalizados</span><span class="sxs-lookup"><span data-stu-id="4cf11-144">Custom roles</span></span>

<span data-ttu-id="4cf11-145">El rol "DNS Zone Contributor" (Colaborador de zona DNS) integrado permite el control total sobre un recurso DNS.</span><span class="sxs-lookup"><span data-stu-id="4cf11-145">The built-in 'DNS Zone Contributor' role enables full control over a DNS resource.</span></span> <span data-ttu-id="4cf11-146">También es posible crear roles de Azure de cliente propios, para proporcionar un control incluso más detallado.</span><span class="sxs-lookup"><span data-stu-id="4cf11-146">It is also possible to build your own customer Azure roles, to provide even finer-grained control.</span></span>

<span data-ttu-id="4cf11-147">Retomemos el ejemplo en el que se crea un registro CNAME en la zona "customers.contoso.com" para cada cuenta de cliente de Contoso Corporation.</span><span class="sxs-lookup"><span data-stu-id="4cf11-147">Consider again the example in which a CNAME record in the zone 'customers.contoso.com' is created for each Contoso Corporation customer account.</span></span>  <span data-ttu-id="4cf11-148">La cuenta que se use para administrar estos registros CNAME solo debe tener permiso para administrar registros CNAME.</span><span class="sxs-lookup"><span data-stu-id="4cf11-148">The account used to manage these CNAMEs should be granted permission to manage CNAME records only.</span></span>  <span data-ttu-id="4cf11-149">Es pues imposible modificar registros de otros tipos (como cambiar registros MX) o realizar operaciones de nivel de zona, como la eliminación de zonas.</span><span class="sxs-lookup"><span data-stu-id="4cf11-149">It is then unable to modify records of other types (such as changing MX records) or perform zone-level operations such as zone delete.</span></span>

<span data-ttu-id="4cf11-150">En el ejemplo siguiente se muestra una definición de rol personalizado para administrar únicamente registros CNAME:</span><span class="sxs-lookup"><span data-stu-id="4cf11-150">The following example shows a custom role definition for managing CNAME records only:</span></span>

```json
{
    "Name": "DNS CNAME Contributor",
    "Id": "",
    "IsCustom": true,
    "Description": "Can manage DNS CNAME records only.",
    "Actions": [
        "Microsoft.Network/dnsZones/CNAME/*",
        "Microsoft.Network/dnsZones/read",
        "Microsoft.Authorization/*/read",
        "Microsoft.Insights/alertRules/*",
        "Microsoft.ResourceHealth/availabilityStatuses/read",
        "Microsoft.Resources/deployments/*",
        "Microsoft.Resources/subscriptions/resourceGroups/read",
        "Microsoft.Support/*"
    ],
    "NotActions": [
    ],
    "AssignableScopes": [
        "/subscriptions/ c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
}
```

<span data-ttu-id="4cf11-151">La propiedad Actions define los siguientes permisos específicos de DNS:</span><span class="sxs-lookup"><span data-stu-id="4cf11-151">The Actions property defines the following DNS-specific permissions:</span></span>

* <span data-ttu-id="4cf11-152">`Microsoft.Network/dnsZones/CNAME/*` concede control total sobre registros CNAME</span><span class="sxs-lookup"><span data-stu-id="4cf11-152">`Microsoft.Network/dnsZones/CNAME/*` grants full control over CNAME records</span></span>
* <span data-ttu-id="4cf11-153">`Microsoft.Network/dnsZones/read` concede permiso para leer zonas DNS, pero no para modificarlas, lo que permite ver la zona en la que se crea el registro CNAME.</span><span class="sxs-lookup"><span data-stu-id="4cf11-153">`Microsoft.Network/dnsZones/read` grants permission to read DNS zones, but not to modify them, enabling you to see the zone in which the CNAME is being created.</span></span>

<span data-ttu-id="4cf11-154">Las acciones restantes se copian desde el [Rol de colaborador de zona DNS integrado](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span><span class="sxs-lookup"><span data-stu-id="4cf11-154">The remaining Actions are copied from the [DNS Zone Contributor built-in role](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span></span>

> [!NOTE]
> <span data-ttu-id="4cf11-155">El uso de un rol RBAC personalizado para evitar que se eliminen conjuntos de registros mientras se permite modificarlos no es un control eficaz.</span><span class="sxs-lookup"><span data-stu-id="4cf11-155">Using a custom RBAC role to prevent deleting record sets while still allowing them to be updated is not an effective control.</span></span> <span data-ttu-id="4cf11-156">Evita que los conjuntos de registros se eliminen, pero no que se modifiquen.</span><span class="sxs-lookup"><span data-stu-id="4cf11-156">It prevents record sets from being deleted, but it does not prevent them from being modified.</span></span>  <span data-ttu-id="4cf11-157">Entre las modificaciones permitidas figuran la adición y eliminación de registros desde el conjunto de registros, incluida la eliminación de todos los registros para dejar un conjunto de registros "empty".</span><span class="sxs-lookup"><span data-stu-id="4cf11-157">Permitted modifications include adding and removing records from the record set, including removing all records to leave an 'empty' record set.</span></span> <span data-ttu-id="4cf11-158">Esto tiene el mismo efecto que eliminar el conjunto de registros desde un punto de vista de la resolución DNS.</span><span class="sxs-lookup"><span data-stu-id="4cf11-158">This has the same effect as deleting the record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="4cf11-159">Actualmente no pueden realizarse definiciones de roles personalizados a través de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="4cf11-159">Custom role definitions cannot currently be defined via the Azure portal.</span></span> <span data-ttu-id="4cf11-160">Puede crearse un rol personalizado basado en esta definición de rol mediante Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4cf11-160">A custom role based on this role definition can be created using Azure PowerShell:</span></span>

```powershell
# Create new role definition based on input file
New-AzureRmRoleDefinition -InputFile <file path>
```

<span data-ttu-id="4cf11-161">También puede crearse a través de la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="4cf11-161">It can also be created via the Azure CLI:</span></span>

```azurecli
# Create new role definition based on input file
azure role create -inputfile <file path>
```

<span data-ttu-id="4cf11-162">El rol se puede asignar después del mismo modo que los roles integrados, tal cual se describe anteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="4cf11-162">The role can then be assigned in the same way as built-in roles, as described earlier in this article.</span></span>

<span data-ttu-id="4cf11-163">Para obtener más información sobre cómo crear, administrar y asignar roles personalizados, vea [Roles personalizados en RBAC de Azure](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="4cf11-163">For more information on how to create, manage, and assign custom roles, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="resource-locks"></a><span data-ttu-id="4cf11-164">Bloqueos de recursos</span><span class="sxs-lookup"><span data-stu-id="4cf11-164">Resource locks</span></span>

<span data-ttu-id="4cf11-165">Además de RBAC, Azure Resource Manager admite otro tipo de control de seguridad, concretamente, la posibilidad de "bloquear" recursos.</span><span class="sxs-lookup"><span data-stu-id="4cf11-165">In addition to RBAC, Azure Resource Manager supports another type of security control, namely the ability to 'lock' resources.</span></span> <span data-ttu-id="4cf11-166">Mientras que las reglas de RBAC permiten controlar las acciones de usuarios y grupos específicos, los bloqueos de recursos se aplican a los recursos y son eficaces en todos los usuarios y roles.</span><span class="sxs-lookup"><span data-stu-id="4cf11-166">Where RBAC rules allow you to control the actions of specific users and groups, resource locks are applied to the resource, and are effective across all users and roles.</span></span> <span data-ttu-id="4cf11-167">Para obtener más información, consulte [Bloqueo de recursos con el Administrador de recursos de Azure](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="4cf11-167">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

<span data-ttu-id="4cf11-168">Hay dos tipos de bloqueo de recurso: **DoNotDelete** y **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="4cf11-168">There are two types of resource lock: **DoNotDelete** and **ReadOnly**.</span></span> <span data-ttu-id="4cf11-169">Pueden aplicarse a una zona DNS o a un conjunto de registros individual.</span><span class="sxs-lookup"><span data-stu-id="4cf11-169">These can be applied either to a DNS zone, or to an individual record set.</span></span>  <span data-ttu-id="4cf11-170">En las secciones siguientes se describen varios escenarios comunes y cómo mantenerlos con bloqueos de recursos.</span><span class="sxs-lookup"><span data-stu-id="4cf11-170">The following sections describe several common scenarios, and how to support them using resource locks.</span></span>

### <a name="protecting-against-all-changes"></a><span data-ttu-id="4cf11-171">Protección contra todos los cambios</span><span class="sxs-lookup"><span data-stu-id="4cf11-171">Protecting against all changes</span></span>

<span data-ttu-id="4cf11-172">Para evitar que se realicen cambios, aplique un bloqueo ReadOnly a la zona.</span><span class="sxs-lookup"><span data-stu-id="4cf11-172">To prevent any changes being made, apply a ReadOnly lock to the zone.</span></span>  <span data-ttu-id="4cf11-173">Esto impide que se creen otros conjuntos de registros y que se modifiquen o eliminen conjuntos de registros existentes.</span><span class="sxs-lookup"><span data-stu-id="4cf11-173">This prevents new record sets from being created, and existing record sets from being modified or deleted.</span></span>

<span data-ttu-id="4cf11-174">Pueden crearse bloqueos de recursos de nivel de zona a través de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="4cf11-174">Zone level resource locks can be created via the Azure portal.</span></span>  <span data-ttu-id="4cf11-175">En la hoja de zona DNS, haga clic en "Bloqueos" y luego en "Agregar":</span><span class="sxs-lookup"><span data-stu-id="4cf11-175">From the DNS zone blade, click 'Locks', then 'Add':</span></span>

![Bloqueos de recursos de nivel de zona a través de Azure Portal](./media/dns-protect-zones-recordsets/locks1.png)

<span data-ttu-id="4cf11-177">También pueden crearse bloqueos de recursos de nivel de zona a través de Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4cf11-177">Zone-level resource locks can also be created via Azure PowerShell:</span></span>

```powershell
# Lock a DNS zone
New-AzureRmResourceLock -LockLevel <lock level> -LockName <lock name> -ResourceName <zone name> -ResourceType Microsoft.Network/DNSZones -ResourceGroupName <resource group name>
```

<span data-ttu-id="4cf11-178">Actualmente no se admite la configuración de bloqueos de recursos de Azure a través de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="4cf11-178">Configuring Azure resource locks is not currently supported via the Azure CLI.</span></span>

### <a name="protecting-individual-records"></a><span data-ttu-id="4cf11-179">Protección de registros individuales</span><span class="sxs-lookup"><span data-stu-id="4cf11-179">Protecting individual records</span></span>

<span data-ttu-id="4cf11-180">Para evitar que se modifique un conjunto de registros de DNS existente, aplique un bloqueo ReadOnly al conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="4cf11-180">To prevent an existing DNS record set against modification, apply a ReadOnly lock to the record set.</span></span>

> [!NOTE]
> <span data-ttu-id="4cf11-181">La aplicación de un bloqueo DoNotDelete a un conjunto de registros no es un control eficaz.</span><span class="sxs-lookup"><span data-stu-id="4cf11-181">Applying a DoNotDelete lock to a record set is not an effective control.</span></span> <span data-ttu-id="4cf11-182">Evita que el conjunto de registros se elimine, pero no que se modifique.</span><span class="sxs-lookup"><span data-stu-id="4cf11-182">It prevents the record set from being deleted, but it does not prevent it from being modified.</span></span>  <span data-ttu-id="4cf11-183">Entre las modificaciones permitidas figuran la adición y eliminación de registros desde el conjunto de registros, incluida la eliminación de todos los registros para dejar un conjunto de registros "empty".</span><span class="sxs-lookup"><span data-stu-id="4cf11-183">Permitted modifications include adding and removing records from the record set, including removing all records to leave an 'empty' record set.</span></span> <span data-ttu-id="4cf11-184">Esto tiene el mismo efecto que eliminar el conjunto de registros desde un punto de vista de la resolución DNS.</span><span class="sxs-lookup"><span data-stu-id="4cf11-184">This has the same effect as deleting the record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="4cf11-185">Actualmente, los bloqueos de recursos de nivel de conjunto de recursos solo pueden configurarse mediante Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4cf11-185">Record set level resource locks can currently only be configured using Azure PowerShell.</span></span>  <span data-ttu-id="4cf11-186">No se admiten en Azure Portal ni en la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="4cf11-186">They are not supported in the Azure portal or Azure CLI.</span></span>

```powershell
# Lock a DNS record set
New-AzureRmResourceLock -LockLevel <lock level> -LockName "<lock name>" -ResourceName "<zone name>/<record set name>" -ResourceType "Microsoft.Network/DNSZones/<record type>" -ResourceGroupName "<resource group name>"
```

### <a name="protecting-against-zone-deletion"></a><span data-ttu-id="4cf11-187">Protección contra la eliminación de zonas</span><span class="sxs-lookup"><span data-stu-id="4cf11-187">Protecting against zone deletion</span></span>

<span data-ttu-id="4cf11-188">Cuando se elimina una zona en DNS de Azure, se eliminan también todos los conjuntos de registros de la zona.</span><span class="sxs-lookup"><span data-stu-id="4cf11-188">When a zone is deleted in Azure DNS, all record sets in the zone are also deleted.</span></span>  <span data-ttu-id="4cf11-189">Esta operación no se puede deshacer.</span><span class="sxs-lookup"><span data-stu-id="4cf11-189">This operation cannot be undone.</span></span>  <span data-ttu-id="4cf11-190">La eliminación accidental de una zona crítica tiene la posibilidad de tener un significativo impacto de negocio.</span><span class="sxs-lookup"><span data-stu-id="4cf11-190">Accidentally deleting a critical zone has the potential to have a significant business impact.</span></span>  <span data-ttu-id="4cf11-191">Por consiguiente, es muy importante que se proteja contra la eliminación accidental de zonas.</span><span class="sxs-lookup"><span data-stu-id="4cf11-191">It is therefore very important to protect against accidental zone deletion.</span></span>

<span data-ttu-id="4cf11-192">La aplicación de un bloqueo DoNotDelete a una zona impide que se elimine la zona.</span><span class="sxs-lookup"><span data-stu-id="4cf11-192">Applying a DoNotDelete lock to a zone prevents the zone from being deleted.</span></span>  <span data-ttu-id="4cf11-193">Pero, como los recursos secundarios heredan los bloqueos, también impide que se eliminen los conjuntos de registros de la zona, lo que puede no ser deseable.</span><span class="sxs-lookup"><span data-stu-id="4cf11-193">However, since locks are inherited by child resources, it also prevents any record sets in the zone from being deleted, which may be undesirable.</span></span>  <span data-ttu-id="4cf11-194">Además, tal como se describe en la nota anterior, tampoco resulta eficaz puesto que todavía se pueden quitar registros de los conjuntos de registros existentes.</span><span class="sxs-lookup"><span data-stu-id="4cf11-194">Furthermore, as described in the note above, it is also ineffective since records can still be removed from the existing record sets.</span></span>

<span data-ttu-id="4cf11-195">Como alternativa, considere la posibilidad de aplicar un bloqueo DoNotDelete a un conjunto de registros de la zona, como el conjunto de registros SOA.</span><span class="sxs-lookup"><span data-stu-id="4cf11-195">As an alternative, consider applying a DoNotDelete lock to a record set in the zone, such as the SOA record set.</span></span>  <span data-ttu-id="4cf11-196">Puesto que la zona no se puede eliminar sin eliminar también los conjuntos de registros, esto protege contra la eliminación de la zona, mientras sigue permitiendo que se modifiquen libremente los conjuntos de registros contenidos en la zona.</span><span class="sxs-lookup"><span data-stu-id="4cf11-196">Since the zone cannot be deleted without also deleting the record sets, this protects against zone deletion, while still allowing record sets within the zone to be modified freely.</span></span> <span data-ttu-id="4cf11-197">Si intenta eliminar la zona, Azure Resource Manager detecta que esto también eliminaría el conjunto de registros SOA y bloquea la llamada porque la SOA está bloqueada.</span><span class="sxs-lookup"><span data-stu-id="4cf11-197">If an attempt is made to delete the zone, Azure Resource Manager detects this would also delete the SOA record set, and blocks the call because the SOA is locked.</span></span>  <span data-ttu-id="4cf11-198">No se elimina ningún conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="4cf11-198">No record sets are deleted.</span></span>

<span data-ttu-id="4cf11-199">El comando de PowerShell siguiente crea un bloqueo DoNotDelete contra el registro SOA de la zona especificada:</span><span class="sxs-lookup"><span data-stu-id="4cf11-199">The following PowerShell command creates a DoNotDelete lock against the SOA record of the given zone:</span></span>

```powershell
# Protect against zone delete with DoNotDelete lock on the record set
New-AzureRmResourceLock -LockLevel DoNotDelete -LockName "<lock name>" -ResourceName "<zone name>/@" -ResourceType" Microsoft.Network/DNSZones/SOA" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="4cf11-200">Otra manera de evitar la eliminación accidental de zonas consiste en usar un rol personalizado para asegurarse de que las cuentas de operador y de servicio que se utilizan para administrar las zonas no dispongan de permisos de eliminación de zonas.</span><span class="sxs-lookup"><span data-stu-id="4cf11-200">Another way to prevent accidental zone deletion is by using a custom role to ensure the operator and service accounts used to manage your zones do not have zone delete permissions.</span></span> <span data-ttu-id="4cf11-201">Cuando tenga que eliminar una zona, puede aplicar una eliminación en dos pasos; de esta forma, se conceden permisos primero para eliminar la zona (en el ámbito de la zona, para evitar la eliminación de una zona incorrecta) y, a continuación, se elimina la zona.</span><span class="sxs-lookup"><span data-stu-id="4cf11-201">When you do need to delete a zone, you can enforce a two-step delete, first granting zone delete permissions (at the zone scope, to prevent deleting the wrong zone) and second to delete the zone.</span></span>

<span data-ttu-id="4cf11-202">Este segundo método tiene la ventaja de que funciona para todas las zonas a las que acceden esas cuentas y no obliga a acordarse de crear bloqueos.</span><span class="sxs-lookup"><span data-stu-id="4cf11-202">This second approach has the advantage that it works for all zones accessed by those accounts, without having to remember to create any locks.</span></span> <span data-ttu-id="4cf11-203">Tiene el inconveniente de que las cuentas con permisos de eliminación de zona, como la del propietario de la suscripción, pueden eliminar por error una zona crítica.</span><span class="sxs-lookup"><span data-stu-id="4cf11-203">It has the disadvantage that any accounts with zone delete permissions, such as the subscription owner, can still accidentally delete a critical zone.</span></span>

<span data-ttu-id="4cf11-204">Es posible utilizar ambos enfoques (el bloqueo de recursos y los roles personalizados) al mismo tiempo, para abordar en profundidad la protección de zonas DNS.</span><span class="sxs-lookup"><span data-stu-id="4cf11-204">It is possible to use both approaches - resource locks and custom roles - at the same time, as a defense-in-depth approach to DNS zone protection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4cf11-205">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4cf11-205">Next steps</span></span>

* <span data-ttu-id="4cf11-206">Para más información sobre cómo trabajar con RBAC, vea [Introducción a la administración de acceso en Azure Portal](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="4cf11-206">For more information about working with RBAC, see [Get started with access management in the Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>
* <span data-ttu-id="4cf11-207">Para más información sobre cómo trabajar con bloqueos de recursos, vea [Bloqueo de recursos con Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="4cf11-207">For more information about working with resource locks, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

