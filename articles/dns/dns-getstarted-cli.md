---
title: aaaGet iniciado en el DNS de Azure mediante Azure CLI 2.0 | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate un DNS zona y este registro de DNS de Azure. Esto es una guía paso a paso toocreate y administrar la primera zona DNS y el registro mediante Hola 2.0 de CLI de Azure."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 8a894941e9910d5cc35394a1be9dbca9792613f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-20"></a><span data-ttu-id="adf33-104">Introducción a Azure DNS con la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="adf33-104">Get started with Azure DNS using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="adf33-105">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="adf33-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="adf33-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="adf33-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="adf33-107">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="adf33-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="adf33-108">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="adf33-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="adf33-109">Este artículo le guiará a través de hello pasos toocreate la primera zona DNS y registro mediante Hola multiplataforma Azure CLI 2.0, que está disponible para Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="adf33-109">This article walks you through hello steps toocreate your first DNS zone and record using hello cross-platform Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="adf33-110">También puede realizar estos pasos con el portal de Azure de Hola o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="adf33-110">You can also perform these steps using hello Azure portal or Azure PowerShell.</span></span>

<span data-ttu-id="adf33-111">Una zona DNS es toohost usado Hola registros DNS para un dominio en particular.</span><span class="sxs-lookup"><span data-stu-id="adf33-111">A DNS zone is used toohost hello DNS records for a particular domain.</span></span> <span data-ttu-id="adf33-112">toostart hospedaje de su dominio de DNS de Azure, necesita toocreate una zona DNS para ese nombre de dominio.</span><span class="sxs-lookup"><span data-stu-id="adf33-112">toostart hosting your domain in Azure DNS, you need toocreate a DNS zone for that domain name.</span></span> <span data-ttu-id="adf33-113">Cada registro DNS del dominio se crea luego en esta zona DNS.</span><span class="sxs-lookup"><span data-stu-id="adf33-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="adf33-114">Por último, toopublish su DNS de la zona toohello Internet, necesitará servidores de nombres de hello tooconfigure para dominio de Hola.</span><span class="sxs-lookup"><span data-stu-id="adf33-114">Finally, toopublish your DNS zone toohello Internet, you need tooconfigure hello name servers for hello domain.</span></span> <span data-ttu-id="adf33-115">A continuación, se describen cada uno de estos pasos.</span><span class="sxs-lookup"><span data-stu-id="adf33-115">Each of these steps is described below.</span></span>

<span data-ttu-id="adf33-116">Estas instrucciones se supone que ya haya instalado y firmado en tooAzure 2.0 de CLI.</span><span class="sxs-lookup"><span data-stu-id="adf33-116">These instructions assume you have already installed and signed in tooAzure CLI 2.0.</span></span> <span data-ttu-id="adf33-117">Para obtener ayuda, consulte [cómo toomanage DNS zonas mediante Azure CLI 2.0](dns-operations-dnszones-cli.md).</span><span class="sxs-lookup"><span data-stu-id="adf33-117">For help, see [How toomanage DNS zones using Azure CLI 2.0](dns-operations-dnszones-cli.md).</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="adf33-118">Crear grupo de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="adf33-118">Create hello resource group</span></span>

<span data-ttu-id="adf33-119">Antes de crear la zona DNS de hello, un grupo de recursos se crea la zona DNS de toocontain Hola.</span><span class="sxs-lookup"><span data-stu-id="adf33-119">Before creating hello DNS zone, a resource group is created toocontain hello DNS Zone.</span></span> <span data-ttu-id="adf33-120">siguiente Hello muestra comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="adf33-120">hello following shows hello command.</span></span>

