---
title: aaaManage DNS zonas en DNS de Azure - 2.0 de CLI de Azure | Documentos de Microsoft
description: "Puede administrar zonas DNS con la CLI de Azure 2.0. Este artículo muestra cómo tooupdate, eliminar y crear las zonas DNS en el DNS de Azure."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: gwallace
ms.openlocfilehash: 3945a558b2db3490e50678d8395a47e55a85c8fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-20"></a><span data-ttu-id="58197-104">¿Cómo toomanage zonas de DNS de DNS de Azure utilizando Hola 2.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="58197-104">How toomanage DNS Zones in Azure DNS using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="58197-105">Portal</span><span class="sxs-lookup"><span data-stu-id="58197-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="58197-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="58197-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="58197-107">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="58197-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="58197-108">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="58197-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)


<span data-ttu-id="58197-109">Esta guía le mostrará cómo toomanage su DNS zonas mediante el uso de hello multiplataforma CLI de Azure, que está disponible para Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="58197-109">This guide shows how toomanage your DNS zones by using hello cross-platform Azure CLI, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="58197-110">También puede administrar las zonas DNS mediante [Azure PowerShell](dns-operations-dnszones.md) u Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="58197-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or hello Azure portal.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="58197-111">Tarea CLI versiones toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="58197-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="58197-112">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="58197-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="58197-113">[Azure 1.0 de CLI](dns-operations-dnszones-cli-nodejs.md) -nuestro CLI para modelos de implementación de administración de recursos y clásico Hola.</span><span class="sxs-lookup"><span data-stu-id="58197-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="58197-114">[Azure 2.0 CLI](dns-operations-dnszones-cli.md) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="58197-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for hello resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="58197-115">Introducción</span><span class="sxs-lookup"><span data-stu-id="58197-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-20-for-azure-dns"></a><span data-ttu-id="58197-116">Configuración de la CLI de Azure 2.0 para Azure DNS</span><span class="sxs-lookup"><span data-stu-id="58197-116">Set up Azure CLI 2.0 for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="58197-117">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="58197-117">Before you begin</span></span>

<span data-ttu-id="58197-118">Compruebe que dispone de hello siguientes elementos antes de comenzar la configuración.</span><span class="sxs-lookup"><span data-stu-id="58197-118">Verify that you have hello following items before beginning your configuration.</span></span>

