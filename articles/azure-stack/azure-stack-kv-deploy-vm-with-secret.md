---
title: "aaaDeploy una máquina virtual con contraseñas almacenadas de manera segura en la pila de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toodeploy una máquina virtual mediante una contraseña almacenada en el almacén de claves de pila de Azure"
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
ms.openlocfilehash: 368addc1dfc5b7adadd2151fbd6d354f7892eea5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-by-retrieving-hello-password-stored-in-a-key-vault"></a><span data-ttu-id="64fa9-103">Crear una máquina virtual mediante la recuperación de contraseña de hello almacenada en un almacén de claves</span><span class="sxs-lookup"><span data-stu-id="64fa9-103">Create a virtual machine by retrieving hello password stored in a Key Vault</span></span>

<span data-ttu-id="64fa9-104">Cuando necesite toopass un valor como una contraseña seguro durante la implementación, puede almacenar ese valor como un secreto en un almacén de claves de la pila de Azure y hacer referencia a él en las plantillas de Azure Resource Manager Hola.</span><span class="sxs-lookup"><span data-stu-id="64fa9-104">When you need toopass a secure value such as a password during deployment, you can store that value as a secret in an Azure Stack key vault and reference it in hello Azure Resource Manager templates.</span></span> <span data-ttu-id="64fa9-105">No es necesario toomanually escriba secreto Hola cada vez que implemente recursos hello, también puede especificar qué usuarios o entidades de servicio pueden tener acceso a secreto Hola.</span><span class="sxs-lookup"><span data-stu-id="64fa9-105">You do not need toomanually enter hello secret each time you deploy hello resources, you can also specify which users or service principals can access hello secret.</span></span> 

<span data-ttu-id="64fa9-106">En este artículo, le guiaremos por hello pasos necesarios toodeploy una máquina virtual de Windows en la pila de Azure mediante la recuperación de contraseña de Hola que se almacena en un almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="64fa9-106">In this article, we walk you through hello steps required toodeploy a Windows virtual machine in Azure Stack by retrieving hello password that is stored in a Key Vault.</span></span> <span data-ttu-id="64fa9-107">Por lo tanto, contraseña de hello nunca se coloca en texto sin formato en el archivo de parámetros de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="64fa9-107">Therefore hello password is never put in plain text in hello template parameter file.</span></span> <span data-ttu-id="64fa9-108">Puede usar estos pasos desde Hola Kit de desarrollo de pila de Azure, o desde un cliente externo si está conectado a través de VPN.</span><span class="sxs-lookup"><span data-stu-id="64fa9-108">You can use these steps either from hello Azure Stack Development Kit, or from an external client if you are connected through VPN.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64fa9-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="64fa9-109">Prerequisites</span></span>

