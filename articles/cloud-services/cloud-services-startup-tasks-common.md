---
title: Tareas de inicio comunes para Cloud Services | Microsoft Docs
description: "Este artículo proporciona algunos ejemplos de tareas de inicio comunes que puede realizar en el rol web o rol de trabajo del servicio en la nube."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: a7095dad-1ee7-4141-bc6a-ef19a6e570f1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: cee23da5b089b02bfc0ef10afd60f0f2272585b1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="common-cloud-service-startup-tasks"></a><span data-ttu-id="16bff-103">Tareas de inicio comunes para los servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="16bff-103">Common Cloud Service startup tasks</span></span>
<span data-ttu-id="16bff-104">Este artículo proporciona algunos ejemplos de tareas comunes de inicio que puede realizar en su servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="16bff-104">This article provides some examples of common startup tasks you may want to perform in your cloud service.</span></span> <span data-ttu-id="16bff-105">Puede usar las tareas de inicio para realizar operaciones antes de que se inicie un rol.</span><span class="sxs-lookup"><span data-stu-id="16bff-105">You can use startup tasks to perform operations before a role starts.</span></span> <span data-ttu-id="16bff-106">Estas operaciones incluyen la instalación de un componente, el registro de componentes COM, el establecimiento de las claves del registro o el inicio de un proceso de ejecución largo.</span><span class="sxs-lookup"><span data-stu-id="16bff-106">Operations that you might want to perform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span> 

<span data-ttu-id="16bff-107">Consulte [este artículo](cloud-services-startup-tasks.md) para entender cómo funcionan las tareas de inicio y de forma específica cómo crear las entradas que definen una tarea de inicio.</span><span class="sxs-lookup"><span data-stu-id="16bff-107">See [this article](cloud-services-startup-tasks.md) to understand how startup tasks work, and specifically how to create the entries that define a startup task.</span></span>

> [!NOTE]
> <span data-ttu-id="16bff-108">Las tareas de inicio no son aplicables a las máquinas virtuales, solo a los roles web y de trabajo del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="16bff-108">Startup tasks are not applicable to Virtual Machines, only to Cloud Service Web and Worker roles.</span></span>
> 

## <a name="define-environment-variables-before-a-role-starts"></a><span data-ttu-id="16bff-109">Definición de variables de entorno antes de que se inicie un rol</span><span class="sxs-lookup"><span data-stu-id="16bff-109">Define environment variables before a role starts</span></span>
<span data-ttu-id="16bff-110">Si necesita las variables de entorno definidas para una tarea específica, use el elemento [Environment] dentro del elemento [Task].</span><span class="sxs-lookup"><span data-stu-id="16bff-110">If you need environment variables defined for a specific task, use the [Environment] element inside the [Task] element.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WorkerRole name="WorkerRole1">
        ...
        <Startup>
            <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
                <Environment>
                    <Variable name="MyEnvironmentVariable" value="MyVariableValue" />
                </Environment>
            </Task>
        </Startup>
    </WorkerRole>
</ServiceDefinition>
```

<span data-ttu-id="16bff-111">También se pueden usar un [valor válido xPath en Azure](cloud-services-role-config-xpath.md) para hacer referencia a algo acerca de la implementación.</span><span class="sxs-lookup"><span data-stu-id="16bff-111">Variables can also use a [valid Azure XPath value](cloud-services-role-config-xpath.md) to reference something about the deployment.</span></span> <span data-ttu-id="16bff-112">En lugar de usar el atributo `value` de atributo, defina un elemento secundario [RoleInstanceValue] .</span><span class="sxs-lookup"><span data-stu-id="16bff-112">Instead of using the `value` attribute, define a [RoleInstanceValue] child element.</span></span>

```xml
<Variable name="PathToStartupStorage">
    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
</Variable>
```


## <a name="configure-iis-startup-with-appcmdexe"></a><span data-ttu-id="16bff-113">Configuración del inicio IIS con AppCmd.exe</span><span class="sxs-lookup"><span data-stu-id="16bff-113">Configure IIS startup with AppCmd.exe</span></span>
<span data-ttu-id="16bff-114">La herramienta de línea de comandos [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) puede usarse para administrar la configuración de IIS en el inicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="16bff-114">The [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) command-line tool can be used to manage IIS settings at startup on Azure.</span></span> <span data-ttu-id="16bff-115">*AppCmd.exe* proporciona acceso práctico a través de la línea de comandos a los ajustes de configuración para su uso en las tareas de inicio en Azure.</span><span class="sxs-lookup"><span data-stu-id="16bff-115">*AppCmd.exe* provides convenient, command-line access to configuration settings for use in startup tasks on Azure.</span></span> <span data-ttu-id="16bff-116">Con *AppCmd.exe*se pueden agregar modificar o quitar ajustes del sitio web para aplicaciones y sitios.</span><span class="sxs-lookup"><span data-stu-id="16bff-116">Using *AppCmd.exe*, Website settings can be added, modified, or removed for applications and sites.</span></span>

<span data-ttu-id="16bff-117">Sin embargo, hay algunos aspectos que hay que tener en cuenta cuando se use *AppCmd.exe* como una tarea de inicio:</span><span class="sxs-lookup"><span data-stu-id="16bff-117">However, there are a few things to watch out for in the use of *AppCmd.exe* as a startup task:</span></span>

* <span data-ttu-id="16bff-118">Las tareas de inicio se pueden ejecutar más de una vez entre reinicios.</span><span class="sxs-lookup"><span data-stu-id="16bff-118">Startup tasks can be run more than once between reboots.</span></span> <span data-ttu-id="16bff-119">Por ejemplo, cuando un rol se recicla.</span><span class="sxs-lookup"><span data-stu-id="16bff-119">For instance, when a role recycles.</span></span>
* <span data-ttu-id="16bff-120">Si una acción *AppCmd.exe* se realiza más de una vez, puede generar un error.</span><span class="sxs-lookup"><span data-stu-id="16bff-120">If a *AppCmd.exe* action is performed more than once, it may generate an error.</span></span> <span data-ttu-id="16bff-121">Por ejemplo, si intenta agregar una sección a *Web.config* dos veces, podría producirse un error.</span><span class="sxs-lookup"><span data-stu-id="16bff-121">For example, attempting to add a section to *Web.config* twice could generate an error.</span></span>
* <span data-ttu-id="16bff-122">Si las tareas de inicio devuelven un código de salida distinto de cero o un **errorlevel**se producirá un error en las mismas.</span><span class="sxs-lookup"><span data-stu-id="16bff-122">Startup tasks fail if they return a non-zero exit code or **errorlevel**.</span></span> <span data-ttu-id="16bff-123">Por ejemplo, cuando *AppCmd.exe* genera un error.</span><span class="sxs-lookup"><span data-stu-id="16bff-123">For example, when *AppCmd.exe* generates an error.</span></span>

<span data-ttu-id="16bff-124">Es recomendable comprobar las respuestas **errorlevel** después de llamar a *AppCmd.exe*, esto es sencillo si encapsula la llamada a *AppCmd.exe* con un archivo *.cmd*.</span><span class="sxs-lookup"><span data-stu-id="16bff-124">It is a good practice to check the **errorlevel** after calling *AppCmd.exe*, which is easy to do if you wrap the call to *AppCmd.exe* with a *.cmd* file.</span></span> <span data-ttu-id="16bff-125">Si se detecta una respuesta **errorlevel** conocida, puede ignorarla o devolverla.</span><span class="sxs-lookup"><span data-stu-id="16bff-125">If you detect a known **errorlevel** response, you can ignore it, or pass it back.</span></span>

<span data-ttu-id="16bff-126">Los mensajes errorlevel que devuelve *AppCmd.exe* se enumeran en el archivo winerror.h y también se pueden ver en [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).</span><span class="sxs-lookup"><span data-stu-id="16bff-126">The errorlevel returned by *AppCmd.exe* are listed in the winerror.h file, and can also be seen on [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).</span></span>

### <a name="example-of-managing-the-error-level"></a><span data-ttu-id="16bff-127">Ejemplo de administración del nivel de error</span><span class="sxs-lookup"><span data-stu-id="16bff-127">Example of managing the error level</span></span>
<span data-ttu-id="16bff-128">Este ejemplo agrega una sección de compresión y una entrada de compresión para JSON al archivo *Web.config* con control de errores y registro.</span><span class="sxs-lookup"><span data-stu-id="16bff-128">This example adds a compression section and a compression entry for JSON to the *Web.config* file, with error handling and logging.</span></span>

<span data-ttu-id="16bff-129">Las secciones relevantes del archivo [ServiceDefinition.csdef] se muestran aquí, e incluyen la configuración del atributo [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) como `elevated` para dar a *AppCmd.exe* permisos suficientes para cambiar la configuración en el archivo *Web.config*:</span><span class="sxs-lookup"><span data-stu-id="16bff-129">The relevant sections of the [ServiceDefinition.csdef] file are shown here, which include setting the [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) attribute to `elevated` to give *AppCmd.exe* sufficient permissions to change the settings in the *Web.config* file:</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WorkerRole name="WorkerRole1">
        ...
        <Startup>
            <Task commandLine="Startup.cmd" executionContext="elevated" taskType="simple" />
        </Startup>
    </WorkerRole>
</ServiceDefinition>
```

