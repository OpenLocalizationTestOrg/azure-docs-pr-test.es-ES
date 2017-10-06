---
title: "aplicación web móvil de aaaDeploy un MVC de ASP.NET 5 en el servicio de aplicación de Azure"
description: "Un tutorial que le enseña cómo toodeploy una tooAzure de aplicación web servicio de aplicaciones con móviles características en ASP.NET MVC de aplicación web 5."
services: app-service
documentationcenter: .net
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 0752c802-8609-4956-a755-686116913645
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 01119c07246c0252fd357562774a2e90b3ef77d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-aspnet-mvc-5-mobile-web-app-in-azure-app-service"></a>Implementar una aplicación web móvil de ASP.NET MVC 5 en el servicio de aplicaciones de Azure
Este tutorial le mostrará también Hola conceptos básicos de cómo toobuild un 5 de MVC de ASP.NET web aplicación que está preparado para dispositivos móviles e implementarlo tooAzure servicio de aplicaciones. Para este tutorial, necesita [Visual Studio Express 2013 para Web] [ Visual Studio Express 2013] Hola edición o professional de Visual Studio si ya tienes que. Puede usar [Visual Studio 2015] pero capturas de pantalla de hello serán diferentes y se deben utilizar plantillas de hello ASP.NET 4.x.

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-youll-build"></a>Lo que creará
Para este tutorial, agregará características para móviles toohello conferencia lista aplicación simple que se proporciona en hello [proyecto inicial][StarterProject]. Hello captura de pantalla siguiente muestra las sesiones ASP.NET de hello en aplicación Hola completado, tal como se muestra en el emulador de explorador hello en herramientas de desarrollo F12 de Internet Explorer 11.

![][FixedSessionsByTag]

Puede usar herramientas de desarrollo F12 de Internet Explorer 11 Hola y Hola [herramienta Fiddler] [ Fiddler] toohelp depurar la aplicación. 

## <a name="skills-youll-learn"></a>Habilidades que aprenderá
Aprenderá lo siguiente:

* ¿Cómo toouse Visual Studio 2013 toopublish su aplicación web directamente tooa aplicación web en el servicio de aplicación de Azure.
* Cómo plantillas Hola ASP.NET MVC 5 usar framework de arranque de CSS de Hola para mejorar la visualización en dispositivos móviles
* ¿Cómo toocreate específica para equipos móviles vistas exploradores móviles específico tootarget, como Hola iPhone y Android
* ¿Cómo toocreate respondiendo vistas (vistas que respondan toodifferent exploradores en todos los dispositivos)

## <a name="set-up-hello-development-environment"></a>Configurar el entorno de desarrollo de Hola
Configurar el entorno de desarrollo instalando hello Azure SDK para .NET 2.5.1 o una versión posterior. 

1. tooinstall hello Azure SDK para. NET, haga clic en el siguiente vínculo de Hola. Si no tiene Visual Studio 2013 instalado todavía, se instalará por el vínculo de Hola. Este tutorial requiere Visual Studio 2013. [Azure SDK para Visual Studio 2013][AzureSDKVs2013]
2. En la ventana del instalador de plataforma Web de hello, haga clic en **instalar** y continuar con la instalación de Hola.

También necesitará un emulador de explorador móvil. Ninguno de los siguientes Hola funcionará:

* Emulador de explorador en las herramientas para desarrolladores de [Internet Explorer 11 F12][EmulatorIE11] (se usan en todas las capturas de pantalla de explorador móvil). Cuenta con los calores predefinidos de cadena de agente de usuario para Windows Phone 8, Windows Phone 7 y Apple iPad.
* Emulador de explorador en [Google Chrome DevTools][EmulatorChrome]. Contiene valores predefinidos para varios dispositivos Android, así como Apple iPhone, Apple iPad y Amazon Kindle Fire. También emula eventos táctiles.
* [Emulador de Opera Mobile][EmulatorOpera]

Proyectos de Visual Studio con C\# código fuente está tooaccompany disponible en este tema:

* [Descarga del proyecto inicial][StarterProject]
* [Descarga del proyecto completado][CompletedProject]

## <a name="bkmk_DeployStarterProject"></a>Implementar la aplicación web de Azure de hello starter proyecto tooan
1. Descargar la aplicación de lista de la conferencia de hello [proyecto inicial][StarterProject].
2. A continuación, en el Explorador de Windows, haga clic en archivo ZIP de descarga de Hola y elija *propiedades*.
3. Hola **propiedades** diálogo cuadro, elija hello **Unblock** botón. (Desbloqueo impide que una advertencia de seguridad que se produce cuando intenta toouse un *.zip* archivo que descargó desde web Hola.)
4. Haga clic en archivo ZIP de Hola y seleccione **extraer todo** para descomprimir el archivo hello. 
5. En Visual Studio, abra hello *C#\Mvc5Mobile.sln* archivo.
6. En el Explorador de soluciones, haga clic en proyecto de Hola y haga clic en **publicar**.
   
   ![][DeployClickPublish]
