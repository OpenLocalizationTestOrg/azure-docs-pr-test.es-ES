---
title: "aaaAdd almacenamiento en caché tooimprove rendimiento en la administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo cargan la latencia de Hola de tooimprove, el consumo de ancho de banda y el servicio web de las llamadas de servicio de administración de API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 740f6a27-8323-474d-ade2-828ae0c75e7a
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 056ab7cf788218327e30bd5c028b76e3b1977fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-caching-tooimprove-performance-in-azure-api-management"></a>Agregar almacenamiento en caché de tooimprove de rendimiento en la administración de API de Azure
En Administración de API, las operaciones se pueden configurar para el almacenamiento en caché de respuestas. El almacenamiento en caché de respuestas puede reducir significativamente la latencia de la API, el consumo de ancho de banda y la carga del servicio web en cuanto a datos que no cambian con frecuencia.

Esta guía le mostrará cómo tooadd respuesta configurar directivas para las operaciones de API de eco de ejemplo de Hola y almacenamiento en caché de la API. A continuación, puede llamar a operación hello en la caché de tooverify portal para desarrolladores de hello en acción.

> [!NOTE]
> Para obtener información sobre el almacenamiento en caché de los elementos por parte de la clave mediante expresiones de directiva, consulte [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).
> 
> 

## <a name="prerequisites"></a>Requisitos previos
Para los pasos siguiente hello en esta guía, debe tener una instancia de servicio de administración de API con una API y un producto configurado. Si aún no ha creado una instancia de servicio de administración de API, consulte [crear una instancia de servicio de administración de API] [ Create an API Management service instance] en hello [Introducción a administración de API de Azure] [ Get started with Azure API Management] tutorial.

## <a name="configure-caching"></a>Configuración de una operación para almacenamiento en caché
En este paso, revisará Hola almacenamiento en caché de configuración de hello **obtener recursos (en caché)** el funcionamiento de ejemplo de Hola a API de eco.

> [!NOTE]
> Cada instancia de servicio de administración de API viene preconfigurado con una API de eco que se pueden tooexperiment usado con y obtener información acerca de la API de administración. Para más información, consulte [Introducción a Azure API Management][Get started with Azure API Management].
> 
> 

tooget iniciado, haga clic en **portal para desarrolladores de** Hola Portal de Azure para el servicio de administración de API. Esto le llevará toohello portal para desarrolladores de administración de API.

![Portal del publicador][api-management-management-console]

Haga clic en **API** de hello **administración de API** menú Hola izquierda y, a continuación, haga clic en **API de eco**.

![API eco][api-management-echo-api]

Haga clic en hello **Operations** ficha y, a continuación, haga clic en hello **obtener recursos (en caché)** operación de hello **Operations** lista.

![Echo API operations][api-management-echo-api-operations]

Haga clic en hello **Caching** Hola de tooview ficha almacenamiento en caché de configuración para esta operación.

![Caching tab][api-management-caching-tab]

tooenable el almacenamiento en caché para una operación, seleccione hello **habilitar** casilla de verificación. En este ejemplo, el almacenamiento en caché está habilitado.

Con una clave de cada respuesta de la operación, basándose en valores Hola Hola **variar por parámetros de cadena de consulta** y **variar por encabezados** campos. Si desea toocache varias respuestas en función de los parámetros de cadena de consulta o los encabezados, puede configurarlos en estos dos campos.

**Duración** especifica el intervalo de expiración de Hola de respuestas de hello en caché. En este ejemplo, es el intervalo de saludo **3600** segundos, que es la hora tooone equivalente.

Usar almacenamiento en caché de configuración en este ejemplo de Hola, Hola primer toohello de solicitud **obtener recursos (en caché)** operación devuelve una respuesta de servicio de back-end de Hola. Esta respuesta se almacenarán en caché, ordenados por hello especificada parámetros de cadena de encabezados y la consulta. Las llamadas subsiguientes operación toohello, con la coincidencia de parámetros, tendrá hello en memoria caché respuesta devuelta, hasta que expire el intervalo de duración de caché de saludo.

## <a name="caching-policies"></a>Hola revisión almacenamiento en caché de directivas
En este paso, revise Hola almacenamiento en caché de configuración de hello **obtener recursos (en caché)** el funcionamiento de ejemplo de Hola a API de eco.

Al almacenamiento en caché se configura para una operación en hello **Caching** ficha almacenamiento en caché de directivas se agregan para la operación de Hola. Estas directivas pueden verse y modificarse en el editor de directiva de Hola.

Haga clic en **directivas** de hello **administración de API** menú Hola izquierda y, a continuación, seleccione **API eco / obtener los recursos (en caché)** de hello **operación**lista desplegable.

