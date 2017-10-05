---
title: "Uso del complemento de Apache Cordova para Aplicaciones móviles de Azure"
description: "Uso del complemento de Apache Cordova para Aplicaciones móviles de Azure"
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
ms.openlocfilehash: ebf0e911eeada0e529f908dd3e3430c94edae763
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-apache-cordova-client-library-for-azure-mobile-apps"></a><span data-ttu-id="d691f-103">Uso de una biblioteca de cliente de Apache Cordova para Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="d691f-103">How to use Apache Cordova client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="d691f-104">En esta guía se muestran algunos escenarios comunes del uso del último [complemento de Apache Cordova para Aplicaciones móviles de Azure].</span><span class="sxs-lookup"><span data-stu-id="d691f-104">This guide teaches you to perform common scenarios using the latest [Apache Cordova Plugin for Azure Mobile Apps].</span></span> <span data-ttu-id="d691f-105">Si no está familiarizado con Aplicaciones móviles de Azure, realice primero el tutorial [Creación de una aplicación de Apache Cordova] para crear un back-end, crear una tabla y descargar un proyecto de Apache Cordova previamente compilado.</span><span class="sxs-lookup"><span data-stu-id="d691f-105">If you are new to Azure Mobile Apps, first complete [Azure Mobile Apps Quick Start] to create a backend, create a table, and download a pre-built Apache Cordova project.</span></span> <span data-ttu-id="d691f-106">En esta guía nos centramos en el complemento de Apache Cordova del lado cliente.</span><span class="sxs-lookup"><span data-stu-id="d691f-106">In this guide, we focus on the client-side Apache Cordova Plugin.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="d691f-107">Plataformas compatibles</span><span class="sxs-lookup"><span data-stu-id="d691f-107">Supported platforms</span></span>
<span data-ttu-id="d691f-108">Este SDK es compatible con la versión 6.0.0 y posterior de Apache Cordova en dispositivos iOS, Android y Windows.</span><span class="sxs-lookup"><span data-stu-id="d691f-108">This SDK supports Apache Cordova v6.0.0 and later on iOS, Android, and Windows devices.</span></span>  <span data-ttu-id="d691f-109">Las plataformas compatibles con las siguientes:</span><span class="sxs-lookup"><span data-stu-id="d691f-109">The platform support is as follows:</span></span>

* <span data-ttu-id="d691f-110">Niveles de API de Android del 19 al 24 (de KitKat a Nougat)</span><span class="sxs-lookup"><span data-stu-id="d691f-110">Android API 19-24 (KitKat through Nougat).</span></span>
* <span data-ttu-id="d691f-111">Versiones 8.0 y posteriores de iOS.</span><span class="sxs-lookup"><span data-stu-id="d691f-111">iOS versions 8.0 and later.</span></span>
* <span data-ttu-id="d691f-112">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="d691f-112">Windows Phone 8.1.</span></span>
* <span data-ttu-id="d691f-113">Plataforma universal de Windows</span><span class="sxs-lookup"><span data-stu-id="d691f-113">Universal Windows Platform.</span></span>

## <span data-ttu-id="d691f-114"><a name="Setup"></a>Configuración y requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d691f-114"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="d691f-115">En esta guía se asume que ha creado un back-end con una tabla.</span><span class="sxs-lookup"><span data-stu-id="d691f-115">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="d691f-116">En esta guía se asume que la tabla tiene el mismo esquema que las tablas de dichos tutoriales.</span><span class="sxs-lookup"><span data-stu-id="d691f-116">This guide assumes that the table has the same schema as the tables in those tutorials.</span></span> <span data-ttu-id="d691f-117">En esta guía también se supone que ha agregado el complemento de Apache Cordova al código.</span><span class="sxs-lookup"><span data-stu-id="d691f-117">This guide also assumes that you have added the Apache Cordova Plugin to your code.</span></span>  <span data-ttu-id="d691f-118">Si no lo ha hecho, puede agregar el complemento Apache Cordova al proyecto en la línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="d691f-118">If you have not done so, you may add the Apache Cordova plugin to your project on the command line:</span></span>

