---
title: "aaaCreate una aplicación de Azure de línea de negocio con la autenticación de Active Directory de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate un ASP.NET MVC de línea de negocio de aplicación de servicio de aplicaciones de Azure que autentica con Azure Active Directory"
services: app-service\web, active-directory
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: ad947bdb-4463-43ff-a5e3-91d9b2169b60
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 09/01/2016
ms.author: cephalin
ms.openlocfilehash: 3bcafad78ac0151889b3e336784cc561009f244f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-azure-active-directory-authentication"></a>Creación de una aplicación de línea de negocio de Azure con autenticación de Azure Active Directory
Este artículo muestra cómo toocreate un .NET de línea de negocio de aplicación en [aplicaciones de Web del servicio de aplicación de Azure](http://go.microsoft.com/fwlink/?LinkId=529714) con hello [autenticación / autorización](../app-service/app-service-authentication-overview.md) característica. También muestra cómo hello toouse [API Graph de Azure Active Directory](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) tooquery datos de directorio de aplicación hello.

inquilino de Azure Active Directory de Hola que usa puede ser un directorio de solo Azure. O bien, puede ser [sincronizado con su Active Directory local](../active-directory/active-directory-aadconnect.md) toocreate una experiencia de inicio de sesión única para los trabajadores que son locales y remotos. En este artículo usa el directorio predeterminado de Hola para su cuenta de Azure.

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a>Lo que va a crear
Va a compilar una aplicación sencilla de crear-lectura-actualización y eliminación (CRUD) de línea de negocio en aplicaciones Web de servicio de aplicación que realiza un seguimiento de elementos de trabajo con hello siguientes características:

* Autentica los usuarios contra Azure Active Directory
* Consulta los usuarios y grupos del directorio con la [API Graph de Azure Active Directory](http://msdn.microsoft.com/library/azure/hh974476.aspx)
* Use Hola ASP.NET MVC *sin autenticación* plantilla

Si necesita control de acceso basado en roles (RBAC) para la aplicación de línea de negocio en Azure, consulte el [siguiente paso](#next).

<a name="bkmk_need"></a>

## <a name="what-you-need"></a>Lo que necesita
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

Necesita Hola siguientes toocomplete este tutorial:

* Un inquilino de Azure Active Directory con usuarios en varios grupos
* Aplicaciones de toocreate de permisos en el inquilino de Azure Active Directory Hola
* Visual Studio 2013, actualización 4 o posterior
* [SDK de Azure 2.8.1 o posterior](https://azure.microsoft.com/downloads/)

<a name="bkmk_deploy"></a>

## <a name="create-and-deploy-a-web-app-tooazure"></a>Crear e implementar un tooAzure de aplicación web
1. En Visual Studio, haga clic en **Archivo** > **Nuevo** > **Proyecto**.
2. Seleccione **Aplicación web ASP.NET**, elija el nombre del proyecto y haga clic en **Aceptar**.
3. Seleccione hello **MVC** plantilla, a continuación, cambie la autenticación Hola demasiado**sin autenticación**. Asegúrese de que **Host Hola nube** está seleccionada y haga clic en **Aceptar**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/1-create-mvc-no-authentication.png)
4. Hola **crear servicio en la aplicación** cuadro de diálogo, haga clic en **agregar una cuenta** (y, a continuación, **agregar una cuenta** en la lista desplegable de hello) toolog en tooyour cuenta de Azure.
5. Después de iniciar sesión, configure la aplicación web. Cree un grupo de recursos y un nuevo plan de servicio de aplicaciones haciendo clic en hello respectivo **New** botón. Haga clic en **explorar servicios adicionales de Azure** toocontinue.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/2-create-app-service.png)
6. Hola **servicios** , haga clic en  **+**  tooadd una base de datos de SQL para la aplicación. 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/3-add-sql-database.png)
7. En **Configurar base de datos de SQL**, haga clic en **New** toocreate una instancia de SQL Server.
8. En **Configurar SQL Server**, configure la instancia de SQL Server. A continuación, haga clic en **Aceptar**, **Aceptar**, y **crear** tookick desactivar la creación de la aplicación de hello en Azure.
9. En **actividad de servicio de aplicación de Azure**, puede ver cuando finalice la creación de aplicación Hola. Haga clic en  **publicar &lt;* appname*> toothis aplicación Web ahora **, a continuación, haga clic en **publicar**. 
   
    Una vez finalizada de Visual Studio, abre Hola publicar la aplicación en el Explorador de Hola. 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/4-published-shown-in-browser.png)

