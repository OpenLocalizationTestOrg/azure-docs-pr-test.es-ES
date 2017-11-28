---
title: "aaaHow tooUse Apache Cordova complemento para las aplicaciones móviles de Azure"
description: "¿Cómo tooUse Apache Cordova complemento para las aplicaciones móviles de Azure"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: a56a1ce4-de0c-4f3c-8763-66252c52aa59
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: d3e0639e6478c409132af25304a2fb0f28401e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-apache-cordova-client-library-for-azure-mobile-apps"></a><span data-ttu-id="6ab74-103">La biblioteca de cliente de Apache Cordova toouse para aplicaciones móviles de Azure</span><span class="sxs-lookup"><span data-stu-id="6ab74-103">How toouse Apache Cordova client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="6ab74-104">Esta guía le enseña con hello más reciente de escenarios comunes de tooperform [Apache Cordova complemento para las aplicaciones de Azure Mobile].</span><span class="sxs-lookup"><span data-stu-id="6ab74-104">This guide teaches you tooperform common scenarios using hello latest [Apache Cordova Plugin for Azure Mobile Apps].</span></span> <span data-ttu-id="6ab74-105">Si estás nuevas aplicaciones de Mobile tooAzure, complete primero [inicio rápido de Azure Mobile Apps] toocreate un back-end, cree una tabla y descargar un proyecto de Apache Cordova pregenerado.</span><span class="sxs-lookup"><span data-stu-id="6ab74-105">If you are new tooAzure Mobile Apps, first complete [Azure Mobile Apps Quick Start] toocreate a backend, create a table, and download a pre-built Apache Cordova project.</span></span> <span data-ttu-id="6ab74-106">Esta guía se centra en Hola de cliente Apache Cordova complemento.</span><span class="sxs-lookup"><span data-stu-id="6ab74-106">In this guide, we focus on hello client-side Apache Cordova Plugin.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="6ab74-107">Plataformas compatibles</span><span class="sxs-lookup"><span data-stu-id="6ab74-107">Supported platforms</span></span>
<span data-ttu-id="6ab74-108">Este SDK es compatible con la versión 6.0.0 y posterior de Apache Cordova en dispositivos iOS, Android y Windows.</span><span class="sxs-lookup"><span data-stu-id="6ab74-108">This SDK supports Apache Cordova v6.0.0 and later on iOS, Android, and Windows devices.</span></span>  <span data-ttu-id="6ab74-109">compatibilidad con la plataforma de Hello es como sigue:</span><span class="sxs-lookup"><span data-stu-id="6ab74-109">hello platform support is as follows:</span></span>

* <span data-ttu-id="6ab74-110">Niveles de API de Android del 19 al 24 (de KitKat a Nougat)</span><span class="sxs-lookup"><span data-stu-id="6ab74-110">Android API 19-24 (KitKat through Nougat).</span></span>
* <span data-ttu-id="6ab74-111">Versiones 8.0 y posteriores de iOS.</span><span class="sxs-lookup"><span data-stu-id="6ab74-111">iOS versions 8.0 and later.</span></span>
* <span data-ttu-id="6ab74-112">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="6ab74-112">Windows Phone 8.1.</span></span>
* <span data-ttu-id="6ab74-113">Plataforma universal de Windows</span><span class="sxs-lookup"><span data-stu-id="6ab74-113">Universal Windows Platform.</span></span>

## <span data-ttu-id="6ab74-114"><a name="Setup"></a>Configuración y requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6ab74-114"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="6ab74-115">En esta guía se asume que ha creado un back-end con una tabla.</span><span class="sxs-lookup"><span data-stu-id="6ab74-115">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="6ab74-116">Esta guía se da por supuesto que tiene de esa tabla Hola Hola mismo esquema como tablas de hello en los tutoriales.</span><span class="sxs-lookup"><span data-stu-id="6ab74-116">This guide assumes that hello table has hello same schema as hello tables in those tutorials.</span></span> <span data-ttu-id="6ab74-117">Esta guía también se da por supuesto que ha agregado código de hello Apache Cordova complemento tooyour.</span><span class="sxs-lookup"><span data-stu-id="6ab74-117">This guide also assumes that you have added hello Apache Cordova Plugin tooyour code.</span></span>  <span data-ttu-id="6ab74-118">Si aún no lo ha hecho, puede agregar el complemento tooyour proyecto de hello Apache Cordova en línea de comandos de hello:</span><span class="sxs-lookup"><span data-stu-id="6ab74-118">If you have not done so, you may add hello Apache Cordova plugin tooyour project on hello command line:</span></span>

