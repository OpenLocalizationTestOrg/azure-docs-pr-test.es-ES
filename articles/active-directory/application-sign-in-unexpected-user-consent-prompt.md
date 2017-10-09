---
title: "petición de consentimiento de aaaUnexpected al iniciar sesión en la aplicación tooan | Documentos de Microsoft"
description: "¿Cómo tootroubleshoot cuando un usuario ve una solicitud de consentimiento para una aplicación ha integrado con Azure AD que no esperaba"
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
ms.openlocfilehash: 32b7a5e6256faee0dcfe2e1644da3d3428812d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-consent-prompt-when-signing-in-tooan-application"></a><span data-ttu-id="5d079-103">Petición de consentimiento inesperado al iniciar sesión en la aplicación de tooan</span><span class="sxs-lookup"><span data-stu-id="5d079-103">Unexpected consent prompt when signing in tooan application</span></span>

<span data-ttu-id="5d079-104">Muchas aplicaciones que se integran con Azure Active Directory requieren recursos de toovarious de permisos en orden toorun.</span><span class="sxs-lookup"><span data-stu-id="5d079-104">Many applications that integrate with Azure Active Directory require permissions toovarious resources in order toorun.</span></span> <span data-ttu-id="5d079-105">Cuando estos recursos también están integrados con Azure Active Directory, tooaccess permisos ellos se solicita mediante hello Azure AD consentimiento framework.</span><span class="sxs-lookup"><span data-stu-id="5d079-105">When these resources are also integrated with Azure Active Directory, permissions tooaccess them is requested using hello Azure AD consent framework.</span></span> 

<span data-ttu-id="5d079-106">Esto produce una solicitud de consentimiento que se está mostrando Hola primera vez que se usa una aplicación, que suele ser una operación única.</span><span class="sxs-lookup"><span data-stu-id="5d079-106">This results in a consent prompt being shown hello first time an application is used, which is often a one-time operation.</span></span> 

## <a name="scenarios-in-which-users-see-consent-prompts"></a><span data-ttu-id="5d079-107">Escenarios en los que los usuarios ven solicitudes de consentimiento</span><span class="sxs-lookup"><span data-stu-id="5d079-107">Scenarios in which users see consent prompts</span></span>

<span data-ttu-id="5d079-108">Se pueden esperar más solicitudes en distintos escenarios:</span><span class="sxs-lookup"><span data-stu-id="5d079-108">Additional prompts can be expected in various scenarios:</span></span>

* <span data-ttu-id="5d079-109">conjunto de Hola de permisos requeridos por la aplicación hello ha cambiado.</span><span class="sxs-lookup"><span data-stu-id="5d079-109">hello set of permissions required by hello application have changed.</span></span>

* <span data-ttu-id="5d079-110">usuario de Hola que originalmente dado su consentimiento toohello aplicación no era administrador, y ahora un usuario diferente (no administrativos) utiliza aplicación hello para hello primera vez.</span><span class="sxs-lookup"><span data-stu-id="5d079-110">hello user who originally consented toohello application was not an administrator, and now a different (non-admin) User is using hello application for hello first time.</span></span>

* <span data-ttu-id="5d079-111">usuario de Hola que originalmente dado su consentimiento toohello aplicación era administrador, pero no dar el consentimiento en nombre de toda la organización Hola.</span><span class="sxs-lookup"><span data-stu-id="5d079-111">hello user who originally consented toohello application was an administrator, but they did not consent on-behalf of hello entire organization.</span></span>

* <span data-ttu-id="5d079-112">está usando la aplicación Hello [consentimiento incremental y dinámico](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) toorequest de permisos adicionales después de haberse otorgado inicialmente consentimiento.</span><span class="sxs-lookup"><span data-stu-id="5d079-112">hello application is using [incremental and dynamic consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) toorequest additional permissions after consent was initially granted.</span></span> <span data-ttu-id="5d079-113">Esto se suele usar cuando las características opcionales de una aplicación adicional requieren permisos más allá de los que se requieren para la funcionalidad de línea base.</span><span class="sxs-lookup"><span data-stu-id="5d079-113">This is often used when optional features of an application additional require permissions beyond those required for baseline functionality.</span></span>

* <span data-ttu-id="5d079-114">Se ha revocado el consentimiento después de que inicialmente se otorgó.</span><span class="sxs-lookup"><span data-stu-id="5d079-114">Consent was revoked after being granted initially.</span></span>

* <span data-ttu-id="5d079-115">desarrollador de Hello configuró Hola aplicación toorequire una solicitud de consentimiento cada vez que se utiliza (Nota: esto no es recomendable).</span><span class="sxs-lookup"><span data-stu-id="5d079-115">hello developer has configured hello application toorequire a consent prompt every time it is used (note: this is not best practice).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d079-116">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5d079-116">Next steps</span></span>

-   [<span data-ttu-id="5d079-117">Aplicaciones, permisos y consentimiento en Azure Active Directory (punto de conexión v1.0)</span><span class="sxs-lookup"><span data-stu-id="5d079-117">Apps, permissions, and consent in Azure Active Directory (v1.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)

-   [<span data-ttu-id="5d079-118">Ámbitos, permisos y consentimiento de hello Azure Active Directory (extremo v2.0)</span><span class="sxs-lookup"><span data-stu-id="5d079-118">Scopes, permissions, and consent in hello Azure Active Directory (v2.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


