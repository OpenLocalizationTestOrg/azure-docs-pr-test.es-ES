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
# <a name="common-cloud-service-startup-tasks"></a>Tareas de inicio comunes para los servicios en la nube
En este artículo se proporciona algunos ejemplos de tareas comunes de inicio puede querer tooperform en su servicio en la nube. Puede utilizar operaciones de tooperform de tareas de inicio antes de que se inicia un rol. Operaciones que podría interesarle tooperform incluyen la instalación de un componente, registrando los componentes COM, configurar claves de registro o iniciar un proceso de ejecución prolongada. 

Vea [este artículo](cloud-services-startup-tasks.md) toounderstand cómo funcionan las tareas de inicio y específicamente cómo toocreate Hola entradas que definen una tarea de inicio.

> [!NOTE]
> Las tareas de inicio no son aplicables tooVirtual máquinas, solo tooCloud servicio Web y roles de trabajo.
> 

## <a name="define-environment-variables-before-a-role-starts"></a>Definición de variables de entorno antes de que se inicie un rol
Si necesita variables de entorno definidas para una tarea específica, use hello [entorno] elemento dentro de hello [tarea] elemento.

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

Las variables también pueden usar un [valor XPath de Azure válido](cloud-services-role-config-xpath.md) tooreference algo acerca de la implementación de Hola. En lugar de usar hello `value` atributo, defina un [RoleInstanceValue] elemento secundario.

```xml
<Variable name="PathToStartupStorage">
    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
</Variable>
```


## <a name="configure-iis-startup-with-appcmdexe"></a>Configuración del inicio IIS con AppCmd.exe
Hola [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) herramienta de línea de comandos puede ser la configuración de IIS toomanage usado en el inicio de Azure. *AppCmd.exe* proporciona opciones de configuración de acceso cómodo y línea de comandos tooconfiguration para su uso en las tareas de inicio en Azure. Con *AppCmd.exe*se pueden agregar modificar o quitar ajustes del sitio web para aplicaciones y sitios.

Sin embargo, hay algunos toowatch de cosas fuera de uso de Hola de *AppCmd.exe* como una tarea de inicio:

* Las tareas de inicio se pueden ejecutar más de una vez entre reinicios. Por ejemplo, cuando un rol se recicla.
* Si una acción *AppCmd.exe* se realiza más de una vez, puede generar un error. Por ejemplo, intentar tooadd una sección demasiado*Web.config* dos veces, podría producirse un error.
* Si las tareas de inicio devuelven un código de salida distinto de cero o un **errorlevel**se producirá un error en las mismas. Por ejemplo, cuando *AppCmd.exe* genera un error.

Es un Hola de toocheck recomendable **errorlevel** después de llamar a *AppCmd.exe*, que es fácil toodo si encapsula llamada Hola demasiado*AppCmd.exe* con un *.cmd*  archivo. Si se detecta una respuesta **errorlevel** conocida, puede ignorarla o devolverla.

Hola errorlevel devuelto por *AppCmd.exe* se muestran en el archivo winerror.h de Hola y también se pueden ver en [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).

### <a name="example-of-managing-hello-error-level"></a>Ejemplo de administración de nivel de error de Hola
Este ejemplo agrega una sección de compresión y una entrada de compresión para JSON toohello *Web.config* archivos con control de errores y registro.

Hola secciones relevantes de hello [ServiceDefinition.csdef] archivo se muestran aquí, que incluyen el establecimiento de hello [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) atributo demasiado`elevated` toogive *AppCmd.exe*  configuración de Hola de toochange de permisos suficientes en hello *Web.config* archivo:

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

Hola *Startup.cmd* por lotes de archivos utiliza *AppCmd.exe* tooadd una sección de compresión y una entrada de compresión para JSON toohello *Web.config* archivo. Hola esperada **errorlevel** de 183 se establece toozero con hello compruebe. Programa de línea de comandos del archivo EXE. Niveles de error inesperados son tooStartupErrorLog.txt ha iniciado.

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

## <a name="add-firewall-rules"></a>Adición de reglas de firewall
A efectos prácticos, hay dos firewalls en Azure. Hola primer firewall controla las conexiones entre la máquina virtual de Hola y Hola fuera world. Este servidor de seguridad se controla mediante hello [extremos] elemento Hola [ServiceDefinition.csdef] archivo.

