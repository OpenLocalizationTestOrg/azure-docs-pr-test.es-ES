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
# <a name="how-toouse-hello-javascript-client-library-for-azure-mobile-apps"></a>¿Cómo tooUse Hola biblioteca de cliente de JavaScript para aplicaciones móviles de Azure
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

Esta guía le enseña con hello más reciente de escenarios comunes de tooperform [JavaScript SDK para aplicaciones móviles de Azure]. Si estás nuevas aplicaciones de Mobile tooAzure, complete primero [inicio rápido de Azure Mobile Apps] toocreate un back-end y cree una tabla. En esta guía, se centran en el uso de back-end de hello móviles en aplicaciones Web HTML/JavaScript.

## <a name="supported-platforms"></a>Plataformas compatibles
Se limitar actual de toohello de compatibilidad con explorador y el apellido de versiones de hello principales exploradores: Google Chrome, Microsoft Edge, Microsoft Internet Explorer y Mozilla Firefox.  Esperamos que Hola SDK toofunction con cualquier explorador moderno relativamente.

paquete de Hola se distribuye como un módulo de JavaScript Universal, por lo que es compatible con las variables globales, AMD, y da formato a CommonJS.

## <a name="Setup"></a>Configuración y requisitos previos
En esta guía se asume que ha creado un back-end con una tabla. Esta guía se da por supuesto que tiene de esa tabla Hola Hola mismo esquema como tablas de hello en los tutoriales.

Instalar Hola SDK de JavaScript de aplicaciones móviles de Azure puede hacerse a través de hello `npm` comando:

```
npm install azure-mobile-apps-client --save
```

biblioteca de Hello también puede utilizarse como un módulo ES2015, dentro de entornos de CommonJS como Browserify y Webpack y como una biblioteca AMD.  Por ejemplo:

```
# For ECMAScript 5.1 CommonJS
var WindowsAzure = require('azure-mobile-apps-client');
# For ES2015 modules
import * as WindowsAzure from 'azure-mobile-apps-client';
```

También puede utilizar una versión previamente compilada de hello SDK descargando directamente desde la red CDN:

```html
<script src="https://zumo.blob.core.windows.net/sdk/azure-mobile-apps-client.min.js"></script>
```

[!INCLUDE [app-service-mobile-html-js-library](../../includes/app-service-mobile-html-js-library.md)]

## <a name="auth"></a>Autenticación de usuarios
Azure App Service es compatible con la autenticación y autorización de los usuarios de aplicaciones mediante diversos proveedores de identidades externos: Facebook, Google, Cuenta Microsoft y Twitter. Puede establecer permisos de acceso de toorestrict de tablas para operaciones específicas tooonly autenticado a los usuarios. También puede utilizar la identidad de Hola de reglas de autorización de los usuarios autenticados tooimplement en scripts de servidor. Para obtener más información, vea hello [empezar a trabajar con autenticación] tutorial.

Se admiten dos flujos de autenticación: un flujo de servidor y un flujo de cliente.  flujo de servidor Hello proporciona experiencia de autenticación más sencilla de hello, tal y como se basa en la interfaz de autenticación del proveedor de hello web. Hello flujo del cliente permite una integración más profunda con capacidades específicas del dispositivo como inicio de sesión único como se basa en SDK específicos del proveedor.

[!INCLUDE [app-service-mobile-html-js-auth-library](../../includes/app-service-mobile-html-js-auth-library.md)]

### <a name="configure-external-redirect-urls"></a>Cómo configurar el servicio de Mobile Apps para URL de redireccionamiento externas
Varios tipos de aplicaciones de JavaScript usan un toohandle de capacidad de bucle invertido que OAuth UI flujos.  Estas son algunas de ellas:

* Ejecución del servicio de manera local
* Uso de recarga de Live con hello marco de trabajo Ionic
* Redirigir tooApp servicio para la autenticación.

Ejecuta de forma local puede causar problemas ya que, de forma predeterminada, la autenticación es solo el servicio de aplicaciones configurado tooallow el acceso desde su aplicación móvil de back-end. Usar hello siguiendo los pasos toochange Hola autenticación de tooenable de configuración de servicio de aplicaciones cuando se ejecuta el servidor de hello localmente:

1. Inicie sesión en toohello [portal de Azure]
2. Navegue back-end de tooyour aplicación móvil.
3. Seleccione **Explorador de recursos** en hello **herramientas de desarrollo** menú.
4. Haga clic en **vaya** Explorador de recursos de hello tooopen para su aplicación móvil de back-end en una nueva pestaña o ventana.
5. Expanda hello **config** > **authsettings** nodo de la aplicación.
6. Haga clic en hello **editar** botón tooenable edición de recursos de Hola.
7. Buscar hello **allowedExternalRedirectUrls** elemento, que debe ser null. Agregue las direcciones URL en una matriz:

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    Reemplazar las direcciones URL de hello en la matriz de hello con hello las direcciones URL del servicio, que en este ejemplo es `http://localhost:3000` de servicio de ejemplo de Hola local Node.js. También puede usar `http://localhost:4400` para servicio de Ripple de Hola o alguna otra dirección URL, según cómo esté configurada la aplicación.
8. En la parte superior de Hola de página de hello, haga clic en **lectura/escritura**, a continuación, haga clic en **colocar** toosave las actualizaciones.

También necesita tooadd Hola configuración de lista blanca de direcciones CORS toohello de direcciones URL de bucle invertido mismo:

1. Desplácese atrás toohello [portal de Azure].
2. Navegue back-end de tooyour aplicación móvil.
3. Haga clic en **CORS** en hello **API** menú.
4. Escriba cada dirección URL en hello vacía **permite orígenes** cuadro de texto.  Se crea un nuevo cuadro de texto.
5. Haga clic en **GUARDAR**

Después de que se actualice el back-end de hello, será capaz de toouse Hola nuevo bucle invertido las direcciones URL en la aplicación.

<!-- URLs. -->
[inicio rápido de Azure Mobile Apps]: app-service-mobile-cordova-get-started.md
[empezar a trabajar con autenticación]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[portal de Azure]: https://portal.azure.com/
[JavaScript SDK para aplicaciones móviles de Azure]: https://www.npmjs.com/package/azure-mobile-apps-client
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
