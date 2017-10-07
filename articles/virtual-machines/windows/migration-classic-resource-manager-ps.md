---
title: aaaMigrate tooResource Manager con PowerShell | Documentos de Microsoft
description: "Este artículo le guía a través de migración de hello admitida por la plataforma de recursos de IaaS, como máquinas virtuales (VM) y redes virtuales (Vnet), las cuentas de almacenamiento de tooAzure clásico Resource Manager (ARM) mediante el uso de comandos de PowerShell de Azure"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2b3dff9b-2e99-4556-acc5-d75ef234af9c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: b5b2987da292f1c241be71a354b0c2e1a96a07c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-powershell"></a>Migrar recursos de IaaS de tooAzure clásico Administrador de recursos mediante el uso de PowerShell de Azure
Estos pasos muestra cómo toouse Azure PowerShell comandos toomigrate infraestructura como un recurso de servicio (IaaS) de modelo de implementación de Azure Resource Manager de toohello modelo de implementación clásica de Hola.

Si lo desea, también puede migrar recursos mediante el uso de hello [interfaz de línea de comandos de Azure (Azure CLI)](../linux/migration-classic-resource-manager-cli.md).

* Para obtener información sobre escenarios de migración admitidos, consulte [admitida por la plataforma de la migración de los recursos de IaaS de tooAzure clásico Administrador de recursos](migration-classic-resource-manager-overview.md).
* Para obtener instrucciones detalladas y una guía de migración, consulte [técnica exhaustiva sobre la migración admitida por la plataforma de tooAzure clásico Administrador de recursos](migration-classic-resource-manager-deep-dive.md).
* [Revisión de los errores más comunes en la migración](migration-classic-resource-manager-errors.md)

<br>
Este es un orden de hello tooidentify de diagrama de flujo en el que es necesario pasos toobe ejecutado durante un proceso de migración

