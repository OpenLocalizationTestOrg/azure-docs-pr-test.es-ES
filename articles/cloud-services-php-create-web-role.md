---
title: aaaCreate Azure roles web y de trabajo para PHP | Documentos de Microsoft
description: "Una guía toocreating PHP roles web y de trabajo en un servicio de nube de Azure y la configuración en tiempo de ejecución PHP de Hola."
services: 
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9f7ccda0-bd96-4f7b-a7af-fb279a9e975b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 04a6e8c9c379cb0f854645941b6bc7d614bb91f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-php-web-and-worker-roles"></a>¿Cómo toocreate roles de web y de trabajo PHP
## <a name="overview"></a>Información general
Esta guía le mostrará cómo los roles de trabajador o web PHP toocreate en un entorno de desarrollo de Windows, elegir una versión específica de PHP Hola "integradas" versiones disponibles, cambiar la configuración de PHP hello, habilitar extensiones y por último, implementar tooAzure. También se describe cómo tooconfigure un rol web o trabajo toouse un tiempo de ejecución PHP (con configuración personalizada y extensiones) proporcionada por usted.

## <a name="what-are-php-web-and-worker-roles"></a>¿Qué son los roles web y de trabajo de PHP?
Azure ofrece tres modelos de proceso para la ejecución de aplicaciones: Servicio de aplicaciones de Azure, Máquinas virtuales de Azure y Servicios en la nube de Azure. Los tres modelos admiten PHP. Servicios en la nube, que incluye roles web y de trabajo, ofrece el modelo *Plataforma como servicio (PaaS)*. Dentro de un servicio de nube, un rol web proporciona un sitio web de Internet Information Services (IIS) dedicado las aplicaciones de servidor toohost front-end web. Un rol de trabajo puede ejecutar tareas asincrónicas, de ejecución prolongada o perpetuas, independientes de la entrada o la interacción del usuario.

Para más información sobre estas opciones, consulte [Cálculo de las opciones de hospedaje proporcionadas por Azure](cloud-services/cloud-services-choose-me.md).

## <a name="download-hello-azure-sdk-for-php"></a>Descargar hello Azure SDK para PHP
Hola [Azure SDK para PHP] consta de varios componentes. Este artículo utiliza dos de ellos: PowerShell de Azure y Hola emuladores de Azure. Estos dos componentes se pueden instalar a través de hello instalador de plataforma Web de Microsoft. Para obtener más información, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).

## <a name="create-a-cloud-services-project"></a>de un proyecto de servicio en la nube
Hola primer paso para crear un rol de trabajo o web PHP es toocreate un proyecto de servicio de Azure. un proyecto de servicio de Azure actúa como un contenedor lógico para los roles de web y de trabajo y que contiene el proyecto de hello [(.csdef) de la definición del servicio] y [configuración del servicio (.cscfg)] archivos.

toocreate un nuevo proyecto de servicio de Azure, ejecute Azure PowerShell como administrador y ejecute el siguiente comando de hello:

    PS C:\>New-AzureServiceProject myProject

Este comando crea un nuevo directorio (`myProject`) toowhich puede agregar los roles web y de trabajo.

## <a name="add-php-web-or-worker-roles"></a>de roles web y de trabajo de PHP
tooadd un proyecto tooa de rol de web PHP, ejecute hello siguiente comando desde dentro del directorio raíz del proyecto de hello:

    PS C:\myProject> Add-AzurePHPWebRole roleName

Para un rol de trabajo, use este comando:

    PS C:\myProject> Add-AzurePHPWorkerRole roleName

> [!NOTE]
> Hola `roleName` parámetro es opcional. Si se omite, se generará automáticamente el nombre del rol de Hola. primer rol de web Hola creado será `WebRole1`, hello en segundo lugar será `WebRole2`, y así sucesivamente. primer rol de trabajo Hola creado será `WorkerRole1`, hello en segundo lugar será `WorkerRole2`, y así sucesivamente.
>
>

