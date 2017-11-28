---
title: Asistente para la seguridad de Azure AD aaaThe Privileged Identity Management
description: "Hello primera vez que utilice la extensión de Azure Active Directory Privileged Identity Management de hello, aparecerá con un Asistente para la seguridad. Este artículo describe los pasos de Hola para utilizar el Asistente de Hola."
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
ms.openlocfilehash: 0b3019134d3c7cfac33b3acfcf430b4d4f67b119
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-security-wizard-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="6ef53-104">Utilizando el Asistente para la seguridad de hello en Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="6ef53-104">Using hello security wizard in Azure AD Privileged Identity Management</span></span> 
<span data-ttu-id="6ef53-105">Si le Hola primera persona toorun Azure Privileged Identity Management (PIM) para su organización, aparecerá un asistente.</span><span class="sxs-lookup"><span data-stu-id="6ef53-105">If you're hello first person toorun Azure Privileged Identity Management (PIM) for your organization, you will be presented with a wizard.</span></span> <span data-ttu-id="6ef53-106">Hola asistente le ayudará a conocer los riesgos de seguridad de Hola de identidades con privilegios y cómo toouse PIM tooreduce esos riesgos.</span><span class="sxs-lookup"><span data-stu-id="6ef53-106">hello wizard helps you understand hello security risks of privileged identities and how toouse PIM tooreduce those risks.</span></span> <span data-ttu-id="6ef53-107">No es necesario toomake las asignaciones de roles de tooexisting cambios en el Asistente de hello, si lo prefiere toodo que más adelante.</span><span class="sxs-lookup"><span data-stu-id="6ef53-107">You don't need toomake any changes tooexisting role assignments in hello wizard, if you prefer toodo it later.</span></span>

## <a name="what-tooexpect"></a><span data-ttu-id="6ef53-108">¿Qué tooexpect</span><span class="sxs-lookup"><span data-stu-id="6ef53-108">What tooexpect</span></span>
<span data-ttu-id="6ef53-109">Antes de que la organización empiece a usar PIM, todas las asignaciones de roles son permanentes: los usuarios de Hola son siempre con estos roles aunque actualmente no es necesario sus privilegios.</span><span class="sxs-lookup"><span data-stu-id="6ef53-109">Before your organization starts using PIM, all role assignments are permanent: hello users are always in these roles even if they do not presently need their privileges.</span></span>  <span data-ttu-id="6ef53-110">primer paso del Asistente para Hola de Hello muestra una lista de roles con privilegios elevados y cuántos usuarios están actualmente en esos roles.</span><span class="sxs-lookup"><span data-stu-id="6ef53-110">hello first step of hello wizard shows you a list of high-privileged roles and how many users are currently in those roles.</span></span> <span data-ttu-id="6ef53-111">Puede profundizar en tooa rol determinado toolearn más información acerca de los usuarios si uno o varios de ellos están familiarizado.</span><span class="sxs-lookup"><span data-stu-id="6ef53-111">You can drill in tooa particular role toolearn more about users if one or more of them are unfamiliar.</span></span>

<span data-ttu-id="6ef53-112">segundo paso del Asistente para Hola de Hello proporciona las asignaciones de roles de administrador toochange oportunidad.</span><span class="sxs-lookup"><span data-stu-id="6ef53-112">hello second step of hello wizard gives you an opportunity toochange administrator's role assignments.</span></span>  

> [!WARNING]
> <span data-ttu-id="6ef53-113">Es importante que tenga al menos un administrador global, y más de un administrador de roles con privilegios con una cuenta de organización (no una cuenta Microsoft).</span><span class="sxs-lookup"><span data-stu-id="6ef53-113">It is important that you have at least one global administrator, and more than one privileged role administrator with an organizational account (not a Microsoft account).</span></span> <span data-ttu-id="6ef53-114">Si hay solo un administrador de roles con privilegios, organización hello no será capaz de toomanage PIM si esa cuenta se elimina.</span><span class="sxs-lookup"><span data-stu-id="6ef53-114">If there is only one privileged role administrator, hello organization will not be able toomanage PIM if that account is deleted.</span></span>
> <span data-ttu-id="6ef53-115">Además, mantenga asignaciones de roles permanente si un usuario tiene una cuenta de Microsoft (una cuenta que usan toosign en servicios de tooMicrosoft como Skype y Outlook.com).</span><span class="sxs-lookup"><span data-stu-id="6ef53-115">Also, keep role assignments permanent if a user has a Microsoft account (An account they use toosign in tooMicrosoft services like Skype and Outlook.com).</span></span> <span data-ttu-id="6ef53-116">Si tiene previsto toorequire MFA para la activación para ese rol, ese usuario se bloqueará.</span><span class="sxs-lookup"><span data-stu-id="6ef53-116">If you plan toorequire MFA for activation for that role, that user will be locked out.</span></span>
> 
> 

<span data-ttu-id="6ef53-117">Después de realizar cambios, ya no se mostrará el Asistente de Hola.</span><span class="sxs-lookup"><span data-stu-id="6ef53-117">After you have made changes, hello wizard will no longer show up.</span></span> <span data-ttu-id="6ef53-118">Hello próxima vez que usted u otro administrador de roles con privilegios usar PIM, verá Hola PIM panel.</span><span class="sxs-lookup"><span data-stu-id="6ef53-118">hello next time you or another privileged role administrator use PIM, you will see hello PIM dashboard.</span></span>  

* <span data-ttu-id="6ef53-119">Si prefiere como tooadd o quitar usuarios de roles o cambiar las asignaciones de tooeligible permanente, más información, lea [cómo tooadd o quitar una función de usuario](active-directory-privileged-identity-management-how-to-add-role-to-user.md).</span><span class="sxs-lookup"><span data-stu-id="6ef53-119">If you would like tooadd or remove users from roles or change assignments from permanent tooeligible, read more at [how tooadd or remove a user's role](active-directory-privileged-identity-management-how-to-add-role-to-user.md).</span></span>
* <span data-ttu-id="6ef53-120">Si desea que toogive más usuarios tener acceso a toomanage PIM, más información, lea [cómo toogive tener acceso a toomanage en PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span><span class="sxs-lookup"><span data-stu-id="6ef53-120">If you would like toogive more users access toomanage PIM, read more at [how toogive access toomanage in PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ef53-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6ef53-121">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