Hola segundo firewall controla las conexiones entre la máquina virtual de Hola y procesos de hello en esa máquina virtual. Este firewall puede controlarse mediante hello `netsh advfirewall firewall` herramienta de línea de comandos.

Azure crea reglas de firewall para los procesos de hello iniciados en sus roles. Por ejemplo, cuando se inicia un servicio o programa, Azure crea automáticamente tooallow de reglas de firewall necesarias de hello toocommunicate de ese servicio con hello Internet. Sin embargo, si crea un servicio que se inicia un proceso fuera de su rol (por ejemplo, un servicio COM + o una tarea programada de Windows), deberá toomanually crear un servicio de toothat de acceso de firewall regla tooallow. Estas reglas de firewall pueden crearse mediante una tarea de inicio.

Una tarea de inicio que crea una regla de firewall tiene que tener para el atributo [executionContext][tarea] un valor **elevated**se producirá un error en las mismas. Agregar Hola después toohello de tarea de inicio [ServiceDefinition.csdef] archivo.

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

regla de firewall de Hola de tooadd, debe usar Hola adecuado `netsh advfirewall firewall` comandos en el archivo por lotes de inicio. En este ejemplo, la tarea de inicio de hello requiere seguridad y cifrado para el puerto TCP 80.

```cmd
REM   Add a firewall rule in a startup task.

REM   Add an inbound rule requiring security and encryption for TCP port 80 traffic.
netsh advfirewall firewall add rule name="Require Encryption for Inbound TCP/80" protocol=TCP dir=in localport=80 security=authdynenc action=allow >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

## <a name="block-a-specific-ip-address"></a>Bloqueo de una dirección IP específica
Puede restringir un conjunto de tooa de acceso de rol web de Azure de direcciones IP especificadas mediante la modificación de los IIS **web.config** archivo. También necesita un archivo de comandos que desbloquee hello toouse **seguridad IP** sección de hello **ApplicationHost.config** archivo.

toodo desbloquear hello **seguridad IP** sección de hello **ApplicationHost.config** , cree un archivo de comandos que se ejecuta en el inicio de rol. Crear una carpeta en el nivel de raíz de Hola de rol web denominado **inicio** y, dentro de esta carpeta, cree un archivo por lotes denominado **startup.cmd**. Agregue este archivo de proyecto de Visual Studio tooyour y establezca propiedades de hello demasiado**copiar siempre** tooensure que se incluye en el paquete.

Agregar Hola después toohello de tarea de inicio [ServiceDefinition.csdef] archivo.

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

Agregar este comando toohello **startup.cmd** archivo:

```cmd
@echo off
@echo Installing "IPv4 Address and Domain Restrictions" feature 
powershell -ExecutionPolicy Unrestricted -command "Install-WindowsFeature Web-IP-Security"
@echo Unlocking configuration for "IPv4 Address and Domain Restrictions" feature 
%windir%\system32\inetsrv\AppCmd.exe unlock config -section:system.webServer/security/ipSecurity
```

Esta tarea hace hello **startup.cmd** por lotes toobe archivo ejecutar cada vez que se inicializa el rol web de hello, asegurándose de que Hola necesario **seguridad IP** sección está desbloqueada.

Por último, modifique hello [sección system.webServer](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) su rol web **web.config** archivos tooadd una lista de direcciones IP que se concede el acceso, tal y como se muestra en el siguiente ejemplo de Hola:

Esta configuración de ejemplo **permite** tooaccess de todas las direcciones IP Hola servidor salvo Hola dos definidas

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

Esta configuración de ejemplo **deniega** todas las direcciones IP tengan acceso a server Hola excepto Hola dos definido.

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

## <a name="create-a-powershell-startup-task"></a>Creación de una tarea de inicio de PowerShell
Scripts de Windows PowerShell no se puede llamar directamente desde hello [ServiceDefinition.csdef] archivo, pero se puede invocar desde dentro de un archivo por lotes de inicio.

PowerShell (de forma predeterminada) no ejecuta scripts sin firmar. A menos que se registra el script, debe tooconfigure PowerShell scripts sin firmar toorun. toorun scripts sin firmar, hello **ExecutionPolicy** debe establecerse demasiado**Unrestricted**. Hola **ExecutionPolicy** configuración use se basa en la versión de Hola de Windows PowerShell.

```cmd
REM   Run an unsigned PowerShell script and log hello output
PowerShell -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

