---
title: "máquinas de aaaVirtual en una plantilla de Azure Resource Manager | Microsoft Azure"
description: "Más información sobre cómo se definen los recursos de máquina virtual de hello en una plantilla de Azure Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f63ab5cc-45b8-43aa-a4e7-69dc42adbb99
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: davidmu
ms.openlocfilehash: 94adcbe5bf44be72ffc1b920461aed15c4fc025f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machines-in-an-azure-resource-manager-template"></a>Máquinas virtuales de una plantilla de Azure Resource Manager

Este artículo describe aspectos de una plantilla de Azure Resource Manager que se aplican toovirtual máquinas. En este artículo no se describe una plantilla completa para crear una máquina virtual. Para ello, necesita definiciones de recursos de cuentas de almacenamiento, interfaces de red, direcciones IP públicas y redes virtuales. Para obtener más información acerca de cómo se pueden definir estos recursos juntos, vea hello [tutorial de la plantilla de administrador de recursos](../../azure-resource-manager/resource-manager-template-walkthrough.md).

Hay muchos [plantillas en la Galería de hello](https://azure.microsoft.com/documentation/templates/?term=VM) que incluyen recursos de máquina virtual de Hola. No todos los elementos que pueden incorporarse en una plantilla se describen aquí.

En este ejemplo se muestra una sección de recursos típica de una plantilla para crear un número especificado de máquinas virtuales:

```json
"resources": [
  { 
    "apiVersion": "2016-04-30-preview", 
    "type": "Microsoft.Compute/virtualMachines", 
    "name": "[concat('myVM', copyindex())]", 
    "location": "[resourceGroup().location]",
    "copy": {
      "name": "virtualMachineLoop", 
      "count": "[parameters('numberOfInstances')]"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/myNIC', copyindex())]" 
    ], 
    "properties": { 
      "hardwareProfile": { 
        "vmSize": "Standard_DS1" 
      }, 
      "osProfile": { 
        "computername": "[concat('myVM', copyindex())]", 
        "adminUsername": "[parameters('adminUsername')]", 
        "adminPassword": "[parameters('adminPassword')]" 
      }, 
      "storageProfile": { 
        "imageReference": { 
          "publisher": "MicrosoftWindowsServer", 
          "offer": "WindowsServer", 
          "sku": "2012-R2-Datacenter", 
          "version": "latest" 
        }, 
        "osDisk": { 
          "name": "[concat('myOSDisk', copyindex())]",
          "caching": "ReadWrite", 
          "createOption": "FromImage" 
        },
        "dataDisks": [
          {
            "name": "[concat('myDataDisk', copyindex())]",
            "diskSizeGB": "100",
            "lun": 0,
            "createOption": "Empty"
          }
        ] 
      }, 
      "networkProfile": { 
        "networkInterfaces": [ 
          { 
            "id": "[resourceId('Microsoft.Network/networkInterfaces',
              concat('myNIC', copyindex()))]" 
          } 
        ] 
      },
      "diagnosticsProfile": {
        "bootDiagnostics": {
          "enabled": "true",
          "storageUri": "[concat('https://', variables('storageName'), '.blob.core.windows.net')]"
        }
      } 
    },
    "resources": [ 
      { 
        "name": "Microsoft.Insights.VMDiagnosticsSettings", 
        "type": "extensions", 
        "location": "[resourceGroup().location]", 
        "apiVersion": "2016-03-30", 
        "dependsOn": [ 
          "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]" 
        ], 
        "properties": { 
          "publisher": "Microsoft.Azure.Diagnostics", 
          "type": "IaaSDiagnostics", 
          "typeHandlerVersion": "1.5", 
          "autoUpgradeMinorVersion": true, 
          "settings": { 
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), 
            variables('wadmetricsresourceid'), 
            concat('myVM', copyindex()),
            variables('wadcfgxend')))]", 
            "storageAccount": "[variables('storageName')]" 
          }, 
          "protectedSettings": { 
            "storageAccountName": "[variables('storageName')]", 
            "storageAccountKey": "[listkeys(variables('accountid'), 
              '2015-06-15').key1]", 
            "storageAccountEndPoint": "https://core.windows.net" 
          } 
        } 
      },
      {
        "name": "MyCustomScriptExtension",
        "type": "extensions",
        "apiVersion": "2016-03-30",
        "location": "[resourceGroup().location]",
        "dependsOn": [
          "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]"
        ],
        "properties": {
          "publisher": "Microsoft.Compute",
          "type": "CustomScriptExtension",
          "typeHandlerVersion": "1.7",
          "autoUpgradeMinorVersion": true,
          "settings": {
            "fileUris": [
              "[concat('https://', variables('storageName'),
                '.blob.core.windows.net/customscripts/start.ps1')]" 
            ],
            "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -File start.ps1"
          }
        }
      } 
    ]
  } 
]
``` 

> [!NOTE] 
>Se basa en una cuenta de almacenamiento que se ha creado previamente. Puede crear cuenta de almacenamiento de hello mediante la implementación de plantilla de Hola. ejemplo de Hola también se basa en una interfaz de red y sus recursos dependientes que se pueden definir en plantilla Hola. Estos recursos no se muestran en el ejemplo de Hola.
>
>

## <a name="api-version"></a>Versión de API

Cuando se implementación mediante una plantilla de recursos, tienes toospecify una versión de Hola API toouse. Hola ilustra los recursos de máquina virtual de hello usando este elemento de valor apiVersion:

```
"apiVersion": "2016-04-30-preview",
```

versión de Hola de hello API que se especifique en la plantilla afecta a qué propiedades se pueden definir en plantilla Hola. En general, debe seleccionar la versión más reciente de la API de hello al crear plantillas. Para las plantillas existentes, puede decidir si desea toocontinue utilizando una versión anterior de la API o actualizar la plantilla para hello última versión tootake las nuevas características.

Use estas oportunidades para obtener versiones más recientes de API de hello:

- API de REST: [Mostrar todos los proveedores de recursos](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)
- PowerShell: [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)
- CLI de Azure 2.0: [az provider show](https://docs.microsoft.com/cli/azure/provider#show)

## <a name="parameters-and-variables"></a>Parámetros y variables

[Parámetros](../../resource-group-authoring-templates.md) facilitan la tarea por usted toospecify valores para la plantilla de hello cuando se ejecuta. En esta sección de parámetros se utiliza en el ejemplo de Hola:

```        
"parameters": {
  "adminUsername": { "type": "string" },
  "adminPassword": { "type": "securestring" },
  "numberOfInstances": { "type": "int" }
},
```

Al implementar la plantilla de ejemplo de Hola, especificar los valores para nombre de Hola y la contraseña de cuenta de administrador de hello en cada máquina virtual y Hola el número de máquinas virtuales toocreate. Tiene la opción de Hola de especificar valores de parámetro en un archivo independiente que se administra con la plantilla de Hola o proporcionar valores cuando se le solicite.

[Las variables](../../resource-group-authoring-templates.md) facilitan automáticamente tooset valores en plantilla de Hola que se usan varias veces a lo largo de él o que cambian con el tiempo. En esta sección de variables se utiliza en el ejemplo de Hola:

```
"variables": { 
  "storageName": "mystore1",
  "accountid": "[concat('/subscriptions/', subscription().subscriptionId, 
    '/resourceGroups/', resourceGroup().name,
  '/providers/','Microsoft.Storage/storageAccounts/', variables('storageName'))]", 
  "wadlogs": "<WadCfg> 
    <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> 
      <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> 
      <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > 
        <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> 
        <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> 
        <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" />
      </WindowsEventLog>", 
  "wadperfcounters": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\">
      <PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Count\">
        <annotation displayName=\"Threads\" locale=\"en-us\"/>
      </PerformanceCounterConfiguration>
    </PerformanceCounters>", 
  "wadcfgxstart": "[concat(variables('wadlogs'), variables('wadperfcounters'), 
    '<Metrics resourceId=\"')]", 
  "wadmetricsresourceid": "[concat('/subscriptions/', subscription().subscriptionId, 
    '/resourceGroups/', resourceGroup().name , 
    '/providers/', 'Microsoft.Compute/virtualMachines/')]", 
  "wadcfgxend": "\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/>
    <MetricAggregation scheduledTransferPeriod=\"PT1M\"/>
    </Metrics></DiagnosticMonitorConfiguration>
    </WadCfg>"
}, 
```

Al implementar la plantilla de ejemplo de Hola, valores de las variables se utilizan para nombre de Hola y el identificador de cuenta de almacenamiento de Hola que creó anteriormente. Las variables también son opciones de Hola de tooprovide usado para la extensión de diagnóstico de Hola. Hola de uso [las prácticas recomendadas para la creación de plantillas de Azure Resource Manager](../../resource-manager-template-best-practices.md) toohelp decida cómo desea toostructure Hola parámetros y variables en la plantilla.

## <a name="resource-loops"></a>bucles de recursos

Si necesita más de una máquina virtual para la aplicación, puede utilizar un elemento de copia en una plantilla. Este elemento opcional recorre creando Hola número de máquinas virtuales que especifica como un parámetro:

```
"copy": {
  "name": "virtualMachineLoop", 
  "count": "[parameters('numberOfInstances')]"
},
```

Además, se utiliza en ejemplo Hola Hola índice de bucle al especificar algunos Hola valores para el recurso de Hola. Por ejemplo, si ha especificado un recuento de instancias de estos tres, nombres de Hola de discos del sistema operativo Hola son myOSDisk1, myOSDisk2 y myOSDisk3:

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
}
```

> [!NOTE] 
>Este ejemplo utiliza discos administrados para las máquinas virtuales de Hola.
>
>

Tenga en cuenta que la creación de un bucle para un recurso de plantilla de hello puede requerir toouse Hola bucle al crear o tener acceso a otros recursos. Por ejemplo, varias máquinas virtuales no pueden usar hello misma interfaz de red, por lo que si recorre en bucle la plantilla de creación de tres máquinas virtuales también debe ejecutar un bucle en crear tres interfaces de red. Al asignar un tooa de interfaz de red virtual, índice de bucle de hello es tooidentify usado:

```
"networkInterfaces": [ { 
  "id": "[resourceId('Microsoft.Network/networkInterfaces',
    concat('myNIC', copyindex()))]" 
} ]
```

## <a name="dependencies"></a>Dependencias

Mayoría de los recursos depende otro toowork recursos correctamente. Máquinas virtuales deben asociarse con una red virtual y toodo que requiere una interfaz de red. Hola [dependsOn](../../resource-group-define-dependencies.md) elemento es toomake usado que esa interfaz de red de hello esté listo toobe usa antes de que se crean máquinas virtuales de hello:

```
"dependsOn": [
  "[concat('Microsoft.Network/networkInterfaces/', 'myNIC', copyindex())]" 
],
```

Resource Manager implementa en paralelo todos los recursos que no dependan de otro que se vaya a implementar. Tenga cuidado al establecer las dependencias porque puede ralentizar accidentalmente el proceso si define algunas que sean innecesarias. Pueden encadenar las dependencias a través de varios recursos. Por ejemplo, interfaz de red de hello depende de la dirección IP pública hello y recursos de red virtual.

¿Cómo puede saber si se requiere una dependencia? Ver valores de hello establecido en la plantilla de Hola. Si un elemento de la definición de recursos de máquina virtual de hello apunta tooanother recursos que está implementado en hello misma plantilla, necesita una dependencia. Por ejemplo, la máquina virtual de ejemplo define un perfil de red:

```
"networkProfile": { 
  "networkInterfaces": [ { 
    "id": "[resourceId('Microsoft.Network/networkInterfaces',
      concat('myNIC', copyindex())]" 
  } ] 
},
```

tooset esta propiedad, la interfaz de red de hello debe existir. Por lo tanto, necesita una dependencia. También debe tooset una dependencia cuando se define un recurso (un elemento secundario) dentro de otro recurso (un elemento primario). Por ejemplo, configuración de diagnóstico de Hola y extensiones de secuencias de comandos personalizadas se definen como recursos secundarios de la máquina virtual de Hola. No se creará hasta que la máquina virtual de hello existe. Por lo tanto, los recursos se marcan como dependiente de la máquina virtual de Hola.

## <a name="profiles"></a>Perfiles

Al definir un recurso de máquina virtual, se utilizan varios elementos de perfil. Algunos son necesarios y otros, opcionales. Por ejemplo, elementos de hello hardwareProfile, osProfile, storageProfile y networkProfile son necesarios, pero hello diagnosticsProfile es opcional. Estos perfiles definen opciones como:
   
- [Tamaño](sizes.md)
- [Nombre](/architecture/best-practices/naming-conventions) y credenciales
- [Configuración del sistema operativo](cli-ps-findimage.md) y disco
- [Interfaz de red](../../virtual-network/virtual-networks-multiple-nics.md) 
- Diagnósticos de arranque

## <a name="disks-and-images"></a>Discos e imágenes
   
En Azure, los archivos de VHD pueden representar [discos o imágenes](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Cuando sistema de operativo hello en un archivo de disco duro virtual está especializada toobe una VM específica, es tooas que se hace referencia un disco. Al sistema operativo de hello en un archivo de disco duro virtual se ha generalizado toobe utiliza toocreate muchas máquinas virtuales, es una imagen de tooas que se hace referencia.   
    
### <a name="create-new-virtual-machines-and-new-disks-from-a-platform-image"></a>Creación de máquinas virtuales y discos a partir de una imagen de plataforma

Cuando se crea una máquina virtual, debe decidir qué toouse de sistema operativo. elemento de imageReference de Hello es sistema de operativo hello toodefine utilizadas de una nueva máquina virtual. ejemplo de Hola muestra una definición para un sistema operativo Windows Server:

```
"imageReference": { 
  "publisher": "MicrosoftWindowsServer", 
  "offer": "WindowsServer", 
  "sku": "2012-R2-Datacenter", 
  "version": "latest" 
},
```

Si desea toocreate un sistema operativo Linux, puede usar esta definición:

```
"imageReference": {
  "publisher": "Canonical",
  "offer": "UbuntuServer",
  "sku": "14.04.2-LTS",
  "version": "latest"
},
```

Opciones de configuración de disco del sistema operativo Hola se asignan por elemento de hello osDisk. Hello en el ejemplo se define un nuevo disco administrado por hello demasiado el almacenamiento en caché el conjunto de modos**ReadWrite** y ese disco Hola se crea a partir un [imagen de la plataforma](cli-ps-findimage.md):

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
},
```

