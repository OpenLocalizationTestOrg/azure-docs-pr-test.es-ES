---
title: "Extensión de máquina virtual del agente de Azure Network Watcher para Linux | Microsoft Docs"
description: "Implemente el agente de Network Watcher en la máquina virtual Linux mediante una extensión de máquina virtual."
services: virtual-machines-linux
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 5c81e94c-e127-4dd2-ae83-a236c4512345
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: eaadd531b9e05a54446e61f98584ae9d75470a5f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-linux"></a><span data-ttu-id="a6578-103">Extensión de máquina virtual del agente de Network Watcher para Linux</span><span class="sxs-lookup"><span data-stu-id="a6578-103">Network Watcher Agent virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="a6578-104">Información general</span><span class="sxs-lookup"><span data-stu-id="a6578-104">Overview</span></span>

<span data-ttu-id="a6578-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) es un servicio de supervisión, diagnóstico y análisis del rendimiento de red que permite supervisar redes de Azure.</span><span class="sxs-lookup"><span data-stu-id="a6578-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="a6578-106">La extensión de máquina virtual del agente de Network Watcher es un requisito para algunas de las características de Network Watcher en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="a6578-106">The Network Watcher Agent virtual machine extension is a requirement for some of the Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="a6578-107">Esto incluye la captura del tráfico de red a petición y otra funcionalidad avanzada.</span><span class="sxs-lookup"><span data-stu-id="a6578-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="a6578-108">En este documento se especifican las plataformas compatibles y las opciones de implementación de la extensión de máquina virtual del agente de Network Watcher para Linux.</span><span class="sxs-lookup"><span data-stu-id="a6578-108">This document details the supported platforms and deployment options for the Network Watcher Agent virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a6578-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a6578-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="a6578-110">Sistema operativo</span><span class="sxs-lookup"><span data-stu-id="a6578-110">Operating system</span></span>

<span data-ttu-id="a6578-111">La extensión del agente de Network Watcher puede ejecutarse en estas distribuciones de Linux:</span><span class="sxs-lookup"><span data-stu-id="a6578-111">The Network Watcher Agent extension can be run against these Linux distributions:</span></span>

| <span data-ttu-id="a6578-112">Distribución</span><span class="sxs-lookup"><span data-stu-id="a6578-112">Distribution</span></span> | <span data-ttu-id="a6578-113">Versión</span><span class="sxs-lookup"><span data-stu-id="a6578-113">Version</span></span> |
|---|---|
| <span data-ttu-id="a6578-114">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="a6578-114">Ubuntu</span></span> | <span data-ttu-id="a6578-115">16.04 LTS, 14.04 LTS y 12.04 LTS</span><span class="sxs-lookup"><span data-stu-id="a6578-115">16.04 LTS, 14.04 LTS and 12.04 LTS</span></span> |
| <span data-ttu-id="a6578-116">Debian</span><span class="sxs-lookup"><span data-stu-id="a6578-116">Debian</span></span> | <span data-ttu-id="a6578-117">7 y 8</span><span class="sxs-lookup"><span data-stu-id="a6578-117">7 and 8</span></span> |
| <span data-ttu-id="a6578-118">Redhat</span><span class="sxs-lookup"><span data-stu-id="a6578-118">RedHat</span></span> | <span data-ttu-id="a6578-119">6.x y 7.x</span><span class="sxs-lookup"><span data-stu-id="a6578-119">6.x and 7.x</span></span> |
| <span data-ttu-id="a6578-120">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="a6578-120">Oracle Linux</span></span> | <span data-ttu-id="a6578-121">7x</span><span class="sxs-lookup"><span data-stu-id="a6578-121">7x</span></span> |
| <span data-ttu-id="a6578-122">Suse</span><span class="sxs-lookup"><span data-stu-id="a6578-122">Suse</span></span> | <span data-ttu-id="a6578-123">11 y 12</span><span class="sxs-lookup"><span data-stu-id="a6578-123">11 and 12</span></span> |
| <span data-ttu-id="a6578-124">OpenSuse</span><span class="sxs-lookup"><span data-stu-id="a6578-124">OpenSuse</span></span> | <span data-ttu-id="a6578-125">7.0</span><span class="sxs-lookup"><span data-stu-id="a6578-125">7.0</span></span> |
| <span data-ttu-id="a6578-126">CentOS</span><span class="sxs-lookup"><span data-stu-id="a6578-126">CentOS</span></span> | <span data-ttu-id="a6578-127">7.0</span><span class="sxs-lookup"><span data-stu-id="a6578-127">7.0</span></span> |

<span data-ttu-id="a6578-128">Tenga en cuenta que CoreOS no se admite en este momento.</span><span class="sxs-lookup"><span data-stu-id="a6578-128">Note that CoreOS is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="a6578-129">Conectividad de Internet</span><span class="sxs-lookup"><span data-stu-id="a6578-129">Internet connectivity</span></span>

