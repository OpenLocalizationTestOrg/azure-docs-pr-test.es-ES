---
title: "Extensión de máquina virtual de Azure y OMS para Windows | Microsoft Docs"
description: "Implemente el agente de OMS en la máquina virtual Windows con una extensión de máquina virtual."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: feae6176-2373-4034-b5d9-a32c6b4e1f10
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: nepeters
ms.openlocfilehash: d933f488fdda0c1d37892be65f2712cf0eb5694e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="oms-virtual-machine-extension-for-windows"></a><span data-ttu-id="cad0b-103">Extensión de máquina virtual de OMS para Windows</span><span class="sxs-lookup"><span data-stu-id="cad0b-103">OMS virtual machine extension for Windows</span></span>

<span data-ttu-id="cad0b-104">Operations Management Suite (OMS) proporciona funcionalidades de corrección de alertas, supervisión y envío de alertas a todos los recursos locales y en la nube.</span><span class="sxs-lookup"><span data-stu-id="cad0b-104">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="cad0b-105">Microsoft, como editor de la extensión de máquina virtual del agente de OMS para Windows, es quien presta los servicios de soporte técnico para esta solución.</span><span class="sxs-lookup"><span data-stu-id="cad0b-105">The OMS Agent virtual machine extension for Windows is published and supported by Microsoft.</span></span> <span data-ttu-id="cad0b-106">La extensión instala al agente de OMS en máquinas virtuales de Azure e inscribe dichas máquinas virtuales en un área de trabajo de OMS existente.</span><span class="sxs-lookup"><span data-stu-id="cad0b-106">The extension installs the OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="cad0b-107">En este documento se especifican las plataformas compatibles, configuraciones y opciones de implementación de la extensión de máquina virtual de OMS para Windows.</span><span class="sxs-lookup"><span data-stu-id="cad0b-107">This document details the supported platforms, configurations, and deployment options for the OMS virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cad0b-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cad0b-108">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="cad0b-109">Sistema operativos</span><span class="sxs-lookup"><span data-stu-id="cad0b-109">Operating system</span></span>
<span data-ttu-id="cad0b-110">La extensión del agente de OMS para Windows se puede ejecutar en las versiones Windows Server 2008 R2, 2012, 2012 R2 y 2016.</span><span class="sxs-lookup"><span data-stu-id="cad0b-110">The OMS Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="cad0b-111">Conectividad de Internet</span><span class="sxs-lookup"><span data-stu-id="cad0b-111">Internet connectivity</span></span>
<span data-ttu-id="cad0b-112">La extensión del agente de OMS para Windows requiere que la máquina virtual de destino esté conectada a Internet.</span><span class="sxs-lookup"><span data-stu-id="cad0b-112">The OMS Agent extension for Windows requires that the target virtual machine is connected to the internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="cad0b-113">Esquema de extensión</span><span class="sxs-lookup"><span data-stu-id="cad0b-113">Extension schema</span></span>

<span data-ttu-id="cad0b-114">El siguiente JSON muestra el esquema para la extensión del agente de OMS.</span><span class="sxs-lookup"><span data-stu-id="cad0b-114">The following JSON shows the schema for the OMS Agent extension.</span></span> <span data-ttu-id="cad0b-115">La extensión requiere el identificador y la clave del área de trabajo de OMS de destino, que se pueden encontrar en el portal de OMS.</span><span class="sxs-lookup"><span data-stu-id="cad0b-115">The extension requires the workspace Id and workspace key from the target OMS workspace, these can be found in the OMS portal.</span></span> <span data-ttu-id="cad0b-116">Como la clave del área de trabajo debe tratarse como datos confidenciales, debe almacenarse en una configuración protegida.</span><span class="sxs-lookup"><span data-stu-id="cad0b-116">Because the workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="cad0b-117">Los datos de configuración protegida de la extensión de VM de Azure están cifrados y solo se descifran en la máquina virtual de destino.</span><span class="sxs-lookup"><span data-stu-id="cad0b-117">Azure VM extension protected setting data is encrypted, and only decrypted on the target virtual machine.</span></span> <span data-ttu-id="cad0b-118">Tenga en cuenta que **workspaceId** y **workspaceKey** distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="cad0b-118">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

