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
ms.openlocfilehash: 3292a2dfefc17e5034c66122a3eab24d6c03e694
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2017
---
# <a name="create-a-virtual-machine-by-retrieving-the-password-stored-in-a-key-vault"></a><span data-ttu-id="6dc4d-103">Creación de una máquina virtual mediante la recuperación de la contraseña almacenada en un almacén de claves</span><span class="sxs-lookup"><span data-stu-id="6dc4d-103">Create a virtual machine by retrieving the password stored in a Key Vault</span></span>

<span data-ttu-id="6dc4d-104">Si necesita pasar un valor seguro, como una contraseña, durante la implementación, puede almacenar ese valor como un secreto en un almacén de claves de Azure Stack y hacer referencia al secreto en las plantillas de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6dc4d-104">When you need to pass a secure value such as a password during deployment, you can store that value as a secret in an Azure Stack key vault and reference it in the Azure Resource Manager templates.</span></span> <span data-ttu-id="6dc4d-105">No tiene que escribir manualmente el secreto cada vez que implemente los recursos, solo tiene que especificar qué usuarios o entidades de servicio pueden tener acceso al secreto.</span><span class="sxs-lookup"><span data-stu-id="6dc4d-105">You do not need to manually enter the secret each time you deploy the resources, you can also specify which users or service principals can access the secret.</span></span> 

<span data-ttu-id="6dc4d-106">En este artículo, se le guiará por los pasos necesarios para implementar una máquina virtual Windows en Azure Stack mediante la recuperación de la contraseña que está guardada en un almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="6dc4d-106">In this article, we walk you through the steps required to deploy a Windows virtual machine in Azure Stack by retrieving the password that is stored in a Key Vault.</span></span> <span data-ttu-id="6dc4d-107">Por lo tanto, la contraseña nunca se coloca en texto sin formato en el archivo de parámetros de plantilla.</span><span class="sxs-lookup"><span data-stu-id="6dc4d-107">Therefore the password is never put in plain text in the template parameter file.</span></span> <span data-ttu-id="6dc4d-108">Puede seguir los pasos descritos aquí ya sea desde Azure Stack Development Kit o desde un cliente externo, si se conecta a través de VPN.</span><span class="sxs-lookup"><span data-stu-id="6dc4d-108">You can use these steps either from the Azure Stack Development Kit, or from an external client if you are connected through VPN.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6dc4d-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6dc4d-109">Prerequisites</span></span>
 
