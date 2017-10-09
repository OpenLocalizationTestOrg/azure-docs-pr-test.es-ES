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
# <a name="connect-azure-virtual-machines-toolog-analytics-with-a-log-analytics-agent"></a><span data-ttu-id="ad65d-104">Conectar máquinas virtuales de Azure tooLog análisis con un agente de análisis de registros</span><span class="sxs-lookup"><span data-stu-id="ad65d-104">Connect Azure virtual machines tooLog Analytics with a Log Analytics agent</span></span>

<span data-ttu-id="ad65d-105">Para equipos Windows y Linux, Hola recomienda método para recopilar registros y métricas son mediante la instalación de agente de análisis de registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad65d-105">For Windows and Linux computers, hello recommended method for collecting logs and metrics is by installing hello Log Analytics agent.</span></span>

<span data-ttu-id="ad65d-106">Hola más fácil manera tooinstall Hola análisis de registros agente en máquinas virtuales de Azure es a través de hello extensión de máquina virtual de análisis de registro.</span><span class="sxs-lookup"><span data-stu-id="ad65d-106">hello easiest way tooinstall hello Log Analytics agent on Azure virtual machines is through hello Log Analytics VM Extension.</span></span>  <span data-ttu-id="ad65d-107">Utilizando la extensión de hello simplifica el proceso de instalación de Hola y configura automáticamente Hola agente toosend datos toohello análisis de registros área de trabajo que especifique.</span><span class="sxs-lookup"><span data-stu-id="ad65d-107">Using hello extension simplifies hello installation process and automatically configures hello agent toosend data toohello Log Analytics workspace that you specify.</span></span> <span data-ttu-id="ad65d-108">agente de Hello también se actualiza automáticamente, asegurándose de que haya correcciones y características más recientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad65d-108">hello agent is also upgraded automatically, ensuring that you have hello latest features and fixes.</span></span>

<span data-ttu-id="ad65d-109">Para las máquinas virtuales de Windows, habilitar hello *Microsoft Monitoring Agent* extensión de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ad65d-109">For Windows virtual machines, you enable hello *Microsoft Monitoring Agent* virtual machine extension.</span></span>
<span data-ttu-id="ad65d-110">Para las máquinas virtuales de Linux, habilitar hello *agente de OMS para Linux* extensión de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ad65d-110">For Linux virtual machines, you enable hello *OMS Agent For Linux* virtual machine extension.</span></span>