<span data-ttu-id="16bff-130">El archivo por lotes *Startup.cmd* usa *AppCmd.exe* para agregar una sección de comprensión y una entrada de comprensión para JSON al archivo *Web.config*.</span><span class="sxs-lookup"><span data-stu-id="16bff-130">The *Startup.cmd* batch file uses *AppCmd.exe* to add a compression section and a compression entry for JSON to the *Web.config* file.</span></span> <span data-ttu-id="16bff-131">El **errorlevel** esperado de 183 se establece en cero mediante el programa de línea de comandos VERIFY.EXE.</span><span class="sxs-lookup"><span data-stu-id="16bff-131">The expected **errorlevel** of 183 is set to zero using the VERIFY.EXE command-line program.</span></span> <span data-ttu-id="16bff-132">Los errorlevels inesperados se registran en StartupErrorLog.txt.</span><span class="sxs-lookup"><span data-stu-id="16bff-132">Unexpected errorlevels are logged to StartupErrorLog.txt.</span></span>

```cmd
REM   *** Add a compression section to the Web.config file. ***
%windir%\system32\inetsrv\appcmd set config /section:urlCompression /doDynamicCompression:True /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1

REM   ERRORLEVEL 183 occurs when trying to add a section that already exists. This error is expected if this
REM   batch file were executed twice. This can occur and must be accounted for in a Azure startup
REM   task. To handle this situation, set the ERRORLEVEL to zero by using the Verify command. The Verify
REM   command will safely set the ERRORLEVEL to zero.
IF %ERRORLEVEL% EQU 183 DO VERIFY > NUL

REM   If the ERRORLEVEL is not zero at this point, some other error occurred.
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding a compression section to the Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Add compression for json. ***
%windir%\system32\inetsrv\appcmd set config  -section:system.webServer/httpCompression /+"dynamicTypes.[mimeType='application/json; charset=utf-8',enabled='True']" /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1
IF %ERRORLEVEL% EQU 183 VERIFY > NUL
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding the JSON compression type to the Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Exit batch file. ***
EXIT /b 0

REM   *** Log error and exit ***
:ErrorExit
REM   Report the date, time, and ERRORLEVEL of the error.
DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
ECHO An error occurred during startup. ERRORLEVEL = %ERRORLEVEL% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT %ERRORLEVEL%
```

## <a name="add-firewall-rules"></a><span data-ttu-id="16bff-133">Adición de reglas de firewall</span><span class="sxs-lookup"><span data-stu-id="16bff-133">Add firewall rules</span></span>
<span data-ttu-id="16bff-134">A efectos prácticos, hay dos firewalls en Azure.</span><span class="sxs-lookup"><span data-stu-id="16bff-134">In Azure, there are effectively two firewalls.</span></span> <span data-ttu-id="16bff-135">El primer firewall controla las conexiones entre la máquina virtual y el exterior.</span><span class="sxs-lookup"><span data-stu-id="16bff-135">The first firewall controls connections between the virtual machine and the outside world.</span></span> <span data-ttu-id="16bff-136">El firewall se controla mediante el elemento [EndPoints] en el archivo [ServiceDefinition.csdef].</span><span class="sxs-lookup"><span data-stu-id="16bff-136">This firewall is controlled by the [EndPoints] element in the [ServiceDefinition.csdef] file.</span></span>

<span data-ttu-id="16bff-137">El segundo firewall controla las conexiones entre la máquina virtual y los procesos dentro de esa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="16bff-137">The second firewall controls connections between the virtual machine and the processes within that virtual machine.</span></span> <span data-ttu-id="16bff-138">Este firewall puede controlarse mediante la herramienta de línea de comandos `netsh advfirewall firewall`.</span><span class="sxs-lookup"><span data-stu-id="16bff-138">This firewall can be controlled by the `netsh advfirewall firewall` command-line tool.</span></span>

<span data-ttu-id="16bff-139">Azure crea reglas de firewall para los procesos que se inician en sus roles.</span><span class="sxs-lookup"><span data-stu-id="16bff-139">Azure creates firewall rules for the processes started within your roles.</span></span> <span data-ttu-id="16bff-140">Por ejemplo, cuando se inicia un servicio o programa, Azure crea automáticamente las reglas de firewall necesarias para permitir que el servicio se comunique con Internet.</span><span class="sxs-lookup"><span data-stu-id="16bff-140">For example, when you start a service or program, Azure automatically creates the necessary firewall rules to allow that service to communicate with the Internet.</span></span> <span data-ttu-id="16bff-141">Sin embargo, si crea un servicio que se inicia con un proceso fuera de su rol (por ejemplo, un servicio COM+ o una tarea programada de Windows), tendrá que crear manualmente una regla de firewall para permitir el acceso a ese servicio.</span><span class="sxs-lookup"><span data-stu-id="16bff-141">However, if you create a service that is started by a process outside your role (like a COM+ service or a Windows Scheduled Task), you need to manually create a firewall rule to allow access to that service.</span></span> <span data-ttu-id="16bff-142">Estas reglas de firewall pueden crearse mediante una tarea de inicio.</span><span class="sxs-lookup"><span data-stu-id="16bff-142">These firewall rules can be created by using a startup task.</span></span>

