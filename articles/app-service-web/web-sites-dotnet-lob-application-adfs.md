---
title: "una aplicación de Azure de línea de negocio con autenticación de AD FS aaaCreate | Documentos de Microsoft"
description: "Obtenga información acerca de cómo una aplicación de línea de negocio en el servicio de aplicaciones de Azure que se autentica con toocreate local a STS. Este tutorial dirige a AD FS como Hola a STS local."
services: app-service\web
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: 0fa9f7a1-37bd-4d11-845f-aeff6fc9e4ca
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 08/31/2016
ms.author: cephalin
ms.openlocfilehash: cfd6f14837642fbf58ca5da9dee72db69cd5ab7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-ad-fs-authentication"></a>Creación de una aplicación de Azure de línea de negocio con autenticación de AD FS
Este artículo muestra cómo toocreate un ASP.NET MVC de línea de negocio de aplicación en [servicio de aplicaciones de Azure](../app-service/app-service-value-prop-what-is.md) mediante una implementación local [los servicios de federación de Active Directory](http://technet.microsoft.com/library/hh831502.aspx) como proveedor de identidades de Hola. Este escenario puede trabajar cuando desea que las aplicaciones de línea de negocio de toocreate en el servicio de aplicación de Azure, pero su organización requiere toobe de datos de directorio almacenado en el sitio.

> [!NOTE]
> Para obtener información general de opciones de autenticación y autorización de empresa diferente de hello para el servicio de aplicaciones de Azure, consulte [autenticar con local de Active Directory en la aplicación de Azure](web-sites-authentication-authorization.md).
> 
> 

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a>Lo que va a crear
Va a compilar una aplicación ASP.NET básica en aplicaciones de Web del servicio de aplicación de Azure con hello siguientes características:

* Autentica a los usuarios con AD FS
* Usa `[Authorize]` tooauthorize a los usuarios para distintas acciones
* Configuración estática para depurar en Visual Studio y para publicar aplicaciones Web del servicio tooApp (configurar una sola vez, depurar y publicar en cualquier momento)  

<a name="bkmk_need"></a>

## <a name="what-you-need"></a>Lo que necesita
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

Necesita Hola siguientes toocomplete este tutorial:

* Una implementación local implementación de AD FS (para ver un tutorial to-end Hola del laboratorio de pruebas utilizado en este tutorial, vea [laboratorio de pruebas: STS independiente con AD FS en máquinas virtuales de Azure (para solo prueba)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))
* Usuario de confianza de permisos toocreate confía en administración de AD FS
* Visual Studio 2013, actualización 4 o posterior
* [SDK de Azure 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) o posterior.

<a name="bkmk_sample"></a>

## <a name="use-sample-application-for-line-of-business-template"></a>Usar la aplicación de ejemplo para la plantilla de línea de negocio
Hola la aplicación de ejemplo en este tutorial, [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), creado por el equipo de Azure Active Directory Hola. Dado que AD FS admite WS-Federation, puede usar como una aplicación de línea de negocio de plantilla toocreate con facilidad. Tiene Hola siguientes características:

* Usa [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) tooauthenticate con una implementación local implementación de AD FS
* Funcionalidad de inicio y de cierre de sesión
* Usa [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (en lugar de Windows Identity Foundation), que es Hola futuras de ASP.NET y mucho más fácil tooset hacia arriba para autenticación y autorización que WIF

<a name="bkmk_setup"></a>

## <a name="set-up-hello-sample-application"></a>Configurar la aplicación de ejemplo de Hola
1. Clonar o descargar la solución de ejemplo de Hola en [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) tooyour de directorio local.
   
   > [!NOTE]
   > Hola instrucciones de [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) mostrarle cómo tooset una aplicación hello con Azure Active Directory. Pero en este tutorial, se configura con AD FS, siga estos pasos de hello en su lugar.
   > 
   > 
2. Abrir solución hello y, a continuación, abra Controllers\AccountController.cs en hello **el Explorador de soluciones**.
   
   Verá que el código de hello simplemente emite un usuario de hello tooauthenticate de desafío de autenticación mediante WS-Federation. Toda la autenticación se configura en App_Start\Startup.Auth.cs.
3. Abra App_Start\Startup.Auth.cs. Hola  `ConfigureAuth` /método siguiente, tenga en cuenta Hola línea:
   
       app.UseWsFederationAuthentication(
           new WsFederationAuthenticationOptions
           {
               Wtrealm = realm,
               MetadataAddress = metadata                                      
           });
   
   Este fragmento de código de Hola a todos OWIN, es en realidad Hola reconstrucción que mínimo necesita autenticación de WS-Federation tooconfigure. Es mucho más sencillo y más elegante de WIF, donde se inyecta Web.config con XML todo lugar Hola. Hola solo información que necesita es Hola del usuario de confianza (RP) hello y el identificador de dirección URL del archivo de metadatos de su servicio de AD FS. Este es un ejemplo:
   
   * Identificador del usuario de confianza: `https://contoso.com/MyLOBApp`
   * Dirección de metadatos: `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`
4. En App_Start\Startup.Auth.cs, cambie Hola siguiendo las definiciones de cadena estática:  
   
   <pre class="prettyprint">
   private static string realm = ConfigurationManager.AppSettings["ida:<mark>RPIdentifier</mark>"];
   <mark><del>private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];</del></mark>
   <mark><del>private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];</del></mark>
   <mark><del>private static string metadata = string.Format("{0}/{1}/federationmetadata/2007-06/federationmetadata.xml", aadInstance, tenant);</del></mark>
   <mark>private static string metadata = string.Format("https://{0}/federationmetadata/2007-06/federationmetadata.xml", ConfigurationManager.AppSettings["ida:ADFS"]);</mark>
   
   <mark><del>string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);</del></mark>
   </pre>
