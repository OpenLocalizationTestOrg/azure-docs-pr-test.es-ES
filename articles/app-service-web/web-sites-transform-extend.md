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
# <a name="azure-app-service-web-app-advanced-config-and-extensions"></a>Configuración avanzada y extensiones de aplicación web del Servicio de aplicaciones de Azure
Mediante el uso de [transformación del documento XML](http://msdn.microsoft.com/library/dd465326.aspx) declaraciones (XDT), puede transformar hello [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) archivo en la aplicación web en el servicio de aplicaciones de Azure. También puede utilizar XDT declaraciones tooadd las extensiones privadas tooenable web personalizado aplicación acciones de administración. Este artículo incluye una extensión de aplicación web del administrador PHP de ejemplo que habilita la administración de la configuración de PHP a través de una interfaz web.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a id="transform"></a>Configuración avanzada mediante ApplicationHost.config
Hola plataforma de servicio de aplicaciones proporciona flexibilidad y control para la configuración de aplicación web. Aunque el archivo de configuración ApplicationHost.config de IIS estándar hello no está disponible para ser editados directamente en el servicio de aplicaciones, plataforma hello es compatible con un modelo de transformación ApplicationHost.config declarativo basado en XML documento transformación (XDT).

tooleverage esta funcionalidad de transformación, puede crear un archivo ApplicationHost.xdt con XDT contenido y coloque en la raíz del sitio (d:\home\site) Hola Hola [Kudu consola](https://github.com/projectkudu/kudu/wiki/Kudu-console). Puede necesitar toorestart hello Web App para cambios tootake efecto.

Hola después applicationHost.xdt ejemplo muestra cómo tooadd una tooa de variable de entorno personalizado nuevo web aplicación que use PHP 5.4.

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

Un archivo de registro con detalles y el estado de transformación está disponible desde la raíz de hello FTP en LogFiles\Transform.

Para ejemplos adicionales, vea [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).

**Nota:**<br />
Elementos de lista de Hola de módulos en `system.webServer` no se puede quitar o reordenar, pero la lista de toohello adiciones son posibles.

## <a id="extend"></a> Ampliación de la aplicación web
### <a id="overview"></a> Información general de las extensiones de aplicación web privada
El Servicio de aplicaciones es compatible con extensiones de aplicación web como punto de extensibilidad para acciones administrativas. De hecho, algunas características de la plataforma del Servicio de aplicaciones se implementan como extensiones preinstaladas. Mientras no se puede modificar preinstalada platform extensions: Hola, puede crear y configurar las extensiones privadas para su propia aplicación web. Esta funcionalidad también se basa en declaraciones XDT. pasos clave de Hola para crear una extensión de la aplicación web privada son siguientes de hello:

1. **Contenido**de la extensión de la aplicación web: crear todas las aplicaciones web compatibles con el Servicio de aplicaciones
2. **Declaración**de la extensión de la aplicación web: crear una aplicación ApplicationHost.xdt
3. Extensión de la aplicación Web **implementación**: coloque el contenido en la carpeta SiteExtensions de hello en`root`

Los vínculos internos de la aplicación web de hello deben apuntar tooa ruta de acceso relativa toohello ruta de la aplicación especificada en el archivo de hello ApplicationHost.xdt. Cualquier archivo de cambio toohello ApplicationHost.xdt requiere un reciclaje de aplicación web.

**Nota**: la información adicional para estos elementos clave se encuentra disponible en [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).

Un ejemplo detallado es tooillustrate incluye Hola pasos para crear y habilitar una extensión de la aplicación web privada. Hola código fuente de ejemplo de Hola a PHP Manager que se indica a continuación puede descargarse desde [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).

### <a id="SiteSample"></a> Ejemplo de extensión de aplicación web:
PHP Manager es una extensión de la aplicación web que permite a los administradores de aplicación de web tooeasily ver y configura sus opciones de PHP con una interfaz web en lugar de tener los archivos .ini de toomodify PHP directamente. Los archivos de configuración comunes para PHP incluyen archivo php.ini de hello ubicado en archivos de programa y Hola. archivo user.ini ubicado en la carpeta raíz de saludo de la aplicación web. Como archivo php.ini de hello no se puede editar directamente en hello plataforma de servicio de aplicaciones, Hola extensión de PHP Manager utiliza Hola. user.ini archivo tooapply cambios en la configuración.

#### <a id="PHPwebapp"></a>Hola aplicación web PHP Manager
Hola te mostramos Hola portada de hello implementación del Administrador de PHP:

![TransformSitePHPUI][TransformSitePHPUI]

Como puede ver, una extensión de la aplicación web es igual que una aplicación web normal, pero con un archivo ApplicationHost.xdt adicional en hello carpeta de raíz de aplicación web de hello (más detalles sobre el archivo de hello ApplicationHost.xdt están disponibles en la sección siguiente de Hola de este artículo).

Hola extensión de PHP Manager se creó con la plantilla de aplicación Web ASP.NET MVC 4 de Visual Studio Hola. Hello siguiente vista del explorador de soluciones muestra hello estructura de extensión de PHP Manager Hola.

![TransformSiteSolEx][TransformSiteSolEx]

Hello solo una lógica especial necesaria para E/S de archivo es tooindicate donde hello directorio wwwroot de hello web app se encuentra. Tal y como se muestra de ejemplo de código siguiente, Hola Hola variable de entorno "HOME" indica Hola ruta de acceso de la aplicación web raíz, y se puede construir la ruta de acceso de hello wwwroot anexando "site\wwwroot":

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


Una vez que la ruta de acceso de directorio de hello, puede usar tooread de operaciones de E/S de archivos normales y escribir toofiles.

Un punto de precaución con extensiones de aplicaciones web que se refiere a control de Hola de vínculos internos.  Si tiene los vínculos en los archivos HTML que proporcionan rutas de acceso absolutas toointernal vínculos en la aplicación web, debe asegurarse de que esos vínculos se anteponen con el nombre de extensión como la raíz. Esto es necesario porque la raíz de hello para la extensión es ahora "/`[your-extension-name]`/" en lugar de ser simplemente "/", por lo que cualquier interno vínculos deben actualizarse según corresponda. Por ejemplo, suponga que su código incluye un siguiente de toohello de vínculo:

`"<a href="/Home/Settings">PHP Settings</a>"`

Al vínculo Hola forma parte de una extensión de la aplicación web, vínculo Hola debe estar en hello siguiente forma:

`"<a href="/[your-site-name]/Home/Settings">Settings</a>"`

Puede solucionar este requisito mediante solo Hola a rutas de acceso relativas en su aplicación web, o en el caso de aplicaciones de ASP.NET, mediante el uso de hello `@Html.ActionLink` método que crea vínculos adecuados de Hola para usted.

#### <a id="XDT"></a>archivo de Hello applicationHost.xdt
código de Hello para la extensión de la aplicación web entra en %HOME%\SiteExtensions\[su nombre de extensión]. Llamaremos a esta raíz de la extensión de Hola.  

tooregister la extensión de la aplicación web con el archivo applicationHost.config de hello, necesita un archivo denominado ApplicationHost.xdt en la raíz de la extensión de hello tooplace. contenido de Hola del archivo de hello ApplicationHost.xdt debería ser como sigue:

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

nombre de Hello seleccionado como el nombre de la extensión debe disponer del mismo nombre de hello como la carpeta de raíz de la extensión.

Esto tiene el efecto de Hola de agregar un nuevo toohello de ruta de acceso de aplicación `system.applicationHost` lista de sitios en un sitio SCM Hola. sitio SCM Hello es un extremo de administración de sitio con las credenciales de acceso específico. Tiene la dirección URL de hello `https://[your-site-name].scm.azurewebsites.net`.  

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

### <a id="deploy"></a> Implementación de extensión de aplicación web
tooinstall la extensión de la aplicación web, puede usar FTP toocopy todos los archivos de saludo de su toohello de aplicación web `\SiteExtensions\[your-extension-name]` carpeta de aplicación web de hello en el que se desea la extensión de hello tooinstall.  Ser seguro toocopy hello ApplicationHost.xdt toothis ubicación del archivo también. Reinicie la extensión de Hola de tooenable de aplicación web.

Debe ser capaz de toosee la extensión de la aplicación web en:

`https://[your-site-name].scm.azurewebsites.net/[your-extension-name]`

Tenga en cuenta que Hola que dirección URL es igual que la dirección URL de hello para la aplicación web, salvo que usa HTTPS y contiene ".scm".

Es privada todos los posibles toodisable (no preinstalado) extensiones para la aplicación web durante el desarrollo y las investigaciones mediante la adición de una configuración de la aplicación con la clave de hello `WEBSITE_PRIVATE_EXTENSIONS` y un valor de `0`.

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
> 
> 

## <a name="whats-changed"></a>Lo que ha cambiado
* Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- IMAGES -->
[TransformSitePHPUI]: ./media/web-sites-transform-extend/TransformSitePHPUI.png
[TransformSiteSolEx]: ./media/web-sites-transform-extend/TransformSiteSolEx.png

