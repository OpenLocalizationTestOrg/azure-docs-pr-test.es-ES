---
title: "Introducción a Azure DNS con la CLI de Azure 2.0 | Microsoft Docs"
description: "Obtenga información sobre cómo crear una zona y un registro DNS en Azure DNS. Esta es una guía paso a paso para crear y administrar su primera zona y su primer registro DNS con la CLI de Azure 2.0."
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
ms.openlocfilehash: 6958d61b29961f59cb22f62bec55f2d467e7e7cb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-20"></a><span data-ttu-id="054cc-104">Introducción a Azure DNS con la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="054cc-104">Get started with Azure DNS using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="054cc-105">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="054cc-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="054cc-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="054cc-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="054cc-107">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="054cc-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="054cc-108">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="054cc-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="054cc-109">Este artículo lo guiará por los pasos necesarios para crear su primera zona y su primer registro DNS mediante la CLI de Azure 2.0 multiplataforma, que está disponible para Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="054cc-109">This article walks you through the steps to create your first DNS zone and record using the cross-platform Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="054cc-110">También puede llevar a cabo estos pasos con Azure Portal o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="054cc-110">You can also perform these steps using the Azure portal or Azure PowerShell.</span></span>

<span data-ttu-id="054cc-111">Una zona DNS se usa para hospedar los registros DNS de un dominio concreto.</span><span class="sxs-lookup"><span data-stu-id="054cc-111">A DNS zone is used to host the DNS records for a particular domain.</span></span> <span data-ttu-id="054cc-112">Para iniciar el hospedaje de su dominio en DNS de Azure, debe crear una zona DNS para ese nombre de dominio.</span><span class="sxs-lookup"><span data-stu-id="054cc-112">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span></span> <span data-ttu-id="054cc-113">Cada registro DNS del dominio se crea luego en esta zona DNS.</span><span class="sxs-lookup"><span data-stu-id="054cc-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="054cc-114">Finalmente, para publicar la zona DNS en Internet, debe configurar los servidores de nombres para el dominio.</span><span class="sxs-lookup"><span data-stu-id="054cc-114">Finally, to publish your DNS zone to the Internet, you need to configure the name servers for the domain.</span></span> <span data-ttu-id="054cc-115">A continuación, se describen cada uno de estos pasos.</span><span class="sxs-lookup"><span data-stu-id="054cc-115">Each of these steps is described below.</span></span>

<span data-ttu-id="054cc-116">En estas instrucciones se da por hecho que ya haya instalado la CLI de Azure 2.0 e iniciado sesión en ella.</span><span class="sxs-lookup"><span data-stu-id="054cc-116">These instructions assume you have already installed and signed in to Azure CLI 2.0.</span></span> <span data-ttu-id="054cc-117">Para obtener ayuda, consulte [Cómo administrar zonas DNS en Azure DNS con la CLI de Azure 2.0](dns-operations-dnszones-cli.md).</span><span class="sxs-lookup"><span data-stu-id="054cc-117">For help, see [How to manage DNS zones using Azure CLI 2.0](dns-operations-dnszones-cli.md).</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="054cc-118">Creación del grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="054cc-118">Create the resource group</span></span>

<span data-ttu-id="054cc-119">Antes de crear la zona DNS, se crea un grupo de recursos para que contenga la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="054cc-119">Before creating the DNS zone, a resource group is created to contain the DNS Zone.</span></span> <span data-ttu-id="054cc-120">A continuación, se muestra el comando.</span><span class="sxs-lookup"><span data-stu-id="054cc-120">The following shows the command.</span></span>

```azurecli
az group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="054cc-121">Creación de una zona DNS</span><span class="sxs-lookup"><span data-stu-id="054cc-121">Create a DNS zone</span></span>

<span data-ttu-id="054cc-122">Una zona DNS se crea con el comando `az network dns zone create` .</span><span class="sxs-lookup"><span data-stu-id="054cc-122">A DNS zone is created using the `az network dns zone create` command.</span></span> <span data-ttu-id="054cc-123">Para ver la ayuda sobre este comando, escriba `az network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="054cc-123">To see help for this command, type `az network dns zone create -h`.</span></span>

<span data-ttu-id="054cc-124">En el ejemplo siguiente, se crea una zona DNS llamada *contoso.com* en el grupo de recursos *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="054cc-124">The following example creates a DNS zone called *contoso.com* in the resource group *MyResourceGroup*.</span></span> <span data-ttu-id="054cc-125">Utilice el ejemplo para crear una zona DNS, sustituyendo los valores por los suyos.</span><span class="sxs-lookup"><span data-stu-id="054cc-125">Use the example to create a DNS zone, substituting the values for your own.</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n contoso.com
```


## <a name="create-a-dns-record"></a><span data-ttu-id="054cc-126">Creación de un registro de DNS</span><span class="sxs-lookup"><span data-stu-id="054cc-126">Create a DNS record</span></span>

<span data-ttu-id="054cc-127">Para crear un registro de DNS, use el comando `az network dns record-set [record type] add-record`.</span><span class="sxs-lookup"><span data-stu-id="054cc-127">To create a DNS record, use the `az network dns record-set [record type] add-record` command.</span></span> <span data-ttu-id="054cc-128">Para obtener ayuda con los registros A, por ejemplo, vea `azure network dns record-set A add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="054cc-128">For help, for A records for example, see `azure network dns record-set A add-record -h`.</span></span>

