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
# <a name="manage-batch-accounts-and-quotas-with-hello-batch-management-client-library-for-net"></a>Administrar las cuentas de lote y las cuotas con la biblioteca de cliente de administración de lotes de Hola para .NET

> [!div class="op_single_selector"]
> * [Portal de Azure](batch-account-create-portal.md)
> * [NET de Administración de Lote](batch-management-dotnet.md)
> 
> 

Sólo puede bajar mantenimiento sobrecarga en las aplicaciones de Azure Batch mediante el uso de hello [.NET de administración de lotes] [ api_mgmt_net] creación de la cuenta de lote de biblioteca tooautomate, eliminación, administración de claves y detección de cuota.

* **Cree y elimine cuentas de Lote** en cualquier región. Si, por ejemplo, como un proveedor de software independiente (ISV) proporciona un servicio para los clientes en la que cada una se asigna una cuenta de lote independiente para la facturación, puede agregar cuenta creación y eliminación capacidades tooyour portal del cliente.
* **Recupere y regenere claves de la cuenta** mediante programación para cualquiera de sus cuentas de Lote. Esto puede ayudarle a cumplir las directivas de seguridad que exigen la sustitución periódica de las claves de cuenta. Si tiene varias cuentas de Batch en distintas regiones de Azure, la automatización de este proceso de sustitución mejorará la eficacia de la solución.
* **Compruebe las cuotas de la cuenta** y eliminan ensayo y error de hello conjeturas determinar qué cuentas de lote tienen los límites. Si comprueba las cuotas de las cuentas antes de iniciar un trabajo, crear un grupo o agregar un nodo de procesos, podrá ajustar de forma proactiva el lugar y el momento en que se crean estos recursos de proceso. Puede determinar qué cuentas requieren un aumento de la cuota antes de asignarles recursos adicionales.
* **Combinar las características de otros servicios de Azure** para una experiencia de administración completa--mediante el uso de .NET de administración de lotes, [Azure Active Directory][aad_about], hello y [Azure El Administrador de recursos] [ resman_overview] en hello misma aplicación. Mediante el uso de estas características y sus API, puede proporcionar una experiencia de autenticación sin dificultades, Hola toocreate de capacidad y eliminar grupos de recursos y las capacidades de hello descritas anteriormente para una solución de administración to-end.

> [!NOTE]
> Aunque en este artículo se centra en la administración mediante programación de Hola de las cuentas, las claves y las cuotas de lote, puede realizar muchas de estas actividades mediante hello [portal de Azure][azure_portal]. Para obtener más información, consulte [crear una cuenta de lote de Azure mediante el portal de Azure de hello](batch-account-create-portal.md) y [las cuotas y límites de hello servicio Azure Batch](batch-quota-limit.md).
> 
> 

## <a name="create-and-delete-batch-accounts"></a>Cree y elimine cuentas de Lote
Como se mencionó, una de las principales características de Hola de hello API de administración de lote es toocreate y eliminar cuentas de lote en una región de Azure. por lo tanto, use toodo [BatchManagementClient.Account.CreateAsync] [ net_create] y [DeleteAsync][net_delete], o en sus equivalentes sincrónicos.

