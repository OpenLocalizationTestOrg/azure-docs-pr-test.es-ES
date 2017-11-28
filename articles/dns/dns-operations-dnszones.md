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
# <a name="how-toomanage-dns-zones-using-powershell"></a><span data-ttu-id="ed9b7-104">¿Cómo toomanage zonas de DNS con PowerShell</span><span class="sxs-lookup"><span data-stu-id="ed9b7-104">How toomanage DNS Zones using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ed9b7-105">Portal</span><span class="sxs-lookup"><span data-stu-id="ed9b7-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="ed9b7-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ed9b7-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="ed9b7-107">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="ed9b7-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="ed9b7-108">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="ed9b7-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="ed9b7-109">Este artículo muestra cómo toomanage su DNS zonas mediante el uso de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="ed9b7-109">This article shows you how toomanage your DNS zones by using Azure PowerShell.</span></span> <span data-ttu-id="ed9b7-110">También puede administrar las zonas DNS con hello multiplataforma [CLI de Azure](dns-operations-dnszones-cli.md) u Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="ed9b7-110">You can also manage your DNS zones using hello cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or hello Azure portal.</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)]


## <a name="create-a-dns-zone"></a><span data-ttu-id="ed9b7-111">Creación de una zona DNS</span><span class="sxs-lookup"><span data-stu-id="ed9b7-111">Create a DNS zone</span></span>

<span data-ttu-id="ed9b7-112">Se crea una zona DNS mediante el uso de hello `New-AzureRmDnsZone` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ed9b7-112">A DNS zone is created by using hello `New-AzureRmDnsZone` cmdlet.</span></span>

