---
title: "Introducción a Azure DNS con la CLI de Azure 1.0 | Microsoft Docs"
description: "Obtenga información sobre cómo crear una zona y un registro DNS en Azure DNS. Esta es una guía paso a paso para crear y administrar su primera zona y su primer registro DNS con la CLI de Azure 1.0."
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
ms.openlocfilehash: f7943b71bbd16c36df09436973d92539eb62b210
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-10"></a><span data-ttu-id="924a3-104">Introducción a Azure DNS con la CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="924a3-104">Get started with Azure DNS using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="924a3-105">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="924a3-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="924a3-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="924a3-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="924a3-107">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="924a3-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="924a3-108">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="924a3-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="924a3-109">Este artículo lo guiará por los pasos necesarios para crear su primera zona y su primer registro DNS mediante la CLI de Azure 1.0 multiplataforma, que está disponible para Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="924a3-109">This article walks you through the steps to create your first DNS zone and record using the cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="924a3-110">También puede llevar a cabo estos pasos con Azure Portal o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="924a3-110">You can also perform these steps using the Azure portal or Azure PowerShell.</span></span>

<span data-ttu-id="924a3-111">Una zona DNS se usa para hospedar los registros DNS de un dominio concreto.</span><span class="sxs-lookup"><span data-stu-id="924a3-111">A DNS zone is used to host the DNS records for a particular domain.</span></span> <span data-ttu-id="924a3-112">Para iniciar el hospedaje de su dominio en DNS de Azure, debe crear una zona DNS para ese nombre de dominio.</span><span class="sxs-lookup"><span data-stu-id="924a3-112">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span></span> <span data-ttu-id="924a3-113">Cada registro DNS del dominio se crea luego en esta zona DNS.</span><span class="sxs-lookup"><span data-stu-id="924a3-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="924a3-114">Finalmente, para publicar la zona DNS en Internet, debe configurar los servidores de nombres para el dominio.</span><span class="sxs-lookup"><span data-stu-id="924a3-114">Finally, to publish your DNS zone to the Internet, you need to configure the name servers for the domain.</span></span> <span data-ttu-id="924a3-115">A continuación, se describen cada uno de estos pasos.</span><span class="sxs-lookup"><span data-stu-id="924a3-115">Each of these steps is described below.</span></span>

