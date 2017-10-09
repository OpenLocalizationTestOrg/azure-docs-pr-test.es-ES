---
title: "recursos locales de aaaAccess usando conexiones híbridas en el servicio de aplicación de Azure"
description: "Creación de una conexión entre una aplicación web en Servicio de aplicaciones de Azure y un recurso local que usa un puerto TCP estático"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: a46ed26b-df8e-4fc3-8e05-2d002a6ee508
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: cephalin
ms.openlocfilehash: de7c57b94f4bd6250a93757817178e8455daae4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="access-on-premises-resources-using-hybrid-connections-in-azure-app-service"></a>Acceso a recursos locales mediante conexiones híbridas en el Servicio de aplicaciones de Azure
Puede conectar un recurso de local de tooany de aplicación de servicio de aplicaciones de Azure que usa un puerto TCP estático, como SQL Server, MySQL, las API Web de HTTP y mayoría de los servicios Web personalizados. Este artículo muestra cómo toocreate una conexión híbrida entre el servicio de aplicaciones y una base de datos de SQL Server local.

> [!NOTE]
> parte de las aplicaciones Web de Hola de característica de conexiones híbridas de hello solo está disponible en hello [Portal de Azure](https://portal.azure.com). toocreate una conexión de servicios de BizTalk, consulte [conexiones híbridas](http://go.microsoft.com/fwlink/p/?LinkID=397274). 
> 
> Este contenido también aplica a aplicaciones de tooMobile en el servicio de aplicación de Azure. 
> 
> 

## <a name="prerequisites"></a>Requisitos previos
* Una suscripción de Azure. Para obtener una suscripción gratuita, consulte [Prueba gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/). 
  
    Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
* toouse un local SQL Server o base de datos de SQL Server Express con una conexión híbrida, TCP/IP debe toobe habilitado en un puerto estático. Se recomienda usar una instancia predeterminada en SQL Server porque usa el puerto estático 1433. Para obtener información sobre cómo instalar y configurar SQL Server Express para usarlo con conexiones híbridas, vea [tooan conectar en SQL Server local desde un sitio web de Azure usando conexiones híbridas](http://go.microsoft.com/fwlink/?LinkID=397979).
* equipo de Hello en el que instale a agente de administrador de conexiones híbridas local Hola que se describe más adelante en este artículo:
  
  * Debe ser capaz de tooconnect tooAzure a través del puerto 5671
  * Debe ser capaz de tooreach hello *hostname*:*portnumber* de su recurso local. 

> [!NOTE]
> pasos de Hello en este artículo se supone que está usando explorador Hola desde equipo Hola que hospedará el agente de conexión híbrida de hello local.
> 
> 

## <a name="create-a-web-app-in-hello-azure-portal"></a>Crear una aplicación web en hello Portal de Azure
> [!NOTE]
> Si ya ha creado una aplicación web o aplicación móvil back-end en hello Portal de Azure que quiere toouse de este tutorial, puede pasar demasiado[crear una conexión híbrida y un BizTalk Service](#CreateHC) e iniciar desde allí.
> 
> 

1. En la esquina izquierda superior de Hola de hello [Portal de Azure](https://portal.azure.com), haga clic en **New** > **Web y móvil** > **aplicación Web**.
   
    ![New web app][NewWebsite]
2. En hello **aplicación Web** hoja, proporcione una dirección URL y haga clic en **crear**. 
   
    ![Website name][WebsiteCreationBlade]
3. Después de unos segundos, se crea la aplicación web de hello y aparece su hoja de la aplicación web. hoja de Hello es un panel puede desplazar verticalmente que le permite administrar el sitio.
   
    ![Website running][WebSiteRunningBlade]
4. sitio de hello tooverify está activo, puede hacer clic en hello **examinar** página predeterminada de icono toodisplay Hola.
   
    ![Haga clic en Examinar toosee su aplicación web][Browse]
   
    ![Página de aplicación web predeterminada][DefaultWebSitePage]

A continuación, creará una conexión híbrida y un servicio de BizTalk para la aplicación web de Hola.

<a name="CreateHC"></a>

## <a name="create-a-hybrid-connection-and-a-biztalk-service"></a>Creación de una conexión híbrida y un servicio de BizTalk
1. En la hoja de la aplicación web, haga clic en **Todas las configuraciones** > **Redes** > **Configurar los puntos de conexión híbrida**.
   
    ![Conexiones híbridas][CreateHCHCIcon]
2. En la hoja de conexiones híbridas de hello, haga clic en **agregar**.
   
    <!-- ![Add a hybrid connnection][CreateHCAddHC]
   -->
3. Hola **agregar una conexión híbrida** abre la hoja.  Puesto que se trata de la primera conexión híbrida, Hola **conexión híbrida nueva** opción está preseleccionada y Hola **crear conexión híbrida** hoja se abre automáticamente.
   
    ![Create a hybrid connection][TwinCreateHCBlades]
   
    En hello **hoja de conexión híbrida crear**:
   
   * Para **nombre**, proporcione un nombre para la conexión de Hola.
   * Para **Hostname**, escriba Hola nombre del equipo local de Hola que hospeda el recurso.
   * Para **puerto**, escriba Hola número de puerto que el recurso local utiliza (1433 para una instancia predeterminada de SQL Server).
   * Haga clic en **Servicio de Biz Talk**
4. Hola **crear servicio de BizTalk** abre la hoja. Escriba un nombre para el servicio de BizTalk de hello y, a continuación, haga clic en **Aceptar**.
   
    ![Crear servicio de BizTalk][CreateHCCreateBTS]
   
    Hola **crear servicio de BizTalk** hoja se cierra y se devuelven toohello **crear conexión híbrida** hoja.
5. En hello crear híbrida conexión hoja, haga clic **Aceptar**. 
   
    ![Haga clic en Aceptar][CreateBTScomplete]
6. Cuando se completa el proceso de hello, área de notificaciones de Hola Hola Portal le informa de que conexión Hola se ha creado correctamente.
   
    <!--- TODO
   
    Everything fails at this step. I can't create a BizTalk service in hello dogfood portal. I switch toohello classic portal
    (full portal) and created hello BizTalk service but it doesn't seem toolet you connnect them - When you finish the
    Create hybrid conn step, you get hello following error
    Failed toocreate hybrid connection RelecIoudHC. hello 
    resource type could not be found in hello namespace 
    'Microsoft.BizTaIkServices for api version 2014-06-01'.
   
    hello error indicates it couldn't find hello type, not hello instance.
    ![Success notification][CreateHCSuccessNotification]
    -->
7. En la hoja de la aplicación web hello, Hola **conexiones híbridas** icono muestra ahora que se ha creado 1 conexión híbrida.
   
    ![One hybrid connection created][CreateHCOneConnectionCreated]

En este momento, ha completado una parte importante de la infraestructura de conexión de hello en la nube híbrida. A continuación, creará la parte local correspondiente.

<a name="InstallHCM"></a>

## <a name="install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a>Instalar Hola local Administrador de conexiones híbridas toocomplete Hola conexión
1. En la hoja de la aplicación de hello web, haga clic en **toda la configuración de** > **red** > **configurar los extremos de conexión híbrida**. 
   
    ![Hybrid connections icon][HCIcon]
2. En hello **conexiones híbridas** hoja, hello **estado** recientemente agrega la columna de hello muestra de extremo **no conectado**. Haga clic en tooconfigure de conexión de Hola.
   
    ![No conectado][NotConnected]
   
    se abre la hoja de conexión híbrida de Hola.
   
    ![NotConnectedBlade][NotConnectedBlade]
3. En la hoja de hello, haga clic en **el programa de instalación de agente de escucha**.
   
    ![Click Listener Setup][ClickListenerSetup]
4. Hola **propiedades de conexión híbrida** abre la hoja. En **Administrador de conexiones híbridas local**, elija **haga clic aquí tooinstall**.
   
    ![Haga clic aquí tooinstall][ClickToInstallHCM]
5. Cuadro de diálogo de advertencia de seguridad ejecutar aplicación Hola, elija **ejecutar** toocontinue.
   
    ![Elija toocontinue de ejecución][ApplicationRunWarning]
6. Hola **User Account Control** cuadro de diálogo, elija **Sí**.
   
   ![Choose Yes][UAC]
7. Hola, Administrador de conexiones híbridas se descargará e instalará automáticamente. 
   
    ![Instalación][HCMInstalling]
8. Cuando se haya completado la instalación de hello, haga clic en **cerrar**.
   
    ![Click Close][HCMInstallComplete]
   
    En hello **conexiones híbridas** hoja, hello **estado** columna muestra ahora **conectado**. 
   
    ![Connected Status][HCStatusConnected]

Ahora esa infraestructura de conexión híbrida Hola está completa, puede crear una aplicación híbrida que lo utilice. 

> [!NOTE]
> Hello las secciones siguientes muestran cómo toouse una conexión híbrida con un proyecto de back-end de .NET de aplicaciones móviles.
> 
> 

## <a name="configure-hello-mobile-app-net-backend-project-tooconnect-toohello-sql-server-database"></a>Configurar Hola Mobile aplicación back-end proyecto tooconnect toohello SQL Server base de datos .NET
En Servicio de aplicaciones, un proyecto de back-end .NET de Aplicaciones móviles es simplemente una aplicación web de ASP.NET con un SDK de Aplicaciones móviles adicional instalado e inicializado. toouse la aplicación web como un back-end de aplicaciones móviles, debe [descargar e inicializar back-end de hello Mobile aplicaciones .NET SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).  

Para las aplicaciones móviles, también necesita toodefine una cadena de conexión de base de datos de hello local y modificar Hola back-end toouse esta conexión. 

1. En el Explorador de soluciones en Visual Studio, el archivo Web.config de hello abierto para el back-end de .NET de aplicación móvil, busque hello **connectionStrings** sección, agregue una nueva entrada de SqlClient como siguiente hello, qué toohello puntos SQL local Base de datos del servidor:
   
        <add name="OnPremisesDBConnection"
         connectionString="Data Source=OnPremisesServer,1433;
         Initial Catalog=OnPremisesDB;
         User ID=HybridConnectionLogin;
         Password=<**secure_password**>;
         MultipleActiveResultSets=True"
         providerName="System.Data.SqlClient" />
   
    Recuerde tooreplace `<**secure_password**>` en esta cadena con la contraseña de Hola que creó para *HybridConnectionLogin*.
2. Haga clic en **guardar** en el archivo Web.config de Visual Studio toosave Hola.
   
   > [!NOTE]
   > Esta configuración de conexión se utiliza cuando se ejecuta en el equipo local de Hola. Cuando se ejecuta en Azure, esta configuración es reemplazada por configuración de conexión de hello definido en el portal de Hola.
   > 
   > 
3. Expanda hello **modelos** carpetas y archivos de modelo de datos abierto hello, que finaliza en *Context.cs*.
4. Modificar hello **DbContext** toopass de constructor de instancia Hola valor `OnPremisesDBConnection` toohello base **DbContext** constructor, toohello similar siguiente fragmento de código:
   
        public class hybridService1Context : DbContext
        {
            public hybridService1Context()
                : base("OnPremisesDBConnection")
            {
            }
        }
   
    servicio de Hello ahora va a usar base de datos de hello nueva conexión toohello SQL Server.

## <a name="update-hello-mobile-app-backend-toouse-hello-on-premises-connection-string"></a>Actualizar la cadena de conexión local de hello aplicación móvil back-end toouse Hola
A continuación, tendrá que tooadd una configuración de aplicación para esta nueva cadena de conexión para que se puede utilizar de Azure.  

1. Nuevo en hello [portal de Azure](https://portal.azure.com) en el código de hello web aplicación back-end de la aplicación móvil, haga clic en **toda la configuración de**, a continuación, **configuración de la aplicación**.
2. Hola **configuración de aplicación Web** hoja, desplácese hacia abajo demasiado**las cadenas de conexión** y agregue un nuevo **SQL Server** cadena de conexión denominada `OnPremisesDBConnection` con un valor como `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.
   
    Reemplace `<**secure_password**>` con contraseña segura de hello para la base de datos local.
   
    ![Cadena de conexión de la base de datos local](./media/web-sites-hybrid-connection-get-started/set-sql-server-database-connection.png)
3. Presione **guardar** conexión híbrida de toosave hello y cadena de conexión que acaba de crear.

En este momento puede volver a publicar el proyecto de servidor de Hola y probar Hola nueva conexión con los clientes existentes de aplicaciones móviles. Datos se pueden leer y escritos toohello de base de datos local mediante la conexión híbrida de Hola.

<a name="NextSteps"></a>

## <a name="next-steps"></a>Pasos siguientes
* Para obtener información acerca de cómo crear una aplicación web ASP.NET que utiliza una conexión híbrida, consulte [tooan conectar en SQL Server local desde un sitio web de Azure usando conexiones híbridas](http://go.microsoft.com/fwlink/?LinkID=397979). 

### <a name="additional-resources"></a>Recursos adicionales
[Introducción a las conexiones híbridas](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[Josh Twist presenta las conexiones híbridas (vídeo de Channel 9)](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[Sitio web de conexiones híbridas](https://azure.microsoft.com/services/biztalk-services/)

[Servicios de BizTalk: pestañas Panel, Monitor, Escala, Configurar y Conexiones híbridas](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[Creación de una nube híbrida del mundo real con una perfecta portabilidad de aplicaciones (vídeo de Channel 9)](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[Conectar tooan local de SQL Server de servicios móviles de Azure usando conexiones híbridas (vídeo de Channel 9)](http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Connect-to-an-on-premises-SQL-Server-from-Azure-Mobile-Services-using-Hybrid-Connections)

## <a name="whats-changed"></a>Lo que ha cambiado
* Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- IMAGES -->
[New]:./media/web-sites-hybrid-connection-get-started/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-get-started/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-get-started/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-get-started/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-get-started/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-get-started/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-get-started/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-get-started/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-get-started/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-get-started/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-get-started/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-get-started/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-get-started/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-get-started/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-get-started/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-get-started/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-get-started/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-get-started/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-get-started/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-get-started/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-get-started/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-get-started/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-get-started/D10HCStatusConnected.png
