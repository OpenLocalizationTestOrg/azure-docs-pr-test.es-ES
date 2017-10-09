---
title: "aaaHow tooMigrate y publicar una aplicación Web tooan del servicio en nube de Azure desde Visual Studio | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomigrate y publicar su tooan de aplicación web servicio de nube de Azure mediante Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 9394adfd-a645-4664-9354-dd5df08e8c91
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: a2832c37d2ebdbc1e69a307d16b65b1c87e9070c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-migrate-and-publish-a-web-application-tooan-azure-cloud-service-from-visual-studio"></a>Cómo: migrar y publicar un servicio de nube de Azure desde Visual Studio tooan de aplicación Web
tootake aprovechar Hola servicios de hospedaje y la escalabilidad de Azure, podría desea toomigrate y publicar el servicio de nube de Azure de tooan de aplicación web. Puede ejecutar una aplicación web en Azure con aplicación de cambios mínimos tooyour existente.

> [!NOTE]
> Este tema trata sobre la implementación de servicios de toocloud, no tooweb sitios. Para obtener información sobre cómo implementar sitios tooweb, consulte [implementar una aplicación web en el servicio de aplicación de Azure](app-service-web/web-sites-deploy.md).
>
>

Para obtener una lista de plantillas específicas que son compatibles con Visual C# y Visual Basic, consulte la sección de hello **plantillas de proyecto compatibles** más adelante en este tema.

Primero debe habilitar la aplicación web para Azure desde Visual Studio. Hola siguientes ilustración muestra hello pasos clave toopublish la aplicación web existente agregando un toouse de proyecto de Azure para la implementación. Este proceso agrega un proyecto de Azure con solución tooyour rol web de hello necesario. Según el tipo de saludo de proyecto web que tiene, propiedades del proyecto Hola ensamblados también se actualizan si el paquete de servicio de hello necesita ensamblados adicionales para la implementación.

![Publicar un tooMicrosoft de aplicación Web Azure](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC748917.png)

> [!NOTE]
> Hola **convertir**, **convertir el proyecto de servicio de nube tooAzure** comando solo se muestra para proyectos web de hello en la solución. Por ejemplo, el comando de hello no está disponible para un proyecto de Silverlight en la solución.
> Al crear un paquete de servicio o publicar su aplicación tooAzure, podrían producir advertencias o errores. Estas advertencias y errores pueden ayudarle a solucionar problemas antes de implementar tooAzure. Por ejemplo, podría recibir una advertencia sobre un ensamblado que falta. Para obtener más información sobre cómo tootreat las advertencias como errores, vea [configurar un proyecto de servicio de nube de Azure con Visual Studio](vs-azure-tools-configuring-an-azure-project.md). Si compila la aplicación, ejecuta localmente mediante el emulador de proceso de Hola o publicarlo tooAzure, podría ver Hola tras error en hello **lista de errores** ventana: **Hola especifica la ruta de acceso, nombre de archivo, o ambos son demasiado largos** . Este error se produce porque Hola del nombre de proyecto de Azure completo hello es demasiado largo. longitud de Hola de nombre de proyecto de hello, incluida la ruta de acceso completa de hello, no puede tener más de 146 caracteres. Por ejemplo, esto es nombre de proyecto completo hello como ruta de acceso de archivo para un proyecto de Azure que se crea para una aplicación de Silverlight: `c:\users\<user name>\documents\visual studio 2015\Projects\SilverlightApplication4\SilverlightApplication4.Web.Azure.ccproj`. Es posible que tenga toomove su solución tooa otro directorio que tiene una longitud de hello tooreduce de ruta de acceso más corta del nombre completo del proyecto de Hola.
>
>

toomigrate y publicar un tooAzure de aplicación web de Visual Studio, siga estos pasos.

