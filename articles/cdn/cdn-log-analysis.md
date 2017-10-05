---
title: "Análisis de registros para la red CDN de Azure | Microsoft Docs"
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
ms.openlocfilehash: 03ff74ae4e40d3f2279caaf4f73e9b4aac6a2ebb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="diagnostics-logs-for-azure-cdn"></a><span data-ttu-id="ffa66-103">Registros de diagnóstico de red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="ffa66-103">Diagnostics Logs for Azure CDN</span></span>

<span data-ttu-id="ffa66-104">Después de habilitar CDN para la aplicación, es probable que quiere supervisar el uso de la red CDN, comprobar el estado de su entrega y solucionar posibles problemas.</span><span class="sxs-lookup"><span data-stu-id="ffa66-104">After enabling CDN for your application, you will likely want to monitor the CDN usage, check the health of your delivery, and troubleshoot potential issues.</span></span> <span data-ttu-id="ffa66-105">La red CDN de Azure proporciona estas funcionalidades con [Análisis Básico de la red CDN](cdn-analyze-usage-patterns.md) y [Registros de diagnóstico](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)</span><span class="sxs-lookup"><span data-stu-id="ffa66-105">Azure CDN provides these capabilities with [CDN Core Analytics](cdn-analyze-usage-patterns.md) and [Diagnostic Logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)</span></span>

## <a name="cdn-core-analytics"></a><span data-ttu-id="ffa66-106">Análisis Básico de la red CDN</span><span class="sxs-lookup"><span data-stu-id="ffa66-106">CDN Core Analytics</span></span>
<span data-ttu-id="ffa66-107">Como usuario actual de la red CDN de Azure con un perfil estándar o premium de Verizon, ya puede ver análisis básicos en el portal complementario accesible mediante la opción "Administrar" de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ffa66-107">As a current Azure CDN user with Verizon standard or premium profile, you are already able to view core analytics in the supplemental portal accessible via the "Manage" option from the Azure portal.</span></span> 

## <a name="azure-diagnostic-logs"></a><span data-ttu-id="ffa66-108">Registros de diagnóstico de Azure</span><span class="sxs-lookup"><span data-stu-id="ffa66-108">Azure Diagnostic Logs</span></span>

<span data-ttu-id="ffa66-109">Con esta nueva característica de Azure, ahora puede ver el análisis básico y guardarlo en uno o más destinos, entre los que se incluyen:</span><span class="sxs-lookup"><span data-stu-id="ffa66-109">Azure With this new feature, you can now view core analytics and save them into one or more destinations including:</span></span>

 - <span data-ttu-id="ffa66-110">Cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="ffa66-110">Azure Storage account</span></span>
 - <span data-ttu-id="ffa66-111">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="ffa66-111">Azure Event Hubs</span></span>
 - [<span data-ttu-id="ffa66-112">Repositorio de Log Analytics de OMS</span><span class="sxs-lookup"><span data-stu-id="ffa66-112">OMS Log Analytics repository</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started)
 
 <span data-ttu-id="ffa66-113">Esta característica está disponible para todos los puntos de conexión de red CDN que pertenecen a Verizon (estándar y premium) y perfiles de red CDN de Akamai (estándar).</span><span class="sxs-lookup"><span data-stu-id="ffa66-113">This feature is available for all CDN endpoints belonging to Verizon (Standard & Premium) and Akamai (Standard) CDN Profiles.</span></span>

<span data-ttu-id="ffa66-114">Los registros de diagnóstico le permiten exportar métricas básicas de uso desde su punto de conexión de la red CDN a diversos orígenes, de modo que pueda consumirlas de forma personalizada.</span><span class="sxs-lookup"><span data-stu-id="ffa66-114">Diagnostics logs allow you to export basic usage metrics from your CDN endpoint to a variety of sources so that you can consume them in a customized way.</span></span> <span data-ttu-id="ffa66-115">Por ejemplo, puede realizar los siguientes tipos de exportación de datos:</span><span class="sxs-lookup"><span data-stu-id="ffa66-115">For example, you can do the following types of data export:</span></span>

- <span data-ttu-id="ffa66-116">Exportar datos a Blob Storage, exportar a CSV y generar gráficos en Excel.</span><span class="sxs-lookup"><span data-stu-id="ffa66-116">Export data to blob storage, export to CSV, and generate graphs in excel.</span></span>
- <span data-ttu-id="ffa66-117">Exportar datos a Event Hubs y correlacionarlos con los datos de otros servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="ffa66-117">Export data to event hubs and correlate with data from other azure services.</span></span>
- <span data-ttu-id="ffa66-118">Exportar datos a Log Analytics y verlos en su propia área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="ffa66-118">Export data to log analytics and view data in your own OMS work space</span></span>

<span data-ttu-id="ffa66-119">La siguiente ilustración muestra una vista habitual de Análisis Básico de la red CDN en los datos.</span><span class="sxs-lookup"><span data-stu-id="ffa66-119">The following figure shows a typical CDN Core Analytics view into data.</span></span>

![Portal: Registros de diagnóstico](./media/cdn-diagnostics-log/01_OMS-workspace.png)

<span data-ttu-id="ffa66-121">*Figura 1: vista de Análisis Básico de la red CDN*</span><span class="sxs-lookup"><span data-stu-id="ffa66-121">*Figure 1 - CDN Core Analytics view*</span></span>

<span data-ttu-id="ffa66-122">El siguiente tutorial le lleva por el esquema de los datos de análisis básico, los pasos que intervienen en la habilitación de la característica y la entrega de dichos datos a diversos destinos y su consumo desde estos destinos.</span><span class="sxs-lookup"><span data-stu-id="ffa66-122">The following walkthrough goes through the schema of the core analytics data, steps involved in enabling the feature and delivering them to various destinations, and consuming from these destinations.</span></span>

## <a name="enable-logging-with-azure-portal"></a><span data-ttu-id="ffa66-123">Habilitación del registro con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ffa66-123">Enable logging with Azure portal</span></span>

> [!NOTE]
> <span data-ttu-id="ffa66-124">Los registros de diagnósticos están **desactivados** de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="ffa66-124">The diagnostics logs are turned **off** by default.</span></span> 

<span data-ttu-id="ffa66-125">Siga los pasos siguientes para habilitar el registro con Análisis Básico de la red CDN:</span><span class="sxs-lookup"><span data-stu-id="ffa66-125">Follow the steps below to enable logging with CDN Core Analytics:</span></span>

