---
title: "aaaCreate artefactos personalizados para la máquina virtual de laboratorios de desarrollo y pruebas | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooauthor sus propios artefactos para usar con laboratorios de desarrollo y pruebas"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 32dcdc61-ec23-4a01-b731-78c029ea5316
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: 2bd603bc1241ca6b669a3a276a677729514f0df2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-artifacts-for-your-devtest-labs-vm"></a>Creación de artefactos personalizados para la máquina virtual de DevTest Labs
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/how-to-author-custom-artifacts/player]
> 
> 

## <a name="overview"></a>Información general
**Artefactos** son toodeploy usado y configurar la aplicación después de aprovisiona una máquina virtual. Un artefacto consta de un archivo de definición de artefacto y otros archivos de script que se almacenan en un repositorio de Git. Archivos de definición de artefacto consisten en JSON y expresiones que se puede usar toospecify qué desea tooinstall en una máquina virtual. Por ejemplo, puede definir nombre Hola de un artefacto, toorun de comandos y parámetros que están disponibles cuando se ejecuta el comando Hola. Puede hacer referencia tooother archivos de script en archivo de definición de artefacto de Hola por su nombre.

## <a name="artifact-definition-file-format"></a>Formato del archivo de definición de artefacto
Hello en el ejemplo siguiente se muestra las secciones de Hola que conforman la estructura básica de Hola de un archivo de definición:

    {
      "$schema": "https://raw.githubusercontent.com/Azure/azure-devtestlab/master/schemas/2016-11-28/dtlArtifacts.json",
      "title": "",
      "description": "",
      "iconUri": "",
      "targetOsType": "",
      "parameters": {
        "<parameterName>": {
          "type": "",
          "displayName": "",
          "description": ""
        }
      },
      "runCommand": {
        "commandToExecute": ""
      }
    }

| Nombre del elemento | ¿Necesario? | Description |
| --- | --- | --- |
| $schema |No |Ubicación del archivo de esquema JSON de Hola que le ayuda a comprobar la validez de Hola Hola del archivo de definición. |
| título |Sí |Nombre del artefacto de Hola que se muestra en el laboratorio de Hola. |
| description |Sí |Descripción del artefacto de Hola que se muestra en el laboratorio de Hola. |
| iconUri |No |URI del icono de hello en laboratorio Hola. |
| targetOsType |Sí |Sistema operativo de hello VM donde está instalado el artefacto. Las opciones admitidas son Windows y Linux. |
| parameters |No |Los valores que se proporcionan cuando el comando de instalación del artefacto se ejecuta en un equipo. Esto ayuda a personalizar el artefacto. |
| runCommand |Sí |Comando de instalación de artefacto que se ejecuta en una máquina virtual. |

### <a name="artifact-parameters"></a>Parámetros de artefacto
En la sección de parámetros de Hola Hola del archivo de definición, especifique los valores que un usuario puede escribir al instalar un artefacto. Puede hacer referencia a valores de toothese de comando de instalación de artefacto de Hola.

Definir parámetros con hello siguiente estructura:

    "parameters": {
        "<parameterName>": {
          "type": "<type-of-parameter-value>",
          "displayName": "<display-name-of-parameter>",
          "description": "<description-of-parameter>"
        }
      }

| Nombre del elemento | ¿Necesario? | Description |
| --- | --- | --- |
| type |Sí |Tipo del valor de parámetro. Vea Hola lista de tipos permitido de hello siguiente: |
| DisplayName |Sí |Nombre del parámetro de Hola que sea usuario de tooa mostrado en el laboratorio de Hola. | |
| description |Sí |Descripción del parámetro de Hola que se muestra en el laboratorio de Hola. |

Hola tipos permitidos son:

* string: cualquier cadena JSON válida
* int: cualquier entero JSON válido
* bool: cualquier booleano JSON válido
* array: cualquier matriz JSON válida

