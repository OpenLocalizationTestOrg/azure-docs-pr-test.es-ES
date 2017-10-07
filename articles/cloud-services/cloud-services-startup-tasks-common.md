---
title: las tareas de inicio de aaaCommon para servicios en la nube | Documentos de Microsoft
description: Se proporcionan algunos ejemplos de tareas comunes de inicio puede tooperform en su rol web de servicios de nube o el rol de trabajo.
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
ms.openlocfilehash: c80fac4079439410dfc3795e4bce0fbc07dbbfab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="common-cloud-service-startup-tasks"></a><span data-ttu-id="db101-103">Tareas de inicio comunes para los servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="db101-103">Common Cloud Service startup tasks</span></span>
<span data-ttu-id="db101-104">En este artículo se proporciona algunos ejemplos de tareas comunes de inicio puede querer tooperform en su servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="db101-104">This article provides some examples of common startup tasks you may want tooperform in your cloud service.</span></span> <span data-ttu-id="db101-105">Puede utilizar operaciones de tooperform de tareas de inicio antes de que se inicia un rol.</span><span class="sxs-lookup"><span data-stu-id="db101-105">You can use startup tasks tooperform operations before a role starts.</span></span> <span data-ttu-id="db101-106">Operaciones que podría interesarle tooperform incluyen la instalación de un componente, registrando los componentes COM, configurar claves de registro o iniciar un proceso de ejecución prolongada.</span><span class="sxs-lookup"><span data-stu-id="db101-106">Operations that you might want tooperform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span> 

<span data-ttu-id="db101-107">Vea [este artículo](cloud-services-startup-tasks.md) toounderstand cómo funcionan las tareas de inicio y específicamente cómo toocreate Hola entradas que definen una tarea de inicio.</span><span class="sxs-lookup"><span data-stu-id="db101-107">See [this article](cloud-services-startup-tasks.md) toounderstand how startup tasks work, and specifically how toocreate hello entries that define a startup task.</span></span>

> [!NOTE]
> <span data-ttu-id="db101-108">Las tareas de inicio no son aplicables tooVirtual máquinas, solo tooCloud servicio Web y roles de trabajo.</span><span class="sxs-lookup"><span data-stu-id="db101-108">Startup tasks are not applicable tooVirtual Machines, only tooCloud Service Web and Worker roles.</span></span>
> 

## <a name="define-environment-variables-before-a-role-starts"></a><span data-ttu-id="db101-109">Definición de variables de entorno antes de que se inicie un rol</span><span class="sxs-lookup"><span data-stu-id="db101-109">Define environment variables before a role starts</span></span>
<span data-ttu-id="db101-110">Si necesita variables de entorno definidas para una tarea específica, use hello [entorno] elemento dentro de hello [tarea] elemento.</span><span class="sxs-lookup"><span data-stu-id="db101-110">If you need environment variables defined for a specific task, use hello [Environment] element inside hello [Task] element.</span></span>

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

<span data-ttu-id="db101-111">Las variables también pueden usar un [valor XPath de Azure válido](cloud-services-role-config-xpath.md) tooreference algo acerca de la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="db101-111">Variables can also use a [valid Azure XPath value](cloud-services-role-config-xpath.md) tooreference something about hello deployment.</span></span> <span data-ttu-id="db101-112">En lugar de usar hello `value` atributo, defina un [RoleInstanceValue] elemento secundario.</span><span class="sxs-lookup"><span data-stu-id="db101-112">Instead of using hello `value` attribute, define a [RoleInstanceValue] child element.</span></span>

```xml
<Variable name="PathToStartupStorage">
    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
</Variable>
```


## <a name="configure-iis-startup-with-appcmdexe"></a><span data-ttu-id="db101-113">Configuración del inicio IIS con AppCmd.exe</span><span class="sxs-lookup"><span data-stu-id="db101-113">Configure IIS startup with AppCmd.exe</span></span>
<span data-ttu-id="db101-114">Hola [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) herramienta de línea de comandos puede ser la configuración de IIS toomanage usado en el inicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="db101-114">hello [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) command-line tool can be used toomanage IIS settings at startup on Azure.</span></span> <span data-ttu-id="db101-115">*AppCmd.exe* proporciona opciones de configuración de acceso cómodo y línea de comandos tooconfiguration para su uso en las tareas de inicio en Azure.</span><span class="sxs-lookup"><span data-stu-id="db101-115">*AppCmd.exe* provides convenient, command-line access tooconfiguration settings for use in startup tasks on Azure.</span></span> <span data-ttu-id="db101-116">Con *AppCmd.exe*se pueden agregar modificar o quitar ajustes del sitio web para aplicaciones y sitios.</span><span class="sxs-lookup"><span data-stu-id="db101-116">Using *AppCmd.exe*, Website settings can be added, modified, or removed for applications and sites.</span></span>

<span data-ttu-id="db101-117">Sin embargo, hay algunos toowatch de cosas fuera de uso de Hola de *AppCmd.exe* como una tarea de inicio:</span><span class="sxs-lookup"><span data-stu-id="db101-117">However, there are a few things toowatch out for in hello use of *AppCmd.exe* as a startup task:</span></span>

* <span data-ttu-id="db101-118">Las tareas de inicio se pueden ejecutar más de una vez entre reinicios.</span><span class="sxs-lookup"><span data-stu-id="db101-118">Startup tasks can be run more than once between reboots.</span></span> <span data-ttu-id="db101-119">Por ejemplo, cuando un rol se recicla.</span><span class="sxs-lookup"><span data-stu-id="db101-119">For instance, when a role recycles.</span></span>
* <span data-ttu-id="db101-120">Si una acción *AppCmd.exe* se realiza más de una vez, puede generar un error.</span><span class="sxs-lookup"><span data-stu-id="db101-120">If a *AppCmd.exe* action is performed more than once, it may generate an error.</span></span> <span data-ttu-id="db101-121">Por ejemplo, intentar tooadd una sección demasiado*Web.config* dos veces, podría producirse un error.</span><span class="sxs-lookup"><span data-stu-id="db101-121">For example, attempting tooadd a section too*Web.config* twice could generate an error.</span></span>
* <span data-ttu-id="db101-122">Si las tareas de inicio devuelven un código de salida distinto de cero o un **errorlevel**se producirá un error en las mismas.</span><span class="sxs-lookup"><span data-stu-id="db101-122">Startup tasks fail if they return a non-zero exit code or **errorlevel**.</span></span> <span data-ttu-id="db101-123">Por ejemplo, cuando *AppCmd.exe* genera un error.</span><span class="sxs-lookup"><span data-stu-id="db101-123">For example, when *AppCmd.exe* generates an error.</span></span>

