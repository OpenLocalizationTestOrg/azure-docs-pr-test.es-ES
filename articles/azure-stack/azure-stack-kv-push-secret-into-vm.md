---
title: "aaaDeploy una máquina virtual con un certificado almacenado de forma segura en la pila de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toodeploy una máquina virtual e inserte un certificado en él mediante una clave del almacén en la pila de Azure"
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
ms.openlocfilehash: b5fa0a502ba582e10ff59b8af0568bf134d3d189
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-and-include-certificate-retrieved-from-a-key-vault"></a><span data-ttu-id="66657-103">Creación de una máquina virtual e inclusión de un certificado recuperado de un almacén de claves</span><span class="sxs-lookup"><span data-stu-id="66657-103">Create a virtual machine and include certificate retrieved from a key vault</span></span>

<span data-ttu-id="66657-104">Este artículo le ayude toocreate una máquina virtual en la pila de Azure y certificados de inserción en él.</span><span class="sxs-lookup"><span data-stu-id="66657-104">This article helps you toocreate a virtual machine in Azure Stack and push certificates onto it.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="66657-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="66657-105">Prerequisites</span></span>

* <span data-ttu-id="66657-106">Deben tener los administradores de la nube de Azure pila [crea una oferta](azure-stack-create-offer.md) que incluye el servicio de almacén de claves de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="66657-106">Azure Stack cloud administrators must have [created an offer](azure-stack-create-offer.md) that includes hello Azure Key Vault service.</span></span>  
* <span data-ttu-id="66657-107">Los usuarios deben [suscribirse tooan oferta](azure-stack-subscribe-plan-provision-vm.md) que incluye el servicio de almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="66657-107">Users must [subscribe tooan offer](azure-stack-subscribe-plan-provision-vm.md) that includes hello Key Vault service.</span></span>  
* [<span data-ttu-id="66657-108">Instale PowerShell para Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="66657-108">Install PowerShell for Azure Stack.</span></span>](azure-stack-powershell-install.md)  
* [<span data-ttu-id="66657-109">Configurar el entorno de PowerShell del usuario de hello pila de Azure</span><span class="sxs-lookup"><span data-stu-id="66657-109">Configure hello Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)

<span data-ttu-id="66657-110">Un almacén de claves en la pila de Azure es toostore usa certificados.</span><span class="sxs-lookup"><span data-stu-id="66657-110">A key vault in Azure Stack is used toostore certificates.</span></span> <span data-ttu-id="66657-111">Los certificados son útiles en varios escenarios diferentes.</span><span class="sxs-lookup"><span data-stu-id="66657-111">Certificates are helpful in many different scenarios.</span></span> <span data-ttu-id="66657-112">Por ejemplo, considere un escenario en el que haya una máquina virtual en Azure Stack que está ejecutando una aplicación que necesita un certificado.</span><span class="sxs-lookup"><span data-stu-id="66657-112">For example, consider a scenario where you have a virtual machine in Azure Stack that is running an application that needs a certificate.</span></span> <span data-ttu-id="66657-113">Este certificado se puede utilizar para cifrar, para autenticar tooActive Directory o SSL en un sitio Web.</span><span class="sxs-lookup"><span data-stu-id="66657-113">This certificate can be used for encrypting, for authenticating tooActive Directory, or for SSL on a website.</span></span> <span data-ttu-id="66657-114">Tener certificado hello en un almacén de claves, le ayuda a asegurarse de que es segura.</span><span class="sxs-lookup"><span data-stu-id="66657-114">Having hello certificate in a key vault helps make sure that it's secure.</span></span>

<span data-ttu-id="66657-115">En este artículo, le guiaremos por hello pasos necesarios toopush un certificado en una máquina virtual de Windows en la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="66657-115">In this article, we walk you through hello steps required toopush a certificate onto a Windows virtual machine in Azure Stack.</span></span> <span data-ttu-id="66657-116">Puede usar estos pasos desde Hola Kit de desarrollo de pila de Azure, o desde un cliente externo basado en Windows, si está conectado a través de VPN.</span><span class="sxs-lookup"><span data-stu-id="66657-116">You can use these steps either from hello Azure Stack Development Kit, or from a Windows-based external client if you are connected through VPN.</span></span>

<span data-ttu-id="66657-117">Hola pasos describe hello toopush de proceso requerido un certificado en la máquina virtual de hello:</span><span class="sxs-lookup"><span data-stu-id="66657-117">hello following steps describe hello process required toopush a certificate onto hello virtual machine:</span></span>

1. <span data-ttu-id="66657-118">Cree un secreto de almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="66657-118">Create a Key Vault secret.</span></span>
2. <span data-ttu-id="66657-119">Actualizar archivo de hello azuredeploy.parameters.json.</span><span class="sxs-lookup"><span data-stu-id="66657-119">Update hello azuredeploy.parameters.json file.</span></span>
3. <span data-ttu-id="66657-120">Implementar la plantilla de Hola</span><span class="sxs-lookup"><span data-stu-id="66657-120">Deploy hello template</span></span>