### <a name="create-new-virtual-machines-from-existing-managed-disks"></a>Creación de máquinas virtuales a partir de discos administrados existentes

Si desea que las máquinas virtuales de toocreate de discos existentes, quite imageReference hello y elementos de osProfile de Hola y definir esta configuración de disco:

```
"osDisk": { 
  "osType": "Windows",
  "managedDisk": { 
    "id": "[resourceId('Microsoft.Compute/disks', [concat('myOSDisk', copyindex())])]" 
  }, 
  "caching": "ReadWrite",
  "createOption": "Attach" 
},
```

### <a name="create-new-virtual-machines-from-a-managed-image"></a>Creación de máquinas virtuales a partir de una imagen administrada

Si desea que una máquina virtual desde una imagen administrada toocreate, cambiar los elementos de imageReference hello y definir esta configuración de disco:

```
"storageProfile": { 
  "imageReference": {
    "id": "[resourceId('Microsoft.Compute/images', 'myImage')]"
  },
  "osDisk": { 
    "name": "[concat('myOSDisk', copyindex())]",
    "osType": "Windows",
    "caching": "ReadWrite", 
    "createOption": "FromImage" 
  }
},
```

### <a name="attach-data-disks"></a>Conexión de discos de datos

Si lo desea, puede agregar datos discos toohello máquinas virtuales. Hola [número de discos](sizes.md) depende Hola tamaño del disco de sistema operativo que utilice. Con hello tamaño de máquinas virtuales de hello establece tooStandard_DS1_v2, número máximo de Hola de discos de datos que se podrían agregar toohello ellos es dos. En el ejemplo de Hola, un disco de datos administrados se agrega tooeach VM:

```
"dataDisks": [
  {
    "name": "[concat('myDataDisk', copyindex())]",
    "diskSizeGB": "100",
    "lun": 0, 
    "caching": "ReadWrite",
    "createOption": "Empty"
  }
],
```

## <a name="extensions"></a>Extensiones

Aunque [extensiones](extensions-features.md) son un recurso independiente, sino tooVMs estrechamente relacionados. Las extensiones se pueden agregar como un recurso secundario de hello VM o como un recurso independiente. ejemplo de Hola muestra hello [extensión de diagnósticos](extensions-diagnostics-template.md) añadidos toohello las máquinas virtuales:

```
{ 
  "name": "Microsoft.Insights.VMDiagnosticsSettings", 
  "type": "extensions", 
  "location": "[resourceGroup().location]", 
  "apiVersion": "2016-03-30", 
  "dependsOn": [ 
    "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]" 
  ], 
  "properties": { 
    "publisher": "Microsoft.Azure.Diagnostics", 
    "type": "IaaSDiagnostics", 
    "typeHandlerVersion": "1.5", 
    "autoUpgradeMinorVersion": true, 
    "settings": { 
      "xmlCfg": "[base64(concat(variables('wadcfgxstart'), 
      variables('wadmetricsresourceid'), 
      concat('myVM', copyindex()),
      variables('wadcfgxend')))]", 
      "storageAccount": "[variables('storageName')]" 
    }, 
    "protectedSettings": { 
      "storageAccountName": "[variables('storageName')]", 
      "storageAccountKey": "[listkeys(variables('accountid'), 
        '2015-06-15').key1]", 
      "storageAccountEndPoint": "https://core.windows.net" 
    } 
  } 
},
```

