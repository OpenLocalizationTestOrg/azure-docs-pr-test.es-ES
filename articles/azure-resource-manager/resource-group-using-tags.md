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
# <a name="use-tags-tooorganize-your-azure-resources"></a><span data-ttu-id="ecd7d-103">Usar etiquetas tooorganize los recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="ecd7d-103">Use tags tooorganize your Azure resources</span></span>
[!INCLUDE [resource-manager-tag-introduction](../../includes/resource-manager-tag-introduction.md)]

> [!NOTE]
> <span data-ttu-id="ecd7d-104">Puede aplicar etiquetas tooresources única que admiten operaciones de administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="ecd7d-104">You can apply tags only tooresources that support Azure Resource Manager operations.</span></span> <span data-ttu-id="ecd7d-105">Si ha creado una máquina virtual, la red virtual o la cuenta de almacenamiento a través del modelo de implementación clásica de hello (por ejemplo Hola como a través portal de Azure clásico), no se puede aplicar un recurso de toothat de etiqueta.</span><span class="sxs-lookup"><span data-stu-id="ecd7d-105">If you created a virtual machine, virtual network, or storage account through hello classic deployment model (such as through hello Azure classic portal), you cannot apply a tag toothat resource.</span></span> <span data-ttu-id="ecd7d-106">toosupport etiquetado, vuelva a implementar estos recursos a través del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="ecd7d-106">toosupport tagging, redeploy these resources through Resource Manager.</span></span> <span data-ttu-id="ecd7d-107">Todos los demás recursos admiten el etiquetado.</span><span class="sxs-lookup"><span data-stu-id="ecd7d-107">All other resources support tagging.</span></span>
> 
> 

## <a name="policies-for-tag-consistency"></a><span data-ttu-id="ecd7d-108">Directivas para la coherencia de etiquetas</span><span class="sxs-lookup"><span data-stu-id="ecd7d-108">Policies for tag consistency</span></span>

<span data-ttu-id="ecd7d-109">Puede usar reglas estándar de toocreate de directivas de recursos para su organización.</span><span class="sxs-lookup"><span data-stu-id="ecd7d-109">You can use resource policies toocreate standard rules for your organization.</span></span> <span data-ttu-id="ecd7d-110">Puede crear directivas que se aseguran de recursos se etiquetan con los valores adecuados de Hola.</span><span class="sxs-lookup"><span data-stu-id="ecd7d-110">You can create policies that ensure resources are tagged with hello appropriate values.</span></span> <span data-ttu-id="ecd7d-111">Para más información, consulte [Aplicación de directivas de recursos para etiquetas](resource-manager-policy-tags.md).</span><span class="sxs-lookup"><span data-stu-id="ecd7d-111">For more information, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="ecd7d-112">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ecd7d-112">PowerShell</span></span>
[!INCLUDE [resource-manager-tag-resources-powershell](../../includes/resource-manager-tag-resources-powershell.md)]

## <a name="azure-cli"></a><span data-ttu-id="ecd7d-113">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="ecd7d-113">Azure CLI</span></span>

<span data-ttu-id="ecd7d-114">toosee Hola las etiquetas existentes para un *grupo de recursos*, use:</span><span class="sxs-lookup"><span data-stu-id="ecd7d-114">toosee hello existing tags for a *resource group*, use:</span></span>

```azurecli
az group show -n examplegroup --query tags
```

<span data-ttu-id="ecd7d-115">Este script devuelve Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="ecd7d-115">That script returns hello following format:</span></span>

```json
{
  "Dept"        : "IT",
  "Environment" : "Test"
}
```

<span data-ttu-id="ecd7d-116">toosee Hola las etiquetas existentes para un *recurso con un identificador de recurso especificado*, use:</span><span class="sxs-lookup"><span data-stu-id="ecd7d-116">toosee hello existing tags for a *resource that has a specified resource ID*, use:</span></span>

```azurecli
az resource show --id {resource-id} --query tags
```

<span data-ttu-id="ecd7d-117">O bien, toosee Hola las etiquetas existentes para un *recurso con un grupo de recursos, tipo y nombre especificado*, usar:</span><span class="sxs-lookup"><span data-stu-id="ecd7d-117">Or, toosee hello existing tags for a *resource that has a specified name, type, and resource group*, use:</span></span>

```azurecli
az resource show -n examplevnet -g examplegroup --resource-type "Microsoft.Network/virtualNetworks" --query tags
```

<span data-ttu-id="ecd7d-118">grupos de recursos de tooget que tienen una etiqueta específica, use `az group list`:</span><span class="sxs-lookup"><span data-stu-id="ecd7d-118">tooget resource groups that have a specific tag, use `az group list`:</span></span>

```azurecli
az group list --tag Dept=IT
```

