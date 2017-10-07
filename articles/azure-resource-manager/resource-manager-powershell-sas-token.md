---
title: plantilla de Azure con PowerShell y el token de SAS aaaDeploy | Documentos de Microsoft
description: "Use el Administrador de recursos de Azure y Azure PowerShell toodeploy tooAzure de recursos de una plantilla que esté protegida con token de SAS."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: b95e096591d6213f8ef79235c8cd85705c4b79ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-powershell"></a>Implementar la plantilla de Resource Manager privada con el token de SAS y Azure PowerShell

Cuando la plantilla reside en una cuenta de almacenamiento, puede restringir la plantilla de toohello de acceso y proporcionar un token de firma (SAS) de acceso compartido durante la implementación. Este tema se explica cómo toouse PowerShell de Azure con el Administrador de recursos plantillas tooprovide un token SAS durante la implementación. 

## <a name="add-private-template-toostorage-account"></a>Agregar plantilla privada toostorage cuenta

Puede agregar la cuenta de almacenamiento de tooa de plantillas y vincular toothem durante la implementación con un token de SAS.

> [!IMPORTANT]
> Siguiendo estos pasos hello, blob de Hola que contiene la plantilla de hello es propietario de la cuenta de acceso tooonly Hola. Sin embargo, cuando se crea un token SAS para blob hello, blob hello es accesible tooanyone con ese URI. Si otro usuario intercepta Hola URI, ese usuario es tooaccess capaz de plantilla de Hola. Con un token SAS es una buena forma de limitar el acceso tooyour plantillas, pero no debe incluir datos confidenciales tales como contraseñas directamente en la plantilla de Hola.
> 
> 

Hello en el ejemplo siguiente se configura un contenedor de la cuenta de almacenamiento privado y carga una plantilla:
   
```powershell
# create a storage account for templates
New-AzureRmResourceGroup -Name ManageGroup -Location "South Central US"
New-AzureRmStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name} -Type Standard_LRS -Location "West US"
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# create a container and upload template
New-AzureStorageContainer -Name templates -Permission Off
Set-AzureStorageBlobContent -Container templates -File c:\MyTemplates\storage.json
```

## <a name="provide-sas-token-during-deployment"></a>Provisión del token de SAS durante la implementación
toodeploy una plantilla privada en una cuenta de almacenamiento, generar un token SAS e incluirla en hello URI para la plantilla de Hola. Establecer tooallow de tiempo de expiración de hello suficiente implementación en tiempo de toocomplete Hola.
   
```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# get hello URI with hello SAS token
$templateuri = New-AzureStorageBlobSASToken -Container templates -Blob storage.json -Permission r `
  -ExpiryTime (Get-Date).AddHours(2.0) -FullUri

# provide URI with SAS token during deployment
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri $templateuri
```

Para obtener un ejemplo del uso de un token de SAS con plantillas vinculadas, consulte [Uso de plantillas vinculadas con Azure Resource Manager](resource-group-linked-templates.md).


## <a name="next-steps"></a>Pasos siguientes
* Para una plantilla de toodeploying introducción, consulte [implementar los recursos con plantillas de administrador de recursos y Azure PowerShell](resource-group-template-deploy.md).
* Para obtener un script de ejemplo completo que implementa una plantilla, vea [Deploy Resource Manager template script](resource-manager-samples-powershell-deploy.md) (Implementar script de plantilla de Resource Manager).
* toodefine parámetros de plantilla, vea [crear plantillas](resource-group-authoring-templates.md#parameters).
* Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).

