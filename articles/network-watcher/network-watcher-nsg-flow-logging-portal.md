---
title: registros de flujo de grupo de seguridad de aaaManage red con Monitor de red de Azure | Documentos de Microsoft
description: "Esta página explica cómo toomanage flujo de grupo de seguridad de red se registra en el Monitor de red de Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 01606cbf-d70b-40ad-bc1d-f03bb642e0af
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fb250337ab9d1a0c0d0d3569c00bc221dd102a3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-group-flow-logs-in-hello-azure-portal"></a><span data-ttu-id="109d0-103">Administrar registros de flujo de grupo de seguridad de red en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="109d0-103">Manage network security group flow logs in hello Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="109d0-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="109d0-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="109d0-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="109d0-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="109d0-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="109d0-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="109d0-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="109d0-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="109d0-108">API DE REST</span><span class="sxs-lookup"><span data-stu-id="109d0-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="109d0-109">Registros de flujo de grupo de seguridad de red son una característica del Monitor de red que permite tooview información sobre el tráfico IP de entrada y de salida a través de un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="109d0-109">Network security group flow logs are a feature of Network Watcher that enables you tooview information about ingress and egress IP traffic through a network security group.</span></span> <span data-ttu-id="109d0-110">Estos registros de flujo se escriben con formato JSON y brinda información importante, la que incluye:</span><span class="sxs-lookup"><span data-stu-id="109d0-110">These flow logs are written in JSON format and provide important information, including:</span></span> 

- <span data-ttu-id="109d0-111">Flujos de entrada y de salida por regla.</span><span class="sxs-lookup"><span data-stu-id="109d0-111">Outbound and inbound flows on a per-rule basis.</span></span>
- <span data-ttu-id="109d0-112">Hola NIC que Hola flujo se aplica a.</span><span class="sxs-lookup"><span data-stu-id="109d0-112">hello NIC that hello flow applies to.</span></span>
- <span data-ttu-id="109d0-113">tupla de 5 información acerca del flujo de hello (dirección IP de origen/destino, puerto de origen/destino, protocolo).</span><span class="sxs-lookup"><span data-stu-id="109d0-113">5-tuple information about hello flow (source/destination IP, source/destination port, protocol).</span></span>
- <span data-ttu-id="109d0-114">Información sobre si se permitió o denegó el tráfico.</span><span class="sxs-lookup"><span data-stu-id="109d0-114">Information about whether traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="109d0-115">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="109d0-115">Before you begin</span></span>

<span data-ttu-id="109d0-116">Este escenario se supone que ya ha seguido los pasos de hello en [crear una instancia del Monitor de red](network-watcher-create.md).</span><span class="sxs-lookup"><span data-stu-id="109d0-116">This scenario assumes you have already followed hello steps in [Create a Network Watcher instance](network-watcher-create.md).</span></span> <span data-ttu-id="109d0-117">escenario de Hello también se supone que una tiene un grupo de recursos con una máquina virtual válida.</span><span class="sxs-lookup"><span data-stu-id="109d0-117">hello scenario also assumes that a you have a resource group with a valid virtual machine.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="109d0-118">Registro del proveedor de Insights</span><span class="sxs-lookup"><span data-stu-id="109d0-118">Register Insights provider</span></span>

<span data-ttu-id="109d0-119">Para el flujo de registro toowork correctamente, Hola **Microsoft.Insights** proveedor debe estar registrado.</span><span class="sxs-lookup"><span data-stu-id="109d0-119">For flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="109d0-120">proveedor de hello tooregister, Hola toman pasos:</span><span class="sxs-lookup"><span data-stu-id="109d0-120">tooregister hello provider, take hello following steps:</span></span> 

1. <span data-ttu-id="109d0-121">Vaya demasiado**suscripciones**y, a continuación, seleccione la suscripción de hello para el que desea que los registros de flujo de tooenable.</span><span class="sxs-lookup"><span data-stu-id="109d0-121">Go too**Subscriptions**, and then select hello subscription for which you want tooenable flow logs.</span></span> 
2. <span data-ttu-id="109d0-122">En hello **suscripción** hoja, seleccione **proveedores de recursos**.</span><span class="sxs-lookup"><span data-stu-id="109d0-122">On hello **Subscription** blade, select **Resource Providers**.</span></span> 
3. <span data-ttu-id="109d0-123">Mire Hola lista de proveedores y compruebe que hello **microsoft.insights** proveedor está registrado.</span><span class="sxs-lookup"><span data-stu-id="109d0-123">Look at hello list of providers, and verify that hello **microsoft.insights** provider is registered.</span></span> <span data-ttu-id="109d0-124">Si no es así, seleccione **Registrarse**.</span><span class="sxs-lookup"><span data-stu-id="109d0-124">If not, then select **Register**.</span></span>

![Visualización de proveedores][providers]

## <a name="enable-flow-logs"></a><span data-ttu-id="109d0-126">Habilitar los registros de flujo</span><span class="sxs-lookup"><span data-stu-id="109d0-126">Enable flow logs</span></span>

<span data-ttu-id="109d0-127">Estos pasos le guiarán en proceso de Hola de habilitar registros de flujo en un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="109d0-127">These steps take you through hello process of enabling flow logs on a network security group.</span></span>