<span data-ttu-id="16bff-143">Una tarea de inicio que crea una regla de firewall tiene que tener para el atributo [executionContext][Task] un valor **elevated**se producirá un error en las mismas.</span><span class="sxs-lookup"><span data-stu-id="16bff-143">A startup task that creates a firewall rule must have an [executionContext][Task] of **elevated**.</span></span> <span data-ttu-id="16bff-144">Agregue la siguiente tarea de inicio al archivo [ServiceDefinition.csdef] .</span><span class="sxs-lookup"><span data-stu-id="16bff-144">Add the following startup task to the [ServiceDefinition.csdef] file.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WorkerRole name="WorkerRole1">
        ...
        <Startup>
            <Task commandLine="AddFirewallRules.cmd" executionContext="elevated" taskType="simple" />
        </Startup>
    </WorkerRole>
</ServiceDefinition>
```

<span data-ttu-id="16bff-145">Para agregar la regla de firewall, tiene que usar los comandos `netsh advfirewall firewall` adecuados en el archivo por lotes de inicio.</span><span class="sxs-lookup"><span data-stu-id="16bff-145">To add the firewall rule, you must use the appropriate `netsh advfirewall firewall` commands in your startup batch file.</span></span> <span data-ttu-id="16bff-146">En este ejemplo, la tarea de inicio requiere seguridad y cifrado para el puerto TCP 80.</span><span class="sxs-lookup"><span data-stu-id="16bff-146">In this example, the startup task requires security and encryption for TCP port 80.</span></span>

```cmd
REM   Add a firewall rule in a startup task.

REM   Add an inbound rule requiring security and encryption for TCP port 80 traffic.
netsh advfirewall firewall add rule name="Require Encryption for Inbound TCP/80" protocol=TCP dir=in localport=80 security=authdynenc action=allow >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return the errorlevel.
EXIT /B %errorlevel%
```

## <a name="block-a-specific-ip-address"></a><span data-ttu-id="16bff-147">Bloqueo de una dirección IP específica</span><span class="sxs-lookup"><span data-stu-id="16bff-147">Block a specific IP address</span></span>
<span data-ttu-id="16bff-148">Puede restringir un acceso de rol web de Azure a un conjunto de direcciones IP especificadas modificando su archivo **web.config** de IIS.</span><span class="sxs-lookup"><span data-stu-id="16bff-148">You can restrict an Azure web role access to a set of specified IP addresses by modifying your IIS **web.config** file.</span></span> <span data-ttu-id="16bff-149">También debe usar un archivo de comandos que desbloquee la sección **ipSecurity** del archivo **ApplicationHost.config**.</span><span class="sxs-lookup"><span data-stu-id="16bff-149">You also need to use a command file which unlocks the **ipSecurity** section of the **ApplicationHost.config** file.</span></span>

<span data-ttu-id="16bff-150">Para desbloquear la sección **ipSecurity** del archivo **ApplicationHost.config**, cree un archivo de comandos que se ejecute al iniciarse el rol.</span><span class="sxs-lookup"><span data-stu-id="16bff-150">To do unlock the **ipSecurity** section of the **ApplicationHost.config** file, create a command file that runs at role start.</span></span> <span data-ttu-id="16bff-151">Cree una carpeta en el nivel raíz del rol web llamada **startup** y, dentro de esta carpeta, cree un archivo por lotes denominado **startup.cmd**.</span><span class="sxs-lookup"><span data-stu-id="16bff-151">Create a folder at the root level of your web role called **startup** and, within this folder, create a batch file called **startup.cmd**.</span></span> <span data-ttu-id="16bff-152">Agregue este archivo a su proyecto de Visual Studio y establezca las propiedades en **Copiar siempre** para asegurarse de que se incluye en el paquete.</span><span class="sxs-lookup"><span data-stu-id="16bff-152">Add this file to your Visual Studio project and set the properties to **Copy Always** to ensure that it is included in your package.</span></span>

<span data-ttu-id="16bff-153">Agregue la siguiente tarea de inicio al archivo [ServiceDefinition.csdef] .</span><span class="sxs-lookup"><span data-stu-id="16bff-153">Add the following startup task to the [ServiceDefinition.csdef] file.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WebRole name="WebRole1">
        ...
        <Startup>
            <Task commandLine="startup.cmd" executionContext="elevated" />
        </Startup>
    </WebRole>
</ServiceDefinition>
```

<span data-ttu-id="16bff-154">Agregue este comando al archivo **startup.cmd** :</span><span class="sxs-lookup"><span data-stu-id="16bff-154">Add this command to the **startup.cmd** file:</span></span>

```cmd
@echo off
@echo Installing "IPv4 Address and Domain Restrictions" feature 
powershell -ExecutionPolicy Unrestricted -command "Install-WindowsFeature Web-IP-Security"
@echo Unlocking configuration for "IPv4 Address and Domain Restrictions" feature 
%windir%\system32\inetsrv\AppCmd.exe unlock config -section:system.webServer/security/ipSecurity
```

<span data-ttu-id="16bff-155">Esta tarea hace que el archivo por lotes **startup.cmd** se ejecute cada vez que se inicializa el rol web, asegurándose de que la sección **ipSecurity** necesaria está desbloqueada.</span><span class="sxs-lookup"><span data-stu-id="16bff-155">This task causes the **startup.cmd** batch file to be run every time the web role is initialized, ensuring that the required **ipSecurity** section is unlocked.</span></span>

<span data-ttu-id="16bff-156">Por último, modifique la [sección system.webServer](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) del archivo de rol web **web.config** para agregar una lista de direcciones IP a las que se concede acceso, tal como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="16bff-156">Finally, modify the [system.webServer section](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) your web role’s **web.config** file to add a list of IP addresses that are granted access, as shown in the following example:</span></span>

<span data-ttu-id="16bff-157">Esta configuración de ejemplo **permite** a todas las direcciones IP el acceso al servidor con la excepción de las dos definidas</span><span class="sxs-lookup"><span data-stu-id="16bff-157">This sample config **allows** all IPs to access the server except the two defined</span></span>

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are granted access-->
    <ipSecurity>
        <!--The following IP addresses are denied access-->
        <add allowed="false" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="false" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

<span data-ttu-id="16bff-158">Esta configuración de ejemplo **deniega** a todas las direcciones IP el acceso al servidor con la excepción de las dos definidas</span><span class="sxs-lookup"><span data-stu-id="16bff-158">This sample config **denies** all IPs from accessing the server except for the two defined.</span></span>

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are denied access-->
    <ipSecurity allowUnlisted="false">
        <!--The following IP addresses are granted access-->
        <add allowed="true" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="true" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