Si está utilizando un sistema operativo de invitado que se ejecuta PowerShell 2.0 o 1.0 puede forzar toorun versión 2 y si no está disponible, utilice la versión 1.

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

## <a name="create-files-in-local-storage-from-a-startup-task"></a>Creación de archivos de una tarea de inicio en un almacenamiento local
Puede usar un toostore de recursos de almacenamiento local archivos creados por la tarea de inicio que se tiene acceso más adelante con la aplicación.

toocreate Hola recurso de almacenamiento local, agregue un [LocalResources] sección toohello [ServiceDefinition.csdef] de archivos y, a continuación, agregue hello [LocalStorage] elemento secundario. Proporcionar recursos de almacenamiento local de hello un nombre único y un tamaño apropiado para la tarea de inicio.

toouse un recurso de almacenamiento local en la tarea de inicio, debe toocreate una ubicación de recursos de almacenamiento local de entorno variable tooreference Hola. Hola, a continuación, la tarea de inicio y aplicación hello tooread capaz de y escribir el recurso de almacenamiento local de archivos toohello.

Hola secciones relevantes de hello **ServiceDefinition.csdef** archivo se muestran a continuación:

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

Por ejemplo, esto **Startup.cmd** archivo por lotes utiliza hello **PathToStartupStorage** archivo de hello toocreate variable de entorno **MyTest.txt** en almacenamiento local de Hola ubicación.

```cmd
REM   Create a simple text file.

ECHO This text will go into hello MyTest.txt file which will be in hello    >  "%PathToStartupStorage%\MyTest.txt"
ECHO path pointed tooby hello PathToStartupStorage environment variable.  >> "%PathToStartupStorage%\MyTest.txt"
ECHO hello contents of hello PathToStartupStorage environment variable is   >> "%PathToStartupStorage%\MyTest.txt"
ECHO "%PathToStartupStorage%".                                          >> "%PathToStartupStorage%\MyTest.txt"

REM   Exit hello batch file with ERRORLEVEL 0.

EXIT /b 0
```

Puede tener acceso a carpeta de almacenamiento local de hello Azure SDK mediante hello [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) método.

```csharp
string localStoragePath = Microsoft.WindowsAzure.ServiceRuntime.RoleEnvironment.GetLocalResource("StartupLocalStorage").RootPath;

string fileContent = System.IO.File.ReadAllText(System.IO.Path.Combine(localStoragePath, "MyTestFile.txt"));
```

## <a name="run-in-hello-emulator-or-cloud"></a>Ejecutar en el emulador de Hola o en la nube
Puede tener la tarea de inicio emprenda acciones diferentes cuando se está ejecutando en hello en la nube en comparación con toowhen que se encuentra en el emulador de proceso de Hola. Por ejemplo, puede que desee toouse una nueva copia de los datos SQL sólo cuando se ejecuta en el emulador de Hola. O bien, puede que desee toodo algunas optimizaciones de rendimiento para la nube de Hola que no es necesario toodo cuando se ejecuta en el emulador de Hola.

Este tooperform capacidad diferente acciones en hello emulador de proceso y Hola nube se consigue mediante la creación de una variable de entorno en hello [ServiceDefinition.csdef] archivo. A continuación, pruebe esa variable de entorno para un valor en la tarea de inicio.

variable de entorno de hello toocreate, agregar hello [Variable]/[RoleInstanceValue] elemento y cree un valor de XPath de `/RoleEnvironment/Deployment/@emulated`. Hola valo hello **ComputeEmulatorRunning %** variable de entorno es `true` cuando se ejecuta en el emulador de proceso de hello, y `false` cuando se ejecuta en la nube de Hola.

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

tarea Hello ahora puede comprobar hello **ComputeEmulatorRunning %** acciones diferentes tooperform variable de entorno, en función de si está ejecutando el rol de hello en hello en la nube u Hola emulador. Aquí tiene un script de shell de .cmd que busca esa variable de entorno.

