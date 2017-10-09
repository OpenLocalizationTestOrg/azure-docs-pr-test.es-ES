---
title: "aaaAzure AD v2 JS SPA guiada por el programa de instalación: el programa de instalación | Documentos de Microsoft"
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
ms.openlocfilehash: 19e15c6c8db8bea2975f30e7505af79ccad17e02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="setting-up-your-web-server-or-project"></a>Configuración del servidor web o proyecto

> ¿Prefiere toodownload proyecto de este ejemplo en su lugar? 
> - [Descargar el proyecto de Visual Studio Hola](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/VisualStudio.zip)
>
> o
> - [Descargar archivos de proyecto de hello](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip) para un servidor web local, como Python
>
> Y, a continuación, omitir toohello [paso de configuración](#create-an-application-express) ejemplo de código de hello tooconfigure antes de ejecutarlo.

## <a name="prerequisites"></a>Requisitos previos
Un servidor web local como [Python http.server](https://www.python.org/downloads/), [http server](https://www.npmjs.com/package/http-server/), [.NET Core](https://www.microsoft.com/net/core), o la integración de IIS Express con [2017 de Visual Studio](https://www.visualstudio.com/downloads/) es necesario toorun esta configuración paso a paso. 

Instrucciones de esta guía se basan en Python y 2017 de Visual Studio, pero Siéntase libre toouse cualquier otro entorno de desarrollo o un servidor Web.

## <a name="create-your-project"></a>Creación del proyecto 

> ### <a name="option-1-visual-studio"></a>Opción 1: Visual Studio 
> Si usa Visual Studio y a crear un nuevo proyecto, siga estos pasos hello toocreate una nueva solución de Visual Studio:
> 1.    En Visual Studio:  `File` > `New` > `Project`
> 2.    En `Visual C#\Web`, seleccione `ASP.NET Web Application (.NET Framework)`
> 3.    Asigne un nombre a la aplicación y haga clic en *Aceptar*.
> 4.    En `New ASP.NET Web Application`, seleccione `Empty`

<p/><!-- -->

> ### <a name="option-2-python-other-web-servers"></a>Opción 2: Python u otros servidores web
> Asegúrese de que ha instalado [Python](https://www.python.org/downloads/), a continuación, siga el paso de Hola a continuación:
> - Crear una carpeta toohost su aplicación.


## <a name="create-your-single-page-applications-ui"></a>Cree la interfaz de usuario de la aplicación de una sola página
1.  Cree un archivo *index.html* para JavaScript SPA. Si usas el proyecto de Visual Studio, seleccione hello (carpeta raíz del proyecto), haga clic en y seleccione: `Add`  >  `New Item`  >  `HTML page` y asígnele el nombre index.html
2.  Agregue Hola después de la página de códigos tooyour:
```html
<!DOCTYPE html>
<html>
<head>
    <!-- bootstrap reference used for styling hello page -->
    <link href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    <title>JavaScript SPA Guided Setup</title>
</head>
<body style="margin: 40px">
    <button id="callGraphButton" type="button" class="btn btn-primary" onclick="callGraphApi()">Call Microsoft Graph API</button>
    <div id="errorMessage" class="text-danger"></div>
    <div class="hidden">
        <h3>Graph API Call Response</h3>
        <pre class="well" id="graphResponse"></pre>
    </div>
    <div class="hidden">
        <h3>Access Token</h3>
        <pre class="well" id="accessToken"></pre>
    </div>
    <div class="hidden">
        <h3>ID Token Claims</h3>
        <pre class="well" id="userInfo"></pre>
    </div>
    <button id="signOutButton" type="button" class="btn btn-primary hidden" onclick="signOut()">Sign out</button>

    <!-- This app uses cdn tooreference msal.js (recommended). 
         You can also download it from: https://github.com/AzureAD/microsoft-authentication-library-for-js -->
    <script src="https://secure.aadcdn.microsoftonline-p.com/lib/0.1.1/js/msal.min.js"></script>

    <!-- hello 'bluebird' and 'fetch' references below are required if you need toorun this application on Internet Explorer -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/bluebird/3.3.4/bluebird.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/fetch/2.0.3/fetch.min.js"></script>

    <script type="text/javascript" src="msalconfig.js"></script>
    <script type="text/javascript" src="app.js"></script>
</body>
</html>
````