<span data-ttu-id="db101-124">Es un Hola de toocheck recomendable **errorlevel** después de llamar a *AppCmd.exe*, que es fácil toodo si encapsula llamada Hola demasiado*AppCmd.exe* con un *.cmd*  archivo.</span><span class="sxs-lookup"><span data-stu-id="db101-124">It is a good practice toocheck hello **errorlevel** after calling *AppCmd.exe*, which is easy toodo if you wrap hello call too*AppCmd.exe* with a *.cmd* file.</span></span> <span data-ttu-id="db101-125">Si se detecta una respuesta **errorlevel** conocida, puede ignorarla o devolverla.</span><span class="sxs-lookup"><span data-stu-id="db101-125">If you detect a known **errorlevel** response, you can ignore it, or pass it back.</span></span>

<span data-ttu-id="db101-126">Hola errorlevel devuelto por *AppCmd.exe* se muestran en el archivo winerror.h de Hola y también se pueden ver en [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).</span><span class="sxs-lookup"><span data-stu-id="db101-126">hello errorlevel returned by *AppCmd.exe* are listed in hello winerror.h file, and can also be seen on [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).</span></span>

### <a name="example-of-managing-hello-error-level"></a><span data-ttu-id="db101-127">Ejemplo de administración de nivel de error de Hola</span><span class="sxs-lookup"><span data-stu-id="db101-127">Example of managing hello error level</span></span>
<span data-ttu-id="db101-128">Este ejemplo agrega una sección de compresión y una entrada de compresión para JSON toohello *Web.config* archivos con control de errores y registro.</span><span class="sxs-lookup"><span data-stu-id="db101-128">This example adds a compression section and a compression entry for JSON toohello *Web.config* file, with error handling and logging.</span></span>

<span data-ttu-id="db101-129">Hola secciones relevantes de hello [ServiceDefinition.csdef] archivo se muestran aquí, que incluyen el establecimiento de hello [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) atributo demasiado`elevated` toogive *AppCmd.exe*  configuración de Hola de toochange de permisos suficientes en hello *Web.config* archivo:</span><span class="sxs-lookup"><span data-stu-id="db101-129">hello relevant sections of hello [ServiceDefinition.csdef] file are shown here, which include setting hello [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) attribute too`elevated` toogive *AppCmd.exe* sufficient permissions toochange hello settings in hello *Web.config* file:</span></span>

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

<span data-ttu-id="db101-130">Hola *Startup.cmd* por lotes de archivos utiliza *AppCmd.exe* tooadd una sección de compresión y una entrada de compresión para JSON toohello *Web.config* archivo.</span><span class="sxs-lookup"><span data-stu-id="db101-130">hello *Startup.cmd* batch file uses *AppCmd.exe* tooadd a compression section and a compression entry for JSON toohello *Web.config* file.</span></span> <span data-ttu-id="db101-131">Hola esperada **errorlevel** de 183 se establece toozero con hello compruebe. Programa de línea de comandos del archivo EXE.</span><span class="sxs-lookup"><span data-stu-id="db101-131">hello expected **errorlevel** of 183 is set toozero using hello VERIFY.EXE command-line program.</span></span> <span data-ttu-id="db101-132">Niveles de error inesperados son tooStartupErrorLog.txt ha iniciado.</span><span class="sxs-lookup"><span data-stu-id="db101-132">Unexpected errorlevels are logged tooStartupErrorLog.txt.</span></span>

```cmd
REM   *** Add a compression section toohello Web.config file. ***
%windir%\system32\inetsrv\appcmd set config /section:urlCompression /doDynamicCompression:True /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1

REM   ERRORLEVEL 183 occurs when trying tooadd a section that already exists. This error is expected if this
REM   batch file were executed twice. This can occur and must be accounted for in a Azure startup
REM   task. toohandle this situation, set hello ERRORLEVEL toozero by using hello Verify command. hello Verify
REM   command will safely set hello ERRORLEVEL toozero.
IF %ERRORLEVEL% EQU 183 DO VERIFY > NUL

REM   If hello ERRORLEVEL is not zero at this point, some other error occurred.
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding a compression section toohello Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Add compression for json. ***
%windir%\system32\inetsrv\appcmd set config  -section:system.webServer/httpCompression /+"dynamicTypes.[mimeType='application/json; charset=utf-8',enabled='True']" /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1
IF %ERRORLEVEL% EQU 183 VERIFY > NUL
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding hello JSON compression type toohello Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Exit batch file. ***
EXIT /b 0

REM   *** Log error and exit ***
:ErrorExit
REM   Report hello date, time, and ERRORLEVEL of hello error.
DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
ECHO An error occurred during startup. ERRORLEVEL = %ERRORLEVEL% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT %ERRORLEVEL%
```

## <a name="add-firewall-rules"></a><span data-ttu-id="db101-133">Adición de reglas de firewall</span><span class="sxs-lookup"><span data-stu-id="db101-133">Add firewall rules</span></span>
<span data-ttu-id="db101-134">A efectos prácticos, hay dos firewalls en Azure.</span><span class="sxs-lookup"><span data-stu-id="db101-134">In Azure, there are effectively two firewalls.</span></span> <span data-ttu-id="db101-135">Hola primer firewall controla las conexiones entre la máquina virtual de Hola y Hola fuera world.</span><span class="sxs-lookup"><span data-stu-id="db101-135">hello first firewall controls connections between hello virtual machine and hello outside world.</span></span> <span data-ttu-id="db101-136">Este servidor de seguridad se controla mediante hello [extremos] elemento Hola [ServiceDefinition.csdef] archivo.</span><span class="sxs-lookup"><span data-stu-id="db101-136">This firewall is controlled by hello [EndPoints] element in hello [ServiceDefinition.csdef] file.</span></span>

<span data-ttu-id="db101-137">Hola segundo firewall controla las conexiones entre la máquina virtual de Hola y procesos de hello en esa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="db101-137">hello second firewall controls connections between hello virtual machine and hello processes within that virtual machine.</span></span> <span data-ttu-id="db101-138">Este firewall puede controlarse mediante hello `netsh advfirewall firewall` herramienta de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="db101-138">This firewall can be controlled by hello `netsh advfirewall firewall` command-line tool.</span></span>

