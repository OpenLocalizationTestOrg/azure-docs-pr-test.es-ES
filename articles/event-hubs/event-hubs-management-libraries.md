---
title: "las bibliotecas de administración de centros de eventos aaaAzure | Documentos de Microsoft"
description: "Administración de entidades y espacios de nombres de Event Hubs desde .NET"
services: event-hubs
cloud: na
documentationcenter: na
author: sethmanheim
manager: timlt
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: b7db0077f6f31397ae46e926c3c28630a157824c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-management-libraries"></a><span data-ttu-id="c3583-103">Bibliotecas de administración de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="c3583-103">Event Hubs management libraries</span></span>

<span data-ttu-id="c3583-104">las bibliotecas de administración de centros de eventos de Hello dinámicamente pueden aprovisionar las entidades y espacios de nombres de los centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="c3583-104">hello Event Hubs management libraries can dynamically provision Event Hubs namespaces and entities.</span></span> <span data-ttu-id="c3583-105">Así, las implementaciones complejas y escenarios de mensajería, por lo que se puede determinar mediante programación qué tooprovision de entidades.</span><span class="sxs-lookup"><span data-stu-id="c3583-105">This enables complex deployments and messaging scenarios, so that you can programmatically determine what entities tooprovision.</span></span> <span data-ttu-id="c3583-106">Estas bibliotecas están actualmente disponibles para .NET.</span><span class="sxs-lookup"><span data-stu-id="c3583-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="c3583-107">Funcionalidad admitida</span><span class="sxs-lookup"><span data-stu-id="c3583-107">Supported functionality</span></span>

* <span data-ttu-id="c3583-108">Creación, actualización y eliminación de espacios de nombres</span><span class="sxs-lookup"><span data-stu-id="c3583-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="c3583-109">Creación, actualización y eliminación de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="c3583-109">Event Hubs creation, update, deletion</span></span>
* <span data-ttu-id="c3583-110">Creación, actualización y eliminación de grupos de consumidores</span><span class="sxs-lookup"><span data-stu-id="c3583-110">Consumer Group creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3583-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c3583-111">Prerequisites</span></span>

<span data-ttu-id="c3583-112">tooget a usar las bibliotecas de administración de centros de eventos de hello, debe autenticarse con Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="c3583-112">tooget started using hello Event Hubs management libraries, you must authenticate with Azure Active Directory (AAD).</span></span> <span data-ttu-id="c3583-113">AAD requiere que autentiquen como una entidad de servicio, que proporciona acceso tooyour recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="c3583-113">AAD requires that you authenticate as a service principal, which provides access tooyour Azure resources.</span></span> <span data-ttu-id="c3583-114">Para más información sobre cómo crear una entidad de servicio, consulte uno de los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="c3583-114">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="c3583-115">Use la aplicación de Active Directory de Azure toocreate portal hello y entidad de servicio que puede tener acceso a recursos</span><span class="sxs-lookup"><span data-stu-id="c3583-115">Use hello Azure portal toocreate Active Directory application and service principal that can access resources</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="c3583-116">Usar una entidad de seguridad tooaccess los recursos del servicio de toocreate de PowerShell de Azure</span><span class="sxs-lookup"><span data-stu-id="c3583-116">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="c3583-117">Usar una entidad de seguridad tooaccess los recursos del servicio de toocreate de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="c3583-117">Use Azure CLI toocreate a service principal tooaccess resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)

<span data-ttu-id="c3583-118">Estos tutoriales le proporcionan una `AppId` (Id. de cliente), `TenantId`, y `ClientSecret` (clave de autenticación), todos ellos se utilizan para la autenticación mediante las bibliotecas de administración de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3583-118">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by hello management libraries.</span></span> <span data-ttu-id="c3583-119">Debe tener **propietario** permisos para el grupo de recursos de hello en el que desea toorun.</span><span class="sxs-lookup"><span data-stu-id="c3583-119">You must have **Owner** permissions for hello resource group on which you want toorun.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="c3583-120">Modelo de programación</span><span class="sxs-lookup"><span data-stu-id="c3583-120">Programming pattern</span></span>

<span data-ttu-id="c3583-121">Hola patrón toomanipulate cualquier recurso de los centros de eventos sigue un protocolo común:</span><span class="sxs-lookup"><span data-stu-id="c3583-121">hello pattern toomanipulate any Event Hubs resource follows a common protocol:</span></span>

1. <span data-ttu-id="c3583-122">Obtener un token de AAD con hello `Microsoft.IdentityModel.Clients.ActiveDirectory` biblioteca.</span><span class="sxs-lookup"><span data-stu-id="c3583-122">Obtain a token from AAD using hello `Microsoft.IdentityModel.Clients.ActiveDirectory` library.</span></span>
    ```csharp
    var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

    var result = await context.AcquireTokenAsync(
        "https://management.core.windows.net/",
        new ClientCredential(clientId, clientSecret)
    );
    ```

1. <span data-ttu-id="c3583-123">Crear hello `EventHubManagementClient` objeto.</span><span class="sxs-lookup"><span data-stu-id="c3583-123">Create hello `EventHubManagementClient` object.</span></span>
    ```csharp
    var creds = new TokenCredentials(token);
    var ehClient = new EventHubManagementClient(creds)
    {
        SubscriptionId = SettingsCache["SubscriptionId"]
    };
    ```

1. <span data-ttu-id="c3583-124">Conjunto hello `CreateOrUpdate` parámetros tooyour los valores especificados.</span><span class="sxs-lookup"><span data-stu-id="c3583-124">Set hello `CreateOrUpdate` parameters tooyour specified values.</span></span>
    ```csharp
    var ehParams = new EventHubCreateOrUpdateParameters()
    {
        Location = SettingsCache["DataCenterLocation"]
    };
    ```

1. <span data-ttu-id="c3583-125">Hola la llamada a Execute.</span><span class="sxs-lookup"><span data-stu-id="c3583-125">Execute hello call.</span></span>
    ```csharp
    await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, EventHubName, ehParams);
    ```

## <a name="next-steps"></a><span data-ttu-id="c3583-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c3583-126">Next steps</span></span>
* [<span data-ttu-id="c3583-127">Ejemplo de administración de .NET</span><span class="sxs-lookup"><span data-stu-id="c3583-127">.NET Management sample</span></span>](https://github.com/Azure-Samples/event-hubs-dotnet-management/)
* [<span data-ttu-id="c3583-128">Referencia de Microsoft.Azure.Management.EventHub</span><span class="sxs-lookup"><span data-stu-id="c3583-128">Microsoft.Azure.Management.EventHub Reference</span></span>](/dotnet/api/Microsoft.Azure.Management.EventHub) 
