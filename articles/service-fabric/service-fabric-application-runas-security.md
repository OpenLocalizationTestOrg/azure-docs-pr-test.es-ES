---
title: aaaLearn acerca de las directivas de seguridad de Azure microservicios | Documentos de Microsoft
description: "Información general sobre cómo toorun una aplicación de Service Fabric en sistema y las cuentas de seguridad local, incluido el punto de SetupEntry Hola donde una aplicación necesita tooperform algunas privilegiado acción antes de empezar"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 4242a1eb-a237-459b-afbf-1e06cfa72732
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: mfussell
ms.openlocfilehash: f5afba69e09aa4f3c9efa4d3efc6995c813a1f71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-security-policies-for-your-application"></a><span data-ttu-id="289f6-103">Configuración de directivas de seguridad para la aplicación</span><span class="sxs-lookup"><span data-stu-id="289f6-103">Configure security policies for your application</span></span>
<span data-ttu-id="289f6-104">Mediante el uso de Azure Service Fabric, puede proteger las aplicaciones que se ejecutan en el clúster de hello en distintas cuentas de usuario.</span><span class="sxs-lookup"><span data-stu-id="289f6-104">By using Azure Service Fabric, you can secure applications that are running in hello cluster under different user accounts.</span></span> <span data-ttu-id="289f6-105">Service Fabric también ayuda a certificados, archivos, directorios y recursos de hello segura que se usan las aplicaciones en tiempo de Hola de implementación con cuentas de usuario de hello, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="289f6-105">Service Fabric also helps secure hello resources that are used by applications at hello time of deployment under hello user accounts--for example, files, directories, and certificates.</span></span> <span data-ttu-id="289f6-106">Esto aumenta la seguridad entre aplicaciones en ejecución, incluso en un entorno hospedado compartido.</span><span class="sxs-lookup"><span data-stu-id="289f6-106">This makes running applications, even in a shared hosted environment, more secure from one another.</span></span>

<span data-ttu-id="289f6-107">De forma predeterminada, aplicaciones de Service Fabric se ejecutan bajo la cuenta de hello hello Fabric.exe proceso se ejecuta bajo.</span><span class="sxs-lookup"><span data-stu-id="289f6-107">By default, Service Fabric applications run under hello account that hello Fabric.exe process runs under.</span></span> <span data-ttu-id="289f6-108">Service Fabric también proporciona capacidad de hello toorun aplicaciones mediante una cuenta de sistema local, que se especifica en el manifiesto de aplicación Hola o cuenta de usuario local.</span><span class="sxs-lookup"><span data-stu-id="289f6-108">Service Fabric also provides hello capability toorun applications under a local user account or local system account, which is specified within hello application manifest.</span></span> <span data-ttu-id="289f6-109">Los tipos de cuenta de sistema local compatibles son **LocalUser**, **NetworkService**, **LocalService** y **LocalSystem**.</span><span class="sxs-lookup"><span data-stu-id="289f6-109">Supported local system account types are **LocalUser**, **NetworkService**, **LocalService**, and **LocalSystem**.</span></span>

 <span data-ttu-id="289f6-110">Si estás ejecutando Service Fabric en Windows Server en el centro de datos utilizando el instalador independiente de hello, puede utilizar cuentas de dominio de Active Directory, incluidas las cuentas de servicio administradas de grupo.</span><span class="sxs-lookup"><span data-stu-id="289f6-110">When you're running Service Fabric on Windows Server in your datacenter by using hello standalone installer, you can use Active Directory domain accounts, including group managed service accounts.</span></span>

<span data-ttu-id="289f6-111">Puede definir y crear grupos de usuarios para que se pueden agregar uno o más usuarios tooeach toobe de grupo administrada de manera conjunta.</span><span class="sxs-lookup"><span data-stu-id="289f6-111">You can define and create user groups so that one or more users can be added tooeach group toobe managed together.</span></span> <span data-ttu-id="289f6-112">Esto es útil cuando hay varios usuarios para los puntos de entrada de servicio diferente y es necesario toohave ciertos privilegios comunes que están disponibles en el nivel de grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="289f6-112">This is useful when there are multiple users for different service entry points and they need toohave certain common privileges that are available at hello group level.</span></span>

## <a name="configure-hello-policy-for-a-service-setup-entry-point"></a><span data-ttu-id="289f6-113">Configurar la directiva de Hola para un punto de entrada del programa de instalación de servicio</span><span class="sxs-lookup"><span data-stu-id="289f6-113">Configure hello policy for a service setup entry point</span></span>
<span data-ttu-id="289f6-114">Como se describe en hello [modelo de aplicación](service-fabric-application-model.md), Hola punto de entrada del programa de instalación, **SetupEntryPoint**, es un punto de entrada con privilegios que se ejecuta con hello mismo credenciales como Service Fabric (normalmente hello *NetworkService* cuenta) antes de cualquier otro punto de entrada.</span><span class="sxs-lookup"><span data-stu-id="289f6-114">As described in hello [application model](service-fabric-application-model.md), hello setup entry point, **SetupEntryPoint**, is a privileged entry point that runs with hello same credentials as Service Fabric (typically hello *NetworkService* account) before any other entry point.</span></span> <span data-ttu-id="289f6-115">archivo ejecutable de Hello especificado por **EntryPoint** suele ser host de servicio de ejecución prolongada de Hola.</span><span class="sxs-lookup"><span data-stu-id="289f6-115">hello executable that is specified by **EntryPoint** is typically hello long-running service host.</span></span> <span data-ttu-id="289f6-116">Por lo que tiene una entrada de programa de instalación independiente de punto, evita tener toorun host del servicio Hola ejecutable con privilegios altos durante largos períodos de tiempo.</span><span class="sxs-lookup"><span data-stu-id="289f6-116">So having a separate setup entry point avoids having toorun hello service host executable with high privileges for extended periods of time.</span></span> <span data-ttu-id="289f6-117">Hola ejecutable que **EntryPoint** especifica se ejecuta después de **SetupEntryPoint** se cierra correctamente.</span><span class="sxs-lookup"><span data-stu-id="289f6-117">hello executable that **EntryPoint** specifies is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="289f6-118">Hello proceso resultante se supervisa y se reinicia y vuelve a comenzar con **SetupEntryPoint** si alguna vez finaliza o se bloquea.</span><span class="sxs-lookup"><span data-stu-id="289f6-118">hello resulting process is monitored and restarted, and begins again with **SetupEntryPoint** if it ever terminates or crashes.</span></span>

