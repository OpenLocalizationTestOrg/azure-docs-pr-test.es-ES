---
title: "Administración de zonas DNS en Azure DNS (CLI de Azure 2.0) | Microsoft Docs"
description: "Puede administrar zonas DNS con la CLI de Azure 2.0. Este artículo muestra cómo actualizar, eliminar y crear zonas DNS en Azure DNS."
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
ms.openlocfilehash: 1414baf9e51d648cc3a46c4f8635040b4d276910
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-dns-zones-in-azure-dns-using-the-azure-cli-20"></a><span data-ttu-id="2d485-104">Cómo administrar zonas DNS en Azure DNS con la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="2d485-104">How to manage DNS Zones in Azure DNS using the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2d485-105">Portal</span><span class="sxs-lookup"><span data-stu-id="2d485-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="2d485-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2d485-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="2d485-107">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="2d485-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="2d485-108">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="2d485-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)


<span data-ttu-id="2d485-109">Esta guía muestra cómo administrar las zonas DNS mediante la CLI de Azure multiplataforma, que está disponible para Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="2d485-109">This guide shows how to manage your DNS zones by using the cross-platform Azure CLI, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="2d485-110">También puede administrar sus zonas DNS mediante [Azure PowerShell](dns-operations-dnszones.md) o Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2d485-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or the Azure portal.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="2d485-111">Versiones de la CLI para completar la tarea</span><span class="sxs-lookup"><span data-stu-id="2d485-111">CLI versions to complete the task</span></span>

<span data-ttu-id="2d485-112">Puede completar la tarea mediante una de las siguientes versiones de la CLI:</span><span class="sxs-lookup"><span data-stu-id="2d485-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="2d485-113">[CLI de Azure 1.0](dns-operations-dnszones-cli-nodejs.md): la CLI para los modelos de implementación clásica y de administración de recursos.</span><span class="sxs-lookup"><span data-stu-id="2d485-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="2d485-114">[CLI de Azure 2.0](dns-operations-dnszones-cli.md): la CLI de última generación para el modelo de implementación de administración de recursos.</span><span class="sxs-lookup"><span data-stu-id="2d485-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for the resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="2d485-115">Introducción</span><span class="sxs-lookup"><span data-stu-id="2d485-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-20-for-azure-dns"></a><span data-ttu-id="2d485-116">Configuración de la CLI de Azure 2.0 para Azure DNS</span><span class="sxs-lookup"><span data-stu-id="2d485-116">Set up Azure CLI 2.0 for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="2d485-117">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="2d485-117">Before you begin</span></span>

<span data-ttu-id="2d485-118">Antes de comenzar con la configuración, compruebe que dispone de los elementos siguientes.</span><span class="sxs-lookup"><span data-stu-id="2d485-118">Verify that you have the following items before beginning your configuration.</span></span>

* <span data-ttu-id="2d485-119">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="2d485-119">An Azure subscription.</span></span> <span data-ttu-id="2d485-120">Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) o registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2d485-120">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="2d485-121">Instale la versión más reciente de la CLI de Azure 2.0, disponible para Windows, Linux o Mac.</span><span class="sxs-lookup"><span data-stu-id="2d485-121">Install the latest version of the Azure CLI 2.0, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="2d485-122">Hay más información disponible en [Install the Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2) (Instalación de la CLI de Azure 2.0).</span><span class="sxs-lookup"><span data-stu-id="2d485-122">More information is available at [Install the Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

### <a name="sign-in-to-your-azure-account"></a><span data-ttu-id="2d485-123">Inicio de sesión en la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="2d485-123">Sign in to your Azure account</span></span>

<span data-ttu-id="2d485-124">Abra una ventana de consola y autentíquese con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="2d485-124">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="2d485-125">Para más información, consulte cómo iniciar sesión en Azure desde la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="2d485-125">For more information, see Log in to Azure from the Azure CLI</span></span>

```
az login
```

### <a name="select-the-subscription"></a><span data-ttu-id="2d485-126">Selección de la suscripción</span><span class="sxs-lookup"><span data-stu-id="2d485-126">Select the subscription</span></span>

<span data-ttu-id="2d485-127">Compruebe las suscripciones para la cuenta.</span><span class="sxs-lookup"><span data-stu-id="2d485-127">Check the subscriptions for the account.</span></span>

```
az account list
```

<span data-ttu-id="2d485-128">Elección de la suscripción de Azure que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="2d485-128">Choose which of your Azure subscriptions to use.</span></span>

