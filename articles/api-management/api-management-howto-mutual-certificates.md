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
# <a name="how-to-secure-back-end-services-using-client-certificate-authentication-in-azure-api-management"></a><span data-ttu-id="9240c-103">Cómo asegurar servicios back-end con la autenticación de certificados de cliente en Administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="9240c-103">How to secure back-end services using client certificate authentication in Azure API Management</span></span>
<span data-ttu-id="9240c-104">Administración de API permite acceder de forma segura al servicio back-end de una API con certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="9240c-104">API Management provides the capability to secure access to the back-end service of an API using client certificates.</span></span> <span data-ttu-id="9240c-105">Esta guía muestra cómo administrar certificados en el portal del publicador de API y cómo configurar una API para acceder al servicio back-end correspondiente con un certificado.</span><span class="sxs-lookup"><span data-stu-id="9240c-105">This guide shows how to manage certificates in the API publisher portal, and how to configure an API to use a certificate to access its back-end service.</span></span>

<span data-ttu-id="9240c-106">Para obtener más información sobre cómo administrar certificados con la API de REST de API Management, consulte el artículo sobre la [entidad de certificado de la API REST de Administración de API de Azure][Azure API Management REST API Certificate entity].</span><span class="sxs-lookup"><span data-stu-id="9240c-106">For information about managing certificates using the API Management REST API, see [Azure API Management REST API Certificate entity][Azure API Management REST API Certificate entity].</span></span>

## <span data-ttu-id="9240c-107"><a name="prerequisites"> </a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9240c-107"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="9240c-108">Esta guía muestra cómo configurar la instancia de servicio de Administración de API para acceder al servicio back-end de una API con la autenticación de certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="9240c-108">This guide shows you how to configure your API Management service instance to use client certificate authentication to access the back-end service for an API.</span></span> <span data-ttu-id="9240c-109">Antes de seguir los pasos incluidos en este tema, debe tener el servicio back-end configurado para la autenticación de certificados de cliente ([para configurar la autenticación de certificados en Azure Websites, consulte este artículo][to configure certificate authentication in Azure WebSites refer to this article]) y disponer de acceso al certificado y a su contraseña para poder cargarlo en el portal para editores API Management.</span><span class="sxs-lookup"><span data-stu-id="9240c-109">Before following the steps in this topic, you should have your back-end service configured for client certificate authentication ([to configure certificate authentication in Azure WebSites refer to this article][to configure certificate authentication in Azure WebSites refer to this article]), and have access to the certificate and the password for the certificate for uploading in the API Management publisher portal.</span></span>

## <span data-ttu-id="9240c-110"><a name="step1"> </a>Cargar un certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="9240c-110"><a name="step1"> </a>Upload a client certificate</span></span>
<span data-ttu-id="9240c-111">Para comenzar, haga clic en **Portal para editores** en Azure Portal para el servicio API Management.</span><span class="sxs-lookup"><span data-stu-id="9240c-111">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="9240c-112">De este modo, se abre el portal del publicador de Administración de API.</span><span class="sxs-lookup"><span data-stu-id="9240c-112">This takes you to the API Management publisher portal.</span></span>

![Portal del publicador de API][api-management-management-console]

