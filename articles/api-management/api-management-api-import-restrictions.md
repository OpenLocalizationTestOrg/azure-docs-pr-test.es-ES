---
title: "importan aaaRestrictions y problemas conocidos de la API de administración de Azure | Documentos de Microsoft"
description: "Detalles de los problemas conocidos y las restricciones en la importación en la administración de API de Azure con formatos de API abiertos, WSDL o WADL de Hola."
services: api-management
documentationcenter: 
author: mattfarm
manager: vlvinogr
editor: 
ms.assetid: 7a5a63f0-3e72-49d3-a28c-1bb23ab495e2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: apipm
ms.openlocfilehash: 0bed5ace47de6ccbfbecba25ea6b69c5329de089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="api-import-restrictions-and-known-issues"></a>Restricciones de importación de API y problemas conocidos
## <a name="about-this-list"></a>Acerca de esta lista
Aunque todo lo posible estará tooensure importar su API en la administración de API de Azure es como transparente y sin problemas como sea posible, en ocasiones imponen restricciones ni identificar los problemas que necesitarán toobe rectifique para poder importar correctamente. Este artículo documentan estos, organizados por el formato de importación de Hola de hello API.

## <a name="open-api"></a>Open API/Swagger
En general, si recibe errores al importar el documento de API abiertos, asegúrese de que los haya validado - mediante el Diseñador de hello en Hola nuevo Portal de Azure (diseño - Front-End - de abrir Editor de especificación de API) o con un 3rd de terceros herramienta como <a href="http://www.swagger.io"> Editor de swagger</a>.

* **Nombre de host**: Se requiere un atributo de nombre de host.
* **Ruta de acceso base**: Se requiere un atributo de ruta de acceso base.
* **Esquemas**: Se requiere una matriz de esquema. 

## <a name="wsdl"></a>WSDL
Archivos WSDL son toogenerate usa las API de paso a través de SOAP o servir como Hola back-end de una API de SOAP y REST.

* **WSDL:Import**: Actualmente no se admiten API que usen este atributo. Los clientes deben combinar elementos de hello importado en un solo documento.
* Los **mensajes con varias partes** no se admiten actualmente.
* Los servicios de SOAP **WCF wsHttpBinding** creados con Windows Communication Foundation deben utilizar basicHttpBinding - wsHttpBinding.
* **MTOM**: Los servicios que usan MTOM <em>pueden</em> funcionar. No se ofrece soporte técnico oficial en este momento.
* **Recursividad** tipos que están definen de forma recursiva (p. ej. consulte la matriz tooan de sí mismos) no se admiten.

## <a name="wadl"></a>WADL
No hay ningún problema de importación WADL conocido actualmente.


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