## <a name="create-a-powershell-startup-task"></a><span data-ttu-id="16bff-159">Creación de una tarea de inicio de PowerShell</span><span class="sxs-lookup"><span data-stu-id="16bff-159">Create a PowerShell startup task</span></span>
<span data-ttu-id="16bff-160">No se puede llamar directamente a los scripts de Windows PowerShell desde el archivo [ServiceDefinition.csdef] , pero se pueden invocar desde dentro de un archivo por lotes de inicio.</span><span class="sxs-lookup"><span data-stu-id="16bff-160">Windows PowerShell scripts cannot be called directly from the [ServiceDefinition.csdef] file, but they can be invoked from within a startup batch file.</span></span>

<span data-ttu-id="16bff-161">PowerShell (de forma predeterminada) no ejecuta scripts sin firmar.</span><span class="sxs-lookup"><span data-stu-id="16bff-161">PowerShell (by default) does not run unsigned scripts.</span></span> <span data-ttu-id="16bff-162">A menos que firme su script, tendrá que configurar PowerShell para ejecutar scripts sin firmar.</span><span class="sxs-lookup"><span data-stu-id="16bff-162">Unless you sign your script, you need to configure PowerShell to run unsigned scripts.</span></span> <span data-ttu-id="16bff-163">Para ejecutar scripts sin firmar, **ExecutionPolicy** tiene que establecerse en **Unrestricted**.</span><span class="sxs-lookup"><span data-stu-id="16bff-163">To run unsigned scripts, the **ExecutionPolicy** must be set to **Unrestricted**.</span></span> <span data-ttu-id="16bff-164">El ajuste **ExecutionPolicy** que vaya a usar se basa en la versión de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="16bff-164">The **ExecutionPolicy** setting that you use is based on the version of Windows PowerShell.</span></span>

```cmd
REM   Run an unsigned PowerShell script and log the output
PowerShell -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return the errorlevel.
EXIT /B %errorlevel%
```

<span data-ttu-id="16bff-165">Si usa un SO invitado que ejecuta PowerShell 2.0 o 1.0 puede forzar la ejecución de la versión 2 y si no está disponible, use la versión 1.</span><span class="sxs-lookup"><span data-stu-id="16bff-165">If you're using a Guest OS that is runs PowerShell 2.0 or 1.0 you can force version 2 to run, and if unavailable, use version 1.</span></span>

```cmd
REM   Attempt to set the execution policy by using PowerShell version 2.0 syntax.
PowerShell -Version 2.0 -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If PowerShell version 2.0 isn't available. Set the execution policy by using the PowerShell
IF %ERRORLEVEL% EQU -393216 (
   PowerShell -Command "Set-ExecutionPolicy Unrestricted" >> "%TEMP%\StartupLog.txt" 2>&1
   PowerShell .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1
)

REM   If an error occurred, return the errorlevel.
EXIT /B %errorlevel%
```

## <a name="create-files-in-local-storage-from-a-startup-task"></a><span data-ttu-id="16bff-166">Creación de archivos de una tarea de inicio en un almacenamiento local</span><span class="sxs-lookup"><span data-stu-id="16bff-166">Create files in local storage from a startup task</span></span>
<span data-ttu-id="16bff-167">Puede usar un recurso de almacenamiento local para almacenar los archivos creados por una tarea de inicio a la que más adelante tiene acceso una aplicación.</span><span class="sxs-lookup"><span data-stu-id="16bff-167">You can use a local storage resource to store files created by your startup task that is accessed later by your application.</span></span>

<span data-ttu-id="16bff-168">Para crear el recurso de almacenamiento local, agregue una sección [LocalResources] al archivo [ServiceDefinition.csdef] y, a continuación, agregue el elemento secundario [LocalStorage].</span><span class="sxs-lookup"><span data-stu-id="16bff-168">To create the local storage resource, add a [LocalResources] section to the [ServiceDefinition.csdef] file and then add the [LocalStorage] child element.</span></span> <span data-ttu-id="16bff-169">Asigne al recurso de almacenamiento local un nombre único y un tamaño adecuado para la tarea de inicio.</span><span class="sxs-lookup"><span data-stu-id="16bff-169">Give the local storage resource a unique name and an appropriate size for your startup task.</span></span>

<span data-ttu-id="16bff-170">Para usar un recurso de almacenamiento local en la tarea de inicio, tiene que crear una variable de entorno para hacer referencia a la ubicación del recurso de almacenamiento local.</span><span class="sxs-lookup"><span data-stu-id="16bff-170">To use a local storage resource in your startup task, you need to create an environment variable to reference the local storage resource location.</span></span> <span data-ttu-id="16bff-171">A continuación, la tarea de inicio y la aplicación pueden leer y escribir archivos en el recurso de almacenamiento local.</span><span class="sxs-lookup"><span data-stu-id="16bff-171">Then the startup task and the application are able to read and write files to the local storage resource.</span></span>

<span data-ttu-id="16bff-172">Las secciones relevantes del archivo **ServiceDefinition.csdef** se muestran aquí:</span><span class="sxs-lookup"><span data-stu-id="16bff-172">The relevant sections of the **ServiceDefinition.csdef** file are shown here:</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WorkerRole name="WorkerRole1">
    ...

    <LocalResources>
      <LocalStorage name="StartupLocalStorage" sizeInMB="5"/>
    </LocalResources>

    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>
          <Variable name="PathToStartupStorage">
            <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
          </Variable>
        </Environment>
      </Task>
    </Startup>
  </WorkerRole>
</ServiceDefinition>
```

<span data-ttu-id="16bff-173">Por ejemplo, este archivo por lotes **Startup.cmd** usa la variable de entorno **PathToStartupStorage** para crear el archivo **MyTest.txt** en la ubicación de almacenamiento local.</span><span class="sxs-lookup"><span data-stu-id="16bff-173">As an example, this **Startup.cmd** batch file uses the **PathToStartupStorage** environment variable to create the file **MyTest.txt** on the local storage location.</span></span>

```cmd
REM   Create a simple text file.

ECHO This text will go into the MyTest.txt file which will be in the    >  "%PathToStartupStorage%\MyTest.txt"
ECHO path pointed to by the PathToStartupStorage environment variable.  >> "%PathToStartupStorage%\MyTest.txt"
ECHO The contents of the PathToStartupStorage environment variable is   >> "%PathToStartupStorage%\MyTest.txt"
ECHO "%PathToStartupStorage%".                                          >> "%PathToStartupStorage%\MyTest.txt"

REM   Exit the batch file with ERRORLEVEL 0.

EXIT /b 0
```

<span data-ttu-id="16bff-174">Puede tener acceso a la carpeta de almacenamiento local desde el SDK de Azure con el método [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) .</span><span class="sxs-lookup"><span data-stu-id="16bff-174">You can access local storage folder from the Azure SDK by using the [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>

```csharp
string localStoragePath = Microsoft.WindowsAzure.ServiceRuntime.RoleEnvironment.GetLocalResource("StartupLocalStorage").RootPath;

