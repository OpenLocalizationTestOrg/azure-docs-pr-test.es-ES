---
title: aaaRun tareas en segundo plano con WebJobs
description: "Obtenga información acerca de cómo toorun tareas en segundo plano en Azure web aplicaciones."
services: app-service
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: af01771e-54eb-4aea-af5f-f883ff39572b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/27/2016
ms.author: glenga
ms.openlocfilehash: 96a3d977a806e7192207f0f4da79dfd248694336
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-background-tasks-with-webjobs"></a><span data-ttu-id="75b1a-103">Ejecutar tareas en segundo plano con trabajos web</span><span class="sxs-lookup"><span data-stu-id="75b1a-103">Run Background tasks with WebJobs</span></span>
## <a name="overview"></a><span data-ttu-id="75b1a-104">Información general</span><span class="sxs-lookup"><span data-stu-id="75b1a-104">Overview</span></span>
<span data-ttu-id="75b1a-105">Puede ejecutar programas o scripts en trabajos web en su aplicación web de [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) de tres maneras: a petición, de forma continua o según una programación.</span><span class="sxs-lookup"><span data-stu-id="75b1a-105">You can run programs or scripts in WebJobs in your [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) web app in three ways: on demand, continuously, or on a schedule.</span></span> <span data-ttu-id="75b1a-106">No hay ningún toouse costo adicional trabajos Web.</span><span class="sxs-lookup"><span data-stu-id="75b1a-106">There is no additional cost toouse WebJobs.</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="75b1a-107">Este artículo muestra cómo toodeploy trabajos Web mediante el uso de Hola [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="75b1a-107">This article shows how toodeploy WebJobs by using hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="75b1a-108">Para obtener información acerca de cómo toodeploy mediante Visual Studio o un proceso de entrega continua, vea [cómo tooDeploy WebJobs de Azure tooWeb aplicaciones](websites-dotnet-deploy-webjobs.md).</span><span class="sxs-lookup"><span data-stu-id="75b1a-108">For information about how toodeploy by using Visual Studio or a continuous delivery process, see [How tooDeploy Azure WebJobs tooWeb Apps](websites-dotnet-deploy-webjobs.md).</span></span>

<span data-ttu-id="75b1a-109">Hola SDK de WebJobs de Azure simplifica muchas tareas de programación de trabajos Web.</span><span class="sxs-lookup"><span data-stu-id="75b1a-109">hello Azure WebJobs SDK simplifies many WebJobs programming tasks.</span></span> <span data-ttu-id="75b1a-110">Para obtener más información, consulte [¿qué es hello SDK de WebJobs](websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="75b1a-110">For more information, see [What is hello WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

 <span data-ttu-id="75b1a-111">Las funciones de Azure proporciona otro toorun funcionamiento de los programas y secuencias de comandos desde un entorno sin servidor o desde una aplicación de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="75b1a-111">Azure Functions provides another way toorun programs and scripts from either a serverless environment or from an App Service app.</span></span> <span data-ttu-id="75b1a-112">Para obtener más información, consulte [Información general sobre Funciones de Azure](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="75b1a-112">For more information, see [Azure Functions overview](../azure-functions/functions-overview.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="75b1a-113"><a name="acceptablefiles"></a>Tipos de archivo válidos para scripts o programas</span><span class="sxs-lookup"><span data-stu-id="75b1a-113"><a name="acceptablefiles"></a>Acceptable file types for scripts or programs</span></span>
<span data-ttu-id="75b1a-114">se acepta Hola siguientes tipos de archivo:</span><span class="sxs-lookup"><span data-stu-id="75b1a-114">hello following file types are accepted:</span></span>

* <span data-ttu-id="75b1a-115">.cmd, .bat, .exe (con windows cmd)</span><span class="sxs-lookup"><span data-stu-id="75b1a-115">.cmd, .bat, .exe (using windows cmd)</span></span>
* <span data-ttu-id="75b1a-116">.ps1 (con powershell)</span><span class="sxs-lookup"><span data-stu-id="75b1a-116">.ps1 (using powershell)</span></span>
* <span data-ttu-id="75b1a-117">.sh (con bash)</span><span class="sxs-lookup"><span data-stu-id="75b1a-117">.sh (using bash)</span></span>
* <span data-ttu-id="75b1a-118">.php (con php)</span><span class="sxs-lookup"><span data-stu-id="75b1a-118">.php (using php)</span></span>
* <span data-ttu-id="75b1a-119">.py (con python)</span><span class="sxs-lookup"><span data-stu-id="75b1a-119">.py (using python)</span></span>
* <span data-ttu-id="75b1a-120">.js (con node)</span><span class="sxs-lookup"><span data-stu-id="75b1a-120">.js (using node)</span></span>
* <span data-ttu-id="75b1a-121">.jar (con java)</span><span class="sxs-lookup"><span data-stu-id="75b1a-121">.jar (using java)</span></span>

## <span data-ttu-id="75b1a-122"><a name="CreateOnDemand"></a>Crear un informe a petición trabajo Web en el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="75b1a-122"><a name="CreateOnDemand"></a>Create an on demand WebJob in hello portal</span></span>
1. <span data-ttu-id="75b1a-123">Hola **aplicación Web** hoja de hello [Portal de Azure](https://portal.azure.com), haga clic en **toda la configuración > trabajos Web** tooshow hello **WebJobs** hoja.</span><span class="sxs-lookup"><span data-stu-id="75b1a-123">In hello **Web App** blade of hello [Azure Portal](https://portal.azure.com), click **All settings > WebJobs** tooshow hello **WebJobs** blade.</span></span>
   
    ![Hoja de WebJobs](./media/web-sites-create-web-jobs/wjblade.png)
2. <span data-ttu-id="75b1a-125">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="75b1a-125">Click **Add**.</span></span> <span data-ttu-id="75b1a-126">Hola **Agregar trabajo Web** aparece el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="75b1a-126">hello **Add WebJob** dialog appears.</span></span>
   
    ![Adición de hoja de WebJobs](./media/web-sites-create-web-jobs/addwjblade.png)
3. <span data-ttu-id="75b1a-128">En **nombre**, proporcione un nombre para hello trabajo Web.</span><span class="sxs-lookup"><span data-stu-id="75b1a-128">Under **Name**, provide a name for hello WebJob.</span></span> <span data-ttu-id="75b1a-129">nombre de Hello debe empezar por una letra o un número y no puede contener ningún carácter especial salvo "-" y "_".</span><span class="sxs-lookup"><span data-stu-id="75b1a-129">hello name must start with a letter or a number and cannot contain any special characters other than "-" and "_".</span></span>
4. <span data-ttu-id="75b1a-130">Hola **cómo tooRun** cuadro, elija **ejecutar a petición**.</span><span class="sxs-lookup"><span data-stu-id="75b1a-130">In hello **How tooRun** box, choose **Run on Demand**.</span></span>
5. <span data-ttu-id="75b1a-131">Hola **cargar archivo** cuadro, haga clic en el icono de carpeta de Hola y examinar toohello zip que contiene el script.</span><span class="sxs-lookup"><span data-stu-id="75b1a-131">In hello **File Upload** box, click hello folder icon and browse toohello zip file that contains your script.</span></span> <span data-ttu-id="75b1a-132">archivo zip de Hello debe contener su archivo ejecutable (.exe .cmd .bat .sh .php .py .js), así como los archivos auxiliares necesarios toorun Hola programa o script.</span><span class="sxs-lookup"><span data-stu-id="75b1a-132">hello zip file should contain your executable (.exe .cmd .bat .sh .php .py .js) as well as any supporting files needed toorun hello program or script.</span></span>
6. <span data-ttu-id="75b1a-133">Comprobar **crear** tooupload Hola script tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="75b1a-133">Check **Create** tooupload hello script tooyour web app.</span></span> 
   
    <span data-ttu-id="75b1a-134">Hello nombre especificado para hello trabajo Web aparece en lista Hola Hola **WebJobs** hoja.</span><span class="sxs-lookup"><span data-stu-id="75b1a-134">hello name you specified for hello WebJob appears in hello list on hello **WebJobs** blade.</span></span>
7. <span data-ttu-id="75b1a-135">Hola toorun trabajo Web, haga clic en su nombre en la lista de Hola y haga clic en **ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="75b1a-135">toorun hello WebJob, right-click its name in hello list and click **Run**.</span></span>
   
    ![Ejecución de WebJobs](./media/web-sites-create-web-jobs/runondemand.png)

## <span data-ttu-id="75b1a-137"><a name="CreateContinuous"></a>Creación de un trabajo web de ejecución continua</span><span class="sxs-lookup"><span data-stu-id="75b1a-137"><a name="CreateContinuous"></a>Create a continuously running WebJob</span></span>
1. <span data-ttu-id="75b1a-138">toocreate un trabajo Web que está ejecutando continuamente, siga Hola mismos pasos para crear un trabajo Web que se ejecuta una vez, pero en hello **cómo tooRun** cuadro, elija **Continuous**.</span><span class="sxs-lookup"><span data-stu-id="75b1a-138">toocreate a continuously executing WebJob, follow hello same steps for creating a WebJob that runs once, but in hello **How tooRun** box, choose **Continuous**.</span></span>
2. <span data-ttu-id="75b1a-139">toostart o detener un trabajo Web continuo, haga clic en hello trabajo Web en la lista de Hola y haga clic en **iniciar** o **detener**.</span><span class="sxs-lookup"><span data-stu-id="75b1a-139">toostart or stop a continuous WebJob, right-click hello WebJob in hello list and click **Start** or **Stop**.</span></span>

> [!NOTE]
> <span data-ttu-id="75b1a-140">Si la aplicación web se ejecuta en más de una instancia, se ejecutará un trabajo web continuamente en todas las instancias.</span><span class="sxs-lookup"><span data-stu-id="75b1a-140">If your web app runs on more than one instance, a continuously running WebJob will run on all of your instances.</span></span> <span data-ttu-id="75b1a-141">Los Trabajos web a petición o programados se ejecutan en una única instancia seleccionada por Microsoft Azure para el equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="75b1a-141">On-demand and scheduled WebJobs run on a single instance selected for load balancing by Microsoft Azure.</span></span>
> 
> <span data-ttu-id="75b1a-142">Para los trabajos Web continuos toorun forma confiable y en todas las instancias, habilitar Hola Always On * valor de configuración para web aplicación hello en caso contrario puede interrumpir la ejecución cuando el sitio de hello SCM host ha estado inactivo durante demasiado tiempo.</span><span class="sxs-lookup"><span data-stu-id="75b1a-142">For Continuous WebJobs toorun reliably and on all instances, enable hello Always On* configuration setting for hello web app otherwise they can stop running when hello SCM host site has been idle for too long.</span></span>
> 
> 

## <span data-ttu-id="75b1a-143"><a name="CreateScheduledCRON"></a>Creación de un trabajo web programado utilizando una expresión CRON</span><span class="sxs-lookup"><span data-stu-id="75b1a-143"><a name="CreateScheduledCRON"></a>Create a scheduled WebJob using a CRON expression</span></span>
<span data-ttu-id="75b1a-144">Esta técnica es aplicaciones tooWeb disponibles que se ejecutan en modo básico, estándar o Premium y requiere hello **Always On** establecer toobe habilitada en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="75b1a-144">This technique is available tooWeb Apps running in Basic, Standard or Premium mode, and requires hello **Always On** setting toobe enabled on hello app.</span></span>

<span data-ttu-id="75b1a-145">tooturn un en trabajo Web petición en un trabajo Web programado, basta con incluir un `settings.job` archivo en hello raíz del archivo zip trabajo Web.</span><span class="sxs-lookup"><span data-stu-id="75b1a-145">tooturn an On Demand WebJob into a scheduled WebJob, simply include a `settings.job` file at hello root of your WebJob zip file.</span></span> <span data-ttu-id="75b1a-146">Este archivo JSON debe incluir una propiedad `schedule` con una [expresión CRON](https://en.wikipedia.org/wiki/Cron)como la siguiente.</span><span class="sxs-lookup"><span data-stu-id="75b1a-146">This JSON file should include a `schedule` property with a [CRON expression](https://en.wikipedia.org/wiki/Cron), per example below.</span></span>

<span data-ttu-id="75b1a-147">Hola expresión CRON se compone de 6 campos: `{second} {minute} {hour} {day} {month} {day of hello week}`.</span><span class="sxs-lookup"><span data-stu-id="75b1a-147">hello CRON expression is composed of 6 fields: `{second} {minute} {hour} {day} {month} {day of hello week}`.</span></span>

<span data-ttu-id="75b1a-148">Por ejemplo, tootrigger su trabajo Web cada 15 minutos, el `settings.job` tendría:</span><span class="sxs-lookup"><span data-stu-id="75b1a-148">For example, tootrigger your WebJob every 15 minutes, your `settings.job` would have:</span></span>

```json
{
    "schedule": "0 */15 * * * *"
}
``` 

<span data-ttu-id="75b1a-149">Otros ejemplos de programación CRON:</span><span class="sxs-lookup"><span data-stu-id="75b1a-149">Other CRON schedule examples:</span></span>

* <span data-ttu-id="75b1a-150">Cada hora (es decir, siempre que sea recuento Hola de minutos es 0):`0 0 * * * *`</span><span class="sxs-lookup"><span data-stu-id="75b1a-150">Every hour (i.e. whenever hello count of minutes is 0): `0 0 * * * *`</span></span> 
* <span data-ttu-id="75b1a-151">Cada hora de 9 AM too5 PM:`0 0 9-17 * * *`</span><span class="sxs-lookup"><span data-stu-id="75b1a-151">Every hour from 9 AM too5 PM: `0 0 9-17 * * *`</span></span> 
* <span data-ttu-id="75b1a-152">A las 9:30 todos los días: `0 30 9 * * *`</span><span class="sxs-lookup"><span data-stu-id="75b1a-152">At 9:30 AM every day: `0 30 9 * * *`</span></span>
* <span data-ttu-id="75b1a-153">A las 9:30 cada día de lunes a viernes: `0 30 9 * * 1-5`</span><span class="sxs-lookup"><span data-stu-id="75b1a-153">At 9:30 AM every week day: `0 30 9 * * 1-5`</span></span>

<span data-ttu-id="75b1a-154">**Tenga en cuenta**: al implementar un trabajo Web desde Visual Studio, asegúrese de que toomark su `settings.job` propiedades del archivo como "Copiar si es posterior".</span><span class="sxs-lookup"><span data-stu-id="75b1a-154">**Note**: when deploying a WebJob from Visual Studio, make sure toomark your `settings.job` file properties as 'Copy if newer'.</span></span>

## <span data-ttu-id="75b1a-155"><a name="CreateScheduled"></a>Crear un trabajo Web programado mediante Hola programador de Azure</span><span class="sxs-lookup"><span data-stu-id="75b1a-155"><a name="CreateScheduled"></a>Create a scheduled WebJob using hello Azure Scheduler</span></span>
<span data-ttu-id="75b1a-156">Hola siguiendo la técnica alternativa hace uso de hello Azure Scheduler.</span><span class="sxs-lookup"><span data-stu-id="75b1a-156">hello following alternate technique makes use of hello Azure Scheduler.</span></span> <span data-ttu-id="75b1a-157">En este caso, el trabajo Web no tiene ningún conocimiento directo de programación de Hola.</span><span class="sxs-lookup"><span data-stu-id="75b1a-157">In this case, your WebJob does not have any direct knowledge of hello schedule.</span></span> <span data-ttu-id="75b1a-158">En su lugar, hello Azure Scheduler obtiene tootrigger configurado su trabajo Web según una programación.</span><span class="sxs-lookup"><span data-stu-id="75b1a-158">Instead, hello Azure Scheduler gets configured tootrigger your WebJob on a schedule.</span></span> 

<span data-ttu-id="75b1a-159">Hola Portal de Azure no tiene todavía a Hola capacidad toocreate un trabajo Web programado, pero hasta que se agregue esta característica puede hacer mediante el uso de hello [portal clásico](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="75b1a-159">hello Azure Portal doesn't yet have hello ability toocreate a scheduled WebJob, but until that feature is added you can do it by using hello [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="75b1a-160">Hola [portal clásico](http://manage.windowsazure.com) toohello página de trabajo Web y haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="75b1a-160">In hello [classic portal](http://manage.windowsazure.com) go toohello WebJob page and click **Add**.</span></span>
2. <span data-ttu-id="75b1a-161">Hola **cómo tooRun** cuadro, elija **ejecutar según una programación**.</span><span class="sxs-lookup"><span data-stu-id="75b1a-161">In hello **How tooRun** box, choose **Run on a schedule**.</span></span>
   
    ![Nuevo trabajo programado][NewScheduledJob]
3. <span data-ttu-id="75b1a-163">Elija hello **programador región** para su trabajo y, a continuación, haga clic en la flecha Hola Hola parte inferior derecha pantalla siguiente de bienvenida diálogo tooproceed toohello.</span><span class="sxs-lookup"><span data-stu-id="75b1a-163">Choose hello **Scheduler Region** for your job, and then click hello arrow on hello bottom right of hello dialog tooproceed toohello next screen.</span></span>
4. <span data-ttu-id="75b1a-164">Hola **crear trabajo de** cuadro de diálogo, elija tipo hello de **periodicidad** desea: **trabajo único** o **trabajo periódica**.</span><span class="sxs-lookup"><span data-stu-id="75b1a-164">In hello **Create Job** dialog, choose hello type of **Recurrence** you want: **One-time job** or **Recurring job**.</span></span>
   
    ![Periodicidad de la programación][SchdRecurrence]
5. <span data-ttu-id="75b1a-166">Elija también una hora de **inicio**: **Ahora** o **En un momento determinado**.</span><span class="sxs-lookup"><span data-stu-id="75b1a-166">Also choose a **Starting** time: **Now** or **At a specific time**.</span></span>
   
    ![Hora de inicio de la programación][SchdStart]
6. <span data-ttu-id="75b1a-168">Si desea toostart en un momento determinado, elija los valores de tiempo inicial en **a partir de**.</span><span class="sxs-lookup"><span data-stu-id="75b1a-168">If you want toostart at a specific time, choose your starting time values under **Starting On**.</span></span>
   
    ![Inicio de la programación a una hora determinada][SchdStartOn]
7. <span data-ttu-id="75b1a-170">Si ha elegido un trabajo periódico, tiene hello **Repetir cada** opción frecuencia de hello toospecify de repetición y hello **final en** opción toospecify una hora de finalización.</span><span class="sxs-lookup"><span data-stu-id="75b1a-170">If you chose a recurring job, you have hello **Recur Every** option toospecify hello frequency of occurrence and hello **Ending On** option toospecify an ending time.</span></span>
   
    ![Periodicidad de la programación][SchdRecurEvery]
8. <span data-ttu-id="75b1a-172">Si elige **semanas**, puede seleccionar hello **en una programación determinada** cuadro y especifique días de saludo de la semana de Hola que desee Hola toorun de trabajo.</span><span class="sxs-lookup"><span data-stu-id="75b1a-172">If you choose **Weeks**, you can select hello **On a Particular Schedule** box and specify hello days of hello week that you want hello job toorun.</span></span>
   
    ![Días de programación de hello semana][SchdWeeksOnParticular]
9. <span data-ttu-id="75b1a-174">Si elige **meses** y seleccione hello **en una programación determinada** cuadro, puede establecer toorun de trabajo de hello en particular numerado **días** mes Hola.</span><span class="sxs-lookup"><span data-stu-id="75b1a-174">If you choose **Months** and select hello **On a Particular Schedule** box, you can set hello job toorun on particular numbered **Days** in hello month.</span></span> 
   
    ![Programar fechas concretas en hello mes][SchdMonthsOnPartDays]
10. <span data-ttu-id="75b1a-176">Si elige **días de la semana**, puede seleccionar qué día o días de la semana de hello en mes de Hola que desea Hola toorun de trabajo en.</span><span class="sxs-lookup"><span data-stu-id="75b1a-176">If you choose **Week Days**, you can select which day or days of hello week in hello month you want hello job toorun on.</span></span>
    
     ![Programación en días determinados de la semana de un mes][SchdMonthsOnPartWeekDays]
11. <span data-ttu-id="75b1a-178">Por último, también puede usar hello **apariciones** opción toochoose qué semana del mes de Hola (primera, segunda, tercera etc.) desea toorun de trabajo de hello en hello días de la semana especificado.</span><span class="sxs-lookup"><span data-stu-id="75b1a-178">Finally, you can also use hello **Occurrences** option toochoose which week in hello month (first, second, third etc.) you want hello job toorun on hello week days you specified.</span></span>
    
    ![Programación en días de la semana específicos de semanas determinadas][SchdMonthsOnPartWeekDaysOccurences]
12. <span data-ttu-id="75b1a-180">Después de haber creado uno o varios trabajos, sus nombres aparecerán en la ficha de trabajos Web Hola con su estado, tipo de programación y otra información.</span><span class="sxs-lookup"><span data-stu-id="75b1a-180">After you have created one or more jobs, their names will appear on hello WebJobs tab with their status, schedule type, and other information.</span></span> <span data-ttu-id="75b1a-181">Se mantiene la información histórica de hello últimos 30 trabajos Web.</span><span class="sxs-lookup"><span data-stu-id="75b1a-181">Historical information for hello last 30  WebJobs is maintained.</span></span>
    
    ![Lista de trabajos][WebJobsListWithSeveralJobs]

### <span data-ttu-id="75b1a-183"><a name="Scheduler"></a>Trabajos programados y Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="75b1a-183"><a name="Scheduler"></a>Scheduled jobs and Azure Scheduler</span></span>
<span data-ttu-id="75b1a-184">Los trabajos programados se pueden configurar aún más en páginas de Azure Scheduler Hola de hello [portal clásico](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="75b1a-184">Scheduled jobs can be further configured in hello Azure Scheduler pages of hello [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="75b1a-185">En la página de trabajos Web hello, haga clic en del trabajo de hello **programación** página del portal de Azure Scheduler de vínculo toonavigate toohello.</span><span class="sxs-lookup"><span data-stu-id="75b1a-185">On hello WebJobs page, click hello job's **schedule** link toonavigate toohello Azure Scheduler portal page.</span></span> 
   
   ![Vínculo tooAzure programador][LinkToScheduler]
2. <span data-ttu-id="75b1a-187">En la página de programador de hello, haga clic en trabajo Hola.</span><span class="sxs-lookup"><span data-stu-id="75b1a-187">On hello Scheduler page, click hello job.</span></span>
   
    ![Trabajo en la página del portal de programador Hola][SchedulerPortal]
3. <span data-ttu-id="75b1a-189">Hola **acción de trabajo** página se abre, donde puede seguir configurando trabajo Hola.</span><span class="sxs-lookup"><span data-stu-id="75b1a-189">hello **Job Action** page opens, where you can further configure hello job.</span></span> 
   
    ![Página de acción del trabajo en el Programador][JobActionPageInScheduler]

## <span data-ttu-id="75b1a-191"><a name="ViewJobHistory"></a>Ver historial de trabajos de Hola</span><span class="sxs-lookup"><span data-stu-id="75b1a-191"><a name="ViewJobHistory"></a>View hello job history</span></span>
1. <span data-ttu-id="75b1a-192">historial de ejecución de hello tooview de un trabajo, incluidos los trabajos creados con hello SDK de WebJobs, haga clic en el vínculo correspondiente, bajo hello **registros** columna de hoja de WebJobs de Hola.</span><span class="sxs-lookup"><span data-stu-id="75b1a-192">tooview hello execution history of a job, including jobs created with hello WebJobs SDK, click  its corresponding link under hello **Logs** column of hello WebJobs blade.</span></span> <span data-ttu-id="75b1a-193">(Puede usar Hola Portapapeles toocopy Hola dirección URL de icono del Portapapeles de hello registro archivo página toohello si lo desea).</span><span class="sxs-lookup"><span data-stu-id="75b1a-193">(You can use hello clipboard icon toocopy hello URL of hello log file page toohello clipboard if you wish.)</span></span>
   
    ![Vínculo de registros](./media/web-sites-create-web-jobs/wjbladelogslink.png)
2. <span data-ttu-id="75b1a-195">Si hace clic en vínculo Hola abrirá la página de detalles de Hola de hello trabajo Web.</span><span class="sxs-lookup"><span data-stu-id="75b1a-195">Clicking hello link opens hello details page for hello WebJob.</span></span> <span data-ttu-id="75b1a-196">Esta página muestra Hola nombre de la ejecución de comandos de Hola Hola últimas veces que se ejecutó, y su éxito o fracaso.</span><span class="sxs-lookup"><span data-stu-id="75b1a-196">This page shows you hello name of hello command run, hello last times it ran, and its success or failure.</span></span> <span data-ttu-id="75b1a-197">En **ejecuciones recientes de trabajos**, haga clic en un toosee más detalles de tiempo.</span><span class="sxs-lookup"><span data-stu-id="75b1a-197">Under **Recent job runs**, click a time toosee further details.</span></span>
   
    ![Detalles del trabajo web][WebJobDetails]
3. <span data-ttu-id="75b1a-199">Hola **detalles de ejecución de trabajo Web** aparece la página.</span><span class="sxs-lookup"><span data-stu-id="75b1a-199">hello **WebJob Run Details** page appears.</span></span> <span data-ttu-id="75b1a-200">Haga clic en **alternar salida** toosee texto de hello de contenido del registro de hello.</span><span class="sxs-lookup"><span data-stu-id="75b1a-200">Click **Toggle Output** toosee hello text of hello log contents.</span></span> <span data-ttu-id="75b1a-201">registro de salida de Hello está en formato de texto.</span><span class="sxs-lookup"><span data-stu-id="75b1a-201">hello output log is in text format.</span></span> 
   
    ![Detalles de ejecución del trabajo web][WebJobRunDetails]
4. <span data-ttu-id="75b1a-203">texto de salida de hello toosee en otra ventana del explorador, haga clic en hello **descargar** vínculo.</span><span class="sxs-lookup"><span data-stu-id="75b1a-203">toosee hello output text in a separate browser window, click hello **download** link.</span></span> <span data-ttu-id="75b1a-204">toodownload Hola propio texto, haga clic en el vínculo de Hola y usar el contenido del archivo explorador opciones toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="75b1a-204">toodownload hello text itself, right-click hello link and use your browser options toosave hello file contents.</span></span>
   
    ![Resultado del registro de descarga][DownloadLogOutput]
5. <span data-ttu-id="75b1a-206">Hola **WebJobs** vínculo situado en la parte superior de Hola de página de hello proporciona una lista de tooa de tooget de forma cómoda de trabajos Web en el panel de historial de Hola.</span><span class="sxs-lookup"><span data-stu-id="75b1a-206">hello **WebJobs** link at hello top of hello page provides a convenient way tooget tooa list of WebJobs on hello history dashboard.</span></span>
   
    ![Lista de vínculos tooWebJobs][WebJobsLinkToDashboardList]
   
    ![Lista de WebJobs el panel del historial][WebJobsListInJobsDashboard]
   
    <span data-ttu-id="75b1a-209">Haga clic en uno de estos vínculos le toohello página de detalles del trabajo Web de trabajo de Hola que seleccionó.</span><span class="sxs-lookup"><span data-stu-id="75b1a-209">Clicking one of these links takes you toohello WebJob Details page for hello job you selected.</span></span>

## <span data-ttu-id="75b1a-210"><a name="WHPNotes"></a>Notas</span><span class="sxs-lookup"><span data-stu-id="75b1a-210"><a name="WHPNotes"></a>Notes</span></span>
* <span data-ttu-id="75b1a-211">Las aplicaciones Web en el modo gratuito pueden tiempo de espera después de 20 minutos si no hay ningún sitio de scm (implementación) de las solicitudes toohello y portal de la aplicación hello web no está abierto en Azure.</span><span class="sxs-lookup"><span data-stu-id="75b1a-211">Web apps in Free mode can time out after 20 minutes if there are no requests toohello scm (deployment) site and hello web app's portal is not open in Azure.</span></span> <span data-ttu-id="75b1a-212">Las solicitudes toohello reales del sitio no restablecerán esto.</span><span class="sxs-lookup"><span data-stu-id="75b1a-212">Requests toohello actual site will not reset this.</span></span>
* <span data-ttu-id="75b1a-213">El código de un trabajo continuo debe toobe escrito toorun en un bucle sin fin.</span><span class="sxs-lookup"><span data-stu-id="75b1a-213">Code for a continuous job needs toobe written toorun in an endless loop.</span></span>
* <span data-ttu-id="75b1a-214">Los trabajos continuos se ejecutan continuamente solo cuando la aplicación web de hello está activa.</span><span class="sxs-lookup"><span data-stu-id="75b1a-214">Continuous jobs run continuously only when hello web app is up.</span></span>
* <span data-ttu-id="75b1a-215">Básica y los modos estándar oferta Hola siempre en características que, cuando se habilita, impide que las aplicaciones web llega a estar inactivo.</span><span class="sxs-lookup"><span data-stu-id="75b1a-215">Basic and Standard modes offer hello Always On feature which, when enabled, prevents web apps from becoming idle.</span></span>
* <span data-ttu-id="75b1a-216">Solo se pueden depurar WebJobs que se ejecutan continuamente.</span><span class="sxs-lookup"><span data-stu-id="75b1a-216">You can only debug continuously running WebJobs.</span></span> <span data-ttu-id="75b1a-217">No se admite la depuración de WebJobs programada o a petición.</span><span class="sxs-lookup"><span data-stu-id="75b1a-217">Debugging scheduled or on-demand WebJobs is not supported.</span></span>

## <span data-ttu-id="75b1a-218"><a name="NextSteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="75b1a-218"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="75b1a-219">Para obtener más información, consulte [Recursos recomendados de WebJobs de Azure][WebJobsRecommendedResources].</span><span class="sxs-lookup"><span data-stu-id="75b1a-219">For more information, see [Azure WebJobs Recommended Resources][WebJobsRecommendedResources].</span></span>

[PSonWebJobs]:http://blogs.msdn.com/b/nicktrog/archive/2014/01/22/running-powershell-web-jobs-on-azure-websites.aspx
[WebJobsRecommendedResources]:http://go.microsoft.com/fwlink/?LinkId=390226

[OnDemandWebJob]: ./media/web-sites-create-web-jobs/01aOnDemandWebJob.png
[WebJobsList]: ./media/web-sites-create-web-jobs/02aWebJobsList.png
[NewContinuousJob]: ./media/web-sites-create-web-jobs/03aNewContinuousJob.png
[NewScheduledJob]: ./media/web-sites-create-web-jobs/04aNewScheduledJob.png
[SchdRecurrence]: ./media/web-sites-create-web-jobs/05SchdRecurrence.png
[SchdStart]: ./media/web-sites-create-web-jobs/06SchdStart.png
[SchdStartOn]: ./media/web-sites-create-web-jobs/07SchdStartOn.png
[SchdRecurEvery]: ./media/web-sites-create-web-jobs/08SchdRecurEvery.png
[SchdWeeksOnParticular]: ./media/web-sites-create-web-jobs/09SchdWeeksOnParticular.png
[SchdMonthsOnPartDays]: ./media/web-sites-create-web-jobs/10SchdMonthsOnPartDays.png
[SchdMonthsOnPartWeekDays]: ./media/web-sites-create-web-jobs/11SchdMonthsOnPartWeekDays.png
[SchdMonthsOnPartWeekDaysOccurences]: ./media/web-sites-create-web-jobs/12SchdMonthsOnPartWeekDaysOccurences.png
[RunOnce]: ./media/web-sites-create-web-jobs/13RunOnce.png
[WebJobsListWithSeveralJobs]: ./media/web-sites-create-web-jobs/13WebJobsListWithSeveralJobs.png
[WebJobLogs]: ./media/web-sites-create-web-jobs/14WebJobLogs.png
[WebJobDetails]: ./media/web-sites-create-web-jobs/15WebJobDetails.png
[WebJobRunDetails]: ./media/web-sites-create-web-jobs/16WebJobRunDetails.png
[DownloadLogOutput]: ./media/web-sites-create-web-jobs/17DownloadLogOutput.png
[WebJobsLinkToDashboardList]: ./media/web-sites-create-web-jobs/18WebJobsLinkToDashboardList.png
[WebJobsListInJobsDashboard]: ./media/web-sites-create-web-jobs/19WebJobsListInJobsDashboard.png
[LinkToScheduler]: ./media/web-sites-create-web-jobs/31LinkToScheduler.png
[SchedulerPortal]: ./media/web-sites-create-web-jobs/32SchedulerPortal.png
[JobActionPageInScheduler]: ./media/web-sites-create-web-jobs/33JobActionPageInScheduler.png