Este recurso de extensión usa los valores de tooprovide de variables de diagnóstico de Hola y de variable de storageName Hola. Si desea toochange Hola datos recopilados por esta extensión, puede agregar más variables de wadperfcounters de toohello de contadores de rendimiento. También puede elegir datos de diagnóstico de hello tooput en una cuenta de almacenamiento diferente a donde se almacenan los discos de máquina virtual de Hola.

Existen muchas extensiones que se pueden instalar en una máquina virtual, pero hello más útil es probablemente hello [extensión de Script personalizado](extensions-customscript.md). En el ejemplo de Hola, un script de PowerShell denominado start.ps1 se ejecuta en cada máquina virtual cuando inicia por primera vez:

```
{
  "name": "MyCustomScriptExtension",
  "type": "extensions",
  "apiVersion": "2016-03-30",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]"
  ],
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.7",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "[concat('https://', variables('storageName'),
          '.blob.core.windows.net/customscripts/start.ps1')]" 
      ],
      "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -File start.ps1"
    }
  }
}
```

secuencia de comandos de Hello start.ps1 puede realizar muchas tareas de configuración. Por ejemplo, no se inicializan los discos de datos de Hola que se agregan toohello máquinas virtuales en el ejemplo de Hola; Puede usar un script personalizado de tooinitialize ellos. Si tiene varios toodo de tareas de inicio, puede usar hello start.ps1 archivo toocall otras secuencias de comandos de PowerShell en el almacenamiento de Azure. ejemplo de Hola usa PowerShell, pero puede usar cualquier método de scripting que está disponible en el sistema operativo de Hola que está usando.

