---
title: aaaRun las tareas de inicio en los servicios de nube de Azure | Documentos de Microsoft
description: "Las tareas de inicio ayudan a preparar el entorno de servicio en la nube para su aplicación. Esto le enseña cómo trabajo las tareas de inicio y cómo toomake ellos"
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
ms.openlocfilehash: 3391a5d7434164f59972b8e497e5c34e33409543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-and-run-startup-tasks-for-a-cloud-service"></a><span data-ttu-id="6eb57-104">Cómo las tareas de inicio tooconfigure y ejecución de un servicio de nube</span><span class="sxs-lookup"><span data-stu-id="6eb57-104">How tooconfigure and run startup tasks for a cloud service</span></span>
<span data-ttu-id="6eb57-105">Puede utilizar operaciones de tooperform de tareas de inicio antes de que se inicia un rol.</span><span class="sxs-lookup"><span data-stu-id="6eb57-105">You can use startup tasks tooperform operations before a role starts.</span></span> <span data-ttu-id="6eb57-106">Operaciones que podría interesarle tooperform incluyen la instalación de un componente, registrando los componentes COM, configurar claves de registro o iniciar un proceso de ejecución prolongada.</span><span class="sxs-lookup"><span data-stu-id="6eb57-106">Operations that you might want tooperform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span>

> [!NOTE]
> <span data-ttu-id="6eb57-107">Las tareas de inicio no son aplicables tooVirtual máquinas, solo tooCloud servicio Web y roles de trabajo.</span><span class="sxs-lookup"><span data-stu-id="6eb57-107">Startup tasks are not applicable tooVirtual Machines, only tooCloud Service Web and Worker roles.</span></span>
> 
> 

## <a name="how-startup-tasks-work"></a><span data-ttu-id="6eb57-108">Cómo funcionan las tareas de inicio</span><span class="sxs-lookup"><span data-stu-id="6eb57-108">How startup tasks work</span></span>
<span data-ttu-id="6eb57-109">Las tareas de inicio son acciones que se realizan antes de que sus roles comienzan y se definen en hello [ServiceDefinition.csdef] archivo mediante hello [tarea] elemento dentro de hello [inicio]elemento.</span><span class="sxs-lookup"><span data-stu-id="6eb57-109">Startup tasks are actions that are taken before your roles begin and are defined in hello [ServiceDefinition.csdef] file by using hello [Task] element within hello [Startup] element.</span></span> <span data-ttu-id="6eb57-110">Con frecuencia, las tareas de inicio son archivos por lotes, pero también pueden ser aplicaciones de consola o archivos por lotes que inician scripts de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6eb57-110">Frequently startup tasks are batch files, but they can also be console applications, or batch files that start PowerShell scripts.</span></span>

<span data-ttu-id="6eb57-111">Las variables de entorno pasan información en una tarea de inicio y almacenamiento local puede tener información de uso toopass fuera de una tarea de inicio.</span><span class="sxs-lookup"><span data-stu-id="6eb57-111">Environment variables pass information into a startup task, and local storage can be used toopass information out of a startup task.</span></span> <span data-ttu-id="6eb57-112">Por ejemplo, una variable de entorno puede especificar el programa de tooa de ruta de acceso de hello desea tooinstall, y se pueden escribir archivos de almacenamiento toolocal que, a continuación, se pueden leer más tarde los roles.</span><span class="sxs-lookup"><span data-stu-id="6eb57-112">For example, an environment variable can specify hello path tooa program you want tooinstall, and files can be written toolocal storage that can then be read later by your roles.</span></span>

<span data-ttu-id="6eb57-113">La tarea de inicio puede registrar información y errores toohello directorio especificado por hello **TEMP** variable de entorno.</span><span class="sxs-lookup"><span data-stu-id="6eb57-113">Your startup task can log information and errors toohello directory specified by hello **TEMP** environment variable.</span></span> <span data-ttu-id="6eb57-114">Durante la tarea de inicio de Hola Hola **TEMP** variable de entorno resuelve toohello *C:\\recursos\\temp\\[guid]. [ roleName]\\RoleTemp* directorio cuando se ejecuta en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="6eb57-114">During hello startup task, hello **TEMP** environment variable resolves toohello *C:\\Resources\\temp\\[guid].[rolename]\\RoleTemp* directory when running on hello cloud.</span></span>