```
cordova plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="6ab74-119">Para más información sobre la creación de [su primera aplicación de Apache Cordova], consulte su documentación.</span><span class="sxs-lookup"><span data-stu-id="6ab74-119">For more information on creating [your first Apache Cordova app], see their documentation.</span></span>

## <span data-ttu-id="6ab74-120"><a name="ionic"></a>Configuración de una aplicación de Ionic v2</span><span class="sxs-lookup"><span data-stu-id="6ab74-120"><a name="ionic"></a>Setting up an Ionic v2 app</span></span>

<span data-ttu-id="6ab74-121">tooproperly configurar un proyecto de Ionic v2, primero cree una aplicación básica y agregar complemento de Cordova hello:</span><span class="sxs-lookup"><span data-stu-id="6ab74-121">tooproperly configure an Ionic v2 project, first create a basic app and add hello Cordova plugin:</span></span>

```
ionic start projectName --v2
cd projectName
ionic plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="6ab74-122">Agregar Hola después líneas demasiado`app.component.ts` objeto de cliente hello toocreate:</span><span class="sxs-lookup"><span data-stu-id="6ab74-122">Add hello following lines too`app.component.ts` toocreate hello client object:</span></span>

```
declare var WindowsAzure: any;
var client = new WindowsAzure.MobileServiceClient("https://yoursite.azurewebsites.net");
```

<span data-ttu-id="6ab74-123">Ahora puede compilar y ejecutar el proyecto de hello en el Explorador de hello:</span><span class="sxs-lookup"><span data-stu-id="6ab74-123">You can now build and run hello project in hello browser:</span></span>

```
ionic platform add browser
ionic run browser
```

<span data-ttu-id="6ab74-124">complemento de Cordova de aplicaciones móviles de Azure de Hello es compatible con ambas aplicaciones Ionic v1 y v2.</span><span class="sxs-lookup"><span data-stu-id="6ab74-124">hello Azure Mobile Apps Cordova plugin supports both Ionic v1 and v2 apps.</span></span>  <span data-ttu-id="6ab74-125">Solo aplicaciones Hola v2 Ionic requieren la declaración adicional para hello `WindowsAzure` objeto.</span><span class="sxs-lookup"><span data-stu-id="6ab74-125">Only hello Ionic v2 apps require the additional declaration for hello `WindowsAzure` object.</span></span>

