---
title: "aaaAzure AD v2 Windows Desktop introducción - prueba | Documentos de Microsoft"
description: "Cómo pueden llamar las aplicaciones .NET de escritorio de Windows (XAML) a una API que requiera tokens de acceso mediante el punto de conexión de Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 0ae9612e1585c54a3fe35ba9d18f92554099b2c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>Prueba del código

En orden tootest para la aplicación, presione `F5` toorun el proyecto en Visual Studio. Aparecerá la ventana principal:

![Captura de pantalla de ejemplo](media/active-directory-mobileanddesktopapp-windowsdesktop-test/samplescreenshot.png)

Cuando esté listo tootest, haga clic en *llamadas API de Microsoft Graph* y usar Microsoft Azure Active Directory (cuenta profesional) o un toosign de cuenta de Microsoft Account (live.com, outlook.com) en. Es Hola primera vez, verá una ventana solicitando al usuario toosign en:

![Inicio de sesión](media/active-directory-mobileanddesktopapp-windowsdesktop-test/signinscreenshot.png)

### <a name="consent"></a>Consentimiento
Hello primera vez que inicie sesión en la aplicación tooyour, le presentará una pantalla de consentimiento similar toohello a continuación, en los que necesite tooexplicitly acepte:

![Pantalla de consentimiento](media/active-directory-mobileanddesktopapp-windowsdesktop-test/consentscreen.png)

### <a name="expected-results"></a>Resultados esperados
Debería ver la información de perfil de usuario devuelto por llamada de API de Microsoft Graph hello en pantalla de resultados de llamar a la API de bienvenida.

También debe ver información básica sobre el token de hello adquirido a través de `AcquireTokenAsync` o `AcquireTokenSilentAsync` en cuadro de información de símbolo (token) de hello:

|Propiedad  |Formato  |Descripción |
|---------|---------|---------|
|Nombre | {Nombre completo del usuario} |usuario de Hola y el apellido nombre|
|Nombre de usuario |<span>user@domain.com</span> |nombre de usuario de Hello usado usuario de hello tooidentify|
|Token Expires |{FechaHora}         |hora de Hello en qué Hola expira el token. MSAL extenderá la fecha de expiración de hello automáticamente al renovar el token de hello cuando sea necesario|
|Access token |{Cadena}         |cadena de token de Hello enviados que se enviarán las solicitudes de tooHTTP que requieren un encabezado de autorización|

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Más información sobre los ámbitos y permisos delegados
API Graph requiere hello `user.read` ámbito tooread perfil de usuario. Este ámbito se agrega automáticamente de forma predeterminada en todas las aplicaciones que se van a registrar en nuestro portal de registro. Otras API Graph, así como las API personalizadas para el servidor back-end, requieren ámbitos adicionales. Por ejemplo, para el gráfico, `Calendars.Read` es calendarios del usuario toolist necesarios. En orden tooaccess Hola calendario del usuario en un contexto de una aplicación, deberá tooadd `Calendars.Read` delegado información del registro de la aplicación y, a continuación, agregue `Calendars.Read` toohello `AcquireTokenAsync` llamar. Se pedirá el nombre de usuario para consentimientos adicionales a medida que aumente el número de Hola de ámbitos.

<!--end-collapse-->



