---
title: "Administración de registros de flujo de grupos de seguridad de red en Azure Network Watcher | Microsoft Docs"
description: "En esta página se explica cómo administrar registros de flujo de grupos de seguridad de red en Azure Network Watcher."
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
ms.openlocfilehash: 41cb5ffab9bd3a3bed75ffdb6a7383ca1690f810
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-network-security-group-flow-logs-in-the-azure-portal"></a><span data-ttu-id="9fc73-103">Administración de registros de flujo de grupos de seguridad de red en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9fc73-103">Manage network security group flow logs in the Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="9fc73-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9fc73-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="9fc73-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9fc73-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="9fc73-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="9fc73-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="9fc73-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9fc73-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="9fc73-108">API de REST</span><span class="sxs-lookup"><span data-stu-id="9fc73-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="9fc73-109">Los registros de flujo de grupos de seguridad de red son una característica de Network Watcher que permite ver información acerca del tráfico IP de entrada y de salida en un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="9fc73-109">Network security group flow logs are a feature of Network Watcher that enables you to view information about ingress and egress IP traffic through a network security group.</span></span> <span data-ttu-id="9fc73-110">Estos registros de flujo se escriben con formato JSON y brinda información importante, la que incluye:</span><span class="sxs-lookup"><span data-stu-id="9fc73-110">These flow logs are written in JSON format and provide important information, including:</span></span> 

- <span data-ttu-id="9fc73-111">Flujos de entrada y de salida por regla.</span><span class="sxs-lookup"><span data-stu-id="9fc73-111">Outbound and inbound flows on a per-rule basis.</span></span>
- <span data-ttu-id="9fc73-112">La NIC a la que se aplica el flujo.</span><span class="sxs-lookup"><span data-stu-id="9fc73-112">The NIC that the flow applies to.</span></span>
- <span data-ttu-id="9fc73-113">Información de 5-tupla sobre el flujo (dirección IP de origen o destino, puerto de origen o destino, protocolo).</span><span class="sxs-lookup"><span data-stu-id="9fc73-113">5-tuple information about the flow (source/destination IP, source/destination port, protocol).</span></span>
- <span data-ttu-id="9fc73-114">Información sobre si se permitió o denegó el tráfico.</span><span class="sxs-lookup"><span data-stu-id="9fc73-114">Information about whether traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9fc73-115">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="9fc73-115">Before you begin</span></span>

<span data-ttu-id="9fc73-116">En este escenario se da por hecho que ya siguió los pasos descritos en el artículo sobre cómo [crear una instancia de Network Watcher](network-watcher-create.md).</span><span class="sxs-lookup"><span data-stu-id="9fc73-116">This scenario assumes you have already followed the steps in [Create a Network Watcher instance](network-watcher-create.md).</span></span> <span data-ttu-id="9fc73-117">En este escenario se da por hecho que tiene un grupo de recursos con una máquina virtual válida.</span><span class="sxs-lookup"><span data-stu-id="9fc73-117">The scenario also assumes that a you have a resource group with a valid virtual machine.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="9fc73-118">Registro del proveedor de Insights</span><span class="sxs-lookup"><span data-stu-id="9fc73-118">Register Insights provider</span></span>

<span data-ttu-id="9fc73-119">Para que el registro del flujo de trabajo funcione correctamente, es necesario registrar el proveedor **Microsoft.Insights**.</span><span class="sxs-lookup"><span data-stu-id="9fc73-119">For flow logging to work successfully, the **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="9fc73-120">Para registrar el proveedor, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9fc73-120">To register the provider, take the following steps:</span></span> 

1. <span data-ttu-id="9fc73-121">Vaya a **Suscripciones** y, luego, seleccione la suscripción para la que desea habilitar los registros de flujo.</span><span class="sxs-lookup"><span data-stu-id="9fc73-121">Go to **Subscriptions**, and then select the subscription for which you want to enable flow logs.</span></span> 
2. <span data-ttu-id="9fc73-122">En la hoja **Suscripción**, seleccione **Proveedores de recursos**.</span><span class="sxs-lookup"><span data-stu-id="9fc73-122">On the **Subscription** blade, select **Resource Providers**.</span></span> 
3. <span data-ttu-id="9fc73-123">Observe la lista de proveedores y compruebe que el proveedor **microsoft.insights** está registrado.</span><span class="sxs-lookup"><span data-stu-id="9fc73-123">Look at the list of providers, and verify that the **microsoft.insights** provider is registered.</span></span> <span data-ttu-id="9fc73-124">Si no es así, seleccione **Registrarse**.</span><span class="sxs-lookup"><span data-stu-id="9fc73-124">If not, then select **Register**.</span></span>

![Visualización de proveedores][providers]

## <a name="enable-flow-logs"></a><span data-ttu-id="9fc73-126">Habilitar los registros de flujo</span><span class="sxs-lookup"><span data-stu-id="9fc73-126">Enable flow logs</span></span>

<span data-ttu-id="9fc73-127">Estos pasos lo guían en el proceso para habilitar registros de flujo en un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="9fc73-127">These steps take you through the process of enabling flow logs on a network security group.</span></span>

