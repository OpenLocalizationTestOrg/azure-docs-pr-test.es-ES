---
title: "Implementación de una máquina virtual con un certificado almacenado de forma segura en Azure Stack | Microsoft Docs"
description: "Aprenda a implementar una máquina virtual e inserte en ella un certificado utilizando un almacén de claves en Azure Stack"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 46590eb1-1746-4ecf-a9e5-41609fde8e89
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/03/2017
ms.author: sngun
ms.openlocfilehash: 95008e783b2597895e870ceb3514bffbd4ab1dbf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-virtual-machine-and-include-certificate-retrieved-from-a-key-vault"></a><span data-ttu-id="47dff-103">Creación de una máquina virtual e inclusión de un certificado recuperado de un almacén de claves</span><span class="sxs-lookup"><span data-stu-id="47dff-103">Create a virtual machine and include certificate retrieved from a key vault</span></span>

<span data-ttu-id="47dff-104">En este artículo le ayuda a crear una máquina virtual en Azure Stack y a insertar certificados en ella.</span><span class="sxs-lookup"><span data-stu-id="47dff-104">This article helps you to create a virtual machine in Azure Stack and push certificates onto it.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="47dff-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="47dff-105">Prerequisites</span></span>

* <span data-ttu-id="47dff-106">Los administradores de nube de Azure Stack tienen que haber [creado una oferta](azure-stack-create-offer.md) que incluya el servicio Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="47dff-106">Azure Stack cloud administrators must have [created an offer](azure-stack-create-offer.md) that includes the Azure Key Vault service.</span></span>  
* <span data-ttu-id="47dff-107">Los usuarios tienen que [suscribirse a una oferta](azure-stack-subscribe-plan-provision-vm.md) que incluya el servicio Key Vault.</span><span class="sxs-lookup"><span data-stu-id="47dff-107">Users must [subscribe to an offer](azure-stack-subscribe-plan-provision-vm.md) that includes the Key Vault service.</span></span>  
* [<span data-ttu-id="47dff-108">Instalación de PowerShell para Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="47dff-108">Install PowerShell for Azure Stack.</span></span>](azure-stack-powershell-install.md)  
* [<span data-ttu-id="47dff-109">Configuración del entorno de PowerShell del usuario de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="47dff-109">Configure the Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)

<span data-ttu-id="47dff-110">Un almacén de claves en Azure Stack se utiliza para almacenar certificados.</span><span class="sxs-lookup"><span data-stu-id="47dff-110">A key vault in Azure Stack is used to store certificates.</span></span> <span data-ttu-id="47dff-111">Los certificados son útiles en varios escenarios diferentes.</span><span class="sxs-lookup"><span data-stu-id="47dff-111">Certificates are helpful in many different scenarios.</span></span> <span data-ttu-id="47dff-112">Por ejemplo, considere un escenario en el que haya una máquina virtual en Azure Stack que está ejecutando una aplicación que necesita un certificado.</span><span class="sxs-lookup"><span data-stu-id="47dff-112">For example, consider a scenario where you have a virtual machine in Azure Stack that is running an application that needs a certificate.</span></span> <span data-ttu-id="47dff-113">Este certificado se puede utilizar para cifrar, para la autenticación en Active Directory, o para SSL en un sitio web.</span><span class="sxs-lookup"><span data-stu-id="47dff-113">This certificate can be used for encrypting, for authenticating to Active Directory, or for SSL on a website.</span></span> <span data-ttu-id="47dff-114">Tener el certificado guardado en un almacén de claves, le ayuda a cerciorarse de que está seguro.</span><span class="sxs-lookup"><span data-stu-id="47dff-114">Having the certificate in a key vault helps make sure that it's secure.</span></span>

<span data-ttu-id="47dff-115">En este artículo, se le guiará por los pasos necesarios para insertar un certificado en una máquina virtual Windows en Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="47dff-115">In this article, we walk you through the steps required to push a certificate onto a Windows virtual machine in Azure Stack.</span></span> <span data-ttu-id="47dff-116">Puede seguir los pasos descritos aquí ya sea desde el kit de desarrollo de Azure Stack o desde un cliente externo basado en Windows, si se conecta a través de VPN.</span><span class="sxs-lookup"><span data-stu-id="47dff-116">You can use these steps either from the Azure Stack Development Kit, or from a Windows-based external client if you are connected through VPN.</span></span>

