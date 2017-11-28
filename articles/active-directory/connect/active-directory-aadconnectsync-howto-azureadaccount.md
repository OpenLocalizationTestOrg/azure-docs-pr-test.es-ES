---
title: "Sincronización de Azure AD Connect: administración de la cuenta de servicio de Azure AD | Microsoft Docs"
description: "En este tema se describe cómo restaurar la cuenta de servicio de Azure AD."
services: active-directory
keywords: "AADSTS70002, AADSTS50054, Procedimiento para restablecer la contraseña de la cuenta de servicio del conector de Azure AD Connect Sync"
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
ms.openlocfilehash: 8e9e8192ee4fcb636b5be91d2616acbc9120c8c0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-how-to-manage-the-azure-ad-service-account"></a><span data-ttu-id="29fb3-104">Sincronización de Azure AD Connect: administración de la cuenta de servicio de Azure AD</span><span class="sxs-lookup"><span data-stu-id="29fb3-104">Azure AD Connect sync: How to manage the Azure AD service account</span></span>
<span data-ttu-id="29fb3-105">Se supone que la cuenta de servicio utilizada por el conector de Azure AD está libre de servicio.</span><span class="sxs-lookup"><span data-stu-id="29fb3-105">The service account used by the Azure AD Connector is supposed to be service free.</span></span> <span data-ttu-id="29fb3-106">Si necesita restablecer sus credenciales, este tema le interesa.</span><span class="sxs-lookup"><span data-stu-id="29fb3-106">If you need to reset its credentials, then this topic is for you.</span></span> <span data-ttu-id="29fb3-107">Por ejemplo, si un administrador global ha restablecido la contraseña por error en la cuenta de servicio mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="29fb3-107">For example, if a Global Administrator has by mistake reset the password on the service account using PowerShell.</span></span>

## <a name="reset-the-credentials"></a><span data-ttu-id="29fb3-108">Restablecimiento de las credenciales</span><span class="sxs-lookup"><span data-stu-id="29fb3-108">Reset the credentials</span></span>
<span data-ttu-id="29fb3-109">Si la cuenta de servicio definida en el conector de Azure AD no puede ponerse en contacto con Azure AD debido a problemas de autenticación, se puede restablecer la contraseña.</span><span class="sxs-lookup"><span data-stu-id="29fb3-109">If the service account defined on the Azure AD Connector cannot contact Azure AD due to authentication problems, the password can be reset.</span></span>

1. <span data-ttu-id="29fb3-110">Inicie sesión en el servidor de Azure AD Connect Sync e inicie PowerShell.</span><span class="sxs-lookup"><span data-stu-id="29fb3-110">Sign in to the Azure AD Connect sync server and start PowerShell.</span></span>
2. <span data-ttu-id="29fb3-111">Ejecute `Add-ADSyncAADServiceAccount`.</span><span class="sxs-lookup"><span data-stu-id="29fb3-111">Run `Add-ADSyncAADServiceAccount`.</span></span>  
   <span data-ttu-id="29fb3-112">![Cmdlet addadsyncaadserviceaccount de PowerShell](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span><span class="sxs-lookup"><span data-stu-id="29fb3-112">![PowerShell cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span></span>
3. <span data-ttu-id="29fb3-113">Proporcione las credenciales de administrador global de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29fb3-113">Provide Azure AD Global admin credentials.</span></span>

<span data-ttu-id="29fb3-114">Este cmdlet restablecerá la contraseña de la cuenta de servicio y la actualizará en Azure AD y en el motor de sincronización.</span><span class="sxs-lookup"><span data-stu-id="29fb3-114">This cmdlet resets the password for the service account and update it both in Azure AD and in the sync engine.</span></span>

## <a name="known-issues-these-steps-can-solve"></a><span data-ttu-id="29fb3-115">Problemas conocidos que pueden solucionarse siguiendo estos pasos</span><span class="sxs-lookup"><span data-stu-id="29fb3-115">Known issues these steps can solve</span></span>
<span data-ttu-id="29fb3-116">Esta sección es una lista de los errores notificados por clientes que se solucionaron mediante un restablecimiento de las credenciales de la cuenta de servicio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29fb3-116">This section is a list of errors reported by customers that were fixed by a credentials reset on the Azure AD service account.</span></span>

- - -
<span data-ttu-id="29fb3-117">Evento 6900</span><span class="sxs-lookup"><span data-stu-id="29fb3-117">Event 6900</span></span>  
<span data-ttu-id="29fb3-118">El servidor encontró un error inesperado al procesar una notificación de cambio de contraseña:</span><span class="sxs-lookup"><span data-stu-id="29fb3-118">The server encountered an unexpected error while processing a password change notification:</span></span>  
<span data-ttu-id="29fb3-119">AADSTS70002: error al validar las credenciales.</span><span class="sxs-lookup"><span data-stu-id="29fb3-119">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="29fb3-120">AADSTS50054: se utilizó una contraseña antigua para realizar la autenticación.</span><span class="sxs-lookup"><span data-stu-id="29fb3-120">AADSTS50054: Old password is used for authentication.</span></span>

- - -
<span data-ttu-id="29fb3-121">Evento 659</span><span class="sxs-lookup"><span data-stu-id="29fb3-121">Event 659</span></span>  
<span data-ttu-id="29fb3-122">Error al recuperar la configuración de sincronización de directivas de contraseña.</span><span class="sxs-lookup"><span data-stu-id="29fb3-122">Error while retrieving password policy sync configuration.</span></span> <span data-ttu-id="29fb3-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span><span class="sxs-lookup"><span data-stu-id="29fb3-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span></span>  
<span data-ttu-id="29fb3-124">AADSTS70002: error al validar las credenciales.</span><span class="sxs-lookup"><span data-stu-id="29fb3-124">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="29fb3-125">AADSTS50054: se utilizó una contraseña antigua para realizar la autenticación.</span><span class="sxs-lookup"><span data-stu-id="29fb3-125">AADSTS50054: Old password is used for authentication.</span></span>

## <a name="next-steps"></a><span data-ttu-id="29fb3-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="29fb3-126">Next steps</span></span>
<span data-ttu-id="29fb3-127">**Temas de introducción**</span><span class="sxs-lookup"><span data-stu-id="29fb3-127">**Overview topics**</span></span>

* [<span data-ttu-id="29fb3-128">Sincronización de Azure AD Connect: comprender y personalizar la sincronización</span><span class="sxs-lookup"><span data-stu-id="29fb3-128">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="29fb3-129">Integración de las identidades locales con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="29fb3-129">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

