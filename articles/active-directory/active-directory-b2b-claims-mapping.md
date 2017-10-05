---
title: "Asignación de notificaciones de usuario de colaboración B2B de Azure Active Directory | Microsoft Docs"
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
ms.openlocfilehash: 5f8559450b24effd40a38879aeae3a8dd03944a3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="b2b-collaboration-user-claims-mapping-in-azure-active-directory"></a><span data-ttu-id="c1c22-103">Asignación de notificaciones de usuario de colaboración B2B de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c1c22-103">B2B collaboration user claims mapping in Azure Active Directory</span></span>

<span data-ttu-id="c1c22-104">Azure Active Directory (Azure AD) admite la personalización de las notificaciones emitidas en el token SAML para los usuarios de colaboración B2B.</span><span class="sxs-lookup"><span data-stu-id="c1c22-104">Azure Active Directory (Azure AD) supports customizing the claims issued in the SAML token for B2B collaboration users.</span></span> <span data-ttu-id="c1c22-105">Cuando un usuario se autentique en la aplicación, Azure AD emitirá un token SAML a la aplicación que contiene información (o notificaciones) sobre el usuario que lo identifica de forma única.</span><span class="sxs-lookup"><span data-stu-id="c1c22-105">When a user authenticates to the application, Azure AD issues a SAML token to the app that contains information (or claims) about the user that uniquely identifies them.</span></span> <span data-ttu-id="c1c22-106">De forma predeterminada, dicha información incluye el nombre de usuario, la dirección de correo electrónico, el nombre y los apellidos del usuario.</span><span class="sxs-lookup"><span data-stu-id="c1c22-106">By default, this includes the user's user name, email address, first name, and last name.</span></span> <span data-ttu-id="c1c22-107">Las notificaciones enviadas en el token SAML a la aplicación se pueden ver o editar en la pestaña Atributos.</span><span class="sxs-lookup"><span data-stu-id="c1c22-107">You can view or edit the claims sent in the SAML token to the application under the Attributes tab.</span></span>

<span data-ttu-id="c1c22-108">Hay dos razones posibles por qué tendría que editar las notificaciones emitidas en el token SAML.</span><span class="sxs-lookup"><span data-stu-id="c1c22-108">There are two possible reasons why you might need to edit the claims issued in the SAML token.</span></span>

1. <span data-ttu-id="c1c22-109">La aplicación se ha creado para requerir un conjunto diferente de URI o valores de notificación.</span><span class="sxs-lookup"><span data-stu-id="c1c22-109">The application has been written to require a different set of claim URIs or claim values</span></span>

2. <span data-ttu-id="c1c22-110">La aplicación requiere que la notificación NameIdentifier tenga un valor que no sea el del nombre principal de usuario almacenado en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c1c22-110">Your application requires the NameIdentifier claim to be something other than the user principal name stored in Azure Active Directory.</span></span>

  ![Visualización de notificaciones en el token SAML](media/active-directory-b2b-claims-mapping/view-claims-in-saml-token.png)

<span data-ttu-id="c1c22-112">Para obtener información sobre cómo agregar y editar notificaciones, consulte este artículo sobre la personalización de notificaciones: [Personalización de notificaciones emitidas en el token SAML para aplicaciones previamente integradas en Azure Active Directory](develop/active-directory-saml-claims-customization.md).</span><span class="sxs-lookup"><span data-stu-id="c1c22-112">For information on how to add and edit claims, check out this article on claims customization, [Customizing claims issued in the SAML token for pre-integrated apps in Azure Active Directory](develop/active-directory-saml-claims-customization.md).</span></span> <span data-ttu-id="c1c22-113">Para los usuarios de colaboración B2B, por motivos de seguridad, se evita realizar la asignación de NameID y UPD entre inquilinos.</span><span class="sxs-lookup"><span data-stu-id="c1c22-113">For B2B collaboration users, mapping NameID and UPN cross-tenant are prevented for security reasons.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c1c22-114">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c1c22-114">Next steps</span></span>

<span data-ttu-id="c1c22-115">Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="c1c22-115">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="c1c22-116">¿Qué es la colaboración B2B de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="c1c22-116">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="c1c22-117">Propiedades de usuario de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="c1c22-117">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="c1c22-118">Incorporación de usuarios de colaboración B2B a un rol</span><span class="sxs-lookup"><span data-stu-id="c1c22-118">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="c1c22-119">Delegación de las invitaciones de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="c1c22-119">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="c1c22-120">Grupos dinámicos y colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="c1c22-120">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="c1c22-121">Código de colaboración B2B y ejemplos de PowerShell</span><span class="sxs-lookup"><span data-stu-id="c1c22-121">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="c1c22-122">Configuración de aplicaciones de SaaS para la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="c1c22-122">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="c1c22-123">Uso compartido externo de Office 365</span><span class="sxs-lookup"><span data-stu-id="c1c22-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="c1c22-124">Tokens de usuario de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="c1c22-124">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="c1c22-125">Limitaciones actuales de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="c1c22-125">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
