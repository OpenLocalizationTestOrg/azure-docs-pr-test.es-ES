---
title: "aaaTag Azure recursos para la organización lógica | Documentos de Microsoft"
description: "Muestra cómo tooapply etiquetas tooorganize Azure recursos de facturación y la administración."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 003a78e5-2ff8-4685-93b4-e94d6fb8ed5b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: AzurePortal
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: tomfitz
ms.openlocfilehash: e07470463d160f8cefe5c80bc91e66a96af6ca45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-tags-tooorganize-your-azure-resources"></a>Usar etiquetas tooorganize los recursos de Azure
[!INCLUDE [resource-manager-tag-introduction](../../includes/resource-manager-tag-introduction.md)]

> [!NOTE]
> Puede aplicar etiquetas tooresources única que admiten operaciones de administrador de recursos de Azure. Si ha creado una máquina virtual, la red virtual o la cuenta de almacenamiento a través del modelo de implementación clásica de hello (por ejemplo Hola como a través portal de Azure clásico), no se puede aplicar un recurso de toothat de etiqueta. toosupport etiquetado, vuelva a implementar estos recursos a través del Administrador de recursos. Todos los demás recursos admiten el etiquetado.
> 
> 

## <a name="policies-for-tag-consistency"></a>Directivas para la coherencia de etiquetas

Puede usar reglas estándar de toocreate de directivas de recursos para su organización. Puede crear directivas que se aseguran de recursos se etiquetan con los valores adecuados de Hola. Para más información, consulte [Aplicación de directivas de recursos para etiquetas](resource-manager-policy-tags.md).

## <a name="powershell"></a>PowerShell
[!INCLUDE [resource-manager-tag-resources-powershell](../../includes/resource-manager-tag-resources-powershell.md)]

## <a name="azure-cli"></a>CLI de Azure

toosee Hola las etiquetas existentes para un *grupo de recursos*, use:

```azurecli
az group show -n examplegroup --query tags
```

Este script devuelve Hola siguiendo el formato:

```json
{
  "Dept"        : "IT",
  "Environment" : "Test"
}
```

toosee Hola las etiquetas existentes para un *recurso con un identificador de recurso especificado*, use:

```azurecli
az resource show --id {resource-id} --query tags
```

O bien, toosee Hola las etiquetas existentes para un *recurso con un grupo de recursos, tipo y nombre especificado*, usar:

```azurecli
az resource show -n examplevnet -g examplegroup --resource-type "Microsoft.Network/virtualNetworks" --query tags
```

grupos de recursos de tooget que tienen una etiqueta específica, use `az group list`:

```azurecli
az group list --tag Dept=IT
```

tooget todos los recursos de Hola que tienen una etiqueta determinada y un valor, use `az resource list`:

```azurecli
az resource list --tag Dept=Finance
```

Cada vez que aplica etiquetas tooa recurso o un grupo de recursos, sobrescribir las etiquetas existentes hello en ese recurso o grupo de recursos. Por lo tanto, debe utilizar un enfoque diferente en función de si el recurso de Hola o grupo de recursos tiene las etiquetas existentes. 

etiquetas de tooadd tooa *grupo de recursos sin las etiquetas existentes*, use:

```azurecli
az group update -n examplegroup --set tags.Environment=Test tags.Dept=IT
```

etiquetas de tooadd tooa *recurso sin las etiquetas existentes*, use:

```azurecli
az resource tag --tags Dept=IT Environment=Test -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
``` 

recurso de tooa de etiquetas de tooadd que ya tiene etiquetas, recuperar las etiquetas existentes hello, volver a formatear ese valor y volver a aplicar etiquetas nuevas y existentes de hello: 

```azurecli
jsonrtag=$(az resource show -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks" --query tags)
rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
az resource tag --tags $rt Project=Redesign -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
```

tooapply todas las etiquetas de recursos de tooits del grupo de recursos, y *no conservar las etiquetas existentes en los recursos de hello*, usar hello siguiente secuencia de comandos:

```azurecli
groups=$(az group list --query [].name --output tsv)
for rg in $groups 
do 
  jsontag=$(az group show -n $rg --query tags)
  t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')
  r=$(az resource list -g $rg --query [].id --output tsv) 
  for resid in $r 
  do 
    az resource tag --tags $t --id $resid
  done 
done
```

tooapply todas las etiquetas de recursos de tooits del grupo de recursos, y *conservar las etiquetas existentes en los recursos*, usar hello siguiente secuencia de comandos:

```azurecli
groups=$(az group list --query [].name --output tsv)
for rg in $groups 
do 
  jsontag=$(az group show -n $rg --query tags)
  t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')
  r=$(az resource list -g $rg --query [].id --output tsv) 
  for resid in $r 
  do 
    jsonrtag=$(az resource show --id $resid --query tags)
    rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
    az resource tag --tags $t$rt --id $resid
  done 
done
```


## <a name="templates"></a>Plantillas

[!INCLUDE [resource-manager-tags-in-templates](../../includes/resource-manager-tags-in-templates.md)]

## <a name="portal"></a>Portal
[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]


## <a name="rest-api"></a>API de REST
Hello portal de Azure y PowerShell usan hello [API de REST del Administrador de recursos](https://docs.microsoft.com/rest/api/resources/) entre bastidores de Hola. Si necesita toointegrate etiquetado en otro entorno, puede obtener etiquetas mediante **obtener** en hello Id. y actualización Hola conjunto de recursos de etiquetas mediante el uso de un **PATCH** llamar.

## <a name="tags-and-billing"></a>Etiquetas y facturación
Puede utilizar etiquetas toogroup los datos de facturación. Por ejemplo, si se ejecutan varias máquinas virtuales para organizaciones diferentes, utilice Hola etiquetas toogroup uso por el centro de costo. También puede utilizar etiquetas toocategorize costos por el entorno en tiempo de ejecución, como el uso de facturación de Hola para máquinas virtuales en ejecución en el entorno de producción de hello.


Puede recuperar información acerca de las etiquetas a través de hello [uso de recursos de Azure y RateCard APIs](../billing/billing-usage-rate-card-overview.md) o archivo de valores separados por comas (CSV) de uso de hello. Descargar archivo de uso de hello de hello [portal de cuenta de Azure](https://account.windowsazure.com/) o [portal EA](https://ea.azure.com). Para obtener más información acerca de la información de toobilling de acceso mediante programación, vea [obtener información sobre el consumo de recursos de Microsoft Azure](../billing/billing-usage-rate-card-overview.md). Para las operaciones de API de REST, vea [Referencia de API de REST de facturación de Azure](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).


Cuando se descarga el uso de hello CSV para servicios que admiten etiquetas con la facturación, etiquetas de hello aparecen en hello **etiquetas** columna. Para más información, consulte [Comprender la factura de Microsoft Azure](../billing/billing-understand-your-bill.md).

![Ver etiquetas en la facturación](./media/resource-group-using-tags/billing_csv.png)

## <a name="next-steps"></a>Pasos siguientes
* Puede aplicar restricciones y convenciones a través de su suscripción con directivas personalizadas. La directiva que define podría requerir que todos los recursos tengan un valor para una etiqueta determinada. Para obtener más información, consulte [usar directivas toomanage recursos y controlar el acceso](resource-manager-policy.md).
* Para una toousing Introducción Azure PowerShell al implementar los recursos, consulte [con Azure PowerShell con el Administrador de recursos de Azure](powershell-azure-resource-manager.md).
* Para un Hola de toousing Introducción CLI de Azure cuando va a implementar los recursos, vea [Using Hola CLI de Azure para Mac, Linux y Windows con el Administrador de recursos de Azure](xplat-cli-azure-resource-manager.md).
* Para un portal de hello toousing de introducción, consulte [Using Hola toomanage portal Azure de los recursos de Azure](resource-group-portal.md).  
* Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).