```cmd
REM   Check if this task is running on hello compute emulator.

IF "%ComputeEmulatorRunning%" == "true" (
    REM   This task is running on hello compute emulator. Perform tasks that must be run only in hello compute emulator.
) ELSE (
    REM   This task is running on hello cloud. Perform tasks that must be run only in hello cloud.
)
```


## <a name="detect-that-your-task-has-already-run"></a>Detección de si la tarea ya se ha ejecutado
rol de Hello puede reciclar sin reiniciar el equipo haciendo que su toorun de tareas de inicio de nuevo. No hay ningún tooindicate de marca que ya se ha ejecutado una tarea en hello hospeda la máquina virtual. Puede que en algunas tareas no importe si se ejecutan varias veces. Sin embargo, puede encontrarse con una situación donde debe tooprevent una tarea de ejecución de más de una vez.

toodetect manera más sencilla Hola que ya se ha ejecutado una tarea es un archivo en hello toocreate **% TEMP %** carpeta cuando se realiza correctamente la tarea hello y búsquelo en hello principio de la tarea hello. Este es un ejemplo script de shell de cmd que lo hace.

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

## <a name="task-best-practices"></a>Prácticas recomendadas para las tareas
A continuación presentamos algunas prácticas recomendadas que debería seguir al configurar una tarea para el rol web o de trabajo.

### <a name="always-log-startup-activities"></a>Registre siempre las actividades de inicio
Visual Studio no proporciona un depurador toostep archivos por lotes, por lo que es buena tooget mayor cantidad de datos en la operación de Hola de archivos por lotes como sea posible. Registro de salida de hello de archivos por lotes, ambos **stdout** y **stderr**, puede obtener información importante al tratar de toodebug y corregir archivos por lotes. toolog ambos **stdout** y **stderr** toohello StartupLog.txt archivo Hola de hello directorio apunta tooby **% TEMP %** variable de entorno, agregue texto hello `>>  "%TEMP%\\StartupLog.txt" 2>&1`toohello final específicas de líneas desea toolog. Por ejemplo, tooexecute setup.exe en hello **% PathToApp1Install %** directorio:

    "%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

toosimplify el código xml, puede crear un contenedor *cmd* archivo que se invocan de la configuración de inicio de tareas junto con el registro y garantiza cada Hola de recursos compartidos de la tarea secundaria mismas variables de entorno.

Quizá le resulte aunque molestar toouse `>> "%TEMP%\StartupLog.txt" 2>&1` en extremo Hola de cada tarea de inicio. Puede aplicar el registro de tareas mediante la creación de un contenedor que controle el registro automáticamente. Este contenedor llama a archivo de lote real de hello desea toorun. Cualquier resultado del archivo por lotes de destino de hello será redirigido toohello *Startuplog.txt* archivo.

Hola de ejemplo siguiente muestra cómo tooredirect todos los resultados desde un archivo por lotes de inicio. En este ejemplo, archivo de hello ServerDefinition.csdef crea una tarea de inicio que llama *logwrap.cmd*. *logwrap.cmd* llamadas *startup2.cmd; para ello*, redirige todos los resultados demasiado**% TEMP %\\StartupLog.txt**.

ServiceDefinition.cmd:

```xml
<Startup>
    <Task commandLine="logwrap.cmd startup2.cmd" executionContext="limited" taskType="simple" />
</Startup>
```

**logwrap.cmd:**

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

**Startup2.cmd:**

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

Ejemplo de salida de hello **StartupLog.txt** archivo:

```txt
[Mon 10/17/2016 20:24:46.75] == START logwrap.cmd ============================================== 
[Mon 10/17/2016 20:24:46.75] Running command1.cmd 
[Mon 10/17/2016 20:24:46.77] Some log information about this task
[Mon 10/17/2016 20:24:46.77] Some more log information about this task
[Mon 10/17/2016 20:24:46.77] Done 
[Mon 10/17/2016 20:24:46.77] == END logwrap.cmd ================================================ 
```

> [!TIP]
> Hola **StartupLog.txt** archivo se encuentra en hello *C:\Resources\temp\\\RoleTemp {identificador de rol}* carpeta.
> 
> 

### <a name="set-executioncontext-appropriately-for-startup-tasks"></a>Establezca executionContext correctamente para las tareas de inicio
Establecer los privilegios de forma adecuada para la tarea de inicio de Hola. A veces, las tareas de inicio deben ejecutar con privilegios elevados, aunque Hola rol se ejecuta con privilegios normales.

