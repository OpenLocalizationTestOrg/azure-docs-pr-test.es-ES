---
title: aaaProtecting zonas y registros DNS | Documentos de Microsoft
description: "¿Cómo tooprotect zonas DNS y un registro se establece en DNS de Microsoft Azure."
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
ms.openlocfilehash: 7945f6240feeed3d79a11d340f9f845e083026ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprotect-dns-zones-and-records"></a><span data-ttu-id="d4075-103">¿Cómo tooprotect DNS zonas y registros</span><span class="sxs-lookup"><span data-stu-id="d4075-103">How tooprotect DNS zones and records</span></span>

<span data-ttu-id="d4075-104">Los registros y las zonas DNS son recursos críticos.</span><span class="sxs-lookup"><span data-stu-id="d4075-104">DNS zones and records are critical resources.</span></span> <span data-ttu-id="d4075-105">Si se elimina una zona DNS o incluso tan solo un registro DNS puede provocar una interrupción total del servicio.</span><span class="sxs-lookup"><span data-stu-id="d4075-105">Deleting a DNS zone or even just a single DNS record can result in a total service outage.</span></span>  <span data-ttu-id="d4075-106">Por consiguiente, es importante proteger las zonas y los registros DNS críticos contra cambios accidentales o no autorizados.</span><span class="sxs-lookup"><span data-stu-id="d4075-106">It is therefore important that critical DNS zones and records are protected against unauthorized or accidental changes.</span></span>

