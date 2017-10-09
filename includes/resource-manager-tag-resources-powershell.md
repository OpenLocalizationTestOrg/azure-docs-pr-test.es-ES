Versión 3.0 del módulo de hello AzureRm.Resources incluye cambios significativos en forma de trabajar con etiquetas. Antes de continuar, compruebe su versión:

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

Si los resultados muestran una versión 3.0 o posterior, ejemplos de hello en este tema trabajar con su entorno. Si no tiene la versión 3.0 o posterior, [actualice su versión](/powershell/azureps-cmdlets-docs/) utilizando la Galería de PowerShell o el Instalador de plataforma web antes de continuar con este tema.

```powershell
Version
-------
3.5.0
```

toosee Hola las etiquetas existentes para un *grupo de recursos*, use:

```powershell
(Get-AzureRmResourceGroup -Name examplegroup).Tags
```

Este script devuelve Hola siguiendo el formato:

```powershell
Name                           Value
----                           -----
Dept                           IT
Environment                    Test
```

toosee Hola las etiquetas existentes para un *recurso con un identificador de recurso especificado*, use:

```powershell
(Get-AzureRmResource -ResourceId {resource-id}).Tags
```

O bien, toosee Hola las etiquetas existentes para un *recurso con un grupo de recursos y el nombre especificado*, use:

```powershell
(Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
```

tooget *grupos de recursos que tienen una etiqueta específica*, use:

```powershell
(Find-AzureRmResourceGroup -Tag @{ Dept="Finance" }).Name 
```

tooget *recursos que tienen una etiqueta específica*, use:

```powershell
(Find-AzureRmResource -TagName Dept -TagValue Finance).Name
```

Cada vez que aplica etiquetas tooa recurso o un grupo de recursos, sobrescribir las etiquetas existentes hello en ese recurso o grupo de recursos. Por lo tanto, debe utilizar un enfoque diferente en función de si el recurso de Hola o grupo de recursos tiene las etiquetas existentes. 

etiquetas de tooadd tooa *grupo de recursos sin las etiquetas existentes*, use:

```powershell
Set-AzureRmResourceGroup -Name examplegroup -Tag @{ Dept="IT"; Environment="Test" }
```

etiquetas de tooadd tooa *grupo de recursos que tiene las etiquetas existentes*, recuperar las etiquetas existentes hello, agregar nueva etiqueta de Hola y volver a aplicar etiquetas de hello:

```powershell
$tags = (Get-AzureRmResourceGroup -Name examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResourceGroup -Tag $tags -Name examplegroup
```

etiquetas de tooadd tooa *recurso sin las etiquetas existentes*, use:

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName examplevnet -ResourceGroupName examplegroup
```

etiquetas de tooadd tooa *recurso con las etiquetas existentes*, use:

```powershell
$tags = (Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName examplevnet -ResourceGroupName examplegroup
```

tooapply todas las etiquetas de recursos de tooits del grupo de recursos, y *no conservar las etiquetas existentes en los recursos de hello*, usar hello siguiente secuencia de comandos:

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName | ForEach-Object {Set-AzureRmResource -ResourceId $_.ResourceId -Tag $g.Tags -Force } 
}
```

tooapply todas las etiquetas de recursos de tooits del grupo de recursos, y *conservar las etiquetas existentes en los recursos que no sean duplicados*, usar hello siguiente secuencia de comandos:

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

tooremove todas las etiquetas, pase una tabla hash vacío:

```powershell
Set-AzureRmResourceGroup -Tag @{} -Name examplegroup
```



