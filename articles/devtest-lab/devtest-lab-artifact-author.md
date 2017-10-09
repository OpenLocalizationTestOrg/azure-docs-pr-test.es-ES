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
# <a name="create-custom-artifacts-for-your-devtest-labs-vm"></a><span data-ttu-id="610b4-103">Creación de artefactos personalizados para la máquina virtual de DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="610b4-103">Create custom artifacts for your DevTest Labs VM</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/how-to-author-custom-artifacts/player]
> 
> 

## <a name="overview"></a><span data-ttu-id="610b4-104">Información general</span><span class="sxs-lookup"><span data-stu-id="610b4-104">Overview</span></span>
<span data-ttu-id="610b4-105">**Artefactos** son toodeploy usado y configurar la aplicación después de aprovisiona una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="610b4-105">**Artifacts** are used toodeploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="610b4-106">Un artefacto consta de un archivo de definición de artefacto y otros archivos de script que se almacenan en un repositorio de Git.</span><span class="sxs-lookup"><span data-stu-id="610b4-106">An artifact consists of an artifact definition file and other script files that are stored in a folder in a git repository.</span></span> <span data-ttu-id="610b4-107">Archivos de definición de artefacto consisten en JSON y expresiones que se puede usar toospecify qué desea tooinstall en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="610b4-107">Artifact definition files consist of JSON and expressions that you can use toospecify what you want tooinstall on a VM.</span></span> <span data-ttu-id="610b4-108">Por ejemplo, puede definir nombre Hola de un artefacto, toorun de comandos y parámetros que están disponibles cuando se ejecuta el comando Hola.</span><span class="sxs-lookup"><span data-stu-id="610b4-108">For example, you can define hello name of an artifact, command toorun, and parameters that are made available when hello command is run.</span></span> <span data-ttu-id="610b4-109">Puede hacer referencia tooother archivos de script en archivo de definición de artefacto de Hola por su nombre.</span><span class="sxs-lookup"><span data-stu-id="610b4-109">You can refer tooother script files within hello artifact definition file by name.</span></span>

## <a name="artifact-definition-file-format"></a><span data-ttu-id="610b4-110">Formato del archivo de definición de artefacto</span><span class="sxs-lookup"><span data-stu-id="610b4-110">Artifact definition file format</span></span>
<span data-ttu-id="610b4-111">Hello en el ejemplo siguiente se muestra las secciones de Hola que conforman la estructura básica de Hola de un archivo de definición:</span><span class="sxs-lookup"><span data-stu-id="610b4-111">hello following example shows hello sections that make up hello basic structure of a definition file:</span></span>

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

