---
title: "Generación del perfil de un servicio en la nube en modo local en el emulador de proceso | Microsoft Docs"
services: cloud-services
description: Investigar los problemas de rendimiento en servicios en la nube con el generador de perfiles de Visual Studio
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
ms.openlocfilehash: 51c8192d8312dc5cf546b4c357aeecf6f19d56b8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="testing-the-performance-of-a-cloud-service-locally-in-the-azure-compute-emulator-using-the-visual-studio-profiler"></a><span data-ttu-id="6ea4c-103">Prueba del rendimiento de un servicio en la nube de manera local en el emulador de proceso de Azure con el generador de perfiles de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6ea4c-103">Testing the Performance of a Cloud Service Locally in the Azure Compute Emulator Using the Visual Studio Profiler</span></span>
<span data-ttu-id="6ea4c-104">Se encuentran disponibles diversas herramientas y técnicas para probar el rendimiento de los servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-104">A variety of tools and techniques are available for testing the performance of cloud services.</span></span>
<span data-ttu-id="6ea4c-105">Al publicar un servicio en la nube en Azure, puede usar Visual Studio para recopilar datos para la generación de perfiles y, luego, analizarlos localmente, como se describe en [Generación de un perfil de una aplicación de Azure][1].</span><span class="sxs-lookup"><span data-stu-id="6ea4c-105">When you publish a cloud service to Azure, you can have Visual Studio collect profiling data and then analyze it locally, as described in [Profiling an Azure Application][1].</span></span>
<span data-ttu-id="6ea4c-106">También puede usar un diagnóstico para hacer un seguimiento de una amplia variedad de contadores de rendimiento, como se describe en [Uso de contadores de rendimiento en Azure][2].</span><span class="sxs-lookup"><span data-stu-id="6ea4c-106">You can also use diagnostics to track a variety of performance counters, as described in [Using performance counters in Azure][2].</span></span>
<span data-ttu-id="6ea4c-107">También es posible que desee generar un perfil de la aplicación localmente en el emulador de proceso antes de implementarlo en la nube.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-107">You might also want to profile your application locally in the compute emulator before deploying it to the cloud.</span></span>

<span data-ttu-id="6ea4c-108">Este artículo abarca el método de muestreo de CPU de la generación de perfiles, que se puede realizar localmente en el emulador.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-108">This article covers the CPU Sampling method of profiling, which can be done locally in the emulator.</span></span> <span data-ttu-id="6ea4c-109">El muestreo de CPU es un método para generar perfiles que no es muy intrusivo.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-109">CPU sampling is a method of profiling that is not very intrusive.</span></span> <span data-ttu-id="6ea4c-110">A un intervalo de muestreo designado, el generador de perfiles realiza una instantánea de la pila de llamadas.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-110">At a designated sampling interval, the profiler takes a snapshot of the call stack.</span></span> <span data-ttu-id="6ea4c-111">Los datos se recopilan por un lapso de tiempo y se muestran en un informe.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-111">The data is collected over a period of time, and shown in a report.</span></span> <span data-ttu-id="6ea4c-112">Este método de generación de perfiles tiende a indicar dónde se está realizando la mayoría del trabajo de la CPU en una aplicación informáticamente intensiva.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-112">This method of profiling tends to indicate where in a computationally intensive application most of the CPU work is being done.</span></span>  <span data-ttu-id="6ea4c-113">Esto le da la oportunidad de centrarse en la "ruta de acceso activa" donde su aplicación pasa la mayor parte del tiempo.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-113">This gives you the opportunity to focus on the "hot path" where your application is spending the most time.</span></span>

