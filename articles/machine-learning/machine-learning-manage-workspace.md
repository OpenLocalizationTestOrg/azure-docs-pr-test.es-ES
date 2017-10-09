---
title: "un área de trabajo de aprendizaje automático de aaaManage | Documentos de Microsoft"
description: "Administrar el acceso a áreas de trabajo de aprendizaje automático de tooAzure, implementar y administrar los servicios web de API de aprendizaje automático"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: daf3d413-7a77-4beb-9a7a-6b4bdf717719
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye
ms.openlocfilehash: 7bd378d82aa46f4340ca974c7dc5a612c089cdca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-machine-learning-workspace"></a><span data-ttu-id="2311b-103">Administración de un área de trabajo de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="2311b-103">Manage an Azure Machine Learning workspace</span></span>

> [!NOTE]
> <span data-ttu-id="2311b-104">Para obtener información sobre la administración de servicios Web en el portal de servicios Web de aprendizaje de máquina de hello, consulte [administrar un servicio Web mediante el portal de servicios Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="2311b-104">For information on managing Web services in hello Machine Learning Web Services portal, see [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span>
> 
> 

<span data-ttu-id="2311b-105">Puede administrar áreas de trabajo de aprendizaje automático en cualquier portal de Azure de Hola u Hola portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="2311b-105">You can manage Machine Learning workspaces in either hello Azure portal or hello Azure classic portal.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="use-hello-azure-portal"></a><span data-ttu-id="2311b-106">Usar hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="2311b-106">Use hello Azure portal</span></span>

<span data-ttu-id="2311b-107">toomanage un área de trabajo en hello portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="2311b-107">toomanage a workspace in hello Azure portal:</span></span>

1. <span data-ttu-id="2311b-108">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/) con una cuenta de administrador de suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="2311b-108">Sign in toohello [Azure portal](https://portal.azure.com/) using an Azure subscription administrator account.</span></span>
2. <span data-ttu-id="2311b-109">En cuadro de búsqueda de hello al principio de Hola de página de hello, escriba "áreas de trabajo de aprendizaje de la máquina" y, a continuación, seleccione **áreas de trabajo de aprendizaje automático**.</span><span class="sxs-lookup"><span data-stu-id="2311b-109">In hello search box at hello top of hello page, enter "machine learning workspaces" and then select **Machine Learning Workspaces**.</span></span>
3. <span data-ttu-id="2311b-110">Haga clic en el área de trabajo de hello desee toomanage.</span><span class="sxs-lookup"><span data-stu-id="2311b-110">Click hello workspace you want toomanage.</span></span>

<span data-ttu-id="2311b-111">Además toohello información de administración de recursos estándar y las opciones disponibles, hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2311b-111">In addition toohello standard resource management information and options available, you can:</span></span>

- <span data-ttu-id="2311b-112">Vista **propiedades** : esta página muestra información de área de trabajo y recursos de Hola y puede cambiar suscripción Hola y el grupo de recursos que está conectada esta área de trabajo con.</span><span class="sxs-lookup"><span data-stu-id="2311b-112">View **Properties** - This page displays hello workspace and resource information, and you can change hello subscription and resource group that this workspace is connected with.</span></span>
- <span data-ttu-id="2311b-113">**Resincronizar claves de almacenamiento** -área de trabajo de hello mantiene la cuenta de almacenamiento de claves toohello.</span><span class="sxs-lookup"><span data-stu-id="2311b-113">**Resync Storage Keys** - hello workspace maintains keys toohello storage account.</span></span> <span data-ttu-id="2311b-114">Si cambiar la cuenta de almacenamiento de hello las claves, puede hacer clic en **Resync claves** claves de hello toosynchronize con el área de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2311b-114">If hello storage account changes keys, then you can click **Resync keys** toosynchronize hello keys with hello workspace.</span></span>

<span data-ttu-id="2311b-115">Servicios de web de hello toomanage asociados a esta área de trabajo, usar el portal de servicios Web de aprendizaje de máquina de Hola.</span><span class="sxs-lookup"><span data-stu-id="2311b-115">toomanage hello web services associated with this workspace, use hello Machine Learning Web Services portal.</span></span> <span data-ttu-id="2311b-116">Vea [administrar un servicio Web mediante el portal de servicios Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md) para obtener información completa.</span><span class="sxs-lookup"><span data-stu-id="2311b-116">See [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md) for complete information.</span></span>

> [!NOTE]
> <span data-ttu-id="2311b-117">toodeploy o administrar los nuevos servicios web debe tener asignado un colaborador o se implementa el rol de administrador en el servicio web de hello suscripción toowhich Hola.</span><span class="sxs-lookup"><span data-stu-id="2311b-117">toodeploy or manage New web services you must be assigned a contributor or administrator role on hello subscription toowhich hello web service is deployed.</span></span> <span data-ttu-id="2311b-118">Si se invitar a otra área de trabajo de aprendizaje de automático de tooa de usuario, debe asignarlos tooa rol Colaborador o administrador de suscripción de Hola para poder implementar o administrar los servicios web.</span><span class="sxs-lookup"><span data-stu-id="2311b-118">If you invite another user tooa machine learning workspace, you must assign them tooa contributor or administrator role on hello subscription before they can deploy or manage web services.</span></span> 
> 
><span data-ttu-id="2311b-119">Para obtener más información sobre cómo establecer permisos de acceso, consulte [ver las asignaciones de acceso para usuarios y grupos en el portal de Azure - versión preliminar pública de hello](../active-directory/role-based-access-control-manage-assignments.md).</span><span class="sxs-lookup"><span data-stu-id="2311b-119">For more information on setting access permissions, see [View access assignments for users and groups in hello Azure portal - Public preview](../active-directory/role-based-access-control-manage-assignments.md).</span></span>

## <a name="use-hello-azure-classic-portal"></a><span data-ttu-id="2311b-120">Usar hello portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="2311b-120">Use hello Azure classic portal</span></span>

<span data-ttu-id="2311b-121">Con hello portal de Azure clásico, puede administrar las áreas de trabajo de aprendizaje automático para:</span><span class="sxs-lookup"><span data-stu-id="2311b-121">Using hello Azure classic portal, you can manage your Machine Learning workspaces to:</span></span>

* <span data-ttu-id="2311b-122">Supervisar la utilización de área de trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="2311b-122">Monitor how hello workspace is being used</span></span>
* <span data-ttu-id="2311b-123">Configurar tooallow de área de trabajo de Hola o denegar el acceso</span><span class="sxs-lookup"><span data-stu-id="2311b-123">Configure hello workspace tooallow or deny access</span></span>
* <span data-ttu-id="2311b-124">Administrar los servicios Web creados en el área de trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="2311b-124">Manage Web services created in hello workspace</span></span>
* <span data-ttu-id="2311b-125">Eliminar área de trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="2311b-125">Delete hello workspace</span></span>

<span data-ttu-id="2311b-126">Además, la pestaña panel Hola proporciona información general sobre el uso del área de trabajo y una vista rápida de la información del área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2311b-126">In addition, hello dashboard tab provides an overview of your workspace usage and a quick glance of your workspace information.</span></span>  

> [!TIP]
> <span data-ttu-id="2311b-127">En estudio de aprendizaje automático de Azure, en hello **servicios WEB** ficha, puede agregar, actualizar o eliminar un servicio Web de aprendizaje de máquina.</span><span class="sxs-lookup"><span data-stu-id="2311b-127">In Azure Machine Learning Studio, on hello **WEB SERVICES** tab, you can add, update, or delete a Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="2311b-128">toomanage un área de trabajo en hello portal de Azure clásico:</span><span class="sxs-lookup"><span data-stu-id="2311b-128">toomanage a workspace in hello Azure classic portal:</span></span>

1. <span data-ttu-id="2311b-129">Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com/) con su Microsoft Azure cuenta - usar cuenta de hello que esté asociada con hello suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="2311b-129">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) using your Microsoft Azure account - use hello account that's associated with hello Azure subscription.</span></span>
2. <span data-ttu-id="2311b-130">En el panel de servicios de Microsoft Azure hello, haga clic en **aprendizaje automático**.</span><span class="sxs-lookup"><span data-stu-id="2311b-130">In hello Microsoft Azure services panel, click **MACHINE LEARNING**.</span></span>
3. <span data-ttu-id="2311b-131">Haga clic en el área de trabajo de hello desee toomanage.</span><span class="sxs-lookup"><span data-stu-id="2311b-131">Click hello workspace you want toomanage.</span></span>