string fileContent = System.IO.File.ReadAllText(System.IO.Path.Combine(localStoragePath, "MyTestFile.txt"));
```

## <a name="run-in-the-emulator-or-cloud"></a><span data-ttu-id="16bff-175">Ejecutar en el emulador o la nube</span><span class="sxs-lookup"><span data-stu-id="16bff-175">Run in the emulator or cloud</span></span>
<span data-ttu-id="16bff-176">Puede hacer que la tarea de inicio emprenda acciones diferentes cuando se ejecuta en la nube en comparación con cuando lo hace en el emulador de proceso.</span><span class="sxs-lookup"><span data-stu-id="16bff-176">You can have your startup task perform different steps when it is operating in the cloud compared to when it is in the compute emulator.</span></span> <span data-ttu-id="16bff-177">Por ejemplo, puede que quiera usar una copia nueva de los datos de SQL solo cuando se ejecuta en el emulador.</span><span class="sxs-lookup"><span data-stu-id="16bff-177">For example, you may want to use a fresh copy of your SQL data only when running in the emulator.</span></span> <span data-ttu-id="16bff-178">O puede que desee hacer algunas optimizaciones de rendimiento para la nube que no necesita cuando la ejecución se realiza en el emulador.</span><span class="sxs-lookup"><span data-stu-id="16bff-178">Or you may want to do some performance optimizations for the cloud that you don't need to do when running in the emulator.</span></span>

<span data-ttu-id="16bff-179">Esta capacidad para realizar distintas acciones en el emulador de proceso y en la nube puede conseguirse mediante la creación de una variable de entorno en el archivo [ServiceDefinition.csdef].</span><span class="sxs-lookup"><span data-stu-id="16bff-179">This ability to perform different actions on the compute emulator and the cloud can be accomplished by creating an environment variable in the [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="16bff-180">A continuación, pruebe esa variable de entorno para un valor en la tarea de inicio.</span><span class="sxs-lookup"><span data-stu-id="16bff-180">You then test that environment variable for a value in your startup task.</span></span>

<span data-ttu-id="16bff-181">Para crear la variable de entorno, agregue el elemento [Variable]/[RoleInstanceValue] y cree un valor de XPath de `/RoleEnvironment/Deployment/@emulated`.</span><span class="sxs-lookup"><span data-stu-id="16bff-181">To create the environment variable, add the [Variable]/[RoleInstanceValue] element and create an XPath value of `/RoleEnvironment/Deployment/@emulated`.</span></span> <span data-ttu-id="16bff-182">El valor de la variable de entorno **%ComputeEmulatorRunning%** es `true` cuando se ejecuta en el emulador de proceso y `false` cuando se ejecuta en la nube.</span><span class="sxs-lookup"><span data-stu-id="16bff-182">The value of the **%ComputeEmulatorRunning%** environment variable is `true` when running on the compute emulator, and `false` when running on the cloud.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WorkerRole name="WorkerRole1">

    ...

    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>
          <Variable name="ComputeEmulatorRunning">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
        </Environment>
      </Task>
    </Startup>

  </WorkerRole>
</ServiceDefinition>
```

<span data-ttu-id="16bff-183">La tarea puede comprobar ahora la variable de entorno **% ComputeEmulatorRunning %** para realizar distintas acciones en función de si se ejecuta el rol en la nube o en el emulador.</span><span class="sxs-lookup"><span data-stu-id="16bff-183">The task can now check the **%ComputeEmulatorRunning%** environment variable to perform different actions based on whether the role is running in the cloud or the emulator.</span></span> <span data-ttu-id="16bff-184">Aquí tiene un script de shell de .cmd que busca esa variable de entorno.</span><span class="sxs-lookup"><span data-stu-id="16bff-184">Here is a .cmd shell script that checks for that environment variable.</span></span>

```cmd
REM   Check if this task is running on the compute emulator.

IF "%ComputeEmulatorRunning%" == "true" (
    REM   This task is running on the compute emulator. Perform tasks that must be run only in the compute emulator.
) ELSE (
    REM   This task is running on the cloud. Perform tasks that must be run only in the cloud.
)
```


## <a name="detect-that-your-task-has-already-run"></a><span data-ttu-id="16bff-185">Detección de si la tarea ya se ha ejecutado</span><span class="sxs-lookup"><span data-stu-id="16bff-185">Detect that your task has already run</span></span>
<span data-ttu-id="16bff-186">El rol puede reciclar sin tener que reiniciar con lo que las tareas de inicio se vuelven a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="16bff-186">The role may recycle without a reboot causing your startup tasks to run again.</span></span> <span data-ttu-id="16bff-187">No hay ninguna marca para indicar que una tarea ya se ha ejecutado en la VM de hospedaje.</span><span class="sxs-lookup"><span data-stu-id="16bff-187">There is no flag to indicate that a task has already run on the hosting VM.</span></span> <span data-ttu-id="16bff-188">Puede que en algunas tareas no importe si se ejecutan varias veces.</span><span class="sxs-lookup"><span data-stu-id="16bff-188">You may have some tasks where it doesn't matter that they run multiple times.</span></span> <span data-ttu-id="16bff-189">Sin embargo, puede haber situaciones en las que es necesario evitar que una tarea se ejecute más de una vez.</span><span class="sxs-lookup"><span data-stu-id="16bff-189">However, you may run into a situation where you need to prevent a task from running more than once.</span></span>

<span data-ttu-id="16bff-190">La manera más sencilla de detectar si una tarea se ha ejecutado ya es crear un archivo en la carpeta **% TEMP %** cuando la tarea se realiza correctamente y buscarlo al inicio de la tarea.</span><span class="sxs-lookup"><span data-stu-id="16bff-190">The simplest way to detect that a task has already run is to create a file in the **%TEMP%** folder when the task is successful and look for it at the start of the task.</span></span> <span data-ttu-id="16bff-191">Este es un ejemplo script de shell de cmd que lo hace.</span><span class="sxs-lookup"><span data-stu-id="16bff-191">Here is a sample cmd shell script that does that for you.</span></span>

```cmd
REM   If Task1_Success.txt exists, then Application 1 is already installed.
IF EXIST "%RoleRoot%\Task1_Success.txt" (
  ECHO Application 1 is already installed. Exiting. >> "%TEMP%\StartupLog.txt" 2>&1
  GOTO Finish
)

REM   Run your real exe task
ECHO Running XYZ >> "%TEMP%\StartupLog.txt" 2>&1
"%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

IF %ERRORLEVEL% EQU 0 (
  REM   The application installed without error. Create a file to indicate that the task
  REM   does not need to be run again.

  ECHO This line will create a file to indicate that Application 1 installed correctly. > "%RoleRoot%\Task1_Success.txt"

) ELSE (
  REM   An error occurred. Log the error and exit with the error code.

  DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
  TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
  ECHO  An error occurred running task 1. Errorlevel = %ERRORLEVEL%. >> "%TEMP%\StartupLog.txt" 2>&1

  EXIT %ERRORLEVEL%
)

:Finish

REM   Exit normally.
EXIT /B 0
```

