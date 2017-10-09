---
title: "extensiones y características de máquina aaaVirtual para Linux | Documentos de Microsoft"
description: "Obtenga información acerca de qué extensiones están disponibles para máquinas virtuales de Azure, agrupadas por lo que proporcionan o mejoran."
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 52f5d0ec-8f75-49e7-9e15-88d46b420e63
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: e0d2ce794c76815ccc6743e8788ee5d9d931e9a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-linux"></a><span data-ttu-id="57025-103">Características y extensiones de las máquinas virtuales para Linux</span><span class="sxs-lookup"><span data-stu-id="57025-103">Virtual machine extensions and features for Linux</span></span>

<span data-ttu-id="57025-104">Las extensiones de máquina virtual de Azure son pequeñas aplicaciones que realizan tareas de automatización y configuración posterior a la implementación en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="57025-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span></span> <span data-ttu-id="57025-105">Por ejemplo, si una máquina virtual requiere la instalación de software, la protección antivirus o configuración de Docker, una extensión de máquina virtual puede ser usado toocomplete estas tareas.</span><span class="sxs-lookup"><span data-stu-id="57025-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used toocomplete these tasks.</span></span> <span data-ttu-id="57025-106">Extensiones de VM de Azure se pueden ejecutar con hello CLI de Azure, PowerShell, plantillas de Azure Resource Manager y Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="57025-106">Azure VM extensions can be run using hello Azure CLI, PowerShell, Azure Resource Manager templates, and hello Azure portal.</span></span> <span data-ttu-id="57025-107">Las extensiones pueden empaquetar con una nueva implementación de máquina virtual o se pueden ejecutar en cualquier sistema existente.</span><span class="sxs-lookup"><span data-stu-id="57025-107">Extensions can be bundled with a new virtual machine deployment, or run against any existing system.</span></span>

<span data-ttu-id="57025-108">Este documento proporciona información general sobre las extensiones de VM, requisitos previos para usar las extensiones de VM de Azure e instrucciones sobre cómo administrar toodetect y quitar extensiones de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="57025-108">This document provides an overview of VM extensions, prerequisites for using Azure VM extensions, and guidance on how toodetect, manage, and remove VM extensions.</span></span> <span data-ttu-id="57025-109">Este documento proporciona información generalizada porque muchas extensiones de máquina virtual están disponibles, cada una con una configuración potencialmente única.</span><span class="sxs-lookup"><span data-stu-id="57025-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span></span> <span data-ttu-id="57025-110">Los detalles específicos de una extensión pueden encontrarse en cada extensión individuales toohello específico de documento.</span><span class="sxs-lookup"><span data-stu-id="57025-110">Extension-specific details can be found in each document specific toohello individual extension.</span></span>

## <a name="use-cases-and-samples"></a><span data-ttu-id="57025-111">Casos de uso y ejemplos</span><span class="sxs-lookup"><span data-stu-id="57025-111">Use cases and samples</span></span>

<span data-ttu-id="57025-112">Varias extensiones de máquina virtual de Azure diferentes están disponibles, cada una con un caso de uso específico.</span><span class="sxs-lookup"><span data-stu-id="57025-112">Several different Azure VM extensions are available, each with a specific use case.</span></span> <span data-ttu-id="57025-113">A continuación, se indican algunos ejemplos:</span><span class="sxs-lookup"><span data-stu-id="57025-113">Some examples are:</span></span>