<span data-ttu-id="2311b-132">página de área de trabajo de Hello tiene tres pestañas:</span><span class="sxs-lookup"><span data-stu-id="2311b-132">hello workspace page has three tabs:</span></span>

* <span data-ttu-id="2311b-133">**PANEL** -permite el uso del área de trabajo de tooview e información</span><span class="sxs-lookup"><span data-stu-id="2311b-133">**DASHBOARD** - Allows you tooview workspace usage and information</span></span>
* <span data-ttu-id="2311b-134">**CONFIGURAR** -permite el área de trabajo de toomanage access toohello</span><span class="sxs-lookup"><span data-stu-id="2311b-134">**CONFIGURE** - Allows you toomanage access toohello workspace</span></span>
* <span data-ttu-id="2311b-135">**SERVICIOS WEB** -permite los servicios Web de toomanage que se han publicado desde esta área de trabajo</span><span class="sxs-lookup"><span data-stu-id="2311b-135">**WEB SERVICES** - Allows you toomanage Web services that have been published from this workspace</span></span>

### <a name="toomonitor-how-hello-workspace-is-being-used"></a><span data-ttu-id="2311b-136">toomonitor cómo se usa el área de trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="2311b-136">toomonitor how hello workspace is being used</span></span>
<span data-ttu-id="2311b-137">Haga clic en hello **panel** ficha.</span><span class="sxs-lookup"><span data-stu-id="2311b-137">Click hello **DASHBOARD** tab.</span></span>

