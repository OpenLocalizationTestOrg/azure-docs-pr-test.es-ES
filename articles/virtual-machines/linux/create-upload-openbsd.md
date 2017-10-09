---
title: aaaCreate y cargar una VM OpenBSD imagen tooAzure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate y cargar un disco duro virtual (VHD) que contiene Hola OpenBSD sistema operativo toocreate una máquina virtual de Azure a través de la CLI de Azure"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: kyliel
ms.openlocfilehash: 0524f45ea1ecec37e55cbe9d54438a571a831de7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-an-openbsd-disk-image-tooazure"></a><span data-ttu-id="9a38a-103">Crear y cargar un tooAzure de imagen de disco OpenBSD</span><span class="sxs-lookup"><span data-stu-id="9a38a-103">Create and Upload an OpenBSD disk image tooAzure</span></span>
<span data-ttu-id="9a38a-104">Este artículo muestra cómo toocreate y cargar un disco duro virtual (VHD) que contiene Hola OpenBSD sistema de operativo.</span><span class="sxs-lookup"><span data-stu-id="9a38a-104">This article shows you how toocreate and upload a virtual hard disk (VHD) that contains hello OpenBSD operating system.</span></span> <span data-ttu-id="9a38a-105">Después de cargarlo, puede usarlo como su propia toocreate imagen una máquina virtual (VM) en Azure a través de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="9a38a-105">After you upload it, you can use it as your own image toocreate a virtual machine (VM) in Azure through Azure CLI.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="9a38a-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9a38a-106">Prerequisites</span></span>
<span data-ttu-id="9a38a-107">Este artículo se supone que dispone de hello siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="9a38a-107">This article assumes that you have hello following items:</span></span>

