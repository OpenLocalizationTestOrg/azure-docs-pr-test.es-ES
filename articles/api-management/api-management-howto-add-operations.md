---
title: "aaaHow tooadd operations tooan API de administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooadd operaciones tooan API de administración de API de Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 1158a023-1913-4e9c-93de-9164b672f9b3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: d57fa59a2b0ceb392cde23150a0cbb326e52d27d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-operations-tooan-api-in-azure-api-management"></a>¿Cómo tooadd operaciones tooan API de administración de API de Azure
Es necesario agregar operaciones para poder utilizar una API en Administración de API. Esta guía muestra cómo tooadd y configurar los distintos tipos de operaciones tooan API Administración de API.

## <a name="add-operation"></a>Agregar una operación
Las operaciones se agregan y configuran tooan API en el portal para desarrolladores de Hola. tooaccess Hola click portal, publisher **portal para desarrolladores de** Hola Portal de Azure para el servicio de administración de API.

![Portal del publicador][api-management-management-console]

> Si aún no ha creado una instancia de servicio de administración de API, consulte [crear una instancia de servicio de administración de API] [ Create an API Management service instance] en hello [Introducción a administración de API de Azure] [ Get started with Azure API Management] tutorial.
> 
> 

Seleccione Hola deseado API en el portal para desarrolladores de hello y, a continuación, seleccione hello **Operations** ficha. 

![Operaciones][api-management-operations]

Haga clic en **Agregar operación** tooadd una operación de nuevo. Hola **nueva operación** se mostrarán y Hola **firma** ficha se seleccionará de forma predeterminada.

![Agregar operación][api-management-add-operation]

Especificar hello **verbo HTTP** mediante la elección de la lista desplegable de Hola.

![HTTP method][api-management-http-method]

<a name="url-template"></a>

Definir la plantilla de dirección URL de hello escribiendo en un fragmento de dirección URL que consta de uno o más segmentos de ruta de acceso de dirección URL y cero o más parámetros de cadena de consulta. plantilla de dirección URL de Hello, toohello anexado de dirección URL base del programa Hola a API, identifica una única operación HTTP. Puede contener uno o más elementos de variable con nombre que se identifican mediante llaves. Estas partes variables se denominan parámetros de plantilla y se les asignan valores extraídos de dirección URL de la solicitud de hello cuando se procesa la solicitud de Hola por plataforma de administración de API de hello dinámicamente.

> plantilla de dirección URL de Hello puede incluir patrones de caracteres comodín. Por ejemplo, si se especifica `/*` al día todas las solicitudes para ese toohello del método HTTP volver finalizará servicio.

![URL template][api-management-url-template]

<a name="rewrite-url-template"></a>

Si lo desea, especifique hello **plantilla de dirección URL de volver a escribir**. Esto permite plantillas estándar de dirección URL de toouse Hola para procesar las solicitudes entrantes en hello front-end, al llamar a Hola back-end a través de una dirección URL convertida según toohello vuelva a escribir plantilla. Parámetros de plantilla de plantilla de dirección URL de hello deben usarse en la plantilla de reescritura de Hola. Hello en el ejemplo siguiente se muestra cómo contenido tipo codificado como segmento de ruta de acceso de servicio web de hello del anterior ejemplo de Hola puede proporcionarse como parámetro de consulta en hello API publicadas a través de hello plataforma de administración de API con plantillas de dirección URL de Hola.

![URL template rewrite][api-management-url-template-rewrite]

Operación de toohello de los llamadores utilizará el formato de hello `/customers?customerid=ALFKI` y se asignarán demasiado`/Customers('ALFKI')` cuando se invoca el servicio back-end de Hola.

**Mostrar** nombre y **descripción** proporcionar una descripción de la operación de Hola y es utilizados tooprovide documentación toohello a los desarrolladores usar esta API en el portal para desarrolladores de Hola.

![Descripción][api-management-description]

Descripción de la operación de Hello puede especificarse como texto sin formato o HTML en hello **descripción** cuadro de texto.

## <a name="operation-caching"></a>Almacenamiento en caché de operaciones
Las respuestas en caché reducen la latencia percibida por los consumidores Hola API, disminuye el consumo de ancho de banda y disminuye la carga de hello en la implementación de servicio de web HTTP de Hola Hola API. 

tooeasily y habilitar rápidamente el almacenamiento en caché para la operación de hello, seleccione hello **Caching** ficha y compruebe hello **habilitar** casilla de verificación.

![Almacenamiento en caché][api-management-caching-tab]

**Duración** especifica Hola período de tiempo durante el que Hola respuesta de la operación permanece en memoria caché de Hola. valor predeterminado de Hello es 3600 segundos o 1 hora.

Las claves de caché son toodifferentiate utilizado entre las respuestas para que la respuesta de hello correspondiente clave de caché diferente tooeach obtendrá su propio valor almacenado en caché independiente. Si lo desea, especifique los parámetros de cadena de consulta específica o toobe de encabezados HTTP utilizado para calcular los valores de clave de caché en hello **variar por parámetros de cadena de consulta** y **variar por encabezados** cuadros de texto respectivamente. Cuando ninguna es la dirección URL de solicitud especificado, completa y Hola después de valores de encabezado HTTP se usa en la generación de claves de caché: **Accept** y **Accept-Charset**.

