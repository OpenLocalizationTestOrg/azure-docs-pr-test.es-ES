---
title: "aaaAzure Mobile Engagement - integración de back-end"
description: "Conectarse de Azure Mobile Engagement con una campaña de toocreate de back-end de SharePoint desde SharePoint"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 06297b43-579f-46e6-8a58-961a68f9aa09
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 89e1ef57db607d63c326a760b20260ad439f08b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement---api-integration"></a><span data-ttu-id="d75a3-103">Azure Mobile Engagement: Integración de la API</span><span class="sxs-lookup"><span data-stu-id="d75a3-103">Azure Mobile Engagement - API integration</span></span>
<span data-ttu-id="d75a3-104">En un sistema automatizado de marketing, crear y activar hello las campañas de marketing también se producen automáticamente.</span><span class="sxs-lookup"><span data-stu-id="d75a3-104">In an automated marketing system, creating and activating hello marketing campaigns also occur automatically.</span></span> <span data-ttu-id="d75a3-105">Con este fin, Azure Mobile Engagement permite crear estas campañas de marketing automatizadas usando las API también.</span><span class="sxs-lookup"><span data-stu-id="d75a3-105">For this purpose - Azure Mobile Engagement enables creating such automated marketing campaigns using APIs as well.</span></span> 

<span data-ttu-id="d75a3-106">Normalmente, los clientes usar Hola Mobile Engagement front-end interfaz toocreate anuncios o sondeos etcetera como parte de sus campañas de marketing.</span><span class="sxs-lookup"><span data-stu-id="d75a3-106">Typically customers use hello Mobile Engagement front end interface toocreate announcements/polls etc as part of their marketing campaigns.</span></span> <span data-ttu-id="d75a3-107">Sin embargo, como Hola se convierten en consolidada de campañas de marketing, hay una necesidad de datos de hello tooleverage bloquean en sistemas de back-end de hello (al igual que cualquier sistema CRM o el sistema CMS como SharePoint) para que se puede crear una canalización totalmente automatizada que crea las campañas de Mobile Hola flujo de datos en sistemas back-end de Hola de manera dinámica a partir de contratación.</span><span class="sxs-lookup"><span data-stu-id="d75a3-107">However as hello marketing campaigns become mature, there is a need tooleverage hello data locked in hello backend systems (like any CRM system or CMS system like SharePoint) so that a fully automated pipeline can be created which creates campaigns in Mobile Engagement dynamically based on hello data flowing in from hello backend systems.</span></span> 

![][5]

<span data-ttu-id="d75a3-108">Este tutorial va a través de un escenario donde un usuario empresarial de SharePoint rellena una lista de SharePoint con datos de marketing y un proceso automatizado recoge elementos de lista de Hola y se conecta con el uso de sistema de Mobile Engagement Hola Hola disponibles de las API de REST toocreate una campaña de marketing de datos de SharePoint de saludo.</span><span class="sxs-lookup"><span data-stu-id="d75a3-108">This tutorial goes through such a scenario where a SharePoint business user populates a SharePoint list with marketing data and an automated process picks up items from hello list and connects with hello Mobile Engagement system using hello available REST APIs toocreate a marketing campaign from hello SharePoint data.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d75a3-109">En general, puede utilizar este ejemplo como punto de partida para comprender cómo toocall cualquier API de REST de Mobile Engagement tal como se detalla Hola dos aspectos fundamentales del Hola API - parámetros de autenticación y pasando de llamada.</span><span class="sxs-lookup"><span data-stu-id="d75a3-109">In general, you can use this sample as a starting point for understanding how toocall any Mobile Engagement REST API as it details hello two key aspects of calling hello APIs - authenticating and passing parameters.</span></span> 
> 
> 

