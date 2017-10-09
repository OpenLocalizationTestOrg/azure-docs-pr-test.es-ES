---
title: procedimientos de aaaBest para crear plantillas de administrador de recursos | Documentos de Microsoft
description: Instrucciones para simplificar las plantillas del Azure Resource Manager.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 31b10deb-0183-47ce-a5ba-6d0ff2ae8ab3
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: tomfitz
ms.openlocfilehash: ec9bbe218c4f2c6a92ca44b5e9c9c71029e22151
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-creating-azure-resource-manager-templates"></a>Procedimientos recomendados para crear plantillas de Azure Resource Manager
Estas instrucciones pueden ayudarle a crear plantillas de Azure Resource Manager toouse fácil y confiable. instrucciones de Hello son solo sugerencias. No son requisitos, excepto si así se indica. El escenario podría requerir una variación de uno de hello siguientes enfoques o ejemplos.

## <a name="resource-names"></a>Nombres de recurso
Por lo general, trabaja con tres tipos de nombres de recursos en Resource Manager:

* Nombres de recurso que deben ser únicos.
* Nombres de los recursos que no son necesarias toobe único, pero elija tooprovide un nombre que puede ayudarle a identificar un recurso basado en contexto.
* Nombres de recurso que pueden ser genéricos.

 Para obtener información sobre las restricciones de los nombres de recurso, consulte [Recommended naming conventions for Azure resources](../guidance/guidance-naming-conventions.md)(Convenciones de nomenclatura recomendadas para los recursos de Azure).

### <a name="unique-resource-names"></a>Nombres de recurso únicos
Debe dar un nombre de recurso único para cualquier tipo de recurso que tenga un punto de conexión de acceso a datos. Entre los tipos de recursos comunes que requieren un nombre único se incluyen los siguientes:

* Azure Storage<sup>1</sup> 
* Característica Web Apps de Azure App Service
* SQL Server
* Almacén de claves de Azure
* Caché en Redis de Azure
* Azure Batch
* Administrador de tráfico de Azure
* Búsqueda de Azure
* HDInsight de Azure

<sup>1</sup> Los nombres de las cuentas de almacenamiento deben estar en minúsculas, tener 24 caracteres o menos y no incluir guiones.