5. Ahora, realizar los cambios correspondientes de hello en el archivo Web.config. Abra Web.config hello y modificar Hola después de la configuración de la aplicación:  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="webpages:Version" value="3.0.0.0" /&gt;
   &lt;add key="webpages:Enabled" value="false" /&gt;
   &lt;add key="ClientValidationEnabled" value="true" /&gt;
   &lt;add key="UnobtrusiveJavaScriptEnabled" value="true" /&gt;
   <mark><del>&lt;add key="ida:Wtrealm" value="[Enter hello App ID URI of WebApp-WSFederation-DotNet https://contoso.onmicrosoft.com/WebApp-WSFederation-DotNet]" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:AADInstance" value="https://login.microsoftonline.com" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" /&gt;</del></mark>
   <mark>&lt;add key="ida:RPIdentifier" value="[Enter hello relying party identifier as configured in AD FS, e.g. https://localhost:44320/]" /&gt;</mark>
   <mark>&lt;add key="ida:ADFS" value="[Enter hello FQDN of AD FS service, e.g. adfs.contoso.com]" /&gt;</mark>
   
   &lt;/appSettings&gt;
   </pre>
   
   Rellene los valores de clave de hello en función del entorno respectivo.
6. Hola toomake de aplicación que no hay ningún error de compilación.

Eso es todo. Ahora la aplicación de ejemplo de Hola es toowork listo con AD FS. Todavía necesita tooconfigure una confianza RP con esta aplicación en AD FS.

<a name="bkmk_deploy"></a>

## <a name="deploy-hello-sample-application-tooazure-app-service-web-apps"></a>Implementar tooAzure de aplicación de ejemplo de Hola aplicación del servicio de aplicaciones Web
En este caso, publicar Hola aplicación tooa web app en aplicaciones Web de servicio de aplicación mientras conserva el entorno de depuración de Hola. Tenga en cuenta que se vayan aplicación hello de toopublish antes de tener una confianza RP con AD FS, por lo que la autenticación sigue sin funciona aún. Sin embargo, si lo hace, ahora puede tener Hola URL de aplicación web que puede usar confianza RP de hello tooconfigure más tarde.

