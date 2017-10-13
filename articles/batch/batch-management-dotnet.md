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
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/11/2017
---
# <a name="manage-batch-accounts-and-quotas-with-the-batch-management-client-library-for-net"></a>Administración de cuentas y cuotas de Batch con la biblioteca cliente de administración de Batch para .NET

> [!div class="op_single_selector"]
> * [Portal de Azure](batch-account-create-portal.md)
> * [NET de Administración de Lote](batch-management-dotnet.md)
> 
> 

Puede reducir la sobrecarga de mantenimiento en las aplicaciones de Azure Batch con la biblioteca [Batch Management .NET][api_mgmt_net] para automatizar la creación, eliminación, administración de claves y detección de cuota de las cuentas de Batch.

* **Cree y elimine cuentas de Lote** en cualquier región. Por ejemplo, si como proveedor de software independiente (ISV) proporciona un servicio a los clientes en el que a cada uno se le asigna una cuenta de Lote independiente para la facturación, puede agregar capacidades de creación y eliminación de la cuenta al portal del cliente.
* **Recupere y regenere claves de la cuenta** mediante programación para cualquiera de sus cuentas de Lote. Esto puede ayudarle a cumplir las directivas de seguridad que exigen la sustitución periódica de las claves de cuenta. Si tiene varias cuentas de Batch en distintas regiones de Azure, la automatización de este proceso de sustitución mejorará la eficacia de la solución.
* **Compruebe las cuotas de la cuenta** y elimine las incertidumbres al determina los límites de cada cuenta de Lote. Si comprueba las cuotas de las cuentas antes de iniciar un trabajo, crear un grupo o agregar un nodo de procesos, podrá ajustar de forma proactiva el lugar y el momento en que se crean estos recursos de proceso. Puede determinar qué cuentas requieren un aumento de la cuota antes de asignarles recursos adicionales.
* **Combine las características de otros servicios de Azure** para una experiencia completa de administración, para lo que debe sacar provecho a la vez de la biblioteca Batch Management .NET, [Azure Active Directory][aad_about] y [Azure Resource Manager][resman_overview] en la misma aplicación. Mediante el uso de estas características y sus API puede proporcionar una experiencia de autenticación sin fricciones, la capacidad para crear y eliminar grupos de recursos, y las funcionalidades que se han descrito anteriormente para una solución de administración de un extremo a otro.

> [!NOTE]
> Aunque este artículo se centra en la administración de sus cuentas de Batch, claves y cuotas mediante programación, puede realizar muchas de estas actividades con [Azure Portal][azure_portal]. Para más información, consulte [Creación de una cuenta de Azure Batch con Azure Portal](batch-account-create-portal.md) y [Cuotas y límites del servicio Azure Batch](batch-quota-limit.md).
> 
> 

## <a name="create-and-delete-batch-accounts"></a>Cree y elimine cuentas de Lote
Tal y como se mencionó anteriormente, una de las principales características de Batch Management API es la creación y eliminación de cuentas de Batch en una región de Azure. Para ello, usará [BatchManagementClient.Account.CreateAsync][net_create] y [DeleteAsync][net_delete], o sus contrapartidas sincrónicas.

