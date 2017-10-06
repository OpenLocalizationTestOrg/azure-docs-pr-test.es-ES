---
title: "extensión de máquina virtual de agente del Monitor de red para Linux aaaAzure | Documentos de Microsoft"
description: "Implementar Hola agente del Monitor de red en la máquina virtual de Linux con una extensión de máquina virtual."
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
ms.openlocfilehash: 84bed132cbda83d0917be490f9a50914578952a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-linux"></a><span data-ttu-id="9e03f-103">Extensión de máquina virtual del agente de Network Watcher para Linux</span><span class="sxs-lookup"><span data-stu-id="9e03f-103">Network Watcher Agent virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="9e03f-104">Información general</span><span class="sxs-lookup"><span data-stu-id="9e03f-104">Overview</span></span>

<span data-ttu-id="9e03f-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) es un servicio de supervisión, diagnóstico y análisis del rendimiento de red que permite supervisar redes de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e03f-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="9e03f-106">Hola extensión de máquina virtual de agente del Monitor de red es un requisito para algunas de las características del Monitor de red de hello en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e03f-106">hello Network Watcher Agent virtual machine extension is a requirement for some of hello Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="9e03f-107">Esto incluye la captura del tráfico de red a petición y otra funcionalidad avanzada.</span><span class="sxs-lookup"><span data-stu-id="9e03f-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="9e03f-108">Este Hola de detalles de documento admite opciones de implementación y plataformas para hello extensión de máquina virtual de agente del Monitor de red para Linux.</span><span class="sxs-lookup"><span data-stu-id="9e03f-108">This document details hello supported platforms and deployment options for hello Network Watcher Agent virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e03f-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9e03f-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="9e03f-110">Sistema operativos</span><span class="sxs-lookup"><span data-stu-id="9e03f-110">Operating system</span></span>

<span data-ttu-id="9e03f-111">Hola extensión del agente de Monitor de red se pueden ejecutar con las distribuciones de Linux:</span><span class="sxs-lookup"><span data-stu-id="9e03f-111">hello Network Watcher Agent extension can be run against these Linux distributions:</span></span>

| <span data-ttu-id="9e03f-112">Distribución</span><span class="sxs-lookup"><span data-stu-id="9e03f-112">Distribution</span></span> | <span data-ttu-id="9e03f-113">Versión</span><span class="sxs-lookup"><span data-stu-id="9e03f-113">Version</span></span> |
|---|---|
| <span data-ttu-id="9e03f-114">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="9e03f-114">Ubuntu</span></span> | <span data-ttu-id="9e03f-115">16.04 LTS, 14.04 LTS y 12.04 LTS</span><span class="sxs-lookup"><span data-stu-id="9e03f-115">16.04 LTS, 14.04 LTS and 12.04 LTS</span></span> |
| <span data-ttu-id="9e03f-116">Debian</span><span class="sxs-lookup"><span data-stu-id="9e03f-116">Debian</span></span> | <span data-ttu-id="9e03f-117">7 y 8</span><span class="sxs-lookup"><span data-stu-id="9e03f-117">7 and 8</span></span> |
| <span data-ttu-id="9e03f-118">Redhat</span><span class="sxs-lookup"><span data-stu-id="9e03f-118">RedHat</span></span> | <span data-ttu-id="9e03f-119">6.x y 7.x</span><span class="sxs-lookup"><span data-stu-id="9e03f-119">6.x and 7.x</span></span> |
| <span data-ttu-id="9e03f-120">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="9e03f-120">Oracle Linux</span></span> | <span data-ttu-id="9e03f-121">7x</span><span class="sxs-lookup"><span data-stu-id="9e03f-121">7x</span></span> |
| <span data-ttu-id="9e03f-122">Suse</span><span class="sxs-lookup"><span data-stu-id="9e03f-122">Suse</span></span> | <span data-ttu-id="9e03f-123">11 y 12</span><span class="sxs-lookup"><span data-stu-id="9e03f-123">11 and 12</span></span> |
| <span data-ttu-id="9e03f-124">OpenSuse</span><span class="sxs-lookup"><span data-stu-id="9e03f-124">OpenSuse</span></span> | <span data-ttu-id="9e03f-125">7.0</span><span class="sxs-lookup"><span data-stu-id="9e03f-125">7.0</span></span> |
| <span data-ttu-id="9e03f-126">CentOS</span><span class="sxs-lookup"><span data-stu-id="9e03f-126">CentOS</span></span> | <span data-ttu-id="9e03f-127">7.0</span><span class="sxs-lookup"><span data-stu-id="9e03f-127">7.0</span></span> |

<span data-ttu-id="9e03f-128">Tenga en cuenta que CoreOS no se admite en este momento.</span><span class="sxs-lookup"><span data-stu-id="9e03f-128">Note that CoreOS is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="9e03f-129">Conectividad de Internet</span><span class="sxs-lookup"><span data-stu-id="9e03f-129">Internet connectivity</span></span>

