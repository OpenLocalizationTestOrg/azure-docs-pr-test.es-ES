---
title: una nube servicio localmente en hello emulador de proceso aaaProfiling | Documentos de Microsoft
services: cloud-services
description: Investigar los problemas de rendimiento en servicios en la nube con el generador de perfiles de Visual Studio Hola
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
tags: 
ms.assetid: 25e40bf3-eea0-4b0b-9f4a-91ffe797f6c3
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: fc37c85dad4db4cc0310f73afad56fc0fe5f3963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="testing-hello-performance-of-a-cloud-service-locally-in-hello-azure-compute-emulator-using-hello-visual-studio-profiler"></a><span data-ttu-id="190b0-103">Hola prueba de rendimiento de un servicio en la nube de forma local en Hola Hola emulador de proceso de Azure con el generador de perfiles de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="190b0-103">Testing hello Performance of a Cloud Service Locally in hello Azure Compute Emulator Using hello Visual Studio Profiler</span></span>
<span data-ttu-id="190b0-104">Una variedad de herramientas y técnicas están disponibles para probar el rendimiento de hello de servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="190b0-104">A variety of tools and techniques are available for testing hello performance of cloud services.</span></span>
<span data-ttu-id="190b0-105">Cuando se publica un tooAzure de servicio de nube, puede tener Visual Studio recopilar datos de generación de perfiles y, a continuación, analizarla localmente, como se describe en [generación de perfiles de una aplicación de Azure][1].</span><span class="sxs-lookup"><span data-stu-id="190b0-105">When you publish a cloud service tooAzure, you can have Visual Studio collect profiling data and then analyze it locally, as described in [Profiling an Azure Application][1].</span></span>
<span data-ttu-id="190b0-106">También puede utilizar tootrack de diagnóstico de los contadores de una variedad de rendimiento, como se describe en [mediante contadores de rendimiento en Azure][2].</span><span class="sxs-lookup"><span data-stu-id="190b0-106">You can also use diagnostics tootrack a variety of performance counters, as described in [Using performance counters in Azure][2].</span></span>
<span data-ttu-id="190b0-107">Puede que le interese tooprofile la aplicación localmente en el emulador de proceso de hello antes de implementarla en la nube toohello.</span><span class="sxs-lookup"><span data-stu-id="190b0-107">You might also want tooprofile your application locally in hello compute emulator before deploying it toohello cloud.</span></span>

<span data-ttu-id="190b0-108">Este artículo trata el método de muestreo de la CPU de Hola de generación de perfiles, que puede realizarse localmente en el emulador de Hola.</span><span class="sxs-lookup"><span data-stu-id="190b0-108">This article covers hello CPU Sampling method of profiling, which can be done locally in hello emulator.</span></span> <span data-ttu-id="190b0-109">El muestreo de CPU es un método para generar perfiles que no es muy intrusivo.</span><span class="sxs-lookup"><span data-stu-id="190b0-109">CPU sampling is a method of profiling that is not very intrusive.</span></span> <span data-ttu-id="190b0-110">En un intervalo de muestreo designado, el generador de perfiles de hello toma una instantánea de pila de llamadas de Hola.</span><span class="sxs-lookup"><span data-stu-id="190b0-110">At a designated sampling interval, hello profiler takes a snapshot of hello call stack.</span></span> <span data-ttu-id="190b0-111">datos de Hola se recopilan durante un período de tiempo y se muestra en un informe.</span><span class="sxs-lookup"><span data-stu-id="190b0-111">hello data is collected over a period of time, and shown in a report.</span></span> <span data-ttu-id="190b0-112">Este método de generación de perfiles suele tooindicate donde en una aplicación de cálculo intensiva de trabajo de hello CPU que se realiza la mayor parte.</span><span class="sxs-lookup"><span data-stu-id="190b0-112">This method of profiling tends tooindicate where in a computationally intensive application most of hello CPU work is being done.</span></span>  <span data-ttu-id="190b0-113">Esto deja Hola toofocus oportunidad en hello "ruta de acceso activa", donde la aplicación está dedicando Hola mayor parte del tiempo.</span><span class="sxs-lookup"><span data-stu-id="190b0-113">This gives you hello opportunity toofocus on hello "hot path" where your application is spending hello most time.</span></span>