<span data-ttu-id="6eb57-115">Las tareas de inicio también se puede ejecutar varias veces entre reinicios.</span><span class="sxs-lookup"><span data-stu-id="6eb57-115">Startup tasks can also be executed several times between reboots.</span></span> <span data-ttu-id="6eb57-116">Por ejemplo, tarea de inicio de Hola se ejecutará cada vez que se recicle el rol de Hola y reciclajes de rol no pueden incluir siempre un reinicio.</span><span class="sxs-lookup"><span data-stu-id="6eb57-116">For example, hello startup task will be run each time hello role recycles, and role recycles may not always include a reboot.</span></span> <span data-ttu-id="6eb57-117">Las tareas de inicio deben escribirse de forma que les permita toorun varias veces sin problemas.</span><span class="sxs-lookup"><span data-stu-id="6eb57-117">Startup tasks should be written in a way that allows them toorun several times without problems.</span></span>

<span data-ttu-id="6eb57-118">Las tareas de inicio deben terminar con un **errorlevel** (o código de salida) de cero para toocomplete de proceso de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="6eb57-118">Startup tasks must end with an **errorlevel** (or exit code) of zero for hello startup process toocomplete.</span></span> <span data-ttu-id="6eb57-119">Si una tarea de inicio termina con un elemento que es distinto de cero **errorlevel**, Hola rol no se iniciará.</span><span class="sxs-lookup"><span data-stu-id="6eb57-119">If a startup task ends with a non-zero **errorlevel**, hello role will not start.</span></span>

## <a name="role-startup-order"></a><span data-ttu-id="6eb57-120">Orden de inicio de rol</span><span class="sxs-lookup"><span data-stu-id="6eb57-120">Role startup order</span></span>
<span data-ttu-id="6eb57-121">Hola listas Hola el procedimiento de inicio de rol en Azure:</span><span class="sxs-lookup"><span data-stu-id="6eb57-121">hello following lists hello role startup procedure in Azure:</span></span>

1. <span data-ttu-id="6eb57-122">Hola instancia se marca como **inicial** y no recibe tráfico.</span><span class="sxs-lookup"><span data-stu-id="6eb57-122">hello instance is marked as **Starting** and does not receive traffic.</span></span>
2. <span data-ttu-id="6eb57-123">Todas las tareas de inicio se ejecutan según tootheir **taskType** atributo.</span><span class="sxs-lookup"><span data-stu-id="6eb57-123">All startup tasks are executed according tootheir **taskType** attribute.</span></span>
   
   * <span data-ttu-id="6eb57-124">Hola **simple** tareas se ejecutan sincrónicamente, uno en uno.</span><span class="sxs-lookup"><span data-stu-id="6eb57-124">hello **simple** tasks are executed synchronously, one at a time.</span></span>
   * <span data-ttu-id="6eb57-125">Hola **fondo** y **primer plano** tareas son tareas de inicio de toohello iniciado de forma asincrónica, en paralelo.</span><span class="sxs-lookup"><span data-stu-id="6eb57-125">hello **background** and **foreground** tasks are started asynchronously, parallel toohello startup task.</span></span>  
     
     > [!WARNING]
     > <span data-ttu-id="6eb57-126">IIS puede no esté completamente configurada durante la fase de tarea de inicio de hello en el proceso de inicio de hello, por lo que los datos específicos de funciones no estén disponibles.</span><span class="sxs-lookup"><span data-stu-id="6eb57-126">IIS may not be fully configured during hello startup task stage in hello startup process, so role-specific data may not be available.</span></span> <span data-ttu-id="6eb57-127">Las tareas de inicio que requieren datos específicos de la role tienen que usar [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).</span><span class="sxs-lookup"><span data-stu-id="6eb57-127">Startup tasks that require role-specific data should use [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).</span></span>
     > 
     > 
