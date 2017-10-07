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
# <a name="using-hello-security-wizard-in-azure-ad-privileged-identity-management"></a>Utilizando el Asistente para la seguridad de hello en Azure AD Privileged Identity Management 
Si le Hola primera persona toorun Azure Privileged Identity Management (PIM) para su organización, aparecerá un asistente. Hola asistente le ayudará a conocer los riesgos de seguridad de Hola de identidades con privilegios y cómo toouse PIM tooreduce esos riesgos. No es necesario toomake las asignaciones de roles de tooexisting cambios en el Asistente de hello, si lo prefiere toodo que más adelante.

## <a name="what-tooexpect"></a>¿Qué tooexpect
Antes de que la organización empiece a usar PIM, todas las asignaciones de roles son permanentes: los usuarios de Hola son siempre con estos roles aunque actualmente no es necesario sus privilegios.  primer paso del Asistente para Hola de Hello muestra una lista de roles con privilegios elevados y cuántos usuarios están actualmente en esos roles. Puede profundizar en tooa rol determinado toolearn más información acerca de los usuarios si uno o varios de ellos están familiarizado.

segundo paso del Asistente para Hola de Hello proporciona las asignaciones de roles de administrador toochange oportunidad.  

> [!WARNING]
> Es importante que tenga al menos un administrador global, y más de un administrador de roles con privilegios con una cuenta de organización (no una cuenta Microsoft). Si hay solo un administrador de roles con privilegios, organización hello no será capaz de toomanage PIM si esa cuenta se elimina.
> Además, mantenga asignaciones de roles permanente si un usuario tiene una cuenta de Microsoft (una cuenta que usan toosign en servicios de tooMicrosoft como Skype y Outlook.com). Si tiene previsto toorequire MFA para la activación para ese rol, ese usuario se bloqueará.
> 
> 

Después de realizar cambios, ya no se mostrará el Asistente de Hola. Hello próxima vez que usted u otro administrador de roles con privilegios usar PIM, verá Hola PIM panel.  

* Si prefiere como tooadd o quitar usuarios de roles o cambiar las asignaciones de tooeligible permanente, más información, lea [cómo tooadd o quitar una función de usuario](active-directory-privileged-identity-management-how-to-add-role-to-user.md).
* Si desea que toogive más usuarios tener acceso a toomanage PIM, más información, lea [cómo toogive tener acceso a toomanage en PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