## <a name="1-configure-visual-studio-for-profiling"></a><span data-ttu-id="190b0-114">1: Configuración de Visual Studio para la generación de perfiles</span><span class="sxs-lookup"><span data-stu-id="190b0-114">1: Configure Visual Studio for profiling</span></span>
<span data-ttu-id="190b0-115">Primero, existen unas pocas opciones de configuración de Visual Studio que podrían ser útiles para la generación de perfiles.</span><span class="sxs-lookup"><span data-stu-id="190b0-115">First, there are a few Visual Studio configuration options that might be helpful when profiling.</span></span> <span data-ttu-id="190b0-116">Hola de sentido toomake de informes de generación de perfiles, necesitará símbolos (archivos .pdb) para la aplicación y también los símbolos para las bibliotecas del sistema.</span><span class="sxs-lookup"><span data-stu-id="190b0-116">toomake sense of hello profiling reports, you'll need symbols (.pdb files) for your application and also symbols for system libraries.</span></span> <span data-ttu-id="190b0-117">Es conveniente que se haga referencia a los servidores de símbolos disponibles de hello toomake.</span><span class="sxs-lookup"><span data-stu-id="190b0-117">You'll want toomake sure that you reference hello available symbol servers.</span></span> <span data-ttu-id="190b0-118">toodo esto en hello **herramientas** menú en Visual Studio, elija **opciones**, a continuación, elija **depuración**, a continuación, **símbolos**.</span><span class="sxs-lookup"><span data-stu-id="190b0-118">toodo this, on hello **Tools** menu in Visual Studio, choose **Options**, then choose **Debugging**, then **Symbols**.</span></span> <span data-ttu-id="190b0-119">Asegúrese de que los servidores de símbolos de Microsoft aparezcan en **Ubicaciones del archivo de símbolos (.pdb)**.</span><span class="sxs-lookup"><span data-stu-id="190b0-119">Make sure that Microsoft Symbol Servers is listed under **Symbol file (.pdb) locations**.</span></span>  <span data-ttu-id="190b0-120">Puede también hacer referencia a http://referencesource.microsoft.com/symbols, el cual podría tener archivos de símbolo adicionales.</span><span class="sxs-lookup"><span data-stu-id="190b0-120">You can also reference http://referencesource.microsoft.com/symbols, which might have additional symbol files.</span></span>

![Opciones Símbolo][4]

<span data-ttu-id="190b0-122">Si lo desea, puede simplificar Hola notifica ese generador de perfiles de hello genera estableciendo solo mi código.</span><span class="sxs-lookup"><span data-stu-id="190b0-122">If desired, you can simplify hello reports that hello profiler generates by setting Just My Code.</span></span> <span data-ttu-id="190b0-123">Con sólo mi código habilitada, se simplifican las pilas de llamadas de función por lo que llama a toolibraries completamente interno y Hola .NET Framework están ocultos en informes de Hola.</span><span class="sxs-lookup"><span data-stu-id="190b0-123">With Just My Code enabled, function call stacks are simplified so that calls entirely internal toolibraries and hello .NET Framework are hidden from hello reports.</span></span> <span data-ttu-id="190b0-124">En hello **herramientas** menú, elija **opciones**.</span><span class="sxs-lookup"><span data-stu-id="190b0-124">On hello **Tools** menu, choose **Options**.</span></span> <span data-ttu-id="190b0-125">A continuación, expanda hello **herramientas de rendimiento** nodo y elija **General**.</span><span class="sxs-lookup"><span data-stu-id="190b0-125">Then expand hello **Performance Tools** node, and choose **General**.</span></span> <span data-ttu-id="190b0-126">Casilla de Hola de **habilitar solo mi código para los informes del generador de perfiles**.</span><span class="sxs-lookup"><span data-stu-id="190b0-126">Select hello checkbox for **Enable Just My Code for profiler reports**.</span></span>

