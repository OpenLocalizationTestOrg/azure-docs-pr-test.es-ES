---
title: Ejecutar tareas en segundo plano con trabajos web
description: "Obtenga información sobre cómo ejecutar tareas en segundo plano en aplicaciones web de Azure."
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
ms.openlocfilehash: 3f8ae748e3d9c6b4e342536926a52b4e8f37ee51
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="run-background-tasks-with-webjobs"></a><span data-ttu-id="9a7d7-103">Ejecutar tareas en segundo plano con trabajos web</span><span class="sxs-lookup"><span data-stu-id="9a7d7-103">Run Background tasks with WebJobs</span></span>
## <a name="overview"></a><span data-ttu-id="9a7d7-104">Información general</span><span class="sxs-lookup"><span data-stu-id="9a7d7-104">Overview</span></span>
<span data-ttu-id="9a7d7-105">Puede ejecutar programas o scripts en trabajos web en su aplicación web de [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) de tres maneras: a petición, de forma continua o según una programación.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-105">You can run programs or scripts in WebJobs in your [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) web app in three ways: on demand, continuously, or on a schedule.</span></span> <span data-ttu-id="9a7d7-106">No hay ningún coste adicional en el uso de trabajos web.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-106">There is no additional cost to use WebJobs.</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="9a7d7-107">En este artículo se muestra cómo implementar Webjobs con el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9a7d7-107">This article shows how to deploy WebJobs by using the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="9a7d7-108">Para obtener información sobre cómo implementar con Visual Studio o con un proceso de entrega continua, consulte [Implementación de Webjobs de Azure en aplicaciones web](websites-dotnet-deploy-webjobs.md).</span><span class="sxs-lookup"><span data-stu-id="9a7d7-108">For information about how to deploy by using Visual Studio or a continuous delivery process, see [How to Deploy Azure WebJobs to Web Apps](websites-dotnet-deploy-webjobs.md).</span></span>