<a name="bkmk_auth"></a>

## <a name="configure-authentication-and-directory-access"></a>Configuración de la autenticación y el acceso al directorio
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Hola menú izquierdo, haga clic en **servicios de aplicaciones** > **&lt;*appname*> ** > **autenticación / autorización**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/5-app-service-authentication.png)
3. Active la autenticación de Azure Active Directory con un clic en **Activada** > **Azure Active Directory** > **Rápido** > **Aceptar**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/6-authentication-express.png)
4. Haga clic en **guardar** en la barra de comandos de Hola.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/7-authentication-save.png)
   
    Una vez que se guardó correctamente la configuración de autenticación de hello, pruebe a navegar por la aplicación de tooyour nuevo en el Explorador de Hola. La configuración predeterminada exigen la autenticación en la aplicación completa de hello. Si ya no inició sesión, es redirigido tooa pantalla de inicio de sesión. Una vez iniciada la sesión, verá la aplicación protegida por HTTPS. A continuación, debe acceder a los tooenable toodirectory datos. 
5. Navegue toohello [portal clásico](https://manage.windowsazure.com).
6. Hola menú izquierdo, haga clic en **Active Directory** > **directorio predeterminado** > **aplicaciones**  >   **&lt;* appname*> **.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/8-find-aad-application.png)
   
    Se trata de aplicaciones de Azure Active Directory de Hola que creó el servicio de aplicación para tooenable Hola autorización o característica de autenticación.
7. Haga clic en **usuarios** y **grupos** toomake seguro de que tiene algunos usuarios y grupos en el directorio de Hola. Si no es así, cree grupos y usuarios de prueba.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/9-create-users-groups.png)
8. Haga clic en **configurar** tooconfigure esta aplicación.
9. Desplácese hacia abajo toohello **claves** sección y agregar una clave, seleccione una duración. A continuación, haga clic en **Permisos delegados** y seleccione **Leer datos de directorio**. 
   Haga clic en **Guardar**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/10-configure-aad-application.png)
10. Una vez que se guarda la configuración, se desplaza hacia arriba toohello **claves** sección y haga clic en hello **copia** clave de cliente de botón toocopy Hola. 
    
     ![](./media/web-sites-dotnet-lob-application-azure-ad/11-get-app-key.png)
    
    > [!IMPORTANT]
    > Si sale ahora esta página, no será capaz de tooaccess este cliente clave nunca más.
    > 
    > 
11. A continuación, debe tooconfigure su aplicación web con esta clave. Inicie sesión en toohello [Explorador de recursos de Azure](https://resources.azure.com) con su cuenta de Azure.
12. En la parte superior de Hola de página de hello, haga clic en **lectura/escritura** toomake cambios en hello Explorador de recursos de Azure.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/12-resource-manager-writable.png)
13. Buscar valores de autenticación para la aplicación, que se encuentra en las suscripciones de hello >  **&lt;* subscriptionname*> ** > **resourceGroups**  >   **&lt;* resourcegroupname*> ** > **proveedores** > **Microsoft.Web**  >  **sitios** > **&lt;*appname*> ** > **config**  >  **authsettings**.
14. Haga clic en **Editar**.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/13-edit-authsettings.png)
15. Hola panel de edición, establezca hello `clientSecret` y `additionalLoginParams` propiedades como se indica a continuación.
    
        ...
        "clientSecret": "<client key from hello Azure Active Directory application>",
        ...
        "additionalLoginParams": ["response_type=code id_token", "resource=https://graph.windows.net"],
        ...
