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
# <a name="python-web-and-worker-roles-with-python-tools-for-visual-studio"></a><span data-ttu-id="e26ab-103">Roles web y de trabajo de Python con herramientas de Python para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e26ab-103">Python web and worker roles with Python Tools for Visual Studio</span></span>

<span data-ttu-id="e26ab-104">En este artículo se ofrece información general sobre el uso de roles web y de trabajo de Python con [herramientas de Python para Visual Studio][Python Tools for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="e26ab-104">This article provides an overview of using Python web and worker roles using [Python Tools for Visual Studio][Python Tools for Visual Studio].</span></span> <span data-ttu-id="e26ab-105">Obtenga información acerca de cómo toouse Visual Studio toocreate e implementar un servicio de nube básico que usa Python.</span><span class="sxs-lookup"><span data-stu-id="e26ab-105">Learn how toouse Visual Studio toocreate and deploy a basic Cloud Service that uses Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e26ab-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e26ab-106">Prerequisites</span></span>
* [<span data-ttu-id="e26ab-107">Visual Studio 2013, 2015 o 2017</span><span class="sxs-lookup"><span data-stu-id="e26ab-107">Visual Studio 2013, 2015, or 2017</span></span>](https://www.visualstudio.com/)
* <span data-ttu-id="e26ab-108">[Herramientas de Python para Visual Studio][Python Tools for Visual Studio] (PTVS)</span><span class="sxs-lookup"><span data-stu-id="e26ab-108">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS)</span></span>
* <span data-ttu-id="e26ab-109">[Herramientas de Azure SDK para VS 2013][Azure SDK Tools for VS 2013] o</span><span class="sxs-lookup"><span data-stu-id="e26ab-109">[Azure SDK Tools for VS 2013][Azure SDK Tools for VS 2013] or</span></span>  
<span data-ttu-id="e26ab-110">[Herramientas de Azure SDK para VS 2015][Azure SDK Tools for VS 2015] o</span><span class="sxs-lookup"><span data-stu-id="e26ab-110">[Azure SDK Tools for VS 2015][Azure SDK Tools for VS 2015] or</span></span>  
<span data-ttu-id="e26ab-111">[Herramientas de Azure SDK para VS 2017][Azure SDK Tools for VS 2017]</span><span class="sxs-lookup"><span data-stu-id="e26ab-111">[Azure SDK Tools for VS 2017][Azure SDK Tools for VS 2017]</span></span>
* <span data-ttu-id="e26ab-112">[Python 2.7 de 32 bits][Python 2.7 32-bit] o [Python 3.5 de 32 bits][Python 3.5 32-bit]</span><span class="sxs-lookup"><span data-stu-id="e26ab-112">[Python 2.7 32-bit][Python 2.7 32-bit] or [Python 3.5 32-bit][Python 3.5 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-are-python-web-and-worker-roles"></a><span data-ttu-id="e26ab-113">¿Qué son los roles web y de trabajo de Python?</span><span class="sxs-lookup"><span data-stu-id="e26ab-113">What are Python web and worker roles?</span></span>
<span data-ttu-id="e26ab-114">Azure ofrece tres modelos de proceso para la ejecución de aplicaciones: [característica Web Apps de Azure App Service][execution model-web sites], [Azure Virtual Machines][execution model-vms], and [Azure Cloud Services][execution model-cloud services].</span><span class="sxs-lookup"><span data-stu-id="e26ab-114">Azure provides three compute models for running applications: [Web Apps feature in Azure App Service][execution model-web sites], [Azure Virtual Machines][execution model-vms], and [Azure Cloud Services][execution model-cloud services].</span></span> <span data-ttu-id="e26ab-115">Los tres modelos admiten Python.</span><span class="sxs-lookup"><span data-stu-id="e26ab-115">All three models support Python.</span></span> <span data-ttu-id="e26ab-116">Cloud Services, que incluye roles web y de trabajo, proporciona una *Plataforma como servicio (PaaS)*.</span><span class="sxs-lookup"><span data-stu-id="e26ab-116">Cloud Services, which include web and worker roles, provide *Platform as a Service (PaaS)*.</span></span> <span data-ttu-id="e26ab-117">Dentro de un servicio de nube, un rol web proporciona a un web de front-end de Internet Information Services (IIS) web server toohost dedicado de las aplicaciones, mientras que un rol de trabajo puede ejecutar tareas asincrónicas, ejecución prolongada o perpetuas independientes de interacción del usuario o una entrada de.</span><span class="sxs-lookup"><span data-stu-id="e26ab-117">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server toohost front end web applications, while a worker role can run asynchronous, long-running, or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="e26ab-118">Para más información, consulte [¿Qué es un servicio en la nube?]</span><span class="sxs-lookup"><span data-stu-id="e26ab-118">For more information, see [What is a Cloud Service?].</span></span>

> [!NOTE]
> <span data-ttu-id="e26ab-119">*¿Busca un sitio Web sencillo toobuild?*</span><span class="sxs-lookup"><span data-stu-id="e26ab-119">*Looking toobuild a simple website?*</span></span>
> <span data-ttu-id="e26ab-120">Si su escenario implica sólo un sitio Web simple front-end, considere el uso de características de las aplicaciones Web ligeras hello en el servicio de aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="e26ab-120">If your scenario involves just a simple website front end, consider using hello lightweight Web Apps feature in Azure App Service.</span></span> <span data-ttu-id="e26ab-121">Puede actualizar fácilmente tooa servicio en la nube que aumenta su sitio Web y cambian los requisitos.</span><span class="sxs-lookup"><span data-stu-id="e26ab-121">You can easily upgrade tooa Cloud Service as your website grows and your requirements change.</span></span> <span data-ttu-id="e26ab-122">Vea hello <a href="/develop/python/">Centro para desarrolladores de Python</a> para los artículos que tratan el desarrollo de característica de aplicaciones Web de hello en el servicio de aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="e26ab-122">See hello <a href="/develop/python/">Python Developer Center</a> for articles that cover development of hello Web Apps feature in Azure App Service.</span></span>
> <br />
> 
> 

## <a name="project-creation"></a><span data-ttu-id="e26ab-123">Creación de un proyecto</span><span class="sxs-lookup"><span data-stu-id="e26ab-123">Project creation</span></span>
<span data-ttu-id="e26ab-124">En Visual Studio, puede seleccionar **servicio de nube de Azure** en hello **nuevo proyecto** cuadro de diálogo **Python**.</span><span class="sxs-lookup"><span data-stu-id="e26ab-124">In Visual Studio, you can select **Azure Cloud Service** in hello **New Project** dialog box, under **Python**.</span></span>

![Cuadro de diálogo Nuevo proyecto](./media/cloud-services-python-ptvs/new-project-cloud-service.png)

<span data-ttu-id="e26ab-126">En el Asistente de servicio de nube de Azure de hello, puede crear nuevo sitio web y roles de trabajo.</span><span class="sxs-lookup"><span data-stu-id="e26ab-126">In hello Azure Cloud Service wizard, you can create new web and worker roles.</span></span>

![Cuadro de diálogo Servicio en la nube de Azure](./media/cloud-services-python-ptvs/new-service-wizard.png)

<span data-ttu-id="e26ab-128">plantilla de rol de trabajo de Hello incluye reutilizable código tooconnect tooan cuenta de almacenamiento de Azure o Service Bus de Azure.</span><span class="sxs-lookup"><span data-stu-id="e26ab-128">hello worker role template comes with boilerplate code tooconnect tooan Azure storage account or Azure Service Bus.</span></span>

![Solución de servicio en la nube](./media/cloud-services-python-ptvs/worker.png)

<span data-ttu-id="e26ab-130">Puede agregar el servicio web o trabajo roles tooan existente en la nube en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="e26ab-130">You can add web or worker roles tooan existing cloud service at any time.</span></span>  <span data-ttu-id="e26ab-131">Puede elegir tooadd los proyectos existentes de la solución o crear otras nuevas.</span><span class="sxs-lookup"><span data-stu-id="e26ab-131">You can choose tooadd existing projects in your solution, or create new ones.</span></span>

![Comando Agregar rol](./media/cloud-services-python-ptvs/add-new-or-existing-role.png)

<span data-ttu-id="e26ab-133">Su servicio en la nube puede contener roles implementados en diferentes lenguajes.</span><span class="sxs-lookup"><span data-stu-id="e26ab-133">Your cloud service can contain roles implemented in different languages.</span></span>  <span data-ttu-id="e26ab-134">Por ejemplo, puede tener un rol web de Python implementado con Django, con Python o con roles de trabajo de C#.</span><span class="sxs-lookup"><span data-stu-id="e26ab-134">For example, you can have a Python web role implemented using Django, with Python, or with C# worker roles.</span></span>  <span data-ttu-id="e26ab-135">Puede comunicarse fácilmente entre sus roles usando colas del Bus de servicio o colas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e26ab-135">You can easily communicate between your roles using Service Bus queues or storage queues.</span></span>

## <a name="install-python-on-hello-cloud-service"></a><span data-ttu-id="e26ab-136">Instalar Python Hola servicio en nube</span><span class="sxs-lookup"><span data-stu-id="e26ab-136">Install Python on hello cloud service</span></span>
> [!WARNING]
> <span data-ttu-id="e26ab-137">scripts de instalación de Hola que se instalan con Visual Studio (en este artículo se actualizó por última vez el tiempo de hello) no funcionan.</span><span class="sxs-lookup"><span data-stu-id="e26ab-137">hello setup scripts that are installed with Visual Studio (at hello time this article was last updated) do not work.</span></span> <span data-ttu-id="e26ab-138">En esta sección se describe una solución alternativa.</span><span class="sxs-lookup"><span data-stu-id="e26ab-138">This section describes a workaround.</span></span>
> 
> 

<span data-ttu-id="e26ab-139">Hola principal problema con las secuencias de comandos del programa de instalación de hello es no instalar python.</span><span class="sxs-lookup"><span data-stu-id="e26ab-139">hello main problem with hello setup scripts is that they do not install python.</span></span> <span data-ttu-id="e26ab-140">En primer lugar, defina dos [las tareas de inicio](cloud-services-startup-tasks.md) en hello [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) archivo.</span><span class="sxs-lookup"><span data-stu-id="e26ab-140">First, define two [startup tasks](cloud-services-startup-tasks.md) in hello [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) file.</span></span> <span data-ttu-id="e26ab-141">primera tarea de Hello (**PrepPython.ps1**) descarga e instala en tiempo de ejecución de Python de Hola.</span><span class="sxs-lookup"><span data-stu-id="e26ab-141">hello first task (**PrepPython.ps1**) downloads and installs hello Python runtime.</span></span> <span data-ttu-id="e26ab-142">segunda tarea de Hello (**PipInstaller.ps1**) se ejecuta pip tooinstall las dependencias puede tener.</span><span class="sxs-lookup"><span data-stu-id="e26ab-142">hello second task (**PipInstaller.ps1**) runs pip tooinstall any dependencies you may have.</span></span>

<span data-ttu-id="e26ab-143">Hola siguientes secuencias de comandos se escribieron destino Python es 3.5.</span><span class="sxs-lookup"><span data-stu-id="e26ab-143">hello following scripts were written targeting Python 3.5.</span></span> <span data-ttu-id="e26ab-144">Si desea toouse Hola versión 2.x de python, conjunto hello **PYTHON2** variable archivo demasiado**en** para las tareas de inicio de hello dos y tarea de hello en tiempo de ejecución: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.</span><span class="sxs-lookup"><span data-stu-id="e26ab-144">If you want toouse hello version 2.x of python, set hello **PYTHON2** variable file too**on** for hello two startup tasks and hello runtime task: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.</span></span>

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

<span data-ttu-id="e26ab-145">Hola **PYTHON2** y **PYPATH** variables se deben agregar tarea de inicio del trabajo de toohello.</span><span class="sxs-lookup"><span data-stu-id="e26ab-145">hello **PYTHON2** and **PYPATH** variables must be added toohello worker startup task.</span></span> <span data-ttu-id="e26ab-146">Hola **PYPATH** variable solo se usa si hello **PYTHON2** variable se establece demasiado**en**.</span><span class="sxs-lookup"><span data-stu-id="e26ab-146">hello **PYPATH** variable is only used if hello **PYTHON2** variable is set too**on**.</span></span>

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

#### <a name="sample-servicedefinitioncsdef"></a><span data-ttu-id="e26ab-147">Archivo ServiceDefinition.csdef de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e26ab-147">Sample ServiceDefinition.csdef</span></span>
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



<span data-ttu-id="e26ab-148">A continuación, cree hello **PrepPython.ps1** y **PipInstaller.ps1** archivos Hola **. / bin** carpeta de su rol.</span><span class="sxs-lookup"><span data-stu-id="e26ab-148">Next, create hello **PrepPython.ps1** and **PipInstaller.ps1** files in hello **./bin** folder of your role.</span></span>

#### <a name="preppythonps1"></a><span data-ttu-id="e26ab-149">PrepPython.ps1</span><span class="sxs-lookup"><span data-stu-id="e26ab-149">PrepPython.ps1</span></span>
<span data-ttu-id="e26ab-150">Este script instala Python.</span><span class="sxs-lookup"><span data-stu-id="e26ab-150">This script installs python.</span></span> <span data-ttu-id="e26ab-151">Si hello **PYTHON2** variable de entorno se establece demasiado**en**, a continuación, instalar Python 2.7, en caso contrario, se instala 3.5 de Python.</span><span class="sxs-lookup"><span data-stu-id="e26ab-151">If hello **PYTHON2** environment variable is set too**on**, then Python 2.7 is installed, otherwise Python 3.5 is installed.</span></span>

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

#### <a name="pipinstallerps1"></a><span data-ttu-id="e26ab-152">PipInstaller.ps1</span><span class="sxs-lookup"><span data-stu-id="e26ab-152">PipInstaller.ps1</span></span>
<span data-ttu-id="e26ab-153">Esta secuencia de comandos llama a una pip e instala todas las dependencias de Hola de Hola **requirements.txt** archivo.</span><span class="sxs-lookup"><span data-stu-id="e26ab-153">This script calls up pip and installs all of hello dependencies in hello **requirements.txt** file.</span></span> <span data-ttu-id="e26ab-154">Si hello **PYTHON2** variable de entorno se establece demasiado**en**, a continuación, se usa Python 2.7, en caso contrario, se usa Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="e26ab-154">If hello **PYTHON2** environment variable is set too**on**, then Python 2.7 is used, otherwise Python 3.5 is used.</span></span>

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

#### <a name="modify-launchworkerps1"></a><span data-ttu-id="e26ab-155">Modificación del archivo LaunchWorker.ps1</span><span class="sxs-lookup"><span data-stu-id="e26ab-155">Modify LaunchWorker.ps1</span></span>
> [!NOTE]
> <span data-ttu-id="e26ab-156">En caso de hello de un **rol de trabajo** proyecto **LauncherWorker.ps1** archivo es necesario tooexecute Hola inicio.</span><span class="sxs-lookup"><span data-stu-id="e26ab-156">In hello case of a **worker role** project, **LauncherWorker.ps1** file is required tooexecute hello startup file.</span></span> <span data-ttu-id="e26ab-157">En un **rol web** proyecto de equipo y hello archivo de inicio se define en Propiedades del proyecto Hola.</span><span class="sxs-lookup"><span data-stu-id="e26ab-157">In a **web role** project, hello startup file is instead defined in hello project properties.</span></span>
> 
> 

<span data-ttu-id="e26ab-158">Hola **bin\LaunchWorker.ps1** creó originalmente toodo una gran cantidad de trabajo de preparación, pero realmente no funciona.</span><span class="sxs-lookup"><span data-stu-id="e26ab-158">hello **bin\LaunchWorker.ps1** was originally created toodo a lot of prep work but it doesn't really work.</span></span> <span data-ttu-id="e26ab-159">Reemplace el contenido de hello en ese archivo por hello siguiente secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="e26ab-159">Replace hello contents in that file with hello following script.</span></span>

<span data-ttu-id="e26ab-160">Esta secuencia de comandos llama hello **worker.py** archivo desde el proyecto de python.</span><span class="sxs-lookup"><span data-stu-id="e26ab-160">This script calls hello **worker.py** file from your python project.</span></span> <span data-ttu-id="e26ab-161">Si hello **PYTHON2** variable de entorno se establece demasiado**en**, a continuación, se usa Python 2.7, en caso contrario, se usa Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="e26ab-161">If hello **PYTHON2** environment variable is set too**on**, then Python 2.7 is used, otherwise Python 3.5 is used.</span></span>

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

#### <a name="pscmd"></a><span data-ttu-id="e26ab-162">ps.cmd</span><span class="sxs-lookup"><span data-stu-id="e26ab-162">ps.cmd</span></span>
<span data-ttu-id="e26ab-163">plantillas de Visual Studio Hola deberían haber creado un **ps.cmd** archivo Hola **. / bin** carpeta.</span><span class="sxs-lookup"><span data-stu-id="e26ab-163">hello Visual Studio templates should have created a **ps.cmd** file in hello **./bin** folder.</span></span> <span data-ttu-id="e26ab-164">Esta secuencia de comandos de shell llama Hola PowerShell scripts de contenedor anteriores y proporciona un registro basándose en nombre Hola Hola PowerShell contenedor llama.</span><span class="sxs-lookup"><span data-stu-id="e26ab-164">This shell script calls out hello PowerShell wrapper scripts above and provides logging based on hello name of hello PowerShell wrapper called.</span></span> <span data-ttu-id="e26ab-165">Si no se ha creado este archivo, esto es lo que debería haber en él.</span><span class="sxs-lookup"><span data-stu-id="e26ab-165">If this file wasn't created, here is what should be in it.</span></span> 

```bat
@echo off

cd /D %~dp0

if not exist "%DiagnosticStore%\LogFiles" mkdir "%DiagnosticStore%\LogFiles"
%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe -ExecutionPolicy Unrestricted -File %* >> "%DiagnosticStore%\LogFiles\%~n1.txt" 2>> "%DiagnosticStore%\LogFiles\%~n1.err.txt"
```



## <a name="run-locally"></a><span data-ttu-id="e26ab-166">Ejecución en modo local</span><span class="sxs-lookup"><span data-stu-id="e26ab-166">Run locally</span></span>
<span data-ttu-id="e26ab-167">Si establece el proyecto de servicio de nube como proyecto de inicio de hello y presione F5, servicio de nube de Hola se ejecuta en el emulador de Azure local Hola.</span><span class="sxs-lookup"><span data-stu-id="e26ab-167">If you set your cloud service project as hello startup project and press F5, hello cloud service runs in hello local Azure emulator.</span></span>

<span data-ttu-id="e26ab-168">Aunque PTVS admite iniciar en el emulador de hello, depuración (por ejemplo, los puntos de interrupción) no funciona.</span><span class="sxs-lookup"><span data-stu-id="e26ab-168">Although PTVS supports launching in hello emulator, debugging (for example, breakpoints) does not work.</span></span>

<span data-ttu-id="e26ab-169">toodebug sus roles web y de trabajo, puede establecer el proyecto de rol de hello como proyecto de inicio de Hola y que, en lugar de depuración.</span><span class="sxs-lookup"><span data-stu-id="e26ab-169">toodebug your web and worker roles, you can set hello role project as hello startup project and debug that instead.</span></span>  <span data-ttu-id="e26ab-170">También puede establecer varios proyectos de inicio.</span><span class="sxs-lookup"><span data-stu-id="e26ab-170">You can also set multiple startup projects.</span></span>  <span data-ttu-id="e26ab-171">Haga clic en soluciones de hello y, a continuación, seleccione **Establecer proyectos de inicio**.</span><span class="sxs-lookup"><span data-stu-id="e26ab-171">Right-click hello solution and then select **Set StartUp Projects**.</span></span>

![Propiedades del proyecto de inicio de la solución](./media/cloud-services-python-ptvs/startup.png)

## <a name="publish-tooazure"></a><span data-ttu-id="e26ab-173">Publicar tooAzure</span><span class="sxs-lookup"><span data-stu-id="e26ab-173">Publish tooAzure</span></span>
<span data-ttu-id="e26ab-174">toopublish, haga clic en proyecto de servicio de nube de hello en soluciones de hello y, a continuación, seleccione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="e26ab-174">toopublish, right-click hello cloud service project in hello solution and then select **Publish**.</span></span>

![Inicio de sesión para publicación de Microsoft Azure](./media/cloud-services-python-ptvs/publish-sign-in.png)

<span data-ttu-id="e26ab-176">Siga al Asistente de Hola.</span><span class="sxs-lookup"><span data-stu-id="e26ab-176">Follow hello wizard.</span></span> <span data-ttu-id="e26ab-177">Si es necesario, habilite el Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="e26ab-177">If you need to, enable remote desktop.</span></span> <span data-ttu-id="e26ab-178">Escritorio remoto es útil cuando necesita toodebug algo.</span><span class="sxs-lookup"><span data-stu-id="e26ab-178">Remote desktop is helpful when you need toodebug something.</span></span>

<span data-ttu-id="e26ab-179">Cuando haya terminado la configuración, haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="e26ab-179">When you are done configuring settings, click **Publish**.</span></span>

<span data-ttu-id="e26ab-180">Algunos progreso aparece en la ventana de salida de hello, a continuación, verá la ventana de registro de actividad de Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e26ab-180">Some progress appears in hello output window, then you'll see hello Microsoft Azure Activity Log window.</span></span>

![Ventana Registro de actividad de Microsoft Azure](./media/cloud-services-python-ptvs/publish-activity-log.png)

<span data-ttu-id="e26ab-182">Implementación tarda varios minutos toocomplete, a continuación, en la web o roles de trabajo se ejecutan en Azure.</span><span class="sxs-lookup"><span data-stu-id="e26ab-182">Deployment takes several minutes toocomplete, then your web and/or worker roles run on Azure!</span></span>

### <a name="investigate-logs"></a><span data-ttu-id="e26ab-183">Investigación de registros</span><span class="sxs-lookup"><span data-stu-id="e26ab-183">Investigate logs</span></span>
<span data-ttu-id="e26ab-184">Después de hello en la nube servicio virtual machine se inicia y se instala Python, puede mirar Hola registros toofind mensajes de error.</span><span class="sxs-lookup"><span data-stu-id="e26ab-184">After hello cloud service virtual machine starts up and installs Python, you can look at hello logs toofind any failure messages.</span></span> <span data-ttu-id="e26ab-185">Estos registros se encuentran en hello **C:\Resources\Directory\\\LogFiles {rol}** carpeta.</span><span class="sxs-lookup"><span data-stu-id="e26ab-185">These logs are located in hello **C:\Resources\Directory\\{role}\LogFiles** folder.</span></span> <span data-ttu-id="e26ab-186">**PrepPython.err.txt** tiene al menos un error en ella desde al script de Hola intenta toodetect si está instalado Python y **PipInstaller.err.txt** puede informar de una versión no actualizada de pip.</span><span class="sxs-lookup"><span data-stu-id="e26ab-186">**PrepPython.err.txt** has at least one error in it from when hello script tries toodetect if Python is installed and **PipInstaller.err.txt** may complain about an outdated version of pip.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e26ab-187">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e26ab-187">Next steps</span></span>
<span data-ttu-id="e26ab-188">Para obtener más información sobre cómo trabajar con roles de web y de trabajo en Python Tools para Visual Studio, consulte la documentación de PTVS de hello:</span><span class="sxs-lookup"><span data-stu-id="e26ab-188">For more detailed information about working with web and worker roles in Python Tools for Visual Studio, see hello PTVS documentation:</span></span>

* <span data-ttu-id="e26ab-189">[Proyectos de servicio en la nube][Cloud Service Projects]</span><span class="sxs-lookup"><span data-stu-id="e26ab-189">[Cloud Service Projects][Cloud Service Projects]</span></span>

<span data-ttu-id="e26ab-190">Para obtener más detalles sobre el uso de servicios de Azure desde los roles web y de trabajo, como el uso de almacenamiento de Azure o Bus de servicio, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="e26ab-190">For more details about using Azure services from your web and worker roles, such as using Azure Storage or Service Bus, see hello following articles:</span></span>

* <span data-ttu-id="e26ab-191">[Blob Service][Blob Service]</span><span class="sxs-lookup"><span data-stu-id="e26ab-191">[Blob Service][Blob Service]</span></span>
* <span data-ttu-id="e26ab-192">[Table Service][Table Service]</span><span class="sxs-lookup"><span data-stu-id="e26ab-192">[Table Service][Table Service]</span></span>
* <span data-ttu-id="e26ab-193">[Queue Service][Queue Service]</span><span class="sxs-lookup"><span data-stu-id="e26ab-193">[Queue Service][Queue Service]</span></span>
* <span data-ttu-id="e26ab-194">[Colas de Service Bus][Service Bus Queues]</span><span class="sxs-lookup"><span data-stu-id="e26ab-194">[Service Bus Queues][Service Bus Queues]</span></span>
* <span data-ttu-id="e26ab-195">[Temas de Service Bus][Service Bus Topics]</span><span class="sxs-lookup"><span data-stu-id="e26ab-195">[Service Bus Topics][Service Bus Topics]</span></span>

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
