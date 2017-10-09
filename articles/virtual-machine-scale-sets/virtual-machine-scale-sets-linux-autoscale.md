---
title: "aaaAutoscale conjuntos de escalas de máquina Virtual de Linux | Documentos de Microsoft"
description: "Configuración del escalado automático para un conjunto de escalado de máquinas virtuales Linux mediante la CLI de Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 83e93d9c-cac0-41d3-8316-6016f5ed0ce4
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 4352b94ec2973c37bc5616e3be25bd0c9442632b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-linux-machines-in-a-virtual-machine-scale-set"></a>Escalado automático de máquinas de Linux en un conjunto de escalado de máquinas virtuales
Conjuntos de escalas de máquina virtual hacen más sencillo para usted toodeploy y administran máquinas virtuales idénticas como un conjunto. Los conjuntos de escala proporcionan una capa de proceso altamente escalable y personalizable para aplicaciones de gran escala y admiten imágenes de la plataforma Windows, imágenes de la plataforma Linux, imágenes personalizadas y extensiones. más información, consulte toolearn [información general de conjuntos de escala de máquina Virtual](virtual-machine-scale-sets-overview.md).

Este tutorial muestra cómo establece toocreate una escala de máquinas virtuales de Linux con la versión más reciente de Hola de Ubuntu Linux. Hola también se muestra cómo establecer máquinas tooautomatically escala Hola Hola. Crear escala de hello establecer y configurar el escalado mediante la creación de una plantilla de Azure Resource Manager e implementación mediante la CLI de Azure. Para más información sobre las plantillas, consulte [Creación de plantillas del Administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md). toolearn más información acerca de escalado automático de conjuntos de escalado, consulte [el escalado automático y establece de la escala en la máquina Virtual](virtual-machine-scale-sets-autoscale-overview.md).

En este tutorial, se implementa siguiente Hola recursos y extensiones:

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

Antes de empezar a trabajar con los pasos de hello en este tutorial, [instalar hello Azure CLI](../cli-install-nodejs.md).

## <a name="step-1-create-a-resource-group-and-a-storage-account"></a>Paso 1: Creación de un grupo de recursos y una cuenta de almacenamiento

1. **Inicie sesión en Azure tooMicrosoft**  
En la interfaz de línea de comandos (intensiva de errores, Terminal, símbolo del sistema), cambiar el modo de administrador de tooResource y, a continuación, [iniciar sesión con su Id. de trabajo o escuela](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login). Siga las indicaciones de Hola para un tooyour de experiencia de inicio de sesión interactivo cuenta de Azure.

    ```cli   
    azure config mode arm

    azure login
    ```
   
    > [!NOTE]
    > Si dispone de un trabajo o Id. de la escuela y no tiene habilitada la autenticación de dos factores, utilice `azure login -u` con toolog de Id. de hello en sin una sesión interactiva. Si no tiene un identificador profesional o educativo, puede [crear uno desde su cuenta personal de Microsoft](../active-directory/active-directory-users-create-azure-portal.md).
    
2. **Cree un grupo de recursos**  
Todos los recursos deben ser implementado tooa grupo de recursos. Para este tutorial, asigne el nombre de grupo de recursos de hello **vmsstest1**.
   
    ```cli
    azure group create vmsstestrg1 centralus
    ```

3. **Implementar una cuenta de almacenamiento en el nuevo grupo de recursos Hola**  
Esta cuenta de almacenamiento es donde se almacena la plantilla de Hola. Cree una cuenta de almacenamiento denominada " **vmsstestsa**".
   
    ```cli
    azure storage account create -g vmsstestrg1 -l centralus --kind Storage --sku-name LRS vmsstestsa
    ```

## <a name="step-2-create-hello-template"></a>Paso 2: Crear plantilla de Hola
Una plantilla de Azure Resource Manager hace posible toodeploy y administrar recursos de Azure de forma conjunta mediante una descripción de JSON de recursos de Hola y parámetros de implementación asociados.

