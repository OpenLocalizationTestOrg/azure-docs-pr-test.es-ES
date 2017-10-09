---
title: "aaaAzure supervisión y máquinas virtuales de Windows | Documentos de Microsoft"
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
ms.openlocfilehash: 191dc5a30d41c25a9e38f8ec2a32efdc05e03015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-windows-virtual-machine-with-azure-powershell"></a><span data-ttu-id="c2aa8-103">Supervisar una máquina virtual Windows con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2aa8-103">Monitor a Windows Virtual Machine with Azure PowerShell</span></span>

<span data-ttu-id="c2aa8-104">Supervisión de Azure usa arranque toocollect de agentes y los datos de rendimiento de las máquinas virtuales de Azure, almacenar estos datos en el almacenamiento de Azure y hacerla accesible a través del portal, módulo de PowerShell de Azure de Hola y Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-104">Azure monitoring uses agents toocollect boot and performance data from Azure VMs, store this data in Azure storage, and make it accessible through portal, hello Azure PowerShell module, and hello Azure CLI.</span></span> <span data-ttu-id="c2aa8-105">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="c2aa8-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c2aa8-106">Habilitar los diagnósticos de arranque en una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c2aa8-106">Enable boot diagnostics on a VM</span></span>
> * <span data-ttu-id="c2aa8-107">Ver los diagnósticos de arranque</span><span class="sxs-lookup"><span data-stu-id="c2aa8-107">View boot diagnostics</span></span>
> * <span data-ttu-id="c2aa8-108">Ver las métricas del host de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c2aa8-108">View VM host metrics</span></span>
> * <span data-ttu-id="c2aa8-109">Instalar extensión de diagnósticos de Hola</span><span class="sxs-lookup"><span data-stu-id="c2aa8-109">Install hello diagnostics extension</span></span>
> * <span data-ttu-id="c2aa8-110">Ver las métricas de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c2aa8-110">View VM metrics</span></span>
> * <span data-ttu-id="c2aa8-111">Crear una alerta</span><span class="sxs-lookup"><span data-stu-id="c2aa8-111">Create an alert</span></span>
> * <span data-ttu-id="c2aa8-112">Configurar la supervisión avanzada</span><span class="sxs-lookup"><span data-stu-id="c2aa8-112">Set up advanced monitoring</span></span>

