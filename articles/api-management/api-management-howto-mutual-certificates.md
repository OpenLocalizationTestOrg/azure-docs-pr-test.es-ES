---
title: "Servicios de back-end de aaaSecure mediante la autenticación de certificado de cliente - Administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toosecure servicios de back-end con cliente de certificado autenticación de administración de API de Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 43453331-39b2-4672-80b8-0a87e4fde3c6
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 565bb61044fed1158944202c36e8abe30edf5729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-back-end-services-using-client-certificate-authentication-in-azure-api-management"></a>Cómo toosecure servicios de back-end con cliente de certificado autenticación de administración de API de Azure
Administración de API ofrece servicio Hola capacidad toosecure acceso toohello back-end de una API mediante certificados de cliente. Esta guía le mostrará cómo toomanage certificados en el portal para desarrolladores de hello API y cómo tooconfigure una API toouse un tooaccess certificado su servicio back-end.

Para obtener información acerca de cómo administrar certificados mediante Hola API de REST de administración, consulte [entidad de certificado de API de REST de administración de API de Azure][Azure API Management REST API Certificate entity].

## <a name="prerequisites"></a>Requisitos previos
Esta guía le mostrará cómo tooconfigure las administración de API servicio instancia toouse cliente certificado autenticación tooaccess Hola servicio back-end para una API. Antes de hello siguiente los pasos de este tema, debe tener el servicio back-end configurado para la autenticación de certificado de cliente ([certificado tooconfigure autenticación en sitios Web de Azure, consulte el artículo de toothis] [ tooconfigure certificate authentication in Azure WebSites refer toothis article]), y tiene acceso toohello contraseña hello y certificados para el certificado de Hola para cargar en el portal para desarrolladores de administración de API Hola.

## <a name="step1"></a>Cargar un certificado de cliente
tooget iniciado, haga clic en **portal para desarrolladores de** Hola Portal de Azure para el servicio de administración de API. Esto le llevará toohello portal para desarrolladores de administración de API.

![Portal del publicador de API][api-management-management-console]

> Si aún no ha creado una instancia de servicio de administración de API, consulte [crear una instancia de servicio de administración de API] [ Create an API Management service instance] en hello [Introducción a administración de API de Azure] [ Get started with Azure API Management] tutorial.
> 
> 

Haga clic en **seguridad** de hello **administración de API** menú Hola izquierda y haga clic en **certificados de cliente**.

![Certificados de cliente][api-management-security-client-certificates]

tooupload un nuevo certificado, haga clic en **cargar certificado**.

![Carga del certificado][api-management-upload-certificate]

Examinar tooyour certificado y, a continuación, escriba contraseña Hola Hola certificado.

> Hola certificado debe estar en **.pfx** formato. Se admiten los certificados autofirmados.
> 
> 

![Carga del certificado][api-management-upload-certificate-form]

Haga clic en **cargar** certificado de hello tooupload.

> se valida la contraseña de certificado de Hello en este momento. Si es incorrecta, aparecerá un mensaje de error.
> 
> 

![Certificado cargado][api-management-certificate-uploaded]

Una vez cargado el certificado de hello, aparece en hello **certificados de cliente** ficha. Si tiene varios certificados, tome nota del asunto Hola u Hola cuatro últimos caracteres de huella digital de hello, que son certificados de hello tooselect usados al configurar un toouse API certificados, tal como se explicó en siguientes hello [configurar un Toouse un certificado de cliente para la autenticación de puerta de enlace de API] [ Configure an API toouse a client certificate for gateway authentication] sección.

> tooturn desactivar la validación de la cadena de certificados cuando se utiliza, por ejemplo, un certificado autofirmado, siga los pasos de hello descritos en estas P+F [elemento](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).
> 
> 

## <a name="step1a"></a>Eliminar un certificado de cliente
toodelete un certificado, haga clic en **eliminar** al lado del certificado que desee Hola.

![Eliminar certificado][api-management-certificate-delete]