7. En Publicación web, haga clic en **Servicio de aplicaciones de Microsoft Azure**.
   
   ![][DeployClickWebSites]
8. Si aún no inició sesión en Azure, haga clic en **Agregar una cuenta**.
   
   ![][DeploySignIn]
9. Siga toolog de mensajes de Hola en su cuenta de Azure.
10. Hola, cuadro de diálogo de servicio de aplicaciones debería aparecer ahora como iniciado sesión. Haga clic en **Nuevo**.
    
    ![][DeployNewWebsite]  
11. Hola **nombre de la aplicación Web** , a continuación, especifique un prefijo de nombre de aplicación único. El nombre completo del sitio será *&lt;prefijo>*.azurewebsites.net. Además, seleccione o especifique un nuevo nombre de grupo de recursos en **Grupo de recursos**. A continuación, haga clic en **New** toocreate un nuevo plan de servicio de aplicaciones.
    
    ![][DeploySiteSettings]
12. Configurar Hola nuevo plan de servicio de aplicaciones y haga clic en **Aceptar**. 
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7a.png)
13. En cuadro de diálogo de hello crear servicio en la aplicación, haga clic en **crear**.
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7b.png) 
14. Después de hello recursos de Azure se crean, cuadro de diálogo de publicación Web de Hola se rellenará con valores de hello para la nueva aplicación. Haga clic en **Publicar**.
    
    ![][DeployPublishSite]
    
    Una vez que Visual Studio finaliza la aplicación web de Azure starter proyecto toohello de publicación hello, Explorador de escritorio de hello abre la aplicación web en directo de toodisplay hello.
15. Inicie el emulador de explorador móvil, copie la dirección URL de hello para la aplicación de la conferencia de hello (*<prefix>*. azurewebsites.net) en el emulador de Windows hello y, a continuación, haga clic en el botón de la parte superior derecha y seleccione **Examinar por etiqueta**. Si usa Internet Explorer 11 como explorador predeterminado de hello, solo deberá tootype `F12`, a continuación, `Ctrl+8`y, a continuación, cambiar perfil de explorador Hola demasiado**de Windows Phone**. La imagen siguiente muestra hello *AllTags* vista en modo vertical (de la elección de **Examinar por etiqueta**).
    
    ![][AllTags]

> [!TIP]
> Aunque puede depurar su aplicación de MVC 5 desde dentro de Visual Studio, puede publicar su tooAzure de aplicación web nuevo tooverify hello en vivo aplicación web directamente desde el explorador móvil o un emulador de explorador.
> 
> 

Visualización de Hello es muy legible en un dispositivo móvil. También puede ver algunos efectos visuales de hello aplicados por el marco de trabajo de hello Bootstrap CSS.
Haga clic en hello **ASP.NET** vínculo.

![][SessionsByTagASP.NET]

Hola vista de etiqueta ASP.NET es pantalla toohello ajusta el zoom, que arranque realiza automáticamente de forma automática. Sin embargo, puede mejorar este explorador móvil vista toobetter palo Hola. Por ejemplo, hello **fecha** columna es difícil de leer. Más adelante en el tutorial Hola cambiará hello *AllTags* ver toomake, preparadas para dispositivos móviles.

## <a name="bkmk_bootstrap"></a> Marco Bootstrap CSS
Nuevo en hello MVC 5 plantilla es la compatibilidad integrada de arranque. Ya hemos visto cómo mejora inmediatamente vistas diferentes de hello en la aplicación. Por ejemplo, barra de navegación superior de Hola Hola es contraíble automáticamente al ancho del explorador de hello es pequeño. En el Explorador de escritorio de hello, intente cambiar el tamaño de la ventana del explorador de Hola y ver cómo la barra de navegación de hello cambia su apariencia y funcionamiento. Se trata de diseño de web con capacidad de respuesta de Hola que está integrado en el arranque.

toosee cómo la aplicación Web de hello sería sin arranque, abra *aplicación\_iniciar\\BundleConfig.cs* y marque como comentario las líneas de Hola que contengan *bootstrap.js* y *bootstrap.css*. Hello código siguiente muestra hello las dos últimas instrucciones de hello `RegisterBundles` método después de cambiar de hello:

     bundles.Add(new ScriptBundle("~/bundles/bootstrap").Include(
              //"~/Scripts/bootstrap.js",
              "~/Scripts/respond.js"));

    bundles.Add(new StyleBundle("~/Content/css").Include(
              //"~/Content/bootstrap.css",
              "~/Content/site.css"));