<span data-ttu-id="2311b-138">En el panel de hello, puede ver el uso general del área de trabajo y obtener una vista rápida de la información del área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2311b-138">From hello dashboard, you can view overall usage of your workspace and get a quick glance of workspace information.</span></span>

* <span data-ttu-id="2311b-139">Hola **proceso** gráfico muestra los recursos de proceso de hello usándola por área de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2311b-139">hello **COMPUTE** chart shows hello compute resources being used by hello workspace.</span></span> <span data-ttu-id="2311b-140">Puede cambiar Hola vista toodisplay relativa o valores absolutos, y puede cambiar el período de tiempo de hello muestra en el gráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="2311b-140">You can change hello view toodisplay relative or absolute values, and you can change hello timeframe displayed in hello chart.</span></span>
* <span data-ttu-id="2311b-141">**Información general del uso** muestra el almacenamiento de Azure que usa el área de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2311b-141">**Usage overview** displays Azure storage being used by hello workspace.</span></span>
* <span data-ttu-id="2311b-142">**Vista rápida** : proporciona un resumen de la información del área de trabajo y vínculos útiles.</span><span class="sxs-lookup"><span data-stu-id="2311b-142">**Quick glance** provides a summary of workspace information and useful links.</span></span>

> [!NOTE]
> <span data-ttu-id="2311b-143">Hola **inicio de sesión tooML Studio** vínculo abre estudio de aprendizaje automático con hello Account Microsoft ha iniciado sesión en.</span><span class="sxs-lookup"><span data-stu-id="2311b-143">hello **Sign-in tooML Studio** link opens Machine Learning Studio using hello Microsoft Account you are currently signed into.</span></span> <span data-ttu-id="2311b-144">Hola Account Microsoft utiliza toosign en toohello toocreate portal clásico un área de trabajo de Azure no automáticamente tiene permiso tooopen esa área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2311b-144">hello Microsoft Account you used toosign in toohello Azure classic portal toocreate a workspace does not automatically have permission tooopen that workspace.</span></span> <span data-ttu-id="2311b-145">tooopen un área de trabajo, debe iniciar sesión en toohello Account de Microsoft que se ha definido como propietario de hello del área de trabajo de Hola o necesita tooreceive una invitación de área de trabajo de hello propietario toojoin Hola.</span><span class="sxs-lookup"><span data-stu-id="2311b-145">tooopen a workspace, you must be signed in toohello Microsoft Account that was defined as hello owner of hello workspace, or you need tooreceive an invitation from hello owner toojoin hello workspace.</span></span>
> 
> 

