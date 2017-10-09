<span data-ttu-id="31b4a-101">tootag un recurso durante la implementación, agregue hello `tags` recursos toohello de elemento que va a implementar.</span><span class="sxs-lookup"><span data-stu-id="31b4a-101">tootag a resource during deployment, add hello `tags` element toohello resource you are deploying.</span></span> <span data-ttu-id="31b4a-102">Proporcionar valor y nombre de etiqueta de Hola.</span><span class="sxs-lookup"><span data-stu-id="31b4a-102">Provide hello tag name and value.</span></span>

### <a name="apply-a-literal-value-toohello-tag-name"></a><span data-ttu-id="31b4a-103">Aplicar un nombre de etiqueta toohello valor literal</span><span class="sxs-lookup"><span data-stu-id="31b4a-103">Apply a literal value toohello tag name</span></span>
<span data-ttu-id="31b4a-104">Hello en el ejemplo siguiente se muestra una cuenta de almacenamiento con dos etiquetas (`Dept` y `Environment`) que se establecen los valores de tooliteral:</span><span class="sxs-lookup"><span data-stu-id="31b4a-104">hello following example shows a storage account with two tags (`Dept` and `Environment`) that are set tooliteral values:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

### <a name="apply-an-object-toohello-tag-element"></a><span data-ttu-id="31b4a-105">Aplique un elemento de etiqueta de objeto toohello</span><span class="sxs-lookup"><span data-stu-id="31b4a-105">Apply an object toohello tag element</span></span>
<span data-ttu-id="31b4a-106">Puede definir un parámetro de objeto que almacena varias etiquetas y aplicar ese elemento de etiqueta de objeto toohello.</span><span class="sxs-lookup"><span data-stu-id="31b4a-106">You can define an object parameter that stores several tags, and apply that object toohello tag element.</span></span> <span data-ttu-id="31b4a-107">Cada propiedad del objeto de Hola se convierte en una etiqueta independiente para el recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="31b4a-107">Each property in hello object becomes a separate tag for hello resource.</span></span> <span data-ttu-id="31b4a-108">el ejemplo siguiente se Hello tiene un parámetro denominado `tagValues` que es el elemento de etiqueta toohello aplicada.</span><span class="sxs-lookup"><span data-stu-id="31b4a-108">hello following example has a parameter named `tagValues` that is applied toohello tag element.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "tagValues": {
      "type": "object",
      "defaultValue": {
        "Dept": "Finance",
        "Environment": "Production"
      }
    }
  },
  "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": "[parameters('tagValues')]",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": {}
    }
  ]
}
```

### <a name="apply-a-json-string-toohello-tag-name"></a><span data-ttu-id="31b4a-109">Aplicar un nombre de etiqueta de toohello de cadena JSON</span><span class="sxs-lookup"><span data-stu-id="31b4a-109">Apply a JSON string toohello tag name</span></span>

<span data-ttu-id="31b4a-110">toostore muchos valores en una única etiqueta, aplicar una cadena JSON que representa los valores de hello.</span><span class="sxs-lookup"><span data-stu-id="31b4a-110">toostore many values in a single tag, apply a JSON string that represents hello values.</span></span> <span data-ttu-id="31b4a-111">cadena JSON completa de Hola se almacena como una etiqueta que no puede superar los 256 caracteres.</span><span class="sxs-lookup"><span data-stu-id="31b4a-111">hello entire JSON string is stored as one tag that cannot exceed 256 characters.</span></span> <span data-ttu-id="31b4a-112">en el ejemplo siguiente se Hello tiene una etiqueta denominada `CostCenter` que contiene varios valores de una cadena JSON:</span><span class="sxs-lookup"><span data-stu-id="31b4a-112">hello following example has a single tag named `CostCenter` that contains several values from a JSON string:</span></span>  

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": {
        "CostCenter": "{\"Dept\":\"Finance\",\"Environment\":\"Production\"}"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```