---
title: "aaaSet el acceso de WinRM para una máquina virtual de Azure | Documentos de Microsoft"
description: "Configurar el acceso de WinRM para su uso con una máquina virtual de Azure creada en el modelo de implementación del Administrador de recursos de Hola."
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
ms.openlocfilehash: 23d1d3a3065cbd8e4036be085c6d835cae36caae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-winrm-access-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="96057-103">Configuración de acceso a WinRM para máquinas virtuales en Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="96057-103">Setting up WinRM access for Virtual Machines in Azure Resource Manager</span></span>
## <a name="winrm-in-azure-service-management-vs-azure-resource-manager"></a><span data-ttu-id="96057-104">WinRM en administración de servicios de Azure frente a Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="96057-104">WinRM in Azure Service Management vs Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

* <span data-ttu-id="96057-105">Para obtener información general de hello Azure Resource Manager, consulte la [artículo](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="96057-105">For an overview of hello Azure Resource Manager, please see this [article](../../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="96057-106">Para conocer las diferencias entre la administración de servicios de Azure y Azure Resource Manager, consulte este [artículo](../../resource-manager-deployment-model.md)</span><span class="sxs-lookup"><span data-stu-id="96057-106">For differences between Azure Service Management and Azure Resource Manager, please see this [article](../../resource-manager-deployment-model.md)</span></span>

<span data-ttu-id="96057-107">Hello diferencia clave al establecer la configuración de WinRM entre las dos pilas de hello es cómo se instala el certificado de hello en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="96057-107">hello key difference in setting up WinRM configuration between hello two stacks is how hello certificate gets installed on hello VM.</span></span> <span data-ttu-id="96057-108">En la pila del Administrador de recursos de Azure hello, certificados de Hola se modelan como recursos administrados por hello el proveedor de recursos del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="96057-108">In hello Azure Resource Manager stack, hello certificates are modeled as resources managed by hello Key Vault Resource Provider.</span></span> <span data-ttu-id="96057-109">Por lo tanto, usuario de hello tooprovide, necesita su propio certificado y cargarlo tooa el almacén de claves antes de usarlo en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="96057-109">Therefore, hello user needs tooprovide their own certificate and upload it tooa Key Vault before using it in a VM.</span></span>

<span data-ttu-id="96057-110">Estos son los pasos de hello necesita tootake tooset seguridad de una máquina virtual con conectividad de WinRM</span><span class="sxs-lookup"><span data-stu-id="96057-110">Here are hello steps you need tootake tooset up a VM with WinRM connectivity</span></span>

1. <span data-ttu-id="96057-111">Creación de un Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="96057-111">Create a Key Vault</span></span>
2. <span data-ttu-id="96057-112">Creación de un certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="96057-112">Create a self-signed certificate</span></span>
3. <span data-ttu-id="96057-113">Cargar el almacén de certificado autofirmado tooKey</span><span class="sxs-lookup"><span data-stu-id="96057-113">Upload your self-signed certificate tooKey Vault</span></span>
4. <span data-ttu-id="96057-114">Obtener dirección URL de hello para el certificado autofirmado en el almacén de claves de Hola</span><span class="sxs-lookup"><span data-stu-id="96057-114">Get hello URL for your self-signed certificate in hello Key Vault</span></span>
5. <span data-ttu-id="96057-115">Referencia a la dirección URL de los certificados autofirmados durante la creación de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="96057-115">Reference your self-signed certificates URL while creating a VM</span></span>

## <a name="step-1-create-a-key-vault"></a><span data-ttu-id="96057-116">Paso 1: Creación de un Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="96057-116">Step 1: Create a Key Vault</span></span>
<span data-ttu-id="96057-117">Puede usar hello debajo de comando toocreate hello el almacén de claves</span><span class="sxs-lookup"><span data-stu-id="96057-117">You can use hello below command toocreate hello Key Vault</span></span>

```
New-AzureRmKeyVault -VaultName "<vault-name>" -ResourceGroupName "<rg-name>" -Location "<vault-location>" -EnabledForDeployment -EnabledForTemplateDeployment
```

## <a name="step-2-create-a-self-signed-certificate"></a><span data-ttu-id="96057-118">Paso 2: Creación de un certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="96057-118">Step 2: Create a self-signed certificate</span></span>
<span data-ttu-id="96057-119">Puede crear un certificado autofirmado mediante este script de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="96057-119">You can create a self-signed certificate using this PowerShell script</span></span>

```
$certificateName = "somename"

$thumbprint = (New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation Cert:\CurrentUser\My -KeySpec KeyExchange).Thumbprint

$cert = (Get-ChildItem -Path cert:\CurrentUser\My\$thumbprint)

$password = Read-Host -Prompt "Please enter hello certificate password." -AsSecureString

Export-PfxCertificate -Cert $cert -FilePath ".\$certificateName.pfx" -Password $password
```

## <a name="step-3-upload-your-self-signed-certificate-toohello-key-vault"></a><span data-ttu-id="96057-120">Paso 3: Cargar el almacén de claves de certificado de firma automática toohello</span><span class="sxs-lookup"><span data-stu-id="96057-120">Step 3: Upload your self-signed certificate toohello Key Vault</span></span>
<span data-ttu-id="96057-121">Antes de cargar Hola certificado toohello el almacén de claves creado en el paso 1, debe tooconverted en un Hola formato Microsoft.Compute comprenderá el proveedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="96057-121">Before uploading hello certificate toohello Key Vault created in step 1, it needs tooconverted into a format hello Microsoft.Compute resource provider will understand.</span></span> <span data-ttu-id="96057-122">Hola siguiente script de PowerShell le permitirá que hacer que</span><span class="sxs-lookup"><span data-stu-id="96057-122">hello below PowerShell script will allow you do that</span></span>

```
$fileName = "<Path toohello .pfx file>"
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

## <a name="step-4-get-hello-url-for-your-self-signed-certificate-in-hello-key-vault"></a><span data-ttu-id="96057-123">Paso 4: Obtener la dirección URL de hello para el certificado autofirmado en el almacén de claves de Hola</span><span class="sxs-lookup"><span data-stu-id="96057-123">Step 4: Get hello URL for your self-signed certificate in hello Key Vault</span></span>
<span data-ttu-id="96057-124">proveedor de recursos de Microsoft.Compute Hola necesita un secreto de toohello de dirección URL en el almacén de claves de Hola durante el aprovisionamiento Hola VM.</span><span class="sxs-lookup"><span data-stu-id="96057-124">hello Microsoft.Compute resource provider needs a URL toohello secret inside hello Key Vault while provisioning hello VM.</span></span> <span data-ttu-id="96057-125">Esto permite secreto Hola de toodownload de proveedor de recursos de hello Microsoft.Compute y crear certificado equivalente de hello en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="96057-125">This enables hello Microsoft.Compute resource provider toodownload hello secret and create hello equivalent certificate on hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="96057-126">dirección URL de Hola de secreto de hello debe tooinclude Hola versión reciente.</span><span class="sxs-lookup"><span data-stu-id="96057-126">hello URL of hello secret needs tooinclude hello version as well.</span></span> <span data-ttu-id="96057-127">Este es un ejemplo de una dirección URL de este tipo https://contosovault.vault.azure.net:443/secretos/contososecret/01h9db0df2cd4300a20ence585a6s7ve</span><span class="sxs-lookup"><span data-stu-id="96057-127">An example URL looks like below https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve</span></span>
> 
> 

#### <a name="templates"></a><span data-ttu-id="96057-128">Plantillas</span><span class="sxs-lookup"><span data-stu-id="96057-128">Templates</span></span>
<span data-ttu-id="96057-129">Puede obtener dirección URL de toohello de vínculo de hello en plantilla de hello mediante Hola por debajo del código</span><span class="sxs-lookup"><span data-stu-id="96057-129">You can get hello link toohello URL in hello template using hello below code</span></span>

    "certificateUrl": "[reference(resourceId(resourceGroup().name, 'Microsoft.KeyVault/vaults/secrets', '<vault-name>', '<secret-name>'), '2015-06-01').secretUriWithVersion]"

#### <a name="powershell"></a><span data-ttu-id="96057-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="96057-130">PowerShell</span></span>
<span data-ttu-id="96057-131">Puede obtener esta dirección URL mediante Hola comando PowerShell siguiente</span><span class="sxs-lookup"><span data-stu-id="96057-131">You can get this URL using hello below PowerShell command</span></span>

    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id

## <a name="step-5-reference-your-self-signed-certificates-url-while-creating-a-vm"></a><span data-ttu-id="96057-132">Paso 5: Referencia a la dirección URL de los certificados autofirmados durante la creación de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="96057-132">Step 5: Reference your self-signed certificates URL while creating a VM</span></span>
#### <a name="azure-resource-manager-templates"></a><span data-ttu-id="96057-133">Plantillas del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="96057-133">Azure Resource Manager Templates</span></span>
<span data-ttu-id="96057-134">Al crear una máquina virtual a través de plantillas, obtiene hace referencia al certificado de Hola de sección de secretos de Hola y Hola winRM como sigue:</span><span class="sxs-lookup"><span data-stu-id="96057-134">While creating a VM through templates, hello certificate gets referenced in hello secrets section and hello winRM section as below:</span></span>

    "osProfile": {
          ...
          "secrets": [
            {
              "sourceVault": {
                "id": "<resource id of hello Key Vault containing hello secret>"
              },
              "vaultCertificates": [
                {
                  "certificateUrl": "<URL for hello certificate you got in Step 4>",
                  "certificateStore": "<Name of hello certificate store on hello VM>"
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
                  "certificateUrl": "<URL for hello certificate you got in Step 4>"
                }
              ]
            },
            ...
          }
        },

<span data-ttu-id="96057-135">Una plantilla de ejemplo de Hola anterior puede encontrarse aquí en [201 vm winrm keyvault windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="96057-135">A sample template for hello above can be found here at [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span></span>

<span data-ttu-id="96057-136">El código fuente de esta plantilla está disponible en [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="96057-136">Source code for this template can be found on [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span></span>

#### <a name="powershell"></a><span data-ttu-id="96057-137">PowerShell</span><span class="sxs-lookup"><span data-stu-id="96057-137">PowerShell</span></span>
    $vm = New-AzureRmVMConfig -VMName "<VM name>" -VMSize "<VM Size>"
    $credential = Get-Credential
    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName "<Computer Name>" -Credential $credential -WinRMHttp -WinRMHttps -WinRMCertificateUrl $secretURL
    $sourceVaultId = (Get-AzureRmKeyVault -ResourceGroupName "<Resource Group name>" -VaultName "<Vault Name>").ResourceId
    $CertificateStore = "My"
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore $CertificateStore -CertificateUrl $secretURL

## <a name="step-6-connecting-toohello-vm"></a><span data-ttu-id="96057-138">Paso 6: Conexión toohello VM</span><span class="sxs-lookup"><span data-stu-id="96057-138">Step 6: Connecting toohello VM</span></span>
<span data-ttu-id="96057-139">Antes de poder conectar toohello VM deberá toomake que su equipo está configurado para la administración remota de WinRM.</span><span class="sxs-lookup"><span data-stu-id="96057-139">Before you can connect toohello VM you'll need toomake sure your machine is configured for WinRM remote management.</span></span> <span data-ttu-id="96057-140">Inicie PowerShell como administrador y ejecute hello debajo de comando toomake seguro de que esté listo.</span><span class="sxs-lookup"><span data-stu-id="96057-140">Start PowerShell as an administrator and execute hello below command toomake sure you're set up.</span></span>

    Enable-PSRemoting -Force

> [!NOTE]
> <span data-ttu-id="96057-141">Puede que tenga toomake que Hola servicio WinRM se esté ejecutando si Hola anterior no funciona.</span><span class="sxs-lookup"><span data-stu-id="96057-141">You might need toomake sure hello WinRM service is running if hello above does not work.</span></span> <span data-ttu-id="96057-142">Para ello, utilice `Get-Service WinRM`</span><span class="sxs-lookup"><span data-stu-id="96057-142">You can do that using `Get-Service WinRM`</span></span>
> 
> 

<span data-ttu-id="96057-143">Una vez que se realiza el programa de instalación de hello, puede conectarse toohello VM mediante Hola comando siguiente</span><span class="sxs-lookup"><span data-stu-id="96057-143">Once hello setup is done, you can connect toohello VM using hello below command</span></span>

    Enter-PSSession -ConnectionUri https://<public-ip-dns-of-the-vm>:5986 -Credential $cred -SessionOption (New-PSSessionOption -SkipCACheck -SkipCNCheck -SkipRevocationCheck) -Authentication Negotiate
