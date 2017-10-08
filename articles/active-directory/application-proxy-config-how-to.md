---
title: "una aplicación de Proxy de aplicación del aaaHow tooconfigure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate un configurar una aplicación de Proxy de aplicación en unos pocos pasos sencillos"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: c64019098fc124e4fe10b8288830bcd2b7239d3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application"></a><span data-ttu-id="85625-103">¿Cómo tooconfigure una aplicación de Proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="85625-103">How tooconfigure an Application Proxy application</span></span>

<span data-ttu-id="85625-104">En este artículo le ayudarán a toounderstand cómo tooconfigure una aplicación de Proxy de aplicación en Azure AD tooexpose su toohello de aplicaciones local en la nube.</span><span class="sxs-lookup"><span data-stu-id="85625-104">This article help you toounderstand how tooconfigure an Application Proxy application within Azure AD tooexpose your on-premises applications toohello cloud.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="85625-105">Documentos recomendados</span><span class="sxs-lookup"><span data-stu-id="85625-105">Recommended documents</span></span> 

<span data-ttu-id="85625-106">toolearn sobre configuraciones iniciales de Hola y la creación de una aplicación de Proxy de aplicación a través de hello Portal de administración, siga hello [publicar aplicaciones mediante el Proxy de aplicación de Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="85625-106">toolearn about hello initial configurations and creation of an Application Proxy application through hello Admin Portal, follow hello [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

<span data-ttu-id="85625-107">Para obtener más información sobre la configuración de conectores, consulte [habilitar Proxy de aplicación en el portal de Azure hello](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="85625-107">For details on configuring Connectors, see [Enable Application Proxy in hello Azure portal](active-directory-application-proxy-enable.md).</span></span>

<span data-ttu-id="85625-108">Para información sobre cómo cargar certificados y usar dominios personalizados, consulte [Uso de dominios personalizados en el proxy de la aplicación de Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span><span class="sxs-lookup"><span data-stu-id="85625-108">For information on uploading certificates and using custom domains, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span>

## <a name="create-hello-applicationsetting-hello-urls"></a><span data-ttu-id="85625-109">Crear hello las direcciones URL de configuración de la aplicación/hello</span><span class="sxs-lookup"><span data-stu-id="85625-109">Create hello Application/Setting hello URLs</span></span>

<span data-ttu-id="85625-110">Si está siguiendo los pasos Hola Hola [publicar aplicaciones mediante el Proxy de aplicación de Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) documentación y se recibe un error al crear la aplicación hello, ver detalles de error de Hola para obtener información y sugerencias sobre cómo aplicación de hello toofix.</span><span class="sxs-lookup"><span data-stu-id="85625-110">If you are following hello steps in hello [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) documentation and are getting an error creating hello application, see hello error details for information and suggestions for how toofix hello application.</span></span> <span data-ttu-id="85625-111">La mayoría de los mensajes de error incluyen una sugerencia de corrección.</span><span class="sxs-lookup"><span data-stu-id="85625-111">Most error messages include a suggested fix.</span></span> <span data-ttu-id="85625-112">tooavoid los errores comunes, compruebe que:</span><span class="sxs-lookup"><span data-stu-id="85625-112">tooavoid common errors, verify:</span></span>

-   <span data-ttu-id="85625-113">Es un administrador con permiso toocreate una aplicación de Proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="85625-113">You are an administrator with permission toocreate an Application Proxy application</span></span>

-   <span data-ttu-id="85625-114">dirección URL interna de Hello es único</span><span class="sxs-lookup"><span data-stu-id="85625-114">hello internal URL is unique</span></span>

-   <span data-ttu-id="85625-115">dirección URL externa de Hello es única</span><span class="sxs-lookup"><span data-stu-id="85625-115">hello external URL is unique</span></span>

-   <span data-ttu-id="85625-116">Hola direcciones URL de inicio con http o https y terminar con un "/"</span><span class="sxs-lookup"><span data-stu-id="85625-116">hello URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="85625-117">dirección URL de Hello debe ser un nombre de dominio, no una dirección IP</span><span class="sxs-lookup"><span data-stu-id="85625-117">hello URL should be a domain name, not an IP address</span></span>

<span data-ttu-id="85625-118">mensaje de error de Hello debe aparecer en la esquina superior derecha de hello cuando se crea la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="85625-118">hello error message should display in hello top right corner when you create hello application.</span></span> <span data-ttu-id="85625-119">También puede seleccionar los mensajes de error de hello notificación icono toosee Hola.</span><span class="sxs-lookup"><span data-stu-id="85625-119">You can also select hello notification icon toosee hello error messages.</span></span>

   ![Mensaje de notificación](./media/application-proxy-config-how-to/error-message.png)

## <a name="configure-connectorsconnector-groups"></a><span data-ttu-id="85625-121">Configuración de conectores y grupos de conectores</span><span class="sxs-lookup"><span data-stu-id="85625-121">Configure connectors/connector groups</span></span>

<span data-ttu-id="85625-122">Si tiene dificultades para la configuración de la aplicación debido a la advertencia sobre los conectores de Hola y grupos de conectores, consulte las instrucciones sobre cómo habilitar el Proxy de aplicación para obtener más información acerca de cómo los conectores de toodownload.</span><span class="sxs-lookup"><span data-stu-id="85625-122">If you are having difficulty configuring your application because of warning about hello connectors and connector groups, see instructions on enabling Application Proxy for details on how toodownload connectors.</span></span> <span data-ttu-id="85625-123">Si desea más información acerca de los conectores de toolearn, vea hello [documentación conectores](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span><span class="sxs-lookup"><span data-stu-id="85625-123">If you want toolearn more about connectors, see hello [connectors documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span></span>

<span data-ttu-id="85625-124">Si los conectores están inactivos, esto significa que son servicios de hello tooreach no se puede.</span><span class="sxs-lookup"><span data-stu-id="85625-124">If your connectors are inactive, this means that they are unable tooreach hello service.</span></span> <span data-ttu-id="85625-125">Esto suele ocurrir porque todos los puertos de hello necesario no están abiertos.</span><span class="sxs-lookup"><span data-stu-id="85625-125">This is often because all hello required ports are not open.</span></span> <span data-ttu-id="85625-126">toosee una lista de los puertos necesarios, vea la sección de requisitos previos de Hola de hello habilitar la documentación de Proxy de aplicación.</span><span class="sxs-lookup"><span data-stu-id="85625-126">toosee a list of required ports, see hello pre-requisites section of hello enabling Application Proxy documentation.</span></span>

## <a name="upload-certificates-for-custom-domains"></a><span data-ttu-id="85625-127">Carga de certificados para dominios personalizados</span><span class="sxs-lookup"><span data-stu-id="85625-127">Upload certificates for custom domains</span></span>

<span data-ttu-id="85625-128">Dominios personalizados permiten dominio de hello toospecify de las direcciones URL externas.</span><span class="sxs-lookup"><span data-stu-id="85625-128">Custom Domains allow you toospecify hello domain of your external URLs.</span></span> <span data-ttu-id="85625-129">toouse dominios personalizados, necesita tooupload Hola certificado para ese dominio.</span><span class="sxs-lookup"><span data-stu-id="85625-129">toouse custom domains, you need tooupload hello certificate for that domain.</span></span> <span data-ttu-id="85625-130">Para información sobre cómo usar certificados y dominios personalizados, consulte [Uso de dominios personalizados en el proxy de la aplicación de Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span><span class="sxs-lookup"><span data-stu-id="85625-130">For information on using custom domains and certificates, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span> 

<span data-ttu-id="85625-131">Si se están produciendo problemas al cargar el certificado, busque mensajes de error de hello en el portal de Hola para obtener información adicional sobre el problema de hello con el certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="85625-131">If you are encountering issues uploading your certificate, look for hello error messages in hello portal for additional information on hello problem with hello certificate.</span></span> <span data-ttu-id="85625-132">Algunos problemas habituales con los certificados son:</span><span class="sxs-lookup"><span data-stu-id="85625-132">Common certificate problems include:</span></span>

-   <span data-ttu-id="85625-133">Certificado expirado</span><span class="sxs-lookup"><span data-stu-id="85625-133">Expired certificate</span></span>

-   <span data-ttu-id="85625-134">Certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="85625-134">Certificate is self-signed</span></span>

-   <span data-ttu-id="85625-135">El certificado no tiene clave privada de Hola</span><span class="sxs-lookup"><span data-stu-id="85625-135">Certificate is missing hello private key</span></span>

<span data-ttu-id="85625-136">presentación de mensajes de error de Hello en hello esquina superior derecha cuando intente certificado de hello tooupload.</span><span class="sxs-lookup"><span data-stu-id="85625-136">hello error message display in hello top right corner as you try tooupload hello certificate.</span></span> <span data-ttu-id="85625-137">También puede seleccionar los mensajes de error de hello notificación icono toosee Hola.</span><span class="sxs-lookup"><span data-stu-id="85625-137">You can also select hello notification icon toosee hello error messages.</span></span>

   ![Mensaje de notificación](./media/application-proxy-config-how-to/error-message2.png)

## <a name="next-steps"></a><span data-ttu-id="85625-139">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="85625-139">Next steps</span></span>
[<span data-ttu-id="85625-140">Publicación de aplicaciones mediante el proxy de aplicación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="85625-140">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