![Opciones Solo mi código][17]

<span data-ttu-id="190b0-128">Puede usar estas instrucciones con un proyecto existente o con un proyecto nuevo.</span><span class="sxs-lookup"><span data-stu-id="190b0-128">You can use these instructions with an existing project or with a new project.</span></span>  <span data-ttu-id="190b0-129">Si crea un nuevo hello tootry de proyecto técnicas que se describen a continuación, elija una de C# **servicio de nube de Azure** de proyecto y seleccione un **rol Web** y un **rol de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="190b0-129">If you create a new project tootry hello techniques described below, choose a C# **Azure Cloud Service** project, and select a **Web Role** and a **Worker Role**.</span></span>

![Roles de proyecto del servicio en la nube de Azure][5]

<span data-ttu-id="190b0-131">Por ejemplo, efectos, agregar algún proyecto de código tooyour que tarda mucho tiempo y se muestra algún problema de rendimiento evidente.</span><span class="sxs-lookup"><span data-stu-id="190b0-131">For example purposes, add some code tooyour project that takes a lot of time and demonstrates some obvious performance problem.</span></span> <span data-ttu-id="190b0-132">Por ejemplo, agregar Hola después de proyecto de rol de trabajo de código tooa:</span><span class="sxs-lookup"><span data-stu-id="190b0-132">For example, add hello following code tooa worker role project:</span></span>

    public class Concatenator
    {
        public static string Concatenate(int number)
        {
            int count;
            string s = "";
            for (count = 0; count < number; count++)
            {
                s += "\n" + count.ToString();
            }
            return s;
        }
    }

<span data-ttu-id="190b0-133">Llamar a este código de hello Coredispatcher método en clase derivada de RoleEntryPoint del rol de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="190b0-133">Call this code from hello RunAsync method in hello worker role's RoleEntryPoint-derived class.</span></span> <span data-ttu-id="190b0-134">(Omitir la advertencia Hola sobre método hello que se ejecuta de forma sincrónica).</span><span class="sxs-lookup"><span data-stu-id="190b0-134">(Ignore hello warning about hello method running synchronously.)</span></span>

        private async Task RunAsync(CancellationToken cancellationToken)
        {
            // TODO: Replace hello following with your own logic.
            while (!cancellationToken.IsCancellationRequested)
            {
                Trace.TraceInformation("Working");
                Concatenator.Concatenate(10000);
            }
        }

<span data-ttu-id="190b0-135">Compilar y ejecutar su servicio en la nube localmente sin depurar (CTRL+F5), con la configuración de solución de hello establecido demasiado**versión**.</span><span class="sxs-lookup"><span data-stu-id="190b0-135">Build and run your cloud service locally without debugging (Ctrl+F5), with hello solution configuration set too**Release**.</span></span> <span data-ttu-id="190b0-136">Esto garantiza que todos los archivos y carpetas se crean para ejecutar la aplicación hello localmente y se asegura de que se hayan iniciado todos los emuladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="190b0-136">This ensures that all files and folders are created for running hello application locally, and ensures that all hello emulators are started.</span></span> <span data-ttu-id="190b0-137">Iniciar Hola IU del emulador de proceso de hello tooverify de barra de tareas que se ejecuta el rol de trabajo.</span><span class="sxs-lookup"><span data-stu-id="190b0-137">Start hello Compute Emulator UI from hello taskbar tooverify that your worker role is running.</span></span>

## <a name="2-attach-tooa-process"></a><span data-ttu-id="190b0-138">2: asociar un proceso de tooa</span><span class="sxs-lookup"><span data-stu-id="190b0-138">2: Attach tooa process</span></span>
<span data-ttu-id="190b0-139">En lugar de generación de perfiles de aplicación hello, empiece por hello IDE de Visual Studio 2010, debe adjuntar Hola profiler tooa Ejecutar proceso.</span><span class="sxs-lookup"><span data-stu-id="190b0-139">Instead of profiling hello application by starting it from hello Visual Studio 2010 IDE, you must attach hello profiler tooa running process.</span></span> 

