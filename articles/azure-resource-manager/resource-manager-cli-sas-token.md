---
title: aaaDeploy plantilla de Azure con el token de SAS y la CLI de Azure | Documentos de Microsoft
description: "Use el Administrador de recursos de Azure y Azure CLI toodeploy tooAzure de recursos de una plantilla que esté protegida con token de SAS."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: tomfitz
ms.openlocfilehash: 59c64616d6e1f5e456d88a72854d0ed99e1bdc0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-cli"></a>Implementar la plantilla de Resource Manager privada con el token de SAS y la CLI de Azure

Cuando la plantilla reside en una cuenta de almacenamiento, puede restringir la plantilla de toohello de acceso y proporcionar un token de firma (SAS) de acceso compartido durante la implementación. Este tema se explica cómo toouse PowerShell de Azure con el Administrador de recursos plantillas tooprovide un token SAS durante la implementación. 

## <a name="add-private-template-toostorage-account"></a>Agregar plantilla privada toostorage cuenta

Puede agregar la cuenta de almacenamiento de tooa de plantillas y vincular toothem durante la implementación con un token de SAS.

> [!IMPORTANT]
> Siguiendo estos pasos hello, blob de Hola que contiene la plantilla de hello es propietario de la cuenta de acceso tooonly Hola. Sin embargo, cuando se crea un token SAS para blob hello, blob hello es accesible tooanyone con ese URI. Si otro usuario intercepta Hola URI, ese usuario es tooaccess capaz de plantilla de Hola. Con un token SAS es una buena forma de limitar el acceso tooyour plantillas, pero no debe incluir datos confidenciales tales como contraseñas directamente en la plantilla de Hola.
> 
> 

Hello en el ejemplo siguiente se configura un contenedor de la cuenta de almacenamiento privado y carga una plantilla:
   
```azurecli
az group create --name "ManageGroup" --location "South Central US"
az storage account create \
    --resource-group ManageGroup \
    --location "South Central US" \
    --sku Standard_LRS \
    --kind Storage \
    --name {your-unique-name}
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name {your-unique-name} \
    --query connectionString)
az storage container create \
    --name templates \
    --public-access Off \
    --connection-string $connection
az storage blob upload \
    --container-name templates \
    --file vmlinux.json \
    --name vmlinux.json \
    --connection-string $connection
```

### <a name="provide-sas-token-during-deployment"></a>Provisión del token de SAS durante la implementación
toodeploy una plantilla privada en una cuenta de almacenamiento, generar un token SAS e incluirla en hello URI para la plantilla de Hola. Establecer tooallow de tiempo de expiración de hello suficiente implementación en tiempo de toocomplete Hola.
   
```azurecli
expiretime=$(date -u -d '30 minutes' +%Y-%m-%dT%H:%MZ)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name {your-unique-name} \
    --query connectionString)
token=$(az storage blob generate-sas \
    --container-name templates \
    --name vmlinux.json \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name vmlinux.json \
    --output tsv \
    --connection-string $connection)
az group deployment create --resource-group ExampleGroup --template-uri $url?$token
```

Para obtener un ejemplo del uso de un token de SAS con plantillas vinculadas, consulte [Uso de plantillas vinculadas con Azure Resource Manager](resource-group-linked-templates.md).

## <a name="next-steps"></a>Pasos siguientes
* Para una plantilla de toodeploying introducción, consulte [implementar los recursos con plantillas de administrador de recursos y Azure PowerShell](resource-group-template-deploy-cli.md).
* Para obtener un script de ejemplo completo que implementa una plantilla, vea [Deploy Resource Manager template script](resource-manager-samples-cli-deploy.md) (Implementar script de plantilla de Resource Manager).
* toodefine parámetros de plantilla, vea [crear plantillas](resource-group-authoring-templates.md#parameters).
* Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).