16. Haga clic en **colocar** en Hola superior toosubmit los cambios.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/14-edit-parameters.png)
17. Ahora, tootest si tienen autorización Hola token tooaccess Hola API Graph de Azure Active Directory, simplemente vaya a  **https://&lt;*appname*>.azurewebsites.net/.auth/me** en el Explorador. Si ha configurado todo correctamente, debería ver Hola `access_token` propiedad Hola respuesta JSON.
    
    Hola `~/.auth/me` ruta de acceso de dirección URL se administra mediante la autenticación de servicio de aplicación / toogive de autorización toda la información de Hola relacionados con la sesión tooyour autenticado. Para obtener más información, consulte [Autenticación y autorización en el Servicio de aplicaciones de Azure](../app-service/app-service-authentication-overview.md).
    
    > [!NOTE]
    > Hola `access_token` tiene un período de caducidad. Sin embargo, la autorización y autenticación de App Service proporciona una funcionalidad de actualización del token con `~/.auth/refresh`. Para obtener más información acerca de cómo toouse, consulte [tienda de símbolo (token) de servicio de aplicaciones](https://cgillum.tech/2016/03/07/app-service-token-store/).
    > 
    > 

A continuación, hará algo útil con los datos del directorio.

<a name="bkmk_crud"></a>

## <a name="add-line-of-business-functionality-tooyour-app"></a>Agregar funcionalidad de línea de negocio tooyour aplicación
Ahora, cree un rastreador de elementos de trabajo CRUD sencillo.  

1. En la carpeta de ~\Models hello, cree un archivo de clase denominado WorkItem.cs y reemplace `public class WorkItem {...}` con hello siguiente código:
   
     using System.ComponentModel.DataAnnotations;
   
     public class WorkItem   {
   
         [Key]
         public int ItemID { get; set; }
         public string AssignedToID { get; set; }
         public string AssignedToName { get; set; }
         public string Description { get; set; }
         public WorkItemStatus Status { get; set; }
     }
   
     public enum WorkItemStatus   {
   
         Open,
         Investigating,
         Resolved,
         Closed
     }
2. Crear Hola proyecto toomake su nueva lógica de scaffolding de toohello accesible de modelo en Visual Studio.
3. Agregar un nuevo elemento con scaffolding `WorkItemsController` toohello ~\Controllers carpeta (haga clic en **controladores**, seleccione demasiado**agregar**y seleccione **nuevo elemento con scaffolding**). 
4. Seleccione **Controlador MVC 5 con vistas, usando Entity Framework** y haga clic en **Agregar**.
5. A continuación, haga clic en el modelo Hola SELECT que ha creado,  **+**  y, a continuación, **agregar** tooadd un contexto de datos y, a continuación, haga clic en **agregar**.
   
   ![](./media/web-sites-dotnet-lob-application-azure-ad/16-add-scaffolded-controller.png)
6. En ~\Views\WorkItems\Create.cshtml (un elemento con scaffolding automáticamente), busque hello `Html.BeginForm` método auxiliar y asegúrese de hello siguiendo el resaltado cambios:  
   
   <pre class="prettyprint">
   @model WebApplication1.Models.WorkItem
   
   @{
    ViewBag.Title = &quot;Create&quot;;
   }
   
   &lt;h2&gt;Create&lt;/h2&gt;
   
   @using (Html.BeginForm(<mark>&quot;Create&quot;, &quot;WorkItems&quot;, FormMethod.Post, new { id = &quot;main-form&quot; }</mark>)) 
   {
    @Html.AntiForgeryToken()
   
    &lt;div class=&quot;form-horizontal&quot;&gt;
        &lt;h4&gt;WorkItem&lt;/h4&gt;
        &lt;hr /&gt;
        @Html.ValidationSummary(true, &quot;&quot;, new { @class = &quot;text-danger&quot; })
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToID, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToID, new { htmlAttributes = new { @class = &quot;form-control&quot;<mark>, @type = &quot;hidden&quot;</mark> } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToID, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToName, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToName, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToName, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Description, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.Description, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.Description, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EnumDropDownListFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;form-control&quot; })
                @Html.ValidationMessageFor(model =&gt; model.Status, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            &lt;div class=&quot;col-md-offset-2 col-md-10&quot;&gt;
                &lt;input type=&quot;submit&quot; value=&quot;Create&quot; class=&quot;btn btn-default&quot;<mark> id=&quot;submit-button&quot;</mark> /&gt;
            &lt;/div&gt;
        &lt;/div&gt;
    &lt;/div&gt;
   }
   
   &lt;div&gt;
    @Html.ActionLink(&quot;Back tooList&quot;, &quot;Index&quot;)
   &lt;/div&gt;
   
   @section Scripts {
    @Scripts.Render(&quot;~/bundles/jqueryval&quot;)
    <mark>&lt;script&gt;
        // People/Group Picker Code
        var maxResultsPerPage = 14;
        var input = document.getElementById(&quot;AssignedToName&quot;);
   
        // Access token from request header, and tenantID from claims identity
        var token = &quot;@Request.Headers[&quot;X-MS-TOKEN-AAD-ACCESS-TOKEN&quot;]&quot;;
        var tenant =&quot;@(System.Security.Claims.ClaimsPrincipal.Current.Claims
                        .Where(c => c.Type == &quot;http://schemas.microsoft.com/identity/claims/tenantid&quot;)
                        .Select(c => c.Value).SingleOrDefault())&quot;;
   
        var picker = new AadPicker(maxResultsPerPage, input, token, tenant);
   
        // Submit hello selected user/group toobe asssigned.
        $(&quot;#submit-button&quot;).click({ picker: picker }, function () {
            if (!picker.Selected())
                return;
            $(&quot;#main-form&quot;).get()[0].elements[&quot;AssignedToID&quot;].value = picker.Selected().objectId;
        });
    &lt;/script&gt;</mark>
   }
   </pre>
   
   Tenga en cuenta que `token` y `tenant` usan hello `AadPicker` toomake objeto llamadas de API Graph de Azure Active Directory. Agregará `AadPicker` más adelante.     
   
   > [!NOTE]
   > Igual de bien que puedas `token` y `tenant` del lado de cliente de hello con `~/.auth/me`, sino que sería una llamada adicional del servidor. Por ejemplo:
   > 
   > $.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });
   > 
   > 
