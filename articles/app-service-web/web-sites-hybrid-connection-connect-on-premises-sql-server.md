---
title: "aaaConnect tooon local SQL Server desde una aplicación web en el servicio de aplicaciones de Azure usando conexiones híbridas"
description: "Crear una aplicación web en Microsoft Azure y conectar base de datos de SQL Server de tooan local"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: 2b4e0539-1a0b-4aa1-8a69-b4b053c3b2e5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2016
ms.author: cephalin
ms.openlocfilehash: 2e8f8f7e0b9733cfb0433697615faba4358c6023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-sql-server-from-a-web-app-in-azure-app-service-using-hybrid-connections"></a>Conectar SQL Server local tooon desde una aplicación web en el servicio de aplicación de Azure usando conexiones híbridas
Pueden conectar las conexiones híbridas [servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714) recursos de tooon locales de aplicaciones Web que utilizan un puerto TCP estático. Los recursos admitidos incluyen Microsoft SQL Server, MySQL, API web HTTP, App Service y la mayoría de servicios web personalizados.

En este tutorial, obtendrá información sobre cómo toocreate un servicio de aplicación web aplicación Hola [Portal de Azure](http://go.microsoft.com/fwlink/?LinkId=529715), conectar hello web app tooyour en instalaciones locales SQL Server base de datos mediante la nueva característica de conexión híbrida hello, cree un ASP.NET simple aplicación que usará la conexión híbrida de hello y, implementar Hola aplicación toohello aplicación de servicio de aplicaciones web. Hola completado web app en Azure almacena las credenciales de usuario en una base de datos de pertenencia en una ubicación local. tutorial de Hello no supone ninguna experiencia previa con Azure o ASP.NET.

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
> 
> parte de las aplicaciones Web de Hola de característica de conexiones híbridas de hello solo está disponible en hello [Portal de Azure](https://portal.azure.com). toocreate una conexión de servicios de BizTalk, consulte [conexiones híbridas](http://go.microsoft.com/fwlink/p/?LinkID=397274).  
> 
> 

## <a name="prerequisites"></a>Requisitos previos
toocomplete este tutorial, necesitará Hola después de productos. Todos están disponibles en versión gratuita, así que puede comenzar a desarrollar en Azure completamente gratis.

* **Suscripción de Azure** : para obtener una suscripción gratuita, consulte [Prueba gratuita de Azure](/pricing/free-trial/).
* **Visual Studio 2013** -toodownload una versión de prueba gratuita de Visual Studio 2013, vea [descargas de Visual Studio](http://www.visualstudio.com/downloads/download-visual-studio-vs). Instale esta aplicación antes de continuar.
* **Microsoft .NET Framework 3.5 Service Pack 1**: si su sistema operativo es Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7 o Windows Server 2008 R2, puede habilitar este producto en Panel de control &gt; Programas y características &gt; Activar o desactivar las características de Windows. En caso contrario, puede descargarlo en hello [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).
* **SQL Server 2014 Express con herramientas** -descargar Microsoft SQL Server Express de forma gratuita en hello [página de base de datos de Microsoft Web Platform](http://www.microsoft.com/web/platform/database.aspx). Elija hello **Express** (no LocalDB) versión. Hola **Express with Tools** versión incluye SQL Server Management Studio, que se usará en este tutorial.
* **SQL Server Management Studio Express** : Esto se incluye con SQL Server 2014 Express de hello en la descarga de herramientas se ha mencionado anteriormente, pero si necesita tooinstall se por separado, se puede descargar e instalarlo desde hello [SQL Server Express página de descarga de](http://www.microsoft.com/web/platform/database.aspx).

tutorial de Hola se da por supuesto que tiene una suscripción a Azure que ha instalado Visual Studio 2013, y que ha instalado o habilitado .NET Framework 3.5. Hola tutorial le mostrará cómo tooinstall SQL Server 2014 Express en una configuración que funciona bien con las conexiones híbridas de Azure Hola característica (una instancia predeterminada con un puerto TCP estático). Antes de iniciar el tutorial de hello, descargar SQL Server 2014 Express con herramientas de ubicación de hello que ya se mencionó anteriormente, si no tiene instalado SQL Server.

### <a name="notes"></a>Notas
toouse un local SQL Server o base de datos de SQL Server Express con una conexión híbrida, TCP/IP debe toobe habilitado en un puerto estático. Las instancias predeterminadas de SQL Server usan el puerto estático 1433, mientras que las instancias con nombre no.

equipo de Hello en el que instale el agente de administrador de conexiones híbridas local hello:

* Debe tener conectividad saliente tooAzure sobre:

| Port | Porqué |
| --- | --- |
| 80 |**Obligatorio** para el puerto HTTP, para la validación de certificados y, de forma opcional, para la conectividad de datos. |
| 443 |**Opcional** para la conectividad de datos. Si too443 conectividad saliente no está disponible, se utiliza el puerto TCP 80. |
| 5671 y 9352 |**Recomendado** , pero opcional para la conectividad de datos. Tenga en cuenta que este modo obtiene mayor rendimiento. Si los puertos toothese conectividad saliente no está disponible, se utiliza el puerto TCP 443. |

* Debe ser capaz de tooreach hello *hostname*:*portnumber* de su recurso local.

pasos de Hello en este artículo se supone que está usando explorador Hola desde equipo Hola que hospedará el agente de conexión híbrida de hello local.

Si ya tiene SQL Server instalado en una configuración y en un entorno que cumple las condiciones de Hola se ha descrito anteriormente, puede saltarse lecciones y empezar con [crear una base de datos de SQL Server local](#CreateSQLDB).

<a name="InstallSQL"></a>

## <a name="a-install-sql-server-express-enable-tcpip-and-create-a-sql-server-database-on-premises"></a>A. Instalación de SQL Server Express, habilitación de TCP/IP y creación de una base de datos SQL Server local
Esta sección muestra cómo habilitar TCP/IP tooinstall SQL Server Express y crear una base de datos para que funcione la aplicación web con hello Portal de Azure.

### <a name="install-sql-server-express"></a>Instalación de SQL Server Express
1. tooinstall SQL Server Express, ejecute hello **SQLEXPRWT_x64_ENU.exe** o **SQLEXPR_x86_ENU.exe** archivo que descargó. aparece el Asistente de Hello centro de instalación de SQL Server.
   
    ![SQL Server Install][SQLServerInstall]
2. Elija **nueva instalación SQL Server independiente o agregar la instalación existente de características tooan**. Siga las instrucciones de hello, acepte las opciones predeterminadas hello y la configuración, hasta llegar toohello **configuración de instancia** página.
3. En hello **configuración de instancia** página, elija **instancia predeterminada**.
   
    ![Choose Default Instance][ChooseDefaultInstance]
   
    De forma predeterminada, instancia predeterminada de Hola de SQL Server escucha las solicitudes de clientes de SQL Server en el puerto 1433, que es qué hello conexiones híbridas requiere la característica. Las instancias con nombre usan puertos dinámicos y UDP, que Conexiones híbridas no admite.
4. Acepte los valores predeterminados de hello en hello **configuración del servidor** página.
5. En hello **configuración del motor de base de datos** página, en **modo de autenticación**, elija **modo mixto (autenticación de SQL Server y la autenticación de Windows)**y proporcionar una contraseña.
   
    ![Choose Mixed Mode][ChooseMixedMode]
   
    En este tutorial se usará la autenticación de SQL Server. Estar seguro tooremember Hola por contraseña que proporcione, ya que la necesitará más adelante.
6. Paso a paso a través de rest de Hola de instalación de hello Asistente toocomplete Hola.

### <a name="enable-tcpip"></a>Habilitar TCP/IP
tooenable TCP/IP, se usará el Administrador de configuración de SQL Server, que se instala al instalar SQL Server Express. Siga los pasos de hello en [habilitar el protocolo de red TCP/IP para SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) antes de continuar.

<a name="CreateSQLDB"></a>

### <a name="create-a-sql-server-database-on-premises"></a>Creación de una base de datos de SQL Server local
La aplicación web de Visual Studio requiere una base de datos de pertenencia a la que pueda acceder Azure. Esto requiere una base de datos de SQL Server o SQL Server Express (no Hola LocalDB base de datos que Hola usos de plantilla MVC predeterminada), por lo que podrá crear base de datos de pertenencia de Hola a continuación.

1. En SQL Server Management Studio, conéctese toohello recién instalada de SQL Server. (Si hello **conectar tooServer** cuadro de diálogo no aparece automáticamente, navegue demasiado**Explorador de objetos** en el panel izquierdo de hello, haga clic en **conectar**y, a continuación, haga clic en **Motor de base de datos**.) ![Conectar tooServer][SSMSConnectToServer]
   
    En **Tipo de servidor**, elija **Motor de la base de datos**. Para **nombre del servidor**, puede usar **localhost** Hola de u Hola equipo que está usando. Elija **autenticación de SQL Server**y, a continuación, inicie sesión con el nombre de usuario de sa de Hola y Hola que creó anteriormente.
2. toocreate una nueva base de datos mediante el uso de SQL Server Management Studio, haga clic en **bases de datos** en el Explorador de objetos y, a continuación, haga clic en **nueva base de datos**.
   
    ![Create new database][SSMScreateNewDB]
3. Hola **nueva base de datos** cuadro de diálogo, escriba MembershipDB de nombre de base de datos de hello y, a continuación, haga clic en **Aceptar**.
   
    ![Provide database name][SSMSprovideDBname]
   
    Tenga en cuenta que no realiza ninguna base de datos de toohello de cambios en este momento. información de pertenencia de Hola se agregará automáticamente más tarde mediante la aplicación web cuando se ejecuta.
4. En el Explorador de objetos, si expande **bases de datos**, verá esa base de datos de pertenencia de Hola se ha creado.
   
    ![MembershipDB created][SSMSMembershipDBCreated]

<a name="CreateSite"></a>

## <a name="b-create-a-web-app-in-hello-azure-portal"></a>B. Crear una aplicación web en hello Portal de Azure
> [!NOTE]
> Si ya ha creado una aplicación web en hello Portal de Azure que quiere toouse de este tutorial, puede pasar demasiado[crear una conexión híbrida y un BizTalk Service](#CreateHC) y continuar desde allí.
> 
> 

1. Hola [Portal de Azure](https://portal.azure.com), haga clic en **New** > **Web y móvil** > **aplicación Web**.
   
    ![New button][New]
2. Configure su aplicación web y, a continuación, haga clic en **Crear**.
   
    ![Website name][WebsiteCreationBlade]
3. Después de unos segundos, se crea la aplicación web de hello y aparece su hoja de la aplicación web. hoja de Hello es un panel puede desplazar verticalmente que le permite administrar la aplicación web.
   
    ![Website running][WebSiteRunningBlade]
   
    aplicación web de tooverify hello es en vivo, puede hacer clic en hello **examinar** página predeterminada de icono toodisplay Hola.

A continuación, creará una conexión híbrida y un servicio de BizTalk para la aplicación web de Hola.

<a name="CreateHC"></a>

## <a name="c-create-a-hybrid-connection-and-a-biztalk-service"></a>C. Creación de una conexión híbrida y un servicio de BizTalk
1. Hola Portal, vaya toosettings atrás y haga clic en **red** > **configurar los extremos de conexión híbrida**.
   
    ![Conexiones híbridas][CreateHCHCIcon]
2. En la hoja de conexiones híbridas de hello, haga clic en **agregar** > **conexión híbrida nueva**.
3. En hello **crear conexión híbrida** hoja:
   
   * Para **nombre**, proporcione un nombre para la conexión de Hola.
   * Para **Hostname**, escriba Hola nombre de equipo del equipo de host de SQL Server.
   * Para **puerto**, escriba 1433 (puerto de hello predeterminado para SQL Server).
   * Haga clic en **BizTalk Service** > **nuevo servicio de BizTalk** y escriba un nombre para el servicio de BizTalk de hello.
     
     ![Create a hybrid connection][TwinCreateHCBlades]
4. Haga clic en **Aceptar** dos veces.
   
    Cuando el proceso de hello finalice, hello **notificaciones** área parpadeará en un color verde **correcto** hello y **conexión híbrida** hoja mostrará conexión híbrida nueva de hello con Hola estado como **no conectado**.
   
    ![One hybrid connection created][CreateHCOneConnectionCreated]

En este momento, ha completado una parte importante de la infraestructura de conexión de hello en la nube híbrida. A continuación, creará la parte local correspondiente.

<a name="InstallHCM"></a>

## <a name="d-install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a>D. Instalar Hola local Administrador de conexiones híbridas toocomplete Hola conexión
[!INCLUDE [app-service-hybrid-connections-manager-install](../../includes/app-service-hybrid-connections-manager-install.md)]

Ahora está completa esa infraestructura de conexión híbrida de hello, creará una aplicación web que lo utiliza.

<a name="CreateASPNET"></a>

## <a name="e-create-a-basic-aspnet-web-project-edit-hello-database-connection-string-and-run-hello-project-locally"></a>E. Cree un proyecto web ASP.NET básico, editar cadena de conexión de base de datos de Hola y ejecutar proyectos de hello localmente
### <a name="create-a-basic-aspnet-project"></a>Creación de un proyecto ASP.NET básico
1. En Visual Studio, en hello **archivo** menú, cree un nuevo proyecto:
   
    ![New Visual Studio project][HCVSNewProject]
2. Hola **plantillas** sección de hello **nuevo proyecto** cuadro de diálogo, seleccione **Web** y elija **aplicación Web ASP.NET**y, a continuación, haga clic en  **Aceptar**.
   
    ![Choose ASP.NET Web Application][HCVSChooseASPNET]
3. Hola **nuevo proyecto ASP.NET** cuadro de diálogo, elija **MVC**y, a continuación, haga clic en **Aceptar**.
   
    ![Choose MVC][HCVSChooseMVC]
4. Cuando se ha creado el proyecto de hello, aparece la página del archivo Léame de aplicación Hola. No ejecute proyecto web de hello todavía.
   
    ![Readme page][HCVSReadmePage]

### <a name="edit-hello-database-connection-string-for-hello-application"></a>Editar cadena de conexión de base de datos de hello para la aplicación hello
En este paso, editar cadena de conexión de Hola que le indica a la aplicación donde toofind local SQL Server Express base de datos. cadena de conexión de Hello es en el archivo Web.config de la aplicación hello, que contiene información de configuración de la aplicación hello.

> [!NOTE]
> tooensure que la aplicación utiliza la base de datos de Hola que creó en SQL Server Express, no hello y uno en LocalDB predeterminada de Visual Studio, es importante que complete este paso antes de ejecutar el proyecto.
> 
> 

1. En el Explorador de soluciones, haga doble clic en el archivo Web.config de Hola.
   
    ![Web.config][HCVSChooseWebConfig]
2. Editar hello **connectionStrings** base de datos de sección toopoint toohello SQL Server en el equipo local, la sintaxis de hello en el siguiente ejemplo de Hola:
   
    ![Cadena de conexión][HCVSConnectionString]
   
    Cuando se crea la cadena de conexión de hello, tenga en siguiente Hola de cuenta:
   
   * Si va a conectar tooa con el nombre de instancia en lugar de una instancia predeterminada (por ejemplo, YourServer\SQLEXPRESS), debe configurar los puertos estáticos toouse de SQL Server. Para obtener información acerca de cómo configurar puertos estáticos, vea [cómo tooconfigure toolisten de SQL Server en un puerto específico](http://support.microsoft.com/kb/823938). De forma predeterminada, las instancias con nombre usan puertos dinámicos y UDP, que Conexiones híbridas no admite.
   * Se recomienda que especifique Hola puerto (1433 de forma predeterminada, tal como se muestra en el ejemplo de Hola) en la cadena de conexión de Hola por lo que puede estar seguro de que el servidor SQL Server local tiene TCP habilitado y está utilizando el puerto correcto de Hola.
   * Recuerde tooconnect de autenticación de SQL Server toouse, especificando el Id. de usuario de Hola y la contraseña en la cadena de conexión.
3. Haga clic en **guardar** en el archivo Web.config de Visual Studio toosave Hola.

### <a name="run-hello-project-locally-and-register-a-new-user"></a>Ejecutar el proyecto de hello localmente y registrar un nuevo usuario
1. Ahora, ejecute el nuevo proyecto web localmente haciendo clic en el botón de examinar hello en la depuración. En este ejemplo se usa Internet Explorer.
   
    ![Run project][HCVSRunProject]
2. En hello esquina superior derecha de página web de hello predeterminada, elija **registrar** tooregister una nueva cuenta:
   
    ![Register a new account][HCVSRegisterLocally]
3. Escriba un nombre de usuario y una contraseña:
   
    ![Enter user name and password][HCVSCreateNewAccount]
   
    Esto crea automáticamente una base de datos en el servidor local de SQL que contiene la información de pertenencia de hello para la aplicación. Una de las tablas de hello (**dbo. AspNetUsers**) contiene web como Hola que acaba de escribir las credenciales de usuario de aplicación. Verá esta tabla más adelante en el tutorial Hola.
4. Cierre la ventana del explorador Hola de página web de hello predeterminada. Esto detiene la aplicación hello en Visual Studio.

Ahora está listo para el paso siguiente de hello, que es toopublish Hola aplicación tooAzure y probarlo.

<a name="PubNTest"></a>

## <a name="f-publish-hello-web-application-tooazure-and-test-it"></a>F. Publicar tooAzure de aplicación web de Hola y probarlo
Ahora, podrá publicar su aplicación de servicio de aplicaciones web de aplicación tooyour y, a continuación, probarlo toosee forma de conexión híbrida de Hola que configuró anteriormente que se va tooconnect usa la base de datos de la toohello de aplicación web en el equipo local.

### <a name="publish-hello-web-application"></a>Publicar la aplicación web de hello
1. Puede descargar el perfil de publicación de hello aplicación de servicio de aplicaciones web en hello Portal de Azure. En la hoja de hello para la aplicación web, haga clic en **Get perfil de publicación**y, a continuación, guardar el equipo de hello archivo tooyour.
   
    ![Descargar perfil de publicación][PortalDownloadPublishProfile]
   
    A continuación, importará este archivo en la aplicación web de Visual Studio.
2. En Visual Studio, haga clic en nombre de proyecto de hello en el Explorador de soluciones y seleccione **publicar**.
   
    ![Select publish][HCVSRightClickProjectSelectPublish]
3. Hola **Publicar Web** cuadro de diálogo, en hello **perfil** ficha, elija **importación**.
   
    ![Importación][HCVSPublishWebDialogImport]
4. Examinar tooyour descarga perfil de publicación, selecciónelo y, a continuación, haga clic en **Aceptar**.
   
    ![Examinar tooprofile][HCVSBrowseToImportPubProfile]
5. La información de publicación se importa y se muestra en hello **conexión** ficha del cuadro de diálogo de Hola.
   
    ![Haga clic en Publicar.][HCVSClickPublish]
   
    Haga clic en **Publicar**.
   
    Cuando se completa la publicación, el explorador se inicie y mostrar la aplicación de ASP.NET ya le es familiar, salvo que ahora es activo en la nube de Azure de Hola!

A continuación, usará su toosee de aplicación web en directo su conexión híbrida en acción.

### <a name="test-hello-completed-web-application-on-azure"></a>Hola de prueba completada la aplicación web en Azure
1. En la parte superior de hello derecha de la página web en Azure, elija **sesión**.
   
    ![Test log in][HCTestLogIn]
2. El servicio de aplicaciones de la aplicación web está ahora conectado a base de datos de pertenencia de la aplicación web tooyour en el equipo local. tooverify, inicie sesión con hello mismas credenciales que especificó en hello local de base de datos anterior.
   
    ![Hello greeting][HCTestHelloContoso]
3. toofurther probar la conexión híbrida nueva, cierre la sesión en la aplicación web de Azure y registrar como otro usuario. Proporcione un nuevo nombre de usuario y contraseña y, a continuación, haga clic en **Registrarse**.
   
    ![Test register another user][HCTestRegisterRelecloud]
4. tooverify que las credenciales del usuario nuevo de Hola se han almacenado en la base de datos local a través de la conexión híbrida, abra SQL Management Studio en el equipo local. En el Explorador de objetos, expanda hello **MembershipDB** base de datos y, a continuación, expanda **tablas**. Menú contextual hello **dbo. AspNetUsers** pertenencia a la tabla y elija **seleccionar 1000 filas superiores** resultados de tooview Hola.
   
    ![Ver los resultados de Hola][HCTestSSMSTree]
5. La tabla de pertenencia local ahora muestra ambas cuentas - Hola uno que creaste localmente y Hola uno que creaste en hello nube de Azure. Hola uno que creó en la nube de Hola se ha guardado tooyour base de datos local a través de la característica de conexión híbrida de Azure.
   
    ![Registered users in on-premises database][HCTestShowMemberDb]

Ahora ha creado e implementado una aplicación web ASP.NET que utiliza una conexión híbrida entre una aplicación web en hello nube de Azure y una base de datos de SQL Server local. ¡Enhorabuena!

## <a name="see-also"></a>Otras referencias
[Introducción a las conexiones híbridas](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[Josh Twist presenta las conexiones híbridas (vídeo de Channel 9)](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[Introducción a las conexiones híbridas](/services/biztalk-services/)

[Servicios de BizTalk: pestañas Panel, Monitor, Escala, Configurar y Conexiones híbridas](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[Creación de una nube híbrida del mundo real con una perfecta portabilidad de aplicaciones (vídeo de Channel 9)](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[Acceso a recursos locales mediante conexiones híbridas en Azure App Service](web-sites-hybrid-connection-get-started.md)

[Introducción a la identidad de ASP.NET](http://www.asp.net/identity)

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

<!-- IMAGES -->
[SQLServerInstall]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A01SQLServerInstall.png
[ChooseDefaultInstance]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A02ChooseDefaultInstance.png
[ChooseMixedMode]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A03ChooseMixedMode.png
[SSMSConnectToServer]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A04SSMSConnectToServer.png
[SSMScreateNewDB]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A05SSMScreateNewDBlh.png
[SSMSprovideDBname]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A06SSMSprovideDBname.png
[SSMSMembershipDBCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A07SSMSMembershipDBCreated.png
[New]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D10HCStatusConnected.png
[HCVSNewProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E01HCVSNewProject.png
[HCVSChooseASPNET]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E02HCVSChooseASPNET.png
[HCVSChooseMVC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E03HCVSChooseMVC.png
[HCVSReadmePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E04HCVSReadmePage.png
[HCVSChooseWebConfig]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E05HCVSChooseWebConfig.png
[HCVSConnectionString]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSConnectionString.png
[HCVSRunProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSRunProject.png
[HCVSRegisterLocally]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E07HCVSRegisterLocally.png
[HCVSCreateNewAccount]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E08HCVSCreateNewAccount.png
[PortalDownloadPublishProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F01PortalDownloadPublishProfile.png
[HCVSPublishProfileInDownloadsFolder]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F02HCVSPublishProfileInDownloadsFolder.png
[HCVSRightClickProjectSelectPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F03HCVSRightClickProjectSelectPublish.png
[HCVSPublishWebDialogImport]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F04HCVSPublishWebDialogImport.png
[HCVSBrowseToImportPubProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F05HCVSBrowseToImportPubProfile.png
[HCVSClickPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F06HCVSClickPublish.png
[HCTestLogIn]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F07HCTestLogIn.png
[HCTestHelloContoso]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F08HCTestHelloContoso.png
[HCTestRegisterRelecloud]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F09HCTestRegisterRelecloud.png
[HCTestSSMSTree]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F10HCTestSSMSTree.png
[HCTestShowMemberDb]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F11HCTestShowMemberDb.png