### <a name="toogrant-or-suspend-access-for-users"></a><span data-ttu-id="2311b-146">toogrant o suspender el acceso a los usuarios</span><span class="sxs-lookup"><span data-stu-id="2311b-146">toogrant or suspend access for users</span></span>
<span data-ttu-id="2311b-147">Haga clic en hello **configurar** ficha.</span><span class="sxs-lookup"><span data-stu-id="2311b-147">Click hello **CONFIGURE** tab.</span></span>

<span data-ttu-id="2311b-148">Desde la ficha de configuración de hello hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2311b-148">From hello configuration tab you can:</span></span>

* <span data-ttu-id="2311b-149">Suspender el área de trabajo de access toohello aprendizaje automático, haga clic en Denegar.</span><span class="sxs-lookup"><span data-stu-id="2311b-149">Suspend access toohello Machine Learning workspace by clicking DENY.</span></span> <span data-ttu-id="2311b-150">Los usuarios ya no estará tooopen capaz de área de trabajo hello en estudio de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="2311b-150">Users will no longer be able tooopen hello workspace in Machine Learning Studio.</span></span> <span data-ttu-id="2311b-151">toorestore acceso, haga clic en permitir.</span><span class="sxs-lookup"><span data-stu-id="2311b-151">toorestore access, click ALLOW.</span></span>

<span data-ttu-id="2311b-152">toomanage cuentas adicionales que tengan acceso toohello área de trabajo en estudio de aprendizaje automático, haga clic en **inicio de sesión tooML Studio** en hello **panel** pestaña (Véase la nota de hello precedente con respecto a  **Sign-In tooML Studio**).</span><span class="sxs-lookup"><span data-stu-id="2311b-152">toomanage additional accounts who have access toohello workspace in Machine Learning Studio, click **Sign-in tooML Studio** in hello **DASHBOARD** tab (see hello preceeding note regarding **Sign-in tooML Studio**).</span></span> <span data-ttu-id="2311b-153">Se abre el área de trabajo de hello en estudio de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="2311b-153">This opens hello workspace in Machine Learning Studio.</span></span> <span data-ttu-id="2311b-154">Desde aquí, haga clic en hello **configuración** ficha y, a continuación, **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="2311b-154">From here, click hello **SETTINGS** tab and then **USERS**.</span></span> <span data-ttu-id="2311b-155">Puede hacer clic en **invitar a más usuarios** toogive a los usuarios tener acceso a área de trabajo de toohello, o seleccione un usuario y haga clic en **quitar**.</span><span class="sxs-lookup"><span data-stu-id="2311b-155">You can click **INVITE MORE USERS** toogive users access toohello workspace, or select a user and click **REMOVE**.</span></span>

### <a name="toomanage-web-services-in-this-workspace"></a><span data-ttu-id="2311b-156">toomanage los servicios web en esta área de trabajo</span><span class="sxs-lookup"><span data-stu-id="2311b-156">toomanage web services in this workspace</span></span>
<span data-ttu-id="2311b-157">Haga clic en hello **servicios WEB** ficha.</span><span class="sxs-lookup"><span data-stu-id="2311b-157">Click hello **WEB SERVICES** tab.</span></span>

