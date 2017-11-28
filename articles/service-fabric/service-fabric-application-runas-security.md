---
title: "Información acerca de las directivas de seguridad de los microservicios de Azure | Microsoft Docs"
description: "Información general sobre cómo ejecutar una aplicación de Service Fabric en cuentas de seguridad locales y del sistema, incluido el punto SetupEntry en el que una aplicación necesita realizar alguna acción con privilegios antes de iniciarse"
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
ms.openlocfilehash: e673b45a43a06d18040c3437caf8765704d5c36a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-security-policies-for-your-application"></a><span data-ttu-id="3c4e3-103">Configuración de directivas de seguridad para la aplicación</span><span class="sxs-lookup"><span data-stu-id="3c4e3-103">Configure security policies for your application</span></span>
<span data-ttu-id="3c4e3-104">Azure Service Fabric le permite proteger aplicaciones que se ejecutan en distintas cuentas de usuario en el clúster.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-104">By using Azure Service Fabric, you can secure applications that are running in the cluster under different user accounts.</span></span> <span data-ttu-id="3c4e3-105">Service Fabric también protege los recursos que usan las aplicaciones en el momento de la implementación con la cuenta de usuario; por ejemplo, archivos, directorios y certificados.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-105">Service Fabric also helps secure the resources that are used by applications at the time of deployment under the user accounts--for example, files, directories, and certificates.</span></span> <span data-ttu-id="3c4e3-106">Esto aumenta la seguridad entre aplicaciones en ejecución, incluso en un entorno hospedado compartido.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-106">This makes running applications, even in a shared hosted environment, more secure from one another.</span></span>

<span data-ttu-id="3c4e3-107">De forma predeterminada, las aplicaciones de Service Fabric se ejecutan en la misma cuenta en que se ejecuta el proceso Fabric.exe.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-107">By default, Service Fabric applications run under the account that the Fabric.exe process runs under.</span></span> <span data-ttu-id="3c4e3-108">Service Fabric también permite ejecutar aplicaciones en una cuenta de usuario local o una cuenta de sistema local especificada en el manifiesto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-108">Service Fabric also provides the capability to run applications under a local user account or local system account, which is specified within the application manifest.</span></span> <span data-ttu-id="3c4e3-109">Los tipos de cuenta de sistema local compatibles son **LocalUser**, **NetworkService**, **LocalService** y **LocalSystem**.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-109">Supported local system account types are **LocalUser**, **NetworkService**, **LocalService**, and **LocalSystem**.</span></span>

 <span data-ttu-id="3c4e3-110">Cuando ejecute Service Fabric en Windows Server en el centro de datos mediante el instalador independiente, puede usar cuentas de dominio de Active Directory, incluidas cuentas de servicio administradas de grupo.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-110">When you're running Service Fabric on Windows Server in your datacenter by using the standalone installer, you can use Active Directory domain accounts, including group managed service accounts.</span></span>

<span data-ttu-id="3c4e3-111">Se pueden definir y crear grupos de usuarios, de modo que se puedan agregar uno o varios usuarios a cada grupo para poder administrarlos de forma conjunta.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-111">You can define and create user groups so that one or more users can be added to each group to be managed together.</span></span> <span data-ttu-id="3c4e3-112">Esto es útil cuando hay varios usuarios para distintos puntos de entrada de servicio y es preciso que tengan ciertos privilegios comunes disponibles en el nivel de grupo.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-112">This is useful when there are multiple users for different service entry points and they need to have certain common privileges that are available at the group level.</span></span>

## <a name="configure-the-policy-for-a-service-setup-entry-point"></a><span data-ttu-id="3c4e3-113">Configuración de la directiva para un punto de entrada del programa de instalación del servicio</span><span class="sxs-lookup"><span data-stu-id="3c4e3-113">Configure the policy for a service setup entry point</span></span>
<span data-ttu-id="3c4e3-114">Tal como se describe en el [modelo de aplicación](service-fabric-application-model.md), el punto de entrada del programa de instalación, **SetupEntryPoint**, es un punto de entrada con privilegios que se ejecuta con las mismas credenciales que Service Fabric (normalmente, la cuenta *NetworkService*) antes que cualquier otro punto de entrada.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-114">As described in the [application model](service-fabric-application-model.md), the setup entry point, **SetupEntryPoint**, is a privileged entry point that runs with the same credentials as Service Fabric (typically the *NetworkService* account) before any other entry point.</span></span> <span data-ttu-id="3c4e3-115">El archivo ejecutable que se especifica con **EntryPoint** suele ser el host de servicio de ejecución prolongada.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-115">The executable that is specified by **EntryPoint** is typically the long-running service host.</span></span> <span data-ttu-id="3c4e3-116">Por lo que tener un punto de entrada de configuración independiente evita tener que ejecutar el ejecutable del host de servicio con privilegios elevados durante largos períodos de tiempo.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-116">So having a separate setup entry point avoids having to run the service host executable with high privileges for extended periods of time.</span></span> <span data-ttu-id="3c4e3-117">El archivo ejecutable especificado por **EntryPoint** se ejecuta después de salir de **SetupEntryPoint** correctamente.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-117">The executable that **EntryPoint** specifies is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="3c4e3-118">El proceso resultante se supervisa y reinicia, comenzando de nuevo con **SetupEntryPoint**si alguna vez finaliza o se bloquea.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-118">The resulting process is monitored and restarted, and begins again with **SetupEntryPoint** if it ever terminates or crashes.</span></span>

