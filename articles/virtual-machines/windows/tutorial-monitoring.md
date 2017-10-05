---
title: "Supervisión de Azure y máquinas virtuales Windows | Microsoft Docs"
description: "Tutorial: Supervisar una máquina virtual Windows con Azure PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/04/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 42a475092bdd615c23154e5f813861b0acefcf29
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-a-windows-virtual-machine-with-azure-powershell"></a><span data-ttu-id="56b27-103">Supervisar una máquina virtual Windows con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="56b27-103">Monitor a Windows Virtual Machine with Azure PowerShell</span></span>

<span data-ttu-id="56b27-104">La supervisión de Azure usa agentes para recopilar datos de arranque y de rendimiento de máquinas virtuales de Azure, almacenar estos datos en Azure Storage y permitir el acceso a ellos a través del portal, el módulo de Azure PowerShell y la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="56b27-104">Azure monitoring uses agents to collect boot and performance data from Azure VMs, store this data in Azure storage, and make it accessible through portal, the Azure PowerShell module, and the Azure CLI.</span></span> <span data-ttu-id="56b27-105">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="56b27-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="56b27-106">Habilitar los diagnósticos de arranque en una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="56b27-106">Enable boot diagnostics on a VM</span></span>
> * <span data-ttu-id="56b27-107">Ver los diagnósticos de arranque</span><span class="sxs-lookup"><span data-stu-id="56b27-107">View boot diagnostics</span></span>
> * <span data-ttu-id="56b27-108">Ver las métricas del host de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="56b27-108">View VM host metrics</span></span>
> * <span data-ttu-id="56b27-109">Instalar la extensión de Diagnostics</span><span class="sxs-lookup"><span data-stu-id="56b27-109">Install the diagnostics extension</span></span>
> * <span data-ttu-id="56b27-110">Ver las métricas de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="56b27-110">View VM metrics</span></span>
> * <span data-ttu-id="56b27-111">Crear una alerta</span><span class="sxs-lookup"><span data-stu-id="56b27-111">Create an alert</span></span>
> * <span data-ttu-id="56b27-112">Configurar la supervisión avanzada</span><span class="sxs-lookup"><span data-stu-id="56b27-112">Set up advanced monitoring</span></span>

