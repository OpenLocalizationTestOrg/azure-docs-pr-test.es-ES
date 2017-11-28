---
title: "aaaSet la clave de almacén para máquinas virtuales de Windows en el Administrador de recursos de Azure | Documentos de Microsoft"
description: "Cómo tooset el almacén de claves para su uso con una máquina virtual de Azure Resource Manager."
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
ms.openlocfilehash: 53bbe90708202ecfdcf754822d04bf2469631f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="346f9-103">Configuración de un Almacén de claves para máquinas virtuales en Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="346f9-103">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="346f9-104">En la pila del Administrador de recursos de Azure, los secretos/certificados se modelan como recursos proporcionados por el proveedor de recursos de Hola de almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="346f9-104">In Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by hello resource provider of Key Vault.</span></span> <span data-ttu-id="346f9-105">toolearn más información sobre el almacén de claves, consulte [¿qué es el almacén de claves de Azure?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="346f9-105">toolearn more about Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span>

> [!NOTE]
> 1. <span data-ttu-id="346f9-106">En orden para toobe de almacén de claves que se utiliza con máquinas virtuales del Administrador de recursos de Azure, Hola **EnabledForDeployment** propiedad en el almacén de claves se debe establecer tootrue.</span><span class="sxs-lookup"><span data-stu-id="346f9-106">In order for Key Vault toobe used with Azure Resource Manager virtual machines, hello **EnabledForDeployment** property on Key Vault must be set tootrue.</span></span> <span data-ttu-id="346f9-107">Puede hacer esto en varios clientes.</span><span class="sxs-lookup"><span data-stu-id="346f9-107">You can do this in various clients.</span></span>
> 2. <span data-ttu-id="346f9-108">necesidades del almacén de claves de Hello toobe creado en Hola misma suscripción y ubicación como Hola Máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="346f9-108">hello Key Vault needs toobe created in hello same subscription and location as hello Virtual Machine.</span></span>
>
>

## <a name="use-powershell-tooset-up-key-vault"></a><span data-ttu-id="346f9-109">Usar PowerShell tooset el almacén de claves</span><span class="sxs-lookup"><span data-stu-id="346f9-109">Use PowerShell tooset up Key Vault</span></span>
<span data-ttu-id="346f9-110">toocreate un almacén de claves mediante PowerShell, consulte [empezar a trabajar con el almacén de claves de Azure](../../key-vault/key-vault-get-started.md#vault).</span><span class="sxs-lookup"><span data-stu-id="346f9-110">toocreate a key vault by using PowerShell, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md#vault).</span></span>

<span data-ttu-id="346f9-111">Para almacenes de claves nuevos, puede usar este cmdlet de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="346f9-111">For new key vaults, you can use this PowerShell cmdlet:</span></span>

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -EnabledForDeployment

<span data-ttu-id="346f9-112">Para almacenes de claves existentes, puede usar este cmdlet de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="346f9-112">For existing key vaults, you can use this PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

## <a name="us-cli-tooset-up-key-vault"></a><span data-ttu-id="346f9-113">Nos CLI tooset el almacén de claves</span><span class="sxs-lookup"><span data-stu-id="346f9-113">Us CLI tooset up Key Vault</span></span>
<span data-ttu-id="346f9-114">toocreate un almacén de claves mediante Hola interfaz de línea de comandos (CLI), consulte [administrar el almacén de claves con CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span><span class="sxs-lookup"><span data-stu-id="346f9-114">toocreate a key vault by using hello command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="346f9-115">Para CLI, es necesario el almacén de claves de hello toocreate antes de asignar la directiva de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="346f9-115">For CLI, you have toocreate hello key vault before you assign hello deployment policy.</span></span> <span data-ttu-id="346f9-116">Puede hacerlo mediante el uso de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="346f9-116">You can do this by using hello following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a><span data-ttu-id="346f9-117">Usar plantillas tooset el almacén de claves</span><span class="sxs-lookup"><span data-stu-id="346f9-117">Use templates tooset up Key Vault</span></span>
<span data-ttu-id="346f9-118">Mientras usa una plantilla, deberá hello tooset `enabledForDeployment` propiedad demasiado`true` para hello recursos de almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="346f9-118">While you use a template, you need tooset hello `enabledForDeployment` property too`true` for hello Key Vault resource.</span></span>

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

<span data-ttu-id="346f9-119">Para otras opciones que puede configurar al crear un almacén de claves mediante plantillas, consulte [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/)(Creación de un almacén de claves).</span><span class="sxs-lookup"><span data-stu-id="346f9-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