## <a name="sharepoint-integration"></a><span data-ttu-id="d75a3-110">Integración de SharePoint</span><span class="sxs-lookup"><span data-stu-id="d75a3-110">SharePoint integration</span></span>
1. <span data-ttu-id="d75a3-111">Este es el ejemplo hello SharePoint lista es similar.</span><span class="sxs-lookup"><span data-stu-id="d75a3-111">Here is what hello sample SharePoint list looks like.</span></span> <span data-ttu-id="d75a3-112">**Título**, **categoría**, **NotificationTitle**, **mensaje** y **URL** se usan para crear el anuncio de Hola.</span><span class="sxs-lookup"><span data-stu-id="d75a3-112">**Title**, **Category**, **NotificationTitle**, **Message** and **URL** are used for creating hello announcement.</span></span> <span data-ttu-id="d75a3-113">Hay una columna denominada **IsProcessed** que se usa por el proceso de automatización de ejemplo de Hola en forma de Hola de un programa de consola.</span><span class="sxs-lookup"><span data-stu-id="d75a3-113">There is a column called **IsProcessed** which is used by hello sample automation process in hello form of a console program.</span></span> <span data-ttu-id="d75a3-114">Se puede ejecutar este programa de consola como un trabajo Web de Azure para que se puede programar o puede usar directamente tooprogram creación de flujo de trabajo de SharePoint de Hola y anuncio de saludo de activación cuando se inserta un elemento en la lista de SharePoint de Hola.</span><span class="sxs-lookup"><span data-stu-id="d75a3-114">You can either run this console program as an Azure WebJob so that you can schedule it or you can directly use hello SharePoint workflow tooprogram creating and activating hello announcement when an item is inserted into hello SharePoint list.</span></span> <span data-ttu-id="d75a3-115">En este ejemplo se usa el programa de consola de Hola que pasa a través de elementos de Hola Hola SharePoint lista y crear un anuncio de Azure Mobile Engagement para cada uno de ellos y, a continuación, por último, marca hello **IsProcessed** toobe true si la marca creación de anuncio correcta.</span><span class="sxs-lookup"><span data-stu-id="d75a3-115">In this sample we use hello console program which goes through hello items in hello SharePoint list and create announcement in Azure Mobile Engagement for each of them and then finally marks hello **IsProcessed** flag toobe true on successful announcement creation.</span></span>
   
    ![][1]
2. <span data-ttu-id="d75a3-116">Estamos utilizando código de hello de ejemplo de Hola a *autenticación remota en SharePoint Online mediante Hola del modelo de objetos cliente* [aquí](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) tooauthenticate con la lista de SharePoint de Hola.</span><span class="sxs-lookup"><span data-stu-id="d75a3-116">We are using hello code from hello sample *Remote Authentication in SharePoint Online Using hello Client Object Model* [here](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) tooauthenticate with hello SharePoint list.</span></span>
3. <span data-ttu-id="d75a3-117">Una vez autenticado, realizamos un bucle a través de toofind de elementos de lista Hola a todos los elementos recién creados (que tendrán **IsProcessed** = false).</span><span class="sxs-lookup"><span data-stu-id="d75a3-117">Once authenticated, we loop through hello list items toofind out any newly created items (which will have **IsProcessed** = false).</span></span> 
   
         static async void CreateCampaignFromSharepoint()
        {
            using (ClientContext clientContext = ClaimClientContext.GetAuthenticatedContext(targetSharepointSite))
            {
                // Using https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c for authentication     
                Web site = clientContext.Web;
                List list = site.Lists.GetByTitle("VideoContent");
                CamlQuery query = new CamlQuery();
                query.ViewXml = "<View/>";
                ListItemCollection items = list.GetItems(query);
   
                // Load hello SharePoint list
                clientContext.Load(list);
                clientContext.Load(items);
                clientContext.ExecuteQuery();
   
                // Loop through hello list toogo through all hello items which are newly added
                foreach (ListItem item in items)
                    if (item["IsProcessed"].ToString() != "Yes")
                    {
                        string name = item["Title"].ToString();
                        string notificationTitle = item["NotificationTitle"].ToString();
                        string notificationMessage = item["Message"].ToString();
                        string category = item["Category"].ToString();
                        string actionURL = ((FieldUrlValue)item["URL"]).Url;
   
                        // Send an HTTP request toocreate AzME campaign
                        int campaignId = CreateAzMECampaign
                            (name, notificationTitle, notificationMessage, category, actionURL).Result;
   
                        if (campaignId != -1)
                        {
                            // If creating campaign is successful then set this tootrue
                            item["IsProcessed"] = "Yes";
   
                            // Now try tooactivate hello campaign also
                            await ActivateAzMECampaign(campaignId);
                        }
                        else
                        {
                            item["IsProcessed"] = "Error";
                        }
                        item.Update();
                    }
                clientContext.ExecuteQuery();
            }
        }

