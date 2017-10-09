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
## <a name="setting-up-your-web-server-or-project"></a><span data-ttu-id="66f04-103">Configuración del servidor web o proyecto</span><span class="sxs-lookup"><span data-stu-id="66f04-103">Setting up your web server or project</span></span>

> <span data-ttu-id="66f04-104">¿Prefiere toodownload proyecto de este ejemplo en su lugar?</span><span class="sxs-lookup"><span data-stu-id="66f04-104">Prefer toodownload this sample's project instead?</span></span> 
> - [<span data-ttu-id="66f04-105">Descargar el proyecto de Visual Studio Hola</span><span class="sxs-lookup"><span data-stu-id="66f04-105">Download hello Visual Studio project</span></span>](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/VisualStudio.zip)
>
> <span data-ttu-id="66f04-106">o</span><span class="sxs-lookup"><span data-stu-id="66f04-106">or</span></span>
> - <span data-ttu-id="66f04-107">[Descargar archivos de proyecto de hello](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip) para un servidor web local, como Python</span><span class="sxs-lookup"><span data-stu-id="66f04-107">[Download hello project files](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip) for a local web server, such as Python</span></span>
>
> <span data-ttu-id="66f04-108">Y, a continuación, omitir toohello [paso de configuración](#create-an-application-express) ejemplo de código de hello tooconfigure antes de ejecutarlo.</span><span class="sxs-lookup"><span data-stu-id="66f04-108">And then  skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing it.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66f04-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="66f04-109">Prerequisites</span></span>
<span data-ttu-id="66f04-110">Un servidor web local como [Python http.server](https://www.python.org/downloads/), [http server](https://www.npmjs.com/package/http-server/), [.NET Core](https://www.microsoft.com/net/core), o la integración de IIS Express con [2017 de Visual Studio](https://www.visualstudio.com/downloads/) es necesario toorun esta configuración paso a paso.</span><span class="sxs-lookup"><span data-stu-id="66f04-110">A local web server such as [Python http.server](https://www.python.org/downloads/), [http-server](https://www.npmjs.com/package/http-server/), [.NET Core](https://www.microsoft.com/net/core), or IIS Express integration with [Visual Studio 2017](https://www.visualstudio.com/downloads/) is required toorun this guided setup.</span></span> 

<span data-ttu-id="66f04-111">Instrucciones de esta guía se basan en Python y 2017 de Visual Studio, pero Siéntase libre toouse cualquier otro entorno de desarrollo o un servidor Web.</span><span class="sxs-lookup"><span data-stu-id="66f04-111">Instructions in this guide are based on both Python and Visual Studio 2017, but feel free toouse any other development environment or Web Server.</span></span>

## <a name="create-your-project"></a><span data-ttu-id="66f04-112">Creación del proyecto</span><span class="sxs-lookup"><span data-stu-id="66f04-112">Create your project</span></span> 

> ### <a name="option-1-visual-studio"></a><span data-ttu-id="66f04-113">Opción 1: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="66f04-113">Option 1: Visual Studio</span></span> 
> <span data-ttu-id="66f04-114">Si usa Visual Studio y a crear un nuevo proyecto, siga estos pasos hello toocreate una nueva solución de Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="66f04-114">If you are using Visual Studio and are creating a new project, follow hello steps below toocreate a new Visual Studio solution:</span></span>
> 1.    <span data-ttu-id="66f04-115">En Visual Studio:  `File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="66f04-115">In Visual Studio:  `File` > `New` > `Project`</span></span>
> 2.    <span data-ttu-id="66f04-116">En `Visual C#\Web`, seleccione `ASP.NET Web Application (.NET Framework)`</span><span class="sxs-lookup"><span data-stu-id="66f04-116">Under `Visual C#\Web`, select `ASP.NET Web Application (.NET Framework)`</span></span>
> 3.    <span data-ttu-id="66f04-117">Asigne un nombre a la aplicación y haga clic en *Aceptar*.</span><span class="sxs-lookup"><span data-stu-id="66f04-117">Name your application and click *OK*</span></span>
> 4.    <span data-ttu-id="66f04-118">En `New ASP.NET Web Application`, seleccione `Empty`</span><span class="sxs-lookup"><span data-stu-id="66f04-118">Under `New ASP.NET Web Application`, select `Empty`</span></span>

<p/><!-- -->

> ### <a name="option-2-python-other-web-servers"></a><span data-ttu-id="66f04-119">Opción 2: Python u otros servidores web</span><span class="sxs-lookup"><span data-stu-id="66f04-119">Option 2: Python/ other web servers</span></span>
> <span data-ttu-id="66f04-120">Asegúrese de que ha instalado [Python](https://www.python.org/downloads/), a continuación, siga el paso de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="66f04-120">Make sure you have installed [Python](https://www.python.org/downloads/), then follow hello step below:</span></span>
> - <span data-ttu-id="66f04-121">Crear una carpeta toohost su aplicación.</span><span class="sxs-lookup"><span data-stu-id="66f04-121">Create a folder toohost your application.</span></span>


## <a name="create-your-single-page-applications-ui"></a><span data-ttu-id="66f04-122">Cree la interfaz de usuario de la aplicación de una sola página</span><span class="sxs-lookup"><span data-stu-id="66f04-122">Create your single page application’s UI</span></span>
1.  <span data-ttu-id="66f04-123">Cree un archivo *index.html* para JavaScript SPA.</span><span class="sxs-lookup"><span data-stu-id="66f04-123">Create an *index.html* file for your JavaScript SPA.</span></span> <span data-ttu-id="66f04-124">Si usas el proyecto de Visual Studio, seleccione hello (carpeta raíz del proyecto), haga clic en y seleccione: `Add`  >  `New Item`  >  `HTML page` y asígnele el nombre index.html</span><span class="sxs-lookup"><span data-stu-id="66f04-124">If you are using Visual Studio, select hello project (project root folder), right click and select: `Add` > `New Item` > `HTML page` and name it index.html</span></span>
2.  <span data-ttu-id="66f04-125">Agregue Hola después de la página de códigos tooyour:</span><span class="sxs-lookup"><span data-stu-id="66f04-125">Add hello following code tooyour page:</span></span>
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