<span data-ttu-id="924a3-116">En estas instrucciones se da por hecho que ya haya instalado la CLI de Azure 1.0 e iniciado sesión en ella.</span><span class="sxs-lookup"><span data-stu-id="924a3-116">These instructions assume you have already installed and signed in to Azure CLI 1.0.</span></span> <span data-ttu-id="924a3-117">Para obtener ayuda, consulte [Cómo administrar zonas DNS en Azure DNS con la CLI de Azure 1.0](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="924a3-117">For help, see [How to manage DNS zones using Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="924a3-118">Creación del grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="924a3-118">Create the resource group</span></span>

<span data-ttu-id="924a3-119">Antes de crear la zona DNS, se crea un grupo de recursos para que contenga la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="924a3-119">Before creating the DNS zone, a resource group is created to contain the DNS Zone.</span></span> <span data-ttu-id="924a3-120">A continuación, se muestra el comando.</span><span class="sxs-lookup"><span data-stu-id="924a3-120">The following shows the command.</span></span>

```azurecli
azure group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="924a3-121">Creación de una zona DNS</span><span class="sxs-lookup"><span data-stu-id="924a3-121">Create a DNS zone</span></span>

<span data-ttu-id="924a3-122">Una zona DNS se crea con el comando `azure network dns zone create` .</span><span class="sxs-lookup"><span data-stu-id="924a3-122">A DNS zone is created using the `azure network dns zone create` command.</span></span> <span data-ttu-id="924a3-123">Para ver la ayuda sobre este comando, escriba `azure network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="924a3-123">To see help for this command, type `azure network dns zone create -h`.</span></span>

<span data-ttu-id="924a3-124">En el ejemplo siguiente, se crea una zona DNS llamada *contoso.com* en el grupo de recursos *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="924a3-124">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*.</span></span> <span data-ttu-id="924a3-125">Utilice el ejemplo para crear una zona DNS, sustituyendo los valores por los suyos.</span><span class="sxs-lookup"><span data-stu-id="924a3-125">Use the example to create a DNS zone, substituting the values for your own.</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```


## <a name="create-a-dns-record"></a><span data-ttu-id="924a3-126">Creación de un registro de DNS</span><span class="sxs-lookup"><span data-stu-id="924a3-126">Create a DNS record</span></span>

<span data-ttu-id="924a3-127">Para crear un registro de DNS, use el comando `azure network dns record-set add-record`.</span><span class="sxs-lookup"><span data-stu-id="924a3-127">To create a DNS record, use the `azure network dns record-set add-record` command.</span></span> <span data-ttu-id="924a3-128">Para obtener ayuda, consulte `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="924a3-128">For help, see `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="924a3-129">En el ejemplo siguiente se crea un conjunto de registros con el nombre relativo "www" en la zona DNS "contoso.com" del grupo de recursos "MyResourceGroup".</span><span class="sxs-lookup"><span data-stu-id="924a3-129">The following example creates a record with the relative name "www" in the DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="924a3-130">El nombre completo del conjunto de registros es www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="924a3-130">The fully-qualified name of the record set is "www.contoso.com".</span></span> <span data-ttu-id="924a3-131">El tipo de registro es "A", con la dirección IP "1.2.3.4", y se utiliza un valor predeterminado TTL de 3600 segundos (1 hora).</span><span class="sxs-lookup"><span data-stu-id="924a3-131">The record type is "A", with IP address "1.2.3.4", and a default TTL of 3600 seconds (1 hour) is used.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

<span data-ttu-id="924a3-132">Para ver otros tipos de registros, conjuntos de registros con más de un registro, valores de TTL alternativos, y para modificar los registros existentes, consulte [Administración de registros de DNS en Azure DNS mediante la CLI de Azure 1.0](dns-operations-recordsets-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="924a3-132">For other record types, for record sets with more than one record, for alternative TTL values, and to modify existing records, see [Manage DNS records and record sets using the Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span></span>


## <a name="view-records"></a><span data-ttu-id="924a3-133">Visualización de los registros</span><span class="sxs-lookup"><span data-stu-id="924a3-133">View records</span></span>

<span data-ttu-id="924a3-134">Para enumerar los registros DNS de su zona, use lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="924a3-134">To list the DNS records in your zone, use:</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```


## <a name="update-name-servers"></a><span data-ttu-id="924a3-135">Actualización de los servidores de nombres</span><span class="sxs-lookup"><span data-stu-id="924a3-135">Update name servers</span></span>

<span data-ttu-id="924a3-136">Una vez haya comprobado que la zona y los registros DNS se han configurado correctamente, tiene que configurar el nombre de dominio para usar los servidores de nombres DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="924a3-136">Once you are satisfied that your DNS zone and records have been set up correctly, you need to configure your domain name to use the Azure DNS name servers.</span></span> <span data-ttu-id="924a3-137">De esta forma, otros usuarios en Internet podrán encontrar los registros DNS.</span><span class="sxs-lookup"><span data-stu-id="924a3-137">This enables other users on the Internet to find your DNS records.</span></span>

<span data-ttu-id="924a3-138">Los servidores de nombres de su zona se proporcionan con el comando `azure network dns zone show`:</span><span class="sxs-lookup"><span data-stu-id="924a3-138">The name servers for your zone are given by the `azure network dns zone show` command:</span></span>

```azurecli
azure network dns zone show MyResourceGroup contoso.com

info:    Executing command network dns zone show
+ Looking up the dns zone "contoso.com"
data:    Id                              : /subscriptions/a385a691-bd93-41b0-8084-8213ebc5bff7/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com
data:    Name                            : contoso.com
data:    Type                            : Microsoft.Network/dnszones
data:    Location                        : global
data:    Number of record sets           : 3
data:    Max number of record sets       : 5000
data:    Name servers:
data:        ns1-01.azure-dns.com.
data:        ns2-01.azure-dns.net.
data:        ns3-01.azure-dns.org.
data:        ns4-01.azure-dns.info.
data:    Tags                            :
info:    network dns zone show command OK
```

<span data-ttu-id="924a3-139">Estos servidores de nombres deben configurarse con el registrador de nombres de dominio (donde adquirió el nombre de dominio).</span><span class="sxs-lookup"><span data-stu-id="924a3-139">These name servers should be configured with the domain name registrar (where you purchased the domain name).</span></span> <span data-ttu-id="924a3-140">El registrador ofrece la opción de configurar los servidores de nombres para el dominio.</span><span class="sxs-lookup"><span data-stu-id="924a3-140">Your registrar will offer the option to set up the name servers for the domain.</span></span> <span data-ttu-id="924a3-141">Si quiere obtener más información, consulte [Delegación del dominio en DNS de Azure](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="924a3-141">For more information, see [Delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="924a3-142">Eliminación de todos los recursos</span><span class="sxs-lookup"><span data-stu-id="924a3-142">Delete all resources</span></span>
 
<span data-ttu-id="924a3-143">Para eliminar todos los recursos creados en este artículo, realice el paso siguiente:</span><span class="sxs-lookup"><span data-stu-id="924a3-143">To delete all resources created in this article, take the following step:</span></span>

```azurecli
azure group delete --name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="924a3-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="924a3-144">Next steps</span></span>

<span data-ttu-id="924a3-145">Para obtener más información sobre Azure DNS, lea [Introducción a DNS de Azure](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="924a3-145">To learn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="924a3-146">Si quiere saber cómo administrar zonas DNS en Azure DNS, consulte [Cómo administrar zonas DNS en Azure DNS con la CLI de Azure 1.0](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="924a3-146">To learn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span></span>

<span data-ttu-id="924a3-147">Para aprender a administrar registros DNS en Azure DNS, consulte [Administración de registros de DNS en Azure DNS mediante la CLI de Azure 1.0](dns-operations-recordsets-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="924a3-147">To learn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span></span>

