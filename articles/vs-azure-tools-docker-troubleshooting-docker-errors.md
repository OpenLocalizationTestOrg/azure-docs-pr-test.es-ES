---
title: los errores de cliente de Docker de aaaTroubleshooting en Windows con Visual Studio | Documentos de Microsoft
description: Solucionar problemas que producirse al usar Visual Studio toocreate e implementar tooDocker de aplicaciones web en Windows con Visual Studio.
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 346f70b9-7b52-4688-a8e8-8f53869618d3
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 7421ae8e044d58fc412d748fb870da4c9b2fdb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-visual-studio-docker-development"></a>Solución de problemas de desarrollo de Docker en Visual Studio

Cuando se trabaja con Visual Studio Tools para la vista previa de Docker, puede encontrar algunos problemas debido a la naturaleza de Hola de vista previa de Hola.
Estos son algunos problemas frecuentes y sus soluciones.  

## <a name="visual-studio-2017-rc"></a>Visual Studio 2017 RC

### <a name="linux-containers"></a>**Contenedores de Linux**

####  <a name="build-errors-occur-when-debugging-a-net-core-web-or-console-application"></a>Se producen errores de compilación cuando se depura una aplicación de consola o web de .NET Core.  

Esto podría ser toonot relacionado comparten unidad de Hola donde reside el proyecto de hello con Docker para Windows.  Puede recibir un error similar Hola siguiente:

```
hello "PrepareForLaunch" task failed unexpectedly.
Microsoft.DotNet.Docker.CommandLineClientException: Creating network "webapplication13628050196_default" with hello default driver
Building webapplication1
Creating webapplication13628050196_webapplication1_1
ERROR: for webapplication1  Cannot create container for service webapplication1: C: drive is not shared. Please share it in Docker for Windows Settings
```
tooresolve este problema:

1. Haga clic en **Docker para Windows** en Hola área de notificación y, a continuación, seleccione **configuración**.  
2. Seleccione **unidades compartidas** y compartir unidad Hola donde reside el proyecto de Hola.

### <a name="windows-containers"></a>**Contenedores de Windows**

Hello problemas siguientes son aplicaciones de web y la consola de .NET Framework de toodebugging específicos en los contenedores de Windows.

#### <a name="prerequisites"></a>Requisitos previos