Presione `Ctrl+F5` aplicación de hello toorun.

Observe que esa barra de navegación contraíble Hola ahora es simplemente una lista sin ordenar normal. Haga nuevamente clic en **Explorar por etiqueta** y luego haga clic en **ASP.NET**.
En la vista del emulador de dispositivos móviles de hello, verá ahora que ya no es pantalla toohello ajusta el zoom y debe desplazar hacia un lado en orden toosee Hola derecha de la tabla de Hola.

![][SessionsByTagASP.NETNoBootstrap]

Deshacer los cambios y actualizar Hola explorador móvil tooverify que se ha restaurado la presentación de hello preparadas para dispositivos móviles.

Bootstrap no es específico tooASP.NET MVC 5, y puede aprovechar estas características en cualquier aplicación web. Sin embargo, ahora está integrado en la plantilla de proyecto de ASP.NET MVC 5, por lo que su aplicación web MVC 5 puede sacar provecho de Bootstrap de manera predeterminada.

Para obtener más información acerca de arranque, consulte toothe [arranque] [ BootstrapSite] sitio.

En la sección siguiente Hola verá cómo vistas específicas de tooprovide explorador móvil.

## <a name="bkmk_overrideviews"></a>Reemplazar Hola vistas, diseños y las vistas parciales
Puede reemplazar cualquier vista (incluidos los diseños y las vistas parciales) para exploradores móviles en general, para un explorador móvil individual o para cualquier explorador específico. ver de un determinado mobile tooprovide, puede copiar un archivo de vista y agregar *. Mobile* toohello nombre de archivo. Toocreate por ejemplo, un teléfono móvil *índice* vista, puede copiar *vistas\\inicio\\Index.cshtml* a *vistas\\inicio\\ Index.Mobile.cshtml*.

En esta sección, creará un archivo de diseño específico para móviles.

toostart, copia *vistas\\Shared\\\_Layout.cshtml* a *vistas\\Shared\\\_Layout.Mobile.cshtml* . Abra  *\_Layout.Mobile.cshtml* y cambie el título de Hola de **MVC5 aplicación** demasiado**MVC5 aplicación (móvil)**.

En cada uno de ellos `Html.ActionLink` prevén la barra de navegación de hello, quite "Buscar por" en cada vínculo *ActionLink*. Hello código siguiente muestra hello completado `<ul class="nav navbar-nav">` etiqueta del archivo de diseño móviles Hola.

    <ul class="nav navbar-nav">
        <li>@Html.ActionLink("Home", "Index", "Home")</li>
        <li>@Html.ActionLink("Date", "AllDates", "Home")</li>
        <li>@Html.ActionLink("Speaker", "AllSpeakers", "Home")</li>
        <li>@Html.ActionLink("Tag", "AllTags", "Home")</li>
    </ul>

Hola copia *vistas\\inicio\\AllTags.cshtml* del archivo a *vistas\\inicio\\AllTags.Mobile.cshtml*. Abra el archivo nuevo de hello y cambie el `<h2>` elemento de "Etiquetas" demasiado "etiquetas (M)":

    <h2>Tags (M)</h2>

Examinar toohello etiquetas página utilizando un explorador de escritorio y el emulador de explorador móvil. emulador de explorador móvil Hello muestra hello dos cambios realizados (Hola título de  *\_Layout.Mobile.cshtml* y el título de Hola de *AllTags.Mobile.cshtml*).

![][AllTagsMobile_LayoutMobile]

En cambio, no ha cambiado la visualización de escritorio de hello (con títulos de  *\_Layout.cshtml* y *AllTags.cshtml*).

![][AllTagsMobile_LayoutMobileDesktop]

## <a name="bkmk_browserviews"></a> Creación de vistas específicas de explorador
Además vistas específicas de escritorio y toomobile, puede crear vistas para un explorador individual. Por ejemplo, puede crear vistas que son específicos para iPhone de Hola o explorador Android Hola. En esta sección, creará un diseño para una versión de iPhone de Hola y de explorador de iPhone de hello *AllTags* vista.

Abra hello *Global.asax* de archivos y agregar Hola después de la parte inferior de toohello de código de la `Application_Start` método.

    DisplayModeProvider.Instance.Modes.Insert(0, new DefaultDisplayMode("iPhone")
    {
        ContextCondition = (context => context.GetOverriddenUserAgent().IndexOf
            ("iPhone", StringComparison.OrdinalIgnoreCase) >= 0)
    });

Este código define un nuevo modo de visualización llamado "iPhone" que se comparará con cada solicitud entrante. Si la solicitud entrante de hello coincide con la condición definida (es decir, si el agente de usuario de hello contiene la cadena hello "iPhone"), ASP.NET MVC buscará vistas cuyo nombre contiene el sufijo "iPhone".

