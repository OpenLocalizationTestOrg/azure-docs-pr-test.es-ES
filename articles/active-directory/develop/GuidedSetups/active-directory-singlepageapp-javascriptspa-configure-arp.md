---
title: "Configuración de SPA de JS en Azure AD v2: configuración (ARP) | Microsoft Docs"
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
ms.openlocfilehash: 708f4ff606d79639de979918a9cacd4ed75db311
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
## <a name="add-the-applications-registration-information-to-your-app"></a><span data-ttu-id="5e9e9-103">Adición de información de registro de la aplicación a su aplicación</span><span class="sxs-lookup"><span data-stu-id="5e9e9-103">Add the application’s registration information to your App</span></span>

<span data-ttu-id="5e9e9-104">En este paso, debe configurar la URL de redireccionamiento de la información de registro de su aplicación y, a continuación, agregar el identificador de la aplicación a la aplicación JavaScript SPA.</span><span class="sxs-lookup"><span data-stu-id="5e9e9-104">In this step, you need to configure the Redirect URL of your application registration information and then add the Application Id to your JavaScript SPA application.</span></span>

### <a name="configure-redirect-url"></a><span data-ttu-id="5e9e9-105">Configuración de la URL de redireccionamiento</span><span class="sxs-lookup"><span data-stu-id="5e9e9-105">Configure redirect URL</span></span>

<span data-ttu-id="5e9e9-106">Configure el campo `Redirect URL` superior con la dirección URL de su página index.html basada en su servidor web y, a continuación, haga clic en *Actualizar*.</span><span class="sxs-lookup"><span data-stu-id="5e9e9-106">Configure the `Redirect URL` field above with the URL for your index.html page based on your web server, then click *Update*.</span></span>


> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a><span data-ttu-id="5e9e9-107">Instrucciones en Visual Studio para obtener la dirección URL de redireccionamiento</span><span class="sxs-lookup"><span data-stu-id="5e9e9-107">Visual Studio instructions for obtaining redirect URL</span></span>
> <span data-ttu-id="5e9e9-108">Siga estas instrucciones para obtener la dirección URL de redireccionamiento:</span><span class="sxs-lookup"><span data-stu-id="5e9e9-108">To obtain your redirect URL, follow the instructions below:</span></span>
> 1.    <span data-ttu-id="5e9e9-109">En el *Explorador de soluciones*, seleccione el proyecto y fíjese en la ventana `Properties` (si no ve una ventana de propiedades, presione `F4`)</span><span class="sxs-lookup"><span data-stu-id="5e9e9-109">In *Solution Explorer*, select the project and look at the `Properties` window (if you don’t see a Properties window, press `F4`)</span></span>
> 2.    <span data-ttu-id="5e9e9-110">Copie el valor de `URL` en el Portapapeles:</span><span class="sxs-lookup"><span data-stu-id="5e9e9-110">Copy the value from `URL` to the clipboard:</span></span><br/> <span data-ttu-id="5e9e9-111">![Propiedades del proyecto](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span><span class="sxs-lookup"><span data-stu-id="5e9e9-111">![Project properties](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span></span><br />
> 3.    <span data-ttu-id="5e9e9-112">Pegue el valor como `Redirect URL` en la parte superior de esta página y, luego, haga clic en `Update`</span><span class="sxs-lookup"><span data-stu-id="5e9e9-112">Paste the value as a `Redirect URL` on the top of this page, then click `Update`</span></span>

<p/>

> #### <a name="setting-redirect-url-for-python"></a><span data-ttu-id="5e9e9-113">Configuración de la dirección URL de redireccionamiento para Python</span><span class="sxs-lookup"><span data-stu-id="5e9e9-113">Setting Redirect URL for Python</span></span>
> <span data-ttu-id="5e9e9-114">Para Python, puede establecer el puerto de servidor web a través de una línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="5e9e9-114">For Python, you can set the web server port via command line.</span></span> <span data-ttu-id="5e9e9-115">Esta configuración paso a paso usa el puerto 8080 como referencia, pero puede usar cualquier otro puerto que esté disponible.</span><span class="sxs-lookup"><span data-stu-id="5e9e9-115">This guided setup uses the port 8080 for reference but feel free to use any other port available.</span></span> <span data-ttu-id="5e9e9-116">Cualquiera sea el caso, siga las instrucciones siguientes para configurar una dirección URL de redireccionamiento en la información de registro de aplicación:</span><span class="sxs-lookup"><span data-stu-id="5e9e9-116">In any case, follow the instructions below to set up a redirect URL in the application registration information:</span></span><br/>
> <span data-ttu-id="5e9e9-117">Establezca `http://localhost:8080/` como `Redirect URL` en la parte superior de esta página, o bien use `http://localhost:[port]/` si usa un puerto TCP personalizado (donde *[puerto]* es el número de puerto TCP personalizado) y, luego, haga clic en "Update" (Actualizar)</span><span class="sxs-lookup"><span data-stu-id="5e9e9-117">Set `http://localhost:8080/` as a `Redirect URL` on the top of this page, or use `http://localhost:[port]/` if you are using a custom TCP port (where *[port]* is the custom TCP port number), and then click 'Update'</span></span>

### <a name="configure-your-javascript-spa-application"></a><span data-ttu-id="5e9e9-118">Configuración de la aplicación JavaScript SPA</span><span class="sxs-lookup"><span data-stu-id="5e9e9-118">Configure your JavaScript SPA application</span></span>

1.  <span data-ttu-id="5e9e9-119">Cree un archivo denominado `msalconfig.js` que contenga la información de registro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5e9e9-119">Create a file named `msalconfig.js` containing the application registration information.</span></span> <span data-ttu-id="5e9e9-120">Si se usa Visual Studio, seleccione el proyecto (carpeta raíz del proyecto), haga clic con el botón derecho y seleccione: `Add` > `New Item` > `JavaScript File`.</span><span class="sxs-lookup"><span data-stu-id="5e9e9-120">If you are using Visual Studio, select the project (project root folder), right-click and select: `Add` > `New Item` > `JavaScript File`.</span></span> <span data-ttu-id="5e9e9-121">Asígnele el nombre `msalconfig.js`.</span><span class="sxs-lookup"><span data-stu-id="5e9e9-121">Name it `msalconfig.js`</span></span>
2.  <span data-ttu-id="5e9e9-122">Agregue el siguiente código al archivo `msalconfig.js`:</span><span class="sxs-lookup"><span data-stu-id="5e9e9-122">Add the following code to your `msalconfig.js` file:</span></span>

```javascript
var msalconfig = {
    clientID: "[Enter the application Id here]",
    redirectUri: location.origin
};
``` 
