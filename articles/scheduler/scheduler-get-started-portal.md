---
title: aaaGet a trabajar con el programador de Azure en el portal de Azure | Documentos de Microsoft
description: "Introducción al Programador de Azure en el Portal de Azure"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: e69542ec-d10f-4f17-9b7a-2ee441ee7d68
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: deli
ms.openlocfilehash: 58255c0ad19da65932f8b1d36cb8fef1ff6e651b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-scheduler-in-azure-portal"></a><span data-ttu-id="3c126-103">Introducción al Programador de Azure en el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="3c126-103">Get started with Azure Scheduler in Azure portal</span></span>
<span data-ttu-id="3c126-104">Es fácil toocreate programar trabajos en el programador de Azure.</span><span class="sxs-lookup"><span data-stu-id="3c126-104">It's easy toocreate scheduled jobs in Azure Scheduler.</span></span> <span data-ttu-id="3c126-105">En este tutorial, aprenderá cómo toocreate un trabajo.</span><span class="sxs-lookup"><span data-stu-id="3c126-105">In this tutorial, you'll learn how toocreate a job.</span></span> <span data-ttu-id="3c126-106">También aprenderá las funcionalidades de supervisión y administración del Programador.</span><span class="sxs-lookup"><span data-stu-id="3c126-106">You'll also learn Scheduler's monitoring and management capabilities.</span></span>

