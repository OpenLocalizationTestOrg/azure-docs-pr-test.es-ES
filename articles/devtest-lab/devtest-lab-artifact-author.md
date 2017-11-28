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
# <a name="create-custom-artifacts-for-your-devtest-labs-vm"></a><span data-ttu-id="89971-103">Creación de artefactos personalizados para la máquina virtual de DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="89971-103">Create custom artifacts for your DevTest Labs VM</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/how-to-author-custom-artifacts/player]
> 
> 

## <a name="overview"></a><span data-ttu-id="89971-104">Información general</span><span class="sxs-lookup"><span data-stu-id="89971-104">Overview</span></span>
<span data-ttu-id="89971-105">**artefactos** se utilizan para implementar y configurar la aplicación después de aprovisionar una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="89971-105">**Artifacts** are used to deploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="89971-106">Un artefacto consta de un archivo de definición de artefacto y otros archivos de script que se almacenan en un repositorio de Git.</span><span class="sxs-lookup"><span data-stu-id="89971-106">An artifact consists of an artifact definition file and other script files that are stored in a folder in a git repository.</span></span> <span data-ttu-id="89971-107">Los archivos de definición de artefacto constan de JSON y expresiones que puede utilizar para especificar lo que desea instalar en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="89971-107">Artifact definition files consist of JSON and expressions that you can use to specify what you want to install on a VM.</span></span> <span data-ttu-id="89971-108">Por ejemplo, puede definir el nombre del artefacto, el comando que se va a ejecutar y los parámetros que están disponibles cuando se ejecuta el comando.</span><span class="sxs-lookup"><span data-stu-id="89971-108">For example, you can define the name of an artifact, command to run, and parameters that are made available when the command is run.</span></span> <span data-ttu-id="89971-109">Puede hacer referencia a otros archivos de script en el archivo de definición de artefacto por nombre.</span><span class="sxs-lookup"><span data-stu-id="89971-109">You can refer to other script files within the artifact definition file by name.</span></span>

## <a name="artifact-definition-file-format"></a><span data-ttu-id="89971-110">Formato del archivo de definición de artefacto</span><span class="sxs-lookup"><span data-stu-id="89971-110">Artifact definition file format</span></span>
<span data-ttu-id="89971-111">En el ejemplo siguiente se muestran las secciones que componen la estructura básica de un archivo de definición:</span><span class="sxs-lookup"><span data-stu-id="89971-111">The following example shows the sections that make up the basic structure of a definition file:</span></span>

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

