---
title: una imagen de una VM de Linux en Azure con CLI 2.0 aaaCapture | Documentos de Microsoft
description: "Capturar una imagen de un toouse de máquina virtual de Azure para implementaciones masivas mediante Hola 2.0 de CLI de Azure."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: 9558332a86186b282775097428df462709373012
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-image-of-a-virtual-machine-or-vhd"></a><span data-ttu-id="fd69f-103">¿Cómo toocreate una imagen de una máquina virtual o un disco duro virtual</span><span class="sxs-lookup"><span data-stu-id="fd69f-103">How toocreate an image of a virtual machine or VHD</span></span>

<!-- generalize, image - extended version of hello tutorial-->

<span data-ttu-id="fd69f-104">toocreate varias copias de una máquina virtual (VM) toouse en Azure, capturar una imagen de VM de Hola u Hola VHD de sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="fd69f-104">toocreate multiple copies of a virtual machine (VM) toouse in Azure, capture an image of hello VM or hello OS VHD.</span></span> <span data-ttu-id="fd69f-105">toocreate una imagen, necesita quitar información de cuenta personal que resulta más seguro toodeploy varias veces.</span><span class="sxs-lookup"><span data-stu-id="fd69f-105">toocreate an image, you need remove personal account information which makes it safer toodeploy multiple times.</span></span> <span data-ttu-id="fd69f-106">Hola siguiendo los pasos que se cancela el aprovisionamiento de una máquina virtual existente, cancelar la asignación y crear una imagen.</span><span class="sxs-lookup"><span data-stu-id="fd69f-106">In hello following steps you deprovision an existing VM, deallocate and create an image.</span></span> <span data-ttu-id="fd69f-107">Puede usar esta imagen toocreate máquinas virtuales a través de cualquier grupo de recursos dentro de su suscripción.</span><span class="sxs-lookup"><span data-stu-id="fd69f-107">You can use this image toocreate VMs across any resource group within your subscription.</span></span>

<span data-ttu-id="fd69f-108">Si desea toocreate una copia de la VM de Linux existentes para copia de seguridad o la depuración, o cargar un VHD de Linux especializadas de una máquina virtual local, vea [cargar y crear una VM Linux de imagen de disco personalizado](upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="fd69f-108">If you want toocreate a copy of your existing Linux VM for backup or debugging, or upload a specialized Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md).</span></span>  

<span data-ttu-id="fd69f-109">También puede usar **compresor** toocreate su configuración personalizada.</span><span class="sxs-lookup"><span data-stu-id="fd69f-109">You can also use **Packer** toocreate your custom configuration.</span></span> <span data-ttu-id="fd69f-110">Para obtener más información sobre el uso de compresor, consulte [cómo imágenes de máquina virtual de toouse compresor toocreate Linux de Azure](build-image-with-packer.md).</span><span class="sxs-lookup"><span data-stu-id="fd69f-110">For more information on using Packer, see [How toouse Packer toocreate Linux virtual machine images in Azure](build-image-with-packer.md).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="fd69f-111">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="fd69f-111">Before you begin</span></span>
<span data-ttu-id="fd69f-112">Asegúrese de que se cumple Hola siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="fd69f-112">Ensure that you meet hello following prerequisites:</span></span>