## <a name="mobile-engagement-integration"></a><span data-ttu-id="d75a3-118">Integración de Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="d75a3-118">Mobile Engagement integration</span></span>
1. <span data-ttu-id="d75a3-119">Una vez que se encuentra un elemento que requiere procesamiento: extraer información de hello necesaria toocreate un anuncio de Hola de elemento de lista y llamar a `CreateAzMECampaign` toocreate y posteriormente `ActivateAzMECampaign` tooactivate lo.</span><span class="sxs-lookup"><span data-stu-id="d75a3-119">Once we find an item which requires processing - we extract hello information required toocreate an announcement from hello list item and call `CreateAzMECampaign` toocreate it and subsequently `ActivateAzMECampaign` tooactivate it.</span></span> <span data-ttu-id="d75a3-120">Estos son básicamente las llamadas de API de REST al llamar a toohello backend de interacción móvil.</span><span class="sxs-lookup"><span data-stu-id="d75a3-120">These are essentially REST API calls calling toohello Mobile Engagement backend.</span></span> 
2. <span data-ttu-id="d75a3-121">requerir Hello las API de REST de Mobile Engagement un **encabezado de autorización HTTP del esquema de autenticación básica** que se compone de hello `ApplicationId` hello y `ApiKey` que obtendrá de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="d75a3-121">hello Mobile Engagement REST APIs require a **Basic auth scheme authorization HTTP header** which is composed of hello `ApplicationId` and hello `ApiKey` which you get from hello Azure portal.</span></span> <span data-ttu-id="d75a3-122">Asegúrese de que está usando Hola clave de hello **claves api** sección y *no* de hello **sdk claves** sección.</span><span class="sxs-lookup"><span data-stu-id="d75a3-122">Make sure that you are using hello Key from hello **api keys** section and *not* from hello **sdk keys** section.</span></span> 
   
   ![][2]
   
       static string CreateAuthZHeader()
       {
           string BasicAuthzHeaderString = "Basic " + EncodeTo64(ApplicationId + ":" + ApiKey);
           return BasicAuthzHeaderString;
       }
   
       static public string EncodeTo64(string toEncode)
       {
           byte[] toEncodeAsBytes = System.Text.ASCIIEncoding.ASCII.GetBytes(toEncode);
           string returnValue = System.Convert.ToBase64String(toEncodeAsBytes);
           return returnValue;
       }  
