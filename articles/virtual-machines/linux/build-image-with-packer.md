---
title: "Creación de imágenes de VM de Azure Linux con Packer | Microsoft Docs"
description: "Aprenda a usar Packer para crear imágenes de máquinas virtuales Linux en Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/18/2017
ms.author: iainfou
ms.openlocfilehash: 49a74648bd3953647d581c4e7c548985c5000f17
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-packer-to-create-linux-virtual-machine-images-in-azure"></a><span data-ttu-id="e7078-103">Uso de Packer para crear imágenes de máquinas virtuales Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="e7078-103">How to use Packer to create Linux virtual machine images in Azure</span></span>
<span data-ttu-id="e7078-104">Cada máquina virtual (VM) en Azure se crea a partir de una imagen que define la distribución de Linux y la versión del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="e7078-104">Each virtual machine (VM) in Azure is created from an image that defines the Linux distribution and OS version.</span></span> <span data-ttu-id="e7078-105">Las imágenes pueden incluir configuraciones y aplicaciones preinstaladas.</span><span class="sxs-lookup"><span data-stu-id="e7078-105">Images can include pre-installed applications and configurations.</span></span> <span data-ttu-id="e7078-106">Azure Marketplace proporciona muchas imágenes propias y de terceros para los entornos de aplicaciones y distribuciones más comunes, pero también puede crear sus propias imágenes personalizadas adaptadas a sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="e7078-106">The Azure Marketplace provides many first and third-party images for most common distributions and application environments, or you can create your own custom images tailored to your needs.</span></span> <span data-ttu-id="e7078-107">En este artículo se detalla cómo utilizar la herramienta de código abierto [Packer](https://www.packer.io/) para definir y crear imágenes personalizadas en Azure.</span><span class="sxs-lookup"><span data-stu-id="e7078-107">This article details how to use the open source tool [Packer](https://www.packer.io/) to define and build custom images in Azure.</span></span>


## <a name="create-azure-resource-group"></a><span data-ttu-id="e7078-108">Creación del grupo de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="e7078-108">Create Azure resource group</span></span>
<span data-ttu-id="e7078-109">Durante el proceso de compilación, Packer crea recursos de Azure temporales mientras genera la máquina virtual de origen.</span><span class="sxs-lookup"><span data-stu-id="e7078-109">During the build process, Packer creates temporary Azure resources as it builds the source VM.</span></span> <span data-ttu-id="e7078-110">Para capturar dicha máquina virtual para usarla como imagen, debe definir un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e7078-110">To capture that source VM for use as an image, you must define a resource group.</span></span> <span data-ttu-id="e7078-111">La salida del proceso de compilación de Packer se almacena en este grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e7078-111">The output from the Packer build process is stored in this resource group.</span></span>

<span data-ttu-id="e7078-112">Cree un grupo de recursos con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="e7078-112">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="e7078-113">En el ejemplo siguiente, se crea un grupo de recursos denominado *myResourceGroup* en la ubicación *eastus*:</span><span class="sxs-lookup"><span data-stu-id="e7078-113">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create -n myResourceGroup -l eastus
```


## <a name="create-azure-credentials"></a><span data-ttu-id="e7078-114">Creación de credenciales de Azure</span><span class="sxs-lookup"><span data-stu-id="e7078-114">Create Azure credentials</span></span>
<span data-ttu-id="e7078-115">Packer se autentica con Azure mediante una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="e7078-115">Packer authenticates with Azure using a service principal.</span></span> <span data-ttu-id="e7078-116">Las entidades de servicio de Azure son identidades de seguridad que pueden usarse con aplicaciones, servicios y herramientas de automatización como Packer.</span><span class="sxs-lookup"><span data-stu-id="e7078-116">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Packer.</span></span> <span data-ttu-id="e7078-117">El usuario controla los permisos y los define con respecto a cuáles son las operaciones que la entidad de servicio puede realizar en Azure.</span><span class="sxs-lookup"><span data-stu-id="e7078-117">You control and define the permissions as to what operations the service principal can perform in Azure.</span></span>

<span data-ttu-id="e7078-118">Cree una entidad de servicio con [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) y genere los credenciales que Packer necesita:</span><span class="sxs-lookup"><span data-stu-id="e7078-118">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output the credentials that Packer needs:</span></span>

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

<span data-ttu-id="e7078-119">A continuación puede ver un ejemplo del resultado de los comandos anteriores:</span><span class="sxs-lookup"><span data-stu-id="e7078-119">An example of the output from the preceding commands is as follows:</span></span>

```azurecli
"f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
"0e760437-bf34-4aad-9f8d-870be799c55d",
"72f988bf-86f1-41af-91ab-2d7cd011db47"
```

<span data-ttu-id="e7078-120">Para autenticarse en Azure, también necesita obtener el identificador de la suscripción de Azure con [az account show](/cli/azure/account#show):</span><span class="sxs-lookup"><span data-stu-id="e7078-120">To authenticate to Azure, you also need to obtain your Azure subscription ID with [az account show](/cli/azure/account#show):</span></span>

```azurecli
az account show --query [id] --output tsv
```

<span data-ttu-id="e7078-121">El resultado de estos dos comandos se usa en el siguiente paso.</span><span class="sxs-lookup"><span data-stu-id="e7078-121">You use the output from these two commands in the next step.</span></span>


## <a name="define-packer-template"></a><span data-ttu-id="e7078-122">Definición de la plantilla de Packer</span><span class="sxs-lookup"><span data-stu-id="e7078-122">Define Packer template</span></span>
<span data-ttu-id="e7078-123">Para crear imágenes, es preciso crear una plantilla en forma de archivo JSON.</span><span class="sxs-lookup"><span data-stu-id="e7078-123">To build images, you create a template as a JSON file.</span></span> <span data-ttu-id="e7078-124">En la plantilla, se definen los generadores y aprovisionadores que realizan el proceso de creación real.</span><span class="sxs-lookup"><span data-stu-id="e7078-124">In the template, you define builders and provisioners that carry out the actual build process.</span></span> <span data-ttu-id="e7078-125">Packer tiene un [aprovisionador para Azure](https://www.packer.io/docs/builders/azure.html) que permite definir los recursos de Azure, como las credenciales de la entidad de servicio creadas en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="e7078-125">Packer has a [provisioner for Azure](https://www.packer.io/docs/builders/azure.html) that allows you to define Azure resources, such as the service principal credentials created in the preceding step.</span></span>

<span data-ttu-id="e7078-126">Cree un archivo denominado *ubuntu.json* y pegue el siguiente contenido.</span><span class="sxs-lookup"><span data-stu-id="e7078-126">Create a file named *ubuntu.json* and paste the following content.</span></span> <span data-ttu-id="e7078-127">Escriba sus propios valores para los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="e7078-127">Enter your own values for the following:</span></span>

| <span data-ttu-id="e7078-128">Parámetro</span><span class="sxs-lookup"><span data-stu-id="e7078-128">Parameter</span></span>                           | <span data-ttu-id="e7078-129">Dónde se obtiene</span><span class="sxs-lookup"><span data-stu-id="e7078-129">Where to obtain</span></span> |
|-------------------------------------|----------------------------------------------------|
| <span data-ttu-id="e7078-130">*client_id*</span><span class="sxs-lookup"><span data-stu-id="e7078-130">*client_id*</span></span>                         | <span data-ttu-id="e7078-131">Primera línea de la salida de `az ad sp` create command - *appId*</span><span class="sxs-lookup"><span data-stu-id="e7078-131">First line of output from `az ad sp` create command - *appId*</span></span> |
| <span data-ttu-id="e7078-132">*client_secret*</span><span class="sxs-lookup"><span data-stu-id="e7078-132">*client_secret*</span></span>                     | <span data-ttu-id="e7078-133">Segunda línea de la salida de `az ad sp` create command - *password*</span><span class="sxs-lookup"><span data-stu-id="e7078-133">Second line of output from `az ad sp` create command - *password*</span></span> |
| <span data-ttu-id="e7078-134">*tenant_id*</span><span class="sxs-lookup"><span data-stu-id="e7078-134">*tenant_id*</span></span>                         | <span data-ttu-id="e7078-135">Tercera línea de la salida de `az ad sp` create command - *tenant*</span><span class="sxs-lookup"><span data-stu-id="e7078-135">Third line of output from `az ad sp` create command - *tenant*</span></span> |
| <span data-ttu-id="e7078-136">*subscription_id*</span><span class="sxs-lookup"><span data-stu-id="e7078-136">*subscription_id*</span></span>                   | <span data-ttu-id="e7078-137">Salida del comando `az account show`</span><span class="sxs-lookup"><span data-stu-id="e7078-137">Output from `az account show` command</span></span> |
| <span data-ttu-id="e7078-138">*managed_image_resource_group_name*</span><span class="sxs-lookup"><span data-stu-id="e7078-138">*managed_image_resource_group_name*</span></span> | <span data-ttu-id="e7078-139">Nombre del grupo de recursos que creó en el primer paso</span><span class="sxs-lookup"><span data-stu-id="e7078-139">Name of resource group you created in the first step</span></span> |
| <span data-ttu-id="e7078-140">*managed_image_name*</span><span class="sxs-lookup"><span data-stu-id="e7078-140">*managed_image_name*</span></span>                | <span data-ttu-id="e7078-141">Nombre de la imagen de disco administrado que se crea</span><span class="sxs-lookup"><span data-stu-id="e7078-141">Name for the managed disk image that is created</span></span> |


```json
{
  "builders": [{
    "type": "azure-arm",

    "client_id": "f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
    "client_secret": "0e760437-bf34-4aad-9f8d-870be799c55d",
    "tenant_id": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "subscription_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx",

    "managed_image_resource_group_name": "myResourceGroup",
    "managed_image_name": "myPackerImage",

    "os_type": "Linux",
    "image_publisher": "Canonical",
    "image_offer": "UbuntuServer",
    "image_sku": "16.04-LTS",

    "azure_tags": {
        "dept": "Engineering",
        "task": "Image deployment"
    },

    "location": "East US",
    "vm_size": "Standard_DS2_v2"
  }],
  "provisioners": [{
    "execute_command": "chmod +x {{ .Path }}; {{ .Vars }} sudo -E sh '{{ .Path }}'",
    "inline": [
      "apt-get update",
      "apt-get upgrade -y",
      "apt-get -y install nginx",

      "/usr/sbin/waagent -force -deprovision+user && export HISTSIZE=0 && sync"
    ],
    "inline_shebang": "/bin/sh -x",
    "type": "shell"
  }]
}
```

<span data-ttu-id="e7078-142">Esta plantilla crea una imagen de Ubuntu 16.04 LTS, instala NGINX y desaprovisiona la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e7078-142">This template builds an Ubuntu 16.04 LTS image, installs NGINX, then deprovisions the VM.</span></span>

> [!NOTE]
> <span data-ttu-id="e7078-143">Si expande esta plantilla para aprovisionar las credenciales del usuario, ajuste el comando aprovisionador que desaprovisiona el agente de Azure para que sea `-deprovision`, en lugar de `deprovision+user`.</span><span class="sxs-lookup"><span data-stu-id="e7078-143">If you expand on this template to provision user credentials, adjust the provisioner command that deprovisions the Azure agent to read `-deprovision` rather than `deprovision+user`.</span></span>
> <span data-ttu-id="e7078-144">La marca `+user` quita todas las cuentas de usuario de la máquina virtual de origen.</span><span class="sxs-lookup"><span data-stu-id="e7078-144">The `+user` flag removes all user accounts from the source VM.</span></span>


## <a name="build-packer-image"></a><span data-ttu-id="e7078-145">Creación de una imagen de Packer</span><span class="sxs-lookup"><span data-stu-id="e7078-145">Build Packer image</span></span>
<span data-ttu-id="e7078-146">Si Packer aún no está instalado en el equipo local, de compresor [siga las instrucciones de instalación de Packer](https://www.packer.io/docs/install/index.html).</span><span class="sxs-lookup"><span data-stu-id="e7078-146">If you don't already have Packer installed on your local machine, [follow the Packer installation instructions](https://www.packer.io/docs/install/index.html).</span></span>

<span data-ttu-id="e7078-147">Para generar la imagen, especifique el archivo de plantilla de Packer como sigue:</span><span class="sxs-lookup"><span data-stu-id="e7078-147">Build the image by specifying your Packer template file as follows:</span></span>

```bash
./packer build ubuntu.json
```

<span data-ttu-id="e7078-148">A continuación puede ver un ejemplo del resultado de los comandos anteriores:</span><span class="sxs-lookup"><span data-stu-id="e7078-148">An example of the output from the preceding commands is as follows:</span></span>

```bash
azure-arm output will be in this color.

==> azure-arm: Running builder ...
    azure-arm: Creating Azure Resource Manager (ARM) client ...
==> azure-arm: Creating resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Location          : ‘East US’
==> azure-arm:  -> Tags              :
==> azure-arm:  ->> dept : Engineering
==> azure-arm:  ->> task : Image deployment
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Getting the VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.218.147’
==> azure-arm: Waiting for SSH to become available...
==> azure-arm: Connected to SSH!
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-shell868574263
    azure-arm: WARNING! The waagent service will be stopped.
    azure-arm: WARNING! Cached DHCP leases will be deleted.
    azure-arm: WARNING! root password will be disabled. You will not be able to login as root.
    azure-arm: WARNING! /etc/resolvconf/resolv.conf.d/tail and /etc/resolvconf/resolv.conf.d/original will be deleted.
    azure-arm: WARNING! packer account and entire home directory will be deleted.
==> azure-arm: Querying the machine’s properties ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Managed OS Disk   : ‘/subscriptions/guid/resourceGroups/packer-Resource-Group-swtxmqm7ly/providers/Microsoft.Compute/disks/osdisk’
==> azure-arm: Powering off machine ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm: Capturing image ...
==> azure-arm:  -> Compute ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Compute Name              : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Compute Location          : ‘East US’
==> azure-arm:  -> Image ResourceGroupName   : ‘myResourceGroup’
==> azure-arm:  -> Image Name                : ‘myPackerImage’
==> azure-arm:  -> Image Location            : ‘eastus’
==> azure-arm: Deleting resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm: Deleting the temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. The artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```


## <a name="create-vm-from-azure-image"></a><span data-ttu-id="e7078-149">Creación de una máquina virtual desde una imagen de Azure</span><span class="sxs-lookup"><span data-stu-id="e7078-149">Create VM from Azure Image</span></span>
<span data-ttu-id="e7078-150">Ya puede crear una máquina virtual a partir de la imagen con [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="e7078-150">You can now create a VM from your Image with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="e7078-151">Especifique la imagen que ha creado con el parámetro `--image`.</span><span class="sxs-lookup"><span data-stu-id="e7078-151">Specify the Image you created with the `--image` parameter.</span></span> <span data-ttu-id="e7078-152">El siguiente ejemplo crea una máquina virtual llamada *myVM* a partir de *myPackerImage* y genera claves SSH, en caso de que no existan:</span><span class="sxs-lookup"><span data-stu-id="e7078-152">The following example creates a VM named *myVM* from *myPackerImage* and generates SSH keys if they do not already exist:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image myPackerImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="e7078-153">La operación de creación de la máquina virtual tarda unos minutos.</span><span class="sxs-lookup"><span data-stu-id="e7078-153">It takes a few minutes to create the VM.</span></span> <span data-ttu-id="e7078-154">Cuando se haya creado la máquina virtual, anote el valor `publicIpAddress` que muestra la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="e7078-154">Once the VM has been created, take note of the `publicIpAddress` displayed by the Azure CLI.</span></span> <span data-ttu-id="e7078-155">Esta dirección se usa para acceder al sitio de NGINX mediante un explorador web.</span><span class="sxs-lookup"><span data-stu-id="e7078-155">This address is used to access the NGINX site via a web browser.</span></span>

<span data-ttu-id="e7078-156">Para permitir que el tráfico web llegue a la máquina virtual, abra el puerto 80 desde Internet con el comando [az vm open-port](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="e7078-156">To allow web traffic to reach your VM, open port 80 from the Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli
az vm open-port \
    --resource-group myResourceGroup \
    --name myVM \
    --port 80
```

## <a name="test-vm-and-nginx"></a><span data-ttu-id="e7078-157">Pruebas de la máquina virtual y de NGINX</span><span class="sxs-lookup"><span data-stu-id="e7078-157">Test VM and NGINX</span></span>
<span data-ttu-id="e7078-158">Ahora puede abrir un explorador web y escribir `http://publicIpAddress` en la barra de direcciones.</span><span class="sxs-lookup"><span data-stu-id="e7078-158">Now you can open a web browser and enter `http://publicIpAddress` in the address bar.</span></span> <span data-ttu-id="e7078-159">Proporcione su propia dirección IP pública obtenida del proceso de creación de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e7078-159">Provide your own public IP address from the VM create process.</span></span> <span data-ttu-id="e7078-160">La página predeterminada de NGINX es como la del ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e7078-160">The default NGINX page is displayed as in the following example:</span></span>

![Sitio predeterminado de NGINX](./media/build-image-with-packer/nginx.png) 


## <a name="next-steps"></a><span data-ttu-id="e7078-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e7078-162">Next steps</span></span>
<span data-ttu-id="e7078-163">En este ejemplo, ha utilizado Packer para crear una imagen de máquina virtual con NGINX instalado.</span><span class="sxs-lookup"><span data-stu-id="e7078-163">In this example, you used Packer to create a VM image with NGINX already installed.</span></span> <span data-ttu-id="e7078-164">Esta imagen se puede usar junto con los flujos de trabajo de la implementación existentes, como implementar la aplicación en las máquinas virtuales que se crean a partir de la imagen con Ansible, Chef o Puppet.</span><span class="sxs-lookup"><span data-stu-id="e7078-164">You can use this VM image alongside existing deployment workflows, such as to deploy your app to VMs created from the Image with Ansible, Chef, or Puppet.</span></span>

<span data-ttu-id="e7078-165">Para ver más plantillas de Packer de ejemplo para otras distribuciones de Linux, consulte [este repositorio de GitHub](https://github.com/hashicorp/packer/tree/master/examples/azure).</span><span class="sxs-lookup"><span data-stu-id="e7078-165">For additional example Packer templates for other Linux distros, see [this GitHub repo](https://github.com/hashicorp/packer/tree/master/examples/azure).</span></span>