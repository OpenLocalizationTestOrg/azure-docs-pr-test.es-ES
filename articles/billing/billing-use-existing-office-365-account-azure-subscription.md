---
title: aaaSign en Azure con la cuenta de Office 365 | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una suscripción de Azure mediante una cuenta de Office 365"
services: 
documentationcenter: 
author: JiangChen79
manager: adpick
editor: 
tags: billing,top-support-issue
ms.assetid: 129cdf7a-2165-483d-83e4-8f11f0fa7f8b
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: cjiang
ms.openlocfilehash: cc331bf7222b5b03e740cb40a214bc13ef585f54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sign-up-for-an-azure-subscription-with-your-office-365-account"></a>Registrarse para obtener una suscripción de Azure con su cuenta de Office 365
Si tiene una suscripción de Office 365, puede usar su toocreate de cuenta de Office 365 una suscripción de Azure. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/) con su nombre de usuario de Office 365 y la contraseña. Si desea tooset las máquinas virtuales o usar otros servicios de Azure, debe registrarse para una suscripción de Azure. Puede compartir su suscripción de Azure con otras personas y [use tooyour de acceso de Control de acceso basado en roles toomanage suscripción de Azure y recursos](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure)

Si ya tiene una cuenta de Office 365 y una suscripción de Azure, consulte [asociar un tooan del inquilino de Office 365 suscripción de Azure](billing-add-office-365-tenant-to-azure-subscription.md).

## <a name="get-an-azure-subscription-using-your-office-365-account"></a>Obtención de una suscripción de Azure con su cuenta de Office 365

Ahorre tiempo y evite la proliferación de cuentas al suscribirse a Azure con el nombre de usuario y la contraseña de Office 365. 

1. Suscríbase en [Azure.com](https://account.azure.com/signup?offer=MS-AZR-0044p&appId=docs). 
2. Inicie sesión con su nombre de usuario y contraseña de Office 365. cuenta de Hello que usa no tiene permisos de administrador de toohave. Si tiene más de una cuenta de Office 365, asegúrese de que usa credenciales de hello para la cuenta de hello Office 365 que desee tooassociate con su suscripción de Azure. 

   ![Captura de pantalla que muestra la página de inicio de sesión de Hola.](./media/billing-use-existing-office-365-account-azure-subscription/billing-sign-in-with-office-365-account.png)

3. Escriba información de hello necesario y el proceso de registro de hello completa. Puede que alguna información no sea necesaria si ya tiene una cuenta de Office 365.

    ![Captura de pantalla que muestra el formulario de registro de hello.](./media/billing-use-existing-office-365-account-azure-subscription/billing-azure-sign-up-fill-information.png)

- Si necesita tooadd otras personas en su suscripción de Azure de toohello de organización, consulte [comenzar con la administración de acceso de hello portal de Azure](../active-directory/role-based-access-control-what-is.md). 

## <a id="more-about-subs">Más información acerca de las suscripciones de Azure y Office 365</a>
Office 365 y Azure usan suscripciones y usuarios de toomanage de servicio de Azure AD de Hola. Hola directorio de Azure es similar a un contenedor en el que puede agrupar a los usuarios y las suscripciones. toouse Hola mismas cuentas de usuario para las suscripciones Azure y Office 365, debe toomake seguro de que hello Azure las suscripciones se crean en hello mismo directorio como las suscripciones de hello Office 365. Tenga en Hola de cuenta siguientes puntos:

* Una suscripción se crea en un directorio
* Los usuarios pertenecen toodirectories
* Llega a una suscripción de directorio de Hola de usuario de Hola que crea la suscripción de Hola. Por lo que la suscripción a Office 365 es toohello ligada misma cuenta de su suscripción de Azure.
* Las suscripciones de Azure pertenecen a usuarios individuales en el directorio de Hola
* El propio directorio Hola posee las suscripciones de Office 365. Los usuarios con permisos adecuados de hello en el directorio de hello pueden administrar estas suscripciones.

![Captura de pantalla que muestra la relación de hello del directorio de hello, los usuarios y las suscripciones.](./media/billing-use-existing-office-365-account-azure-subscription/19-background-information.png)

Para más información, consulte [Asociación de las suscripciones de Azure con Azure Active Directory](../active-directory/active-directory-how-subscriptions-associated-directory.md).

## <a name="need-help-contact-support"></a>¿Necesita ayuda? Póngase en contacto con el servicio de soporte técnico.
Si aún necesita ayuda, [póngase en contacto con soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget rápidamente para solucionar el problema. 