## <a name="specify-hello-built-in-php-version"></a>Especificar versión PHP integrado Hola
Cuando se agrega un proyecto PHP tooa de rol de trabajo o web, archivos de configuración del proyecto de Hola se modifican para que PHP se instalará en cada instancia de trabajador o web de la aplicación cuando se implementa. versión de hello toosee de PHP que se instalará de forma predeterminada, ejecute el siguiente comando de hello:

    PS C:\myProject> Get-AzureServiceProjectRoleRuntime

Hello salida del comando hello anterior tendrá un aspecto similar toowhat se muestra a continuación. En este ejemplo, Hola `IsDefault` marca se establece demasiado`true` para PHP 5.3.17, que indica que será versión PHP predeterminado Hola instalada.

```
Runtime Version     PackageUri                      IsDefault
------- -------     ----------                      ---------
Node 0.6.17         http://nodertncu.blob.core...   False
Node 0.6.20         http://nodertncu.blob.core...   True
Node 0.8.4          http://nodertncu.blob.core...   False
IISNode 0.1.21      http://nodertncu.blob.core...   True
Cache 1.8.0         http://nodertncu.blob.core...   True
PHP 5.3.17          http://nodertncu.blob.core...   True
PHP 5.4.0           http://nodertncu.blob.core...   False
```

Puede establecer Hola PHP en tiempo de ejecución versión tooany de versiones PHP de Hola que aparecen. Por ejemplo, versión de PHP de tooset Hola (para un rol con nombre hello `roleName`) too5.4.0, Hola de uso siguiente comando:

    PS C:\myProject> Set-AzureServiceProjectRole roleName php 5.4.0

> [!NOTE]
> Versiones PHP disponibles pueden cambiar en futuras Hola.
>
>

## <a name="customize-hello-built-in-php-runtime"></a>Personalizar el tiempo de ejecución de hello integrado PHP
Tiene un control completo sobre la configuración de Hola de en tiempo de ejecución PHP de Hola que se instala al seguir los pasos de hello anteriormente, incluida la modificación de `php.ini` configuración y habilitación de extensiones.

toocustomize Hola integrado en tiempo de ejecución PHP, siga estos pasos:

1. Agregar una nueva carpeta denominada `php`, toohello `bin` directorio de su rol web. Para que un rol de trabajo, debe agregarlo directorio de raíz del rol toohello.
2. Hola `php` carpeta, cree otra carpeta denominada `ext`. Ponga ningún `.dll` archivos de extensión (p. ej., `php_mongo.dll`) que desea tooenable en esta carpeta.
3. Agregar un `php.ini` archivo toohello `php` carpeta. Habilite todas las extensiones personalizadas y defina todas las directivas de PHP en este archivo. Por ejemplo, si deseara tooturn `display_errors` en y habilitar hello `php_mongo.dll` extensión, el contenido de Hola de su `php.ini` archivo sería como sigue:

        display_errors=On
        extension=php_mongo.dll

> [!NOTE]
> Cualquier configuración que no establece explícitamente en hello `php.ini` archivo que proporcione automáticamente will establecerse como valores predeterminados de tootheir. Sin embargo, tenga en cuenta que puede agregar un archivo `php.ini` completo.
>
>

## <a name="use-your-own-php-runtime"></a>del tiempo de ejecución de PHP propio
En algunos casos, en lugar de seleccionar un tiempo de ejecución PHP integrado y configurarlo como se describió anteriormente, puede que desee tooprovide su propio tiempo de ejecución PHP. Por ejemplo, puede usar Hola mismo en tiempo de ejecución PHP en un rol web o de trabajo que se utiliza en el entorno de desarrollo. Esto hace más fácil tooensure esa aplicación hello no cambiará el comportamiento en el entorno de producción.

### <a name="configure-a-web-role-toouse-your-own-php-runtime"></a>Configurar una toouse de rol web en su propio tiempo de ejecución PHP
tooconfigure un toouse de rol web un tiempo de ejecución PHP que proporcione, siga estos pasos:

