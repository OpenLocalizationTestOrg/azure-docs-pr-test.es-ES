---
title: "Creación de plantillas con extensiones de máquina virtual Linux | Microsoft Docs"
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
ms.openlocfilehash: 8b017306474670bf8dde1440128e16ec35146f24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="authoring-azure-resource-manager-templates-with-linux-vm-extensions"></a><span data-ttu-id="57b0a-103">Creación de plantillas de Azure Resource Manager con extensiones de máquina virtual de Linux</span><span class="sxs-lookup"><span data-stu-id="57b0a-103">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="57b0a-104">En la CLI de Azure, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="57b0a-104">From Azure CLI, run the following commnad:</span></span>

      Azure VM extension list

<span data-ttu-id="57b0a-105">Este comando devuelve el nombre del editor y el nombre y la versión de la extensión del siguiente modo:</span><span class="sxs-lookup"><span data-stu-id="57b0a-105">This command returns the publisher name, extension name and version as following:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="57b0a-106">Estas tres propiedades se asignan a "publisher", "type" y "typeHandlerVersion", respectivamente, en el fragmento de plantilla anterior.</span><span class="sxs-lookup"><span data-stu-id="57b0a-106">These three properties map to "publisher", "type", and "typeHandlerVersion" respectively in the above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="57b0a-107">Siempre se recomienda usar la versión más reciente de la extensión para obtener la funcionalidad más actualizada.</span><span class="sxs-lookup"><span data-stu-id="57b0a-107">It's always recommended to use the latest extension version to get the most updated functionality.</span></span>
> 
> 

## <a name="identifying-the-schema-for-the-extension-configuration-parameters"></a><span data-ttu-id="57b0a-108">Identificación del esquema de los parámetros de configuración de la extensión</span><span class="sxs-lookup"><span data-stu-id="57b0a-108">Identifying the schema for the extension configuration parameters</span></span>
<span data-ttu-id="57b0a-109">El siguiente paso en la creación de una plantilla de extensión consiste en identificar el formato para proporcionar parámetros de configuración.</span><span class="sxs-lookup"><span data-stu-id="57b0a-109">The next step with authoring an extension template is to identify the format for providing configuration parameters.</span></span> <span data-ttu-id="57b0a-110">Cada extensión es compatible con su propio conjunto de parámetros.</span><span class="sxs-lookup"><span data-stu-id="57b0a-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="57b0a-111">Para consultar configuraciones de ejemplo para extensiones de Linux, haga clic en la documentación [Ejemplos de extensiones de Linux](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="57b0a-111">To look at sample configurations for Linux extensions, click the documentation for see [Linux eExtensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="57b0a-112">Consulte el siguiente artículo para obtener una plantilla totalmente completa con extensiones de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="57b0a-112">Please refer to the following to get a fully complete template with VM Extensions.</span></span>

[<span data-ttu-id="57b0a-113">Custom script extension on a Linux VM (Extensión del script personalizado en una máquina virtual de Linux)</span><span class="sxs-lookup"><span data-stu-id="57b0a-113">Custom script extension on a Linux VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

<span data-ttu-id="57b0a-114">Una vez creada la plantilla, puede implementarla con la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="57b0a-114">After authoring the template, you can deploy it using the Azure CLI.</span></span>