> [!NOTE]
> Al agregar específicas del explorador móvil modos de presentación, como para iPhone y Android, ser seguro tooset Hola primeros argumentos demasiado`0` (inserción en la parte superior de Hola de lista de Hola) toomake seguro de que el modo de explorador específico hello tiene prioridad sobre la plantilla móvil Hola (*. Mobile.cshtml). Si Hola móviles plantilla princip Hola de lista de hello en su lugar, se seleccionará en el modo de presentación deseado (Hola wins primera coincidencia y plantilla móvil Hola coincide con todos los exploradores móviles). 
> 
> 

En el código de hello, haga clic en `DefaultDisplayMode`, elija **resolver**y, a continuación, elija `using System.Web.WebPages;`. Esto agrega una referencia toothe `System.Web.WebPages` espacio de nombres, que es donde el `DisplayModeProvider` y `DefaultDisplayMode` se definen los tipos.

![][ResolveDefaultDisplayMode]

Como alternativa, puede agregar simplemente manualmente Hola después línea toothe `using` sección del archivo de Hola.

    using System.Web.WebPages;

Guarde los cambios de Hola. Copie el archivo *Views\\Shared\\\_Layout.Mobile.cshtml* a *Views\\Shared\\\_Layout.iPhone.cshtml*. Abra Hola nuevo archivo y, a continuación, Cambiar título Hola de `MVC5 Application (Mobile)` a `MVC5 Application (iPhone)`.

Hola copia *vistas\\inicio\\AllTags.Mobile.cshtml* del archivo a *vistas\\inicio\\AllTags.iPhone.cshtml*. En el nuevo archivo hello, cambie hello `<h2>` elemento de "etiquetas (M)" demasiadas "etiquetas (iPhone)".

Ejecute la aplicación hello. Ejecutar un emulador de explorador móvil, asegúrese de que el agente de usuario se establece demasiado "iPhone" y examinar toohello *AllTags* vista. Si usas emulador hello en herramientas de desarrollo F12 de Internet Explorer 11, configure siguiente de toohello de emulación:

* Perfil de explorador = **Windows Phone**
* Cadena de agente de usuario = **Custom**
* Cadena personalizada = **Apple-iPhone5C1/1001.525**

captura de pantalla siguiente Hello muestra hello *AllTags* vista representada en el emulador en herramientas de desarrollo F12 de Internet Explorer 11 con la cadena de agente de usuario personalizado de hello (Esto es una cadena de agente de usuario de iPhone 5 C).

![][AllTagsIPhone_LayoutIPhone]

En el explorador móvil de hello, seleccione hello **altavoces** vínculo. Porque no hay una vista móvil (*AllSpeakers.Mobile.cshtml*), ver los altavoces de hello predeterminado (*AllSpeakers.cshtml*) se representa mediante la vista de diseño de móviles hello ( *\_ Layout.Mobile.cshtml*). Tal y como se muestra a continuación, el título de hello **MVC5 aplicación (móvil)** se define en  *\_Layout.Mobile.cshtml*.

![][AllSpeakers_LayoutMobile]

Global puede deshabilitar una vista de (no son móviles) predeterminado de representación dentro de un diseño móvil estableciendo `RequireConsistentDisplayMode` a `true` en hello *vistas\\\_ViewStart.cshtml* archivo, similar al siguiente:

    @{
        Layout = "~/Views/Shared/_Layout.cshtml";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = true;
    }

Cuando `RequireConsistentDisplayMode` se establece demasiado`true`, diseño móviles hello (*\_Layout.Mobile.cshtml*) se utiliza únicamente para las vistas móviles (es decir, cuando es el archivo de vista de formulario de hello  ***ViewName** . Mobile.cshtml*). Es recomendable tooset `RequireConsistentDisplayMode` demasiado`true` si su diseño móvil no funciona bien con las vistas no son móviles. Hello captura de pantalla siguiente muestra cómo Hola *altavoces* la página presenta cuando `RequireConsistentDisplayMode` se establece demasiado`true` (sin cadena de hello "(móvil)" en la navegación de la barra en la parte superior de Hola Hola).

![][AllSpeakers_LayoutMobileOverridden]

Puede deshabilitar el modo de presentación coherente en una vista específica estableciendo `RequireConsistentDisplayMode` demasiado`false` en archivo de vista de Hola. El siguiente marcado en hello *vistas\\inicio\\AllSpeakers.cshtml* archivo establece `RequireConsistentDisplayMode` demasiado`false`:

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All speakers";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = false;
    }

