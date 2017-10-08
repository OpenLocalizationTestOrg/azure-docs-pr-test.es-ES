---
title: "aaaAzure AD v2 JS SPA configuración paso a paso: configurar (ARP) | Documentos de Microsoft"
description: "Cómo pueden llamar las aplicaciones SPA de JavaScript a una API que requiera tokens de acceso mediante el punto de conexión de Azure Active Directory v2 (ARP)"
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
ms.openlocfilehash: 157f4e342cd684294e24da6ee1fad8a7c2fc266a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a>Agregar tooyour de información de registro de la aplicación hello aplicación

En este paso, necesita la dirección URL de redireccionamiento de hello tooconfigure de la información de registro de aplicación y, a continuación, Agregar aplicación de JavaScript SPA tooyour de hello Id. de aplicación.

### <a name="configure-redirect-url"></a>Configuración de la URL de redireccionamiento

Configurar hello `Redirect URL` campo anteriormente con la dirección URL de hello para la página index.html basándose en el servidor web, a continuación, haga clic en *actualización*.


> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a>Instrucciones en Visual Studio para obtener la dirección URL de redireccionamiento
> tooobtain la dirección URL de redireccionamiento, siga las instrucciones de Hola a continuación:
> 1.    En *el Explorador de soluciones*, seleccione el proyecto de Hola y mire hello `Properties` ventana (si no ve una ventana de propiedades, presione `F4`)
> 2.    Copiar valor de Hola de `URL` toohello Portapapeles:<br/> ![Propiedades del proyecto](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)<br />
> 3.    Pegue el valor de Hola como un `Redirect URL` en hello parte superior de esta página, a continuación, haga clic en`Update`

<p/>

> #### <a name="setting-redirect-url-for-python"></a>Configuración de la dirección URL de redireccionamiento para Python
> Para Python, puede establecer el puerto de servidor web de Hola a través de la línea de comandos. Este programa de instalación guiada utiliza el puerto de hello 8080 para referencia pero Siéntase libre toouse cualquier puerto disponible. En cualquier caso, siga instrucciones hello tooset una dirección URL de redireccionamiento en información de registro de aplicación Hola:<br/>
> Establecer `http://localhost:8080/` como un `Redirect URL` Hola parte superior de esta página, o use `http://localhost:[port]/` si usa un puerto TCP personalizado (donde *[puerto]* es el número de puerto TCP personalizado hello) y, a continuación, haga clic en "Actualizar"

### <a name="configure-your-javascript-spa-application"></a>Configuración de la aplicación JavaScript SPA

1.  Cree un archivo denominado `msalconfig.js` que contiene información de registro de aplicación Hola. Si usas el proyecto de Visual Studio, seleccione hello (carpeta raíz del proyecto), haga clic en y seleccione: `Add`  >  `New Item`  >  `JavaScript File`. Asígnele el nombre `msalconfig.js`.
2.  Agregar Hola después código tooyour `msalconfig.js` archivo:

```javascript
var msalconfig = {
    clientID: "[Enter hello application Id here]",
    redirectUri: location.origin
};
``` 
