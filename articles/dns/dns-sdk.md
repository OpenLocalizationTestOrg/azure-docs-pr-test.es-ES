---
title: las zonas DNS de aaaCreate y conjuntos de registros de DNS de Azure utilizando Hola .NET SDK | Documentos de Microsoft
description: "¿Cómo toocreate zonas DNS y un registro establece en DNS de Azure mediante Hola .NET SDK."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: eed99b87-f4d4-4fbf-a926-263f7e30b884
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/19/2016
ms.author: jonatul
ms.openlocfilehash: e3bab98b13b787427219acb7ec55e53490512fe7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-dns-zones-and-record-sets-using-hello-net-sdk"></a><span data-ttu-id="85f2d-103">Crear las zonas DNS y los conjuntos de registros mediante Hola SDK para .NET</span><span class="sxs-lookup"><span data-stu-id="85f2d-103">Create DNS zones and record sets using hello .NET SDK</span></span>

<span data-ttu-id="85f2d-104">Puede automatizar operaciones toocreate, eliminación o actualización de zonas de DNS, conjuntos de registros y los registros mediante DNS SDK con la biblioteca de administración de DNS. NET.</span><span class="sxs-lookup"><span data-stu-id="85f2d-104">You can automate operations toocreate, delete, or update DNS zones, record sets, and records by using DNS SDK with .NET DNS Management library.</span></span> <span data-ttu-id="85f2d-105">Un proyecto completo de Visual Studio se encuentra disponible [aquí](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True).</span><span class="sxs-lookup"><span data-stu-id="85f2d-105">A full Visual Studio project is available [here.](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)</span></span>

## <a name="create-a-service-principal-account"></a><span data-ttu-id="85f2d-106">Creación de una cuenta de entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="85f2d-106">Create a service principal account</span></span>

<span data-ttu-id="85f2d-107">Normalmente, se concede recursos tooAzure de acceso mediante programación a través de una cuenta dedicada en lugar de sus propias credenciales de usuario.</span><span class="sxs-lookup"><span data-stu-id="85f2d-107">Typically, programmatic access tooAzure resources is granted via a dedicated account rather than your own user credentials.</span></span> <span data-ttu-id="85f2d-108">Estas cuentas dedicadas se denominan cuentas de 'entidad de servicio'.</span><span class="sxs-lookup"><span data-stu-id="85f2d-108">These dedicated accounts are called 'service principal' accounts.</span></span> <span data-ttu-id="85f2d-109">proyecto de ejemplo de Hola toouse Azure SDK de DNS, primero necesita una cuenta de entidad de servicio toocreate y asignar los permisos correctos de Hola.</span><span class="sxs-lookup"><span data-stu-id="85f2d-109">toouse hello Azure DNS SDK sample project, you first need toocreate a service principal account and assign it hello correct permissions.</span></span>

