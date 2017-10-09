---
title: aaaGet a trabajar con aplicaciones de API y ASP.NET en el servicio de aplicaciones | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate, implementar y utilizar una aplicación de API de ASP.NET en el servicio de aplicación de Azure, mediante Visual Studio 2015."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: ddc028b2-cde0-4567-a6ee-32cb264a830a
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: alkarche
ms.openlocfilehash: d3e90f1585907d183b0435c6cafc5585bc1e29ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-api-apps-aspnet-and-swagger-in-azure-app-service"></a>Introducción a Aplicaciones de API, ASP.NET y Swagger en el Servicio de aplicaciones de Azure
[!INCLUDE [selector](../../includes/app-service-api-get-started-selector.md)]

Esto es hello en primer lugar en una serie de tutoriales que muestran cómo toouse características de la aplicación de Azure Service que son útiles para desarrollar y hospedar las API de REST.  En este tutorial se explica la compatibilidad con los metadatos de la API en formato Swagger.

Aprenderá a realizar los siguientes procedimientos:

* ¿Cómo toocreate e implementar [aplicaciones de API](app-service-api-apps-why-best-platform.md) en el servicio de aplicación de Azure mediante las herramientas integradas en Visual Studio 2015.
* Cómo tooautomate API de detección mediante el uso de hello Swashbuckle NuGet paquete toodynamically generar metadatos de Swagger API.
* Cómo tooautomatically de metadatos de Swagger API toouse generar código de cliente para una aplicación de API.

## <a name="sample-application-overview"></a>Información general de la aplicación de ejemplo
En este tutorial, se trabaja con una aplicación de ejemplo de lista de tareas pendientes sencilla. aplicación Hello tiene una aplicación de página (SPA) front-end, un nivel intermedio de ASP.NET Web API y una capa de datos de ASP.NET Web API.

![Diagrama de la aplicación de ejemplo de Aplicaciones de API](./media/app-service-api-dotnet-get-started/noauthdiagram.png)

Esta es una captura de pantalla de hello [AngularJS](https://angularjs.org/) front-end.

![Lista de toodo de aplicación de ejemplo de aplicaciones de API](./media/app-service-api-dotnet-get-started/todospa.png)

Hola solución de Visual Studio incluye tres proyectos:

![](./media/app-service-api-dotnet-get-started/projectsinse.png)

* **ToDoListAngular** -front-end de hello: un SPA de AngularJS que llama el nivel intermedio de Hola.
* **ToDoListAPI** -nivel intermedio de hello: un proyecto de ASP.NET Web API que llama a nivel de datos de hello tooperform las operaciones CRUD de elementos pendientes.
* **ToDoListDataAPI** -nivel de datos de hello: un proyecto de ASP.NET Web API que realiza operaciones CRUD en elementos pendientes.

arquitectura de tres niveles de Hello es una de las arquitecturas que puede implementar mediante el uso de aplicaciones de API y se usa aquí únicamente con fines de demostración. código de Hello en cada nivel es tan sencillo como características de aplicaciones de API de posibles toodemonstrate; Por ejemplo, capa de datos de hello utiliza memoria del servidor en lugar de una base de datos como su mecanismo de persistencia.

Al llevar a cabo este tutorial, tendrá dos proyectos API Web Hola de seguridad y ejecutan en la nube de hello en aplicaciones de API de servicio de aplicación.

tutorial siguiente de Hello en serie de Hola implementa en la nube Hola SPA front-end toohello.

## <a name="prerequisites"></a>Requisitos previos
* Instrucciones del tutorial Hola ASP.NET Web API - suponga que tiene un conocimiento básico de cómo toowork con ASP.NET [API Web 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) en Visual Studio.
* Cuenta de Azure: puede [abrir una cuenta gratuita de Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) o [activar las ventajas de las que disfrutan los suscriptores de Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).
  
    Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/). Ahí puede crear de forma inmediata una aplicación de inicio de corta duración en App Service ( **no se requiere tarjeta de crédito**ni se establece ningún compromiso).