```azurecli
az group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="adf33-121">Creación de una zona DNS</span><span class="sxs-lookup"><span data-stu-id="adf33-121">Create a DNS zone</span></span>

<span data-ttu-id="adf33-122">Se crea una zona DNS con hello `az network dns zone create` comando.</span><span class="sxs-lookup"><span data-stu-id="adf33-122">A DNS zone is created using hello `az network dns zone create` command.</span></span> <span data-ttu-id="adf33-123">Ayuda de toosee para este comando, escriba `az network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="adf33-123">toosee help for this command, type `az network dns zone create -h`.</span></span>

<span data-ttu-id="adf33-124">Hello en el ejemplo siguiente se crea una zona DNS denominada *contoso.com* en grupo de recursos de hello *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="adf33-124">hello following example creates a DNS zone called *contoso.com* in hello resource group *MyResourceGroup*.</span></span> <span data-ttu-id="adf33-125">Utilice toocreate de ejemplo de Hola una zona DNS, sustituyendo los valores de hello para su propio.</span><span class="sxs-lookup"><span data-stu-id="adf33-125">Use hello example toocreate a DNS zone, substituting hello values for your own.</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n contoso.com
```


## <a name="create-a-dns-record"></a><span data-ttu-id="adf33-126">Creación de un registro de DNS</span><span class="sxs-lookup"><span data-stu-id="adf33-126">Create a DNS record</span></span>

<span data-ttu-id="adf33-127">toocreate un registro DNS, usar hello `az network dns record-set [record type] add-record` comando.</span><span class="sxs-lookup"><span data-stu-id="adf33-127">toocreate a DNS record, use hello `az network dns record-set [record type] add-record` command.</span></span> <span data-ttu-id="adf33-128">Para obtener ayuda con los registros A, por ejemplo, vea `azure network dns record-set A add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="adf33-128">For help, for A records for example, see `azure network dns record-set A add-record -h`.</span></span>

<span data-ttu-id="adf33-129">Hello en el ejemplo siguiente se crea un registro con el nombre relativo de Hola "www" Hola "contoso.com", en el grupo de recursos "MyResourceGroup" de la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="adf33-129">hello following example creates a record with hello relative name "www" in hello DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="adf33-130">nombre completo de Hola de conjunto de registros de hello es "www.contoso.com".</span><span class="sxs-lookup"><span data-stu-id="adf33-130">hello fully-qualified name of hello record set is "www.contoso.com".</span></span> <span data-ttu-id="adf33-131">tipo de registro de Hello es "A", con la dirección IP "1.2.3.4" y se utiliza un valor predeterminado TTL de 3600 segundos (1 hora).</span><span class="sxs-lookup"><span data-stu-id="adf33-131">hello record type is "A", with IP address "1.2.3.4", and a default TTL of 3600 seconds (1 hour) is used.</span></span>

```azurecli
az network dns record-set a add-record -g MyResourceGroup -z contoso.com -n www -a 1.2.3.4
```

<span data-ttu-id="adf33-132">Para otros tipos de registros, para conjuntos de registros con más de un registro, para los valores TTL alternativos y toomodify los registros existentes, consulte [registros administrar DNS y los conjuntos de registros con hello Azure CLI 2.0](dns-operations-recordsets-cli.md).</span><span class="sxs-lookup"><span data-stu-id="adf33-132">For other record types, for record sets with more than one record, for alternative TTL values, and toomodify existing records, see [Manage DNS records and record sets using hello Azure CLI 2.0](dns-operations-recordsets-cli.md).</span></span>


## <a name="view-records"></a><span data-ttu-id="adf33-133">Visualización de los registros</span><span class="sxs-lookup"><span data-stu-id="adf33-133">View records</span></span>

<span data-ttu-id="adf33-134">registros DNS de hello toolist en su zona, use:</span><span class="sxs-lookup"><span data-stu-id="adf33-134">toolist hello DNS records in your zone, use:</span></span>

```azurecli
az network dns record-set list -g MyResourceGroup -z contoso.com
```


## <a name="update-name-servers"></a><span data-ttu-id="adf33-135">Actualización de los servidores de nombres</span><span class="sxs-lookup"><span data-stu-id="adf33-135">Update name servers</span></span>

