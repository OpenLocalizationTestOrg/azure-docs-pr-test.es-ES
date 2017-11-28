---
title: "Ejecución de tareas de inicio en Azure Cloud Services | Microsoft Docs"
description: "Las tareas de inicio ayudan a preparar el entorno de servicio en la nube para su aplicación. Esto le enseñará cómo funcionan las tareas de inicio y cómo realizarlas"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 886939be-4b5b-49cc-9a6e-2172e3c133e9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 1c1b3aa86dc8211de0c07c9fb68da5685c86f551
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-and-run-startup-tasks-for-a-cloud-service"></a><span data-ttu-id="72a2e-104">Configuración y ejecución de tareas de inicio para un servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="72a2e-104">How to configure and run startup tasks for a cloud service</span></span>
<span data-ttu-id="72a2e-105">Puede usar las tareas de inicio para realizar operaciones antes de que se inicie un rol.</span><span class="sxs-lookup"><span data-stu-id="72a2e-105">You can use startup tasks to perform operations before a role starts.</span></span> <span data-ttu-id="72a2e-106">Estas operaciones incluyen la instalación de un componente, el registro de componentes COM, el establecimiento de las claves del registro o el inicio de un proceso de ejecución largo.</span><span class="sxs-lookup"><span data-stu-id="72a2e-106">Operations that you might want to perform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span>

> [!NOTE]
> <span data-ttu-id="72a2e-107">Las tareas de inicio no son aplicables a las máquinas virtuales, solo a los roles web y de trabajo del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="72a2e-107">Startup tasks are not applicable to Virtual Machines, only to Cloud Service Web and Worker roles.</span></span>
> 
> 

## <a name="how-startup-tasks-work"></a><span data-ttu-id="72a2e-108">Cómo funcionan las tareas de inicio</span><span class="sxs-lookup"><span data-stu-id="72a2e-108">How startup tasks work</span></span>
<span data-ttu-id="72a2e-109">Las tareas de inicio son acciones que se emprenden antes de comenzar los roles y se definen en el archivo [ServiceDefinition.csdef] con el uso del elemento [Task] dentro del elemento [Startup].</span><span class="sxs-lookup"><span data-stu-id="72a2e-109">Startup tasks are actions that are taken before your roles begin and are defined in the [ServiceDefinition.csdef] file by using the [Task] element within the [Startup] element.</span></span> <span data-ttu-id="72a2e-110">Con frecuencia, las tareas de inicio son archivos por lotes, pero también pueden ser aplicaciones de consola o archivos por lotes que inician scripts de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="72a2e-110">Frequently startup tasks are batch files, but they can also be console applications, or batch files that start PowerShell scripts.</span></span>

<span data-ttu-id="72a2e-111">Las variables de entorno pasan información a una tarea de inicio y el almacenamiento local puede usarse para pasar información de una tarea de inicio.</span><span class="sxs-lookup"><span data-stu-id="72a2e-111">Environment variables pass information into a startup task, and local storage can be used to pass information out of a startup task.</span></span> <span data-ttu-id="72a2e-112">Por ejemplo, una variable de entorno puede especificar la ruta de acceso a un programa que quiera instalar, los archivos pueden escribirse en un almacenamiento local desde donde los roles los pueden leer más tarde.</span><span class="sxs-lookup"><span data-stu-id="72a2e-112">For example, an environment variable can specify the path to a program you want to install, and files can be written to local storage that can then be read later by your roles.</span></span>

<span data-ttu-id="72a2e-113">La tarea de inicio puede registrar información y errores en el directorio especificado por la variable de entorno **TEMP** .</span><span class="sxs-lookup"><span data-stu-id="72a2e-113">Your startup task can log information and errors to the directory specified by the **TEMP** environment variable.</span></span> <span data-ttu-id="72a2e-114">Durante la tarea de inicio, la variable de entorno **TEMP** se resuelve en el directorio *C:\\Resources\\temp\\[guid].[rolename]\\RoleTemp* cuando se ejecuta en la nube.</span><span class="sxs-lookup"><span data-stu-id="72a2e-114">During the startup task, the **TEMP** environment variable resolves to the *C:\\Resources\\temp\\[guid].[rolename]\\RoleTemp* directory when running on the cloud.</span></span>