<span data-ttu-id="db101-139">Azure crea reglas de firewall para los procesos de hello iniciados en sus roles.</span><span class="sxs-lookup"><span data-stu-id="db101-139">Azure creates firewall rules for hello processes started within your roles.</span></span> <span data-ttu-id="db101-140">Por ejemplo, cuando se inicia un servicio o programa, Azure crea automáticamente tooallow de reglas de firewall necesarias de hello toocommunicate de ese servicio con hello Internet.</span><span class="sxs-lookup"><span data-stu-id="db101-140">For example, when you start a service or program, Azure automatically creates hello necessary firewall rules tooallow that service toocommunicate with hello Internet.</span></span> <span data-ttu-id="db101-141">Sin embargo, si crea un servicio que se inicia un proceso fuera de su rol (por ejemplo, un servicio COM + o una tarea programada de Windows), deberá toomanually crear un servicio de toothat de acceso de firewall regla tooallow.</span><span class="sxs-lookup"><span data-stu-id="db101-141">However, if you create a service that is started by a process outside your role (like a COM+ service or a Windows Scheduled Task), you need toomanually create a firewall rule tooallow access toothat service.</span></span> <span data-ttu-id="db101-142">Estas reglas de firewall pueden crearse mediante una tarea de inicio.</span><span class="sxs-lookup"><span data-stu-id="db101-142">These firewall rules can be created by using a startup task.</span></span>

<span data-ttu-id="db101-143">Una tarea de inicio que crea una regla de firewall tiene que tener para el atributo [executionContext][tarea] un valor **elevated**se producirá un error en las mismas.</span><span class="sxs-lookup"><span data-stu-id="db101-143">A startup task that creates a firewall rule must have an [executionContext][Task] of **elevated**.</span></span> <span data-ttu-id="db101-144">Agregar Hola después toohello de tarea de inicio [ServiceDefinition.csdef] archivo.</span><span class="sxs-lookup"><span data-stu-id="db101-144">Add hello following startup task toohello [ServiceDefinition.csdef] file.</span></span>

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

<span data-ttu-id="db101-145">regla de firewall de Hola de tooadd, debe usar Hola adecuado `netsh advfirewall firewall` comandos en el archivo por lotes de inicio.</span><span class="sxs-lookup"><span data-stu-id="db101-145">tooadd hello firewall rule, you must use hello appropriate `netsh advfirewall firewall` commands in your startup batch file.</span></span> <span data-ttu-id="db101-146">En este ejemplo, la tarea de inicio de hello requiere seguridad y cifrado para el puerto TCP 80.</span><span class="sxs-lookup"><span data-stu-id="db101-146">In this example, hello startup task requires security and encryption for TCP port 80.</span></span>

```cmd
REM   Add a firewall rule in a startup task.

REM   Add an inbound rule requiring security and encryption for TCP port 80 traffic.
netsh advfirewall firewall add rule name="Require Encryption for Inbound TCP/80" protocol=TCP dir=in localport=80 security=authdynenc action=allow >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

## <a name="block-a-specific-ip-address"></a><span data-ttu-id="db101-147">Bloqueo de una dirección IP específica</span><span class="sxs-lookup"><span data-stu-id="db101-147">Block a specific IP address</span></span>
<span data-ttu-id="db101-148">Puede restringir un conjunto de tooa de acceso de rol web de Azure de direcciones IP especificadas mediante la modificación de los IIS **web.config** archivo.</span><span class="sxs-lookup"><span data-stu-id="db101-148">You can restrict an Azure web role access tooa set of specified IP addresses by modifying your IIS **web.config** file.</span></span> <span data-ttu-id="db101-149">También necesita un archivo de comandos que desbloquee hello toouse **seguridad IP** sección de hello **ApplicationHost.config** archivo.</span><span class="sxs-lookup"><span data-stu-id="db101-149">You also need toouse a command file which unlocks hello **ipSecurity** section of hello **ApplicationHost.config** file.</span></span>

<span data-ttu-id="db101-150">toodo desbloquear hello **seguridad IP** sección de hello **ApplicationHost.config** , cree un archivo de comandos que se ejecuta en el inicio de rol.</span><span class="sxs-lookup"><span data-stu-id="db101-150">toodo unlock hello **ipSecurity** section of hello **ApplicationHost.config** file, create a command file that runs at role start.</span></span> <span data-ttu-id="db101-151">Crear una carpeta en el nivel de raíz de Hola de rol web denominado **inicio** y, dentro de esta carpeta, cree un archivo por lotes denominado **startup.cmd**.</span><span class="sxs-lookup"><span data-stu-id="db101-151">Create a folder at hello root level of your web role called **startup** and, within this folder, create a batch file called **startup.cmd**.</span></span> <span data-ttu-id="db101-152">Agregue este archivo de proyecto de Visual Studio tooyour y establezca propiedades de hello demasiado**copiar siempre** tooensure que se incluye en el paquete.</span><span class="sxs-lookup"><span data-stu-id="db101-152">Add this file tooyour Visual Studio project and set hello properties too**Copy Always** tooensure that it is included in your package.</span></span>

<span data-ttu-id="db101-153">Agregar Hola después toohello de tarea de inicio [ServiceDefinition.csdef] archivo.</span><span class="sxs-lookup"><span data-stu-id="db101-153">Add hello following startup task toohello [ServiceDefinition.csdef] file.</span></span>

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

<span data-ttu-id="db101-154">Agregar este comando toohello **startup.cmd** archivo:</span><span class="sxs-lookup"><span data-stu-id="db101-154">Add this command toohello **startup.cmd** file:</span></span>

```cmd
@echo off
@echo Installing "IPv4 Address and Domain Restrictions" feature 
powershell -ExecutionPolicy Unrestricted -command "Install-WindowsFeature Web-IP-Security"
@echo Unlocking configuration for "IPv4 Address and Domain Restrictions" feature 
%windir%\system32\inetsrv\AppCmd.exe unlock config -section:system.webServer/security/ipSecurity
```

<span data-ttu-id="db101-155">Esta tarea hace hello **startup.cmd** por lotes toobe archivo ejecutar cada vez que se inicializa el rol web de hello, asegurándose de que Hola necesario **seguridad IP** sección está desbloqueada.</span><span class="sxs-lookup"><span data-stu-id="db101-155">This task causes hello **startup.cmd** batch file toobe run every time hello web role is initialized, ensuring that hello required **ipSecurity** section is unlocked.</span></span>

<span data-ttu-id="db101-156">Por último, modifique hello [sección system.webServer](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) su rol web **web.config** archivos tooadd una lista de direcciones IP que se concede el acceso, tal y como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="db101-156">Finally, modify hello [system.webServer section](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) your web role’s **web.config** file tooadd a list of IP addresses that are granted access, as shown in hello following example:</span></span>

<span data-ttu-id="db101-157">Esta configuración de ejemplo **permite** tooaccess de todas las direcciones IP Hola servidor salvo Hola dos definidas</span><span class="sxs-lookup"><span data-stu-id="db101-157">This sample config **allows** all IPs tooaccess hello server except hello two defined</span></span>

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are granted access-->
    <ipSecurity>
        <!--hello following IP addresses are denied access-->
        <add allowed="false" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="false" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

<span data-ttu-id="db101-158">Esta configuración de ejemplo **deniega** todas las direcciones IP tengan acceso a server Hola excepto Hola dos definido.</span><span class="sxs-lookup"><span data-stu-id="db101-158">This sample config **denies** all IPs from accessing hello server except for hello two defined.</span></span>

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are denied access-->
    <ipSecurity allowUnlisted="false">
        <!--hello following IP addresses are granted access-->
        <add allowed="true" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="true" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

## <a name="create-a-powershell-startup-task"></a><span data-ttu-id="db101-159">Creación de una tarea de inicio de PowerShell</span><span class="sxs-lookup"><span data-stu-id="db101-159">Create a PowerShell startup task</span></span>
<span data-ttu-id="db101-160">Scripts de Windows PowerShell no se puede llamar directamente desde hello [ServiceDefinition.csdef] archivo, pero se puede invocar desde dentro de un archivo por lotes de inicio.</span><span class="sxs-lookup"><span data-stu-id="db101-160">Windows PowerShell scripts cannot be called directly from hello [ServiceDefinition.csdef] file, but they can be invoked from within a startup batch file.</span></span>

<span data-ttu-id="db101-161">PowerShell (de forma predeterminada) no ejecuta scripts sin firmar.</span><span class="sxs-lookup"><span data-stu-id="db101-161">PowerShell (by default) does not run unsigned scripts.</span></span> <span data-ttu-id="db101-162">A menos que se registra el script, debe tooconfigure PowerShell scripts sin firmar toorun.</span><span class="sxs-lookup"><span data-stu-id="db101-162">Unless you sign your script, you need tooconfigure PowerShell toorun unsigned scripts.</span></span> <span data-ttu-id="db101-163">toorun scripts sin firmar, hello **ExecutionPolicy** debe establecerse demasiado**Unrestricted**.</span><span class="sxs-lookup"><span data-stu-id="db101-163">toorun unsigned scripts, hello **ExecutionPolicy** must be set too**Unrestricted**.</span></span> <span data-ttu-id="db101-164">Hola **ExecutionPolicy** configuración use se basa en la versión de Hola de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="db101-164">hello **ExecutionPolicy** setting that you use is based on hello version of Windows PowerShell.</span></span>

```cmd
REM   Run an unsigned PowerShell script and log hello output
PowerShell -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

