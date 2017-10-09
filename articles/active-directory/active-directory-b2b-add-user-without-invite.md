---
title: "aaaAdd B2B colaboración a los usuarios tooAzure Active Directory sin una invitación | Documentos de Microsoft"
description: "Puede permitir que un usuario invitado agregar otro tooyour de los usuarios invitados Azure AD sin canjear una invitación en colaboración B2B de Azure Active Directory."
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
ms.openlocfilehash: 459d99b9f856a35973d1b2cbfabdc23fe40c8f44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-b2b-collaboration-guest-users-without-an-invitation"></a><span data-ttu-id="79e04-103">Incorporación de usuarios de colaboración B2B sin invitación</span><span class="sxs-lookup"><span data-stu-id="79e04-103">Add B2B collaboration guest users without an invitation</span></span>

<span data-ttu-id="79e04-104">Puede permitir que a un usuario, como un socio comercial representativo, tooadd los usuarios de hello asociado tooyour organización sin necesidad de toobe invitaciones canjeado.</span><span class="sxs-lookup"><span data-stu-id="79e04-104">You can allow a user, such as a partner representative, tooadd users from hello partner tooyour organization without needing invitations toobe redeemed.</span></span> <span data-ttu-id="79e04-105">Todo lo que debe hacer es conceder ese usuario privilegios de enumeración en directorio de Hola que está usando para org de hello asociado.</span><span class="sxs-lookup"><span data-stu-id="79e04-105">All you must do is grant that user enumeration privileges in hello directory you're using for hello partner org.</span></span> 

<span data-ttu-id="79e04-106">Conceda estos privilegios cuando se den estas condiciones:</span><span class="sxs-lookup"><span data-stu-id="79e04-106">Grant these privileges when:</span></span>

1. <span data-ttu-id="79e04-107">Un usuario de hello host organización (por ejemplo, WoodGrove) invita a un usuario de la organización del asociado de hello (por ejemplo, Sam@litware.com) como invitado.</span><span class="sxs-lookup"><span data-stu-id="79e04-107">A user in hello host organization (for example, WoodGrove) invites one user from hello partner organization (for example, Sam@litware.com) as Guest.</span></span>
2. <span data-ttu-id="79e04-108">Hola, Administrador de organización de host de hello configura directivas que permiten Sam tooidentify y agregar otros usuarios de la organización del asociado de hello (Litware).</span><span class="sxs-lookup"><span data-stu-id="79e04-108">hello admin in hello host organization sets up policies that allow Sam tooidentify and add other users from hello partner organization (Litware).</span></span>
3. <span data-ttu-id="79e04-109">Sam ahora puede agregar otros usuarios del directorio de Litware toohello WoodGrove, grupos o las aplicaciones sin necesidad de toobe invitaciones canjeado.</span><span class="sxs-lookup"><span data-stu-id="79e04-109">Now Sam can add other users from Litware toohello WoodGrove directory, groups, or applications without needing invitations toobe redeemed.</span></span> <span data-ttu-id="79e04-110">Si Sam tiene privilegios de la enumeración adecuada de hello en Litware, se produce automáticamente.</span><span class="sxs-lookup"><span data-stu-id="79e04-110">If Sam has hello appropriate enumeration privileges in Litware, it happens automatically.</span></span>

### <a name="next-steps"></a><span data-ttu-id="79e04-111">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="79e04-111">Next steps</span></span>

<span data-ttu-id="79e04-112">Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="79e04-112">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="79e04-113">¿Qué es la colaboración B2B de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="79e04-113">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="79e04-114">¿Cómo agregan los administradores de Azure Active Directory usuarios de colaboración B2B?</span><span class="sxs-lookup"><span data-stu-id="79e04-114">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="79e04-115">¿Cómo agregan los trabajadores de la información usuarios de colaboración B2B?</span><span class="sxs-lookup"><span data-stu-id="79e04-115">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="79e04-116">elementos de saludo de correo electrónico de invitación de colaboración B2B de hello</span><span class="sxs-lookup"><span data-stu-id="79e04-116">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="79e04-117">Canje de invitación de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="79e04-117">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="79e04-118">Concesión de licencias de colaboración B2B de Azure AD</span><span class="sxs-lookup"><span data-stu-id="79e04-118">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="79e04-119">Solución de problemas de colaboración B2B de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="79e04-119">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="79e04-120">Preguntas frecuentes sobre la colaboración B2B de Azure Active Directory (P+F)</span><span class="sxs-lookup"><span data-stu-id="79e04-120">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="79e04-121">Personalización y API de colaboración B2B de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="79e04-121">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="79e04-122">Autenticación multifactor para usuarios de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="79e04-122">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="79e04-123">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="79e04-123">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)