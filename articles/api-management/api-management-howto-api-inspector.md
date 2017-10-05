---
title: 'Seguimiento de llamadas con API Inspector: Azure API Management | Microsoft Docs'
description: "Obtenga información acerca de cómo realizar un seguimiento de las llamadas con API Inspector en Administración de API de Azure."
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
ms.openlocfilehash: a9d4d3be7f046af975f6dc25670070204848588c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-api-inspector-to-trace-calls-in-azure-api-management"></a><span data-ttu-id="50a89-103">Uso del API Inspector para hacer un seguimiento de las llamadas en Administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="50a89-103">How to use the API Inspector to trace calls in Azure API Management</span></span>
<span data-ttu-id="50a89-104">Administración de API ofrece la herramienta API Inspector para ayudarle con la depuración y la solución de problemas de las API.</span><span class="sxs-lookup"><span data-stu-id="50a89-104">API Management provides an API Inspector tool to help you with debugging and troubleshooting your APIs.</span></span> <span data-ttu-id="50a89-105">El API Inspector se puede usar mediante programación y también directamente desde el portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="50a89-105">The API Inspector can be used programmatically and can also be used directly from the developer portal.</span></span> 

<span data-ttu-id="50a89-106">Además de las operaciones de seguimiento, API Inspector también realiza el seguimiento de evaluaciones de [expresiones de directivas](https://msdn.microsoft.com/library/azure/dn910913.aspx) .</span><span class="sxs-lookup"><span data-stu-id="50a89-106">In addition to tracing operations, API Inspector also traces [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx) evaluations.</span></span> <span data-ttu-id="50a89-107">Para obtener una demostración, consulte [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) y avance rápidamente hasta el minuto 21:00.</span><span class="sxs-lookup"><span data-stu-id="50a89-107">For a demonstration, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 21:00.</span></span>

<span data-ttu-id="50a89-108">En esta guía se explica el uso del API Inspector.</span><span class="sxs-lookup"><span data-stu-id="50a89-108">This guide provides a walk-through of using API Inspector.</span></span>

> [!NOTE]
> <span data-ttu-id="50a89-109">Los seguimientos de API Inspector solo se generan y están disponibles para las solicitudes que contiene claves de suscripción que pertenecen a la cuenta de [administrador](api-management-howto-create-groups.md) .</span><span class="sxs-lookup"><span data-stu-id="50a89-109">API Inspector traces are only generated and made available for requests containing subscription keys that belong to the [administrator](api-management-howto-create-groups.md) account.</span></span>
> 
> 

## <span data-ttu-id="50a89-110"><a name="trace-call"> </a> Uso de API Inspector para realizar el seguimiento de una llamada</span><span class="sxs-lookup"><span data-stu-id="50a89-110"><a name="trace-call"> </a> Use API Inspector to trace a call</span></span>
<span data-ttu-id="50a89-111">Para usar API Inspector, agregue un encabezado de solicitud **ocp-apim-trace: true** a la llamada a la operación y luego descargue e inspeccione el seguimiento con la URL indicada mediante el encabezado de respuesta **ocp-apim-trace-location**.</span><span class="sxs-lookup"><span data-stu-id="50a89-111">To use API Inspector, add an **ocp-apim-trace: true** request header to your operation call, and then download and inspect the trace using the URL indicated by the **ocp-apim-trace-location** response header.</span></span> <span data-ttu-id="50a89-112">Esto puede realizarse mediante programación y también directamente desde el portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="50a89-112">This can be done programatically, and can also be done directly from the developer portal.</span></span>

<span data-ttu-id="50a89-113">Este tutorial muestra cómo utilizar el API Inspector para realizar un seguimiento de las operaciones mediante la API de calculadora básica que se configura en el tutorial de introducción [Administrar su primera API](api-management-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="50a89-113">This tutorial shows how to use the API Inspector to trace operations using the Basic Calculator API that is configured in the [Manage your first API](api-management-get-started.md) getting started tutorial.</span></span> <span data-ttu-id="50a89-114">Si no ha realizado ese tutorial, solo tardará unos minutos en importar la API de calculadora básica, o puede usar otra API de su elección, como la Echo API.</span><span class="sxs-lookup"><span data-stu-id="50a89-114">If you haven't completed that tutorial it only takes a few moments to import the Basic Calculator API, or you can use another API of your choosing such as the Echo API.</span></span> <span data-ttu-id="50a89-115">Cada instancia del servicio Administración de API viene previamente configurada con una API Eco que se puede usar para experimentar con Administración de API y aprender de esta.</span><span class="sxs-lookup"><span data-stu-id="50a89-115">Each API Management service instance comes pre-configured with an Echo API that can be used to experiment with and learn about API Management.</span></span> <span data-ttu-id="50a89-116">La Echo API devuelve cualquier entrada que se le envíe.</span><span class="sxs-lookup"><span data-stu-id="50a89-116">The Echo API returns back whatever input is sent to it.</span></span> <span data-ttu-id="50a89-117">Para usarla, se puede invocar cualquier verbo HTTP, y el valor devuelto será simplemente el que se envíe.</span><span class="sxs-lookup"><span data-stu-id="50a89-117">To use it, you can invoke any HTTP verb, and the return value will simply be what you sent.</span></span> 

<span data-ttu-id="50a89-118">Para comenzar, haga clic en **Portal para desarrolladores** en Azure Portal para el servicio API Management.</span><span class="sxs-lookup"><span data-stu-id="50a89-118">To get started, click **Developer portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="50a89-119">Se puede llamar a las operaciones directamente desde el portal para desarrolladores, lo que proporciona una forma cómoda de ver y probar las operaciones de una API.</span><span class="sxs-lookup"><span data-stu-id="50a89-119">Operations can be called directly from the developer portal which provides a convenient way to view and test the operations of an API.</span></span>

> <span data-ttu-id="50a89-120">Si todavía no ha creado una instancia del servicio API Management, consulte [Creación de una instancia del servicio API Management][Create an API Management service instance] en el tutorial de [introducción a Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="50a89-120">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

![API Management developer portal][api-management-developer-portal-menu]

<span data-ttu-id="50a89-122">Haga clic en **API** en el menú superior y después en **Calculadora básica**.</span><span class="sxs-lookup"><span data-stu-id="50a89-122">Click **APIs** from the top menu, and then click **Basic Calculator**.</span></span>

![API eco][api-management-api]

<span data-ttu-id="50a89-124">Haga clic en **Inténtelo** para intentar la operación **Agregar dos enteros**.</span><span class="sxs-lookup"><span data-stu-id="50a89-124">Click **Try it** to try the **Add two integers** operation.</span></span>

![Pruébelo][api-management-open-console]

<span data-ttu-id="50a89-126">Mantenga los valores predeterminados de los valores de parámetros y seleccione la clave de suscripción para el producto que desee usar desde la lista desplegable **suscription-key** .</span><span class="sxs-lookup"><span data-stu-id="50a89-126">Keep the default parameter values, and select the subscription key for the product you want to use from the **subscription-key** drop-down.</span></span>

<span data-ttu-id="50a89-127">En el portal para desarrolladores, el encabezado **Ocp-Apim-Trace** ya está establecido en **true**.</span><span class="sxs-lookup"><span data-stu-id="50a89-127">By default in the developer portal the **Ocp-Apim-Trace** header is already set to **true**.</span></span> <span data-ttu-id="50a89-128">Este encabezado configura si se ha generado o no un seguimiento.</span><span class="sxs-lookup"><span data-stu-id="50a89-128">This header configures whether or not a trace is generated.</span></span>

![Enviar][api-management-http-get]

<span data-ttu-id="50a89-130">Haga clic en **Enviar** para invocar la operación.</span><span class="sxs-lookup"><span data-stu-id="50a89-130">Click **Send** to invoke the operation.</span></span>

![Enviar][api-management-send-results]

<span data-ttu-id="50a89-132">En los encabezados de respuesta habrá una entrada **ocp-apim-trace-location** con un valor similar al que aparece en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="50a89-132">In the response headers will be an **ocp-apim-trace-location** with a value similar to the following example.</span></span>

```
ocp-apim-trace-location : https://contosoltdxw7zagdfsprykd.blob.core.windows.net/apiinspectorcontainer/ZW3e23NsW4wQyS-SHjS0Og2-2?sv=2013-08-15&sr=b&sig=Mgx7cMHsLmVDv%2B%2BSzvg3JR8qGTHoOyIAV7xDsZbF7%2Bk%3D&se=2014-05-04T21%3A00%3A13Z&sp=r&verify_guid=a56a17d83de04fcb8b9766df38514742
```

<span data-ttu-id="50a89-133">El seguimiento puede descargarse de la ubicación especificada y revisarse, como se demuestra en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="50a89-133">The trace can be downloaded from the specified location and reviewed as demonstrated in the next step.</span></span> <span data-ttu-id="50a89-134">Tenga en cuenta que solo se almacenan las últimas 100 entradas del registro y que las ubicaciones de registro se reutilizan de forma rotativa.</span><span class="sxs-lookup"><span data-stu-id="50a89-134">Note that only the last 100 log entries are stored and log locations are reused in rotation.</span></span> <span data-ttu-id="50a89-135">Por tanto, si realiza más de 100 llamadas con el seguimiento habilitado, al final comenzará a sobrescribir los primeros seguimientos que haya.</span><span class="sxs-lookup"><span data-stu-id="50a89-135">So if you make more than 100 calls with tracing enabled you will eventually start overwriting the first traces in place.</span></span>

## <span data-ttu-id="50a89-136"><a name="inspect-trace"> </a>Inspección del seguimiento</span><span class="sxs-lookup"><span data-stu-id="50a89-136"><a name="inspect-trace"> </a>Inspect the trace</span></span>
<span data-ttu-id="50a89-137">Para revisar los valores del seguimiento, descargue el archivo de seguimiento de la URL de **ocp-apim-trace-location** .</span><span class="sxs-lookup"><span data-stu-id="50a89-137">To review the values in the trace, download the trace file from the **ocp-apim-trace-location** URL.</span></span> <span data-ttu-id="50a89-138">Se trata de un archivo de texto en formato JSON y contiene entradas similares a las que aparecen en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="50a89-138">It is a text file in JSON format, and contains entries similar to the following example.</span></span>

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
                    "message": "Request is being forwarded to the backend service.",
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
                    "message": "Response headers have been sent to the caller. Starting to stream the response body."
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1963155",
                "data": {
                    "message": "Response body streaming to the caller is complete."
                }
            }
        ]
    }
}
```

## <span data-ttu-id="50a89-139"><a name="next-steps"> </a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="50a89-139"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="50a89-140">Vea una demostración del seguimiento de expresiones de directivas en [Cloud Cover Episodio 177: Más características de administración de API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span><span class="sxs-lookup"><span data-stu-id="50a89-140">Watch a demo of tracing policy expressions in [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span></span> <span data-ttu-id="50a89-141">Avance rápidamente hasta el minuto 21:00 para ver la demostración.</span><span class="sxs-lookup"><span data-stu-id="50a89-141">Fast-forward to 21:00 to see the demo.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Cloud+Cover/Episode-177-More-API-Management-Features-with-Vlad-Vinogradsky/player]
> 
> 

[Use API Inspector to trace a call]: #trace-call
[Inspect the trace]: #inspect-trace
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




