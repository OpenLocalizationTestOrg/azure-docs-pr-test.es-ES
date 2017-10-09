---
title: "aaaCreate NET WebJob en el servicio de aplicación de Azure | Documentos de Microsoft"
description: "Cree una aplicación de varios niveles utilizando ASP.NET MVC y Azure. Hola front-end ejecuta en una aplicación web en el servicio de aplicación de Azure y Hola back-end se ejecuta como un trabajo Web. aplicación Hello usa Entity Framework, base de datos de SQL y las colas de almacenamiento de Azure y blobs."
services: app-service
documentationcenter: .net
author: tdykstra
manager: erikre
editor: mollybos
ms.assetid: 99cb9917-483a-45f8-a98d-07d19c68c753
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/14/2017
ms.author: glenga
ms.openlocfilehash: d92fc4b81cc0d58f8e900f257e747af56d32b911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-net-webjob-in-azure-app-service"></a>Creación de un WebJob .NET en el Servicio de aplicaciones de Azure
Este tutorial muestra cómo toowrite código para una aplicación de ASP.NET MVC 5 multinivel simple que usa hello [SDK de WebJobs](websites-dotnet-webjobs-sdk.md).

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

Hola propósito de hello [SDK de WebJobs](websites-webjobs-resources.md) es código de hello toosimplify que se escribe para las tareas comunes que puede realizar un trabajo Web, como procesamiento de imágenes, procesamiento de colas, agregación de RSS, mantenimiento del archivo y enviar mensajes de correo electrónico. Hola SDK de WebJobs tiene características integradas para trabajar con el almacenamiento de Azure y Bus de servicio, para programar tareas y control de errores y para muchos otros escenarios comunes. Además, ha diseñado toobe extensible y no hay un [repositorio de código abierto para las extensiones](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).

aplicación de ejemplo de Hola es un tablón de anuncios publicitarios. Los usuarios pueden cargar imágenes para anuncios y un proceso de back-end convierte Hola imágenes toothumbnails. página de lista de anuncios de Hola muestra vistas en miniatura de Hola y página de detalles del anuncio de Hola muestra la imagen a tamaño completo Hola. A continuación se muestra una captura de pantalla:

![Ad list](./media/websites-dotnet-webjobs-sdk-get-started/list.png)

