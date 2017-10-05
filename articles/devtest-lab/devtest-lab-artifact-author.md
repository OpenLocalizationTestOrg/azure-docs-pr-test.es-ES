---
title: "Creación de artefactos personalizados para la máquina virtual de DevTest Labs | Microsoft Docs"
description: Aprenda a crear sus propios artefactos para usarlos con laboratorios de desarrollo y pruebas
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
ms.openlocfilehash: 2412033daa1d97860dd9f380178622b1ddc590c0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-custom-artifacts-for-your-devtest-labs-vm"></a>Creación de artefactos personalizados para la máquina virtual de DevTest Labs
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/how-to-author-custom-artifacts/player]
> 
> 

## <a name="overview"></a>Información general
**artefactos** se utilizan para implementar y configurar la aplicación después de aprovisionar una máquina virtual. Un artefacto consta de un archivo de definición de artefacto y otros archivos de script que se almacenan en un repositorio de Git. Los archivos de definición de artefacto constan de JSON y expresiones que puede utilizar para especificar lo que desea instalar en una máquina virtual. Por ejemplo, puede definir el nombre del artefacto, el comando que se va a ejecutar y los parámetros que están disponibles cuando se ejecuta el comando. Puede hacer referencia a otros archivos de script en el archivo de definición de artefacto por nombre.

## <a name="artifact-definition-file-format"></a>Formato del archivo de definición de artefacto
En el ejemplo siguiente se muestran las secciones que componen la estructura básica de un archivo de definición:

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
| $schema |No |Ubicación del archivo de esquema JSON que ayuda a probar la validez del archivo de definición. |
| título |Sí |Nombre del artefacto que se muestra en el laboratorio. |
| Description |Sí |Descripción del artefacto que se muestra en el laboratorio. |
| iconUri |No |Identificador URI del icono que se muestra en el laboratorio. |
| targetOsType |Sí |Sistema operativo de la máquina virtual donde se instala el artefacto. Las opciones admitidas son Windows y Linux. |
| parameters |No |Los valores que se proporcionan cuando el comando de instalación del artefacto se ejecuta en un equipo. Esto ayuda a personalizar el artefacto. |
| runCommand |Sí |Comando de instalación de artefacto que se ejecuta en una máquina virtual. |

### <a name="artifact-parameters"></a>Parámetros de artefacto
En la sección de parámetros del archivo de definición, especifique los valores que un usuario puede indicar al instalar un artefacto. Puede hacer referencia a estos valores en el comando de instalación del artefacto.

Defina recursos con la estructura siguiente:

    "parameters": {
        "<parameterName>": {
          "type": "<type-of-parameter-value>",
          "displayName": "<display-name-of-parameter>",
          "description": "<description-of-parameter>"
        }
      }

| Nombre del elemento | ¿Necesario? | Description |
| --- | --- | --- |
| type |Sí |Tipo del valor de parámetro. Consulte la lista siguiente de los tipos permitidos: |
| DisplayName |Sí |Nombre del parámetro que se muestra a un usuario en el laboratorio. | |
| Description |Sí |Descripción del parámetro que se muestra en el laboratorio. |

Los tipos permitidos son:

* string: cualquier cadena JSON válida
* int: cualquier entero JSON válido
* bool: cualquier booleano JSON válido
* array: cualquier matriz JSON válida

## <a name="artifact-expressions-and-functions"></a>Expresiones y funciones de artefacto
Puede utilizar la expresión y las funciones para construir el comando de instalación del artefacto.
Las expresiones se incluyen entre corchetes ([ y ]) y se evalúan cuando se instala el artefacto. Pueden aparecer expresiones en cualquier lugar de un valor de cadena JSON y devolver siempre otro valor JSON. Si necesita usar una cadena literal que comienza por un corchete [, debe usar dos corchetes [[.
Normalmente, se utilizan expresiones con funciones para construir un valor. Al igual que en JavaScript, las llamadas de función tienen el formato functionName(arg1,arg2,arg3).

En la lista siguiente se muestran las funciones comunes:

* Parameters(ParameterName): devuelve un valor de parámetro que se proporciona cuando se ejecuta el comando de artefacto.
* concat(arg1,arg2,arg3,…): combina varios valores de cadena. Esta función puede tomar cualquier número de argumentos.

En el ejemplo siguiente se muestra cómo utilizar expresiones y funciones para construir un valor:

    runCommand": {
         "commandToExecute": "[concat('powershell.exe -ExecutionPolicy bypass \"& ./startChocolatey.ps1'
    , ' -RawPackagesList ', parameters('packages')
    , ' -Username ', parameters('installUsername')
    , ' -Password ', parameters('installPassword'))]"
    }

## <a name="create-a-custom-artifact"></a>Creación de un artefacto personalizado
Cree su artefacto personalizado siguiendo estos pasos:

1. Instale un editor de JSON: necesita un editor de JSON para trabajar con los archivos de definición del artefacto. Se recomienda usar el [código de Visual Studio](https://code.visualstudio.com/), que está disponible para Windows, Linux y OS X.
2. Obtenga un archivo artifactfile.json de ejemplo: consulte los artefactos creados por el equipo de Azure DevTest Labs en nuestro [repositorio de GitHub](https://github.com/Azure/azure-devtestlab), donde hemos creado una completa biblioteca de artefactos que le ayudará a crear sus propios artefactos. Descargue un archivo de definición de artefacto y haga cambios sobre él para crear sus propios artefactos.
3. Haga uso de IntelliSense: aproveche IntelliSense para ver elementos válidos que se pueden utilizar para construir un archivo de definición de artefacto. También puede ver las distintas opciones para los valores de un elemento. Por ejemplo, IntelliSense le muestra las dos opciones de Windows o Linux al editar el elemento **targetOsType** .
4. Almacenamiento del artefacto en un [repositorio de Git](devtest-lab-add-artifact-repo.md).
   
   1. Cree un directorio independiente para cada artefacto donde el nombre del directorio sea el mismo que el nombre del artefacto.
   2. Almacene el archivo de definición de artefacto (artifactfile.json) en el directorio que ha creado.
   3. Almacene los scripts a los que hace referencia el comando de instalación del artefacto.
      
      Este es un ejemplo del aspecto que tendrá una carpeta de artefacto:
      
      ![Ejemplo de repositorio de Git de artefacto](./media/devtest-lab-artifact-author/git-repo.png)
5. Agregue el repositorio de artefactos al laboratorio: consulte el artículo sobre cómo [agregar un repositorio Git para artefactos y plantillas](devtest-lab-add-artifact-repo.md).

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-articles"></a>Artículos relacionados
* [How to diagnose artifact failures in DevTest Labs](devtest-lab-troubleshoot-artifact-failure.md) (Diagnóstico de errores de artefactos en DevTest Labs)
* [Join a VM to existing AD Domain using a resource manager template in Azure DevTest Labs](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs) (Unión de una máquina virtual al dominio de AD existente mediante la plantilla de Resource Manager en Azure DevTest Labs)

## <a name="next-steps"></a>Pasos siguientes
* Aprenda cómo [agregar un repositorio de artefactos Git a un laboratorio](devtest-lab-add-artifact-repo.md).

