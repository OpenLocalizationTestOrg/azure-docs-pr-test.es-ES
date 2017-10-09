---
title: "aaaUpgrade de servicios móviles tooAzure servicio de aplicaciones - Node.js"
description: "Obtenga información acerca de cómo tooeasily actualizar su tooan de aplicación de servicios móviles aplicación móvil de servicio de aplicación"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: yochayk
editor: 
ms.assetid: c58f6df0-5aad-40a3-bddc-319c378218e3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 722cda244d4f633247827f58ea6f1397137ea600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-existing-nodejs-azure-mobile-service-tooapp-service"></a>Actualizar su tooApp existente de servicios móviles de Azure de Node.js servicio
Servicio de aplicaciones móviles son una nueva manera toobuild móviles las aplicaciones con Microsoft Azure. más información, consulte toolearn [¿qué aplicaciones móviles?].

Este tema se describe cómo una aplicación existente de back-end de Node.js de servicios móviles de Azure tooa tooupgrade aplicaciones móviles de nueva aplicación de servicio. Cuando realiza esta actualización, la aplicación de servicios móviles existente puede seguir realizando toooperate.  Si necesita una aplicación de back-end de Node.js tooupgrade, consulte demasiado[actualizar los servicios móviles de .NET](app-service-mobile-net-upgrading-from-mobile-services.md).

Una vez un back-end móvil actualizado tooAzure servicio de aplicaciones, tiene tooall de acceso a características del servicio de aplicación y facturan según demasiado[servicio de aplicaciones precios], no los servicios móviles de precios.