> Para obtener más información sobre el almacenamiento en caché y almacenamiento en caché de directivas, consulte [cómo toocache operación da como resultado en la administración de API de Azure][How toocache operation results in Azure API Management].
> 
> 

## <a name="request-parameters"></a>Parámetros de solicitud
Parámetros de operación se administran en la ficha parámetros de Hola. Los parámetros especificados en hello **plantilla de dirección URL** en hello **firma** ficha se agregan automáticamente y se puede cambiar mediante la edición de plantilla de dirección URL de Hola. Se pueden introducir manualmente parámetros adicionales.

tooadd un nuevo parámetro de consulta, haga clic en **Agregar parámetro de consulta** y escriba Hola siguiente información:

* **Nombre** : nombre del parámetro.
* **Descripción** -una breve descripción del parámetro hello (opcional).
* **Tipo** -tipo de parámetro, seleccionado en la lista desplegable de Hola.
* **Valores** -valores que se pueden asignar parámetros de toothis. Uno de los valores de hello puede marcarse como valor predeterminado (opcional).
* **Necesario** -que parámetro hello obligatorio activando la casilla de verificación de Hola. 

![Parámetros de solicitud][api-management-request-parameters]

## <a name="request-body"></a>Cuerpo de la solicitud
Si permite la operación de hello (p. ej., PUT, POST) y requiere un cuerpo puede proporcionar un ejemplo del mismo en todos los de hello admite formatos de representación (por ejemplo, json, XML). 

> cuerpo de la solicitud de saludo se utiliza únicamente con fines de documentación y no se valida.
> 
> 

tooenter un cuerpo de solicitud, cambiar toohello **cuerpo** ficha.

Haga clic en **representación en forma de agregar**, empiece a escribir el nombre de tipo de contenido deseado (por ejemplo, application/json), selecciónelo en la lista desplegable de Hola y Hola pegar deseado ejemplo del cuerpo de solicitud con formato de hello seleccionado en el cuadro de texto de Hola. 

![Request body][api-management-request-body]

En toorepresentations adicionales, también puede especificar una descripción de texto opcional en hello **descripción** cuadro de texto.

## <a name="responses"></a>Respuestas
Es un ejemplos de tooprovide buenas prácticas de respuestas para todos los códigos de estado que se puede producir la operación de Hola. Cada código de estado puede tener más de un ejemplo de cuerpo de respuesta, uno para cada uno de hello admite tipos de contenido. 

tooadd una respuesta, haga clic en **agregar** y comience a escribir código de estado de hello deseado. En este ejemplo de estado de hello es código **200 Aceptar**. Una vez que se muestra el código de hello en Hola de lista desplegable, selecciónela y código de respuesta de hello es operación tooyour creado y agregado.

![Response code][api-management-response-code]

Haga clic en **representación en forma de agregar**, comience a escribir el nombre de tipo de contenido deseado hello (por ejemplo, application/json) y, a continuación, seleccione en Hola de lista desplegable.

![Body content type][api-management-response-body-content-type]

Pegar ejemplo Hola del cuerpo de respuesta en formato seleccionado de hello en el cuadro de texto de Hola. 

![Response body][api-management-response-body]

Si lo desea, agregue una descripción opcional en hello **descripción** cuadro de texto.

Una vez que se configura la operación de hello, haga clic en **guardar**.

## <a name="next-steps"></a>Pasos siguientes
Una vez que las operaciones de Hola se agregan tooan API, Hola siguiente paso es tooassociate hello API con un producto y publicarlo para que los desarrolladores pueden llamar a sus operaciones.

* [¿Cómo toocreate y publicación de productos][How toocreate and publish a product]

[api-management-management-console]: ./media/api-management-howto-add-operations/api-management-management-console.png
[api-management-operations]: ./media/api-management-howto-add-operations/api-management-operations.png
[api-management-add-operation]: ./media/api-management-howto-add-operations/api-management-add-operation.png
[api-management-http-method]: ./media/api-management-howto-add-operations/api-management-http-method.png
[api-management-url-template]: ./media/api-management-howto-add-operations/api-management-url-template.png
[api-management-url-template-rewrite]: ./media/api-management-howto-add-operations/api-management-url-template-rewrite.png
[api-management-description]: ./media/api-management-howto-add-operations/api-management-description.png
[api-management-caching-tab]: ./media/api-management-howto-add-operations/api-management-caching-tab.png
[api-management-request-parameters]: ./media/api-management-howto-add-operations/api-management-request-parameters.png
[api-management-request-body]: ./media/api-management-howto-add-operations/api-management-request-body.png
[api-management-response-code]: ./media/api-management-howto-add-operations/api-management-response-code.png
[api-management-response-body-content-type]: ./media/api-management-howto-add-operations/api-management-response-body-content-type.png
[api-management-response-body]: ./media/api-management-howto-add-operations/api-management-response-body.png


[api-management-contoso-api]: ./media/api-management-howto-add-operations/api-management-contoso-api.png

[api-management-add-new-api]: ./media/api-management-howto-add-operations/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-add-operations/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-add-operations/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-add-operations/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-add-operations/api-management-echo-operations.png

[Add an operation]: #add-operation
[Operation caching]: #operation-caching
[Request parameters]: #request-parameters
[Request body]: #request-body
[Responses]: #responses
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocache operation results in Azure API Management]: api-management-howto-cache.md
