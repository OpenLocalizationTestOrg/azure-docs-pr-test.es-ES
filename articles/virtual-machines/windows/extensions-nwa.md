---
title: "extensión de máquina virtual de agente del Monitor de red para Windows aaaAzure | Documentos de Microsoft"
description: "Implementar Hola agente del Monitor de red en la máquina virtual de Windows con una extensión de máquina virtual."
services: virtual-machines-windows
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 27e46af7-2150-45e8-b084-ba33de8c5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: 21298706e462ff32c4d314f9a1ad127074ddf481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-windows"></a><span data-ttu-id="614ba-103">Extensión de máquina virtual del agente de Network Watcher para Windows</span><span class="sxs-lookup"><span data-stu-id="614ba-103">Network Watcher Agent virtual machine extension for Windows</span></span>

## <a name="overview"></a><span data-ttu-id="614ba-104">Información general</span><span class="sxs-lookup"><span data-stu-id="614ba-104">Overview</span></span>

<span data-ttu-id="614ba-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) es un servicio de supervisión, diagnóstico y análisis del rendimiento de red que permite supervisar redes de Azure.</span><span class="sxs-lookup"><span data-stu-id="614ba-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="614ba-106">Hola extensión de máquina virtual de agente del Monitor de red es un requisito para algunas de las características del Monitor de red de hello en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="614ba-106">hello Network Watcher Agent virtual machine extension is a requirement for some of hello Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="614ba-107">Esto incluye la captura del tráfico de red a petición y otra funcionalidad avanzada.</span><span class="sxs-lookup"><span data-stu-id="614ba-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="614ba-108">Este Hola de detalles de documento admite plataformas y opciones de implementación para hello extensión de máquina virtual de agente del Monitor de red para Windows.</span><span class="sxs-lookup"><span data-stu-id="614ba-108">This document details hello supported platforms and deployment options for hello Network Watcher Agent virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="614ba-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="614ba-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="614ba-110">Sistema operativos</span><span class="sxs-lookup"><span data-stu-id="614ba-110">Operating system</span></span>

<span data-ttu-id="614ba-111">Hola extensión del agente de Monitor de red de Windows se pueden ejecutar en Windows Server 2008 R2, 2012, 2012 R2 y 2016 libera.</span><span class="sxs-lookup"><span data-stu-id="614ba-111">hello Network Watcher Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span> <span data-ttu-id="614ba-112">Tenga en cuenta que Hola Nano Server no se admite en este momento.</span><span class="sxs-lookup"><span data-stu-id="614ba-112">Note that hello Nano Server is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="614ba-113">Conectividad de Internet</span><span class="sxs-lookup"><span data-stu-id="614ba-113">Internet connectivity</span></span>