## <a name="migrate-vs-upgrade"></a>Migración frente a actualización
[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

> [!TIP]
> Se recomienda [realizar una migración](app-service-mobile-migrating-from-mobile-services.md) antes de pasar por una actualización. De esta manera, puede colocar las dos versiones de la aplicación Hola mismo Plan de servicio de aplicación y no acumulando costo adicional alguno.
>
>

### <a name="improvements-in-mobile-apps-nodejs-server-sdk"></a>Mejoras en el SDK de servidor para Node.js de Aplicaciones móviles
Actualizar toohello nueva [SDK de aplicaciones móviles](https://www.npmjs.com/package/azure-mobile-apps) proporciona una gran cantidad de mejoras, incluido:

* En función de hello [Express framework](http://expressjs.com/en/index.html), hello nuevo SDK del nodo es ligero y diseñado tookeep seguridad con nuevas versiones de nodo tal y como saldrá. Puede personalizar el comportamiento de la aplicación hello con middleware de Express.
* Mejoras de rendimiento significativas en comparación con toohello SDK de servicios móviles.
* Ahora puede hospedar un sitio Web junto con el back-end móvil; del mismo modo, es fácil tooadd Hola SDK de Azure Mobile tooany existente express.v4 aplicación.
* Creado para el desarrollo multiplataforma y local, puede desarrollado Hola SDK de aplicaciones móviles y ejecutar localmente en las plataformas Windows, Linux y OSX. Ahora es fácil toouse técnicas de desarrollo de nodo comunes como ejecución [Mocha](https://mochajs.org/) prueba toodeployment anterior.

## <a name="overview"></a>Información general básica de actualización
tooaid al actualizar un backend de Node.js, servicio de aplicaciones de Azure ha proporcionado un paquete de compatibilidad.  Después de la actualización, tendrá un sitio de niew que puede ser implementado tooa nuevo sitio de servicio de aplicaciones.

SDK de cliente de servicios móviles de Hello es **no** compatibles con el servidor de aplicaciones móviles nueva Hola SDK. En orden tooprovide la continuidad del servicio para la aplicación, no debería publicar sitio tooa de cambios actualmente actúa a clientes publicados. En su lugar, debe crear una aplicación móvil que actúe como duplicado. Puede colocar esta aplicación Hola mismo servicio de aplicaciones previsto tooavoid incurrir en costes financieros adicionales.

A continuación, tendrá dos versiones de la aplicación hello: uno que permanece igual Hola y actúa las aplicaciones publicadas en hello naturaleza y la otra que, a continuación, puede actualizar y destino con un nuevo cliente de la versión. Puede mover y probar el código a su ritmo, pero debe asegurarse de que las correcciones de errores de que asegúrese obtener tooboth aplicada. Cuando se sienta que un número deseado de las aplicaciones de cliente en la naturaleza actualizaron versión más reciente de toohello, puede eliminar la aplicación migrada de hello original si así lo desea. Lo no incurre en ningún cualquier monetarios costos adicionales, si hospeda en el mismo servicio de aplicaciones planear como su aplicación móvil de Hola.

descripción completa del Hola de proceso de actualización de hello es como sigue:

1. Descargue el servicio móvil de Azure existente (migrado).
2. Convertir Hola proyecto tooan aplicación móvil de Azure mediante el paquete de compatibilidad de Hola.
3. Corrija cualquier diferencia (como la configuración de autenticación).
4. Implementar el convertido tooa de proyecto de aplicación móvil de Azure nuevo servicio en la aplicación.
5. Lanzará una nueva versión de la aplicación cliente que use Hola nueva aplicación móvil.
6. (Opcional) Eliminar la aplicación de servicio móvil migrada original

La eliminación puede tener lugar cuando no vea tráfico alguno en el servicio móvil migrado original.

## <a name="install-npm-package"></a>Instalar requisitos previos de Hola
Debe instalar [Node] en el equipo local.  También debe instalar el paquete de compatibilidad de Hola.  Después de instala el nodo, puede ejecutar Hola siguiente comando desde un cmd nueva o el símbolo del sistema de PowerShell:

```npm i -g azure-mobile-apps-compatibility```

## <a name="obtain-ams-scripts"></a> Obtención de los scripts de Servicios móviles de Azure
* Inicie sesión en toohello [Portal de Azure].
* Mediante **Todos los recursos** o **App Services**, busque el sitio de Mobile Services.
* En el sitio de hello, haga clic en **herramientas** -> **Kudu** -> **vaya** sitio Kudu de tooopen Hola.
* Haga clic en **consola de depuración** -> **PowerShell** consola de depuración tooopen Hola.
* Navegue demasiado`site/wwwroot/App_Data/config` haciendo clic en cada directorio a su vez
* Haga clic en el icono de descarga hello toohello siguiente `scripts` directory.

Esto descargará las secuencias de comandos de hello en formato ZIP.  Crear un nuevo directorio en el equipo local y descomprima hello `scripts.ZIP` archivo dentro del directorio de Hola.  Se crea un directorio `scripts` .

## <a name="scaffold-app"></a>Aplicar la técnica scaffolding Hola aplicaciones móviles de Azure back-end
Ejecute hello siguiente comando de directorio de Hola que contiene el directorio de scripts de hello:

```scaffold-mobile-app scripts out```

Esto creará un back-end con scaffolding de aplicaciones móviles de Azure en hello `out` directory.  Aunque no es necesario, es una Hola de toocheck buena idea `out` directorio en un repositorio de código fuente de su elección.

## <a name="deploy-ama-app"></a> Implementación del back-end de Aplicaciones móviles de Azure
Durante la implementación, se necesita toodo Hola siguiente:

1. Crear una nueva aplicación móvil en hello [Portal de Azure].
2. Ejecute hello `createViews.sql` script en la base de datos conectada.
3. Base de datos de Hola de vínculo está vinculado tooyour servicio móvil tooyour nuevo servicio en la aplicación.
4. Vincular otra toohello de recursos (como centros de notificaciones) nuevo servicio en la aplicación.
5. Implementar el nuevo sitio de hello genera código tooyour.

### <a name="create-a-new-mobile-app"></a>Creación de una aplicación móvil
1. Inicie sesión en hello [Portal de Azure].
2. Haga clic en **+NUEVO** > **Web y móvil** > **Aplicación móvil** y, después, proporcione un nombre para el back-end de la aplicación móvil.
3. Para hello **grupo de recursos**, seleccione un grupo de recursos existente o crear uno nuevo (usando Hola el mismo nombre que la aplicación).

    Puede seleccionar un plan de Servicio de aplicaciones ya existente o crear uno nuevo. Para obtener más información sobre los planes de servicios de aplicaciones y cómo toocreate un nuevo plan de precios de diferentes capas y en la ubicación deseada, consulte [información general detallada de planes de servicio de aplicaciones de Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
4. Para hello **plan de servicio de aplicaciones**, plan de hello predeterminado (Hola [nivel estándar](https://azure.microsoft.com/pricing/details/app-service/)) está seleccionado. También puede seleccionar otro plan o [crear uno](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan). la configuración del plan del servicio de aplicación Hello determina hello [ubicación, características, costo y recursos de proceso](https://azure.microsoft.com/pricing/details/app-service/) asociados a su aplicación.

    Después de decidir plan hello, haga clic en **crear**. Esto crea la aplicación móvil de hello back-end.

### <a name="run-createviewssql"></a>Ejecución de CreateViews.SQL
aplicación con scaffolding de Hello contiene un archivo denominado `createViews.sql`.  Este script debe ejecutarse con la base de datos de destino.  cadena de conexión de Hello para la base de datos de destino de hello puede obtenerse de su servicio móvil migrado desde hello **configuración** hoja bajo **las cadenas de conexión**.  Se llama `MS_TableConnectionString`.

Puede ejecutar este script desde SQL Server Management Studio o Visual Studio.

### <a name="link-hello-database-tooyour-app-service"></a>Hola de vínculo tooyour servicio de aplicaciones de base de datos
Hola de vínculo existente tooyour servicio de aplicaciones de base de datos:

* Hola [Portal de Azure], abra el servicio de aplicaciones.
* Seleccione **Toda la configuración** -> **Conexiones de datos**.
* Haga clic en **+ Agregar**.
* En la lista desplegable de hello, seleccione **base de datos SQL**
* En **SQL Database**, seleccione la base de datos existente y haga clic en **Seleccionar**.
* En **cadena de conexión**, escriba Hola username y password para base de datos de hello, a continuación, haga clic en **Aceptar**.
* Hola **agregar conexiones de datos** hoja, haga clic en **Aceptar**.

contraseña y nombre de usuario de hello pueden encontrarse viendo Hola cadena de conexión de base de datos de destino de hello en su servicio móvil migrados.

### <a name="set-up-authentication"></a>Configuración de la autenticación
Aplicaciones móviles de Azure permite la autenticación de Azure Active Directory, Facebook, Google, Microsoft y Twitter de tooconfigure dentro de servicio de Hola.  Autenticación personalizada deberá toobe desarrollada por separado.  Hacer referencia a saludos [conceptos de autenticación] documentación y [inicio rápido de autenticación] documentación para obtener más información.  

## <a name="updating-clients"></a>Actualización de los clientes móviles
Cuando tenga un back-end de aplicación móvil operativo, podrá trabajar en una nueva versión de la aplicación cliente que lo usa. Aplicaciones móviles también incluye una nueva versión del SDK de cliente de Hola y similar toohello actualización del servidor anterior, deberá tooremove todas las referencias de SDK de servicios móviles de toohello antes de instalar las versiones de aplicaciones móviles.

Uno de los cambios principales de hello entre las versiones de hello es que los constructores de hello ya no necesitan una clave de aplicación.
Ahora basta con pasa en dirección URL de saludo de la aplicación móvil. Por ejemplo, en los clientes de .NET de hello, Hola `MobileServiceClient` constructor está ahora:

        public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://contoso.azurewebsites.net" // URL of hello Mobile App
        );

Puede leer acerca de cómo instalar Hola nuevos SDK y el uso de la nueva estructura de Hola a través de vínculos de hello siguientes:

* [Versión de Android 2.2 o posterior](app-service-mobile-android-how-to-use-client-library.md)
* [iOS versión 3.0.0 o posterior](app-service-mobile-ios-how-to-use-client-library.md)
* [.NET (Windows/Xamarin) versión 2.0.0 o posterior](app-service-mobile-dotnet-how-to-use-client-library.md)
* [Apache Cordova versión 2.0 o posterior](app-service-mobile-cordova-how-to-use-client-library.md)

Si la aplicación realiza el uso de notificaciones de inserción, tome nota de hello instrucciones de registro específico para cada plataforma, tal y como han habido algunos cambios también.

Cuando haya Hola nueva versión de cliente listo, pruébelo en su proyecto de servidor actualizado. Después de comprobar que funciona, puede liberar una nueva versión de la aplicación toocustomers. Finalmente, una vez que los clientes han tenido una oportunidad tooreceive estas actualizaciones, puede eliminar la versión de servicios móviles de saludo de la aplicación. En este punto, ha actualizado completamente tooan aplicación móvil de servicio de aplicación con el servidor de aplicaciones móviles más reciente de hello SDK.

<!-- URLs. -->

[Portal de Azure]: https://portal.azure.com/
[Azure classic portal]: https://manage.windowsazure.com/
[¿qué aplicaciones móviles?]: app-service-mobile-value-prop.md
[I already use web sites and mobile services – how does App Service help me?]: /en-us/documentation/articles/app-service-mobile-value-prop-migration-from-mobile-services
[Mobile App Server SDK]: https://www.npmjs.com/package/azure-mobile-apps
[Create a Mobile App]: app-service-mobile-xamarin-ios-get-started.md
[Add push notifications tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-push.md
[Add authentication tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-users.md
[Azure Scheduler]: /en-us/documentation/services/scheduler/
[Web Job]: ../app-service-web/websites-webjobs-resources.md
[How toouse hello .NET server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Migrate from Mobile Services tooan App Service Mobile App]: app-service-mobile-migrating-from-mobile-services.md
[Migrate your existing Mobile Service tooApp Service]: app-service-mobile-migrating-from-mobile-services.md
[servicio de aplicaciones precios]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[.NET server SDK overview]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[conceptos de autenticación]: ../app-service/app-service-authentication-overview.md
[inicio rápido de autenticación]: app-service-mobile-auth.md

[Portal de Azure]: https://portal.azure.com/
[OData]: http://www.odata.org
[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[basicapp sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[todo sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[samples directory on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Node.js Tools 1.1 for Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node.js package]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html
[Winston]: https://github.com/winstonjs/winston
