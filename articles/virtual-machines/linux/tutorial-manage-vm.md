---
title: "aaaCreate y administrar máquinas virtuales de Linux con Hola CLI de Azure | Documentos de Microsoft"
description: "Tutorial: crear y administrar máquinas virtuales de Linux con Hola CLI de Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 05f7c1cf860f809bc13f110778d3bddd619ac6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-linux-vms-with-hello-azure-cli"></a>Crear y administrar máquinas virtuales de Linux con Hola CLI de Azure

Las máquinas virtuales de Azure proporcionan un entorno informático completamente configurable y flexible. En este tutorial se tratan elementos básicos de la implementación de máquinas virtuales de Azure, como la selección de su tamaño, la selección de una imagen de máquina virtual y la implementación de una máquina virtual. Aprenderá a:

> [!div class="checklist"]
> * Crear y conectar tooa VM
> * Seleccionar y usar imágenes de máquinas virtuales
> * Ver y usar tamaños de una máquina virtual específicos
> * Cambiar el tamaño de una máquina virtual
> * Ver y entender el estado de las máquinas virtuales


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-resource-group"></a>Creación de un grupo de recursos

Crear un grupo de recursos con hello [crear grupo az](https://docs.microsoft.com/cli/azure/group#create) comando. 

Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure. Se debe crear un grupo de recursos antes de una máquina virtual. En este ejemplo, un grupo de recursos denominado *myResourceGroupVM* se crea en hello *eastus* región. 

```azurecli-interactive 
az group create --name myResourceGroupVM --location eastus
```

grupo de recursos de Hola se especifica al crear o modificar una máquina virtual, que puede ser vista a lo largo de este tutorial.

## <a name="create-virtual-machine"></a>Create virtual machine

Crear una máquina virtual con hello [crear vm az](https://docs.microsoft.com/cli/azure/vm#create) comando. 

Al crear una máquina virtual, están disponibles varias opciones, como la imagen de sistema operativo, tamaño de disco y credenciales administrativas. En este ejemplo, se crea una máquina virtual llamada *myVM* que se ejecuta en Ubuntu. 

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM --image UbuntuLTS --generate-ssh-keys
```

Una vez Hola que se ha creado la máquina virtual, Hola CLI de Azure genera información acerca de hello VM. Tome nota de hello `publicIpAddress`, esta dirección puede ser una máquina virtual de tooaccess usado Hola... 

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroupVM/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroupVM"
}
```

## <a name="connect-toovm"></a>Conectar tooVM

Ahora puede conectarse toohello VM mediante SSH. Reemplace la dirección IP de ejemplo de Hola con hello `publicIpAddress` anotó en el paso anterior de Hola.

```bash
ssh 52.174.34.95
```

Una vez finalizado con hello VM, cierre la sesión de SSH de Hola. 

```bash
exit
```

## <a name="understand-vm-images"></a>Descripción de las imágenes de máquina virtual

Hello Azure marketplace incluye muchas imágenes que pueden ser utilizados toocreate las máquinas virtuales. En los pasos anteriores de hello, una máquina virtual se creó con una imagen de Ubuntu. En este paso, Hola que CLI de Azure es marketplace de hello toosearch usado para una imagen de CentOS, que es, a continuación, utiliza toodeploy una segunda máquina virtual.  

toosee una lista de hello suelen usarse imágenes, use hello [lista de imágenes de máquina virtual de az](/cli/azure/vm/image#list) comando.

```azurecli-interactive 
az vm image list --output table
```

resultado del comando Hello devuelve imágenes de máquina virtual más populares de hello en Azure.

```bash
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
WindowsServer  MicrosoftWindowsServer  2016-Datacenter     MicrosoftWindowsServer:WindowsServer:2016-Datacenter:latest     Win2016Datacenter    latest
WindowsServer  MicrosoftWindowsServer  2012-R2-Datacenter  MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest  Win2012R2Datacenter  latest
WindowsServer  MicrosoftWindowsServer  2008-R2-SP1         MicrosoftWindowsServer:WindowsServer:2008-R2-SP1:latest         Win2008R2SP1         latest
WindowsServer  MicrosoftWindowsServer  2012-Datacenter     MicrosoftWindowsServer:WindowsServer:2012-Datacenter:latest     Win2012Datacenter    latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
```

Puede ver una lista completa mediante la adición de hello `--all` argumento. También se puede filtrar la lista de imágenes de Hola por `--publisher` o `–-offer`. En este ejemplo, se filtra la lista de Hola para todas las imágenes con una oferta que coincida con *CentOS*. 

```azurecli-interactive 
az vm image list --offer CentOS --all --output table
```

Salida parcial:

```azurecli-interactive 
Offer             Publisher         Sku   Urn                                     Version
----------------  ----------------  ----  --------------------------------------  -----------
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201501         6.5.201501
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201503         6.5.201503
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201506         6.5.201506
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20150904       6.5.20150904
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20160309       6.5.20160309
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20170207       6.5.20170207
```

toodeploy una máquina virtual mediante una imagen específica, tome nota del valor de hello en hello *Urn* columna. Al especificar la imagen de hello, número de versión de imagen de hello puede reemplazarse con "más reciente", que selecciona la versión más reciente de Hola de distribución de Hola. En este ejemplo, Hola `--image` argumento es la versión más reciente de hello toospecify utilizadas de una imagen de CentOS 6.5.  

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM2 --image OpenLogic:CentOS:6.5:latest --generate-ssh-keys
```

## <a name="understand-vm-sizes"></a>Comprensión de los tamaños de máquina virtual

Un tamaño de máquina virtual determina la cantidad de Hola de recursos de proceso, como CPU y GPU, memoria que se realizan la máquina virtual de toohello disponible. Máquinas virtuales deben toobe el tamaño adecuado para la carga de trabajo de hello esperado. Si aumenta la carga de trabajo, se puede cambiar el tamaño de una máquina virtual existente.

### <a name="vm-sizes"></a>Tamaños de máquina virtual

Hello en la tabla siguiente clasifica tamaños en casos de uso.  

| Tipo                     | Tamaños           |    Descripción       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [Uso general](sizes-general.md)         |Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7| Uso equilibrado de CPU y memoria. Ideal para desarrollo / pruebas y las soluciones de aplicaciones y datos de toomedium pequeños.  |
| [Proceso optimizado](sizes-compute.md)   | Fs, F             | Uso elevado de la CPU respecto a la memoria. Adecuado para aplicaciones, dispositivos de red y procesos por lotes con tráfico mediano.        |
| [Memoria optimizada](../virtual-machines-windows-sizes-memory.md)    | Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D   | Uso elevado de memoria respecto al núcleo. Muy bien para bases de datos relacionales, las cachés de toolarge intermedio y análisis en memoria.                 |
| [Almacenamiento optimizado](../virtual-machines-windows-sizes-storage.md)      | LS                | Alto rendimiento de disco y E/S. Perfecto para bases de datos SQL y NoSQL y macrodatos.                                                         |
| [GPU](sizes-gpu.md)          | NV, NC            | Máquinas virtuales especializadas específicas para actividades intensas de representación de gráficos y edición de vídeo.       |
| [Alto rendimiento](sizes-hpc.md) | H, A8-11          | Nuestras máquinas virtuales con CPU más eficaces e interfaces de red de alto rendimiento (RDMA) opcionales. 


### <a name="find-available-vm-sizes"></a>Búsqueda de los tamaños de máquina virtual disponibles

toosee una lista de la máquina virtual los tamaños disponibles en una región determinada, use hello [tamaños de lista de máquinas virtuales az](/cli/azure/vm#list-sizes) comando. 

```azurecli-interactive 
az vm list-sizes --location eastus --output table
```

Salida parcial:

```azurecli-interactive 
  MaxDataDiskCount    MemoryInMb  Name                      NumberOfCores    OsDiskSizeInMb    ResourceDiskSizeInMb
------------------  ------------  ----------------------  ---------------  ----------------  ----------------------
                 2          3584  Standard_DS1                          1           1047552                    7168
                 4          7168  Standard_DS2                          2           1047552                   14336
                 8         14336  Standard_DS3                          4           1047552                   28672
                16         28672  Standard_DS4                          8           1047552                   57344
                 4         14336  Standard_DS11                         2           1047552                   28672
                 8         28672  Standard_DS12                         4           1047552                   57344
                16         57344  Standard_DS13                         8           1047552                  114688
                32        114688  Standard_DS14                        16           1047552                  229376
                 1           768  Standard_A0                           1           1047552                   20480
                 2          1792  Standard_A1                           1           1047552                   71680
                 4          3584  Standard_A2                           2           1047552                  138240
                 8          7168  Standard_A3                           4           1047552                  291840
                 4         14336  Standard_A5                           2           1047552                  138240
                16         14336  Standard_A4                           8           1047552                  619520
                 8         28672  Standard_A6                           4           1047552                  291840
                16         57344  Standard_A7                           8           1047552                  619520
```

### <a name="create-vm-with-specific-size"></a>Creación de máquinas virtuales con un tamaño específico

En el ejemplo de creación de VM anterior hello, un tamaño no se proporcionó, lo que produce un tamaño predeterminado. Se puede seleccionar un tamaño de máquina virtual en el momento de creación utilizando [crear vm az](/cli/azure/vm#create) hello y `--size` argumento. 

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupVM \
    --name myVM3 \
    --image UbuntuLTS \
    --size Standard_F4s \
    --generate-ssh-keys
```

### <a name="resize-a-vm"></a>Cambiar el tamaño de una máquina virtual

Una vez implementada una máquina virtual, puede tooincrease cuyo tamaño ha cambiado o reducir la asignación de recursos.

Antes de cambiar el tamaño de una máquina virtual, compruebe si hello tamaño deseado está disponible en el clúster de Azure actual Hola. Hola [lista de vm az-vm-resize-options](/cli/azure/vm#list-vm-resize-options) comando devuelve la lista de tamaños de Hola. 

```azurecli-interactive 
az vm list-vm-resize-options --resource-group myResourceGroupVM --name myVM --query [].name
```
Si Hola deseado tamaño está disponible, hello VM puede cambiarse desde un estado encendido, sin embargo, se reinicia durante la operación de Hola. Hola de uso [cambiar el tamaño de vm az]( /cli/azure/vm#resize) comando tooperform Hola resize.

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_DS4_v2
```

Si Hola tamaño deseado no está en el clúster actual hello, Hola VM necesidades puede producirse toobe cancela la asignación antes de hello cambiar el tamaño de operación. Hola de uso [cancelar la asignación de máquina virtual az]( /cli/azure/vm#deallocate) comando toostop y cancelar la asignación Hola máquina virtual. Tenga en cuenta que cuando hello máquina virtual está encendida volver, desaparecerán todos los datos en disco temporal de Hola. dirección IP pública de Hello también cambia a menos que se está usando una dirección IP estática. 

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupVM --name myVM
```

Una vez cancelada la asignación, puede producirse el cambio de tamaño de Hola. 

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_GS1
```

Después de cambiar el tamaño de hello, Hola VM se puede iniciar.

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

## <a name="vm-power-states"></a>Estados de una máquina virtual

Una máquina virtual de Azure puede tener uno de muchos estados de energía. Este estado representa estado actual de Hola de hello VM desde la perspectiva de Hola de hipervisor de Hola. 

### <a name="power-states"></a>Estados de energía

| Estado de energía | Descripción
|----|----|
| Iniciando | Indica que se está iniciando la máquina virtual de Hola. |
| En ejecución | Indica que la máquina virtual Hola se está ejecutando. |
| Deteniéndose | Indica que la máquina virtual Hola se está deteniendo. | 
| Stopped | Indica que la máquina virtual Hola se ha detenido. Máquinas virtuales en estado de hello detenido sigue acumulando cargos de proceso.  |
| Desasignando | Indica que la máquina virtual Hola se está desasignando. |
| Desasignado | Indica que la máquina virtual Hola está quitarse de hipervisor de hello pero seguirá estando disponible en el plano de control de Hola. Máquinas virtuales en estado desasignado hello no acumulando cargos de proceso. |
| - | Indica que el estado de energía de Hola de máquina virtual de hello es desconocido. |

### <a name="find-power-state"></a>Búsqueda del estado de una máquina virtual

estado de hello tooretrieve de una máquina virtual concreta, use hello [az vm obtener vista de instancia](/cli/azure/vm#get-instance-view) comando. Ser seguro toospecify un nombre válido para una máquina virtual y el grupo de recursos. 

```azurecli-interactive 
az vm get-instance-view \
    --name myVM \
    --resource-group myResourceGroupVM \
    --query instanceView.statuses[1] --output table
```

Salida:

```azurecli-interactive 
ode                DisplayStatus    Level
------------------  ---------------  -------
PowerState/running  VM running       Info
```

## <a name="management-tasks"></a>Tareas de administración

Durante el ciclo de vida Hola de una máquina virtual, puede desear toorun tareas de administración, como iniciar, detener o eliminar una máquina virtual. Además, puede que desee toocreate tooautomate repetitivas o complejas tareas de secuencias de comandos. Con hello CLI de Azure, muchas tareas comunes de administración se pueden ejecutar desde la línea de comandos de Hola o en scripts. 

### <a name="get-ip-address"></a>Obtención de dirección IP

Este comando devuelve las direcciones IP de hello públicas y privadas de una máquina virtual.  

```azurecli-interactive 
az vm list-ip-addresses --resource-group myResourceGroupVM --name myVM --output table
```

### <a name="stop-virtual-machine"></a>Detener una máquina virtual

```azurecli-interactive 
az vm stop --resource-group myResourceGroupVM --name myVM
```

### <a name="start-virtual-machine"></a>Iniciar una máquina virtual

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

### <a name="delete-resource-group"></a>Eliminación de un grupo de recursos

Al eliminar un grupo de recursos se eliminan también todos los recursos contenidos en el mismo.

```azurecli-interactive 
az group delete --name myResourceGroupVM --no-wait --yes
```

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido conceptos básicos sobre la creación y administración de máquinas virtuales. Por ejemplo:

> [!div class="checklist"]
> * Crear y conectar tooa VM
> * Seleccionar y usar imágenes de máquinas virtuales
> * Ver y usar tamaños de una máquina virtual específicos
> * Cambiar el tamaño de una máquina virtual
> * Ver y entender el estado de las máquinas virtuales

Avanzar toohello toolearn de tutorial siguiente acerca de los discos de máquina virtual.  

> [!div class="nextstepaction"]
> [Creación y administración de discos de máquinas virtuales](./tutorial-manage-disks.md)