![Policy scope operation][api-management-operation-dropdown]

Esto muestra las directivas de Hola para esta operación en el editor de directiva de Hola.

![API Management policy editor][api-management-policy-editor]

definición de la directiva de Hola para esta operación incluye hello las directivas que definen Hola configuración de caché que se revisaron con hello **Caching** ficha en el paso anterior de Hola.

```xml
<policies>
    <inbound>
        <base />
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false">
            <vary-by-header>Accept</vary-by-header>
            <vary-by-header>Accept-Charset</vary-by-header>
        </cache-lookup>
        <rewrite-uri template="/resource" />
    </inbound>
    <outbound>
        <base />
        <cache-store caching-mode="cache-on" duration="3600" />
    </outbound>
</policies>
```

> [!NOTE]
> Almacenamiento en caché de directivas en el editor de directiva de Hola de toohello de los cambios realizados se reflejarán en hello **Caching** pestaña de una operación y viceversa.
> 
> 

## <a name="test-operation"></a>Llamar a una operación y probar el almacenamiento en caché de Hola
Hola toosee almacenamiento en caché en acción, podemos llamar operación Hola desde portal para desarrolladores de Hola. Haga clic en **portal para desarrolladores de** en el menú superior derecho de Hola.

![portal para desarrolladores][api-management-developer-portal-menu]

Haga clic en **API** en Hola menú superior y, a continuación, seleccione **API de eco**.

![API eco][api-management-apis-echo-api]

> Si tiene sólo una API configurada o cuenta tooyour visible, a continuación, haga clic en las API le lleva directamente operaciones toohello para la API.
> 
> 

Seleccione hello **obtener recursos (en caché)** operación y, a continuación, haga clic en **abrir la consola de**.

![Open console][api-management-open-console]

Hola consola permite operaciones de tooinvoke directamente desde el portal para desarrolladores de Hola.

![Consola][api-management-console]

Mantener valores predeterminados de Hola para **param1** y **param2**.

Seleccione Hola clave deseado de hello **clave de suscripción** lista desplegable. Si su cuenta tiene solo una suscripción, ya estará seleccionada.

Escriba **sampleheader:value1** en hello **encabezados de solicitud** cuadro de texto.

Haga clic en **HTTP Get** y tome nota de hello encabezados de respuesta.

Escriba **sampleheader:value2** en hello **encabezados de solicitud** cuadro de texto y, a continuación, haga clic en **HTTP Get**.

Tenga en cuenta ese valor Hola de **sampleheader** sigue siendo **value1** en respuesta Hola. Pruebe algunos valores diferentes y tenga en cuenta que Hola respuesta almacenada en caché de la primera llamada de Hola se devuelve.

Escriba **25** en hello **param2** campo y, a continuación, haga clic en **HTTP Get**.

Tenga en cuenta ese valor Hola de **sampleheader** en hello respuesta es ahora **value2**. Porque los resultados de la operación de hello están organizados por cadena de consulta, no ha devuelto la respuesta almacenada en caché de hello anterior.

## <a name="next-steps"></a>Pasos siguientes
* Para obtener más información sobre el almacenamiento en caché de directivas, consulte [almacenamiento en caché de directivas de] [ Caching policies] en hello [referencia de directiva de administración de API][API Management policy reference].
* Para obtener información sobre el almacenamiento en caché de los elementos por parte de la clave mediante expresiones de directiva, consulte [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).

[api-management-management-console]: ./media/api-management-howto-cache/api-management-management-console.png
[api-management-echo-api]: ./media/api-management-howto-cache/api-management-echo-api.png
[api-management-echo-api-operations]: ./media/api-management-howto-cache/api-management-echo-api-operations.png
[api-management-caching-tab]: ./media/api-management-howto-cache/api-management-caching-tab.png
[api-management-operation-dropdown]: ./media/api-management-howto-cache/api-management-operation-dropdown.png
[api-management-policy-editor]: ./media/api-management-howto-cache/api-management-policy-editor.png
[api-management-developer-portal-menu]: ./media/api-management-howto-cache/api-management-developer-portal-menu.png
[api-management-apis-echo-api]: ./media/api-management-howto-cache/api-management-apis-echo-api.png
[api-management-open-console]: ./media/api-management-howto-cache/api-management-open-console.png
[api-management-console]: ./media/api-management-howto-cache/api-management-console.png


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md

[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx

[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Configure an operation for caching]: #configure-caching
[Review hello caching policies]: #caching-policies
[Call an operation and test hello caching]: #test-operation
[Next steps]: #next-steps