Esta aplicación de ejemplo funciona con [colas de Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) y [blobs de Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage). Hello tutorial le mostrará cómo toodeploy Hola aplicación demasiado[servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714) y [base de datos de SQL Azure](http://msdn.microsoft.com/library/azure/ee336279).

## <a id="prerequisites"></a>Requisitos previos
Hello tutorial se supone que ya sabe cómo toowork con [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) proyectos de Visual Studio.

tutorial de Hello escribió originalmente para Visual Studio 2013, pero puede utilizarse con las versiones posteriores de Visual Studio. Si está utilizando Visual Studio 2015 o 2017, tome nota antes de ejecutar la aplicación hello localmente, debe cambiar hello `Data Source` forma parte de la cadena de conexión de SQL Server LocalDB hello en los archivos Web.config y App.config Hola de `Data Source=(localdb)\v11.0` demasiado`Data Source=(LocalDb)\MSSQLLocalDB`.

> [!NOTE]
> <a name="note"></a>Debe tener una cuenta de Azure toocomplete este tutorial:
>
> * También puede [abrir una cuenta de Azure de forma gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): obtenga créditos que puede usar tootry los servicios de Azure de pago e incluso después de que se utilizan, puede mantener la cuenta de hello y usar los servicios de Azure gratuitos, como sitios Web. Nunca se cargará su tarjeta de crédito a menos que cambiar la configuración y pida toobe cobrado explícitamente.
> * Puede [activar Crédito mensual de Azure para suscriptores de Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): su suscripción le proporciona crédito todos los meses que puede usar con servicios de Azure de pago.
>
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
>
>

## <a id="learn"></a>Temas que se abordarán
Hola tutorial le muestra cómo hello toodo siguientes tareas:

* Habilitar el equipo de desarrollo de Azure mediante la instalación de hello Azure SDK (solo para usuarios de 2015 y Visual Studio 2013).
* Cree un proyecto de aplicación de consola que se implementa automáticamente como un trabajo Web de Azure al implementar un proyecto web asociado Hola.
* Probar un back-end de SDK de WebJobs localmente en el equipo de desarrollo de Hola.
* Publicar una aplicación con una aplicación web de trabajos Web back-end tooa en el servicio de aplicaciones.
* Cargar archivos y almacenarlos en hello servicio Blob de Azure.
* Usar hello toowork de SDK de WebJobs de Azure con blobs y colas de almacenamiento de Azure.

## <a id="contosoads"></a>Arquitectura de la aplicación
aplicación de ejemplo de Hola utiliza hello [centrada en la cola de trabajo patrón](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff carga de trabajo de hello intensiva de CPU de creación de proceso de miniaturas tooa back-end.

aplicación Hello almacena anuncios en una base de datos SQL con tablas de hello toocreate Entity Framework Code First y acceder a los datos de Hola. Para cada anuncio de la base de datos de hello almacena dos direcciones URL: uno para la imagen a tamaño completo hello y otro para la miniatura de Hola.

![Ad table](./media/websites-dotnet-webjobs-sdk-get-started/adtable.png)

Cuando un usuario carga una imagen, la aplicación web de hello almacena la imagen de hello en un [blobs de Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), y almacena información de anuncios de Hola en base de datos de hello con una dirección URL que señala toohello blob. Hola al mismo tiempo, escribe un tooan mensaje cola de Azure. En un proceso de back-end que se ejecuta como un trabajo Web de Azure, SDK de WebJobs Hola sondea Hola si hay mensajes nuevos. Cuando aparezca un mensaje nuevo, Hola trabajo Web crea una vista en miniatura de esa imagen y actualizaciones Hola campo de base de datos de dirección URL en miniatura para que ad. Éste es un diagrama que muestra cómo interactúan las partes de Hola de aplicación hello:

![Contoso Ads architecture](./media/websites-dotnet-webjobs-sdk-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]  
instrucciones del tutorial Hola aplican tooAzure SDK para .NET 2.7.1 o una versión posterior.

## <a id="storage"></a>Creación de una cuenta de almacenamiento de Azure
Una cuenta de almacenamiento de Azure proporciona recursos para almacenar datos de cola y blob en la nube de Hola. También se usa por hello datos de registro de toostore de SDK de WebJobs para el panel de Hola.

En una aplicación real, normalmente crea cuentas independientes para los datos de aplicación frente a los datos de registro, y cuentas diferentes para los datos de prueba frente a los datos de producción. En este tutorial, usará solamente una cuenta.

1. Abra hello **Explorador de servidores** ventana de Visual Studio.
2. Menú contextual hello **Azure** nodo y, a continuación, haga clic en **conectar tooMicrosoft suscripción de Azure...** .
   
   ![Conectar tooAzure](./media/websites-dotnet-webjobs-sdk-get-started/connaz.png)

3. Inicie sesión con sus credenciales de Azure.
4. Haga clic en **almacenamiento** en Hola nodos de Azure y, a continuación, haga clic en **crear cuenta de almacenamiento**.
   
   ![Crear cuenta de almacenamiento](./media/websites-dotnet-webjobs-sdk-get-started/createstor.png)
   
5. Hola **crear cuenta de almacenamiento** cuadro de diálogo, escriba un nombre para la cuenta de almacenamiento de Hola.

    debe ser el nombre de Hello debe ser único (ninguna otra cuenta de almacenamiento de Azure puede tener Hola mismo nombre). Si nombre hello especificado ya está en uso, obtendrá un toochange posibilidad.

    Hola tooaccess de dirección URL será la cuenta de almacenamiento *{name}*. core.windows.net.
6. Conjunto hello **región o grupo de afinidad** tooyou de lista desplegable toohello región más cercana.

    Esta configuración especifica el centro de datos de Azure que va a almacenar la cuenta de almacenamiento. En este tutorial, la opción que elija no tendrá mucha repercusión. Sin embargo, para una aplicación web de producción, desea que el servidor web y la toobe de la cuenta de almacenamiento en hello mismo latencia toominimize de región y datos cargos de salida. aplicación web de Hello (que creará más adelante) Centro de datos debe ser lo más parecida posibles exploradores toohello acceso a aplicación web de hello en la latencia de toominimize de orden.
7. Conjunto hello **replicación** lista desplegable lista demasiado**redundancia local**.

    Replicación geográfica está habilitada para una cuenta de almacenamiento, contenido de hello almacenado replicada tooa centro de datos secundario tooenable conmutación por error toothat ubicación es en el caso de un desastre importante en la ubicación principal de Hola. La replicación geográfica puede suponer costes adicionales. Para las cuentas de prueba y desarrollo, generalmente no desea toopay para la replicación geográfica. Para obtener más información, consulte [Creación, administración o eliminación de una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md).
8. Haga clic en **Crear**.

    ![New storage account](./media/websites-dotnet-webjobs-sdk-get-started/newstorage.png)

## <a id="download"></a>Descargar la aplicación hello
1. Descargue y descomprima hello [completado solución](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).
2. Inicie Visual Studio.
3. De hello **archivo** menú elija **Abrir > proyecto/solución**, desplácese toowhere descargó solución hello y, a continuación, abra el archivo de solución de Hola.
4. Presione la solución CTRL + MAYÚS + B toobuild Hola.

    De forma predeterminada, Visual Studio restaurará automáticamente contenido del paquete NuGet hello, que no se incluyó en hello *.zip* archivo. Si no se restauran los paquetes de saludo, instálelos manualmente va toohello **administrar paquetes de NuGet para la solución** cuadro de diálogo y haga clic en hello **restaurar** situado en la parte superior de hello derecha.
5. En **el Explorador de soluciones**, asegúrese de que **ContosoAdsWeb** está seleccionado como proyecto de inicio de Hola.

## <a id="configurestorage"></a>Configurar la cuenta de almacenamiento de toouse de aplicación Hola
1. Abra la aplicación hello *Web.config* archivo hello ContosoAdsWeb proyecto.

    archivo Hello contiene una cadena de conexión de SQL y una cadena de conexión de almacenamiento de Azure para trabajar con blobs y colas.

    cadena de conexión SQL Hola señala tooa [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) base de datos.

    cadena de conexión de almacenamiento de Hello es un ejemplo que tiene los marcadores de posición de clave de acceso y nombre de la cuenta del almacenamiento Hola. Va a reemplazar con una cadena de conexión que tiene el nombre de Hola y la clave de la cuenta de almacenamiento.  

    ```
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
        <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
    </connectionStrings>
    ```
    cadena de conexión de almacenamiento de Hola se denomina AzureWebJobsStorage porque es Hola Hola de nombre de que usa el SDK de WebJobs forma predeterminada. Hola mismo nombre se utiliza aquí por lo que tiene valor de cadena de conexión solo tooset Hola entorno de Azure.
2. En **Explorador de servidores**, haga clic en la cuenta de almacenamiento en hello **almacenamiento** nodo y, a continuación, haga clic en **propiedades**.

    ![Haga clic en propiedades de cuenta de almacenamiento](./media/websites-dotnet-webjobs-sdk-get-started/storppty.png)
3. Hola **propiedades** ventana, haga clic en **claves de la cuenta de almacenamiento**y, a continuación, haga clic en el botón de puntos suspensivos Hola.

    ![Claves de cuenta de almacenamiento](./media/websites-dotnet-webjobs-sdk-get-started/stor-account-keys.png)
4. Hola copia **cadena de conexión**.

    ![Cuadro de diálogo Claves de cuenta de almacenamiento](./media/websites-dotnet-webjobs-sdk-get-started/cpak.png)
5. Reemplace la cadena de conexión de almacenamiento de Hola Hola *Web.config* archivo con la cadena de conexión de Hola que acaba de copiar. Asegúrese de que seleccionar todos los elementos dentro de comillas de hello pero sin incluir las comillas de hello antes de pegar.
6. Abra hello *App.config* archivo hello ContosoAdsWebJob proyecto.

    Este archivo tiene dos cadenas de conexión de almacenamiento, una para los datos de aplicación y otra para registro. Puede utilizar cuentas de almacenamiento independientes para los datos de aplicación y el registro, y usar [varias cuentas de almacenamiento para datos](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs). Para este tutorial, usará una única cuenta de almacenamiento. las cadenas de conexión de Hello tienen marcadores de posición para claves de cuenta de almacenamiento de Hola.

    ```
    <configuration>
        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;"/>
    </connectionStrings>
        <startup>
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    </configuration>

    ```

    De forma predeterminada, Hola SDK de WebJobs busca las cadenas de conexión denominado AzureWebJobsStorage y AzureWebJobsDashboard. Como alternativa, también puede [almacenar la cadena de conexión de hello pero que desee y pasa de forma explícita toohello `JobHost` objeto](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).
7. Reemplace ambas cadenas de conexión de almacenamiento con la cadena de conexión de Hola que copió anteriormente.
8. Guarde los cambios.

## <a id="run"></a>Ejecutar la aplicación hello localmente
1. toostart hello web front-end de la aplicación hello, presione CTRL + F5.

    explorador predeterminado de Hello abre la página de inicio de toohello. (proyecto de hello web se ejecuta ya se ha hecho proyecto de inicio de Hola.)

    ![Página principal de Contoso Ads](./media/websites-dotnet-webjobs-sdk-get-started/home.png)
2. toostart Hola trabajo Web back-end de la aplicación hello, haga clic en proyecto de ContosoAdsWebJob de hello en **el Explorador de soluciones**y, a continuación, haga clic en **depurar** > **Iniciar nueva instancia** .

    Una ventana de la aplicación de consola se abre y muestra mensajes de registro que indica el objeto de trabajos Web SDK JobHost Hola inició toorun.

    ![Ventana de la aplicación de consola que muestra ese Hola de back-end se ejecuta](./media/websites-dotnet-webjobs-sdk-get-started/backendrunning.png)
3. En el explorador, haga clic en **Crear un anuncio**.
4. Escriba algunos datos de prueba, seleccione un tooupload de imagen y, a continuación, haga clic en **crear**.

    ![Create page](./media/websites-dotnet-webjobs-sdk-get-started/create.png)

    aplicación Hello queda toohello página de índice, pero no muestra una vista en miniatura para nuevo anuncio de Hola dado que el procesamiento no se ha realizado.

    Mientras tanto, después de una breve espera un mensaje de registro en la ventana de aplicación de consola de hello muestra que un mensaje de la cola se recibió y se ha procesado.

    ![Ventana de la aplicación de consola que muestra que se ha procesado un mensaje de cola](./media/websites-dotnet-webjobs-sdk-get-started/backendlogs.png)
5. Después de ver Hola registrar mensajes en la ventana de aplicación de consola de hello, actualizar vista en miniatura de hello índice página toosee Hola.

    ![Página de índice](./media/websites-dotnet-webjobs-sdk-get-started/list.png)
6. Haga clic en **detalles** para la imagen a tamaño completo ad toosee Hola.

    ![Details page](./media/websites-dotnet-webjobs-sdk-get-started/details.png)

Ha estado ejecutando aplicación hello en el equipo local y que está usando un SQL Server, base de datos ubicada en el equipo, pero está trabajando con las colas y blobs de hello en la nube. Hola pasos de la sección ejecutaremos aplicación hello en nube de hello, con una base de datos en la nube, así como en la nube blobs y colas.  

## <a id="runincloud"></a>Ejecutar la aplicación hello en la nube de Hola
Deberá llevar a cabo Hola tras la aplicación de hello toorun de pasos en la nube de hello:

* Implementar aplicaciones de tooWeb. Visual Studio crea automáticamente una aplicación web en el Servicio de aplicaciones y una instancia de Base de datos SQL.
* Configurar toouse de aplicación web de hello en su cuenta de almacenamiento y la base de datos de SQL Azure.

Después de haber creado algunos anuncios mientras se ejecuta en la nube de hello, podrá ver HOLA hola de toosee de panel de SDK de WebJobs enriquecido de características tiene toooffer de supervisión.

### <a name="deploy-tooweb-apps"></a>Implementar aplicaciones de tooWeb

1. Cierre el Explorador de Hola y ventana de aplicación de consola de Hola.
2. Siga los pasos de Hola Hola [publicar tooAzure con base de datos SQL](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) sección.
3. Después de completar los pasos para implementar hello, continúe con las tareas restantes de hello en este artículo.

### <a name="configure-hello-web-app-toouse-your-azure-sql-database-and-storage-account"></a>Configurar toouse de aplicación web de hello su cuenta de almacenamiento y la base de datos de SQL Azure
Es una práctica recomendada de seguridad demasiado[evitar colocar información confidencial como cadenas de conexión en archivos que se almacenan en repositorios de código de origen](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets). Azure proporciona una manera toodo: puede establecer la cadena de conexión y otros valores de configuración en hello entorno de Azure y API de configuración de ASP.NET recoge estos valores de automáticamente cuando la aplicación hello se ejecuta en Azure. Puede establecer estos valores en Azure mediante **Explorador de servidores**, Hola Portal de Azure, Windows PowerShell, u Hola interfaz de línea de comandos entre plataformas. Para obtener más información, consulte [Funcionamiento de las cadenas de aplicación y de las cadenas de conexión](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).

En esta sección, utilice **Explorador de servidores** tooset valores de cadena de conexión en Azure.

1. En el **Explorador de servidores**, haga clic con el botón derecho en la aplicación web en **Azure > App Service > {su grupo de recursos}** y luego haga clic en **Ver configuración**.

    Hola **aplicación Web de Azure** ventana se abre en hello **configuración** ficha.
2. Cambiar el nombre de Hola de nombre de toohello de cadena de conexión de hello DefaultConnection elegido al configurar la base de datos SQL de Hola Hola [publicar tooAzure con base de datos SQL](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) artículo.

    Azure crea automáticamente esta cadena de conexión cuando se creó la aplicación web de hello con una base de datos asociada, por lo que ya tiene valor de cadena de conexión adecuada de Hola. Está cambiando simplemente Hola nombre toowhat que busca el código.
3. Agregue dos cadenas de conexión nuevas, llamadas AzureWebJobsStorage y AzureWebJobsDashboard. Establecer tipo de base de datos de hello demasiado**personalizado**y el mismo valor que usó anteriormente para hello conjunto Hola conexión cadena valor toohello *Web.config* y *App.config* archivos. (Asegúrese de incluir la cadena de conexión completa de hello, no solo tecla de acceso de hello y no incluya comillas hello).

    Estas cadenas de conexión se utilizan por hello SDK de WebJobs, uno para los datos de aplicación y otro para el registro. Como se vio anteriormente, Hola de datos de aplicación también se usa código de hello web front-end.
4. Haga clic en **Guardar**.

    ![Cadenas de conexión en el Portal de Azure](./media/websites-dotnet-webjobs-sdk-get-started/azconnstr.png)
5. En **Explorador de servidores**, haga clic en la aplicación web de hello y, a continuación, haga clic en **detener**.
6. Cuando se detenga la aplicación web de hello, haga clic en aplicación web de Hola de nuevo y, a continuación, haga clic en **iniciar**.

   Hola trabajo Web se inicia automáticamente cuando publica, pero se detiene al cambiar una configuración. toorestart, puede reiniciar la aplicación web de Hola o reiniciar Hola trabajo Web en hello [Portal de Azure](http://go.microsoft.com/fwlink/?LinkId=529715). Es generalmente recomendada toorestart hello web aplicación después de un cambio de configuración.
7. Actualice la ventana del explorador de Hola que tiene la URL de la aplicación web hello en su barra de direcciones.

    aparece la página de inicio de Hola.
8. Crear un anuncio, tal y como lo hizo cuando se [se ejecutaba aplicación hello localmente](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).

   página de índice de Hello muestra sin una miniatura al principio.
9. Actualice la página de hello después de unos segundos y aparece hello miniatura.

   Si no aparece la miniatura de hello, puede tener toowait aproximadamente un minuto para hello toorestart de trabajo Web. Si después de un tiempo, aún no ve la miniatura de hello al actualizar página hello, Hola trabajo Web no se inicia automáticamente. En ese caso, vaya toohello **servicios de aplicaciones** hoja en hello [portal de Azure](https://portal.azure.com/), busque la aplicación web y, a continuación, haga clic en **iniciar**.

### <a name="view-hello-webjobs-sdk-dashboard"></a>Hola de vista panel de SDK de WebJobs
1. Hola [portal de Azure](https://portal.azure.com/), seleccione hello **hoja de servicios de aplicaciones**, busque la aplicación web y seleccione **WebJobs**.
3. Seleccione hello **registros** ficha.

    ![Pestaña Registros](./media/websites-dotnet-webjobs-sdk-get-started/log-tab.png)

    Una nueva pestaña de explorador abre toohello panel de SDK de WebJobs. panel de Hello muestra ese Hola trabajo Web se ejecuta y muestra una lista de funciones en el código que Hola que activa de SDK de WebJobs.
4. Haga clic en uno de hello funciones toosee detalles sobre la ejecución.

    ![Panel del SDK de WebJobs](./media/websites-dotnet-webjobs-sdk-get-started/wjdashboardhome.png)

    ![Panel del SDK de WebJobs](./media/websites-dotnet-webjobs-sdk-get-started/wjfunctiondetails.png)

    Hola **función reproducción** botón en esta página hace que Hola SDK de WebJobs framework toocall Hola función nuevo y le ofrece una función de toohello de datos que se pasan de oportunidad toochange hello en primer lugar.

> [!NOTE]
> Cuando haya terminado de pruebas, considere la posibilidad de eliminar la aplicación web de hello, cuenta de almacenamiento y la instancia de base de datos SQL. aplicación web de Hello es gratuito, pero hello cuenta de almacenamiento SQL y la instancia de base de datos generan cargos (si bien es cierto, mínimo debido toohello pequeño tamaño). Además, si deja hello web aplicación en ejecución, cualquier persona que se encuentra la dirección URL puede crear y ver anuncios. 
>
>

### <a name="delete-your-web-app"></a>Eliminar la aplicación web
En el portal de hello, vaya toohello **servicios de aplicaciones** hoja, busque y seleccione la aplicación web y, a continuación, haga clic en **eliminar**. Si solo desea tootemporarily impedir que otras personas tengan acceso a aplicaciones web de hello, haga clic en **detener** en su lugar. En ese caso, seguirán aplicando costos tooaccrue para hello cuenta de almacenamiento y la base de datos SQL.

### <a name="delete-your-storage-account"></a>Eliminar la cuenta de almacenamiento
toodelete su cuenta de almacenamiento, consulte [eliminar una cuenta de almacenamiento](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account). 

### <a name="delete-your-database"></a>Eliminar la base de datos
toodelete SQL de base de datos, vea hello [API de REST de base de datos de SQL Azure](https://docs.microsoft.com/rest/api/sql/) documentación.

## <a id="create"></a>Crear aplicación hello desde el principio
En esta sección deberá llevar a cabo hello las siguientes tareas:

* Crear una solución de Visual Studio con un proyecto web.
* Agregue un proyecto de biblioteca de clases para los datos de hello capa de acceso que se comparte entre Hola front-end y back-end.
* Agregue un proyecto de aplicación de consola de back-end de hello, con la implementación de trabajos Web habilitada.
* Agregar paquetes NuGet.
* Establecer preferencias del proyecto.
* Copiar archivos de código y la configuración de aplicaciones de aplicación Hola descargado que trabajó en la sección anterior de Hola de tutorial Hola.
* Revise las partes de Hola de código de hello que trabajan con colas y blobs de Azure y Hola SDK de WebJobs.

### <a name="create-a-visual-studio-solution-with-a-web-project-and-class-library-project"></a>Creación de una solución de Visual Studio con un proyecto web y un proyecto de biblioteca de clases
1. En Visual Studio, seleccione **Archivo** > **Nuevo** > **Proyecto**.
2. Hola **nuevo proyecto** cuadro de diálogo, elija **Visual C#** > **Web** > **aplicación Web de ASP.NET (.NET Framework)**.
3. Denomine el proyecto de hello ContosoAdsWeb, asigne el nombre de solución de hello ContosoAdsWebJobsSDK (cambiar el nombre de la solución de hello si se va a colocar en hello misma carpeta que Hola descargado solución) y, a continuación, haga clic en **Aceptar**.

    ![Nuevo proyecto](./media/websites-dotnet-webjobs-sdk-get-started/newproject.png)
4. Hola **nueva aplicación Web ASP.NET** cuadro de diálogo, elija la plantilla MVC de Hola y seleccione **Cambiar autenticación**.

    ![Cambiar autenticación](./media/websites-dotnet-webjobs-sdk-get-started/chgauth.png)
5. Hola **Cambiar autenticación** cuadro de diálogo, elija **sin autenticación**y, a continuación, haga clic en **Aceptar**.

    ![Sin autenticación](./media/websites-dotnet-webjobs-sdk-get-started/noauth.png)
6. Hola **nueva aplicación Web ASP.NET** cuadro de diálogo, haga clic en **Aceptar**.

    Visual Studio crea la solución de Hola y un proyecto de web de Hola.
7. En **el Explorador de soluciones**, haga clic en la solución de hello (no en proyecto de hello) y elija **agregar** > **nuevo proyecto**.
8. Hola **Agregar nuevo proyecto** cuadro de diálogo, elija **Visual C#** > **escritorio clásico de Windows** > **biblioteca de clases (. NET Marco de trabajo)** plantilla.  
9. Proyecto de hello Name *ContosoAdsCommon*y, a continuación, haga clic en **Aceptar**.

    Este proyecto contendrá contexto de Entity Framework de Hola y Hola data model que Hola front-end y back-end va a usar. Como alternativa, podría definir las clases relacionadas con EF de hello en el proyecto web de Hola y hacer referencia a ese proyecto desde el proyecto de WebJob de Hola. Sin embargo, a continuación, su proyecto WebJob tendría un ensamblados de referencia de tooweb, que no es necesario.

### <a name="add-a-console-application-project-that-has-webjobs-deployment-enabled"></a>Incorporación de un proyecto de aplicación de consola con la implementación de WebJobs habilitada
1. Haga clic en proyecto de web hello (no Hola solución o proyecto de biblioteca de clases de hello) y, a continuación, haga clic en **agregar** > **nuevo proyecto de WebJob de Azure**.

    ![Selección del menú Nuevo proyecto WebJob de Azure](./media/websites-dotnet-webjobs-sdk-get-started/newawjp.png)
2. Hola **Agregar trabajo Web de Azure** cuadro de diálogo, escriba ContosoAdsWebJob como ambos hello **nombre del proyecto** hello y **nombre del trabajo Web**. Deje **modo de trabajo Web ejecutan** establecido demasiado**ejecutar continuamente**.
3. Haga clic en **Aceptar**.

   Visual Studio crea una aplicación de consola que esté configurado toodeploy como un trabajo Web cada vez que implementar el proyecto web de Hola. toodo, que realiza Hola siguiente las tareas después de crear el proyecto de hello:

   * Agrega un *settings.json publicar el trabajo Web* archivo en la carpeta de propiedades del proyecto de hello trabajo Web.
   * Agrega un *webjobs list.json* archivo en la carpeta de propiedades del proyecto de hello web.
   * Instala Hola paquete Microsoft.Web.WebJobs.Publish NuGet en proyecto de WebJob Hola.

   Para obtener más información sobre estos cambios, consulte [cómo toodeploy trabajos Web mediante Visual Studio](websites-dotnet-deploy-webjobs.md).

### <a name="add-nuget-packages"></a>Incorporación de paquetes NuGet
plantilla de proyecto nuevo de Hola para un proyecto de trabajo Web instala automáticamente el paquete de NuGet de SDK de WebJobs de hello [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) y sus dependencias.

Uno de hello las dependencias del SDK de WebJobs que se instala automáticamente en el proyecto de WebJob Hola están Hola biblioteca de cliente de almacenamiento de Azure (SCL). Sin embargo, debe tooadd toohello toowork de proyecto web con blobs y colas.

1. Abra hello **administrar paquetes de NuGet** cuadro de diálogo de solución de Hola.
2. En el panel izquierdo de hello, seleccione **paquetes instalados**.
3. Buscar hello *el almacenamiento de Azure* del paquete y, a continuación, haga clic en **administrar**.
4. Hola **seleccionar proyectos** cuadro, seleccione hello **ContosoAdsWeb** casilla de verificación y, a continuación, haga clic en **Aceptar**.

    Los tres proyectos utilizan Hola Entity Framework toowork con datos de base de datos de SQL.
5. En el panel izquierdo de hello, seleccione **Online**.
6. Buscar hello *EntityFramework* NuGet empaquetar e instalarlo en los tres proyectos.

### <a name="set-project-references"></a>Establecimiento de preferencias del proyecto
Web y proyectos de trabajo Web funcionan con la base de datos SQL de hello, por lo tanto necesitan un proyecto de ContosoAdsCommon toohello de referencia.

1. Hola ContosoAdsWeb proyecto, establecer una referencia de proyecto de ContosoAdsCommon toohello. (Haga clic en proyecto de hello ContosoAdsWeb y, a continuación, haga clic en **agregar** > **referencia**. 
2. Hola **Administrador de referencias** cuadro de diálogo, seleccione **proyectos** > **solución** > **ContosoAdsCommon**y, a continuación, haga clic en **Aceptar**.)
   
    proyecto de WebJob de Hola necesita referencias para trabajar con imágenes y para tener acceso a las cadenas de conexión.

4. En proyectos de ContosoAdsWebJob hello, establezca una referencia demasiado`System.Drawing` y `System.Configuration`.

### <a name="add-code-and-configuration-files"></a>Agregar archivos de configuración y de código
Este tutorial no muestra cómo demasiado[crear controladores MVC y vistas que usan la técnica scaffolding](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), cómo demasiado[escribir código de Entity Framework que funciona con bases de datos de SQL Server](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), o [Hola conceptos básicos de la programación asincrónica en ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async). Por lo tanto, todo lo que sigue siendo toodo es copiar los archivos de código y la configuración de solución de hello descargado en la nueva solución de Hola. Después de hacerlo, hello las secciones siguientes se muestran y explican los elementos clave del código de hello.

tooadd archivos tooa proyecto o una carpeta, proyecto de Hola de menú contextual o carpeta y haga clic en **agregar** > **elemento existente**. Hola seleccione los archivos desee y haga clic en **agregar**. Si se le pregunta si desea que tooreplace los archivos existentes, haga clic en **Sí**.

1. En el proyecto ContosoAdsCommon de hello, elimine hello *Class1.cs* de archivos y agregar su Hola de contexto siguientes archivos de proyecto Hola descargado.

   * *Ad.cs*
   * *ContosoAdscontext.cs*
   * *BlobInformation.cs*
2. En proyecto de ContosoAdsWeb de hello, agregue Hola siguientes archivos de proyecto Hola descargado.

   * *Web.config*
   * *Global.asax.cs*  
   * Hola *controladores* carpeta: *AdController.cs*
   * Hola *Views\Shared* carpeta: *_Layout.cshtml* archivo
   * Hola *Views\Home* carpeta: *Index.cshtml*
   * Hola *Views\Ad* carpeta (crear carpeta de hello en primer lugar): cinco *.cshtml* archivos
3. En proyecto de ContosoAdsWebJob de hello, agregue Hola siguientes archivos de proyecto Hola descargado.

   * *App.config* (cambiar el filtro de tipo de archivo de hello demasiado**todos los archivos**)
   * *Program.cs*
   * *Functions.cs*

Ahora puede compilar, ejecutar e implementar aplicación de hello tal como se indica anteriormente en el tutorial de Hola. Antes de hacerlo, sin embargo, detenga Hola trabajo Web que se esté ejecutando en hello primera aplicación web que se implementan en. En caso contrario, ese trabajo Web procesar mensajes en cola creados localmente o por aplicación Hola que se ejecuta en una nueva aplicación web, ya que todos utilizan Hola mismo cuenta de almacenamiento.

## <a id="code"></a>Revise el código de la aplicación hello
Hello las secciones siguientes explican el código de hello relacionados con tooworking con hello SDK de WebJobs y blobs de almacenamiento de Azure y colas.

> [!NOTE]
> Para toohello específico Hola código SDK de WebJobs, visite toohello [Program.cs y Functions.cs](#programcs) secciones.
>
>

### <a name="contosoadscommon---adcs"></a>ContosoAdsCommon - Ad.cs
archivo de Hello Ad.cs define una enumeración de categorías de ad y una clase de entidad POCO para obtener información de ad.

        public enum Category
        {
            Cars,
            [Display(Name="Real Estate")]
            RealEstate,
            [Display(Name = "Free Stuff")]
            FreeStuff
        }

        public class Ad
        {
            public int AdId { get; set; }

            [StringLength(100)]
            public string Title { get; set; }

            public int Price { get; set; }

            [StringLength(1000)]
            [DataType(DataType.MultilineText)]
            public string Description { get; set; }

            [StringLength(1000)]
            [DisplayName("Full-size Image")]
            public string ImageURL { get; set; }

            [StringLength(1000)]
            [DisplayName("Thumbnail")]
            public string ThumbnailURL { get; set; }

            [DataType(DataType.Date)]
            [DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
            public DateTime PostedDate { get; set; }

            public Category? Category { get; set; }
            [StringLength(12)]
            public string Phone { get; set; }
        }

### <a name="contosoadscommon---contosoadscontextcs"></a>ContosoAdsCommon - ContosoAdsContext.cs
Hola ContosoAdsContext clase especifica que se utiliza la clase de Ad de hello en una colección de DbSet, que Entity Framework se almacena en una base de datos SQL.

        public class ContosoAdsContext : DbContext
        {
            public ContosoAdsContext() : base("name=ContosoAdsContext")
            {
            }
            public ContosoAdsContext(string connString)
                : base(connString)
            {
            }
            public System.Data.Entity.DbSet<Ad> Ads { get; set; }
        }

clase Hello tiene dos constructores. Hola primero participa en el proyecto web de Hola y especifica Hola nombre de una cadena de conexión que se almacena en el archivo Web.config de Hola o entorno de Azure en tiempo de ejecución de Hola. segundo constructor de Hello permite toopass en la cadena de conexión real de Hola. Es necesario para el proyecto WebJob de hello porque no tiene un archivo Web.config. Se ha visto anteriormente donde se almacenó esta cadena de conexión y podrá ver más adelante cómo código de hello recupera la cadena de conexión de hello cuando crea una instancia de clase de DbContext Hola.

### <a name="contosoadscommon---blobinformationcs"></a>ContosoAdsCommon - BlobInformation.cs
Hola `BlobInformation` clase es toostore usa información acerca de un blob de imágenes en un mensaje de la cola.

        public class BlobInformation
        {
            public Uri BlobUri { get; set; }

            public string BlobName
            {
                get
                {
                    return BlobUri.Segments[BlobUri.Segments.Length - 1];
                }
            }
            public string BlobNameWithoutExtension
            {
                get
                {
                    return Path.GetFileNameWithoutExtension(BlobName);
                }
            }
            public int AdId { get; set; }
        }


### <a name="contosoadsweb---globalasaxcs"></a>ContosoAdsWeb - Global.asax.cs
Código que se llama desde hello `Application_Start` método crea un *imágenes* contenedor de blobs y una *imágenes* cola si todavía no existen. Esto garantiza que cada vez que se inicia con una nueva cuenta de almacenamiento, Hola necesarias se crean automáticamente a la cola y el contenedor de blobs.

Hola cuenta de almacenamiento de toohello de código obtiene acceso mediante el uso de la cadena de conexión de almacenamiento de Hola de hello *Web.config* entorno de Azure en tiempo de ejecución o de archivo.

        var storageAccount = CloudStorageAccount.Parse
            (ConfigurationManager.ConnectionStrings["AzureWebJobsStorage"].ToString());

A continuación, obtiene una referencia toohello *imágenes* contenedor de blobs, crea el contenedor de hello si aún no existe, y establece permisos en el nuevo contenedor de Hola de acceso. De forma predeterminada, nuevos contenedores de permitir que a sólo los clientes con blobs de tooaccess de credenciales de cuenta de almacenamiento. aplicación web de Hello necesita Hola blobs toobe público para que pueden mostrar imágenes con direcciones URL que blobs de imagen toohello de punto.

        var blobClient = storageAccount.CreateCloudBlobClient();
        var imagesBlobContainer = blobClient.GetContainerReference("images");
        if (imagesBlobContainer.CreateIfNotExists())
        {
            imagesBlobContainer.SetPermissions(
                new BlobContainerPermissions
                {
                    PublicAccess = BlobContainerPublicAccessType.Blob
                });
        }

Un código similar Obtiene una referencia toohello *thumbnailrequest* poner en cola y crea una nueva cola. En este caso no es necesario cambios de permiso.

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        var imagesQueue = queueClient.GetQueueReference("thumbnailrequest");
        imagesQueue.CreateIfNotExists();

### <a name="contosoadsweb---layoutcshtml"></a>ContosoAdsWeb - _Layout.cshtml
Hola *_Layout.cshtml* archivo establece el nombre de la aplicación hello en hello encabezado y pie y crea una entrada de menú "Anuncios".

### <a name="contosoadsweb---viewshomeindexcshtml"></a>ContosoAdsWeb - Views\Home\Index.cshtml
Hola *Views\Home\Index.cshtml* archivo muestra los vínculos de categoría en la página de inicio de Hola. vínculos de Hello pasan el valor entero Hola Hola `Category` enumeración en una página de índice de anuncios de toohello variable de cadena de consulta.

        <li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
        <li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
        <li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
        <li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>

### <a name="contosoadsweb---adcontrollercs"></a>ContosoAdsWeb - AdController.cs
Hola *AdController.cs* archivo, llamadas de constructor Hola Hola `InitializeStorage` objetos de biblioteca de cliente de almacenamiento de Azure de toocreate del método que proporcionan una API para trabajar con blobs y colas.

A continuación, el código de hello Obtiene una referencia toohello *imágenes* contenedor de blob como vimos anteriormente en *Global.asax.cs*. Mientras hace eso, establece una [directiva de reintentos](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) apropiada para una aplicación web. Directiva de reintentos de retroceso exponencial de Hello predeterminada podría dejar de responder hello web app para más de un minuto en varios intentos para un error transitorio. Directiva de reintentos de Hello especificada aquí espera tres segundos después de cada uno de ellos probar para una toothree intentos.

        var blobClient = storageAccount.CreateCloudBlobClient();
        blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesBlobContainer = blobClient.GetContainerReference("images");

Un código similar Obtiene una referencia toohello *imágenes* cola.

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesQueue = queueClient.GetQueueReference("blobnamerequest");

La mayoría del código de controlador de hello es típico para trabajar con un modelo de datos de Entity Framework mediante una clase DbContext. Una excepción es hello HttpPost `Create` método, que carga un archivo y lo guarda en el almacenamiento de blobs. enlazador de modelos de Hello proporciona un [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) toohello método del objeto.

        [HttpPost]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> Create(
            [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
            HttpPostedFileBase imageFile)

Si el usuario de hello seleccionó un tooupload de archivo, código de hello carga el archivo hello, lo guarda en un blob y actualiza el registro de base de datos de Ad de hello con una dirección URL que señala toohello blob.

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            blob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = blob.Uri.ToString();
        }

Hello código Hola carga es Hola `UploadAndSaveBlobAsync` método. Crea un nombre GUID para el blob de hello, cargas y archivo de hello guarda y devuelve un blob de referencia toohello guardado.

        private async Task<CloudBlockBlob> UploadAndSaveBlobAsync(HttpPostedFileBase imageFile)
        {
            string blobName = Guid.NewGuid().ToString() + Path.GetExtension(imageFile.FileName);
            CloudBlockBlob imageBlob = imagesBlobContainer.GetBlockBlobReference(blobName);
            using (var fileStream = imageFile.InputStream)
            {
                await imageBlob.UploadFromStreamAsync(fileStream);
            }
            return imageBlob;
        }

Después de hello HttpPost `Create` método carga un blob y Hola de las actualizaciones de base de datos, crea un proceso de back-end de Hola de tooinform para cola de mensajes que una imagen está lista para la vista en miniatura de conversión tooa.

        BlobInformation blobInfo = new BlobInformation() { AdId = ad.AdId, BlobUri = new Uri(ad.ImageURL) };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        await thumbnailRequestQueue.AddMessageAsync(queueMessage);

Hola código de hello HttpPost `Edit` método es similar, salvo que si el usuario de hello selecciona un nuevo archivo de imagen, deben eliminarse los blobs que ya existen para este anuncio.

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            await DeleteAdBlobsAsync(ad);
            imageBlob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = imageBlob.Uri.ToString();
        }

Este es el código de hello que elimina los blobs cuando se elimina un anuncio:

        private async Task DeleteAdBlobsAsync(Ad ad)
        {
            if (!string.IsNullOrWhiteSpace(ad.ImageURL))
            {
                Uri blobUri = new Uri(ad.ImageURL);
                await DeleteAdBlobAsync(blobUri);
            }
            if (!string.IsNullOrWhiteSpace(ad.ThumbnailURL))
            {
                Uri blobUri = new Uri(ad.ThumbnailURL);
                await DeleteAdBlobAsync(blobUri);
            }
        }
        private static async Task DeleteAdBlobAsync(Uri blobUri)
        {
            string blobName = blobUri.Segments[blobUri.Segments.Length - 1];
            CloudBlockBlob blobToDelete = imagesBlobContainer.GetBlockBlobReference(blobName);
            await blobToDelete.DeleteAsync();
        }

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a>ContosoAdsWeb - Views\Ad\Index.cshtml y Details.cshtml
Hola *Index.cshtml* archivo muestra vistas en miniatura con hello otros datos de ad:

        <img  src="@Html.Raw(item.ThumbnailURL)" />

Hola *Details.cshtml* archivo muestra la imagen a tamaño completo hello:

        <img src="@Html.Raw(Model.ImageURL)" />

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a>ContosoAdsWeb - Views\Ad\Create.cshtml y Edit.cshtml
Hola *Create.cshtml* y *Edit.cshtml* archivos especifican formulario codificación que permite Hola Hola de controlador tooget `HttpPostedFileBase` objeto.

        @using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))

Un `<input>` elemento indica Hola explorador tooprovide un cuadro de diálogo de selección de archivo.

        <input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />

### <a id="programcs"></a>ContosoAdsWebJob: Program.cs
Cuando Hola trabajo Web que se inicia, hello `Main` llamadas al método Hola SDK de WebJobs `JobHost.RunAndBlock` toobegin ejecución del método de desencadenadas funciones en el subproceso actual Hola.

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

### <a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - Método GenerateThumbnail
Hola SDK de WebJobs llama a este método cuando se recibe un mensaje de la cola. método Hello crea una vista en miniatura y coloca Hola miniatura de la dirección URL en la base de datos de Hola.

        public static void GenerateThumbnail(
        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,
        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)
        {
            using (Stream output = outputBlob.OpenWrite())
            {
                ConvertImageToThumbnailJPG(input, output);
                outputBlob.Properties.ContentType = "image/jpeg";
            }

            // Entity Framework context class is not thread-safe, so it must
            // be instantiated and disposed within hello function.
            using (ContosoAdsContext db = new ContosoAdsContext())
            {
                var id = blobInfo.AdId;
                Ad ad = db.Ads.Find(id);
                if (ad == null)
                {
                    throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", id.ToString()));
                }
                ad.ThumbnailURL = outputBlob.Uri.ToString();
                db.SaveChanges();
            }
        }

* Hola `QueueTrigger` atributo dirige hello toocall de SDK de WebJobs este método cuando se recibe un mensaje nuevo en la cola de thumbnailrequest Hola.

        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,

    Hola `BlobInformation` objeto de mensaje de bienvenida de cola es automáticamente deserializado en hello `blobInfo` parámetro. Cuando se completa el método hello, se elimina el mensaje de bienvenida de cola. Si se produce un error en el método hello antes de completar, no se elimina el mensaje de bienvenida de cola; Después de que expire una concesión de 10 minutos, mensaje de bienvenida es toobe lanzamiento nuevo recoge y procesa. Esta secuencia no se repite de manera indefinida cuando un mensaje provoca siempre una excepción. Después de 5 incorrecta intentos tooprocess un mensaje, mensaje de bienvenida es tooa movida cola denominada {queuename}-dudoso. Hola número máximo de intentos es configurable.
* Hola dos `Blob` atributos proporcionan los objetos que están enlazados tooblobs: un blob de imágenes existente toohello y uno tooa nuevo en miniatura blob que crea el método hello.

        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)

    Nombres de BLOB proceden de propiedades de hello `BlobInformation` objeto recibido en el mensaje de bienvenida de cola (`BlobName` y `BlobNameWithoutExtension`). tooget Hola todas las funcionalidades de hello biblioteca cliente de almacenamiento, puede usar hello `CloudBlockBlob` toowork de clase con los blobs. Si desea que el código de tooreuse que escribió toowork con `Stream` objetos, puede utilizar hello `Stream` clase.

Para obtener más información acerca de cómo toowrite las funciones utilizan atributos de SDK de WebJobs, vea Hola recursos siguientes:

* [¿Cómo toouse Azure cola de almacenamiento con hello SDK de WebJobs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [¿Cómo toouse Azure blob storage con hello SDK de WebJobs](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [Cómo toouse Azure tabla almacenamiento con hello SDK de WebJobs](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [Cómo toouse de Bus de servicio de Azure con Hola SDK de WebJobs](websites-dotnet-webjobs-sdk-service-bus.md)

> [!NOTE]
> * Si la aplicación web se ejecuta en varias máquinas virtuales, se ejecutarán simultáneamente varios trabajos Web, y en algunos casos esto puede producir en hello mismo datos procesados varias veces. Esto no es un problema si usa cola integrados de hello, blob y desencadenadores de Bus de servicio. Hola SDK garantiza que las funciones se procesará una sola vez para cada mensaje o blob.
> * Para obtener información acerca de cómo tooimplement apagado ordenado, consulte [apagado ordenado](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).
> * Hola código de hello `ConvertImageToThumbnailJPG` método (no mostrado) usa las clases en hello `System.Drawing` espacio de nombres para simplificar el trabajo. Sin embargo, las clases de hello en este espacio de nombres se diseñaron para su uso con Windows Forms. No se admiten para usarse en un servicio de Windows o ASP.NET. Para más información acerca de las opciones de procesamiento de imagen, consulte [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) (Generación de imagen dinámica) y [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na) (Cambio de tamaño de imagen profunda).
>
>

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha visto una aplicación simple de varios niveles que emplea Hola SDK de WebJobs para el procesamiento de back-end. En esta sección se ofrecen algunas sugerencias para obtener más información acerca de las aplicaciones de múltiples niveles de ASP.NET y WebJobs.

### <a name="missing-features"></a>Características que faltan
se ha conservado simple aplicación Hello para obtener un tutorial de introducción. En una aplicación del mundo real, debería implementar [inyección de dependencia](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) hello y [repositorio y una unidad de trabajan patrones](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), use [una interfaz para el registro](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), utilice [ EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) datos toomanage cambios en el modelo y usar [resistencia de conexión de EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage errores transitorios de red.

### <a name="scaling-webjobs"></a>Escalado de WebJobs
Los trabajos Web se ejecuta en hello contexto de una aplicación web y no es escalables por separado. Por ejemplo, si tiene una instancia de aplicación web estándar, tiene solo una instancia de su proceso de segundo plano que se ejecuta y que está usando algunos de los recursos del servidor hello (CPU, memoria, etc.) que lo contrario estarían disponibles tooserve contenido de web.

Si tráfico varía según la hora del día o día de la semana, y si necesita Hola back-end de procesamiento puede esperar toodo, puede programar los trabajos Web toorun en momentos de poco tráfico. Si carga Hola sigue siendo demasiado alto para esa solución, puede ejecutar Hola back-end como un trabajo Web en una aplicación web independiente dedicado para ese fin. A continuación, puede escalar la aplicación web back-end con independencia de la aplicación web front-end.

Para obtener más información, consulte [Escalado de WebJobs](websites-webjobs-resources.md#scale).

### <a name="avoiding-web-app-timeout-shut-downs"></a>Evitar tiempos de inactividad por tiempo de espera agotado en aplicaciones web
toomake seguro sus trabajos Web se ejecuta siempre, y se ejecuta en todas las instancias de la aplicación web, tiene hello tooenable [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) característica.

### <a name="using-hello-webjobs-sdk-outside-of-webjobs"></a>Uso de hello SDK de WebJobs fuera de trabajos Web
Un programa que usa el SDK de WebJobs de hello no tiene toorun en Azure en un trabajo Web. Se puede ejecutar localmente y también se puede ejecutar en otros entornos, como por ejemplo un rol de trabajo Servicio en la nube o un servicio de Windows. Sin embargo, solo puede acceder a Hola panel de SDK de WebJobs a través de una aplicación web de Azure. panel de hello toouse tiene tooconnect cuenta de almacenamiento de la toohello de hello web app usa al establecer una cadena de conexión de hello AzureWebJobsDashboard en hello **configurar** ficha del portal clásico de Hola. A continuación, puede obtener toohello panel mediante Hola después de la dirección URL:

https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions

Para obtener más información, consulte [obtener un panel para el desarrollo local con hello SDK de WebJobs](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), pero tenga en cuenta que muestra un nombre de cadena de conexión anterior.

### <a name="more-webjobs-documentation"></a>Más documentación sobre WebJobs
Para obtener más información, consulte [Recursos de documentación de WebJobs de Azure](http://go.microsoft.com/fwlink/?LinkId=390226).