![Captura de pantalla que muestra los pasos de migración de Hola](media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-plan-for-migration"></a>Paso 1: Planear la migración
Estas son algunas prácticas recomendadas que se recomienda evaluar migrar recursos de IaaS de tooResource clásico Manager:

* Lea hello [admiten y cuáles no características y configuraciones](migration-classic-resource-manager-overview.md). Si tiene máquinas virtuales que usan configuraciones no admitidas o características, se recomienda que espere Hola configuración o característica Compatibilidad con toobe anunciado. O bien, si se adapte a sus necesidades, quitar esa característica o salir de que la migración de configuración tooenable.
* Si han automatizado las secuencias de comandos que implementan la infraestructura y las aplicaciones de hoy en día, intente toocreate un programa de instalación de prueba similar con esos scripts para la migración. Como alternativa, puede configurar entornos de ejemplo mediante el uso de hello portal de Azure.

> [!IMPORTANT]
> Las puertas de enlace de la aplicación no se admiten actualmente para la migración de clásico tooResource Manager. toomigrate una red virtual clásica con una puerta de enlace de aplicaciones, quitar la puerta de enlace de hello antes de ejecutar una red de Hola de toomove de operación de preparación. Después de completar la migración de hello, vuelva a conectar la puerta de enlace de hello en el Administrador de recursos de Azure.
>
>Conectar los circuitos tooExpressRoute en otra suscripción de puertas de enlace de ExpressRoute no se pueden migrar automáticamente. En tales casos, quite la puerta de enlace de ExpressRoute de hello, migrar la red virtual de Hola y vuelva a puerta de enlace de Hola. Vea [ExpressRoute migrar circuitos y asociado redes virtuales de modelo de implementación de administrador de recursos de hello toohello clásico](../../expressroute/expressroute-migration-classic-resource-manager.md) para obtener más información.
>
>

## <a name="step-2-install-hello-latest-version-of-azure-powershell"></a>Paso 2: Instalar la versión más reciente de Hola de PowerShell de Azure
Hay dos opciones principales tooinstall PowerShell de Azure: [Galería de PowerShell](https://www.powershellgallery.com/profiles/azure-sdk/) o [instalador de plataforma Web (WPI)](http://aka.ms/webpi-azps). WebPI recibe actualizaciones mensuales. La galería de PowerShell recibe actualizaciones de forma continua. Este artículo se basa en los cmdlets de la versión 2.1.0 de Azure PowerShell.

Para obtener instrucciones de instalación, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).

<br>

## <a name="step-3-ensure-that-you-are-an-administrator-for-hello-subscription-in-azure-portal"></a>Paso 3: Asegúrese de que un administrador para la suscripción de hello en el portal de Azure
tooperform esta migración, se debe agregar como Coadministrador de suscripción de Hola Hola [portal de Azure](https://portal.azure.com).

1. Inicio de sesión en hello [portal de Azure](https://portal.azure.com).
2. En el menú del concentrador hello, seleccione **suscripción**. Si no lo ve, haga clic en **Más servicios**.
3. Buscar entrada de suscripción adecuado de Hola y después examine hello **mi rol** campo. De un Coadministrador, debe ser el valor de hello _Administrador de la cuenta_.

Si no es capaz de tooadd un Coadministrador, a continuación, póngase en contacto con un administrador de servicios o Coadministrador para hello suscripción tooget usted mismo agregado.   

## <a name="step-4-set-your-subscription-and-sign-up-for-migration"></a>Paso 4: Establecimiento de la suscripción y registro para la migración
En primer lugar, inicie un símbolo del sistema de PowerShell. Para la migración, necesita tooset del entorno para ambos clásico y Administrador de recursos.

Inicie sesión en la cuenta de tooyour para el modelo de administrador de recursos de Hola.

```powershell
    Login-AzureRmAccount
```

Obtener suscripciones disponibles hello mediante Hola siguiente comando:

```powershell
    Get-AzureRMSubscription | Sort Name | Select Name
```

Establecer la suscripción de Azure para hello sesión actual. Este ejemplo establece Hola nombre de la suscripción predeterminada demasiado**mi suscripción de Azure**. Reemplace el nombre de suscripción de ejemplo de Hola por los suyos propios.

```powershell
    Select-AzureRmSubscription –SubscriptionName "My Azure Subscription"
```

> [!NOTE]
> El registro es un paso que solo se realiza una vez, pero debe hacerlo antes de intentar la migración. Sin registrar, vea Hola mensaje de error siguiente:
>
> *BadRequest: Subscription is not registered for migration* (BadRequest: la suscripción no está registrada para la migración)
>
>

Registrar con el proveedor de recursos de migración de hello mediante Hola siguiente comando:

```powershell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

Espere cinco minutos para toofinish de registro de hello. Puede comprobar el estado de Hola de aprobación de hello mediante el uso de hello siguiente comando:

```powershell
    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

Asegúrese de que RegistrationState sea `Registered` antes de continuar.

Ahora, inicie sesión en tooyour cuenta para el modelo clásico de Hola.

```powershell
    Add-AzureAccount
```

Obtener suscripciones disponibles hello mediante Hola siguiente comando:

```powershell
    Get-AzureSubscription | Sort SubscriptionName | Select SubscriptionName
```

Establecer la suscripción de Azure para hello sesión actual. Este ejemplo establece suscripción predeterminada de hello demasiado**mi suscripción de Azure**. Reemplace el nombre de suscripción de ejemplo de Hola por los suyos propios.

```powershell
    Select-AzureSubscription –SubscriptionName "My Azure Subscription"
```

<br>

## <a name="step-5-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a>Paso 5: Asegúrese de que tiene suficientes núcleos de máquina Virtual de Azure Resource Manager Hola región de Azure de su implementación actual o la red virtual
Puede usar Hola siguiente PowerShell comando toocheck Hola actual número de núcleos que tiene en el Administrador de recursos de Azure. toolearn más información acerca de las cuotas de núcleo, consulte [hello Azure Resource Manager y límites](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).

Este ejemplo comprueba la disponibilidad de Hola Hola **West US** región. Reemplace el nombre de región de ejemplo de Hola por los suyos propios.

```powershell
Get-AzureRmVMUsage -Location "West US"
```

## <a name="step-6-run-commands-toomigrate-your-iaas-resources"></a>Paso 6: Ejecutar comandos toomigrate los recursos de IaaS
> [!NOTE]
> Todas las operaciones de hello descritas aquí son idempotentes. Si tiene un problema que no sea una característica no compatible o un error de configuración, se recomienda que vuelva a intentar Hola preparar, anular o confirmar la operación. plataforma de Hello, a continuación, intenta volver a la acción de Hola.
>
>

## <a name="step-61-option-1---migrate-virtual-machines-in-a-cloud-service-not-in-a-virtual-network"></a>Paso 6.1: Opción 1: Migración de máquinas virtuales en un servicio en la nube (no en una red virtual)
Hola obtención de una lista de servicios en la nube mediante el uso de hello siguiente comando y, a continuación, servicio de nube de Hola de selección que desea toomigrate. Si hello las máquinas virtuales en el servicio de nube de Hola se encuentran en una red virtual o si tienen roles web o de trabajo, el comando de hello devuelve un mensaje de error.

```powershell
    Get-AzureService | ft Servicename
```

Obtener nombre de la implementación de Hola Hola servicio de nube. En este ejemplo, es el nombre del servicio de hello **mi servicio**. Reemplace el nombre de servicio de ejemplo de Hola con su propio nombre de servicio.

```powershell
    $serviceName = "My Service"
    $deployment = Get-AzureDeployment -ServiceName $serviceName
    $deploymentName = $deployment.DeploymentName
```

Preparar las máquinas virtuales de Hola Hola del servicio en nube para la migración. Tiene dos toochoose de opciones de.

* **Opción 1. Migrar la red virtual para crear plataforma tooa de máquinas virtuales Hola**

    En primer lugar, validar si puede migrar servicio en la nube hello mediante Hola siguientes comandos:

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    $validate.ValidationMessages
    ```

    Hello comando anterior muestra las advertencias y los errores que bloquear la migración. Si la validación es correcta, puede mover en toohello **preparar** paso:

    ```powershell
    Move-AzureService -Prepare -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    ```
* **Opción 2. Migrar tooan de red virtual existente en el modelo de implementación del Administrador de recursos de Hola**

    Este ejemplo establece Hola nombre del grupo de recursos demasiado**myResourceGroup**, Hola nombre de red virtual demasiado**myVirtualNetwork** y Hola nombre de subred demasiado**mySubNet**. Reemplazar nombres de hello en el ejemplo de Hola con nombres Hola de sus propios recursos.

    ```powershell
    $existingVnetRGName = "myResourceGroup"
    $vnetName = "myVirtualNetwork"
    $subnetName = "mySubNet"
    ```

    En primer lugar, validar si se puede migrar la red virtual de hello con hello siguiente comando:

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName -VirtualNetworkName $vnetName -SubnetName $subnetName
    $validate.ValidationMessages
    ```

    Hello comando anterior muestra las advertencias y los errores que bloquear la migración. Si la validación es correcta, puede continuar con hello siguiendo el paso de preparación:

    ```powershell
        Move-AzureService -Prepare -ServiceName $serviceName -DeploymentName $deploymentName `
        -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName `
        -VirtualNetworkName $vnetName -SubnetName $subnetName
    ```

Después de hello operación de preparación se realiza correctamente con cualquiera de hello anterior opciones, consultar el estado de migración de Hola de hello las máquinas virtuales. Asegúrese de que se encuentran en hello `Prepared` estado.

Este ejemplo establece Hola nombre de máquina virtual demasiado**myVM**. Reemplace el nombre de ejemplo de Hola con su propio nombre de máquina virtual.

```powershell
    $vmName = "myVM"
    $vm = Get-AzureVM -ServiceName $serviceName -Name $vmName
    $vm.VM.MigrationState
```

Comprobar la configuración de Hola para hello preparado recursos con PowerShell u Hola portal de Azure. Si no está listo para la migración y desea que el estado anterior de toogo toohello atrás, use Hola siguiente comando:

```powershell
    Move-AzureService -Abort -ServiceName $serviceName -DeploymentName $deploymentName
```

Si configuración preparada hello es correcto, puede desplazarse hacia delante y confirmar recursos Hola usando el siguiente comando de hello:

```powershell
    Move-AzureService -Commit -ServiceName $serviceName -DeploymentName $deploymentName
```

## <a name="step-61-option-2---migrate-virtual-machines-in-a-virtual-network"></a>Paso 6.1: Opción 2: Migración de máquinas virtuales en una red virtual

toomigrate las máquinas virtuales en una red virtual, se migra la red virtual de Hola. máquinas virtuales de Hello migrar automáticamente con la red virtual de Hola. Selección Hola red virtual que desea toomigrate.
> [!NOTE]
> [Migrar máquina virtual solo en clásico](migrate-single-classic-to-resource-manager.md) mediante la creación de una nueva máquina virtual de administrador de recursos con discos administrados utilizando los archivos de (sistema operativo y datos) de disco duro virtual Hola de máquina virtual de Hola.
<br>

> [!NOTE]
> nombre de red virtual de Hello puede ser diferente de lo que se muestra en hello nuevo Portal. nuevo Portal de Azure Hello muestra nombre hello como `[vnet-name]` nombre de red virtual real de hello es del tipo `Group [resource-group-name] [vnet-name]`. Antes de migrar, nombre de red virtual real de Hola de búsqueda con el comando de hello `Get-AzureVnetSite | Select -Property Name` o verlo en hello antiguo Portal de Azure. 

Este ejemplo establece Hola nombre de red virtual demasiado**myVnet**. Reemplace el nombre de red virtual de ejemplo de Hola por los suyos propios.

```powershell
    $vnetName = "myVnet"
```

> [!NOTE]
> Si la red virtual de Hola contiene web o roles de trabajo o máquinas virtuales con las configuraciones no compatibles, obtendrá un mensaje de error de validación.
>
>

En primer lugar, validar si se puede migrar la red virtual de hello usando el siguiente comando de hello:

```powershell
    Move-AzureVirtualNetwork -Validate -VirtualNetworkName $vnetName
```

Hello comando anterior muestra las advertencias y los errores que bloquear la migración. Si la validación es correcta, puede continuar con hello siguiendo el paso de preparación:

```powershell
    Move-AzureVirtualNetwork -Prepare -VirtualNetworkName $vnetName
```

Comprobar la configuración de Hola para hello preparado máquinas virtuales mediante el uso de PowerShell de Azure u Hola portal de Azure. Si no está listo para la migración y desea que el estado anterior de toogo toohello atrás, use Hola siguiente comando:

```powershell
    Move-AzureVirtualNetwork -Abort -VirtualNetworkName $vnetName
```

Si configuración preparada hello es correcto, puede desplazarse hacia delante y confirmar recursos Hola usando el siguiente comando de hello:

```powershell
    Move-AzureVirtualNetwork -Commit -VirtualNetworkName $vnetName
```

## <a name="step-62-migrate-a-storage-account"></a>Paso 6.2: Migración de una cuenta de almacenamiento
Una vez que haya terminado la migración de máquinas virtuales hello, se recomienda que migrar las cuentas de almacenamiento de Hola.

Antes de migrar cuentas de almacenamiento de hello, lleve a cabo anteriores comprobaciones de requisitos previos:

* **Migrar máquinas virtuales clásicas cuyos discos se almacenan en la cuenta de almacenamiento de Hola**

    Anterior comando devuelve RoleName y DiskName de las propiedades de todos los discos de máquina virtual clásicas de hello en la cuenta de almacenamiento de Hola. RoleName es nombre de Hola de hello toowhich de máquina virtual que un disco está conectado. Si precede el comando devuelve los discos, a continuación, asegúrese de que toowhich de máquinas virtuales estos discos conectados se migran antes de migrar Hola cuenta de almacenamiento.
    ```powershell
     $storageAccountName = 'yourStorageAccountName'
      Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Select-Object -ExpandProperty AttachedTo -Property `
      DiskName | Format-List -Property RoleName, DiskName

    ```
* **Eliminar adjuntas clásicos discos de máquina virtual almacenados en la cuenta de almacenamiento de Hola**

    Buscar adjuntas clásicos discos de máquina virtual en el almacenamiento de hello cuenta mediante comando siguiente:

    ```powershell
        $storageAccountName = 'yourStorageAccountName'
        Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Where-Object -Property AttachedTo -EQ $null | Format-List -Property DiskName  

    ```
    Si el comando anterior devuelve discos, elimínelos con el comando siguiente:

    ```powershell
       Remove-AzureDisk -DiskName 'yourDiskName'
    ```
* **Eliminar imágenes de máquina virtual almacenadas en la cuenta de almacenamiento de Hola**

    Anterior comando devuelve todas las imágenes de máquina virtual de hello con disco del sistema operativo almacenado en la cuenta de almacenamiento de Hola.
     ```powershell
        Get-AzureVmImage | Where-Object { $_.OSDiskConfiguration.MediaLink -ne $null -and $_.OSDiskConfiguration.MediaLink.Host.Contains($storageAccountName)`
                                } | Select-Object -Property ImageName, ImageLabel
     ```
     Anterior comando devuelve todas las imágenes de máquina virtual de hello con discos de datos almacenados en la cuenta de almacenamiento de Hola.
     ```powershell

        Get-AzureVmImage | Where-Object {$_.DataDiskConfigurations -ne $null `
                                         -and ($_.DataDiskConfigurations | Where-Object {$_.MediaLink -ne $null -and $_.MediaLink.Host.Contains($storageAccountName)}).Count -gt 0 `
                                        } | Select-Object -Property ImageName, ImageLabel
     ```
    Eliminar todas las imágenes de máquina virtual de hello devueltos por encima de comandos mediante el comando anterior:
    ```powershell
    Remove-AzureVMImage -ImageName 'yourImageName'
    ```

Validar cada cuenta de almacenamiento para la migración mediante Hola siguiente comando. En este ejemplo, es el nombre de cuenta de almacenamiento de hello **myStorageAccount**. Sustituir el nombre de ejemplo de Hola por Hola de su propia cuenta de almacenamiento.

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Validate -StorageAccountName $storageAccountName
```

Siguiente paso es la cuenta de almacenamiento de hello tooPrepare para la migración

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Prepare -StorageAccountName $storageAccountName
```

Comprobar la configuración de Hola para hello preparado cuenta de almacenamiento mediante el uso de PowerShell de Azure u Hola portal de Azure. Si no está listo para la migración y desea que el estado anterior de toogo toohello atrás, use Hola siguiente comando:

```powershell
    Move-AzureStorageAccount -Abort -StorageAccountName $storageAccountName
```

Si configuración preparada hello es correcto, puede desplazarse hacia delante y confirmar recursos Hola usando el siguiente comando de hello:

```powershell
    Move-AzureStorageAccount -Commit -StorageAccountName $storageAccountName
```

## <a name="next-steps"></a>Pasos siguientes
* [Información general de migración admitida por la plataforma de recursos de IaaS de tooAzure clásico Administrador de recursos](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Técnica de fondo admitida por la plataforma de migración de clásico tooAzure el Administrador de recursos](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Planear la migración de los recursos de IaaS de tooAzure clásico Administrador de recursos](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Usar recursos de IaaS CLI toomigrate de tooAzure clásico Administrador de recursos](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Herramientas de la Comunidad para ayudar con la migración de los recursos de IaaS de tooAzure clásico Administrador de recursos](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Revisión de los errores más comunes en la migración](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Hola de revisión más preguntas más frecuentes acerca de cómo migrar recursos de IaaS de tooAzure clásico Administrador de recursos](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
