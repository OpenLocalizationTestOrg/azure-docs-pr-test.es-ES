---
title: "autenticación de aaaUser para las aplicaciones de API de servicio de aplicaciones de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooprotect una aplicación de API de servicio de aplicaciones de Azure por lo que permite tener acceso a tooauthenticated solo a los usuarios."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 3896760d-46ff-4b67-b98a-edd233f24758
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: alkarche
ms.openlocfilehash: 4702fc77fcfe736405e22b033c35d22ae3c5a300
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="user-authentication-for-api-apps-in-azure-app-service"></a>Autenticación de usuario para aplicaciones de API en el Servicio de aplicaciones de Azure
## <a name="overview"></a>Información general
Este artículo muestra cómo puede llamarlo tooprotect una aplicación de API de Azure para solo los usuarios autenticados. Hello artículo se da por supuesto que ha leído hello [información general de la autenticación de servicio de aplicaciones de Azure](../app-service/app-service-authentication-overview.md).

Aprenderá a realizar los siguientes procedimientos:

* ¿Cómo tooconfigure un proveedor de autenticación, con detalles de Azure Active Directory (Azure AD).
* Cómo tooconsume una aplicación de API protegida mediante el uso de Hola [Active Directory Authentication Library (ADAL) para JavaScript](https://github.com/AzureAD/azure-activedirectory-library-for-js).

artículo de Hello contiene dos secciones:

* Hola [cómo tooconfigure autenticación de usuario en el servicio de aplicación de Azure](#authconfig) sección se explica cómo general tooconfigure de autenticación de usuario para cualquier aplicación de API y se aplica por igual marcos tooall compatibles con el servicio de aplicación, incluidos los. NET, Node.js y Java.
* A partir de hello [continuar tutoriales de aplicaciones de API de .NET de hello](#tutorialstart) sección, Hola guías de artículo a través de la configuración de una aplicación de ejemplo con .NET crear final y un front-end de AngularJS que usa Azure Active Directory para el usuario autenticación. 

## <a id="authconfig"></a>¿Cómo tooconfigure autenticación de usuario en el servicio de aplicación de Azure
Esta sección proporciona instrucciones generales que se aplican a la aplicación de API de tooany. Para pasos específicos toohello tooDo aplicación de ejemplo de .NET de la lista, vaya demasiado[continuar tutoriales de introducción a .NET de hello](#tutorialstart).

1. Hola [portal de Azure](https://portal.azure.com/), navegue toohello **configuración** hoja de aplicación Hola API que desea tooprotect, buscar hello **características** sección y, a continuación, haga clic en  **Autenticación / autorización**.
   
    ![Autenticación/autorización del Portal de Azure](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. Hola **autenticación / autorización** hoja, haga clic en **en**.
3. Seleccione una de las opciones de Hola de hello **tootake de acción cuando no se autentica la solicitud** lista desplegable.
   
   * Si desea que sólo llamadas autenticadas tooreach la aplicación de API, elija uno de hello **iniciar sesión con...**  opciones. Esta opción permite tooprotect API aplicación hello sin escribir ningún código que se ejecuta en él.
   * Elija si desea que todas las llamadas tooreach la aplicación de API, **Permitir solicitud (ninguna acción)**. Puede usar esta opción de tooa opción toodirect sin autenticar los llamadores de proveedores de autenticación. Con esta opción tiene autorización de toowrite código toohandle.
     
     Para más información, consulte [Autenticación y autorización para Aplicaciones de API en el Servicio de aplicaciones de Azure](app-service-api-authentication.md#multiple-protection-options).
4. Seleccione uno o varios de hello **proveedores de autenticación**.
   
    imagen de Hello muestra las opciones que requieren todos los toobe de los llamadores autentica Azure AD.
   
    ![Hoja Autenticación/autorización del Portal de Azure](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
   
    Al elegir un proveedor de autenticación, el portal de hello muestra una hoja de configuración para dicho proveedor. 
   
    Para obtener instrucciones detalladas que explican cómo tooconfigure Hola hojas de configuración de proveedor de autenticación, vea [cómo tooconfigure su inicio de sesión de Azure Active Directory de servicio de aplicaciones aplicación toouse](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). (vínculo de hello queda tooan artículo sobre Azure AD, pero artículo Hola propio contiene las pestañas que vinculan tooarticles para hello otros proveedores de autenticación).
5. Cuando haya terminado con la hoja de configuración de proveedor de autenticación de hello, haga clic en **Aceptar**.
6. Hola **autenticación / autorización** hoja, haga clic en **guardar**.

Cuando esto sucede, el servicio de aplicación autentica todas las llamadas API antes de alcanzar la aplicación de API de Hola. trabajo de servicios de autenticación de Hola Hola igual para todos los idiomas que admite el servicio de aplicaciones, incluido. NET, Node.js y Java. 

toomake había autenticado llamadas a la API, llamador Hola incluye el token de portador de OAuth 2.0 del proveedor de autenticación de Hola Hola encabezado de autorización de solicitudes HTTP. símbolo (token) de Hello puede ser adquirida mediante el uso SDK del proveedor de autenticación de hello.

## <a id="tutorialstart"></a>Tutoriales de aplicaciones de API de .NET de hello ininterrumpidos
Si está siguiendo los tutoriales de Node.js o Java de Hola para aplicaciones de API, omitir toohello siguiente artículo, [autenticación principal del servicio para las aplicaciones de la API](app-service-api-dotnet-service-principal-auth.md). 

Si está siguiendo la serie de tutoriales de hello .NET para aplicaciones de API y ya se ha implementado la aplicación de ejemplo de Hola como se indica en hello [primer](app-service-api-dotnet-get-started.md) y [segundo](app-service-api-cors-consume-javascript.md) tutoriales, omitir toohello [configurar la autenticación en el servicio de aplicaciones y Azure AD](#azureauth) sección.

Si desea toofollow este tutorial sin tener que pasar a través de tutoriales primeros y segunda hello, Hola siguiendo los pasos que explican cómo tooget se inicia con una aplicación de ejemplo de Hola de toodeploy proceso automatizado.

> [!NOTE]
> Hello pasos siguientes permiten toohello como si Hola los dos primeros tutoriales, con una excepción de punto de partida mismo: Visual Studio ya no sabe qué aplicación web o una aplicación de API que cada proyecto se implementa en. Eso significa que no tiene las instrucciones exactas en este tutorial que explican cómo toodeploy toohello derecho destinos. Si no le convencen pensar en cómo los pasos en su propia implementación de hello toodo, es mejor serie de tutoriales de hello toofollow de hello [primer tutorial](app-service-api-dotnet-get-started.md) que toostart con este automatizar el proceso de implementación.
> 
> 

1. Asegúrese de que dispone de todos los requisitos previos de hello descritos en hello [primer tutorial](app-service-api-dotnet-get-started.md). En suma toohello requisitos previos descritos estos tutoriales de autenticación se supone que ha trabajado con aplicaciones de servicio de aplicaciones web y aplicaciones de API en Visual Studio y Hola portal de Azure.
2. Haga clic en hello **implementar tooAzure** botón en hello [archivo Léame de tooDo lista sample repositorio](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/readme.md) hello y aplicaciones de API de hello toodeploy de aplicación web. Tome nota del grupo de recursos de Azure de Hola que se crea, ya puede usar este toolook más adelante la aplicación web y los nombres de aplicación de API.
3. Descarga u Hola clon [repositorio de ejemplo de lista de tooDo](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) código de hello tooget que trabajará con localmente en Visual Studio.

## <a id="azureauth"></a> Configuración de la autenticación en el Servicio de aplicaciones y Azure AD
Ahora dispone de aplicación Hola que se ejecuta en el servicio de aplicación de Azure sin necesidad de que los usuarios se autentiquen. En esta sección agregará autenticación haciendo Hola siguientes tareas:

* Configurar la autenticación de Azure Active Directory (Azure AD) toorequire de servicio de aplicaciones para llamar a la aplicación de API de nivel intermedio de hello.
* Crear una aplicación de Azure.
* Configurar el token portador hello Azure AD aplicación toosend Hola después de front-end de inicio de sesión toohello AngularJS. 

Si experimenta problemas al siguiente instrucciones de tutorial de hello, vea hello [solución de problemas](#troubleshooting) sección al final de hello del tutorial Hola. 

### <a name="configure-authentication-for-hello-middle-tier-api-app"></a>Configurar la autenticación de nivel intermedio de hello aplicación de API
1. Hola [portal de Azure](https://portal.azure.com/), navegue toohello **configuración** hoja de aplicación Hola API que creó para el proyecto de ToDoListAPI hello, encontrar Hola **características** sección y, a continuación, Haga clic en **autenticación / autorización**.
   
    ![Autenticación/autorización del Portal de Azure](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. Hola **autenticación / autorización** hoja, haga clic en **en**.
3. Hola **tootake de acción cuando no se autentica la solicitud** lista desplegable, seleccione **iniciar sesión con Azure Active Directory**.
   
    Esta opción garantiza que ninguna solicitud unauathenticated alcanzará la aplicación de API de hello. 
4. En **Proveedores de autenticación**, haga clic en **Azure Active Directory**.
   
    ![Hoja Autenticación/autorización del Portal de Azure](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. Hola **configuración de Azure Active Directory** hoja, haga clic en **Express**
   
    ![Opción Express de Autenticación/autorización del Portal de Azure](./media/app-service-api-dotnet-user-principal-auth/aadsettings.png)
   
    Con hello **Express** opción, servicio de aplicaciones puede crear automáticamente una aplicación de Azure AD en Azure AD [inquilino](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant). 
   
    No tienes toocreate un inquilino, porque cada cuenta de Azure automáticamente tiene uno.
6. En **modo de administración**, haga clic en **crear nueva aplicación de AD** si no está ya seleccionada y observe el valor de Hola Hola **crear aplicación** cuadro de texto; podrá buscar este AAD aplicación Hola portal de Azure clásico más adelante.
   
    ![Configuración de Azure AD del Portal de Azure](./media/app-service-api-dotnet-user-principal-auth/aadsettings2.png)
   
    Azure creará automáticamente una aplicación de Azure AD con el nombre indicado de hello en el inquilino de Azure AD. De forma predeterminada, se denomina aplicación de Azure AD Hola Hola igual como aplicación hello API. Si lo prefiere, escriba un nombre diferente.
7. Haga clic en **Aceptar**.
8. Hola **autenticación / autorización** hoja, haga clic en **guardar**.
   
    ![Haga clic en Guardar](./media/app-service-api-dotnet-user-principal-auth/authsave.png)

Ahora solo los usuarios de su inquilino de Azure AD pueden llamar a la aplicación de API de Hola.

### <a name="optional-test-hello-api-app"></a>Opcional: Probar la aplicación hello API
1. En un explorador, vaya toohello URL de aplicación hello API: Hola **aplicación de API** hoja Hola portal de Azure, haga clic en vínculo hello en **URL**.  
   
    Son redirigidos tooa pantalla de inicio de sesión dado que las solicitudes no autenticadas no se permiten la aplicación de API de hello tooreach.
   
    Si el explorador deja de página toohello "se creó correctamente", ya se podría registrar explorador hello en--en ese caso, abra una ventana de InPrivate o de incógnito y vaya URL de la aplicación toohello API.
2. Inicie sesión con las credenciales de un usuario en su inquilino de Azure AD.
   
    Cuando ha iniciado sesión, Hola "se creó correctamente" página aparece en el Explorador de Hola.
3. Explorador de hello cerrar.

### <a name="configure-hello-azure-ad-application"></a>Configurar la aplicación hello Azure AD
Cuando se configuró la autenticación de Azure AD, el Servicio de aplicaciones creó automáticamente una aplicación de Azure AD. De forma predeterminada la aplicación hello nuevo Azure AD era URL de la aplicación de tooprovide configurado Hola portador token toohello API. En esta sección configurará hello Azure AD aplicación tooprovide Hola portador token toohello AngularJS front-end en lugar de la aplicación de API de nivel intermedio de toohello directamente. front-end de Hello AngularJS enviará Hola token toohello API aplicación cuando llama a la aplicación de API de Hola.

> [!NOTE]
> proceso de hello tookeep tan simple como sea posible, este tutorial usa un único Azure AD aplicación front-end de Hola y aplicación de API de nivel intermedio de hello. Otra opción es toouse dos aplicaciones de Azure AD. En ese caso tendría de toogive Hola front-end Azure AD aplicación permiso toocall Hola de Azure AD aplicación de nivel medio. Este enfoque de varias aplicaciones proporcionaría más control granular sobre el nivel de permisos tooeach.
> 
> 

1. Hola [portal de Azure clásico](https://manage.windowsazure.com/), vaya demasiado**Azure Active Directory**.
   
   Tener portal clásico de hello toouse porque ciertas opciones de Azure Active Directory que necesita tener acceso a tooare no está disponible todavía en el portal de Azure actual Hola.
2. En hello **directorio** , haga clic en su inquilino de AAD.
   
   ![Azure AD en el Portal clásico](./media/app-service-api-dotnet-user-principal-auth/selecttenant.png)
3. Haga clic en **aplicaciones > las aplicaciones que tiene mi compañía**y, a continuación, haga clic en la casilla de verificación Hola.
   
   También tendrá la nueva aplicación de toorefresh Hola página toosee Hola.
4. En la lista Hola de aplicaciones, haga clic en Hola Hola uno que Azure crea automáticamente cuando se ha habilitado la autenticación de la aplicación de API.
   
   ![Pestaña Aplicaciones de Azure AD](./media/app-service-api-dotnet-user-principal-auth/appstab.png)
5. Haga clic en **Configurar**.
   
   ![Pestaña Configurar de Azure AD](./media/app-service-api-dotnet-user-principal-auth/configure.png)
6. Establecer **dirección URL de inicio de sesión** toohello URL de la aplicación web de AngularJS, ninguna barra diagonal final.
   
   Por ejemplo, https://todolistangular.azurewebsites.net.
   
   ![URL de inicio de sesión](./media/app-service-api-dotnet-user-principal-auth/signonurlazure.png)
7. Establecer **dirección URL de respuesta** toohello URL de la aplicación web, ninguna barra diagonal final.
   
   Por ejemplo: https://todolistsangular.azurewebsites.net.
8. Haga clic en **Save**.
   
   ![URL de respuesta](./media/app-service-api-dotnet-user-principal-auth/replyurlazure.png)
9. En la parte inferior de Hola de página de hello, haga clic en **administrar manifiesto > descarga manifiesto**.
   
   ![Descargar el manifiesto](./media/app-service-api-dotnet-user-principal-auth/downloadmanifest.png)
10. Descargar la ubicación del archivo de hello tooa donde se puede editar.
11. Hola Descargar archivo de manifiesto, busque hello `oauth2AllowImplicitFlow` propiedad. Cambiar valor Hola de esta propiedad desde `false` demasiado`true`y, a continuación, guarde el archivo hello.
    
    Esta configuración es necesaria para el acceso desde una aplicación de una página de JavaScript. Permite devuelto en el fragmento de dirección URL de Hola Hola Oauth 2.0 portador token toobe.
12. Haga clic en **administrar manifiesto > cargar manifiesto**y el archivo de Hola de carga que actualizaron en hello anterior paso.
    
    ![Cargar el manifiesto](./media/app-service-api-dotnet-user-principal-auth/uploadmanifest.png)
13. Hola copia **Id. de cliente** valor y guárdelo en algún lugar puede obtener desde más tarde.

## <a name="configure-hello-todolistangular-project-toouse-authentication"></a>Configurar la autenticación de hello ToDoListAngular proyecto toouse
En esta sección Cambiar front-end de hello AngularJS para que use la biblioteca de autenticación de Active Directory (ADAL) de JS tooacquire un token de portador de hello usuario que inició sesión de Azure AD. código de Hello incluirá token hello en las solicitudes HTTP enviadas toohello nivel intermedio, como se muestra en hello siguiente diagrama. 

![Diagrama de autenticación de usuario](./media/app-service-api-dotnet-user-principal-auth/appdiagram.png)

Asegúrese de hello después toofiles cambios en el proyecto de ToDoListAngular Hola.

1. Abra hello *index.cshtml* archivo.
2. Quite el comentario de las líneas de Hola que hacen referencia a hello biblioteca de autenticación de Active Directory (ADAL) para las secuencias de comandos JS.
   
        <script src="app/scripts/adal.js"></script>
        <script src="app/scripts/adal-angular.js"></script>
3. Abra hello *app/scripts/app.js* archivo.
4. Comenta bloque Hola de código marcado para "sin autenticación" y quite el bloque de Hola de código marcado para "con la autenticación".
   
    Este cambio hace referencia a proveedor de autenticación de ADAL JS hello y proporciona tooit de valores de configuración. Hola siguiendo los pasos debe establecer valores de configuración de Hola para su aplicación de API y la aplicación de Azure AD.
5. En el código de hello establece hello `endpoints` URL de la API de hello variable, establezca toohello dirección URL de aplicación Hola API que se crean para hello ToDoListAPI proyecto y establecer hello Azure AD aplicación identificador toohello Id. de cliente que copió de hello portal de Azure clásico.
   
    código de Hello está similar toohello siguiente ejemplo.
   
        var endpoints = {
            "https://todolistapi0121.azurewebsites.net/": "1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3"
        };
6. Hola llamar demasiado`adalProvider.init`, establezca `tenant` tooyour nombre del inquilino y `clientId` valor toosame que utilizó en el paso anterior de Hola.
   
    código de Hello está similar toohello siguiente ejemplo.
   
        adalProvider.init(
            {
                instance: 'https://login.microsoftonline.com/', 
                tenant: 'contoso.onmicrosoft.com',
                clientId: '1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3',
                extraQueryParameter: 'nux=1',
                endpoints: endpoints
            },
            $httpProvider
            );
   
    Estos cambios se demasiado`app.js` especificar que código de llamada de Hola y Hola denominado API están en aplicación hello misma instancia de Azure AD.
7. Abra hello *app/scripts/homeCtrl.js* archivo.
8. Comenta bloque Hola de código marcado para "sin autenticación" y quite el bloque de Hola de código marcado para "con la autenticación".
9. Abra hello *app/scripts/indexCtrl.js* archivo.
10. Comenta bloque Hola de código marcado para "sin autenticación" y quite el bloque de Hola de código marcado para "con la autenticación".

### <a name="deploy-hello-todolistangular-project-tooazure"></a>Implementar hello ToDoListAngular proyecto tooAzure
1. En **el Explorador de soluciones**, haga clic en proyecto de hello ToDoListAngular y, a continuación, haga clic en **publicar**.
2. Haga clic en **Publicar**.
   
    Visual Studio implementa Hola proyecto y abre la dirección URL base de la aplicación web de toohello de explorador. Esto mostrará una página de 403 error, que es normal que un intento de toogo tooa API Web dirección URL base desde un explorador.
   
    También tendrá toomake un nivel intermedio de toohello de cambio de aplicación de API para poder probar la aplicación hello.
3. Explorador de hello cerrar.

## <a name="configure-hello-todolistapi-project-toouse-authentication"></a>Configurar la autenticación de hello ToDoListAPI proyecto toouse
Hola actualmente envíos de proyecto ToDoListAPI "*" como hello `owner` tooToDoListDataAPI de valor. En esta sección Cambiar Hola código toosend Hola ID de usuario que inició sesión Hola.

Asegúrese de hello siguientes cambios en el proyecto de ToDoListAPI Hola.

1. Abra hello *Controllers/ToDoListController.cs* de archivos y quite el comentario de línea de hello en cada método de acción que establece `owner` toohello Azure AD `NameIdentifier` valor de notificación. Por ejemplo:
   
        owner = ((ClaimsIdentity)User.Identity).FindFirst(ClaimTypes.NameIdentifier).Value;
   
    **Importante**: no quite comentarios del código de hello `ToDoListDataAPI` método; lo hará más adelante para el tutorial de autenticación principal de servicio de Hola.

### <a name="deploy-hello-todolistapi-project-tooazure"></a>Implementar hello ToDoListAPI proyecto tooAzure
1. En **el Explorador de soluciones**, haga clic en proyecto de hello ToDoListAPI y, a continuación, haga clic en **publicar**.
2. Haga clic en **Publicar**.
   
    Visual Studio implementa Hola proyecto y abre la dirección URL base de la aplicación API de toohello de explorador.
3. Explorador de hello cerrar.

### <a name="test-hello-application"></a>Probar la aplicación hello
1. Ir a dirección URL de toohello de aplicación web de hello, **mediante HTTPS y no HTTP**.
2. Haga clic en hello **tooDo lista** ficha.
   
    Son toolog solicitada en.
3. Inicie sesión con credenciales de Hola de un usuario en su inquilino de AAD.
4. Hola **tooDo lista** aparecerá la página.
   
   ![página de lista tooDo](./media/app-service-api-dotnet-user-principal-auth/webappindex.png)
   
   No se muestran tareas pendientes porque hasta todas han sido para el propietario "*". Ahora nivel intermedio Hola solicita elementos para el usuario que inició sesión hello y no se ha creado aún.
5. Agregar nueva tooverify de elementos de tarea que funciona la aplicación hello.
6. En otra ventana del explorador, vaya toohello Swagger dirección URL de interfaz de usuario para la aplicación de API de ToDoListDataAPI hello y haga clic en **ToDoList > obtener**. Escriba un asterisco para hello `owner` parámetro y, a continuación, haga clic en **Pruébelo**.
   
   respuesta de Hello muestra que elementos pendientes de la nueva Hola tienen Id. de usuario de hello real AD de Azure en la propiedad Owner Hola.
   
   ![Id. de propietario en respuesta JSON](./media/app-service-api-dotnet-user-principal-auth/todolistapiauth.png)

## <a name="building-hello-projects-from-scratch"></a>Compilar proyectos de Hola desde el principio
proyectos de Hello dos API Web se crearon con hello **aplicación de API de Azure** de proyectos de plantilla y reemplazando Hola valores de controlador predeterminado con un controlador ToDoList. 

Para obtener información acerca de cómo crear demasiado una aplicación de página de AngularJS con un API Web 2 back-end, vea [manos en laboratorio: compilar una aplicación de página única (SPA) con ASP.NET Web API y Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs). Para obtener información acerca de cómo tooadd código de autenticación de Azure AD, vea Hola recursos siguientes:

* [Seguridad de las aplicaciones de una sola página AngularJS con Azure AD](../active-directory/active-directory-devquickstarts-angular.md).
* [Introducing ADAL JS v1 (Presentación de ADAL JS v1)](http://www.cloudidentity.com/blog/2015/02/19/introducing-adal-js-v1/)

## <a name="troubleshooting"></a>Solución de problemas
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* Asegúrese de no confundir ToDoListAPI (nivel intermedio) con ToDoListDataAPI (capa de datos). Por ejemplo, compruebe que ha agregado la aplicación de API de nivel intermedio de toohello autenticación, no la capa de datos Hola. 
* Asegúrese de que hello y URL de la aplicación de API de nivel intermedio de AngularJS origen código referencias Hola Hola (ToDoListAPI, no ToDoListDataAPI) corrijan identificador de cliente de Azure AD. 

## <a name="next-steps"></a>Pasos siguientes
En este tutorial ha aprendido cómo toouse autenticación de servicio de aplicaciones para una aplicación de API y cómo toocall Hola aplicación de API mediante el uso de Hola biblioteca de AAL JS. En el tutorial siguiente Hola aprenderá cómo demasiado[un acceso seguro tooyour API de aplicación para los escenarios de servicio a servicio](app-service-api-dotnet-service-principal-auth.md).