## <a name="artifact-expressions-and-functions"></a>Expresiones y funciones de artefacto
Puede utilizar la expresión y artefactos de funciones tooconstruct Hola el comando de instalación.
Las expresiones se incluyen entre corchetes ([y]) y se evalúan cuando se instala el artefacto de Hola. Pueden aparecer expresiones en cualquier lugar de un valor de cadena JSON y devolver siempre otro valor JSON. Si necesita una cadena literal que se inicia con un corchete de cierre de toouse [, debe usar dos corchetes [[.
Por lo general, se usan expresiones con funciones tooconstruct un valor. Al igual que en JavaScript, las llamadas de función tienen el formato functionName(arg1,arg2,arg3).

Hello siguiente lista muestra funciones comunes:

* Parameters(ParameterName) - devuelve un valor de parámetro que se proporciona cuando se ejecuta el comando de artefacto de Hola.
* concat(arg1,arg2,arg3,…): combina varios valores de cadena. Esta función puede tomar cualquier número de argumentos.

Hola siguiente ejemplo se muestra cómo tooconstruct toouse un valor de expresión y funciones:

    runCommand": {
         "commandToExecute": "[concat('powershell.exe -ExecutionPolicy bypass \"& ./startChocolatey.ps1'
    , ' -RawPackagesList ', parameters('packages')
    , ' -Username ', parameters('installUsername')
    , ' -Password ', parameters('installPassword'))]"
    }

## <a name="create-a-custom-artifact"></a>Creación de un artefacto personalizado
Cree su artefacto personalizado siguiendo estos pasos:

1. Instalación de un editor de JSON - necesita un toowork de editor de JSON con archivos de definición de artefacto. Se recomienda usar el [código de Visual Studio](https://code.visualstudio.com/), que está disponible para Windows, Linux y OS X.
2. Get un artifactfile.json de ejemplo - desprotección artefactos Hola creado por equipo de laboratorios de desarrollo y pruebas de Azure en nuestro [repositorio de GitHub](https://github.com/Azure/azure-devtestlab), donde hemos creado una biblioteca enriquecida de artefactos que le ayudarán a crearán sus propios artefactos. Descargar un archivo de definición de artefacto y realice cambios tooit toocreate sus propios artefactos.
3. Asegúrese de usar de IntelliSense: aproveche IntelliSense toosee elementos válidos que pueden ser tooconstruct usa un archivo de definición de artefacto. También puede ver Hola distintas opciones para los valores de un elemento. Por ejemplo, la presentación del IntelliSense Hola dos opciones de Windows o Linux al editar hello **targetOsType** elemento.
4. Artefacto de Hola de tienda en un [repositorio de git](devtest-lab-add-artifact-repo.md).
   
   1. Cree un directorio independiente para cada artefacto donde el nombre del directorio de hello es Hola igual como nombre del artefacto Hola.
   2. Almacenar archivo de definición de artefacto de hello (artifactfile.json) en el directorio de hello creado.
   3. Comando de instalación de las secuencias de comandos de Hola de almacén que se hace referencia de artefacto de Hola.
      
      Este es un ejemplo del aspecto que tendrá una carpeta de artefacto:
      
      ![Ejemplo de repositorio de Git de artefacto](./media/devtest-lab-artifact-author/git-repo.png)
5. Agregar el laboratorio de toohello de repositorio de artefactos de hello: consulte el artículo toohello, [agregar un repositorio Git de artefactos y plantillas de](devtest-lab-add-artifact-repo.md).

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-articles"></a>Artículos relacionados
* [¿Cómo toodiagnose errores de artefactos en los laboratorios de desarrollo y pruebas](devtest-lab-troubleshoot-artifact-failure.md)
* [Unirse a un dominio de Active Directory mediante una plantilla de administrador de recursos en los laboratorios de desarrollo y pruebas de Azure tooexisting VM](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[agregar un laboratorio de tooa repositorio de Git artefacto](devtest-lab-add-artifact-repo.md).

