---
title: "Delegación de dominios en DNS de Azure | Microsoft Docs"
description: "Información sobre cómo cambiar la delegación de dominios y usar los servidores de nombres DNS de Azure para ofrecer hospedaje de dominios."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 257da6ec-d6e2-4b6f-ad76-ee2dde4efbcc
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: gwallace
ms.openlocfilehash: 33b3ec24432ff1268860b9a2e9d5098600a8dedc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="delegate-a-domain-to-azure-dns"></a><span data-ttu-id="3eb84-103">Delegación de un dominio en DNS de Azure</span><span class="sxs-lookup"><span data-stu-id="3eb84-103">Delegate a domain to Azure DNS</span></span>

<span data-ttu-id="3eb84-104">DNS de Azure le permite hospedar una zona DNS y administrar los registros DNS de un dominio en Azure.</span><span class="sxs-lookup"><span data-stu-id="3eb84-104">Azure DNS allows you to host a DNS zone and manage the DNS records for a domain in Azure.</span></span> <span data-ttu-id="3eb84-105">Para que las consultas DNS de un dominio lleguen a DNS de Azure, es necesario haber delegado dicho dominio en DNS de Azure desde el dominio primario.</span><span class="sxs-lookup"><span data-stu-id="3eb84-105">In order for DNS queries for a domain to reach Azure DNS, the domain has to be delegated to Azure DNS from the parent domain.</span></span> <span data-ttu-id="3eb84-106">Tenga en cuenta que DNS de Azure no es el registrador de dominios.</span><span class="sxs-lookup"><span data-stu-id="3eb84-106">Keep in mind Azure DNS is not the domain registrar.</span></span> <span data-ttu-id="3eb84-107">En este artículo se explica cómo delegar el dominio a Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="3eb84-107">This article explains how to delegate your domain to Azure DNS.</span></span>

<span data-ttu-id="3eb84-108">Si se trata de dominios adquiridos a un registrador, este último ofrecerá la opción de configurar tales registros NS.</span><span class="sxs-lookup"><span data-stu-id="3eb84-108">For domains purchased from a registrar, your registrar offers the option to set up these NS records.</span></span> <span data-ttu-id="3eb84-109">No tiene que poseer un nombre de dominio para crear una zona DNS con dicho nombre de dominio en Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="3eb84-109">You do not have to own a domain to create a DNS zone with that domain name in Azure DNS.</span></span> <span data-ttu-id="3eb84-110">No obstante, sí necesita disponer de un dominio para configurar la delegación en DNS de Azure con un registrador.</span><span class="sxs-lookup"><span data-stu-id="3eb84-110">However, you do need to own the domain to set up the delegation to Azure DNS with the registrar.</span></span>

<span data-ttu-id="3eb84-111">Por ejemplo, supongamos que adquiere el dominio “contoso.net” y que crea una zona con el nombre “contoso.net” en Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="3eb84-111">For example, suppose you purchase the domain 'contoso.net' and create a zone with the name 'contoso.net' in Azure DNS.</span></span> <span data-ttu-id="3eb84-112">Como propietario del dominio, el registrador le ofrecerá la opción de configurar las direcciones del servidor de nombres (es decir, los registros NS) para el dominio.</span><span class="sxs-lookup"><span data-stu-id="3eb84-112">As the owner of the domain, your registrar offers you the option to configure the name server addresses (that is, the NS records) for your domain.</span></span> <span data-ttu-id="3eb84-113">El registrador almacena estos registros NS en el dominio primario, en este caso, “.net”.</span><span class="sxs-lookup"><span data-stu-id="3eb84-113">The registrar stores these NS records in the parent domain, in this case '.net'.</span></span> <span data-ttu-id="3eb84-114">A los clientes de todo el mundo se les remitirá entonces al dominio en cuestión en la zona DNS de Azure al tratar de resolver registros DNS en “contoso.net”.</span><span class="sxs-lookup"><span data-stu-id="3eb84-114">Clients around the world can then be directed to your domain in Azure DNS zone when trying to resolve DNS records in 'contoso.net'.</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="3eb84-115">Creación de una zona DNS</span><span class="sxs-lookup"><span data-stu-id="3eb84-115">Create a DNS zone</span></span>

