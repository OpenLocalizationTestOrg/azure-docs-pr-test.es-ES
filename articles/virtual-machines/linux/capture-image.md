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
# <a name="how-toocreate-an-image-of-a-virtual-machine-or-vhd"></a>¿Cómo toocreate una imagen de una máquina virtual o un disco duro virtual

<!-- generalize, image - extended version of hello tutorial-->

toocreate varias copias de una máquina virtual (VM) toouse en Azure, capturar una imagen de VM de Hola u Hola VHD de sistema operativo. toocreate una imagen, necesita quitar información de cuenta personal que resulta más seguro toodeploy varias veces. Hola siguiendo los pasos que se cancela el aprovisionamiento de una máquina virtual existente, cancelar la asignación y crear una imagen. Puede usar esta imagen toocreate máquinas virtuales a través de cualquier grupo de recursos dentro de su suscripción.

Si desea toocreate una copia de la VM de Linux existentes para copia de seguridad o la depuración, o cargar un VHD de Linux especializadas de una máquina virtual local, vea [cargar y crear una VM Linux de imagen de disco personalizado](upload-vhd.md).  

También puede usar **compresor** toocreate su configuración personalizada. Para obtener más información sobre el uso de compresor, consulte [cómo imágenes de máquina virtual de toouse compresor toocreate Linux de Azure](build-image-with-packer.md).


## <a name="before-you-begin"></a>Antes de empezar
Asegúrese de que se cumple Hola siguiendo los requisitos previos:

* Necesita una máquina virtual de Azure creados en el modelo de implementación de administrador de recursos de hello mediante discos administrados. Si no ha creado una VM de Linux, puede usar hello [portal](quick-create-portal.md), hello [CLI de Azure](quick-create-cli.md), o [plantillas del Administrador de recursos](create-ssh-secured-vm-from-template.md). Configurar Hola VM según sea necesario. Por ejemplo, [agregue discos de datos](add-disk.md), aplique actualizaciones e instale aplicaciones. 

