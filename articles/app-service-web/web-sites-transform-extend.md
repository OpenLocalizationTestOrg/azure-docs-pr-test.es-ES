---
title: "Configuración avanzada y extensiones de aplicación web del Servicio de aplicaciones de Azure"
description: "Las declaraciones de XML Document Transformation (XDT) se usan para transformar el archivo ApplicationHost.config en su aplicación web del Servicio de aplicaciones de Azure y agregar extensiones privadas para habilitar acciones de administración personalizadas."
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
ms.openlocfilehash: 314d3a954e712b829e7cf5eb37b23b31670f976b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-app-service-web-app-advanced-config-and-extensions"></a><span data-ttu-id="56e86-103">Configuración avanzada y extensiones de aplicación web del Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="56e86-103">Azure App Service web app advanced config and extensions</span></span>
<span data-ttu-id="56e86-104">Con las declaraciones de [XML Document Transformation](http://msdn.microsoft.com/library/dd465326.aspx) (XDT), puede transformar el archivo [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) en su aplicación web de Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="56e86-104">By using [XML Document Transformation](http://msdn.microsoft.com/library/dd465326.aspx) (XDT) declarations, you can transform the [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) file in your web app in Azure App Service.</span></span> <span data-ttu-id="56e86-105">También puede usar las declaraciones XDT a fin de agregar extensiones privadas para habilitar acciones de administración de la aplicación web personalizada.</span><span class="sxs-lookup"><span data-stu-id="56e86-105">You can also use XDT declarations to add private extensions to enable custom web app administration actions.</span></span> <span data-ttu-id="56e86-106">Este artículo incluye una extensión de aplicación web del administrador PHP de ejemplo que habilita la administración de la configuración de PHP a través de una interfaz web.</span><span class="sxs-lookup"><span data-stu-id="56e86-106">This article includes a sample PHP Manager web app extension that enables management of PHP settings through a web interface.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="56e86-107"><a id="transform"></a>Configuración avanzada mediante ApplicationHost.config</span><span class="sxs-lookup"><span data-stu-id="56e86-107"><a id="transform"></a>Advanced configuration through ApplicationHost.config</span></span>
<span data-ttu-id="56e86-108">La plataforma del Servicio de aplicaciones proporciona flexibilidad y control para la configuración de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="56e86-108">The App Service platform provides flexibility and control for web app configuration.</span></span> <span data-ttu-id="56e86-109">Aunque el archivo de configuración ApplicationHost.config de IIS estándar no está disponible para la edición directa en el Servicio de aplicaciones, la plataforma es compatible con un modelo de transformación ApplicationHost.config declarativo basado en XML Document Transformation (XDT).</span><span class="sxs-lookup"><span data-stu-id="56e86-109">Although the standard IIS ApplicationHost.config configuration file is not available for direct editing in App Service, the platform supports a declarative ApplicationHost.config transform model based on XML Document Transformation (XDT).</span></span>

<span data-ttu-id="56e86-110">Para sacar provecho de esta funcionalidad de transformación, cree un archivo ApplicationHost.xdt con contenido XDT y colóquelo en la raíz del sitio (d:\home\site) en la [consola Kudu](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span><span class="sxs-lookup"><span data-stu-id="56e86-110">To leverage this transform functionality, you create an ApplicationHost.xdt file with XDT content and place under the site root (d:\home\site) in the [Kudu Console](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span></span> <span data-ttu-id="56e86-111">Puede que necesite reiniciar la aplicación web para que los cambios surtan efecto.</span><span class="sxs-lookup"><span data-stu-id="56e86-111">You may need to restart the Web App for changes to take effect.</span></span>

<span data-ttu-id="56e86-112">El siguiente ejemplo de applicationHost.xdt muestra cómo agregar una nueva variable de entorno personalizada en una aplicación web que use PHP 5.4.</span><span class="sxs-lookup"><span data-stu-id="56e86-112">The following applicationHost.xdt sample shows how to add a new custom environment variable to a web app that uses PHP 5.4.</span></span>

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

<span data-ttu-id="56e86-113">Hay un archivo de registro con información y estado de trasformación disponible en la raíz del FTP en LogFiles\Transform.</span><span class="sxs-lookup"><span data-stu-id="56e86-113">A log file with transform status and details is available from the FTP root under LogFiles\Transform.</span></span>

<span data-ttu-id="56e86-114">Para ejemplos adicionales, vea [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span><span class="sxs-lookup"><span data-stu-id="56e86-114">For additional samples, see [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span></span>

<span data-ttu-id="56e86-115">**Nota:**</span><span class="sxs-lookup"><span data-stu-id="56e86-115">**Note**</span></span><br />
<span data-ttu-id="56e86-116">Los elementos de la lista de módulos en `system.webServer` no pueden quitarse o reordenarse, aunque sí es posible agregar elementos a la lista.</span><span class="sxs-lookup"><span data-stu-id="56e86-116">Elements from the list of modules under `system.webServer` cannot be removed or reordered, but additions to the list are possible.</span></span>

## <span data-ttu-id="56e86-117"><a id="extend"></a> Ampliación de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="56e86-117"><a id="extend"></a> Extend your web app</span></span>
### <span data-ttu-id="56e86-118"><a id="overview"></a> Información general de las extensiones de aplicación web privada</span><span class="sxs-lookup"><span data-stu-id="56e86-118"><a id="overview"></a> Overview of private web app extensions</span></span>
<span data-ttu-id="56e86-119">El Servicio de aplicaciones es compatible con extensiones de aplicación web como punto de extensibilidad para acciones administrativas.</span><span class="sxs-lookup"><span data-stu-id="56e86-119">App Service supports web app extensions as an extensibility point for administrative actions.</span></span> <span data-ttu-id="56e86-120">De hecho, algunas características de la plataforma del Servicio de aplicaciones se implementan como extensiones preinstaladas.</span><span class="sxs-lookup"><span data-stu-id="56e86-120">In fact, some App Service platform features are implemented as pre-installed extensions.</span></span> <span data-ttu-id="56e86-121">Cuando las extensiones preinstaladas de la plataforma no se puedan modificar, puede crear y configurar extensiones privadas para su propia aplicación web.</span><span class="sxs-lookup"><span data-stu-id="56e86-121">While the pre-installed platform extensions cannot be modified, you can create and configure private extensions for your own web app.</span></span> <span data-ttu-id="56e86-122">Esta funcionalidad también se basa en declaraciones XDT.</span><span class="sxs-lookup"><span data-stu-id="56e86-122">This functionality also relies on XDT declarations.</span></span> <span data-ttu-id="56e86-123">Los pasos clave para la creación de una extensión de la aplicación web privada son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="56e86-123">The key steps for creating a private web app extension are the following:</span></span>

1. <span data-ttu-id="56e86-124">**Contenido**de la extensión de la aplicación web: crear todas las aplicaciones web compatibles con el Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="56e86-124">Web app extension **content**: create any web application supported by App Service</span></span>
2. <span data-ttu-id="56e86-125">**Declaración**de la extensión de la aplicación web: crear una aplicación ApplicationHost.xdt</span><span class="sxs-lookup"><span data-stu-id="56e86-125">Web app extension **declaration**: create an ApplicationHost.xdt file</span></span>
3. <span data-ttu-id="56e86-126">**Implementación** de la extensión de la aplicación web: colocar contenido en la carpeta SiteExtensions en `root`</span><span class="sxs-lookup"><span data-stu-id="56e86-126">Web app extension **deployment**: place content in the SiteExtensions folder under `root`</span></span>

<span data-ttu-id="56e86-127">Los vínculos internos para la aplicación web deben apuntar a una ruta relacionada con la ruta de la aplicación especificada en el archivo ApplicationHost.xdt.</span><span class="sxs-lookup"><span data-stu-id="56e86-127">Internal links for the web app should point to a path relative to the application path specified in the ApplicationHost.xdt file.</span></span> <span data-ttu-id="56e86-128">Cualquier cambio en el archivo ApplicationHost.xdt requiere reciclar la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="56e86-128">Any change to the ApplicationHost.xdt file requires a web app recycle.</span></span>

<span data-ttu-id="56e86-129">**Nota**: la información adicional para estos elementos clave se encuentra disponible en [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span><span class="sxs-lookup"><span data-stu-id="56e86-129">**Note**: Additional information for these key elements is available at [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span></span>

<span data-ttu-id="56e86-130">Se incluye un ejemplo detallado para mostrar los pasos para la creación y habilitación de una extensión de aplicación web privada.</span><span class="sxs-lookup"><span data-stu-id="56e86-130">A detailed example is included to illustrate the steps for creating and enabling a private web app extension.</span></span> <span data-ttu-id="56e86-131">El código fuente para el administrador PHP siguiente puede descargarse en [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span><span class="sxs-lookup"><span data-stu-id="56e86-131">The source code for the PHP Manager example that follows can be downloaded from [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span></span>

### <span data-ttu-id="56e86-132"><a id="SiteSample"></a> Ejemplo de extensión de aplicación web:</span><span class="sxs-lookup"><span data-stu-id="56e86-132"><a id="SiteSample"></a> Web app extension example: PHP Manager</span></span>
<span data-ttu-id="56e86-133">El administrador PHP es una extensión de la aplicación web que permite a los administradores de la aplicación web ver y configurar fácilmente su configuración PHP con una interfaz web en lugar de tener que modificar archivos .ini PHP directamente.</span><span class="sxs-lookup"><span data-stu-id="56e86-133">PHP Manager is a web app extension that allows web app administrators to easily view and configure their PHP settings using a web interface instead of having to modify PHP .ini files directly.</span></span> <span data-ttu-id="56e86-134">Los archivos de configuración comunes para PHP incluyen el archivo php.ini ubicado en Archivos de programa y el archivo .user.ini ubicado en la carpeta raíz de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="56e86-134">Common configuration files for PHP include the php.ini file located under Program Files and the .user.ini file located in the root folder of your web app.</span></span> <span data-ttu-id="56e86-135">Puesto que el archivo php.ini no es directamente editable en la plataforma del Servicio de aplicaciones, la extensión del administrador PHP usa el archivo .user.ini para aplicar los cambios de configuración.</span><span class="sxs-lookup"><span data-stu-id="56e86-135">Since the php.ini file is not directly editable on the App Service platform, the PHP Manager extension uses the .user.ini file to apply setting changes.</span></span>

#### <span data-ttu-id="56e86-136"><a id="PHPwebapp"></a> Aplicación web del administrador PHP</span><span class="sxs-lookup"><span data-stu-id="56e86-136"><a id="PHPwebapp"></a> The PHP Manager web application</span></span>
<span data-ttu-id="56e86-137">A continuación se muestra la página principal de la implementación del administrador PHP:</span><span class="sxs-lookup"><span data-stu-id="56e86-137">The following is the home page of the PHP Manager deployment:</span></span>

![TransformSitePHPUI][TransformSitePHPUI]

<span data-ttu-id="56e86-139">Como puede ver, una extensión de la aplicación web es como una aplicación web normal, pero con un archivo ApplicationHost.xdt adicional situado en la carpeta raíz de la aplicación web (puede encontrar más información sobre el archivo ApplicationHost.xdt disponible en la siguiente sección de este artículo).</span><span class="sxs-lookup"><span data-stu-id="56e86-139">As you can see, a web app extension is just like a regular web application, but with an additional ApplicationHost.xdt file placed in the root folder of the web app (more details about the ApplicationHost.xdt file are available in the next section of this article).</span></span>

<span data-ttu-id="56e86-140">La extensión del administrador PHP se creó mediante la plantilla de la aplicación ASP.NET MVC 4 Web Application de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="56e86-140">The PHP Manager extension was created using the Visual Studio ASP.NET MVC 4 Web Application template.</span></span> <span data-ttu-id="56e86-141">La siguiente vista del Explorador de soluciones muestra la estructura de la extensión del administrador PHP.</span><span class="sxs-lookup"><span data-stu-id="56e86-141">The following view from Solution Explorer shows the structure of the PHP Manager extension.</span></span>

![TransformSiteSolEx][TransformSiteSolEx]

<span data-ttu-id="56e86-143">La única lógica especial necesaria para la E/S del archivo es indicar dónde se encuentra el directorio wwwroot de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="56e86-143">The only special logic needed for file I/O is to indicate where the wwwroot directory of the web app is located.</span></span> <span data-ttu-id="56e86-144">Puesto que se muestra el siguiente ejemplo de código, la variable de entorno "HOME" indica la ruta raíz de la aplicación web y la ruta wwwroot puede construirse anexando "site\wwwroot":</span><span class="sxs-lookup"><span data-stu-id="56e86-144">As the following code example shows, the environment variable "HOME" indicates the web app's root path, and the wwwroot path can be constructed by appending "site\wwwroot":</span></span>

```csharp
/// <summary>
/// Gives the location of the .user.ini file, even if one doesn't exist yet
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


<span data-ttu-id="56e86-145">Una vez que disponga de la ruta de acceso al directorio, puede usar las operaciones de E/S del archivo normal para leer y escribir en los archivos.</span><span class="sxs-lookup"><span data-stu-id="56e86-145">After you have the directory path, you can use regular file I/O operations to read and write to files.</span></span>

<span data-ttu-id="56e86-146">Un punto de advertencia en relación con las extensiones de la aplicación web hace referencia a la administración de los vínculos internos.</span><span class="sxs-lookup"><span data-stu-id="56e86-146">One point of caution with web app extensions regards the handling of internal links.</span></span>  <span data-ttu-id="56e86-147">Si dispone de vínculos en los archivos HTML que proporcionen rutas absolutas a vínculos internos en la aplicación web, debe asegurarse de que esos vínculos se anexen al nombre de extensión como su raíz.</span><span class="sxs-lookup"><span data-stu-id="56e86-147">If you have any links in your HTML files that give absolute paths to internal links on your web app, you must ensure those links are prepended with your extension name as your root.</span></span> <span data-ttu-id="56e86-148">Esto es necesario porque la ruta del sitio para la extensión es ahora "/`[your-extension-name]`/" en lugar de solo "/", por lo que los vínculos internos deben actualizarse como corresponda.</span><span class="sxs-lookup"><span data-stu-id="56e86-148">This is needed because the root for your extension is now "/`[your-extension-name]`/" rather than being just "/", so any internal links must be updated accordingly.</span></span> <span data-ttu-id="56e86-149">Por ejemplo, suponga que el código incluye un vínculo a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="56e86-149">For example, suppose your code includes a link to the following:</span></span>

`"<a href="/Home/Settings">PHP Settings</a>"`

<span data-ttu-id="56e86-150">Cuando el vínculo forma parte de una extensión de la aplicación web, el vínculo debe tener la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="56e86-150">When the link is part of a web app extension, the link must be in the following form:</span></span>

`"<a href="/[your-site-name]/Home/Settings">Settings</a>"`

<span data-ttu-id="56e86-151">Puede satisfacer este requisito usando solo rutas relativas en la aplicación web o, en caso de aplicaciones ASP.NET, usando el método `@Html.ActionLink` que crea los vínculos apropiados para usted.</span><span class="sxs-lookup"><span data-stu-id="56e86-151">You can work around this requirement by either using only relative paths within your web application, or in the case of ASP.NET applications, by using the `@Html.ActionLink` method which creates the appropriate links for you.</span></span>

#### <span data-ttu-id="56e86-152"><a id="XDT"></a> Archivo applicationHost.xdt</span><span class="sxs-lookup"><span data-stu-id="56e86-152"><a id="XDT"></a> The applicationHost.xdt file</span></span>
<span data-ttu-id="56e86-153">El código de la extensión de la aplicación web se encuentra en %HOME%\SiteExtensions\[nombre-extensión].</span><span class="sxs-lookup"><span data-stu-id="56e86-153">The code for your web app extension goes under %HOME%\SiteExtensions\[your-extension-name].</span></span> <span data-ttu-id="56e86-154">Llamaremos a esto raíz de extensión.</span><span class="sxs-lookup"><span data-stu-id="56e86-154">We'll call this the extension root.</span></span>  

<span data-ttu-id="56e86-155">Para registrar la extensión de la aplicación web con el archivo applicationHost.config, tendrá que colocar un archivo denominado ApplicationHost.xdt en la raíz de extensión.</span><span class="sxs-lookup"><span data-stu-id="56e86-155">To register your web app extension with the applicationHost.config file, you need to place a file called ApplicationHost.xdt in the extension root.</span></span> <span data-ttu-id="56e86-156">El contenido del archivo ApplicationHost.xdt debe ser el siguiente:</span><span class="sxs-lookup"><span data-stu-id="56e86-156">The content of the ApplicationHost.xdt file should be as follows:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.applicationHost>
    <sites>
      <site name="%XDT_SCMSITENAME%" xdt:Locator="Match(name)">
        <!-- NOTE: Add your extension name in the application paths below -->
        <application path="/[your-extension-name]" xdt:Locator="Match(path)" xdt:Transform="Remove" />
        <application path="/[your-extension-name]" applicationPool="%XDT_APPPOOLNAME%" xdt:Transform="Insert">
          <virtualDirectory path="/" physicalPath="%XDT_EXTENSIONPATH%" />
        </application>
      </site>
    </sites>
  </system.applicationHost>
</configuration>
```

<span data-ttu-id="56e86-157">El nombre que seleccione como nombre de extensión debe tener el mismo nombre que la carpeta raíz de extensión.</span><span class="sxs-lookup"><span data-stu-id="56e86-157">The name you select as your extension name should have the same name as your extension root folder.</span></span>

<span data-ttu-id="56e86-158">Esto provoca la suma de una nueva ruta de aplicación a la lista de sitios `system.applicationHost` en el sitio SCM.</span><span class="sxs-lookup"><span data-stu-id="56e86-158">This has the effect of adding a new application path to the `system.applicationHost` sites list under the SCM site.</span></span> <span data-ttu-id="56e86-159">El sitio SCM es un punto final de administración que especifica credenciales de acceso.</span><span class="sxs-lookup"><span data-stu-id="56e86-159">The SCM site is a site administration end point with specific access credentials.</span></span> <span data-ttu-id="56e86-160">Dispone de la dirección URL `https://[your-site-name].scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="56e86-160">It has the URL `https://[your-site-name].scm.azurewebsites.net`.</span></span>  

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
      <!-- Note the custom changes that go here -->
      <application path="/[your-extension-name]" applicationPool="[your-website]">
        <virtualDirectory path="/" physicalPath="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\SiteExtensions\[your-extension-name]" />
      </application>
    </site>
  </sites>
  ... 
</system.applicationHost>
```

### <span data-ttu-id="56e86-161"><a id="deploy"></a> Implementación de extensión de aplicación web</span><span class="sxs-lookup"><span data-stu-id="56e86-161"><a id="deploy"></a> Web app extension deployment</span></span>
<span data-ttu-id="56e86-162">Para instalar la extensión de la aplicación web, puede usar FTP para copiar todos los archivos de la aplicación web en la carpeta `\SiteExtensions\[your-extension-name]` de la aplicación web en la que desea instalar la extensión.</span><span class="sxs-lookup"><span data-stu-id="56e86-162">To install your web app extension, you can use FTP to copy all the files of your web application to the `\SiteExtensions\[your-extension-name]` folder of the web app on which you want to install the extension.</span></span>  <span data-ttu-id="56e86-163">Asegúrese de copiar el archivo ApplicationHost.xdt en la ubicación también.</span><span class="sxs-lookup"><span data-stu-id="56e86-163">Be sure to copy the ApplicationHost.xdt file to this location as well.</span></span> <span data-ttu-id="56e86-164">Reinicie la aplicación web para habilitar la extensión.</span><span class="sxs-lookup"><span data-stu-id="56e86-164">Restart your web app to enable the extension.</span></span>

<span data-ttu-id="56e86-165">Debe poder ver la extensión de la aplicación web en:</span><span class="sxs-lookup"><span data-stu-id="56e86-165">You should be able to see your web app extension at:</span></span>

`https://[your-site-name].scm.azurewebsites.net/[your-extension-name]`

<span data-ttu-id="56e86-166">Tenga en cuenta que el aspecto de la dirección URL es parecido al de la dirección URL de su aplicación web, con la diferencia de que usa HTTPS y contiene ".scm".</span><span class="sxs-lookup"><span data-stu-id="56e86-166">Note that the URL looks just like the URL for your web app, except that it uses HTTPS and contains ".scm".</span></span>

<span data-ttu-id="56e86-167">Es posible deshabilitar todas las extensiones (no preinstaladas) privadas para su aplicación web durante el desarrollo y las investigaciones agregando una configuración de la aplicación con la clave `WEBSITE_PRIVATE_EXTENSIONS` y un valor de `0`.</span><span class="sxs-lookup"><span data-stu-id="56e86-167">It is possible to disable all private (not pre-installed) extensions for your web app during development and investigations by adding an app settings with the key `WEBSITE_PRIVATE_EXTENSIONS` and a value of `0`.</span></span>

> [!NOTE]
> <span data-ttu-id="56e86-168">Si desea empezar a trabajar con el Servicio de aplicaciones de Azure antes de inscribirse para abrir una cuenta de Azure, vaya a [App Service](https://azure.microsoft.com/try/app-service/), donde podrá crear inmediatamente una aplicación web de inicio de corta duración en el Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="56e86-168">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="56e86-169">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="56e86-169">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="56e86-170">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="56e86-170">What's changed</span></span>
* <span data-ttu-id="56e86-171">Para obtener una guía del cambio de Websites a App Service, consulte: [Azure App Service y su impacto en los servicios de Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="56e86-171">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- IMAGES -->
[TransformSitePHPUI]: ./media/web-sites-transform-extend/TransformSitePHPUI.png
[TransformSiteSolEx]: ./media/web-sites-transform-extend/TransformSiteSolEx.png