El fragmento de código siguiente crea una cuenta, obtiene la cuenta recién creada del servicio Lote y la elimina. En este y otros fragmentos de código que aparecen en el artículo, `batchManagementClient` es una instancia completamente inicializada de [BatchManagementClient][net_mgmt_client].

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
> Las aplicaciones que utilizan la biblioteca Batch Management .NET y su clase BatchManagementClient necesitan tener acceso de **administrador de servicio** o **coadministrador** en la suscripción propietaria de la cuenta de Batch que se va a administrar. Para más información, consulte la sección [Azure Active Directory](#azure-active-directory) a continuación y el código de ejemplo [AccountManagement][acct_mgmt_sample].
> 
> 

## <a name="retrieve-and-regenerate-account-keys"></a>Recupere y regenere claves de la cuenta
Obtenga las claves de las cuentas principal y secundaria de cualquier cuenta de Batch de su suscripción con [ListKeysAsync][net_list_keys]. Dichas claves se pueden regenerar con [RegenerateKeyAsync][net_regenerate_keys].

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
> Puede crear un flujo de trabajo de conexión simplificada para las aplicaciones de administración. En primer lugar, obtenga una clave de cuenta para la cuenta de Batch que desea administrar con [ListKeysAsync][net_list_keys]. Después, use esta clave al inicializar la clase [BatchSharedKeyCredentials][net_sharedkeycred] de la biblioteca de .NET de Batch, que se usa al inicializar [BatchClient][net_batch_client].
> 
> 

## <a name="check-azure-subscription-and-batch-account-quotas"></a>Comprobación de la suscripción de Azure y cuotas de la cuenta de Lote
Las suscripciones de Azure y los servicios individuales de Azure, como Lote, tienen cuotas predeterminadas que limitan el número de determinadas entidades que contienen. Para conocer las cuotas predeterminadas de las suscripciones de Azure, consulte [Límites, cuotas y restricciones de suscripción y servicios de Microsoft Azure](../azure-subscription-service-limits.md). Para conocer las cuotas predeterminadas del servicio Lote, consulte [Cuotas y límites del servicio de Lote de Azure](batch-quota-limit.md). Con la biblioteca Batch Management .NET, pude comprobar estas cuotas en sus aplicaciones. Esto le permite tomar decisiones sobre la asignación antes de agregar cuentas o recursos de proceso como los grupos y nodos de ejecución.

### <a name="check-an-azure-subscription-for-batch-account-quotas"></a>Comprobación de una suscripción de Azure para las cuotas de cuentas de Lote
Antes de crear una cuenta de Lote en una región, puede comprobar la suscripción de Azure para ver si se puede agregar una cuenta en esa región.

En el siguiente fragmento de código, primero se usa [BatchManagementClient.Accounts.ListAsync][net_mgmt_listaccounts] para obtener una colección de todas las cuentas de Batch que están en una suscripción. Una vez obtenida esta colección, se determina el número de cuentas que están en la región de destino. Posteriormente, se usa [BatchManagementClient.Subscriptions][net_mgmt_subscriptions] para obtener la cuota de la cuenta de Batch y determinar el número de cuentas que se pueden crear en dicha región (si se puede crear alguna).

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

En el fragmento de código anterior, `creds` es una instancia de [TokenCloudCredentials][azure_tokencreds]. Para ver un ejemplo de creación de este objeto, consulte el ejemplo de código [AccountManagement][acct_mgmt_sample] en GitHub.

### <a name="check-a-batch-account-for-compute-resource-quotas"></a>Comprobación de una cuenta de Lote para las cuotas de recursos de proceso
Antes de incrementar los recursos de proceso en la solución de Batch, puede hacer una comprobación para asegurarse de que los recursos que quiere asignar no sobrepasan las cuotas de la cuenta. En el fragmento de código siguiente, se imprime la información de cuota de la cuenta de Batch llamada `mybatchaccount`. Puede utilizar esta información en su aplicación para determinar si la cuenta es capaz de administrar los recursos adicionales que se van a crear.

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
> Aunque existen cuotas predeterminadas para los servicios y las suscripciones de Azure, muchos de estos límites se pueden aumentar mediante una solicitud en [Azure Portal][azure_portal]. Por ejemplo, consulte [Cuotas y límites del servicio de Lote de Azure](batch-quota-limit.md) para obtener instrucciones sobre cómo aumentar las cuotas de la cuenta de Lote.
> 
> 

## <a name="use-azure-ad-with-batch-management-net"></a>Uso de Azure AD con .NET de administración de Batch

La biblioteca .NET de administración de Batch es un cliente de proveedor de recursos de Azure y se utiliza junto con [Azure Resource Manager][resman_overview] para administrar estos recursos de cuenta mediante programación. Se requiere Azure AD para autenticar las solicitudes realizadas a través de cualquier cliente de proveedor de recursos de Azure, incluida la biblioteca .NET de administración de Batch y a través de [Azure Resource Manager][resman_overview]. Para obtener información acerca del uso de Azure AD con la biblioteca .NET de administración de Batch, vea [Uso de Azure Active Directory para autenticar soluciones de Batch](batch-aad-auth.md). 

## <a name="sample-project-on-github"></a>Proyecto de ejemplo en GitHub

Para ver Batch Management .NET en acción, consulte el proyecto de ejemplo [AccountManagment][acct_mgmt_sample] en GitHub. La aplicación de ejemplo AccountManagement muestra las siguientes operaciones:

1. Adquiera un token de seguridad en Azure AD mediante [ADAL][aad_adal]. Si el usuario aún no ha iniciado sesión, se le pedirán sus credenciales de Azure.
2. Cree un objeto [SubscriptionClient][resman_subclient] mediante el token de seguridad obtenido de Azure AD para consultar en Azure una lista de las suscripciones asociadas a la cuenta. El usuario puede seleccionar una suscripción de la lista si contiene más de una suscripción.
3. Obtenga las credenciales asociadas con la suscripción seleccionada.
4. Cree un objeto [ResourceManagementClient][resman_client] con las credenciales.
5. Use un objeto [ResourceManagementClient][resman_client] para crear un grupo de recursos.
6. Use un objeto [BatchManagementClient][net_mgmt_client] para realizar varias operaciones de cuenta de Batch:
   * Crear una cuenta de Batch en el nuevo grupo de recursos.
   * Obtener la cuenta recién creada desde el servicio Lote.
   * Imprimir las claves de la nueva cuenta.
   * Regenerar una nueva clave principal para la cuenta.
   * Imprimir la información de cuota de la cuenta.
   * Imprimir la información de cuota de la suscripción.
   * Imprimir todas las cuentas de la suscripción.
   * Eliminar la cuenta recién creada.
7. Elimine el grupo de recursos.

Antes de eliminar el grupo de recursos y la cuenta de Batch recién creados, puede verlos en [Azure Portal][azure_portal]:

Para ejecutar la aplicación de ejemplo correctamente, primero debe registrarla en el inquilino de Azure AD en Azure Portal y conceder permisos a la API de Azure Resource Manager. Siga los pasos proporcionados en [Autenticación de soluciones de administración de Batch con Active Directory](batch-aad-auth-management.md).


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
