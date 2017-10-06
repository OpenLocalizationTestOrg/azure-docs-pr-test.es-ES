---
title: aaaGet a trabajar con ASP.NET y servicios de nube de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una aplicación de varios nivel con ASP.NET MVC y Azure. aplicación Hello se ejecuta en un servicio de nube, con el rol web y rol de trabajo. Utiliza Entity Framework, Base de datos SQL y blobs y colas de Almacenamiento de Azure."
services: cloud-services, storage
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: d7aa440d-af4a-4f80-b804-cc46178df4f9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/15/2017
ms.author: adegeo
ms.openlocfilehash: 86271c29b79fad3f01f8ea0e88fd00c7aefc970c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cloud-services-and-aspnet"></a>Introducción a Servicios en la nube de Azure y ASP.NET

## <a name="overview"></a>Información general
Este tutorial se muestra cómo toocreate una aplicación de varios niveles .NET con un front-end, ASP.NET MVC e implementarlo tooan [servicio de nube de Azure](cloud-services-choose-me.md). Hola aplicación usa [base de datos de SQL Azure](http://msdn.microsoft.com/library/azure/ee336279), hello [servicio Blob de Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), hello y [servicio cola de Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern). También puede [descargar el proyecto de Visual Studio de hello](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) de hello MSDN Code Gallery.

Hola tutorial le muestra cómo localmente, aplicación hello toobuild y ejecute cómo toodeploy lo tooAzure y Hola de ejecución en la nube y cómo toobuild desde cero. Puede iniciar creación desde el principio y, a continuación, Hola prueba e implementar pasos más adelante si lo prefiere.

## <a name="contoso-ads-application"></a>Aplicación Contoso Ads
aplicación Hello es un tablón de anuncios publicitarios. Los usuarios crean un anuncio introduciendo texto y cargando una imagen. Puede ver una lista de anuncios con imágenes en miniatura y pueden ver imagen a tamaño completo hello cuando selecciona un detalles de hello toosee de ad.

![Ad list](./media/cloud-services-dotnet-get-started/list.png)

aplicación Hello usa hello [centrada en la cola de trabajo patrón](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff carga de trabajo de hello intensiva de CPU de creación de proceso de miniaturas tooa back-end.

## <a name="alternative-architecture-websites-and-webjobs"></a>Arquitectura alternativa: sitios web y WebJobs
Este tutorial muestra cómo toorun front-end y back-end en un Azure cloud service. Una alternativa es toorun Hola front-end en una [sitio Web de Azure](/services/web-sites/) y usar hello [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) característica (actualmente en versión preliminar) para hello back-end. Para obtener un tutorial que utiliza trabajos Web, consulte [empezar a trabajar con el SDK de WebJobs de Azure hello](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md). Para obtener información acerca de cómo los servicios toochoose Hola que mejor ajusta su escenario, consulte [comparación de sitios Web de Azure, servicios en la nube y máquinas virtuales](../app-service-web/choose-web-site-cloud-service-vm.md).

## <a name="what-youll-learn"></a>Temas que se abordarán
* ¿Cómo tooenable Hola a su equipo de desarrollo de Azure mediante la instalación del SDK de Azure.
* ¿Cómo toocreate un en Visual Studio en la nube proyecto de servicio con un rol web de ASP.NET MVC y un rol de trabajo.
* ¿Cómo tootest Hola nube proyecto de servicio localmente, mediante el emulador de almacenamiento de Azure Hola.
* Cómo toopublish Hola nube proyecto tooan Azure servicio en la nube y pruebe el uso de una cuenta de almacenamiento de Azure.
* Cómo tooupload archivos y almacenarlos en el servicio de Blob de Azure Hola.
* ¿Cómo toouse Hola servicio de cola de Azure para la comunicación entre niveles.

## <a name="prerequisites"></a>Requisitos previos
Hello tutorial se da por supuesto que comprende [servicios de nube de los conceptos básicos sobre Azure](cloud-services-choose-me.md) como *rol web* y *rol de trabajo* terminología.  También se supone que sabe cómo toowork con [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) o [formularios Web Forms](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) proyectos de Visual Studio. aplicación de ejemplo de Hola utiliza MVC, pero la mayoría de tutorial de hello también se aplica tooWeb formularios.

Puede ejecutar la aplicación hello localmente sin una suscripción de Azure, pero necesitará una toodeploy Hola aplicación toohello en la nube. Si aún no la tiene, puede [activar los beneficios de suscripción a MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) o [registrarse para obtener una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).

instrucciones del tutorial Hola trabajan con cualquiera de hello siguientes productos:

* Visual Studio 2013
* Visual Studio 2015
* Visual Studio 2017

Si no tiene uno de estos, Visual Studio puede instalarse automáticamente al instalar hello Azure SDK.

## <a name="application-architecture"></a>Arquitectura de la aplicación
aplicación Hello almacena anuncios en una base de datos SQL con tablas de hello toocreate Entity Framework Code First y acceder a los datos de Hola. Para cada anuncio Hola base de datos almacena dos direcciones URL, uno para Hola imagen a tamaño completo y otra para la miniatura de Hola.

![Ad table](./media/cloud-services-dotnet-get-started/adtable.png)

Cuando un usuario carga una imagen, front-end de Hola que se ejecuta en un rol web almacena la imagen de hello en un [blobs de Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), y almacena información de anuncios de Hola en base de datos de hello con una dirección URL que señala toohello blob. Hola al mismo tiempo, escribe un tooan mensaje cola de Azure. Un proceso de back-end que se ejecuta en un rol de trabajo periódicamente sondea Hola si hay mensajes nuevos. Cuando aparezca un mensaje nuevo, rol de trabajo de hello crea una vista en miniatura de esa imagen y actualizaciones Hola campo de base de datos de dirección URL en miniatura para que ad. Hello siguiente diagrama muestra cómo interactúan las partes de Hola de aplicación hello.

![Contoso Ads architecture](./media/cloud-services-dotnet-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]

## <a name="download-and-run-hello-completed-solution"></a>Descargue y ejecute la solución de hello completado
1. Descargue y descomprima hello [completado solución](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).
2. Inicie Visual Studio.
3. De hello **archivo** menú elija **Abrir proyecto**, desplácese toowhere descargó solución hello y, a continuación, abra el archivo de solución de Hola.
4. Presione la solución CTRL + MAYÚS + B toobuild Hola.

    De forma predeterminada, Visual Studio restaurará automáticamente contenido del paquete NuGet hello, que no se incluyó en hello *.zip* archivo. Si no se restauran los paquetes de saludo, instálelos manualmente va toohello **administrar paquetes de NuGet para la solución** cuadro de diálogo y haga clic en hello **restaurar** situado en la parte superior de hello derecha.
5. En **el Explorador de soluciones**, asegúrese de que **ContosoAdsCloudService** está seleccionado como proyecto de inicio de Hola.
6. Si está utilizando Visual Studio 2015 o versiones posteriores, cambie la cadena de conexión de SQL Server de hello en la aplicación hello *Web.config* archivo de proyecto de ContosoAdsWeb de Hola y Hola *ServiceConfiguration.Local.cscfg* archivo del proyecto de ContosoAdsCloudService Hola. En cada caso, cambie "(localdb) \v11.0" demasiado "(localdb) \MSSQLLocalDB".
7. Presione la aplicación de hello toorun CTRL + F5.

    Cuando se ejecuta un proyecto de servicio de nube localmente, Visual Studio, se invoca automáticamente hello Azure *emulador de proceso* y Azure *emulador de almacenamiento*. Hola de proceso utiliza emulador rol web de su equipo recursos toosimulate hello y entornos de rol de trabajo. emulador de almacenamiento de Hello usa un [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) toosimulate almacenamiento en nube de Azure de la base de datos.

    Hello primera vez que se ejecuta un proyecto de servicio de nube, que tarda aproximadamente un minuto Hola emuladores toostart seguridad. Cuando haya finalizado de inicio del emulador, explorador predeterminado de hello abre toohello página de inicio de aplicaciones.

    ![Contoso Ads architecture](./media/cloud-services-dotnet-get-started/home.png)
8. Haga clic en **Crear un anuncio**.
9. Escriba algunos datos de prueba y seleccione un *.jpg* tooupload la imagen y, a continuación, haga clic en **crear**.

    ![Create page](./media/cloud-services-dotnet-get-started/create.png)

    aplicación Hello queda toohello página de índice, pero no muestra una vista en miniatura para nuevo anuncio de Hola dado que el procesamiento no se ha realizado.
10. Espere unos instantes y, a continuación, actualizar la vista en miniatura de hello índice página toosee Hola.

     ![Página de índice](./media/cloud-services-dotnet-get-started/list.png)
11. Haga clic en **detalles** para la imagen a tamaño completo ad toosee Hola.

     ![Details page](./media/cloud-services-dotnet-get-started/details.png)

Ha ha estado ejecutando la aplicación hello por completo en el equipo local, sin nube toohello de conexión. emulador de almacenamiento de Hello almacena cola hello y datos de blob en una base de datos de SQL Server Express LocalDB y aplicación hello almacenan los datos de ad de hello en otra base de datos de LocalDB. Base de datos de Entity Framework Code First Hola creada automáticamente ad Hola primera vez hello web aplicación intentó tooaccess lo.

Hola pasos de la sección configurará recursos de nube de Azure toouse Hola la solución para las colas, blobs y base de datos de aplicación Hola cuando se ejecuta en la nube de Hola. Si deseara toocontinue toorun localmente, pero usar los recursos de almacenamiento y base de datos en la nube, puede hacerlo. Es simplemente una cuestión de configuración de las cadenas de conexión, que podrá ver cómo toodo.

## <a name="deploy-hello-application-tooazure"></a>Implementar Hola aplicación tooAzure
Deberá llevar a cabo Hola tras la aplicación de hello toorun de pasos en la nube de hello:

* Cree un servicio en la nube de Azure.
* Cree una base de datos SQL de Azure.
* Cree una cuenta de Azure Storage.
* Configurar Hola solución toouse la base de datos de SQL Azure cuando se ejecuta en Azure.
* Configurar Hola solución toouse su cuenta de almacenamiento de Azure cuando se ejecuta en Azure.
* Implementar el servicio de nube de Azure de hello proyecto tooyour.

### <a name="create-an-azure-cloud-service"></a>Crear un servicio en la nube de Azure
Un servicio de nube de Azure es Hola entorno Hola aplicación se ejecutará en.

1. En el explorador, abra hello [portal de Azure](https://portal.azure.com).
2. Haga clic en **Nuevo > Proceso > Servicio en la nube**.

3. En el cuadro de entrada de hello DNS nombre, escriba un prefijo de dirección URL para el servicio en la nube Hola.

    Esta dirección URL tiene toobe único.  Obtendrá un mensaje de error si elige el prefijo de Hola ya está en uso.
4. Especifique un nuevo grupo de recursos para el servicio de Hola. Haga clic en **crear nuevo** y, a continuación, escriba un nombre en hello recursos grupo cuadro de entrada, como CS_contososadsRG.

5. Elija la región de Hola donde desea que la aplicación de hello toodeploy.

    Este campo especifica el centro de datos en el que se hospedará el servicio en la nube. Para una aplicación de producción, elegiría a clientes más cercanos tooyour hello de la región. Para este tutorial, elija tooyou de hello región más cercana.
5. Haga clic en **Crear**.

    En Hola después de la imagen, se crea un servicio de nube con hello CSvccontosoads.cloudapp.net de dirección URL.

    ![New Cloud Service](./media/cloud-services-dotnet-get-started/newcs.png)

### <a name="create-an-azure-sql-database"></a>Crear una base de datos SQL de Azure
Cuando la aplicación hello se ejecuta en la nube de hello, usará una base de datos en la nube.

1. Hola [portal de Azure](https://portal.azure.com), haga clic en **nuevo > bases de datos > base de datos SQL**.
2. Hola **nombre de base de datos** cuadro, escriba *contosoads*.
3. Hola **grupo de recursos**, haga clic en **utilizar existente** y grupo de recursos de hello seleccione utilizado para servicio de nube de Hola.
4. Hola después de la imagen, haga clic en **Server: configurar los valores obligatorios** y **crear un nuevo servidor**.

    ![Servidor de túnel toodatabase](./media/cloud-services-dotnet-get-started/newdb.png)

    O bien, si su suscripción ya tiene un servidor, puede seleccionar que el servidor de la lista desplegable de Hola.
5. Hola **nombre del servidor** cuadro, escriba *csvccontosodbserver*.

6. Complete los campos **Nombre de inicio de sesión** y **Contraseña** con los datos de un administrador.

    Si seleccionó **Crear un servidor nuevo**, no escribirá aquí un nombre y una contraseña existentes. Que se están escribiendo un nuevo nombre y una contraseña que está definiendo ahora toouse más adelante cuando tiene acceso a la base de datos de Hola. Si ha seleccionado un servidor que creó anteriormente, se le pedirá para que ya haya creado la cuenta de usuario administrativo Hola contraseña toohello.
7. Elija Hola mismo **ubicación** que eligió para el servicio en la nube Hola.

    Cuando Servicios de nube de Hola y base de datos están en distintos centros de datos (regiones diferentes), aumentará la latencia y le cobrará por el ancho de banda fuera Hola data center. El ancho de banda del centro de datos es gratuito.
8. Comprobar **server tooaccess de permitir que los servicios de azure**.
9. Haga clic en **seleccione** para nuevo servidor de Hola.

    ![Nuevo servidor de SQL Database](./media/cloud-services-dotnet-get-started/newdbserver.png)
10. Haga clic en **Crear**.

### <a name="create-an-azure-storage-account"></a>Creación de una cuenta de Azure Storage
Una cuenta de almacenamiento de Azure proporciona recursos para almacenar datos de cola y blob en la nube de Hola.

En una aplicación real, normalmente crearía cuentas independientes para los datos de aplicación frente a los datos de registro, y cuentas diferentes para datos de prueba frente a datos de producción. En este tutorial, usará solamente una cuenta.

1. Hola [portal de Azure](https://portal.azure.com), haga clic en **nuevo > almacenamiento > cuenta de almacenamiento: blob, archivo, tabla, cola**.
2. Hola **nombre** cuadro, escriba un prefijo de dirección URL.

    Este texto de prefijo más Hola que se observan en el cuadro de hello será la cuenta de almacenamiento de dirección URL única de Hola tooyour. Si ya se ha utilizado el prefijo de Hola que escriba por otra persona, tendrá que toochoose es un prefijo diferente.
3. Conjunto hello **modelo de implementación** demasiado*clásico*.

4. Conjunto hello **replicación** lista desplegable lista demasiado**almacenamiento con redundancia local**.

    Cuando la replicación geográfica está habilitada para una cuenta de almacenamiento, contenido de Hola almacenado está replicada tooa centro de datos secundario tooenable conmutación por error si se produce un desastre importante en la ubicación principal Hola. La replicación geográfica puede suponer costes adicionales. Para las cuentas de prueba y desarrollo, generalmente no desea toopay para la replicación geográfica. Para obtener más información, consulte [Creación, administración o eliminación de una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md).

5. Hola **grupo de recursos**, haga clic en **utilizar existente** y grupo de recursos de hello seleccione utilizado para servicio de nube de Hola.
6. Conjunto hello **ubicación** toohello de lista desplegable misma región que eligió para el servicio en la nube Hola.

    Cuando se encuentran cuenta de almacenamiento y el servicio de nube de hello en distintos centros de datos (regiones diferentes), aumentará la latencia y le cobrará por el ancho de banda fuera Hola data center. El ancho de banda del centro de datos es gratuito.

    Grupos de afinidad de Azure proporcionan una distancia de hello mecanismo toominimize entre los recursos en un centro de datos, lo que puede reducir la latencia. Este tutorial no usa grupos de afinidad. Para obtener más información, consulte [cómo tooCreate una afinidad de grupo en Azure](http://msdn.microsoft.com/library/jj156209.aspx).
7. Haga clic en **Crear**.

    ![New storage account](./media/cloud-services-dotnet-get-started/newstorage.png)

    En la imagen de hello, se crea una cuenta de almacenamiento con la dirección URL de hello `csvccontosoads.core.windows.net`.

### <a name="configure-hello-solution-toouse-your-azure-sql-database-when-it-runs-in-azure"></a>Configurar la base de datos de SQL Azure de hello solución toouse cuando se ejecuta en Azure
Hola proyecto web y proyecto de rol de trabajo cada hello tiene su propia cadena de conexión de base de datos y es necesario que cada base de datos de SQL Azure de toopoint toohello cuando la aplicación hello se ejecuta en Azure.

Usará un [transformación de Web.config](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) para el rol web de hello y una configuración de entorno de servicio de nube para rol de trabajo de Hola.

> [!NOTE]
> En esta sección y la sección siguiente de hello, almacenar credenciales en archivos de proyecto. [No almacene información confidencial en repositorios de código fuente público.](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets)
>
>

1. En el proyecto de ContosoAdsWeb hello, abra hello *Web.Release.config* archivo de transformación para la aplicación hello *Web.config* de archivos, elimine el bloque de comentario de Hola que contiene un `<connectionStrings>` elemento y pegar Hola siguiente código en su lugar.

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="{connectionstring}"
        providerName="System.Data.SqlClient" xdt:Transform="SetAttributes" xdt:Locator="Match(name)"/>
    </connectionStrings>
    ```

    Deje el archivo hello abierta para su edición.
2. Hola [portal de Azure](https://portal.azure.com), haga clic en **bases de datos SQL** en el panel izquierdo de hello, haga clic en la base de datos de Hola que creó para este tutorial y, a continuación, haga clic en **mostrar cadenas de conexión**.

    ![Mostrar cadenas de conexión](./media/cloud-services-dotnet-get-started/showcs.png)

    portal de Hello muestra las cadenas de conexión, con un marcador de posición para contraseña de Hola.

    ![Cadenas de conexión](./media/cloud-services-dotnet-get-started/connstrings.png)
3. Hola *Web.Release.config* transformar el archivo, elimine `{connectionstring}` y pegar en su cadena de conexión de ADO.NET de hello portal de Azure Hola de contexto.
4. En cadena de conexión de Hola que pegó en hello *Web.Release.config* transformar el archivo, reemplace `{your_password_here}` con contraseña de Hola que creó para la base de datos SQL nueva Hola.
5. Guarde el archivo hello.  
6. Seleccione y copie la cadena de conexión de hello (sin Hola que rodean las comillas) para su uso en hello siguiendo los pasos para configurar el proyecto de rol de trabajo de Hola.
7. En **el Explorador de soluciones**, en **Roles** en el proyecto de servicio de nube de hello, haga clic en **ContosoAdsWorker** y, a continuación, haga clic en **propiedades**.

    ![Role properties](./media/cloud-services-dotnet-get-started/rolepropertiesworker.png)
8. Haga clic en hello **configuración** ficha.
9. Cambio **configuración del servicio** demasiado**nube**.
10. Seleccione hello **valor** field para hello `ContosoAdsDbConnectionString` establecer y, a continuación, pegue la cadena de conexión de Hola que copió de la sección anterior de Hola de tutorial Hola.

     ![Database connection string for worker role](./media/cloud-services-dotnet-get-started/workerdbcs.png)
11. Guarde los cambios.  

### <a name="configure-hello-solution-toouse-your-azure-storage-account-when-it-runs-in-azure"></a>Configurar la cuenta de almacenamiento de Azure de hello solución toouse cuando se ejecuta en Azure
Cadenas de conexión de cuenta de almacenamiento de Azure para proyecto de rol web de Hola y proyecto de rol de trabajo de Hola se almacenan en la configuración del entorno en el proyecto de servicio de nube Hola. Para cada proyecto, hay un conjunto independiente de toobe de configuración que se usa cuando la aplicación hello se ejecuta localmente y cuando se ejecuta en la nube de Hola. Se actualizará la configuración del entorno de nube de Hola para proyectos de rol web y de trabajo.

1. En **el Explorador de soluciones**, haga clic en **ContosoAdsWeb** en **Roles** en hello **ContosoAdsCloudService** del proyecto y, a continuación, haga clic en **Propiedades**.

    ![Role properties](./media/cloud-services-dotnet-get-started/roleproperties.png)
2. Haga clic en hello **configuración** ficha. Hola **configuración del servicio** desplegable cuadro, elija **nube**.

    ![Cloud configuration](./media/cloud-services-dotnet-get-started/sccloud.png)
3. Seleccione hello **StorageConnectionString** entrada y verá un botón de puntos suspensivos (**...** ) situado en el extremo derecho de Hola de línea de saludo. Haga clic en Hola Hola de tooopen de botón de puntos suspensivos **crear la cadena de conexión de la cuenta de almacenamiento** cuadro de diálogo.

    ![Open Connection String Create box](./media/cloud-services-dotnet-get-started/opencscreate.png)
4. Hola **crear cadenas de conexión de almacenamiento** cuadro de diálogo, haga clic en **su suscripción**, elija la cuenta de almacenamiento de Hola que creó anteriormente y, a continuación, haga clic en **Aceptar**. Si no ha iniciado sesión, se le pedirán las credenciales de la cuenta de Azure.

    ![Create Storage Connection String](./media/cloud-services-dotnet-get-started/createstoragecs.png)
5. Guarde los cambios.
6. Seguimiento Hola mismo procedimiento que utilizó para hello `StorageConnectionString` Hola de tooset de cadena de conexión `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` cadena de conexión.

    Esta cadena de conexión se usa para registro.
7. Seguimiento Hola mismo procedimiento que utilizó para hello **ContosoAdsWeb** tooset rol ambas cadenas de conexión para hello **ContosoAdsWorker** rol. No olvide tooset **configuración del servicio** demasiado**nube**.

configuración del entorno de rol de Hola que ha configurado en hello interfaz de usuario de Visual Studio se almacena en hello siguientes archivos de proyecto de hello ContosoAdsCloudService:

* *ServiceDefinition.csdef* -define los nombres de configuración de Hola.
* *ServiceConfiguration.Cloud.cscfg* -proporciona valores para cuando se ejecuta la aplicación hello en la nube de Hola.
* *ServiceConfiguration.Local.cscfg* -proporciona valores para la aplicación hello ejecución localmente.

Por ejemplo, hello ServiceDefinition.csdef incluye Hola siguientes definiciones:

```xml
<ConfigurationSettings>
    <Setting name="StorageConnectionString" />
    <Setting name="ContosoAdsDbConnectionString" />
</ConfigurationSettings>
```

Hello y *ServiceConfiguration.Cloud.cscfg* archivo incluye valores de hello que escribió para la configuración de Visual Studio.

```xml
<Role name="ContosoAdsWorker">
    <Instances count="1" />
    <ConfigurationSettings>
        <Setting name="StorageConnectionString" value="{yourconnectionstring}" />
        <Setting name="ContosoAdsDbConnectionString" value="{yourconnectionstring}" />
        <!-- other settings not shown -->

    </ConfigurationSettings>
    <!-- other settings not shown -->

</Role>
```

Hola `<Instances>` configuración especifica Hola número de máquinas virtuales que Azure ejecutará código de rol de trabajo de hello en. Hola [pasos siguientes](#next-steps) sección incluye vínculos toomore información acerca de cómo escalar horizontalmente un servicio de nube

### <a name="deploy-hello-project-tooazure"></a>Implementar Hola proyecto tooAzure
1. En **el Explorador de soluciones**, contextual hello **ContosoAdsCloudService** proyecto en la nube y, a continuación, seleccione **publicar**.

   ![Publish menu](./media/cloud-services-dotnet-get-started/pubmenu.png)
2. Hola **iniciar sesión en** paso de hello **publicar aplicación de Azure** asistente, haga clic en **siguiente**.

    ![Sign in step](./media/cloud-services-dotnet-get-started/pubsignin.png)
3. Hola **configuración** paso del Asistente de hello, haga clic en **siguiente**.

    ![Settings step](./media/cloud-services-dotnet-get-started/pubsettings.png)

    Hola configuración predeterminada de hello **avanzadas** ficha son válidas para este tutorial. Para obtener información acerca de la ficha Opciones avanzadas de hello, consulte [Asistente para publicar aplicaciones de Azure](http://msdn.microsoft.com/library/hh535756.aspx).
4. Hola **resumen** paso a paso, haga clic en **publicar**.

    ![Summary step](./media/cloud-services-dotnet-get-started/pubsummary.png)

   Hola **Azure Activity Log** ventana se abre en Visual Studio.
5. Haga clic en detalles de implementación de hello flecha derecha icono tooexpand Hola.

    implementación de Hello puede tardar hasta too5 minutos o más toocomplete.

    ![Azure Activity Log window](./media/cloud-services-dotnet-get-started/waal.png)
6. Cuando el estado de implementación de hello finalice, haga clic en hello **dirección URL de la aplicación Web** aplicación de hello toostart.
7. Ahora puede probar aplicación hello por crear, ver y editar algunos de los anuncios, como lo hizo cuando se ejecuta la aplicación hello localmente.

> [!NOTE]
> Cuando termine de probar, eliminar o detener servicio de nube de Hola. Incluso si no está utilizando el servicio de nube de hello, lo acumulados cargos porque se reservan recursos de máquina virtual para él. Y si lo deja ejecutando, cualquiera que encuentre su dirección URL puede crear y ver anuncios. Hola [portal de Azure](https://portal.azure.com), vaya toohello **Introducción** pestaña para el servicio de nube y, a continuación, haga clic en hello **eliminar** situado en la parte superior de Hola de página de Hola. Si solo desea tootemporarily impedir que otras personas tengan acceso a sitio hello, haga clic en **detener** en su lugar. En ese caso, seguirán aplicando costos tooaccrue. Puede seguir un Hola de toodelete procedimiento similar cuenta de almacenamiento y base de datos SQL cuando ya no los necesite.
>
>

## <a name="create-hello-application-from-scratch"></a>Crear aplicación hello desde el principio
Si ya ha descargado [aplicación hello completado](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), hágalo ahora. Podrá copiar archivos de proyecto descargado de hello en nuevo proyecto de Hola.

Crear aplicación Contoso anuncios de Hola implica Hola pasos:

* Crear una solución de Visual Studio para un servicio en la nube.
* Actualizar y agregar paquetes de NuGet.
* Establecer preferencias del proyecto.
* Configurar cadenas de conexión.
* Agregar archivos de código.

Después de crea la solución de hello, podrá revisar el código de hello que es único toocloud proyectos de servicio como blobs de Azure y colas.

### <a name="create-a-cloud-service-visual-studio-solution"></a>Crear una solución de Visual Studio para un servicio en la nube
1. En Visual Studio, elija **nuevo proyecto** de hello **archivo** menú.
2. En panel izquierdo de Hola de hello **nuevo proyecto** cuadro de diálogo, expanda **Visual C#** y elija **nube** plantillas y, a continuación, elija hello **deserviciodenubedeAzure** plantilla.
3. Nombre de proyecto de Hola y solución ContosoAdsCloudService y, a continuación, haga clic en **Aceptar**.

    ![Nuevo proyecto](./media/cloud-services-dotnet-get-started/newproject.png)
4. Hola **nuevo servicio de nube de Azure** diálogo cuadro, agregue un rol web y un rol de trabajo. Nombre de rol web de hello ContosoAdsWeb y el nombre de rol de trabajo de hello ContosoAdsWorker. (Utilice el icono de lápiz Hola de hello panel derecho toochange Hola nombres predeterminados de las funciones hello.)

    ![New Cloud Service Project](./media/cloud-services-dotnet-get-started/newcsproj.png)
5. Cuando vea hello **nuevo proyecto ASP.NET** cuadro de diálogo de rol web de hello, elija la plantilla MVC de hello y, a continuación, haga clic en **Cambiar autenticación**.

    ![Cambiar autenticación](./media/cloud-services-dotnet-get-started/chgauth.png)
6. Hola **Cambiar autenticación** diálogo cuadro, elija **sin autenticación**y, a continuación, haga clic en **Aceptar**.

    ![Sin autenticación](./media/cloud-services-dotnet-get-started/noauth.png)
7. Hola **nuevo proyecto ASP.NET** cuadro de diálogo, haga clic en **Aceptar**.
8. En **el Explorador de soluciones**, haga clic en la solución de hello (no de uno de los proyectos de hello) y elija **Add - nuevo proyecto**.
9. Hola **Agregar nuevo proyecto** diálogo cuadro, elija **Windows** en **Visual C#** en Hola panel izquierdo y, a continuación, haga clic en hello **biblioteca de clases** plantilla.  
10. Proyecto de hello Name *ContosoAdsCommon*y, a continuación, haga clic en **Aceptar**.

    Necesita tooreference Hola Entity Framework hello y contexto de modelo de datos de proyectos de rol web y de trabajo. Como alternativa, puede definir clases relacionadas con EF de hello en proyecto de rol web de Hola y hacer referencia a ese proyecto desde el proyecto de rol de trabajo de Hola. Pero en el enfoque alternativo de hello, su proyecto de rol de trabajo tendría un ensamblados de referencia de tooweb que no es necesario.

### <a name="update-and-add-nuget-packages"></a>Actualizar y agregar paquetes de NuGet
1. Abra hello **administrar paquetes de NuGet** cuadro de diálogo de solución de Hola.
2. Hola parte superior de ventana hello, seleccione **actualizaciones**.
3. Busque hello *WindowsAzure.Storage* del paquete y si se encuentra en la lista de hello, selecciónela y seleccione tooupdate de proyectos web y de trabajo de hello en y, a continuación, haga clic en **actualización**.

    biblioteca de cliente de almacenamiento de Hola se actualiza con más frecuencia que las plantillas de proyecto de Visual Studio, por lo que a menudo encontrará esa versión de hello en un toobe de necesidades de proyecto recién creado actualizado.
4. Hola parte superior de ventana hello, seleccione **examinar**.
5. Buscar hello *EntityFramework* NuGet empaquetar e instalarlo en los tres proyectos.
6. Buscar hello *Microsoft.WindowsAzure.ConfigurationManager* NuGet empaquetar e instalarlo en el proyecto de rol de trabajo de Hola.

### <a name="set-project-references"></a>Establecimiento de preferencias del proyecto
1. Hola ContosoAdsWeb proyecto, establecer una referencia de proyecto de ContosoAdsCommon toohello. Haga clic en proyecto de hello ContosoAdsWeb y, a continuación, haga clic en **referencias** - **agregar referencias**. Hola **Administrador de referencias** cuadro de diálogo, seleccione **solución – proyectos** en hello panel izquierdo, seleccione **ContosoAdsCommon**y, a continuación, haga clic en **Aceptar**.
2. Hola ContosoAdsWorker proyecto, establecer una referencia de proyecto de ContosAdsCommon toohello.

    ContosoAdsCommon contendrá Hola datos modelo y el contexto de clase de Entity Framework, que se usará en ambos Hola front-end y back-end.
3. En proyectos de ContosoAdsWorker hello, establezca una referencia demasiado`System.Drawing`.

    Hola back-end tooconvert imágenes toothumbnails usa este ensamblado.

### <a name="configure-connection-strings"></a>Configurar cadenas de conexión
En esta sección configurará Azure Storage y cadenas de conexión de SQL para pruebas locales. instrucciones de implementación de Hello anteriormente en el tutorial de Hola explica cómo tooset conexión Hola cadenas para cuando hello aplicación se ejecuta en la nube de Hola.

1. Proyecto de ContosoAdsWeb de hello, archivo Web.config de la aplicación de hello abierto y siguiente de hello insert `connectionStrings` elemento después de hello `configSections` elemento.

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    Si va a usar Visual Studio 2015 o una versión superior, sustituya "v11.0" por "MSSQLLocalDB".
2. Guarde los cambios.
3. En el proyecto de ContosoAdsCloudService hello, haga clic en ContosoAdsWeb en **Roles**y, a continuación, haga clic en **propiedades**.

    ![Role properties](./media/cloud-services-dotnet-get-started/roleproperties.png)
4. Hola **ContosAdsWeb [rol]** ventana Propiedades, haga clic en hello **configuración** ficha y, a continuación, haga clic en **Agregar configuración**.

    Deje **configuración del servicio** establecido demasiado**todas las configuraciones de**.
5. Agregue un nuevo valor llamado *StorageConnectionString*. Establecer **tipo** demasiado*ConnectionString*y establezca **valor** demasiado*UseDevelopmentStorage = true*.

    ![New connection string](./media/cloud-services-dotnet-get-started/scall.png)
6. Guarde los cambios.
7. Seguimiento Hola mismo tooadd procedimiento una cadena de conexión de almacenamiento de propiedades de la función ContosoAdsWorker Hola.
8. Aún en hello **ContosoAdsWorker [rol]** ventana Propiedades, agregue otra cadena de conexión:

   * Nombre: ContosoAdsDbConnectionString
   * Tipo: String
   * Valor: Pegar Hola misma cadena de conexión utilizada para el proyecto de rol web de Hola. (el siguiente ejemplo de Hola es para Visual Studio 2013. No olvide toochange Hola origen de datos si se copia en este ejemplo y que está utilizando Visual Studio 2015 o superior.)

       ```
       Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;
       ```

### <a name="add-code-files"></a>Agregar archivos de código
En esta sección, copie los archivos de código de solución de hello descargado en la nueva solución de Hola. Hello las secciones siguientes se muestra y explica los elementos clave de este código.

tooadd archivos tooa proyecto o una carpeta, proyecto de Hola de menú contextual o carpeta y haga clic en **agregar** - **elemento existente**. Seleccione los archivos de Hola que desee y, a continuación, haga clic en **agregar**. Si se le pregunta si desea que tooreplace los archivos existentes, haga clic en **Sí**.

1. En proyectos de ContosoAdsCommon hello, elimine hello *Class1.cs* de archivos y agregar en su lugar hello *Ad.cs* y *ContosoAdscontext.cs* archivos de hello descargan el proyecto.
2. En proyecto de ContosoAdsWeb de hello, agregue Hola siguientes archivos de proyecto Hola descargado.

   * *Global.asax.cs*.  
   * Hola *Views\Shared* carpeta:  *\_Layout.cshtml*.
   * Hola *Views\Home* carpeta: *Index.cshtml*.
   * Hola *controladores* carpeta: *AdController.cs*.
   * Hola *Views\Ad* carpeta (crear carpeta de hello en primer lugar): cinco *.cshtml* archivos.
3. En hello ContosoAdsWorker proyecto, agregue *WorkerRole.cs* de hello descargaste el proyecto.

Ahora puede compilar y ejecutar la aplicación hello tal como se indica anteriormente en el tutorial de Hola y aplicación hello usará la base de datos local y los recursos de emulador de almacenamiento.

Hello las secciones siguientes explican el código de hello tooworking relacionado con Hola entorno de Azure, blobs y colas. Este tutorial no se explica cómo los controladores MVC toocreate y vistas mediante la técnica scaffolding, cómo toowrite código de Entity Framework que funciona con bases de datos de SQL Server o conceptos básicos de saludo de la programación asincrónica en ASP.NET 4.5. Para obtener información acerca de estos temas, vea Hola recursos siguientes:

* [Introducción a MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [Introducción a EF 6 y MVC 5](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc)
* [Programación de tooasynchronous de introducción en .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).

### <a name="contosoadscommon---adcs"></a>ContosoAdsCommon - Ad.cs
archivo de Hello Ad.cs define una enumeración de categorías de ad y una clase de entidad POCO para obtener información de ad.

```csharp
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
```

### <a name="contosoadscommon---contosoadscontextcs"></a>ContosoAdsCommon - ContosoAdsContext.cs
Hola ContosoAdsContext clase especifica que se utiliza la clase de Ad de hello en una colección de DbSet, que Entity Framework, se almacenará en una base de datos SQL.

```csharp
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
```

clase Hello tiene dos constructores. Hola primero de ellos participa en el proyecto web de Hola y especifica el nombre de Hola de una cadena de conexión que se almacena en el archivo Web.config de hello. segundo constructor de Hello permite toopass en la cadena de conexión real de hello utilizada por el proyecto de rol de trabajo de hello, puesto que no tiene un archivo Web.config. Se ha visto anteriormente donde se almacenó esta cadena de conexión y podrá ver más adelante cómo código de hello recupera la cadena de conexión de hello cuando crea una instancia de clase de DbContext Hola.

### <a name="contosoadsweb---globalasaxcs"></a>ContosoAdsWeb - Global.asax.cs
Código que se llama desde hello `Application_Start` método crea un *imágenes* contenedor de blobs y una *imágenes* cola si todavía no existen. Esto garantiza que cada vez que empiece a usar una cuenta de almacenamiento, o empezar a usar el emulador de almacenamiento de hello en un equipo nuevo, cola y el contenedor de blobs necesarios Hola se creará automáticamente.

Hola cuenta de almacenamiento de toohello de código obtiene acceso mediante el uso de la cadena de conexión de almacenamiento de Hola de hello *.cscfg* archivo.

```csharp
var storageAccount = CloudStorageAccount.Parse
    (RoleEnvironment.GetConfigurationSettingValue("StorageConnectionString"));
```

A continuación, obtiene una referencia toohello *imágenes* contenedor de blobs, crea el contenedor de hello si aún no existe, y establece permisos en el nuevo contenedor de Hola de acceso. De forma predeterminada, nuevos contenedores solo permiten a los clientes con la cuenta de almacenamiento de blobs de tooaccess de credenciales. sitio Web de Hello necesita Hola blobs toobe público para que pueden mostrar imágenes con direcciones URL que blobs de imagen toohello de punto.

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
var imagesBlobContainer = blobClient.GetContainerReference("images");
if (imagesBlobContainer.CreateIfNotExists())
{
    imagesBlobContainer.SetPermissions(
        new BlobContainerPermissions
        {
            PublicAccess =BlobContainerPublicAccessType.Blob
        });
}
```

Un código similar Obtiene una referencia toohello *imágenes* poner en cola y crea una nueva cola. En este caso no es necesario cambios de permiso.

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
var imagesQueue = queueClient.GetQueueReference("images");
imagesQueue.CreateIfNotExists();
```

### <a name="contosoadsweb---layoutcshtml"></a>ContosoAdsWeb - \_Layout.cshtml
Hola *_Layout.cshtml* archivo establece el nombre de la aplicación hello en hello encabezado y pie y crea una entrada de menú "Anuncios".

### <a name="contosoadsweb---viewshomeindexcshtml"></a>ContosoAdsWeb - Views\Home\Index.cshtml
Hola *Views\Home\Index.cshtml* archivo muestra los vínculos de categoría en la página de inicio de Hola. vínculos de Hello pasan el valor entero Hola Hola `Category` enumeración en una página de índice de anuncios de toohello variable de cadena de consulta.

```razor
<li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
<li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
<li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
<li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>
```

### <a name="contosoadsweb---adcontrollercs"></a>ContosoAdsWeb - AdController.cs
Hola *AdController.cs* archivo, llamadas de constructor Hola Hola `InitializeStorage` objetos de biblioteca de cliente de almacenamiento de Azure de toocreate del método que proporcionan una API para trabajar con blobs y colas.

A continuación, el código de hello Obtiene una referencia toohello *imágenes* contenedor de blob como vimos anteriormente en *Global.asax.cs*. Mientras hace eso, establece una [directiva de reintentos](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) apropiada para una aplicación web. Directiva de reintentos de retroceso exponencial de Hello predeterminada podría dejar de responder hello web app para más de un minuto en varios intentos para un error transitorio. Directiva de reintentos de Hello especificada aquí espera tres segundos después de cada uno de ellos probar para una toothree intentos.

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesBlobContainer = blobClient.GetContainerReference("images");
```

Un código similar Obtiene una referencia toohello *imágenes* cola.

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesQueue = queueClient.GetQueueReference("images");
```

La mayoría del código de controlador de hello es típico para trabajar con un modelo de datos de Entity Framework mediante una clase DbContext. Una excepción es hello HttpPost `Create` método, que carga un archivo y lo guarda en el almacenamiento de blobs. enlazador de modelos de Hello proporciona un [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) toohello método del objeto.

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<ActionResult> Create(
    [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
    HttpPostedFileBase imageFile)
```

Si el usuario de hello seleccionó un tooupload de archivo, código de hello carga el archivo hello, lo guarda en un blob y actualiza el registro de base de datos de Ad de hello con una dirección URL que señala toohello blob.

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    blob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = blob.Uri.ToString();
}
```

Hello código Hola carga es Hola `UploadAndSaveBlobAsync` método. Crea un nombre GUID para el blob de hello, cargas y archivo de hello guarda y devuelve un blob de referencia toohello guardado.

```csharp
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
```

Después de hello HttpPost `Create` método carga un blob y Hola de las actualizaciones de base de datos, crea un tooinform de mensaje de cola ese proceso de back-end que está lista para la vista en miniatura de conversión tooa una imagen.

```csharp
string queueMessageString = ad.AdId.ToString();
var queueMessage = new CloudQueueMessage(queueMessageString);
await queue.AddMessageAsync(queueMessage);
```

Hola código de hello HttpPost `Edit` método es similar, salvo que si el usuario de hello selecciona un nuevo archivo de imagen deben eliminarse los blobs que ya existen.

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    await DeleteAdBlobsAsync(ad);
    imageBlob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = imageBlob.Uri.ToString();
}
```

el ejemplo siguiente se Hello muestra código de hello blobs se elimina cuando se elimina un anuncio.

```csharp
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
```

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a>ContosoAdsWeb - Views\Ad\Index.cshtml y Details.cshtml
Hola *Index.cshtml* archivo muestra vistas en miniatura con hello otros datos de ad.

```razor
<img src="@Html.Raw(item.ThumbnailURL)" />
```

Hola *Details.cshtml* archivo muestra la imagen a tamaño completo Hola.

```razor
<img src="@Html.Raw(Model.ImageURL)" />
```

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a>ContosoAdsWeb - Views\Ad\Create.cshtml y Edit.cshtml
Hola *Create.cshtml* y *Edit.cshtml* archivos especifican formulario codificación que permite Hola Hola de controlador tooget `HttpPostedFileBase` objeto.

```razor
@using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))
```

Un `<input>` elemento indica Hola explorador tooprovide un cuadro de diálogo de selección de archivo.

```razor
<input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />
```

### <a name="contosoadsworker---workerrolecs---onstart-method"></a>ContosoAdsWorker - WorkerRole.cs - Método OnStart
entorno de rol de trabajador de Azure de Hello llama hello `OnStart` método Hola `WorkerRole` clase al rol de trabajo de hello es introducción y llama hello `Run` método cuando hello `OnStart` método finaliza.

Hola `OnStart` método obtiene la cadena de conexión de base de datos de Hola de hello *.cscfg* archivo y lo pasa en la clase de Entity Framework DbContext toohello. proveedor de SQLClient Hola se utiliza de forma predeterminada, por lo que el proveedor hello no tiene toobe especificado.

```csharp
var dbConnString = CloudConfigurationManager.GetSetting("ContosoAdsDbConnectionString");
db = new ContosoAdsContext(dbConnString);
```

Después de eso, método hello Obtiene una cuenta de almacenamiento de toohello de referencia y crea la cola y el contenedor de blobs de hello si no existen. código de Hello para el que es toowhat similar ya vio en el rol web de hello `Application_Start` método.

### <a name="contosoadsworker---workerrolecs---run-method"></a>ContosoAdsWorker - WorkerRole.cs - Método Run
Hola `Run` método se llama cuando hello `OnStart` método finaliza su tarea de inicialización. método Hello ejecuta un bucle infinito que inspecciona los nuevos mensajes de cola y procesa cuando vayan llegando.

```csharp
public override void Run()
{
    CloudQueueMessage msg = null;

    while (true)
    {
        try
        {
            msg = this.imagesQueue.GetMessage();
            if (msg != null)
            {
                ProcessQueueMessage(msg);
            }
            else
            {
                System.Threading.Thread.Sleep(1000);
            }
        }
        catch (StorageException e)
        {
            if (msg != null && msg.DequeueCount > 5)
            {
                this.imagesQueue.DeleteMessage(msg);
            }
            System.Threading.Thread.Sleep(5000);
        }
    }
}
```

Después de cada iteración del bucle de hello, si se encuentra ningún mensaje de cola, programa hello en suspensión durante un segundo. Esto impide que el rol de trabajo de hello incurrir en costes excesivos de la transacción del almacenamiento y tiempo de CPU. Hola, equipo de asesoramiento al cliente de Microsoft cuente una historia acerca de un desarrollador que se haya olvidado tooinclude, implementado tooproduction y deja de vacaciones. Al que obtuvo, su supervisión son más caras que las vacaciones de Hola.

A veces contenido Hola de un mensaje de la cola provoca un error en el procesamiento. Esto se denomina una *mensaje dudoso*, y si simplemente se registra un error y reiniciar bucle hello, interminablemente intente tooprocess ese mensaje.  Por lo tanto, el bloque catch de hello incluye if instrucción que comprueba toosee cuántas veces aplicación hello probada tooprocess Hola mensaje actual y si han pasado más de 5 veces, mensaje de saludo se elimina de la cola de Hola.

`ProcessQueueMessage` se llama cuando se encuentra un mensaje de cola.

```csharp
private void ProcessQueueMessage(CloudQueueMessage msg)
{
    var adId = int.Parse(msg.AsString);
    Ad ad = db.Ads.Find(adId);
    if (ad == null)
    {
        throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", adId.ToString()));
    }

    CloudBlockBlob inputBlob = this.imagesBlobContainer.GetBlockBlobReference(ad.ImageURL);

    string thumbnailName = Path.GetFileNameWithoutExtension(inputBlob.Name) + "thumb.jpg";
    CloudBlockBlob outputBlob = this.imagesBlobContainer.GetBlockBlobReference(thumbnailName);

    using (Stream input = inputBlob.OpenRead())
    using (Stream output = outputBlob.OpenWrite())
    {
        ConvertImageToThumbnailJPG(input, output);
        outputBlob.Properties.ContentType = "image/jpeg";
    }

    ad.ThumbnailURL = outputBlob.Uri.ToString();
    db.SaveChanges();

    this.imagesQueue.DeleteMessage(msg);
}
```

Este código lee la dirección URL de imagen de hello base de datos tooget hello, convierte la miniatura de la imagen tooa hello, guarda la miniatura de hello en un blob, actualiza la base de datos de hello con la dirección URL del blob en miniatura de Hola y elimina el mensaje de bienvenida de cola.

> [!NOTE]
> Hola código de hello `ConvertImageToThumbnailJPG` método usa las clases en el espacio de nombres de hello System.Drawing para simplificar el trabajo. Sin embargo, las clases de hello en este espacio de nombres se diseñaron para su uso con Windows Forms. No se admiten para usarse en un servicio de Windows o ASP.NET. Para más información acerca de las opciones de procesamiento de imagen, consulte [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) (Generación de imagen dinámica) y [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na) (Profundización en el cambio de tamaño de imágenes).
>
>

## <a name="troubleshooting"></a>Solución de problemas
En caso de que algo no funciona mientras que siga las instrucciones de hello en este tutorial, aquí se muestran algunos errores comunes y cómo tooresolve ellos.

### <a name="serviceruntimeroleenvironmentexception"></a>ServiceRuntime.RoleEnvironmentException
Hola `RoleEnvironment` objeto proporciona Azure cuando se ejecuta una aplicación en Azure o cuando se ejecuta localmente mediante Hola emulador de proceso de Azure.  Si recibe este error cuando se ejecuta localmente, asegúrese de que haya establecido como proyecto de inicio de hello proyecto ContosoAdsCloudService de Hola. Esta acción configura Hola proyecto toorun mediante Hola emulador de proceso de Azure.

Uno de los aspectos de Hola Hola aplicación usa Hola RoleEnvironment de Azure para es tooget valores de cadena de conexión de Hola que se almacenan en hello *.cscfg* archivos, por lo que otra causa de esta excepción es una cadena de conexión que faltan. Asegúrese de que ha creado configuración StorageConnectionString de Hola para tanto en la nube y las configuraciones locales en hello ContosoAdsWeb proyecto y había creado ambas cadenas de conexión para ambas configuraciones en el proyecto de ContosoAdsWorker Hola. Si lo hace un **buscar todos** búsqueda para StorageConnectionString en toda la solución hello, que debería verla 9 veces en 6 archivos.

### <a name="cannot-override-tooport-xxx-new-port-below-minimum-allowed-value-8080-for-protocol-http"></a>No se puede reemplazar tooport xxx. El nuevo puerto está por debajo del valor mínimo permitido de 8080 para el protocolo http.
Intente cambiar el número de puerto de hello usa Hola proyecto de web. Haga clic en proyecto de hello ContosoAdsWeb y, a continuación, haga clic en **propiedades**. Haga clic en hello **Web** ficha y, a continuación, cambie el número de puerto de hello en hello **dirección Url del proyecto** configuración.

Para otra alternativa que se resuelva el problema de hello, vea Hola pasos de la sección.

### <a name="other-errors-when-running-locally"></a>Otros errores al realizar la ejecución localmente
En la nube predeterminado nuevo proyectos de servicio usan Hola de toosimulate express de emulador de proceso de Azure de hello entorno de Azure. Se trata de una versión ligera de emulador de proceso completo de hello y, en algunos Hola condiciones emulador completo funcionará cuando versión express de hello no lo hace.  

toochange Hola emulador completo de proyecto toouse hello, haga clic en proyecto de hello ContosoAdsCloudService y, a continuación, haga clic en **propiedades**. Hola **propiedades** ventana, haga clic en hello **Web** ficha y, a continuación, haga clic en hello **usar emulador completo** botón de radio.

En la aplicación Hola de toorun de pedidos con el emulador completo de hello, tiene tooopen Visual Studio con privilegios de administrador.

## <a name="next-steps"></a>Pasos siguientes
aplicación Contoso anuncios de Hola se intencionadamente ha conservado simple para obtener un tutorial de introducción. Por ejemplo, no implementa [inyección de dependencia](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) o hello [repositorio y una unidad de trabajan patrones](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), pero no ocurre así [usar una interfaz para el registro](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), no usa [ EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) datos toomanage cambios en el modelo o [resistencia de conexión de EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage transitorio errores de red y así sucesivamente.

A continuación, incluimos algunas aplicaciones de ejemplo de servicio de nube que muestran más prácticas de codificación de mundo real, enumeradas de menos complejo toomore complejo:

* [PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31). Un concepto similar tooContoso anuncios pero implementa más características y prácticas de codificación más reales.
* [Aplicación de niveles múltiples de servicios en la nube de Azure con Tablas, Colas y Blobs.](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36)Presenta las tablas de Almacenamiento de Azure, así como blobs y colas. Basadas en una versión anterior del SDK de Azure para. Se basa en una versión anterior de hello Azure SDK para. NET, requerirá algunos toowork modificaciones con la versión actual de Hola.
* [Fundamentos de servicios en la nube en Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649). Un ejemplo completo que muestra una amplia gama de procedimientos recomendados, generado por el grupo de Microsoft Patterns and Practices de Hola.

Para obtener información general sobre el desarrollo de la nube de hello, consulte [creación de aplicaciones de nube reales con Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).

Para un almacenamiento de vídeo de introducción tooAzure procedimientos recomendados y patrones, vea [almacenamiento de Microsoft Azure: ¿qué es nuevo, prácticas recomendadas y patrones](http://channel9.msdn.com/Events/Build/2014/3-628).

Para obtener más información, vea Hola recursos siguientes:

* [Servicios de nube de Azure, parte 1: Introducción](http://justazure.com/microsoft-azure-cloud-services-part-1-introduction/)
* [Cómo toomanage los servicios de nube](cloud-services-how-to-manage.md)
* [Azure Storage](/documentation/services/storage/)
* [¿Cómo toochoose una nube de proveedor de servicios](https://azure.microsoft.com/overview/choosing-a-cloud-service-provider/)
