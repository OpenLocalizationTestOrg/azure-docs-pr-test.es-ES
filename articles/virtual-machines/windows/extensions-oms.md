---
title: "extensión de máquina virtual de Azure para Windows aaaOMS | Documentos de Microsoft"
description: "Implementar el agente de OMS de hello en la máquina virtual de Windows con una extensión de máquina virtual."
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
ms.openlocfilehash: 3000f66c0acdec1d1fad2125b8c6b72a92b1ec92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-windows"></a><span data-ttu-id="831ba-103">Extensión de máquina virtual de OMS para Windows</span><span class="sxs-lookup"><span data-stu-id="831ba-103">OMS virtual machine extension for Windows</span></span>

<span data-ttu-id="831ba-104">Operations Management Suite (OMS) proporciona funcionalidades de corrección de alertas, supervisión y envío de alertas a todos los recursos locales y en la nube.</span><span class="sxs-lookup"><span data-stu-id="831ba-104">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="831ba-105">extensión de máquina virtual de agente de OMS para Windows Hello se publica y compatible con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="831ba-105">hello OMS Agent virtual machine extension for Windows is published and supported by Microsoft.</span></span> <span data-ttu-id="831ba-106">extensión de Hello instala el agente OMS de hello en máquinas virtuales de Azure e inscribe máquinas virtuales en un área de trabajo OMS existente.</span><span class="sxs-lookup"><span data-stu-id="831ba-106">hello extension installs hello OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="831ba-107">Este Hola de detalles de documento admite plataformas, configuraciones y opciones de implementación para hello extensión de máquina virtual OMS para Windows.</span><span class="sxs-lookup"><span data-stu-id="831ba-107">This document details hello supported platforms, configurations, and deployment options for hello OMS virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="831ba-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="831ba-108">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="831ba-109">Sistema operativos</span><span class="sxs-lookup"><span data-stu-id="831ba-109">Operating system</span></span>
<span data-ttu-id="831ba-110">Hola extensión del agente de OMS para Windows se pueden ejecutar en Windows Server 2008 R2, 2012, 2012 R2 y 2016 libera.</span><span class="sxs-lookup"><span data-stu-id="831ba-110">hello OMS Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="831ba-111">Conectividad de Internet</span><span class="sxs-lookup"><span data-stu-id="831ba-111">Internet connectivity</span></span>
<span data-ttu-id="831ba-112">extensión del agente de OMS para Windows Hello requiere esa máquina virtual de destino de hello es toohello conectado internet.</span><span class="sxs-lookup"><span data-stu-id="831ba-112">hello OMS Agent extension for Windows requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="831ba-113">Esquema de extensión</span><span class="sxs-lookup"><span data-stu-id="831ba-113">Extension schema</span></span>

<span data-ttu-id="831ba-114">Hello JSON siguiente muestra esquema Hola Hola extensión del agente de OMS.</span><span class="sxs-lookup"><span data-stu-id="831ba-114">hello following JSON shows hello schema for hello OMS Agent extension.</span></span> <span data-ttu-id="831ba-115">extensión de Hello requiere Hola área de trabajo área de trabajo y el identificador de clave de área de trabajo OMS de destino de hello, estos pueden encontrarse en el portal de OMS Hola.</span><span class="sxs-lookup"><span data-stu-id="831ba-115">hello extension requires hello workspace Id and workspace key from hello target OMS workspace, these can be found in hello OMS portal.</span></span> <span data-ttu-id="831ba-116">Porque la clave de área de trabajo de hello debe tratarse como datos confidenciales, se deben almacenar en una configuración protegida.</span><span class="sxs-lookup"><span data-stu-id="831ba-116">Because hello workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="831ba-117">Datos de configuración de extensión protegido de VM de Azure cifrados y solo descifrados en la máquina virtual de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="831ba-117">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span> <span data-ttu-id="831ba-118">Tenga en cuenta que **workspaceId** y **workspaceKey** distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="831ba-118">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

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
### <a name="property-values"></a><span data-ttu-id="831ba-119">Valores de propiedad</span><span class="sxs-lookup"><span data-stu-id="831ba-119">Property values</span></span>

| <span data-ttu-id="831ba-120">Nombre</span><span class="sxs-lookup"><span data-stu-id="831ba-120">Name</span></span> | <span data-ttu-id="831ba-121">Valor / ejemplo</span><span class="sxs-lookup"><span data-stu-id="831ba-121">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="831ba-122">apiVersion</span><span class="sxs-lookup"><span data-stu-id="831ba-122">apiVersion</span></span> | <span data-ttu-id="831ba-123">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="831ba-123">2015-06-15</span></span> |
| <span data-ttu-id="831ba-124">publisher</span><span class="sxs-lookup"><span data-stu-id="831ba-124">publisher</span></span> | <span data-ttu-id="831ba-125">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="831ba-125">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="831ba-126">type</span><span class="sxs-lookup"><span data-stu-id="831ba-126">type</span></span> | <span data-ttu-id="831ba-127">MicrosoftMonitoringAgent</span><span class="sxs-lookup"><span data-stu-id="831ba-127">MicrosoftMonitoringAgent</span></span> |
| <span data-ttu-id="831ba-128">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="831ba-128">typeHandlerVersion</span></span> | <span data-ttu-id="831ba-129">1.0</span><span class="sxs-lookup"><span data-stu-id="831ba-129">1.0</span></span> |
| <span data-ttu-id="831ba-130">workspaceId (p.ej)</span><span class="sxs-lookup"><span data-stu-id="831ba-130">workspaceId (e.g)</span></span> | <span data-ttu-id="831ba-131">6f680a37-00c6-41c7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="831ba-131">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="831ba-132">workspaceKey (p. ej.)</span><span class="sxs-lookup"><span data-stu-id="831ba-132">workspaceKey (e.g)</span></span> | <span data-ttu-id="831ba-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span><span class="sxs-lookup"><span data-stu-id="831ba-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="831ba-134">Implementación de plantilla</span><span class="sxs-lookup"><span data-stu-id="831ba-134">Template deployment</span></span>