<span data-ttu-id="9a7d7-109">El SDK de trabajos web de Azure simplifica muchas de las tareas de programación de trabajos web.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-109">The Azure WebJobs SDK simplifies many WebJobs programming tasks.</span></span> <span data-ttu-id="9a7d7-110">Para obtener más información, consulte [¿Qué es el SDK de Webjobs?](websites-dotnet-webjobs-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="9a7d7-110">For more information, see [What is the WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

 <span data-ttu-id="9a7d7-111">Azure Functions proporciona otra manera de ejecutar programas y scripts desde un entorno sin servidor o desde una aplicación de App Service.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-111">Azure Functions provides another way to run programs and scripts from either a serverless environment or from an App Service app.</span></span> <span data-ttu-id="9a7d7-112">Para obtener más información, consulte [Información general sobre Funciones de Azure](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9a7d7-112">For more information, see [Azure Functions overview](../azure-functions/functions-overview.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="9a7d7-113"><a name="acceptablefiles"></a>Tipos de archivo válidos para scripts o programas</span><span class="sxs-lookup"><span data-stu-id="9a7d7-113"><a name="acceptablefiles"></a>Acceptable file types for scripts or programs</span></span>
<span data-ttu-id="9a7d7-114">Se aceptan los siguientes tipos de archivo:</span><span class="sxs-lookup"><span data-stu-id="9a7d7-114">The following file types are accepted:</span></span>

* <span data-ttu-id="9a7d7-115">.cmd, .bat, .exe (con windows cmd)</span><span class="sxs-lookup"><span data-stu-id="9a7d7-115">.cmd, .bat, .exe (using windows cmd)</span></span>
* <span data-ttu-id="9a7d7-116">.ps1 (con powershell)</span><span class="sxs-lookup"><span data-stu-id="9a7d7-116">.ps1 (using powershell)</span></span>
* <span data-ttu-id="9a7d7-117">.sh (con bash)</span><span class="sxs-lookup"><span data-stu-id="9a7d7-117">.sh (using bash)</span></span>
* <span data-ttu-id="9a7d7-118">.php (con php)</span><span class="sxs-lookup"><span data-stu-id="9a7d7-118">.php (using php)</span></span>
* <span data-ttu-id="9a7d7-119">.py (con python)</span><span class="sxs-lookup"><span data-stu-id="9a7d7-119">.py (using python)</span></span>
* <span data-ttu-id="9a7d7-120">.js (con node)</span><span class="sxs-lookup"><span data-stu-id="9a7d7-120">.js (using node)</span></span>
* <span data-ttu-id="9a7d7-121">.jar (con java)</span><span class="sxs-lookup"><span data-stu-id="9a7d7-121">.jar (using java)</span></span>

## <span data-ttu-id="9a7d7-122"><a name="CreateOnDemand"></a>Creación de un trabajo web a petición en el portal</span><span class="sxs-lookup"><span data-stu-id="9a7d7-122"><a name="CreateOnDemand"></a>Create an on demand WebJob in the portal</span></span>
1. <span data-ttu-id="9a7d7-123">En la hoja **Aplicación web** de [Azure Portal](https://portal.azure.com), haga clic en **Toda la configuración > Webjobs** para mostrar la hoja **Webjobs**.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-123">In the **Web App** blade of the [Azure Portal](https://portal.azure.com), click **All settings > WebJobs** to show the **WebJobs** blade.</span></span>
   
    ![Hoja de WebJobs](./media/web-sites-create-web-jobs/wjblade.png)
2. <span data-ttu-id="9a7d7-125">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-125">Click **Add**.</span></span> <span data-ttu-id="9a7d7-126">Aparecerá el cuadro de diálogo **Agregar Webjob** .</span><span class="sxs-lookup"><span data-stu-id="9a7d7-126">The **Add WebJob** dialog appears.</span></span>
   
    ![Adición de hoja de WebJobs](./media/web-sites-create-web-jobs/addwjblade.png)
3. <span data-ttu-id="9a7d7-128">En **Nombre**, escriba un nombre para el trabajo web.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-128">Under **Name**, provide a name for the WebJob.</span></span> <span data-ttu-id="9a7d7-129">El nombre debe comenzar con una letra o un número y no puede contener ningún carácter especial salvo "-" y "_".</span><span class="sxs-lookup"><span data-stu-id="9a7d7-129">The name must start with a letter or a number and cannot contain any special characters other than "-" and "_".</span></span>
4. <span data-ttu-id="9a7d7-130">En el cuadro **Cómo ejecutar**, elija **Ejecutar a petición**.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-130">In the **How to Run** box, choose **Run on Demand**.</span></span>
5. <span data-ttu-id="9a7d7-131">En el cuadro **Carga de archivos** , haga clic en el icono de la carpeta y busque el archivo zip que contiene el script.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-131">In the **File Upload** box, click the folder icon and browse to the zip file that contains your script.</span></span> <span data-ttu-id="9a7d7-132">El archivo zip debe contener el ejecutable (.exe, .cmd, .bat, .sh, .php, .py, .js) así como cualquier archivo complementario necesario para ejecutar el programa o script.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-132">The zip file should contain your executable (.exe .cmd .bat .sh .php .py .js) as well as any supporting files needed to run the program or script.</span></span>
6. <span data-ttu-id="9a7d7-133">Active **Crear** para cargar el script de su aplicación web.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-133">Check **Create** to upload the script to your web app.</span></span> 
   
    <span data-ttu-id="9a7d7-134">El nombre especificado para el trabajo web aparece en la lista de la hoja **WebJobs** .</span><span class="sxs-lookup"><span data-stu-id="9a7d7-134">The name you specified for the WebJob appears in the list on the **WebJobs** blade.</span></span>
7. <span data-ttu-id="9a7d7-135">Para ejecutar el trabajo web, haga clic en su nombre en la lista y haga clic en **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-135">To run the WebJob, right-click its name in the list and click **Run**.</span></span>
   
    ![Ejecución de WebJobs](./media/web-sites-create-web-jobs/runondemand.png)

## <span data-ttu-id="9a7d7-137"><a name="CreateContinuous"></a>Creación de un trabajo web de ejecución continua</span><span class="sxs-lookup"><span data-stu-id="9a7d7-137"><a name="CreateContinuous"></a>Create a continuously running WebJob</span></span>
1. <span data-ttu-id="9a7d7-138">Para crear un WebJob de ejecución continua, siga los pasos descritos para crear un WebJob que se ejecuta solo una vez, pero en el cuadro **Cómo ejecutar**, elija **Continua**.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-138">To create a continuously executing WebJob, follow the same steps for creating a WebJob that runs once, but in the **How to Run** box, choose **Continuous**.</span></span>
2. <span data-ttu-id="9a7d7-139">Para iniciar o detener un WebJob continuo, haga clic con el botón derecho en el WebJob en la lista y haga clic en **Iniciar** o **Detener**.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-139">To start or stop a continuous WebJob, right-click the WebJob in the list and click **Start** or **Stop**.</span></span>

> [!NOTE]
> <span data-ttu-id="9a7d7-140">Si la aplicación web se ejecuta en más de una instancia, se ejecutará un trabajo web continuamente en todas las instancias.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-140">If your web app runs on more than one instance, a continuously running WebJob will run on all of your instances.</span></span> <span data-ttu-id="9a7d7-141">Los Trabajos web a petición o programados se ejecutan en una única instancia seleccionada por Microsoft Azure para el equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-141">On-demand and scheduled WebJobs run on a single instance selected for load balancing by Microsoft Azure.</span></span>
> 
> <span data-ttu-id="9a7d7-142">Para que los WebJobs continuos sigan ejecutándose en todas las instancias y de forma confiable, habilite la configuración Siempre activado* de la aplicación web, en caso contrario, es posible que dejen de funcionar cuando el sitio host SCM esté inactivo durante demasiado tiempo.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-142">For Continuous WebJobs to run reliably and on all instances, enable the Always On* configuration setting for the web app otherwise they can stop running when the SCM host site has been idle for too long.</span></span>
> 
> 

## <span data-ttu-id="9a7d7-143"><a name="CreateScheduledCRON"></a>Creación de un trabajo web programado utilizando una expresión CRON</span><span class="sxs-lookup"><span data-stu-id="9a7d7-143"><a name="CreateScheduledCRON"></a>Create a scheduled WebJob using a CRON expression</span></span>
<span data-ttu-id="9a7d7-144">Esta técnica está disponible para aplicaciones web que se ejecutan en modo Básico, Estándar o Premium y requiere que la opción **AlwaysOn** esté habilitada en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-144">This technique is available to Web Apps running in Basic, Standard or Premium mode, and requires the **Always On** setting to be enabled on the app.</span></span>

<span data-ttu-id="9a7d7-145">Para convertir un trabajo web a petición en un trabajo web programado, basta con incluir un archivo `settings.job` en la raíz del archivo ZIP del trabajo web.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-145">To turn an On Demand WebJob into a scheduled WebJob, simply include a `settings.job` file at the root of your WebJob zip file.</span></span> <span data-ttu-id="9a7d7-146">Este archivo JSON debe incluir una propiedad `schedule` con una [expresión CRON](https://en.wikipedia.org/wiki/Cron)como la siguiente.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-146">This JSON file should include a `schedule` property with a [CRON expression](https://en.wikipedia.org/wiki/Cron), per example below.</span></span>

<span data-ttu-id="9a7d7-147">La expresión CRON se compone de 6 campos: `{second} {minute} {hour} {day} {month} {day of the week}`.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-147">The CRON expression is composed of 6 fields: `{second} {minute} {hour} {day} {month} {day of the week}`.</span></span>

<span data-ttu-id="9a7d7-148">Por ejemplo, para desencadenar el trabajo web cada 15 minutos, la `settings.job` tendría:</span><span class="sxs-lookup"><span data-stu-id="9a7d7-148">For example, to trigger your WebJob every 15 minutes, your `settings.job` would have:</span></span>

```json
{
    "schedule": "0 */15 * * * *"
}
``` 

<span data-ttu-id="9a7d7-149">Otros ejemplos de programación CRON:</span><span class="sxs-lookup"><span data-stu-id="9a7d7-149">Other CRON schedule examples:</span></span>

* <span data-ttu-id="9a7d7-150">Cada hora (es decir, siempre que el número de minutos sea 0): `0 0 * * * *`</span><span class="sxs-lookup"><span data-stu-id="9a7d7-150">Every hour (i.e. whenever the count of minutes is 0): `0 0 * * * *`</span></span> 
* <span data-ttu-id="9a7d7-151">Cada hora de 9 a 17 horas: `0 0 9-17 * * *`</span><span class="sxs-lookup"><span data-stu-id="9a7d7-151">Every hour from 9 AM to 5 PM: `0 0 9-17 * * *`</span></span> 
* <span data-ttu-id="9a7d7-152">A las 9:30 todos los días: `0 30 9 * * *`</span><span class="sxs-lookup"><span data-stu-id="9a7d7-152">At 9:30 AM every day: `0 30 9 * * *`</span></span>
* <span data-ttu-id="9a7d7-153">A las 9:30 cada día de lunes a viernes: `0 30 9 * * 1-5`</span><span class="sxs-lookup"><span data-stu-id="9a7d7-153">At 9:30 AM every week day: `0 30 9 * * 1-5`</span></span>

<span data-ttu-id="9a7d7-154">**Nota**: Cuando se implemente un WebJob desde Visual Studio, asegúrese de marcar las propiedades de archivo `settings.job` como "Copiar si es posterior".</span><span class="sxs-lookup"><span data-stu-id="9a7d7-154">**Note**: when deploying a WebJob from Visual Studio, make sure to mark your `settings.job` file properties as 'Copy if newer'.</span></span>

## <span data-ttu-id="9a7d7-155"><a name="CreateScheduled"></a>Creación de un trabajo web programado mediante el programador de Azure</span><span class="sxs-lookup"><span data-stu-id="9a7d7-155"><a name="CreateScheduled"></a>Create a scheduled WebJob using the Azure Scheduler</span></span>
<span data-ttu-id="9a7d7-156">La técnica alternativa siguiente hace uso del programador de Azure.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-156">The following alternate technique makes use of the Azure Scheduler.</span></span> <span data-ttu-id="9a7d7-157">En este caso, el trabajo web no tiene ningún conocimiento directo de la programación.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-157">In this case, your WebJob does not have any direct knowledge of the schedule.</span></span> <span data-ttu-id="9a7d7-158">En su lugar, se debe configurar el programador de Azure para desencadenar el trabajo web según una programación.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-158">Instead, the Azure Scheduler gets configured to trigger your WebJob on a schedule.</span></span> 

<span data-ttu-id="9a7d7-159">El Portal de Azure aún no tiene la capacidad para crear un trabajo web programado, pero hasta que se agregue esa característica, puede hacerlo con el [Portal clásico](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="9a7d7-159">The Azure Portal doesn't yet have the ability to create a scheduled WebJob, but until that feature is added you can do it by using the [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="9a7d7-160">En el [Portal clásico](http://manage.windowsazure.com) , vaya a la página del trabajo web y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-160">In the [classic portal](http://manage.windowsazure.com) go to the WebJob page and click **Add**.</span></span>
2. <span data-ttu-id="9a7d7-161">En el cuadro **Cómo ejecutar**, seleccione **Ejecutar según una programación**.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-161">In the **How to Run** box, choose **Run on a schedule**.</span></span>
   
    ![Nuevo trabajo programado][NewScheduledJob]
3. <span data-ttu-id="9a7d7-163">Elija una región en la opción **Región del programador** para el trabajo y luego haga clic en la flecha de la parte inferior derecha del cuadro de diálogo para continuar a la pantalla siguiente.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-163">Choose the **Scheduler Region** for your job, and then click the arrow on the bottom right of the dialog to proceed to the next screen.</span></span>
4. <span data-ttu-id="9a7d7-164">En el cuadro de diálogo **Crear trabajo**, elija el tipo de **periodicidad** que quiere: **Trabajo único** o **Trabajo periódico**.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-164">In the **Create Job** dialog, choose the type of **Recurrence** you want: **One-time job** or **Recurring job**.</span></span>
   
    ![Periodicidad de la programación][SchdRecurrence]
5. <span data-ttu-id="9a7d7-166">Elija también una hora de **inicio**: **Ahora** o **En un momento determinado**.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-166">Also choose a **Starting** time: **Now** or **At a specific time**.</span></span>
   
    ![Hora de inicio de la programación][SchdStart]
6. <span data-ttu-id="9a7d7-168">Si desea comenzar a una hora determinada, elija los valores de la hora de inicio en **Iniciar a las**.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-168">If you want to start at a specific time, choose your starting time values under **Starting On**.</span></span>
   
    ![Inicio de la programación a una hora determinada][SchdStartOn]
7. <span data-ttu-id="9a7d7-170">Si elige un trabajo periódico, en la opción **Repetir cada** podrá especificar la frecuencia de la periodicidad y en la opción **Finalizar a las** podrá especificar una hora de finalización.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-170">If you chose a recurring job, you have the **Recur Every** option to specify the frequency of occurrence and the **Ending On** option to specify an ending time.</span></span>
   
    ![Periodicidad de la programación][SchdRecurEvery]
8. <span data-ttu-id="9a7d7-172">Si elige **Semanas**, puede seleccionar la casilla **Según un programa determinado** y especificar los días de la semana en los que quiere que se ejecute el trabajo.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-172">If you choose **Weeks**, you can select the **On a Particular Schedule** box and specify the days of the week that you want the job to run.</span></span>
   
    ![Días de la semana de la programación][SchdWeeksOnParticular]
9. <span data-ttu-id="9a7d7-174">Si elige **Meses** y selecciona la casilla **Según un programa determinado** podrá establecer que el trabajo se ejecute en un número de días determinado del mes seleccionándolos en la opción **Días**.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-174">If you choose **Months** and select the **On a Particular Schedule** box, you can set the job to run on particular numbered **Days** in the month.</span></span> 
   
    ![Fechas determinadas del mes de la programación][SchdMonthsOnPartDays]
10. <span data-ttu-id="9a7d7-176">Si elige **Días de la semana**, podrá seleccionar el día o días de la semana del mes en los que desea que se ejecute el trabajo.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-176">If you choose **Week Days**, you can select which day or days of the week in the month you want the job to run on.</span></span>
    
     ![Programación en días determinados de la semana de un mes][SchdMonthsOnPartWeekDays]
11. <span data-ttu-id="9a7d7-178">Finalmente, también puede utilizar la opción **Repeticiones** para elegir en qué semana del mes (primera, segunda, tercera, etc.) desea que se ejecute el trabajo en los días de la semana especificados.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-178">Finally, you can also use the **Occurrences** option to choose which week in the month (first, second, third etc.) you want the job to run on the week days you specified.</span></span>
    
    ![Programación en días de la semana específicos de semanas determinadas][SchdMonthsOnPartWeekDaysOccurences]
12. <span data-ttu-id="9a7d7-180">Después de haber creado uno o varios trabajos, sus nombres aparecerán en la pestaña WebJobs con su estado, tipo de programación y otra información.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-180">After you have created one or more jobs, their names will appear on the WebJobs tab with their status, schedule type, and other information.</span></span> <span data-ttu-id="9a7d7-181">Se conserva la información histórica de los últimos 30 WebJobs.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-181">Historical information for the last 30  WebJobs is maintained.</span></span>
    
    ![Lista de trabajos][WebJobsListWithSeveralJobs]

### <span data-ttu-id="9a7d7-183"><a name="Scheduler"></a>Trabajos programados y Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="9a7d7-183"><a name="Scheduler"></a>Scheduled jobs and Azure Scheduler</span></span>
<span data-ttu-id="9a7d7-184">Los trabajos programados se pueden configurar adicionalmente en las páginas del Programador de Azure del [Portal clásico](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="9a7d7-184">Scheduled jobs can be further configured in the Azure Scheduler pages of the [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="9a7d7-185">En la página WebJobs, haga clic en el vínculo **Programar** para desplazarse a la página del portal del Programador de Azure.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-185">On the WebJobs page, click the job's **schedule** link to navigate to the Azure Scheduler portal page.</span></span> 
   
   ![Vínculo al Programador de Azure][LinkToScheduler]
2. <span data-ttu-id="9a7d7-187">En la página del Programador, haga clic en el trabajo.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-187">On the Scheduler page, click the job.</span></span>
   
    ![Trabajo en la página del portal del Programador][SchedulerPortal]
3. <span data-ttu-id="9a7d7-189">Se abre la página **Acción del trabajo** , donde puede configurar adicionalmente el trabajo.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-189">The **Job Action** page opens, where you can further configure the job.</span></span> 
   
    ![Página de acción del trabajo en el Programador][JobActionPageInScheduler]

## <span data-ttu-id="9a7d7-191"><a name="ViewJobHistory"></a>Visualización del historial de trabajos</span><span class="sxs-lookup"><span data-stu-id="9a7d7-191"><a name="ViewJobHistory"></a>View the job history</span></span>
1. <span data-ttu-id="9a7d7-192">Para ver el historial de ejecución de un trabajo, incluidos los trabajos creados con el SDK de WebJobs, haga clic en su vínculo correspondiente en la columna **Registros** de la hoja WebJobs.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-192">To view the execution history of a job, including jobs created with the WebJobs SDK, click  its corresponding link under the **Logs** column of the WebJobs blade.</span></span> <span data-ttu-id="9a7d7-193">(Puede utilizar el icono del Portapapeles para copiar la dirección URL de la página de archivo de registro en el Portapapeles si lo desea).</span><span class="sxs-lookup"><span data-stu-id="9a7d7-193">(You can use the clipboard icon to copy the URL of the log file page to the clipboard if you wish.)</span></span>
   
    ![Vínculo de registros](./media/web-sites-create-web-jobs/wjbladelogslink.png)
2. <span data-ttu-id="9a7d7-195">Al hacer clic en el vínculo, se abre la página de detalles del trabajo web.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-195">Clicking the link opens the details page for the WebJob.</span></span> <span data-ttu-id="9a7d7-196">En esta página se muestra el nombre de la ejecución del comando, las últimas veces que se ha ejecutado y si se ha ejecutado correctamente o no.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-196">This page shows you the name of the command run, the last times it ran, and its success or failure.</span></span> <span data-ttu-id="9a7d7-197">En **Ejecuciones del trabajo recientes**, haga clic una vez para ver más detalles.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-197">Under **Recent job runs**, click a time to see further details.</span></span>
   
    ![Detalles del trabajo web][WebJobDetails]
3. <span data-ttu-id="9a7d7-199">Se muestra la página **Detalles de ejecución del trabajo web** .</span><span class="sxs-lookup"><span data-stu-id="9a7d7-199">The **WebJob Run Details** page appears.</span></span> <span data-ttu-id="9a7d7-200">Haga clic en **Alternar salida** para ver el texto del contenido del registro.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-200">Click **Toggle Output** to see the text of the log contents.</span></span> <span data-ttu-id="9a7d7-201">El registro de resultados se muestra en formato de texto.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-201">The output log is in text format.</span></span> 
   
    ![Detalles de ejecución del trabajo web][WebJobRunDetails]
4. <span data-ttu-id="9a7d7-203">Para ver el texto de salida en otra ventana del explorador, haga clic en el vínculo de **descarga** .</span><span class="sxs-lookup"><span data-stu-id="9a7d7-203">To see the output text in a separate browser window, click the **download** link.</span></span> <span data-ttu-id="9a7d7-204">Para descargar el texto propiamente dicho, haga clic con el botón secundario en el vínculo y utilice las opciones del explorador para guardar el contenido del archivo.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-204">To download the text itself, right-click the link and use your browser options to save the file contents.</span></span>
   
    ![Resultado del registro de descarga][DownloadLogOutput]
5. <span data-ttu-id="9a7d7-206">El vínculo **Trabajos web** situado en la parte superior de la página ofrece una forma cómoda de obtener una lista de los trabajos web en el panel del historial.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-206">The **WebJobs** link at the top of the page provides a convenient way to get to a list of WebJobs on the history dashboard.</span></span>
   
    ![Vínculo a la lista de WebJobs][WebJobsLinkToDashboardList]
   
    ![Lista de WebJobs el panel del historial][WebJobsListInJobsDashboard]
   
    <span data-ttu-id="9a7d7-209">Al hacer clic en uno de estos vínculos, obtendrá acceso a la página de detalles de WebJob para el trabajo que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-209">Clicking one of these links takes you to the WebJob Details page for the job you selected.</span></span>

## <span data-ttu-id="9a7d7-210"><a name="WHPNotes"></a>Notas</span><span class="sxs-lookup"><span data-stu-id="9a7d7-210"><a name="WHPNotes"></a>Notes</span></span>
* <span data-ttu-id="9a7d7-211">Las aplicaciones web en modo libre pueden agotar su tiempo de espera tras 20 minutos si no se realizan solicitudes al sitio de scm (implementación) y el portal de la aplicación web no está abierto en Azure.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-211">Web apps in Free mode can time out after 20 minutes if there are no requests to the scm (deployment) site and the web app's portal is not open in Azure.</span></span> <span data-ttu-id="9a7d7-212">Las solicitudes al sitio real no restablecerán esto.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-212">Requests to the actual site will not reset this.</span></span>
* <span data-ttu-id="9a7d7-213">Debe escribirse el código para un trabajo continuo para que se ejecute en un bucle infinito.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-213">Code for a continuous job needs to be written to run in an endless loop.</span></span>
* <span data-ttu-id="9a7d7-214">Los trabajos continuos solo se ejecutan continuamente cuando la aplicación web está activa.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-214">Continuous jobs run continuously only when the web app is up.</span></span>
* <span data-ttu-id="9a7d7-215">Los modos básico y estándar ofrecen la característica Siempre disponible que, cuando está habilitada, impide que las aplicaciones web se vuelvan inactivas.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-215">Basic and Standard modes offer the Always On feature which, when enabled, prevents web apps from becoming idle.</span></span>
* <span data-ttu-id="9a7d7-216">Solo se pueden depurar WebJobs que se ejecutan continuamente.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-216">You can only debug continuously running WebJobs.</span></span> <span data-ttu-id="9a7d7-217">No se admite la depuración de WebJobs programada o a petición.</span><span class="sxs-lookup"><span data-stu-id="9a7d7-217">Debugging scheduled or on-demand WebJobs is not supported.</span></span>

## <span data-ttu-id="9a7d7-218"><a name="NextSteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9a7d7-218"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="9a7d7-219">Para obtener más información, consulte [Recursos recomendados de WebJobs de Azure][WebJobsRecommendedResources].</span><span class="sxs-lookup"><span data-stu-id="9a7d7-219">For more information, see [Azure WebJobs Recommended Resources][WebJobsRecommendedResources].</span></span>

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