<span data-ttu-id="ffa66-126">Inicie sesión en [Azure Portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ffa66-126">Sign in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="ffa66-127">Si no se ha habilitado ya la red CDN para el flujo de trabajo, [habilítela](cdn-create-new-endpoint.md) antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="ffa66-127">If you don't already have CDN enabled for your workflow, [Enable Azure CDN](cdn-create-new-endpoint.md) before you continue.</span></span>

1. <span data-ttu-id="ffa66-128">En el portal, vaya a **Perfil de CDN**.</span><span class="sxs-lookup"><span data-stu-id="ffa66-128">In the portal, navigate to **CDN profile**.</span></span>
2. <span data-ttu-id="ffa66-129">Seleccione un perfil de CDN y luego seleccione el punto de conexión de CDN para el que desea habilitar **Registros de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="ffa66-129">Select a CDN profile, then select the CDN endpoint that you want to enable **Diagnostics Logs**.</span></span>

    ![Portal: Registros de diagnóstico](./media/cdn-diagnostics-log/02_Browse-to-Diagnostics-logs.png)

3. <span data-ttu-id="ffa66-131">Vaya a la hoja **Registros de diagnóstico** en la sección **Supervisión**, y cambie el estado a **Activado**.</span><span class="sxs-lookup"><span data-stu-id="ffa66-131">Go to **Diagnostics Logs** blade Under **Monitoring** section, then change the status to **On**.</span></span>

    ![Portal: Registros de diagnóstico](./media/cdn-diagnostics-log/03_Diagnostics-logs-options.png)

### <a name="enable-logging-with-azure-storage"></a><span data-ttu-id="ffa66-133">Habilitación del registro con Azure Storage</span><span class="sxs-lookup"><span data-stu-id="ffa66-133">Enable logging with Azure Storage</span></span>
    
<span data-ttu-id="ffa66-134">Para usar Azure Storage para almacenar los registros, seleccione **Archivar en una cuenta de almacenamiento**, seleccione los días de retención y haga clic en **Análisis básico** en **Registro**.</span><span class="sxs-lookup"><span data-stu-id="ffa66-134">To use Azure Storage to store the logs, select **Archive to a storage account**, select retention days, and click **CoreAnalytics** under **Log**.</span></span>

![Portal: Registros de diagnóstico](./media/cdn-diagnostics-log/04_Diagnostics-logs-storage.png)

<span data-ttu-id="ffa66-136">*Figura 2: registro con Azure Storage*</span><span class="sxs-lookup"><span data-stu-id="ffa66-136">*Figure 2 - Logging with Azure Storage*</span></span>

### <a name="logging-with-oms-log-analytics"></a><span data-ttu-id="ffa66-137">Registro con Log Analytics de OMS</span><span class="sxs-lookup"><span data-stu-id="ffa66-137">Logging with OMS Log Analytics</span></span>

<span data-ttu-id="ffa66-138">Para usar Log Analytics de OMS para almacenar los registros, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="ffa66-138">To use OMS Log Analytics to store the logs, follow these steps:</span></span>

1. <span data-ttu-id="ffa66-139">Desde la hoja **Registros de diagnóstico** en **Supervisión**, seleccione **Enviar a Log Analytics**</span><span class="sxs-lookup"><span data-stu-id="ffa66-139">From the **Diagnostics Logs** blade Under **Monitoring**, select **Send to Log Analytics** from</span></span> 

    ![Portal: Registros de diagnóstico](./media/cdn-diagnostics-log/05_Ready-to-Configure.png)    

2. <span data-ttu-id="ffa66-141">Para configurar el registro de Log Analytics, haga clic en Configurar.</span><span class="sxs-lookup"><span data-stu-id="ffa66-141">Configure the Log Analytics logging by clicking on Configure.</span></span> <span data-ttu-id="ffa66-142">Esto le lleva a un cuadro de diálogo donde puede seleccionar un área de trabajo anterior o crear una nueva.</span><span class="sxs-lookup"><span data-stu-id="ffa66-142">This takes you to a dialog where you can select a previous workspace or create a new one.</span></span>

    ![Portal: Registros de diagnóstico](./media/cdn-diagnostics-log/06_Choose-workspace.png)

3. <span data-ttu-id="ffa66-144">Haga clic en **Crear nueva área de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="ffa66-144">Click **Create New Workspace**.</span></span>

    ![Portal: Registros de diagnóstico](./media/cdn-diagnostics-log/07_Create-new.png)

4. <span data-ttu-id="ffa66-146">A continuación debe seleccionar un nuevo nombre de área de trabajo, una suscripción existente, un grupo de recursos (nuevo o existente), la ubicación y el plan de tarifa.</span><span class="sxs-lookup"><span data-stu-id="ffa66-146">Next you must select a new workspace name, existing subscription, resource group (new or existing), location, and pricing tier.</span></span> <span data-ttu-id="ffa66-147">Tiene la opción de fijar esta configuración al panel.</span><span class="sxs-lookup"><span data-stu-id="ffa66-147">You have the option of pinning this configuration to your dashboard.</span></span> <span data-ttu-id="ffa66-148">Haga clic en Aceptar para completar la configuración.</span><span class="sxs-lookup"><span data-stu-id="ffa66-148">Click OK to complete the configuration.</span></span>

    <span data-ttu-id="ffa66-149">A continuación debería ver el área de trabajo con los nombres del grupo de recursos y del área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="ffa66-149">Next you should see your workspace with your OMS Workspace and Resource group names.</span></span> <span data-ttu-id="ffa66-150">Los nombres deben ser únicos y solo se pueden usar letras, números y guiones.</span><span class="sxs-lookup"><span data-stu-id="ffa66-150">Names must be unique and can only use letters, numbers, and hyphens.</span></span> <span data-ttu-id="ffa66-151">No se permiten espacios ni caracteres de subrayado.</span><span class="sxs-lookup"><span data-stu-id="ffa66-151">Spaces and underscores are not allowed.</span></span> 

    ![Portal: Registros de diagnóstico](./media/cdn-diagnostics-log/08_Workspace-resource.png)

5. <span data-ttu-id="ffa66-153">A continuación, obtendrá un mensaje breve que indica que se ha creado el área de trabajo y se le devuelve a la pantalla de configuración de registro.</span><span class="sxs-lookup"><span data-stu-id="ffa66-153">You next get a short message saying that your workspace has been created and you are returned to your logging configuration screen.</span></span> <span data-ttu-id="ffa66-154">Puede confirmar el nombre del área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="ffa66-154">You can confirm the name of your Log Analytics workspace.</span></span>

    ![Portal: Registros de diagnóstico](./media/cdn-diagnostics-log/09_Return-to-logging.png)

    <span data-ttu-id="ffa66-156">Una vez haya realizado la configuración de Log Analytics, asegúrese de que también marca la casilla Análisis Básico para el registro de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="ffa66-156">Once you have set up the Log Analytics configuration, make sure you also check the CoreAnalytics box for CDN logging.</span></span>

6. <span data-ttu-id="ffa66-157">Si todo está correcto, haga clic en el botón **Guardar** situado en la parte superior del cuadro de diálogo de configuración.</span><span class="sxs-lookup"><span data-stu-id="ffa66-157">If everything is to your liking, click the **Save** button at the top of the configuration dialog.</span></span>

    ![Portal: Registros de diagnóstico](./media/cdn-diagnostics-log/10_Save-me.png)

    <span data-ttu-id="ffa66-159">El botón **Guardar** ya no se muestra activo y el botón ON/OFF ahora está en ON, pero azul en lugar de púrpura.</span><span class="sxs-lookup"><span data-stu-id="ffa66-159">The **Save** button is no longer active and that the ON/OFF button is now ON, but blue instead of purple.</span></span>

7. <span data-ttu-id="ffa66-160">Si desea ver la nueva área de trabajo de OMS, vaya al panel de Azure Portal y haga clic en el nombre del área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="ffa66-160">If you want to see your new OMS workspace, go to your Azure portal Dashboard, click the name of your Log Analytics workspace.</span></span> <span data-ttu-id="ffa66-161">A continuación, verá el área de trabajo (asegúrese de que el área de trabajo de OMS esta resaltado a la izquierda).</span><span class="sxs-lookup"><span data-stu-id="ffa66-161">Next you will see your workspace (make sure that OMS Workspace is highlighted on the left).</span></span> <span data-ttu-id="ffa66-162">Haga clic en el icono de Portal de OMS para ver el área de trabajo en el repositorio de OMS.</span><span class="sxs-lookup"><span data-stu-id="ffa66-162">Click on the OMS Portal tile to see your workspace in the OMS repository.</span></span> 

    ![Portal: Registros de diagnóstico](./media/cdn-diagnostics-log/11_OMS-dashboard.png) 

    <span data-ttu-id="ffa66-164">El repositorio de OMS ahora está listo para registrar los datos.</span><span class="sxs-lookup"><span data-stu-id="ffa66-164">Your OMS repository is now ready to log data.</span></span> <span data-ttu-id="ffa66-165">Para consumir estos datos, debe utilizar una [solución de OMS](#consuming-oms-log-analytics-data), descrito más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="ffa66-165">In order to consume that data, you must use an [OMS Solution](#consuming-oms-log-analytics-data), covered later in this article.</span></span>

<span data-ttu-id="ffa66-166">Para más información sobre los retardos en el registro de datos, vaya [aquí](#log-data-delays).</span><span class="sxs-lookup"><span data-stu-id="ffa66-166">For more information about log data delays, go [here](#log-data-delays).</span></span>

## <a name="enable-logging-with-powershell"></a><span data-ttu-id="ffa66-167">Habilitación del registro con PowerShell</span><span class="sxs-lookup"><span data-stu-id="ffa66-167">Enable logging with PowerShell</span></span>

<span data-ttu-id="ffa66-168">A continuación se muestra un ejemplo de cómo habilitar y obtener registros de diagnóstico mediante cmdlets de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ffa66-168">Below is an example on how to enable and get Diagnostic Logs via the Azure PowerShell Cmdlets.</span></span>

###<a name="enabling-diagnostic-logs-in-a-storage-account"></a><span data-ttu-id="ffa66-169">Habilitación de registros de diagnóstico en una cuenta de Storage</span><span class="sxs-lookup"><span data-stu-id="ffa66-169">Enabling Diagnostic Logs in a Storage Account</span></span>

<span data-ttu-id="ffa66-170">Inicio de sesión y selección de una suscripción:</span><span class="sxs-lookup"><span data-stu-id="ffa66-170">First log in and select a subscription:</span></span>

    Login-AzureRmAccount 

    Select-AzureSubscription -SubscriptionId 


<span data-ttu-id="ffa66-171">Para habilitar los registros de diagnóstico en una cuenta de Storage, use este comando:</span><span class="sxs-lookup"><span data-stu-id="ffa66-171">To Enable Diagnostic Logs in a Storage Account, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}" -StorageAccountId "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicStorage/storageAccounts/{storageAccountName}" -Enabled $true -Categories CoreAnalytics
```
<span data-ttu-id="ffa66-172">Para habilitar el Registro de diagnósticos en un área de trabajo de OMS, use este comando:</span><span class="sxs-lookup"><span data-stu-id="ffa66-172">To Enable Diagnostics Logs in an OMS workspace, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/`{subscriptionId}<subscriptionId>
    .<subscriptionName>" -WorkspaceId "/subscriptions/<workspaceId>.<workspaceName>" -Enabled $true -Categories CoreAnalytics 
```



## <a name="consuming-diagnostics-logs-from-azure-storage"></a><span data-ttu-id="ffa66-173">Consumo de registros de diagnósticos desde Azure Storage</span><span class="sxs-lookup"><span data-stu-id="ffa66-173">Consuming diagnostics logs from Azure Storage</span></span>
<span data-ttu-id="ffa66-174">En esta sección se describe el esquema del análisis básico de la red CDN, cómo se organiza dentro de una cuenta de Azure Storage y se proporciona código de ejemplo para descargar los registros en un archivo CSV.</span><span class="sxs-lookup"><span data-stu-id="ffa66-174">This section describes the schema of the CDN core analytics, how these are organized inside of an Azure Storage Account and provides sample code to download the logs in to a CSV file.</span></span>

### <a name="using-microsoft-azure-storage-explorer"></a><span data-ttu-id="ffa66-175">Uso del Explorador de Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="ffa66-175">Using Microsoft Azure Storage Explorer</span></span>
<span data-ttu-id="ffa66-176">Antes de poder acceder a los datos de análisis básico desde la cuenta de Azure Storage, primero necesita una herramienta para acceder a los contenidos de una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ffa66-176">Before you can access the core analytics data from the Azure Storage Account, you first need a tool to access the contents in a storage account.</span></span> <span data-ttu-id="ffa66-177">Aunque hay varias herramientas disponibles en el mercado, la única que recomendamos es el Explorador de Microsoft Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="ffa66-177">While there are several tools available in the market, the one that we recommend is the Microsoft Azure Storage Explorer.</span></span> <span data-ttu-id="ffa66-178">Puede descargar la herramienta desde [aquí](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="ffa66-178">You can download the tool from [here](http://storageexplorer.com/).</span></span> <span data-ttu-id="ffa66-179">Después de descargar e instalar el software, configúrelo para usar la misma cuenta de Azure Storage que configuró como destino para Registro de diagnósticos de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="ffa66-179">After downloading and installing the software, configure it to use the same Azure Storage Account that was configured as a destination to the CDN Diagnostics Logs.</span></span>

1.  <span data-ttu-id="ffa66-180">Abra el **Explorador de Microsoft Azure Storage**</span><span class="sxs-lookup"><span data-stu-id="ffa66-180">Open **Microsoft Azure Storage Explorer**</span></span>
2.  <span data-ttu-id="ffa66-181">Busque la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ffa66-181">Locate the storage account</span></span>
3.  <span data-ttu-id="ffa66-182">Vaya al nodo **"Contenedores de blob”** en esta cuenta de almacenamiento y expanda el nodo.</span><span class="sxs-lookup"><span data-stu-id="ffa66-182">Go to the **“Blob Containers”** node under this storage account and expand the node</span></span>
4.  <span data-ttu-id="ffa66-183">Seleccione el contenedor llamado **"insights-logs-coreanalytics"** y haga doble clic en él</span><span class="sxs-lookup"><span data-stu-id="ffa66-183">Select the container named **“insights-logs-coreanalytics”** and double-click it</span></span>
5.  <span data-ttu-id="ffa66-184">Los resultados se muestran en el panel derecho, comenzando por el primer nivel, que se parece a **"resourceId="**.</span><span class="sxs-lookup"><span data-stu-id="ffa66-184">Results show up on the right-hand pane starting with the first level, which looks like **“resourceId=”**.</span></span> <span data-ttu-id="ffa66-185">Siga haciendo clic hasta que vea el archivo **PT1H.json**.</span><span class="sxs-lookup"><span data-stu-id="ffa66-185">Continue clicking all the way until you see the file **PT1H.json**.</span></span> <span data-ttu-id="ffa66-186">Consulte la nota siguiente para ver una explicación de la ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="ffa66-186">See the following note for explanation of the path.</span></span>
6.  <span data-ttu-id="ffa66-187">Cada blob **PT1H.json** representa los registros de análisis durante una hora de un punto de conexión de red CDN concreto o de su dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="ffa66-187">Each blob **PT1H.json** represents the analytics logs for one hour for a specific CDN endpoint or its custom domain.</span></span>
7.  <span data-ttu-id="ffa66-188">El esquema del contenido de este archivo JSON se describe en la sección Esquema de los registros de análisis básico.</span><span class="sxs-lookup"><span data-stu-id="ffa66-188">The schema of the contents of this JSON file is described in the section Schema of the Core Analytics Logs</span></span>


> [!NOTE]
> <span data-ttu-id="ffa66-189">**Formato de ruta de acceso de blob**</span><span class="sxs-lookup"><span data-stu-id="ffa66-189">**Blob path format**</span></span>
> 
> <span data-ttu-id="ffa66-190">Los registros de análisis básico se generan cada hora.</span><span class="sxs-lookup"><span data-stu-id="ffa66-190">Core Analytics logs are generated every hour.</span></span> <span data-ttu-id="ffa66-191">Todos los datos de una hora se recopilan y almacenan dentro de un único blob de Azure como una carga JSON.</span><span class="sxs-lookup"><span data-stu-id="ffa66-191">All data for an hour are collected and stored inside a single Azure Blob as a JSON payload.</span></span> <span data-ttu-id="ffa66-192">La ruta de acceso a este blob de Azure aparece como si hubiera una estructura jerárquica.</span><span class="sxs-lookup"><span data-stu-id="ffa66-192">The path to this Azure Blob appears as if there is a hierarchical structure.</span></span> <span data-ttu-id="ffa66-193">Este se debe a que la herramienta Explorador de Storage interpreta "/" como un separador de directorio y muestra la jerarquía por motivos de comodidad.</span><span class="sxs-lookup"><span data-stu-id="ffa66-193">This is because the Storage explorer tool interprets '/' as a directory separator and shows the hierarchy for convenience.</span></span> <span data-ttu-id="ffa66-194">En realidad, la ruta de acceso completa solo representa el nombre del blob.</span><span class="sxs-lookup"><span data-stu-id="ffa66-194">Actually, the whole path just represents the blob name.</span></span> <span data-ttu-id="ffa66-195">Este nombre del blob sigue la convención de nomenclatura siguiente:</span><span class="sxs-lookup"><span data-stu-id="ffa66-195">This name of the blob follows the following naming convention</span></span>   
    
    resourceId=/SUBSCRIPTIONS/{Subscription Id}/RESOURCEGROUPS/{Resource Group Name}/PROVIDERS/MICROSOFT.CDN/PROFILES/{Profile Name}/ENDPOINTS/{Endpoint Name}/ y={Year}/m={Month}/d={Day}/h={Hour}/m={Minutes}/PT1H.json

<span data-ttu-id="ffa66-196">**Descripción de los campos:**</span><span class="sxs-lookup"><span data-stu-id="ffa66-196">**Description of fields:**</span></span>

|<span data-ttu-id="ffa66-197">value</span><span class="sxs-lookup"><span data-stu-id="ffa66-197">value</span></span>|<span data-ttu-id="ffa66-198">Descripción</span><span class="sxs-lookup"><span data-stu-id="ffa66-198">description</span></span>|
|-------|---------|
|<span data-ttu-id="ffa66-199">Id. de suscripción</span><span class="sxs-lookup"><span data-stu-id="ffa66-199">Subscription ID</span></span>    |<span data-ttu-id="ffa66-200">Identificador de la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="ffa66-200">ID of the Azure Subscription.</span></span> <span data-ttu-id="ffa66-201">Está en formato Guid.</span><span class="sxs-lookup"><span data-stu-id="ffa66-201">This is in the Guid format.</span></span>|
|<span data-ttu-id="ffa66-202">Recurso</span><span class="sxs-lookup"><span data-stu-id="ffa66-202">Resource</span></span> |<span data-ttu-id="ffa66-203">Nombre del grupo   Nombre del grupo de recursos al que pertenecen los recursos de red CDN.</span><span class="sxs-lookup"><span data-stu-id="ffa66-203">Group Name   Name of the resource group to which the CDN resources belong.</span></span>|
|<span data-ttu-id="ffa66-204">Nombre del perfil</span><span class="sxs-lookup"><span data-stu-id="ffa66-204">Profile Name</span></span> |<span data-ttu-id="ffa66-205">Nombre del perfil de CDN</span><span class="sxs-lookup"><span data-stu-id="ffa66-205">Name of the CDN Profile</span></span>|
|<span data-ttu-id="ffa66-206">Nombre del punto de conexión</span><span class="sxs-lookup"><span data-stu-id="ffa66-206">Endpoint Name</span></span> |<span data-ttu-id="ffa66-207">Nombre del punto de conexión de CDN</span><span class="sxs-lookup"><span data-stu-id="ffa66-207">Name of the CDN Endpoint</span></span>|
|<span data-ttu-id="ffa66-208">Year</span><span class="sxs-lookup"><span data-stu-id="ffa66-208">Year</span></span>|  <span data-ttu-id="ffa66-209">Representación del año en formato de cuatro dígitos, por ejemplo, 2017</span><span class="sxs-lookup"><span data-stu-id="ffa66-209">4-digit representation of the year for example, 2017</span></span>|
|<span data-ttu-id="ffa66-210">Mes</span><span class="sxs-lookup"><span data-stu-id="ffa66-210">Month</span></span>| <span data-ttu-id="ffa66-211">Representación del mes en formato de dos dígitos.</span><span class="sxs-lookup"><span data-stu-id="ffa66-211">2-digit representation of the month number.</span></span> <span data-ttu-id="ffa66-212">01=enero ... 12=diciembre</span><span class="sxs-lookup"><span data-stu-id="ffa66-212">01=January ... 12=December</span></span>|
|<span data-ttu-id="ffa66-213">Día</span><span class="sxs-lookup"><span data-stu-id="ffa66-213">Day</span></span>|   <span data-ttu-id="ffa66-214">Representación del día del mes en formato de dos dígitos.</span><span class="sxs-lookup"><span data-stu-id="ffa66-214">2 digit representation of the day of the month</span></span>|
|<span data-ttu-id="ffa66-215">PT1H.json</span><span class="sxs-lookup"><span data-stu-id="ffa66-215">PT1H.json</span></span>| <span data-ttu-id="ffa66-216">Archivo JSON real donde se almacenan los datos de análisis</span><span class="sxs-lookup"><span data-stu-id="ffa66-216">Actual JSON file where the analytics data is stored</span></span>|

### <a name="exporting-the-core-analytics-data-to-a-csv-file"></a><span data-ttu-id="ffa66-217">Exportación de los datos de análisis básico a un archivo CSV</span><span class="sxs-lookup"><span data-stu-id="ffa66-217">Exporting the Core Analytics Data to a CSV File</span></span>

<span data-ttu-id="ffa66-218">Para facilitar el acceso al Análisis Básico, se proporciona un código de ejemplo para una herramienta, que permite descargar los archivos JSON en un formato plano de archivo separado por comas que se puede usar para crear fácilmente gráficos y otras agregaciones.</span><span class="sxs-lookup"><span data-stu-id="ffa66-218">To make it easy to access the Core Analytics, we provide a sample code for a tool, which allows downloading the JSON files into a flat comma-separated file format, which can be used to easily create charts or other aggregations.</span></span>

<span data-ttu-id="ffa66-219">A continuación se muestra cómo puede usar la herramienta:</span><span class="sxs-lookup"><span data-stu-id="ffa66-219">Here is how you can use the tool:</span></span>

1.  <span data-ttu-id="ffa66-220">Visite el vínculo de GitHub: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv ](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )</span><span class="sxs-lookup"><span data-stu-id="ffa66-220">Visit the github link: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv ](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )</span></span>
2.  <span data-ttu-id="ffa66-221">Descargar el código</span><span class="sxs-lookup"><span data-stu-id="ffa66-221">Download the code</span></span>
3.  <span data-ttu-id="ffa66-222">Siga las instrucciones para compilarlo y configurarlo.</span><span class="sxs-lookup"><span data-stu-id="ffa66-222">Follow instructions to compile and configure</span></span>
4.  <span data-ttu-id="ffa66-223">Ejecute la herramienta.</span><span class="sxs-lookup"><span data-stu-id="ffa66-223">Run the tool</span></span>
5.  <span data-ttu-id="ffa66-224">El archivo CSV resultante muestra los datos de análisis en una jerarquía sencilla plana.</span><span class="sxs-lookup"><span data-stu-id="ffa66-224">Resulting CSV file shows the analytics data in a simple flat hierarchy.</span></span>

## <a name="consuming-diagnostics-logs-from-an-oms-log-analytics-repository"></a><span data-ttu-id="ffa66-225">Consumo de registros de diagnóstico desde un repositorio de Log Analytics de OMS</span><span class="sxs-lookup"><span data-stu-id="ffa66-225">Consuming diagnostics logs from an OMS Log Analytics repository</span></span>
<span data-ttu-id="ffa66-226">Log Analytics es un servicio de Operations Management Suite (OMS) que supervisa los entornos local y en la nube para mantener su disponibilidad y rendimiento.</span><span class="sxs-lookup"><span data-stu-id="ffa66-226">Log Analytics is a service in Operations Management Suite (OMS) that monitors your cloud and on-premises environments to maintain their availability and performance.</span></span> <span data-ttu-id="ffa66-227">Recopila los datos generados por los recursos en los entornos local y de nube y mediante otras herramientas de supervisión, para proporcionar análisis entre varios orígenes.</span><span class="sxs-lookup"><span data-stu-id="ffa66-227">It collects data generated by resources in your cloud and on-premises environments and from other monitoring tools to provide analysis across multiple sources.</span></span> 

<span data-ttu-id="ffa66-228">Para usar Log Analytics, debe [habilitar el registro](#enable-logging-with-azure-storage) en el repositorio de Log Analytics de OMS de Azure, que se describe anteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="ffa66-228">To use Log Analytics, you must [enable logging](#enable-logging-with-azure-storage) to the Azure OMS Log Analytics repository, which is discussed earlier in this article.</span></span>

### <a name="using-the-oms-repository"></a><span data-ttu-id="ffa66-229">Uso del repositorio OMS</span><span class="sxs-lookup"><span data-stu-id="ffa66-229">Using the OMS Repository</span></span>

 <span data-ttu-id="ffa66-230">El siguiente diagrama muestra la arquitectura de las entradas y salidas del repositorio:</span><span class="sxs-lookup"><span data-stu-id="ffa66-230">The following diagram shows the architecture of the inputs and outputs of the repository:</span></span>

![Repositorio de Log Analytics de OMS](./media/cdn-diagnostics-log/12_Repo-overview.png)

<span data-ttu-id="ffa66-232">*Figura 3: repositorio de Log Analytics*</span><span class="sxs-lookup"><span data-stu-id="ffa66-232">*Figure 3 - Log Analytics Repository*</span></span>

<span data-ttu-id="ffa66-233">Puede mostrar los datos en una variedad de formas mediante el uso de Soluciones de administración.</span><span class="sxs-lookup"><span data-stu-id="ffa66-233">You can display the data in a variety of ways by using Management Solutions.</span></span> <span data-ttu-id="ffa66-234">Puede obtener Soluciones de administración en [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).</span><span class="sxs-lookup"><span data-stu-id="ffa66-234">You can obtain Management Solutions from the [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).</span></span>

<span data-ttu-id="ffa66-235">Puede instalar las Soluciones de administración de Azure Marketplace, haciendo clic en el vínculo **Obtenerla ahora** en la parte inferior de cada solución.</span><span class="sxs-lookup"><span data-stu-id="ffa66-235">You can install management solutions from Azure marketplace by clicking the **Get it now** link at the bottom of each solution.</span></span>

### <a name="adding-an-oms-cdn-management-solution"></a><span data-ttu-id="ffa66-236">Agregación de una solución de administración de la red CDN de OMS</span><span class="sxs-lookup"><span data-stu-id="ffa66-236">Adding an OMS CDN Management Solution</span></span>

<span data-ttu-id="ffa66-237">Siga estos pasos para agregar una solución de administración:</span><span class="sxs-lookup"><span data-stu-id="ffa66-237">Follow these steps to add a Management Solution:</span></span>

1.   <span data-ttu-id="ffa66-238">Si aún no lo ha hecho, inicie sesión en Azure Portal mediante su suscripción de Azure y vaya al panel.</span><span class="sxs-lookup"><span data-stu-id="ffa66-238">If you haven't already done so, sign in to the Azure portal using your Azure subscription and go to your Dashboard.</span></span>
    <span data-ttu-id="ffa66-239">![Panel de Azure](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="ffa66-239">![Azure Dashboard](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span></span>

2. <span data-ttu-id="ffa66-240">En la hoja **Nuevo**, en **Marketplace**, seleccione **Supervisión y administración**.</span><span class="sxs-lookup"><span data-stu-id="ffa66-240">In the **New** blade under **Marketplace**, select **Monitoring + management**.</span></span>

    ![Marketplace](./media/cdn-diagnostics-log/14_Marketplace.png)

3. <span data-ttu-id="ffa66-242">En la hoja **Supervisión y administración**, haga clic en **Ver todo**.</span><span class="sxs-lookup"><span data-stu-id="ffa66-242">In the **Monitoring + management** blade, click **See all**.</span></span>

    ![Ver todos](./media/cdn-diagnostics-log/15_See-all.png)

4.  <span data-ttu-id="ffa66-244">Busque CDN en el cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="ffa66-244">Search for CDN in the search box.</span></span>

    ![Ver todos](./media/cdn-diagnostics-log/16_Search-for.png)

5.  <span data-ttu-id="ffa66-246">Seleccione **Análisis Básico de la red CDN de Azure**.</span><span class="sxs-lookup"><span data-stu-id="ffa66-246">Select **Azure CDN Core Analytics**.</span></span> 

    ![Ver todos](./media/cdn-diagnostics-log/17_Core-analytics.png)

6.  <span data-ttu-id="ffa66-248">Después de hacer clic en **Crear**, se le pedirá que cree una nueva área de trabajo de OMS o que utilice una ya existente.</span><span class="sxs-lookup"><span data-stu-id="ffa66-248">After clicking **Create**, you will be asked to create a new OMS workspace or use an existing one.</span></span> 

    ![Ver todos](./media/cdn-diagnostics-log/18_Adding-solution.png)

7.  <span data-ttu-id="ffa66-250">Seleccione el área de trabajo que creó antes.</span><span class="sxs-lookup"><span data-stu-id="ffa66-250">Select the workspace you created before.</span></span> <span data-ttu-id="ffa66-251">A continuación, debe agregar una cuenta de Automation.</span><span class="sxs-lookup"><span data-stu-id="ffa66-251">You then need to add an automation account.</span></span>

    ![Ver todos](./media/cdn-diagnostics-log/19_Add-automation.png)

8. <span data-ttu-id="ffa66-253">La siguiente pantalla muestra el formulario de la cuenta de Automation que debe rellenar.</span><span class="sxs-lookup"><span data-stu-id="ffa66-253">The following screen shows the automation account form you must fill out.</span></span> 

    ![Ver todos](./media/cdn-diagnostics-log/20_Automation.png)

9. <span data-ttu-id="ffa66-255">Una vez haya creado la cuenta de Automation, está listo para agregar la solución.</span><span class="sxs-lookup"><span data-stu-id="ffa66-255">Once you have created the automation account, you are ready to add your solution.</span></span> <span data-ttu-id="ffa66-256">Haga clic en el botón **Crear** .</span><span class="sxs-lookup"><span data-stu-id="ffa66-256">Click the **Create** button.</span></span>

    ![Ver todos](./media/cdn-diagnostics-log/21_Ready.png)

10. <span data-ttu-id="ffa66-258">La solución se ha agregado al área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="ffa66-258">Your solution has now been added to your workspace.</span></span> <span data-ttu-id="ffa66-259">Vuelva al panel de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ffa66-259">Go back to your Azure portal Dashboard.</span></span>

    ![Ver todos](./media/cdn-diagnostics-log/22_Dashboard.png)

    <span data-ttu-id="ffa66-261">Haga clic en el área de trabajo de Log Analytics que ha creado para ir al área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="ffa66-261">Click the Log Analytics workspace you created to go to your workspace.</span></span> 

11. <span data-ttu-id="ffa66-262">Haga clic en el icono del **Portal de OMS** para ver la nueva solución en el portal de OMS.</span><span class="sxs-lookup"><span data-stu-id="ffa66-262">Click the **OMS Portal** tile to see your new solution in the OMS portal.</span></span>

    ![Ver todos](./media/cdn-diagnostics-log/23_workspace.png)

12. <span data-ttu-id="ffa66-264">El portal de OMS debería tener un aspecto similar al de la siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="ffa66-264">Your OMS portal should now look like the following screen:</span></span>

    ![Ver todos](./media/cdn-diagnostics-log/24_OMS-solution.png)

    <span data-ttu-id="ffa66-266">Haga clic en uno de los iconos para ver las distintas vistas de los datos.</span><span class="sxs-lookup"><span data-stu-id="ffa66-266">Click one of the tiles to see several views into your data.</span></span>

    ![Ver todos](./media/cdn-diagnostics-log/25_Interior-view.png)

    <span data-ttu-id="ffa66-268">Puede desplazarse a izquierda o derecha para ver más iconos que representan vistas individuales de los datos.</span><span class="sxs-lookup"><span data-stu-id="ffa66-268">You can scroll left or right to see further tiles representing individual views into the data.</span></span> 

    <span data-ttu-id="ffa66-269">Al hacer clic en uno de los iconos, se dan más detalles sobre los datos.</span><span class="sxs-lookup"><span data-stu-id="ffa66-269">Clicking one of the tiles gives you more details about your data.</span></span>

     ![Ver todos](./media/cdn-diagnostics-log/26_Further-detail.png)

### <a name="offers-and-pricing-tiers"></a><span data-ttu-id="ffa66-271">Ofertas y planes de tarifa</span><span class="sxs-lookup"><span data-stu-id="ffa66-271">Offers and pricing tiers</span></span>

<span data-ttu-id="ffa66-272">Puede ver ofertas y planes de tarifa de las soluciones de administración de OMS [aquí](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).</span><span class="sxs-lookup"><span data-stu-id="ffa66-272">You can see offers and pricing tiers for OMS management solutions [here](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).</span></span>

### <a name="customizing-views"></a><span data-ttu-id="ffa66-273">Personalización de las vistas</span><span class="sxs-lookup"><span data-stu-id="ffa66-273">Customizing views</span></span>

<span data-ttu-id="ffa66-274">Puede personalizar la vista de los datos mediante el **Diseñador de vistas**.</span><span class="sxs-lookup"><span data-stu-id="ffa66-274">You can customize the view into your data by using the **View Designer**.</span></span> <span data-ttu-id="ffa66-275">Vaya al área de trabajo de OMS y comience a diseñar haciendo clic en el icono del **Diseñador de vistas**.</span><span class="sxs-lookup"><span data-stu-id="ffa66-275">Go to your OMS workspace and begin designing by clicking the **View Designer** tile.</span></span>

![Ver diseñador](./media/cdn-diagnostics-log/27_Designer.png)

<span data-ttu-id="ffa66-277">Puede arrastrar y soltar tipos de gráficos desde la izquierda y rellenar los detalles de los datos que desea analizar a la izquierda.</span><span class="sxs-lookup"><span data-stu-id="ffa66-277">You can drag and drop types of charts from the left and fill in the data details you want to analyze on the left.</span></span>

![Ver diseñador](./media/cdn-diagnostics-log/28_Designer.png)

    
## <a name="log-data-delays"></a><span data-ttu-id="ffa66-279">Retrasos en el registro de datos</span><span class="sxs-lookup"><span data-stu-id="ffa66-279">Log data delays</span></span>

<span data-ttu-id="ffa66-280">Retrasos en el registro de datos de Verizon</span><span class="sxs-lookup"><span data-stu-id="ffa66-280">Verizon log data delays</span></span> | <span data-ttu-id="ffa66-281">Retrasos en el registro de datos de Akamai</span><span class="sxs-lookup"><span data-stu-id="ffa66-281">Akamai log data delays</span></span>
--- | ---
<span data-ttu-id="ffa66-282">Los datos de registro de Verizon llevan 1 hora de retraso y tardan 2 horas en comenzar a aparecer tras la finalización de la propagación del punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="ffa66-282">Verizon log data is 1 hour delayed, and take up to 2 hours to start appearing after endpoint propagation completion.</span></span> | <span data-ttu-id="ffa66-283">Los datos de registro de Akamai llevan 24 horas de retraso y tardan 24 horas en comenzar a aparecer si se crearon hace más de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="ffa66-283">Akamai log data is 24 hours delayed, and takes up to 2 hours to start appearing if it was created more than 24 hours ago.</span></span> <span data-ttu-id="ffa66-284">Si se acaban de crear, los registros tardan en comenzar a aparecer hasta 25 horas.</span><span class="sxs-lookup"><span data-stu-id="ffa66-284">If it was recently created, it can take up to 25 hours for the logs to start appearing.</span></span>

## <a name="diagnostic-log-types-for-cdn-core-analytics"></a><span data-ttu-id="ffa66-285">Tipos de registro de diagnósticos para el Análisis Básico de la red CDN</span><span class="sxs-lookup"><span data-stu-id="ffa66-285">Diagnostic log types for CDN Core Analytics</span></span>

<span data-ttu-id="ffa66-286">Actualmente solo se ofrecen los registros de Análisis Básico que contienen métricas que muestran estadísticas de respuesta HTTP y estadísticas de salida, como se ven desde los servidores POP y perimetrales de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="ffa66-286">We currently offer only Core Analytics logs, which contain metrics showing HTTP response statistics and egress statistics as seen from the CDN POPs/edges.</span></span>

### <a name="core-analytics-metrics-details"></a><span data-ttu-id="ffa66-287">Detalles de las métricas de análisis básico</span><span class="sxs-lookup"><span data-stu-id="ffa66-287">Core Analytics Metrics Details</span></span>
<span data-ttu-id="ffa66-288">A continuación se muestra una lista de métricas disponibles en los registros de Análisis Básico.</span><span class="sxs-lookup"><span data-stu-id="ffa66-288">The following table shows a list of metrics available in the Core Analytics logs.</span></span> <span data-ttu-id="ffa66-289">No todas las métricas están disponibles en todos los proveedores, si bien tales diferencias son mínimas.</span><span class="sxs-lookup"><span data-stu-id="ffa66-289">Not all metrics are available from all providers, although such differences are minimal.</span></span> <span data-ttu-id="ffa66-290">La tabla siguiente también muestra si una determinada métrica está disponible en un proveedor.</span><span class="sxs-lookup"><span data-stu-id="ffa66-290">The following table also shows if a given metric is available from a provider.</span></span> <span data-ttu-id="ffa66-291">Tenga en cuenta que las métricas solo están disponibles para esos puntos de conexión de CDN que contienen tráfico.</span><span class="sxs-lookup"><span data-stu-id="ffa66-291">Please note that the metrics are available for only those CDN endpoints that have traffic on them.</span></span>


|<span data-ttu-id="ffa66-292">Métrica</span><span class="sxs-lookup"><span data-stu-id="ffa66-292">Metric</span></span>                     | <span data-ttu-id="ffa66-293">Descripción</span><span class="sxs-lookup"><span data-stu-id="ffa66-293">Description</span></span>   | <span data-ttu-id="ffa66-294">Verizon</span><span class="sxs-lookup"><span data-stu-id="ffa66-294">Verizon</span></span>  | <span data-ttu-id="ffa66-295">Akamai</span><span class="sxs-lookup"><span data-stu-id="ffa66-295">Akamai</span></span> 
|---------------------------|---------------|---|---|
| <span data-ttu-id="ffa66-296">RequestCountTotal</span><span class="sxs-lookup"><span data-stu-id="ffa66-296">RequestCountTotal</span></span>         |<span data-ttu-id="ffa66-297">Número total de solicitudes durante este periodo</span><span class="sxs-lookup"><span data-stu-id="ffa66-297">Total number of request hits during this period</span></span>| <span data-ttu-id="ffa66-298">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-298">Yes</span></span>  |<span data-ttu-id="ffa66-299">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-299">Yes</span></span>   |
| <span data-ttu-id="ffa66-300">RequestCountHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="ffa66-300">RequestCountHttpStatus2xx</span></span> |<span data-ttu-id="ffa66-301">Recuento de todas las solicitudes que dieron lugar a un código HTTP 2xx (por ejemplo, 200, 202)</span><span class="sxs-lookup"><span data-stu-id="ffa66-301">Count of all requests that resulted in a 2xx HTTP code (e.g. 200, 202)</span></span>              | <span data-ttu-id="ffa66-302">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-302">Yes</span></span>  |<span data-ttu-id="ffa66-303">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-303">Yes</span></span>   |
| <span data-ttu-id="ffa66-304">RequestCountHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="ffa66-304">RequestCountHttpStatus3xx</span></span> | <span data-ttu-id="ffa66-305">Recuento de todas las solicitudes que dieron lugar a un código HTTP 3xx (por ejemplo, 300, 302)</span><span class="sxs-lookup"><span data-stu-id="ffa66-305">Count of all requests that resulted in a 3xx HTTP code (e.g. 300, 302)</span></span>              | <span data-ttu-id="ffa66-306">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-306">Yes</span></span>  |<span data-ttu-id="ffa66-307">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-307">Yes</span></span>   |
| <span data-ttu-id="ffa66-308">RequestCountHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="ffa66-308">RequestCountHttpStatus4xx</span></span> |<span data-ttu-id="ffa66-309">Recuento de todas las solicitudes que dieron lugar a un código HTTP 4xx (por ejemplo, 400, 404)</span><span class="sxs-lookup"><span data-stu-id="ffa66-309">Count of all requests that resulted in a 4xx HTTP code (e.g. 400, 404)</span></span>               | <span data-ttu-id="ffa66-310">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-310">Yes</span></span>   |<span data-ttu-id="ffa66-311">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-311">Yes</span></span>   |
| <span data-ttu-id="ffa66-312">RequestCountHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="ffa66-312">RequestCountHttpStatus5xx</span></span> | <span data-ttu-id="ffa66-313">Recuento de todas las solicitudes que dieron lugar a un código HTTP 5xx (por ejemplo, 500, 504)</span><span class="sxs-lookup"><span data-stu-id="ffa66-313">Count of all requests that resulted in a 5xx HTTP code (e.g. 500, 504)</span></span>              | <span data-ttu-id="ffa66-314">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-314">Yes</span></span>  |<span data-ttu-id="ffa66-315">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-315">Yes</span></span>   |
| <span data-ttu-id="ffa66-316">RequestCountHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="ffa66-316">RequestCountHttpStatusOthers</span></span> |  <span data-ttu-id="ffa66-317">Recuento de todos los demás códigos HTTP (fuera del intervalo 2xx-5xx)</span><span class="sxs-lookup"><span data-stu-id="ffa66-317">Count of all other HTTP codes (outside of 2xx-5xx)</span></span> | <span data-ttu-id="ffa66-318">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-318">Yes</span></span>  |<span data-ttu-id="ffa66-319">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-319">Yes</span></span>   |
| <span data-ttu-id="ffa66-320">RequestCountHttpStatus200</span><span class="sxs-lookup"><span data-stu-id="ffa66-320">RequestCountHttpStatus200</span></span> | <span data-ttu-id="ffa66-321">Recuento de todas las solicitudes que dieron lugar a una respuesta de código HTTP 200</span><span class="sxs-lookup"><span data-stu-id="ffa66-321">Count of all requests that resulted in a 200 HTTP code response</span></span>              |<span data-ttu-id="ffa66-322">No</span><span class="sxs-lookup"><span data-stu-id="ffa66-322">No</span></span>   |<span data-ttu-id="ffa66-323">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-323">Yes</span></span>   |
| <span data-ttu-id="ffa66-324">RequestCountHttpStatus206</span><span class="sxs-lookup"><span data-stu-id="ffa66-324">RequestCountHttpStatus206</span></span> | <span data-ttu-id="ffa66-325">Recuento de todas las solicitudes que dieron lugar a una respuesta de código HTTP 206</span><span class="sxs-lookup"><span data-stu-id="ffa66-325">Count of all requests that resulted in a 206 HTTP code response</span></span>              |<span data-ttu-id="ffa66-326">No</span><span class="sxs-lookup"><span data-stu-id="ffa66-326">No</span></span>   |<span data-ttu-id="ffa66-327">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-327">Yes</span></span>   |
| <span data-ttu-id="ffa66-328">RequestCountHttpStatus302</span><span class="sxs-lookup"><span data-stu-id="ffa66-328">RequestCountHttpStatus302</span></span> | <span data-ttu-id="ffa66-329">Recuento de todas las solicitudes que dieron lugar a una respuesta de código HTTP 302</span><span class="sxs-lookup"><span data-stu-id="ffa66-329">Count of all requests that resulted in a 302 HTTP code response</span></span>              |<span data-ttu-id="ffa66-330">No</span><span class="sxs-lookup"><span data-stu-id="ffa66-330">No</span></span>   |<span data-ttu-id="ffa66-331">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-331">Yes</span></span>   |
| <span data-ttu-id="ffa66-332">RequestCountHttpStatus304</span><span class="sxs-lookup"><span data-stu-id="ffa66-332">RequestCountHttpStatus304</span></span> |  <span data-ttu-id="ffa66-333">Recuento de todas las solicitudes que dieron lugar a una respuesta de código HTTP 304</span><span class="sxs-lookup"><span data-stu-id="ffa66-333">Count of all requests that resulted in a 304 HTTP code response</span></span>             |<span data-ttu-id="ffa66-334">No</span><span class="sxs-lookup"><span data-stu-id="ffa66-334">No</span></span>   |<span data-ttu-id="ffa66-335">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-335">Yes</span></span>   |
| <span data-ttu-id="ffa66-336">RequestCountHttpStatus404</span><span class="sxs-lookup"><span data-stu-id="ffa66-336">RequestCountHttpStatus404</span></span> | <span data-ttu-id="ffa66-337">Recuento de todas las solicitudes que dieron lugar a una respuesta de código HTTP 404</span><span class="sxs-lookup"><span data-stu-id="ffa66-337">Count of all requests that resulted in a 404 HTTP code response</span></span>              |<span data-ttu-id="ffa66-338">No</span><span class="sxs-lookup"><span data-stu-id="ffa66-338">No</span></span>   |<span data-ttu-id="ffa66-339">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-339">Yes</span></span>   |
| <span data-ttu-id="ffa66-340">RequestCountCacheHit</span><span class="sxs-lookup"><span data-stu-id="ffa66-340">RequestCountCacheHit</span></span> |<span data-ttu-id="ffa66-341">Recuento de todas las solicitudes que dieron lugar a un acierto de caché.</span><span class="sxs-lookup"><span data-stu-id="ffa66-341">Count of all requests that resulted in a Cache Hit.</span></span> <span data-ttu-id="ffa66-342">Esto significa que el recurso se atendió directamente desde el servidor POP al cliente.</span><span class="sxs-lookup"><span data-stu-id="ffa66-342">This means the asset was served directly from the POP to the Client.</span></span>               | <span data-ttu-id="ffa66-343">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-343">Yes</span></span>  |<span data-ttu-id="ffa66-344">No</span><span class="sxs-lookup"><span data-stu-id="ffa66-344">No</span></span>   |
| <span data-ttu-id="ffa66-345">RequestCountCacheMiss</span><span class="sxs-lookup"><span data-stu-id="ffa66-345">RequestCountCacheMiss</span></span> | <span data-ttu-id="ffa66-346">Recuento de todas las solicitudes que dieron lugar a un error de caché.</span><span class="sxs-lookup"><span data-stu-id="ffa66-346">Count of all requests that resulted in a Cache Miss.</span></span> <span data-ttu-id="ffa66-347">Esto significa que el recurso no se encontró en el servidor POP más cercano al cliente y, por tanto, se recupera del origen.</span><span class="sxs-lookup"><span data-stu-id="ffa66-347">This means the asset was not found on the POP closest to the client, and therefore was retrieved from the Origin.</span></span>              |<span data-ttu-id="ffa66-348">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-348">Yes</span></span>   | <span data-ttu-id="ffa66-349">No</span><span class="sxs-lookup"><span data-stu-id="ffa66-349">No</span></span>  |
| <span data-ttu-id="ffa66-350">RequestCountCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="ffa66-350">RequestCountCacheNoCache</span></span> | <span data-ttu-id="ffa66-351">Recuento de todas las solicitudes a un recurso a las que se les impide almacenarse en caché debido a una configuración de usuario en el servidor perimetral.</span><span class="sxs-lookup"><span data-stu-id="ffa66-351">Count of all requests to an asset that are prevented from being cached due to a user configuration on the edge.</span></span>              |<span data-ttu-id="ffa66-352">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-352">Yes</span></span>   | <span data-ttu-id="ffa66-353">No</span><span class="sxs-lookup"><span data-stu-id="ffa66-353">No</span></span>  |
| <span data-ttu-id="ffa66-354">RequestCountCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="ffa66-354">RequestCountCacheUncacheable</span></span> | <span data-ttu-id="ffa66-355">Recuento de todas las solicitudes a recursos cuyos encabezados Cache-Control y Expires impiden que se almacenen en caché. Estos encabezados indican que no se deben almacenar en caché en un servidor POP o por el cliente HTTP.</span><span class="sxs-lookup"><span data-stu-id="ffa66-355">Count of all requests to assets that are prevented from being cached by the asset's Cache-Control and Expires headers, which indicate that it should not be cached on a POP or by the HTTP client</span></span>                |<span data-ttu-id="ffa66-356">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-356">Yes</span></span>   |<span data-ttu-id="ffa66-357">No</span><span class="sxs-lookup"><span data-stu-id="ffa66-357">No</span></span>   |
| <span data-ttu-id="ffa66-358">RequestCountCacheOthers</span><span class="sxs-lookup"><span data-stu-id="ffa66-358">RequestCountCacheOthers</span></span> | <span data-ttu-id="ffa66-359">Recuento de todas las solicitudes con un estado de caché no cubierto por lo anterior.</span><span class="sxs-lookup"><span data-stu-id="ffa66-359">Count of all requests with cache status not covered by above.</span></span>              |<span data-ttu-id="ffa66-360">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-360">Yes</span></span>   | <span data-ttu-id="ffa66-361">No</span><span class="sxs-lookup"><span data-stu-id="ffa66-361">No</span></span>  |
| <span data-ttu-id="ffa66-362">EgressTotal</span><span class="sxs-lookup"><span data-stu-id="ffa66-362">EgressTotal</span></span> | <span data-ttu-id="ffa66-363">Transferencia de datos salientes en GB</span><span class="sxs-lookup"><span data-stu-id="ffa66-363">Outbound data transfer in GB</span></span>              |<span data-ttu-id="ffa66-364">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-364">Yes</span></span>   |<span data-ttu-id="ffa66-365">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-365">Yes</span></span>   |
| <span data-ttu-id="ffa66-366">EgressHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="ffa66-366">EgressHttpStatus2xx</span></span> | <span data-ttu-id="ffa66-367">Transferencia de datos salientes* para respuestas con códigos de estado HTTP 2xx en GB</span><span class="sxs-lookup"><span data-stu-id="ffa66-367">Outbound data transfer* for responses with 2xx HTTP status codes in GB</span></span>            |<span data-ttu-id="ffa66-368">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-368">Yes</span></span>   |<span data-ttu-id="ffa66-369">No</span><span class="sxs-lookup"><span data-stu-id="ffa66-369">No</span></span>   |
| <span data-ttu-id="ffa66-370">EgressHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="ffa66-370">EgressHttpStatus3xx</span></span> | <span data-ttu-id="ffa66-371">Transferencia de datos salientes para respuestas con códigos de estado HTTP 3xx en GB</span><span class="sxs-lookup"><span data-stu-id="ffa66-371">Outbound data transfer for responses with 3xx HTTP status codes in GB</span></span>              |<span data-ttu-id="ffa66-372">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-372">Yes</span></span>   |<span data-ttu-id="ffa66-373">No</span><span class="sxs-lookup"><span data-stu-id="ffa66-373">No</span></span>   |
| <span data-ttu-id="ffa66-374">EgressHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="ffa66-374">EgressHttpStatus4xx</span></span> | <span data-ttu-id="ffa66-375">Transferencia de datos de salida para respuestas con códigos de estado HTTP 4xx en GB</span><span class="sxs-lookup"><span data-stu-id="ffa66-375">Outbound data transfer for responses with 4xx HTTP status codes in GB</span></span>               |<span data-ttu-id="ffa66-376">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-376">Yes</span></span>   | <span data-ttu-id="ffa66-377">No</span><span class="sxs-lookup"><span data-stu-id="ffa66-377">No</span></span>  |
| <span data-ttu-id="ffa66-378">EgressHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="ffa66-378">EgressHttpStatus5xx</span></span> | <span data-ttu-id="ffa66-379">Transferencia de datos de salida para respuestas con códigos de estado HTTP 5xx en GB</span><span class="sxs-lookup"><span data-stu-id="ffa66-379">Outbound data transfer for responses with 5xx HTTP status codes in GB</span></span>               |<span data-ttu-id="ffa66-380">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-380">Yes</span></span>   |  <span data-ttu-id="ffa66-381">No</span><span class="sxs-lookup"><span data-stu-id="ffa66-381">No</span></span> |
| <span data-ttu-id="ffa66-382">EgressHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="ffa66-382">EgressHttpStatusOthers</span></span> | <span data-ttu-id="ffa66-383">Transferencia de datos de salida para respuestas con otros códigos de estado HTTP en GB</span><span class="sxs-lookup"><span data-stu-id="ffa66-383">Outbound data transfer for responses with other HTTP status codes in GB</span></span>                |<span data-ttu-id="ffa66-384">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-384">Yes</span></span>   |<span data-ttu-id="ffa66-385">No</span><span class="sxs-lookup"><span data-stu-id="ffa66-385">No</span></span>   |
| <span data-ttu-id="ffa66-386">EgressCacheHit</span><span class="sxs-lookup"><span data-stu-id="ffa66-386">EgressCacheHit</span></span> |  <span data-ttu-id="ffa66-387">Transferencia de datos de salida para respuestas que se entregaron directamente desde la caché de la red CDN en los servidores POP/perimetrales de la red CDN</span><span class="sxs-lookup"><span data-stu-id="ffa66-387">Outbound data transfer for responses that were delivered directly from the CDN cache on the CDN POPs/Edges</span></span>  |<span data-ttu-id="ffa66-388">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-388">Yes</span></span>   |  <span data-ttu-id="ffa66-389">No</span><span class="sxs-lookup"><span data-stu-id="ffa66-389">No</span></span> |
| <span data-ttu-id="ffa66-390">EgressCacheMiss</span><span class="sxs-lookup"><span data-stu-id="ffa66-390">EgressCacheMiss</span></span> | <span data-ttu-id="ffa66-391">Transferencia de datos de salida para respuestas que no se encontraron en el servidor POP más cercano y que se recuperaron del servidor de origen</span><span class="sxs-lookup"><span data-stu-id="ffa66-391">Outbound data transfer for responses that were not found on the nearest POP server, and retrieved from the origin server</span></span>              |<span data-ttu-id="ffa66-392">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-392">Yes</span></span>   |  <span data-ttu-id="ffa66-393">No</span><span class="sxs-lookup"><span data-stu-id="ffa66-393">No</span></span> |
| <span data-ttu-id="ffa66-394">EgressCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="ffa66-394">EgressCacheNoCache</span></span> | <span data-ttu-id="ffa66-395">Transferencia de datos de salida para recursos a los que se les impide almacenarse en caché debido a una configuración de usuario en el servidor perimetral.</span><span class="sxs-lookup"><span data-stu-id="ffa66-395">Outbound data transfer for assets that are prevented from being cached due to a user configuration on the edge.</span></span>                |<span data-ttu-id="ffa66-396">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-396">Yes</span></span>   |<span data-ttu-id="ffa66-397">No</span><span class="sxs-lookup"><span data-stu-id="ffa66-397">No</span></span>   |
| <span data-ttu-id="ffa66-398">EgressCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="ffa66-398">EgressCacheUncacheable</span></span> | <span data-ttu-id="ffa66-399">Transferencia de datos de salida para recursos cuyos encabezados Cache-Control o Expires impiden que se almacenen en caché. Estos encabezados indican que no se deben almacenar en caché en un servidor POP o por el cliente HTTP.</span><span class="sxs-lookup"><span data-stu-id="ffa66-399">Outbound data transfer for assets that are prevented from being cached by the asset's Cache-Control and/or Expires headers, which indicate that it should not be cached on a POP or by the HTTP client</span></span>                    |<span data-ttu-id="ffa66-400">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-400">Yes</span></span>   | <span data-ttu-id="ffa66-401">No</span><span class="sxs-lookup"><span data-stu-id="ffa66-401">No</span></span>  |
| <span data-ttu-id="ffa66-402">EgressCacheOthers</span><span class="sxs-lookup"><span data-stu-id="ffa66-402">EgressCacheOthers</span></span> |  <span data-ttu-id="ffa66-403">Transferencias de datos de salida para otros escenarios de caché.</span><span class="sxs-lookup"><span data-stu-id="ffa66-403">Outbound data transfers for other cache scenarios.</span></span>             |<span data-ttu-id="ffa66-404">Sí</span><span class="sxs-lookup"><span data-stu-id="ffa66-404">Yes</span></span>   | <span data-ttu-id="ffa66-405">No</span><span class="sxs-lookup"><span data-stu-id="ffa66-405">No</span></span>  |

<span data-ttu-id="ffa66-406">*Con transferencia de datos de salida nos referimos al tráfico entregado al cliente desde los servidores POP de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="ffa66-406">*Outbound data transfer refers to traffic delivered from CDN POP servers to the client.</span></span>


### <a name="schema-of-the-core-analytics-logs"></a><span data-ttu-id="ffa66-407">Esquema de los registros de análisis básico</span><span class="sxs-lookup"><span data-stu-id="ffa66-407">Schema of the Core Analytics Logs</span></span> 

<span data-ttu-id="ffa66-408">Todos los registros se almacenan en formato JSON y cada entrada tiene campos de cadena que siguen el siguiente esquema:</span><span class="sxs-lookup"><span data-stu-id="ffa66-408">All logs are stored in JSON format and each entry has string fields following the below schema:</span></span>

```json
    "records": [
        {
            "time": "2017-04-27T01:00:00",
            "resourceId": "<ARM Resource Id of the CDN Endpoint>",
            "operationName": "Microsoft.Cdn/profiles/endpoints/contentDelivery",
            "category": "CoreAnalytics",
            "properties": {
                "DomainName": "<Name of the domain for which the statistics is reported>",
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

<span data-ttu-id="ffa66-409">Donde "time" representa la hora de inicio del límite horario cuyas estadísticas se notifican.</span><span class="sxs-lookup"><span data-stu-id="ffa66-409">Where the ‘time’ represents the start time of the hour boundary for which the statistics is reported.</span></span> <span data-ttu-id="ffa66-410">Cuando un proveedor de CDN no admite una métrica, en lugar de un valor doble o entero, habrá un valor nulo.</span><span class="sxs-lookup"><span data-stu-id="ffa66-410">When a metric is not supported by a CDN provider, instead of a double or integer value, there will be a null value.</span></span> <span data-ttu-id="ffa66-411">Este valor nulo indica la ausencia de una métrica, y esto es diferente de un valor de 0.</span><span class="sxs-lookup"><span data-stu-id="ffa66-411">This null value indicates the absence of a metric, and this is different from a 0 value.</span></span> <span data-ttu-id="ffa66-412">Tenga en cuenta también que habrá un conjunto de estas métricas por dominio configurado en el punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="ffa66-412">Also note that there will be one set of these metrics per domain configured on the endpoint.</span></span>

<span data-ttu-id="ffa66-413">Propiedades de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ffa66-413">Example properties below:</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="ffa66-414">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="ffa66-414">Additional resources</span></span>

* [<span data-ttu-id="ffa66-415">Registros de diagnóstico de Azure</span><span class="sxs-lookup"><span data-stu-id="ffa66-415">Azure Diagnostic logs</span></span>](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)
* [<span data-ttu-id="ffa66-416">Análisis básico mediante el portal complementario de la red CDN</span><span class="sxs-lookup"><span data-stu-id="ffa66-416">Core analytics via Azure CDN supplemental portal</span></span>](https://docs.microsoft.com/azure/cdn/cdn-analyze-usage-patterns)
* [<span data-ttu-id="ffa66-417">Log Analytics de OMS de Azure</span><span class="sxs-lookup"><span data-stu-id="ffa66-417">Azure OMS Log Analytics</span></span>](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-overview)
* [<span data-ttu-id="ffa66-418">API de REST de Azure Log Analytics</span><span class="sxs-lookup"><span data-stu-id="ffa66-418">Azure Log Analytics REST API</span></span>](https://docs.microsoft.com/en-us/rest/api/loganalytics)