<span data-ttu-id="72a2e-115">Las tareas de inicio también se puede ejecutar varias veces entre reinicios.</span><span class="sxs-lookup"><span data-stu-id="72a2e-115">Startup tasks can also be executed several times between reboots.</span></span> <span data-ttu-id="72a2e-116">Por ejemplo, se ejecutará la tarea de inicio cada vez que el rol se recicla y los reciclajes de rol pueden no incluir siempre un reinicio.</span><span class="sxs-lookup"><span data-stu-id="72a2e-116">For example, the startup task will be run each time the role recycles, and role recycles may not always include a reboot.</span></span> <span data-ttu-id="72a2e-117">Las tareas de inicio deben escribirse de forma que les sea posible ejecutarse varias veces sin problemas.</span><span class="sxs-lookup"><span data-stu-id="72a2e-117">Startup tasks should be written in a way that allows them to run several times without problems.</span></span>

<span data-ttu-id="72a2e-118">Las tareas de inicio tienen que terminar con un **errorlevel** (o código de salida) de cero para que el proceso de inicio se complete.</span><span class="sxs-lookup"><span data-stu-id="72a2e-118">Startup tasks must end with an **errorlevel** (or exit code) of zero for the startup process to complete.</span></span> <span data-ttu-id="72a2e-119">Si una tarea de inicio finaliza con un **errorlevel**distinto de cero, el rol no se iniciará.</span><span class="sxs-lookup"><span data-stu-id="72a2e-119">If a startup task ends with a non-zero **errorlevel**, the role will not start.</span></span>

## <a name="role-startup-order"></a><span data-ttu-id="72a2e-120">Orden de inicio de rol</span><span class="sxs-lookup"><span data-stu-id="72a2e-120">Role startup order</span></span>
<span data-ttu-id="72a2e-121">A continuación se enumera el procedimiento de inicio de rol en Azure:</span><span class="sxs-lookup"><span data-stu-id="72a2e-121">The following lists the role startup procedure in Azure:</span></span>

1. <span data-ttu-id="72a2e-122">La instancia se marca como **Starting** y no recibe tráfico.</span><span class="sxs-lookup"><span data-stu-id="72a2e-122">The instance is marked as **Starting** and does not receive traffic.</span></span>
2. <span data-ttu-id="72a2e-123">Todas las tareas de inicio se ejecutan de acuerdo con su atributo **taskType** .</span><span class="sxs-lookup"><span data-stu-id="72a2e-123">All startup tasks are executed according to their **taskType** attribute.</span></span>
   
   * <span data-ttu-id="72a2e-124">Las tareas con el valor **simple** se ejecutan sincrónicamente, una a una.</span><span class="sxs-lookup"><span data-stu-id="72a2e-124">The **simple** tasks are executed synchronously, one at a time.</span></span>
   * <span data-ttu-id="72a2e-125">Las tareas con los valores **background** y **foreground** se inician de forma asincrónica, paralelas a la tarea de inicio.</span><span class="sxs-lookup"><span data-stu-id="72a2e-125">The **background** and **foreground** tasks are started asynchronously, parallel to the startup task.</span></span>  
     
     > [!WARNING]
     > <span data-ttu-id="72a2e-126">Puede que IIS no se haya configurado por completo durante la fase de la tarea de inicio en el proceso de inicio, por lo que los datos específicos de rol pueden no estar disponibles.</span><span class="sxs-lookup"><span data-stu-id="72a2e-126">IIS may not be fully configured during the startup task stage in the startup process, so role-specific data may not be available.</span></span> <span data-ttu-id="72a2e-127">Las tareas de inicio que requieren datos específicos de la role tienen que usar [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).</span><span class="sxs-lookup"><span data-stu-id="72a2e-127">Startup tasks that require role-specific data should use [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).</span></span>
     > 
     > 