## <a name="enable-a-web-application-for-deployment-tooazure"></a>Habilitar una aplicación Web tooAzure de implementación
### <a name="tooenable-a-web-application-for-deployment-tooazure"></a>una aplicación web para la implementación tooAzure tooenable
1. tooenable la aplicación web para la implementación tooAzure, menú contextual de hello abierto para un sitio web del proyecto en la solución y elija Agregar un proyecto de implementación de Azure.

    se produce Hola siguientes acciones:

   * Llama a un proyecto de Azure `<name of hello web project>.Azure` se agrega toohello solución para la aplicación.
   * Un rol web para el proyecto de hello web se agrega toothis proyecto de Azure.
   * Hola **Copy Local** tootrue se establece una propiedad para los ensamblados que son necesarios para MVC 2, MVC 3, MVC 4 y las aplicaciones de negocios de Silverlight. Esto agrega estos paquete de servicio de toohello de ensamblados que se utiliza para la implementación.

   > [!IMPORTANT]
   > Si tiene otros ensamblados o archivos que son necesarios para esta aplicación web, debe establecer manualmente las propiedades de Hola para estos archivos. Para obtener información sobre cómo tooset estas propiedades, vea Hola sección **archivos de inclusión en hello paquete del servicio** más adelante en este artículo.
   >
   > [!NOTE]
   > Si ya existe un rol web para un proyecto web específico en un proyecto de Azure en la solución de hello, **convertir**, **convertir el proyecto de servicio de nube tooAzure** no se muestra en el menú contextual de Hola para este proyecto web .
   >
   >

   Si tiene varios proyectos web en la aplicación web y desea que los roles web toocreate para cada proyecto web, debe realizar pasos de hello en este procedimiento para cada proyecto web. Esto crea proyectos de Azure diferentes para cada rol web. Cada proyecto web puede publicarse por separado. Como alternativa, puede agregar manualmente otro rol tooan existente Azure proyecto web en la aplicación web. toodo, menú contextual abierto Hola Hola **Roles** carpeta en su proyecto de Azure, elija **agregar**, a continuación, **proyecto de rol Web de la solución**, elija hello tooadd de proyecto como un sitio web rol y, a continuación, elija hello **Aceptar** botón.

## <a name="use-an-azure-sql-database-for-your-application"></a>Usar una Base de datos SQL Azure para su aplicación
Si tiene una cadena de conexión para la aplicación web que usa una base de datos de SQL Server que sea local hello, debe cambiar este toouse de cadena de conexión una instancia de base de datos de SQL que hospeda Azure en su lugar.

