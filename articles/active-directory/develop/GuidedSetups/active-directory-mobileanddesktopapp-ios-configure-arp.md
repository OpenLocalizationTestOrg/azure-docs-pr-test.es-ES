---
title: "aaaAzure AD v2 iOS Introducción - configurar direcciones (ARP) | Documentos de Microsoft"
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
ms.openlocfilehash: e5087e13160243d808b1d02771fa66fb332cfad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a>Agregar aplicación de tooyour de información de registro de la aplicación hello

En este paso, necesita proyecto tooyour de tooadd Hola Id. de aplicación:

1.  En `ViewController.swift`, reemplace la línea hello que empieza por '`let kClientID`' con:
```swift
let kClientID = "[Enter hello application Id here]"
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
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
            <string>msal[Enter hello application Id here]</string>
            <string>auth</string>
        </array>
    </dict>
</array>
```
