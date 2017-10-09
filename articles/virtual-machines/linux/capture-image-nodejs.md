---
title: "aaaCapture un toouse de máquina virtual de Linux de Azure como una plantilla | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocapture y generalizar una imagen de una basados en Linux Azure máquina virtual (VM) creada con el modelo de implementación de hello Azure Resource Manager."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 877eee5c842bebe80e755c2240cdaaef4ade6ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="capture-a-linux-virtual-machine-running-on-azure"></a>Captura de una máquina virtual Linux que se ejecuta en Azure
Siga los pasos de hello en este artículo toogeneralize y capturar la máquina virtual de Linux de Azure (VM) en el modelo de implementación del Administrador de recursos de Hola. Cuando se generaliza Hola VM, quita información de la cuenta personal y preparar Hola VM toobe utilizado como una imagen. , A continuación, captura la imagen de un disco duro virtual (VHD) generalizado para hello OS, discos duros virtuales en los discos de datos adjuntos, y un [plantilla del Administrador de recursos](../../azure-resource-manager/resource-group-overview.md) para nuevas implementaciones de máquina virtual. Este artículo detalla cómo toocapture una máquina virtual de la imagen con hello 1.0 de CLI de Azure para una máquina virtual con discos no administrados. También puede [capturar una máquina virtual mediante discos de Azure administrados con hello Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Discos administrados se controlan mediante la plataforma Windows Azure hello y no requieren ningún toostore los preparativos o ubicación ellos. Para obtener más información, consulte [Azure Managed Disks overview](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Información general sobre Azure Managed Disks). 

toocreate máquinas virtuales con la imagen de hello, configurar los recursos de red para cada nueva máquina virtual y usar Hola plantilla (un archivo JavaScript Object Notation o JSON,) toodeploy de hello captura imágenes de disco duro virtual. De esta manera, puede replicar una máquina virtual con su actual configuración de software, manera toohello similar que use imágenes en hello Azure Marketplace.

> [!TIP]
> Si desea toocreate una copia de la VM de Linux existente con su estado especializada para la depuración o de copia de seguridad, consulte [crear una copia de una máquina virtual de Linux con Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Si desea tooupload un VHD Linux desde una máquina virtual local vea [cargar y crear una VM Linux de imagen de disco personalizado](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).  

## <a name="cli-versions-toocomplete-hello-task"></a>Tarea CLI versiones toocomplete hello
Puede completar la tarea hello mediante uno de hello después de las versiones CLI:

- [Azure 1.0 de CLI](#before-you-begin) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)
- [Azure 2.0 CLI](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola

## <a name="before-you-begin"></a>Antes de empezar
Asegúrese de que se cumple Hola siguiendo los requisitos previos:

* **Máquina virtual de Azure creado en el modelo de implementación del Administrador de recursos de hello** -si no ha creado una VM de Linux, puede usar hello [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), hello [CLI de Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), o [el Administrador de recursos plantillas de](create-ssh-secured-vm-from-template.md). 
  
    Configurar Hola VM según sea necesario. Por ejemplo, [agregue discos de datos](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), aplique actualizaciones e instale aplicaciones. 
* **CLI de Azure** -Install hello [CLI de Azure](../../cli-install-nodejs.md) en un equipo local.

## <a name="step-1-remove-hello-azure-linux-agent"></a>Paso 1: Quitar el agente de Linux de Azure de Hola
En primer lugar, ejecute hello **waagent** comando con hello **deprovision** parámetro en hello VM de Linux. Este comando elimina archivos y datos toomake Hola VM listo para generalizar. Para obtener más información, vea hello [manual de usuario del agente Linux de Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

1. Conectar tooyour VM de Linux con un cliente de SSH.
2. En la ventana de hello SSH, escriba Hola siguiente comando:
   
    ```bash
    sudo waagent -deprovision+user
    ```
   > [!NOTE]
   > Solo se ejecute este comando en una máquina virtual que piensa toocapture como una imagen. No se garantiza dicha imagen Hola se borra de toda la información confidencial o es adecuada para su redistribución.
 
3. Tipo de **y** toocontinue. Puede agregar hello **-forzar** parámetro tooavoid este paso de confirmación.
4. Una vez completado el comando de hello, escriba **salir**. Este paso cierra el cliente de SSH Hola.

## <a name="step-2-capture-hello-vm"></a>Paso 2: Capturar Hola VM
Utilice hello Azure CLI toogeneralize y capturar Hola máquina virtual. En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores. Los nombres de parámetro de ejemplo incluyen **myResourceGroup**, **myVnet** y **myVM**.

1. En el equipo local, abra Hola CLI de Azure y [tooyour suscripción de Azure de inicio de sesión](../../xplat-cli-connect.md). 
2. Asegúrese de que está en modo de Resource Manager.
   
    ```azurecli
    azure config mode arm
    ```
3. Apagar la máquina virtual que ya se desaprovisionó utilizando el siguiente comando de Hola Hola:
   
    ```azurecli
    azure vm deallocate -g myResourceGroup -n myVM
    ```
4. Generalizar Hola VM con hello siguiente comando:
   
    ```azurecli
    azure vm generalize -g myResourceGroup -n myVM
    ```
5. Ahora ejecute hello **captura de máquina virtual de azure** comando, que captura Hola máquina virtual. En el siguiente ejemplo de Hola, imagen Hola discos duros virtuales se capturan con nombres empiezan por **MyVHDNamePrefix**, hello y **-t** opción especifica una plantilla de ruta de acceso toohello **MyTemplate.json**. 
   
    ```azurecli
    azure vm capture -g myResourceGroup -n myVM -p myVHDNamePrefix -t myTemplate.json
    ```
   
   > [!IMPORTANT]
   > archivos de disco duro virtual de imagen de Hello creando de forma predeterminada en hello usa la misma cuenta de almacenamiento que Hola VM original. Hola de uso *misma cuenta de almacenamiento* toostore Hola discos duros virtuales para las nuevas máquinas virtuales se crea desde Hola imagen. 

6. ubicación de hello toofind de una imagen capturada, plantilla JSON de hello abierto en un editor de texto. Hola **storageProfile**, encontrar Hola **uri** de hello **imagen** ubicado en hello **system** contenedor. Por ejemplo, hello URI de imagen de disco de SO hello es similar demasiado`https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`

## <a name="step-3-create-a-vm-from-hello-captured-image"></a>Paso 3: Crear una máquina virtual desde la imagen de captura de Hola
Ahora puede usar imagen Hola con un toocreate plantilla una VM de Linux. Estos pasos muestran cómo toouse Hola CLI de Azure y Hola plantilla de archivo JSON se capturó toocreate Hola VM en una nueva red virtual.

### <a name="create-network-resources"></a>Crear recursos de red
plantilla de hello toouse, primero debe tooset seguridad de una red virtual y la NIC para la nueva máquina virtual. Se recomienda que crear un grupo de recursos para estos recursos en lugar de Hola donde se almacena la imagen de máquina virtual. Ejecute comandos similar toohello siguientes, sustituyendo los nombres de los recursos y una ubicación de Azure adecuada ("centralus" en estos comandos):

```azurecli
azure group create myResourceGroup1 -l "centralus"

azure network vnet create myResourceGroup1 myVnet -l "centralus"

azure network vnet subnet create myResourceGroup1 myVnet mySubnet

azure network public-ip create myResourceGroup1 myPublicIP -l "centralus"

azure network nic create myResourceGroup1 myNIC -k mySubnet -m myVnet -p myPublicIP -l "centralus"
```

### <a name="get-hello-id-of-hello-nic"></a>Obtener Hola Id. de hello NIC
toodeploy una máquina virtual desde la imagen de hello mediante Hola guardó durante la captura JSON, necesita Hola Id. de hello NIC. Obtenerlo ejecutando Hola siguiente comando:

```azurecli
azure network nic show myResourceGroup1 myNIC
```

Hola **identificador** Hola salida es similar demasiado`/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`

### <a name="create-a-vm"></a>Creación de una VM
Ahora la siguiente ejecución Hola comando toocreate la máquina virtual de hello captura la imagen de máquina virtual. Hola de uso **-f** toohello plantilla JSON de parámetro toospecify Hola ruta de acceso de archivo se guarda.

```azurecli
azure group deployment create myResourceGroup1 MyDeployment -f MyTemplate.json
```

En la salida del comando hello, son toosupply solicitada un nuevo nombre de máquina virtual, nombre de usuario de administrador de hello y una contraseña y Hola Id. de hello NIC que creó anteriormente.

```bash
info:    Executing command group deployment create
info:    Supply values for hello following parameters
vmName: myNewVM
adminUserName: myAdminuser
adminPassword: ********
networkInterfaceId: /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resource Groups/myResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
```

Hola siguiendo el ejemplo muestra lo que se ve una implementación correcta:

```bash
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment xxxxxxx
+ Waiting for deployment toocomplete
data:    DeploymentName     : MyDeployment
data:    ResourceGroupName  : MyResourceGroup1
data:    ProvisioningState  : Succeeded
data:    Timestamp          : xxxxxxx
data:    Mode               : Incremental
data:    Name                Type          Value

data:    ------------------  ------------  -------------------------------------

data:    vmName              String        myNewVM

data:    vmSize              String        Standard_D1

data:    adminUserName       String        myAdminuser

data:    adminPassword       SecureString  undefined

data:    networkInterfaceId  String        /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
info:    group deployment create command OK
```

### <a name="verify-hello-deployment"></a>Comprobar la implementación de Hola
Ahora SSH toohello máquina virtual que creó la implementación de hello tooverify y empezar a usar Hola nueva máquina virtual. tooconnect mediante SSH, buscar la dirección IP de Hola de hello máquina virtual que creó mediante la ejecución de hello siguiente comando:

```azurecli
azure network public-ip show myResourceGroup1 myPublicIP
```

la dirección IP pública Hola se muestra en la salida del comando Hola. De forma predeterminada se conectará toohello VM de Linux mediante SSH en el puerto 22.

## <a name="create-additional-vms"></a>Creación de máquinas virtuales adicionales
Hola de uso captura imagen y plantilla toodeploy máquinas virtuales adicionales siguiendo los pasos de Hola Hola sección anterior. Otro toocreate máquinas virtuales de opciones de imagen de hello incluyen utilizando una plantilla de inicio rápido o ejecutando hello **crear la máquina virtual de azure** comando.

### <a name="use-hello-captured-template"></a>Usar plantilla capturada Hola
Hola toouse captura imagen y plantilla, siga estos pasos (que se detallan en la sección anterior de hello):

* Asegúrese de que la imagen de máquina virtual está en hello misma cuenta de almacenamiento que hospeda el VHD de la máquina virtual.
* Copie el archivo JSON de hello plantilla y especifique un nombre único para el disco del sistema operativo Hola de hello nueva VM VHD (o discos duros virtuales). Por ejemplo, en hello **storageProfile**, en **vhd**, en **uri**, especifique un nombre único para hello **osDisk** VHD, similar demasiado`https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`
* Cree una NIC en cualquier Hola mismo u otra red virtual.
* Mediante el archivo JSON de plantilla de hello modificado, cree una implementación en el grupo de recursos de hello en el que configura la red virtual de Hola.

### <a name="use-a-quickstart-template"></a>Uso de una plantilla de inicio rápido
Si desea configurar automáticamente cuando se crea una máquina virtual desde la imagen de Hola de red de hello, puede especificar esos recursos en una plantilla. Por ejemplo, vea hello [plantilla de imagen de máquina virtual de usuario de 101](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) desde GitHub. Esta plantilla crea una máquina virtual desde su imagen personalizada y red virtual de hello es necesario, la dirección IP pública y recursos NIC. Para ver un tutorial del uso de plantilla de Hola Hola portal de Azure, consulte [cómo toocreate una máquina virtual desde una imagen personalizada con una plantilla de administrador de recursos](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).

### <a name="use-hello-azure-vm-create-command"></a>Use hello azure vm create, comando
Normalmente es más fácil toouse un toocreate de plantilla de administrador de recursos una máquina virtual desde la imagen de Hola. Sin embargo, puede crear Hola VM *imperativamente* mediante el uso de hello **crear la máquina virtual de azure** comando con hello **-Q** (**--imagen urn**) parámetro . Si utiliza este método, también pasar hello **-d** (**vhd del disco de SO--**) Hola de ubicación de hello toospecify de parámetro del archivo .vhd de hello OS para nueva máquina virtual. Este archivo debe estar en el contenedor de discos duros virtuales de Hola de cuenta de almacenamiento de Hola donde se almacena el archivo de disco duro virtual de imagen de hello. Hola comando copias Hola VHD para hello nueva máquina virtual automáticamente toohello **discos duros virtuales** contenedor.

Antes de ejecutar **crear la máquina virtual de azure** con la imagen de hello, completar Hola pasos:

1. Crear un grupo de recursos o identificar un grupo de recursos existente para la implementación de Hola.
2. Crear un complemento público recurso de dirección IP y un recurso NIC para Hola nueva máquina virtual. Para pasos toocreate una red virtual, dirección IP pública y NIC mediante el uso de hello CLI, vea anteriormente en este artículo. (**crear la máquina virtual de azure** también se puede crear una NIC, pero debe toopass los parámetros adicionales para una red virtual y subred.)

A continuación, ejecutar un comando que pasa a URI hello existente de la imagen y archivo tooboth Hola de nuevo disco duro virtual del sistema operativo. En este ejemplo, se crea un tamaño de VM de Standard_A1 en la región de hello este de EE..

```azurecli
azure vm create -g myResourceGroup1 -n myNewVM -l eastus -y Linux \
-z Standard_A1 -u myAdminname -p myPassword -f myNIC \
-d "https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix.vhd" \
-Q "https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.vhd"
```

Para obtener opciones de comando adicionales, ejecute `azure help vm create`.

## <a name="next-steps"></a>Pasos siguientes
toomanage las máquinas virtuales con hello CLI, vea tareas de hello en [implementar y administrar máquinas virtuales usando plantillas del Administrador de recursos de Azure y hello Azure CLI](create-ssh-secured-vm-from-template.md).

