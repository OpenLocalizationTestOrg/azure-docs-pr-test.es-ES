---
title: "aaaRun scripts personalizados en máquinas virtuales de Linux en Azure | Documentos de Microsoft"
description: "Automatizar tareas de configuración de VM de Linux mediante el uso de hello extensión de Script personalizado"
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cf17ab2b-8d7e-4078-b6df-955c6d5071c2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: f2c273a5fbd4cd1695aea48fa4bd08e691511e5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-custom-script-extension-with-linux-virtual-machines"></a>Uso de hello extensión de Script personalizado de Azure con las máquinas virtuales Linux
Extensión de Script personalizado de Hello descarga y ejecuta scripts en máquinas virtuales de Azure. Esta extensión es útil para la configuración posterior a la implementación, la instalación de software o cualquier otra tarea de configuración o administración. Las secuencias de comandos se pueden descargar desde el almacenamiento de Azure u otra ubicación de internet accesible o proporciona extensión toohello tiempo de ejecución. Hola extensión de Script personalizado se integra con plantillas de Azure Resource Manager y también se puede ejecutar mediante Hola CLI de Azure, PowerShell, portal de Azure u Hola API de REST de máquina Virtual de Azure.

Este documento se explica cómo toouse Hola extensión de Script personalizado de Hola CLI de Azure y una plantilla de Azure Resource Manager y también detalles de la solución de problemas de pasos en los sistemas Linux.

## <a name="extension-configuration"></a>Configuración de la extensión
configuración de extensión de Script personalizado de Hello especifica elementos tales como ubicación del script y hello toobe de comando ejecutar. Esta configuración se puede almacenar en archivos de configuración especificados en la línea de comandos de hello, o en una plantilla de Azure Resource Manager. Los datos confidenciales se pueden almacenar en una configuración protegida, que se cifra y descifra solo dentro de la máquina virtual de Hola. configuración protegida Hello es útil al comando de ejecución de hello incluye secretos, como una contraseña.

### <a name="public-configuration"></a>Configuración pública
Esquema:

**Nota**: Los nombres de propiedad distinguen entre mayúsculas y minúsculas. Utilice nombres de hello tal como se muestra a continuación tooavoid problemas de implementación.

* **commandToExecute**: (requerido, string) Hola tooexecute de secuencia de comandos de punto de entrada
* **fileUris**: (opcional, matriz de cadena) hello las direcciones URL para toobe archivos descargan.
* **marca de tiempo** (entero opcional) use esta tootrigger solo un vuelva a ejecutar script de Hola de campo, cambie el valor de este campo.

```json
{
  "fileUris": ["<url>"],
  "commandToExecute": "<command-to-execute>"
}
```

### <a name="protected-configuration"></a>Configuración protegida
Esquema:

**Nota**: Los nombres de propiedad distinguen entre mayúsculas y minúsculas. Utilice nombres de hello tal como se muestra a continuación tooavoid problemas de implementación.

* **commandToExecute**: (opcional, string) Hola tooexecute de secuencia de comandos de punto de entrada. Use este campo si el comando contiene secretos tales como contraseñas.
* **storageAccountName**: (opcional, string) nombre Hola de cuenta de almacenamiento. Si especifica credenciales de almacenamiento, todos los valores de fileUri deben ser direcciones URL de blobs de Azure.
* **storageAccountKey**: (opcional, string) clave de acceso de Hola de cuenta de almacenamiento.

```json
{
  "commandToExecute": "<command-to-execute>",
  "storageAccountName": "<storage-account-name>",
  "storageAccountKey": "<storage-account-key>"
}
```

## <a name="azure-cli"></a>CLI de Azure
Cuando se usa toorun Hola extensión de Script personalizado de hello CLI de Azure, cree un archivo de configuración o archivos que contengan en el uri de archivo mínimo hello y comandos de ejecución de script de Hola.

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

