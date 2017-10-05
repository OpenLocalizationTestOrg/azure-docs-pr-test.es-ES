---
title: "Bibliotecas de administración de Azure Event Hubs | Microsoft Docs"
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
ms.openlocfilehash: 0d659cb860a6c98342b548212820efe046decfcc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="event-hubs-management-libraries"></a><span data-ttu-id="1e815-103">Bibliotecas de administración de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="1e815-103">Event Hubs management libraries</span></span>

<span data-ttu-id="1e815-104">Las bibliotecas de administración de Event Hubs pueden aprovisionar dinámicamente las entidades y los espacios de nombres de Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="1e815-104">The Event Hubs management libraries can dynamically provision Event Hubs namespaces and entities.</span></span> <span data-ttu-id="1e815-105">Esto posibilita los escenarios complejos de implementación y mensajería, lo que permite determinar mediante programación qué entidades aprovisionar.</span><span class="sxs-lookup"><span data-stu-id="1e815-105">This enables complex deployments and messaging scenarios, so that you can programmatically determine what entities to provision.</span></span> <span data-ttu-id="1e815-106">Estas bibliotecas están actualmente disponibles para .NET.</span><span class="sxs-lookup"><span data-stu-id="1e815-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="1e815-107">Funcionalidad admitida</span><span class="sxs-lookup"><span data-stu-id="1e815-107">Supported functionality</span></span>

* <span data-ttu-id="1e815-108">Creación, actualización y eliminación de espacios de nombres</span><span class="sxs-lookup"><span data-stu-id="1e815-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="1e815-109">Creación, actualización y eliminación de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="1e815-109">Event Hubs creation, update, deletion</span></span>
* <span data-ttu-id="1e815-110">Creación, actualización y eliminación de grupos de consumidores</span><span class="sxs-lookup"><span data-stu-id="1e815-110">Consumer Group creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e815-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1e815-111">Prerequisites</span></span>

<span data-ttu-id="1e815-112">Para comenzar a usar las bibliotecas de administración de Event Hubs, debe autenticarse con Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="1e815-112">To get started using the Event Hubs management libraries, you must authenticate with Azure Active Directory (AAD).</span></span> <span data-ttu-id="1e815-113">AAD requiere que se autentique como una entidad de servicio que proporciona acceso a los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="1e815-113">AAD requires that you authenticate as a service principal, which provides access to your Azure resources.</span></span> <span data-ttu-id="1e815-114">Para más información sobre cómo crear una entidad de servicio, consulte uno de los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="1e815-114">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="1e815-115">Uso de Azure Portal para crear una aplicación de Active Directory y una entidad de servicio con acceso a los recursos</span><span class="sxs-lookup"><span data-stu-id="1e815-115">Use the Azure portal to create Active Directory application and service principal that can access resources</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="1e815-116">Uso de Azure PowerShell para crear a una entidad de servicio para acceder a recursos</span><span class="sxs-lookup"><span data-stu-id="1e815-116">Use Azure PowerShell to create a service principal to access resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="1e815-117">Uso de la CLI de Azure para crear a una entidad de servicio para acceder a recursos</span><span class="sxs-lookup"><span data-stu-id="1e815-117">Use Azure CLI to create a service principal to access resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)

<span data-ttu-id="1e815-118">Estos tutoriales le proporcionan valores para `AppId` (identificador de cliente), `TenantId` y `ClientSecret` (clave de autenticación), que usan las bibliotecas de administración con fines de autenticación.</span><span class="sxs-lookup"><span data-stu-id="1e815-118">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by the management libraries.</span></span> <span data-ttu-id="1e815-119">Debe tener permisos de **Propietario** en el grupo de recursos en el que desea realizar la ejecución.</span><span class="sxs-lookup"><span data-stu-id="1e815-119">You must have **Owner** permissions for the resource group on which you want to run.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="1e815-120">Modelo de programación</span><span class="sxs-lookup"><span data-stu-id="1e815-120">Programming pattern</span></span>

<span data-ttu-id="1e815-121">El patrón para manipular los recursos de Event Hubs sigue un protocolo común:</span><span class="sxs-lookup"><span data-stu-id="1e815-121">The pattern to manipulate any Event Hubs resource follows a common protocol:</span></span>

1. <span data-ttu-id="1e815-122">Obtenga un token de AAD mediante la biblioteca `Microsoft.IdentityModel.Clients.ActiveDirectory`.</span><span class="sxs-lookup"><span data-stu-id="1e815-122">Obtain a token from AAD using the `Microsoft.IdentityModel.Clients.ActiveDirectory` library.</span></span>
    ```csharp
    var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

    var result = await context.AcquireTokenAsync(
        "https://management.core.windows.net/",
        new ClientCredential(clientId, clientSecret)
    );
    ```

1. <span data-ttu-id="1e815-123">Cree el objeto `EventHubManagementClient`.</span><span class="sxs-lookup"><span data-stu-id="1e815-123">Create the `EventHubManagementClient` object.</span></span>
    ```csharp
    var creds = new TokenCredentials(token);
    var ehClient = new EventHubManagementClient(creds)
    {
        SubscriptionId = SettingsCache["SubscriptionId"]
    };
    ```

1. <span data-ttu-id="1e815-124">Establezca los parámetros de `CreateOrUpdate` en los valores especificados.</span><span class="sxs-lookup"><span data-stu-id="1e815-124">Set the `CreateOrUpdate` parameters to your specified values.</span></span>
    ```csharp
    var ehParams = new EventHubCreateOrUpdateParameters()
    {
        Location = SettingsCache["DataCenterLocation"]
    };
    ```

1. <span data-ttu-id="1e815-125">Ejecute la llamada.</span><span class="sxs-lookup"><span data-stu-id="1e815-125">Execute the call.</span></span>
    ```csharp
    await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, EventHubName, ehParams);
    ```

## <a name="next-steps"></a><span data-ttu-id="1e815-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1e815-126">Next steps</span></span>
* [<span data-ttu-id="1e815-127">Ejemplo de administración de .NET</span><span class="sxs-lookup"><span data-stu-id="1e815-127">.NET Management sample</span></span>](https://github.com/Azure-Samples/event-hubs-dotnet-management/)
* [<span data-ttu-id="1e815-128">Referencia de Microsoft.Azure.Management.EventHub</span><span class="sxs-lookup"><span data-stu-id="1e815-128">Microsoft.Azure.Management.EventHub Reference</span></span>](/dotnet/api/Microsoft.Azure.Management.EventHub) 
