---
title: "máquinas virtuales de Linux aaaMonitor en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomonitor arrancar las métricas de rendimiento y diagnóstico en una máquina virtual de Linux en Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 282da0f03ab0bf37bd44750c22813ca8d1c89560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="7ac58-103">¿Cómo toomonitor una máquina virtual de Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="7ac58-103">How toomonitor a Linux virtual machine in Azure</span></span>

<span data-ttu-id="7ac58-104">tooensure que las máquinas virtuales (VM) en Azure se ejecuta correctamente, puede revisar las métricas de rendimiento y diagnóstico de arranque.</span><span class="sxs-lookup"><span data-stu-id="7ac58-104">tooensure your virtual machines (VMs) in Azure are running correctly, you can review boot diagnostics and performance metrics.</span></span> <span data-ttu-id="7ac58-105">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="7ac58-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7ac58-106">Habilitar los diagnósticos de arranque en hello VM</span><span class="sxs-lookup"><span data-stu-id="7ac58-106">Enable boot diagnostics on hello VM</span></span>
> * <span data-ttu-id="7ac58-107">Ver los diagnósticos de arranque</span><span class="sxs-lookup"><span data-stu-id="7ac58-107">View boot diagnostics</span></span>
> * <span data-ttu-id="7ac58-108">Visualización de las métricas del host</span><span class="sxs-lookup"><span data-stu-id="7ac58-108">View host metrics</span></span>
> * <span data-ttu-id="7ac58-109">Habilitar la extensión de diagnósticos en hello VM</span><span class="sxs-lookup"><span data-stu-id="7ac58-109">Enable diagnostics extension on hello VM</span></span>
> * <span data-ttu-id="7ac58-110">Ver las métricas de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="7ac58-110">View VM metrics</span></span>
> * <span data-ttu-id="7ac58-111">Crear alertas basadas en métricas de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="7ac58-111">Create alerts based on diagnostic metrics</span></span>
> * <span data-ttu-id="7ac58-112">Configurar la supervisión avanzada</span><span class="sxs-lookup"><span data-stu-id="7ac58-112">Set up advanced monitoring</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7ac58-113">Si elige tooinstall y usar hello CLI localmente, este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="7ac58-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="7ac58-114">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="7ac58-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="7ac58-115">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7ac58-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-vm"></a><span data-ttu-id="7ac58-116">Creación de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="7ac58-116">Create VM</span></span>