1. En su editor favorito, cree el archivo hello VMSSTemplate.json y agregue Hola inicial JSON toosupport Hola plantilla de la estructura.

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
   * Un nombre para la cuenta de almacenamiento de Hola donde se almacena la plantilla de Hola.
   * número de Hola de instancias de máquinas virtuales tooinitially crea en el conjunto de escalas de Hola.
   * Un nombre y una contraseña de cuenta de administrador de hello en máquinas virtuales de Hola.
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
    "wadlogs": "<WadCfg><DiagnosticMonitorConfiguration>",
    "wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor\\PercentProcessorTime\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU percentage guest OS\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
    "wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
    "wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
    "wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
    ```

   * Los nombres DNS que se usan por hello interfaces de red.
   * Hola nombres de las direcciones IP y los prefijos de red virtual de Hola y las subredes.
   * Hello nombres e identificadores de red virtual de hello, equilibrador de carga y las interfaces de red.
   * Nombres de cuenta de almacenamiento para las cuentas de hello asociados a las máquinas de hello en el conjunto de escalas de Hola.
   * Configuración de extensión de diagnóstico que se instala en máquinas virtuales de Hola Hola. Para obtener más información acerca de la extensión de diagnósticos de hello, consulte [crear una máquina Virtual de Windows con la supervisión y diagnósticos mediante la plantilla de administrador de recursos de Azure](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

4. Agregar recurso de cuenta de almacenamiento de hello bajo el elemento primario Hola recursos que agregó toohello plantilla. Esta plantilla utiliza un hello toocreate de bucle recomendada cinco cuentas de almacenamiento donde se almacenan los discos del sistema operativo hello y datos de diagnóstico. Puede admitir este conjunto de cuentas de seguridad de máquinas virtuales de too100 en un conjunto de escala, que es el máximo actual de Hola. Cada cuenta de almacenamiento se denomina con un designador de letra que se definió en variables de hello combinadas con el sufijo de Hola que se proporciona en los parámetros de hello para la plantilla de Hola.
   
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
                "id": "[resourceId('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
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
              "backendPort": 22
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
            "publisher": "Canonical",
            "offer": "UbuntuServer",
            "sku": "14.04.4-LTS",
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

10. Agregar el recurso de conjunto de escalas de máquina virtual de Hola y especifique la extensión de diagnósticos de Hola que está instalado en todas las máquinas virtuales en el conjunto de escalas de Hola. Muchos de los valores de hello para este recurso son similares con el recurso de máquina virtual de Hola. Hola principales diferencias son elementos de la capacidad de Hola que especifica el número de Hola de máquinas virtuales en el conjunto de escalas de Hola y upgradePolicy que especifica cómo se realizan las actualizaciones toovirtual máquinas. Hello conjunto de escala no se crea hasta que se crean todas las cuentas de almacenamiento de hello según se haya especificado con el elemento dependsOn de Hola.

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
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[0],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[1],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[2],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[3],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[4],'.blob.core.windows.net/vmss')]"
              ],
              "name": "vmssosdisk",
              "caching": "ReadOnly",
              "createOption": "FromImage"
            },
            "imageReference": {
              "publisher": "Canonical",
              "offer": "UbuntuServer",
              "sku": "14.04.4-LTS",
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
                "name":"LinuxDiagnostic",
                "properties": {
                  "publisher":"Microsoft.OSTCExtensions",
                  "type":"LinuxDiagnostic",
                  "typeHandlerVersion":"2.1",
                  "autoUpgradeMinorVersion":false,
                  "settings": {
                    "xmlCfg":"[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
                    "storageAccount":"[variables('diagnosticsStorageAccountName')]"
                  },
                  "protectedSettings": {
                    "storageAccountName":"[variables('diagnosticsStorageAccountName')]",
                    "storageAccountKey":"[listkeys(variables('accountid'), '2015-06-15').key1]",
                    "storageAccountEndPoint":"https://core.windows.net"
                  }
                }
              }
            ]
          }
        }
      }
    },
    ```

11. Agregue hello autoscaleSettings recurso que define cómo se ajusta según el uso de procesador en máquinas de hello en el conjunto de Hola Hola conjunto de escala.

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
                  "metricName": "\\Processor\\PercentProcessorTime",
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
    Este valor es Hola igual que el contador de rendimiento de Hola que hemos definido en la variable de wadperfcounter Hola. Con esa variable, extensión de diagnósticos de hello recopila hello **Processor\PercentProcessorTime** contador.
    
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
    Este valor desencadena la acción de escalado de Hola. En esta plantilla, las máquinas se agregan escala toohello establecer una vez Hola uso de la CPU entre máquinas en conjunto hello más de 50%.
    
    * **dirección**  
    Este valor determina la acción de Hola que se realiza cuando se obtiene el valor de umbral de Hola. valores posibles de Hello son aumentan o disminuyen. En esta plantilla, hello número de máquinas virtuales en el conjunto de escalas de hello aumenta si el umbral de hello es más de 50% en el período de tiempo de hello definido.

    * **type**  
    Este valor es el tipo de Hola de acción que se realizarán y se debe establecer tooChangeCount.
    
    * **value**  
    Este valor es el número de Hola de máquinas virtuales que se agregan o quitan del conjunto de escalas de Hola. Este valor debe ser 1 o un valor superior. valor predeterminado de Hello es 1. En esta plantilla, Hola establece número de máquinas en escala de hello aumenta 1 cuando se alcanza el umbral de Hola.

    * **cooldown**  
    Este valor es cantidad de Hola de toowait de tiempo desde la última acción de escalado de hello antes de que se produce la acción siguiente Hola. Debe estar comprendido entre un minuto y una semana.

