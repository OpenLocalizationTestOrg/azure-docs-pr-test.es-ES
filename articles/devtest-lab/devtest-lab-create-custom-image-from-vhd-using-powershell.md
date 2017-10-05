---
title: "Creación de una imagen personalizada en Azure DevTest Labs a partir de un archivo VHD mediante PowerShell | Microsoft Docs"
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
ms.openlocfilehash: a4729f70aae80a13233fbe96a5d8a56c0c9d01d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-from-a-vhd-file-using-powershell"></a><span data-ttu-id="728a0-103">Creación de una imagen personalizada a partir de un archivo VHD mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="728a0-103">Create a custom image from a VHD file using PowerShell</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="728a0-104">Instrucciones paso a paso</span><span class="sxs-lookup"><span data-stu-id="728a0-104">Step-by-step instructions</span></span>

<span data-ttu-id="728a0-105">Los siguientes pasos le guían en la creación de una imagen personalizada a partir de un archivo VHD mediante PowerShell:</span><span class="sxs-lookup"><span data-stu-id="728a0-105">The following steps walk you through creating a custom image from a VHD file using PowerShell:</span></span>

1. <span data-ttu-id="728a0-106">En un símbolo del sistema de PowerShell, inicie sesión en su cuenta de Azure con la siguiente llamada al cmdlet **Login-AzureRmAccount**.</span><span class="sxs-lookup"><span data-stu-id="728a0-106">At a PowerShell prompt, log in to your Azure account with the following call to the **Login-AzureRmAccount** cmdlet.</span></span>  
    
    ```PowerShell
    Login-AzureRmAccount
    ```

1.  <span data-ttu-id="728a0-107">Seleccione la suscripción de Azure deseada mediante una llamada al cmdlet **Select-AzureRmSubscription**.</span><span class="sxs-lookup"><span data-stu-id="728a0-107">Select the desired Azure subscription by calling the **Select-AzureRmSubscription** cmdlet.</span></span> <span data-ttu-id="728a0-108">Reemplace el marcador de posición siguiente de la variable **$subscriptionId** por un identificador de suscripción válido de Azure.</span><span class="sxs-lookup"><span data-stu-id="728a0-108">Replace the following placeholder for the **$subscriptionId** variable with a valid Azure subscription ID.</span></span> 

    ```PowerShell
    $subscriptionId = '<Specify your subscription ID here>'
    Select-AzureRmSubscription -SubscriptionId $subscriptionId
    ```

1.  <span data-ttu-id="728a0-109">Obtenga el objeto de laboratorio mediante la llamada al cmdlet **Get-AzureRmResource**.</span><span class="sxs-lookup"><span data-stu-id="728a0-109">Get the lab object by calling the **Get-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="728a0-110">Reemplace los siguientes marcadores de posición de las variables **$labRg** y **$labName** por los valores adecuados para su entorno.</span><span class="sxs-lookup"><span data-stu-id="728a0-110">Replace the following placeholders for the **$labRg** and **$labName** variables with the appropriate values for your environment.</span></span> 

    ```PowerShell
    $labRg = '<Specify your lab resource group name here>'
    $labName = '<Specify your lab name here>'
    $lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    ```
 
1.  <span data-ttu-id="728a0-111">Obtenga la cuenta de almacenamiento del laboratorio y sus valores de clave del objeto de laboratorio.</span><span class="sxs-lookup"><span data-stu-id="728a0-111">Get the lab storage account and lab storage account key values from the lab object.</span></span> 

    ```PowerShell
    $labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
    $labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value
    ```

1.  <span data-ttu-id="728a0-112">Reemplace el siguiente marcador de posición de la variable **$vhdUri** por el identificador URI al archivo VHD cargado.</span><span class="sxs-lookup"><span data-stu-id="728a0-112">Replace the following placeholder for the **$vhdUri** variable with the URI to your uploaded VHD file.</span></span> <span data-ttu-id="728a0-113">Puede obtener el identificador URI del archivo VHD en la hoja del blob de la cuenta de almacenamiento en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="728a0-113">You can get the VHD file's URI from the storage account's blob blade in the Azure portal.</span></span>

    ```PowerShell
    $vhdUri = '<Specify the VHD URI here>'
    ```

1.  <span data-ttu-id="728a0-114">Cree la imagen personalizada mediante el cmdlet **New-AzureRmResourceGroupDeployment**.</span><span class="sxs-lookup"><span data-stu-id="728a0-114">Create the custom image using the **New-AzureRmResourceGroupDeployment** cmdlet.</span></span> <span data-ttu-id="728a0-115">Reemplace los siguientes marcadores de posición de las variables **$customImageName** y **$customImageDescription** por nombres significativos en su entorno.</span><span class="sxs-lookup"><span data-stu-id="728a0-115">Replace the following placeholders for the **$customImageName** and **$customImageDescription** variables to meaningful names for your environment.</span></span>

    ```PowerShell
    $customImageName = '<Specify the custom image name>'
    $customImageDescription = '<Specify the custom image description>'

    $parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

    New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
    ```

## <a name="powershell-script-to-create-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="728a0-116">Script de PowerShell para crear una imagen personalizada a partir de un archivo VHD</span><span class="sxs-lookup"><span data-stu-id="728a0-116">PowerShell script to create a custom image from a VHD file</span></span>

<span data-ttu-id="728a0-117">El siguiente script de PowerShell se puede usar para crear una imagen personalizada a partir de un archivo VHD.</span><span class="sxs-lookup"><span data-stu-id="728a0-117">The following PowerShell script can be used to create a custom image from a VHD file.</span></span> <span data-ttu-id="728a0-118">Reemplace los marcadores de posición (inicio y fin con corchetes angulares) por los valores adecuados según sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="728a0-118">Replace the placeholders (starting and ending with angle brackets) with the appropriate values for your needs.</span></span> 

```PowerShell
# Log in to your Azure account.  
Login-AzureRmAccount

# Select the desired Azure subscription. 
$subscriptionId = '<Specify your subscription ID here>'
Select-AzureRmSubscription -SubscriptionId $subscriptionId

# Get the lab object.
$labRg = '<Specify your lab resource group name here>'
$labName = '<Specify your lab name here>'
$lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)

# Get the lab storage account and lab storage account key values.
$labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
$labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value

# Set the URI of the VHD file.  
$vhdUri = '<Specify the VHD URI here>'

# Set the custom image name and description values.
$customImageName = '<Specify the custom image name>'
$customImageDescription = '<Specify the custom image description>'

# Set up the parameters object.
$parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

# Create the custom image. 
New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
```

## <a name="related-blog-posts"></a><span data-ttu-id="728a0-119">Entradas blogs relacionadas</span><span class="sxs-lookup"><span data-stu-id="728a0-119">Related blog posts</span></span>

- [<span data-ttu-id="728a0-120">Custom images or formulas? (¿Imágenes personalizadas o fórmulas?)</span><span class="sxs-lookup"><span data-stu-id="728a0-120">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="728a0-121">Copying Custom Images between Azure DevTest Labs (Copiar imágenes personalizadas entre instancias de Azure DevTest Labs)</span><span class="sxs-lookup"><span data-stu-id="728a0-121">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="728a0-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="728a0-122">Next steps</span></span>

- [<span data-ttu-id="728a0-123">Agregar una máquina virtual al laboratorio</span><span class="sxs-lookup"><span data-stu-id="728a0-123">Add a VM to your lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
