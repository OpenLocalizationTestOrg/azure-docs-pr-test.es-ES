---
title: plantillas de aaaAuthoring con las extensiones de VM de Linux | Documentos de Microsoft
description: "Obtenga información sobre cómo crear plantillas de Azure Resource Manager con extensiones para máquinas virtuales de Linux."
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 322f8f0b-6697-4acb-b5f3-b3f58d28358b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: b797e442d8706956bbc06c5be611a2b0119055d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="authoring-azure-resource-manager-templates-with-linux-vm-extensions"></a><span data-ttu-id="ff380-103">Creación de plantillas de Azure Resource Manager con extensiones de máquina virtual de Linux</span><span class="sxs-lookup"><span data-stu-id="ff380-103">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="ff380-104">Desde la CLI de Azure, ejecute hello después %1"...cerrando:</span><span class="sxs-lookup"><span data-stu-id="ff380-104">From Azure CLI, run hello following commnad:</span></span>

      Azure VM extension list

<span data-ttu-id="ff380-105">Este comando devuelve el nombre de publicador hello, nombre de la extensión y versión como sigue:</span><span class="sxs-lookup"><span data-stu-id="ff380-105">This command returns hello publisher name, extension name and version as following:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="ff380-106">Estas tres propiedades se asignan demasiado "publisher", "type" y "typeHandlerVersion" respectivamente en hello por encima del fragmento de código de plantilla.</span><span class="sxs-lookup"><span data-stu-id="ff380-106">These three properties map too"publisher", "type", and "typeHandlerVersion" respectively in hello above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="ff380-107">Siempre es toouse recomendada hello más reciente extensión versión tooget Hola actualizado más funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="ff380-107">It's always recommended toouse hello latest extension version tooget hello most updated functionality.</span></span>
> 
> 

## <a name="identifying-hello-schema-for-hello-extension-configuration-parameters"></a><span data-ttu-id="ff380-108">Esquema de identificación Hola para parámetros de configuración de extensión de Hola</span><span class="sxs-lookup"><span data-stu-id="ff380-108">Identifying hello schema for hello extension configuration parameters</span></span>
<span data-ttu-id="ff380-109">Hola siguiente paso a la creación de una plantilla de la extensión es formato de hello tooidentify para proporcionar parámetros de configuración.</span><span class="sxs-lookup"><span data-stu-id="ff380-109">hello next step with authoring an extension template is tooidentify hello format for providing configuration parameters.</span></span> <span data-ttu-id="ff380-110">Cada extensión es compatible con su propio conjunto de parámetros.</span><span class="sxs-lookup"><span data-stu-id="ff380-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="ff380-111">toolook en configuraciones de ejemplo para extensiones de Linux, haga clic en la documentación de Hola para, consulte [Linux eExtensions ejemplos](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ff380-111">toolook at sample configurations for Linux extensions, click hello documentation for see [Linux eExtensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="ff380-112">Consulte toohello después tooget una plantilla se completará con extensiones de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ff380-112">Please refer toohello following tooget a fully complete template with VM Extensions.</span></span>

[<span data-ttu-id="ff380-113">Custom script extension on a Linux VM (Extensión del script personalizado en una máquina virtual de Linux)</span><span class="sxs-lookup"><span data-stu-id="ff380-113">Custom script extension on a Linux VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

<span data-ttu-id="ff380-114">Después de crear la plantilla de hello, puede implementar mediante Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="ff380-114">After authoring hello template, you can deploy it using hello Azure CLI.</span></span>