1. Cree un proyecto del servicio de Azure y agregue un rol web de PHP según se describe anteriormente en este tema.
2. Crear un `php` carpeta Hola `bin` carpeta que se encuentra en el directorio de raíz del rol web y, a continuación, agregue el toohello de tiempo de ejecución (todos los archivos binarios, archivos de configuración, las subcarpetas, etc.) de PHP `php` carpeta.
3. (OPCIONAL) Si el tiempo de ejecución PHP usa hello [Microsoft Drivers for PHP para SQL Server][sqlsrv drivers], necesitará tooconfigure su tooinstall de rol web [SQL Server Native Client 2012] [ sql native client] cuando se aprovisiona. toodo, agregar hello [sqlncli.msi x64 installer] toohello `bin` carpeta en el directorio de raíz del rol web. script de inicio de Hola se describe en el paso siguiente Hola ejecutará en modo silencioso instalador hello cuando se aprovisiona el rol de Hola. Si el tiempo de ejecución PHP no usa Hola Microsoft Drivers for PHP para SQL Server, puede quitar Hola siguientes línea de script de Hola mostrado en el paso siguiente de hello:

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. Defina una tarea de inicio que configura [Internet Information Services (IIS)] [ iis.net] toouse solicita su toohandle en tiempo de ejecución PHP para `.php` páginas. toodo, abra hello `setup_web.cmd` archivo (Hola `bin` archivo del directorio de raíz del rol web) en un editor de texto y reemplazar su contenido con Hola después de la secuencia de comandos:

    ```cmd
    @ECHO ON
    cd "%~dp0"

    if "%EMULATED%"=="true" exit /b 0

    msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES

    SET PHP_FULL_PATH=%~dp0php\php-cgi.exe
    SET NEW_PATH=%PATH%;%RoleRoot%\base\x86

    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%',maxInstances='12',idleTimeout='60000',activityTimeout='3600',requestTimeout='60000',instanceMaxRequests='10000',protocol='NamedPipe',flushNamedPipe='False']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%'].environmentVariables.[name='PATH',value='%NEW_PATH%']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%'].environmentVariables.[name='PHP_FCGI_MAX_REQUESTS',value='10000']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/handlers /+"[name='PHP',path='*.php',verb='GET,HEAD,POST',modules='FastCgiModule',scriptProcessor='%PHP_FULL_PATH%',resourceType='Either',requireAccess='Script']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /"[fullPath='%PHP_FULL_PATH%'].queueLength:50000"
    ```
