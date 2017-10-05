---
title: "Conexión de máquinas virtuales de Azure a Log Analytics | Microsoft Docs"
description: "Para máquinas virtuales de Windows y Linux que se ejecutan en Azure, se recomienda instalar la extensión de máquina virtual de Azure de Log Analytics para recopilar registros y métricas. Puede usar Azure Portal o PowerShell para instalar la extensión de máquina virtual de Log Analytics en VM de Azure."
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
ms.openlocfilehash: cdae291b546fef4d7fdb8b067c8e4f4c9708d43f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="connect-azure-virtual-machines-to-log-analytics-with-a-log-analytics-agent"></a><span data-ttu-id="6125c-104">Conexión de máquinas virtuales de Azure al agente de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="6125c-104">Connect Azure virtual machines to Log Analytics with a Log Analytics agent</span></span>

<span data-ttu-id="6125c-105">En equipos Windows y Linux, para recopilar registros y métricas se recomienda instalar el agente de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="6125c-105">For Windows and Linux computers, the recommended method for collecting logs and metrics is by installing the Log Analytics agent.</span></span>

<span data-ttu-id="6125c-106">Para instalar al agente de Log Analytics en máquinas virtuales de Azure, lo más sencillo es utilizar la extensión de máquina virtual de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="6125c-106">The easiest way to install the Log Analytics agent on Azure virtual machines is through the Log Analytics VM Extension.</span></span>  <span data-ttu-id="6125c-107">El uso de una extensión simplifica el proceso de instalación y configura automáticamente el agente para enviar datos al área de trabajo de Log Analytics que especifique.</span><span class="sxs-lookup"><span data-stu-id="6125c-107">Using the extension simplifies the installation process and automatically configures the agent to send data to the Log Analytics workspace that you specify.</span></span> <span data-ttu-id="6125c-108">El agente también se actualiza automáticamente, garantizando así que disponga de las características y correcciones más recientes.</span><span class="sxs-lookup"><span data-stu-id="6125c-108">The agent is also upgraded automatically, ensuring that you have the latest features and fixes.</span></span>

<span data-ttu-id="6125c-109">Para máquinas virtuales Windows, debe habilitar la extensión de máquina virtual *Microsoft Monitoring Agent*.</span><span class="sxs-lookup"><span data-stu-id="6125c-109">For Windows virtual machines, you enable the *Microsoft Monitoring Agent* virtual machine extension.</span></span>
<span data-ttu-id="6125c-110">Para máquinas virtuales Linux, debe habilitar la extensión de máquina virtual *Agente de OMS para Linux*.</span><span class="sxs-lookup"><span data-stu-id="6125c-110">For Linux virtual machines, you enable the *OMS Agent For Linux* virtual machine extension.</span></span>

