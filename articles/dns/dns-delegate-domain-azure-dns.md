---
title: aaaDelegate su tooAzure de dominio DNS | Documentos de Microsoft
description: "Comprender cómo toochange delegación del dominio y el uso de DNS de Azure nombre servidores tooprovide dominio hospeda."
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
ms.openlocfilehash: f780bdaa416150e5e3afe6c6845dc75ba54b6203
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-a-domain-tooazure-dns"></a><span data-ttu-id="72c1a-103">Delegar un tooAzure de dominio DNS</span><span class="sxs-lookup"><span data-stu-id="72c1a-103">Delegate a domain tooAzure DNS</span></span>

<span data-ttu-id="72c1a-104">DNS de Azure permite toohost una zona DNS y administrar los registros DNS de Hola para un dominio de Azure.</span><span class="sxs-lookup"><span data-stu-id="72c1a-104">Azure DNS allows you toohost a DNS zone and manage hello DNS records for a domain in Azure.</span></span> <span data-ttu-id="72c1a-105">En el orden de las consultas DNS para un tooreach de dominio DNS de Azure, el dominio de hello tiene toobe delegar tooAzure DNS de dominio primario de Hola.</span><span class="sxs-lookup"><span data-stu-id="72c1a-105">In order for DNS queries for a domain tooreach Azure DNS, hello domain has toobe delegated tooAzure DNS from hello parent domain.</span></span> <span data-ttu-id="72c1a-106">Tenga en cuenta el DNS de Azure no es un registrador de dominios de Hola.</span><span class="sxs-lookup"><span data-stu-id="72c1a-106">Keep in mind Azure DNS is not hello domain registrar.</span></span> <span data-ttu-id="72c1a-107">Este artículo se explica cómo toodelegate su tooAzure de dominio DNS.</span><span class="sxs-lookup"><span data-stu-id="72c1a-107">This article explains how toodelegate your domain tooAzure DNS.</span></span>

<span data-ttu-id="72c1a-108">En el caso de adquiridas a través de un registrador de dominios, el registrador ofrece Hola opción tooset estos registros NS.</span><span class="sxs-lookup"><span data-stu-id="72c1a-108">For domains purchased from a registrar, your registrar offers hello option tooset up these NS records.</span></span> <span data-ttu-id="72c1a-109">No es necesario tooown una toocreate de dominio una zona DNS con ese nombre de dominio en DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="72c1a-109">You do not have tooown a domain toocreate a DNS zone with that domain name in Azure DNS.</span></span> <span data-ttu-id="72c1a-110">Sin embargo, deberá tooown Hola dominio tooset seguridad hello tooAzure de delegación DNS con el registrador de Hola.</span><span class="sxs-lookup"><span data-stu-id="72c1a-110">However, you do need tooown hello domain tooset up hello delegation tooAzure DNS with hello registrar.</span></span>

<span data-ttu-id="72c1a-111">Por ejemplo, supongamos que compra dominio hello 'contoso.net' y crea una zona con nombre hello 'contoso.net' en DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="72c1a-111">For example, suppose you purchase hello domain 'contoso.net' and create a zone with hello name 'contoso.net' in Azure DNS.</span></span> <span data-ttu-id="72c1a-112">Como propietario de hello del dominio de hello, el registrador ofrece que Hola direcciones del servidor de nombre de opción tooconfigure Hola (es decir, registros de hello NS) para su dominio.</span><span class="sxs-lookup"><span data-stu-id="72c1a-112">As hello owner of hello domain, your registrar offers you hello option tooconfigure hello name server addresses (that is, hello NS records) for your domain.</span></span> <span data-ttu-id="72c1a-113">registrador de Hello almacena estos registros NS en dominio primario de hello, en este caso '.net'.</span><span class="sxs-lookup"><span data-stu-id="72c1a-113">hello registrar stores these NS records in hello parent domain, in this case '.net'.</span></span> <span data-ttu-id="72c1a-114">Los clientes alrededor de Hola a todos, a continuación, pueden ser dirigido tooyour dominio en la zona DNS de Azure al tratar de tooresolve registros DNS en 'contoso.net'.</span><span class="sxs-lookup"><span data-stu-id="72c1a-114">Clients around hello world can then be directed tooyour domain in Azure DNS zone when trying tooresolve DNS records in 'contoso.net'.</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="72c1a-115">Creación de una zona DNS</span><span class="sxs-lookup"><span data-stu-id="72c1a-115">Create a DNS zone</span></span>

