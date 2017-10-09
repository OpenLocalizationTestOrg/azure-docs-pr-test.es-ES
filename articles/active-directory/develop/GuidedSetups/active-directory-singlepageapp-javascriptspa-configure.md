---
title: "aaaAzure AD v2 JS SPA guiada por el programa de instalación: configurar | Documentos de Microsoft"
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
ms.openlocfilehash: 1b93298d4bd4e17dd261dbb75502a122c30aac97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="register-your-application"></a>Registrar su aplicación

Hay varias maneras toocreate una aplicación, seleccione uno de ellos:

### <a name="option-1-register-your-application-express-mode"></a>Opción 1: Registro de la aplicación (modo Rápido)
Ahora deberá tooregister la aplicación Hola *Portal de registro de aplicación de Microsoft*:

1.  Registrar la aplicación a través de hello [Portal de registro de aplicación de Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)
2.  Escriba el nombre de la aplicación y su correo electrónico.
3.  Asegúrese de opción de hello seguro *el programa de instalación interactiva* está activada
4.  Siga el identificador de la aplicación de hello instrucciones tooobtain hello y péguelo en el código

### <a name="option-2-register-your-application-advanced-mode"></a>Opción 2: Registro de la aplicación (modo Avanzado)

1. Vaya toohello [Portal de registro de aplicación de Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister una aplicación
2. Escriba el nombre de la aplicación y su correo electrónico. 
3. Asegúrese de opción de hello seguro *el programa de instalación interactiva* está desactivada
4.  Haga clic en `Add Platform` y luego en `Web`.
5. Agregar hello `Redirect URL` que corresponden a direcciones URL de la aplicación toohello basándose en el servidor web. Vea las secciones de Hola a continuación para obtener instrucciones sobre cómo tooset / obtener la dirección URL de redireccionamiento de hello en Visual Studio y Python.
6. Haga clic en *Guardar*

> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a>Instrucciones en Visual Studio para obtener la dirección URL de redireccionamiento
> Siga Hola instrucciones tooobtain la dirección URL de redireccionamiento:
> 1.    En *el Explorador de soluciones*, seleccione el proyecto de Hola y mire hello `Properties` ventana (si no ve una ventana de propiedades, presione `F4`)
> 2.    Copiar valor de Hola de `URL` toohello Portapapeles:<br/> ![Propiedades del proyecto](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)<br />
> 3.    Cambiar atrás toohello *Portal de registro de aplicación* y pegue el valor de Hola como un `Redirect URL` y haga clic en 'Guardar'

<p/>

> #### <a name="setting-redirect-url-for-python"></a>Configuración de la dirección URL de redireccionamiento para Python
> Para Python, puede establecer el puerto de servidor web de Hola a través de la línea de comandos. Este programa de instalación guiada utiliza el puerto de hello 8080 para referencia pero Siéntase libre toouse cualquier puerto disponible. En cualquier caso, siga instrucciones hello tooset una dirección URL de redireccionamiento en información de registro de aplicación Hola:<br/>
> - Cambiar toohello Atrás *Portal de registro de aplicación* y establecer `http://localhost:8080/` como un `Redirect URL`, o usar `http://localhost:[port]/` si usa un puerto TCP personalizado (donde *[puerto]* es el puerto TCP personalizado Hola número) y haga clic en 'Guardar'


#### <a name="configure-your-javascript-spa"></a>Configuración de JavaScript SPA

1.  Cree un archivo denominado `msalconfig.js` que contiene información de registro de aplicación Hola. Si usas el proyecto de Visual Studio, seleccione hello (carpeta raíz del proyecto), haga clic en y seleccione: `Add`  >  `New Item`  >  `JavaScript File`. Asígnele el nombre `msalconfig.js`.
2.  Agregar Hola después código tooyour `msalconfig.js` archivo:

```javascript
var msalconfig = {
    clientID: "Enter_the_Application_Id_here",
    redirectUri: location.origin
};
```
<ol start="3">
<li>
Reemplace <code>Enter_the_Application_Id_here</code> con hello que acaba de registrar el identificador de aplicación
</li>
</ol>
