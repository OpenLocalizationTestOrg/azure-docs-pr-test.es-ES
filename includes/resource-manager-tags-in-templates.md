<span data-ttu-id="6d4f4-101">Para etiquetar un recurso durante la implementación, agregue el elemento `tags` al recurso que se va a implementar.</span><span class="sxs-lookup"><span data-stu-id="6d4f4-101">To tag a resource during deployment, add the `tags` element to the resource you are deploying.</span></span> <span data-ttu-id="6d4f4-102">Proporcione el nombre y el valor de la etiqueta.</span><span class="sxs-lookup"><span data-stu-id="6d4f4-102">Provide the tag name and value.</span></span>

### <a name="apply-a-literal-value-to-the-tag-name"></a><span data-ttu-id="6d4f4-103">Aplicación de un valor literal al nombre de etiqueta</span><span class="sxs-lookup"><span data-stu-id="6d4f4-103">Apply a literal value to the tag name</span></span>
<span data-ttu-id="6d4f4-104">En el ejemplo siguiente se muestra una cuenta de almacenamiento con dos etiquetas (`Dept` y `Environment`) que se establecen en valores literales:</span><span class="sxs-lookup"><span data-stu-id="6d4f4-104">The following example shows a storage account with two tags (`Dept` and `Environment`) that are set to literal values:</span></span>

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

### <a name="apply-an-object-to-the-tag-element"></a><span data-ttu-id="6d4f4-105">Aplicación de un objeto al elemento de etiqueta</span><span class="sxs-lookup"><span data-stu-id="6d4f4-105">Apply an object to the tag element</span></span>
<span data-ttu-id="6d4f4-106">Puede definir un parámetro de objeto que almacene varias etiquetas y aplicar ese objeto al elemento de etiqueta.</span><span class="sxs-lookup"><span data-stu-id="6d4f4-106">You can define an object parameter that stores several tags, and apply that object to the tag element.</span></span> <span data-ttu-id="6d4f4-107">Cada propiedad del objeto se convierte en una etiqueta independiente para el recurso.</span><span class="sxs-lookup"><span data-stu-id="6d4f4-107">Each property in the object becomes a separate tag for the resource.</span></span> <span data-ttu-id="6d4f4-108">El siguiente ejemplo tiene un parámetro denominado `tagValues` que se aplica al elemento de etiqueta.</span><span class="sxs-lookup"><span data-stu-id="6d4f4-108">The following example has a parameter named `tagValues` that is applied to the tag element.</span></span>

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

### <a name="apply-a-json-string-to-the-tag-name"></a><span data-ttu-id="6d4f4-109">Aplicación de una cadena JSON al nombre de etiqueta</span><span class="sxs-lookup"><span data-stu-id="6d4f4-109">Apply a JSON string to the tag name</span></span>

<span data-ttu-id="6d4f4-110">Para almacenar muchos valores en una única etiqueta, aplique una cadena JSON que represente los valores.</span><span class="sxs-lookup"><span data-stu-id="6d4f4-110">To store many values in a single tag, apply a JSON string that represents the values.</span></span> <span data-ttu-id="6d4f4-111">Toda la cadena JSON se almacena como una etiqueta que no puede superar los 256 caracteres.</span><span class="sxs-lookup"><span data-stu-id="6d4f4-111">The entire JSON string is stored as one tag that cannot exceed 256 characters.</span></span> <span data-ttu-id="6d4f4-112">En el ejemplo siguiente se muestra una etiqueta denominada `CostCenter` que contiene varios valores de una cadena JSON:</span><span class="sxs-lookup"><span data-stu-id="6d4f4-112">The following example has a single tag named `CostCenter` that contains several values from a JSON string:</span></span>  

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