<span data-ttu-id="a6578-130">Parte de la funcionalidad del agente de Network Watcher requiere que la máquina virtual de destino esté conectada a Internet.</span><span class="sxs-lookup"><span data-stu-id="a6578-130">Some of the Network Watcher Agent functionality requires that the target virtual machine be connected to the Internet.</span></span> <span data-ttu-id="a6578-131">Sin la capacidad de establecer conexiones salientes, algunas de las características del agente de Network Watcher pueden funcionar mal o dejar de estar disponibles.</span><span class="sxs-lookup"><span data-stu-id="a6578-131">Without the ability to establish outgoing connections some of the Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="a6578-132">Para más detalles, consulte la [documentación de Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/).</span><span class="sxs-lookup"><span data-stu-id="a6578-132">For more details, please see the [Network Watcher documentation](https://review.docs.microsoft.com/en-us/azure/network-watcher/).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="a6578-133">Esquema de extensión</span><span class="sxs-lookup"><span data-stu-id="a6578-133">Extension schema</span></span>

<span data-ttu-id="a6578-134">El siguiente JSON muestra el esquema para la extensión del agente de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="a6578-134">The following JSON shows the schema for the Network Watcher Agent extension.</span></span> <span data-ttu-id="a6578-135">La extensión no requiere ni admite ninguna configuración proporcionada por el usuario en este momento y se basa en su propia configuración predeterminada.</span><span class="sxs-lookup"><span data-stu-id="a6578-135">The extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

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
        "type": "NetworkWatcherAgentLinux",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a><span data-ttu-id="a6578-136">Valores de propiedad</span><span class="sxs-lookup"><span data-stu-id="a6578-136">Property values</span></span>

| <span data-ttu-id="a6578-137">Nombre</span><span class="sxs-lookup"><span data-stu-id="a6578-137">Name</span></span> | <span data-ttu-id="a6578-138">Valor / ejemplo</span><span class="sxs-lookup"><span data-stu-id="a6578-138">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="a6578-139">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a6578-139">apiVersion</span></span> | <span data-ttu-id="a6578-140">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="a6578-140">2015-06-15</span></span> |
| <span data-ttu-id="a6578-141">publisher</span><span class="sxs-lookup"><span data-stu-id="a6578-141">publisher</span></span> | <span data-ttu-id="a6578-142">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="a6578-142">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="a6578-143">type</span><span class="sxs-lookup"><span data-stu-id="a6578-143">type</span></span> | <span data-ttu-id="a6578-144">NetworkWatcherAgentLinux</span><span class="sxs-lookup"><span data-stu-id="a6578-144">NetworkWatcherAgentLinux</span></span> |
| <span data-ttu-id="a6578-145">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="a6578-145">typeHandlerVersion</span></span> | <span data-ttu-id="a6578-146">1.4</span><span class="sxs-lookup"><span data-stu-id="a6578-146">1.4</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="a6578-147">Implementación de plantilla</span><span class="sxs-lookup"><span data-stu-id="a6578-147">Template deployment</span></span>

<span data-ttu-id="a6578-148">Las extensiones de VM de Azure pueden implementarse con plantillas de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a6578-148">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="a6578-149">El esquema JSON detallado en la sección anterior se puede usar en una plantilla de Azure Resource Manager para ejecutar la extensión del agente de Network Watcher durante la implementación de dicha plantilla.</span><span class="sxs-lookup"><span data-stu-id="a6578-149">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="azure-cli-deployment"></a><span data-ttu-id="a6578-150">Implementación de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="a6578-150">Azure CLI deployment</span></span>

<span data-ttu-id="a6578-151">La CLI de Azure puede utilizarse para implementar la extensión de VM del agente de Network Watcher en una máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="a6578-151">The Azure CLI can be used to deploy the Network Watcher Agent VM extension to an existing virtual machine.</span></span>

```azurecli
azure vm extension set myResourceGroup1 myVM1 NetworkWatcherAgentLinux Microsoft.Azure.NetworkWatcher 1.4
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="a6578-152">Solución de problemas y soporte técnico</span><span class="sxs-lookup"><span data-stu-id="a6578-152">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="a6578-153">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="a6578-153">Troubleshooting</span></span>

<span data-ttu-id="a6578-154">Los datos sobre el estado de las implementaciones de extensiones pueden recuperarse desde Azure Portal y mediante la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="a6578-154">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure CLI.</span></span> <span data-ttu-id="a6578-155">Para ver el estado de implementación de las extensiones de una VM determinada, ejecute el comando siguiente con la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="a6578-155">To see the deployment state of extensions for a given VM, run the following command using the Azure CLI.</span></span>

```azurecli
azure vm extension get myResourceGroup1 myVM1
```

<span data-ttu-id="a6578-156">El resultado de la ejecución de las extensiones se registra en los archivos que se encuentran en el siguiente directorio:</span><span class="sxs-lookup"><span data-stu-id="a6578-156">Extension execution output is logged to files found in the following directory:</span></span>

`
/var/log/azure/Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentLinux/
`

### <a name="support"></a><span data-ttu-id="a6578-157">Soporte técnico</span><span class="sxs-lookup"><span data-stu-id="a6578-157">Support</span></span>

<span data-ttu-id="a6578-158">Si necesita más ayuda con cualquier aspecto de este artículo, puede consultar la documentación de Network Watcher o ponerse en contacto con los expertos de Azure en los [foros de MSDN Azure o Stack Overflow](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="a6578-158">If you need more help at any point in this article, you can refer to the Network Watcher documentation or contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="a6578-159">Como alternativa, puede registrar un incidente de soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="a6578-159">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="a6578-160">Vaya al [sitio de soporte técnico de Azure](https://azure.microsoft.com/en-us/support/options/) y seleccione Obtener soporte.</span><span class="sxs-lookup"><span data-stu-id="a6578-160">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="a6578-161">Para obtener información sobre el uso del soporte técnico, lea las [Preguntas más frecuentes de soporte técnico de Microsoft Azure](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="a6578-161">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