Haga clic en **Sí, eliminarlo** tooconfirm.

![Confirmar eliminación][api-management-confirm-delete]

Si el certificado de hello está en uso por una API, se muestra una pantalla de advertencia. certificado de hello toodelete hello, quite primero el certificado de ninguna API que esté configurado toouse lo.

![Confirmar eliminación][api-management-confirm-delete-policy]

## <a name="step2"></a>Configurar un toouse un certificado de cliente para la autenticación de puerta de enlace de API
Haga clic en **API** de hello **administración de API** menú Hola izquierda, haga clic en nombre de Hola de API de hello deseado y haga clic en hello **seguridad** ficha.

![Seguridad de API][api-management-api-security]

Seleccione **certificados de cliente** de hello **con credenciales** lista desplegable.

![Certificados de cliente][api-management-mutual-certificates]

Seleccione Hola certificado que quiera en hello **certificado de cliente** lista desplegable. Si hay varios certificados puede observar asunto Hola u Hola cuatro últimos caracteres de huella digital de hello como se ha indicado en el certificado correcto de hello anterior sección toodetermine Hola.

![Seleccionar certificado][api-management-select-certificate]

Haga clic en **guardar** toohello de cambio de configuración de toosave Hola API.

> Este cambio es efectivo de inmediato y llamadas toooperations de esa API utilizará Hola tooauthenticate de certificado en el servidor back-end de Hola.
> 
> 

![Guardar cambios de API][api-management-save-api]

> Cuando se especifica un certificado para la autenticación de puerta de enlace de servicio de back-end de Hola de una API, se convierte en parte de la directiva de hello para la API y puede verse en el editor de directiva de Hola.
> 
> 

![Directiva de certificados][api-management-certificate-policy]

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre otra maneras toosecure el servicio back-end, como HTTP autenticación básica o compartido secreto, vea Hola después de vídeo.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Last-mile-Security/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-mutual-certificates/api-management-management-console.png
[api-management-security-client-certificates]: ./media/api-management-howto-mutual-certificates/api-management-security-client-certificates.png
[api-management-upload-certificate]: ./media/api-management-howto-mutual-certificates/api-management-upload-certificate.png
[api-management-upload-certificate-form]: ./media/api-management-howto-mutual-certificates/api-management-upload-certificate-form.png
[api-management-certificate-uploaded]: ./media/api-management-howto-mutual-certificates/api-management-certificate-uploaded.png
[api-management-api-security]: ./media/api-management-howto-mutual-certificates/api-management-api-security.png
[api-management-mutual-certificates]: ./media/api-management-howto-mutual-certificates/api-management-mutual-certificates.png
[api-management-select-certificate]: ./media/api-management-howto-mutual-certificates/api-management-select-certificate.png
[api-management-save-api]: ./media/api-management-howto-mutual-certificates/api-management-save-api.png
[api-management-certificate-policy]: ./media/api-management-howto-mutual-certificates/api-management-certificate-policy.png
[api-management-certificate-delete]: ./media/api-management-howto-mutual-certificates/api-management-certificate-delete.png
[api-management-confirm-delete]: ./media/api-management-howto-mutual-certificates/api-management-confirm-delete.png
[api-management-confirm-delete-policy]: ./media/api-management-howto-mutual-certificates/api-management-confirm-delete-policy.png



[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Azure API Management REST API Certificate entity]: http://msdn.microsoft.com/library/azure/dn783483.aspx
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[tooconfigure certificate authentication in Azure WebSites refer toothis article]: https://azure.microsoft.com/en-us/documentation/articles/app-service-web-configure-tls-mutual-auth/

[Prerequisites]: #prerequisites
[Upload a client certificate]: #step1
[Delete a client certificate]: #step1a
[Configure an API toouse a client certificate for gateway authentication]: #step2
[Test hello configuration by calling an operation in hello Developer Portal]: #step3
[Next steps]: #next-steps