1. Haga clic con el botón derecho en el proyecto y seleccione **Publicar**.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/01-publish-website.png)
2. Seleccione **Servicio de aplicaciones de Microsoft Azure**.
3. Si no está registrado en tooAzure, haga clic en **inicio de sesión** y utilizar cuenta de Microsoft de Hola para su toosign de suscripción de Azure en.
4. Una vez iniciado sesión, haga clic en **New** toocreate una aplicación web.
5. Rellene todos los campos obligatorios. Va datos tooon local de tooconnect más adelante, por lo que no cree una base de datos de esta aplicación web.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/02-create-website.png)
6. Haga clic en **Crear**. Una vez creada la aplicación web de hello, se abre el cuadro de diálogo de publicación Web de Hola.
7. En **dirección URL de destino**, cambiar **http** demasiado**https**. Copie Hola todo URL tooa editor de texto para su uso posterior. A continuación, haga clic en **Publicar**.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/03-destination-url.png)
8. En Visual Studio, abra **Web.Release.config** en el proyecto. Insertar Hola continuación de XML en hello `<configuration>` etiqueta y reemplace el valor de clave de Hola con la dirección URL de la aplicación web publicar.  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="ida:RPIdentifier" value="<mark>[e.g. https://mylobapp.azurewebsites.net/]</mark>" xdt:Transform="SetAttributes" xdt:Locator="Match(key)" /&gt;
   &lt;/appSettings&gt;</pre>

Cuando haya terminado, tendrá dos identificadores RP configurados en su proyecto, uno para el entorno de depuración en Visual Studio, y uno para hello publica la aplicación web en Azure. Configurará una confianza RP para cada uno de los dos entornos de hello en AD FS. Durante la depuración, configuración de aplicaciones de hello en el archivo Web.config está toomake usa su **depurar** trabajo de configuración con AD FS. Cuando se publica (de forma predeterminada, Hola **versión** se publica la configuración), se carga un archivo Web.config transformado que incorpora cambios de configuración de aplicación hello en Web.Release.config.

Si desea tooattach hello web publicado aplicación en Azure toohello depurador (es decir, debe cargar símbolos de depuración del código de aplicación web publicada de hello), puede crear un clon del programa Hola a depurar la configuración de depuración de Azure, pero con su propio archivo Web.config personalizado transformar) Por ejemplo, Web.AzureDebug.config) que usa la configuración de la aplicación hello desde Web.Release.config. Esto le permite toomaintain una configuración estática entre diferentes entornos de Hola.

<a name="bkmk_rptrusts"></a>

## <a name="configure-relying-party-trusts-in-ad-fs-management"></a>Configurar las relaciones de confianza para usuarios autenticados en la administración de AD FS
Ahora debe tooconfigure una confianza RP en administración de AD FS para poder usar la aplicación de ejemplo y autenticarse con AD FS. Necesitará tooset dos relaciones de confianza de RP independientes, uno para el entorno de depuración y otro para la aplicación web publicada.

> [!NOTE]
> Asegúrese de que repita Hola siguiendo los pasos para ambos de sus entornos.
> 
> 

1. En el servidor de AD FS, inicie sesión con las credenciales que tienen derechos de administración tooAD FS.
2. Abra Administración de AD FS. Haga clic con el botón derecho en **AD FS\Trusted Relationships\Relying Party Trusts** y seleccione **Agregar relación de confianza para usuario de confianza**.
   
   ![](./media/web-sites-dotnet-lob-application-adfs/1-add-rptrust.png)
3. Hola **Seleccionar origen de datos** , seleccione **escribir manualmente los datos sobre el usuario de confianza de hello**. 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/2-enter-rp-manually.png)
4. Hola **especificar nombre para mostrar** página, escriba un nombre para mostrar para la aplicación hello y haga clic en **siguiente**.
5. Hola **elegir protocolo** página, haga clic en **siguiente**.
6. Hola **configurar certificado** página, haga clic en **siguiente**.
   
   > [!NOTE]
   > Puesto que ya debería estar usando HTTPS, los tokens cifrados son opcionales. Si realmente desea tooencrypt tokens de AD FS en esta página, también debe agregar lógica de descifrado de token en el código. Para obtener más información, consulte [Configurar manualmente middleware de WS-Federation de OWIN y aceptar tokens cifrados](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).
   > 
   > 
