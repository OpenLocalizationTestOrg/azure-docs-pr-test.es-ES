---
title: "Administración de un área de trabajo de Aprendizaje automático de Azure | Microsoft Docs"
description: "Administrar el acceso a las áreas de trabajo del aprendizaje automático de Azure, e implementar y administrar servicios web de la API del aprendizaje automático"
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
ms.openlocfilehash: 94800f51baf83311c33490cada5f991ff2101da9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-an-azure-machine-learning-workspace"></a><span data-ttu-id="c593c-103">Administración de un área de trabajo de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="c593c-103">Manage an Azure Machine Learning workspace</span></span>

> [!NOTE]
> <span data-ttu-id="c593c-104">Para obtener información acerca de cómo administrar servicios web en el portal Servicios web Machine Learning, consulte [Administración de un servicio web mediante el portal Servicios web Azure Machine Learning](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="c593c-104">For information on managing Web services in the Machine Learning Web Services portal, see [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span>
> 
> 

<span data-ttu-id="c593c-105">Las áreas de trabajo de Machine Learning se pueden administrar en Azure Portal o en el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="c593c-105">You can manage Machine Learning workspaces in either the Azure portal or the Azure classic portal.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="use-the-azure-portal"></a><span data-ttu-id="c593c-106">Uso del Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c593c-106">Use the Azure portal</span></span>

<span data-ttu-id="c593c-107">Para administrar un área de trabajo en Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="c593c-107">To manage a workspace in the Azure portal:</span></span>

1. <span data-ttu-id="c593c-108">Inicie sesión en [Azure Portal](https://portal.azure.com/) mediante una cuenta de administrador de la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="c593c-108">Sign in to the [Azure portal](https://portal.azure.com/) using an Azure subscription administrator account.</span></span>
2. <span data-ttu-id="c593c-109">En el cuadro de búsqueda de la parte superior de la página, escriba "áreas de trabajo de Machine Learning" y, después, seleccione **Áreas de trabajo de Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="c593c-109">In the search box at the top of the page, enter "machine learning workspaces" and then select **Machine Learning Workspaces**.</span></span>
3. <span data-ttu-id="c593c-110">Haga clic en el área de trabajo que desea administrar.</span><span class="sxs-lookup"><span data-stu-id="c593c-110">Click the workspace you want to manage.</span></span>

<span data-ttu-id="c593c-111">Además de la información de administración de recursos estándar y de las opciones disponibles, puede:</span><span class="sxs-lookup"><span data-stu-id="c593c-111">In addition to the standard resource management information and options available, you can:</span></span>

- <span data-ttu-id="c593c-112">Ver **Propiedades**: esta página muestra la información del área de trabajo y de los recursos, y puede cambiar la suscripción y el grupo de recursos con el que esta área de trabajo está conectado.</span><span class="sxs-lookup"><span data-stu-id="c593c-112">View **Properties** - This page displays the workspace and resource information, and you can change the subscription and resource group that this workspace is connected with.</span></span>
- <span data-ttu-id="c593c-113">**Resincronizar las claves de almacenamiento**: el área de trabajo mantiene las claves de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c593c-113">**Resync Storage Keys** - The workspace maintains keys to the storage account.</span></span> <span data-ttu-id="c593c-114">Si la cuenta de almacenamiento cambia las claves, puede hacer clic en **Resincronizar claves** para sincronizar las claves con el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="c593c-114">If the storage account changes keys, then you can click **Resync keys** to synchronize the keys with the workspace.</span></span>

<span data-ttu-id="c593c-115">Para administrar los servicios web asociados a esta área de trabajo, use el Portal de servicios web Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="c593c-115">To manage the web services associated with this workspace, use the Machine Learning Web Services portal.</span></span> <span data-ttu-id="c593c-116">Para obtener una información más completa, consulte [Administración de un servicio web mediante el portal Servicios web Azure Machine Learning](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="c593c-116">See [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md) for complete information.</span></span>

> [!NOTE]
> <span data-ttu-id="c593c-117">Para implementar o administrar nuevos servicios web, es preciso que se le haya asignado un rol de colaborador o administrador en la suscripción en la que se implementa el servicio web.</span><span class="sxs-lookup"><span data-stu-id="c593c-117">To deploy or manage New web services you must be assigned a contributor or administrator role on the subscription to which the web service is deployed.</span></span> <span data-ttu-id="c593c-118">Si invita a otro usuario a un área de trabajo de Machine Learning, debe asignarle un rol de colaborador o administrador en la suscripción para que pueda implementar o administrar servicios web.</span><span class="sxs-lookup"><span data-stu-id="c593c-118">If you invite another user to a machine learning workspace, you must assign them to a contributor or administrator role on the subscription before they can deploy or manage web services.</span></span> 
> 
><span data-ttu-id="c593c-119">Para más información sobre cómo establecer permisos de acceso, vea [Visualización de asignaciones de acceso para usuarios y grupos en Azure Portal (versión preliminar pública)](../active-directory/role-based-access-control-manage-assignments.md).</span><span class="sxs-lookup"><span data-stu-id="c593c-119">For more information on setting access permissions, see [View access assignments for users and groups in the Azure portal - Public preview](../active-directory/role-based-access-control-manage-assignments.md).</span></span>

## <a name="use-the-azure-classic-portal"></a><span data-ttu-id="c593c-120">Uso del Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="c593c-120">Use the Azure classic portal</span></span>

<span data-ttu-id="c593c-121">Mediante el Portal de Azure clásico, puede administrar las áreas de trabajo de Aprendizaje automático para realizar las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="c593c-121">Using the Azure classic portal, you can manage your Machine Learning workspaces to:</span></span>

* <span data-ttu-id="c593c-122">Supervisar el uso del área de trabajo</span><span class="sxs-lookup"><span data-stu-id="c593c-122">Monitor how the workspace is being used</span></span>
* <span data-ttu-id="c593c-123">Configurar el área de trabajo para permitir o denegar el acceso</span><span class="sxs-lookup"><span data-stu-id="c593c-123">Configure the workspace to allow or deny access</span></span>
* <span data-ttu-id="c593c-124">Administrar servicios web creados en el área de trabajo</span><span class="sxs-lookup"><span data-stu-id="c593c-124">Manage Web services created in the workspace</span></span>
* <span data-ttu-id="c593c-125">Eliminar el área de trabajo</span><span class="sxs-lookup"><span data-stu-id="c593c-125">Delete the workspace</span></span>

<span data-ttu-id="c593c-126">Además, la pestaña Panel muestra una descripción general del uso del área de trabajo y una vista rápida de la información que contiene.</span><span class="sxs-lookup"><span data-stu-id="c593c-126">In addition, the dashboard tab provides an overview of your workspace usage and a quick glance of your workspace information.</span></span>  

> [!TIP]
> <span data-ttu-id="c593c-127">En Azure Machine Learning Studio, en la pestaña **SERVICIOS WEB**, puede agregar, actualizar o eliminar un servicio web Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="c593c-127">In Azure Machine Learning Studio, on the **WEB SERVICES** tab, you can add, update, or delete a Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="c593c-128">Para administrar un área de trabajo en el Portal de Azure clásico:</span><span class="sxs-lookup"><span data-stu-id="c593c-128">To manage a workspace in the Azure classic portal:</span></span>

1. <span data-ttu-id="c593c-129">Inicie sesión en el [Portal de Azure clásico](https://manage.windowsazure.com/) con su cuenta de Microsoft Azure (use la cuenta que está asociada a la suscripción de Azure).</span><span class="sxs-lookup"><span data-stu-id="c593c-129">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) using your Microsoft Azure account - use the account that's associated with the Azure subscription.</span></span>
2. <span data-ttu-id="c593c-130">En el panel de servicios de Microsoft Azure, haga clic en **APRENDIZAJE AUTOMÁTICO**.</span><span class="sxs-lookup"><span data-stu-id="c593c-130">In the Microsoft Azure services panel, click **MACHINE LEARNING**.</span></span>
3. <span data-ttu-id="c593c-131">Haga clic en el área de trabajo que desea administrar.</span><span class="sxs-lookup"><span data-stu-id="c593c-131">Click the workspace you want to manage.</span></span>

<span data-ttu-id="c593c-132">La página del área de trabajo tiene tres pestañas:</span><span class="sxs-lookup"><span data-stu-id="c593c-132">The workspace page has three tabs:</span></span>

* <span data-ttu-id="c593c-133">**Panel** : permite ver el uso y la información del área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="c593c-133">**DASHBOARD** - Allows you to view workspace usage and information</span></span>
* <span data-ttu-id="c593c-134">**Configurar** : permite administrar el acceso al área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="c593c-134">**CONFIGURE** - Allows you to manage access to the workspace</span></span>
* <span data-ttu-id="c593c-135">**SERVICIOS WEB**: permite administrar los servicios web que se han publicado desde esta área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="c593c-135">**WEB SERVICES** - Allows you to manage Web services that have been published from this workspace</span></span>

### <a name="to-monitor-how-the-workspace-is-being-used"></a><span data-ttu-id="c593c-136">Para supervisar el uso del área de trabajo</span><span class="sxs-lookup"><span data-stu-id="c593c-136">To monitor how the workspace is being used</span></span>
<span data-ttu-id="c593c-137">Haga clic en la pestaña **Panel** .</span><span class="sxs-lookup"><span data-stu-id="c593c-137">Click the **DASHBOARD** tab.</span></span>

<span data-ttu-id="c593c-138">En el panel, puede ver el uso general del área de trabajo y obtener una vista rápida de su información.</span><span class="sxs-lookup"><span data-stu-id="c593c-138">From the dashboard, you can view overall usage of your workspace and get a quick glance of workspace information.</span></span>

* <span data-ttu-id="c593c-139">El gráfico **Proceso** muestra los recursos de proceso que se usan en el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="c593c-139">The **COMPUTE** chart shows the compute resources being used by the workspace.</span></span> <span data-ttu-id="c593c-140">Puede cambiar la vista para mostrar valores relativos o absolutos, y puede cambiar el período de tiempo que se muestra en el gráfico.</span><span class="sxs-lookup"><span data-stu-id="c593c-140">You can change the view to display relative or absolute values, and you can change the timeframe displayed in the chart.</span></span>
* <span data-ttu-id="c593c-141">**Información general del uso** : muestra el almacenamiento de Azure que usa el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="c593c-141">**Usage overview** displays Azure storage being used by the workspace.</span></span>
* <span data-ttu-id="c593c-142">**Vista rápida** : proporciona un resumen de la información del área de trabajo y vínculos útiles.</span><span class="sxs-lookup"><span data-stu-id="c593c-142">**Quick glance** provides a summary of workspace information and useful links.</span></span>

> [!NOTE]
> <span data-ttu-id="c593c-143">El vínculo **Iniciar sesión en ML Studio** permite abrir Machine Learning Studio mediante la cuenta Microsoft en la que haya iniciado la sesión actual.</span><span class="sxs-lookup"><span data-stu-id="c593c-143">The **Sign-in to ML Studio** link opens Machine Learning Studio using the Microsoft Account you are currently signed into.</span></span> <span data-ttu-id="c593c-144">La cuenta de Microsoft que usó para iniciar sesión en el Portal de Azure clásico para crear un área de trabajo no tiene automáticamente permiso para abrir el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="c593c-144">The Microsoft Account you used to sign in to the Azure classic portal to create a workspace does not automatically have permission to open that workspace.</span></span> <span data-ttu-id="c593c-145">Para abrir un área de trabajo, debe iniciar sesión en la cuenta de Microsoft que se definió como propietaria del área de trabajo. También puede hacerlo si recibe una invitación del propietario para unirse al área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="c593c-145">To open a workspace, you must be signed in to the Microsoft Account that was defined as the owner of the workspace, or you need to receive an invitation from the owner to join the workspace.</span></span>
> 
> 

### <a name="to-grant-or-suspend-access-for-users"></a><span data-ttu-id="c593c-146">Concesión o suspensión del acceso de los usuarios</span><span class="sxs-lookup"><span data-stu-id="c593c-146">To grant or suspend access for users</span></span>
<span data-ttu-id="c593c-147">Haga clic en la pestaña **Configurar** .</span><span class="sxs-lookup"><span data-stu-id="c593c-147">Click the **CONFIGURE** tab.</span></span>

<span data-ttu-id="c593c-148">En la pestaña de configuración puede realizar las acciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="c593c-148">From the configuration tab you can:</span></span>

* <span data-ttu-id="c593c-149">Suspender el acceso al área de trabajo de Aprendizaje automático haciendo clic en Denegar.</span><span class="sxs-lookup"><span data-stu-id="c593c-149">Suspend access to the Machine Learning workspace by clicking DENY.</span></span> <span data-ttu-id="c593c-150">Los usuarios ya no podrán abrir el área de trabajo en Estudio de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="c593c-150">Users will no longer be able to open the workspace in Machine Learning Studio.</span></span> <span data-ttu-id="c593c-151">Para restaurar el acceso, haga clic en Permitir.</span><span class="sxs-lookup"><span data-stu-id="c593c-151">To restore access, click ALLOW.</span></span>

<span data-ttu-id="c593c-152">Para administrar cuentas adicionales que dispongan de acceso al área de trabajo en Machine Learning Studio, haga clic en **Iniciar sesión en ML Studio** en la pestaña **PANEL** (consulte la nota anterior respecto a **Iniciar sesión en ML Studio**).</span><span class="sxs-lookup"><span data-stu-id="c593c-152">To manage additional accounts who have access to the workspace in Machine Learning Studio, click **Sign-in to ML Studio** in the **DASHBOARD** tab (see the preceeding note regarding **Sign-in to ML Studio**).</span></span> <span data-ttu-id="c593c-153">De esta manera, se abre el área de trabajo en Estudio de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="c593c-153">This opens the workspace in Machine Learning Studio.</span></span> <span data-ttu-id="c593c-154">Desde aquí, haga clic en la pestaña **CONFIGURACIÓN** y luego en **USUARIOS**.</span><span class="sxs-lookup"><span data-stu-id="c593c-154">From here, click the **SETTINGS** tab and then **USERS**.</span></span> <span data-ttu-id="c593c-155">Puede hacer clic en **INVITAR MÁS USUARIOS** para permitir el acceso a otros usuarios al área de trabajo. También puede seleccionar un usuario y hacer clic en **QUITAR**.</span><span class="sxs-lookup"><span data-stu-id="c593c-155">You can click **INVITE MORE USERS** to give users access to the workspace, or select a user and click **REMOVE**.</span></span>

### <a name="to-manage-web-services-in-this-workspace"></a><span data-ttu-id="c593c-156">Para administrar servicios web en esta área de trabajo</span><span class="sxs-lookup"><span data-stu-id="c593c-156">To manage web services in this workspace</span></span>
<span data-ttu-id="c593c-157">Haga clic en la ficha **Servicios web** .</span><span class="sxs-lookup"><span data-stu-id="c593c-157">Click the **WEB SERVICES** tab.</span></span>

<span data-ttu-id="c593c-158">Esto muestra una lista de servicios web publicados desde esta área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="c593c-158">This displays a list of web services published from this workspace.</span></span>
<span data-ttu-id="c593c-159">Para administrar un servicio web, haga clic en el nombre en la lista y se abrirá la página correspondiente.</span><span class="sxs-lookup"><span data-stu-id="c593c-159">To manage a web service, click the name in the list to open the Web service page.</span></span>

<span data-ttu-id="c593c-160">Un servicio web puede tener uno o varios puntos de conexión definidos.</span><span class="sxs-lookup"><span data-stu-id="c593c-160">A Web service may have one or more endpoints defined.</span></span>

* <span data-ttu-id="c593c-161">Puede definir más puntos de conexión, además del punto de conexión "predeterminado".</span><span class="sxs-lookup"><span data-stu-id="c593c-161">You can define more endpoints in addition to the "Default" endpoint.</span></span> <span data-ttu-id="c593c-162">Para agregar un punto de conexión, haga clic en **Manage Endpoints** (Administrar puntos de conexión) en la parte inferior del panel para abrir el portal Servicios web Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="c593c-162">To add the endpoint, click **Manage Endpoints** at the bottom of the dashboard to open the Azure Machine Learning Web Services portal.</span></span>
* <span data-ttu-id="c593c-163">Para eliminar un punto de conexión (no se puede eliminar el punto de conexión "Predeterminado"), haga clic en la casilla situada al principio de la fila del punto de conexión y luego en **ELIMINAR**.</span><span class="sxs-lookup"><span data-stu-id="c593c-163">To delete an endpoint (you cannot delete the "Default" endpoint), click the check box at the beginning of the endpoint row, and click **DELETE**.</span></span> <span data-ttu-id="c593c-164">De esta manera, se elimina el punto de conexión del servicio web.</span><span class="sxs-lookup"><span data-stu-id="c593c-164">This removes the endpoint from the Web service.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="c593c-165">Si una aplicación está utilizando el extremo del servicio web cuando se elimina dicho extremo, la aplicación recibirá un error la próxima vez que intente acceder al servicio.</span><span class="sxs-lookup"><span data-stu-id="c593c-165">If an application is using the web service endpoint when the endpoint is deleted, the application will receive an error the next time it tries to access the service.</span></span>
  > 
  > 

<span data-ttu-id="c593c-166">Haga clic en el nombre de un punto de conexión de servicio web para abrirlo.</span><span class="sxs-lookup"><span data-stu-id="c593c-166">Click the name of a Web service endpoint to open it.</span></span> 

<span data-ttu-id="c593c-167">En el panel puede ver el uso general del servicio web durante un periodo.</span><span class="sxs-lookup"><span data-stu-id="c593c-167">From the dashboard, you can view overall usage of your Web service over a period of time.</span></span> <span data-ttu-id="c593c-168">Puede seleccionar el periodo para verlo en el menú desplegable Periodo situado en la esquina superior derecha de los gráficos de uso.</span><span class="sxs-lookup"><span data-stu-id="c593c-168">You can select the period to view from the Period dropdown menu in the upper right of the usage charts.</span></span> <span data-ttu-id="c593c-169">El panel muestra la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="c593c-169">The dashboard shows the following information:</span></span>

* <span data-ttu-id="c593c-170">**Requests Over Time** (Solicitudes a lo largo de un periodo) muestra un gráfico de escalera del número de solicitudes durante el periodo seleccionado.</span><span class="sxs-lookup"><span data-stu-id="c593c-170">**Requests Over Time** displays a step graph of the number of requests over the selected time period.</span></span> <span data-ttu-id="c593c-171">Puede ayudarlo a identificar si se están experimentando picos de uso.</span><span class="sxs-lookup"><span data-stu-id="c593c-171">It can help identify if you are experiencing spikes in usage.</span></span>
* <span data-ttu-id="c593c-172">**Request-Response Requests** (Solicitudes de solicitud-respuesta) muestra el número total de llamadas de solicitud-respuesta que ha recibido el servicio durante el periodo seleccionado y cuántas tienen errores.</span><span class="sxs-lookup"><span data-stu-id="c593c-172">**Request-Response Requests** displays the total number of Request-Response calls the service has received over the selected time period and how many of them failed.</span></span>
* <span data-ttu-id="c593c-173">**Average Request-Response Compute Time** (Tiempo de proceso medio de solicitud-respuesta) muestra un promedio del tiempo necesario para ejecutar las solicitudes recibidas.</span><span class="sxs-lookup"><span data-stu-id="c593c-173">**Average Request-Response Compute Time** displays an average of the time needed to execute the received requests.</span></span>
* <span data-ttu-id="c593c-174">**Batch Requests** (Solicitudes por lotes) muestra el número total de solicitudes por lotes que ha recibido el servicio en el periodo seleccionado y cuántas tienen errores.</span><span class="sxs-lookup"><span data-stu-id="c593c-174">**Batch Requests** displays the total number of Batch Requests the service has received over the selected time period and how many of them failed.</span></span>
* <span data-ttu-id="c593c-175">**Average Job Latency** (Latencia media de los trabajos) muestra un promedio del tiempo necesario para ejecutar las solicitudes recibidas.</span><span class="sxs-lookup"><span data-stu-id="c593c-175">**Average Job Latency** displays an average of the time needed to execute the received requests.</span></span>
* <span data-ttu-id="c593c-176">**Errores** muestra el número total de errores que se han producido en las llamadas al servicio web.</span><span class="sxs-lookup"><span data-stu-id="c593c-176">**Errors** displays the aggregate number of errors that have occurred on calls to the web service.</span></span>
* <span data-ttu-id="c593c-177">**Services Costs** (Costos de los servicios) muestra los cargos correspondientes al plan de facturación asociado con el servicio.</span><span class="sxs-lookup"><span data-stu-id="c593c-177">**Services Costs** displays the charges for the billing plan associated with the service.</span></span>

<span data-ttu-id="c593c-178">En la página Configurar puede actualizar las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="c593c-178">From the Configure page, you can update the following properties:</span></span>

* <span data-ttu-id="c593c-179">**Descripción** permite escribir una descripción del servicio web.</span><span class="sxs-lookup"><span data-stu-id="c593c-179">**Description** allows you to enter a description for the Web service.</span></span> <span data-ttu-id="c593c-180">La descripción es un campo obligatorio.</span><span class="sxs-lookup"><span data-stu-id="c593c-180">Description is a required field.</span></span>
* <span data-ttu-id="c593c-181">**Registro** permite habilitar o deshabilitar el registro de errores en el punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="c593c-181">**Logging** allows you to enable or disable error logging on the endpoint.</span></span> <span data-ttu-id="c593c-182">Para obtener más información sobre el registro, consulte [Habilitación del registro para los servicios web Machine Learning](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="c593c-182">For more information on Logging, see Enable [logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>
* <span data-ttu-id="c593c-183">**Habilitar datos de ejemplo** permite ofrecer datos de ejemplo que pueden usarse para probar el servicio de solicitud-respuesta.</span><span class="sxs-lookup"><span data-stu-id="c593c-183">**Enable Sample data** allows you to provide sample data that you can use to test the Request-Response service.</span></span> <span data-ttu-id="c593c-184">Si ha creado el servicio web en Estudio de aprendizaje automático de Microsoft Azure, los datos de ejemplo se toman de los utilizados para entrenar el modelo.</span><span class="sxs-lookup"><span data-stu-id="c593c-184">If you created the web service in Machine Learning Studio, the sample data is taken from the data your used to train your model.</span></span> <span data-ttu-id="c593c-185">Si ha creado el servicio mediante programación, los datos se extraen de los datos de ejemplo ofrecidos como parte del paquete JSON.</span><span class="sxs-lookup"><span data-stu-id="c593c-185">If you created the service programmatically, the data is taken from the example data you provided as part of the JSON package.</span></span>

