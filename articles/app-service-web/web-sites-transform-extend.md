---
title: "aplicación de servicio de aplicaciones web aaaAzure configuración avanzada y extensiones"
description: "Utilice Transformation(XDT) del documento XML el archivo ApplicationHost.config de declaraciones tootransform hello en los servicio de aplicaciones de Azure web app y tooadd las extensiones privadas tooenable personalizado acciones de administración."
author: cephalin
writer: cephalin
editor: mollybos
manager: erikre
services: app-service
documentationcenter: 
ms.assetid: b441a286-ef38-4abc-b102-cdb249baf5bc
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/25/2016
ms.author: cephalin
ms.openlocfilehash: 873347ac13113d1ac989cba29128382c81dcfcca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-web-app-advanced-config-and-extensions"></a><span data-ttu-id="3c14e-103">Configuración avanzada y extensiones de aplicación web del Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="3c14e-103">Azure App Service web app advanced config and extensions</span></span>
<span data-ttu-id="3c14e-104">Mediante el uso de [transformación del documento XML](http://msdn.microsoft.com/library/dd465326.aspx) declaraciones (XDT), puede transformar hello [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) archivo en la aplicación web en el servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="3c14e-104">By using [XML Document Transformation](http://msdn.microsoft.com/library/dd465326.aspx) (XDT) declarations, you can transform hello [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) file in your web app in Azure App Service.</span></span> <span data-ttu-id="3c14e-105">También puede utilizar XDT declaraciones tooadd las extensiones privadas tooenable web personalizado aplicación acciones de administración.</span><span class="sxs-lookup"><span data-stu-id="3c14e-105">You can also use XDT declarations tooadd private extensions tooenable custom web app administration actions.</span></span> <span data-ttu-id="3c14e-106">Este artículo incluye una extensión de aplicación web del administrador PHP de ejemplo que habilita la administración de la configuración de PHP a través de una interfaz web.</span><span class="sxs-lookup"><span data-stu-id="3c14e-106">This article includes a sample PHP Manager web app extension that enables management of PHP settings through a web interface.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="3c14e-107"><a id="transform"></a>Configuración avanzada mediante ApplicationHost.config</span><span class="sxs-lookup"><span data-stu-id="3c14e-107"><a id="transform"></a>Advanced configuration through ApplicationHost.config</span></span>
<span data-ttu-id="3c14e-108">Hola plataforma de servicio de aplicaciones proporciona flexibilidad y control para la configuración de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="3c14e-108">hello App Service platform provides flexibility and control for web app configuration.</span></span> <span data-ttu-id="3c14e-109">Aunque el archivo de configuración ApplicationHost.config de IIS estándar hello no está disponible para ser editados directamente en el servicio de aplicaciones, plataforma hello es compatible con un modelo de transformación ApplicationHost.config declarativo basado en XML documento transformación (XDT).</span><span class="sxs-lookup"><span data-stu-id="3c14e-109">Although hello standard IIS ApplicationHost.config configuration file is not available for direct editing in App Service, hello platform supports a declarative ApplicationHost.config transform model based on XML Document Transformation (XDT).</span></span>

<span data-ttu-id="3c14e-110">tooleverage esta funcionalidad de transformación, puede crear un archivo ApplicationHost.xdt con XDT contenido y coloque en la raíz del sitio (d:\home\site) Hola Hola [Kudu consola](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span><span class="sxs-lookup"><span data-stu-id="3c14e-110">tooleverage this transform functionality, you create an ApplicationHost.xdt file with XDT content and place under hello site root (d:\home\site) in hello [Kudu Console](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span></span> <span data-ttu-id="3c14e-111">Puede necesitar toorestart hello Web App para cambios tootake efecto.</span><span class="sxs-lookup"><span data-stu-id="3c14e-111">You may need toorestart hello Web App for changes tootake effect.</span></span>

<span data-ttu-id="3c14e-112">Hola después applicationHost.xdt ejemplo muestra cómo tooadd una tooa de variable de entorno personalizado nuevo web aplicación que use PHP 5.4.</span><span class="sxs-lookup"><span data-stu-id="3c14e-112">hello following applicationHost.xdt sample shows how tooadd a new custom environment variable tooa web app that uses PHP 5.4.</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.webServer>
    <fastCgi>
      <application>
        <environmentVariables>
          <environmentVariable name="CONFIGTEST" value="TEST" xdt:Transform="Insert" xdt:Locator="XPath(/configuration/system.webServer/fastCgi/application[contains(@fullPath,'5.4')]/environmentVariables)" />
        </environmentVariables>
      </application>
    </fastCgi>
  </system.webServer>
</configuration>
```

<span data-ttu-id="3c14e-113">Un archivo de registro con detalles y el estado de transformación está disponible desde la raíz de hello FTP en LogFiles\Transform.</span><span class="sxs-lookup"><span data-stu-id="3c14e-113">A log file with transform status and details is available from hello FTP root under LogFiles\Transform.</span></span>

<span data-ttu-id="3c14e-114">Para ejemplos adicionales, vea [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span><span class="sxs-lookup"><span data-stu-id="3c14e-114">For additional samples, see [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span></span>

<span data-ttu-id="3c14e-115">**Nota:**</span><span class="sxs-lookup"><span data-stu-id="3c14e-115">**Note**</span></span><br />
<span data-ttu-id="3c14e-116">Elementos de lista de Hola de módulos en `system.webServer` no se puede quitar o reordenar, pero la lista de toohello adiciones son posibles.</span><span class="sxs-lookup"><span data-stu-id="3c14e-116">Elements from hello list of modules under `system.webServer` cannot be removed or reordered, but additions toohello list are possible.</span></span>

## <span data-ttu-id="3c14e-117"><a id="extend"></a> Ampliación de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="3c14e-117"><a id="extend"></a> Extend your web app</span></span>
### <span data-ttu-id="3c14e-118"><a id="overview"></a> Información general de las extensiones de aplicación web privada</span><span class="sxs-lookup"><span data-stu-id="3c14e-118"><a id="overview"></a> Overview of private web app extensions</span></span>
<span data-ttu-id="3c14e-119">El Servicio de aplicaciones es compatible con extensiones de aplicación web como punto de extensibilidad para acciones administrativas.</span><span class="sxs-lookup"><span data-stu-id="3c14e-119">App Service supports web app extensions as an extensibility point for administrative actions.</span></span> <span data-ttu-id="3c14e-120">De hecho, algunas características de la plataforma del Servicio de aplicaciones se implementan como extensiones preinstaladas.</span><span class="sxs-lookup"><span data-stu-id="3c14e-120">In fact, some App Service platform features are implemented as pre-installed extensions.</span></span> <span data-ttu-id="3c14e-121">Mientras no se puede modificar preinstalada platform extensions: Hola, puede crear y configurar las extensiones privadas para su propia aplicación web.</span><span class="sxs-lookup"><span data-stu-id="3c14e-121">While hello pre-installed platform extensions cannot be modified, you can create and configure private extensions for your own web app.</span></span> <span data-ttu-id="3c14e-122">Esta funcionalidad también se basa en declaraciones XDT.</span><span class="sxs-lookup"><span data-stu-id="3c14e-122">This functionality also relies on XDT declarations.</span></span> <span data-ttu-id="3c14e-123">pasos clave de Hola para crear una extensión de la aplicación web privada son siguientes de hello:</span><span class="sxs-lookup"><span data-stu-id="3c14e-123">hello key steps for creating a private web app extension are hello following:</span></span>

1. <span data-ttu-id="3c14e-124">**Contenido**de la extensión de la aplicación web: crear todas las aplicaciones web compatibles con el Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="3c14e-124">Web app extension **content**: create any web application supported by App Service</span></span>
2. <span data-ttu-id="3c14e-125">**Declaración**de la extensión de la aplicación web: crear una aplicación ApplicationHost.xdt</span><span class="sxs-lookup"><span data-stu-id="3c14e-125">Web app extension **declaration**: create an ApplicationHost.xdt file</span></span>
3. <span data-ttu-id="3c14e-126">Extensión de la aplicación Web **implementación**: coloque el contenido en la carpeta SiteExtensions de hello en`root`</span><span class="sxs-lookup"><span data-stu-id="3c14e-126">Web app extension **deployment**: place content in hello SiteExtensions folder under `root`</span></span>

<span data-ttu-id="3c14e-127">Los vínculos internos de la aplicación web de hello deben apuntar tooa ruta de acceso relativa toohello ruta de la aplicación especificada en el archivo de hello ApplicationHost.xdt.</span><span class="sxs-lookup"><span data-stu-id="3c14e-127">Internal links for hello web app should point tooa path relative toohello application path specified in hello ApplicationHost.xdt file.</span></span> <span data-ttu-id="3c14e-128">Cualquier archivo de cambio toohello ApplicationHost.xdt requiere un reciclaje de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="3c14e-128">Any change toohello ApplicationHost.xdt file requires a web app recycle.</span></span>

<span data-ttu-id="3c14e-129">**Nota**: la información adicional para estos elementos clave se encuentra disponible en [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span><span class="sxs-lookup"><span data-stu-id="3c14e-129">**Note**: Additional information for these key elements is available at [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span></span>

<span data-ttu-id="3c14e-130">Un ejemplo detallado es tooillustrate incluye Hola pasos para crear y habilitar una extensión de la aplicación web privada.</span><span class="sxs-lookup"><span data-stu-id="3c14e-130">A detailed example is included tooillustrate hello steps for creating and enabling a private web app extension.</span></span> <span data-ttu-id="3c14e-131">Hola código fuente de ejemplo de Hola a PHP Manager que se indica a continuación puede descargarse desde [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span><span class="sxs-lookup"><span data-stu-id="3c14e-131">hello source code for hello PHP Manager example that follows can be downloaded from [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span></span>

### <span data-ttu-id="3c14e-132"><a id="SiteSample"></a> Ejemplo de extensión de aplicación web:</span><span class="sxs-lookup"><span data-stu-id="3c14e-132"><a id="SiteSample"></a> Web app extension example: PHP Manager</span></span>
<span data-ttu-id="3c14e-133">PHP Manager es una extensión de la aplicación web que permite a los administradores de aplicación de web tooeasily ver y configura sus opciones de PHP con una interfaz web en lugar de tener los archivos .ini de toomodify PHP directamente.</span><span class="sxs-lookup"><span data-stu-id="3c14e-133">PHP Manager is a web app extension that allows web app administrators tooeasily view and configure their PHP settings using a web interface instead of having toomodify PHP .ini files directly.</span></span> <span data-ttu-id="3c14e-134">Los archivos de configuración comunes para PHP incluyen archivo php.ini de hello ubicado en archivos de programa y Hola. archivo user.ini ubicado en la carpeta raíz de saludo de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="3c14e-134">Common configuration files for PHP include hello php.ini file located under Program Files and hello .user.ini file located in hello root folder of your web app.</span></span> <span data-ttu-id="3c14e-135">Como archivo php.ini de hello no se puede editar directamente en hello plataforma de servicio de aplicaciones, Hola extensión de PHP Manager utiliza Hola. user.ini archivo tooapply cambios en la configuración.</span><span class="sxs-lookup"><span data-stu-id="3c14e-135">Since hello php.ini file is not directly editable on hello App Service platform, hello PHP Manager extension uses hello .user.ini file tooapply setting changes.</span></span>

#### <span data-ttu-id="3c14e-136"><a id="PHPwebapp"></a>Hola aplicación web PHP Manager</span><span class="sxs-lookup"><span data-stu-id="3c14e-136"><a id="PHPwebapp"></a> hello PHP Manager web application</span></span>
<span data-ttu-id="3c14e-137">Hola te mostramos Hola portada de hello implementación del Administrador de PHP:</span><span class="sxs-lookup"><span data-stu-id="3c14e-137">hello following is hello home page of hello PHP Manager deployment:</span></span>

![TransformSitePHPUI][TransformSitePHPUI]

<span data-ttu-id="3c14e-139">Como puede ver, una extensión de la aplicación web es igual que una aplicación web normal, pero con un archivo ApplicationHost.xdt adicional en hello carpeta de raíz de aplicación web de hello (más detalles sobre el archivo de hello ApplicationHost.xdt están disponibles en la sección siguiente de Hola de este artículo).</span><span class="sxs-lookup"><span data-stu-id="3c14e-139">As you can see, a web app extension is just like a regular web application, but with an additional ApplicationHost.xdt file placed in hello root folder of hello web app (more details about hello ApplicationHost.xdt file are available in hello next section of this article).</span></span>

<span data-ttu-id="3c14e-140">Hola extensión de PHP Manager se creó con la plantilla de aplicación Web ASP.NET MVC 4 de Visual Studio Hola.</span><span class="sxs-lookup"><span data-stu-id="3c14e-140">hello PHP Manager extension was created using hello Visual Studio ASP.NET MVC 4 Web Application template.</span></span> <span data-ttu-id="3c14e-141">Hello siguiente vista del explorador de soluciones muestra hello estructura de extensión de PHP Manager Hola.</span><span class="sxs-lookup"><span data-stu-id="3c14e-141">hello following view from Solution Explorer shows hello structure of hello PHP Manager extension.</span></span>

![TransformSiteSolEx][TransformSiteSolEx]

<span data-ttu-id="3c14e-143">Hello solo una lógica especial necesaria para E/S de archivo es tooindicate donde hello directorio wwwroot de hello web app se encuentra.</span><span class="sxs-lookup"><span data-stu-id="3c14e-143">hello only special logic needed for file I/O is tooindicate where hello wwwroot directory of hello web app is located.</span></span> <span data-ttu-id="3c14e-144">Tal y como se muestra de ejemplo de código siguiente, Hola Hola variable de entorno "HOME" indica Hola ruta de acceso de la aplicación web raíz, y se puede construir la ruta de acceso de hello wwwroot anexando "site\wwwroot":</span><span class="sxs-lookup"><span data-stu-id="3c14e-144">As hello following code example shows, hello environment variable "HOME" indicates hello web app's root path, and hello wwwroot path can be constructed by appending "site\wwwroot":</span></span>

```csharp
/// <summary>
/// Gives hello location of hello .user.ini file, even if one doesn't exist yet
/// </summary>
private static string GetUserSettingsFilePath()
{
  var rootPath = Environment.GetEnvironmentVariable("HOME"); // For use on Azure Websites
  if (rootPath == null)
  {
    rootPath = System.IO.Path.GetTempPath(); // For testing purposes
  };
  var userSettingsFile = Path.Combine(rootPath, @"site\wwwroot\.user.ini");
  return userSettingsFile;
}
```


<span data-ttu-id="3c14e-145">Una vez que la ruta de acceso de directorio de hello, puede usar tooread de operaciones de E/S de archivos normales y escribir toofiles.</span><span class="sxs-lookup"><span data-stu-id="3c14e-145">After you have hello directory path, you can use regular file I/O operations tooread and write toofiles.</span></span>

<span data-ttu-id="3c14e-146">Un punto de precaución con extensiones de aplicaciones web que se refiere a control de Hola de vínculos internos.</span><span class="sxs-lookup"><span data-stu-id="3c14e-146">One point of caution with web app extensions regards hello handling of internal links.</span></span>  <span data-ttu-id="3c14e-147">Si tiene los vínculos en los archivos HTML que proporcionan rutas de acceso absolutas toointernal vínculos en la aplicación web, debe asegurarse de que esos vínculos se anteponen con el nombre de extensión como la raíz.</span><span class="sxs-lookup"><span data-stu-id="3c14e-147">If you have any links in your HTML files that give absolute paths toointernal links on your web app, you must ensure those links are prepended with your extension name as your root.</span></span> <span data-ttu-id="3c14e-148">Esto es necesario porque la raíz de hello para la extensión es ahora "/`[your-extension-name]`/" en lugar de ser simplemente "/", por lo que cualquier interno vínculos deben actualizarse según corresponda.</span><span class="sxs-lookup"><span data-stu-id="3c14e-148">This is needed because hello root for your extension is now "/`[your-extension-name]`/" rather than being just "/", so any internal links must be updated accordingly.</span></span> <span data-ttu-id="3c14e-149">Por ejemplo, suponga que su código incluye un siguiente de toohello de vínculo:</span><span class="sxs-lookup"><span data-stu-id="3c14e-149">For example, suppose your code includes a link toohello following:</span></span>

`"<a href="/Home/Settings">PHP Settings</a>"`

<span data-ttu-id="3c14e-150">Al vínculo Hola forma parte de una extensión de la aplicación web, vínculo Hola debe estar en hello siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="3c14e-150">When hello link is part of a web app extension, hello link must be in hello following form:</span></span>

`"<a href="/[your-site-name]/Home/Settings">Settings</a>"`

<span data-ttu-id="3c14e-151">Puede solucionar este requisito mediante solo Hola a rutas de acceso relativas en su aplicación web, o en el caso de aplicaciones de ASP.NET, mediante el uso de hello `@Html.ActionLink` método que crea vínculos adecuados de Hola para usted.</span><span class="sxs-lookup"><span data-stu-id="3c14e-151">You can work around this requirement by either using only relative paths within your web application, or in hello case of ASP.NET applications, by using hello `@Html.ActionLink` method which creates hello appropriate links for you.</span></span>

#### <span data-ttu-id="3c14e-152"><a id="XDT"></a>archivo de Hello applicationHost.xdt</span><span class="sxs-lookup"><span data-stu-id="3c14e-152"><a id="XDT"></a> hello applicationHost.xdt file</span></span>
<span data-ttu-id="3c14e-153">código de Hello para la extensión de la aplicación web entra en %HOME%\SiteExtensions\[su nombre de extensión].</span><span class="sxs-lookup"><span data-stu-id="3c14e-153">hello code for your web app extension goes under %HOME%\SiteExtensions\[your-extension-name].</span></span> <span data-ttu-id="3c14e-154">Llamaremos a esta raíz de la extensión de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c14e-154">We'll call this hello extension root.</span></span>  

<span data-ttu-id="3c14e-155">tooregister la extensión de la aplicación web con el archivo applicationHost.config de hello, necesita un archivo denominado ApplicationHost.xdt en la raíz de la extensión de hello tooplace.</span><span class="sxs-lookup"><span data-stu-id="3c14e-155">tooregister your web app extension with hello applicationHost.config file, you need tooplace a file called ApplicationHost.xdt in hello extension root.</span></span> <span data-ttu-id="3c14e-156">contenido de Hola del archivo de hello ApplicationHost.xdt debería ser como sigue:</span><span class="sxs-lookup"><span data-stu-id="3c14e-156">hello content of hello ApplicationHost.xdt file should be as follows:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.applicationHost>
    <sites>
      <site name="%XDT_SCMSITENAME%" xdt:Locator="Match(name)">
        <!-- NOTE: Add your extension name in hello application paths below -->
        <application path="/[your-extension-name]" xdt:Locator="Match(path)" xdt:Transform="Remove" />
        <application path="/[your-extension-name]" applicationPool="%XDT_APPPOOLNAME%" xdt:Transform="Insert">
          <virtualDirectory path="/" physicalPath="%XDT_EXTENSIONPATH%" />
        </application>
      </site>
    </sites>
  </system.applicationHost>
</configuration>
```

<span data-ttu-id="3c14e-157">nombre de Hello seleccionado como el nombre de la extensión debe disponer del mismo nombre de hello como la carpeta de raíz de la extensión.</span><span class="sxs-lookup"><span data-stu-id="3c14e-157">hello name you select as your extension name should have hello same name as your extension root folder.</span></span>

<span data-ttu-id="3c14e-158">Esto tiene el efecto de Hola de agregar un nuevo toohello de ruta de acceso de aplicación `system.applicationHost` lista de sitios en un sitio SCM Hola.</span><span class="sxs-lookup"><span data-stu-id="3c14e-158">This has hello effect of adding a new application path toohello `system.applicationHost` sites list under hello SCM site.</span></span> <span data-ttu-id="3c14e-159">sitio SCM Hello es un extremo de administración de sitio con las credenciales de acceso específico.</span><span class="sxs-lookup"><span data-stu-id="3c14e-159">hello SCM site is a site administration end point with specific access credentials.</span></span> <span data-ttu-id="3c14e-160">Tiene la dirección URL de hello `https://[your-site-name].scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="3c14e-160">It has hello URL `https://[your-site-name].scm.azurewebsites.net`.</span></span>  

```xml
<system.applicationHost>
  ...       
  <sites>
    <site name="~1[your-website]" id="1716402716">
      <bindings>
        <binding protocol="http" bindingInformation="*:80: [your-website].scm.azurewebsites.net" />
        <binding protocol="https" bindingInformation="*:443: [your-website].scm.azurewebsites.net" />
      </bindings>
      <traceFailedRequestsLogging enabled="false" directory="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\LogFiles" />
      <detailedErrorLogging enabled="false" directory="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\LogFiles\DetailedErrors" />
      <logFile logSiteId="false" />
      <application path="/" applicationPool="[your-website]">
        <virtualDirectory path="/" physicalPath="D:\Program Files (x86)\SiteExtensions\Kudu\1.24.20926.5" />
      </application>
      <!-- Note hello custom changes that go here -->
      <application path="/[your-extension-name]" applicationPool="[your-website]">
        <virtualDirectory path="/" physicalPath="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\SiteExtensions\[your-extension-name]" />
      </application>
    </site>
  </sites>
  ... 
</system.applicationHost>
```

### <span data-ttu-id="3c14e-161"><a id="deploy"></a> Implementación de extensión de aplicación web</span><span class="sxs-lookup"><span data-stu-id="3c14e-161"><a id="deploy"></a> Web app extension deployment</span></span>
<span data-ttu-id="3c14e-162">tooinstall la extensión de la aplicación web, puede usar FTP toocopy todos los archivos de saludo de su toohello de aplicación web `\SiteExtensions\[your-extension-name]` carpeta de aplicación web de hello en el que se desea la extensión de hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="3c14e-162">tooinstall your web app extension, you can use FTP toocopy all hello files of your web application toohello `\SiteExtensions\[your-extension-name]` folder of hello web app on which you want tooinstall hello extension.</span></span>  <span data-ttu-id="3c14e-163">Ser seguro toocopy hello ApplicationHost.xdt toothis ubicación del archivo también.</span><span class="sxs-lookup"><span data-stu-id="3c14e-163">Be sure toocopy hello ApplicationHost.xdt file toothis location as well.</span></span> <span data-ttu-id="3c14e-164">Reinicie la extensión de Hola de tooenable de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="3c14e-164">Restart your web app tooenable hello extension.</span></span>

<span data-ttu-id="3c14e-165">Debe ser capaz de toosee la extensión de la aplicación web en:</span><span class="sxs-lookup"><span data-stu-id="3c14e-165">You should be able toosee your web app extension at:</span></span>

`https://[your-site-name].scm.azurewebsites.net/[your-extension-name]`

<span data-ttu-id="3c14e-166">Tenga en cuenta que Hola que dirección URL es igual que la dirección URL de hello para la aplicación web, salvo que usa HTTPS y contiene ".scm".</span><span class="sxs-lookup"><span data-stu-id="3c14e-166">Note that hello URL looks just like hello URL for your web app, except that it uses HTTPS and contains ".scm".</span></span>

<span data-ttu-id="3c14e-167">Es privada todos los posibles toodisable (no preinstalado) extensiones para la aplicación web durante el desarrollo y las investigaciones mediante la adición de una configuración de la aplicación con la clave de hello `WEBSITE_PRIVATE_EXTENSIONS` y un valor de `0`.</span><span class="sxs-lookup"><span data-stu-id="3c14e-167">It is possible toodisable all private (not pre-installed) extensions for your web app during development and investigations by adding an app settings with hello key `WEBSITE_PRIVATE_EXTENSIONS` and a value of `0`.</span></span>

> [!NOTE]
> <span data-ttu-id="3c14e-168">Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3c14e-168">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="3c14e-169">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="3c14e-169">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="3c14e-170">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="3c14e-170">What's changed</span></span>
* <span data-ttu-id="3c14e-171">Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="3c14e-171">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- IMAGES -->
[TransformSitePHPUI]: ./media/web-sites-transform-extend/TransformSitePHPUI.png
[TransformSiteSolEx]: ./media/web-sites-transform-extend/TransformSiteSolEx.png

