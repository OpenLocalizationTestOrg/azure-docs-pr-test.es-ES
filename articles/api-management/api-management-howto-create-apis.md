---
title: "aaaHow toocreate las API de administración de API de Azure"
description: "Obtenga información acerca de cómo toocreate y configurar las API de administración de API de Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 14c20da4-f29f-4b28-bec7-3d4c50b734da
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 48ed8d93947253aa1e67ad995927ed6101cac072
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-apis-in-azure-api-management"></a>¿Cómo toocreate las API de administración de API de Azure
En Administración de API, una API representa un conjunto de operaciones que puede invocarse por las aplicaciones cliente. Nuevas API se crean en el portal para desarrolladores de hello y, a continuación, Hola deseado se agregan las operaciones. Una vez que se agregan las operaciones de hello, Hola API se agrega tooa producto y se puede publicar. Una vez publicada una API, puede ser suscrita tooand utilizado por los desarrolladores.

Esta guía muestra el primer paso de hello en proceso de hello: cómo toocreate y configurar una nueva API de administración de API. Para obtener más información sobre las operaciones de agregar y publicar un producto, consulte [cómo tooadd operaciones tooan API] [ How tooadd operations tooan API] y [cómo toocreate y publicar un producto] [ How toocreate and publish a product].

## <a name="create-new-api"></a>Creación de una API
Las API se crean y configuran en el portal para desarrolladores de Hola. tooaccess Hola click portal, publisher **portal para desarrolladores de** Hola Portal de Azure para el servicio de administración de API.

![Portal del publicador][api-management-management-console]

> Si aún no ha creado una instancia de servicio de administración de API, consulte [crear una instancia de servicio de administración de API] [ Create an API Management service instance] en hello [Introducción a administración de API de Azure] [ Get started with Azure API Management] tutorial.
> 
> 

Haga clic en **API** de hello **administración de API** menú Hola izquierda y, a continuación, haga clic en **agregar API**.

![Create API][api-management-create-api]

Hola de uso **agregar nueva API** tooconfigure ventana Hola nueva API.

![Add new API][api-management-add-new-api]

Hola después campos es tooconfigure usado Hola nueva API.

* **Nombre de la API Web** proporciona un nombre único y descriptivo para hello API. Se muestra en los portales de desarrollador y el publicador de Hola.
* **Dirección URL del servicio Web** referencias Hola implementa Hola API de servicio HTTP. Administración de API reenvía las solicitudes de toothis dirección.
* **Sufijo de URL de la API de Web** es toohello anexado dirección URL base del servicio de administración de API de Hola. dirección URL base de Hello es común para todas las API hospedadas en una instancia de servicio de administración de API. Administración de API distingue API mediante su sufijo y, por tanto, el sufijo de hello debe ser único para todas las API de un publicador determinado.
* **Esquema de dirección URL de la API de Web** determina qué protocolos pueden ser utilizados tooaccess Hola API. HTTPs es el protocolo especificado de forma predeterminada.
* toooptionally agregar este nuevo producto tooa de API, haga clic en hello **productos (opcionales)** lista desplegable y elija un producto. Este paso puede ser varias repetidas veces tooadd Hola API toomultiple productos.

Una vez Hola deseado se configuran los valores, haga clic en **guardar**. Una vez creada la nueva API de hello, hello página de resumen de la API de Hola se muestra en el portal para desarrolladores de Hola.

![API summary][api-management-api-summary]

## <a name="configure-api-settings"></a>Definición de la configuración de la API
Puede usar hello **configuración** ficha tooverify y editar configuración de Hola de una API. **Nombre de la API Web**, **dirección URL del servicio Web**, y **sufijo de URL de la API de Web** se establecen inicialmente cuando Hola API se crea y se puede modificar aquí. **Descripción** proporciona una descripción opcional, y **esquema de dirección URL de Web API** determina qué protocolos pueden ser utilizados tooaccess Hola API.

![API settings][api-management-api-settings]

autenticación de puerta de enlace de tooconfigure hello back-end de servicio API de implementación hello, seleccione hello **seguridad** Hola de pestaña. **con credenciales** desplegable puede ser usado tooconfigure **HTTP básico** o **certificados de cliente** autenticación. la autenticación básica HTTP toouse, simplemente escriba las credenciales de hello deseado. Para obtener información sobre el uso de autenticación de certificado de cliente, consulte [cómo toosecure servicios de back-end con cliente de certificado autenticación de administración de API de Azure][How toosecure back-end services using client certificate authentication in Azure API Management].

Hola **seguridad** ficha también puede ser utilizado tooconfigure **autorización del usuario** mediante OAuth 2.0. Para obtener más información, consulte [cómo tooauthorize developer cuentas con OAuth 2.0 en la administración de API de Azure][How tooauthorize developer accounts using OAuth 2.0 in Azure API Management].

![Basic authentication settings][api-management-api-settings-credentials]

Haga clic en **guardar** toosave los cambios que realice toohello configuración de la API.

## <a name="next-steps"></a>Pasos siguientes
Una vez que se crea una API y configuración de hello, pasos siguientes hello tooadd Hola operaciones toohello API, agregar Hola API tooa producto y publicarlo para que esté disponible para los desarrolladores. Para obtener más información, vea Hola siguientes artículos.

* [¿Cómo tooadd operaciones tooan API][How tooadd operations tooan API]
* [¿Cómo toocreate y publicación de productos][How toocreate and publish a product]

[api-management-create-api]: ./media/api-management-howto-create-apis/api-management-create-api.png
[api-management-management-console]: ./media/api-management-howto-create-apis/api-management-management-console.png
[api-management-add-new-api]: ./media/api-management-howto-create-apis/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-create-apis/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-create-apis/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-create-apis/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-create-apis/api-management-echo-operations.png

[What is an API?]: #what-is-api
[Create a new API]: #create-new-api
[Configure API settings]: #configure-api-settings
[Configure API operations]: #configure-api-operations
[Next steps]: #next-steps

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[How toosecure back-end services using client certificate authentication in Azure API Management]: api-management-howto-mutual-certificates.md
[How tooauthorize developer accounts using OAuth 2.0 in Azure API Management]: api-management-howto-oauth2.md
