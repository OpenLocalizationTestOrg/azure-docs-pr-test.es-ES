usar tooadd un grupo de recursos de etiqueta tooa, **del conjunto de grupos de azure**. Si el grupo de recursos de hello no tiene las etiquetas existentes, pasar etiqueta Hola.

```azurecli
azure group set -n tag-demo-group -t Dept=Finance
```

Las etiquetas se actualizan en conjunto. Si desea tooadd un grupo de recursos de tooa de etiqueta con las etiquetas existentes, pase todas las etiquetas de Hola. 

```azurecli
azure group set -n tag-demo-group -t Dept=Finance;Environment=Production;Project=Upgrade
```

Los recursos de un grupo de recursos no heredan las etiquetas. tooadd un recurso de tooa etiqueta, utilice **conjunto de recursos de azure**. Pasar Hola número de versión de API para el tipo de recurso de Hola que va a agregar la etiqueta de Hola a. Si necesita tooretrieve Hola API versión, usar hello siguiente comando con el proveedor de recursos de hello para el tipo de hello que esté configurando:

```azurecli
azure provider show -n Microsoft.Storage --json
```

En los resultados de hello, buscar el tipo de recurso de Hola que desee.

```azurecli
"resourceTypes": [
{
  "resourceType": "storageAccounts",
  ...
  "apiVersions": [
    "2016-01-01",
    "2015-06-15",
    "2015-05-01-preview"
  ]
}
...
```

Ahora, proporcione esa versión de API, el nombre del grupo de recursos, el nombre del recurso, el tipo de recurso y el valor de etiqueta como parámetros.

```azurecli
azure resource set -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -t Dept=Finance -o 2016-01-01
```

Las etiquetas existen directamente en los recursos y grupos de recursos. toosee las etiquetas existentes hello, obtener un grupo de recursos y sus recursos con **mostrar grupo azure**.

```azurecli
azure group show -n tag-demo-group --json
```

Que devuelve los metadatos sobre el grupo de recursos de hello, incluido cualquier tooit etiquetas aplicadas.

```azurecli
{
  "id": "/subscriptions/4705409c-9372-42f0-914c-64a504530837/resourceGroups/tag-demo-group",
  "name": "tag-demo-group",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "location": "southcentralus",
  "tags": {
    "Dept": "Finance",
    "Environment": "Production",
    "Project": "Upgrade"
  },
  ...
}
```

Ver etiquetas de Hola para un recurso determinado mediante **mostrar recursos de azure**.

```azurecli
azure resource show -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -o 2016-01-01 --json
```

tooretrieve todos los recursos de hello con un valor de etiqueta, utilice:

```azurecli
azure resource list -t Dept=Finance --json
```

tooretrieve todos los grupos de recursos de hello con un valor de etiqueta, utilice:

```azurecli
azure group list -t Dept=Finance
```

Puede ver las etiquetas existentes hello en su suscripción con hello siguiente comando:

```azurecli
azure tag list
```
