---
title: "Petición de consentimiento inesperada al iniciar sesión en una aplicación | Microsoft Docs"
description: "Cómo solucionar problemas cuando un usuario ve una solicitud de consentimiento para una aplicación que ha integrado con Azure AD que no esperaba"
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
ms.openlocfilehash: e5b823e1251a7221f73efe6838d439f827f9665d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="unexpected-consent-prompt-when-signing-in-to-an-application"></a><span data-ttu-id="99ef0-103">Petición de consentimiento inesperada al iniciar sesión en una aplicación</span><span class="sxs-lookup"><span data-stu-id="99ef0-103">Unexpected consent prompt when signing in to an application</span></span>

<span data-ttu-id="99ef0-104">Muchas aplicaciones que se integran con Azure Active Directory requieren permisos para acceder a diversos recursos para poder ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="99ef0-104">Many applications that integrate with Azure Active Directory require permissions to various resources in order to run.</span></span> <span data-ttu-id="99ef0-105">Cuando estos recursos también se integran con Azure Active Directory, suelen solicitarse permisos para acceder a ellos mediante el marco de consentimiento de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99ef0-105">When these resources are also integrated with Azure Active Directory, permissions to access them is requested using the Azure AD consent framework.</span></span> 

<span data-ttu-id="99ef0-106">Esto da como resultado que la primera vez que se usa una aplicación aparece una solicitud de consentimiento, que suele ser una operación única.</span><span class="sxs-lookup"><span data-stu-id="99ef0-106">This results in a consent prompt being shown the first time an application is used, which is often a one-time operation.</span></span> 

## <a name="scenarios-in-which-users-see-consent-prompts"></a><span data-ttu-id="99ef0-107">Escenarios en los que los usuarios ven solicitudes de consentimiento</span><span class="sxs-lookup"><span data-stu-id="99ef0-107">Scenarios in which users see consent prompts</span></span>

<span data-ttu-id="99ef0-108">Se pueden esperar más solicitudes en distintos escenarios:</span><span class="sxs-lookup"><span data-stu-id="99ef0-108">Additional prompts can be expected in various scenarios:</span></span>

* <span data-ttu-id="99ef0-109">El conjunto de permisos que requiere la aplicación ha cambiado.</span><span class="sxs-lookup"><span data-stu-id="99ef0-109">The set of permissions required by the application have changed.</span></span>

* <span data-ttu-id="99ef0-110">El usuario que originalmente otorgó su consentimiento a la aplicación no era administrador, y ahora un usuario diferente (no administrador) está usando la aplicación por primera vez.</span><span class="sxs-lookup"><span data-stu-id="99ef0-110">The user who originally consented to the application was not an administrator, and now a different (non-admin) User is using the application for the first time.</span></span>

* <span data-ttu-id="99ef0-111">El usuario que originalmente otorgó su consentimiento a la aplicación era administrador, pero no otorgó el consentimiento en nombre de toda la organización.</span><span class="sxs-lookup"><span data-stu-id="99ef0-111">The user who originally consented to the application was an administrator, but they did not consent on-behalf of the entire organization.</span></span>

* <span data-ttu-id="99ef0-112">La aplicación usa [consentimiento incremental y dinámico](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) para solicitar permisos adicionales después de haberse otorgado inicialmente el consentimiento.</span><span class="sxs-lookup"><span data-stu-id="99ef0-112">The application is using [incremental and dynamic consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) to request additional permissions after consent was initially granted.</span></span> <span data-ttu-id="99ef0-113">Esto se suele usar cuando las características opcionales de una aplicación adicional requieren permisos más allá de los que se requieren para la funcionalidad de línea base.</span><span class="sxs-lookup"><span data-stu-id="99ef0-113">This is often used when optional features of an application additional require permissions beyond those required for baseline functionality.</span></span>

* <span data-ttu-id="99ef0-114">Se ha revocado el consentimiento después de que inicialmente se otorgó.</span><span class="sxs-lookup"><span data-stu-id="99ef0-114">Consent was revoked after being granted initially.</span></span>

* <span data-ttu-id="99ef0-115">El desarrollador ha configurado la aplicación para que requiera una solicitud de consentimiento cada vez que se utilice (nota: esto no es recomendable).</span><span class="sxs-lookup"><span data-stu-id="99ef0-115">The developer has configured the application to require a consent prompt every time it is used (note: this is not best practice).</span></span>

## <a name="next-steps"></a><span data-ttu-id="99ef0-116">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="99ef0-116">Next steps</span></span>

-   [<span data-ttu-id="99ef0-117">Aplicaciones, permisos y consentimiento en Azure Active Directory (punto de conexión v1.0)</span><span class="sxs-lookup"><span data-stu-id="99ef0-117">Apps, permissions, and consent in Azure Active Directory (v1.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)

-   [<span data-ttu-id="99ef0-118">Ámbitos, permisos y consentimiento en Azure Active Directory (punto de conexión v2.0)</span><span class="sxs-lookup"><span data-stu-id="99ef0-118">Scopes, permissions, and consent in the Azure Active Directory (v2.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