<span data-ttu-id="190b0-140">proceso de tooa de tooattach Hola generador de perfiles, en hello **analizar** menú, elija **Profiler** y **adjuntar y separar**.</span><span class="sxs-lookup"><span data-stu-id="190b0-140">tooattach hello profiler tooa process, on hello **Analyze** menu, choose **Profiler** and **Attach/Detach**.</span></span>

![Opción para adjuntar perfil][6]

<span data-ttu-id="190b0-142">Para un rol de trabajo, busque el proceso de WaWorkerHost.exe de Hola.</span><span class="sxs-lookup"><span data-stu-id="190b0-142">For a worker role, find hello WaWorkerHost.exe process.</span></span>

![Proceso WaWorkerHost][7]

<span data-ttu-id="190b0-144">Si la carpeta del proyecto está en una unidad de red, el generador de perfiles de hello le preguntará si tooprovide Hola de toosave otra ubicación informes de generación de perfiles.</span><span class="sxs-lookup"><span data-stu-id="190b0-144">If your project folder is on a network drive, hello profiler will ask you tooprovide another location toosave hello profiling reports.</span></span>

 <span data-ttu-id="190b0-145">También puede adjuntar el rol web de tooa adjuntando tooWaIISHost.exe.</span><span class="sxs-lookup"><span data-stu-id="190b0-145">You can also attach tooa web role by attaching tooWaIISHost.exe.</span></span>
<span data-ttu-id="190b0-146">Si hay varios procesos de rol de trabajo en la aplicación, necesita toouse Hola processID toodistinguish ellos.</span><span class="sxs-lookup"><span data-stu-id="190b0-146">If there are multiple worker role processes in your application, you need toouse hello processID toodistinguish them.</span></span> <span data-ttu-id="190b0-147">Puede consultar Hola processID mediante programación mediante el acceso a objetos de proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="190b0-147">You can query hello processID programmatically by accessing hello Process object.</span></span> <span data-ttu-id="190b0-148">Por ejemplo, si agrega este método de ejecución de código toohello de clase derivada de RoleEntryPoint de hello en un rol, se puede volver en el registro en hello IU del emulador de proceso tooknow qué tooconnect de proceso a.</span><span class="sxs-lookup"><span data-stu-id="190b0-148">For example, if you add this code toohello Run method of hello RoleEntryPoint-derived class in a role, you can look at the log in hello Compute Emulator UI tooknow what process tooconnect to.</span></span>

    var process = System.Diagnostics.Process.GetCurrentProcess();
    var message = String.Format("Process ID: {0}", process.Id);
    Trace.WriteLine(message, "Information");

<span data-ttu-id="190b0-149">registro de hello tooview, Hola IU del emulador de proceso de inicio.</span><span class="sxs-lookup"><span data-stu-id="190b0-149">tooview hello log, start hello Compute Emulator UI.</span></span>

![Iniciar Hola IU del emulador de proceso][8]

<span data-ttu-id="190b0-151">Abra la ventana de consola de registro de rol de trabajo de Hola Hola IU del emulador de proceso haciendo clic en la barra de título de la ventana de consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="190b0-151">Open hello worker role log console window in hello Compute Emulator UI by clicking on hello console window's title bar.</span></span> <span data-ttu-id="190b0-152">Puede ver el Id. de proceso de hello en el registro de hello.</span><span class="sxs-lookup"><span data-stu-id="190b0-152">You can see hello process ID in hello log.</span></span>

![Visualización del identificador de proceso][9]

<span data-ttu-id="190b0-154">Uno que ha adjuntado, siga los pasos de hello en escenario de Hola de tooreproduce de interfaz de usuario (si es necesario) de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="190b0-154">One you've attached, perform hello steps in your application's UI (if needed) tooreproduce hello scenario.</span></span>

