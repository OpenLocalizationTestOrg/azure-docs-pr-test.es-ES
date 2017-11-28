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
# <a name="using-net-sdk-tooaccess-azure-mobile-engagement-service-apis"></a><span data-ttu-id="7536b-103">Uso de las API de servicio de Azure Mobile Engagement del SDK de .NET tooaccess</span><span class="sxs-lookup"><span data-stu-id="7536b-103">Using .NET SDK tooaccess Azure Mobile Engagement Service APIs</span></span>
<span data-ttu-id="7536b-104">Azure Mobile Engagement expone un conjunto de API para que los dispositivos toomanage, cobertura o insertar campañas toointeract etc. con estas API, se proporcionan también un [archivo Swagger](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) que puede usar con herramientas de SDK de toogenerate para su preferido idioma.</span><span class="sxs-lookup"><span data-stu-id="7536b-104">Azure Mobile Engagement exposes a set of APIs for you toomanage Devices, Reach/Push campaigns etc. toointeract with these APIs, we also provide you a [Swagger file](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) that you can use with tools toogenerate SDKs for your preferred language.</span></span> <span data-ttu-id="7536b-105">Se recomienda usar hello [AutoRest](https://github.com/Azure/AutoRest) toogenerate de herramientas del SDK de nuestro archivo Swagger.</span><span class="sxs-lookup"><span data-stu-id="7536b-105">We recommend using hello [AutoRest](https://github.com/Azure/AutoRest) tool toogenerate your SDK from our Swagger file.</span></span>

> [!NOTE]
> <span data-ttu-id="7536b-106">servicio de Azure Mobile Engagement Hola se retirará de 2018 de marzo y actualmente solo los clientes de tooexisting disponible.</span><span class="sxs-lookup"><span data-stu-id="7536b-106">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="7536b-107">Para más información, consulte [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="7536b-107">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="7536b-108">Hemos creado un SDK para .NET de forma similar, que le permite toointeract con estas API utilizando un contenedor de C# y no tiene toodo Hola negociación del token de autenticación y actualizar usted mismo.</span><span class="sxs-lookup"><span data-stu-id="7536b-108">We have created a .NET SDK in a similar manner which allows you toointeract with these APIs using a C# wrapper and you don't have toodo hello authentication token negotiation and refresh yourself.</span></span>  

<span data-ttu-id="7536b-109">Este ejemplo pasa por conjunto de Hola de pasos toofollow toouse Hola .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="7536b-109">This sample goes through hello set of steps toofollow toouse hello .NET SDK:</span></span>

1. <span data-ttu-id="7536b-110">En primer lugar, necesita la autenticación de hello toosetup para su API con hello Azure Active Directory tal y como se describe [aquí](mobile-engagement-api-authentication.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="7536b-110">First of all, you need toosetup hello authentication for your APIs using hello Azure Active Directory as described [here](mobile-engagement-api-authentication.md#authentication).</span></span> <span data-ttu-id="7536b-111">Al final de Hola de estos pasos, debe tener un válido **SubscriptionId**, **TenantId**, **ApplicationId** y **secreto**.</span><span class="sxs-lookup"><span data-stu-id="7536b-111">At hello end of these steps, you should have a valid **SubscriptionId**, **TenantId**, **ApplicationId** and **Secret**.</span></span> 
2. <span data-ttu-id="7536b-112">Usaremos una simple toodemonstrate de aplicación de consola de Windows funciona con hello .NET SDK con el escenario de Hola de creación de una campaña de anuncio.</span><span class="sxs-lookup"><span data-stu-id="7536b-112">We will use a simple Windows Console app toodemonstrate working with hello .NET SDK with hello scenario of creating an Announcement campaign.</span></span> <span data-ttu-id="7536b-113">Abra Visual Studio y cree una **aplicación de consola**.</span><span class="sxs-lookup"><span data-stu-id="7536b-113">So open up Visual Studio and create a **Console Application**.</span></span>   
3. <span data-ttu-id="7536b-114">A continuación deberá hello toodownload SDK de .NET que está disponible como **biblioteca de administración de Microsoft Azure Engagement** en la Galería de Nuget hello [aquí](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/).</span><span class="sxs-lookup"><span data-stu-id="7536b-114">Next you need toodownload hello .NET SDK which is available as **Microsoft Azure Engagement Management Library** in hello Nuget gallery [here](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/).</span></span>
   <span data-ttu-id="7536b-115">Si va a instalar Hola Nuget desde Visual Studio, necesita tooensure que dispone de verificación marcada hello **versión preliminar de inclusión** opción al buscar el paquete de hello:</span><span class="sxs-lookup"><span data-stu-id="7536b-115">If you are installing hello Nuget from Visual Studio, you need tooensure that you have check marked hello **Include prerelease** option while searching for hello package:</span></span>
   
    ![][1]
4. <span data-ttu-id="7536b-116">Hola `Program.cs` , agregue Hola después de los espacios de nombres:</span><span class="sxs-lookup"><span data-stu-id="7536b-116">In hello `Program.cs` file, add hello following namespaces:</span></span>
   
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Azure.Management.Engagement;
        using Microsoft.Azure.Management.Engagement.Models;
5. <span data-ttu-id="7536b-117">A continuación debe toodefine Hola después de constantes que se usará para la autenticación e interactuar con la aplicación de interacción móvil de hello en el que va a crear la campaña de anuncio Hola:</span><span class="sxs-lookup"><span data-stu-id="7536b-117">Next you need toodefine hello following constants that we will use for authentication and interacting with hello Mobile Engagement App in which you are creating hello Announcement campaign:</span></span>
   
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
6. <span data-ttu-id="7536b-118">Definir hello `EngagementManagementClient` variable que vamos a usar métodos de SDK de Mobile Engagement Hola toocall:</span><span class="sxs-lookup"><span data-stu-id="7536b-118">Define hello `EngagementManagementClient` variable which we will use toocall hello Mobile Engagement SDK methods:</span></span>
   
        static EngagementManagementClient engagementClient; 
7. <span data-ttu-id="7536b-119">Agregar Hola después tooyour `Main` método:</span><span class="sxs-lookup"><span data-stu-id="7536b-119">Add hello following tooyour `Main` method:</span></span>
   
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
8. <span data-ttu-id="7536b-120">Definir Hola siguiendo el método que se encarga de inicializar hello `EngagementManagementClient` mediante la autenticación en primer lugar y, a continuación, asociar propio con la aplicación de interacción móvil de hello en el que piensa campaña de anuncio de Hola toocreate:</span><span class="sxs-lookup"><span data-stu-id="7536b-120">Define hello following method which takes care of initializing hello `EngagementManagementClient` by first authenticating and then associating itself with hello Mobile Engagement App in which you plan toocreate hello Announcement campaign:</span></span>
   
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
   > <span data-ttu-id="7536b-121">Tenga en cuenta que debe hello toouse **nombre de recurso de aplicación** tal como se define en el portal de administración de Azure de hello para el parámetro de AppName Hola.</span><span class="sxs-lookup"><span data-stu-id="7536b-121">Note that you need toouse hello **App Resource Name** as defined in hello Azure management portal for hello AppName parameter.</span></span> 
   > 
   > 
9. <span data-ttu-id="7536b-122">Por último, definir método CreateCampaign de hello que se encargará del uso de hello inicializado anteriormente EngagementClient toocreate simple **en cualquier momento** & **solo notificación** campaña con un título y un mensaje:</span><span class="sxs-lookup"><span data-stu-id="7536b-122">Lastly, define hello CreateCampaign method which will take care of using hello previously initialized EngagementClient toocreate a simple **AnyTime** & **Notification-only** campaign with a title and message:</span></span> 
   
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
10. <span data-ttu-id="7536b-123">Aplicación de consola de ejecución hello y verá la siguiente Hola durante la creación correcta de campaña de hello:</span><span class="sxs-lookup"><span data-stu-id="7536b-123">Run hello console app and you will see hello following on successful creation of hello campaign:</span></span>
    
    <span data-ttu-id="7536b-124">**Campaign Id '159' was created successfully and it is in 'draft' state**</span><span class="sxs-lookup"><span data-stu-id="7536b-124">**Campaign Id '159' was created successfully and it is in 'draft' state**</span></span>

<!-- Images. -->

[1]: ./media/mobile-engagement-dotnet-sdk-service-api/include-prerelease.png
