---
title: "Etiquetado de recursos de Azure para organización lógica | Microsoft Docs"
description: "Muestra cómo aplicar etiquetas para organizar los recursos de Azure para la facturación y administración."
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
ms.openlocfilehash: 4f52c30614ad39da8a34ff6ecfb707b75400517f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="use-tags-to-organize-your-azure-resources"></a><span data-ttu-id="29852-103">Uso de etiquetas para organizar los recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="29852-103">Use tags to organize your Azure resources</span></span>
[!INCLUDE [resource-manager-tag-introduction](../../includes/resource-manager-tag-introduction.md)]

> [!NOTE]
> <span data-ttu-id="29852-104">Solo puede aplicar etiquetas a recursos que admiten operaciones de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="29852-104">You can apply tags only to resources that support Azure Resource Manager operations.</span></span> <span data-ttu-id="29852-105">Si creó una máquina virtual, una red virtual o una cuenta de almacenamiento mediante el modelo de implementación clásica (por ejemplo, a través del Portal de Azure clásico), no podrá aplicar una etiqueta a ese recurso.</span><span class="sxs-lookup"><span data-stu-id="29852-105">If you created a virtual machine, virtual network, or storage account through the classic deployment model (such as through the Azure classic portal), you cannot apply a tag to that resource.</span></span> <span data-ttu-id="29852-106">Para admitir el etiquetado, vuelva a implementar estos recursos mediante Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="29852-106">To support tagging, redeploy these resources through Resource Manager.</span></span> <span data-ttu-id="29852-107">Todos los demás recursos admiten el etiquetado.</span><span class="sxs-lookup"><span data-stu-id="29852-107">All other resources support tagging.</span></span>
> 
> 

## <a name="policies-for-tag-consistency"></a><span data-ttu-id="29852-108">Directivas para la coherencia de etiquetas</span><span class="sxs-lookup"><span data-stu-id="29852-108">Policies for tag consistency</span></span>

<span data-ttu-id="29852-109">Puede usar directivas de recursos para crear reglas estándar para su organización.</span><span class="sxs-lookup"><span data-stu-id="29852-109">You can use resource policies to create standard rules for your organization.</span></span> <span data-ttu-id="29852-110">Puede crear directivas que se aseguren de que los recursos están etiquetados con los valores adecuados.</span><span class="sxs-lookup"><span data-stu-id="29852-110">You can create policies that ensure resources are tagged with the appropriate values.</span></span> <span data-ttu-id="29852-111">Para más información, consulte [Aplicación de directivas de recursos para etiquetas](resource-manager-policy-tags.md).</span><span class="sxs-lookup"><span data-stu-id="29852-111">For more information, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="29852-112">PowerShell</span><span class="sxs-lookup"><span data-stu-id="29852-112">PowerShell</span></span>
[!INCLUDE [resource-manager-tag-resources-powershell](../../includes/resource-manager-tag-resources-powershell.md)]

## <a name="azure-cli"></a><span data-ttu-id="29852-113">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="29852-113">Azure CLI</span></span>

<span data-ttu-id="29852-114">Para ver las etiquetas existentes de un *grupo de recursos*, use:</span><span class="sxs-lookup"><span data-stu-id="29852-114">To see the existing tags for a *resource group*, use:</span></span>

```azurecli
az group show -n examplegroup --query tags
```

<span data-ttu-id="29852-115">Ese script devuelve el siguiente formato:</span><span class="sxs-lookup"><span data-stu-id="29852-115">That script returns the following format:</span></span>

```json
{
  "Dept"        : "IT",
  "Environment" : "Test"
}
```

<span data-ttu-id="29852-116">Para ver las etiquetas existentes de un *recurso que tiene un identificador de recurso especificado*, use:</span><span class="sxs-lookup"><span data-stu-id="29852-116">To see the existing tags for a *resource that has a specified resource ID*, use:</span></span>

```azurecli
az resource show --id {resource-id} --query tags
```

<span data-ttu-id="29852-117">O bien, para ver las etiquetas existentes para un *recurso que tiene un nombre, un tipo y un grupo de recursos especificados*, use:</span><span class="sxs-lookup"><span data-stu-id="29852-117">Or, to see the existing tags for a *resource that has a specified name, type, and resource group*, use:</span></span>

```azurecli
az resource show -n examplevnet -g examplegroup --resource-type "Microsoft.Network/virtualNetworks" --query tags
```

<span data-ttu-id="29852-118">Para obtener grupos de recursos que tengan una etiqueta específica, use `az group list`:</span><span class="sxs-lookup"><span data-stu-id="29852-118">To get resource groups that have a specific tag, use `az group list`:</span></span>

```azurecli
az group list --tag Dept=IT
```