## <a name="1-configure-visual-studio-for-profiling"></a><span data-ttu-id="6ea4c-114">1: Configuración de Visual Studio para la generación de perfiles</span><span class="sxs-lookup"><span data-stu-id="6ea4c-114">1: Configure Visual Studio for profiling</span></span>
<span data-ttu-id="6ea4c-115">Primero, existen unas pocas opciones de configuración de Visual Studio que podrían ser útiles para la generación de perfiles.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-115">First, there are a few Visual Studio configuration options that might be helpful when profiling.</span></span> <span data-ttu-id="6ea4c-116">Para que los informes de generación de perfiles tengan sentido, necesitará símbolos (archivos .pdb) para su aplicación y también símbolos para las bibliotecas del sistema.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-116">To make sense of the profiling reports, you'll need symbols (.pdb files) for your application and also symbols for system libraries.</span></span> <span data-ttu-id="6ea4c-117">Necesitará asegurarse de que hace referencia a los servidores de símbolos disponibles.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-117">You'll want to make sure that you reference the available symbol servers.</span></span> <span data-ttu-id="6ea4c-118">Para hacer esto, en el menú **Herramientas** de Visual Studio, elija **Opciones** y, a continuación, elija **Depuración** y luego, **Símbolos**.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-118">To do this, on the **Tools** menu in Visual Studio, choose **Options**, then choose **Debugging**, then **Symbols**.</span></span> <span data-ttu-id="6ea4c-119">Asegúrese de que los servidores de símbolos de Microsoft aparezcan en **Ubicaciones del archivo de símbolos (.pdb)**.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-119">Make sure that Microsoft Symbol Servers is listed under **Symbol file (.pdb) locations**.</span></span>  <span data-ttu-id="6ea4c-120">Puede también hacer referencia a http://referencesource.microsoft.com/symbols, el cual podría tener archivos de símbolo adicionales.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-120">You can also reference http://referencesource.microsoft.com/symbols, which might have additional symbol files.</span></span>

![Opciones Símbolo][4]

<span data-ttu-id="6ea4c-122">Si lo desea, puede simplificar los informes que genera el generador de perfiles al configurar Solo mi código.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-122">If desired, you can simplify the reports that the profiler generates by setting Just My Code.</span></span> <span data-ttu-id="6ea4c-123">Si Solo mi código está habilitado, las pilas de llamadas de función se simplifican de modo que las llamadas que son completamente internas para las bibliotecas y el .NET Framework están ocultas de los informes.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-123">With Just My Code enabled, function call stacks are simplified so that calls entirely internal to libraries and the .NET Framework are hidden from the reports.</span></span> <span data-ttu-id="6ea4c-124">En el menú **Herramientas**, elija **Opciones**.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-124">On the **Tools** menu, choose **Options**.</span></span> <span data-ttu-id="6ea4c-125">A continuación, expanda el nodo **Herramientas de rendimiento** y elija **General**.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-125">Then expand the **Performance Tools** node, and choose **General**.</span></span> <span data-ttu-id="6ea4c-126">Seleccione la casilla **Habilitar solo mi código para informes del generador de perfiles**.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-126">Select the checkbox for **Enable Just My Code for profiler reports**.</span></span>

![Opciones Solo mi código][17]

<span data-ttu-id="6ea4c-128">Puede usar estas instrucciones con un proyecto existente o con un proyecto nuevo.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-128">You can use these instructions with an existing project or with a new project.</span></span>  <span data-ttu-id="6ea4c-129">Si crea un proyecto nuevo para probar las técnicas que se describen a continuación, elija un proyecto de C# de **Servicio en la nube de Azure** y seleccione un **rol web** y un **rol de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-129">If you create a new project to try the techniques described below, choose a C# **Azure Cloud Service** project, and select a **Web Role** and a **Worker Role**.</span></span>

![Roles de proyecto del servicio en la nube de Azure][5]

<span data-ttu-id="6ea4c-131">Para propósitos de ejemplo, agregue parte del código al proyecto que tarda demasiado tiempo y demuestra un problema de rendimiento obvio.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-131">For example purposes, add some code to your project that takes a lot of time and demonstrates some obvious performance problem.</span></span> <span data-ttu-id="6ea4c-132">Por ejemplo, agregue el siguiente código a un proyecto de rol de trabajo:</span><span class="sxs-lookup"><span data-stu-id="6ea4c-132">For example, add the following code to a worker role project:</span></span>

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

<span data-ttu-id="6ea4c-133">Llame a este código desde el método RunAsync en la clase derivada de RoleEntryPoint del rol de trabajo.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-133">Call this code from the RunAsync method in the worker role's RoleEntryPoint-derived class.</span></span> <span data-ttu-id="6ea4c-134">(Ignore la advertencia sobre el método que se ejecuta sincrónicamente).</span><span class="sxs-lookup"><span data-stu-id="6ea4c-134">(Ignore the warning about the method running synchronously.)</span></span>

        private async Task RunAsync(CancellationToken cancellationToken)
        {
            // TODO: Replace the following with your own logic.
            while (!cancellationToken.IsCancellationRequested)
            {
                Trace.TraceInformation("Working");
                Concatenator.Concatenate(10000);
            }
        }