3. <span data-ttu-id="6eb57-128">se inicia el proceso de host de rol de Hola y se crea el sitio de hello en IIS.</span><span class="sxs-lookup"><span data-stu-id="6eb57-128">hello role host process is started and hello site is created in IIS.</span></span>
4. <span data-ttu-id="6eb57-129">Hola [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) se llama al método.</span><span class="sxs-lookup"><span data-stu-id="6eb57-129">hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method is called.</span></span>
5. <span data-ttu-id="6eb57-130">Hola instancia se marca como **listo** y tráfico enrutado toohello instancia.</span><span class="sxs-lookup"><span data-stu-id="6eb57-130">hello instance is marked as **Ready** and traffic is routed toohello instance.</span></span>
6. <span data-ttu-id="6eb57-131">Hola [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) se llama al método.</span><span class="sxs-lookup"><span data-stu-id="6eb57-131">hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method is called.</span></span>

## <a name="example-of-a-startup-task"></a><span data-ttu-id="6eb57-132">Ejemplo de una tarea de inicio</span><span class="sxs-lookup"><span data-stu-id="6eb57-132">Example of a startup task</span></span>
<span data-ttu-id="6eb57-133">Las tareas de inicio se definen en hello [ServiceDefinition.csdef] archivo Hola **tarea** elemento.</span><span class="sxs-lookup"><span data-stu-id="6eb57-133">Startup tasks are defined in hello [ServiceDefinition.csdef] file, in hello **Task** element.</span></span> <span data-ttu-id="6eb57-134">Hola **commandLine** atributo especifica el nombre de Hola y parámetros de proceso por lotes de inicio de Hola de archivo o comando de la consola, hello **executionContext** atributo especifica el nivel de privilegio de Hola de inicio de Hola tarea y hello **taskType** atributo especifica cómo se ejecutará la tarea hello.</span><span class="sxs-lookup"><span data-stu-id="6eb57-134">hello **commandLine** attribute specifies hello name and parameters of hello startup batch file or console command, hello **executionContext** attribute specifies hello privilege level of hello startup task, and hello **taskType** attribute specifies how hello task will be executed.</span></span>

<span data-ttu-id="6eb57-135">En este ejemplo, una variable de entorno **MyVersionNumber**, se crea para la tarea de inicio de Hola y establezca el valor de toohello "**1.0.0.0**".</span><span class="sxs-lookup"><span data-stu-id="6eb57-135">In this example, an environment variable, **MyVersionNumber**, is created for hello startup task and set toohello value "**1.0.0.0**".</span></span>

<span data-ttu-id="6eb57-136">**ServiceDefinition.csdef**:</span><span class="sxs-lookup"><span data-stu-id="6eb57-136">**ServiceDefinition.csdef**:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
        <Environment>
            <Variable name="MyVersionNumber" value="1.0.0.0" />
        </Environment>
    </Task>