<span data-ttu-id="289f6-119">Hola aquí te mostramos un ejemplo de manifiesto de servicio simple que muestra Hola SetupEntryPoint y Hola punto de entrada principal para el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="289f6-119">hello following is a simple service manifest example that shows hello SetupEntryPoint and hello main EntryPoint for hello service.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
        <WorkingFolder>CodePackage</WorkingFolder>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
  </CodePackage>
  <ConfigPackage Name="Config" Version="1.0.0" />
</ServiceManifest>
```

### <a name="configure-hello-policy-by-using-a-local-account"></a><span data-ttu-id="289f6-120">Configurar directiva de hello mediante una cuenta local</span><span class="sxs-lookup"><span data-stu-id="289f6-120">Configure hello policy by using a local account</span></span>
<span data-ttu-id="289f6-121">Después de configurar Hola servicio toohave un punto de entrada del programa de instalación, puede cambiar los permisos de seguridad de Hola que se ejecuta bajo en el manifiesto de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="289f6-121">After you configure hello service toohave a setup entry point, you can change hello security permissions that it runs under in hello application manifest.</span></span> <span data-ttu-id="289f6-122">Hola de ejemplo siguiente muestra cómo tooconfigure Hola toorun de servicio con privilegios de cuenta de usuario administrador.</span><span class="sxs-lookup"><span data-stu-id="289f6-122">hello following example shows how tooconfigure hello service toorun under user administrator account privileges.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="SetupAdminUser" EntryPointType="Setup" />
      </Policies>
   </ServiceManifestImport>
   <Principals>
      <Users>
         <User Name="SetupAdminUser">
            <MemberOf>
               <SystemGroup Name="Administrators" />
            </MemberOf>
         </User>
      </Users>
   </Principals>
</ApplicationManifest>
```

<span data-ttu-id="289f6-123">En primer lugar, cree una sección **Principals** con un nombre de usuario, como SetupAdminUser.</span><span class="sxs-lookup"><span data-stu-id="289f6-123">First, create a **Principals** section with a user name, such as SetupAdminUser.</span></span> <span data-ttu-id="289f6-124">Esto indica que ese usuario hello es un miembro del grupo de sistema de los administradores de Hola.</span><span class="sxs-lookup"><span data-stu-id="289f6-124">This indicates that hello user is a member of hello Administrators system group.</span></span>

<span data-ttu-id="289f6-125">Después, en hello **ServiceManifestImport** sección, configure una directiva tooapply esta entidad de seguridad demasiado**SetupEntryPoint**.</span><span class="sxs-lookup"><span data-stu-id="289f6-125">Next, under hello **ServiceManifestImport** section, configure a policy tooapply this principal too**SetupEntryPoint**.</span></span> <span data-ttu-id="289f6-126">Esto indica a Service Fabric que cuando hello **MySetup.bat** archivo se ejecuta, debería ser `RunAs` con privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="289f6-126">This tells Service Fabric that when hello **MySetup.bat** file is run, it should be `RunAs` with administrator privileges.</span></span> <span data-ttu-id="289f6-127">Dado que tiene *no* aplicar un punto de entrada principal de toohello de directiva, el código de hello en **MyServiceHost.exe** se ejecuta en el sistema de hello **NetworkService** cuenta.</span><span class="sxs-lookup"><span data-stu-id="289f6-127">Given that you have *not* applied a policy toohello main entry point, hello code in **MyServiceHost.exe** runs under hello system **NetworkService** account.</span></span> <span data-ttu-id="289f6-128">Se trata de cuenta predeterminada de Hola que todos los puntos de entrada de servicio se ejecutan como.</span><span class="sxs-lookup"><span data-stu-id="289f6-128">This is hello default account that all service entry points are run as.</span></span>

<span data-ttu-id="289f6-129">Ahora agreguemos Hola archivo MySetup.bat toohello Visual Studio project tootest Hola privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="289f6-129">Let's now add hello file MySetup.bat toohello Visual Studio project tootest hello administrator privileges.</span></span> <span data-ttu-id="289f6-130">En Visual Studio, haga clic en proyecto de servicio de Hola y agregue un nuevo archivo denominado MySetup.bat.</span><span class="sxs-lookup"><span data-stu-id="289f6-130">In Visual Studio, right-click hello service project and add a new file called MySetup.bat.</span></span>

<span data-ttu-id="289f6-131">A continuación, asegúrese de que ese archivo de MySetup.bat Hola se incluye en el paquete del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="289f6-131">Next, ensure that hello MySetup.bat file is included in hello service package.</span></span> <span data-ttu-id="289f6-132">De forma predeterminada, no lo está.</span><span class="sxs-lookup"><span data-stu-id="289f6-132">By default, it is not.</span></span> <span data-ttu-id="289f6-133">Seleccione el archivo hello, haga clic en el menú contextual de tooget hello y elija **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="289f6-133">Select hello file, right-click tooget hello context menu, and choose **Properties**.</span></span> <span data-ttu-id="289f6-134">En el cuadro de diálogo de propiedades de hello, asegúrese de que **copiar tooOutput directorio** se establece demasiado**copiar si es posterior**.</span><span class="sxs-lookup"><span data-stu-id="289f6-134">In hello Properties dialog box, ensure that **Copy tooOutput Directory** is set too**Copy if newer**.</span></span> <span data-ttu-id="289f6-135">Vea Hola siguiente captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="289f6-135">See hello following screenshot.</span></span>

![CopyToOutput de Visual Studio para el archivo por lotes de SetupEntryPoint][image1]

<span data-ttu-id="289f6-137">Ahora abra hello MySetup.bat archivo y agregue Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="289f6-137">Now open hello MySetup.bat file and add hello following commands:</span></span>

```
REM Set a system environment variable. This requires administrator privilege
setx -m TestVariable "MyValue"
echo System TestVariable set too> out.txt
echo %TestVariable% >> out.txt

REM toodelete this system variable us
REM REG delete "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment" /v TestVariable /f
```