<span data-ttu-id="db101-165">Si está utilizando un sistema operativo de invitado que se ejecuta PowerShell 2.0 o 1.0 puede forzar toorun versión 2 y si no está disponible, utilice la versión 1.</span><span class="sxs-lookup"><span data-stu-id="db101-165">If you're using a Guest OS that is runs PowerShell 2.0 or 1.0 you can force version 2 toorun, and if unavailable, use version 1.</span></span>

```cmd
REM   Attempt tooset hello execution policy by using PowerShell version 2.0 syntax.
PowerShell -Version 2.0 -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If PowerShell version 2.0 isn't available. Set hello execution policy by using hello PowerShell
IF %ERRORLEVEL% EQU -393216 (
   PowerShell -Command "Set-ExecutionPolicy Unrestricted" >> "%TEMP%\StartupLog.txt" 2>&1
   PowerShell .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1
)

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

## <a name="create-files-in-local-storage-from-a-startup-task"></a><span data-ttu-id="db101-166">Creación de archivos de una tarea de inicio en un almacenamiento local</span><span class="sxs-lookup"><span data-stu-id="db101-166">Create files in local storage from a startup task</span></span>
<span data-ttu-id="db101-167">Puede usar un toostore de recursos de almacenamiento local archivos creados por la tarea de inicio que se tiene acceso más adelante con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="db101-167">You can use a local storage resource toostore files created by your startup task that is accessed later by your application.</span></span>

<span data-ttu-id="db101-168">toocreate Hola recurso de almacenamiento local, agregue un [LocalResources] sección toohello [ServiceDefinition.csdef] de archivos y, a continuación, agregue hello [LocalStorage] elemento secundario.</span><span class="sxs-lookup"><span data-stu-id="db101-168">toocreate hello local storage resource, add a [LocalResources] section toohello [ServiceDefinition.csdef] file and then add hello [LocalStorage] child element.</span></span> <span data-ttu-id="db101-169">Proporcionar recursos de almacenamiento local de hello un nombre único y un tamaño apropiado para la tarea de inicio.</span><span class="sxs-lookup"><span data-stu-id="db101-169">Give hello local storage resource a unique name and an appropriate size for your startup task.</span></span>

<span data-ttu-id="db101-170">toouse un recurso de almacenamiento local en la tarea de inicio, debe toocreate una ubicación de recursos de almacenamiento local de entorno variable tooreference Hola.</span><span class="sxs-lookup"><span data-stu-id="db101-170">toouse a local storage resource in your startup task, you need toocreate an environment variable tooreference hello local storage resource location.</span></span> <span data-ttu-id="db101-171">Hola, a continuación, la tarea de inicio y aplicación hello tooread capaz de y escribir el recurso de almacenamiento local de archivos toohello.</span><span class="sxs-lookup"><span data-stu-id="db101-171">Then hello startup task and hello application are able tooread and write files toohello local storage resource.</span></span>

<span data-ttu-id="db101-172">Hola secciones relevantes de hello **ServiceDefinition.csdef** archivo se muestran a continuación:</span><span class="sxs-lookup"><span data-stu-id="db101-172">hello relevant sections of hello **ServiceDefinition.csdef** file are shown here:</span></span>

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

<span data-ttu-id="db101-173">Por ejemplo, esto **Startup.cmd** archivo por lotes utiliza hello **PathToStartupStorage** archivo de hello toocreate variable de entorno **MyTest.txt** en almacenamiento local de Hola ubicación.</span><span class="sxs-lookup"><span data-stu-id="db101-173">As an example, this **Startup.cmd** batch file uses hello **PathToStartupStorage** environment variable toocreate hello file **MyTest.txt** on hello local storage location.</span></span>

```cmd
REM   Create a simple text file.

ECHO This text will go into hello MyTest.txt file which will be in hello    >  "%PathToStartupStorage%\MyTest.txt"
ECHO path pointed tooby hello PathToStartupStorage environment variable.  >> "%PathToStartupStorage%\MyTest.txt"
ECHO hello contents of hello PathToStartupStorage environment variable is   >> "%PathToStartupStorage%\MyTest.txt"
ECHO "%PathToStartupStorage%".                                          >> "%PathToStartupStorage%\MyTest.txt"