<span data-ttu-id="47dff-117">Los pasos siguientes describen el proceso necesario para insertar un certificado en la máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="47dff-117">The following steps describe the process required to push a certificate onto the virtual machine:</span></span>

1. <span data-ttu-id="47dff-118">Cree un secreto de almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="47dff-118">Create a Key Vault secret.</span></span>
2. <span data-ttu-id="47dff-119">Actualice el archivo azuredeploy.parameters.json.</span><span class="sxs-lookup"><span data-stu-id="47dff-119">Update the azuredeploy.parameters.json file.</span></span>
3. <span data-ttu-id="47dff-120">Implementación de la plantilla</span><span class="sxs-lookup"><span data-stu-id="47dff-120">Deploy the template</span></span>

## <a name="create-a-key-vault-secret"></a><span data-ttu-id="47dff-121">Creación de un secreto de almacén de claves</span><span class="sxs-lookup"><span data-stu-id="47dff-121">Create a Key Vault secret</span></span>

<span data-ttu-id="47dff-122">El script siguiente crea un certificado con el formato .pfx, crea un almacén de claves y almacena el certificado en el almacén de claves como un secreto.</span><span class="sxs-lookup"><span data-stu-id="47dff-122">The following script creates a certificate in the .pfx format, creates a key vault, and stores the certificate in the key vault as a secret.</span></span> <span data-ttu-id="47dff-123">Use el parámetro `-EnabledForDeployment` al crear el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="47dff-123">You must use the `-EnabledForDeployment` parameter when you're creating the key vault.</span></span> <span data-ttu-id="47dff-124">Este parámetro se asegura de que se puede hacer referencia al almacén de claves desde las plantillas de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="47dff-124">This parameter makes sure that the key vault can be referenced from Azure Resource Manager templates.</span></span>

```powershell

# Create a certificate in the .pfx format
New-SelfSignedCertificate `
  -certstorelocation cert:\LocalMachine\My `
  -dnsname contoso.microsoft.com

$pwd = ConvertTo-SecureString `
  -String "<Password used to export the certificate>" `
  -Force `
  -AsPlainText

Export-PfxCertificate `
  -cert "cert:\localMachine\my\<Certificate Thumbprint that was created in the previous step>" `
  -FilePath "<Fully qualified path where the exported certificate can be stored>" `
  -Password $pwd

# Create a key vault and upload the certificate into the key vault as a secret
$vaultName = "contosovault"
$resourceGroup = "contosovaultrg"
$location = "local"
$secretName = "servicecert"
$fileName = "<Fully qualified path where the exported certificate can be stored>"
$certPassword = "<Password used to export the certificate>"

$fileContentBytes = get-content $fileName `
  -Encoding Byte

$fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
$jsonObject = @"
{
"data": "$filecontentencoded",
"dataType" :"pfx",
"password": "$certPassword"
}
"@
$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

New-AzureRmResourceGroup `
  -Name $resourceGroup `
  -Location $location

New-AzureRmKeyVault `
  -VaultName $vaultName `
  -ResourceGroupName $resourceGroup `
  -Location $location `
  -sku standard `
  -EnabledForDeployment

$secret = ConvertTo-SecureString `
  -String $jsonEncoded `
  -AsPlainText -Force

Set-AzureKeyVaultSecret `
  -VaultName $vaultName `
  -Name $secretName `
   -SecretValue $secret

