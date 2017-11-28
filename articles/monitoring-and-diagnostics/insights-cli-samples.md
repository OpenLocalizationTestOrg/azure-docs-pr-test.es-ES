---
title: "ejemplos de inicio rápido de aaaAzure Monitor CLI 1.0. | Microsoft Docs"
description: "Comandos de ejemplo de la CLI 1.0 para las características de Azure Monitor. Monitor de Azure es un servicio de Microsoft Azure que permite las notificaciones de alerta de toosend, direcciones URL web de llamada en función de los valores de los datos de telemetría configurado y servicios de escalado automático en la nube, máquinas virtuales y aplicaciones Web."
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 1653aa81-0ee6-4622-9c65-d4801ed9006f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 6cd9cd62b3a1977276563f5e43f5384ccca66247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor--cross-platform-cli-10-quick-start-samples"></a><span data-ttu-id="0ffd9-105">Ejemplos de inicio rápido de la CLI multiplataforma de Azure Monitor 1.0</span><span class="sxs-lookup"><span data-stu-id="0ffd9-105">Azure Monitor  Cross-platform CLI 1.0 quick start samples</span></span>
<span data-ttu-id="0ffd9-106">Este artículo se demuestra que tome las muestras toohelp de comandos de interfaz de línea de comandos (CLI) tener acceso a características del Monitor de Azure.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-106">This article shows you sample command-line interface (CLI) commands toohelp you access Azure Monitor features.</span></span> <span data-ttu-id="0ffd9-107">Monitor de Azure le permite tooAutoScale servicios en la nube, máquinas virtuales y las aplicaciones Web y toosend notificaciones de alerta o direcciones URL de web de llamada basadas en valores de datos de telemetría configurado.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-107">Azure Monitor allows you tooAutoScale Cloud Services, Virtual Machines, and Web Apps and toosend alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="0ffd9-108">Monitor de Azure es Hola nuevo nombre lo que se conoce como "Azure Insights" hasta 25 de septiembre de 2016.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-108">Azure Monitor is hello new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="0ffd9-109">Sin embargo, los espacios de nombres de hello y, por lo tanto, comandos de hello siguientes sigue sin contengan visión"Hola".</span><span class="sxs-lookup"><span data-stu-id="0ffd9-109">However, hello namespaces and thus hello commands below still contain hello "insights".</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="0ffd9-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0ffd9-110">Prerequisites</span></span>
<span data-ttu-id="0ffd9-111">Si aún no ha instalado Hola CLI de Azure, consulte [Install hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="0ffd9-111">If you haven't already installed hello Azure CLI, see [Install hello Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="0ffd9-112">Si no está familiarizado con la CLI de Azure, puede obtener más información al respecto en [Hola Utilice CLI de Azure para Mac, Linux y Windows con el Administrador de recursos de Azure](../xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="0ffd9-112">If you're unfamiliar with Azure CLI, you can read more about it at [Use hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../xplat-cli-azure-resource-manager.md).</span></span>

<span data-ttu-id="0ffd9-113">En Windows, instale npm de hello [sitio Web de Node.js](https://nodejs.org/).</span><span class="sxs-lookup"><span data-stu-id="0ffd9-113">In Windows, install npm from hello [Node.js website](https://nodejs.org/).</span></span> <span data-ttu-id="0ffd9-114">Después de completar la instalación de hello, usando CMD.exe con privilegios de ejecutar como administrador, ejecute siguiente Hola de carpeta Hola donde está instalado npm:</span><span class="sxs-lookup"><span data-stu-id="0ffd9-114">After you complete hello installation, using CMD.exe with Run As Administrator privileges, execute hello following from hello folder where npm is installed:</span></span>

```console
npm install azure-cli --global
```

<span data-ttu-id="0ffd9-115">A continuación, desplácese tooany/ubicación de la carpeta que desee y escriba en Hola de línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="0ffd9-115">Next, navigate tooany folder/location you want and type at hello command-line:</span></span>

```console
azure help
```

## <a name="log-in-tooazure"></a><span data-ttu-id="0ffd9-116">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="0ffd9-116">Log in tooAzure</span></span>
<span data-ttu-id="0ffd9-117">Hola primer paso es toologin tooyour cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-117">hello first step is toologin tooyour Azure account.</span></span>

```console
azure login
```

<span data-ttu-id="0ffd9-118">Después de ejecutar este comando, tiene toosign en a través de instrucciones de hello en pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-118">After running this command, you have toosign in via hello instructions on hello screen.</span></span> <span data-ttu-id="0ffd9-119">Después, podrá ver el id. predeterminado de la suscripción, el id. de inquilino y la cuenta. Todos los comandos funcionan en el contexto de Hola de su suscripción de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-119">Afterward, you see your Account, TenantId, and default Subscription Id. All commands work in hello context of your default subscription.</span></span>

<span data-ttu-id="0ffd9-120">detalles de hello toolist de su suscripción actual, use Hola siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-120">toolist hello details of your current subscription, use hello following command.</span></span>

```console
azure account show
```

<span data-ttu-id="0ffd9-121">toochange trabajo contexto tooa otra suscripción, Hola de uso siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-121">toochange working context tooa different subscription, use hello following command.</span></span>

```console
azure account set "subscription ID or subscription name"
```

<span data-ttu-id="0ffd9-122">toouse Administrador de recursos de Azure y Azure Monitor comandos, necesita toobe en modo Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-122">toouse Azure Resource Manager and Azure Monitor commands, you need toobe in Azure Resource Manager mode.</span></span>

```console
azure config mode arm
```

<span data-ttu-id="0ffd9-123">tooview una lista de todos los comandos admitidos de Monitor de Azure, realice siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-123">tooview a list of all supported Azure Monitor commands, perform hello following.</span></span>

```console
azure insights
```

## <a name="view-activity-log-for-a-subscription"></a><span data-ttu-id="0ffd9-124">Visualización del registro de actividades para una suscripción</span><span class="sxs-lookup"><span data-stu-id="0ffd9-124">View activity log for a subscription</span></span>
<span data-ttu-id="0ffd9-125">tooview una lista de eventos de registro de actividad, realice el siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-125">tooview a list of activity log events, perform hello following.</span></span>

```console
azure insights logs list [options]
```

<span data-ttu-id="0ffd9-126">Intente Hola después tooview todas las opciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-126">Try hello following tooview all available options.</span></span>

```console
azure insights logs list -help
```

<span data-ttu-id="0ffd9-127">Este es un ejemplo registros toolist por un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="0ffd9-127">Here is an example toolist logs by a resourceGroup</span></span>

```console
azure insights logs list --resourceGroup "myrg1"
```

<span data-ttu-id="0ffd9-128">Registros de toolist de ejemplo de llamada</span><span class="sxs-lookup"><span data-stu-id="0ffd9-128">Example toolist logs by caller</span></span>

```console
azure insights logs list --caller "myname@company.com"
```

<span data-ttu-id="0ffd9-129">Registros de toolist de ejemplo por el llamador en un tipo de recurso, dentro de una fecha de inicio y finalización</span><span class="sxs-lookup"><span data-stu-id="0ffd9-129">Example toolist logs by caller on a resource type, within a start and end date</span></span>

```console
azure insights logs list --resourceProvider "Microsoft.Web" --caller "myname@company.com" --startTime 2016-03-08T00:00:00Z --endTime 2016-03-16T00:00:00Z
```

## <a name="work-with-alerts"></a><span data-ttu-id="0ffd9-130">Uso de alertas</span><span class="sxs-lookup"><span data-stu-id="0ffd9-130">Work with alerts</span></span>
<span data-ttu-id="0ffd9-131">Puede utilizar información de hello en hello sección toowork con las alertas.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-131">You can use hello information in hello section toowork with alerts.</span></span>

### <a name="get-alert-rules-in-a-resource-group"></a><span data-ttu-id="0ffd9-132">Obtención de reglas de alerta en un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="0ffd9-132">Get alert rules in a resource group</span></span>
```console
azure insights alerts rule list abhingrgtest123
azure insights alerts rule list abhingrgtest123 --ruleName andy0323
```

### <a name="create-a-metric-alert-rule"></a><span data-ttu-id="0ffd9-133">Creación de una regla de alerta de métrica</span><span class="sxs-lookup"><span data-stu-id="0ffd9-133">Create a metric alert rule</span></span>
```console
azure insights alerts actions email create --customEmails foo@microsoft.com
azure insights alerts actions webhook create https://someuri.com
azure insights alerts rule metric set andy0323 eastus abhingrgtest123 PT5M GreaterThan 2 /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Web-EastUS/providers/Microsoft.Web/serverfarms/Default1 BytesReceived Total
```

### <a name="create-webtest-alert-rule"></a><span data-ttu-id="0ffd9-134">Creación de una regla de alerta de WebTest</span><span class="sxs-lookup"><span data-stu-id="0ffd9-134">Create webtest alert rule</span></span>
```console
azure insights alerts rule webtest set leowebtestr1-webtestr1 eastus Default-Web-WestUS PT5M 1 GSMT_AvRaw /subscriptions/b67f7fec-69fc-4974-9099-a26bd6ffeda3/resourcegroups/Default-Web-WestUS/providers/microsoft.insights/webtests/leowebtestr1-webtestr1
```

### <a name="delete-an-alert-rule"></a><span data-ttu-id="0ffd9-135">Creación una regla de alerta</span><span class="sxs-lookup"><span data-stu-id="0ffd9-135">Delete an alert rule</span></span>
```console
azure insights alerts rule delete abhingrgtest123 andy0323
```

## <a name="log-profiles"></a><span data-ttu-id="0ffd9-136">Perfiles de registro</span><span class="sxs-lookup"><span data-stu-id="0ffd9-136">Log profiles</span></span>
<span data-ttu-id="0ffd9-137">Utilice la información de hello en este toowork sección con los perfiles de registro.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-137">Use hello information in this section toowork with log profiles.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="0ffd9-138">Obtención de un perfil de registro</span><span class="sxs-lookup"><span data-stu-id="0ffd9-138">Get a log profile</span></span>
```console
azure insights logprofile list
azure insights logprofile get -n default
```


### <a name="add-a-log-profile-without-retention"></a><span data-ttu-id="0ffd9-139">Adición de un perfil de registro sin retención de datos</span><span class="sxs-lookup"><span data-stu-id="0ffd9-139">Add a log profile without retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="0ffd9-140">Eliminación de un perfil de registro</span><span class="sxs-lookup"><span data-stu-id="0ffd9-140">Remove a log profile</span></span>
```console
azure insights logprofile delete --name default
```

### <a name="add-a-log-profile-with-retention"></a><span data-ttu-id="0ffd9-141">Adición de un perfil de registro con retención de datos</span><span class="sxs-lookup"><span data-stu-id="0ffd9-141">Add a log profile with retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```

### <a name="add-a-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="0ffd9-142">Adición de un perfil de registro con retención y EventHub</span><span class="sxs-lookup"><span data-stu-id="0ffd9-142">Add a log profile with retention and EventHub</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --serviceBusRuleId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/testshoeboxeastus/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```


## <a name="diagnostics"></a><span data-ttu-id="0ffd9-143">Diagnóstico</span><span class="sxs-lookup"><span data-stu-id="0ffd9-143">Diagnostics</span></span>
<span data-ttu-id="0ffd9-144">Utilice la información de hello en este toowork sección con la configuración de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-144">Use hello information in this section toowork with diagnostic settings.</span></span>

### <a name="get-a-diagnostic-setting"></a><span data-ttu-id="0ffd9-145">Obtención de la configuración de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="0ffd9-145">Get a diagnostic setting</span></span>
```console
azure insights diagnostic get --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp
```

### <a name="disable-a-diagnostic-setting"></a><span data-ttu-id="0ffd9-146">Deshabilitación de la configuración de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="0ffd9-146">Disable a diagnostic setting</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled false
```

### <a name="enable-a-diagnostic-setting-without-retention"></a><span data-ttu-id="0ffd9-147">Habilitación de la configuración de diagnóstico sin retención</span><span class="sxs-lookup"><span data-stu-id="0ffd9-147">Enable a diagnostic setting without retention</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled true
```


## <a name="autoscale"></a><span data-ttu-id="0ffd9-148">Autoscale</span><span class="sxs-lookup"><span data-stu-id="0ffd9-148">Autoscale</span></span>
<span data-ttu-id="0ffd9-149">Utilice la información de hello en este toowork sección con la configuración de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-149">Use hello information in this section toowork with autoscale settings.</span></span> <span data-ttu-id="0ffd9-150">Debe toomodify estos ejemplos.</span><span class="sxs-lookup"><span data-stu-id="0ffd9-150">You need toomodify these examples.</span></span>

### <a name="get-autoscale-settings-for-a-resource-group"></a><span data-ttu-id="0ffd9-151">Obtención de la configuración de escalado automático de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="0ffd9-151">Get autoscale settings for a resource group</span></span>
```console
azure insights autoscale setting list montest2
```

### <a name="get-autoscale-settings-by-name-in-a-resource-group"></a><span data-ttu-id="0ffd9-152">Obtención de valores de escalado automático por su nombre en un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="0ffd9-152">Get autoscale settings by name in a resource group</span></span>
```console
azure insights autoscale setting list montest2 -n setting2
```


### <a name="set-auotoscale-settings"></a><span data-ttu-id="0ffd9-153">Establecimiento de la configuración de escalado automático</span><span class="sxs-lookup"><span data-stu-id="0ffd9-153">Set auotoscale settings</span></span>
```console
azure insights autoscale setting set montest2 -n setting2 --settingSpec
```
