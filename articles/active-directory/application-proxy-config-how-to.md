---
title: "Configuración de una aplicación de proxy de aplicación | Microsoft Docs"
description: "Aprenda a configurar una aplicación de proxy de aplicación en unos pocos pasos sencillos"
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
ms.openlocfilehash: c8f98536048a85ebb3f061d840457130579196d9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-an-application-proxy-application"></a><span data-ttu-id="7f483-103">Configuración de una aplicación de proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="7f483-103">How to configure an Application Proxy application</span></span>

<span data-ttu-id="7f483-104">Este artículo lo ayuda a entender cómo configurar una aplicación de proxy de aplicación en Azure AD para exponer las aplicaciones locales a la nube.</span><span class="sxs-lookup"><span data-stu-id="7f483-104">This article help you to understand how to configure an Application Proxy application within Azure AD to expose your on-premises applications to the cloud.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="7f483-105">Documentos recomendados</span><span class="sxs-lookup"><span data-stu-id="7f483-105">Recommended documents</span></span> 

<span data-ttu-id="7f483-106">Para aprender sobre las configuraciones iniciales y la creación de una aplicación de proxy de aplicación mediante el portal de administración, consulte [Publicación de aplicaciones mediante el proxy de aplicación de Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="7f483-106">To learn about the initial configurations and creation of an Application Proxy application through the Admin Portal, follow the [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

<span data-ttu-id="7f483-107">Para ver detalles sobre la configuración de conectores, consulte [Habilitación del proxy de aplicación en Azure Portal](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="7f483-107">For details on configuring Connectors, see [Enable Application Proxy in the Azure portal](active-directory-application-proxy-enable.md).</span></span>

<span data-ttu-id="7f483-108">Para información sobre cómo cargar certificados y usar dominios personalizados, consulte [Uso de dominios personalizados en el proxy de la aplicación de Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span><span class="sxs-lookup"><span data-stu-id="7f483-108">For information on uploading certificates and using custom domains, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span>

## <a name="create-the-applicationsetting-the-urls"></a><span data-ttu-id="7f483-109">Creación de la aplicación y establecimiento de las direcciones URL</span><span class="sxs-lookup"><span data-stu-id="7f483-109">Create the Application/Setting the URLs</span></span>

<span data-ttu-id="7f483-110">Si está siguiendo los pasos de la documentación [Publicación de aplicaciones mediante el proxy de aplicación de Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) y obtiene un error al crear la aplicación, consulte los detalles del error para ver información y sugerencias para corregir la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7f483-110">If you are following the steps in the [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) documentation and are getting an error creating the application, see the error details for information and suggestions for how to fix the application.</span></span> <span data-ttu-id="7f483-111">La mayoría de los mensajes de error incluyen una sugerencia de corrección.</span><span class="sxs-lookup"><span data-stu-id="7f483-111">Most error messages include a suggested fix.</span></span> <span data-ttu-id="7f483-112">Para evitar errores habituales, compruebe que:</span><span class="sxs-lookup"><span data-stu-id="7f483-112">To avoid common errors, verify:</span></span>

-   <span data-ttu-id="7f483-113">Sea un administrador con permiso para crear una aplicación de proxy de aplicación;</span><span class="sxs-lookup"><span data-stu-id="7f483-113">You are an administrator with permission to create an Application Proxy application</span></span>

-   <span data-ttu-id="7f483-114">La dirección URL interna sea única;</span><span class="sxs-lookup"><span data-stu-id="7f483-114">The internal URL is unique</span></span>

-   <span data-ttu-id="7f483-115">La dirección URL externa sea única;</span><span class="sxs-lookup"><span data-stu-id="7f483-115">The external URL is unique</span></span>

-   <span data-ttu-id="7f483-116">Las direcciones URL empiecen por http o https y terminen en "/";</span><span class="sxs-lookup"><span data-stu-id="7f483-116">The URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="7f483-117">La dirección URL debe ser un nombre de dominio y no una dirección IP.</span><span class="sxs-lookup"><span data-stu-id="7f483-117">The URL should be a domain name, not an IP address</span></span>

<span data-ttu-id="7f483-118">El mensaje de error debería aparecer en la esquina superior derecha cuando cree la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7f483-118">The error message should display in the top right corner when you create the application.</span></span> <span data-ttu-id="7f483-119">También puede seleccionar el icono de notificación para ver los mensajes de error.</span><span class="sxs-lookup"><span data-stu-id="7f483-119">You can also select the notification icon to see the error messages.</span></span>

   ![Mensaje de notificación](./media/application-proxy-config-how-to/error-message.png)

## <a name="configure-connectorsconnector-groups"></a><span data-ttu-id="7f483-121">Configuración de conectores y grupos de conectores</span><span class="sxs-lookup"><span data-stu-id="7f483-121">Configure connectors/connector groups</span></span>

<span data-ttu-id="7f483-122">Si tiene dificultades para configurar la aplicación a causa de la advertencia sobre los conectores y grupos de conectores, consulte las instrucciones para habilitar el proxy de aplicación, donde se ofrecen más detalles sobre cómo descargar conectores.</span><span class="sxs-lookup"><span data-stu-id="7f483-122">If you are having difficulty configuring your application because of warning about the connectors and connector groups, see instructions on enabling Application Proxy for details on how to download connectors.</span></span> <span data-ttu-id="7f483-123">Si desea más información acerca de los conectores, consulte la [documentación sobre los conectores](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span><span class="sxs-lookup"><span data-stu-id="7f483-123">If you want to learn more about connectors, see the [connectors documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span></span>

<span data-ttu-id="7f483-124">Si los conectores están inactivos, esto significa que no pueden alcanzar el servicio.</span><span class="sxs-lookup"><span data-stu-id="7f483-124">If your connectors are inactive, this means that they are unable to reach the service.</span></span> <span data-ttu-id="7f483-125">Esto suele ocurrir porque no están abiertos todos los puertos necesarios.</span><span class="sxs-lookup"><span data-stu-id="7f483-125">This is often because all the required ports are not open.</span></span> <span data-ttu-id="7f483-126">Para ver una lista de los puertos necesarios, consulte la sección Requisitos previos de la documentación sobre la habilitación del proxy de aplicación.</span><span class="sxs-lookup"><span data-stu-id="7f483-126">To see a list of required ports, see the pre-requisites section of the enabling Application Proxy documentation.</span></span>

## <a name="upload-certificates-for-custom-domains"></a><span data-ttu-id="7f483-127">Carga de certificados para dominios personalizados</span><span class="sxs-lookup"><span data-stu-id="7f483-127">Upload certificates for custom domains</span></span>

<span data-ttu-id="7f483-128">Los dominios personalizados le permiten especificar el dominio de las direcciones URL externas.</span><span class="sxs-lookup"><span data-stu-id="7f483-128">Custom Domains allow you to specify the domain of your external URLs.</span></span> <span data-ttu-id="7f483-129">Para usar dominios personalizados, debe cargar el certificado para ese dominio.</span><span class="sxs-lookup"><span data-stu-id="7f483-129">To use custom domains, you need to upload the certificate for that domain.</span></span> <span data-ttu-id="7f483-130">Para información sobre cómo usar certificados y dominios personalizados, consulte [Uso de dominios personalizados en el proxy de la aplicación de Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span><span class="sxs-lookup"><span data-stu-id="7f483-130">For information on using custom domains and certificates, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span> 

<span data-ttu-id="7f483-131">Si se están produciendo problemas al cargar el certificado, busque los mensajes de error en el portal para más información sobre el problema con el certificado.</span><span class="sxs-lookup"><span data-stu-id="7f483-131">If you are encountering issues uploading your certificate, look for the error messages in the portal for additional information on the problem with the certificate.</span></span> <span data-ttu-id="7f483-132">Algunos problemas habituales con los certificados son:</span><span class="sxs-lookup"><span data-stu-id="7f483-132">Common certificate problems include:</span></span>

-   <span data-ttu-id="7f483-133">Certificado expirado</span><span class="sxs-lookup"><span data-stu-id="7f483-133">Expired certificate</span></span>

-   <span data-ttu-id="7f483-134">Certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="7f483-134">Certificate is self-signed</span></span>

-   <span data-ttu-id="7f483-135">Certificado que carece de clave privada</span><span class="sxs-lookup"><span data-stu-id="7f483-135">Certificate is missing the private key</span></span>

<span data-ttu-id="7f483-136">El mensaje de error se muestra en la esquina superior derecha cuando se intenta cargar el certificado.</span><span class="sxs-lookup"><span data-stu-id="7f483-136">The error message display in the top right corner as you try to upload the certificate.</span></span> <span data-ttu-id="7f483-137">También puede seleccionar el icono de notificación para ver los mensajes de error.</span><span class="sxs-lookup"><span data-stu-id="7f483-137">You can also select the notification icon to see the error messages.</span></span>

   ![Mensaje de notificación](./media/application-proxy-config-how-to/error-message2.png)

## <a name="next-steps"></a><span data-ttu-id="7f483-139">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7f483-139">Next steps</span></span>
[<span data-ttu-id="7f483-140">Publicación de aplicaciones mediante el proxy de aplicación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f483-140">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
