---
title: aaaGet a trabajar con Python y los servicios de nube de Azure | Documentos de Microsoft
description: "Información general del uso de Python Tools para los servicios de nube de Azure de Visual Studio toocreate incluidos los roles web y roles de trabajo."
services: cloud-services
documentationcenter: python
author: thraka
manager: timlt
editor: 
ms.assetid: 5489405d-6fa9-4b11-a161-609103cbdc18
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: f5fd85e754839f146abe912351c59dc4a148c990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="python-web-and-worker-roles-with-python-tools-for-visual-studio"></a>Roles web y de trabajo de Python con herramientas de Python para Visual Studio

En este artículo se ofrece información general sobre el uso de roles web y de trabajo de Python con [herramientas de Python para Visual Studio][Python Tools for Visual Studio]. Obtenga información acerca de cómo toouse Visual Studio toocreate e implementar un servicio de nube básico que usa Python.

## <a name="prerequisites"></a>Requisitos previos
* [Visual Studio 2013, 2015 o 2017](https://www.visualstudio.com/)
* [Herramientas de Python para Visual Studio][Python Tools for Visual Studio] (PTVS)
* [Herramientas de Azure SDK para VS 2013][Azure SDK Tools for VS 2013] o  
[Herramientas de Azure SDK para VS 2015][Azure SDK Tools for VS 2015] o  
[Herramientas de Azure SDK para VS 2017][Azure SDK Tools for VS 2017]
* [Python 2.7 de 32 bits][Python 2.7 32-bit] o [Python 3.5 de 32 bits][Python 3.5 32-bit]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-are-python-web-and-worker-roles"></a>¿Qué son los roles web y de trabajo de Python?
Azure ofrece tres modelos de proceso para la ejecución de aplicaciones: [característica Web Apps de Azure App Service][execution model-web sites], [Azure Virtual Machines][execution model-vms], and [Azure Cloud Services][execution model-cloud services]. Los tres modelos admiten Python. Cloud Services, que incluye roles web y de trabajo, proporciona una *Plataforma como servicio (PaaS)*. Dentro de un servicio de nube, un rol web proporciona a un web de front-end de Internet Information Services (IIS) web server toohost dedicado de las aplicaciones, mientras que un rol de trabajo puede ejecutar tareas asincrónicas, ejecución prolongada o perpetuas independientes de interacción del usuario o una entrada de.

Para más información, consulte [¿Qué es un servicio en la nube?]

> [!NOTE]
> *¿Busca un sitio Web sencillo toobuild?*
> Si su escenario implica sólo un sitio Web simple front-end, considere el uso de características de las aplicaciones Web ligeras hello en el servicio de aplicación de Azure. Puede actualizar fácilmente tooa servicio en la nube que aumenta su sitio Web y cambian los requisitos. Vea hello <a href="/develop/python/">Centro para desarrolladores de Python</a> para los artículos que tratan el desarrollo de característica de aplicaciones Web de hello en el servicio de aplicación de Azure.
> <br />
> 
> 

## <a name="project-creation"></a>Creación de un proyecto
En Visual Studio, puede seleccionar **servicio de nube de Azure** en hello **nuevo proyecto** cuadro de diálogo **Python**.

![Cuadro de diálogo Nuevo proyecto](./media/cloud-services-python-ptvs/new-project-cloud-service.png)

En el Asistente de servicio de nube de Azure de hello, puede crear nuevo sitio web y roles de trabajo.

![Cuadro de diálogo Servicio en la nube de Azure](./media/cloud-services-python-ptvs/new-service-wizard.png)

plantilla de rol de trabajo de Hello incluye reutilizable código tooconnect tooan cuenta de almacenamiento de Azure o Service Bus de Azure.

![Solución de servicio en la nube](./media/cloud-services-python-ptvs/worker.png)

Puede agregar el servicio web o trabajo roles tooan existente en la nube en cualquier momento.  Puede elegir tooadd los proyectos existentes de la solución o crear otras nuevas.

![Comando Agregar rol](./media/cloud-services-python-ptvs/add-new-or-existing-role.png)

Su servicio en la nube puede contener roles implementados en diferentes lenguajes.  Por ejemplo, puede tener un rol web de Python implementado con Django, con Python o con roles de trabajo de C#.  Puede comunicarse fácilmente entre sus roles usando colas del Bus de servicio o colas de almacenamiento.

## <a name="install-python-on-hello-cloud-service"></a>Instalar Python Hola servicio en nube
> [!WARNING]
> scripts de instalación de Hola que se instalan con Visual Studio (en este artículo se actualizó por última vez el tiempo de hello) no funcionan. En esta sección se describe una solución alternativa.
> 
> 

Hola principal problema con las secuencias de comandos del programa de instalación de hello es no instalar python. En primer lugar, defina dos [las tareas de inicio](cloud-services-startup-tasks.md) en hello [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) archivo. primera tarea de Hello (**PrepPython.ps1**) descarga e instala en tiempo de ejecución de Python de Hola. segunda tarea de Hello (**PipInstaller.ps1**) se ejecuta pip tooinstall las dependencias puede tener.

Hola siguientes secuencias de comandos se escribieron destino Python es 3.5. Si desea toouse Hola versión 2.x de python, conjunto hello **PYTHON2** variable archivo demasiado**en** para las tareas de inicio de hello dos y tarea de hello en tiempo de ejecución: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.

```xml
<Startup>

  <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PrepPython.ps1">
    <Environment>
      <Variable name="EMULATED">
        <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
      </Variable>
      <Variable name="PYTHON2" value="off" />
    </Environment>
  </Task>

  <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PipInstaller.ps1">
    <Environment>
      <Variable name="EMULATED">
        <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
      </Variable>
      <Variable name="PYTHON2" value="off" />
    </Environment>

  </Task>

</Startup>
```

Hola **PYTHON2** y **PYPATH** variables se deben agregar tarea de inicio del trabajo de toohello. Hola **PYPATH** variable solo se usa si hello **PYTHON2** variable se establece demasiado**en**.

```xml
<Runtime>
  <Environment>
    <Variable name="EMULATED">
      <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
    </Variable>
    <Variable name="PYTHON2" value="off" />
    <Variable name="PYPATH" value="%SystemDrive%\Python27" />
  </Environment>
  <EntryPoint>
    <ProgramEntryPoint commandLine="bin\ps.cmd LaunchWorker.ps1" setReadyOnProcessStart="true" />
  </EntryPoint>
</Runtime>
```

#### <a name="sample-servicedefinitioncsdef"></a>Archivo ServiceDefinition.csdef de ejemplo
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="AzureCloudServicePython" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2015-04.2.6">
  <WorkerRole name="WorkerRole1" vmsize="Small">
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" />
      <Setting name="Python2" />
    </ConfigurationSettings>
    <Startup>
      <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PrepPython.ps1">
        <Environment>
          <Variable name="EMULATED">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
          <Variable name="PYTHON2" value="off" />
        </Environment>
      </Task>
      <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PipInstaller.ps1">
        <Environment>
          <Variable name="EMULATED">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
          <Variable name="PYTHON2" value="off" />
        </Environment>
      </Task>
    </Startup>
    <Runtime>
      <Environment>
        <Variable name="EMULATED">
          <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
        </Variable>
        <Variable name="PYTHON2" value="off" />
        <Variable name="PYPATH" value="%SystemDrive%\Python27" />
      </Environment>
      <EntryPoint>
        <ProgramEntryPoint commandLine="bin\ps.cmd LaunchWorker.ps1" setReadyOnProcessStart="true" />
      </EntryPoint>
    </Runtime>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
  </WorkerRole>
</ServiceDefinition>
```



A continuación, cree hello **PrepPython.ps1** y **PipInstaller.ps1** archivos Hola **. / bin** carpeta de su rol.

#### <a name="preppythonps1"></a>PrepPython.ps1
Este script instala Python. Si hello **PYTHON2** variable de entorno se establece demasiado**en**, a continuación, instalar Python 2.7, en caso contrario, se instala 3.5 de Python.

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated){
    Write-Output "Checking if python is installed...$nl"
    if ($is_python2) {
        & "${env:SystemDrive}\Python27\python.exe"  -V | Out-Null
    }
    else {
        py -V | Out-Null
    }

    if (-not $?) {

        $url = "https://www.python.org/ftp/python/3.5.2/python-3.5.2-amd64.exe"
        $outFile = "${env:TEMP}\python-3.5.2-amd64.exe"

        if ($is_python2) {
            $url = "https://www.python.org/ftp/python/2.7.12/python-2.7.12.amd64.msi"
            $outFile = "${env:TEMP}\python-2.7.12.amd64.msi"
        }

        Write-Output "Not found, downloading $url too$outFile$nl"
        Invoke-WebRequest $url -OutFile $outFile
        Write-Output "Installing$nl"

        if ($is_python2) {
            Start-Process msiexec.exe -ArgumentList "/q", "/i", "$outFile", "ALLUSERS=1" -Wait
        }
        else {
            Start-Process "$outFile" -ArgumentList "/quiet", "InstallAllUsers=1" -Wait
        }

        Write-Output "Done$nl"
    }
    else {
        Write-Output "Already installed"
    }
}
```

#### <a name="pipinstallerps1"></a>PipInstaller.ps1
Esta secuencia de comandos llama a una pip e instala todas las dependencias de Hola de Hola **requirements.txt** archivo. Si hello **PYTHON2** variable de entorno se establece demasiado**en**, a continuación, se usa Python 2.7, en caso contrario, se usa Python 3.5.

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated){
    Write-Output "Checking if requirements.txt exists$nl"
    if (Test-Path ..\requirements.txt) {
        Write-Output "Found. Processing pip$nl"

        if ($is_python2) {
            & "${env:SystemDrive}\Python27\python.exe" -m pip install -r ..\requirements.txt
        }
        else {
            py -m pip install -r ..\requirements.txt
        }

        Write-Output "Done$nl"
    }
    else {
        Write-Output "Not found$nl"
    }
}
```

#### <a name="modify-launchworkerps1"></a>Modificación del archivo LaunchWorker.ps1
> [!NOTE]
> En caso de hello de un **rol de trabajo** proyecto **LauncherWorker.ps1** archivo es necesario tooexecute Hola inicio. En un **rol web** proyecto de equipo y hello archivo de inicio se define en Propiedades del proyecto Hola.
> 
> 

Hola **bin\LaunchWorker.ps1** creó originalmente toodo una gran cantidad de trabajo de preparación, pero realmente no funciona. Reemplace el contenido de hello en ese archivo por hello siguiente secuencia de comandos.

Esta secuencia de comandos llama hello **worker.py** archivo desde el proyecto de python. Si hello **PYTHON2** variable de entorno se establece demasiado**en**, a continuación, se usa Python 2.7, en caso contrario, se usa Python 3.5.

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated)
{
    Write-Output "Running worker.py$nl"

    if ($is_python2) {
        cd..
        iex "$env:PYPATH\python.exe worker.py"
    }
    else {
        cd..
        iex "py worker.py"
    }
}
else
{
    Write-Output "Running (EMULATED) worker.py$nl"

    # Customize tooyour local dev environment

    if ($is_python2) {
        cd..
        iex "$env:PYPATH\python.exe worker.py"
    }
    else {
        cd..
        iex "py worker.py"
    }
}
```