<span data-ttu-id="6ea4c-135">Compile y ejecute localmente su servicio en la nube sin depuración (Ctrl+F5), con la configuración de solución establecida en **Liberar**.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-135">Build and run your cloud service locally without debugging (Ctrl+F5), with the solution configuration set to **Release**.</span></span> <span data-ttu-id="6ea4c-136">Esto asegura que todos los archivos y carpetas se crean para ejecutar la aplicación localmente y asegura que se inicien todos los emuladores.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-136">This ensures that all files and folders are created for running the application locally, and ensures that all the emulators are started.</span></span> <span data-ttu-id="6ea4c-137">Comience la interfaz de usuario del emulador de proceso desde la barra de tareas para comprobar que el rol de trabajo se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-137">Start the Compute Emulator UI from the taskbar to verify that your worker role is running.</span></span>

## <a name="2-attach-to-a-process"></a><span data-ttu-id="6ea4c-138">2: Asociación a un proceso</span><span class="sxs-lookup"><span data-stu-id="6ea4c-138">2: Attach to a process</span></span>
<span data-ttu-id="6ea4c-139">En vez de generar un perfil en la aplicación al iniciarla desde Visual Studio 2010 IDE, debe asociar el generador de perfiles a un proceso en ejecución.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-139">Instead of profiling the application by starting it from the Visual Studio 2010 IDE, you must attach the profiler to a running process.</span></span> 

<span data-ttu-id="6ea4c-140">Para asociar el generador de perfiles a un proceso, en el menú **Analizar**, elija **Generador de perfiles** y **Asociar/desasociar**.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-140">To attach the profiler to a process, on the **Analyze** menu, choose **Profiler** and **Attach/Detach**.</span></span>

![Opción para adjuntar perfil][6]

<span data-ttu-id="6ea4c-142">Para un rol de trabajo, busque el proceso WaWorkerHost.exe.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-142">For a worker role, find the WaWorkerHost.exe process.</span></span>

![Proceso WaWorkerHost][7]

<span data-ttu-id="6ea4c-144">Si la carpeta de su proyecto se encuentra en una unidad de red, el generador de perfiles le pedirá proporcionar otra ubicación para guardar los informes de generación de perfiles.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-144">If your project folder is on a network drive, the profiler will ask you to provide another location to save the profiling reports.</span></span>

 <span data-ttu-id="6ea4c-145">Se puede también asociar a un rol web asociándose al archivo WaIISHost.exe.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-145">You can also attach to a web role by attaching to WaIISHost.exe.</span></span>
<span data-ttu-id="6ea4c-146">Si hay varios procesos de rol de trabajo en su aplicación, necesita usar processID para distinguirlos.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-146">If there are multiple worker role processes in your application, you need to use the processID to distinguish them.</span></span> <span data-ttu-id="6ea4c-147">Puede consultar el processID de manera programática al tener acceso al objeto del proceso.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-147">You can query the processID programmatically by accessing the Process object.</span></span> <span data-ttu-id="6ea4c-148">Por ejemplo, si agrega este código al método Run de la clase derivada de RoleEntryPoint en un rol, puede ver el registro en la interfaz de usuario del emulador de proceso para conocer el proceso al que debe conectarse.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-148">For example, if you add this code to the Run method of the RoleEntryPoint-derived class in a role, you can look at the log in the Compute Emulator UI to know what process to connect to.</span></span>

    var process = System.Diagnostics.Process.GetCurrentProcess();
    var message = String.Format("Process ID: {0}", process.Id);
    Trace.WriteLine(message, "Information");

<span data-ttu-id="6ea4c-149">Para ver el registro, inicie la interfaz de usuario del emulador de proceso.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-149">To view the log, start the Compute Emulator UI.</span></span>

![Inicio de la interfaz de usuario del emulador de proceso][8]

<span data-ttu-id="6ea4c-151">Abra la ventana de consola de registro del rol de trabajo en la interfaz de usuario del emulador de proceso al hacer clic en la barra de título de la ventana de la consola.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-151">Open the worker role log console window in the Compute Emulator UI by clicking on the console window's title bar.</span></span> <span data-ttu-id="6ea4c-152">Puede ver el identificador de proceso en el registro.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-152">You can see the process ID in the log.</span></span>

![Visualización del identificador de proceso][9]

<span data-ttu-id="6ea4c-154">Después de que se haya asociado, realice los pasos en la interfaz de usuario de su aplicación (si es necesario) para reproducir el escenario.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-154">One you've attached, perform the steps in your application's UI (if needed) to reproduce the scenario.</span></span>

<span data-ttu-id="6ea4c-155">Cuando desee detener la generación de perfiles, seleccione el vínculo **Detener generación de perfiles** .</span><span class="sxs-lookup"><span data-stu-id="6ea4c-155">When you want to stop profiling, choose the **Stop Profiling** link.</span></span>

![Opción Detener generación de perfiles][10]

