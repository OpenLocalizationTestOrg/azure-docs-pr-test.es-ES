---
title: aaaCreate una imagen personalizada de laboratorios de desarrollo y pruebas de Azure desde un archivo de disco duro virtual mediante PowerShell | Documentos de Microsoft
description: "Automatización de la creación de una imagen personalizada en Azure DevTest Labs a partir de un archivo VHD mediante PowerShell"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 39b4005fa46cdf86cf0800ca376128134bcfb650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vhd-file-using-powershell"></a><span data-ttu-id="3eced-103">Creación de una imagen personalizada a partir de un archivo VHD mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="3eced-103">Create a custom image from a VHD file using PowerShell</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="3eced-104">Instrucciones paso a paso</span><span class="sxs-lookup"><span data-stu-id="3eced-104">Step-by-step instructions</span></span>

<span data-ttu-id="3eced-105">Hello pasos siguientes le guían por la creación de una imagen personalizada desde un archivo de disco duro virtual con PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3eced-105">hello following steps walk you through creating a custom image from a VHD file using PowerShell:</span></span>

1. <span data-ttu-id="3eced-106">En un símbolo del sistema de PowerShell, inicie sesión tooyour cuenta de Azure con hello después llamada toohello **AzureRmAccount de inicio de sesión** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3eced-106">At a PowerShell prompt, log in tooyour Azure account with hello following call toohello **Login-AzureRmAccount** cmdlet.</span></span>  
    
    ```PowerShell
    Login-AzureRmAccount
    ```

1.  <span data-ttu-id="3eced-107">Seleccione Hola deseado suscripción de Azure por llamada hello **AzureRmSubscription seleccione** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3eced-107">Select hello desired Azure subscription by calling hello **Select-AzureRmSubscription** cmdlet.</span></span> <span data-ttu-id="3eced-108">Reemplace Hola siguiente marcador de posición para hello **$subscriptionId** variable con un identificador de suscripción válida a Azure.</span><span class="sxs-lookup"><span data-stu-id="3eced-108">Replace hello following placeholder for hello **$subscriptionId** variable with a valid Azure subscription ID.</span></span> 

    ```PowerShell
    $subscriptionId = '<Specify your subscription ID here>'
    Select-AzureRmSubscription -SubscriptionId $subscriptionId
    ```

1.  <span data-ttu-id="3eced-109">Obtener objetos de laboratorio de Hola Hola llamada **Get-AzureRmResource** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3eced-109">Get hello lab object by calling hello **Get-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="3eced-110">Reemplace Hola siguientes marcadores de posición para hello **$labRg** y **$labName** variables con hello los valores adecuados para su entorno.</span><span class="sxs-lookup"><span data-stu-id="3eced-110">Replace hello following placeholders for hello **$labRg** and **$labName** variables with hello appropriate values for your environment.</span></span> 

    ```PowerShell
    $labRg = '<Specify your lab resource group name here>'
    $labName = '<Specify your lab name here>'
    $lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    ```
 
1.  <span data-ttu-id="3eced-111">Obtener cuenta de almacenamiento del laboratorio de Hola y cuenta de almacenamiento de laboratorio valores de clave del objeto de laboratorio Hola.</span><span class="sxs-lookup"><span data-stu-id="3eced-111">Get hello lab storage account and lab storage account key values from hello lab object.</span></span> 

    ```PowerShell
    $labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
    $labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value
    ```

1.  <span data-ttu-id="3eced-112">Reemplace Hola siguiente marcador de posición para hello **$vhdUri** variable con hello URI tooyour cargar archivo de disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="3eced-112">Replace hello following placeholder for hello **$vhdUri** variable with hello URI tooyour uploaded VHD file.</span></span> <span data-ttu-id="3eced-113">Puede obtener el URI del archivo de disco duro virtual de Hola de hoja de blob de la cuenta de almacenamiento de Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3eced-113">You can get hello VHD file's URI from hello storage account's blob blade in hello Azure portal.</span></span>

    ```PowerShell
    $vhdUri = '<Specify hello VHD URI here>'
    ```

1.  <span data-ttu-id="3eced-114">Crear imagen personalizada de hello con hello **AzureRmResourceGroupDeployment New** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3eced-114">Create hello custom image using hello **New-AzureRmResourceGroupDeployment** cmdlet.</span></span> <span data-ttu-id="3eced-115">Reemplace Hola siguientes marcadores de posición para hello **$customImageName** y **$customImageDescription** nombres de variables toomeaningful para su entorno.</span><span class="sxs-lookup"><span data-stu-id="3eced-115">Replace hello following placeholders for hello **$customImageName** and **$customImageDescription** variables toomeaningful names for your environment.</span></span>

    ```PowerShell
    $customImageName = '<Specify hello custom image name>'
    $customImageDescription = '<Specify hello custom image description>'

    $parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

    New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
    ```

## <a name="powershell-script-toocreate-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="3eced-116">Script de PowerShell toocreate una imagen personalizada desde un archivo de disco duro virtual</span><span class="sxs-lookup"><span data-stu-id="3eced-116">PowerShell script toocreate a custom image from a VHD file</span></span>

<span data-ttu-id="3eced-117">Hola siguiente script de PowerShell pueden toocreate usa una imagen personalizada desde un archivo de disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="3eced-117">hello following PowerShell script can be used toocreate a custom image from a VHD file.</span></span> <span data-ttu-id="3eced-118">Reemplace los marcadores de posición de hello (inicial y final con corchetes angulares) con los valores adecuados de Hola para sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="3eced-118">Replace hello placeholders (starting and ending with angle brackets) with hello appropriate values for your needs.</span></span> 

```PowerShell
# Log in tooyour Azure account.  
Login-AzureRmAccount

# Select hello desired Azure subscription. 
$subscriptionId = '<Specify your subscription ID here>'
Select-AzureRmSubscription -SubscriptionId $subscriptionId

# Get hello lab object.
$labRg = '<Specify your lab resource group name here>'
$labName = '<Specify your lab name here>'
$lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)

# Get hello lab storage account and lab storage account key values.
$labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
$labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value

# Set hello URI of hello VHD file.  
$vhdUri = '<Specify hello VHD URI here>'

# Set hello custom image name and description values.
$customImageName = '<Specify hello custom image name>'
$customImageDescription = '<Specify hello custom image description>'

# Set up hello parameters object.
$parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

# Create hello custom image. 
New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
```

## <a name="related-blog-posts"></a><span data-ttu-id="3eced-119">Entradas blogs relacionadas</span><span class="sxs-lookup"><span data-stu-id="3eced-119">Related blog posts</span></span>

- [<span data-ttu-id="3eced-120">Custom images or formulas? (¿Imágenes personalizadas o fórmulas?)</span><span class="sxs-lookup"><span data-stu-id="3eced-120">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="3eced-121">Copying Custom Images between Azure DevTest Labs (Copiar imágenes personalizadas entre instancias de Azure DevTest Labs)</span><span class="sxs-lookup"><span data-stu-id="3eced-121">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="3eced-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3eced-122">Next steps</span></span>

- [<span data-ttu-id="3eced-123">Agregar un laboratorio de tooyour VM</span><span class="sxs-lookup"><span data-stu-id="3eced-123">Add a VM tooyour lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