| <span data-ttu-id="610b4-112">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="610b4-112">Element name</span></span> | <span data-ttu-id="610b4-113">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="610b4-113">Required?</span></span> | <span data-ttu-id="610b4-114">Description</span><span class="sxs-lookup"><span data-stu-id="610b4-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="610b4-115">$schema</span><span class="sxs-lookup"><span data-stu-id="610b4-115">$schema</span></span> |<span data-ttu-id="610b4-116">No</span><span class="sxs-lookup"><span data-stu-id="610b4-116">No</span></span> |<span data-ttu-id="610b4-117">Ubicación del archivo de esquema JSON de Hola que le ayuda a comprobar la validez de Hola Hola del archivo de definición.</span><span class="sxs-lookup"><span data-stu-id="610b4-117">Location of hello JSON schema file that helps in testing hello validity of hello definition file.</span></span> |
| <span data-ttu-id="610b4-118">título</span><span class="sxs-lookup"><span data-stu-id="610b4-118">title</span></span> |<span data-ttu-id="610b4-119">Sí</span><span class="sxs-lookup"><span data-stu-id="610b4-119">Yes</span></span> |<span data-ttu-id="610b4-120">Nombre del artefacto de Hola que se muestra en el laboratorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="610b4-120">Name of hello artifact displayed in hello lab.</span></span> |
| <span data-ttu-id="610b4-121">description</span><span class="sxs-lookup"><span data-stu-id="610b4-121">description</span></span> |<span data-ttu-id="610b4-122">Sí</span><span class="sxs-lookup"><span data-stu-id="610b4-122">Yes</span></span> |<span data-ttu-id="610b4-123">Descripción del artefacto de Hola que se muestra en el laboratorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="610b4-123">Description of hello artifact displayed in hello lab.</span></span> |
| <span data-ttu-id="610b4-124">iconUri</span><span class="sxs-lookup"><span data-stu-id="610b4-124">iconUri</span></span> |<span data-ttu-id="610b4-125">No</span><span class="sxs-lookup"><span data-stu-id="610b4-125">No</span></span> |<span data-ttu-id="610b4-126">URI del icono de hello en laboratorio Hola.</span><span class="sxs-lookup"><span data-stu-id="610b4-126">Uri of hello icon displayed in hello lab.</span></span> |
| <span data-ttu-id="610b4-127">targetOsType</span><span class="sxs-lookup"><span data-stu-id="610b4-127">targetOsType</span></span> |<span data-ttu-id="610b4-128">Sí</span><span class="sxs-lookup"><span data-stu-id="610b4-128">Yes</span></span> |<span data-ttu-id="610b4-129">Sistema operativo de hello VM donde está instalado el artefacto.</span><span class="sxs-lookup"><span data-stu-id="610b4-129">Operating system of hello VM where artifact is installed.</span></span> <span data-ttu-id="610b4-130">Las opciones admitidas son Windows y Linux.</span><span class="sxs-lookup"><span data-stu-id="610b4-130">Supported options are: Windows and Linux.</span></span> |
| <span data-ttu-id="610b4-131">parameters</span><span class="sxs-lookup"><span data-stu-id="610b4-131">parameters</span></span> |<span data-ttu-id="610b4-132">No</span><span class="sxs-lookup"><span data-stu-id="610b4-132">No</span></span> |<span data-ttu-id="610b4-133">Los valores que se proporcionan cuando el comando de instalación del artefacto se ejecuta en un equipo.</span><span class="sxs-lookup"><span data-stu-id="610b4-133">Values that are provided when artifact install command is run on a machine.</span></span> <span data-ttu-id="610b4-134">Esto ayuda a personalizar el artefacto.</span><span class="sxs-lookup"><span data-stu-id="610b4-134">This helps in customizing your artifact.</span></span> |
| <span data-ttu-id="610b4-135">runCommand</span><span class="sxs-lookup"><span data-stu-id="610b4-135">runCommand</span></span> |<span data-ttu-id="610b4-136">Sí</span><span class="sxs-lookup"><span data-stu-id="610b4-136">Yes</span></span> |<span data-ttu-id="610b4-137">Comando de instalación de artefacto que se ejecuta en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="610b4-137">Artifact install command that is executed on a VM.</span></span> |

### <a name="artifact-parameters"></a><span data-ttu-id="610b4-138">Parámetros de artefacto</span><span class="sxs-lookup"><span data-stu-id="610b4-138">Artifact parameters</span></span>
<span data-ttu-id="610b4-139">En la sección de parámetros de Hola Hola del archivo de definición, especifique los valores que un usuario puede escribir al instalar un artefacto.</span><span class="sxs-lookup"><span data-stu-id="610b4-139">In hello parameters section of hello definition file, you specify which values a user can input when installing an artifact.</span></span> <span data-ttu-id="610b4-140">Puede hacer referencia a valores de toothese de comando de instalación de artefacto de Hola.</span><span class="sxs-lookup"><span data-stu-id="610b4-140">You can refer toothese values in hello artifact install command.</span></span>

<span data-ttu-id="610b4-141">Definir parámetros con hello siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="610b4-141">You define parameters with hello following structure:</span></span>

    "parameters": {
        "<parameterName>": {
          "type": "<type-of-parameter-value>",
          "displayName": "<display-name-of-parameter>",
          "description": "<description-of-parameter>"
        }
      }