#### <a name="pscmd"></a>ps.cmd
plantillas de Visual Studio Hola deberían haber creado un **ps.cmd** archivo Hola **. / bin** carpeta. Esta secuencia de comandos de shell llama Hola PowerShell scripts de contenedor anteriores y proporciona un registro basándose en nombre Hola Hola PowerShell contenedor llama. Si no se ha creado este archivo, esto es lo que debería haber en él. 

```bat
@echo off

cd /D %~dp0

if not exist "%DiagnosticStore%\LogFiles" mkdir "%DiagnosticStore%\LogFiles"
%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe -ExecutionPolicy Unrestricted -File %* >> "%DiagnosticStore%\LogFiles\%~n1.txt" 2>> "%DiagnosticStore%\LogFiles\%~n1.err.txt"
```



## <a name="run-locally"></a>Ejecución en modo local
Si establece el proyecto de servicio de nube como proyecto de inicio de hello y presione F5, servicio de nube de Hola se ejecuta en el emulador de Azure local Hola.

Aunque PTVS admite iniciar en el emulador de hello, depuración (por ejemplo, los puntos de interrupción) no funciona.

toodebug sus roles web y de trabajo, puede establecer el proyecto de rol de hello como proyecto de inicio de Hola y que, en lugar de depuración.  También puede establecer varios proyectos de inicio.  Haga clic en soluciones de hello y, a continuación, seleccione **Establecer proyectos de inicio**.