7. Antes de pasar al paso siguiente de hello, necesita una parte de la información de su proyecto de Visual Studio. En Propiedades del proyecto hello, tenga en cuenta hello **dirección URL de SSL** de aplicación hello. 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/3-ssl-url.png)
8. En administración de AD FS, en hello **configurar dirección URL** página de hello **entidad confiar en Asistente para agregar**, seleccione **habilitar la compatibilidad de protocolo WS-Federation Passive hello** y Escriba Hola dirección URL de SSL de su proyecto de Visual Studio que anotó en el paso anterior de Hola. A continuación, haga clic en **Siguiente**.
   
   ![](./media/web-sites-dotnet-lob-application-adfs/4-configure-url.png)
   
   > [!NOTE]
   > Dirección URL especifica donde el cliente de hello toosend tras la autenticación se realiza correctamente. Para el entorno de depuración de hello, debe ser <code>https://localhost:&lt;port&gt;/</code>. Para la aplicación web publicada de hello, debe ser URL de la aplicación hello web.
   > 
   > 
9. Hola **configurar identificadores** página, compruebe que la dirección URL de SSL de proyecto ya aparece y haga clic en **siguiente**. Haga clic en **siguiente** todos Hola final de manera toohello del Asistente para hello con selecciones predeterminadas.
   
   > [!NOTE]
   > En App_Start\Startup.Auth.cs de su proyecto de Visual Studio, este identificador se compara con valor de Hola de <code>WsFederationAuthenticationOptions.Wtrealm</code> durante la autenticación federada. De forma predeterminada, la dirección URL de la aplicación hello del paso anterior Hola se agrega como un identificador RP.
   > 
   > 