<span data-ttu-id="289f6-138">A continuación, compile e implemente el clúster de desarrollo local de hello solución tooa.</span><span class="sxs-lookup"><span data-stu-id="289f6-138">Next, build and deploy hello solution tooa local development cluster.</span></span> <span data-ttu-id="289f6-139">Después de que se inició el servicio de hello tal como se muestra en el Explorador de tejido de servicio, puede ver que ese archivo de MySetup.bat Hola fue correcto de una de dos maneras.</span><span class="sxs-lookup"><span data-stu-id="289f6-139">After hello service has started, as shown in Service Fabric Explorer, you can see that hello MySetup.bat file was successful in a two ways.</span></span> <span data-ttu-id="289f6-140">Abra un símbolo del sistema de PowerShell y escriba:</span><span class="sxs-lookup"><span data-stu-id="289f6-140">Open a PowerShell command prompt and type:</span></span>

```
PS C:\ [Environment]::GetEnvironmentVariable("TestVariable","Machine")
MyValue
```

<span data-ttu-id="289f6-141">Tenga en cuenta, a continuación, nombre de hello del nodo de Hola donde servicio Hola se ha implementado y se inició en el Explorador de Service Fabric: por ejemplo, nodo 2.</span><span class="sxs-lookup"><span data-stu-id="289f6-141">Then, note hello name of hello node where hello service was deployed and started in Service Fabric Explorer--for example, Node 2.</span></span> <span data-ttu-id="289f6-142">A continuación, navegue toohello instancia trabajo carpeta toofind hello out.txt archivo de aplicación que muestra el valor de Hola de **TestVariable**.</span><span class="sxs-lookup"><span data-stu-id="289f6-142">Next, navigate toohello application instance work folder toofind hello out.txt file that shows hello value of **TestVariable**.</span></span> <span data-ttu-id="289f6-143">Por ejemplo, si este servicio se ha implementado tooNode 2, a continuación, puede ir hello en la ruta de acceso toothis **MyApplicationType**:</span><span class="sxs-lookup"><span data-stu-id="289f6-143">For example, if this service was deployed tooNode 2, then you can go toothis path for hello **MyApplicationType**:</span></span>

```
C:\SfDevCluster\Data\_App\Node.2\MyApplicationType_App\work\out.txt
```

### <a name="configure-hello-policy-by-using-local-system-accounts"></a><span data-ttu-id="289f6-144">Configurar la directiva de hello mediante cuentas de sistema local</span><span class="sxs-lookup"><span data-stu-id="289f6-144">Configure hello policy by using local system accounts</span></span>
<span data-ttu-id="289f6-145">A menudo, es preferible toorun script de inicio de hello usando una cuenta de sistema local en lugar de una cuenta de administrador.</span><span class="sxs-lookup"><span data-stu-id="289f6-145">Often, it's preferable toorun hello startup script by using a local system account rather than an administrator account.</span></span> <span data-ttu-id="289f6-146">Ejecutar la directiva de ejecución de hello como miembro del programa Hola a grupo de administradores normalmente no funciona bien porque máquinas tienen Control de acceso de usuario (UAC) habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="289f6-146">Running hello RunAs policy as a member of hello Administrators group typically doesn’t work well because machines have User Access Control (UAC) enabled by default.</span></span> <span data-ttu-id="289f6-147">En tales casos, **recomendación de hello es toorun hello SetupEntryPoint como LocalSystem, en lugar de como un grupo de usuario local agregada tooAdministrators**.</span><span class="sxs-lookup"><span data-stu-id="289f6-147">In such cases, **hello recommendation is toorun hello SetupEntryPoint as LocalSystem, instead of as a local user added tooAdministrators group**.</span></span> <span data-ttu-id="289f6-148">Hello en el ejemplo siguiente se muestra configuración hello SetupEntryPoint toorun como LocalSystem:</span><span class="sxs-lookup"><span data-stu-id="289f6-148">hello following example shows setting hello SetupEntryPoint toorun as LocalSystem:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="SetupLocalSystem" EntryPointType="Setup" />
      </Policies>
   </ServiceManifestImport>
   <Principals>
      <Users>
         <User Name="SetupLocalSystem" AccountType="LocalSystem" />
      </Users>
   </Principals>
</ApplicationManifest>
```

## <a name="start-powershell-commands-from-a-setup-entry-point"></a><span data-ttu-id="289f6-149">Inicio de comandos de PowerShell desde un SetupEntryPoint</span><span class="sxs-lookup"><span data-stu-id="289f6-149">Start PowerShell commands from a setup entry point</span></span>
<span data-ttu-id="289f6-150">toorun PowerShell de hello **SetupEntryPoint** punto, puede ejecutar **PowerShell.exe** en un archivo por lotes que señala tooa PowerShell de archivos.</span><span class="sxs-lookup"><span data-stu-id="289f6-150">toorun PowerShell from hello **SetupEntryPoint** point, you can run **PowerShell.exe** in a batch file that points tooa PowerShell file.</span></span> <span data-ttu-id="289f6-151">En primer lugar, agregue un proyecto de servicio de PowerShell archivo toohello: por ejemplo, **MySetup.ps1**.</span><span class="sxs-lookup"><span data-stu-id="289f6-151">First, add a PowerShell file toohello service project--for example, **MySetup.ps1**.</span></span> <span data-ttu-id="289f6-152">Recuerde hello tooset *copiar si es posterior* propiedad para ese archivo hello también se incluye en el paquete del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="289f6-152">Remember tooset hello *Copy if newer* property so that hello file is also included in hello service package.</span></span> <span data-ttu-id="289f6-153">Hello en el ejemplo siguiente se muestra un archivo por lotes de ejemplo que se inicia un archivo de PowerShell denominado MySetup.ps1, que establece una variable de entorno de sistema denominada **TestVariable**.</span><span class="sxs-lookup"><span data-stu-id="289f6-153">hello following example shows a sample batch file that starts a PowerShell file called MySetup.ps1, which sets a system environment variable called **TestVariable**.</span></span>

<span data-ttu-id="289f6-154">MySetup.bat toostart un archivo de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="289f6-154">MySetup.bat toostart a PowerShell file:</span></span>

```
powershell.exe -ExecutionPolicy Bypass -Command ".\MySetup.ps1"
```

<span data-ttu-id="289f6-155">En el archivo de PowerShell de hello, agregue Hola después tooset una variable de entorno del sistema:</span><span class="sxs-lookup"><span data-stu-id="289f6-155">In hello PowerShell file, add hello following tooset a system environment variable:</span></span>

```
[Environment]::SetEnvironmentVariable("TestVariable", "MyValue", "Machine")
[Environment]::GetEnvironmentVariable("TestVariable","Machine") > out.txt
```

> [!NOTE]
> <span data-ttu-id="289f6-156">De forma predeterminada, cuando se ejecuta el archivo por lotes de hello, parece en la carpeta de la aplicación hello llama **trabajar** para los archivos.</span><span class="sxs-lookup"><span data-stu-id="289f6-156">By default, when hello batch file runs, it looks at hello application folder called **work** for files.</span></span> <span data-ttu-id="289f6-157">En este caso, cuando se ejecuta MySetup.bat, queremos este hello toofind MySetup.ps1 en el archivo hello misma carpeta, que es la aplicación hello **el paquete de código** carpeta.</span><span class="sxs-lookup"><span data-stu-id="289f6-157">In this case, when MySetup.bat runs, we want this toofind hello MySetup.ps1 file in hello same folder, which is hello application **code package** folder.</span></span> <span data-ttu-id="289f6-158">toochange esta carpeta, la carpeta de trabajo de Hola de conjunto:</span><span class="sxs-lookup"><span data-stu-id="289f6-158">toochange this folder, set hello working folder:</span></span>
> 
> 

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    </ExeHost>
</SetupEntryPoint>
```

