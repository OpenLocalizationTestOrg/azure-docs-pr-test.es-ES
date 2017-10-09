---
title: 'Azure AD Connect sync: la cuenta de servicio toomanage hello Azure AD | Documentos de Microsoft'
description: Este tema documenta la cuenta de servicio toorestore hello Azure AD.
services: active-directory
keywords: "AADSTS70002, AADSTS50054, cómo tooreset Hola contraseña de hello Azure AD Connect sync cuenta de servicio de conector"
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 6077043a-27f1-4304-a44b-81dc46620f24
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: e563518eae173de42a1d40bb5a76e63f29f9da42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-how-toomanage-hello-azure-ad-service-account"></a><span data-ttu-id="e69d9-104">Azure AD Connect sync: la cuenta de servicio toomanage hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e69d9-104">Azure AD Connect sync: How toomanage hello Azure AD service account</span></span>
<span data-ttu-id="e69d9-105">cuenta de servicio de Hello usada por hello conector de Azure AD se supone que toobe servicio gratuito.</span><span class="sxs-lookup"><span data-stu-id="e69d9-105">hello service account used by hello Azure AD Connector is supposed toobe service free.</span></span> <span data-ttu-id="e69d9-106">Si necesita tooreset sus credenciales, este tema es para usted.</span><span class="sxs-lookup"><span data-stu-id="e69d9-106">If you need tooreset its credentials, then this topic is for you.</span></span> <span data-ttu-id="e69d9-107">Por ejemplo, si un administrador Global tiene por error Hola de restablecimiento de contraseñas de cuenta de servicio de hello mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e69d9-107">For example, if a Global Administrator has by mistake reset hello password on hello service account using PowerShell.</span></span>

## <a name="reset-hello-credentials"></a><span data-ttu-id="e69d9-108">Restablecer credenciales de Hola</span><span class="sxs-lookup"><span data-stu-id="e69d9-108">Reset hello credentials</span></span>
<span data-ttu-id="e69d9-109">Si la cuenta de servicio de hello definida en hello conector de Azure AD no puede ponerse en contacto con Azure AD debido a problemas de tooauthentication, se puede restablecer contraseña Hola.</span><span class="sxs-lookup"><span data-stu-id="e69d9-109">If hello service account defined on hello Azure AD Connector cannot contact Azure AD due tooauthentication problems, hello password can be reset.</span></span>

1. <span data-ttu-id="e69d9-110">Inicie sesión en el servidor de sincronización de Azure AD Connect toohello e inicie PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e69d9-110">Sign in toohello Azure AD Connect sync server and start PowerShell.</span></span>
2. <span data-ttu-id="e69d9-111">Ejecute `Add-ADSyncAADServiceAccount`.</span><span class="sxs-lookup"><span data-stu-id="e69d9-111">Run `Add-ADSyncAADServiceAccount`.</span></span>  
   <span data-ttu-id="e69d9-112">![Cmdlet addadsyncaadserviceaccount de PowerShell](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span><span class="sxs-lookup"><span data-stu-id="e69d9-112">![PowerShell cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span></span>
3. <span data-ttu-id="e69d9-113">Proporcione las credenciales de administrador global de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e69d9-113">Provide Azure AD Global admin credentials.</span></span>

<span data-ttu-id="e69d9-114">Este cmdlet restablece la contraseña de hello para la cuenta de servicio de Hola y actualizarla en Azure AD y en el motor de sincronización de Hola.</span><span class="sxs-lookup"><span data-stu-id="e69d9-114">This cmdlet resets hello password for hello service account and update it both in Azure AD and in hello sync engine.</span></span>

## <a name="known-issues-these-steps-can-solve"></a><span data-ttu-id="e69d9-115">Problemas conocidos que pueden solucionarse siguiendo estos pasos</span><span class="sxs-lookup"><span data-stu-id="e69d9-115">Known issues these steps can solve</span></span>
<span data-ttu-id="e69d9-116">Esta sección es una lista de errores notificados por los clientes que se corrigieron por un credenciales restablecer en hello cuenta de servicio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e69d9-116">This section is a list of errors reported by customers that were fixed by a credentials reset on hello Azure AD service account.</span></span>

- - -
<span data-ttu-id="e69d9-117">Evento 6900</span><span class="sxs-lookup"><span data-stu-id="e69d9-117">Event 6900</span></span>  
<span data-ttu-id="e69d9-118">servidor de Hello encontró un error inesperado al procesar una notificación de cambio de contraseña:</span><span class="sxs-lookup"><span data-stu-id="e69d9-118">hello server encountered an unexpected error while processing a password change notification:</span></span>  
<span data-ttu-id="e69d9-119">AADSTS70002: error al validar las credenciales.</span><span class="sxs-lookup"><span data-stu-id="e69d9-119">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="e69d9-120">AADSTS50054: se utilizó una contraseña antigua para realizar la autenticación.</span><span class="sxs-lookup"><span data-stu-id="e69d9-120">AADSTS50054: Old password is used for authentication.</span></span>

- - -
<span data-ttu-id="e69d9-121">Evento 659</span><span class="sxs-lookup"><span data-stu-id="e69d9-121">Event 659</span></span>  
<span data-ttu-id="e69d9-122">Error al recuperar la configuración de sincronización de directivas de contraseña.</span><span class="sxs-lookup"><span data-stu-id="e69d9-122">Error while retrieving password policy sync configuration.</span></span> <span data-ttu-id="e69d9-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span><span class="sxs-lookup"><span data-stu-id="e69d9-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span></span>  
<span data-ttu-id="e69d9-124">AADSTS70002: error al validar las credenciales.</span><span class="sxs-lookup"><span data-stu-id="e69d9-124">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="e69d9-125">AADSTS50054: se utilizó una contraseña antigua para realizar la autenticación.</span><span class="sxs-lookup"><span data-stu-id="e69d9-125">AADSTS50054: Old password is used for authentication.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e69d9-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e69d9-126">Next steps</span></span>
<span data-ttu-id="e69d9-127">**Temas de introducción**</span><span class="sxs-lookup"><span data-stu-id="e69d9-127">**Overview topics**</span></span>

* [<span data-ttu-id="e69d9-128">Sincronización de Azure AD Connect: comprender y personalizar la sincronización</span><span class="sxs-lookup"><span data-stu-id="e69d9-128">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="e69d9-129">Integración de las identidades locales con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e69d9-129">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

