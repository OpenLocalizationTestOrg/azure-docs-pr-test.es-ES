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
# <a name="how-toouse-apache-cordova-client-library-for-azure-mobile-apps"></a>La biblioteca de cliente de Apache Cordova toouse para aplicaciones móviles de Azure
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

Esta guía le enseña con hello más reciente de escenarios comunes de tooperform [Apache Cordova complemento para las aplicaciones de Azure Mobile]. Si estás nuevas aplicaciones de Mobile tooAzure, complete primero [inicio rápido de Azure Mobile Apps] toocreate un back-end, cree una tabla y descargar un proyecto de Apache Cordova pregenerado. Esta guía se centra en Hola de cliente Apache Cordova complemento.

## <a name="supported-platforms"></a>Plataformas compatibles
Este SDK es compatible con la versión 6.0.0 y posterior de Apache Cordova en dispositivos iOS, Android y Windows.  compatibilidad con la plataforma de Hello es como sigue:

* Niveles de API de Android del 19 al 24 (de KitKat a Nougat)
* Versiones 8.0 y posteriores de iOS.
* Windows Phone 8.1
* Plataforma universal de Windows

## <a name="Setup"></a>Configuración y requisitos previos
En esta guía se asume que ha creado un back-end con una tabla. Esta guía se da por supuesto que tiene de esa tabla Hola Hola mismo esquema como tablas de hello en los tutoriales. Esta guía también se da por supuesto que ha agregado código de hello Apache Cordova complemento tooyour.  Si aún no lo ha hecho, puede agregar el complemento tooyour proyecto de hello Apache Cordova en línea de comandos de hello:

```
cordova plugin add cordova-plugin-ms-azure-mobile-apps
```

Para más información sobre la creación de [su primera aplicación de Apache Cordova], consulte su documentación.

## <a name="ionic"></a>Configuración de una aplicación de Ionic v2

tooproperly configurar un proyecto de Ionic v2, primero cree una aplicación básica y agregar complemento de Cordova hello:

```
ionic start projectName --v2
cd projectName
ionic plugin add cordova-plugin-ms-azure-mobile-apps
```

Agregar Hola después líneas demasiado`app.component.ts` objeto de cliente hello toocreate:

```
declare var WindowsAzure: any;
var client = new WindowsAzure.MobileServiceClient("https://yoursite.azurewebsites.net");
```

Ahora puede compilar y ejecutar el proyecto de hello en el Explorador de hello:

```
ionic platform add browser
ionic run browser
```

complemento de Cordova de aplicaciones móviles de Azure de Hello es compatible con ambas aplicaciones Ionic v1 y v2.  Solo aplicaciones Hola v2 Ionic requieren la declaración adicional para hello `WindowsAzure` objeto.

[!INCLUDE [app-service-mobile-html-js-library.md](../../includes/app-service-mobile-html-js-library.md)]

## <a name="auth"></a>Autenticación de usuarios
Azure App Service es compatible con la autenticación y autorización de los usuarios de aplicaciones mediante diversos proveedores de identidades externos: Facebook, Google, Cuenta Microsoft y Twitter. Puede establecer permisos de acceso de toorestrict de tablas para operaciones específicas tooonly autenticado a los usuarios. También puede utilizar la identidad de Hola de reglas de autorización de los usuarios autenticados tooimplement en scripts de servidor. Para obtener más información, vea hello [empezar a trabajar con autenticación] tutorial.

Al utilizar la autenticación en una aplicación de Apache Cordova, Hola siguiendo los complementos de Cordova debe estar disponible:

* [cordova-plugin-device]
* [cordova-plugin-inappbrowser]

Se admiten dos flujos de autenticación: un flujo de servidor y un flujo de cliente.  flujo de servidor Hello proporciona experiencia de autenticación más sencilla de hello, tal y como se basa en la interfaz de autenticación del proveedor de hello web. Hello flujo del cliente permite una integración más profunda con capacidades específicas del dispositivo como inicio de sesión único como se basa en el SDK de específica del proveedor específico del dispositivo.

[!INCLUDE [app-service-mobile-html-js-auth-library.md](../../includes/app-service-mobile-html-js-auth-library.md)]