1. <span data-ttu-id="3eb84-116">Inicie sesión en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3eb84-116">Sign in to the Azure portal</span></span>
1. <span data-ttu-id="3eb84-117">En el menú Concentrador, haga clic en **Nuevo > Redes >** y, luego, en **Zona DNS** para abrir la hoja Crear zona DNS.</span><span class="sxs-lookup"><span data-stu-id="3eb84-117">On the Hub menu, click and click **New > Networking >** and then click **DNS zone** to open the Create DNS zone blade.</span></span>

    ![Zona DNS](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="3eb84-119">En la hoja **Crear zona DNS**, escriba los valores siguientes y haga clic en **Crear**:</span><span class="sxs-lookup"><span data-stu-id="3eb84-119">On the **Create DNS zone** blade enter the following values, then click **Create**:</span></span>

   | <span data-ttu-id="3eb84-120">**Configuración**</span><span class="sxs-lookup"><span data-stu-id="3eb84-120">**Setting**</span></span> | <span data-ttu-id="3eb84-121">**Valor**</span><span class="sxs-lookup"><span data-stu-id="3eb84-121">**Value**</span></span> | <span data-ttu-id="3eb84-122">**Detalles**</span><span class="sxs-lookup"><span data-stu-id="3eb84-122">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="3eb84-123">**Name**</span><span class="sxs-lookup"><span data-stu-id="3eb84-123">**Name**</span></span>|<span data-ttu-id="3eb84-124">contoso.net</span><span class="sxs-lookup"><span data-stu-id="3eb84-124">contoso.net</span></span>|<span data-ttu-id="3eb84-125">El nombre de la zona DNS</span><span class="sxs-lookup"><span data-stu-id="3eb84-125">The name of the DNS zone</span></span>|
   |<span data-ttu-id="3eb84-126">**Suscripción**</span><span class="sxs-lookup"><span data-stu-id="3eb84-126">**Subscription**</span></span>|<span data-ttu-id="3eb84-127">[Su suscripción]</span><span class="sxs-lookup"><span data-stu-id="3eb84-127">[Your subscription]</span></span>|<span data-ttu-id="3eb84-128">Seleccione una suscripción donde se va a crear la puerta de enlace de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3eb84-128">Select a subscription to create the application gateway in.</span></span>|
   |<span data-ttu-id="3eb84-129">**Grupos de recursos**</span><span class="sxs-lookup"><span data-stu-id="3eb84-129">**Resource group**</span></span>|<span data-ttu-id="3eb84-130">**Crear nuevo:** contosoRG</span><span class="sxs-lookup"><span data-stu-id="3eb84-130">**Create new:** contosoRG</span></span>|<span data-ttu-id="3eb84-131">Cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3eb84-131">Create a resource group.</span></span> <span data-ttu-id="3eb84-132">El nombre del grupo de recursos debe ser único dentro de la suscripción seleccionada.</span><span class="sxs-lookup"><span data-stu-id="3eb84-132">The resource group name must be unique within the subscription you selected.</span></span> <span data-ttu-id="3eb84-133">Para más información sobre los grupos de recursos, lea el artículo [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="3eb84-133">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="3eb84-134">**Ubicación**</span><span class="sxs-lookup"><span data-stu-id="3eb84-134">**Location**</span></span>|<span data-ttu-id="3eb84-135">Oeste de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="3eb84-135">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="3eb84-136">El grupo de recursos se refiere a la ubicación del grupo de recursos y no tiene efecto alguno sobre la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="3eb84-136">The resource group refers to the location of the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="3eb84-137">La ubicación de la zona DNS siempre es "global" y no se muestra.</span><span class="sxs-lookup"><span data-stu-id="3eb84-137">The DNS zone location is always "global", and is not shown.</span></span>

## <a name="retrieve-name-servers"></a><span data-ttu-id="3eb84-138">Recuperación de los servidores de nombres</span><span class="sxs-lookup"><span data-stu-id="3eb84-138">Retrieve name servers</span></span>

<span data-ttu-id="3eb84-139">Antes de poder delegar la zona DNS a DNS de Azure, primero debe conocer los nombres del servidor de nombres de la zona.</span><span class="sxs-lookup"><span data-stu-id="3eb84-139">Before you can delegate your DNS zone to Azure DNS, you first need to know the name server names for your zone.</span></span> <span data-ttu-id="3eb84-140">El DNS de Azure asigna los servidores de nombres de un grupo cada vez que se crea una zona.</span><span class="sxs-lookup"><span data-stu-id="3eb84-140">Azure DNS allocates name servers from a pool each time a zone is created.</span></span>

1. <span data-ttu-id="3eb84-141">Con la zona DNS creada, en el panel **Favoritos** de Azure Portal, haga clic en **Todos los recursos**.</span><span class="sxs-lookup"><span data-stu-id="3eb84-141">With the DNS zone created, in the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="3eb84-142">Haga clic en la zona DNS **contoso.net** en la hoja **Todos los recursos**.</span><span class="sxs-lookup"><span data-stu-id="3eb84-142">Click the **contoso.net** DNS zone in the **All resources** blade.</span></span> <span data-ttu-id="3eb84-143">Si la suscripción que seleccionó ya tiene varios recursos en ella, puede escribir **contoso.net** en el cuadro Filtrar por nombre…</span><span class="sxs-lookup"><span data-stu-id="3eb84-143">If the subscription you selected already has several resources in it, you can enter **contoso.net** in the Filter by name…</span></span> <span data-ttu-id="3eb84-144">para acceder fácilmente a la puerta de enlace de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3eb84-144">box to easily access the application gateway.</span></span> 

1. <span data-ttu-id="3eb84-145">Recupere los servidores de nombres en la hoja Zona DNS.</span><span class="sxs-lookup"><span data-stu-id="3eb84-145">Retrieve the name servers from the DNS zone blade.</span></span> <span data-ttu-id="3eb84-146">En este ejemplo, a la zona “contoso.net” se le han asignado los servidores de nombres “ns1-01.azure-dns.com”, “ns2-01.azure-dns.net”, “ns3-01.azure-dns.org” y “ns4-01.azure-dns.info”’:</span><span class="sxs-lookup"><span data-stu-id="3eb84-146">In this example, the zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="3eb84-148">El DNS de Azure crea automáticamente los registros NS autoritativos en la zona que contiene los servidores de nombres asignados.</span><span class="sxs-lookup"><span data-stu-id="3eb84-148">Azure DNS automatically creates authoritative NS records in your zone containing the assigned name servers.</span></span>  <span data-ttu-id="3eb84-149">Para ver los nombres del servidor de nombres mediante Azure PowerShell o CLI de Azure, simplemente necesita recuperar estos registros.</span><span class="sxs-lookup"><span data-stu-id="3eb84-149">To see the name server names via Azure PowerShell or Azure CLI, you simply need to retrieve these records.</span></span>

<span data-ttu-id="3eb84-150">Los siguientes ejemplos también proporcionan los pasos para recuperar los servidores de nombres para una zona de Azure DNS con PowerShell y la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="3eb84-150">The following examples also provide the steps to retrieve the name servers for a zone in Azure DNS with PowerShell and Azure CLI.</span></span>

### <a name="powershell"></a><span data-ttu-id="3eb84-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3eb84-151">PowerShell</span></span>

```powershell
# The record name "@" is used to refer to records at the top of the zone.
$zone = Get-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -Zone $zone
```

<span data-ttu-id="3eb84-152">El ejemplo siguiente es la respuesta.</span><span class="sxs-lookup"><span data-stu-id="3eb84-152">The following example is the response.</span></span>

```
Name              : @
ZoneName          : contoso.net
ResourceGroupName : contosorg
Ttl               : 172800
Etag              : 03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5
RecordType        : NS
Records           : {ns1-07.azure-dns.com., ns2-07.azure-dns.net., ns3-07.azure-dns.org.,
                    ns4-07.azure-dns.info.}
Metadata          :
```

### <a name="azure-cli"></a><span data-ttu-id="3eb84-153">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="3eb84-153">Azure CLI</span></span>

```azurecli
az network dns record-set show --resource-group contosoRG --zone-name contoso.net --type NS --name @
```

<span data-ttu-id="3eb84-154">El ejemplo siguiente es la respuesta.</span><span class="sxs-lookup"><span data-stu-id="3eb84-154">The following example is the response.</span></span>

```json
{
  "etag": "03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosoRG/providers/Microsoft.Network/dnszones/contoso.net/NS/@",
  "metadata": null,
  "name": "@",
  "nsRecords": [
    {
      "nsdname": "ns1-07.azure-dns.com."
    },
    {
      "nsdname": "ns2-07.azure-dns.net."
    },
    {
      "nsdname": "ns3-07.azure-dns.org."
    },
    {
      "nsdname": "ns4-07.azure-dns.info."
    }
  ],
  "resourceGroup": "contosoRG",
  "ttl": 172800,
  "type": "Microsoft.Network/dnszones/NS"
}
```

## <a name="delegate-the-domain"></a><span data-ttu-id="3eb84-155">Delegación del dominio</span><span class="sxs-lookup"><span data-stu-id="3eb84-155">Delegate the domain</span></span>

<span data-ttu-id="3eb84-156">Ahora que se crea la zona DNS y que tiene los servidores de nombres, el dominio primario debe actualizarse con los servidores de nombres de Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="3eb84-156">Now that the DNS zone is created and you have the name servers, the parent domain needs to be updated with the Azure DNS name servers.</span></span> <span data-ttu-id="3eb84-157">Cada registrador dispone de sus propias herramientas de administración de DNS para cambiar los registros de servidores de nombres de un dominio.</span><span class="sxs-lookup"><span data-stu-id="3eb84-157">Each registrar has their own DNS management tools to change the name server records for a domain.</span></span> <span data-ttu-id="3eb84-158">En la página de administración de DNS del registrador, edite los registros NS y reemplácelos con los que DNS de Azure ha creado.</span><span class="sxs-lookup"><span data-stu-id="3eb84-158">In the registrar's DNS management page, edit the NS records and replace the NS records with the ones Azure DNS created.</span></span>

<span data-ttu-id="3eb84-159">Al delegar un dominio a DNS de Azure, debe usar los nombres de servidor DNS proporcionados por DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="3eb84-159">When delegating a domain to Azure DNS, you must use the name server names provided by Azure DNS.</span></span> <span data-ttu-id="3eb84-160">Es recomendable usar siempre los cuatro nombres de servidor de nombres, independientemente del nombre de su dominio.</span><span class="sxs-lookup"><span data-stu-id="3eb84-160">It is recommended to use all four name server names, regardless of the name of your domain.</span></span> <span data-ttu-id="3eb84-161">La delegación de dominios no requiere que el nombre del servidor de nombres use el mismo dominio de primer nivel que su dominio.</span><span class="sxs-lookup"><span data-stu-id="3eb84-161">Domain delegation does not require the name server name to use the same top-level domain as your domain.</span></span>

<span data-ttu-id="3eb84-162">No debe usar 'registros de adherencia' para apuntar a direcciones IP del servidor DNS de Azure, ya que estas direcciones IP pueden cambiar en el futuro.</span><span class="sxs-lookup"><span data-stu-id="3eb84-162">You should not use 'glue records' to point to the Azure DNS name server IP addresses, since these IP addresses may change in future.</span></span> <span data-ttu-id="3eb84-163">Las delegaciones que usan nombres de servidor en su propia zona (a veces denominados "servidores DNS personalizados") no se admiten de momento en DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="3eb84-163">Delegations using name server names in your own zone, sometimes called 'vanity name servers', are not currently supported in Azure DNS.</span></span>

## <a name="verify-name-resolution-is-working"></a><span data-ttu-id="3eb84-164">Comprobación del funcionamiento de la resolución de nombres</span><span class="sxs-lookup"><span data-stu-id="3eb84-164">Verify name resolution is working</span></span>

<span data-ttu-id="3eb84-165">Cuando finalice la delegación, puede verificar que la resolución de nombres funciona usando una herramienta como “nslookup” para consultar el registro SOA para su zona (que también se crea automáticamente cuando se crea la zona).</span><span class="sxs-lookup"><span data-stu-id="3eb84-165">After completing the delegation, you can verify that name resolution is working by using a tool such as 'nslookup' to query the SOA record for your zone (which is also automatically created when the zone is created).</span></span>

<span data-ttu-id="3eb84-166">No es necesario especificar los servidores de nombres DNS de Azure, ya que el proceso de resolución DNS normal encontrará los servidores de nombres automáticamente si la delegación se ha configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="3eb84-166">You do not have to specify the Azure DNS name servers, if the delegation has been set up correctly, the normal DNS resolution process finds the name servers automatically.</span></span>

```
nslookup -type=SOA contoso.com
```

<span data-ttu-id="3eb84-167">Lo siguiente es una respuesta de ejemplo del comando anterior:</span><span class="sxs-lookup"><span data-stu-id="3eb84-167">The following is an example response from the preceding command:</span></span>

```
Server: ns1-04.azure-dns.com
Address: 208.76.47.4

contoso.com
primary name server = ns1-04.azure-dns.com
responsible mail addr = msnhst.microsoft.com
serial = 1
refresh = 900 (15 mins)
retry = 300 (5 mins)
expire = 604800 (7 days)
default TTL = 300 (5 mins)
```

## <a name="delegate-sub-domains-in-azure-dns"></a><span data-ttu-id="3eb84-168">Delegación de subdominios en Azure DNS</span><span class="sxs-lookup"><span data-stu-id="3eb84-168">Delegate sub-domains in Azure DNS</span></span>

<span data-ttu-id="3eb84-169">Si desea configurar una zona secundaria independiente, puede delegar un subdominio en DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="3eb84-169">If you want to set up a separate child zone, you can delegate a sub-domain in Azure DNS.</span></span> <span data-ttu-id="3eb84-170">Por ejemplo, después de configurar y delegar "contoso.net" en Azure DNS, suponga que desea configurar una zona secundaria independiente, "partners.contoso.net".</span><span class="sxs-lookup"><span data-stu-id="3eb84-170">For example, having set up and delegated 'contoso.net' in Azure DNS, suppose you would like to set up a separate child zone, 'partners.contoso.net'.</span></span>

1. <span data-ttu-id="3eb84-171">Cree la zona secundaria "partners.contoso.net" en Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="3eb84-171">Create the child zone 'partners.contoso.net' in Azure DNS.</span></span>
2. <span data-ttu-id="3eb84-172">Busque los registros NS autoritativos en la zona secundaria para obtener los servidores de nombres que hospedan la zona secundaria en DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="3eb84-172">Look up the authoritative NS records in the child zone to obtain the name servers hosting the child zone in Azure DNS.</span></span>
3. <span data-ttu-id="3eb84-173">Delegue la zona secundaria mediante la configuración de los registros NS de la zona principal que apuntan a la zona secundaria.</span><span class="sxs-lookup"><span data-stu-id="3eb84-173">Delegate the child zone by configuring NS records in the parent zone pointing to the child zone.</span></span>

### <a name="create-a-dns-zone"></a><span data-ttu-id="3eb84-174">Creación de una zona DNS</span><span class="sxs-lookup"><span data-stu-id="3eb84-174">Create a DNS zone</span></span>

1. <span data-ttu-id="3eb84-175">Inicie sesión en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3eb84-175">Sign in to the Azure portal</span></span>
1. <span data-ttu-id="3eb84-176">En el menú Concentrador, haga clic en **Nuevo > Redes >** y, luego, en **Zona DNS** para abrir la hoja Crear zona DNS.</span><span class="sxs-lookup"><span data-stu-id="3eb84-176">On the Hub menu, click and click **New > Networking >** and then click **DNS zone** to open the Create DNS zone blade.</span></span>

    ![Zona DNS](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="3eb84-178">En la hoja **Crear zona DNS**, escriba los valores siguientes y haga clic en **Crear**:</span><span class="sxs-lookup"><span data-stu-id="3eb84-178">On the **Create DNS zone** blade enter the following values, then click **Create**:</span></span>

   | <span data-ttu-id="3eb84-179">**Configuración**</span><span class="sxs-lookup"><span data-stu-id="3eb84-179">**Setting**</span></span> | <span data-ttu-id="3eb84-180">**Valor**</span><span class="sxs-lookup"><span data-stu-id="3eb84-180">**Value**</span></span> | <span data-ttu-id="3eb84-181">**Detalles**</span><span class="sxs-lookup"><span data-stu-id="3eb84-181">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="3eb84-182">**Name**</span><span class="sxs-lookup"><span data-stu-id="3eb84-182">**Name**</span></span>|<span data-ttu-id="3eb84-183">partners.contoso.net</span><span class="sxs-lookup"><span data-stu-id="3eb84-183">partners.contoso.net</span></span>|<span data-ttu-id="3eb84-184">El nombre de la zona DNS</span><span class="sxs-lookup"><span data-stu-id="3eb84-184">The name of the DNS zone</span></span>|
   |<span data-ttu-id="3eb84-185">**Suscripción**</span><span class="sxs-lookup"><span data-stu-id="3eb84-185">**Subscription**</span></span>|<span data-ttu-id="3eb84-186">[Su suscripción]</span><span class="sxs-lookup"><span data-stu-id="3eb84-186">[Your subscription]</span></span>|<span data-ttu-id="3eb84-187">Seleccione una suscripción donde se va a crear la puerta de enlace de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3eb84-187">Select a subscription to create the application gateway in.</span></span>|
   |<span data-ttu-id="3eb84-188">**Grupos de recursos**</span><span class="sxs-lookup"><span data-stu-id="3eb84-188">**Resource group**</span></span>|<span data-ttu-id="3eb84-189">**Usar existente:** contosoRG</span><span class="sxs-lookup"><span data-stu-id="3eb84-189">**Use Existing:** contosoRG</span></span>|<span data-ttu-id="3eb84-190">Cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3eb84-190">Create a resource group.</span></span> <span data-ttu-id="3eb84-191">El nombre del grupo de recursos debe ser único dentro de la suscripción seleccionada.</span><span class="sxs-lookup"><span data-stu-id="3eb84-191">The resource group name must be unique within the subscription you selected.</span></span> <span data-ttu-id="3eb84-192">Para más información sobre los grupos de recursos, lea el artículo [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="3eb84-192">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="3eb84-193">**Ubicación**</span><span class="sxs-lookup"><span data-stu-id="3eb84-193">**Location**</span></span>|<span data-ttu-id="3eb84-194">Oeste de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="3eb84-194">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="3eb84-195">El grupo de recursos se refiere a la ubicación del grupo de recursos y no tiene efecto alguno sobre la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="3eb84-195">The resource group refers to the location of the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="3eb84-196">La ubicación de la zona DNS siempre es "global" y no se muestra.</span><span class="sxs-lookup"><span data-stu-id="3eb84-196">The DNS zone location is always "global", and is not shown.</span></span>

### <a name="retrieve-name-servers"></a><span data-ttu-id="3eb84-197">Recuperación de los servidores de nombres</span><span class="sxs-lookup"><span data-stu-id="3eb84-197">Retrieve name servers</span></span>

1. <span data-ttu-id="3eb84-198">Con la zona DNS creada, en el panel **Favoritos** de Azure Portal, haga clic en **Todos los recursos**.</span><span class="sxs-lookup"><span data-stu-id="3eb84-198">With the DNS zone created, in the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="3eb84-199">Haga clic en la zona DNS **partners.contoso.net** en la hoja **Todos los recursos**.</span><span class="sxs-lookup"><span data-stu-id="3eb84-199">Click the **partners.contoso.net** DNS zone in the **All resources** blade.</span></span> <span data-ttu-id="3eb84-200">Si la suscripción que seleccionó ya tiene varios recursos en ella, puede escribir **partners.contoso.net** en el cuadro Filtrar por nombre…</span><span class="sxs-lookup"><span data-stu-id="3eb84-200">If the subscription you selected already has several resources in it, you can enter **partners.contoso.net** in the Filter by name…</span></span> <span data-ttu-id="3eb84-201">para acceder fácilmente a la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="3eb84-201">box to easily access the DNS zone.</span></span>

1. <span data-ttu-id="3eb84-202">Recupere los servidores de nombres en la hoja Zona DNS.</span><span class="sxs-lookup"><span data-stu-id="3eb84-202">Retrieve the name servers from the DNS zone blade.</span></span> <span data-ttu-id="3eb84-203">En este ejemplo, a la zona “contoso.net” se le han asignado los servidores de nombres “ns1-01.azure-dns.com”, “ns2-01.azure-dns.net”, “ns3-01.azure-dns.org” y “ns4-01.azure-dns.info”’:</span><span class="sxs-lookup"><span data-stu-id="3eb84-203">In this example, the zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="3eb84-205">El DNS de Azure crea automáticamente los registros NS autoritativos en la zona que contiene los servidores de nombres asignados.</span><span class="sxs-lookup"><span data-stu-id="3eb84-205">Azure DNS automatically creates authoritative NS records in your zone containing the assigned name servers.</span></span>  <span data-ttu-id="3eb84-206">Para ver los nombres del servidor de nombres mediante Azure PowerShell o CLI de Azure, simplemente necesita recuperar estos registros.</span><span class="sxs-lookup"><span data-stu-id="3eb84-206">To see the name server names via Azure PowerShell or Azure CLI, you simply need to retrieve these records.</span></span>

### <a name="create-name-server-record-in-parent-zone"></a><span data-ttu-id="3eb84-207">Creación de un registro de servidor de nombres en la zona primaria</span><span class="sxs-lookup"><span data-stu-id="3eb84-207">Create name server record in parent zone</span></span>

1. <span data-ttu-id="3eb84-208">Navegue hasta la zona DNS **contoso.net** en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3eb84-208">Navigate to the **contoso.net** DNS zone in the Azure portal.</span></span>
1. <span data-ttu-id="3eb84-209">Haga clic en **+ Conjunto de registros**.</span><span class="sxs-lookup"><span data-stu-id="3eb84-209">Click **+ Record set**</span></span>
1. <span data-ttu-id="3eb84-210">En la hoja **Agregar conjunto de registros**, escriba los valores siguientes y haga clic en **Aceptar**:</span><span class="sxs-lookup"><span data-stu-id="3eb84-210">On the **Add record set** blade, enter the following values, then click **OK**:</span></span>

   | <span data-ttu-id="3eb84-211">**Configuración**</span><span class="sxs-lookup"><span data-stu-id="3eb84-211">**Setting**</span></span> | <span data-ttu-id="3eb84-212">**Valor**</span><span class="sxs-lookup"><span data-stu-id="3eb84-212">**Value**</span></span> | <span data-ttu-id="3eb84-213">**Detalles**</span><span class="sxs-lookup"><span data-stu-id="3eb84-213">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="3eb84-214">**Name**</span><span class="sxs-lookup"><span data-stu-id="3eb84-214">**Name**</span></span>|<span data-ttu-id="3eb84-215">asociados</span><span class="sxs-lookup"><span data-stu-id="3eb84-215">partners</span></span>|<span data-ttu-id="3eb84-216">El nombre de la zona DNS secundaria</span><span class="sxs-lookup"><span data-stu-id="3eb84-216">The name of the child DNS zone</span></span>|
   |<span data-ttu-id="3eb84-217">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="3eb84-217">**Type**</span></span>|<span data-ttu-id="3eb84-218">NS</span><span class="sxs-lookup"><span data-stu-id="3eb84-218">NS</span></span>|<span data-ttu-id="3eb84-219">Utilice NS para los registros del servidor de nombres.</span><span class="sxs-lookup"><span data-stu-id="3eb84-219">Use NS for name server records.</span></span>|
   |<span data-ttu-id="3eb84-220">**TTL**</span><span class="sxs-lookup"><span data-stu-id="3eb84-220">**TTL**</span></span>|<span data-ttu-id="3eb84-221">1</span><span class="sxs-lookup"><span data-stu-id="3eb84-221">1</span></span>|<span data-ttu-id="3eb84-222">Período de vida.</span><span class="sxs-lookup"><span data-stu-id="3eb84-222">Time to live.</span></span>|
   |<span data-ttu-id="3eb84-223">**Unidad de TTL**</span><span class="sxs-lookup"><span data-stu-id="3eb84-223">**TTL unit**</span></span>|<span data-ttu-id="3eb84-224">Horas</span><span class="sxs-lookup"><span data-stu-id="3eb84-224">Hours</span></span>|<span data-ttu-id="3eb84-225">establece la unidad de período de vida en horas</span><span class="sxs-lookup"><span data-stu-id="3eb84-225">sets time to live unit to hours</span></span>|
   |<span data-ttu-id="3eb84-226">**SERVIDOR DE NOMBRES**</span><span class="sxs-lookup"><span data-stu-id="3eb84-226">**NAME SERVER**</span></span>|<span data-ttu-id="3eb84-227">{servidores de nombres de la zona partners.contoso.net}</span><span class="sxs-lookup"><span data-stu-id="3eb84-227">{name servers from partners.contoso.net zone}</span></span>|<span data-ttu-id="3eb84-228">Escriba los cuatro servidores de nombres en la zona partners.contoso.net.</span><span class="sxs-lookup"><span data-stu-id="3eb84-228">Enter all 4 of the name servers from partners.contoso.net zone.</span></span> |

   ![Dns-nameserver](./media/dns-domain-delegation/partnerzone.png)


### <a name="delegating-sub-domains-in-azure-dns-with-other-tools"></a><span data-ttu-id="3eb84-230">Delegación de subdominios en Azure DNS con otras herramientas</span><span class="sxs-lookup"><span data-stu-id="3eb84-230">Delegating sub-domains in Azure DNS with other tools</span></span>

<span data-ttu-id="3eb84-231">En los ejemplos siguientes se proporcionan los pasos para delegar subdominios en Azure DNS con PowerShell y la CLI:</span><span class="sxs-lookup"><span data-stu-id="3eb84-231">The following examples provide the steps to delegate sub-domains in Azure DNS with PowerShell and CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="3eb84-232">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3eb84-232">PowerShell</span></span>

<span data-ttu-id="3eb84-233">En el siguiente ejemplo de PowerShell se muestra cómo funciona.</span><span class="sxs-lookup"><span data-stu-id="3eb84-233">The following PowerShell example demonstrates how this works.</span></span> <span data-ttu-id="3eb84-234">Los mismos pasos se pueden ejecutar mediante Azure Portal o mediante la CLI de Azure multiplataforma.</span><span class="sxs-lookup"><span data-stu-id="3eb84-234">The same steps can be executed via the Azure portal, or via the cross-platform Azure CLI.</span></span>

```powershell
# Create the parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
$parent = New-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
$child = New-AzureRmDnsZone -Name partners.contoso.net -ResourceGroupName contosoRG

# Retrieve the authoritative NS records from the child zone as shown in the next example. This contains the name servers assigned to the child zone.
$child_ns_recordset = Get-AzureRmDnsRecordSet -Zone $child -Name "@" -RecordType NS

# Create the corresponding NS record set in the parent zone to complete the delegation. The record set name in the parent zone matches the child zone name, in this case "partners".
$parent_ns_recordset = New-AzureRmDnsRecordSet -Zone $parent -Name "partners" -RecordType NS -Ttl 3600
$parent_ns_recordset.Records = $child_ns_recordset.Records
Set-AzureRmDnsRecordSet -RecordSet $parent_ns_recordset
```

<span data-ttu-id="3eb84-235">Utilice `nslookup` para comprobar que todo está configurado correctamente mirando el registro SOA de la zona secundaria.</span><span class="sxs-lookup"><span data-stu-id="3eb84-235">Use `nslookup` to verify that everything is set up correctly by looking up the SOA record of the child zone.</span></span>

```
nslookup -type=SOA partners.contoso.com
```

```
Server: ns1-08.azure-dns.com
Address: 208.76.47.8

partners.contoso.com
    primary name server = ns1-08.azure-dns.com
    responsible mail addr = msnhst.microsoft.com
    serial = 1
    refresh = 900 (15 mins)
    retry = 300 (5 mins)
    expire = 604800 (7 days)
    default TTL = 300 (5 mins)
```

#### <a name="azure-cli"></a><span data-ttu-id="3eb84-236">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="3eb84-236">Azure CLI</span></span>

```azurecli
#!/bin/bash

# Create the parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
az network dns zone create -g contosoRG -n contoso.net
az network dns zone create -g contosoRG -n partners.contoso.net
```

<span data-ttu-id="3eb84-237">Recupere los servidores de nombres para la zona `partners.contoso.net` desde la salida.</span><span class="sxs-lookup"><span data-stu-id="3eb84-237">Retrieve the name servers for the `partners.contoso.net` zone from the output.</span></span>

```
{
  "etag": "00000003-0000-0000-418f-250de2b2d201",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosorg/providers/Microsoft.Network/dnszones/partners.contoso.net",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "partners.contoso.net",
  "nameServers": [
    "ns1-09.azure-dns.com.",
    "ns2-09.azure-dns.net.",
    "ns3-09.azure-dns.org.",
    "ns4-09.azure-dns.info."
  ],
  "numberOfRecordSets": 2,
  "resourceGroup": "contosorg",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

<span data-ttu-id="3eb84-238">Cree el conjunto de registros y los registros NS para cada servidor de nombres.</span><span class="sxs-lookup"><span data-stu-id="3eb84-238">Create the record set and NS records for each name server.</span></span>

```azurecli
#!/bin/bash

# Create the record set
az network dns record-set ns create --resource-group contosorg --zone-name contoso.net --name partners

# Create a ns record for each name server.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns1-09.azure-dns.com.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns2-09.azure-dns.net.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns3-09.azure-dns.org.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns4-09.azure-dns.info.
```

## <a name="delete-all-resources"></a><span data-ttu-id="3eb84-239">Eliminación de todos los recursos</span><span class="sxs-lookup"><span data-stu-id="3eb84-239">Delete all resources</span></span>

<span data-ttu-id="3eb84-240">Para eliminar todos los recursos creados en este artículo, complete los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3eb84-240">To delete all resources created in this article, complete the following steps:</span></span>

1. <span data-ttu-id="3eb84-241">En el panel **Favoritos** de Azure Portal, haga clic en **Todos los recursos**.</span><span class="sxs-lookup"><span data-stu-id="3eb84-241">In the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="3eb84-242">Haga clic en el grupo de recursos **contosorg** en la hoja Todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="3eb84-242">Click the **contosorg** resource group in the All resources blade.</span></span> <span data-ttu-id="3eb84-243">Si la suscripción que seleccionó ya tiene varios recursos en ella, puede escribir **contosorg** en el cuadro **Filtrar por nombre**</span><span class="sxs-lookup"><span data-stu-id="3eb84-243">If the subscription you selected already has several resources in it, you can enter **contosorg** in the **Filter by name…**</span></span> <span data-ttu-id="3eb84-244">para acceder fácilmente al grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3eb84-244">box to easily access the resource group.</span></span>
1. <span data-ttu-id="3eb84-245">En la hoja **contosorg**, haga clic en el botón **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="3eb84-245">In the **contosorg** blade, click the **Delete** button.</span></span>
1. <span data-ttu-id="3eb84-246">El portal requiere que escriba el nombre del grupo de recursos para confirmar que desea eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="3eb84-246">The portal requires you to type the name of the resource group to confirm that you want to delete it.</span></span> <span data-ttu-id="3eb84-247">Escriba *contosorg* como nombre de grupo de recursos y haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="3eb84-247">Type *contosorg* for the resource group name, then click **Delete**.</span></span> <span data-ttu-id="3eb84-248">Al eliminarse un grupo de recursos, se eliminan todos los recursos que contiene, por lo que siempre debe asegurarse de comprobar su contenido antes de eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="3eb84-248">Deleting a resource group deletes all resources within the resource group, so always be sure to confirm the contents of a resource group before deleting it.</span></span> <span data-ttu-id="3eb84-249">El portal elimina todos los recursos incluidos en el grupo de recursos y, después, el grupo de recursos en sí.</span><span class="sxs-lookup"><span data-stu-id="3eb84-249">The portal deletes all resources contained within the resource group, then deletes the resource group itself.</span></span> <span data-ttu-id="3eb84-250">Este proceso tarda varios minutos.</span><span class="sxs-lookup"><span data-stu-id="3eb84-250">This process takes several minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3eb84-251">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3eb84-251">Next steps</span></span>

[<span data-ttu-id="3eb84-252">Administración de zonas DNS</span><span class="sxs-lookup"><span data-stu-id="3eb84-252">Manage DNS zones</span></span>](dns-operations-dnszones.md)

[<span data-ttu-id="3eb84-253">Administración de registros DNS</span><span class="sxs-lookup"><span data-stu-id="3eb84-253">Manage DNS records</span></span>](dns-operations-recordsets.md)
