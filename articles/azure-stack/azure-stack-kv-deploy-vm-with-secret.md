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
# <a name="create-a-virtual-machine-by-retrieving-hello-password-stored-in-a-key-vault"></a>Crear una máquina virtual mediante la recuperación de contraseña de hello almacenada en un almacén de claves

Cuando necesite toopass un valor como una contraseña seguro durante la implementación, puede almacenar ese valor como un secreto en un almacén de claves de la pila de Azure y hacer referencia a él en las plantillas de Azure Resource Manager Hola. No es necesario toomanually escriba secreto Hola cada vez que implemente recursos hello, también puede especificar qué usuarios o entidades de servicio pueden tener acceso a secreto Hola. 

En este artículo, le guiaremos por hello pasos necesarios toodeploy una máquina virtual de Windows en la pila de Azure mediante la recuperación de contraseña de Hola que se almacena en un almacén de claves. Por lo tanto, contraseña de hello nunca se coloca en texto sin formato en el archivo de parámetros de plantilla de Hola. Puede usar estos pasos desde Hola Kit de desarrollo de pila de Azure, o desde un cliente externo si está conectado a través de VPN.

## <a name="prerequisites"></a>Requisitos previos

* Deben tener los administradores de la nube de Azure pila [crea una oferta](azure-stack-create-offer.md) que incluye el servicio de almacén de claves de Azure de Hola.  
* Los usuarios deben [suscribirse tooan oferta](azure-stack-subscribe-plan-provision-vm.md) que incluye el servicio de almacén de claves de Hola.  
* [Instale PowerShell para Azure Stack.](azure-stack-powershell-install.md)  
* [Configurar el entorno de PowerShell del usuario de hello Azure pila.](azure-stack-powershell-configure-user.md)

Hello siguientes pasos describen Hola proceso necesario toocreate una máquina virtual mediante la recuperación de contraseña de hello almacenada en un almacén de claves:

1. Cree un secreto de almacén de claves.
2. Actualizar archivo de hello azuredeploy.parameters.json.
3. Implementar la plantilla de Hola.

## <a name="create-a-key-vault-secret"></a>Creación de un secreto de almacén de claves

Hello secuencia de comandos siguiente crea un almacén de claves y almacena una contraseña en el almacén de claves de Hola como un secreto. Hola de uso `-EnabledForDeployment` parámetro al crear el almacén de claves Hola. Este parámetro se asegura de ese almacén de claves de hello puede hacer referencia a partir de plantillas de Azure Resource Manager.

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

Cuando se ejecuta el script anterior hello, salida de hello incluye secreto Hola URI. Anote este URI. Tendrá que tooreference en hello [máquina virtual de implementar Windows con contraseña en la plantilla de almacén de claves](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-secure-password). Descargar hello [101-vm-proteger-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-secure-password) carpeta en el equipo de desarrollo. Esta carpeta contiene Hola `azuredeploy.json` y `azuredeploy.parameters.json` archivos, lo que necesitará en pasos de Hola.

Modificar hello `azuredeploy.parameters.json` archivo según tooyour valores de entorno. parámetros de Hola de especial interés son el nombre del almacén de hello, grupo de recursos de almacén de Hola y Hola secreto URI (como las generadas por script anterior Hola). Hola el archivo siguiente es un ejemplo de un archivo de parámetros:

## <a name="update-hello-azuredeployparametersjson-file"></a>Archivo de actualización hello azuredeploy.parameters.json

Actualizar archivo de hello azuredeploy.parameters.json con hello KeyVault URI, secretName, adminUsername de valores de la máquina virtual de hello según su entorno. Hello archivo JSON siguiente muestra un ejemplo de archivo de parámetros de plantilla de hello: 

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

## <a name="template-deployment"></a>Implementación de plantilla

Ahora puede implementar plantilla hello mediante Hola siguiente script de PowerShell:

```powershell
New-AzureRmResourceGroupDeployment `
  -Name KVPwdDeployment `
  -ResourceGroupName $resourceGroup `
  -TemplateFile "<Fully qualified path toohello azuredeploy.json file>" `
  -TemplateParameterFile "<Fully qualified path toohello azuredeploy.parameters.json file>"
```
Cuando se implementa correctamente la plantilla de hello, resulta en hello después de salida:

![Salida de la implementación](media\azure-stack-kv-deploy-vm-with-secret/deployment-output.png)


## <a name="next-steps"></a>Pasos siguientes
[Implementación de una aplicación de ejemplo con Key Vault](azure-stack-kv-sample-app.md)

[Implementación de una máquina virtual con un certificado de Key Vault](azure-stack-kv-push-secret-into-vm.md)