<span data-ttu-id="3c4e3-119">A continuación aparece un ejemplo de manifiesto de servicio básico que muestra SetupEntryPoint y el EntryPoint principal del servicio.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-119">The following is a simple service manifest example that shows the SetupEntryPoint and the main EntryPoint for the service.</span></span>

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

### <a name="configure-the-policy-by-using-a-local-account"></a><span data-ttu-id="3c4e3-120">Configuración de la directiva mediante una cuenta local</span><span class="sxs-lookup"><span data-stu-id="3c4e3-120">Configure the policy by using a local account</span></span>
<span data-ttu-id="3c4e3-121">Tras configurar el servicio para que tenga un punto de entrada de configuración, puede cambiar los permisos de seguridad que ejecuta en el manifiesto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-121">After you configure the service to have a setup entry point, you can change the security permissions that it runs under in the application manifest.</span></span> <span data-ttu-id="3c4e3-122">En el ejemplo siguiente se muestra cómo configurar el servicio para que se ejecute con privilegios de cuenta de administrador de usuarios.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-122">The following example shows how to configure the service to run under user administrator account privileges.</span></span>

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

<span data-ttu-id="3c4e3-123">En primer lugar, cree una sección **Principals** con un nombre de usuario, como SetupAdminUser.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-123">First, create a **Principals** section with a user name, such as SetupAdminUser.</span></span> <span data-ttu-id="3c4e3-124">Esto indica que el usuario es miembro del grupo de administradores del sistema.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-124">This indicates that the user is a member of the Administrators system group.</span></span>

<span data-ttu-id="3c4e3-125">Después, debajo de la sección **ServiceManifestImport**, configure una directiva para aplicar esta entidad de seguridad a **SetupEntryPoint**.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-125">Next, under the **ServiceManifestImport** section, configure a policy to apply this principal to **SetupEntryPoint**.</span></span> <span data-ttu-id="3c4e3-126">Esto indica a Service Fabric que, cuando el archivo **MySetup.bat** se ejecute, debería ser `RunAs` con privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-126">This tells Service Fabric that when the **MySetup.bat** file is run, it should be `RunAs` with administrator privileges.</span></span> <span data-ttu-id="3c4e3-127">Dado que *no* ha aplicado una directiva al punto de entrada principal, el código de **MyServiceHost.exe** se ejecuta en la cuenta **NetworkService** del sistema.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-127">Given that you have *not* applied a policy to the main entry point, the code in **MyServiceHost.exe** runs under the system **NetworkService** account.</span></span> <span data-ttu-id="3c4e3-128">Esta es la cuenta predeterminada como la que se ejecutan todos los puntos de entrada de servicio.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-128">This is the default account that all service entry points are run as.</span></span>

<span data-ttu-id="3c4e3-129">Ahora agreguemos el archivo MySetup.bat al proyecto de Visual Studio para probar los privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-129">Let's now add the file MySetup.bat to the Visual Studio project to test the administrator privileges.</span></span> <span data-ttu-id="3c4e3-130">En Visual Studio, haga clic con el botón derecho en el proyecto de servicio y agregue un nuevo archivo, MySetup.bat.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-130">In Visual Studio, right-click the service project and add a new file called MySetup.bat.</span></span>

<span data-ttu-id="3c4e3-131">Después asegúrese de que el archivo MySetup.bat está incluido en el paquete de servicio.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-131">Next, ensure that the MySetup.bat file is included in the service package.</span></span> <span data-ttu-id="3c4e3-132">De forma predeterminada, no lo está.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-132">By default, it is not.</span></span> <span data-ttu-id="3c4e3-133">Seleccione el archivo, haga clic con el botón derecho para ver el menú contextual y elija **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-133">Select the file, right-click to get the context menu, and choose **Properties**.</span></span> <span data-ttu-id="3c4e3-134">En el cuadro de diálogo de propiedades, asegúrese de que **Copiar en el directorio de salida** está establecido en **Copiar si es posterior**.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-134">In the Properties dialog box, ensure that **Copy to Output Directory** is set to **Copy if newer**.</span></span> <span data-ttu-id="3c4e3-135">Vea la siguiente captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-135">See the following screenshot.</span></span>

![CopyToOutput de Visual Studio para el archivo por lotes de SetupEntryPoint][image1]

<span data-ttu-id="3c4e3-137">Ahora abra el archivo MySetup.bat y agregue los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="3c4e3-137">Now open the MySetup.bat file and add the following commands:</span></span>

```
REM Set a system environment variable. This requires administrator privilege
setx -m TestVariable "MyValue"
echo System TestVariable set to > out.txt
echo %TestVariable% >> out.txt

REM To delete this system variable us
REM REG delete "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment" /v TestVariable /f
```

