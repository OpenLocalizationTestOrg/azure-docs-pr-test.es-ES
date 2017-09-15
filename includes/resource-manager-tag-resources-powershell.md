<span data-ttu-id="5f5b0-101">La versión 3.0 del módulo AzureRm.Resources incluye cambios significativos en la forma de trabajar con las etiquetas.</span><span class="sxs-lookup"><span data-stu-id="5f5b0-101">Version 3.0 of the AzureRm.Resources module included significant changes in how you work with tags.</span></span> <span data-ttu-id="5f5b0-102">Antes de continuar, compruebe su versión:</span><span class="sxs-lookup"><span data-stu-id="5f5b0-102">Before you proceed, check your version:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="5f5b0-103">Si el resultado muestra una versión 3.0 o posterior, los ejemplos de este tema funcionan con su entorno.</span><span class="sxs-lookup"><span data-stu-id="5f5b0-103">If your results show version 3.0 or later, the examples in this topic work with your environment.</span></span> <span data-ttu-id="5f5b0-104">Si no tiene la versión 3.0 o posterior, [actualice su versión](/powershell/azureps-cmdlets-docs/) utilizando la Galería de PowerShell o el Instalador de plataforma web antes de continuar con este tema.</span><span class="sxs-lookup"><span data-stu-id="5f5b0-104">If you do not have version 3.0 or later, [update your version](/powershell/azureps-cmdlets-docs/) by using PowerShell Gallery or Web Platform Installer before you proceed with this topic.</span></span>

```powershell
Version
-------
3.5.0
```

<span data-ttu-id="5f5b0-105">Para ver las etiquetas existentes de un *grupo de recursos*, use:</span><span class="sxs-lookup"><span data-stu-id="5f5b0-105">To see the existing tags for a *resource group*, use:</span></span>

```powershell
(Get-AzureRmResourceGroup -Name examplegroup).Tags
```

<span data-ttu-id="5f5b0-106">Ese script devuelve el siguiente formato:</span><span class="sxs-lookup"><span data-stu-id="5f5b0-106">That script returns the following format:</span></span>

```powershell
Name                           Value
----                           -----
Dept                           IT
Environment                    Test
```

<span data-ttu-id="5f5b0-107">Para ver las etiquetas existentes de un *recurso que tiene un identificador de recurso especificado*, use:</span><span class="sxs-lookup"><span data-stu-id="5f5b0-107">To see the existing tags for a *resource that has a specified resource ID*, use:</span></span>

```powershell
(Get-AzureRmResource -ResourceId {resource-id}).Tags
```

<span data-ttu-id="5f5b0-108">O bien, para ver las etiquetas existentes para un *recurso que tiene un nombre y un grupo de recursos especificados*, use:</span><span class="sxs-lookup"><span data-stu-id="5f5b0-108">Or, to see the existing tags for a *resource that has a specified name and resource group*, use:</span></span>

```powershell
(Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
```

<span data-ttu-id="5f5b0-109">Para obtener *grupos de recursos que tengan una etiqueta específica*, use:</span><span class="sxs-lookup"><span data-stu-id="5f5b0-109">To get *resource groups that have a specific tag*, use:</span></span>

```powershell
(Find-AzureRmResourceGroup -Tag @{ Dept="Finance" }).Name 
```

<span data-ttu-id="5f5b0-110">Para obtener *recursos que tengan una etiqueta específica*, use:</span><span class="sxs-lookup"><span data-stu-id="5f5b0-110">To get *resources that have a specific tag*, use:</span></span>

```powershell
(Find-AzureRmResource -TagName Dept -TagValue Finance).Name
```

<span data-ttu-id="5f5b0-111">Cada vez que aplique etiquetas a un recurso o grupo de recursos, sobrescribirá las etiquetas existentes en ese recurso o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="5f5b0-111">Every time you apply tags to a resource or a resource group, you overwrite the existing tags on that resource or resource group.</span></span> <span data-ttu-id="5f5b0-112">Por lo tanto, tiene que utilizar un enfoque diferente en función de si el recurso o grupo de recursos tienen etiquetas existentes.</span><span class="sxs-lookup"><span data-stu-id="5f5b0-112">Therefore, you must use a different approach based on whether the resource or resource group has existing tags.</span></span> 

<span data-ttu-id="5f5b0-113">Para agregar etiquetas a un *grupo de recursos sin etiquetas*, use:</span><span class="sxs-lookup"><span data-stu-id="5f5b0-113">To add tags to a *resource group without existing tags*, use:</span></span>

```powershell
Set-AzureRmResourceGroup -Name examplegroup -Tag @{ Dept="IT"; Environment="Test" }
```

<span data-ttu-id="5f5b0-114">Para agregar etiquetas a un *grupo de recursos que ya tiene etiquetas*, recupere las etiquetas existentes, agregue la nueva y vuelva a aplicar todas:</span><span class="sxs-lookup"><span data-stu-id="5f5b0-114">To add tags to a *resource group that has existing tags*, retrieve the existing tags, add the new tag, and reapply the tags:</span></span>

```powershell
$tags = (Get-AzureRmResourceGroup -Name examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResourceGroup -Tag $tags -Name examplegroup
```

<span data-ttu-id="5f5b0-115">Para agregar etiquetas a un *recurso sin etiquetas*, use:</span><span class="sxs-lookup"><span data-stu-id="5f5b0-115">To add tags to a *resource without existing tags*, use:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName examplevnet -ResourceGroupName examplegroup
```

<span data-ttu-id="5f5b0-116">Para agregar etiquetas a un *recurso que ya tiene etiquetas*, use:</span><span class="sxs-lookup"><span data-stu-id="5f5b0-116">To add tags to a *resource that has existing tags*, use:</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName examplevnet -ResourceGroupName examplegroup
```

<span data-ttu-id="5f5b0-117">Para aplicar todas las etiquetas de un grupo de recursos a sus recursos y *no conservar ninguna de las etiquetas existentes en los recursos*, use el siguiente script:</span><span class="sxs-lookup"><span data-stu-id="5f5b0-117">To apply all tags from a resource group to its resources, and *not retain existing tags on the resources*, use the following script:</span></span>

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName | ForEach-Object {Set-AzureRmResource -ResourceId $_.ResourceId -Tag $g.Tags -Force } 
}
```

<span data-ttu-id="5f5b0-118">Para aplicar todas las etiquetas de un grupo de recursos a sus recursos y *conservar las etiquetas existentes en los recursos que no son duplicados*, use el siguiente script:</span><span class="sxs-lookup"><span data-stu-id="5f5b0-118">To apply all tags from a resource group to its resources, and *retain existing tags on resources that are not duplicates*, use the following script:</span></span>

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    if ($g.Tags -ne $null) {
        $resources = Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName 
        foreach ($r in $resources)
        {
            $resourcetags = (Get-AzureRmResource -ResourceId $r.ResourceId).Tags
            foreach ($key in $g.Tags.Keys)
            {
                if ($resourcetags.ContainsKey($key)) { $resourcetags.Remove($key) }
            }
            $resourcetags += $g.Tags
            Set-AzureRmResource -Tag $resourcetags -ResourceId $r.ResourceId -Force
        }
    }
}
```

<span data-ttu-id="5f5b0-119">Para quitar todas las etiquetas, pase una tabla hash vacía:</span><span class="sxs-lookup"><span data-stu-id="5f5b0-119">To remove all tags, pass an empty hash table:</span></span>

```powershell
Set-AzureRmResourceGroup -Tag @{} -Name examplegroup
```



