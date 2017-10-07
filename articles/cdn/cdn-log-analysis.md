---
title: "análisis de aaaLog para red CDN de Azure | Documentos de Microsoft"
description: "Los clientes pueden habilitar el análisis de registros para la red CDN de Azure."
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 95e18b3c-b987-46c2-baa8-a27a029e3076
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: v-semcev
ms.openlocfilehash: 56e5a4fec46fd156cf38252732afb4522741d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-logs-for-azure-cdn"></a><span data-ttu-id="9641c-103">Registros de diagnóstico de red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="9641c-103">Diagnostics Logs for Azure CDN</span></span>

<span data-ttu-id="9641c-104">Después de habilitar CDN para la aplicación, es probable que se desea el uso CDN Hola toomonitor, comprobará el estado de saludo de la entrega y solucionar posibles problemas.</span><span class="sxs-lookup"><span data-stu-id="9641c-104">After enabling CDN for your application, you will likely want toomonitor hello CDN usage, check hello health of your delivery, and troubleshoot potential issues.</span></span> <span data-ttu-id="9641c-105">La red CDN de Azure proporciona estas funcionalidades con [Análisis Básico de la red CDN](cdn-analyze-usage-patterns.md) y [Registros de diagnóstico](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)</span><span class="sxs-lookup"><span data-stu-id="9641c-105">Azure CDN provides these capabilities with [CDN Core Analytics](cdn-analyze-usage-patterns.md) and [Diagnostic Logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)</span></span>

## <a name="cdn-core-analytics"></a><span data-ttu-id="9641c-106">Análisis Básico de la red CDN</span><span class="sxs-lookup"><span data-stu-id="9641c-106">CDN Core Analytics</span></span>
<span data-ttu-id="9641c-107">Como un usuario de red CDN de Azure actual con Verizon estándar o el perfil de premium, se le asignará ya tooview capaz de análisis de núcleo portal complementario de hello accesible a través de la opción de "Administrar" hello de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9641c-107">As a current Azure CDN user with Verizon standard or premium profile, you are already able tooview core analytics in hello supplemental portal accessible via hello "Manage" option from hello Azure portal.</span></span> 

## <a name="azure-diagnostic-logs"></a><span data-ttu-id="9641c-108">Registros de diagnóstico de Azure</span><span class="sxs-lookup"><span data-stu-id="9641c-108">Azure Diagnostic Logs</span></span>

<span data-ttu-id="9641c-109">Con esta nueva característica de Azure, ahora puede ver el análisis básico y guardarlo en uno o más destinos, entre los que se incluyen:</span><span class="sxs-lookup"><span data-stu-id="9641c-109">Azure With this new feature, you can now view core analytics and save them into one or more destinations including:</span></span>

 - <span data-ttu-id="9641c-110">Cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="9641c-110">Azure Storage account</span></span>
 - <span data-ttu-id="9641c-111">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="9641c-111">Azure Event Hubs</span></span>
 - [<span data-ttu-id="9641c-112">Repositorio de Log Analytics de OMS</span><span class="sxs-lookup"><span data-stu-id="9641c-112">OMS Log Analytics repository</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started)
 
 <span data-ttu-id="9641c-113">Esta característica está disponible para todos los puntos de conexión de red CDN que pertenecen tooVerizon (Standard y Premium) y perfiles de red CDN de Akamai (estándar).</span><span class="sxs-lookup"><span data-stu-id="9641c-113">This feature is available for all CDN endpoints belonging tooVerizon (Standard & Premium) and Akamai (Standard) CDN Profiles.</span></span>

<span data-ttu-id="9641c-114">Registros de diagnóstico le permiten tooexport métricas de uso básico de la red CDN extremo tooa de diversos orígenes, por lo que se puede utilizar de una manera personalizada.</span><span class="sxs-lookup"><span data-stu-id="9641c-114">Diagnostics logs allow you tooexport basic usage metrics from your CDN endpoint tooa variety of sources so that you can consume them in a customized way.</span></span> <span data-ttu-id="9641c-115">Por ejemplo, puede hacer Hola tipos de exportación de datos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9641c-115">For example, you can do hello following types of data export:</span></span>

- <span data-ttu-id="9641c-116">Exportar el almacenamiento de datos tooblob, exportar tooCSV y generar gráficos en excel.</span><span class="sxs-lookup"><span data-stu-id="9641c-116">Export data tooblob storage, export tooCSV, and generate graphs in excel.</span></span>
- <span data-ttu-id="9641c-117">Exporte los centros de datos tooevent y correlacionar con los datos de otros servicios de azure.</span><span class="sxs-lookup"><span data-stu-id="9641c-117">Export data tooevent hubs and correlate with data from other azure services.</span></span>
- <span data-ttu-id="9641c-118">Exportar datos toolog análisis y ver los datos en su propio espacio de trabajo OMS</span><span class="sxs-lookup"><span data-stu-id="9641c-118">Export data toolog analytics and view data in your own OMS work space</span></span>

<span data-ttu-id="9641c-119">Hello en la ilustración siguiente se muestra una vista de análisis de núcleo de CDN habitual en los datos.</span><span class="sxs-lookup"><span data-stu-id="9641c-119">hello following figure shows a typical CDN Core Analytics view into data.</span></span>

![Portal: Registros de diagnóstico](./media/cdn-diagnostics-log/01_OMS-workspace.png)

<span data-ttu-id="9641c-121">*Figura 1: vista de Análisis Básico de la red CDN*</span><span class="sxs-lookup"><span data-stu-id="9641c-121">*Figure 1 - CDN Core Analytics view*</span></span>

<span data-ttu-id="9641c-122">Hola tutorial pasa por esquema Hola de datos de análisis de núcleo de hello, pasos necesarios para habilitar la característica de Hola y entregarlos toovarious destinos y consumir a partir de estos destinos.</span><span class="sxs-lookup"><span data-stu-id="9641c-122">hello following walkthrough goes through hello schema of hello core analytics data, steps involved in enabling hello feature and delivering them toovarious destinations, and consuming from these destinations.</span></span>

## <a name="enable-logging-with-azure-portal"></a><span data-ttu-id="9641c-123">Habilitación del registro con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9641c-123">Enable logging with Azure portal</span></span>

> [!NOTE]
> <span data-ttu-id="9641c-124">Hello registros de diagnóstico se activan **desactivar** de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="9641c-124">hello diagnostics logs are turned **off** by default.</span></span> 

<span data-ttu-id="9641c-125">Siga los pasos de hello debajo de registro tooenable con análisis de núcleo de red CDN:</span><span class="sxs-lookup"><span data-stu-id="9641c-125">Follow hello steps below tooenable logging with CDN Core Analytics:</span></span>