| <span data-ttu-id="610b4-142">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="610b4-142">Element name</span></span> | <span data-ttu-id="610b4-143">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="610b4-143">Required?</span></span> | <span data-ttu-id="610b4-144">Description</span><span class="sxs-lookup"><span data-stu-id="610b4-144">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="610b4-145">type</span><span class="sxs-lookup"><span data-stu-id="610b4-145">type</span></span> |<span data-ttu-id="610b4-146">Sí</span><span class="sxs-lookup"><span data-stu-id="610b4-146">Yes</span></span> |<span data-ttu-id="610b4-147">Tipo del valor de parámetro.</span><span class="sxs-lookup"><span data-stu-id="610b4-147">Type of parameter value.</span></span> <span data-ttu-id="610b4-148">Vea Hola lista de tipos permitido de hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="610b4-148">See hello following list for hello allowed types:</span></span> |
| <span data-ttu-id="610b4-149">DisplayName</span><span class="sxs-lookup"><span data-stu-id="610b4-149">displayName</span></span> |<span data-ttu-id="610b4-150">Sí</span><span class="sxs-lookup"><span data-stu-id="610b4-150">Yes</span></span> |<span data-ttu-id="610b4-151">Nombre del parámetro de Hola que sea usuario de tooa mostrado en el laboratorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="610b4-151">Name of hello parameter that is displayed tooa user in hello lab.</span></span> | |
| <span data-ttu-id="610b4-152">description</span><span class="sxs-lookup"><span data-stu-id="610b4-152">description</span></span> |<span data-ttu-id="610b4-153">Sí</span><span class="sxs-lookup"><span data-stu-id="610b4-153">Yes</span></span> |<span data-ttu-id="610b4-154">Descripción del parámetro de Hola que se muestra en el laboratorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="610b4-154">Description of hello parameter that is displayed in hello lab.</span></span> |

<span data-ttu-id="610b4-155">Hola tipos permitidos son:</span><span class="sxs-lookup"><span data-stu-id="610b4-155">hello allowed types are:</span></span>

* <span data-ttu-id="610b4-156">string: cualquier cadena JSON válida</span><span class="sxs-lookup"><span data-stu-id="610b4-156">string – any valid JSON string</span></span>
* <span data-ttu-id="610b4-157">int: cualquier entero JSON válido</span><span class="sxs-lookup"><span data-stu-id="610b4-157">int – any valid JSON integer</span></span>
* <span data-ttu-id="610b4-158">bool: cualquier booleano JSON válido</span><span class="sxs-lookup"><span data-stu-id="610b4-158">bool – any valid JSON Boolean</span></span>
* <span data-ttu-id="610b4-159">array: cualquier matriz JSON válida</span><span class="sxs-lookup"><span data-stu-id="610b4-159">array – any valid JSON array</span></span>

