---
title: "las bibliotecas de administración de Service Bus aaaAzure | Documentos de Microsoft"
description: "Administración de espacios de nombres y entidades de mensajería de Service Bus desde .NET"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: sethm
ms.openlocfilehash: 9e4ad91f22815ca0838e6e4647a3606109b2b441
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-management-libraries"></a><span data-ttu-id="a066e-103">Bibliotecas de administración de Service Bus</span><span class="sxs-lookup"><span data-stu-id="a066e-103">Service Bus management libraries</span></span>

<span data-ttu-id="a066e-104">las bibliotecas de administración de Service Bus de Azure Hola dinámicamente pueden aprovisionar las entidades y espacios de nombres de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="a066e-104">hello Azure Service Bus management libraries can dynamically provision Service Bus namespaces and entities.</span></span> <span data-ttu-id="a066e-105">Esto permite que las implementaciones complejas y escenarios de mensajería y hace posible tooprogrammatically determinar qué tooprovision de entidades.</span><span class="sxs-lookup"><span data-stu-id="a066e-105">This enables complex deployments and messaging scenarios, and makes it possible tooprogrammatically determine what entities tooprovision.</span></span> <span data-ttu-id="a066e-106">Estas bibliotecas están actualmente disponibles para .NET.</span><span class="sxs-lookup"><span data-stu-id="a066e-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="a066e-107">Funcionalidad admitida</span><span class="sxs-lookup"><span data-stu-id="a066e-107">Supported functionality</span></span>

* <span data-ttu-id="a066e-108">Creación, actualización y eliminación de espacios de nombres</span><span class="sxs-lookup"><span data-stu-id="a066e-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="a066e-109">Creación, actualización y eliminación de colas</span><span class="sxs-lookup"><span data-stu-id="a066e-109">Queue creation, update, deletion</span></span>
* <span data-ttu-id="a066e-110">Creación, actualización y eliminación de temas</span><span class="sxs-lookup"><span data-stu-id="a066e-110">Topic creation, update, deletion</span></span>
* <span data-ttu-id="a066e-111">Creación, actualización y eliminación de suscripciones</span><span class="sxs-lookup"><span data-stu-id="a066e-111">Subscription creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a066e-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a066e-112">Prerequisites</span></span>

<span data-ttu-id="a066e-113">tooget a usar las bibliotecas de administración de Service Bus hello, debe autenticarse con hello servicio de Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="a066e-113">tooget started using hello Service Bus management libraries, you must authenticate with hello Azure Active Directory (AAD) service.</span></span> <span data-ttu-id="a066e-114">AAD requiere que autentiquen como una entidad de servicio, que proporciona acceso tooyour recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="a066e-114">AAD requires that you authenticate as a service principal, which provides access tooyour Azure resources.</span></span> <span data-ttu-id="a066e-115">Para más información sobre cómo crear una entidad de servicio, consulte uno de los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="a066e-115">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="a066e-116">Use la aplicación de Active Directory de Azure toocreate portal hello y entidad de servicio que puede tener acceso a recursos</span><span class="sxs-lookup"><span data-stu-id="a066e-116">Use hello Azure portal toocreate Active Directory application and service principal that can access resources</span></span>](/azure/azure-resource-manager/resource-group-create-service-principal-portal)
* [<span data-ttu-id="a066e-117">Usar una entidad de seguridad tooaccess los recursos del servicio de toocreate de PowerShell de Azure</span><span class="sxs-lookup"><span data-stu-id="a066e-117">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="a066e-118">Usar una entidad de seguridad tooaccess los recursos del servicio de toocreate de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="a066e-118">Use Azure CLI toocreate a service principal tooaccess resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)

<span data-ttu-id="a066e-119">Estos tutoriales le proporcionan una `AppId` (Id. de cliente), `TenantId`, y `ClientSecret` (clave de autenticación), todos ellos se utilizan para la autenticación mediante las bibliotecas de administración de Hola.</span><span class="sxs-lookup"><span data-stu-id="a066e-119">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by hello management libraries.</span></span> <span data-ttu-id="a066e-120">Debe tener **propietario** permisos para el grupo de recursos de hello en el que desea toorun.</span><span class="sxs-lookup"><span data-stu-id="a066e-120">You must have **Owner** permissions for hello resource group on which you wish toorun.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="a066e-121">Modelo de programación</span><span class="sxs-lookup"><span data-stu-id="a066e-121">Programming pattern</span></span>

<span data-ttu-id="a066e-122">Hola patrón toomanipulate cualquier recurso de Bus de servicio sigue un protocolo común:</span><span class="sxs-lookup"><span data-stu-id="a066e-122">hello pattern toomanipulate any Service Bus resource follows a common protocol:</span></span>

1. <span data-ttu-id="a066e-123">Obtener un token de Azure Active Directory con hello **Microsoft.IdentityModel.Clients.ActiveDirectory** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="a066e-123">Obtain a token from Azure Active Directory using hello **Microsoft.IdentityModel.Clients.ActiveDirectory** library.</span></span>
   ```csharp
   var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

   var result = await context.AcquireTokenAsync("https://management.core.windows.net/", new ClientCredential(clientId, clientSecret));
   ```

1. <span data-ttu-id="a066e-124">Crear hello `ServiceBusManagementClient` objeto.</span><span class="sxs-lookup"><span data-stu-id="a066e-124">Create hello `ServiceBusManagementClient` object.</span></span>

   ```csharp
   var creds = new TokenCredentials(token);
   var sbClient = new ServiceBusManagementClient(creds)
   {
       SubscriptionId = SettingsCache["SubscriptionId"]
   };
   ```

1. <span data-ttu-id="a066e-125">Conjunto hello `CreateOrUpdate` parámetros tooyour los valores especificados.</span><span class="sxs-lookup"><span data-stu-id="a066e-125">Set hello `CreateOrUpdate` parameters tooyour specified values.</span></span>

   ```csharp
   var queueParams = new QueueCreateOrUpdateParameters()
   {
       Location = SettingsCache["DataCenterLocation"],
       EnablePartitioning = true
   };
   ```

1. <span data-ttu-id="a066e-126">Hola la llamada a Execute.</span><span class="sxs-lookup"><span data-stu-id="a066e-126">Execute hello call.</span></span>

   ```csharp
   await sbClient.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, QueueName, queueParams);
   ```

## <a name="next-steps"></a><span data-ttu-id="a066e-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a066e-127">Next steps</span></span>
* [<span data-ttu-id="a066e-128">Ejemplo de administración de .NET</span><span class="sxs-lookup"><span data-stu-id="a066e-128">.NET management sample</span></span>](https://github.com/Azure-Samples/service-bus-dotnet-management/)
* <span data-ttu-id="a066e-129">[Microsoft.Azure.Management.ServiceBus API reference](/dotnet/api/Microsoft.Azure.Management.ServiceBus) (Referencia de API de Microsoft.Azure.Management.ServiceBus)</span><span class="sxs-lookup"><span data-stu-id="a066e-129">[Microsoft.Azure.Management.ServiceBus API reference](/dotnet/api/Microsoft.Azure.Management.ServiceBus)</span></span>