```json
{
    "type": "extensions",
    "name": "OMSExtension",
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
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```
### <a name="property-values"></a><span data-ttu-id="cad0b-119">Valores de propiedad</span><span class="sxs-lookup"><span data-stu-id="cad0b-119">Property values</span></span>

| <span data-ttu-id="cad0b-120">Nombre</span><span class="sxs-lookup"><span data-stu-id="cad0b-120">Name</span></span> | <span data-ttu-id="cad0b-121">Valor / ejemplo</span><span class="sxs-lookup"><span data-stu-id="cad0b-121">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="cad0b-122">apiVersion</span><span class="sxs-lookup"><span data-stu-id="cad0b-122">apiVersion</span></span> | <span data-ttu-id="cad0b-123">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="cad0b-123">2015-06-15</span></span> |
| <span data-ttu-id="cad0b-124">publisher</span><span class="sxs-lookup"><span data-stu-id="cad0b-124">publisher</span></span> | <span data-ttu-id="cad0b-125">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="cad0b-125">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="cad0b-126">type</span><span class="sxs-lookup"><span data-stu-id="cad0b-126">type</span></span> | <span data-ttu-id="cad0b-127">MicrosoftMonitoringAgent</span><span class="sxs-lookup"><span data-stu-id="cad0b-127">MicrosoftMonitoringAgent</span></span> |
| <span data-ttu-id="cad0b-128">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="cad0b-128">typeHandlerVersion</span></span> | <span data-ttu-id="cad0b-129">1.0</span><span class="sxs-lookup"><span data-stu-id="cad0b-129">1.0</span></span> |
| <span data-ttu-id="cad0b-130">workspaceId (p.ej)</span><span class="sxs-lookup"><span data-stu-id="cad0b-130">workspaceId (e.g)</span></span> | <span data-ttu-id="cad0b-131">6f680a37-00c6-41c7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="cad0b-131">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="cad0b-132">workspaceKey (p. ej.)</span><span class="sxs-lookup"><span data-stu-id="cad0b-132">workspaceKey (e.g)</span></span> | <span data-ttu-id="cad0b-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span><span class="sxs-lookup"><span data-stu-id="cad0b-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="cad0b-134">Implementación de plantilla</span><span class="sxs-lookup"><span data-stu-id="cad0b-134">Template deployment</span></span>

