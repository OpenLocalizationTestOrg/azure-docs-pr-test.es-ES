---
title: aaaGet iniciado en el DNS de Azure mediante PowerShell | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate un DNS zona y este registro de DNS de Azure. Esto es una guía paso a paso toocreate y administrar la primera zona DNS y registre mediante PowerShell."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 0f9dead1e4b44fcc74c84a024c41cdfaeb02b5d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-powershell"></a><span data-ttu-id="6413d-104">Introducción a DNS de Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="6413d-104">Get Started with Azure DNS using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6413d-105">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="6413d-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="6413d-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6413d-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="6413d-107">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="6413d-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="6413d-108">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="6413d-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="6413d-109">Este artículo le guiará a través de hello pasos toocreate la primera zona DNS y el registro mediante Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6413d-109">This article walks you through hello steps toocreate your first DNS zone and record using Azure PowerShell.</span></span> <span data-ttu-id="6413d-110">También puede realizar estos pasos con el portal de Azure de Hola u Hola CLI de Azure entre plataformas.</span><span class="sxs-lookup"><span data-stu-id="6413d-110">You can also perform these steps using hello Azure portal or hello cross-platform Azure CLI.</span></span>

<span data-ttu-id="6413d-111">Una zona DNS es toohost usado Hola registros DNS para un dominio en particular.</span><span class="sxs-lookup"><span data-stu-id="6413d-111">A DNS zone is used toohost hello DNS records for a particular domain.</span></span> <span data-ttu-id="6413d-112">toostart hospedaje de su dominio de DNS de Azure, necesita toocreate una zona DNS para ese nombre de dominio.</span><span class="sxs-lookup"><span data-stu-id="6413d-112">toostart hosting your domain in Azure DNS, you need toocreate a DNS zone for that domain name.</span></span> <span data-ttu-id="6413d-113">Cada registro DNS del dominio se crea luego en esta zona DNS.</span><span class="sxs-lookup"><span data-stu-id="6413d-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="6413d-114">Por último, toopublish su DNS de la zona toohello Internet, necesitará servidores de nombres de hello tooconfigure para dominio de Hola.</span><span class="sxs-lookup"><span data-stu-id="6413d-114">Finally, toopublish your DNS zone toohello Internet, you need tooconfigure hello name servers for hello domain.</span></span> <span data-ttu-id="6413d-115">A continuación, se describen cada uno de estos pasos.</span><span class="sxs-lookup"><span data-stu-id="6413d-115">Each of these steps is described below.</span></span>

<span data-ttu-id="6413d-116">Estas instrucciones se supone que ya haya instalado y firmado en tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6413d-116">These instructions assume you have already installed and signed in tooAzure PowerShell.</span></span> <span data-ttu-id="6413d-117">Para obtener ayuda, consulte [cómo toomanage DNS zonas con PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="6413d-117">For help, see [How toomanage DNS zones using PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="6413d-118">Crear grupo de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="6413d-118">Create hello resource group</span></span>

<span data-ttu-id="6413d-119">Antes de crear la zona DNS de hello, un grupo de recursos se crea la zona DNS de toocontain Hola.</span><span class="sxs-lookup"><span data-stu-id="6413d-119">Before creating hello DNS zone, a resource group is created toocontain hello DNS Zone.</span></span> <span data-ttu-id="6413d-120">siguiente Hello muestra comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6413d-120">hello following shows hello command.</span></span>