<span data-ttu-id="3c4e3-138">Seguidamente, compile e implemente la solución en un clúster de desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-138">Next, build and deploy the solution to a local development cluster.</span></span> <span data-ttu-id="3c4e3-139">Una vez iniciado el servicio, tal como se muestra en Service Fabric Explorer, hay dos maneras de ver que MySetup.bat se ha ejecutado correctamente.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-139">After the service has started, as shown in Service Fabric Explorer, you can see that the MySetup.bat file was successful in a two ways.</span></span> <span data-ttu-id="3c4e3-140">Abra un símbolo del sistema de PowerShell y escriba:</span><span class="sxs-lookup"><span data-stu-id="3c4e3-140">Open a PowerShell command prompt and type:</span></span>

```
PS C:\ [Environment]::GetEnvironmentVariable("TestVariable","Machine")
MyValue
```

<span data-ttu-id="3c4e3-141">Anote el nombre del nodo donde el servicio se ha implementado e iniciado en Service Fabric Explorer, por ejemplo, Node 2.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-141">Then, note the name of the node where the service was deployed and started in Service Fabric Explorer--for example, Node 2.</span></span> <span data-ttu-id="3c4e3-142">Después, navegue hasta la carpeta de trabajo de la instancia de aplicación para buscar el archivo out.txt que muestra el valor de **TestVariable**.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-142">Next, navigate to the application instance work folder to find the out.txt file that shows the value of **TestVariable**.</span></span> <span data-ttu-id="3c4e3-143">Por ejemplo, si este servicio se implementó en Node 2, puede ir a esta ruta de acceso para ver el valor de **MyApplicationType**:</span><span class="sxs-lookup"><span data-stu-id="3c4e3-143">For example, if this service was deployed to Node 2, then you can go to this path for the **MyApplicationType**:</span></span>

```
C:\SfDevCluster\Data\_App\Node.2\MyApplicationType_App\work\out.txt
```

### <a name="configure-the-policy-by-using-local-system-accounts"></a><span data-ttu-id="3c4e3-144">Configuración de la directiva mediante cuentas de sistema locales</span><span class="sxs-lookup"><span data-stu-id="3c4e3-144">Configure the policy by using local system accounts</span></span>
<span data-ttu-id="3c4e3-145">A menudo es preferible ejecutar el script de inicio mediante una cuenta de sistema local en lugar de usar una cuenta de administrador.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-145">Often, it's preferable to run the startup script by using a local system account rather than an administrator account.</span></span> <span data-ttu-id="3c4e3-146">Normalmente, el hecho de ejecutar la directiva RunAs como miembro del grupo Administradores no funciona bien, ya que las máquinas tienen el Control de acceso de usuario (UAC) habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-146">Running the RunAs policy as a member of the Administrators group typically doesn’t work well because machines have User Access Control (UAC) enabled by default.</span></span> <span data-ttu-id="3c4e3-147">En estos casos, **la recomendación es ejecutar el SetupEntryPoint como LocalSystem y no como un usuario local agregado al grupo de administradores**.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-147">In such cases, **the recommendation is to run the SetupEntryPoint as LocalSystem, instead of as a local user added to Administrators group**.</span></span> <span data-ttu-id="3c4e3-148">En el ejemplo siguiente se muestra cómo establecer SetupEntryPoint para que se ejecute como LocalSystem:</span><span class="sxs-lookup"><span data-stu-id="3c4e3-148">The following example shows setting the SetupEntryPoint to run as LocalSystem:</span></span>

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

## <a name="start-powershell-commands-from-a-setup-entry-point"></a><span data-ttu-id="3c4e3-149">Inicio de comandos de PowerShell desde un SetupEntryPoint</span><span class="sxs-lookup"><span data-stu-id="3c4e3-149">Start PowerShell commands from a setup entry point</span></span>
<span data-ttu-id="3c4e3-150">Para ejecutar PowerShell desde el punto **SetupEntryPoint**, puede ejecutar **PowerShell.exe** en un archivo por lotes que apunte al archivo de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-150">To run PowerShell from the **SetupEntryPoint** point, you can run **PowerShell.exe** in a batch file that points to a PowerShell file.</span></span> <span data-ttu-id="3c4e3-151">En primer lugar, agregue un archivo de PowerShell al proyecto de servicio, por ejemplo, **MySetup.ps1**.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-151">First, add a PowerShell file to the service project--for example, **MySetup.ps1**.</span></span> <span data-ttu-id="3c4e3-152">No olvide configurar la propiedad *Copiar si es posterior* para que el archivo se incluya también en el paquete de servicio.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-152">Remember to set the *Copy if newer* property so that the file is also included in the service package.</span></span> <span data-ttu-id="3c4e3-153">En el ejemplo siguiente se muestra un archivo por lotes de ejemplo que inicia un archivo de PowerShell denominado MySetup.ps1, que establece una variable de entorno del sistema denominada **TestVariable**.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-153">The following example shows a sample batch file that starts a PowerShell file called MySetup.ps1, which sets a system environment variable called **TestVariable**.</span></span>

<span data-ttu-id="3c4e3-154">MySetup.bat para iniciar un archivo de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3c4e3-154">MySetup.bat to start a PowerShell file:</span></span>

```
powershell.exe -ExecutionPolicy Bypass -Command ".\MySetup.ps1"
```