<span data-ttu-id="6125c-111">Obtenga más información sobre las [extensiones de máquina virtual de Azure](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) y el [Agente Linux](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6125c-111">Learn more about [Azure virtual machine extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and the [Linux agent](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="6125c-112">Cuando se usa una recopilación basada en agente para los datos de registro, debe configurar [orígenes de datos en Log Analytics](log-analytics-data-sources.md) para especificar los registros y las métricas que desea recopilar.</span><span class="sxs-lookup"><span data-stu-id="6125c-112">When you use agent-based collection for log data, you must configure [data sources in Log Analytics](log-analytics-data-sources.md) to specify the logs and metrics that you want to collect.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6125c-113">Si configura Log Analytics para indexar los datos de registro mediante [Diagnósticos de Azure](log-analytics-azure-storage.md) y configura el agente para recopilar los mismos registros, los registros se recopilan dos veces.</span><span class="sxs-lookup"><span data-stu-id="6125c-113">If you configure Log Analytics to index log data by using [Azure diagnostics](log-analytics-azure-storage.md), and you configure the agent to collect the same logs, then the logs are collected twice.</span></span> <span data-ttu-id="6125c-114">Se le cobrará por los dos orígenes de datos.</span><span class="sxs-lookup"><span data-stu-id="6125c-114">You are charged for both data sources.</span></span> <span data-ttu-id="6125c-115">Si tiene instalado el agente, recopile datos de registro solo mediante el agente; no configure Log Analytics para recopilar datos de registro de diagnósticos de Azure.</span><span class="sxs-lookup"><span data-stu-id="6125c-115">If you have the agent installed, then collect log data by using only the agent - don't configure Log Analytics to collect log data from Azure diagnostics.</span></span>
>
>

<span data-ttu-id="6125c-116">Existen tres maneras sencillas de habilitar la extensión de la máquina virtual de Log Analytics:</span><span class="sxs-lookup"><span data-stu-id="6125c-116">There are three easy ways to enable the Log Analytics virtual machine extension:</span></span>

* <span data-ttu-id="6125c-117">Mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="6125c-117">By using the Azure portal</span></span>
* <span data-ttu-id="6125c-118">Mediante Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6125c-118">By using Azure PowerShell</span></span>
* <span data-ttu-id="6125c-119">Mediante el uso de una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6125c-119">By using an Azure Resource Manager template</span></span>

## <a name="enable-the-vm-extension-in-the-azure-portal"></a><span data-ttu-id="6125c-120">Habilitación de la extensión de máquina virtual en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6125c-120">Enable the VM extension in the Azure portal</span></span>
<span data-ttu-id="6125c-121">Puede instalar el agente para Log Analytics y conectar la máquina virtual de Azure donde se ejecuta mediante [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6125c-121">You can install the agent for Log Analytics and connect the Azure virtual machine that it runs on by using the [Azure portal](https://portal.azure.com).</span></span>

### <a name="to-install-the-log-analytics-agent-and-connect-the-virtual-machine-to-a-log-analytics-workspace"></a><span data-ttu-id="6125c-122">Para instalar al agente de Log Analytics y conectar la máquina virtual a un área de trabajo de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="6125c-122">To install the Log Analytics agent and connect the virtual machine to a Log Analytics workspace</span></span>
1. <span data-ttu-id="6125c-123">Inicie sesión en el [Portal de Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6125c-123">Sign into the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="6125c-124">Seleccione **Examinar** en el lado izquierdo del portal y, a continuación, vaya a **Log Analytics (OMS)** y selecciónelo.</span><span class="sxs-lookup"><span data-stu-id="6125c-124">Select **Browse** on the left side of the portal, and then go to **Log Analytics (OMS)** and select it.</span></span>
3. <span data-ttu-id="6125c-125">En la lista de áreas de trabajo de Log Analytics, seleccione el área que desea usar con la máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="6125c-125">In your list of Log Analytics workspaces, select the one that you want to use with the Azure VM.</span></span>  
   ![Áreas de trabajo de OMS](./media/log-analytics-azure-vm-extension/oms-connect-azure-01.png)
4. <span data-ttu-id="6125c-127">En **Log analytics management** (Administración de Log Analytics), seleccione **Máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="6125c-127">Under **Log analytics management**, select **Virtual machines**.</span></span>  
   <span data-ttu-id="6125c-128">![Máquinas virtuales](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span><span class="sxs-lookup"><span data-stu-id="6125c-128">![Virtual machines](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span></span>
5. <span data-ttu-id="6125c-129">En la lista de **máquinas virtuales**, seleccione la máquina virtual donde desea instalar el agente.</span><span class="sxs-lookup"><span data-stu-id="6125c-129">In the list of **Virtual machines**, select the virtual machine on which you want to install the agent.</span></span> <span data-ttu-id="6125c-130">El **estado de la conexión de OMS** de la máquina virtual indica que **no está conectado**.</span><span class="sxs-lookup"><span data-stu-id="6125c-130">The **OMS connection status** for the VM indicates that it is **Not connected**.</span></span>  
   <span data-ttu-id="6125c-131">![VM no conectada](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span><span class="sxs-lookup"><span data-stu-id="6125c-131">![VM not connected](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span></span>
6. <span data-ttu-id="6125c-132">En los detalles de la máquina virtual, seleccione **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="6125c-132">In the details for your virtual machine, select **Connect**.</span></span> <span data-ttu-id="6125c-133">El agente se instala y se configura automáticamente para el área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="6125c-133">The agent is automatically installed and configured for your Log Analytics workspace.</span></span> <span data-ttu-id="6125c-134">Este proceso tarda unos minutos, durante los que el estado de conexión de OMS indica que se está *conectando*.</span><span class="sxs-lookup"><span data-stu-id="6125c-134">This process takes a few minutes, during which time the OMS Connection status is *Connecting...*</span></span>  
   <span data-ttu-id="6125c-135">![Conectar VM](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span><span class="sxs-lookup"><span data-stu-id="6125c-135">![Connect VM](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span></span>
7. <span data-ttu-id="6125c-136">Cuando el agente esté instalado y conectado, el estado de la **conexión de OMS** se actualizará para mostrar **This workspace** (Esta área de trabajo).</span><span class="sxs-lookup"><span data-stu-id="6125c-136">After you install and connect the agent, the **OMS connection** status will be updated to show **This workspace**.</span></span>  
   <span data-ttu-id="6125c-137">![Conectada](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span><span class="sxs-lookup"><span data-stu-id="6125c-137">![Connected](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span></span>

## <a name="enable-the-vm-extension-using-powershell"></a><span data-ttu-id="6125c-138">Habilitación de la extensión de máquina virtual con PowerShell</span><span class="sxs-lookup"><span data-stu-id="6125c-138">Enable the VM extension using PowerShell</span></span>
<span data-ttu-id="6125c-139">Al configurar la máquina virtual con PowerShell, es necesario proporcionar el **identificador del área de trabajo** y la **clave del área de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="6125c-139">When you configure your virtual machine by using PowerShell, you need to provide the **workspaceId** and **workspaceKey**.</span></span> <span data-ttu-id="6125c-140">Los nombres de propiedad de la configuración de json **distinguen entre mayúsculas y minúsculas**.</span><span class="sxs-lookup"><span data-stu-id="6125c-140">The property names in your json configuration are **case-sensitive**.</span></span>

<span data-ttu-id="6125c-141">Puede encontrar la clave principal y el identificador en la página **Configuración** del portal de OMS. También puede usar PowerShell como se ilustra en el ejemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="6125c-141">You can find the Id and key on the **Settings** page of the OMS portal, or by using PowerShell as shown in the preceding example.</span></span>

![Identificador de área de trabajo y clave principal](./media/log-analytics-azure-vm-extension/oms-analyze-azure-sources.png)

<span data-ttu-id="6125c-143">Hay comandos diferentes para máquinas virtuales clásicas de Azure y máquinas virtuales de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6125c-143">There are different commands for Azure classic virtual machines and Resource Manager virtual machines.</span></span> <span data-ttu-id="6125c-144">A continuación se incluyen ejemplos para máquinas virtuales clásicas y de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6125c-144">Following are examples for both classic and Resource Manager virtual machines.</span></span>

<span data-ttu-id="6125c-145">En el caso de las máquinas virtuales clásicas, use el siguiente ejemplo de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6125c-145">For classic virtual machines, use the following PowerShell example:</span></span>

```PowerShell
Add-AzureAccount

$workspaceId = "enter workspace ID here"
$workspaceKey = "enter workspace key here"
$hostedService = "enter hosted service here"

$vm = Get-AzureVM –ServiceName $hostedService

# For Windows VM uncomment the following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'MicrosoftMonitoringAgent' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose

# For Linux VM uncomment the following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'OmsAgentForLinux' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose
```

<span data-ttu-id="6125c-146">Para VM con Linux de Resource Manager que usan la CLI siguiente</span><span class="sxs-lookup"><span data-stu-id="6125c-146">For Resource Manager Linux VMs using the following CLI</span></span>
```azurecli
az vm extension set --resource-group myRGMonitor --vm-name myMonitorVM --name OmsAgentForLinux --publisher Microsoft.EnterpriseCloud.Monitoring --version 1.3 --protected-settings ‘{"workspaceKey": "<workspace-key>"}’ --settings ‘{"workspaceId": "<workspace-id>"}’ 
```

<span data-ttu-id="6125c-147">En el caso de las máquinas virtuales de Resource Manager, use el siguiente ejemplo de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6125c-147">For Resource Manager virtual machines, use the following PowerShell example:</span></span>

```PowerShell
Login-AzureRMAccount
Select-AzureRMSubscription -SubscriptionId "**"

$workspaceName = "your workspace name"
$VMresourcegroup = "**"
$VMresourcename = "**"

$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq $workspaceName})

if ($workspace.Name -ne $workspaceName)
{
    Write-Error "Unable to find OMS Workspace $workspaceName. Do you need to run Select-AzureRMSubscription?"
}

$workspaceId = $workspace.CustomerId
$workspaceKey = (Get-AzureRmOperationalInsightsWorkspaceSharedKeys -ResourceGroupName $workspace.ResourceGroupName -Name $workspace.Name).PrimarySharedKey

$vm = Get-AzureRmVM -ResourceGroupName $VMresourcegroup -Name $VMresourcename
$location = $vm.Location

# For Windows VM uncomment the following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'MicrosoftMonitoringAgent' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'MicrosoftMonitoringAgent' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"

# For Linux VM uncomment the following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'OmsAgentForLinux' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'OmsAgentForLinux' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"


```


## <a name="deploy-the-vm-extension-using-a-template"></a><span data-ttu-id="6125c-148">Implementación de la extensión de máquina virtual mediante una plantilla</span><span class="sxs-lookup"><span data-stu-id="6125c-148">Deploy the VM extension using a template</span></span>
<span data-ttu-id="6125c-149">Con Azure Resource Manager, puede crear una plantilla (en formato JSON) que defina la implementación y configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6125c-149">By using Azure Resource Manager, you can create a template (in JSON format) that defines the deployment and configuration of your application.</span></span> <span data-ttu-id="6125c-150">Esta plantilla se conoce como plantilla de Administrador de recursos y proporciona una manera declarativa de definir la implementación.</span><span class="sxs-lookup"><span data-stu-id="6125c-150">This template is known as a Resource Manager template and provides a declarative way to define deployment.</span></span> <span data-ttu-id="6125c-151">El uso de una plantilla permite implementar la aplicación repetidamente a lo largo del ciclo de vida de esta y tener la seguridad de que los recursos se implementan de forma coherente.</span><span class="sxs-lookup"><span data-stu-id="6125c-151">By using a template, you can repeatedly deploy your application throughout the app lifecycle and have confidence that your resources are being deployed in a consistent state.</span></span>

<span data-ttu-id="6125c-152">La inclusión del agente de Log Analytics como parte de la plantilla de Resource Manager le permite garantizar que todas las máquinas virtuales estén preconfiguradas para informar al área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="6125c-152">By including the Log Analytics agent as part of your Resource Manager template, you can ensure that each virtual machine is pre-configured to report to your Log Analytics workspace.</span></span>

<span data-ttu-id="6125c-153">Para más información sobre las plantillas de Resource Manager, consulte [Creación de plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6125c-153">For more information about Resource Manager templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="6125c-154">A continuación se incluye un ejemplo de una plantilla de Resource Manager que se utiliza para la implementación de una máquina virtual que ejecuta Windows con la extensión Microsoft Monitoring Agent instalada.</span><span class="sxs-lookup"><span data-stu-id="6125c-154">Following is an example of a Resource Manager template that's used for deploying a virtual machine that's running Windows with the Microsoft Monitoring Agent extension installed.</span></span> <span data-ttu-id="6125c-155">Se trata de una plantilla de máquina virtual típica, con las siguientes adiciones:</span><span class="sxs-lookup"><span data-stu-id="6125c-155">This template is a typical virtual machine template, with the following additions:</span></span>

* <span data-ttu-id="6125c-156">Parámetros workspaceId y workspaceName</span><span class="sxs-lookup"><span data-stu-id="6125c-156">workspaceId and workspaceName parameters</span></span>
* <span data-ttu-id="6125c-157">Sección de extensión de recursos Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="6125c-157">Microsoft.EnterpriseCloud.Monitoring resource extension section</span></span>
* <span data-ttu-id="6125c-158">Salidas para buscar workspaceId y workspaceSharedKey</span><span class="sxs-lookup"><span data-stu-id="6125c-158">Outputs to look up the workspaceId and workspaceSharedKey</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adminUsername": {
      "type": "string",
      "metadata": {
        "description": "Username for the Virtual Machine."
      }
    },
    "adminPassword": {
      "type": "securestring",
      "metadata": {
        "description": "Password for the Virtual Machine."
      }
    },
    "dnsLabelPrefix": {
       "type": "string",
       "metadata": {
          "description": "DNS Label for the Public IP. Must be lowercase. It should match with the following regular expression: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$ or it will raise an error."
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
        "description": "The Windows version for the VM. This will pick a fully patched image of this given Windows version. Allowed values: 2008-R2-SP1, 2012-Datacenter, 2012-R2-Datacenter, Windows-Server-Technical-Preview."
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

<span data-ttu-id="6125c-159">Puede implementar una plantilla mediante el siguiente comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6125c-159">You can deploy a template by using the following PowerShell command:</span></span>

```PowerShell
New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath
```

## <a name="troubleshooting-the-log-analytics-vm-extension"></a><span data-ttu-id="6125c-160">Solución de problemas de la extensión de máquina virtual de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="6125c-160">Troubleshooting the Log Analytics VM extension</span></span>
<span data-ttu-id="6125c-161">Normalmente, cuando algo no funciona bien, recibe un mensaje desde Azure Portal o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6125c-161">Usually you receive a message when things don't work, from either Azure portal or Azure powershell.</span></span>

1. <span data-ttu-id="6125c-162">Inicie sesión en el [Portal de Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6125c-162">Sign into the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="6125c-163">Busque la máquina virtual y abra sus detalles.</span><span class="sxs-lookup"><span data-stu-id="6125c-163">Find the VM and open VM details.</span></span>
3. <span data-ttu-id="6125c-164">Haga clic en **Extensiones** para comprobar si la extensión OMS está habilitada o no.</span><span class="sxs-lookup"><span data-stu-id="6125c-164">Click **Extensions** to check if OMS extension is enabled or not.</span></span>

   ![Vista de la extensión de máquina virtual](./media/log-analytics-azure-vm-extension/oms-vmview-extensions.png)

4. <span data-ttu-id="6125c-166">Haga clic en la extensión *MicrosoftMonitoringAgent* (Windows) o *OmsAgentForLinux* (Linux) y vea los detalles.</span><span class="sxs-lookup"><span data-stu-id="6125c-166">Click the *MicrosoftMonitoringAgent*(Windows) or *OmsAgentForLinux*(Linux) extension and view details.</span></span> 

   ![Detalles de la extensión de máquina virtual](./media/log-analytics-azure-vm-extension/oms-vmview-extensiondetails.png)

### <a name="troubleshooting-windows-virtual-machines"></a><span data-ttu-id="6125c-168">Solución de problemas con máquinas virtuales Windows</span><span class="sxs-lookup"><span data-stu-id="6125c-168">Troubleshooting Windows Virtual Machines</span></span>
<span data-ttu-id="6125c-169">Si la extensión del agente de VM *Microsoft Monitoring Agent* no se instala o no envía informes, puede realizar los pasos siguientes para solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="6125c-169">If the *Microsoft Monitoring Agent* VM agent extension is not installing or reporting, you can perform the following steps to troubleshoot the issue.</span></span>

1. <span data-ttu-id="6125c-170">Siga los pasos de [KB 2965986](https://support.microsoft.com/kb/2965986#mt1) para comprobar que el agente de máquina virtual de Azure está instalado y funciona correctamente.</span><span class="sxs-lookup"><span data-stu-id="6125c-170">Check if the Azure VM agent is installed and working correctly by using the steps in [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).</span></span>
   * <span data-ttu-id="6125c-171">También puede revisar el archivo de registro del agente de máquina virtual `C:\WindowsAzure\logs\WaAppAgent.log`</span><span class="sxs-lookup"><span data-stu-id="6125c-171">You can also review the VM agent log file `C:\WindowsAzure\logs\WaAppAgent.log`</span></span>
   * <span data-ttu-id="6125c-172">Si el registro no existe, el agente de máquina virtual no estará instalado.</span><span class="sxs-lookup"><span data-stu-id="6125c-172">If the log does not exist, the VM agent is not installed.</span></span>
     * [<span data-ttu-id="6125c-173">Instale el agente de máquina virtual de Azure en máquinas virtuales de Azure clásicas.</span><span class="sxs-lookup"><span data-stu-id="6125c-173">Install the Azure VM Agent on classic VMs</span></span>](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
2. <span data-ttu-id="6125c-174">Confirme que se está ejecutando la tarea de latido de la extensión de Microsoft Monitoring Agent mediante los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="6125c-174">Confirm the Microsoft Monitoring Agent extension heartbeat task is running using the following steps:</span></span>
   * <span data-ttu-id="6125c-175">Inicie sesión en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6125c-175">Log in to the virtual machine</span></span>
   * <span data-ttu-id="6125c-176">Abra el programador de tareas y busque la tarea `update_azureoperationalinsight_agent_heartbeat`.</span><span class="sxs-lookup"><span data-stu-id="6125c-176">Open task scheduler and find the `update_azureoperationalinsight_agent_heartbeat` task</span></span>
   * <span data-ttu-id="6125c-177">Confirme que la tarea está habilitada y se ejecuta cada minuto.</span><span class="sxs-lookup"><span data-stu-id="6125c-177">Confirm the task is enabled and is running every one minute</span></span>
   * <span data-ttu-id="6125c-178">Consulte el archivo de registro de latido en `C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`.</span><span class="sxs-lookup"><span data-stu-id="6125c-178">Check the heartbeat logfile in `C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span></span>
3. <span data-ttu-id="6125c-179">Revise los archivos de registro de la extensión de máquina virtual de Microsoft Monitoring Agent en `C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`.</span><span class="sxs-lookup"><span data-stu-id="6125c-179">Review the Microsoft Monitoring Agent VM extension log files in `C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span></span>
4. <span data-ttu-id="6125c-180">Asegúrese de que la máquina virtual puede ejecutar scripts de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6125c-180">Ensure the virtual machine can run PowerShell scripts</span></span>
5. <span data-ttu-id="6125c-181">Asegúrese de que no se hayan modificado los permisos en C:\Windows\temp.</span><span class="sxs-lookup"><span data-stu-id="6125c-181">Ensure permissions on C:\Windows\temp haven’t been changed</span></span>
6. <span data-ttu-id="6125c-182">Consulte el estado de Microsoft Monitoring Agent, para lo que debe escribir el siguiente comando en una ventana de PowerShell con privilegios elevados en la máquina virtual `  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`.</span><span class="sxs-lookup"><span data-stu-id="6125c-182">View the status of the Microsoft Monitoring Agent by typing the following command in an elevated PowerShell window on the virtual machine `  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span></span>
7. <span data-ttu-id="6125c-183">Revise los archivos de registro de instalación de Microsoft Monitoring Agent en `C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`.</span><span class="sxs-lookup"><span data-stu-id="6125c-183">Review the Microsoft Monitoring Agent setup log files in `C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span></span>

<span data-ttu-id="6125c-184">Para más información, consulte [Solución de problemas de la extensión de máquina virtual de Microsoft Azure](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6125c-184">For more information, see [troubleshooting Windows extensions](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="troubleshooting-linux-virtual-machines"></a><span data-ttu-id="6125c-185">Solución de problemas con máquinas virtuales Linux</span><span class="sxs-lookup"><span data-stu-id="6125c-185">Troubleshooting Linux Virtual Machines</span></span>
<span data-ttu-id="6125c-186">Si la extensión del agente de VM *Agente de OMS para Linux* no se instala o no envía informes, puede realizar los pasos siguientes para solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="6125c-186">If the *OMS Agent for Linux* VM agent extension is not installing or reporting, you can perform the following steps to troubleshoot the issue.</span></span>

1. <span data-ttu-id="6125c-187">Si el estado de la extensión es *desconocido*, compruebe si el agente de máquina virtual de Azure está instalado y funciona correctamente revisando el archivo de registro del agente de máquina virtual `/var/log/waagent.log`.</span><span class="sxs-lookup"><span data-stu-id="6125c-187">If the extension status is *Unknown* check if the Azure VM agent is installed and working correctly by reviewing the VM agent log file `/var/log/waagent.log`</span></span>
   * <span data-ttu-id="6125c-188">Si el registro no existe, el agente de máquina virtual no estará instalado.</span><span class="sxs-lookup"><span data-stu-id="6125c-188">If the log does not exist, the VM agent is not installed.</span></span>
   * [<span data-ttu-id="6125c-189">Instale el agente de máquina virtual de Azure en máquinas virtuales Linux.</span><span class="sxs-lookup"><span data-stu-id="6125c-189">Install the Azure VM Agent on Linux VMs</span></span>](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. <span data-ttu-id="6125c-190">Para otros estados incorrectos, revise los archivos de registro de extensión de máquina virtual del Agente de OMS para Linux en `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` y `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`.</span><span class="sxs-lookup"><span data-stu-id="6125c-190">For other unhealthy statuses, review the OMS Agent for Linux VM extension logs files in `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` and `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span></span>
3. <span data-ttu-id="6125c-191">Si el estado de la extensión es correcto, pero no se están cargando datos, revise los archivos de registro del Agente de OMS para Linux en `/var/opt/microsoft/omsagent/log/omsagent.log`.</span><span class="sxs-lookup"><span data-stu-id="6125c-191">If the extension status is healthy, but data is not being uploaded review the OMS Agent for Linux log files in `/var/opt/microsoft/omsagent/log/omsagent.log`</span></span>

## <a name="next-steps"></a><span data-ttu-id="6125c-192">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6125c-192">Next steps</span></span>
* <span data-ttu-id="6125c-193">Configure [orígenes de datos de Log Analytics](log-analytics-data-sources.md) para especificar los registros y las métricas que desea recopilar.</span><span class="sxs-lookup"><span data-stu-id="6125c-193">Configure [data sources in Log Analytics](log-analytics-data-sources.md) to specify the logs and metrics to collect.</span></span>
* <span data-ttu-id="6125c-194">Para recopilar datos de máquinas virtuales, [incorpore soluciones de Log Analytics desde la galería de soluciones](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="6125c-194">To gather data from virtual machines [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
* <span data-ttu-id="6125c-195">[Recopile datos con Diagnósticos de Azure](log-analytics-azure-storage.md) para otros recursos que se ejecutan en Azure.</span><span class="sxs-lookup"><span data-stu-id="6125c-195">[Collect data by using Azure Diagnostics](log-analytics-azure-storage.md) for other resources that are running in Azure.</span></span>

<span data-ttu-id="6125c-196">Para equipos que no se ejecutan en Azure, puede instalar el agente de Log Analytics mediante los métodos descritos en los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="6125c-196">For computers that are not in Azure, you can install the Log Analytics agent by using the methods that are described in the following articles:</span></span>

* [<span data-ttu-id="6125c-197">Conexión de equipos Windows a Log Analytics</span><span class="sxs-lookup"><span data-stu-id="6125c-197">Connect Windows computers to Log Analytics</span></span>](log-analytics-windows-agents.md)
* [<span data-ttu-id="6125c-198">Conexión de equipos Linux a Log Analytics</span><span class="sxs-lookup"><span data-stu-id="6125c-198">Connect Linux computers to Log Analytics</span></span>](log-analytics-linux-agents.md)