<span data-ttu-id="7ac58-117">toosee diagnósticos y las métricas en acción, necesita una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7ac58-117">toosee diagnostics and metrics in action, you need a VM.</span></span> <span data-ttu-id="7ac58-118">En primer lugar, cree un grupo de recursos con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="7ac58-118">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="7ac58-119">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroupMonitor* en hello *eastus* ubicación.</span><span class="sxs-lookup"><span data-stu-id="7ac58-119">hello following example creates a resource group named *myResourceGroupMonitor* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupMonitor --location eastus
```

<span data-ttu-id="7ac58-120">Ahora cree una máquina virtual con el comando [az vm create](https://docs.microsoft.com/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="7ac58-120">Now create a VM with [az vm create](https://docs.microsoft.com/cli/azure/vm#create).</span></span> <span data-ttu-id="7ac58-121">Hello en el ejemplo siguiente se crea una máquina virtual denominada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="7ac58-121">hello following example creates a VM named *myVM*:</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

## <a name="enable-boot-diagnostics"></a><span data-ttu-id="7ac58-122">Habilitación de los diagnósticos de arranque</span><span class="sxs-lookup"><span data-stu-id="7ac58-122">Enable boot diagnostics</span></span>

<span data-ttu-id="7ac58-123">Como el arranque de máquinas virtuales de Linux, extensión de diagnóstico de arranque de hello captura el resultado de arranque y lo almacena en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="7ac58-123">As Linux VMs boot, hello boot diagnostic extension captures boot output and stores it in Azure storage.</span></span> <span data-ttu-id="7ac58-124">Estos datos pueden ser utilizados tootroubleshoot de problemas de inicio de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7ac58-124">This data can be used tootroubleshoot VM boot issues.</span></span> <span data-ttu-id="7ac58-125">Diagnóstico de arranque no se habilita automáticamente cuando se crea una VM de Linux con hello CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="7ac58-125">Boot diagnostics are not automatically enabled when you create a Linux VM using hello Azure CLI.</span></span>

<span data-ttu-id="7ac58-126">Antes de habilitar el diagnóstico de arranque, una cuenta de almacenamiento debe toobe creado para almacenar archivos de registro de arranque.</span><span class="sxs-lookup"><span data-stu-id="7ac58-126">Before enabling boot diagnostics, a storage account needs toobe created for storing boot logs.</span></span> <span data-ttu-id="7ac58-127">Las cuentas de almacenamiento deben tener un nombre único global, tener entre 3 y 24 caracteres, y deben contener solo números y letras en minúscula.</span><span class="sxs-lookup"><span data-stu-id="7ac58-127">Storage accounts must have a globally unique name, be between 3 and 24 characters, and must contain only numbers and lowercase letters.</span></span> <span data-ttu-id="7ac58-128">Crear una cuenta de almacenamiento con hello [crear cuenta de almacenamiento az](/cli/azure/storage/account#create) comando.</span><span class="sxs-lookup"><span data-stu-id="7ac58-128">Create a storage account with hello [az storage account create](/cli/azure/storage/account#create) command.</span></span> <span data-ttu-id="7ac58-129">En este ejemplo, una cadena aleatoria es toocreate usa un nombre de cuenta de almacenamiento único.</span><span class="sxs-lookup"><span data-stu-id="7ac58-129">In this example, a random string is used toocreate a unique storage account name.</span></span> 

```azurecli-interactive 
storageacct=mydiagdata$RANDOM

az storage account create \
  --resource-group myResourceGroupMonitor \
  --name $storageacct \
  --sku Standard_LRS \
  --location eastus
```

<span data-ttu-id="7ac58-130">Al habilitar el diagnóstico de arranque, se necesita el contenedor de almacenamiento de blobs de hello URI toohello.</span><span class="sxs-lookup"><span data-stu-id="7ac58-130">When enabling boot diagnostics, hello URI toohello blob storage container is needed.</span></span> <span data-ttu-id="7ac58-131">Hello las consultas del comando siguiente Hola tooreturn de cuenta de almacenamiento este URI.</span><span class="sxs-lookup"><span data-stu-id="7ac58-131">hello following command queries hello storage account tooreturn this URI.</span></span> <span data-ttu-id="7ac58-132">Hola valor URI se almacena en los nombres de variable *bloburi*, que se usa en el paso siguiente de saludo.</span><span class="sxs-lookup"><span data-stu-id="7ac58-132">hello URI value is stored in a variable names *bloburi*, which is used in hello next step.</span></span>

```azurecli-interactive 
bloburi=$(az storage account show --resource-group myResourceGroupMonitor --name $storageacct --query 'primaryEndpoints.blob' -o tsv)
```

<span data-ttu-id="7ac58-133">Habilite ahora los diagnósticos de arranque con [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable).</span><span class="sxs-lookup"><span data-stu-id="7ac58-133">Now enable boot diagnostics with [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable).</span></span> <span data-ttu-id="7ac58-134">Hola `--storage` valor es blob Hola URI recopilado en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="7ac58-134">hello `--storage` value is hello blob URI collected in hello previous step.</span></span>

```azurecli-interactive 
az vm boot-diagnostics enable \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --storage $bloburi
```


## <a name="view-boot-diagnostics"></a><span data-ttu-id="7ac58-135">Ver los diagnósticos de arranque</span><span class="sxs-lookup"><span data-stu-id="7ac58-135">View boot diagnostics</span></span>

<span data-ttu-id="7ac58-136">Cuando se habilitan los diagnósticos de arranque, cada vez que detiene e inicia Hola VM, información sobre el proceso de arranque de Hola se escribe tooa archivo de registro.</span><span class="sxs-lookup"><span data-stu-id="7ac58-136">When boot diagnostics are enabled, each time you stop and start hello VM, information about hello boot process is written tooa log file.</span></span> <span data-ttu-id="7ac58-137">En este ejemplo, en primer lugar desasignar Hola VM con hello [cancelar la asignación de máquina virtual az](/cli/azure/vm#deallocate) comando como sigue:</span><span class="sxs-lookup"><span data-stu-id="7ac58-137">For this example, first deallocate hello VM with hello [az vm deallocate](/cli/azure/vm#deallocate) command as follows:</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupMonitor --name myVM
```