<span data-ttu-id="3c4e3-155">En el archivo de PowerShell, agregue el siguiente procedimiento para establecer una variable de entorno del sistema.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-155">In the PowerShell file, add the following to set a system environment variable:</span></span>

```
[Environment]::SetEnvironmentVariable("TestVariable", "MyValue", "Machine")
[Environment]::GetEnvironmentVariable("TestVariable","Machine") > out.txt
```

> [!NOTE]
> <span data-ttu-id="3c4e3-156">De forma predeterminada, cuando se ejecuta el archivo por lotes, la búsqueda de archivos se realiza en la carpeta de aplicación denominada **work**.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-156">By default, when the batch file runs, it looks at the application folder called **work** for files.</span></span> <span data-ttu-id="3c4e3-157">En este caso, cuando se ejecuta MySetup.bat queremos que encuentre el archivo MySetup.ps1 en la misma carpeta, que es la carpeta **paquete de código** de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-157">In this case, when MySetup.bat runs, we want this to find the MySetup.ps1 file in the same folder, which is the application **code package** folder.</span></span> <span data-ttu-id="3c4e3-158">Para cambiar esta carpeta, configure la carpeta de trabajo:</span><span class="sxs-lookup"><span data-stu-id="3c4e3-158">To change this folder, set the working folder:</span></span>
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

## <a name="use-console-redirection-for-local-debugging"></a><span data-ttu-id="3c4e3-159">Uso de la redirección de la consola para la depuración local</span><span class="sxs-lookup"><span data-stu-id="3c4e3-159">Use console redirection for local debugging</span></span>
<span data-ttu-id="3c4e3-160">En ocasiones, resulta útil ver el resultado de la consola tras ejecutar un script con fines de depuración.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-160">Occasionally, it's useful to see the console output from running a script for debugging purposes.</span></span> <span data-ttu-id="3c4e3-161">Para ello, puede establecer una directiva de redirección de la consola que escriba la salida en un archivo.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-161">To do this, you can set a console redirection policy, which writes the output to a file.</span></span> <span data-ttu-id="3c4e3-162">La salida del archivo se escribe en la carpeta de aplicación denominada **log** en el nodo donde se ha implementado y ejecutado la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-162">The file output is written to the application folder called **log** on the node where the application is deployed and run.</span></span> <span data-ttu-id="3c4e3-163">(Vea dónde encontrar esto en el ejemplo anterior).</span><span class="sxs-lookup"><span data-stu-id="3c4e3-163">(See where to find this in the preceding example.)</span></span>

> [!WARNING]
> <span data-ttu-id="3c4e3-164">No use nunca la directiva de redirección de la consola en una aplicación implementada en producción, ya que esto puede afectar a la capacidad de conmutación por error de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-164">Never use the console redirection policy in an application that is deployed in production because this can affect the application failover.</span></span> <span data-ttu-id="3c4e3-165">*Solo* debe usarla con fines de depuración y desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-165">*Only* use this for local development and debugging purposes.</span></span>  
> 
> 

<span data-ttu-id="3c4e3-166">En el ejemplo siguiente, se muestra cómo establecer la redirección de la consola con un valor de FileRetentionCount:</span><span class="sxs-lookup"><span data-stu-id="3c4e3-166">The following example shows setting the console redirection with a FileRetentionCount value:</span></span>

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="10"/>
    </ExeHost>
