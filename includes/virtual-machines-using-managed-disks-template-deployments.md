# <a name="using-managed-disks-in-azure-resource-manager-templates"></a>Uso de discos administrados en plantillas de Azure Resource Manager

Este documento le guía a través de las diferencias de hello entre los discos administrados y no administrados cuando se usa máquinas virtuales de Azure Resource Manager plantillas tooprovision. Esto le permitirá tooupdate plantillas existentes que usan discos de toomanaged de discos no administrados. Como referencia, estamos utilizando hello [101 vm simple windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) plantilla como guía. Puede ver la plantilla Hola utilizan ambos [discos administrados por](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) y una versión anterior usando [sin administrar discos](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) si lo desea toodirectly compararlos.

## <a name="unmanaged-disks-template-formatting"></a>Formato de plantilla de discos no administrados

toobegin, echaremos un vistazo en discos sin administrar cómo se implementan. Al crear discos no administrados, tiene un archivos de disco duro virtual de almacenamiento cuenta toohold Hola. Puede crear una cuenta de almacenamiento o usar una ya existente. En este artículo le mostrará cómo toocreate una nueva cuenta de almacenamiento. tooaccomplish, necesita un recurso de la cuenta de almacenamiento en bloque de recursos de hello tal y como se muestra a continuación.

```
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2016-01-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "kind": "Storage",
    "properties": {}
}
```

En el objeto de máquina virtual de hello, necesitamos una dependencia en tooensure de cuenta de almacenamiento de Hola que ha creado antes de la máquina virtual de Hola. Dentro de hello `storageProfile` sección, a continuación, especificamos Hola URI completo de hello ubicación del disco duro virtual, que hace referencia la cuenta de almacenamiento de Hola y es necesario para el disco de SO de Hola y los discos de datos. 

```
{
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "name": "osdisk",
                "vhd": {
                    "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/osdisk.vhd')]"
                },
                "caching": "ReadWrite",
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "name": "datadisk1",
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "vhd": {
                        "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/datadisk1.vhd')]"
                    },
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

## <a name="managed-disks-template-formatting"></a>Formato de plantilla de discos administrados

Con los discos de Azure administrados, disco Hola se convierte en un recurso de nivel superior y ya no requiere una toobe de cuenta de almacenamiento creado por el usuario de Hola. Discos administrados están expuestos en primer lugar en hello `2016-04-30-preview` versión de API, están disponibles en todas las versiones posteriores de API y ahora son tipo de disco de hello predeterminado. Hello las secciones siguientes se guiarán a través de la configuración predeterminada de Hola y de detallan cómo toofurther personalizar los discos.

> [!NOTE]
> Se recomienda una API toouse versión posterior a `2016-04-30-preview` tal y como se produjeron cambios importantes entre `2016-04-30-preview` y `2017-03-30`.
>
>

### <a name="default-managed-disk-settings"></a>Configuración predeterminada de discos administrados

toocreate una máquina virtual con discos administrados, que ya no necesita el recurso de cuenta de almacenamiento de toocreate hello y puede actualizar el recurso de máquina virtual como se indica a continuación. Tenga en cuenta específicamente esa hello `apiVersion` refleja `2017-03-30` hello y `osDisk` y `dataDisks` ya no hacen referencia tooa URI específico para hello VHD. Al implementar sin especificar propiedades adicionales, usará el disco de hello [almacenamiento estándar LRS](../articles/storage/common/storage-redundancy.md). Si no se especifica ningún nombre, toma el formato hello `<VMName>_OsDisk_1_<randomstring>` para el disco de SO de Hola y `<VMName>_disk<#>_<randomstring>` para cada disco de datos. De forma predeterminada, se deshabilita el cifrado de disco de Azure; almacenamiento en caché es lectura/escritura para el disco de SO de Hola y ninguno de los discos de datos. Puede observar en el siguiente ejemplo de Hola que sigue habiendo una dependencia de cuenta de almacenamiento, aunque esto es solo para el almacenamiento de diagnósticos y no es necesario para el almacenamiento en disco.

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="using-a-top-level-managed-disk-resource"></a>Uso de un recurso de disco administrado de nivel superior