| <span data-ttu-id="89971-112">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="89971-112">Element name</span></span> | <span data-ttu-id="89971-113">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="89971-113">Required?</span></span> | <span data-ttu-id="89971-114">Description</span><span class="sxs-lookup"><span data-stu-id="89971-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="89971-115">$schema</span><span class="sxs-lookup"><span data-stu-id="89971-115">$schema</span></span> |<span data-ttu-id="89971-116">No</span><span class="sxs-lookup"><span data-stu-id="89971-116">No</span></span> |<span data-ttu-id="89971-117">Ubicación del archivo de esquema JSON que ayuda a probar la validez del archivo de definición.</span><span class="sxs-lookup"><span data-stu-id="89971-117">Location of the JSON schema file that helps in testing the validity of the definition file.</span></span> |
| <span data-ttu-id="89971-118">título</span><span class="sxs-lookup"><span data-stu-id="89971-118">title</span></span> |<span data-ttu-id="89971-119">Sí</span><span class="sxs-lookup"><span data-stu-id="89971-119">Yes</span></span> |<span data-ttu-id="89971-120">Nombre del artefacto que se muestra en el laboratorio.</span><span class="sxs-lookup"><span data-stu-id="89971-120">Name of the artifact displayed in the lab.</span></span> |
| <span data-ttu-id="89971-121">Description</span><span class="sxs-lookup"><span data-stu-id="89971-121">description</span></span> |<span data-ttu-id="89971-122">Sí</span><span class="sxs-lookup"><span data-stu-id="89971-122">Yes</span></span> |<span data-ttu-id="89971-123">Descripción del artefacto que se muestra en el laboratorio.</span><span class="sxs-lookup"><span data-stu-id="89971-123">Description of the artifact displayed in the lab.</span></span> |
| <span data-ttu-id="89971-124">iconUri</span><span class="sxs-lookup"><span data-stu-id="89971-124">iconUri</span></span> |<span data-ttu-id="89971-125">No</span><span class="sxs-lookup"><span data-stu-id="89971-125">No</span></span> |<span data-ttu-id="89971-126">Identificador URI del icono que se muestra en el laboratorio.</span><span class="sxs-lookup"><span data-stu-id="89971-126">Uri of the icon displayed in the lab.</span></span> |
| <span data-ttu-id="89971-127">targetOsType</span><span class="sxs-lookup"><span data-stu-id="89971-127">targetOsType</span></span> |<span data-ttu-id="89971-128">Sí</span><span class="sxs-lookup"><span data-stu-id="89971-128">Yes</span></span> |<span data-ttu-id="89971-129">Sistema operativo de la máquina virtual donde se instala el artefacto.</span><span class="sxs-lookup"><span data-stu-id="89971-129">Operating system of the VM where artifact is installed.</span></span> <span data-ttu-id="89971-130">Las opciones admitidas son Windows y Linux.</span><span class="sxs-lookup"><span data-stu-id="89971-130">Supported options are: Windows and Linux.</span></span> |
| <span data-ttu-id="89971-131">parameters</span><span class="sxs-lookup"><span data-stu-id="89971-131">parameters</span></span> |<span data-ttu-id="89971-132">No</span><span class="sxs-lookup"><span data-stu-id="89971-132">No</span></span> |<span data-ttu-id="89971-133">Los valores que se proporcionan cuando el comando de instalación del artefacto se ejecuta en un equipo.</span><span class="sxs-lookup"><span data-stu-id="89971-133">Values that are provided when artifact install command is run on a machine.</span></span> <span data-ttu-id="89971-134">Esto ayuda a personalizar el artefacto.</span><span class="sxs-lookup"><span data-stu-id="89971-134">This helps in customizing your artifact.</span></span> |
| <span data-ttu-id="89971-135">runCommand</span><span class="sxs-lookup"><span data-stu-id="89971-135">runCommand</span></span> |<span data-ttu-id="89971-136">Sí</span><span class="sxs-lookup"><span data-stu-id="89971-136">Yes</span></span> |<span data-ttu-id="89971-137">Comando de instalación de artefacto que se ejecuta en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="89971-137">Artifact install command that is executed on a VM.</span></span> |

### <a name="artifact-parameters"></a><span data-ttu-id="89971-138">Parámetros de artefacto</span><span class="sxs-lookup"><span data-stu-id="89971-138">Artifact parameters</span></span>
<span data-ttu-id="89971-139">En la sección de parámetros del archivo de definición, especifique los valores que un usuario puede indicar al instalar un artefacto.</span><span class="sxs-lookup"><span data-stu-id="89971-139">In the parameters section of the definition file, you specify which values a user can input when installing an artifact.</span></span> <span data-ttu-id="89971-140">Puede hacer referencia a estos valores en el comando de instalación del artefacto.</span><span class="sxs-lookup"><span data-stu-id="89971-140">You can refer to these values in the artifact install command.</span></span>

<span data-ttu-id="89971-141">Defina recursos con la estructura siguiente:</span><span class="sxs-lookup"><span data-stu-id="89971-141">You define parameters with the following structure:</span></span>

    "parameters": {
        "<parameterName>": {
          "type": "<type-of-parameter-value>",
          "displayName": "<display-name-of-parameter>",
          "description": "<description-of-parameter>"
        }
      }

