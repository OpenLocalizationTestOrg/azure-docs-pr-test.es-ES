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
# <a name="event-hubs-management-libraries"></a>Bibliotecas de administración de Event Hubs

las bibliotecas de administración de centros de eventos de Hello dinámicamente pueden aprovisionar las entidades y espacios de nombres de los centros de eventos. Así, las implementaciones complejas y escenarios de mensajería, por lo que se puede determinar mediante programación qué tooprovision de entidades. Estas bibliotecas están actualmente disponibles para .NET.

## <a name="supported-functionality"></a>Funcionalidad admitida

* Creación, actualización y eliminación de espacios de nombres
* Creación, actualización y eliminación de Event Hubs
* Creación, actualización y eliminación de grupos de consumidores

## <a name="prerequisites"></a>Requisitos previos

tooget a usar las bibliotecas de administración de centros de eventos de hello, debe autenticarse con Azure Active Directory (AAD). AAD requiere que autentiquen como una entidad de servicio, que proporciona acceso tooyour recursos de Azure. Para más información sobre cómo crear una entidad de servicio, consulte uno de los siguientes artículos:  

* [Use la aplicación de Active Directory de Azure toocreate portal hello y entidad de servicio que puede tener acceso a recursos](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [Usar una entidad de seguridad tooaccess los recursos del servicio de toocreate de PowerShell de Azure](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [Usar una entidad de seguridad tooaccess los recursos del servicio de toocreate de CLI de Azure](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)

Estos tutoriales le proporcionan una `AppId` (Id. de cliente), `TenantId`, y `ClientSecret` (clave de autenticación), todos ellos se utilizan para la autenticación mediante las bibliotecas de administración de Hola. Debe tener **propietario** permisos para el grupo de recursos de hello en el que desea toorun.

## <a name="programming-pattern"></a>Modelo de programación

Hola patrón toomanipulate cualquier recurso de los centros de eventos sigue un protocolo común:

1. Obtener un token de AAD con hello `Microsoft.IdentityModel.Clients.ActiveDirectory` biblioteca.
    ```csharp
    var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

    var result = await context.AcquireTokenAsync(
        "https://management.core.windows.net/",
        new ClientCredential(clientId, clientSecret)
    );
    ```

1. Crear hello `EventHubManagementClient` objeto.
    ```csharp
    var creds = new TokenCredentials(token);
    var ehClient = new EventHubManagementClient(creds)
    {
        SubscriptionId = SettingsCache["SubscriptionId"]
    };
    ```

1. Conjunto hello `CreateOrUpdate` parámetros tooyour los valores especificados.
    ```csharp
    var ehParams = new EventHubCreateOrUpdateParameters()
    {
        Location = SettingsCache["DataCenterLocation"]
    };
    ```

1. Hola la llamada a Execute.
    ```csharp
    await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, EventHubName, ehParams);
    ```

## <a name="next-steps"></a>Pasos siguientes
* [Ejemplo de administración de .NET](https://github.com/Azure-Samples/event-hubs-dotnet-management/)
* [Referencia de Microsoft.Azure.Management.EventHub](/dotnet/api/Microsoft.Azure.Management.EventHub) 