REM   Exit hello batch file with ERRORLEVEL 0.

EXIT /b 0
```

<span data-ttu-id="db101-174">Puede tener acceso a carpeta de almacenamiento local de hello Azure SDK mediante hello [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) método.</span><span class="sxs-lookup"><span data-stu-id="db101-174">You can access local storage folder from hello Azure SDK by using hello [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>

```csharp
string localStoragePath = Microsoft.WindowsAzure.ServiceRuntime.RoleEnvironment.GetLocalResource("StartupLocalStorage").RootPath;

string fileContent = System.IO.File.ReadAllText(System.IO.Path.Combine(localStoragePath, "MyTestFile.txt"));
```

## <a name="run-in-hello-emulator-or-cloud"></a><span data-ttu-id="db101-175">Ejecutar en el emulador de Hola o en la nube</span><span class="sxs-lookup"><span data-stu-id="db101-175">Run in hello emulator or cloud</span></span>
<span data-ttu-id="db101-176">Puede tener la tarea de inicio emprenda acciones diferentes cuando se está ejecutando en hello en la nube en comparación con toowhen que se encuentra en el emulador de proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="db101-176">You can have your startup task perform different steps when it is operating in hello cloud compared toowhen it is in hello compute emulator.</span></span> <span data-ttu-id="db101-177">Por ejemplo, puede que desee toouse una nueva copia de los datos SQL sólo cuando se ejecuta en el emulador de Hola.</span><span class="sxs-lookup"><span data-stu-id="db101-177">For example, you may want toouse a fresh copy of your SQL data only when running in hello emulator.</span></span> <span data-ttu-id="db101-178">O bien, puede que desee toodo algunas optimizaciones de rendimiento para la nube de Hola que no es necesario toodo cuando se ejecuta en el emulador de Hola.</span><span class="sxs-lookup"><span data-stu-id="db101-178">Or you may want toodo some performance optimizations for hello cloud that you don't need toodo when running in hello emulator.</span></span>

<span data-ttu-id="db101-179">Este tooperform capacidad diferente acciones en hello emulador de proceso y Hola nube se consigue mediante la creación de una variable de entorno en hello [ServiceDefinition.csdef] archivo.</span><span class="sxs-lookup"><span data-stu-id="db101-179">This ability tooperform different actions on hello compute emulator and hello cloud can be accomplished by creating an environment variable in hello [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="db101-180">A continuación, pruebe esa variable de entorno para un valor en la tarea de inicio.</span><span class="sxs-lookup"><span data-stu-id="db101-180">You then test that environment variable for a value in your startup task.</span></span>

<span data-ttu-id="db101-181">variable de entorno de hello toocreate, agregar hello [Variable]/[RoleInstanceValue] elemento y cree un valor de XPath de `/RoleEnvironment/Deployment/@emulated`.</span><span class="sxs-lookup"><span data-stu-id="db101-181">toocreate hello environment variable, add hello [Variable]/[RoleInstanceValue] element and create an XPath value of `/RoleEnvironment/Deployment/@emulated`.</span></span> <span data-ttu-id="db101-182">Hola valo hello **ComputeEmulatorRunning %** variable de entorno es `true` cuando se ejecuta en el emulador de proceso de hello, y `false` cuando se ejecuta en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="db101-182">hello value of hello **%ComputeEmulatorRunning%** environment variable is `true` when running on hello compute emulator, and `false` when running on hello cloud.</span></span>

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

<span data-ttu-id="db101-183">tarea Hello ahora puede comprobar hello **ComputeEmulatorRunning %** acciones diferentes tooperform variable de entorno, en función de si está ejecutando el rol de hello en hello en la nube u Hola emulador.</span><span class="sxs-lookup"><span data-stu-id="db101-183">hello task can now check hello **%ComputeEmulatorRunning%** environment variable tooperform different actions based on whether hello role is running in hello cloud or hello emulator.</span></span> <span data-ttu-id="db101-184">Aquí tiene un script de shell de .cmd que busca esa variable de entorno.</span><span class="sxs-lookup"><span data-stu-id="db101-184">Here is a .cmd shell script that checks for that environment variable.</span></span>

```cmd
REM   Check if this task is running on hello compute emulator.

IF "%ComputeEmulatorRunning%" == "true" (
    REM   This task is running on hello compute emulator. Perform tasks that must be run only in hello compute emulator.
) ELSE (
    REM   This task is running on hello cloud. Perform tasks that must be run only in hello cloud.
)
```


## <a name="detect-that-your-task-has-already-run"></a><span data-ttu-id="db101-185">Detección de si la tarea ya se ha ejecutado</span><span class="sxs-lookup"><span data-stu-id="db101-185">Detect that your task has already run</span></span>
<span data-ttu-id="db101-186">rol de Hello puede reciclar sin reiniciar el equipo haciendo que su toorun de tareas de inicio de nuevo.</span><span class="sxs-lookup"><span data-stu-id="db101-186">hello role may recycle without a reboot causing your startup tasks toorun again.</span></span> <span data-ttu-id="db101-187">No hay ningún tooindicate de marca que ya se ha ejecutado una tarea en hello hospeda la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="db101-187">There is no flag tooindicate that a task has already run on hello hosting VM.</span></span> <span data-ttu-id="db101-188">Puede que en algunas tareas no importe si se ejecutan varias veces.</span><span class="sxs-lookup"><span data-stu-id="db101-188">You may have some tasks where it doesn't matter that they run multiple times.</span></span> <span data-ttu-id="db101-189">Sin embargo, puede encontrarse con una situación donde debe tooprevent una tarea de ejecución de más de una vez.</span><span class="sxs-lookup"><span data-stu-id="db101-189">However, you may run into a situation where you need tooprevent a task from running more than once.</span></span>

<span data-ttu-id="db101-190">toodetect manera más sencilla Hola que ya se ha ejecutado una tarea es un archivo en hello toocreate **% TEMP %** carpeta cuando se realiza correctamente la tarea hello y búsquelo en hello principio de la tarea hello.</span><span class="sxs-lookup"><span data-stu-id="db101-190">hello simplest way toodetect that a task has already run is toocreate a file in hello **%TEMP%** folder when hello task is successful and look for it at hello start of hello task.</span></span> <span data-ttu-id="db101-191">Este es un ejemplo script de shell de cmd que lo hace.</span><span class="sxs-lookup"><span data-stu-id="db101-191">Here is a sample cmd shell script that does that for you.</span></span>

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
  REM   hello application installed without error. Create a file tooindicate that hello task
  REM   does not need toobe run again.

  ECHO This line will create a file tooindicate that Application 1 installed correctly. > "%RoleRoot%\Task1_Success.txt"

) ELSE (
  REM   An error occurred. Log hello error and exit with hello error code.

  DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
  TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
  ECHO  An error occurred running task 1. Errorlevel = %ERRORLEVEL%. >> "%TEMP%\StartupLog.txt" 2>&1

  EXIT %ERRORLEVEL%
)

:Finish

REM   Exit normally.
EXIT /B 0
```

