---
title: "Administración de zonas DNS en Azure DNS (CLI de Azure 1.0) | Microsoft Docs"
description: "Puede administrar zonas DNS con la CLI de Azure 1.0. Este artículo muestra cómo actualizar, eliminar y crear zonas DNS en Azure DNS."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: 588c87749f049eff5b9e0729f6769c8367ba41e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-dns-zones-in-azure-dns-using-the-azure-cli-10"></a><span data-ttu-id="e90fd-104">Cómo administrar zonas DNS en Azure DNS con la CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="e90fd-104">How to manage DNS Zones in Azure DNS using the Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e90fd-105">Portal</span><span class="sxs-lookup"><span data-stu-id="e90fd-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="e90fd-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e90fd-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="e90fd-107">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="e90fd-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="e90fd-108">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="e90fd-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="e90fd-109">Esta guía muestra cómo administrar las zonas DNS mediante la CLI de Azure 1.0 multiplataforma, que está disponible para Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="e90fd-109">This guide shows how to manage your DNS zones by using the cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="e90fd-110">También puede administrar sus zonas DNS mediante [Azure PowerShell](dns-operations-dnszones.md) o Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e90fd-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or the Azure portal.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="e90fd-111">Versiones de la CLI para completar la tarea</span><span class="sxs-lookup"><span data-stu-id="e90fd-111">CLI versions to complete the task</span></span>

<span data-ttu-id="e90fd-112">Puede completar la tarea mediante una de las siguientes versiones de la CLI:</span><span class="sxs-lookup"><span data-stu-id="e90fd-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="e90fd-113">[CLI de Azure 1.0](dns-operations-dnszones-cli-nodejs.md): la CLI para los modelos de implementación clásica y de administración de recursos.</span><span class="sxs-lookup"><span data-stu-id="e90fd-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="e90fd-114">[CLI de Azure 2.0](dns-operations-dnszones-cli.md): la CLI de última generación para el modelo de implementación de administración de recursos.</span><span class="sxs-lookup"><span data-stu-id="e90fd-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for the resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="e90fd-115">Introducción</span><span class="sxs-lookup"><span data-stu-id="e90fd-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-cli-setup](../../includes/dns-cli-setup-include.md)]

## <a name="getting-help"></a><span data-ttu-id="e90fd-116">Ayuda</span><span class="sxs-lookup"><span data-stu-id="e90fd-116">Getting help</span></span>

<span data-ttu-id="e90fd-117">Todos los comandos de la CLI 1.0 relacionados con Azure DNS comienzan por `azure network dns`.</span><span class="sxs-lookup"><span data-stu-id="e90fd-117">All CLI 1.0 commands relating to Azure DNS start with `azure network dns`.</span></span> <span data-ttu-id="e90fd-118">La ayuda está disponible para cada comando con la opción `--help` (formato abreviado `-h`).</span><span class="sxs-lookup"><span data-stu-id="e90fd-118">Help is available for each command using the `--help` option (short form `-h`).</span></span>  <span data-ttu-id="e90fd-119">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e90fd-119">For example:</span></span>

```azurecli
azure network dns -h
azure network dns zone -h
azure network dns zone create -h
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="e90fd-120">Creación de una zona DNS</span><span class="sxs-lookup"><span data-stu-id="e90fd-120">Create a DNS zone</span></span>

<span data-ttu-id="e90fd-121">Una zona DNS se crea con el comando `azure network dns zone create` .</span><span class="sxs-lookup"><span data-stu-id="e90fd-121">A DNS zone is created using the `azure network dns zone create` command.</span></span> <span data-ttu-id="e90fd-122">Para obtener ayuda, consulte `azure network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="e90fd-122">For help, see `azure network dns zone create -h`.</span></span>

