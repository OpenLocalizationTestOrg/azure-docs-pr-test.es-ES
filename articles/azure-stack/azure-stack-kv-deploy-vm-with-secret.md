---
title: "Implementación de una máquina virtual con una contraseña almacenada de forma segura en Azure Stack | Microsoft Docs"
description: "Aprenda a implementar una máquina virtual usando una contraseña almacenada en el almacén de claves de Azure Stack"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 23322a49-fb7e-4dc2-8d0e-43de8cd41f80
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/08/2017
ms.author: sngun
ms.openlocfilehash: a1137ffefbc3fafbd7e9492819058f6a72537e22
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-virtual-machine-by-retrieving-the-password-stored-in-a-key-vault"></a><span data-ttu-id="32f0f-103">Creación de una máquina virtual mediante la recuperación de la contraseña almacenada en un almacén de claves</span><span class="sxs-lookup"><span data-stu-id="32f0f-103">Create a virtual machine by retrieving the password stored in a Key Vault</span></span>

<span data-ttu-id="32f0f-104">Si necesita pasar un valor seguro, como una contraseña, durante la implementación, puede almacenar ese valor como un secreto en un almacén de claves de Azure Stack y hacer referencia al secreto en las plantillas de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="32f0f-104">When you need to pass a secure value such as a password during deployment, you can store that value as a secret in an Azure Stack key vault and reference it in the Azure Resource Manager templates.</span></span> <span data-ttu-id="32f0f-105">No tiene que escribir manualmente el secreto cada vez que implemente los recursos, solo tiene que especificar qué usuarios o entidades de servicio pueden tener acceso al secreto.</span><span class="sxs-lookup"><span data-stu-id="32f0f-105">You do not need to manually enter the secret each time you deploy the resources, you can also specify which users or service principals can access the secret.</span></span> 

<span data-ttu-id="32f0f-106">En este artículo, se le guiará por los pasos necesarios para implementar una máquina virtual Windows en Azure Stack mediante la recuperación de la contraseña que está guardada en un almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="32f0f-106">In this article, we walk you through the steps required to deploy a Windows virtual machine in Azure Stack by retrieving the password that is stored in a Key Vault.</span></span> <span data-ttu-id="32f0f-107">Por lo tanto, la contraseña nunca se coloca en texto sin formato en el archivo de parámetros de plantilla.</span><span class="sxs-lookup"><span data-stu-id="32f0f-107">Therefore the password is never put in plain text in the template parameter file.</span></span> <span data-ttu-id="32f0f-108">Puede seguir los pasos descritos aquí ya sea desde Azure Stack Development Kit o desde un cliente externo, si se conecta a través de VPN.</span><span class="sxs-lookup"><span data-stu-id="32f0f-108">You can use these steps either from the Azure Stack Development Kit, or from an external client if you are connected through VPN.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32f0f-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="32f0f-109">Prerequisites</span></span>