3. <span data-ttu-id="72a2e-128">Se inicia el proceso de host de rol y se crea el sitio en IIS.</span><span class="sxs-lookup"><span data-stu-id="72a2e-128">The role host process is started and the site is created in IIS.</span></span>
4. <span data-ttu-id="72a2e-129">Se llama al método [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) .</span><span class="sxs-lookup"><span data-stu-id="72a2e-129">The [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method is called.</span></span>
5. <span data-ttu-id="72a2e-130">La instancia se marca como **Ready** y el tráfico se enruta a la instancia.</span><span class="sxs-lookup"><span data-stu-id="72a2e-130">The instance is marked as **Ready** and traffic is routed to the instance.</span></span>
6. <span data-ttu-id="72a2e-131">Se llama al método [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) .</span><span class="sxs-lookup"><span data-stu-id="72a2e-131">The [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method is called.</span></span>

## <a name="example-of-a-startup-task"></a><span data-ttu-id="72a2e-132">Ejemplo de una tarea de inicio</span><span class="sxs-lookup"><span data-stu-id="72a2e-132">Example of a startup task</span></span>
<span data-ttu-id="72a2e-133">Las tareas de inicio se definen en el archivo [ServiceDefinition.csdef] , en el elemento **Task** .</span><span class="sxs-lookup"><span data-stu-id="72a2e-133">Startup tasks are defined in the [ServiceDefinition.csdef] file, in the **Task** element.</span></span> <span data-ttu-id="72a2e-134">El atributo **commandLine** especifica el nombre y los parámetros del archivo por lotes o del comando de consola, el atributo **executionContext** especifica el nivel de privilegio de la tarea de inicio y el atributo **taskType** especifica cómo se ejecutará la tarea.</span><span class="sxs-lookup"><span data-stu-id="72a2e-134">The **commandLine** attribute specifies the name and parameters of the startup batch file or console command, the **executionContext** attribute specifies the privilege level of the startup task, and the **taskType** attribute specifies how the task will be executed.</span></span>

<span data-ttu-id="72a2e-135">En este ejemplo, una variable de entorno **MyVersionNumber**, se crea para la tarea de inicio y se establece en el valor "**1.0.0.0**".</span><span class="sxs-lookup"><span data-stu-id="72a2e-135">In this example, an environment variable, **MyVersionNumber**, is created for the startup task and set to the value "**1.0.0.0**".</span></span>

<span data-ttu-id="72a2e-136">**ServiceDefinition.csdef**:</span><span class="sxs-lookup"><span data-stu-id="72a2e-136">**ServiceDefinition.csdef**:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
        <Environment>
            <Variable name="MyVersionNumber" value="1.0.0.0" />
        </Environment>
    </Task>
</Startup>
```

<span data-ttu-id="72a2e-137">En el ejemplo siguiente, el archivo por lotes **Startup.cmd** escribe la línea "The current version is 1.0.0.0" en el archivo StartupLog.txt en el directorio especificado por la variable de entorno TEMP.</span><span class="sxs-lookup"><span data-stu-id="72a2e-137">In the following example, the **Startup.cmd** batch file writes the line "The current version is 1.0.0.0" to the StartupLog.txt file in the directory specified by the TEMP environment variable.</span></span> <span data-ttu-id="72a2e-138">La línea `EXIT /B 0` garantiza que la tarea de inicio finaliza con un **errorlevel** de cero.</span><span class="sxs-lookup"><span data-stu-id="72a2e-138">The `EXIT /B 0` line ensures that the startup task ends with an **errorlevel** of zero.</span></span>

```cmd
ECHO The current version is %MyVersionNumber% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT /B 0
```

> [!NOTE]
> <span data-ttu-id="72a2e-139">En Visual Studio, la propiedad **Copiar en el directorio de salida** para el archivo por lotes de inicio debe establecerse en **Copiar siempre** para asegurarse de que el archivo por lotes de inicio se implementa debidamente en el proyecto en Azure (**approot\\bin** para los roles web y **approot** para los roles de trabajo).</span><span class="sxs-lookup"><span data-stu-id="72a2e-139">In Visual Studio, the **Copy to Output Directory** property for your startup batch file should be set to **Copy Always** to be sure that your startup batch file is properly deployed to your project on Azure (**approot\\bin** for Web roles, and **approot** for worker roles).</span></span>
> 
> 

## <a name="description-of-task-attributes"></a><span data-ttu-id="72a2e-140">Descripción de los atributos de la tarea</span><span class="sxs-lookup"><span data-stu-id="72a2e-140">Description of task attributes</span></span>
<span data-ttu-id="72a2e-141">A continuación se describen los atributos del elemento **Task** en el archivo [ServiceDefinition.csdef] :</span><span class="sxs-lookup"><span data-stu-id="72a2e-141">The following describes the attributes of the **Task** element in the [ServiceDefinition.csdef] file:</span></span>

<span data-ttu-id="72a2e-142">**commandLine** - especifica la línea de comandos para la tarea de inicio:</span><span class="sxs-lookup"><span data-stu-id="72a2e-142">**commandLine** - Specifies the command line for the startup task:</span></span>

* <span data-ttu-id="72a2e-143">El comando, con los parámetros de línea de comandos opcionales, que comienza la tarea de inicio.</span><span class="sxs-lookup"><span data-stu-id="72a2e-143">The command, with optional command line parameters, which begins the startup task.</span></span>
* <span data-ttu-id="72a2e-144">Con frecuencia es el nombre de archivo de un archivo por lotes .bat o .cmd.</span><span class="sxs-lookup"><span data-stu-id="72a2e-144">Frequently this is the filename of a .cmd or .bat batch file.</span></span>
* <span data-ttu-id="72a2e-145">La tarea es relativa a la carpeta AppRoot\\Bin para la implementación.</span><span class="sxs-lookup"><span data-stu-id="72a2e-145">The task is relative to the AppRoot\\Bin folder for the deployment.</span></span> <span data-ttu-id="72a2e-146">Las variables de entorno no se expanden para determinar la ruta de acceso y el archivo de la tarea.</span><span class="sxs-lookup"><span data-stu-id="72a2e-146">Environment variables are not expanded in determining the path and file of the task.</span></span> <span data-ttu-id="72a2e-147">Si se requiere la expansión del entorno, puede crear un pequeño script .cmd que llame a la tarea de inicio.</span><span class="sxs-lookup"><span data-stu-id="72a2e-147">If environment expansion is required, you can create a small .cmd script that calls your startup task.</span></span>
* <span data-ttu-id="72a2e-148">Puede ser una aplicación de consola o un archivo por lotes que inicie un [script de PowerShell](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).</span><span class="sxs-lookup"><span data-stu-id="72a2e-148">Can be a console application or a batch file that starts a [PowerShell script](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).</span></span>

<span data-ttu-id="72a2e-149">**executionContext** - especifica el nivel de privilegio de la tarea de inicio.</span><span class="sxs-lookup"><span data-stu-id="72a2e-149">**executionContext** - Specifies the privilege level for the startup task.</span></span> <span data-ttu-id="72a2e-150">El nivel de privilegio puede tener los valores limited o elevated:</span><span class="sxs-lookup"><span data-stu-id="72a2e-150">The privilege level can be limited or elevated:</span></span>

* <span data-ttu-id="72a2e-151">**limited**</span><span class="sxs-lookup"><span data-stu-id="72a2e-151">**limited**</span></span>  
  <span data-ttu-id="72a2e-152">la tarea de inicio se ejecuta con los mismos privilegios que el rol.</span><span class="sxs-lookup"><span data-stu-id="72a2e-152">The startup task runs with the same privileges as the role.</span></span> <span data-ttu-id="72a2e-153">Cuando el atributo **executionContext** para el elemento [Runtime] también tiene el valor **limited**, se usan los privilegios de usuario.</span><span class="sxs-lookup"><span data-stu-id="72a2e-153">When the **executionContext** attribute for the [Runtime] element is also **limited**, then user privileges are used.</span></span>
* <span data-ttu-id="72a2e-154">**elevated**</span><span class="sxs-lookup"><span data-stu-id="72a2e-154">**elevated**</span></span>  
  <span data-ttu-id="72a2e-155">la tarea de inicio se ejecuta con privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="72a2e-155">The startup task runs with administrator privileges.</span></span> <span data-ttu-id="72a2e-156">Esto permite a las tareas de inicio instalar programas, realizar cambios en la configuración de IIS, realizar cambios en el registro y otras tareas de nivel de administrador, sin aumentar el nivel de privilegio del propio rol.</span><span class="sxs-lookup"><span data-stu-id="72a2e-156">This allows startup tasks to install programs, make IIS configuration changes, perform registry changes, and other administrator level tasks, without increasing the privilege level of the role itself.</span></span>  

> [!NOTE]
> <span data-ttu-id="72a2e-157">No es preciso que el nivel de privilegios de la tarea de inicio sea el mismo que el del propio rol.</span><span class="sxs-lookup"><span data-stu-id="72a2e-157">The privilege level of a startup task does not need to be the same as the role itself.</span></span>
> 
> 

<span data-ttu-id="72a2e-158">**taskType** - especifica la manera en que se ejecuta una tarea de inicio.</span><span class="sxs-lookup"><span data-stu-id="72a2e-158">**taskType** - Specifies the way a startup task is executed.</span></span>

* <span data-ttu-id="72a2e-159">**simple**</span><span class="sxs-lookup"><span data-stu-id="72a2e-159">**simple**</span></span>  
  <span data-ttu-id="72a2e-160">Las tareas se ejecutan sincrónicamente, una a una, en el orden especificado en el archivo [ServiceDefinition.csdef] .</span><span class="sxs-lookup"><span data-stu-id="72a2e-160">Tasks are executed synchronously, one at a time, in the order specified in the [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="72a2e-161">Cuando una tarea de inicio **simple** finaliza con un **errorlevel** de cero, se ejecuta la siguiente tarea de inicio **simple**.</span><span class="sxs-lookup"><span data-stu-id="72a2e-161">When one **simple** startup task ends with an **errorlevel** of zero, the next **simple** startup task is executed.</span></span> <span data-ttu-id="72a2e-162">Si no hay más tareas de inicio con el valor **simple** para ejecutarse, se iniciará el propio rol.</span><span class="sxs-lookup"><span data-stu-id="72a2e-162">If there are no more **simple** startup tasks to execute, then the role itself will be started.</span></span>   
  
  > [!NOTE]
  > <span data-ttu-id="72a2e-163">Si la tarea **simple** finaliza con un valor **errorlevel** distinto de cero, se bloqueará la instancia.</span><span class="sxs-lookup"><span data-stu-id="72a2e-163">If the **simple** task ends with a non-zero **errorlevel**, the instance will be blocked.</span></span> <span data-ttu-id="72a2e-164">Las subsiguientes tareas de inicio **simple** y el propio rol no se iniciarán.</span><span class="sxs-lookup"><span data-stu-id="72a2e-164">Subsequent **simple** startup tasks, and the role itself, will not start.</span></span>
  > 
  > 
  
    <span data-ttu-id="72a2e-165">Para asegurarse de que el archivo por lotes finaliza con un valor **errorlevel** de cero, ejecute el comando `EXIT /B 0` al final del proceso de archivo por lotes.</span><span class="sxs-lookup"><span data-stu-id="72a2e-165">To ensure that your batch file ends with an **errorlevel** of zero, execute the command `EXIT /B 0` at the end of your batch file process.</span></span>
* <span data-ttu-id="72a2e-166">**background**</span><span class="sxs-lookup"><span data-stu-id="72a2e-166">**background**</span></span>  
  <span data-ttu-id="72a2e-167">Las tareas se ejecutan de forma asincrónica, en paralelo con el inicio del rol.</span><span class="sxs-lookup"><span data-stu-id="72a2e-167">Tasks are executed asynchronously, in parallel with the startup of the role.</span></span>
* <span data-ttu-id="72a2e-168">**foreground**</span><span class="sxs-lookup"><span data-stu-id="72a2e-168">**foreground**</span></span>  
  <span data-ttu-id="72a2e-169">Las tareas se ejecutan de forma asincrónica, en paralelo con el inicio del rol.</span><span class="sxs-lookup"><span data-stu-id="72a2e-169">Tasks are executed asynchronously, in parallel with the startup of the role.</span></span> <span data-ttu-id="72a2e-170">La diferencia clave entre una tarea con el valor **foreground** y otra con el valor **background** es que una tarea **foreground** impide que el rol se recicle o se cierre hasta que haya finalizado la tarea.</span><span class="sxs-lookup"><span data-stu-id="72a2e-170">The key difference between a **foreground** and a **background** task is that a **foreground** task prevents the role from recycling or shutting down until the task has ended.</span></span> <span data-ttu-id="72a2e-171">Las tareas con el valor **background** no tienen esta restricción.</span><span class="sxs-lookup"><span data-stu-id="72a2e-171">The **background** tasks do not have this restriction.</span></span>

## <a name="environment-variables"></a><span data-ttu-id="72a2e-172">Variables de entorno</span><span class="sxs-lookup"><span data-stu-id="72a2e-172">Environment variables</span></span>
<span data-ttu-id="72a2e-173">Las variables de entorno son una manera de pasar información a una tarea de inicio.</span><span class="sxs-lookup"><span data-stu-id="72a2e-173">Environment variables are a way to pass information to a startup task.</span></span> <span data-ttu-id="72a2e-174">Por ejemplo, puede colocar la ruta de acceso a un blob que contiene un programa para instalar, o los números de puerto que usará el rol o las configuraciones que controlan las funciones de la tarea de inicio.</span><span class="sxs-lookup"><span data-stu-id="72a2e-174">For example, you can put the path to a blob that contains a program to install, or port numbers that your role will use, or settings to control features of your startup task.</span></span>

<span data-ttu-id="72a2e-175">Hay dos tipos de variables de entorno para las tareas de inicio; variables de entorno estáticas y variables de entorno basadas en los miembros de la clase [RoleEnvironment] .</span><span class="sxs-lookup"><span data-stu-id="72a2e-175">There are two kinds of environment variables for startup tasks; static environment variables and environment variables based on members of the [RoleEnvironment] class.</span></span> <span data-ttu-id="72a2e-176">Ambos tipos se encuentran en las sección [Environment] del archivo [ServiceDefinition.csdef] y usan el elemento [Variable] y el atributo **name**.</span><span class="sxs-lookup"><span data-stu-id="72a2e-176">Both are in the [Environment] section of the [ServiceDefinition.csdef] file, and both use the [Variable] element and **name** attribute.</span></span>

<span data-ttu-id="72a2e-177">Las variables de entorno estáticas usan el atributo **value** del elemento [Variable] .</span><span class="sxs-lookup"><span data-stu-id="72a2e-177">Static environment variables uses the **value** attribute of the [Variable] element.</span></span> <span data-ttu-id="72a2e-178">El ejemplo anterior crea la variable de entorno **MyVersionNumber** que tiene un valor estático de "**1.0.0.0**".</span><span class="sxs-lookup"><span data-stu-id="72a2e-178">The example above creates the environment variable **MyVersionNumber** which has a static value of "**1.0.0.0**".</span></span> <span data-ttu-id="72a2e-179">Otro ejemplo sería crear una variable de entorno **StagingOrProduction** para la que pueda establecer manualmente los valores de "**staging**" o "**production**" para realizar acciones de inicio diferentes en función del valor de la variable de entorno **StagingOrProduction**.</span><span class="sxs-lookup"><span data-stu-id="72a2e-179">Another example would be to create a **StagingOrProduction** environment variable which you can manually set to values of "**staging**" or "**production**" to perform different startup actions based on the value of the **StagingOrProduction** environment variable.</span></span>

<span data-ttu-id="72a2e-180">Las variables de entorno que se basan en los miembros de la clase RoleEnvironment no usan el atributo **value** del elemento [Variable] .</span><span class="sxs-lookup"><span data-stu-id="72a2e-180">Environment variables based on members of the RoleEnvironment class do not use the **value** attribute of the [Variable] element.</span></span> <span data-ttu-id="72a2e-181">En su lugar, el elemento secundario [RoleInstanceValue], con el valor de atributo **XPath** adecuado, se usa para crear una variable de entorno basada en un miembro específico de la clase [RoleEnvironment].</span><span class="sxs-lookup"><span data-stu-id="72a2e-181">Instead, the [RoleInstanceValue] child element, with the appropriate **XPath** attribute value, are used to create an environment variable based on a specific member of the [RoleEnvironment] class.</span></span> <span data-ttu-id="72a2e-182">Los valores del atributo **XPath** para acceder a distintos valores [RoleEnvironment] pueden encontrarse [aquí](cloud-services-role-config-xpath.md).</span><span class="sxs-lookup"><span data-stu-id="72a2e-182">Values for the **XPath** attribute to access various [RoleEnvironment] values can be found [here](cloud-services-role-config-xpath.md).</span></span>

<span data-ttu-id="72a2e-183">Por ejemplo, para crear una variable de entorno que sea "**true**" cuando se ejecuta la instancia en el emulador de proceso, y "**false**" cuando se ejecuta en la nube, use los siguientes elementos [Variable] y [RoleInstanceValue]:</span><span class="sxs-lookup"><span data-stu-id="72a2e-183">For example, to create an environment variable that is "**true**" when the instance is running in the compute emulator, and "**false**" when running in the cloud, use the following [Variable] and [RoleInstanceValue] elements:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>

            <!-- Create the environment variable that informs the startup task whether it is running
                in the Compute Emulator or in the cloud. "%ComputeEmulatorRunning%"=="true" when
                running in the Compute Emulator, "%ComputeEmulatorRunning%"=="false" when running
                in the cloud. -->

            <Variable name="ComputeEmulatorRunning">
                <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
            </Variable>

        </Environment>
    </Task>
</Startup>
```

## <a name="next-steps"></a><span data-ttu-id="72a2e-184">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="72a2e-184">Next steps</span></span>
<span data-ttu-id="72a2e-185">Aprenda a realizar algunas [tareas de inicio comunes](cloud-services-startup-tasks-common.md) con el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="72a2e-185">Learn how to perform some [common startup tasks](cloud-services-startup-tasks-common.md) with your Cloud Service.</span></span>

<span data-ttu-id="72a2e-186">[Empaquete](cloud-services-model-and-package.md) el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="72a2e-186">[Package](cloud-services-model-and-package.md) your Cloud Service.</span></span>  

<span data-ttu-id="72a2e-187">[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef</span><span class="sxs-lookup"><span data-stu-id="72a2e-187">[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef</span></span>
<span data-ttu-id="72a2e-188">[Task]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task</span><span class="sxs-lookup"><span data-stu-id="72a2e-188">[Task]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task</span></span>
<span data-ttu-id="72a2e-189">[Startup]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup</span><span class="sxs-lookup"><span data-stu-id="72a2e-189">[Startup]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup</span></span>
<span data-ttu-id="72a2e-190">[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime</span><span class="sxs-lookup"><span data-stu-id="72a2e-190">[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime</span></span>
<span data-ttu-id="72a2e-191">[Environment]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment</span><span class="sxs-lookup"><span data-stu-id="72a2e-191">[Environment]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment</span></span>
<span data-ttu-id="72a2e-192">[Variable]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable</span><span class="sxs-lookup"><span data-stu-id="72a2e-192">[Variable]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable</span></span>
<span data-ttu-id="72a2e-193">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span><span class="sxs-lookup"><span data-stu-id="72a2e-193">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span></span>
<span data-ttu-id="72a2e-194">[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx</span><span class="sxs-lookup"><span data-stu-id="72a2e-194">[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx</span></span>