1. <span data-ttu-id="85f2d-110">Siga [estas instrucciones](../azure-resource-manager/resource-group-authenticate-service-principal.md) toocreate una cuenta de entidad de servicio (proyecto de ejemplo de SDK de DNS de Azure de hello supone autenticación basada en contraseña).</span><span class="sxs-lookup"><span data-stu-id="85f2d-110">Follow [these instructions](../azure-resource-manager/resource-group-authenticate-service-principal.md) toocreate a service principal account (hello Azure DNS SDK sample project assumes password-based authentication.)</span></span>
2. <span data-ttu-id="85f2d-111">Cree un grupo de recursos ([aquí se explica cómo](../azure-resource-manager/resource-group-template-deploy-portal.md)).</span><span class="sxs-lookup"><span data-stu-id="85f2d-111">Create a resource group ([here's how](../azure-resource-manager/resource-group-template-deploy-portal.md)).</span></span>
3. <span data-ttu-id="85f2d-112">Use RBAC de Azure toogrant Hola servicio cuenta de entidad 'Colaborador de zona DNS' permisos toohello grupo de recursos ([mostramos cómo](../active-directory/role-based-access-control-configure.md).)</span><span class="sxs-lookup"><span data-stu-id="85f2d-112">Use Azure RBAC toogrant hello service principal account 'DNS Zone Contributor' permissions toohello resource group ([here's how](../active-directory/role-based-access-control-configure.md).)</span></span>
4. <span data-ttu-id="85f2d-113">Si utiliza el proyecto de ejemplo de SDK de DNS de Azure de hello, edite hello 'program.cs' como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="85f2d-113">If using hello Azure DNS SDK sample project, edit hello 'program.cs' file as follows:</span></span>

   * <span data-ttu-id="85f2d-114">Insertar valores correctos de Hola hello tenantId, clientId (también conocido como Id. de cuenta), secreto (contraseña de cuenta de entidad de servicio) y Id. de suscripción como se utiliza en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="85f2d-114">Insert hello correct values for hello tenantId, clientId (also known as account ID), secret (service principal account password) and subscriptionId as used in step 1.</span></span>
   * <span data-ttu-id="85f2d-115">Escriba el nombre del grupo de recursos de hello elegido en el paso 2.</span><span class="sxs-lookup"><span data-stu-id="85f2d-115">Enter hello resource group name chosen in step 2.</span></span>
   * <span data-ttu-id="85f2d-116">Escriba un nombre de zona DNS de su elección.</span><span class="sxs-lookup"><span data-stu-id="85f2d-116">Enter a DNS zone name of your choice.</span></span>

## <a name="nuget-packages-and-namespace-declarations"></a><span data-ttu-id="85f2d-117">Paquetes NuGet y declaraciones de espacio de nombres</span><span class="sxs-lookup"><span data-stu-id="85f2d-117">NuGet packages and namespace declarations</span></span>

<span data-ttu-id="85f2d-118">toouse Hola DNS de Azure .NET SDK, deberá hello tooinstall **biblioteca de administración de DNS de Azure** paquete de NuGet y otro necesario paquetes de Azure.</span><span class="sxs-lookup"><span data-stu-id="85f2d-118">toouse hello Azure DNS .NET SDK, you need tooinstall hello **Azure DNS Management Library** NuGet package and other required Azure packages.</span></span>

1. <span data-ttu-id="85f2d-119">En **Visual Studio**, abra un proyecto o cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="85f2d-119">In **Visual Studio**, open a project or new project.</span></span>
2. <span data-ttu-id="85f2d-120">Vaya demasiado**herramientas**  **>**  **Administrador de paquetes de NuGet**  **>**  **administrar paquetes de NuGet para Solución...** .</span><span class="sxs-lookup"><span data-stu-id="85f2d-120">Go too**Tools** **>** **NuGet Package Manager** **>** **Manage NuGet Packages for Solution...**.</span></span>
3. <span data-ttu-id="85f2d-121">Haga clic en **examinar**, habilitar hello **versión preliminar de inclusión** casilla de verificación y el tipo de **Microsoft.Azure.Management.Dns** en el cuadro de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="85f2d-121">Click **Browse**, enable hello **Include prerelease** checkbox, and type **Microsoft.Azure.Management.Dns** in hello search box.</span></span>
4. <span data-ttu-id="85f2d-122">Seleccione el paquete de Hola y haga clic en **instalar** tooadd, proyecto de Visual Studio tooyour.</span><span class="sxs-lookup"><span data-stu-id="85f2d-122">Select hello package and click **Install** tooadd it tooyour Visual Studio project.</span></span>
5. <span data-ttu-id="85f2d-123">Repetir proceso Hola anteriormente tooalso instalación Hola siguientes paquetes: **Microsoft.Rest.ClientRuntime.Azure.Authentication** y **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="85f2d-123">Repeat hello process above tooalso install hello following packages: **Microsoft.Rest.ClientRuntime.Azure.Authentication** and **Microsoft.Azure.Management.ResourceManager**.</span></span>

## <a name="add-namespace-declarations"></a><span data-ttu-id="85f2d-124">Incorporación de declaraciones de espacio de nombres</span><span class="sxs-lookup"><span data-stu-id="85f2d-124">Add namespace declarations</span></span>

<span data-ttu-id="85f2d-125">Agregar Hola siguientes declaraciones de espacio de nombres</span><span class="sxs-lookup"><span data-stu-id="85f2d-125">Add hello following namespace declarations</span></span>

```cs
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
```

## <a name="initialize-hello-dns-management-client"></a><span data-ttu-id="85f2d-126">Inicializar el cliente de administración de DNS de Hola</span><span class="sxs-lookup"><span data-stu-id="85f2d-126">Initialize hello DNS management client</span></span>

<span data-ttu-id="85f2d-127">Hola *DnsManagementClient* contiene métodos de Hola y propiedades necesarios para administrar zonas DNS y los conjuntos de registros.</span><span class="sxs-lookup"><span data-stu-id="85f2d-127">hello *DnsManagementClient* contains hello methods and properties necessary for managing DNS zones and recordsets.</span></span>  <span data-ttu-id="85f2d-128">Hola código siguiente registra en la cuenta de entidad de servicio toohello y crea un objeto DnsManagementClient.</span><span class="sxs-lookup"><span data-stu-id="85f2d-128">hello following code logs in toohello service principal account and creates a DnsManagementClient object.</span></span>

```cs
// Build hello service credentials and DNS management client
var serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
var dnsClient = new DnsManagementClient(serviceCreds);
dnsClient.SubscriptionId = subscriptionId;
```

## <a name="create-or-update-a-dns-zone"></a><span data-ttu-id="85f2d-129">Creación o actualización de una zona DNS</span><span class="sxs-lookup"><span data-stu-id="85f2d-129">Create or update a DNS zone</span></span>

<span data-ttu-id="85f2d-130">toocreate una zona DNS, en primer lugar "de zona" se crea un objeto los parámetros de zona DNS de toocontain Hola.</span><span class="sxs-lookup"><span data-stu-id="85f2d-130">toocreate a DNS zone, first a "Zone" object is created toocontain hello DNS zone parameters.</span></span> <span data-ttu-id="85f2d-131">Dado que las zonas DNS no son región específica tooa vinculado, ubicación de Hola se establece too'global'.</span><span class="sxs-lookup"><span data-stu-id="85f2d-131">Because DNS zones are not linked tooa specific region, hello location is set too'global'.</span></span> <span data-ttu-id="85f2d-132">En este ejemplo, un [Azure Resource Manager 'etiqueta'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) también se agrega la zona toohello.</span><span class="sxs-lookup"><span data-stu-id="85f2d-132">In this example, an [Azure Resource Manager 'tag'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) is also added toohello zone.</span></span>

<span data-ttu-id="85f2d-133">tooactually crear o actualizar la zona de DNS de Azure, objeto de la zona de Hola que contiene los parámetros de la zona de Hola Hola se pasa toohello *DnsManagementClient.Zones.CreateOrUpdateAsyc* método.</span><span class="sxs-lookup"><span data-stu-id="85f2d-133">tooactually create or update hello zone in Azure DNS, hello zone object containing hello zone parameters is passed toohello *DnsManagementClient.Zones.CreateOrUpdateAsyc* method.</span></span>

> [!NOTE]
> <span data-ttu-id="85f2d-134">DnsManagementClient admite tres modos de funcionamiento: sincrónica ('CreateOrUpdate'), asincrónica ('CreateOrUpdateAsync'), o asincrónico con la respuesta de acceso toohello HTTP ('CreateOrUpdateWithHttpMessagesAsync').</span><span class="sxs-lookup"><span data-stu-id="85f2d-134">DnsManagementClient supports three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access toohello HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span></span>  <span data-ttu-id="85f2d-135">Puede elegir cualquiera de estos modos, dependiendo de sus necesidades de aplicación.</span><span class="sxs-lookup"><span data-stu-id="85f2d-135">You can choose any of these modes, depending on your application needs.</span></span>

<span data-ttu-id="85f2d-136">DNS de Azure admite la simultaneidad optimista denominada [Etags](dns-getstarted-create-dnszone.md).</span><span class="sxs-lookup"><span data-stu-id="85f2d-136">Azure DNS supports optimistic concurrency, called [Etags](dns-getstarted-create-dnszone.md).</span></span> <span data-ttu-id="85f2d-137">En este ejemplo, especifica "*" para el encabezado de hello 'If-None-Match' indica toocreate DNS de Azure una zona DNS si no existe.</span><span class="sxs-lookup"><span data-stu-id="85f2d-137">In this example, specifying "*" for hello 'If-None-Match' header tells Azure DNS toocreate a DNS zone if one does not already exist.</span></span>  <span data-ttu-id="85f2d-138">se produce un error en la llamada de Hello si ya existe una zona con el nombre especificado de Hola Hola dado el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="85f2d-138">hello call fails if a zone with hello given name already exists in hello given resource group.</span></span>

```cs
// Create zone parameters
var dnsZoneParams = new Zone("global"); // All DNS zones must have location = "global"

// Create a Azure Resource Manager 'tag'.  This is optional.  You can add multiple tags
dnsZoneParams.Tags = new Dictionary<string, string>();
dnsZoneParams.Tags.Add("dept", "finance");

// Create hello actual zone.
// Note: Uses 'If-None-Match *' ETAG check, so will fail if hello zone exists already.
// Note: For non-async usage, call dnsClient.Zones.CreateOrUpdate(resourceGroupName, zoneName, dnsZoneParams, null, "*")
// Note: For getting hello http response, call dnsClient.Zones.CreateOrUpdateWithHttpMessagesAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*")
var dnsZone = await dnsClient.Zones.CreateOrUpdateAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*");
```

## <a name="create-dns-record-sets-and-records"></a><span data-ttu-id="85f2d-139">Creación de registros y conjuntos de registros de DNS</span><span class="sxs-lookup"><span data-stu-id="85f2d-139">Create DNS record sets and records</span></span>

<span data-ttu-id="85f2d-140">Los registros DNS se administran como un conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="85f2d-140">DNS records are managed as a record set.</span></span> <span data-ttu-id="85f2d-141">Un conjunto de registros es un conjunto de registros con hello mismo nombre y grabar tipo dentro de una zona.</span><span class="sxs-lookup"><span data-stu-id="85f2d-141">A record set is a set of records with hello same name and record type within a zone.</span></span>  <span data-ttu-id="85f2d-142">nombre de conjunto de registros de Hello es el nombre de la zona de toohello relativa, no Hola nombre DNS completo.</span><span class="sxs-lookup"><span data-stu-id="85f2d-142">hello record set name is relative toohello zone name, not hello fully qualified DNS name.</span></span>

<span data-ttu-id="85f2d-143">toocreate o actualización de un conjunto de registros, se crea un objeto de parámetros de "Conjunto de registros" y se pasan demasiado*DnsManagementClient.RecordSets.CreateOrUpdateAsync*.</span><span class="sxs-lookup"><span data-stu-id="85f2d-143">toocreate or update a record set, a "RecordSet" parameters object is created and passed too*DnsManagementClient.RecordSets.CreateOrUpdateAsync*.</span></span> <span data-ttu-id="85f2d-144">Como con las zonas DNS, hay tres modos de operación: sincrónica ('CreateOrUpdate'), asincrónica ('CreateOrUpdateAsync'), o asincrónico con la respuesta de acceso toohello HTTP ('CreateOrUpdateWithHttpMessagesAsync').</span><span class="sxs-lookup"><span data-stu-id="85f2d-144">As with DNS zones, there are three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access toohello HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span></span>

<span data-ttu-id="85f2d-145">Al igual que con las zonas DNS, las operaciones en los conjuntos de registros incluyen compatibilidad con la simultaneidad optimista.</span><span class="sxs-lookup"><span data-stu-id="85f2d-145">As with DNS zones, operations on record sets include support for optimistic concurrency.</span></span>  <span data-ttu-id="85f2d-146">En este ejemplo, puesto que se especifica 'If-Match' ni 'If-None-Match', conjunto de registros de hello siempre se crea.</span><span class="sxs-lookup"><span data-stu-id="85f2d-146">In this example, since neither 'If-Match' nor 'If-None-Match' are specified, hello record set is always created.</span></span>  <span data-ttu-id="85f2d-147">Esta llamada sobrescribe cualquier registro existente establecido con hello mismo nombre y registre el tipo de esta zona DNS.</span><span class="sxs-lookup"><span data-stu-id="85f2d-147">This call overwrites any existing record set with hello same name and record type in this DNS zone.</span></span>

```cs
// Create record set parameters
var recordSetParams = new RecordSet();
recordSetParams.TTL = 3600;

// Add records toohello record set parameter object.  In this case, we'll add a record of type 'A'
recordSetParams.ARecords = new List<ARecord>();
recordSetParams.ARecords.Add(new ARecord("1.2.3.4"));

// Add metadata toohello record set.  Similar tooAzure Resource Manager tags, this is optional and you can add multiple metadata name/value pairs
recordSetParams.Metadata = new Dictionary<string, string>();
recordSetParams.Metadata.Add("user", "Mary");

// Create hello actual record set in Azure DNS
// Note: no ETAG checks specified, will overwrite existing record set if one exists
var recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSetParams);
```

## <a name="get-zones-and-record-sets"></a><span data-ttu-id="85f2d-148">Obtención de zonas y conjuntos de registros</span><span class="sxs-lookup"><span data-stu-id="85f2d-148">Get zones and record sets</span></span>

<span data-ttu-id="85f2d-149">Hola *DnsManagementClient.Zones.Get* y *DnsManagementClient.RecordSets.Get* métodos recuperan zonas individuales y conjuntos de registros, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="85f2d-149">hello *DnsManagementClient.Zones.Get* and *DnsManagementClient.RecordSets.Get* methods retrieve individual zones and record sets, respectively.</span></span> <span data-ttu-id="85f2d-150">Conjuntos de registros se identifican por su tipo, el nombre y el grupo de recursos y la zona de hello existen en.</span><span class="sxs-lookup"><span data-stu-id="85f2d-150">RecordSets are identified by their type, name, and hello zone and resource group they exist in.</span></span> <span data-ttu-id="85f2d-151">Las zonas se identifican por su grupo de recursos de hello y el nombre que se encuentran en.</span><span class="sxs-lookup"><span data-stu-id="85f2d-151">Zones are identified by their name and hello resource group they exist in.</span></span>

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);
```

## <a name="update-an-existing-record-set"></a><span data-ttu-id="85f2d-152">Actualización de un conjunto de registros existente</span><span class="sxs-lookup"><span data-stu-id="85f2d-152">Update an existing record set</span></span>

<span data-ttu-id="85f2d-153">conjunto de tooupdate un registro DNS existente, recuperar primero el conjunto de registros de hello, a continuación, actualizar registro de hello el contenido del conjunto, a continuación, envíe el cambio de Hola.</span><span class="sxs-lookup"><span data-stu-id="85f2d-153">tooupdate an existing DNS record set, first retrieve hello record set, then update hello record set contents, then submit hello change.</span></span>  <span data-ttu-id="85f2d-154">En este ejemplo, especificamos Hola "Etag" de hello recupera el conjunto de registros de parámetro de 'If-Match' hello.</span><span class="sxs-lookup"><span data-stu-id="85f2d-154">In this example, we specify hello 'Etag' from hello retrieved record set in hello 'If-Match' parameter.</span></span> <span data-ttu-id="85f2d-155">se produce un error en la llamada de Hello si una operación simultánea modificó Hola conjunto de registros de hello mientras tanto.</span><span class="sxs-lookup"><span data-stu-id="85f2d-155">hello call fails if a concurrent operation has modified hello record set in hello meantime.</span></span>

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);

// Add a new record toohello local object.  Note that records in a record set must be unique/distinct
recordSet.ARecords.Add(new ARecord("5.6.7.8"));

// Update hello record set in Azure DNS
// Note: ETAG check specified, update will be rejected if hello record set has changed in hello meantime
recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSet, recordSet.Etag);
```

## <a name="list-zones-and-record-sets"></a><span data-ttu-id="85f2d-156">Enumeración de zonas y conjuntos de registros</span><span class="sxs-lookup"><span data-stu-id="85f2d-156">List zones and record sets</span></span>

<span data-ttu-id="85f2d-157">zonas de toolist, usar hello *DnsManagementClient.Zones.List...*  utilizan métodos, que admiten enumerar a todas las zonas de un determinado grupo de recursos o todas las zonas de conjuntos de registros de una toolist determinada suscripción de Azure (a través de grupos de recursos.), *DnsManagementClient.RecordSets.List...*  métodos, que son compatibles con enumerar todos los conjuntos de registros en una zona determinada o solo los conjuntos de registros de un tipo específico.</span><span class="sxs-lookup"><span data-stu-id="85f2d-157">toolist zones, use hello *DnsManagementClient.Zones.List...* methods, which support listing either all zones in a given resource group or all zones in a given Azure subscription (across resource groups.) toolist record sets, use *DnsManagementClient.RecordSets.List...* methods, which support either listing all record sets in a given zone or only those record sets of a specific type.</span></span>

<span data-ttu-id="85f2d-158">Al mostrar zonas y conjuntos de registros, tenga en cuenta que los resultados pueden estar paginados.</span><span class="sxs-lookup"><span data-stu-id="85f2d-158">Note when listing zones and record sets that results may be paginated.</span></span>  <span data-ttu-id="85f2d-159">Hola siguiente ejemplo se muestra cómo tooiterate a través de páginas de Hola de resultados.</span><span class="sxs-lookup"><span data-stu-id="85f2d-159">hello following example shows how tooiterate through hello pages of results.</span></span> <span data-ttu-id="85f2d-160">(Un tamaño de página artificialmente pequeño de '2' es tooforce usado paginación; en la práctica este parámetro, se debe omitir y Hola tamaño de página predeterminado utilizado).</span><span class="sxs-lookup"><span data-stu-id="85f2d-160">(An artificially small page size of '2' is used tooforce paging; in practice this parameter should be omitted and hello default page size used.)</span></span>

```cs
// Note: in this demo, we'll use a very small page size (2 record sets) toodemonstrate paging
// In practice, tooimprove performance you would use a large page size or just use hello system default
int recordSets = 0;
var page = await dnsClient.RecordSets.ListAllInResourceGroupAsync(resourceGroupName, zoneName, "2");
recordSets += page.Count();

while (page.NextPageLink != null)
{
    page = await dnsClient.RecordSets.ListAllInResourceGroupNextAsync(page.NextPageLink);
    recordSets += page.Count();
}
```

## <a name="next-steps"></a><span data-ttu-id="85f2d-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="85f2d-161">Next steps</span></span>

<span data-ttu-id="85f2d-162">Descargar hello [proyecto de ejemplo de SDK de .NET de DNS de Azure](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), que incluyen más ejemplos de cómo toouse Hola SDK de .NET de DNS de Azure, incluidos ejemplos para otros tipos de registro de DNS.</span><span class="sxs-lookup"><span data-stu-id="85f2d-162">Download hello [Azure DNS .NET SDK sample project](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), which includes further examples of how toouse hello Azure DNS .NET SDK, including examples for other DNS record types.</span></span>