* <span data-ttu-id="64fa9-110">Deben tener los administradores de la nube de Azure pila [crea una oferta](azure-stack-create-offer.md) que incluye el servicio de almacén de claves de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="64fa9-110">Azure Stack cloud administrators must have [created an offer](azure-stack-create-offer.md) that includes hello Azure Key Vault service.</span></span>  
* <span data-ttu-id="64fa9-111">Los usuarios deben [suscribirse tooan oferta](azure-stack-subscribe-plan-provision-vm.md) que incluye el servicio de almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="64fa9-111">Users must [subscribe tooan offer](azure-stack-subscribe-plan-provision-vm.md) that includes hello Key Vault service.</span></span>  
* [<span data-ttu-id="64fa9-112">Instale PowerShell para Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="64fa9-112">Install PowerShell for Azure Stack.</span></span>](azure-stack-powershell-install.md)  
* [<span data-ttu-id="64fa9-113">Configurar el entorno de PowerShell del usuario de hello Azure pila.</span><span class="sxs-lookup"><span data-stu-id="64fa9-113">Configure hello Azure Stack user's PowerShell environment.</span></span>](azure-stack-powershell-configure-user.md)

<span data-ttu-id="64fa9-114">Hello siguientes pasos describen Hola proceso necesario toocreate una máquina virtual mediante la recuperación de contraseña de hello almacenada en un almacén de claves:</span><span class="sxs-lookup"><span data-stu-id="64fa9-114">hello following steps describe hello process required toocreate a virtual machine by retrieving hello password stored in a Key Vault:</span></span>

1. <span data-ttu-id="64fa9-115">Cree un secreto de almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="64fa9-115">Create a Key Vault secret.</span></span>
2. <span data-ttu-id="64fa9-116">Actualizar archivo de hello azuredeploy.parameters.json.</span><span class="sxs-lookup"><span data-stu-id="64fa9-116">Update hello azuredeploy.parameters.json file.</span></span>
3. <span data-ttu-id="64fa9-117">Implementar la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="64fa9-117">Deploy hello template.</span></span>

## <a name="create-a-key-vault-secret"></a><span data-ttu-id="64fa9-118">Creación de un secreto de almacén de claves</span><span class="sxs-lookup"><span data-stu-id="64fa9-118">Create a Key Vault secret</span></span>

<span data-ttu-id="64fa9-119">Hello secuencia de comandos siguiente crea un almacén de claves y almacena una contraseña en el almacén de claves de Hola como un secreto.</span><span class="sxs-lookup"><span data-stu-id="64fa9-119">hello following script creates a key vault, and stores a password in hello key vault as a secret.</span></span> <span data-ttu-id="64fa9-120">Hola de uso `-EnabledForDeployment` parámetro al crear el almacén de claves Hola.</span><span class="sxs-lookup"><span data-stu-id="64fa9-120">Use hello `-EnabledForDeployment` parameter when you're creating hello key vault.</span></span> <span data-ttu-id="64fa9-121">Este parámetro se asegura de ese almacén de claves de hello puede hacer referencia a partir de plantillas de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="64fa9-121">This parameter makes sure that hello key vault can be referenced from Azure Resource Manager templates.</span></span>

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

<span data-ttu-id="64fa9-122">Cuando se ejecuta el script anterior hello, salida de hello incluye secreto Hola URI.</span><span class="sxs-lookup"><span data-stu-id="64fa9-122">When you run hello previous script, hello output includes hello secret URI.</span></span> <span data-ttu-id="64fa9-123">Anote este URI.</span><span class="sxs-lookup"><span data-stu-id="64fa9-123">Make a note of this URI.</span></span> <span data-ttu-id="64fa9-124">Tendrá que tooreference en hello [máquina virtual de implementar Windows con contraseña en la plantilla de almacén de claves](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-secure-password).</span><span class="sxs-lookup"><span data-stu-id="64fa9-124">You have tooreference it in hello [Deploy Windows virtual machine with password in key vault template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-secure-password).</span></span> <span data-ttu-id="64fa9-125">Descargar hello [101-vm-proteger-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-secure-password) carpeta en el equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="64fa9-125">Download hello [101-vm-secure-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-secure-password) folder onto your development computer.</span></span> <span data-ttu-id="64fa9-126">Esta carpeta contiene Hola `azuredeploy.json` y `azuredeploy.parameters.json` archivos, lo que necesitará en pasos de Hola.</span><span class="sxs-lookup"><span data-stu-id="64fa9-126">This folder contains hello `azuredeploy.json` and `azuredeploy.parameters.json` files, which you will need in hello next steps.</span></span>

<span data-ttu-id="64fa9-127">Modificar hello `azuredeploy.parameters.json` archivo según tooyour valores de entorno.</span><span class="sxs-lookup"><span data-stu-id="64fa9-127">Modify hello `azuredeploy.parameters.json` file according tooyour environment values.</span></span> <span data-ttu-id="64fa9-128">parámetros de Hola de especial interés son el nombre del almacén de hello, grupo de recursos de almacén de Hola y Hola secreto URI (como las generadas por script anterior Hola).</span><span class="sxs-lookup"><span data-stu-id="64fa9-128">hello parameters of special interest are hello vault name, hello vault resource group, and hello secret URI (as generated by hello previous script).</span></span> <span data-ttu-id="64fa9-129">Hola el archivo siguiente es un ejemplo de un archivo de parámetros:</span><span class="sxs-lookup"><span data-stu-id="64fa9-129">hello following file is an example of a parameter file:</span></span>

## <a name="update-hello-azuredeployparametersjson-file"></a><span data-ttu-id="64fa9-130">Archivo de actualización hello azuredeploy.parameters.json</span><span class="sxs-lookup"><span data-stu-id="64fa9-130">Update hello azuredeploy.parameters.json file</span></span>

<span data-ttu-id="64fa9-131">Actualizar archivo de hello azuredeploy.parameters.json con hello KeyVault URI, secretName, adminUsername de valores de la máquina virtual de hello según su entorno.</span><span class="sxs-lookup"><span data-stu-id="64fa9-131">Update hello azuredeploy.parameters.json file with hello KeyVault URI, secretName, adminUsername of hello virtual machine values as per your environment.</span></span> <span data-ttu-id="64fa9-132">Hello archivo JSON siguiente muestra un ejemplo de archivo de parámetros de plantilla de hello:</span><span class="sxs-lookup"><span data-stu-id="64fa9-132">hello following JSON file shows an example of hello template parameters file:</span></span> 

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

## <a name="template-deployment"></a><span data-ttu-id="64fa9-133">Implementación de plantilla</span><span class="sxs-lookup"><span data-stu-id="64fa9-133">Template deployment</span></span>

<span data-ttu-id="64fa9-134">Ahora puede implementar plantilla hello mediante Hola siguiente script de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="64fa9-134">Now deploy hello template by using hello following PowerShell script:</span></span>

```powershell
New-AzureRmResourceGroupDeployment `
  -Name KVPwdDeployment `
  -ResourceGroupName $resourceGroup `
  -TemplateFile "<Fully qualified path toohello azuredeploy.json file>" `
  -TemplateParameterFile "<Fully qualified path toohello azuredeploy.parameters.json file>"
```
<span data-ttu-id="64fa9-135">Cuando se implementa correctamente la plantilla de hello, resulta en hello después de salida:</span><span class="sxs-lookup"><span data-stu-id="64fa9-135">When hello template is deployed successfully, it results in hello following output:</span></span>

![Salida de la implementación](media\azure-stack-kv-deploy-vm-with-secret/deployment-output.png)


## <a name="next-steps"></a><span data-ttu-id="64fa9-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="64fa9-137">Next steps</span></span>
[<span data-ttu-id="64fa9-138">Implementación de una aplicación de ejemplo con Key Vault</span><span class="sxs-lookup"><span data-stu-id="64fa9-138">Deploy a sample app with Key Vault</span></span>](azure-stack-kv-sample-app.md)

[<span data-ttu-id="64fa9-139">Implementación de una máquina virtual con un certificado de Key Vault</span><span class="sxs-lookup"><span data-stu-id="64fa9-139">Deploy a VM with a Key Vault certificate</span></span>](azure-stack-kv-push-secret-into-vm.md)