12. Guarde el archivo de plantilla de hello.    

## <a name="step-3-upload-hello-template-toostorage"></a>Paso 3: Cargar Hola plantilla toostorage
plantilla de Hola se puede cargar como sabe hello y clave principal de la cuenta de almacenamiento de Hola que creó en el paso 1.

1. En la interfaz de línea de comandos (intensiva de errores, Terminal, símbolo del sistema), ejecutar estos comandos tooset variables de entorno de hello necesarios tooaccess Hola cuenta de almacenamiento:

    ```cli   
    export AZURE_STORAGE_ACCOUNT={account_name}
    export AZURE_STORAGE_ACCESS_KEY={key}
    ```
    
    Puede obtener la clave de hello haciendo clic en un icono de llave Hola al ver los recursos de cuenta de almacenamiento de Hola Hola portal de Azure. Cuando use un símbolo del sistema de Windows, escriba **set** en lugar de export.

2. Crear contenedor de Hola para almacenar la plantilla de Hola.
   
    ```cli
    azure storage container create -p Blob templates
    ```

3. Cargar nuevo contenedor toohello del archivo de plantilla de Hola.
   
    ```cli
    azure storage blob upload VMSSTemplate.json templates VMSSTemplate.json
    ```

## <a name="step-4-deploy-hello-template"></a>Paso 4: Implementar la plantilla de Hola
Ahora que ha creado la plantilla de hello, puede empezar a implementar los recursos de Hola. Utilice este proceso de hello toostart de comando:

```cli
azure group deployment create --template-uri https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json vmsstestrg1 vmsstestdp1
```

Cuando se presiona escriba, son valores tooprovide solicitadas para las variables de Hola que asignó. Proporcione estos valores:

```cli
vmName: vmsstestvm1
vmSSName: vmsstest1
instanceCount: 5
adminUserName: vmadmin1
adminPassword: VMpass1
resourcePrefix: vmsstest
```

Para implementar todos los toosuccessfully de recursos de hello tardará aproximadamente 15 minutos.

> [!NOTE]
> También puede usar recursos del portal de hello capacidad toodeploy Hola. Use este vínculo: https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template>


## <a name="step-5-monitor-resources"></a>Paso 5: Supervisión de recursos
Puede obtener información acerca de los conjuntos de escala de máquinas virtuales mediante estos métodos:

* Hola portal de Azure: actualmente, puede obtener una cantidad limitada de información mediante el portal de Hola.

* Hola [Explorador de recursos de Azure](https://resources.azure.com/) -esta herramienta es más adecuado para explorar el estado actual de Hola de su conjunto de escalas de hello. Siga esta ruta de acceso y debería ver la vista de instancia de Hola de escala de hello establecido que creó:
  
    ```cli
    subscriptions > {your subscription} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines
    ```

* CLI de Azure - usar este comando tooget cierta información:

    ```cli  
    azure resource show -n vmsstest1 -r Microsoft.Compute/virtualMachineScaleSets -o 2015-06-15 -g vmsstestrg1
    ```

* Conectar máquina virtual de toohello jumpbox tal como lo haría con cualquier otro equipo y, a continuación, se pueden obtener acceso remoto a máquinas virtuales de hello en procesos individuales de hello escala conjunto toomonitor.

> [!NOTE]
> Una API de REST completa para obtener más información sobre los conjuntos de escala se puede encontrar en [Conjuntos de escala de máquinas virtuales](https://msdn.microsoft.com/library/mt589023.aspx)

## <a name="step-6-remove-hello-resources"></a>Paso 6: Quitar recursos de Hola
Dado que se le cobra por recursos que usa en Azure, siempre es un recursos toodelete recomendable que ya no son necesarios. No es necesario toodelete cada recurso por separado de un grupo de recursos. Puede eliminar el grupo de recursos de Hola y todos sus recursos se eliminan automáticamente.

```cli
azure group delete vmsstestrg1
```

## <a name="next-steps"></a>Pasos siguientes
* Encuentre ejemplos de las características de supervisión de Azure Monitor en [Ejemplos de inicio rápido de CLI multiplataforma de Azure Monitor](../monitoring-and-diagnostics/insights-cli-samples.md)
* Obtenga información sobre las características de notificación de [usar escalado automático acciones toosend correo electrónico y webhook notificaciones de alerta en el Monitor de Azure](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)
* Obtenga información acerca de cómo demasiado[toosend webhook y correo electrónico notificaciones de alerta de registros de auditoría de uso en el Monitor de Azure](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)
* Extraer del repositorio hello [aplicación de demostración de escalado automático en Ubuntu 16.04](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) plantilla que configura un hello tooexercise de aplicación de Python/bottle automática de ajuste de escala en la funcionalidad de los conjuntos de la escala en la máquina Virtual.

