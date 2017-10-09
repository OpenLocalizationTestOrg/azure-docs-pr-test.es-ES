---
title: Grupos de recursos de Azure que contienen las extensiones de VM aaaExporting | Documentos de Microsoft
description: "Exportar plantillas de Resource Manager que incluyen extensiones de máquina virtual."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7f4e2ca6-f1c7-4f59-a2cc-8f63132de279
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 12/05/2016
ms.author: nepeters
ms.openlocfilehash: cdbc2030988a19fe68429e8733dc60536c264abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="exporting-resource-groups-that-contain-vm-extensions"></a>Exportación de grupos de recursos que contienen extensiones de VM

Los grupos de recursos de Azure se pueden exportar a una nueva plantilla de Resource Manager que, después, se puede volver a implementar. Hello proceso de exportación interpreta los recursos existentes y crea una plantilla de administrador de recursos que cuando se implementa da como resultado un grupo de recursos similares. Cuando se usa la opción de exportación de grupo de recursos de hello en un grupo de recursos que contiene las extensiones de máquina Virtual, varios elementos necesidad toobe había considerado como compatibilidad de extensión y protegido configuración.

Este documento se explica cómo funciona la Hola proceso de exportación del grupo de recursos con respecto a las extensiones de máquina virtual, incluida una lista de extensiones admitidas y detalles sobre el control de los datos protegen.

## <a name="supported-virtual-machine-extensions"></a>Extensiones de máquina virtual admitidas

Hay muchas extensiones de máquina virtual disponibles. No todas las extensiones se pueden exportar a una plantilla de administrador de recursos mediante la característica de "Script de automatización" Hola. Si no se admite una extensión de máquina virtual, debe toobe manualmente vuelve a colocar en plantilla exportada Hola.

Hello siguientes extensiones se pueden exportar con la característica de secuencia de comandos de automatización de Hola.

| Extensión ||||
|---|---|---|---|
| Acronis Backup | Datadog Windows Agent | OS Patching For Linux | VM Snapshot Linux
| Acronis Backup Linux | Extensión de Docker | Puppet Agent |
| Bg Info | Extensión DSC | Site 24x7 Apm Insight |
| BMC CTM Agent Linux | Dynatrace Linux | Site 24x7 Linux Server |
| BMC CTM Agent Windows | Dynatrace Windows | Site 24x7 Windows Server |
| Chef Client | HPE Security Application Defender | Trend Micro DSA |
| Script personalizado | IaaS Antimalware | Trend Micro DSA Linux |
| Extensión Custom Script | IaaS Diagnostics | VM Access For Linux |
| Script personalizado para Linux | Linux Chef Client | VM Access For Linux |
| Datadog Linux Agent | Linux Diagnostic | VM Snapshot |

## <a name="export-hello-resource-group"></a>Exportar Hola grupo de recursos

tooexport un grupo de recursos en una plantilla reutilizable, Hola completa pasos:

1. Inicie sesión en toohello portal de Azure
2. En el menú del concentrador de hello, haga clic en grupos de recursos
3. Seleccione el grupo de recursos de destino de hello en lista de Hola
4. En la hoja de grupo de recursos de hello, haga clic en Script de automatización

![Exportación de plantilla](./media/extensions-export-templates/template-export.png)

Hello secuencia de comandos de Azure Resource Manager automatizaciones genera una plantilla de administrador de recursos, un archivo de parámetros y varias secuencias de comandos de implementación de ejemplo como PowerShell y la CLI de Azure. En este momento, se puede descargar plantilla exportada hello mediante el botón de descarga de hello, agrega como una biblioteca de plantillas de toohello plantilla nuevo o volver a implementar mediante Hola botón implementar.

## <a name="configure-protected-settings"></a>Definición de la configuración protegida

Muchas extensiones de máquina virtual de Azure incluyen una configuración protegida, que cifra los datos confidenciales, como credenciales y cadenas de configuración. Configuración protegida no se exporta con script de automatización de Hola. Si toobe volver a insertar en hello es necesario la configuración protegida, es necesario exporta con plantilla.

