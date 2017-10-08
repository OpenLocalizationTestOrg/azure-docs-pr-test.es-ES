---
title: "aaaAzure AD v2 Android Introducción - prueba | Documentos de Microsoft"
description: "Cómo puede una aplicación de Android obtener un token de acceso y llamar a las API Graph que requieren tokens de acceso desde el punto de conexión de Azure Active Directory v2"
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
ms.openlocfilehash: 499f32b46fd44cca0e52179bced49b311135d8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>Prueba del código

1. Implementar el código tooyour/emulador de dispositivos.
2. Cuando esté listo tootest, use Microsoft Azure Active Directory (cuenta profesional) o un toosign de cuenta de Microsoft Account (live.com, outlook.com) en. 

![Captura de pantalla de ejemplo](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
<br/><br/>
![Inicio de sesión](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)

### <a name="consent"></a>Consentimiento
Hello primera vez que un usuario inicia sesión en la aplicación tooyour, le presentará una pantalla de consentimiento similar toohello siguiente, donde deben aceptar tooexplicitly: 

![Consentimiento](media/active-directory-mobileanddesktopapp-android-test/androidconsent.png)


### <a name="expected-results"></a>Resultados esperados
Debería ver resultados de Hola de un tooMicrosoft de llamada de API Graph 'me' punto de conexión usa el perfil de usuario de hello tootooobtain - https://graph.microsoft.com/v1.0/me. Para ver una lista de los puntos de conexión comunes de Microsoft Graph, consulte este [artículo](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Más información sobre los ámbitos y permisos delegados

Hola Microsoft Graph API requiere hello `user.read` definir el ámbito de perfil de usuario de tooread Hola. Este ámbito se agrega automáticamente de forma predeterminada en todas las aplicaciones que se van a registrar en nuestro portal de registro. Otras API de Microsoft Graph, así como las API personalizadas para el servidor back-end, pueden requerir ámbitos adicionales. Por ejemplo, para Microsoft Graph, Hola ámbito `Calendars.Read` es calendarios del usuario requiere toolist Hola. En orden tooaccess Hola calendario del usuario en un contexto de una aplicación, deberá tooadd Hola `Calendars.Read` delegado información del registro de aplicación de permiso toohello y, a continuación, agregue hello `Calendars.Read` toohello ámbito `acquireTokenSilentAsync` llamar. usuario de Hola se solicitarán consentimientos adicionales a medida que aumente el número de Hola de ámbitos.

<!--end-collapse-->
