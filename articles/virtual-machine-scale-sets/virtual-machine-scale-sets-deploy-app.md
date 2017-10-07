---
title: "establece aaaDeploy una aplicación en la escala de máquinas virtuales"
description: "Utilizar extensiones toodepoy una aplicación en conjuntos de escalas de máquina Virtual de Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8892199-f2e2-4b82-988a-28ca8a7fd1eb
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: 5f3988b9511d80370a8be1fc042c21fee212506e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-application-on-virtual-machine-scale-sets"></a>Implementación de la aplicación en conjuntos de escalado de máquinas virtuales

Este artículo describen distintas formas de cómo establece el software tooinstall de escala de tiempo del Hola Hola se aprovisionó.

Puede que desee hello tooreview [Introducción al diseño de conjunto escala](virtual-machine-scale-sets-design-overview.md) artículo, que se describe algunos de los límites de hello impuestos por conjuntos de escalas de máquina virtual.

## <a name="capture-and-reuse-an-image"></a>Captura y reutilización de una imagen

Puede usar una máquina virtual que en Azure tooprepare una imagen base para la escala estableciste. Este proceso crea un disco administrado en su cuenta de almacenamiento, que puede hacer referencia como imagen base hello para el conjunto de escala. 

Hola lo siguiente:

1. Cree una máquina virtual de Azure.
   * [Linux][linux-vm-create]
   * [Windows][windows-vm-create]

2. Remoto en Hola máquina virtual y personalizar gusto de tooyour de sistema de Hola.

   Si quiere, puede instalar la aplicación ahora. Sin embargo, saber que al instalar la aplicación ahora, puede realizar actualización de la aplicación más complicada porque puede que necesite tooremove primero. En su lugar, puede usar este paso tooinstall todos los requisitos previos que necesita la aplicación, como una característica específica de sistema operativo o en tiempo de ejecución.

3. Siga Hola "capturar una máquina" tutorial para cualquiera [Linux] [ linux-vm-capture] o [Windows][windows-vm-capture].

4. Crear un [conjunto de escala de máquinas virtuales] [ vmss-create] con hello imagen URI se capturó en el paso anterior de Hola.

Para obtener más información sobre los discos, consulte [Información general de Managed Disks](../virtual-machines/windows/managed-disks-overview.md) y [Uso de datos de discos conectados](virtual-machine-scale-sets-attached-disks.md).

## <a name="install-when-hello-scale-set-is-provisioned"></a>Instalar cuando se aprovisiona el conjunto de escalas de Hola

Las extensiones de máquina virtual se pueden aplicar tooa conjunto de escalas de máquina virtual. Con una extensión de máquina virtual, puede personalizar máquinas virtuales de hello en una escala establecida como un grupo entero. Para obtener más información sobre extensiones, consulte [Extensiones de máquinas virtuales](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Hay tres extensiones principales que puede usar en función de si el sistema operativo está basado en Linux o Windows.

### <a name="windows"></a>Windows

Para un sistema operativo basado en Windows, use cualquier hello **Script personalizado v1.8** Hola o extensiones **PowerShell DSC** extensión.

#### <a name="custom-script"></a>Script personalizado

Hola extensión de Script personalizado ejecuta un script en cada instancia de máquina virtual en el conjunto de escalas de Hola. Un archivo de configuración o una variable indica qué archivos son la máquina virtual de toohello descargado y, a continuación, se ejecuta el comando. Por ejemplo se pudieron utilizar esta toorun un instalador, una secuencia de comandos, un archivo por lotes, cualquier archivo ejecutable.

PowerShell utiliza una tabla hash para los valores de hello. Este ejemplo configura toorun de extensión de script personalizado de hello un script de PowerShell que se instala IIS.

```powershell
# Setup extension configuration hashtable variable
$customConfig = @{
  "fileUris" = @("https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1");
  "commandToExecute" = "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> `"%TEMP%\StartupLog.txt`" 2>&1";
};

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Compute -Type CustomScriptExtension -TypeHandlerVersion 1.8 -Name "customscript1" -Setting $customConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "MyVmssTest143"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
>Hola de uso `-ProtectedSetting` cambie para cualquier configuración que puede contener información confidencial.

---------


CLI de Azure utiliza un archivo json para valores de hello. Este ejemplo configura toorun de extensión de script personalizado de hello un script de PowerShell que se instala IIS. Guardar Hola siguiente archivo de json como _settings.json_.

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1"
  ],
  "commandToExecute": "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> \"%TEMP%\StartupLog.txt\" 2>&1"
}
```

A continuación, ejecute este comando de CLI de Azure.

```azurecli
az vmss extension set --publisher Microsoft.Compute --version 1.8 --name CustomScriptExtension --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
>Hola de uso `--protected-settings` cambie para cualquier configuración que puede contener información confidencial.

### <a name="powershell-dsc"></a>PowerShell DSC

Puede usar instancias de vm de conjunto de escala de DSC de PowerShell toocustomize Hola. Hola **DSC** extensión publicada por **Microsoft.Powershell** implementa y ejecuta la configuración de DSC de hello proporcionado en cada instancia de máquina virtual. Un archivo de configuración o una variable indica extensión Hola donde *.zip* es el paquete y que _función de script_ toorun de combinación.

PowerShell utiliza una tabla hash para los valores de hello. En este ejemplo se implementa un paquete DSC que instala IIS.