## <a name="task-best-practices"></a><span data-ttu-id="16bff-192">Prácticas recomendadas para las tareas</span><span class="sxs-lookup"><span data-stu-id="16bff-192">Task best practices</span></span>
<span data-ttu-id="16bff-193">A continuación presentamos algunas prácticas recomendadas que debería seguir al configurar una tarea para el rol web o de trabajo.</span><span class="sxs-lookup"><span data-stu-id="16bff-193">Here are some best practices you should follow when configuring task for your web or worker role.</span></span>

### <a name="always-log-startup-activities"></a><span data-ttu-id="16bff-194">Registre siempre las actividades de inicio</span><span class="sxs-lookup"><span data-stu-id="16bff-194">Always log startup activities</span></span>
<span data-ttu-id="16bff-195">Visual Studio no proporciona un depurador para repasar los archivos por lotes, por eso es conveniente tener tantos datos sobre el funcionamiento de archivos por lotes como sea posible.</span><span class="sxs-lookup"><span data-stu-id="16bff-195">Visual Studio does not provide a debugger to step through batch files, so it's good to get as much data on the operation of batch files as possible.</span></span> <span data-ttu-id="16bff-196">El registro de la salida de archivos por lotes, **stdout** y **stderr**, puede proporcionar información importante a la hora de depurar y corregir los archivos por lotes.</span><span class="sxs-lookup"><span data-stu-id="16bff-196">Logging the output of batch files, both **stdout** and **stderr**, can give you important information when trying to debug and fix batch files.</span></span> <span data-ttu-id="16bff-197">Para registrar **stdout** y **stderr** en el archivo StartupLog.txt en el directorio señalado por la variable de entorno **%TEMP%**, agregue el texto `>>  "%TEMP%\\StartupLog.txt" 2>&1` al final de líneas específicas que desee registrar.</span><span class="sxs-lookup"><span data-stu-id="16bff-197">To log both **stdout** and **stderr** to the StartupLog.txt file in the directory pointed to by the **%TEMP%** environment variable, add the text `>>  "%TEMP%\\StartupLog.txt" 2>&1` to the end of specific lines you want to log.</span></span> <span data-ttu-id="16bff-198">Por ejemplo, para ejecutar setup.exe en el directorio **% PathToApp1Install %** :</span><span class="sxs-lookup"><span data-stu-id="16bff-198">For example, to execute setup.exe in the **%PathToApp1Install%** directory:</span></span>

    "%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

<span data-ttu-id="16bff-199">Para simplificar el código xml, puede crear un archivo *cmd* de contenedor que llame a todas las tareas de inicio junto con el registro y garantice que cada tarea secundaria comparte las mismas variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="16bff-199">To simplify your xml, you can create a wrapper *cmd* file that calls all of your startup tasks along with logging and ensures each child-task shares the same environment variables.</span></span>

<span data-ttu-id="16bff-200">Puede resultarle molesto, sin embargo, a la hora de usar `>> "%TEMP%\StartupLog.txt" 2>&1` en el extremo de cada tarea de inicio.</span><span class="sxs-lookup"><span data-stu-id="16bff-200">You may find it annoying though to use `>> "%TEMP%\StartupLog.txt" 2>&1` on the end of each startup task.</span></span> <span data-ttu-id="16bff-201">Puede aplicar el registro de tareas mediante la creación de un contenedor que controle el registro automáticamente.</span><span class="sxs-lookup"><span data-stu-id="16bff-201">You can enforce task logging by creating a wrapper that handles logging for you.</span></span> <span data-ttu-id="16bff-202">Este contenedor llama al archivo por lotes real que desea ejecutar.</span><span class="sxs-lookup"><span data-stu-id="16bff-202">This wrapper calls the real batch file you want to run.</span></span> <span data-ttu-id="16bff-203">Cualquier salida del archivo por lotes de destino se redirigirá al archivo *Startuplog.txt*.</span><span class="sxs-lookup"><span data-stu-id="16bff-203">Any output from the target batch file will be redirected to the *Startuplog.txt* file.</span></span>

<span data-ttu-id="16bff-204">En el ejemplo siguiente se muestra cómo redirigir todas las salidas de un archivo por lotes de inicio.</span><span class="sxs-lookup"><span data-stu-id="16bff-204">The following example shows how to redirect all output from a startup batch file.</span></span> <span data-ttu-id="16bff-205">En este ejemplo, el archivo ServerDefinition.csdef crea una tarea de inicio que llama a *logwrap.cmd*.</span><span class="sxs-lookup"><span data-stu-id="16bff-205">In this example, the ServerDefinition.csdef file creates a startup task that calls *logwrap.cmd*.</span></span> <span data-ttu-id="16bff-206">*logwrap.cmd* llama a *Startup2.cmd*, redirigiendo todas las salidas a **%TEMP%\\StartupLog.txt**.</span><span class="sxs-lookup"><span data-stu-id="16bff-206">*logwrap.cmd* calls *Startup2.cmd*, redirecting all output to **%TEMP%\\StartupLog.txt**.</span></span>

<span data-ttu-id="16bff-207">ServiceDefinition.cmd:</span><span class="sxs-lookup"><span data-stu-id="16bff-207">ServiceDefinition.cmd:</span></span>

```xml
<Startup>
    <Task commandLine="logwrap.cmd startup2.cmd" executionContext="limited" taskType="simple" />
</Startup>
```

<span data-ttu-id="16bff-208">**logwrap.cmd:**</span><span class="sxs-lookup"><span data-stu-id="16bff-208">**logwrap.cmd:**</span></span>

```cmd
@ECHO OFF

REM   logwrap.cmd calls passed in batch file, redirecting all output to the StartupLog.txt log file.

ECHO [%date% %time%] == START logwrap.cmd ============================================== >> "%TEMP%\StartupLog.txt" 2>&1
ECHO [%date% %time%] Running %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Call the child command batch file, redirecting all output to the StartupLog.txt log file.
START /B /WAIT %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Log the completion of child command.
ECHO [%date% %time%] Done >> "%TEMP%\StartupLog.txt" 2>&1

IF %ERRORLEVEL% EQU 0 (

   REM   No errors occurred. Exit logwrap.cmd normally.
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B 0

) ELSE (

   REM   Log the error.
   ECHO [%date% %time%] An error occurred. The ERRORLEVEL = %ERRORLEVEL%.  >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B %ERRORLEVEL%

)
```

<span data-ttu-id="16bff-209">**Startup2.cmd:**</span><span class="sxs-lookup"><span data-stu-id="16bff-209">**Startup2.cmd:**</span></span>

