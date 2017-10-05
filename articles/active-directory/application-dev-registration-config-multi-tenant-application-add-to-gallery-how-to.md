---
title: "Incorporación de una aplicación multiinquilino a la galería de aplicaciones de Azure AD | Microsoft Docs"
description: "En este artículo se explica cómo se puede mostrar una aplicación multiinquilino personalizada en la galería de aplicaciones de Azure AD"
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
ms.openlocfilehash: 208f0d40bd7a8e8f35f16e1fcb09c305d833dbb2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-add-a-multi-tenant-application-to-the-azure-ad-application-gallery"></a><span data-ttu-id="c3ab3-103">Incorporación de una aplicación multiinquilino a la galería de aplicaciones de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3ab3-103">How to add a multi-tenant application to the Azure AD application gallery</span></span>

## <a name="what-is-the-azure-ad-application-gallery"></a><span data-ttu-id="c3ab3-104">¿Qué es la galería de aplicaciones de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="c3ab3-104">What is the Azure AD Application Gallery?</span></span>

<span data-ttu-id="c3ab3-105">La galería de aplicaciones de Azure AD constituye un mecanismo ideal para mostrar la aplicación a los millones de clientes de Azure Active Directory y, de esta forma, ampliar el alcance y el impacto de la aplicación en el mercado.</span><span class="sxs-lookup"><span data-stu-id="c3ab3-105">The Azure AD Application Gallery is a great way to get your application in front of all the millions of Azure Active Directory customers to broaden the impact and reach of your application in the marketplace.</span></span> <span data-ttu-id="c3ab3-106">En los pasos siguientes, se explica cómo puede incluir la aplicación en la galería de aplicaciones de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3ab3-106">The below steps explain how you can list your application in the Azure AD Application Gallery.</span></span>

## <a name="if-your-application-supports-saml-or-openidconnect"></a><span data-ttu-id="c3ab3-107">Si la aplicación es compatible con SAML o con OpenIDConnect</span><span class="sxs-lookup"><span data-stu-id="c3ab3-107">If your application supports SAML or OpenIDConnect</span></span>
<span data-ttu-id="c3ab3-108">Si tiene una aplicación multiinquilino y le gustaría que apareciera en la galería de aplicaciones de Azure AD, primero debe asegurarse de que es compatible con una de las siguientes tecnologías de inicio de sesión único:</span><span class="sxs-lookup"><span data-stu-id="c3ab3-108">If you have a multi-tenant application you'd like to list in the Azure AD Application Gallery, you must first make sure that your application supports one of the following single sign-on technologies:</span></span>

1. <span data-ttu-id="c3ab3-109">**OpenID Connect** : integración directa con Azure AD mediante OpenID Connect para autenticación y la API de consentimiento de Azure AD para configuración.</span><span class="sxs-lookup"><span data-stu-id="c3ab3-109">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and the Azure AD consent API for configuration.</span></span> <span data-ttu-id="c3ab3-110">Si acaba de iniciar una integración y la aplicación no es compatible con SAML, este es el modo recomendado.</span><span class="sxs-lookup"><span data-stu-id="c3ab3-110">If you are just starting an integration and your application does not support SAML, then this is the recommend mode.</span></span>
2. <span data-ttu-id="c3ab3-111">**SAML** : la aplicación ya tiene la capacidad de configurar proveedores de identidad de terceros mediante el protocolo SAML.</span><span class="sxs-lookup"><span data-stu-id="c3ab3-111">**SAML** – Your application already has the ability to configure third-party identity providers using the SAML protocol.</span></span>

<span data-ttu-id="c3ab3-112">Si la aplicación multiinquilino es compatible con uno de estos modos de inicio de sesión único y le gustaría incluirla en la galería de aplicaciones de Azure AD, puede seguir el procedimiento del documento que se indica más abajo.</span><span class="sxs-lookup"><span data-stu-id="c3ab3-112">If your application supports one of these single sign-on modes and you'd like to list your multi-tenant application in the Azure AD Application Gallery, you can follow the steps in the document below.</span></span> <span data-ttu-id="c3ab3-113">Si desea empezar rápidamente, envíe un correo electrónico a **waadpartners@microsoft.com**.</span><span class="sxs-lookup"><span data-stu-id="c3ab3-113">To get started quickly send an email to **waadpartners@microsoft.com**.</span></span>

## <a name="if-your-application-does-not-support-saml-or-openidconnect"></a><span data-ttu-id="c3ab3-114">Si la aplicación no es compatible con SAML ni con OpenIDConnect</span><span class="sxs-lookup"><span data-stu-id="c3ab3-114">If your application does not support SAML or OpenIDConnect</span></span>
<span data-ttu-id="c3ab3-115">Aunque la aplicación no sea compatible con ninguno de estos modos, puede incluirla en la galería. Para ello, tiene que usar nuestra tecnología de inicio de sesión único con contraseña.</span><span class="sxs-lookup"><span data-stu-id="c3ab3-115">Even if your application does not support one of these modes, we can still integrate it into our gallery using our Password Single Sign-on technology.</span></span> <span data-ttu-id="c3ab3-116">Si desea valorar esta opción, puede enviar un correo electrónico a **waadpartners@microsoft.com**.</span><span class="sxs-lookup"><span data-stu-id="c3ab3-116">If you'd like to explore this option, you can send an email to **waadpartners@microsoft.com**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3ab3-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c3ab3-117">Next steps</span></span>
[<span data-ttu-id="c3ab3-118">Anuncio de la aplicación en la galería de aplicaciones de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c3ab3-118">How to list your application in the Azure Active Directory application gallery</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing)