Como una configuración de disco de hello toospecifying alternativo en el objeto de máquina virtual de hello, puede crear un recurso de disco de nivel superior y adjuntar como parte de la creación de máquinas virtuales de Hola. Por ejemplo, podemos crear un recurso de disco de manera toouse como un disco de datos.

```
{
    "type": "Microsoft.Compute/disks",
    "name": "[concat(variables('vmName'),'-datadisk1')]",
    "apiVersion": "2017-03-30",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "properties": {
        "creationData": {
            "createOption": "Empty"
        },
        "diskSizeGB": 1023
    }
}
```

En el objeto de máquina virtual de hello, a continuación, podemos hacer referencia a este toobe de objeto de disco conectado. Especificar el Id. de recurso de Hola de hello administrado disco que creamos en hello `managedDisk` datos adjuntos de hello del disco de hello como Hola se crea la máquina virtual que permite la propiedad. Tenga en cuenta que hello `apiVersion` de hello recurso de máquina virtual se establece demasiado`2017-03-30`. Tenga en cuenta también que hemos creado una dependencia en tooensure de recursos de disco Hola se crea correctamente antes de la creación de la máquina virtual. 

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]",
        "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "lun": 0,
                    "name": "[concat(variables('vmName'),'-datadisk1')]",
                    "createOption": "attach",
                    "managedDisk": {
                        "id": "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
                    }
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="create-managed-availability-sets-with-vms-using-managed-disks"></a>Creación de conjuntos de disponibilidad administrados con máquinas virtuales con discos administrados

toocreate administrado disponibilidad conjuntos con máquinas virtuales con discos administrados, agregar hello `sku` disponibilidad toohello de objeto establezca recursos y hello `name` propiedad demasiado`Aligned`. Esto garantiza que los discos de Hola para cada máquina virtual estén suficientemente aislados entre sí tooavoid puntos únicos de error. Tenga en cuenta también que hello `apiVersion` para recurso de conjunto de disponibilidad de Hola se establece demasiado`2017-03-30`.

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/availabilitySets",
    "location": "[resourceGroup().location]",
    "name": "[variables('avSetName')]",
    "properties": {
        "PlatformUpdateDomainCount": 3,
        "PlatformFaultDomainCount": 2
    },
    "sku": {
        "name": "Aligned"
    }
}
```

### <a name="additional-scenarios-and-customizations"></a>Personalizaciones y escenarios adicionales

toofind toda la información de especificaciones de la API de REST de hello, revise hello [crear un disco administrado documentación de la API de REST](/rest/api/manageddisks/disks/disks-create-or-update). Encontrará escenarios adicionales, así como valor predeterminado y los valores aceptables que pueden ser API toohello enviados a través de las implementaciones de plantilla. 

## <a name="next-steps"></a>Pasos siguientes

* Para plantillas completas que usan discos administrados visitan Hola siguientes vínculos de repositorio de inicio rápido de Azure.
    * [Máquina virtual Windows con disco administrado](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
    * [Máquina virtual Linux con disco administrado](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
    * [Lista completa de plantillas de discos administrados](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* Visite hello [información general de Azure administra discos](../articles/virtual-machines/windows/managed-disks-overview.md) documento toolearn Obtenga más información sobre discos administrados.
* Consultar la documentación de referencia de plantilla de Hola para recursos de máquina virtual visitando hello [referencia de plantillas de Microsoft.Compute/virtualMachines](/templates/microsoft.compute/virtualmachines) documento.
* Consultar la documentación de referencia de plantilla de Hola para recursos de disco visitando hello [referencia de plantillas de Microsoft.Compute/disks](/templates/microsoft.compute/disks) documento.
 
