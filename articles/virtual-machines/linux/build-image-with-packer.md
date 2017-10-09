---
title: "aaaHow toocreate imágenes de máquina virtual de Azure de Linux con compresor | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse imágenes de toocreate compresor de máquinas virtuales de Linux en Azure"
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
ms.openlocfilehash: 5990598859e73efac477884bc8de5fd5138bf6e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-packer-toocreate-linux-virtual-machine-images-in-azure"></a><span data-ttu-id="c1161-103">Cómo imágenes de máquina virtual de toouse compresor toocreate Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="c1161-103">How toouse Packer toocreate Linux virtual machine images in Azure</span></span>
<span data-ttu-id="c1161-104">Cada máquina virtual (VM) en Azure se crea a partir de una imagen que defina Hola distribución de Linux y la versión de sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="c1161-104">Each virtual machine (VM) in Azure is created from an image that defines hello Linux distribution and OS version.</span></span> <span data-ttu-id="c1161-105">Las imágenes pueden incluir configuraciones y aplicaciones preinstaladas.</span><span class="sxs-lookup"><span data-stu-id="c1161-105">Images can include pre-installed applications and configurations.</span></span> <span data-ttu-id="c1161-106">Hello Azure Marketplace proporciona muchas imágenes primeros y tercero para distribuciones más comunes y los entornos de aplicaciones, o puede crear sus propias necesidades de tooyour imágenes personalizadas adaptadas.</span><span class="sxs-lookup"><span data-stu-id="c1161-106">hello Azure Marketplace provides many first and third-party images for most common distributions and application environments, or you can create your own custom images tailored tooyour needs.</span></span> <span data-ttu-id="c1161-107">Este artículo detalla cómo toouse Hola Abrir herramienta de código fuente [compresor](https://www.packer.io/) toodefine y compilación imágenes personalizadas en Azure.</span><span class="sxs-lookup"><span data-stu-id="c1161-107">This article details how toouse hello open source tool [Packer](https://www.packer.io/) toodefine and build custom images in Azure.</span></span>


## <a name="create-azure-resource-group"></a><span data-ttu-id="c1161-108">Creación del grupo de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="c1161-108">Create Azure resource group</span></span>
<span data-ttu-id="c1161-109">Durante el proceso de compilación de hello, compresor crea recursos de Azure temporales cuando genera una VM de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="c1161-109">During hello build process, Packer creates temporary Azure resources as it builds hello source VM.</span></span> <span data-ttu-id="c1161-110">toocapture que son origen de máquina virtual para su uso como una imagen, debe definir un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c1161-110">toocapture that source VM for use as an image, you must define a resource group.</span></span> <span data-ttu-id="c1161-111">Hello resultado del proceso de compilación de compresor Hola se almacena en este grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c1161-111">hello output from hello Packer build process is stored in this resource group.</span></span>

<span data-ttu-id="c1161-112">Cree un grupo de recursos con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="c1161-112">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="c1161-113">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación:</span><span class="sxs-lookup"><span data-stu-id="c1161-113">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create -n myResourceGroup -l eastus
```


## <a name="create-azure-credentials"></a><span data-ttu-id="c1161-114">Creación de credenciales de Azure</span><span class="sxs-lookup"><span data-stu-id="c1161-114">Create Azure credentials</span></span>
<span data-ttu-id="c1161-115">Packer se autentica con Azure mediante una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="c1161-115">Packer authenticates with Azure using a service principal.</span></span> <span data-ttu-id="c1161-116">Las entidades de servicio de Azure son identidades de seguridad que pueden usarse con aplicaciones, servicios y herramientas de automatización como Packer.</span><span class="sxs-lookup"><span data-stu-id="c1161-116">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Packer.</span></span> <span data-ttu-id="c1161-117">Controlar y definir permisos de hello como entidad de servicio de hello toowhat operaciones puede llevar a cabo en Azure.</span><span class="sxs-lookup"><span data-stu-id="c1161-117">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span>

<span data-ttu-id="c1161-118">Crear un servicio principal con [az ad sp crear-de-rbac](/cli/azure/ad/sp#create-for-rbac) y las credenciales de Hola de salida que necesita de compresor:</span><span class="sxs-lookup"><span data-stu-id="c1161-118">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output hello credentials that Packer needs:</span></span>

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

<span data-ttu-id="c1161-119">Un ejemplo de salida de hello de hello anterior comandos es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="c1161-119">An example of hello output from hello preceding commands is as follows:</span></span>

```azurecli
"f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
"0e760437-bf34-4aad-9f8d-870be799c55d",
"72f988bf-86f1-41af-91ab-2d7cd011db47"
```

<span data-ttu-id="c1161-120">tooauthenticate tooAzure, también deberá tooobtain Id. de la suscripción de Azure con [mostrar de la cuenta de az](/cli/azure/account#show):</span><span class="sxs-lookup"><span data-stu-id="c1161-120">tooauthenticate tooAzure, you also need tooobtain your Azure subscription ID with [az account show](/cli/azure/account#show):</span></span>

```azurecli
az account show --query [id] --output tsv
```

<span data-ttu-id="c1161-121">Utilice la salida de hello de estos dos comandos en el paso siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="c1161-121">You use hello output from these two commands in hello next step.</span></span>


## <a name="define-packer-template"></a><span data-ttu-id="c1161-122">Definición de la plantilla de Packer</span><span class="sxs-lookup"><span data-stu-id="c1161-122">Define Packer template</span></span>
<span data-ttu-id="c1161-123">toobuild imágenes, crear una plantilla como un archivo JSON.</span><span class="sxs-lookup"><span data-stu-id="c1161-123">toobuild images, you create a template as a JSON file.</span></span> <span data-ttu-id="c1161-124">En la plantilla de hello, defina los generadores y provisioners que efectúan Hola real de proceso de compilación.</span><span class="sxs-lookup"><span data-stu-id="c1161-124">In hello template, you define builders and provisioners that carry out hello actual build process.</span></span> <span data-ttu-id="c1161-125">Compresor tiene un [aprovisionador para Azure](https://www.packer.io/docs/builders/azure.html) que le permite toodefine Azure recursos, como credenciales principal del servicio Hola creados en hello anterior paso.</span><span class="sxs-lookup"><span data-stu-id="c1161-125">Packer has a [provisioner for Azure](https://www.packer.io/docs/builders/azure.html) that allows you toodefine Azure resources, such as hello service principal credentials created in hello preceding step.</span></span>

<span data-ttu-id="c1161-126">Cree un archivo denominado *ubuntu.json* y pegar Hola siguen contenido.</span><span class="sxs-lookup"><span data-stu-id="c1161-126">Create a file named *ubuntu.json* and paste hello following content.</span></span> <span data-ttu-id="c1161-127">Escriba sus propios valores para siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="c1161-127">Enter your own values for hello following:</span></span>

| <span data-ttu-id="c1161-128">Parámetro</span><span class="sxs-lookup"><span data-stu-id="c1161-128">Parameter</span></span>                           | <span data-ttu-id="c1161-129">Donde tooobtain</span><span class="sxs-lookup"><span data-stu-id="c1161-129">Where tooobtain</span></span> |
|-------------------------------------|----------------------------------------------------|
| <span data-ttu-id="c1161-130">*client_id*</span><span class="sxs-lookup"><span data-stu-id="c1161-130">*client_id*</span></span>                         | <span data-ttu-id="c1161-131">Primera línea de la salida de `az ad sp` create command - *appId*</span><span class="sxs-lookup"><span data-stu-id="c1161-131">First line of output from `az ad sp` create command - *appId*</span></span> |
| <span data-ttu-id="c1161-132">*client_secret*</span><span class="sxs-lookup"><span data-stu-id="c1161-132">*client_secret*</span></span>                     | <span data-ttu-id="c1161-133">Segunda línea de la salida de `az ad sp` create command - *password*</span><span class="sxs-lookup"><span data-stu-id="c1161-133">Second line of output from `az ad sp` create command - *password*</span></span> |
| <span data-ttu-id="c1161-134">*tenant_id*</span><span class="sxs-lookup"><span data-stu-id="c1161-134">*tenant_id*</span></span>                         | <span data-ttu-id="c1161-135">Tercera línea de la salida de `az ad sp` create command - *tenant*</span><span class="sxs-lookup"><span data-stu-id="c1161-135">Third line of output from `az ad sp` create command - *tenant*</span></span> |
| <span data-ttu-id="c1161-136">*subscription_id*</span><span class="sxs-lookup"><span data-stu-id="c1161-136">*subscription_id*</span></span>                   | <span data-ttu-id="c1161-137">Salida del comando `az account show`</span><span class="sxs-lookup"><span data-stu-id="c1161-137">Output from `az account show` command</span></span> |
| <span data-ttu-id="c1161-138">*managed_image_resource_group_name*</span><span class="sxs-lookup"><span data-stu-id="c1161-138">*managed_image_resource_group_name*</span></span> | <span data-ttu-id="c1161-139">Nombre del grupo de recursos que creó en el primer paso de Hola</span><span class="sxs-lookup"><span data-stu-id="c1161-139">Name of resource group you created in hello first step</span></span> |
| <span data-ttu-id="c1161-140">*managed_image_name*</span><span class="sxs-lookup"><span data-stu-id="c1161-140">*managed_image_name*</span></span>                | <span data-ttu-id="c1161-141">Nombre de imagen de disco administrado Hola que se crea</span><span class="sxs-lookup"><span data-stu-id="c1161-141">Name for hello managed disk image that is created</span></span> |


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

<span data-ttu-id="c1161-142">Esta plantilla crea una imagen de Ubuntu 16.04 LTS, instalará NGINX, a continuación, desactiva Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c1161-142">This template builds an Ubuntu 16.04 LTS image, installs NGINX, then deprovisions hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="c1161-143">Si expande esta plantilla tooprovision las credenciales de usuario, ajustar el comando aprovisionador de Hola que desactiva hello Azure agente tooread `-deprovision` en lugar de `deprovision+user`.</span><span class="sxs-lookup"><span data-stu-id="c1161-143">If you expand on this template tooprovision user credentials, adjust hello provisioner command that deprovisions hello Azure agent tooread `-deprovision` rather than `deprovision+user`.</span></span>
> <span data-ttu-id="c1161-144">Hola `+user` marca Quita todas las cuentas de usuario de una VM de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="c1161-144">hello `+user` flag removes all user accounts from hello source VM.</span></span>


## <a name="build-packer-image"></a><span data-ttu-id="c1161-145">Creación de una imagen de Packer</span><span class="sxs-lookup"><span data-stu-id="c1161-145">Build Packer image</span></span>
<span data-ttu-id="c1161-146">Si no se ha instalado en el equipo local, de compresor [siga las instrucciones de instalación de compresor hello](https://www.packer.io/docs/install/index.html).</span><span class="sxs-lookup"><span data-stu-id="c1161-146">If you don't already have Packer installed on your local machine, [follow hello Packer installation instructions](https://www.packer.io/docs/install/index.html).</span></span>

<span data-ttu-id="c1161-147">Crear imagen de Hola especificando el compresor archivo de plantilla como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="c1161-147">Build hello image by specifying your Packer template file as follows:</span></span>

```bash
./packer build ubuntu.json
```

<span data-ttu-id="c1161-148">Un ejemplo de salida de hello de hello anterior comandos es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="c1161-148">An example of hello output from hello preceding commands is as follows:</span></span>

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
==> azure-arm: Getting hello VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.218.147’
==> azure-arm: Waiting for SSH toobecome available...
==> azure-arm: Connected tooSSH!
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-shell868574263
    azure-arm: WARNING! hello waagent service will be stopped.
    azure-arm: WARNING! Cached DHCP leases will be deleted.
    azure-arm: WARNING! root password will be disabled. You will not be able toologin as root.
    azure-arm: WARNING! /etc/resolvconf/resolv.conf.d/tail and /etc/resolvconf/resolv.conf.d/original will be deleted.
    azure-arm: WARNING! packer account and entire home directory will be deleted.
==> azure-arm: Querying hello machine’s properties ...
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
==> azure-arm: Deleting hello temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. hello artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```


## <a name="create-vm-from-azure-image"></a><span data-ttu-id="c1161-149">Creación de una máquina virtual desde una imagen de Azure</span><span class="sxs-lookup"><span data-stu-id="c1161-149">Create VM from Azure Image</span></span>
<span data-ttu-id="c1161-150">Ya puede crear una máquina virtual a partir de la imagen con [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="c1161-150">You can now create a VM from your Image with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="c1161-151">Especificar Hola imagen creada con hello `--image` parámetro.</span><span class="sxs-lookup"><span data-stu-id="c1161-151">Specify hello Image you created with hello `--image` parameter.</span></span> <span data-ttu-id="c1161-152">Hello en el ejemplo siguiente se crea una máquina virtual denominada *myVM* de *myPackerImage* y genera claves de SSH si aún no existen:</span><span class="sxs-lookup"><span data-stu-id="c1161-152">hello following example creates a VM named *myVM* from *myPackerImage* and generates SSH keys if they do not already exist:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image myPackerImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="c1161-153">Se tarda unos minutos toocreate Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c1161-153">It takes a few minutes toocreate hello VM.</span></span> <span data-ttu-id="c1161-154">Una vez que se ha creado Hola VM, tome nota de hello `publicIpAddress` muestra de Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="c1161-154">Once hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="c1161-155">Esta dirección es tooaccess usado hello NGINX a través del sitio un explorador web.</span><span class="sxs-lookup"><span data-stu-id="c1161-155">This address is used tooaccess hello NGINX site via a web browser.</span></span>

<span data-ttu-id="c1161-156">tooallow web tooreach de tráfico de la máquina virtual, abrir el puerto 80 de hello Internet con [az de vm abrir puerto](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="c1161-156">tooallow web traffic tooreach your VM, open port 80 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli
az vm open-port \
    --resource-group myResourceGroup \
    --name myVM \
    --port 80
```

## <a name="test-vm-and-nginx"></a><span data-ttu-id="c1161-157">Pruebas de la máquina virtual y de NGINX</span><span class="sxs-lookup"><span data-stu-id="c1161-157">Test VM and NGINX</span></span>
<span data-ttu-id="c1161-158">Ahora puede abrir un explorador web y escriba `http://publicIpAddress` en la barra de direcciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="c1161-158">Now you can open a web browser and enter `http://publicIpAddress` in hello address bar.</span></span> <span data-ttu-id="c1161-159">Proporcionar su propia público dirección IP de hello VM crear proceso.</span><span class="sxs-lookup"><span data-stu-id="c1161-159">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="c1161-160">página NGINX Hola predeterminada se muestra como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="c1161-160">hello default NGINX page is displayed as in hello following example:</span></span>

![Sitio predeterminado de NGINX](./media/build-image-with-packer/nginx.png) 


## <a name="next-steps"></a><span data-ttu-id="c1161-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c1161-162">Next steps</span></span>
<span data-ttu-id="c1161-163">En este ejemplo, ha utilizado compresor toocreate una imagen de VM con NGINX ya instalado.</span><span class="sxs-lookup"><span data-stu-id="c1161-163">In this example, you used Packer toocreate a VM image with NGINX already installed.</span></span> <span data-ttu-id="c1161-164">Puede usar esta imagen de máquina virtual junto con los flujos de trabajo existente de implementación, como toodeploy su tooVMs de aplicación creado a partir de hello imagen con Ansible, Chef o Puppet.</span><span class="sxs-lookup"><span data-stu-id="c1161-164">You can use this VM image alongside existing deployment workflows, such as toodeploy your app tooVMs created from hello Image with Ansible, Chef, or Puppet.</span></span>

<span data-ttu-id="c1161-165">Para ver más plantillas de Packer de ejemplo para otras distribuciones de Linux, consulte [este repositorio de GitHub](https://github.com/hashicorp/packer/tree/master/examples/azure).</span><span class="sxs-lookup"><span data-stu-id="c1161-165">For additional example Packer templates for other Linux distros, see [this GitHub repo](https://github.com/hashicorp/packer/tree/master/examples/azure).</span></span>