## <a name="create-a-key-vault-secret"></a><span data-ttu-id="66657-121">Creación de un secreto de almacén de claves</span><span class="sxs-lookup"><span data-stu-id="66657-121">Create a Key Vault secret</span></span>

<span data-ttu-id="66657-122">Hello script siguiente crea un certificado en formato .pfx de hello, crea un almacén de claves y almacena el certificado de hello en el almacén de claves de Hola como un secreto.</span><span class="sxs-lookup"><span data-stu-id="66657-122">hello following script creates a certificate in hello .pfx format, creates a key vault, and stores hello certificate in hello key vault as a secret.</span></span> <span data-ttu-id="66657-123">Debe usar hello `-EnabledForDeployment` parámetro al crear el almacén de claves Hola.</span><span class="sxs-lookup"><span data-stu-id="66657-123">You must use hello `-EnabledForDeployment` parameter when you're creating hello key vault.</span></span> <span data-ttu-id="66657-124">Este parámetro se asegura de ese almacén de claves de hello puede hacer referencia a partir de plantillas de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="66657-124">This parameter makes sure that hello key vault can be referenced from Azure Resource Manager templates.</span></span>

```powershell

# Create a certificate in hello .pfx format
New-SelfSignedCertificate `
  -certstorelocation cert:\LocalMachine\My `
  -dnsname contoso.microsoft.com

$pwd = ConvertTo-SecureString `
  -String "<Password used tooexport hello certificate>" `
  -Force `
  -AsPlainText

Export-PfxCertificate `
  -cert "cert:\localMachine\my\<Certificate Thumbprint that was created in hello previous step>" `
  -FilePath "<Fully qualified path where hello exported certificate can be stored>" `
  -Password $pwd

# Create a key vault and upload hello certificate into hello key vault as a secret
$vaultName = "contosovault"
$resourceGroup = "contosovaultrg"
$location = "local"
$secretName = "servicecert"
$fileName = "<Fully qualified path where hello exported certificate can be stored>"
$certPassword = "<Password used tooexport hello certificate>"

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

<span data-ttu-id="66657-125">Cuando se ejecuta el script anterior hello, salida de hello incluye secreto Hola URI.</span><span class="sxs-lookup"><span data-stu-id="66657-125">When you run hello previous script, hello output includes hello secret URI.</span></span> <span data-ttu-id="66657-126">Anote este URI.</span><span class="sxs-lookup"><span data-stu-id="66657-126">Make a note of this URI.</span></span> <span data-ttu-id="66657-127">Tendrá que tooreference en hello [insertar certificado tooWindows plantilla del Administrador de recursos](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows).</span><span class="sxs-lookup"><span data-stu-id="66657-127">You have tooreference it in hello [Push certificate tooWindows Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows).</span></span> <span data-ttu-id="66657-128">Descargar hello [plantilla de vm inserción certificado windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows) carpeta en el equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="66657-128">Download hello [vm-push-certificate-windows template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows) folder onto your development computer.</span></span> <span data-ttu-id="66657-129">Esta carpeta contiene Hola `azuredeploy.json` y `azuredeploy.parameters.json` archivos, lo que necesitará en pasos de Hola.</span><span class="sxs-lookup"><span data-stu-id="66657-129">This folder contains hello `azuredeploy.json` and `azuredeploy.parameters.json` files, which you will need in hello next steps.</span></span>

<span data-ttu-id="66657-130">Modificar hello `azuredeploy.parameters.json` archivo según tooyour valores de entorno.</span><span class="sxs-lookup"><span data-stu-id="66657-130">Modify hello `azuredeploy.parameters.json` file according tooyour environment values.</span></span> <span data-ttu-id="66657-131">parámetros de Hola de especial interés son el nombre del almacén de hello, grupo de recursos de almacén de Hola y Hola secreto URI (como las generadas por script anterior Hola).</span><span class="sxs-lookup"><span data-stu-id="66657-131">hello parameters of special interest are hello vault name, hello vault resource group, and hello secret URI (as generated by hello previous script).</span></span> <span data-ttu-id="66657-132">Hola el archivo siguiente es un ejemplo de un archivo de parámetros:</span><span class="sxs-lookup"><span data-stu-id="66657-132">hello following file is an example of a parameter file:</span></span>

## <a name="update-hello-azuredeployparametersjson-file"></a><span data-ttu-id="66657-133">Archivo de actualización hello azuredeploy.parameters.json</span><span class="sxs-lookup"><span data-stu-id="66657-133">Update hello azuredeploy.parameters.json file</span></span>

<span data-ttu-id="66657-134">Actualizar archivo de hello azuredeploy.parameters.json con el nombre de almacén de hello, URI secreto, VmName y otros valores según el entorno.</span><span class="sxs-lookup"><span data-stu-id="66657-134">Update hello azuredeploy.parameters.json file with hello vaultName, secret URI, VmName, and other values as per your environment.</span></span> <span data-ttu-id="66657-135">Hello archivo JSON siguiente muestra un ejemplo de archivo de parámetros de plantilla de hello:</span><span class="sxs-lookup"><span data-stu-id="66657-135">hello following JSON file shows an example of hello template parameters file:</span></span> 

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

## <a name="deploy-hello-template"></a><span data-ttu-id="66657-136">Implementar la plantilla de Hola</span><span class="sxs-lookup"><span data-stu-id="66657-136">Deploy hello template</span></span>

<span data-ttu-id="66657-137">Ahora puede implementar plantilla hello mediante Hola siguiente script de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="66657-137">Now deploy hello template by using hello following PowerShell script:</span></span>

```powershell
# Deploy a Resource Manager template toocreate a VM and push hello secret onto it
New-AzureRmResourceGroupDeployment `
  -Name KVDeployment `
  -ResourceGroupName $resourceGroup `
  -TemplateFile "<Fully qualified path toohello azuredeploy.json file>" `
  -TemplateParameterFile "<Fully qualified path toohello azuredeploy.parameters.json file>"