<span data-ttu-id="adf33-136">Una vez haya satisface que la zona DNS y los registros se han configurado correctamente, necesita tooconfigure su nombre de dominio toouse servidores de nombres DNS de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="adf33-136">Once you are satisfied that your DNS zone and records have been set up correctly, you need tooconfigure your domain name toouse hello Azure DNS name servers.</span></span> <span data-ttu-id="adf33-137">Esto permite a otros usuarios Hola Internet toofind los registros DNS.</span><span class="sxs-lookup"><span data-stu-id="adf33-137">This enables other users on hello Internet toofind your DNS records.</span></span>

<span data-ttu-id="adf33-138">servidores de nombres de Hello para la zona se proporcionan por hello `az network dns zone show` comando.</span><span class="sxs-lookup"><span data-stu-id="adf33-138">hello name servers for your zone are given by hello `az network dns zone show` command.</span></span> <span data-ttu-id="adf33-139">nombres de servidor de nombre de hello toosee, usar JSON de salida, como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="adf33-139">toosee hello name server names, use JSON output, as shown in hello following example.</span></span>

```azurecli
az network dns zone show -g MyResourceGroup -n contoso.com -o json

{
  "etag": "00000003-0000-0000-b40d-0996b97ed101",
  "id": "/subscriptions/a385a691-bd93-41b0-8084-8213ebc5bff7/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-01.azure-dns.com.",
    "ns2-01.azure-dns.net.",
    "ns3-01.azure-dns.org.",
    "ns4-01.azure-dns.info."
  ],
  "numberOfRecordSets": 3,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

<span data-ttu-id="adf33-140">Estos servidores de nombres deben configurarse con el registrador de nombres de dominio de hello (que adquirió nombre de dominio de hello).</span><span class="sxs-lookup"><span data-stu-id="adf33-140">These name servers should be configured with hello domain name registrar (where you purchased hello domain name).</span></span> <span data-ttu-id="adf33-141">El registrador proporcionará Hola opción tooset los servidores de nombres de hello para el dominio de Hola.</span><span class="sxs-lookup"><span data-stu-id="adf33-141">Your registrar will offer hello option tooset up hello name servers for hello domain.</span></span> <span data-ttu-id="adf33-142">Para obtener más información, consulte [delegar su tooAzure de dominio DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="adf33-142">For more information, see [Delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="adf33-143">Eliminación de todos los recursos</span><span class="sxs-lookup"><span data-stu-id="adf33-143">Delete all resources</span></span>
 
<span data-ttu-id="adf33-144">toodelete todos los recursos que se crean en este artículo, Hola toman siguiendo el paso:</span><span class="sxs-lookup"><span data-stu-id="adf33-144">toodelete all resources created in this article, take hello following step:</span></span>

```azurecli
az group delete --name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="adf33-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="adf33-145">Next steps</span></span>

<span data-ttu-id="adf33-146">toolearn más información acerca de DNS de Azure, consulte [Introducción a DNS de Azure](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="adf33-146">toolearn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="adf33-147">toolearn más acerca de cómo administrar zonas DNS en DNS de Azure, consulte [zonas DNS de administrar en DNS de Azure mediante Azure CLI 2.0](dns-operations-dnszones-cli.md).</span><span class="sxs-lookup"><span data-stu-id="adf33-147">toolearn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using Azure CLI 2.0](dns-operations-dnszones-cli.md).</span></span>

<span data-ttu-id="adf33-148">toolearn más información acerca de la administración de registros DNS en DNS de Azure, consulte [registros administrar DNS y un registro se establece en DNS de Azure mediante Azure CLI 2.0](dns-operations-recordsets-cli.md).</span><span class="sxs-lookup"><span data-stu-id="adf33-148">toolearn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using Azure CLI 2.0](dns-operations-recordsets-cli.md).</span></span>
