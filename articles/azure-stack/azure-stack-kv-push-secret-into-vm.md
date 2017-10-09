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
# <a name="create-a-virtual-machine-and-include-certificate-retrieved-from-a-key-vault"></a>Creación de una máquina virtual e inclusión de un certificado recuperado de un almacén de claves

Este artículo le ayude toocreate una máquina virtual en la pila de Azure y certificados de inserción en él. 

## <a name="prerequisites"></a>Requisitos previos

* Deben tener los administradores de la nube de Azure pila [crea una oferta](azure-stack-create-offer.md) que incluye el servicio de almacén de claves de Azure de Hola.  
* Los usuarios deben [suscribirse tooan oferta](azure-stack-subscribe-plan-provision-vm.md) que incluye el servicio de almacén de claves de Hola.  
* [Instale PowerShell para Azure Stack.](azure-stack-powershell-install.md)  
* [Configurar el entorno de PowerShell del usuario de hello pila de Azure](azure-stack-powershell-configure-user.md)

Un almacén de claves en la pila de Azure es toostore usa certificados. Los certificados son útiles en varios escenarios diferentes. Por ejemplo, considere un escenario en el que haya una máquina virtual en Azure Stack que está ejecutando una aplicación que necesita un certificado. Este certificado se puede utilizar para cifrar, para autenticar tooActive Directory o SSL en un sitio Web. Tener certificado hello en un almacén de claves, le ayuda a asegurarse de que es segura.

En este artículo, le guiaremos por hello pasos necesarios toopush un certificado en una máquina virtual de Windows en la pila de Azure. Puede usar estos pasos desde Hola Kit de desarrollo de pila de Azure, o desde un cliente externo basado en Windows, si está conectado a través de VPN.

Hola pasos describe hello toopush de proceso requerido un certificado en la máquina virtual de hello:

1. Cree un secreto de almacén de claves.
2. Actualizar archivo de hello azuredeploy.parameters.json.
3. Implementar la plantilla de Hola

## <a name="create-a-key-vault-secret"></a>Creación de un secreto de almacén de claves

Hello script siguiente crea un certificado en formato .pfx de hello, crea un almacén de claves y almacena el certificado de hello en el almacén de claves de Hola como un secreto. Debe usar hello `-EnabledForDeployment` parámetro al crear el almacén de claves Hola. Este parámetro se asegura de ese almacén de claves de hello puede hacer referencia a partir de plantillas de Azure Resource Manager.

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

Cuando se ejecuta el script anterior hello, salida de hello incluye secreto Hola URI. Anote este URI. Tendrá que tooreference en hello [insertar certificado tooWindows plantilla del Administrador de recursos](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows). Descargar hello [plantilla de vm inserción certificado windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows) carpeta en el equipo de desarrollo. Esta carpeta contiene Hola `azuredeploy.json` y `azuredeploy.parameters.json` archivos, lo que necesitará en pasos de Hola.

Modificar hello `azuredeploy.parameters.json` archivo según tooyour valores de entorno. parámetros de Hola de especial interés son el nombre del almacén de hello, grupo de recursos de almacén de Hola y Hola secreto URI (como las generadas por script anterior Hola). Hola el archivo siguiente es un ejemplo de un archivo de parámetros:

## <a name="update-hello-azuredeployparametersjson-file"></a>Archivo de actualización hello azuredeploy.parameters.json

Actualizar archivo de hello azuredeploy.parameters.json con el nombre de almacén de hello, URI secreto, VmName y otros valores según el entorno. Hello archivo JSON siguiente muestra un ejemplo de archivo de parámetros de plantilla de hello: 

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

## <a name="deploy-hello-template"></a>Implementar la plantilla de Hola

Ahora puede implementar plantilla hello mediante Hola siguiente script de PowerShell:

```powershell
# Deploy a Resource Manager template toocreate a VM and push hello secret onto it
New-AzureRmResourceGroupDeployment `
  -Name KVDeployment `
  -ResourceGroupName $resourceGroup `
  -TemplateFile "<Fully qualified path toohello azuredeploy.json file>" `
  -TemplateParameterFile "<Fully qualified path toohello azuredeploy.parameters.json file>"
```

Cuando se implementa correctamente la plantilla de hello, resulta en hello después de salida:

![Salida de la implementación](media\azure-stack-kv-push-secret-into-vm/deployment-output.png)

Cuando se implementa esta máquina virtual, Azure pila inserta certificado hello en máquina virtual de Hola. En Windows, certificados de Hola se agregan toohello LocalMachine ubicación del certificado, con el certificado de hello almacenar ese proporcionado por el usuario Hola. En Linux, Hola certificado se ha colocado en directorio de /var/lib/waagent hello, con el nombre de archivo de hello &lt;UppercaseThumbprint&gt;.crt hello X509 archivo de certificado y &lt;UppercaseThumbprint&gt;.prv para hello clave privada.

## <a name="retire-certificates"></a>Retirada de certificados

En la sección anterior de hello, le mostramos cómo toopush un nuevo certificado en una máquina virtual. El certificado antiguo está todavía en la máquina virtual de hello y no se puede quitar. Sin embargo, se puede deshabilitar versión anterior de Hola de secreto de hello mediante hello `Set-AzureKeyVaultSecretAttribute` cmdlet. Hola aquí te mostramos un ejemplo de uso de este cmdlet. Asegúrese de nombre de almacén de hello tooreplace seguro, nombre de secreto y valores de versión según el entorno de tooyour:

```powershell
Set-AzureKeyVaultSecretAttribute -VaultName contosovault -Name servicecert -Version e3391a126b65414f93f6f9806743a1f7 -Enable 0
```

## <a name="next-steps"></a>Pasos siguientes

* [Implementación de una máquina virtual con una contraseña de Key Vault](azure-stack-kv-deploy-vm-with-secret.md)
* [Permitir que un almacén de claves de aplicación tooaccess](azure-stack-kv-sample-app.md)


