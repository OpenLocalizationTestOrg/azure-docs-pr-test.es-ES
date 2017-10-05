---
title: Asistente para seguridad de Privileged Identity Management de Azure AD
description: "La primera vez que use la extensión de Privileged Identity Management de Azure Active Directory, aparecerá un asistente para seguridad. En este artículo se describen los pasos para usar al asistente."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: a53a3719-8cc7-4fc7-8164-aafca192871b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: 260d178f3d8158411b3ad266e3b0d15edbebc722
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-security-wizard-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="5429f-104">Uso del Asistente para seguridad de Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="5429f-104">Using the security wizard in Azure AD Privileged Identity Management</span></span> 
<span data-ttu-id="5429f-105">Si es la primera persona que ejecuta Privileged Identity Management (PIM) de Azure en su organización, se le presentará un asistente.</span><span class="sxs-lookup"><span data-stu-id="5429f-105">If you're the first person to run Azure Privileged Identity Management (PIM) for your organization, you will be presented with a wizard.</span></span> <span data-ttu-id="5429f-106">El asistente le ayuda a comprender los riesgos de seguridad de las identidades con privilegios y a usar PIM para reducirlos.</span><span class="sxs-lookup"><span data-stu-id="5429f-106">The wizard helps you understand the security risks of privileged identities and how to use PIM to reduce those risks.</span></span> <span data-ttu-id="5429f-107">No tiene que realizar cambios en las asignaciones de roles existentes en el asistente; si lo prefiere, puede hacerlo más adelante.</span><span class="sxs-lookup"><span data-stu-id="5429f-107">You don't need to make any changes to existing role assignments in the wizard, if you prefer to do it later.</span></span>

## <a name="what-to-expect"></a><span data-ttu-id="5429f-108">Qué esperar</span><span class="sxs-lookup"><span data-stu-id="5429f-108">What to expect</span></span>
<span data-ttu-id="5429f-109">Antes de que su organización comienza a usar PIM, todas las asignaciones de roles son permanentes: los usuarios siempre tienen estos roles aunque en el momento actual no necesiten sus privilegios.</span><span class="sxs-lookup"><span data-stu-id="5429f-109">Before your organization starts using PIM, all role assignments are permanent: the users are always in these roles even if they do not presently need their privileges.</span></span>  <span data-ttu-id="5429f-110">El primer paso del asistente muestra una lista de roles con privilegios elevados y cuántos usuarios tienen actualmente esos roles.</span><span class="sxs-lookup"><span data-stu-id="5429f-110">The first step of the wizard shows you a list of high-privileged roles and how many users are currently in those roles.</span></span> <span data-ttu-id="5429f-111">Puede explorar en profundidad un rol determinado para conocer mejor a los usuarios en caso de que alguno de ellos no le resulte familiar.</span><span class="sxs-lookup"><span data-stu-id="5429f-111">You can drill in to a particular role to learn more about users if one or more of them are unfamiliar.</span></span>

<span data-ttu-id="5429f-112">El segundo paso del asistente le ofrece la oportunidad de cambiar las asignaciones de roles del administrador.</span><span class="sxs-lookup"><span data-stu-id="5429f-112">The second step of the wizard gives you an opportunity to change administrator's role assignments.</span></span>  

> [!WARNING]
> <span data-ttu-id="5429f-113">Es importante que tenga al menos un administrador global, y más de un administrador de roles con privilegios con una cuenta de organización (no una cuenta Microsoft).</span><span class="sxs-lookup"><span data-stu-id="5429f-113">It is important that you have at least one global administrator, and more than one privileged role administrator with an organizational account (not a Microsoft account).</span></span> <span data-ttu-id="5429f-114">Si solo hay un administrador de roles con privilegios, la organización no podrá administrar PIM si esa cuenta se elimina.</span><span class="sxs-lookup"><span data-stu-id="5429f-114">If there is only one privileged role administrator, the organization will not be able to manage PIM if that account is deleted.</span></span>
> <span data-ttu-id="5429f-115">Además, mantenga las asignaciones de roles permanente si un usuario tiene una cuenta de Microsoft (una cuenta que usan para iniciar sesión en servicios de Microsoft como Skype y Outlook.com).</span><span class="sxs-lookup"><span data-stu-id="5429f-115">Also, keep role assignments permanent if a user has a Microsoft account (An account they use to sign in to Microsoft services like Skype and Outlook.com).</span></span> <span data-ttu-id="5429f-116">Si tiene pensado exigir MFA para la activación de ese rol, ese usuario se bloqueará.</span><span class="sxs-lookup"><span data-stu-id="5429f-116">If you plan to require MFA for activation for that role, that user will be locked out.</span></span>
> 
> 

<span data-ttu-id="5429f-117">Una vez realizados los cambios, ya no se mostrará el asistente.</span><span class="sxs-lookup"><span data-stu-id="5429f-117">After you have made changes, the wizard will no longer show up.</span></span> <span data-ttu-id="5429f-118">La próxima vez que usted u otro administrador de roles con privilegios use PIM, verá el panel de PIM.</span><span class="sxs-lookup"><span data-stu-id="5429f-118">The next time you or another privileged role administrator use PIM, you will see the PIM dashboard.</span></span>  

* <span data-ttu-id="5429f-119">Si desea agregar o quitar usuarios a roles, o cambiar las asignaciones de permanentes a aptas, puede obtener más información en [Privileged Identity Management de Azure AD: Incorporación o eliminación de un rol de usuario](active-directory-privileged-identity-management-how-to-add-role-to-user.md).</span><span class="sxs-lookup"><span data-stu-id="5429f-119">If you would like to add or remove users from roles or change assignments from permanent to eligible, read more at [how to add or remove a user's role](active-directory-privileged-identity-management-how-to-add-role-to-user.md).</span></span>
* <span data-ttu-id="5429f-120">Si desea conceder acceso a más usuarios para administrar PIM, aprenda cómo hacerlo en [Concesión de acceso para administrar Privileged Identity Management de Azure AD](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span><span class="sxs-lookup"><span data-stu-id="5429f-120">If you would like to give more users access to manage PIM, read more at [how to give access to manage in PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5429f-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5429f-121">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

