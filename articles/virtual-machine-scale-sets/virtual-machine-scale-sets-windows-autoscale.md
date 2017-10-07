---
title: "aaaAutoscale conjuntos de escalas de máquina Virtual de Windows | Documentos de Microsoft"
description: "Configuración del escalado automático para un conjunto de escalado de máquinas virtuales Windows mediante Azure PowerShell"
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 88886cad-a2f0-46bc-8b58-32ac2189fc93
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 67cf1c5063ceba4fc076dc270090defdbddbcfe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-machines-in-a-virtual-machine-scale-set"></a>Escalado automático de máquinas en un conjunto de escalado de máquinas virtuales
Conjuntos de escalas de máquina virtual hacen más sencillo para usted toodeploy y administran máquinas virtuales idénticas como un conjunto. Los conjuntos de escala proporcionan una capa de proceso altamente escalable y personalizable para aplicaciones de gran escala y admiten imágenes de la plataforma Windows, imágenes de la plataforma Linux, imágenes personalizadas y extensiones. Para más información acerca de los conjuntos de escala, consulte [Conjuntos de escala de máquinas virtuales](virtual-machine-scale-sets-overview.md).

Este tutorial muestra cómo establece un conjunto de escala de máquinas virtuales de Windows y, automáticamente, escala de máquinas de Hola Hola toocreate. Crear escala de hello establecer y configurar el escalado mediante la creación de una plantilla de Azure Resource Manager e implementación mediante PowerShell de Azure. Para más información sobre las plantillas, consulte [Creación de plantillas del Administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md). toolearn más información acerca de escalado automático de conjuntos de escalado, consulte [el escalado automático y establece de la escala en la máquina Virtual](virtual-machine-scale-sets-autoscale-overview.md).

En este artículo, implementar siguiente Hola recursos y extensiones:

* Microsoft.Storage/storageAccounts
* Microsoft.Network/virtualNetworks
* Microsoft.Network/publicIPAddresses
* Microsoft.Network/loadBalancers
* Microsoft.Network/networkInterfaces
* Microsoft.Compute/virtualMachines
* Microsoft.Compute/virtualMachineScaleSets
* Microsoft.Insights.VMDiagnosticsSettings
* Microsoft.Insights/autoscaleSettings

Para más información sobre los recursos de Resource Manager, consulte [Implementación mediante Azure Resource Manager frente al modelo clásico](../azure-resource-manager/resource-manager-deployment-model.md).

## <a name="step-1-install-azure-powershell"></a>Paso 1: Instalación de Azure PowerShell
Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) para obtener información acerca de cómo instalar la versión más reciente de Hola de PowerShell de Azure, seleccione su suscripción y firma en tooAzure.

## <a name="step-2-create-a-resource-group-and-a-storage-account"></a>Paso 2: Creación de un grupo de recursos y una cuenta de almacenamiento
1. **Crear un grupo de recursos** : todos los recursos deben ser el grupo de recursos de tooa implementado. Use [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx) toocreate un grupo de recursos denominado **vmsstestrg1**.
2. **Crear una cuenta de almacenamiento** : esta cuenta de almacenamiento es donde se almacena la plantilla de Hola. Use [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) toocreate una cuenta de almacenamiento denominada **vmsstestsa**.

## <a name="step-3-create-hello-template"></a>Paso 3: Crear plantilla de Hola
Una plantilla de Azure Resource Manager hace posible toodeploy y administrar recursos de Azure de forma conjunta mediante una descripción de JSON de recursos de Hola y parámetros de implementación asociados.

1. En su editor favorito, cree el archivo hello C:\VMSSTemplate.json y agregue Hola inicial JSON toosupport Hola plantilla de la estructura.

    ```json
    {
      "$schema":"http://schema.management.azure.com/schemas/2014-04-01-preview/VM.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
      },
      "variables": {
      },
      "resources": [
      ]
    }
    ```

