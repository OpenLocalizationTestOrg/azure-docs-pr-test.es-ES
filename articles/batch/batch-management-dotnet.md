---
title: recursos de la cuenta aaaManage por lotes con la biblioteca de cliente de Hola para .NET - Azure | Documentos de Microsoft
description: "Crear, eliminar y modificar recursos de la cuenta de lote de Azure con la biblioteca de .NET de administración de lotes de Hola."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 16279b23-60ff-4b16-b308-5de000e4c028
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/24/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 638d8129f3841ffcfb2e10f5d531a319bcbb7701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-accounts-and-quotas-with-hello-batch-management-client-library-for-net"></a><span data-ttu-id="42705-103">Administrar las cuentas de lote y las cuotas con la biblioteca de cliente de administración de lotes de Hola para .NET</span><span class="sxs-lookup"><span data-stu-id="42705-103">Manage Batch accounts and quotas with hello Batch Management client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="42705-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="42705-104">Azure portal</span></span>](batch-account-create-portal.md)
> * [<span data-ttu-id="42705-105">NET de Administración de Lote</span><span class="sxs-lookup"><span data-stu-id="42705-105">Batch Management .NET</span></span>](batch-management-dotnet.md)
> 
> 

<span data-ttu-id="42705-106">Sólo puede bajar mantenimiento sobrecarga en las aplicaciones de Azure Batch mediante el uso de hello [.NET de administración de lotes] [ api_mgmt_net] creación de la cuenta de lote de biblioteca tooautomate, eliminación, administración de claves y detección de cuota.</span><span class="sxs-lookup"><span data-stu-id="42705-106">You can lower maintenance overhead in your Azure Batch applications by using hello [Batch Management .NET][api_mgmt_net] library tooautomate Batch account creation, deletion, key management, and quota discovery.</span></span>

* <span data-ttu-id="42705-107">**Cree y elimine cuentas de Lote** en cualquier región.</span><span class="sxs-lookup"><span data-stu-id="42705-107">**Create and delete Batch accounts** within any region.</span></span> <span data-ttu-id="42705-108">Si, por ejemplo, como un proveedor de software independiente (ISV) proporciona un servicio para los clientes en la que cada una se asigna una cuenta de lote independiente para la facturación, puede agregar cuenta creación y eliminación capacidades tooyour portal del cliente.</span><span class="sxs-lookup"><span data-stu-id="42705-108">If, as an independent software vendor (ISV) for example, you provide a service for your clients in which each is assigned a separate Batch account for billing purposes, you can add account creation and deletion capabilities tooyour customer portal.</span></span>
* <span data-ttu-id="42705-109">**Recupere y regenere claves de la cuenta** mediante programación para cualquiera de sus cuentas de Lote.</span><span class="sxs-lookup"><span data-stu-id="42705-109">**Retrieve and regenerate account keys** programmatically for any of your Batch accounts.</span></span> <span data-ttu-id="42705-110">Esto puede ayudarle a cumplir las directivas de seguridad que exigen la sustitución periódica de las claves de cuenta.</span><span class="sxs-lookup"><span data-stu-id="42705-110">This can help you comply with security policies that enforce periodic rollover or expiry of account keys.</span></span> <span data-ttu-id="42705-111">Si tiene varias cuentas de Batch en distintas regiones de Azure, la automatización de este proceso de sustitución mejorará la eficacia de la solución.</span><span class="sxs-lookup"><span data-stu-id="42705-111">When you have several Batch accounts in various Azure regions, automation of this rollover process increases your solution's efficiency.</span></span>
* <span data-ttu-id="42705-112">**Compruebe las cuotas de la cuenta** y eliminan ensayo y error de hello conjeturas determinar qué cuentas de lote tienen los límites.</span><span class="sxs-lookup"><span data-stu-id="42705-112">**Check account quotas** and take hello trial-and-error guesswork out of determining which Batch accounts have what limits.</span></span> <span data-ttu-id="42705-113">Si comprueba las cuotas de las cuentas antes de iniciar un trabajo, crear un grupo o agregar un nodo de procesos, podrá ajustar de forma proactiva el lugar y el momento en que se crean estos recursos de proceso.</span><span class="sxs-lookup"><span data-stu-id="42705-113">By checking your account quotas before starting jobs, creating pools, or adding compute nodes, you can proactively adjust where or when these compute resources are created.</span></span> <span data-ttu-id="42705-114">Puede determinar qué cuentas requieren un aumento de la cuota antes de asignarles recursos adicionales.</span><span class="sxs-lookup"><span data-stu-id="42705-114">You can determine which accounts require quota increases before allocating additional resources in those accounts.</span></span>
* <span data-ttu-id="42705-115">**Combinar las características de otros servicios de Azure** para una experiencia de administración completa--mediante el uso de .NET de administración de lotes, [Azure Active Directory][aad_about], hello y [Azure El Administrador de recursos] [ resman_overview] en hello misma aplicación.</span><span class="sxs-lookup"><span data-stu-id="42705-115">**Combine features of other Azure services** for a full-featured management experience--by using Batch Management .NET, [Azure Active Directory][aad_about], and hello [Azure Resource Manager][resman_overview] together in hello same application.</span></span> <span data-ttu-id="42705-116">Mediante el uso de estas características y sus API, puede proporcionar una experiencia de autenticación sin dificultades, Hola toocreate de capacidad y eliminar grupos de recursos y las capacidades de hello descritas anteriormente para una solución de administración to-end.</span><span class="sxs-lookup"><span data-stu-id="42705-116">By using these features and their APIs, you can provide a frictionless authentication experience, hello ability toocreate and delete resource groups, and hello capabilities that are described above for an end-to-end management solution.</span></span>

