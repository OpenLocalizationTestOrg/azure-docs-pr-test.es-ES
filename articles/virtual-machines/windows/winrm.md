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
# <a name="setting-up-winrm-access-for-virtual-machines-in-azure-resource-manager"></a>Configuración de acceso a WinRM para máquinas virtuales en Azure Resource Manager
## <a name="winrm-in-azure-service-management-vs-azure-resource-manager"></a>WinRM en administración de servicios de Azure frente a Azure Resource Manager

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

* Para obtener información general de hello Azure Resource Manager, consulte la [artículo](../../azure-resource-manager/resource-group-overview.md)
* Para conocer las diferencias entre la administración de servicios de Azure y Azure Resource Manager, consulte este [artículo](../../resource-manager-deployment-model.md)

Hello diferencia clave al establecer la configuración de WinRM entre las dos pilas de hello es cómo se instala el certificado de hello en hello máquina virtual. En la pila del Administrador de recursos de Azure hello, certificados de Hola se modelan como recursos administrados por hello el proveedor de recursos del almacén de claves. Por lo tanto, usuario de hello tooprovide, necesita su propio certificado y cargarlo tooa el almacén de claves antes de usarlo en una máquina virtual.

Estos son los pasos de hello necesita tootake tooset seguridad de una máquina virtual con conectividad de WinRM

1. Creación de un Almacén de claves
2. Creación de un certificado autofirmado
3. Cargar el almacén de certificado autofirmado tooKey
4. Obtener dirección URL de hello para el certificado autofirmado en el almacén de claves de Hola
5. Referencia a la dirección URL de los certificados autofirmados durante la creación de una máquina virtual

## <a name="step-1-create-a-key-vault"></a>Paso 1: Creación de un Almacén de claves
Puede usar hello debajo de comando toocreate hello el almacén de claves

```
New-AzureRmKeyVault -VaultName "<vault-name>" -ResourceGroupName "<rg-name>" -Location "<vault-location>" -EnabledForDeployment -EnabledForTemplateDeployment
```

## <a name="step-2-create-a-self-signed-certificate"></a>Paso 2: Creación de un certificado autofirmado
Puede crear un certificado autofirmado mediante este script de PowerShell:

```
$certificateName = "somename"

$thumbprint = (New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation Cert:\CurrentUser\My -KeySpec KeyExchange).Thumbprint

$cert = (Get-ChildItem -Path cert:\CurrentUser\My\$thumbprint)

$password = Read-Host -Prompt "Please enter hello certificate password." -AsSecureString

Export-PfxCertificate -Cert $cert -FilePath ".\$certificateName.pfx" -Password $password
```

## <a name="step-3-upload-your-self-signed-certificate-toohello-key-vault"></a>Paso 3: Cargar el almacén de claves de certificado de firma automática toohello
Antes de cargar Hola certificado toohello el almacén de claves creado en el paso 1, debe tooconverted en un Hola formato Microsoft.Compute comprenderá el proveedor de recursos. Hola siguiente script de PowerShell le permitirá que hacer que

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

## <a name="step-4-get-hello-url-for-your-self-signed-certificate-in-hello-key-vault"></a>Paso 4: Obtener la dirección URL de hello para el certificado autofirmado en el almacén de claves de Hola
proveedor de recursos de Microsoft.Compute Hola necesita un secreto de toohello de dirección URL en el almacén de claves de Hola durante el aprovisionamiento Hola VM. Esto permite secreto Hola de toodownload de proveedor de recursos de hello Microsoft.Compute y crear certificado equivalente de hello en hello máquina virtual.

> [!NOTE]
> dirección URL de Hola de secreto de hello debe tooinclude Hola versión reciente. Este es un ejemplo de una dirección URL de este tipo https://contosovault.vault.azure.net:443/secretos/contososecret/01h9db0df2cd4300a20ence585a6s7ve
> 
> 

#### <a name="templates"></a>Plantillas
Puede obtener dirección URL de toohello de vínculo de hello en plantilla de hello mediante Hola por debajo del código

    "certificateUrl": "[reference(resourceId(resourceGroup().name, 'Microsoft.KeyVault/vaults/secrets', '<vault-name>', '<secret-name>'), '2015-06-01').secretUriWithVersion]"

#### <a name="powershell"></a>PowerShell
Puede obtener esta dirección URL mediante Hola comando PowerShell siguiente

    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id

## <a name="step-5-reference-your-self-signed-certificates-url-while-creating-a-vm"></a>Paso 5: Referencia a la dirección URL de los certificados autofirmados durante la creación de una máquina virtual
#### <a name="azure-resource-manager-templates"></a>Plantillas del Administrador de recursos de Azure
Al crear una máquina virtual a través de plantillas, obtiene hace referencia al certificado de Hola de sección de secretos de Hola y Hola winRM como sigue:

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

Una plantilla de ejemplo de Hola anterior puede encontrarse aquí en [201 vm winrm keyvault windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)

El código fuente de esta plantilla está disponible en [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)

#### <a name="powershell"></a>PowerShell
    $vm = New-AzureRmVMConfig -VMName "<VM name>" -VMSize "<VM Size>"
    $credential = Get-Credential
    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName "<Computer Name>" -Credential $credential -WinRMHttp -WinRMHttps -WinRMCertificateUrl $secretURL
    $sourceVaultId = (Get-AzureRmKeyVault -ResourceGroupName "<Resource Group name>" -VaultName "<Vault Name>").ResourceId
    $CertificateStore = "My"
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore $CertificateStore -CertificateUrl $secretURL

## <a name="step-6-connecting-toohello-vm"></a>Paso 6: Conexión toohello VM
Antes de poder conectar toohello VM deberá toomake que su equipo está configurado para la administración remota de WinRM. Inicie PowerShell como administrador y ejecute hello debajo de comando toomake seguro de que esté listo.

    Enable-PSRemoting -Force

> [!NOTE]
> Puede que tenga toomake que Hola servicio WinRM se esté ejecutando si Hola anterior no funciona. Para ello, utilice `Get-Service WinRM`
> 
> 

Una vez que se realiza el programa de instalación de hello, puede conectarse toohello VM mediante Hola comando siguiente

    Enter-PSSession -ConnectionUri https://<public-ip-dns-of-the-vm>:5986 -Credential $cred -SessionOption (New-PSSessionOption -SkipCACheck -SkipCNCheck -SkipRevocationCheck) -Authentication Negotiate
