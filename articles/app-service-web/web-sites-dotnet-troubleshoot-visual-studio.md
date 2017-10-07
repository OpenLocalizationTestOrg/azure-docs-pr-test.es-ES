---
title: "aaaTroubleshoot una aplicación web en el servicio de aplicaciones de Azure con Visual Studio"
description: "Obtenga información acerca de cómo tootroubleshoot una aplicación web de Azure mediante la depuración remota, seguimiento y registro de las herramientas que están integradas en tooVisual Studio 2013."
services: app-service
documentationcenter: .net
author: tdykstra
manager: erikre
editor: 
ms.assetid: def8e481-7803-4371-aa55-64025d116c97
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/29/2016
ms.author: rachelap
ms.openlocfilehash: 8e3a8a58293f2ebcdc131fbf2534f8ff99b26730
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-web-app-in-azure-app-service-using-visual-studio"></a>Solución de problemas de una aplicación web en el Servicio de aplicaciones de Azure con Visual Studio
## <a name="overview"></a>Información general
Este tutorial muestra cómo toouse herramientas de Visual Studio que ayudan a depuración una aplicación web en [servicio de aplicaciones](http://go.microsoft.com/fwlink/?LinkId=529714), mediante la ejecución [el modo de depuración](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) al ver los registros de aplicación y los registros del servidor web o de forma remota.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

Aprenderá a realizar los siguientes procedimientos:

* Funciones de administración de aplicaciones web de Azure disponibles en Visual Studio.
* Cómo remota de Visual Studio toouse ver cambios rápidos toomake en una aplicación web remota.
* Cómo toorun el modo de depuración remota mientras un proyecto se ejecuta en Azure, para una aplicación web y para un trabajo Web.
* ¿Cómo toocreate aplicación los registros de seguimiento y verlos mientras la aplicación hello su creación.
* Cómo registros tooview del servidor web, incluidos los mensajes de error detallan y error del seguimiento de la solicitud.
* ¿Cómo toosend diagnóstico registra tooan cuenta de almacenamiento de Azure y verlos no existe.

Si tiene Visual Studio Ultimate, también puede usar [IntelliTrace](http://msdn.microsoft.com/library/vstudio/dd264915.aspx) para la depuración. IntelliTrace no se trata en este tutorial.

## <a name="prerequisites"></a>Requisitos previos
Este tutorial funciona con el entorno de desarrollo de hello, proyecto web y aplicaciones web de Azure que configuró en [Introducción a Azure y ASP.NET][GetStarted]. Para las secciones de hello trabajos Web, necesitará aplicación hello que cree en [empezar a trabajar con el SDK de WebJobs de Azure hello][GetStartedWJ].

código de Hello ejemplos que se muestran en este tutorial son para una aplicación web de MVC de C#, pero Hola procedimientos de solución de problemas se Hola mismo para las aplicaciones de Visual Basic y formularios Web Forms.

tutorial de Hola se da por supuesto que está utilizando Visual Studio 2015 o 2013. Si usa Visual Studio 2013, requieren características de trabajos Web hello [actualización 4](http://go.microsoft.com/fwlink/?LinkID=510314) o una versión posterior.

registros de streaming de Hello característica solo funciona para las aplicaciones que tienen como destino .NET Framework 4 o posterior.

## <a name="sitemanagement"></a>Administración y configuración de la aplicación web
Visual Studio proporciona acceso tooa subconjunto de funciones de administración de aplicaciones web de Hola y valores de configuración disponibles en hello [Portal de Azure](http://go.microsoft.com/fwlink/?LinkId=529715). En esta sección podrá ver las opciones y funciones disponibles mediante el **Explorador de servidores**. probar características integración de Azure más recientes a toosee hello, **Explorer nube** también. Puede abrir ambas ventanas de hello **vista** menú.

1. Si ya no están firmados en tooAzure en Visual Studio, haga clic en hello **conectar tooAzure** botón en **Explorador de servidores**.

    Una alternativa es tooinstall un certificado de administración que permite tener acceso a la cuenta de tooyour. Si elige tooinstall un certificado, haga clic en hello **Azure** nodo **Explorador de servidores**y, a continuación, haga clic en **administrar y filtrar suscripciones** en el menú contextual de Hola. Hola **administrar suscripciones de Azure** diálogo cuadro, haga clic en hello **certificados** ficha y, a continuación, haga clic en **importación**. Siga toodownload de direcciones de hello y, a continuación, importar un archivo de suscripción (también denominado una *.publishsettings* archivo) para su cuenta de Azure.

   > [!NOTE]
   > Si descarga un archivo de suscripción, guárdelo tooa carpeta fuera de los directorios de código de origen (por ejemplo, en la carpeta de descargas de hello) y, a continuación, eliminarlo una vez completada la importación de Hola. Un usuario malintencionado que obtenga el archivo de suscripción de acceso toohello puede modificar, crear y eliminar los servicios de Azure.
   >
   >

    Para obtener más información acerca de cómo conectar tooAzure recursos desde Visual Studio, vea [administrar cuentas, suscripciones y Roles administrativos](http://go.microsoft.com/fwlink/?LinkId=324796#BKMK_AccountVCert).
2. En el **Explorador de servidores**, expanda **Azure** y, a continuación, **App Service**.
3. Expanda grupo de recursos de Hola que incluye la aplicación web de hello que creó en [Introducción a Azure y ASP.NET][GetStarted]y, a continuación, haga clic en el nodo de la aplicación hello web y haga clic en **ver la configuración de**.

    ![Ver configuración en el Explorador de servidores](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-viewsettings.png)

    Hola **aplicación Web de Azure** ficha aparece y puede ver Hola allí web app configuración y administración de tareas que están disponibles en Visual Studio.

    ![Ventana de aplicaciones web de Azure](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-configtab.png)

    En este tutorial usará el registro de hello y listas desplegables de la traza. También podrá usar la depuración remota, pero deberá usar un método diferente tooenable lo.

    Para obtener información acerca de los cuadros de configuración de la aplicación y cadenas de conexión de hello en esta ventana, consulte [aplicaciones Web de Azure: cómo las cadenas de la aplicación y el trabajo de las cadenas de conexión](http://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx).

    Si desea tooperform una tarea de administración de aplicaciones web que no se puede realizar en esta ventana, haga clic en **abrir en el Portal de administración** tooopen un toohello de ventana de explorador portal de Azure.

## <a name="remoteview"></a>Acceso a archivos de aplicaciones web en el Explorador de servidores
Normalmente se implementa un proyecto de web con hello `customErrors` demasiado se marcan en el conjunto de archivos Web.config de hello`On` o `RemoteOnly`, lo que significa que no obtendrá un mensaje de error útiles cuando algo va mal. Para muchos errores todo obtendrá es una página como uno de hello los siguiendo.

**Error del servidor en la aplicación '/':**

![Página de error poco práctica](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror.png)

**Se produjo un error:**

![Página de error poco práctica](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror1.png)

**sitio Web de Hello no puede mostrar la página de Hola**

![Página de error poco práctica](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror2.png)

Con frecuencia hello más fácil manera toofind Hola causa del error hello es tooenable mensajes de error detallados que Hola primero de hello anterior capturas de pantalla se explica cómo toodo. Que requiere el que archivo Web.config implementado de un cambio en Hola. Puede editar hello *Web.config* de archivos de proyecto de Hola y volver a implementar hello, o cree una [transformación de Web.config](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) e implementar una compilación de depuración, pero hay una manera más rápida: en **solución El Explorador de** directamente, puede ver y editar archivos de aplicación web remota de hello mediante hello *vista remota* característica.

1. En **Explorador de servidores**, expanda **Azure**, expanda **servicio de aplicaciones**, expanda el grupo de recursos de Hola que la aplicación web se encuentra en y, a continuación, expanda el nodo de hello para la aplicación web.

    Podrá ver los nodos que proporcionan los archivos de contenido y archivos de registro de la aplicación web de acceso toohello.
2. Expanda hello **archivos** nodo y haga doble clic en hello *Web.config* archivo.

    ![Abrir Web.config](./media/web-sites-dotnet-troubleshoot-visual-studio/webconfig.png)

    Visual Studio abre el archivo Web.config de hello de aplicación web remota de hello y [remoto] nombre de archivo toohello siguiente muestra en la barra de título de Hola.
3. Agregar Hola después línea toohello `system.web` elemento:

    `<customErrors mode="Off"></customErrors>`

    ![Editar Web.config](./media/web-sites-dotnet-troubleshoot-visual-studio/webconfigedit.png)
4. Actualizar explorador Hola que está mostrando un mensaje de error poco práctico de Hola y ahora obtendrá un mensaje de error detallado, como el siguiente ejemplo de Hola:

    ![Mensajes de error detallados](./media/web-sites-dotnet-troubleshoot-visual-studio/detailederror.png)

    (error de Hola se muestra se creó mediante la adición de línea de saludo se muestra en rojo demasiado*Views\Home\Index.cshtml*.)

Edición archivo Web.config de hello es sólo un ejemplo de en qué capacidad hello tooread y editar archivos en la aplicación web de Azure Asegúrese de solución de problemas de escenarios.

## <a name="remotedebug"></a>Aplicaciones web de depuración remota
Si mensaje de error detallado de hello no proporciona suficiente información, y se no se puede volver a crear localmente el error de hello, tootroubleshoot de otra manera es toorun en modo de depuración remota. Puede establecer puntos de interrupción, manipula la memoria directamente, recorrer el código e incluso cambiar la ruta de acceso de código de hello.

La depuración remota no funciona en ediciones Express de Visual Studio.

Esta sección muestra cómo toodebug de forma remota con hello project cree en [Introducción a Azure y ASP.NET][GetStarted].

1. Proyecto de web Hola abierto que ha creado en [Introducción a Azure y ASP.NET][GetStarted].
2. Abra *Controllers\HomeController.cs*.
3. Eliminar hello `About()` método y siguiente de Hola de inserción de código en su lugar.

        public ActionResult About()
        {
            string currentTime = DateTime.Now.ToLongTimeString();
            ViewBag.Message = "hello current time is " + currentTime;
            return View();
        }
4. [Establecer un punto de interrupción](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) en hello `ViewBag.Message` línea.
5. En **el Explorador de soluciones**, haga clic en proyecto de Hola y haga clic en **publicar**.
6. Hola **perfil** lista desplegable, seleccione Hola mismo perfil que haya utilizado en [Introducción a Azure y ASP.NET][GetStarted].
7. Haga clic en hello **configuración** pestaña y cambie **configuración** demasiado**depurar**y, a continuación, haga clic en **publicar**.

    ![Publicar en modo de depuración](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-publishdebug.png)
8. Después de la implementación finaliza y el explorador se abre toohello dirección URL de Azure de la aplicación web, el Explorador de hello cerrar.
9. En el **Explorador de servidores**, haga clic con el botón derecho en la aplic. web y, luego, haga clic en **Asociar depurador**.

    ![Asociar depurador](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-attachdebugger.png)

    explorador Hola automáticamente abre la página de inicio de tooyour ejecuta en Azure. Podría tener toowait 20 segundos o tan mientras Azure configura el servidor de hello para la depuración. Este retraso sólo ocurre Hola primera vez que se ejecute en modo de depuración en una aplicación web. Las siguientes veces dentro de hello siguientes 48 horas al comenzar la depuración de nuevo se no será un retraso.

    **Nota:** si tiene algún problema para iniciar el depurador de hello, pruebe a toodo mediante **Explorer nube** en lugar de **Explorador de servidores**.
10. Haga clic en **sobre** en el menú de Hola.

     Visual Studio se detiene en el punto de interrupción de Hola y código de hello se ejecuta en Azure, no en el equipo local.
11. Mantenga el mouse sobre hello `currentTime` valor de hora de hello toosee variable.

     ![Ver la variable en ejecución en modo de depuración en Azure](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugviewinwa.png)

     tiempo de Hello que verá es tiempo de servidor de Azure de hello, que puede estar en una zona horaria diferente que el equipo local.
12. Escriba un nuevo valor de hello `currentTime` variable, por ejemplo, "Ahora se ejecuta en Azure".
13. Presione toocontinue F5 ejecutando.

     Hola acerca de la página que se ejecuta en Azure muestra Hola nuevo valor que ha introducido en la variable de hello currentTime.

     ![Página About con el valor nuevo](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugchangeinwa.png)

## <a name="remotedebugwj"></a> WebJobs de depuración remota
Esta sección muestra cómo se toodebug de forma remota con hello proyecto y la aplicación web crean en [empezar a trabajar con el SDK de WebJobs de Azure hello](websites-dotnet-webjobs-sdk.md).

características de Hola se muestra en esta sección solo están disponibles en Visual Studio 2013 con Update 4 o posterior.

La depuración remota solo funciona con WebJobs continuos. Los WebJobs bajo demanda y programados no admiten la depuración.

1. Proyecto de web Hola abierto que ha creado en [empezar a trabajar con el SDK de WebJobs de Azure hello][GetStartedWJ].
2. En hello ContosoAdsWebJob proyecto, abra *Functions.cs*.
3. [Establecer un punto de interrupción](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) en la primera instrucción de Hola Hola `GnerateThumbnail` método.

    ![Establecimiento de punto de interrupción](./media/web-sites-dotnet-troubleshoot-visual-studio/wjbreakpoint.png)
4. En **el Explorador de soluciones**, haga clic en proyecto de web hello (no en el proyecto de hello trabajo Web) y haga clic en **publicar**.
5. Hola **perfil** lista desplegable, seleccione Hola mismo perfil que haya utilizado en [empezar a trabajar con el SDK de WebJobs de Azure hello](websites-dotnet-webjobs-sdk.md).
6. Haga clic en hello **configuración** pestaña y cambie **configuración** demasiado**depurar**y, a continuación, haga clic en **publicar**.

    Visual Studio implementa Hola proyectos web y trabajo Web y el explorador abre toohello dirección URL de la aplicación web de Azure.
7. En el **Explorador de servidores**, expanda **Azure > App Service > su grupo de recursos > su aplic. web > WebJobs > Continuo** y, a continuación, haga clic con el botón derecho en **ContosoAdsWebJob**.
8. Haga clic en **Adjuntar el depurador**.

    ![Asociar depurador](./media/web-sites-dotnet-troubleshoot-visual-studio/wjattach.png)

    explorador Hola automáticamente abre la página de inicio de tooyour ejecuta en Azure. Podría tener toowait 20 segundos o tan mientras Azure configura el servidor de hello para la depuración. Este retraso sólo ocurre Hola primera vez que se ejecute en modo de depuración en una aplicación web. Hola vuela a adjuntar a depurador de Hola allí no existir un retraso, si lo hace en 48 horas.
9. En el Explorador de web de Hola que es la página de inicio de anuncios de Contoso toohello abierto, cree un nuevo anuncio.

    Creación de un anuncio, hace un toobe de mensaje de cola creado, que se recoge Hola trabajo Web y se procesarán. Cuando llama a Hola SDK de WebJobs de mensaje de la cola de hello función tooprocess hello, código de hello alcanzará el punto de interrupción.
10. Cuando se interrumpe el depurador hello en el punto de interrupción, puede examinar y cambiar los valores de las variables mientras ejecuta el programa de hello en la nube Hola. Hola depurador de hello ilustración siguiente muestra contenido de Hola Hola blobInfo del objeto de que se pasó toohello GenerateThumbnail método.

     ![Objeto blobInfo en el depurador](./media/web-sites-dotnet-troubleshoot-visual-studio/blobinfo.png)
11. Presione toocontinue F5 ejecutando.

     Hola GenerateThumbnail método finaliza la creación de miniatura Hola.
12. En el Explorador de hello, página de índice de actualización hello y se ve Hola miniatura.
13. En Visual Studio, presione MAYÚS + F5 toostop depuración.
14. En **Explorador de servidores**, haga clic en hello ContosoAdsWebJob nodo y haga clic en **panel de vista**.
15. Inicie sesión con sus credenciales de Azure y, a continuación, haga clic en página toohello toogo nombre del trabajo Web hello para el trabajo Web.

     ![Clic en ContosoAdsWebJob](./media/web-sites-dotnet-troubleshoot-visual-studio/clickcaw.png)

     Hola panel muestra esa función GenerateThumbnail ejecutado recientemente Hola.

     (Hola la próxima vez que haga clic en **panel de vista**, no tiene toosign en y Explorador de hello directamente deja toohello página durante su trabajo Web.)
16. Haga clic en detalles de toosee de nombre de función de hello sobre la ejecución de la función de Hola.

     ![Detalles de la función](./media/web-sites-dotnet-troubleshoot-visual-studio/funcdetails.png)

Si la función [escribió registros](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs), puede hacer clic en **ToggleOutput** toosee ellos.

## <a name="notes-about-remote-debugging"></a>Notas acerca de la depuración remota
* No se recomienda ejecutar el modo de depuración en producción. Si la aplicación web de producción no se escala toomultiple instancias de servidor, la depuración evitará servidor web de Hola desde responde las solicitudes de tooother. Si lo hace varias instancias del servidor web, al adjuntar depurador toohello obtendrá una instancia aleatoria y no tiene el tooensure de ninguna manera ese explorador posterior solicitudes enviarán toothat instancia. Además, por lo general, no implemente un tooproduction de compilación de depuración, y las optimizaciones del compilador para las compilaciones de versión pueden hacer imposible tooshow lo que está sucediendo línea por línea en el código fuente. Para solucionar problemas de producción, su mejor recurso son los registros de servidor web y de seguimiento de la aplicación.
* Evite detenciones prolongadas en los puntos de interrupción durante la depuración remota. Azure considera un proceso detenido durante más de unos minutos como un proceso sin respuesta y lo apaga.
* Durante la depuración, el servidor de hello está enviando datos tooVisual Studio, que podría afectar a los cargos de ancho de banda. Para obtener información acerca de las tarifas de ancho de banda, consulte [Precios de Azure](https://azure.microsoft.com/pricing/calculator/).
* Asegúrese de que ese hello `debug` atributo de hello `compilation` elemento Hola *Web.config* archivo se establece tootrue. Tootrue se establece de forma predeterminada cuando se publica una configuración de compilación de depuración.

        <system.web>
          <compilation debug="true" targetFramework="4.5" />
          <httpRuntime targetFramework="4.5" />
        </system.web>
* Si encuentra que depurador hello no ir al código que desea que toodebug, quizás tenga la opción de solo mi código de hello de toochange.  Para obtener más información, consulte [restringir la ejecución paso a paso tooJust mi código](http://msdn.microsoft.com/library/vstudio/y740d9d3.aspx#BKMK_Restrict_stepping_to_Just_My_Code).
* Inicia un temporizador en el servidor de hello cuando se habilita la característica de depuración remota de Hola y después de 48 horas característica Hola se desactiva automáticamente. Este límite de 48 horas es por motivos de seguridad y rendimiento. Fácilmente puede activar la característica de hello en tantas veces como sea necesario. Recomendamos dejarla deshabilitada cuando no esté realizando activamente una depuración.
* Puede asociar manualmente Hola depurador tooany proceso, no solo hello web app (w3wp.exe). Para obtener más información acerca de cómo toouse modo de depuración en Visual Studio, vea [depurar en Visual Studio](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx).

## <a name="logsoverview"></a>Información general de registros de diagnóstico
Una aplicación de ASP.NET que se ejecuta en una aplicación web de Azure puede crear Hola siguientes tipos de registros:

* **Registros de seguimiento de aplicación**<br/>
  Hello aplicación crea estos registros llamando a métodos de hello [System.Diagnostics.Trace](http://msdn.microsoft.com/library/system.diagnostics.trace.aspx) clase.
* **Registros de servidor web**<br/>
  servidor web de Hello crea una entrada de registro para cada aplicación de web de toohello de solicitud HTTP.
* **Registros de mensaje de error detallados**<br/>
  servidor web de Hello crea una página HTML con información adicional para solicitudes con error HTTP (aquellas que son el resultado en el código de estado 400 o mayor).
* **Registros de seguimiento de solicitudes con error**<br/>
  servidor web de Hello crea un archivo XML con información de seguimiento detallada para las solicitudes HTTP con error. servidor web de Hello también proporciona un Hola XSL tooformat de archivo XML en un explorador.

Registro afecta al rendimiento de aplicación web, por lo que le ofrece Azure Hola capacidad tooenable o deshabilitar a cada tipo de registro según sea necesario. En el caso de registros de aplicaciones, puede especificar que solo se escriban los registros por encima de un determinado nivel de gravedad. Cuando crea una aplicación web, todos los registros están deshabilitados de manera predeterminada.

Toofiles se escriben los registros un *LogFiles* carpeta Hola sistema de archivos de su aplicación web y son accesible a través de FTP. Registros del servidor Web y registros de la aplicación también se pueden escribir tooan cuenta de almacenamiento de Azure. Puede conservar un mayor volumen de registros en una cuenta de almacenamiento que es posible en el sistema de archivos de Hola. Está limitado tooa máximo de 100 megabytes de registros cuando se usa el sistema de archivos de Hola. (Los registros del sistema de archivos solo sirven para la conservación a corto plazo. Azure elimina antiguo espacio toomake de archivos de registro para ver los nuevos cuando se alcanza el límite de hello).  

## <a name="apptracelogs"></a>Creación y visualización de registros de seguimiento de aplicación
En esta sección deberá llevar a cabo hello las siguientes tareas:

* Agregar proyecto de web de toohello de instrucciones de seguimiento que creó en [Introducción a Azure y ASP.NET][GetStarted].
* Ver los registros de hello cuando se ejecuta el proyecto de hello localmente.
* Ver los registros de hello tal y como se generan por aplicación Hola que se ejecuta en Azure.

Para obtener información acerca de cómo toocreate aplicación registra en trabajos Web, consulte [cómo toowork con el uso de almacenamiento de cola de Azure Hola SDK de WebJobs - modo toowrite registra](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs). Hello las instrucciones siguientes para ver registros y para controlar cómo se almacenan en Azure aplican también tooapplication registros creados por los trabajos Web.

### <a name="add-tracing-statements-toohello-application"></a>Agregar aplicación de toohello de instrucciones de seguimiento
1. Abra *controllers\homecontroller*y reemplace hello `Index`, `About`, y `Contact` código métodos con hello siguiendo en orden tooadd `Trace` instrucciones y un `using` instrucción para `System.Diagnostics`:

        public ActionResult Index()
        {
            Trace.WriteLine("Entering Index method");
            ViewBag.Message = "Modify this template toojump-start your ASP.NET MVC application.";
            Trace.TraceInformation("Displaying hello Index page at " + DateTime.Now.ToLongTimeString());
            Trace.WriteLine("Leaving Index method");
            return View();
        }

        public ActionResult About()
        {
            Trace.WriteLine("Entering About method");
            ViewBag.Message = "Your app description page.";
            Trace.TraceWarning("Transient error on hello About page at " + DateTime.Now.ToShortTimeString());
            Trace.WriteLine("Leaving About method");
            return View();
        }

        public ActionResult Contact()
        {
            Trace.WriteLine("Entering Contact method");
            ViewBag.Message = "Your contact page.";
            Trace.TraceError("Fatal error on hello Contact page at " + DateTime.Now.ToLongTimeString());
            Trace.WriteLine("Leaving Contact method");
            return View();
        }        
2. Agregar una `using System.Diagnostics;` parte superior de toohello de instrucción de archivo hello.

### <a name="view-hello-tracing-output-locally"></a>Seguimiento de hello vista salido localmente
1. Presione aplicación hello de F5 toorun en modo de depuración.

    agente de escucha de seguimiento de Hello predeterminado escribe todos los toohello de salida de seguimiento **salida** ventana, junto con otros resultados de la depuración. Hello en la ilustración siguiente se muestra hello resultado de hello las instrucciones de seguimiento que se ha agregado toohello `Index` método.

    ![Ventana de seguimiento en depuración](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugtracing.png)

    Hola siguientes pasos muestra cómo tooview la salida en una página web, sin tener que compilar en modo de depuración.
2. Abra el archivo Web.config de la aplicación hello (Hola uno ubicado en la carpeta del proyecto Hola) y agregue un `<system.diagnostics>` elemento final Hola de archivo hello justo antes de cerrarse de hello `</configuration>` elemento:

          <system.diagnostics>
            <trace>
              <listeners>
                <add name="WebPageTraceListener"
                    type="System.Web.WebPageTraceListener,
                    System.Web,
                    Version=4.0.0.0,
                    Culture=neutral,
                    PublicKeyToken=b03f5f7f11d50a3a" />
              </listeners>
            </trace>
          </system.diagnostics>

    Hola `WebPageTraceListener` le permiten ver los resultados de seguimiento examinando demasiado`/trace.axd`.
3. Agregar un <a href="http://msdn.microsoft.com/library/vstudio/6915t83k(v=vs.100).aspx">elemento trace</a> en `<system.web>` en el archivo Web.config de hello, como el siguiente ejemplo de Hola:

        <trace enabled="true" writeToDiagnosticsTrace="true" mostRecent="true" pageOutput="false" />
4. Presione la aplicación de hello toorun CTRL + F5.
5. En la barra de direcciones de Hola de ventana del explorador de hello, agregue *trace.axd* toohello dirección URL, y, a continuación, presione ENTRAR (dirección URL de hello será toohttp://localhost:53370/trace.axd similar).
6. En hello **seguimiento de la aplicación** página, haga clic en **ver detalles** en primera línea de hello (y no Hola BrowserLink línea).

    ![trace.axd](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-traceaxd1.png)

    Hola **detalles de la solicitud** aparece en la página y en hello **información de seguimiento** sección verá unos resultados de Hola de instrucciones de seguimiento de Hola que agregó toohello `Index` método.

    ![trace.axd](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-traceaxd2.png)

    De manera predeterminada, `trace.axd` solo está disponible localmente. Si deseara toomake está disponible desde una aplicación web remota, podría agregar `localOnly="false"` toohello `trace` elemento Hola *Web.config* de archivos, como se muestra en el siguiente ejemplo de Hola:

        <trace enabled="true" writeToDiagnosticsTrace="true" localOnly="false" mostRecent="true" pageOutput="false" />

    Sin embargo, habilitar `trace.axd` en producción aplicación web por lo general no se recomienda por motivos de seguridad, y en las secciones siguientes de hello, verá un tooread de manera más fácil de seguimiento en una aplicación web de Azure.

### <a name="view-hello-tracing-output-in-azure"></a>Ver el resultado del seguimiento de hello en Azure
1. En **el Explorador de soluciones**, haga clic en proyecto de web de Hola y haga clic en **publicar**.
2. Hola **Publicar Web** cuadro de diálogo, haga clic en **publicar**.

    Después de que Visual Studio publica su actualización, se abre una página principal del explorador ventana tooyour (suponiendo que no desactive **dirección URL de destino** en hello **conexión** ficha).
3. En el **Explorador de servidores**, haga clic con el botón derecho en su aplic. web y seleccione **Ver registros de streaming**.

    ![Ver registros de streaming en el menú contextual](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-viewlogsmenu.png)

    Hola **salida** ventana muestra que están conectado toohello transmisión por secuencias de registro del servicio y agrega una línea de notificación cada minuto que pasa el sin un toodisplay de registro.

    ![Ver registros de streaming en el menú contextual](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-nologsyet.png)
4. En la ventana del explorador de Hola que muestra la página de inicio de aplicación, haga clic en **póngase en contacto con**.

    Dentro de unos Hola de segundos de salida del seguimiento de nivel de error de hello agregado toohello `Contact` método aparece en hello **salida** ventana.

    ![Seguimiento de errores en la ventana Output](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-errortrace.png)

    Visual Studio sólo muestra seguimientos de nivel de error ya que ese es el valor predeterminado de hello cuando se habilita el registro de hello servicio de supervisión. Cuando se crea una nueva aplicación web de Azure, todos los registros se deshabilitan de forma predeterminada, tal y como se vio cuando abrió la página de configuración de hello anteriormente:

    ![Registro de aplicación desactivado](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-apploggingoff.png)

    Sin embargo, si seleccionó **ver registros de Streaming**, Visual Studio cambia automáticamente **aplicación Logging(File System)** demasiado**Error**, lo que significa que los registros de nivel de error informar. En el orden de toosee todos los registros de seguimiento, puede cambiar esta configuración demasiado**detallado**. Cuando selecciona un nivel de gravedad inferior al error, también se notifican todos los registros para niveles de gravedad más altos. Por lo tanto, cuando selecciona detallado, también verá registros de errores, advertencias e información.  

1. En **Explorador de servidores**, haga clic en la aplicación web de hello y, a continuación, haga clic en **ver la configuración de** como lo hizo anteriormente.
2. Cambio **(sistema de archivos) del registro de aplicaciones** demasiado**detallado**y, a continuación, haga clic en **guardar**.

    ![Establecer tooVerbose de nivel de seguimiento](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-applogverbose.png)
3. En ventana del explorador de Hola que ahora se muestra la **póngase en contacto con** página, haga clic en **inicio**, a continuación, haga clic en **sobre**y, a continuación, haga clic en **póngase en contacto con**.

    Dentro de unos segundos, Hola **salida** ventana muestra todos los resultados de seguimiento.

    ![Resultados detallados del seguimiento](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-verbosetraces.png)

    En esta sección aprendió a habilitar y deshabilitar el registro mediante la configuración de la aplicación web de Azure. También puede habilitar y deshabilitar los agentes de escucha de seguimiento modificando el archivo Web.config de Hola. Sin embargo, modificar el archivo Web.config de hello hace hello toorecycle de dominio de aplicación, mientras que al habilitar el registro mediante la configuración de aplicación web de hello no lo. Si el problema de hello toma un tooreproduce mucho tiempo o es intermitente, reciclaje de dominio de aplicación Hola podría "corregir" y forzar toowait hasta que se produce de nuevo. Permitir el diagnóstico en Azure no lo hace, por lo que puede comenzar inmediatamente a capturar información sobre el error.

### <a name="output-window-features"></a>Características de la ventana de salida
Hola **registros de Azure** ficha de hello **salida** ventana tiene varios botones y un cuadro de texto:

![Botones de la pestaña de registros](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-icons.png)

Estos operadores aritméticos realizan Hola siguientes funciones:

* Desactive hello **salida** ventana.
* Habilitar o deshabilitar el ajuste automático de línea.
* Iniciar o detener la supervisión de los registros.
* Especificar qué registros toomonitor.
* Descargar registros.
* Filtrar los registros según una cadena de búsqueda o una expresión regular.
* Hola cerrar **salida** ventana.

Si escribe una cadena de búsqueda o la expresión regular, Visual Studio filtra la información de registro en el cliente de Hola. Es decir, puede especificar criterios de hello después de que se muestran registros de Hola Hola **salida** ventana puede cambiar los criterios de filtrado sin tener tooregenerate Hola registros.

## <a name="webserverlogs"></a>Visualización de registros de servidor web
Registros de servidor Web registran toda la actividad HTTP para la aplicación web de Hola. En orden toosee ellas en hello **salida** ventana tiene tooenable para hello web app e indican a Visual Studio que desea toomonitor ellos.

1. Hola **configuración de aplicación Web de Azure** ficha que abrió desde **Explorador de servidores**, cambiar el registro del servidor Web también**en**y, a continuación, haga clic en **guardar**.

    ![Habilitar el registro de servidor web](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-webserverloggingon.png)
2. Hola **salida** ventana, haga clic en hello **especificar qué toomonitor registros de Azure** botón.

    ![Especifique qué toomonitor registros de Azure](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-specifylogs.png)
3. Hola **opciones de registro de Azure** cuadro de diálogo, seleccione **Web server registros**y, a continuación, haga clic en **Aceptar**.

    ![Supervisar los registros de servidor web](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-monitorwslogson.png)
4. En la ventana del explorador de Hola que muestra la aplicación web de hello, haga clic en **inicio**, a continuación, haga clic en **sobre**y, a continuación, haga clic en **póngase en contacto con**.

    registros de la aplicación Hello normalmente aparecen en primer lugar, seguida de hello registros del servidor web. Es posible que tenga toowait unos instantes para hello registra tooappear.

    ![Registros de servidor web en la ventana Output](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-wslogs.png)

De forma predeterminada, cuando se habilitan primero registros de servidor web mediante Visual Studio, Azure escribe Hola registros toohello FileSystem. Como alternativa, puede usar hello Azure portal toospecify que web server registros debe escribirse tooa contenedor de blobs en una cuenta de almacenamiento.

Si utiliza el servidor de web de portal tooenable Hola registro tooan cuenta de almacenamiento de Azure y, a continuación, deshabilite el registro en Visual Studio, al volver a habilitar el registro en Visual Studio se restaura la configuración de la cuenta de almacenamiento.

## <a name="detailederrorlogs"></a>Visualización de registros de mensajes de error detallados
Los registros de error detallados proporcionan información adicional acerca de las solicitudes HTTP que generaron códigos de respuesta con error (400 o superiores). En orden toosee ellas en hello **salida** ventana, tendrá que tooenable para hello web app e indican a Visual Studio que desea toomonitor ellos.

1. Hola **configuración de aplicación Web de Azure** ficha que abrió desde **Explorador de servidores**, cambiar **mensajes de Error detallados** demasiado**en**, y a continuación, haga clic en **guardar**.

    ![Habilitar los mensajes de error detallados](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailedlogson.png)
2. Hola **salida** ventana, haga clic en hello **especificar qué toomonitor registros de Azure** botón.
3. Hola **opciones de registro de Azure** cuadro de diálogo, haga clic en **todos los registros de**y, a continuación, haga clic en **Aceptar**.

    ![Supervisar todos los registros](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-monitorall.png)
4. En la barra de direcciones de Hola de ventana del explorador de hello, agregar una dirección URL de toohello carácter adicional toocause un 404 error (por ejemplo, `http://localhost:53370/Home/Contactx`), y presione ENTRAR.

    Después de unos segundos aparece registro de errores detallado de Hola Hola Visual Studio **salida** ventana.

    ![Registro de error detallado en la ventana Resultados](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailederrorlog.png)

    Controlar y haga clic en salida de registro de hello en toosee de hello vínculo con formato en un explorador:

    ![Registro de error detallado en la ventana del explorador](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailederrorloginbrowser.png)

## <a name="downloadlogs"></a>Descarga de registros del sistema de archivos
Los registros que se pueden supervisar en hello **salida** ventana también pueden descargarse como un *.zip* archivo.

1. Hola **salida** ventana, haga clic en **descargar registros de Streaming**.

    ![Botones de la pestaña de registros](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-downloadicon.png)

    Abre el Explorador de archivos tooyour *descarga* carpeta con hello descargar el archivo seleccionado.

    ![Archivo descargado](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-downloadedfile.png)
2. Extraer hello *.zip* archivo y ver Hola siguiendo la estructura de carpetas:

    ![Archivo descargado](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-logfilefolders.png)

   * Registros de seguimiento de la aplicación están en *.txt* archivos Hola *LogFiles\Application* carpeta.
   * Los registros de servidor Web están en *.log* archivos Hola *LogFiles\http\RawLogs* carpeta. Puede usar una herramienta como [analizador del registro](http://www.microsoft.com/download/details.aspx?displaylang=en&id=24659) tooview y manipular estos archivos.
   * Registros de mensajes de error detallados están en *.html* archivos Hola *LogFiles\DetailedErrors* carpeta.

     (hello *implementaciones* carpeta es para los archivos creados por el control de código fuente de publicación; no tiene una publicación de Studio tooVisual cualquier elemento relacionado. Hola *Git* carpeta es seguimientos relacionados toosource control hello y publicación de archivo de registro de servicio de streaming.)  

## <a name="storagelogs"></a>Visualización de registros de almacenamiento
Registros de seguimiento de la aplicación también pueden enviarse tooan cuenta de almacenamiento de Azure, y puede verlos en Visual Studio. toodo que deberá crear una cuenta de almacenamiento, habilitar los registros de almacenamiento en el portal clásico de Hola y verlos en hello **registros** ficha de hello **aplicación Web de Azure** ventana.

Puede enviar registros tooany o la totalidad de tres destinos:

* sistema de archivos de Hola.
* Tablas de cuentas de almacenamiento.
* Blobs de cuentas de almacenamiento.

Puede especificar un nivel de gravedad distinto para cada destino.

Las tablas que sea fácil tooview detalles de registros en línea y que admiten la transmisión por secuencias; puede realizar consultas de registros en tablas y ver los nuevos registros tal y como se crea. Blobs que sea fácil toodownload registros en archivos y tooanalyze mediante HDInsight, porque HDInsight sabe cómo toowork con almacenamiento de blobs. Para obtener más información, consulte **Hadoop y MapReduce** en [Opciones de almacenamiento de datos (Creación de aplicaciones reales con Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options).

Actualmente tiene nivel de tooverbose de conjunto de registros de la sistema de archivos; Hello pasos siguientes aprenderá a través de configuración de tablas de información de nivel de registros toogo toostorage cuenta. El nivel de información se refiere a que se mostrarán todos los registros creados al llamar a  `Trace.TraceInformation`, `Trace.TraceWarning` y `Trace.TraceError`, pero no los creados al llamar a `Trace.WriteLine`.

Las cuentas de almacenamiento ofrecen más almacenamiento y duraderas y retención de registros en comparación con el sistema de archivos de toohello. Otra ventaja de la aplicación de envío toostorage de registros de seguimiento es que se obtiene información adicional con cada registro que no obtendrá de registros del sistema de archivos.

1. Haga clic en **almacenamiento** en Hola nodos de Azure y, a continuación, haga clic en **crear cuenta de almacenamiento**.

![Crear cuenta de almacenamiento](./media/web-sites-dotnet-troubleshoot-visual-studio/createstor.png)

1. Hola **crear cuenta de almacenamiento** cuadro de diálogo, escriba un nombre para la cuenta de almacenamiento de Hola.

    debe ser el nombre de Hello debe ser único (ninguna otra cuenta de almacenamiento de Azure puede tener Hola mismo nombre). Si nombre hello especificado ya está en uso obtendrá un toochange posibilidad.

    Hola tooaccess de dirección URL será la cuenta de almacenamiento *{name}*. core.windows.net.
2. Conjunto hello **región o grupo de afinidad** tooyou de lista desplegable toohello región más cercana.

    Esta configuración especifica el centro de datos de Azure que va a almacenar la cuenta de almacenamiento. Para este tutorial, su elección no suponer una diferencia notable, pero para una aplicación web de producción que desea que el servidor web y la toobe de la cuenta de almacenamiento en hello mismo latencia toominimize de región y datos cargos de salida. aplicación web de Hello (que creará más adelante) debe ejecutarse en una región lo más cerca exploradores toohello posible obtener acceso a la aplicación web de latencia de toominimize de orden.
3. Conjunto hello **replicación** lista desplegable lista demasiado**redundancia local**.
   
    Replicación geográfica está habilitada para una cuenta de almacenamiento, contenido de hello almacenado replicada tooa centro de datos secundario tooenable conmutación por error toothat ubicación es en el caso de un desastre importante en la ubicación principal de Hola. La replicación geográfica puede suponer costes adicionales. Para las cuentas de prueba y desarrollo, generalmente no desea toopay para la replicación geográfica. Para obtener más información, consulte [Creación, administración o eliminación de una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md).
4. Haga clic en **Crear**.

    ![New storage account](./media/web-sites-dotnet-troubleshoot-visual-studio/newstorage.png)    
5. En Visual Studio hello **aplicación Web de Azure** ventana, haga clic en hello **registros** ficha y, a continuación, haga clic en **configurar registro en el Portal de administración**.

    <!-- todo:screenshot of new portal if hello VS page link goes toonew portal -->
    ![registro](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-configlogging.png)

    Se abrirá hello **configurar** Hola portal clásico de la aplicación web de.
6. En del portal clásico de hello **configurar** ficha, desplácese hacia abajo de la sección de diagnósticos de aplicación toohello y, a continuación, cambiar **(almacenamiento de tabla) de registro de aplicaciones** demasiado**en**.
7. Cambio **Logging Level** demasiado**información**.
8. Haga clic en **Administrar almacenamiento de tablas**.

    ![Hacer clic en Manage Table Storage](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-stgsettingsmgmtportal.png)

    Hola **administrar almacenamiento de tablas para application diagnostics** cuadro, puede elegir la cuenta de almacenamiento si tiene más de uno. Puede crear una tabla o usar una existente.

    ![Administrar almacenamiento de tablas](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-choosestorageacct.png)
9. Hola **administrar almacenamiento de tablas para application diagnostics** cuadro, haga clic en cuadro de Hola de tooclose de marca de verificación de Hola.
10. En del portal clásico de hello **configurar** , haga clic en **guardar**.
11. En la ventana del explorador de Hola que muestra la aplicación de hello aplicación web, haga clic en **inicio**, a continuación, haga clic en **sobre**y, a continuación, haga clic en **póngase en contacto con**.

     información de registro de Hello producidos por examinar estas páginas web se escribirán toohello cuenta de almacenamiento.
12. Hola **registros** ficha de hello **aplicación Web de Azure** ventana de Visual Studio, haga clic en **actualizar** en **resumen de diagnóstico**.

     ![Haga clic en Actualizar](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-refreshstorage.png)

     Hola **resumen de diagnóstico** sección muestra registros de hello últimos 15 minutos de forma predeterminada. Puede cambiar toosee período hello más registros.

     (Si se producirá un error de "tabla no se encuentra", compruebe que examinarse páginas toohello que Hola seguimiento después de haber habilitado **(almacenamiento) de registro de aplicaciones** y después hizo clic **guardar**.)

     ![Registros de almacenamiento](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-storagelogs.png)

     Observe que en esta vista vea **Id. de proceso** y **Thread ID** para cada registro, que no obtendrá en hello registros del sistema de archivos. Puede ver campos adicionales mediante la visualización de tabla de almacenamiento de Azure Hola directamente.
13. Haga clic en **Ver todos los registros de aplicación**.

     tabla de registro de seguimiento de Hello aparece en el Visor de tablas de almacenamiento de Azure Hola.

     (Si se producirá un error de "secuencia no contiene elementos", abra **Explorador de servidores**, expanda el nodo de hello para la cuenta de almacenamiento en hello **Azure** nodo y, a continuación, haga **tablas**y haga clic en **actualizar**.)

     ![Registros de almacenamiento en vista de tabla](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-tracelogtableview.png)

     Esta vista muestra campos adicionales que no están disponibles en otras vistas. Esta vista también permite toofilter registros mediante especial interfaz de usuario de generador de consultas para construir una consulta. Para obtener más información, consulte Trabajo con recursos de tabla - Filtrado de entidades en [Exploración de recursos de almacenamiento con el Explorador de servidores](http://msdn.microsoft.com/library/ff683677.aspx).
14. toolook en los detalles de Hola para una sola fila, haga doble clic en una de las filas de Hola.

     ![Tabla de seguimiento en el Explorador de servidores](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-tracetablerow.png)

## <a name="failedrequestlogs"></a>Visualización de registros de seguimiento de solicitudes con error
Registros de seguimiento de solicitudes con error son útiles cuando es necesario toounderstand detalles de Hola de cómo IIS lleva a cabo una solicitud HTTP, en escenarios como los problemas de autenticación o la reescritura de direcciones URL.

Hola de uso de aplicaciones web de Azure mismo no se pudo solicitar la funcionalidad de seguimiento que ha estado disponible con IIS 7.0 y versiones posteriores. No es necesario toohello acceso a configuración de IIS que configura qué errores se registran, sin embargo. Cuando habilita el seguimiento de solicitudes con error, se capturan todos los errores.

Puede habilitar el seguimiento de solicitudes con error a través de Visual Studio, pero no puede verlas ahí. Estos registros son archivos XML. transmisión por secuencias solo el servicio de registro de Hello supervisa los archivos que se consideran legibles en modo de texto sin formato: *.txt*, *.html*, y *.log* archivos.

Puede ver los registros de seguimiento de solicitudes con error en un explorador directamente a través de FTP o localmente después de usar un toodownload de herramienta FTP ellos tooyour de equipo local. En esta sección los verá directamente en un explorador.

1. Hola **configuración** ficha de hello **aplicación Web de Azure** ventana que abrió desde **Explorador de servidores**, cambiar **Failed Request Tracing**demasiado**en**y, a continuación, haga clic en **guardar**.

    ![Habilitar el seguimiento de solicitudes con error](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-failedrequeston.png)
2. En la barra de direcciones de Hola de ventana del explorador de Hola que muestra la aplicación web de hello, agregue una dirección URL toohello de carácter adicional y haga clic en entrar toocause un error 404.

    Esto hace que un toobe de registro de seguimiento de solicitudes con error creado y hello pasos siguientes muestran cómo tooview o descarga Hola registro.
3. En Visual Studio, en hello **configuración** ficha de hello **aplicación Web de Azure** ventana, haga clic en **abrir en el Portal de administración**.
4. Hola [Portal de Azure](https://portal.azure.com) **configuración** hoja de la aplicación web, haga clic en **las credenciales de implementación**y, a continuación, escriba un nuevo nombre de usuario y una contraseña.

    ![Nuevo nombre de usuario y contraseña de FTP](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-enterftpcredentials.png)

    ** Al iniciar sesión, tiene nombre de usuario completo de hello toouse con tooit como prefijo del nombre de hello web app. Por ejemplo, si escribe "MiID" como un nombre de usuario y el sitio de hello es "myexample", inicie sesión como "myexample\myid".
5. En una nueva ventana del explorador, vaya toohello URL que se muestra en **nombre de host FTP** o **FTPS hostname** en hello **aplicación Web** hoja de la aplicación web.
6. Inicie sesión con credenciales de hello FTP que creó anteriormente (incluidas las hello web prefijo de nombre de aplicación para el nombre de usuario de hello).

    Explorador de Hello muestra la carpeta de raíz de Hola de hello web app.
7. Abra hello *LogFiles* carpeta.

    ![Abrir la carpeta LogFiles](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-logfilesfolder.png)
8. Abra la carpeta de Hola que se denomina W3SVC además de un valor numérico.

    ![Abrir la carpeta W3SVC](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-w3svcfolder.png)

    carpeta de Hello contiene archivos XML para los errores que se han registrado después de haber habilitado el seguimiento de solicitudes con error y un archivo XSL que puede utilizar un explorador tooformat Hola XML.

    ![Carpeta W3SVC](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-w3svcfoldercontents.png)
9. Haga clic en el archivo XML de hello para solicitudes con error Hola que desee toosee información de seguimiento para.

    Hello en la ilustración siguiente se muestra parte de la información de seguimiento de Hola para un error de ejemplo.

    ![Seguimiento de solicitudes con error en un explorador](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-failedrequestinbrowser.png)

## <a name="nextsteps"></a>Pasos siguientes
Ha visto cómo Visual Studio hace que sea fácil tooview registros creados por una aplicación web de Azure. Hello las secciones siguientes proporcionan vínculos toomore recursos en temas relacionados:

* Solución de problemas de las aplicaciones web de Azure
* Depuración en Visual Studio
* Depuración remota en Azure
* Seguimiento en aplicaciones de ASP.NET
* Análisis de registros de servidor web
* Análisis de registros de seguimiento de solicitudes con error
* Depuración de Servicios en la nube

### <a name="azure-web-app-troubleshooting"></a>Solución de problemas de las aplicaciones web de Azure
Para obtener más información sobre cómo solucionar problemas de aplicaciones web en el servicio de aplicaciones de Azure, vea Hola recursos siguientes:

* [¿Cómo toomonitor aplicaciones de web](/manage/services/web-sites/how-to-monitor-websites/)
* [Investigación de fugas de memoria en Aplicaciones web de Azure con Visual Studio 2013](http://blogs.msdn.com/b/visualstudioalm/archive/2013/12/20/investigating-memory-leaks-in-azure-web-sites-with-visual-studio-2013.aspx). Artículo del blog ALM de Microsoft sobre las características de Visual Studio para el análisis de problemas de memoria administrada.
* [Herramientas en línea de Aplicaciones web de Azure que debe conocer](https://azure.microsoft.com/blog/2014/03/28/windows-azure-websites-online-tools-you-should-know-about-2/). Publicación en el blog de Amit Apple.

Para obtener ayuda con una pregunta específica de solución de problemas, iniciar un subproceso en uno de los siguientes foros de Hola:

* [Hola foro de Azure en el sitio ASP.NET de hello](http://forums.asp.net/1247.aspx/1?Azure+and+ASP+NET).
* [Hola foro de Azure en MSDN](http://social.msdn.microsoft.com/Forums/windowsazure/).
* [StackOverflow.com](http://www.stackoverflow.com).

### <a name="debugging-in-visual-studio"></a>Depuración en Visual Studio
Para obtener más información acerca de cómo toouse modo de depuración en Visual Studio, vea hello [depurar en Visual Studio](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx) tema de MSDN y [sugerencias de depuración con Visual Studio 2010](http://weblogs.asp.net/scottgu/archive/2010/08/18/debugging-tips-with-visual-studio-2010.aspx).

### <a name="remote-debugging-in-azure"></a>Depuración remota en Azure
Para obtener más información sobre la depuración remota de aplicaciones web de Azure y trabajos Web, vea Hola recursos siguientes:

* [Introducción tooRemote depuración de aplicación de servicio de aplicaciones Web de Azure](https://azure.microsoft.com/blog/2014/05/06/introduction-to-remote-debugging-on-azure-web-sites/).
* [Introducción tooRemote depuración de aplicación de servicio de aplicaciones Web de Azure parte 2, dentro de la depuración remota](https://azure.microsoft.com/blog/2014/05/07/introduction-to-remote-debugging-azure-web-sites-part-2-inside-remote-debugging/)
* [Introducción tooRemote depuración por parte de aplicaciones de Web del servicio de aplicación de Azure 3 - entorno de varias instancias y GIT](https://azure.microsoft.com/blog/2014/05/08/introduction-to-remote-debugging-on-azure-web-sites-part-3-multi-instance-environment-and-git/)
* [Depuración de WebJobs](https://www.youtube.com/watch?v=ncQm9q5ZFZs&list=UU_SjTh-ZltPmTYzAybypB-g&index=1)

Si la aplicación web utiliza una API Web de Azure o servicios móviles de back-end y necesita toodebug que vea [depuración de .NET back-end en Visual Studio](http://blogs.msdn.com/b/azuremobile/archive/2014/03/14/debugging-net-backend-in-visual-studio.aspx).

### <a name="tracing-in-aspnet-applications"></a>Seguimiento en aplicaciones de ASP.NET
No hay ningún tooASP.NET introducciones completa y actualizada de seguimiento disponibles en hello Internet. Hola mejor que puede hacer es empezar a trabajar con material introductorio antiguo escrito para formularios Web Forms porque MVC no existe todavía y complemente con blog más recientes publicaciones que se centran en problemas específicos. Algunos toostart buenas fuentes son Hola recursos siguientes:

* [Supervisión y telemetría (crear aplicaciones en la nube para el mundo real con Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry).<br>
  Capítulo de un libro electrónico con recomendaciones para realizar seguimiento en aplicaciones de la nube de Azure.
* [Seguimiento de ASP.NET](http://msdn.microsoft.com/library/ms972204.aspx)<br/>
  Antiguo pero todavía un buen recurso para un asunto de toohello introducción básica.
* [Agentes de escucha de seguimiento](http://msdn.microsoft.com/library/4y5y10s7.aspx)<br/>
  Obtener información sobre los agentes de escucha de seguimiento, pero no mencione hello [WebPageTraceListener](http://msdn.microsoft.com/library/system.web.webpagetracelistener.aspx).
* [Tutorial: Integración del seguimiento de ASP.NET con el seguimiento de System.Diagnostics](http://msdn.microsoft.com/library/b0ectfxd.aspx)<br/>
  Esto es antigua demasiado, pero incluye información adicional no tratados en dicho artículo introductorio Hola.
* [Seguimiento en vistas Razor de ASP.NET MVC](http://blogs.msdn.com/b/webdev/archive/2013/07/16/tracing-in-asp-net-mvc-razor-views.aspx)<br/>
  Además de traza en las vistas de Razor, post hello también explica cómo toocreate error filtrar en orden toolog excepciones no controladas todo en una aplicación MVC. Para obtener información acerca de cómo no controlada toolog todas las excepciones en una aplicación de formularios Web Forms, vea el ejemplo de Global.asax hello en [ejemplo completo para los controladores de Error](http://msdn.microsoft.com/library/bb397417.aspx) en MSDN. En MVC o formularios Web Forms, si desea toolog ciertas excepciones pero permiten framework predeterminado de hello control surten efecto para ellos, puede detectar y volver a producirlas como en el siguiente ejemplo de Hola:

        try
        {
           // Your code that might cause an exception toobe thrown.
        }
        catch (Exception ex)
        {
            Trace.TraceError("Exception: " + ex.ToString());
            throw;
        }
* [Transmisión por secuencias de registro de seguimiento de diagnóstico desde la línea de comandos de Azure hello (más perspectiva!)](http://www.hanselman.com/blog/StreamingDiagnosticsTraceLoggingFromTheAzureCommandLinePlusGlimpse.aspx)<br/>
  ¿Cómo toouse Hola toodo de línea de comandos qué este tutorial muestra cómo toodo en Visual Studio. [Glimpse](http://www.hanselman.com/blog/IfYoureNotUsingGlimpseWithASPNETForDebuggingAndProfilingYoureMissingOut.aspx) es una herramienta de depuración de aplicaciones ASP.NET.
* [Uso de diagnósticos y registro de Web Apps - con David Ebbo](/documentation/videos/azure-web-site-logging-and-diagnostics/) y [Registros de streaming desde Web Apps - con David Ebbo](/documentation/videos/log-streaming-with-azure-web-sites/)<br>
  Vídeos de Scott Hanselman y David Ebbo.

Para el registro de error, una alternativa toowriting su propio código de seguimiento es toouse un código abierto de marco de registro como [ELMAH](http://nuget.org/packages/elmah/). Para obtener más información, consulte [Publicaciones de blog de Scott Hanselman sobre ELMAH](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx).

Además, tenga en cuenta que no tiene toouse ASP.NET o registros de seguimiento de System.Diagnostics si desea tooget de transmisión por secuencias de Azure. Hello aplicación web de Azure que el servicio de registro de streaming transmitirá cualquiera *.txt*, *.html*, o *.log* archivo que encuentre en hello *LogFiles* carpeta. Por lo tanto, puede crear su propio sistema de registro que escribe toohello sistema de archivos de aplicación web de Hola y el archivo se transmite por secuencias y descargar automáticamente. Lo único que toodo es escribir código de aplicación que crea archivos en hello *d:\home\logfiles* carpeta.

### <a name="analyzing-web-server-logs"></a>Análisis de registros de servidor web
Para obtener más información acerca del análisis de registros de servidor web, vea Hola recursos siguientes:

* [LogParser](http://www.microsoft.com/download/details.aspx?id=24659)<br/>
  Una herramienta para visualizar datos en registros de servidor web (archivos*.log* ).
* [Solución de problemas de rendimiento de IIS o errores de aplicación al usar LogParser](http://www.iis.net/learn/troubleshoot/performance-issues/troubleshooting-iis-performance-issues-or-application-errors-using-logparser)<br/>
  Registra una herramienta de analizador del registro de toohello de introducción que puede usar el servidor de web tooanalyze.
* [Publicaciones en el blog de Robert McMurray sobre el uso de LogParser](http://blogs.msdn.com/b/robert_mcmurray/archive/tags/logparser/)<br/>
* [Hola código de estado HTTP en IIS 7.0, IIS 7.5 y 8.0 de IIS](http://support.microsoft.com/kb/943891)

### <a name="analyzing-failed-request-tracing-logs"></a>Análisis de registros de seguimiento de solicitudes con error
sitio Web de Microsoft TechNet Hola incluye un [Using Failed Request Tracing](http://www.iis.net/learn/troubleshoot/using-failed-request-tracing) sección que puede ser útil para comprender cómo toouse estos registros. Sin embargo, esta documentación se centra principalmente en la configuración del seguimiento de solicitudes con error en IIS, algo que no puede hacer en Aplicaciones web Azure.

[GetStarted]: app-service-web-get-started-dotnet.md
[GetStartedWJ]: websites-dotnet-webjobs-sdk.md