<span data-ttu-id="7ac58-138">Iniciar ahora Hola VM con hello [inicio de vm az]( /cli/azure/vm#stop) comando como sigue:</span><span class="sxs-lookup"><span data-stu-id="7ac58-138">Now start hello VM with hello [az vm start]( /cli/azure/vm#stop) command as follows:</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupMonitor --name myVM
```

<span data-ttu-id="7ac58-139">Puede obtener datos de diagnóstico de arranque de Hola para *myVM* con hello [diagnóstico de arranque de vm az get-arranque-log](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) comando como sigue:</span><span class="sxs-lookup"><span data-stu-id="7ac58-139">You can get hello boot diagnostic data for *myVM* with hello [az vm boot-diagnostics get-boot-log](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) command as follows:</span></span>

```azurecli-interactive 
az vm boot-diagnostics get-boot-log --resource-group myResourceGroupMonitor --name myVM
```


## <a name="view-host-metrics"></a><span data-ttu-id="7ac58-140">Visualización de las métricas del host</span><span class="sxs-lookup"><span data-stu-id="7ac58-140">View host metrics</span></span>

<span data-ttu-id="7ac58-141">Una máquina virtual Linux tiene un host dedicado de Azure que interactúa con.</span><span class="sxs-lookup"><span data-stu-id="7ac58-141">A Linux VM has a dedicated host in Azure that it interacts with.</span></span> <span data-ttu-id="7ac58-142">Las métricas se recopilan automáticamente para el host de Hola y pueden verse en hello portal de Azure como sigue:</span><span class="sxs-lookup"><span data-stu-id="7ac58-142">Metrics are automatically collected for hello host and can be viewed in hello Azure portal as follows:</span></span>

1. <span data-ttu-id="7ac58-143">Hola portal de Azure, haga clic en **grupos de recursos**, seleccione **myResourceGroupMonitor**y, a continuación, seleccione **myVM** en la lista de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7ac58-143">In hello Azure portal, click **Resource Groups**, select **myResourceGroupMonitor**, and then select **myVM** in hello resource list.</span></span>
1. <span data-ttu-id="7ac58-144">toosee cómo está realizando la máquina virtual del host de hello, haga clic en **métricas** en la hoja de la máquina virtual de hello, a continuación, seleccione cualquiera de hello *[Host]* métricas en **métricas disponibles**.</span><span class="sxs-lookup"><span data-stu-id="7ac58-144">toosee how hello host VM is performing, click **Metrics** on hello VM blade, then select any of hello *[Host]* metrics under **Available metrics**.</span></span>

    ![Visualización de las métricas del host](./media/tutorial-monitoring/monitor-host-metrics.png)


## <a name="install-diagnostics-extension"></a><span data-ttu-id="7ac58-146">Instalar la extensión de Diagnostics</span><span class="sxs-lookup"><span data-stu-id="7ac58-146">Install diagnostics extension</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7ac58-147">Este documento describe la versión 2.3 de hello extensión de diagnóstico de Linux, que está en desuso.</span><span class="sxs-lookup"><span data-stu-id="7ac58-147">This document describes version 2.3 of hello Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="7ac58-148">Se admitirá la versión 2.3 hasta el 30 de junio de 2018.</span><span class="sxs-lookup"><span data-stu-id="7ac58-148">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="7ac58-149">Versión 3.0 de hello que extensión de diagnóstico de Linux pueden habilitarse en su lugar.</span><span class="sxs-lookup"><span data-stu-id="7ac58-149">Version 3.0 of hello Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="7ac58-150">Para obtener más información, consulte [Hola documentación](./diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="7ac58-150">For more information, see [hello documentation](./diagnostic-extension.md).</span></span>

<span data-ttu-id="7ac58-151">métricas de host básica Hello están disponibles, pero toosee más granular y métricas específica de la máquina virtual, se tooneed tooinstall hello Azure extensión de diagnósticos en hello VM.</span><span class="sxs-lookup"><span data-stu-id="7ac58-151">hello basic host metrics are available, but toosee more granular and VM-specific metrics, you tooneed tooinstall hello Azure diagnostics extension on hello VM.</span></span> <span data-ttu-id="7ac58-152">Hola extensión de diagnósticos de Azure permite toobe de datos de diagnóstico recuperados de hello VM y supervisión adicional.</span><span class="sxs-lookup"><span data-stu-id="7ac58-152">hello Azure diagnostics extension allows additional monitoring and diagnostics data toobe retrieved from hello VM.</span></span> <span data-ttu-id="7ac58-153">Puede ver estas métricas de rendimiento y crear alertas basadas en cómo realiza Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7ac58-153">You can view these performance metrics and create alerts based on how hello VM performs.</span></span> <span data-ttu-id="7ac58-154">extensión de diagnóstico de Hola se instala a través de hello portal de Azure como sigue:</span><span class="sxs-lookup"><span data-stu-id="7ac58-154">hello diagnostic extension is installed through hello Azure portal as follows:</span></span>

1. <span data-ttu-id="7ac58-155">Hola portal de Azure, haga clic en **grupos de recursos**, seleccione **myResourceGroup**y, a continuación, seleccione **myVM** en la lista de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7ac58-155">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
1. <span data-ttu-id="7ac58-156">Haga clic en **Configuración de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="7ac58-156">Click **Diagnosis settings**.</span></span> <span data-ttu-id="7ac58-157">lista de Hello muestra que *diagnósticos de arranque* ya están habilitados desde la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="7ac58-157">hello list shows that *Boot diagnostics* are already enabled from hello previous section.</span></span> <span data-ttu-id="7ac58-158">Haga clic en la casilla de verificación hello *métricas básicas*.</span><span class="sxs-lookup"><span data-stu-id="7ac58-158">Click hello check box for *Basic metrics*.</span></span>
1. <span data-ttu-id="7ac58-159">Hola *cuenta de almacenamiento* sección, examinar Hola seleccione tooand *mydiagdata [1234]* cuenta creada en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="7ac58-159">In hello *Storage account* section, browse tooand select hello *mydiagdata[1234]* account created in hello previous section.</span></span>
1. <span data-ttu-id="7ac58-160">Haga clic en hello **guardar** botón.</span><span class="sxs-lookup"><span data-stu-id="7ac58-160">Click hello **Save** button.</span></span>

    ![Ver métricas de diagnósticos](./media/tutorial-monitoring/enable-diagnostics-extension.png)


## <a name="view-vm-metrics"></a><span data-ttu-id="7ac58-162">Ver las métricas de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="7ac58-162">View VM metrics</span></span>

<span data-ttu-id="7ac58-163">Puede ver las métricas de máquina virtual de Hola Hola igual que ver las métricas de máquina virtual de host de hello:</span><span class="sxs-lookup"><span data-stu-id="7ac58-163">You can view hello VM metrics in hello same way that you viewed hello host VM metrics:</span></span>

1. <span data-ttu-id="7ac58-164">Hola portal de Azure, haga clic en **grupos de recursos**, seleccione **myResourceGroup**y, a continuación, seleccione **myVM** en la lista de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7ac58-164">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
1. <span data-ttu-id="7ac58-165">toosee cómo está realizando Hola VM, haga clic en **métricas** en Hola hoja de la máquina virtual y, a continuación, seleccione cualquiera de las métricas de diagnóstico de hello en **métricas disponibles**.</span><span class="sxs-lookup"><span data-stu-id="7ac58-165">toosee how hello VM is performing, click **Metrics** on hello VM blade, and then select any of hello diagnostics metrics under **Available metrics**.</span></span>

    ![Ver las métricas de la máquina virtual](./media/tutorial-monitoring/monitor-vm-metrics.png)


## <a name="create-alerts"></a><span data-ttu-id="7ac58-167">Creación de alertas</span><span class="sxs-lookup"><span data-stu-id="7ac58-167">Create alerts</span></span>

<span data-ttu-id="7ac58-168">Puede crear alertas basadas en métricas de rendimiento concretas.</span><span class="sxs-lookup"><span data-stu-id="7ac58-168">You can create alerts based on specific performance metrics.</span></span> <span data-ttu-id="7ac58-169">Las alertas pueden ser usado toonotify cuando uso medio de CPU supera un determinado umbral o espacio en disco disponible cae por debajo de una determinada cantidad, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="7ac58-169">Alerts can be used toonotify you when average CPU usage exceeds a certain threshold or available free disk space drops below a certain amount, for example.</span></span> <span data-ttu-id="7ac58-170">Las alertas se muestran en el portal de Azure de Hola o se pueden enviar por correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="7ac58-170">Alerts are displayed in hello Azure portal or can be sent via email.</span></span> <span data-ttu-id="7ac58-171">También puede desencadenar runbooks de automatización de Azure o las aplicaciones lógicas de Azure en tooalerts de respuesta que se está generando.</span><span class="sxs-lookup"><span data-stu-id="7ac58-171">You can also trigger Azure Automation runbooks or Azure Logic Apps in response tooalerts being generated.</span></span>

<span data-ttu-id="7ac58-172">Hello en el ejemplo siguiente se crea una alerta para el uso medio de CPU.</span><span class="sxs-lookup"><span data-stu-id="7ac58-172">hello following example creates an alert for average CPU usage.</span></span>

1. <span data-ttu-id="7ac58-173">Hola portal de Azure, haga clic en **grupos de recursos**, seleccione **myResourceGroup**y, a continuación, seleccione **myVM** en la lista de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7ac58-173">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="7ac58-174">Haga clic en **reglas de alerta** en la hoja de la máquina virtual de hello, a continuación, haga clic en **Agregar alerta métrica** a través de la parte superior de Hola de hoja de alertas de Hola.</span><span class="sxs-lookup"><span data-stu-id="7ac58-174">Click **Alert rules** on hello VM blade, then click **Add metric alert** across hello top of hello alerts blade.</span></span>
4. <span data-ttu-id="7ac58-175">Especifique un **nombre** para la alerta, como *myAlertRule*.</span><span class="sxs-lookup"><span data-stu-id="7ac58-175">Provide a **Name** for your alert, such as *myAlertRule*</span></span>
5. <span data-ttu-id="7ac58-176">tootrigger una alerta cuando el porcentaje de CPU supera 1.0 durante cinco minutos, deje Hola todos los demás valores predeterminados seleccionados.</span><span class="sxs-lookup"><span data-stu-id="7ac58-176">tootrigger an alert when CPU percentage exceeds 1.0 for five minutes, leave all hello other defaults selected.</span></span>
6. <span data-ttu-id="7ac58-177">Si lo desea, active casilla de Hola para *correo electrónico a los propietarios, contributors y readers* toosend notificación de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="7ac58-177">Optionally, check hello box for *Email owners, contributors, and readers* toosend email notification.</span></span> <span data-ttu-id="7ac58-178">acción predeterminada de Hello es toopresent una notificación en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="7ac58-178">hello default action is toopresent a notification in hello portal.</span></span>
7. <span data-ttu-id="7ac58-179">Haga clic en hello **Aceptar** botón.</span><span class="sxs-lookup"><span data-stu-id="7ac58-179">Click hello **OK** button.</span></span>


## <a name="advanced-monitoring"></a><span data-ttu-id="7ac58-180">Supervisión avanzada</span><span class="sxs-lookup"><span data-stu-id="7ac58-180">Advanced monitoring</span></span> 

<span data-ttu-id="7ac58-181">Mediante [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) se puede realizar una supervisión más avanzada de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7ac58-181">You can do more advanced monitoring of your VM by using [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span></span> <span data-ttu-id="7ac58-182">Si aún no lo ha hecho, puede suscribirse para disfrutar de una [evaluación gratuita](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) de Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="7ac58-182">If you haven't already done so, you can sign up for a [free trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) of Operations Management Suite.</span></span>

<span data-ttu-id="7ac58-183">Cuando se tiene acceso toohello OMS portal, puede encontrar identificador de clave y el área de trabajo del área de trabajo de hello en la hoja de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="7ac58-183">When you have access toohello OMS portal, you can find hello workspace key and workspace identifier on hello Settings blade.</span></span> <span data-ttu-id="7ac58-184">Reemplace < clave de área de trabajo > y < Id. de área de trabajo > con valores de hello para de la OMS puede usar el área de trabajo y, a continuación, **conjunto de extensión de vm az** tooadd Hola OMS extensión toohello VM:</span><span class="sxs-lookup"><span data-stu-id="7ac58-184">Replace <workspace-key> and <workspace-id> with hello values for from your OMS workspace and then you can use **az vm extension set** tooadd hello OMS extension toohello VM:</span></span>

```azurecli-interactive 
az vm extension set \
  --resource-group myResourceGroupMonitor \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.3 \
  --protected-settings '{"workspaceKey": "<workspace-key>"}' \
  --settings '{"workspaceId": "<workspace-id>"}'
```

<span data-ttu-id="7ac58-185">En la hoja de búsqueda de registros de Hola de portal de OMS hello, debería ver *myVM* como lo que se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="7ac58-185">On hello Log Search blade of hello OMS portal, you should see *myVM* such as what is shown in hello following picture:</span></span>

![Hoja OMS](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a><span data-ttu-id="7ac58-187">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7ac58-187">Next steps</span></span>

<span data-ttu-id="7ac58-188">En este tutorial, ha configurado y revisado las máquinas virtuales con Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="7ac58-188">In this tutorial, you configured and reviewed VMs with Azure Security Center.</span></span> <span data-ttu-id="7ac58-189">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="7ac58-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7ac58-190">Habilitar los diagnósticos de arranque en hello VM</span><span class="sxs-lookup"><span data-stu-id="7ac58-190">Enable boot diagnostics on hello VM</span></span>
> * <span data-ttu-id="7ac58-191">Ver los diagnósticos de arranque</span><span class="sxs-lookup"><span data-stu-id="7ac58-191">View boot diagnostics</span></span>
> * <span data-ttu-id="7ac58-192">Visualización de las métricas del host</span><span class="sxs-lookup"><span data-stu-id="7ac58-192">View host metrics</span></span>
> * <span data-ttu-id="7ac58-193">Habilitar la extensión de diagnósticos en hello VM</span><span class="sxs-lookup"><span data-stu-id="7ac58-193">Enable diagnostics extension on hello VM</span></span>
> * <span data-ttu-id="7ac58-194">Ver las métricas de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="7ac58-194">View VM metrics</span></span>
> * <span data-ttu-id="7ac58-195">Crear alertas basadas en métricas de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="7ac58-195">Create alerts based on diagnostic metrics</span></span>
> * <span data-ttu-id="7ac58-196">Configurar la supervisión avanzada</span><span class="sxs-lookup"><span data-stu-id="7ac58-196">Set up advanced monitoring</span></span>

<span data-ttu-id="7ac58-197">Avanzar toohello siguiente toolearn de tutorial acerca del centro de seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="7ac58-197">Advance toohello next tutorial toolearn about Azure security center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7ac58-198">Administración de la seguridad de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="7ac58-198">Manage VM security</span></span>](./tutorial-azure-security.md)