![Propiedades del proyecto de inicio de la solución](./media/cloud-services-python-ptvs/startup.png)

## <a name="publish-tooazure"></a>Publicar tooAzure
toopublish, haga clic en proyecto de servicio de nube de hello en soluciones de hello y, a continuación, seleccione **publicar**.

![Inicio de sesión para publicación de Microsoft Azure](./media/cloud-services-python-ptvs/publish-sign-in.png)

Siga al Asistente de Hola. Si es necesario, habilite el Escritorio remoto. Escritorio remoto es útil cuando necesita toodebug algo.

Cuando haya terminado la configuración, haga clic en **Publicar**.

Algunos progreso aparece en la ventana de salida de hello, a continuación, verá la ventana de registro de actividad de Microsoft Azure hello.

![Ventana Registro de actividad de Microsoft Azure](./media/cloud-services-python-ptvs/publish-activity-log.png)

Implementación tarda varios minutos toocomplete, a continuación, en la web o roles de trabajo se ejecutan en Azure.

### <a name="investigate-logs"></a>Investigación de registros
Después de hello en la nube servicio virtual machine se inicia y se instala Python, puede mirar Hola registros toofind mensajes de error. Estos registros se encuentran en hello **C:\Resources\Directory\\\LogFiles {rol}** carpeta. **PrepPython.err.txt** tiene al menos un error en ella desde al script de Hola intenta toodetect si está instalado Python y **PipInstaller.err.txt** puede informar de una versión no actualizada de pip.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre cómo trabajar con roles de web y de trabajo en Python Tools para Visual Studio, consulte la documentación de PTVS de hello:

* [Proyectos de servicio en la nube][Cloud Service Projects]

Para obtener más detalles sobre el uso de servicios de Azure desde los roles web y de trabajo, como el uso de almacenamiento de Azure o Bus de servicio, vea Hola siguientes artículos:

* [Blob Service][Blob Service]
* [Table Service][Table Service]
* [Queue Service][Queue Service]
* [Colas de Service Bus][Service Bus Queues]
* [Temas de Service Bus][Service Bus Topics]

<!--Link references-->

[¿Qué es un servicio en la nube?]: cloud-services-choose-me.md
[execution model-web sites]: ../app-service-web/app-service-web-overview.md
[execution model-vms]:../virtual-machines/windows/overview.md
[execution model-cloud services]: cloud-services-choose-me.md
[Python Developer Center]: /develop/python/

[Blob Service]:../storage/blobs/storage-python-how-to-use-blob-storage.md
[Queue Service]: ../storage/queues/storage-python-how-to-use-queue-storage.md
[Table Service]:../cosmos-db/table-storage-how-to-use-python.md
[Service Bus Queues]: ../service-bus-messaging/service-bus-python-how-to-use-queues.md
[Service Bus Topics]: ../service-bus-messaging/service-bus-python-how-to-use-topics-subscriptions.md


<!--External Link references-->

[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs
[Cloud Service Projects]: http://go.microsoft.com/fwlink/?LinkId=624028
[Azure SDK Tools for VS 2013]: http://go.microsoft.com/fwlink/?LinkId=746482
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=746481
[Azure SDK Tools for VS 2017]: http://go.microsoft.com/fwlink/?LinkId=746483
[Python 2.7 32-bit]: https://www.python.org/downloads/
[Python 3.5 32-bit]: https://www.python.org/downloads/
