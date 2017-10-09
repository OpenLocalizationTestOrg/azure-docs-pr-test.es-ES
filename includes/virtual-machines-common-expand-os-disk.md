## <a name="overview"></a>Información general
Cuando se crea una nueva máquina virtual (VM) en un grupo de recursos mediante la implementación de una imagen de [Azure Marketplace](https://azure.microsoft.com/marketplace/), unidad de sistema operativo de hello predeterminada es 127 GB. Aunque es posible tooadd datos discos toohello VM (según cuántos Hola SKU que ha elegido) y además es tooinstall recomendada aplicaciones y cargas de trabajo intensivas de CPU en estos discos anexo, a menudo los clientes necesitan tooexpand Hola SO unidad toosupport determinados escenarios como la siguiente:

1. Compatibilidad con aplicaciones heredadas que instalan componentes en la unidad del sistema operativo.
2. Migración de una máquina virtual o un equipo físico desde local con una unidad del sistema operativo más grande.

> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: Resource Manager y el clásico. Este artículo incluye el uso de modelo del Administrador de recursos de Hola. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.
> 
> 

## <a name="resize-hello-os-drive"></a>Cambiar el tamaño de unidad de hello SO
En este artículo se podrá llevar a cabo la tarea hello de cambiar el tamaño de unidad de hello SO mediante módulos de administrador de recursos de [Azure Powershell](/powershell/azureps-cmdlets-docs). Abra el ISE de Powershell o la ventana de Powershell en modo de administrador y siga Hola pasos siguientes:

1. Inicio de sesión tooyour Microsoft Azure en modo de administración de recursos de la cuenta y seleccione su suscripción como se indica a continuación:
   
   ```Powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription –SubscriptionName 'my-subscription-name'
   ```
2. Configure el nombre de grupo de recursos y el nombre de la máquina virtual de la siguiente forma:
   
   ```Powershell
   $rgName = 'my-resource-group-name'
   $vmName = 'my-vm-name'
   ```
3. Obtener un tooyour referencia VM como se indica a continuación:
   
   ```Powershell
   $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```
4. Detener Hola VM antes de cambiar el tamaño de disco de hello como se indica a continuación:
   
    ```Powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    ```
5. Y aquí viene momento Hola que nos hemos estado esperando. Establecer tamaño de Hola de valor de hello SO discos toohello deseado y actualizar Hola VM como se indica a continuación:
   
   ```Powershell
   $vm.StorageProfile.OSDisk.DiskSizeGB = 1023
   Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
   ```
   
   > [!WARNING]
   > Hola nuevo tamaño debe ser mayor que el tamaño del disco de hello existente. Hola máximo permitido es de 1023 GB.
   > 
   > 
6. Hola actualizando máquina virtual puede tardar unos segundos. Una vez que el comando hello termina de ejecutarse, reinicie Hola VM como se indica a continuación:
   
   ```Powershell
   Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```

Eso es todo. Ahora RDP en Hola de máquina virtual, abra Administración de equipos (o administración de discos) y expanda la unidad de hello mediante Hola espacio recién asignado.

## <a name="summary"></a>Resumen
En este artículo, se usan Azure Resource Manager módulos de Powershell tooexpand hello unidad de sistema operativo de una máquina virtual de IaaS. Reproducir a continuación es el script completo de Hola para su referencia:

```Powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName 'my-subscription-name'
$rgName = 'my-resource-group-name'
$vmName = 'my-vm-name'
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
$vm.StorageProfile.OSDisk.DiskSizeGB = 1023
Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```

## <a name="next-steps"></a>Pasos siguientes
Aunque en este artículo, nos centramos principalmente en disco Hola SO de hello VM de expansión, hello desarrollado script también se puede usar para cambiar una sola línea de código de expansión Hola datos discos conectados toohello VM. Por ejemplo, tooexpand Hola primero los datos toohello adjunto VM de disco, reemplace hello ```OSDisk``` objeto de ```StorageProfile``` con ```DataDisks``` de matriz y usar un tooobtain índice numérico un disco de datos adjuntos de toofirst de referencia, tal y como se muestra a continuación:

```Powershell
$vm.StorageProfile.DataDisks[0].DiskSizeGB = 1023
```
Del mismo modo puede hacer referencia a otro discos de datos adjunto toohello virtual, ya sea mediante un índice, como se muestra arriba u Hola ```Name``` propiedad del disco de hello tal como se muestra a continuación:

```Powershell
($vm.StorageProfile.DataDisks | Where {$_.Name -eq 'my-second-data-disk'})[0].DiskSizeGB = 1023
```

Active esta casilla si desea toofind out cómo tooattach discos tooan VM de Azure Resource Manager, [artículo](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