2. Parámetros no son siempre obligatorios, pero proporcionan una manera tooinput valores cuando se implementa la plantilla de Hola. Agregue estos parámetros en el elemento primario Hola parámetros que agregó toohello plantilla.

    ```json   
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
    * Un nombre para la máquina virtual independiente hello tooaccess usado Hola máquinas en conjunto de escalas de Hola.
    * nombre de Hola de cuenta de almacenamiento de Hola donde se almacena la plantilla de Hola.
    * número de Hola de máquinas virtuales tooinitially crear en el conjunto de escalas de Hola.
    * nombre de Hola y la contraseña de cuenta de administrador de hello en máquinas virtuales de Hola.
    * Establece un prefijo de nombre de los recursos de Hola que se crean la escala de hello toosupport.

3. Las variables pueden usarse en un valores toospecify de plantilla que se pueden cambiar con frecuencia o valores que necesitan toobe crean a partir de una combinación de valores de parámetro. Agregue estas variables en el elemento primario Hola variables que agregó toohello plantilla.

    ```json
    "dnsName1": "[concat(parameters('resourcePrefix'),'dn1')]",
    "dnsName2": "[concat(parameters('resourcePrefix'),'dn2')]",
    "publicIP1": "[concat(parameters('resourcePrefix'),'ip1')]",
    "publicIP2": "[concat(parameters('resourcePrefix'),'ip2')]",
    "loadBalancerName": "[concat(parameters('resourcePrefix'),'lb1')]",
    "virtualNetworkName": "[concat(parameters('resourcePrefix'),'vn1')]",
    "nicName": "[concat(parameters('resourcePrefix'),'nc1')]",
    "lbID": "[resourceId('Microsoft.Network/loadBalancers',variables('loadBalancerName'))]",
    "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/loadBalancerFrontEnd')]",
    "storageAccountSuffix": [ "a", "g", "m", "s", "y" ],
    "diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'a')]",
    "accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/','Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
      "wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
    "wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Processor Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU utilization\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
    "wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
    "wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
    "wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
    ```
   
    * Los nombres DNS que se usan por hello interfaces de red.

        * Hola nombres de las direcciones IP y los prefijos de red virtual de Hola y las subredes.
        * Hello nombres e identificadores de red virtual de hello, equilibrador de carga y las interfaces de red.
        * Nombres de cuenta de almacenamiento para las cuentas de hello asociados a las máquinas de hello en el conjunto de escalas de Hola.
        * Configuración de extensión de diagnóstico que se instala en máquinas virtuales de Hola Hola. Para obtener más información acerca de la extensión de diagnósticos de hello, consulte [crear una máquina Virtual de Windows con la supervisión y diagnósticos mediante la plantilla de administrador de recursos de Azure](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

4. Agregar recurso de cuenta de almacenamiento de hello bajo el elemento primario Hola recursos que agregó toohello plantilla. Esta plantilla utiliza un hello toocreate de bucle recomendada cinco cuentas de almacenamiento donde se almacenan los discos del sistema operativo hello y datos de diagnóstico. Puede admitir este conjunto de cuentas de seguridad de máquinas virtuales de too100 en un conjunto de escala, que es el máximo actual de Hola. Cada cuenta de almacenamiento se denomina con un designador de letra que se definió en variables de hello combinadas con prefijo de Hola que se proporciona en los parámetros de hello para la plantilla de Hola.

    ```json
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat(parameters('resourcePrefix'), variables('storageAccountSuffix')[copyIndex()])]",
      "apiVersion": "2015-06-15",
      "copy": {
        "name": "storageLoop",
        "count": 5
      },
      "location": "[resourceGroup().location]",
      "properties": { "accountType": "Standard_LRS" }
    },
    ```

5. Agregar recursos de red virtual de Hola. Consulte [Proveedor de recursos de red](../virtual-network/resource-groups-networking.md)para más información.

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
        "subnets": [
          {
            "name": "subnet1",
            "properties": { "addressPrefix": "10.0.0.0/24" }
          }
        ]
      }
    },
    ```