<span data-ttu-id="ad65d-111">Obtenga más información sobre [extensiones de máquina virtual de Azure](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) hello y [agente Linux](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ad65d-111">Learn more about [Azure virtual machine extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and hello [Linux agent](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="ad65d-112">Cuando se usa la colección basada en agente para los datos de registro, debe configurar [orígenes de datos de análisis de registros](log-analytics-data-sources.md) toospecify Hola registros y las métricas que desea toocollect.</span><span class="sxs-lookup"><span data-stu-id="ad65d-112">When you use agent-based collection for log data, you must configure [data sources in Log Analytics](log-analytics-data-sources.md) toospecify hello logs and metrics that you want toocollect.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ad65d-113">Si configurar datos de registro de análisis de registros tooindex mediante [diagnósticos de Azure](log-analytics-azure-storage.md), y configurar Hola Hola de toocollect agente mismo inicia una sesión, a continuación, los registros de Hola se recopilan dos veces.</span><span class="sxs-lookup"><span data-stu-id="ad65d-113">If you configure Log Analytics tooindex log data by using [Azure diagnostics](log-analytics-azure-storage.md), and you configure hello agent toocollect hello same logs, then hello logs are collected twice.</span></span> <span data-ttu-id="ad65d-114">Se le cobrará por los dos orígenes de datos.</span><span class="sxs-lookup"><span data-stu-id="ad65d-114">You are charged for both data sources.</span></span> <span data-ttu-id="ad65d-115">Si tiene instalado el agente de hello, recopilar datos de registro mediante el agente de hello solo - no configurar datos de registro de toocollect de análisis de registros de diagnóstico de Azure.</span><span class="sxs-lookup"><span data-stu-id="ad65d-115">If you have hello agent installed, then collect log data by using only hello agent - don't configure Log Analytics toocollect log data from Azure diagnostics.</span></span>
>
>

<span data-ttu-id="ad65d-116">Hay tres maneras sencillas de extensión de máquina virtual de análisis de registros de hello tooenable:</span><span class="sxs-lookup"><span data-stu-id="ad65d-116">There are three easy ways tooenable hello Log Analytics virtual machine extension:</span></span>

* <span data-ttu-id="ad65d-117">Mediante el uso de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="ad65d-117">By using hello Azure portal</span></span>
* <span data-ttu-id="ad65d-118">Mediante Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ad65d-118">By using Azure PowerShell</span></span>
* <span data-ttu-id="ad65d-119">Mediante el uso de una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ad65d-119">By using an Azure Resource Manager template</span></span>

## <a name="enable-hello-vm-extension-in-hello-azure-portal"></a><span data-ttu-id="ad65d-120">Habilitar la extensión de máquina virtual de Hola Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="ad65d-120">Enable hello VM extension in hello Azure portal</span></span>
<span data-ttu-id="ad65d-121">Puede instalar agente de hello para el análisis de registros y conectar la máquina virtual de Azure que se ejecuta mediante el uso de Hola Hola [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ad65d-121">You can install hello agent for Log Analytics and connect hello Azure virtual machine that it runs on by using hello [Azure portal](https://portal.azure.com).</span></span>

### <a name="tooinstall-hello-log-analytics-agent-and-connect-hello-virtual-machine-tooa-log-analytics-workspace"></a><span data-ttu-id="ad65d-122">tooinstall Hola agente de análisis de registros y conecte el área de trabajo de análisis de registros de hello máquina virtual tooa</span><span class="sxs-lookup"><span data-stu-id="ad65d-122">tooinstall hello Log Analytics agent and connect hello virtual machine tooa Log Analytics workspace</span></span>
1. <span data-ttu-id="ad65d-123">Inicio de sesión en hello [portal de Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ad65d-123">Sign into hello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="ad65d-124">Seleccione **examinar** en hello lado izquierdo de hello portal y, a continuación, vaya demasiado**Log Analytics (OMS)** y selecciónelo.</span><span class="sxs-lookup"><span data-stu-id="ad65d-124">Select **Browse** on hello left side of hello portal, and then go too**Log Analytics (OMS)** and select it.</span></span>
3. <span data-ttu-id="ad65d-125">En la lista de áreas de trabajo de análisis de registros, seleccione Hola uno que desea toouse con hello VM de Azure.</span><span class="sxs-lookup"><span data-stu-id="ad65d-125">In your list of Log Analytics workspaces, select hello one that you want toouse with hello Azure VM.</span></span>  
   ![Áreas de trabajo de OMS](./media/log-analytics-azure-vm-extension/oms-connect-azure-01.png)
4. <span data-ttu-id="ad65d-127">En **Log analytics management** (Administración de Log Analytics), seleccione **Máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="ad65d-127">Under **Log analytics management**, select **Virtual machines**.</span></span>  
   <span data-ttu-id="ad65d-128">![Máquinas virtuales](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span><span class="sxs-lookup"><span data-stu-id="ad65d-128">![Virtual machines](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span></span>
5. <span data-ttu-id="ad65d-129">En la lista de Hola de **máquinas virtuales**, seleccione Hola máquina virtual en el que desea que el agente de hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="ad65d-129">In hello list of **Virtual machines**, select hello virtual machine on which you want tooinstall hello agent.</span></span> <span data-ttu-id="ad65d-130">Hola **estado de la conexión de OMS** para hello VM indica que se está **no conectado**.</span><span class="sxs-lookup"><span data-stu-id="ad65d-130">hello **OMS connection status** for hello VM indicates that it is **Not connected**.</span></span>  
   <span data-ttu-id="ad65d-131">![VM no conectada](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span><span class="sxs-lookup"><span data-stu-id="ad65d-131">![VM not connected](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span></span>
6. <span data-ttu-id="ad65d-132">En detalles de hello para la máquina virtual, seleccione **conectar**.</span><span class="sxs-lookup"><span data-stu-id="ad65d-132">In hello details for your virtual machine, select **Connect**.</span></span> <span data-ttu-id="ad65d-133">agente Hola automáticamente está instalado y configurado para el área de trabajo de análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="ad65d-133">hello agent is automatically installed and configured for your Log Analytics workspace.</span></span> <span data-ttu-id="ad65d-134">Este proceso tarda unos minutos, durante el cual hello estado de la conexión de OMS es *conexión...*</span><span class="sxs-lookup"><span data-stu-id="ad65d-134">This process takes a few minutes, during which time hello OMS Connection status is *Connecting...*</span></span>  
   <span data-ttu-id="ad65d-135">![Conectar VM](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span><span class="sxs-lookup"><span data-stu-id="ad65d-135">![Connect VM](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span></span>
7. <span data-ttu-id="ad65d-136">Después de instalar y conecta el agente de hello, Hola **conexión a OMS** estado será actualizada tooshow **esta área de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="ad65d-136">After you install and connect hello agent, hello **OMS connection** status will be updated tooshow **This workspace**.</span></span>  
   <span data-ttu-id="ad65d-137">![Conectada](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span><span class="sxs-lookup"><span data-stu-id="ad65d-137">![Connected](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span></span>

## <a name="enable-hello-vm-extension-using-powershell"></a><span data-ttu-id="ad65d-138">Habilitar la extensión de máquina virtual de hello mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="ad65d-138">Enable hello VM extension using PowerShell</span></span>
<span data-ttu-id="ad65d-139">Cuando se configura la máquina virtual mediante PowerShell, necesita hello tooprovide **workspaceId** y **workspaceKey**.</span><span class="sxs-lookup"><span data-stu-id="ad65d-139">When you configure your virtual machine by using PowerShell, you need tooprovide hello **workspaceId** and **workspaceKey**.</span></span> <span data-ttu-id="ad65d-140">nombres de propiedad de Hello en la configuración de json son **entre mayúsculas y minúsculas**.</span><span class="sxs-lookup"><span data-stu-id="ad65d-140">hello property names in your json configuration are **case-sensitive**.</span></span>

<span data-ttu-id="ad65d-141">Puede encontrar Hola Id. y clave en hello **configuración** página de portal de OMS de hello, o mediante el uso de PowerShell como se muestra en el anterior ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad65d-141">You can find hello Id and key on hello **Settings** page of hello OMS portal, or by using PowerShell as shown in hello preceding example.</span></span>

![Identificador de área de trabajo y clave principal](./media/log-analytics-azure-vm-extension/oms-analyze-azure-sources.png)

<span data-ttu-id="ad65d-143">Hay comandos diferentes para máquinas virtuales clásicas de Azure y máquinas virtuales de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ad65d-143">There are different commands for Azure classic virtual machines and Resource Manager virtual machines.</span></span> <span data-ttu-id="ad65d-144">A continuación se incluyen ejemplos para máquinas virtuales clásicas y de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ad65d-144">Following are examples for both classic and Resource Manager virtual machines.</span></span>

<span data-ttu-id="ad65d-145">Para máquinas virtuales clásicas, use Hola siguiente ejemplo de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ad65d-145">For classic virtual machines, use hello following PowerShell example:</span></span>

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

<span data-ttu-id="ad65d-146">Para máquinas virtuales de Linux de administrador de recursos mediante Hola después CLI</span><span class="sxs-lookup"><span data-stu-id="ad65d-146">For Resource Manager Linux VMs using hello following CLI</span></span>
```azurecli
az vm extension set --resource-group myRGMonitor --vm-name myMonitorVM --name OmsAgentForLinux --publisher Microsoft.EnterpriseCloud.Monitoring --version 1.3 --protected-settings ‘{"workspaceKey": "<workspace-key>"}’ --settings ‘{"workspaceId": "<workspace-id>"}’ 
```

<span data-ttu-id="ad65d-147">Para las máquinas virtuales de administrador de recursos, utilice Hola siguiente ejemplo de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ad65d-147">For Resource Manager virtual machines, use hello following PowerShell example:</span></span>

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


## <a name="deploy-hello-vm-extension-using-a-template"></a><span data-ttu-id="ad65d-148">Implementar la extensión de máquina virtual de hello mediante una plantilla</span><span class="sxs-lookup"><span data-stu-id="ad65d-148">Deploy hello VM extension using a template</span></span>
<span data-ttu-id="ad65d-149">Mediante el Administrador de recursos de Azure, puede crear una plantilla (en formato JSON) que define la implementación de Hola y la configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ad65d-149">By using Azure Resource Manager, you can create a template (in JSON format) that defines hello deployment and configuration of your application.</span></span> <span data-ttu-id="ad65d-150">Esta plantilla se conoce como una plantilla de administrador de recursos y proporciona una implementación de toodefine de manera declarativa.</span><span class="sxs-lookup"><span data-stu-id="ad65d-150">This template is known as a Resource Manager template and provides a declarative way toodefine deployment.</span></span> <span data-ttu-id="ad65d-151">Mediante una plantilla, puede implementar la aplicación a lo largo del ciclo de vida de aplicación Hola repetidamente y estar seguro de que se están implementando los recursos en un estado coherente.</span><span class="sxs-lookup"><span data-stu-id="ad65d-151">By using a template, you can repeatedly deploy your application throughout hello app lifecycle and have confidence that your resources are being deployed in a consistent state.</span></span>

<span data-ttu-id="ad65d-152">Mediante la inclusión de agente de análisis de registros de hello como parte de la plantilla de administrador de recursos, puede asegurarse de que cada máquina virtual es el área de trabajo de análisis de registros de tooyour de tooreport configuradas previamente.</span><span class="sxs-lookup"><span data-stu-id="ad65d-152">By including hello Log Analytics agent as part of your Resource Manager template, you can ensure that each virtual machine is pre-configured tooreport tooyour Log Analytics workspace.</span></span>

<span data-ttu-id="ad65d-153">Para más información sobre las plantillas de Resource Manager, consulte [Creación de plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ad65d-153">For more information about Resource Manager templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="ad65d-154">Aquí te mostramos un ejemplo de una plantilla de administrador de recursos que se usa para implementar una máquina virtual que ejecuta Windows con hello extensión del agente de supervisión de Microsoft instalado.</span><span class="sxs-lookup"><span data-stu-id="ad65d-154">Following is an example of a Resource Manager template that's used for deploying a virtual machine that's running Windows with hello Microsoft Monitoring Agent extension installed.</span></span> <span data-ttu-id="ad65d-155">Esta plantilla es una plantilla de máquina virtual típico, con hello siguientes adiciones:</span><span class="sxs-lookup"><span data-stu-id="ad65d-155">This template is a typical virtual machine template, with hello following additions:</span></span>

* <span data-ttu-id="ad65d-156">Parámetros workspaceId y workspaceName</span><span class="sxs-lookup"><span data-stu-id="ad65d-156">workspaceId and workspaceName parameters</span></span>
* <span data-ttu-id="ad65d-157">Sección de extensión de recursos Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="ad65d-157">Microsoft.EnterpriseCloud.Monitoring resource extension section</span></span>
* <span data-ttu-id="ad65d-158">Salidas toolook hello workspaceId y workspaceSharedKey</span><span class="sxs-lookup"><span data-stu-id="ad65d-158">Outputs toolook up hello workspaceId and workspaceSharedKey</span></span>

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

<span data-ttu-id="ad65d-159">Puede implementar una plantilla mediante Hola siguiente comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ad65d-159">You can deploy a template by using hello following PowerShell command:</span></span>

```PowerShell
New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath
```

## <a name="troubleshooting-hello-log-analytics-vm-extension"></a><span data-ttu-id="ad65d-160">Solución de problemas de extensión de máquina virtual de análisis de registro de hello</span><span class="sxs-lookup"><span data-stu-id="ad65d-160">Troubleshooting hello Log Analytics VM extension</span></span>
<span data-ttu-id="ad65d-161">Normalmente, cuando algo no funciona bien, recibe un mensaje desde Azure Portal o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ad65d-161">Usually you receive a message when things don't work, from either Azure portal or Azure powershell.</span></span>

1. <span data-ttu-id="ad65d-162">Inicio de sesión en hello [portal de Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ad65d-162">Sign into hello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="ad65d-163">Buscar Hola VM y abrir los detalles de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ad65d-163">Find hello VM and open VM details.</span></span>
3. <span data-ttu-id="ad65d-164">Haga clic en **extensiones** toocheck si la extensión OMS está habilitado o no.</span><span class="sxs-lookup"><span data-stu-id="ad65d-164">Click **Extensions** toocheck if OMS extension is enabled or not.</span></span>

   ![Vista de la extensión de máquina virtual](./media/log-analytics-azure-vm-extension/oms-vmview-extensions.png)

4. <span data-ttu-id="ad65d-166">Haga clic en hello *MicrosoftMonitoringAgent*(Windows) o *OmsAgentForLinux*(Linux) extensión y ver los detalles.</span><span class="sxs-lookup"><span data-stu-id="ad65d-166">Click hello *MicrosoftMonitoringAgent*(Windows) or *OmsAgentForLinux*(Linux) extension and view details.</span></span> 

   ![Detalles de la extensión de máquina virtual](./media/log-analytics-azure-vm-extension/oms-vmview-extensiondetails.png)

### <a name="troubleshooting-windows-virtual-machines"></a><span data-ttu-id="ad65d-168">Solución de problemas con máquinas virtuales Windows</span><span class="sxs-lookup"><span data-stu-id="ad65d-168">Troubleshooting Windows Virtual Machines</span></span>
<span data-ttu-id="ad65d-169">Si hello *Microsoft Monitoring Agent* no está instalando la extensión del agente VM o informes, puede realizar Hola siguiendo el problema de pasos tootroubleshoot Hola.</span><span class="sxs-lookup"><span data-stu-id="ad65d-169">If hello *Microsoft Monitoring Agent* VM agent extension is not installing or reporting, you can perform hello following steps tootroubleshoot hello issue.</span></span>

1. <span data-ttu-id="ad65d-170">Compruebe si está instalado el agente de máquina virtual de Azure de Hola y los pasos de trabajo correctamente mediante el uso de Hola de [2965986 KB](https://support.microsoft.com/kb/2965986#mt1).</span><span class="sxs-lookup"><span data-stu-id="ad65d-170">Check if hello Azure VM agent is installed and working correctly by using hello steps in [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).</span></span>
   * <span data-ttu-id="ad65d-171">También puede revisar el archivo de registro de agente VM de Hola`C:\WindowsAzure\logs\WaAppAgent.log`</span><span class="sxs-lookup"><span data-stu-id="ad65d-171">You can also review hello VM agent log file `C:\WindowsAzure\logs\WaAppAgent.log`</span></span>
   * <span data-ttu-id="ad65d-172">Si no existe registro de hello, no está instalado el agente de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad65d-172">If hello log does not exist, hello VM agent is not installed.</span></span>
     * [<span data-ttu-id="ad65d-173">Instalar Hola agente de máquina virtual de Azure en máquinas virtuales clásicas</span><span class="sxs-lookup"><span data-stu-id="ad65d-173">Install hello Azure VM Agent on classic VMs</span></span>](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
2. <span data-ttu-id="ad65d-174">Confirmar Hola el agente de supervisión de Microsoft está ejecutando tarea de latido de extensión utilizando Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="ad65d-174">Confirm hello Microsoft Monitoring Agent extension heartbeat task is running using hello following steps:</span></span>
   * <span data-ttu-id="ad65d-175">Inicie sesión en la máquina virtual de toohello</span><span class="sxs-lookup"><span data-stu-id="ad65d-175">Log in toohello virtual machine</span></span>
   * <span data-ttu-id="ad65d-176">Abra el programador de tareas y busque hello `update_azureoperationalinsight_agent_heartbeat` tarea</span><span class="sxs-lookup"><span data-stu-id="ad65d-176">Open task scheduler and find hello `update_azureoperationalinsight_agent_heartbeat` task</span></span>
   * <span data-ttu-id="ad65d-177">Confirme la tarea hello está habilitado y ejecuta cada minuto</span><span class="sxs-lookup"><span data-stu-id="ad65d-177">Confirm hello task is enabled and is running every one minute</span></span>
   * <span data-ttu-id="ad65d-178">Compruebe el archivo de registro de hello latido`C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span><span class="sxs-lookup"><span data-stu-id="ad65d-178">Check hello heartbeat logfile in `C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span></span>
3. <span data-ttu-id="ad65d-179">Revise los archivos de registro de extensión de máquina virtual de agente de supervisión de Microsoft de hello en`C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span><span class="sxs-lookup"><span data-stu-id="ad65d-179">Review hello Microsoft Monitoring Agent VM extension log files in `C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span></span>
4. <span data-ttu-id="ad65d-180">Asegúrese de máquina virtual de hello puede ejecutar scripts de PowerShell</span><span class="sxs-lookup"><span data-stu-id="ad65d-180">Ensure hello virtual machine can run PowerShell scripts</span></span>
5. <span data-ttu-id="ad65d-181">Asegúrese de que no se hayan modificado los permisos en C:\Windows\temp.</span><span class="sxs-lookup"><span data-stu-id="ad65d-181">Ensure permissions on C:\Windows\temp haven’t been changed</span></span>
6. <span data-ttu-id="ad65d-182">Ver el estado de Hola de hello Microsoft Monitoring Agent para ello, escriba el siguiente comando en una ventana de PowerShell con privilegios elevados en la máquina virtual de Hola de Hola`  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span><span class="sxs-lookup"><span data-stu-id="ad65d-182">View hello status of hello Microsoft Monitoring Agent by typing hello following command in an elevated PowerShell window on hello virtual machine `  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span></span>
7. <span data-ttu-id="ad65d-183">Revise los archivos de registro de instalación de Microsoft Monitoring Agent de hello en`C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span><span class="sxs-lookup"><span data-stu-id="ad65d-183">Review hello Microsoft Monitoring Agent setup log files in `C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span></span>

<span data-ttu-id="ad65d-184">Para más información, consulte [Solución de problemas de la extensión de máquina virtual de Microsoft Azure](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ad65d-184">For more information, see [troubleshooting Windows extensions](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="troubleshooting-linux-virtual-machines"></a><span data-ttu-id="ad65d-185">Solución de problemas con máquinas virtuales Linux</span><span class="sxs-lookup"><span data-stu-id="ad65d-185">Troubleshooting Linux Virtual Machines</span></span>
<span data-ttu-id="ad65d-186">Si hello *agente de OMS para Linux* no está instalando la extensión del agente VM o informes, puede realizar Hola siguiendo el problema de pasos tootroubleshoot Hola.</span><span class="sxs-lookup"><span data-stu-id="ad65d-186">If hello *OMS Agent for Linux* VM agent extension is not installing or reporting, you can perform hello following steps tootroubleshoot hello issue.</span></span>

1. <span data-ttu-id="ad65d-187">Si el estado de la extensión de hello es *desconocido* comprueba si está instalado el agente de máquina virtual de Azure de Hola y funciona correctamente, revise el archivo de registro de agente VM de Hola`/var/log/waagent.log`</span><span class="sxs-lookup"><span data-stu-id="ad65d-187">If hello extension status is *Unknown* check if hello Azure VM agent is installed and working correctly by reviewing hello VM agent log file `/var/log/waagent.log`</span></span>
   * <span data-ttu-id="ad65d-188">Si no existe registro de hello, no está instalado el agente de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad65d-188">If hello log does not exist, hello VM agent is not installed.</span></span>
   * [<span data-ttu-id="ad65d-189">Instalar Hola agente de máquina virtual de Azure en máquinas virtuales de Linux</span><span class="sxs-lookup"><span data-stu-id="ad65d-189">Install hello Azure VM Agent on Linux VMs</span></span>](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. <span data-ttu-id="ad65d-190">Para otros Estados incorrecto, revisión hello agente de OMS para extensión de VM de Linux archivos de registro `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` y`/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span><span class="sxs-lookup"><span data-stu-id="ad65d-190">For other unhealthy statuses, review hello OMS Agent for Linux VM extension logs files in `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` and `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span></span>
3. <span data-ttu-id="ad65d-191">Si el estado de extensión hello es correcto, pero no se está cargando datos revise Hola agente de OMS para Linux archivos de registro`/var/opt/microsoft/omsagent/log/omsagent.log`</span><span class="sxs-lookup"><span data-stu-id="ad65d-191">If hello extension status is healthy, but data is not being uploaded review hello OMS Agent for Linux log files in `/var/opt/microsoft/omsagent/log/omsagent.log`</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad65d-192">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ad65d-192">Next steps</span></span>
* <span data-ttu-id="ad65d-193">Configurar [orígenes de datos de análisis de registros](log-analytics-data-sources.md) toospecify toocollect de registros y las métricas de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad65d-193">Configure [data sources in Log Analytics](log-analytics-data-sources.md) toospecify hello logs and metrics toocollect.</span></span>
* <span data-ttu-id="ad65d-194">datos de toogather de máquinas virtuales [soluciones de análisis de registro agregar desde la Galería de soluciones de hello](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="ad65d-194">toogather data from virtual machines [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
* <span data-ttu-id="ad65d-195">[Recopile datos con Diagnósticos de Azure](log-analytics-azure-storage.md) para otros recursos que se ejecutan en Azure.</span><span class="sxs-lookup"><span data-stu-id="ad65d-195">[Collect data by using Azure Diagnostics](log-analytics-azure-storage.md) for other resources that are running in Azure.</span></span>

<span data-ttu-id="ad65d-196">Para los equipos que no están en Azure, puede instalar a agente de análisis de registros de hello mediante métodos de Hola que se describen en los siguientes artículos de hello:</span><span class="sxs-lookup"><span data-stu-id="ad65d-196">For computers that are not in Azure, you can install hello Log Analytics agent by using hello methods that are described in hello following articles:</span></span>

* [<span data-ttu-id="ad65d-197">Conectar los equipos de Windows tooLog análisis</span><span class="sxs-lookup"><span data-stu-id="ad65d-197">Connect Windows computers tooLog Analytics</span></span>](log-analytics-windows-agents.md)
* [<span data-ttu-id="ad65d-198">Conectar los equipos de Linux tooLog análisis</span><span class="sxs-lookup"><span data-stu-id="ad65d-198">Connect Linux computers tooLog Analytics</span></span>](log-analytics-linux-agents.md)