## <a name="task-best-practices"></a><span data-ttu-id="db101-192">Prácticas recomendadas para las tareas</span><span class="sxs-lookup"><span data-stu-id="db101-192">Task best practices</span></span>
<span data-ttu-id="db101-193">A continuación presentamos algunas prácticas recomendadas que debería seguir al configurar una tarea para el rol web o de trabajo.</span><span class="sxs-lookup"><span data-stu-id="db101-193">Here are some best practices you should follow when configuring task for your web or worker role.</span></span>

### <a name="always-log-startup-activities"></a><span data-ttu-id="db101-194">Registre siempre las actividades de inicio</span><span class="sxs-lookup"><span data-stu-id="db101-194">Always log startup activities</span></span>
<span data-ttu-id="db101-195">Visual Studio no proporciona un depurador toostep archivos por lotes, por lo que es buena tooget mayor cantidad de datos en la operación de Hola de archivos por lotes como sea posible.</span><span class="sxs-lookup"><span data-stu-id="db101-195">Visual Studio does not provide a debugger toostep through batch files, so it's good tooget as much data on hello operation of batch files as possible.</span></span> <span data-ttu-id="db101-196">Registro de salida de hello de archivos por lotes, ambos **stdout** y **stderr**, puede obtener información importante al tratar de toodebug y corregir archivos por lotes.</span><span class="sxs-lookup"><span data-stu-id="db101-196">Logging hello output of batch files, both **stdout** and **stderr**, can give you important information when trying toodebug and fix batch files.</span></span> <span data-ttu-id="db101-197">toolog ambos **stdout** y **stderr** toohello StartupLog.txt archivo Hola de hello directorio apunta tooby **% TEMP %** variable de entorno, agregue texto hello `>>  "%TEMP%\\StartupLog.txt" 2>&1`toohello final específicas de líneas desea toolog.</span><span class="sxs-lookup"><span data-stu-id="db101-197">toolog both **stdout** and **stderr** toohello StartupLog.txt file in hello directory pointed tooby hello **%TEMP%** environment variable, add hello text `>>  "%TEMP%\\StartupLog.txt" 2>&1` toohello end of specific lines you want toolog.</span></span> <span data-ttu-id="db101-198">Por ejemplo, tooexecute setup.exe en hello **% PathToApp1Install %** directorio:</span><span class="sxs-lookup"><span data-stu-id="db101-198">For example, tooexecute setup.exe in hello **%PathToApp1Install%** directory:</span></span>

    "%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

<span data-ttu-id="db101-199">toosimplify el código xml, puede crear un contenedor *cmd* archivo que se invocan de la configuración de inicio de tareas junto con el registro y garantiza cada Hola de recursos compartidos de la tarea secundaria mismas variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="db101-199">toosimplify your xml, you can create a wrapper *cmd* file that calls all of your startup tasks along with logging and ensures each child-task shares hello same environment variables.</span></span>

<span data-ttu-id="db101-200">Quizá le resulte aunque molestar toouse `>> "%TEMP%\StartupLog.txt" 2>&1` en extremo Hola de cada tarea de inicio.</span><span class="sxs-lookup"><span data-stu-id="db101-200">You may find it annoying though toouse `>> "%TEMP%\StartupLog.txt" 2>&1` on hello end of each startup task.</span></span> <span data-ttu-id="db101-201">Puede aplicar el registro de tareas mediante la creación de un contenedor que controle el registro automáticamente.</span><span class="sxs-lookup"><span data-stu-id="db101-201">You can enforce task logging by creating a wrapper that handles logging for you.</span></span> <span data-ttu-id="db101-202">Este contenedor llama a archivo de lote real de hello desea toorun.</span><span class="sxs-lookup"><span data-stu-id="db101-202">This wrapper calls hello real batch file you want toorun.</span></span> <span data-ttu-id="db101-203">Cualquier resultado del archivo por lotes de destino de hello será redirigido toohello *Startuplog.txt* archivo.</span><span class="sxs-lookup"><span data-stu-id="db101-203">Any output from hello target batch file will be redirected toohello *Startuplog.txt* file.</span></span>

<span data-ttu-id="db101-204">Hola de ejemplo siguiente muestra cómo tooredirect todos los resultados desde un archivo por lotes de inicio.</span><span class="sxs-lookup"><span data-stu-id="db101-204">hello following example shows how tooredirect all output from a startup batch file.</span></span> <span data-ttu-id="db101-205">En este ejemplo, archivo de hello ServerDefinition.csdef crea una tarea de inicio que llama *logwrap.cmd*.</span><span class="sxs-lookup"><span data-stu-id="db101-205">In this example, hello ServerDefinition.csdef file creates a startup task that calls *logwrap.cmd*.</span></span> <span data-ttu-id="db101-206">*logwrap.cmd* llamadas *startup2.cmd; para ello*, redirige todos los resultados demasiado**% TEMP %\\StartupLog.txt**.</span><span class="sxs-lookup"><span data-stu-id="db101-206">*logwrap.cmd* calls *Startup2.cmd*, redirecting all output too**%TEMP%\\StartupLog.txt**.</span></span>

<span data-ttu-id="db101-207">ServiceDefinition.cmd:</span><span class="sxs-lookup"><span data-stu-id="db101-207">ServiceDefinition.cmd:</span></span>

```xml
<Startup>
    <Task commandLine="logwrap.cmd startup2.cmd" executionContext="limited" taskType="simple" />
</Startup>
```

<span data-ttu-id="db101-208">**logwrap.cmd:**</span><span class="sxs-lookup"><span data-stu-id="db101-208">**logwrap.cmd:**</span></span>

```cmd
@ECHO OFF

REM   logwrap.cmd calls passed in batch file, redirecting all output toohello StartupLog.txt log file.

ECHO [%date% %time%] == START logwrap.cmd ============================================== >> "%TEMP%\StartupLog.txt" 2>&1
ECHO [%date% %time%] Running %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Call hello child command batch file, redirecting all output toohello StartupLog.txt log file.
START /B /WAIT %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Log hello completion of child command.
ECHO [%date% %time%] Done >> "%TEMP%\StartupLog.txt" 2>&1

IF %ERRORLEVEL% EQU 0 (

   REM   No errors occurred. Exit logwrap.cmd normally.
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B 0

) ELSE (

   REM   Log hello error.
   ECHO [%date% %time%] An error occurred. hello ERRORLEVEL = %ERRORLEVEL%.  >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B %ERRORLEVEL%

)
```