1. Visual Studio 2017 RC (o posterior) con Hola .NET Core y carga de trabajo de vista previa de Docker debe estar instalado.
2. Actualización de aniversario de Windows 10 con las revisiones de Windows Update más recientes. En concreto, [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016) debe estar instalado. 
3. [Docker para Windows](https://docs.docker.com/docker-for-windows/) (compilación 1.13.0 o posterior) debe estar instalado.
4. **Cambiar tooWindows contenedores** debe seleccionarse. En el área de notificación de hello, haga clic en **Docker para Windows**y, a continuación, seleccione **cambiar contenedores tooWindows**. Una vez reiniciado el equipo de hello, asegúrese de que esta configuración se conserva.

#### <a name="console-output-does-not-appear-in-visual-studios-output-window-while-debugging-a-console-application"></a>La salida de la consola no aparece en la ventana de salida de Visual Studio cuando se depura una aplicación de consola.

Se trata de un problema conocido con el depurador de Visual Studio (msvsmon.exe), de Hola que actualmente no está diseñado para este escenario. En un futuro podría incluirse compatibilidad para este escenario. resultado de toosee de aplicación de consola de hello en Visual Studio, use **Docker: Iniciar proyecto**, que es equivalente**iniciar sin depurar**.

#### <a name="debugging-web-applications-with-hello-release-configuration-fails-with-403-forbidden-error"></a>Se produce un error de configuración con error (403) prohibido de la versión de depuración de aplicaciones web con hello

toowork resolver este problema, abra web.release.config de solución de Hola y comente o eliminar Hola siguientes líneas:

```
<compilation xdt:Transform="RemoveAttributes(debug)" />
```

## <a name="visual-studio-2015"></a>Visual Studio 2015

### <a name="linux-containers"></a>**Contenedores de Linux**

#### <a name="unable-toovalidate-volume-mapping"></a>Asignación de volúmenes no se puede toovalidate
Asignación de volúmenes es necesario tooshare Hola código y archivos binarios de la aplicación con la carpeta de la aplicación hello en el contenedor de Hola.  Las asignaciones de volumen específicas se encuentran dentro de los archivos docker-compose.dev.debug.yml y docker-compose.dev.release.yml. Los archivos se cambien en el equipo host, contenedores de hello reflejan estos cambios en una estructura de carpeta similar.

asignación de volúmenes de tooenable:

1. Haga clic en **Moby** en el área de notificación de Hola y seleccione **configuración**.
2. Seleccione **Shared Drives** (Unidades compartidas).
3. Seleccione la unidad de Hola que hospeda la unidad de hello y el proyecto en el que reside % USERPROFILE %.
4. Haga clic en **Apply**.

tootest si funciona la asignación de volúmenes, volver a generar y seleccione F5 desde dentro de Visual Studio después de que se han compartido una o varias unidades, o ejecute hello siguiente código desde un símbolo del sistema.

> [!NOTE]
> En este ejemplo da por supuesto que la carpeta Usuarios se encuentra en la unidad "C" y se ha compartido.
> Revise en caso de que haya compartido una unidad diferente.

```
docker run -it -v /c/Users/Public:/wormhole busybox
```

Ejecute hello siguiente código en el contenedor de Linux Hola.

```
/ # ls
```

Debería ver una lista de directorios de Hola a los usuarios y carpetas públicas. Si no se muestran archivos y la carpeta /c/Usuarios/Público no está vacía, la asignación de volúmenes no está configurada correctamente.

```
bin       etc       proc      sys       usr       wormhole
dev       home      root      tmp       var
```

Cambiar toohello túnel espacial directory toosee Hola contenido de hello `/c/Users/Public` directorio:

```
/ # cd wormhole/
/wormhole # ls
AccountPictures  Downloads        Music            Videos
Desktop          Host             NuGet.Config     desktop.ini
Documents        Libraries        Pictures
/wormhole #
```

> [!NOTE]
> Cuando se trabaja con máquinas virtuales de Linux, el sistema de archivos del contenedor de hello distingue mayúsculas de minúsculas.

## <a name="build-prepareforbuild-task-failed-unexpectedly"></a>Compilación: Error inesperado en la tarea "PrepareForBuild".

Microsoft.DotNet.Docker.CommandLine.ClientException: Error al tratar de tooconnect.

Compruebe que ese host de Docker de hello predeterminado se está ejecutando. Abra un símbolo del sistema y ejecute:

```
docker info
```

Si se devuelve un error, a continuación, intente hello toostart **Docker para Windows** una aplicación de escritorio. Si está ejecutando una aplicación de escritorio hello, a continuación, **Moby** debería estar visible en el área de notificación de Hola. Haga clic en **Moby** y abra **Settings** (Configuración). Haga clic en **Reset** (Restablecer) y, a continuación, reinicie Docker.

## <a name="an-error-dialog-occurs-when-attempting-tooadd-docker-support-or-debug-f5-an-aspnet-core-application-in-a-container"></a>Un cuadro de diálogo de error aparece al intentar tooadd soporte de Docker o depurar una aplicación de ASP.NET Core en un contenedor de (F5)

Después de desinstalar e instalar las extensiones, Hola caché de Managed Extensibility Framework (MEF) en Visual Studio puede resultar dañada. Cuando esto ocurre, puede causar diversos mensajes de error cuando está agregando compatibilidad con Docker o intentar toorun o depurar su aplicación de ASP.NET Core de (F5). Como solución temporal, use Hola siguiendo los pasos toodelete y regenerate Hola MEF la memoria caché.

1. Cierre todas las instancias de Visual Studio.
1. Abra %USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.
1. Eliminar Hola siguientes carpetas:
     ```
       ComponentModelCache
       Extensions
       MEFCacheBackup
    ```
1. Abra Visual Studio.
1. Vuelva a intentar el escenario de Hola.