En esta sección que hemos visto cómo toocreate móviles diseños, vistas y cómo toocreate diseños y las vistas para dispositivos específicos como Hola iPhone.
Sin embargo, Hola principal ventaja del marco de trabajo de Bootstrap CSS hello es el diseño dinámico, lo que significa que una sola hoja de estilos puede aplicarse a través de escritorio y teléfono, tableta exploradores toocreate una apariencia coherente. En la sección siguiente Hola verá cómo tooleverage arrancar toocreate preparadas para dispositivos móviles vistas.

## <a name="bkmk_Improvespeakerslist"></a>Mejorar Hola altavoces lista
Como ha visto, Hola *altavoces* vista es legible, pero Hola vínculos son pequeños y son difíciles de tootap en un dispositivo móvil. En esta sección, hará hello *AllSpeakers* preparadas para dispositivos móviles, la vista que muestra vínculos grandes y fácil de tap y contiene un tooquickly del cuadro de búsqueda encontró altavoces.

Puede usar hello Bootstrap [grupo de la lista vinculada] [ linked list group] estilos para mejorar hello *altavoces* vista. En *vistas\\inicio\\AllSpeakers.cshtml*, reemplace el contenido de hello del archivo de Razor Hola con código de hello siguiente.

     @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, "SessionsBySpeaker", new { speaker }, new { @class = "list-group-item" })
        }
    </div>

Hola `class="list-group"` atributo Hola `<div>` etiqueta aplica el estilo de lista de arranque, hello y `class="input-group-item"` vínculo de tooeach de estilo de elementos de lista de arranque aplica el atributo.

Actualice el explorador móvil Hola. Hola actualiza vista es similar al siguiente:

![][AllSpeakersFixed]

Hola Bootstrap [grupo de la lista vinculada] [ linked list group] estilo hace Hola un cuadro completo para cada vínculo interactivo, que es una experiencia de usuario mucho mejor. Cambiar la vista de escritorio toothe y observe la apariencia y funcionamiento coherente Hola.

![][AllSpeakersFixedDesktop]

Aunque se mejoró la vista de explorador móvil hello, es difícil la navegación lista larga de Hola de altavoces. Bootstrap no proporciona una funcionalidad de filtro de búsqueda de forma predeterminada, pero puede agregarla con unas pocas líneas de código. En primer lugar se agregará una vista de toohello del cuadro de búsqueda, a continuación, enlazar con el código de JavaScript para la función de filtro de Hola Hola. En *vistas\\inicio\\AllSpeakers.cshtml*, agregue un \<formulario\> etiqueta justo después de hello \<h2\> etiqueta, tal y como se muestra a continuación:

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <form class="input-group">
        <span class="input-group-addon"><span class="glyphicon glyphicon-search"></span></span>
        <input type="text" class="form-control" placeholder="Search speaker">
    </form>
    <br />
    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class = "list-group-item" })
        }
    </div>

Tenga en cuenta que hello `<form>` y `<input>` etiquetas ambos tienen Hola arranque estilos aplicados toothem. Hola `<span>` elemento agrega un arranque [glyphicon] [ glyphicon] toothe cuadro de búsqueda.

Hola *Scripts* carpeta, agregue un archivo JavaScript denominado *filter.js*. Abra el archivo hello y pegue Hola siguiente código en él:

    $(function () {

        // reset hello search form when hello page loads
        $("form").each(function () {
            this.reset();
        });

        // wire up hello events toohello <input> element for search/filter
        $("input").bind("keyup change", function () {
            var searchtxt = this.value.toLowerCase();
            var items = $(".list-group-item");

            // show all speakers that begin with hello typed text and hide others
            for (var i = 0; i < items.length; i++) {
                var val = items[i].text.toLowerCase();
                val = val.substring(0, searchtxt.length);
                if (val == searchtxt) {
                    $(items[i]).show();
                }
                else {
                    $(items[i]).hide();
                }
            }
        });
    });

También necesita tooinclude filter.js en sus agrupaciones registradas. Abra *aplicación\_iniciar\\BundleConfig.cs* y cambiar paquetes primera Hola. Cambiar la primera `bundles.Add` instrucción (para hello **jquery** agrupación) tooinclude *Scripts\\filter.js*, como se indica a continuación:

     bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                "~/Scripts/jquery-{version}.js",
                "~/Scripts/filter.js"));

Hola **jquery** agrupación ya se representa de forma predeterminada de hello  *\_diseño* vista. Más adelante, puede utilizar Hola JavaScript mismo código tooapply las vistas de lista de tooother de funcionalidad de filtro.

Actualice el explorador móvil hello y vaya toohello *AllSpeakers* vista. En el cuadro de búsqueda, escriba "sc". Ahora se debe filtrar lista de altavoces Hola según la cadena de búsqueda de tooyour.

![][AllSpeakersFixedSearchBySC]