```
cordova plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="d691f-119">Para más información sobre la creación de [su primera aplicación de Apache Cordova], consulte su documentación.</span><span class="sxs-lookup"><span data-stu-id="d691f-119">For more information on creating [your first Apache Cordova app], see their documentation.</span></span>

## <span data-ttu-id="d691f-120"><a name="ionic"></a>Configuración de una aplicación de Ionic v2</span><span class="sxs-lookup"><span data-stu-id="d691f-120"><a name="ionic"></a>Setting up an Ionic v2 app</span></span>

<span data-ttu-id="d691f-121">Para configurar correctamente un proyecto de Ionic v2, primero cree una aplicación básica y agregue el complemento de Cordova:</span><span class="sxs-lookup"><span data-stu-id="d691f-121">To properly configure an Ionic v2 project, first create a basic app and add the Cordova plugin:</span></span>

```
ionic start projectName --v2
cd projectName
ionic plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="d691f-122">Agregue las siguientes líneas a `app.component.ts` para crear el objeto de cliente:</span><span class="sxs-lookup"><span data-stu-id="d691f-122">Add the following lines to `app.component.ts` to create the client object:</span></span>

```
declare var WindowsAzure: any;
var client = new WindowsAzure.MobileServiceClient("https://yoursite.azurewebsites.net");
```

<span data-ttu-id="d691f-123">Ahora puede compilar y ejecutar el proyecto en el explorador:</span><span class="sxs-lookup"><span data-stu-id="d691f-123">You can now build and run the project in the browser:</span></span>

```
ionic platform add browser
ionic run browser
```

<span data-ttu-id="d691f-124">El complemento de Cordova de Azure Mobile Apps es compatible con Ionic v1 y v2.</span><span class="sxs-lookup"><span data-stu-id="d691f-124">The Azure Mobile Apps Cordova plugin supports both Ionic v1 and v2 apps.</span></span>  <span data-ttu-id="d691f-125">Solo las aplicaciones de Ionic v2 requieren la declaración adicional para el objeto `WindowsAzure`.</span><span class="sxs-lookup"><span data-stu-id="d691f-125">Only the Ionic v2 apps require the additional declaration for the `WindowsAzure` object.</span></span>

