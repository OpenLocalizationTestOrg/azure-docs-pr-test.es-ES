tootag un recurso durante la implementación, agregue hello `tags` recursos toohello de elemento que va a implementar. Proporcionar valor y nombre de etiqueta de Hola.

### <a name="apply-a-literal-value-toohello-tag-name"></a>Aplicar un nombre de etiqueta toohello valor literal
Hello en el ejemplo siguiente se muestra una cuenta de almacenamiento con dos etiquetas (`Dept` y `Environment`) que se establecen los valores de tooliteral:

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

### <a name="apply-an-object-toohello-tag-element"></a>Aplique un elemento de etiqueta de objeto toohello
Puede definir un parámetro de objeto que almacena varias etiquetas y aplicar ese elemento de etiqueta de objeto toohello. Cada propiedad del objeto de Hola se convierte en una etiqueta independiente para el recurso de Hola. el ejemplo siguiente se Hello tiene un parámetro denominado `tagValues` que es el elemento de etiqueta toohello aplicada.

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

### <a name="apply-a-json-string-toohello-tag-name"></a>Aplicar un nombre de etiqueta de toohello de cadena JSON

toostore muchos valores en una única etiqueta, aplicar una cadena JSON que representa los valores de hello. cadena JSON completa de Hola se almacena como una etiqueta que no puede superar los 256 caracteres. en el ejemplo siguiente se Hello tiene una etiqueta denominada `CostCenter` que contiene varios valores de una cadena JSON:  

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