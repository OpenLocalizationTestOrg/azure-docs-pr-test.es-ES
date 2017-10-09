---
title: "aaaHow tooUse Hola JavaScript SDK para aplicaciones móviles de Azure"
description: "¿Cómo tooUse v para aplicaciones móviles de Azure"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 53b78965-caa3-4b22-bb67-5bd5c19d03c4
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 3fcbb0c5bd6918a285bdafa1946ba0bd47bb21b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-javascript-client-library-for-azure-mobile-apps"></a><span data-ttu-id="5d81c-103">¿Cómo tooUse Hola biblioteca de cliente de JavaScript para aplicaciones móviles de Azure</span><span class="sxs-lookup"><span data-stu-id="5d81c-103">How tooUse hello JavaScript client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="5d81c-104">Esta guía le enseña con hello más reciente de escenarios comunes de tooperform [JavaScript SDK para aplicaciones móviles de Azure].</span><span class="sxs-lookup"><span data-stu-id="5d81c-104">This guide teaches you tooperform common scenarios using hello latest [JavaScript SDK for Azure Mobile Apps].</span></span> <span data-ttu-id="5d81c-105">Si estás nuevas aplicaciones de Mobile tooAzure, complete primero [inicio rápido de Azure Mobile Apps] toocreate un back-end y cree una tabla.</span><span class="sxs-lookup"><span data-stu-id="5d81c-105">If you are new tooAzure Mobile Apps, first complete [Azure Mobile Apps Quick Start] toocreate a backend and create a table.</span></span> <span data-ttu-id="5d81c-106">En esta guía, se centran en el uso de back-end de hello móviles en aplicaciones Web HTML/JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5d81c-106">In this guide, we focus on using hello mobile backend in HTML/JavaScript Web applications.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="5d81c-107">Plataformas compatibles</span><span class="sxs-lookup"><span data-stu-id="5d81c-107">Supported platforms</span></span>
<span data-ttu-id="5d81c-108">Se limitar actual de toohello de compatibilidad con explorador y el apellido de versiones de hello principales exploradores: Google Chrome, Microsoft Edge, Microsoft Internet Explorer y Mozilla Firefox.</span><span class="sxs-lookup"><span data-stu-id="5d81c-108">We limit browser support toohello current and last versions of hello major browsers:  Google Chrome, Microsoft Edge, Microsoft Internet Explorer, and Mozilla Firefox.</span></span>  <span data-ttu-id="5d81c-109">Esperamos que Hola SDK toofunction con cualquier explorador moderno relativamente.</span><span class="sxs-lookup"><span data-stu-id="5d81c-109">We expect hello SDK toofunction with any relatively modern browser.</span></span>

<span data-ttu-id="5d81c-110">paquete de Hola se distribuye como un módulo de JavaScript Universal, por lo que es compatible con las variables globales, AMD, y da formato a CommonJS.</span><span class="sxs-lookup"><span data-stu-id="5d81c-110">hello package is distributed as a Universal JavaScript Module, so it supports globals, AMD, and CommonJS formats.</span></span>

## <span data-ttu-id="5d81c-111"><a name="Setup"></a>Configuración y requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5d81c-111"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="5d81c-112">En esta guía se asume que ha creado un back-end con una tabla.</span><span class="sxs-lookup"><span data-stu-id="5d81c-112">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="5d81c-113">Esta guía se da por supuesto que tiene de esa tabla Hola Hola mismo esquema como tablas de hello en los tutoriales.</span><span class="sxs-lookup"><span data-stu-id="5d81c-113">This guide assumes that hello table has hello same schema as hello tables in those tutorials.</span></span>

<span data-ttu-id="5d81c-114">Instalar Hola SDK de JavaScript de aplicaciones móviles de Azure puede hacerse a través de hello `npm` comando:</span><span class="sxs-lookup"><span data-stu-id="5d81c-114">Installing hello Azure Mobile Apps JavaScript SDK can be done via hello `npm` command:</span></span>

```
npm install azure-mobile-apps-client --save
```

<span data-ttu-id="5d81c-115">biblioteca de Hello también puede utilizarse como un módulo ES2015, dentro de entornos de CommonJS como Browserify y Webpack y como una biblioteca AMD.</span><span class="sxs-lookup"><span data-stu-id="5d81c-115">hello library can also be used as an ES2015 module, within CommonJS environments such as Browserify and Webpack and as an AMD library.</span></span>  <span data-ttu-id="5d81c-116">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5d81c-116">For example:</span></span>

```
# For ECMAScript 5.1 CommonJS
var WindowsAzure = require('azure-mobile-apps-client');
# For ES2015 modules
import * as WindowsAzure from 'azure-mobile-apps-client';
```