<span data-ttu-id="ecd7d-119">tooget todos los recursos de Hola que tienen una etiqueta determinada y un valor, use `az resource list`:</span><span class="sxs-lookup"><span data-stu-id="ecd7d-119">tooget all hello resources that have a particular tag and value, use `az resource list`:</span></span>

```azurecli
az resource list --tag Dept=Finance
```

<span data-ttu-id="ecd7d-120">Cada vez que aplica etiquetas tooa recurso o un grupo de recursos, sobrescribir las etiquetas existentes hello en ese recurso o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ecd7d-120">Every time you apply tags tooa resource or a resource group, you overwrite hello existing tags on that resource or resource group.</span></span> <span data-ttu-id="ecd7d-121">Por lo tanto, debe utilizar un enfoque diferente en función de si el recurso de Hola o grupo de recursos tiene las etiquetas existentes.</span><span class="sxs-lookup"><span data-stu-id="ecd7d-121">Therefore, you must use a different approach based on whether hello resource or resource group has existing tags.</span></span> 

<span data-ttu-id="ecd7d-122">etiquetas de tooadd tooa *grupo de recursos sin las etiquetas existentes*, use:</span><span class="sxs-lookup"><span data-stu-id="ecd7d-122">tooadd tags tooa *resource group without existing tags*, use:</span></span>

```azurecli
az group update -n examplegroup --set tags.Environment=Test tags.Dept=IT
```

<span data-ttu-id="ecd7d-123">etiquetas de tooadd tooa *recurso sin las etiquetas existentes*, use:</span><span class="sxs-lookup"><span data-stu-id="ecd7d-123">tooadd tags tooa *resource without existing tags*, use:</span></span>

```azurecli
az resource tag --tags Dept=IT Environment=Test -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
``` 

<span data-ttu-id="ecd7d-124">recurso de tooa de etiquetas de tooadd que ya tiene etiquetas, recuperar las etiquetas existentes hello, volver a formatear ese valor y volver a aplicar etiquetas nuevas y existentes de hello:</span><span class="sxs-lookup"><span data-stu-id="ecd7d-124">tooadd tags tooa resource that already has tags, retrieve hello existing tags, reformat that value, and reapply hello existing and new tags:</span></span> 

```azurecli
jsonrtag=$(az resource show -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks" --query tags)
rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
az resource tag --tags $rt Project=Redesign -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
```

<span data-ttu-id="ecd7d-125">tooapply todas las etiquetas de recursos de tooits del grupo de recursos, y *no conservar las etiquetas existentes en los recursos de hello*, usar hello siguiente secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="ecd7d-125">tooapply all tags from a resource group tooits resources, and *not retain existing tags on hello resources*, use hello following script:</span></span>

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

<span data-ttu-id="ecd7d-126">tooapply todas las etiquetas de recursos de tooits del grupo de recursos, y *conservar las etiquetas existentes en los recursos*, usar hello siguiente secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="ecd7d-126">tooapply all tags from a resource group tooits resources, and *retain existing tags on resources*, use hello following script:</span></span>

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


## <a name="templates"></a><span data-ttu-id="ecd7d-127">Plantillas</span><span class="sxs-lookup"><span data-stu-id="ecd7d-127">Templates</span></span>

[!INCLUDE [resource-manager-tags-in-templates](../../includes/resource-manager-tags-in-templates.md)]

## <a name="portal"></a><span data-ttu-id="ecd7d-128">Portal</span><span class="sxs-lookup"><span data-stu-id="ecd7d-128">Portal</span></span>
[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]