### <a name="step-1---remove-template-parameter"></a>Paso 1: Quitar parámetro de plantilla

Cuando Hola que se exporta el grupo de recursos, un parámetro de plantilla solo se crea tooprovide un toohello valor exporta configuración protegida. Este parámetro se puede quitar. parámetro de hello tooremove, buscar a través de la lista de parámetros de Hola y eliminar parámetro hello que comprueba el ejemplo JSON toothis similar.

```json
"extensions_extensionname_protectedSettings": {
    "defaultValue": null,
    "type": "SecureObject"
}
```

### <a name="step-2---get-protected-settings-properties"></a>Paso 2: Obtener propiedades de configuración protegida

Dado que cada configuración protegido tiene un conjunto de propiedades necesarias, una lista de estas propiedades necesario toobe recopilada. Cada parámetro de configuración protegida de hello puede encontrarse en hello [esquema del Administrador de recursos de Azure en GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json). Este esquema incluye solo los conjuntos de parámetros de Hola para las extensiones de hello indicadas en la sección de información general de Hola de este documento. 

Desde dentro de repositorio de esquema de hello, busque extensión Hola deseado, en este ejemplo `IaaSDiagnostics`. Una vez Hola extensiones `protectedSettings` objeto se ha localizado, tome nota de cada parámetro. En el ejemplo de Hola de hello `IaasDiagnostic` Hola de extensión, requieren parámetros son `storageAccountName`, `storageAccountKey`, y `storageAccountEndPoint`.

```json
"protectedSettings": {
    "type": "object",
    "properties": {
        "storageAccountName": {
            "type": "string"
        },
        "storageAccountKey": {
            "type": "string"
        },
        "storageAccountEndPoint": {
            "type": "string"
        }
    },
    "required": [
        "storageAccountName",
        "storageAccountKey",
        "storageAccountEndPoint"
    ]
}
```

### <a name="step-3---re-create-hello-protected-configuration"></a>Paso 3: volver a crear la configuración de hello protegido

En Hola plantilla exportada, busque `protectedSettings` y reemplazar Hola exportado protegido al establecer un objeto con uno nuevo que incluye parámetros de extensión de hello necesario y un valor para cada uno de ellos.

En el ejemplo de Hola de hello `IaasDiagnostic` extensión, Hola nueva protegido establecer la configuración tendrá el aspecto siguiente ejemplo de Hola:

```json
"protectedSettings": {
    "storageAccountName": "[parameters('storageAccountName')]",
    "storageAccountKey": "[parameters('storageAccountKey')]",
    "storageAccountEndPoint": "https://core.windows.net"
}
```

recursos de extensión final Hello tiene un aspecto similar toohello siguiente JSON de ejemplo:

```json
{
    "name": "Microsoft.Insights.VMDiagnosticsSettings",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "[variables('apiVersion')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "tags": {
        "displayName": "AzureDiagnostics"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), variables('vmName'), variables('wadcfgxend')))]",
            "storageAccount": "[parameters('existingdiagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
            "storageAccountName": "[parameters('storageAccountName')]",
            "storageAccountKey": "[parameters('storageAccountKey')]",
            "storageAccountEndPoint": "https://core.windows.net"
        }
    }
}
```

Si utiliza valores de propiedad de tooprovide de parámetros de plantilla, estos necesitan toobe creado. Al crear parámetros de plantilla para los valores de configuración protegida, que seguro Hola de toouse `SecureString` tipo de parámetro para que se protegen los valores confidenciales. Para más información sobre el uso de parámetros, consulte [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md) (Creación de plantillas de Azure Resource Manager).

En el ejemplo de Hola de hello `IaasDiagnostic` extensión, Hola parámetros siguientes se crea en la sección de parámetros de Hola de plantilla de administrador de recursos de Hola.

```json
"storageAccountName": {
    "defaultValue": null,
    "type": "SecureString"
},
"storageAccountKey": {
    "defaultValue": null,
    "type": "SecureString"
}
```

En este momento, plantilla de hello puede implementarse mediante cualquier método de implementación de plantilla.
