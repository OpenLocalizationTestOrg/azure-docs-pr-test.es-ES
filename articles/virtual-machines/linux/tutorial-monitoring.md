---
title: "máquinas virtuales de Linux aaaMonitor en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomonitor arrancar las métricas de rendimiento y diagnóstico en una máquina virtual de Linux en Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 282da0f03ab0bf37bd44750c22813ca8d1c89560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-a-linux-virtual-machine-in-azure"></a>¿Cómo toomonitor una máquina virtual de Linux en Azure

tooensure que las máquinas virtuales (VM) en Azure se ejecuta correctamente, puede revisar las métricas de rendimiento y diagnóstico de arranque. En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Habilitar los diagnósticos de arranque en hello VM
> * Ver los diagnósticos de arranque
> * Visualización de las métricas del host
> * Habilitar la extensión de diagnósticos en hello VM
> * Ver las métricas de la máquina virtual
> * Crear alertas basadas en métricas de diagnóstico
> * Configurar la supervisión avanzada


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-vm"></a>Creación de una máquina virtual

toosee diagnósticos y las métricas en acción, necesita una máquina virtual. En primer lugar, cree un grupo de recursos con [az group create](/cli/azure/group#create). Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroupMonitor* en hello *eastus* ubicación.

```azurecli-interactive 
az group create --name myResourceGroupMonitor --location eastus
```

Ahora cree una máquina virtual con el comando [az vm create](https://docs.microsoft.com/cli/azure/vm#create). Hello en el ejemplo siguiente se crea una máquina virtual denominada *myVM*:

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

## <a name="enable-boot-diagnostics"></a>Habilitación de los diagnósticos de arranque

Como el arranque de máquinas virtuales de Linux, extensión de diagnóstico de arranque de hello captura el resultado de arranque y lo almacena en el almacenamiento de Azure. Estos datos pueden ser utilizados tootroubleshoot de problemas de inicio de máquina virtual. Diagnóstico de arranque no se habilita automáticamente cuando se crea una VM de Linux con hello CLI de Azure.

Antes de habilitar el diagnóstico de arranque, una cuenta de almacenamiento debe toobe creado para almacenar archivos de registro de arranque. Las cuentas de almacenamiento deben tener un nombre único global, tener entre 3 y 24 caracteres, y deben contener solo números y letras en minúscula. Crear una cuenta de almacenamiento con hello [crear cuenta de almacenamiento az](/cli/azure/storage/account#create) comando. En este ejemplo, una cadena aleatoria es toocreate usa un nombre de cuenta de almacenamiento único. 

```azurecli-interactive 
storageacct=mydiagdata$RANDOM

az storage account create \
  --resource-group myResourceGroupMonitor \
  --name $storageacct \
  --sku Standard_LRS \
  --location eastus
```

Al habilitar el diagnóstico de arranque, se necesita el contenedor de almacenamiento de blobs de hello URI toohello. Hello las consultas del comando siguiente Hola tooreturn de cuenta de almacenamiento este URI. Hola valor URI se almacena en los nombres de variable *bloburi*, que se usa en el paso siguiente de saludo.

```azurecli-interactive 
bloburi=$(az storage account show --resource-group myResourceGroupMonitor --name $storageacct --query 'primaryEndpoints.blob' -o tsv)
```

Habilite ahora los diagnósticos de arranque con [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable). Hola `--storage` valor es blob Hola URI recopilado en el paso anterior de Hola.

```azurecli-interactive 
az vm boot-diagnostics enable \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --storage $bloburi
```


## <a name="view-boot-diagnostics"></a>Ver los diagnósticos de arranque

Cuando se habilitan los diagnósticos de arranque, cada vez que detiene e inicia Hola VM, información sobre el proceso de arranque de Hola se escribe tooa archivo de registro. En este ejemplo, en primer lugar desasignar Hola VM con hello [cancelar la asignación de máquina virtual az](/cli/azure/vm#deallocate) comando como sigue:

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupMonitor --name myVM
```

Iniciar ahora Hola VM con hello [inicio de vm az]( /cli/azure/vm#stop) comando como sigue:

```azurecli-interactive 
az vm start --resource-group myResourceGroupMonitor --name myVM
```

Puede obtener datos de diagnóstico de arranque de Hola para *myVM* con hello [diagnóstico de arranque de vm az get-arranque-log](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) comando como sigue:

```azurecli-interactive 
az vm boot-diagnostics get-boot-log --resource-group myResourceGroupMonitor --name myVM
```


## <a name="view-host-metrics"></a>Visualización de las métricas del host

Una máquina virtual Linux tiene un host dedicado de Azure que interactúa con. Las métricas se recopilan automáticamente para el host de Hola y pueden verse en hello portal de Azure como sigue:

1. Hola portal de Azure, haga clic en **grupos de recursos**, seleccione **myResourceGroupMonitor**y, a continuación, seleccione **myVM** en la lista de recursos de Hola.
1. toosee cómo está realizando la máquina virtual del host de hello, haga clic en **métricas** en la hoja de la máquina virtual de hello, a continuación, seleccione cualquiera de hello *[Host]* métricas en **métricas disponibles**.

    ![Visualización de las métricas del host](./media/tutorial-monitoring/monitor-host-metrics.png)


## <a name="install-diagnostics-extension"></a>Instalar la extensión de Diagnostics

> [!IMPORTANT]
> Este documento describe la versión 2.3 de hello extensión de diagnóstico de Linux, que está en desuso. Se admitirá la versión 2.3 hasta el 30 de junio de 2018.
>
> Versión 3.0 de hello que extensión de diagnóstico de Linux pueden habilitarse en su lugar. Para obtener más información, consulte [Hola documentación](./diagnostic-extension.md).

métricas de host básica Hello están disponibles, pero toosee más granular y métricas específica de la máquina virtual, se tooneed tooinstall hello Azure extensión de diagnósticos en hello VM. Hola extensión de diagnósticos de Azure permite toobe de datos de diagnóstico recuperados de hello VM y supervisión adicional. Puede ver estas métricas de rendimiento y crear alertas basadas en cómo realiza Hola máquina virtual. extensión de diagnóstico de Hola se instala a través de hello portal de Azure como sigue:

1. Hola portal de Azure, haga clic en **grupos de recursos**, seleccione **myResourceGroup**y, a continuación, seleccione **myVM** en la lista de recursos de Hola.
1. Haga clic en **Configuración de diagnóstico**. lista de Hello muestra que *diagnósticos de arranque* ya están habilitados desde la sección anterior de Hola. Haga clic en la casilla de verificación hello *métricas básicas*.
1. Hola *cuenta de almacenamiento* sección, examinar Hola seleccione tooand *mydiagdata [1234]* cuenta creada en la sección anterior de Hola.
1. Haga clic en hello **guardar** botón.

    ![Ver métricas de diagnósticos](./media/tutorial-monitoring/enable-diagnostics-extension.png)


## <a name="view-vm-metrics"></a>Ver las métricas de la máquina virtual

Puede ver las métricas de máquina virtual de Hola Hola igual que ver las métricas de máquina virtual de host de hello:

1. Hola portal de Azure, haga clic en **grupos de recursos**, seleccione **myResourceGroup**y, a continuación, seleccione **myVM** en la lista de recursos de Hola.
1. toosee cómo está realizando Hola VM, haga clic en **métricas** en Hola hoja de la máquina virtual y, a continuación, seleccione cualquiera de las métricas de diagnóstico de hello en **métricas disponibles**.

    ![Ver las métricas de la máquina virtual](./media/tutorial-monitoring/monitor-vm-metrics.png)


## <a name="create-alerts"></a>Creación de alertas

Puede crear alertas basadas en métricas de rendimiento concretas. Las alertas pueden ser usado toonotify cuando uso medio de CPU supera un determinado umbral o espacio en disco disponible cae por debajo de una determinada cantidad, por ejemplo. Las alertas se muestran en el portal de Azure de Hola o se pueden enviar por correo electrónico. También puede desencadenar runbooks de automatización de Azure o las aplicaciones lógicas de Azure en tooalerts de respuesta que se está generando.

Hello en el ejemplo siguiente se crea una alerta para el uso medio de CPU.

1. Hola portal de Azure, haga clic en **grupos de recursos**, seleccione **myResourceGroup**y, a continuación, seleccione **myVM** en la lista de recursos de Hola.
2. Haga clic en **reglas de alerta** en la hoja de la máquina virtual de hello, a continuación, haga clic en **Agregar alerta métrica** a través de la parte superior de Hola de hoja de alertas de Hola.
4. Especifique un **nombre** para la alerta, como *myAlertRule*.
5. tootrigger una alerta cuando el porcentaje de CPU supera 1.0 durante cinco minutos, deje Hola todos los demás valores predeterminados seleccionados.
6. Si lo desea, active casilla de Hola para *correo electrónico a los propietarios, contributors y readers* toosend notificación de correo electrónico. acción predeterminada de Hello es toopresent una notificación en el portal de Hola.
7. Haga clic en hello **Aceptar** botón.


## <a name="advanced-monitoring"></a>Supervisión avanzada 

Mediante [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) se puede realizar una supervisión más avanzada de la máquina virtual. Si aún no lo ha hecho, puede suscribirse para disfrutar de una [evaluación gratuita](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) de Operations Management Suite.

Cuando se tiene acceso toohello OMS portal, puede encontrar identificador de clave y el área de trabajo del área de trabajo de hello en la hoja de configuración de Hola. Reemplace < clave de área de trabajo > y < Id. de área de trabajo > con valores de hello para de la OMS puede usar el área de trabajo y, a continuación, **conjunto de extensión de vm az** tooadd Hola OMS extensión toohello VM:

```azurecli-interactive 
az vm extension set \
  --resource-group myResourceGroupMonitor \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.3 \
  --protected-settings '{"workspaceKey": "<workspace-key>"}' \
  --settings '{"workspaceId": "<workspace-id>"}'
```

En la hoja de búsqueda de registros de Hola de portal de OMS hello, debería ver *myVM* como lo que se muestra en hello después de imagen:

![Hoja OMS](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha configurado y revisado las máquinas virtuales con Azure Security Center. Ha aprendido a:

> [!div class="checklist"]
> * Habilitar los diagnósticos de arranque en hello VM
> * Ver los diagnósticos de arranque
> * Visualización de las métricas del host
> * Habilitar la extensión de diagnósticos en hello VM
> * Ver las métricas de la máquina virtual
> * Crear alertas basadas en métricas de diagnóstico
> * Configurar la supervisión avanzada

Avanzar toohello siguiente toolearn de tutorial acerca del centro de seguridad de Azure.

> [!div class="nextstepaction"]
> [Administración de la seguridad de máquinas virtuales](./tutorial-azure-security.md)