* <span data-ttu-id="32f0f-110">Los administradores de nube de Azure Stack tienen que haber [creado una oferta](azure-stack-create-offer.md) que incluya el servicio Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="32f0f-110">Azure Stack cloud administrators must have [created an offer](azure-stack-create-offer.md) that includes the Azure Key Vault service.</span></span>  
* <span data-ttu-id="32f0f-111">Los usuarios tienen que [suscribirse a una oferta](azure-stack-subscribe-plan-provision-vm.md) que incluya el servicio Key Vault.</span><span class="sxs-lookup"><span data-stu-id="32f0f-111">Users must [subscribe to an offer](azure-stack-subscribe-plan-provision-vm.md) that includes the Key Vault service.</span></span>  
* [<span data-ttu-id="32f0f-112">Instalación de PowerShell para Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="32f0f-112">Install PowerShell for Azure Stack.</span></span>](azure-stack-powershell-install.md)  
* [<span data-ttu-id="32f0f-113">Configuración del entorno de PowerShell del usuario de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="32f0f-113">Configure the Azure Stack user's PowerShell environment.</span></span>](azure-stack-powershell-configure-user.md)

<span data-ttu-id="32f0f-114">Los pasos siguientes describen el proceso necesario para crear una máquina virtual mediante la recuperación de la contraseña almacenada en un almacén de claves:</span><span class="sxs-lookup"><span data-stu-id="32f0f-114">The following steps describe the process required to create a virtual machine by retrieving the password stored in a Key Vault:</span></span>

1. <span data-ttu-id="32f0f-115">Cree un secreto de almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="32f0f-115">Create a Key Vault secret.</span></span>
2. <span data-ttu-id="32f0f-116">Actualice el archivo azuredeploy.parameters.json.</span><span class="sxs-lookup"><span data-stu-id="32f0f-116">Update the azuredeploy.parameters.json file.</span></span>
3. <span data-ttu-id="32f0f-117">Implemente la plantilla.</span><span class="sxs-lookup"><span data-stu-id="32f0f-117">Deploy the template.</span></span>

## <a name="create-a-key-vault-secret"></a><span data-ttu-id="32f0f-118">Creación de un secreto de almacén de claves</span><span class="sxs-lookup"><span data-stu-id="32f0f-118">Create a Key Vault secret</span></span>

<span data-ttu-id="32f0f-119">El script siguiente crea un almacén de claves y almacena en él una contraseña como un secreto.</span><span class="sxs-lookup"><span data-stu-id="32f0f-119">The following script creates a key vault, and stores a password in the key vault as a secret.</span></span> <span data-ttu-id="32f0f-120">Use el parámetro `-EnabledForDeployment` al crear el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="32f0f-120">Use the `-EnabledForDeployment` parameter when you're creating the key vault.</span></span> <span data-ttu-id="32f0f-121">Este parámetro se asegura de que se puede hacer referencia al almacén de claves desde las plantillas de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="32f0f-121">This parameter makes sure that the key vault can be referenced from Azure Resource Manager templates.</span></span>

```powershell

$vaultName = "contosovault"
$resourceGroup = "contosovaultrg"
$location = "local"
$secretName = "MySecret"

New-AzureRmResourceGroup `
  -Name $resourceGroup `
  -Location $location

New-AzureRmKeyVault `
  -VaultName $vaultName `
  -ResourceGroupName $resourceGroup `
  -Location $location
  -EnabledForTemplateDeployment

$secretValue = ConvertTo-SecureString -String '<Password for your virtual machine>' -AsPlainText -Force

Set-AzureKeyVaultSecret `
  -VaultName $vaultName `
  -Name $secretName `
  -SecretValue $secretValue

```

<span data-ttu-id="32f0f-122">Cuando se ejecuta el script anterior, la salida incluye el identificador URI del secreto.</span><span class="sxs-lookup"><span data-stu-id="32f0f-122">When you run the previous script, the output includes the secret URI.</span></span> <span data-ttu-id="32f0f-123">Anote este URI.</span><span class="sxs-lookup"><span data-stu-id="32f0f-123">Make a note of this URI.</span></span> <span data-ttu-id="32f0f-124">Tendrá que hacer referencia a él durante la [implementación de máquina virtual Windows con contraseña en la plantilla de almacén de claves](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-secure-password).</span><span class="sxs-lookup"><span data-stu-id="32f0f-124">You have to reference it in the [Deploy Windows virtual machine with password in key vault template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-secure-password).</span></span> <span data-ttu-id="32f0f-125">Descargue la carpeta [101-vm-secure-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-secure-password) en el equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="32f0f-125">Download the [101-vm-secure-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-secure-password) folder onto your development computer.</span></span> <span data-ttu-id="32f0f-126">Esta carpeta contiene los archivos `azuredeploy.json` y `azuredeploy.parameters.json` que necesitará en los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="32f0f-126">This folder contains the `azuredeploy.json` and `azuredeploy.parameters.json` files, which you will need in the next steps.</span></span>

<span data-ttu-id="32f0f-127">Modificar el archivo `azuredeploy.parameters.json` según los valores del entorno.</span><span class="sxs-lookup"><span data-stu-id="32f0f-127">Modify the `azuredeploy.parameters.json` file according to your environment values.</span></span> <span data-ttu-id="32f0f-128">Los parámetros de especial interés son el nombre del almacén, el grupo de recursos del almacén y el identificador URI del secreto (que se generó en el script anterior).</span><span class="sxs-lookup"><span data-stu-id="32f0f-128">The parameters of special interest are the vault name, the vault resource group, and the secret URI (as generated by the previous script).</span></span> <span data-ttu-id="32f0f-129">El archivo siguiente es un ejemplo de un archivo de parámetros:</span><span class="sxs-lookup"><span data-stu-id="32f0f-129">The following file is an example of a parameter file:</span></span>

## <a name="update-the-azuredeployparametersjson-file"></a><span data-ttu-id="32f0f-130">Actualice el archivo azuredeploy.parameters.json</span><span class="sxs-lookup"><span data-stu-id="32f0f-130">Update the azuredeploy.parameters.json file</span></span>

<span data-ttu-id="32f0f-131">Actualice el archivo azuredeploy.parameters.json con los valores de KeyVault URI, secretName y adminUsername de la máquina virtual correspondientes a su entorno.</span><span class="sxs-lookup"><span data-stu-id="32f0f-131">Update the azuredeploy.parameters.json file with the KeyVault URI, secretName, adminUsername of the virtual machine values as per your environment.</span></span> <span data-ttu-id="32f0f-132">El siguiente archivo JSON muestra un ejemplo del archivo de parámetros de plantilla:</span><span class="sxs-lookup"><span data-stu-id="32f0f-132">The following JSON file shows an example of the template parameters file:</span></span> 

```json
{
    "$schema":  "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion":  "1.0.0.0",
    "parameters":  {
       "adminUsername":  {
         "value":  "demouser"
          },
         "adminPassword":  {
           "reference":  {
              "keyVault":  {
                "id":  "/subscriptions/xxxxxx/resourceGroups/RgKvPwd/providers/Microsoft.KeyVault/vaults/KvPwd"
                },
              "secretName":  "MySecret"
           }
         },
       "dnsLabelPrefix":  {
          "value":  "mydns123456"
        },
        "windowsOSVersion":  {
          "value":  "2016-Datacenter"
        }
    }
}

```

## <a name="template-deployment"></a><span data-ttu-id="32f0f-133">Implementación de plantilla</span><span class="sxs-lookup"><span data-stu-id="32f0f-133">Template deployment</span></span>

<span data-ttu-id="32f0f-134">Ahora implemente la plantilla con el siguiente script de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="32f0f-134">Now deploy the template by using the following PowerShell script:</span></span>

```powershell
New-AzureRmResourceGroupDeployment `
  -Name KVPwdDeployment `
  -ResourceGroupName $resourceGroup `
  -TemplateFile "<Fully qualified path to the azuredeploy.json file>" `
  -TemplateParameterFile "<Fully qualified path to the azuredeploy.parameters.json file>"
```
<span data-ttu-id="32f0f-135">Cuando la plantilla se ha implementado correctamente, se producen en la siguiente salida:</span><span class="sxs-lookup"><span data-stu-id="32f0f-135">When the template is deployed successfully, it results in the following output:</span></span>

![Salida de la implementación](media\azure-stack-kv-deploy-vm-with-secret/deployment-output.png)


## <a name="next-steps"></a><span data-ttu-id="32f0f-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="32f0f-137">Next steps</span></span>
[<span data-ttu-id="32f0f-138">Implementación de una aplicación de ejemplo con Key Vault</span><span class="sxs-lookup"><span data-stu-id="32f0f-138">Deploy a sample app with Key Vault</span></span>](azure-stack-kv-sample-app.md)

[<span data-ttu-id="32f0f-139">Implementación de una máquina virtual con un certificado de Key Vault</span><span class="sxs-lookup"><span data-stu-id="32f0f-139">Deploy a VM with a Key Vault certificate</span></span>](azure-stack-kv-push-secret-into-vm.md)

