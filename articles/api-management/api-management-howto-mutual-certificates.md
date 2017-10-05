---
title: "Asegurar servicios back-end con la autenticación de certificados de cliente - Azure API Management | Microsoft Docs"
description: "Averigüe cómo asegurar servicios back-end con la autenticación de certificados de cliente en Administración de API de Azure"
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
ms.openlocfilehash: 2ebe71c96fd9076a48f689041634dbd23d3d8414
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-secure-back-end-services-using-client-certificate-authentication-in-azure-api-management"></a>Cómo asegurar servicios back-end con la autenticación de certificados de cliente en Administración de API de Azure
Administración de API permite acceder de forma segura al servicio back-end de una API con certificados de cliente. Esta guía muestra cómo administrar certificados en el portal del publicador de API y cómo configurar una API para acceder al servicio back-end correspondiente con un certificado.

Para obtener más información sobre cómo administrar certificados con la API de REST de API Management, consulte el artículo sobre la [entidad de certificado de la API REST de Administración de API de Azure][Azure API Management REST API Certificate entity].

## <a name="prerequisites"> </a>Requisitos previos
Esta guía muestra cómo configurar la instancia de servicio de Administración de API para acceder al servicio back-end de una API con la autenticación de certificados de cliente. Antes de seguir los pasos incluidos en este tema, debe tener el servicio back-end configurado para la autenticación de certificados de cliente ([para configurar la autenticación de certificados en Azure Websites, consulte este artículo][to configure certificate authentication in Azure WebSites refer to this article]) y disponer de acceso al certificado y a su contraseña para poder cargarlo en el portal para editores API Management.

## <a name="step1"> </a>Cargar un certificado de cliente
Para comenzar, haga clic en **Portal para editores** en Azure Portal para el servicio API Management. De este modo, se abre el portal del publicador de Administración de API.

![Portal del publicador de API][api-management-management-console]

> Si aún no ha creado ninguna instancia del servicio de API Management, consulte [Creación de una instancia del servicio API Management][Create an API Management service instance] en el tutorial [Introducción a Azure API Management][Get started with Azure API Management].
> 
> 

Haga clic en **Seguridad** en el menú **API Management** de la izquierda y en **Certificados de cliente**.

![Certificados de cliente][api-management-security-client-certificates]

Para cargar un certificado nuevo, haga clic en **Cargar certificado**.

![Cargar certificado][api-management-upload-certificate]

Examine el certificado y escriba la contraseña correspondiente.

> El certificado debe estar en formato **.pfx** . Se admiten los certificados autofirmados.
> 
> 

![Cargar certificado][api-management-upload-certificate-form]

Haga clic en **Cargar** para cargar el certificado.

> En ese momento se validará la contraseña del certificado. Si es incorrecta, aparecerá un mensaje de error.
> 
> 

![Certificado cargado][api-management-certificate-uploaded]

Cuando el certificado se carga, aparece en la pestaña **Certificados de cliente** . Si cuenta con varios certificados, anote el asunto o los cuatro últimos caracteres de la huella digital con los que se selecciona el certificado al configurar una API para usar certificados (conforme a la sección [Configurar una API para realizar la autenticación de puerta de enlace con un certificado de cliente][Configure an API to use a client certificate for gateway authentication] que aparece más abajo).

> Para desactivar la validación de la cadena de certificados cuando se utiliza, por ejemplo, un certificado autofirmado, siga los pasos descritos en esta [sección](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end) de preguntas más frecuentes.
> 
> 

## <a name="step1a"> </a>Eliminar un certificado de cliente
Para eliminar un certificado, haga clic en **Eliminar** junto a este.

![Eliminar certificado][api-management-certificate-delete]

Haga clic en **Sí, eliminar** para confirmar.

![Confirmar eliminación][api-management-confirm-delete]

Si alguna API está usando el certificado, aparecerá una pantalla de advertencia. Para eliminar el certificado, primero quítelo de todas las API que se hayan configurado para usarlo.

![Confirmar eliminación][api-management-confirm-delete-policy]

## <a name="step2"> </a>Configurar una API para realizar la autenticación de puerta de enlace con un certificado de cliente
Haga clic en **API** en el menú **API Management** de la izquierda, en el nombre de la API en cuestión y en la pestaña **Seguridad**.

![Seguridad de API][api-management-api-security]

Seleccione **Certificados de cliente** en la lista desplegable **Con credenciales**.

![Certificados de cliente][api-management-mutual-certificates]

Seleccione el certificado que desea en la lista desplegable **Certificado de cliente** . Si aparecen varios certificados, revise el asunto o los últimos cuatro caracteres de la huella digital (conforme a la sección anterior) para determinar cuál es el certificado correcto.

![Seleccionar certificado][api-management-select-certificate]

Haga clic en **Guardar** para guardar el cambio de configuración de la API.

> Este cambio se hace efectivo de forma inmediata y llama a las operaciones de la API que realizarán la autenticación en el servidor back-end con el certificado.
> 
> 

![Guardar cambios de API][api-management-save-api]

> Cuando se especifica un certificado para la autenticación de puerta de enlace del servicio back-end de una API, el certificado se integra en la directiva de dicha API y puede verse en el editor de directivas.
> 
> 

![Directiva de certificados][api-management-certificate-policy]

## <a name="next-steps"></a>Pasos siguientes
Para más información sobre otras formas de proteger el servicio back-end, como la autenticación HTTP básica o de secretos compartidos, vea el siguiente vídeo.

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



[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Azure API Management REST API Certificate entity]: http://msdn.microsoft.com/library/azure/dn783483.aspx
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[to configure certificate authentication in Azure WebSites refer to this article]: https://azure.microsoft.com/en-us/documentation/articles/app-service-web-configure-tls-mutual-auth/

[Prerequisites]: #prerequisites
[Upload a client certificate]: #step1
[Delete a client certificate]: #step1a
[Configure an API to use a client certificate for gateway authentication]: #step2
[Test the configuration by calling an operation in the Developer Portal]: #step3
[Next steps]: #next-steps



