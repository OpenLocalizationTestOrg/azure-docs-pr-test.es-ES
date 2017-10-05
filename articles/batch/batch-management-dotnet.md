---
title: "Administración de recursos de la cuenta de Batch con la biblioteca de cliente de .NET: Azure | Microsoft Docs"
description: Cree, elimine y modifique recursos de cuenta de Azure Batch con la biblioteca Batch Management .NET.
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
ms.openlocfilehash: eafde9258222a2ab09ade2e366f9cc595a303dec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-batch-accounts-and-quotas-with-the-batch-management-client-library-for-net"></a><span data-ttu-id="b8cfc-103">Administración de cuentas y cuotas de Batch con la biblioteca cliente de administración de Batch para .NET</span><span class="sxs-lookup"><span data-stu-id="b8cfc-103">Manage Batch accounts and quotas with the Batch Management client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b8cfc-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="b8cfc-104">Azure portal</span></span>](batch-account-create-portal.md)
> * [<span data-ttu-id="b8cfc-105">NET de Administración de Lote</span><span class="sxs-lookup"><span data-stu-id="b8cfc-105">Batch Management .NET</span></span>](batch-management-dotnet.md)
> 
> 

<span data-ttu-id="b8cfc-106">Puede reducir la sobrecarga de mantenimiento en las aplicaciones de Azure Batch con la biblioteca [Batch Management .NET][api_mgmt_net] para automatizar la creación, eliminación, administración de claves y detección de cuota de las cuentas de Batch.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-106">You can lower maintenance overhead in your Azure Batch applications by using the [Batch Management .NET][api_mgmt_net] library to automate Batch account creation, deletion, key management, and quota discovery.</span></span>

* <span data-ttu-id="b8cfc-107">**Cree y elimine cuentas de Lote** en cualquier región.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-107">**Create and delete Batch accounts** within any region.</span></span> <span data-ttu-id="b8cfc-108">Por ejemplo, si como proveedor de software independiente (ISV) proporciona un servicio a los clientes en el que a cada uno se le asigna una cuenta de Lote independiente para la facturación, puede agregar capacidades de creación y eliminación de la cuenta al portal del cliente.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-108">If, as an independent software vendor (ISV) for example, you provide a service for your clients in which each is assigned a separate Batch account for billing purposes, you can add account creation and deletion capabilities to your customer portal.</span></span>
* <span data-ttu-id="b8cfc-109">**Recupere y regenere claves de la cuenta** mediante programación para cualquiera de sus cuentas de Lote.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-109">**Retrieve and regenerate account keys** programmatically for any of your Batch accounts.</span></span> <span data-ttu-id="b8cfc-110">Esto puede ayudarle a cumplir las directivas de seguridad que exigen la sustitución periódica de las claves de cuenta.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-110">This can help you comply with security policies that enforce periodic rollover or expiry of account keys.</span></span> <span data-ttu-id="b8cfc-111">Si tiene varias cuentas de Batch en distintas regiones de Azure, la automatización de este proceso de sustitución mejorará la eficacia de la solución.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-111">When you have several Batch accounts in various Azure regions, automation of this rollover process increases your solution's efficiency.</span></span>
* <span data-ttu-id="b8cfc-112">**Compruebe las cuotas de la cuenta** y elimine las incertidumbres al determina los límites de cada cuenta de Lote.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-112">**Check account quotas** and take the trial-and-error guesswork out of determining which Batch accounts have what limits.</span></span> <span data-ttu-id="b8cfc-113">Si comprueba las cuotas de las cuentas antes de iniciar un trabajo, crear un grupo o agregar un nodo de procesos, podrá ajustar de forma proactiva el lugar y el momento en que se crean estos recursos de proceso.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-113">By checking your account quotas before starting jobs, creating pools, or adding compute nodes, you can proactively adjust where or when these compute resources are created.</span></span> <span data-ttu-id="b8cfc-114">Puede determinar qué cuentas requieren un aumento de la cuota antes de asignarles recursos adicionales.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-114">You can determine which accounts require quota increases before allocating additional resources in those accounts.</span></span>
* <span data-ttu-id="b8cfc-115">**Combine las características de otros servicios de Azure** para una experiencia completa de administración, para lo que debe sacar provecho a la vez de la biblioteca Batch Management .NET, [Azure Active Directory][aad_about] y [Azure Resource Manager][resman_overview] en la misma aplicación.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-115">**Combine features of other Azure services** for a full-featured management experience--by using Batch Management .NET, [Azure Active Directory][aad_about], and the [Azure Resource Manager][resman_overview] together in the same application.</span></span> <span data-ttu-id="b8cfc-116">Mediante el uso de estas características y sus API puede proporcionar una experiencia de autenticación sin fricciones, la capacidad para crear y eliminar grupos de recursos, y las funcionalidades que se han descrito anteriormente para una solución de administración de un extremo a otro.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-116">By using these features and their APIs, you can provide a frictionless authentication experience, the ability to create and delete resource groups, and the capabilities that are described above for an end-to-end management solution.</span></span>