```

<span data-ttu-id="47dff-125">Cuando se ejecuta el script anterior, la salida incluye el identificador URI del secreto.</span><span class="sxs-lookup"><span data-stu-id="47dff-125">When you run the previous script, the output includes the secret URI.</span></span> <span data-ttu-id="47dff-126">Anote este URI.</span><span class="sxs-lookup"><span data-stu-id="47dff-126">Make a note of this URI.</span></span> <span data-ttu-id="47dff-127">Tendrá que hacer referencia a él en la [inserción de certificado en la plantilla de Resource Manager de Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows).</span><span class="sxs-lookup"><span data-stu-id="47dff-127">You have to reference it in the [Push certificate to Windows Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows).</span></span> <span data-ttu-id="47dff-128">Descargue la carpeta de la [plantilla vm-push-certificate-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows) en el equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="47dff-128">Download the [vm-push-certificate-windows template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows) folder onto your development computer.</span></span> <span data-ttu-id="47dff-129">Esta carpeta contiene los archivos `azuredeploy.json` y `azuredeploy.parameters.json` que necesitará en los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="47dff-129">This folder contains the `azuredeploy.json` and `azuredeploy.parameters.json` files, which you will need in the next steps.</span></span>

<span data-ttu-id="47dff-130">Modificar el archivo `azuredeploy.parameters.json` según los valores del entorno.</span><span class="sxs-lookup"><span data-stu-id="47dff-130">Modify the `azuredeploy.parameters.json` file according to your environment values.</span></span> <span data-ttu-id="47dff-131">Los parámetros de especial interés son el nombre del almacén, el grupo de recursos del almacén y el identificador URI del secreto (que se generó en el script anterior).</span><span class="sxs-lookup"><span data-stu-id="47dff-131">The parameters of special interest are the vault name, the vault resource group, and the secret URI (as generated by the previous script).</span></span> <span data-ttu-id="47dff-132">El archivo siguiente es un ejemplo de un archivo de parámetros:</span><span class="sxs-lookup"><span data-stu-id="47dff-132">The following file is an example of a parameter file:</span></span>

## <a name="update-the-azuredeployparametersjson-file"></a><span data-ttu-id="47dff-133">Actualice el archivo azuredeploy.parameters.json</span><span class="sxs-lookup"><span data-stu-id="47dff-133">Update the azuredeploy.parameters.json file</span></span>

<span data-ttu-id="47dff-134">Actualice el archivo azuredeploy.parameters.json con los valores de vaultName (nombre del almacén), URI del secreto, VmName (nombre de la máquina virtual) y otros valores según el entorno.</span><span class="sxs-lookup"><span data-stu-id="47dff-134">Update the azuredeploy.parameters.json file with the vaultName, secret URI, VmName, and other values as per your environment.</span></span> <span data-ttu-id="47dff-135">El siguiente archivo JSON muestra un ejemplo del archivo de parámetros de plantilla:</span><span class="sxs-lookup"><span data-stu-id="47dff-135">The following JSON file shows an example of the template parameters file:</span></span> 

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "newStorageAccountName": {
      "value": "kvstorage01"
    },
    "vmName": {
      "value": "VM1"
    },
    "vmSize": {
      "value": "Standard_D1_v2"
    },
    "adminUserName": {
      "value": "demouser"
    },
    "adminPassword": {
      "value": "demouser@123"
    },
    "vaultName": {
      "value": "contosovault"
    },
    "vaultResourceGroup": {
      "value": "contosovaultrg"
    },
    "secretUrlWithVersion": {
      "value": "https://testkv001.vault.local.azurestack.external/secrets/testcert002/82afeeb84f4442329ce06593502e7840"
    }
  }
}
```

## <a name="deploy-the-template"></a><span data-ttu-id="47dff-136">Implementación de la plantilla</span><span class="sxs-lookup"><span data-stu-id="47dff-136">Deploy the template</span></span>

<span data-ttu-id="47dff-137">Ahora implemente la plantilla con el siguiente script de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="47dff-137">Now deploy the template by using the following PowerShell script:</span></span>

```powershell
# Deploy a Resource Manager template to create a VM and push the secret onto it
New-AzureRmResourceGroupDeployment `
  -Name KVDeployment `
  -ResourceGroupName $resourceGroup `
  -TemplateFile "<Fully qualified path to the azuredeploy.json file>" `
  -TemplateParameterFile "<Fully qualified path to the azuredeploy.parameters.json file>"
```

