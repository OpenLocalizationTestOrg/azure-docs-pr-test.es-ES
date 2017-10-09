---
title: registros DNS de aaaManage en DNS de Azure mediante Hola 2.0 de CLI de Azure | Documentos de Microsoft
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
ms.openlocfilehash: 9d6f8e74ebad55ccd2381fd84a830d2c7bbb1f30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-hello-azure-cli-20"></a><span data-ttu-id="b6015-104">Administrar registros DNS y los conjuntos de registros en DNS de Azure con hello 2.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="b6015-104">Manage DNS records and recordsets in Azure DNS using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b6015-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b6015-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="b6015-106">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="b6015-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="b6015-107">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="b6015-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="b6015-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b6015-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="b6015-109">Este artículo muestra cómo toomanage registros DNS para la zona DNS mediante el uso de Hola multiplataforma Azure interfaz de línea de comandos (CLI) 2.0, que está disponible para Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="b6015-109">This article shows you how toomanage DNS records for your DNS zone by using hello cross-platform Azure command-line interface (CLI) 2.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="b6015-110">También puede administrar los registros DNS mediante [Azure PowerShell](dns-operations-recordsets.md) o hello [portal de Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b6015-110">You can also manage your DNS records using [Azure PowerShell](dns-operations-recordsets.md) or hello [Azure portal](dns-operations-recordsets-portal.md).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="b6015-111">Tarea CLI versiones toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="b6015-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="b6015-112">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="b6015-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="b6015-113">[Azure 1.0 de CLI](dns-operations-recordsets-cli-nodejs.md) -nuestro CLI para modelos de implementación de administración de recursos y clásico Hola.</span><span class="sxs-lookup"><span data-stu-id="b6015-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="b6015-114">[Azure 2.0 CLI](dns-operations-recordsets-cli.md) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6015-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) - our next generation CLI for hello resource management deployment model.</span></span>