* <span data-ttu-id="fd69f-113">Necesita una máquina virtual de Azure creados en el modelo de implementación de administrador de recursos de hello mediante discos administrados.</span><span class="sxs-lookup"><span data-stu-id="fd69f-113">You need an Azure VM created in hello Resource Manager deployment model using managed disks.</span></span> <span data-ttu-id="fd69f-114">Si no ha creado una VM de Linux, puede usar hello [portal](quick-create-portal.md), hello [CLI de Azure](quick-create-cli.md), o [plantillas del Administrador de recursos](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="fd69f-114">If you haven't created a Linux VM, you can use hello [portal](quick-create-portal.md), hello [Azure CLI](quick-create-cli.md), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span></span> <span data-ttu-id="fd69f-115">Configurar Hola VM según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="fd69f-115">Configure hello VM as needed.</span></span> <span data-ttu-id="fd69f-116">Por ejemplo, [agregue discos de datos](add-disk.md), aplique actualizaciones e instale aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="fd69f-116">For example, [add data disks](add-disk.md), apply updates, and install applications.</span></span> 

* <span data-ttu-id="fd69f-117">También necesita toohave hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y haber iniciado sesión tooan cuenta de Azure con [inicio de sesión de az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="fd69f-117">You also need toohave hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and be logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="fd69f-118">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="fd69f-118">Quick commands</span></span>

<span data-ttu-id="fd69f-119">Para una versión simplificada de este tema, para las pruebas, evaluar o de aprendizaje sobre máquinas virtuales en Azure, consulte [crear una imagen personalizada de una máquina virtual de Azure con hello CLI](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="fd69f-119">For a simplified version of this topic, for testing, evaluating or learning about VMs in Azure, see [Create a custom image of an Azure VM using hello CLI](tutorial-custom-images.md).</span></span>


## <a name="step-1-deprovision-hello-vm"></a><span data-ttu-id="fd69f-120">Paso 1: Desaprovisionar Hola VM</span><span class="sxs-lookup"><span data-stu-id="fd69f-120">Step 1: Deprovision hello VM</span></span>
<span data-ttu-id="fd69f-121">Cancela el aprovisionamiento de hello VM utilizando el agente de máquina virtual de Azure de hello, archivos específicos de máquina de toodelete y datos.</span><span class="sxs-lookup"><span data-stu-id="fd69f-121">You deprovision hello VM, using hello Azure VM agent, toodelete machine specific files and data.</span></span> <span data-ttu-id="fd69f-122">Hola de uso `waagent` comando con hello *-desaprovisionamiento + usuario* parámetro en el origen de VM de Linux.</span><span class="sxs-lookup"><span data-stu-id="fd69f-122">Use hello `waagent` command with hello *-deprovision+user* parameter on your source Linux VM.</span></span> <span data-ttu-id="fd69f-123">Para obtener más información, vea hello [manual de usuario del agente Linux de Azure](../windows/agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="fd69f-123">For more information, see hello [Azure Linux Agent user guide](../windows/agent-user-guide.md).</span></span>

1. <span data-ttu-id="fd69f-124">Conectar tooyour VM de Linux con un cliente de SSH.</span><span class="sxs-lookup"><span data-stu-id="fd69f-124">Connect tooyour Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="fd69f-125">En la ventana de hello SSH, escriba Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="fd69f-125">In hello SSH window, type hello following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
<br>
   > [!NOTE]
   > <span data-ttu-id="fd69f-126">Solo se ejecute este comando en una máquina virtual que piensa toocapture como una imagen.</span><span class="sxs-lookup"><span data-stu-id="fd69f-126">Only run this command on a VM that you intend toocapture as an image.</span></span> <span data-ttu-id="fd69f-127">No se garantiza dicha imagen Hola se borra de toda la información confidencial o es adecuada para su redistribución.</span><span class="sxs-lookup"><span data-stu-id="fd69f-127">It does not guarantee that hello image is cleared of all sensitive information or is suitable for redistribution.</span></span> <span data-ttu-id="fd69f-128">Hola *+ usuario* parámetro también elimina la última cuenta de usuario aprovisionado Hola.</span><span class="sxs-lookup"><span data-stu-id="fd69f-128">hello *+user* parameter also removes hello last provisioned user account.</span></span> <span data-ttu-id="fd69f-129">Si desea que las credenciales de cuenta de tookeep Hola VM, use *-deprovision* tooleave cuenta de usuario de hello en su lugar.</span><span class="sxs-lookup"><span data-stu-id="fd69f-129">If you want tookeep account credentials in hello VM, just use *-deprovision* tooleave hello user account in place.</span></span>
 
3. <span data-ttu-id="fd69f-130">Tipo de **y** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="fd69f-130">Type **y** toocontinue.</span></span> <span data-ttu-id="fd69f-131">Puede agregar hello **-forzar** parámetro tooavoid este paso de confirmación.</span><span class="sxs-lookup"><span data-stu-id="fd69f-131">You can add hello **-force** parameter tooavoid this confirmation step.</span></span>
4. <span data-ttu-id="fd69f-132">Una vez completado el comando de hello, escriba **salir**.</span><span class="sxs-lookup"><span data-stu-id="fd69f-132">After hello command completes, type **exit**.</span></span> <span data-ttu-id="fd69f-133">Este paso cierra el cliente de SSH Hola.</span><span class="sxs-lookup"><span data-stu-id="fd69f-133">This step closes hello SSH client.</span></span>

## <a name="step-2-create-vm-image"></a><span data-ttu-id="fd69f-134">Paso 2: Crear la imagen de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="fd69f-134">Step 2: Create VM image</span></span>
<span data-ttu-id="fd69f-135">Utilice Hola CLI de Azure 2.0 toomark Hola VM tal y como se ha generalizado y capturar imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd69f-135">Use hello Azure CLI 2.0 toomark hello VM as generalized and capture hello image.</span></span> <span data-ttu-id="fd69f-136">En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="fd69f-136">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="fd69f-137">Los nombres de parámetro de ejemplo incluyen *myResourceGroup*, *myVnet* y *myVM*.</span><span class="sxs-lookup"><span data-stu-id="fd69f-137">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

1. <span data-ttu-id="fd69f-138">Cancela la asignación de hello máquina virtual que canceló el aprovisionamiento con [cancelar la asignación de máquina virtual az](/cli//azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="fd69f-138">Deallocate hello VM that you deprovisioned with [az vm deallocate](/cli//azure/vm#deallocate).</span></span> <span data-ttu-id="fd69f-139">Hello en el ejemplo siguiente se desasigna Hola máquina virtual denominada *myVM* en grupo de recursos de hello llamado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="fd69f-139">hello following example deallocates hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>
   
    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myVM
    ```

2. <span data-ttu-id="fd69f-140">Hola marca VM tal y como se ha generalizado con [az vm generalizar](/cli//azure/vm#generalize).</span><span class="sxs-lookup"><span data-stu-id="fd69f-140">Mark hello VM as generalized with [az vm generalize](/cli//azure/vm#generalize).</span></span> <span data-ttu-id="fd69f-141">Hola después de la máquina virtual denominada ejemplo marcas Hola Hola *myVM* en grupo de recursos de hello llamado *myResourceGroup* como generalizado:</span><span class="sxs-lookup"><span data-stu-id="fd69f-141">hello following example marks hello hello VM named *myVM* in hello resource group named *myResourceGroup* as generalized:</span></span>
   
    ```azurecli
    az vm generalize \
      --resource-group myResourceGroup \
      --name myVM
    ```

3. <span data-ttu-id="fd69f-142">Ahora cree una imagen del recurso de la máquina virtual de hello con [crear imagen az](/cli//azure/image#create).</span><span class="sxs-lookup"><span data-stu-id="fd69f-142">Now create an image of hello VM resource with [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="fd69f-143">Hello en el ejemplo siguiente se crea una imagen denominada *myImage* en grupo de recursos de hello llamado *myResourceGroup* utilizando el recurso de máquina virtual de hello denominado *myVM*:</span><span class="sxs-lookup"><span data-stu-id="fd69f-143">hello following example creates an image named *myImage* in hello resource group named *myResourceGroup* using hello VM resource named *myVM*:</span></span>
   
    ```azurecli
    az image create \
      --resource-group myResourceGroup \
      --name myImage --source myVM
    ```
   
   > [!NOTE]
   > <span data-ttu-id="fd69f-144">Hello imagen se crea en Hola mismo grupo de recursos que la máquina virtual de origen.</span><span class="sxs-lookup"><span data-stu-id="fd69f-144">hello image is created in hello same resource group as your source VM.</span></span> <span data-ttu-id="fd69f-145">Puede crear VM en cualquier grupo de recursos dentro de la suscripción a partir de esta imagen.</span><span class="sxs-lookup"><span data-stu-id="fd69f-145">You can create VMs in any resource group within your subscription from this image.</span></span> <span data-ttu-id="fd69f-146">Desde una perspectiva de administración, es recomendable toocreate un grupo de recursos específicos para los recursos de máquina virtual y las imágenes.</span><span class="sxs-lookup"><span data-stu-id="fd69f-146">From a management perspective, you may wish toocreate a specific resource group for your VM resources and images.</span></span>

## <a name="step-3-create-a-vm-from-hello-captured-image"></a><span data-ttu-id="fd69f-147">Paso 3: Crear una máquina virtual desde la imagen de captura de Hola</span><span class="sxs-lookup"><span data-stu-id="fd69f-147">Step 3: Create a VM from hello captured image</span></span>
<span data-ttu-id="fd69f-148">Crear una máquina virtual mediante la imagen de hello creadas con [crear vm az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="fd69f-148">Create a VM using hello image you created with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="fd69f-149">Hello en el ejemplo siguiente se crea una máquina virtual denominada *myVMDeployed* de imagen de hello denominada *myImage*:</span><span class="sxs-lookup"><span data-stu-id="fd69f-149">hello following example creates a VM named *myVMDeployed* from hello image named *myImage*:</span></span>

```azurecli
az vm create \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --image myImage\
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```

### <a name="creating-hello-vm-in-another-resource-group"></a><span data-ttu-id="fd69f-150">Creación de hello VM en otro grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="fd69f-150">Creating hello VM in another resource group</span></span> 

<span data-ttu-id="fd69f-151">Puede crear máquinas virtuales en cualquier grupo de recursos dentro de la suscripción a partir de una imagen.</span><span class="sxs-lookup"><span data-stu-id="fd69f-151">You can create VMs from an image in any resource group within your subscription.</span></span> <span data-ttu-id="fd69f-152">toocreate una máquina virtual en otro grupo de recursos de imagen de hello, especifique la imagen de tooyour de Id. de completa a recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd69f-152">toocreate a VM in a different resource group than hello image, specify hello full resource ID tooyour image.</span></span> <span data-ttu-id="fd69f-153">Use [lista de imágenes de az](/cli/azure/image#list) tooview una lista de imágenes.</span><span class="sxs-lookup"><span data-stu-id="fd69f-153">Use [az image list](/cli/azure/image#list) tooview a list of images.</span></span> <span data-ttu-id="fd69f-154">Hola de salida es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fd69f-154">hello output is similar toohello following example:</span></span>

```json
"id": "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage",
   "location": "westus",
   "name": "myImage",
```

<span data-ttu-id="fd69f-155">Hello siguiente ejemplo se utiliza [crear vm az](/cli/azure/vm#create) toocreate una máquina virtual en otro grupo de recursos de imagen de origen de hello especificando el identificador de recurso de imagen de hello:</span><span class="sxs-lookup"><span data-stu-id="fd69f-155">hello following example uses [az vm create](/cli/azure/vm#create) toocreate a VM in a different resource group than hello source image by specifying hello image resource ID:</span></span>

```azurecli
az vm create \
   --resource-group myOtherResourceGroup \
   --name myOtherVMDeployed \
   --image "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage" \
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```


## <a name="step-4-verify-hello-deployment"></a><span data-ttu-id="fd69f-156">Paso 4: Comprobar la implementación de Hola</span><span class="sxs-lookup"><span data-stu-id="fd69f-156">Step 4: Verify hello deployment</span></span>

<span data-ttu-id="fd69f-157">Ahora SSH toohello máquina virtual que creó la implementación de hello tooverify y empezar a usar Hola nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fd69f-157">Now SSH toohello virtual machine you created tooverify hello deployment and start using hello new VM.</span></span> <span data-ttu-id="fd69f-158">tooconnect mediante SSH, buscar la dirección IP de Hola o el FQDN de la máquina virtual con [mostrar de la máquina virtual de az](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="fd69f-158">tooconnect via SSH, find hello IP address or FQDN of your VM with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --show-details
```

## <a name="next-steps"></a><span data-ttu-id="fd69f-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fd69f-159">Next steps</span></span>
<span data-ttu-id="fd69f-160">Puede crear varias VM a partir de la imagen de VM de origen.</span><span class="sxs-lookup"><span data-stu-id="fd69f-160">You can create multiple VMs from your source VM image.</span></span> <span data-ttu-id="fd69f-161">Si necesita que la imagen de tooyour de toomake cambios:</span><span class="sxs-lookup"><span data-stu-id="fd69f-161">If you need toomake changes tooyour image:</span></span> 

- <span data-ttu-id="fd69f-162">Cree una máquina virtual a partir de la imagen.</span><span class="sxs-lookup"><span data-stu-id="fd69f-162">Create a VM from your image.</span></span>
- <span data-ttu-id="fd69f-163">Realice actualizaciones o cambios de configuración.</span><span class="sxs-lookup"><span data-stu-id="fd69f-163">Make any updates or configuration changes.</span></span>
- <span data-ttu-id="fd69f-164">Siga Hola nuevo pasos toodeprovision, cancelar la asignación, generalizar y crear una imagen.</span><span class="sxs-lookup"><span data-stu-id="fd69f-164">Follow hello steps again toodeprovision, deallocate, generalize, and create an image.</span></span>
- <span data-ttu-id="fd69f-165">Use esta nueva imagen para implementaciones futuras.</span><span class="sxs-lookup"><span data-stu-id="fd69f-165">Use this new image for future deployments.</span></span> <span data-ttu-id="fd69f-166">Si lo desea, elimine la imagen original Hola.</span><span class="sxs-lookup"><span data-stu-id="fd69f-166">If desired, delete hello original image.</span></span>

<span data-ttu-id="fd69f-167">Para obtener más información acerca de cómo administrar las máquinas virtuales con hello CLI, consulte [CLI de Azure 2.0](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fd69f-167">For more information on managing your VMs with hello CLI, see [Azure CLI 2.0](/cli/azure/overview).</span></span>