---
title: aaaUsing .NET SDK tooaccess las API de servicio de Azure Mobile Engagement
description: "Describe cómo toouse Hola .NET SDK de Mobile Engagement tooaccess las API de servicio de Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: c07728aa-43f2-4238-8b4a-c9eddf9d838b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 812be6f507b29f7b2de6454e06face8082c2d161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-net-sdk-tooaccess-azure-mobile-engagement-service-apis"></a>Uso de las API de servicio de Azure Mobile Engagement del SDK de .NET tooaccess
Azure Mobile Engagement expone un conjunto de API para que los dispositivos toomanage, cobertura o insertar campañas toointeract etc. con estas API, se proporcionan también un [archivo Swagger](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) que puede usar con herramientas de SDK de toogenerate para su preferido idioma. Se recomienda usar hello [AutoRest](https://github.com/Azure/AutoRest) toogenerate de herramientas del SDK de nuestro archivo Swagger.

> [!NOTE]
> servicio de Azure Mobile Engagement Hola se retirará de 2018 de marzo y actualmente solo los clientes de tooexisting disponible. Para más información, consulte [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).

Hemos creado un SDK para .NET de forma similar, que le permite toointeract con estas API utilizando un contenedor de C# y no tiene toodo Hola negociación del token de autenticación y actualizar usted mismo.  

Este ejemplo pasa por conjunto de Hola de pasos toofollow toouse Hola .NET SDK:

1. En primer lugar, necesita la autenticación de hello toosetup para su API con hello Azure Active Directory tal y como se describe [aquí](mobile-engagement-api-authentication.md#authentication). Al final de Hola de estos pasos, debe tener un válido **SubscriptionId**, **TenantId**, **ApplicationId** y **secreto**. 
2. Usaremos una simple toodemonstrate de aplicación de consola de Windows funciona con hello .NET SDK con el escenario de Hola de creación de una campaña de anuncio. Abra Visual Studio y cree una **aplicación de consola**.   
3. A continuación deberá hello toodownload SDK de .NET que está disponible como **biblioteca de administración de Microsoft Azure Engagement** en la Galería de Nuget hello [aquí](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/).
   Si va a instalar Hola Nuget desde Visual Studio, necesita tooensure que dispone de verificación marcada hello **versión preliminar de inclusión** opción al buscar el paquete de hello:
   
    ![][1]
4. Hola `Program.cs` , agregue Hola después de los espacios de nombres:
   
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Azure.Management.Engagement;
        using Microsoft.Azure.Management.Engagement.Models;
5. A continuación debe toodefine Hola después de constantes que se usará para la autenticación e interactuar con la aplicación de interacción móvil de hello en el que va a crear la campaña de anuncio Hola:
   
        // For authentication
        const string TENANT_ID = "<Your TenantId>";
        const string CLIENT_ID = "<Your Application Id>";
        const string CLIENT_SECRET = "<Your Secret>";
        const string SUBSCRIPTION_ID = "<Your Subscription Id>";
   
        // This is hello Azure Resource group concept for grouping together resources 
        //  see here: https://azure.microsoft.com/en-us/documentation/articles/resource-group-portal/
        const string RESOURCE_GROUP = "";
   
        // For Mobile Engagement operations
        // App Collection Name 
        const string APP_COLLECTION_NAME = "";
        // Application Resource Name - make sure you are using hello one as specified in hello Azure portal (NOT hello App Name)
        const string APP_RESOURCE_NAME = "";
6. Definir hello `EngagementManagementClient` variable que vamos a usar métodos de SDK de Mobile Engagement Hola toocall:
   
        static EngagementManagementClient engagementClient; 
7. Agregar Hola después tooyour `Main` método:
   
        try
            {
                // Initialize hello Engagement SDK toocall out APIs. 
                InitEngagementClient().Wait();
   
                // Create a Reach campaign
                CreateCampaign().Wait();
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.InnerException.Message);
                throw ex;
            }
8. Definir Hola siguiendo el método que se encarga de inicializar hello `EngagementManagementClient` mediante la autenticación en primer lugar y, a continuación, asociar propio con la aplicación de interacción móvil de hello en el que piensa campaña de anuncio de Hola toocreate:
   
        private static async Task InitEngagementClient()
        {
            var credentials = await ApplicationTokenProvider.LoginSilentAsync(TENANT_ID, CLIENT_ID, CLIENT_SECRET);
            engagementClient = new EngagementManagementClient(credentials) { SubscriptionId = SUBSCRIPTION_ID };
   
            // This is hello Azure concept of ResourceGroup
            engagementClient.ResourceGroupName = RESOURCE_GROUP;
   
            // This is your Mobile Engagement App Collection & App Resource Name in which you create hello campaign
            engagementClient.AppCollection = APP_COLLECTION_NAME;
            engagementClient.AppName = APP_RESOURCE_NAME;
        }
   
   > [!IMPORTANT]
   > Tenga en cuenta que debe hello toouse **nombre de recurso de aplicación** tal como se define en el portal de administración de Azure de hello para el parámetro de AppName Hola. 
   > 
   > 
9. Por último, definir método CreateCampaign de hello que se encargará del uso de hello inicializado anteriormente EngagementClient toocreate simple **en cualquier momento** & **solo notificación** campaña con un título y un mensaje: 
   
        private async static Task CreateCampaign()
        {
            //  Refer toohello Announcement Campaign format from here - 
            //      https://msdn.microsoft.com/en-us/library/azure/mt683751.aspx
            // Make sure you are passing all hello non-optional parameters
            Campaign parameters = new Campaign(
                name:"WelcomeCampaign",
                notificationTitle: "Welcome", 
                notificationMessage: "Thank you for installing hello app!",
                type:"only_notif",
                deliveryTime:"any"
                );
   
            // Refer toohello Campaign Kinds from here - https://msdn.microsoft.com/en-us/library/azure/mt683742.aspx
            CampaignStateResult result = 
                await engagementClient.Campaigns.CreateAsync(CampaignKinds.Announcements, parameters);
            Console.WriteLine("Campaign Id '{0}' was created successfully and it is in '{1}' state", result.Id, result.State);
        }
10. Aplicación de consola de ejecución hello y verá la siguiente Hola durante la creación correcta de campaña de hello:
    
    **Campaign Id '159' was created successfully and it is in 'draft' state**

<!-- Images. -->

[1]: ./media/mobile-engagement-dotnet-sdk-service-api/include-prerelease.png