</SetupEntryPoint>
```

<span data-ttu-id="3c4e3-167">Si cambia el archivo MySetup.ps1 para escribir un comando **Echo**, este se escribirá en el archivo de salida con fines de depuración:</span><span class="sxs-lookup"><span data-stu-id="3c4e3-167">If you now change the MySetup.ps1 file to write an **Echo** command, this will write to the output file for debugging purposes:</span></span>

```
Echo "Test console redirection which writes to the application log folder on the node that the application is deployed to"
```

<span data-ttu-id="3c4e3-168">**Después de haber depurado el script, quite inmediatamente esta directiva de redireccionamiento de consola**.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-168">**After you debug your script, immediately remove this console redirection policy**.</span></span>

## <a name="configure-a-policy-for-service-code-packages"></a><span data-ttu-id="3c4e3-169">Configuración de una directiva para los paquetes de código del servicio</span><span class="sxs-lookup"><span data-stu-id="3c4e3-169">Configure a policy for service code packages</span></span>
<span data-ttu-id="3c4e3-170">En los pasos anteriores se explicaba cómo aplicar la directiva RunAs a SetupEntryPoint.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-170">In the preceding steps, you saw how to apply a RunAs policy to SetupEntryPoint.</span></span> <span data-ttu-id="3c4e3-171">Ahora se explicará más detalladamente cómo crear diferentes entidades de seguridad que se pueden aplicar como directivas de servicio.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-171">Let's look a little deeper into how to create different principals that can be applied as service policies.</span></span>

### <a name="create-local-user-groups"></a><span data-ttu-id="3c4e3-172">Creación de grupos de usuarios locales</span><span class="sxs-lookup"><span data-stu-id="3c4e3-172">Create local user groups</span></span>
<span data-ttu-id="3c4e3-173">Se pueden definir y crear grupos de usuarios que permitan agregar uno o varios usuarios a un grupo.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-173">You can define and create user groups that allow one or more users to be added to a group.</span></span> <span data-ttu-id="3c4e3-174">Esto es útil si hay varios usuarios para distintos puntos de entrada de servicio y es preciso que tengan ciertos privilegios comunes disponibles en el nivel de grupo.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-174">This is useful if there are multiple users for different service entry points and they need to have certain common privileges that are available at the group level.</span></span> <span data-ttu-id="3c4e3-175">En el ejemplo siguiente se muestra un grupo local denominado **LocalAdminGroup** con privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-175">The following example shows a local group called **LocalAdminGroup** that has administrator privileges.</span></span> <span data-ttu-id="3c4e3-176">Dos usuarios, Customer1 y Customer2, se convierten en miembros de este grupo local.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-176">Two users, Customer1 and Customer2, are made members of this local group.</span></span>

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

### <a name="create-local-users"></a><span data-ttu-id="3c4e3-177">Creación de usuarios locales</span><span class="sxs-lookup"><span data-stu-id="3c4e3-177">Create local users</span></span>
<span data-ttu-id="3c4e3-178">Puede crear un usuario local para proteger un servicio dentro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-178">You can create a local user that can be used to help secure a service within the application.</span></span> <span data-ttu-id="3c4e3-179">Si se especifica un tipo de cuenta **LocalUser** en la sección de entidades de seguridad del manifiesto de aplicación, Service Fabric crea cuentas de usuario locales en las máquinas donde se implementa la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-179">When a **LocalUser** account type is specified in the principals section of the application manifest, Service Fabric creates local user accounts on machines where the application is deployed.</span></span> <span data-ttu-id="3c4e3-180">De forma predeterminada, los nombres de dichas cuentas no coinciden con los que se especifican en el manifiesto de aplicación (por ejemplo, Customer3 en el ejemplo siguiente).</span><span class="sxs-lookup"><span data-stu-id="3c4e3-180">By default, these accounts do not have the same names as those specified in the application manifest (for example, Customer3 in the following sample).</span></span> <span data-ttu-id="3c4e3-181">En su lugar, se generan dinámicamente y tienen contraseñas aleatorias.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-181">Instead, they are dynamically generated and have random passwords.</span></span>

```xml
<Principals>
  <Users>
     <User Name="Customer3" AccountType="LocalUser" />
  </Users>
</Principals>
```

<span data-ttu-id="3c4e3-182">Si una aplicación requiere que la cuenta de usuario y la contraseña coincidan en todas las máquinas (por ejemplo, para habilitar la autenticación NTLM), el manifiesto de clúster debe establecer NTLMAuthenticationEnabled en true.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-182">If an application requires that the user account and password be same on all machines (for example, to enable NTLM authentication), the cluster manifest must set NTLMAuthenticationEnabled to true.</span></span> <span data-ttu-id="3c4e3-183">El manifiesto de clúster también debe especificar un NTLMAuthenticationPasswordSecret que se use para generar la misma contraseña en todos los equipos.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-183">The cluster manifest must also specify an NTLMAuthenticationPasswordSecret that is used to generate the same password across all machines.</span></span>

```xml
<Section Name="Hosting">
      <Parameter Name="EndpointProviderEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationPassworkSecret" Value="******" IsEncrypted="true"/>
 </Section>