<span data-ttu-id="e90fd-123">En el ejemplo siguiente, se crea una zona DNS llamada *contoso.com* en el grupo de recursos *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="e90fd-123">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*:</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```

### <a name="to-create-a-dns-zone-with-tags"></a><span data-ttu-id="e90fd-124">Para crear una zona DNS con etiquetas.</span><span class="sxs-lookup"><span data-stu-id="e90fd-124">To create a DNS zone with tags</span></span>

<span data-ttu-id="e90fd-125">En el ejemplo siguiente se muestra cómo crear una zona DNS con dos [etiquetas de Azure Resource Manager](dns-zones-records.md#tags), *project = demo* y *env = test*, con el parámetro `--tags` (forma abreviada `-t`):</span><span class="sxs-lookup"><span data-stu-id="e90fd-125">The following example shows how to create a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using the `--tags` parameter (short form `-t`):</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com -t "project=demo";"env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="e90fd-126">Recuperación de una zona DNS</span><span class="sxs-lookup"><span data-stu-id="e90fd-126">Get a DNS zone</span></span>

<span data-ttu-id="e90fd-127">Para recuperar una zona DNS, use `azure network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="e90fd-127">To retrieve a DNS zone, use `azure network dns zone show`.</span></span> <span data-ttu-id="e90fd-128">Para obtener ayuda, consulte `azure network dns zone show -h`.</span><span class="sxs-lookup"><span data-stu-id="e90fd-128">For help, see `azure network dns zone show -h`.</span></span>

<span data-ttu-id="e90fd-129">El ejemplo siguiente devuelve la zona DNS *contoso.com* y sus datos asociados del grupo de recursos *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="e90fd-129">The following example returns the DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
azure network dns zone show MyResourceGroup contoso.com
```

<span data-ttu-id="e90fd-130">El ejemplo siguiente es la respuesta.</span><span class="sxs-lookup"><span data-stu-id="e90fd-130">The following example is the response.</span></span>

```
info:    Executing command network dns zone show
+ Looking up the dns zone "contoso.com"
data:    Id                              : /subscriptions/.../contoso.com
data:    Name                            : contoso.com
data:    Type                            : Microsoft.Network/dnszones
data:    Location                        : global
data:    Number of record sets           : 2
data:    Max number of record sets       : 5000
data:    Name servers:
data:        ns1-01.azure-dns.com.
data:        ns2-01.azure-dns.net.
data:        ns3-01.azure-dns.org.
data:        ns4-01.azure-dns.info.
data:    Tags                            : project=demo;env=test
info:    network dns zone show command OK
```

<span data-ttu-id="e90fd-131">Tenga en cuenta que `azure network dns zone show` no devuelve los registros DNS.</span><span class="sxs-lookup"><span data-stu-id="e90fd-131">Note that DNS records are not returned by `azure network dns zone show`.</span></span> <span data-ttu-id="e90fd-132">Para enumerar los registros DNS, utilice `azure network dns record-set list`.</span><span class="sxs-lookup"><span data-stu-id="e90fd-132">To list DNS records, use `azure network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="e90fd-133">Enumeración de zonas DNS</span><span class="sxs-lookup"><span data-stu-id="e90fd-133">List DNS zones</span></span>

<span data-ttu-id="e90fd-134">Para enumerar las zonas DNS, utilice `azure network dns zone list`.</span><span class="sxs-lookup"><span data-stu-id="e90fd-134">To enumerate DNS zones, use `azure network dns zone list`.</span></span> <span data-ttu-id="e90fd-135">Para obtener ayuda, consulte `azure network dns zone list -h`.</span><span class="sxs-lookup"><span data-stu-id="e90fd-135">For help, see `azure network dns zone list -h`.</span></span>

<span data-ttu-id="e90fd-136">Si se especifica el grupo de recursos, se enumeran solo esas zonas dentro del grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="e90fd-136">Specifying the resource group lists only those zones within the resource group:</span></span>

```azurecli
azure network dns zone list MyResourceGroup
```

<span data-ttu-id="e90fd-137">Si se omite el grupo de recursos, se enumeran todas las zonas en la suscripción:</span><span class="sxs-lookup"><span data-stu-id="e90fd-137">Omitting the resource group lists all zones in the subscription:</span></span>