## <a name="3-view-performance-reports"></a><span data-ttu-id="6ea4c-157">3: Vista de informes de rendimiento</span><span class="sxs-lookup"><span data-stu-id="6ea4c-157">3: View performance reports</span></span>
<span data-ttu-id="6ea4c-158">Aparece el informe de rendimiento de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-158">The performance report for your application is displayed.</span></span>

<span data-ttu-id="6ea4c-159">En este punto, el generador de perfiles detiene su ejecución, guarda los datos en un archivo .vsp y exhibe un informe que muestra un análisis de estos datos.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-159">At this point, the profiler stops executing, saves data in a .vsp file, and displays a report that shows an analysis of this data.</span></span>

![Informe del generador de perfiles][11]

<span data-ttu-id="6ea4c-161">Si ve String.wstrcpy en la ruta de acceso activa, haga clic en Solo mi código para cambiar la vista a fin de mostrar el código de usuario solamente.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-161">If you see String.wstrcpy in the Hot Path, click on Just My Code to change the view to show user code only.</span></span>  <span data-ttu-id="6ea4c-162">Si ve String.Concat, intente presionar el botón Mostrar todo el código.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-162">If you see String.Concat, try pressing the Show All Code button.</span></span>

<span data-ttu-id="6ea4c-163">Debería ver el método Concatenate y String.Concat que ocupan una gran parte del tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-163">You should see the Concatenate method and String.Concat taking up a large portion of the execution time.</span></span>

![Análisis del informe][12]

<span data-ttu-id="6ea4c-165">Si agregó el código de concatenación de cadena en este artículo, debería ver una advertencia en la lista de tareas para esta.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-165">If you added the string concatenation code in this article, you should see a warning in the Task List for this.</span></span> <span data-ttu-id="6ea4c-166">Es posible que también vea una advertencia de que hay una cantidad excesiva de elementos no utilizados, lo que se debe a la cantidad de cadenas que se crearon y desplegaron.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-166">You may also see a warning that there is an excessive amount of garbage collection, which is due to the number of strings that are created and disposed.</span></span>

![Advertencias de rendimiento][14]

## <a name="4-make-changes-and-compare-performance"></a><span data-ttu-id="6ea4c-168">4: Realización de cambios y comparación del rendimiento</span><span class="sxs-lookup"><span data-stu-id="6ea4c-168">4: Make changes and compare performance</span></span>
<span data-ttu-id="6ea4c-169">Puede también comparar el rendimiento antes y después de un cambio en el código.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-169">You can also compare the performance before and after a code change.</span></span>  <span data-ttu-id="6ea4c-170">Detenga el proceso de ejecución y edite el código para reemplazar la operación de concatenación de cadena con el uso de StringBuilder:</span><span class="sxs-lookup"><span data-stu-id="6ea4c-170">Stop the running process, and edit the code to replace the string concatenation operation with the use of StringBuilder:</span></span>

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

<span data-ttu-id="6ea4c-171">Realice otra ejecución de rendimiento y, a continuación, compárelo.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-171">Do another performance run, and then compare the performance.</span></span> <span data-ttu-id="6ea4c-172">En el Explorador de rendimiento, si las ejecuciones se encuentran en la misma sesión, simplemente puede seleccionar ambos informes, abrir el menú de acceso directo y seleccionar **Comparar informes de rendimiento**.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-172">In the Performance Explorer, if the runs are in the same session, you can just select both reports, open the shortcut menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="6ea4c-173">Si desea realizar una comparación con una ejecución en otra sesión de rendimiento, abra el menú **Analizar** y seleccione **Comparar informes de rendimiento**.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-173">If you want to compare with a run in another performance session, open the **Analyze** menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="6ea4c-174">En el cuadro de diálogo que aparece, especifique ambos archivos.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-174">Specify both files in the dialog box that appears.</span></span>

![Opción para comparar informes de rendimiento][15]

<span data-ttu-id="6ea4c-176">Los informes resaltan las diferencias entre las dos ejecuciones.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-176">The reports highlight differences between the two runs.</span></span>

![Informe de comparación][16]