10. Ahora haya terminado de configurar Hola aplicación RP para el proyecto en AD FS. A continuación, configure este toosend aplicación Hola notificaciones necesarios para la aplicación. Hola **editar reglas de notificación** cuadro de diálogo se abre de forma predeterminada para al final de hello del Asistente de Hola para que pueda empezar inmediatamente. Vamos a configurar al menos Hola siguientes notificaciones (con esquemas entre paréntesis):
    
    * Nombre (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - utilizado por ASP.NET toohydrate `User.Identity.Name`.
    * Usuario nombre de entidad de seguridad (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - usado toouniquely identificar a los usuarios en la organización de Hola.
    * Pertenencia a grupos como roles (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - puede utilizarse con `[Authorize(Roles="role1, role2,...")]` decoración tooauthorize controladores o acciones. En realidad, este enfoque puede no ser Hola que ofrece mayor rendimiento para la autorización de rol. Si los usuarios de AD pertenecen toohundreds de grupos de seguridad, se convierten en cientos de notificaciones de rol en el token SAML de Hola. Un enfoque alternativo es toosend una única función de notificación condicionalmente según la pertenencia del usuario de hello en un grupo determinado. Sin embargo, lo mantendremos sencillo para este tutorial.
    * Identificador de nombre (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier): se puede usar para la validación de antifalsificación. Para obtener más información sobre cómo toomake funciona con validación antifalsificación, vea hello **agregar funcionalidad de línea de negocio** sección de [crear una aplicación de Azure de línea de negocio con la autenticación de Azure Active Directory ](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).
    
    > [!NOTE]
    > Hello notificación tipos que se necesita tooconfigure la aplicación se determina mediante las necesidades de su aplicación. Lista de Hola de notificaciones admitidos por las aplicaciones de Azure Active Directory (es decir, las confianzas RP), por ejemplo, vea [admite tokens y los tipos de notificación](http://msdn.microsoft.com/library/azure/dn195587.aspx).
    > 
    > 
11. En el cuadro de diálogo de hello editar reglas de notificación, haga clic en **Agregar regla**.
12. Configurar notificaciones de rol, UPN y nombre de hello tal y como se muestra en la captura de pantalla de Hola y haga clic en **finalizar**.
    
    ![](./media/web-sites-dotnet-lob-application-adfs/5-ldap-claims.png)
    
    A continuación, cree un nombre temporal Id. de notificación mediante Hola pasos mostrados en [identificadores de nombre en las aserciones de SAML](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).
13. Haga clic en **Agregar regla** de nuevo.
14. Seleccione **Enviar notificaciones con una regla personalizada** y haga clic en **Siguiente**.
15. Siguiente de hello pegar regla lenguaje en hello **regla personalizada** cuadro, nombre de regla de hello **por el identificador de sesión** y haga clic en **finalizar**.  
    
    <pre class="prettyprint">
    c1:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"] &amp;&amp;
    c2:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant"]
     => add(
         store = "_OpaqueIdStore",
         types = ("<mark>http://contoso.com/internal/sessionid</mark>"),
         query = "{0};{1};{2};{3};{4}",
         param = "useEntropy",
         param = c1.Value,
         param = c1.OriginalIssuer,
         param = "",
         param = c2.Value);
    </pre>
    
    Su regla personalizada debe tener un aspecto similar a esta captura de pantalla:
    
    ![](./media/web-sites-dotnet-lob-application-adfs/6-per-session-identifier.png)
16. Haga clic en **Agregar regla** de nuevo.
17. Seleccione **Transformar una notificación entrante** y haga clic en **Siguiente**.
18. Configurar regla de hello tal y como se muestra en la captura de pantalla de hello (mediante el tipo de notificación de Hola que creó en la regla personalizada hello) y haga clic en **finalizar**.
    
    ![](./media/web-sites-dotnet-lob-application-adfs/7-transient-name-id.png)
    
    Para obtener información detallada sobre los pasos de Hola para notificación de Id. de nombre transitorio hello, consulte [identificadores de nombre en las aserciones de SAML](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).
19. Haga clic en **aplicar** en hello **editar reglas de notificación** cuadro de diálogo. Ahora debería ser similar Hola siguiente captura de pantalla:
    
    ![](./media/web-sites-dotnet-lob-application-adfs/8-all-claim-rules.png)
    
    > [!NOTE]
    > Nuevamente, asegúrese de repetir estos pasos tanto para el entorno de depuración como para la aplicación web publicada.
    > 
    > 

<a name="bkmk_test"></a>

## <a name="test-federated-authentication-for-your-application"></a>Probar la autenticación federada para la aplicación
Se está tootest listo lógica de autenticación de la aplicación en AD FS. En el entorno de laboratorio de AD FS, tengo un usuario de prueba que pertenece el grupo de prueba de tooa en Active Directory (AD).

![](./media/web-sites-dotnet-lob-application-adfs/10-test-user-and-group.png)

autenticación de tootest en el depurador hello, todo lo que necesita toodo ahora es de tipo `F5`. Si desea que la autenticación tootest en aplicación web publicada de hello, Explorar dirección URL de toohello.

Una vez cargada la aplicación web de hello, haga clic en **inicio de sesión**. Ahora deberá obtener cualquier un inicio de sesión Hola o cuadro de diálogo Inicio de sesión página atendida por AD FS, según el método de autenticación de hello elegido por AD FS. Esto es lo que aparece en Internet Explorer 11.

![](./media/web-sites-dotnet-lob-application-adfs/9-test-debugging.png)

Una vez que inicie sesión con un usuario de dominio de AD de Hola de implementación de hello AD FS, ahora debería ver la página principal de hello nuevo con **Hola, <User Name>!** en la esquina de Hola. Esto es lo que vemos.

![](./media/web-sites-dotnet-lob-application-adfs/11-test-debugging-success.png)

Hasta ahora, ha logrado Hola siguientes maneras:

* La aplicación ha alcanzado correctamente AD FS y un identificador RP coincidente se encuentra en hello base de datos de AD FS
* AD FS haya autenticado correctamente una redirección de realizar la copia de la página de inicio de la aplicación toohello y usuarios de AD
* AD FS como nombre de hello enviado correctamente de notificación (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) tooyour aplicación, como se indica por el hecho de hello ese usuario Hola nombre se muestra en la esquina de Hola. 

Si falta la notificación de nombre de hello, habría visto **Hola!**. Si observa Views\Shared\_LoginPartial.cshtml, encontrará que usa `User.Identity.Name` nombre de usuario de toodisplay Hola. Como se mencionó anteriormente, si nombre Hola de notificación de hello autenticado de usuario está disponible en el token SAML de hello, ASP.NET hydrates esta propiedad con él. toosee que Hola a todos de notificaciones que se envían por AD FS, coloque un punto de interrupción en controllers\homecontroller. cs, Hola método de acción de índice. Una vez autenticado el usuario hello, inspeccionar hello `System.Security.Claims.Current.Claims` colección.

![](./media/web-sites-dotnet-lob-application-adfs/12-test-debugging-all-claims.png) 

<a name="bkmk_authorize"></a>

## <a name="authorize-users-for-specific-controllers-or-actions"></a>Autorizar a los usuarios para acciones o controladores concretos
Puesto que ha incluido las pertenencias a grupos como notificaciones de rol en la configuración de confianza RP, ahora puede usar ellos directamente en hello `[Authorize(Roles="...")]` decoración para controladores y acciones. En una aplicación de línea de negocio con patrón de hello crear-lectura-actualización y eliminación (CRUD), puede autorizar a roles específicos tooaccess cada acción. Por ahora, simplemente intentará el uso de esta característica en el controlador principal existente de Hola.

1. Abra Controllers\HomeController.cs.
2. Decorar hello `About` y `Contact` toohello similar de acción métodos siguiente código, el uso de miembros de grupos de seguridad que el usuario autenticado.  
   
    <pre class="prettyprint">
    <mark>[Authorize(Roles="Test Group")]</mark>
    public ActionResult About()
    {
        ViewBag.Message = "Your application description page.";
   
        return View();
    }
   
    <mark>[Authorize(Roles="Domain Admins")]</mark>
    public ActionResult Contact()
    {
        ViewBag.Message = "Your contact page.";
   
        return View();
    }
    </pre>
   
    Puesto que se ha agregado **usuario de prueba** demasiado**grupo de prueba** en mi entorno de laboratorio de AD FS, podrá usar autorización de grupo de prueba tootest en `About`. Para `Contact`, probará caso negativo de Hola de **Admins. del dominio**, toowhich **usuario probar** no pertenece.
3. Iniciar el depurador de hello escribiendo `F5` e iniciar sesión, a continuación, haga clic en **sobre**. Se debería ver ahora hello `~/About/Index` página correctamente, si el usuario autenticado tiene autorización para esa acción.
4. Ahora haga clic en **póngase en contacto con**, que en mi caso debe autorizar no **usuario de prueba** para la acción de Hola. Sin embargo, Explorador de hello es redirigido tooAD FS, que finalmente se muestra este mensaje:
   
    ![](./media/web-sites-dotnet-lob-application-adfs/13-authorize-adfs-error.png)
   
    Si investigar este error en el Visor de eventos en el servidor de AD FS de hello, verá este mensaje de excepción:  
   
    <pre class="prettyprint">
    Microsoft.IdentityServer.Web.InvalidRequestException: MSIS7042: <mark>hello same client browser session has made '6' requests in hello last '11' seconds.</mark> Contact your administrator for details.
       at Microsoft.IdentityServer.Web.Protocols.PassiveProtocolHandler.UpdateLoopDetectionCookie(WrappedHttpListenerContext context)
       at Microsoft.IdentityServer.Web.Protocols.WSFederation.WSFederationProtocolHandler.SendSignInResponse(WSFederationContext context, MSISSignInResponse response)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.ProcessProtocolRequest(ProtocolContext protocolContext, PassiveProtocolHandler protocolHandler)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.OnGetContext(WrappedHttpListenerContext context)
    </pre>
   
    motivo de Hola de este error es que de forma predeterminada, MVC devuelve un 401 no autorizado cuando roles de usuario no están autorizados. Esto desencadena un proveedor de identidad de la reautenticación solicitud tooyour (AD FS). Puesto que ya está autenticado el usuario Hola, AD FS devuelve toohello sintonía, que, a continuación, emite otra 401, crear un bucle de redirección. Deberá reemplazar de AuthorizeAttribute `HandleUnauthorizedRequest` método con una lógica sencilla tooshow algo que tiene sentido en lugar de bucle de redirección de hello continuando.
5. Cree un archivo de proyecto de hello denominado AuthorizeAttribute.cs y Hola pegar siguiente código en él.
   
        using System;
        using System.Web.Mvc;
        using System.Web.Routing;
   
        namespace WebApp_WSFederation_DotNet
        {
            [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
            public class AuthorizeAttribute : System.Web.Mvc.AuthorizeAttribute
            {
                protected override void HandleUnauthorizedRequest(AuthorizationContext filterContext)
                {
                    if (filterContext.HttpContext.Request.IsAuthenticated)
                    {
                        filterContext.Result = new System.Web.Mvc.HttpStatusCodeResult((int)System.Net.HttpStatusCode.Forbidden);
                    }
                    else
                    {
                        base.HandleUnauthorizedRequest(filterContext);
                    }
                }
            }
        }
   
    Hola invalidar envía un HTTP 403 (prohibido) de código en lugar de HTTP 401 (no autorizado) en los casos autenticados pero no autorizados.
6. Ejecutar el depurador de hello nuevo con `F5`. Si se hace clic en **Contacto** aparece ahora un mensaje de error más informativo (aunque poco atractivo):
   
    ![](./media/web-sites-dotnet-lob-application-adfs/14-unauthorized-forbidden.png)
7. Vuelva a publicar Hola aplicación tooAzure aplicación del servicio de aplicaciones Web y probar el comportamiento de Hola de aplicación de hello en vivo.

<a name="bkmk_data"></a>

## <a name="connect-tooon-premises-data"></a>Conectar datos tooon locales
Un motivo que desearía tooimplement la aplicación de línea de negocio con AD FS en lugar de Azure Active Directory es problemas de compatibilidad con la actualización de la organización datos local y remota. Esto también puede significar que la aplicación web en Azure debe tener acceso a las bases de datos local, ya que no se permiten toouse [base de datos SQL](/services/sql-database/) como capa de datos de Hola para las aplicaciones web.

Azure App Service Web Apps admite el acceso a bases de datos locales con dos enfoques: [Conexiones híbridas](../biztalk-services/integration-hybrid-connection-overview.md) y [Redes virtuales](web-sites-integrate-with-vnet.md). Para obtener más información, consulte [Uso de integración VNET y conexiones híbridas con Aplicaciones web del Servicio de aplicaciones de Azure](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).

<a name="bkmk_resources"></a>

## <a name="further-resources"></a>Recursos adicionales
* [Autenticación con Active Directory local en aplicaciones de Azure](web-sites-authentication-authorization.md)
* [Creación de una aplicación de línea de negocio de Azure con autenticación de Azure Active Directory](web-sites-dotnet-lob-application-azure-ad.md)
* [Usar hello local organizativa autenticación opción (ADFS) con ASP.NET en Visual Studio 2013](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)
* [Migrar un proyecto de VS2013 Web de WIF tooKatana](http://www.cloudidentity.com/blog/2014/09/15/MIGRATE-A-VS2013-WEB-PROJECT-FROM-WIF-TO-KATANA/)
* [Información general de Servicios de federación de Active Directory](http://technet.microsoft.com/library/hh831502.aspx)
* [Especificación de WS-Federation 1.1](http://download.boulder.ibm.com/ibmdl/pub/software/dw/specs/ws-fed/WS-Federation-V1-1B.pdf?S_TACT=105AGX04&S_CMP=LP)