<span data-ttu-id="47dff-138">Cuando la plantilla se ha implementado correctamente, se producen en la siguiente salida:</span><span class="sxs-lookup"><span data-stu-id="47dff-138">When the template is deployed successfully, it results in the following output:</span></span>

![Salida de la implementación](media\azure-stack-kv-push-secret-into-vm/deployment-output.png)

<span data-ttu-id="47dff-140">Cuando se implementa esta máquina virtual, Azure Stack inserta el certificado en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47dff-140">When this virtual machine is deployed, Azure Stack pushes the certificate onto the virtual machine.</span></span> <span data-ttu-id="47dff-141">En Windows, el certificado se agrega a la ubicación de certificados LocalMachine, con el almacén de certificados que el usuario proporcionó.</span><span class="sxs-lookup"><span data-stu-id="47dff-141">In Windows, the certificate is added to the LocalMachine certificate location, with the certificate store that the user provided.</span></span> <span data-ttu-id="47dff-142">En Linux, el certificado se coloca en el directorio /var/lib/waagent, con el nombre de archivo &lt;UppercaseThumbprint&gt;.crt para el archivo de certificado X509 y &lt;UppercaseThumbprint&gt;.prv para la clave privada.</span><span class="sxs-lookup"><span data-stu-id="47dff-142">In Linux, the certificate is placed under the /var/lib/waagent directory, with the file name &lt;UppercaseThumbprint&gt;.crt for the X509 certificate file and &lt;UppercaseThumbprint&gt;.prv for the private key.</span></span>

## <a name="retire-certificates"></a><span data-ttu-id="47dff-143">Retirada de certificados</span><span class="sxs-lookup"><span data-stu-id="47dff-143">Retire certificates</span></span>

<span data-ttu-id="47dff-144">En la sección anterior, se muestra cómo insertar un nuevo certificado en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47dff-144">In the preceding section, we showed you how to push a new certificate onto a virtual machine.</span></span> <span data-ttu-id="47dff-145">El certificado antiguo todavía está en la máquina virtual y no se puede quitar.</span><span class="sxs-lookup"><span data-stu-id="47dff-145">Your old certificate is still on the virtual machine, and it can't be removed.</span></span> <span data-ttu-id="47dff-146">Sin embargo, puede deshabilitar la versión anterior del secreto mediante el cmdlet `Set-AzureKeyVaultSecretAttribute`.</span><span class="sxs-lookup"><span data-stu-id="47dff-146">However, you can disable the older version of the secret by using the `Set-AzureKeyVaultSecretAttribute` cmdlet.</span></span> <span data-ttu-id="47dff-147">A continuación, verá un ejemplo de cómo usar este cmdlet.</span><span class="sxs-lookup"><span data-stu-id="47dff-147">The following is an example usage of this cmdlet.</span></span> <span data-ttu-id="47dff-148">Asegúrese de reemplazar el nombre del almacén, nombre de secreto y valores de versión de acuerdo con su entorno:</span><span class="sxs-lookup"><span data-stu-id="47dff-148">Make sure to replace the vault name, secret name, and version values according to your environment:</span></span>

```powershell
Set-AzureKeyVaultSecretAttribute -VaultName contosovault -Name servicecert -Version e3391a126b65414f93f6f9806743a1f7 -Enable 0
```

## <a name="next-steps"></a><span data-ttu-id="47dff-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="47dff-149">Next steps</span></span>

* [<span data-ttu-id="47dff-150">Implementación de una máquina virtual con una contraseña de Key Vault</span><span class="sxs-lookup"><span data-stu-id="47dff-150">Deploy a VM with a Key Vault password</span></span>](azure-stack-kv-deploy-vm-with-secret.md)
* [<span data-ttu-id="47dff-151">Permitir el acceso de una aplicación a Key Vault</span><span class="sxs-lookup"><span data-stu-id="47dff-151">Allow an application to access Key Vault</span></span>](azure-stack-kv-sample-app.md)


