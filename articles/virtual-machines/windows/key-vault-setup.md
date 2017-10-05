---
title: "Configuración de Key Vault para máquinas virtuales Windows en Azure Resource Manager | Microsoft Docs"
description: "Cómo configurar un Almacén de claves para usarlo con una máquina virtual de Azure Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 33a483e2-cfbc-4c62-a588-5d9fd52491e2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: kasing
ms.openlocfilehash: a5083a5216efbfd76fd912ec48c2f0ec3b30c4a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="cae07-103">Configuración de un Almacén de claves para máquinas virtuales en Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cae07-103">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="cae07-104">En la pila de Azure Resource Manager, los certificados o secretos se modelan como recursos que se proporcionan mediante el proveedor de recursos del Almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="cae07-104">In Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by the resource provider of Key Vault.</span></span> <span data-ttu-id="cae07-105">Para más información sobre el Almacén de claves, consulte [¿Qué es el Almacén de claves de Azure?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="cae07-105">To learn more about Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span>

> [!NOTE]
> 1. <span data-ttu-id="cae07-106">Para que un Almacén de claves se utilice con máquinas virtuales de Azure Resource Manager, la propiedad **EnabledForDeployment** del Almacén de claves se debe establecer en true.</span><span class="sxs-lookup"><span data-stu-id="cae07-106">In order for Key Vault to be used with Azure Resource Manager virtual machines, the **EnabledForDeployment** property on Key Vault must be set to true.</span></span> <span data-ttu-id="cae07-107">Puede hacer esto en varios clientes.</span><span class="sxs-lookup"><span data-stu-id="cae07-107">You can do this in various clients.</span></span>
> 2. <span data-ttu-id="cae07-108">El Almacén de claves debe crearse en la misma ubicación y suscripción que la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cae07-108">The Key Vault needs to be created in the same subscription and location as the Virtual Machine.</span></span>
>
>

## <a name="use-powershell-to-set-up-key-vault"></a><span data-ttu-id="cae07-109">Uso de PowerShell para configurar el Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="cae07-109">Use PowerShell to set up Key Vault</span></span>
<span data-ttu-id="cae07-110">Para crear un almacén de claves usando PowerShell, consulte [Introducción al Almacén de claves de Azure](../../key-vault/key-vault-get-started.md#vault).</span><span class="sxs-lookup"><span data-stu-id="cae07-110">To create a key vault by using PowerShell, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md#vault).</span></span>

<span data-ttu-id="cae07-111">Para almacenes de claves nuevos, puede usar este cmdlet de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="cae07-111">For new key vaults, you can use this PowerShell cmdlet:</span></span>

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -EnabledForDeployment

<span data-ttu-id="cae07-112">Para almacenes de claves existentes, puede usar este cmdlet de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="cae07-112">For existing key vaults, you can use this PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

## <a name="us-cli-to-set-up-key-vault"></a><span data-ttu-id="cae07-113">Uso de la CLI para configurar el Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="cae07-113">Us CLI to set up Key Vault</span></span>
<span data-ttu-id="cae07-114">Para crear un almacén de claves mediante la interfaz de la línea de comandos (CLI), consulte [Administración del Almacén de claves mediante CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span><span class="sxs-lookup"><span data-stu-id="cae07-114">To create a key vault by using the command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="cae07-115">Para la CLI, primero debe crear el almacén de claves y luego asignar la directiva de implementación.</span><span class="sxs-lookup"><span data-stu-id="cae07-115">For CLI, you have to create the key vault before you assign the deployment policy.</span></span> <span data-ttu-id="cae07-116">Para ello, puede usar el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="cae07-116">You can do this by using the following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-to-set-up-key-vault"></a><span data-ttu-id="cae07-117">Uso de plantillas para configurar el Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="cae07-117">Use templates to set up Key Vault</span></span>
<span data-ttu-id="cae07-118">Al utilizar plantillas, deberá establecer la propiedad `enabledForDeployment` en `true` para el recurso de Almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="cae07-118">While you use a template, you need to set the `enabledForDeployment` property to `true` for the Key Vault resource.</span></span>

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

<span data-ttu-id="cae07-119">Para otras opciones que puede configurar al crear un almacén de claves mediante plantillas, consulte [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/)(Creación de un almacén de claves).</span><span class="sxs-lookup"><span data-stu-id="cae07-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
