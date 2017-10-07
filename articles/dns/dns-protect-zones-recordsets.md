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
# <a name="how-tooprotect-dns-zones-and-records"></a>¿Cómo tooprotect DNS zonas y registros

Los registros y las zonas DNS son recursos críticos. Si se elimina una zona DNS o incluso tan solo un registro DNS puede provocar una interrupción total del servicio.  Por consiguiente, es importante proteger las zonas y los registros DNS críticos contra cambios accidentales o no autorizados.

Este artículo explica cómo DNS de Azure permite tooprotect sus zonas y registros DNS con dichos cambios.  Aplicamos dos eficaces características de seguridad que proporciona Azure Resource Manager: [control de acceso basado en rol](../active-directory/role-based-access-control-what-is.md) y [bloqueos de recursos](../azure-resource-manager/resource-group-lock-resources.md).

## <a name="role-based-access-control"></a>Control de acceso basado en rol

El control de acceso basado en rol (RBAC) de Azure permite realizar una administración detallada del acceso de usuarios, grupos y recursos de Azure. Usar RBAC, puede conceder con precisión el importe de Hola de acceso que los usuarios necesitan tooperform sus trabajos. Para más información sobre cómo RBAC ayuda a administrar el acceso, vea [Introducción a la administración de acceso en Azure Portal](../active-directory/role-based-access-control-what-is.md).

### <a name="hello-dns-zone-contributor-role"></a>rol de Hello 'Colaborador de zona DNS'

rol de Hello 'Colaborador de zona DNS' es un rol integrado proporcionado por Azure para administrar recursos DNS.  Asignación de grupo o usuario de tooa de permisos de colaborador de la zona de DNS permite que agrupar toomanage los recursos DNS, pero no los recursos de cualquier otro tipo.

Por ejemplo, suponga que el grupo de recursos de hello 'myzones' contiene cinco zonas para Contoso Corporation. La concesión Hola DNS administrador 'Colaborador de zona DNS' permisos toothat grupo de recursos, permite control total sobre las zonas DNS. También evita conceder permisos innecesarios, por ejemplo el administrador DNS hello no puede crear ni detener máquinas virtuales.

permisos de RBAC de manera más sencillos de Hello tooassign es [a través del portal de Azure hello](../active-directory/role-based-access-control-configure.md).  Abra hoja hello 'control de acceso (de índices IAM)' para el grupo de recursos de hello, a continuación, haga clic en 'Agregar' y seleccione el rol de hello 'Colaborador de zona DNS' y usuarios de hello seleccione necesario o grupos toogrant permisos.

![Nivel de grupo de recursos RBAC a través de hello portal de Azure](./media/dns-protect-zones-recordsets/rbac1.png)

Los permisos también se pueden [conceder mediante Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):

```powershell
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>"
```

También es el comando equivalente de Hello [disponibles a través de hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):

```azurecli
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --resourceGroup "<resource group name>"
```

### <a name="zone-level-rbac"></a>RBAC de nivel de zona

Las reglas de RBAC Azure pueden ser suscripción tooa aplicado, un recurso de individuales de tooan o grupo de recursos. En caso de hello de DNS de Azure, ese recurso puede ser una zona DNS individual, o incluso un conjunto de registros individual.

Por ejemplo, suponga que el grupo de recursos de hello 'myzones' contiene una subzona 'customers.contoso.com' en el que se crean los registros CNAME para cada cuenta de cliente y zona hello 'contoso.com'.  Hola cuenta usada toomanage estos registros CNAME deben asignarse registros de toocreate de permisos de zona sólo de hello 'customers.contoso.com', no debería tener acceso toohello otras zonas.

Se pueden conceder permisos de nivel de zona RBAC a través de hello portal de Azure.  Abrir hello 'Control de acceso (de índices IAM)' hoja para zona de hello, a continuación, haga clic en 'Agregar', seleccione el rol de 'Colaborador de zona DNS' hello y usuarios de hello seleccione necesario o permisos de toogrant de grupos.

![RBAC de nivel de zona DNS a través de hello portal de Azure](./media/dns-protect-zones-recordsets/rbac2.png)

Los permisos también se pueden [conceder mediante Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):

```powershell
# Grant 'DNS Zone Contributor' permissions tooa specific zone
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>" -ResourceName "<zone name>" -ResourceType Microsoft.Network/DNSZones
```

También es el comando equivalente de Hello [disponibles a través de hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):

```azurecli
# Grant 'DNS Zone Contributor' permissions tooa specific zone
azure role assignment create --signInName <user email address> --roleName "DNS Zone Contributor" --resource-name <zone name> --resource-type Microsoft.Network/DNSZones --resource-group <resource group name>
```

### <a name="record-set-level-rbac"></a>RBAC de nivel de conjunto de registros