6. Agregar Hola públicos recursos de dirección IP que se usan por hello equilibrador de carga y la interfaz de red.

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP1')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName1')]"
        }
      }
    },
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP2')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName2')]"
        }
      }
    },
    ```

7. Agregar recurso de equilibrador de carga de hello utilizado por el conjunto de escalas de Hola. Para más información, consulte [Compatibilidad del Administrador de recursos de Azure con el equilibrador de carga](../load-balancer/load-balancer-arm.md)

    ```json   
    {
      "apiVersion": "2015-06-15",
      "name": "[variables('loadBalancerName')]",
      "type": "Microsoft.Network/loadBalancers",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
      ],
      "properties": {
        "frontendIPConfigurations": [
          {
            "name": "loadBalancerFrontEnd",
            "properties": {
              "publicIPAddress": {
                "id": "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
              }
            }
          }
        ],
        "backendAddressPools": [ { "name": "bepool1" } ],
        "inboundNatPools": [
          {
            "name": "natpool1",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[variables('frontEndIPConfigID')]"
              },
              "protocol": "tcp",
              "frontendPortRangeStart": 50000,
              "frontendPortRangeEnd": 50500,
              "backendPort": 3389
            }
          }
        ]
      }
    },
    ```

8. Agregar recurso de interfaz de red de Hola que usa la máquina virtual independiente de Hola. Dado que las máquinas en un conjunto de escala no están accesibles a través de una dirección IP pública, una máquina virtual independiente se crea en Hola mismo virtual máquinas Hola de tooremotely acceso de red.

    ```json  
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP2'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIP2'))]"
              },
              "subnet": {
                "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
              }
            }
          }
        ]
      }
    },
    ```

9. Agregar máquina virtual independiente que Hola Hola misma red que el conjunto de escalas de Hola.

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[parameters('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": { "vmSize": "Standard_A1" },
        "osProfile": {
          "computername": "[parameters('vmName')]",
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
            "name": "[concat(parameters('resourcePrefix'), 'os1')]",
            "vhd": {
              "uri":  "[concat('https://',parameters('resourcePrefix'),'a.blob.core.windows.net/vhds/',parameters('resourcePrefix'),'os1.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"        
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
          ]
        }
      }
    },
    ```

10. Agregar el recurso de conjunto de escalas de máquina virtual de Hola y especifique la extensión de diagnósticos de Hola que está instalado en todas las máquinas virtuales en el conjunto de escalas de Hola. Muchos de los valores de hello para este recurso son similares con el recurso de máquina virtual de Hola. Hola principales diferencias son elementos de capacidad de Hola que especifica el número de Hola de máquinas virtuales en el conjunto de escalas de Hola y upgradePolicy que especifica cómo se realizan las actualizaciones toovirtual máquinas. Hello conjunto de escala no se crea hasta que se crean todas las cuentas de almacenamiento de hello según se haya especificado con el elemento dependsOn de Hola.

    ```json
    {
      "type": "Microsoft.Compute/virtualMachineScaleSets",
      "apiVersion": "2016-03-30",
      "name": "[parameters('vmSSName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
        "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
      ],
      "sku": {
        "name": "Standard_A1",
        "tier": "Standard",
        "capacity": "[parameters('instanceCount')]"
      },
      "properties": {
        "upgradePolicy": {
          "mode": "Manual"
        },
        "virtualMachineProfile": {
          "storageProfile": {
            "osDisk": {
              "vhdContainers": [
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[0], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[1], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[2], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[3], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[4], '.blob.core.windows.net/vhds')]"
              ],
              "name": "vmssosdisk",
              "caching": "ReadOnly",
              "createOption": "FromImage"
            },
            "imageReference": {
              "publisher": "MicrosoftWindowsServer",
              "offer": "WindowsServer",
              "sku": "2012-R2-Datacenter",
              "version": "latest"
            }
          },
          "osProfile": {
            "computerNamePrefix": "[parameters('vmSSName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
          },
          "networkProfile": {
            "networkInterfaceConfigurations": [
              {
                "name": "networkconfig1",
                "properties": {
                  "primary": "true",
                  "ipConfigurations": [
                    {
                      "name": "ip1",
                      "properties": {
                        "subnet": {
                          "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
                        },
                        "loadBalancerBackendAddressPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/backendAddressPools/bepool1')]"
                          }
                        ],
                        "loadBalancerInboundNatPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/inboundNatPools/natpool1')]"
                          }
                        ]
                      }
                    }
                  ]
                }
              }
            ]
          },
          "extensionProfile": {
            "extensions": [
              {
                "name": "Microsoft.Insights.VMDiagnosticsSettings",
                "properties": {
                  "publisher": "Microsoft.Azure.Diagnostics",
                  "type": "IaaSDiagnostics",
                  "typeHandlerVersion": "1.5",
                  "autoUpgradeMinorVersion": true,
                  "settings": {
                    "xmlCfg": "[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
                    "storageAccount": "[variables('diagnosticsStorageAccountName')]"
                  },
                  "protectedSettings": {
                    "storageAccountName": "[variables('diagnosticsStorageAccountName')]",
                    "storageAccountKey": "[listkeys(variables('accountid'), '2015-06-15').key1]",
                    "storageAccountEndPoint": "https://core.windows.net"
                  }
                }
              }
            ]
          }
        }
      }
    },
    ```