## <a name="rest-api"></a><span data-ttu-id="ecd7d-129">API de REST</span><span class="sxs-lookup"><span data-stu-id="ecd7d-129">REST API</span></span>
<span data-ttu-id="ecd7d-130">Hello portal de Azure y PowerShell usan hello [API de REST del Administrador de recursos](https://docs.microsoft.com/rest/api/resources/) entre bastidores de Hola.</span><span class="sxs-lookup"><span data-stu-id="ecd7d-130">hello Azure portal and PowerShell both use hello [Resource Manager REST API](https://docs.microsoft.com/rest/api/resources/) behind hello scenes.</span></span> <span data-ttu-id="ecd7d-131">Si necesita toointegrate etiquetado en otro entorno, puede obtener etiquetas mediante **obtener** en hello Id. y actualización Hola conjunto de recursos de etiquetas mediante el uso de un **PATCH** llamar.</span><span class="sxs-lookup"><span data-stu-id="ecd7d-131">If you need toointegrate tagging into another environment, you can get tags by using **GET** on hello resource ID and update hello set of tags by using a **PATCH** call.</span></span>

## <a name="tags-and-billing"></a><span data-ttu-id="ecd7d-132">Etiquetas y facturación</span><span class="sxs-lookup"><span data-stu-id="ecd7d-132">Tags and billing</span></span>
<span data-ttu-id="ecd7d-133">Puede utilizar etiquetas toogroup los datos de facturación.</span><span class="sxs-lookup"><span data-stu-id="ecd7d-133">You can use tags toogroup your billing data.</span></span> <span data-ttu-id="ecd7d-134">Por ejemplo, si se ejecutan varias máquinas virtuales para organizaciones diferentes, utilice Hola etiquetas toogroup uso por el centro de costo.</span><span class="sxs-lookup"><span data-stu-id="ecd7d-134">For example, if you are running multiple VMs for different organizations, use hello tags toogroup usage by cost center.</span></span> <span data-ttu-id="ecd7d-135">También puede utilizar etiquetas toocategorize costos por el entorno en tiempo de ejecución, como el uso de facturación de Hola para máquinas virtuales en ejecución en el entorno de producción de hello.</span><span class="sxs-lookup"><span data-stu-id="ecd7d-135">You can also use tags toocategorize costs by runtime environment, such as hello billing usage for VMs running in hello production environment.</span></span>


<span data-ttu-id="ecd7d-136">Puede recuperar información acerca de las etiquetas a través de hello [uso de recursos de Azure y RateCard APIs](../billing/billing-usage-rate-card-overview.md) o archivo de valores separados por comas (CSV) de uso de hello.</span><span class="sxs-lookup"><span data-stu-id="ecd7d-136">You can retrieve information about tags through hello [Azure Resource Usage and RateCard APIs](../billing/billing-usage-rate-card-overview.md) or hello usage comma-separated values (CSV) file.</span></span> <span data-ttu-id="ecd7d-137">Descargar archivo de uso de hello de hello [portal de cuenta de Azure](https://account.windowsazure.com/) o [portal EA](https://ea.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ecd7d-137">You download hello usage file from hello [Azure account portal](https://account.windowsazure.com/) or [EA portal](https://ea.azure.com).</span></span> <span data-ttu-id="ecd7d-138">Para obtener más información acerca de la información de toobilling de acceso mediante programación, vea [obtener información sobre el consumo de recursos de Microsoft Azure](../billing/billing-usage-rate-card-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ecd7d-138">For more information about programmatic access toobilling information, see [Gain insights into your Microsoft Azure resource consumption](../billing/billing-usage-rate-card-overview.md).</span></span> <span data-ttu-id="ecd7d-139">Para las operaciones de API de REST, vea [Referencia de API de REST de facturación de Azure](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span><span class="sxs-lookup"><span data-stu-id="ecd7d-139">For REST API operations, see [Azure Billing REST API Reference](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span></span>


<span data-ttu-id="ecd7d-140">Cuando se descarga el uso de hello CSV para servicios que admiten etiquetas con la facturación, etiquetas de hello aparecen en hello **etiquetas** columna.</span><span class="sxs-lookup"><span data-stu-id="ecd7d-140">When you download hello usage CSV for services that support tags with billing, hello tags appear in hello **Tags** column.</span></span> <span data-ttu-id="ecd7d-141">Para más información, consulte [Comprender la factura de Microsoft Azure](../billing/billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="ecd7d-141">For more information, see [Understand your bill for Microsoft Azure](../billing/billing-understand-your-bill.md).</span></span>

![Ver etiquetas en la facturación](./media/resource-group-using-tags/billing_csv.png)

## <a name="next-steps"></a><span data-ttu-id="ecd7d-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ecd7d-143">Next steps</span></span>
* <span data-ttu-id="ecd7d-144">Puede aplicar restricciones y convenciones a través de su suscripción con directivas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="ecd7d-144">You can apply restrictions and conventions across your subscription by using customized policies.</span></span> <span data-ttu-id="ecd7d-145">La directiva que define podría requerir que todos los recursos tengan un valor para una etiqueta determinada.</span><span class="sxs-lookup"><span data-stu-id="ecd7d-145">A policy that you define might require that all resources have a value for a particular tag.</span></span> <span data-ttu-id="ecd7d-146">Para obtener más información, consulte [usar directivas toomanage recursos y controlar el acceso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="ecd7d-146">For more information, see [Use policies toomanage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="ecd7d-147">Para una toousing Introducción Azure PowerShell al implementar los recursos, consulte [con Azure PowerShell con el Administrador de recursos de Azure](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="ecd7d-147">For an introduction toousing Azure PowerShell when you're deploying resources, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="ecd7d-148">Para un Hola de toousing Introducción CLI de Azure cuando va a implementar los recursos, vea [Using Hola CLI de Azure para Mac, Linux y Windows con el Administrador de recursos de Azure](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="ecd7d-148">For an introduction toousing hello Azure CLI when you're deploying resources, see [Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="ecd7d-149">Para un portal de hello toousing de introducción, consulte [Using Hola toomanage portal Azure de los recursos de Azure](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ecd7d-149">For an introduction toousing hello portal, see [Using hello Azure portal toomanage your Azure resources](resource-group-portal.md).</span></span>  
* <span data-ttu-id="ecd7d-150">Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="ecd7d-150">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

