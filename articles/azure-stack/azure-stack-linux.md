---
title: Invitados de aaaLinux en la pila de Azure | Documentos de Microsoft
description: "Aprenda a crear máquinas virtuales basadas en Linux en Azure Stack."
services: azure-stack
documentationcenter: 
author: anjayajodha
manager: byronr
editor: 
ms.assetid: d2155c59-902e-4f63-ac58-d19e6a765380
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: anajod
ms.openlocfilehash: 225bed7d630b676ca760add25731e347516b5bf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-linux-virtual-machines-on-azure-stack"></a>Implementación de máquinas virtuales Linux en Azure Stack
Puede implementar máquinas virtuales Linux en hello Kit de desarrollo de pila de Azure mediante la adición de una imagen basada en Linux en hello Azure Marketplace de pila. Varios proveedores de Linux han proporcionado imágenes que se pueden agregar a Azure Stack Development Kit o puede crear las suyas propias.

## <a name="download-an-image"></a>Descarga de una imagen
1. Descargue y extraiga una imagen compatible con Azure pila Hola siguientes vínculos o preparar su propia:
   
   * [Bitnami](https://bitnami.com/azure-stack)
   * [CentOS](http://olstacks.cloudapp.net/latest/)
   * [CoreOS](https://stable.release.core-os.net/amd64-usr/current/coreos_production_azure_image.vhd.bz2)
   * [SuSE](https://download.suse.com/Download?buildid=VCFi7y7MsFQ~)
   * [Ubuntu 14.04 LTS](https://partner-images.canonical.com/azure/azure_stack/) / [Ubuntu 16.04 LTS](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)
2. Extraiga la imagen de hello VHD si es necesario y [Agregar imagen de hello toohello Marketplace](azure-stack-add-vm-image.md). Asegúrese de que ese hello `OSType` parámetro está establecido demasiado`Linux`.
3. Una vez agregado Hola imagen toohello Marketplace, se crea un elemento de Marketplace y puede implementar una máquina virtual Linux.

## <a name="prepare-your-own-image"></a>Preparación de su propia imagen
1. Preparar su propia imagen de Linux mediante uno de hello siguiendo las instrucciones:
   
   * [Distribuciones basadas en CentOS](../virtual-machines/linux/create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [Debian Linux](../virtual-machines/linux/debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [Oracle Linux](../virtual-machines/linux/oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [Red Hat Enterprise Linux](../virtual-machines/linux/redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [SLES y openSUSE](../virtual-machines/linux/suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [Ubuntu](../virtual-machines/linux/create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. Descargue e instale hello [agente Linux de Azure](https://github.com/Azure/WALinuxAgent/)
   
    Hola versión del agente de Linux de Azure 2.1.3 o posterior es necesario tooprovision la VM de Linux en la pila de Azure. Muchas de las distribuciones de hello mencionadas anteriormente ya incluyen esta versión de agente de Hola o superior como un paquete en sus repositorios (suele denominarse `WALinuxAgent` o `walinuxagent`). Sin embargo, si hello versión del paquete de agente de Azure de hello es menor que 2.1.3 (es decir, 2.0.18 o inferior), tendrá que instalar manualmente el agente de Hola. puede determinar la versión de Hola instalado desde el nombre del paquete de Hola o mediante la ejecución de `/usr/sbin/waagent -version` en hello máquina virtual.
   
    Siga las instrucciones de hello debajo de agente de Linux de Azure de hello tooinstall de manualmente:
   
   * En primer lugar, descargue Hola de agente de Linux de Azure más reciente de [GitHub](https://github.com/Azure/WALinuxAgent/releases), ejemplo:
     
            # wget https://github.com/Azure/WALinuxAgent/archive/v2.2.0.tar.gz
   * Desempaquetar Hola agente de Azure:
     
            # tar -vzxf v2.2.0.tar.gz
   * Instale python-setuptools
     
        **Debian y Ubuntu**
     
            # sudo apt-get update
            # sudo apt-get install python-setuptools
     
        **Ubuntu 16.04+**
     
            # sudo apt-get install python3-setuptools
     
        **RHEL, CentOS y Oracle Linux**
     
            # sudo yum install python-setuptools
   * Instalar Hola agente de Azure:
     
            # cd WALinuxAgent-2.2.0
            # sudo python setup.py install --register-service
     
     Sistemas con Python 2.x y 3.x instalado de Python side-by-side pueden necesitar hello toorun siguiente comando:
     
         sudo python3 setup.py install --register-service
     Para obtener más información, vea Hola agente Linux de Azure [Léame](https://github.com/Azure/WALinuxAgent/blob/master/README.md).
3. [Agregar imagen de hello toohello Marketplace](azure-stack-add-vm-image.md). Asegúrese de que ese hello `OSType` parámetro está establecido demasiado`Linux`.
4. Una vez agregado Hola imagen toohello Marketplace, se crea un elemento de Marketplace y puede implementar una máquina virtual Linux.

## <a name="next-steps"></a>Pasos siguientes
[Preguntas frecuentes acerca de Azure Stack](azure-stack-faq.md)