## <a name="create-a-job"></a><span data-ttu-id="3c126-107">Creación de un trabajo</span><span class="sxs-lookup"><span data-stu-id="3c126-107">Create a job</span></span>
1. <span data-ttu-id="3c126-108">Inicie sesión en demasiado[portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3c126-108">Sign in too[Azure portal](https://portal.azure.com/).</span></span>  
2. <span data-ttu-id="3c126-109">Haga clic en **+ nuevo** > tipo *programador* en el cuadro de búsqueda de hello > seleccione **programador** en resultados > haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="3c126-109">Click **+New** > type *Scheduler* in hello search box >  select **Scheduler** in results > click **Create**.</span></span>
   
    ![][marketplace-create]
3. <span data-ttu-id="3c126-110">Vamos a crear un trabajo que simplemente selecciona http://www.microsoft.com/ con una solicitud GET.</span><span class="sxs-lookup"><span data-stu-id="3c126-110">Let’s create a job that simply hits http://www.microsoft.com/ with a GET request.</span></span> <span data-ttu-id="3c126-111">Hola **trabajo del programador** pantalla, escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="3c126-111">In hello **Scheduler Job** screen, enter hello following information:</span></span>
   
   1. <span data-ttu-id="3c126-112">**Nombre:**`getmicrosoft`</span><span class="sxs-lookup"><span data-stu-id="3c126-112">**Name:** `getmicrosoft`</span></span>  
   2. <span data-ttu-id="3c126-113">**Suscripción** : su suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="3c126-113">**Subscription:** Your Azure subscription</span></span>   
   3. <span data-ttu-id="3c126-114">**Colección de trabajos:** seleccione una colección de trabajos existente o haga clic en **Crear nueva** y escriba un nombre.</span><span class="sxs-lookup"><span data-stu-id="3c126-114">**Job Collection:** Select an existing job collection, or click **Create New** > enter a name.</span></span>
4. <span data-ttu-id="3c126-115">Después, en **configuración de la acción**, definir Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="3c126-115">Next, in **Action Settings**, define hello following values:</span></span>
   
   1. <span data-ttu-id="3c126-116">**Tipo de acción:**` HTTP`</span><span class="sxs-lookup"><span data-stu-id="3c126-116">**Action Type:** ` HTTP`</span></span>  
   2. <span data-ttu-id="3c126-117">**Método:**`GET`</span><span class="sxs-lookup"><span data-stu-id="3c126-117">**Method:** `GET`</span></span>  
   3. <span data-ttu-id="3c126-118">**URL:**` http://www.microsoft.com`</span><span class="sxs-lookup"><span data-stu-id="3c126-118">**URL:** ` http://www.microsoft.com`</span></span>  
      
      ![][action-settings]
5. <span data-ttu-id="3c126-119">Por último, vamos a definir una programación.</span><span class="sxs-lookup"><span data-stu-id="3c126-119">Finally, let's define a schedule.</span></span> <span data-ttu-id="3c126-120">trabajo de Hello puede definirse como un trabajo único, pero vamos a seleccionar una programación de periodicidad:</span><span class="sxs-lookup"><span data-stu-id="3c126-120">hello job could be defined as a one-time job, but let’s pick a recurrence schedule:</span></span>
   
   1. <span data-ttu-id="3c126-121">**Periocidad**: `Recurring`</span><span class="sxs-lookup"><span data-stu-id="3c126-121">**Recurrence**: `Recurring`</span></span>
   2. <span data-ttu-id="3c126-122">**Inicio**: la fecha de hoy</span><span class="sxs-lookup"><span data-stu-id="3c126-122">**Start**: Today's date</span></span>
   3. <span data-ttu-id="3c126-123">**Repetir cada**: `12 Hours`</span><span class="sxs-lookup"><span data-stu-id="3c126-123">**Recur every**: `12 Hours`</span></span>
   4. <span data-ttu-id="3c126-124">**Finalización**: dos días a partir de hoy</span><span class="sxs-lookup"><span data-stu-id="3c126-124">**End by**: Two days from today's date</span></span>  
      
      ![][recurrence-schedule]
6. <span data-ttu-id="3c126-125">Haga clic en **Crear**</span><span class="sxs-lookup"><span data-stu-id="3c126-125">Click **Create**</span></span>

## <a name="manage-and-monitor-jobs"></a><span data-ttu-id="3c126-126">Administración y supervisión de trabajos</span><span class="sxs-lookup"><span data-stu-id="3c126-126">Manage and monitor jobs</span></span>
<span data-ttu-id="3c126-127">Una vez que se crea un trabajo, aparece en el panel de Azure principal Hola.</span><span class="sxs-lookup"><span data-stu-id="3c126-127">Once a job is created, it appears in hello main Azure dashboard.</span></span> <span data-ttu-id="3c126-128">Haga clic en trabajo hello y una nueva ventana se abrirá con hello siguientes pestañas:</span><span class="sxs-lookup"><span data-stu-id="3c126-128">Click hello job and a new window opens with hello following tabs:</span></span>

1. <span data-ttu-id="3c126-129">Propiedades</span><span class="sxs-lookup"><span data-stu-id="3c126-129">Properties</span></span>  
2. <span data-ttu-id="3c126-130">Configuración de la acción</span><span class="sxs-lookup"><span data-stu-id="3c126-130">Action Settings</span></span>  
3. <span data-ttu-id="3c126-131">Schedule</span><span class="sxs-lookup"><span data-stu-id="3c126-131">Schedule</span></span>  
4. <span data-ttu-id="3c126-132">Historial</span><span class="sxs-lookup"><span data-stu-id="3c126-132">History</span></span>
5. <span data-ttu-id="3c126-133">Usuarios</span><span class="sxs-lookup"><span data-stu-id="3c126-133">Users</span></span>
   
   ![][job-overview]

### <a name="properties"></a><span data-ttu-id="3c126-134">Propiedades</span><span class="sxs-lookup"><span data-stu-id="3c126-134">Properties</span></span>
<span data-ttu-id="3c126-135">Estas propiedades de sólo lectura describen los metadatos de la administración de hello para el trabajo del programador de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c126-135">These read-only properties describe hello management metadata for hello Scheduler job.</span></span>

   ![][job-properties]

### <a name="action-settings"></a><span data-ttu-id="3c126-136">Configuración de la acción</span><span class="sxs-lookup"><span data-stu-id="3c126-136">Action settings</span></span>
<span data-ttu-id="3c126-137">Al hacer clic en un trabajo en hello **trabajos** pantalla le permite tooconfigure ese trabajo.</span><span class="sxs-lookup"><span data-stu-id="3c126-137">Clicking on a job in hello **Jobs** screen allows you tooconfigure that job.</span></span> <span data-ttu-id="3c126-138">Esto le permite configurar opciones avanzadas, si no configura Hola Asistente de creación rápida.</span><span class="sxs-lookup"><span data-stu-id="3c126-138">This lets you configure advanced settings, if you didn't configure them in hello quick-create wizard.</span></span>

<span data-ttu-id="3c126-139">Para todos los tipos de acción, puede cambiar la directiva de reintentos hello y acción de error de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c126-139">For all action types, you may change hello retry policy and hello error action.</span></span>

<span data-ttu-id="3c126-140">Para los tipos de acción de trabajo HTTP y HTTPS, puede cambiar Hola método tooany permitida el verbo HTTP.</span><span class="sxs-lookup"><span data-stu-id="3c126-140">For HTTP and HTTPS job action types, you may change hello method tooany allowed HTTP verb.</span></span> <span data-ttu-id="3c126-141">También se pueden agregar, eliminar o cambiar los encabezados de Hola y la información de autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="3c126-141">You may also add, delete, or change hello headers and basic authentication information.</span></span>

<span data-ttu-id="3c126-142">Para los tipos de acción de cola de almacenamiento, puede cambiar la cuenta de almacenamiento de hello, nombre de la cola, token SAS y cuerpo.</span><span class="sxs-lookup"><span data-stu-id="3c126-142">For storage queue action types, you may change hello storage account, queue name, SAS token, and body.</span></span>

<span data-ttu-id="3c126-143">Para los tipos de acción de bus de servicio, puede cambiar el espacio de nombres de hello, ruta de acceso de cola/tema, configuración de autenticación, tipo de transporte, propiedades del mensaje y el cuerpo del mensaje.</span><span class="sxs-lookup"><span data-stu-id="3c126-143">For service bus action types, you may change hello namespace, topic/queue path, authentication settings, transport type, message properties, and message body.</span></span>

   ![][job-action-settings]

### <a name="schedule"></a><span data-ttu-id="3c126-144">Schedule</span><span class="sxs-lookup"><span data-stu-id="3c126-144">Schedule</span></span>
<span data-ttu-id="3c126-145">Esto le permite volver a configurar programación de hello, si desea que la programación de hello toochange que creó en hello Asistente de creación rápida.</span><span class="sxs-lookup"><span data-stu-id="3c126-145">This lets you reconfigure hello schedule, if you'd like toochange hello schedule you created in hello quick-create wizard.</span></span>

<span data-ttu-id="3c126-146">Se trata de una oportunidad toobuild [programaciones complejas y periodicidad avanzada en el trabajo](scheduler-advanced-complexity.md)</span><span class="sxs-lookup"><span data-stu-id="3c126-146">This is an opportunity toobuild [complex schedules and advanced recurrence in your job](scheduler-advanced-complexity.md)</span></span>

<span data-ttu-id="3c126-147">Puede cambiar la fecha de inicio de Hola y Hola, la programación de periodicidad y la hora fecha de finalización y hora (si el trabajo de hello es periódico).</span><span class="sxs-lookup"><span data-stu-id="3c126-147">You may change hello start date and time, recurrence schedule, and hello end date and time (if hello job is recurring.)</span></span>

   ![][job-schedule]

### <a name="history"></a><span data-ttu-id="3c126-148">Historial</span><span class="sxs-lookup"><span data-stu-id="3c126-148">History</span></span>
<span data-ttu-id="3c126-149">Hola **historial** pestaña muestra las métricas seleccionadas para cada ejecución del trabajo de sistema de hello para el trabajo seleccionado de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c126-149">hello **History** tab displays selected metrics for every job execution in hello system for hello selected job.</span></span> <span data-ttu-id="3c126-150">Estas métricas proporcionan valores en tiempo real con respecto a estado Hola de Scheduler:</span><span class="sxs-lookup"><span data-stu-id="3c126-150">These metrics provide real-time values regarding hello health of your Scheduler:</span></span>

1. <span data-ttu-id="3c126-151">Estado</span><span class="sxs-lookup"><span data-stu-id="3c126-151">Status</span></span>  
2. <span data-ttu-id="3c126-152">Detalles</span><span class="sxs-lookup"><span data-stu-id="3c126-152">Details</span></span>  
3. <span data-ttu-id="3c126-153">Número de reintentos</span><span class="sxs-lookup"><span data-stu-id="3c126-153">Retry attempts</span></span>
4. <span data-ttu-id="3c126-154">Periodicidad: 1ª, 2ª, 3ª, etc.</span><span class="sxs-lookup"><span data-stu-id="3c126-154">Occurrence: 1st, 2nd, 3rd, etc.</span></span>
5. <span data-ttu-id="3c126-155">Hora de inicio de ejecución</span><span class="sxs-lookup"><span data-stu-id="3c126-155">Start time of execution</span></span>  
6. <span data-ttu-id="3c126-156">Hora de finalización de ejecución</span><span class="sxs-lookup"><span data-stu-id="3c126-156">End time of execution</span></span>
   
   ![][job-history]

<span data-ttu-id="3c126-157">Puede hacer clic en una ejecución tooview su **detalles del historial de**, incluida la respuesta completa de Hola para cada ejecución.</span><span class="sxs-lookup"><span data-stu-id="3c126-157">You can click on a run tooview its **History Details**, including hello whole response for every execution.</span></span> <span data-ttu-id="3c126-158">Este cuadro de diálogo también permite Portapapeles toohello de toocopy Hola respuesta.</span><span class="sxs-lookup"><span data-stu-id="3c126-158">This dialog box also allows you toocopy hello response toohello clipboard.</span></span>

   ![][job-history-details]

### <a name="users"></a><span data-ttu-id="3c126-159">Usuarios</span><span class="sxs-lookup"><span data-stu-id="3c126-159">Users</span></span>
<span data-ttu-id="3c126-160">El control de acceso basado en roles (RBAC) de Azure permite realizar una administración detallada del acceso al Programador de Azure.</span><span class="sxs-lookup"><span data-stu-id="3c126-160">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure Scheduler.</span></span> <span data-ttu-id="3c126-161">toolearn cómo toouse Hola ficha de usuarios, consulte demasiado[Azure Role-Based el Control de acceso](../active-directory/role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="3c126-161">toolearn how toouse hello Users tab, refer too[Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md)</span></span>

## <a name="see-also"></a><span data-ttu-id="3c126-162">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="3c126-162">See also</span></span>
 [<span data-ttu-id="3c126-163">¿Qué es Programador?</span><span class="sxs-lookup"><span data-stu-id="3c126-163">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="3c126-164">Jerarquía de entidades, terminología y conceptos del Programador</span><span class="sxs-lookup"><span data-stu-id="3c126-164">Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="3c126-165">Planes y facturación en Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="3c126-165">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="3c126-166">¿Cómo se programa toobuild complejo y periodicidad avanzada con el programador de Azure</span><span class="sxs-lookup"><span data-stu-id="3c126-166">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="3c126-167">Referencia de API de REST del Programador</span><span class="sxs-lookup"><span data-stu-id="3c126-167">Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="3c126-168">Referencia de cmdlets de PowerShell del Programador</span><span class="sxs-lookup"><span data-stu-id="3c126-168">Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="3c126-169">Alta disponibilidad y confiabilidad del Programador</span><span class="sxs-lookup"><span data-stu-id="3c126-169">Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="3c126-170">Límites, valores predeterminados y códigos de error de Programador</span><span class="sxs-lookup"><span data-stu-id="3c126-170">Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="3c126-171">Autenticación de salida del Programador</span><span class="sxs-lookup"><span data-stu-id="3c126-171">Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

[marketplace-create]: ./media/scheduler-get-started-portal/scheduler-v2-portal-marketplace-create.png
[action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-action-settings.png
[recurrence-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-recurrence-schedule.png
[job-properties]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-properties.png
[job-overview]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-overview-1.png
[job-action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-action-settings.png
[job-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-schedule.png
[job-history]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history.png
[job-history-details]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history-details.png


[1]: ./media/scheduler-get-started-portal/scheduler-get-started-portal001.png
[2]: ./media/scheduler-get-started-portal/scheduler-get-started-portal002.png
[3]: ./media/scheduler-get-started-portal/scheduler-get-started-portal003.png
[4]: ./media/scheduler-get-started-portal/scheduler-get-started-portal004.png
[5]: ./media/scheduler-get-started-portal/scheduler-get-started-portal005.png
[6]: ./media/scheduler-get-started-portal/scheduler-get-started-portal006.png
[7]: ./media/scheduler-get-started-portal/scheduler-get-started-portal007.png
[8]: ./media/scheduler-get-started-portal/scheduler-get-started-portal008.png
[9]: ./media/scheduler-get-started-portal/scheduler-get-started-portal009.png
[10]: ./media/scheduler-get-started-portal/scheduler-get-started-portal010.png
[11]: ./media/scheduler-get-started-portal/scheduler-get-started-portal011.png
[12]: ./media/scheduler-get-started-portal/scheduler-get-started-portal012.png
[13]: ./media/scheduler-get-started-portal/scheduler-get-started-portal013.png
[14]: ./media/scheduler-get-started-portal/scheduler-get-started-portal014.png
[15]: ./media/scheduler-get-started-portal/scheduler-get-started-portal015.png