<span data-ttu-id="9e03f-130">Algunos de hello funcionalidad de agente del Monitor de red requiere a esa máquina virtual de destino de Hola sea toohello conectado Internet.</span><span class="sxs-lookup"><span data-stu-id="9e03f-130">Some of hello Network Watcher Agent functionality requires that hello target virtual machine be connected toohello Internet.</span></span> <span data-ttu-id="9e03f-131">Sin conexiones salientes de hello capacidad tooestablish algunas de las características del agente de Monitor de red Hola pueden funcione incorrectamente o dejan de estar disponibles.</span><span class="sxs-lookup"><span data-stu-id="9e03f-131">Without hello ability tooestablish outgoing connections some of hello Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="9e03f-132">Para obtener más información, vea hello [documentación del Monitor de red](https://review.docs.microsoft.com/en-us/azure/network-watcher/).</span><span class="sxs-lookup"><span data-stu-id="9e03f-132">For more details, please see hello [Network Watcher documentation](https://review.docs.microsoft.com/en-us/azure/network-watcher/).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="9e03f-133">Esquema de extensión</span><span class="sxs-lookup"><span data-stu-id="9e03f-133">Extension schema</span></span>

<span data-ttu-id="9e03f-134">Hello JSON siguiente muestra esquema Hola Hola extensión del agente de Monitor de red.</span><span class="sxs-lookup"><span data-stu-id="9e03f-134">hello following JSON shows hello schema for hello Network Watcher Agent extension.</span></span> <span data-ttu-id="9e03f-135">extensión de Hello no requiere ni admite cualquier configuración proporcionada por el usuario en este momento y se basa en su configuración predeterminada.</span><span class="sxs-lookup"><span data-stu-id="9e03f-135">hello extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

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

### <a name="property-values"></a><span data-ttu-id="9e03f-136">Valores de propiedad</span><span class="sxs-lookup"><span data-stu-id="9e03f-136">Property values</span></span>

| <span data-ttu-id="9e03f-137">Nombre</span><span class="sxs-lookup"><span data-stu-id="9e03f-137">Name</span></span> | <span data-ttu-id="9e03f-138">Valor / ejemplo</span><span class="sxs-lookup"><span data-stu-id="9e03f-138">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="9e03f-139">apiVersion</span><span class="sxs-lookup"><span data-stu-id="9e03f-139">apiVersion</span></span> | <span data-ttu-id="9e03f-140">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="9e03f-140">2015-06-15</span></span> |
| <span data-ttu-id="9e03f-141">publisher</span><span class="sxs-lookup"><span data-stu-id="9e03f-141">publisher</span></span> | <span data-ttu-id="9e03f-142">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="9e03f-142">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="9e03f-143">type</span><span class="sxs-lookup"><span data-stu-id="9e03f-143">type</span></span> | <span data-ttu-id="9e03f-144">NetworkWatcherAgentLinux</span><span class="sxs-lookup"><span data-stu-id="9e03f-144">NetworkWatcherAgentLinux</span></span> |
| <span data-ttu-id="9e03f-145">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="9e03f-145">typeHandlerVersion</span></span> | <span data-ttu-id="9e03f-146">1.4</span><span class="sxs-lookup"><span data-stu-id="9e03f-146">1.4</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="9e03f-147">Implementación de plantilla</span><span class="sxs-lookup"><span data-stu-id="9e03f-147">Template deployment</span></span>

<span data-ttu-id="9e03f-148">Las extensiones de VM de Azure pueden implementarse con plantillas de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9e03f-148">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="9e03f-149">esquema JSON de Hello detallado en la sección anterior de hello puede usarse en un hello toorun de plantilla de Azure Resource Manager extensión del agente de Monitor de red durante la implementación de plantilla Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9e03f-149">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="azure-cli-deployment"></a><span data-ttu-id="9e03f-150">Implementación de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="9e03f-150">Azure CLI deployment</span></span>

<span data-ttu-id="9e03f-151">Hola CLI de Azure puede ser usado toodeploy Hola VM de agente del Monitor de red extensión tooan máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="9e03f-151">hello Azure CLI can be used toodeploy hello Network Watcher Agent VM extension tooan existing virtual machine.</span></span>

```azurecli
azure vm extension set myResourceGroup1 myVM1 NetworkWatcherAgentLinux Microsoft.Azure.NetworkWatcher 1.4
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="9e03f-152">Solución de problemas y soporte técnico</span><span class="sxs-lookup"><span data-stu-id="9e03f-152">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="9e03f-153">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="9e03f-153">Troubleshooting</span></span>

<span data-ttu-id="9e03f-154">Datos acerca del estado de Hola de implementaciones de extensión se pueden recuperar desde Hola portal de Azure y mediante el uso de hello CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e03f-154">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure CLI.</span></span> <span data-ttu-id="9e03f-155">estado de implementación de hello toosee de extensiones para una máquina virtual determinada, ejecute hello después de usar el comando Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e03f-155">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure CLI.</span></span>

```azurecli
azure vm extension get myResourceGroup1 myVM1
```

<span data-ttu-id="9e03f-156">Ejecución de la extensión de salida es posterior a toofiles registrados se encuentra en hello directorio:</span><span class="sxs-lookup"><span data-stu-id="9e03f-156">Extension execution output is logged toofiles found in hello following directory:</span></span>

`
/var/log/azure/Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentLinux/
`

### <a name="support"></a><span data-ttu-id="9e03f-157">Soporte técnico</span><span class="sxs-lookup"><span data-stu-id="9e03f-157">Support</span></span>

<span data-ttu-id="9e03f-158">Si necesita más ayuda en cualquier momento en este artículo, puede consulte la documentación del Monitor de red toohello o póngase en contacto con hello Azure expertos en hello [foros de Azure de MSDN y el desbordamiento de la pila](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="9e03f-158">If you need more help at any point in this article, you can refer toohello Network Watcher documentation or contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="9e03f-159">Como alternativa, puede registrar un incidente de soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e03f-159">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="9e03f-160">Vaya toohello [sitio de soporte técnico de Azure](https://azure.microsoft.com/en-us/support/options/) y seleccione la obtención de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="9e03f-160">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="9e03f-161">Para obtener información acerca del uso de soporte técnico de Azure, lea hello [P+F de soporte de Microsoft Azure](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="9e03f-161">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
