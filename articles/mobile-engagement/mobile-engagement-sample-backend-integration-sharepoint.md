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
# <a name="azure-mobile-engagement---api-integration"></a>Azure Mobile Engagement: Integración de la API
En un sistema automatizado de marketing, crear y activar hello las campañas de marketing también se producen automáticamente. Con este fin, Azure Mobile Engagement permite crear estas campañas de marketing automatizadas usando las API también. 

Normalmente, los clientes usar Hola Mobile Engagement front-end interfaz toocreate anuncios o sondeos etcetera como parte de sus campañas de marketing. Sin embargo, como Hola se convierten en consolidada de campañas de marketing, hay una necesidad de datos de hello tooleverage bloquean en sistemas de back-end de hello (al igual que cualquier sistema CRM o el sistema CMS como SharePoint) para que se puede crear una canalización totalmente automatizada que crea las campañas de Mobile Hola flujo de datos en sistemas back-end de Hola de manera dinámica a partir de contratación. 

![][5]

Este tutorial va a través de un escenario donde un usuario empresarial de SharePoint rellena una lista de SharePoint con datos de marketing y un proceso automatizado recoge elementos de lista de Hola y se conecta con el uso de sistema de Mobile Engagement Hola Hola disponibles de las API de REST toocreate una campaña de marketing de datos de SharePoint de saludo. 

> [!IMPORTANT]
> En general, puede utilizar este ejemplo como punto de partida para comprender cómo toocall cualquier API de REST de Mobile Engagement tal como se detalla Hola dos aspectos fundamentales del Hola API - parámetros de autenticación y pasando de llamada. 
> 
> 

## <a name="sharepoint-integration"></a>Integración de SharePoint
1. Este es el ejemplo hello SharePoint lista es similar. **Título**, **categoría**, **NotificationTitle**, **mensaje** y **URL** se usan para crear el anuncio de Hola. Hay una columna denominada **IsProcessed** que se usa por el proceso de automatización de ejemplo de Hola en forma de Hola de un programa de consola. Se puede ejecutar este programa de consola como un trabajo Web de Azure para que se puede programar o puede usar directamente tooprogram creación de flujo de trabajo de SharePoint de Hola y anuncio de saludo de activación cuando se inserta un elemento en la lista de SharePoint de Hola. En este ejemplo se usa el programa de consola de Hola que pasa a través de elementos de Hola Hola SharePoint lista y crear un anuncio de Azure Mobile Engagement para cada uno de ellos y, a continuación, por último, marca hello **IsProcessed** toobe true si la marca creación de anuncio correcta.
   
    ![][1]
2. Estamos utilizando código de hello de ejemplo de Hola a *autenticación remota en SharePoint Online mediante Hola del modelo de objetos cliente* [aquí](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) tooauthenticate con la lista de SharePoint de Hola.
3. Una vez autenticado, realizamos un bucle a través de toofind de elementos de lista Hola a todos los elementos recién creados (que tendrán **IsProcessed** = false). 
   
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

## <a name="mobile-engagement-integration"></a>Integración de Mobile Engagement
1. Una vez que se encuentra un elemento que requiere procesamiento: extraer información de hello necesaria toocreate un anuncio de Hola de elemento de lista y llamar a `CreateAzMECampaign` toocreate y posteriormente `ActivateAzMECampaign` tooactivate lo. Estos son básicamente las llamadas de API de REST al llamar a toohello backend de interacción móvil. 
2. requerir Hello las API de REST de Mobile Engagement un **encabezado de autorización HTTP del esquema de autenticación básica** que se compone de hello `ApplicationId` hello y `ApiKey` que obtendrá de hello portal de Azure. Asegúrese de que está usando Hola clave de hello **claves api** sección y *no* de hello **sdk claves** sección. 
   
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
3. Para crear el tipo de anuncio Hola de campaña: consulte toohello [documentación](https://msdn.microsoft.com/library/azure/mt683750.aspx). Necesita toomake seguro de que está especificando campaña hello `kind` como *anuncio* hello y [carga](https://msdn.microsoft.com/library/azure/mt683751.aspx) y pasarlo como FormUrlEncodedContent. 
   
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
4. Una vez haya creado de anuncio de Hola, verá algo parecido a Hola siguientes en el portal de interacción móvil hello (tenga en cuenta que Hola estado = borrador y activada = n /)
   
    ![][3]
5. `CreateAzMECampaign`crea una campaña de anuncio y devuelve su llamador toohello de identificador. `ActivateAzMECampaign`necesita este identificador como campaña de hello parámetro tooactivate Hola. 
   
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
6. Una vez que tenga activado el anuncio de Hola, verá algo parecido a Hola siguiente en el portal de interacción móvil de hello:
   
    ![][4]
7. En cuanto se activará la campaña de hello, los dispositivos que cumplen el criterio de hello en campaña Hola empezará a ver las notificaciones. 
8. También observará que ese elemento de lista Hola marcado con IsProcessed = false se estableció tooTrue una vez creada la campaña de anuncio Hola.  

Este ejemplo crea una campaña de anuncio simple especificación de propiedades de hello necesario principalmente. Puede personalizar tanto como posible desde el portal de hello con información de hello [aquí](https://msdn.microsoft.com/library/azure/mt683751.aspx). 

<!-- Images. -->
[1]: ./media/mobile-engagement-sample-backend-integration-sharepoint/sharepointlist.png
[2]: ./media/mobile-engagement-sample-backend-integration-sharepoint/properties.png
[3]: ./media/mobile-engagement-sample-backend-integration-sharepoint/new-announcement.png
[4]: ./media/mobile-engagement-sample-backend-integration-sharepoint/activate-announcement.png
[5]: ./media/mobile-engagement-sample-backend-integration-sharepoint/diagram.png