| <span data-ttu-id="89971-142">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="89971-142">Element name</span></span> | <span data-ttu-id="89971-143">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="89971-143">Required?</span></span> | <span data-ttu-id="89971-144">Description</span><span class="sxs-lookup"><span data-stu-id="89971-144">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="89971-145">type</span><span class="sxs-lookup"><span data-stu-id="89971-145">type</span></span> |<span data-ttu-id="89971-146">Sí</span><span class="sxs-lookup"><span data-stu-id="89971-146">Yes</span></span> |<span data-ttu-id="89971-147">Tipo del valor de parámetro.</span><span class="sxs-lookup"><span data-stu-id="89971-147">Type of parameter value.</span></span> <span data-ttu-id="89971-148">Consulte la lista siguiente de los tipos permitidos:</span><span class="sxs-lookup"><span data-stu-id="89971-148">See the following list for the allowed types:</span></span> |
| <span data-ttu-id="89971-149">DisplayName</span><span class="sxs-lookup"><span data-stu-id="89971-149">displayName</span></span> |<span data-ttu-id="89971-150">Sí</span><span class="sxs-lookup"><span data-stu-id="89971-150">Yes</span></span> |<span data-ttu-id="89971-151">Nombre del parámetro que se muestra a un usuario en el laboratorio.</span><span class="sxs-lookup"><span data-stu-id="89971-151">Name of the parameter that is displayed to a user in the lab.</span></span> | |
| <span data-ttu-id="89971-152">Description</span><span class="sxs-lookup"><span data-stu-id="89971-152">description</span></span> |<span data-ttu-id="89971-153">Sí</span><span class="sxs-lookup"><span data-stu-id="89971-153">Yes</span></span> |<span data-ttu-id="89971-154">Descripción del parámetro que se muestra en el laboratorio.</span><span class="sxs-lookup"><span data-stu-id="89971-154">Description of the parameter that is displayed in the lab.</span></span> |

<span data-ttu-id="89971-155">Los tipos permitidos son:</span><span class="sxs-lookup"><span data-stu-id="89971-155">The allowed types are:</span></span>

* <span data-ttu-id="89971-156">string: cualquier cadena JSON válida</span><span class="sxs-lookup"><span data-stu-id="89971-156">string – any valid JSON string</span></span>
* <span data-ttu-id="89971-157">int: cualquier entero JSON válido</span><span class="sxs-lookup"><span data-stu-id="89971-157">int – any valid JSON integer</span></span>
* <span data-ttu-id="89971-158">bool: cualquier booleano JSON válido</span><span class="sxs-lookup"><span data-stu-id="89971-158">bool – any valid JSON Boolean</span></span>
* <span data-ttu-id="89971-159">array: cualquier matriz JSON válida</span><span class="sxs-lookup"><span data-stu-id="89971-159">array – any valid JSON array</span></span>