Si proporciona un parámetro para un nombre de recurso, debe proporcionar un nombre único al implementar recursos de Hola. Si lo desea, puede crear una variable que utiliza hello [uniqueString()](resource-group-template-functions-string.md#uniquestring) toogenerate un nombre de función. 

También podría desea tooadd un prefijo o sufijo toohello **uniqueString** resultado. Nombre único de modificación Hola permite identificar más fácilmente Hola el tipo de recurso de nombre de Hola. Por ejemplo, puede generar un nombre único para una cuenta de almacenamiento mediante el uso de hello después de variable:

```json
"variables": {
    "storageAccountName": "[concat(uniqueString(resourceGroup().id),'storage')]"
}
```

### <a name="resource-names-for-identification"></a>Nombres de recurso para la identificación
Algunos tipos de recursos puede tooname, pero no es necesario toobe único en sus nombres. Para estos tipos de recursos, puede proporcionar un nombre que identifica el contexto del recurso de Hola y el tipo de recurso de Hola. Proporcione un nombre descriptivo que le ayuda a identificar los recursos de hello en una lista de recursos. Si necesita un nombre de recurso diferente para las distintas implementaciones de toouse, puede usar un parámetro de nombre de hello:

```json
"parameters": {
    "vmName": { 
        "type": "string",
        "defaultValue": "demoLinuxVM",
        "metadata": {
            "description": "hello name of hello VM toocreate."
        }
    }
}
```

Si no es necesario toopass en un nombre durante la implementación, puede usar una variable: 

```json
"variables": {
    "vmName": "demoLinuxVM"
}
```

También puede usar un valor codificado de forma rígida:

```json
{
  "type": "Microsoft.Compute/virtualMachines",
  "name": "demoLinuxVM",
  ...
}
```

### <a name="generic-resource-names"></a>Nombres de recurso genéricos
Tipos de recursos que puede acceso principalmente a través de un recurso diferente, puede utilizar un nombre genérico que está codificado de forma rígida en la plantilla de Hola. Por ejemplo, puede establecer un nombre genérico estándar para reglas de firewall en un servidor SQL:

```json
{
    "type": "firewallrules",
    "name": "AllowAllWindowsAzureIps",
    ...
}
```

## <a name="parameters"></a>parameters
Hello siguiente información puede ser útil al trabajar con parámetros:

* Minimice el uso de los parámetros. Siempre que sea posible, use una variable o un valor literal. Solo use parámetros en estos escenarios:
   
   * Configuración que desea que las variaciones de toouse de según tooenvironment (SKU, tamaño, la capacidad).
   * Nombres de los recursos que desea toospecify para facilitar su identificación.
   * Valores que se usa con frecuencia toocomplete otras tareas (por ejemplo, un nombre de usuario de administrador).
   * Secretos (como contraseñas).
   * número de Hola o matriz de valores toouse al crear varias instancias de un tipo de recurso.
* Use una mezcla de mayúsculas y minúsculas para los nombres de parámetro.
* Proporcione una descripción de cada parámetro en los metadatos de hello:

   ```json
   "parameters": {
       "storageAccountType": {
           "type": "string",
           "metadata": {
               "description": "hello type of hello new storage account created toostore hello VM disks."
           }
       }
   }
   ```

* Defina los valores predeterminados de los parámetros (excepto en el caso de contraseñas y claves SSH):
   
   ```json
   "parameters": {
        "storageAccountType": {
            "type": "string",
            "defaultValue": "Standard_GRS",
            "metadata": {
                "description": "hello type of hello new storage account created toostore hello VM disks."
            }
        }
   }
   ```

* Use **SecureString** para todas las contraseñas y secretos: 
   
   ```json
   "parameters": {
       "secretValue": {
           "type": "securestring",
           "metadata": {
               "description": "hello value of hello secret toostore in hello vault."
           }
       }
   }
   ```

* Siempre que sea posible, no utilice una ubicación de toospecify de parámetro. En su lugar, use hello **ubicación** propiedad Hola del grupo de recursos. Mediante el uso de hello **resourceGroup () .location** expresión para todos los recursos, los recursos de plantilla de Hola se implementan en Hola la misma ubicación que el grupo de recursos de hello:
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         ...
     }
   ]
   ```
   
   Si un tipo de recurso es compatible con solo un número limitado de ubicaciones, conviene toospecify una ubicación válida directamente en la plantilla de Hola. Si tiene que utilizar un **ubicación** parámetro, compartir ese valor de parámetro tanto como sea posible con los recursos que son probable toobe Hola misma ubicación. Esto reduce el número de Hola de veces que se piden a los usuarios información sobre la ubicación tooprovide.
* Evite el uso de un parámetro o variable de versión de API de Hola para un tipo de recurso. Las propiedades y los valores de los recursos pueden variar en función del número de la versión. IntelliSense en un editor de código no puede determinar el esquema correcto de hello cuando se establece la versión de la API de hello tooa parámetro o variable. En su lugar, codificar Hola versión de API en la plantilla de Hola.

## <a name="variables"></a>variables
Hello siguiente información puede ser útil al trabajar con variables:

* Usar variables para los valores que necesite toouse más de una vez en una plantilla. Si se usa un valor una sola vez, un valor codificado de forma rígida hace su tooread sea más fácil de plantilla.
* No se puede usar hello [referencia](resource-group-template-functions-resource.md#reference) función Hola **variables** sección de plantilla de Hola. Hola **referencia** función deriva su valor de estado de tiempo de ejecución del recurso de Hola. Sin embargo, las variables se resuelven durante el saludo inicial de análisis de plantilla de Hola. Generar valores que necesitan hello **referencia** función directamente en hello **recursos** o **genera** sección de plantilla de Hola.
* Incluya variables para los nombres de recurso que deben ser únicos, como se describe en [Nombres de recurso](#resource-names).
* Puede agrupar las variables en objetos complejos. Hola de uso **variable.subentry** tooreference un valor de un objeto complejo de formato. Agrupar las variables puede ayudarlo a hacer seguimiento de variables relacionadas. También mejora la legibilidad de plantilla de Hola. Este es un ejemplo:
   
   ```json
   "variables": {
       "storage": {
           "name": "[concat(uniqueString(resourceGroup().id),'storage')]",
           "type": "Standard_LRS"
       }
   },
   "resources": [
     {
         "type": "Microsoft.Storage/storageAccounts",
         "name": "[variables('storage').name]",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "sku": {
             "name": "[variables('storage').type]"
         },
         ...
     }
   ]
   ```
   
   > [!NOTE]
   > Los objetos complejos no pueden contener una expresión que haga referencia a un valor de un objeto complejo. Defina una variable independiente para tal fin.
   > 
   > 
   
     Para ejemplos avanzados de cómo usar objetos complejos como variables, consulte [Uso compartido de estado en plantillas de Azure Resource Manager](best-practices-resource-manager-state.md).

## <a name="resources"></a>Recursos
Hello siguiente información puede ser útil cuando se trabaja con recursos:

* toohelp otros colaboradores de entender Hola propósito del recurso de hello, especifique **comentarios** para cada recurso de plantilla de hello:
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "comments": "This storage account is used toostore hello VM disks.",
         ...
     }
   ]
   ```

