<span data-ttu-id="a6153-101">Versión 3.0 del módulo de hello AzureRm.Resources incluye cambios significativos en forma de trabajar con etiquetas.</span><span class="sxs-lookup"><span data-stu-id="a6153-101">Version 3.0 of hello AzureRm.Resources module included significant changes in how you work with tags.</span></span> <span data-ttu-id="a6153-102">Antes de continuar, compruebe su versión:</span><span class="sxs-lookup"><span data-stu-id="a6153-102">Before you proceed, check your version:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="a6153-103">Si los resultados muestran una versión 3.0 o posterior, ejemplos de hello en este tema trabajar con su entorno.</span><span class="sxs-lookup"><span data-stu-id="a6153-103">If your results show version 3.0 or later, hello examples in this topic work with your environment.</span></span> <span data-ttu-id="a6153-104">Si no tiene la versión 3.0 o posterior, [actualice su versión](/powershell/azureps-cmdlets-docs/) utilizando la Galería de PowerShell o el Instalador de plataforma web antes de continuar con este tema.</span><span class="sxs-lookup"><span data-stu-id="a6153-104">If you do not have version 3.0 or later, [update your version](/powershell/azureps-cmdlets-docs/) by using PowerShell Gallery or Web Platform Installer before you proceed with this topic.</span></span>

```powershell
Version
-------
3.5.0
```

<span data-ttu-id="a6153-105">toosee Hola las etiquetas existentes para un *grupo de recursos*, use:</span><span class="sxs-lookup"><span data-stu-id="a6153-105">toosee hello existing tags for a *resource group*, use:</span></span>

```powershell
(Get-AzureRmResourceGroup -Name examplegroup).Tags
```

<span data-ttu-id="a6153-106">Este script devuelve Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="a6153-106">That script returns hello following format:</span></span>

```powershell
Name                           Value
----                           -----
Dept                           IT
Environment                    Test
```

<span data-ttu-id="a6153-107">toosee Hola las etiquetas existentes para un *recurso con un identificador de recurso especificado*, use:</span><span class="sxs-lookup"><span data-stu-id="a6153-107">toosee hello existing tags for a *resource that has a specified resource ID*, use:</span></span>

```powershell
(Get-AzureRmResource -ResourceId {resource-id}).Tags
```

<span data-ttu-id="a6153-108">O bien, toosee Hola las etiquetas existentes para un *recurso con un grupo de recursos y el nombre especificado*, use:</span><span class="sxs-lookup"><span data-stu-id="a6153-108">Or, toosee hello existing tags for a *resource that has a specified name and resource group*, use:</span></span>

```powershell
(Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
```

<span data-ttu-id="a6153-109">tooget *grupos de recursos que tienen una etiqueta específica*, use:</span><span class="sxs-lookup"><span data-stu-id="a6153-109">tooget *resource groups that have a specific tag*, use:</span></span>

```powershell
(Find-AzureRmResourceGroup -Tag @{ Dept="Finance" }).Name 
```

<span data-ttu-id="a6153-110">tooget *recursos que tienen una etiqueta específica*, use:</span><span class="sxs-lookup"><span data-stu-id="a6153-110">tooget *resources that have a specific tag*, use:</span></span>

```powershell
(Find-AzureRmResource -TagName Dept -TagValue Finance).Name
```

<span data-ttu-id="a6153-111">Cada vez que aplica etiquetas tooa recurso o un grupo de recursos, sobrescribir las etiquetas existentes hello en ese recurso o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a6153-111">Every time you apply tags tooa resource or a resource group, you overwrite hello existing tags on that resource or resource group.</span></span> <span data-ttu-id="a6153-112">Por lo tanto, debe utilizar un enfoque diferente en función de si el recurso de Hola o grupo de recursos tiene las etiquetas existentes.</span><span class="sxs-lookup"><span data-stu-id="a6153-112">Therefore, you must use a different approach based on whether hello resource or resource group has existing tags.</span></span> 

<span data-ttu-id="a6153-113">etiquetas de tooadd tooa *grupo de recursos sin las etiquetas existentes*, use:</span><span class="sxs-lookup"><span data-stu-id="a6153-113">tooadd tags tooa *resource group without existing tags*, use:</span></span>

```powershell
Set-AzureRmResourceGroup -Name examplegroup -Tag @{ Dept="IT"; Environment="Test" }
```

<span data-ttu-id="a6153-114">etiquetas de tooadd tooa *grupo de recursos que tiene las etiquetas existentes*, recuperar las etiquetas existentes hello, agregar nueva etiqueta de Hola y volver a aplicar etiquetas de hello:</span><span class="sxs-lookup"><span data-stu-id="a6153-114">tooadd tags tooa *resource group that has existing tags*, retrieve hello existing tags, add hello new tag, and reapply hello tags:</span></span>

```powershell
$tags = (Get-AzureRmResourceGroup -Name examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResourceGroup -Tag $tags -Name examplegroup
```

<span data-ttu-id="a6153-115">etiquetas de tooadd tooa *recurso sin las etiquetas existentes*, use:</span><span class="sxs-lookup"><span data-stu-id="a6153-115">tooadd tags tooa *resource without existing tags*, use:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName examplevnet -ResourceGroupName examplegroup
```

<span data-ttu-id="a6153-116">etiquetas de tooadd tooa *recurso con las etiquetas existentes*, use:</span><span class="sxs-lookup"><span data-stu-id="a6153-116">tooadd tags tooa *resource that has existing tags*, use:</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName examplevnet -ResourceGroupName examplegroup
```

<span data-ttu-id="a6153-117">tooapply todas las etiquetas de recursos de tooits del grupo de recursos, y *no conservar las etiquetas existentes en los recursos de hello*, usar hello siguiente secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="a6153-117">tooapply all tags from a resource group tooits resources, and *not retain existing tags on hello resources*, use hello following script:</span></span>

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName | ForEach-Object {Set-AzureRmResource -ResourceId $_.ResourceId -Tag $g.Tags -Force } 
}
```

<span data-ttu-id="a6153-118">tooapply todas las etiquetas de recursos de tooits del grupo de recursos, y *conservar las etiquetas existentes en los recursos que no sean duplicados*, usar hello siguiente secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="a6153-118">tooapply all tags from a resource group tooits resources, and *retain existing tags on resources that are not duplicates*, use hello following script:</span></span>

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

<span data-ttu-id="a6153-119">tooremove todas las etiquetas, pase una tabla hash vacío:</span><span class="sxs-lookup"><span data-stu-id="a6153-119">tooremove all tags, pass an empty hash table:</span></span>

```powershell
Set-AzureRmResourceGroup -Tag @{} -Name examplegroup
```