## <a name="use-console-redirection-for-local-debugging"></a><span data-ttu-id="289f6-159">Uso de la redirección de la consola para la depuración local</span><span class="sxs-lookup"><span data-stu-id="289f6-159">Use console redirection for local debugging</span></span>
<span data-ttu-id="289f6-160">En ocasiones, resulta útil toosee salida de la consola Hola de ejecución de un script para fines de depuración.</span><span class="sxs-lookup"><span data-stu-id="289f6-160">Occasionally, it's useful toosee hello console output from running a script for debugging purposes.</span></span> <span data-ttu-id="289f6-161">toodo esto, puede establecer una directiva de redirección de consola, que escribe el archivo de tooa de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="289f6-161">toodo this, you can set a console redirection policy, which writes hello output tooa file.</span></span> <span data-ttu-id="289f6-162">Hello archivo de salida se denomina de carpeta de la aplicación escrita toohello **registro** en el nodo de Hola donde se ha implementado y ejecutar aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="289f6-162">hello file output is written toohello application folder called **log** on hello node where hello application is deployed and run.</span></span> <span data-ttu-id="289f6-163">(Consulte dónde toofind esto en el anterior ejemplo de Hola.)</span><span class="sxs-lookup"><span data-stu-id="289f6-163">(See where toofind this in hello preceding example.)</span></span>

> [!WARNING]
> <span data-ttu-id="289f6-164">Nunca use Directiva de redirección de consola de hello en una aplicación que se implementa en producción porque esto puede afectar a la conmutación por error de aplicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="289f6-164">Never use hello console redirection policy in an application that is deployed in production because this can affect hello application failover.</span></span> <span data-ttu-id="289f6-165">*Solo* debe usarla con fines de depuración y desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="289f6-165">*Only* use this for local development and debugging purposes.</span></span>  
> 
> 

<span data-ttu-id="289f6-166">Hello en el ejemplo siguiente se muestra redirección de la consola de configuración Hola con un valor de FileRetentionCount:</span><span class="sxs-lookup"><span data-stu-id="289f6-166">hello following example shows setting hello console redirection with a FileRetentionCount value:</span></span>

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="10"/>
    </ExeHost>
</SetupEntryPoint>
```

<span data-ttu-id="289f6-167">Si cambia ahora hello MySetup.ps1 archivo toowrite una **Echo** comando, se escribirá toohello el archivo de salida con fines de depuración:</span><span class="sxs-lookup"><span data-stu-id="289f6-167">If you now change hello MySetup.ps1 file toowrite an **Echo** command, this will write toohello output file for debugging purposes:</span></span>

```
Echo "Test console redirection which writes toohello application log folder on hello node that hello application is deployed to"
```

<span data-ttu-id="289f6-168">**Después de haber depurado el script, quite inmediatamente esta directiva de redireccionamiento de consola**.</span><span class="sxs-lookup"><span data-stu-id="289f6-168">**After you debug your script, immediately remove this console redirection policy**.</span></span>

## <a name="configure-a-policy-for-service-code-packages"></a><span data-ttu-id="289f6-169">Configuración de una directiva para los paquetes de código del servicio</span><span class="sxs-lookup"><span data-stu-id="289f6-169">Configure a policy for service code packages</span></span>
<span data-ttu-id="289f6-170">En hello pasos anteriores, ha visto cómo tooapply una tooSetupEntryPoint de directiva de ejecución.</span><span class="sxs-lookup"><span data-stu-id="289f6-170">In hello preceding steps, you saw how tooapply a RunAs policy tooSetupEntryPoint.</span></span> <span data-ttu-id="289f6-171">Echemos un vistazo un poco más en cómo toocreate diferentes entidades de seguridad que se pueden aplicar como directivas de servicio.</span><span class="sxs-lookup"><span data-stu-id="289f6-171">Let's look a little deeper into how toocreate different principals that can be applied as service policies.</span></span>

### <a name="create-local-user-groups"></a><span data-ttu-id="289f6-172">Creación de grupos de usuarios locales</span><span class="sxs-lookup"><span data-stu-id="289f6-172">Create local user groups</span></span>
<span data-ttu-id="289f6-173">Puede definir y crear grupos de usuarios que permite que uno o más toobe a los usuarios agrega grupo tooa.</span><span class="sxs-lookup"><span data-stu-id="289f6-173">You can define and create user groups that allow one or more users toobe added tooa group.</span></span> <span data-ttu-id="289f6-174">Esto es útil si hay varios usuarios para los puntos de entrada de servicio diferente y necesitan toohave ciertos privilegios comunes que están disponibles en el nivel de grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="289f6-174">This is useful if there are multiple users for different service entry points and they need toohave certain common privileges that are available at hello group level.</span></span> <span data-ttu-id="289f6-175">Hello en el ejemplo siguiente se muestra un grupo local denominado **LocalAdminGroup** que tenga privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="289f6-175">hello following example shows a local group called **LocalAdminGroup** that has administrator privileges.</span></span> <span data-ttu-id="289f6-176">Dos usuarios, Customer1 y Customer2, se convierten en miembros de este grupo local.</span><span class="sxs-lookup"><span data-stu-id="289f6-176">Two users, Customer1 and Customer2, are made members of this local group.</span></span>

```xml
<Principals>
 <Groups>
   <Group Name="LocalAdminGroup">
     <Membership>
       <SystemGroup Name="Administrators"/>
     </Membership>
   </Group>
 </Groups>
  <Users>
     <User Name="Customer1">
        <MemberOf>
           <Group NameRef="LocalAdminGroup" />
        </MemberOf>
     </User>
    <User Name="Customer2">
      <MemberOf>
        <Group NameRef="LocalAdminGroup" />
      </MemberOf>
    </User>
  </Users>