[!INCLUDE [app-service-mobile-html-js-library.md](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="d691f-126"><a name="auth"></a>Autenticación de usuarios</span><span class="sxs-lookup"><span data-stu-id="d691f-126"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="d691f-127">Azure App Service es compatible con la autenticación y autorización de los usuarios de aplicaciones mediante diversos proveedores de identidades externos: Facebook, Google, Cuenta Microsoft y Twitter.</span><span class="sxs-lookup"><span data-stu-id="d691f-127">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="d691f-128">Puede establecer permisos en tablas para restringir el acceso a operaciones específicas solo a usuarios autenticados.</span><span class="sxs-lookup"><span data-stu-id="d691f-128">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="d691f-129">También puede usar la identidad de usuarios autenticados para implementar reglas de autorización en scripts del servidor.</span><span class="sxs-lookup"><span data-stu-id="d691f-129">You can also use the identity of authenticated users to implement authorization rules in server scripts.</span></span> <span data-ttu-id="d691f-130">Para obtener más información, consulte el tutorial [Introducción a la autenticación] .</span><span class="sxs-lookup"><span data-stu-id="d691f-130">For more information, see the [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="d691f-131">Al utilizar la autenticación en una aplicación de Apache Cordova, los siguientes complementos de Cordova deben estar disponibles:</span><span class="sxs-lookup"><span data-stu-id="d691f-131">When using authentication in an Apache Cordova app, the following Cordova plugins must be available:</span></span>

* <span data-ttu-id="d691f-132">[cordova-plugin-device]</span><span class="sxs-lookup"><span data-stu-id="d691f-132">[cordova-plugin-device]</span></span>
* <span data-ttu-id="d691f-133">[cordova-plugin-inappbrowser]</span><span class="sxs-lookup"><span data-stu-id="d691f-133">[cordova-plugin-inappbrowser]</span></span>

<span data-ttu-id="d691f-134">Se admiten dos flujos de autenticación: un flujo de servidor y un flujo de cliente.</span><span class="sxs-lookup"><span data-stu-id="d691f-134">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="d691f-135">El flujo de servidor ofrece la experiencia de autenticación más simple, ya que se basa en la interfaz de autenticación web del proveedor.</span><span class="sxs-lookup"><span data-stu-id="d691f-135">The server flow provides the simplest authentication experience, as it relies on the provider's web authentication interface.</span></span> <span data-ttu-id="d691f-136">El flujo de cliente permite una mayor integración con capacidades específicas del dispositivo, como el inicio de sesión único, ya que se basa en SDK específicos del dispositivo y específicos del proveedor.</span><span class="sxs-lookup"><span data-stu-id="d691f-136">The client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific device-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library.md](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="d691f-137"><a name="configure-external-redirect-urls"></a>Cómo configurar el servicio de Mobile Apps para URL de redireccionamiento externas</span><span class="sxs-lookup"><span data-stu-id="d691f-137"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="d691f-138">Varios tipos de aplicaciones de Apache Cordova utilizan una función de bucle invertido para controlar los flujos de la interfaz de usuario de OAuth.</span><span class="sxs-lookup"><span data-stu-id="d691f-138">Several types of Apache Cordova applications use a loopback capability to handle OAuth UI flows.</span></span>  <span data-ttu-id="d691f-139">Los flujos de interfaz de usuario de OAuth conllevan problemas, ya que el servicio de autenticación solo sabe cómo utilizar el servicio de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="d691f-139">OAuth UI flows on localhost cause problems since the authentication service only knows how to utilize your service by default.</span></span>  <span data-ttu-id="d691f-140">Ejemplos de flujos de interfaz de usuario de OAuth problemáticos:</span><span class="sxs-lookup"><span data-stu-id="d691f-140">Examples of problematic OAuth UI flows include:</span></span>

* <span data-ttu-id="d691f-141">El emulador Ripple</span><span class="sxs-lookup"><span data-stu-id="d691f-141">The Ripple emulator.</span></span>
* <span data-ttu-id="d691f-142">La característica Live Reload con Ionic</span><span class="sxs-lookup"><span data-stu-id="d691f-142">Live Reload with Ionic.</span></span>
* <span data-ttu-id="d691f-143">Ejecución del back-end móvil localmente</span><span class="sxs-lookup"><span data-stu-id="d691f-143">Running the mobile backend locally</span></span>
* <span data-ttu-id="d691f-144">Ejecución del back-end móvil en una instancia de Azure App Service diferente a la que proporciona la autenticación.</span><span class="sxs-lookup"><span data-stu-id="d691f-144">Running the mobile backend in a different Azure App Service than the one providing authentication.</span></span>

<span data-ttu-id="d691f-145">Siga estas instrucciones para agregar los ajustes locales a la configuración:</span><span class="sxs-lookup"><span data-stu-id="d691f-145">Follow these instructions to add your local settings to the configuration:</span></span>

1. <span data-ttu-id="d691f-146">Inicie sesión en el [Portal de Azure]</span><span class="sxs-lookup"><span data-stu-id="d691f-146">Log in to the [Azure portal]</span></span>
2. <span data-ttu-id="d691f-147">Seleccione **Todos los recursos** o **App Services** y haga clic en el nombre de la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="d691f-147">Select **All resources** or **App Services** then click the name of your Mobile App.</span></span>
3. <span data-ttu-id="d691f-148">Haga clic en **Herramientas**</span><span class="sxs-lookup"><span data-stu-id="d691f-148">Click **Tools**</span></span>
4. <span data-ttu-id="d691f-149">Haga clic en la opción **Explorador de recursos** del menú OBSERVAR y, después, en **Ir**.</span><span class="sxs-lookup"><span data-stu-id="d691f-149">Click **Resource explorer** in the OBSERVE menu, then click **Go**.</span></span>  <span data-ttu-id="d691f-150">Se abrirá una nueva ventana o pestaña.</span><span class="sxs-lookup"><span data-stu-id="d691f-150">A new window or tab opens.</span></span>
5. <span data-ttu-id="d691f-151">Expanda los nodos **config** y **authsettings** de su sitio en el panel de navegación izquierdo.</span><span class="sxs-lookup"><span data-stu-id="d691f-151">Expand the **config**, **authsettings** nodes for your site in the left-hand navigation.</span></span>
6. <span data-ttu-id="d691f-152">Haga clic en **Editar**</span><span class="sxs-lookup"><span data-stu-id="d691f-152">Click **Edit**</span></span>
7. <span data-ttu-id="d691f-153">Busque el elemento "allowedExternalRedirectUrls".</span><span class="sxs-lookup"><span data-stu-id="d691f-153">Look for the "allowedExternalRedirectUrls" element.</span></span>  <span data-ttu-id="d691f-154">Se puede establecer en Null o una matriz de valores.</span><span class="sxs-lookup"><span data-stu-id="d691f-154">It may be set to null or an array of values.</span></span>  <span data-ttu-id="d691f-155">Cambie el valor al siguiente:</span><span class="sxs-lookup"><span data-stu-id="d691f-155">Change the value to the following value:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="d691f-156">Sustituya las URL por las de su servicio.</span><span class="sxs-lookup"><span data-stu-id="d691f-156">Replace the URLs with the URLs of your service.</span></span>  <span data-ttu-id="d691f-157">Por ejemplo: "http://localhost:3000" (para el servicio de muestra Node.js) o "http://localhost:4400" (para el servicio de Ripple).</span><span class="sxs-lookup"><span data-stu-id="d691f-157">Examples include "http://localhost:3000" (for the Node.js sample service), or "http://localhost:4400" (for the Ripple service).</span></span>  <span data-ttu-id="d691f-158">Sin embargo, estas URL no son más que ejemplos. Es decir, su situación puede ser distinta, incluso si debe configurar los servicios mencionados en los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="d691f-158">However, these URLs are examples - your situation, including for the services mentioned in the examples, may be different.</span></span>
8. <span data-ttu-id="d691f-159">Haga clic en el botón **Lectura/escritura** situado en la esquina superior derecha de la pantalla.</span><span class="sxs-lookup"><span data-stu-id="d691f-159">Click the **Read/Write** button in the top-right corner of the screen.</span></span>
9. <span data-ttu-id="d691f-160">Haga clic en el botón verde **PUT** .</span><span class="sxs-lookup"><span data-stu-id="d691f-160">Click the green **PUT** button.</span></span>

<span data-ttu-id="d691f-161">La configuración se guardará en este momento.</span><span class="sxs-lookup"><span data-stu-id="d691f-161">The settings are saved at this point.</span></span>  <span data-ttu-id="d691f-162">No cierre la ventana del explorador hasta que la configuración haya terminado de guardarse.</span><span class="sxs-lookup"><span data-stu-id="d691f-162">Do not close the browser window until the settings have finished saving.</span></span>
<span data-ttu-id="d691f-163">Agregue también estas URL de bucle invertido a la configuración de CORS:</span><span class="sxs-lookup"><span data-stu-id="d691f-163">Also add these loopback URLs to the CORS settings for your App Service:</span></span>

1. <span data-ttu-id="d691f-164">Inicie sesión en el [Portal de Azure]</span><span class="sxs-lookup"><span data-stu-id="d691f-164">Log in to the [Azure portal]</span></span>
2. <span data-ttu-id="d691f-165">Seleccione **Todos los recursos** o **App Services** y haga clic en el nombre de la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="d691f-165">Select **All resources** or **App Services** then click the name of your Mobile App.</span></span>
3. <span data-ttu-id="d691f-166">Se abrirá automáticamente la hoja Configuración.</span><span class="sxs-lookup"><span data-stu-id="d691f-166">The Settings blade opens automatically.</span></span>  <span data-ttu-id="d691f-167">En caso contrario, haga clic en **Toda la configuración**.</span><span class="sxs-lookup"><span data-stu-id="d691f-167">If it doesn't, click **All Settings**.</span></span>
4. <span data-ttu-id="d691f-168">Haga clic en la opción **CORS** del menú API.</span><span class="sxs-lookup"><span data-stu-id="d691f-168">Click **CORS** under the API menu.</span></span>
5. <span data-ttu-id="d691f-169">Escriba la dirección URL que quiera agregar en el cuadro proporcionado y presione Intro.</span><span class="sxs-lookup"><span data-stu-id="d691f-169">Enter the URL that you wish to add in the box provided and press Enter.</span></span>
6. <span data-ttu-id="d691f-170">Escriba las direcciones URL adicionales que necesite.</span><span class="sxs-lookup"><span data-stu-id="d691f-170">Enter additional URLs as needed.</span></span>
7. <span data-ttu-id="d691f-171">Haga clic en **Guardar** para guardar la configuración.</span><span class="sxs-lookup"><span data-stu-id="d691f-171">Click **Save** to save the settings.</span></span>

<span data-ttu-id="d691f-172">Los nuevos ajustes tardarán aproximadamente entre 10 y 15 segundos en surtir efecto.</span><span class="sxs-lookup"><span data-stu-id="d691f-172">It takes approximately 10-15 seconds for the new settings to take effect.</span></span>

## <span data-ttu-id="d691f-173"><a name="register-for-push"></a>Registrar notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="d691f-173"><a name="register-for-push"></a>How to: Register for push notifications</span></span>
<span data-ttu-id="d691f-174">Instale [phonegap-plugin-push] para administrar las notificaciones push.</span><span class="sxs-lookup"><span data-stu-id="d691f-174">Install the [phonegap-plugin-push] to handle push notifications.</span></span>  <span data-ttu-id="d691f-175">Este complemento se puede agregar fácilmente mediante el comando `cordova plugin add` en la línea de comandos o por medio del instalador de complementos Git dentro de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d691f-175">This plugin can be easily added using the `cordova plugin add` command on the command line, or via the Git plugin installer within Visual Studio.</span></span>  <span data-ttu-id="d691f-176">El siguiente código de la aplicación de Apache Cordova registrará el dispositivo para notificaciones push:</span><span class="sxs-lookup"><span data-stu-id="d691f-176">The following code in your Apache Cordova app registers your device for push notifications:</span></span>

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
    // For cross-platform, you can use the device plugin to determine the device
    // Best is to use device.platform
    var name = 'gcm'; // For android - default
    if (device.platform.toLowerCase() === 'ios')
        name = 'apns';
    if (device.platform.toLowerCase().substring(0, 3) === 'win')
        name = 'wns';
    client.push.register(name, registrationId);
});

pushHandler.on('notification', function (data) {
    // data is an object and is whatever is sent by the PNS - check the format
    // for your particular PNS
});

pushHandler.on('error', function (error) {
    // Handle errors
});
```

<span data-ttu-id="d691f-177">Use el SDK de Centros de notificaciones para enviar notificaciones push desde el servidor.</span><span class="sxs-lookup"><span data-stu-id="d691f-177">Use the Notification Hubs SDK to send push notifications from the server.</span></span>  <span data-ttu-id="d691f-178">No envíe nunca notificaciones push directamente desde la aplicación,</span><span class="sxs-lookup"><span data-stu-id="d691f-178">Never send push notifications directly from clients.</span></span> <span data-ttu-id="d691f-179">ya que podría usarse para desencadenar un ataque de denegación de servicio en Notification Hubs o el PNS.</span><span class="sxs-lookup"><span data-stu-id="d691f-179">Doing so could be used to trigger a denial of service attack against Notification Hubs or the PNS.</span></span>  <span data-ttu-id="d691f-180">El PNS puede prohibir el tráfico como resultado de estos ataques.</span><span class="sxs-lookup"><span data-stu-id="d691f-180">The PNS could ban your traffic as a result of such attacks.</span></span>

## <a name="more-information"></a><span data-ttu-id="d691f-181">Más información</span><span class="sxs-lookup"><span data-stu-id="d691f-181">More information</span></span>

<span data-ttu-id="d691f-182">Puede encontrar información detallada sobre las API en nuestra [documentación de la API](http://azure.github.io/azure-mobile-apps-js-client/).</span><span class="sxs-lookup"><span data-stu-id="d691f-182">You can find detailed API details in our [API documentation](http://azure.github.io/azure-mobile-apps-js-client/).</span></span>

<!-- URLs. -->
<span data-ttu-id="d691f-183">[Portal de Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="d691f-183">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="d691f-184">[Creación de una aplicación de Apache Cordova]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="d691f-184">[Azure Mobile Apps Quick Start]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="d691f-185">[Introducción a la autenticación]: app-service-mobile-cordova-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="d691f-185">[Get started with authentication]: app-service-mobile-cordova-get-started-users.md</span></span>
[Add authentication to your app]: app-service-mobile-cordova-get-started-users.md

<span data-ttu-id="d691f-186">[complemento de Apache Cordova para Aplicaciones móviles de Azure]: https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-apps</span><span class="sxs-lookup"><span data-stu-id="d691f-186">[Apache Cordova Plugin for Azure Mobile Apps]: https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-apps</span></span>
<span data-ttu-id="d691f-187">[su primera aplicación de Apache Cordova]: http://cordova.apache.org/#getstarted</span><span class="sxs-lookup"><span data-stu-id="d691f-187">[your first Apache Cordova app]: http://cordova.apache.org/#getstarted</span></span>
[phonegap-facebook-plugin]: https://github.com/wizcorp/phonegap-facebook-plugin
<span data-ttu-id="d691f-188">[phonegap-plugin-push]: https://www.npmjs.com/package/phonegap-plugin-push</span><span class="sxs-lookup"><span data-stu-id="d691f-188">[phonegap-plugin-push]: https://www.npmjs.com/package/phonegap-plugin-push</span></span>
<span data-ttu-id="d691f-189">[cordova-plugin-device]: https://www.npmjs.com/package/cordova-plugin-device</span><span class="sxs-lookup"><span data-stu-id="d691f-189">[cordova-plugin-device]: https://www.npmjs.com/package/cordova-plugin-device</span></span>
<span data-ttu-id="d691f-190">[cordova-plugin-inappbrowser]: https://www.npmjs.com/package/cordova-plugin-inappbrowser</span><span class="sxs-lookup"><span data-stu-id="d691f-190">[cordova-plugin-inappbrowser]: https://www.npmjs.com/package/cordova-plugin-inappbrowser</span></span>
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