<span data-ttu-id="9641c-126">Inicie sesión en toohello [portal de Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9641c-126">Sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="9641c-127">Si no se ha habilitado ya la red CDN para el flujo de trabajo, [habilítela](cdn-create-new-endpoint.md) antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="9641c-127">If you don't already have CDN enabled for your workflow, [Enable Azure CDN](cdn-create-new-endpoint.md) before you continue.</span></span>

1. <span data-ttu-id="9641c-128">En el portal de hello, navegue demasiado**perfil de CDN**.</span><span class="sxs-lookup"><span data-stu-id="9641c-128">In hello portal, navigate too**CDN profile**.</span></span>
2. <span data-ttu-id="9641c-129">Seleccione un perfil de CDN, a continuación, seleccione el extremo de red CDN Hola que desea tooenable **registros de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="9641c-129">Select a CDN profile, then select hello CDN endpoint that you want tooenable **Diagnostics Logs**.</span></span>

    ![Portal: Registros de diagnóstico](./media/cdn-diagnostics-log/02_Browse-to-Diagnostics-logs.png)

3. <span data-ttu-id="9641c-131">Vaya demasiado**registros de diagnóstico** hoja bajo **supervisión** sección, a continuación, cambiar el estado de hello demasiado**en**.</span><span class="sxs-lookup"><span data-stu-id="9641c-131">Go too**Diagnostics Logs** blade Under **Monitoring** section, then change hello status too**On**.</span></span>

    ![Portal: Registros de diagnóstico](./media/cdn-diagnostics-log/03_Diagnostics-logs-options.png)

### <a name="enable-logging-with-azure-storage"></a><span data-ttu-id="9641c-133">Habilitación del registro con Azure Storage</span><span class="sxs-lookup"><span data-stu-id="9641c-133">Enable logging with Azure Storage</span></span>
    
<span data-ttu-id="9641c-134">toouse almacenamiento de Azure toostore Hola registros, seleccione **tooa cuenta de almacenamiento de archivo**, seleccione los días de retención y haga clic en **CoreAnalytics** en **registro**.</span><span class="sxs-lookup"><span data-stu-id="9641c-134">toouse Azure Storage toostore hello logs, select **Archive tooa storage account**, select retention days, and click **CoreAnalytics** under **Log**.</span></span>

![Portal: Registros de diagnóstico](./media/cdn-diagnostics-log/04_Diagnostics-logs-storage.png)

<span data-ttu-id="9641c-136">*Figura 2: registro con Azure Storage*</span><span class="sxs-lookup"><span data-stu-id="9641c-136">*Figure 2 - Logging with Azure Storage*</span></span>

### <a name="logging-with-oms-log-analytics"></a><span data-ttu-id="9641c-137">Registro con Log Analytics de OMS</span><span class="sxs-lookup"><span data-stu-id="9641c-137">Logging with OMS Log Analytics</span></span>

<span data-ttu-id="9641c-138">registros de toouse análisis de registros de OMS toostore hello, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="9641c-138">toouse OMS Log Analytics toostore hello logs, follow these steps:</span></span>

1. <span data-ttu-id="9641c-139">De hello **registros de diagnóstico** hoja bajo **supervisión**, seleccione **enviar tooLog análisis** desde</span><span class="sxs-lookup"><span data-stu-id="9641c-139">From hello **Diagnostics Logs** blade Under **Monitoring**, select **Send tooLog Analytics** from</span></span> 

    ![Portal: Registros de diagnóstico](./media/cdn-diagnostics-log/05_Ready-to-Configure.png)    

2. <span data-ttu-id="9641c-141">Configurar el registro de análisis de registros de hello haciendo clic en configurar.</span><span class="sxs-lookup"><span data-stu-id="9641c-141">Configure hello Log Analytics logging by clicking on Configure.</span></span> <span data-ttu-id="9641c-142">Esto le llevará tooa el cuadro de diálogo donde puede seleccionar un área de trabajo anterior o cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="9641c-142">This takes you tooa dialog where you can select a previous workspace or create a new one.</span></span>

    ![Portal: Registros de diagnóstico](./media/cdn-diagnostics-log/06_Choose-workspace.png)

3. <span data-ttu-id="9641c-144">Haga clic en **Crear nueva área de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="9641c-144">Click **Create New Workspace**.</span></span>

    ![Portal: Registros de diagnóstico](./media/cdn-diagnostics-log/07_Create-new.png)

4. <span data-ttu-id="9641c-146">A continuación debe seleccionar un nuevo nombre de área de trabajo, una suscripción existente, un grupo de recursos (nuevo o existente), la ubicación y el plan de tarifa.</span><span class="sxs-lookup"><span data-stu-id="9641c-146">Next you must select a new workspace name, existing subscription, resource group (new or existing), location, and pricing tier.</span></span> <span data-ttu-id="9641c-147">Tiene la opción de hello Anclar este panel de tooyour de configuración de.</span><span class="sxs-lookup"><span data-stu-id="9641c-147">You have hello option of pinning this configuration tooyour dashboard.</span></span> <span data-ttu-id="9641c-148">Haga clic en configuración de hello toocomplete Aceptar.</span><span class="sxs-lookup"><span data-stu-id="9641c-148">Click OK toocomplete hello configuration.</span></span>

    <span data-ttu-id="9641c-149">A continuación debería ver el área de trabajo con los nombres del grupo de recursos y del área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="9641c-149">Next you should see your workspace with your OMS Workspace and Resource group names.</span></span> <span data-ttu-id="9641c-150">Los nombres deben ser únicos y solo se pueden usar letras, números y guiones.</span><span class="sxs-lookup"><span data-stu-id="9641c-150">Names must be unique and can only use letters, numbers, and hyphens.</span></span> <span data-ttu-id="9641c-151">No se permiten espacios ni caracteres de subrayado.</span><span class="sxs-lookup"><span data-stu-id="9641c-151">Spaces and underscores are not allowed.</span></span> 

    ![Portal: Registros de diagnóstico](./media/cdn-diagnostics-log/08_Workspace-resource.png)

5. <span data-ttu-id="9641c-153">A continuación, obtendrá un mensaje breve que indica que se ha creado el área de trabajo y se devuelven tooyour la pantalla de configuración de registro.</span><span class="sxs-lookup"><span data-stu-id="9641c-153">You next get a short message saying that your workspace has been created and you are returned tooyour logging configuration screen.</span></span> <span data-ttu-id="9641c-154">Puede confirmar nombre hello del área de trabajo de análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="9641c-154">You can confirm hello name of your Log Analytics workspace.</span></span>

    ![Portal: Registros de diagnóstico](./media/cdn-diagnostics-log/09_Return-to-logging.png)

    <span data-ttu-id="9641c-156">Una vez haya configurado la configuración de análisis de registros de hello, asegúrese de que también casilla hello CoreAnalytics para el registro de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="9641c-156">Once you have set up hello Log Analytics configuration, make sure you also check hello CoreAnalytics box for CDN logging.</span></span>

6. <span data-ttu-id="9641c-157">Si todo está tooyour gusto, haga clic en hello **guardar** situado en la parte superior de hello del cuadro de diálogo de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="9641c-157">If everything is tooyour liking, click hello **Save** button at hello top of hello configuration dialog.</span></span>

    ![Portal: Registros de diagnóstico](./media/cdn-diagnostics-log/10_Save-me.png)

    <span data-ttu-id="9641c-159">Hola **guardar** botón ya no está activa y que hello en/botón ahora es ON, pero azul en lugar de púrpura.</span><span class="sxs-lookup"><span data-stu-id="9641c-159">hello **Save** button is no longer active and that hello ON/OFF button is now ON, but blue instead of purple.</span></span>

7. <span data-ttu-id="9641c-160">Si desea que toosee la nueva área de trabajo OMS, vaya tooyour portal de Azure panel, haga clic en nombre de hello del área de trabajo de análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="9641c-160">If you want toosee your new OMS workspace, go tooyour Azure portal Dashboard, click hello name of your Log Analytics workspace.</span></span> <span data-ttu-id="9641c-161">A continuación, verá el área de trabajo (asegúrese de que el área de trabajo de OMS se resalta en hello izquierda).</span><span class="sxs-lookup"><span data-stu-id="9641c-161">Next you will see your workspace (make sure that OMS Workspace is highlighted on hello left).</span></span> <span data-ttu-id="9641c-162">Haga clic en toosee de icono de Portal de OMS Hola el área de trabajo en el repositorio OMS Hola.</span><span class="sxs-lookup"><span data-stu-id="9641c-162">Click on hello OMS Portal tile toosee your workspace in hello OMS repository.</span></span> 

    ![Portal: Registros de diagnóstico](./media/cdn-diagnostics-log/11_OMS-dashboard.png) 

    <span data-ttu-id="9641c-164">El repositorio OMS ahora está listo toolog datos.</span><span class="sxs-lookup"><span data-stu-id="9641c-164">Your OMS repository is now ready toolog data.</span></span> <span data-ttu-id="9641c-165">En orden tooconsume esos datos, debe usar un [solución de OMS](#consuming-oms-log-analytics-data), cubierto más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="9641c-165">In order tooconsume that data, you must use an [OMS Solution](#consuming-oms-log-analytics-data), covered later in this article.</span></span>

<span data-ttu-id="9641c-166">Para más información sobre los retardos en el registro de datos, vaya [aquí](#log-data-delays).</span><span class="sxs-lookup"><span data-stu-id="9641c-166">For more information about log data delays, go [here](#log-data-delays).</span></span>

## <a name="enable-logging-with-powershell"></a><span data-ttu-id="9641c-167">Habilitación del registro con PowerShell</span><span class="sxs-lookup"><span data-stu-id="9641c-167">Enable logging with PowerShell</span></span>

<span data-ttu-id="9641c-168">A continuación se muestra un ejemplo sobre cómo tooenable y obtener registros de diagnóstico a través de Hola Cmdlets de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="9641c-168">Below is an example on how tooenable and get Diagnostic Logs via hello Azure PowerShell Cmdlets.</span></span>

###<a name="enabling-diagnostic-logs-in-a-storage-account"></a><span data-ttu-id="9641c-169">Habilitación de registros de diagnóstico en una cuenta de Storage</span><span class="sxs-lookup"><span data-stu-id="9641c-169">Enabling Diagnostic Logs in a Storage Account</span></span>

<span data-ttu-id="9641c-170">Inicio de sesión y selección de una suscripción:</span><span class="sxs-lookup"><span data-stu-id="9641c-170">First log in and select a subscription:</span></span>

    Login-AzureRmAccount 

    Select-AzureSubscription -SubscriptionId 


<span data-ttu-id="9641c-171">tooEnable registros de diagnóstico de una cuenta de almacenamiento, use este comando:</span><span class="sxs-lookup"><span data-stu-id="9641c-171">tooEnable Diagnostic Logs in a Storage Account, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}" -StorageAccountId "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicStorage/storageAccounts/{storageAccountName}" -Enabled $true -Categories CoreAnalytics
```
<span data-ttu-id="9641c-172">tooEnable registros de diagnóstico en un área de trabajo OMS, use este comando:</span><span class="sxs-lookup"><span data-stu-id="9641c-172">tooEnable Diagnostics Logs in an OMS workspace, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/`{subscriptionId}<subscriptionId>
    .<subscriptionName>" -WorkspaceId "/subscriptions/<workspaceId>.<workspaceName>" -Enabled $true -Categories CoreAnalytics 
```



## <a name="consuming-diagnostics-logs-from-azure-storage"></a><span data-ttu-id="9641c-173">Consumo de registros de diagnósticos desde Azure Storage</span><span class="sxs-lookup"><span data-stu-id="9641c-173">Consuming diagnostics logs from Azure Storage</span></span>
<span data-ttu-id="9641c-174">Esta sección describe los esquemas de Hola de análisis de núcleo CDN Hola, cómo éstos se organizan dentro de una cuenta de almacenamiento de Azure y proporciona Hola de toodownload de código de ejemplo se registra en el archivo CSV de tooa.</span><span class="sxs-lookup"><span data-stu-id="9641c-174">This section describes hello schema of hello CDN core analytics, how these are organized inside of an Azure Storage Account and provides sample code toodownload hello logs in tooa CSV file.</span></span>

### <a name="using-microsoft-azure-storage-explorer"></a><span data-ttu-id="9641c-175">Uso del Explorador de Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="9641c-175">Using Microsoft Azure Storage Explorer</span></span>
<span data-ttu-id="9641c-176">Antes de poder acceder a datos de análisis de núcleo de Hola de hello cuenta de almacenamiento de Azure, debe primero un contenido de herramienta tooaccess hello en una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9641c-176">Before you can access hello core analytics data from hello Azure Storage Account, you first need a tool tooaccess hello contents in a storage account.</span></span> <span data-ttu-id="9641c-177">Aunque hay varias herramientas disponibles en el mercado de hello, Hola uno que se recomienda es hello Explorador de almacenamiento de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9641c-177">While there are several tools available in hello market, hello one that we recommend is hello Microsoft Azure Storage Explorer.</span></span> <span data-ttu-id="9641c-178">Puede descargar la herramienta de Hola desde [aquí](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="9641c-178">You can download hello tool from [here](http://storageexplorer.com/).</span></span> <span data-ttu-id="9641c-179">Después de descargar e instalar software de hello, configurarlo toouse Hola misma cuenta de almacenamiento de Azure que se configuró como un toohello registros de diagnósticos de red CDN de destino.</span><span class="sxs-lookup"><span data-stu-id="9641c-179">After downloading and installing hello software, configure it toouse hello same Azure Storage Account that was configured as a destination toohello CDN Diagnostics Logs.</span></span>

1.  <span data-ttu-id="9641c-180">Abra el **Explorador de Microsoft Azure Storage**</span><span class="sxs-lookup"><span data-stu-id="9641c-180">Open **Microsoft Azure Storage Explorer**</span></span>
2.  <span data-ttu-id="9641c-181">Busque la cuenta de almacenamiento de Hola</span><span class="sxs-lookup"><span data-stu-id="9641c-181">Locate hello storage account</span></span>
3.  <span data-ttu-id="9641c-182">Vaya toohello **"Contenedores de blobs"** nodo bajo este almacenamiento cuenta y expanda el nodo de Hola</span><span class="sxs-lookup"><span data-stu-id="9641c-182">Go toohello **“Blob Containers”** node under this storage account and expand hello node</span></span>
4.  <span data-ttu-id="9641c-183">Contenedor de hello seleccione denominado **"coreanalytics de registros de visión"** y haga doble clic en él</span><span class="sxs-lookup"><span data-stu-id="9641c-183">Select hello container named **“insights-logs-coreanalytics”** and double-click it</span></span>
5.  <span data-ttu-id="9641c-184">Mostrar los resultados de una en hello panel derecho a partir de hello primero nivel, qué aspecto **"resourceId ="**.</span><span class="sxs-lookup"><span data-stu-id="9641c-184">Results show up on hello right-hand pane starting with hello first level, which looks like **“resourceId=”**.</span></span> <span data-ttu-id="9641c-185">Siga haciendo clic en forma de hello todos los hasta que vea el archivo hello **PT1H.json**.</span><span class="sxs-lookup"><span data-stu-id="9641c-185">Continue clicking all hello way until you see hello file **PT1H.json**.</span></span> <span data-ttu-id="9641c-186">Vea Hola después Nota para ver una explicación de la ruta de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="9641c-186">See hello following note for explanation of hello path.</span></span>
6.  <span data-ttu-id="9641c-187">Cada blob **PT1H.json** representa Hola registros de análisis durante una hora para un punto de conexión de red CDN concreto o de su dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="9641c-187">Each blob **PT1H.json** represents hello analytics logs for one hour for a specific CDN endpoint or its custom domain.</span></span>
7.  <span data-ttu-id="9641c-188">esquema de Hola de contenido de Hola de este archivo JSON se describe en la sección de hello esquema de hello registros de análisis de núcleo</span><span class="sxs-lookup"><span data-stu-id="9641c-188">hello schema of hello contents of this JSON file is described in hello section Schema of hello Core Analytics Logs</span></span>


> [!NOTE]
> <span data-ttu-id="9641c-189">**Formato de ruta de acceso de blob**</span><span class="sxs-lookup"><span data-stu-id="9641c-189">**Blob path format**</span></span>
> 
> <span data-ttu-id="9641c-190">Los registros de análisis básico se generan cada hora.</span><span class="sxs-lookup"><span data-stu-id="9641c-190">Core Analytics logs are generated every hour.</span></span> <span data-ttu-id="9641c-191">Todos los datos de una hora se recopilan y almacenan dentro de un único blob de Azure como una carga JSON.</span><span class="sxs-lookup"><span data-stu-id="9641c-191">All data for an hour are collected and stored inside a single Azure Blob as a JSON payload.</span></span> <span data-ttu-id="9641c-192">ruta de acceso de Hello toothis blobs de Azure aparece como si hay una estructura jerárquica.</span><span class="sxs-lookup"><span data-stu-id="9641c-192">hello path toothis Azure Blob appears as if there is a hierarchical structure.</span></span> <span data-ttu-id="9641c-193">Esto es porque interpreta la herramienta Explorador de almacenamiento de hello '/' como separador de directorios y muestra la jerarquía de Hola para su comodidad.</span><span class="sxs-lookup"><span data-stu-id="9641c-193">This is because hello Storage explorer tool interprets '/' as a directory separator and shows hello hierarchy for convenience.</span></span> <span data-ttu-id="9641c-194">En realidad, ruta de acceso completa de hello representa solo el nombre del blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="9641c-194">Actually, hello whole path just represents hello blob name.</span></span> <span data-ttu-id="9641c-195">Este nombre de blob de hello sigue Hola sigue la convención de nomenclatura</span><span class="sxs-lookup"><span data-stu-id="9641c-195">This name of hello blob follows hello following naming convention</span></span> 
    
    resourceId=/SUBSCRIPTIONS/{Subscription Id}/RESOURCEGROUPS/{Resource Group Name}/PROVIDERS/MICROSOFT.CDN/PROFILES/{Profile Name}/ENDPOINTS/{Endpoint Name}/ y={Year}/m={Month}/d={Day}/h={Hour}/m={Minutes}/PT1H.json

<span data-ttu-id="9641c-196">**Descripción de los campos:**</span><span class="sxs-lookup"><span data-stu-id="9641c-196">**Description of fields:**</span></span>

|<span data-ttu-id="9641c-197">value</span><span class="sxs-lookup"><span data-stu-id="9641c-197">value</span></span>|<span data-ttu-id="9641c-198">Descripción</span><span class="sxs-lookup"><span data-stu-id="9641c-198">description</span></span>|
|-------|---------|
|<span data-ttu-id="9641c-199">Id. de suscripción</span><span class="sxs-lookup"><span data-stu-id="9641c-199">Subscription ID</span></span>    |<span data-ttu-id="9641c-200">Id. de suscripción de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="9641c-200">ID of hello Azure Subscription.</span></span> <span data-ttu-id="9641c-201">Está en formato de Guid de Hola.</span><span class="sxs-lookup"><span data-stu-id="9641c-201">This is in hello Guid format.</span></span>|
|<span data-ttu-id="9641c-202">Recurso</span><span class="sxs-lookup"><span data-stu-id="9641c-202">Resource</span></span> |<span data-ttu-id="9641c-203">Nombre de grupo de recursos de red CDN Hola recursos grupo toowhich Hola pertenecen.</span><span class="sxs-lookup"><span data-stu-id="9641c-203">Group Name   Name of hello resource group toowhich hello CDN resources belong.</span></span>|
|<span data-ttu-id="9641c-204">Nombre del perfil</span><span class="sxs-lookup"><span data-stu-id="9641c-204">Profile Name</span></span> |<span data-ttu-id="9641c-205">Nombre del perfil de CDN Hola</span><span class="sxs-lookup"><span data-stu-id="9641c-205">Name of hello CDN Profile</span></span>|
|<span data-ttu-id="9641c-206">Nombre del punto de conexión</span><span class="sxs-lookup"><span data-stu-id="9641c-206">Endpoint Name</span></span> |<span data-ttu-id="9641c-207">Nombre del extremo de red CDN Hola</span><span class="sxs-lookup"><span data-stu-id="9641c-207">Name of hello CDN Endpoint</span></span>|
|<span data-ttu-id="9641c-208">Year</span><span class="sxs-lookup"><span data-stu-id="9641c-208">Year</span></span>|  <span data-ttu-id="9641c-209">representación en forma de 4 dígitos del año de hello, por ejemplo, de 2017</span><span class="sxs-lookup"><span data-stu-id="9641c-209">4-digit representation of hello year for example, 2017</span></span>|
|<span data-ttu-id="9641c-210">Mes</span><span class="sxs-lookup"><span data-stu-id="9641c-210">Month</span></span>| <span data-ttu-id="9641c-211">representación de 2 dígitos del número del mes Hola.</span><span class="sxs-lookup"><span data-stu-id="9641c-211">2-digit representation of hello month number.</span></span> <span data-ttu-id="9641c-212">01=enero ... 12=diciembre</span><span class="sxs-lookup"><span data-stu-id="9641c-212">01=January ... 12=December</span></span>|
|<span data-ttu-id="9641c-213">Día</span><span class="sxs-lookup"><span data-stu-id="9641c-213">Day</span></span>|   <span data-ttu-id="9641c-214">representación de 2 dígitos del día de hello del mes de Hola</span><span class="sxs-lookup"><span data-stu-id="9641c-214">2 digit representation of hello day of hello month</span></span>|
|<span data-ttu-id="9641c-215">PT1H.json</span><span class="sxs-lookup"><span data-stu-id="9641c-215">PT1H.json</span></span>| <span data-ttu-id="9641c-216">Archivo JSON real donde se almacenan los datos de análisis de Hola</span><span class="sxs-lookup"><span data-stu-id="9641c-216">Actual JSON file where hello analytics data is stored</span></span>|

### <a name="exporting-hello-core-analytics-data-tooa-csv-file"></a><span data-ttu-id="9641c-217">Exportar datos de análisis de núcleo de hello tooa archivo CSV</span><span class="sxs-lookup"><span data-stu-id="9641c-217">Exporting hello Core Analytics Data tooa CSV File</span></span>

<span data-ttu-id="9641c-218">toomake TI tooaccess fácil Hola análisis Core, proporcionamos un código de ejemplo para una herramienta que permite descargar los archivos JSON de hello en un formato de archivo sin formato separados por comas, que puede ser usado tooeasily crear gráficos u otras agregaciones.</span><span class="sxs-lookup"><span data-stu-id="9641c-218">toomake it easy tooaccess hello Core Analytics, we provide a sample code for a tool, which allows downloading hello JSON files into a flat comma-separated file format, which can be used tooeasily create charts or other aggregations.</span></span>

<span data-ttu-id="9641c-219">Le mostramos cómo puede usar la herramienta de hello:</span><span class="sxs-lookup"><span data-stu-id="9641c-219">Here is how you can use hello tool:</span></span>

1.  <span data-ttu-id="9641c-220">Visite el vínculo de Hola github: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )</span><span class="sxs-lookup"><span data-stu-id="9641c-220">Visit hello github link: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv ](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )</span></span>
2.  <span data-ttu-id="9641c-221">Descargar código de hello</span><span class="sxs-lookup"><span data-stu-id="9641c-221">Download hello code</span></span>
3.  <span data-ttu-id="9641c-222">Siga las instrucciones toocompile y configurar</span><span class="sxs-lookup"><span data-stu-id="9641c-222">Follow instructions toocompile and configure</span></span>
4.  <span data-ttu-id="9641c-223">Ejecutar la herramienta de Hola</span><span class="sxs-lookup"><span data-stu-id="9641c-223">Run hello tool</span></span>
5.  <span data-ttu-id="9641c-224">Archivo CSV resultante muestra datos de análisis de hello en una jerarquía plana simple.</span><span class="sxs-lookup"><span data-stu-id="9641c-224">Resulting CSV file shows hello analytics data in a simple flat hierarchy.</span></span>

## <a name="consuming-diagnostics-logs-from-an-oms-log-analytics-repository"></a><span data-ttu-id="9641c-225">Consumo de registros de diagnóstico desde un repositorio de Log Analytics de OMS</span><span class="sxs-lookup"><span data-stu-id="9641c-225">Consuming diagnostics logs from an OMS Log Analytics repository</span></span>
<span data-ttu-id="9641c-226">Análisis de registros es un servicio en Operations Management Suite (OMS) que supervisa su toomaintain de entornos de nube y locales su disponibilidad y el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="9641c-226">Log Analytics is a service in Operations Management Suite (OMS) that monitors your cloud and on-premises environments toomaintain their availability and performance.</span></span> <span data-ttu-id="9641c-227">Recopila los datos generados por los recursos en los entornos de nube y locales y de otros análisis de tooprovide herramientas supervisión a través de varios orígenes.</span><span class="sxs-lookup"><span data-stu-id="9641c-227">It collects data generated by resources in your cloud and on-premises environments and from other monitoring tools tooprovide analysis across multiple sources.</span></span> 

<span data-ttu-id="9641c-228">toouse análisis de registros, debe [habilitar el registro](#enable-logging-with-azure-storage) repositorio de análisis de registros de OMS de Azure toohello, que se describe anteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="9641c-228">toouse Log Analytics, you must [enable logging](#enable-logging-with-azure-storage) toohello Azure OMS Log Analytics repository, which is discussed earlier in this article.</span></span>

### <a name="using-hello-oms-repository"></a><span data-ttu-id="9641c-229">Uso de hello repositorio de OMS</span><span class="sxs-lookup"><span data-stu-id="9641c-229">Using hello OMS Repository</span></span>

 <span data-ttu-id="9641c-230">Hola siguiente diagrama muestra la arquitectura de Hola de entradas de Hola y salidas del repositorio de hello:</span><span class="sxs-lookup"><span data-stu-id="9641c-230">hello following diagram shows hello architecture of hello inputs and outputs of hello repository:</span></span>

![Repositorio de Log Analytics de OMS](./media/cdn-diagnostics-log/12_Repo-overview.png)

<span data-ttu-id="9641c-232">*Figura 3: repositorio de Log Analytics*</span><span class="sxs-lookup"><span data-stu-id="9641c-232">*Figure 3 - Log Analytics Repository*</span></span>

<span data-ttu-id="9641c-233">Puede mostrar datos de hello en una variedad de maneras con las soluciones de administración.</span><span class="sxs-lookup"><span data-stu-id="9641c-233">You can display hello data in a variety of ways by using Management Solutions.</span></span> <span data-ttu-id="9641c-234">Puede obtener soluciones de administración de hello [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).</span><span class="sxs-lookup"><span data-stu-id="9641c-234">You can obtain Management Solutions from hello [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).</span></span>

<span data-ttu-id="9641c-235">Puede instalar soluciones de administración de Azure marketplace, haga clic en hello **obtenerlo ahora** vínculo Hola final de cada solución.</span><span class="sxs-lookup"><span data-stu-id="9641c-235">You can install management solutions from Azure marketplace by clicking hello **Get it now** link at hello bottom of each solution.</span></span>

### <a name="adding-an-oms-cdn-management-solution"></a><span data-ttu-id="9641c-236">Agregación de una solución de administración de la red CDN de OMS</span><span class="sxs-lookup"><span data-stu-id="9641c-236">Adding an OMS CDN Management Solution</span></span>

<span data-ttu-id="9641c-237">Siga estas tooadd una solución de administración de pasos:</span><span class="sxs-lookup"><span data-stu-id="9641c-237">Follow these steps tooadd a Management Solution:</span></span>

1.   <span data-ttu-id="9641c-238">Si aún no lo ha hecho, inicie sesión en toohello portal de Azure con su suscripción de Azure y vaya tooyour panel.</span><span class="sxs-lookup"><span data-stu-id="9641c-238">If you haven't already done so, sign in toohello Azure portal using your Azure subscription and go tooyour Dashboard.</span></span>
    <span data-ttu-id="9641c-239">![Panel de Azure](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="9641c-239">![Azure Dashboard](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span></span>

2. <span data-ttu-id="9641c-240">Hola **New** hoja bajo **Marketplace**, seleccione **supervisión + administración**.</span><span class="sxs-lookup"><span data-stu-id="9641c-240">In hello **New** blade under **Marketplace**, select **Monitoring + management**.</span></span>

    ![Marketplace](./media/cdn-diagnostics-log/14_Marketplace.png)

3. <span data-ttu-id="9641c-242">Hola **supervisión + administración** hoja, haga clic en **ver todas**.</span><span class="sxs-lookup"><span data-stu-id="9641c-242">In hello **Monitoring + management** blade, click **See all**.</span></span>

    ![Ver todos](./media/cdn-diagnostics-log/15_See-all.png)

4.  <span data-ttu-id="9641c-244">Búsqueda de CDN en el cuadro de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="9641c-244">Search for CDN in hello search box.</span></span>

    ![Ver todos](./media/cdn-diagnostics-log/16_Search-for.png)

5.  <span data-ttu-id="9641c-246">Seleccione **Análisis Básico de la red CDN de Azure**.</span><span class="sxs-lookup"><span data-stu-id="9641c-246">Select **Azure CDN Core Analytics**.</span></span> 

    ![Ver todos](./media/cdn-diagnostics-log/17_Core-analytics.png)

6.  <span data-ttu-id="9641c-248">Después de hacer clic **crear**, estará más toocreate una nueva área de trabajo OMS o utilizar uno existente.</span><span class="sxs-lookup"><span data-stu-id="9641c-248">After clicking **Create**, you will be asked toocreate a new OMS workspace or use an existing one.</span></span> 

    ![Ver todos](./media/cdn-diagnostics-log/18_Adding-solution.png)

7.  <span data-ttu-id="9641c-250">Seleccione el área de trabajo de Hola que creó antes.</span><span class="sxs-lookup"><span data-stu-id="9641c-250">Select hello workspace you created before.</span></span> <span data-ttu-id="9641c-251">A continuación, deberá tooadd una cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="9641c-251">You then need tooadd an automation account.</span></span>

    ![Ver todos](./media/cdn-diagnostics-log/19_Add-automation.png)

8. <span data-ttu-id="9641c-253">Hola de pantalla siguiente muestra formulario de la cuenta de automatización Hola que se debe rellenar.</span><span class="sxs-lookup"><span data-stu-id="9641c-253">hello following screen shows hello automation account form you must fill out.</span></span> 

    ![Ver todos](./media/cdn-diagnostics-log/20_Automation.png)

9. <span data-ttu-id="9641c-255">Una vez haya creado la cuenta de automatización de hello, está listo tooadd la solución.</span><span class="sxs-lookup"><span data-stu-id="9641c-255">Once you have created hello automation account, you are ready tooadd your solution.</span></span> <span data-ttu-id="9641c-256">Haga clic en hello **crear** botón.</span><span class="sxs-lookup"><span data-stu-id="9641c-256">Click hello **Create** button.</span></span>

    ![Ver todos](./media/cdn-diagnostics-log/21_Ready.png)

10. <span data-ttu-id="9641c-258">La solución se ha agregado tooyour área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="9641c-258">Your solution has now been added tooyour workspace.</span></span> <span data-ttu-id="9641c-259">Volver atrás tooyour panel de portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9641c-259">Go back tooyour Azure portal Dashboard.</span></span>

    ![Ver todos](./media/cdn-diagnostics-log/22_Dashboard.png)

    <span data-ttu-id="9641c-261">Haga clic en el área de trabajo de análisis de registros de hello creó el área de trabajo de toogo tooyour.</span><span class="sxs-lookup"><span data-stu-id="9641c-261">Click hello Log Analytics workspace you created toogo tooyour workspace.</span></span> 

11. <span data-ttu-id="9641c-262">Haga clic en hello **Portal de OMS** icono toosee la nueva solución de portal de OMS Hola.</span><span class="sxs-lookup"><span data-stu-id="9641c-262">Click hello **OMS Portal** tile toosee your new solution in hello OMS portal.</span></span>

    ![Ver todos](./media/cdn-diagnostics-log/23_workspace.png)

12. <span data-ttu-id="9641c-264">El portal OMS debe parecerse Hola después de pantalla:</span><span class="sxs-lookup"><span data-stu-id="9641c-264">Your OMS portal should now look like hello following screen:</span></span>

    ![Ver todos](./media/cdn-diagnostics-log/24_OMS-solution.png)

    <span data-ttu-id="9641c-266">Haga clic en uno de hello iconos toosee varias vistas en los datos.</span><span class="sxs-lookup"><span data-stu-id="9641c-266">Click one of hello tiles toosee several views into your data.</span></span>

    ![Ver todos](./media/cdn-diagnostics-log/25_Interior-view.png)

    <span data-ttu-id="9641c-268">Puede desplazarse a la izquierda o derecha toosee más iconos que representan vistas individuales en datos Hola.</span><span class="sxs-lookup"><span data-stu-id="9641c-268">You can scroll left or right toosee further tiles representing individual views into hello data.</span></span> 

    <span data-ttu-id="9641c-269">Haga clic en uno de los iconos de hello ofrece más detalles sobre los datos.</span><span class="sxs-lookup"><span data-stu-id="9641c-269">Clicking one of hello tiles gives you more details about your data.</span></span>

     ![Ver todos](./media/cdn-diagnostics-log/26_Further-detail.png)

### <a name="offers-and-pricing-tiers"></a><span data-ttu-id="9641c-271">Ofertas y planes de tarifa</span><span class="sxs-lookup"><span data-stu-id="9641c-271">Offers and pricing tiers</span></span>

<span data-ttu-id="9641c-272">Puede ver ofertas y planes de tarifa de las soluciones de administración de OMS [aquí](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).</span><span class="sxs-lookup"><span data-stu-id="9641c-272">You can see offers and pricing tiers for OMS management solutions [here](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).</span></span>

### <a name="customizing-views"></a><span data-ttu-id="9641c-273">Personalización de las vistas</span><span class="sxs-lookup"><span data-stu-id="9641c-273">Customizing views</span></span>

<span data-ttu-id="9641c-274">Puede personalizar vista hello en los datos mediante el uso de hello **Diseñador de vistas**.</span><span class="sxs-lookup"><span data-stu-id="9641c-274">You can customize hello view into your data by using hello **View Designer**.</span></span> <span data-ttu-id="9641c-275">Vaya tooyour área de trabajo OMS y comienza a diseñar haciendo clic en hello **Diseñador de vistas** icono.</span><span class="sxs-lookup"><span data-stu-id="9641c-275">Go tooyour OMS workspace and begin designing by clicking hello **View Designer** tile.</span></span>

![Ver diseñador](./media/cdn-diagnostics-log/27_Designer.png)

<span data-ttu-id="9641c-277">Puede arrastra y coloca tipos de gráficos desde la izquierda de Hola y rellene Hola detalles de datos que desee tooanalyze en hello izquierda.</span><span class="sxs-lookup"><span data-stu-id="9641c-277">You can drag and drop types of charts from hello left and fill in hello data details you want tooanalyze on hello left.</span></span>

![Ver diseñador](./media/cdn-diagnostics-log/28_Designer.png)

    
## <a name="log-data-delays"></a><span data-ttu-id="9641c-279">Retrasos en el registro de datos</span><span class="sxs-lookup"><span data-stu-id="9641c-279">Log data delays</span></span>

<span data-ttu-id="9641c-280">Retrasos en el registro de datos de Verizon</span><span class="sxs-lookup"><span data-stu-id="9641c-280">Verizon log data delays</span></span> | <span data-ttu-id="9641c-281">Retrasos en el registro de datos de Akamai</span><span class="sxs-lookup"><span data-stu-id="9641c-281">Akamai log data delays</span></span>
--- | ---
<span data-ttu-id="9641c-282">Datos de registro de Verizon se retrasan de 1 hora y ocupan too2 horas toostart que aparecen después de la finalización de la propagación de punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="9641c-282">Verizon log data is 1 hour delayed, and take up too2 hours toostart appearing after endpoint propagation completion.</span></span> | <span data-ttu-id="9641c-283">Datos de registro de Akamai son de 24 horas retrasados y ocupa too2 horas toostart que aparece si se ha creado hace más de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="9641c-283">Akamai log data is 24 hours delayed, and takes up too2 hours toostart appearing if it was created more than 24 hours ago.</span></span> <span data-ttu-id="9641c-284">Si se ha creado recientemente, pueden tardar horas too25 Hola registros toostart que aparecen.</span><span class="sxs-lookup"><span data-stu-id="9641c-284">If it was recently created, it can take up too25 hours for hello logs toostart appearing.</span></span>

## <a name="diagnostic-log-types-for-cdn-core-analytics"></a><span data-ttu-id="9641c-285">Tipos de registro de diagnósticos para el Análisis Básico de la red CDN</span><span class="sxs-lookup"><span data-stu-id="9641c-285">Diagnostic log types for CDN Core Analytics</span></span>

<span data-ttu-id="9641c-286">Ofrecemos actualmente solo registros de análisis de núcleo, que contienen las métricas que muestra estadísticas de respuesta HTTP y salida tal como se muestra de Hola POP CDN/bordes.</span><span class="sxs-lookup"><span data-stu-id="9641c-286">We currently offer only Core Analytics logs, which contain metrics showing HTTP response statistics and egress statistics as seen from hello CDN POPs/edges.</span></span>

### <a name="core-analytics-metrics-details"></a><span data-ttu-id="9641c-287">Detalles de las métricas de análisis básico</span><span class="sxs-lookup"><span data-stu-id="9641c-287">Core Analytics Metrics Details</span></span>
<span data-ttu-id="9641c-288">Hello en la tabla siguiente muestra una lista de métricas disponibles en hello que registros de análisis de núcleo.</span><span class="sxs-lookup"><span data-stu-id="9641c-288">hello following table shows a list of metrics available in hello Core Analytics logs.</span></span> <span data-ttu-id="9641c-289">No todas las métricas están disponibles en todos los proveedores, si bien tales diferencias son mínimas.</span><span class="sxs-lookup"><span data-stu-id="9641c-289">Not all metrics are available from all providers, although such differences are minimal.</span></span> <span data-ttu-id="9641c-290">Hello en la tabla siguiente también se muestra si hay una métrica determinada de un proveedor.</span><span class="sxs-lookup"><span data-stu-id="9641c-290">hello following table also shows if a given metric is available from a provider.</span></span> <span data-ttu-id="9641c-291">Tenga en cuenta que las métricas de hello están disponibles para únicamente los extremos de red CDN que tienen el tráfico.</span><span class="sxs-lookup"><span data-stu-id="9641c-291">Please note that hello metrics are available for only those CDN endpoints that have traffic on them.</span></span>


|<span data-ttu-id="9641c-292">Métrica</span><span class="sxs-lookup"><span data-stu-id="9641c-292">Metric</span></span>                     | <span data-ttu-id="9641c-293">Descripción</span><span class="sxs-lookup"><span data-stu-id="9641c-293">Description</span></span>   | <span data-ttu-id="9641c-294">Verizon</span><span class="sxs-lookup"><span data-stu-id="9641c-294">Verizon</span></span>  | <span data-ttu-id="9641c-295">Akamai</span><span class="sxs-lookup"><span data-stu-id="9641c-295">Akamai</span></span> 
|---------------------------|---------------|---|---|
| <span data-ttu-id="9641c-296">RequestCountTotal</span><span class="sxs-lookup"><span data-stu-id="9641c-296">RequestCountTotal</span></span>         |<span data-ttu-id="9641c-297">Número total de solicitudes durante este periodo</span><span class="sxs-lookup"><span data-stu-id="9641c-297">Total number of request hits during this period</span></span>| <span data-ttu-id="9641c-298">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-298">Yes</span></span>  |<span data-ttu-id="9641c-299">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-299">Yes</span></span>   |
| <span data-ttu-id="9641c-300">RequestCountHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="9641c-300">RequestCountHttpStatus2xx</span></span> |<span data-ttu-id="9641c-301">Recuento de todas las solicitudes que dieron lugar a un código HTTP 2xx (por ejemplo, 200, 202)</span><span class="sxs-lookup"><span data-stu-id="9641c-301">Count of all requests that resulted in a 2xx HTTP code (e.g. 200, 202)</span></span>              | <span data-ttu-id="9641c-302">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-302">Yes</span></span>  |<span data-ttu-id="9641c-303">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-303">Yes</span></span>   |
| <span data-ttu-id="9641c-304">RequestCountHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="9641c-304">RequestCountHttpStatus3xx</span></span> | <span data-ttu-id="9641c-305">Recuento de todas las solicitudes que dieron lugar a un código HTTP 3xx (por ejemplo, 300, 302)</span><span class="sxs-lookup"><span data-stu-id="9641c-305">Count of all requests that resulted in a 3xx HTTP code (e.g. 300, 302)</span></span>              | <span data-ttu-id="9641c-306">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-306">Yes</span></span>  |<span data-ttu-id="9641c-307">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-307">Yes</span></span>   |
| <span data-ttu-id="9641c-308">RequestCountHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="9641c-308">RequestCountHttpStatus4xx</span></span> |<span data-ttu-id="9641c-309">Recuento de todas las solicitudes que dieron lugar a un código HTTP 4xx (por ejemplo, 400, 404)</span><span class="sxs-lookup"><span data-stu-id="9641c-309">Count of all requests that resulted in a 4xx HTTP code (e.g. 400, 404)</span></span>               | <span data-ttu-id="9641c-310">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-310">Yes</span></span>   |<span data-ttu-id="9641c-311">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-311">Yes</span></span>   |
| <span data-ttu-id="9641c-312">RequestCountHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="9641c-312">RequestCountHttpStatus5xx</span></span> | <span data-ttu-id="9641c-313">Recuento de todas las solicitudes que dieron lugar a un código HTTP 5xx (por ejemplo, 500, 504)</span><span class="sxs-lookup"><span data-stu-id="9641c-313">Count of all requests that resulted in a 5xx HTTP code (e.g. 500, 504)</span></span>              | <span data-ttu-id="9641c-314">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-314">Yes</span></span>  |<span data-ttu-id="9641c-315">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-315">Yes</span></span>   |
| <span data-ttu-id="9641c-316">RequestCountHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="9641c-316">RequestCountHttpStatusOthers</span></span> |  <span data-ttu-id="9641c-317">Recuento de todos los demás códigos HTTP (fuera del intervalo 2xx-5xx)</span><span class="sxs-lookup"><span data-stu-id="9641c-317">Count of all other HTTP codes (outside of 2xx-5xx)</span></span> | <span data-ttu-id="9641c-318">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-318">Yes</span></span>  |<span data-ttu-id="9641c-319">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-319">Yes</span></span>   |
| <span data-ttu-id="9641c-320">RequestCountHttpStatus200</span><span class="sxs-lookup"><span data-stu-id="9641c-320">RequestCountHttpStatus200</span></span> | <span data-ttu-id="9641c-321">Recuento de todas las solicitudes que dieron lugar a una respuesta de código HTTP 200</span><span class="sxs-lookup"><span data-stu-id="9641c-321">Count of all requests that resulted in a 200 HTTP code response</span></span>              |<span data-ttu-id="9641c-322">No</span><span class="sxs-lookup"><span data-stu-id="9641c-322">No</span></span>   |<span data-ttu-id="9641c-323">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-323">Yes</span></span>   |
| <span data-ttu-id="9641c-324">RequestCountHttpStatus206</span><span class="sxs-lookup"><span data-stu-id="9641c-324">RequestCountHttpStatus206</span></span> | <span data-ttu-id="9641c-325">Recuento de todas las solicitudes que dieron lugar a una respuesta de código HTTP 206</span><span class="sxs-lookup"><span data-stu-id="9641c-325">Count of all requests that resulted in a 206 HTTP code response</span></span>              |<span data-ttu-id="9641c-326">No</span><span class="sxs-lookup"><span data-stu-id="9641c-326">No</span></span>   |<span data-ttu-id="9641c-327">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-327">Yes</span></span>   |
| <span data-ttu-id="9641c-328">RequestCountHttpStatus302</span><span class="sxs-lookup"><span data-stu-id="9641c-328">RequestCountHttpStatus302</span></span> | <span data-ttu-id="9641c-329">Recuento de todas las solicitudes que dieron lugar a una respuesta de código HTTP 302</span><span class="sxs-lookup"><span data-stu-id="9641c-329">Count of all requests that resulted in a 302 HTTP code response</span></span>              |<span data-ttu-id="9641c-330">No</span><span class="sxs-lookup"><span data-stu-id="9641c-330">No</span></span>   |<span data-ttu-id="9641c-331">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-331">Yes</span></span>   |
| <span data-ttu-id="9641c-332">RequestCountHttpStatus304</span><span class="sxs-lookup"><span data-stu-id="9641c-332">RequestCountHttpStatus304</span></span> |  <span data-ttu-id="9641c-333">Recuento de todas las solicitudes que dieron lugar a una respuesta de código HTTP 304</span><span class="sxs-lookup"><span data-stu-id="9641c-333">Count of all requests that resulted in a 304 HTTP code response</span></span>             |<span data-ttu-id="9641c-334">No</span><span class="sxs-lookup"><span data-stu-id="9641c-334">No</span></span>   |<span data-ttu-id="9641c-335">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-335">Yes</span></span>   |
| <span data-ttu-id="9641c-336">RequestCountHttpStatus404</span><span class="sxs-lookup"><span data-stu-id="9641c-336">RequestCountHttpStatus404</span></span> | <span data-ttu-id="9641c-337">Recuento de todas las solicitudes que dieron lugar a una respuesta de código HTTP 404</span><span class="sxs-lookup"><span data-stu-id="9641c-337">Count of all requests that resulted in a 404 HTTP code response</span></span>              |<span data-ttu-id="9641c-338">No</span><span class="sxs-lookup"><span data-stu-id="9641c-338">No</span></span>   |<span data-ttu-id="9641c-339">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-339">Yes</span></span>   |
| <span data-ttu-id="9641c-340">RequestCountCacheHit</span><span class="sxs-lookup"><span data-stu-id="9641c-340">RequestCountCacheHit</span></span> |<span data-ttu-id="9641c-341">Recuento de todas las solicitudes que dieron lugar a un acierto de caché.</span><span class="sxs-lookup"><span data-stu-id="9641c-341">Count of all requests that resulted in a Cache Hit.</span></span> <span data-ttu-id="9641c-342">Esto significa que se realizó el servicio activo Hola directamente desde Hola POP toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="9641c-342">This means hello asset was served directly from hello POP toohello Client.</span></span>               | <span data-ttu-id="9641c-343">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-343">Yes</span></span>  |<span data-ttu-id="9641c-344">No</span><span class="sxs-lookup"><span data-stu-id="9641c-344">No</span></span>   |
| <span data-ttu-id="9641c-345">RequestCountCacheMiss</span><span class="sxs-lookup"><span data-stu-id="9641c-345">RequestCountCacheMiss</span></span> | <span data-ttu-id="9641c-346">Recuento de todas las solicitudes que dieron lugar a un error de caché.</span><span class="sxs-lookup"><span data-stu-id="9641c-346">Count of all requests that resulted in a Cache Miss.</span></span> <span data-ttu-id="9641c-347">Esto significa Hola activo no se encontró en el cliente de toohello más cercano de hello POP y, por tanto, se recuperó de hello origen.</span><span class="sxs-lookup"><span data-stu-id="9641c-347">This means hello asset was not found on hello POP closest toohello client, and therefore was retrieved from hello Origin.</span></span>              |<span data-ttu-id="9641c-348">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-348">Yes</span></span>   | <span data-ttu-id="9641c-349">No</span><span class="sxs-lookup"><span data-stu-id="9641c-349">No</span></span>  |
| <span data-ttu-id="9641c-350">RequestCountCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="9641c-350">RequestCountCacheNoCache</span></span> | <span data-ttu-id="9641c-351">Recuento de todas las solicitudes activo tooan que se evita que se almacenen en caché debido tooa configuración de usuario en el borde de Hola.</span><span class="sxs-lookup"><span data-stu-id="9641c-351">Count of all requests tooan asset that are prevented from being cached due tooa user configuration on hello edge.</span></span>              |<span data-ttu-id="9641c-352">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-352">Yes</span></span>   | <span data-ttu-id="9641c-353">No</span><span class="sxs-lookup"><span data-stu-id="9641c-353">No</span></span>  |
| <span data-ttu-id="9641c-354">RequestCountCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="9641c-354">RequestCountCacheUncacheable</span></span> | <span data-ttu-id="9641c-355">Recuento de todas las solicitudes tooassets que se impide que se almacena en memoria caché Cache-Control del recurso de hello y expira encabezados, que indican que no se debe guardar en un POP o cliente hello HTTP</span><span class="sxs-lookup"><span data-stu-id="9641c-355">Count of all requests tooassets that are prevented from being cached by hello asset's Cache-Control and Expires headers, which indicate that it should not be cached on a POP or by hello HTTP client</span></span>                |<span data-ttu-id="9641c-356">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-356">Yes</span></span>   |<span data-ttu-id="9641c-357">No</span><span class="sxs-lookup"><span data-stu-id="9641c-357">No</span></span>   |
| <span data-ttu-id="9641c-358">RequestCountCacheOthers</span><span class="sxs-lookup"><span data-stu-id="9641c-358">RequestCountCacheOthers</span></span> | <span data-ttu-id="9641c-359">Recuento de todas las solicitudes con un estado de caché no cubierto por lo anterior.</span><span class="sxs-lookup"><span data-stu-id="9641c-359">Count of all requests with cache status not covered by above.</span></span>              |<span data-ttu-id="9641c-360">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-360">Yes</span></span>   | <span data-ttu-id="9641c-361">No</span><span class="sxs-lookup"><span data-stu-id="9641c-361">No</span></span>  |
| <span data-ttu-id="9641c-362">EgressTotal</span><span class="sxs-lookup"><span data-stu-id="9641c-362">EgressTotal</span></span> | <span data-ttu-id="9641c-363">Transferencia de datos salientes en GB</span><span class="sxs-lookup"><span data-stu-id="9641c-363">Outbound data transfer in GB</span></span>              |<span data-ttu-id="9641c-364">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-364">Yes</span></span>   |<span data-ttu-id="9641c-365">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-365">Yes</span></span>   |
| <span data-ttu-id="9641c-366">EgressHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="9641c-366">EgressHttpStatus2xx</span></span> | <span data-ttu-id="9641c-367">Transferencia de datos salientes* para respuestas con códigos de estado HTTP 2xx en GB</span><span class="sxs-lookup"><span data-stu-id="9641c-367">Outbound data transfer* for responses with 2xx HTTP status codes in GB</span></span>            |<span data-ttu-id="9641c-368">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-368">Yes</span></span>   |<span data-ttu-id="9641c-369">No</span><span class="sxs-lookup"><span data-stu-id="9641c-369">No</span></span>   |
| <span data-ttu-id="9641c-370">EgressHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="9641c-370">EgressHttpStatus3xx</span></span> | <span data-ttu-id="9641c-371">Transferencia de datos salientes para respuestas con códigos de estado HTTP 3xx en GB</span><span class="sxs-lookup"><span data-stu-id="9641c-371">Outbound data transfer for responses with 3xx HTTP status codes in GB</span></span>              |<span data-ttu-id="9641c-372">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-372">Yes</span></span>   |<span data-ttu-id="9641c-373">No</span><span class="sxs-lookup"><span data-stu-id="9641c-373">No</span></span>   |
| <span data-ttu-id="9641c-374">EgressHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="9641c-374">EgressHttpStatus4xx</span></span> | <span data-ttu-id="9641c-375">Transferencia de datos de salida para respuestas con códigos de estado HTTP 4xx en GB</span><span class="sxs-lookup"><span data-stu-id="9641c-375">Outbound data transfer for responses with 4xx HTTP status codes in GB</span></span>               |<span data-ttu-id="9641c-376">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-376">Yes</span></span>   | <span data-ttu-id="9641c-377">No</span><span class="sxs-lookup"><span data-stu-id="9641c-377">No</span></span>  |
| <span data-ttu-id="9641c-378">EgressHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="9641c-378">EgressHttpStatus5xx</span></span> | <span data-ttu-id="9641c-379">Transferencia de datos de salida para respuestas con códigos de estado HTTP 5xx en GB</span><span class="sxs-lookup"><span data-stu-id="9641c-379">Outbound data transfer for responses with 5xx HTTP status codes in GB</span></span>               |<span data-ttu-id="9641c-380">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-380">Yes</span></span>   |  <span data-ttu-id="9641c-381">No</span><span class="sxs-lookup"><span data-stu-id="9641c-381">No</span></span> |
| <span data-ttu-id="9641c-382">EgressHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="9641c-382">EgressHttpStatusOthers</span></span> | <span data-ttu-id="9641c-383">Transferencia de datos de salida para respuestas con otros códigos de estado HTTP en GB</span><span class="sxs-lookup"><span data-stu-id="9641c-383">Outbound data transfer for responses with other HTTP status codes in GB</span></span>                |<span data-ttu-id="9641c-384">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-384">Yes</span></span>   |<span data-ttu-id="9641c-385">No</span><span class="sxs-lookup"><span data-stu-id="9641c-385">No</span></span>   |
| <span data-ttu-id="9641c-386">EgressCacheHit</span><span class="sxs-lookup"><span data-stu-id="9641c-386">EgressCacheHit</span></span> |  <span data-ttu-id="9641c-387">Transferencia de datos de salida para las respuestas que se enviaron directamente desde la caché de la red CDN Hola en hello POP de CDN/bordes</span><span class="sxs-lookup"><span data-stu-id="9641c-387">Outbound data transfer for responses that were delivered directly from hello CDN cache on hello CDN POPs/Edges</span></span>  |<span data-ttu-id="9641c-388">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-388">Yes</span></span>   |  <span data-ttu-id="9641c-389">No</span><span class="sxs-lookup"><span data-stu-id="9641c-389">No</span></span> |
| <span data-ttu-id="9641c-390">EgressCacheMiss</span><span class="sxs-lookup"><span data-stu-id="9641c-390">EgressCacheMiss</span></span> | <span data-ttu-id="9641c-391">Transferencia de datos de salida para las respuestas que no se encuentra en hello más próximo servidor POP y recuperar desde el servidor de origen de Hola</span><span class="sxs-lookup"><span data-stu-id="9641c-391">Outbound data transfer for responses that were not found on hello nearest POP server, and retrieved from hello origin server</span></span>              |<span data-ttu-id="9641c-392">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-392">Yes</span></span>   |  <span data-ttu-id="9641c-393">No</span><span class="sxs-lookup"><span data-stu-id="9641c-393">No</span></span> |
| <span data-ttu-id="9641c-394">EgressCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="9641c-394">EgressCacheNoCache</span></span> | <span data-ttu-id="9641c-395">Transferencia de datos de salida para los activos que se evita que se almacenen en caché debido tooa configuración de usuario en el borde de Hola.</span><span class="sxs-lookup"><span data-stu-id="9641c-395">Outbound data transfer for assets that are prevented from being cached due tooa user configuration on hello edge.</span></span>                |<span data-ttu-id="9641c-396">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-396">Yes</span></span>   |<span data-ttu-id="9641c-397">No</span><span class="sxs-lookup"><span data-stu-id="9641c-397">No</span></span>   |
| <span data-ttu-id="9641c-398">EgressCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="9641c-398">EgressCacheUncacheable</span></span> | <span data-ttu-id="9641c-399">Transferencia de datos de salida para los activos que se impidieron que se almacena en memoria caché del recurso de hello Cache-Control o Expires encabezados, que indican que no se debe guardar en un POP o cliente hello HTTP</span><span class="sxs-lookup"><span data-stu-id="9641c-399">Outbound data transfer for assets that are prevented from being cached by hello asset's Cache-Control and/or Expires headers, which indicate that it should not be cached on a POP or by hello HTTP client</span></span>                    |<span data-ttu-id="9641c-400">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-400">Yes</span></span>   | <span data-ttu-id="9641c-401">No</span><span class="sxs-lookup"><span data-stu-id="9641c-401">No</span></span>  |
| <span data-ttu-id="9641c-402">EgressCacheOthers</span><span class="sxs-lookup"><span data-stu-id="9641c-402">EgressCacheOthers</span></span> |  <span data-ttu-id="9641c-403">Transferencias de datos de salida para otros escenarios de caché.</span><span class="sxs-lookup"><span data-stu-id="9641c-403">Outbound data transfers for other cache scenarios.</span></span>             |<span data-ttu-id="9641c-404">Sí</span><span class="sxs-lookup"><span data-stu-id="9641c-404">Yes</span></span>   | <span data-ttu-id="9641c-405">No</span><span class="sxs-lookup"><span data-stu-id="9641c-405">No</span></span>  |

<span data-ttu-id="9641c-406">* Transferencia de datos saliente hace referencia tootraffic entregado de cliente de toohello de servidores de POP de CDN.</span><span class="sxs-lookup"><span data-stu-id="9641c-406">*Outbound data transfer refers tootraffic delivered from CDN POP servers toohello client.</span></span>


### <a name="schema-of-hello-core-analytics-logs"></a><span data-ttu-id="9641c-407">Esquema de hello registros de análisis de núcleo</span><span class="sxs-lookup"><span data-stu-id="9641c-407">Schema of hello Core Analytics Logs</span></span> 

<span data-ttu-id="9641c-408">Todos los registros se almacenan en formato JSON y cada entrada tiene campos de cadena siguientes Hola siguiente esquema:</span><span class="sxs-lookup"><span data-stu-id="9641c-408">All logs are stored in JSON format and each entry has string fields following hello below schema:</span></span>

```json
    "records": [
        {
            "time": "2017-04-27T01:00:00",
            "resourceId": "<ARM Resource Id of hello CDN Endpoint>",
            "operationName": "Microsoft.Cdn/profiles/endpoints/contentDelivery",
            "category": "CoreAnalytics",
            "properties": {
                "DomainName": "<Name of hello domain for which hello statistics is reported>",
                "RequestCountTotal": integer value,
                "RequestCountHttpStatus2xx": integer value,
                "RequestCountHttpStatus3xx": integer value,
                "RequestCountHttpStatus4xx": integer value,
                "RequestCountHttpStatus5xx": integer value,
                "RequestCountHttpStatusOthers": integer value,
                "RequestCountHttpStatus200": integer value,
                "RequestCountHttpStatus206": integer value,
                "RequestCountHttpStatus302": integer value,
                "RequestCountHttpStatus304": integer value,
                "RequestCountHttpStatus404": integer value,
                "RequestCountCacheHit": integer value,
                "RequestCountCacheMiss": integer value,
                "RequestCountCacheNoCache": integer value,
                "RequestCountCacheUncacheable": integer value,
                "RequestCountCacheOthers": integer value,
                "EgressTotal": double value,
                "EgressHttpStatus2xx": double value,
                "EgressHttpStatus3xx": double value,
                "EgressHttpStatus4xx": double value,
                "EgressHttpStatus5xx": double value,
                "EgressHttpStatusOthers": double value,
                "EgressCacheHit": double value,
                "EgressCacheMiss": double value,
                "EgressCacheNoCache": double value,
                "EgressCacheUncacheable": double value,
                "EgressCacheOthers": double value,
            }
        }

    ]
}
```

<span data-ttu-id="9641c-409">Donde hello 'tiempo' representa el tiempo de inicio de Hola de límite de hora de hello para el que se notifican las estadísticas de Hola.</span><span class="sxs-lookup"><span data-stu-id="9641c-409">Where hello ‘time’ represents hello start time of hello hour boundary for which hello statistics is reported.</span></span> <span data-ttu-id="9641c-410">Cuando un proveedor de CDN no admite una métrica, en lugar de un valor doble o entero, habrá un valor nulo.</span><span class="sxs-lookup"><span data-stu-id="9641c-410">When a metric is not supported by a CDN provider, instead of a double or integer value, there will be a null value.</span></span> <span data-ttu-id="9641c-411">Este valor nulo indica la ausencia de Hola de una métrica, y esto es diferente de un valor de 0.</span><span class="sxs-lookup"><span data-stu-id="9641c-411">This null value indicates hello absence of a metric, and this is different from a 0 value.</span></span> <span data-ttu-id="9641c-412">Tenga en cuenta que habrá un conjunto de estas métricas por dominio configurado en el punto de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="9641c-412">Also note that there will be one set of these metrics per domain configured on hello endpoint.</span></span>

<span data-ttu-id="9641c-413">Propiedades de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9641c-413">Example properties below:</span></span>

```json
{
     "DomainName": "manlingakamaitest2.azureedge.net",
     "RequestCountTotal": 480,
     "RequestCountHttpStatus2xx": 480,
     "RequestCountHttpStatus3xx": 0,
     "RequestCountHttpStatus4xx": 0,
     "RequestCountHttpStatus5xx": 0,
     "RequestCountHttpStatusOthers": 0,
     "RequestCountHttpStatus200": 480,
     "RequestCountHttpStatus206": 0,
     "RequestCountHttpStatus302": 0,
     "RequestCountHttpStatus304": 0,
     "RequestCountHttpStatus404": 0,
     "RequestCountCacheHit": null,
     "RequestCountCacheMiss": null,
     "RequestCountCacheNoCache": null,
     "RequestCountCacheUncacheable": null,
     "RequestCountCacheOthers": null,
     "EgressTotal": 0.09,
     "EgressHttpStatus2xx": null,
     "EgressHttpStatus3xx": null,
     "EgressHttpStatus4xx": null,
     "EgressHttpStatus5xx": null,
     "EgressHttpStatusOthers": null,
     "EgressCacheHit": null,
     "EgressCacheMiss": null,
     "EgressCacheNoCache": null,
     "EgressCacheUncacheable": null,
     "EgressCacheOthers": null
}

```

## <a name="additional-resources"></a><span data-ttu-id="9641c-414">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="9641c-414">Additional resources</span></span>

* [<span data-ttu-id="9641c-415">Registros de diagnóstico de Azure</span><span class="sxs-lookup"><span data-stu-id="9641c-415">Azure Diagnostic logs</span></span>](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)
* [<span data-ttu-id="9641c-416">Análisis básico mediante el portal complementario de la red CDN</span><span class="sxs-lookup"><span data-stu-id="9641c-416">Core analytics via Azure CDN supplemental portal</span></span>](https://docs.microsoft.com/azure/cdn/cdn-analyze-usage-patterns)
* [<span data-ttu-id="9641c-417">Log Analytics de OMS de Azure</span><span class="sxs-lookup"><span data-stu-id="9641c-417">Azure OMS Log Analytics</span></span>](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-overview)
* [<span data-ttu-id="9641c-418">API de REST de Azure Log Analytics</span><span class="sxs-lookup"><span data-stu-id="9641c-418">Azure Log Analytics REST API</span></span>](https://docs.microsoft.com/en-us/rest/api/loganalytics)







