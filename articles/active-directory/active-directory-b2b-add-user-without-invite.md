---
title: "Incorporación de usuarios de colaboración B2B a Azure Active Directory sin invitación | Microsoft Docs"
description: "Puede permitir que un usuario invitado agregue otros usuarios invitados a Azure AD sin canjear una invitación en Colaboración de Azure Active Directory B2B."
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
ms.openlocfilehash: 91b9477cdb679851e7d8d2942c06999a05f64e46
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="add-b2b-collaboration-guest-users-without-an-invitation"></a><span data-ttu-id="e4fd1-103">Incorporación de usuarios de colaboración B2B sin invitación</span><span class="sxs-lookup"><span data-stu-id="e4fd1-103">Add B2B collaboration guest users without an invitation</span></span>

<span data-ttu-id="e4fd1-104">Puede permitir que a un usuario, por ejemplo, un representante del asociado comercial, agregue a los usuarios del asociado a su organización sin necesidad de canjear invitaciones.</span><span class="sxs-lookup"><span data-stu-id="e4fd1-104">You can allow a user, such as a partner representative, to add users from the partner to your organization without needing invitations to be redeemed.</span></span> <span data-ttu-id="e4fd1-105">Todo lo que debe hacer es conceder a ese usuario privilegios de enumeración en el directorio que esté usando para la organización de asociado.</span><span class="sxs-lookup"><span data-stu-id="e4fd1-105">All you must do is grant that user enumeration privileges in the directory you're using for the partner org.</span></span> 

<span data-ttu-id="e4fd1-106">Conceda estos privilegios cuando se den estas condiciones:</span><span class="sxs-lookup"><span data-stu-id="e4fd1-106">Grant these privileges when:</span></span>

1. <span data-ttu-id="e4fd1-107">Un usuario de la organización anfitriona (por ejemplo, WoodGrove) invita a un usuario de la organización asociada (por ejemplo, Sam@litware.com) como invitado.</span><span class="sxs-lookup"><span data-stu-id="e4fd1-107">A user in the host organization (for example, WoodGrove) invites one user from the partner organization (for example, Sam@litware.com) as Guest.</span></span>
2. <span data-ttu-id="e4fd1-108">El administrador de la organización anfitriona configura directivas que permiten a Sam identificar y agregar otros usuarios de la organización del asociado (Litware).</span><span class="sxs-lookup"><span data-stu-id="e4fd1-108">The admin in the host organization sets up policies that allow Sam to identify and add other users from the partner organization (Litware).</span></span>
3. <span data-ttu-id="e4fd1-109">Ahora, Sam puede agregar otros usuarios de Litware al directorio, los grupos o las aplicaciones de WoodGrove sin necesidad de canjear invitaciones.</span><span class="sxs-lookup"><span data-stu-id="e4fd1-109">Now Sam can add other users from Litware to the WoodGrove directory, groups, or applications without needing invitations to be redeemed.</span></span> <span data-ttu-id="e4fd1-110">Si Sam tiene los privilegios de enumeración adecuados en Litware, se hará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="e4fd1-110">If Sam has the appropriate enumeration privileges in Litware, it happens automatically.</span></span>

### <a name="next-steps"></a><span data-ttu-id="e4fd1-111">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e4fd1-111">Next steps</span></span>

<span data-ttu-id="e4fd1-112">Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="e4fd1-112">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="e4fd1-113">¿Qué es la colaboración B2B de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="e4fd1-113">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="e4fd1-114">¿Cómo agregan los administradores de Azure Active Directory usuarios de colaboración B2B?</span><span class="sxs-lookup"><span data-stu-id="e4fd1-114">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="e4fd1-115">¿Cómo agregan los trabajadores de la información usuarios de colaboración B2B?</span><span class="sxs-lookup"><span data-stu-id="e4fd1-115">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="e4fd1-116">Los elementos del correo electrónico de invitación de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="e4fd1-116">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="e4fd1-117">Canje de invitación de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="e4fd1-117">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="e4fd1-118">Concesión de licencias de colaboración B2B de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e4fd1-118">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="e4fd1-119">Solución de problemas de colaboración B2B de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e4fd1-119">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="e4fd1-120">Preguntas frecuentes sobre la colaboración B2B de Azure Active Directory (P+F)</span><span class="sxs-lookup"><span data-stu-id="e4fd1-120">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="e4fd1-121">Personalización y API de colaboración B2B de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e4fd1-121">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="e4fd1-122">Autenticación multifactor para usuarios de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="e4fd1-122">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="e4fd1-123">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e4fd1-123">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)