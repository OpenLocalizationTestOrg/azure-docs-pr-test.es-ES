---
title: "aaaAzure AD v2 iOS Introducción - prueba | Documentos de Microsoft"
description: "Cómo pueden llamar las aplicaciones de iOS (Swift) a una API que requiera tokens de acceso mediante el punto de conexión de Azure Active Directory v2"
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
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 98c73eddabf9664feb19ac6878e9d7315b9aa79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="test-querying-hello-microsoft-graph-api-from-your-ios-application"></a>Probar consultas Hola API Graph de Microsoft desde su aplicación de iOS

Presione `Command`  +  `R` toorun código de hello en el simulador de Hola.

![Captura de pantalla de ejemplo](media/active-directory-mobileanddesktopapp-ios-test/iostestscreenshot.png)

Cuando esté listo tootest, pulse *'Llamar a las API de Graph de Microsoft'* y será tootype solicitada su nombre de usuario y contraseña.

### <a name="consent"></a>Consentimiento
Hello primera vez que inicie sesión en la aplicación tooyour, le presentará una pantalla de consentimiento similar toohello a continuación, en los que necesite tooexplicitly acepte:

![Pantalla de consentimiento](media/active-directory-mobileanddesktopapp-ios-test/iosconsentscreen.png)

### <a name="expected-results"></a>Resultados esperados
Debería ver la información de perfil de usuario devuelto por la llamada de API de Microsoft Graph Hola Hola *registro* sección.

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Más información sobre los ámbitos y permisos delegados

Hola Microsoft Graph API requiere hello `user.read` definir el ámbito de perfil de usuario de tooread Hola. Este ámbito se agrega automáticamente de forma predeterminada en todas las aplicaciones que se van a registrar en nuestro portal de registro. Otras API de Microsoft Graph, así como las API personalizadas para el servidor back-end, pueden requerir ámbitos adicionales. Por ejemplo, para Microsoft Graph, Hola ámbito `Calendars.Read` es calendarios del usuario requiere toolist Hola. En orden tooaccess Hola calendario del usuario en un contexto de una aplicación, deberá tooadd Hola `Calendars.Read` delegado información del registro de aplicación de permiso toohello y, a continuación, agregue hello `Calendars.Read` toohello ámbito `acquireTokenSilent` llamar. usuario de Hola se solicitarán consentimientos adicionales a medida que aumente el número de Hola de ámbitos.

<!--end-collapse-->