<span data-ttu-id="c2aa8-113">Este tutorial requiere hello Azure PowerShell versión 3.6 o posterior del módulo.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="c2aa8-114">Ejecutar ` Get-Module -ListAvailable AzureRM` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="c2aa8-115">Si necesita tooupgrade, consulte [módulo instalar Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="c2aa8-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

<span data-ttu-id="c2aa8-116">ejemplo de Hola a toocomplete en este tutorial, debe tener una máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-116">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="c2aa8-117">Si es necesario, este [script de ejemplo](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) puede crear una.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-117">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="c2aa8-118">Al trabajar con el tutorial de hello, reemplace el grupo de recursos de hello, el nombre de máquina virtual y la ubicación donde sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-118">When working through hello tutorial, replace hello resource group, VM name, and location where needed.</span></span>

## <a name="view-boot-diagnostics"></a><span data-ttu-id="c2aa8-119">Ver los diagnósticos de arranque</span><span class="sxs-lookup"><span data-stu-id="c2aa8-119">View boot diagnostics</span></span>

<span data-ttu-id="c2aa8-120">Máquinas virtuales de Windows arrancar, agente de diagnóstico de arranque de hello captura salida de pantalla que se puede usar para solucionar problemas de uso.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-120">As Windows virtual machines boot up, hello boot diagnostic agent captures screen output that can be used for troubleshooting purpose.</span></span> <span data-ttu-id="c2aa8-121">Esta funcionalidad está habilitada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-121">This capability is enabled by default.</span></span> <span data-ttu-id="c2aa8-122">Hola captura pantalla capturas se almacenan en una cuenta de almacenamiento de Azure, que también se crea de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-122">hello captured screen shots are stored in an Azure storage account, which is also created by default.</span></span> 

<span data-ttu-id="c2aa8-123">Puede obtener datos de diagnóstico de arranque de hello con hello [Get AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata) comando.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-123">You can get hello boot diagnostic data with hello [Get-AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata) command.</span></span> <span data-ttu-id="c2aa8-124">En el siguiente ejemplo de Hola, diagnóstico de arranque es la raíz de toohello descargado de Hola * c:\* unidad.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-124">In hello following example, boot diagnostics are downloaded toohello root of hello *c:\* drive.</span></span> 

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup -Name myVM -Windows -LocalPath "c:\"
```

## <a name="view-host-metrics"></a><span data-ttu-id="c2aa8-125">Visualización de las métricas del host</span><span class="sxs-lookup"><span data-stu-id="c2aa8-125">View host metrics</span></span>

<span data-ttu-id="c2aa8-126">Una máquina virtual Windows tiene una máquina virtual host dedicada en Azure con la que interactúa.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-126">A Windows VM has a dedicated Host VM in Azure that it interacts with.</span></span> <span data-ttu-id="c2aa8-127">Las métricas se recopilan automáticamente para hello Host y pueden verse en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-127">Metrics are automatically collected for hello Host and can be viewed in hello Azure portal.</span></span>

1. <span data-ttu-id="c2aa8-128">Hola portal de Azure, haga clic en **grupos de recursos**, seleccione **myResourceGroup**y, a continuación, seleccione **myVM** en la lista de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-128">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="c2aa8-129">Haga clic en **métricas** en Hola hoja de la máquina virtual y, a continuación, seleccione cualquiera de las métricas de Host de hello en **métricas disponibles** toosee el rendimiento de hello máquina virtual de Host.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-129">Click **Metrics** on hello VM blade, and then select any of hello Host metrics under **Available metrics** toosee how hello Host VM is performing.</span></span>

    ![Visualización de las métricas del host](./media/tutorial-monitoring/tutorial-monitor-host-metrics.png)

## <a name="install-diagnostics-extension"></a><span data-ttu-id="c2aa8-131">Instalar la extensión de Diagnostics</span><span class="sxs-lookup"><span data-stu-id="c2aa8-131">Install diagnostics extension</span></span>

<span data-ttu-id="c2aa8-132">métricas de host básica Hello están disponibles, pero toosee más granular y métricas específica de la máquina virtual, se tooneed tooinstall hello Azure extensión de diagnósticos en hello VM.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-132">hello basic host metrics are available, but toosee more granular and VM-specific metrics, you tooneed tooinstall hello Azure diagnostics extension on hello VM.</span></span> <span data-ttu-id="c2aa8-133">Hola extensión de diagnósticos de Azure permite toobe de datos de diagnóstico recuperados de hello VM y supervisión adicional.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-133">hello Azure diagnostics extension allows additional monitoring and diagnostics data toobe retrieved from hello VM.</span></span> <span data-ttu-id="c2aa8-134">Puede ver estas métricas de rendimiento y crear alertas basadas en cómo realiza Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-134">You can view these performance metrics and create alerts based on how hello VM performs.</span></span> <span data-ttu-id="c2aa8-135">extensión de diagnóstico de Hola se instala a través de hello portal de Azure como sigue:</span><span class="sxs-lookup"><span data-stu-id="c2aa8-135">hello diagnostic extension is installed through hello Azure portal as follows:</span></span>

1. <span data-ttu-id="c2aa8-136">Hola portal de Azure, haga clic en **grupos de recursos**, seleccione **myResourceGroup**y, a continuación, seleccione **myVM** en la lista de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-136">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="c2aa8-137">Haga clic en **Configuración de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-137">Click **Diagnosis settings**.</span></span> <span data-ttu-id="c2aa8-138">lista de Hello muestra que *diagnósticos de arranque* ya están habilitados desde la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-138">hello list shows that *Boot diagnostics* are already enabled from hello previous section.</span></span> <span data-ttu-id="c2aa8-139">Haga clic en la casilla de verificación hello *métricas básicas*.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-139">Click hello check box for *Basic metrics*.</span></span>
3. <span data-ttu-id="c2aa8-140">Haga clic en hello **habilitar la supervisión de nivel de invitado** botón.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-140">Click hello **Enable guest-level monitoring** button.</span></span>

    ![Ver métricas de diagnósticos](./media/tutorial-monitoring/enable-diagnostics-extension.png)

## <a name="view-vm-metrics"></a><span data-ttu-id="c2aa8-142">Ver las métricas de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c2aa8-142">View VM metrics</span></span>

<span data-ttu-id="c2aa8-143">Puede ver las métricas de máquina virtual de Hola Hola igual que ver las métricas de máquina virtual de host de hello:</span><span class="sxs-lookup"><span data-stu-id="c2aa8-143">You can view hello VM metrics in hello same way that you viewed hello host VM metrics:</span></span>

1. <span data-ttu-id="c2aa8-144">Hola portal de Azure, haga clic en **grupos de recursos**, seleccione **myResourceGroup**y, a continuación, seleccione **myVM** en la lista de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-144">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="c2aa8-145">toosee cómo está realizando Hola VM, haga clic en **métricas** en Hola hoja de la máquina virtual y, a continuación, seleccione cualquiera de las métricas de diagnóstico de hello en **métricas disponibles**.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-145">toosee how hello VM is performing, click **Metrics** on hello VM blade, and then select any of hello diagnostics metrics under **Available metrics**.</span></span>

    ![Ver las métricas de la máquina virtual](./media/tutorial-monitoring/monitor-vm-metrics.png)

## <a name="create-alerts"></a><span data-ttu-id="c2aa8-147">Creación de alertas</span><span class="sxs-lookup"><span data-stu-id="c2aa8-147">Create alerts</span></span>

<span data-ttu-id="c2aa8-148">Puede crear alertas basadas en métricas de rendimiento concretas.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-148">You can create alerts based on specific performance metrics.</span></span> <span data-ttu-id="c2aa8-149">Las alertas pueden ser usado toonotify cuando uso medio de CPU supera un determinado umbral o espacio en disco disponible cae por debajo de una determinada cantidad, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-149">Alerts can be used toonotify you when average CPU usage exceeds a certain threshold or available free disk space drops below a certain amount, for example.</span></span> <span data-ttu-id="c2aa8-150">Las alertas se muestran en el portal de Azure de Hola o se pueden enviar por correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-150">Alerts are displayed in hello Azure portal or can be sent via email.</span></span> <span data-ttu-id="c2aa8-151">También puede desencadenar runbooks de automatización de Azure o las aplicaciones lógicas de Azure en tooalerts de respuesta que se está generando.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-151">You can also trigger Azure Automation runbooks or Azure Logic Apps in response tooalerts being generated.</span></span>

<span data-ttu-id="c2aa8-152">Hello en el ejemplo siguiente se crea una alerta para el uso medio de CPU.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-152">hello following example creates an alert for average CPU usage.</span></span>

1. <span data-ttu-id="c2aa8-153">Hola portal de Azure, haga clic en **grupos de recursos**, seleccione **myResourceGroup**y, a continuación, seleccione **myVM** en la lista de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-153">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="c2aa8-154">Haga clic en **reglas de alerta** en la hoja de la máquina virtual de hello, a continuación, haga clic en **Agregar alerta métrica** a través de la parte superior de Hola de hoja de alertas de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-154">Click **Alert rules** on hello VM blade, then click **Add metric alert** across hello top of hello alerts blade.</span></span>
4. <span data-ttu-id="c2aa8-155">Especifique un **nombre** para la alerta, como *myAlertRule*.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-155">Provide a **Name** for your alert, such as *myAlertRule*</span></span>
5. <span data-ttu-id="c2aa8-156">tootrigger una alerta cuando el porcentaje de CPU supera 1.0 durante cinco minutos, deje Hola todos los demás valores predeterminados seleccionados.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-156">tootrigger an alert when CPU percentage exceeds 1.0 for five minutes, leave all hello other defaults selected.</span></span>
6. <span data-ttu-id="c2aa8-157">Si lo desea, active casilla de Hola para *correo electrónico a los propietarios, contributors y readers* toosend notificación de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-157">Optionally, check hello box for *Email owners, contributors, and readers* toosend email notification.</span></span> <span data-ttu-id="c2aa8-158">acción predeterminada de Hello es toopresent una notificación en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-158">hello default action is toopresent a notification in hello portal.</span></span>
7. <span data-ttu-id="c2aa8-159">Haga clic en hello **Aceptar** botón.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-159">Click hello **OK** button.</span></span>

## <a name="advanced-monitoring"></a><span data-ttu-id="c2aa8-160">Supervisión avanzada</span><span class="sxs-lookup"><span data-stu-id="c2aa8-160">Advanced monitoring</span></span> 

<span data-ttu-id="c2aa8-161">Mediante [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) se puede realizar una supervisión más avanzada de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-161">You can do more advanced monitoring of your VM by using [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span></span> <span data-ttu-id="c2aa8-162">Si aún no lo ha hecho, puede suscribirse para disfrutar de una [evaluación gratuita](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) de Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-162">If you haven't already done so, you can sign up for a [free trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) of Operations Management Suite.</span></span>

<span data-ttu-id="c2aa8-163">Cuando se tiene acceso toohello OMS portal, puede encontrar identificador de clave y el área de trabajo del área de trabajo de hello en la hoja de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-163">When you have access toohello OMS portal, you can find hello workspace key and workspace identifier on hello Settings blade.</span></span> <span data-ttu-id="c2aa8-164">Hola de uso [conjunto AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) suministra tootooadd Hola OMS extensión toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-164">Use hello [Set-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) cmmand tootooadd hello OMS extension toohello VM.</span></span> <span data-ttu-id="c2aa8-165">Actualización Hola valores de las variables en hello debajo de ejemplo tooreflect, Id. de área de trabajo y clave de área de trabajo OMS</span><span class="sxs-lookup"><span data-stu-id="c2aa8-165">Update hello variable values in hello below sample tooreflect you OMS workspace key and workspace Id.</span></span>  

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

<span data-ttu-id="c2aa8-166">Después de unos minutos, debería ver Hola nueva máquina virtual en el área de trabajo OMS Hola.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-166">After a few minutes, you should see hello new VM in hello OMS workspace.</span></span> 

![Hoja OMS](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a><span data-ttu-id="c2aa8-168">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c2aa8-168">Next steps</span></span>
<span data-ttu-id="c2aa8-169">En este tutorial, ha configurado y revisado las máquinas virtuales con Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-169">In this tutorial, you configured and reviewed VMs with Azure Security Center.</span></span> <span data-ttu-id="c2aa8-170">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="c2aa8-170">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c2aa8-171">Crear una red virtual</span><span class="sxs-lookup"><span data-stu-id="c2aa8-171">Create a virtual network</span></span>
> * <span data-ttu-id="c2aa8-172">Crear un grupo de recursos y una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c2aa8-172">Create a resource group and VM</span></span> 
> * <span data-ttu-id="c2aa8-173">Habilitar los diagnósticos de arranque en hello VM</span><span class="sxs-lookup"><span data-stu-id="c2aa8-173">Enable boot diagnostics on hello VM</span></span>
> * <span data-ttu-id="c2aa8-174">Ver los diagnósticos de arranque</span><span class="sxs-lookup"><span data-stu-id="c2aa8-174">View boot diagnostics</span></span>
> * <span data-ttu-id="c2aa8-175">Visualización de las métricas del host</span><span class="sxs-lookup"><span data-stu-id="c2aa8-175">View host metrics</span></span>
> * <span data-ttu-id="c2aa8-176">Instalar extensión de diagnósticos de Hola</span><span class="sxs-lookup"><span data-stu-id="c2aa8-176">Install hello diagnostics extension</span></span>
> * <span data-ttu-id="c2aa8-177">Ver las métricas de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c2aa8-177">View VM metrics</span></span>
> * <span data-ttu-id="c2aa8-178">Crear una alerta</span><span class="sxs-lookup"><span data-stu-id="c2aa8-178">Create an alert</span></span>
> * <span data-ttu-id="c2aa8-179">Configurar la supervisión avanzada</span><span class="sxs-lookup"><span data-stu-id="c2aa8-179">Set up advanced monitoring</span></span>

<span data-ttu-id="c2aa8-180">Avanzar toohello siguiente toolearn de tutorial acerca del centro de seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="c2aa8-180">Advance toohello next tutorial toolearn about Azure security center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c2aa8-181">Administración de la seguridad de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="c2aa8-181">Manage VM security</span></span>](./tutorial-azure-security.md)