11. Agregue hello autoscaleSettings recurso que define cómo se ajusta según el uso de procesador de hello en máquinas de hello en el conjunto de escalas de Hola Hola conjunto de escala.

    ```json
    {
      "type": "Microsoft.Insights/autoscaleSettings",
      "apiVersion": "2015-04-01",
      "name": "[concat(parameters('resourcePrefix'),'as1')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      ],
      "properties": {
        "enabled": true,
        "name": "[concat(parameters('resourcePrefix'),'as1')]",
        "profiles": [
          {
            "name": "Profile1",
            "capacity": {
              "minimum": "1",
              "maximum": "10",
              "default": "1"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "\\Processor(_Total)\\% Processor Time",
                  "metricNamespace": "",
                  "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]",
                  "timeGrain": "PT1M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 50.0
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          }
        ],
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      }
    }
    ```

    Para este tutorial, destacan estos valores:
    
    * **metricName**  
    Este valor es Hola igual que el contador de rendimiento de Hola que hemos definido en la variable de wadperfcounter Hola. Con esa variable, extensión de diagnósticos de hello recopila hello **procesador (_Total)\% tiempo de procesador** contador.
    
    * **metricResourceUri**  
    Este valor es el identificador de recurso de hello del conjunto de escalas de máquina virtual de Hola.
    
    * **timeGrain**  
    Este valor es la granularidad de Hola de métricas de Hola que se recopilan. En esta plantilla, se establece tooone minuto.
    
    * **statistic**  
    Este valor determina la forma métricas Hola Hola combinado tooaccommodate acción de escala automática. Hola los valores posibles son: Average, Min, Max. En esta plantilla, se recopila Hola promedio uso total de CPU de las máquinas virtuales de Hola.
    
    * **timeWindow**  
    Este valor es Hola intervalo de tiempo en el que se recopilan datos de instancia. Debe estar comprendido entre 5 minutos y 12 horas.
    
    * **timeAggregation**  
    su valor determina cómo se deben combinar los datos de Hola que se recopilan con el tiempo. valor predeterminado de Hello es Media. Hola los valores posibles son: promedio, mínimo, máximo, último, Total, recuento.
    
    * **operator**  
    Este valor es el operador de Hola que es usado toocompare Hola hello y datos de umbral de métrica. Hola los valores posibles son: es igual a, valores, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.
    
    * **threshold**  
    Este valor es el valor de Hola que desencadena la acción de escalado de Hola. En esta plantilla, las máquinas se agregan escala toohello establecer una vez Hola uso de la CPU entre máquinas en conjunto hello más de 50%.
    
    * **dirección**  
    Este valor determina la acción de Hola que se realiza cuando se obtiene el valor de umbral de Hola. valores posibles de Hello son aumentan o disminuyen. En esta plantilla, hello número de máquinas virtuales en el conjunto de escalas de hello aumenta si el umbral de hello es más de 50% en el período de tiempo de hello definido.
    
    * **type**  
    Este valor es el tipo de Hola de acción que se realizarán y se debe establecer tooChangeCount.
    
    * **value**  
    Este valor es el número de Hola de máquinas virtuales que se agregan o quitan del conjunto de escalas de Hola. Este valor debe ser 1 o un valor superior. valor predeterminado de Hello es 1. En esta plantilla, Hola establece número de máquinas en escala de hello aumenta 1 cuando se alcanza el umbral de Hola.
    
    * **cooldown**  
    Este valor es cantidad de Hola de toowait de tiempo desde la última acción de escalado de hello antes de que se produce la acción siguiente Hola. Debe estar comprendido entre un minuto y una semana.

12. Guarde el archivo de plantilla de hello.    

## <a name="step-4-upload-hello-template-toostorage"></a>Paso 4: Cargar Hola plantilla toostorage
plantilla de Hola se puede cargar como sabe hello y clave principal de la cuenta de almacenamiento de Hola que creó en el paso 1.

1. En la ventana de Microsoft Azure PowerShell hello, establecer una variable que especifica el nombre de Hola de cuenta de almacenamiento de Hola que creó en el paso 1.
   
    ```powershell
    $storageAccountName = "vmstestsa"
    ```

2. Establecer una variable que especifica la clave principal de Hola de cuenta de almacenamiento de Hola.
   
    ```powershell
    $storageAccountKey = "<primary-account-key>"
    ```
   
   Puede obtener esta clave, haga clic en un icono de llave Hola al ver los recursos de cuenta de almacenamiento de Hola Hola portal de Azure.