```azurecli
az account set --subscription "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="2d485-129">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="2d485-129">Create a resource group</span></span>

<span data-ttu-id="2d485-130">El Administrador de recursos de Azure requiere que todos los grupos de recursos especifiquen una ubicación.</span><span class="sxs-lookup"><span data-stu-id="2d485-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="2d485-131">Esta se utiliza como ubicación predeterminada para los recursos de ese grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2d485-131">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="2d485-132">Sin embargo, puesto que todos los recursos DNS son globales y no regionales, la elección de la ubicación del grupo de recursos no incide en DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="2d485-132">However, because all DNS resources are global, not regional, the choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="2d485-133">Puede omitir este paso si utiliza un grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="2d485-133">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a><span data-ttu-id="2d485-134">Ayuda</span><span class="sxs-lookup"><span data-stu-id="2d485-134">Getting help</span></span>

<span data-ttu-id="2d485-135">Todos los comandos de la CLI 2.0 relacionados con Azure DNS comienzan por `az network dns`.</span><span class="sxs-lookup"><span data-stu-id="2d485-135">All CLI 2.0 commands relating to Azure DNS start with `az network dns`.</span></span> <span data-ttu-id="2d485-136">La ayuda está disponible para cada comando con la opción `--help` (formato abreviado `-h`).</span><span class="sxs-lookup"><span data-stu-id="2d485-136">Help is available for each command using the `--help` option (short form `-h`).</span></span>  <span data-ttu-id="2d485-137">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2d485-137">For example:</span></span>

```azurecli
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="2d485-138">Creación de una zona DNS</span><span class="sxs-lookup"><span data-stu-id="2d485-138">Create a DNS zone</span></span>

<span data-ttu-id="2d485-139">Una zona DNS se crea con el comando `az network dns zone create` .</span><span class="sxs-lookup"><span data-stu-id="2d485-139">A DNS zone is created using the `az network dns zone create` command.</span></span> <span data-ttu-id="2d485-140">Para obtener ayuda, consulte `az network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="2d485-140">For help, see `az network dns zone create -h`.</span></span>

<span data-ttu-id="2d485-141">En el ejemplo siguiente, se crea una zona DNS llamada *contoso.com* en el grupo de recursos *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="2d485-141">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*:</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="to-create-a-dns-zone-with-tags"></a><span data-ttu-id="2d485-142">Para crear una zona DNS con etiquetas.</span><span class="sxs-lookup"><span data-stu-id="2d485-142">To create a DNS zone with tags</span></span>

<span data-ttu-id="2d485-143">En el ejemplo siguiente se muestra cómo crear una zona DNS con dos [etiquetas de Azure Resource Manager](dns-zones-records.md#tags), *project = demo* y *env = test*, con el parámetro `--tags` (forma abreviada `-t`):</span><span class="sxs-lookup"><span data-stu-id="2d485-143">The following example shows how to create a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using the `--tags` parameter (short form `-t`):</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="2d485-144">Recuperación de una zona DNS</span><span class="sxs-lookup"><span data-stu-id="2d485-144">Get a DNS zone</span></span>

<span data-ttu-id="2d485-145">Para recuperar una zona DNS, use `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="2d485-145">To retrieve a DNS zone, use `az network dns zone show`.</span></span> <span data-ttu-id="2d485-146">Para obtener ayuda, consulte `az network dns zone show --help`.</span><span class="sxs-lookup"><span data-stu-id="2d485-146">For help, see `az network dns zone show --help`.</span></span>

<span data-ttu-id="2d485-147">El ejemplo siguiente devuelve la zona DNS *contoso.com* y sus datos asociados del grupo de recursos *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="2d485-147">The following example returns the DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

<span data-ttu-id="2d485-148">El ejemplo siguiente es la respuesta.</span><span class="sxs-lookup"><span data-stu-id="2d485-148">The following example is the response.</span></span>

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

<span data-ttu-id="2d485-149">Tenga en cuenta que `az network dns zone show` no devuelve los registros DNS.</span><span class="sxs-lookup"><span data-stu-id="2d485-149">Note that DNS records are not returned by `az network dns zone show`.</span></span> <span data-ttu-id="2d485-150">Para enumerar los registros DNS, utilice `az network dns record-set list`.</span><span class="sxs-lookup"><span data-stu-id="2d485-150">To list DNS records, use `az network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="2d485-151">Enumeración de zonas DNS</span><span class="sxs-lookup"><span data-stu-id="2d485-151">List DNS zones</span></span>

<span data-ttu-id="2d485-152">Para enumerar las zonas DNS, utilice `az network dns zone list`.</span><span class="sxs-lookup"><span data-stu-id="2d485-152">To enumerate DNS zones, use `az network dns zone list`.</span></span> <span data-ttu-id="2d485-153">Para obtener ayuda, consulte `az network dns zone list --help`.</span><span class="sxs-lookup"><span data-stu-id="2d485-153">For help, see `az network dns zone list --help`.</span></span>

<span data-ttu-id="2d485-154">Si se especifica el grupo de recursos, se enumeran solo esas zonas dentro del grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="2d485-154">Specifying the resource group lists only those zones within the resource group:</span></span>

```azurecli
az network dns zone list --resource-group MyResourceGroup
```

<span data-ttu-id="2d485-155">Si se omite el grupo de recursos, se enumeran todas las zonas en la suscripción:</span><span class="sxs-lookup"><span data-stu-id="2d485-155">Omitting the resource group lists all zones in the subscription:</span></span>

```azurecli
az network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="2d485-156">Actualización de una zona DNS</span><span class="sxs-lookup"><span data-stu-id="2d485-156">Update a DNS zone</span></span>