## <a name="artifact-expressions-and-functions"></a><span data-ttu-id="610b4-160">Expresiones y funciones de artefacto</span><span class="sxs-lookup"><span data-stu-id="610b4-160">Artifact expressions and functions</span></span>
<span data-ttu-id="610b4-161">Puede utilizar la expresión y artefactos de funciones tooconstruct Hola el comando de instalación.</span><span class="sxs-lookup"><span data-stu-id="610b4-161">You can use expression and functions tooconstruct hello artifact install command.</span></span>
<span data-ttu-id="610b4-162">Las expresiones se incluyen entre corchetes ([y]) y se evalúan cuando se instala el artefacto de Hola.</span><span class="sxs-lookup"><span data-stu-id="610b4-162">Expressions are enclosed with brackets ([ and ]), and are evaluated when hello artifact is installed.</span></span> <span data-ttu-id="610b4-163">Pueden aparecer expresiones en cualquier lugar de un valor de cadena JSON y devolver siempre otro valor JSON.</span><span class="sxs-lookup"><span data-stu-id="610b4-163">Expressions can appear anywhere in a JSON string value and always return another JSON value.</span></span> <span data-ttu-id="610b4-164">Si necesita una cadena literal que se inicia con un corchete de cierre de toouse [, debe usar dos corchetes [[.</span><span class="sxs-lookup"><span data-stu-id="610b4-164">If you need toouse a literal string that starts with a bracket [, you must use two brackets [[.</span></span>
<span data-ttu-id="610b4-165">Por lo general, se usan expresiones con funciones tooconstruct un valor.</span><span class="sxs-lookup"><span data-stu-id="610b4-165">Typically, you use expressions with functions tooconstruct a value.</span></span> <span data-ttu-id="610b4-166">Al igual que en JavaScript, las llamadas de función tienen el formato functionName(arg1,arg2,arg3).</span><span class="sxs-lookup"><span data-stu-id="610b4-166">Just like in JavaScript, function calls are formatted as functionName(arg1,arg2,arg3).</span></span>

<span data-ttu-id="610b4-167">Hello siguiente lista muestra funciones comunes:</span><span class="sxs-lookup"><span data-stu-id="610b4-167">hello following list shows common functions:</span></span>

* <span data-ttu-id="610b4-168">Parameters(ParameterName) - devuelve un valor de parámetro que se proporciona cuando se ejecuta el comando de artefacto de Hola.</span><span class="sxs-lookup"><span data-stu-id="610b4-168">parameters(parameterName) - Returns a parameter value that is provided when hello artifact command is run.</span></span>
* <span data-ttu-id="610b4-169">concat(arg1,arg2,arg3,…): combina varios valores de cadena.</span><span class="sxs-lookup"><span data-stu-id="610b4-169">concat(arg1,arg2,arg3, …..) -     Combines multiple string values.</span></span> <span data-ttu-id="610b4-170">Esta función puede tomar cualquier número de argumentos.</span><span class="sxs-lookup"><span data-stu-id="610b4-170">This function can take any number of arguments.</span></span>

<span data-ttu-id="610b4-171">Hola siguiente ejemplo se muestra cómo tooconstruct toouse un valor de expresión y funciones:</span><span class="sxs-lookup"><span data-stu-id="610b4-171">hello following example shows how toouse expression and functions tooconstruct a value:</span></span>

    runCommand": {
         "commandToExecute": "[concat('powershell.exe -ExecutionPolicy bypass \"& ./startChocolatey.ps1'
    , ' -RawPackagesList ', parameters('packages')
    , ' -Username ', parameters('installUsername')
    , ' -Password ', parameters('installPassword'))]"
    }

## <a name="create-a-custom-artifact"></a><span data-ttu-id="610b4-172">Creación de un artefacto personalizado</span><span class="sxs-lookup"><span data-stu-id="610b4-172">Create a custom artifact</span></span>
<span data-ttu-id="610b4-173">Cree su artefacto personalizado siguiendo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="610b4-173">Create your custom artifact by following these steps:</span></span>

1. <span data-ttu-id="610b4-174">Instalación de un editor de JSON - necesita un toowork de editor de JSON con archivos de definición de artefacto.</span><span class="sxs-lookup"><span data-stu-id="610b4-174">Install a JSON editor - You need a JSON editor toowork with artifact definition files.</span></span> <span data-ttu-id="610b4-175">Se recomienda usar el [código de Visual Studio](https://code.visualstudio.com/), que está disponible para Windows, Linux y OS X.</span><span class="sxs-lookup"><span data-stu-id="610b4-175">We recommend using [Visual Studio Code](https://code.visualstudio.com/), which is available for Windows, Linux and OS X.</span></span>
2. <span data-ttu-id="610b4-176">Get un artifactfile.json de ejemplo - desprotección artefactos Hola creado por equipo de laboratorios de desarrollo y pruebas de Azure en nuestro [repositorio de GitHub](https://github.com/Azure/azure-devtestlab), donde hemos creado una biblioteca enriquecida de artefactos que le ayudarán a crearán sus propios artefactos.</span><span class="sxs-lookup"><span data-stu-id="610b4-176">Get a sample artifactfile.json - Check out hello artifacts created by Azure DevTest Labs team at our [GitHub repository](https://github.com/Azure/azure-devtestlab), where we have created a rich library of artifacts that help you create your own artifacts.</span></span> <span data-ttu-id="610b4-177">Descargar un archivo de definición de artefacto y realice cambios tooit toocreate sus propios artefactos.</span><span class="sxs-lookup"><span data-stu-id="610b4-177">Download an artifact definition file and make changes tooit toocreate your own artifacts.</span></span>
3. <span data-ttu-id="610b4-178">Asegúrese de usar de IntelliSense: aproveche IntelliSense toosee elementos válidos que pueden ser tooconstruct usa un archivo de definición de artefacto.</span><span class="sxs-lookup"><span data-stu-id="610b4-178">Make use of IntelliSense - Leverage IntelliSense toosee valid elements that can be used tooconstruct an artifact definition file.</span></span> <span data-ttu-id="610b4-179">También puede ver Hola distintas opciones para los valores de un elemento.</span><span class="sxs-lookup"><span data-stu-id="610b4-179">You can also see hello different options for values of an element.</span></span> <span data-ttu-id="610b4-180">Por ejemplo, la presentación del IntelliSense Hola dos opciones de Windows o Linux al editar hello **targetOsType** elemento.</span><span class="sxs-lookup"><span data-stu-id="610b4-180">For example, IntelliSense show you hello two choices of Windows or Linux when editing hello **targetOsType** element.</span></span>
4. <span data-ttu-id="610b4-181">Artefacto de Hola de tienda en un [repositorio de git](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="610b4-181">Store hello artifact in a [git repository](devtest-lab-add-artifact-repo.md).</span></span>
   
   1. <span data-ttu-id="610b4-182">Cree un directorio independiente para cada artefacto donde el nombre del directorio de hello es Hola igual como nombre del artefacto Hola.</span><span class="sxs-lookup"><span data-stu-id="610b4-182">Create a separate directory for each artifact where hello directory name is hello same as hello artifact name.</span></span>
   2. <span data-ttu-id="610b4-183">Almacenar archivo de definición de artefacto de hello (artifactfile.json) en el directorio de hello creado.</span><span class="sxs-lookup"><span data-stu-id="610b4-183">Store hello artifact definition file (artifactfile.json) in hello directory you created.</span></span>
   3. <span data-ttu-id="610b4-184">Comando de instalación de las secuencias de comandos de Hola de almacén que se hace referencia de artefacto de Hola.</span><span class="sxs-lookup"><span data-stu-id="610b4-184">Store hello scripts that are referenced from hello artifact install command.</span></span>
      
      <span data-ttu-id="610b4-185">Este es un ejemplo del aspecto que tendrá una carpeta de artefacto:</span><span class="sxs-lookup"><span data-stu-id="610b4-185">Here is an example of how an artifact folder might look:</span></span>
      
      ![Ejemplo de repositorio de Git de artefacto](./media/devtest-lab-artifact-author/git-repo.png)
5. <span data-ttu-id="610b4-187">Agregar el laboratorio de toohello de repositorio de artefactos de hello: consulte el artículo toohello, [agregar un repositorio Git de artefactos y plantillas de](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="610b4-187">Add hello artifacts repository toohello lab - Refer toohello article, [Add a Git repository for artifacts and templates](devtest-lab-add-artifact-repo.md).</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-articles"></a><span data-ttu-id="610b4-188">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="610b4-188">Related articles</span></span>
* [<span data-ttu-id="610b4-189">¿Cómo toodiagnose errores de artefactos en los laboratorios de desarrollo y pruebas</span><span class="sxs-lookup"><span data-stu-id="610b4-189">How toodiagnose artifact failures in DevTest Labs</span></span>](devtest-lab-troubleshoot-artifact-failure.md)
* [<span data-ttu-id="610b4-190">Unirse a un dominio de Active Directory mediante una plantilla de administrador de recursos en los laboratorios de desarrollo y pruebas de Azure tooexisting VM</span><span class="sxs-lookup"><span data-stu-id="610b4-190">Join a VM tooexisting AD Domain using a resource manager template in Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a><span data-ttu-id="610b4-191">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="610b4-191">Next steps</span></span>
* <span data-ttu-id="610b4-192">Obtenga información acerca de cómo demasiado[agregar un laboratorio de tooa repositorio de Git artefacto](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="610b4-192">Learn how too[add a Git artifact repository tooa lab](devtest-lab-add-artifact-repo.md).</span></span>

