---
title: plantillas de toocheck aaaUse validador de plantilla para la pila de Azure | Documentos de Microsoft
description: "Compruebe las plantillas de implementación tooAzure pila"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: d9e6aee1-4cba-4df5-b5a3-6f38da9627a3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: helaw
ms.openlocfilehash: ee649f2ebf77486ca5036116dd73a45d66884704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="check-your-templates-for-azure-stack-with-template-validator"></a>Compruebe las plantillas para Azure Stack con el validador de plantilla
Puede usar Hola plantilla validación herramienta toocheck si el Administrador de recursos de Azure [plantillas](azure-stack-arm-templates.md) están listos para la pila de Azure. herramienta de validación de plantilla de Hello está disponible como parte de herramientas de la pila de Azure de Hola. Descargar herramientas de Azure pila hello mediante pasos de hello descritos en hello [descargar herramientas de GitHub](azure-stack-powershell-download.md) artículo. 

plantillas de toovalidate, utilice Hola después de módulos de PowerShell y Hola JSON archivo ubicado en **TemplateValidator** y **CloudCapabilities** carpetas: 

 - AzureRM.CloudCapabilities.psm1 crea un archivo JSON de las capacidades de nube que representa los servicios de Hola y las versiones en una nube como Azure pila.
 - AzureRM.TemplateValidator.psm1 usa capacidades de la nube plantillas de tootest de archivos JSON para la implementación en la pila de Azure.
 - AzureStackCloudCapabilities_with_AddOns_20170627.json es un archivo predeterminado de funcionalidades de la nube.  Puede crear sus propios o utilizar este tooget archivo iniciado. 

En este tema, ejecute la validación en las plantillas y, opcionalmente, genere un archivo de funcionalidades de la nube.

## <a name="validate-templates"></a>Validar plantillas
En estos pasos, valida plantillas mediante Hola módulo AzureRM.TemplateValidator PowerShell. Puede usar sus propias plantillas o validar hello [plantillas de inicio rápido de Azure pila](https://github.com/Azure/AzureStack-QuickStart-Templates).

1.  Importe el módulo de PowerShell de AzureRM.TemplateValidator.psm1 de hello:
    
    ```PowerShell
    cd "c:\AzureStack-Tools-master\TemplateValidator"
    Import-Module .\AzureRM.TemplateValidator.psm1
    ```

2.  Ejecute el validador de plantilla hello:

    ```PowerShell
    Test-AzureRMTemplate -TemplatePath <path tootemplate.json or template folder> `
    -CapabilitiesPath <path toocloudcapabilities.json> `
    -Verbose
    ```

Cualquier error o advertencia de validación de plantilla es registrados toohello consola de PowerShell y también es archivo HTML de tooan registrado en el directorio de origen Hola. Un ejemplo de salida de informe de validación de hello tiene el siguiente aspecto:

![informe de validación de ejemplo](./media/azure-stack-validate-templates/image1.png)

### <a name="parameters"></a>parameters

| Parámetro | Descripción | Obligatorio |
| ----- | -----| ----- |
| TemplatePath | Especifica toorecursively de ruta de acceso de hello buscar plantillas de administrador de recursos | Sí | 
| TemplatePattern | Especifica el nombre de Hola de toomatch de archivos de plantilla. | No |
| CapabilitiesPath | Especifica el archivo JSON capacidades de hello ruta de acceso toocloud | Sí | 
| IncludeComputeCapabilities | Incluye la evaluación de recursos de IaaS como tamaños de máquina virtual y extensiones de máquina virtual | No |
| IncludeStorageCapabilities | Incluye la evaluación de recursos de almacenamiento como los tipos SKU | No |
| Informe | Especifica el nombre del programa Hola genera informes HTML | No |
| Detallado | Registra errores y advertencias consola toohello | No|


### <a name="examples"></a>Ejemplos
En este ejemplo valida todos los hello [plantillas de inicio rápido de Azure pila](https://github.com/Azure/AzureStack-QuickStart-Templates) descargado localmente y también valida los tamaños de máquinas virtuales de Hola y extensiones con las funciones del Kit de desarrollo de pila de Azure.

```PowerShell
test-AzureRMTemplate -TemplatePath C:\AzureStack-Quickstart-Templates `
-CapabilitiesPath .\TemplateValidator\AzureStackCloudCapabilities_with_AddOns_20170627.json.json `
-TemplatePattern MyStandardTemplateName.json`
-IncludeComputeCapabilities`
-Report TemplateReport.html
```

## <a name="build-cloud-capabilities-file"></a>Genere el archivo de funcionalidades de la nube
los archivos descargados Hello incluyen un valor predeterminado *AzureStackCloudCapabilities_with_AddOns_20170627.json* archivo, que describe las versiones de servicio de hello disponibles en el Kit de desarrollo de pila de Azure con los servicios de PaaS instalados.  Si instala a proveedores de recursos adicionales, puede usar hello toobuild de módulo de AzureRM.CloudCapabilities PowerShell un archivo JSON, incluidos los nuevos servicios de Hola.  

1.  Asegúrese de que tiene conectividad tooAzure pila.  Estos pasos se pueden realizar desde el host de kit de desarrollo de Azure pila hello, o puede usar [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) tooconnect desde su estación de trabajo. 
2.  Hola de importar el módulo de AzureRM.CloudCapabilities PowerShell:

    ```PowerShell
    Import-Module .\CloudCapabilities\AzureRM.CloudCapabilities.psm1
    ``` 

3.  Utilizan versiones de hello CloudCapabilities Get cmdlet tooretrieve service y cree un archivo JSON de las capacidades de nube:

    ```PowerShell
    Get-AzureRMCloudCapabilities -Location 'local' -Verbose
    ```             


## <a name="next-steps"></a>Pasos siguientes
 - [Implementar plantillas tooAzure pila](azure-stack-arm-templates.md)
 - [Desarrollar plantillas para Azure Stack] (azure-stack-develop-templates.md)

