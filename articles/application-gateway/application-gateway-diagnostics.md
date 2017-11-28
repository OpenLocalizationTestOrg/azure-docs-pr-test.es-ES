---
title: "aaaMonitor obtener acceso a los registros, registros de rendimiento, estado de back-end y las métricas de puerta de enlace de aplicaciones | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooenable y administrar los registros de acceso y registros de rendimiento para la puerta de enlace de aplicaciones"
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: tysonn
tags: azure-resource-manager
ms.assetid: 300628b8-8e3d-40ab-b294-3ecc5e48ef98
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: amitsriva
ms.openlocfilehash: 36ebf15c28f776158350ef8e73d617ef68e09266
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="back-end-health-diagnostic-logs-and-metrics-for-application-gateway"></a><span data-ttu-id="565b2-103">Mantenimiento del back-end, registro de diagnóstico y métricas de Application Gateway</span><span class="sxs-lookup"><span data-stu-id="565b2-103">Back-end health, diagnostic logs, and metrics for Application Gateway</span></span>

<span data-ttu-id="565b2-104">Mediante el uso de puerta de enlace de aplicaciones de Azure, puede supervisar los recursos en hello siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="565b2-104">By using Azure Application Gateway, you can monitor resources in hello following ways:</span></span>

* <span data-ttu-id="565b2-105">[Estado de back-end](#back-end-health): puerta de enlace de aplicaciones proporciona mantenimiento de hello capacidad toomonitor Hola de servidores de Hola Hola grupos de back-end a través de hello portal de Azure y a través de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="565b2-105">[Back-end health](#back-end-health): Application Gateway provides hello capability toomonitor hello health of hello servers in hello back-end pools through hello Azure portal and through PowerShell.</span></span> <span data-ttu-id="565b2-106">También puede encontrar el estado de Hola de grupos de back-end de Hola a través de los registros de diagnóstico de rendimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="565b2-106">You can also find hello health of hello back-end pools through hello performance diagnostic logs.</span></span>

* <span data-ttu-id="565b2-107">[Registros](#diagnostic-logs): los registros permiten para el rendimiento, acceso, y otro datos toobe guarda o consumidos de un recurso con fines de supervisión.</span><span class="sxs-lookup"><span data-stu-id="565b2-107">[Logs](#diagnostic-logs): Logs allow for performance, access, and other data toobe saved or consumed from a resource for monitoring purposes.</span></span>

* <span data-ttu-id="565b2-108">[Métricas](#metrics): en estos momentos, Application Gateway tiene una métrica.</span><span class="sxs-lookup"><span data-stu-id="565b2-108">[Metrics](#metrics): Application Gateway currently has one metric.</span></span> <span data-ttu-id="565b2-109">Esta métrica mide el rendimiento de Hola de puerta de enlace de aplicaciones de hello en bytes por segundo.</span><span class="sxs-lookup"><span data-stu-id="565b2-109">This metric measures hello throughput of hello application gateway in bytes per second.</span></span>

## <a name="back-end-health"></a><span data-ttu-id="565b2-110">Mantenimiento del back-end</span><span class="sxs-lookup"><span data-stu-id="565b2-110">Back-end health</span></span>

<span data-ttu-id="565b2-111">Puerta de enlace de aplicaciones proporciona mantenimiento de hello capacidad toomonitor Hola de miembros individuales de grupos de back-end de Hola a través del portal hello, PowerShell y Hola interfaz de línea de comandos (CLI).</span><span class="sxs-lookup"><span data-stu-id="565b2-111">Application Gateway provides hello capability toomonitor hello health of individual members of hello back-end pools through hello portal, PowerShell, and hello command-line interface (CLI).</span></span> <span data-ttu-id="565b2-112">También puede encontrar un estado agregado resumen de grupos de back-end a través de los registros de diagnóstico de rendimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="565b2-112">You can also find an aggregated health summary of back-end pools through hello performance diagnostic logs.</span></span> 

<span data-ttu-id="565b2-113">informe de mantenimiento de back-end de Hello refleja la salida de hello de instancias de hello Application Gateway mantenimiento sondeo toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="565b2-113">hello back-end health report reflects hello output of hello Application Gateway health probe toohello back-end instances.</span></span> <span data-ttu-id="565b2-114">Cuando el sondeo se realiza correctamente y Hola volver final puede recibir tráfico, se considera correcta.</span><span class="sxs-lookup"><span data-stu-id="565b2-114">When probing is successful and hello back end can receive traffic, it's considered healthy.</span></span> <span data-ttu-id="565b2-115">En caso contrario, se considera incorrecto.</span><span class="sxs-lookup"><span data-stu-id="565b2-115">Otherwise, it's considered unhealthy.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="565b2-116">Si hay un grupo de seguridad de red (NSG) en una subred de puerta de enlace de aplicaciones, abra 65503 65534 de intervalos de puertos de subred de puerta de enlace de aplicación hello para el tráfico entrante.</span><span class="sxs-lookup"><span data-stu-id="565b2-116">If there is a network security group (NSG) on an Application Gateway subnet, open port ranges 65503-65534 on hello Application Gateway subnet for inbound traffic.</span></span> <span data-ttu-id="565b2-117">Estos puertos son necesarios para toowork de API de hello estado back-end.</span><span class="sxs-lookup"><span data-stu-id="565b2-117">These ports are required for hello back-end health API toowork.</span></span>


### <a name="view-back-end-health-through-hello-portal"></a><span data-ttu-id="565b2-118">Ver el estado de back-end a través del portal de Hola</span><span class="sxs-lookup"><span data-stu-id="565b2-118">View back-end health through hello portal</span></span>

<span data-ttu-id="565b2-119">En el portal de hello, mantenimiento de back-end se proporciona automáticamente.</span><span class="sxs-lookup"><span data-stu-id="565b2-119">In hello portal, back-end health is provided automatically.</span></span> <span data-ttu-id="565b2-120">En una puerta de enlace de aplicaciones existente, vaya a **Supervisión** > **Estado del back-end**.</span><span class="sxs-lookup"><span data-stu-id="565b2-120">In an existing application gateway, select **Monitoring** > **Backend health**.</span></span> 

<span data-ttu-id="565b2-121">Cada miembro del grupo de back-end de Hola se muestra en esta página (ya sea una NIC, IP o FQDN).</span><span class="sxs-lookup"><span data-stu-id="565b2-121">Each member in hello back-end pool is listed on this page (whether it's a NIC, IP, or FQDN).</span></span> <span data-ttu-id="565b2-122">Se muestran el nombre del grupo de back-end, el puerto, la configuración HTTP del back-end y el estado de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="565b2-122">Back-end pool name, port, back-end HTTP settings name, and health status are shown.</span></span> <span data-ttu-id="565b2-123">Los valores válidos para el estado de mantenimiento son **Correcto**, **Incorrecto** y **Desconocido**.</span><span class="sxs-lookup"><span data-stu-id="565b2-123">Valid values for health status are **Healthy**, **Unhealthy**, and **Unknown**.</span></span>

> [!NOTE]
> <span data-ttu-id="565b2-124">Si ve un estado de mantenimiento de back-end de **desconocido**, asegúrese de que ese acceso toohello back-end no está bloqueada por una regla de NSG, una ruta definida por el usuario (UDR) o un DNS personalizado en la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="565b2-124">If you see a back-end health status of **Unknown**, ensure that access toohello back end is not blocked by an NSG rule, a user-defined route (UDR), or a custom DNS in hello virtual network.</span></span>

![Mantenimiento del back-end][10]

### <a name="view-back-end-health-through-powershell"></a><span data-ttu-id="565b2-126">Visualización del mantenimiento del back-end mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="565b2-126">View back-end health through PowerShell</span></span>

<span data-ttu-id="565b2-127">Hola siguiente código de PowerShell muestra cómo tooview mantenimiento de back-end mediante el uso de Hola `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="565b2-127">hello following PowerShell code shows how tooview back-end health by using hello `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:</span></span>

```powershell
Get-AzureRmApplicationGatewayBackendHealth -Name ApplicationGateway1 -ResourceGroupName Contoso
```

### <a name="view-back-end-health-through-azure-cli-20"></a><span data-ttu-id="565b2-128">Visualización del mantenimiento del back-end mediante la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="565b2-128">View back-end health through Azure CLI 2.0</span></span>

```azurecli
az network application-gateway show-backend-health --resource-group AdatumAppGatewayRG --name AdatumAppGateway
```

### <a name="results"></a><span data-ttu-id="565b2-129">Results</span><span class="sxs-lookup"><span data-stu-id="565b2-129">Results</span></span>

<span data-ttu-id="565b2-130">Hola siguiente fragmento de código muestra un ejemplo de respuesta de hello:</span><span class="sxs-lookup"><span data-stu-id="565b2-130">hello following snippet shows an example of hello response:</span></span>

```json
{
"BackendAddressPool": {
    "Id": "/subscriptions/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/appGatewayBackendPool"
},
"BackendHttpSettingsCollection": [
    {
    "BackendHttpSettings": {
        "Id": "/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings"
    },
    "Servers": [
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        },
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        }
    ]
    }
]
}
```

## <span data-ttu-id="565b2-131"><a name="diagnostic-logging"></a>Registros de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="565b2-131"><a name="diagnostic-logging"></a>Diagnostic logs</span></span>

<span data-ttu-id="565b2-132">Puede usar varios tipos de registros de Azure toomanage y solucionar problemas de las puertas de enlace de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="565b2-132">You can use different types of logs in Azure toomanage and troubleshoot application gateways.</span></span> <span data-ttu-id="565b2-133">Puede tener acceso a algunos de estos registros a través del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="565b2-133">You can access some of these logs through hello portal.</span></span> <span data-ttu-id="565b2-134">Se pueden extraer todos los registros de Azure Blob Storage y visualizarse en distintas herramientas, como [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel y PowerBI.</span><span class="sxs-lookup"><span data-stu-id="565b2-134">All logs can be extracted from Azure Blob storage and viewed in different tools, such as [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel, and Power BI.</span></span> <span data-ttu-id="565b2-135">Puede aprender más sobre Hola diferentes tipos de registros de hello lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="565b2-135">You can learn more about hello different types of logs from hello following list:</span></span>

* <span data-ttu-id="565b2-136">**Registro de actividad**: puede usar [registros de actividad de Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (anteriormente conocidos como registros operativos y los registros de auditoría) tooview todas las operaciones que son envían tooyour suscripción de Azure y su estado.</span><span class="sxs-lookup"><span data-stu-id="565b2-136">**Activity log**: You can use [Azure activity logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as operational logs and audit logs) tooview all operations that are submitted tooyour Azure subscription, and their status.</span></span> <span data-ttu-id="565b2-137">Las entradas del registro de actividades se recopilan de forma predeterminada, y puede verlos en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="565b2-137">Activity log entries are collected by default, and you can view them in hello Azure portal.</span></span>
* <span data-ttu-id="565b2-138">**Registro de acceso**: puede usar esta patrones de acceso de registro tooview puerta de enlace de aplicación y analizar información importante, incluyendo llamador Hola IP, dirección URL solicitada, latencia de la respuesta, código de retorno y los bytes de entrada y salida. El registro de acceso se recopila cada 300 segundos.</span><span class="sxs-lookup"><span data-stu-id="565b2-138">**Access log**: You can use this log tooview Application Gateway access patterns and analyze important information, including hello caller's IP, requested URL, response latency, return code, and bytes in and out. An access log is collected every 300 seconds.</span></span> <span data-ttu-id="565b2-139">Este registro contiene un registro por cada instancia de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="565b2-139">This log contains one record per instance of Application Gateway.</span></span> <span data-ttu-id="565b2-140">instancia de puerta de enlace de aplicación Hola puede identificarse por la propiedad instanceId de Hola.</span><span class="sxs-lookup"><span data-stu-id="565b2-140">hello Application Gateway instance can be identified by hello instanceId property.</span></span>
* <span data-ttu-id="565b2-141">**Registro de rendimiento**: puede usar esta tooview de registro que el rendimiento de las instancias de puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="565b2-141">**Performance log**: You can use this log tooview how Application Gateway instances are performing.</span></span> <span data-ttu-id="565b2-142">Este registro captura la información de rendimiento de cada instancia, incluida la cantidad total de solicitudes atendidas, el rendimiento en bytes, la cantidad de solicitudes con error y el número de instancias de back-end con un mantenimiento correcto o incorrecto.</span><span class="sxs-lookup"><span data-stu-id="565b2-142">This log captures performance information for each instance, including total requests served, throughput in bytes, total requests served, failed request count, and healthy and unhealthy back-end instance count.</span></span> <span data-ttu-id="565b2-143">El registro de rendimiento se recopila cada 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="565b2-143">A performance log is collected every 60 seconds.</span></span>
* <span data-ttu-id="565b2-144">**Registro de Firewall**: puede usar este registro de solicitudes de Hola de tooview que se registra con el modo de detección o prevención de una puerta de enlace de la aplicación que está configurado con el servidor de aplicaciones web de Hola.</span><span class="sxs-lookup"><span data-stu-id="565b2-144">**Firewall log**: You can use this log tooview hello requests that are logged through either detection or prevention mode of an application gateway that is configured with hello web application firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="565b2-145">Registros solo están disponibles para los recursos implementados en el modelo de implementación de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="565b2-145">Logs are available only for resources deployed in hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="565b2-146">No puede usar registros de recursos en el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="565b2-146">You cannot use logs for resources in hello classic deployment model.</span></span> <span data-ttu-id="565b2-147">Para entender mejor de los modelos de hello dos, vea hello [Administrador de recursos de la descripción y la implementación clásica](../azure-resource-manager/resource-manager-deployment-model.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="565b2-147">For a better understanding of hello two models, see hello [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="565b2-148">Tiene tres opciones para almacenar los archivos de registro:</span><span class="sxs-lookup"><span data-stu-id="565b2-148">You have three options for storing your logs:</span></span>

* <span data-ttu-id="565b2-149">**Cuenta de almacenamiento**: cuentas que resultan especialmente útiles para registros cuando estos se almacenan durante mucho tiempo y se revisan cuando es necesario.</span><span class="sxs-lookup"><span data-stu-id="565b2-149">**Storage account**: Storage accounts are best used for logs when logs are stored for a longer duration and reviewed when needed.</span></span>
* <span data-ttu-id="565b2-150">**Los concentradores de eventos**: concentradores de eventos son una buena opción para la integración con otra información de seguridad y tooget alertas en los recursos de las herramientas de administración de eventos (SEIM).</span><span class="sxs-lookup"><span data-stu-id="565b2-150">**Event hubs**: Event hubs are a great option for integrating with other security information and event management (SEIM) tools tooget alerts on your resources.</span></span>
* <span data-ttu-id="565b2-151">**Log Analytics**: se usa para la supervisión general en tiempo real de la aplicación o para examinar las tendencias.</span><span class="sxs-lookup"><span data-stu-id="565b2-151">**Log Analytics**: Log Analytics is best used for general real-time monitoring of your application or looking at trends.</span></span>

### <a name="enable-logging-through-powershell"></a><span data-ttu-id="565b2-152">Habilitación del registro con PowerShell</span><span class="sxs-lookup"><span data-stu-id="565b2-152">Enable logging through PowerShell</span></span>

<span data-ttu-id="565b2-153">El registro de actividades se habilita automáticamente para todos los recursos de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="565b2-153">Activity logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="565b2-154">Debe habilitar el acceso y toostart de registro de rendimiento recolección de datos de hello disponibles a través de esos registros.</span><span class="sxs-lookup"><span data-stu-id="565b2-154">You must enable access and performance logging toostart collecting hello data available through those logs.</span></span> <span data-ttu-id="565b2-155">tooenable registro Hola uso pasos:</span><span class="sxs-lookup"><span data-stu-id="565b2-155">tooenable logging, use hello following steps:</span></span>

1. <span data-ttu-id="565b2-156">Tenga en cuenta los identificadores de recursos de su cuenta de almacenamiento, donde se almacenan los datos de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="565b2-156">Note your storage account's resource ID, where hello log data is stored.</span></span> <span data-ttu-id="565b2-157">Este valor es del formulario de hello: / Subscriptions /\<subscriptionId\>/ResourceGroups /\<nombre del grupo de recursos\>/providers/Microsoft.Storage/storageAccounts/\<denombredelacuentadealmacenamiento\>.</span><span class="sxs-lookup"><span data-stu-id="565b2-157">This value is of hello form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Storage/storageAccounts/\<storage account name\>.</span></span> <span data-ttu-id="565b2-158">Puede usar cualquier cuenta de almacenamiento de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="565b2-158">You can use any storage account in your subscription.</span></span> <span data-ttu-id="565b2-159">Hola toofind portal Azure puede usar esta información.</span><span class="sxs-lookup"><span data-stu-id="565b2-159">You can use hello Azure portal toofind this information.</span></span>

    ![Portal: identificador de recurso de la cuenta de almacenamiento](./media/application-gateway-diagnostics/diagnostics1.png)

2. <span data-ttu-id="565b2-161">Observe el identificador de recurso de la puerta de enlace de aplicaciones para la que se está habilitando el registro.</span><span class="sxs-lookup"><span data-stu-id="565b2-161">Note your application gateway's resource ID for which logging is enabled.</span></span> <span data-ttu-id="565b2-162">Este valor es del formulario de hello: / Subscriptions /\<subscriptionId\>/ResourceGroups /\<nombre del grupo de recursos\>/providers/Microsoft.Network/applicationGateways/\<puerta de enlace de aplicaciones nombre\>.</span><span class="sxs-lookup"><span data-stu-id="565b2-162">This value is of hello form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Network/applicationGateways/\<application gateway name\>.</span></span> <span data-ttu-id="565b2-163">Puede utilizar Hola portal toofind esta información.</span><span class="sxs-lookup"><span data-stu-id="565b2-163">You can use hello portal toofind this information.</span></span>

    ![Portal: identificador de recurso de la puerta de enlace de aplicaciones](./media/application-gateway-diagnostics/diagnostics2.png)

3. <span data-ttu-id="565b2-165">Habilitar el registro de diagnóstico utilizando Hola siguiente cmdlet de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="565b2-165">Enable diagnostic logging by using hello following PowerShell cmdlet:</span></span>

    ```powershell
    Set-AzureRmDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name> -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> -Enabled $true     
    ```
    
> [!TIP] 
><span data-ttu-id="565b2-166">Los registros de actividades no requieren una cuenta de almacenamiento separada.</span><span class="sxs-lookup"><span data-stu-id="565b2-166">Activity logs do not require a separate storage account.</span></span> <span data-ttu-id="565b2-167">uso de Hola de almacenamiento para el acceso y el registro de rendimiento incurre en cargos por servicio.</span><span class="sxs-lookup"><span data-stu-id="565b2-167">hello use of storage for access and performance logging incurs service charges.</span></span>

### <a name="enable-logging-through-hello-azure-portal"></a><span data-ttu-id="565b2-168">Habilitar el registro a través de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="565b2-168">Enable logging through hello Azure portal</span></span>

1. <span data-ttu-id="565b2-169">En Hola portal de Azure, busque el recurso y haga clic en **registros de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="565b2-169">In hello Azure portal, find your resource and click **Diagnostic logs**.</span></span>

   <span data-ttu-id="565b2-170">Hay tres registros de auditoría disponibles para Application Gateway:</span><span class="sxs-lookup"><span data-stu-id="565b2-170">For Application Gateway, three logs are available:</span></span>

   * <span data-ttu-id="565b2-171">Registro de acceso</span><span class="sxs-lookup"><span data-stu-id="565b2-171">Access log</span></span>
   * <span data-ttu-id="565b2-172">Registro de rendimiento</span><span class="sxs-lookup"><span data-stu-id="565b2-172">Performance log</span></span>
   * <span data-ttu-id="565b2-173">Registro de firewall</span><span class="sxs-lookup"><span data-stu-id="565b2-173">Firewall log</span></span>

2. <span data-ttu-id="565b2-174">recopilar datos de toostart, haga clic en **Activar diagnósticos**.</span><span class="sxs-lookup"><span data-stu-id="565b2-174">toostart collecting data, click **Turn on diagnostics**.</span></span>

   ![Activación de los diagnósticos][1]

3. <span data-ttu-id="565b2-176">Hola **configuración de diagnóstico** hoja proporciona una configuración de Hola para hello registros de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="565b2-176">hello **Diagnostics settings** blade provides hello settings for hello diagnostic logs.</span></span> <span data-ttu-id="565b2-177">En este ejemplo, análisis de registros almacena los registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="565b2-177">In this example, Log Analytics stores hello logs.</span></span> <span data-ttu-id="565b2-178">Haga clic en **configurar** en **análisis de registros** tooconfigure el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="565b2-178">Click **Configure** under **Log Analytics** tooconfigure your workspace.</span></span> <span data-ttu-id="565b2-179">También puede utilizar un registros de diagnóstico de Hola de almacenamiento cuenta toosave y centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="565b2-179">You can also use event hubs and a storage account toosave hello diagnostic logs.</span></span>

   ![Iniciar el proceso de configuración Hola][2]

4. <span data-ttu-id="565b2-181">En Operations Management Suite (OMS), elija un área de trabajo existente o cree uno.</span><span class="sxs-lookup"><span data-stu-id="565b2-181">Choose an existing Operations Management Suite (OMS) workspace or create a new one.</span></span> <span data-ttu-id="565b2-182">Este ejemplo utiliza una existente.</span><span class="sxs-lookup"><span data-stu-id="565b2-182">This example uses an existing one.</span></span>

   ![Opciones para áreas de trabajo OMS][3]

5. <span data-ttu-id="565b2-184">Confirmar configuración de Hola y haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="565b2-184">Confirm hello settings and click **Save**.</span></span>

   ![Hoja de configuración de diagnóstico con selecciones][4]

### <a name="activity-log"></a><span data-ttu-id="565b2-186">Registro de actividades</span><span class="sxs-lookup"><span data-stu-id="565b2-186">Activity log</span></span>

<span data-ttu-id="565b2-187">Azure genera el registro de actividad de Hola de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="565b2-187">Azure generates hello activity log by default.</span></span> <span data-ttu-id="565b2-188">Hola registros se conservan durante 90 días en almacén de hello Azure registros de eventos.</span><span class="sxs-lookup"><span data-stu-id="565b2-188">hello logs are preserved for 90 days in hello Azure event logs store.</span></span> <span data-ttu-id="565b2-189">Obtener más información sobre estos registros leyendo hello [ver eventos y registros de actividad](../monitoring-and-diagnostics/insights-debugging-with-events.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="565b2-189">Learn more about these logs by reading hello [View events and activity log](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

### <a name="access-log"></a><span data-ttu-id="565b2-190">Registro de acceso</span><span class="sxs-lookup"><span data-stu-id="565b2-190">Access log</span></span>

<span data-ttu-id="565b2-191">registro de acceso de Hola se genera solo si se ha habilitado en cada instancia de puerta de enlace de aplicaciones, como se detalla en hello pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="565b2-191">hello access log is generated only if you've enabled it on each Application Gateway instance, as detailed in hello preceding steps.</span></span> <span data-ttu-id="565b2-192">Hola datos se almacenan en la cuenta de almacenamiento de Hola que especificó cuando se habilitó el registro de hello.</span><span class="sxs-lookup"><span data-stu-id="565b2-192">hello data is stored in hello storage account that you specified when you enabled hello logging.</span></span> <span data-ttu-id="565b2-193">Cada acceso de puerta de enlace de aplicaciones se registra en formato JSON, tal y como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="565b2-193">Each access of Application Gateway is logged in JSON format, as shown in hello following example:</span></span>


|<span data-ttu-id="565b2-194">Valor</span><span class="sxs-lookup"><span data-stu-id="565b2-194">Value</span></span>  |<span data-ttu-id="565b2-195">Descripción</span><span class="sxs-lookup"><span data-stu-id="565b2-195">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="565b2-196">instanceId</span><span class="sxs-lookup"><span data-stu-id="565b2-196">instanceId</span></span>     | <span data-ttu-id="565b2-197">Esa solicitud Hola atienden la instancia de puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="565b2-197">Application Gateway instance that served hello request.</span></span>        |
|<span data-ttu-id="565b2-198">clientIP</span><span class="sxs-lookup"><span data-stu-id="565b2-198">clientIP</span></span>     | <span data-ttu-id="565b2-199">IP de origen para la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="565b2-199">Originating IP for hello request.</span></span>        |
|<span data-ttu-id="565b2-200">clientPort</span><span class="sxs-lookup"><span data-stu-id="565b2-200">clientPort</span></span>     | <span data-ttu-id="565b2-201">Puerto de solicitud de Hola de origen.</span><span class="sxs-lookup"><span data-stu-id="565b2-201">Originating port for hello request.</span></span>       |
|<span data-ttu-id="565b2-202">httpMethod</span><span class="sxs-lookup"><span data-stu-id="565b2-202">httpMethod</span></span>     | <span data-ttu-id="565b2-203">Método HTTP utilizado por solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="565b2-203">HTTP method used by hello request.</span></span>       |
|<span data-ttu-id="565b2-204">requestUri</span><span class="sxs-lookup"><span data-stu-id="565b2-204">requestUri</span></span>     | <span data-ttu-id="565b2-205">URI de solicitud recibido Hola.</span><span class="sxs-lookup"><span data-stu-id="565b2-205">URI of hello received request.</span></span>        |
|<span data-ttu-id="565b2-206">RequestQuery</span><span class="sxs-lookup"><span data-stu-id="565b2-206">RequestQuery</span></span>     | <span data-ttu-id="565b2-207">**Server enrutara**: instancia de grupo Back-end que se envió la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="565b2-207">**Server-Routed**: Back-end pool instance that was sent hello request.</span></span> </br> <span data-ttu-id="565b2-208">**X-AzureApplicationGateway-registro-ID**: Id. de correlación usado para solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="565b2-208">**X-AzureApplicationGateway-LOG-ID**: Correlation ID used for hello request.</span></span> <span data-ttu-id="565b2-209">Puede ser problemas de tráfico de tootroubleshoot usadas en servidores de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="565b2-209">It can be used tootroubleshoot traffic issues on hello back-end servers.</span></span> </br><span data-ttu-id="565b2-210">**ESTADO del servidor**: código de respuesta HTTP que recibe de puerta de enlace de aplicaciones de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="565b2-210">**SERVER-STATUS**: HTTP response code that Application Gateway received from hello back end.</span></span>       |
|<span data-ttu-id="565b2-211">UserAgent</span><span class="sxs-lookup"><span data-stu-id="565b2-211">UserAgent</span></span>     | <span data-ttu-id="565b2-212">Agente de usuario Hola HTTP del encabezado de solicitud.</span><span class="sxs-lookup"><span data-stu-id="565b2-212">User agent from hello HTTP request header.</span></span>        |
|<span data-ttu-id="565b2-213">httpStatus</span><span class="sxs-lookup"><span data-stu-id="565b2-213">httpStatus</span></span>     | <span data-ttu-id="565b2-214">Código de estado HTTP devuelto toohello cliente de puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="565b2-214">HTTP status code returned toohello client from Application Gateway.</span></span>       |
|<span data-ttu-id="565b2-215">HttpVersion</span><span class="sxs-lookup"><span data-stu-id="565b2-215">httpVersion</span></span>     | <span data-ttu-id="565b2-216">Versión HTTP de solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="565b2-216">HTTP version of hello request.</span></span>        |
|<span data-ttu-id="565b2-217">receivedBytes</span><span class="sxs-lookup"><span data-stu-id="565b2-217">receivedBytes</span></span>     | <span data-ttu-id="565b2-218">Tamaño de paquete recibido, en bytes.</span><span class="sxs-lookup"><span data-stu-id="565b2-218">Size of packet received, in bytes.</span></span>        |
|<span data-ttu-id="565b2-219">sentBytes</span><span class="sxs-lookup"><span data-stu-id="565b2-219">sentBytes</span></span>| <span data-ttu-id="565b2-220">Tamaño de paquete enviado, en bytes.</span><span class="sxs-lookup"><span data-stu-id="565b2-220">Size of packet sent, in bytes.</span></span>|
|<span data-ttu-id="565b2-221">timeTaken</span><span class="sxs-lookup"><span data-stu-id="565b2-221">timeTaken</span></span>| <span data-ttu-id="565b2-222">Período de tiempo (en milisegundos) que se tarda en un toobe solicitud procesados y su toobe de respuesta enviados.</span><span class="sxs-lookup"><span data-stu-id="565b2-222">Length of time (in milliseconds) that it takes for a request toobe processed and its response toobe sent.</span></span> <span data-ttu-id="565b2-223">Esto se calcula como el intervalo de saludo de tiempo de hello cuando la puerta de enlace de aplicación recibe el primer byte de una hora de toohello de solicitud HTTP respuesta Hola enviar operación finalice Hola.</span><span class="sxs-lookup"><span data-stu-id="565b2-223">This is calculated as hello interval from hello time when Application Gateway receives hello first byte of an HTTP request toohello time when hello response send operation finishes.</span></span> <span data-ttu-id="565b2-224">Es importante toonote que Hola campo Time-Taken normalmente incluye el tiempo de Hola que viajan a través de red de hello paquetes de saludo de solicitud y respuesta.</span><span class="sxs-lookup"><span data-stu-id="565b2-224">It's important toonote that hello Time-Taken field usually includes hello time that hello request and response packets are traveling over hello network.</span></span> |
|<span data-ttu-id="565b2-225">sslEnabled</span><span class="sxs-lookup"><span data-stu-id="565b2-225">sslEnabled</span></span>| <span data-ttu-id="565b2-226">Indica si los grupos de back-end de comunicación toohello utilizan SSL.</span><span class="sxs-lookup"><span data-stu-id="565b2-226">Whether communication toohello back-end pools used SSL.</span></span> <span data-ttu-id="565b2-227">Los valores válidos son on y off.</span><span class="sxs-lookup"><span data-stu-id="565b2-227">Valid values are on and off.</span></span>|
```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/PEERINGTEST/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayAccess",
    "time": "2017-04-26T19:27:38Z",
    "category": "ApplicationGatewayAccessLog",
    "properties": {
        "instanceId": "ApplicationGatewayRole_IN_0",
        "clientIP": "191.96.249.97",
        "clientPort": 46886,
        "httpMethod": "GET",
        "requestUri": "/phpmyadmin/scripts/setup.php",
        "requestQuery": "X-AzureApplicationGateway-CACHE-HIT=0&SERVER-ROUTED=10.4.0.4&X-AzureApplicationGateway-LOG-ID=874f1f0f-6807-41c9-b7bc-f3cfa74aa0b1&SERVER-STATUS=404",
        "userAgent": "-",
        "httpStatus": 404,
        "httpVersion": "HTTP/1.0",
        "receivedBytes": 65,
        "sentBytes": 553,
        "timeTaken": 205,
        "sslEnabled": "off"
    }
}
```

### <a name="performance-log"></a><span data-ttu-id="565b2-228">Registro de rendimiento</span><span class="sxs-lookup"><span data-stu-id="565b2-228">Performance log</span></span>

<span data-ttu-id="565b2-229">registro de rendimiento de Hola se genera solo si se ha habilitado en cada instancia de puerta de enlace de aplicaciones, como se detalla en hello pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="565b2-229">hello performance log is generated only if you have enabled it on each Application Gateway instance, as detailed in hello preceding steps.</span></span> <span data-ttu-id="565b2-230">Hola datos se almacenan en la cuenta de almacenamiento de Hola que especificó cuando se habilitó el registro de hello.</span><span class="sxs-lookup"><span data-stu-id="565b2-230">hello data is stored in hello storage account that you specified when you enabled hello logging.</span></span> <span data-ttu-id="565b2-231">datos de registro de rendimiento de saludo se generan en intervalos de 1 minuto.</span><span class="sxs-lookup"><span data-stu-id="565b2-231">hello performance log data is generated in 1-minute intervals.</span></span> <span data-ttu-id="565b2-232">se registra Hola datos siguientes:</span><span class="sxs-lookup"><span data-stu-id="565b2-232">hello following data is logged:</span></span>


|<span data-ttu-id="565b2-233">Valor</span><span class="sxs-lookup"><span data-stu-id="565b2-233">Value</span></span>  |<span data-ttu-id="565b2-234">Descripción</span><span class="sxs-lookup"><span data-stu-id="565b2-234">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="565b2-235">instanceId</span><span class="sxs-lookup"><span data-stu-id="565b2-235">instanceId</span></span>     |  <span data-ttu-id="565b2-236">Instancia de Application Gateway para la que se van a generar los datos.</span><span class="sxs-lookup"><span data-stu-id="565b2-236">Application Gateway instance for which performance data is being generated.</span></span> <span data-ttu-id="565b2-237">Si hay varias instancias de Application Gateway, hay una fila por cada instancia.</span><span class="sxs-lookup"><span data-stu-id="565b2-237">For a multiple-instance application gateway, there is one row per instance.</span></span>        |
|<span data-ttu-id="565b2-238">healthyHostCount</span><span class="sxs-lookup"><span data-stu-id="565b2-238">healthyHostCount</span></span>     | <span data-ttu-id="565b2-239">Número de hosts correcto en el grupo de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="565b2-239">Number of healthy hosts in hello back-end pool.</span></span>        |
|<span data-ttu-id="565b2-240">unHealthyHostCount</span><span class="sxs-lookup"><span data-stu-id="565b2-240">unHealthyHostCount</span></span>     | <span data-ttu-id="565b2-241">Número de hosts en mal estado en el grupo de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="565b2-241">Number of unhealthy hosts in hello back-end pool.</span></span>        |
|<span data-ttu-id="565b2-242">requestCount</span><span class="sxs-lookup"><span data-stu-id="565b2-242">requestCount</span></span>     | <span data-ttu-id="565b2-243">Número de solicitudes atendidas.</span><span class="sxs-lookup"><span data-stu-id="565b2-243">Number of requests served.</span></span>        |
|<span data-ttu-id="565b2-244">latency</span><span class="sxs-lookup"><span data-stu-id="565b2-244">latency</span></span> | <span data-ttu-id="565b2-245">Latencia (en milisegundos) de las solicitudes de hello instancia toohello back-end que atiende solicitudes de Hola.</span><span class="sxs-lookup"><span data-stu-id="565b2-245">Latency (in milliseconds) of requests from hello instance toohello back end that serves hello requests.</span></span> |
|<span data-ttu-id="565b2-246">failedRequestCount</span><span class="sxs-lookup"><span data-stu-id="565b2-246">failedRequestCount</span></span>| <span data-ttu-id="565b2-247">Número de solicitudes con error.</span><span class="sxs-lookup"><span data-stu-id="565b2-247">Number of failed requests.</span></span>|
|<span data-ttu-id="565b2-248">throughput</span><span class="sxs-lookup"><span data-stu-id="565b2-248">throughput</span></span>| <span data-ttu-id="565b2-249">Rendimiento medio desde el último registro de hello, medido en bytes por segundo.</span><span class="sxs-lookup"><span data-stu-id="565b2-249">Average throughput since hello last log, measured in bytes per second.</span></span>|

```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayPerformance",
    "time": "2016-04-09T00:00:00Z",
    "category": "ApplicationGatewayPerformanceLog",
    "properties":
    {
        "instanceId":"ApplicationGatewayRole_IN_1",
        "healthyHostCount":"4",
        "unHealthyHostCount":"0",
        "requestCount":"185",
        "latency":"0",
        "failedRequestCount":"0",
        "throughput":"119427"
    }
}
```

> [!NOTE]
> <span data-ttu-id="565b2-250">Latencia se calcula a partir de la hora de hello cuando el primer byte de la solicitud HTTP de Hola Hola es tiempo toohello recibidos cuando se envía el último byte de respuesta HTTP Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="565b2-250">Latency is calculated from hello time when hello first byte of hello HTTP request is received toohello time when hello last byte of hello HTTP response is sent.</span></span> <span data-ttu-id="565b2-251">Suma del Hola su de Hola tiempo de procesamiento de puerta de enlace de aplicaciones más hello toohello de costo de red nuevo finalizar, más tiempo de Hola que Hola back-end toma tooprocess Hola solicitud.</span><span class="sxs-lookup"><span data-stu-id="565b2-251">It's hello sum of hello Application Gateway processing time plus hello network cost toohello back end, plus hello time that hello back end takes tooprocess hello request.</span></span>

### <a name="firewall-log"></a><span data-ttu-id="565b2-252">Registro de firewall</span><span class="sxs-lookup"><span data-stu-id="565b2-252">Firewall log</span></span>

<span data-ttu-id="565b2-253">registro de firewall de Hola se genera solo si se ha habilitado para cada puerta de enlace de la aplicación, como se detalla en hello pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="565b2-253">hello firewall log is generated only if you have enabled it for each application gateway, as detailed in hello preceding steps.</span></span> <span data-ttu-id="565b2-254">Este registro también requiere que firewall de aplicación web de hello esté configurado en una puerta de enlace de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="565b2-254">This log also requires that hello web application firewall is configured on an application gateway.</span></span> <span data-ttu-id="565b2-255">Hola datos se almacenan en la cuenta de almacenamiento de Hola que especificó cuando se habilitó el registro de hello.</span><span class="sxs-lookup"><span data-stu-id="565b2-255">hello data is stored in hello storage account that you specified when you enabled hello logging.</span></span> <span data-ttu-id="565b2-256">se registra Hola datos siguientes:</span><span class="sxs-lookup"><span data-stu-id="565b2-256">hello following data is logged:</span></span>


|<span data-ttu-id="565b2-257">Valor</span><span class="sxs-lookup"><span data-stu-id="565b2-257">Value</span></span>  |<span data-ttu-id="565b2-258">Descripción</span><span class="sxs-lookup"><span data-stu-id="565b2-258">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="565b2-259">instanceId</span><span class="sxs-lookup"><span data-stu-id="565b2-259">instanceId</span></span>     | <span data-ttu-id="565b2-260">Instancia de Application Gateway para la que se van a generar los datos de firewall.</span><span class="sxs-lookup"><span data-stu-id="565b2-260">Application Gateway instance for which firewall data is being generated.</span></span> <span data-ttu-id="565b2-261">Si hay varias instancias de Application Gateway, hay una fila por cada instancia.</span><span class="sxs-lookup"><span data-stu-id="565b2-261">For a multiple-instance application gateway, there is one row per instance.</span></span>         |
|<span data-ttu-id="565b2-262">clientIp</span><span class="sxs-lookup"><span data-stu-id="565b2-262">clientIp</span></span>     |   <span data-ttu-id="565b2-263">IP de origen para la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="565b2-263">Originating IP for hello request.</span></span>      |
|<span data-ttu-id="565b2-264">clientPort</span><span class="sxs-lookup"><span data-stu-id="565b2-264">clientPort</span></span>     |  <span data-ttu-id="565b2-265">Puerto de solicitud de Hola de origen.</span><span class="sxs-lookup"><span data-stu-id="565b2-265">Originating port for hello request.</span></span>       |
|<span data-ttu-id="565b2-266">requestUri</span><span class="sxs-lookup"><span data-stu-id="565b2-266">requestUri</span></span>     | <span data-ttu-id="565b2-267">Dirección URL de solicitud recibida Hola.</span><span class="sxs-lookup"><span data-stu-id="565b2-267">URL of hello received request.</span></span>       |
|<span data-ttu-id="565b2-268">ruleSetType</span><span class="sxs-lookup"><span data-stu-id="565b2-268">ruleSetType</span></span>     | <span data-ttu-id="565b2-269">Tipo de conjunto de reglas.</span><span class="sxs-lookup"><span data-stu-id="565b2-269">Rule set type.</span></span> <span data-ttu-id="565b2-270">valor de Hello disponible es OWASP.</span><span class="sxs-lookup"><span data-stu-id="565b2-270">hello available value is OWASP.</span></span>        |
|<span data-ttu-id="565b2-271">ruleSetVersion</span><span class="sxs-lookup"><span data-stu-id="565b2-271">ruleSetVersion</span></span>     | <span data-ttu-id="565b2-272">Versión utilizada del conjunto de reglas.</span><span class="sxs-lookup"><span data-stu-id="565b2-272">Rule set version used.</span></span> <span data-ttu-id="565b2-273">Los valores disponibles son 2.2.9 y 3.0.</span><span class="sxs-lookup"><span data-stu-id="565b2-273">Available values are 2.2.9 and 3.0.</span></span>     |
|<span data-ttu-id="565b2-274">ruleId</span><span class="sxs-lookup"><span data-stu-id="565b2-274">ruleId</span></span>     | <span data-ttu-id="565b2-275">Id. de regla de hello desencadenar el evento.</span><span class="sxs-lookup"><span data-stu-id="565b2-275">Rule ID of hello triggering event.</span></span>        |
|<span data-ttu-id="565b2-276">Mensaje</span><span class="sxs-lookup"><span data-stu-id="565b2-276">message</span></span>     | <span data-ttu-id="565b2-277">Mensaje descriptivo para desencadenar eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="565b2-277">User-friendly message for hello triggering event.</span></span> <span data-ttu-id="565b2-278">En la sección de detalles de Hola se proporcionan más detalles.</span><span class="sxs-lookup"><span data-stu-id="565b2-278">More details are provided in hello details section.</span></span>        |
|<span data-ttu-id="565b2-279">action</span><span class="sxs-lookup"><span data-stu-id="565b2-279">action</span></span>     |  <span data-ttu-id="565b2-280">Acción realizada en la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="565b2-280">Action taken on hello request.</span></span> <span data-ttu-id="565b2-281">Los valores disponibles son Blocked y Allowed.</span><span class="sxs-lookup"><span data-stu-id="565b2-281">Available values are Blocked and Allowed.</span></span>      |
|<span data-ttu-id="565b2-282">site</span><span class="sxs-lookup"><span data-stu-id="565b2-282">site</span></span>     | <span data-ttu-id="565b2-283">Sitio para que Hola se generó el registro.</span><span class="sxs-lookup"><span data-stu-id="565b2-283">Site for which hello log was generated.</span></span> <span data-ttu-id="565b2-284">Actualmente, solo se incluye Global porque las reglas son globales.</span><span class="sxs-lookup"><span data-stu-id="565b2-284">Currently, only Global is listed because rules are global.</span></span>|
|<span data-ttu-id="565b2-285">details</span><span class="sxs-lookup"><span data-stu-id="565b2-285">details</span></span>     | <span data-ttu-id="565b2-286">Detalles del programa Hola a desencadenar el evento.</span><span class="sxs-lookup"><span data-stu-id="565b2-286">Details of hello triggering event.</span></span>        |
|<span data-ttu-id="565b2-287">details.message</span><span class="sxs-lookup"><span data-stu-id="565b2-287">details.message</span></span>     | <span data-ttu-id="565b2-288">Descripción de regla de Hola.</span><span class="sxs-lookup"><span data-stu-id="565b2-288">Description of hello rule.</span></span>        |
|<span data-ttu-id="565b2-289">details.data</span><span class="sxs-lookup"><span data-stu-id="565b2-289">details.data</span></span>     | <span data-ttu-id="565b2-290">Datos específicos encuentran en la solicitud esa regla coincidente Hola.</span><span class="sxs-lookup"><span data-stu-id="565b2-290">Specific data found in request that matched hello rule.</span></span>         |
|<span data-ttu-id="565b2-291">details.file</span><span class="sxs-lookup"><span data-stu-id="565b2-291">details.file</span></span>     | <span data-ttu-id="565b2-292">Archivo de configuración que contiene la regla de Hola.</span><span class="sxs-lookup"><span data-stu-id="565b2-292">Configuration file that contained hello rule.</span></span>        |
|<span data-ttu-id="565b2-293">details.line</span><span class="sxs-lookup"><span data-stu-id="565b2-293">details.line</span></span>     | <span data-ttu-id="565b2-294">Número de línea del archivo de configuración de Hola que desencadenó el evento de Hola.</span><span class="sxs-lookup"><span data-stu-id="565b2-294">Line number in hello configuration file that triggered hello event.</span></span>       |

```json
{
  "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
  "operationName": "ApplicationGatewayFirewall",
  "time": "2017-03-20T15:52:09.1494499Z",
  "category": "ApplicationGatewayFirewallLog",
  "properties": {
    "instanceId": "ApplicationGatewayRole_IN_0",
    "clientIp": "104.210.252.3",
    "clientPort": "4835",
    "requestUri": "/?a=%3Cscript%3Ealert(%22Hello%22);%3C/script%3E",
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "ruleId": "941320",
    "message": "Possible XSS Attack Detected - HTML Tag Handler",
    "action": "Blocked",
    "site": "Global",
    "details": {
      "message": "Warning. Pattern match \"<(a|abbr|acronym|address|applet|area|audioscope|b|base|basefront|bdo|bgsound|big|blackface|blink|blockquote|body|bq|br|button|caption|center|cite|code|col|colgroup|comment|dd|del|dfn|dir|div|dl|dt|em|embed|fieldset|fn|font|form|frame|frameset|h1|head|h ...\" at ARGS:a.",
      "data": "Matched Data: <script> found within ARGS:a: <script>alert(\\x22hello\\x22);</script>",
      "file": "rules/REQUEST-941-APPLICATION-ATTACK-XSS.conf",
      "line": "865"
    }
  }
} 

```

### <a name="view-and-analyze-hello-activity-log"></a><span data-ttu-id="565b2-295">Ver y analizar el registro de actividad de Hola</span><span class="sxs-lookup"><span data-stu-id="565b2-295">View and analyze hello activity log</span></span>

<span data-ttu-id="565b2-296">Puede ver y analizar datos de registro de actividad mediante cualquiera de los siguientes métodos de hello:</span><span class="sxs-lookup"><span data-stu-id="565b2-296">You can view and analyze activity log data by using any of hello following methods:</span></span>

* <span data-ttu-id="565b2-297">**Herramientas de Azure**: recuperar la información de registro de actividad de Hola a través de PowerShell de Azure, CLI de Azure, API de REST de Azure, Hola Hola u Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="565b2-297">**Azure tools**: Retrieve information from hello activity log through Azure PowerShell, hello Azure CLI, hello Azure REST API, or hello Azure portal.</span></span> <span data-ttu-id="565b2-298">Instrucciones paso a paso para cada método se detallan en hello [operaciones de actividad con el Administrador de recursos](../azure-resource-manager/resource-group-audit.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="565b2-298">Step-by-step instructions for each method are detailed in hello [Activity operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="565b2-299">**Power BI:** si todavía no tiene una cuenta de [Power BI](https://powerbi.microsoft.com/pricing) , puede probarlo gratis.</span><span class="sxs-lookup"><span data-stu-id="565b2-299">**Power BI**: If you don't already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="565b2-300">Mediante el uso de hello [contenido de los registros de actividad de Azure para Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), puede analizar los datos con paneles preconfigurados que pueden usar tal cual o personalizar.</span><span class="sxs-lookup"><span data-stu-id="565b2-300">By using hello [Azure Activity Logs content pack for Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), you can analyze your data with preconfigured dashboards that you can use as is or customize.</span></span>

### <a name="view-and-analyze-hello-access-performance-and-firewall-logs"></a><span data-ttu-id="565b2-301">Ver y analizar el acceso de hello, el rendimiento y los registros de firewall</span><span class="sxs-lookup"><span data-stu-id="565b2-301">View and analyze hello access, performance, and firewall logs</span></span>

<span data-ttu-id="565b2-302">Azure [análisis de registros](../log-analytics/log-analytics-azure-networking-analytics.md) puede recopilar archivos de registro de eventos y contadores de hello de la cuenta de almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="565b2-302">Azure [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) can collect hello counter and event log files from your Blob storage account.</span></span> <span data-ttu-id="565b2-303">Incluye visualizaciones y tooanalyze de las capacidades de búsqueda eficaces los registros.</span><span class="sxs-lookup"><span data-stu-id="565b2-303">It includes visualizations and powerful search capabilities tooanalyze your logs.</span></span>

<span data-ttu-id="565b2-304">También puede conectar la cuenta de almacenamiento de tooyour y recuperar entradas de registro de hello JSON para los registros de acceso y el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="565b2-304">You can also connect tooyour storage account and retrieve hello JSON log entries for access and performance logs.</span></span> <span data-ttu-id="565b2-305">Después de descargar los archivos JSON hello, puede convertirlos tooCSV y verlos en Excel, Power BI o cualquier otra herramienta de visualización de datos.</span><span class="sxs-lookup"><span data-stu-id="565b2-305">After you download hello JSON files, you can convert them tooCSV and view them in Excel, Power BI, or any other data-visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="565b2-306">Si está familiarizado con los conceptos básicos del cambio de valores de constantes y variables de C# y Visual Studio, puede usar hello [iniciar herramientas de convertidor](https://github.com/Azure-Samples/networking-dotnet-log-converter) disponible en GitHub.</span><span class="sxs-lookup"><span data-stu-id="565b2-306">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use hello [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>
> 
> 

## <a name="metrics"></a><span data-ttu-id="565b2-307">Métricas</span><span class="sxs-lookup"><span data-stu-id="565b2-307">Metrics</span></span>

<span data-ttu-id="565b2-308">Las métricas son una característica para determinados recursos de Azure donde puede ver los contadores de rendimiento en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="565b2-308">Metrics are a feature for certain Azure resources where you can view performance counters in hello portal.</span></span> <span data-ttu-id="565b2-309">En el caso de Application Gateway, actualmente hay disponible una métrica.</span><span class="sxs-lookup"><span data-stu-id="565b2-309">For Application Gateway, one metric is available now.</span></span> <span data-ttu-id="565b2-310">Esta métrica es el rendimiento, y puede verlo en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="565b2-310">This metric is throughput, and you can see it in hello portal.</span></span> <span data-ttu-id="565b2-311">Puerta de enlace de aplicaciones de tooan y haga clic en **métricas**.</span><span class="sxs-lookup"><span data-stu-id="565b2-311">Browse tooan application gateway and click **Metrics**.</span></span> <span data-ttu-id="565b2-312">valores de hello tooview, seleccione rendimiento Hola **métricas disponibles** sección.</span><span class="sxs-lookup"><span data-stu-id="565b2-312">tooview hello values, select throughput in hello **Available metrics** section.</span></span> <span data-ttu-id="565b2-313">Hola después de la imagen, puede ver un ejemplo con filtros de Hola que puede usar datos de hello toodisplay en intervalos de tiempo diferentes.</span><span class="sxs-lookup"><span data-stu-id="565b2-313">In hello following image, you can see an example with hello filters that you can use toodisplay hello data in different time ranges.</span></span>

![Vista de métrica con filtros][5]

<span data-ttu-id="565b2-315">vea una lista actualizada de las métricas, toosee [métricas con el Monitor de Azure admitidas](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="565b2-315">toosee a current list of metrics, see [Supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

### <a name="alert-rules"></a><span data-ttu-id="565b2-316">Las reglas de alertas</span><span class="sxs-lookup"><span data-stu-id="565b2-316">Alert rules</span></span>

<span data-ttu-id="565b2-317">Puede iniciar las reglas de alerta en función de las métricas de un recurso.</span><span class="sxs-lookup"><span data-stu-id="565b2-317">You can start alert rules based on metrics for a resource.</span></span> <span data-ttu-id="565b2-318">Por ejemplo, una alerta puede llamar a un webhook o un administrador de correo electrónico si el rendimiento de puerta de enlace de aplicación Hola Hola es encima, debajo o con un umbral durante un período especificado.</span><span class="sxs-lookup"><span data-stu-id="565b2-318">For example, an alert can call a webhook or email an administrator if hello throughput of hello application gateway is above, below, or at a threshold for a specified period.</span></span>

<span data-ttu-id="565b2-319">Hola ejemplo siguiente le guía por la creación de una regla de alerta que envía un administrador de tooan de correo electrónico después de las infracciones de rendimiento un umbral:</span><span class="sxs-lookup"><span data-stu-id="565b2-319">hello following example walks you through creating an alert rule that sends an email tooan administrator after throughput breaches a threshold:</span></span>

1. <span data-ttu-id="565b2-320">Haga clic en **Agregar alerta métrica** tooopen hello **Agregar regla** hoja.</span><span class="sxs-lookup"><span data-stu-id="565b2-320">Click **Add metric alert** tooopen hello **Add rule** blade.</span></span> <span data-ttu-id="565b2-321">También puede tener acceso a esta hoja de hoja de métricas de Hola.</span><span class="sxs-lookup"><span data-stu-id="565b2-321">You can also reach this blade from hello metrics blade.</span></span>

   ![Botón “Agregar alerta de métrica”][6]

2. <span data-ttu-id="565b2-323">En hello **Agregar regla** hoja, rellene el nombre de hello, condición y notificar a secciones y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="565b2-323">On hello **Add rule** blade, fill out hello name, condition, and notify sections, and click **OK**.</span></span>

   * <span data-ttu-id="565b2-324">Hola **condición** selector, seleccione uno de los valores de hello cuatro: **mayor**, **igual o mayor que**, **inferior a**, o  **Menor o igual que**.</span><span class="sxs-lookup"><span data-stu-id="565b2-324">In hello **Condition** selector, select one of hello four values: **Greater than**, **Greater than or equal**, **Less than**, or **Less than or equal to**.</span></span>

   * <span data-ttu-id="565b2-325">Hola **período** selector, seleccione un período de 5 minutos too6 horas.</span><span class="sxs-lookup"><span data-stu-id="565b2-325">In hello **Period** selector, select a period from 5 minutes too6 hours.</span></span>

   * <span data-ttu-id="565b2-326">Si selecciona **correo electrónico a los propietarios, contributors y readers**, correo electrónico de hello puede ser dinámica en función de los usuarios de Hola que tienen acceso a recursos de toothat.</span><span class="sxs-lookup"><span data-stu-id="565b2-326">If you select **Email owners, contributors, and readers**, hello email can be dynamic based on hello users who have access toothat resource.</span></span> <span data-ttu-id="565b2-327">En caso contrario, puede proporcionar una lista separada por comas de los usuarios de hello **email(s) Administrador adicional** cuadro.</span><span class="sxs-lookup"><span data-stu-id="565b2-327">Otherwise, you can provide a comma-separated list of users in hello **Additional administrator email(s)** box.</span></span>

   ![Hoja Agregar regla][7]

<span data-ttu-id="565b2-329">Si se supera el umbral de hello, llega un correo electrónico que es toohello similar uno Hola después de imagen:</span><span class="sxs-lookup"><span data-stu-id="565b2-329">If hello threshold is breached, an email that's similar toohello one in hello following image arrives:</span></span>

![Correo electrónico para el umbral infringido][8]

<span data-ttu-id="565b2-331">Después de crear una alerta de métrica, aparece una lista de alertas.</span><span class="sxs-lookup"><span data-stu-id="565b2-331">A list of alerts appears after you create a metric alert.</span></span> <span data-ttu-id="565b2-332">Proporciona una visión general de todas las reglas de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="565b2-332">It provides an overview of all hello alert rules.</span></span>

![Lista de alertas y reglas][9]

<span data-ttu-id="565b2-334">toolearn más información acerca de las notificaciones de alerta, consulte [recibir notificaciones de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="565b2-334">toolearn more about alert notifications, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="565b2-335">toounderstand más información acerca de webhooks y cómo se pueden utilizar las alertas, visite [configurar un webhook en una alerta de métrica Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="565b2-335">toounderstand more about webhooks and how you can use them with alerts, visit [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="565b2-336">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="565b2-336">Next steps</span></span>

* <span data-ttu-id="565b2-337">Visualice el contador y los registros de eventos con [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="565b2-337">Visualize counter and event logs by using [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).</span></span>
* <span data-ttu-id="565b2-338">Consulte la entrada de blog [Visualize your Azure Activity Logs with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) (Visualizar los registros de actividades de Azure con Power BI).</span><span class="sxs-lookup"><span data-stu-id="565b2-338">[Visualize your Azure activity log with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="565b2-339">Consulte la entrada de blog [View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) (Consulta y análisis de registros de auditoría de Azure en Power BI y más).</span><span class="sxs-lookup"><span data-stu-id="565b2-339">[View and analyze Azure activity logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

[1]: ./media/application-gateway-diagnostics/figure1.png
[2]: ./media/application-gateway-diagnostics/figure2.png
[3]: ./media/application-gateway-diagnostics/figure3.png
[4]: ./media/application-gateway-diagnostics/figure4.png
[5]: ./media/application-gateway-diagnostics/figure5.png
[6]: ./media/application-gateway-diagnostics/figure6.png
[7]: ./media/application-gateway-diagnostics/figure7.png
[8]: ./media/application-gateway-diagnostics/figure8.png
[9]: ./media/application-gateway-diagnostics/figure9.png
[10]: ./media/application-gateway-diagnostics/figure10.png