```

<span data-ttu-id="66657-138">Cuando se implementa correctamente la plantilla de hello, resulta en hello después de salida:</span><span class="sxs-lookup"><span data-stu-id="66657-138">When hello template is deployed successfully, it results in hello following output:</span></span>

![Salida de la implementación](media\azure-stack-kv-push-secret-into-vm/deployment-output.png)

<span data-ttu-id="66657-140">Cuando se implementa esta máquina virtual, Azure pila inserta certificado hello en máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="66657-140">When this virtual machine is deployed, Azure Stack pushes hello certificate onto hello virtual machine.</span></span> <span data-ttu-id="66657-141">En Windows, certificados de Hola se agregan toohello LocalMachine ubicación del certificado, con el certificado de hello almacenar ese proporcionado por el usuario Hola.</span><span class="sxs-lookup"><span data-stu-id="66657-141">In Windows, hello certificate is added toohello LocalMachine certificate location, with hello certificate store that hello user provided.</span></span> <span data-ttu-id="66657-142">En Linux, Hola certificado se ha colocado en directorio de /var/lib/waagent hello, con el nombre de archivo de hello &lt;UppercaseThumbprint&gt;.crt hello X509 archivo de certificado y &lt;UppercaseThumbprint&gt;.prv para hello clave privada.</span><span class="sxs-lookup"><span data-stu-id="66657-142">In Linux, hello certificate is placed under hello /var/lib/waagent directory, with hello file name &lt;UppercaseThumbprint&gt;.crt for hello X509 certificate file and &lt;UppercaseThumbprint&gt;.prv for hello private key.</span></span>

## <a name="retire-certificates"></a><span data-ttu-id="66657-143">Retirada de certificados</span><span class="sxs-lookup"><span data-stu-id="66657-143">Retire certificates</span></span>

<span data-ttu-id="66657-144">En la sección anterior de hello, le mostramos cómo toopush un nuevo certificado en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="66657-144">In hello preceding section, we showed you how toopush a new certificate onto a virtual machine.</span></span> <span data-ttu-id="66657-145">El certificado antiguo está todavía en la máquina virtual de hello y no se puede quitar.</span><span class="sxs-lookup"><span data-stu-id="66657-145">Your old certificate is still on hello virtual machine, and it can't be removed.</span></span> <span data-ttu-id="66657-146">Sin embargo, se puede deshabilitar versión anterior de Hola de secreto de hello mediante hello `Set-AzureKeyVaultSecretAttribute` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="66657-146">However, you can disable hello older version of hello secret by using hello `Set-AzureKeyVaultSecretAttribute` cmdlet.</span></span> <span data-ttu-id="66657-147">Hola aquí te mostramos un ejemplo de uso de este cmdlet.</span><span class="sxs-lookup"><span data-stu-id="66657-147">hello following is an example usage of this cmdlet.</span></span> <span data-ttu-id="66657-148">Asegúrese de nombre de almacén de hello tooreplace seguro, nombre de secreto y valores de versión según el entorno de tooyour:</span><span class="sxs-lookup"><span data-stu-id="66657-148">Make sure tooreplace hello vault name, secret name, and version values according tooyour environment:</span></span>

```powershell
Set-AzureKeyVaultSecretAttribute -VaultName contosovault -Name servicecert -Version e3391a126b65414f93f6f9806743a1f7 -Enable 0
```

## <a name="next-steps"></a><span data-ttu-id="66657-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="66657-149">Next steps</span></span>

* [<span data-ttu-id="66657-150">Implementación de una máquina virtual con una contraseña de Key Vault</span><span class="sxs-lookup"><span data-stu-id="66657-150">Deploy a VM with a Key Vault password</span></span>](azure-stack-kv-deploy-vm-with-secret.md)
* [<span data-ttu-id="66657-151">Permitir que un almacén de claves de aplicación tooaccess</span><span class="sxs-lookup"><span data-stu-id="66657-151">Allow an application tooaccess Key Vault</span></span>](azure-stack-kv-sample-app.md)


