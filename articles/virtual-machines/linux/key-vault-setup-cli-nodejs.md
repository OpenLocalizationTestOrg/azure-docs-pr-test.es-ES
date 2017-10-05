---
title: "Configuración de Key Vault para máquinas virtuales Linux con la CLI de Azure 1.0 | Microsoft Docs"
description: "Configuración de Key Vault para usarlo con una máquina virtual de Azure Resource Manager con la CLI 1.0 de Azure."
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
ms.openlocfilehash: fed612a354d45f34619f2a66bd40d78740c43ac7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager-with-the-azure-cli-10"></a><span data-ttu-id="4153b-103">Configuración de Key Vault para máquinas virtuales en Azure Resource Manager con la CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="4153b-103">Set up Key Vault for virtual machines in Azure Resource Manager with the Azure CLI 1.0</span></span>
<span data-ttu-id="4153b-104">En la pila de Azure Resource Manager, los certificados o secretos se modelan como recursos que se proporcionan mediante el proveedor de recursos de Key Vault.</span><span class="sxs-lookup"><span data-stu-id="4153b-104">In the Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by the resource provider of Key Vault.</span></span> <span data-ttu-id="4153b-105">Para más información sobre el Almacén de claves de Azure, consulte [¿Qué es el Almacén de claves de Azure?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="4153b-105">To learn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="4153b-106">Para que un Almacén de claves se utilice con máquinas virtuales de Azure Resource Manager, la propiedad *EnabledForDeployment* del Almacén de claves se debe establecer en true.</span><span class="sxs-lookup"><span data-stu-id="4153b-106">In order for Key Vault to be used with Azure Resource Manager virtual machines, the *EnabledForDeployment* property on Key Vault must be set to true.</span></span> <span data-ttu-id="4153b-107">Puede hacer esto en varios clientes.</span><span class="sxs-lookup"><span data-stu-id="4153b-107">You can do this in various clients.</span></span> <span data-ttu-id="4153b-108">En este artículo se muestra cómo configurar Key Vault para su uso con Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="4153b-108">This article shows you how to set up Key Vault for use with Azure Virtual Machines.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="4153b-109">Versiones de la CLI para completar la tarea</span><span class="sxs-lookup"><span data-stu-id="4153b-109">CLI versions to complete the task</span></span>
<span data-ttu-id="4153b-110">Puede completar la tarea mediante una de las siguientes versiones de la CLI</span><span class="sxs-lookup"><span data-stu-id="4153b-110">You can complete the task using one of the following CLI versions</span></span>

- <span data-ttu-id="4153b-111">[CLI de Azure 1.0](#quick-commands): la CLI para los modelos de implementación clásico y de Resource Manager (este artículo)</span><span class="sxs-lookup"><span data-stu-id="4153b-111">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="4153b-112">[CLI de Azure 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json): la CLI de última generación para el modelo de implementación de administración de recursos.</span><span class="sxs-lookup"><span data-stu-id="4153b-112">[Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="use-cli-10-to-set-up-key-vault"></a><span data-ttu-id="4153b-113">Uso de la CLI 1.0 para configurar Key Vault</span><span class="sxs-lookup"><span data-stu-id="4153b-113">Use CLI 1.0 to set up Key Vault</span></span>
<span data-ttu-id="4153b-114">Para crear un almacén de claves mediante la interfaz de la línea de comandos (CLI), consulte [Administración del Almacén de claves mediante CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span><span class="sxs-lookup"><span data-stu-id="4153b-114">To create a key vault by using the command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="4153b-115">Para la CLI 1.0, primero debe crear el almacén de claves y luego asignar la directiva de implementación.</span><span class="sxs-lookup"><span data-stu-id="4153b-115">For CLI 1.0, you have to create the key vault before you assign the deployment policy.</span></span> <span data-ttu-id="4153b-116">A continuación, puede asignar la directiva mediante el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="4153b-116">You can then assign the policy by using the following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-to-set-up-key-vault"></a><span data-ttu-id="4153b-117">Uso de plantillas para configurar el Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="4153b-117">Use templates to set up Key Vault</span></span>
<span data-ttu-id="4153b-118">Al utilizar plantillas, debe configurar la propiedad `enabledForDeployment` como `true` para el recurso del Almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="4153b-118">When you use a template, you need to set the `enabledForDeployment` property to `true` for the Key Vault resource.</span></span>

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

<span data-ttu-id="4153b-119">Para otras opciones que puede configurar al crear un almacén de claves mediante plantillas, consulte [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/)(Creación de un almacén de claves).</span><span class="sxs-lookup"><span data-stu-id="4153b-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