<span data-ttu-id="d4075-107">Este artículo explica cómo DNS de Azure permite tooprotect sus zonas y registros DNS con dichos cambios.</span><span class="sxs-lookup"><span data-stu-id="d4075-107">This article explains how Azure DNS enables you tooprotect your DNS zones and records against such changes.</span></span>  <span data-ttu-id="d4075-108">Aplicamos dos eficaces características de seguridad que proporciona Azure Resource Manager: [control de acceso basado en rol](../active-directory/role-based-access-control-what-is.md) y [bloqueos de recursos](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="d4075-108">We apply two powerful security features provided by Azure Resource Manager: [role-based access control](../active-directory/role-based-access-control-what-is.md) and [resource locks](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

## <a name="role-based-access-control"></a><span data-ttu-id="d4075-109">Control de acceso basado en rol</span><span class="sxs-lookup"><span data-stu-id="d4075-109">Role-based access control</span></span>

<span data-ttu-id="d4075-110">El control de acceso basado en rol (RBAC) de Azure permite realizar una administración detallada del acceso de usuarios, grupos y recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="d4075-110">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure users, groups, and resources.</span></span> <span data-ttu-id="d4075-111">Usar RBAC, puede conceder con precisión el importe de Hola de acceso que los usuarios necesitan tooperform sus trabajos.</span><span class="sxs-lookup"><span data-stu-id="d4075-111">Using RBAC, you can grant precisely hello amount of access that users need tooperform their jobs.</span></span> <span data-ttu-id="d4075-112">Para más información sobre cómo RBAC ayuda a administrar el acceso, vea [Introducción a la administración de acceso en Azure Portal](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="d4075-112">For more information about how RBAC helps you manage access, see [What is Role-Based Access Control](../active-directory/role-based-access-control-what-is.md).</span></span>

### <a name="hello-dns-zone-contributor-role"></a><span data-ttu-id="d4075-113">rol de Hello 'Colaborador de zona DNS'</span><span class="sxs-lookup"><span data-stu-id="d4075-113">hello 'DNS Zone Contributor' role</span></span>

<span data-ttu-id="d4075-114">rol de Hello 'Colaborador de zona DNS' es un rol integrado proporcionado por Azure para administrar recursos DNS.</span><span class="sxs-lookup"><span data-stu-id="d4075-114">hello 'DNS Zone Contributor' role is a built-in role provided by Azure for managing DNS resources.</span></span>  <span data-ttu-id="d4075-115">Asignación de grupo o usuario de tooa de permisos de colaborador de la zona de DNS permite que agrupar toomanage los recursos DNS, pero no los recursos de cualquier otro tipo.</span><span class="sxs-lookup"><span data-stu-id="d4075-115">Assigning DNS Zone Contributor permissions tooa user or group enables that group toomanage DNS resources, but not resources of any other type.</span></span>

<span data-ttu-id="d4075-116">Por ejemplo, suponga que el grupo de recursos de hello 'myzones' contiene cinco zonas para Contoso Corporation.</span><span class="sxs-lookup"><span data-stu-id="d4075-116">For example, suppose hello resource group 'myzones' contains five zones for Contoso Corporation.</span></span> <span data-ttu-id="d4075-117">La concesión Hola DNS administrador 'Colaborador de zona DNS' permisos toothat grupo de recursos, permite control total sobre las zonas DNS.</span><span class="sxs-lookup"><span data-stu-id="d4075-117">Granting hello DNS administrator 'DNS Zone Contributor' permissions toothat resource group, enables full control over those DNS zones.</span></span> <span data-ttu-id="d4075-118">También evita conceder permisos innecesarios, por ejemplo el administrador DNS hello no puede crear ni detener máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="d4075-118">It also avoids granting unnecessary permissions, for example hello DNS administrator cannot create or stop Virtual Machines.</span></span>

<span data-ttu-id="d4075-119">permisos de RBAC de manera más sencillos de Hello tooassign es [a través del portal de Azure hello](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="d4075-119">hello simplest way tooassign RBAC permissions is [via hello Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>  <span data-ttu-id="d4075-120">Abra hoja hello 'control de acceso (de índices IAM)' para el grupo de recursos de hello, a continuación, haga clic en 'Agregar' y seleccione el rol de hello 'Colaborador de zona DNS' y usuarios de hello seleccione necesario o grupos toogrant permisos.</span><span class="sxs-lookup"><span data-stu-id="d4075-120">Open hello 'Access control (IAM)' blade for hello resource group, then click 'Add', then select hello 'DNS Zone Contributor' role and select hello required users or groups toogrant permissions.</span></span>

![Nivel de grupo de recursos RBAC a través de hello portal de Azure](./media/dns-protect-zones-recordsets/rbac1.png)

<span data-ttu-id="d4075-122">Los permisos también se pueden [conceder mediante Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="d4075-122">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="d4075-123">También es el comando equivalente de Hello [disponibles a través de hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="d4075-123">hello equivalent command is also [available via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --resourceGroup "<resource group name>"
```

### <a name="zone-level-rbac"></a><span data-ttu-id="d4075-124">RBAC de nivel de zona</span><span class="sxs-lookup"><span data-stu-id="d4075-124">Zone level RBAC</span></span>

<span data-ttu-id="d4075-125">Las reglas de RBAC Azure pueden ser suscripción tooa aplicado, un recurso de individuales de tooan o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d4075-125">Azure RBAC rules can be applied tooa subscription, a resource group or tooan individual resource.</span></span> <span data-ttu-id="d4075-126">En caso de hello de DNS de Azure, ese recurso puede ser una zona DNS individual, o incluso un conjunto de registros individual.</span><span class="sxs-lookup"><span data-stu-id="d4075-126">In hello case of Azure DNS, that resource can be an individual DNS zone, or even an individual record set.</span></span>

<span data-ttu-id="d4075-127">Por ejemplo, suponga que el grupo de recursos de hello 'myzones' contiene una subzona 'customers.contoso.com' en el que se crean los registros CNAME para cada cuenta de cliente y zona hello 'contoso.com'.</span><span class="sxs-lookup"><span data-stu-id="d4075-127">For example, suppose hello resource group 'myzones' contains hello zone 'contoso.com' and a subzone 'customers.contoso.com' in which CNAME records are created for each customer account.</span></span>  <span data-ttu-id="d4075-128">Hola cuenta usada toomanage estos registros CNAME deben asignarse registros de toocreate de permisos de zona sólo de hello 'customers.contoso.com', no debería tener acceso toohello otras zonas.</span><span class="sxs-lookup"><span data-stu-id="d4075-128">hello account used toomanage these CNAME records should be assigned permissions toocreate records in hello 'customers.contoso.com' zone only, it should not have access toohello other zones.</span></span>

<span data-ttu-id="d4075-129">Se pueden conceder permisos de nivel de zona RBAC a través de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="d4075-129">Zone-level RBAC permissions can be granted via hello Azure portal.</span></span>  <span data-ttu-id="d4075-130">Abrir hello 'Control de acceso (de índices IAM)' hoja para zona de hello, a continuación, haga clic en 'Agregar', seleccione el rol de 'Colaborador de zona DNS' hello y usuarios de hello seleccione necesario o permisos de toogrant de grupos.</span><span class="sxs-lookup"><span data-stu-id="d4075-130">Open hello 'Access control (IAM)' blade for hello zone, then click 'Add', then select hello 'DNS Zone Contributor' role and select hello required users or groups toogrant permissions.</span></span>

![RBAC de nivel de zona DNS a través de hello portal de Azure](./media/dns-protect-zones-recordsets/rbac2.png)

<span data-ttu-id="d4075-132">Los permisos también se pueden [conceder mediante Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="d4075-132">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions tooa specific zone
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>" -ResourceName "<zone name>" -ResourceType Microsoft.Network/DNSZones
```

<span data-ttu-id="d4075-133">También es el comando equivalente de Hello [disponibles a través de hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="d4075-133">hello equivalent command is also [available via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions tooa specific zone
azure role assignment create --signInName <user email address> --roleName "DNS Zone Contributor" --resource-name <zone name> --resource-type Microsoft.Network/DNSZones --resource-group <resource group name>
```

### <a name="record-set-level-rbac"></a><span data-ttu-id="d4075-134">RBAC de nivel de conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="d4075-134">Record set level RBAC</span></span>

<span data-ttu-id="d4075-135">Podemos ir más lejos.</span><span class="sxs-lookup"><span data-stu-id="d4075-135">We can go one step further.</span></span> <span data-ttu-id="d4075-136">Considere la posibilidad de administrador de correo electrónico de Hola para Contoso Corporation, que necesita acceso toohello MX y registros TXT en vértice Hola de zona de 'contoso.com' hello.</span><span class="sxs-lookup"><span data-stu-id="d4075-136">Consider hello mail administrator for Contoso Corporation, who needs access toohello MX and TXT records at hello apex of hello 'contoso.com' zone.</span></span>  <span data-ttu-id="d4075-137">No necesita tener acceso a tooany otros registros MX o TXT o tooany registros de cualquier otro tipo.</span><span class="sxs-lookup"><span data-stu-id="d4075-137">She doesn't need access tooany other MX or TXT records, or tooany records of any other type.</span></span>  <span data-ttu-id="d4075-138">DNS de Azure permite que los permisos tooassign Hola conjunto de registros, tooprecisely Hola registros a nivel que Hola Administrador de correo electrónico necesita tener acceso a.</span><span class="sxs-lookup"><span data-stu-id="d4075-138">Azure DNS allows you tooassign permissions at hello record set level, tooprecisely hello records that hello mail administrator needs access to.</span></span>  <span data-ttu-id="d4075-139">Hello correo se concede al administrador controlar con precisión de hello ella necesita y es no se puede toomake cualquier otro cambio.</span><span class="sxs-lookup"><span data-stu-id="d4075-139">hello mail administrator is granted precisely hello control she needs, and is unable toomake any other changes.</span></span>

<span data-ttu-id="d4075-140">Permisos de RBAC de nivel de conjunto de registros se pueden configurar a través del portal de Azure, con el botón Hola 'usuarios' en la hoja de conjunto de registros de Hola Hola:</span><span class="sxs-lookup"><span data-stu-id="d4075-140">Record-set level RBAC permissions can be configured via hello Azure portal, using hello 'Users' button in hello record set blade:</span></span>

![Nivel de RBAC a través del portal de Azure Hola de conjunto de registros](./media/dns-protect-zones-recordsets/rbac3.png)

<span data-ttu-id="d4075-142">Los permisos RBAC de nivel de conjunto de registros también se pueden [conceder mediante Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="d4075-142">Record-set level RBAC permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant permissions tooa specific record set
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -Scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

<span data-ttu-id="d4075-143">También es el comando equivalente de Hello [disponibles a través de hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="d4075-143">hello equivalent command is also [available via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant permissions tooa specific record set
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

### <a name="custom-roles"></a><span data-ttu-id="d4075-144">Roles personalizados</span><span class="sxs-lookup"><span data-stu-id="d4075-144">Custom roles</span></span>

<span data-ttu-id="d4075-145">rol de Hello integrado 'Colaborador de zona DNS' permite un control total sobre un recurso DNS.</span><span class="sxs-lookup"><span data-stu-id="d4075-145">hello built-in 'DNS Zone Contributor' role enables full control over a DNS resource.</span></span> <span data-ttu-id="d4075-146">También es posible toobuild su propio cliente Azure roles, control de tooprovide incluso más precisa.</span><span class="sxs-lookup"><span data-stu-id="d4075-146">It is also possible toobuild your own customer Azure roles, tooprovide even finer-grained control.</span></span>

<span data-ttu-id="d4075-147">Considere la posibilidad de nuevo ejemplo hello en el que se crea un registro CNAME en la zona de hello 'customers.contoso.com' para cada cuenta de cliente de Contoso Corporation.</span><span class="sxs-lookup"><span data-stu-id="d4075-147">Consider again hello example in which a CNAME record in hello zone 'customers.contoso.com' is created for each Contoso Corporation customer account.</span></span>  <span data-ttu-id="d4075-148">Hola cuenta usada toomanage estos CNAME debe contar con permiso toomanage CNAME sólo los registros.</span><span class="sxs-lookup"><span data-stu-id="d4075-148">hello account used toomanage these CNAMEs should be granted permission toomanage CNAME records only.</span></span>  <span data-ttu-id="d4075-149">Es, a continuación, no se puede toomodify registros de otros tipos (por ejemplo, cambiar los registros MX) o realizar operaciones de nivel de zona como la eliminación de zona.</span><span class="sxs-lookup"><span data-stu-id="d4075-149">It is then unable toomodify records of other types (such as changing MX records) or perform zone-level operations such as zone delete.</span></span>

<span data-ttu-id="d4075-150">Hola de ejemplo siguiente muestra una definición de rol personalizada para administrar solo los registros CNAME:</span><span class="sxs-lookup"><span data-stu-id="d4075-150">hello following example shows a custom role definition for managing CNAME records only:</span></span>

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

<span data-ttu-id="d4075-151">Hola propiedad Actions define Hola los siguientes permisos específicas de DNS:</span><span class="sxs-lookup"><span data-stu-id="d4075-151">hello Actions property defines hello following DNS-specific permissions:</span></span>

* <span data-ttu-id="d4075-152">`Microsoft.Network/dnsZones/CNAME/*` concede control total sobre registros CNAME</span><span class="sxs-lookup"><span data-stu-id="d4075-152">`Microsoft.Network/dnsZones/CNAME/*` grants full control over CNAME records</span></span>
* <span data-ttu-id="d4075-153">`Microsoft.Network/dnsZones/read`confiere a las zonas DNS de tooread de permiso, pero no toomodify ellos, lo que permite toosee Hola zona en qué Hola CNAME se está creando.</span><span class="sxs-lookup"><span data-stu-id="d4075-153">`Microsoft.Network/dnsZones/read` grants permission tooread DNS zones, but not toomodify them, enabling you toosee hello zone in which hello CNAME is being created.</span></span>

<span data-ttu-id="d4075-154">Hola acciones restantes se copian de hello [rol de colaborador de zona DNS integrado](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span><span class="sxs-lookup"><span data-stu-id="d4075-154">hello remaining Actions are copied from hello [DNS Zone Contributor built-in role](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span></span>

> [!NOTE]
> <span data-ttu-id="d4075-155">Usar un tooprevent personalizado de rol RBAC eliminando el registro conjuntos mientras sigue permitiendo toobe actualizado no es un control efectivo.</span><span class="sxs-lookup"><span data-stu-id="d4075-155">Using a custom RBAC role tooprevent deleting record sets while still allowing them toobe updated is not an effective control.</span></span> <span data-ttu-id="d4075-156">Evita que los conjuntos de registros se eliminen, pero no que se modifiquen.</span><span class="sxs-lookup"><span data-stu-id="d4075-156">It prevents record sets from being deleted, but it does not prevent them from being modified.</span></span>  <span data-ttu-id="d4075-157">Modificaciones permitidas incluyen la adición y eliminación de registros del conjunto de registros de hello, incluida la eliminación de todos los registra tooleave un conjunto de registros 'empty'.</span><span class="sxs-lookup"><span data-stu-id="d4075-157">Permitted modifications include adding and removing records from hello record set, including removing all records tooleave an 'empty' record set.</span></span> <span data-ttu-id="d4075-158">Esto tiene Hola establece el mismo efecto que eliminar registro de hello desde un punto de vista de resolución DNS.</span><span class="sxs-lookup"><span data-stu-id="d4075-158">This has hello same effect as deleting hello record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="d4075-159">Las definiciones de roles personalizados actualmente no se puede definir a través de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="d4075-159">Custom role definitions cannot currently be defined via hello Azure portal.</span></span> <span data-ttu-id="d4075-160">Puede crearse un rol personalizado basado en esta definición de rol mediante Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d4075-160">A custom role based on this role definition can be created using Azure PowerShell:</span></span>

```powershell
# Create new role definition based on input file
New-AzureRmRoleDefinition -InputFile <file path>
```

<span data-ttu-id="d4075-161">También pueden crearse a través de hello CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="d4075-161">It can also be created via hello Azure CLI:</span></span>

```azurecli
# Create new role definition based on input file
azure role create -inputfile <file path>
```

<span data-ttu-id="d4075-162">Hello rol, a continuación, se puede asignar en hello misma manera como funciones integradas, como se describe anteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="d4075-162">hello role can then be assigned in hello same way as built-in roles, as described earlier in this article.</span></span>

<span data-ttu-id="d4075-163">Para obtener más información acerca de cómo administrar toocreate y asignar roles personalizados, consulte [Roles personalizados en Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="d4075-163">For more information on how toocreate, manage, and assign custom roles, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="resource-locks"></a><span data-ttu-id="d4075-164">Bloqueos de recursos</span><span class="sxs-lookup"><span data-stu-id="d4075-164">Resource locks</span></span>

<span data-ttu-id="d4075-165">En suma tooRBAC, Administrador de recursos de Azure admite otro tipo de control de seguridad, es decir Hola capacidad too'lock' recursos.</span><span class="sxs-lookup"><span data-stu-id="d4075-165">In addition tooRBAC, Azure Resource Manager supports another type of security control, namely hello ability too'lock' resources.</span></span> <span data-ttu-id="d4075-166">Donde las reglas RBAC permiten acciones de hello toocontrol de usuarios y grupos concretos, bloqueos de recursos aplicada toohello recursos y son eficaces a través de todos los usuarios y roles.</span><span class="sxs-lookup"><span data-stu-id="d4075-166">Where RBAC rules allow you toocontrol hello actions of specific users and groups, resource locks are applied toohello resource, and are effective across all users and roles.</span></span> <span data-ttu-id="d4075-167">Para obtener más información, consulte [Bloqueo de recursos con el Administrador de recursos de Azure](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="d4075-167">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

<span data-ttu-id="d4075-168">Hay dos tipos de bloqueo de recurso: **DoNotDelete** y **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="d4075-168">There are two types of resource lock: **DoNotDelete** and **ReadOnly**.</span></span> <span data-ttu-id="d4075-169">Estos se pueden aplicar tooa zona DNS o tooan conjunto de registros individuales.</span><span class="sxs-lookup"><span data-stu-id="d4075-169">These can be applied either tooa DNS zone, or tooan individual record set.</span></span>  <span data-ttu-id="d4075-170">Hello las secciones siguientes describen varios escenarios comunes y cómo toosupport mediante bloqueos de recursos.</span><span class="sxs-lookup"><span data-stu-id="d4075-170">hello following sections describe several common scenarios, and how toosupport them using resource locks.</span></span>

### <a name="protecting-against-all-changes"></a><span data-ttu-id="d4075-171">Protección contra todos los cambios</span><span class="sxs-lookup"><span data-stu-id="d4075-171">Protecting against all changes</span></span>

<span data-ttu-id="d4075-172">tooprevent cualquier modificación que se va a realizar, aplicar una zona de toohello de bloqueo de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="d4075-172">tooprevent any changes being made, apply a ReadOnly lock toohello zone.</span></span>  <span data-ttu-id="d4075-173">Esto impide que se creen otros conjuntos de registros y que se modifiquen o eliminen conjuntos de registros existentes.</span><span class="sxs-lookup"><span data-stu-id="d4075-173">This prevents new record sets from being created, and existing record sets from being modified or deleted.</span></span>

<span data-ttu-id="d4075-174">Bloqueos de recursos en el nivel de zona se pueden crear a través de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="d4075-174">Zone level resource locks can be created via hello Azure portal.</span></span>  <span data-ttu-id="d4075-175">Desde la hoja de la zona DNS de hello, haga clic en 'Bloqueos', 'Add' a continuación:</span><span class="sxs-lookup"><span data-stu-id="d4075-175">From hello DNS zone blade, click 'Locks', then 'Add':</span></span>

![Bloqueos de recursos en el nivel de zona a través de hello portal de Azure](./media/dns-protect-zones-recordsets/locks1.png)

<span data-ttu-id="d4075-177">También pueden crearse bloqueos de recursos de nivel de zona a través de Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d4075-177">Zone-level resource locks can also be created via Azure PowerShell:</span></span>

```powershell
# Lock a DNS zone
New-AzureRmResourceLock -LockLevel <lock level> -LockName <lock name> -ResourceName <zone name> -ResourceType Microsoft.Network/DNSZones -ResourceGroupName <resource group name>
```

<span data-ttu-id="d4075-178">Configuración de bloqueos de recursos de Azure no se admite actualmente a través de hello CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="d4075-178">Configuring Azure resource locks is not currently supported via hello Azure CLI.</span></span>

### <a name="protecting-individual-records"></a><span data-ttu-id="d4075-179">Protección de registros individuales</span><span class="sxs-lookup"><span data-stu-id="d4075-179">Protecting individual records</span></span>

<span data-ttu-id="d4075-180">tooprevent un registro DNS existente establecer frente a su modificación, aplicar un conjunto de registros de toohello de bloqueo de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="d4075-180">tooprevent an existing DNS record set against modification, apply a ReadOnly lock toohello record set.</span></span>

> [!NOTE]
> <span data-ttu-id="d4075-181">Aplicar un tooa de bloqueo DoNotDelete conjunto de registros no es un control efectivo.</span><span class="sxs-lookup"><span data-stu-id="d4075-181">Applying a DoNotDelete lock tooa record set is not an effective control.</span></span> <span data-ttu-id="d4075-182">Se evita que el conjunto que se eliminen de registros de hello, pero no se impide que está modificando.</span><span class="sxs-lookup"><span data-stu-id="d4075-182">It prevents hello record set from being deleted, but it does not prevent it from being modified.</span></span>  <span data-ttu-id="d4075-183">Modificaciones permitidas incluyen la adición y eliminación de registros del conjunto de registros de hello, incluida la eliminación de todos los registra tooleave un conjunto de registros 'empty'.</span><span class="sxs-lookup"><span data-stu-id="d4075-183">Permitted modifications include adding and removing records from hello record set, including removing all records tooleave an 'empty' record set.</span></span> <span data-ttu-id="d4075-184">Esto tiene Hola establece el mismo efecto que eliminar registro de hello desde un punto de vista de resolución DNS.</span><span class="sxs-lookup"><span data-stu-id="d4075-184">This has hello same effect as deleting hello record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="d4075-185">Actualmente, los bloqueos de recursos de nivel de conjunto de recursos solo pueden configurarse mediante Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d4075-185">Record set level resource locks can currently only be configured using Azure PowerShell.</span></span>  <span data-ttu-id="d4075-186">No se admiten en el portal de Azure de Hola o CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="d4075-186">They are not supported in hello Azure portal or Azure CLI.</span></span>

```powershell
# Lock a DNS record set
New-AzureRmResourceLock -LockLevel <lock level> -LockName "<lock name>" -ResourceName "<zone name>/<record set name>" -ResourceType "Microsoft.Network/DNSZones/<record type>" -ResourceGroupName "<resource group name>"
```

### <a name="protecting-against-zone-deletion"></a><span data-ttu-id="d4075-187">Protección contra la eliminación de zonas</span><span class="sxs-lookup"><span data-stu-id="d4075-187">Protecting against zone deletion</span></span>

<span data-ttu-id="d4075-188">Cuando se elimina una zona de DNS de Azure, también se eliminan todos los conjuntos de registros de zona de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4075-188">When a zone is deleted in Azure DNS, all record sets in hello zone are also deleted.</span></span>  <span data-ttu-id="d4075-189">Esta operación no se puede deshacer.</span><span class="sxs-lookup"><span data-stu-id="d4075-189">This operation cannot be undone.</span></span>  <span data-ttu-id="d4075-190">La eliminación accidental de una zona crítica afecte al toohave posibles Hola significativos para el negocio.</span><span class="sxs-lookup"><span data-stu-id="d4075-190">Accidentally deleting a critical zone has hello potential toohave a significant business impact.</span></span>  <span data-ttu-id="d4075-191">Por lo tanto, es muy importante tooprotect contra la eliminación accidental de zona.</span><span class="sxs-lookup"><span data-stu-id="d4075-191">It is therefore very important tooprotect against accidental zone deletion.</span></span>

<span data-ttu-id="d4075-192">La aplicación de una zona de tooa DoNotDelete bloqueo impide zona Hola se eliminen.</span><span class="sxs-lookup"><span data-stu-id="d4075-192">Applying a DoNotDelete lock tooa zone prevents hello zone from being deleted.</span></span>  <span data-ttu-id="d4075-193">Sin embargo, puesto que los bloqueos son heredados por recursos secundarios, también evita que los conjuntos de registros en la zona de Hola se eliminen, lo que puede no ser deseable.</span><span class="sxs-lookup"><span data-stu-id="d4075-193">However, since locks are inherited by child resources, it also prevents any record sets in hello zone from being deleted, which may be undesirable.</span></span>  <span data-ttu-id="d4075-194">Además, como se describe en la nota de hello anterior, también es ineficaces ya que todavía se pueden quitar registros de conjuntos de registros existentes de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4075-194">Furthermore, as described in hello note above, it is also ineffective since records can still be removed from hello existing record sets.</span></span>

<span data-ttu-id="d4075-195">Como alternativa, considere la posibilidad de aplicar un registro de tooa DoNotDelete bloqueo establecida en zona de hello, como conjunto de registros de SOA de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4075-195">As an alternative, consider applying a DoNotDelete lock tooa record set in hello zone, such as hello SOA record set.</span></span>  <span data-ttu-id="d4075-196">Puesto que no se puede eliminar la zona de hello sin eliminar también los conjuntos de registros de hello, esto protege contra la eliminación de zona, mientras sigue permitiendo conjuntos de registros dentro de hello zona toobe modificado libremente.</span><span class="sxs-lookup"><span data-stu-id="d4075-196">Since hello zone cannot be deleted without also deleting hello record sets, this protects against zone deletion, while still allowing record sets within hello zone toobe modified freely.</span></span> <span data-ttu-id="d4075-197">Si se realiza un intento toodelete zona de hello, Azure Resource Manager detecta esto también eliminaría el conjunto de registros de SOA de Hola y bloques de Hola llamada porque está bloqueado Hola SOA.</span><span class="sxs-lookup"><span data-stu-id="d4075-197">If an attempt is made toodelete hello zone, Azure Resource Manager detects this would also delete hello SOA record set, and blocks hello call because hello SOA is locked.</span></span>  <span data-ttu-id="d4075-198">No se elimina ningún conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="d4075-198">No record sets are deleted.</span></span>

<span data-ttu-id="d4075-199">Hola siguiente comando de PowerShell crea un bloqueo de DoNotDelete en el registro SOA de Hola de hello dado zona:</span><span class="sxs-lookup"><span data-stu-id="d4075-199">hello following PowerShell command creates a DoNotDelete lock against hello SOA record of hello given zone:</span></span>

```powershell
# Protect against zone delete with DoNotDelete lock on hello record set
New-AzureRmResourceLock -LockLevel DoNotDelete -LockName "<lock name>" -ResourceName "<zone name>/@" -ResourceType" Microsoft.Network/DNSZones/SOA" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="d4075-200">Otra manera de eliminación de zona accidental de tooprevent es mediante un operador de roles personalizados tooensure hello y servicio toomanage de cuentas que se usan las zonas no dispone de zona eliminar los permisos.</span><span class="sxs-lookup"><span data-stu-id="d4075-200">Another way tooprevent accidental zone deletion is by using a custom role tooensure hello operator and service accounts used toomanage your zones do not have zone delete permissions.</span></span> <span data-ttu-id="d4075-201">Cuando es necesario toodelete una zona, puede aplicar una eliminación de dos pasos, primer conceda permisos de eliminación de zona (en el ámbito de zona de hello, tooprevent eliminar zona incorrecta hello) y la segunda zona de hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="d4075-201">When you do need toodelete a zone, you can enforce a two-step delete, first granting zone delete permissions (at hello zone scope, tooprevent deleting hello wrong zone) and second toodelete hello zone.</span></span>

<span data-ttu-id="d4075-202">Este segundo método tiene la ventaja de Hola que funciona para todas las zonas de acceso a esas cuentas sin necesidad de tooremember toocreate los bloqueos.</span><span class="sxs-lookup"><span data-stu-id="d4075-202">This second approach has hello advantage that it works for all zones accessed by those accounts, without having tooremember toocreate any locks.</span></span> <span data-ttu-id="d4075-203">Tiene la desventaja de Hola que las cuentas con permisos de eliminación de zona, como propietario de la suscripción de hello, pueden eliminar accidentalmente aún una zona crítica.</span><span class="sxs-lookup"><span data-stu-id="d4075-203">It has hello disadvantage that any accounts with zone delete permissions, such as hello subscription owner, can still accidentally delete a critical zone.</span></span>

<span data-ttu-id="d4075-204">Es posible toouse ambos enfoques, bloqueos de recursos y roles personalizados, en hello mismo tiempo, como un enfoque de defensa en profundidad tooDNS zona de protección.</span><span class="sxs-lookup"><span data-stu-id="d4075-204">It is possible toouse both approaches - resource locks and custom roles - at hello same time, as a defense-in-depth approach tooDNS zone protection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4075-205">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d4075-205">Next steps</span></span>

* <span data-ttu-id="d4075-206">Para obtener más información sobre cómo trabajar con RBAC, consulte [comenzar con la administración de acceso de hello portal de Azure](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="d4075-206">For more information about working with RBAC, see [Get started with access management in hello Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>
* <span data-ttu-id="d4075-207">Para más información sobre cómo trabajar con bloqueos de recursos, vea [Bloqueo de recursos con Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="d4075-207">For more information about working with resource locks, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