</Principals>
```

### <a name="create-local-users"></a><span data-ttu-id="289f6-177">Creación de usuarios locales</span><span class="sxs-lookup"><span data-stu-id="289f6-177">Create local users</span></span>
<span data-ttu-id="289f6-178">Puede crear un usuario local que puede ser utilizado toohelp segura de servicios dentro de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="289f6-178">You can create a local user that can be used toohelp secure a service within hello application.</span></span> <span data-ttu-id="289f6-179">Cuando un **usuarioLocal** tipo de cuenta se especifica en la sección de entidades de seguridad de Hola Hola del manifiesto de aplicación, Service Fabric crea cuentas de usuario locales en equipos donde se implementa la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="289f6-179">When a **LocalUser** account type is specified in hello principals section of hello application manifest, Service Fabric creates local user accounts on machines where hello application is deployed.</span></span> <span data-ttu-id="289f6-180">De forma predeterminada, estas cuentas no tienen Hola mismos nombres que los especificados en la aplicación hello manifiesto (por ejemplo, Customer3 en el siguiente ejemplo de Hola).</span><span class="sxs-lookup"><span data-stu-id="289f6-180">By default, these accounts do not have hello same names as those specified in hello application manifest (for example, Customer3 in hello following sample).</span></span> <span data-ttu-id="289f6-181">En su lugar, se generan dinámicamente y tienen contraseñas aleatorias.</span><span class="sxs-lookup"><span data-stu-id="289f6-181">Instead, they are dynamically generated and have random passwords.</span></span>

```xml
<Principals>
  <Users>
     <User Name="Customer3" AccountType="LocalUser" />
  </Users>
</Principals>
```

<span data-ttu-id="289f6-182">Si una aplicación requiere que ser la misma en todos los equipos (por ejemplo, la autenticación NTLM tooenable) Hola cuentas de usuario y contraseñas, el manifiesto de clúster de Hola debe establecer NTLMAuthenticationEnabled tootrue.</span><span class="sxs-lookup"><span data-stu-id="289f6-182">If an application requires that hello user account and password be same on all machines (for example, tooenable NTLM authentication), hello cluster manifest must set NTLMAuthenticationEnabled tootrue.</span></span> <span data-ttu-id="289f6-183">Hello manifiesto de clúster debe especificar una NTLMAuthenticationPasswordSecret que se usa toogenerate Hola la misma contraseña en todos los equipos.</span><span class="sxs-lookup"><span data-stu-id="289f6-183">hello cluster manifest must also specify an NTLMAuthenticationPasswordSecret that is used toogenerate hello same password across all machines.</span></span>

```xml
<Section Name="Hosting">
      <Parameter Name="EndpointProviderEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationPassworkSecret" Value="******" IsEncrypted="true"/>
 </Section>
```

### <a name="assign-policies-toohello-service-code-packages"></a><span data-ttu-id="289f6-184">Asignar directivas toohello paquetes de código de servicio</span><span class="sxs-lookup"><span data-stu-id="289f6-184">Assign policies toohello service code packages</span></span>
<span data-ttu-id="289f6-185">Hola **RunAsPolicy** sección un **ServiceManifestImport** especifica la cuenta de hello de sección de entidades de seguridad de Hola que debería ser toorun usa un paquete de código.</span><span class="sxs-lookup"><span data-stu-id="289f6-185">hello **RunAsPolicy** section for a **ServiceManifestImport** specifies hello account from hello principals section that should be used toorun a code package.</span></span> <span data-ttu-id="289f6-186">También asocia código manifiesto de paquetes de servicio de hello con cuentas de usuario en la sección de hello las entidades de seguridad.</span><span class="sxs-lookup"><span data-stu-id="289f6-186">It also associates code packages from hello service manifest with user accounts in hello principals section.</span></span> <span data-ttu-id="289f6-187">Esto puede especificarse para el programa de instalación de Hola o puntos de entrada principal, o puede especificar `All` tooapply lo tooboth.</span><span class="sxs-lookup"><span data-stu-id="289f6-187">You can specify this for hello setup or main entry points, or you can specify `All` tooapply it tooboth.</span></span> <span data-ttu-id="289f6-188">Hello en el ejemplo siguiente se muestra distintas directivas que se va a aplicar:</span><span class="sxs-lookup"><span data-stu-id="289f6-188">hello following example shows different policies being applied:</span></span>

```xml
<Policies>
<RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup"/>
<RunAsPolicy CodePackageRef="Code" UserRef="Customer3" EntryPointType="Main"/>
</Policies>
```

<span data-ttu-id="289f6-189">Si **EntryPointType** no se especifica, valor predeterminado de Hola se establece tooEntryPointType = "Main".</span><span class="sxs-lookup"><span data-stu-id="289f6-189">If **EntryPointType** is not specified, hello default is set tooEntryPointType=”Main”.</span></span> <span data-ttu-id="289f6-190">Especificar **SetupEntryPoint** es especialmente útil cuando desea toorun ciertas operaciones de instalación con privilegios elevados con una cuenta de sistema.</span><span class="sxs-lookup"><span data-stu-id="289f6-190">Specifying **SetupEntryPoint** is especially useful when you want toorun certain high-privilege setup operations under a system account.</span></span> <span data-ttu-id="289f6-191">código de servicio real de Hello puede ejecutar bajo una cuenta con menos privilegios.</span><span class="sxs-lookup"><span data-stu-id="289f6-191">hello actual service code can run under a lower-privilege account.</span></span>

### <a name="apply-a-default-policy-tooall-service-code-packages"></a><span data-ttu-id="289f6-192">Aplicar un paquetes de código predeterminada directiva tooall servicio</span><span class="sxs-lookup"><span data-stu-id="289f6-192">Apply a default policy tooall service code packages</span></span>
<span data-ttu-id="289f6-193">Usar hello **DefaultRunAsPolicy** sección toospecify una cuenta de usuario predeterminada para todos los paquetes de código que no tienen un determinado **RunAsPolicy** definido.</span><span class="sxs-lookup"><span data-stu-id="289f6-193">You use hello **DefaultRunAsPolicy** section toospecify a default user account for all code packages that don’t have a specific **RunAsPolicy** defined.</span></span> <span data-ttu-id="289f6-194">Si la mayoría de los paquetes de código de hello que se especifican en el manifiesto del servicio Hola utilizado por una aplicación necesita toorun en Hola mismo usuario, hello aplicación solo puede definir una directiva de ejecución predeterminada con esa cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="289f6-194">If most of hello code packages that are specified in hello service manifest used by an application need toorun under hello same user, hello application can just define a default RunAs policy with that user account.</span></span> <span data-ttu-id="289f6-195">Hello en el ejemplo siguiente se especifica que, si un paquete de código no tiene un **RunAsPolicy** especificado, debe ejecutar el paquete de código de hello en hello **MyDefaultAccount** especificado en la sección de hello las entidades de seguridad.</span><span class="sxs-lookup"><span data-stu-id="289f6-195">hello following example specifies that if a code package does not have a **RunAsPolicy** specified, hello code package should run under hello **MyDefaultAccount** specified in hello principals section.</span></span>

```xml
<Policies>
  <DefaultRunAsPolicy UserRef="MyDefaultAccount"/>
