---
title: aaaInstall .NET en las funciones de servicios de nube de Azure | Documentos de Microsoft
description: "En este artículo se describe cómo toomanually instalar .NET Framework hello en los roles de web y de trabajo de servicio de nube"
services: cloud-services
documentationcenter: .net
author: thraka
manager: timlt
editor: 
ms.assetid: 8d1243dc-879c-4d1f-9ed0-eecd1f6a6653
ms.service: cloud-services
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: adegeo
ms.openlocfilehash: 45f0f30221292f98c591511b091b02ebe1c1272c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-net-on-azure-cloud-services-roles"></a>Instalación de .NET en roles de Azure Cloud Services
Este artículo describe cómo tooinstall las versiones de .NET Framework que no vienen con Hola SO invitado de Azure. Puede usar .NET en hello SO invitado tooconfigure sus roles web y de trabajo del servicio de nube.

Por ejemplo, puede instalar .NET 4.6.1 en hello familia del SO invitado 4, que no procede con cualquier versión de .NET 4.6. (Hola familia del SO invitado 5 incluyen .NET 4.6). Para obtener información más reciente de hello en hello versiones SO invitado de Azure, consulte hello [noticias de la versión de SO invitado de Azure](cloud-services-guestos-update-matrix.md). 

>[!IMPORTANT]
>Hello Azure SDK 2.9 contiene una restricción sobre la implementación de .NET 4.6 en la familia de SO invitado de hello 4 o versiones anterior. Corrección de restricción de hello está disponible en hello [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) sitio.

tooinstall .NET en sus roles web y de trabajo, incluye el instalador web de hello .NET como parte de su proyecto de servicio de nube. Inicie el instalador de hello como parte de las tareas de inicio del rol de Hola. 

## <a name="add-hello-net-installer-tooyour-project"></a>Agregar proyecto de tooyour de instalador de .NET de Hola
instalador de toodownload hello web Hola .NET Framework, elegir versión de Hola que desea tooinstall:

* [Instalador web de .NET 4.7](http://go.microsoft.com/fwlink/?LinkId=825298)
* [Instalador web de .NET 4.6.1](http://go.microsoft.com/fwlink/?LinkId=671729)

instalador de hello tooadd para un *web* rol:
  1. En el **Explorador de soluciones**, en **Roles** del proyecto de servicio en la nube, haga clic con el botón derecho en el rol *web* y seleccione **Agregar** > **Nueva carpeta**. Cree una carpeta llamada **bin**.
  2. Haga clic en la carpeta bin de Hola y seleccione **agregar** > **elemento existente**. Seleccione el instalador de .NET de Hola y Agregar carpeta bin de toohello.
  
instalador de hello tooadd para un *trabajo* rol:
* Haga clic con el botón derecho en el rol de *trabajo* y seleccione **Agregar** > **Elemento existente**. Seleccione el instalador de .NET de Hola y agregar rol toohello. 

Cuando se agregan archivos en esta carpeta de contenido de rol de manera toohello, estas se agregan automáticamente tooyour paquete de servicio de nube. Hola archivos pasan a ser implementado tooa ubicación coherente en la máquina virtual de Hola. Repita este proceso para cada rol web y de trabajo en el servicio de nube para que todos los roles tienen una copia del instalador de Hola.

> [!NOTE]
> Debe instalar .NET 4.6.1 en su rol de servicio en la nube, incluso si la aplicación tiene como destino .NET 4.6. Hola SO invitado incluye Base de conocimiento de hello [actualizar 3098779](https://support.microsoft.com/kb/3098779) y [actualizar 3097997](https://support.microsoft.com/kb/3097997). Pueden producirse problemas al ejecutar las aplicaciones de .NET si está instalado .NET 4.6 encima de las actualizaciones de Base de conocimiento de Hola. tooavoid estos problemas, instale .NET 4.6.1 en lugar de la versión 4.6. Para obtener más información, vea hello [el artículo de Knowledge Base 3118750](https://support.microsoft.com/kb/3118750).
> 
> 

![Contenidos de rol con archivos de instalador][1]

## <a name="define-startup-tasks-for-your-roles"></a>Definir las tareas de inicio para los roles
Puede utilizar operaciones de tooperform de tareas de inicio antes de que se inicia un rol. Instalar Hola .NET Framework como parte de la tarea de inicio de hello garantiza framework Hola está instalado antes de que se ejecute cualquier código de aplicación. Para más información sobre de las tareas de inicio, consulte [Ejecución de tareas de inicio en Azure](cloud-services-startup-tasks.md). 

1. Agregar Hola siguiente contenido toohello el archivo ServiceDefinition.csdef bajo hello **WebRole** o **WorkerRole** nodo para todos los roles:
   
    ```xml
    <LocalResources>
      <LocalStorage name="NETFXInstall" sizeInMB="1024" cleanOnRoleRecycle="false" />
    </LocalResources>    
    <Startup>
      <Task commandLine="install.cmd" executionContext="elevated" taskType="simple">
        <Environment>
          <Variable name="PathToNETFXInstall">
            <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='NETFXInstall']/@path" />
          </Variable>
          <Variable name="ComputeEmulatorRunning">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
        </Environment>
      </Task>
    </Startup>
    ```
   
    Hello configuración anterior ejecuta comandos de consola de hello `install.cmd` con tooinstall de privilegios de administrador Hola .NET Framework. configuración de Hello también crea un **LocalStorage** elemento denominado **NETFXInstall**. script de inicio de Hello establece toouse de la carpeta temporal de hello este recurso de almacenamiento local. 
    
    > [!IMPORTANT]
    > tooensure corregir instalación de framework hello, tamaño del conjunto de Hola de este recurso tooat menos 1024 MB.
    
    Para más información sobre las tareas de inicio, consulte las [tareas de inicio comunes de Azure Cloud Services](cloud-services-startup-tasks-common.md).

2. Cree un archivo denominado **install.cmd** y agregue la siguiente Hola instala archivos de script toohello.

    script de Hola comprueba si versión especificada de Hola de hello .NET Framework ya está instalado en el equipo de hello consultando el registro de hello. Si no está instalada la versión de .NET de hello, se abre el instalador web de .NET de Hola. toohelp solucionar los problemas, el script de Hola registra todas las actividades toohello archivo startuptasklog-(fecha y hora actuales) .txt que se almacena en **InstallLogs** almacenamiento local.

    > [!IMPORTANT]
    > Utilice un editor de texto básico como el Bloc de notas de Windows toocreate Hola install.cmd archivo. Si utiliza Visual Studio toocreate un archivo de texto y cambie Hola extensión too.cmd, archivo hello todavía podría contener una marca de orden de bytes UTF-8. Esta marca puede producir un error cuando se ejecuta la primera línea del script de Hola de Hola. tooavoid este error, asegúrese de primera línea de Hola de hello una REM (instrucción) que se puede omitir por el procesamiento de orden de bytes de Hola de secuencias de comandos. 
    > 
    >
   
    ```cmd
    REM Set hello value of netfx tooinstall appropriate .NET Framework. 
    REM ***** tooinstall .NET 4.5.2 set hello variable netfx too"NDP452" *****
    REM ***** tooinstall .NET 4.6 set hello variable netfx too"NDP46" *****
    REM ***** tooinstall .NET 4.6.1 set hello variable netfx too"NDP461" *****
    REM ***** tooinstall .NET 4.6.2 set hello variable netfx too"NDP462" *****
    REM ***** tooinstall .NET 4.7 set hello variable netfx too"NDP47" *****
    set netfx="NDP47"

    REM ***** Set script start timestamp *****
    set timehour=%time:~0,2%
    set timestamp=%date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2%
    set "log=install.cmd started %timestamp%."

    REM ***** Exit script if running in Emulator *****
    if %ComputeEmulatorRunning%=="true" goto exit

    REM ***** Needed toocorrectly install .NET 4.6.1, otherwise you may see an out of disk space error *****
    set TMP=%PathToNETFXInstall%
    set TEMP=%PathToNETFXInstall%

    REM ***** Setup .NET filenames and registry keys *****
    if %netfx%=="NDP47" goto NDP47
    if %netfx%=="NDP462" goto NDP462
    if %netfx%=="NDP461" goto NDP461
    if %netfx%=="NDP46" goto NDP46
        set "netfxinstallfile=NDP452-KB2901954-Web.exe"
        set netfxregkey="0x5cbf5"
        goto logtimestamp

    :NDP46
    set "netfxinstallfile=NDP46-KB3045560-Web.exe"
    set netfxregkey="0x6004f"
    goto logtimestamp

    :NDP461
    set "netfxinstallfile=NDP461-KB3102438-Web.exe"
    set netfxregkey="0x6040e"
    goto logtimestamp

    :NDP462
    set "netfxinstallfile=NDP462-KB3151802-Web.exe"
    set netfxregkey="0x60632"

    :NDP47
    set "netfxinstallfile=NDP47-KB3186500-Web.exe"
    set netfxregkey="0x707FE"

    :logtimestamp
    REM ***** Setup LogFile with timestamp *****
    md "%PathToNETFXInstall%\log"
    set startuptasklog="%PathToNETFXInstall%log\startuptasklog-%timestamp%.txt"
    set netfxinstallerlog="%PathToNETFXInstall%log\NetFXInstallerLog-%timestamp%"
    echo %log% >> %startuptasklog%
    echo Logfile generated at: %startuptasklog% >> %startuptasklog%
    echo TMP set to: %TMP% >> %startuptasklog%
    echo TEMP set to: %TEMP% >> %startuptasklog%

    REM ***** Check if .NET is installed *****
    echo Checking if .NET (%netfx%) is installed >> %startuptasklog%
    set /A netfxregkeydecimal=%netfxregkey%
    set foundkey=0
    FOR /F "usebackq skip=2 tokens=1,2*" %%A in (`reg query "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full" /v Release 2^>nul`) do @set /A foundkey=%%C
    echo Minimum required key: %netfxregkeydecimal% -- found key: %foundkey% >> %startuptasklog%
    if %foundkey% GEQ %netfxregkeydecimal% goto installed

    REM ***** Installing .NET *****
    echo Installing .NET with commandline: start /wait %~dp0%netfxinstallfile% /q /serialdownload /log %netfxinstallerlog%  /chainingpackage "CloudService Startup Task" >> %startuptasklog%
    start /wait %~dp0%netfxinstallfile% /q /serialdownload /log %netfxinstallerlog% /chainingpackage "CloudService Startup Task" >> %startuptasklog% 2>>&1
    if %ERRORLEVEL%== 0 goto installed
        echo .NET installer exited with code %ERRORLEVEL% >> %startuptasklog%    
        if %ERRORLEVEL%== 3010 goto restart
        if %ERRORLEVEL%== 1641 goto restart
        echo .NET (%netfx%) install failed with Error Code %ERRORLEVEL%. Further logs can be found in %netfxinstallerlog% >> %startuptasklog%

    :restart
    echo Restarting toocomplete .NET (%netfx%) installation >> %startuptasklog%
    EXIT /B %ERRORLEVEL%

    :installed
    echo .NET (%netfx%) is installed >> %startuptasklog%

    :end
    echo install.cmd completed: %date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2% >> %startuptasklog%

    :exit
    EXIT /B 0
    ```
   
   > [!NOTE]
   > Este script muestra cómo tooinstall .NET 4.5.2 o la versión 4.6 de continuidad, aunque ya está disponible en .NET 4.5.2 Hola SO invitado de Azure. Directamente debe instalar .NET 4.6.1 en lugar de la versión 4.6, tal y como se describe en hello [el artículo de Knowledge Base 3118750](https://support.microsoft.com/kb/3118750).
   > 
   > 

3. Agregar el rol tooeach de hello install.cmd archivos mediante el uso de **agregar** > **elemento existente** en **el Explorador de soluciones** tal como se describe anteriormente en este tema. 

    Una vez completado este paso, deben tener todos los roles de archivo de instalador de .NET de hello y archivo de hello install.cmd.

   ![Contenidos de rol con todos los archivos][2]

## <a name="configure-diagnostics-tootransfer-startup-logs-tooblob-storage"></a>Configurar el almacenamiento de información de diagnóstico tootransfer inicio registros tooBlob
toosimplify solución de problemas de instalación, puede configurar diagnósticos de Azure tootransfer script o bienvenida almacenamiento de blobs de tooAzure de instalador de .NET a los archivos de registro generados por el inicio de Hola. Con este enfoque, puede ver registros de Hola por descargar archivos de registro de hello desde almacenamiento de blobs, en lugar de tener tooremote escritorio en función de Hola.

tooconfigure diagnósticos, abra el archivo diagnostics.wadcfgx de hello y agregue Hola siguen contenido en hello **directorios** nodo: 

```xml 
<DataSources>
 <DirectoryConfiguration containerName="netfx-install">
  <LocalResource name="NETFXInstall" relativePath="log"/>
 </DirectoryConfiguration>
</DataSources>
```

Este código XML configura archivos de diagnóstico tootransfer hello en el directorio de registro de hello en hello **NETFXInstall** recurso toohello cuenta de almacenamiento de diagnósticos en hello **netfx install** contenedor de blobs.

## <a name="deploy-your-cloud-service"></a>Implementación del servicio en la nube
Al implementar el servicio de nube, las tareas de inicio de Hola instalación Hola .NET Framework si aún no está instalado. Los roles de servicio de nube están en hello *ocupado* estado mientras se instala framework Hola. Si la instalación de framework Hola requiere un reinicio, los roles del servicio hello también podrían reiniciarse. 

## <a name="additional-resources"></a>Recursos adicionales
* [Hola instalar .NET Framework][Installing hello .NET Framework]
* [Determinación de las versiones instaladas de .NET Framework][How to: Determine Which .NET Framework Versions Are Installed]
* [Solución de problemas en instalaciones de .NET Framework][Troubleshooting .NET Framework Installations]

[How to: Determine Which .NET Framework Versions Are Installed]: https://msdn.microsoft.com/library/hh925568.aspx
[Installing hello .NET Framework]: https://msdn.microsoft.com/library/5a4x27ek.aspx
[Troubleshooting .NET Framework Installations]: https://msdn.microsoft.com/library/hh925569.aspx

<!--Image references-->
[1]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithinstallerfiles.png
[2]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithallfiles.png
