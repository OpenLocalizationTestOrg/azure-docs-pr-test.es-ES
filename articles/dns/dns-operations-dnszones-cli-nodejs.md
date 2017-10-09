---
title: aaaManage DNS zonas en DNS de Azure - 1.0 de CLI de Azure | Documentos de Microsoft
description: "Puede administrar zonas DNS con la CLI de Azure 1.0. Este artículo muestra cómo tooupdate, eliminar y crear las zonas DNS en el DNS de Azure."
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
ms.openlocfilehash: cb9790cc46626ef7f38a43edb57511104fe6057e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-10"></a><span data-ttu-id="b988d-104">¿Cómo toomanage zonas de DNS de DNS de Azure utilizando Hola 1.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="b988d-104">How toomanage DNS Zones in Azure DNS using hello Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b988d-105">Portal</span><span class="sxs-lookup"><span data-stu-id="b988d-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="b988d-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b988d-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="b988d-107">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="b988d-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="b988d-108">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="b988d-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="b988d-109">Esta guía le mostrará cómo toomanage su DNS zonas mediante el uso de hello multiplataforma CLI de Azure 1.0, que está disponible para Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="b988d-109">This guide shows how toomanage your DNS zones by using hello cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="b988d-110">También puede administrar las zonas DNS mediante [Azure PowerShell](dns-operations-dnszones.md) u Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b988d-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or hello Azure portal.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="b988d-111">Tarea CLI versiones toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="b988d-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="b988d-112">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="b988d-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="b988d-113">[Azure 1.0 de CLI](dns-operations-dnszones-cli-nodejs.md) -nuestro CLI para modelos de implementación de administración de recursos y clásico Hola.</span><span class="sxs-lookup"><span data-stu-id="b988d-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="b988d-114">[Azure 2.0 CLI](dns-operations-dnszones-cli.md) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b988d-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for hello resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="b988d-115">Introducción</span><span class="sxs-lookup"><span data-stu-id="b988d-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-cli-setup](../../includes/dns-cli-setup-include.md)]

## <a name="getting-help"></a><span data-ttu-id="b988d-116">Ayuda</span><span class="sxs-lookup"><span data-stu-id="b988d-116">Getting help</span></span>

<span data-ttu-id="b988d-117">Inician todos los comandos de CLI 1.0 relativas tooAzure DNS con `azure network dns`.</span><span class="sxs-lookup"><span data-stu-id="b988d-117">All CLI 1.0 commands relating tooAzure DNS start with `azure network dns`.</span></span> <span data-ttu-id="b988d-118">La Ayuda está disponible para cada comando con hello `--help` opción (forma abreviada `-h`).</span><span class="sxs-lookup"><span data-stu-id="b988d-118">Help is available for each command using hello `--help` option (short form `-h`).</span></span>  <span data-ttu-id="b988d-119">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b988d-119">For example:</span></span>

```azurecli
azure network dns -h
azure network dns zone -h
azure network dns zone create -h
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="b988d-120">Creación de una zona DNS</span><span class="sxs-lookup"><span data-stu-id="b988d-120">Create a DNS zone</span></span>

<span data-ttu-id="b988d-121">Se crea una zona DNS con hello `azure network dns zone create` comando.</span><span class="sxs-lookup"><span data-stu-id="b988d-121">A DNS zone is created using hello `azure network dns zone create` command.</span></span> <span data-ttu-id="b988d-122">Para obtener ayuda, consulte `azure network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="b988d-122">For help, see `azure network dns zone create -h`.</span></span>

<span data-ttu-id="b988d-123">Hello en el ejemplo siguiente se crea una zona DNS denominada *contoso.com* en grupo de recursos de hello denominado *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="b988d-123">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*:</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a><span data-ttu-id="b988d-124">toocreate una zona DNS con etiquetas</span><span class="sxs-lookup"><span data-stu-id="b988d-124">toocreate a DNS zone with tags</span></span>

