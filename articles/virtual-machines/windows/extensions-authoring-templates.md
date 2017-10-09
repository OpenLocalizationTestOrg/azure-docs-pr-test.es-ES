---
title: aaaAuthoring plantillas con las extensiones de VM de Windows | Documentos de Microsoft
description: "Obtenga información sobre cómo crear plantillas del Administrador de recursos de Azure con extensiones para máquinas virtuales de Windows."
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 418dd1f7-ded8-45ab-9a5a-a59d245e2555
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: c5156cb3859f7ff86bebda942150d268e57d6486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="authoring-azure-resource-manager-templates-with-windows-vm-extensions"></a><span data-ttu-id="266d6-103">Creación de plantillas del Administrador de recursos de Azure con extensiones de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="266d6-103">Authoring Azure Resource Manager templates with Windows VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="266d6-104">De Azure PowerShell, ejecute hello siguiente cmdlet de PowerShell de Azure:</span><span class="sxs-lookup"><span data-stu-id="266d6-104">From Azure PowerShell, run hello following Azure PowerShell cmdlet:</span></span>

      Get-AzureVMAvailableExtension


<span data-ttu-id="266d6-105">Este cmdlet devuelve el nombre del publicador de hello, el nombre de extensión y la versión de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="266d6-105">This cmdlet returns hello publisher name, extension name, and version as follows:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="266d6-106">Estas tres propiedades se asignan demasiado "publisher", "type" y "typeHandlerVersion" respectivamente en hello por encima del fragmento de código de plantilla.</span><span class="sxs-lookup"><span data-stu-id="266d6-106">These three properties map too"publisher", "type", and "typeHandlerVersion" respectively in hello above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="266d6-107">Siempre es toouse recomendada hello más reciente extensión versión tooget Hola actualizado más funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="266d6-107">It's always recommended toouse hello latest extension version tooget hello most updated functionality.</span></span>
> 
> 

## <a name="identifying-hello-schema-for-hello-extension-configuration-parameters"></a><span data-ttu-id="266d6-108">Esquema de identificación Hola para parámetros de configuración de extensión de Hola</span><span class="sxs-lookup"><span data-stu-id="266d6-108">Identifying hello schema for hello extension configuration parameters</span></span>
<span data-ttu-id="266d6-109">Hola siguiente paso a la creación de una plantilla de la extensión es formato de hello tooidentify para proporcionar parámetros de configuración.</span><span class="sxs-lookup"><span data-stu-id="266d6-109">hello next step with authoring an extension template is tooidentify hello format for providing configuration parameters.</span></span> <span data-ttu-id="266d6-110">Cada extensión es compatible con su propio conjunto de parámetros.</span><span class="sxs-lookup"><span data-stu-id="266d6-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="266d6-111">toolook en configuraciones de ejemplo para las extensiones de Windows, vea [ejemplos de extensiones de Windows](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="266d6-111">toolook at sample configurations for Windows extensions, see [Windows extensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="266d6-112">Consulte toohello después tooget una plantilla se completará con extensiones de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="266d6-112">Please refer toohello following tooget a fully complete template with VM extensions.</span></span>

[<span data-ttu-id="266d6-113">Extensión de script personalizada en una máquina virtual de Windows</span><span class="sxs-lookup"><span data-stu-id="266d6-113">Custom Script Extension on a Windows VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/201-list-storage-keys-windows-vm/azuredeploy.json/)

<span data-ttu-id="266d6-114">Después de crear la plantilla de hello, puede implementar mediante PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="266d6-114">After authoring hello template, you can deploy it using Azure PowerShell.</span></span>