<span data-ttu-id="190b0-155">Si desea toostop de generación de perfiles, elija hello **detener la generación de perfiles** vínculo.</span><span class="sxs-lookup"><span data-stu-id="190b0-155">When you want toostop profiling, choose hello **Stop Profiling** link.</span></span>

![Opción Detener generación de perfiles][10]

## <a name="3-view-performance-reports"></a><span data-ttu-id="190b0-157">3: Vista de informes de rendimiento</span><span class="sxs-lookup"><span data-stu-id="190b0-157">3: View performance reports</span></span>
<span data-ttu-id="190b0-158">se muestra el informe de rendimiento de Hello para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="190b0-158">hello performance report for your application is displayed.</span></span>

<span data-ttu-id="190b0-159">En este momento, el generador de perfiles de hello deja de ejecutarse, guarda los datos en un archivo .vsp y muestra un informe que muestra un análisis de los datos.</span><span class="sxs-lookup"><span data-stu-id="190b0-159">At this point, hello profiler stops executing, saves data in a .vsp file, and displays a report that shows an analysis of this data.</span></span>

![Informe del generador de perfiles][11]

<span data-ttu-id="190b0-161">Si ve String.wstrcpy en Hola ruta de acceso activa, haga clic en sólo mi código toochange Hola vista tooshow código de usuario solo.</span><span class="sxs-lookup"><span data-stu-id="190b0-161">If you see String.wstrcpy in hello Hot Path, click on Just My Code toochange hello view tooshow user code only.</span></span>  <span data-ttu-id="190b0-162">Si ve String.Concat, pruebe a presionar el botón Mostrar todo el código de hello.</span><span class="sxs-lookup"><span data-stu-id="190b0-162">If you see String.Concat, try pressing hello Show All Code button.</span></span>

<span data-ttu-id="190b0-163">Debería ver método concatenación de hello y String.Concat ocupa una gran parte del tiempo de ejecución de Hola.</span><span class="sxs-lookup"><span data-stu-id="190b0-163">You should see hello Concatenate method and String.Concat taking up a large portion of hello execution time.</span></span>

![Análisis del informe][12]

<span data-ttu-id="190b0-165">Si agrega código de concatenación de cadena de hello en este artículo, verá una advertencia en la lista de tareas de Hola para esto.</span><span class="sxs-lookup"><span data-stu-id="190b0-165">If you added hello string concatenation code in this article, you should see a warning in hello Task List for this.</span></span> <span data-ttu-id="190b0-166">También puede ver una advertencia que hay una cantidad excesiva de recolección de elementos, que es de vencimiento toohello número de cadenas que se crean y se eliminan.</span><span class="sxs-lookup"><span data-stu-id="190b0-166">You may also see a warning that there is an excessive amount of garbage collection, which is due toohello number of strings that are created and disposed.</span></span>

![Advertencias de rendimiento][14]

## <a name="4-make-changes-and-compare-performance"></a><span data-ttu-id="190b0-168">4: Realización de cambios y comparación del rendimiento</span><span class="sxs-lookup"><span data-stu-id="190b0-168">4: Make changes and compare performance</span></span>
<span data-ttu-id="190b0-169">También puede comparar el rendimiento de hello antes y después de un cambio en el código.</span><span class="sxs-lookup"><span data-stu-id="190b0-169">You can also compare hello performance before and after a code change.</span></span>  <span data-ttu-id="190b0-170">Detener Hola Ejecutar proceso y editar Hola código tooreplace Hola cadena operación de concatenación con el uso de Hola de StringBuilder:</span><span class="sxs-lookup"><span data-stu-id="190b0-170">Stop hello running process, and edit hello code tooreplace hello string concatenation operation with hello use of StringBuilder:</span></span>

    public static string Concatenate(int number)
    {
        int count;
        System.Text.StringBuilder builder = new System.Text.StringBuilder("");
        for (count = 0; count < number; count++)
        {
             builder.Append("\n" + count.ToString());
        }
        return builder.ToString();
    }