</Policies>
```
### <a name="use-an-active-directory-domain-group-or-user"></a><span data-ttu-id="289f6-196">Uso de un usuario o un grupo de dominios de Active Directory</span><span class="sxs-lookup"><span data-stu-id="289f6-196">Use an Active Directory domain group or user</span></span>
<span data-ttu-id="289f6-197">Para una instancia de Service Fabric que se instaló en Windows Server mediante el instalador independiente de hello, puede ejecutar Hola servicio con credenciales de Hola para una cuenta de usuario o grupo de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="289f6-197">For an instance of Service Fabric that was installed on Windows Server by using hello standalone installer, you can run hello service under hello credentials for an Active Directory user or group account.</span></span> <span data-ttu-id="289f6-198">Esto se aplica a Active Directory local dentro del dominio y no a Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="289f6-198">This is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="289f6-199">Mediante el uso de un grupo o usuario de dominio, a continuación, puede tener acceso a otros recursos de dominio de hello (por ejemplo, recursos compartidos de archivos) que se han concedido permisos.</span><span class="sxs-lookup"><span data-stu-id="289f6-199">By using a domain user or group, you can then access other resources in hello domain (for example, file shares) that have been granted permissions.</span></span>

<span data-ttu-id="289f6-200">Hello en el ejemplo siguiente se muestra un usuario de Active Directory denominado *Usuarioprueba* con su dominio llamado contraseña cifrada mediante un certificado *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="289f6-200">hello following example shows an Active Directory user called *TestUser* with their domain password encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="289f6-201">Puede usar hello `Invoke-ServiceFabricEncryptText` texto de cifrado secreto de Hola de toocreate de comandos de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="289f6-201">You can use hello `Invoke-ServiceFabricEncryptText` PowerShell command toocreate hello secret cipher text.</span></span> <span data-ttu-id="289f6-202">Vea [Administración de secretos en aplicaciones de Service Fabric](service-fabric-application-secret-management.md) | Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="289f6-202">See [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md) for details.</span></span>

<span data-ttu-id="289f6-203">Debe implementar la clave privada de hello del equipo local del toohello de contraseña de hello certificado toodecrypt hello mediante el uso de un método fuera de banda (en Azure, esto es a través del Administrador de recursos de Azure).</span><span class="sxs-lookup"><span data-stu-id="289f6-203">You must deploy hello private key of hello certificate toodecrypt hello password toohello local machine by using an out-of-band method (in Azure, this is via Azure Resource Manager).</span></span> <span data-ttu-id="289f6-204">A continuación, cuando Service Fabric implementa la máquina de toohello de paquete de servicio de hello, es capaz de toodecrypt Hola secreto y (junto con el nombre de usuario de Hola) se autentican con Active Directory toorun en esas credenciales.</span><span class="sxs-lookup"><span data-stu-id="289f6-204">Then, when Service Fabric deploys hello service package toohello machine, it is able toodecrypt hello secret and (along with hello user name) authenticate with Active Directory toorun under those credentials.</span></span>

```xml
<Principals>
  <Users>
    <User Name="TestUser" AccountType="DomainUser" AccountName="Domain\User" Password="[Put encrypted password here using MyCert certificate]" PasswordEncrypted="true" />
  </Users>
</Principals>
<Policies>
  <DefaultRunAsPolicy UserRef="TestUser" />
  <SecurityAccessPolicies>
    <SecurityAccessPolicy ResourceRef="MyCert" PrincipalRef="TestUser" GrantRights="Full" ResourceType="Certificate" />
  </SecurityAccessPolicies>
