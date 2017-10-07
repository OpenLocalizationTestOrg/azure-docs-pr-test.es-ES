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
# <a name="service-bus-management-libraries"></a>Bibliotecas de administración de Service Bus

las bibliotecas de administración de Service Bus de Azure Hola dinámicamente pueden aprovisionar las entidades y espacios de nombres de Bus de servicio. Esto permite que las implementaciones complejas y escenarios de mensajería y hace posible tooprogrammatically determinar qué tooprovision de entidades. Estas bibliotecas están actualmente disponibles para .NET.

## <a name="supported-functionality"></a>Funcionalidad admitida

* Creación, actualización y eliminación de espacios de nombres
* Creación, actualización y eliminación de colas
* Creación, actualización y eliminación de temas
* Creación, actualización y eliminación de suscripciones

## <a name="prerequisites"></a>Requisitos previos

tooget a usar las bibliotecas de administración de Service Bus hello, debe autenticarse con hello servicio de Azure Active Directory (AAD). AAD requiere que autentiquen como una entidad de servicio, que proporciona acceso tooyour recursos de Azure. Para más información sobre cómo crear una entidad de servicio, consulte uno de los siguientes artículos:  

* [Use la aplicación de Active Directory de Azure toocreate portal hello y entidad de servicio que puede tener acceso a recursos](/azure/azure-resource-manager/resource-group-create-service-principal-portal)
* [Usar una entidad de seguridad tooaccess los recursos del servicio de toocreate de PowerShell de Azure](/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [Usar una entidad de seguridad tooaccess los recursos del servicio de toocreate de CLI de Azure](/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)

Estos tutoriales le proporcionan una `AppId` (Id. de cliente), `TenantId`, y `ClientSecret` (clave de autenticación), todos ellos se utilizan para la autenticación mediante las bibliotecas de administración de Hola. Debe tener **propietario** permisos para el grupo de recursos de hello en el que desea toorun.

## <a name="programming-pattern"></a>Modelo de programación

Hola patrón toomanipulate cualquier recurso de Bus de servicio sigue un protocolo común:

1. Obtener un token de Azure Active Directory con hello **Microsoft.IdentityModel.Clients.ActiveDirectory** biblioteca.
   ```csharp
   var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

   var result = await context.AcquireTokenAsync("https://management.core.windows.net/", new ClientCredential(clientId, clientSecret));
   ```

1. Crear hello `ServiceBusManagementClient` objeto.

   ```csharp
   var creds = new TokenCredentials(token);
   var sbClient = new ServiceBusManagementClient(creds)
   {
       SubscriptionId = SettingsCache["SubscriptionId"]
   };
   ```

1. Conjunto hello `CreateOrUpdate` parámetros tooyour los valores especificados.

   ```csharp
   var queueParams = new QueueCreateOrUpdateParameters()
   {
       Location = SettingsCache["DataCenterLocation"],
       EnablePartitioning = true
   };
   ```

1. Hola la llamada a Execute.

   ```csharp
   await sbClient.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, QueueName, queueParams);
   ```

## <a name="next-steps"></a>Pasos siguientes
* [Ejemplo de administración de .NET](https://github.com/Azure-Samples/service-bus-dotnet-management/)
* [Microsoft.Azure.Management.ServiceBus API reference](/dotnet/api/Microsoft.Azure.Management.ServiceBus) (Referencia de API de Microsoft.Azure.Management.ServiceBus)
