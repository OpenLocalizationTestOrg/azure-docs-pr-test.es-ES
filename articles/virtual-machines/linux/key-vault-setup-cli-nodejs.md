---
title: "aaaSet el almacén de claves para las máquinas virtuales de Linux con hello 1.0 de CLI de Azure | Documentos de Microsoft"
description: "Cómo tooset el almacén de claves para su uso con una máquina virtual de Azure Resource Manager con Hola 1.0 de CLI de Azure."
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: 275022e4e7e26d7363784c289dd7512047c07bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager-with-hello-azure-cli-10"></a><span data-ttu-id="b19a7-103">Configurar el almacén de claves para las máquinas virtuales en el Administrador de recursos de Azure con hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="b19a7-103">Set up Key Vault for virtual machines in Azure Resource Manager with hello Azure CLI 1.0</span></span>
<span data-ttu-id="b19a7-104">En la pila del Administrador de recursos de Azure hello, secretos/certificados se modelan como recursos proporcionados por el proveedor de recursos de Hola de almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="b19a7-104">In hello Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by hello resource provider of Key Vault.</span></span> <span data-ttu-id="b19a7-105">toolearn más información acerca del almacén de claves de Azure, consulte [¿qué es el almacén de claves de Azure?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="b19a7-105">toolearn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="b19a7-106">En orden para toobe de almacén de claves que se utiliza con máquinas virtuales del Administrador de recursos de Azure, Hola *EnabledForDeployment* propiedad en el almacén de claves se debe establecer tootrue.</span><span class="sxs-lookup"><span data-stu-id="b19a7-106">In order for Key Vault toobe used with Azure Resource Manager virtual machines, hello *EnabledForDeployment* property on Key Vault must be set tootrue.</span></span> <span data-ttu-id="b19a7-107">Puede hacer esto en varios clientes.</span><span class="sxs-lookup"><span data-stu-id="b19a7-107">You can do this in various clients.</span></span> <span data-ttu-id="b19a7-108">Este artículo muestra cómo tooset el almacén de claves para su uso con máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="b19a7-108">This article shows you how tooset up Key Vault for use with Azure Virtual Machines.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="b19a7-109">Tarea CLI versiones toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="b19a7-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="b19a7-110">Puede completar la tarea hello mediante uno de los siguientes versiones CLI de Hola</span><span class="sxs-lookup"><span data-stu-id="b19a7-110">You can complete hello task using one of hello following CLI versions</span></span>

- <span data-ttu-id="b19a7-111">[Azure 1.0 de CLI](#quick-commands) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)</span><span class="sxs-lookup"><span data-stu-id="b19a7-111">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="b19a7-112">[Azure 2.0 CLI](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="b19a7-112">[Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="use-cli-10-tooset-up-key-vault"></a><span data-ttu-id="b19a7-113">Utilice CLI 1.0 tooset el almacén de claves</span><span class="sxs-lookup"><span data-stu-id="b19a7-113">Use CLI 1.0 tooset up Key Vault</span></span>
<span data-ttu-id="b19a7-114">toocreate un almacén de claves mediante Hola interfaz de línea de comandos (CLI), consulte [administrar el almacén de claves con CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span><span class="sxs-lookup"><span data-stu-id="b19a7-114">toocreate a key vault by using hello command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="b19a7-115">Para CLI 1.0, es necesario el almacén de claves de hello toocreate antes de asignar la directiva de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="b19a7-115">For CLI 1.0, you have toocreate hello key vault before you assign hello deployment policy.</span></span> <span data-ttu-id="b19a7-116">A continuación, puede asignar directivas de hello mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b19a7-116">You can then assign hello policy by using hello following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a><span data-ttu-id="b19a7-117">Usar plantillas tooset el almacén de claves</span><span class="sxs-lookup"><span data-stu-id="b19a7-117">Use templates tooset up Key Vault</span></span>
<span data-ttu-id="b19a7-118">Cuando se usa una plantilla, deberá hello tooset `enabledForDeployment` propiedad demasiado`true` para hello recursos de almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="b19a7-118">When you use a template, you need tooset hello `enabledForDeployment` property too`true` for hello Key Vault resource.</span></span>

    {
      "type": "Microsoft.KeyVault/vaults",
      "name": "ContosoKeyVault",
      "apiVersion": "2015-06-01",
      "location": "<location-of-key-vault>",
      "properties": {
        "enabledForDeployment": "true",
        ....
        ....
      }
    }

<span data-ttu-id="b19a7-119">Para otras opciones que puede configurar al crear un almacén de claves mediante plantillas, consulte [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/)(Creación de un almacén de claves).</span><span class="sxs-lookup"><span data-stu-id="b19a7-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