7. Realizar Hola mismos cambios con ~ \Views\WorkItems\Edit.cshtml.
8. Hola `AadPicker` objeto se define en una secuencia de comandos que necesita tooadd tooyour proyecto. Haga clic en hello ~\Scripts carpeta, seleccione demasiado**agregar**y haga clic en **archivo JavaScript**. Tipo de `AadPickerLibrary` Hola filename y haga clic en **Aceptar**.
9. Copiar el contenido de Hola de [aquí](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) en ~ \Scripts\AadPickerLibrary.js.
   
   En el script de Hola, Hola `AadPicker` objeto llamadas [API Graph de Azure Active Directory](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) toosearch para usuarios y grupos que coinciden con la entrada de Hola.  
10. ~\Scripts\AadPickerLibrary.js también utiliza hello [jQuery UI Autocompletar widget](https://jqueryui.com/autocomplete/). Por lo que deberá proyecto tooyour de tooadd jQuery UI. Haga clic con el botón derecho en el proyecto y haga clic en **Administrar paquetes NuGet**.
11. En el Administrador de paquetes de NuGet hello, haga clic en Examinar, tipo **jquery ui** en Hola barra de búsqueda y haga clic en **jQuery.UI.Combined**.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/17-add-jquery-ui-nuget.png)
12. En el panel derecho de hello, haga clic en **instalar**, a continuación, haga clic en **Aceptar** tooproceed.
13. Abra ~\App_Start\BundleConfig.cs y realice Hola siguiendo el resaltado cambios:  
    
    <pre class="prettyprint">
    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle(&quot;~/bundles/jquery&quot;).Include(
                    &quot;~/Scripts/jquery-{version}.js&quot;<mark>,
                    &quot;~/Scripts/jquery-ui-{version}.js&quot;,
                    &quot;~/Scripts/AadPickerLibrary.js&quot;</mark>));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/jqueryval&quot;).Include(
                    &quot;~/Scripts/jquery.validate*&quot;));
    
        // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
        // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
        bundles.Add(new ScriptBundle(&quot;~/bundles/modernizr&quot;).Include(
                    &quot;~/Scripts/modernizr-*&quot;));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/bootstrap&quot;).Include(
                    &quot;~/Scripts/bootstrap.js&quot;,
                    &quot;~/Scripts/respond.js&quot;));
    
        bundles.Add(new StyleBundle(&quot;~/Content/css&quot;).Include(
                    &quot;~/Content/bootstrap.css&quot;,
                    &quot;~/Content/site.css&quot;<mark>,
                    &quot;~/Content/themes/base/jquery-ui.css&quot;</mark>));
    }
    </pre>
    
    Hay más rendimiento maneras toomanage JavaScript y archivos CSS en la aplicación. Sin embargo, para simplificar el trabajo solo va toopiggyback en las agrupaciones de Hola que se cargan con cada vista.
