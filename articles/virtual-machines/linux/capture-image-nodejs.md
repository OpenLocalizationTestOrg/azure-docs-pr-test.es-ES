---
title: "aaaCapture un toouse de máquina virtual de Linux de Azure como una plantilla | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocapture y generalizar una imagen de una basados en Linux Azure máquina virtual (VM) creada con el modelo de implementación de hello Azure Resource Manager."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 877eee5c842bebe80e755c2240cdaaef4ade6ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="capture-a-linux-virtual-machine-running-on-azure"></a><span data-ttu-id="db607-103">Captura de una máquina virtual Linux que se ejecuta en Azure</span><span class="sxs-lookup"><span data-stu-id="db607-103">Capture a Linux virtual machine running on Azure</span></span>
<span data-ttu-id="db607-104">Siga los pasos de hello en este artículo toogeneralize y capturar la máquina virtual de Linux de Azure (VM) en el modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="db607-104">Follow hello steps in this article toogeneralize and capture your Azure Linux virtual machine (VM) in hello Resource Manager deployment model.</span></span> <span data-ttu-id="db607-105">Cuando se generaliza Hola VM, quita información de la cuenta personal y preparar Hola VM toobe utilizado como una imagen.</span><span class="sxs-lookup"><span data-stu-id="db607-105">When you generalize hello VM, you remove personal account information and prepare hello VM toobe used as an image.</span></span> <span data-ttu-id="db607-106">, A continuación, captura la imagen de un disco duro virtual (VHD) generalizado para hello OS, discos duros virtuales en los discos de datos adjuntos, y un [plantilla del Administrador de recursos](../../azure-resource-manager/resource-group-overview.md) para nuevas implementaciones de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="db607-106">You then capture a generalized virtual hard disk (VHD) image for hello OS, VHDs for attached data disks, and a [Resource Manager template](../../azure-resource-manager/resource-group-overview.md) for new VM deployments.</span></span> <span data-ttu-id="db607-107">Este artículo detalla cómo toocapture una máquina virtual de la imagen con hello 1.0 de CLI de Azure para una máquina virtual con discos no administrados.</span><span class="sxs-lookup"><span data-stu-id="db607-107">This article details how toocapture a VM image with hello Azure CLI 1.0 for a VM using unmanaged disks.</span></span> <span data-ttu-id="db607-108">También puede [capturar una máquina virtual mediante discos de Azure administrados con hello Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="db607-108">You can also [capture a VM using Azure Managed Disks with hello Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="db607-109">Discos administrados se controlan mediante la plataforma Windows Azure hello y no requieren ningún toostore los preparativos o ubicación ellos.</span><span class="sxs-lookup"><span data-stu-id="db607-109">Managed disks are handled by hello Azure platform and do not require any preparation or location toostore them.</span></span> <span data-ttu-id="db607-110">Para obtener más información, consulte [Azure Managed Disks overview](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Información general sobre Azure Managed Disks).</span><span class="sxs-lookup"><span data-stu-id="db607-110">For more information, see [Azure Managed Disks overview](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="db607-111">toocreate máquinas virtuales con la imagen de hello, configurar los recursos de red para cada nueva máquina virtual y usar Hola plantilla (un archivo JavaScript Object Notation o JSON,) toodeploy de hello captura imágenes de disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="db607-111">toocreate VMs using hello image, set up network resources for each new VM, and use hello template (a JavaScript Object Notation, or JSON, file) toodeploy it from hello captured VHD images.</span></span> <span data-ttu-id="db607-112">De esta manera, puede replicar una máquina virtual con su actual configuración de software, manera toohello similar que use imágenes en hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="db607-112">In this way, you can replicate a VM with its current software configuration, similar toohello way you use images in hello Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="db607-113">Si desea toocreate una copia de la VM de Linux existente con su estado especializada para la depuración o de copia de seguridad, consulte [crear una copia de una máquina virtual de Linux con Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="db607-113">If you want toocreate a copy of your existing Linux VM with its specialized state for backup or debugging, see [Create a copy of a Linux virtual machine running on Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="db607-114">Si desea tooupload un VHD Linux desde una máquina virtual local vea [cargar y crear una VM Linux de imagen de disco personalizado](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="db607-114">And if you want tooupload a Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>  

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="db607-115">Tarea CLI versiones toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="db607-115">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="db607-116">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="db607-116">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="db607-117">[Azure 1.0 de CLI](#before-you-begin) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)</span><span class="sxs-lookup"><span data-stu-id="db607-117">[Azure CLI 1.0](#before-you-begin) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="db607-118">[Azure 2.0 CLI](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="db607-118">[Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="db607-119">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="db607-119">Before you begin</span></span>
<span data-ttu-id="db607-120">Asegúrese de que se cumple Hola siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="db607-120">Ensure that you meet hello following prerequisites:</span></span>

* <span data-ttu-id="db607-121">**Máquina virtual de Azure creado en el modelo de implementación del Administrador de recursos de hello** -si no ha creado una VM de Linux, puede usar hello [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), hello [CLI de Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), o [el Administrador de recursos plantillas de](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="db607-121">**Azure VM created in hello Resource Manager deployment model** - If you haven't created a Linux VM, you can use hello [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), hello [Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span></span> 
  
    <span data-ttu-id="db607-122">Configurar Hola VM según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="db607-122">Configure hello VM as needed.</span></span> <span data-ttu-id="db607-123">Por ejemplo, [agregue discos de datos](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), aplique actualizaciones e instale aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="db607-123">For example, [add data disks](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), apply updates, and install applications.</span></span> 
* <span data-ttu-id="db607-124">**CLI de Azure** -Install hello [CLI de Azure](../../cli-install-nodejs.md) en un equipo local.</span><span class="sxs-lookup"><span data-stu-id="db607-124">**Azure CLI** - Install hello [Azure CLI](../../cli-install-nodejs.md) on a local computer.</span></span>

## <a name="step-1-remove-hello-azure-linux-agent"></a><span data-ttu-id="db607-125">Paso 1: Quitar el agente de Linux de Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="db607-125">Step 1: Remove hello Azure Linux agent</span></span>
<span data-ttu-id="db607-126">En primer lugar, ejecute hello **waagent** comando con hello **deprovision** parámetro en hello VM de Linux.</span><span class="sxs-lookup"><span data-stu-id="db607-126">First, run hello **waagent** command with hello **deprovision** parameter on hello Linux VM.</span></span> <span data-ttu-id="db607-127">Este comando elimina archivos y datos toomake Hola VM listo para generalizar.</span><span class="sxs-lookup"><span data-stu-id="db607-127">This command deletes files and data toomake hello VM ready for generalizing.</span></span> <span data-ttu-id="db607-128">Para obtener más información, vea hello [manual de usuario del agente Linux de Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="db607-128">For details, see hello [Azure Linux Agent user guide](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

1. <span data-ttu-id="db607-129">Conectar tooyour VM de Linux con un cliente de SSH.</span><span class="sxs-lookup"><span data-stu-id="db607-129">Connect tooyour Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="db607-130">En la ventana de hello SSH, escriba Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="db607-130">In hello SSH window, type hello following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
   > [!NOTE]
   > <span data-ttu-id="db607-131">Solo se ejecute este comando en una máquina virtual que piensa toocapture como una imagen.</span><span class="sxs-lookup"><span data-stu-id="db607-131">Only run this command on a VM that you intend toocapture as an image.</span></span> <span data-ttu-id="db607-132">No se garantiza dicha imagen Hola se borra de toda la información confidencial o es adecuada para su redistribución.</span><span class="sxs-lookup"><span data-stu-id="db607-132">It does not guarantee that hello image is cleared of all sensitive information or is suitable for redistribution.</span></span>
 
3. <span data-ttu-id="db607-133">Tipo de **y** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="db607-133">Type **y** toocontinue.</span></span> <span data-ttu-id="db607-134">Puede agregar hello **-forzar** parámetro tooavoid este paso de confirmación.</span><span class="sxs-lookup"><span data-stu-id="db607-134">You can add hello **-force** parameter tooavoid this confirmation step.</span></span>
4. <span data-ttu-id="db607-135">Una vez completado el comando de hello, escriba **salir**.</span><span class="sxs-lookup"><span data-stu-id="db607-135">After hello command completes, type **exit**.</span></span> <span data-ttu-id="db607-136">Este paso cierra el cliente de SSH Hola.</span><span class="sxs-lookup"><span data-stu-id="db607-136">This step closes hello SSH client.</span></span>

## <a name="step-2-capture-hello-vm"></a><span data-ttu-id="db607-137">Paso 2: Capturar Hola VM</span><span class="sxs-lookup"><span data-stu-id="db607-137">Step 2: Capture hello VM</span></span>
<span data-ttu-id="db607-138">Utilice hello Azure CLI toogeneralize y capturar Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="db607-138">Use hello Azure CLI toogeneralize and capture hello VM.</span></span> <span data-ttu-id="db607-139">En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="db607-139">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="db607-140">Los nombres de parámetro de ejemplo incluyen **myResourceGroup**, **myVnet** y **myVM**.</span><span class="sxs-lookup"><span data-stu-id="db607-140">Example parameter names include **myResourceGroup**, **myVnet**, and **myVM**.</span></span>

1. <span data-ttu-id="db607-141">En el equipo local, abra Hola CLI de Azure y [tooyour suscripción de Azure de inicio de sesión](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="db607-141">From your local computer, open hello Azure CLI and [login tooyour Azure subscription](../../xplat-cli-connect.md).</span></span> 
2. <span data-ttu-id="db607-142">Asegúrese de que está en modo de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="db607-142">Make sure you are in Resource Manager mode.</span></span>
   
    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="db607-143">Apagar la máquina virtual que ya se desaprovisionó utilizando el siguiente comando de Hola Hola:</span><span class="sxs-lookup"><span data-stu-id="db607-143">Shut down hello VM that you already deprovisioned by using hello following command:</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup -n myVM
    ```
4. <span data-ttu-id="db607-144">Generalizar Hola VM con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="db607-144">Generalize hello VM with hello following command:</span></span>
   
    ```azurecli
    azure vm generalize -g myResourceGroup -n myVM
    ```
5. <span data-ttu-id="db607-145">Ahora ejecute hello **captura de máquina virtual de azure** comando, que captura Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="db607-145">Now run hello **azure vm capture** command, which captures hello VM.</span></span> <span data-ttu-id="db607-146">En el siguiente ejemplo de Hola, imagen Hola discos duros virtuales se capturan con nombres empiezan por **MyVHDNamePrefix**, hello y **-t** opción especifica una plantilla de ruta de acceso toohello **MyTemplate.json**.</span><span class="sxs-lookup"><span data-stu-id="db607-146">In hello following example, hello image VHDs are captured with names beginning with **MyVHDNamePrefix**, and hello **-t** option specifies a path toohello template **MyTemplate.json**.</span></span> 
   
    ```azurecli
    azure vm capture -g myResourceGroup -n myVM -p myVHDNamePrefix -t myTemplate.json
    ```
   
   > [!IMPORTANT]
   > <span data-ttu-id="db607-147">archivos de disco duro virtual de imagen de Hello creando de forma predeterminada en hello usa la misma cuenta de almacenamiento que Hola VM original.</span><span class="sxs-lookup"><span data-stu-id="db607-147">hello image VHD files get created by default in hello same storage account that hello original VM used.</span></span> <span data-ttu-id="db607-148">Hola de uso *misma cuenta de almacenamiento* toostore Hola discos duros virtuales para las nuevas máquinas virtuales se crea desde Hola imagen.</span><span class="sxs-lookup"><span data-stu-id="db607-148">Use hello *same storage account* toostore hello VHDs for any new VMs you create from hello image.</span></span> 

6. <span data-ttu-id="db607-149">ubicación de hello toofind de una imagen capturada, plantilla JSON de hello abierto en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="db607-149">toofind hello location of a captured image, open hello JSON template in a text editor.</span></span> <span data-ttu-id="db607-150">Hola **storageProfile**, encontrar Hola **uri** de hello **imagen** ubicado en hello **system** contenedor.</span><span class="sxs-lookup"><span data-stu-id="db607-150">In hello **storageProfile**, find hello **uri** of hello **image** located in hello **system** container.</span></span> <span data-ttu-id="db607-151">Por ejemplo, hello URI de imagen de disco de SO hello es similar demasiado`https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span><span class="sxs-lookup"><span data-stu-id="db607-151">For example, hello URI of hello OS disk image is similar too`https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>

## <a name="step-3-create-a-vm-from-hello-captured-image"></a><span data-ttu-id="db607-152">Paso 3: Crear una máquina virtual desde la imagen de captura de Hola</span><span class="sxs-lookup"><span data-stu-id="db607-152">Step 3: Create a VM from hello captured image</span></span>
<span data-ttu-id="db607-153">Ahora puede usar imagen Hola con un toocreate plantilla una VM de Linux.</span><span class="sxs-lookup"><span data-stu-id="db607-153">Now use hello image with a template toocreate a Linux VM.</span></span> <span data-ttu-id="db607-154">Estos pasos muestran cómo toouse Hola CLI de Azure y Hola plantilla de archivo JSON se capturó toocreate Hola VM en una nueva red virtual.</span><span class="sxs-lookup"><span data-stu-id="db607-154">These steps show you how toouse hello Azure CLI and hello JSON file template you captured toocreate hello VM in a new virtual network.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="db607-155">Crear recursos de red</span><span class="sxs-lookup"><span data-stu-id="db607-155">Create network resources</span></span>
<span data-ttu-id="db607-156">plantilla de hello toouse, primero debe tooset seguridad de una red virtual y la NIC para la nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="db607-156">toouse hello template, you first need tooset up a virtual network and NIC for your new VM.</span></span> <span data-ttu-id="db607-157">Se recomienda que crear un grupo de recursos para estos recursos en lugar de Hola donde se almacena la imagen de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="db607-157">We recommend you create a resource group for these resources in hello location where your VM image is stored.</span></span> <span data-ttu-id="db607-158">Ejecute comandos similar toohello siguientes, sustituyendo los nombres de los recursos y una ubicación de Azure adecuada ("centralus" en estos comandos):</span><span class="sxs-lookup"><span data-stu-id="db607-158">Run commands similar toohello following, substituting names for your resources and an appropriate Azure location ("centralus" in these commands):</span></span>

```azurecli
azure group create myResourceGroup1 -l "centralus"

azure network vnet create myResourceGroup1 myVnet -l "centralus"

azure network vnet subnet create myResourceGroup1 myVnet mySubnet

azure network public-ip create myResourceGroup1 myPublicIP -l "centralus"

azure network nic create myResourceGroup1 myNIC -k mySubnet -m myVnet -p myPublicIP -l "centralus"
```

### <a name="get-hello-id-of-hello-nic"></a><span data-ttu-id="db607-159">Obtener Hola Id. de hello NIC</span><span class="sxs-lookup"><span data-stu-id="db607-159">Get hello Id of hello NIC</span></span>
<span data-ttu-id="db607-160">toodeploy una máquina virtual desde la imagen de hello mediante Hola guardó durante la captura JSON, necesita Hola Id. de hello NIC.</span><span class="sxs-lookup"><span data-stu-id="db607-160">toodeploy a VM from hello image by using hello JSON you saved during capture, you need hello Id of hello NIC.</span></span> <span data-ttu-id="db607-161">Obtenerlo ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="db607-161">Obtain it by running hello following command:</span></span>

```azurecli
azure network nic show myResourceGroup1 myNIC
```

<span data-ttu-id="db607-162">Hola **identificador** Hola salida es similar demasiado`/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`</span><span class="sxs-lookup"><span data-stu-id="db607-162">hello **Id** in hello output is similar too`/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`</span></span>

### <a name="create-a-vm"></a><span data-ttu-id="db607-163">Creación de una VM</span><span class="sxs-lookup"><span data-stu-id="db607-163">Create a VM</span></span>
<span data-ttu-id="db607-164">Ahora la siguiente ejecución Hola comando toocreate la máquina virtual de hello captura la imagen de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="db607-164">Now run hello following command toocreate your VM from hello captured VM image.</span></span> <span data-ttu-id="db607-165">Hola de uso **-f** toohello plantilla JSON de parámetro toospecify Hola ruta de acceso de archivo se guarda.</span><span class="sxs-lookup"><span data-stu-id="db607-165">Use hello **-f** parameter toospecify hello path toohello template JSON file you saved.</span></span>

```azurecli
azure group deployment create myResourceGroup1 MyDeployment -f MyTemplate.json
```

<span data-ttu-id="db607-166">En la salida del comando hello, son toosupply solicitada un nuevo nombre de máquina virtual, nombre de usuario de administrador de hello y una contraseña y Hola Id. de hello NIC que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="db607-166">In hello command output, you are prompted toosupply a new VM name, hello admin user name and password, and hello Id of hello NIC you created previously.</span></span>

```bash
info:    Executing command group deployment create
info:    Supply values for hello following parameters
vmName: myNewVM
adminUserName: myAdminuser
adminPassword: ********
networkInterfaceId: /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resource Groups/myResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
```

<span data-ttu-id="db607-167">Hola siguiendo el ejemplo muestra lo que se ve una implementación correcta:</span><span class="sxs-lookup"><span data-stu-id="db607-167">hello following sample shows what you see for a successful deployment:</span></span>

```bash
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment xxxxxxx
+ Waiting for deployment toocomplete
data:    DeploymentName     : MyDeployment
data:    ResourceGroupName  : MyResourceGroup1
data:    ProvisioningState  : Succeeded
data:    Timestamp          : xxxxxxx
data:    Mode               : Incremental
data:    Name                Type          Value

data:    ------------------  ------------  -------------------------------------

data:    vmName              String        myNewVM

data:    vmSize              String        Standard_D1

data:    adminUserName       String        myAdminuser

data:    adminPassword       SecureString  undefined

data:    networkInterfaceId  String        /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
info:    group deployment create command OK
```

### <a name="verify-hello-deployment"></a><span data-ttu-id="db607-168">Comprobar la implementación de Hola</span><span class="sxs-lookup"><span data-stu-id="db607-168">Verify hello deployment</span></span>
<span data-ttu-id="db607-169">Ahora SSH toohello máquina virtual que creó la implementación de hello tooverify y empezar a usar Hola nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="db607-169">Now SSH toohello virtual machine you created tooverify hello deployment and start using hello new VM.</span></span> <span data-ttu-id="db607-170">tooconnect mediante SSH, buscar la dirección IP de Hola de hello máquina virtual que creó mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="db607-170">tooconnect via SSH, find hello IP address of hello VM you created by running hello following command:</span></span>

```azurecli
azure network public-ip show myResourceGroup1 myPublicIP
```

<span data-ttu-id="db607-171">la dirección IP pública Hola se muestra en la salida del comando Hola.</span><span class="sxs-lookup"><span data-stu-id="db607-171">hello public IP address is listed in hello command output.</span></span> <span data-ttu-id="db607-172">De forma predeterminada se conectará toohello VM de Linux mediante SSH en el puerto 22.</span><span class="sxs-lookup"><span data-stu-id="db607-172">By default you connect toohello Linux VM by SSH on port 22.</span></span>

## <a name="create-additional-vms"></a><span data-ttu-id="db607-173">Creación de máquinas virtuales adicionales</span><span class="sxs-lookup"><span data-stu-id="db607-173">Create additional VMs</span></span>
<span data-ttu-id="db607-174">Hola de uso captura imagen y plantilla toodeploy máquinas virtuales adicionales siguiendo los pasos de Hola Hola sección anterior.</span><span class="sxs-lookup"><span data-stu-id="db607-174">Use hello captured image and template toodeploy additional VMs using hello steps in hello preceding section.</span></span> <span data-ttu-id="db607-175">Otro toocreate máquinas virtuales de opciones de imagen de hello incluyen utilizando una plantilla de inicio rápido o ejecutando hello **crear la máquina virtual de azure** comando.</span><span class="sxs-lookup"><span data-stu-id="db607-175">Other options toocreate VMs from hello image include using a quickstart template or running hello **azure vm create** command.</span></span>

### <a name="use-hello-captured-template"></a><span data-ttu-id="db607-176">Usar plantilla capturada Hola</span><span class="sxs-lookup"><span data-stu-id="db607-176">Use hello captured template</span></span>
<span data-ttu-id="db607-177">Hola toouse captura imagen y plantilla, siga estos pasos (que se detallan en la sección anterior de hello):</span><span class="sxs-lookup"><span data-stu-id="db607-177">toouse hello captured image and template, follow these steps (detailed in hello preceding section):</span></span>

* <span data-ttu-id="db607-178">Asegúrese de que la imagen de máquina virtual está en hello misma cuenta de almacenamiento que hospeda el VHD de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="db607-178">Ensure that your VM image is in hello same storage account that hosts your VM's VHD.</span></span>
* <span data-ttu-id="db607-179">Copie el archivo JSON de hello plantilla y especifique un nombre único para el disco del sistema operativo Hola de hello nueva VM VHD (o discos duros virtuales).</span><span class="sxs-lookup"><span data-stu-id="db607-179">Copy hello template JSON file and specify a unique name for hello OS disk of hello new VM's VHD (or VHDs).</span></span> <span data-ttu-id="db607-180">Por ejemplo, en hello **storageProfile**, en **vhd**, en **uri**, especifique un nombre único para hello **osDisk** VHD, similar demasiado`https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span><span class="sxs-lookup"><span data-stu-id="db607-180">For example, in hello **storageProfile**, under **vhd**, in **uri**, specify a unique name for hello **osDisk** VHD, similar too`https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span></span>
* <span data-ttu-id="db607-181">Cree una NIC en cualquier Hola mismo u otra red virtual.</span><span class="sxs-lookup"><span data-stu-id="db607-181">Create a NIC in either hello same or a different virtual network.</span></span>
* <span data-ttu-id="db607-182">Mediante el archivo JSON de plantilla de hello modificado, cree una implementación en el grupo de recursos de hello en el que configura la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="db607-182">Using hello modified template JSON file, create a deployment in hello resource group in which you set up hello virtual network.</span></span>

### <a name="use-a-quickstart-template"></a><span data-ttu-id="db607-183">Uso de una plantilla de inicio rápido</span><span class="sxs-lookup"><span data-stu-id="db607-183">Use a quickstart template</span></span>
<span data-ttu-id="db607-184">Si desea configurar automáticamente cuando se crea una máquina virtual desde la imagen de Hola de red de hello, puede especificar esos recursos en una plantilla.</span><span class="sxs-lookup"><span data-stu-id="db607-184">If you want hello network set up automatically when you create a VM from hello image, you can specify those resources in a template.</span></span> <span data-ttu-id="db607-185">Por ejemplo, vea hello [plantilla de imagen de máquina virtual de usuario de 101](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="db607-185">For example, see hello [101-vm-from-user-image template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) from GitHub.</span></span> <span data-ttu-id="db607-186">Esta plantilla crea una máquina virtual desde su imagen personalizada y red virtual de hello es necesario, la dirección IP pública y recursos NIC.</span><span class="sxs-lookup"><span data-stu-id="db607-186">This template creates a VM from your custom image and hello necessary virtual network, public IP address, and NIC resources.</span></span> <span data-ttu-id="db607-187">Para ver un tutorial del uso de plantilla de Hola Hola portal de Azure, consulte [cómo toocreate una máquina virtual desde una imagen personalizada con una plantilla de administrador de recursos](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).</span><span class="sxs-lookup"><span data-stu-id="db607-187">For a walkthrough of using hello template in hello Azure portal, see [How toocreate a virtual machine from a custom image using a Resource Manager template](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).</span></span>

### <a name="use-hello-azure-vm-create-command"></a><span data-ttu-id="db607-188">Use hello azure vm create, comando</span><span class="sxs-lookup"><span data-stu-id="db607-188">Use hello azure vm create command</span></span>
<span data-ttu-id="db607-189">Normalmente es más fácil toouse un toocreate de plantilla de administrador de recursos una máquina virtual desde la imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="db607-189">Usually it's easiest toouse a Resource Manager template toocreate a VM from hello image.</span></span> <span data-ttu-id="db607-190">Sin embargo, puede crear Hola VM *imperativamente* mediante el uso de hello **crear la máquina virtual de azure** comando con hello **-Q** (**--imagen urn**) parámetro .</span><span class="sxs-lookup"><span data-stu-id="db607-190">However, you can create hello VM *imperatively* by using hello **azure vm create** command with hello **-Q** (**--image-urn**) parameter.</span></span> <span data-ttu-id="db607-191">Si utiliza este método, también pasar hello **-d** (**vhd del disco de SO--**) Hola de ubicación de hello toospecify de parámetro del archivo .vhd de hello OS para nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="db607-191">If you use this method, you also pass hello **-d** (**--os-disk-vhd**) parameter toospecify hello location of hello OS .vhd file for hello new VM.</span></span> <span data-ttu-id="db607-192">Este archivo debe estar en el contenedor de discos duros virtuales de Hola de cuenta de almacenamiento de Hola donde se almacena el archivo de disco duro virtual de imagen de hello.</span><span class="sxs-lookup"><span data-stu-id="db607-192">This file must be in hello vhds container of hello storage account where hello image VHD file is stored.</span></span> <span data-ttu-id="db607-193">Hola comando copias Hola VHD para hello nueva máquina virtual automáticamente toohello **discos duros virtuales** contenedor.</span><span class="sxs-lookup"><span data-stu-id="db607-193">hello command copies hello VHD for hello new VM automatically toohello **vhds** container.</span></span>

<span data-ttu-id="db607-194">Antes de ejecutar **crear la máquina virtual de azure** con la imagen de hello, completar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="db607-194">Before running **azure vm create** with hello image, complete hello following steps:</span></span>

1. <span data-ttu-id="db607-195">Crear un grupo de recursos o identificar un grupo de recursos existente para la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="db607-195">Create a resource group, or identify an existing resource group for hello deployment.</span></span>
2. <span data-ttu-id="db607-196">Crear un complemento público recurso de dirección IP y un recurso NIC para Hola nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="db607-196">Create a public IP address resource and a NIC resource for hello new VM.</span></span> <span data-ttu-id="db607-197">Para pasos toocreate una red virtual, dirección IP pública y NIC mediante el uso de hello CLI, vea anteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="db607-197">For steps toocreate a virtual network, public IP address, and NIC by using hello CLI, see earlier in this article.</span></span> <span data-ttu-id="db607-198">(**crear la máquina virtual de azure** también se puede crear una NIC, pero debe toopass los parámetros adicionales para una red virtual y subred.)</span><span class="sxs-lookup"><span data-stu-id="db607-198">(**azure vm create** can also create a NIC, but you need toopass additional parameters for a virtual network and subnet.)</span></span>

<span data-ttu-id="db607-199">A continuación, ejecutar un comando que pasa a URI hello existente de la imagen y archivo tooboth Hola de nuevo disco duro virtual del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="db607-199">Then run a command that passes URIs tooboth hello new OS VHD file and hello existing image.</span></span> <span data-ttu-id="db607-200">En este ejemplo, se crea un tamaño de VM de Standard_A1 en la región de hello este de EE..</span><span class="sxs-lookup"><span data-stu-id="db607-200">In this example, a size Standard_A1 VM is created in hello East US region.</span></span>

```azurecli
azure vm create -g myResourceGroup1 -n myNewVM -l eastus -y Linux \
-z Standard_A1 -u myAdminname -p myPassword -f myNIC \
-d "https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix.vhd" \
-Q "https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.vhd"
```

<span data-ttu-id="db607-201">Para obtener opciones de comando adicionales, ejecute `azure help vm create`.</span><span class="sxs-lookup"><span data-stu-id="db607-201">For additional command options, run `azure help vm create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db607-202">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="db607-202">Next steps</span></span>
<span data-ttu-id="db607-203">toomanage las máquinas virtuales con hello CLI, vea tareas de hello en [implementar y administrar máquinas virtuales usando plantillas del Administrador de recursos de Azure y hello Azure CLI](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="db607-203">toomanage your VMs with hello CLI, see hello tasks in [Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI](create-ssh-secured-vm-from-template.md).</span></span>