Hola [executionContext][tarea] atributo establece el nivel de privilegio de Hola de tarea de inicio de Hola. Usar `executionContext="limited"` significa tiene la tarea de inicio de Hola Hola de mismo nivel de privilegios como rol de Hola. Usar `executionContext="elevated"` significa la tarea de inicio de hello tiene privilegios de administrador, que permite el inicio de hello tareas del Administrador de tareas tooperform sin asignar rol de tooyour de privilegios de administrador.

Un ejemplo de una tarea de inicio que requiere privilegios elevados es una tarea de inicio que utiliza **AppCmd.exe** tooconfigure IIS. **AppCmd.exe** requiere `executionContext="elevated"`.

### <a name="use-hello-appropriate-tasktype"></a>Usar valor de taskType apropiado de Hola
Hola [taskType][tarea] atributo determina que se ejecuta la tarea de inicio de hello forma Hola. Hay tres valores: **simple**, **background** y **foreground**. Hello tareas de fondo y primer plano se inician de forma asincrónica y, a continuación, se ejecutan las tareas sencillas de hello sincrónicamente uno en uno.

Con **simple** las tareas de inicio, puede establecer el orden de hello en el que se ejecutan las tareas de Hola por orden de hello en qué Hola se enumeran las tareas en el archivo ServiceDefinition.csdef de Hola. Si un **simple** tarea finaliza con un usuario que no sea cero código de salida, a continuación, Hola procedimiento de inicio se detiene y no se inicia el rol de Hola.

Hola diferencia entre **fondo** las tareas de inicio y **primer plano** las tareas de inicio es que **primer plano** tareas mantener la ejecución de la función de hello hasta hello  **primer plano** finaliza la tarea. Esto también significa que si hello **primer plano** tarea se bloquea o se bloquea, el rol de hello no se reciclará hasta hello **primer plano** se fuerza la tarea cerrado. Por esta razón, **fondo** se recomiendan las tareas para tareas de inicio asincrónicas a menos que necesite esa función de hello **primer plano** tarea.

### <a name="end-batch-files-with-exit-b-0"></a>Finalice lo archivos por lotes con EXIT /B 0
Hello rol solo se iniciará si hello **errorlevel** de cada uno de su inicio simple tarea es cero. No todos los programas establecen hello **errorlevel** (código de salida) correctamente, por lo que archivo por lotes de hello debe terminar con un `EXIT /B 0` si todo lo que se ejecutaba correctamente.

Falta un `EXIT /B 0` en hello final de un archivo por lotes de inicio es una causa frecuente de los roles que no se inician.

> [!NOTE]
> He observado ese lote anidado archivos a veces bloquearse cuando se utiliza hello `/B` parámetro. Puede que desee toomake seguro de que en este problema de falta de respuesta no se realiza si el archivo por lotes actual llama a otro archivo por lotes, como si usa hello [contenedor del registro](#always-log-startup-activities). Puede omitir hello `/B` parámetro en este caso.
> 
> 

### <a name="expect-startup-tasks-toorun-more-than-once"></a>Esperar toorun de tareas de inicio más de una vez
No todos los reciclajes de rol incluyen un reinicio, pero todos incluyen la ejecución de todas las tareas de inicio. Esto significa que las tareas de inicio deben ser capaz de toorun varias veces entre reinicios sin problemas. Esto se explica en hello [sección anterior](#detect-that-your-task-has-already-run).

### <a name="use-local-storage-toostore-files-that-must-be-accessed-in-hello-role"></a>Utilizar almacenamiento local toostore archivos que deben tener acceso en función de Hola
Si desea toocopy o crear un archivo durante la tarea de inicio, a continuación, es accesible tooyour rol, ese archivo se debe colocar en el almacenamiento local. Vea hello [sección anterior](#create-files-in-local-storage-from-a-startup-task).

## <a name="next-steps"></a>Pasos siguientes
Revise en la nube hello [modelo y el paquete de servicio](cloud-services-model-and-package.md)

Obtener más información acerca de cómo funcionan las [tareas](cloud-services-startup-tasks.md) .

[Crear e implementar](cloud-services-how-to-create-deploy-portal.md) el paquete de servicio en la nube

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