</Policies>
<Certificates>
```
### <a name="use-a-group-managed-service-account"></a><span data-ttu-id="289f6-205">Use una cuenta de servicio administrada de grupo.</span><span class="sxs-lookup"><span data-stu-id="289f6-205">Use a Group Managed Service Account.</span></span>
<span data-ttu-id="289f6-206">Para una instancia de Service Fabric que se instaló en Windows Server mediante el instalador independiente de hello, puede ejecutar el servicio de Hola como un grupo de cuentas de servicio administradas (gMSA).</span><span class="sxs-lookup"><span data-stu-id="289f6-206">For an instance of Service Fabric that was installed on Windows Server by using hello standalone installer, you can run hello service as a group Managed Service Account (gMSA).</span></span> <span data-ttu-id="289f6-207">Tenga en cuenta que esto se aplica a Active Directory local dentro del dominio y no para Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="289f6-207">Note that this is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="289f6-208">Mediante el uso de una gMSA hay ninguna contraseña o la contraseña cifrada que se almacenan en hello `Application Manifest`.</span><span class="sxs-lookup"><span data-stu-id="289f6-208">By using a gMSA there is no password or encrypted password stored in hello `Application Manifest`.</span></span>

<span data-ttu-id="289f6-209">Hello en el ejemplo siguiente se muestra cómo toocreate una cuenta de gMSA llama *svc prueba$*; el modo toodeploy que administran los nodos de clúster de toohello de cuenta de servicio; y cómo tooconfigure Hola principal de usuario.</span><span class="sxs-lookup"><span data-stu-id="289f6-209">hello following example shows how toocreate a gMSA account called *svc-Test$*; how toodeploy that managed service account toohello cluster nodes; and how tooconfigure hello user principal.</span></span>

##### <a name="prerequisites"></a><span data-ttu-id="289f6-210">Requisitos previos.</span><span class="sxs-lookup"><span data-stu-id="289f6-210">Prerequisites.</span></span>
- <span data-ttu-id="289f6-211">dominio de Hello necesita una clave de raíz KDS.</span><span class="sxs-lookup"><span data-stu-id="289f6-211">hello domain needs a KDS root key.</span></span>
- <span data-ttu-id="289f6-212">dominio de Hello debe toobe en un nivel funcional de versiones posteriores o Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="289f6-212">hello domain needs toobe at a Windows Server 2012 or later functional level.</span></span>

##### <a name="example"></a><span data-ttu-id="289f6-213">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="289f6-213">Example</span></span>
1. <span data-ttu-id="289f6-214">Tiene un administrador de dominio de active directory crear una cuenta de servicio administradas de grupo con hello `New-ADServiceAccount` commandlet y asegúrese de que hello `PrincipalsAllowedToRetrieveManagedPassword` incluye todos Hola service fabric nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="289f6-214">Have an active directory domain administrator create a group managed service account using hello `New-ADServiceAccount` commandlet and ensure that hello `PrincipalsAllowedToRetrieveManagedPassword` includes all of hello service fabric cluster nodes.</span></span> <span data-ttu-id="289f6-215">Tenga en cuenta que `AccountName`, `DnsHostName` y `ServicePrincipalName` deben ser únicos.</span><span class="sxs-lookup"><span data-stu-id="289f6-215">Note that `AccountName`, `DnsHostName`, and `ServicePrincipalName` must be unique.</span></span>
```
New-ADServiceAccount -name svc-Test$ -DnsHostName svc-test.contoso.com  -ServicePrincipalNames http/svc-test.contoso.com -PrincipalsAllowedToRetrieveManagedPassword SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$
```
2. <span data-ttu-id="289f6-216">En cada uno de los nodos del clúster de tejido de hello servicio (por ejemplo, `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`), instalar y probar hello gMSA.</span><span class="sxs-lookup"><span data-stu-id="289f6-216">On each of hello service fabric cluster nodes (for example, `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`), install and test hello gMSA.</span></span>
```
Add-WindowsFeature RSAT-AD-PowerShell
Install-AdServiceAccount svc-Test$
Test-AdServiceAccount svc-Test$
```
3. <span data-ttu-id="289f6-217">Configurar la entidad de seguridad de usuario de Hola y configurar hello RunAsPolicy tooreference Hola usuario.</span><span class="sxs-lookup"><span data-stu-id="289f6-217">Configure hello User principal, and configure hello RunAsPolicy tooreference hello user.</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="DomaingMSA"/>
      </Policies>
   </ServiceManifestImport>
  <Principals>
    <Users>
      <User Name="DomaingMSA" AccountType="ManagedServiceAccount" AccountName="domain\svc-Test$"/>
    </Users>
  </Principals>
</ApplicationManifest>
```

## <a name="assign-a-security-access-policy-for-http-and-https-endpoints"></a><span data-ttu-id="289f6-218">Asignación de una directiva de acceso de seguridad a los puntos de conexión HTTP y HTTPS</span><span class="sxs-lookup"><span data-stu-id="289f6-218">Assign a security access policy for HTTP and HTTPS endpoints</span></span>
<span data-ttu-id="289f6-219">Si aplica un servicio de tooa de directiva de ejecución y manifiesto de servicio de hello declara los recursos de punto de conexión con protocolo de hello HTTP, debe especificar un **SecurityAccessPolicy** tooensure que los puertos asignan extremos toothese están correctamente control de acceso incluyen hello cuenta de usuario de ejecución que se ejecuta el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="289f6-219">If you apply a RunAs policy tooa service and hello service manifest declares endpoint resources with hello HTTP protocol, you must specify a **SecurityAccessPolicy** tooensure that ports allocated toothese endpoints are correctly access-control listed for hello RunAs user account that hello service runs under.</span></span> <span data-ttu-id="289f6-220">En caso contrario, **http.sys** no tienen acceso toohello servicio y obtener errores con llamadas de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="289f6-220">Otherwise, **http.sys** does not have access toohello service, and you get failures with calls from hello client.</span></span> <span data-ttu-id="289f6-221">Hello en el ejemplo siguiente se aplica hello Customer1 cuenta tooan punto de conexión llamado **EndpointName**, que proporciona derechos de acceso completo.</span><span class="sxs-lookup"><span data-stu-id="289f6-221">hello following example applies hello Customer1 account tooan endpoint called **EndpointName**, which gives it full access rights.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
   <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