* También necesita toohave hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y haber iniciado sesión tooan cuenta de Azure con [inicio de sesión de az](/cli/azure/#login).

## <a name="quick-commands"></a>Comandos rápidos

Para una versión simplificada de este tema, para las pruebas, evaluar o de aprendizaje sobre máquinas virtuales en Azure, consulte [crear una imagen personalizada de una máquina virtual de Azure con hello CLI](tutorial-custom-images.md).


## <a name="step-1-deprovision-hello-vm"></a>Paso 1: Desaprovisionar Hola VM
Cancela el aprovisionamiento de hello VM utilizando el agente de máquina virtual de Azure de hello, archivos específicos de máquina de toodelete y datos. Hola de uso `waagent` comando con hello *-desaprovisionamiento + usuario* parámetro en el origen de VM de Linux. Para obtener más información, vea hello [manual de usuario del agente Linux de Azure](../windows/agent-user-guide.md).

1. Conectar tooyour VM de Linux con un cliente de SSH.
2. En la ventana de hello SSH, escriba Hola siguiente comando:
   
    ```bash
    sudo waagent -deprovision+user
    ```
<br>
   > [!NOTE]
   > Solo se ejecute este comando en una máquina virtual que piensa toocapture como una imagen. No se garantiza dicha imagen Hola se borra de toda la información confidencial o es adecuada para su redistribución. Hola *+ usuario* parámetro también elimina la última cuenta de usuario aprovisionado Hola. Si desea que las credenciales de cuenta de tookeep Hola VM, use *-deprovision* tooleave cuenta de usuario de hello en su lugar.
 
3. Tipo de **y** toocontinue. Puede agregar hello **-forzar** parámetro tooavoid este paso de confirmación.
4. Una vez completado el comando de hello, escriba **salir**. Este paso cierra el cliente de SSH Hola.

## <a name="step-2-create-vm-image"></a>Paso 2: Crear la imagen de máquina virtual
Utilice Hola CLI de Azure 2.0 toomark Hola VM tal y como se ha generalizado y capturar imagen de Hola. En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores. Los nombres de parámetro de ejemplo incluyen *myResourceGroup*, *myVnet* y *myVM*.

1. Cancela la asignación de hello máquina virtual que canceló el aprovisionamiento con [cancelar la asignación de máquina virtual az](/cli//azure/vm#deallocate). Hello en el ejemplo siguiente se desasigna Hola máquina virtual denominada *myVM* en grupo de recursos de hello llamado *myResourceGroup*:
   
    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myVM
    ```

2. Hola marca VM tal y como se ha generalizado con [az vm generalizar](/cli//azure/vm#generalize). Hola después de la máquina virtual denominada ejemplo marcas Hola Hola *myVM* en grupo de recursos de hello llamado *myResourceGroup* como generalizado:
   
    ```azurecli
    az vm generalize \
      --resource-group myResourceGroup \
      --name myVM
    ```

3. Ahora cree una imagen del recurso de la máquina virtual de hello con [crear imagen az](/cli//azure/image#create). Hello en el ejemplo siguiente se crea una imagen denominada *myImage* en grupo de recursos de hello llamado *myResourceGroup* utilizando el recurso de máquina virtual de hello denominado *myVM*:
   
    ```azurecli
    az image create \
      --resource-group myResourceGroup \
      --name myImage --source myVM
    ```
   
   > [!NOTE]
   > Hello imagen se crea en Hola mismo grupo de recursos que la máquina virtual de origen. Puede crear VM en cualquier grupo de recursos dentro de la suscripción a partir de esta imagen. Desde una perspectiva de administración, es recomendable toocreate un grupo de recursos específicos para los recursos de máquina virtual y las imágenes.

## <a name="step-3-create-a-vm-from-hello-captured-image"></a>Paso 3: Crear una máquina virtual desde la imagen de captura de Hola
Crear una máquina virtual mediante la imagen de hello creadas con [crear vm az](/cli/azure/vm#create). Hello en el ejemplo siguiente se crea una máquina virtual denominada *myVMDeployed* de imagen de hello denominada *myImage*:

```azurecli
az vm create \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --image myImage\
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```

### <a name="creating-hello-vm-in-another-resource-group"></a>Creación de hello VM en otro grupo de recursos 

Puede crear máquinas virtuales en cualquier grupo de recursos dentro de la suscripción a partir de una imagen. toocreate una máquina virtual en otro grupo de recursos de imagen de hello, especifique la imagen de tooyour de Id. de completa a recursos de Hola. Use [lista de imágenes de az](/cli/azure/image#list) tooview una lista de imágenes. Hola de salida es similar toohello siguiente ejemplo:

```json
"id": "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage",
   "location": "westus",
   "name": "myImage",
```

Hello siguiente ejemplo se utiliza [crear vm az](/cli/azure/vm#create) toocreate una máquina virtual en otro grupo de recursos de imagen de origen de hello especificando el identificador de recurso de imagen de hello:

```azurecli
az vm create \
   --resource-group myOtherResourceGroup \
   --name myOtherVMDeployed \
   --image "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage" \
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```


## <a name="step-4-verify-hello-deployment"></a>Paso 4: Comprobar la implementación de Hola

Ahora SSH toohello máquina virtual que creó la implementación de hello tooverify y empezar a usar Hola nueva máquina virtual. tooconnect mediante SSH, buscar la dirección IP de Hola o el FQDN de la máquina virtual con [mostrar de la máquina virtual de az](/cli/azure/vm#show):

```azurecli
az vm show \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --show-details
```

## <a name="next-steps"></a>Pasos siguientes
Puede crear varias VM a partir de la imagen de VM de origen. Si necesita que la imagen de tooyour de toomake cambios: 

- Cree una máquina virtual a partir de la imagen.
- Realice actualizaciones o cambios de configuración.
- Siga Hola nuevo pasos toodeprovision, cancelar la asignación, generalizar y crear una imagen.
- Use esta nueva imagen para implementaciones futuras. Si lo desea, elimine la imagen original Hola.

Para obtener más información acerca de cómo administrar las máquinas virtuales con hello CLI, consulte [CLI de Azure 2.0](/cli/azure/overview).