```cmd
@ECHO OFF

REM   This is the batch file where the startup steps should be performed. Because of the
REM   way Startup2.cmd was called, all commands and their outputs will be stored in the
REM   StartupLog.txt file in the directory pointed to by the TEMP environment variable.

REM   If an error occurs, the following command will pass the ERRORLEVEL back to the
REM   calling batch file.

ECHO [%date% %time%] Some log information about this task
ECHO [%date% %time%] Some more log information about this task

EXIT %ERRORLEVEL%
```

<span data-ttu-id="16bff-210">Salida de ejemplo en el archivo **StartupLog.txt**:</span><span class="sxs-lookup"><span data-stu-id="16bff-210">Sample output in the **StartupLog.txt** file:</span></span>

```txt
[Mon 10/17/2016 20:24:46.75] == START logwrap.cmd ============================================== 
[Mon 10/17/2016 20:24:46.75] Running command1.cmd 
[Mon 10/17/2016 20:24:46.77] Some log information about this task
[Mon 10/17/2016 20:24:46.77] Some more log information about this task
[Mon 10/17/2016 20:24:46.77] Done 
[Mon 10/17/2016 20:24:46.77] == END logwrap.cmd ================================================ 
```

> [!TIP]
> <span data-ttu-id="16bff-211">El archivo **StartupLog.txt** se encuentra en la carpeta *C:\Resources\temp\\\RoleTemp {identificador de rol}*.</span><span class="sxs-lookup"><span data-stu-id="16bff-211">The **StartupLog.txt** file is located in the *C:\Resources\temp\\{role identifier}\RoleTemp* folder.</span></span>
> 
> 

### <a name="set-executioncontext-appropriately-for-startup-tasks"></a><span data-ttu-id="16bff-212">Establezca executionContext correctamente para las tareas de inicio</span><span class="sxs-lookup"><span data-stu-id="16bff-212">Set executionContext appropriately for startup tasks</span></span>
<span data-ttu-id="16bff-213">Establezca correctamente los privilegios para la tarea de inicio.</span><span class="sxs-lookup"><span data-stu-id="16bff-213">Set privileges appropriately for the startup task.</span></span> <span data-ttu-id="16bff-214">A veces las tareas de inicio tienen que ejecutarse con privilegios elevados, incluso si el rol se ejecuta con privilegios normales.</span><span class="sxs-lookup"><span data-stu-id="16bff-214">Sometimes startup tasks must run with elevated privileges even though the role runs with normal privileges.</span></span>

<span data-ttu-id="16bff-215">La herramienta de línea de comandos [executionContext][Task] establece el nivel de privilegio de la tarea de inicio.</span><span class="sxs-lookup"><span data-stu-id="16bff-215">The [executionContext][Task] attribute sets the privilege level of the startup task.</span></span> <span data-ttu-id="16bff-216">Si usa `executionContext="limited"` la tarea de inicio tendrá el mismo nivel de privilegio que el rol.</span><span class="sxs-lookup"><span data-stu-id="16bff-216">Using `executionContext="limited"` means the startup task has the same privilege level as the role.</span></span> <span data-ttu-id="16bff-217">Si usa `executionContext="elevated"` la tarea de inicio tendrá privilegios de administrador, lo que permite que la tarea de inicio realice tareas de administrador sin otorgar privilegios de administrador a su rol.</span><span class="sxs-lookup"><span data-stu-id="16bff-217">Using `executionContext="elevated"` means the startup task has administrator privileges, which allows the startup task to perform administrator tasks without giving administrator privileges to your role.</span></span>

<span data-ttu-id="16bff-218">Un ejemplo de tarea de inicio que requiere privilegios de nivel "elevated" sería una tarea de inicio que use **AppCmd.exe** para configurar IIS.</span><span class="sxs-lookup"><span data-stu-id="16bff-218">An example of a startup task that requires elevated privileges is a startup task that uses **AppCmd.exe** to configure IIS.</span></span> <span data-ttu-id="16bff-219">**AppCmd.exe** requiere `executionContext="elevated"`.</span><span class="sxs-lookup"><span data-stu-id="16bff-219">**AppCmd.exe** requires `executionContext="elevated"`.</span></span>

### <a name="use-the-appropriate-tasktype"></a><span data-ttu-id="16bff-220">Use el valor de taskType apropiado</span><span class="sxs-lookup"><span data-stu-id="16bff-220">Use the appropriate taskType</span></span>
<span data-ttu-id="16bff-221">El atributo [taskType][Task] determina la forma en la que se ejecuta la tarea de inicio.</span><span class="sxs-lookup"><span data-stu-id="16bff-221">The [taskType][Task] attribute determines the way the startup task is executed.</span></span> <span data-ttu-id="16bff-222">Hay tres valores: **simple**, **background** y **foreground**.</span><span class="sxs-lookup"><span data-stu-id="16bff-222">There are three values: **simple**, **background**, and **foreground**.</span></span> <span data-ttu-id="16bff-223">Las tareas con valor background y foreground se inician de forma asincrónica, mientras que las tareas con valor simple se ejecutan sincrónicamente una después de otra.</span><span class="sxs-lookup"><span data-stu-id="16bff-223">The background and foreground tasks are started asynchronously, and then the simple tasks are executed synchronously one at a time.</span></span>

<span data-ttu-id="16bff-224">Con las tareas de inicio **simple**, puede establecer el orden en que se ejecutan las tareas a través del orden de las tareas en el archivo ServiceDefinition.csdef.</span><span class="sxs-lookup"><span data-stu-id="16bff-224">With **simple** startup tasks, you can set the order in which the tasks run by the order in which the tasks are listed in the ServiceDefinition.csdef file.</span></span> <span data-ttu-id="16bff-225">Si una tarea **simple** finaliza con un código de salida distinto de cero, el procedimiento de inicio se detendrá y el rol no se iniciará.</span><span class="sxs-lookup"><span data-stu-id="16bff-225">If a **simple** task ends with a non-zero exit code, then the startup procedure stops and the role does not start.</span></span>

<span data-ttu-id="16bff-226">La diferencia entre las tareas de inicio con valor **background** y aquellas con valor **foreground** es que las tareas **foreground** mantienen el rol en ejecución hasta que la tarea **foreground** finaliza.</span><span class="sxs-lookup"><span data-stu-id="16bff-226">The difference between **background** startup tasks and **foreground** startup tasks is that **foreground** tasks keep the role running until the **foreground** task ends.</span></span> <span data-ttu-id="16bff-227">Esto también significa que si la tarea **foreground** se bloquea o falla, el rol no se reciclará hasta que se fuerce el cierre de la tarea **foreground**.</span><span class="sxs-lookup"><span data-stu-id="16bff-227">This also means that if the **foreground** task hangs or crashes, the role will not recycle until the **foreground** task is forced closed.</span></span> <span data-ttu-id="16bff-228">Por este motivo, las tareas **background** se recomiendan para las tareas de inicio asincrónicas a menos que necesite esa característica de la tarea **foreground**.</span><span class="sxs-lookup"><span data-stu-id="16bff-228">For this reason, **background** tasks are recommended for asynchronous startup tasks unless you need that feature of the **foreground** task.</span></span>