<span data-ttu-id="2311b-158">Esto muestra una lista de servicios web publicados desde esta área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2311b-158">This displays a list of web services published from this workspace.</span></span>
<span data-ttu-id="2311b-159">toomanage un servicio web, haga clic en nombre de hello en la página del servicio Web Hola lista tooopen Hola.</span><span class="sxs-lookup"><span data-stu-id="2311b-159">toomanage a web service, click hello name in hello list tooopen hello Web service page.</span></span>

<span data-ttu-id="2311b-160">Un servicio web puede tener uno o varios puntos de conexión definidos.</span><span class="sxs-lookup"><span data-stu-id="2311b-160">A Web service may have one or more endpoints defined.</span></span>

* <span data-ttu-id="2311b-161">Puede definir varios puntos de conexión en el punto de conexión de adición toohello "Default".</span><span class="sxs-lookup"><span data-stu-id="2311b-161">You can define more endpoints in addition toohello "Default" endpoint.</span></span> <span data-ttu-id="2311b-162">tooadd Hola de punto de conexión, haga clic en **administrar extremos** final Hola del portal de servicios Web de Azure Machine Learning de hello panel tooopen Hola.</span><span class="sxs-lookup"><span data-stu-id="2311b-162">tooadd hello endpoint, click **Manage Endpoints** at hello bottom of hello dashboard tooopen hello Azure Machine Learning Web Services portal.</span></span>
* <span data-ttu-id="2311b-163">toodelete un punto de conexión (no se puede eliminar el punto de conexión de Hola "Default"), haga clic en casilla de verificación de hello en principio Hola de fila del punto de conexión de Hola y haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="2311b-163">toodelete an endpoint (you cannot delete hello "Default" endpoint), click hello check box at hello beginning of hello endpoint row, and click **DELETE**.</span></span> <span data-ttu-id="2311b-164">Esto quita el punto de conexión de Hola Hola servicio Web.</span><span class="sxs-lookup"><span data-stu-id="2311b-164">This removes hello endpoint from hello Web service.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="2311b-165">Si una aplicación está utilizando el extremo del servicio web hello cuando se elimina el punto de conexión de hello, aplicación hello recibirá un Hola error próxima vez que intente servicio de hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="2311b-165">If an application is using hello web service endpoint when hello endpoint is deleted, hello application will receive an error hello next time it tries tooaccess hello service.</span></span>
  > 
  > 

<span data-ttu-id="2311b-166">Haga clic en nombre de Hola de un tooopen de punto de conexión de servicio Web.</span><span class="sxs-lookup"><span data-stu-id="2311b-166">Click hello name of a Web service endpoint tooopen it.</span></span> 

<span data-ttu-id="2311b-167">En el panel de hello, puede ver el uso general del servicio Web durante un período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="2311b-167">From hello dashboard, you can view overall usage of your Web service over a period of time.</span></span> <span data-ttu-id="2311b-168">Puede seleccionar tooview período Hola desde el menú desplegable periodo de hello en la esquina superior derecha de Hola de gráficos de uso de Hola.</span><span class="sxs-lookup"><span data-stu-id="2311b-168">You can select hello period tooview from hello Period dropdown menu in hello upper right of hello usage charts.</span></span> <span data-ttu-id="2311b-169">panel de Hello muestra hello siguiente información:</span><span class="sxs-lookup"><span data-stu-id="2311b-169">hello dashboard shows hello following information:</span></span>