<span data-ttu-id="190b0-171">Realice otra ejecución de rendimiento y, a continuación, comparar el rendimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="190b0-171">Do another performance run, and then compare hello performance.</span></span> <span data-ttu-id="190b0-172">En el Explorador de rendimiento de hello, si hello ejecuciones estarán en hello misma sesión, solo puede seleccionar ambos informes, abra el menú contextual de Hola y elija **comparar informes de rendimiento**.</span><span class="sxs-lookup"><span data-stu-id="190b0-172">In hello Performance Explorer, if hello runs are in hello same session, you can just select both reports, open hello shortcut menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="190b0-173">Si desea toocompare con una ejecución en otra sesión de rendimiento, abra hello **analizar** menú y elija **comparar informes de rendimiento**.</span><span class="sxs-lookup"><span data-stu-id="190b0-173">If you want toocompare with a run in another performance session, open hello **Analyze** menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="190b0-174">Especifique ambos archivos en el cuadro de diálogo de Hola que aparece.</span><span class="sxs-lookup"><span data-stu-id="190b0-174">Specify both files in hello dialog box that appears.</span></span>

![Opción para comparar informes de rendimiento][15]

<span data-ttu-id="190b0-176">informes de Hello resalta las diferencias entre dos ejecuciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="190b0-176">hello reports highlight differences between hello two runs.</span></span>

![Informe de comparación][16]

