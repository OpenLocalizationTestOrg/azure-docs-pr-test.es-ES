---
title: "Administración de zonas DNS en Azure DNS - PowerShell | Microsoft Docs"
description: "Puede administrar zonas DNS con Azure Powershell. Este artículo describe cómo actualizar, eliminar y crear zonas DNS en Azure DNS"
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
ms.openlocfilehash: 92f1da660d875c76d5d826669d6c1d12018c3d0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-dns-zones-using-powershell"></a><span data-ttu-id="b4d7a-104">Cómo administrar zonas DNS con PowerShell</span><span class="sxs-lookup"><span data-stu-id="b4d7a-104">How to manage DNS Zones using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b4d7a-105">Portal</span><span class="sxs-lookup"><span data-stu-id="b4d7a-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="b4d7a-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b4d7a-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="b4d7a-107">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="b4d7a-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="b4d7a-108">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="b4d7a-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="b4d7a-109">En este artículo se muestra cómo administrar sus zonas DNS mediante Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-109">This article shows you how to manage your DNS zones by using Azure PowerShell.</span></span> <span data-ttu-id="b4d7a-110">También se pueden administrar las zonas DNS mediante la [CLI de Azure](dns-operations-dnszones-cli.md) multiplataforma o Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-110">You can also manage your DNS zones using the cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or the Azure portal.</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)]


## <a name="create-a-dns-zone"></a><span data-ttu-id="b4d7a-111">Creación de una zona DNS</span><span class="sxs-lookup"><span data-stu-id="b4d7a-111">Create a DNS zone</span></span>

<span data-ttu-id="b4d7a-112">Una zona DNS se crea mediante el cmdlet `New-AzureRmDnsZone` .</span><span class="sxs-lookup"><span data-stu-id="b4d7a-112">A DNS zone is created by using the `New-AzureRmDnsZone` cmdlet.</span></span>

