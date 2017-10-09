---
title: aaaIntroduction tooLinux en Azure | Documentos de Microsoft
description: "Aprenda a utilizar máquinas virtuales de Linux en Azure."
services: virtual-machines-linux
documentationcenter: python
author: szarkos
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: b13bf305-87bf-4df3-815e-e8f6337aa6ea
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: szark
ms.openlocfilehash: 3a931447ee23ce7000174ca314c3e10abc6b8e74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toolinux-on-azure"></a>Introducción tooLinux en Azure
Este tema proporciona información general sobre algunos aspectos del uso de máquinas virtuales de Linux en hello nube de Azure. La implementación de una máquina virtual Linux es un proceso sencillo usar una imagen de la Galería de Hola.

## <a name="authentication-usernames-passwords-and-ssh-keys"></a>Autenticación: Nombres de usuario, contraseñas y claves SSH.
Al crear una máquina virtual de Linux con hello portal de Azure, deberá tooprovide un cualquier nombre de usuario y una contraseña o una clave pública SSH. elección de un nombre de usuario para la implementación de una máquina virtual de Linux en Azure Hello es toohello asunto siguiente restricción: nombres de cuentas del sistema (UID < 100) ya está presente en hello máquina virtual no se permiten, 'raíz' por ejemplo.

* Consulte [Creación de una máquina virtual que ejecuta Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Vea [cómo tooUse SSH con Linux en Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="obtaining-superuser-privileges-using-sudo"></a>Obtención de privilegios de superusuario con el uso de `sudo`
cuenta de usuario de Hola que se especifica durante la implementación de la instancia de máquina virtual en Azure es una cuenta con privilegios. Esta cuenta se configura por mediante Hola Hola agente Linux de Azure toobe tooelevate capaz de privilegios tooroot (cuenta de superusuario) `sudo` utilidad. Una vez iniciada la sesión con esta cuenta de usuario, será capaz de toorun comandos como raíz mediante la sintaxis de comando de hello:

    # sudo <COMMAND>

También puede obtener un shell root con **sudo -s**.

* Consulte [Uso de privilegios raíz en máquinas virtuales con Linux en Azure](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="firewall-configuration"></a>Configuración del firewall
Azure proporciona un filtro de paquetes entrantes que restringe tooports conectividad especificado en hello portal de Azure. De forma predeterminada, hello sólo puerto permitido es SSH. Puede abrir puertos tooadditional de acceso en la máquina virtual de Linux mediante la configuración de puntos de conexión en hello portal de Azure:

* Véase: [cómo tooSet extremos tooa Máquina Virtual](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

las imágenes de Linux de Hola Hola Galería de Azure permiten hello *iptables* firewall de forma predeterminada. Si lo desea, puede configurarse firewall hello tooprovide un filtrado adicional.

## <a name="hostname-changes"></a>Cambios del nombre de host
Cuando se implementa inicialmente una instancia de una imagen de Linux, son tooprovide requiere un nombre de host de máquina virtual de Hola. Una vez que se ejecuta la máquina virtual de hello, este nombre de host es servidores DNS de plataforma de toohello publicado para que varios tooeach de máquinas virtuales conectadas otros puedan realizar búsquedas de direcciones IP con nombres de host.

Si desea realizar cambios de nombre de host con una vez implementada una máquina virtual, use el comando hello

    # sudo hostname <newname>

Hola agente Linux de Azure incluye funcionalidad tooautomatically detectar este cambio de nombre y adecuadamente configurar toopersist de máquina virtual de hello este cambio y publicar este servidores DNS de cambio toohello plataforma.

* [Guía de usuario del Agente de Linux de Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="cloud-init"></a>Cloud-Init
Las imágenes de **Ubuntu** y **CoreOS** usan cloud-init en Azure, que proporciona funcionalidades adicionales para arrancar una máquina virtual.

* [¿Cómo tooInject datos personalizados](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Custom Data and Cloud-Init on Microsoft Azure (Datos personalizados y cloud-init en Microsoft Azure)](https://azure.microsoft.com/blog/2014/04/21/custom-data-and-cloud-init-on-windows-azure/)
* [Create Azure Swap Partitions Using Cloud-Init (Creación de particiones de intercambio de Azure con cloud-init)](https://wiki.ubuntu.com/AzureSwapPartitions)
* [Cómo tooUse CoreOS en Azure](https://coreos.com/os/docs/latest/booting-on-azure.html)

## <a name="virtual-machine-image-capture"></a>Captura de imagen de máquina virtual
Azure proporciona estado de hello capacidad toocapture Hola de una máquina virtual existente en una imagen que posteriormente se puede ser instancias de máquina virtual adicional de toodeploy usado. Hola agente Linux de Azure puede ser usado toorollback algunos de Hola personalización que se realizó durante el proceso de aprovisionamiento de Hola. Puede seguir estos pasos hello toocapture una máquina virtual como una imagen:

1. Ejecutar **waagent-deprovision** tooundo aprovisionamiento de personalización. O **waagent-deprovision + usuario** toooptionally eliminar cuenta de usuario de hello especificada durante el aprovisionamiento y todos los datos asociados.
2. Apagar abajo/apagar máquina virtual de Hola.
3. Haga clic en **capturar** hello Azure Hola portal o use PowerShell o CLI herramientas toocapture Hola virtual machine como una imagen.
   
   * Véase: [cómo tooCapture una tooUse de máquina Virtual Linux como una plantilla](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="attaching-disks"></a>Acoplamiento de discos
Las máquinas virtuales disponen de un *disco de recursos* local y temporal acoplado. Porque los datos en un disco de recursos pueden no ser duraderos durante el reinicio, se utiliza a menudo, las aplicaciones y procesos que se ejecutan en la máquina virtual de Hola para transitorio y **temporal** almacenamiento de datos. También es usado toostore Hola página o archivos de intercambio para el sistema operativo de Hola.

En Linux, se suele estar a cargo Hola agente Linux de Azure y monta automáticamente demasiado disco del recurso de hello**/mnt/resource** (o **/mnt** en Ubuntu imágenes).

> [!NOTE]
> Tenga en cuenta ese disco del recurso de hello es un **temporal** en disco y que se puede eliminar y cambiar el formato cuando hello VM se reinicia.
> 
> 

En Linux, disco de datos de hello podría llamarse kernel hello como `/dev/sdc`, y los usuarios deberán toopartition, dar formato y montar ese recurso. Este tema se trata el tutorial de hello instrucciones paso a paso: [cómo tooAttach una máquina Virtual de disco de datos tooa](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

* **Consulte también:**[Configuración del software RAID en Linux](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) y  & [Configuración del LVM en una máquina virtual Linux en Azure](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

