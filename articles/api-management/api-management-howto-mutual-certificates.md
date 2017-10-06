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
# <a name="how-toosecure-back-end-services-using-client-certificate-authentication-in-azure-api-management"></a><span data-ttu-id="b14f7-103">Cómo toosecure servicios de back-end con cliente de certificado autenticación de administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="b14f7-103">How toosecure back-end services using client certificate authentication in Azure API Management</span></span>
<span data-ttu-id="b14f7-104">Administración de API ofrece servicio Hola capacidad toosecure acceso toohello back-end de una API mediante certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="b14f7-104">API Management provides hello capability toosecure access toohello back-end service of an API using client certificates.</span></span> <span data-ttu-id="b14f7-105">Esta guía le mostrará cómo toomanage certificados en el portal para desarrolladores de hello API y cómo tooconfigure una API toouse un tooaccess certificado su servicio back-end.</span><span class="sxs-lookup"><span data-stu-id="b14f7-105">This guide shows how toomanage certificates in hello API publisher portal, and how tooconfigure an API toouse a certificate tooaccess its back-end service.</span></span>

<span data-ttu-id="b14f7-106">Para obtener información acerca de cómo administrar certificados mediante Hola API de REST de administración, consulte [entidad de certificado de API de REST de administración de API de Azure][Azure API Management REST API Certificate entity].</span><span class="sxs-lookup"><span data-stu-id="b14f7-106">For information about managing certificates using hello API Management REST API, see [Azure API Management REST API Certificate entity][Azure API Management REST API Certificate entity].</span></span>

## <span data-ttu-id="b14f7-107"><a name="prerequisites"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b14f7-107"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="b14f7-108">Esta guía le mostrará cómo tooconfigure las administración de API servicio instancia toouse cliente certificado autenticación tooaccess Hola servicio back-end para una API.</span><span class="sxs-lookup"><span data-stu-id="b14f7-108">This guide shows you how tooconfigure your API Management service instance toouse client certificate authentication tooaccess hello back-end service for an API.</span></span> <span data-ttu-id="b14f7-109">Antes de hello siguiente los pasos de este tema, debe tener el servicio back-end configurado para la autenticación de certificado de cliente ([certificado tooconfigure autenticación en sitios Web de Azure, consulte el artículo de toothis] [ tooconfigure certificate authentication in Azure WebSites refer toothis article]), y tiene acceso toohello contraseña hello y certificados para el certificado de Hola para cargar en el portal para desarrolladores de administración de API Hola.</span><span class="sxs-lookup"><span data-stu-id="b14f7-109">Before following hello steps in this topic, you should have your back-end service configured for client certificate authentication ([tooconfigure certificate authentication in Azure WebSites refer toothis article][tooconfigure certificate authentication in Azure WebSites refer toothis article]), and have access toohello certificate and hello password for hello certificate for uploading in hello API Management publisher portal.</span></span>

## <span data-ttu-id="b14f7-110"><a name="step1"></a>Cargar un certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="b14f7-110"><a name="step1"> </a>Upload a client certificate</span></span>
<span data-ttu-id="b14f7-111">tooget iniciado, haga clic en **portal para desarrolladores de** Hola Portal de Azure para el servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="b14f7-111">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="b14f7-112">Esto le llevará toohello portal para desarrolladores de administración de API.</span><span class="sxs-lookup"><span data-stu-id="b14f7-112">This takes you toohello API Management publisher portal.</span></span>

![Portal del publicador de API][api-management-management-console]

