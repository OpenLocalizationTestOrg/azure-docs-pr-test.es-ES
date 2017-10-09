---
title: aaaDifferent formas toocreate una VM de Linux en Azure | Microsoft Azure
description: "Obtenga información acerca de maneras diferentes de hello toocreate una máquina virtual de Linux en Azure, incluidos los vínculos tootools y tutoriales para cada método."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 250e92c063c87a8c1279097dc2264777d95478d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-linux-vm"></a>Diferentes maneras toocreate una VM de Linux
Tiene flexibilidad de hello en Azure toocreate una máquina virtual de Linux (VM) con herramientas y flujos de trabajo tooyou cómodo. En este artículo se resume estas diferencias y ejemplos para crear las máquinas virtuales de Linux, incluidas Hola 2.0 de CLI de Azure. También puede ver las opciones de creación incluido hello [Azure CLI 1.0](creation-choices-nodejs.md).

Hola [CLI de Azure 2.0](/cli/azure/install-az-cli2) está disponible en las distintas plataformas a través de un paquete de npm, paquetes suministrados por la distribución o el contenedor de Docker. Instale Hola build más adecuada para su entorno e inicie sesión con cuenta de Azure de tooan [inicio de sesión de az](/cli/azure/#login)

* [Crear una VM de Linux con hello 2.0 de CLI de Azure](quick-create-cli.md)
  
  * Cree un grupo de recursos con [az group create](/cli/azure/group#create) llamado *myResourceGroup*: 
   
    ```azurecli
    az group create --name myResourceGroup --location eastus
    ```
    
  * Crear una máquina virtual con [crear vm az](/cli/azure/vm#create) denominado *myVM* utilizando Hola más reciente *UbuntuLTS* de la imagen y generar claves SSH si aún no existen en *~/.ssh*:

    ```azurecli
    az vm create \
        --resource-group myResourceGroup \
        --name myVM \
        --image UbuntuLTS \
        --generate-ssh-keys
    ```

* [Creación de una máquina virtual Linux mediante una plantilla de Azure](create-ssh-secured-vm-from-template.md)
  
  * Hello siguiente ejemplo se utiliza [Crear implementación de grupo az](/cli/azure/group/deployment#create) toocreate una máquina virtual desde una plantilla almacenada en GitHub:
    
    ```azurecli
    az group deployment create --resource-group myResourceGroup \ 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
      --parameters @myparameters.json
    ```
* [Creación de una máquina virtual Linux y su personalización con cloud-init](tutorial-automate-vm-deployment.md)

* [Creación de una aplicación de equilibrio de carga y alta disponibilidad en varias máquinas virtuales Linux](tutorial-load-balancer.md)


## <a name="azure-portal"></a>Azure Portal
Hola [portal de Azure](https://portal.azure.com) permite tooquickly crear una máquina virtual porque no hay nada tooinstall en el sistema. Use Hola toocreate portal Azure Hola VM:

* [Crear una VM de Linux con hello portal de Azure](quick-create-portal.md) 


## <a name="operating-system-and-image-choices"></a>Sistema operativo y opciones de imagen
Al crear una máquina virtual, puede elegir una imagen basada en hello desea toorun de sistema operativo. Azure y sus socios ofrecen muchas imágenes, algunas de las cuales incluyen aplicaciones y herramientas preinstaladas. O bien, cargue uno de sus propias imágenes (consulte [Hola después de la sección](#use-your-own-image)).

### <a name="azure-images"></a>Imágenes de Azure
Hola de uso [imagen de máquina virtual az](/cli/azure/vm/image) comandos toosee lo que está disponible por publicador, versión de distribución y las compilaciones.

Lista de publicadores disponibles:

```azurecli
az vm image list-publishers --location eastus
```

Lista de productos disponibles (ofertas) de un publicador determinado:

```azurecli
az vm image list-offers --publisher Canonical --location eastus
```

Lista de SKU disponibles (versiones de distribución) de una oferta determinada:

```azurecli
az vm image list-skus --publisher Canonical --offer UbuntuServer --location eastus
```

Lista de todas las imágenes disponibles para una versión determinada:

```azurecli
az vm image list --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS --location eastus
```

Para obtener más ejemplos sobre cómo examinar y utilizar imágenes disponibles, vea [navegue y seleccione las imágenes de máquina virtual de Azure con hello Azure CLI](cli-ps-findimage.md).

Hola [crear vm az](/cli/azure/vm#create) comando tiene el alias que se puede utilizar acceso tooquickly Hola distribuciones más comunes y sus versiones más recientes. Uso de alias suele ser más rápido que especifica el publicador de hello, oferta, SKU y versión cada vez que cree una máquina virtual:

| Alias | Publicador | Oferta | SKU | Versión |
|:--- |:--- |:--- |:--- |:--- |
| CentOS |OpenLogic |CentOS |7,2 |más reciente |
| CoreOS |CoreOS |CoreOS |Stable |más reciente |
| Debian |credativ |Debian |8 |más reciente |
| openSUSE |SUSE |openSUSE |13.2 |más reciente |
| RHEL |Redhat |RHEL |7,2 |más reciente |
| SLES |SLES |SLES |12-SP1 |más reciente |
| UbuntuLTS |Canonical |UbuntuServer |14.04.4-LTS |más reciente |

### <a name="use-your-own-image"></a>Uso de su propia imagen
Si necesita realizar cambios personalizados específicos, use una imagen basada en una máquina virtual de Azure existente; para ello, capture esa máquina virtual. También puede cargar una imagen creada de forma local. Para obtener más información sobre las distribuciones compatibles y cómo toouse sus propias imágenes, vea Hola siguientes artículos:

* [Distribuciones aprobadas por Azure](endorsed-distros.md)
* [Información para las distribuciones no aprobadas](create-upload-generic.md)
* [¿Cómo toocreate una imagen de una máquina virtual de Azure existente](tutorial-custom-images.md).
  
  * Inicio rápido de comandos de ejemplo toocreate una imagen de una máquina virtual de Azure existente:
    
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm generalize --resource-group myResourceGroup --name myVM
    az vm image create --resource-group myResourceGroup --source myVM --name myImage
    ```

## <a name="next-steps"></a>Pasos siguientes
* Crear una VM de Linux con hello [CLI](quick-create-cli.md), de hello [portal](quick-create-portal.md), o mediante un [plantilla de Azure Resource Manager](../windows/cli-deploy-templates.md).
* Después de crear una máquina virtual Linux, [aprenda sobre los discos y el almacenamiento de Azure](tutorial-manage-disks.md).
* Los pasos demasiado rápido[restablecer una contraseña o claves SSH y administrar los usuarios](using-vmaccess-extension.md).