### <a name="configure-external-redirect-urls"></a>Cómo configurar el servicio de Mobile Apps para URL de redireccionamiento externas
Varios tipos de aplicaciones de Apache Cordova usan un toohandle de capacidad de bucle invertido que OAuth UI flujos.  Flujos de OAuth UI en localhost causar problemas ya que solo conoce el servicio de autenticación de hello cómo tooutilize su servicio de forma predeterminada.  Ejemplos de flujos de interfaz de usuario de OAuth problemáticos:

* emulador Hola.
* La característica Live Reload con Ionic
* Ejecución Hola móviles back-end localmente
* Ejecuta back-end de hello móvil en un servicio de aplicación de Azure diferente que la autenticación de proporcionando un saludo.

Siga estas instrucciones tooadd la configuración de toohello de configuración local:

1. Inicie sesión en toohello [portal de Azure]
2. Seleccione **todos los recursos** o **servicios de aplicaciones** , a continuación, haga clic en nombre de saludo de la aplicación móvil.
3. Haga clic en **Herramientas**
4. Haga clic en **Explorador de recursos** en el menú OBSERVE hello, a continuación, haga clic en **vaya**.  Se abrirá una nueva ventana o pestaña.
5. Expanda hello **config**, **authsettings** nodos para su sitio en el panel de navegación izquierdo Hola.
6. Haga clic en **Editar**
7. Busque el elemento de "allowedExternalRedirectUrls" Hola.  Se puede establecer toonull o una matriz de valores.  Cambiar Hola valor toohello siguiente valor:

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    Reemplace hello las direcciones URL con hello las direcciones URL de su servicio.  Algunos ejemplos son "http://localhost:3000" (para el servicio de ejemplo de Node.js Hola) o "http://localhost:4400" (para el servicio de Ripple Hola).  Sin embargo, estas direcciones URL son ejemplos: su situación, incluidos los servicios de hello mencionados en los ejemplos de hello, pueden ser diferentes.
8. Haga clic en hello **lectura/escritura** botón en la esquina superior derecha de Hola de pantalla de bienvenida.
9. Haga clic en hello verde **colocar** botón.

configuración de Hola se guarda en este momento.  No cierre la ventana del explorador Hola hasta que finaliza la configuración de hello guardar.
Agregar esta configuración de CORS de toohello de bucle invertido las direcciones URL para el servicio de aplicaciones:

1. Inicie sesión en toohello [portal de Azure]
2. Seleccione **todos los recursos** o **servicios de aplicaciones** , a continuación, haga clic en nombre de saludo de la aplicación móvil.
3. hoja de configuración de Hola se abre automáticamente.  En caso contrario, haga clic en **Toda la configuración**.
4. Haga clic en **CORS** en el menú de hello API.
5. Escriba la dirección URL de Hola que desee tooadd en cuadro Hola correspondiente y presione ENTRAR.
6. Escriba las direcciones URL adicionales que necesite.
7. Haga clic en **guardar** configuración de toosave Hola.

Tarda aproximadamente 10-15 segundos para el efecto de hello nueva configuración tootake.

## <a name="register-for-push"></a>Registrar notificaciones de inserción
Instalar hello [phonegap-plugin-inserción] toohandle notificaciones de inserción.  Este complemento se puede agregar fácilmente mediante la `cordova plugin add` comando en la línea de comandos de hello, o mediante el instalador de complemento de hello Git en Visual Studio.  El siguiente código de la aplicación de Apache Cordova registrará el dispositivo para notificaciones push:

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

Usar notificaciones de inserción de toosend Hola SDK de bases de datos centrales de notificación del servidor de Hola.  No envíe nunca notificaciones push directamente desde la aplicación, Al hacerlo así podría tootrigger usado un ataque de denegación de servicio en los centros de notificaciones u Hola PNS.  Hola PNS podría prohibir el tráfico como resultado de estos ataques.

## <a name="more-information"></a>Más información

Puede encontrar información detallada sobre las API en nuestra [documentación de la API](http://azure.github.io/azure-mobile-apps-js-client/).

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
