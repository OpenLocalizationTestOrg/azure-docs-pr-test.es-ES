---
title: "Solución de problemas de pertenencia dinámica para grupos| Microsoft Docs"
description: "Solución de problemas para la pertenencia dinámica para grupos en Azure AD."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 89bb04b6-a379-49c2-8465-fe386641816a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: 32947e8cc69c9a48d9a285bf0a37ab3398571f86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a><span data-ttu-id="3eaff-103">Solución de problemas relacionados con las pertenencias dinámicas para grupos</span><span class="sxs-lookup"><span data-stu-id="3eaff-103">Troubleshooting dynamic memberships for groups</span></span>
<span data-ttu-id="3eaff-104">**He configurado una regla en un grupo pero las pertenencias no se actualizan en el grupo**.</span><span class="sxs-lookup"><span data-stu-id="3eaff-104">**I configured a rule on a group but no memberships get updated in the group**</span></span><br/><span data-ttu-id="3eaff-105">Compruebe que la opción **Habilitar la administración de grupos delegados** está establecida en **Sí** en la pestaña **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="3eaff-105">Verify that the **Enable delegated group management** setting is set to **Yes** in the **Configure** tab.</span></span> <span data-ttu-id="3eaff-106">Esta opción solo se verá si ha iniciado sesión como un usuario a quien se ha asignado una licencia de Active Directory Premium de Azure.</span><span class="sxs-lookup"><span data-stu-id="3eaff-106">You will see this setting only if you are signed in as a user to whom an Azure Active Directory Premium license is assigned.</span></span> <span data-ttu-id="3eaff-107">Compruebe los valores de atributos de usuario en la regla: ¿hay usuarios que cumplen la regla?</span><span class="sxs-lookup"><span data-stu-id="3eaff-107">Verify the values for user attributes on the rule: are there users that satisfy the rule?</span></span>

<span data-ttu-id="3eaff-108">**He configurado una regla, pero ahora se han quitado los miembros existentes de la regla**.</span><span class="sxs-lookup"><span data-stu-id="3eaff-108">**I configured a rule, but now the existing members of the rule are removed**</span></span><br/><span data-ttu-id="3eaff-109">Este es el comportamiento esperado.</span><span class="sxs-lookup"><span data-stu-id="3eaff-109">This is expected behavior.</span></span> <span data-ttu-id="3eaff-110">Los miembros existentes del grupo se quitan cuando una regla se habilita o se cambia.</span><span class="sxs-lookup"><span data-stu-id="3eaff-110">Existing members of the group are removed when a rule is enabled or changed.</span></span> <span data-ttu-id="3eaff-111">Los usuarios devueltos tras la evaluación de la regla se agregan como miembros al grupo.</span><span class="sxs-lookup"><span data-stu-id="3eaff-111">The users returned from evaluation of the rule are added as members to the group.</span></span>     

<span data-ttu-id="3eaff-112">**No veo los cambios en la pertenencia al instante cuando agrego o cambio una regla, ¿por qué pasa esto?**</span><span class="sxs-lookup"><span data-stu-id="3eaff-112">**I don’t see membership changes instantly when I add or change a rule, why not?**</span></span><br/><span data-ttu-id="3eaff-113">La evaluación de pertenencia dedicada se realiza periódicamente en un proceso asincrónico en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="3eaff-113">Dedicated membership evaluation is done periodically in an asynchronous background process.</span></span> <span data-ttu-id="3eaff-114">La duración del proceso viene determinada por el número de usuarios del directorio y el tamaño del grupo creado como resultado de la regla.</span><span class="sxs-lookup"><span data-stu-id="3eaff-114">How long the process takes is determined by the number of users in your directory and the size of the group created as a result of the rule.</span></span> <span data-ttu-id="3eaff-115">Normalmente, los directorios con un número pequeño de usuarios verán los cambios en la pertenencia al grupo en unos pocos minutos.</span><span class="sxs-lookup"><span data-stu-id="3eaff-115">Typically, directories with small numbers of users will see the group membership changes in less than a few minutes.</span></span> <span data-ttu-id="3eaff-116">Los directorios con un gran número de usuarios pueden tardar 30 minutos o más en completarse.</span><span class="sxs-lookup"><span data-stu-id="3eaff-116">Directories with a large number of users can take 30 minutes or longer to populate.</span></span>

### <a name="next-steps"></a><span data-ttu-id="3eaff-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3eaff-117">Next steps</span></span>
<span data-ttu-id="3eaff-118">Estos artículos proporcionan información adicional sobre Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3eaff-118">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="3eaff-119">Administración del acceso a los recursos con grupos de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3eaff-119">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="3eaff-120">Índice de artículos sobre la administración de aplicaciones en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3eaff-120">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="3eaff-121">¿Qué es Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3eaff-121">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="3eaff-122">Integración de las identidades locales con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3eaff-122">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
