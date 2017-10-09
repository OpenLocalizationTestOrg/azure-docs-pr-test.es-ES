---
title: "máquinas virtuales de Azure de aaaConnect tooLog análisis | Documentos de Microsoft"
description: "Para Windows y Linux máquinas virtuales que se ejecutan en Azure, Hola recomienda manera de recopilados registros y métricas son instalar la extensión de máquina virtual de Azure de análisis de registro de hello. Puede usar Hola portal de Azure o PowerShell tooinstall Hola extensión de máquina virtual de análisis de registros en máquinas virtuales de Azure."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: ca39e586-a6af-42fe-862e-80978a58d9b1
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: richrund
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac96c242d03ed3a22ca96368e5a8cc53f9a993db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-azure-virtual-machines-toolog-analytics-with-a-log-analytics-agent"></a>Conectar máquinas virtuales de Azure tooLog análisis con un agente de análisis de registros

Para equipos Windows y Linux, Hola recomienda método para recopilar registros y métricas son mediante la instalación de agente de análisis de registros de Hola.

Hola más fácil manera tooinstall Hola análisis de registros agente en máquinas virtuales de Azure es a través de hello extensión de máquina virtual de análisis de registro.  Utilizando la extensión de hello simplifica el proceso de instalación de Hola y configura automáticamente Hola agente toosend datos toohello análisis de registros área de trabajo que especifique. agente de Hello también se actualiza automáticamente, asegurándose de que haya correcciones y características más recientes de Hola.

Para las máquinas virtuales de Windows, habilitar hello *Microsoft Monitoring Agent* extensión de máquina virtual.
Para las máquinas virtuales de Linux, habilitar hello *agente de OMS para Linux* extensión de máquina virtual.