<span data-ttu-id="b4d7a-113">En el ejemplo siguiente, se crea una zona DNS llamada *contoso.com* en el grupo de recursos *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="b4d7a-113">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="b4d7a-114">En el ejemplo siguiente se muestra cómo crear una zona DNS con dos [etiquetas Azure Resource Manager](dns-zones-records.md#tags), *project = demo* y *env = test*:</span><span class="sxs-lookup"><span data-stu-id="b4d7a-114">The following example shows how to create a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="b4d7a-115">Recuperación de una zona DNS</span><span class="sxs-lookup"><span data-stu-id="b4d7a-115">Get a DNS zone</span></span>

<span data-ttu-id="b4d7a-116">Para recuperar una zona DNS, use el cmdlet `Get-AzureRmDnsZone` .</span><span class="sxs-lookup"><span data-stu-id="b4d7a-116">To retrieve a DNS zone, use the `Get-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="b4d7a-117">Esta operación devuelve un objeto de la zona DNS correspondiente a una zona existente en DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-117">This operation returns a DNS zone object corresponding to an existing zone in Azure DNS.</span></span> <span data-ttu-id="b4d7a-118">El objeto contiene datos sobre la zona (por ejemplo, el número de conjuntos de registros), pero no contiene los conjuntos de registros (vea `Get-AzureRmDnsRecordSet`).</span><span class="sxs-lookup"><span data-stu-id="b4d7a-118">The object contains data about the zone (such as the number of record sets), but does not contain the record sets themselves (see `Get-AzureRmDnsRecordSet`).</span></span>

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

## <a name="list-dns-zones"></a><span data-ttu-id="b4d7a-119">Enumeración de zonas DNS</span><span class="sxs-lookup"><span data-stu-id="b4d7a-119">List DNS zones</span></span>

<span data-ttu-id="b4d7a-120">Si se omite el nombre de la zona de `Get-AzureRmDnsZone`, puede enumerar todas las zonas en un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-120">By omitting the zone name from `Get-AzureRmDnsZone`, you can enumerate all zones in a resource group.</span></span> <span data-ttu-id="b4d7a-121">Esta operación devuelve una matriz de objetos de la zona.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-121">This operation returns an array of zone objects.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="b4d7a-122">Si se omite tanto el nombre de zona como el nombre del grupo de recursos de `Get-AzureRmDnsZone`, puede enumerar todas las zonas de la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-122">By omitting both the zone name and the resource group name from `Get-AzureRmDnsZone`, you can enumerate all zones in the Azure subscription.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="b4d7a-123">Actualización de una zona DNS</span><span class="sxs-lookup"><span data-stu-id="b4d7a-123">Update a DNS zone</span></span>

<span data-ttu-id="b4d7a-124">Los cambios en los recursos de una zona DNS se pueden realizar mediante `Set-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-124">Changes to a DNS zone resource can be made by using `Set-AzureRmDnsZone`.</span></span> <span data-ttu-id="b4d7a-125">Este cmdlet no actualiza ninguno de los conjuntos de registros de DNS de la zona (consulte [Administración de registros DNS](dns-operations-recordsets.md)).</span><span class="sxs-lookup"><span data-stu-id="b4d7a-125">This cmdlet does not update any of the DNS record sets within the zone (see [How to Manage DNS records](dns-operations-recordsets.md)).</span></span> <span data-ttu-id="b4d7a-126">Solo se utiliza para actualizar las propiedades de los recursos de la zona.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-126">It's only used to update properties of the zone resource itself.</span></span> <span data-ttu-id="b4d7a-127">Las propiedades de zona que se pueden escribir están actualmente limitadas a las ["etiquetas" Azure Resource Manager para el recurso de la zona](dns-zones-records.md#tags).</span><span class="sxs-lookup"><span data-stu-id="b4d7a-127">The writable zone properties are currently limited to the [Azure Resource Manager ‘tags’ for the zone resource](dns-zones-records.md#tags).</span></span>

<span data-ttu-id="b4d7a-128">Utilice una de las dos opciones siguientes para actualizar una zona DNS:</span><span class="sxs-lookup"><span data-stu-id="b4d7a-128">Use one of the following two ways to update a DNS zone:</span></span>

### <a name="specify-the-zone-using-the-zone-name-and-resource-group"></a><span data-ttu-id="b4d7a-129">Especificar la zona con la utilización del nombre de zona y el grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="b4d7a-129">Specify the zone using the zone name and resource group</span></span>

<span data-ttu-id="b4d7a-130">Este método reemplaza las etiquetas de zona existentes con los valores especificados.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-130">This approach replaces the existing zone tags with the values specified.</span></span>

```powershell
Set-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

### <a name="specify-the-zone-using-a-zone-object"></a><span data-ttu-id="b4d7a-131">Especificar la zona utilizando un objeto $zone</span><span class="sxs-lookup"><span data-stu-id="b4d7a-131">Specify the zone using a $zone object</span></span>

<span data-ttu-id="b4d7a-132">Este método recupera el objeto de zona existente, modifica las etiquetas y, a continuación, confirma los cambios.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-132">This approach retrieves the existing zone object, modifies the tags, and then commits the changes.</span></span> <span data-ttu-id="b4d7a-133">De este modo, se pueden conservar las etiquetas existentes.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-133">In this way, existing tags can be preserved.</span></span>

```powershell
# Get the zone object
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup

# Remove an existing tag
$zone.Tags.Remove("project")

# Add a new tag
$zone.Tags.Add("status","approved")

# Commit changes
Set-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="b4d7a-134">Al usar `Set-AzureRmDnsZone` con un objeto $zone, se utilizan las [comprobaciones de ETag](dns-zones-records.md#etags) para garantizar que no se sobrescriben los cambios simultáneos.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-134">When using `Set-AzureRmDnsZone` with a $zone object, [Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="b4d7a-135">Puede usar el modificador `-Overwrite` opcional para suprimir estas comprobaciones.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-135">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

## <a name="delete-a-dns-zone"></a><span data-ttu-id="b4d7a-136">Eliminación de una zona DNS</span><span class="sxs-lookup"><span data-stu-id="b4d7a-136">Delete a DNS Zone</span></span>

<span data-ttu-id="b4d7a-137">Las zonas DNS se pueden eliminar mediante el cmdlet `Remove-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-137">DNS zones can be deleted using the `Remove-AzureRmDnsZone` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="b4d7a-138">Si se elimina una zona DNS, también se eliminan todos los registros DNS dentro de la zona.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-138">Deleting a DNS zone also deletes all DNS records within the zone.</span></span> <span data-ttu-id="b4d7a-139">Esta operación no se puede deshacer.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-139">This operation cannot be undone.</span></span> <span data-ttu-id="b4d7a-140">Si la zona DNS está en uso, los servicios con la zona provocarán un error cuando se elimina la zona.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-140">If the DNS zone is in use, services using the zone will fail when the zone is deleted.</span></span>
>
><span data-ttu-id="b4d7a-141">Para protegerse contra la eliminación accidental de zona, consulte [Proteger registros y zonas DNS](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="b4d7a-141">To protect against accidental zone deletion, see [How to protect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>


<span data-ttu-id="b4d7a-142">Utilice una de las dos opciones siguientes para eliminar una zona DNS:</span><span class="sxs-lookup"><span data-stu-id="b4d7a-142">Use one of the following two ways to delete a DNS zone:</span></span>

### <a name="specify-the-zone-using-the-zone-name-and-resource-group-name"></a><span data-ttu-id="b4d7a-143">Especificar la zona con la utilización del nombre de zona y el nombre del grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="b4d7a-143">Specify the zone using the zone name and resource group name</span></span>

```powershell
Remove-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

### <a name="specify-the-zone-using-a-zone-object"></a><span data-ttu-id="b4d7a-144">Especificar la zona utilizando un objeto $zone</span><span class="sxs-lookup"><span data-stu-id="b4d7a-144">Specify the zone using a $zone object</span></span>

<span data-ttu-id="b4d7a-145">Puede especificar la zona que desee eliminar mediante un objeto `$zone` devuelto por `Get-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-145">You can specify the zone to be deleted using a `$zone` object returned by `Get-AzureRmDnsZone`.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
Remove-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="b4d7a-146">También se puede canalizar el objeto de la zona en lugar de pasarlo como parámetro:</span><span class="sxs-lookup"><span data-stu-id="b4d7a-146">The zone object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup | Remove-AzureRmDnsZone

```

<span data-ttu-id="b4d7a-147">Como con `Set-AzureRmDnsZone`, especificar la zona utilizando un objeto `$zone` permite realizar las comprobaciones de ETag para asegurarse de que no se eliminan los cambios simultáneos.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-147">As with `Set-AzureRmDnsZone`, specifying the zone using a `$zone` object enables Etag checks to ensure concurrent changes are not deleted.</span></span> <span data-ttu-id="b4d7a-148">Use el modificador `-Overwrite` para suprimir estas comprobaciones.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-148">Use the `-Overwrite` switch to suppress these checks.</span></span>

## <a name="confirmation-prompts"></a><span data-ttu-id="b4d7a-149">Mensajes de confirmación</span><span class="sxs-lookup"><span data-stu-id="b4d7a-149">Confirmation prompts</span></span>

<span data-ttu-id="b4d7a-150">Los cmdlets `New-AzureRmDnsZone`, `Set-AzureRmDnsZone` y `Remove-AzureRmDnsZone` todos admiten mensajes de confirmación.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-150">The `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, and `Remove-AzureRmDnsZone` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="b4d7a-151">Ambos `New-AzureRmDnsZone` y `Set-AzureRmDnsZone` piden confirmación si la variable de preferencia de PowerShell `$ConfirmPreference` tiene un valor de `Medium` o inferior.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-151">Both `New-AzureRmDnsZone` and `Set-AzureRmDnsZone` prompt for confirmation if the `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="b4d7a-152">Debido al impacto potencialmente alto que puede tener la eliminación de una zona DNS, el cmdlet `Remove-AzureRmDnsZone` pide confirmación si la variable de PowerShell `$ConfirmPreference` tiene cualquier valor distinto de `None`.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-152">Due to the potentially high impact of deleting a DNS zone, the `Remove-AzureRmDnsZone` cmdlet prompts for confirmation if the `$ConfirmPreference` PowerShell variable has any value other than `None`.</span></span>

<span data-ttu-id="b4d7a-153">Puesto que el valor predeterminado para `$ConfirmPreference` es `High`, solo `Remove-AzureRmDnsZone` pide confirmación de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-153">Since the default value for `$ConfirmPreference` is `High`, only `Remove-AzureRmDnsZone` prompts for confirmation by default.</span></span>

<span data-ttu-id="b4d7a-154">Puede invalidar el valor actual de `$ConfirmPreference` mediante el parámetro `-Confirm`.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-154">You can override the current `$ConfirmPreference` setting using the `-Confirm` parameter.</span></span> <span data-ttu-id="b4d7a-155">Si especifica `-Confirm` o `-Confirm:$True`, el cmdlet solicita confirmación antes de ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-155">If you specify `-Confirm` or `-Confirm:$True` , the cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="b4d7a-156">Si especifica `-Confirm:$False`, el cmdlet no solicita confirmación.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-156">If you specify `-Confirm:$False` , the cmdlet does not prompt you for confirmation.</span></span>

<span data-ttu-id="b4d7a-157">Para más información sobre `-Confirm` y `$ConfirmPreference`, consulte [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables) (Acerca de las variables de preferencias).</span><span class="sxs-lookup"><span data-stu-id="b4d7a-157">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4d7a-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b4d7a-158">Next steps</span></span>

<span data-ttu-id="b4d7a-159">En esta guía se explica cómo [administrar conjuntos de registros y registros](dns-operations-recordsets.md) en la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="b4d7a-159">Learn how to [manage record sets and records](dns-operations-recordsets.md) in your DNS zone.</span></span>
<br>
<span data-ttu-id="b4d7a-160">Aprenda a cómo [delegar el dominio a Azure DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="b4d7a-160">Learn how to [delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>
<br>
<span data-ttu-id="b4d7a-161">Revise la [documentación de referencia de PowerShell para Azure DNS](/powershell/module/azurerm.dns).</span><span class="sxs-lookup"><span data-stu-id="b4d7a-161">Review the [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>