### <a name="step-1"></a><span data-ttu-id="9fc73-128">Paso 1</span><span class="sxs-lookup"><span data-stu-id="9fc73-128">Step 1</span></span>

<span data-ttu-id="9fc73-129">Vaya a una instancia de Network Watcher y seleccione **Registros de flujo de NSG**.</span><span class="sxs-lookup"><span data-stu-id="9fc73-129">Go to a Network Watcher instance, and then select **NSG Flow logs**.</span></span>

![Información general de los registros de flujo][1]

### <a name="step-2"></a><span data-ttu-id="9fc73-131">Paso 2</span><span class="sxs-lookup"><span data-stu-id="9fc73-131">Step 2</span></span>

<span data-ttu-id="9fc73-132">Seleccione un grupo de seguridad de red desde la lista.</span><span class="sxs-lookup"><span data-stu-id="9fc73-132">Select a network security group from the list.</span></span>

![Información general de los registros de flujo][2]

### <a name="step-3"></a><span data-ttu-id="9fc73-134">Paso 3</span><span class="sxs-lookup"><span data-stu-id="9fc73-134">Step 3</span></span> 

<span data-ttu-id="9fc73-135">En la hoja **Configuración de los registros de flujo**, establezca el estado en **On** (Activado) y, luego, configure una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9fc73-135">On the **Flow logs settings** blade, set the status to **On**, and then configure a storage account.</span></span>  <span data-ttu-id="9fc73-136">Cuando finalice, seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9fc73-136">When you're done, select **OK**.</span></span> <span data-ttu-id="9fc73-137">Después, seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9fc73-137">Then select **Save**.</span></span>

![Información general de los registros de flujo][3]

## <a name="download-flow-logs"></a><span data-ttu-id="9fc73-139">Descarga de registros de flujo</span><span class="sxs-lookup"><span data-stu-id="9fc73-139">Download flow logs</span></span>

<span data-ttu-id="9fc73-140">Los registros de flujo se guardan en una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9fc73-140">Flow logs are saved in a storage account.</span></span> <span data-ttu-id="9fc73-141">Descargue los registros de flujo para verlos.</span><span class="sxs-lookup"><span data-stu-id="9fc73-141">Download your flow logs to view them.</span></span>

### <a name="step-1"></a><span data-ttu-id="9fc73-142">Paso 1</span><span class="sxs-lookup"><span data-stu-id="9fc73-142">Step 1</span></span>

<span data-ttu-id="9fc73-143">Para descargar registros de flujo, seleccione **Puede descargar los registros de flujo desde cuentas de almacenamiento configuradas**.</span><span class="sxs-lookup"><span data-stu-id="9fc73-143">To download flow logs, select **You can download flow logs from configured storage accounts**.</span></span> <span data-ttu-id="9fc73-144">Este paso lo lleva a una vista de cuenta de almacenamiento en la que puede elegir los registros que se van a descargar.</span><span class="sxs-lookup"><span data-stu-id="9fc73-144">This step takes you to a storage account view where you can choose which logs to download.</span></span>

![Configuración de registros de flujo][4]

### <a name="step-2"></a><span data-ttu-id="9fc73-146">Paso 2</span><span class="sxs-lookup"><span data-stu-id="9fc73-146">Step 2</span></span>

<span data-ttu-id="9fc73-147">Vaya a la cuenta de almacenamiento correcta.</span><span class="sxs-lookup"><span data-stu-id="9fc73-147">Go to the correct storage account.</span></span> <span data-ttu-id="9fc73-148">Luego, seleccione **Contenedores** > **insights-log-networksecuritygroupflowevent**.</span><span class="sxs-lookup"><span data-stu-id="9fc73-148">Then select **Containers** > **insights-log-networksecuritygroupflowevent**.</span></span>

![Configuración de registros de flujo][5]

### <a name="step-3"></a><span data-ttu-id="9fc73-150">Paso 3</span><span class="sxs-lookup"><span data-stu-id="9fc73-150">Step 3</span></span>

<span data-ttu-id="9fc73-151">Vaya a la ubicación del registro de flujo, selecciónelo y, luego, seleccione **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="9fc73-151">Go to the location of the flow log, select it, and then select **Download**.</span></span>

![Configuración de registros de flujo][6]

<span data-ttu-id="9fc73-153">Para información sobre la estructura del registro, visite la [introducción a los registros de flujo de grupos de seguridad de red](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9fc73-153">For information about the structure of the log, visit [Network security group flow log overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9fc73-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9fc73-154">Next steps</span></span>

<span data-ttu-id="9fc73-155">Obtenga información sobre cómo [visualizar los registros de flujo de NSG con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="9fc73-155">Learn how to [visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-portal/figure1.png
[2]: ./media/network-watcher-nsg-flow-logging-portal/figure2.png
[3]: ./media/network-watcher-nsg-flow-logging-portal/figure3.png
[4]: ./media/network-watcher-nsg-flow-logging-portal/figure4.png
[5]: ./media/network-watcher-nsg-flow-logging-portal/figure5.png
[6]: ./media/network-watcher-nsg-flow-logging-portal/figure6.png
[providers]: ./media/network-watcher-nsg-flow-logging-portal/providers.png