3. Crear objeto de contexto de cuenta de almacenamiento de hello es decir, las operaciones de toovalidate utilizado con la cuenta de almacenamiento de Hola.
   
    ```powershell
    $ctx = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
    ```

4. Crear contenedor de Hola para almacenar la plantilla de Hola.

    ```powershell
    $containerName = "templates"
    New-AzureStorageContainer -Name $containerName -Context $ctx  -Permission Blob
    ```

5. Cargar nuevo contenedor toohello del archivo de plantilla de Hola.

    ```powershell   
    $blobName = "VMSSTemplate.json"
    $fileName = "C:\" + $BlobName
    Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob  $blobName -Context $ctx
    ```

## <a name="step-5-deploy-hello-template"></a>Paso 5: Implementar la plantilla de Hola
Ahora que ha creado la plantilla de hello, puede empezar a implementar los recursos de Hola. Utilice este proceso de hello toostart de comando:

```powershell
New-AzureRmResourceGroupDeployment -Name "vmsstestdp1" -ResourceGroupName "vmsstestrg1" -TemplateUri "https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json"
```

Cuando se presiona escriba, son valores tooprovide solicitadas para las variables de Hola que asignó. Proporcione estos valores:

```powershell
vmName: vmsstestvm1
  vmSSName: vmsstest1
  instanceCount: 5
  adminUserName: vmadmin1
  adminPassword: VMpass1
  resourcePrefix: vmsstest
```

Para implementar todos los toosuccessfully de recursos de hello tardará aproximadamente 15 minutos.

> [!NOTE]
> También puede usar recursos del portal de hello capacidad toodeploy Hola. Utilice este vínculo: "https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template>"
> 
> 

## <a name="step-6-monitor-resources"></a>Paso 6: Supervisión de recursos
Puede obtener información acerca de los conjuntos de escala de máquinas virtuales mediante estos métodos:

* Hola portal de Azure: actualmente, puede obtener una cantidad limitada de información mediante el portal de Hola.
* Hola [Explorador de recursos de Azure](https://resources.azure.com/) -esta herramienta es más adecuado para explorar el estado actual de Hola de su conjunto de escalas de hello. Siga esta ruta de acceso y debería ver la vista de instancia de Hola de escala de hello establecido que creó:
  
    Suscripciones > {su suscripción} > resourceGroups > vmsstestrg1 > proveedores > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines

* Azure PowerShell, Use este comando tooget cierta información:

  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
  ```
  
  O
  
  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceView
  ```

* Conectar máquina virtual independiente que toohello tal como lo haría con cualquier otro equipo y, a continuación, se pueden obtener acceso remoto a máquinas virtuales de hello en procesos individuales de hello escala conjunto toomonitor.

> [!NOTE]
> Una API de REST completa para más información acerca de los conjuntos de escala se puede encontrar en [Conjuntos de escala de máquinas virtuales](https://msdn.microsoft.com/library/mt589023.aspx)

## <a name="step-7-remove-hello-resources"></a>Paso 7: Quitar recursos de Hola
Dado que se le cobra por recursos que usa en Azure, siempre es un recursos toodelete recomendable que ya no son necesarios. No es necesario toodelete cada recurso por separado de un grupo de recursos. Puede eliminar el grupo de recursos de Hola y todos sus recursos se eliminan automáticamente.

  ```powershell
  Remove-AzureRmResourceGroup -Name vmsstestrg1
  ```

Si desea tookeep el grupo de recursos, puede eliminar sólo al conjunto de escala de Hola.

  ```powershell
  Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name"
  ```

## <a name="next-steps"></a>Pasos siguientes
* Administrar conjunto de escalas de hello recién creado con información de hello en [administrar máquinas virtuales en un conjunto de escala de máquinas virtuales](virtual-machine-scale-sets-windows-manage.md).
* Más información sobre el escalado vertical si consulta [Escalado automático vertical con conjuntos de escalado de máquinas virtuales](virtual-machine-scale-sets-vertical-scale-reprovision.md)
* Encuentre ejemplos de características de supervisión de Azure Monitor en [Ejemplos de inicio rápido de PowerShell de Azure Monitor](../monitoring-and-diagnostics/insights-powershell-samples.md).
* Obtenga información sobre las características de notificación de [usar escalado automático acciones toosend correo electrónico y webhook notificaciones de alerta en el Monitor de Azure](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)
* Obtenga información acerca de cómo demasiado[toosend webhook y correo electrónico notificaciones de alerta de registros de auditoría de uso en el Monitor de Azure](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)