## <a name="bkmk_improvetags"></a>Mejorar Hola lista etiquetas
Al igual que hello *altavoces* ver, hello *etiquetas* vista es legible, pero los vínculos de hello son pequeño y difícil de tootap en un dispositivo móvil. Puede corregir hello *etiquetas* vista Hola igual manera de corregir hello *altavoces* ver, si utiliza los cambios de código de hello descritos anteriormente, pero con la siguiente hello `Html.ActionLink` sintaxis de método en  *Vistas\\inicio\\AllTags.cshtml*:

    @Html.ActionLink(tag, 
                     "SessionsByTag", 
                     new { tag }, 
                     new { @class = "list-group-item" })

Hola actualiza Explorador de escritorio aparece como se indica a continuación:

![][AllTagsFixedDesktop]

Y Hola actualiza explorador móvil aparece como sigue: 

![][AllTagsFixed]

> [!NOTE]
> Si observa ese formato de la lista original de hello sigue estando allí en Hola explorador móvil y se pregunte qué aplicación de estilos de arranque "nice" de tooyour problema, se trata de un artefacto de las anterior acción toocreate móviles vistas específicas. Sin embargo, ahora que utilizas Hola Bootstrap CSS framework toocreate un diseño web con capacidad de respuesta, avanzar y quitar estas vistas específicas de mobile y vistas de diseño específicos de mobile Hola. Una vez que lo ha hecho, explorador móvil actualizado de hello mostrará un estilo de arranque de Hola.
> 
> 

## <a name="bkmk_improvedates"></a>Mejorar Hola lista de fechas
Puede mejorar hello *fechas* ver como mejorado hello *altavoces* y *etiquetas* vistas si usas Hola cambios en el código se describe anteriormente, pero con hello después `Html.ActionLink` sintaxis de método en *vistas\\inicio\\AllDates.cshtml*:

    @Html.ActionLink(date.ToString("ddd, MMM dd, h:mm tt"), 
                     "SessionsByDate", 
                     new { date }, 
                     new { @class = "list-group-item" })

Obtendrá una vista de explorador móvil actualizada con el aspecto siguiente:

![][AllDatesFixed]

Puede mejorar aún más hello *fechas* vista de organizar los valores de fecha y hora de Hola por fecha. Esto puede hacerse con hello Bootstrap [paneles] [ panels] aplicación de estilos. Reemplazar contenido Hola de hello *vistas\\inicio\\AllDates.cshtml* archivo con el código siguiente:

    @model IEnumerable<DateTime>

    @{
        ViewBag.Title = "All Dates";
    }

    <h2>Dates</h2>

    @foreach (var dategroup in Model.GroupBy(x=>x.Date))
    {
        <div class="panel panel-primary">
            <div class="panel-heading">
                @dategroup.Key.ToString("ddd, MMM dd")
            </div>
            <div class="panel-body list-group">
                @foreach (var date in dategroup)
                {
                    @Html.ActionLink(date.ToString("h:mm tt"), 
                                     "SessionsByDate", 
                                     new { date }, 
                                     new { @class = "list-group-item" })
                }
            </div>
        </div>
    }

Este código crea otro `<div class="panel panel-primary">` etiqueta para cada fecha en la lista de Hola y Hola usa distinto [grupo de la lista vinculada] [ linked list group] para los respectivos vincula como antes. Este es el explorador móvil Hola aspecto cuando se ejecuta este código:

![][AllDatesFixed2]

Explorador de escritorio toohello de conmutador. De nuevo, tenga en cuenta Hola apariencia coherente.

![][AllDatesFixed2Desktop]

## <a name="bkmk_improvesessionstable"></a>Mejorar hello SessionsTable vista
En esta sección, hará hello *SessionsTable* ver más preparado para dispositivos móviles. Este cambio es más amplias cambios anteriores de Hola.

En el explorador móvil de hello, puntee en hello **etiqueta** , a continuación, escriba `asp` en el cuadro de búsqueda.

![][AllTagsFixedSearchByASP]

Pulse hello **ASP.NET** vínculo.

![][SessionsTableTagASP.NET]

Como puede ver, mostrar hello se formatea como una tabla, que está diseñado actualmente toobe ver en el Explorador de escritorio de Hola. Sin embargo, es un poco difícil tooread en un explorador móvil. toofix, abra *vistas\\inicio\\SessionsTable.cshtml* y, a continuación, reemplace el contenido de hello del archivo con el siguiente código de hello:

    @model IEnumerable<Mvc5Mobile.Models.Session>

    <h2>@ViewBag.Title</h2>

    <div class="container">
        <div class="row">
            @foreach (var session in Model)
            {
                <div class="col-md-4">
                    <div class="list-group">
                        @Html.ActionLink(session.Title, 
                                         "SessionByCode", 
                                         new { session.Code }, 
                                         new { @class="list-group-item active" })
                        <div class="list-group-item">
                            <div class="list-group-item-text">
                                @Html.Partial("_SpeakersLinks", session)
                            </div>
                            <div class="list-group-item-info">
                                @session.DateText
                            </div>
                            <div class="list-group-item-info small hidden-xs">
                                @Html.Partial("_TagsLinks", session)
                            </div>
                        </div>
                    </div>
                </div>
            }
        </div>
    </div>