1. <span data-ttu-id="72c1a-116">Inicie sesión en toohello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="72c1a-116">Sign in toohello Azure portal</span></span>
1. <span data-ttu-id="72c1a-117">En el menú del concentrador hello, haga clic en y haga clic en **nuevo > redes >** y, a continuación, haga clic en **zona DNS** hoja de zona de DNS crear de tooopen Hola.</span><span class="sxs-lookup"><span data-stu-id="72c1a-117">On hello Hub menu, click and click **New > Networking >** and then click **DNS zone** tooopen hello Create DNS zone blade.</span></span>

    ![Zona DNS](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="72c1a-119">En hello **zona DNS crear** escriba Hola después valores hoja, haga clic en **crear**:</span><span class="sxs-lookup"><span data-stu-id="72c1a-119">On hello **Create DNS zone** blade enter hello following values, then click **Create**:</span></span>

   | <span data-ttu-id="72c1a-120">**Configuración**</span><span class="sxs-lookup"><span data-stu-id="72c1a-120">**Setting**</span></span> | <span data-ttu-id="72c1a-121">**Valor**</span><span class="sxs-lookup"><span data-stu-id="72c1a-121">**Value**</span></span> | <span data-ttu-id="72c1a-122">**Detalles**</span><span class="sxs-lookup"><span data-stu-id="72c1a-122">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="72c1a-123">**Name**</span><span class="sxs-lookup"><span data-stu-id="72c1a-123">**Name**</span></span>|<span data-ttu-id="72c1a-124">contoso.net</span><span class="sxs-lookup"><span data-stu-id="72c1a-124">contoso.net</span></span>|<span data-ttu-id="72c1a-125">nombre de Hola de zona DNS de Hola</span><span class="sxs-lookup"><span data-stu-id="72c1a-125">hello name of hello DNS zone</span></span>|
   |<span data-ttu-id="72c1a-126">**Suscripción**</span><span class="sxs-lookup"><span data-stu-id="72c1a-126">**Subscription**</span></span>|<span data-ttu-id="72c1a-127">[Su suscripción]</span><span class="sxs-lookup"><span data-stu-id="72c1a-127">[Your subscription]</span></span>|<span data-ttu-id="72c1a-128">Seleccione una puerta de enlace de suscripción toocreate Hola aplicación en.</span><span class="sxs-lookup"><span data-stu-id="72c1a-128">Select a subscription toocreate hello application gateway in.</span></span>|
   |<span data-ttu-id="72c1a-129">**Grupos de recursos**</span><span class="sxs-lookup"><span data-stu-id="72c1a-129">**Resource group**</span></span>|<span data-ttu-id="72c1a-130">**Crear nuevo:** contosoRG</span><span class="sxs-lookup"><span data-stu-id="72c1a-130">**Create new:** contosoRG</span></span>|<span data-ttu-id="72c1a-131">Cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="72c1a-131">Create a resource group.</span></span> <span data-ttu-id="72c1a-132">nombre de grupo de recursos de Hello debe ser único dentro de la suscripción de Hola que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="72c1a-132">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="72c1a-133">más información acerca de los grupos de recursos, leer hello toolearn [el Administrador de recursos](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) artículo de información general.</span><span class="sxs-lookup"><span data-stu-id="72c1a-133">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="72c1a-134">**Ubicación**</span><span class="sxs-lookup"><span data-stu-id="72c1a-134">**Location**</span></span>|<span data-ttu-id="72c1a-135">Oeste de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="72c1a-135">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="72c1a-136">grupo de recursos de Hello hace referencia la ubicación de toohello Hola del grupo de recursos y no tiene ningún efecto en la zona DNS de Hola.</span><span class="sxs-lookup"><span data-stu-id="72c1a-136">hello resource group refers toohello location of hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="72c1a-137">ubicación de la zona DNS Hola siempre es "global" y no se muestra.</span><span class="sxs-lookup"><span data-stu-id="72c1a-137">hello DNS zone location is always "global", and is not shown.</span></span>

## <a name="retrieve-name-servers"></a><span data-ttu-id="72c1a-138">Recuperación de los servidores de nombres</span><span class="sxs-lookup"><span data-stu-id="72c1a-138">Retrieve name servers</span></span>

<span data-ttu-id="72c1a-139">Antes de que puede delegar su tooAzure de zona DNS de DNS, primero debe tooknow Hola nombre nombres de los servidores de la zona.</span><span class="sxs-lookup"><span data-stu-id="72c1a-139">Before you can delegate your DNS zone tooAzure DNS, you first need tooknow hello name server names for your zone.</span></span> <span data-ttu-id="72c1a-140">El DNS de Azure asigna los servidores de nombres de un grupo cada vez que se crea una zona.</span><span class="sxs-lookup"><span data-stu-id="72c1a-140">Azure DNS allocates name servers from a pool each time a zone is created.</span></span>

1. <span data-ttu-id="72c1a-141">Con zona DNS de hello creada, en el portal de Azure hello **favoritos** panel, haga clic en **todos los recursos**.</span><span class="sxs-lookup"><span data-stu-id="72c1a-141">With hello DNS zone created, in hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="72c1a-142">Haga clic en hello **contoso.net** zona DNS en hello **todos los recursos** hoja.</span><span class="sxs-lookup"><span data-stu-id="72c1a-142">Click hello **contoso.net** DNS zone in hello **All resources** blade.</span></span> <span data-ttu-id="72c1a-143">Si la suscripción de Hola que ha seleccionado ya tiene varios recursos en ella, puede escribir **contoso.net** Hola filtro por nombre...</span><span class="sxs-lookup"><span data-stu-id="72c1a-143">If hello subscription you selected already has several resources in it, you can enter **contoso.net** in hello Filter by name…</span></span> <span data-ttu-id="72c1a-144">puerta de enlace de cuadro tooeasily acceso Hola aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="72c1a-144">box tooeasily access hello application gateway.</span></span> 

1. <span data-ttu-id="72c1a-145">Recuperar los servidores de nombres de Hola de hoja de zona DNS de Hola.</span><span class="sxs-lookup"><span data-stu-id="72c1a-145">Retrieve hello name servers from hello DNS zone blade.</span></span> <span data-ttu-id="72c1a-146">En este ejemplo, zona hello 'contoso.net' se ha asignado los servidores de nombres ' ns1-01.azure-dns.com', 'ns2-01.azure-dns .net', ' ns3-01.azure-dns.org', y ' ns4-01.azure-dns.info':</span><span class="sxs-lookup"><span data-stu-id="72c1a-146">In this example, hello zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="72c1a-148">DNS de Azure crea automáticamente los registros NS autoritativos en la zona que contiene servidores de nombres asignado de Hola.</span><span class="sxs-lookup"><span data-stu-id="72c1a-148">Azure DNS automatically creates authoritative NS records in your zone containing hello assigned name servers.</span></span>  <span data-ttu-id="72c1a-149">nombres de servidor de nombres de hello toosee a través de Azure PowerShell o CLI de Azure, simplemente necesita tooretrieve estos registros.</span><span class="sxs-lookup"><span data-stu-id="72c1a-149">toosee hello name server names via Azure PowerShell or Azure CLI, you simply need tooretrieve these records.</span></span>

<span data-ttu-id="72c1a-150">Hello en los ejemplos siguientes también proporcionan pasos Hola servidores de nombres de hello tooretrieve para una zona de DNS de Azure con PowerShell y la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="72c1a-150">hello following examples also provide hello steps tooretrieve hello name servers for a zone in Azure DNS with PowerShell and Azure CLI.</span></span>

### <a name="powershell"></a><span data-ttu-id="72c1a-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="72c1a-151">PowerShell</span></span>

```powershell
# hello record name "@" is used toorefer toorecords at hello top of hello zone.
$zone = Get-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -Zone $zone
```

<span data-ttu-id="72c1a-152">Hola siguiente ejemplo es la respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="72c1a-152">hello following example is hello response.</span></span>

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

### <a name="azure-cli"></a><span data-ttu-id="72c1a-153">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="72c1a-153">Azure CLI</span></span>

```azurecli
az network dns record-set show --resource-group contosoRG --zone-name contoso.net --type NS --name @
```

<span data-ttu-id="72c1a-154">Hola siguiente ejemplo es la respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="72c1a-154">hello following example is hello response.</span></span>

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

## <a name="delegate-hello-domain"></a><span data-ttu-id="72c1a-155">Dominio de Hola de delegado</span><span class="sxs-lookup"><span data-stu-id="72c1a-155">Delegate hello domain</span></span>

<span data-ttu-id="72c1a-156">Ahora que se crea la zona DNS de Hola y tiene servidores de nombres de hello, dominio primario de hello debe toobe actualizado con servidores de nombres DNS de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="72c1a-156">Now that hello DNS zone is created and you have hello name servers, hello parent domain needs toobe updated with hello Azure DNS name servers.</span></span> <span data-ttu-id="72c1a-157">Cada registrador tiene sus propios registros DNS administración herramientas toochange Hola nombre servidor para un dominio.</span><span class="sxs-lookup"><span data-stu-id="72c1a-157">Each registrar has their own DNS management tools toochange hello name server records for a domain.</span></span> <span data-ttu-id="72c1a-158">En la página de administración de DNS del registrador de hello, editar los registros NS hello y reemplace los registros NS Hola por hello las que DNS de Azure creado.</span><span class="sxs-lookup"><span data-stu-id="72c1a-158">In hello registrar's DNS management page, edit hello NS records and replace hello NS records with hello ones Azure DNS created.</span></span>

<span data-ttu-id="72c1a-159">Al delegar un tooAzure de dominio DNS, debe usar nombres de servidor de nombre de hello proporcionados por DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="72c1a-159">When delegating a domain tooAzure DNS, you must use hello name server names provided by Azure DNS.</span></span> <span data-ttu-id="72c1a-160">Se recomienda toouse todos los cuatro nombres para los nombres de servidor, independientemente del nombre de Hola de su dominio.</span><span class="sxs-lookup"><span data-stu-id="72c1a-160">It is recommended toouse all four name server names, regardless of hello name of your domain.</span></span> <span data-ttu-id="72c1a-161">Delegación de dominio no requiere toouse de nombre de servidor de nombre de Hola Hola mismo dominio de nivel superior que el dominio.</span><span class="sxs-lookup"><span data-stu-id="72c1a-161">Domain delegation does not require hello name server name toouse hello same top-level domain as your domain.</span></span>

<span data-ttu-id="72c1a-162">No se deben usar 'búsqueda de registros' toopoint toohello Azure nombre IP direcciones de servidor DNS, puesto que estas direcciones IP pueden cambiar en el futuro.</span><span class="sxs-lookup"><span data-stu-id="72c1a-162">You should not use 'glue records' toopoint toohello Azure DNS name server IP addresses, since these IP addresses may change in future.</span></span> <span data-ttu-id="72c1a-163">Las delegaciones que usan nombres de servidor en su propia zona (a veces denominados "servidores DNS personalizados") no se admiten de momento en DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="72c1a-163">Delegations using name server names in your own zone, sometimes called 'vanity name servers', are not currently supported in Azure DNS.</span></span>

## <a name="verify-name-resolution-is-working"></a><span data-ttu-id="72c1a-164">Comprobación del funcionamiento de la resolución de nombres</span><span class="sxs-lookup"><span data-stu-id="72c1a-164">Verify name resolution is working</span></span>

<span data-ttu-id="72c1a-165">Después de completar la delegación hello, puede comprobar que la resolución de nombres funciona con una herramienta como 'nslookup' tooquery Hola registro SOA de la zona (que se crea automáticamente cuando se crea la zona de hello).</span><span class="sxs-lookup"><span data-stu-id="72c1a-165">After completing hello delegation, you can verify that name resolution is working by using a tool such as 'nslookup' tooquery hello SOA record for your zone (which is also automatically created when hello zone is created).</span></span>

<span data-ttu-id="72c1a-166">No tiene servidores de nombres DNS de Azure de toospecify hello, si se ha configurado la delegación Hola correctamente, Hola DNS resolución proceso normal busca automáticamente los servidores de nombres de Hola.</span><span class="sxs-lookup"><span data-stu-id="72c1a-166">You do not have toospecify hello Azure DNS name servers, if hello delegation has been set up correctly, hello normal DNS resolution process finds hello name servers automatically.</span></span>

```
nslookup -type=SOA contoso.com
```

<span data-ttu-id="72c1a-167">Hola te mostramos una respuesta de ejemplo de Hola anterior comando:</span><span class="sxs-lookup"><span data-stu-id="72c1a-167">hello following is an example response from hello preceding command:</span></span>

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

## <a name="delegate-sub-domains-in-azure-dns"></a><span data-ttu-id="72c1a-168">Delegación de subdominios en Azure DNS</span><span class="sxs-lookup"><span data-stu-id="72c1a-168">Delegate sub-domains in Azure DNS</span></span>

<span data-ttu-id="72c1a-169">Si desea tooset una zona secundaria independiente, puede delegar un subdominio en DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="72c1a-169">If you want tooset up a separate child zone, you can delegate a sub-domain in Azure DNS.</span></span> <span data-ttu-id="72c1a-170">Por ejemplo, después de configurar y delegado 'contoso.net' en el DNS de Azure, suponga que le gustaría tooset una zona secundaria independiente, 'partners.contoso.net'.</span><span class="sxs-lookup"><span data-stu-id="72c1a-170">For example, having set up and delegated 'contoso.net' in Azure DNS, suppose you would like tooset up a separate child zone, 'partners.contoso.net'.</span></span>

1. <span data-ttu-id="72c1a-171">Crear zona de secundarios de hello 'partners.contoso.net' en el DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="72c1a-171">Create hello child zone 'partners.contoso.net' in Azure DNS.</span></span>
2. <span data-ttu-id="72c1a-172">Buscar registros NS autoritativos de hello en hello secundarios zona tooobtain Hola servidores de nombres donde se hospeda Hola secundarios zona de DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="72c1a-172">Look up hello authoritative NS records in hello child zone tooobtain hello name servers hosting hello child zone in Azure DNS.</span></span>
3. <span data-ttu-id="72c1a-173">Delegar la zona secundaria de hello mediante la configuración de los registros NS en zona primaria de Hola que señala la zona secundaria de toohello.</span><span class="sxs-lookup"><span data-stu-id="72c1a-173">Delegate hello child zone by configuring NS records in hello parent zone pointing toohello child zone.</span></span>

### <a name="create-a-dns-zone"></a><span data-ttu-id="72c1a-174">Creación de una zona DNS</span><span class="sxs-lookup"><span data-stu-id="72c1a-174">Create a DNS zone</span></span>

1. <span data-ttu-id="72c1a-175">Inicie sesión en toohello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="72c1a-175">Sign in toohello Azure portal</span></span>
1. <span data-ttu-id="72c1a-176">En el menú del concentrador hello, haga clic en y haga clic en **nuevo > redes >** y, a continuación, haga clic en **zona DNS** hoja de zona de DNS crear de tooopen Hola.</span><span class="sxs-lookup"><span data-stu-id="72c1a-176">On hello Hub menu, click and click **New > Networking >** and then click **DNS zone** tooopen hello Create DNS zone blade.</span></span>

    ![Zona DNS](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="72c1a-178">En hello **zona DNS crear** escriba Hola después valores hoja, haga clic en **crear**:</span><span class="sxs-lookup"><span data-stu-id="72c1a-178">On hello **Create DNS zone** blade enter hello following values, then click **Create**:</span></span>

   | <span data-ttu-id="72c1a-179">**Configuración**</span><span class="sxs-lookup"><span data-stu-id="72c1a-179">**Setting**</span></span> | <span data-ttu-id="72c1a-180">**Valor**</span><span class="sxs-lookup"><span data-stu-id="72c1a-180">**Value**</span></span> | <span data-ttu-id="72c1a-181">**Detalles**</span><span class="sxs-lookup"><span data-stu-id="72c1a-181">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="72c1a-182">**Name**</span><span class="sxs-lookup"><span data-stu-id="72c1a-182">**Name**</span></span>|<span data-ttu-id="72c1a-183">partners.contoso.net</span><span class="sxs-lookup"><span data-stu-id="72c1a-183">partners.contoso.net</span></span>|<span data-ttu-id="72c1a-184">nombre de Hola de zona DNS de Hola</span><span class="sxs-lookup"><span data-stu-id="72c1a-184">hello name of hello DNS zone</span></span>|
   |<span data-ttu-id="72c1a-185">**Suscripción**</span><span class="sxs-lookup"><span data-stu-id="72c1a-185">**Subscription**</span></span>|<span data-ttu-id="72c1a-186">[Su suscripción]</span><span class="sxs-lookup"><span data-stu-id="72c1a-186">[Your subscription]</span></span>|<span data-ttu-id="72c1a-187">Seleccione una puerta de enlace de suscripción toocreate Hola aplicación en.</span><span class="sxs-lookup"><span data-stu-id="72c1a-187">Select a subscription toocreate hello application gateway in.</span></span>|
   |<span data-ttu-id="72c1a-188">**Grupos de recursos**</span><span class="sxs-lookup"><span data-stu-id="72c1a-188">**Resource group**</span></span>|<span data-ttu-id="72c1a-189">**Usar existente:** contosoRG</span><span class="sxs-lookup"><span data-stu-id="72c1a-189">**Use Existing:** contosoRG</span></span>|<span data-ttu-id="72c1a-190">Cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="72c1a-190">Create a resource group.</span></span> <span data-ttu-id="72c1a-191">nombre de grupo de recursos de Hello debe ser único dentro de la suscripción de Hola que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="72c1a-191">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="72c1a-192">más información acerca de los grupos de recursos, leer hello toolearn [el Administrador de recursos](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) artículo de información general.</span><span class="sxs-lookup"><span data-stu-id="72c1a-192">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="72c1a-193">**Ubicación**</span><span class="sxs-lookup"><span data-stu-id="72c1a-193">**Location**</span></span>|<span data-ttu-id="72c1a-194">Oeste de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="72c1a-194">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="72c1a-195">grupo de recursos de Hello hace referencia la ubicación de toohello Hola del grupo de recursos y no tiene ningún efecto en la zona DNS de Hola.</span><span class="sxs-lookup"><span data-stu-id="72c1a-195">hello resource group refers toohello location of hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="72c1a-196">ubicación de la zona DNS Hola siempre es "global" y no se muestra.</span><span class="sxs-lookup"><span data-stu-id="72c1a-196">hello DNS zone location is always "global", and is not shown.</span></span>

### <a name="retrieve-name-servers"></a><span data-ttu-id="72c1a-197">Recuperación de los servidores de nombres</span><span class="sxs-lookup"><span data-stu-id="72c1a-197">Retrieve name servers</span></span>

1. <span data-ttu-id="72c1a-198">Con zona DNS de hello creada, en el portal de Azure hello **favoritos** panel, haga clic en **todos los recursos**.</span><span class="sxs-lookup"><span data-stu-id="72c1a-198">With hello DNS zone created, in hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="72c1a-199">Haga clic en hello **partners.contoso.net** zona DNS en hello **todos los recursos** hoja.</span><span class="sxs-lookup"><span data-stu-id="72c1a-199">Click hello **partners.contoso.net** DNS zone in hello **All resources** blade.</span></span> <span data-ttu-id="72c1a-200">Si la suscripción de Hola que ha seleccionado ya tiene varios recursos en ella, puede escribir **partners.contoso.net** Hola filtro por nombre...</span><span class="sxs-lookup"><span data-stu-id="72c1a-200">If hello subscription you selected already has several resources in it, you can enter **partners.contoso.net** in hello Filter by name…</span></span> <span data-ttu-id="72c1a-201">zona DNS de cuadro tooeasily acceso Hola.</span><span class="sxs-lookup"><span data-stu-id="72c1a-201">box tooeasily access hello DNS zone.</span></span>

1. <span data-ttu-id="72c1a-202">Recuperar los servidores de nombres de Hola de hoja de zona DNS de Hola.</span><span class="sxs-lookup"><span data-stu-id="72c1a-202">Retrieve hello name servers from hello DNS zone blade.</span></span> <span data-ttu-id="72c1a-203">En este ejemplo, zona hello 'contoso.net' se ha asignado los servidores de nombres ' ns1-01.azure-dns.com', 'ns2-01.azure-dns .net', ' ns3-01.azure-dns.org', y ' ns4-01.azure-dns.info':</span><span class="sxs-lookup"><span data-stu-id="72c1a-203">In this example, hello zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="72c1a-205">DNS de Azure crea automáticamente los registros NS autoritativos en la zona que contiene servidores de nombres asignado de Hola.</span><span class="sxs-lookup"><span data-stu-id="72c1a-205">Azure DNS automatically creates authoritative NS records in your zone containing hello assigned name servers.</span></span>  <span data-ttu-id="72c1a-206">nombres de servidor de nombres de hello toosee a través de Azure PowerShell o CLI de Azure, simplemente necesita tooretrieve estos registros.</span><span class="sxs-lookup"><span data-stu-id="72c1a-206">toosee hello name server names via Azure PowerShell or Azure CLI, you simply need tooretrieve these records.</span></span>

### <a name="create-name-server-record-in-parent-zone"></a><span data-ttu-id="72c1a-207">Creación de un registro de servidor de nombres en la zona primaria</span><span class="sxs-lookup"><span data-stu-id="72c1a-207">Create name server record in parent zone</span></span>

1. <span data-ttu-id="72c1a-208">Navegue toohello **contoso.net** zona DNS en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="72c1a-208">Navigate toohello **contoso.net** DNS zone in hello Azure portal.</span></span>
1. <span data-ttu-id="72c1a-209">Haga clic en **+ Conjunto de registros**.</span><span class="sxs-lookup"><span data-stu-id="72c1a-209">Click **+ Record set**</span></span>
1. <span data-ttu-id="72c1a-210">En hello **Agregar conjunto de registros** hoja, escriba Hola después de valores, a continuación, haga clic en **Aceptar**:</span><span class="sxs-lookup"><span data-stu-id="72c1a-210">On hello **Add record set** blade, enter hello following values, then click **OK**:</span></span>

   | <span data-ttu-id="72c1a-211">**Configuración**</span><span class="sxs-lookup"><span data-stu-id="72c1a-211">**Setting**</span></span> | <span data-ttu-id="72c1a-212">**Valor**</span><span class="sxs-lookup"><span data-stu-id="72c1a-212">**Value**</span></span> | <span data-ttu-id="72c1a-213">**Detalles**</span><span class="sxs-lookup"><span data-stu-id="72c1a-213">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="72c1a-214">**Name**</span><span class="sxs-lookup"><span data-stu-id="72c1a-214">**Name**</span></span>|<span data-ttu-id="72c1a-215">asociados</span><span class="sxs-lookup"><span data-stu-id="72c1a-215">partners</span></span>|<span data-ttu-id="72c1a-216">nombre de Hola de zona DNS secundarios Hola</span><span class="sxs-lookup"><span data-stu-id="72c1a-216">hello name of hello child DNS zone</span></span>|
   |<span data-ttu-id="72c1a-217">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="72c1a-217">**Type**</span></span>|<span data-ttu-id="72c1a-218">NS</span><span class="sxs-lookup"><span data-stu-id="72c1a-218">NS</span></span>|<span data-ttu-id="72c1a-219">Utilice NS para los registros del servidor de nombres.</span><span class="sxs-lookup"><span data-stu-id="72c1a-219">Use NS for name server records.</span></span>|
   |<span data-ttu-id="72c1a-220">**TTL**</span><span class="sxs-lookup"><span data-stu-id="72c1a-220">**TTL**</span></span>|<span data-ttu-id="72c1a-221">1</span><span class="sxs-lookup"><span data-stu-id="72c1a-221">1</span></span>|<span data-ttu-id="72c1a-222">Tiempo toolive.</span><span class="sxs-lookup"><span data-stu-id="72c1a-222">Time toolive.</span></span>|
   |<span data-ttu-id="72c1a-223">**Unidad de TTL**</span><span class="sxs-lookup"><span data-stu-id="72c1a-223">**TTL unit**</span></span>|<span data-ttu-id="72c1a-224">Horas</span><span class="sxs-lookup"><span data-stu-id="72c1a-224">Hours</span></span>|<span data-ttu-id="72c1a-225">establece toohours toolive unidad de tiempo</span><span class="sxs-lookup"><span data-stu-id="72c1a-225">sets time toolive unit toohours</span></span>|
   |<span data-ttu-id="72c1a-226">**SERVIDOR DE NOMBRES**</span><span class="sxs-lookup"><span data-stu-id="72c1a-226">**NAME SERVER**</span></span>|<span data-ttu-id="72c1a-227">{servidores de nombres de la zona partners.contoso.net}</span><span class="sxs-lookup"><span data-stu-id="72c1a-227">{name servers from partners.contoso.net zone}</span></span>|<span data-ttu-id="72c1a-228">Escriba todos los 4 hello de servidores de nombres de zona partners.contoso.net.</span><span class="sxs-lookup"><span data-stu-id="72c1a-228">Enter all 4 of hello name servers from partners.contoso.net zone.</span></span> |

   ![Dns-nameserver](./media/dns-domain-delegation/partnerzone.png)


### <a name="delegating-sub-domains-in-azure-dns-with-other-tools"></a><span data-ttu-id="72c1a-230">Delegación de subdominios en Azure DNS con otras herramientas</span><span class="sxs-lookup"><span data-stu-id="72c1a-230">Delegating sub-domains in Azure DNS with other tools</span></span>

<span data-ttu-id="72c1a-231">Hello en los ejemplos siguientes proporcionan pasos hello toodelegate subdominios en DNS de Azure con PowerShell y la CLI:</span><span class="sxs-lookup"><span data-stu-id="72c1a-231">hello following examples provide hello steps toodelegate sub-domains in Azure DNS with PowerShell and CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="72c1a-232">PowerShell</span><span class="sxs-lookup"><span data-stu-id="72c1a-232">PowerShell</span></span>

<span data-ttu-id="72c1a-233">Hola PowerShell ejemplo siguiente muestra cómo funciona.</span><span class="sxs-lookup"><span data-stu-id="72c1a-233">hello following PowerShell example demonstrates how this works.</span></span> <span data-ttu-id="72c1a-234">Hola mismos pasos se pueden ejecutar a través del portal de Azure de Hola o a través de Hola CLI de Azure entre plataformas.</span><span class="sxs-lookup"><span data-stu-id="72c1a-234">hello same steps can be executed via hello Azure portal, or via hello cross-platform Azure CLI.</span></span>

```powershell
# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
$parent = New-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
$child = New-AzureRmDnsZone -Name partners.contoso.net -ResourceGroupName contosoRG

# Retrieve hello authoritative NS records from hello child zone as shown in hello next example. This contains hello name servers assigned toohello child zone.
$child_ns_recordset = Get-AzureRmDnsRecordSet -Zone $child -Name "@" -RecordType NS

# Create hello corresponding NS record set in hello parent zone toocomplete hello delegation. hello record set name in hello parent zone matches hello child zone name, in this case "partners".
$parent_ns_recordset = New-AzureRmDnsRecordSet -Zone $parent -Name "partners" -RecordType NS -Ttl 3600
$parent_ns_recordset.Records = $child_ns_recordset.Records
Set-AzureRmDnsRecordSet -RecordSet $parent_ns_recordset
```

<span data-ttu-id="72c1a-235">Use `nslookup` tooverify que todo está configurado correctamente mediante la búsqueda Hola registro SOA de zona secundaria de Hola.</span><span class="sxs-lookup"><span data-stu-id="72c1a-235">Use `nslookup` tooverify that everything is set up correctly by looking up hello SOA record of hello child zone.</span></span>

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

#### <a name="azure-cli"></a><span data-ttu-id="72c1a-236">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="72c1a-236">Azure CLI</span></span>

```azurecli
#!/bin/bash

# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
az network dns zone create -g contosoRG -n contoso.net
az network dns zone create -g contosoRG -n partners.contoso.net
```

<span data-ttu-id="72c1a-237">Recuperar los servidores de nombres de Hola para hello `partners.contoso.net` zona desde la salida de hello.</span><span class="sxs-lookup"><span data-stu-id="72c1a-237">Retrieve hello name servers for hello `partners.contoso.net` zone from hello output.</span></span>

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

<span data-ttu-id="72c1a-238">Crear conjunto de registros de Hola y los registros NS para cada servidor de nombres.</span><span class="sxs-lookup"><span data-stu-id="72c1a-238">Create hello record set and NS records for each name server.</span></span>

```azurecli
#!/bin/bash

# Create hello record set
az network dns record-set ns create --resource-group contosorg --zone-name contoso.net --name partners

# Create a ns record for each name server.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns1-09.azure-dns.com.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns2-09.azure-dns.net.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns3-09.azure-dns.org.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns4-09.azure-dns.info.
```

## <a name="delete-all-resources"></a><span data-ttu-id="72c1a-239">Eliminación de todos los recursos</span><span class="sxs-lookup"><span data-stu-id="72c1a-239">Delete all resources</span></span>

<span data-ttu-id="72c1a-240">toodelete todos los recursos que se crean en este artículo, Hola completa pasos:</span><span class="sxs-lookup"><span data-stu-id="72c1a-240">toodelete all resources created in this article, complete hello following steps:</span></span>

1. <span data-ttu-id="72c1a-241">En el portal de Azure hello **favoritos** panel, haga clic en **todos los recursos**.</span><span class="sxs-lookup"><span data-stu-id="72c1a-241">In hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="72c1a-242">Haga clic en hello **contosorg** grupo de recursos en hello todos los módulos de recursos.</span><span class="sxs-lookup"><span data-stu-id="72c1a-242">Click hello **contosorg** resource group in hello All resources blade.</span></span> <span data-ttu-id="72c1a-243">Si la suscripción de Hola que ha seleccionado ya tiene varios recursos en ella, puede escribir **contosorg** en hello **filtrar por nombre...**</span><span class="sxs-lookup"><span data-stu-id="72c1a-243">If hello subscription you selected already has several resources in it, you can enter **contosorg** in hello **Filter by name…**</span></span> <span data-ttu-id="72c1a-244">grupo de recursos de cuadro tooeasily acceso Hola.</span><span class="sxs-lookup"><span data-stu-id="72c1a-244">box tooeasily access hello resource group.</span></span>
1. <span data-ttu-id="72c1a-245">Hola **contosorg** hoja, haga clic en hello **eliminar** botón.</span><span class="sxs-lookup"><span data-stu-id="72c1a-245">In hello **contosorg** blade, click hello **Delete** button.</span></span>
1. <span data-ttu-id="72c1a-246">Hello portal requiere tootype Hola nombre del tooconfirm de grupo de recursos de Hola que desea que toodelete lo.</span><span class="sxs-lookup"><span data-stu-id="72c1a-246">hello portal requires you tootype hello name of hello resource group tooconfirm that you want toodelete it.</span></span> <span data-ttu-id="72c1a-247">Tipo de *contosorg* nombre de grupo de recursos de hello, a continuación, haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="72c1a-247">Type *contosorg* for hello resource group name, then click **Delete**.</span></span> <span data-ttu-id="72c1a-248">Al eliminar un grupo de recursos eliminan todos los recursos en el grupo de recursos de hello, por lo que siempre puede tooconfirm seguro de contenido de Hola de un grupo de recursos antes de eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="72c1a-248">Deleting a resource group deletes all resources within hello resource group, so always be sure tooconfirm hello contents of a resource group before deleting it.</span></span> <span data-ttu-id="72c1a-249">portal de Hello elimina todos los recursos incluidos en el grupo de recursos de hello, a continuación, elimina el grupo de recursos de hello propio.</span><span class="sxs-lookup"><span data-stu-id="72c1a-249">hello portal deletes all resources contained within hello resource group, then deletes hello resource group itself.</span></span> <span data-ttu-id="72c1a-250">Este proceso tarda varios minutos.</span><span class="sxs-lookup"><span data-stu-id="72c1a-250">This process takes several minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72c1a-251">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="72c1a-251">Next steps</span></span>

[<span data-ttu-id="72c1a-252">Administración de zonas DNS</span><span class="sxs-lookup"><span data-stu-id="72c1a-252">Manage DNS zones</span></span>](dns-operations-dnszones.md)

[<span data-ttu-id="72c1a-253">Administración de registros DNS</span><span class="sxs-lookup"><span data-stu-id="72c1a-253">Manage DNS records</span></span>](dns-operations-recordsets.md)
