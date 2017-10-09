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
# <a name="how-toouse-packer-toocreate-linux-virtual-machine-images-in-azure"></a>Cómo imágenes de máquina virtual de toouse compresor toocreate Linux de Azure
Cada máquina virtual (VM) en Azure se crea a partir de una imagen que defina Hola distribución de Linux y la versión de sistema operativo. Las imágenes pueden incluir configuraciones y aplicaciones preinstaladas. Hello Azure Marketplace proporciona muchas imágenes primeros y tercero para distribuciones más comunes y los entornos de aplicaciones, o puede crear sus propias necesidades de tooyour imágenes personalizadas adaptadas. Este artículo detalla cómo toouse Hola Abrir herramienta de código fuente [compresor](https://www.packer.io/) toodefine y compilación imágenes personalizadas en Azure.


## <a name="create-azure-resource-group"></a>Creación del grupo de recursos de Azure
Durante el proceso de compilación de hello, compresor crea recursos de Azure temporales cuando genera una VM de origen Hola. toocapture que son origen de máquina virtual para su uso como una imagen, debe definir un grupo de recursos. Hello resultado del proceso de compilación de compresor Hola se almacena en este grupo de recursos.

Cree un grupo de recursos con [az group create](/cli/azure/group#create). Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación:

```azurecli
az group create -n myResourceGroup -l eastus
```


## <a name="create-azure-credentials"></a>Creación de credenciales de Azure
Packer se autentica con Azure mediante una entidad de servicio. Las entidades de servicio de Azure son identidades de seguridad que pueden usarse con aplicaciones, servicios y herramientas de automatización como Packer. Controlar y definir permisos de hello como entidad de servicio de hello toowhat operaciones puede llevar a cabo en Azure.

Crear un servicio principal con [az ad sp crear-de-rbac](/cli/azure/ad/sp#create-for-rbac) y las credenciales de Hola de salida que necesita de compresor:

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

Un ejemplo de salida de hello de hello anterior comandos es la siguiente:

```azurecli
"f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
"0e760437-bf34-4aad-9f8d-870be799c55d",
"72f988bf-86f1-41af-91ab-2d7cd011db47"
```

tooauthenticate tooAzure, también deberá tooobtain Id. de la suscripción de Azure con [mostrar de la cuenta de az](/cli/azure/account#show):

```azurecli
az account show --query [id] --output tsv
```

Utilice la salida de hello de estos dos comandos en el paso siguiente Hola.


## <a name="define-packer-template"></a>Definición de la plantilla de Packer
toobuild imágenes, crear una plantilla como un archivo JSON. En la plantilla de hello, defina los generadores y provisioners que efectúan Hola real de proceso de compilación. Compresor tiene un [aprovisionador para Azure](https://www.packer.io/docs/builders/azure.html) que le permite toodefine Azure recursos, como credenciales principal del servicio Hola creados en hello anterior paso.

Cree un archivo denominado *ubuntu.json* y pegar Hola siguen contenido. Escriba sus propios valores para siguiente hello:

| Parámetro                           | Donde tooobtain |
|-------------------------------------|----------------------------------------------------|
| *client_id*                         | Primera línea de la salida de `az ad sp` create command - *appId* |
| *client_secret*                     | Segunda línea de la salida de `az ad sp` create command - *password* |
| *tenant_id*                         | Tercera línea de la salida de `az ad sp` create command - *tenant* |
| *subscription_id*                   | Salida del comando `az account show` |
| *managed_image_resource_group_name* | Nombre del grupo de recursos que creó en el primer paso de Hola |
| *managed_image_name*                | Nombre de imagen de disco administrado Hola que se crea |


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

Esta plantilla crea una imagen de Ubuntu 16.04 LTS, instalará NGINX, a continuación, desactiva Hola máquina virtual.

> [!NOTE]
> Si expande esta plantilla tooprovision las credenciales de usuario, ajustar el comando aprovisionador de Hola que desactiva hello Azure agente tooread `-deprovision` en lugar de `deprovision+user`.
> Hola `+user` marca Quita todas las cuentas de usuario de una VM de origen Hola.


## <a name="build-packer-image"></a>Creación de una imagen de Packer
Si no se ha instalado en el equipo local, de compresor [siga las instrucciones de instalación de compresor hello](https://www.packer.io/docs/install/index.html).

Crear imagen de Hola especificando el compresor archivo de plantilla como se indica a continuación:

```bash
./packer build ubuntu.json
```

Un ejemplo de salida de hello de hello anterior comandos es la siguiente:

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


## <a name="create-vm-from-azure-image"></a>Creación de una máquina virtual desde una imagen de Azure
Ya puede crear una máquina virtual a partir de la imagen con [az vm create](/cli/azure/vm#create). Especificar Hola imagen creada con hello `--image` parámetro. Hello en el ejemplo siguiente se crea una máquina virtual denominada *myVM* de *myPackerImage* y genera claves de SSH si aún no existen:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image myPackerImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

Se tarda unos minutos toocreate Hola máquina virtual. Una vez que se ha creado Hola VM, tome nota de hello `publicIpAddress` muestra de Hola CLI de Azure. Esta dirección es tooaccess usado hello NGINX a través del sitio un explorador web.

tooallow web tooreach de tráfico de la máquina virtual, abrir el puerto 80 de hello Internet con [az de vm abrir puerto](/cli/azure/vm#open-port):

```azurecli
az vm open-port \
    --resource-group myResourceGroup \
    --name myVM \
    --port 80
```

## <a name="test-vm-and-nginx"></a>Pruebas de la máquina virtual y de NGINX
Ahora puede abrir un explorador web y escriba `http://publicIpAddress` en la barra de direcciones de Hola. Proporcionar su propia público dirección IP de hello VM crear proceso. página NGINX Hola predeterminada se muestra como en el siguiente ejemplo de Hola:

![Sitio predeterminado de NGINX](./media/build-image-with-packer/nginx.png) 


## <a name="next-steps"></a>Pasos siguientes
En este ejemplo, ha utilizado compresor toocreate una imagen de VM con NGINX ya instalado. Puede usar esta imagen de máquina virtual junto con los flujos de trabajo existente de implementación, como toodeploy su tooVMs de aplicación creado a partir de hello imagen con Ansible, Chef o Puppet.

Para ver más plantillas de Packer de ejemplo para otras distribuciones de Linux, consulte [este repositorio de GitHub](https://github.com/hashicorp/packer/tree/master/examples/azure).