* <span data-ttu-id="58197-119">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="58197-119">An Azure subscription.</span></span> <span data-ttu-id="58197-120">Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) o registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="58197-120">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="58197-121">Instale Hola la versión más reciente de hello CLI de Azure 2.0, disponible para Windows, Linux o Mac.</span><span class="sxs-lookup"><span data-stu-id="58197-121">Install hello latest version of hello Azure CLI 2.0, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="58197-122">Hay disponible más información en [Install hello Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="58197-122">More information is available at [Install hello Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

### <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="58197-123">Inicie sesión en tooyour cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="58197-123">Sign in tooyour Azure account</span></span>

<span data-ttu-id="58197-124">Abra una ventana de consola y autentíquese con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="58197-124">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="58197-125">Para obtener más información, consulte el registro en tooAzure de hello CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="58197-125">For more information, see Log in tooAzure from hello Azure CLI</span></span>

```
az login
```

### <a name="select-hello-subscription"></a><span data-ttu-id="58197-126">Seleccione la suscripción de Hola</span><span class="sxs-lookup"><span data-stu-id="58197-126">Select hello subscription</span></span>

<span data-ttu-id="58197-127">Compruebe las suscripciones de hello para la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="58197-127">Check hello subscriptions for hello account.</span></span>

```
az account list
```

<span data-ttu-id="58197-128">Elija qué su toouse de las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="58197-128">Choose which of your Azure subscriptions toouse.</span></span>

```azurecli
az account set --subscription "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="58197-129">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="58197-129">Create a resource group</span></span>

<span data-ttu-id="58197-130">Azure Resource Manager requiere que todos los grupos de recursos especifiquen una ubicación.</span><span class="sxs-lookup"><span data-stu-id="58197-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="58197-131">Esto se utiliza como ubicación predeterminada de Hola para recursos de ese grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="58197-131">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="58197-132">Sin embargo, dado que todos los recursos DNS son globales, no regionales, elección de Hola de ubicación del grupo de recursos tiene ningún impacto en el DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="58197-132">However, because all DNS resources are global, not regional, hello choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="58197-133">Puede omitir este paso si utiliza un grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="58197-133">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a><span data-ttu-id="58197-134">Ayuda</span><span class="sxs-lookup"><span data-stu-id="58197-134">Getting help</span></span>

<span data-ttu-id="58197-135">Inician todos los comandos de CLI 2.0 relativas tooAzure DNS con `az network dns`.</span><span class="sxs-lookup"><span data-stu-id="58197-135">All CLI 2.0 commands relating tooAzure DNS start with `az network dns`.</span></span> <span data-ttu-id="58197-136">La Ayuda está disponible para cada comando con hello `--help` opción (forma abreviada `-h`).</span><span class="sxs-lookup"><span data-stu-id="58197-136">Help is available for each command using hello `--help` option (short form `-h`).</span></span>  <span data-ttu-id="58197-137">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="58197-137">For example:</span></span>

```azurecli
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="58197-138">Creación de una zona DNS</span><span class="sxs-lookup"><span data-stu-id="58197-138">Create a DNS zone</span></span>

<span data-ttu-id="58197-139">Se crea una zona DNS con hello `az network dns zone create` comando.</span><span class="sxs-lookup"><span data-stu-id="58197-139">A DNS zone is created using hello `az network dns zone create` command.</span></span> <span data-ttu-id="58197-140">Para obtener ayuda, consulte `az network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="58197-140">For help, see `az network dns zone create -h`.</span></span>

<span data-ttu-id="58197-141">Hello en el ejemplo siguiente se crea una zona DNS denominada *contoso.com* en grupo de recursos de hello denominado *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="58197-141">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*:</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a><span data-ttu-id="58197-142">toocreate una zona DNS con etiquetas</span><span class="sxs-lookup"><span data-stu-id="58197-142">toocreate a DNS zone with tags</span></span>

<span data-ttu-id="58197-143">Hello en el ejemplo siguiente se muestra cómo toocreate un DNS de la zona con dos [etiquetas de Azure Resource Manager](dns-zones-records.md#tags), *proyecto = demostración* y *env = test*, mediante el uso de hello `--tags` parámetro (forma abreviada `-t`):</span><span class="sxs-lookup"><span data-stu-id="58197-143">hello following example shows how toocreate a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using hello `--tags` parameter (short form `-t`):</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="58197-144">Recuperación de una zona DNS</span><span class="sxs-lookup"><span data-stu-id="58197-144">Get a DNS zone</span></span>

<span data-ttu-id="58197-145">tooretrieve una zona DNS, use `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="58197-145">tooretrieve a DNS zone, use `az network dns zone show`.</span></span> <span data-ttu-id="58197-146">Para obtener ayuda, consulte `az network dns zone show --help`.</span><span class="sxs-lookup"><span data-stu-id="58197-146">For help, see `az network dns zone show --help`.</span></span>

<span data-ttu-id="58197-147">Hello en el ejemplo siguiente se devuelve la zona DNS hello *contoso.com* y sus datos asociados del grupo de recursos *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="58197-147">hello following example returns hello DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

<span data-ttu-id="58197-148">Hola siguiente ejemplo es la respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="58197-148">hello following example is hello response.</span></span>

```json
{
  "etag": "00000002-0000-0000-3d4d-64aa3689d201",
  "id": "/subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-04.azure-dns.com.",
    "ns2-04.azure-dns.net.",
    "ns3-04.azure-dns.org.",
    "ns4-04.azure-dns.info."
  ],
  "numberOfRecordSets": 4,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

<span data-ttu-id="58197-149">Tenga en cuenta que `az network dns zone show` no devuelve los registros DNS.</span><span class="sxs-lookup"><span data-stu-id="58197-149">Note that DNS records are not returned by `az network dns zone show`.</span></span> <span data-ttu-id="58197-150">usar los registros DNS toolist, `az network dns record-set list`.</span><span class="sxs-lookup"><span data-stu-id="58197-150">toolist DNS records, use `az network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="58197-151">Enumeración de zonas DNS</span><span class="sxs-lookup"><span data-stu-id="58197-151">List DNS zones</span></span>

<span data-ttu-id="58197-152">las zonas DNS tooenumerate, utilizar `az network dns zone list`.</span><span class="sxs-lookup"><span data-stu-id="58197-152">tooenumerate DNS zones, use `az network dns zone list`.</span></span> <span data-ttu-id="58197-153">Para obtener ayuda, consulte `az network dns zone list --help`.</span><span class="sxs-lookup"><span data-stu-id="58197-153">For help, see `az network dns zone list --help`.</span></span>

<span data-ttu-id="58197-154">Grupo de recursos de hello especificando muestra solo las zonas en el grupo de recursos de hello:</span><span class="sxs-lookup"><span data-stu-id="58197-154">Specifying hello resource group lists only those zones within hello resource group:</span></span>

```azurecli
az network dns zone list --resource-group MyResourceGroup
```

<span data-ttu-id="58197-155">Si se omite el grupo de recursos de hello enumera todas las zonas de suscripción de hello:</span><span class="sxs-lookup"><span data-stu-id="58197-155">Omitting hello resource group lists all zones in hello subscription:</span></span>

```azurecli
az network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="58197-156">Actualización de una zona DNS</span><span class="sxs-lookup"><span data-stu-id="58197-156">Update a DNS zone</span></span>

<span data-ttu-id="58197-157">Tooa cambios recursos de zona DNS pueden realizarse con `az network dns zone update`.</span><span class="sxs-lookup"><span data-stu-id="58197-157">Changes tooa DNS zone resource can be made using `az network dns zone update`.</span></span> <span data-ttu-id="58197-158">Para obtener ayuda, consulte `az network dns zone update --help`.</span><span class="sxs-lookup"><span data-stu-id="58197-158">For help, see `az network dns zone update --help`.</span></span>

<span data-ttu-id="58197-159">Este comando no actualiza cualquiera de los conjuntos de registros de DNS de hello en la zona de hello (vea [cómo los registros DNS tooManage](dns-operations-recordsets-cli.md)).</span><span class="sxs-lookup"><span data-stu-id="58197-159">This command does not update any of hello DNS record sets within hello zone (see [How tooManage DNS records](dns-operations-recordsets-cli.md)).</span></span> <span data-ttu-id="58197-160">Es solo tooupdate usa propiedades del propio recurso de zona Hola.</span><span class="sxs-lookup"><span data-stu-id="58197-160">It is only used tooupdate properties of hello zone resource itself.</span></span> <span data-ttu-id="58197-161">Estas propiedades están limitada actualmente toohello [Azure Resource Manager «etiquetas»](dns-zones-records.md#tags) para recursos de la zona de Hola.</span><span class="sxs-lookup"><span data-stu-id="58197-161">These properties are currently limited toohello [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for hello zone resource.</span></span>

<span data-ttu-id="58197-162">Hello en el ejemplo siguiente se muestra cómo tooupdate Hola etiquetas en una zona DNS.</span><span class="sxs-lookup"><span data-stu-id="58197-162">hello following example shows how tooupdate hello tags on a DNS zone.</span></span> <span data-ttu-id="58197-163">las etiquetas existentes Hola se reemplazan por valor de hello especificado.</span><span class="sxs-lookup"><span data-stu-id="58197-163">hello existing tags are replaced by hello value specified.</span></span>

```azurecli
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="58197-164">Eliminar una zona DNS</span><span class="sxs-lookup"><span data-stu-id="58197-164">Delete a DNS zone</span></span>

<span data-ttu-id="58197-165">Las zonas DNS se pueden eliminar mediante `az network dns zone delete`.</span><span class="sxs-lookup"><span data-stu-id="58197-165">DNS zones can be deleted using `az network dns zone delete`.</span></span> <span data-ttu-id="58197-166">Para obtener ayuda, consulte `az network dns zone delete --help`.</span><span class="sxs-lookup"><span data-stu-id="58197-166">For help, see `az network dns zone delete --help`.</span></span>

> [!NOTE]
> <span data-ttu-id="58197-167">Al eliminar una zona DNS, también eliminan todos los registros DNS en la zona de Hola.</span><span class="sxs-lookup"><span data-stu-id="58197-167">Deleting a DNS zone also deletes all DNS records within hello zone.</span></span> <span data-ttu-id="58197-168">Esta operación no se puede deshacer.</span><span class="sxs-lookup"><span data-stu-id="58197-168">This operation cannot be undone.</span></span> <span data-ttu-id="58197-169">Si la zona DNS Hola está en uso, se producirá un error en servicios con zona de hello cuando se elimina la zona de Hola.</span><span class="sxs-lookup"><span data-stu-id="58197-169">If hello DNS zone is in use, services using hello zone will fail when hello zone is deleted.</span></span>
>
><span data-ttu-id="58197-170">tooprotect contra la eliminación accidental de zona, consulte [cómo tooprotect DNS zonas y registros](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="58197-170">tooprotect against accidental zone deletion, see [How tooprotect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="58197-171">Este comando solicita confirmación.</span><span class="sxs-lookup"><span data-stu-id="58197-171">This command prompts for confirmation.</span></span> <span data-ttu-id="58197-172">Hola opcional `--yes` modificador suprime esta solicitud.</span><span class="sxs-lookup"><span data-stu-id="58197-172">hello optional `--yes` switch suppresses this prompt.</span></span>

<span data-ttu-id="58197-173">Hello en el ejemplo siguiente se muestra cómo toodelete Hola zona *contoso.com* del grupo de recursos *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="58197-173">hello following example shows how toodelete hello zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="58197-174">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="58197-174">Next steps</span></span>

<span data-ttu-id="58197-175">Obtenga información acerca de cómo demasiado[administrar conjuntos de registros y registros](dns-getstarted-create-recordset-cli.md) en la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="58197-175">Learn how too[manage record sets and records](dns-getstarted-create-recordset-cli.md) in your DNS zone.</span></span>

<span data-ttu-id="58197-176">Obtenga información acerca de cómo demasiado[delegar su tooAzure de dominio DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="58197-176">Learn how too[delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