* Visual Studio 2015 con hello [Azure SDK para .NET](https://azure.microsoft.com/downloads/archive-net-downloads/) -Hola SDK instala Visual Studio 2015 automáticamente si aún no lo tiene.
  
  * En Visual Studio, haga clic en Ayuda -> Acerca de Microsoft Visual Studio y asegúrese de que tiene instalado "Azure App Service Tools v2.9.1", o una versión superior.
    
    ![Versión de Azure App Tools](./media/app-service-api-dotnet-get-started/apiversion.png)
    
    > [!NOTE]
    > Dependiendo de cuántas de las dependencias del SDK de hello ya tiene en su equipo, instalar Hola SDK podría tardar mucho tiempo, desde unos minutos tooa media hora o más.
    > 
    > 

## <a name="download-hello-sample-application"></a>Descargar la aplicación de ejemplo de Hola
1. Descargar hello [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) repositorio.
   
    Puede hacer clic en hello **Download ZIP** botón o un clon repositorio hello en el equipo local.
2. Abra la solución de ToDoList de hello en Visual Studio 2015 o 2013.
   
   1. Necesitará tootrust cada solución.
         ![Advertencia de seguridad](./media/app-service-api-dotnet-get-started/securitywarning.png)
3. Crear paquetes de NuGet de hello soluciones (CTRL + MAYÚS + B) toorestore Hola.
   
    Si desea que toosee Hola aplicación en funcionamiento antes de implementarla, puede ejecutarlo localmente. Asegúrese de que ToDoListDataAPI es la solución de ejecución Hola y el proyecto de inicio. En el explorador, puede producirse error toosee un código 403 de HTTP.

## <a name="use-swagger-api-metadata-and-ui"></a>Uso de la interfaz de usuario y los metadatos de la API de Swagger
La compatibilidad con los metadatos de la API de [Swagger 2.0](http://swagger.io/) está integrada en el Servicio de aplicaciones de Azure. Cada aplicación de API puede especificar un punto de conexión de dirección URL que devuelve los metadatos para hello API en formato JSON de Swagger. Hello metadatos devueltos desde ese punto de conexión pueden ser código de cliente de toogenerate usado.

Un proyecto de ASP.NET Web API puede generar dinámicamente los metadatos de Swagger mediante hello [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) paquete NuGet. Hola Swashbuckle NuGet paquete ya está instalado en los proyectos de ToDoListDataAPI y ToDoListAPI de Hola que ha descargado.

En esta sección del tutorial de hello, mirar los metadatos de Swagger 2.0 Hola generado y, a continuación, pruebe una prueba de interfaz de usuario que se basa en los metadatos de Swagger Hola.

1. Establecer el proyecto de hello ToDoListDataAPI (**no** proyecto ToDoListAPI de hello) como proyecto de inicio de Hola.
   
    ![Establezca ToDoDataAPI como proyecto de inicio](./media/app-service-api-dotnet-get-started/startupproject.png)
2. Presione F5 o haga clic en **Depurar > Iniciar depuración** toorun proyecto de hello en modo de depuración.
   
    Explorador de Hola se abre y muestra la página de error 403 de HTTP de Hola.
3. En la barra de direcciones del explorador, agregue `swagger/docs/v1` toohello final de línea de hello y, a continuación, presione ENTRAR. (Hola dirección URL es `http://localhost:45914/swagger/docs/v1`.)
   
    Se trata de dirección URL predeterminada de hello usado metadatos de Swagger 2.0 JSON tooreturn Swashbuckle para hello API.
   
    Si está usando Internet Explorer, Explorador de hello le pide que toodownload una *v1.json* archivo.
   
    ![Descargar metadatos de JSON en Internet Explorer](./media/app-service-api-dotnet-get-started/iev1json.png)
   
    Si usas Chrome, Firefox o borde, Explorador de hello muestra hello JSON en la ventana del explorador Hola. Otros exploradores administrar JSON de manera diferente y la ventana del explorador puede no ser exactamente igual que el ejemplo de Hola.
   
    ![Metadatos de JSON en Chrome](./media/app-service-api-dotnet-get-started/chromev1json.png)
   
    Hello en el ejemplo siguiente muestra la Hola primera sección de metadatos de Swagger de Hola de hello API, con definición Hola Hola Get (método). Estos metadatos son qué Hola unidades Swagger interfaz de usuario que usa en hello pasos, y se usa en una sección posterior de hello tutorial tooautomatically generar código de cliente.
   
        {
          "swagger": "2.0",
          "info": {
            "version": "v1",
            "title": "ToDoListDataAPI"
          },
          "host": "localhost:45914",
          "schemes": [ "http" ],
          "paths": {
            "/api/ToDoList": {
              "get": {
                "tags": [ "ToDoList" ],
                "operationId": "ToDoList_GetByOwner",
                "consumes": [ ],
                "produces": [ "application/json", "text/json", "application/xml", "text/xml" ],
                "parameters": [
                  {
                    "name": "owner",
                    "in": "query",
                    "required": true,
                    "type": "string"
                  }
                ],
                "responses": {
                  "200": {
                    "description": "OK",
                    "schema": {
                      "type": "array",
                      "items": { "$ref": "#/definitions/ToDoItem" }
                    }
                  }
                },
                "deprecated": false
              },
4. Cierre el Explorador de Hola y detener la depuración de Visual Studio.
5. Hola ToDoListDataAPI del proyecto en **el Explorador de soluciones**, abra hello *App_Start\SwaggerConfig.cs* archivo y, a continuación, desplácese hacia abajo tooline 174 y quite el siguiente código de hello.
   
        /*
            })
        .EnableSwaggerUi(c =>
            {
        */
   
    Hola *SwaggerConfig.cs* archivo se crea cuando se instala el paquete de Swashbuckle de hello en un proyecto. archivo Hello proporciona una serie de formas tooconfigure Swashbuckle.
   
    código de Hello que ha sin comentarios Hola habilita la interfaz de usuario Swagger que se utilizan en hello siguiendo los pasos. Cuando crea un proyecto de API Web mediante el uso de la plantilla de proyecto de aplicación de API de hello, este código está comentado de forma predeterminada como una medida de seguridad.
6. Vuelva a ejecutar el proyecto de Hola.
7. En la barra de direcciones del explorador, agregue `swagger` toohello final de línea de hello y, a continuación, presione ENTRAR. (Hola dirección URL es `http://localhost:45914/swagger`.)
8. Cuando aparezca la página de interfaz de usuario de Swagger de hello, haga clic en **ToDoList** métodos de hello toosee disponibles.
   
    ![Métodos disponibles en la interfaz de usuario de Swagger](./media/app-service-api-dotnet-get-started/methods.png)
9. Haga clic primero en hello **obtener** botón de lista de Hola.
10. Hola **parámetros** sección, escriba un asterisco como valor de Hola de hello `owner` parámetro y, a continuación, haga clic en **Pruébelo**.
    
    Al agregar la autenticación en tutoriales posteriores, nivel intermedio Hola proporcionará capa de datos de toohello de Id. de usuario real de Hola. Por ahora, todas las tareas tendrá asterisco como su Id. del propietario mientras se ejecuta aplicación hello sin la autenticación habilitada.
    
    ![Botón Try it out (Probar) de la interfaz de usuario de Swagger](./media/app-service-api-dotnet-get-started/gettryitout1.png)
    
    Hola Swagger de interfaz de usuario llama a Hola método ToDoList Get y muestra el código de respuesta de Hola y los resultados JSON.
    
    ![Resultado de hacer clic en el botón Try it out (Probar) de la interfaz de usuario de Swagger](./media/app-service-api-dotnet-get-started/gettryitout.png)
11. Haga clic en **Post**y, a continuación, haga clic en cuadro de hello en **esquema del modelo**.
    
    Al hacer clic en hello modelo esquema prefills Hola cuadro de entrada donde puede especificar el valor del parámetro Hola Hola método Post. (Si esto no funciona en Internet Explorer, use un explorador diferente o escribir manualmente el valor del parámetro hello en el paso siguiente de hello).  
    
    ![Publicación tras hacer clic en el botón Try it out (Probar) de la interfaz de usuario de Swagger](./media/app-service-api-dotnet-get-started/post.png)
12. Hola de cambio JSON en hello `todo` parámetro de entrada de cuadro para que se parezca al siguiente ejemplo de Hola o sustituir su propio texto de descripción:
    
        {
          "ID": 2,
          "Description": "buy hello dog a toy",
          "Owner": "*"
        }
13. Haga clic en **Try it out**(Probar).
    
    Hola ToDoList API devuelve un código de respuesta HTTP 204 que indica una ejecución correcta.
14. Haga clic primero en hello **obtener** botón y, a continuación, haga clic en hello en esa sección de página de hello **Pruébelo** botón.
    
    Hola respuesta de obtención de método incluye ahora el nuevo elemento de toodo Hola.
15. Opcional: También intente Hola Put, Delete y obtener mediante métodos de identificador.
16. Cierre el Explorador de Hola y detener la depuración de Visual Studio.

Swashbuckle funciona con cualquier proyecto de ASP.NET Web API. Si desea que el proyecto existente del tooan de generación de metadatos de Swagger para tooadd, simplemente Instalar paquete de Swashbuckle Hola.

> [!NOTE]
> Los metadatos de Swagger incluyen un identificador único para cada operación de la API. De manera predeterminada, Swashbuckle puede generar identificadores de operación de Swagger duplicados para los métodos del controlador de la API web. Esto sucede si el controlador tiene métodos HTTP sobrecargados, tales como `Get()` y `Get(id)`. Para obtener información acerca de cómo se sobrecargan toohandle, consulte [definiciones de API genera personalizar Swashbuckle](app-service-api-dotnet-swashbuckle-customize.md). Si crea un proyecto de API Web en Visual Studio mediante el uso de la plantilla de aplicación de API de Azure de hello, código que genera el Id. único de la operación se agrega automáticamente toohello *SwaggerConfig.cs* archivo.  
> 
> 

## <a id="createapiapp"></a>Crear una aplicación de API de Azure e implementar código tooit
En esta sección, utilizará las herramientas de Azure que están integradas en Visual Studio hello **Publicar Web** Asistente toocreate una API nueva aplicación en Azure. A continuación, implemente hello ToDoListDataAPI proyecto toohello nueva aplicación de API y llamar a la API de hello ejecutando hello Swagger de interfaz de usuario.

1. En **el Explorador de soluciones**, haga clic en proyecto de hello ToDoListDataAPI y, a continuación, haga clic en **publicar**.
   
    ![Haga clic en Publicar en Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu.png)
2. Hola **perfil** paso de hello **Publicar Web** asistente, haga clic en **servicio de aplicaciones de Microsoft Azure**.
   
   ![Haga clic en Servicio de aplicaciones de Azure en Publicación web](./media/app-service-api-dotnet-get-started/selectappservice.png)
3. Inicie sesión en tooyour cuenta de Azure si aún no lo ha hecho, o actualice sus credenciales si está caducados.
4. En cuadro de diálogo de servicio de aplicaciones de Hola, elija hello Azure **suscripción** que desee toouse y, a continuación, haga clic en **nuevo**.
   
    ![Haga clic en Nuevo en el cuadro de diálogo Servicio de aplicaciones](./media/app-service-api-dotnet-get-started/clicknew.png)
   
    Hola **hospedaje** ficha de hello **crear servicio en la aplicación** aparece el cuadro de diálogo.
   
    Dado que va a implementar un proyecto de Web API con Swashbuckle instalado, Visual Studio se da por supuesto que desea toocreate una API App. Esto se indica mediante hello **API App Name** title y por Hola hechos que hello **cambiar tipo** lista desplegable se establece demasiado**API App**.
   
    ![Tipo de aplicación en el cuadro de diálogo Servicio de aplicaciones](./media/app-service-api-dotnet-get-started/apptype.png)
5. Escriba un **API App Name** que es único en hello *azurewebsites.net* dominio. Puede aceptar el nombre predeterminado de Hola que propone de Visual Studio.
   
    Si escribe un nombre que otra persona ya usado, puede ver una marca de exclamación roja toohello.
   
    Hello dirección URL de la aplicación hello API será `{API app name}.azurewebsites.net`.
6. Hola **grupo de recursos** lista desplegable, haga clic en **nuevo**y, a continuación, escriba "ToDoListGroup" u otro nombre si lo prefiere.
   
    Un grupo de recursos es una colección de recursos de Azure tales como aplicaciones de API, bases de datos, máquinas virtuales, etc.    Para este tutorial, es mejor toocreate un nuevo grupo de recursos ya hace fácil toodelete en un solo paso, que todos los recursos de Azure que se crean para el tutorial de Hola de Hola.
   
    Este cuadro permite seleccionar un [grupo de recursos](../azure-resource-manager/resource-group-overview.md) existente o crear uno nuevo, para lo que se debe escribir un nombre de grupo recursos que no exista en la suscripción.
7. Haga clic en hello **New** botón siguiente toohello **Plan de servicio de aplicaciones** lista desplegable.
   
    captura de pantalla de Hello muestra valores de ejemplo de **API App Name**, **suscripción**, y **grupo de recursos** --los valores serán diferentes.
   
    ![Cuadro de diálogo Crear servicio de aplicaciones](./media/app-service-api-dotnet-get-started/createas.png)
   
    Hola pasos crear un plan de servicio de aplicaciones para nuevo grupo de recursos Hola. Un plan de servicio de aplicaciones especifica los recursos de proceso de Hola que se ejecuta la aplicación de API en. Por ejemplo, si elige nivel gratuito de hello, la aplicación de API se ejecuta en máquinas virtuales compartidas, mientras para algunos niveles de pago se ejecuta en máquinas virtuales dedicadas. Para más información sobre los planes del Servicio de aplicaciones, consulte [Introducción detallada sobre los planes del Servicio de aplicaciones de Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
8. Hola **configurar el Plan de servicio de aplicación** cuadro de diálogo, escriba "ToDoListPlan" u otro nombre si lo prefiere.
9. Hola **ubicación** lista desplegable, elija la ubicación de hello tooyou más cercano.
   
    Esta opción especifica en qué centro de datos de Azure se ejecutará su aplicación. Elija una ubicación cerrar tooyou toominimize [latencia](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).
10. Hola **tamaño** lista desplegable, haga clic en **libre**.
    
    Para este tutorial, Hola libre de nivel de precios proporcionará un rendimiento suficiente.
11. Hola **configurar el Plan de servicio de aplicación** cuadro de diálogo, haga clic en **Aceptar**.
    
    ![Haga clic en Aceptar en Configurar el plan de servicio de aplicaciones](./media/app-service-api-dotnet-get-started/configasp.png)
12. Hola **crear servicio en la aplicación** cuadro de diálogo, haga clic en **crear**.
    
    ![Haga clic en Crear en el cuadro de diálogo Crear servicio de aplicaciones](./media/app-service-api-dotnet-get-started/clickcreate.png)
    
    Visual Studio crea la aplicación de API de hello y un perfil de publicación que tiene todos los valores de hello necesario para la aplicación hello API. A continuación, se abre hello **Publicar Web** asistente, que usará proyecto de hello toodeploy.
    
    Hola **Publicar Web** abre el Asistente para en hello **conexión** pestaña (se muestra a continuación).
    
    En hello **conexión** ficha hello **Server** y **nombre del sitio** aplicación de API de configuración tooyour de punto. Hola **nombre de usuario** y **contraseña** son credenciales de implementación que Azure crea automáticamente. Después de la implementación, Visual Studio abre un explorador toohello **dirección URL de destino** (que es el único propósito de Hola de **dirección URL de destino**).  
13. Haga clic en **Siguiente**.
    
    ![Haga clic en Siguiente en la pestaña Conexión de Publicación web](./media/app-service-api-dotnet-get-started/connnext.png)
    
    pestaña siguiente Hello es hello **configuración** pestaña (se muestra a continuación). Aquí puede cambiar los toodeploy de pestaña de configuración de compilación de hello una compilación de depuración para [depuración remota](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug). Hello ficha también ofrece varios **File Publish Options**:
    
    * Quitar archivos adicionales en el destino.
    * Precompilar durante la publicación.
    * Excluir archivos de la carpeta App_Data de Hola
    
    Para este tutorial no necesita ninguna de ellas. Para información más detallada de lo que hacen, consulte [How to: Deploy a Web Project Using One-Click Publish in Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx)(Implementación de un proyecto web mediante publicación con un solo clic en Visual Studio).
14. Haga clic en **Siguiente**.
    
    ![Haga clic en Siguiente en la pestaña Configuración de Publicación web](./media/app-service-api-dotnet-get-started/settingsnext.png)
    
    A continuación figura hello **vista previa** pestaña (se muestra a continuación), que proporciona un toosee oportunidad qué archivos van toobe copiado desde la aplicación de toohello API de proyecto. Si va a implementar una aplicación de API tooan de proyecto que se implementó tooearlier, se copian archivos modificados únicamente. Si desea toosee una lista de lo que se va a copiar, haga clic en hello **iniciar Preview** botón.
15. Haga clic en **Publicar**.
    
    ![Haga clic en Publicar en la pestaña Vista previa de Publicación web](./media/app-service-api-dotnet-get-started/clickpublish.png)
    
    Visual Studio implementa hello ToDoListDataAPI proyecto toohello nueva aplicación de API. Hola **salida** ventana registra una implementación correcta, y aparece una página "se creó correctamente" en una dirección URL toohello ventana abierta del explorador de la aplicación hello API.
    
    ![Implementación correcta en la ventana Salida](./media/app-service-api-dotnet-get-started/deploymentoutput.png)
    
    ![Página nueva que indica que la aplicación de API se creó correctamente](./media/app-service-api-dotnet-get-started/appcreated.png)
16. Agregar dirección URL de toohello "swagger" en la barra de direcciones del explorador de hello y, a continuación, presione ENTRAR. (Hola dirección URL es `http://{apiappname}.azurewebsites.net/swagger`.)
    
    Explorador de Hello muestra hello misma UI Swagger que vio anteriormente, pero ahora se ejecuta en la nube de Hola. Pruebe Hola método Get, y verá que tiene elementos de tareas 2 toohello atrás predeterminados. cambios de Hello realizadas anteriormente se guardaron en la memoria en el equipo local de Hola.
17. Abra hello [portal de Azure](https://portal.azure.com/).
    
    Hola portal de Azure es una interfaz web para administración de recursos de Azure, como aplicaciones de API.
18. Haga clic en **Más servicios > App Services**.
    
    ![Examinar Servicios de aplicaciones](./media/app-service-api-dotnet-get-started/browseas.png)
19. Hola **servicios de aplicaciones** hoja, busque y haga clic en la nueva aplicación de API. (En hello portal de Azure, se denominan ventanas que se abren derecha toohello *hojas*.)
    
    ![Hoja Servicios de aplicaciones](./media/app-service-api-dotnet-get-started/choosenewapiappinportal.png)
    
    Se abren dos hojas: Un módulo tiene una visión general de la aplicación de API de hello y uno tiene una larga lista de valores que puede ver y cambiar.
20. Hola **configuración** hoja, buscar hello **API** sección y haga clic en **definición de la API**.
    
    ![Definición de la API en hoja Configuración](./media/app-service-api-dotnet-get-started/apidefinsettings.png)
    
    Hola **definición de la API** hoja le permite especificar la dirección URL de Hola que devuelve los metadatos de Swagger 2.0 en formato JSON. Cuando Visual Studio crea la aplicación hello API, Establece el valor predeterminado toohello de hello API definición dirección URL de metadatos generados de forma Swashbuckle que vio anteriormente, que es la aplicación hello API de base de la dirección URL más `/swagger/docs/v1`.
    
    ![Dirección URL de definición de la API](./media/app-service-api-dotnet-get-started/apidefurl.png)
    
    Cuando se selecciona un código de cliente de toogenerate de aplicación de API para él, Visual Studio recupera metadatos de Hola desde esta dirección URL.

## <a id="codegen"></a>Generar código de cliente de capa de datos de Hola
Una de las ventajas de saludo de la integración de Swagger en aplicaciones de API de Azure es la generación automática de código. Clases de cliente generado resultará más fácil código toowrite que llama a una aplicación de API.

proyecto de Hello ToDoListAPI ya tiene Hola genera código de cliente, pero en hello pasos podrá eliminarla y volver a generarlo toosee cómo hello toodo la generación de código.

1. En Visual Studio **el Explorador de soluciones**, Hola ToDoListAPI proyecto de equipo y eliminar hello *ToDoListDataAPI* carpeta. **Precaución: Eliminar la carpeta de hello solo, no en proyecto de ToDoListDataAPI Hola.**
   
    ![Eliminar código de cliente generado](./media/app-service-api-dotnet-get-started/deletecodegen.png)
   
    Esta carpeta se creó mediante el proceso de generación de código de hello que le sobre toogo a través de.
2. Haga clic en proyecto de hello ToDoListAPI y, a continuación, haga clic en **Agregar > cliente de la API de REST**.
   
    ![Agregar cliente de API de REST en Visual Studio](./media/app-service-api-dotnet-get-started/codegenmenu.png)
3. Hola **Agregar cliente de API de REST** cuadro de diálogo, haga clic en **dirección URL de Swagger**y, a continuación, haga clic en **Seleccionar activos de Azure**.
   
    ![Seleccionar recurso de Azure](./media/app-service-api-dotnet-get-started/codegenbrowse.png)
4. Hola **servicio de aplicaciones** cuadro de diálogo, expanda grupo de recursos de Hola que está usando para este tutorial y seleccione la aplicación de API y, a continuación, haga clic en **Aceptar**.
   
    ![Seleccione aplicación de API para la generación de código](./media/app-service-api-dotnet-get-started/codegenselect.png)
   
    Tenga en cuenta que, cuando se regresa toohello **Agregar cliente de API de REST** cuadro de diálogo, cuadro de texto de Hola se ha rellenado con la definición de hello API valor de dirección URL que vio anteriormente en el portal de Hola.
   
    ![Dirección URL de definición de la API](./media/app-service-api-dotnet-get-started/codegenurlplugged.png)
   
   > [!TIP]
   > Metadatos de tooget de una manera alternativa para la generación de código están tooenter Hola URL directamente en lugar de pasar a través del cuadro de diálogo de examinar Hola. O si desea toogenerate código de cliente antes de implementar tooAzure, podría ejecutar el proyecto de API Web de hello localmente, ir a dirección URL de toohello que proporciona el archivo de Swagger JSON hello, guarde el archivo de hello, y utilizar hello **selecciona un archivo de metadatos de Swagger existente**opción.
   > 
   > 
5. Hola **Agregar cliente de API de REST** cuadro de diálogo, haga clic en **Aceptar**.
   
    Visual Studio crea una carpeta denominada después de la aplicación hello API y genera las clases de cliente.
   
    ![Archivos de código para cliente generado](./media/app-service-api-dotnet-get-started/codegenfiles.png)
6. En hello ToDoListAPI proyecto, abra *Controllers\ToDoListController.cs* toosee código de hello en línea 40 que llame a las API de hello mediante cliente hello generado.
   
    Hola siguiente fragmento de código muestra cómo el código de hello crea una instancia de objeto de cliente de Hola y Hola de llamadas de método Get.
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));
            return client;
        }
   
        public async Task<IEnumerable<ToDoItem>> Get()
        {
            using (var client = NewDataAPIClient())
            {
                var results = await client.ToDoList.GetByOwnerAsync(owner);
                return results.Select(m => new ToDoItem
                {
                    Description = m.Description,
                    ID = (int)m.ID,
                    Owner = m.Owner
                });
            }
        }
   
    parámetro de constructor de Hello Obtiene la dirección URL del extremo de Hola de hello `toDoListDataAPIURL` configuración de la aplicación. En el archivo Web.config de hello, ese valor es toohello conjunto local URL de IIS Express de hello API del proyecto para que pueda ejecutar aplicación hello localmente. Si se omite el parámetro de constructor de hello, el punto de conexión de hello predeterminado es dirección URL de Hola que genera código de hello desde.
7. Se generará la clase de cliente con un nombre diferente en función de su nombre de la aplicación de API; cambiar código de hello en *Controllers\ToDoListController.cs* para que hello nombre de tipo coincida con lo que se generó en el proyecto. Por ejemplo, si el nombre de la aplicación de API es ToDoListDataAPI071316, cambiaría este código:
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));

toothis:

        private static ToDoListDataAPI071316 NewDataAPIClient()
        {
            var client = new ToDoListDataAPI071316(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));


## <a name="create-an-api-app-toohost-hello-middle-tier"></a>Crear un nivel intermedio de API aplicación toohost Hola
Anteriormente se [crear aplicación de API de nivel de datos de hello e implementar código tooit](#createapiapp).  Ahora siga Hola mismo procedimiento para la aplicación de API de nivel intermedio de hello.

1. En **el Explorador de soluciones**, nivel intermedio de contextual hello ToDoListAPI (no Hola capa de datos ToDoListDataAPI) del proyecto y, a continuación, haga clic en **publicar**.
   
    ![Haga clic en Publicar en Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu2.png)
2. Hola **perfil** ficha de hello **Publicar Web** asistente, haga clic en **servicio de aplicaciones de Microsoft Azure**.
3. Hola **servicio de aplicaciones** cuadro de diálogo, haga clic en **nuevo**.
4. Hola **hospedaje** ficha de hello **crear servicio en la aplicación** diálogo cuadro, acepte el valor predeterminado de hello **API App Name** o escriba un nombre que sea único en hello  *azurewebsites.NET* dominio.
5. Elija hello Azure **suscripción** ha utilizado.
6. Hola **grupo de recursos** lista desplegable, elija Hola mismo grupo de recursos que creó anteriormente.
7. Hola **Plan de servicio de aplicaciones** lista desplegable, elija Hola mismo plan que creó anteriormente. Valor de toothat tomará predeterminado.
8. Haga clic en **Crear**.
   
    Visual Studio crea la aplicación hello API, crea un perfil de publicación para él y se muestra hello **conexión** paso de hello **Publicar Web** asistente.
9. Hola **conexión** paso de hello **Publicar Web** asistente, haga clic en **publicar**.
   
   Visual Studio implementa hello ToDoListAPI proyecto toohello nueva aplicación de API y abre una dirección URL toohello del explorador de la aplicación de API de hello. aparece la página de Hola "se creó correctamente".

## <a name="configure-hello-middle-tier-toocall-hello-data-tier"></a>Configurar la capa de datos de hello nivel intermedio toocall Hola
Si se llama ahora aplicación de API de nivel intermedio de hello, intentaría capa de datos de hello toocall con dirección URL de localhost de Hola que sigue en el archivo Web.config de Hola. En esta sección se introduce URL de aplicación de API de nivel de datos de hello en una configuración de entorno de aplicación de API de nivel intermedio de Hola. Cuando hello código de aplicación de API de nivel intermedio de hello recupera configuración de dirección URL de capa de datos de hello, configuración del entorno Hola reemplazará lo que aparece en el archivo Web.config de Hola.

1. Vaya toohello [portal de Azure](https://portal.azure.com/)y, a continuación, navegue toohello **API App** hoja para que se creó toohost hello TodoListAPI (nivel intermedio) proyecto de aplicación de hello API.
2. En Hola de API App **configuración** hoja, haga clic en **configuración de la aplicación**.
3. En Hola de API App **configuración de la aplicación** hoja, desplácese hacia abajo toohello **configuración de la aplicación** sección y agregue Hola siguiente clave y valor. valor de Hello será la dirección URL de Hola de hello primera API aplicación publicada en este tutorial.
   
   | **Clave** | toDoListDataAPIURL |
   | --- | --- |
   | **Valor** |https://{nombre de la aplicación de API de capa de datos}.azurewebsites.net |
   | **Ejemplo** |https://todolistdataapi.azurewebsites.net |
4. Haga clic en **Guardar**.
   
    ![Haga clic en Guardar en Configuración de aplicaciones](./media/app-service-api-dotnet-get-started/asinportal.png)
   
    Cuando se ejecuta código de hello en Azure, este valor ahora invalidará la dirección URL de localhost de Hola que se encuentra en el archivo Web.config de Hola.

## <a name="test"></a>Prueba
1. En una ventana del explorador, examinar dirección URL de toohello de nivel intermedio nueva aplicación de API que acaba de crear para ToDoListAPI de Hola. Se puede obtener haciendo clic en la dirección URL de hello en la hoja principal de la aplicación hello API en el portal de Hola.
2. Agregar dirección URL de toohello "swagger" en la barra de direcciones del explorador de hello y, a continuación, presione ENTRAR. (Hola dirección URL es `http://{apiappname}.azurewebsites.net/swagger`.)
   
    muestra de explorador Hola Hola misma UI Swagger que vio anteriormente para ToDoListDataAPI, pero ahora `owner` no es un campo obligatorio para la operación de obtención de hello, como aplicación de API de nivel intermedio de hello realiza el envío esa aplicación de API de nivel de datos de valor toohello automáticamente. (Cuando hello tutoriales de autenticación, nivel intermedio Hola enviará Id. de usuario real para hello `owner` parámetro; para ahora lo es codificar un asterisco.)
3. Pruebe Hola método Get y hello otro toovalidate de métodos que Hola aplicación de API de nivel intermedio es llamar correctamente a nivel de datos de hello aplicación de API.
   
    ![Método Get de la interfaz de usuario de Swagger](./media/app-service-api-dotnet-get-started/midtierget.png)

## <a name="troubleshooting"></a>Solución de problemas
Si experimenta algún problema mientras lleva a cabo este tutorial, aquí se ofrecen ideas para solucionarlo:

* Asegúrese de que está usando la versión más reciente de Hola de hello [Azure SDK para .NET](http://go.microsoft.com/fwlink/?linkid=518003).
* Dos de los nombres de proyecto Hola son similar (ToDoListAPI, ToDoListDataAPI). Si no tiene el aspecto como se describe en las instrucciones de hello cuando se trabaja con un proyecto, asegúrese de que ha abierto el proyecto correcto Hola.
* Si está en una red corporativa y está tratando de toodeploy tooAzure servicio de aplicaciones a través de un firewall, asegúrese de que los puertos 443 y 8172 están abiertos para Web Deploy. Si no puede abrir estos puertos, puede usar otros métodos de implementación.  Vea [implementar su aplicación de servicio de aplicación tooAzure](../app-service-web/web-sites-deploy.md).
* Errores de "nombres de ruta deben ser únicos"--podría obtener estos si accidentalmente implementar aplicación de hello proyecto equivocado tooan API y su posterior implementación una tooit correcta de Hola. toocorrect, aplicación de API toohello volver a implementar hello proyecto correcto y en hello **configuración** ficha de hello **Publicar Web** asistente, seleccione **quitar archivos adicionales en destino**.

Una vez que su aplicación de API de ASP.NET que se ejecuta en el servicio de aplicación de Azure, puede que desee toolearn más acerca de las características de Visual Studio que simplifican la solución de problemas. Para más información sobre el registro o la depuración remota, entre otros temas, consulte [Solución de problemas de una aplicación web en Azure App Service con Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).

## <a name="next-steps"></a>Pasos siguientes
Ha visto cómo generar código de cliente para aplicaciones de API toodeploy API Web proyectos tooAPI las aplicaciones existentes y utilicen las aplicaciones de API de los clientes. NET. Hola tutorial siguiente de esta serie, se muestra cómo demasiado[usar CORS tooconsume API aplicaciones desde clientes de JavaScript](app-service-api-cors-consume-javascript.md).

Para obtener más información acerca de la generación de código de cliente, vea hello [Azure/AutoRest](https://github.com/azure/autorest) repositorio en GitHub.com. Para obtener ayuda con problemas al usar el cliente de hello generado, abra un [problema en el repositorio de hello AutoRest](https://github.com/azure/autorest/issues).

Si desea toocreate nuevos proyectos de aplicación de API desde el principio, usar hello **aplicación de API de Azure** plantilla.

![Plantilla Aplicación de API en Visual Studio](./media/app-service-api-dotnet-get-started/apiapptemplate.png)

Hola **aplicación de API de Azure** plantilla de proyecto está Hola equivalente toochoosing **vacía** ASP.NET 4.5.2 plantilla, haga clic en compatibilidad con API Web de tooadd de casilla de verificación de Hola y Hola Swashbuckle NuGet paquete de instalación. Además, la plantilla de hello agrega algunos creación de hello Swashbuckle configuración código diseñado tooprevent de operación de Swagger identificadores duplicados. Una vez que ha creado un proyecto de API App, puede implementarlo Hola de aplicación de API de tooan igual que hemos visto en este tutorial.