* Puede utilizar etiquetas tooadd metadatos tooresources. Usar metadatos tooadd información acerca de los recursos. Por ejemplo, puede agregar detalles de facturación de toorecord de metadatos para un recurso. Para obtener más información, consulte [mediante etiquetas tooorganize los recursos de Azure](resource-group-using-tags.md).
* Si utiliza un *punto de conexión público* en la plantilla (por ejemplo, un Blob de Azure almacenamiento extremo público), *realice no codifique de forma rígida* Hola espacio de nombres. Hola de uso **referencia** función toodynamically recuperar espacio de nombres de Hola. Puede usar este enfoque toodeploy Hola plantilla toodifferent espacio de nombres públicos los entornos sin cambiar el punto de conexión de hello en plantilla Hola manualmente. Establecer Hola API versión toohello misma versión que está usando para la cuenta de almacenamiento de hello en la plantilla:
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   Si se implementa la cuenta de almacenamiento de Hola Hola misma plantilla que está creando, no es necesario espacio de nombres de proveedor de toospecify Hola al hacer referencia a recursos de Hola. Ésta es la sintaxis de hello simplificado:
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(variables('storageAccountName'), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   Si tiene otros valores en la plantilla que están configurado toouse un espacio de nombres público, cambiar estos valores tooreflect Hola mismo **referencia** función. Por ejemplo, puede establecer hello **storageUri** propiedad de perfil de diagnóstico de máquina virtual de hello:
   
   ```json
   "diagnosticsProfile": {
       "bootDiagnostics": {
           "enabled": "true",
           "storageUri": "[reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob]"
       }
   }
   ```
   
   También puede hacer referencia a una cuenta de almacenamiento existente que se encuentra en un grupo de recursos distinto:

   ```json
   "osDisk": {
       "name": "osdisk", 
       "vhd": {
           "uri":"[concat(reference(resourceId(parameters('existingResourceGroup'), 'Microsoft.Storage/storageAccounts/', parameters('existingStorageAccountName')), '2016-01-01').primaryEndpoints.blob,  variables('vmStorageAccountContainerName'), '/', variables('OSDiskName'),'.vhd')]"
       }
   }
   ```

* Asignar automático público de virtual tooa de direcciones IP solo cuando una aplicación lo requiera. tooconnect tooa máquina virtual (VM) para la depuración, o para la administración o con fines administrativos, use reglas NAT de entrada, una puerta de enlace de red virtual o un jumpbox.
   
     Para obtener más información acerca de cómo conectar máquinas toovirtual, consulte:
   
   * [Ejecución de máquinas virtuales para una arquitectura de n niveles en Azure](../guidance/guidance-compute-n-tier-vm.md)
   * [Configuración de acceso a WinRM para máquinas virtuales en Azure Resource Manager](../virtual-machines/windows/winrm.md)
   * [Permitir el acceso externo tooyour VM con hello portal de Azure](../virtual-machines/windows/nsg-quickstart-portal.md)
   * [Permitir el acceso externo tooyour máquina virtual con PowerShell](../virtual-machines/windows/nsg-quickstart-powershell.md)
   * [Permitir el acceso externo tooyour VM de Linux con CLI de Azure](../virtual-machines/virtual-machines-linux-nsg-quickstart.md)
* Hola **domainNameLabel** propiedad para las direcciones IP públicas debe ser único. Hola **domainNameLabel** valor debe tener entre 3 y 63 caracteres y seguir reglas de hello especificadas por esta expresión regular: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`. Dado que hello **uniqueString** función genera una cadena que es 13 caracteres, hello **dnsPrefixString** parámetro es limitado too50 caracteres:

   ```json
   "parameters": {
       "dnsPrefixString": {
           "type": "string",
           "maxLength": 50,
           "metadata": {
               "description": "hello DNS label for hello public IP address. It must be lowercase. It should match hello following regular expression, or it will raise an error: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$"
           }
       }
   },
   "variables": {
       "dnsPrefix": "[concat(parameters('dnsPrefixString'),uniquestring(resourceGroup().id))]"
   }
   ```

* Cuando se agrega una extensión de script personalizado de tooa de contraseña, utilice hello **commandToExecute** propiedad Hola **protectedSettings** propiedad:
   
   ```json
   "properties": {
       "publisher": "Microsoft.Azure.Extensions",
       "type": "CustomScript",
       "typeHandlerVersion": "2.0",
       "autoUpgradeMinorVersion": true,
       "settings": {
           "fileUris": [
               "[concat(variables('template').assets, '/lamp-app/install_lamp.sh')]"
           ]
       },
       "protectedSettings": {
           "commandToExecute": "[concat('sh install_lamp.sh ', parameters('mySqlPassword'))]"
       }
   }
   ```
   
   > [!NOTE]
   > tooensure que son secretos cifrados cuando se pasan como parámetros tooVMs y extensiones, usar hello **protectedSettings** propiedad de las extensiones pertinentes de Hola.
   > 
   > 

## <a name="outputs"></a>Salidas
Si utiliza una plantilla toocreate las direcciones IP públicas, incluya una **genera** sección que devuelve los detalles de dirección IP de Hola y el nombre de dominio completo (FQDN) de Hola. Puede utilizar la salida valores tooeasily recuperar detalles acerca de FQDN y direcciones IP públicas después de la implementación. Al hacer referencia a recursos de hello, use versión Hola API que usa toocreate: 

```json
"outputs": {
    "fqdn": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').dnsSettings.fqdn]",
        "type": "string"
    },
    "ipaddress": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').ipAddress]",
        "type": "string"
    }
}
```

## <a name="single-template-vs-nested-templates"></a>Comparación entre plantilla única y plantillas anidadas
toodeploy la solución, puede usar una única plantilla o una plantilla principal con varias plantillas anidadas. Las plantillas anidadas son comunes en escenarios más avanzados. Uso de un proporciona plantillas anidadas Hola siguientes ventajas:

* Puede descomponer una solución en componentes específicos.
* Puede volver a usar plantillas anidadas con distintas plantillas principales.

Si elige plantillas toouse anidado, Hola siguiendo las directrices puede ayudarle a normalizar el diseño de plantilla. Estas instrucciones se basan en [patrones para diseñar plantillas de Azure Resource Manager](best-practices-resource-manager-design-templates.md). Se recomienda un diseño que tenga Hola siguientes plantillas:

* **Plantilla principal** (azuredeploy.json). Se usa para los parámetros de entrada de Hola.
* **Plantilla de recursos compartidos**. Toodeploy de uso compartido de recursos que usan todos los demás recursos (por ejemplo, virtual red y disponibilidad conjuntos). Hola de uso **dependsOn** tooensure de expresión que se implementa esta plantilla antes de otras plantillas.
* **Plantilla de recursos opcionales**. Use tooconditionally implementar recursos en función de un parámetro (por ejemplo, un jumpbox).
* **Plantilla de recursos de miembros**. Cada tipo de instancia dentro de una capa de aplicación tiene su propia configuración. Dentro de un nivel, puede definir los distintos tipos de instancia. (Por ejemplo, Hola primera instancia crea un clúster y se agregan instancias adicionales toohello de clúster existente). Cada tipo de instancia tiene su propia plantilla de implementación.
* **Scripts**. Se pueden aplicar scripts ampliamente reutilizables a cada tipo de instancia (por ejemplo, para inicializar y formatear discos adicionales). Scripts personalizados que se crean para un propósito específico personalización son diferentes, según el tipo de instancia Hola.

![Plantilla anidada](./media/resource-manager-template-best-practices/nestedTemplateDesign.png)

Para más información, consulte [Uso de plantillas vinculadas con Azure Resource Manager](resource-group-linked-templates.md).

## <a name="conditionally-link-toonested-templates"></a>Vincular condicionalmente toonested plantillas
Puede usar un parámetro tooconditionally vínculo toonested las plantillas. parámetro Hello pasa a formar parte del programa Hola URI para la plantilla de hello:

```json
"parameters": {
    "newOrExisting": {
        "type": "String",
        "allowedValues": [
            "new",
            "existing"
        ]
    }
},
"variables": {
    "templatelink": "[concat('https://raw.githubusercontent.com/Contoso/Templates/master/',parameters('newOrExisting'),'StorageAccount.json')]"
},
"resources": [
    {
        "apiVersion": "2015-01-01",
        "name": "nestedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
            "mode": "incremental",
            "templateLink": {
                "uri": "[variables('templatelink')]",
                "contentVersion": "1.0.0.0"
            },
            "parameters": {
            }
        }
    }
]
```

## <a name="template-format"></a>Formato de plantilla
Es una buena práctica toopass la plantilla a través de un validador de JSON. Un validador puede ayudarle a quitar comas, paréntesis y corchetes extraños que pueden provocar un error durante la implementación. Pruebe [JSONLint](http://jsonlint.com/) o un paquete de linter para el entorno de edición de su preferencia (Visual Studio Code, Atom, Sublime Text, Visual Studio).

También es una buena idea tooformat su JSON para mejorar la legibilidad. Puede utilizar un paquete de formateador de JSON para el editor local. En Visual Studio, documentos de hello tooformat, presione **Ctrl + K, Ctrl + D**. En Visual Studio Code, presione **Alt+Mayús+F**. Si el editor local no dar formato a documentos de hello, puede usar un [formateador en línea](https://www.bing.com/search?q=json+formatter).

## <a name="next-steps"></a>Pasos siguientes
* Para instrucciones sobre cómo diseñar la solución para las máquinas virtuales, consulte [Ejecución de una máquina virtual Windows en Azure](../guidance/guidance-compute-single-vm.md) y [Ejecución de una máquina virtual Linux en Azure](../guidance/guidance-compute-single-vm-linux.md).
* Si desea obtener instrucciones sobre cómo configurar una cuenta de almacenamiento, consulte [Lista de comprobación de rendimiento y escalabilidad de Azure Storage](../storage/common/storage-performance-checklist.md).
* toolearn acerca de cómo una empresa puede usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise: regulador prescriptiva suscripción](resource-manager-subscription-governance.md).