[!INCLUDE [app-service-mobile-html-js-library.md](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="6ab74-126"><a name="auth"></a>Autenticación de usuarios</span><span class="sxs-lookup"><span data-stu-id="6ab74-126"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="6ab74-127">Azure App Service es compatible con la autenticación y autorización de los usuarios de aplicaciones mediante diversos proveedores de identidades externos: Facebook, Google, Cuenta Microsoft y Twitter.</span><span class="sxs-lookup"><span data-stu-id="6ab74-127">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="6ab74-128">Puede establecer permisos de acceso de toorestrict de tablas para operaciones específicas tooonly autenticado a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="6ab74-128">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="6ab74-129">También puede utilizar la identidad de Hola de reglas de autorización de los usuarios autenticados tooimplement en scripts de servidor.</span><span class="sxs-lookup"><span data-stu-id="6ab74-129">You can also use hello identity of authenticated users tooimplement authorization rules in server scripts.</span></span> <span data-ttu-id="6ab74-130">Para obtener más información, vea hello [empezar a trabajar con autenticación] tutorial.</span><span class="sxs-lookup"><span data-stu-id="6ab74-130">For more information, see hello [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="6ab74-131">Al utilizar la autenticación en una aplicación de Apache Cordova, Hola siguiendo los complementos de Cordova debe estar disponible:</span><span class="sxs-lookup"><span data-stu-id="6ab74-131">When using authentication in an Apache Cordova app, hello following Cordova plugins must be available:</span></span>

* <span data-ttu-id="6ab74-132">[cordova-plugin-device]</span><span class="sxs-lookup"><span data-stu-id="6ab74-132">[cordova-plugin-device]</span></span>
* <span data-ttu-id="6ab74-133">[cordova-plugin-inappbrowser]</span><span class="sxs-lookup"><span data-stu-id="6ab74-133">[cordova-plugin-inappbrowser]</span></span>

<span data-ttu-id="6ab74-134">Se admiten dos flujos de autenticación: un flujo de servidor y un flujo de cliente.</span><span class="sxs-lookup"><span data-stu-id="6ab74-134">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="6ab74-135">flujo de servidor Hello proporciona experiencia de autenticación más sencilla de hello, tal y como se basa en la interfaz de autenticación del proveedor de hello web.</span><span class="sxs-lookup"><span data-stu-id="6ab74-135">hello server flow provides hello simplest authentication experience, as it relies on hello provider's web authentication interface.</span></span> <span data-ttu-id="6ab74-136">Hello flujo del cliente permite una integración más profunda con capacidades específicas del dispositivo como inicio de sesión único como se basa en el SDK de específica del proveedor específico del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6ab74-136">hello client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific device-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library.md](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="6ab74-137"><a name="configure-external-redirect-urls"></a>Cómo configurar el servicio de Mobile Apps para URL de redireccionamiento externas</span><span class="sxs-lookup"><span data-stu-id="6ab74-137"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="6ab74-138">Varios tipos de aplicaciones de Apache Cordova usan un toohandle de capacidad de bucle invertido que OAuth UI flujos.</span><span class="sxs-lookup"><span data-stu-id="6ab74-138">Several types of Apache Cordova applications use a loopback capability toohandle OAuth UI flows.</span></span>  <span data-ttu-id="6ab74-139">Flujos de OAuth UI en localhost causar problemas ya que solo conoce el servicio de autenticación de hello cómo tooutilize su servicio de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="6ab74-139">OAuth UI flows on localhost cause problems since hello authentication service only knows how tooutilize your service by default.</span></span>  <span data-ttu-id="6ab74-140">Ejemplos de flujos de interfaz de usuario de OAuth problemáticos:</span><span class="sxs-lookup"><span data-stu-id="6ab74-140">Examples of problematic OAuth UI flows include:</span></span>

* <span data-ttu-id="6ab74-141">emulador Hola.</span><span class="sxs-lookup"><span data-stu-id="6ab74-141">hello Ripple emulator.</span></span>
* <span data-ttu-id="6ab74-142">La característica Live Reload con Ionic</span><span class="sxs-lookup"><span data-stu-id="6ab74-142">Live Reload with Ionic.</span></span>
* <span data-ttu-id="6ab74-143">Ejecución Hola móviles back-end localmente</span><span class="sxs-lookup"><span data-stu-id="6ab74-143">Running hello mobile backend locally</span></span>
* <span data-ttu-id="6ab74-144">Ejecuta back-end de hello móvil en un servicio de aplicación de Azure diferente que la autenticación de proporcionando un saludo.</span><span class="sxs-lookup"><span data-stu-id="6ab74-144">Running hello mobile backend in a different Azure App Service than hello one providing authentication.</span></span>

<span data-ttu-id="6ab74-145">Siga estas instrucciones tooadd la configuración de toohello de configuración local:</span><span class="sxs-lookup"><span data-stu-id="6ab74-145">Follow these instructions tooadd your local settings toohello configuration:</span></span>

1. <span data-ttu-id="6ab74-146">Inicie sesión en toohello [portal de Azure]</span><span class="sxs-lookup"><span data-stu-id="6ab74-146">Log in toohello [Azure portal]</span></span>
2. <span data-ttu-id="6ab74-147">Seleccione **todos los recursos** o **servicios de aplicaciones** , a continuación, haga clic en nombre de saludo de la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="6ab74-147">Select **All resources** or **App Services** then click hello name of your Mobile App.</span></span>
3. <span data-ttu-id="6ab74-148">Haga clic en **Herramientas**</span><span class="sxs-lookup"><span data-stu-id="6ab74-148">Click **Tools**</span></span>
4. <span data-ttu-id="6ab74-149">Haga clic en **Explorador de recursos** en el menú OBSERVE hello, a continuación, haga clic en **vaya**.</span><span class="sxs-lookup"><span data-stu-id="6ab74-149">Click **Resource explorer** in hello OBSERVE menu, then click **Go**.</span></span>  <span data-ttu-id="6ab74-150">Se abrirá una nueva ventana o pestaña.</span><span class="sxs-lookup"><span data-stu-id="6ab74-150">A new window or tab opens.</span></span>
5. <span data-ttu-id="6ab74-151">Expanda hello **config**, **authsettings** nodos para su sitio en el panel de navegación izquierdo Hola.</span><span class="sxs-lookup"><span data-stu-id="6ab74-151">Expand hello **config**, **authsettings** nodes for your site in hello left-hand navigation.</span></span>
6. <span data-ttu-id="6ab74-152">Haga clic en **Editar**</span><span class="sxs-lookup"><span data-stu-id="6ab74-152">Click **Edit**</span></span>
7. <span data-ttu-id="6ab74-153">Busque el elemento de "allowedExternalRedirectUrls" Hola.</span><span class="sxs-lookup"><span data-stu-id="6ab74-153">Look for hello "allowedExternalRedirectUrls" element.</span></span>  <span data-ttu-id="6ab74-154">Se puede establecer toonull o una matriz de valores.</span><span class="sxs-lookup"><span data-stu-id="6ab74-154">It may be set toonull or an array of values.</span></span>  <span data-ttu-id="6ab74-155">Cambiar Hola valor toohello siguiente valor:</span><span class="sxs-lookup"><span data-stu-id="6ab74-155">Change hello value toohello following value:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="6ab74-156">Reemplace hello las direcciones URL con hello las direcciones URL de su servicio.</span><span class="sxs-lookup"><span data-stu-id="6ab74-156">Replace hello URLs with hello URLs of your service.</span></span>  <span data-ttu-id="6ab74-157">Algunos ejemplos son "http://localhost:3000" (para el servicio de ejemplo de Node.js Hola) o "http://localhost:4400" (para el servicio de Ripple Hola).</span><span class="sxs-lookup"><span data-stu-id="6ab74-157">Examples include "http://localhost:3000" (for hello Node.js sample service), or "http://localhost:4400" (for hello Ripple service).</span></span>  <span data-ttu-id="6ab74-158">Sin embargo, estas direcciones URL son ejemplos: su situación, incluidos los servicios de hello mencionados en los ejemplos de hello, pueden ser diferentes.</span><span class="sxs-lookup"><span data-stu-id="6ab74-158">However, these URLs are examples - your situation, including for hello services mentioned in hello examples, may be different.</span></span>
8. <span data-ttu-id="6ab74-159">Haga clic en hello **lectura/escritura** botón en la esquina superior derecha de Hola de pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="6ab74-159">Click hello **Read/Write** button in hello top-right corner of hello screen.</span></span>
9. <span data-ttu-id="6ab74-160">Haga clic en hello verde **colocar** botón.</span><span class="sxs-lookup"><span data-stu-id="6ab74-160">Click hello green **PUT** button.</span></span>

<span data-ttu-id="6ab74-161">configuración de Hola se guarda en este momento.</span><span class="sxs-lookup"><span data-stu-id="6ab74-161">hello settings are saved at this point.</span></span>  <span data-ttu-id="6ab74-162">No cierre la ventana del explorador Hola hasta que finaliza la configuración de hello guardar.</span><span class="sxs-lookup"><span data-stu-id="6ab74-162">Do not close hello browser window until hello settings have finished saving.</span></span>
<span data-ttu-id="6ab74-163">Agregar esta configuración de CORS de toohello de bucle invertido las direcciones URL para el servicio de aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="6ab74-163">Also add these loopback URLs toohello CORS settings for your App Service:</span></span>

1. <span data-ttu-id="6ab74-164">Inicie sesión en toohello [portal de Azure]</span><span class="sxs-lookup"><span data-stu-id="6ab74-164">Log in toohello [Azure portal]</span></span>
2. <span data-ttu-id="6ab74-165">Seleccione **todos los recursos** o **servicios de aplicaciones** , a continuación, haga clic en nombre de saludo de la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="6ab74-165">Select **All resources** or **App Services** then click hello name of your Mobile App.</span></span>
3. <span data-ttu-id="6ab74-166">hoja de configuración de Hola se abre automáticamente.</span><span class="sxs-lookup"><span data-stu-id="6ab74-166">hello Settings blade opens automatically.</span></span>  <span data-ttu-id="6ab74-167">En caso contrario, haga clic en **Toda la configuración**.</span><span class="sxs-lookup"><span data-stu-id="6ab74-167">If it doesn't, click **All Settings**.</span></span>
4. <span data-ttu-id="6ab74-168">Haga clic en **CORS** en el menú de hello API.</span><span class="sxs-lookup"><span data-stu-id="6ab74-168">Click **CORS** under hello API menu.</span></span>
5. <span data-ttu-id="6ab74-169">Escriba la dirección URL de Hola que desee tooadd en cuadro Hola correspondiente y presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="6ab74-169">Enter hello URL that you wish tooadd in hello box provided and press Enter.</span></span>
6. <span data-ttu-id="6ab74-170">Escriba las direcciones URL adicionales que necesite.</span><span class="sxs-lookup"><span data-stu-id="6ab74-170">Enter additional URLs as needed.</span></span>
7. <span data-ttu-id="6ab74-171">Haga clic en **guardar** configuración de toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="6ab74-171">Click **Save** toosave hello settings.</span></span>

<span data-ttu-id="6ab74-172">Tarda aproximadamente 10-15 segundos para el efecto de hello nueva configuración tootake.</span><span class="sxs-lookup"><span data-stu-id="6ab74-172">It takes approximately 10-15 seconds for hello new settings tootake effect.</span></span>

## <span data-ttu-id="6ab74-173"><a name="register-for-push"></a>Registrar notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="6ab74-173"><a name="register-for-push"></a>How to: Register for push notifications</span></span>
<span data-ttu-id="6ab74-174">Instalar hello [phonegap-plugin-inserción] toohandle notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="6ab74-174">Install hello [phonegap-plugin-push] toohandle push notifications.</span></span>  <span data-ttu-id="6ab74-175">Este complemento se puede agregar fácilmente mediante la `cordova plugin add` comando en la línea de comandos de hello, o mediante el instalador de complemento de hello Git en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6ab74-175">This plugin can be easily added using the `cordova plugin add` command on hello command line, or via hello Git plugin installer within Visual Studio.</span></span>  <span data-ttu-id="6ab74-176">El siguiente código de la aplicación de Apache Cordova registrará el dispositivo para notificaciones push:</span><span class="sxs-lookup"><span data-stu-id="6ab74-176">The following code in your Apache Cordova app registers your device for push notifications:</span></span>

```
var pushOptions = {
    android: {
        senderId: '<from-gcm-console>'
    },
    ios: {
        alert: true,
        badge: true,
        sound: true
    },
    windows: {
    }
};
pushHandler = PushNotification.init(pushOptions);

pushHandler.on('registration', function (data) {
    registrationId = data.registrationId;
    // For cross-platform, you can use hello device plugin toodetermine hello device
    // Best is toouse device.platform
    var name = 'gcm'; // For android - default
    if (device.platform.toLowerCase() === 'ios')
        name = 'apns';
    if (device.platform.toLowerCase().substring(0, 3) === 'win')
        name = 'wns';
    client.push.register(name, registrationId);
});

pushHandler.on('notification', function (data) {
    // data is an object and is whatever is sent by hello PNS - check hello format
    // for your particular PNS
});

pushHandler.on('error', function (error) {
    // Handle errors
});
```

<span data-ttu-id="6ab74-177">Usar notificaciones de inserción de toosend Hola SDK de bases de datos centrales de notificación del servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="6ab74-177">Use hello Notification Hubs SDK toosend push notifications from hello server.</span></span>  <span data-ttu-id="6ab74-178">No envíe nunca notificaciones push directamente desde la aplicación,</span><span class="sxs-lookup"><span data-stu-id="6ab74-178">Never send push notifications directly from clients.</span></span> <span data-ttu-id="6ab74-179">Al hacerlo así podría tootrigger usado un ataque de denegación de servicio en los centros de notificaciones u Hola PNS.</span><span class="sxs-lookup"><span data-stu-id="6ab74-179">Doing so could be used tootrigger a denial of service attack against Notification Hubs or hello PNS.</span></span>  <span data-ttu-id="6ab74-180">Hola PNS podría prohibir el tráfico como resultado de estos ataques.</span><span class="sxs-lookup"><span data-stu-id="6ab74-180">hello PNS could ban your traffic as a result of such attacks.</span></span>

## <a name="more-information"></a><span data-ttu-id="6ab74-181">Más información</span><span class="sxs-lookup"><span data-stu-id="6ab74-181">More information</span></span>

<span data-ttu-id="6ab74-182">Puede encontrar información detallada sobre las API en nuestra [documentación de la API](http://azure.github.io/azure-mobile-apps-js-client/).</span><span class="sxs-lookup"><span data-stu-id="6ab74-182">You can find detailed API details in our [API documentation](http://azure.github.io/azure-mobile-apps-js-client/).</span></span>

<!-- URLs. -->
[Portal de Azure]: https://portal.azure.com
[Creación de una aplicación de Apache Cordova]: app-service-mobile-cordova-get-started.md
[Introducción a la autenticación]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[complemento de Apache Cordova para Aplicaciones móviles de Azure]: https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-apps
[su primera aplicación de Apache Cordova]: http://cordova.apache.org/#getstarted
[phonegap-facebook-plugin]: https://github.com/wizcorp/phonegap-facebook-plugin
[phonegap-plugin-push]: https://www.npmjs.com/package/phonegap-plugin-push
[cordova-plugin-device]: https://www.npmjs.com/package/cordova-plugin-device
[cordova-plugin-inappbrowser]: https://www.npmjs.com/package/cordova-plugin-inappbrowser
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