* <span data-ttu-id="6dc4d-110">Debe suscribirse a una oferta que incluya el servicio Key Vault.</span><span class="sxs-lookup"><span data-stu-id="6dc4d-110">You must must subscribe to an offer that includes the Key Vault service.</span></span>  
* [<span data-ttu-id="6dc4d-111">Instale PowerShell para Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="6dc4d-111">Install PowerShell for Azure Stack.</span></span>](azure-stack-powershell-install.md)  
* [<span data-ttu-id="6dc4d-112">Configuración del entorno de PowerShell del usuario de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="6dc4d-112">Configure the Azure Stack user's PowerShell environment.</span></span>](azure-stack-powershell-configure-user.md)

<span data-ttu-id="6dc4d-113">Los pasos siguientes describen el proceso necesario para crear una máquina virtual mediante la recuperación de la contraseña almacenada en un almacén de claves:</span><span class="sxs-lookup"><span data-stu-id="6dc4d-113">The following steps describe the process required to create a virtual machine by retrieving the password stored in a Key Vault:</span></span>

1. <span data-ttu-id="6dc4d-114">Cree un secreto de almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="6dc4d-114">Create a Key Vault secret.</span></span>
2. <span data-ttu-id="6dc4d-115">Actualice el archivo azuredeploy.parameters.json.</span><span class="sxs-lookup"><span data-stu-id="6dc4d-115">Update the azuredeploy.parameters.json file.</span></span>
3. <span data-ttu-id="6dc4d-116">Implemente la plantilla.</span><span class="sxs-lookup"><span data-stu-id="6dc4d-116">Deploy the template.</span></span>

## <a name="create-a-key-vault-secret"></a><span data-ttu-id="6dc4d-117">Creación de un secreto de almacén de claves</span><span class="sxs-lookup"><span data-stu-id="6dc4d-117">Create a Key Vault secret</span></span>

<span data-ttu-id="6dc4d-118">El script siguiente crea un almacén de claves y almacena en él una contraseña como un secreto.</span><span class="sxs-lookup"><span data-stu-id="6dc4d-118">The following script creates a key vault, and stores a password in the key vault as a secret.</span></span> <span data-ttu-id="6dc4d-119">Use el parámetro `-EnabledForDeployment` al crear el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="6dc4d-119">Use the `-EnabledForDeployment` parameter when you're creating the key vault.</span></span> <span data-ttu-id="6dc4d-120">Este parámetro se asegura de que se puede hacer referencia al almacén de claves desde las plantillas de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6dc4d-120">This parameter makes sure that the key vault can be referenced from Azure Resource Manager templates.</span></span>

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

<span data-ttu-id="6dc4d-121">Cuando se ejecuta el script anterior, la salida incluye el identificador URI del secreto.</span><span class="sxs-lookup"><span data-stu-id="6dc4d-121">When you run the previous script, the output includes the secret URI.</span></span> <span data-ttu-id="6dc4d-122">Anote este URI.</span><span class="sxs-lookup"><span data-stu-id="6dc4d-122">Make a note of this URI.</span></span> <span data-ttu-id="6dc4d-123">Tendrá que hacer referencia a él durante la [implementación de máquina virtual Windows con contraseña en la plantilla de almacén de claves](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-vm-windows-create-passwordfromkv).</span><span class="sxs-lookup"><span data-stu-id="6dc4d-123">You have to reference it in the [Deploy Windows virtual machine with password in key vault template](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-vm-windows-create-passwordfromkv).</span></span> <span data-ttu-id="6dc4d-124">Descargue la carpeta [101-vm-secure-password](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-vm-windows-create-passwordfromkv) en el equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="6dc4d-124">Download the [101-vm-secure-password](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-vm-windows-create-passwordfromkv) folder onto your development computer.</span></span> <span data-ttu-id="6dc4d-125">Esta carpeta contiene los archivos `azuredeploy.json` y `azuredeploy.parameters.json` que necesitará en los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="6dc4d-125">This folder contains the `azuredeploy.json` and `azuredeploy.parameters.json` files, which you will need in the next steps.</span></span>

<span data-ttu-id="6dc4d-126">Modificar el archivo `azuredeploy.parameters.json` según los valores del entorno.</span><span class="sxs-lookup"><span data-stu-id="6dc4d-126">Modify the `azuredeploy.parameters.json` file according to your environment values.</span></span> <span data-ttu-id="6dc4d-127">Los parámetros de especial interés son el nombre del almacén, el grupo de recursos del almacén y el identificador URI del secreto (que se generó en el script anterior).</span><span class="sxs-lookup"><span data-stu-id="6dc4d-127">The parameters of special interest are the vault name, the vault resource group, and the secret URI (as generated by the previous script).</span></span> <span data-ttu-id="6dc4d-128">El archivo siguiente es un ejemplo de un archivo de parámetros:</span><span class="sxs-lookup"><span data-stu-id="6dc4d-128">The following file is an example of a parameter file:</span></span>

## <a name="update-the-azuredeployparametersjson-file"></a><span data-ttu-id="6dc4d-129">Actualice el archivo azuredeploy.parameters.json</span><span class="sxs-lookup"><span data-stu-id="6dc4d-129">Update the azuredeploy.parameters.json file</span></span>

<span data-ttu-id="6dc4d-130">Actualice el archivo azuredeploy.parameters.json con los valores de KeyVault URI, secretName y adminUsername de la máquina virtual correspondientes a su entorno.</span><span class="sxs-lookup"><span data-stu-id="6dc4d-130">Update the azuredeploy.parameters.json file with the KeyVault URI, secretName, adminUsername of the virtual machine values as per your environment.</span></span> <span data-ttu-id="6dc4d-131">El siguiente archivo JSON muestra un ejemplo del archivo de parámetros de plantilla:</span><span class="sxs-lookup"><span data-stu-id="6dc4d-131">The following JSON file shows an example of the template parameters file:</span></span> 

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

## <a name="template-deployment"></a><span data-ttu-id="6dc4d-132">Implementación de plantilla</span><span class="sxs-lookup"><span data-stu-id="6dc4d-132">Template deployment</span></span>

<span data-ttu-id="6dc4d-133">Ahora implemente la plantilla con el siguiente script de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6dc4d-133">Now deploy the template by using the following PowerShell script:</span></span>

```powershell
New-AzureRmResourceGroupDeployment `
  -Name KVPwdDeployment `
  -ResourceGroupName $resourceGroup `
  -TemplateFile "<Fully qualified path to the azuredeploy.json file>" `
  -TemplateParameterFile "<Fully qualified path to the azuredeploy.parameters.json file>"
```
<span data-ttu-id="6dc4d-134">Cuando la plantilla se ha implementado correctamente, se producen en la siguiente salida:</span><span class="sxs-lookup"><span data-stu-id="6dc4d-134">When the template is deployed successfully, it results in the following output:</span></span>

![Salida de la implementación](media/azure-stack-kv-deploy-vm-with-secret/deployment-output.png)


## <a name="next-steps"></a><span data-ttu-id="6dc4d-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6dc4d-136">Next steps</span></span>
[<span data-ttu-id="6dc4d-137">Implementación de una aplicación de ejemplo con Key Vault</span><span class="sxs-lookup"><span data-stu-id="6dc4d-137">Deploy a sample app with Key Vault</span></span>](azure-stack-kv-sample-app.md)

[<span data-ttu-id="6dc4d-138">Implementación de una máquina virtual con un certificado de Key Vault</span><span class="sxs-lookup"><span data-stu-id="6dc4d-138">Deploy a VM with a Key Vault certificate</span></span>](azure-stack-kv-push-secret-into-vm.md)