<span data-ttu-id="2d485-157">Los cambios en los recursos de una zona DNS se pueden realizar con `az network dns zone update`.</span><span class="sxs-lookup"><span data-stu-id="2d485-157">Changes to a DNS zone resource can be made using `az network dns zone update`.</span></span> <span data-ttu-id="2d485-158">Para obtener ayuda, consulte `az network dns zone update --help`.</span><span class="sxs-lookup"><span data-stu-id="2d485-158">For help, see `az network dns zone update --help`.</span></span>

<span data-ttu-id="2d485-159">Este comando no actualiza los conjuntos de registros DNS de la zona (consulte [Administración de registros DNS](dns-operations-recordsets-cli.md)).</span><span class="sxs-lookup"><span data-stu-id="2d485-159">This command does not update any of the DNS record sets within the zone (see [How to Manage DNS records](dns-operations-recordsets-cli.md)).</span></span> <span data-ttu-id="2d485-160">Solo se utiliza para actualizar las propiedades de los recursos de la zona.</span><span class="sxs-lookup"><span data-stu-id="2d485-160">It is only used to update properties of the zone resource itself.</span></span> <span data-ttu-id="2d485-161">Estas propiedades están actualmente limitadas a las ["etiquetas" Azure Resource Manager ](dns-zones-records.md#tags) para los recursos de la zona.</span><span class="sxs-lookup"><span data-stu-id="2d485-161">These properties are currently limited to the [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for the zone resource.</span></span>

<span data-ttu-id="2d485-162">En el ejemplo siguiente se muestra cómo actualizar las etiquetas en una zona DNS.</span><span class="sxs-lookup"><span data-stu-id="2d485-162">The following example shows how to update the tags on a DNS zone.</span></span> <span data-ttu-id="2d485-163">Las etiquetas existentes se reemplazan por el valor especificado.</span><span class="sxs-lookup"><span data-stu-id="2d485-163">The existing tags are replaced by the value specified.</span></span>

```azurecli
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="2d485-164">Eliminar una zona DNS</span><span class="sxs-lookup"><span data-stu-id="2d485-164">Delete a DNS zone</span></span>

<span data-ttu-id="2d485-165">Las zonas DNS se pueden eliminar mediante `az network dns zone delete`.</span><span class="sxs-lookup"><span data-stu-id="2d485-165">DNS zones can be deleted using `az network dns zone delete`.</span></span> <span data-ttu-id="2d485-166">Para obtener ayuda, consulte `az network dns zone delete --help`.</span><span class="sxs-lookup"><span data-stu-id="2d485-166">For help, see `az network dns zone delete --help`.</span></span>

> [!NOTE]
> <span data-ttu-id="2d485-167">Si se elimina una zona DNS, también se eliminan todos los registros DNS dentro de la zona.</span><span class="sxs-lookup"><span data-stu-id="2d485-167">Deleting a DNS zone also deletes all DNS records within the zone.</span></span> <span data-ttu-id="2d485-168">Esta operación no se puede deshacer.</span><span class="sxs-lookup"><span data-stu-id="2d485-168">This operation cannot be undone.</span></span> <span data-ttu-id="2d485-169">Si la zona DNS está en uso, los servicios con la zona provocarán un error cuando se elimina la zona.</span><span class="sxs-lookup"><span data-stu-id="2d485-169">If the DNS zone is in use, services using the zone will fail when the zone is deleted.</span></span>
>
><span data-ttu-id="2d485-170">Para protegerse contra la eliminación accidental de zona, consulte [Proteger registros y zonas DNS](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="2d485-170">To protect against accidental zone deletion, see [How to protect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="2d485-171">Este comando solicita confirmación.</span><span class="sxs-lookup"><span data-stu-id="2d485-171">This command prompts for confirmation.</span></span> <span data-ttu-id="2d485-172">El modificador `--yes` opcional suprime este mensaje.</span><span class="sxs-lookup"><span data-stu-id="2d485-172">The optional `--yes` switch suppresses this prompt.</span></span>

<span data-ttu-id="2d485-173">En el ejemplo siguiente se muestra cómo eliminar la zona *contoso.com* del grupo de recursos *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="2d485-173">The following example shows how to delete the zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="2d485-174">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2d485-174">Next steps</span></span>

<span data-ttu-id="2d485-175">En esta guía se explica cómo [administrar conjuntos de registros y registros](dns-getstarted-create-recordset-cli.md) en la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="2d485-175">Learn how to [manage record sets and records](dns-getstarted-create-recordset-cli.md) in your DNS zone.</span></span>

<span data-ttu-id="2d485-176">Aprenda a cómo [delegar el dominio a Azure DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="2d485-176">Learn how to [delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