```powershell
New-AzureRMResourceGroup -name MyResourceGroup -location "westus"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="6413d-121">Creación de una zona DNS</span><span class="sxs-lookup"><span data-stu-id="6413d-121">Create a DNS zone</span></span>

<span data-ttu-id="6413d-122">Se crea una zona DNS mediante el uso de hello `New-AzureRmDnsZone` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6413d-122">A DNS zone is created by using hello `New-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="6413d-123">Hello en el ejemplo siguiente se crea una zona DNS denominada *contoso.com* en grupo de recursos de hello denominado *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="6413d-123">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*.</span></span> <span data-ttu-id="6413d-124">Utilice toocreate de ejemplo de Hola una zona DNS, sustituyendo los valores de hello para su propio.</span><span class="sxs-lookup"><span data-stu-id="6413d-124">Use hello example toocreate a DNS zone, substituting hello values for your own.</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyResourceGroup
```

## <a name="create-a-dns-record"></a><span data-ttu-id="6413d-125">Creación de un registro de DNS</span><span class="sxs-lookup"><span data-stu-id="6413d-125">Create a DNS record</span></span>

<span data-ttu-id="6413d-126">Crear conjuntos de registros mediante hello `New-AzureRmDnsRecordSet` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6413d-126">You create record sets by using hello `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="6413d-127">Hello en el ejemplo siguiente se crea un registro con el nombre relativo de Hola "www" Hola "contoso.com", en el grupo de recursos "MyResourceGroup" de la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="6413d-127">hello following example creates a record with hello relative name "www" in hello DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="6413d-128">nombre completo de Hola de conjunto de registros de hello es "www.contoso.com".</span><span class="sxs-lookup"><span data-stu-id="6413d-128">hello fully-qualified name of hello record set is "www.contoso.com".</span></span> <span data-ttu-id="6413d-129">tipo de registro de Hello es "A", con la dirección IP "1.2.3.4" y Hola TTL es 3600 segundos.</span><span class="sxs-lookup"><span data-stu-id="6413d-129">hello record type is "A", with IP address "1.2.3.4", and hello TTL is 3600 seconds.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName contoso.com -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4")
```

<span data-ttu-id="6413d-130">Para otros tipos de registros, para conjuntos de registros con más de un registro y toomodify los registros existentes, consulte [registros administrar DNS y los conjuntos de registros con Azure PowerShell](dns-operations-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="6413d-130">For other record types, for record sets with more than one record, and toomodify existing records, see [Manage DNS records and record sets using Azure PowerShell](dns-operations-recordsets.md).</span></span> 


## <a name="view-records"></a><span data-ttu-id="6413d-131">Visualización de los registros</span><span class="sxs-lookup"><span data-stu-id="6413d-131">View records</span></span>

<span data-ttu-id="6413d-132">registros DNS de hello toolist en su zona, use:</span><span class="sxs-lookup"><span data-stu-id="6413d-132">toolist hello DNS records in your zone, use:</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName contoso.com -ResourceGroupName MyResourceGroup
```


## <a name="update-name-servers"></a><span data-ttu-id="6413d-133">Actualización de los servidores de nombres</span><span class="sxs-lookup"><span data-stu-id="6413d-133">Update name servers</span></span>

<span data-ttu-id="6413d-134">Una vez haya satisface que la zona DNS y los registros se han configurado correctamente, necesita tooconfigure su nombre de dominio toouse servidores de nombres DNS de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="6413d-134">Once you are satisfied that your DNS zone and records have been set up correctly, you need tooconfigure your domain name toouse hello Azure DNS name servers.</span></span> <span data-ttu-id="6413d-135">Esto permite a otros usuarios Hola Internet toofind los registros DNS.</span><span class="sxs-lookup"><span data-stu-id="6413d-135">This enables other users on hello Internet toofind your DNS records.</span></span>

<span data-ttu-id="6413d-136">servidores de nombres de Hello para la zona se proporcionan por hello `Get-AzureRmDnsZone` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="6413d-136">hello name servers for your zone are given by hello `Get-AzureRmDnsZone` cmdlet:</span></span>

```powershell
Get-AzureRmDnsZone -ZoneName contoso.com -ResourceGroupName MyResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-b40d-0996b97ed101
Tags                  : {}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org., ns4-01.azure-dns.info.}
NumberOfRecordSets    : 3
MaxNumberOfRecordSets : 5000
```

<span data-ttu-id="6413d-137">Estos servidores de nombres deben configurarse con el registrador de nombres de dominio de hello (que adquirió nombre de dominio de hello).</span><span class="sxs-lookup"><span data-stu-id="6413d-137">These name servers should be configured with hello domain name registrar (where you purchased hello domain name).</span></span> <span data-ttu-id="6413d-138">El registrador proporcionará Hola opción tooset los servidores de nombres de hello para el dominio de Hola.</span><span class="sxs-lookup"><span data-stu-id="6413d-138">Your registrar will offer hello option tooset up hello name servers for hello domain.</span></span> <span data-ttu-id="6413d-139">Para obtener más información, consulte [delegar su tooAzure de dominio DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="6413d-139">For more information, see [Delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="6413d-140">Eliminación de todos los recursos</span><span class="sxs-lookup"><span data-stu-id="6413d-140">Delete all resources</span></span>

<span data-ttu-id="6413d-141">toodelete todos los recursos que se crean en este artículo, Hola toman siguiendo el paso:</span><span class="sxs-lookup"><span data-stu-id="6413d-141">toodelete all resources created in this article, take hello following step:</span></span>

```powershell
Remove-AzureRMResourceGroup -Name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="6413d-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6413d-142">Next steps</span></span>

<span data-ttu-id="6413d-143">toolearn más información acerca de DNS de Azure, consulte [Introducción a DNS de Azure](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6413d-143">toolearn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="6413d-144">toolearn más acerca de cómo administrar zonas DNS en DNS de Azure, consulte [zonas DNS de administrar en DNS de Azure con PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="6413d-144">toolearn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using PowerShell](dns-operations-dnszones.md).</span></span>

<span data-ttu-id="6413d-145">toolearn más información acerca de la administración de registros DNS en DNS de Azure, consulte [registros administrar DNS y un registro se establece en DNS de Azure con PowerShell](dns-operations-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="6413d-145">toolearn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using PowerShell](dns-operations-recordsets.md).</span></span>