<span data-ttu-id="831ba-135">Las extensiones de VM de Azure pueden implementarse con plantillas de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="831ba-135">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="831ba-136">esquema JSON de Hello detallado en la sección anterior de hello puede usarse en un hello toorun de plantilla de Azure Resource Manager extensión del agente de OMS durante la implementación de plantilla Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="831ba-136">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello OMS Agent extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="831ba-137">Una plantilla de ejemplo que incluye la extensión de máquina virtual de agente de OMS de hello puede encontrarse en hello [Galería de inicio rápido de Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="831ba-137">A sample template that includes hello OMS Agent VM extension can be found on hello [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span></span> 

<span data-ttu-id="831ba-138">Hola JSON para una extensión de máquina virtual puede anidada dentro de recurso de la máquina virtual de hello, o se coloca en la raíz de Hola o de nivel superior de una plantilla JSON del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="831ba-138">hello JSON for a virtual machine extension can be nested inside hello virtual machine resource, or placed at hello root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="831ba-139">selección de ubicación de Hola de hello JSON afecta al valor de Hola de nombre de recurso de Hola y el tipo.</span><span class="sxs-lookup"><span data-stu-id="831ba-139">hello placement of hello JSON affects hello value of hello resource name and type.</span></span> <span data-ttu-id="831ba-140">Para obtener más información, consulte el artículo sobre cómo [establecer el nombre y el tipo de recursos secundarios](../../azure-resource-manager/resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="831ba-140">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="831ba-141">Hello en el ejemplo siguiente se supone extensión OMS Hola está anidada dentro de recurso de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="831ba-141">hello following example assumes hello OMS extension is nested inside hello virtual machine resource.</span></span> <span data-ttu-id="831ba-142">Cuando se anidan los recursos de extensión de hello, Hola JSON se coloca en hello `"resources": []` objeto de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="831ba-142">When nesting hello extension resource, hello JSON is placed in hello `"resources": []` object of hello virtual machine.</span></span>


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

<span data-ttu-id="831ba-143">Al colocar extensión Hola JSON en raíz de Hola de plantilla de hello, el nombre del recurso de hello incluye una máquina virtual de referencia toohello primario, y tipo hello refleja configuración anidados Hola.</span><span class="sxs-lookup"><span data-stu-id="831ba-143">When placing hello extension JSON at hello root of hello template, hello resource name includes a reference toohello parent virtual machine, and hello type reflects hello nested configuration.</span></span> 

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

## <a name="powershell-deployment"></a><span data-ttu-id="831ba-144">Implementación de PowerShell</span><span class="sxs-lookup"><span data-stu-id="831ba-144">PowerShell deployment</span></span>

<span data-ttu-id="831ba-145">Hola `Set-AzureRmVMExtension` comando puede ser usado toodeploy Hola agente de OMS máquina virtual extensión tooan máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="831ba-145">hello `Set-AzureRmVMExtension` command can be used toodeploy hello OMS Agent virtual machine extension tooan existing virtual machine.</span></span> <span data-ttu-id="831ba-146">Antes de ejecutar el comando de hello, configuraciones públicas y privadas de hello necesitan toobe almacenado en una tabla de hash de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="831ba-146">Before running hello command, hello public and private configurations need toobe stored in a PowerShell hash table.</span></span> 

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

## <a name="troubleshoot-and-support"></a><span data-ttu-id="831ba-147">Solución de problemas y asistencia</span><span class="sxs-lookup"><span data-stu-id="831ba-147">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="831ba-148">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="831ba-148">Troubleshoot</span></span>

<span data-ttu-id="831ba-149">Datos acerca del estado de Hola de implementaciones de extensión se pueden recuperar desde Hola portal de Azure y mediante el módulo de PowerShell de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="831ba-149">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="831ba-150">estado de implementación de hello toosee de extensiones para una máquina virtual determinada, Hola ejecución sigue usando el comando Hola módulo Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="831ba-150">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="831ba-151">Ejecución de la extensión de salida es posterior a toofiles registrados se encuentra en hello directorio:</span><span class="sxs-lookup"><span data-stu-id="831ba-151">Extension execution output is logged toofiles found in hello following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\
```

### <a name="support"></a><span data-ttu-id="831ba-152">Soporte técnico</span><span class="sxs-lookup"><span data-stu-id="831ba-152">Support</span></span>

<span data-ttu-id="831ba-153">Si necesita más ayuda en cualquier momento en este artículo, puede ponerse en contacto con hello Azure expertos en hello [foros de Azure de MSDN y el desbordamiento de la pila](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="831ba-153">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="831ba-154">Como alternativa, puede registrar un incidente de soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="831ba-154">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="831ba-155">Vaya toohello [sitio de soporte técnico de Azure](https://azure.microsoft.com/en-us/support/options/) y seleccione la obtención de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="831ba-155">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="831ba-156">Para obtener información acerca del uso de soporte técnico de Azure, lea hello [P+F de soporte de Microsoft Azure](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="831ba-156">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