<span data-ttu-id="56b27-113">Para realizar este tutorial es necesaria la versión 3.6 del módulo de Azure PowerShell, o cualquier versión posterior.</span><span class="sxs-lookup"><span data-stu-id="56b27-113">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="56b27-114">Ejecute ` Get-Module -ListAvailable AzureRM` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="56b27-114">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="56b27-115">Si necesita actualizarla, vea [Instalación del módulo de Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="56b27-115">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

<span data-ttu-id="56b27-116">Para completar el ejemplo de este tutorial, debe tener una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="56b27-116">To complete the example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="56b27-117">Si es necesario, este [script de ejemplo](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) puede crear una.</span><span class="sxs-lookup"><span data-stu-id="56b27-117">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="56b27-118">Al trabajar en el tutorial, reemplace el grupo de recursos, el nombre de la máquina virtual y la ubicación cuando proceda.</span><span class="sxs-lookup"><span data-stu-id="56b27-118">When working through the tutorial, replace the resource group, VM name, and location where needed.</span></span>

## <a name="view-boot-diagnostics"></a><span data-ttu-id="56b27-119">Ver los diagnósticos de arranque</span><span class="sxs-lookup"><span data-stu-id="56b27-119">View boot diagnostics</span></span>

<span data-ttu-id="56b27-120">Cuando las máquinas virtuales Windows arrancan, el agente de diagnóstico de arranque captura una salida de pantalla que se puede usar para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="56b27-120">As Windows virtual machines boot up, the boot diagnostic agent captures screen output that can be used for troubleshooting purpose.</span></span> <span data-ttu-id="56b27-121">Esta funcionalidad está habilitada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="56b27-121">This capability is enabled by default.</span></span> <span data-ttu-id="56b27-122">Las capturas de pantalla se almacenan en una cuenta de Azure Storage, que también se crea de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="56b27-122">The captured screen shots are stored in an Azure storage account, which is also created by default.</span></span> 

<span data-ttu-id="56b27-123">Puede obtener los datos de diagnóstico de arranque con el comando [Get-AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata).</span><span class="sxs-lookup"><span data-stu-id="56b27-123">You can get the boot diagnostic data with the [Get-AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata) command.</span></span> <span data-ttu-id="56b27-124">En el ejemplo siguiente, el diagnóstico de arranque se descarga en la raíz de la unidad *c:\*.</span><span class="sxs-lookup"><span data-stu-id="56b27-124">In the following example, boot diagnostics are downloaded to the root of the *c:\* drive.</span></span> 

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup -Name myVM -Windows -LocalPath "c:\"
```

## <a name="view-host-metrics"></a><span data-ttu-id="56b27-125">Ver las métricas del host</span><span class="sxs-lookup"><span data-stu-id="56b27-125">View host metrics</span></span>

<span data-ttu-id="56b27-126">Una máquina virtual Windows tiene una máquina virtual host dedicada en Azure con la que interactúa.</span><span class="sxs-lookup"><span data-stu-id="56b27-126">A Windows VM has a dedicated Host VM in Azure that it interacts with.</span></span> <span data-ttu-id="56b27-127">Las métricas del host se recopilan automáticamente y se pueden ver en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="56b27-127">Metrics are automatically collected for the Host and can be viewed in the Azure portal.</span></span>

1. <span data-ttu-id="56b27-128">En Azure Portal, haga clic en **Grupos de recursos**, seleccione **myResourceGroup** y, después, seleccione **myVM** en la lista de recursos.</span><span class="sxs-lookup"><span data-stu-id="56b27-128">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
2. <span data-ttu-id="56b27-129">Haga clic en **Métricas** en la hoja de la máquina virtual y seleccione cualquiera de las métricas del host en **Métricas disponibles** para ver el funcionamiento de la máquina virtual host.</span><span class="sxs-lookup"><span data-stu-id="56b27-129">Click **Metrics** on the VM blade, and then select any of the Host metrics under **Available metrics** to see how the Host VM is performing.</span></span>

    ![Ver las métricas del host](./media/tutorial-monitoring/tutorial-monitor-host-metrics.png)

## <a name="install-diagnostics-extension"></a><span data-ttu-id="56b27-131">Instalar la extensión de Diagnostics</span><span class="sxs-lookup"><span data-stu-id="56b27-131">Install diagnostics extension</span></span>

<span data-ttu-id="56b27-132">Hay disponibles métricas básicas del host, pero para ver métricas más pormenorizadas específicas de la máquina virtual, es preciso instalar la extensión de Azure Diagnostics en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="56b27-132">The basic host metrics are available, but to see more granular and VM-specific metrics, you to need to install the Azure diagnostics extension on the VM.</span></span> <span data-ttu-id="56b27-133">La extensión de Azure Diagnostics permite recuperar más datos de supervisión y diagnóstico de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="56b27-133">The Azure diagnostics extension allows additional monitoring and diagnostics data to be retrieved from the VM.</span></span> <span data-ttu-id="56b27-134">Puede ver estas métricas de rendimiento y crear alertas basadas en el funcionamiento de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="56b27-134">You can view these performance metrics and create alerts based on how the VM performs.</span></span> <span data-ttu-id="56b27-135">La extensión de diagnósticos se instala a través de Azure Portal como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="56b27-135">The diagnostic extension is installed through the Azure portal as follows:</span></span>

1. <span data-ttu-id="56b27-136">En Azure Portal, haga clic en **Grupos de recursos**, seleccione **myResourceGroup** y, después, seleccione **myVM** en la lista de recursos.</span><span class="sxs-lookup"><span data-stu-id="56b27-136">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
2. <span data-ttu-id="56b27-137">Haga clic en **Configuración de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="56b27-137">Click **Diagnosis settings**.</span></span> <span data-ttu-id="56b27-138">La lista muestra que los *diagnósticos de arranque* ya están habilitados desde la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="56b27-138">The list shows that *Boot diagnostics* are already enabled from the previous section.</span></span> <span data-ttu-id="56b27-139">Haga clic en la casilla *Métricas básicas*.</span><span class="sxs-lookup"><span data-stu-id="56b27-139">Click the check box for *Basic metrics*.</span></span>
3. <span data-ttu-id="56b27-140">Haga clic en el botón **Habilitar supervisión a nivel de invitado**.</span><span class="sxs-lookup"><span data-stu-id="56b27-140">Click the **Enable guest-level monitoring** button.</span></span>

    ![Ver métricas de diagnósticos](./media/tutorial-monitoring/enable-diagnostics-extension.png)

## <a name="view-vm-metrics"></a><span data-ttu-id="56b27-142">Ver las métricas de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="56b27-142">View VM metrics</span></span>

<span data-ttu-id="56b27-143">Las métricas de la máquina virtual se pueden ver de la misma manera que las de la máquina virtual host:</span><span class="sxs-lookup"><span data-stu-id="56b27-143">You can view the VM metrics in the same way that you viewed the host VM metrics:</span></span>

1. <span data-ttu-id="56b27-144">En Azure Portal, haga clic en **Grupos de recursos**, seleccione **myResourceGroup** y, después, seleccione **myVM** en la lista de recursos.</span><span class="sxs-lookup"><span data-stu-id="56b27-144">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
2. <span data-ttu-id="56b27-145">Para ver el rendimiento de la máquina virtual, haga clic en **Métricas** en la hoja de la máquina virtual y seleccione cualquiera de las métricas de diagnóstico en **Métricas disponibles**.</span><span class="sxs-lookup"><span data-stu-id="56b27-145">To see how the VM is performing, click **Metrics** on the VM blade, and then select any of the diagnostics metrics under **Available metrics**.</span></span>

    ![Ver las métricas de la máquina virtual](./media/tutorial-monitoring/monitor-vm-metrics.png)

## <a name="create-alerts"></a><span data-ttu-id="56b27-147">Creación de alertas</span><span class="sxs-lookup"><span data-stu-id="56b27-147">Create alerts</span></span>

<span data-ttu-id="56b27-148">Puede crear alertas basadas en métricas de rendimiento concretas.</span><span class="sxs-lookup"><span data-stu-id="56b27-148">You can create alerts based on specific performance metrics.</span></span> <span data-ttu-id="56b27-149">Se pueden usar alertas para enviar una notificación, por ejemplo, cuando el uso medio de la CPU supera un umbral concreto o cuando el espacio libre en disco disponible cae por debajo de una cantidad determinada.</span><span class="sxs-lookup"><span data-stu-id="56b27-149">Alerts can be used to notify you when average CPU usage exceeds a certain threshold or available free disk space drops below a certain amount, for example.</span></span> <span data-ttu-id="56b27-150">Las alertas se muestran en Azure Portal o se pueden enviar por correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="56b27-150">Alerts are displayed in the Azure portal or can be sent via email.</span></span> <span data-ttu-id="56b27-151">También puede desencadenar runbooks de Azure Automation o Azure Logic Apps en respuesta a las alertas que se generan.</span><span class="sxs-lookup"><span data-stu-id="56b27-151">You can also trigger Azure Automation runbooks or Azure Logic Apps in response to alerts being generated.</span></span>

<span data-ttu-id="56b27-152">En el siguiente ejemplo se crea una alerta para el uso medio de la CPU.</span><span class="sxs-lookup"><span data-stu-id="56b27-152">The following example creates an alert for average CPU usage.</span></span>

1. <span data-ttu-id="56b27-153">En Azure Portal, haga clic en **Grupos de recursos**, seleccione **myResourceGroup** y, después, seleccione **myVM** en la lista de recursos.</span><span class="sxs-lookup"><span data-stu-id="56b27-153">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
2. <span data-ttu-id="56b27-154">Haga clic en **Reglas de alertas** en la hoja de la máquina virtual y, después, en **Agregar alerta de métrica** en la parte superior de la hoja de alertas.</span><span class="sxs-lookup"><span data-stu-id="56b27-154">Click **Alert rules** on the VM blade, then click **Add metric alert** across the top of the alerts blade.</span></span>
4. <span data-ttu-id="56b27-155">Especifique un **nombre** para la alerta, como *myAlertRule*.</span><span class="sxs-lookup"><span data-stu-id="56b27-155">Provide a **Name** for your alert, such as *myAlertRule*</span></span>
5. <span data-ttu-id="56b27-156">Para desencadenar una alerta cuando el porcentaje de la CPU supera 1,0 durante cinco minutos, deje el resto de valores predeterminados seleccionados.</span><span class="sxs-lookup"><span data-stu-id="56b27-156">To trigger an alert when CPU percentage exceeds 1.0 for five minutes, leave all the other defaults selected.</span></span>
6. <span data-ttu-id="56b27-157">Opcionalmente, active la casilla *Enviar correo electrónico a propietarios, colaboradores y lectores* para enviar una notificación por correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="56b27-157">Optionally, check the box for *Email owners, contributors, and readers* to send email notification.</span></span> <span data-ttu-id="56b27-158">La acción predeterminada es presentar una notificación en el portal.</span><span class="sxs-lookup"><span data-stu-id="56b27-158">The default action is to present a notification in the portal.</span></span>
7. <span data-ttu-id="56b27-159">Haga clic en el botón **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="56b27-159">Click the **OK** button.</span></span>

## <a name="advanced-monitoring"></a><span data-ttu-id="56b27-160">Supervisión avanzada</span><span class="sxs-lookup"><span data-stu-id="56b27-160">Advanced monitoring</span></span> 

<span data-ttu-id="56b27-161">Mediante [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) se puede realizar una supervisión más avanzada de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="56b27-161">You can do more advanced monitoring of your VM by using [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span></span> <span data-ttu-id="56b27-162">Si aún no lo ha hecho, puede suscribirse para disfrutar de una [evaluación gratuita](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) de Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="56b27-162">If you haven't already done so, you can sign up for a [free trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) of Operations Management Suite.</span></span>

<span data-ttu-id="56b27-163">Cuando tenga acceso al portal de OMS, puede buscar la clave y el identificador del área de trabajo en la hoja Configuración.</span><span class="sxs-lookup"><span data-stu-id="56b27-163">When you have access to the OMS portal, you can find the workspace key and workspace identifier on the Settings blade.</span></span> <span data-ttu-id="56b27-164">Use el comando [Set-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) para agregar la extensión de OMS a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="56b27-164">Use the [Set-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) cmmand to to add the OMS extension to the VM.</span></span> <span data-ttu-id="56b27-165">Actualice los valores de variable del ejemplo siguiente de modo que reflejen la clave y el identificador del área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="56b27-165">Update the variable values in the below sample to reflect you OMS workspace key and workspace Id.</span></span>  

```powershell
$omsId = "<Replace with your OMS Id>"
$omsKey = "<Replace with your OMS key>"

Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
  -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
  -VMName myVM `
  -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
  -ExtensionType "MicrosoftMonitoringAgent" `
  -TypeHandlerVersion 1.0 `
  -Settings @{"workspaceId" = $omsId} `
  -ProtectedSettings @{"workspaceKey" = $omsKey} `
  -Location eastus
```

<span data-ttu-id="56b27-166">Después de unos minutos, debería ver la nueva máquina virtual en el área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="56b27-166">After a few minutes, you should see the new VM in the OMS workspace.</span></span> 

![Hoja OMS](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a><span data-ttu-id="56b27-168">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="56b27-168">Next steps</span></span>
<span data-ttu-id="56b27-169">En este tutorial, ha configurado y revisado las máquinas virtuales con Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="56b27-169">In this tutorial, you configured and reviewed VMs with Azure Security Center.</span></span> <span data-ttu-id="56b27-170">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="56b27-170">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="56b27-171">Crear una red virtual</span><span class="sxs-lookup"><span data-stu-id="56b27-171">Create a virtual network</span></span>
> * <span data-ttu-id="56b27-172">Crear un grupo de recursos y una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="56b27-172">Create a resource group and VM</span></span> 
> * <span data-ttu-id="56b27-173">Habilitar los diagnósticos de arranque en la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="56b27-173">Enable boot diagnostics on the VM</span></span>
> * <span data-ttu-id="56b27-174">Ver los diagnósticos de arranque</span><span class="sxs-lookup"><span data-stu-id="56b27-174">View boot diagnostics</span></span>
> * <span data-ttu-id="56b27-175">Ver las métricas del host</span><span class="sxs-lookup"><span data-stu-id="56b27-175">View host metrics</span></span>
> * <span data-ttu-id="56b27-176">Instalar la extensión de Diagnostics</span><span class="sxs-lookup"><span data-stu-id="56b27-176">Install the diagnostics extension</span></span>
> * <span data-ttu-id="56b27-177">Ver las métricas de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="56b27-177">View VM metrics</span></span>
> * <span data-ttu-id="56b27-178">Crear una alerta</span><span class="sxs-lookup"><span data-stu-id="56b27-178">Create an alert</span></span>
> * <span data-ttu-id="56b27-179">Configurar la supervisión avanzada</span><span class="sxs-lookup"><span data-stu-id="56b27-179">Set up advanced monitoring</span></span>

<span data-ttu-id="56b27-180">En el siguiente tutorial obtendrá información sobre Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="56b27-180">Advance to the next tutorial to learn about Azure security center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="56b27-181">Administración de la seguridad de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="56b27-181">Manage VM security</span></span>](./tutorial-azure-security.md)