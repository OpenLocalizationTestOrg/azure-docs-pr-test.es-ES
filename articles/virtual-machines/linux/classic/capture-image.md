---
title: aaaCapture una imagen de una VM de Linux | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocapture una imagen de una basados en Linux Azure máquina virtual (VM) creado con el modelo de implementación clásica de Hola."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17d7ffee-a58e-4290-9de1-64c3cf1ddc05
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 33c4059d5bb919a86bdc3492abca540750f365ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocapture-a-classic-linux-virtual-machine-as-an-image"></a>¿Cómo toocapture una máquina virtual de Linux clásica como imagen
> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. Obtenga información acerca de cómo demasiado[realizar estos pasos con el modelo del Administrador de recursos de hello](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Este artículo muestra cómo toocapture una clásica máquina virtual de Azure (VM) ejecutan Linux como una imagen toocreate otras máquinas virtuales. Esta imagen de disco del sistema operativo hello y discos de datos acoplados toohello máquina virtual. No incluye la configuración de red, por lo que necesita tooconfigure que cuando creas Hola otra máquina virtual desde la imagen de Hola.

Almacenes de Azure Hola imagen en **imágenes**, junto con las imágenes que ha cargado. Para obtener más información sobre las imágenes, consulte [Acerca de las imágenes para las máquinas virtuales Linux][About Virtual Machine Images in Azure].

## <a name="before-you-begin"></a>Antes de empezar
Estos pasos se supone que ya ha creado una máquina virtual de Azure mediante el modelo de implementación clásica de Hola y sistema operativo de hello configurado, incluida la conexión de los discos de datos. Si necesita toocreate una máquina virtual, lea [cómo tooCreate una máquina Virtual Linux][How tooCreate a Linux Virtual Machine].

## <a name="capture-hello-virtual-machine"></a>Captura de máquina virtual de Hola
1. [Conectar toohello VM](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) mediante un cliente de SSH de su elección.
2. En la ventana de hello SSH, escriba Hola siguiente comando. Hola de salida de `waagent` puede variar ligeramente según la versión de Hola de esta utilidad:

    ```bash
    sudo waagent -deprovision+user
    ```

    Hola comando anterior intentos de sistema de hello tooclean y que sea adecuado para reaprovisionamiento. Esta operación realiza Hola siguientes tareas:

   * Quita las claves de host SSH (si Provisioning.RegenerateSshHostKeyPair es 'y' en el archivo de configuración de hello)
   * Borra la configuración de Nameserver en /etc/resolv.conf
   * Quita hello `root` contraseña de usuario de/etcetera/instantáneas (si Provisioning.DeleteRootPassword es 'y' en el archivo de configuración de hello)
   * Quita concesiones del cliente de DHCP en caché
   * Restablece toolocalhost.localdomain de nombre de host
   * Elimina la última cuenta de usuario aprovisionado hello (obtenido de /var/lib/waagent) **y los datos asociados**.

     > [!NOTE]
     > Desaprovisionamiento elimina archivos y datos demasiado "generalizar" hello imagen. Solo se ejecute este comando en una máquina virtual que piensa toocapture como una nueva plantilla de imagen. No se garantiza dicha imagen Hola se borra de toda la información confidencial o es adecuada para las partes de toothird de redistribución.

3. Tipo de **y** toocontinue. Puede agregar hello `-force` parámetro tooavoid este paso de confirmación.
4. Tipo de **Exit** cliente de SSH de tooclose Hola.

   > [!NOTE]
   > Hello pasos restantes se supone que ya está [instalado hello Azure CLI](../../../cli-install-nodejs.md) en el equipo cliente. También es posible Hola todos los pasos en hello [portal de Azure](http://portal.azure.com).

5. En el equipo cliente, abra CLI de Azure y el inicio de sesión tooyour suscripción de Azure. Para obtener más información, lea [conectarse tooan suscripción de Azure desde hello Azure CLI](../../../xplat-cli-connect.md).

   > [!NOTE]
   > Hola portal de Azure, inicie sesión en el portal de toohello.

6. Asegúrese de que está en modo de administración de servicios:

    ```azurecli
    azure config mode asm
    ```

7. Apagar máquina virtual que ya se desaprovisiona Hola. Hello en el ejemplo siguiente se cierra Hola máquina virtual denominada `myVM`:

    ```azurecli
    azure vm shutdown myVM
    ```
   Si es necesario, puede ver una lista Hola todas las máquinas virtuales se crea en su suscripción mediante`azure vm list`

   > [!NOTE]
   > Si usas Hola portal de Azure, seleccione Hola máquina virtual y haga clic en **detener** apagar VM Hola.

8. Cuando se detiene Hola VM, capture la imagen de Hola. Hola siguientes capturas de ejemplo Hola máquina virtual denominada `myVM` y crea una imagen generalizada denominada `myNewVM`:

    ```azurecli
    azure vm capture -t myVM myNewVM
    ```

    Hola `-t` subcomando eliminaciones Hola máquina virtual original.

    > [!NOTE]
    > Hola portal de Azure, puede capturar una imagen seleccionando **imagen** desde el menú del concentrador de Hola. Necesita hello toosupply siguiendo la información de imagen de Hola: nombre, grupo de recursos, ubicación, tipo de sistema operativo y ruta de acceso de almacenamiento blob.

9. Hola nueva imagen está ahora disponible en hello lista de imágenes que se puede usa tooconfigure cualquier nueva máquina virtual. Puede verlo con el comando hello:

   ```azurecli
   azure vm image list
   ```

   En hello [portal de Azure](http://portal.azure.com), Hola nueva imagen aparece en hello **imágenes de máquina virtual (clásica)** que pertenece toohello **proceso** servicios. Puede tener acceso a **imágenes de máquina virtual (clásica)** haciendo clic en _más servicios_ final Hola de hello Azure servicio lista y, a continuación, busca en hello **proceso** servicios.   

   ![Captura correcta de la imagen](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a>Pasos siguientes
imagen de Hello es toocreate toobe listo usa máquinas virtuales. Puede usar el comando de CLI de Azure de hello `azure vm create` y nombre de la imagen de Hola de alimentación que creó. Para obtener más información, consulte [Using Hola CLI de Azure con el modelo de implementación clásica](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

O bien, usar hello [portal de Azure](http://portal.azure.com) toocreate una máquina virtual personalizada mediante el uso de hello **imagen** método y seleccionando hello de la imagen que ha creado. Para obtener más información, consulte [cómo tooCreate una VM personalizada][How tooCreate a Custom Virtual Machine].

**Consulte también:**[Guía de usuario del Agente de Linux de Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[About Virtual Machine Images in Azure]:../../virtual-machines-linux-classic-about-images.md
[How tooCreate a Custom Virtual Machine]:create-custom.md
[How tooAttach a Data Disk tooa Virtual Machine]:attach-disk.md
[How tooCreate a Linux Virtual Machine]:create-custom.md