> [!IMPORTANT]
> Su suscripción debe permitir toouse base de datos SQL. Si tiene acceso a su suscripción de hello [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885), puede determinar qué servicios proporciona su suscripción. Hello instrucciones siguientes aplican toohello publicado [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885). Si usas hello [portal de Azure](http://portal.microsoft.com), omita el procedimiento siguiente toohello.
>
>

### <a name="toouse-a-sql-database-instance-in-your-web-role-for-your-connection-string"></a>toouse una instancia de base de datos SQL en el rol web para la cadena de conexión
1. una instancia de base de datos SQL en hello toocreate [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885), siga los pasos de Hola Hola artículo siguiente: [crear una base de datos de SQL Server](http://go.microsoft.com/fwlink/?LinkId=225109).

   > [!NOTE]
   > Al configurar las reglas de firewall de hello para la instancia de base de datos SQL, debe seleccionar hello **permitir que otros servicios de Azure tooaccess este servidor** casilla de verificación.
   >
   >
2. toocreate una instancia de base de datos SQL toouse para la cadena de conexión, siga los pasos de hello en la próxima sección de Hola de hello artículo siguiente: [crear una base de datos de SQL](http://go.microsoft.com/fwlink/?LinkId=225110).
3. toouse toocopy Hola ADO.NET connection string para la cadena de conexión, realizar Hola siguiendo los pasos de hello [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885).  

   1. Elija hello **base de datos** botón y nodo de hello, a continuación, abra para suscripción de hello usa toocreate en la instancia de base de datos SQL.
   2. instancias disponibles de hello toodisplay de base de datos de SQL, elija hello **bases de datos SQL** nodo.
   3. propiedades de hello toodisplay de base de datos de hello, elija una base de Hola. Hola **propiedades** vista aparece.

      > [!NOTE]
      > Si hello **propiedades** vista no aparece, puede que tenga tooopen mediante Hola divisor.
      >
      >
   4. cadenas de conexión de toodisplay hello, elija tooView siguiente del botón de puntos suspensivos (...) Hola.

      Hola **las cadenas de conexión** aparece el cuadro de diálogo.
   5. Hola toocopy cadena de conexión de ADO.NET, resaltar texto hello y elija las teclas CTRL+c de Hola.
   6. cuadro de diálogo de hello tooclose cuadro, elija hello **cerrar** botón.
4. conexión de hello tooreplace cadena en hello web.config archivo toouse esta instancia de base de datos de SQL, abra el archivo web.config de hello, resalte la entrada de cadena de conexión existente de hello y, a continuación, elija teclas de CTRL+v Hola. Hola cadena de conexión de ADO.NET para la instancia de Hola de base de datos SQL reemplaza la cadena de conexión existente de Hola.
5. También debe agregar el parámetro hello `MultipleActiveResultSets=True` toohello cadena de conexión. cadena de conexión de Hello debe tener Hola siguiendo el formato:

    ```
    connectionString=”Server=tcp:<database_server>.database.windows.net,1433;Database=<database_name>;User ID=<user_name>@<database_server>;Password=<myPassword>;Trusted_Connection=False;Encrypt=True;MultipleActiveResultSets=True"
    ```
6. (Opcional) Una cadena de conexión de método alternativo toochanging Hola directamente en el archivo web.config de hello es tooadd una sección en uno de los archivos de la transformación de web.config hello, dependiendo de la configuración de compilación de Hola que utiliza toocreate su paquete del servicio. Abrir archivo de hello Web.Debug.Config o archivo de hello Web.Release.Config. Agregue Hola pasos de la sección en este archivo:

    ```
    XMLCopy<connectionStrings><addname="DefaultConnection"connectionString="Server=tcp:<database_server>.database.windows.net,1433;Database=<database_name>;User ID=<user_name>@<database_server>;Password=<myPassword>;Trusted_Connection=False;Encrypt=True;MultipleActiveResultSets=True"xdt:Transform="SetAttributes"xdt:Locator="Match(name)"/></connectionStrings>
    ```
7. Guardar archivo de Hola que modificó y volver a publicar la aplicación.

### <a name="toouse-an-instance-of-sql-database-by-using-hello-azure-classic-portal"></a>Hola a toouse una instancia de base de datos de SQL mediante el portal de Azure clásico
1. Hola [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885), elija el nodo de bases de datos SQL de Hola.

   * Si aparece en la instancia de Hola de base de datos de SQL que desea toouse, elija tooopen lo.
   * Si no ha creado ninguna instancia, elija el vínculo apropiado de hello y, a continuación, cree una instancia.
2. Después de abrir o crear una instancia de base de datos, elija hello **las cadenas de conexión** vínculo.
3. Final Hola de hello página, elija la configuración del firewall de hello vínculo tooconfigure y acepte los valores predeterminados de Hola o configurar valores de hello que necesita.
4. Copie la cadena de conexión de ADO.NET de hello, péguelo en el archivo web.config en la cadena de conexión antigua de Hola para base de datos de hello en local y ser seguro tooadd `MultipleActiveResultSets=True`.

## <a name="publish-a-web-application-tooazure"></a>Publicar una aplicación Web tooAzure
### <a name="toopublish-a-web-application-tooazure"></a>toopublish una tooAzure de aplicación Web
1. aplicación de hello tootest en entorno de desarrollo local hello mediante el emulador de proceso de Azure de hello, menú contextual abierto Hola Hola Azure de proyecto de rol web de Hola y elija **establecer como proyecto de inicio**. A continuación, elija **Depurar**, **Iniciar depuración** (teclado: **F5**).

    Hola **inicio Hola entorno de depuración de Azure** abre el cuadro de diálogo y aplicación hello comienza en el Explorador de Hola. Para obtener detalles específicos acerca de cómo toostart cada tipo de aplicación web en hello emulador de proceso, consulte la tabla hello en esta sección.
2. tooset los servicios de Hola para su tooAzure toopublish de aplicación, debe tener una cuenta de Microsoft y una suscripción de Azure. Hola de uso de los pasos de hello después tooset de tema de los servicios: [preparar toopublish o implementar una aplicación de Azure desde Visual Studio](vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md).
3. toopublish hello web aplicación tooAzure, abra el acceso directo de hello para el proyecto web de Hola y elija **publicar tooAzure**.

    Hola **publicar aplicación de Azure** abre el cuadro de diálogo y Visual Studio inicia el proceso de implementación de Hola. Para obtener más información acerca de cómo toopublish Hola aplicación, consulte la sección hello **publicar una aplicación de Azure desde Visual Studio** en [publicar un servicio de nube mediante herramientas de Azure de hello](vs-azure-tools-publishing-a-cloud-service.md).

   > [!NOTE]
   > También puede publicar aplicación web de hello de hello proyecto de Azure. toodo, abra el acceso directo de Hola para hello proyecto de Azure y elija **publicar**.
   >
   >
4. progreso de hello toosee de implementación de hello, puede ver hello **Azure Activity Log** ventana. Este registro se muestra automáticamente cuando se inicia el proceso de implementación de Hola. Puede expandir Hola de elemento de línea en el registro de actividad de hello tooshow información detallada, como se muestra en hello siguiente ilustración:

    ![VST_AzureActivityLog](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC744149.png)
5. Proceso de implementación de hello toocancel (opcional), abra el menú de acceso directo de Hola de artículo de línea de Hola en registro de actividad de Hola y elija **Cancelar y quitar**. Esto detiene el proceso de implementación de Hola y elimina el entorno de implementación de Hola de Azure.

   > [!NOTE]
   > tooremove este entorno de implementación después de ha sido implementado, debe usar hello [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885).
   >
   >
6. (Opcional) Después de que hayan iniciado las instancias de rol, Visual Studio muestra automáticamente el entorno de implementación de Hola Hola **cálculo de Azure** nodo **Explorer nube** o **delexploradordeservidores**. Desde aquí puede ver estado de Hola Hola individuales de instancias de rol.

    Hello en la ilustración siguiente se muestra instancias de rol de hello en **Explorador de servidores** mientras están todavía en estado Initializing hello:

    ![VST_DeployComputeNode](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC744134.png)
7. tooaccess la aplicación después de la implementación, elija Hola flecha siguiente tooyour implementación al estado **completado** aparece en hello **registro de actividad de Azure**. Esto muestra la dirección URL de hello para la aplicación web en Azure. Vea Hola para obtener detalles de hello sobre cómo toostart un determinado tipo de aplicación web de Azure en la tabla siguiente.

    Hello en la tabla siguiente muestra los detalles de hello acerca de cómo toostart las aplicaciones de Azure o toorun web o depurar una aplicación web localmente mediante Hola emulador de proceso de Azure:

   | Tipo de aplicación web | Hola ejecutar/depurar localmente mediante el emulador de cálculo | Ejecución en Azure |
   | --- | --- | --- |
   | Aplicación web ASP.NET |En la barra de menús de hello, elija **depurar**, **Iniciar depuración** (teclado: elija hello **F5** clave.). |Elija el hipervínculo de dirección URL de hello muestra de Hola **implementación** ficha para hello **registro de actividad de Azure** página de inicio de tooload hello en el Explorador de Hola. |
   | Aplicación web MVC 2 de ASP.NET |En la barra de menús de hello, elija **depurar**, **Iniciar depuración** (teclado: elija hello **F5** clave.). |Elija el hipervínculo de dirección URL de hello muestra de Hola **implementación** ficha para hello **registro de actividad de Azure** página de inicio de tooload hello en el Explorador de Hola. |
   | Aplicación web MVC 3 de ASP.NET |En la barra de menús de hello, elija **depurar**, **Iniciar depuración** (teclado: elija hello **F5** clave.). |Elija el hipervínculo de dirección URL de hello muestra de Hola **implementación** ficha para hello **registro de actividad de Azure** página de inicio de tooload hello en el Explorador de Hola. |
   | Aplicación web MVC 4 de ASP.NET |En la barra de menús de hello, elija **depurar**, **Iniciar depuración** (teclado: elija hello **F5** clave.). |Elija el hipervínculo de dirección URL de hello muestra de Hola **implementación** ficha para hello **registro de actividad de Azure** página de inicio de tooload hello en el Explorador de Hola. |
   | Aplicación web ASP.NET vacía |Debe agregar una página .aspx en la aplicación que establecer como página de inicio de hello para el proyecto web. A continuación, en la barra de menús de hello, elija **depurar**, **Iniciar depuración** (teclado: elija hello **F5** clave.). |Si tiene una página .aspx predeterminada en la aplicación, elija el hipervínculo de dirección URL de hello mostrado en hello **implementación** ficha para hello **registro de actividad de Azure** y esta página se cargará en el Explorador de Hola. Si tiene una página .aspx diferente, deberá toonavigate toothis página específica usando Hola siguiendo el formato para la dirección url:`<url for deployment>/<name of page>.aspx` |
   | Aplicación de Silverlight |En la barra de menús de hello, elija **depurar**, **Iniciar depuración** (teclado: elija hello **F5** clave.). |Página específica de toonavigate toohello se necesita para su aplicación mediante Hola siguiendo el formato para la dirección url:`<url for deployment>/<name of page>.aspx` |
   | Aplicación de negocios de Silverlight |En la barra de menús de hello, elija **depurar**, **Iniciar depuración** (teclado: elija hello **F5** clave.). |Página específica de toonavigate toohello se necesita para su aplicación mediante Hola siguiendo el formato para la dirección url:`<url for deployment>/<name of page>.aspx` |
   | Aplicación de navegación de Silverlight |En la barra de menús de hello, elija **depurar**, **Iniciar depuración** (teclado: elija hello **F5** clave.). |Página específica de toonavigate toohello se necesita para su aplicación mediante Hola siguiendo el formato para la dirección url:`<url for deployment>/<name of page>.aspx` |
   | Aplicación de servicio de WCF |También debe establecer archivo .svc de hello como Hola página de inicio para el proyecto de servicio WCF. A continuación, en la barra de menús de hello, elija **depurar**, **Iniciar depuración** (teclado: elija hello **F5** clave.). |Necesita el archivo svc de toonavigate toohello de la aplicación usando Hola siguiendo el formato para la dirección url:`<url for deployment>/<name of service file>.svc` |
   | Aplicación de servicio de flujo de trabajo WCF |También debe establecer archivo .svc de hello como Hola página de inicio para el proyecto de servicio WCF. A continuación, en la barra de menús de hello, elija **depurar**, **Iniciar depuración** (teclado: elija hello **F5** clave.). |Necesita el archivo svc de toonavigate toohello de la aplicación usando Hola siguiendo el formato para la dirección url:`<url for deployment>/<name of service file>.svc` |
   | Entidades dinámicas de ASP.NET |En la barra de menús de hello, elija **depurar**, **Iniciar depuración** (teclado: elija hello **F5** clave.). |Debe actualizar la cadena de conexión de hello (vea la siguiente sección). También necesita página específica de toonavigate toohello de la aplicación usando Hola siguiendo el formato para la dirección url:`<url for deployment>/<name of page>.aspx` |
   | TooSQL de Linq de datos dinámicos de ASP.NET |En la barra de menús de hello, elija **depurar**, **Iniciar depuración** (teclado: elija hello **F5** clave.). |Debe seguir los pasos de hello en este procedimiento: utilizar una base de datos de SQL Azure para su aplicación (consulte la sección anterior de este tema). También necesita página específica de toonavigate toohello de la aplicación usando Hola siguiendo el formato para la dirección url:`<url for deployment>/<name of page>.aspx` |

## <a name="update-a-connection-string-for-aspnet-dynamic-entities"></a>Actualizar una cadena de conexión para Entidades dinámicas de ASP.NET
### <a name="tooupdate-a-connection-string-for-aspnet-dynamic-entities"></a>tooUpdate una cadena de conexión para entidades dinámicas de ASP.NET
1. toocreate una base de datos de SQL Azure que puede usarse para una aplicación web de entidades dinámicas de ASP.NET, siga los pasos de hello en el procedimiento de hello **utilizar una base de datos de SQL Azure para su aplicación** anteriormente en este tema.
2. Agregar tablas de Hola y los campos que necesite para esta base de datos de hello [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885).
3. cadena de conexión de Hola para este tipo de aplicación tiene Hola siguiendo el formato en el archivo web.config de hello:  

    ```
    <addname="tempdbEntities"connectionString="metadata=res://*/Model1.csdl|res://*/Model1.ssdl|res://*/Model1.msl;provider=System.Data.SqlClient;provider connection string=&quot;data source=<server name>\SQLEXPRESS;initial catalog=<database name>;integrated security=True;multipleactiveresultsets=True;App=EntityFramework&quot;"providerName="System.Data.EntityClient"/>
    ```

    Hola de actualización *connectionString* valor con hello cadena de conexión de ADO.NET para la base de datos de SQL Azure como sigue:

    ```
    XMLCopy<addname="tempdbEntities"connectionString="metadata=res://*/Model1.csdl|res://*/Model1.ssdl|res://*/Model1.msl;provider=System.Data.SqlClient;provider connection string=&quot;Server=tcp:<SQL Azure server name>.database.windows.net,1433;Database=<database name>;User ID=<user name>;Password=<password>;Trusted_Connection=False;Encrypt=True;multipleactiveresultsets=True;App=EntityFramework&quot;"providerName="System.Data.EntityClient"/>
    ```
4. archivo web.config que hello toosave incluye cambios de Hola que haya realizado toohello cadena de conexión, en la barra de menús de hello elija **archivo**, **guardar web.config**.

## <a name="supported-project-templates"></a>Plantillas de proyecto compatibles
toopublish una tooAzure de aplicación web, aplicación hello debe usar uno Hola plantillas de proyecto para C# o Visual Basic que aparece en la siguiente tabla se Hola.

| Grupo de plantillas de proyecto | Plantilla de proyecto |
| --- | --- |
| Web |Aplicación web ASP.NET |
| Web |Aplicación web MVC 2 de ASP.NET |
| Web |Aplicación web MVC 3 de ASP.NET |
| Web |Aplicación web MVC 4 de ASP.NET |
| Web |Aplicación web ASP.NET vacía |
| Web |Aplicación web MVC 2 de ASP.NET vacía |
| Web |Aplicación web de Entidades de datos dinámicos de ASP.NET |
| Web |TooSQL de Linq de datos dinámicos de ASP.NET aplicación Web |
| Silverlight |Aplicación de Silverlight |
| Silverlight |Aplicación de negocios de Silverlight |
| Silverlight |Aplicación de navegación de Silverlight |
| WCF |Aplicación de servicio de WCF |
| WCF |Aplicación de servicio de flujo de trabajo WCF |
| Flujo de trabajo |Aplicación de servicio de flujo de trabajo WCF |

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre la publicación, vea [preparar tooPublish o implementar una aplicación de Azure desde Visual Studio](vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md). Consulte también [Configuración de credenciales de autenticación con nombre](vs-azure-tools-setting-up-named-authentication-credentials.md).
