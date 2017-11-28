---
title: "asignación en Azure Active Directory las notificaciones de usuario de colaboración aaaB2B | Documentos de Microsoft"
description: "referencia de asignación de notificaciones para la colaboración B2B de Azure Active Directory"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 9e26085e91a6004b2f11286ae9c1df133bd47341
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="b2b-collaboration-user-claims-mapping-in-azure-active-directory"></a><span data-ttu-id="c02dd-103">Asignación de notificaciones de usuario de colaboración B2B de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c02dd-103">B2B collaboration user claims mapping in Azure Active Directory</span></span>

<span data-ttu-id="c02dd-104">Azure Active Directory (Azure AD) es compatible con personalizar las notificaciones de hello emitidas en el token SAML de Hola para los usuarios de la colaboración B2B.</span><span class="sxs-lookup"><span data-stu-id="c02dd-104">Azure Active Directory (Azure AD) supports customizing hello claims issued in hello SAML token for B2B collaboration users.</span></span> <span data-ttu-id="c02dd-105">Cuando un usuario autentica toohello aplicación, Azure AD emite una aplicación de toohello token de SAML que contiene información (o notificaciones) acerca del usuario de Hola que identifica de forma única a ellos.</span><span class="sxs-lookup"><span data-stu-id="c02dd-105">When a user authenticates toohello application, Azure AD issues a SAML token toohello app that contains information (or claims) about hello user that uniquely identifies them.</span></span> <span data-ttu-id="c02dd-106">De forma predeterminada, esto incluye el nombre de usuario, dirección de correo electrónico, nombre y apellido del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="c02dd-106">By default, this includes hello user's user name, email address, first name, and last name.</span></span> <span data-ttu-id="c02dd-107">Puede ver o editar notificaciones Hola enviados en la aplicación de toohello token de SAML en la ficha de atributos de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="c02dd-107">You can view or edit hello claims sent in hello SAML token toohello application under hello Attributes tab.</span></span>

<span data-ttu-id="c02dd-108">Hay dos razones posibles por las que puede necesitar notificaciones de hello tooedit emitidas en el token SAML de Hola.</span><span class="sxs-lookup"><span data-stu-id="c02dd-108">There are two possible reasons why you might need tooedit hello claims issued in hello SAML token.</span></span>

1. <span data-ttu-id="c02dd-109">aplicación Hello se ha escrito toorequire otro conjunto de notificaciones URI o valores de notificación</span><span class="sxs-lookup"><span data-stu-id="c02dd-109">hello application has been written toorequire a different set of claim URIs or claim values</span></span>

2. <span data-ttu-id="c02dd-110">La aplicación necesita toobe de notificación de NameIdentifier Hola algo distinto de nombre principal de usuario Hola almacenado en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c02dd-110">Your application requires hello NameIdentifier claim toobe something other than hello user principal name stored in Azure Active Directory.</span></span>

  ![Visualización de notificaciones en el token SAML](media/active-directory-b2b-claims-mapping/view-claims-in-saml-token.png)

<span data-ttu-id="c02dd-112">Para obtener información sobre cómo tooadd y editar notificaciones, consulte este artículo sobre la personalización de notificaciones, [personalizar las notificaciones emitidas en el token SAML de Hola para las aplicaciones previamente integradas en Azure Active Directory](develop/active-directory-saml-claims-customization.md).</span><span class="sxs-lookup"><span data-stu-id="c02dd-112">For information on how tooadd and edit claims, check out this article on claims customization, [Customizing claims issued in hello SAML token for pre-integrated apps in Azure Active Directory](develop/active-directory-saml-claims-customization.md).</span></span> <span data-ttu-id="c02dd-113">Para los usuarios de colaboración B2B, por motivos de seguridad, se evita realizar la asignación de NameID y UPD entre inquilinos.</span><span class="sxs-lookup"><span data-stu-id="c02dd-113">For B2B collaboration users, mapping NameID and UPN cross-tenant are prevented for security reasons.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c02dd-114">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c02dd-114">Next steps</span></span>

<span data-ttu-id="c02dd-115">Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="c02dd-115">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="c02dd-116">¿Qué es la colaboración B2B de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="c02dd-116">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="c02dd-117">Propiedades de usuario de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="c02dd-117">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="c02dd-118">Agregar un rol de tooa de usuario de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="c02dd-118">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="c02dd-119">Delegación de las invitaciones de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="c02dd-119">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="c02dd-120">Grupos dinámicos y colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="c02dd-120">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="c02dd-121">Código de colaboración B2B y ejemplos de PowerShell</span><span class="sxs-lookup"><span data-stu-id="c02dd-121">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="c02dd-122">Configuración de aplicaciones de SaaS para la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="c02dd-122">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="c02dd-123">Uso compartido externo de Office 365</span><span class="sxs-lookup"><span data-stu-id="c02dd-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="c02dd-124">Tokens de usuario de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="c02dd-124">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="c02dd-125">Limitaciones actuales de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="c02dd-125">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
