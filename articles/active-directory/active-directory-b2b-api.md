---
title: "aaaAzure B2B de Active Directory personalización y colaboración API | Documentos de Microsoft"
description: "Colaboración B2B de Active Directory de Azure es compatible con las relaciones entre empresas habilitando tooselectively los socios comerciales acceso aplicaciones corporativas"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 04/11/2017
ms.author: sasubram
ms.openlocfilehash: 2609971ffa5d2ebc9466c61f4e4af11f5b045ecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-api-and-customization"></a>Personalización y API de colaboración B2B de Active Directory Azure

Hemos tenido muchos clientes nos indican que desean que el proceso de invitación de hello toocustomize de forma que se adapte mejor a sus organizaciones. Con nuestra API, pueden hacer justamente eso. [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="capabilities-of-hello-invitation-api"></a>Capacidades de invitación de hello API
Hola API ofrece Hola siguientes capacidades:

1. Invite a un usuario externo con *cualquier* dirección de correo electrónico.

    ```
    "invitedUserDisplayName": "Sam"
    "invitedUserEmailAddress": "gsamoogle@gmail.com"
    ```

2. Personalizar donde desea que su tooland a los usuarios después de que acepten la invitación.

    ```
    "inviteRedirectUrl": "https://myapps.microsoft.com/"
    ```

3. Elija correo electrónico de invitación estándar de toosend Hola por medio de nosotros

    ```
    "sendInvitationMessage": true
    ```

  con un destinatario del mensaje toohello que se puede personalizar

    ```
    "customizedMessageBody": "Hello Sam, let's collaborate!"
    ```

4. Y elija toocc: personas que desea tookeep Hola bucle sobre su invitar a este colaborador.

5. O bien personalizar completamente su invitación y el flujo de trabajo de incorporación eligiendo no toosend notificaciones a través de Azure AD.

    ```
    "sendInvitationMessage": false
    ```

  En este caso, se recibe una URL de pago de hello API que se puede incrustar en una plantilla de correo electrónico, mensajería instantánea u otro método de distribución de su elección.

6. Por último, si es administrador, puede elegir usuario de hello tooinvite como miembro.

    ```
    "invitedUserType": "Member"
    ```


## <a name="authorization-model"></a>Modelo de autorización
Hola API se puede ejecutar en los siguientes modos de autorización de hello:

### <a name="app--user-mode"></a>Aplicación y modo de usuario
En este modo, gana el jugador que está usando Hola API necesidades toohave Hola permisos toobe crear invitaciones de B2B.

### <a name="app-only-mode"></a>Modo de solo aplicación
En el contexto solo de aplicación, aplicación hello debe hello User.ReadWrite.All o Directory.ReadWrite.All ámbitos para hello invitación toosucceed.

Para obtener más información, consulte: https://graph.microsoft.io/docs/authorization/permission_scopes.


## <a name="powershell"></a>PowerShell
Es ahora toouse posibles PowerShell tooadd e invitar a usuarios externos tooan organización fácilmente. Crear una invitación con hello cmdlet:

```
New-AzureADMSInvitation
```

Puede usar Hola siguientes opciones:

* -InvitedUserDisplayName
* -InvitedUserEmailAddress
* -SendInvitationMessage
* -InvitedUserMessageInfo

También es posible desproteger referencia de API de invitación de hello en [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="next-steps"></a>Pasos siguientes

Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:

* [¿Qué es la colaboración B2B de Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [¿Cómo agregan los administradores de Azure Active Directory usuarios de colaboración B2B?](active-directory-b2b-admin-add-users.md)
* [¿Cómo agregan los trabajadores de la información usuarios de colaboración B2B?](active-directory-b2b-iw-add-users.md)
* [elementos de saludo de correo electrónico de invitación de colaboración B2B de hello](active-directory-b2b-invitation-email.md)
* [Canje de invitación de colaboración B2B](active-directory-b2b-redemption-experience.md)
* [Concesión de licencias de colaboración B2B de Azure AD](active-directory-b2b-licensing.md)
* [Solución de problemas de colaboración B2B de Azure Active Directory](active-directory-b2b-troubleshooting.md)
* [Preguntas frecuentes sobre la colaboración B2B de Azure Active Directory (P+F)](active-directory-b2b-faq.md)
* [Autenticación multifactor para usuarios de colaboración B2B](active-directory-b2b-mfa-instructions.md)
* [Incorporación de usuarios de colaboración B2B sin invitación](active-directory-b2b-add-user-without-invite.md)
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)