</Startup>
```

<span data-ttu-id="6eb57-137">En el siguiente ejemplo de Hola Hola **Startup.cmd** archivo por lotes escribe "la versión actual de hello es 1.0.0.0" toohello StartupLog.txt archivo línea hello en directorio de hello especificado por la variable de entorno TEMP Hola.</span><span class="sxs-lookup"><span data-stu-id="6eb57-137">In hello following example, hello **Startup.cmd** batch file writes hello line "hello current version is 1.0.0.0" toohello StartupLog.txt file in hello directory specified by hello TEMP environment variable.</span></span> <span data-ttu-id="6eb57-138">Hola `EXIT /B 0` línea garantiza que esa tarea de inicio de hello termina con un **errorlevel** de cero.</span><span class="sxs-lookup"><span data-stu-id="6eb57-138">hello `EXIT /B 0` line ensures that hello startup task ends with an **errorlevel** of zero.</span></span>

```cmd
ECHO hello current version is %MyVersionNumber% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT /B 0
```

> [!NOTE]
> <span data-ttu-id="6eb57-139">En Visual Studio, Hola **copiar tooOutput directorio** propiedad para el archivo por lotes de inicio debe establecerse demasiado**copiar siempre** toobe seguro de que el archivo por lotes de inicio esté correctamente implementado tooyour proyecto en Azure (**approot\\bin** para los roles de Web, y **approot** para roles de trabajo).</span><span class="sxs-lookup"><span data-stu-id="6eb57-139">In Visual Studio, hello **Copy tooOutput Directory** property for your startup batch file should be set too**Copy Always** toobe sure that your startup batch file is properly deployed tooyour project on Azure (**approot\\bin** for Web roles, and **approot** for worker roles).</span></span>
> 
> 

## <a name="description-of-task-attributes"></a><span data-ttu-id="6eb57-140">Descripción de los atributos de la tarea</span><span class="sxs-lookup"><span data-stu-id="6eb57-140">Description of task attributes</span></span>
<span data-ttu-id="6eb57-141">Hello siguiente describe los atributos de Hola de hello **tarea** elemento Hola [ServiceDefinition.csdef] archivo:</span><span class="sxs-lookup"><span data-stu-id="6eb57-141">hello following describes hello attributes of hello **Task** element in hello [ServiceDefinition.csdef] file:</span></span>

<span data-ttu-id="6eb57-142">**la línea de comandos** -especifica la línea de comandos de hello para la tarea de inicio de hello:</span><span class="sxs-lookup"><span data-stu-id="6eb57-142">**commandLine** - Specifies hello command line for hello startup task:</span></span>

* <span data-ttu-id="6eb57-143">comando de Hello, con los parámetros de línea de comandos opcionales, que comienza la tarea de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="6eb57-143">hello command, with optional command line parameters, which begins hello startup task.</span></span>
* <span data-ttu-id="6eb57-144">Con frecuencia, se trata de nombre de archivo de Hola de un archivo por lotes .bat o .cmd.</span><span class="sxs-lookup"><span data-stu-id="6eb57-144">Frequently this is hello filename of a .cmd or .bat batch file.</span></span>
* <span data-ttu-id="6eb57-145">tarea Hello es relativa toohello AppRoot\\carpeta Bin para la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="6eb57-145">hello task is relative toohello AppRoot\\Bin folder for hello deployment.</span></span> <span data-ttu-id="6eb57-146">No se expanden las variables de entorno para determinar la ruta de acceso de Hola y de tarea hello.</span><span class="sxs-lookup"><span data-stu-id="6eb57-146">Environment variables are not expanded in determining hello path and file of hello task.</span></span> <span data-ttu-id="6eb57-147">Si se requiere la expansión del entorno, puede crear un pequeño script .cmd que llame a la tarea de inicio.</span><span class="sxs-lookup"><span data-stu-id="6eb57-147">If environment expansion is required, you can create a small .cmd script that calls your startup task.</span></span>
* <span data-ttu-id="6eb57-148">Puede ser una aplicación de consola o un archivo por lotes que inicie un [script de PowerShell](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).</span><span class="sxs-lookup"><span data-stu-id="6eb57-148">Can be a console application or a batch file that starts a [PowerShell script](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).</span></span>

<span data-ttu-id="6eb57-149">**executionContext** -especifica el nivel de privilegio de hello para la tarea de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="6eb57-149">**executionContext** - Specifies hello privilege level for hello startup task.</span></span> <span data-ttu-id="6eb57-150">nivel de privilegio de Hello puede limitado o con permisos elevado:</span><span class="sxs-lookup"><span data-stu-id="6eb57-150">hello privilege level can be limited or elevated:</span></span>

* <span data-ttu-id="6eb57-151">**limited**</span><span class="sxs-lookup"><span data-stu-id="6eb57-151">**limited**</span></span>  
  <span data-ttu-id="6eb57-152">tarea de inicio de Hola se ejecuta con hello mismo privilegios como rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="6eb57-152">hello startup task runs with hello same privileges as hello role.</span></span> <span data-ttu-id="6eb57-153">Cuando Hola **executionContext** atributo para hello [en tiempo de ejecución] elemento también es **limitado**, a continuación, se utilizan los privilegios de usuario.</span><span class="sxs-lookup"><span data-stu-id="6eb57-153">When hello **executionContext** attribute for hello [Runtime] element is also **limited**, then user privileges are used.</span></span>
* <span data-ttu-id="6eb57-154">**elevated**</span><span class="sxs-lookup"><span data-stu-id="6eb57-154">**elevated**</span></span>  
  <span data-ttu-id="6eb57-155">tarea de inicio de Hola se ejecuta con privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="6eb57-155">hello startup task runs with administrator privileges.</span></span> <span data-ttu-id="6eb57-156">Esto permite que las tareas de inicio programas tooinstall, realizar cambios de configuración de IIS, realizar cambios en el registro y otras tareas de nivel de administrador, sin aumentar el nivel de privilegio de Hola de propio rol Hola.</span><span class="sxs-lookup"><span data-stu-id="6eb57-156">This allows startup tasks tooinstall programs, make IIS configuration changes, perform registry changes, and other administrator level tasks, without increasing hello privilege level of hello role itself.</span></span>  

> [!NOTE]
> <span data-ttu-id="6eb57-157">Hello nivel de privilegio de una tarea de inicio no es necesario toobe Hola mismo como el propio rol Hola.</span><span class="sxs-lookup"><span data-stu-id="6eb57-157">hello privilege level of a startup task does not need toobe hello same as hello role itself.</span></span>
> 
> 

<span data-ttu-id="6eb57-158">**taskType** -especifica Hola forma una tarea de inicio se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="6eb57-158">**taskType** - Specifies hello way a startup task is executed.</span></span>

* <span data-ttu-id="6eb57-159">**simple**</span><span class="sxs-lookup"><span data-stu-id="6eb57-159">**simple**</span></span>  
  <span data-ttu-id="6eb57-160">Las tareas se ejecutan sincrónicamente, especifique uno a la vez, en orden de hello en hello [ServiceDefinition.csdef] archivo.</span><span class="sxs-lookup"><span data-stu-id="6eb57-160">Tasks are executed synchronously, one at a time, in hello order specified in hello [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="6eb57-161">Cuando una **simple** tarea de inicio finaliza con un **errorlevel** de cero, a continuación Hola **simple** se ejecuta la tarea de inicio.</span><span class="sxs-lookup"><span data-stu-id="6eb57-161">When one **simple** startup task ends with an **errorlevel** of zero, hello next **simple** startup task is executed.</span></span> <span data-ttu-id="6eb57-162">Si hay más **simple** tooexecute, las tareas de inicio, a continuación, se iniciará el propio rol Hola.</span><span class="sxs-lookup"><span data-stu-id="6eb57-162">If there are no more **simple** startup tasks tooexecute, then hello role itself will be started.</span></span>   
  
  > [!NOTE]
  > <span data-ttu-id="6eb57-163">Si hello **simple** tarea finaliza con un elemento que es distinto de cero **errorlevel**, instancia de Hola se bloqueará.</span><span class="sxs-lookup"><span data-stu-id="6eb57-163">If hello **simple** task ends with a non-zero **errorlevel**, hello instance will be blocked.</span></span> <span data-ttu-id="6eb57-164">Posteriores **simple** las tareas de inicio y el rol de hello, no se iniciarán.</span><span class="sxs-lookup"><span data-stu-id="6eb57-164">Subsequent **simple** startup tasks, and hello role itself, will not start.</span></span>
  > 
  > 
  
    <span data-ttu-id="6eb57-165">tooensure que el archivo por lotes finaliza con un **errorlevel** de cero, ejecute el comando hello `EXIT /B 0` final Hola de su proceso de archivo por lotes.</span><span class="sxs-lookup"><span data-stu-id="6eb57-165">tooensure that your batch file ends with an **errorlevel** of zero, execute hello command `EXIT /B 0` at hello end of your batch file process.</span></span>
* <span data-ttu-id="6eb57-166">**background**</span><span class="sxs-lookup"><span data-stu-id="6eb57-166">**background**</span></span>  
  <span data-ttu-id="6eb57-167">Las tareas se ejecutan de forma asincrónica, en paralelo con inicio de Hola de rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="6eb57-167">Tasks are executed asynchronously, in parallel with hello startup of hello role.</span></span>
* <span data-ttu-id="6eb57-168">**foreground**</span><span class="sxs-lookup"><span data-stu-id="6eb57-168">**foreground**</span></span>  
  <span data-ttu-id="6eb57-169">Las tareas se ejecutan de forma asincrónica, en paralelo con inicio de Hola de rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="6eb57-169">Tasks are executed asynchronously, in parallel with hello startup of hello role.</span></span> <span data-ttu-id="6eb57-170">Hola diferencia clave entre un **primer plano** y un **fondo** tarea es que un **primer plano** tarea impide que el rol Hola de reciclaje o el cierre hasta que tenga la tarea hello ha finalizado.</span><span class="sxs-lookup"><span data-stu-id="6eb57-170">hello key difference between a **foreground** and a **background** task is that a **foreground** task prevents hello role from recycling or shutting down until hello task has ended.</span></span> <span data-ttu-id="6eb57-171">Hola **fondo** las tareas no tienen esta restricción.</span><span class="sxs-lookup"><span data-stu-id="6eb57-171">hello **background** tasks do not have this restriction.</span></span>

## <a name="environment-variables"></a><span data-ttu-id="6eb57-172">Variables de entorno</span><span class="sxs-lookup"><span data-stu-id="6eb57-172">Environment variables</span></span>
<span data-ttu-id="6eb57-173">Las variables de entorno son una tarea de inicio de manera toopass información tooa.</span><span class="sxs-lookup"><span data-stu-id="6eb57-173">Environment variables are a way toopass information tooa startup task.</span></span> <span data-ttu-id="6eb57-174">Por ejemplo, puede colocar el blob de tooa de ruta de acceso de Hola que contiene un tooinstall de programa, o números de puerto que usará el rol o características de toocontrol de configuración de la tarea de inicio.</span><span class="sxs-lookup"><span data-stu-id="6eb57-174">For example, you can put hello path tooa blob that contains a program tooinstall, or port numbers that your role will use, or settings toocontrol features of your startup task.</span></span>

<span data-ttu-id="6eb57-175">Hay dos tipos de variables de entorno para las tareas de inicio; variables de entorno estáticas y variables de entorno basan en los miembros de hello [ RoleEnvironment] clase.</span><span class="sxs-lookup"><span data-stu-id="6eb57-175">There are two kinds of environment variables for startup tasks; static environment variables and environment variables based on members of hello [RoleEnvironment] class.</span></span> <span data-ttu-id="6eb57-176">Ambos están en hello [entorno] sección de hello [ServiceDefinition.csdef] ambos hello de uso y de archivo [ Variable] elemento y **nombre** atributo.</span><span class="sxs-lookup"><span data-stu-id="6eb57-176">Both are in hello [Environment] section of hello [ServiceDefinition.csdef] file, and both use hello [Variable] element and **name** attribute.</span></span>

<span data-ttu-id="6eb57-177">Hola de usos de variables de entorno estáticas **valor** atributo de hello [ Variable] elemento.</span><span class="sxs-lookup"><span data-stu-id="6eb57-177">Static environment variables uses hello **value** attribute of hello [Variable] element.</span></span> <span data-ttu-id="6eb57-178">ejemplo de Hola anterior crea la variable de entorno de hello **MyVersionNumber** que tiene un valor estático de "**1.0.0.0**".</span><span class="sxs-lookup"><span data-stu-id="6eb57-178">hello example above creates hello environment variable **MyVersionNumber** which has a static value of "**1.0.0.0**".</span></span> <span data-ttu-id="6eb57-179">Otro ejemplo sería toocreate una **StagingOrProduction** variable de entorno que puede establecer manualmente las toovalues de "**de ensayo**"o"**producción**" tooperform acciones de inicio diferentes basadas en valor Hola de hello **StagingOrProduction** variable de entorno.</span><span class="sxs-lookup"><span data-stu-id="6eb57-179">Another example would be toocreate a **StagingOrProduction** environment variable which you can manually set toovalues of "**staging**" or "**production**" tooperform different startup actions based on hello value of hello **StagingOrProduction** environment variable.</span></span>

<span data-ttu-id="6eb57-180">Las variables de entorno en función de los miembros del programa Hola a clase RoleEnvironment no utilizan Hola **valor** atributo de hello [ Variable] elemento.</span><span class="sxs-lookup"><span data-stu-id="6eb57-180">Environment variables based on members of hello RoleEnvironment class do not use hello **value** attribute of hello [Variable] element.</span></span> <span data-ttu-id="6eb57-181">En su lugar, Hola [RoleInstanceValue] elemento secundario, con hello adecuado **XPath** valor de atributo, es toocreate usa una variable de entorno en función de un miembro concreto de hello [ RoleEnvironment] clase.</span><span class="sxs-lookup"><span data-stu-id="6eb57-181">Instead, hello [RoleInstanceValue] child element, with hello appropriate **XPath** attribute value, are used toocreate an environment variable based on a specific member of hello [RoleEnvironment] class.</span></span> <span data-ttu-id="6eb57-182">Valores de hello **XPath** atributo tooaccess varios [ RoleEnvironment] valores se pueden encontrar [aquí](cloud-services-role-config-xpath.md).</span><span class="sxs-lookup"><span data-stu-id="6eb57-182">Values for hello **XPath** attribute tooaccess various [RoleEnvironment] values can be found [here](cloud-services-role-config-xpath.md).</span></span>

<span data-ttu-id="6eb57-183">Toocreate por ejemplo, una variable de entorno que es "**true**" cuando se ejecuta la instancia de hello en el emulador de proceso de hello, y "**false**" cuando se ejecuta en la nube de hello, utilice el siguiente de hello [ Variable] y [RoleInstanceValue] elementos:</span><span class="sxs-lookup"><span data-stu-id="6eb57-183">For example, toocreate an environment variable that is "**true**" when hello instance is running in hello compute emulator, and "**false**" when running in hello cloud, use hello following [Variable] and [RoleInstanceValue] elements:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>

            <!-- Create hello environment variable that informs hello startup task whether it is running
                in hello Compute Emulator or in hello cloud. "%ComputeEmulatorRunning%"=="true" when
                running in hello Compute Emulator, "%ComputeEmulatorRunning%"=="false" when running
                in hello cloud. -->

            <Variable name="ComputeEmulatorRunning">
                <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
            </Variable>

        </Environment>
    </Task>
</Startup>
```

## <a name="next-steps"></a><span data-ttu-id="6eb57-184">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6eb57-184">Next steps</span></span>
<span data-ttu-id="6eb57-185">Obtenga información acerca de cómo tooperform algunos [tareas comunes de inicio](cloud-services-startup-tasks-common.md) con su servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="6eb57-185">Learn how tooperform some [common startup tasks](cloud-services-startup-tasks-common.md) with your Cloud Service.</span></span>

<span data-ttu-id="6eb57-186">[Empaquete](cloud-services-model-and-package.md) el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="6eb57-186">[Package](cloud-services-model-and-package.md) your Cloud Service.</span></span>  

[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef
[tarea]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task
[inicio]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[en tiempo de ejecución]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
[entorno]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment
[ Variable]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
[ RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