<span data-ttu-id="db101-209">**Startup2.cmd:**</span><span class="sxs-lookup"><span data-stu-id="db101-209">**Startup2.cmd:**</span></span>

```cmd
@ECHO OFF

REM   This is hello batch file where hello startup steps should be performed. Because of the
REM   way Startup2.cmd was called, all commands and their outputs will be stored in the
REM   StartupLog.txt file in hello directory pointed tooby hello TEMP environment variable.

REM   If an error occurs, hello following command will pass hello ERRORLEVEL back toothe
REM   calling batch file.

ECHO [%date% %time%] Some log information about this task
ECHO [%date% %time%] Some more log information about this task

EXIT %ERRORLEVEL%
```

<span data-ttu-id="db101-210">Ejemplo de salida de hello **StartupLog.txt** archivo:</span><span class="sxs-lookup"><span data-stu-id="db101-210">Sample output in hello **StartupLog.txt** file:</span></span>

```txt
[Mon 10/17/2016 20:24:46.75] == START logwrap.cmd ============================================== 
[Mon 10/17/2016 20:24:46.75] Running command1.cmd 
[Mon 10/17/2016 20:24:46.77] Some log information about this task
[Mon 10/17/2016 20:24:46.77] Some more log information about this task
[Mon 10/17/2016 20:24:46.77] Done 
[Mon 10/17/2016 20:24:46.77] == END logwrap.cmd ================================================ 
```

> [!TIP]
> <span data-ttu-id="db101-211">Hola **StartupLog.txt** archivo se encuentra en hello *C:\Resources\temp\\\RoleTemp {identificador de rol}* carpeta.</span><span class="sxs-lookup"><span data-stu-id="db101-211">hello **StartupLog.txt** file is located in hello *C:\Resources\temp\\{role identifier}\RoleTemp* folder.</span></span>
> 
> 

### <a name="set-executioncontext-appropriately-for-startup-tasks"></a><span data-ttu-id="db101-212">Establezca executionContext correctamente para las tareas de inicio</span><span class="sxs-lookup"><span data-stu-id="db101-212">Set executionContext appropriately for startup tasks</span></span>
<span data-ttu-id="db101-213">Establecer los privilegios de forma adecuada para la tarea de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="db101-213">Set privileges appropriately for hello startup task.</span></span> <span data-ttu-id="db101-214">A veces, las tareas de inicio deben ejecutar con privilegios elevados, aunque Hola rol se ejecuta con privilegios normales.</span><span class="sxs-lookup"><span data-stu-id="db101-214">Sometimes startup tasks must run with elevated privileges even though hello role runs with normal privileges.</span></span>

<span data-ttu-id="db101-215">Hola [executionContext][tarea] atributo establece el nivel de privilegio de Hola de tarea de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="db101-215">hello [executionContext][Task] attribute sets hello privilege level of hello startup task.</span></span> <span data-ttu-id="db101-216">Usar `executionContext="limited"` significa tiene la tarea de inicio de Hola Hola de mismo nivel de privilegios como rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="db101-216">Using `executionContext="limited"` means hello startup task has hello same privilege level as hello role.</span></span> <span data-ttu-id="db101-217">Usar `executionContext="elevated"` significa la tarea de inicio de hello tiene privilegios de administrador, que permite el inicio de hello tareas del Administrador de tareas tooperform sin asignar rol de tooyour de privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="db101-217">Using `executionContext="elevated"` means hello startup task has administrator privileges, which allows hello startup task tooperform administrator tasks without giving administrator privileges tooyour role.</span></span>

<span data-ttu-id="db101-218">Un ejemplo de una tarea de inicio que requiere privilegios elevados es una tarea de inicio que utiliza **AppCmd.exe** tooconfigure IIS.</span><span class="sxs-lookup"><span data-stu-id="db101-218">An example of a startup task that requires elevated privileges is a startup task that uses **AppCmd.exe** tooconfigure IIS.</span></span> <span data-ttu-id="db101-219">**AppCmd.exe** requiere `executionContext="elevated"`.</span><span class="sxs-lookup"><span data-stu-id="db101-219">**AppCmd.exe** requires `executionContext="elevated"`.</span></span>

### <a name="use-hello-appropriate-tasktype"></a><span data-ttu-id="db101-220">Usar valor de taskType apropiado de Hola</span><span class="sxs-lookup"><span data-stu-id="db101-220">Use hello appropriate taskType</span></span>
<span data-ttu-id="db101-221">Hola [taskType][tarea] atributo determina que se ejecuta la tarea de inicio de hello forma Hola.</span><span class="sxs-lookup"><span data-stu-id="db101-221">hello [taskType][Task] attribute determines hello way hello startup task is executed.</span></span> <span data-ttu-id="db101-222">Hay tres valores: **simple**, **background** y **foreground**.</span><span class="sxs-lookup"><span data-stu-id="db101-222">There are three values: **simple**, **background**, and **foreground**.</span></span> <span data-ttu-id="db101-223">Hello tareas de fondo y primer plano se inician de forma asincrónica y, a continuación, se ejecutan las tareas sencillas de hello sincrónicamente uno en uno.</span><span class="sxs-lookup"><span data-stu-id="db101-223">hello background and foreground tasks are started asynchronously, and then hello simple tasks are executed synchronously one at a time.</span></span>

<span data-ttu-id="db101-224">Con **simple** las tareas de inicio, puede establecer el orden de hello en el que se ejecutan las tareas de Hola por orden de hello en qué Hola se enumeran las tareas en el archivo ServiceDefinition.csdef de Hola.</span><span class="sxs-lookup"><span data-stu-id="db101-224">With **simple** startup tasks, you can set hello order in which hello tasks run by hello order in which hello tasks are listed in hello ServiceDefinition.csdef file.</span></span> <span data-ttu-id="db101-225">Si un **simple** tarea finaliza con un usuario que no sea cero código de salida, a continuación, Hola procedimiento de inicio se detiene y no se inicia el rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="db101-225">If a **simple** task ends with a non-zero exit code, then hello startup procedure stops and hello role does not start.</span></span>