Puede ver estado de Hola de extensiones de hello instalado desde la configuración de extensiones de hello en el portal de hello:

![Consulta del estado de la extensión](./media/template-description/virtual-machines-show-extensions.png)

También puede obtener información de la extensión mediante hello **Get AzureRmVMExtension** PowerShell comando hello **get de la extensión de vm** comando de CLI de Azure 2.0 o hello **obtener información de la extensión**  API de REST.

## <a name="deployments"></a>Implementaciones

Cuando se implementa una plantilla, los recursos de hello Azure pistas que ha implementado como un grupo y automáticamente asigna a un grupo de toothis implementado de nombre. nombre de Hola de implementación de hello es Hola mismo que el nombre de plantilla de Hola Hola.

Si desea obtener sobre el estado de Hola de recursos de implementación de hello, puede usar hoja del grupo de recursos de Hola Hola portal de Azure:

![Obtención de la información de implementación](./media/template-description/virtual-machines-deployment-info.png)
    
No es un problema toouse Hola los mismos recursos de plantilla toocreate o tooupdate los recursos existentes. Al utilizar plantillas de toodeploy de comandos, tiene Hola oportunidad toosay que [modo](../../resource-group-template-deploy.md) desea toouse. se puede establecer el modo de Hello tooeither **completar** o **Incremental**. valor predeterminado de Hello es toodo las actualizaciones incrementales. Tenga precaución al utilizar hello **completar** modo porque se pueden eliminar accidentalmente los recursos. Al establecer el modo de hello demasiado**completar**, Administrador de recursos elimina los recursos de grupo de recursos de Hola que no están en la plantilla de Hola.

## <a name="next-steps"></a>Pasos siguientes

- Cree su propia plantilla con las [Creación de plantillas de Azure Resource Manager](../../resource-group-authoring-templates.md).
- Implementar la plantilla de Hola que creó mediante [crear una máquina virtual de Windows con una plantilla de administrador de recursos](ps-template.md).
- Obtenga información acerca de cómo toomanage Hola las máquinas virtuales que se creó mediante la revisión de [crear y administrar máquinas virtuales de Windows con el módulo de PowerShell de Azure de hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
