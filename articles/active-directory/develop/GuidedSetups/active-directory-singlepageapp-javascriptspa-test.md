---
title: aaaAzure AD v2 JS SPA interactiva Setup - prueba | Documentos de Microsoft
description: "Cómo pueden llamar las aplicaciones SPA de JavaScript a una API que requiera tokens de acceso mediante el punto de conexión de Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: b2339431a070b5c4ad4058e6c1a9b19b83c84c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>Prueba del código

> ### <a name="testing-with-visual-studio"></a>Pruebas con Visual Studio
> Si se utiliza Visual Studio, presione `F5` toorun el proyecto: explorador Hola se abre y le dirige demasiado*http://localhost: {port}* donde verá hello *llamadas API de Microsoft Graph* botón.

<p/><!-- -->

> ### <a name="testing-with-python-or-another-web-server"></a>Pruebas con Python u otro servidor web
> Si no se utiliza Visual Studio, asegúrese de que el servidor web se inicia y se configura el puerto TCP de toolisten tooa según Hola carpeta que contiene su *index.html* archivo. Para Python, puede iniciar la escucha toohello puerto mediante la ejecución de Hola en comando hello prompt / terminal, desde la carpeta de la aplicación hello:
> 
> ```bash
> python -m http.server 8080
> ```
>  A continuación, abra el Explorador de Hola y escriba *http://localhost: 8080* o *http://localhost: {port}* : si hello *puerto* corresponde puerto toohello que es el servidor web escuchar. Debería ver contenido de saludo de la página index.html con hello *llamadas API de Microsoft Graph* botón.

## <a name="test-your-application"></a>Prueba de la aplicación

Después de explorador Hola carga su *index.html*, haga clic en hello *llamadas API de Microsoft Graph* botón. Si se trata de hello primera vez, Hola explorador redirecciones toohello v2 de Microsoft Azure Active Directory extremo, que te encuentres solicita toosign en.
 
![Captura de pantalla de ejemplo](media/active-directory-singlepageapp-javascriptspa-test/javascriptspascreenshot1.png)


### <a name="consent"></a>Consentimiento
Hello primera vez que inicie sesión en la aplicación tooyour, se le presentará una consentimiento pantalla similar toohello a continuación, en las que necesite tooaccept:

 ![Pantalla de consentimiento](media/active-directory-singlepageapp-javascriptspa-test/javascriptspaconsent.png)


### <a name="expected-results"></a>Resultados esperados
Debería ver la información de perfil de usuario devuelto por hello respuesta a llamadas de API Graph de Microsoft.
 
 ![Results](media/active-directory-singlepageapp-javascriptspa-test/javascriptsparesults.png)

También verá información básica sobre el token de hello adquirido en hello *Token de acceso* y *notificaciones del Token de Id. de* cuadros.

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Más información sobre los ámbitos y permisos delegados

Hola Microsoft Graph API requiere hello `user.read` definir el ámbito de perfil de usuario de tooread Hola. Este ámbito se agrega automáticamente de forma predeterminada en todas las aplicaciones que se van a registrar en nuestro portal de registro. Otras API de Microsoft Graph, así como las API personalizadas para el servidor back-end, pueden requerir ámbitos adicionales. Por ejemplo, para Microsoft Graph, Hola ámbito `Calendars.Read` es calendarios del usuario requiere toolist Hola. En orden tooaccess Hola calendario del usuario en el contexto de Hola de una aplicación, deberá tooadd Hola `Calendars.Read` delegado información del registro de aplicación de permiso toohello y, a continuación, agregue hello `Calendars.Read` toohello ámbito `acquireTokenSilent` llamar. usuario de Hola se solicitarán consentimientos adicionales a medida que aumente el número de Hola de ámbitos.

Si un API de back-end no requiere un ámbito (no recomendado), puede usar hello `clientId` como ámbito de Hola Hola `acquireTokenSilent` o `acquireTokenRedirect` llamadas.

<!--end-collapse-->