código de Hello hace 3 cosas:

* usa Hola Bootstrap [grupo personalizado de lista vinculada] [ custom linked list group] tooformat Hola verticalmente, información de la sesión para que toda esta información es legible en un explorador móvil (mediante clases como lista grupo-elemento de texto)
* se aplica hello [sistema cuadrícula] [ grid system] toothe diseño, por lo que esa sesión Hola elementos de flujo horizontal en el Explorador de escritorio de Hola y verticalmente en explorador móvil hello (mediante la clase de hello col-md-4)
* hello usa [utilidades respondiendo] [ responsive utilities] para ocultar las etiquetas de sesión de hello cuando se ve en el explorador móvil hello (mediante la clase de hello extra oculto)

También puede puntear en una sesión título vínculo toogo toohello respectivos. imagen de Hello siguiente refleja los cambios de código de hello.

![][FixedSessionsByTag]

sistema de arranque cuadrícula Hola que aplican automáticamente Organiza las sesiones verticalmente en explorador móvil Hola. Además, tenga en cuenta que no se muestran las etiquetas de Hola. Explorador de escritorio toohello de conmutador.

![][SessionsTableFixedTagASP.NETDesktop]

En el Explorador de escritorio de hello, tenga en cuenta que ahora se muestran las etiquetas de Hola. Además, puede ver que sistema de arranque cuadrícula Hola aplicados organiza los elementos de la sesión de hello en dos columnas. Si amplía el explorador, verá que los cambios de organización de hello toothree columnas.

## <a name="bkmk_improvesessionbycode"></a>Mejorar hello SessionByCode vista
Por último, va a corregir hello *SessionByCode* ver toomake, preparadas para dispositivos móviles.

En el explorador móvil de hello, puntee en hello **etiqueta** , a continuación, escriba `asp` en el cuadro de búsqueda.

![][AllTagsFixedSearchByASP]

Pulse hello **ASP.NET** vínculo. Se mostrarán las sesiones de etiqueta ASP.NET de Hola.

![][FixedSessionsByTag]

Elija hello **crear una aplicación de página única con ASP.NET y AngularJS** vínculo.

![][SessionByCode3-644]

vista de escritorio de Hello predeterminada es correcto, pero puede mejorar el aspecto de hello fácilmente mediante el uso de algunos componentes de GUI de arranque.

Abra *vistas\\inicio\\SessionByCode.cshtml* y reemplace el contenido de hello con hello sigue marcado:

    @model Mvc5Mobile.Models.Session

    @{
        ViewBag.Title = "Session details";
    }
    <h3>@Model.Title (@Model.Code)</h3>
    <p>
        <strong>@Model.DateText</strong> in <strong>@Model.Room</strong>
    </p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Speakers
        </div>
        @foreach (var speaker in Model.Speakers)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class="panel-body" })
        }
    </div>

    <p>@Model.Abstract</p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Tags
        </div>
        @foreach (var tag in Model.Tags)
        {
            @Html.ActionLink(tag, 
                             "SessionsByTag", 
                             new { tag }, 
                             new { @class = "panel-body" })
        }
    </div>

nueva marca de Hello usa arranque paneles vista móvil de tooimprove Hola de aplicación de estilos. 

Actualice el explorador móvil Hola. Hello imagen siguiente refleja los cambios de código de hello que acaba de crear:

![][SessionByCodeFixed3-644]

## <a name="wrap-up-and-review"></a>Resumen y revisión
Este tutorial le ha mostrado cómo las aplicaciones Web de ASP.NET MVC 5 toodevelop preparadas para dispositivos móviles toouse. Entre ellos se incluyen los siguientes:

* Implementar un tooan de aplicación de ASP.NET MVC 5 aplicación de servicio de aplicaciones web
* Usar el diseño de capacidad de respuesta web de arranque toocreate en la aplicación de MVC 5
* Invalidación del diseño, las vistas y las vistas parciales, tanto de manera global como para una vista individual
* Control del diseño y aplicación de la invalidación parcial mediante la propiedad `RequireConsistentDisplayMode`
* Crear vistas que tienen como destino exploradores específicos, como el Explorador de iPhone Hola
* Aplicación del estilo de Bootstrap en el código de Razor