- <span data-ttu-id="57025-114">Aplicar el estado deseado de PowerShell configuraciones tooa máquina virtual a través Hola extensión de DSC para Linux.</span><span class="sxs-lookup"><span data-stu-id="57025-114">Apply PowerShell Desired State configurations tooa virtual machine using hello DSC extension for Linux.</span></span> <span data-ttu-id="57025-115">Para obtener más información, consulte la sección sobre la [extensión de configuración de estado deseado de Azure](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).</span><span class="sxs-lookup"><span data-stu-id="57025-115">For more information, see [Azure Desired State configuration extension](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).</span></span>
- <span data-ttu-id="57025-116">Configurar la supervisión de una máquina virtual con hello extensión de máquina virtual de agente de supervisión de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="57025-116">Configure monitoring of a virtual machine with hello Microsoft Monitoring Agent VM extension.</span></span> <span data-ttu-id="57025-117">Para obtener más información, consulte [cómo toomonitor una VM Linux](tutorial-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="57025-117">For more information, see [How toomonitor a Linux VM](tutorial-monitoring.md).</span></span>
- <span data-ttu-id="57025-118">Configurar la supervisión de la infraestructura de Azure con hello Datadog extensión.</span><span class="sxs-lookup"><span data-stu-id="57025-118">Configure monitoring of your Azure infrastructure with hello Datadog extension.</span></span> <span data-ttu-id="57025-119">Para obtener más información, vea hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span><span class="sxs-lookup"><span data-stu-id="57025-119">For more information, see hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span></span>
- <span data-ttu-id="57025-120">Configurar un host Docker en una máquina virtual de Azure con la extensión de máquina virtual Docker Hola.</span><span class="sxs-lookup"><span data-stu-id="57025-120">Configure a Docker host on an Azure virtual machine using hello Docker VM extension.</span></span> <span data-ttu-id="57025-121">Para obtener más información, consulte [Extensión de máquina virtual de Docker](dockerextension.md).</span><span class="sxs-lookup"><span data-stu-id="57025-121">For more information, see [Docker VM extension](dockerextension.md).</span></span>

<span data-ttu-id="57025-122">Además extensiones específicas de tooprocess, una extensión de Script personalizado está disponible para máquinas virtuales Windows y Linux.</span><span class="sxs-lookup"><span data-stu-id="57025-122">In addition tooprocess-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span></span> <span data-ttu-id="57025-123">Hola extensión de Script personalizado para Linux permite cualquier toobe de secuencia de comandos de Bash ejecutar en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="57025-123">hello Custom Script extension for Linux allows any Bash script toobe run on a virtual machine.</span></span> <span data-ttu-id="57025-124">Los scripts personalizados resultan útiles para diseñar implementaciones de Azure que requieren una configuración más allá de lo que las herramientas de Azure nativas pueden proporcionar.</span><span class="sxs-lookup"><span data-stu-id="57025-124">Custom scripts are useful for designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span></span> <span data-ttu-id="57025-125">Para obtener más información, consulte la sección sobre la [extensión de script personalizado de máquina virtual Linux](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="57025-125">For more information, see [Linux VM Custom Script extension](extensions-customscript.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="57025-126">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="57025-126">Prerequisites</span></span>

<span data-ttu-id="57025-127">Cada extensión de máquina virtual puede tener su propio conjunto de requisitos previos.</span><span class="sxs-lookup"><span data-stu-id="57025-127">Each virtual machine extension might have its own set of prerequisites.</span></span> <span data-ttu-id="57025-128">Por ejemplo, hello extensión de máquina virtual Docker tiene un requisito previo de la distribución de Linux compatible.</span><span class="sxs-lookup"><span data-stu-id="57025-128">For instance, hello Docker VM extension has a prerequisite of a supported Linux distribution.</span></span> <span data-ttu-id="57025-129">Requisitos de extensiones individuales se detallan en la documentación específica de la extensión de Hola.</span><span class="sxs-lookup"><span data-stu-id="57025-129">Requirements of individual extensions are detailed in hello extension-specific documentation.</span></span>

### <a name="azure-vm-agent"></a><span data-ttu-id="57025-130">Agente de máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="57025-130">Azure VM agent</span></span>

<span data-ttu-id="57025-131">agente de máquina virtual de Azure de Hello administra las interacciones entre una máquina virtual de Azure y el controlador de tejido de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="57025-131">hello Azure VM agent manages interactions between an Azure virtual machine and hello Azure fabric controller.</span></span> <span data-ttu-id="57025-132">agente de máquina virtual de Hello es responsable de muchos aspectos funcionales de la implementación y administración de máquinas virtuales de Azure, incluida la ejecución de extensiones de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="57025-132">hello VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span></span> <span data-ttu-id="57025-133">agente de máquina virtual de Azure de Hello está preinstalado en imágenes de Azure Marketplace y puede instalarse manualmente en los sistemas operativos compatibles.</span><span class="sxs-lookup"><span data-stu-id="57025-133">hello Azure VM agent is preinstalled on Azure Marketplace images and can be installed manually on supported operating systems.</span></span>

<span data-ttu-id="57025-134">Para obtener información sobre las instrucciones de instalación y los sistemas operativos compatibles, consulte [Agente de máquina virtual de Azure](../windows/classic/agents-and-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="57025-134">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](../windows/classic/agents-and-extensions.md).</span></span>

## <a name="discover-vm-extensions"></a><span data-ttu-id="57025-135">Detección de extensiones de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="57025-135">Discover VM extensions</span></span>

<span data-ttu-id="57025-136">Hay muchas extensiones de máquina virtual diferentes disponibles para su uso con máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="57025-136">Many different VM extensions are available for use with Azure virtual machines.</span></span> <span data-ttu-id="57025-137">toosee una lista completa, ejecute hello siguiente comando con hello CLI de Azure, reemplazando la ubicación de ejemplo de Hola por ubicación de Hola de su elección.</span><span class="sxs-lookup"><span data-stu-id="57025-137">toosee a complete list, run hello following command with hello Azure CLI, replacing hello example location with hello location of your choice.</span></span>

```azurecli
az vm extension image list --location westus -o table
```

## <a name="run-vm-extensions"></a><span data-ttu-id="57025-138">Ejecución de extensiones de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="57025-138">Run VM extensions</span></span>

<span data-ttu-id="57025-139">Las extensiones de máquina virtual de Azure se pueden ejecutar en máquinas virtuales existentes, que son útiles cuando necesita cambios de configuración de toomake o recuperar conectividad en una máquina virtual ya implementada.</span><span class="sxs-lookup"><span data-stu-id="57025-139">Azure virtual machine extensions can be run on existing virtual machines, which are useful when you need toomake configuration changes or recover connectivity on an already deployed VM.</span></span> <span data-ttu-id="57025-140">Las extensiones de máquina virtual también pueden agruparse con las implementaciones de plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="57025-140">VM extensions can also be bundled with Azure Resource Manager template deployments.</span></span> <span data-ttu-id="57025-141">Al usar las extensiones con plantillas de Resource Manager, las máquinas virtuales de Azure se pueden implementar y configurar sin intervención alguna después de la implementación.</span><span class="sxs-lookup"><span data-stu-id="57025-141">By using extensions with Resource Manager templates, Azure virtual machines can be deployed and configured without post-deployment intervention.</span></span>

<span data-ttu-id="57025-142">Hola siguiendo métodos puede ser toorun usa una extensión en una máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="57025-142">hello following methods can be used toorun an extension against an existing virtual machine.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="57025-143">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="57025-143">Azure CLI</span></span>

<span data-ttu-id="57025-144">Extensiones de máquina virtual de Azure se pueden ejecutar en una máquina virtual existente mediante el uso de hello `az vm extension set` comando.</span><span class="sxs-lookup"><span data-stu-id="57025-144">Azure virtual machine extensions can be run against an existing virtual machine by using hello `az vm extension set` command.</span></span> <span data-ttu-id="57025-145">Este ejemplo ejecuta la extensión de script personalizado de hello en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="57025-145">This example runs hello custom script extension against a virtual machine.</span></span>

```azurecli
az vm extension set `
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"],"commandToExecute": "./hello.sh"}'
```

<span data-ttu-id="57025-146">Hola script genera resultados similares toohello siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="57025-146">hello script produces output similar toohello following text:</span></span>

```azurecli
info:    Executing command vm extension set
+ Looking up hello VM "myVM"
+ Installing extension "CustomScript", VM: "mvVM"
info:    vm extension set command OK
```

### <a name="azure-portal"></a><span data-ttu-id="57025-147">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="57025-147">Azure portal</span></span>

<span data-ttu-id="57025-148">Extensiones de máquina virtual pueden ser tooan aplicada de máquina virtual existente a través de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="57025-148">VM extensions can be applied tooan existing virtual machine through hello Azure portal.</span></span> <span data-ttu-id="57025-149">toodo por lo tanto, seleccione la máquina virtual de hello, elija **extensiones**y haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="57025-149">toodo so, select hello virtual machine, choose **Extensions**, and click **Add**.</span></span> <span data-ttu-id="57025-150">Seleccionar extensión de Hola que desee desde la lista de Hola de extensiones disponibles y siga las instrucciones de hello en el Asistente de Hola.</span><span class="sxs-lookup"><span data-stu-id="57025-150">Select hello extension you want from hello list of available extensions and follow hello instructions in hello wizard.</span></span>

<span data-ttu-id="57025-151">Hello siguiente imagen muestra instalación Hola de hello extensión de Script personalizado de Linux de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="57025-151">hello following image shows hello installation of hello Linux Custom Script extension from hello Azure portal.</span></span>

![Instalar la extensión de script personalizado](./media/extensions-features/installscriptextensionlinux.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="57025-153">Plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="57025-153">Azure Resource Manager templates</span></span>

<span data-ttu-id="57025-154">Extensiones de máquina virtual pueden ser plantilla de Azure Resource Manager tooan agregada y ejecutan con la implementación de Hola de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="57025-154">VM extensions can be added tooan Azure Resource Manager template and executed with hello deployment of hello template.</span></span> <span data-ttu-id="57025-155">Al implementar una extensión con una plantilla, puede crear implementaciones de Azure completamente configuradas.</span><span class="sxs-lookup"><span data-stu-id="57025-155">When you deploy an extension with a template, you can create fully configured Azure deployments.</span></span> <span data-ttu-id="57025-156">Por ejemplo, hello que JSON siguiente procede de una plantilla de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="57025-156">For example, hello following JSON is taken from a Resource Manager template.</span></span> <span data-ttu-id="57025-157">plantilla de Hello implementa un conjunto de máquinas virtuales de equilibrio de carga y una base de datos de SQL Azure y, a continuación, instala una aplicación de .NET Core en cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="57025-157">hello template deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span></span> <span data-ttu-id="57025-158">Hola extensión de máquina virtual se encarga de la instalación de software de Hola.</span><span class="sxs-lookup"><span data-stu-id="57025-158">hello VM extension takes care of hello software installation.</span></span>

<span data-ttu-id="57025-159">Para obtener más información, vea Hola completa [plantilla del Administrador de recursos](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="57025-159">For more information, see hello full [Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
    }
}
```

<span data-ttu-id="57025-160">Para más información, consulte [Creación de plantillas de Azure Resource Manager](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span><span class="sxs-lookup"><span data-stu-id="57025-160">For more information, see [Authoring Azure Resource Manager templates](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span></span>

## <a name="secure-vm-extension-data"></a><span data-ttu-id="57025-161">Protección de datos de extensión de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="57025-161">Secure VM extension data</span></span>

<span data-ttu-id="57025-162">Si estás ejecutando una extensión de máquina virtual, puede ser necesario tooinclude información confidencial, como las credenciales y los nombres de cuenta de almacenamiento, las teclas de acceso de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="57025-162">When you're running a VM extension, it may be necessary tooinclude sensitive information such as credentials, storage account names, and storage account access keys.</span></span> <span data-ttu-id="57025-163">Muchas de las extensiones de VM incluyen una configuración protegida, que cifra los datos y los descifra solo dentro de la máquina virtual de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="57025-163">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside hello target virtual machine.</span></span> <span data-ttu-id="57025-164">Cada extensión tiene un esquema específico de configuración protegida que se detalla de forma individual en la documentación específica de extensión.</span><span class="sxs-lookup"><span data-stu-id="57025-164">Each extension has a specific protected configuration schema, and each is detailed in extension-specific documentation.</span></span>

<span data-ttu-id="57025-165">Hola de ejemplo siguiente muestra una instancia de hello extensión de Script personalizado para Linux.</span><span class="sxs-lookup"><span data-stu-id="57025-165">hello following example shows an instance of hello Custom Script extension for Linux.</span></span> <span data-ttu-id="57025-166">Tenga en cuenta que tooexecute de comando hello incluye un conjunto de credenciales.</span><span class="sxs-lookup"><span data-stu-id="57025-166">Notice that hello command tooexecute includes a set of credentials.</span></span> <span data-ttu-id="57025-167">En este ejemplo, no se cifrarán Hola comando tooexecute.</span><span class="sxs-lookup"><span data-stu-id="57025-167">In this example, hello command tooexecute will not be encrypted.</span></span>


```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ],
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

<span data-ttu-id="57025-168">Hola móvil **comando tooexecute** propiedad toohello **protegido** configuración protege la cadena de ejecución de Hola.</span><span class="sxs-lookup"><span data-stu-id="57025-168">Moving hello **command tooexecute** property toohello **protected** configuration secures hello execution string.</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

## <a name="troubleshoot-vm-extensions"></a><span data-ttu-id="57025-169">Solución de problemas de extensiones de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="57025-169">Troubleshoot VM extensions</span></span>

<span data-ttu-id="57025-170">Cada extensión de máquina virtual puede tener la extensión de toohello concreto de pasos de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="57025-170">Each VM extension may have troubleshooting steps specific toohello extension.</span></span> <span data-ttu-id="57025-171">Por ejemplo, cuando se usa la extensión de Script personalizado de hello, detalles de ejecución de script encontrará localmente en la máquina virtual de hello en el que se ejecutó la extensión de Hola.</span><span class="sxs-lookup"><span data-stu-id="57025-171">For example, when you're using hello Custom Script extension, script execution details can be found locally on hello virtual machine on which hello extension was run.</span></span> <span data-ttu-id="57025-172">Todos los pasos de solución de problemas específicos de extensión aparecen detallados en la documentación específica de extensión.</span><span class="sxs-lookup"><span data-stu-id="57025-172">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span></span>

<span data-ttu-id="57025-173">Hola siguiendo los pasos de solución de problemas aplica tooall extensiones de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="57025-173">hello following troubleshooting steps apply tooall virtual machine extensions.</span></span>

### <a name="view-extension-status"></a><span data-ttu-id="57025-174">Consulta del estado de la extensión</span><span class="sxs-lookup"><span data-stu-id="57025-174">View extension status</span></span>

<span data-ttu-id="57025-175">Después de una extensión de máquina virtual se ha ejecutado en una máquina virtual, use Hola siguiendo el estado de extensión de tooreturn de comando de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="57025-175">After a virtual machine extension has been run against a virtual machine, use hello following Azure CLI command tooreturn extension status.</span></span> <span data-ttu-id="57025-176">Reemplace los nombres de parámetros de ejemplo por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="57025-176">Replace example parameter names with your own values.</span></span>

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

<span data-ttu-id="57025-177">salida de Hello es similar a Hola siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="57025-177">hello output looks like hello following text:</span></span>

```azurecli
AutoUpgradeMinorVersion    Location    Name          ProvisioningState    Publisher                   ResourceGroup      TypeHandlerVersion  VirtualMachineExtensionType
-------------------------  ----------  ------------  -------------------  --------------------------  ---------------  --------------------  -----------------------------
True                       westus      customScript  Succeeded            Microsoft.Azure.Extensions  exttest                             2  customScript
```

<span data-ttu-id="57025-178">Estado de ejecución de extensión también puede encontrarse en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="57025-178">Extension execution status can also be found in hello Azure portal.</span></span> <span data-ttu-id="57025-179">estado de hello tooview de una extensión, la máquina virtual de hello seleccione, elija **extensiones**, y seleccione Hola extensión deseada.</span><span class="sxs-lookup"><span data-stu-id="57025-179">tooview hello status of an extension, select hello virtual machine, choose **Extensions**, and select hello desired extension.</span></span>

### <a name="rerun-a-vm-extension"></a><span data-ttu-id="57025-180">Repetición de ejecución de una extensión de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="57025-180">Rerun a VM extension</span></span>

<span data-ttu-id="57025-181">Puede haber casos en que una extensión de máquina virtual necesita toobe vuelva a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="57025-181">There may be cases in which a virtual machine extension needs toobe rerun.</span></span> <span data-ttu-id="57025-182">Puede volver a ejecutar una extensión quitarlo y, a continuación, volver a ejecutar la extensión de hello con un método de ejecución de su elección.</span><span class="sxs-lookup"><span data-stu-id="57025-182">You can rerun an extension by removing it, and then rerunning hello extension with an execution method of your choice.</span></span> <span data-ttu-id="57025-183">tooremove una extensión, al ejecutar el siguiente comando con hello Azure CLI de Hola.</span><span class="sxs-lookup"><span data-stu-id="57025-183">tooremove an extension, run hello following command with hello Azure CLI.</span></span> <span data-ttu-id="57025-184">Reemplace los nombres de parámetros de ejemplo por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="57025-184">Replace example parameter names with your own values.</span></span>

```azurecli
az vm extension delete --name customScript --resource-group myResourceGroup --vm-name myVM
```

<span data-ttu-id="57025-185">Puede quitar una extensión mediante Hola pasos de hello portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="57025-185">You can remove an extension by using hello following steps in hello Azure portal:</span></span>

1. <span data-ttu-id="57025-186">Seleccione una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="57025-186">Select a virtual machine.</span></span>
2. <span data-ttu-id="57025-187">Elija **Extensiones**.</span><span class="sxs-lookup"><span data-stu-id="57025-187">Choose **Extensions**.</span></span>
3. <span data-ttu-id="57025-188">Seleccionar extensión de hello deseado.</span><span class="sxs-lookup"><span data-stu-id="57025-188">Select hello desired extension.</span></span>
4. <span data-ttu-id="57025-189">Elija **Desinstalar**.</span><span class="sxs-lookup"><span data-stu-id="57025-189">Choose **Uninstall**.</span></span>

## <a name="common-vm-extension-reference"></a><span data-ttu-id="57025-190">Referencia de extensión de máquina virtual común</span><span class="sxs-lookup"><span data-stu-id="57025-190">Common VM extension reference</span></span>
| <span data-ttu-id="57025-191">Nombre de la extensión</span><span class="sxs-lookup"><span data-stu-id="57025-191">Extension name</span></span> | <span data-ttu-id="57025-192">Descripción</span><span class="sxs-lookup"><span data-stu-id="57025-192">Description</span></span> | <span data-ttu-id="57025-193">Más información</span><span class="sxs-lookup"><span data-stu-id="57025-193">More information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="57025-194">Extensión de script personalizado para Linux</span><span class="sxs-lookup"><span data-stu-id="57025-194">Custom Script extension for Linux</span></span> |<span data-ttu-id="57025-195">Ejecución de scripts en una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="57025-195">Run scripts against an Azure virtual machine</span></span> |[<span data-ttu-id="57025-196">Extensión de script personalizado para Linux</span><span class="sxs-lookup"><span data-stu-id="57025-196">Custom Script extension for Linux</span></span>](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="57025-197">Extensión de Docker</span><span class="sxs-lookup"><span data-stu-id="57025-197">Docker extension</span></span> |<span data-ttu-id="57025-198">Comandos de Docker remotos de hello Docker daemon toosupport de instalación.</span><span class="sxs-lookup"><span data-stu-id="57025-198">Install hello Docker daemon toosupport remote Docker commands.</span></span> |[<span data-ttu-id="57025-199">Extensión de máquina virtual de Docker</span><span class="sxs-lookup"><span data-stu-id="57025-199">Docker VM extension</span></span>](dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="57025-200">Extensión de acceso a máquina virtual</span><span class="sxs-lookup"><span data-stu-id="57025-200">VM Access extension</span></span> |<span data-ttu-id="57025-201">Recuperar el acceso tooan máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="57025-201">Regain access tooan Azure virtual machine</span></span> |[<span data-ttu-id="57025-202">Extensión de acceso a máquina virtual</span><span class="sxs-lookup"><span data-stu-id="57025-202">VM Access extension</span></span>](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) |
| <span data-ttu-id="57025-203">Extensión de Diagnósticos de Azure</span><span class="sxs-lookup"><span data-stu-id="57025-203">Azure Diagnostics extension</span></span> |<span data-ttu-id="57025-204">Administración de Diagnósticos de Azure</span><span class="sxs-lookup"><span data-stu-id="57025-204">Manage Azure Diagnostics</span></span> |[<span data-ttu-id="57025-205">Extensión de Diagnósticos de Azure</span><span class="sxs-lookup"><span data-stu-id="57025-205">Azure Diagnostics extension</span></span>](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| <span data-ttu-id="57025-206">Extensión de acceso a máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="57025-206">Azure VM Access extension</span></span> |<span data-ttu-id="57025-207">Administración de usuarios y credenciales</span><span class="sxs-lookup"><span data-stu-id="57025-207">Manage users and credentials</span></span> |[<span data-ttu-id="57025-208">Extensión de acceso a máquina virtual para Linux</span><span class="sxs-lookup"><span data-stu-id="57025-208">VM Access extension for Linux</span></span>](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