<span data-ttu-id="5d81c-117">También puede utilizar una versión previamente compilada de hello SDK descargando directamente desde la red CDN:</span><span class="sxs-lookup"><span data-stu-id="5d81c-117">You can also use a pre-built version of hello SDK by downloading directly from our CDN:</span></span>

```html
<script src="https://zumo.blob.core.windows.net/sdk/azure-mobile-apps-client.min.js"></script>
```

[!INCLUDE [app-service-mobile-html-js-library](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="5d81c-118"><a name="auth"></a>Autenticación de usuarios</span><span class="sxs-lookup"><span data-stu-id="5d81c-118"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="5d81c-119">Azure App Service es compatible con la autenticación y autorización de los usuarios de aplicaciones mediante diversos proveedores de identidades externos: Facebook, Google, Cuenta Microsoft y Twitter.</span><span class="sxs-lookup"><span data-stu-id="5d81c-119">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="5d81c-120">Puede establecer permisos de acceso de toorestrict de tablas para operaciones específicas tooonly autenticado a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="5d81c-120">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="5d81c-121">También puede utilizar la identidad de Hola de reglas de autorización de los usuarios autenticados tooimplement en scripts de servidor.</span><span class="sxs-lookup"><span data-stu-id="5d81c-121">You can also use hello identity of authenticated users tooimplement authorization rules in server scripts.</span></span> <span data-ttu-id="5d81c-122">Para obtener más información, vea hello [empezar a trabajar con autenticación] tutorial.</span><span class="sxs-lookup"><span data-stu-id="5d81c-122">For more information, see hello [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="5d81c-123">Se admiten dos flujos de autenticación: un flujo de servidor y un flujo de cliente.</span><span class="sxs-lookup"><span data-stu-id="5d81c-123">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="5d81c-124">flujo de servidor Hello proporciona experiencia de autenticación más sencilla de hello, tal y como se basa en la interfaz de autenticación del proveedor de hello web.</span><span class="sxs-lookup"><span data-stu-id="5d81c-124">hello server flow provides hello simplest authentication experience, as it relies on hello provider's web authentication interface.</span></span> <span data-ttu-id="5d81c-125">Hello flujo del cliente permite una integración más profunda con capacidades específicas del dispositivo como inicio de sesión único como se basa en SDK específicos del proveedor.</span><span class="sxs-lookup"><span data-stu-id="5d81c-125">hello client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="5d81c-126"><a name="configure-external-redirect-urls"></a>Cómo configurar el servicio de Mobile Apps para URL de redireccionamiento externas</span><span class="sxs-lookup"><span data-stu-id="5d81c-126"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="5d81c-127">Varios tipos de aplicaciones de JavaScript usan un toohandle de capacidad de bucle invertido que OAuth UI flujos.</span><span class="sxs-lookup"><span data-stu-id="5d81c-127">Several types of JavaScript applications use a loopback capability toohandle OAuth UI flows.</span></span>  <span data-ttu-id="5d81c-128">Estas son algunas de ellas:</span><span class="sxs-lookup"><span data-stu-id="5d81c-128">These capabilities include:</span></span>

* <span data-ttu-id="5d81c-129">Ejecución del servicio de manera local</span><span class="sxs-lookup"><span data-stu-id="5d81c-129">Running your service locally</span></span>
* <span data-ttu-id="5d81c-130">Uso de recarga de Live con hello marco de trabajo Ionic</span><span class="sxs-lookup"><span data-stu-id="5d81c-130">Using Live Reload with hello Ionic Framework</span></span>
* <span data-ttu-id="5d81c-131">Redirigir tooApp servicio para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="5d81c-131">Redirecting tooApp Service for authentication.</span></span>

<span data-ttu-id="5d81c-132">Ejecuta de forma local puede causar problemas ya que, de forma predeterminada, la autenticación es solo el servicio de aplicaciones configurado tooallow el acceso desde su aplicación móvil de back-end.</span><span class="sxs-lookup"><span data-stu-id="5d81c-132">Running locally can cause problems because, by default, App Service authentication is only configured tooallow access from your Mobile App backend.</span></span> <span data-ttu-id="5d81c-133">Usar hello siguiendo los pasos toochange Hola autenticación de tooenable de configuración de servicio de aplicaciones cuando se ejecuta el servidor de hello localmente:</span><span class="sxs-lookup"><span data-stu-id="5d81c-133">Use hello following steps toochange hello App Service settings tooenable authentication when running hello server locally:</span></span>

1. <span data-ttu-id="5d81c-134">Inicie sesión en toohello [portal de Azure]</span><span class="sxs-lookup"><span data-stu-id="5d81c-134">Log in toohello [Azure portal]</span></span>
2. <span data-ttu-id="5d81c-135">Navegue back-end de tooyour aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="5d81c-135">Navigate tooyour Mobile App backend.</span></span>
3. <span data-ttu-id="5d81c-136">Seleccione **Explorador de recursos** en hello **herramientas de desarrollo** menú.</span><span class="sxs-lookup"><span data-stu-id="5d81c-136">Select **Resource explorer** in hello **DEVELOPMENT TOOLS** menu.</span></span>
4. <span data-ttu-id="5d81c-137">Haga clic en **vaya** Explorador de recursos de hello tooopen para su aplicación móvil de back-end en una nueva pestaña o ventana.</span><span class="sxs-lookup"><span data-stu-id="5d81c-137">Click **Go** tooopen hello resource explorer for your Mobile App backend in a new tab or window.</span></span>
5. <span data-ttu-id="5d81c-138">Expanda hello **config** > **authsettings** nodo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5d81c-138">Expand hello **config** > **authsettings** node for your app.</span></span>
6. <span data-ttu-id="5d81c-139">Haga clic en hello **editar** botón tooenable edición de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d81c-139">Click hello **Edit** button tooenable editing of hello resource.</span></span>
7. <span data-ttu-id="5d81c-140">Buscar hello **allowedExternalRedirectUrls** elemento, que debe ser null.</span><span class="sxs-lookup"><span data-stu-id="5d81c-140">Find hello **allowedExternalRedirectUrls** element, which should be null.</span></span> <span data-ttu-id="5d81c-141">Agregue las direcciones URL en una matriz:</span><span class="sxs-lookup"><span data-stu-id="5d81c-141">Add your URLs in an array:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="5d81c-142">Reemplazar las direcciones URL de hello en la matriz de hello con hello las direcciones URL del servicio, que en este ejemplo es `http://localhost:3000` de servicio de ejemplo de Hola local Node.js.</span><span class="sxs-lookup"><span data-stu-id="5d81c-142">Replace hello URLs in hello array with hello URLs of your service, which in this example is `http://localhost:3000` for hello local Node.js sample service.</span></span> <span data-ttu-id="5d81c-143">También puede usar `http://localhost:4400` para servicio de Ripple de Hola o alguna otra dirección URL, según cómo esté configurada la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5d81c-143">You could also use `http://localhost:4400` for hello Ripple service or some other URL, depending on how your app is configured.</span></span>
8. <span data-ttu-id="5d81c-144">En la parte superior de Hola de página de hello, haga clic en **lectura/escritura**, a continuación, haga clic en **colocar** toosave las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="5d81c-144">At hello top of hello page, click **Read/Write**, then click **PUT** toosave your updates.</span></span>

<span data-ttu-id="5d81c-145">También necesita tooadd Hola configuración de lista blanca de direcciones CORS toohello de direcciones URL de bucle invertido mismo:</span><span class="sxs-lookup"><span data-stu-id="5d81c-145">You also need tooadd hello same loopback URLs toohello CORS whitelist settings:</span></span>

1. <span data-ttu-id="5d81c-146">Desplácese atrás toohello [portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="5d81c-146">Navigate back toohello [Azure portal].</span></span>
2. <span data-ttu-id="5d81c-147">Navegue back-end de tooyour aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="5d81c-147">Navigate tooyour Mobile App backend.</span></span>
3. <span data-ttu-id="5d81c-148">Haga clic en **CORS** en hello **API** menú.</span><span class="sxs-lookup"><span data-stu-id="5d81c-148">Click **CORS** in hello **API** menu.</span></span>
4. <span data-ttu-id="5d81c-149">Escriba cada dirección URL en hello vacía **permite orígenes** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="5d81c-149">Enter each URL in hello empty **Allowed Origins** text box.</span></span>  <span data-ttu-id="5d81c-150">Se crea un nuevo cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="5d81c-150">A new text box is created.</span></span>
5. <span data-ttu-id="5d81c-151">Haga clic en **GUARDAR**</span><span class="sxs-lookup"><span data-stu-id="5d81c-151">Click **SAVE**</span></span>

<span data-ttu-id="5d81c-152">Después de que se actualice el back-end de hello, será capaz de toouse Hola nuevo bucle invertido las direcciones URL en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5d81c-152">After hello backend updates, you will be able toouse hello new loopback URLs in your app.</span></span>

<!-- URLs. -->
[inicio rápido de Azure Mobile Apps]: app-service-mobile-cordova-get-started.md
[empezar a trabajar con autenticación]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[portal de Azure]: https://portal.azure.com/
[JavaScript SDK para aplicaciones móviles de Azure]: https://www.npmjs.com/package/azure-mobile-apps-client
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