<span data-ttu-id="b988d-125">Hello en el ejemplo siguiente se muestra cómo toocreate un DNS de la zona con dos [etiquetas de Azure Resource Manager](dns-zones-records.md#tags), *proyecto = demostración* y *env = test*, mediante el uso de hello `--tags` parámetro (forma abreviada `-t`):</span><span class="sxs-lookup"><span data-stu-id="b988d-125">hello following example shows how toocreate a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using hello `--tags` parameter (short form `-t`):</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com -t "project=demo";"env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="b988d-126">Recuperación de una zona DNS</span><span class="sxs-lookup"><span data-stu-id="b988d-126">Get a DNS zone</span></span>

<span data-ttu-id="b988d-127">tooretrieve una zona DNS, use `azure network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="b988d-127">tooretrieve a DNS zone, use `azure network dns zone show`.</span></span> <span data-ttu-id="b988d-128">Para obtener ayuda, consulte `azure network dns zone show -h`.</span><span class="sxs-lookup"><span data-stu-id="b988d-128">For help, see `azure network dns zone show -h`.</span></span>

<span data-ttu-id="b988d-129">Hello en el ejemplo siguiente se devuelve la zona DNS hello *contoso.com* y sus datos asociados del grupo de recursos *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="b988d-129">hello following example returns hello DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
azure network dns zone show MyResourceGroup contoso.com
```

<span data-ttu-id="b988d-130">Hola siguiente ejemplo es la respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="b988d-130">hello following example is hello response.</span></span>

```
info:    Executing command network dns zone show
+ Looking up hello dns zone "contoso.com"
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

<span data-ttu-id="b988d-131">Tenga en cuenta que `azure network dns zone show` no devuelve los registros DNS.</span><span class="sxs-lookup"><span data-stu-id="b988d-131">Note that DNS records are not returned by `azure network dns zone show`.</span></span> <span data-ttu-id="b988d-132">usar los registros DNS toolist, `azure network dns record-set list`.</span><span class="sxs-lookup"><span data-stu-id="b988d-132">toolist DNS records, use `azure network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="b988d-133">Enumeración de zonas DNS</span><span class="sxs-lookup"><span data-stu-id="b988d-133">List DNS zones</span></span>

<span data-ttu-id="b988d-134">las zonas DNS tooenumerate, utilizar `azure network dns zone list`.</span><span class="sxs-lookup"><span data-stu-id="b988d-134">tooenumerate DNS zones, use `azure network dns zone list`.</span></span> <span data-ttu-id="b988d-135">Para obtener ayuda, consulte `azure network dns zone list -h`.</span><span class="sxs-lookup"><span data-stu-id="b988d-135">For help, see `azure network dns zone list -h`.</span></span>

<span data-ttu-id="b988d-136">Grupo de recursos de hello especificando muestra solo las zonas en el grupo de recursos de hello:</span><span class="sxs-lookup"><span data-stu-id="b988d-136">Specifying hello resource group lists only those zones within hello resource group:</span></span>

```azurecli
azure network dns zone list MyResourceGroup
```

<span data-ttu-id="b988d-137">Si se omite el grupo de recursos de hello enumera todas las zonas de suscripción de hello:</span><span class="sxs-lookup"><span data-stu-id="b988d-137">Omitting hello resource group lists all zones in hello subscription:</span></span>

```azurecli
azure network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="b988d-138">Actualización de una zona DNS</span><span class="sxs-lookup"><span data-stu-id="b988d-138">Update a DNS zone</span></span>

<span data-ttu-id="b988d-139">Tooa cambios recursos de zona DNS pueden realizarse con `azure network dns zone set`.</span><span class="sxs-lookup"><span data-stu-id="b988d-139">Changes tooa DNS zone resource can be made using `azure network dns zone set`.</span></span> <span data-ttu-id="b988d-140">Para obtener ayuda, consulte `azure network dns zone set -h`.</span><span class="sxs-lookup"><span data-stu-id="b988d-140">For help, see `azure network dns zone set -h`.</span></span>

<span data-ttu-id="b988d-141">Este comando no actualiza cualquiera de los conjuntos de registros de DNS de hello en la zona de hello (vea [cómo los registros DNS tooManage](dns-operations-recordsets-cli-nodejs.md)).</span><span class="sxs-lookup"><span data-stu-id="b988d-141">This command does not update any of hello DNS record sets within hello zone (see [How tooManage DNS records](dns-operations-recordsets-cli-nodejs.md)).</span></span> <span data-ttu-id="b988d-142">Es solo tooupdate usa propiedades del propio recurso de zona Hola.</span><span class="sxs-lookup"><span data-stu-id="b988d-142">It is only used tooupdate properties of hello zone resource itself.</span></span> <span data-ttu-id="b988d-143">Estas propiedades están limitada actualmente toohello [Azure Resource Manager «etiquetas»](dns-zones-records.md#tags) para recursos de la zona de Hola.</span><span class="sxs-lookup"><span data-stu-id="b988d-143">These properties are currently limited toohello [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for hello zone resource.</span></span>

<span data-ttu-id="b988d-144">Hello en el ejemplo siguiente se muestra cómo tooupdate Hola etiquetas en una zona DNS.</span><span class="sxs-lookup"><span data-stu-id="b988d-144">hello following example shows how tooupdate hello tags on a DNS zone.</span></span> <span data-ttu-id="b988d-145">las etiquetas existentes Hola se reemplazan por valor de hello especificado.</span><span class="sxs-lookup"><span data-stu-id="b988d-145">hello existing tags are replaced by hello value specified.</span></span>

```azurecli
azure network dns zone set MyResourceGroup contoso.com -t "team=support"
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="b988d-146">Eliminación de una zona DNS</span><span class="sxs-lookup"><span data-stu-id="b988d-146">Delete a DNS Zone</span></span>

<span data-ttu-id="b988d-147">Las zonas DNS se pueden eliminar mediante `azure network dns zone delete`.</span><span class="sxs-lookup"><span data-stu-id="b988d-147">DNS zones can be deleted using `azure network dns zone delete`.</span></span> <span data-ttu-id="b988d-148">Para obtener ayuda, consulte `azure network dns zone delete -h`.</span><span class="sxs-lookup"><span data-stu-id="b988d-148">For help, see `azure network dns zone delete -h`.</span></span>

> [!NOTE]
> <span data-ttu-id="b988d-149">Al eliminar una zona DNS, también eliminan todos los registros DNS en la zona de Hola.</span><span class="sxs-lookup"><span data-stu-id="b988d-149">Deleting a DNS zone also deletes all DNS records within hello zone.</span></span> <span data-ttu-id="b988d-150">Esta operación no se puede deshacer.</span><span class="sxs-lookup"><span data-stu-id="b988d-150">This operation cannot be undone.</span></span> <span data-ttu-id="b988d-151">Si la zona DNS Hola está en uso, se producirá un error en servicios con zona de hello cuando se elimina la zona de Hola.</span><span class="sxs-lookup"><span data-stu-id="b988d-151">If hello DNS zone is in use, services using hello zone will fail when hello zone is deleted.</span></span>
>
><span data-ttu-id="b988d-152">tooprotect contra la eliminación accidental de zona, consulte [cómo tooprotect DNS zonas y registros](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="b988d-152">tooprotect against accidental zone deletion, see [How tooprotect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="b988d-153">Este comando solicita confirmación.</span><span class="sxs-lookup"><span data-stu-id="b988d-153">This command prompts for confirmation.</span></span> <span data-ttu-id="b988d-154">Hola opcional `--quiet` cambiar (forma abreviada `-q`) no se muestre este mensaje.</span><span class="sxs-lookup"><span data-stu-id="b988d-154">hello optional `--quiet` switch (short form `-q`) suppresses this prompt.</span></span>

<span data-ttu-id="b988d-155">Hello en el ejemplo siguiente se muestra cómo toodelete Hola zona *contoso.com* del grupo de recursos *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="b988d-155">hello following example shows how toodelete hello zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
azure network dns zone delete MyResourceGroup contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="b988d-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b988d-156">Next steps</span></span>

<span data-ttu-id="b988d-157">Obtenga información acerca de cómo demasiado[administrar conjuntos de registros y registros](dns-getstarted-create-recordset-cli-nodejs.md) en la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="b988d-157">Learn how too[manage record sets and records](dns-getstarted-create-recordset-cli-nodejs.md) in your DNS zone.</span></span>

<span data-ttu-id="b988d-158">Obtenga información acerca de cómo demasiado[delegar su tooAzure de dominio DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="b988d-158">Learn how too[delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

