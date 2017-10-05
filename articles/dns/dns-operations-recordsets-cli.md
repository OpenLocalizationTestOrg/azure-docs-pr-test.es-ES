---
title: "Administración de registros de DNS en Azure DNS mediante la CLI de Azure 2.0 | Microsoft Docs"
description: "Administración de conjuntos de registros y registros DNS en DNS de Azure al hospedar dominios en DNS de Azure. Todos los comandos de la CLI 2.0 para operaciones en conjuntos de registros y registros."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 5356a3a5-8dec-44ac-9709-0c2b707f6cb5
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: jonatul
ms.openlocfilehash: 9543759d7ba88c7c5068021cebbeec6b8d63633e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-the-azure-cli-20"></a><span data-ttu-id="7289d-104">Administración de conjuntos de registros y registros de DNS en Azure DNS mediante la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="7289d-104">Manage DNS records and recordsets in Azure DNS using the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7289d-105">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="7289d-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="7289d-106">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="7289d-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="7289d-107">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="7289d-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="7289d-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7289d-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="7289d-109">En este artículo se muestra cómo administrar los registros de DNS para su zona DNS mediante la versión 2.0 de la interfaz de la línea de comandos (CLI) multiplataforma de Azure, disponible para Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="7289d-109">This article shows you how to manage DNS records for your DNS zone by using the cross-platform Azure command-line interface (CLI) 2.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="7289d-110">También puede administrar sus registros de DNS mediante [Azure PowerShell](dns-operations-recordsets.md) o [Azure Portal](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7289d-110">You can also manage your DNS records using [Azure PowerShell](dns-operations-recordsets.md) or the [Azure portal](dns-operations-recordsets-portal.md).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="7289d-111">Versiones de la CLI para completar la tarea</span><span class="sxs-lookup"><span data-stu-id="7289d-111">CLI versions to complete the task</span></span>

<span data-ttu-id="7289d-112">Puede completar la tarea mediante una de las siguientes versiones de la CLI:</span><span class="sxs-lookup"><span data-stu-id="7289d-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="7289d-113">[CLI de Azure 1.0](dns-operations-recordsets-cli-nodejs.md): la CLI para los modelos de implementación clásica y de administración de recursos.</span><span class="sxs-lookup"><span data-stu-id="7289d-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="7289d-114">[CLI de Azure 2.0](dns-operations-recordsets-cli.md): la CLI de última generación para el modelo de implementación de administración de recursos.</span><span class="sxs-lookup"><span data-stu-id="7289d-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) - our next generation CLI for the resource management deployment model.</span></span>

<span data-ttu-id="7289d-115">En los ejemplos de este artículo se supone que ya ha [instalado la CLI de Azure 2.0, iniciado sesión y creado una zona DNS](dns-operations-dnszones-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7289d-115">The examples in this article assume you have already [installed the Azure CLI 2.0, signed in, and created a DNS zone](dns-operations-dnszones-cli.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="7289d-116">Introducción</span><span class="sxs-lookup"><span data-stu-id="7289d-116">Introduction</span></span>

<span data-ttu-id="7289d-117">Antes de crear registros DNS en Azure DNS, es necesario que comprenda cómo Azure DNS los organiza en conjuntos de registros DNS.</span><span class="sxs-lookup"><span data-stu-id="7289d-117">Before creating DNS records in Azure DNS, you first need to understand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="7289d-118">Para más información sobre los registros DNS en Azure DNS, consulte [DNS zones and records](dns-zones-records.md) (Zonas y registros DNS).</span><span class="sxs-lookup"><span data-stu-id="7289d-118">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>

## <a name="create-a-dns-record"></a><span data-ttu-id="7289d-119">Creación de un registro de DNS</span><span class="sxs-lookup"><span data-stu-id="7289d-119">Create a DNS record</span></span>

<span data-ttu-id="7289d-120">Para crear un registro DNS, use el comando `az network dns record-set <record-type> set-record` (donde `<record-type>` es el tipo de registro, es decir,</span><span class="sxs-lookup"><span data-stu-id="7289d-120">To create a DNS record, use the `az network dns record-set <record-type> set-record` command (where `<record-type>` is the type of record, i.e</span></span> <span data-ttu-id="7289d-121">a, srv, txt, etc.) Para obtener ayuda, consulte `az network dns record-set --help`.</span><span class="sxs-lookup"><span data-stu-id="7289d-121">a, srv, txt, etc.) For help, see `az network dns record-set --help`.</span></span>

<span data-ttu-id="7289d-122">Al crear un registro, debe especificar los nombres del grupo de recursos, de la zona y del conjunto de registros, el tipo de registro y los detalles del registro que se están creando.</span><span class="sxs-lookup"><span data-stu-id="7289d-122">When creating a record, you need to specify the resource group name, zone name, record set name, the record type, and the details of the record being created.</span></span> <span data-ttu-id="7289d-123">El nombre del conjunto de registros especificado debe ser un nombre *relativo*; es decir, debe excluir el nombre de zona.</span><span class="sxs-lookup"><span data-stu-id="7289d-123">The record set name given must be a *relative* name, meaning it must exclude the zone name.</span></span>

<span data-ttu-id="7289d-124">Si el conjunto de registros aún no existe, este comando lo crea automáticamente.</span><span class="sxs-lookup"><span data-stu-id="7289d-124">If the record set does not already exist, this command creates it for you.</span></span> <span data-ttu-id="7289d-125">Si el conjunto de registros ya existe, este comando agrega el registro que especifique al conjunto de registros existente.</span><span class="sxs-lookup"><span data-stu-id="7289d-125">If the record set already exists, this command adds the record you specify to the existing record set.</span></span>

<span data-ttu-id="7289d-126">Si se crea un conjunto de registros, se utiliza el valor predeterminado del período de vida (3600).</span><span class="sxs-lookup"><span data-stu-id="7289d-126">If a new record set is created, a default time-to-live (TTL) of 3600 is used.</span></span> <span data-ttu-id="7289d-127">Para obtener instrucciones sobre cómo usar diferentes TTL, consulte [Creación de un conjunto de registros de DNS](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="7289d-127">For instructions on how to use different TTLs, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="7289d-128">En el ejemplo siguiente se crea un registro A denominado *www* en la zona *contoso.com* del grupo de recursos *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="7289d-128">The following example creates an A record called *www* in the zone *contoso.com* in the resource group *MyResourceGroup*.</span></span> <span data-ttu-id="7289d-129">La dirección IP del registro A es *1.2.3.4*.</span><span class="sxs-lookup"><span data-stu-id="7289d-129">The IP address of the A record is *1.2.3.4*.</span></span>

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 1.2.3.4
```

<span data-ttu-id="7289d-130">Para crear un conjunto de registros en el vértice de la zona (en este caso, "contoso.com"), utilice el nombre de registro "@", incluidas las comillas:</span><span class="sxs-lookup"><span data-stu-id="7289d-130">To create a record set in the apex of the zone (in this case, "contoso.com"), use the record name "@", including the quotation marks:</span></span>

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --ipv4-address 1.2.3.4
```

## <a name="create-a-dns-record-set"></a><span data-ttu-id="7289d-131">Creación de un conjunto de registros de DNS</span><span class="sxs-lookup"><span data-stu-id="7289d-131">Create a DNS record set</span></span>

<span data-ttu-id="7289d-132">En los ejemplos anteriores, bien se agregó el registro de DNS en un conjunto de registros existente, bien se creó el conjunto de registros *implícitamente*.</span><span class="sxs-lookup"><span data-stu-id="7289d-132">In the above examples, the DNS record was either added to an existing record set, or the record set was created *implicitly*.</span></span> <span data-ttu-id="7289d-133">También puede crear el conjunto de registros *explícitamente* antes de agregarle registros.</span><span class="sxs-lookup"><span data-stu-id="7289d-133">You can also create the record set *explicitly* before adding records to it.</span></span> <span data-ttu-id="7289d-134">La DNS de Azure admite conjuntos de registros "vacíos" que pueden funcionar como marcador de posición para reservar un nombre DNS antes de crear registros de DNS.</span><span class="sxs-lookup"><span data-stu-id="7289d-134">Azure DNS supports 'empty' record sets, which can act as a placeholder to reserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="7289d-135">Los conjuntos de registros vacíos se pueden ver en el panel de control de DNS de Azure, pero no aparecen en los servidores de nombres de DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="7289d-135">Empty record sets are visible in the Azure DNS control plane, but do not appear on the Azure DNS name servers.</span></span>

<span data-ttu-id="7289d-136">Los conjuntos de registros se crean con el comando `az network dns record-set <record-type> create`.</span><span class="sxs-lookup"><span data-stu-id="7289d-136">Record sets are created using the `az network dns record-set <record-type> create` command.</span></span> <span data-ttu-id="7289d-137">Para obtener ayuda, consulte `az network dns record-set <record-type> create --help`.</span><span class="sxs-lookup"><span data-stu-id="7289d-137">For help, see `az network dns record-set <record-type> create --help`.</span></span>

<span data-ttu-id="7289d-138">Al crear el conjunto de registros explícitamente, podrá especificar las propiedades de este, como el [período de vida (TTL)](dns-zones-records.md#time-to-live) y los metadatos.</span><span class="sxs-lookup"><span data-stu-id="7289d-138">Creating the record set explicitly allows you to specify record set properties such as the [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) and metadata.</span></span> <span data-ttu-id="7289d-139">Se pueden usar [metadatos del conjunto de registros](dns-zones-records.md#tags-and-metadata) para asociar datos específicos de la aplicación con cada conjunto de registros como pares clave-valor.</span><span class="sxs-lookup"><span data-stu-id="7289d-139">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="7289d-140">En el ejemplo siguiente se crea un conjunto de registros vacío de tipo "A" con un TTL de 60 segundos mediante el parámetro `--ttl` (forma abreviada `-l`):</span><span class="sxs-lookup"><span data-stu-id="7289d-140">The following example creates an empty record set of type 'A' with a 60-second TTL, by using the `--ttl` parameter (short form `-l`):</span></span>

```azurecli
az network dns record-set a create --resource-group myresourcegroup --zone-name contoso.com --name www --ttl 60
```

<span data-ttu-id="7289d-141">En el siguiente ejemplo, se crea un conjunto de registros con dos entradas de metadatos, "dept=finance" y "environment=production", mediante el parámetro `--metadata`:</span><span class="sxs-lookup"><span data-stu-id="7289d-141">The following example creates a record set with two metadata entries, "dept=finance" and "environment=production", by using the `--metadata` parameter :</span></span>

```azurecli
az network dns record-set a create --resource-group myresourcegroup --zone-name contoso.com --name www --metadata "dept=finance" "environment=production"
```

<span data-ttu-id="7289d-142">Tras haber creado un conjunto de registros vacío, se podrán añadir el registro mediante `azure network dns record-set <record-type> set-record`, como se describe en [Creación de un registro de DNS](#create-a-dns-record).</span><span class="sxs-lookup"><span data-stu-id="7289d-142">Having created an empty record set, records can be added using `azure network dns record-set <record-type> set-record` as described in [Create a DNS record](#create-a-dns-record).</span></span>

## <a name="create-records-of-other-types"></a><span data-ttu-id="7289d-143">Creación de registros de otros tipos</span><span class="sxs-lookup"><span data-stu-id="7289d-143">Create records of other types</span></span>

<span data-ttu-id="7289d-144">Después de haber visto de forma detallada cómo crear registros "A", en los siguientes ejemplos se muestra cómo crear registros de otros tipos compatibles con DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="7289d-144">Having seen in detail how to create 'A' records, the following examples show how to create record of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="7289d-145">Los parámetros utilizados para especificar los datos del registro varían según el tipo del registro.</span><span class="sxs-lookup"><span data-stu-id="7289d-145">The parameters used to specify the record data vary depending on the type of the record.</span></span> <span data-ttu-id="7289d-146">Por ejemplo, para un registro de tipo "A", especifique la dirección IPv4 con el parámetro `--ipv4-address <IPv4 address>`.</span><span class="sxs-lookup"><span data-stu-id="7289d-146">For example, for a record of type "A", you specify the IPv4 address with the parameter `--ipv4-address <IPv4 address>`.</span></span> <span data-ttu-id="7289d-147">Es posible obtener una lista de los parámetros de cada tipo de registro con `az network dns record-set <record-type> set-record --help`.</span><span class="sxs-lookup"><span data-stu-id="7289d-147">The parameters for each record type can be listed using `az network dns record-set <record-type> set-record --help`.</span></span>

<span data-ttu-id="7289d-148">En cada caso, se muestra cómo crear un único registro.</span><span class="sxs-lookup"><span data-stu-id="7289d-148">In each case, we show how to create a single record.</span></span> <span data-ttu-id="7289d-149">Se agrega el registro al conjunto de registros existente o a uno creado de forma implícita.</span><span class="sxs-lookup"><span data-stu-id="7289d-149">The record is added to the existing record set, or a record set created implicitly.</span></span> <span data-ttu-id="7289d-150">Para obtener más información sobre cómo crear conjuntos de registros y definir explícitamente los parámetros de un conjunto de registros, consulte [Creación de un conjunto de registros de DNS](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="7289d-150">For more information on creating record sets and defining record set parameter explicitly, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="7289d-151">No se proporciona un ejemplo para crear un conjunto de registros SOA, dado que los registros SOA se crean y eliminan con cada zona de DNS y no lo pueden hacer por separado.</span><span class="sxs-lookup"><span data-stu-id="7289d-151">We do not give an example to create an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="7289d-152">Sin embargo, [el registro SOA se puede modificar, como se muestra en un ejemplo más adelante](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="7289d-152">However, [the SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record"></a><span data-ttu-id="7289d-153">Creación de un registro AAAA</span><span class="sxs-lookup"><span data-stu-id="7289d-153">Create an AAAA record</span></span>

```azurecli
az network dns record-set aaaa set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-aaaa --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a><span data-ttu-id="7289d-154">Creación de un registro CNAME</span><span class="sxs-lookup"><span data-stu-id="7289d-154">Create a CNAME record</span></span>

> [!NOTE]
> <span data-ttu-id="7289d-155">Los estándares DNS no permiten registros CNAME en el vértice de una zona (`--Name "@"`), ni permiten conjuntos de registros que contengan más de un registro.</span><span class="sxs-lookup"><span data-stu-id="7289d-155">The DNS standards do not permit CNAME records at the apex of a zone (`--Name "@"`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="7289d-156">Para más información, consulte [Registros CNAME](dns-zones-records.md#cname-records).</span><span class="sxs-lookup"><span data-stu-id="7289d-156">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>

```azurecli
az network dns record-set cname set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-cname --cname www.contoso.com
```

### <a name="create-an-mx-record"></a><span data-ttu-id="7289d-157">Creación de un registro MX</span><span class="sxs-lookup"><span data-stu-id="7289d-157">Create an MX record</span></span>

<span data-ttu-id="7289d-158">En este ejemplo, se utiliza el nombre de conjunto de registros "@" para crear el registro MX en el vértice de la zona (en este caso, "contoso.com").</span><span class="sxs-lookup"><span data-stu-id="7289d-158">In this example, we use the record set name "@" to create the MX record at the zone apex (in this case, "contoso.com").</span></span>

```azurecli
az network dns record-set mx set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a><span data-ttu-id="7289d-159">Creación de un registro NS</span><span class="sxs-lookup"><span data-stu-id="7289d-159">Create an NS record</span></span>

```azurecli
az network dns record-set ns set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-ns --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a><span data-ttu-id="7289d-160">Creación de un registro PTR</span><span class="sxs-lookup"><span data-stu-id="7289d-160">Create a PTR record</span></span>

<span data-ttu-id="7289d-161">En este caso "my-arpa-zone.com" representa la zona ARPA que representa el intervalo IP.</span><span class="sxs-lookup"><span data-stu-id="7289d-161">In this case, 'my-arpa-zone.com' represents the ARPA zone representing your IP range.</span></span> <span data-ttu-id="7289d-162">Cada registro PTR establecido en esta zona se corresponde con una dirección IP dentro de este intervalo IP.</span><span class="sxs-lookup"><span data-stu-id="7289d-162">Each PTR record set in this zone corresponds to an IP address within this IP range.</span></span>  <span data-ttu-id="7289d-163">El nombre de registro "10" es el último octeto de la dirección IP dentro del intervalo IP que representa dicho registro.</span><span class="sxs-lookup"><span data-stu-id="7289d-163">The record name '10' is the last octet of the IP address within this IP range represented by this record.</span></span>

```azurecli
az network dns record-set ptr set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name my-arpa.zone.com --ptrdname myservice.contoso.com
```

### <a name="create-an-srv-record"></a><span data-ttu-id="7289d-164">Creación de un registro SRV</span><span class="sxs-lookup"><span data-stu-id="7289d-164">Create an SRV record</span></span>

<span data-ttu-id="7289d-165">Al crear un [conjunto de registros SRV](dns-zones-records.md#srv-records), especifique el *\_servicio* y el *\_protocolo* en el nombre del conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="7289d-165">When creating an [SRV record set](dns-zones-records.md#srv-records), specify the *\_service* and *\_protocol* in the record set name.</span></span> <span data-ttu-id="7289d-166">No es necesario incluir "@" en el nombre del conjunto de registros al crear un conjunto de registros SRV en el vértice de la zona.</span><span class="sxs-lookup"><span data-stu-id="7289d-166">There is no need to include "@" in the record set name when creating an SRV record set at the zone apex.</span></span>

```azurecli
az network dns record-set srv set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name _sip._tls --priority 10 --weight 5 --port 8080 --target sip.contoso.com
```

### <a name="create-a-txt-record"></a><span data-ttu-id="7289d-167">Creación de un registro TXT</span><span class="sxs-lookup"><span data-stu-id="7289d-167">Create a TXT record</span></span>

<span data-ttu-id="7289d-168">En el ejemplo siguiente se muestra cómo crear un registro TXT.</span><span class="sxs-lookup"><span data-stu-id="7289d-168">The following example shows how to create a TXT record.</span></span> <span data-ttu-id="7289d-169">Para más información sobre la longitud de cadena máxima admitida en registros TXT, consulte [Registros TXT](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="7289d-169">For more information about the maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```azurecli
az network dns record-set txt set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-txt --value "This is a TXT record"
```

## <a name="get-a-record-set"></a><span data-ttu-id="7289d-170">Recuperación de un conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="7289d-170">Get a record set</span></span>

<span data-ttu-id="7289d-171">Para recuperar un conjunto de registros existente, use `az network dns record-set <record-type> show`.</span><span class="sxs-lookup"><span data-stu-id="7289d-171">To retrieve an existing record set, use `az network dns record-set <record-type> show`.</span></span> <span data-ttu-id="7289d-172">Para obtener ayuda, consulte `az network dns record-set <record-type> show --help`.</span><span class="sxs-lookup"><span data-stu-id="7289d-172">For help, see `az network dns record-set <record-type> show --help`.</span></span>

<span data-ttu-id="7289d-173">Al igual que sucede con la creación de un registro o conjunto de registros, el nombre del conjunto de registros especificado debe ser un nombre *relativo*, lo que significa que debe excluir el nombre de zona.</span><span class="sxs-lookup"><span data-stu-id="7289d-173">As when creating a record or record set, the record set name given must be a *relative* name, meaning it must exclude the zone name.</span></span> <span data-ttu-id="7289d-174">También debe especificar el tipo de registro, la zona que contiene el conjunto de registros y el grupo de recursos que contiene la zona.</span><span class="sxs-lookup"><span data-stu-id="7289d-174">You also need to specify the record type, the zone containing the record set, and the resource group containing the zone.</span></span>

<span data-ttu-id="7289d-175">En el ejemplo siguiente se recupera el registro *www* de tipo A de la zona *contoso.com*, que se encuentra en el grupo de recursos *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="7289d-175">The following example retrieves the record *www* of type A from zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
az network dns record-set a show --resource-group myresourcegroup --zone-name contoso.com --name www
```

## <a name="list-record-sets"></a><span data-ttu-id="7289d-176">Enumeración de conjuntos de registros</span><span class="sxs-lookup"><span data-stu-id="7289d-176">List record sets</span></span>

<span data-ttu-id="7289d-177">Puede mostrar todos los registros de una zona DNS con el comando `az network dns record-set list` .</span><span class="sxs-lookup"><span data-stu-id="7289d-177">You can list all records in a DNS zone by using the `az network dns record-set list` command.</span></span> <span data-ttu-id="7289d-178">Para obtener ayuda, consulte `az network dns record-set list --help`.</span><span class="sxs-lookup"><span data-stu-id="7289d-178">For help, see `az network dns record-set list --help`.</span></span>

<span data-ttu-id="7289d-179">En este ejemplo, se devuelve todos los conjuntos de registros de la zona *contoso.com*, que se encuentra en el grupo de recursos *MyResourceGroup*, con independencia del nombre o del tipo de registro:</span><span class="sxs-lookup"><span data-stu-id="7289d-179">This example returns all record sets in the zone *contoso.com*, in resource group *MyResourceGroup*, regardless of name or record type:</span></span>

```azurecli
az network dns record-set list --resource-group myresourcegroup --zone-name contoso.com
```

<span data-ttu-id="7289d-180">En este ejemplo, se devuelven todos los conjuntos de registros que coinciden con el tipo de registro especificado (en este caso, los registros "A"):</span><span class="sxs-lookup"><span data-stu-id="7289d-180">This example returns all record sets that match the given record type (in this case, 'A' records):</span></span>

```azurecli
az network dns record-set a list --resource-group myresourcegroup --zone-name contoso.com 
```

## <a name="add-a-record-to-an-existing-record-set"></a><span data-ttu-id="7289d-181">Adición de un registro a un conjunto de registros existente</span><span class="sxs-lookup"><span data-stu-id="7289d-181">Add a record to an existing record set</span></span>

<span data-ttu-id="7289d-182">Puede usar `az network dns record-set <record-type> set-record` tanto para crear un registro en un nuevo conjunto de registros como para agregar un registro a un conjunto de registros existente.</span><span class="sxs-lookup"><span data-stu-id="7289d-182">You can use `az network dns record-set <record-type> set-record` both to create a record in a new record set, or to add a record to an existing record set.</span></span>

<span data-ttu-id="7289d-183">Para obtener más información, consulte las secciones [Creación de un registro de DNS](#create-a-dns-record) y [Creación de registros de otros tipos](#create-records-of-other-types).</span><span class="sxs-lookup"><span data-stu-id="7289d-183">For more information, see [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="7289d-184">Quite un registro de un conjunto de registros existente.</span><span class="sxs-lookup"><span data-stu-id="7289d-184">Remove a record from an existing record set.</span></span>

<span data-ttu-id="7289d-185">Para quitar un registro de DNS de un conjunto de registros existente, use `az network dns record-set <record-type> remove-record`.</span><span class="sxs-lookup"><span data-stu-id="7289d-185">To remove a DNS record from an existing record set, use `az network dns record-set <record-type> remove-record`.</span></span> <span data-ttu-id="7289d-186">Para obtener ayuda, consulte `az network dns record-set <record-type> remove-record -h`.</span><span class="sxs-lookup"><span data-stu-id="7289d-186">For help, see `az network dns record-set <record-type> remove-record -h`.</span></span>

<span data-ttu-id="7289d-187">Este comando elimina un registro de DNS de un conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="7289d-187">This command deletes a DNS record from a record set.</span></span> <span data-ttu-id="7289d-188">Si se elimina el último registro de un conjunto de registros, el conjunto de registros propiamente dicho también se elimina.</span><span class="sxs-lookup"><span data-stu-id="7289d-188">If the last record in a record set is deleted, the record set itself is also deleted.</span></span> <span data-ttu-id="7289d-189">Si, por el contrario, desea mantener el registro vacío, use la opción `--keep-empty-record-set`.</span><span class="sxs-lookup"><span data-stu-id="7289d-189">To keep the empty record set instead, use the `--keep-empty-record-set` option.</span></span>

<span data-ttu-id="7289d-190">Debe especificar el registro que desee eliminar y la zona de la que se debe eliminar; para ello, use los mismos parámetros empleados al crear el registro con `az network dns record-set <record-type> set-record`.</span><span class="sxs-lookup"><span data-stu-id="7289d-190">You need to specify the record to be deleted and the zone it should be deleted from, using the same parameters as when creating a record using `az network dns record-set <record-type> set-record`.</span></span> <span data-ttu-id="7289d-191">Estos parámetros se describen en las secciones [Creación de un registro de DNS](#create-a-dns-record) y [Creación de registros de otros tipos](#create-records-of-other-types).</span><span class="sxs-lookup"><span data-stu-id="7289d-191">These parameters are described in [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

<span data-ttu-id="7289d-192">En el ejemplo siguiente se elimina el registro A con el valor "1.2.3.4" del conjunto de registros con el nombre *www* de la zona *contoso.com*, que se encuentra en el grupo de recursos *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="7289d-192">The following example deletes the A record with value '1.2.3.4' from the record set named *www* in the zone *contoso.com*, in the resource group *MyResourceGroup*.</span></span>

```azurecli
az network dns record-set a remove-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "www" --ipv4-address 1.2.3.4
```

## <a name="modify-an-existing-record-set"></a><span data-ttu-id="7289d-193">Modificación de un conjunto de registros existente</span><span class="sxs-lookup"><span data-stu-id="7289d-193">Modify an existing record set</span></span>

<span data-ttu-id="7289d-194">Cada conjunto de registros contiene un [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadatos](dns-zones-records.md#tags-and-metadata)y los registros de DNS.</span><span class="sxs-lookup"><span data-stu-id="7289d-194">Each record set contains a [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadata](dns-zones-records.md#tags-and-metadata), and DNS records.</span></span> <span data-ttu-id="7289d-195">En las siguientes secciones se explican cómo modificar cada una de estas propiedades.</span><span class="sxs-lookup"><span data-stu-id="7289d-195">The following sections explain how to modify each of these properties.</span></span>

### <a name="to-modify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a><span data-ttu-id="7289d-196">Para modificar un registro A, AAAA, MX, NS, PTR, SRV o TXT</span><span class="sxs-lookup"><span data-stu-id="7289d-196">To modify an A, AAAA, MX, NS, PTR, SRV, or TXT record</span></span>

<span data-ttu-id="7289d-197">Para modificar un registro existente de tipo A, AAAA, MX, NS, PTR, SRV o TXT, debe agregar primero un nuevo registro y, después, eliminar el existente.</span><span class="sxs-lookup"><span data-stu-id="7289d-197">To modify an existing record of type A, AAAA, MX, NS, PTR, SRV, or TXT, you should first add a new record and then delete the existing record.</span></span> <span data-ttu-id="7289d-198">Para obtener instrucciones detalladas sobre cómo eliminar y agregar registros, consulte las secciones anteriores de este artículo.</span><span class="sxs-lookup"><span data-stu-id="7289d-198">For detailed instructions on how to delete and add records, see the earlier sections of this article.</span></span>

<span data-ttu-id="7289d-199">En el ejemplo siguiente se muestra cómo modificar un registro "A", de la dirección IP 1.2.3.4 a la 5.6.7.8:</span><span class="sxs-lookup"><span data-stu-id="7289d-199">The following example shows how to modify an 'A' record, from IP address 1.2.3.4 to IP address 5.6.7.8:</span></span>

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 5.6.7.8
az network dns record-set a remove-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 1.2.3.4
```

<span data-ttu-id="7289d-200">No puede agregar, quitar ni modificar los registros del conjunto de registros NS creado automáticamente en el vértice de zona (`--Name "@"`, comillas incluidas).</span><span class="sxs-lookup"><span data-stu-id="7289d-200">You cannot add, remove, or modify the records in the automatically created NS record set at the zone apex (`--Name "@"`, including quote marks).</span></span> <span data-ttu-id="7289d-201">En el caso de este conjunto de registros, los únicos cambios permitidos son modificar el TTL del conjunto de registros y los metadatos.</span><span class="sxs-lookup"><span data-stu-id="7289d-201">For this record set, the only changes permitted are to modify the record set TTL and metadata.</span></span>

### <a name="to-modify-a-cname-record"></a><span data-ttu-id="7289d-202">Para modificar un registro CNAME</span><span class="sxs-lookup"><span data-stu-id="7289d-202">To modify a CNAME record</span></span>

<span data-ttu-id="7289d-203">A diferencia de la mayoría de otros tipos de registros, un conjunto de registros CNAME solo puede contener un único registro.</span><span class="sxs-lookup"><span data-stu-id="7289d-203">Unlike most other record types, a CNAME record set can only contain a single record.</span></span>  <span data-ttu-id="7289d-204">Por lo tanto, para reemplazar el valor actual no se puede agregar un nuevo registro y quitar el existente, como en otros tipos de registros.</span><span class="sxs-lookup"><span data-stu-id="7289d-204">Therefore, you cannot replace the current value by adding a new record and removing the existing record, as for other record types.</span></span>

<span data-ttu-id="7289d-205">En su lugar, para modificar un registro CNAME, use `az network dns record-set cname set-record`.</span><span class="sxs-lookup"><span data-stu-id="7289d-205">Instead, to modify a CNAME record, use `az network dns record-set cname set-record`.</span></span> <span data-ttu-id="7289d-206">Para obtener ayuda, consulte `az network dns record-set cname set-record --help`.</span><span class="sxs-lookup"><span data-stu-id="7289d-206">For help, see `az network dns record-set cname set-record --help`</span></span>

<span data-ttu-id="7289d-207">En el ejemplo se modifica el conjunto de registros CNAME *www* de la zona *contoso.com*, que se encuentra en el grupo de recursos *MyResourceGroup*, para que apunte a "www.fabrikam.net" en lugar de a su valor existente:</span><span class="sxs-lookup"><span data-stu-id="7289d-207">The example modifies the CNAME record set *www* in the zone *contoso.com*, in resource group *MyResourceGroup*, to point to 'www.fabrikam.net' instead of its existing value:</span></span>

```azurecli
az network dns record-set cname set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-cname --cname www.fabrikam.net
``` 

### <a name="to-modify-an-soa-record"></a><span data-ttu-id="7289d-208">Para modificar un registro SOA</span><span class="sxs-lookup"><span data-stu-id="7289d-208">To modify an SOA record</span></span>

<span data-ttu-id="7289d-209">A diferencia de la mayoría de otros tipos de registros, un conjunto de registros CNAME solo puede contener un único registro.</span><span class="sxs-lookup"><span data-stu-id="7289d-209">Unlike most other record types, a CNAME record set can only contain a single record.</span></span>  <span data-ttu-id="7289d-210">Por lo tanto, para reemplazar el valor actual no se puede agregar un nuevo registro y quitar el existente, como en otros tipos de registros.</span><span class="sxs-lookup"><span data-stu-id="7289d-210">Therefore, you cannot replace the current value by adding a new record and removing the existing record, as for other record types.</span></span>

<span data-ttu-id="7289d-211">En su lugar, para modificar el registro SOA, use `az network dns record-set soa update`.</span><span class="sxs-lookup"><span data-stu-id="7289d-211">Instead, to modify the SOA record, use `az network dns record-set soa update`.</span></span> <span data-ttu-id="7289d-212">Para obtener ayuda, consulte `az network dns record-set soa update --help`.</span><span class="sxs-lookup"><span data-stu-id="7289d-212">For help, see `az network dns record-set soa update --help`.</span></span>

<span data-ttu-id="7289d-213">En el ejemplo siguiente se muestra cómo establecer la propiedad "email" del registro SOA de la zona *contoso.com* del grupo de recursos *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="7289d-213">The following example shows how to set the 'email' property of the SOA record for the zone *contoso.com* in the resource group *MyResourceGroup*:</span></span>

```azurecli
az network dns record-set soa update --resource-group myresourcegroup --zone-name contoso.com --email admin.contoso.com
```

### <a name="to-modify-ns-records-at-the-zone-apex"></a><span data-ttu-id="7289d-214">Para modificar los registros NS en el vértice de zona</span><span class="sxs-lookup"><span data-stu-id="7289d-214">To modify NS records at the zone apex</span></span>

<span data-ttu-id="7289d-215">El conjunto de registros NS en el vértice de zona se crea automáticamente con cada zona DNS.</span><span class="sxs-lookup"><span data-stu-id="7289d-215">The NS record set at the zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="7289d-216">Este conjunto de registros contiene los nombres de los servidores de nombres de Azure DNS asignados a la zona.</span><span class="sxs-lookup"><span data-stu-id="7289d-216">It contains the names of the Azure DNS name servers assigned to the zone.</span></span>

<span data-ttu-id="7289d-217">Puede agregar más servidores de nombres a este conjunto de registros NS, para admitir dominios de hospedaje conjunto con más de un proveedor DNS.</span><span class="sxs-lookup"><span data-stu-id="7289d-217">You can add additional name servers to this NS record set, to support co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="7289d-218">También puede modificar el TTL y los metadatos de este conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="7289d-218">You can also modify the TTL and metadata for this record set.</span></span> <span data-ttu-id="7289d-219">Sin embargo, no puede quitar ni modificar los servidores de nombres de Azure DNS rellenados previamente.</span><span class="sxs-lookup"><span data-stu-id="7289d-219">However, you cannot remove or modify the pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="7289d-220">Tenga en cuenta que esto solo se aplica al conjunto de registros NS en el vértice de zona.</span><span class="sxs-lookup"><span data-stu-id="7289d-220">Note that this applies only to the NS record set at the zone apex.</span></span> <span data-ttu-id="7289d-221">Otros conjuntos de registros NS de su zona (como los que se usan para delegar zonas secundarias) se pueden modificar sin restricciones.</span><span class="sxs-lookup"><span data-stu-id="7289d-221">Other NS record sets in your zone (as used to delegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="7289d-222">En el ejemplo siguiente se muestra cómo agregar un servidor de nombres adicional al conjunto de registros NS en el vértice de zona:</span><span class="sxs-lookup"><span data-stu-id="7289d-222">The following example shows how to add an additional name server to the NS record set at the zone apex:</span></span>

```azurecli
az network dns record-set ns set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --nsdname ns1.myotherdnsprovider.com 
```

### <a name="to-modify-the-ttl-of-an-existing-record-set"></a><span data-ttu-id="7289d-223">Para modificar el TTL de un conjunto de registros existente</span><span class="sxs-lookup"><span data-stu-id="7289d-223">To modify the TTL of an existing record set</span></span>

<span data-ttu-id="7289d-224">Para modificar el TTL de un conjunto de registros existente, utilice `azure network dns record-set <record-type> update`.</span><span class="sxs-lookup"><span data-stu-id="7289d-224">To modify the TTL of an existing record set, use `azure network dns record-set <record-type> update`.</span></span> <span data-ttu-id="7289d-225">Para obtener ayuda, consulte `azure network dns record-set <record-type> update --help`.</span><span class="sxs-lookup"><span data-stu-id="7289d-225">For help, see `azure network dns record-set <record-type> update --help`.</span></span>

<span data-ttu-id="7289d-226">En el ejemplo siguiente se muestra cómo modificar el TTL de un conjunto de registros, en este caso a 60 segundos:</span><span class="sxs-lookup"><span data-stu-id="7289d-226">The following example shows how to modify a record set TTL, in this case to 60 seconds:</span></span>

```azurecli
az network dns record-set a update --resource-group myresourcegroup --zone-name contoso.com --name www --set ttl=60
```

### <a name="to-modify-the-metadata-of-an-existing-record-set"></a><span data-ttu-id="7289d-227">Para modificar los metadatos de un conjunto de registros existente</span><span class="sxs-lookup"><span data-stu-id="7289d-227">To modify the metadata of an existing record set</span></span>

<span data-ttu-id="7289d-228">Se pueden usar [metadatos del conjunto de registros](dns-zones-records.md#tags-and-metadata) para asociar datos específicos de la aplicación con cada conjunto de registros como pares clave-valor.</span><span class="sxs-lookup"><span data-stu-id="7289d-228">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="7289d-229">Para modificar los metadatos de un conjunto de registros existente, utilice `az network dns record-set <record-type> update`.</span><span class="sxs-lookup"><span data-stu-id="7289d-229">To modify the metadata of an existing record set, use `az network dns record-set <record-type> update`.</span></span> <span data-ttu-id="7289d-230">Para obtener ayuda, consulte `az network dns record-set <record-type> update --help`.</span><span class="sxs-lookup"><span data-stu-id="7289d-230">For help, see `az network dns record-set <record-type> update --help`.</span></span>

<span data-ttu-id="7289d-231">En el ejemplo siguiente se muestra cómo crear un conjunto de registros con dos entradas de metadatos: "dept=finance" y "environment=production".</span><span class="sxs-lookup"><span data-stu-id="7289d-231">The following example shows how to modify a record set with two metadata entries, "dept=finance" and "environment=production".</span></span> <span data-ttu-id="7289d-232">Tenga en cuenta que los metadatos existentes se *sustituyen* por los valores especificados.</span><span class="sxs-lookup"><span data-stu-id="7289d-232">Note that any existing metadata is *replaced* by the values given.</span></span>

```azurecli
az network dns record-set a update --resource-group myresourcegroup --zone-name contoso.com --name www --set metadata.dept=finance metadata.environment=production
```

## <a name="delete-a-record-set"></a><span data-ttu-id="7289d-233">Eliminación de un conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="7289d-233">Delete a record set</span></span>

<span data-ttu-id="7289d-234">Los conjuntos de registros pueden eliminarse mediante el comando `az network dns record-set <record-type> delete`.</span><span class="sxs-lookup"><span data-stu-id="7289d-234">Record sets can be deleted by using the `az network dns record-set <record-type> delete` command.</span></span> <span data-ttu-id="7289d-235">Para obtener ayuda, consulte `azure network dns record-set <record-type> delete --help`.</span><span class="sxs-lookup"><span data-stu-id="7289d-235">For help, see `azure network dns record-set <record-type> delete --help`.</span></span> <span data-ttu-id="7289d-236">Al eliminar un conjunto de registros también se eliminan todos los registros que contiene.</span><span class="sxs-lookup"><span data-stu-id="7289d-236">Deleting a record set also deletes all records within the record set.</span></span>

> [!NOTE]
> <span data-ttu-id="7289d-237">No se pueden eliminar los conjuntos de registros SOA y NS en el vértice de zona (`--name "@"`).</span><span class="sxs-lookup"><span data-stu-id="7289d-237">You cannot delete the SOA and NS record sets at the zone apex (`--name "@"`).</span></span>  <span data-ttu-id="7289d-238">Se crean automáticamente cuando se crea la zona y se eliminan automáticamente cuando se elimina.</span><span class="sxs-lookup"><span data-stu-id="7289d-238">These are created automatically when the zone was created, and are deleted automatically when the zone is deleted.</span></span>

<span data-ttu-id="7289d-239">En el ejemplo siguiente se elimina el conjunto de registros con el nombre *www* de tipo A de la zona *contoso.com*, la cual se encuentra en el grupo de recursos *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="7289d-239">The following example deletes the record set named *www* of type A from the zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
az network dns record-set a delete --resource-group myresourcegroup --zone-name contoso.com --name www
```

<span data-ttu-id="7289d-240">Se le pide que confirme la operación de eliminación.</span><span class="sxs-lookup"><span data-stu-id="7289d-240">You are prompted to confirm the delete operation.</span></span> <span data-ttu-id="7289d-241">Para suprimir este mensaje, use el modificador `--yes`.</span><span class="sxs-lookup"><span data-stu-id="7289d-241">To suppress this prompt, use the `--yes` switch.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7289d-242">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7289d-242">Next steps</span></span>

<span data-ttu-id="7289d-243">Más información sobre [zonas y registros en Azure DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="7289d-243">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="7289d-244">Aprenda a [proteger las zonas y los registros](dns-protect-zones-recordsets.md) cuando se usa Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="7289d-244">Learn how to [protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