<span data-ttu-id="29852-119">Para obtener todos los recursos que tengan una etiqueta y un valor particulares, use `az resource list`:</span><span class="sxs-lookup"><span data-stu-id="29852-119">To get all the resources that have a particular tag and value, use `az resource list`:</span></span>

```azurecli
az resource list --tag Dept=Finance
```

<span data-ttu-id="29852-120">Cada vez que aplique etiquetas a un recurso o grupo de recursos, sobrescribirá las etiquetas existentes en ese recurso o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="29852-120">Every time you apply tags to a resource or a resource group, you overwrite the existing tags on that resource or resource group.</span></span> <span data-ttu-id="29852-121">Por lo tanto, tiene que utilizar un enfoque diferente en función de si el recurso o grupo de recursos tienen etiquetas existentes.</span><span class="sxs-lookup"><span data-stu-id="29852-121">Therefore, you must use a different approach based on whether the resource or resource group has existing tags.</span></span> 

<span data-ttu-id="29852-122">Para agregar etiquetas a un *grupo de recursos sin etiquetas existentes*, use:</span><span class="sxs-lookup"><span data-stu-id="29852-122">To add tags to a *resource group without existing tags*, use:</span></span>

```azurecli
az group update -n examplegroup --set tags.Environment=Test tags.Dept=IT
```

<span data-ttu-id="29852-123">Para agregar etiquetas a un *recurso sin etiquetas*, use:</span><span class="sxs-lookup"><span data-stu-id="29852-123">To add tags to a *resource without existing tags*, use:</span></span>

```azurecli
az resource tag --tags Dept=IT Environment=Test -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
``` 

<span data-ttu-id="29852-124">Para agregar etiquetas a un recurso que ya tiene etiquetas, recupere las etiquetas existentes, vuelva a formatear el valor y vuelva a aplicar las etiquetas existentes y nuevas:</span><span class="sxs-lookup"><span data-stu-id="29852-124">To add tags to a resource that already has tags, retrieve the existing tags, reformat that value, and reapply the existing and new tags:</span></span> 

```azurecli
jsonrtag=$(az resource show -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks" --query tags)
rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
az resource tag --tags $rt Project=Redesign -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
```

<span data-ttu-id="29852-125">Para aplicar todas las etiquetas de un grupo de recursos a sus recursos y *no conservar ninguna de las etiquetas existentes en los recursos*, use el siguiente script:</span><span class="sxs-lookup"><span data-stu-id="29852-125">To apply all tags from a resource group to its resources, and *not retain existing tags on the resources*, use the following script:</span></span>

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

<span data-ttu-id="29852-126">Para aplicar todas las etiquetas de un grupo de recursos a sus recursos y *conservar las etiquetas existentes en los recursos*, use el siguiente script:</span><span class="sxs-lookup"><span data-stu-id="29852-126">To apply all tags from a resource group to its resources, and *retain existing tags on resources*, use the following script:</span></span>

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


## <a name="templates"></a><span data-ttu-id="29852-127">Plantillas</span><span class="sxs-lookup"><span data-stu-id="29852-127">Templates</span></span>

[!INCLUDE [resource-manager-tags-in-templates](../../includes/resource-manager-tags-in-templates.md)]

## <a name="portal"></a><span data-ttu-id="29852-128">Portal</span><span class="sxs-lookup"><span data-stu-id="29852-128">Portal</span></span>
[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]


