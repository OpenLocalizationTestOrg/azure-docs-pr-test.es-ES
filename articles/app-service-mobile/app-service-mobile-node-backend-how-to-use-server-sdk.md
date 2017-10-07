---
title: "aaaHow toowork con el servidor back-end de Node.js Hola SDK para aplicaciones móviles | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toowork con Hola servidor back-end de Node.js SDK para aplicaciones de Mobile de servicio de aplicación de Azure."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: e7d97d3b-356e-4fb3-ba88-38ecbda5ea50
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2b1ea5fda6f6ca422b92fe29ff8d16bf035018d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-nodejs-sdk"></a>¿Cómo toouse Hola SDK de Node.js de aplicaciones móviles de Azure
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

Este artículo proporciona información detallada y ejemplos que muestran cómo toowork con un back-end de Node.js en aplicaciones de Mobile de servicio de aplicación de Azure.

## <a name="Introduction"></a>Introducción
Aplicaciones móviles de Azure aplicación de servicio proporciona acceso de datos de tooadd optimizadas para el móvil de capacidad de hello aplicación de API Web tooa web.  Hola SDK de aplicaciones de Mobile de servicio de aplicaciones de Azure se proporciona para aplicaciones web ASP.NET y Node.js.  Hola SDK proporciona hello las siguientes operaciones:

* Operaciones de tabla (lectura, inserción, actualización, eliminación) para el acceso a datos
* Operaciones API personalizadas

Ambas operaciones se incluyen para autenticación en todos los proveedores de identidades permitidos por el Servicio de aplicaciones de Azure, incluidos los proveedores de identidades sociales, como Facebook, Twitter, Google y Microsoft, así como Azure Active Directory para la identidad de empresa.

Puede encontrar ejemplos para cada caso de uso en hello [directorio de ejemplos en GitHub].

## <a name="supported-platforms"></a>Plataformas compatibles
Hola SDK de nodo de aplicaciones móviles de Azure admite hello que LTS actuales de la versión del nodo y versiones posteriores.  Redactar, versión más reciente de LTS de hello es v4.5.0 de nodo.  Aunque es posible que funcionen otras versiones de Node, no son compatibles.

Hola SDK de nodo de aplicaciones móviles de Azure es compatible con dos controladores de base de datos: hello nodo mssql controlador es compatible con SQL Azure y las instancias de SQL Server locales.  controlador de sqlite3 de Hello es compatible con las bases de datos de SQLite en una sola instancia.

### <a name="howto-cmdline-basicapp"></a>Cómo: crear un back-end de Node.js básico mediante la línea de comandos de Hola
Cada back-end de Node.js de aplicación móvil del Servicio de aplicaciones de Azure se inicia como una aplicación ExpressJS.  ExpressJS es hello más popular marco del servicio web disponible para Node.js.  Puede crear una aplicación [Express] básica de la forma siguiente:

1. En una ventana de comandos o de PowerShell, cree un directorio para el proyecto.

        mkdir basicapp
2. Ejecute la estructura del paquete de npm init tooinitialize Hola.

        cd basicapp
        npm init

    comando de Hello npm init solicita un conjunto de proyectos de hello tooinitialize preguntas.  Ver un resultado de ejemplo de Hola:

    ![salida de Hello npm init][0]
3. Instalar bibliotecas de express y aplicaciones móviles de azure de Hola de repositorio de npm Hola.

        npm install --save express azure-mobile-apps
4. Crear un app.js tooimplement hello básico móviles servidor de archivos.

        var express = require('express'),
            azureMobileApps = require('azure-mobile-apps');

        var app = express(),
            mobile = azureMobileApps();

        // Define a TodoItem table
        mobile.tables.add('TodoItem');

        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);

Esta aplicación crea una WebAPI móvil optimizada con un solo punto de conexión (`/tables/TodoItem`) que proporciona tooan de acceso no autenticado subyacente de almacén de datos SQL mediante un esquema dinámico.  Es adecuado para los siguientes inicios rápidos de la biblioteca de cliente:

* [Inicio rápido de cliente de Android]
* [Inicio rápido de cliente de Apache Cordova]
* [Inicio rápido de cliente de iOS]
* [Inicio rápido de cliente de Windows]
* [Inicio rápido de cliente de Xamarin.iOS]
* [Inicio rápido de cliente de Xamarin.Android]
* [Inicio rápido de cliente de Xamarin.Forms]

Puede encontrar código de hello para esta aplicación básica de hello [ejemplo basicapp en GitHub].

### <a name="howto-vs2015-basicapp"></a>Creación de un back-end de Node con Visual Studio de 2015
Visual Studio 2015 requiere una aplicación de extensión toodevelop Node.js en hello IDE.  toostart, instalar hello [Node.js Tools 1.1 para Visual Studio].  Una vez que se instalan hello Node.js Tools para Visual Studio, cree una aplicación de 4.x Express:

1. Abra hello **nuevo proyecto** diálogo (desde **archivo** > **New** > **proyecto...** ).
2. Expanda **Plantillas** > **JavaScript** > **Node.js**.
3. Seleccione hello **básica Node.js de Azure Express 4 aplicación**.
4. Rellene el nombre del proyecto de Hola.  Haga clic en *Aceptar*.

    ![Nuevo proyecto de Visual Studio de 2015][1]
5. Menú contextual hello **npm** nodo y seleccione **instalar nuevos paquetes de npm...** .
6. Puede que necesite toorefresh catálogo de npm Hola acerca de cómo crear su primera aplicación Node.js.  Haga clic en **Actualizar** si es necesario.
7. Escriba *aplicaciones móviles de azure* en el cuadro de búsqueda de Hola.  Haga clic en hello **azure-mobile-apps 2.0.0** del paquete, a continuación, haga clic en **Instalar paquete**.

    ![Instalar nuevos paquetes npm][2]
8. Haga clic en **Cerrar**.
9. Abra hello *app.js* tooadd compatibilidad para hello SDK de aplicaciones móviles de Azure de archivos.  En parte inferior de línea de 6 at Hola de biblioteca de hello requieren instrucciones, agregue Hola siguiente código:

        var bodyParser = require('body-parser');
        var azureMobileApps = require('azure-mobile-apps');

    En aproximadamente línea 27 después Hola otras instrucciones app.use, agregue Hola siguiente código:

        app.use('/users', users);

        // Azure Mobile Apps Initialization
        var mobile = azureMobileApps();
        mobile.tables.add('TodoItem');
        app.use(mobile);

    Guarde el archivo hello.