> [!NOTE]
> <span data-ttu-id="b8cfc-117">Aunque este artículo se centra en la administración de sus cuentas de Batch, claves y cuotas mediante programación, puede realizar muchas de estas actividades con [Azure Portal][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="b8cfc-117">While this article focuses on the programmatic management of your Batch accounts, keys, and quotas, you can perform many of these activities by using the [Azure portal][azure_portal].</span></span> <span data-ttu-id="b8cfc-118">Para más información, consulte [Creación de una cuenta de Azure Batch con Azure Portal](batch-account-create-portal.md) y [Cuotas y límites del servicio Azure Batch](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="b8cfc-118">For more information, see [Create an Azure Batch account using the Azure portal](batch-account-create-portal.md) and [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span></span>
> 
> 

## <a name="create-and-delete-batch-accounts"></a><span data-ttu-id="b8cfc-119">Cree y elimine cuentas de Lote</span><span class="sxs-lookup"><span data-stu-id="b8cfc-119">Create and delete Batch accounts</span></span>
<span data-ttu-id="b8cfc-120">Tal y como se mencionó anteriormente, una de las principales características de Batch Management API es la creación y eliminación de cuentas de Batch en una región de Azure.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-120">As mentioned, one of the primary features of the Batch Management API is to create and delete Batch accounts in an Azure region.</span></span> <span data-ttu-id="b8cfc-121">Para ello, usará [BatchManagementClient.Account.CreateAsync][net_create] y [DeleteAsync][net_delete], o sus contrapartidas sincrónicas.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-121">To do so, use [BatchManagementClient.Account.CreateAsync][net_create] and [DeleteAsync][net_delete], or their synchronous counterparts.</span></span>

<span data-ttu-id="b8cfc-122">El fragmento de código siguiente crea una cuenta, obtiene la cuenta recién creada del servicio Lote y la elimina.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-122">The following code snippet creates an account, obtains the newly created account from the Batch service, and then deletes it.</span></span> <span data-ttu-id="b8cfc-123">En este y otros fragmentos de código que aparecen en el artículo, `batchManagementClient` es una instancia completamente inicializada de [BatchManagementClient][net_mgmt_client].</span><span class="sxs-lookup"><span data-stu-id="b8cfc-123">In this snippet and the others in this article, `batchManagementClient` is a fully initialized instance of [BatchManagementClient][net_mgmt_client].</span></span>

```csharp
// Create a new Batch account
await batchManagementClient.Account.CreateAsync("MyResourceGroup",
    "mynewaccount",
    new BatchAccountCreateParameters() { Location = "West US" });

// Get the new account from the Batch service
AccountResource account = await batchManagementClient.Account.GetAsync(
    "MyResourceGroup",
    "mynewaccount");

// Delete the account
await batchManagementClient.Account.DeleteAsync("MyResourceGroup", account.Name);
```

> [!NOTE]
> <span data-ttu-id="b8cfc-124">Las aplicaciones que utilizan la biblioteca Batch Management .NET y su clase BatchManagementClient necesitan tener acceso de **administrador de servicio** o **coadministrador** en la suscripción propietaria de la cuenta de Batch que se va a administrar.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-124">Applications that use the Batch Management .NET library and its BatchManagementClient class require **service administrator** or **coadministrator** access to the subscription that owns the Batch account to be managed.</span></span> <span data-ttu-id="b8cfc-125">Para más información, consulte la sección [Azure Active Directory](#azure-active-directory) a continuación y el código de ejemplo [AccountManagement][acct_mgmt_sample].</span><span class="sxs-lookup"><span data-stu-id="b8cfc-125">For more information, see the [Azure Active Directory](#azure-active-directory) section and the [AccountManagement][acct_mgmt_sample] code sample.</span></span>
> 
> 

## <a name="retrieve-and-regenerate-account-keys"></a><span data-ttu-id="b8cfc-126">Recupere y regenere claves de la cuenta</span><span class="sxs-lookup"><span data-stu-id="b8cfc-126">Retrieve and regenerate account keys</span></span>
<span data-ttu-id="b8cfc-127">Obtenga las claves de las cuentas principal y secundaria de cualquier cuenta de Batch de su suscripción con [ListKeysAsync][net_list_keys].</span><span class="sxs-lookup"><span data-stu-id="b8cfc-127">Obtain primary and secondary account keys from any Batch account within your subscription by using [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="b8cfc-128">Dichas claves se pueden regenerar con [RegenerateKeyAsync][net_regenerate_keys].</span><span class="sxs-lookup"><span data-stu-id="b8cfc-128">You can regenerate those keys by using [RegenerateKeyAsync][net_regenerate_keys].</span></span>

```csharp
// Get and print the primary and secondary keys
BatchAccountListKeyResult accountKeys =
    await batchManagementClient.Account.ListKeysAsync(
        "MyResourceGroup",
        "mybatchaccount");
Console.WriteLine("Primary key:   {0}", accountKeys.Primary);
Console.WriteLine("Secondary key: {0}", accountKeys.Secondary);

// Regenerate the primary key
BatchAccountRegenerateKeyResponse newKeys =
    await batchManagementClient.Account.RegenerateKeyAsync(
        "MyResourceGroup",
        "mybatchaccount",
        new BatchAccountRegenerateKeyParameters() {
            KeyName = AccountKeyType.Primary
            });
```

> [!TIP]
> <span data-ttu-id="b8cfc-129">Puede crear un flujo de trabajo de conexión simplificada para las aplicaciones de administración.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-129">You can create a streamlined connection workflow for your management applications.</span></span> <span data-ttu-id="b8cfc-130">En primer lugar, obtenga una clave de cuenta para la cuenta de Batch que desea administrar con [ListKeysAsync][net_list_keys].</span><span class="sxs-lookup"><span data-stu-id="b8cfc-130">First, obtain an account key for the Batch account you wish to manage with [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="b8cfc-131">Después, use esta clave al inicializar la clase [BatchSharedKeyCredentials][net_sharedkeycred] de la biblioteca de .NET de Batch, que se usa al inicializar [BatchClient][net_batch_client].</span><span class="sxs-lookup"><span data-stu-id="b8cfc-131">Then, use this key when initializing the Batch .NET library's [BatchSharedKeyCredentials][net_sharedkeycred] class, which is used when initializing [BatchClient][net_batch_client].</span></span>
> 
> 

## <a name="check-azure-subscription-and-batch-account-quotas"></a><span data-ttu-id="b8cfc-132">Comprobación de la suscripción de Azure y cuotas de la cuenta de Lote</span><span class="sxs-lookup"><span data-stu-id="b8cfc-132">Check Azure subscription and Batch account quotas</span></span>
<span data-ttu-id="b8cfc-133">Las suscripciones de Azure y los servicios individuales de Azure, como Lote, tienen cuotas predeterminadas que limitan el número de determinadas entidades que contienen.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-133">Azure subscriptions and the individual Azure services like Batch all have default quotas that limit the number of certain entities within them.</span></span> <span data-ttu-id="b8cfc-134">Para conocer las cuotas predeterminadas de las suscripciones de Azure, consulte [Límites, cuotas y restricciones de suscripción y servicios de Microsoft Azure](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="b8cfc-134">For the default quotas for Azure subscriptions, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="b8cfc-135">Para conocer las cuotas predeterminadas del servicio Lote, consulte [Cuotas y límites del servicio de Lote de Azure](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="b8cfc-135">For the default quotas of the Batch service, see [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span></span> <span data-ttu-id="b8cfc-136">Con la biblioteca Batch Management .NET, pude comprobar estas cuotas en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-136">By using the Batch Management .NET library, you can check these quotas in your applications.</span></span> <span data-ttu-id="b8cfc-137">Esto le permite tomar decisiones sobre la asignación antes de agregar cuentas o recursos de proceso como los grupos y nodos de ejecución.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-137">This enables you to make allocation decisions before you add accounts or compute resources like pools and compute nodes.</span></span>

### <a name="check-an-azure-subscription-for-batch-account-quotas"></a><span data-ttu-id="b8cfc-138">Comprobación de una suscripción de Azure para las cuotas de cuentas de Lote</span><span class="sxs-lookup"><span data-stu-id="b8cfc-138">Check an Azure subscription for Batch account quotas</span></span>
<span data-ttu-id="b8cfc-139">Antes de crear una cuenta de Lote en una región, puede comprobar la suscripción de Azure para ver si se puede agregar una cuenta en esa región.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-139">Before creating a Batch account in a region, you can check your Azure subscription to see whether you are able to add an account in that region.</span></span>

<span data-ttu-id="b8cfc-140">En el siguiente fragmento de código, primero se usa [BatchManagementClient.Accounts.ListAsync][net_mgmt_listaccounts] para obtener una colección de todas las cuentas de Batch que están en una suscripción.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-140">In the code snippet below, we first use [BatchManagementClient.Account.ListAsync][net_mgmt_listaccounts] to get a collection of all Batch accounts that are within a subscription.</span></span> <span data-ttu-id="b8cfc-141">Una vez obtenida esta colección, se determina el número de cuentas que están en la región de destino.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-141">Once we've obtained this collection, we determine how many accounts are in the target region.</span></span> <span data-ttu-id="b8cfc-142">Posteriormente, se usa [BatchManagementClient.Subscriptions][net_mgmt_subscriptions] para obtener la cuota de la cuenta de Batch y determinar el número de cuentas que se pueden crear en dicha región (si se puede crear alguna).</span><span class="sxs-lookup"><span data-stu-id="b8cfc-142">Then we use [BatchManagementClient.Subscriptions][net_mgmt_subscriptions] to obtain the Batch account quota and determine how many accounts (if any) can be created in that region.</span></span>

```csharp
// Get a collection of all Batch accounts within the subscription
BatchAccountListResponse listResponse =
        await batchManagementClient.Account.ListAsync(new AccountListParameters());
IList<AccountResource> accounts = listResponse.Accounts;
Console.WriteLine("Total number of Batch accounts under subscription id {0}:  {1}",
    creds.SubscriptionId,
    accounts.Count);

// Get a count of all accounts within the target region
string region = "westus";
int accountsInRegion = accounts.Count(o => o.Location == region);

// Get the account quota for the specified region
SubscriptionQuotasGetResponse quotaResponse = await batchManagementClient.Subscriptions.GetSubscriptionQuotasAsync(region);
Console.WriteLine("Account quota for {0} region: {1}", region, quotaResponse.AccountQuota);

// Determine how many accounts can be created in the target region
Console.WriteLine("Accounts in {0}: {1}", region, accountsInRegion);
Console.WriteLine("You can create {0} accounts in the {1} region.", quotaResponse.AccountQuota - accountsInRegion, region);
```

<span data-ttu-id="b8cfc-143">En el fragmento de código anterior, `creds` es una instancia de [TokenCloudCredentials][azure_tokencreds].</span><span class="sxs-lookup"><span data-stu-id="b8cfc-143">In the snippet above, `creds` is an instance of [TokenCloudCredentials][azure_tokencreds].</span></span> <span data-ttu-id="b8cfc-144">Para ver un ejemplo de creación de este objeto, consulte el ejemplo de código [AccountManagement][acct_mgmt_sample] en GitHub.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-144">To see an example of creating this object, see the [AccountManagement][acct_mgmt_sample] code sample on GitHub.</span></span>

### <a name="check-a-batch-account-for-compute-resource-quotas"></a><span data-ttu-id="b8cfc-145">Comprobación de una cuenta de Lote para las cuotas de recursos de proceso</span><span class="sxs-lookup"><span data-stu-id="b8cfc-145">Check a Batch account for compute resource quotas</span></span>
<span data-ttu-id="b8cfc-146">Antes de incrementar los recursos de proceso en la solución de Batch, puede hacer una comprobación para asegurarse de que los recursos que quiere asignar no sobrepasan las cuotas de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-146">Before increasing compute resources in your Batch solution, you can check to ensure the resources you want to allocate won't exceed the account's quotas.</span></span> <span data-ttu-id="b8cfc-147">En el fragmento de código siguiente, se imprime la información de cuota de la cuenta de Batch llamada `mybatchaccount`.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-147">In the code snippet below, we print the quota information for the Batch account named `mybatchaccount`.</span></span> <span data-ttu-id="b8cfc-148">Puede utilizar esta información en su aplicación para determinar si la cuenta es capaz de administrar los recursos adicionales que se van a crear.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-148">In your own application, you could use such information to determine whether the account can handle the additional resources to be created.</span></span>

```csharp
// First obtain the Batch account
BatchAccountGetResponse getResponse =
    await batchManagementClient.Account.GetAsync("MyResourceGroup", "mybatchaccount");
AccountResource account = getResponse.Resource;

// Now print the compute resource quotas for the account
Console.WriteLine("Core quota: {0}", account.Properties.CoreQuota);
Console.WriteLine("Pool quota: {0}", account.Properties.PoolQuota);
Console.WriteLine("Active job and job schedule quota: {0}", account.Properties.ActiveJobAndJobScheduleQuota);
```

> [!IMPORTANT]
> <span data-ttu-id="b8cfc-149">Aunque existen cuotas predeterminadas para los servicios y las suscripciones de Azure, muchos de estos límites se pueden aumentar mediante una solicitud en [Azure Portal][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="b8cfc-149">While there are default quotas for Azure subscriptions and services, many of these limits can be raised by issuing a request in the [Azure portal][azure_portal].</span></span> <span data-ttu-id="b8cfc-150">Por ejemplo, consulte [Cuotas y límites del servicio de Lote de Azure](batch-quota-limit.md) para obtener instrucciones sobre cómo aumentar las cuotas de la cuenta de Lote.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-150">For example, see [Quotas and limits for the Azure Batch service](batch-quota-limit.md) for instructions on increasing your Batch account quotas.</span></span>
> 
> 

## <a name="use-azure-ad-with-batch-management-net"></a><span data-ttu-id="b8cfc-151">Uso de Azure AD con .NET de administración de Batch</span><span class="sxs-lookup"><span data-stu-id="b8cfc-151">Use Azure AD with Batch Management .NET</span></span>

<span data-ttu-id="b8cfc-152">La biblioteca .NET de administración de Batch es un cliente de proveedor de recursos de Azure y se utiliza junto con [Azure Resource Manager][resman_overview] para administrar estos recursos de cuenta mediante programación.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-152">The Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] to manage account resources programmatically.</span></span> <span data-ttu-id="b8cfc-153">Se requiere Azure AD para autenticar las solicitudes realizadas a través de cualquier cliente de proveedor de recursos de Azure, incluida la biblioteca .NET de administración de Batch y a través de [Azure Resource Manager][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="b8cfc-153">Azure AD is required to authenticate requests made through any Azure resource provider client, including the Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span> <span data-ttu-id="b8cfc-154">Para obtener información acerca del uso de Azure AD con la biblioteca .NET de administración de Batch, vea [Uso de Azure Active Directory para autenticar soluciones de Batch](batch-aad-auth.md).</span><span class="sxs-lookup"><span data-stu-id="b8cfc-154">For information about using Azure AD with the Batch Management .NET library, see [Use Azure Active Directory to authenticate Batch solutions](batch-aad-auth.md).</span></span> 

## <a name="sample-project-on-github"></a><span data-ttu-id="b8cfc-155">Proyecto de ejemplo en GitHub</span><span class="sxs-lookup"><span data-stu-id="b8cfc-155">Sample project on GitHub</span></span>

<span data-ttu-id="b8cfc-156">Para ver Batch Management .NET en acción, consulte el proyecto de ejemplo [AccountManagment][acct_mgmt_sample] en GitHub.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-156">To see Batch Management .NET in action, check out the [AccountManagment][acct_mgmt_sample] sample project on GitHub.</span></span> <span data-ttu-id="b8cfc-157">La aplicación de ejemplo AccountManagement muestra las siguientes operaciones:</span><span class="sxs-lookup"><span data-stu-id="b8cfc-157">The AccountManagment sample application demonstrates the following operations:</span></span>

1. <span data-ttu-id="b8cfc-158">Adquiera un token de seguridad en Azure AD mediante [ADAL][aad_adal].</span><span class="sxs-lookup"><span data-stu-id="b8cfc-158">Acquire a security token from Azure AD by using [ADAL][aad_adal].</span></span> <span data-ttu-id="b8cfc-159">Si el usuario aún no ha iniciado sesión, se le pedirán sus credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-159">If the user is not already signed in, they are prompted for their Azure credentials.</span></span>
2. <span data-ttu-id="b8cfc-160">Cree un objeto [SubscriptionClient][resman_subclient] mediante el token de seguridad obtenido de Azure AD para consultar en Azure una lista de las suscripciones asociadas a la cuenta.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-160">With the security token obtained from Azure AD, create a [SubscriptionClient][resman_subclient] to query Azure for a list of subscriptions associated with the account.</span></span> <span data-ttu-id="b8cfc-161">El usuario puede seleccionar una suscripción de la lista si contiene más de una suscripción.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-161">The user can select a subscription from the list if it contains more than one subscription.</span></span>
3. <span data-ttu-id="b8cfc-162">Obtenga las credenciales asociadas con la suscripción seleccionada.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-162">Get credentials associated with the selected subscription.</span></span>
4. <span data-ttu-id="b8cfc-163">Cree un objeto [ResourceManagementClient][resman_client] con las credenciales.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-163">Create a [ResourceManagementClient][resman_client] object by using the credentials.</span></span>
5. <span data-ttu-id="b8cfc-164">Use un objeto [ResourceManagementClient][resman_client] para crear un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-164">Use a [ResourceManagementClient][resman_client] object to create a resource group.</span></span>
6. <span data-ttu-id="b8cfc-165">Use un objeto [BatchManagementClient][net_mgmt_client] para realizar varias operaciones de cuenta de Batch:</span><span class="sxs-lookup"><span data-stu-id="b8cfc-165">Use a [BatchManagementClient][net_mgmt_client] object to perform several Batch account operations:</span></span>
   * <span data-ttu-id="b8cfc-166">Crear una cuenta de Batch en el nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-166">Create a Batch account in the new resource group.</span></span>
   * <span data-ttu-id="b8cfc-167">Obtener la cuenta recién creada desde el servicio Lote.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-167">Get the newly created account from the Batch service.</span></span>
   * <span data-ttu-id="b8cfc-168">Imprimir las claves de la nueva cuenta.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-168">Print the account keys for the new account.</span></span>
   * <span data-ttu-id="b8cfc-169">Regenerar una nueva clave principal para la cuenta.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-169">Regenerate a new primary key for the account.</span></span>
   * <span data-ttu-id="b8cfc-170">Imprimir la información de cuota de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-170">Print the quota information for the account.</span></span>
   * <span data-ttu-id="b8cfc-171">Imprimir la información de cuota de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-171">Print the quota information for the subscription.</span></span>
   * <span data-ttu-id="b8cfc-172">Imprimir todas las cuentas de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-172">Print all accounts within the subscription.</span></span>
   * <span data-ttu-id="b8cfc-173">Eliminar la cuenta recién creada.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-173">Delete newly created account.</span></span>
7. <span data-ttu-id="b8cfc-174">Elimine el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-174">Delete the resource group.</span></span>

<span data-ttu-id="b8cfc-175">Antes de eliminar el grupo de recursos y la cuenta de Batch recién creados, puede verlos en [Azure Portal][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="b8cfc-175">Before deleting the newly created Batch account and resource group, you can view them in the [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="b8cfc-176">Para ejecutar la aplicación de ejemplo correctamente, primero debe registrarla en el inquilino de Azure AD en Azure Portal y conceder permisos a la API de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b8cfc-176">To run the sample application successfully, you must first register it with your Azure AD tenant in the Azure portal and grant permissions to the Azure Resource Manager API.</span></span> <span data-ttu-id="b8cfc-177">Siga los pasos proporcionados en [Autenticación de soluciones de administración de Batch con Active Directory](batch-aad-auth-management.md).</span><span class="sxs-lookup"><span data-stu-id="b8cfc-177">Follow the steps provided in [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span>


<span data-ttu-id="b8cfc-178">[aad_about]: ../active-directory/active-directory-whatis.md "¿Qué es Azure Active Directory?"</span><span class="sxs-lookup"><span data-stu-id="b8cfc-178">[aad_about]: ../active-directory/active-directory-whatis.md "What is Azure Active Directory?"</span></span>
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
<span data-ttu-id="b8cfc-179">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Escenarios de autenticación para Azure AD"</span><span class="sxs-lookup"><span data-stu-id="b8cfc-179">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Authentication Scenarios for Azure AD"</span></span>
<span data-ttu-id="b8cfc-180">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integración de aplicaciones con Azure Active Directory"</span><span class="sxs-lookup"><span data-stu-id="b8cfc-180">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrating Applications with Azure Active Directory"</span></span>
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
