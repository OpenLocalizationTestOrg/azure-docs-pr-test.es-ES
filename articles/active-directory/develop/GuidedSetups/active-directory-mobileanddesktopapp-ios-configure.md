---
title: "Introducción a la aaaAzure AD v2 iOS: configurar | Documentos de Microsoft"
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
ms.openlocfilehash: 537cc7f0de6cd947fe340566c9e93f8bb08d57a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>Creación de una aplicación (proceso rápido)
Ahora deberá tooregister la aplicación Hola *Portal de registro de aplicación de Microsoft*:
1. Registrar la aplicación a través de hello [Portal de registro de aplicación de Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)
2.  Escriba el nombre de la aplicación y su correo electrónico.
3.  Asegúrese de que está activada la opción de hello para el programa de instalación interactiva
4.  Siga el identificador de la aplicación de hello instrucciones tooobtain hello y péguelo en el código

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Agregar la solución de tooyour información de registro de aplicación (avanzado)

1.  Vaya demasiado[Portal de registro de aplicación de Microsoft](https://apps.dev.microsoft.com/portal/register-app)
2.  Escriba el nombre de la aplicación y su correo electrónico.
3.  Asegúrese de que está desactivada la opción de hello para el programa de instalación interactiva
4.  Haga clic en `Add Platform`, seleccione `Native Application` y haga clic en `Save`.
5.  Volver atrás tooXcode. En `ViewController.swift`, reemplace la línea hello que empieza por '`let kClientID`' con el Id. de aplicación Hola que acaba de registrar:

```swift
let kClientID = "Your_Application_Id_Here"
```

<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
Control + clic <code>Info.plist</code> toobring una copia de seguridad del menú contextual hello y, a continuación, haga clic en: <code>Open As</code>> <code>Source Code</code>
</li>
<li>
En hello <code>dict</code> nodo raíz, agregue Hola siguientes:
</li>
</ol>

```xml
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLName</key>
        <string>$(PRODUCT_BUNDLE_IDENTIFIER)</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>msal[Your_Application_Id_Here]</string>
            <string>auth</string>
        </array>
    </dict>
</array>
```
<ol start="8">
<li>
Reemplace <i> <code>[Your_Application_Id_Here]</code> </i> con hello que acaba de registrar el identificador de aplicación
</li>
</ol>