```

### <a name="assign-policies-to-the-service-code-packages"></a><span data-ttu-id="3c4e3-184">Asignación de directivas a los paquetes de código de servicio</span><span class="sxs-lookup"><span data-stu-id="3c4e3-184">Assign policies to the service code packages</span></span>
<span data-ttu-id="3c4e3-185">En la sección **RunAsPolicy** de **ServiceManifestImport**, se especifica la cuenta de la sección de entidades de seguridad que debe usarse para ejecutar un paquete de código.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-185">The **RunAsPolicy** section for a **ServiceManifestImport** specifies the account from the principals section that should be used to run a code package.</span></span> <span data-ttu-id="3c4e3-186">También se asocian los paquetes de código del manifiesto de servicio con las cuentas de usuario de la sección de entidades de seguridad.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-186">It also associates code packages from the service manifest with user accounts in the principals section.</span></span> <span data-ttu-id="3c4e3-187">Puede especificarlo para los puntos de entrada de configuración o principales, o bien puede especificar `All` para que se aplique a ambos.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-187">You can specify this for the setup or main entry points, or you can specify `All` to apply it to both.</span></span> <span data-ttu-id="3c4e3-188">En el ejemplo siguiente se muestra la aplicación de diferentes directivas:</span><span class="sxs-lookup"><span data-stu-id="3c4e3-188">The following example shows different policies being applied:</span></span>

```xml
<Policies>
<RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup"/>
<RunAsPolicy CodePackageRef="Code" UserRef="Customer3" EntryPointType="Main"/>
</Policies>
```

<span data-ttu-id="3c4e3-189">Si no se especifica **EntryPointType** , el valor predeterminado se establece en EntryPointType =”Main”.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-189">If **EntryPointType** is not specified, the default is set to EntryPointType=”Main”.</span></span> <span data-ttu-id="3c4e3-190">El uso de **SetupEntryPoint** es especialmente útil si lo que se desea es ejecutar determinadas operaciones de instalación con privilegios elevados en una cuenta de sistema.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-190">Specifying **SetupEntryPoint** is especially useful when you want to run certain high-privilege setup operations under a system account.</span></span> <span data-ttu-id="3c4e3-191">El código de servicio real puede ejecutarse en una cuenta con menos privilegios.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-191">The actual service code can run under a lower-privilege account.</span></span>

### <a name="apply-a-default-policy-to-all-service-code-packages"></a><span data-ttu-id="3c4e3-192">Aplicación de una directiva predeterminada a todos los paquetes de código de servicio</span><span class="sxs-lookup"><span data-stu-id="3c4e3-192">Apply a default policy to all service code packages</span></span>
<span data-ttu-id="3c4e3-193">La sección **DefaultRunAsPolicy** se usa para especificar una cuenta de usuario predeterminada para todos los paquetes de código que no tienen definido ningún parámetro **RunAsPolicy** específico.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-193">You use the **DefaultRunAsPolicy** section to specify a default user account for all code packages that don’t have a specific **RunAsPolicy** defined.</span></span> <span data-ttu-id="3c4e3-194">Si la mayoría de los paquetes de código especificados en el manifiesto de servicio que usa una aplicación deben ejecutarse en el mismo usuario, la aplicación solo puede definir una directiva RunAs predeterminada con dicha cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-194">If most of the code packages that are specified in the service manifest used by an application need to run under the same user, the application can just define a default RunAs policy with that user account.</span></span> <span data-ttu-id="3c4e3-195">En el ejemplo siguiente, se especifica que si un paquete de código no tiene una directiva **RunAsPolicy** especificada, tendrá que ejecutarse en la directiva **MyDefaultAccount** especificada en la sección de entidades de seguridad.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-195">The following example specifies that if a code package does not have a **RunAsPolicy** specified, the code package should run under the **MyDefaultAccount** specified in the principals section.</span></span>

```xml
<Policies>
  <DefaultRunAsPolicy UserRef="MyDefaultAccount"/>
