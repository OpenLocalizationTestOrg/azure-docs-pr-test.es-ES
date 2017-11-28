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
## <a name="add-hello-applications-registration-information-tooyour-app"></a><span data-ttu-id="53413-103">Agregar tooyour de información de registro de la aplicación hello aplicación</span><span class="sxs-lookup"><span data-stu-id="53413-103">Add hello application’s registration information tooyour App</span></span>

<span data-ttu-id="53413-104">En este paso, necesita la dirección URL de redireccionamiento de hello tooconfigure de la información de registro de aplicación y, a continuación, Agregar aplicación de JavaScript SPA tooyour de hello Id. de aplicación.</span><span class="sxs-lookup"><span data-stu-id="53413-104">In this step, you need tooconfigure hello Redirect URL of your application registration information and then add hello Application Id tooyour JavaScript SPA application.</span></span>

### <a name="configure-redirect-url"></a><span data-ttu-id="53413-105">Configuración de la URL de redireccionamiento</span><span class="sxs-lookup"><span data-stu-id="53413-105">Configure redirect URL</span></span>

<span data-ttu-id="53413-106">Configurar hello `Redirect URL` campo anteriormente con la dirección URL de hello para la página index.html basándose en el servidor web, a continuación, haga clic en *actualización*.</span><span class="sxs-lookup"><span data-stu-id="53413-106">Configure hello `Redirect URL` field above with hello URL for your index.html page based on your web server, then click *Update*.</span></span>


> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a><span data-ttu-id="53413-107">Instrucciones en Visual Studio para obtener la dirección URL de redireccionamiento</span><span class="sxs-lookup"><span data-stu-id="53413-107">Visual Studio instructions for obtaining redirect URL</span></span>
> <span data-ttu-id="53413-108">tooobtain la dirección URL de redireccionamiento, siga las instrucciones de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="53413-108">tooobtain your redirect URL, follow hello instructions below:</span></span>
> 1.    <span data-ttu-id="53413-109">En *el Explorador de soluciones*, seleccione el proyecto de Hola y mire hello `Properties` ventana (si no ve una ventana de propiedades, presione `F4`)</span><span class="sxs-lookup"><span data-stu-id="53413-109">In *Solution Explorer*, select hello project and look at hello `Properties` window (if you don’t see a Properties window, press `F4`)</span></span>
> 2.    <span data-ttu-id="53413-110">Copiar valor de Hola de `URL` toohello Portapapeles:</span><span class="sxs-lookup"><span data-stu-id="53413-110">Copy hello value from `URL` toohello clipboard:</span></span><br/> <span data-ttu-id="53413-111">![Propiedades del proyecto](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span><span class="sxs-lookup"><span data-stu-id="53413-111">![Project properties](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span></span><br />
> 3.    <span data-ttu-id="53413-112">Pegue el valor de Hola como un `Redirect URL` en hello parte superior de esta página, a continuación, haga clic en`Update`</span><span class="sxs-lookup"><span data-stu-id="53413-112">Paste hello value as a `Redirect URL` on hello top of this page, then click `Update`</span></span>

<p/>

> #### <a name="setting-redirect-url-for-python"></a><span data-ttu-id="53413-113">Configuración de la dirección URL de redireccionamiento para Python</span><span class="sxs-lookup"><span data-stu-id="53413-113">Setting Redirect URL for Python</span></span>
> <span data-ttu-id="53413-114">Para Python, puede establecer el puerto de servidor web de Hola a través de la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="53413-114">For Python, you can set hello web server port via command line.</span></span> <span data-ttu-id="53413-115">Este programa de instalación guiada utiliza el puerto de hello 8080 para referencia pero Siéntase libre toouse cualquier puerto disponible.</span><span class="sxs-lookup"><span data-stu-id="53413-115">This guided setup uses hello port 8080 for reference but feel free toouse any other port available.</span></span> <span data-ttu-id="53413-116">En cualquier caso, siga instrucciones hello tooset una dirección URL de redireccionamiento en información de registro de aplicación Hola:</span><span class="sxs-lookup"><span data-stu-id="53413-116">In any case, follow hello instructions below tooset up a redirect URL in hello application registration information:</span></span><br/>
> <span data-ttu-id="53413-117">Establecer `http://localhost:8080/` como un `Redirect URL` Hola parte superior de esta página, o use `http://localhost:[port]/` si usa un puerto TCP personalizado (donde *[puerto]* es el número de puerto TCP personalizado hello) y, a continuación, haga clic en "Actualizar"</span><span class="sxs-lookup"><span data-stu-id="53413-117">Set `http://localhost:8080/` as a `Redirect URL` on hello top of this page, or use `http://localhost:[port]/` if you are using a custom TCP port (where *[port]* is hello custom TCP port number), and then click 'Update'</span></span>

### <a name="configure-your-javascript-spa-application"></a><span data-ttu-id="53413-118">Configuración de la aplicación JavaScript SPA</span><span class="sxs-lookup"><span data-stu-id="53413-118">Configure your JavaScript SPA application</span></span>

1.  <span data-ttu-id="53413-119">Cree un archivo denominado `msalconfig.js` que contiene información de registro de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="53413-119">Create a file named `msalconfig.js` containing hello application registration information.</span></span> <span data-ttu-id="53413-120">Si usas el proyecto de Visual Studio, seleccione hello (carpeta raíz del proyecto), haga clic en y seleccione: `Add`  >  `New Item`  >  `JavaScript File`.</span><span class="sxs-lookup"><span data-stu-id="53413-120">If you are using Visual Studio, select hello project (project root folder), right-click and select: `Add` > `New Item` > `JavaScript File`.</span></span> <span data-ttu-id="53413-121">Asígnele el nombre `msalconfig.js`.</span><span class="sxs-lookup"><span data-stu-id="53413-121">Name it `msalconfig.js`</span></span>
2.  <span data-ttu-id="53413-122">Agregar Hola después código tooyour `msalconfig.js` archivo:</span><span class="sxs-lookup"><span data-stu-id="53413-122">Add hello following code tooyour `msalconfig.js` file:</span></span>

```javascript
var msalconfig = {
    clientID: "[Enter hello application Id here]",
    redirectUri: location.origin
};
``` 