```azurecli
azure network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="e90fd-138">Actualización de una zona DNS</span><span class="sxs-lookup"><span data-stu-id="e90fd-138">Update a DNS zone</span></span>

<span data-ttu-id="e90fd-139">Los cambios en los recursos de una zona DNS se pueden realizar con `azure network dns zone set`.</span><span class="sxs-lookup"><span data-stu-id="e90fd-139">Changes to a DNS zone resource can be made using `azure network dns zone set`.</span></span> <span data-ttu-id="e90fd-140">Para obtener ayuda, consulte `azure network dns zone set -h`.</span><span class="sxs-lookup"><span data-stu-id="e90fd-140">For help, see `azure network dns zone set -h`.</span></span>

<span data-ttu-id="e90fd-141">Este comando no actualiza los conjuntos de registros DNS de la zona (consulte [Administración de registros DNS](dns-operations-recordsets-cli-nodejs.md)).</span><span class="sxs-lookup"><span data-stu-id="e90fd-141">This command does not update any of the DNS record sets within the zone (see [How to Manage DNS records](dns-operations-recordsets-cli-nodejs.md)).</span></span> <span data-ttu-id="e90fd-142">Solo se utiliza para actualizar las propiedades de los recursos de la zona.</span><span class="sxs-lookup"><span data-stu-id="e90fd-142">It is only used to update properties of the zone resource itself.</span></span> <span data-ttu-id="e90fd-143">Estas propiedades están actualmente limitadas a las ["etiquetas" Azure Resource Manager ](dns-zones-records.md#tags) para los recursos de la zona.</span><span class="sxs-lookup"><span data-stu-id="e90fd-143">These properties are currently limited to the [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for the zone resource.</span></span>

<span data-ttu-id="e90fd-144">En el ejemplo siguiente se muestra cómo actualizar las etiquetas en una zona DNS.</span><span class="sxs-lookup"><span data-stu-id="e90fd-144">The following example shows how to update the tags on a DNS zone.</span></span> <span data-ttu-id="e90fd-145">Las etiquetas existentes se reemplazan por el valor especificado.</span><span class="sxs-lookup"><span data-stu-id="e90fd-145">The existing tags are replaced by the value specified.</span></span>

```azurecli
azure network dns zone set MyResourceGroup contoso.com -t "team=support"
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="e90fd-146">Eliminación de una zona DNS</span><span class="sxs-lookup"><span data-stu-id="e90fd-146">Delete a DNS Zone</span></span>

<span data-ttu-id="e90fd-147">Las zonas DNS se pueden eliminar mediante `azure network dns zone delete`.</span><span class="sxs-lookup"><span data-stu-id="e90fd-147">DNS zones can be deleted using `azure network dns zone delete`.</span></span> <span data-ttu-id="e90fd-148">Para obtener ayuda, consulte `azure network dns zone delete -h`.</span><span class="sxs-lookup"><span data-stu-id="e90fd-148">For help, see `azure network dns zone delete -h`.</span></span>

> [!NOTE]
> <span data-ttu-id="e90fd-149">Si se elimina una zona DNS, también se eliminan todos los registros DNS dentro de la zona.</span><span class="sxs-lookup"><span data-stu-id="e90fd-149">Deleting a DNS zone also deletes all DNS records within the zone.</span></span> <span data-ttu-id="e90fd-150">Esta operación no se puede deshacer.</span><span class="sxs-lookup"><span data-stu-id="e90fd-150">This operation cannot be undone.</span></span> <span data-ttu-id="e90fd-151">Si la zona DNS está en uso, los servicios con la zona provocarán un error cuando se elimina la zona.</span><span class="sxs-lookup"><span data-stu-id="e90fd-151">If the DNS zone is in use, services using the zone will fail when the zone is deleted.</span></span>
>
><span data-ttu-id="e90fd-152">Para protegerse contra la eliminación accidental de zona, consulte [Proteger registros y zonas DNS](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="e90fd-152">To protect against accidental zone deletion, see [How to protect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="e90fd-153">Este comando solicita confirmación.</span><span class="sxs-lookup"><span data-stu-id="e90fd-153">This command prompts for confirmation.</span></span> <span data-ttu-id="e90fd-154">El conmutador `--quiet` opcional (forma abreviada `-q`) elimina esta confirmación.</span><span class="sxs-lookup"><span data-stu-id="e90fd-154">The optional `--quiet` switch (short form `-q`) suppresses this prompt.</span></span>

<span data-ttu-id="e90fd-155">En el ejemplo siguiente se muestra cómo eliminar la zona *contoso.com* del grupo de recursos *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="e90fd-155">The following example shows how to delete the zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
azure network dns zone delete MyResourceGroup contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="e90fd-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e90fd-156">Next steps</span></span>

<span data-ttu-id="e90fd-157">En esta guía se explica cómo [administrar conjuntos de registros y registros](dns-getstarted-create-recordset-cli-nodejs.md) en la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="e90fd-157">Learn how to [manage record sets and records](dns-getstarted-create-recordset-cli-nodejs.md) in your DNS zone.</span></span>

<span data-ttu-id="e90fd-158">Aprenda a cómo [delegar el dominio a Azure DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="e90fd-158">Learn how to [delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

