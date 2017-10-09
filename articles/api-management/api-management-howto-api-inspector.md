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
# <a name="how-toouse-hello-api-inspector-tootrace-calls-in-azure-api-management"></a>Cómo llama a toouse hello tootrace API Inspector de administración de API de Azure
Administración de API proporciona un API Inspector toohelp de herramienta de depuración y solución de problemas de las API. Hola API Inspector pueden usarse mediante programación y también puede utilizarse directamente desde el portal para desarrolladores de Hola. 

Además tootracing operaciones, API Inspector también realiza un seguimiento de [expresión de directiva](https://msdn.microsoft.com/library/azure/dn910913.aspx) evaluaciones. Para ver una demostración, vea [177 episodio abarcan de nube: más características de administración de API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) y avancemos too21:00.

En esta guía se explica el uso del API Inspector.

> [!NOTE]
> Seguimientos de API Inspector solo se genera y están disponibles para las solicitudes que contiene las claves de la suscripción que pertenecen toohello [administrador](api-management-howto-create-groups.md) cuenta.
> 
> 

## <a name="trace-call"></a> Tootrace una llamada de Inspector de API de uso
Agregar toouse API Inspector, un **ocp-apim-trace: true** solicitud de llamada de la operación de tooyour de encabezado y, a continuación, descargar e inspeccionar el seguimiento de hello mediante dirección URL de hello indicado por hello **ocp apim seguimiento ubicación** encabezado de respuesta. Esto puede hacerse mediante programación y permite llevar a cabo directamente desde el portal para desarrolladores de Hola.

Este tutorial muestra cómo toouse Hola API Inspector tootrace las operaciones con Hola API calculadora básica que se configura en hello [administrar su primera API](api-management-get-started.md) tutorial de introducción. Si no se han completado este tutorial sólo tarda unos instantes tooimport Hola API calculadora básica, o puede usar otra API de su elección, como la API de eco hello. Cada instancia de servicio de administración de API viene preconfigurado con una API de eco que se pueden tooexperiment usado con y obtener información acerca de la API de administración. API de eco Hello devuelve cualquier entrada se envía tooit. toouse, puede invocar cualquier verbo HTTP y valor devuelto de hello simplemente será lo que envía. 

tooget iniciado, haga clic en **portal para desarrolladores de** Hola Portal de Azure para el servicio de administración de API. Las operaciones pueden llamarse directamente desde el portal para desarrolladores de Hola que proporciona una manera cómoda de tooview y pruebe las operaciones de Hola de una API.

> Si aún no ha creado una instancia de servicio de administración de API, consulte [crear una instancia de servicio de administración de API] [ Create an API Management service instance] en hello [Introducción a administración de API de Azure] [ Get started with Azure API Management] tutorial.
> 
> 

![API Management developer portal][api-management-developer-portal-menu]

Haga clic en **API** desde el menú superior de hello y, a continuación, haga clic en **calculadora básica**.

![API eco][api-management-api]

Haga clic en **Pruébelo** tootry hello **agrega dos enteros** operación.

![Pruébelo][api-management-open-console]

Mantener valores de parámetros predeterminados de Hola y clave de suscripción Hola seleccione producto Hola desea toouse de hello **clave de suscripción** lista desplegable.

De forma predeterminada en Hola Hola de portal para desarrolladores **Ocp-Apim-Trace** encabezado ya está establecido demasiado**true**. Este encabezado configura si se ha generado o no un seguimiento.

![Los métodos Send][api-management-http-get]

Haga clic en **enviar** operación de hello tooinvoke.

![Los métodos Send][api-management-send-results]

En la respuesta de hello encabezados será un **ocp apim seguimiento ubicación** con un toohello similar valor siguiente ejemplo.

```
ocp-apim-trace-location : https://contosoltdxw7zagdfsprykd.blob.core.windows.net/apiinspectorcontainer/ZW3e23NsW4wQyS-SHjS0Og2-2?sv=2013-08-15&sr=b&sig=Mgx7cMHsLmVDv%2B%2BSzvg3JR8qGTHoOyIAV7xDsZbF7%2Bk%3D&se=2014-05-04T21%3A00%3A13Z&sp=r&verify_guid=a56a17d83de04fcb8b9766df38514742
```

seguimiento de Hello puede descargarse desde Hola ubicación especificada y revisado como se muestra en el paso siguiente Hola. Tenga en cuenta que solo Hola última 100 entradas del registro se almacenan y se reutilizan ubicaciones del registro de rotación. Por tanto, si realiza más de 100 llamadas con el seguimiento habilitado se iniciarán finalmente seguimientos primera hello en lugar de sobrescribir.

## <a name="inspect-trace"></a>Inspeccionar seguimiento Hola
valores de hello tooreview en seguimiento de hello, descargue el archivo de seguimiento de Hola de Hola **ocp apim seguimiento ubicación** dirección URL. Es un archivo de texto en formato JSON y contiene entradas toohello similar siguiente ejemplo.

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

## <a name="next-steps"></a>Pasos siguientes
* Vea una demostración del seguimiento de expresiones de directivas en [Cloud Cover Episodio 177: Más características de administración de API](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/). Demostración de avance rápido too21:00 toosee Hola.

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