<span data-ttu-id="cad0b-135">Las extensiones de VM de Azure pueden implementarse con plantillas de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cad0b-135">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="cad0b-136">El esquema JSON detallado en la sección anterior se puede usar en una plantilla de Azure Resource Manager para ejecutar el agente de OMS durante la implementación de una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cad0b-136">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the OMS Agent extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="cad0b-137">Puede encontrar una plantilla de ejemplo que incluye la extensión de VM del agente de OMS en la [Galería de inicio rápido de Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="cad0b-137">A sample template that includes the OMS Agent VM extension can be found on the [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span></span> 

<span data-ttu-id="cad0b-138">El JSON de una extensión de máquina virtual puede estar anidada en el recurso de máquina virtual, o colocada en la raíz o un nivel superior de una plantilla JSON de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cad0b-138">The JSON for a virtual machine extension can be nested inside the virtual machine resource, or placed at the root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="cad0b-139">La colocación de la plantilla JSON afecta al valor del nombre y tipo del recurso.</span><span class="sxs-lookup"><span data-stu-id="cad0b-139">The placement of the JSON affects the value of the resource name and type.</span></span> <span data-ttu-id="cad0b-140">Para obtener más información, consulte el artículo sobre cómo [establecer el nombre y el tipo de recursos secundarios](../../azure-resource-manager/resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="cad0b-140">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="cad0b-141">En el siguiente ejemplo se da por supuesto que la extensión OMS está anidada dentro de los recursos de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cad0b-141">The following example assumes the OMS extension is nested inside the virtual machine resource.</span></span> <span data-ttu-id="cad0b-142">Cuando se anidan los recursos de extensión, la plantilla JSON se coloca en el objeto `"resources": []` de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cad0b-142">When nesting the extension resource, the JSON is placed in the `"resources": []` object of the virtual machine.</span></span>


```json
{
    "type": "extensions",
    "name": "OMSExtension",
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
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

<span data-ttu-id="cad0b-143">Al colocar la plantilla JSON de la extensión en la raíz de la plantilla, el nombre de recurso incluye una referencia a la máquina virtual principal, y el tipo refleja la configuración anidada.</span><span class="sxs-lookup"><span data-stu-id="cad0b-143">When placing the extension JSON at the root of the template, the resource name includes a reference to the parent virtual machine, and the type reflects the nested configuration.</span></span> 

```json
{
    "type": "Microsoft.Compute/virtualMachines/extensions",
    "name": "<parentVmResource>/OMSExtension",
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
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

## <a name="powershell-deployment"></a><span data-ttu-id="cad0b-144">Implementación de PowerShell</span><span class="sxs-lookup"><span data-stu-id="cad0b-144">PowerShell deployment</span></span>

<span data-ttu-id="cad0b-145">El comando `Set-AzureRmVMExtension` puede utilizarse para implementar la extensión de máquina virtual del agente de OMS en una máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="cad0b-145">The `Set-AzureRmVMExtension` command can be used to deploy the OMS Agent virtual machine extension to an existing virtual machine.</span></span> <span data-ttu-id="cad0b-146">Antes de ejecutar el comando, las configuraciones públicas y privadas deben estar almacenadas en una tabla hash de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cad0b-146">Before running the command, the public and private configurations need to be stored in a PowerShell hash table.</span></span> 

```powershell
$PublicSettings = @{"workspaceId" = "myWorkspaceId"}
$ProtectedSettings = @{"workspaceKey" = "myWorkspaceKey"}

Set-AzureRmVMExtension -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
    -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" `
    -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
    -ExtensionType "MicrosoftMonitoringAgent" `
    -TypeHandlerVersion 1.0 `
    -Settings $PublicSettings `
    -ProtectedSettings $ProtectedSettings `
    -Location WestUS ` 
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="cad0b-147">Solución de problemas y soporte técnico</span><span class="sxs-lookup"><span data-stu-id="cad0b-147">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="cad0b-148">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="cad0b-148">Troubleshoot</span></span>

<span data-ttu-id="cad0b-149">Los datos sobre el estado de las implementaciones de extensiones pueden recuperarse desde Azure Portal y mediante el módulo Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cad0b-149">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure PowerShell module.</span></span> <span data-ttu-id="cad0b-150">Para ver el estado de implementación de las extensiones de una VM determinada, ejecute el comando siguiente con el módulo de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cad0b-150">To see the deployment state of extensions for a given VM, run the following command using the Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="cad0b-151">El resultado de la ejecución de las extensiones se registra en los archivos que se encuentran en el siguiente directorio:</span><span class="sxs-lookup"><span data-stu-id="cad0b-151">Extension execution output is logged to files found in the following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\
```

### <a name="support"></a><span data-ttu-id="cad0b-152">Soporte técnico</span><span class="sxs-lookup"><span data-stu-id="cad0b-152">Support</span></span>

<span data-ttu-id="cad0b-153">Si necesita más ayuda con cualquier aspecto de este artículo, puede ponerse en contacto con los expertos de Azure en los [foros de MSDN Azure o Stack Overflow](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="cad0b-153">If you need more help at any point in this article, you can contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="cad0b-154">Como alternativa, puede registrar un incidente de soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="cad0b-154">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="cad0b-155">Vaya al [sitio de soporte técnico de Azure](https://azure.microsoft.com/en-us/support/options/) y seleccione Obtener soporte.</span><span class="sxs-lookup"><span data-stu-id="cad0b-155">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="cad0b-156">Para obtener información sobre el uso del soporte técnico, lea las [Preguntas más frecuentes de soporte técnico de Microsoft Azure](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="cad0b-156">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
