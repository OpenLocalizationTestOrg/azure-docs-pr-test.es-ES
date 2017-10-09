---
title: "llamadas de aaaTrace con el Inspector de API - Administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo llamadas tootrace utilizando Hola Inspector de API de administración de API de Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 4b222327-c8a4-4f33-9a06-adff2a9834d9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: b0c401caa8da1b789f6cfe5edf97a5f118d78f26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-api-inspector-tootrace-calls-in-azure-api-management"></a><span data-ttu-id="f99b4-103">Cómo llama a toouse hello tootrace API Inspector de administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="f99b4-103">How toouse hello API Inspector tootrace calls in Azure API Management</span></span>
<span data-ttu-id="f99b4-104">Administración de API proporciona un API Inspector toohelp de herramienta de depuración y solución de problemas de las API.</span><span class="sxs-lookup"><span data-stu-id="f99b4-104">API Management provides an API Inspector tool toohelp you with debugging and troubleshooting your APIs.</span></span> <span data-ttu-id="f99b4-105">Hola API Inspector pueden usarse mediante programación y también puede utilizarse directamente desde el portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="f99b4-105">hello API Inspector can be used programmatically and can also be used directly from hello developer portal.</span></span> 

<span data-ttu-id="f99b4-106">Además tootracing operaciones, API Inspector también realiza un seguimiento de [expresión de directiva](https://msdn.microsoft.com/library/azure/dn910913.aspx) evaluaciones.</span><span class="sxs-lookup"><span data-stu-id="f99b4-106">In addition tootracing operations, API Inspector also traces [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx) evaluations.</span></span> <span data-ttu-id="f99b4-107">Para ver una demostración, vea [177 episodio abarcan de nube: más características de administración de API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) y avancemos too21:00.</span><span class="sxs-lookup"><span data-stu-id="f99b4-107">For a demonstration, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too21:00.</span></span>

<span data-ttu-id="f99b4-108">En esta guía se explica el uso del API Inspector.</span><span class="sxs-lookup"><span data-stu-id="f99b4-108">This guide provides a walk-through of using API Inspector.</span></span>

> [!NOTE]
> <span data-ttu-id="f99b4-109">Seguimientos de API Inspector solo se genera y están disponibles para las solicitudes que contiene las claves de la suscripción que pertenecen toohello [administrador](api-management-howto-create-groups.md) cuenta.</span><span class="sxs-lookup"><span data-stu-id="f99b4-109">API Inspector traces are only generated and made available for requests containing subscription keys that belong toohello [administrator](api-management-howto-create-groups.md) account.</span></span>
> 
> 

## <span data-ttu-id="f99b4-110"><a name="trace-call"></a> Tootrace una llamada de Inspector de API de uso</span><span class="sxs-lookup"><span data-stu-id="f99b4-110"><a name="trace-call"> </a> Use API Inspector tootrace a call</span></span>
<span data-ttu-id="f99b4-111">Agregar toouse API Inspector, un **ocp-apim-trace: true** solicitud de llamada de la operación de tooyour de encabezado y, a continuación, descargar e inspeccionar el seguimiento de hello mediante dirección URL de hello indicado por hello **ocp apim seguimiento ubicación** encabezado de respuesta.</span><span class="sxs-lookup"><span data-stu-id="f99b4-111">toouse API Inspector, add an **ocp-apim-trace: true** request header tooyour operation call, and then download and inspect hello trace using hello URL indicated by hello **ocp-apim-trace-location** response header.</span></span> <span data-ttu-id="f99b4-112">Esto puede hacerse mediante programación y permite llevar a cabo directamente desde el portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="f99b4-112">This can be done programatically, and can also be done directly from hello developer portal.</span></span>

<span data-ttu-id="f99b4-113">Este tutorial muestra cómo toouse Hola API Inspector tootrace las operaciones con Hola API calculadora básica que se configura en hello [administrar su primera API](api-management-get-started.md) tutorial de introducción.</span><span class="sxs-lookup"><span data-stu-id="f99b4-113">This tutorial shows how toouse hello API Inspector tootrace operations using hello Basic Calculator API that is configured in hello [Manage your first API](api-management-get-started.md) getting started tutorial.</span></span> <span data-ttu-id="f99b4-114">Si no se han completado este tutorial sólo tarda unos instantes tooimport Hola API calculadora básica, o puede usar otra API de su elección, como la API de eco hello.</span><span class="sxs-lookup"><span data-stu-id="f99b4-114">If you haven't completed that tutorial it only takes a few moments tooimport hello Basic Calculator API, or you can use another API of your choosing such as hello Echo API.</span></span> <span data-ttu-id="f99b4-115">Cada instancia de servicio de administración de API viene preconfigurado con una API de eco que se pueden tooexperiment usado con y obtener información acerca de la API de administración.</span><span class="sxs-lookup"><span data-stu-id="f99b4-115">Each API Management service instance comes pre-configured with an Echo API that can be used tooexperiment with and learn about API Management.</span></span> <span data-ttu-id="f99b4-116">API de eco Hello devuelve cualquier entrada se envía tooit.</span><span class="sxs-lookup"><span data-stu-id="f99b4-116">hello Echo API returns back whatever input is sent tooit.</span></span> <span data-ttu-id="f99b4-117">toouse, puede invocar cualquier verbo HTTP y valor devuelto de hello simplemente será lo que envía.</span><span class="sxs-lookup"><span data-stu-id="f99b4-117">toouse it, you can invoke any HTTP verb, and hello return value will simply be what you sent.</span></span> 

<span data-ttu-id="f99b4-118">tooget iniciado, haga clic en **portal para desarrolladores de** Hola Portal de Azure para el servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="f99b4-118">tooget started, click **Developer portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="f99b4-119">Las operaciones pueden llamarse directamente desde el portal para desarrolladores de Hola que proporciona una manera cómoda de tooview y pruebe las operaciones de Hola de una API.</span><span class="sxs-lookup"><span data-stu-id="f99b4-119">Operations can be called directly from hello developer portal which provides a convenient way tooview and test hello operations of an API.</span></span>

> <span data-ttu-id="f99b4-120">Si aún no ha creado una instancia de servicio de administración de API, consulte [crear una instancia de servicio de administración de API] [ Create an API Management service instance] en hello [Introducción a administración de API de Azure] [ Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="f99b4-120">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

![API Management developer portal][api-management-developer-portal-menu]

<span data-ttu-id="f99b4-122">Haga clic en **API** desde el menú superior de hello y, a continuación, haga clic en **calculadora básica**.</span><span class="sxs-lookup"><span data-stu-id="f99b4-122">Click **APIs** from hello top menu, and then click **Basic Calculator**.</span></span>

![API eco][api-management-api]

<span data-ttu-id="f99b4-124">Haga clic en **Pruébelo** tootry hello **agrega dos enteros** operación.</span><span class="sxs-lookup"><span data-stu-id="f99b4-124">Click **Try it** tootry hello **Add two integers** operation.</span></span>

![Pruébelo][api-management-open-console]

<span data-ttu-id="f99b4-126">Mantener valores de parámetros predeterminados de Hola y clave de suscripción Hola seleccione producto Hola desea toouse de hello **clave de suscripción** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="f99b4-126">Keep hello default parameter values, and select hello subscription key for hello product you want toouse from hello **subscription-key** drop-down.</span></span>

<span data-ttu-id="f99b4-127">De forma predeterminada en Hola Hola de portal para desarrolladores **Ocp-Apim-Trace** encabezado ya está establecido demasiado**true**.</span><span class="sxs-lookup"><span data-stu-id="f99b4-127">By default in hello developer portal hello **Ocp-Apim-Trace** header is already set too**true**.</span></span> <span data-ttu-id="f99b4-128">Este encabezado configura si se ha generado o no un seguimiento.</span><span class="sxs-lookup"><span data-stu-id="f99b4-128">This header configures whether or not a trace is generated.</span></span>

![Los métodos Send][api-management-http-get]

<span data-ttu-id="f99b4-130">Haga clic en **enviar** operación de hello tooinvoke.</span><span class="sxs-lookup"><span data-stu-id="f99b4-130">Click **Send** tooinvoke hello operation.</span></span>

![Los métodos Send][api-management-send-results]

<span data-ttu-id="f99b4-132">En la respuesta de hello encabezados será un **ocp apim seguimiento ubicación** con un toohello similar valor siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="f99b4-132">In hello response headers will be an **ocp-apim-trace-location** with a value similar toohello following example.</span></span>

```
ocp-apim-trace-location : https://contosoltdxw7zagdfsprykd.blob.core.windows.net/apiinspectorcontainer/ZW3e23NsW4wQyS-SHjS0Og2-2?sv=2013-08-15&sr=b&sig=Mgx7cMHsLmVDv%2B%2BSzvg3JR8qGTHoOyIAV7xDsZbF7%2Bk%3D&se=2014-05-04T21%3A00%3A13Z&sp=r&verify_guid=a56a17d83de04fcb8b9766df38514742
```

<span data-ttu-id="f99b4-133">seguimiento de Hello puede descargarse desde Hola ubicación especificada y revisado como se muestra en el paso siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="f99b4-133">hello trace can be downloaded from hello specified location and reviewed as demonstrated in hello next step.</span></span> <span data-ttu-id="f99b4-134">Tenga en cuenta que solo Hola última 100 entradas del registro se almacenan y se reutilizan ubicaciones del registro de rotación.</span><span class="sxs-lookup"><span data-stu-id="f99b4-134">Note that only hello last 100 log entries are stored and log locations are reused in rotation.</span></span> <span data-ttu-id="f99b4-135">Por tanto, si realiza más de 100 llamadas con el seguimiento habilitado se iniciarán finalmente seguimientos primera hello en lugar de sobrescribir.</span><span class="sxs-lookup"><span data-stu-id="f99b4-135">So if you make more than 100 calls with tracing enabled you will eventually start overwriting hello first traces in place.</span></span>

## <span data-ttu-id="f99b4-136"><a name="inspect-trace"></a>Inspeccionar seguimiento Hola</span><span class="sxs-lookup"><span data-stu-id="f99b4-136"><a name="inspect-trace"> </a>Inspect hello trace</span></span>
<span data-ttu-id="f99b4-137">valores de hello tooreview en seguimiento de hello, descargue el archivo de seguimiento de Hola de Hola **ocp apim seguimiento ubicación** dirección URL.</span><span class="sxs-lookup"><span data-stu-id="f99b4-137">tooreview hello values in hello trace, download hello trace file from hello **ocp-apim-trace-location** URL.</span></span> <span data-ttu-id="f99b4-138">Es un archivo de texto en formato JSON y contiene entradas toohello similar siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="f99b4-138">It is a text file in JSON format, and contains entries similar toohello following example.</span></span>

```json
{
    "traceId": "abcd8ea63d134c1fabe6371566c7cbea",
    "traceEntries": {
        "inbound": [
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.2998610Z",
                "elapsed": "00:00:00.0725926",
                "data": {
                    "request": {
                        "method": "GET",
                        "url": "https://contoso5.azure-api.net/calc/add?a=51&b=49",
                        "headers": [
                            {
                                "name": "Ocp-Apim-Subscription-Key",
                                "value": "5d7c41af64a44a68a2ea46580d271a59"
                            },
                            {
                                "name": "Connection",
                                "value": "Keep-Alive"
                            },
                            {
                                "name": "Host",
                                "value": "contoso5.azure-api.net"
                            }
                        ]
                    }
                }
            },
            {
                "source": "mapper",
                "timestamp": "2015-06-23T19:51:35.2998610Z",
                "elapsed": "00:00:00.0726213",
                "data": {
                    "configuration": {
                        "api": {
                            "from": "/calc",
                            "to": {
                                "scheme": "http",
                                "host": "calcapi.cloudapp.net",
                                "port": 80,
                                "path": "/api",
                                "queryString": "",
                                "query": {},
                                "isDefaultPort": true
                            }
                        },
                        "operation": {
                            "method": "GET",
                            "uriTemplate": "/add?a={a}&b={b}"
                        },
                        "user": {
                            "id": 1,
                            "groups": [
                                "Administrators",
                                "Developers"
                            ]
                        },
                        "product": {
                            "id": 1
                        }
                    }
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.2998610Z",
                "elapsed": "00:00:00.0727522",
                "data": {
                    "message": "Request is being forwarded toohello backend service.",
                    "request": {
                        "method": "GET",
                        "url": "http://calcapi.cloudapp.net/api/add?a=51&b=49",
                        "headers": [
                            {
                                "name": "Ocp-Apim-Subscription-Key",
                                "value": "5d7c41af64a44a68a2ea46580d271a59"
                            },
                            {
                                "name": "X-Forwarded-For",
                                "value": "33.52.215.35"
                            }
                        ]
                    }
                }
            }
        ],
        "outbound": [
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1960601",
                "data": {
                    "response": {
                        "status": {
                            "code": 200,
                            "reason": "OK"
                        },
                        "headers": [
                            {
                                "name": "Pragma",
                                "value": "no-cache"
                            },
                            {
                                "name": "Content-Length",
                                "value": "124"
                            },
                            {
                                "name": "Cache-Control",
                                "value": "no-cache"
                            },
                            {
                                "name": "Content-Type",
                                "value": "application/xml; charset=utf-8"
                            },
                            {
                                "name": "Date",
                                "value": "Tue, 23 Jun 2015 19:51:35 GMT"
                            },
                            {
                                "name": "Expires",
                                "value": "-1"
                            },
                            {
                                "name": "Server",
                                "value": "Microsoft-IIS/8.5"
                            },
                            {
                                "name": "X-AspNet-Version",
                                "value": "4.0.30319"
                            },
                            {
                                "name": "X-Powered-By",
                                "value": "ASP.NET"
                            }
                        ]
                    }
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1961112",
                "data": {
                    "message": "Response headers have been sent toohello caller. Starting toostream hello response body."
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1963155",
                "data": {
                    "message": "Response body streaming toohello caller is complete."
                }
            }
        ]
    }
}
```

## <span data-ttu-id="f99b4-139"><a name="next-steps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f99b4-139"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="f99b4-140">Vea una demostración del seguimiento de expresiones de directivas en [Cloud Cover Episodio 177: Más características de administración de API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span><span class="sxs-lookup"><span data-stu-id="f99b4-140">Watch a demo of tracing policy expressions in [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span></span> <span data-ttu-id="f99b4-141">Demostración de avance rápido too21:00 toosee Hola.</span><span class="sxs-lookup"><span data-stu-id="f99b4-141">Fast-forward too21:00 toosee hello demo.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Cloud+Cover/Episode-177-More-API-Management-Features-with-Vlad-Vinogradsky/player]
> 
> 

[Use API Inspector tootrace a call]: #trace-call
[Inspect hello trace]: #inspect-trace
[Next steps]: #next-steps

[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Azure Classic Portal]: https://manage.windowsazure.com/


[api-management-developer-portal-menu]: ./media/api-management-howto-api-inspector/api-management-developer-portal-menu.png
[api-management-api]: ./media/api-management-howto-api-inspector/api-management-api.png
[api-management-echo-api-get]: ./media/api-management-howto-api-inspector/api-management-echo-api-get.png
[api-management-developer-key]: ./media/api-management-howto-api-inspector/api-management-developer-key.png
[api-management-open-console]: ./media/api-management-howto-api-inspector/api-management-open-console.png
[api-management-http-get]: ./media/api-management-howto-api-inspector/api-management-http-get.png
[api-management-send-results]: ./media/api-management-howto-api-inspector/api-management-send-results.png