Si lo desea puede especificarse configuración hello en comando hello como una cadena con formato JSON. Esto permite hello toobe de configuración especificado durante la ejecución y sin un archivo de configuración diferente.

```azurecli
az vm extension set '
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],"commandToExecute": "./test.sh"}'
```

### <a name="azure-cli-examples"></a>Ejemplos de la CLI de Azure

**Ejemplo 1** : configuración pública con archivo de script.

```json
{
  "fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],
  "commandToExecute": "./test.sh"
}
```

Comando de la CLI de Azure:

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

**Ejemplo 2** : configuración pública sin archivo de script.

```json
{
  "commandToExecute": "apt-get -y update && apt-get install -y apache2"
}
```

Comando de la CLI de Azure:

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

**Ejemplo 3** : un archivo de configuración pública es identificador URI de archivo de script de Hola toospecify usado y un archivo de configuración protegida es toospecify usado Hola comando toobe ejecuta.

Archivo de configuración pública:

```json
{
  "fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"]
}
```

Archivo de configuración protegida:  

```json
{
  "commandToExecute": "./hello.sh <password>"
}
```

Comando de la CLI de Azure:

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json --protected-settings ./protected-config.json
```

## <a name="resource-manager-template"></a>Plantilla de Resource Manager
Hola extensión de Script personalizado de Azure se puede ejecutar en el momento de la implementación de máquina Virtual mediante una plantilla de administrador de recursos. toodo por lo tanto, agregue la plantilla de implementación de toohello JSON con el formato correcto.

### <a name="resource-manager-examples"></a>Ejemplos de Resource Manager
**Ejemplo 1** : configuración pública.

```json
{
    "name": "scriptextensiondemo",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-15",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', parameters('scriptextensiondemoName'))]"
    ],
    "tags": {
        "displayName": "scriptextensiondemo"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Extensions",
        "type": "CustomScript",
        "typeHandlerVersion": "2.0",
        "autoUpgradeMinorVersion": true,
      "settings": {
        "fileUris": [
          "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
        ],
        "commandToExecute": "sh hello.sh"
      }
    }
}
```

**Ejemplo 2** : comando de ejecución en la configuración protegida.

```json
{
  "name": "config-app",
  "type": "extensions",
  "location": "[resourceGroup().location]",
  "apiVersion": "2015-06-15",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
      ]              
    },
    "protectedSettings": {
      "commandToExecute": "sh hello.sh <password>"
    }
  }
}
```

Ver tienda de música de hello .net Core demostración para obtener un ejemplo completo - [demostración de la tienda de música](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).

## <a name="troubleshooting"></a>Solución de problemas
Cuando se ejecuta la extensión de Script personalizado de Hola, script de Hola se crea o se ha descargado a una toohello similar del directorio siguiente ejemplo. También se guarda la salida del comando Hello en este directorio en `stdout` y `stderr` archivo.

```bash
/var/lib/waagent/custom-script/download/0/
```

Hola extensión de Script de Azure genera un registro, que puede encontrarse aquí.

```bash
/var/log/azure/custom-script/handler.log
```

También se puede recuperar el estado de la ejecución de Hola de hello extensión de Script personalizado con hello CLI de Azure.

```azurecli
az vm extension list -g myResourceGroup --vm-name myVM
```

salida de Hello es similar a Hola siguiente texto:

```azurecli
info:    Executing command vm extension get
+ Looking up hello VM "scripttst001"
data:    Publisher                   Name                                      Version  State
data:    --------------------------  ----------------------------------------  -------  ---------
data:    Microsoft.Azure.Extensions  CustomScript                              2.0      Succeeded
data:    Microsoft.OSTCExtensions    Microsoft.Insights.VMDiagnosticsSettings  2.3      Succeeded
info:    vm extension get command OK
```

## <a name="next-steps"></a>Pasos siguientes
Para más información sobre otras extensiones de script de máquina virtual, consulte [Introducción a la extensión de script de Azure para Linux](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