## <a name="see-also"></a>Otras referencias
* [Nueve principios básicos del diseño web con respuesta](http://blog.froont.com/9-basic-principles-of-responsive-web-design/)
* [Bootstrap][BootstrapSite]
* [Blog oficial de Bootstrap][Official Bootstrap Blog]
* [Tutorial de Twitter Bootstrap de Tutorial Republic][Twitter Bootstrap Tutorial from Tutorial Republic]
* [Hola Bootstrap Playground][hello Bootstrap Playground]
* [Prácticas recomendadas y recomendaciones de W3C para aplicaciones web móviles][W3C Recommendation Mobile Web Application Best Practices]
* [Recomendación de candidatos de W3C para consultas multimedia][W3C Candidate Recommendation for media queries]

## <a name="whats-changed"></a>Lo que ha cambiado
* Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- Internal Links -->
[Deploy hello starter project tooan Azure web app]: #bkmk_DeployStarterProject
[Bootstrap CSS Framework]: #bkmk_bootstrap
[Override hello Views, Layouts, and Partial Views]: #bkmk_overrideviews
[Create Browser-Specific Views]:#bkmk_browserviews
[Improve hello Speakers List]: #bkmk_Improvespeakerslist
[Improve hello Tags List]: #bkmk_improvetags
[Improve hello Dates List]: #bkmk_improvedates
[Improve hello SessionsTable View]: #bkmk_improvesessionstable
[Improve hello SessionByCode View]: #bkmk_improvesessionbycode

<!-- External Links -->
[Visual Studio Express 2013]: http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-web
[Visual Studio 2015]: https://www.visualstudio.com/downloads/download-visual-studio-vs
[AzureSDKVs2013]: http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409
[Fiddler]: http://www.fiddler2.com/fiddler2/
[EmulatorIE11]: http://msdn.microsoft.com/library/ie/dn255001.aspx
[EmulatorChrome]: https://developers.google.com/chrome-developer-tools/docs/mobile-emulation
[EmulatorOpera]: http://www.opera.com/developer/tools/mobile/
[StarterProject]: http://go.microsoft.com/fwlink/?LinkID=398780&clcid=0x409
[CompletedProject]: http://go.microsoft.com/fwlink/?LinkID=398781&clcid=0x409
[BootstrapSite]: http://getbootstrap.com/
[WebPIAzureSdk23NetVS13]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/WebPIAzureSdk23NetVS13.png
[linked list group]: http://getbootstrap.com/components/#list-group-linked
[glyphicon]: http://getbootstrap.com/components/#glyphicons
[panels]: http://getbootstrap.com/components/#panels
[custom linked list group]: http://getbootstrap.com/components/#list-group-custom-content
[grid system]: http://getbootstrap.com/css/#grid
[responsive utilities]: http://getbootstrap.com/css/#responsive-utilities
[Official Bootstrap Blog]: http://blog.getbootstrap.com/
[Twitter Bootstrap Tutorial from Tutorial Republic]: http://www.tutorialrepublic.com/twitter-bootstrap-tutorial/
[hello Bootstrap Playground]: http://www.bootply.com/
[W3C Recommendation Mobile Web Application Best Practices]: http://www.w3.org/TR/mwabp/
[W3C Candidate Recommendation for media queries]: http://www.w3.org/TR/css3-mediaqueries/

<!-- Images -->
[DeployClickPublish]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-1.png
[DeployClickWebSites]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-2.png
[DeploySignIn]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-3.png
[DeployUsername]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-4.png
[DeployPassword]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-5.png
[DeployNewWebsite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-6.png
[DeploySiteSettings]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7.png
[DeployPublishSite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-8.png
[MobileHomePage]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/mobile-home-page.png
[FixedSessionsByTag]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-Fixed.png
[AllTags]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags.png
[SessionsByTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET.png
[SessionsByTagASP.NETNoBootstrap]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-NoBootstrap.png
[AllTagsMobile_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile.png
[AllTagsMobile_LayoutMobileDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile-Desktop.png
[ResolveDefaultDisplayMode]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/Resolve-DefaultDisplayMode.png
[AllTagsIPhone_LayoutIPhone]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsIPhone-_LayoutIPhone.png
[AllSpeakers_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile.png
[AllSpeakers_LayoutMobileOverridden]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile-Overridden.png
[AllSpeakersFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed.png
[AllSpeakersFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-Desktop.png
[AllSpeakersFixedSearchBySC]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-SearchBySC.png
[AllTagsFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-Desktop.png 
[AllTagsFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed.png
[AllDatesFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed.png
[AllDatesFixed2]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2.png
[AllDatesFixed2Desktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2-Desktop.png
[AllTagsFixedSearchByASP]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-SearchByASP.png
[SessionsTableTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Tag-ASP.NET.png
[SessionsTableFixedTagASP.NETDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Fixed-Tag-ASP.NET-Desktop.png
[SessionByCode3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-3-644.png
[SessionByCodeFixed3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-Fixed-3-644.png

