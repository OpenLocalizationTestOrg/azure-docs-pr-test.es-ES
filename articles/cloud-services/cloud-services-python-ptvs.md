---
title: "Introducción a Python y a Azure Cloud Services | Microsoft Docs"
description: "Información general sobre el uso de Python Tools para Visual Studio para crear servicios en la nube de Azure, incluidos roles web y roles de trabajo."
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
ms.openlocfilehash: 7d2bc89943087323e92cf06981bbacaf4b8ff060
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="python-web-and-worker-roles-with-python-tools-for-visual-studio"></a><span data-ttu-id="c6fb7-103">Roles web y de trabajo de Python con herramientas de Python para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c6fb7-103">Python web and worker roles with Python Tools for Visual Studio</span></span>

<span data-ttu-id="c6fb7-104">En este artículo se ofrece información general sobre el uso de roles web y de trabajo de Python con [herramientas de Python para Visual Studio][Python Tools for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="c6fb7-104">This article provides an overview of using Python web and worker roles using [Python Tools for Visual Studio][Python Tools for Visual Studio].</span></span> <span data-ttu-id="c6fb7-105">Obtenga información acerca de cómo usar Visual Studio para crear e implementar un servicio en la nube básico que usa Python.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-105">Learn how to use Visual Studio to create and deploy a basic Cloud Service that uses Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6fb7-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c6fb7-106">Prerequisites</span></span>
* [<span data-ttu-id="c6fb7-107">Visual Studio 2013, 2015 o 2017</span><span class="sxs-lookup"><span data-stu-id="c6fb7-107">Visual Studio 2013, 2015, or 2017</span></span>](https://www.visualstudio.com/)
* <span data-ttu-id="c6fb7-108">[Herramientas de Python para Visual Studio][Python Tools for Visual Studio] (PTVS)</span><span class="sxs-lookup"><span data-stu-id="c6fb7-108">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS)</span></span>
* <span data-ttu-id="c6fb7-109">[Herramientas de Azure SDK para VS 2013][Azure SDK Tools for VS 2013] o</span><span class="sxs-lookup"><span data-stu-id="c6fb7-109">[Azure SDK Tools for VS 2013][Azure SDK Tools for VS 2013] or</span></span>  
<span data-ttu-id="c6fb7-110">[Herramientas de Azure SDK para VS 2015][Azure SDK Tools for VS 2015] o</span><span class="sxs-lookup"><span data-stu-id="c6fb7-110">[Azure SDK Tools for VS 2015][Azure SDK Tools for VS 2015] or</span></span>  
<span data-ttu-id="c6fb7-111">[Herramientas de Azure SDK para VS 2017][Azure SDK Tools for VS 2017]</span><span class="sxs-lookup"><span data-stu-id="c6fb7-111">[Azure SDK Tools for VS 2017][Azure SDK Tools for VS 2017]</span></span>
* <span data-ttu-id="c6fb7-112">[Python 2.7 de 32 bits][Python 2.7 32-bit] o [Python 3.5 de 32 bits][Python 3.5 32-bit]</span><span class="sxs-lookup"><span data-stu-id="c6fb7-112">[Python 2.7 32-bit][Python 2.7 32-bit] or [Python 3.5 32-bit][Python 3.5 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-are-python-web-and-worker-roles"></a><span data-ttu-id="c6fb7-113">¿Qué son los roles web y de trabajo de Python?</span><span class="sxs-lookup"><span data-stu-id="c6fb7-113">What are Python web and worker roles?</span></span>
<span data-ttu-id="c6fb7-114">Azure ofrece tres modelos de proceso para la ejecución de aplicaciones: [característica Web Apps de Azure App Service][execution model-web sites], [Azure Virtual Machines][execution model-vms], and [Azure Cloud Services][execution model-cloud services].</span><span class="sxs-lookup"><span data-stu-id="c6fb7-114">Azure provides three compute models for running applications: [Web Apps feature in Azure App Service][execution model-web sites], [Azure Virtual Machines][execution model-vms], and [Azure Cloud Services][execution model-cloud services].</span></span> <span data-ttu-id="c6fb7-115">Los tres modelos admiten Python.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-115">All three models support Python.</span></span> <span data-ttu-id="c6fb7-116">Cloud Services, que incluye roles web y de trabajo, proporciona una *Plataforma como servicio (PaaS)*.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-116">Cloud Services, which include web and worker roles, provide *Platform as a Service (PaaS)*.</span></span> <span data-ttu-id="c6fb7-117">En un servicio en la nube, un rol web ofrece un servidor web dedicado de Internet Information Services (IIS) para hospedar aplicaciones web front-end, mientras que un rol de trabajo puede ejecutar tareas asincrónicas, de ejecución prolongada o tareas perpetuas independientes de la entrada o la interacción del usuario.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-117">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server to host front end web applications, while a worker role can run asynchronous, long-running, or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="c6fb7-118">Para más información, consulte [¿Qué es un servicio en la nube?]</span><span class="sxs-lookup"><span data-stu-id="c6fb7-118">For more information, see [What is a Cloud Service?].</span></span>

> [!NOTE]
> <span data-ttu-id="c6fb7-119">*¿Desea compilar un sitio web sencillo?*</span><span class="sxs-lookup"><span data-stu-id="c6fb7-119">*Looking to build a simple website?*</span></span>
> <span data-ttu-id="c6fb7-120">Si el escenario solo requiere un sitio web de front-end sencillo, considere la posibilidad de usar la característica Web Apps ligera en Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-120">If your scenario involves just a simple website front end, consider using the lightweight Web Apps feature in Azure App Service.</span></span> <span data-ttu-id="c6fb7-121">Puede actualizar a un Servicio en la nube más adelante, cuando su sitio web sea más grande y sus requisitos cambien.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-121">You can easily upgrade to a Cloud Service as your website grows and your requirements change.</span></span> <span data-ttu-id="c6fb7-122">Consulte el <a href="/develop/python/">Centro para desarrolladores de Python</a> para obtener artículos sobre el desarrollo de la característica Web Apps en Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-122">See the <a href="/develop/python/">Python Developer Center</a> for articles that cover development of the Web Apps feature in Azure App Service.</span></span>
> <br />
> 
> 

## <a name="project-creation"></a><span data-ttu-id="c6fb7-123">Creación de un proyecto</span><span class="sxs-lookup"><span data-stu-id="c6fb7-123">Project creation</span></span>
<span data-ttu-id="c6fb7-124">En Visual Studio, puede seleccionar **Servicio en la nube de Azure** en el cuadro de diálogo **Nuevo proyecto**, en **Python**.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-124">In Visual Studio, you can select **Azure Cloud Service** in the **New Project** dialog box, under **Python**.</span></span>

![Cuadro de diálogo Nuevo proyecto](./media/cloud-services-python-ptvs/new-project-cloud-service.png)

<span data-ttu-id="c6fb7-126">En el asistente Servicio en la nube de Azure, puede crear roles web y de trabajo nuevos.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-126">In the Azure Cloud Service wizard, you can create new web and worker roles.</span></span>

![Cuadro de diálogo Servicio en la nube de Azure](./media/cloud-services-python-ptvs/new-service-wizard.png)

<span data-ttu-id="c6fb7-128">La plantilla de rol de trabajo incluye código reutilizable que conecta a una cuenta de Azure Storage o Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-128">The worker role template comes with boilerplate code to connect to an Azure storage account or Azure Service Bus.</span></span>

![Solución de servicio en la nube](./media/cloud-services-python-ptvs/worker.png)

<span data-ttu-id="c6fb7-130">Puede agregar roles web o de trabajo a un servicio en la nube que ya existe en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-130">You can add web or worker roles to an existing cloud service at any time.</span></span>  <span data-ttu-id="c6fb7-131">Puede optar por agregar proyectos existentes a su solución o por crear otros nuevos.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-131">You can choose to add existing projects in your solution, or create new ones.</span></span>

![Comando Agregar rol](./media/cloud-services-python-ptvs/add-new-or-existing-role.png)

<span data-ttu-id="c6fb7-133">Su servicio en la nube puede contener roles implementados en diferentes lenguajes.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-133">Your cloud service can contain roles implemented in different languages.</span></span>  <span data-ttu-id="c6fb7-134">Por ejemplo, puede tener un rol web de Python implementado con Django, con Python o con roles de trabajo de C#.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-134">For example, you can have a Python web role implemented using Django, with Python, or with C# worker roles.</span></span>  <span data-ttu-id="c6fb7-135">Puede comunicarse fácilmente entre sus roles usando colas del Bus de servicio o colas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-135">You can easily communicate between your roles using Service Bus queues or storage queues.</span></span>

## <a name="install-python-on-the-cloud-service"></a><span data-ttu-id="c6fb7-136">Instalación de Python en el servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="c6fb7-136">Install Python on the cloud service</span></span>
> [!WARNING]
> <span data-ttu-id="c6fb7-137">No funcionan los scripts de configuración que se instalaron con Visual Studio (en el momento en que se actualizó por última vez este artículo).</span><span class="sxs-lookup"><span data-stu-id="c6fb7-137">The setup scripts that are installed with Visual Studio (at the time this article was last updated) do not work.</span></span> <span data-ttu-id="c6fb7-138">En esta sección se describe una solución alternativa.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-138">This section describes a workaround.</span></span>
> 
> 

<span data-ttu-id="c6fb7-139">El problema principal con los scripts de configuración consiste en que instalan Python.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-139">The main problem with the setup scripts is that they do not install python.</span></span> <span data-ttu-id="c6fb7-140">En primer lugar, defina dos [tareas de inicio](cloud-services-startup-tasks.md) en el archivo [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef).</span><span class="sxs-lookup"><span data-stu-id="c6fb7-140">First, define two [startup tasks](cloud-services-startup-tasks.md) in the [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) file.</span></span> <span data-ttu-id="c6fb7-141">La primera tarea (**PrepPython.ps1**) descarga e instala el entorno de tiempo de ejecución de Python.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-141">The first task (**PrepPython.ps1**) downloads and installs the Python runtime.</span></span> <span data-ttu-id="c6fb7-142">La segunda tarea (**PipInstaller.ps1**) ejecuta pip para instalar todas las dependencias que pueda tener.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-142">The second task (**PipInstaller.ps1**) runs pip to install any dependencies you may have.</span></span>

<span data-ttu-id="c6fb7-143">Los siguientes scripts se escribieron para Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-143">The following scripts were written targeting Python 3.5.</span></span> <span data-ttu-id="c6fb7-144">Si desea usar la versión 2.x de Python, establezca el archivo de variables **PYTHON2** en **activado** para las dos tareas de inicio y la tarea en tiempo de ejecución: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-144">If you want to use the version 2.x of python, set the **PYTHON2** variable file to **on** for the two startup tasks and the runtime task: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.</span></span>

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

<span data-ttu-id="c6fb7-145">Se deben agregar las variables **PYTHON2** y **PYPATH** a la tarea de inicio del trabajo.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-145">The **PYTHON2** and **PYPATH** variables must be added to the worker startup task.</span></span> <span data-ttu-id="c6fb7-146">La variable **PYPATH** solo se usa si la variable **PYTHON2** se establece en **activado**.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-146">The **PYPATH** variable is only used if the **PYTHON2** variable is set to **on**.</span></span>

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

#### <a name="sample-servicedefinitioncsdef"></a><span data-ttu-id="c6fb7-147">Archivo ServiceDefinition.csdef de ejemplo</span><span class="sxs-lookup"><span data-stu-id="c6fb7-147">Sample ServiceDefinition.csdef</span></span>
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



<span data-ttu-id="c6fb7-148">A continuación, cree los archivos **PrepPython.ps1** y **PipInstaller.ps1** en la carpeta **./bin** del rol.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-148">Next, create the **PrepPython.ps1** and **PipInstaller.ps1** files in the **./bin** folder of your role.</span></span>

#### <a name="preppythonps1"></a><span data-ttu-id="c6fb7-149">PrepPython.ps1</span><span class="sxs-lookup"><span data-stu-id="c6fb7-149">PrepPython.ps1</span></span>
<span data-ttu-id="c6fb7-150">Este script instala Python.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-150">This script installs python.</span></span> <span data-ttu-id="c6fb7-151">Si la variable de entorno **PYTHON2** se establece en **on,** (activado) se instala Python 2.7 o, en caso contrario, se instala Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-151">If the **PYTHON2** environment variable is set to **on**, then Python 2.7 is installed, otherwise Python 3.5 is installed.</span></span>

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

        Write-Output "Not found, downloading $url to $outFile$nl"
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

#### <a name="pipinstallerps1"></a><span data-ttu-id="c6fb7-152">PipInstaller.ps1</span><span class="sxs-lookup"><span data-stu-id="c6fb7-152">PipInstaller.ps1</span></span>
<span data-ttu-id="c6fb7-153">Este script se llama pip e instala todas las dependencias en el archivo **requirements.txt**.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-153">This script calls up pip and installs all of the dependencies in the **requirements.txt** file.</span></span> <span data-ttu-id="c6fb7-154">Si la variable de entorno **PYTHON2** se establece en **on,** (activado) se usa Python 2.7 o, en caso contrario, se usa Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-154">If the **PYTHON2** environment variable is set to **on**, then Python 2.7 is used, otherwise Python 3.5 is used.</span></span>

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

#### <a name="modify-launchworkerps1"></a><span data-ttu-id="c6fb7-155">Modificación del archivo LaunchWorker.ps1</span><span class="sxs-lookup"><span data-stu-id="c6fb7-155">Modify LaunchWorker.ps1</span></span>
> [!NOTE]
> <span data-ttu-id="c6fb7-156">En caso de un proyecto de **rol de trabajo**, se necesita el archivo **LauncherWorker.ps1** para ejecutar el archivo de inicio.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-156">In the case of a **worker role** project, **LauncherWorker.ps1** file is required to execute the startup file.</span></span> <span data-ttu-id="c6fb7-157">En un proyecto de **rol web**, el archivo de inicio se define por el contrario en las propiedades del proyecto.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-157">In a **web role** project, the startup file is instead defined in the project properties.</span></span>
> 
> 

<span data-ttu-id="c6fb7-158">El archivo **bin\LaunchWorker.ps1** se creó originalmente para hacer una gran cantidad de trabajo de preparación pero realmente no funciona.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-158">The **bin\LaunchWorker.ps1** was originally created to do a lot of prep work but it doesn't really work.</span></span> <span data-ttu-id="c6fb7-159">Reemplace el contenido del archivo por el script siguiente.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-159">Replace the contents in that file with the following script.</span></span>

<span data-ttu-id="c6fb7-160">Este script llama al archivo **worker.py** desde el proyecto de Python.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-160">This script calls the **worker.py** file from your python project.</span></span> <span data-ttu-id="c6fb7-161">Si la variable de entorno **PYTHON2** se establece en **on,** (activado) se usa Python 2.7 o, en caso contrario, se usa Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-161">If the **PYTHON2** environment variable is set to **on**, then Python 2.7 is used, otherwise Python 3.5 is used.</span></span>

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

    # Customize to your local dev environment

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

#### <a name="pscmd"></a><span data-ttu-id="c6fb7-162">ps.cmd</span><span class="sxs-lookup"><span data-stu-id="c6fb7-162">ps.cmd</span></span>
<span data-ttu-id="c6fb7-163">Las plantillas de Visual Studio deben haber creado un archivo **ps.cmd** en la carpeta **./bin**.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-163">The Visual Studio templates should have created a **ps.cmd** file in the **./bin** folder.</span></span> <span data-ttu-id="c6fb7-164">Este script de shell llama a los scripts anteriores del contenedor de PowerShell y proporciona un registro basado en el nombre del contenedor de PowerShell que se ha llamado.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-164">This shell script calls out the PowerShell wrapper scripts above and provides logging based on the name of the PowerShell wrapper called.</span></span> <span data-ttu-id="c6fb7-165">Si no se ha creado este archivo, esto es lo que debería haber en él.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-165">If this file wasn't created, here is what should be in it.</span></span> 

```bat
@echo off

cd /D %~dp0

if not exist "%DiagnosticStore%\LogFiles" mkdir "%DiagnosticStore%\LogFiles"
%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe -ExecutionPolicy Unrestricted -File %* >> "%DiagnosticStore%\LogFiles\%~n1.txt" 2>> "%DiagnosticStore%\LogFiles\%~n1.err.txt"
```



## <a name="run-locally"></a><span data-ttu-id="c6fb7-166">Ejecución en modo local</span><span class="sxs-lookup"><span data-stu-id="c6fb7-166">Run locally</span></span>
<span data-ttu-id="c6fb7-167">Si establece su proyecto de servicio en la nube como proyecto de inicio y presiona F5, el servicio en la nube se ejecuta en el emulador de Azure local.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-167">If you set your cloud service project as the startup project and press F5, the cloud service runs in the local Azure emulator.</span></span>

<span data-ttu-id="c6fb7-168">Aunque PTVS admite el inicio en el emulador, la depuración (por ejemplo, puntos de interrupción) no funciona.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-168">Although PTVS supports launching in the emulator, debugging (for example, breakpoints) does not work.</span></span>

<span data-ttu-id="c6fb7-169">Para depurar roles web y de trabajo, puede establecer el proyecto de rol como proyecto de inicio y depurarlo.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-169">To debug your web and worker roles, you can set the role project as the startup project and debug that instead.</span></span>  <span data-ttu-id="c6fb7-170">También puede establecer varios proyectos de inicio.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-170">You can also set multiple startup projects.</span></span>  <span data-ttu-id="c6fb7-171">Haga clic con el botón derecho en la solución y luego seleccione **Establecer proyectos de inicio**.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-171">Right-click the solution and then select **Set StartUp Projects**.</span></span>

![Propiedades del proyecto de inicio de la solución](./media/cloud-services-python-ptvs/startup.png)

## <a name="publish-to-azure"></a><span data-ttu-id="c6fb7-173">Publicación en Azure</span><span class="sxs-lookup"><span data-stu-id="c6fb7-173">Publish to Azure</span></span>
<span data-ttu-id="c6fb7-174">Para publicar, haga clic con el botón derecho en el proyecto del servicio en la nube de la solución y luego seleccione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-174">To publish, right-click the cloud service project in the solution and then select **Publish**.</span></span>

![Inicio de sesión para publicación de Microsoft Azure](./media/cloud-services-python-ptvs/publish-sign-in.png)

<span data-ttu-id="c6fb7-176">Siga las instrucciones del asistente.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-176">Follow the wizard.</span></span> <span data-ttu-id="c6fb7-177">Si es necesario, habilite el Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-177">If you need to, enable remote desktop.</span></span> <span data-ttu-id="c6fb7-178">El Escritorio remoto es útil cuando necesita depurar algo.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-178">Remote desktop is helpful when you need to debug something.</span></span>

<span data-ttu-id="c6fb7-179">Cuando haya terminado la configuración, haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-179">When you are done configuring settings, click **Publish**.</span></span>

<span data-ttu-id="c6fb7-180">En la ventana de salida se ve cierto progreso y después se verá la ventana Registro de actividad de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-180">Some progress appears in the output window, then you'll see the Microsoft Azure Activity Log window.</span></span>

![Ventana Registro de actividad de Microsoft Azure](./media/cloud-services-python-ptvs/publish-activity-log.png)

<span data-ttu-id="c6fb7-182">La implementación tarda varios minutos y después sus roles web y/o de trabajo estarán ejecutándose en Azure.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-182">Deployment takes several minutes to complete, then your web and/or worker roles run on Azure!</span></span>

### <a name="investigate-logs"></a><span data-ttu-id="c6fb7-183">Investigación de registros</span><span class="sxs-lookup"><span data-stu-id="c6fb7-183">Investigate logs</span></span>
<span data-ttu-id="c6fb7-184">Después de que la máquina virtual del servicio en la nube se inicie e instale Python, puede mirar los registros para buscar mensajes de error.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-184">After the cloud service virtual machine starts up and installs Python, you can look at the logs to find any failure messages.</span></span> <span data-ttu-id="c6fb7-185">Estos registros se encuentran en la carpeta **C:\Resources\Directory\\{role}\LogFiles**.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-185">These logs are located in the **C:\Resources\Directory\\{role}\LogFiles** folder.</span></span> <span data-ttu-id="c6fb7-186">**PrepPython.err.txt** tiene al menos un error cuando el script intente detectar si está instalado Python y **PipInstaller.err.txt** puede informar acerca de una versión obsoleta de pip.</span><span class="sxs-lookup"><span data-stu-id="c6fb7-186">**PrepPython.err.txt** has at least one error in it from when the script tries to detect if Python is installed and **PipInstaller.err.txt** may complain about an outdated version of pip.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6fb7-187">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c6fb7-187">Next steps</span></span>
<span data-ttu-id="c6fb7-188">Para obtener información detallada sobre el trabajo con roles web y de trabajo en Python Tools para Visual Studio, consulte la documentación de PTVS:</span><span class="sxs-lookup"><span data-stu-id="c6fb7-188">For more detailed information about working with web and worker roles in Python Tools for Visual Studio, see the PTVS documentation:</span></span>

* <span data-ttu-id="c6fb7-189">[Proyectos de servicio en la nube][Cloud Service Projects]</span><span class="sxs-lookup"><span data-stu-id="c6fb7-189">[Cloud Service Projects][Cloud Service Projects]</span></span>

<span data-ttu-id="c6fb7-190">Para más información sobre el uso de servicios de Azure desde roles web y de trabajo, como el uso de Azure Storage o Service Bus, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="c6fb7-190">For more details about using Azure services from your web and worker roles, such as using Azure Storage or Service Bus, see the following articles:</span></span>

* <span data-ttu-id="c6fb7-191">[Blob Service][Blob Service]</span><span class="sxs-lookup"><span data-stu-id="c6fb7-191">[Blob Service][Blob Service]</span></span>
* <span data-ttu-id="c6fb7-192">[Table Service][Table Service]</span><span class="sxs-lookup"><span data-stu-id="c6fb7-192">[Table Service][Table Service]</span></span>
* <span data-ttu-id="c6fb7-193">[Queue Service][Queue Service]</span><span class="sxs-lookup"><span data-stu-id="c6fb7-193">[Queue Service][Queue Service]</span></span>
* <span data-ttu-id="c6fb7-194">[Colas de Service Bus][Service Bus Queues]</span><span class="sxs-lookup"><span data-stu-id="c6fb7-194">[Service Bus Queues][Service Bus Queues]</span></span>
* <span data-ttu-id="c6fb7-195">[Temas de Service Bus][Service Bus Topics]</span><span class="sxs-lookup"><span data-stu-id="c6fb7-195">[Service Bus Topics][Service Bus Topics]</span></span>

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