## <a name="artifact-expressions-and-functions"></a><span data-ttu-id="89971-160">Expresiones y funciones de artefacto</span><span class="sxs-lookup"><span data-stu-id="89971-160">Artifact expressions and functions</span></span>
<span data-ttu-id="89971-161">Puede utilizar la expresión y las funciones para construir el comando de instalación del artefacto.</span><span class="sxs-lookup"><span data-stu-id="89971-161">You can use expression and functions to construct the artifact install command.</span></span>
<span data-ttu-id="89971-162">Las expresiones se incluyen entre corchetes ([ y ]) y se evalúan cuando se instala el artefacto.</span><span class="sxs-lookup"><span data-stu-id="89971-162">Expressions are enclosed with brackets ([ and ]), and are evaluated when the artifact is installed.</span></span> <span data-ttu-id="89971-163">Pueden aparecer expresiones en cualquier lugar de un valor de cadena JSON y devolver siempre otro valor JSON.</span><span class="sxs-lookup"><span data-stu-id="89971-163">Expressions can appear anywhere in a JSON string value and always return another JSON value.</span></span> <span data-ttu-id="89971-164">Si necesita usar una cadena literal que comienza por un corchete [, debe usar dos corchetes [[.</span><span class="sxs-lookup"><span data-stu-id="89971-164">If you need to use a literal string that starts with a bracket [, you must use two brackets [[.</span></span>
<span data-ttu-id="89971-165">Normalmente, se utilizan expresiones con funciones para construir un valor.</span><span class="sxs-lookup"><span data-stu-id="89971-165">Typically, you use expressions with functions to construct a value.</span></span> <span data-ttu-id="89971-166">Al igual que en JavaScript, las llamadas de función tienen el formato functionName(arg1,arg2,arg3).</span><span class="sxs-lookup"><span data-stu-id="89971-166">Just like in JavaScript, function calls are formatted as functionName(arg1,arg2,arg3).</span></span>

<span data-ttu-id="89971-167">En la lista siguiente se muestran las funciones comunes:</span><span class="sxs-lookup"><span data-stu-id="89971-167">The following list shows common functions:</span></span>

* <span data-ttu-id="89971-168">Parameters(ParameterName): devuelve un valor de parámetro que se proporciona cuando se ejecuta el comando de artefacto.</span><span class="sxs-lookup"><span data-stu-id="89971-168">parameters(parameterName) - Returns a parameter value that is provided when the artifact command is run.</span></span>
* <span data-ttu-id="89971-169">concat(arg1,arg2,arg3,…): combina varios valores de cadena.</span><span class="sxs-lookup"><span data-stu-id="89971-169">concat(arg1,arg2,arg3, …..) -     Combines multiple string values.</span></span> <span data-ttu-id="89971-170">Esta función puede tomar cualquier número de argumentos.</span><span class="sxs-lookup"><span data-stu-id="89971-170">This function can take any number of arguments.</span></span>

<span data-ttu-id="89971-171">En el ejemplo siguiente se muestra cómo utilizar expresiones y funciones para construir un valor:</span><span class="sxs-lookup"><span data-stu-id="89971-171">The following example shows how to use expression and functions to construct a value:</span></span>

    runCommand": {
         "commandToExecute": "[concat('powershell.exe -ExecutionPolicy bypass \"& ./startChocolatey.ps1'
    , ' -RawPackagesList ', parameters('packages')
    , ' -Username ', parameters('installUsername')
    , ' -Password ', parameters('installPassword'))]"
    }

## <a name="create-a-custom-artifact"></a><span data-ttu-id="89971-172">Creación de un artefacto personalizado</span><span class="sxs-lookup"><span data-stu-id="89971-172">Create a custom artifact</span></span>
<span data-ttu-id="89971-173">Cree su artefacto personalizado siguiendo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="89971-173">Create your custom artifact by following these steps:</span></span>

1. <span data-ttu-id="89971-174">Instale un editor de JSON: necesita un editor de JSON para trabajar con los archivos de definición del artefacto.</span><span class="sxs-lookup"><span data-stu-id="89971-174">Install a JSON editor - You need a JSON editor to work with artifact definition files.</span></span> <span data-ttu-id="89971-175">Se recomienda usar el [código de Visual Studio](https://code.visualstudio.com/), que está disponible para Windows, Linux y OS X.</span><span class="sxs-lookup"><span data-stu-id="89971-175">We recommend using [Visual Studio Code](https://code.visualstudio.com/), which is available for Windows, Linux and OS X.</span></span>
2. <span data-ttu-id="89971-176">Obtenga un archivo artifactfile.json de ejemplo: consulte los artefactos creados por el equipo de Azure DevTest Labs en nuestro [repositorio de GitHub](https://github.com/Azure/azure-devtestlab), donde hemos creado una completa biblioteca de artefactos que le ayudará a crear sus propios artefactos.</span><span class="sxs-lookup"><span data-stu-id="89971-176">Get a sample artifactfile.json - Check out the artifacts created by Azure DevTest Labs team at our [GitHub repository](https://github.com/Azure/azure-devtestlab), where we have created a rich library of artifacts that help you create your own artifacts.</span></span> <span data-ttu-id="89971-177">Descargue un archivo de definición de artefacto y haga cambios sobre él para crear sus propios artefactos.</span><span class="sxs-lookup"><span data-stu-id="89971-177">Download an artifact definition file and make changes to it to create your own artifacts.</span></span>
3. <span data-ttu-id="89971-178">Haga uso de IntelliSense: aproveche IntelliSense para ver elementos válidos que se pueden utilizar para construir un archivo de definición de artefacto.</span><span class="sxs-lookup"><span data-stu-id="89971-178">Make use of IntelliSense - Leverage IntelliSense to see valid elements that can be used to construct an artifact definition file.</span></span> <span data-ttu-id="89971-179">También puede ver las distintas opciones para los valores de un elemento.</span><span class="sxs-lookup"><span data-stu-id="89971-179">You can also see the different options for values of an element.</span></span> <span data-ttu-id="89971-180">Por ejemplo, IntelliSense le muestra las dos opciones de Windows o Linux al editar el elemento **targetOsType** .</span><span class="sxs-lookup"><span data-stu-id="89971-180">For example, IntelliSense show you the two choices of Windows or Linux when editing the **targetOsType** element.</span></span>
4. <span data-ttu-id="89971-181">Almacenamiento del artefacto en un [repositorio de Git](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="89971-181">Store the artifact in a [git repository](devtest-lab-add-artifact-repo.md).</span></span>
   
   1. <span data-ttu-id="89971-182">Cree un directorio independiente para cada artefacto donde el nombre del directorio sea el mismo que el nombre del artefacto.</span><span class="sxs-lookup"><span data-stu-id="89971-182">Create a separate directory for each artifact where the directory name is the same as the artifact name.</span></span>
   2. <span data-ttu-id="89971-183">Almacene el archivo de definición de artefacto (artifactfile.json) en el directorio que ha creado.</span><span class="sxs-lookup"><span data-stu-id="89971-183">Store the artifact definition file (artifactfile.json) in the directory you created.</span></span>
   3. <span data-ttu-id="89971-184">Almacene los scripts a los que hace referencia el comando de instalación del artefacto.</span><span class="sxs-lookup"><span data-stu-id="89971-184">Store the scripts that are referenced from the artifact install command.</span></span>
      
      <span data-ttu-id="89971-185">Este es un ejemplo del aspecto que tendrá una carpeta de artefacto:</span><span class="sxs-lookup"><span data-stu-id="89971-185">Here is an example of how an artifact folder might look:</span></span>
      
      ![Ejemplo de repositorio de Git de artefacto](./media/devtest-lab-artifact-author/git-repo.png)
5. <span data-ttu-id="89971-187">Agregue el repositorio de artefactos al laboratorio: consulte el artículo sobre cómo [agregar un repositorio Git para artefactos y plantillas](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="89971-187">Add the artifacts repository to the lab - Refer to the article, [Add a Git repository for artifacts and templates](devtest-lab-add-artifact-repo.md).</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-articles"></a><span data-ttu-id="89971-188">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="89971-188">Related articles</span></span>
* <span data-ttu-id="89971-189">[How to diagnose artifact failures in DevTest Labs](devtest-lab-troubleshoot-artifact-failure.md) (Diagnóstico de errores de artefactos en DevTest Labs)</span><span class="sxs-lookup"><span data-stu-id="89971-189">[How to diagnose artifact failures in DevTest Labs](devtest-lab-troubleshoot-artifact-failure.md)</span></span>
* <span data-ttu-id="89971-190">[Join a VM to existing AD Domain using a resource manager template in Azure DevTest Labs](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs) (Unión de una máquina virtual al dominio de AD existente mediante la plantilla de Resource Manager en Azure DevTest Labs)</span><span class="sxs-lookup"><span data-stu-id="89971-190">[Join a VM to existing AD Domain using a resource manager template in Azure DevTest Labs](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)</span></span>

## <a name="next-steps"></a><span data-ttu-id="89971-191">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="89971-191">Next steps</span></span>
* <span data-ttu-id="89971-192">Aprenda cómo [agregar un repositorio de artefactos Git a un laboratorio](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="89971-192">Learn how to [add a Git artifact repository to a lab](devtest-lab-add-artifact-repo.md).</span></span>