* <span data-ttu-id="9a38a-108">**Una suscripción de Azure**: si no tiene una cuenta, puede crear una en un par de minutos.</span><span class="sxs-lookup"><span data-stu-id="9a38a-108">**An Azure subscription** - If you don't have an account, you can create one in just a couple of minutes.</span></span> <span data-ttu-id="9a38a-109">Si tiene una suscripción a MSDN, consulte [Crédito mensual de Azure para suscriptores de Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="9a38a-109">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="9a38a-110">De lo contrario, obtenga información acerca de cómo demasiado[crear una cuenta de prueba gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9a38a-110">Otherwise, learn how too[create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span>  
* <span data-ttu-id="9a38a-111">**Azure 2.0 CLI** -Asegúrese de que tiene más reciente Hola [CLI de Azure 2.0](/cli/azure/install-azure-cli) instalado y registrado en tooyour cuenta de Azure con [inicio de sesión de az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="9a38a-111">**Azure CLI 2.0** - Make sure you have hello latest [Azure CLI 2.0](/cli/azure/install-azure-cli) installed and logged in tooyour Azure account with [az login](/cli/azure/#login).</span></span>
* <span data-ttu-id="9a38a-112">**Sistema de operativo OpenBSD instalado en un archivo .vhd** -un sistema de operativo OpenBSD compatible (6.1 versión) debe ser el disco duro virtual de tooa instalado.</span><span class="sxs-lookup"><span data-stu-id="9a38a-112">**OpenBSD operating system installed in a .vhd file** - A supported OpenBSD operating system (6.1 version) must be installed tooa virtual hard disk.</span></span> <span data-ttu-id="9a38a-113">Varias herramientas existen archivos .vhd de toocreate.</span><span class="sxs-lookup"><span data-stu-id="9a38a-113">Multiple tools exist toocreate .vhd files.</span></span> <span data-ttu-id="9a38a-114">Por ejemplo, puede usar una solución de virtualización como archivo .vhd de Hyper-V toocreate Hola e instalar sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9a38a-114">For example, you can use a virtualization solution such as Hyper-V toocreate hello .vhd file and install hello operating system.</span></span> <span data-ttu-id="9a38a-115">Para obtener instrucciones sobre cómo tooinstall y usar Hyper-V, vea [instalar Hyper-V y crear una máquina virtual](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="9a38a-115">For instructions about how tooinstall and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>


## <a name="prepare-openbsd-image-for-azure"></a><span data-ttu-id="9a38a-116">Preparación de la imagen de OpenBSD para Azure</span><span class="sxs-lookup"><span data-stu-id="9a38a-116">Prepare OpenBSD image for Azure</span></span>
<span data-ttu-id="9a38a-117">En hello VM donde instaló el sistema de operativo de OpenBSD de hello 6.1, que agrega compatibilidad con Hyper-V, complete Hola procedimientos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9a38a-117">On hello VM where you installed hello OpenBSD operating system 6.1, which added Hyper-V support, complete hello following procedures:</span></span>

1. <span data-ttu-id="9a38a-118">Si DHCP no está habilitado durante la instalación, habilite servicio hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="9a38a-118">If DHCP is not enabled during installation, enable hello service as follows:</span></span>

    ```sh    
    echo dhcp > /etc/hostname.hvn0
    ```

2. <span data-ttu-id="9a38a-119">Configure una consola de serie como sigue:</span><span class="sxs-lookup"><span data-stu-id="9a38a-119">Set up a serial console as follows:</span></span>

    ```sh
    echo "stty com0 115200" >> /etc/boot.conf
    echo "set tty com0" >> /etc/boot.conf
    ```

3. <span data-ttu-id="9a38a-120">Configure la instalación del paquete como sigue:</span><span class="sxs-lookup"><span data-stu-id="9a38a-120">Configure Package installation as follows:</span></span>

    ```sh
    echo "https://ftp.openbsd.org/pub/OpenBSD" > /etc/installurl
    ```
   
4. <span data-ttu-id="9a38a-121">De forma predeterminada, Hola `root` usuario está deshabilitado en máquinas virtuales en Azure.</span><span class="sxs-lookup"><span data-stu-id="9a38a-121">By default, hello `root` user is disabled on virtual machines in Azure.</span></span> <span data-ttu-id="9a38a-122">Los usuarios pueden ejecutar comandos con privilegios elevados mediante el uso de hello `doas` comando OpenBSD VM.</span><span class="sxs-lookup"><span data-stu-id="9a38a-122">Users can run commands with elevated privileges by using hello `doas` command on OpenBSD VM.</span></span> <span data-ttu-id="9a38a-123">El comando doas está habilitado de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="9a38a-123">Doas is enabled by default.</span></span> <span data-ttu-id="9a38a-124">Para más información, consulte [doas.conf](http://man.openbsd.org/doas.conf.5).</span><span class="sxs-lookup"><span data-stu-id="9a38a-124">For more information, see [doas.conf](http://man.openbsd.org/doas.conf.5).</span></span> 

5. <span data-ttu-id="9a38a-125">Instalar y configurar los requisitos previos para hello agente de Azure como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="9a38a-125">Install and configure prerequisites for hello Azure Agent as follows:</span></span>

    ```sh
    pkg_add py-setuptools openssl git
    ln -sf /usr/local/bin/python2.7 /usr/local/bin/python
    ln -sf /usr/local/bin/python2.7-2to3 /usr/local/bin/2to3
    ln -sf /usr/local/bin/python2.7-config /usr/local/bin/python-config
    ln -sf /usr/local/bin/pydoc2.7  /usr/local/bin/pydoc
    ```

6. <span data-ttu-id="9a38a-126">versión más reciente de Hola de hello agente de Azure siempre se encuentra en [Github](https://github.com/Azure/WALinuxAgent/releases).</span><span class="sxs-lookup"><span data-stu-id="9a38a-126">hello latest release of hello Azure agent can always be found on [Github](https://github.com/Azure/WALinuxAgent/releases).</span></span> <span data-ttu-id="9a38a-127">Instalar a agente de hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="9a38a-127">Install hello agent as follows:</span></span>

    ```sh
    git clone https://github.com/Azure/WALinuxAgent 
    cd WALinuxAgent
    python setup.py install
    waagent -register-service
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="9a38a-128">Después de instalar al agente de Azure, es un tooverify buena idea que se está ejecutando como sigue:</span><span class="sxs-lookup"><span data-stu-id="9a38a-128">After you install Azure Agent, it's a good idea tooverify that it's running as follows:</span></span>
    >
    > ```bash
    > ps auxw | grep waagent
    > root     79309  0.0  1.5  9184 15356 p1  S      4:11PM    0:00.46 python /usr/local/sbin/waagent -daemon (python2.7)
    > cat /var/log/waagent.log
    > ```

7. <span data-ttu-id="9a38a-129">Desaprovisionamiento Hola tooclean del sistema y asegúrese de que adecuado para reaprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="9a38a-129">Deprovision hello system tooclean it and make it suitable for reprovisioning.</span></span> <span data-ttu-id="9a38a-130">Hello siguiente comando también elimina última cuenta de usuario aprovisionado Hola y Hola asociado datos:</span><span class="sxs-lookup"><span data-stu-id="9a38a-130">hello following command also deletes hello last provisioned user account and hello associated data:</span></span>

    ```sh
    waagent -deprovision+user -force
    ```

<span data-ttu-id="9a38a-131">Ahora ya puede apagar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9a38a-131">Now you can shut down your VM.</span></span>


## <a name="prepare-hello-vhd"></a><span data-ttu-id="9a38a-132">Preparar Hola VHD</span><span class="sxs-lookup"><span data-stu-id="9a38a-132">Prepare hello VHD</span></span>
<span data-ttu-id="9a38a-133">no se admite el formato VHDX Hello en Azure, solo **VHD fijo**.</span><span class="sxs-lookup"><span data-stu-id="9a38a-133">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span> <span data-ttu-id="9a38a-134">Puede convertir el formato de disco duro virtual de toofixed Hola disco mediante el Administrador de Hyper-V u Hola Powershell [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9a38a-134">You can convert hello disk toofixed VHD format using Hyper-V Manager or hello Powershell [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) cmdlet.</span></span> <span data-ttu-id="9a38a-135">A continuación se muestra un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="9a38a-135">An example is as following.</span></span>

```powershell
Convert-VHD OpenBSD61.vhdx OpenBSD61.vhd -VHDType Fixed
```

## <a name="create-storage-resources-and-upload"></a><span data-ttu-id="9a38a-136">Creación de recursos de almacenamiento y de carga</span><span class="sxs-lookup"><span data-stu-id="9a38a-136">Create storage resources and upload</span></span>
<span data-ttu-id="9a38a-137">En primer lugar, cree un grupo de recursos con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="9a38a-137">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="9a38a-138">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación:</span><span class="sxs-lookup"><span data-stu-id="9a38a-138">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="9a38a-139">tooupload el disco duro virtual, cree una cuenta de almacenamiento con [crear cuenta de almacenamiento az](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="9a38a-139">tooupload your VHD, create a storage account with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="9a38a-140">Los nombres de la cuenta de almacenamiento deben ser únicos, así que indique su propio nombre.</span><span class="sxs-lookup"><span data-stu-id="9a38a-140">Storage account names must be unique, so provide your own name.</span></span> <span data-ttu-id="9a38a-141">Hello en el ejemplo siguiente se crea una cuenta de almacenamiento denominada *mystorageaccount*:</span><span class="sxs-lookup"><span data-stu-id="9a38a-141">hello following example creates a storage account named *mystorageaccount*:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup \
    --name mystorageaccount \
    --location eastus \
    --sku Premium_LRS
```

<span data-ttu-id="9a38a-142">toocontrol tener acceso a la cuenta de almacenamiento toohello, obtener la clave de almacenamiento de hello con [lista de claves de cuenta de almacenamiento az](/cli/azure/storage/account/keys#list) como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="9a38a-142">toocontrol access toohello storage account, obtain hello storage key with [az storage account keys list](/cli/azure/storage/account/keys#list) as follows:</span></span>

```azurecli
STORAGE_KEY=$(az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount \
    --query "[?keyName=='key1']  | [0].value" -o tsv)
```

<span data-ttu-id="9a38a-143">Hola independiente de toologically discos duros virtuales carga, crear un contenedor dentro de la cuenta de almacenamiento de hello con [crear contenedor de almacenamiento az](/cli/azure/storage/container#create):</span><span class="sxs-lookup"><span data-stu-id="9a38a-143">toologically separate hello VHDs you upload, create a container within hello storage account with [az storage container create](/cli/azure/storage/container#create):</span></span>

```azurecli
az storage container create \
    --name vhds \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```

<span data-ttu-id="9a38a-144">Por último, cargue el VHD con el comando [az storage blob upload](/cli/azure/storage/blob#upload) como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="9a38a-144">Finally, upload your VHD with [az storage blob upload](/cli/azure/storage/blob#upload) as follows:</span></span>

```azurecli
az storage blob upload \
    --container-name vhds \
    --file ./OpenBSD61.vhd \
    --name OpenBSD61.vhd \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```


## <a name="create-vm-from-your-vhd"></a><span data-ttu-id="9a38a-145">Creación de una máquina virtual desde el disco duro virtual</span><span class="sxs-lookup"><span data-stu-id="9a38a-145">Create VM from your VHD</span></span>
<span data-ttu-id="9a38a-146">Puede crear una máquina virtual con un [script de ejemplo](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) o directamente con [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="9a38a-146">You can create a VM with a [sample script](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) or directly with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="9a38a-147">toospecify Hola se cargan, de VHD OpenBSD uso hello `--image` parámetro como sigue:</span><span class="sxs-lookup"><span data-stu-id="9a38a-147">toospecify hello OpenBSD VHD you uploaded, use hello `--image` parameter as follows:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myOpenBSD61 \
    --image "https://mystorageaccount.blob.core.windows.net/vhds/OpenBSD61.vhd" \
    --os-type linux \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

<span data-ttu-id="9a38a-148">Obtener dirección IP de hello de la VM OpenBSD con [az vm lista-ip-addresses](/cli/azure/vm#list-ip-addresses) como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="9a38a-148">Obtain hello IP address for your OpenBSD VM with [az vm list-ip-addresses](/cli/azure/vm#list-ip-addresses) as follows:</span></span>

```azurecli
az vm list-ip-addresses --resource-group myResourceGroup --name myOpenBSD61
```

<span data-ttu-id="9a38a-149">Ahora puede SSH tooyour OpenBSD VM como normal:</span><span class="sxs-lookup"><span data-stu-id="9a38a-149">Now you can SSH tooyour OpenBSD VM as normal:</span></span>
        
```bash
ssh azureuser@<ip address>
```


## <a name="next-steps"></a><span data-ttu-id="9a38a-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9a38a-150">Next steps</span></span>
<span data-ttu-id="9a38a-151">Si desea más información acerca de Hyper-V se admiten en OpenBSD6.1 de tooknow, leer [OpenBSD 6.1](https://www.openbsd.org/61.html) y [hyperv.4](http://man.openbsd.org/hyperv.4).</span><span class="sxs-lookup"><span data-stu-id="9a38a-151">If you want tooknow more about Hyper-V support on OpenBSD6.1, read [OpenBSD 6.1](https://www.openbsd.org/61.html) and [hyperv.4](http://man.openbsd.org/hyperv.4).</span></span>

<span data-ttu-id="9a38a-152">Si desea toocreate una máquina virtual desde disco administrado, leer [disco az](/cli/azure/disk).</span><span class="sxs-lookup"><span data-stu-id="9a38a-152">If you want toocreate a VM from managed disk, read [az disk](/cli/azure/disk).</span></span> 
