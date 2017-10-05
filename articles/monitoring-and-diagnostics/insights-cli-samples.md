---
title: "Ejemplos de inicio rápido de CLI de Azure Monitor 1.0 | Microsoft Docs"
description: "Comandos de ejemplo de la CLI 1.0 para las características de Azure Monitor. Azure Monitor es un servicio de Microsoft Azure que permite enviar notificaciones de alerta, llamar a direcciones URL web en función de los valores de datos de telemetría configurados y escalar automáticamente Cloud Services, Virtual Machines y Web Apps."
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
ms.openlocfilehash: ec4512500dc3c77a40d2ebd1e6b460d5bb005811
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-monitor--cross-platform-cli-10-quick-start-samples"></a><span data-ttu-id="c597b-105">Ejemplos de inicio rápido de la CLI multiplataforma de Azure Monitor 1.0</span><span class="sxs-lookup"><span data-stu-id="c597b-105">Azure Monitor  Cross-platform CLI 1.0 quick start samples</span></span>
<span data-ttu-id="c597b-106">En este artículo se muestran comandos de la interfaz de la línea de comandos (CLI) de ejemplo que lo ayudarán a acceder a las características de supervisión de Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="c597b-106">This article shows you sample command-line interface (CLI) commands to help you access Azure Monitor features.</span></span> <span data-ttu-id="c597b-107">Azure Monitor permite escalar automáticamente Cloud Services, Virtual Machines y Web Apps para enviar notificaciones de alerta o llamar a direcciones URL web en función de los valores de datos de telemetría configurados.</span><span class="sxs-lookup"><span data-stu-id="c597b-107">Azure Monitor allows you to AutoScale Cloud Services, Virtual Machines, and Web Apps and to send alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="c597b-108">Azure Monitor es el nuevo nombre de lo que se conocía como "Azure Insights" hasta el 25 de septiembre de 2016.</span><span class="sxs-lookup"><span data-stu-id="c597b-108">Azure Monitor is the new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="c597b-109">Sin embargo, los espacios de nombres y, por tanto, los siguientes comandos aún contienen el término "insights".</span><span class="sxs-lookup"><span data-stu-id="c597b-109">However, the namespaces and thus the commands below still contain the "insights".</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="c597b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c597b-110">Prerequisites</span></span>
<span data-ttu-id="c597b-111">Si no ha instalado aún la CLI, consulte [Instalación de la CLI de Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c597b-111">If you haven't already installed the Azure CLI, see [Install the Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="c597b-112">Si no está familiarizado con la CLI de Azure, puede obtener más información en [Uso de la CLI de Azure para Mac, Linux y Windows con Azure Resource Manager](../xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="c597b-112">If you're unfamiliar with Azure CLI, you can read more about it at [Use the Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../xplat-cli-azure-resource-manager.md).</span></span>

<span data-ttu-id="c597b-113">En Windows, instale npm desde el [sitio web de Node.js](https://nodejs.org/).</span><span class="sxs-lookup"><span data-stu-id="c597b-113">In Windows, install npm from the [Node.js website](https://nodejs.org/).</span></span> <span data-ttu-id="c597b-114">Después de completar la instalación, usando el archivo CMD.exe con los privilegios Ejecutar como administrador, ejecute el siguiente comando desde la carpeta donde se ha instalado npm:</span><span class="sxs-lookup"><span data-stu-id="c597b-114">After you complete the installation, using CMD.exe with Run As Administrator privileges, execute the following from the folder where npm is installed:</span></span>

```console
npm install azure-cli --global
```

<span data-ttu-id="c597b-115">Después, vaya a cualquier carpeta o ubicación que desee y escriba en la línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="c597b-115">Next, navigate to any folder/location you want and type at the command-line:</span></span>

```console
azure help
```

## <a name="log-in-to-azure"></a><span data-ttu-id="c597b-116">Inicie sesión en Azure.</span><span class="sxs-lookup"><span data-stu-id="c597b-116">Log in to Azure</span></span>
<span data-ttu-id="c597b-117">El primer paso consiste en iniciar sesión en su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="c597b-117">The first step is to login to your Azure account.</span></span>

```console
azure login
```

<span data-ttu-id="c597b-118">Después de ejecutar este comando, tendrá que iniciar sesión siguiendo las instrucciones de la pantalla.</span><span class="sxs-lookup"><span data-stu-id="c597b-118">After running this command, you have to sign in via the instructions on the screen.</span></span> <span data-ttu-id="c597b-119">Después, podrá ver el id. predeterminado de la suscripción, el id. de inquilino y la cuenta. Todos los comandos funcionan en el contexto de la suscripción predeterminada.</span><span class="sxs-lookup"><span data-stu-id="c597b-119">Afterward, you see your Account, TenantId, and default Subscription Id. All commands work in the context of your default subscription.</span></span>

<span data-ttu-id="c597b-120">Para mostrar los detalles de la suscripción actual, utilice el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="c597b-120">To list the details of your current subscription, use the following command.</span></span>

```console
azure account show
```

<span data-ttu-id="c597b-121">Para cambiar el contexto de trabajo a una suscripción diferente, utilice el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="c597b-121">To change working context to a different subscription, use the following command.</span></span>

```console
azure account set "subscription ID or subscription name"
```

<span data-ttu-id="c597b-122">Para utilizar los comandos de Azure Resource Manager y Azure Monitor, debe estar en el modo ARM.</span><span class="sxs-lookup"><span data-stu-id="c597b-122">To use Azure Resource Manager and Azure Monitor commands, you need to be in Azure Resource Manager mode.</span></span>

```console
azure config mode arm
```

<span data-ttu-id="c597b-123">Para ver una lista de todos los comandos de Azure Monitor admitidos, realice lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="c597b-123">To view a list of all supported Azure Monitor commands, perform the following.</span></span>

```console
azure insights
```

## <a name="view-activity-log-for-a-subscription"></a><span data-ttu-id="c597b-124">Visualización del registro de actividades para una suscripción</span><span class="sxs-lookup"><span data-stu-id="c597b-124">View activity log for a subscription</span></span>
<span data-ttu-id="c597b-125">Para ver una lista de eventos del registro de actividades, realice lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="c597b-125">To view a list of activity log events, perform the following.</span></span>

```console
azure insights logs list [options]
```

<span data-ttu-id="c597b-126">Pruebe el siguiente comando para ver todas las opciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="c597b-126">Try the following to view all available options.</span></span>

```console
azure insights logs list -help
```

<span data-ttu-id="c597b-127">Se trata de un ejemplo para mostrar los registros por grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c597b-127">Here is an example to list logs by a resourceGroup</span></span>

```console
azure insights logs list --resourceGroup "myrg1"
```

<span data-ttu-id="c597b-128">Ejemplo para mostrar registros por autor de llamada</span><span class="sxs-lookup"><span data-stu-id="c597b-128">Example to list logs by caller</span></span>

```console
azure insights logs list --caller "myname@company.com"
```

<span data-ttu-id="c597b-129">Ejemplo para mostrar registros por tipo de recurso en una fecha de inicio y de finalización</span><span class="sxs-lookup"><span data-stu-id="c597b-129">Example to list logs by caller on a resource type, within a start and end date</span></span>

```console
azure insights logs list --resourceProvider "Microsoft.Web" --caller "myname@company.com" --startTime 2016-03-08T00:00:00Z --endTime 2016-03-16T00:00:00Z
```

## <a name="work-with-alerts"></a><span data-ttu-id="c597b-130">Uso de alertas</span><span class="sxs-lookup"><span data-stu-id="c597b-130">Work with alerts</span></span>
<span data-ttu-id="c597b-131">Puede usar la información de la sección sobre cómo usar las alertas.</span><span class="sxs-lookup"><span data-stu-id="c597b-131">You can use the information in the section to work with alerts.</span></span>

### <a name="get-alert-rules-in-a-resource-group"></a><span data-ttu-id="c597b-132">Obtención de reglas de alerta en un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="c597b-132">Get alert rules in a resource group</span></span>
```console
azure insights alerts rule list abhingrgtest123
azure insights alerts rule list abhingrgtest123 --ruleName andy0323
```

### <a name="create-a-metric-alert-rule"></a><span data-ttu-id="c597b-133">Creación de una regla de alerta de métrica</span><span class="sxs-lookup"><span data-stu-id="c597b-133">Create a metric alert rule</span></span>
```console
azure insights alerts actions email create --customEmails foo@microsoft.com
azure insights alerts actions webhook create https://someuri.com
azure insights alerts rule metric set andy0323 eastus abhingrgtest123 PT5M GreaterThan 2 /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Web-EastUS/providers/Microsoft.Web/serverfarms/Default1 BytesReceived Total
```

### <a name="create-webtest-alert-rule"></a><span data-ttu-id="c597b-134">Creación de una regla de alerta de WebTest</span><span class="sxs-lookup"><span data-stu-id="c597b-134">Create webtest alert rule</span></span>
```console
azure insights alerts rule webtest set leowebtestr1-webtestr1 eastus Default-Web-WestUS PT5M 1 GSMT_AvRaw /subscriptions/b67f7fec-69fc-4974-9099-a26bd6ffeda3/resourcegroups/Default-Web-WestUS/providers/microsoft.insights/webtests/leowebtestr1-webtestr1
```

### <a name="delete-an-alert-rule"></a><span data-ttu-id="c597b-135">Creación una regla de alerta</span><span class="sxs-lookup"><span data-stu-id="c597b-135">Delete an alert rule</span></span>
```console
azure insights alerts rule delete abhingrgtest123 andy0323
```

## <a name="log-profiles"></a><span data-ttu-id="c597b-136">Perfiles de registro</span><span class="sxs-lookup"><span data-stu-id="c597b-136">Log profiles</span></span>
<span data-ttu-id="c597b-137">Utilice la información de esta sección para usar perfiles de registro.</span><span class="sxs-lookup"><span data-stu-id="c597b-137">Use the information in this section to work with log profiles.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="c597b-138">Obtención de un perfil de registro</span><span class="sxs-lookup"><span data-stu-id="c597b-138">Get a log profile</span></span>
```console
azure insights logprofile list
azure insights logprofile get -n default
```


### <a name="add-a-log-profile-without-retention"></a><span data-ttu-id="c597b-139">Adición de un perfil de registro sin retención de datos</span><span class="sxs-lookup"><span data-stu-id="c597b-139">Add a log profile without retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="c597b-140">Eliminación de un perfil de registro</span><span class="sxs-lookup"><span data-stu-id="c597b-140">Remove a log profile</span></span>
```console
azure insights logprofile delete --name default
```

### <a name="add-a-log-profile-with-retention"></a><span data-ttu-id="c597b-141">Adición de un perfil de registro con retención de datos</span><span class="sxs-lookup"><span data-stu-id="c597b-141">Add a log profile with retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```

### <a name="add-a-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="c597b-142">Adición de un perfil de registro con retención y EventHub</span><span class="sxs-lookup"><span data-stu-id="c597b-142">Add a log profile with retention and EventHub</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --serviceBusRuleId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/testshoeboxeastus/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```


## <a name="diagnostics"></a><span data-ttu-id="c597b-143">Diagnóstico</span><span class="sxs-lookup"><span data-stu-id="c597b-143">Diagnostics</span></span>
<span data-ttu-id="c597b-144">Utilice la información de esta sección para usar la configuración de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="c597b-144">Use the information in this section to work with diagnostic settings.</span></span>

### <a name="get-a-diagnostic-setting"></a><span data-ttu-id="c597b-145">Obtención de la configuración de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="c597b-145">Get a diagnostic setting</span></span>
```console
azure insights diagnostic get --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp
```

### <a name="disable-a-diagnostic-setting"></a><span data-ttu-id="c597b-146">Deshabilitación de la configuración de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="c597b-146">Disable a diagnostic setting</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled false
```

### <a name="enable-a-diagnostic-setting-without-retention"></a><span data-ttu-id="c597b-147">Habilitación de la configuración de diagnóstico sin retención</span><span class="sxs-lookup"><span data-stu-id="c597b-147">Enable a diagnostic setting without retention</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled true
```


## <a name="autoscale"></a><span data-ttu-id="c597b-148">Autoscale</span><span class="sxs-lookup"><span data-stu-id="c597b-148">Autoscale</span></span>
<span data-ttu-id="c597b-149">Utilice la información de esta sección para usar la configuración de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="c597b-149">Use the information in this section to work with autoscale settings.</span></span> <span data-ttu-id="c597b-150">Tendrá que modificar estos ejemplos.</span><span class="sxs-lookup"><span data-stu-id="c597b-150">You need to modify these examples.</span></span>

### <a name="get-autoscale-settings-for-a-resource-group"></a><span data-ttu-id="c597b-151">Obtención de la configuración de escalado automático de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="c597b-151">Get autoscale settings for a resource group</span></span>
```console
azure insights autoscale setting list montest2
```

### <a name="get-autoscale-settings-by-name-in-a-resource-group"></a><span data-ttu-id="c597b-152">Obtención de valores de escalado automático por su nombre en un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="c597b-152">Get autoscale settings by name in a resource group</span></span>
```console
azure insights autoscale setting list montest2 -n setting2
```


### <a name="set-auotoscale-settings"></a><span data-ttu-id="c597b-153">Establecimiento de la configuración de escalado automático</span><span class="sxs-lookup"><span data-stu-id="c597b-153">Set auotoscale settings</span></span>
```console
azure insights autoscale setting set montest2 -n setting2 --settingSpec
```
