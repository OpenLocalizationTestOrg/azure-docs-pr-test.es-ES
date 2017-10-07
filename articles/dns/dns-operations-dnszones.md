---
title: aaaManage DNS zonas en DNS de Azure - PowerShell | Documentos de Microsoft
description: "Puede administrar zonas DNS con Azure Powershell. Este artículo describe cómo eliminar tooupdate y cómo crear las zonas DNS en el DNS de Azure"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: a67992ab-8166-4052-9b28-554c5a39e60c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: gwallace
ms.openlocfilehash: 261b89f72213aa9784034d47ff9d1c55a4e80d65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-using-powershell"></a>¿Cómo toomanage zonas de DNS con PowerShell

> [!div class="op_single_selector"]
> * [Portal](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [CLI de Azure 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [CLI de Azure 2.0](dns-operations-dnszones-cli.md)

Este artículo muestra cómo toomanage su DNS zonas mediante el uso de PowerShell de Azure. También puede administrar las zonas DNS con hello multiplataforma [CLI de Azure](dns-operations-dnszones-cli.md) u Hola portal de Azure.

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)]


## <a name="create-a-dns-zone"></a>Creación de una zona DNS

Se crea una zona DNS mediante el uso de hello `New-AzureRmDnsZone` cmdlet.

Hello en el ejemplo siguiente se crea una zona DNS denominada *contoso.com* en grupo de recursos de hello denominado *MyResourceGroup*:

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

