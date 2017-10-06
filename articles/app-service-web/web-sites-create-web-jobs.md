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
# <a name="run-background-tasks-with-webjobs"></a>Ejecutar tareas en segundo plano con trabajos web
## <a name="overview"></a>Información general
Puede ejecutar programas o scripts en trabajos web en su aplicación web de [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) de tres maneras: a petición, de forma continua o según una programación. No hay ningún toouse costo adicional trabajos Web.

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

Este artículo muestra cómo toodeploy trabajos Web mediante el uso de Hola [Portal de Azure](https://portal.azure.com). Para obtener información acerca de cómo toodeploy mediante Visual Studio o un proceso de entrega continua, vea [cómo tooDeploy WebJobs de Azure tooWeb aplicaciones](websites-dotnet-deploy-webjobs.md).

Hola SDK de WebJobs de Azure simplifica muchas tareas de programación de trabajos Web. Para obtener más información, consulte [¿qué es hello SDK de WebJobs](websites-dotnet-webjobs-sdk.md).

 Las funciones de Azure proporciona otro toorun funcionamiento de los programas y secuencias de comandos desde un entorno sin servidor o desde una aplicación de servicio de aplicaciones. Para obtener más información, consulte [Información general sobre Funciones de Azure](../azure-functions/functions-overview.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="acceptablefiles"></a>Tipos de archivo válidos para scripts o programas
se acepta Hola siguientes tipos de archivo:

* .cmd, .bat, .exe (con windows cmd)
* .ps1 (con powershell)
* .sh (con bash)
* .php (con php)
* .py (con python)
* .js (con node)
* .jar (con java)

## <a name="CreateOnDemand"></a>Crear un informe a petición trabajo Web en el portal de Hola
1. Hola **aplicación Web** hoja de hello [Portal de Azure](https://portal.azure.com), haga clic en **toda la configuración > trabajos Web** tooshow hello **WebJobs** hoja.
   
    ![Hoja de WebJobs](./media/web-sites-create-web-jobs/wjblade.png)
2. Haga clic en **Agregar**. Hola **Agregar trabajo Web** aparece el cuadro de diálogo.
   
    ![Adición de hoja de WebJobs](./media/web-sites-create-web-jobs/addwjblade.png)
3. En **nombre**, proporcione un nombre para hello trabajo Web. nombre de Hello debe empezar por una letra o un número y no puede contener ningún carácter especial salvo "-" y "_".
4. Hola **cómo tooRun** cuadro, elija **ejecutar a petición**.
5. Hola **cargar archivo** cuadro, haga clic en el icono de carpeta de Hola y examinar toohello zip que contiene el script. archivo zip de Hello debe contener su archivo ejecutable (.exe .cmd .bat .sh .php .py .js), así como los archivos auxiliares necesarios toorun Hola programa o script.
6. Comprobar **crear** tooupload Hola script tooyour web app. 
   
    Hello nombre especificado para hello trabajo Web aparece en lista Hola Hola **WebJobs** hoja.
7. Hola toorun trabajo Web, haga clic en su nombre en la lista de Hola y haga clic en **ejecutar**.
   
    ![Ejecución de WebJobs](./media/web-sites-create-web-jobs/runondemand.png)

## <a name="CreateContinuous"></a>Creación de un trabajo web de ejecución continua
1. toocreate un trabajo Web que está ejecutando continuamente, siga Hola mismos pasos para crear un trabajo Web que se ejecuta una vez, pero en hello **cómo tooRun** cuadro, elija **Continuous**.
2. toostart o detener un trabajo Web continuo, haga clic en hello trabajo Web en la lista de Hola y haga clic en **iniciar** o **detener**.

> [!NOTE]
> Si la aplicación web se ejecuta en más de una instancia, se ejecutará un trabajo web continuamente en todas las instancias. Los Trabajos web a petición o programados se ejecutan en una única instancia seleccionada por Microsoft Azure para el equilibrio de carga.
> 
> Para los trabajos Web continuos toorun forma confiable y en todas las instancias, habilitar Hola Always On * valor de configuración para web aplicación hello en caso contrario puede interrumpir la ejecución cuando el sitio de hello SCM host ha estado inactivo durante demasiado tiempo.
> 
> 

## <a name="CreateScheduledCRON"></a>Creación de un trabajo web programado utilizando una expresión CRON
Esta técnica es aplicaciones tooWeb disponibles que se ejecutan en modo básico, estándar o Premium y requiere hello **Always On** establecer toobe habilitada en la aplicación hello.

tooturn un en trabajo Web petición en un trabajo Web programado, basta con incluir un `settings.job` archivo en hello raíz del archivo zip trabajo Web. Este archivo JSON debe incluir una propiedad `schedule` con una [expresión CRON](https://en.wikipedia.org/wiki/Cron)como la siguiente.

Hola expresión CRON se compone de 6 campos: `{second} {minute} {hour} {day} {month} {day of hello week}`.

Por ejemplo, tootrigger su trabajo Web cada 15 minutos, el `settings.job` tendría:

```json
{
    "schedule": "0 */15 * * * *"
}
``` 

Otros ejemplos de programación CRON:

* Cada hora (es decir, siempre que sea recuento Hola de minutos es 0):`0 0 * * * *` 
* Cada hora de 9 AM too5 PM:`0 0 9-17 * * *` 
* A las 9:30 todos los días: `0 30 9 * * *`
* A las 9:30 cada día de lunes a viernes: `0 30 9 * * 1-5`

**Tenga en cuenta**: al implementar un trabajo Web desde Visual Studio, asegúrese de que toomark su `settings.job` propiedades del archivo como "Copiar si es posterior".

## <a name="CreateScheduled"></a>Crear un trabajo Web programado mediante Hola programador de Azure
Hola siguiendo la técnica alternativa hace uso de hello Azure Scheduler. En este caso, el trabajo Web no tiene ningún conocimiento directo de programación de Hola. En su lugar, hello Azure Scheduler obtiene tootrigger configurado su trabajo Web según una programación. 

Hola Portal de Azure no tiene todavía a Hola capacidad toocreate un trabajo Web programado, pero hasta que se agregue esta característica puede hacer mediante el uso de hello [portal clásico](http://manage.windowsazure.com).

1. Hola [portal clásico](http://manage.windowsazure.com) toohello página de trabajo Web y haga clic en **agregar**.
2. Hola **cómo tooRun** cuadro, elija **ejecutar según una programación**.
   
    ![Nuevo trabajo programado][NewScheduledJob]
3. Elija hello **programador región** para su trabajo y, a continuación, haga clic en la flecha Hola Hola parte inferior derecha pantalla siguiente de bienvenida diálogo tooproceed toohello.
4. Hola **crear trabajo de** cuadro de diálogo, elija tipo hello de **periodicidad** desea: **trabajo único** o **trabajo periódica**.
   
    ![Periodicidad de la programación][SchdRecurrence]
5. Elija también una hora de **inicio**: **Ahora** o **En un momento determinado**.
   
    ![Hora de inicio de la programación][SchdStart]
6. Si desea toostart en un momento determinado, elija los valores de tiempo inicial en **a partir de**.
   
    ![Inicio de la programación a una hora determinada][SchdStartOn]
7. Si ha elegido un trabajo periódico, tiene hello **Repetir cada** opción frecuencia de hello toospecify de repetición y hello **final en** opción toospecify una hora de finalización.
   
    ![Periodicidad de la programación][SchdRecurEvery]
8. Si elige **semanas**, puede seleccionar hello **en una programación determinada** cuadro y especifique días de saludo de la semana de Hola que desee Hola toorun de trabajo.
   
    ![Días de programación de hello semana][SchdWeeksOnParticular]
9. Si elige **meses** y seleccione hello **en una programación determinada** cuadro, puede establecer toorun de trabajo de hello en particular numerado **días** mes Hola. 
   
    ![Programar fechas concretas en hello mes][SchdMonthsOnPartDays]
10. Si elige **días de la semana**, puede seleccionar qué día o días de la semana de hello en mes de Hola que desea Hola toorun de trabajo en.
    
     ![Programación en días determinados de la semana de un mes][SchdMonthsOnPartWeekDays]
11. Por último, también puede usar hello **apariciones** opción toochoose qué semana del mes de Hola (primera, segunda, tercera etc.) desea toorun de trabajo de hello en hello días de la semana especificado.
    
    ![Programación en días de la semana específicos de semanas determinadas][SchdMonthsOnPartWeekDaysOccurences]
12. Después de haber creado uno o varios trabajos, sus nombres aparecerán en la ficha de trabajos Web Hola con su estado, tipo de programación y otra información. Se mantiene la información histórica de hello últimos 30 trabajos Web.
    
    ![Lista de trabajos][WebJobsListWithSeveralJobs]

### <a name="Scheduler"></a>Trabajos programados y Programador de Azure
Los trabajos programados se pueden configurar aún más en páginas de Azure Scheduler Hola de hello [portal clásico](http://manage.windowsazure.com).

1. En la página de trabajos Web hello, haga clic en del trabajo de hello **programación** página del portal de Azure Scheduler de vínculo toonavigate toohello. 
   
   ![Vínculo tooAzure programador][LinkToScheduler]
2. En la página de programador de hello, haga clic en trabajo Hola.
   
    ![Trabajo en la página del portal de programador Hola][SchedulerPortal]
3. Hola **acción de trabajo** página se abre, donde puede seguir configurando trabajo Hola. 
   
    ![Página de acción del trabajo en el Programador][JobActionPageInScheduler]

## <a name="ViewJobHistory"></a>Ver historial de trabajos de Hola
1. historial de ejecución de hello tooview de un trabajo, incluidos los trabajos creados con hello SDK de WebJobs, haga clic en el vínculo correspondiente, bajo hello **registros** columna de hoja de WebJobs de Hola. (Puede usar Hola Portapapeles toocopy Hola dirección URL de icono del Portapapeles de hello registro archivo página toohello si lo desea).
   
    ![Vínculo de registros](./media/web-sites-create-web-jobs/wjbladelogslink.png)
2. Si hace clic en vínculo Hola abrirá la página de detalles de Hola de hello trabajo Web. Esta página muestra Hola nombre de la ejecución de comandos de Hola Hola últimas veces que se ejecutó, y su éxito o fracaso. En **ejecuciones recientes de trabajos**, haga clic en un toosee más detalles de tiempo.
   
    ![Detalles del trabajo web][WebJobDetails]
3. Hola **detalles de ejecución de trabajo Web** aparece la página. Haga clic en **alternar salida** toosee texto de hello de contenido del registro de hello. registro de salida de Hello está en formato de texto. 
   
    ![Detalles de ejecución del trabajo web][WebJobRunDetails]
4. texto de salida de hello toosee en otra ventana del explorador, haga clic en hello **descargar** vínculo. toodownload Hola propio texto, haga clic en el vínculo de Hola y usar el contenido del archivo explorador opciones toosave Hola.
   
    ![Resultado del registro de descarga][DownloadLogOutput]
5. Hola **WebJobs** vínculo situado en la parte superior de Hola de página de hello proporciona una lista de tooa de tooget de forma cómoda de trabajos Web en el panel de historial de Hola.
   
    ![Lista de vínculos tooWebJobs][WebJobsLinkToDashboardList]
   
    ![Lista de WebJobs el panel del historial][WebJobsListInJobsDashboard]
   
    Haga clic en uno de estos vínculos le toohello página de detalles del trabajo Web de trabajo de Hola que seleccionó.

## <a name="WHPNotes"></a>Notas
* Las aplicaciones Web en el modo gratuito pueden tiempo de espera después de 20 minutos si no hay ningún sitio de scm (implementación) de las solicitudes toohello y portal de la aplicación hello web no está abierto en Azure. Las solicitudes toohello reales del sitio no restablecerán esto.
* El código de un trabajo continuo debe toobe escrito toorun en un bucle sin fin.
* Los trabajos continuos se ejecutan continuamente solo cuando la aplicación web de hello está activa.
* Básica y los modos estándar oferta Hola siempre en características que, cuando se habilita, impide que las aplicaciones web llega a estar inactivo.
* Solo se pueden depurar WebJobs que se ejecutan continuamente. No se admite la depuración de WebJobs programada o a petición.

## <a name="NextSteps"></a>Pasos siguientes
Para obtener más información, consulte [Recursos recomendados de WebJobs de Azure][WebJobsRecommendedResources].

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