<span data-ttu-id="190b0-178">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="190b0-178">Congratulations!</span></span> <span data-ttu-id="190b0-179">Haya empezado con el generador de perfiles de Hola.</span><span class="sxs-lookup"><span data-stu-id="190b0-179">You've gotten started with hello profiler.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="190b0-180">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="190b0-180">Troubleshooting</span></span>
* <span data-ttu-id="190b0-181">Asegúrese de que va a generar un perfil de una compilación de versión e iniciar sin depuración.</span><span class="sxs-lookup"><span data-stu-id="190b0-181">Make sure you are profiling a Release build and start without debugging.</span></span>
* <span data-ttu-id="190b0-182">Si Hola adjuntar y separar opción no está habilitada en el menú del generador de perfiles de hello, ejecute hello Asistente de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="190b0-182">If hello Attach/Detach option is not enabled on hello Profiler menu, run hello Performance Wizard.</span></span>
* <span data-ttu-id="190b0-183">Utilice Hola IU del emulador de proceso tooview Hola estado de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="190b0-183">Use hello Compute Emulator UI tooview hello status of your application.</span></span> 
* <span data-ttu-id="190b0-184">Si tiene problemas para iniciar aplicaciones en el emulador de Hola o adjuntar Hola generador de perfiles, apague el emulador de proceso de Hola y reiniciarlo.</span><span class="sxs-lookup"><span data-stu-id="190b0-184">If you have problems starting applications in hello emulator, or attaching hello profiler, shut down hello compute emulator and restart it.</span></span> <span data-ttu-id="190b0-185">Si no se soluciona el problema de hello, pruebe a reiniciar.</span><span class="sxs-lookup"><span data-stu-id="190b0-185">If that doesn't solve hello problem, try rebooting.</span></span> <span data-ttu-id="190b0-186">Este problema puede producirse si usa toosuspend de emulador de proceso de Hola y quitar las implementaciones de ejecución.</span><span class="sxs-lookup"><span data-stu-id="190b0-186">This problem can occur if you use hello Compute Emulator toosuspend and remove running deployments.</span></span>
* <span data-ttu-id="190b0-187">Si ha usado alguna de hello comandos desde la línea de comandos de generación de perfiles, especialmente Hola configuración global, asegúrese de que se ha llamado VSPerfClrEnv /globaloff y que se haya apagado VsPerfMon.exe.</span><span class="sxs-lookup"><span data-stu-id="190b0-187">If you have used any of hello profiling commands from the command line, especially hello global settings, make sure that VSPerfClrEnv /globaloff has been called and that VsPerfMon.exe has been shut down.</span></span>
* <span data-ttu-id="190b0-188">Si durante el muestreo, verá un mensaje de saludo "PRF0025: No se recopilaron datos," Compruebe que Hola adjunta actividad toohas CPU de proceso.</span><span class="sxs-lookup"><span data-stu-id="190b0-188">If when sampling, you see hello message "PRF0025: No data was collected," check that hello process you attached toohas CPU activity.</span></span> <span data-ttu-id="190b0-189">Es posible que las aplicaciones que no están realizando ningún trabajo informático no produzcan datos de muestreo.</span><span class="sxs-lookup"><span data-stu-id="190b0-189">Applications that are not doing any computational work might not produce any sampling data.</span></span>  <span data-ttu-id="190b0-190">También es posible que el proceso de hello terminado antes de realiza cualquier muestreo.</span><span class="sxs-lookup"><span data-stu-id="190b0-190">It's also possible that hello process exited before any sampling was done.</span></span> <span data-ttu-id="190b0-191">No termina con toosee de comprobación que Hola método Run a un rol que está generando perfiles.</span><span class="sxs-lookup"><span data-stu-id="190b0-191">Check toosee that hello Run method for a role that you are profiling does not terminate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="190b0-192">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="190b0-192">Next Steps</span></span>
<span data-ttu-id="190b0-193">No se admite la instrumentación de los binarios de Azure en el emulador de hello en el generador de perfiles de Visual Studio de hello, pero si desea que la asignación de memoria tootest, puede elegir esa opción cuando la generación de perfiles.</span><span class="sxs-lookup"><span data-stu-id="190b0-193">Instrumenting Azure binaries in hello emulator is not supported in hello Visual Studio profiler, but if you want tootest memory allocation, you can choose that option when profiling.</span></span> <span data-ttu-id="190b0-194">También puede generar perfiles de simultaneidad, que le ayuda a determinar si los subprocesos desaprovechan tiempo compiten por los bloqueos, o de nivel de generación de perfiles de interacción, que le ayudará a realizar un seguimiento de problemas de rendimiento al interactuar entre las capas de una aplicación, más con frecuencia entre la capa de datos de Hola y un rol de trabajo.</span><span class="sxs-lookup"><span data-stu-id="190b0-194">You can also choose concurrency profiling, which helps you determine whether threads are wasting time competing for locks, or tier interaction profiling, which helps you track down performance problems when interacting between tiers of an application, most frequently between hello data tier and a worker role.</span></span>  <span data-ttu-id="190b0-195">Puede ver las consultas de base de datos de Hola que genera la aplicación y usar hello generación de perfiles de datos tooimprove el uso de la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="190b0-195">You can view hello database queries that your app generates and use hello profiling data tooimprove your use of hello database.</span></span> <span data-ttu-id="190b0-196">Para obtener información sobre la generación de perfiles de interacción de capas, consulte el blog de hello [Tutorial: usar Hola generador de perfiles de interacción de capa de Visual Studio Team System 2010][3].</span><span class="sxs-lookup"><span data-stu-id="190b0-196">For information about tier interaction profiling, see hello blog post [Walkthrough: Using hello Tier Interaction Profiler in Visual Studio Team System 2010][3].</span></span>

[1]: http://msdn.microsoft.com/library/azure/hh369930.aspx
[2]: http://msdn.microsoft.com/library/azure/hh411542.aspx
[3]: http://blogs.msdn.com/b/habibh/archive/2009/06/30/walkthrough-using-the-tier-interaction-profiler-in-visual-studio-team-system-2010.aspx
[4]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally09.png
[5]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally10.png
[6]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally02.png
[7]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally05.png
[8]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally010.png
[9]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally07.png
[10]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally06.png
[11]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally03.png
[12]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally011.png
[14]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally04.png 
[15]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally013.png
[16]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally012.png
[17]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally08.png