Hello en el ejemplo siguiente se muestra cómo toocreate un DNS de la zona con dos [etiquetas de Azure Resource Manager](dns-zones-records.md#tags), *proyecto = demostración* y *env = test*:

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

## <a name="get-a-dns-zone"></a>Recuperación de una zona DNS

tooretrieve una zona DNS, usar hello `Get-AzureRmDnsZone` cmdlet. Esta operación devuelve un DNS de la zona objeto tooan existente zona correspondiente en DNS de Azure. Hello objeto contiene los datos sobre la zona de hello (por ejemplo, el número de Hola de conjuntos de registros), pero no contiene conjuntos de registros de Hola a sí mismos (consulte `Get-AzureRmDnsRecordSet`).

```powershell
Get-AzureRmDnsZone -Name contoso.com –ResourceGroupName MyAzureResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-8ec2-f4879750d201
Tags                  : {project, env}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org.,
                        ns4-01.azure-dns.info.}
NumberOfRecordSets    : 2
MaxNumberOfRecordSets : 5000
```

## <a name="list-dns-zones"></a>Enumeración de zonas DNS

Si se omite el nombre de la zona de hello `Get-AzureRmDnsZone`, puede enumerar todas las zonas de un grupo de recursos. Esta operación devuelve una matriz de objetos de la zona.

```powershell
$zoneList = Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

Si se omite el nombre de la zona de Hola y el nombre del grupo de recursos de hello `Get-AzureRmDnsZone`, puede enumerar todas las zonas de hello suscripción de Azure.

```powershell
$zoneList = Get-AzureRmDnsZone
```

## <a name="update-a-dns-zone"></a>Actualización de una zona DNS

Cambia tooa recursos de la zona DNS pueden hacerse mediante `Set-AzureRmDnsZone`. Este cmdlet no actualiza cualquiera de los conjuntos de registros de DNS de hello en la zona de hello (vea [cómo los registros DNS tooManage](dns-operations-recordsets.md)). Solo ha utilizado propiedades tooupdate del propio recurso de zona Hola. propiedades de la zona de escritura de Hello están limitada actualmente toohello [Azure Resource Manager 'etiqueta' para el recurso de la zona de hello](dns-zones-records.md#tags).

Use uno de hello después tooupdate de dos maneras una zona DNS:

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group"></a>Especifique zona hello mediante el grupo de recursos y el nombre de la zona de Hola

Este enfoque reemplaza las etiquetas existentes de zona Hola con valores de hello especificados.

```powershell
Set-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

### <a name="specify-hello-zone-using-a-zone-object"></a>Especificar la zona de hello mediante un objeto $zone

Este método recupera el objeto existente de la zona de hello, modifica etiquetas de hello y, a continuación, confirme los cambios de Hola. De este modo, se pueden conservar las etiquetas existentes.

```powershell
# Get hello zone object
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup

# Remove an existing tag
$zone.Tags.Remove("project")

# Add a new tag
$zone.Tags.Add("status","approved")

# Commit changes
Set-AzureRmDnsZone -Zone $zone
```

Cuando se usa `Set-AzureRmDnsZone` con un objeto $zone, [Etag comprueba](dns-zones-records.md#etags) sirven cambios simultáneos tooensure no se sobrescriben. Puede usar Hola opcional `-Overwrite` cambiar toosuppress estas comprobaciones.

## <a name="delete-a-dns-zone"></a>Eliminación de una zona DNS

Las zonas DNS pueden eliminarse con hello `Remove-AzureRmDnsZone` cmdlet.

> [!NOTE]
> Al eliminar una zona DNS, también eliminan todos los registros DNS en la zona de Hola. Esta operación no se puede deshacer. Si la zona DNS Hola está en uso, se producirá un error en servicios con zona de hello cuando se elimina la zona de Hola.
>
>tooprotect contra la eliminación accidental de zona, consulte [cómo tooprotect DNS zonas y registros](dns-protect-zones-recordsets.md).


Use uno de hello después toodelete de dos maneras una zona DNS:

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group-name"></a>Especifique con el nombre de la zona de Hola y el nombre del grupo de recursos de zona de Hola

```powershell
Remove-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

### <a name="specify-hello-zone-using-a-zone-object"></a>Especificar la zona de hello mediante un objeto $zone

Puede especificar Hola zona toobe eliminado mediante una `$zone` objeto devuelto por `Get-AzureRmDnsZone`.

```powershell
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
Remove-AzureRmDnsZone -Zone $zone
```

También se puede canalizar el objeto de la zona de Hello en lugar de que se pasa como parámetro:

```powershell
Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup | Remove-AzureRmDnsZone

```

Al igual que con `Set-AzureRmDnsZone`, especificar Hola zona mediante una `$zone` habilita Etag comprueba los cambios simultáneos de tooensure no se eliminan del objeto. Hola de uso `-Overwrite` cambiar toosuppress estas comprobaciones.

## <a name="confirmation-prompts"></a>Mensajes de confirmación

Hola `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, y `Remove-AzureRmDnsZone` todos los cmdlets admiten mensajes de confirmación.

Ambos `New-AzureRmDnsZone` y `Set-AzureRmDnsZone` solicite confirmación si hello `$ConfirmPreference` variable de preferencia de PowerShell tiene un valor de `Medium` o inferior. Pagar toohello potencialmente alto impacto de la eliminación de una zona DNS, hello `Remove-AzureRmDnsZone` cmdlet pide confirmación si hello `$ConfirmPreference` variable de PowerShell tiene cualquier valor distinto de `None`.

Desde el valor predeterminado de Hola para `$ConfirmPreference` es `High`, solo `Remove-AzureRmDnsZone` pide confirmación de forma predeterminada.

Puede invalidar Hola actual `$ConfirmPreference` configuración mediante hello `-Confirm` parámetro. Si especifica `-Confirm` o `-Confirm:$True` , Hola cmdlet solicita confirmación antes de que se ejecuta. Si especifica `-Confirm:$False` , Hola cmdlet no pide confirmación.

Para más información sobre `-Confirm` y `$ConfirmPreference`, consulte [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables) (Acerca de las variables de preferencias).

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo demasiado[administrar conjuntos de registros y registros](dns-operations-recordsets.md) en la zona DNS.
<br>
Obtenga información acerca de cómo demasiado[delegar su tooAzure de dominio DNS](dns-domain-delegation.md).
<br>
Hola de revisión [documentación de referencia de PowerShell de DNS de Azure](/powershell/module/azurerm.dns).