Hello fragmento de código siguiente crea una cuenta, obtiene Hola recién creado cuenta de hello servicio por lotes y, a continuación, lo elimina. En este fragmento de código y otros Hola en este artículo, `batchManagementClient` es una instancia totalmente inicializada de [BatchManagementClient][net_mgmt_client].

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
> Aplicaciones que utilizan la biblioteca de .NET de administración de lotes de Hola y su clase BatchManagementClient requieren **Administrador de servicios** o **coadministrator** acceder a suscripción toohello que posee Hola Cuenta de lote toobe administrado. Para obtener más información, vea hello [Azure Active Directory](#azure-active-directory) hello y sección [AccountManagement] [ acct_mgmt_sample] ejemplo de código.
> 
> 

## <a name="retrieve-and-regenerate-account-keys"></a>Recupere y regenere claves de la cuenta
Obtenga las claves de las cuentas principal y secundaria de cualquier cuenta de Batch de su suscripción con [ListKeysAsync][net_list_keys]. Dichas claves se pueden regenerar con [RegenerateKeyAsync][net_regenerate_keys].

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
> Puede crear un flujo de trabajo de conexión simplificada para las aplicaciones de administración. En primer lugar, obtenga una clave de cuenta para la cuenta de lote de hello desea toomanage con [ListKeysAsync][net_list_keys]. A continuación, utilice esta clave al inicializar la biblioteca de .NET de lotes de hello [BatchSharedKeyCredentials] [ net_sharedkeycred] (clase), que se usa al inicializar [BatchClient] [net_batch_client].
> 
> 

## <a name="check-azure-subscription-and-batch-account-quotas"></a>Comprobación de la suscripción de Azure y cuotas de la cuenta de Lote
Las suscripciones de Azure y Hola servicios individuales de Azure como procesar por lotes todas tienen cuotas predeterminadas que limitan el número de Hola de ciertas entidades dentro de ellos. Para cuotas de hello predeterminadas para las suscripciones de Azure, consulte [suscripción de Azure y límites de servicio, cuotas y restricciones](../azure-subscription-service-limits.md). Para las cuotas predeterminadas de Hola de hello servicio por lotes, vea [las cuotas y límites de hello servicio Azure Batch](batch-quota-limit.md). Mediante la biblioteca de .NET de administración de lotes de hello, puede comprobar estas cuotas en sus aplicaciones. Esto le permite tomar decisiones de asignación de toomake antes de agregar las cuentas o recursos como grupos de proceso y nodos de proceso.

### <a name="check-an-azure-subscription-for-batch-account-quotas"></a>Comprobación de una suscripción de Azure para las cuotas de cuentas de Lote
Antes de crear una cuenta de lote en una región, puede comprobar su suscripción de Azure toosee tanto si es capaz de tooadd una cuenta en dicha región.

En el fragmento de código de hello a continuación, se utiliza primero [BatchManagementClient.Account.ListAsync] [ net_mgmt_listaccounts] tooget una colección de todas las cuentas de proceso por lotes que están dentro de una suscripción. Una vez que hemos obtenido esta colección, se determina cuántas cuentas están en la región de destino de Hola. A continuación, usamos [BatchManagementClient.Subscriptions] [ net_mgmt_subscriptions] tooobtain Hola cuota de la cuenta de lote y determinar el número de cuentas (si existe) se puede crear en dicha región.

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

En el fragmento de código de hello anterior, `creds` es una instancia de [TokenCloudCredentials][azure_tokencreds]. toosee muestra un ejemplo de creación de este objeto, vea hello [AccountManagement] [ acct_mgmt_sample] ejemplo de código en GitHub.

### <a name="check-a-batch-account-for-compute-resource-quotas"></a>Comprobación de una cuenta de Lote para las cuotas de recursos de proceso
Antes de aumentar los recursos de proceso en la solución de lote, puede comprobar los recursos de hello tooensure desea tooallocate no superan las cuotas de la cuenta de hello. En el fragmento de código de hello a continuación, imprimir información de cuota de Hola para hello con el nombre de cuenta de lote `mybatchaccount`. En su propia aplicación, podría utilizar este tipo toodetermine información si puede gestionar cuenta de Hola Hola recursos adicionales toobe creado.

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
> Aunque hay cuotas predeterminadas para los servicios y las suscripciones de Azure, muchos de estos límites pueden generarse mediante la emisión de una solicitud en hello [portal de Azure][azure_portal]. Por ejemplo, vea [las cuotas y límites de hello servicio Azure Batch](batch-quota-limit.md) para obtener instrucciones acerca de cómo aumentar las cuotas de la cuenta de lote.
> 
> 

## <a name="use-azure-ad-with-batch-management-net"></a>Uso de Azure AD con .NET de administración de Batch

biblioteca de .NET de administración de lotes de Hello es un cliente de proveedor de recursos de Azure y se utiliza junto con [Azure Resource Manager] [ resman_overview] toomanage cuenta de recursos mediante programación. Azure AD es las solicitudes de tooauthenticate necesario realizadas a través de cualquier cliente de proveedor de recursos de Azure, incluidos la biblioteca de .NET de administración de lotes de hello y [Azure Resource Manager][resman_overview]. Para obtener información acerca del uso de Azure AD con la biblioteca de .NET de administración de lotes de hello, consulte [soluciones de lote de uso de Azure Active Directory tooauthenticate](batch-aad-auth.md). 

## <a name="sample-project-on-github"></a>Proyecto de ejemplo en GitHub

toosee .NET de administración de lotes de acción, consulte hello [AccountManagment] [ acct_mgmt_sample] proyecto de ejemplo en GitHub. Hola AccountManagment aplicación de ejemplo muestra hello las siguientes operaciones:

1. Adquiera un token de seguridad en Azure AD mediante [ADAL][aad_adal]. Si el usuario de hello no ha iniciado ya sesión, se piden sus credenciales de Azure.
2. Con el token de seguridad de hello obtenido de Azure AD, crear un [SubscriptionClient] [ resman_subclient] tooquery Azure para obtener una lista de las suscripciones asociadas a la cuenta de hello. usuario de Hello puede seleccionar una suscripción de la lista de hello si contiene más de una suscripción.
3. Obtener las credenciales asociadas a la suscripción de hello seleccionado.
4. Crear un [ResourceManagementClient] [ resman_client] objeto mediante el uso de credenciales de Hola.
5. Use un [ResourceManagementClient] [ resman_client] toocreate un grupo de recursos de objeto.
6. Use un [BatchManagementClient] [ net_mgmt_client] objeto tooperform varias operaciones de la cuenta de lote:
   * Crear una cuenta de lote en el nuevo grupo de recursos Hola.
   * Obtener Hola recién creado cuenta de hello servicio por lotes.
   * Imprimir claves de cuenta de hello para la nueva cuenta de hello.
   * Volver a generar una nueva clave principal para la cuenta de hello.
   * Imprimir la información de cuota de hello para la cuenta de hello.
   * Imprimir la información de cuota de hello para la suscripción de Hola.
   * Imprimir todas las cuentas de suscripción de Hola.
   * Eliminar la cuenta recién creada.
7. Elimine el grupo de recursos de Hola.

Antes de eliminar el grupo de cuentas y recursos de proceso por lotes de hello recién creado, puede verlos en hello [portal de Azure][azure_portal]:

aplicación de ejemplo de Hola toorun correctamente, debe primero registrarlo con el inquilino de Azure AD en hello Azure portal y conceda permisos toohello API del Administrador de recursos de Azure. Siga los pasos de hello proporcionados en [soluciones de administración de lote autenticarse con Active Directory](batch-aad-auth-management.md).


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