<span data-ttu-id="b6015-115">ejemplos de Hello en este artículo se supone que ya está [instalado Hola 2.0 de CLI de Azure, firmado y ha creado una zona DNS](dns-operations-dnszones-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b6015-115">hello examples in this article assume you have already [installed hello Azure CLI 2.0, signed in, and created a DNS zone](dns-operations-dnszones-cli.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="b6015-116">Introducción</span><span class="sxs-lookup"><span data-stu-id="b6015-116">Introduction</span></span>

<span data-ttu-id="b6015-117">Antes de crear los registros DNS en DNS de Azure, primero debe toounderstand cómo Azure DNS organiza los registros DNS en conjuntos de registros de DNS.</span><span class="sxs-lookup"><span data-stu-id="b6015-117">Before creating DNS records in Azure DNS, you first need toounderstand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="b6015-118">Para más información sobre los registros DNS en Azure DNS, consulte [DNS zones and records](dns-zones-records.md) (Zonas y registros DNS).</span><span class="sxs-lookup"><span data-stu-id="b6015-118">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>

## <a name="create-a-dns-record"></a><span data-ttu-id="b6015-119">Creación de un registro de DNS</span><span class="sxs-lookup"><span data-stu-id="b6015-119">Create a DNS record</span></span>

<span data-ttu-id="b6015-120">toocreate un registro DNS, usar hello `az network dns record-set <record-type> set-record` comando (donde `<record-type>` es de tipo hello de registro, es decir</span><span class="sxs-lookup"><span data-stu-id="b6015-120">toocreate a DNS record, use hello `az network dns record-set <record-type> set-record` command (where `<record-type>` is hello type of record, i.e</span></span> <span data-ttu-id="b6015-121">a, srv, txt, etc.) Para obtener ayuda, consulte `az network dns record-set --help`.</span><span class="sxs-lookup"><span data-stu-id="b6015-121">a, srv, txt, etc.) For help, see `az network dns record-set --help`.</span></span>

<span data-ttu-id="b6015-122">Al crear un registro, necesita el nombre de grupo de recursos de hello toospecify, nombre de la zona, conjunto de registros, nombre, tipo de registro de hello y detalles de Hola de registro de hello va a crear.</span><span class="sxs-lookup"><span data-stu-id="b6015-122">When creating a record, you need toospecify hello resource group name, zone name, record set name, hello record type, and hello details of hello record being created.</span></span> <span data-ttu-id="b6015-123">Hello dado el nombre de conjunto de registros debe ser un *relativa* nombre, lo que significa que debe excluir el nombre de la zona de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6015-123">hello record set name given must be a *relative* name, meaning it must exclude hello zone name.</span></span>

<span data-ttu-id="b6015-124">Si aún no existe el conjunto de registros de hello, este comando lo crea automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b6015-124">If hello record set does not already exist, this command creates it for you.</span></span> <span data-ttu-id="b6015-125">Si no existe registro de hello ya establecido, este comando agrega el registro de hello especificar toohello conjunto de registros existente.</span><span class="sxs-lookup"><span data-stu-id="b6015-125">If hello record set already exists, this command adds hello record you specify toohello existing record set.</span></span>

<span data-ttu-id="b6015-126">Si se crea un conjunto de registros, se utiliza el valor predeterminado del período de vida (3600).</span><span class="sxs-lookup"><span data-stu-id="b6015-126">If a new record set is created, a default time-to-live (TTL) of 3600 is used.</span></span> <span data-ttu-id="b6015-127">Para obtener instrucciones sobre cómo toouse TTLs diferentes, consulte [crear un conjunto de registros de DNS](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="b6015-127">For instructions on how toouse different TTLs, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="b6015-128">Hello en el ejemplo siguiente se crea un registro denominado *www* en zona de hello *contoso.com* en grupo de recursos de hello *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="b6015-128">hello following example creates an A record called *www* in hello zone *contoso.com* in hello resource group *MyResourceGroup*.</span></span> <span data-ttu-id="b6015-129">Hola dirección IP de un registro es de hello *1.2.3.4*.</span><span class="sxs-lookup"><span data-stu-id="b6015-129">hello IP address of hello A record is *1.2.3.4*.</span></span>

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 1.2.3.4
```

<span data-ttu-id="b6015-130">toocreate un registro se establece en vértice Hola de zona de hello (en este caso, "contoso.com"), use el nombre de registro de hello "@", incluidas las comillas de hello:</span><span class="sxs-lookup"><span data-stu-id="b6015-130">toocreate a record set in hello apex of hello zone (in this case, "contoso.com"), use hello record name "@", including hello quotation marks:</span></span>

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --ipv4-address 1.2.3.4
```

## <a name="create-a-dns-record-set"></a><span data-ttu-id="b6015-131">Creación de un conjunto de registros de DNS</span><span class="sxs-lookup"><span data-stu-id="b6015-131">Create a DNS record set</span></span>

<span data-ttu-id="b6015-132">Hola por encima de los ejemplos, registro DNS de Hola se cualquier agregado tooan existente de conjunto de registros, o se creó el conjunto de registros de hello *implícitamente*.</span><span class="sxs-lookup"><span data-stu-id="b6015-132">In hello above examples, hello DNS record was either added tooan existing record set, or hello record set was created *implicitly*.</span></span> <span data-ttu-id="b6015-133">También puede crear el conjunto de registros de hello *explícitamente* antes de que se agregan registros tooit.</span><span class="sxs-lookup"><span data-stu-id="b6015-133">You can also create hello record set *explicitly* before adding records tooit.</span></span> <span data-ttu-id="b6015-134">DNS de Azure es compatible con conjuntos de registros 'empty', que pueden actuar como un marcador de posición tooreserve un nombre DNS antes de crear los registros DNS.</span><span class="sxs-lookup"><span data-stu-id="b6015-134">Azure DNS supports 'empty' record sets, which can act as a placeholder tooreserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="b6015-135">Conjuntos de registros vacíos son visibles en hello Azure DNS control plano, pero no aparecen en los servidores de nombres DNS de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="b6015-135">Empty record sets are visible in hello Azure DNS control plane, but do not appear on hello Azure DNS name servers.</span></span>

<span data-ttu-id="b6015-136">Conjuntos de registros se crean mediante hello `az network dns record-set <record-type> create` comando.</span><span class="sxs-lookup"><span data-stu-id="b6015-136">Record sets are created using hello `az network dns record-set <record-type> create` command.</span></span> <span data-ttu-id="b6015-137">Para obtener ayuda, consulte `az network dns record-set <record-type> create --help`.</span><span class="sxs-lookup"><span data-stu-id="b6015-137">For help, see `az network dns record-set <record-type> create --help`.</span></span>

<span data-ttu-id="b6015-138">Crear registro de hello establecen explícitamente permite toospecify propiedades de conjunto de registros como hello [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) y metadatos.</span><span class="sxs-lookup"><span data-stu-id="b6015-138">Creating hello record set explicitly allows you toospecify record set properties such as hello [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) and metadata.</span></span> <span data-ttu-id="b6015-139">[Metadatos del conjunto de registros](dns-zones-records.md#tags-and-metadata) pueden ser datos específicos de la aplicación de tooassociate usado con cada conjunto de registros, como pares de clave-valor.</span><span class="sxs-lookup"><span data-stu-id="b6015-139">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="b6015-140">Hello en el ejemplo siguiente se crea un conjunto de registros vacío de tipo 'A' con un TTL de 60 segundos, mediante el uso de hello `--ttl` parámetro (forma abreviada `-l`):</span><span class="sxs-lookup"><span data-stu-id="b6015-140">hello following example creates an empty record set of type 'A' with a 60-second TTL, by using hello `--ttl` parameter (short form `-l`):</span></span>

```azurecli
az network dns record-set a create --resource-group myresourcegroup --zone-name contoso.com --name www --ttl 60
```

<span data-ttu-id="b6015-141">Hello en el ejemplo siguiente se crea un conjunto de registros con dos entradas de metadatos, "departamento = Finanzas" y "entorno = producción", mediante el uso de hello `--metadata` parámetro:</span><span class="sxs-lookup"><span data-stu-id="b6015-141">hello following example creates a record set with two metadata entries, "dept=finance" and "environment=production", by using hello `--metadata` parameter :</span></span>

```azurecli
az network dns record-set a create --resource-group myresourcegroup --zone-name contoso.com --name www --metadata "dept=finance" "environment=production"
```

<span data-ttu-id="b6015-142">Tras haber creado un conjunto de registros vacío, se podrán añadir el registro mediante `azure network dns record-set <record-type> set-record`, como se describe en [Creación de un registro de DNS](#create-a-dns-record).</span><span class="sxs-lookup"><span data-stu-id="b6015-142">Having created an empty record set, records can be added using `azure network dns record-set <record-type> set-record` as described in [Create a DNS record](#create-a-dns-record).</span></span>

## <a name="create-records-of-other-types"></a><span data-ttu-id="b6015-143">Creación de registros de otros tipos</span><span class="sxs-lookup"><span data-stu-id="b6015-143">Create records of other types</span></span>

<span data-ttu-id="b6015-144">Después de ver en detalle cómo registros toocreate 'A', Hola siguientes ejemplos se muestra cómo se admite toocreate registro de otros tipos de registros DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="b6015-144">Having seen in detail how toocreate 'A' records, hello following examples show how toocreate record of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="b6015-145">parámetros de Hello usar registro de hello toospecify datos varían según el tipo de saludo del registro de hello.</span><span class="sxs-lookup"><span data-stu-id="b6015-145">hello parameters used toospecify hello record data vary depending on hello type of hello record.</span></span> <span data-ttu-id="b6015-146">Por ejemplo, para un registro de tipo "A", especificar dirección Hola IPv4 con el parámetro hello `--ipv4-address <IPv4 address>`.</span><span class="sxs-lookup"><span data-stu-id="b6015-146">For example, for a record of type "A", you specify hello IPv4 address with hello parameter `--ipv4-address <IPv4 address>`.</span></span> <span data-ttu-id="b6015-147">Hola parámetros para cada tipo de registro puede aparecer con `az network dns record-set <record-type> set-record --help`.</span><span class="sxs-lookup"><span data-stu-id="b6015-147">hello parameters for each record type can be listed using `az network dns record-set <record-type> set-record --help`.</span></span>

<span data-ttu-id="b6015-148">En cada caso, le mostramos cómo toocreate un único registro.</span><span class="sxs-lookup"><span data-stu-id="b6015-148">In each case, we show how toocreate a single record.</span></span> <span data-ttu-id="b6015-149">registro de Hello es agregado toohello existente de conjunto de registros o un conjunto de registros se crea de forma implícita.</span><span class="sxs-lookup"><span data-stu-id="b6015-149">hello record is added toohello existing record set, or a record set created implicitly.</span></span> <span data-ttu-id="b6015-150">Para obtener más información sobre cómo crear conjuntos de registros y definir explícitamente los parámetros de un conjunto de registros, consulte [Creación de un conjunto de registros de DNS](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="b6015-150">For more information on creating record sets and defining record set parameter explicitly, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="b6015-151">No damos un toocreate ejemplo un conjunto de registros SOA, ya que se crea SOA y eliminar con cada zona DNS y no puede crearse o eliminarse por separado.</span><span class="sxs-lookup"><span data-stu-id="b6015-151">We do not give an example toocreate an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="b6015-152">Sin embargo, [Hola SOA se puede modificar, como se muestra en un ejemplo posterior](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="b6015-152">However, [hello SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record"></a><span data-ttu-id="b6015-153">Creación de un registro AAAA</span><span class="sxs-lookup"><span data-stu-id="b6015-153">Create an AAAA record</span></span>

```azurecli
az network dns record-set aaaa set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-aaaa --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a><span data-ttu-id="b6015-154">Creación de un registro CNAME</span><span class="sxs-lookup"><span data-stu-id="b6015-154">Create a CNAME record</span></span>

> [!NOTE]
> <span data-ttu-id="b6015-155">los estándares de DNS Hello no permiten registros CNAME en vértice Hola de una zona (`--Name "@"`), ni permiten a los conjuntos de registros que contiene más de un registro.</span><span class="sxs-lookup"><span data-stu-id="b6015-155">hello DNS standards do not permit CNAME records at hello apex of a zone (`--Name "@"`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="b6015-156">Para más información, consulte [Registros CNAME](dns-zones-records.md#cname-records).</span><span class="sxs-lookup"><span data-stu-id="b6015-156">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>

```azurecli
az network dns record-set cname set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-cname --cname www.contoso.com
```

### <a name="create-an-mx-record"></a><span data-ttu-id="b6015-157">Creación de un registro MX</span><span class="sxs-lookup"><span data-stu-id="b6015-157">Create an MX record</span></span>

<span data-ttu-id="b6015-158">En este ejemplo, se utiliza el nombre de conjunto de registros de Hola "@" hello toocreate registro MX en vértice de la zona de hello (en este caso, "contoso.com").</span><span class="sxs-lookup"><span data-stu-id="b6015-158">In this example, we use hello record set name "@" toocreate hello MX record at hello zone apex (in this case, "contoso.com").</span></span>

```azurecli
az network dns record-set mx set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a><span data-ttu-id="b6015-159">Creación de un registro NS</span><span class="sxs-lookup"><span data-stu-id="b6015-159">Create an NS record</span></span>

```azurecli
az network dns record-set ns set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-ns --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a><span data-ttu-id="b6015-160">Creación de un registro PTR</span><span class="sxs-lookup"><span data-stu-id="b6015-160">Create a PTR record</span></span>

<span data-ttu-id="b6015-161">En este caso, ' Mi-arpa-zone.com' representa Hola zona ARPA que representa el intervalo de IP.</span><span class="sxs-lookup"><span data-stu-id="b6015-161">In this case, 'my-arpa-zone.com' represents hello ARPA zone representing your IP range.</span></span> <span data-ttu-id="b6015-162">Cada registro PTR establecida en esta zona corresponde tooan dirección IP dentro de este intervalo IP.</span><span class="sxs-lookup"><span data-stu-id="b6015-162">Each PTR record set in this zone corresponds tooan IP address within this IP range.</span></span>  <span data-ttu-id="b6015-163">Hola último octeto de la dirección IP de hello dentro de este intervalo IP representado por este registro es el nombre de registro de Hello '10'.</span><span class="sxs-lookup"><span data-stu-id="b6015-163">hello record name '10' is hello last octet of hello IP address within this IP range represented by this record.</span></span>

```azurecli
az network dns record-set ptr set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name my-arpa.zone.com --ptrdname myservice.contoso.com
```

### <a name="create-an-srv-record"></a><span data-ttu-id="b6015-164">Creación de un registro SRV</span><span class="sxs-lookup"><span data-stu-id="b6015-164">Create an SRV record</span></span>

<span data-ttu-id="b6015-165">Al crear un [conjunto de registros SRV](dns-zones-records.md#srv-records), especifique hello  *\_servicio* y  *\_protocolo* Hola nombre de conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="b6015-165">When creating an [SRV record set](dns-zones-records.md#srv-records), specify hello *\_service* and *\_protocol* in hello record set name.</span></span> <span data-ttu-id="b6015-166">No hay ninguna necesidad de tooinclude "@" Hola registro establece el nombre al crear un registro SRV en vértice de la zona de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6015-166">There is no need tooinclude "@" in hello record set name when creating an SRV record set at hello zone apex.</span></span>

```azurecli
az network dns record-set srv set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name _sip._tls --priority 10 --weight 5 --port 8080 --target sip.contoso.com
```

### <a name="create-a-txt-record"></a><span data-ttu-id="b6015-167">Creación de un registro TXT</span><span class="sxs-lookup"><span data-stu-id="b6015-167">Create a TXT record</span></span>

<span data-ttu-id="b6015-168">Hello en el ejemplo siguiente se muestra cómo registrar toocreate TXT.</span><span class="sxs-lookup"><span data-stu-id="b6015-168">hello following example shows how toocreate a TXT record.</span></span> <span data-ttu-id="b6015-169">Para obtener más información acerca de la longitud de cadena máxima Hola admitida en registros TXT, consulte [registros TXT](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="b6015-169">For more information about hello maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```azurecli
az network dns record-set txt set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-txt --value "This is a TXT record"
```

## <a name="get-a-record-set"></a><span data-ttu-id="b6015-170">Recuperación de un conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="b6015-170">Get a record set</span></span>

<span data-ttu-id="b6015-171">tooretrieve un conjunto de registros existente, utilice `az network dns record-set <record-type> show`.</span><span class="sxs-lookup"><span data-stu-id="b6015-171">tooretrieve an existing record set, use `az network dns record-set <record-type> show`.</span></span> <span data-ttu-id="b6015-172">Para obtener ayuda, consulte `az network dns record-set <record-type> show --help`.</span><span class="sxs-lookup"><span data-stu-id="b6015-172">For help, see `az network dns record-set <record-type> show --help`.</span></span>

<span data-ttu-id="b6015-173">Al crear un registro o un conjunto de registros, registro de hello establecer nombre dado debe ser un *relativa* nombre, lo que significa que debe excluir el nombre de la zona de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6015-173">As when creating a record or record set, hello record set name given must be a *relative* name, meaning it must exclude hello zone name.</span></span> <span data-ttu-id="b6015-174">También necesita toospecify tipo de registro de hello, zona Hola que contiene el registro de hello establecido y Hola grupo de recursos que contiene la zona de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6015-174">You also need toospecify hello record type, hello zone containing hello record set, and hello resource group containing hello zone.</span></span>

<span data-ttu-id="b6015-175">Hello en el ejemplo siguiente se recupera el registro de hello *www* de un tipo de zona *contoso.com* en grupo de recursos *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="b6015-175">hello following example retrieves hello record *www* of type A from zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
az network dns record-set a show --resource-group myresourcegroup --zone-name contoso.com --name www
```

## <a name="list-record-sets"></a><span data-ttu-id="b6015-176">Enumeración de conjuntos de registros</span><span class="sxs-lookup"><span data-stu-id="b6015-176">List record sets</span></span>

<span data-ttu-id="b6015-177">Puede enumerar todos los registros de una zona DNS mediante hello `az network dns record-set list` comando.</span><span class="sxs-lookup"><span data-stu-id="b6015-177">You can list all records in a DNS zone by using hello `az network dns record-set list` command.</span></span> <span data-ttu-id="b6015-178">Para obtener ayuda, consulte `az network dns record-set list --help`.</span><span class="sxs-lookup"><span data-stu-id="b6015-178">For help, see `az network dns record-set list --help`.</span></span>

<span data-ttu-id="b6015-179">Este ejemplo devuelve todos los registros se establece en la zona de hello *contoso.com*, en el grupo de recursos *MyResourceGroup*independientemente del nombre o tipo de registro:</span><span class="sxs-lookup"><span data-stu-id="b6015-179">This example returns all record sets in hello zone *contoso.com*, in resource group *MyResourceGroup*, regardless of name or record type:</span></span>

```azurecli
az network dns record-set list --resource-group myresourcegroup --zone-name contoso.com
```

<span data-ttu-id="b6015-180">Este ejemplo devuelve todos los conjuntos de registros que coinciden con hello tiene el tipo de registro (en este caso, 'A' registros):</span><span class="sxs-lookup"><span data-stu-id="b6015-180">This example returns all record sets that match hello given record type (in this case, 'A' records):</span></span>

```azurecli
az network dns record-set a list --resource-group myresourcegroup --zone-name contoso.com 
```

## <a name="add-a-record-tooan-existing-record-set"></a><span data-ttu-id="b6015-181">Agregar un registro tooan existente de conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="b6015-181">Add a record tooan existing record set</span></span>

<span data-ttu-id="b6015-182">Puede usar `az network dns record-set <record-type> set-record` ambas toocreate un registro en un nuevo registro configurado o tooadd un registro existente tooan registros.</span><span class="sxs-lookup"><span data-stu-id="b6015-182">You can use `az network dns record-set <record-type> set-record` both toocreate a record in a new record set, or tooadd a record tooan existing record set.</span></span>

<span data-ttu-id="b6015-183">Para obtener más información, consulte las secciones [Creación de un registro de DNS](#create-a-dns-record) y [Creación de registros de otros tipos](#create-records-of-other-types).</span><span class="sxs-lookup"><span data-stu-id="b6015-183">For more information, see [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="b6015-184">Quite un registro de un conjunto de registros existente.</span><span class="sxs-lookup"><span data-stu-id="b6015-184">Remove a record from an existing record set.</span></span>

<span data-ttu-id="b6015-185">grabar tooremove un DNS de un conjunto de registros existente, use `az network dns record-set <record-type> remove-record`.</span><span class="sxs-lookup"><span data-stu-id="b6015-185">tooremove a DNS record from an existing record set, use `az network dns record-set <record-type> remove-record`.</span></span> <span data-ttu-id="b6015-186">Para obtener ayuda, consulte `az network dns record-set <record-type> remove-record -h`.</span><span class="sxs-lookup"><span data-stu-id="b6015-186">For help, see `az network dns record-set <record-type> remove-record -h`.</span></span>

<span data-ttu-id="b6015-187">Este comando elimina un registro de DNS de un conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="b6015-187">This command deletes a DNS record from a record set.</span></span> <span data-ttu-id="b6015-188">Si se elimina el último registro de hello en un conjunto de registros, también se elimina el registro de hello configurarse automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b6015-188">If hello last record in a record set is deleted, hello record set itself is also deleted.</span></span> <span data-ttu-id="b6015-189">conjunto de registros tookeep Hola vacía en su lugar, use hello `--keep-empty-record-set` opción.</span><span class="sxs-lookup"><span data-stu-id="b6015-189">tookeep hello empty record set instead, use hello `--keep-empty-record-set` option.</span></span>

<span data-ttu-id="b6015-190">Necesita toospecify hello toobe registro eliminado y la zona de Hola debe eliminarse, con Hola mismos parámetros que al crear un registro mediante `az network dns record-set <record-type> set-record`.</span><span class="sxs-lookup"><span data-stu-id="b6015-190">You need toospecify hello record toobe deleted and hello zone it should be deleted from, using hello same parameters as when creating a record using `az network dns record-set <record-type> set-record`.</span></span> <span data-ttu-id="b6015-191">Estos parámetros se describen en las secciones [Creación de un registro de DNS](#create-a-dns-record) y [Creación de registros de otros tipos](#create-records-of-other-types).</span><span class="sxs-lookup"><span data-stu-id="b6015-191">These parameters are described in [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

<span data-ttu-id="b6015-192">Después de eliminaciones de ejemplo de Hola Hola un registro con valor '1.2.3.4' del registro de hello conjunto con nombre *www* en zona de hello *contoso.com*, en el grupo de recursos de hello *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="b6015-192">hello following example deletes hello A record with value '1.2.3.4' from hello record set named *www* in hello zone *contoso.com*, in hello resource group *MyResourceGroup*.</span></span>

```azurecli
az network dns record-set a remove-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "www" --ipv4-address 1.2.3.4
```

## <a name="modify-an-existing-record-set"></a><span data-ttu-id="b6015-193">Modificación de un conjunto de registros existente</span><span class="sxs-lookup"><span data-stu-id="b6015-193">Modify an existing record set</span></span>

<span data-ttu-id="b6015-194">Cada conjunto de registros contiene un [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadatos](dns-zones-records.md#tags-and-metadata)y los registros de DNS.</span><span class="sxs-lookup"><span data-stu-id="b6015-194">Each record set contains a [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadata](dns-zones-records.md#tags-and-metadata), and DNS records.</span></span> <span data-ttu-id="b6015-195">Hello siguientes secciones se explica cómo toomodify de estas propiedades.</span><span class="sxs-lookup"><span data-stu-id="b6015-195">hello following sections explain how toomodify each of these properties.</span></span>

### <a name="toomodify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a><span data-ttu-id="b6015-196">toomodify un registro A, AAAA, MX, NS, PTR, SRV o TXT</span><span class="sxs-lookup"><span data-stu-id="b6015-196">toomodify an A, AAAA, MX, NS, PTR, SRV, or TXT record</span></span>

<span data-ttu-id="b6015-197">toomodify un registro existente de tipo A, AAAA, MX, NS, PTR, SRV o TXT, primero debe agregar un nuevo registro y, a continuación, un registro existente de Hola de eliminación.</span><span class="sxs-lookup"><span data-stu-id="b6015-197">toomodify an existing record of type A, AAAA, MX, NS, PTR, SRV, or TXT, you should first add a new record and then delete hello existing record.</span></span> <span data-ttu-id="b6015-198">Para obtener instrucciones detalladas sobre cómo toodelete y agregar registros, vea hello las secciones anteriores de este artículo.</span><span class="sxs-lookup"><span data-stu-id="b6015-198">For detailed instructions on how toodelete and add records, see hello earlier sections of this article.</span></span>

<span data-ttu-id="b6015-199">Hola de ejemplo siguiente muestra cómo toomodify un registro de 'A', de IP dirección 1.2.3.4 tooIP direccionan 5.6.7.8:</span><span class="sxs-lookup"><span data-stu-id="b6015-199">hello following example shows how toomodify an 'A' record, from IP address 1.2.3.4 tooIP address 5.6.7.8:</span></span>

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 5.6.7.8
az network dns record-set a remove-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 1.2.3.4
```

<span data-ttu-id="b6015-200">No se puede agregar, quitar o modificar los registros de Hola Hola creado automáticamente el registro NS establecido en vértice de la zona de hello (`--Name "@"`, incluidas las comillas).</span><span class="sxs-lookup"><span data-stu-id="b6015-200">You cannot add, remove, or modify hello records in hello automatically created NS record set at hello zone apex (`--Name "@"`, including quote marks).</span></span> <span data-ttu-id="b6015-201">Para este conjunto de registros, cambios solo Hola permitidos son registro de hello toomodify establece TTL y metadatos.</span><span class="sxs-lookup"><span data-stu-id="b6015-201">For this record set, hello only changes permitted are toomodify hello record set TTL and metadata.</span></span>

### <a name="toomodify-a-cname-record"></a><span data-ttu-id="b6015-202">toomodify un registro CNAME</span><span class="sxs-lookup"><span data-stu-id="b6015-202">toomodify a CNAME record</span></span>

<span data-ttu-id="b6015-203">A diferencia de la mayoría de otros tipos de registros, un conjunto de registros CNAME solo puede contener un único registro.</span><span class="sxs-lookup"><span data-stu-id="b6015-203">Unlike most other record types, a CNAME record set can only contain a single record.</span></span>  <span data-ttu-id="b6015-204">Por lo tanto, no se puede reemplazar el valor actual de hello agregando un nuevo registro y quitar el registro existente de hello, que para otros tipos de registros.</span><span class="sxs-lookup"><span data-stu-id="b6015-204">Therefore, you cannot replace hello current value by adding a new record and removing hello existing record, as for other record types.</span></span>

<span data-ttu-id="b6015-205">En su lugar, use un registro CNAME, toomodify `az network dns record-set cname set-record`.</span><span class="sxs-lookup"><span data-stu-id="b6015-205">Instead, toomodify a CNAME record, use `az network dns record-set cname set-record`.</span></span> <span data-ttu-id="b6015-206">Para obtener ayuda, consulte `az network dns record-set cname set-record --help`.</span><span class="sxs-lookup"><span data-stu-id="b6015-206">For help, see `az network dns record-set cname set-record --help`</span></span>

<span data-ttu-id="b6015-207">ejemplo Hello modifica conjunto de registros CNAME de hello *www* en zona de hello *contoso.com*, en el grupo de recursos *MyResourceGroup*, toopoint demasiado 'www.fabrikam.net' en lugar de su valor existente:</span><span class="sxs-lookup"><span data-stu-id="b6015-207">hello example modifies hello CNAME record set *www* in hello zone *contoso.com*, in resource group *MyResourceGroup*, toopoint too'www.fabrikam.net' instead of its existing value:</span></span>

```azurecli
az network dns record-set cname set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-cname --cname www.fabrikam.net
``` 

### <a name="toomodify-an-soa-record"></a><span data-ttu-id="b6015-208">toomodify un registro SOA</span><span class="sxs-lookup"><span data-stu-id="b6015-208">toomodify an SOA record</span></span>

<span data-ttu-id="b6015-209">A diferencia de la mayoría de otros tipos de registros, un conjunto de registros CNAME solo puede contener un único registro.</span><span class="sxs-lookup"><span data-stu-id="b6015-209">Unlike most other record types, a CNAME record set can only contain a single record.</span></span>  <span data-ttu-id="b6015-210">Por lo tanto, no se puede reemplazar el valor actual de hello agregando un nuevo registro y quitar el registro existente de hello, que para otros tipos de registros.</span><span class="sxs-lookup"><span data-stu-id="b6015-210">Therefore, you cannot replace hello current value by adding a new record and removing hello existing record, as for other record types.</span></span>

<span data-ttu-id="b6015-211">En su lugar, use toomodify Hola registro SOA, `az network dns record-set soa update`.</span><span class="sxs-lookup"><span data-stu-id="b6015-211">Instead, toomodify hello SOA record, use `az network dns record-set soa update`.</span></span> <span data-ttu-id="b6015-212">Para obtener ayuda, consulte `az network dns record-set soa update --help`.</span><span class="sxs-lookup"><span data-stu-id="b6015-212">For help, see `az network dns record-set soa update --help`.</span></span>

<span data-ttu-id="b6015-213">Hello en el ejemplo siguiente se muestra cómo registrar propiedad tooset Hola "email" Hola SOA de zona de hello *contoso.com* en grupo de recursos de hello *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="b6015-213">hello following example shows how tooset hello 'email' property of hello SOA record for hello zone *contoso.com* in hello resource group *MyResourceGroup*:</span></span>

```azurecli
az network dns record-set soa update --resource-group myresourcegroup --zone-name contoso.com --email admin.contoso.com
```

### <a name="toomodify-ns-records-at-hello-zone-apex"></a><span data-ttu-id="b6015-214">registros de toomodify NS en vértice de la zona de Hola</span><span class="sxs-lookup"><span data-stu-id="b6015-214">toomodify NS records at hello zone apex</span></span>

<span data-ttu-id="b6015-215">registro de NS de Hello establecido en vértice de la zona de Hola se crea automáticamente con cada zona DNS.</span><span class="sxs-lookup"><span data-stu-id="b6015-215">hello NS record set at hello zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="b6015-216">Contiene los nombres de Hola de zona de hello Azure DNS nombre servidores toohello asignado.</span><span class="sxs-lookup"><span data-stu-id="b6015-216">It contains hello names of hello Azure DNS name servers assigned toohello zone.</span></span>

<span data-ttu-id="b6015-217">Puede agregar nombre adicionales servidores toothis NS conjunto de registros, toosupport alojar conjuntamente dominios con más de un proveedor DNS.</span><span class="sxs-lookup"><span data-stu-id="b6015-217">You can add additional name servers toothis NS record set, toosupport co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="b6015-218">También puede modificar Hola TTL y los metadatos para este conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="b6015-218">You can also modify hello TTL and metadata for this record set.</span></span> <span data-ttu-id="b6015-219">Sin embargo, no se puede quitar o modificar servidores de nombres DNS de Azure previamente rellenados Hola.</span><span class="sxs-lookup"><span data-stu-id="b6015-219">However, you cannot remove or modify hello pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="b6015-220">Tenga en cuenta que esto se aplica solo toohello NS conjunto de registros en vértice de la zona de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6015-220">Note that this applies only toohello NS record set at hello zone apex.</span></span> <span data-ttu-id="b6015-221">Otros conjuntos de registros NS en su zona (como las zonas secundarias de toodelegate usado) pueden modificarse sin restricción.</span><span class="sxs-lookup"><span data-stu-id="b6015-221">Other NS record sets in your zone (as used toodelegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="b6015-222">Hola de ejemplo siguiente muestra cómo tooadd establece de un registro de NS de toohello de servidor de nombres adicionales en vértice de la zona de hello:</span><span class="sxs-lookup"><span data-stu-id="b6015-222">hello following example shows how tooadd an additional name server toohello NS record set at hello zone apex:</span></span>

```azurecli
az network dns record-set ns set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --nsdname ns1.myotherdnsprovider.com 
```

### <a name="toomodify-hello-ttl-of-an-existing-record-set"></a><span data-ttu-id="b6015-223">establece toomodify Hola TTL de un registro existente</span><span class="sxs-lookup"><span data-stu-id="b6015-223">toomodify hello TTL of an existing record set</span></span>

<span data-ttu-id="b6015-224">establece toomodify Hola TTL de un registro existente, use `azure network dns record-set <record-type> update`.</span><span class="sxs-lookup"><span data-stu-id="b6015-224">toomodify hello TTL of an existing record set, use `azure network dns record-set <record-type> update`.</span></span> <span data-ttu-id="b6015-225">Para obtener ayuda, consulte `azure network dns record-set <record-type> update --help`.</span><span class="sxs-lookup"><span data-stu-id="b6015-225">For help, see `azure network dns record-set <record-type> update --help`.</span></span>

<span data-ttu-id="b6015-226">Hola de ejemplo siguiente muestra cómo toomodify un conjunto de registros TTL, en este caso a too60 segundos:</span><span class="sxs-lookup"><span data-stu-id="b6015-226">hello following example shows how toomodify a record set TTL, in this case too60 seconds:</span></span>

```azurecli
az network dns record-set a update --resource-group myresourcegroup --zone-name contoso.com --name www --set ttl=60
```

### <a name="toomodify-hello-metadata-of-an-existing-record-set"></a><span data-ttu-id="b6015-227">toomodify Hola metadatos de un conjunto de registros existente</span><span class="sxs-lookup"><span data-stu-id="b6015-227">toomodify hello metadata of an existing record set</span></span>

<span data-ttu-id="b6015-228">[Metadatos del conjunto de registros](dns-zones-records.md#tags-and-metadata) pueden ser datos específicos de la aplicación de tooassociate usado con cada conjunto de registros, como pares de clave-valor.</span><span class="sxs-lookup"><span data-stu-id="b6015-228">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="b6015-229">establecen toomodify Hola metadatos de un registro existente, use `az network dns record-set <record-type> update`.</span><span class="sxs-lookup"><span data-stu-id="b6015-229">toomodify hello metadata of an existing record set, use `az network dns record-set <record-type> update`.</span></span> <span data-ttu-id="b6015-230">Para obtener ayuda, consulte `az network dns record-set <record-type> update --help`.</span><span class="sxs-lookup"><span data-stu-id="b6015-230">For help, see `az network dns record-set <record-type> update --help`.</span></span>

<span data-ttu-id="b6015-231">Hello en el ejemplo siguiente se muestra cómo toomodify un conjunto de registros con dos entradas de metadatos, "departamento = Finanzas" y "entorno = producción".</span><span class="sxs-lookup"><span data-stu-id="b6015-231">hello following example shows how toomodify a record set with two metadata entries, "dept=finance" and "environment=production".</span></span> <span data-ttu-id="b6015-232">Tenga en cuenta que los metadatos existentes *reemplaza* por valores de hello dados.</span><span class="sxs-lookup"><span data-stu-id="b6015-232">Note that any existing metadata is *replaced* by hello values given.</span></span>

```azurecli
az network dns record-set a update --resource-group myresourcegroup --zone-name contoso.com --name www --set metadata.dept=finance metadata.environment=production
```

## <a name="delete-a-record-set"></a><span data-ttu-id="b6015-233">Eliminación de un conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="b6015-233">Delete a record set</span></span>

<span data-ttu-id="b6015-234">Conjuntos de registros pueden eliminarse mediante el uso de hello `az network dns record-set <record-type> delete` comando.</span><span class="sxs-lookup"><span data-stu-id="b6015-234">Record sets can be deleted by using hello `az network dns record-set <record-type> delete` command.</span></span> <span data-ttu-id="b6015-235">Para obtener ayuda, consulte `azure network dns record-set <record-type> delete --help`.</span><span class="sxs-lookup"><span data-stu-id="b6015-235">For help, see `azure network dns record-set <record-type> delete --help`.</span></span> <span data-ttu-id="b6015-236">Eliminación de un conjunto de registros, también elimina todas las entradas de conjunto de registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6015-236">Deleting a record set also deletes all records within hello record set.</span></span>

> [!NOTE]
> <span data-ttu-id="b6015-237">No se puede eliminar Hola SOA y NS conjuntos de registros en vértice de la zona de hello (`--name "@"`).</span><span class="sxs-lookup"><span data-stu-id="b6015-237">You cannot delete hello SOA and NS record sets at hello zone apex (`--name "@"`).</span></span>  <span data-ttu-id="b6015-238">Se crean automáticamente cuando se creó zona hello y se eliminan automáticamente cuando se elimina la zona de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6015-238">These are created automatically when hello zone was created, and are deleted automatically when hello zone is deleted.</span></span>

<span data-ttu-id="b6015-239">Hello en el ejemplo siguiente se elimina conjunto con nombre de registros de hello *www* de un tipo de zona de hello *contoso.com* en grupo de recursos *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="b6015-239">hello following example deletes hello record set named *www* of type A from hello zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
az network dns record-set a delete --resource-group myresourcegroup --zone-name contoso.com --name www
```

<span data-ttu-id="b6015-240">Son la operación de eliminación de hello tooconfirm solicitadas.</span><span class="sxs-lookup"><span data-stu-id="b6015-240">You are prompted tooconfirm hello delete operation.</span></span> <span data-ttu-id="b6015-241">toosuppress este símbolo del sistema, use hello `--yes` cambiar.</span><span class="sxs-lookup"><span data-stu-id="b6015-241">toosuppress this prompt, use hello `--yes` switch.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6015-242">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b6015-242">Next steps</span></span>

<span data-ttu-id="b6015-243">Más información sobre [zonas y registros en Azure DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="b6015-243">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="b6015-244">Obtenga información acerca de cómo demasiado[proteger sus zonas y registros](dns-protect-zones-recordsets.md) cuando se usa DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="b6015-244">Learn how too[protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