* <span data-ttu-id="2311b-170">**Las solicitudes de un período** muestra un gráfico de paso del número de Hola de solicitudes Hola período de tiempo seleccionado.</span><span class="sxs-lookup"><span data-stu-id="2311b-170">**Requests Over Time** displays a step graph of hello number of requests over hello selected time period.</span></span> <span data-ttu-id="2311b-171">Puede ayudarlo a identificar si se están experimentando picos de uso.</span><span class="sxs-lookup"><span data-stu-id="2311b-171">It can help identify if you are experiencing spikes in usage.</span></span>
* <span data-ttu-id="2311b-172">**Las solicitudes de solicitudes y respuestas** muestra hello número total de llamadas de solicitud-respuesta servicio Hola ha recibido a través hello período de tiempo seleccionado y no se pudo cuántos de ellos.</span><span class="sxs-lookup"><span data-stu-id="2311b-172">**Request-Response Requests** displays hello total number of Request-Response calls hello service has received over hello selected time period and how many of them failed.</span></span>
* <span data-ttu-id="2311b-173">**Promedio de tiempo de respuesta de solicitud de proceso** muestra un promedio de tiempo de hello necesarios tooexecute Hola recibe solicitudes.</span><span class="sxs-lookup"><span data-stu-id="2311b-173">**Average Request-Response Compute Time** displays an average of hello time needed tooexecute hello received requests.</span></span>
* <span data-ttu-id="2311b-174">**Las solicitudes por lote** muestra hello el número total de servicio de Hola de solicitudes por lotes ha recibido a través Hola período de tiempo seleccionado y no se pudo cuántos de ellos.</span><span class="sxs-lookup"><span data-stu-id="2311b-174">**Batch Requests** displays hello total number of Batch Requests hello service has received over hello selected time period and how many of them failed.</span></span>
* <span data-ttu-id="2311b-175">**Promedio de latencia de trabajo** muestra un promedio de tiempo de hello necesarios tooexecute Hola recibe solicitudes.</span><span class="sxs-lookup"><span data-stu-id="2311b-175">**Average Job Latency** displays an average of hello time needed tooexecute hello received requests.</span></span>
* <span data-ttu-id="2311b-176">**Errores** muestra agregación del número de errores que se han producido hello en el servicio web de llamadas a toohello.</span><span class="sxs-lookup"><span data-stu-id="2311b-176">**Errors** displays hello aggregate number of errors that have occurred on calls toohello web service.</span></span>
* <span data-ttu-id="2311b-177">**Los costos de servicios** muestra hello cargos para el plan de facturación de hello asociado con el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="2311b-177">**Services Costs** displays hello charges for hello billing plan associated with hello service.</span></span>

<span data-ttu-id="2311b-178">Hola en página de configuración, puede actualizar Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="2311b-178">From hello Configure page, you can update hello following properties:</span></span>

* <span data-ttu-id="2311b-179">**Descripción** permite tooenter una descripción para el servicio Web de Hola.</span><span class="sxs-lookup"><span data-stu-id="2311b-179">**Description** allows you tooenter a description for hello Web service.</span></span> <span data-ttu-id="2311b-180">La descripción es un campo obligatorio.</span><span class="sxs-lookup"><span data-stu-id="2311b-180">Description is a required field.</span></span>
* <span data-ttu-id="2311b-181">**Registro** permite error tooenable o deshabilitar el registro en el extremo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2311b-181">**Logging** allows you tooenable or disable error logging on hello endpoint.</span></span> <span data-ttu-id="2311b-182">Para obtener más información sobre el registro, consulte [Habilitación del registro para los servicios web Machine Learning](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="2311b-182">For more information on Logging, see Enable [logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>
* <span data-ttu-id="2311b-183">**Habilitar los datos de ejemplo** permite tooprovide datos de ejemplo que puede usar tootest Hola respuesta de solicitud de servicio.</span><span class="sxs-lookup"><span data-stu-id="2311b-183">**Enable Sample data** allows you tooprovide sample data that you can use tootest hello Request-Response service.</span></span> <span data-ttu-id="2311b-184">Si ha creado el servicio web de hello en estudio de aprendizaje automático, datos de ejemplo de Hola procede de datos de hello su tootrain usa el modelo.</span><span class="sxs-lookup"><span data-stu-id="2311b-184">If you created hello web service in Machine Learning Studio, hello sample data is taken from hello data your used tootrain your model.</span></span> <span data-ttu-id="2311b-185">Si ha creado el servicio de hello mediante programación, los datos de Hola se toman de los datos de ejemplo de Hola proporcionados como parte del paquete de hello JSON.</span><span class="sxs-lookup"><span data-stu-id="2311b-185">If you created hello service programmatically, hello data is taken from hello example data you provided as part of hello JSON package.</span></span>