<span data-ttu-id="ed9b7-113">Hello en el ejemplo siguiente se crea una zona DNS denominada *contoso.com* en grupo de recursos de hello denominado *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="ed9b7-113">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="ed9b7-114">Hello en el ejemplo siguiente se muestra cómo toocreate un DNS de la zona con dos [etiquetas de Azure Resource Manager](dns-zones-records.md#tags), *proyecto = demostración* y *env = test*:</span><span class="sxs-lookup"><span data-stu-id="ed9b7-114">hello following example shows how toocreate a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="ed9b7-115">Recuperación de una zona DNS</span><span class="sxs-lookup"><span data-stu-id="ed9b7-115">Get a DNS zone</span></span>

<span data-ttu-id="ed9b7-116">tooretrieve una zona DNS, usar hello `Get-AzureRmDnsZone` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ed9b7-116">tooretrieve a DNS zone, use hello `Get-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="ed9b7-117">Esta operación devuelve un DNS de la zona objeto tooan existente zona correspondiente en DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="ed9b7-117">This operation returns a DNS zone object corresponding tooan existing zone in Azure DNS.</span></span> <span data-ttu-id="ed9b7-118">Hello objeto contiene los datos sobre la zona de hello (por ejemplo, el número de Hola de conjuntos de registros), pero no contiene conjuntos de registros de Hola a sí mismos (consulte `Get-AzureRmDnsRecordSet`).</span><span class="sxs-lookup"><span data-stu-id="ed9b7-118">hello object contains data about hello zone (such as hello number of record sets), but does not contain hello record sets themselves (see `Get-AzureRmDnsRecordSet`).</span></span>

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

## <a name="list-dns-zones"></a><span data-ttu-id="ed9b7-119">Enumeración de zonas DNS</span><span class="sxs-lookup"><span data-stu-id="ed9b7-119">List DNS zones</span></span>

<span data-ttu-id="ed9b7-120">Si se omite el nombre de la zona de hello `Get-AzureRmDnsZone`, puede enumerar todas las zonas de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ed9b7-120">By omitting hello zone name from `Get-AzureRmDnsZone`, you can enumerate all zones in a resource group.</span></span> <span data-ttu-id="ed9b7-121">Esta operación devuelve una matriz de objetos de la zona.</span><span class="sxs-lookup"><span data-stu-id="ed9b7-121">This operation returns an array of zone objects.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="ed9b7-122">Si se omite el nombre de la zona de Hola y el nombre del grupo de recursos de hello `Get-AzureRmDnsZone`, puede enumerar todas las zonas de hello suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="ed9b7-122">By omitting both hello zone name and hello resource group name from `Get-AzureRmDnsZone`, you can enumerate all zones in hello Azure subscription.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="ed9b7-123">Actualización de una zona DNS</span><span class="sxs-lookup"><span data-stu-id="ed9b7-123">Update a DNS zone</span></span>

<span data-ttu-id="ed9b7-124">Cambia tooa recursos de la zona DNS pueden hacerse mediante `Set-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="ed9b7-124">Changes tooa DNS zone resource can be made by using `Set-AzureRmDnsZone`.</span></span> <span data-ttu-id="ed9b7-125">Este cmdlet no actualiza cualquiera de los conjuntos de registros de DNS de hello en la zona de hello (vea [cómo los registros DNS tooManage](dns-operations-recordsets.md)).</span><span class="sxs-lookup"><span data-stu-id="ed9b7-125">This cmdlet does not update any of hello DNS record sets within hello zone (see [How tooManage DNS records](dns-operations-recordsets.md)).</span></span> <span data-ttu-id="ed9b7-126">Solo ha utilizado propiedades tooupdate del propio recurso de zona Hola.</span><span class="sxs-lookup"><span data-stu-id="ed9b7-126">It's only used tooupdate properties of hello zone resource itself.</span></span> <span data-ttu-id="ed9b7-127">propiedades de la zona de escritura de Hello están limitada actualmente toohello [Azure Resource Manager 'etiqueta' para el recurso de la zona de hello](dns-zones-records.md#tags).</span><span class="sxs-lookup"><span data-stu-id="ed9b7-127">hello writable zone properties are currently limited toohello [Azure Resource Manager ‘tags’ for hello zone resource](dns-zones-records.md#tags).</span></span>

<span data-ttu-id="ed9b7-128">Use uno de hello después tooupdate de dos maneras una zona DNS:</span><span class="sxs-lookup"><span data-stu-id="ed9b7-128">Use one of hello following two ways tooupdate a DNS zone:</span></span>

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group"></a><span data-ttu-id="ed9b7-129">Especifique zona hello mediante el grupo de recursos y el nombre de la zona de Hola</span><span class="sxs-lookup"><span data-stu-id="ed9b7-129">Specify hello zone using hello zone name and resource group</span></span>

<span data-ttu-id="ed9b7-130">Este enfoque reemplaza las etiquetas existentes de zona Hola con valores de hello especificados.</span><span class="sxs-lookup"><span data-stu-id="ed9b7-130">This approach replaces hello existing zone tags with hello values specified.</span></span>

```powershell
Set-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

### <a name="specify-hello-zone-using-a-zone-object"></a><span data-ttu-id="ed9b7-131">Especificar la zona de hello mediante un objeto $zone</span><span class="sxs-lookup"><span data-stu-id="ed9b7-131">Specify hello zone using a $zone object</span></span>

<span data-ttu-id="ed9b7-132">Este método recupera el objeto existente de la zona de hello, modifica etiquetas de hello y, a continuación, confirme los cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed9b7-132">This approach retrieves hello existing zone object, modifies hello tags, and then commits hello changes.</span></span> <span data-ttu-id="ed9b7-133">De este modo, se pueden conservar las etiquetas existentes.</span><span class="sxs-lookup"><span data-stu-id="ed9b7-133">In this way, existing tags can be preserved.</span></span>

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

<span data-ttu-id="ed9b7-134">Cuando se usa `Set-AzureRmDnsZone` con un objeto $zone, [Etag comprueba](dns-zones-records.md#etags) sirven cambios simultáneos tooensure no se sobrescriben.</span><span class="sxs-lookup"><span data-stu-id="ed9b7-134">When using `Set-AzureRmDnsZone` with a $zone object, [Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="ed9b7-135">Puede usar Hola opcional `-Overwrite` cambiar toosuppress estas comprobaciones.</span><span class="sxs-lookup"><span data-stu-id="ed9b7-135">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

## <a name="delete-a-dns-zone"></a><span data-ttu-id="ed9b7-136">Eliminación de una zona DNS</span><span class="sxs-lookup"><span data-stu-id="ed9b7-136">Delete a DNS Zone</span></span>

<span data-ttu-id="ed9b7-137">Las zonas DNS pueden eliminarse con hello `Remove-AzureRmDnsZone` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ed9b7-137">DNS zones can be deleted using hello `Remove-AzureRmDnsZone` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="ed9b7-138">Al eliminar una zona DNS, también eliminan todos los registros DNS en la zona de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed9b7-138">Deleting a DNS zone also deletes all DNS records within hello zone.</span></span> <span data-ttu-id="ed9b7-139">Esta operación no se puede deshacer.</span><span class="sxs-lookup"><span data-stu-id="ed9b7-139">This operation cannot be undone.</span></span> <span data-ttu-id="ed9b7-140">Si la zona DNS Hola está en uso, se producirá un error en servicios con zona de hello cuando se elimina la zona de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed9b7-140">If hello DNS zone is in use, services using hello zone will fail when hello zone is deleted.</span></span>
>
><span data-ttu-id="ed9b7-141">tooprotect contra la eliminación accidental de zona, consulte [cómo tooprotect DNS zonas y registros](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="ed9b7-141">tooprotect against accidental zone deletion, see [How tooprotect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>


<span data-ttu-id="ed9b7-142">Use uno de hello después toodelete de dos maneras una zona DNS:</span><span class="sxs-lookup"><span data-stu-id="ed9b7-142">Use one of hello following two ways toodelete a DNS zone:</span></span>

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group-name"></a><span data-ttu-id="ed9b7-143">Especifique con el nombre de la zona de Hola y el nombre del grupo de recursos de zona de Hola</span><span class="sxs-lookup"><span data-stu-id="ed9b7-143">Specify hello zone using hello zone name and resource group name</span></span>

```powershell
Remove-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

### <a name="specify-hello-zone-using-a-zone-object"></a><span data-ttu-id="ed9b7-144">Especificar la zona de hello mediante un objeto $zone</span><span class="sxs-lookup"><span data-stu-id="ed9b7-144">Specify hello zone using a $zone object</span></span>

<span data-ttu-id="ed9b7-145">Puede especificar Hola zona toobe eliminado mediante una `$zone` objeto devuelto por `Get-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="ed9b7-145">You can specify hello zone toobe deleted using a `$zone` object returned by `Get-AzureRmDnsZone`.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
Remove-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="ed9b7-146">También se puede canalizar el objeto de la zona de Hello en lugar de que se pasa como parámetro:</span><span class="sxs-lookup"><span data-stu-id="ed9b7-146">hello zone object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup | Remove-AzureRmDnsZone

```

<span data-ttu-id="ed9b7-147">Al igual que con `Set-AzureRmDnsZone`, especificar Hola zona mediante una `$zone` habilita Etag comprueba los cambios simultáneos de tooensure no se eliminan del objeto.</span><span class="sxs-lookup"><span data-stu-id="ed9b7-147">As with `Set-AzureRmDnsZone`, specifying hello zone using a `$zone` object enables Etag checks tooensure concurrent changes are not deleted.</span></span> <span data-ttu-id="ed9b7-148">Hola de uso `-Overwrite` cambiar toosuppress estas comprobaciones.</span><span class="sxs-lookup"><span data-stu-id="ed9b7-148">Use hello `-Overwrite` switch toosuppress these checks.</span></span>

## <a name="confirmation-prompts"></a><span data-ttu-id="ed9b7-149">Mensajes de confirmación</span><span class="sxs-lookup"><span data-stu-id="ed9b7-149">Confirmation prompts</span></span>

<span data-ttu-id="ed9b7-150">Hola `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, y `Remove-AzureRmDnsZone` todos los cmdlets admiten mensajes de confirmación.</span><span class="sxs-lookup"><span data-stu-id="ed9b7-150">hello `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, and `Remove-AzureRmDnsZone` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="ed9b7-151">Ambos `New-AzureRmDnsZone` y `Set-AzureRmDnsZone` solicite confirmación si hello `$ConfirmPreference` variable de preferencia de PowerShell tiene un valor de `Medium` o inferior.</span><span class="sxs-lookup"><span data-stu-id="ed9b7-151">Both `New-AzureRmDnsZone` and `Set-AzureRmDnsZone` prompt for confirmation if hello `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="ed9b7-152">Pagar toohello potencialmente alto impacto de la eliminación de una zona DNS, hello `Remove-AzureRmDnsZone` cmdlet pide confirmación si hello `$ConfirmPreference` variable de PowerShell tiene cualquier valor distinto de `None`.</span><span class="sxs-lookup"><span data-stu-id="ed9b7-152">Due toohello potentially high impact of deleting a DNS zone, hello `Remove-AzureRmDnsZone` cmdlet prompts for confirmation if hello `$ConfirmPreference` PowerShell variable has any value other than `None`.</span></span>

<span data-ttu-id="ed9b7-153">Desde el valor predeterminado de Hola para `$ConfirmPreference` es `High`, solo `Remove-AzureRmDnsZone` pide confirmación de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="ed9b7-153">Since hello default value for `$ConfirmPreference` is `High`, only `Remove-AzureRmDnsZone` prompts for confirmation by default.</span></span>

<span data-ttu-id="ed9b7-154">Puede invalidar Hola actual `$ConfirmPreference` configuración mediante hello `-Confirm` parámetro.</span><span class="sxs-lookup"><span data-stu-id="ed9b7-154">You can override hello current `$ConfirmPreference` setting using hello `-Confirm` parameter.</span></span> <span data-ttu-id="ed9b7-155">Si especifica `-Confirm` o `-Confirm:$True` , Hola cmdlet solicita confirmación antes de que se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="ed9b7-155">If you specify `-Confirm` or `-Confirm:$True` , hello cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="ed9b7-156">Si especifica `-Confirm:$False` , Hola cmdlet no pide confirmación.</span><span class="sxs-lookup"><span data-stu-id="ed9b7-156">If you specify `-Confirm:$False` , hello cmdlet does not prompt you for confirmation.</span></span>

<span data-ttu-id="ed9b7-157">Para más información sobre `-Confirm` y `$ConfirmPreference`, consulte [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables) (Acerca de las variables de preferencias).</span><span class="sxs-lookup"><span data-stu-id="ed9b7-157">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed9b7-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ed9b7-158">Next steps</span></span>

<span data-ttu-id="ed9b7-159">Obtenga información acerca de cómo demasiado[administrar conjuntos de registros y registros](dns-operations-recordsets.md) en la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="ed9b7-159">Learn how too[manage record sets and records](dns-operations-recordsets.md) in your DNS zone.</span></span>
<br>
<span data-ttu-id="ed9b7-160">Obtenga información acerca de cómo demasiado[delegar su tooAzure de dominio DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="ed9b7-160">Learn how too[delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>
<br>
<span data-ttu-id="ed9b7-161">Hola de revisión [documentación de referencia de PowerShell de DNS de Azure](/powershell/module/azurerm.dns).</span><span class="sxs-lookup"><span data-stu-id="ed9b7-161">Review hello [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>