### <a name="step-1"></a><span data-ttu-id="109d0-128">Paso 1</span><span class="sxs-lookup"><span data-stu-id="109d0-128">Step 1</span></span>

<span data-ttu-id="109d0-129">Vaya tooa instancia de Monitor de red y, a continuación, seleccione **registros de flujo de NSG**.</span><span class="sxs-lookup"><span data-stu-id="109d0-129">Go tooa Network Watcher instance, and then select **NSG Flow logs**.</span></span>

![Información general de los registros de flujo][1]

### <a name="step-2"></a><span data-ttu-id="109d0-131">Paso 2</span><span class="sxs-lookup"><span data-stu-id="109d0-131">Step 2</span></span>

<span data-ttu-id="109d0-132">Seleccione un grupo de seguridad de red de hello lista.</span><span class="sxs-lookup"><span data-stu-id="109d0-132">Select a network security group from hello list.</span></span>

![Información general de los registros de flujo][2]

### <a name="step-3"></a><span data-ttu-id="109d0-134">Paso 3</span><span class="sxs-lookup"><span data-stu-id="109d0-134">Step 3</span></span> 

<span data-ttu-id="109d0-135">En hello **configuración de registros de flujo de** hoja, establecer el estado de hello demasiado**en**y, a continuación, configure una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="109d0-135">On hello **Flow logs settings** blade, set hello status too**On**, and then configure a storage account.</span></span>  <span data-ttu-id="109d0-136">Cuando finalice, seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="109d0-136">When you're done, select **OK**.</span></span> <span data-ttu-id="109d0-137">Después, seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="109d0-137">Then select **Save**.</span></span>

![Información general de los registros de flujo][3]

## <a name="download-flow-logs"></a><span data-ttu-id="109d0-139">Descarga de registros de flujo</span><span class="sxs-lookup"><span data-stu-id="109d0-139">Download flow logs</span></span>

<span data-ttu-id="109d0-140">Los registros de flujo se guardan en una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="109d0-140">Flow logs are saved in a storage account.</span></span> <span data-ttu-id="109d0-141">Descargue el tooview de registros de flujo ellos.</span><span class="sxs-lookup"><span data-stu-id="109d0-141">Download your flow logs tooview them.</span></span>

### <a name="step-1"></a><span data-ttu-id="109d0-142">Paso 1</span><span class="sxs-lookup"><span data-stu-id="109d0-142">Step 1</span></span>

<span data-ttu-id="109d0-143">seleccionar registros de flujo de toodownload, **puede descargar los registros de flujo de las cuentas de almacenamiento configurado**.</span><span class="sxs-lookup"><span data-stu-id="109d0-143">toodownload flow logs, select **You can download flow logs from configured storage accounts**.</span></span> <span data-ttu-id="109d0-144">Este paso le tooa vista de cuentas de almacenamiento donde puede elegir qué toodownload de registros.</span><span class="sxs-lookup"><span data-stu-id="109d0-144">This step takes you tooa storage account view where you can choose which logs toodownload.</span></span>

![Configuración de registros de flujo][4]

### <a name="step-2"></a><span data-ttu-id="109d0-146">Paso 2</span><span class="sxs-lookup"><span data-stu-id="109d0-146">Step 2</span></span>

<span data-ttu-id="109d0-147">Vaya toohello cuenta de almacenamiento correcta.</span><span class="sxs-lookup"><span data-stu-id="109d0-147">Go toohello correct storage account.</span></span> <span data-ttu-id="109d0-148">Luego, seleccione **Contenedores** > **insights-log-networksecuritygroupflowevent**.</span><span class="sxs-lookup"><span data-stu-id="109d0-148">Then select **Containers** > **insights-log-networksecuritygroupflowevent**.</span></span>

![Configuración de registros de flujo][5]

### <a name="step-3"></a><span data-ttu-id="109d0-150">Paso 3</span><span class="sxs-lookup"><span data-stu-id="109d0-150">Step 3</span></span>

<span data-ttu-id="109d0-151">Vaya a toohello ubicación del registro de flujo de hello, selecciónelo y, a continuación, seleccione **descargar**.</span><span class="sxs-lookup"><span data-stu-id="109d0-151">Go toohello location of hello flow log, select it, and then select **Download**.</span></span>

![Configuración de registros de flujo][6]

<span data-ttu-id="109d0-153">Para obtener información acerca de la estructura de Hola de registro de hello, visite [información general sobre el registro de flujo de red seguridad grupo](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="109d0-153">For information about hello structure of hello log, visit [Network security group flow log overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="109d0-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="109d0-154">Next steps</span></span>

<span data-ttu-id="109d0-155">Obtenga información acerca de cómo demasiado[visualizar los registros de flujo NSG con PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="109d0-155">Learn how too[visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-portal/figure1.png
[2]: ./media/network-watcher-nsg-flow-logging-portal/figure2.png
[3]: ./media/network-watcher-nsg-flow-logging-portal/figure3.png
[4]: ./media/network-watcher-nsg-flow-logging-portal/figure4.png
[5]: ./media/network-watcher-nsg-flow-logging-portal/figure5.png
[6]: ./media/network-watcher-nsg-flow-logging-portal/figure6.png
[providers]: ./media/network-watcher-nsg-flow-logging-portal/providers.png