</Policies>
```
### <a name="use-an-active-directory-domain-group-or-user"></a><span data-ttu-id="3c4e3-196">Uso de un usuario o un grupo de dominios de Active Directory</span><span class="sxs-lookup"><span data-stu-id="3c4e3-196">Use an Active Directory domain group or user</span></span>
<span data-ttu-id="3c4e3-197">Para una instancia de Service Fabric que se instale en Windows Server mediante el instalador independiente, puede ejecutar el servicio con las credenciales de una cuenta de grupo o usuario de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-197">For an instance of Service Fabric that was installed on Windows Server by using the standalone installer, you can run the service under the credentials for an Active Directory user or group account.</span></span> <span data-ttu-id="3c4e3-198">Esto se aplica a Active Directory local dentro del dominio y no a Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="3c4e3-198">This is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="3c4e3-199">Mediante el uso de un grupo o usuario de dominio puede tener acceso a otros recursos del dominio (por ejemplo, recursos compartidos de archivos) para los que se han concedido permisos.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-199">By using a domain user or group, you can then access other resources in the domain (for example, file shares) that have been granted permissions.</span></span>

<span data-ttu-id="3c4e3-200">El ejemplo siguiente muestra un usuario de Active Directory denominado *TestUser* con la contraseña de dominio cifrada mediante un certificado llamado *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-200">The following example shows an Active Directory user called *TestUser* with their domain password encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="3c4e3-201">Puede usar el comando de PowerShell `Invoke-ServiceFabricEncryptText` para crear el texto cifrado secreto.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-201">You can use the `Invoke-ServiceFabricEncryptText` PowerShell command to create the secret cipher text.</span></span> <span data-ttu-id="3c4e3-202">Vea [Administración de secretos en aplicaciones de Service Fabric](service-fabric-application-secret-management.md) | Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-202">See [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md) for details.</span></span>

<span data-ttu-id="3c4e3-203">La clave privada del certificado para descifrar la contraseña se debe implementar en la máquina local con un método fuera de banda (en Azure esto se realiza mediante Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="3c4e3-203">You must deploy the private key of the certificate to decrypt the password to the local machine by using an out-of-band method (in Azure, this is via Azure Resource Manager).</span></span> <span data-ttu-id="3c4e3-204">Posteriormente, cuando Service Fabric implemente el paquete de servicio en la máquina, podrá descifrar el secreto y, junto con el nombre de usuario, autenticarse mediante Active Directory para ejecutarse con esas credenciales.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-204">Then, when Service Fabric deploys the service package to the machine, it is able to decrypt the secret and (along with the user name) authenticate with Active Directory to run under those credentials.</span></span>

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
### <a name="use-a-group-managed-service-account"></a><span data-ttu-id="3c4e3-205">Use una cuenta de servicio administrada de grupo.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-205">Use a Group Managed Service Account.</span></span>
<span data-ttu-id="3c4e3-206">En el caso de una instancia de Service Fabric instalada en Windows Server mediante el instalador independiente, puede ejecutar el servicio como una cuenta de servicio administrada de grupo (gMSA).</span><span class="sxs-lookup"><span data-stu-id="3c4e3-206">For an instance of Service Fabric that was installed on Windows Server by using the standalone installer, you can run the service as a group Managed Service Account (gMSA).</span></span> <span data-ttu-id="3c4e3-207">Tenga en cuenta que esto se aplica a Active Directory local dentro del dominio y no para Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="3c4e3-207">Note that this is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="3c4e3-208">Con una gMSA no hay ninguna contraseña ni contraseña cifrada almacenada en el `Application Manifest`.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-208">By using a gMSA there is no password or encrypted password stored in the `Application Manifest`.</span></span>

<span data-ttu-id="3c4e3-209">En el ejemplo siguiente se muestra cómo crear una cuenta gMSA denominada *svc-Test$*, cómo implementar esa cuenta de servicio administrada en los nodos del clúster y cómo configurar la entidad de seguridad de usuario.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-209">The following example shows how to create a gMSA account called *svc-Test$*; how to deploy that managed service account to the cluster nodes; and how to configure the user principal.</span></span>

##### <a name="prerequisites"></a><span data-ttu-id="3c4e3-210">Requisitos previos.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-210">Prerequisites.</span></span>
- <span data-ttu-id="3c4e3-211">El dominio necesita una clave raíz KDS.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-211">The domain needs a KDS root key.</span></span>
- <span data-ttu-id="3c4e3-212">El dominio debe estar en un nivel funcional de Windows Server 2012 o superior.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-212">The domain needs to be at a Windows Server 2012 or later functional level.</span></span>

##### <a name="example"></a><span data-ttu-id="3c4e3-213">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="3c4e3-213">Example</span></span>
1. <span data-ttu-id="3c4e3-214">Haga que un administrador de dominio de Active Directory cree una cuenta de servicio administrada de grupo mediante el commandlet `New-ADServiceAccount` y asegúrese de que `PrincipalsAllowedToRetrieveManagedPassword` incluya todos los nodos del clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-214">Have an active directory domain administrator create a group managed service account using the `New-ADServiceAccount` commandlet and ensure that the `PrincipalsAllowedToRetrieveManagedPassword` includes all of the service fabric cluster nodes.</span></span> <span data-ttu-id="3c4e3-215">Tenga en cuenta que `AccountName`, `DnsHostName` y `ServicePrincipalName` deben ser únicos.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-215">Note that `AccountName`, `DnsHostName`, and `ServicePrincipalName` must be unique.</span></span>
```
New-ADServiceAccount -name svc-Test$ -DnsHostName svc-test.contoso.com  -ServicePrincipalNames http/svc-test.contoso.com -PrincipalsAllowedToRetrieveManagedPassword SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$
```
2. <span data-ttu-id="3c4e3-216">En cada uno de los nodos del clúster de Service Fabric (por ejemplo, `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`), instale y pruebe la gMSA.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-216">On each of the service fabric cluster nodes (for example, `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`), install and test the gMSA.</span></span>
```
Add-WindowsFeature RSAT-AD-PowerShell
Install-AdServiceAccount svc-Test$
Test-AdServiceAccount svc-Test$
```
3. <span data-ttu-id="3c4e3-217">Configure la entidad de seguridad de usuario y RunAsPolicy para que hagan referencia al usuario.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-217">Configure the User principal, and configure the RunAsPolicy to reference the user.</span></span>
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

## <a name="assign-a-security-access-policy-for-http-and-https-endpoints"></a><span data-ttu-id="3c4e3-218">Asignación de una directiva de acceso de seguridad a los puntos de conexión HTTP y HTTPS</span><span class="sxs-lookup"><span data-stu-id="3c4e3-218">Assign a security access policy for HTTP and HTTPS endpoints</span></span>
<span data-ttu-id="3c4e3-219">Si se aplica una directiva RunAs a un servicio y el manifiesto de servicio declara que hay recursos de puntos de conexión con el protocolo HTTP, es preciso especificar una directiva **SecurityAccessPolicy** para asegurarse de que los puertos asignados a dichos puntos de conexión aparezcan correctamente en la lista de control de acceso de la cuenta de usuario RunAs en la que se ejecuta el servicio.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-219">If you apply a RunAs policy to a service and the service manifest declares endpoint resources with the HTTP protocol, you must specify a **SecurityAccessPolicy** to ensure that ports allocated to these endpoints are correctly access-control listed for the RunAs user account that the service runs under.</span></span> <span data-ttu-id="3c4e3-220">En caso contrario, **http.sys** no tendrá acceso al servicio y aparecerán errores en las llamadas del cliente.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-220">Otherwise, **http.sys** does not have access to the service, and you get failures with calls from the client.</span></span> <span data-ttu-id="3c4e3-221">En el ejemplo siguiente se aplica la cuenta Customer1 a un punto de conexión denominado **EndpointName**, que le concede derechos de acceso total.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-221">The following example applies the Customer1 account to an endpoint called **EndpointName**, which gives it full access rights.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
   <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and the Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
</Policies>
```

