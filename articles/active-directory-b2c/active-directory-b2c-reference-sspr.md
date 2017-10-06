---
title: "Azure Active Directory B2C: restablecimiento de contraseña de autoservicio | Microsoft Docs"
description: "Un tema que muestra cómo restablece tooset la contraseña de autoservicio para los consumidores en Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: curtand
ms.assetid: c87ed86e-1520-42b1-8c31-46cd44ed5310
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: ff87eea42259b610702da73af35d0a38eb7dd33d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-set-up-self-service-password-reset-for-your-consumers"></a>Azure Active Directory B2C: configurar el autoservicio de restablecimiento de contraseña para los consumidores
Con hello característica de restablecimiento de contraseña de autoservicio, los consumidores (que se suscribieron para cuentas locales) pueden restablecer sus contraseñas por sí solas. Esto reduce considerablemente carga hello en su personal de soporte técnico, sobre todo si la aplicación tiene millones de los consumidores que usan de forma regular. Actualmente, solo se admite como método de recuperación el uso de una dirección de correo electrónico comprobada. Métodos de recuperación adicionales (número de teléfono comprobado, preguntas de seguridad, etc.) se agregará en un futuro Hola.

> [!NOTE]
> Este artículo aplica la contraseña del servicio tooself restablecimiento utilizado en el contexto de Hola de una directiva de inicio de sesión. Si necesita invocar directivas de restablecimiento de contraseña totalmente personalizables desde su aplicación, consulte [este artículo](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).
> 
> 

De forma predeterminada, el directorio no tendrá activado el autoservicio de restablecimiento de contraseña. Use Hola siguientes pasos tooturn en:

1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com/) como Hola Administrador de la suscripción. Se trata de hello mismo trabajo o educativa cuenta u Hola la misma cuenta de Microsoft que usa toocreate su directorio.
2. Navegue toohello extensión de Active Directory en la barra de navegación de hello en el lado izquierdo de Hola.
3. Buscar el directorio en hello **Directory** ficha y haga clic en él.
4. Haga clic en hello **configurar** ficha.
5. Desplácese hacia abajo toohello **políticas para restablecer contraseñas de usuario** sección y alternar hello **usuarios habilitados para restablecer la contraseña** opción demasiado**Sí**. Tenga en cuenta que hello **dirección de correo electrónico alternativa** opción está activada; dejarlo tal cual.
   
    ![Restablecimiento de la contraseña de autoservicio](./media/active-directory-b2c-reference-sspr/sspr.png)
6. Haga clic en **guardar** final Hola de página Hola. ¡Y ya está!

tootest, característica de "Ejecutar ahora" hello de uso en cualquier directiva de inicio de sesión que tiene las cuentas locales como proveedor de identidades. En el inicio de sesión de cuenta local de hello página (donde se introducirán una dirección de correo electrónico y contraseña, o un nombre de usuario y una contraseña), haga clic en **no se puede acceder a su cuenta?** experiencia del consumidor tooverify Hola.

> [!NOTE]
> Hello páginas de restablecimiento de contraseña de autoservicio pueden personalizarse mediante el uso de hello [característica de personalización de marca de empresa](../active-directory/active-directory-add-company-branding.md).
> 
> 