</Policies>
```

<span data-ttu-id="289f6-222">Para el extremo HTTPS de hello, también tiene tooindicate Hola nombre de hello certificado tooreturn toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="289f6-222">For hello HTTPS endpoint, you also have tooindicate hello name of hello certificate tooreturn toohello client.</span></span> <span data-ttu-id="289f6-223">Puede hacerlo mediante el uso de **EndpointBindingPolicy**, con certificado Hola definida en una sección de certificados en el manifiesto de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="289f6-223">You can do this by using **EndpointBindingPolicy**, with hello certificate defined in a certificates section in hello application manifest.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
  <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
  <!--EndpointBindingPolicy is needed if hello EndpointName is secured with https -->
  <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
</Policies
```
## <a name="upgrading-multiple-applications-with-https-endpoints"></a><span data-ttu-id="289f6-224">Actualización de varias aplicaciones con puntos de conexión https</span><span class="sxs-lookup"><span data-stu-id="289f6-224">Upgrading multiple applications with https endpoints</span></span>
<span data-ttu-id="289f6-225">Necesita toobe cuidado de no toouse hello **mismo puerto** para distintas instancias de hello misma aplicación cuando se utiliza http**s**.</span><span class="sxs-lookup"><span data-stu-id="289f6-225">You need toobe careful not toouse hello **same port** for different instances of hello same application when using http**s**.</span></span> <span data-ttu-id="289f6-226">motivo de Hello es que Service Fabric no sea cert, Hola tooupgrade pueda por una de las instancias de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="289f6-226">hello reason is that Service Fabric won't be able tooupgrade hello cert for one of hello application instances.</span></span> <span data-ttu-id="289f6-227">Por ejemplo, si desea que la aplicación 1 o de la aplicación 2 ambos tooupgrade su toocert cert 1 2.</span><span class="sxs-lookup"><span data-stu-id="289f6-227">For example, if application 1 or application 2 both want tooupgrade their cert 1 toocert 2.</span></span> <span data-ttu-id="289f6-228">Cuando se produzca la actualización de hello, Service Fabric que podría limpiado registro de certificado 1 Hola con http.sys aunque hello otra aplicación está seguir utilizándolo.</span><span class="sxs-lookup"><span data-stu-id="289f6-228">When hello upgrade happens, Service Fabric might have cleaned up hello cert 1 registration with http.sys even though hello other application is still using it.</span></span> <span data-ttu-id="289f6-229">tooprevent, Service Fabric detecta que ya hay otra instancia de la aplicación registrada en el puerto de hello con certificado de Hola (due toohttp.sys) y se produce un error Hola operación.</span><span class="sxs-lookup"><span data-stu-id="289f6-229">tooprevent this, Service Fabric detects that there is already another application instance registered on hello port with hello certificate (due toohttp.sys) and fails hello operation.</span></span>

<span data-ttu-id="289f6-230">Por lo tanto, Service Fabric no admite la actualización de dos servicios diferentes mediante **Hola mismo puerto** en instancias de aplicación diferente.</span><span class="sxs-lookup"><span data-stu-id="289f6-230">Hence Service Fabric does not support upgrading two different services using **hello same port** in different application instances.</span></span> <span data-ttu-id="289f6-231">En otras palabras, no puede usar Hola mismo certificado en diferentes servicios en hello mismo puerto.</span><span class="sxs-lookup"><span data-stu-id="289f6-231">In other words, you cannot use hello same certificate on different services on hello same port.</span></span> <span data-ttu-id="289f6-232">Si necesita toohave un certificado en hello mismo puerto, deberá tooensure ese Hola servicios se colocan en distintos equipos con las restricciones de posición.</span><span class="sxs-lookup"><span data-stu-id="289f6-232">If you need toohave a shared certificate on hello same port, you need tooensure that hello services are placed on different machines with placement constraints.</span></span> <span data-ttu-id="289f6-233">También puede considerar la posibilidad de utilizar puertos dinámicos de Service Fabric para cada servicio en cada instancia de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="289f6-233">Or consider using Service Fabric dynamic ports if possible for each service in each application instance.</span></span> 

<span data-ttu-id="289f6-234">Si ve un error de actualización con https, una advertencia de error que dice "hello Windows HTTP Server API no admite varios certificados para las aplicaciones que compartan un puerto."</span><span class="sxs-lookup"><span data-stu-id="289f6-234">If you see an upgrade fail with https, an error warning saying "hello Windows HTTP Server API does not support multiple certificates for applications that share a port.”</span></span>

## <a name="a-complete-application-manifest-example"></a><span data-ttu-id="289f6-235">Ejemplo completo de un manifiesto de aplicación</span><span class="sxs-lookup"><span data-stu-id="289f6-235">A complete application manifest example</span></span>
<span data-ttu-id="289f6-236">Hola siguiendo el manifiesto de aplicación muestra muchos de hello valores distintos:</span><span class="sxs-lookup"><span data-stu-id="289f6-236">hello following application manifest shows many of hello different settings:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="Application3Type" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Parameters>
      <Parameter Name="Stateless1_InstanceCount" DefaultValue="-1" />
   </Parameters>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="Stateless1Pkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
         <RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup" />
        <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
         <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
        <!--EndpointBindingPolicy is needed hello EndpointName is secured with https -->
        <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
     </Policies>
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="Stateless1">
         <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
            <SingletonPartition />
         </StatelessService>
      </Service>
   </DefaultServices>
   <Principals>
      <Groups>
         <Group Name="LocalAdminGroup">
            <Membership>
               <SystemGroup Name="Administrators" />
            </Membership>
         </Group>
      </Groups>
      <Users>
         <User Name="LocalAdmin">
            <MemberOf>
               <Group NameRef="LocalAdminGroup" />
            </MemberOf>
         </User>
         <!--Customer1 below create a local account that this service runs under -->
         <User Name="Customer1" />
         <User Name="MyDefaultAccount" AccountType="NetworkService" />
      </Users>
   </Principals>
   <Policies>
      <DefaultRunAsPolicy UserRef="LocalAdmin" />
   </Policies>
   <Certificates>
     <EndpointCertificate Name="Cert1" X509FindValue="FF EE E0 TT JJ DD JJ EE EE XX 23 4T 66 "/>
  </Certificates>
</ApplicationManifest>
```


<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="289f6-237">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="289f6-237">Next steps</span></span>
* [<span data-ttu-id="289f6-238">Entender el modelo de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="289f6-238">Understand hello application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="289f6-239">Especificación de los recursos en un manifiesto de servicio</span><span class="sxs-lookup"><span data-stu-id="289f6-239">Specify resources in a service manifest</span></span>](service-fabric-service-manifest-resources.md)
* [<span data-ttu-id="289f6-240">Implementar una aplicación</span><span class="sxs-lookup"><span data-stu-id="289f6-240">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[image1]: ./media/service-fabric-application-runas-security/copy-to-output.png