<span data-ttu-id="6ea4c-178">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="6ea4c-178">Congratulations!</span></span> <span data-ttu-id="6ea4c-179">Ya ha empezado a usar el generador de perfiles.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-179">You've gotten started with the profiler.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="6ea4c-180">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="6ea4c-180">Troubleshooting</span></span>
* <span data-ttu-id="6ea4c-181">Asegúrese de que va a generar un perfil de una compilación de versión e iniciar sin depuración.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-181">Make sure you are profiling a Release build and start without debugging.</span></span>
* <span data-ttu-id="6ea4c-182">Si la opción Asociar/Desasociar no está habilitada en el menú del Generador de perfiles, ejecute el Asistente de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-182">If the Attach/Detach option is not enabled on the Profiler menu, run the Performance Wizard.</span></span>
* <span data-ttu-id="6ea4c-183">Use la interfaz de usuario del emulador de proceso para ver el estado de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-183">Use the Compute Emulator UI to view the status of your application.</span></span> 
* <span data-ttu-id="6ea4c-184">Si tiene problemas al iniciar aplicaciones en el emulador o asociar el generador de perfiles, apague el emulador de proceso y reinícielo.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-184">If you have problems starting applications in the emulator, or attaching the profiler, shut down the compute emulator and restart it.</span></span> <span data-ttu-id="6ea4c-185">Si el problema no se soluciona, intente reiniciar.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-185">If that doesn't solve the problem, try rebooting.</span></span> <span data-ttu-id="6ea4c-186">Este problema se produce si usa el emulador de proceso para suspender y quitar implementaciones en ejecución.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-186">This problem can occur if you use the Compute Emulator to suspend and remove running deployments.</span></span>
* <span data-ttu-id="6ea4c-187">Si ha utilizado cualquiera de los comandos de generación de perfiles desde la línea de comandos, especialmente la configuración global, asegúrese de que se haya llamado a VSPerfClrEnv /globaloff y que VsPerfMon.exe se haya apagado.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-187">If you have used any of the profiling commands from the command line, especially the global settings, make sure that VSPerfClrEnv /globaloff has been called and that VsPerfMon.exe has been shut down.</span></span>
* <span data-ttu-id="6ea4c-188">Si al realizar el muestreo, ve el mensaje "PRF0025: no se recopilaron datos", compruebe que el proceso al que se asoció tiene actividad de CPU.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-188">If when sampling, you see the message "PRF0025: No data was collected," check that the process you attached to has CPU activity.</span></span> <span data-ttu-id="6ea4c-189">Es posible que las aplicaciones que no están realizando ningún trabajo informático no produzcan datos de muestreo.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-189">Applications that are not doing any computational work might not produce any sampling data.</span></span>  <span data-ttu-id="6ea4c-190">También es posible que el proceso haya finalizado antes de que se haya realizado muestreo alguno.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-190">It's also possible that the process exited before any sampling was done.</span></span> <span data-ttu-id="6ea4c-191">Compruebe que el método de ejecución de un rol para el cual está generando un perfil no termine.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-191">Check to see that the Run method for a role that you are profiling does not terminate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ea4c-192">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6ea4c-192">Next Steps</span></span>
<span data-ttu-id="6ea4c-193">La instrumentación de binarios de Azure en el emulador no es compatible en el generador de perfiles de Visual Studio; sin embargo, si desea probar la asignación de memoria, puede seleccionar esta opción al generar perfiles.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-193">Instrumenting Azure binaries in the emulator is not supported in the Visual Studio profiler, but if you want to test memory allocation, you can choose that option when profiling.</span></span> <span data-ttu-id="6ea4c-194">También puede seleccionar una generación de perfiles de concurrencia, la cual le ayuda a determinar si los subprocesos están desperdiciando tiempo al competir por bloqueos, o la generación de perfiles de interacción de capa, que le ayuda a hacer un seguimiento de los problemas de rendimiento cuando se interactúa entre las capas de una aplicación, con mayor frecuencia entre la capa de datos y un rol de trabajo.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-194">You can also choose concurrency profiling, which helps you determine whether threads are wasting time competing for locks, or tier interaction profiling, which helps you track down performance problems when interacting between tiers of an application, most frequently between the data tier and a worker role.</span></span>  <span data-ttu-id="6ea4c-195">Puede ver las consultas de la base de datos que genera la aplicación y usar los datos de generación de perfiles para mejorar el uso que hace de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="6ea4c-195">You can view the database queries that your app generates and use the profiling data to improve your use of the database.</span></span> <span data-ttu-id="6ea4c-196">Para obtener información sobre la generación de perfiles de interacción de capa, vea la entrada de blog [Walkthrough: Using the Tier Interaction Profiler in Visual Studio Team System 2010][3] (Tutorial: Uso del generador de perfiles de interacción de capas en Visual Studio Team System 2010).</span><span class="sxs-lookup"><span data-stu-id="6ea4c-196">For information about tier interaction profiling, see the blog post [Walkthrough: Using the Tier Interaction Profiler in Visual Studio Team System 2010][3].</span></span>

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
