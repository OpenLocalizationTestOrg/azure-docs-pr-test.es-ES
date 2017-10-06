---
title: "Azure Active Directory B2C: Deshabilitación de la comprobación de correos electrónicos durante la suscripción de consumidores | Microsoft Docs"
description: "Un tema que muestra cómo toodisable enviar por correo electrónico de comprobación durante el inicio de sesión en Azure Active Directory B2C consumidor"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 433f32b8-96d2-4113-aa82-efcf42fa9827
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/06/2017
ms.author: parakhj
ms.openlocfilehash: a8a42eddcb577725f04d70e1b1ebbebf10b5937c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-disable-email-verification-during-consumer-sign-up"></a>Azure Active Directory B2C: Deshabilitación de la comprobación de correos electrónicos durante la suscripción de consumidores
Cuando se habilita, B2C de Azure Active Directory (Azure AD) proporciona un consumidor Hola toosign de capacidad para las aplicaciones al proporcionar una dirección de correo electrónico y crear una cuenta local. B2C de Azure AD garantiza direcciones de correo electrónico válida al exigir a los consumidores tooverify usarlas durante el proceso de registro de hello. También impide que un proceso automatizado malintencionado generar falsas cuentas para aplicaciones de Hola.

Algunos desarrolladores de aplicaciones prefieren tooskip comprobación de correo electrónico durante el proceso de registro de hello y en su lugar, tiene que los consumidores comprobar la dirección de correo electrónico de hello más tarde. toosupport, Azure AD B2C puede ser configurado toodisable comprobación de correo electrónico. Si lo hace, crea un proceso de inicio de sesión más suave y ofrece a los desarrolladores Hola flexibilidad toodifferentiate Hola los consumidores que han comprobado su dirección de correo electrónico de los consumidores que no lo ha hecho.

De forma predeterminada, las directivas de inicio de sesión tienen activada la comprobación de correos electrónicos. Use Hola siguientes pasos tooturn desactivada:

1. [Siga estos módulos de características de pasos toonavigate toohello B2C en hello portal de Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Haga clic en **Sign-up policies** (Directivas de registro) o **Sign-up or sign-in policies** (Directivas de inicio de sesión o registro) dependiendo de lo que haya configurado para el inicio de sesión.
3. Haga clic en la directiva (por ejemplo, "B2C_1_SiUp") tooopen. Haga clic en **editar** princip Hola de hoja de Hola.
4. Haga clic en **Page UI Customization** (Personalización de la IU de la página).
5. Haga clic en **Página de suscripción de cuenta local**.
6. Haga clic en **dirección de correo electrónico** en hello **nombre** columna bajo hello **atributos suscripción** sección.
7. Hola de alternancia **Requerir comprobación** opción demasiado**No**.
8. Haga clic en **Aceptar** en parte inferior de hello hasta llegar a hello **Editar directiva** hoja.
9. Haga clic en **guardar** princip Hola de hoja de Hola. ¡Y ya está!

> [!NOTE]
> Deshabilitar la comprobación de correo electrónico en el proceso de registro de hello puede provocar toospam. Si deshabilita Hola seleccionado de modo predeterminado, se recomienda agregar su propio sistema de comprobación.
> 
> 

Estamos siempre toofeedback abierta y sugerencias. Si tiene dificultades con este tema, o tiene las recomendaciones para mejorar el contenido, le agradeceríamos sus comentarios en la parte inferior de Hola de página de Hola. Para las solicitudes de características, agregarlos demasiado[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).