14. Por último, en ~ \Global.asax, agregar Hola después de la línea de código de hello `Application_Start()` método. `Ctrl`+`.`en cada error de resolución de nombres demasiado corregirlo.
    
        AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.NameIdentifier;
    
    > [!NOTE]
    > Necesita esta línea de código porque usa la plantilla MVC predeterminada hello <code>[ValidateAntiForgeryToken]</code> decoración en algunas de las acciones de Hola. Pagar comportamiento toohello descrito por [Allen Brock](https://twitter.com/BrockLAllen) en [MVC 4, AntiForgeryToken y notificaciones](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) su HTTP POST puede producir un error de validación del token antifalsificación porque:
    > 
    > * Azure Active Directory no envía http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider hello, y es necesario de forma predeterminada para el token antifalsificación de Hola.
    > * Si Azure Active Directory directory sincronizado con AD FS, confianza Hola AD FS de forma predeterminada no enviar hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider notificación, aunque puede configurar manualmente AD FS toosend Esta notificación.
    > 
    > `ClaimTypes.NameIdentifies`Especifica la notificación de hello `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, que proporciona Azure Active Directory.  
    > 
    > 
15. Ahora, publique los cambios. Haga clic con el botón derecho en el proyecto y haga clic en **Publicar**.
16. Haga clic en **configuración**, asegúrese de que hay un tooyour de cadena de conexión base de datos SQL, seleccione **Actualizar base de datos** toomake Hola cambios de esquema para el modelo y haga clic en **publicar** .
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/18-publish-crud-changes.png)
17. En el Explorador de hello, desplácese toohttps: / /&lt;*appname*>.azurewebsites.net/workitems y haga clic en **crear nuevo**.
18. Haga clic en hello **AssignedToName** cuadro. Ahora debería ver los usuarios y grupos desde el inquilino de Azure Active Directory en una lista desplegable. Puede escribir toofilter, o usar hello `Up` o `Down` clave o haga clic en tooselect Hola usuario o grupo. 
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/19-use-aadpicker.png)
19. Haga clic en **crear** cambios de hello toosave. A continuación, haga clic en **editar** en el trabajo de hello creado elemento tooobserve Hola mismo comportamiento.

Enhorabuena, está ejecutando una aplicación de línea de negocio en Azure con acceso al directorio. No hay mucho más que puede hacer con hello API Graph. Consulte [Azure AD Graph API reference](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog)(Referencias de la API Graph de Azure AD).

<a name="next"></a>

## <a name="next-step"></a>siguiente paso
Si tiene el control de acceso basado en roles (RBAC) para la aplicación de línea de negocio de azure, consulte [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) para obtener un ejemplo de equipo de Azure Active Directory Hola. Muestra cómo tooenable roles para la aplicación de Azure Active Directory y, a continuación, autorizar a los usuarios con hello `[Authorize]` decoración.

Si la aplicación de línea de negocio debe tener acceso a datos tooon locales, consulte [acceder a recursos usando conexiones híbridas en el servicio de aplicación de Azure local](web-sites-hybrid-connection-get-started.md).

<a name="bkmk_resources"></a>

## <a name="further-resources"></a>Recursos adicionales
* [Autenticación y autorización en el Servicio de aplicaciones de Azure](../app-service/app-service-authentication-overview.md)
* [Autenticación con Active Directory local en aplicaciones de Azure](web-sites-authentication-authorization.md)
* [Creación de una aplicación de línea de negocio en Azure con autenticación de AD FS](web-sites-dotnet-lob-application-adfs.md)
* [Hello Azure AD Graph API y autenticación de servicio de la aplicación](https://cgillum.tech/2016/03/25/app-service-auth-aad-graph-api/)
* [Ejemplos y documentación de Microsoft Azure Active Directory](https://github.com/AzureADSamples)
* [Tipos de notificaciones y tokens admitidos de Azure Active Directory](http://msdn.microsoft.com/library/azure/dn195587.aspx)
