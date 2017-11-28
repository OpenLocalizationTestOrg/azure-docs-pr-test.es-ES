---
title: "Configuración del acceso a WinRM para una máquina virtual de Azure | Microsoft Docs"
description: "Configure el acceso a WinRM para usarlo con una máquina virtual Azure creada con el modelo de implementación de Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 9718e85b-d360-4621-90b8-0b0b84a21208
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/16/2016
ms.author: kasing
ms.openlocfilehash: 2d6533462400bc1d93d0d3b0227769784e2658a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="setting-up-winrm-access-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="8f77e-103">Configuración de acceso a WinRM para máquinas virtuales en Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8f77e-103">Setting up WinRM access for Virtual Machines in Azure Resource Manager</span></span>
## <a name="winrm-in-azure-service-management-vs-azure-resource-manager"></a><span data-ttu-id="8f77e-104">WinRM en administración de servicios de Azure frente a Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8f77e-104">WinRM in Azure Service Management vs Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

* <span data-ttu-id="8f77e-105">Para ver información general sobre Azure Resource Manager, consulte este [artículo](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="8f77e-105">For an overview of the Azure Resource Manager, please see this [article](../../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="8f77e-106">Para conocer las diferencias entre la administración de servicios de Azure y Azure Resource Manager, consulte este [artículo](../../resource-manager-deployment-model.md)</span><span class="sxs-lookup"><span data-stu-id="8f77e-106">For differences between Azure Service Management and Azure Resource Manager, please see this [article](../../resource-manager-deployment-model.md)</span></span>

<span data-ttu-id="8f77e-107">La diferencia clave en la configuración de WinRM entre las dos pilas es el modo en que se instala el certificado en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8f77e-107">The key difference in setting up WinRM configuration between the two stacks is how the certificate gets installed on the VM.</span></span> <span data-ttu-id="8f77e-108">En la pila de Azure Resource Manager, los certificados se modelan como recursos que se administran mediante el proveedor de recursos del Almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="8f77e-108">In the Azure Resource Manager stack, the certificates are modeled as resources managed by the Key Vault Resource Provider.</span></span> <span data-ttu-id="8f77e-109">Por lo tanto, el usuario debe proporcionar su propio certificado y cargarlo en un Almacén de claves antes de usar una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8f77e-109">Therefore, the user needs to provide their own certificate and upload it to a Key Vault before using it in a VM.</span></span>

<span data-ttu-id="8f77e-110">Estos son los pasos que debe seguir para configurar una máquina virtual con conectividad de WinRM.</span><span class="sxs-lookup"><span data-stu-id="8f77e-110">Here are the steps you need to take to set up a VM with WinRM connectivity</span></span>

1. <span data-ttu-id="8f77e-111">Creación de un Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="8f77e-111">Create a Key Vault</span></span>
2. <span data-ttu-id="8f77e-112">Creación de un certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="8f77e-112">Create a self-signed certificate</span></span>
3. <span data-ttu-id="8f77e-113">Carga del certificado autofirmado en el Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="8f77e-113">Upload your self-signed certificate to Key Vault</span></span>
4. <span data-ttu-id="8f77e-114">Obtención de la dirección URL para el certificado autofirmado en el Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="8f77e-114">Get the URL for your self-signed certificate in the Key Vault</span></span>
5. <span data-ttu-id="8f77e-115">Referencia a la dirección URL de los certificados autofirmados durante la creación de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8f77e-115">Reference your self-signed certificates URL while creating a VM</span></span>

## <a name="step-1-create-a-key-vault"></a><span data-ttu-id="8f77e-116">Paso 1: Creación de un Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="8f77e-116">Step 1: Create a Key Vault</span></span>
<span data-ttu-id="8f77e-117">Puede utilizar el siguiente comando para crear el Almacén de claves:</span><span class="sxs-lookup"><span data-stu-id="8f77e-117">You can use the below command to create the Key Vault</span></span>

```
New-AzureRmKeyVault -VaultName "<vault-name>" -ResourceGroupName "<rg-name>" -Location "<vault-location>" -EnabledForDeployment -EnabledForTemplateDeployment
```

## <a name="step-2-create-a-self-signed-certificate"></a><span data-ttu-id="8f77e-118">Paso 2: Creación de un certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="8f77e-118">Step 2: Create a self-signed certificate</span></span>
<span data-ttu-id="8f77e-119">Puede crear un certificado autofirmado mediante este script de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8f77e-119">You can create a self-signed certificate using this PowerShell script</span></span>

```
$certificateName = "somename"

$thumbprint = (New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation Cert:\CurrentUser\My -KeySpec KeyExchange).Thumbprint

$cert = (Get-ChildItem -Path cert:\CurrentUser\My\$thumbprint)

$password = Read-Host -Prompt "Please enter the certificate password." -AsSecureString

Export-PfxCertificate -Cert $cert -FilePath ".\$certificateName.pfx" -Password $password
```

## <a name="step-3-upload-your-self-signed-certificate-to-the-key-vault"></a><span data-ttu-id="8f77e-120">Paso 3: Carga del certificado autofirmado en el Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="8f77e-120">Step 3: Upload your self-signed certificate to the Key Vault</span></span>
<span data-ttu-id="8f77e-121">Antes de cargar el certificado en el Almacén de claves que creó en el paso 1, debe convertirlo a un formato que entienda el proveedor de recursos Microsoft.Compute.</span><span class="sxs-lookup"><span data-stu-id="8f77e-121">Before uploading the certificate to the Key Vault created in step 1, it needs to converted into a format the Microsoft.Compute resource provider will understand.</span></span> <span data-ttu-id="8f77e-122">El siguiente script de PowerShell le permitirá hacer eso:</span><span class="sxs-lookup"><span data-stu-id="8f77e-122">The below PowerShell script will allow you do that</span></span>

```
$fileName = "<Path to the .pfx file>"
$fileContentBytes = Get-Content $fileName -Encoding Byte
$fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

$jsonObject = @"
{
  "data": "$filecontentencoded",
  "dataType" :"pfx",
  "password": "<password>"
}
"@

$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText –Force
Set-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>" -SecretValue $secret
```

## <a name="step-4-get-the-url-for-your-self-signed-certificate-in-the-key-vault"></a><span data-ttu-id="8f77e-123">Paso 4: Obtención de la dirección URL del certificado autofirmado en el Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="8f77e-123">Step 4: Get the URL for your self-signed certificate in the Key Vault</span></span>
<span data-ttu-id="8f77e-124">El proveedor de recursos Microsoft.Compute necesita una dirección URL al secreto en el Almacén de claves durante el aprovisionamiento de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8f77e-124">The Microsoft.Compute resource provider needs a URL to the secret inside the Key Vault while provisioning the VM.</span></span> <span data-ttu-id="8f77e-125">De esta manera, dicho proveedor podrá descargar el secreto y crear el certificado equivalente en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8f77e-125">This enables the Microsoft.Compute resource provider to download the secret and create the equivalent certificate on the VM.</span></span>

> [!NOTE]
> <span data-ttu-id="8f77e-126">La dirección URL del secreto debe incluir también la versión.</span><span class="sxs-lookup"><span data-stu-id="8f77e-126">The URL of the secret needs to include the version as well.</span></span> <span data-ttu-id="8f77e-127">Este es un ejemplo de una dirección URL de este tipo https://contosovault.vault.azure.net:443/secretos/contososecret/01h9db0df2cd4300a20ence585a6s7ve</span><span class="sxs-lookup"><span data-stu-id="8f77e-127">An example URL looks like below https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve</span></span>
> 
> 

#### <a name="templates"></a><span data-ttu-id="8f77e-128">Plantillas</span><span class="sxs-lookup"><span data-stu-id="8f77e-128">Templates</span></span>
<span data-ttu-id="8f77e-129">Puede obtener el vínculo a la dirección URL en la plantilla mediante el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="8f77e-129">You can get the link to the URL in the template using the below code</span></span>

    "certificateUrl": "[reference(resourceId(resourceGroup().name, 'Microsoft.KeyVault/vaults/secrets', '<vault-name>', '<secret-name>'), '2015-06-01').secretUriWithVersion]"

#### <a name="powershell"></a><span data-ttu-id="8f77e-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f77e-130">PowerShell</span></span>
<span data-ttu-id="8f77e-131">Puede obtener esta dirección URL mediante el siguiente comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8f77e-131">You can get this URL using the below PowerShell command</span></span>

    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id

## <a name="step-5-reference-your-self-signed-certificates-url-while-creating-a-vm"></a><span data-ttu-id="8f77e-132">Paso 5: Referencia a la dirección URL de los certificados autofirmados durante la creación de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8f77e-132">Step 5: Reference your self-signed certificates URL while creating a VM</span></span>
#### <a name="azure-resource-manager-templates"></a><span data-ttu-id="8f77e-133">Plantillas del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="8f77e-133">Azure Resource Manager Templates</span></span>
<span data-ttu-id="8f77e-134">Al crear una máquina virtual mediante plantillas, se hace referencia al certificado en la sección de secretos y en la sección de WinRM de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="8f77e-134">While creating a VM through templates, the certificate gets referenced in the secrets section and the winRM section as below:</span></span>

    "osProfile": {
          ...
          "secrets": [
            {
              "sourceVault": {
                "id": "<resource id of the Key Vault containing the secret>"
              },
              "vaultCertificates": [
                {
                  "certificateUrl": "<URL for the certificate you got in Step 4>",
                  "certificateStore": "<Name of the certificate store on the VM>"
                }
              ]
            }
          ],
          "windowsConfiguration": {
            ...
            "winRM": {
              "listeners": [
                {
                  "protocol": "http"
                },
                {
                  "protocol": "https",
                  "certificateUrl": "<URL for the certificate you got in Step 4>"
                }
              ]
            },
            ...
          }
        },

<span data-ttu-id="8f77e-135">Una plantilla de ejemplo para el caso mencionado se puede encontrar aquí en [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="8f77e-135">A sample template for the above can be found here at [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span></span>

<span data-ttu-id="8f77e-136">El código fuente de esta plantilla está disponible en [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="8f77e-136">Source code for this template can be found on [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span></span>

#### <a name="powershell"></a><span data-ttu-id="8f77e-137">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f77e-137">PowerShell</span></span>
    $vm = New-AzureRmVMConfig -VMName "<VM name>" -VMSize "<VM Size>"
    $credential = Get-Credential
    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName "<Computer Name>" -Credential $credential -WinRMHttp -WinRMHttps -WinRMCertificateUrl $secretURL
    $sourceVaultId = (Get-AzureRmKeyVault -ResourceGroupName "<Resource Group name>" -VaultName "<Vault Name>").ResourceId
    $CertificateStore = "My"
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore $CertificateStore -CertificateUrl $secretURL

## <a name="step-6-connecting-to-the-vm"></a><span data-ttu-id="8f77e-138">Paso 6: Conexión a la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8f77e-138">Step 6: Connecting to the VM</span></span>
<span data-ttu-id="8f77e-139">Antes de poder conectarse a la máquina virtual, debe asegurarse de que el equipo esté configurado para la administración remota de WinRM.</span><span class="sxs-lookup"><span data-stu-id="8f77e-139">Before you can connect to the VM you'll need to make sure your machine is configured for WinRM remote management.</span></span> <span data-ttu-id="8f77e-140">Inicie PowerShell como administrador y ejecute el siguiente comando para asegurarse de que se encuentra en el programa de instalación.</span><span class="sxs-lookup"><span data-stu-id="8f77e-140">Start PowerShell as an administrator and execute the below command to make sure you're set up.</span></span>

    Enable-PSRemoting -Force

> [!NOTE]
> <span data-ttu-id="8f77e-141">Si la solución anterior no funciona, debe asegurarse de que el servicio WinRM esté en ejecución.</span><span class="sxs-lookup"><span data-stu-id="8f77e-141">You might need to make sure the WinRM service is running if the above does not work.</span></span> <span data-ttu-id="8f77e-142">Para ello, utilice `Get-Service WinRM`</span><span class="sxs-lookup"><span data-stu-id="8f77e-142">You can do that using `Get-Service WinRM`</span></span>
> 
> 

<span data-ttu-id="8f77e-143">Cuando haya finalizado la instalación, puede conectarse a la máquina virtual mediante el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="8f77e-143">Once the setup is done, you can connect to the VM using the below command</span></span>

    Enter-PSSession -ConnectionUri https://<public-ip-dns-of-the-vm>:5986 -Credential $cred -SessionOption (New-PSSessionOption -SkipCACheck -SkipCNCheck -SkipRevocationCheck) -Authentication Negotiate