Obtenga más información sobre [extensiones de máquina virtual de Azure](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) hello y [agente Linux](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Cuando se usa la colección basada en agente para los datos de registro, debe configurar [orígenes de datos de análisis de registros](log-analytics-data-sources.md) toospecify Hola registros y las métricas que desea toocollect.

> [!IMPORTANT]
> Si configurar datos de registro de análisis de registros tooindex mediante [diagnósticos de Azure](log-analytics-azure-storage.md), y configurar Hola Hola de toocollect agente mismo inicia una sesión, a continuación, los registros de Hola se recopilan dos veces. Se le cobrará por los dos orígenes de datos. Si tiene instalado el agente de hello, recopilar datos de registro mediante el agente de hello solo - no configurar datos de registro de toocollect de análisis de registros de diagnóstico de Azure.
>
>

Hay tres maneras sencillas de extensión de máquina virtual de análisis de registros de hello tooenable:

* Mediante el uso de hello portal de Azure
* Mediante Azure PowerShell.
* Mediante el uso de una plantilla de Azure Resource Manager.

## <a name="enable-hello-vm-extension-in-hello-azure-portal"></a>Habilitar la extensión de máquina virtual de Hola Hola portal de Azure
Puede instalar agente de hello para el análisis de registros y conectar la máquina virtual de Azure que se ejecuta mediante el uso de Hola Hola [portal de Azure](https://portal.azure.com).

### <a name="tooinstall-hello-log-analytics-agent-and-connect-hello-virtual-machine-tooa-log-analytics-workspace"></a>tooinstall Hola agente de análisis de registros y conecte el área de trabajo de análisis de registros de hello máquina virtual tooa
1. Inicio de sesión en hello [portal de Azure](http://portal.azure.com).
2. Seleccione **examinar** en hello lado izquierdo de hello portal y, a continuación, vaya demasiado**Log Analytics (OMS)** y selecciónelo.
3. En la lista de áreas de trabajo de análisis de registros, seleccione Hola uno que desea toouse con hello VM de Azure.  
   ![Áreas de trabajo de OMS](./media/log-analytics-azure-vm-extension/oms-connect-azure-01.png)
4. En **Log analytics management** (Administración de Log Analytics), seleccione **Máquinas virtuales**.  
   ![Máquinas virtuales](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)
5. En la lista de Hola de **máquinas virtuales**, seleccione Hola máquina virtual en el que desea que el agente de hello tooinstall. Hola **estado de la conexión de OMS** para hello VM indica que se está **no conectado**.  
   ![VM no conectada](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)
6. En detalles de hello para la máquina virtual, seleccione **conectar**. agente Hola automáticamente está instalado y configurado para el área de trabajo de análisis de registros. Este proceso tarda unos minutos, durante el cual hello estado de la conexión de OMS es *conexión...*  
   ![Conectar VM](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)
7. Después de instalar y conecta el agente de hello, Hola **conexión a OMS** estado será actualizada tooshow **esta área de trabajo**.  
   ![Conectada](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)

## <a name="enable-hello-vm-extension-using-powershell"></a>Habilitar la extensión de máquina virtual de hello mediante PowerShell
Cuando se configura la máquina virtual mediante PowerShell, necesita hello tooprovide **workspaceId** y **workspaceKey**. nombres de propiedad de Hello en la configuración de json son **entre mayúsculas y minúsculas**.

Puede encontrar Hola Id. y clave en hello **configuración** página de portal de OMS de hello, o mediante el uso de PowerShell como se muestra en el anterior ejemplo de Hola.

![Identificador de área de trabajo y clave principal](./media/log-analytics-azure-vm-extension/oms-analyze-azure-sources.png)

Hay comandos diferentes para máquinas virtuales clásicas de Azure y máquinas virtuales de Resource Manager. A continuación se incluyen ejemplos para máquinas virtuales clásicas y de Resource Manager.

Para máquinas virtuales clásicas, use Hola siguiente ejemplo de PowerShell:

```PowerShell
Add-AzureAccount

$workspaceId = "enter workspace ID here"
$workspaceKey = "enter workspace key here"
$hostedService = "enter hosted service here"

$vm = Get-AzureVM –ServiceName $hostedService

# For Windows VM uncomment hello following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'MicrosoftMonitoringAgent' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose

# For Linux VM uncomment hello following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'OmsAgentForLinux' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose
```

Para máquinas virtuales de Linux de administrador de recursos mediante Hola después CLI
```azurecli
az vm extension set --resource-group myRGMonitor --vm-name myMonitorVM --name OmsAgentForLinux --publisher Microsoft.EnterpriseCloud.Monitoring --version 1.3 --protected-settings ‘{"workspaceKey": "<workspace-key>"}’ --settings ‘{"workspaceId": "<workspace-id>"}’ 
```

Para las máquinas virtuales de administrador de recursos, utilice Hola siguiente ejemplo de PowerShell:

```PowerShell
Login-AzureRMAccount
Select-AzureRMSubscription -SubscriptionId "**"

$workspaceName = "your workspace name"
$VMresourcegroup = "**"
$VMresourcename = "**"

$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq $workspaceName})

if ($workspace.Name -ne $workspaceName)
{
    Write-Error "Unable toofind OMS Workspace $workspaceName. Do you need toorun Select-AzureRMSubscription?"
}

$workspaceId = $workspace.CustomerId
$workspaceKey = (Get-AzureRmOperationalInsightsWorkspaceSharedKeys -ResourceGroupName $workspace.ResourceGroupName -Name $workspace.Name).PrimarySharedKey

$vm = Get-AzureRmVM -ResourceGroupName $VMresourcegroup -Name $VMresourcename
$location = $vm.Location

# For Windows VM uncomment hello following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'MicrosoftMonitoringAgent' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'MicrosoftMonitoringAgent' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"

# For Linux VM uncomment hello following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'OmsAgentForLinux' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'OmsAgentForLinux' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"


```


## <a name="deploy-hello-vm-extension-using-a-template"></a>Implementar la extensión de máquina virtual de hello mediante una plantilla
Mediante el Administrador de recursos de Azure, puede crear una plantilla (en formato JSON) que define la implementación de Hola y la configuración de la aplicación. Esta plantilla se conoce como una plantilla de administrador de recursos y proporciona una implementación de toodefine de manera declarativa. Mediante una plantilla, puede implementar la aplicación a lo largo del ciclo de vida de aplicación Hola repetidamente y estar seguro de que se están implementando los recursos en un estado coherente.

Mediante la inclusión de agente de análisis de registros de hello como parte de la plantilla de administrador de recursos, puede asegurarse de que cada máquina virtual es el área de trabajo de análisis de registros de tooyour de tooreport configuradas previamente.

Para más información sobre las plantillas de Resource Manager, consulte [Creación de plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

Aquí te mostramos un ejemplo de una plantilla de administrador de recursos que se usa para implementar una máquina virtual que ejecuta Windows con hello extensión del agente de supervisión de Microsoft instalado. Esta plantilla es una plantilla de máquina virtual típico, con hello siguientes adiciones:

* Parámetros workspaceId y workspaceName
* Sección de extensión de recursos Microsoft.EnterpriseCloud.Monitoring
* Salidas toolook hello workspaceId y workspaceSharedKey

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adminUsername": {
      "type": "string",
      "metadata": {
        "description": "Username for hello Virtual Machine."
      }
    },
    "adminPassword": {
      "type": "securestring",
      "metadata": {
        "description": "Password for hello Virtual Machine."
      }
    },
    "dnsLabelPrefix": {
       "type": "string",
       "metadata": {
          "description": "DNS Label for hello Public IP. Must be lowercase. It should match with hello following regular expression: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$ or it will raise an error."
       }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "OMS workspace ID"
      }
    },
    "workspaceName": {
      "type": "string",
      "metadata": {
         "description": "OMS workspace name"
      }
    },
    "windowsOSVersion": {
      "type": "string",
      "defaultValue": "2012-R2-Datacenter",
      "allowedValues": [
        "2008-R2-SP1",
        "2012-Datacenter",
        "2012-R2-Datacenter",
        "Windows-Server-Technical-Preview"
      ],
      "metadata": {
        "description": "hello Windows version for hello VM. This will pick a fully patched image of this given Windows version. Allowed values: 2008-R2-SP1, 2012-Datacenter, 2012-R2-Datacenter, Windows-Server-Technical-Preview."
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]",
    "apiVersion": "2015-06-15",
    "imagePublisher": "MicrosoftWindowsServer",
    "imageOffer": "WindowsServer",
    "OSDiskName": "osdiskforwindowssimple",
    "nicName": "myVMNic",
    "addressPrefix": "10.0.0.0/16",
    "subnetName": "Subnet",
    "subnetPrefix": "10.0.0.0/24",
    "storageAccountType": "Standard_LRS",
    "publicIPAddressName": "myPublicIP",
    "publicIPAddressType": "Dynamic",
    "vmStorageAccountContainerName": "vhds",
    "vmName": "MyWindowsVM",
    "vmSize": "Standard_DS1",
    "virtualNetworkName": "MyVNET",
    "resourceId": "[resourceGroup().id]",
    "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
    "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "[variables('apiVersion')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "accountType": "[variables('storageAccountType')]"
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIPAddressName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
        "dnsSettings": {
          "domainNameLabel": "[parameters('dnsLabelPrefix')]"
        }
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": {
          "addressPrefixes": [
            "[variables('addressPrefix')]"
          ]
        },
        "subnets": [
          {
            "name": "[variables('subnetName')]",
            "properties": {
              "addressPrefix": "[variables('subnetPrefix')]"
            }
          }
        ]
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
              },
              "subnet": {
                "id": "[variables('subnetRef')]"
              }
            }
          }
        ]
      }
    },
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[variables('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": {
          "vmSize": "[variables('vmSize')]"
        },
        "osProfile": {
          "computername": "[variables('vmName')]",
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "[variables('imagePublisher')]",
            "offer": "[variables('imageOffer')]",
            "sku": "[parameters('windowsOSVersion')]",
            "version": "latest"
          },
          "osDisk": {
            "name": "osdisk",
            "vhd": {
              "uri": "[concat('http://',variables('storageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/',variables('OSDiskName'),'.vhd')]"
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
        },
        "diagnosticsProfile": {
          "bootDiagnostics": {
             "enabled": "true",
             "storageUri": "[concat('http://',variables('storageAccountName'),'.blob.core.windows.net')]"
          }
        }
      },
      "resources": [
        {
          "type": "extensions",
          "name": "Microsoft.EnterpriseCloud.Monitoring",
          "apiVersion": "[variables('apiVersion')]",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
          ],
          "properties": {
            "publisher": "Microsoft.EnterpriseCloud.Monitoring",
            "type": "MicrosoftMonitoringAgent",
            "typeHandlerVersion": "1.0",
            "autoUpgradeMinorVersion": true,
            "settings": {
              "workspaceId": "[parameters('workspaceId')]"
            },
            "protectedSettings": {
              "workspaceKey": "[listKeys(resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspaceName')), '2015-03-20').primarySharedKey]"
            }
          }
        }
      ]
    }
  ],
  "outputs": {
      "sharedKeyOutput": {
         "value": "[listKeys(resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-03-20').primarySharedKey]",
         "type": "string"
      },
      "workspaceIdOutput": {
         "value": "[reference(concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-03-20').customerId]",
        "type" : "string"
      }
  }
}
```

Puede implementar una plantilla mediante Hola siguiente comando de PowerShell:

```PowerShell
New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath
```

## <a name="troubleshooting-hello-log-analytics-vm-extension"></a>Solución de problemas de extensión de máquina virtual de análisis de registro de hello
Normalmente, cuando algo no funciona bien, recibe un mensaje desde Azure Portal o Azure PowerShell.

1. Inicio de sesión en hello [portal de Azure](http://portal.azure.com).
2. Buscar Hola VM y abrir los detalles de la máquina virtual.
3. Haga clic en **extensiones** toocheck si la extensión OMS está habilitado o no.

   ![Vista de la extensión de máquina virtual](./media/log-analytics-azure-vm-extension/oms-vmview-extensions.png)

4. Haga clic en hello *MicrosoftMonitoringAgent*(Windows) o *OmsAgentForLinux*(Linux) extensión y ver los detalles. 

   ![Detalles de la extensión de máquina virtual](./media/log-analytics-azure-vm-extension/oms-vmview-extensiondetails.png)

### <a name="troubleshooting-windows-virtual-machines"></a>Solución de problemas con máquinas virtuales Windows
Si hello *Microsoft Monitoring Agent* no está instalando la extensión del agente VM o informes, puede realizar Hola siguiendo el problema de pasos tootroubleshoot Hola.

1. Compruebe si está instalado el agente de máquina virtual de Azure de Hola y los pasos de trabajo correctamente mediante el uso de Hola de [2965986 KB](https://support.microsoft.com/kb/2965986#mt1).
   * También puede revisar el archivo de registro de agente VM de Hola`C:\WindowsAzure\logs\WaAppAgent.log`
   * Si no existe registro de hello, no está instalado el agente de máquina virtual de Hola.
     * [Instalar Hola agente de máquina virtual de Azure en máquinas virtuales clásicas](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
2. Confirmar Hola el agente de supervisión de Microsoft está ejecutando tarea de latido de extensión utilizando Hola pasos:
   * Inicie sesión en la máquina virtual de toohello
   * Abra el programador de tareas y busque hello `update_azureoperationalinsight_agent_heartbeat` tarea
   * Confirme la tarea hello está habilitado y ejecuta cada minuto
   * Compruebe el archivo de registro de hello latido`C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`
3. Revise los archivos de registro de extensión de máquina virtual de agente de supervisión de Microsoft de hello en`C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`
4. Asegúrese de máquina virtual de hello puede ejecutar scripts de PowerShell
5. Asegúrese de que no se hayan modificado los permisos en C:\Windows\temp.
6. Ver el estado de Hola de hello Microsoft Monitoring Agent para ello, escriba el siguiente comando en una ventana de PowerShell con privilegios elevados en la máquina virtual de Hola de Hola`  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`
7. Revise los archivos de registro de instalación de Microsoft Monitoring Agent de hello en`C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`

Para más información, consulte [Solución de problemas de la extensión de máquina virtual de Microsoft Azure](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="troubleshooting-linux-virtual-machines"></a>Solución de problemas con máquinas virtuales Linux
Si hello *agente de OMS para Linux* no está instalando la extensión del agente VM o informes, puede realizar Hola siguiendo el problema de pasos tootroubleshoot Hola.

1. Si el estado de la extensión de hello es *desconocido* comprueba si está instalado el agente de máquina virtual de Azure de Hola y funciona correctamente, revise el archivo de registro de agente VM de Hola`/var/log/waagent.log`
   * Si no existe registro de hello, no está instalado el agente de máquina virtual de Hola.
   * [Instalar Hola agente de máquina virtual de Azure en máquinas virtuales de Linux](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. Para otros Estados incorrecto, revisión hello agente de OMS para extensión de VM de Linux archivos de registro `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` y`/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`
3. Si el estado de extensión hello es correcto, pero no se está cargando datos revise Hola agente de OMS para Linux archivos de registro`/var/opt/microsoft/omsagent/log/omsagent.log`

## <a name="next-steps"></a>Pasos siguientes
* Configurar [orígenes de datos de análisis de registros](log-analytics-data-sources.md) toospecify toocollect de registros y las métricas de Hola.
* datos de toogather de máquinas virtuales [soluciones de análisis de registro agregar desde la Galería de soluciones de hello](log-analytics-add-solutions.md).
* [Recopile datos con Diagnósticos de Azure](log-analytics-azure-storage.md) para otros recursos que se ejecutan en Azure.

Para los equipos que no están en Azure, puede instalar a agente de análisis de registros de hello mediante métodos de Hola que se describen en los siguientes artículos de hello:

* [Conectar los equipos de Windows tooLog análisis](log-analytics-windows-agents.md)
* [Conectar los equipos de Linux tooLog análisis](log-analytics-linux-agents.md)
