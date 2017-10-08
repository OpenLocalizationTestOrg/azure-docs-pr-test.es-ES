---
title: "aaaListing la aplicación en la Galería de aplicaciones de Azure Active Directory Hola"
description: "¿Cómo toolist una aplicación que admite el inicio de sesión único en Hola Galería de Azure Active Directory | Microsoft Azure"
services: active-directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 09ccd3b4645a180059b9a9d502e39f1b8933c988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="listing-your-application-in-hello-azure-active-directory-application-gallery"></a><span data-ttu-id="3f1cf-103">Lista de la aplicación en la Galería de aplicaciones de Azure Active Directory Hola</span><span class="sxs-lookup"><span data-stu-id="3f1cf-103">Listing your application in hello Azure Active Directory application gallery</span></span>
<span data-ttu-id="3f1cf-104">una aplicación que admita un inicio de sesión único con Azure Active Directory en hello toolist [Galería de Azure AD](https://azure.microsoft.com/marketplace/active-directory/all/), aplicación hello en primer lugar debe tooimplement uno de los siguientes modos de integración de Hola:</span><span class="sxs-lookup"><span data-stu-id="3f1cf-104">toolist an application that supports single sign-on with Azure Active Directory in hello [Azure AD gallery](https://azure.microsoft.com/marketplace/active-directory/all/), hello application first needs tooimplement one of hello following integration modes:</span></span>

* <span data-ttu-id="3f1cf-105">**OpenID Connect** : la integración directa con Azure AD usa OpenID Connect para la autenticación y Hola consentimiento de Azure AD API para la configuración.</span><span class="sxs-lookup"><span data-stu-id="3f1cf-105">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and hello Azure AD consent API for configuration.</span></span> <span data-ttu-id="3f1cf-106">Si es la primera vez una integración y la aplicación no es compatible con SAML, es el modo recomendado de Hola.</span><span class="sxs-lookup"><span data-stu-id="3f1cf-106">If you are just starting an integration and your application does not support SAML, then this is hello recommend mode.</span></span>
* <span data-ttu-id="3f1cf-107">**SAML** : la aplicación ya tiene proveedores de identidad de otro fabricante Hola capacidad tooconfigure con protocolo SAML de Hola.</span><span class="sxs-lookup"><span data-stu-id="3f1cf-107">**SAML** – Your application already has hello ability tooconfigure third-party identity providers using hello SAML protocol.</span></span>

<span data-ttu-id="3f1cf-108">A continuación se enumeran los requisitos para cada modo.</span><span class="sxs-lookup"><span data-stu-id="3f1cf-108">Listing requirements for each mode are below.</span></span>

## <a name="openid-connect-integration"></a><span data-ttu-id="3f1cf-109">Integración mediante OpenID Connect</span><span class="sxs-lookup"><span data-stu-id="3f1cf-109">OpenID Connect Integration</span></span>
<span data-ttu-id="3f1cf-110">toointegrate su aplicación con Azure AD, Hola siguiente [instrucciones para desarrolladores](active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="3f1cf-110">toointegrate your application with Azure AD, following hello [developer instructions](active-directory-authentication-scenarios.md).</span></span> <span data-ttu-id="3f1cf-111">A continuación, completar las siguientes preguntas de Hola y enviar toowaadpartners@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="3f1cf-111">Then complete hello questions below and send toowaadpartners@microsoft.com.</span></span>

* <span data-ttu-id="3f1cf-112">Proporcione las credenciales para una cuenta o el inquilino de prueba con la aplicación que puede utilizarse en hello integración de Azure AD equipo tootest Hola.</span><span class="sxs-lookup"><span data-stu-id="3f1cf-112">Provide credentials for a test tenant or account with your application that can be used by hello Azure AD team tootest hello integration.</span></span>  
* <span data-ttu-id="3f1cf-113">Se proporcionan instrucciones sobre el modo en que el equipo de hello Azure AD puede iniciar sesión y conectarse a una instancia de aplicación de Azure AD tooyour con hello [marco de consentimiento de Azure AD](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span><span class="sxs-lookup"><span data-stu-id="3f1cf-113">Provide instructions on how hello Azure AD team can sign in and connect an instance of Azure AD tooyour application using hello [Azure AD consent framework](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span></span> 
* <span data-ttu-id="3f1cf-114">Proporcionar el resto de instrucciones necesaria para hello Azure AD de equipo tootest inicio de sesión único con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3f1cf-114">Provide any further instructions required for hello Azure AD team tootest single sign-on with your application.</span></span> 
* <span data-ttu-id="3f1cf-115">Proporcionar información de hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="3f1cf-115">Provide hello info below:</span></span>

> <span data-ttu-id="3f1cf-116">Nombre de la empresa:</span><span class="sxs-lookup"><span data-stu-id="3f1cf-116">Company Name:</span></span>
> 
> <span data-ttu-id="3f1cf-117">Sitio web de la empresa:</span><span class="sxs-lookup"><span data-stu-id="3f1cf-117">Company Website:</span></span>
> 
> <span data-ttu-id="3f1cf-118">Nombre de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="3f1cf-118">Application Name:</span></span>
> 
> <span data-ttu-id="3f1cf-119">Descripción de la aplicación (límite de 200 caracteres):</span><span class="sxs-lookup"><span data-stu-id="3f1cf-119">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="3f1cf-120">Sitio web de la aplicación (informativo):</span><span class="sxs-lookup"><span data-stu-id="3f1cf-120">Application Website (informational):</span></span>
> 
> <span data-ttu-id="3f1cf-121">Sitio web de soporte de técnico de la aplicación o información de contacto:</span><span class="sxs-lookup"><span data-stu-id="3f1cf-121">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="3f1cf-122">Id. de aplicación de la aplicación hello, como se muestra en los detalles de la aplicación hello en https://portal.azure.com:</span><span class="sxs-lookup"><span data-stu-id="3f1cf-122">Application  ID of hello application, as shown in hello application details at https://portal.azure.com:</span></span>
> 
> <span data-ttu-id="3f1cf-123">Dirección URL de suscripción a la aplicación donde los clientes vaya toosign para y y/o aplicación hello de compra:</span><span class="sxs-lookup"><span data-stu-id="3f1cf-123">Application Sign-Up URL where customers go toosign up for and /or purchase hello application:</span></span>
> 
> <span data-ttu-id="3f1cf-124">Elija la categoría de toothree para su toobe aplicación aparecen en (para categorías disponibles, vea hello Azure Active Directory Marketplace):</span><span class="sxs-lookup"><span data-stu-id="3f1cf-124">Choose up toothree categories for your application toobe listed under (for available categories see hello Azure Active Directory Marketplace):</span></span>
> 
> <span data-ttu-id="3f1cf-125">Adjunte un icono pequeño de la aplicación (archivo PNG, 45 px por 45 px, color de fondo sólido):</span><span class="sxs-lookup"><span data-stu-id="3f1cf-125">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="3f1cf-126">Adjunte un icono grande de la aplicación (archivo PNG, 215 px por 215 px, color de fondo sólido):</span><span class="sxs-lookup"><span data-stu-id="3f1cf-126">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="3f1cf-127">Adjunte el logotipo de la aplicación (archivo PNG, 150 px por 122 px, color de fondo transparente):</span><span class="sxs-lookup"><span data-stu-id="3f1cf-127">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

## <a name="saml-integration"></a><span data-ttu-id="3f1cf-128">Integración SAML</span><span class="sxs-lookup"><span data-stu-id="3f1cf-128">SAML Integration</span></span>
<span data-ttu-id="3f1cf-129">Cualquier aplicación que admita SAML 2.0 puede integrarse directamente con un inquilino de Azure AD mediante [estos tooadd instrucciones una aplicación personalizada](../active-directory-saas-custom-apps.md).</span><span class="sxs-lookup"><span data-stu-id="3f1cf-129">Any app that supports SAML 2.0 can be integrated directly with an Azure AD tenant using [these instructions tooadd a custom application](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="3f1cf-130">Una vez que haya probado que la integración de la aplicación funciona con Azure AD, enviar Hola siguiente información demasiado<mailto:waadpartners@microsoft.com>.</span><span class="sxs-lookup"><span data-stu-id="3f1cf-130">Once you have tested that your application integration works with Azure AD, send hello following information too<mailto:waadpartners@microsoft.com>.</span></span>

* <span data-ttu-id="3f1cf-131">Proporcione las credenciales para una cuenta o el inquilino de prueba con la aplicación que puede utilizarse en hello integración de Azure AD equipo tootest Hola.</span><span class="sxs-lookup"><span data-stu-id="3f1cf-131">Provide credentials for a test tenant or account with your application that can be used by hello Azure AD team tootest hello integration.</span></span>  
* <span data-ttu-id="3f1cf-132">Proporcionar Hola SAML Sign On URL, dirección URL del emisor (Id. de entidad), y los valores de dirección URL de respuesta (servicio de consumidor de aserción) para la aplicación, tal como se describe [aquí](../active-directory-saas-custom-apps.md).</span><span class="sxs-lookup"><span data-stu-id="3f1cf-132">Provide hello SAML Sign-On URL, Issuer URL (entity ID), and Reply URL (assertion consumer service) values for your application, as described [here](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="3f1cf-133">Si normalmente proporciona estos valores como parte de un archivo de metadatos SAML, envíelos también.</span><span class="sxs-lookup"><span data-stu-id="3f1cf-133">If you typically provide these values as part of a SAML metadata file, then please send that as well.</span></span>
* <span data-ttu-id="3f1cf-134">Proporciona una breve descripción de cómo tooconfigure Azure AD como proveedor de identidades en su aplicación mediante SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="3f1cf-134">Provide a brief description of how tooconfigure Azure AD as an identity provider in your application using SAML 2.0.</span></span> <span data-ttu-id="3f1cf-135">Si la aplicación admite configurar Azure AD como proveedor de identidades a través de un portal de autoservicio administrativo, a continuación, asegúrese de las credenciales de hello proporcionadas anteriormente incluyen hello capacidad tooset este proceso.</span><span class="sxs-lookup"><span data-stu-id="3f1cf-135">If your application supports configuring Azure AD as an identity provider through a self-service administrative portal, then please ensure hello credentials provided above include hello ability tooset this up.</span></span>
* <span data-ttu-id="3f1cf-136">Proporcionar información de hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="3f1cf-136">Provide hello info below:</span></span>

> <span data-ttu-id="3f1cf-137">Nombre de la empresa:</span><span class="sxs-lookup"><span data-stu-id="3f1cf-137">Company Name:</span></span>
> 
> <span data-ttu-id="3f1cf-138">Sitio web de la empresa:</span><span class="sxs-lookup"><span data-stu-id="3f1cf-138">Company Website:</span></span>
> 
> <span data-ttu-id="3f1cf-139">Nombre de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="3f1cf-139">Application Name:</span></span>
> 
> <span data-ttu-id="3f1cf-140">Descripción de la aplicación (límite de 200 caracteres):</span><span class="sxs-lookup"><span data-stu-id="3f1cf-140">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="3f1cf-141">Sitio web de la aplicación (informativo):</span><span class="sxs-lookup"><span data-stu-id="3f1cf-141">Application Website (informational):</span></span>
> 
> <span data-ttu-id="3f1cf-142">Sitio web de soporte de técnico de la aplicación o información de contacto:</span><span class="sxs-lookup"><span data-stu-id="3f1cf-142">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="3f1cf-143">Dirección URL de suscripción a la aplicación donde los clientes vaya toosign para y y/o aplicación hello de compra:</span><span class="sxs-lookup"><span data-stu-id="3f1cf-143">Application Sign-Up URL where customers go toosign up for and /or purchase hello application:</span></span>
> 
> <span data-ttu-id="3f1cf-144">Elija las categorías de toothree para su toobe aplicación aparecen en (para categorías disponibles, vea hello [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):</span><span class="sxs-lookup"><span data-stu-id="3f1cf-144">Choose up toothree categories for your application toobe listed under (for available categories see hello [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):</span></span>
> 
> <span data-ttu-id="3f1cf-145">Adjunte un icono pequeño de la aplicación (archivo PNG, 45 px por 45 px, color de fondo sólido):</span><span class="sxs-lookup"><span data-stu-id="3f1cf-145">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="3f1cf-146">Adjunte un icono grande de la aplicación (archivo PNG, 215 px por 215 px, color de fondo sólido):</span><span class="sxs-lookup"><span data-stu-id="3f1cf-146">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="3f1cf-147">Adjunte el logotipo de la aplicación (archivo PNG, 150 px por 122 px, color de fondo transparente):</span><span class="sxs-lookup"><span data-stu-id="3f1cf-147">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