3. <span data-ttu-id="d75a3-123">Para crear el tipo de anuncio Hola de campaña: consulte toohello [documentación](https://msdn.microsoft.com/library/azure/mt683750.aspx).</span><span class="sxs-lookup"><span data-stu-id="d75a3-123">For creating hello announcement type campaign - refer toohello [documentation](https://msdn.microsoft.com/library/azure/mt683750.aspx).</span></span> <span data-ttu-id="d75a3-124">Necesita toomake seguro de que está especificando campaña hello `kind` como *anuncio* hello y [carga](https://msdn.microsoft.com/library/azure/mt683751.aspx) y pasarlo como FormUrlEncodedContent.</span><span class="sxs-lookup"><span data-stu-id="d75a3-124">You need toomake sure that you are specifying hello campaign `kind` as *announcement* and hello [payload](https://msdn.microsoft.com/library/azure/mt683751.aspx) and passing it as FormUrlEncodedContent.</span></span> 
   
        static async Task<int> CreateAzMECampaign(string campaignName, string notificationTitle, 
            string notificationMessage, string notificationCategory, string actionURL)
        {
            string createURIFragment = "/reach/1/create";
   
            using (var client = new HttpClient())
            {
                // Add Authorization Header
                client.DefaultRequestHeaders.TryAddWithoutValidation("Authorization", CreateAuthZHeader());
   
                // Create hello payload toosend hello content
                // Reference -> https://msdn.microsoft.com/library/dn913749.aspx
                string data =
                    @"{""name"":""" + campaignName + @"""," + 
                    @"""type"":""only_notif""," + 
                    @"""deliveryTime"":""any"","" + 
                    @""notificationTitle"":""" + notificationTitle + 
                    @""",""notificationMessage"":""" + notificationMessage + 
                    @""",""actionUrl"":""" + actionURL + @"""}";
   
                var content = new FormUrlEncodedContent(new[] 
                {
                    new KeyValuePair<string, string>("kind", "announcement"),
                    new KeyValuePair<string, string>("data", data),
                });
   
                // Send hello POST request
                var response = await client.PostAsync(url + createURIFragment, content);
                var responseString = response.Content.ReadAsStringAsync().Result;
                int campaignId = -1;
                if (response.StatusCode.ToString() == "OK")
                {
                    // This is hello campaign id
                    campaignId = Convert.ToInt32(responseString);
                    Console.WriteLine("Campaign successfully created with id {0}", campaignId);
                }
                else
                {
                    Console.WriteLine("Campaign creation failed with error - '{0}'", responseString);
                }
                return campaignId;
            }
        }
4. <span data-ttu-id="d75a3-125">Una vez haya creado de anuncio de Hola, verá algo parecido a Hola siguientes en el portal de interacción móvil hello (tenga en cuenta que Hola estado = borrador y activada = n /)</span><span class="sxs-lookup"><span data-stu-id="d75a3-125">Once you have hello announcement created, you will see something like hello following on hello Mobile Engagement portal (note that hello State=Draft and Activated = N/A)</span></span>
   
    ![][3]
5. <span data-ttu-id="d75a3-126">`CreateAzMECampaign`crea una campaña de anuncio y devuelve su llamador toohello de identificador.</span><span class="sxs-lookup"><span data-stu-id="d75a3-126">`CreateAzMECampaign` creates an announcement campaign and returns its Id toohello caller.</span></span> <span data-ttu-id="d75a3-127">`ActivateAzMECampaign`necesita este identificador como campaña de hello parámetro tooactivate Hola.</span><span class="sxs-lookup"><span data-stu-id="d75a3-127">`ActivateAzMECampaign` requires this Id as hello parameter tooactivate hello campaign.</span></span> 
   
        static async Task<bool> ActivateAzMECampaign(int campaignId)
        {
            string activateUriFragment = "/reach/1/activate";
            using (var client = new HttpClient())
            {
                // Add Authorization Header
                client.DefaultRequestHeaders.TryAddWithoutValidation("Authorization", CreateAuthZHeader());
   
                var content = new FormUrlEncodedContent(new[] 
                {
                    new KeyValuePair<string, string>("kind", "announcement"),
                    new KeyValuePair<string, string>("id", campaignId.ToString()),
                });
   
                // Send hello POST request
                var response = await client.PostAsync(url + activateUriFragment, content);
                var responseString = response.Content.ReadAsStringAsync().Result;
                if (response.StatusCode.ToString() == "OK")
                {
                    Console.WriteLine("Campaign successfully activated");
                    return true;
                }
                else
                {
                    Console.WriteLine("Campaign activation failed with error - '{0}'", responseString);
                    return false;
                }
            }
        }
6. <span data-ttu-id="d75a3-128">Una vez que tenga activado el anuncio de Hola, verá algo parecido a Hola siguiente en el portal de interacción móvil de hello:</span><span class="sxs-lookup"><span data-stu-id="d75a3-128">Once you have hello announcement activated, you will see something like hello following on hello Mobile Engagement portal:</span></span>
   
    ![][4]
7. <span data-ttu-id="d75a3-129">En cuanto se activará la campaña de hello, los dispositivos que cumplen el criterio de hello en campaña Hola empezará a ver las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="d75a3-129">As soon as hello campaign gets activated, any devices which satisfy hello criterion on hello campaign will start seeing notifications.</span></span> 
8. <span data-ttu-id="d75a3-130">También observará que ese elemento de lista Hola marcado con IsProcessed = false se estableció tooTrue una vez creada la campaña de anuncio Hola.</span><span class="sxs-lookup"><span data-stu-id="d75a3-130">You will also notice that hello list item marked with IsProcessed = false has been set tooTrue once hello announcement campaign is created.</span></span>  

<span data-ttu-id="d75a3-131">Este ejemplo crea una campaña de anuncio simple especificación de propiedades de hello necesario principalmente.</span><span class="sxs-lookup"><span data-stu-id="d75a3-131">This sample created a simple announcement campaign specifying mostly hello required properties.</span></span> <span data-ttu-id="d75a3-132">Puede personalizar tanto como posible desde el portal de hello con información de hello [aquí](https://msdn.microsoft.com/library/azure/mt683751.aspx).</span><span class="sxs-lookup"><span data-stu-id="d75a3-132">You can customize this as much as you can from hello portal by using hello information [here](https://msdn.microsoft.com/library/azure/mt683751.aspx).</span></span> 

<!-- Images. -->
[1]: ./media/mobile-engagement-sample-backend-integration-sharepoint/sharepointlist.png
[2]: ./media/mobile-engagement-sample-backend-integration-sharepoint/properties.png
[3]: ./media/mobile-engagement-sample-backend-integration-sharepoint/new-announcement.png
[4]: ./media/mobile-engagement-sample-backend-integration-sharepoint/activate-announcement.png
[5]: ./media/mobile-engagement-sample-backend-integration-sharepoint/diagram.png