> [!NOTE]
> <span data-ttu-id="42705-117">Aunque en este artículo se centra en la administración mediante programación de Hola de las cuentas, las claves y las cuotas de lote, puede realizar muchas de estas actividades mediante hello [portal de Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="42705-117">While this article focuses on hello programmatic management of your Batch accounts, keys, and quotas, you can perform many of these activities by using hello [Azure portal][azure_portal].</span></span> <span data-ttu-id="42705-118">Para obtener más información, consulte [crear una cuenta de lote de Azure mediante el portal de Azure de hello](batch-account-create-portal.md) y [las cuotas y límites de hello servicio Azure Batch](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="42705-118">For more information, see [Create an Azure Batch account using hello Azure portal](batch-account-create-portal.md) and [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span>
> 
> 

## <a name="create-and-delete-batch-accounts"></a><span data-ttu-id="42705-119">Cree y elimine cuentas de Lote</span><span class="sxs-lookup"><span data-stu-id="42705-119">Create and delete Batch accounts</span></span>
<span data-ttu-id="42705-120">Como se mencionó, una de las principales características de Hola de hello API de administración de lote es toocreate y eliminar cuentas de lote en una región de Azure.</span><span class="sxs-lookup"><span data-stu-id="42705-120">As mentioned, one of hello primary features of hello Batch Management API is toocreate and delete Batch accounts in an Azure region.</span></span> <span data-ttu-id="42705-121">por lo tanto, use toodo [BatchManagementClient.Account.CreateAsync] [ net_create] y [DeleteAsync][net_delete], o en sus equivalentes sincrónicos.</span><span class="sxs-lookup"><span data-stu-id="42705-121">toodo so, use [BatchManagementClient.Account.CreateAsync][net_create] and [DeleteAsync][net_delete], or their synchronous counterparts.</span></span>

<span data-ttu-id="42705-122">Hello fragmento de código siguiente crea una cuenta, obtiene Hola recién creado cuenta de hello servicio por lotes y, a continuación, lo elimina.</span><span class="sxs-lookup"><span data-stu-id="42705-122">hello following code snippet creates an account, obtains hello newly created account from hello Batch service, and then deletes it.</span></span> <span data-ttu-id="42705-123">En este fragmento de código y otros Hola en este artículo, `batchManagementClient` es una instancia totalmente inicializada de [BatchManagementClient][net_mgmt_client].</span><span class="sxs-lookup"><span data-stu-id="42705-123">In this snippet and hello others in this article, `batchManagementClient` is a fully initialized instance of [BatchManagementClient][net_mgmt_client].</span></span>

```csharp
// Create a new Batch account
await batchManagementClient.Account.CreateAsync("MyResourceGroup",
    "mynewaccount",
    new BatchAccountCreateParameters() { Location = "West US" });

// Get hello new account from hello Batch service
AccountResource account = await batchManagementClient.Account.GetAsync(
    "MyResourceGroup",
    "mynewaccount");

// Delete hello account
await batchManagementClient.Account.DeleteAsync("MyResourceGroup", account.Name);
```

> [!NOTE]
> <span data-ttu-id="42705-124">Aplicaciones que utilizan la biblioteca de .NET de administración de lotes de Hola y su clase BatchManagementClient requieren **Administrador de servicios** o **coadministrator** acceder a suscripción toohello que posee Hola Cuenta de lote toobe administrado.</span><span class="sxs-lookup"><span data-stu-id="42705-124">Applications that use hello Batch Management .NET library and its BatchManagementClient class require **service administrator** or **coadministrator** access toohello subscription that owns hello Batch account toobe managed.</span></span> <span data-ttu-id="42705-125">Para obtener más información, vea hello [Azure Active Directory](#azure-active-directory) hello y sección [AccountManagement] [ acct_mgmt_sample] ejemplo de código.</span><span class="sxs-lookup"><span data-stu-id="42705-125">For more information, see hello [Azure Active Directory](#azure-active-directory) section and hello [AccountManagement][acct_mgmt_sample] code sample.</span></span>
> 
> 

## <a name="retrieve-and-regenerate-account-keys"></a><span data-ttu-id="42705-126">Recupere y regenere claves de la cuenta</span><span class="sxs-lookup"><span data-stu-id="42705-126">Retrieve and regenerate account keys</span></span>
<span data-ttu-id="42705-127">Obtenga las claves de las cuentas principal y secundaria de cualquier cuenta de Batch de su suscripción con [ListKeysAsync][net_list_keys].</span><span class="sxs-lookup"><span data-stu-id="42705-127">Obtain primary and secondary account keys from any Batch account within your subscription by using [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="42705-128">Dichas claves se pueden regenerar con [RegenerateKeyAsync][net_regenerate_keys].</span><span class="sxs-lookup"><span data-stu-id="42705-128">You can regenerate those keys by using [RegenerateKeyAsync][net_regenerate_keys].</span></span>

```csharp
// Get and print hello primary and secondary keys
BatchAccountListKeyResult accountKeys =
    await batchManagementClient.Account.ListKeysAsync(
        "MyResourceGroup",
        "mybatchaccount");
Console.WriteLine("Primary key:   {0}", accountKeys.Primary);
Console.WriteLine("Secondary key: {0}", accountKeys.Secondary);

// Regenerate hello primary key
BatchAccountRegenerateKeyResponse newKeys =
    await batchManagementClient.Account.RegenerateKeyAsync(
        "MyResourceGroup",
        "mybatchaccount",
        new BatchAccountRegenerateKeyParameters() {
            KeyName = AccountKeyType.Primary
            });
```

> [!TIP]
> <span data-ttu-id="42705-129">Puede crear un flujo de trabajo de conexión simplificada para las aplicaciones de administración.</span><span class="sxs-lookup"><span data-stu-id="42705-129">You can create a streamlined connection workflow for your management applications.</span></span> <span data-ttu-id="42705-130">En primer lugar, obtenga una clave de cuenta para la cuenta de lote de hello desea toomanage con [ListKeysAsync][net_list_keys].</span><span class="sxs-lookup"><span data-stu-id="42705-130">First, obtain an account key for hello Batch account you wish toomanage with [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="42705-131">A continuación, utilice esta clave al inicializar la biblioteca de .NET de lotes de hello [BatchSharedKeyCredentials] [ net_sharedkeycred] (clase), que se usa al inicializar [BatchClient] [net_batch_client].</span><span class="sxs-lookup"><span data-stu-id="42705-131">Then, use this key when initializing hello Batch .NET library's [BatchSharedKeyCredentials][net_sharedkeycred] class, which is used when initializing [BatchClient][net_batch_client].</span></span>
> 
> 

## <a name="check-azure-subscription-and-batch-account-quotas"></a><span data-ttu-id="42705-132">Comprobación de la suscripción de Azure y cuotas de la cuenta de Lote</span><span class="sxs-lookup"><span data-stu-id="42705-132">Check Azure subscription and Batch account quotas</span></span>
<span data-ttu-id="42705-133">Las suscripciones de Azure y Hola servicios individuales de Azure como procesar por lotes todas tienen cuotas predeterminadas que limitan el número de Hola de ciertas entidades dentro de ellos.</span><span class="sxs-lookup"><span data-stu-id="42705-133">Azure subscriptions and hello individual Azure services like Batch all have default quotas that limit hello number of certain entities within them.</span></span> <span data-ttu-id="42705-134">Para cuotas de hello predeterminadas para las suscripciones de Azure, consulte [suscripción de Azure y límites de servicio, cuotas y restricciones](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="42705-134">For hello default quotas for Azure subscriptions, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="42705-135">Para las cuotas predeterminadas de Hola de hello servicio por lotes, vea [las cuotas y límites de hello servicio Azure Batch](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="42705-135">For hello default quotas of hello Batch service, see [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span> <span data-ttu-id="42705-136">Mediante la biblioteca de .NET de administración de lotes de hello, puede comprobar estas cuotas en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="42705-136">By using hello Batch Management .NET library, you can check these quotas in your applications.</span></span> <span data-ttu-id="42705-137">Esto le permite tomar decisiones de asignación de toomake antes de agregar las cuentas o recursos como grupos de proceso y nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="42705-137">This enables you toomake allocation decisions before you add accounts or compute resources like pools and compute nodes.</span></span>

### <a name="check-an-azure-subscription-for-batch-account-quotas"></a><span data-ttu-id="42705-138">Comprobación de una suscripción de Azure para las cuotas de cuentas de Lote</span><span class="sxs-lookup"><span data-stu-id="42705-138">Check an Azure subscription for Batch account quotas</span></span>
<span data-ttu-id="42705-139">Antes de crear una cuenta de lote en una región, puede comprobar su suscripción de Azure toosee tanto si es capaz de tooadd una cuenta en dicha región.</span><span class="sxs-lookup"><span data-stu-id="42705-139">Before creating a Batch account in a region, you can check your Azure subscription toosee whether you are able tooadd an account in that region.</span></span>

<span data-ttu-id="42705-140">En el fragmento de código de hello a continuación, se utiliza primero [BatchManagementClient.Account.ListAsync] [ net_mgmt_listaccounts] tooget una colección de todas las cuentas de proceso por lotes que están dentro de una suscripción.</span><span class="sxs-lookup"><span data-stu-id="42705-140">In hello code snippet below, we first use [BatchManagementClient.Account.ListAsync][net_mgmt_listaccounts] tooget a collection of all Batch accounts that are within a subscription.</span></span> <span data-ttu-id="42705-141">Una vez que hemos obtenido esta colección, se determina cuántas cuentas están en la región de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="42705-141">Once we've obtained this collection, we determine how many accounts are in hello target region.</span></span> <span data-ttu-id="42705-142">A continuación, usamos [BatchManagementClient.Subscriptions] [ net_mgmt_subscriptions] tooobtain Hola cuota de la cuenta de lote y determinar el número de cuentas (si existe) se puede crear en dicha región.</span><span class="sxs-lookup"><span data-stu-id="42705-142">Then we use [BatchManagementClient.Subscriptions][net_mgmt_subscriptions] tooobtain hello Batch account quota and determine how many accounts (if any) can be created in that region.</span></span>

```csharp
// Get a collection of all Batch accounts within hello subscription
BatchAccountListResponse listResponse =
        await batchManagementClient.Account.ListAsync(new AccountListParameters());
IList<AccountResource> accounts = listResponse.Accounts;
Console.WriteLine("Total number of Batch accounts under subscription id {0}:  {1}",
    creds.SubscriptionId,
    accounts.Count);

// Get a count of all accounts within hello target region
string region = "westus";
int accountsInRegion = accounts.Count(o => o.Location == region);

// Get hello account quota for hello specified region
SubscriptionQuotasGetResponse quotaResponse = await batchManagementClient.Subscriptions.GetSubscriptionQuotasAsync(region);
Console.WriteLine("Account quota for {0} region: {1}", region, quotaResponse.AccountQuota);

// Determine how many accounts can be created in hello target region
Console.WriteLine("Accounts in {0}: {1}", region, accountsInRegion);
Console.WriteLine("You can create {0} accounts in hello {1} region.", quotaResponse.AccountQuota - accountsInRegion, region);
```

<span data-ttu-id="42705-143">En el fragmento de código de hello anterior, `creds` es una instancia de [TokenCloudCredentials][azure_tokencreds].</span><span class="sxs-lookup"><span data-stu-id="42705-143">In hello snippet above, `creds` is an instance of [TokenCloudCredentials][azure_tokencreds].</span></span> <span data-ttu-id="42705-144">toosee muestra un ejemplo de creación de este objeto, vea hello [AccountManagement] [ acct_mgmt_sample] ejemplo de código en GitHub.</span><span class="sxs-lookup"><span data-stu-id="42705-144">toosee an example of creating this object, see hello [AccountManagement][acct_mgmt_sample] code sample on GitHub.</span></span>

### <a name="check-a-batch-account-for-compute-resource-quotas"></a><span data-ttu-id="42705-145">Comprobación de una cuenta de Lote para las cuotas de recursos de proceso</span><span class="sxs-lookup"><span data-stu-id="42705-145">Check a Batch account for compute resource quotas</span></span>
<span data-ttu-id="42705-146">Antes de aumentar los recursos de proceso en la solución de lote, puede comprobar los recursos de hello tooensure desea tooallocate no superan las cuotas de la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="42705-146">Before increasing compute resources in your Batch solution, you can check tooensure hello resources you want tooallocate won't exceed hello account's quotas.</span></span> <span data-ttu-id="42705-147">En el fragmento de código de hello a continuación, imprimir información de cuota de Hola para hello con el nombre de cuenta de lote `mybatchaccount`.</span><span class="sxs-lookup"><span data-stu-id="42705-147">In hello code snippet below, we print hello quota information for hello Batch account named `mybatchaccount`.</span></span> <span data-ttu-id="42705-148">En su propia aplicación, podría utilizar este tipo toodetermine información si puede gestionar cuenta de Hola Hola recursos adicionales toobe creado.</span><span class="sxs-lookup"><span data-stu-id="42705-148">In your own application, you could use such information toodetermine whether hello account can handle hello additional resources toobe created.</span></span>

```csharp
// First obtain hello Batch account
BatchAccountGetResponse getResponse =
    await batchManagementClient.Account.GetAsync("MyResourceGroup", "mybatchaccount");
AccountResource account = getResponse.Resource;

// Now print hello compute resource quotas for hello account
Console.WriteLine("Core quota: {0}", account.Properties.CoreQuota);
Console.WriteLine("Pool quota: {0}", account.Properties.PoolQuota);
Console.WriteLine("Active job and job schedule quota: {0}", account.Properties.ActiveJobAndJobScheduleQuota);
```

> [!IMPORTANT]
> <span data-ttu-id="42705-149">Aunque hay cuotas predeterminadas para los servicios y las suscripciones de Azure, muchos de estos límites pueden generarse mediante la emisión de una solicitud en hello [portal de Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="42705-149">While there are default quotas for Azure subscriptions and services, many of these limits can be raised by issuing a request in hello [Azure portal][azure_portal].</span></span> <span data-ttu-id="42705-150">Por ejemplo, vea [las cuotas y límites de hello servicio Azure Batch](batch-quota-limit.md) para obtener instrucciones acerca de cómo aumentar las cuotas de la cuenta de lote.</span><span class="sxs-lookup"><span data-stu-id="42705-150">For example, see [Quotas and limits for hello Azure Batch service](batch-quota-limit.md) for instructions on increasing your Batch account quotas.</span></span>
> 
> 

## <a name="use-azure-ad-with-batch-management-net"></a><span data-ttu-id="42705-151">Uso de Azure AD con .NET de administración de Batch</span><span class="sxs-lookup"><span data-stu-id="42705-151">Use Azure AD with Batch Management .NET</span></span>

<span data-ttu-id="42705-152">biblioteca de .NET de administración de lotes de Hello es un cliente de proveedor de recursos de Azure y se utiliza junto con [Azure Resource Manager] [ resman_overview] toomanage cuenta de recursos mediante programación.</span><span class="sxs-lookup"><span data-stu-id="42705-152">hello Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] toomanage account resources programmatically.</span></span> <span data-ttu-id="42705-153">Azure AD es las solicitudes de tooauthenticate necesario realizadas a través de cualquier cliente de proveedor de recursos de Azure, incluidos la biblioteca de .NET de administración de lotes de hello y [Azure Resource Manager][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="42705-153">Azure AD is required tooauthenticate requests made through any Azure resource provider client, including hello Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span> <span data-ttu-id="42705-154">Para obtener información acerca del uso de Azure AD con la biblioteca de .NET de administración de lotes de hello, consulte [soluciones de lote de uso de Azure Active Directory tooauthenticate](batch-aad-auth.md).</span><span class="sxs-lookup"><span data-stu-id="42705-154">For information about using Azure AD with hello Batch Management .NET library, see [Use Azure Active Directory tooauthenticate Batch solutions](batch-aad-auth.md).</span></span> 

## <a name="sample-project-on-github"></a><span data-ttu-id="42705-155">Proyecto de ejemplo en GitHub</span><span class="sxs-lookup"><span data-stu-id="42705-155">Sample project on GitHub</span></span>

<span data-ttu-id="42705-156">toosee .NET de administración de lotes de acción, consulte hello [AccountManagment] [ acct_mgmt_sample] proyecto de ejemplo en GitHub.</span><span class="sxs-lookup"><span data-stu-id="42705-156">toosee Batch Management .NET in action, check out hello [AccountManagment][acct_mgmt_sample] sample project on GitHub.</span></span> <span data-ttu-id="42705-157">Hola AccountManagment aplicación de ejemplo muestra hello las siguientes operaciones:</span><span class="sxs-lookup"><span data-stu-id="42705-157">hello AccountManagment sample application demonstrates hello following operations:</span></span>

1. <span data-ttu-id="42705-158">Adquiera un token de seguridad en Azure AD mediante [ADAL][aad_adal].</span><span class="sxs-lookup"><span data-stu-id="42705-158">Acquire a security token from Azure AD by using [ADAL][aad_adal].</span></span> <span data-ttu-id="42705-159">Si el usuario de hello no ha iniciado ya sesión, se piden sus credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="42705-159">If hello user is not already signed in, they are prompted for their Azure credentials.</span></span>
2. <span data-ttu-id="42705-160">Con el token de seguridad de hello obtenido de Azure AD, crear un [SubscriptionClient] [ resman_subclient] tooquery Azure para obtener una lista de las suscripciones asociadas a la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="42705-160">With hello security token obtained from Azure AD, create a [SubscriptionClient][resman_subclient] tooquery Azure for a list of subscriptions associated with hello account.</span></span> <span data-ttu-id="42705-161">usuario de Hello puede seleccionar una suscripción de la lista de hello si contiene más de una suscripción.</span><span class="sxs-lookup"><span data-stu-id="42705-161">hello user can select a subscription from hello list if it contains more than one subscription.</span></span>
3. <span data-ttu-id="42705-162">Obtener las credenciales asociadas a la suscripción de hello seleccionado.</span><span class="sxs-lookup"><span data-stu-id="42705-162">Get credentials associated with hello selected subscription.</span></span>
4. <span data-ttu-id="42705-163">Crear un [ResourceManagementClient] [ resman_client] objeto mediante el uso de credenciales de Hola.</span><span class="sxs-lookup"><span data-stu-id="42705-163">Create a [ResourceManagementClient][resman_client] object by using hello credentials.</span></span>
5. <span data-ttu-id="42705-164">Use un [ResourceManagementClient] [ resman_client] toocreate un grupo de recursos de objeto.</span><span class="sxs-lookup"><span data-stu-id="42705-164">Use a [ResourceManagementClient][resman_client] object toocreate a resource group.</span></span>
6. <span data-ttu-id="42705-165">Use un [BatchManagementClient] [ net_mgmt_client] objeto tooperform varias operaciones de la cuenta de lote:</span><span class="sxs-lookup"><span data-stu-id="42705-165">Use a [BatchManagementClient][net_mgmt_client] object tooperform several Batch account operations:</span></span>
   * <span data-ttu-id="42705-166">Crear una cuenta de lote en el nuevo grupo de recursos Hola.</span><span class="sxs-lookup"><span data-stu-id="42705-166">Create a Batch account in hello new resource group.</span></span>
   * <span data-ttu-id="42705-167">Obtener Hola recién creado cuenta de hello servicio por lotes.</span><span class="sxs-lookup"><span data-stu-id="42705-167">Get hello newly created account from hello Batch service.</span></span>
   * <span data-ttu-id="42705-168">Imprimir claves de cuenta de hello para la nueva cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="42705-168">Print hello account keys for hello new account.</span></span>
   * <span data-ttu-id="42705-169">Volver a generar una nueva clave principal para la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="42705-169">Regenerate a new primary key for hello account.</span></span>
   * <span data-ttu-id="42705-170">Imprimir la información de cuota de hello para la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="42705-170">Print hello quota information for hello account.</span></span>
   * <span data-ttu-id="42705-171">Imprimir la información de cuota de hello para la suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="42705-171">Print hello quota information for hello subscription.</span></span>
   * <span data-ttu-id="42705-172">Imprimir todas las cuentas de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="42705-172">Print all accounts within hello subscription.</span></span>
   * <span data-ttu-id="42705-173">Eliminar la cuenta recién creada.</span><span class="sxs-lookup"><span data-stu-id="42705-173">Delete newly created account.</span></span>
7. <span data-ttu-id="42705-174">Elimine el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="42705-174">Delete hello resource group.</span></span>

<span data-ttu-id="42705-175">Antes de eliminar el grupo de cuentas y recursos de proceso por lotes de hello recién creado, puede verlos en hello [portal de Azure][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="42705-175">Before deleting hello newly created Batch account and resource group, you can view them in hello [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="42705-176">aplicación de ejemplo de Hola toorun correctamente, debe primero registrarlo con el inquilino de Azure AD en hello Azure portal y conceda permisos toohello API del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="42705-176">toorun hello sample application successfully, you must first register it with your Azure AD tenant in hello Azure portal and grant permissions toohello Azure Resource Manager API.</span></span> <span data-ttu-id="42705-177">Siga los pasos de hello proporcionados en [soluciones de administración de lote autenticarse con Active Directory](batch-aad-auth-management.md).</span><span class="sxs-lookup"><span data-stu-id="42705-177">Follow hello steps provided in [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span>


[aad_about]: ../active-directory/active-directory-whatis.md "¿Qué es Azure Active Directory?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Escenarios de autenticación para Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integración de aplicaciones con Azure Active Directory"
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_mgmt_net]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[azure_portal]: http://portal.azure.com
[azure_storage]: https://azure.microsoft.com/services/storage/
[azure_tokencreds]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.tokencloudcredentials.aspx
[batch_explorer_project]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[net_batch_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_list_keys]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.listkeysasync.aspx
[net_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.createasync.aspx
[net_delete]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.deleteasync.aspx
[net_regenerate_keys]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.regeneratekeyasync.aspx
[net_sharedkeycred]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.auth.batchsharedkeycredentials.aspx
[net_mgmt_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.batchmanagementclient.aspx
[net_mgmt_subscriptions]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.batchmanagementclient.subscriptions.aspx
[net_mgmt_listaccounts]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.iaccountoperations.listasync.aspx
[resman_api]: https://msdn.microsoft.com/library/azure/mt418626.aspx
[resman_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.resources.resourcemanagementclient.aspx
[resman_subclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.subscriptions.subscriptionclient.aspx
[resman_overview]: ../azure-resource-manager/resource-group-overview.md

[1]: ./media/batch-management-dotnet/portal-01.png
[2]: ./media/batch-management-dotnet/portal-02.png
[3]: ./media/batch-management-dotnet/portal-03.png