## <a name="rest-api"></a><span data-ttu-id="29852-129">API de REST</span><span class="sxs-lookup"><span data-stu-id="29852-129">REST API</span></span>
<span data-ttu-id="29852-130">Tanto Azure Portal como PowerShell usan la [API de REST de Resource Manager](https://docs.microsoft.com/rest/api/resources/) en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="29852-130">The Azure portal and PowerShell both use the [Resource Manager REST API](https://docs.microsoft.com/rest/api/resources/) behind the scenes.</span></span> <span data-ttu-id="29852-131">Si necesita integrar el etiquetado en otro entorno, puede obtener etiquetas con un comando **GET** en el identificador de recurso y actualizar el conjunto de etiquetas con una llamada **PATCH**.</span><span class="sxs-lookup"><span data-stu-id="29852-131">If you need to integrate tagging into another environment, you can get tags by using **GET** on the resource ID and update the set of tags by using a **PATCH** call.</span></span>

## <a name="tags-and-billing"></a><span data-ttu-id="29852-132">Etiquetas y facturación</span><span class="sxs-lookup"><span data-stu-id="29852-132">Tags and billing</span></span>
<span data-ttu-id="29852-133">Puede usar etiquetas a fin de agrupar los datos de facturación.</span><span class="sxs-lookup"><span data-stu-id="29852-133">You can use tags to group your billing data.</span></span> <span data-ttu-id="29852-134">Por ejemplo, si va a ejecutar varias máquinas virtuales para organizaciones diferentes, use etiquetas para agrupar el uso por centro de costo.</span><span class="sxs-lookup"><span data-stu-id="29852-134">For example, if you are running multiple VMs for different organizations, use the tags to group usage by cost center.</span></span> <span data-ttu-id="29852-135">También puede usar etiquetas para clasificar los costos por entorno de tiempo de ejecución; por ejemplo, el uso de facturación en máquinas virtuales que se ejecutan en el entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="29852-135">You can also use tags to categorize costs by runtime environment, such as the billing usage for VMs running in the production environment.</span></span>


<span data-ttu-id="29852-136">Puede recuperar información sobre las etiquetas a través de las [API de RateCard y de uso de recursos de Azure](../billing/billing-usage-rate-card-overview.md) o mediante el archivo de valores separados por coma (CSV).</span><span class="sxs-lookup"><span data-stu-id="29852-136">You can retrieve information about tags through the [Azure Resource Usage and RateCard APIs](../billing/billing-usage-rate-card-overview.md) or the usage comma-separated values (CSV) file.</span></span> <span data-ttu-id="29852-137">Puede descargar el archivo de uso en el [Portal de cuentas de Azure](https://account.windowsazure.com/) o el [portal EA](https://ea.azure.com).</span><span class="sxs-lookup"><span data-stu-id="29852-137">You download the usage file from the [Azure account portal](https://account.windowsazure.com/) or [EA portal](https://ea.azure.com).</span></span> <span data-ttu-id="29852-138">Para obtener más información sobre el acceso a información de facturación mediante programación, vea [Obtención de información sobre el consumo de recursos de Microsoft Azure](../billing/billing-usage-rate-card-overview.md).</span><span class="sxs-lookup"><span data-stu-id="29852-138">For more information about programmatic access to billing information, see [Gain insights into your Microsoft Azure resource consumption](../billing/billing-usage-rate-card-overview.md).</span></span> <span data-ttu-id="29852-139">Para las operaciones de API de REST, vea [Referencia de API de REST de facturación de Azure](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span><span class="sxs-lookup"><span data-stu-id="29852-139">For REST API operations, see [Azure Billing REST API Reference](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span></span>


<span data-ttu-id="29852-140">Al descargar el CSV de uso correspondiente a los servicios que admiten etiquetas con facturación, las etiquetas aparecen en la columna **Etiquetas** .</span><span class="sxs-lookup"><span data-stu-id="29852-140">When you download the usage CSV for services that support tags with billing, the tags appear in the **Tags** column.</span></span> <span data-ttu-id="29852-141">Para más información, consulte [Comprender la factura de Microsoft Azure](../billing/billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="29852-141">For more information, see [Understand your bill for Microsoft Azure](../billing/billing-understand-your-bill.md).</span></span>

![Ver etiquetas en la facturación](./media/resource-group-using-tags/billing_csv.png)

## <a name="next-steps"></a><span data-ttu-id="29852-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="29852-143">Next steps</span></span>
* <span data-ttu-id="29852-144">Puede aplicar restricciones y convenciones a través de su suscripción con directivas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="29852-144">You can apply restrictions and conventions across your subscription by using customized policies.</span></span> <span data-ttu-id="29852-145">La directiva que define podría requerir que todos los recursos tengan un valor para una etiqueta determinada.</span><span class="sxs-lookup"><span data-stu-id="29852-145">A policy that you define might require that all resources have a value for a particular tag.</span></span> <span data-ttu-id="29852-146">Para obtener más información, consulte [Uso de directivas para administrar los recursos y controlar el acceso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="29852-146">For more information, see [Use policies to manage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="29852-147">Para obtener información sobre cómo usar Azure PowerShell al implementar recursos, consulte [Uso de Azure PowerShell con Azure Resource Manager](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="29852-147">For an introduction to using Azure PowerShell when you're deploying resources, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="29852-148">Para obtener información sobre cómo usar la interfaz de la línea de comandos (CLI) de Azure al implementar recursos, consulte [Uso de la CLI de Azure para Mac, Linux y Windows con Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="29852-148">For an introduction to using the Azure CLI when you're deploying resources, see [Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="29852-149">Para obtener información sobre cómo usar el portal, consulte [Uso de Azure Portal para administrar los recursos de Azure](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="29852-149">For an introduction to using the portal, see [Using the Azure portal to manage your Azure resources](resource-group-portal.md).</span></span>  
* <span data-ttu-id="29852-150">Para obtener instrucciones sobre cómo las empresas pueden utilizar Resource Manager para administrar eficazmente las suscripciones, vea [Scaffold empresarial de Azure: Gobierno de suscripción prescriptivo](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="29852-150">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