<span data-ttu-id="3c4e3-222">En el caso del punto de conexión HTTPS, también es preciso indicar el nombre del certificado que se va a devolver al cliente.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-222">For the HTTPS endpoint, you also have to indicate the name of the certificate to return to the client.</span></span> <span data-ttu-id="3c4e3-223">Para ello, puede utilizar **EndpointBindingPolicy**, con el certificado definido en una sección de certificados del manifiesto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-223">You can do this by using **EndpointBindingPolicy**, with the certificate defined in a certificates section in the application manifest.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
  <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and the Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
  <!--EndpointBindingPolicy is needed if the EndpointName is secured with https -->
  <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
</Policies
```
## <a name="upgrading-multiple-applications-with-https-endpoints"></a><span data-ttu-id="3c4e3-224">Actualización de varias aplicaciones con puntos de conexión https</span><span class="sxs-lookup"><span data-stu-id="3c4e3-224">Upgrading multiple applications with https endpoints</span></span>
<span data-ttu-id="3c4e3-225">Debe tener cuidado de no usar el **mismo puerto** para distintas instancias de la misma aplicación cuando use http**s**.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-225">You need to be careful not to use the **same port** for different instances of the same application when using http**s**.</span></span> <span data-ttu-id="3c4e3-226">El motivo es que Service Fabric no podrá actualizar el certificado para una de las instancias de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-226">The reason is that Service Fabric won't be able to upgrade the cert for one of the application instances.</span></span> <span data-ttu-id="3c4e3-227">Por ejemplo, si la aplicación 1 o 2 desean actualizar sus certificados 1 a 2.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-227">For example, if application 1 or application 2 both want to upgrade their cert 1 to cert 2.</span></span> <span data-ttu-id="3c4e3-228">Una vez realizada la actualización, es posible que Service Fabric borre el registro del certificado 1 con http.sys, aunque la otra aplicación lo siga utilizando.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-228">When the upgrade happens, Service Fabric might have cleaned up the cert 1 registration with http.sys even though the other application is still using it.</span></span> <span data-ttu-id="3c4e3-229">Para evitar esto, Service Fabric detecta que hay ya otra instancia de la aplicación registrada en el puerto con el certificado (debido a http.sys) y se produce un error en la operación.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-229">To prevent this, Service Fabric detects that there is already another application instance registered on the port with the certificate (due to http.sys) and fails the operation.</span></span>

<span data-ttu-id="3c4e3-230">Por lo tanto, Service Fabric no admite la actualización de dos servicios diferentes que usen **el mismo puerto** en diferentes instancias de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-230">Hence Service Fabric does not support upgrading two different services using **the same port** in different application instances.</span></span> <span data-ttu-id="3c4e3-231">En otras palabras, no puede utilizar el mismo certificado en diferentes servicios en el mismo puerto.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-231">In other words, you cannot use the same certificate on different services on the same port.</span></span> <span data-ttu-id="3c4e3-232">Si necesita tener un certificado compartido en el mismo puerto, tiene que asegurarse de que los servicios se encuentren en distintos equipos con restricciones de posición.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-232">If you need to have a shared certificate on the same port, you need to ensure that the services are placed on different machines with placement constraints.</span></span> <span data-ttu-id="3c4e3-233">También puede considerar la posibilidad de utilizar puertos dinámicos de Service Fabric para cada servicio en cada instancia de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3c4e3-233">Or consider using Service Fabric dynamic ports if possible for each service in each application instance.</span></span> 

<span data-ttu-id="3c4e3-234">Si visualiza un error de actualización con https, aparecerá una advertencia de error que indica que "La API de servidor HTTP de Windows no admite varios certificados para las aplicaciones que comparten un puerto".</span><span class="sxs-lookup"><span data-stu-id="3c4e3-234">If you see an upgrade fail with https, an error warning saying "The Windows HTTP Server API does not support multiple certificates for applications that share a port.”</span></span>

## <a name="a-complete-application-manifest-example"></a><span data-ttu-id="3c4e3-235">Ejemplo completo de un manifiesto de aplicación</span><span class="sxs-lookup"><span data-stu-id="3c4e3-235">A complete application manifest example</span></span>
<span data-ttu-id="3c4e3-236">El siguiente manifiesto de aplicación muestra muchos de los diferentes valores:</span><span class="sxs-lookup"><span data-stu-id="3c4e3-236">The following application manifest shows many of the different settings:</span></span>

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
        <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and the Endpoint is http -->
         <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
        <!--EndpointBindingPolicy is needed the EndpointName is secured with https -->
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


<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="3c4e3-237">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3c4e3-237">Next steps</span></span>
* [<span data-ttu-id="3c4e3-238">Entender el modelo de aplicación</span><span class="sxs-lookup"><span data-stu-id="3c4e3-238">Understand the application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="3c4e3-239">Especificación de los recursos en un manifiesto de servicio</span><span class="sxs-lookup"><span data-stu-id="3c4e3-239">Specify resources in a service manifest</span></span>](service-fabric-service-manifest-resources.md)
* [<span data-ttu-id="3c4e3-240">Implementar una aplicación</span><span class="sxs-lookup"><span data-stu-id="3c4e3-240">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[image1]: ./media/service-fabric-application-runas-security/copy-to-output.png