10. Ejecutar aplicación de hello localmente (Hola API se sirve en http://localhost:3000) o publicar tooAzure.

### <a name="create-node-backend-portal"></a>Cómo: crear un back-end de Node.js con hello portal de Azure
Puede crear un derecho de back-end de la aplicación móvil en hello [portal de Azure]. O bien puede seguir Hola siguientes pasos o crear un cliente y servidor juntos Hola después [crear una aplicación móvil](app-service-mobile-ios-get-started.md) tutorial. tutorial de Hello contiene una versión simplificada de estas instrucciones y es más adecuado para la prueba de proyectos de concepto.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

En hello *Introducción* hoja, en **crear una tabla API**, elija **Node.js** como su **idioma de back-end**.
Casilla de Hola para "**reconozco que esta acción sobrescribirá todo contenido de sitio.**", a continuación, haga clic en **TodoItem crear tabla**.

### <a name="download-quickstart"></a>Cómo: Descargar proyecto de código de la inicio rápido de hello Node.js back-end mediante Git
Cuando se crea un aplicación de Node.js móvil de back-end mediante el portal de hello **inicio rápido** hoja, se crea un proyecto de Node.js para usted y sitio tooyour implementado. Puede agregar tablas y las API y editar archivos de código de back-end de hello Node.js en el portal de Hola. También puede utilizar el proyecto de back-end de hello toodownload de herramientas de implementación distintos por lo que puede agregar o modificar las tablas y las API y luego volver a publicar proyecto Hola. Para obtener más información, consulte la [guía de implementación de Azure App Service]. Hello siguiente procedimiento usa un código de proyecto de inicio rápido de Git repositorio toodownload Hola.

1. Si aún no lo ha hecho, instale Git. Hola pasos necesarios tooinstall Git varían entre los sistemas operativos. Consulte el artículo de [instalación de Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) para obtener una guía sobre la instalación y las distribuciones específicas del sistema operativo.
2. Siga los pasos de hello en [Enable Hola repositorio de aplicación de servicio de aplicaciones](../app-service-web/app-service-deploy-local-git.md#Step3) tooenable repositorio de Git de hello para el sitio de back-end, que realiza una nota del nombre de usuario de implementación de Hola y la contraseña.
3. En la hoja de Hola para su aplicación móvil de back-end, tome nota de hello **dirección URL de clonación de Git** configuración.
4. Ejecute hello `git clone` comando mediante la dirección URL de clonación de Git hello, escribir la contraseña cuando sea necesario, como en el ejemplo siguiente:

        $ git clone https://username@todolist.scm.azurewebsites.net:443/todolist.git
5. Directorio de toolocal examinar, que en el anterior ejemplo de Hola es /todolist y tenga en cuenta que los archivos de proyecto se han descargado. Busque hello `todoitem.json` archivo Hola `/tables` directory.  Este archivo define permisos en la tabla.  También encontrará hello `todoitem.js` en el archivo hello mismo directorio, que define que operación CRUD secuencias de comandos para la tabla de Hola.
6. Después de realizar cambios tooproject archivos, ejecute hello siga los comandos tooadd, confirmar, a continuación, cargar el sitio de toohello de cambios:

        $ git commit -m "updated hello table script"
        $ git push origin master

    Cuando se agrega el nuevo proyecto de archivos toohello, primero debe hello tooexecute `git add .` comando.

sitio de Hola se vuelve a publicar cada vez que se inserta un nuevo conjunto de confirmaciones de toohello sitio.

### <a name="howto-publish-to-azure"></a>Cómo: publicar su tooAzure de back-end de Node.js
Microsoft Azure proporciona varios mecanismos para publicar su Node.js de aplicaciones de Azure aplicación Servicio móvil de back-end para Hola servicio de Azure.  Incluyen el uso de herramientas de implementación integradas en Visual Studio, herramientas de línea de comandos y opciones de implementación continua basadas en control de código fuente.  Para obtener más información sobre este tema, consulte la [guía de implementación de Azure App Service].

El Servicio de aplicaciones de Azure tiene instrucciones específicas para la aplicación de Node.js que usted debe revisar antes de realizar la implementación:

* Cómo demasiado[especificar Hola versión del nodo]
* Cómo demasiado[usar módulos de nodo]

### <a name="howto-enable-homepage"></a>Habilitación de una página de inicio para la aplicación
Muchas aplicaciones son una combinación de aplicaciones móviles y web y el marco de trabajo de hello ExpressJS permite toocombine los dos facetas.  A veces, sin embargo, es recomendable tooonly implemente una interfaz móvil.  Resulta útil tooprovide que un servicio de aplicaciones de aterrizaje página tooensure Hola está en funcionamiento.  Puede proporcionar su propia página de inicio o habilitar una de carácter temporal.  tooenable una página principal temporal, utilice Hola después de aplicaciones móviles de Azure de tooinstantiate:

    var mobile = azureMobileApps({ homePage: true });

Si solo desea que esta opción está disponible al desarrollar de forma local, puede agregar esta configuración tooyour `azureMobile.js` archivo.

## <a name="TableOperations"></a>Operaciones de tabla
Hello SDK de servidor de aplicaciones móviles de azure Node.js proporciona mecanismos tooexpose datos las tablas almacenadas en la base de datos de SQL de Azure como un WebAPI.  Se proporcionan cinco operaciones.

| Operación | Descripción |
| --- | --- |
| GET /tables/*nombredelatabla* |Obtener todos los registros en la tabla de Hola |
| GET /tables/*nombredelatabla*/:id |Obtener un registro específico en la tabla de Hola |
| POST /tables/*nombredelatabla* |Crear un registro en la tabla de Hola |
| PATCH /tables/*nombredelatabla*/:id |Actualizar un registro en la tabla Hola |
| DELETE /tables/*nombredelatabla*/:id |Eliminar un registro de la tabla de Hola |

Es compatible con esta WebAPI [OData] y extiende Hola tabla esquema toosupport [sincronización de datos sin conexión].

### <a name="howto-dynamicschema"></a>Definición de tablas con un esquema dinámico
Antes de usar una tabla, esta debe definirse.  Las tablas pueden definirse con un esquema estático (donde desarrollador Hola define columnas hello en el esquema de hello) o dinámicamente (donde hello SDK controla el esquema de hello en función de las solicitudes entrantes). Además, para desarrolladores de hello pueden controlar aspectos específicos de hello WebAPI mediante la adición de definición de toohello de código de Javascript.

Como práctica recomendada, se debe definir cada tabla en un archivo de Javascript en el directorio de tablas de hello, utilice las tablas de hello tables.import() método tooimport.  Extender la aplicación hello basic, se ajustaría archivo app.js de hello:

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Define hello database schema that is exposed
    mobile.tables.import('./tables');

    // Provide initialization of any tables that are statically defined
    mobile.tables.initialize().then(function () {
        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);
    });

Definir la tabla de hello en. / tables/TodoItem.js:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Additional configuration for hello table goes here

    module.exports = table;

Las tablas usan el esquema dinámico de forma predeterminada.  tooturn desactivar esquema dinámico globalmente, Establece configuración de la aplicación hello **MS_DynamicSchema** toofalse en hello portal de Azure.

Puede encontrar un ejemplo completo en hello [ejemplo de lista de tareas en GitHub].

### <a name="howto-staticschema"></a>Definición de tablas con un esquema estático
Puede definir explícitamente Hola columnas tooexpose a través de hello WebAPI.  Hola que SDK de Node.js de aplicaciones móviles de azure agrega automáticamente las columnas adicionales necesarias para la lista de toohello de sincronización de datos sin conexión que proporcione.  Por ejemplo, las aplicaciones de cliente de inicio rápido requieren una tabla con dos columnas: text (una cadena) y complete (un booleano).  
tabla de Hola se puede definir en la tabla definición JavaScript archivo hello (que se encuentra en el directorio de tablas de hello) como se indica a continuación:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    module.exports = table;

Si define las tablas estáticamente, también debe llamar esquema de base de datos de hello tables.initialize() método toocreate Hola durante el inicio.  Hola tables.initialize() método devuelve un [Promise] para que el servicio web de hello no sirve a las solicitudes antes de la base de datos de Hola que se está inicializando.

### <a name="howto-sqlexpress-setup"></a>Uso de SQL Express como almacén de datos de desarrollo en el equipo local
Hola Hola AzureMobile aplicaciones nodo SDK de aplicaciones móviles de Azure proporciona tres opciones para servir datos fuera del cuadro de hello: SDK proporciona tres opciones para enviar datos desde el principio de hello:

* Hola de uso **memoria** almacén de controladores de ejemplo tooprovide no persistentes
* Hola de uso **mssql** tooprovide controlador para el desarrollo de un almacén de datos SQL Express
* Hola de uso **mssql** controlador tooprovide un almacén de datos de la base de datos de SQL Azure para la producción

Hola SDK de Node.js de aplicaciones móviles de Azure usa hello [mssql Node.js paquete] tooestablish y utilizar una base de datos de SQL y tooboth de conexión SQL Express.  Este paquete requiere que habilite las conexiones TCP en la instancia de SQL Express.

> [!TIP]
> controlador de memoria de Hello no proporciona un conjunto completo de servicios para probar.  Si desea tootest el back-end de forma local, se recomienda usar Hola de un almacén de datos de SQL Express y Hola mssql controlador.
>
>

1. Descargue e instale [Microsoft SQL Server 2014 Express].  Asegúrese de que instalar SQL Server 2014 Express de hello con la edición de herramientas.  A menos que necesite explícitamente la compatibilidad con 64 bits, versión de 32 bits de hello consume menos memoria cuando se ejecuta.
2. Ejecute hello Administrador de configuración de SQL Server 2014.

   1. Expanda hello **configuración de red de SQL Server** nodo en el menú de árbol de la izquierda de Hola.
   2. Haga clic en **Protocolos para SQLEXPRESS**.
   3. Haga clic con el botón derecho en **TCP/IP** y seleccione **Habilitar**.  Haga clic en **Aceptar** en el cuadro de diálogo emergente de Hola.
   4. Haga clic con el botón derecho en **TCP/IP** y seleccione **Propiedades**.
   5. Haga clic en hello **direcciones IP** ficha.
   6. Buscar hello **IPAll** nodo.  Hola **el puerto TCP** , escriba **1433**.

          ![Configure SQL Express for TCP/IP][3]
   7. Haga clic en **Aceptar**.  Haga clic en **Aceptar** en el cuadro de diálogo emergente de Hola.
   8. Haga clic en **Services de SQL Server** en el menú de árbol de la izquierda de Hola.
   9. Haga clic con el botón derecho en **SQL Server (SQLEXPRESS)** y seleccione **Reiniciar**.
   10. Hola cerrar el Administrador de configuración de SQL Server 2014.
3. Ejecute hello SQL Server 2014 Management Studio y conéctese tooyour instancia de SQL Express local

   1. Haga clic en la instancia en el Explorador de objetos de Hola y seleccione **propiedades**
   2. Seleccione hello **seguridad** página.
   3. Asegúrese de hello **modo autenticación de Windows y SQL Server** está seleccionada
   4. Haga clic en **Aceptar**

          ![Configure SQL Express Authentication][4]
   5. Expanda **seguridad** > **inicios de sesión** Hola Explorador de objetos
   6. Haga clic con el botón derecho en **Inicios de sesión** y seleccione **Nuevo inicio de sesión...**
   7. Escriba un nombre de inicio de sesión.  Seleccione **Autenticación de SQL Server**.  Escriba una contraseña, a continuación, escriba Hola misma contraseña en **Confirmar contraseña**.  contraseña de Hello debe cumplir los requisitos de complejidad de Windows.
   8. Haga clic en **Aceptar**

          ![Add a new user tooSQL Express][5]
   9. Haga clic con el botón derecho en el nuevo inicio de sesión y seleccione **Propiedades**
   10. Seleccione hello **Roles de servidor** página
   11. Comprobar Hola cuadro siguiente toohello **dbcreator** rol de servidor
   12. Haga clic en **Aceptar**
   13. Cerrar Hola 2015 de SQL Server Management Studio

Asegurarse de que el nombre de usuario de registro hello y contraseña que has seleccionado.  Puede que tenga permisos o roles de servidor adicionales tooassign dependiendo de los requisitos de base de datos específica.

Hola aplicación Node.js lee hello **SQLCONNSTR_MS_TableConnectionString** variable de entorno para la cadena de conexión de Hola para esta base de datos.  Se puede establecer en el entorno.  Por ejemplo, puede usar esta variable de entorno tooset de PowerShell:

    $env:SQLCONNSTR_MS_TableConnectionString = "Server=127.0.0.1; Database=mytestdatabase; User Id=azuremobile; Password=T3stPa55word;"

Hola de acceso a la base de datos a través de una conexión TCP/IP y proporcionar un nombre de usuario y una contraseña para la conexión de Hola.

### <a name="howto-config-localdev"></a>Configuración del proyecto para el desarrollo local
Aplicaciones móviles de Azure lee un archivo JavaScript denominado *azureMobile.js* de sistema de archivos local Hola.  No usar este hello de tooconfigure archivo SDK de aplicaciones móviles de Azure en producción: usar la configuración de aplicación dentro de hello [portal de Azure] en su lugar.  Hola *azureMobile.js* archivo debe exportar un objeto de configuración.  valores de Hello más comunes son:

* Database Settings
* Configuración del registro de diagnóstico
* Configuración de CORS alternativa

Un ejemplo *azureMobile.js* archivo implementa Hola anterior sigue de configuración de base de datos:

    module.exports = {
        cors: {
            origins: [ 'localhost' ]
        },
        data: {
            provider: 'mssql',
            server: '127.0.0.1',
            database: 'mytestdatabase',
            user: 'azuremobile',
            password: 'T3stPa55word'
        },
        logging: {
            level: 'verbose'
        }
    };

Se recomienda que agregue *azureMobile.js* tooyour *.gitignore* archivo (o en otro control de código fuente Omitir archivo) tooprevent contraseñas se almacenen en la nube de Hola.  Configure siempre la configuración de producción en la configuración de la aplicación dentro de hello [portal de Azure].

### <a name="howto-appsettings"></a>Configuración de aplicaciones móviles
Mayoría de las configuraciones de hello *azureMobile.js* archivo tiene una configuración de aplicación equivalente en hello [portal de Azure].  Usar hello sigue lista tooconfigure la aplicación en la configuración de la aplicación:

| Configuración de aplicación | *azureMobile.js* | Descripción | Valores válidos |
|:--- |:--- |:--- |:--- |
| **MS_MobileAppName** |name |nombre de Hola de aplicación hello |cadena |
| **MS_MobileLoggingLevel** |logging.level |Nivel de registro mínimo de mensajes toolog |error, advertencia, información, detallado, depuración, absurdo |
| **MS_DebugMode** |debug |Habilitar o deshabilitar el modo de depuración |true, false |
| **MS_TableSchema** |data.schema |Nombre del esquema predeterminado para tablas SQL |cadena (valor predeterminado: dbo) |
| **MS_DynamicSchema** |data.dynamicSchema |Habilitar o deshabilitar el modo de depuración |true, false |
| **MS_DisableVersionHeader** |versión (conjunto tooundefined) |Deshabilita el encabezado X-ZUMO-Server-Version Hola |true, false |
| **MS_SkipVersionCheck** |skipversioncheck |Deshabilita la comprobación de la versión de Hola API de cliente |true, false |

tooset una configuración de aplicación:

1. Inicie sesión en toohello [portal de Azure].
2. Seleccione **todos los recursos** o **servicios de aplicaciones** , a continuación, haga clic en nombre de saludo de la aplicación móvil.
3. hoja de configuración de Hola se abre de forma predeterminada. En caso contrario, haga clic en **Configuración**.
4. Haga clic en **configuración de la aplicación** menú GENERAL Hola.
5. Desplácese toohello sección de configuración de la aplicación.
6. Si la aplicación si se establece ya existe, haga clic en valor de Hola de hello aplicación tooedit Hola valor.
7. Si la configuración de la aplicación no existe, escriba Hola configuración de la aplicación en el cuadro clave de Hola y el valor de hello en el cuadro del valor de Hola.
8. Cuando termine, haga clic en **Guardar**.

Si cambia la mayoría de las opciones de configuración de la aplicación habrá que reiniciar el servicio.

### <a name="howto-use-sqlazure"></a>Uso de Base de datos SQL como almacén de datos de producción
<!--- ALTERNATE INCLUDE - we can't use ../includes/app-service-mobile-dotnet-backend-create-new-service.md - slightly different semantics -->

El uso de Base de datos SQL de Azure como almacén de datos es idéntico en todos los tipos de aplicaciones del Servicio de aplicaciones de Azure. Si aún no lo ha hecho, siga estas toocreate pasos un aplicación móvil de back-end.

1. Inicie sesión en toohello [portal de Azure].
2. Hello parte superior izquierda de la ventana hello en, haga clic en hello **+ nuevo** botón > **Web y móvil** > **aplicación móvil**, a continuación, proporcione un nombre para su aplicación móvil de back-end.
3. Hola **grupo de recursos** cuadro, escriba Hola mismo nombre que su aplicación.
4. plan de servicio de aplicaciones predeterminado de Hello está seleccionado.  Si desea que toochange su plan de servicio de aplicaciones, puede hacerlo haciendo clic en el Plan de servicio de aplicación Hola > **+ crear nuevos**.  Proporcione un nombre del nuevo plan de servicio de aplicaciones de Hola y seleccione una ubicación adecuada.  Haga clic en el nivel de precios de Hola y seleccione un nivel de precios adecuado para el servicio de Hola. Seleccione **todas las ver** tooview más precios opciones, como **libre** y **Shared**.  Una vez haya seleccionado el nivel de precios, haga clic en hello **seleccione** botón.  Nuevo en hello **plan de servicio de aplicaciones** hoja, haga clic en **Aceptar**.
5. Haga clic en **Crear**. El aprovisionamiento de un back-end de la aplicación móvil puede tardar unos minutos.  Cuando se aprovisiona la aplicación móvil de hello back-end, el portal de hello abre hello **configuración** hoja para aplicación móvil de hello back-end.

Una vez creado el back-end de hello aplicación móvil, puede elegir tooeither conectarse un backend de la aplicación móvil de tooyour de base de datos SQL existente o crear una nueva base de datos SQL.  En esta sección, crearemos una nueva base de datos SQL.

> [!NOTE]
> Si ya tiene una base de datos en hello misma ubicación que el back-end de hello aplicación móvil, puede elegir en su lugar **usar una base de datos** y, a continuación, seleccione esa base de datos. no se recomienda el uso de Hola de una base de datos en una ubicación diferente debido a latencias más altas.
>
>

1. En hello nueva aplicación móvil back-end, haga clic en **configuración** > **aplicación móvil** > **datos** > **+ agregar**.
2. Hola **Agregar conexión de datos** hoja, haga clic en **base de datos de SQL - configurar los valores obligatorios** > **crear una nueva base de datos**.  Escriba el nombre de Hola de base de datos nueva Hola Hola **nombre** campo.
3. Haga clic en **Servidor**.  Hola **nuevo servidor** hoja, escriba un nombre de servidor único en hello **nombre del servidor** campo y proporcionar un adecuado **inicio de sesión de administrador de servidor** y **contraseña**.  Asegúrese de **server tooaccess de permitir que los servicios de azure** está activada.  Haga clic en **Aceptar**.

    ![Creación de una Base de datos SQL de Azure][6]
4. En hello **nueva base de datos** hoja, haga clic en **Aceptar**.
5. En hello **Agregar conexión de datos** hoja, seleccione **cadena de conexión**, escriba el inicio de sesión de Hola y la contraseña que proporcionó al crear la base de datos de Hola.  Si utiliza una base de datos existente, proporcione las credenciales de inicio de sesión de Hola para esa base de datos.  Cuando las especifique, haga clic en **Aceptar**.
6. En hello **Agregar conexión de datos** de nuevo, haga clic en la hoja **Aceptar** base de datos de toocreate Hola.

<!--- END OF ALTERNATE INCLUDE -->

Creación de base de datos de hello puede tardar unos minutos.  Hola de uso **notificaciones** progreso de hello toomonitor de área de implementación de Hola.  No se avanza hasta que la base de datos de Hola se ha implementado correctamente.  Una vez implementado correctamente, se crea una cadena de conexión para la instancia de base de datos SQL de hello en la configuración de la aplicación de back-end móvil.  Puede ver esta configuración de aplicación Hola **configuración** > **configuración de la aplicación** > **las cadenas de conexión**.

### <a name="howto-tables-auth"></a>Cómo: requerir la autenticación para acceso tootables
Si desea toouse autenticación del servicio de aplicación con el punto de conexión de hello tablas, debe configurar autenticación de servicio de aplicación Hola [portal de Azure] primero.  Para obtener más información acerca de cómo configurar la autenticación en un servicio de aplicaciones de Azure, revise hello Guía de configuración para el proveedor de identidades de hello piensa toouse:

* [¿Cómo tooconfigure autenticación de Azure Active Directory]
* [¿Cómo tooconfigure autenticación de Facebook]
* [¿Cómo tooconfigure autenticación de Google]
* [¿Cómo tooconfigure Microsoft Authentication]
* [¿Cómo tooconfigure autenticación de Twitter]

Cada tabla tiene una propiedad de access que puede ser usado toocontrol acceso toohello tabla.  Hola siguiente ejemplo muestra una tabla definida de forma estática con requiere autenticación.

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

propiedad de acceso de Hello puede tomar uno de estos tres valores

* *anónimo* indica que aplicación de cliente hello tooread datos sin autenticación
* *autenticado* indica que la aplicación de cliente de hello debe enviar un token de autenticación válido con la solicitud de Hola
* *disabled* indica que esta tabla está deshabilitada actualmente

Si la propiedad de acceso de hello no está definido, se permite el acceso no autenticado.

### <a name="howto-tables-getidentity"></a>Uso de notificaciones de autenticación con las tablas
Puede configurar varias notificaciones que se solicitan cuando se configura la autenticación.  Estas notificaciones normalmente no están disponibles a través de hello `context.user` objeto.  Sin embargo, se pueden recuperar mediante hello `context.user.getIdentity()` método.  Hola `getIdentity()` método devuelve una promesa que se resuelve el objeto tooan.  objeto de Hello es ordenado por el método de autenticación (facebook, google, twitter, cuenta de Microsoft o aad).

Por ejemplo, si establece la autenticación de Microsoft Account y notificación de direcciones de correo electrónico de solicitud hello, puede agregar registro de toohello de dirección de correo electrónico de hello con hello siguiente controlador de tabla:

    var azureMobileApps = require('azure-mobile-apps');

    // Create a new table definition
    var table = azureMobileApps.table();

    table.columns = {
        "emailAddress": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;
    table.access = 'authenticated';

    /**
    * Limit hello context query toothose records with hello authenticated user email address
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function queryContextForEmail(context) {
        return context.user.getIdentity().then((data) => {
            context.query.where({ emailAddress: data.microsoftaccount.claims.emailaddress });
            return context.execute();
        });
    }

    /**
    * Adds hello email address from hello claims toohello context item - used for
    * insert operations
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function addEmailToContext(context) {
        return context.user.getIdentity().then((data) => {
            context.item.emailAddress = data.microsoftaccount.claims.emailaddress;
            return context.execute();
        });
    }

    // Configure specific code when hello client does a request
    // READ - only return records belonging toohello authenticated user
    table.read(queryContextForEmail);

    // CREATE - add or overwrite hello userId based on hello authenticated user
    table.insert(addEmailToContext);

    // UPDATE - only allow updating of record belong toohello authenticated user
    table.update(queryContextForEmail);

    // DELETE - only allow deletion of records belong toohello authenticated uer
    table.delete(queryContextForEmail);

    module.exports = table;

toosee qué notificaciones están disponibles, use un Hola de tooview de explorador web `/.auth/me` punto de conexión del sitio.

### <a name="howto-tables-disabled"></a>Cómo: deshabilitar la tabla de toospecific operaciones de acceso
En suma tooappearing en la tabla de hello, propiedad de acceso de hello puede ser usado toocontrol las operaciones individuales.  Hay cuatro operaciones:

* *leer* es Hola obtener RESTful operación en la tabla de Hola
* *Insertar* es Hola POST RESTful operación en la tabla de Hola
* *actualizar* es operación PATCH RESTful de hello en la tabla de Hola
* *eliminar* es Hola eliminar RESTful operación en la tabla de Hola

Por ejemplo, podría desear tooprovide una tabla de solo lectura no autenticada:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Read-Only table - only allow READ operations
    table.read.access = 'anonymous';
    table.insert.access = 'disabled';
    table.update.access = 'disabled';
    table.delete.access = 'disabled';

    module.exports = table;

### <a name="howto-tables-query"></a>Cómo: ajustar Hola consulta que se usa con las operaciones de tabla
Un requisito común de las operaciones de tabla es una vista restringida de datos de hello tooprovide.  Por ejemplo, puede proporcionar una tabla que tiene una etiqueta con hello autenticado Id. de usuario de forma que sólo puede leer o actualizar sus propios registros.  Hola después de la definición de la tabla proporciona la siguiente funcionalidad:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define a static schema for hello table
    table.columns = {
        "userId": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;

    // Require authentication for this table
    table.access = 'authenticated';

    // Ensure that only records for hello authenticated user are retrieved
    table.read(function (context) {
        context.query.where({ userId: context.user.id });
        return context.execute();
    });

    // When adding records, add or overwrite hello userId with hello authenticated user
    table.insert(function (context) {
        context.item.userId = context.user.id;
        return context.execute();
    });

    module.exports = table;

Las operaciones que normalmente ejecutan una consulta tendrán una propiedad de consulta que se puede ajustar con una cláusula where. propiedad de la consulta de Hello es un [QueryJS] objeto que se puede procesar tooconvert usado un toosomething de consulta de OData que Hola datos back-end.  Para los casos de igualdad simple (por ejemplo, Hola anteriores), puede utilizarse un mapa. También puede agregar cláusulas SQL específicas:

    context.query.where('myfield eq ?', 'value');

### <a name="howto-tables-softdelete"></a>Configuración de una eliminación temporal en una tabla
La eliminación temporal no elimina realmente los registros.  En su lugar, marca como eliminados en base de datos de hello estableciendo Hola eliminar columna tootrue.  Hola SDK de aplicaciones móviles de Azure quita automáticamente los registros eliminados temporalmente de resultados a menos que Hola SDK del cliente móvil use IncludeDeleted().  tooconfigure eliminar una tabla de software, establezca hello `softDelete` propiedad en el archivo de definición de tabla de hello:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Turn on Soft Delete
    table.softDelete = true;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

Debe establecer un mecanismo para depurar registros, ya sea desde una aplicación cliente a través de un trabajo web, una función de Azure o mediante una API personalizada.

### <a name="howto-tables-seeding"></a>Inicialización de la base de datos con datos
Al crear una nueva aplicación, puede llamar a tooseed una tabla con datos.  Esto puede hacerse en archivo de JavaScript de definición de tabla de hello como sigue:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };
    table.seed = [
        { text: 'Example 1', complete: false },
        { text: 'Example 2', complete: true }
    ];

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

La propagación de datos solo se realiza cuando se crea la tabla de Hola por hello SDK de aplicaciones móviles de Azure.  Si la tabla Hola ya existe en la base de datos de hello, no se aplica ningún dato en tabla Hola.  Si un esquema dinámico está activado, se deducirá el esquema de datos de hello propagado.

Se recomienda que se llame explícitamente a hello `tables.initialize()` tabla de hello toocreate del método al servicio de hello comienza a ejecutarse.

### <a name="Swagger"></a>Habilitación de la compatibilidad con Swagger
Aplicaciones móviles del Servicio de aplicaciones de Azure incorpora compatibilidad con [Swagger] .  tooenable Swagger compatibilidad, instale primero Hola de interfaz de usuario swagger como una dependencia:

    npm install --save swagger-ui

Una vez instalado, puede habilitar la compatibilidad de Swagger en el constructor de hello aplicaciones móviles de Azure:

    var mobile = azureMobileApps({ swagger: true });

Probablemente solo desea tooenable compatibilidad de Swagger en las ediciones de desarrollo.  Puede hacerlo mediante la configuración de aplicación `NODE_ENV` :

    var mobile = azureMobileApps({ swagger: process.env.NODE_ENV !== 'production' });

Hello extremo de swagger se encuentra en http://*su sitio*.azurewebsites.net/swagger.  Puede tener acceso a hello Swagger de interfaz de usuario a través de hello `/swagger/ui` punto de conexión.  Si elige la autenticación de toorequire en toda la aplicación, Swagger genera un error.  Para obtener mejores resultados, elija tooallow sin autenticar solicitudes a través de Hola autenticación del servicio de aplicación de Azure / configuración de autorización, a continuación, controlar la autenticación mediante hello `table.access` propiedad.

También puede agregar hello Swagger opción tooyour `azureMobile.js` archivo si solo desea soporte técnico de Swagger al desarrollar de forma local.

## <a name="a-namepushpush-notifications"></a><a name="push">Notificaciones push
Aplicaciones móviles se integra con centros de notificaciones de Azure tooenable se toosend destinada toomillions de notificaciones de inserción de dispositivos en todas las plataformas principales. Mediante el uso de los centros de notificaciones, puede enviar inserción tooiOS de notificaciones, dispositivos Android y Windows. toolearn más información acerca de todo lo que pueden hacer con los centros de notificaciones, consulte [información general de los centros de notificación](../notification-hubs/notification-hubs-push-notification-overview.md).

### </a><a name="send-push"></a>Envío de notificaciones push
Hola siguiente código muestra cómo toouse Hola inserción objeto toosend una difusión push dispositivos iOS de tooregistered de notificación:

    // Create an APNS payload.
    var payload = '{"aps": {"alert": "This is an APNS payload."}}';

    // Only do hello push if configured
    if (context.push) {
        // Send a push notification using APNS.
        context.push.apns.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

Mediante la creación de un registro de plantilla de inserción de cliente hello, puede enviar en su lugar un toodevices de mensaje de inserción de plantilla en todas las plataformas admitidas. Hola el siguiente código muestra cómo toosend una notificación de plantilla:

    // Define hello template payload.
    var payload = '{"messageParam": "This is a template payload."}';

    // Only do hello push if configured
    if (context.push) {
        // Send a template notification.
        context.push.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }


### <a name="push-user"></a>Cómo: tooan de notificaciones de inserción de envío autentica usuarios mediante etiquetas
Cuando un usuario autenticado se registra para las notificaciones de inserción, una etiqueta de Id. de usuario se agrega automáticamente el registro de toohello. Mediante el uso de esta etiqueta, puede enviar inserción dispositivos de tooall notificaciones registrados por un usuario específico. Hello código siguiente obtiene el SID del usuario que realiza la solicitud de Hola Hola y envía un registro de dispositivos plantilla tooevery de notificación de inserción para que el usuario:

    // Only do hello push if configured
    if (context.push) {
        // Send a notification toohello current user.
        context.push.send(context.user.id, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

Cuando se registre para notificaciones push desde un cliente autenticado, asegúrese de que la autenticación se ha completado antes de intentar el registro.

## <a name="CustomAPI"></a> API personalizadas
### <a name="howto-customapi-basic"></a>Definición de una API personalizada
Además toohello de acceso a datos API a través de punto de conexión de hello /tables, aplicaciones móviles de Azure puede proporcionar cobertura de API personalizada.  Las API personalizadas se definen en un definiciones de tabla de toohello de manera similar y puede tener acceso a toda Hola facilidades, incluida la autenticación.

Si desea toouse autenticación de servicio de la aplicación con una API personalizada, debe configurar la autenticación del servicio de aplicación Hola [portal de Azure] primero.  Para obtener más información acerca de cómo configurar la autenticación en un servicio de aplicaciones de Azure, revise hello Guía de configuración para el proveedor de identidades de hello piensa toouse:

* [¿Cómo tooconfigure autenticación de Azure Active Directory]
* [¿Cómo tooconfigure autenticación de Facebook]
* [¿Cómo tooconfigure autenticación de Google]
* [¿Cómo tooconfigure Microsoft Authentication]
* [¿Cómo tooconfigure autenticación de Twitter]

Las API personalizadas se definen en gran parte Hola la misma manera que Hola API de tablas.

1. Crear un directorio **api** .
2. Crear un archivo de JavaScript de la definición de API en hello **api** directory.
3. Use Hola importación método tooimport Hola **api** directory.

Aquí es la definición de la api de prototipo Hola basada en hello basic aplicación ejemplo que hemos usado anteriormente.

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

Veamos un ejemplo de API que devuelven la fecha de servidor de hello con hello *Date.now()* método.  Este es el archivo de hello api/date.js:

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };

    module.exports = api;

Cada parámetro es uno de hello RESTful verbos estándar: GET, POST, PATCH o DELETE.  método Hello es un estándar [ExpressJS Middleware] función que envía el resultado de hello necesario.

### <a name="howto-customapi-auth"></a>Cómo: solicitar autenticación para la API de acceso tooa personalizada
SDK de aplicaciones móviles Azure implementa la autenticación en hello igual en el punto de conexión de hello las tablas y las API personalizadas.  Para agregar autenticación toohello API desarrollado en la sección anterior de hello, agregue un **acceso** propiedad:

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };
    // All methods must be authenticated.
    api.access = 'authenticated';

    module.exports = api;

También puede especificar la autenticación en operaciones específicas:

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        }
    };
    // hello GET methods must be authenticated.
    api.get.access = 'authenticated';

    module.exports = api;

Hello mismo token que se utiliza para el punto de conexión de hello tablas debe utilizarse para las API personalizadas que requiera autenticación.

### <a name="howto-customapi-auth"></a>Control de cargas de archivos de gran tamaño
SDK de aplicaciones de Azure Mobile usa hello [cuerpo analizador middleware](https://github.com/expressjs/body-parser) tooaccept y descodificar el contenido del cuerpo en el envío.  Puede configurar previamente cargas de archivos mayores de cuerpo analizador tooaccept:

    var express = require('express'),
        bodyParser = require('body-parser'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Set up large body content handling
    app.use(bodyParser.json({ limit: '50mb' }));
    app.use(bodyParser.urlencoded({ limit: '50mb', extended: true }));

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

archivo Hello es codificados antes de la transmisión en base 64.  Esto aumenta el tamaño de Hola de carga real de hello (y Hola, por lo que debe tener en cuenta para el tamaño).

### <a name="howto-customapi-sql"></a>Ejecución de instrucciones SQL personalizadas
Hola SDK de aplicaciones móviles de Azure permite acceso toohello todo contexto a través del objeto de solicitud de hello, permitiéndole tooexecute parámetros proveedor de datos definidos de toohello de instrucciones SQL fácilmente:

    var api = {
        get: function (request, response, next) {
            // Check for parameters - if not there, pass on tooa later API call
            if (typeof request.params.completed === 'undefined')
                return next();

            // Define hello query - anything that can be handled by hello mssql
            // driver is allowed.
            var query = {
                sql: 'UPDATE TodoItem SET complete=@completed',
                parameters: [{
                    completed: request.params.completed
                }]
            };

            // Execute hello query.  hello context for Azure Mobile Apps is available through
            // request.azureMobile - hello data object contains hello configured data provider.
            request.azureMobile.data.execute(query)
            .then(function (results) {
                response.json(results);
            });
        }
    };

    api.get.access = 'authenticated';
    module.exports = api;

## <a name="Debugging"></a>Depuración, y tablas y API fáciles
### <a name="howto-diagnostic-logs"></a>Depuración, diagnóstico y solución de problemas de Mobile Apps de Azure
Hola servicio de aplicaciones de Azure proporciona varias depuración y solución de problemas de técnicas para aplicaciones Node.js.
Consulte toohello después tooget artículos iniciado en el back-end de Node.js Mobile de solución de problemas:

* [Supervisión de Aplicaciones web en el Servicio de aplicaciones de Azure]
* [Habilitación del registro de diagnóstico para aplicaciones web en el Servicio de aplicaciones de Azure]
* [Solución de problemas del Servicio de aplicaciones de Azure en Visual Studio]

Las aplicaciones Node.js tienen acceso tooa amplia gama de herramientas de registro de diagnóstico.  Internamente, se usa el SDK de Node.js de aplicaciones móviles de Azure hello [Winston] para el registro de diagnóstico.  El registro se habilita automáticamente al habilitar el modo de depuración o establecer hello **MS_DebugMode** tootrue de configuración de aplicación Hola [portal de Azure]. Registros generados aparecen en registros de diagnóstico de hello en hello [portal de Azure].

### <a name="in-portal-editing"></a><a name="work-easy-tables"></a>Cómo: trabajar con tablas fácil Hola portal de Azure
Tablas fácil en el portal de hello le permiten crear y trabajar con el derecho de tablas en el portal de Hola. Incluso puede editar las operaciones de tabla mediante Hola Editor de aplicación de servicio.

Al hacer clic en **Tablas fáciles** en la configuración del sitio del back-end, puede agregar, modificar o eliminar una tabla. También puede ver datos de tabla de Hola.

![Trabajo con tablas fáciles](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-tables.png)

Hello comandos siguientes están disponibles en la barra de comandos de Hola para una tabla:

* **Cambiar los permisos** : Hola permiso de lectura de modificación, inserciones, actualizaciones y operaciones delete en la tabla de Hola.
  Las opciones son tooallow el acceso anónimo, autenticación toorequire o toodisable todos los accesos toohello operación.
* **Editar script** -se abre el archivo de script de Hola para la tabla de Hola Hola Editor de aplicación de servicio.
* **Administrar el esquema** : agregar o eliminar columnas o cambiar el índice de la tabla de Hola.
* **Borrar tabla** -trunca una tabla existente se elimina todas las filas de datos, pero deja el esquema de hello sin cambios.
* **Eliminar filas** : elimina filas individuales de datos.
* **Ver los registros de streaming** -conecta toohello servicio de registro para el sitio de streaming.

### <a name="work-easy-apis"></a>Cómo: trabajar con las API sencilla de hello portal de Azure
API sencilla en el portal de hello permiten crear y trabajar con derecho personalizado de las API en el portal de Hola. Puede editar los scripts de API con hello Editor de aplicación de servicio.

Al hacer clic en **API fáciles** en la configuración del sitio del back-end, puede agregar un nuevo punto de conexión de API personalizado, así como modificar o eliminar un punto de conexión de API existente.

![Trabajo con API fáciles](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-apis.png)

En el portal de hello, puede cambiar los permisos de acceso de Hola para una acción determinada de HTTP, editar el archivo de script de API de hello en el Editor del servicio de aplicación o ver registros de streaming de Hola.

### <a name="online-editor"></a>Cómo: editar código de hello Editor de aplicación de servicio
Hola portal de Azure le permite modificar los archivos de script de back-end de Node.js en hello Editor de aplicación de servicio sin tener que descargar el equipo local de hello proyecto tooyour. archivos de script tooedit en el editor de hello en línea:

1. En la hoja de back-end de la aplicación móvil, haga clic en **Toda la configuración** > **Tablas fáciles** o **API fáciles**, haga clic en una tabla o API y luego en **Editar script**. se abre el archivo de script de Hola en hello Editor de aplicación de servicio.

    ![Editor del Servicio de aplicaciones](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-visual-studio-editor.png)
2. Hacer que el archivo de código de toohello de cambios en el editor en línea hello. Los cambios se guardan automáticamente a medida que se escriben.

<!-- Images -->
[0]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/npm-init.png
[1]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-new-project.png
[2]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-install-npm.png
[3]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-config.png
[4]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-authconfig.png
[5]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-newuser-1.png
[6]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/dotnet-backend-create-db.png

<!-- URLs -->
[Inicio rápido de cliente de Android]: app-service-mobile-android-get-started.md
[Inicio rápido de cliente de Apache Cordova]: app-service-mobile-cordova-get-started.md
[Inicio rápido de cliente de iOS]: app-service-mobile-ios-get-started.md
[Inicio rápido de cliente de Xamarin.iOS]: app-service-mobile-xamarin-ios-get-started.md
[Inicio rápido de cliente de Xamarin.Android]: app-service-mobile-xamarin-android-get-started.md
[Inicio rápido de cliente de Xamarin.Forms]: app-service-mobile-xamarin-forms-get-started.md
[Inicio rápido de cliente de Windows]: app-service-mobile-windows-store-dotnet-get-started.md
[HTML/Javascript Client QuickStart]: app-service-html-get-started.md
[sincronización de datos sin conexión]: app-service-mobile-offline-data-sync.md
[¿Cómo tooconfigure autenticación de Azure Active Directory]: app-service-mobile-how-to-configure-active-directory-authentication.md
[¿Cómo tooconfigure autenticación de Facebook]: app-service-mobile-how-to-configure-facebook-authentication.md
[¿Cómo tooconfigure autenticación de Google]: app-service-mobile-how-to-configure-google-authentication.md
[¿Cómo tooconfigure Microsoft Authentication]: app-service-mobile-how-to-configure-microsoft-authentication.md
[¿Cómo tooconfigure autenticación de Twitter]: app-service-mobile-how-to-configure-twitter-authentication.md
[guía de implementación de Azure App Service]: ../app-service-web/web-sites-deploy.md
[Supervisión de Aplicaciones web en el Servicio de aplicaciones de Azure]: ../app-service-web/web-sites-monitor.md
[Habilitación del registro de diagnóstico para aplicaciones web en el Servicio de aplicaciones de Azure]: ../app-service-web/web-sites-enable-diagnostic-log.md
[Solución de problemas del Servicio de aplicaciones de Azure en Visual Studio]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md
[especificar Hola versión del nodo]: ../nodejs-specify-node-version-azure-apps.md
[usar módulos de nodo]: ../nodejs-use-node-modules-azure-apps.md
[Create a new Azure App Service]: ../app-service-web/
[azure-mobile-apps]: https://www.npmjs.com/package/azure-mobile-apps
[Express]: http://expressjs.com/
[Swagger]: http://swagger.io/

[portal de Azure]: https://portal.azure.com/
[OData]: http://www.odata.org
[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[ejemplo basicapp en GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[ejemplo de lista de tareas en GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[directorio de ejemplos en GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Node.js Tools 1.1 para Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node.js paquete]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html
[Winston]: https://github.com/winstonjs/winston