<span data-ttu-id="054cc-129">En el ejemplo siguiente se crea un conjunto de registros con el nombre relativo "www" en la zona DNS "contoso.com" del grupo de recursos "MyResourceGroup".</span><span class="sxs-lookup"><span data-stu-id="054cc-129">The following example creates a record with the relative name "www" in the DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="054cc-130">El nombre completo del conjunto de registros es www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="054cc-130">The fully-qualified name of the record set is "www.contoso.com".</span></span> <span data-ttu-id="054cc-131">El tipo de registro es "A", con la dirección IP "1.2.3.4", y se utiliza un valor predeterminado TTL de 3600 segundos (1 hora).</span><span class="sxs-lookup"><span data-stu-id="054cc-131">The record type is "A", with IP address "1.2.3.4", and a default TTL of 3600 seconds (1 hour) is used.</span></span>

```azurecli
az network dns record-set a add-record -g MyResourceGroup -z contoso.com -n www -a 1.2.3.4
```

<span data-ttu-id="054cc-132">Para ver otros tipos de registros, conjuntos de registros con más de un registro, valores de TTL alternativos, y para modificar los registros existentes, consulte [Administración de registros de DNS en Azure DNS mediante la CLI de Azure 2.0](dns-operations-recordsets-cli.md).</span><span class="sxs-lookup"><span data-stu-id="054cc-132">For other record types, for record sets with more than one record, for alternative TTL values, and to modify existing records, see [Manage DNS records and record sets using the Azure CLI 2.0](dns-operations-recordsets-cli.md).</span></span>


## <a name="view-records"></a><span data-ttu-id="054cc-133">Visualización de los registros</span><span class="sxs-lookup"><span data-stu-id="054cc-133">View records</span></span>

<span data-ttu-id="054cc-134">Para enumerar los registros DNS de su zona, use lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="054cc-134">To list the DNS records in your zone, use:</span></span>

```azurecli
az network dns record-set list -g MyResourceGroup -z contoso.com
```


## <a name="update-name-servers"></a><span data-ttu-id="054cc-135">Actualización de los servidores de nombres</span><span class="sxs-lookup"><span data-stu-id="054cc-135">Update name servers</span></span>

<span data-ttu-id="054cc-136">Una vez haya comprobado que la zona y los registros DNS se han configurado correctamente, tiene que configurar el nombre de dominio para usar los servidores de nombres DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="054cc-136">Once you are satisfied that your DNS zone and records have been set up correctly, you need to configure your domain name to use the Azure DNS name servers.</span></span> <span data-ttu-id="054cc-137">De esta forma, otros usuarios en Internet podrán encontrar los registros DNS.</span><span class="sxs-lookup"><span data-stu-id="054cc-137">This enables other users on the Internet to find your DNS records.</span></span>

<span data-ttu-id="054cc-138">Los servidores de nombres de su zona se proporcionan con el comando `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="054cc-138">The name servers for your zone are given by the `az network dns zone show` command.</span></span> <span data-ttu-id="054cc-139">Para ver los nombres del servidor de nombres, utilice la salida JSON, como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="054cc-139">To see the name server names, use JSON output, as shown in the following example.</span></span>

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

<span data-ttu-id="054cc-140">Estos servidores de nombres deben configurarse con el registrador de nombres de dominio (donde adquirió el nombre de dominio).</span><span class="sxs-lookup"><span data-stu-id="054cc-140">These name servers should be configured with the domain name registrar (where you purchased the domain name).</span></span> <span data-ttu-id="054cc-141">El registrador ofrece la opción de configurar los servidores de nombres para el dominio.</span><span class="sxs-lookup"><span data-stu-id="054cc-141">Your registrar will offer the option to set up the name servers for the domain.</span></span> <span data-ttu-id="054cc-142">Si quiere obtener más información, consulte [Delegación del dominio en DNS de Azure](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="054cc-142">For more information, see [Delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="054cc-143">Eliminación de todos los recursos</span><span class="sxs-lookup"><span data-stu-id="054cc-143">Delete all resources</span></span>
 
<span data-ttu-id="054cc-144">Para eliminar todos los recursos creados en este artículo, realice el paso siguiente:</span><span class="sxs-lookup"><span data-stu-id="054cc-144">To delete all resources created in this article, take the following step:</span></span>

```azurecli
az group delete --name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="054cc-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="054cc-145">Next steps</span></span>

<span data-ttu-id="054cc-146">Para obtener más información sobre Azure DNS, lea [Introducción a DNS de Azure](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="054cc-146">To learn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="054cc-147">Si quiere saber cómo administrar zonas DNS en Azure DNS, consulte [Cómo administrar zonas DNS en Azure DNS con la CLI de Azure 2.0](dns-operations-dnszones-cli.md).</span><span class="sxs-lookup"><span data-stu-id="054cc-147">To learn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using Azure CLI 2.0](dns-operations-dnszones-cli.md).</span></span>

<span data-ttu-id="054cc-148">Para aprender a administrar registros DNS en Azure DNS, consulte [Administración de registros de DNS en Azure DNS mediante la CLI de Azure 2.0](dns-operations-recordsets-cli.md).</span><span class="sxs-lookup"><span data-stu-id="054cc-148">To learn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using Azure CLI 2.0](dns-operations-recordsets-cli.md).</span></span>