> <span data-ttu-id="b14f7-114">Si aún no ha creado una instancia de servicio de administración de API, consulte [crear una instancia de servicio de administración de API] [ Create an API Management service instance] en hello [Introducción a administración de API de Azure] [ Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="b14f7-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="b14f7-115">Haga clic en **seguridad** de hello **administración de API** menú Hola izquierda y haga clic en **certificados de cliente**.</span><span class="sxs-lookup"><span data-stu-id="b14f7-115">Click **Security** from hello **API Management** menu on hello left, and click **Client certificates**.</span></span>

![Certificados de cliente][api-management-security-client-certificates]

<span data-ttu-id="b14f7-117">tooupload un nuevo certificado, haga clic en **cargar certificado**.</span><span class="sxs-lookup"><span data-stu-id="b14f7-117">tooupload a new certificate, click **Upload certificate**.</span></span>

![Carga del certificado][api-management-upload-certificate]

<span data-ttu-id="b14f7-119">Examinar tooyour certificado y, a continuación, escriba contraseña Hola Hola certificado.</span><span class="sxs-lookup"><span data-stu-id="b14f7-119">Browse tooyour certificate, and then enter hello password for hello certificate.</span></span>

> <span data-ttu-id="b14f7-120">Hola certificado debe estar en **.pfx** formato.</span><span class="sxs-lookup"><span data-stu-id="b14f7-120">hello certificate must be in **.pfx** format.</span></span> <span data-ttu-id="b14f7-121">Se admiten los certificados autofirmados.</span><span class="sxs-lookup"><span data-stu-id="b14f7-121">Self-signed certificates are allowed.</span></span>
> 
> 

![Carga del certificado][api-management-upload-certificate-form]

<span data-ttu-id="b14f7-123">Haga clic en **cargar** certificado de hello tooupload.</span><span class="sxs-lookup"><span data-stu-id="b14f7-123">Click **Upload** tooupload hello certificate.</span></span>

> <span data-ttu-id="b14f7-124">se valida la contraseña de certificado de Hello en este momento.</span><span class="sxs-lookup"><span data-stu-id="b14f7-124">hello certificate password is validated at this time.</span></span> <span data-ttu-id="b14f7-125">Si es incorrecta, aparecerá un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="b14f7-125">If it is incorrect an error message is displayed.</span></span>
> 
> 

![Certificado cargado][api-management-certificate-uploaded]

<span data-ttu-id="b14f7-127">Una vez cargado el certificado de hello, aparece en hello **certificados de cliente** ficha. Si tiene varios certificados, tome nota del asunto Hola u Hola cuatro últimos caracteres de huella digital de hello, que son certificados de hello tooselect usados al configurar un toouse API certificados, tal como se explicó en siguientes hello [configurar un Toouse un certificado de cliente para la autenticación de puerta de enlace de API] [ Configure an API toouse a client certificate for gateway authentication] sección.</span><span class="sxs-lookup"><span data-stu-id="b14f7-127">Once hello certificate is uploaded, it appears on hello **Client certificates** tab. If you have multiple certificates, make a note of hello subject, or hello last four characters of hello thumbprint, which are used tooselect hello certificate when configuring an API toouse certificates, as covered in hello following [Configure an API toouse a client certificate for gateway authentication][Configure an API toouse a client certificate for gateway authentication] section.</span></span>

> <span data-ttu-id="b14f7-128">tooturn desactivar la validación de la cadena de certificados cuando se utiliza, por ejemplo, un certificado autofirmado, siga los pasos de hello descritos en estas P+F [elemento](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).</span><span class="sxs-lookup"><span data-stu-id="b14f7-128">tooturn off certificate chain validation when using, for example, a self-signed certificate, follow hello steps described in this FAQ [item](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).</span></span>
> 
> 

## <span data-ttu-id="b14f7-129"><a name="step1a"></a>Eliminar un certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="b14f7-129"><a name="step1a"> </a>Delete a client certificate</span></span>
<span data-ttu-id="b14f7-130">toodelete un certificado, haga clic en **eliminar** al lado del certificado que desee Hola.</span><span class="sxs-lookup"><span data-stu-id="b14f7-130">toodelete a certificate, click **Delete** beside hello desired certificate.</span></span>

![Eliminar certificado][api-management-certificate-delete]

<span data-ttu-id="b14f7-132">Haga clic en **Sí, eliminarlo** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="b14f7-132">Click **Yes, delete it** tooconfirm.</span></span>

![Confirmar eliminación][api-management-confirm-delete]

<span data-ttu-id="b14f7-134">Si el certificado de hello está en uso por una API, se muestra una pantalla de advertencia.</span><span class="sxs-lookup"><span data-stu-id="b14f7-134">If hello certificate is in use by an API, then a warning screen is displayed.</span></span> <span data-ttu-id="b14f7-135">certificado de hello toodelete hello, quite primero el certificado de ninguna API que esté configurado toouse lo.</span><span class="sxs-lookup"><span data-stu-id="b14f7-135">toodelete hello certificate you must first remove hello certificate from any APIs that are configured toouse it.</span></span>

![Confirmar eliminación][api-management-confirm-delete-policy]

## <span data-ttu-id="b14f7-137"><a name="step2"></a>Configurar un toouse un certificado de cliente para la autenticación de puerta de enlace de API</span><span class="sxs-lookup"><span data-stu-id="b14f7-137"><a name="step2"> </a>Configure an API toouse a client certificate for gateway authentication</span></span>
<span data-ttu-id="b14f7-138">Haga clic en **API** de hello **administración de API** menú Hola izquierda, haga clic en nombre de Hola de API de hello deseado y haga clic en hello **seguridad** ficha.</span><span class="sxs-lookup"><span data-stu-id="b14f7-138">Click **APIs** from hello **API Management** menu on hello left, click hello name of hello desired API, and click hello **Security** tab.</span></span>

![Seguridad de API][api-management-api-security]

<span data-ttu-id="b14f7-140">Seleccione **certificados de cliente** de hello **con credenciales** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="b14f7-140">Select **Client certificates** from hello **With credentials** drop-down list.</span></span>

![Certificados de cliente][api-management-mutual-certificates]

<span data-ttu-id="b14f7-142">Seleccione Hola certificado que quiera en hello **certificado de cliente** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="b14f7-142">Select hello desired certificate from hello **Client certificate** drop-down list.</span></span> <span data-ttu-id="b14f7-143">Si hay varios certificados puede observar asunto Hola u Hola cuatro últimos caracteres de huella digital de hello como se ha indicado en el certificado correcto de hello anterior sección toodetermine Hola.</span><span class="sxs-lookup"><span data-stu-id="b14f7-143">If there are multiple certificates you can look at hello subject or hello last four characters of hello thumbprint as noted in hello previous section toodetermine hello correct certificate.</span></span>

![Seleccionar certificado][api-management-select-certificate]

<span data-ttu-id="b14f7-145">Haga clic en **guardar** toohello de cambio de configuración de toosave Hola API.</span><span class="sxs-lookup"><span data-stu-id="b14f7-145">Click **Save** toosave hello configuration change toohello API.</span></span>

> <span data-ttu-id="b14f7-146">Este cambio es efectivo de inmediato y llamadas toooperations de esa API utilizará Hola tooauthenticate de certificado en el servidor back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="b14f7-146">This change is effective immediately, and calls toooperations of that API will use hello certificate tooauthenticate on hello back-end server.</span></span>
> 
> 

![Guardar cambios de API][api-management-save-api]

> <span data-ttu-id="b14f7-148">Cuando se especifica un certificado para la autenticación de puerta de enlace de servicio de back-end de Hola de una API, se convierte en parte de la directiva de hello para la API y puede verse en el editor de directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="b14f7-148">When a certificate is specified for gateway authentication for hello back-end service of an API, it becomes part of hello policy for that API, and can be viewed in hello policy editor.</span></span>
> 
> 

![Directiva de certificados][api-management-certificate-policy]

## <a name="next-steps"></a><span data-ttu-id="b14f7-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b14f7-150">Next steps</span></span>
<span data-ttu-id="b14f7-151">Para obtener más información sobre otra maneras toosecure el servicio back-end, como HTTP autenticación básica o compartido secreto, vea Hola después de vídeo.</span><span class="sxs-lookup"><span data-stu-id="b14f7-151">For more information on other ways toosecure your backend service, such as HTTP basic or shared secret authentication, see hello following video.</span></span>

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