### <a name="end-batch-files-with-exit-b-0"></a><span data-ttu-id="16bff-229">Finalice lo archivos por lotes con EXIT /B 0</span><span class="sxs-lookup"><span data-stu-id="16bff-229">End batch files with EXIT /B 0</span></span>
<span data-ttu-id="16bff-230">El rol solo se iniciará si **errorlevel** de cada una de las tareas de inicio de valor simple es cero.</span><span class="sxs-lookup"><span data-stu-id="16bff-230">The role will only start if the **errorlevel** from each of your simple startup task is zero.</span></span> <span data-ttu-id="16bff-231">No todos los programas establecen el **errorlevel** (código de salida) correctamente, por lo que el archivo por lotes debe terminar con `EXIT /B 0` si todo se ejecutó correctamente.</span><span class="sxs-lookup"><span data-stu-id="16bff-231">Not all programs set the **errorlevel** (exit code) correctly, so the batch file should end with an `EXIT /B 0` if everything ran correctly.</span></span>

<span data-ttu-id="16bff-232">La falta de `EXIT /B 0` al final de un archivo por lotes de inicio es una causa común de que un rol no se inicie.</span><span class="sxs-lookup"><span data-stu-id="16bff-232">A missing `EXIT /B 0` at the end of a startup batch file is a common cause of roles that do not start.</span></span>

> [!NOTE]
> <span data-ttu-id="16bff-233">He observado que los archivos por lotes anidados se bloquean a veces al usar el parámetro `/B`.</span><span class="sxs-lookup"><span data-stu-id="16bff-233">I've noticed that nested batch files sometimes hang when using the `/B` parameter.</span></span> <span data-ttu-id="16bff-234">Puede que desee asegurarse de que este problema de bloqueo no se produce si otro archivo por lotes llama a su archivo por lotes actual, como si usara el [contenedor del registro](#always-log-startup-activities).</span><span class="sxs-lookup"><span data-stu-id="16bff-234">You may want to make sure that this hang problem does not happen if another batch file calls your current batch file, like if you use the [log wrapper](#always-log-startup-activities).</span></span> <span data-ttu-id="16bff-235">Puede omitir el parámetro `/B` en este caso.</span><span class="sxs-lookup"><span data-stu-id="16bff-235">You can omit the `/B` parameter in this case.</span></span>
> 
> 

### <a name="expect-startup-tasks-to-run-more-than-once"></a><span data-ttu-id="16bff-236">Espere que las tareas de inicio se ejecuten más de una vez</span><span class="sxs-lookup"><span data-stu-id="16bff-236">Expect startup tasks to run more than once</span></span>
<span data-ttu-id="16bff-237">No todos los reciclajes de rol incluyen un reinicio, pero todos incluyen la ejecución de todas las tareas de inicio.</span><span class="sxs-lookup"><span data-stu-id="16bff-237">Not all role recycles include a reboot, but all role recycles include running all startup tasks.</span></span> <span data-ttu-id="16bff-238">Esto significa que las tareas de inicio tienen que poder ejecutarse varias veces entre reinicios sin problemas.</span><span class="sxs-lookup"><span data-stu-id="16bff-238">This means that startup tasks must be able to run multiple times between reboots without any problems.</span></span> <span data-ttu-id="16bff-239">Esto se explica en la [sección anterior](#detect-that-your-task-has-already-run).</span><span class="sxs-lookup"><span data-stu-id="16bff-239">This is discussed in the [preceding section](#detect-that-your-task-has-already-run).</span></span>

### <a name="use-local-storage-to-store-files-that-must-be-accessed-in-the-role"></a><span data-ttu-id="16bff-240">Use el almacenamiento local para almacenar los archivos que tienen que accederse en el rol</span><span class="sxs-lookup"><span data-stu-id="16bff-240">Use local storage to store files that must be accessed in the role</span></span>
<span data-ttu-id="16bff-241">Si desea copiar o crear un archivo durante la tarea de inicio que en ese momento es accesible para el rol, ese archivo tiene que colocarse en el almacenamiento local.</span><span class="sxs-lookup"><span data-stu-id="16bff-241">If you want to copy or create a file during your startup task that is then accessible to your role, then that file must be placed in local storage.</span></span> <span data-ttu-id="16bff-242">Consulte la [sección anterior](#create-files-in-local-storage-from-a-startup-task).</span><span class="sxs-lookup"><span data-stu-id="16bff-242">See the [preceding section](#create-files-in-local-storage-from-a-startup-task).</span></span>

## <a name="next-steps"></a><span data-ttu-id="16bff-243">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="16bff-243">Next steps</span></span>
<span data-ttu-id="16bff-244">Revisar el [modelo de servicio y paquete](cloud-services-model-and-package.md)</span><span class="sxs-lookup"><span data-stu-id="16bff-244">Review the cloud [service model and package](cloud-services-model-and-package.md)</span></span>

<span data-ttu-id="16bff-245">Obtener más información acerca de cómo funcionan las [tareas](cloud-services-startup-tasks.md) .</span><span class="sxs-lookup"><span data-stu-id="16bff-245">Learn more about how [Tasks](cloud-services-startup-tasks.md) work.</span></span>

<span data-ttu-id="16bff-246">[Crear e implementar](cloud-services-how-to-create-deploy-portal.md) el paquete de servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="16bff-246">[Create and deploy](cloud-services-how-to-create-deploy-portal.md) your cloud service package.</span></span>

<span data-ttu-id="16bff-247">[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef</span><span class="sxs-lookup"><span data-stu-id="16bff-247">[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef</span></span>
<span data-ttu-id="16bff-248">[Task]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task</span><span class="sxs-lookup"><span data-stu-id="16bff-248">[Task]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task</span></span>
[Startup]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
<span data-ttu-id="16bff-249">[Environment]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment</span><span class="sxs-lookup"><span data-stu-id="16bff-249">[Environment]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment</span></span>
<span data-ttu-id="16bff-250">[Variable]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable</span><span class="sxs-lookup"><span data-stu-id="16bff-250">[Variable]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable</span></span>
<span data-ttu-id="16bff-251">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span><span class="sxs-lookup"><span data-stu-id="16bff-251">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span></span>
[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
<span data-ttu-id="16bff-252">[Endpoints]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Endpoints</span><span class="sxs-lookup"><span data-stu-id="16bff-252">[Endpoints]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Endpoints</span></span>
<span data-ttu-id="16bff-253">[LocalStorage]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalStorage</span><span class="sxs-lookup"><span data-stu-id="16bff-253">[LocalStorage]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalStorage</span></span>
<span data-ttu-id="16bff-254">[LocalResources]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalResources</span><span class="sxs-lookup"><span data-stu-id="16bff-254">[LocalResources]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalResources</span></span>
<span data-ttu-id="16bff-255">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span><span class="sxs-lookup"><span data-stu-id="16bff-255">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span></span>