```powershell
# Setup extension configuration hashtable variable
$dscConfig = @{
  "wmfVersion" = "latest";
  "configuration" = @{
    "url" = "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip";
    "script" = "configure-http.ps1";
    "function" = "WebsiteTest";
  };
}

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Powershell -Type DSC -TypeHandlerVersion 2.24 -Name "dsc1" -Setting $dscConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "myscaleset1"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
>Hola de uso `-ProtectedSetting` cambie para cualquier configuración que puede contener información confidencial.

-----------

CLI de Azure usa json para la configuración de Hola. En este ejemplo se implementa un paquete DSC que instala IIS. Guardar Hola siguiente archivo de json como _settings.json_.

```json
{
  "wmfVersion": "latest",
  "configuration": {
    "url": "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip",
    "script": "configure-http.ps1",
    "function": "WebsiteTest"
  }
}
```

A continuación, ejecute este comando de CLI de Azure.

```azurecli
az vmss extension set --publisher Microsoft.Powershell --version 2.24 --name DSC --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
>Hola de uso `--protected-settings` cambie para cualquier configuración que puede contener información confidencial.

### <a name="linux"></a>Linux

Linux puede usar cualquier hello **v2.0 de Script personalizado** extensión o use **init de la nube** durante la creación.

Secuencia de comandos personalizada es una extensión simple que descarga las instancias de máquina virtual de toohello de archivos y se ejecuta un comando.

#### <a name="custom-script"></a>Script personalizado

Guardar Hola siguiente archivo de json como _settings.json_.

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
  ],
  "commandToExecute": "bash installserver.sh"
}
```

Utilice hello Azure CLI tooadd esta tooan de extensión existente de conjunto de escalas de máquina virtual. Cada máquina virtual en la escala de hello establecen automáticamente se ejecuta Hola extensión.

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
>Hola de uso `--protected-settings` cambie para cualquier configuración que puede contener información confidencial.

#### <a name="cloud-init"></a>Cloud-Init

En la nube Init se utiliza cuando se crea el conjunto de escalas de Hola. En primer lugar, cree un archivo local denominado _init.txt nube_ y agregue su tooit de configuración. Por ejemplo, consulte [este gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt).

Establece Hola uso toocreate una escala de CLI de Azure. Hola `--custom-data` campo acepta el nombre de archivo de Hola de una secuencia de comandos init de la nube.

```azurecli
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image Canonical:UbuntuServer:14.04.4-LTS:latest \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

## <a name="how-do-i-manage-application-updates"></a>Instrucciones de administración de actualizaciones de aplicaciones

Si ha implementado la aplicación a través de una extensión, modifique la definición de extensión de Hola de alguna manera. Este cambio hace que las instancias de máquina virtual de hello extensión toobe volver a implementar tooall. Algo **debe** cambiarse acerca de la extensión de hello, como cambiar el nombre de un archivo que se hace referencia, en caso contrario, Azure hace que no vería que Hola extensión ha cambiado.

Si incrustadas aplicación hello en su propia imagen de sistema operativo, use una canalización de implementación automatizada de actualizaciones de la aplicación. Diseñar su toofacilitate arquitectura rápido de intercambio de una escala de ensayada se ha establecido en producción. Un buen ejemplo de este enfoque es hello [trabajo de controlador de Azure Spinnaker](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).

[Compresor](https://www.packer.io/) y [Terraform](https://www.terraform.io/) soporte técnico de Azure Resource Manager, por lo que también puede definir las imágenes "como código" y compilarlos en Azure, a continuación, use Hola VHD en el conjunto de escala. Sin embargo, hacerlo así sería problemático para las imágenes de marketplace, donde los scripts de extensiones o los personalizados se vuelven más importantes ya que no manipula directamente los bits de marketplace.

## <a name="what-happens-when-a-scale-set-scales-out"></a>¿Qué pasa cuando un conjunto de escalado escala horizontalmente?
Al agregar uno o más el conjunto de escala de máquinas virtuales tooa, se instala automáticamente la aplicación hello. Para el ejemplo se si establece la escala de hello tiene extensiones definidas, en una nueva máquina virtual ejecute cada vez que se crea. Si el conjunto de escalas de Hola se basa en una imagen personalizada, cualquier nueva máquina virtual es una copia de la imagen personalizada del origen de Hola. Si las máquinas virtuales conjunto Hola escala son hosts de contenedor, tendrá contenedores de Hola de tooload de código de inicio en una extensión de Script personalizado. O bien podría haber una extensión que instalara un agente que se registre con un orquestador de clúster, como Azure Container Service.


## <a name="how-do-you-roll-out-an-os-update-across-update-domains"></a>¿Cómo aplicar una actualización de sistema operativo a través de dominios de actualización?
Imagine que desea tooupdate la imagen del SO manteniendo escalas de máquina virtual de hello establecer ejecutando. Hello Azure CLI y PowerShell pueden actualizar las imágenes de máquina virtual de hello, una máquina virtual a la vez. Hola [actualizar un conjunto de escala de máquinas virtuales](./virtual-machine-scale-sets-upgrade-scale-set.md) artículo también proporciona información adicional sobre qué opciones están disponible tooperform actualizar un sistema operativo a través de un conjunto de escalas de máquina virtual.

## <a name="next-steps"></a>Pasos siguientes

* [Usar PowerShell toomanage el conjunto de escala.](virtual-machine-scale-sets-windows-manage.md)
* [Creación de una plantilla de conjunto de escalado](virtual-machine-scale-sets-mvss-start.md).


[linux-vm-create]: ../virtual-machines/linux/tutorial-manage-vm.md
[windows-vm-create]: ../virtual-machines/windows/tutorial-manage-vm.md
[linux-vm-capture]: ../virtual-machines/linux/capture-image.md
[windows-vm-capture]: ../virtual-machines/windows/capture-image.md 
[vmss-create]: virtual-machine-scale-sets-create.md