Podemos ir más lejos. Considere la posibilidad de administrador de correo electrónico de Hola para Contoso Corporation, que necesita acceso toohello MX y registros TXT en vértice Hola de zona de 'contoso.com' hello.  No necesita tener acceso a tooany otros registros MX o TXT o tooany registros de cualquier otro tipo.  DNS de Azure permite que los permisos tooassign Hola conjunto de registros, tooprecisely Hola registros a nivel que Hola Administrador de correo electrónico necesita tener acceso a.  Hello correo se concede al administrador controlar con precisión de hello ella necesita y es no se puede toomake cualquier otro cambio.

Permisos de RBAC de nivel de conjunto de registros se pueden configurar a través del portal de Azure, con el botón Hola 'usuarios' en la hoja de conjunto de registros de Hola Hola:

![Nivel de RBAC a través del portal de Azure Hola de conjunto de registros](./media/dns-protect-zones-recordsets/rbac3.png)

Los permisos RBAC de nivel de conjunto de registros también se pueden [conceder mediante Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):

```powershell
# Grant permissions tooa specific record set
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -Scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

También es el comando equivalente de Hello [disponibles a través de hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):

```azurecli
# Grant permissions tooa specific record set
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

### <a name="custom-roles"></a>Roles personalizados

rol de Hello integrado 'Colaborador de zona DNS' permite un control total sobre un recurso DNS. También es posible toobuild su propio cliente Azure roles, control de tooprovide incluso más precisa.

Considere la posibilidad de nuevo ejemplo hello en el que se crea un registro CNAME en la zona de hello 'customers.contoso.com' para cada cuenta de cliente de Contoso Corporation.  Hola cuenta usada toomanage estos CNAME debe contar con permiso toomanage CNAME sólo los registros.  Es, a continuación, no se puede toomodify registros de otros tipos (por ejemplo, cambiar los registros MX) o realizar operaciones de nivel de zona como la eliminación de zona.

Hola de ejemplo siguiente muestra una definición de rol personalizada para administrar solo los registros CNAME:

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

Hola propiedad Actions define Hola los siguientes permisos específicas de DNS:

* `Microsoft.Network/dnsZones/CNAME/*` concede control total sobre registros CNAME
* `Microsoft.Network/dnsZones/read`confiere a las zonas DNS de tooread de permiso, pero no toomodify ellos, lo que permite toosee Hola zona en qué Hola CNAME se está creando.

Hola acciones restantes se copian de hello [rol de colaborador de zona DNS integrado](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).

> [!NOTE]
> Usar un tooprevent personalizado de rol RBAC eliminando el registro conjuntos mientras sigue permitiendo toobe actualizado no es un control efectivo. Evita que los conjuntos de registros se eliminen, pero no que se modifiquen.  Modificaciones permitidas incluyen la adición y eliminación de registros del conjunto de registros de hello, incluida la eliminación de todos los registra tooleave un conjunto de registros 'empty'. Esto tiene Hola establece el mismo efecto que eliminar registro de hello desde un punto de vista de resolución DNS.

Las definiciones de roles personalizados actualmente no se puede definir a través de hello portal de Azure. Puede crearse un rol personalizado basado en esta definición de rol mediante Azure PowerShell:

```powershell
# Create new role definition based on input file
New-AzureRmRoleDefinition -InputFile <file path>
```

También pueden crearse a través de hello CLI de Azure:

```azurecli
# Create new role definition based on input file
azure role create -inputfile <file path>
```

Hello rol, a continuación, se puede asignar en hello misma manera como funciones integradas, como se describe anteriormente en este artículo.

Para obtener más información acerca de cómo administrar toocreate y asignar roles personalizados, consulte [Roles personalizados en Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).

## <a name="resource-locks"></a>Bloqueos de recursos

En suma tooRBAC, Administrador de recursos de Azure admite otro tipo de control de seguridad, es decir Hola capacidad too'lock' recursos. Donde las reglas RBAC permiten acciones de hello toocontrol de usuarios y grupos concretos, bloqueos de recursos aplicada toohello recursos y son eficaces a través de todos los usuarios y roles. Para obtener más información, consulte [Bloqueo de recursos con el Administrador de recursos de Azure](../azure-resource-manager/resource-group-lock-resources.md).

Hay dos tipos de bloqueo de recurso: **DoNotDelete** y **ReadOnly**. Estos se pueden aplicar tooa zona DNS o tooan conjunto de registros individuales.  Hello las secciones siguientes describen varios escenarios comunes y cómo toosupport mediante bloqueos de recursos.

### <a name="protecting-against-all-changes"></a>Protección contra todos los cambios

tooprevent cualquier modificación que se va a realizar, aplicar una zona de toohello de bloqueo de solo lectura.  Esto impide que se creen otros conjuntos de registros y que se modifiquen o eliminen conjuntos de registros existentes.

Bloqueos de recursos en el nivel de zona se pueden crear a través de hello portal de Azure.  Desde la hoja de la zona DNS de hello, haga clic en 'Bloqueos', 'Add' a continuación:

![Bloqueos de recursos en el nivel de zona a través de hello portal de Azure](./media/dns-protect-zones-recordsets/locks1.png)

También pueden crearse bloqueos de recursos de nivel de zona a través de Azure PowerShell:

```powershell
# Lock a DNS zone
New-AzureRmResourceLock -LockLevel <lock level> -LockName <lock name> -ResourceName <zone name> -ResourceType Microsoft.Network/DNSZones -ResourceGroupName <resource group name>
```

Configuración de bloqueos de recursos de Azure no se admite actualmente a través de hello CLI de Azure.

### <a name="protecting-individual-records"></a>Protección de registros individuales

tooprevent un registro DNS existente establecer frente a su modificación, aplicar un conjunto de registros de toohello de bloqueo de solo lectura.

> [!NOTE]
> Aplicar un tooa de bloqueo DoNotDelete conjunto de registros no es un control efectivo. Se evita que el conjunto que se eliminen de registros de hello, pero no se impide que está modificando.  Modificaciones permitidas incluyen la adición y eliminación de registros del conjunto de registros de hello, incluida la eliminación de todos los registra tooleave un conjunto de registros 'empty'. Esto tiene Hola establece el mismo efecto que eliminar registro de hello desde un punto de vista de resolución DNS.

Actualmente, los bloqueos de recursos de nivel de conjunto de recursos solo pueden configurarse mediante Azure PowerShell.  No se admiten en el portal de Azure de Hola o CLI de Azure.

```powershell
# Lock a DNS record set
New-AzureRmResourceLock -LockLevel <lock level> -LockName "<lock name>" -ResourceName "<zone name>/<record set name>" -ResourceType "Microsoft.Network/DNSZones/<record type>" -ResourceGroupName "<resource group name>"
```

### <a name="protecting-against-zone-deletion"></a>Protección contra la eliminación de zonas

Cuando se elimina una zona de DNS de Azure, también se eliminan todos los conjuntos de registros de zona de Hola.  Esta operación no se puede deshacer.  La eliminación accidental de una zona crítica afecte al toohave posibles Hola significativos para el negocio.  Por lo tanto, es muy importante tooprotect contra la eliminación accidental de zona.

La aplicación de una zona de tooa DoNotDelete bloqueo impide zona Hola se eliminen.  Sin embargo, puesto que los bloqueos son heredados por recursos secundarios, también evita que los conjuntos de registros en la zona de Hola se eliminen, lo que puede no ser deseable.  Además, como se describe en la nota de hello anterior, también es ineficaces ya que todavía se pueden quitar registros de conjuntos de registros existentes de Hola.

Como alternativa, considere la posibilidad de aplicar un registro de tooa DoNotDelete bloqueo establecida en zona de hello, como conjunto de registros de SOA de Hola.  Puesto que no se puede eliminar la zona de hello sin eliminar también los conjuntos de registros de hello, esto protege contra la eliminación de zona, mientras sigue permitiendo conjuntos de registros dentro de hello zona toobe modificado libremente. Si se realiza un intento toodelete zona de hello, Azure Resource Manager detecta esto también eliminaría el conjunto de registros de SOA de Hola y bloques de Hola llamada porque está bloqueado Hola SOA.  No se elimina ningún conjunto de registros.

Hola siguiente comando de PowerShell crea un bloqueo de DoNotDelete en el registro SOA de Hola de hello dado zona:

```powershell
# Protect against zone delete with DoNotDelete lock on hello record set
New-AzureRmResourceLock -LockLevel DoNotDelete -LockName "<lock name>" -ResourceName "<zone name>/@" -ResourceType" Microsoft.Network/DNSZones/SOA" -ResourceGroupName "<resource group name>"
```

Otra manera de eliminación de zona accidental de tooprevent es mediante un operador de roles personalizados tooensure hello y servicio toomanage de cuentas que se usan las zonas no dispone de zona eliminar los permisos. Cuando es necesario toodelete una zona, puede aplicar una eliminación de dos pasos, primer conceda permisos de eliminación de zona (en el ámbito de zona de hello, tooprevent eliminar zona incorrecta hello) y la segunda zona de hello toodelete.

Este segundo método tiene la ventaja de Hola que funciona para todas las zonas de acceso a esas cuentas sin necesidad de tooremember toocreate los bloqueos. Tiene la desventaja de Hola que las cuentas con permisos de eliminación de zona, como propietario de la suscripción de hello, pueden eliminar accidentalmente aún una zona crítica.

Es posible toouse ambos enfoques, bloqueos de recursos y roles personalizados, en hello mismo tiempo, como un enfoque de defensa en profundidad tooDNS zona de protección.

## <a name="next-steps"></a>Pasos siguientes

* Para obtener más información sobre cómo trabajar con RBAC, consulte [comenzar con la administración de acceso de hello portal de Azure](../active-directory/role-based-access-control-what-is.md).
* Para más información sobre cómo trabajar con bloqueos de recursos, vea [Bloqueo de recursos con Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).