5. Agregue el directorio raíz de aplicación archivos tooyour del rol web. Este será el directorio raíz del servidor de hello web.
6. Publicar su aplicación, como se describe en hello [publicar su aplicación](#publish-your-application) sección más adelante.

> [!NOTE]
> Hola `download.ps1` secuencia de comandos (Hola `bin` carpeta del directorio de raíz del rol web Hola) se pueden eliminar después de seguir los pasos de hello descritos anteriormente para usar su propio tiempo de ejecución PHP.
>
>

### <a name="configure-a-worker-role-toouse-your-own-php-runtime"></a>Configurar una toouse de rol de trabajo en su propio tiempo de ejecución PHP
tooconfigure un toouse de rol de trabajo un tiempo de ejecución PHP que proporcione, siga estos pasos:

1. Cree un proyecto del servicio de Azure y agregue un rol de trabajo de PHP según se describe anteriormente en este tema.
2. Crear un `php` carpeta en el directorio de raíz del rol de trabajo de hello y, a continuación, agregue el toohello de tiempo de ejecución (todos los archivos binarios, archivos de configuración, las subcarpetas, etc.) de PHP `php` carpeta.
3. (OPCIONAL) Si usa el tiempo de ejecución PHP [Microsoft Drivers for PHP para SQL Server][sqlsrv drivers], necesitará tooconfigure su tooinstall de rol de trabajo [SQL Server Native Client 2012] [ sql native client] cuando se aprovisiona. toodo, agregar hello [sqlncli.msi x64 installer] directorio de raíz del rol de trabajo toohello. script de inicio de Hola se describe en el paso siguiente Hola ejecutará en modo silencioso instalador hello cuando se aprovisiona el rol de Hola. Si el tiempo de ejecución PHP no usa Hola Microsoft Drivers for PHP para SQL Server, puede quitar Hola siguientes línea de script de Hola mostrado en el paso siguiente de hello:

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. Defina una tarea de inicio que agrega el `php.exe` variable de entorno de ruta de acceso del rol de trabajo ejecutable toohello cuando se aprovisiona el rol de Hola. toodo, abra hello `setup_worker.cmd` de archivos (en el directorio de raíz del rol de trabajo de Hola) en un editor de texto y reemplace su contenido con hello siguiente secuencia de comandos:

    ```cmd
    @echo on

    cd "%~dp0"

    echo Granting permissions for Network Service toohello web root directory...
    icacls ..\ /grant "Network Service":(OI)(CI)W
    if %ERRORLEVEL% neq 0 goto error
    echo OK

    if "%EMULATED%"=="true" exit /b 0

    msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES

    setx Path "%PATH%;%~dp0php" /M

    if %ERRORLEVEL% neq 0 goto error

    echo SUCCESS
    exit /b 0

    :error

    echo FAILED
    exit /b -1
    ```
5. Agregue el directorio raíz de la aplicación archivos tooyour del rol de trabajo.
6. Publicar su aplicación, como se describe en hello [publicar su aplicación](#publish-your-application) sección más adelante.

## <a name="run-your-application-in-hello-compute-and-storage-emulators"></a>Ejecutar la aplicación en hello emuladores de proceso y almacenamiento
Hello emuladores de Azure proporcionan un entorno local en el que puede probar la aplicación de Azure antes de implementarla en la nube toohello. Hay algunas diferencias entre los emuladores de Hola y Hola entorno de Azure. toounderstand esto mejor, vea [usar el emulador de almacenamiento de Azure de Hola para desarrollo y pruebas](storage/common/storage-use-emulator.md).

Tenga en cuenta que debe tener PHP había instalado localmente emulador de proceso de toouse Hola. emulador de proceso de Hello usará su local toorun de instalación de PHP la aplicación.

ejecutar el proyecto en emuladores de hello, de toorun Hola siguiente comando desde el directorio raíz de su proyecto:

    PS C:\MyProject> Start-AzureEmulator

Verá toothis similar de salida:

    Creating local package...
    Starting Emulator...
    Role is running at http://127.0.0.1:81
    Started

Puede ver la aplicación que se ejecuta en el emulador de hello, abra un explorador web y exploración toohello dirección local se muestra en la salida de hello (`http://127.0.0.1:81` en la salida de ejemplo de Hola anterior).

emuladores de hello toostop, ejecute este comando:

    PS C:\MyProject> Stop-AzureEmulator

## <a name="publish-your-application"></a>Publicación de la aplicación
toopublish la aplicación, necesita toofirst importar la configuración de publicación mediante el uso de hello [importación-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) cmdlet. A continuación, puede publicar su aplicación mediante el uso de hello [AzureServiceProject publicar](https://msdn.microsoft.com/library/azure/dn495166.aspx) cmdlet. Para obtener información acerca de la firma, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información, vea hello [Centro para desarrolladores de PHP](/develop/php/).

[Azure SDK para PHP]: /develop/php/common-tasks/download-php-sdk/
[install ps and emulators]: http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409
[(.csdef) de la definición del servicio]: http://msdn.microsoft.com/library/windowsazure/ee758711.aspx
[configuración del servicio (.cscfg)]: http://msdn.microsoft.com/library/windowsazure/ee758710.aspx
[iis.net]: http://www.iis.net/
[sql native client]: http://msdn.microsoft.com/sqlserver/aa937733.aspx
[sqlsrv drivers]: http://php.net/sqlsrv
[sqlncli.msi x64 installer]: http://go.microsoft.com/fwlink/?LinkID=239648
