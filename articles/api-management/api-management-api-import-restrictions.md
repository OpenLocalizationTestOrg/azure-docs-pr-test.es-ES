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
# <a name="api-import-restrictions-and-known-issues"></a><span data-ttu-id="93ab7-103">Restricciones de importación de API y problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="93ab7-103">API import restrictions and known issues</span></span>
## <a name="about-this-list"></a><span data-ttu-id="93ab7-104">Acerca de esta lista</span><span class="sxs-lookup"><span data-stu-id="93ab7-104">About this list</span></span>
<span data-ttu-id="93ab7-105">Aunque todo lo posible estará tooensure importar su API en la administración de API de Azure es como transparente y sin problemas como sea posible, en ocasiones imponen restricciones ni identificar los problemas que necesitarán toobe rectifique para poder importar correctamente.</span><span class="sxs-lookup"><span data-stu-id="93ab7-105">While every effort is made tooensure that importing your API into Azure API Management is as seamless and problem-free as possible, we do occasionally impose restrictions or identify issues that will need toobe rectified before you can successfully import.</span></span> <span data-ttu-id="93ab7-106">Este artículo documentan estos, organizados por el formato de importación de Hola de hello API.</span><span class="sxs-lookup"><span data-stu-id="93ab7-106">This article documents these, organised by hello import format of hello API.</span></span>

## <span data-ttu-id="93ab7-107"><a name="open-api"></a>Open API/Swagger</span><span class="sxs-lookup"><span data-stu-id="93ab7-107"><a name="open-api"> </a>Open API/Swagger</span></span>
<span data-ttu-id="93ab7-108">En general, si recibe errores al importar el documento de API abiertos, asegúrese de que los haya validado - mediante el Diseñador de hello en Hola nuevo Portal de Azure (diseño - Front-End - de abrir Editor de especificación de API) o con un 3rd de terceros herramienta como <a href="http://www.swagger.io"> Editor de swagger</a>.</span><span class="sxs-lookup"><span data-stu-id="93ab7-108">In general, if you are receiving errors importing your Open API document, please ensure you have validated it - either using hello designer in hello new Azure Portal (Design - Front End - Open API Specification Editor), or with a 3rd party tool such as <a href="http://www.swagger.io">Swagger Editor</a>.</span></span>

* <span data-ttu-id="93ab7-109">**Nombre de host**: Se requiere un atributo de nombre de host.</span><span class="sxs-lookup"><span data-stu-id="93ab7-109">**Host Name** we require a host name attribute.</span></span>
* <span data-ttu-id="93ab7-110">**Ruta de acceso base**: Se requiere un atributo de ruta de acceso base.</span><span class="sxs-lookup"><span data-stu-id="93ab7-110">**Base Path** we require a base path attribute.</span></span>
* <span data-ttu-id="93ab7-111">**Esquemas**: Se requiere una matriz de esquema.</span><span class="sxs-lookup"><span data-stu-id="93ab7-111">**Schemes** we require a scheme array.</span></span> 

## <span data-ttu-id="93ab7-112"><a name="wsdl"></a>WSDL</span><span class="sxs-lookup"><span data-stu-id="93ab7-112"><a name="wsdl"> </a>WSDL</span></span>
<span data-ttu-id="93ab7-113">Archivos WSDL son toogenerate usa las API de paso a través de SOAP o servir como Hola back-end de una API de SOAP y REST.</span><span class="sxs-lookup"><span data-stu-id="93ab7-113">WSDL files are used toogenerate SOAP Pass-through APIs, or serve as hello backend of a SOAP-to-REST API.</span></span>

* <span data-ttu-id="93ab7-114">**WSDL:Import**: Actualmente no se admiten API que usen este atributo.</span><span class="sxs-lookup"><span data-stu-id="93ab7-114">**WSDL:Import** we do not currently support APIs using this attribute.</span></span> <span data-ttu-id="93ab7-115">Los clientes deben combinar elementos de hello importado en un solo documento.</span><span class="sxs-lookup"><span data-stu-id="93ab7-115">Customers should merge hello imported elements into one document.</span></span>
* <span data-ttu-id="93ab7-116">Los **mensajes con varias partes** no se admiten actualmente.</span><span class="sxs-lookup"><span data-stu-id="93ab7-116">**Messages with multiple parts** are currently not supported.</span></span>
* <span data-ttu-id="93ab7-117">Los servicios de SOAP **WCF wsHttpBinding** creados con Windows Communication Foundation deben utilizar basicHttpBinding - wsHttpBinding.</span><span class="sxs-lookup"><span data-stu-id="93ab7-117">**WCF wsHttpBinding** SOAP services created with Windows Communication Foundation should use basicHttpBinding - wsHttpBinding is not supported.</span></span>
* <span data-ttu-id="93ab7-118">**MTOM**: Los servicios que usan MTOM <em>pueden</em> funcionar.</span><span class="sxs-lookup"><span data-stu-id="93ab7-118">**MTOM** Services using MTOM <em>may</em> work.</span></span> <span data-ttu-id="93ab7-119">No se ofrece soporte técnico oficial en este momento.</span><span class="sxs-lookup"><span data-stu-id="93ab7-119">Official support is not offered at this time.</span></span>
* <span data-ttu-id="93ab7-120">**Recursividad** tipos que están definen de forma recursiva (p. ej. consulte la matriz tooan de sí mismos) no se admiten.</span><span class="sxs-lookup"><span data-stu-id="93ab7-120">**Recursion** types that are defined recursively (e.g. refer tooan array of themselves) are not supported.</span></span>

## <span data-ttu-id="93ab7-121"><a name="wadl"></a>WADL</span><span class="sxs-lookup"><span data-stu-id="93ab7-121"><a name="wadl"> </a>WADL</span></span>
<span data-ttu-id="93ab7-122">No hay ningún problema de importación WADL conocido actualmente.</span><span class="sxs-lookup"><span data-stu-id="93ab7-122">There are no known WADL import issues currently.</span></span>


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