<span data-ttu-id="db101-226">Hola diferencia entre **fondo** las tareas de inicio y **primer plano** las tareas de inicio es que **primer plano** tareas mantener la ejecución de la función de hello hasta hello  **primer plano** finaliza la tarea.</span><span class="sxs-lookup"><span data-stu-id="db101-226">hello difference between **background** startup tasks and **foreground** startup tasks is that **foreground** tasks keep hello role running until hello **foreground** task ends.</span></span> <span data-ttu-id="db101-227">Esto también significa que si hello **primer plano** tarea se bloquea o se bloquea, el rol de hello no se reciclará hasta hello **primer plano** se fuerza la tarea cerrado.</span><span class="sxs-lookup"><span data-stu-id="db101-227">This also means that if hello **foreground** task hangs or crashes, hello role will not recycle until hello **foreground** task is forced closed.</span></span> <span data-ttu-id="db101-228">Por esta razón, **fondo** se recomiendan las tareas para tareas de inicio asincrónicas a menos que necesite esa función de hello **primer plano** tarea.</span><span class="sxs-lookup"><span data-stu-id="db101-228">For this reason, **background** tasks are recommended for asynchronous startup tasks unless you need that feature of hello **foreground** task.</span></span>

### <a name="end-batch-files-with-exit-b-0"></a><span data-ttu-id="db101-229">Finalice lo archivos por lotes con EXIT /B 0</span><span class="sxs-lookup"><span data-stu-id="db101-229">End batch files with EXIT /B 0</span></span>
<span data-ttu-id="db101-230">Hello rol solo se iniciará si hello **errorlevel** de cada uno de su inicio simple tarea es cero.</span><span class="sxs-lookup"><span data-stu-id="db101-230">hello role will only start if hello **errorlevel** from each of your simple startup task is zero.</span></span> <span data-ttu-id="db101-231">No todos los programas establecen hello **errorlevel** (código de salida) correctamente, por lo que archivo por lotes de hello debe terminar con un `EXIT /B 0` si todo lo que se ejecutaba correctamente.</span><span class="sxs-lookup"><span data-stu-id="db101-231">Not all programs set hello **errorlevel** (exit code) correctly, so hello batch file should end with an `EXIT /B 0` if everything ran correctly.</span></span>

<span data-ttu-id="db101-232">Falta un `EXIT /B 0` en hello final de un archivo por lotes de inicio es una causa frecuente de los roles que no se inician.</span><span class="sxs-lookup"><span data-stu-id="db101-232">A missing `EXIT /B 0` at hello end of a startup batch file is a common cause of roles that do not start.</span></span>

> [!NOTE]
> <span data-ttu-id="db101-233">He observado ese lote anidado archivos a veces bloquearse cuando se utiliza hello `/B` parámetro.</span><span class="sxs-lookup"><span data-stu-id="db101-233">I've noticed that nested batch files sometimes hang when using hello `/B` parameter.</span></span> <span data-ttu-id="db101-234">Puede que desee toomake seguro de que en este problema de falta de respuesta no se realiza si el archivo por lotes actual llama a otro archivo por lotes, como si usa hello [contenedor del registro](#always-log-startup-activities).</span><span class="sxs-lookup"><span data-stu-id="db101-234">You may want toomake sure that this hang problem does not happen if another batch file calls your current batch file, like if you use hello [log wrapper](#always-log-startup-activities).</span></span> <span data-ttu-id="db101-235">Puede omitir hello `/B` parámetro en este caso.</span><span class="sxs-lookup"><span data-stu-id="db101-235">You can omit hello `/B` parameter in this case.</span></span>
> 
> 

### <a name="expect-startup-tasks-toorun-more-than-once"></a><span data-ttu-id="db101-236">Esperar toorun de tareas de inicio más de una vez</span><span class="sxs-lookup"><span data-stu-id="db101-236">Expect startup tasks toorun more than once</span></span>
<span data-ttu-id="db101-237">No todos los reciclajes de rol incluyen un reinicio, pero todos incluyen la ejecución de todas las tareas de inicio.</span><span class="sxs-lookup"><span data-stu-id="db101-237">Not all role recycles include a reboot, but all role recycles include running all startup tasks.</span></span> <span data-ttu-id="db101-238">Esto significa que las tareas de inicio deben ser capaz de toorun varias veces entre reinicios sin problemas.</span><span class="sxs-lookup"><span data-stu-id="db101-238">This means that startup tasks must be able toorun multiple times between reboots without any problems.</span></span> <span data-ttu-id="db101-239">Esto se explica en hello [sección anterior](#detect-that-your-task-has-already-run).</span><span class="sxs-lookup"><span data-stu-id="db101-239">This is discussed in hello [preceding section](#detect-that-your-task-has-already-run).</span></span>

### <a name="use-local-storage-toostore-files-that-must-be-accessed-in-hello-role"></a><span data-ttu-id="db101-240">Utilizar almacenamiento local toostore archivos que deben tener acceso en función de Hola</span><span class="sxs-lookup"><span data-stu-id="db101-240">Use local storage toostore files that must be accessed in hello role</span></span>
<span data-ttu-id="db101-241">Si desea toocopy o crear un archivo durante la tarea de inicio, a continuación, es accesible tooyour rol, ese archivo se debe colocar en el almacenamiento local.</span><span class="sxs-lookup"><span data-stu-id="db101-241">If you want toocopy or create a file during your startup task that is then accessible tooyour role, then that file must be placed in local storage.</span></span> <span data-ttu-id="db101-242">Vea hello [sección anterior](#create-files-in-local-storage-from-a-startup-task).</span><span class="sxs-lookup"><span data-stu-id="db101-242">See hello [preceding section](#create-files-in-local-storage-from-a-startup-task).</span></span>

## <a name="next-steps"></a><span data-ttu-id="db101-243">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="db101-243">Next steps</span></span>
<span data-ttu-id="db101-244">Revise en la nube hello [modelo y el paquete de servicio](cloud-services-model-and-package.md)</span><span class="sxs-lookup"><span data-stu-id="db101-244">Review hello cloud [service model and package](cloud-services-model-and-package.md)</span></span>

<span data-ttu-id="db101-245">Obtener más información acerca de cómo funcionan las [tareas](cloud-services-startup-tasks.md) .</span><span class="sxs-lookup"><span data-stu-id="db101-245">Learn more about how [Tasks](cloud-services-startup-tasks.md) work.</span></span>

<span data-ttu-id="db101-246">[Crear e implementar](cloud-services-how-to-create-deploy-portal.md) el paquete de servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="db101-246">[Create and deploy](cloud-services-how-to-create-deploy-portal.md) your cloud service package.</span></span>

[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef
[tarea]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task
[Startup]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
[entorno]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment
[Variable]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
[Endpoints]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Endpoints
[LocalStorage]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalStorage
[LocalResources]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalResources
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
