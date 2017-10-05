---
title: "Introducción al Programador de Azure en Azure Portal | Microsoft Docs"
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
ms.openlocfilehash: 3861ee121ed1c4d086ea81640e84d924d7d17ea1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-scheduler-in-azure-portal"></a><span data-ttu-id="4c814-103">Introducción al Programador de Azure en el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="4c814-103">Get started with Azure Scheduler in Azure portal</span></span>
<span data-ttu-id="4c814-104">Es fácil crear trabajos programados en el Programador de Azure.</span><span class="sxs-lookup"><span data-stu-id="4c814-104">It's easy to create scheduled jobs in Azure Scheduler.</span></span> <span data-ttu-id="4c814-105">En este tutorial, aprenderá a crear un trabajo:</span><span class="sxs-lookup"><span data-stu-id="4c814-105">In this tutorial, you'll learn how to create a job.</span></span> <span data-ttu-id="4c814-106">También aprenderá las funcionalidades de supervisión y administración del Programador.</span><span class="sxs-lookup"><span data-stu-id="4c814-106">You'll also learn Scheduler's monitoring and management capabilities.</span></span>

## <a name="create-a-job"></a><span data-ttu-id="4c814-107">Creación de un trabajo</span><span class="sxs-lookup"><span data-stu-id="4c814-107">Create a job</span></span>
1. <span data-ttu-id="4c814-108">Inicie sesión en el [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4c814-108">Sign in to [Azure portal](https://portal.azure.com/).</span></span>  
2. <span data-ttu-id="4c814-109">Haga clic en **+Nuevo** > escriba *Programador* en el cuadro de búsqueda > seleccione **Programador** en resultados > haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="4c814-109">Click **+New** > type *Scheduler* in the search box >  select **Scheduler** in results > click **Create**.</span></span>
   
    ![][marketplace-create]
3. <span data-ttu-id="4c814-110">Vamos a crear un trabajo que simplemente selecciona http://www.microsoft.com/ con una solicitud GET.</span><span class="sxs-lookup"><span data-stu-id="4c814-110">Let’s create a job that simply hits http://www.microsoft.com/ with a GET request.</span></span> <span data-ttu-id="4c814-111">En la pantalla **Trabajo del Programador** , escriba la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="4c814-111">In the **Scheduler Job** screen, enter the following information:</span></span>
   
   1. <span data-ttu-id="4c814-112">**Nombre:** `getmicrosoft`</span><span class="sxs-lookup"><span data-stu-id="4c814-112">**Name:** `getmicrosoft`</span></span>  
   2. <span data-ttu-id="4c814-113">**Suscripción** : su suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="4c814-113">**Subscription:** Your Azure subscription</span></span>   
   3. <span data-ttu-id="4c814-114">**Colección de trabajos:** seleccione una colección de trabajos existente o haga clic en **Crear nueva** y escriba un nombre.</span><span class="sxs-lookup"><span data-stu-id="4c814-114">**Job Collection:** Select an existing job collection, or click **Create New** > enter a name.</span></span>
4. <span data-ttu-id="4c814-115">Después, en **Configuración de la acción**, defina los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="4c814-115">Next, in **Action Settings**, define the following values:</span></span>
   
   1. <span data-ttu-id="4c814-116">**Tipo de acción:** ` HTTP`</span><span class="sxs-lookup"><span data-stu-id="4c814-116">**Action Type:** ` HTTP`</span></span>  
   2. <span data-ttu-id="4c814-117">**Método:** `GET`</span><span class="sxs-lookup"><span data-stu-id="4c814-117">**Method:** `GET`</span></span>  
   3. <span data-ttu-id="4c814-118">**URL:** ` http://www.microsoft.com`</span><span class="sxs-lookup"><span data-stu-id="4c814-118">**URL:** ` http://www.microsoft.com`</span></span>  
      
      ![][action-settings]
5. <span data-ttu-id="4c814-119">Por último, vamos a definir una programación.</span><span class="sxs-lookup"><span data-stu-id="4c814-119">Finally, let's define a schedule.</span></span> <span data-ttu-id="4c814-120">El trabajo se puede definir como un trabajo único, pero vamos a seleccionar una programación de periodicidad:</span><span class="sxs-lookup"><span data-stu-id="4c814-120">The job could be defined as a one-time job, but let’s pick a recurrence schedule:</span></span>
   
   1. <span data-ttu-id="4c814-121">**Periocidad**: `Recurring`</span><span class="sxs-lookup"><span data-stu-id="4c814-121">**Recurrence**: `Recurring`</span></span>
   2. <span data-ttu-id="4c814-122">**Inicio**: la fecha de hoy</span><span class="sxs-lookup"><span data-stu-id="4c814-122">**Start**: Today's date</span></span>
   3. <span data-ttu-id="4c814-123">**Repetir cada**: `12 Hours`</span><span class="sxs-lookup"><span data-stu-id="4c814-123">**Recur every**: `12 Hours`</span></span>
   4. <span data-ttu-id="4c814-124">**Finalización**: dos días a partir de hoy</span><span class="sxs-lookup"><span data-stu-id="4c814-124">**End by**: Two days from today's date</span></span>  
      
      ![][recurrence-schedule]
6. <span data-ttu-id="4c814-125">Haga clic en **Crear**</span><span class="sxs-lookup"><span data-stu-id="4c814-125">Click **Create**</span></span>

## <a name="manage-and-monitor-jobs"></a><span data-ttu-id="4c814-126">Administración y supervisión de trabajos</span><span class="sxs-lookup"><span data-stu-id="4c814-126">Manage and monitor jobs</span></span>
<span data-ttu-id="4c814-127">Una vez que se crea un trabajo, aparece en el Panel principal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4c814-127">Once a job is created, it appears in the main Azure dashboard.</span></span> <span data-ttu-id="4c814-128">Haga clic en el trabajo y se abrirá una nueva ventana con las pestañas siguientes:</span><span class="sxs-lookup"><span data-stu-id="4c814-128">Click the job and a new window opens with the following tabs:</span></span>

1. <span data-ttu-id="4c814-129">Propiedades</span><span class="sxs-lookup"><span data-stu-id="4c814-129">Properties</span></span>  
2. <span data-ttu-id="4c814-130">Configuración de la acción</span><span class="sxs-lookup"><span data-stu-id="4c814-130">Action Settings</span></span>  
3. <span data-ttu-id="4c814-131">Schedule</span><span class="sxs-lookup"><span data-stu-id="4c814-131">Schedule</span></span>  
4. <span data-ttu-id="4c814-132">Historial</span><span class="sxs-lookup"><span data-stu-id="4c814-132">History</span></span>
5. <span data-ttu-id="4c814-133">Usuarios</span><span class="sxs-lookup"><span data-stu-id="4c814-133">Users</span></span>
   
   ![][job-overview]

### <a name="properties"></a><span data-ttu-id="4c814-134">Propiedades</span><span class="sxs-lookup"><span data-stu-id="4c814-134">Properties</span></span>
<span data-ttu-id="4c814-135">Estas propiedades de solo lectura describen los metadatos de administración para el trabajo del Programador.</span><span class="sxs-lookup"><span data-stu-id="4c814-135">These read-only properties describe the management metadata for the Scheduler job.</span></span>

   ![][job-properties]

### <a name="action-settings"></a><span data-ttu-id="4c814-136">Configuración de la acción</span><span class="sxs-lookup"><span data-stu-id="4c814-136">Action settings</span></span>
<span data-ttu-id="4c814-137">Al hacer clic en un trabajo en la pantalla **Trabajos** puede configurar ese trabajo.</span><span class="sxs-lookup"><span data-stu-id="4c814-137">Clicking on a job in the **Jobs** screen allows you to configure that job.</span></span> <span data-ttu-id="4c814-138">Esto le permitirá configurar opciones avanzadas, si no las ha configurado en el Asistente de creación rápida.</span><span class="sxs-lookup"><span data-stu-id="4c814-138">This lets you configure advanced settings, if you didn't configure them in the quick-create wizard.</span></span>

<span data-ttu-id="4c814-139">Para todos los tipos de acción, puede cambiar la directiva de reintentos y la acción en caso de error.</span><span class="sxs-lookup"><span data-stu-id="4c814-139">For all action types, you may change the retry policy and the error action.</span></span>

<span data-ttu-id="4c814-140">Para los tipos de acción de los trabajos HTTP y HTTPS, puede cambiar el método a cualquier verbo HTTP permitido.</span><span class="sxs-lookup"><span data-stu-id="4c814-140">For HTTP and HTTPS job action types, you may change the method to any allowed HTTP verb.</span></span> <span data-ttu-id="4c814-141">También puede agregar, eliminar o cambiar los encabezados y la información de autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="4c814-141">You may also add, delete, or change the headers and basic authentication information.</span></span>

<span data-ttu-id="4c814-142">Para los tipos de acciones de la cola de almacenamiento, puede cambiar la cuenta de almacenamiento, el nombre de la cola, el token SAS y el cuerpo.</span><span class="sxs-lookup"><span data-stu-id="4c814-142">For storage queue action types, you may change the storage account, queue name, SAS token, and body.</span></span>

<span data-ttu-id="4c814-143">Para los tipos de acción del Bus de servicio, puede cambiar el espacio de nombres, la ruta de tema/cola, la configuración de autenticación, el tipo de transporte, las propiedades de mensaje y el cuerpo del mensaje.</span><span class="sxs-lookup"><span data-stu-id="4c814-143">For service bus action types, you may change the namespace, topic/queue path, authentication settings, transport type, message properties, and message body.</span></span>

   ![][job-action-settings]

### <a name="schedule"></a><span data-ttu-id="4c814-144">Schedule</span><span class="sxs-lookup"><span data-stu-id="4c814-144">Schedule</span></span>
<span data-ttu-id="4c814-145">Esto le permite volver a configurar la programación, si es que desea cambiar la programación que creó en el Asistente de creación rápida.</span><span class="sxs-lookup"><span data-stu-id="4c814-145">This lets you reconfigure the schedule, if you'd like to change the schedule you created in the quick-create wizard.</span></span>

<span data-ttu-id="4c814-146">Esta es una oportunidad para crear [programaciones complejas y periodicidad avanzada en el trabajo](scheduler-advanced-complexity.md)</span><span class="sxs-lookup"><span data-stu-id="4c814-146">This is an opportunity to build [complex schedules and advanced recurrence in your job](scheduler-advanced-complexity.md)</span></span>

<span data-ttu-id="4c814-147">Puede cambiar la fecha y hora de inicio, la programación de periodicidad y la fecha y hora de finalización (si el trabajo es periódico).</span><span class="sxs-lookup"><span data-stu-id="4c814-147">You may change the start date and time, recurrence schedule, and the end date and time (if the job is recurring.)</span></span>

   ![][job-schedule]

### <a name="history"></a><span data-ttu-id="4c814-148">Historial</span><span class="sxs-lookup"><span data-stu-id="4c814-148">History</span></span>
<span data-ttu-id="4c814-149">La pestaña **Historial** muestra métricas seleccionadas para cada ejecución del trabajo en el sistema para el trabajo seleccionado.</span><span class="sxs-lookup"><span data-stu-id="4c814-149">The **History** tab displays selected metrics for every job execution in the system for the selected job.</span></span> <span data-ttu-id="4c814-150">Estas métricas proporcionan valores en tiempo real relacionados con el estado del Programador:</span><span class="sxs-lookup"><span data-stu-id="4c814-150">These metrics provide real-time values regarding the health of your Scheduler:</span></span>

1. <span data-ttu-id="4c814-151">Estado</span><span class="sxs-lookup"><span data-stu-id="4c814-151">Status</span></span>  
2. <span data-ttu-id="4c814-152">Detalles</span><span class="sxs-lookup"><span data-stu-id="4c814-152">Details</span></span>  
3. <span data-ttu-id="4c814-153">Número de reintentos</span><span class="sxs-lookup"><span data-stu-id="4c814-153">Retry attempts</span></span>
4. <span data-ttu-id="4c814-154">Periodicidad: 1ª, 2ª, 3ª, etc.</span><span class="sxs-lookup"><span data-stu-id="4c814-154">Occurrence: 1st, 2nd, 3rd, etc.</span></span>
5. <span data-ttu-id="4c814-155">Hora de inicio de ejecución</span><span class="sxs-lookup"><span data-stu-id="4c814-155">Start time of execution</span></span>  
6. <span data-ttu-id="4c814-156">Hora de finalización de ejecución</span><span class="sxs-lookup"><span data-stu-id="4c814-156">End time of execution</span></span>
   
   ![][job-history]

<span data-ttu-id="4c814-157">Puede hacer clic en una ejecución para ver su información en **Detalles del historial**, incluida la respuesta completa a cada ejecución.</span><span class="sxs-lookup"><span data-stu-id="4c814-157">You can click on a run to view its **History Details**, including the whole response for every execution.</span></span> <span data-ttu-id="4c814-158">Este cuadro de diálogo también le permite copiar la respuesta en el Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="4c814-158">This dialog box also allows you to copy the response to the clipboard.</span></span>

   ![][job-history-details]

### <a name="users"></a><span data-ttu-id="4c814-159">Usuarios</span><span class="sxs-lookup"><span data-stu-id="4c814-159">Users</span></span>
<span data-ttu-id="4c814-160">El control de acceso basado en roles (RBAC) de Azure permite realizar una administración detallada del acceso al Programador de Azure.</span><span class="sxs-lookup"><span data-stu-id="4c814-160">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure Scheduler.</span></span> <span data-ttu-id="4c814-161">Para aprender a usar la pestaña Usuarios, consulte [Control de acceso basado en rol de Azure](../active-directory/role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="4c814-161">To learn how to use the Users tab, refer to [Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md)</span></span>

## <a name="see-also"></a><span data-ttu-id="4c814-162">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="4c814-162">See also</span></span>
 [<span data-ttu-id="4c814-163">¿Qué es Programador?</span><span class="sxs-lookup"><span data-stu-id="4c814-163">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="4c814-164">Jerarquía de entidades, terminología y conceptos del Programador</span><span class="sxs-lookup"><span data-stu-id="4c814-164">Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="4c814-165">Planes y facturación en Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="4c814-165">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="4c814-166">Creación de programaciones complejas y periodicidad avanzada con Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="4c814-166">How to build complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="4c814-167">Referencia de API de REST del Programador</span><span class="sxs-lookup"><span data-stu-id="4c814-167">Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="4c814-168">Referencia de cmdlets de PowerShell del Programador</span><span class="sxs-lookup"><span data-stu-id="4c814-168">Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="4c814-169">Alta disponibilidad y confiabilidad del Programador</span><span class="sxs-lookup"><span data-stu-id="4c814-169">Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="4c814-170">Límites, valores predeterminados y códigos de error de Programador</span><span class="sxs-lookup"><span data-stu-id="4c814-170">Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="4c814-171">Autenticación de salida del Programador</span><span class="sxs-lookup"><span data-stu-id="4c814-171">Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

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