> <span data-ttu-id="9240c-114">Si aún no ha creado ninguna instancia del servicio de API Management, consulte [Creación de una instancia del servicio API Management][Create an API Management service instance] en el tutorial [Introducción a Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="9240c-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="9240c-115">Haga clic en **Seguridad** en el menú **API Management** de la izquierda y en **Certificados de cliente**.</span><span class="sxs-lookup"><span data-stu-id="9240c-115">Click **Security** from the **API Management** menu on the left, and click **Client certificates**.</span></span>

![Certificados de cliente][api-management-security-client-certificates]

<span data-ttu-id="9240c-117">Para cargar un certificado nuevo, haga clic en **Cargar certificado**.</span><span class="sxs-lookup"><span data-stu-id="9240c-117">To upload a new certificate, click **Upload certificate**.</span></span>

![Cargar certificado][api-management-upload-certificate]

<span data-ttu-id="9240c-119">Examine el certificado y escriba la contraseña correspondiente.</span><span class="sxs-lookup"><span data-stu-id="9240c-119">Browse to your certificate, and then enter the password for the certificate.</span></span>

> <span data-ttu-id="9240c-120">El certificado debe estar en formato **.pfx** .</span><span class="sxs-lookup"><span data-stu-id="9240c-120">The certificate must be in **.pfx** format.</span></span> <span data-ttu-id="9240c-121">Se admiten los certificados autofirmados.</span><span class="sxs-lookup"><span data-stu-id="9240c-121">Self-signed certificates are allowed.</span></span>
> 
> 

![Cargar certificado][api-management-upload-certificate-form]

<span data-ttu-id="9240c-123">Haga clic en **Cargar** para cargar el certificado.</span><span class="sxs-lookup"><span data-stu-id="9240c-123">Click **Upload** to upload the certificate.</span></span>

> <span data-ttu-id="9240c-124">En ese momento se validará la contraseña del certificado.</span><span class="sxs-lookup"><span data-stu-id="9240c-124">The certificate password is validated at this time.</span></span> <span data-ttu-id="9240c-125">Si es incorrecta, aparecerá un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="9240c-125">If it is incorrect an error message is displayed.</span></span>
> 
> 

![Certificado cargado][api-management-certificate-uploaded]

<span data-ttu-id="9240c-127">Cuando el certificado se carga, aparece en la pestaña **Certificados de cliente** .</span><span class="sxs-lookup"><span data-stu-id="9240c-127">Once the certificate is uploaded, it appears on the **Client certificates** tab.</span></span> <span data-ttu-id="9240c-128">Si cuenta con varios certificados, anote el asunto o los cuatro últimos caracteres de la huella digital con los que se selecciona el certificado al configurar una API para usar certificados (conforme a la sección [Configurar una API para realizar la autenticación de puerta de enlace con un certificado de cliente][Configure an API to use a client certificate for gateway authentication] que aparece más abajo).</span><span class="sxs-lookup"><span data-stu-id="9240c-128">If you have multiple certificates, make a note of the subject, or the last four characters of the thumbprint, which are used to select the certificate when configuring an API to use certificates, as covered in the following [Configure an API to use a client certificate for gateway authentication][Configure an API to use a client certificate for gateway authentication] section.</span></span>

> <span data-ttu-id="9240c-129">Para desactivar la validación de la cadena de certificados cuando se utiliza, por ejemplo, un certificado autofirmado, siga los pasos descritos en esta [sección](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end) de preguntas más frecuentes.</span><span class="sxs-lookup"><span data-stu-id="9240c-129">To turn off certificate chain validation when using, for example, a self-signed certificate, follow the steps described in this FAQ [item](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).</span></span>
> 
> 

## <span data-ttu-id="9240c-130"><a name="step1a"> </a>Eliminar un certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="9240c-130"><a name="step1a"> </a>Delete a client certificate</span></span>
<span data-ttu-id="9240c-131">Para eliminar un certificado, haga clic en **Eliminar** junto a este.</span><span class="sxs-lookup"><span data-stu-id="9240c-131">To delete a certificate, click **Delete** beside the desired certificate.</span></span>

![Eliminar certificado][api-management-certificate-delete]

<span data-ttu-id="9240c-133">Haga clic en **Sí, eliminar** para confirmar.</span><span class="sxs-lookup"><span data-stu-id="9240c-133">Click **Yes, delete it** to confirm.</span></span>

![Confirmar eliminación][api-management-confirm-delete]

<span data-ttu-id="9240c-135">Si alguna API está usando el certificado, aparecerá una pantalla de advertencia.</span><span class="sxs-lookup"><span data-stu-id="9240c-135">If the certificate is in use by an API, then a warning screen is displayed.</span></span> <span data-ttu-id="9240c-136">Para eliminar el certificado, primero quítelo de todas las API que se hayan configurado para usarlo.</span><span class="sxs-lookup"><span data-stu-id="9240c-136">To delete the certificate you must first remove the certificate from any APIs that are configured to use it.</span></span>

![Confirmar eliminación][api-management-confirm-delete-policy]

## <span data-ttu-id="9240c-138"><a name="step2"> </a>Configurar una API para realizar la autenticación de puerta de enlace con un certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="9240c-138"><a name="step2"> </a>Configure an API to use a client certificate for gateway authentication</span></span>
<span data-ttu-id="9240c-139">Haga clic en **API** en el menú **API Management** de la izquierda, en el nombre de la API en cuestión y en la pestaña **Seguridad**.</span><span class="sxs-lookup"><span data-stu-id="9240c-139">Click **APIs** from the **API Management** menu on the left, click the name of the desired API, and click the **Security** tab.</span></span>

![Seguridad de API][api-management-api-security]

<span data-ttu-id="9240c-141">Seleccione **Certificados de cliente** en la lista desplegable **Con credenciales**.</span><span class="sxs-lookup"><span data-stu-id="9240c-141">Select **Client certificates** from the **With credentials** drop-down list.</span></span>

![Certificados de cliente][api-management-mutual-certificates]

<span data-ttu-id="9240c-143">Seleccione el certificado que desea en la lista desplegable **Certificado de cliente** .</span><span class="sxs-lookup"><span data-stu-id="9240c-143">Select the desired certificate from the **Client certificate** drop-down list.</span></span> <span data-ttu-id="9240c-144">Si aparecen varios certificados, revise el asunto o los últimos cuatro caracteres de la huella digital (conforme a la sección anterior) para determinar cuál es el certificado correcto.</span><span class="sxs-lookup"><span data-stu-id="9240c-144">If there are multiple certificates you can look at the subject or the last four characters of the thumbprint as noted in the previous section to determine the correct certificate.</span></span>

![Seleccionar certificado][api-management-select-certificate]

<span data-ttu-id="9240c-146">Haga clic en **Guardar** para guardar el cambio de configuración de la API.</span><span class="sxs-lookup"><span data-stu-id="9240c-146">Click **Save** to save the configuration change to the API.</span></span>

> <span data-ttu-id="9240c-147">Este cambio se hace efectivo de forma inmediata y llama a las operaciones de la API que realizarán la autenticación en el servidor back-end con el certificado.</span><span class="sxs-lookup"><span data-stu-id="9240c-147">This change is effective immediately, and calls to operations of that API will use the certificate to authenticate on the back-end server.</span></span>
> 
> 

![Guardar cambios de API][api-management-save-api]

> <span data-ttu-id="9240c-149">Cuando se especifica un certificado para la autenticación de puerta de enlace del servicio back-end de una API, el certificado se integra en la directiva de dicha API y puede verse en el editor de directivas.</span><span class="sxs-lookup"><span data-stu-id="9240c-149">When a certificate is specified for gateway authentication for the back-end service of an API, it becomes part of the policy for that API, and can be viewed in the policy editor.</span></span>
> 
> 

![Directiva de certificados][api-management-certificate-policy]

## <a name="next-steps"></a><span data-ttu-id="9240c-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9240c-151">Next steps</span></span>
<span data-ttu-id="9240c-152">Para más información sobre otras formas de proteger el servicio back-end, como la autenticación HTTP básica o de secretos compartidos, vea el siguiente vídeo.</span><span class="sxs-lookup"><span data-stu-id="9240c-152">For more information on other ways to secure your backend service, such as HTTP basic or shared secret authentication, see the following video.</span></span>

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