<span data-ttu-id="614ba-114">Algunos de hello funcionalidad de agente del Monitor de red requiere a esa máquina virtual de destino de Hola sea toohello conectado Internet.</span><span class="sxs-lookup"><span data-stu-id="614ba-114">Some of hello Network Watcher Agent functionality requires that hello target virtual machine be connected toohello Internet.</span></span> <span data-ttu-id="614ba-115">Sin conexiones salientes de hello capacidad tooestablish algunas de las características del agente de Monitor de red Hola pueden funcione incorrectamente o dejan de estar disponibles.</span><span class="sxs-lookup"><span data-stu-id="614ba-115">Without hello ability tooestablish outgoing connections some of hello Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="614ba-116">Para obtener más información, vea hello [documentación del Monitor de red](../../network-watcher/network-watcher-monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="614ba-116">For more details, please see hello [Network Watcher documentation](../../network-watcher/network-watcher-monitoring-overview.md).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="614ba-117">Esquema de extensión</span><span class="sxs-lookup"><span data-stu-id="614ba-117">Extension schema</span></span>

<span data-ttu-id="614ba-118">Hello JSON siguiente muestra esquema Hola Hola extensión del agente de Monitor de red.</span><span class="sxs-lookup"><span data-stu-id="614ba-118">hello following JSON shows hello schema for hello Network Watcher Agent extension.</span></span> <span data-ttu-id="614ba-119">extensión de Hello no requiere ni admite cualquier configuración proporcionada por el usuario en este momento y se basa en su configuración predeterminada.</span><span class="sxs-lookup"><span data-stu-id="614ba-119">hello extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

```json
{
    "type": "extensions",
    "name": "Microsoft.Azure.NetworkWatcher",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.Azure.NetworkWatcher",
        "type": "NetworkWatcherAgentWindows",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a><span data-ttu-id="614ba-120">Valores de propiedad</span><span class="sxs-lookup"><span data-stu-id="614ba-120">Property values</span></span>

| <span data-ttu-id="614ba-121">Nombre</span><span class="sxs-lookup"><span data-stu-id="614ba-121">Name</span></span> | <span data-ttu-id="614ba-122">Valor / ejemplo</span><span class="sxs-lookup"><span data-stu-id="614ba-122">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="614ba-123">apiVersion</span><span class="sxs-lookup"><span data-stu-id="614ba-123">apiVersion</span></span> | <span data-ttu-id="614ba-124">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="614ba-124">2015-06-15</span></span> |
| <span data-ttu-id="614ba-125">publisher</span><span class="sxs-lookup"><span data-stu-id="614ba-125">publisher</span></span> | <span data-ttu-id="614ba-126">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="614ba-126">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="614ba-127">type</span><span class="sxs-lookup"><span data-stu-id="614ba-127">type</span></span> | <span data-ttu-id="614ba-128">NetworkWatcherAgentWindows</span><span class="sxs-lookup"><span data-stu-id="614ba-128">NetworkWatcherAgentWindows</span></span> |
| <span data-ttu-id="614ba-129">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="614ba-129">typeHandlerVersion</span></span> | <span data-ttu-id="614ba-130">1.4</span><span class="sxs-lookup"><span data-stu-id="614ba-130">1.4</span></span> |


## <a name="template-deployment"></a><span data-ttu-id="614ba-131">Implementación de plantilla</span><span class="sxs-lookup"><span data-stu-id="614ba-131">Template deployment</span></span>

<span data-ttu-id="614ba-132">Las extensiones de VM de Azure pueden implementarse con plantillas de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="614ba-132">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="614ba-133">esquema JSON de Hello detallado en la sección anterior de hello puede usarse en un hello toorun de plantilla de Azure Resource Manager extensión del agente de Monitor de red durante la implementación de plantilla Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="614ba-133">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="614ba-134">Implementación de PowerShell</span><span class="sxs-lookup"><span data-stu-id="614ba-134">PowerShell deployment</span></span>

<span data-ttu-id="614ba-135">Hola `Set-AzureRmVMExtension` comando puede ser usado toodeploy Hola agente del Monitor de red máquina virtual extensión tooan máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="614ba-135">hello `Set-AzureRmVMExtension` command can be used toodeploy hello Network Watcher Agent virtual machine extension tooan existing virtual machine.</span></span>

```powershell
Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup1" `
                       -Location "WestUS" `
                       -VMName "myVM1" `
                       -Name "networkWatcherAgent" `
                       -Publisher "Microsoft.Azure.NetworkWatcher" `
                       -Type "NetworkWatcherAgentWindows" `
                       -TypeHandlerVersion "1.4"
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="614ba-136">Solución de problemas y soporte técnico</span><span class="sxs-lookup"><span data-stu-id="614ba-136">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="614ba-137">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="614ba-137">Troubleshooting</span></span>

<span data-ttu-id="614ba-138">Datos acerca del estado de Hola de implementaciones de extensión se pueden recuperar desde Hola portal de Azure y mediante el módulo de PowerShell de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="614ba-138">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="614ba-139">estado de implementación de hello toosee de extensiones para una máquina virtual determinada, Hola ejecución sigue usando el comando Hola módulo Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="614ba-139">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup1 -VMName myVM1 -Name networkWatcherAgent
```

<span data-ttu-id="614ba-140">Ejecución de la extensión de salida es posterior a toofiles registrados se encuentra en hello directorio:</span><span class="sxs-lookup"><span data-stu-id="614ba-140">Extension execution output is logged toofiles found in hello following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentWindows\
```

### <a name="support"></a><span data-ttu-id="614ba-141">Soporte técnico</span><span class="sxs-lookup"><span data-stu-id="614ba-141">Support</span></span>

<span data-ttu-id="614ba-142">Si necesita más ayuda en cualquier momento en este artículo, puede consulte la documentación de la Guía de usuario del Monitor de red de toohello o póngase en contacto con hello Azure expertos en hello [foros de Azure de MSDN y el desbordamiento de la pila](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="614ba-142">If you need more help at any point in this article, you can refer toohello Network Watcher User Guide documentation or contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="614ba-143">Como alternativa, puede registrar un incidente de soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="614ba-143">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="614ba-144">Vaya toohello [sitio de soporte técnico de Azure](https://azure.microsoft.com/en-us/support/options/) y seleccione la obtención de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="614ba-144">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="614ba-145">Para obtener información acerca del uso de soporte técnico de Azure, lea hello [P+F de soporte de Microsoft Azure](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="614ba-145">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
