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
# <a name="create-and-upload-an-openbsd-disk-image-tooazure"></a>Crear y cargar un tooAzure de imagen de disco OpenBSD
Este artículo muestra cómo toocreate y cargar un disco duro virtual (VHD) que contiene Hola OpenBSD sistema de operativo. Después de cargarlo, puede usarlo como su propia toocreate imagen una máquina virtual (VM) en Azure a través de la CLI de Azure.


## <a name="prerequisites"></a>Requisitos previos
Este artículo se supone que dispone de hello siguientes elementos:

* **Una suscripción de Azure**: si no tiene una cuenta, puede crear una en un par de minutos. Si tiene una suscripción a MSDN, consulte [Crédito mensual de Azure para suscriptores de Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/). De lo contrario, obtenga información acerca de cómo demasiado[crear una cuenta de prueba gratuita](https://azure.microsoft.com/pricing/free-trial/).  
* **Azure 2.0 CLI** -Asegúrese de que tiene más reciente Hola [CLI de Azure 2.0](/cli/azure/install-azure-cli) instalado y registrado en tooyour cuenta de Azure con [inicio de sesión de az](/cli/azure/#login).
* **Sistema de operativo OpenBSD instalado en un archivo .vhd** -un sistema de operativo OpenBSD compatible (6.1 versión) debe ser el disco duro virtual de tooa instalado. Varias herramientas existen archivos .vhd de toocreate. Por ejemplo, puede usar una solución de virtualización como archivo .vhd de Hyper-V toocreate Hola e instalar sistema operativo de Hola. Para obtener instrucciones sobre cómo tooinstall y usar Hyper-V, vea [instalar Hyper-V y crear una máquina virtual](http://technet.microsoft.com/library/hh846766.aspx).


## <a name="prepare-openbsd-image-for-azure"></a>Preparación de la imagen de OpenBSD para Azure
En hello VM donde instaló el sistema de operativo de OpenBSD de hello 6.1, que agrega compatibilidad con Hyper-V, complete Hola procedimientos siguientes:

1. Si DHCP no está habilitado durante la instalación, habilite servicio hello como sigue:

    ```sh    
    echo dhcp > /etc/hostname.hvn0
    ```

2. Configure una consola de serie como sigue:

    ```sh
    echo "stty com0 115200" >> /etc/boot.conf
    echo "set tty com0" >> /etc/boot.conf
    ```

3. Configure la instalación del paquete como sigue:

    ```sh
    echo "https://ftp.openbsd.org/pub/OpenBSD" > /etc/installurl
    ```
   
4. De forma predeterminada, Hola `root` usuario está deshabilitado en máquinas virtuales en Azure. Los usuarios pueden ejecutar comandos con privilegios elevados mediante el uso de hello `doas` comando OpenBSD VM. El comando doas está habilitado de manera predeterminada. Para más información, consulte [doas.conf](http://man.openbsd.org/doas.conf.5). 

5. Instalar y configurar los requisitos previos para hello agente de Azure como se indica a continuación:

    ```sh
    pkg_add py-setuptools openssl git
    ln -sf /usr/local/bin/python2.7 /usr/local/bin/python
    ln -sf /usr/local/bin/python2.7-2to3 /usr/local/bin/2to3
    ln -sf /usr/local/bin/python2.7-config /usr/local/bin/python-config
    ln -sf /usr/local/bin/pydoc2.7  /usr/local/bin/pydoc
    ```

6. versión más reciente de Hola de hello agente de Azure siempre se encuentra en [Github](https://github.com/Azure/WALinuxAgent/releases). Instalar a agente de hello como sigue:

    ```sh
    git clone https://github.com/Azure/WALinuxAgent 
    cd WALinuxAgent
    python setup.py install
    waagent -register-service
    ```

    > [!IMPORTANT]
    > Después de instalar al agente de Azure, es un tooverify buena idea que se está ejecutando como sigue:
    >
    > ```bash
    > ps auxw | grep waagent
    > root     79309  0.0  1.5  9184 15356 p1  S      4:11PM    0:00.46 python /usr/local/sbin/waagent -daemon (python2.7)
    > cat /var/log/waagent.log
    > ```

7. Desaprovisionamiento Hola tooclean del sistema y asegúrese de que adecuado para reaprovisionamiento. Hello siguiente comando también elimina última cuenta de usuario aprovisionado Hola y Hola asociado datos:

    ```sh
    waagent -deprovision+user -force
    ```

Ahora ya puede apagar la máquina virtual.


## <a name="prepare-hello-vhd"></a>Preparar Hola VHD
no se admite el formato VHDX Hello en Azure, solo **VHD fijo**. Puede convertir el formato de disco duro virtual de toofixed Hola disco mediante el Administrador de Hyper-V u Hola Powershell [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) cmdlet. A continuación se muestra un ejemplo.

```powershell
Convert-VHD OpenBSD61.vhdx OpenBSD61.vhd -VHDType Fixed
```

## <a name="create-storage-resources-and-upload"></a>Creación de recursos de almacenamiento y de carga
En primer lugar, cree un grupo de recursos con [az group create](/cli/azure/group#create). Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación:

```azurecli
az group create --name myResourceGroup --location eastus
```

tooupload el disco duro virtual, cree una cuenta de almacenamiento con [crear cuenta de almacenamiento az](/cli/azure/storage/account#create). Los nombres de la cuenta de almacenamiento deben ser únicos, así que indique su propio nombre. Hello en el ejemplo siguiente se crea una cuenta de almacenamiento denominada *mystorageaccount*:

```azurecli
az storage account create --resource-group myResourceGroup \
    --name mystorageaccount \
    --location eastus \
    --sku Premium_LRS
```

toocontrol tener acceso a la cuenta de almacenamiento toohello, obtener la clave de almacenamiento de hello con [lista de claves de cuenta de almacenamiento az](/cli/azure/storage/account/keys#list) como se indica a continuación:

```azurecli
STORAGE_KEY=$(az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount \
    --query "[?keyName=='key1']  | [0].value" -o tsv)
```

Hola independiente de toologically discos duros virtuales carga, crear un contenedor dentro de la cuenta de almacenamiento de hello con [crear contenedor de almacenamiento az](/cli/azure/storage/container#create):

```azurecli
az storage container create \
    --name vhds \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```

Por último, cargue el VHD con el comando [az storage blob upload](/cli/azure/storage/blob#upload) como se indica a continuación:

```azurecli
az storage blob upload \
    --container-name vhds \
    --file ./OpenBSD61.vhd \
    --name OpenBSD61.vhd \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```


## <a name="create-vm-from-your-vhd"></a>Creación de una máquina virtual desde el disco duro virtual
Puede crear una máquina virtual con un [script de ejemplo](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) o directamente con [az vm create](/cli/azure/vm#create). toospecify Hola se cargan, de VHD OpenBSD uso hello `--image` parámetro como sigue:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myOpenBSD61 \
    --image "https://mystorageaccount.blob.core.windows.net/vhds/OpenBSD61.vhd" \
    --os-type linux \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

Obtener dirección IP de hello de la VM OpenBSD con [az vm lista-ip-addresses](/cli/azure/vm#list-ip-addresses) como se indica a continuación:

```azurecli
az vm list-ip-addresses --resource-group myResourceGroup --name myOpenBSD61
```

Ahora puede SSH tooyour OpenBSD VM como normal:
        
```bash
ssh azureuser@<ip address>
```


## <a name="next-steps"></a>Pasos siguientes
Si desea más información acerca de Hyper-V se admiten en OpenBSD6.1 de tooknow, leer [OpenBSD 6.1](https://www.openbsd.org/61.html) y [hyperv.4](http://man.openbsd.org/hyperv.4).

Si desea toocreate una máquina virtual desde disco administrado, leer [disco az](/cli/azure/disk). 
